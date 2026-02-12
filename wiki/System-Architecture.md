# System Architecture

This page explains how Commutr is structured internally, how components interact, and why we made specific design decisions.

## High-Level Overview

Commutr follows a layered architecture with clear separation of concerns:

```
┌─────────────────────────────────────────────────────────┐
│                    CLIENT LAYER                          │
│  ┌──────────────┐              ┌──────────────┐        │
│  │  Web Client  │              │ Mobile Client │        │
│  │   (React)    │              │  (Future)     │        │
│  └──────────────┘              └──────────────┘        │
└─────────────────────────────────────────────────────────┘
                         ↓ HTTPS
┌─────────────────────────────────────────────────────────┐
│                     API LAYER                            │
│              ┌──────────────────┐                       │
│              │   API Gateway    │                       │
│              │   (Express.js)   │                       │
│              └──────────────────┘                       │
└─────────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────────┐
│                  APPLICATION LAYER                       │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐ │
│  │    Route     │  │     Fare     │  │Accessibility │ │
│  │   Planner    │  │  Calculator  │  │   Analyzer   │ │
│  └──────────────┘  └──────────────┘  └──────────────┘ │
│  ┌──────────────┐  ┌──────────────┐                   │
│  │   Business   │  │  Navigation  │                   │
│  │   Registry   │  │    Engine    │                   │
│  └──────────────┘  └──────────────┘                   │
└─────────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────────┐
│                AI & INTELLIGENCE LAYER                   │
│              ┌──────────────────┐                       │
│              │  Route Reasoning │                       │
│              │   (Python/LLM)   │                       │
│              └──────────────────┘                       │
└─────────────────────────────────────────────────────────┘
                         ↓
┌─────────────────────────────────────────────────────────┐
│                     DATA LAYER                           │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐ │
│  │  PostgreSQL  │  │    PostGIS   │  │    Redis     │ │
│  │ (Transport)  │  │  (Location)  │  │   (Cache)    │ │
│  └──────────────┘  └──────────────┘  └──────────────┘ │
└─────────────────────────────────────────────────────────┘
```

## Component Breakdown

### 1. Client Layer

**Responsibility**: User interface and interaction

**Components**:
- **Web Client**: React application for desktop and mobile browsers
- **Mobile Client** (planned): Native iOS/Android apps

**Key Features**:
- Location input with autocomplete
- Interactive route visualization
- Accessibility preference selection
- Real-time navigation instructions

**Technology**: React, TypeScript, Tailwind CSS, Mapbox

### 2. API Layer

**Responsibility**: Request routing, authentication, and validation

**Components**:
- **API Gateway**: Express.js server handling all client requests

**Key Features**:
- RESTful endpoints for route planning, business registration
- Input validation before processing
- Rate limiting to prevent abuse
- Error handling and logging

**Endpoints**:
```
POST /api/routes/search       - Find routes
GET  /api/routes/:id          - Get route details
POST /api/businesses/register - Register business
GET  /api/businesses/nearby   - Find businesses near route
POST /api/navigation/generate - Generate turn-by-turn instructions
```

**Technology**: Node.js, Express.js

### 3. Application Layer

**Responsibility**: Core business logic

#### Route Planner

**What it does**:
- Validates source and destination locations
- Queries transport data for available routes
- Evaluates multiple route options
- Selects optimal route based on user preferences

**Key algorithms**:
- Dijkstra's algorithm for shortest path
- A* search for faster pathfinding
- Multi-criteria optimization (cost + accessibility)

**Inputs**: Source, destination, preferences (cost priority, accessibility requirements)

**Outputs**: Ranked list of routes with complete details

#### Fare Calculator

**What it does**:
- Computes total fare for each route
- Breaks down costs by segment
- Handles zone-based pricing
- Calculates transfer fees

**Inputs**: Route with transport segments

**Outputs**: Fare breakdown with total cost

#### Accessibility Analyzer

**What it does**:
- Evaluates physical accessibility of routes
- Counts stairs, checks elevator availability
- Measures walking distances
- Filters routes based on accessibility requirements

**Inputs**: Route segments, user accessibility requirements

**Outputs**: Accessibility summary, pass/fail for requirements

#### Business Registry

**What it does**:
- Manages business registration and lifecycle
- Validates business information
- Processes listing fee payments
- Finds businesses near routes (proximity-based only)

**Key principle**: Businesses are ordered by distance from route, never by payment amount

**Inputs**: Business registration data, route coordinates

**Outputs**: List of nearby businesses ordered by proximity

#### Navigation Engine

**What it does**:
- Generates step-by-step instructions from route data
- Formats instructions for text and voice output
- Includes timing, directions, and transfer information

**Inputs**: Selected route with segments

**Outputs**: Sequential navigation instructions in text and voice formats

### 4. AI & Intelligence Layer

**Responsibility**: Natural language understanding and route reasoning

**Components**:
- **Route Reasoning Engine**: Python service using LLMs

**What it does**:
- Understands natural language queries ("cheapest way to downtown")
- Explains route choices in plain language
- Provides multilingual support
- Handles ambiguous location names

**Important**: AI is used for understanding and explanation, NOT for core route calculation. Route algorithms are deterministic and testable.

**Technology**: Python, FastAPI, LLM APIs

### 5. Data Layer

**Responsibility**: Data storage and retrieval

#### PostgreSQL
- Stores transport routes, schedules, fares
- Stores business listings
- Stores user preferences (if logged in)
- ACID compliance ensures data integrity

#### PostGIS
- Spatial extension for PostgreSQL
- Enables geographic queries (distance calculations, proximity searches)
- Indexes location data for fast lookups

#### Redis
- Caches frequently requested routes
- Stores session data
- Reduces database load
- Provides sub-millisecond response times

## Data Flow

### Route Planning Flow

1. **User submits request** (source, destination, preferences)
2. **API Gateway validates** input format
3. **Route Planner validates** locations are within service area
4. **Route Planner queries** transport data for available routes
5. **Fare Calculator computes** costs for each route
6. **Accessibility Analyzer evaluates** each route
7. **Route Planner ranks** routes by cost and accessibility
8. **Business Registry finds** nearby businesses
9. **Navigation Engine generates** instructions
10. **API Gateway returns** complete route with all details
11. **Client displays** route to user

### Business Registration Flow

1. **Shopkeeper submits** business details
2. **API Gateway validates** input format
3. **Business Registry validates** business information
4. **Business Registry creates** listing with "pending payment" status
5. **Payment processor** handles listing fee
6. **Business Registry activates** listing on successful payment
7. **API Gateway returns** confirmation

## Scalability Considerations

### Horizontal Scaling

- **API Gateway**: Multiple instances behind load balancer
- **Application Services**: Stateless, can run multiple instances
- **Database**: Read replicas for query load distribution

### Caching Strategy

- **Route Cache**: Store popular routes in Redis (1 hour TTL)
- **Business Cache**: Cache business listings by location (24 hour TTL)
- **Transport Data Cache**: Cache schedules and fares (refresh every 15 minutes)

### Database Optimization

- **Indexes**: Location-based indexes on business listings
- **Partitioning**: Partition transport data by date
- **Connection Pooling**: Reuse database connections

### Performance Targets

- Route calculation: < 2 seconds for 95th percentile
- API response time: < 500ms for cached routes
- Database queries: < 100ms for indexed lookups

## Security Considerations

### Input Validation

- Validate all user inputs before processing
- Sanitize location data to prevent injection attacks
- Rate limit API requests to prevent abuse

### Authentication

- API keys for business registration
- JWT tokens for user sessions (future)
- OAuth for third-party integrations (future)

### Data Protection

- HTTPS for all client-server communication
- Encrypted database connections
- No storage of sensitive payment information (handled by payment processor)

## Monitoring & Observability

### Logging

- Structured JSON logs for all requests
- Error tracking with stack traces
- Performance metrics (response times, query times)

### Metrics

- Request count by endpoint
- Error rate by component
- Cache hit/miss ratio
- Database query performance

### Alerts

- API error rate > 5%
- Response time > 5 seconds
- Database connection failures
- Cache unavailability

## Design Principles

### 1. Modularity

Each component has a single, well-defined responsibility. Components communicate through clear interfaces. This makes the system easier to understand, test, and modify.

### 2. Testability

Business logic is separated from infrastructure. Components can be tested independently with mocked dependencies. Property-based tests verify correctness across all inputs.

### 3. Fail-Safe Defaults

When external services fail, the system degrades gracefully:
- If transport API is down, use cached data
- If LLM is unavailable, fall back to template-based responses
- If Redis is down, query database directly (slower but functional)

### 4. Explicit Over Implicit

Configuration is explicit and documented. Data flows are clear and traceable. Error messages are specific and actionable.

## Future Architecture Changes

### Planned Improvements

1. **Event-Driven Architecture**: Use message queues for async processing
2. **Microservices**: Split application layer into independent services
3. **GraphQL Gateway**: Add GraphQL alongside REST for complex queries
4. **Real-Time Updates**: WebSocket connections for live route updates

### Not Planned

- **Blockchain**: No use case for distributed ledger
- **Serverless**: Cold start latency doesn't fit our needs
- **NoSQL**: PostgreSQL meets our requirements

---

*Questions about architecture? Open a discussion on GitHub.*
