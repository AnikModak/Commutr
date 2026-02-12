# Tech Stack & Tools

This page explains every major technology choice in Commutr and why we made it.

## Frontend

### React
**What**: JavaScript library for building user interfaces  
**Why**: 
- Component-based architecture matches our modular design philosophy
- Large ecosystem of accessibility-focused libraries
- Strong TypeScript support
- Excellent developer tools and community

### TypeScript
**What**: Typed superset of JavaScript  
**Why**:
- Catches errors at compile time, not runtime
- Makes refactoring safer as the codebase grows
- Improves code documentation through type definitions
- Better IDE support with autocomplete and inline documentation

### Tailwind CSS
**What**: Utility-first CSS framework  
**Why**:
- Rapid UI development without writing custom CSS
- Consistent design system through configuration
- Small bundle size with purging unused styles
- Easy to maintain and customize

### Mapbox
**What**: Maps and location services  
**Why**:
- Better customization than Google Maps
- Affordable pricing for open-source projects
- Excellent route visualization capabilities
- Good accessibility features for map interactions

## Backend

### Node.js
**What**: JavaScript runtime for server-side code  
**Why**:
- Same language as frontend (TypeScript/JavaScript)
- Non-blocking I/O perfect for handling multiple route requests
- Large package ecosystem (npm)
- Easy to deploy and scale

### Express.js
**What**: Minimal web framework for Node.js  
**Why**:
- Simple and unopinionated
- Extensive middleware ecosystem
- Easy to understand and debug
- Well-documented and battle-tested

### REST API
**What**: Architectural style for web services  
**Why**:
- Simple and widely understood
- Easy to test and debug
- Works with any client (web, mobile, CLI)
- Stateless design scales well

## AI & Intelligence Layer

### Python
**What**: High-level programming language  
**Why**:
- Excellent libraries for route optimization algorithms
- Strong data processing capabilities
- Easy integration with machine learning models
- Fast prototyping for complex logic

### FastAPI
**What**: Modern Python web framework  
**Why**:
- Automatic API documentation (OpenAPI/Swagger)
- Built-in data validation with Pydantic
- Async support for better performance
- Type hints improve code quality

### Large Language Models (LLM)
**What**: AI models for natural language understanding  
**Why**:
- Understand user queries in natural language ("cheapest route to downtown")
- Multilingual support without manual translation
- Explain route choices in plain language
- Handle ambiguous location names

**Note**: We use LLMs for understanding and explanation, not for core route calculation. Route algorithms are deterministic and testable.

## Data Layer

### PostgreSQL
**What**: Open-source relational database  
**Why**:
- ACID compliance ensures data integrity
- Excellent performance for complex queries
- Strong JSON support for flexible schemas
- Mature and reliable

### PostGIS
**What**: Spatial database extension for PostgreSQL  
**Why**:
- Efficient geographic queries (find businesses near route)
- Calculate distances and proximity
- Index spatial data for fast lookups
- Industry standard for location-based applications

### Redis
**What**: In-memory data store  
**Why**:
- Cache frequently requested routes
- Store session data
- Fast response times (sub-millisecond)
- Reduces load on PostgreSQL

## Cloud Infrastructure (AWS)

### EC2 (Elastic Compute Cloud)
**What**: Virtual servers in the cloud  
**Why**:
- Full control over server configuration
- Easy to scale up or down
- Pay only for what you use
- Reliable uptime

### RDS (Relational Database Service)
**What**: Managed PostgreSQL hosting  
**Why**:
- Automatic backups
- Easy scaling
- Handles maintenance and updates
- High availability with multi-AZ deployment

### S3 (Simple Storage Service)
**What**: Object storage  
**Why**:
- Store static assets (images, diagrams)
- Backup database dumps
- Cheap and durable (99.999999999% durability)
- Integrates with CloudFront for fast delivery

### CloudFront
**What**: Content delivery network (CDN)  
**Why**:
- Fast asset delivery worldwide
- Reduces latency for users
- Handles traffic spikes
- SSL/TLS encryption included

## Development Tools

### Git & GitHub
**What**: Version control and collaboration platform  
**Why**:
- Industry standard for open-source projects
- Pull request workflow for code review
- Issue tracking and project management
- GitHub Actions for CI/CD

### ESLint
**What**: JavaScript/TypeScript linter  
**Why**:
- Enforces consistent code style
- Catches common errors
- Configurable rules
- Integrates with editors

### Prettier
**What**: Code formatter  
**Why**:
- Automatic code formatting
- Eliminates style debates
- Consistent formatting across team
- Saves time in code review

### Jest
**What**: JavaScript testing framework  
**Why**:
- Fast test execution
- Built-in mocking and assertions
- Snapshot testing for UI components
- Excellent TypeScript support

### fast-check
**What**: Property-based testing library  
**Why**:
- Tests code with thousands of random inputs
- Finds edge cases humans miss
- Validates correctness properties
- Complements traditional unit tests

### Docker
**What**: Containerization platform  
**Why**:
- Consistent development environment
- Easy deployment
- Isolates dependencies
- Simplifies local setup

## Why Not Other Technologies?

### Why Not GraphQL?
REST is simpler for our use case. We don't have complex nested data requirements that would benefit from GraphQL's flexibility. REST is easier for new contributors to understand.

### Why Not MongoDB?
We need strong consistency guarantees for business listings and route data. PostgreSQL's ACID compliance and PostGIS spatial features are better suited to our needs than MongoDB's eventual consistency model.

### Why Not Kubernetes?
Our current scale doesn't justify Kubernetes complexity. EC2 with Docker is sufficient. We may revisit this as we grow, but we prefer simplicity now.

### Why Not Vue or Angular?
React has the largest ecosystem and community. More contributors are familiar with React, making onboarding easier. The choice is pragmatic, not ideological.

### Why Not Serverless (Lambda)?
Route calculation can take several seconds for complex queries. Lambda's timeout limits and cold start latency don't fit our use case well. Traditional servers give us more control.

## Technology Principles

When choosing technologies, we prioritize:

1. **Simplicity**: Prefer boring, proven technologies over cutting-edge
2. **Community**: Choose tools with large, active communities
3. **Documentation**: Good docs reduce onboarding friction
4. **Accessibility**: Tools must support building accessible applications
5. **Cost**: Open-source and affordable for a community project

## Future Considerations

Technologies we're watching but not using yet:

- **Rust**: For performance-critical route algorithms
- **WebAssembly**: For client-side route calculation
- **Temporal**: For workflow orchestration
- **Grafana**: For monitoring and observability

We'll adopt new technologies when they solve real problems, not for novelty.

---

*Have questions about our tech choices? Open an issue or discussion on GitHub.*
