# Design Document: Commutr

## Overview

Commutr is a web-based platform that provides optimal public transport route planning with integrated business discovery. The system architecture follows a modular design with clear separation between route planning, fare calculation, accessibility analysis, business management, and navigation components.

The platform serves two distinct user workflows:
1. **Commuter Workflow**: Users input source/destination, specify preferences, receive optimized routes with cost/accessibility details and nearby businesses
2. **Shopkeeper Workflow**: Business owners register, pay listing fees, and gain neutral visibility along user routes

Key design principles:
- **Neutrality**: Business listings are never prioritized based on payment
- **Accessibility-First**: All routes include comprehensive accessibility information
- **Cost Transparency**: Complete fare breakdowns for all route options
- **Modularity**: Independent components for route planning, fare calculation, accessibility analysis, and business management

## Architecture

### System Components

```
┌─────────────────────────────────────────────────────────────┐
│                      Web Application                         │
│  ┌──────────────────┐         ┌──────────────────┐         │
│  │  User Interface  │         │ Shopkeeper Panel │         │
│  └────────┬─────────┘         └────────┬─────────┘         │
│           │                             │                    │
└───────────┼─────────────────────────────┼────────────────────┘
            │                             │
┌───────────┼─────────────────────────────┼────────────────────┐
│           │      Application Layer      │                    │
│  ┌────────▼─────────┐         ┌────────▼─────────┐         │
│  │  Route Planner   │         │ Business Registry │         │
│  │                  │         │                   │         │
│  │ - Input Validator│         │ - Registration    │         │
│  │ - Route Finder   │         │ - Payment Handler │         │
│  │ - Route Selector │         │ - Proximity Search│         │
│  └────────┬─────────┘         └───────────────────┘         │
│           │                                                   │
│  ┌────────▼─────────┐  ┌──────────────┐  ┌──────────────┐  │
│  │ Fare Calculator  │  │Accessibility │  │  Navigation  │  │
│  │                  │  │  Analyzer    │  │   Engine     │  │
│  └──────────────────┘  └──────────────┘  └──────────────┘  │
└───────────────────────────────────────────────────────────────┘
            │                             │
┌───────────┼─────────────────────────────┼────────────────────┐
│           │       Data Layer            │                    │
│  ┌────────▼─────────┐         ┌────────▼─────────┐         │
│  │ Transport Data   │         │  Business Data   │         │
│  │  - Routes        │         │  - Listings      │         │
│  │  - Schedules     │         │  - Locations     │         │
│  │  - Fares         │         │  - Categories    │         │
│  │  - Accessibility │         │                  │         │
│  └──────────────────┘         └──────────────────┘         │
└───────────────────────────────────────────────────────────────┘
```

### Component Responsibilities

**Route Planner**:
- Validates user input (source, destination, preferences)
- Finds all available public transport routes
- Evaluates routes based on cost and accessibility criteria
- Selects optimal route based on user preferences
- Coordinates with Fare Calculator and Accessibility Analyzer

**Fare Calculator**:
- Computes total fare for each route
- Breaks down costs by transport segment
- Handles zone-based pricing, transfers, and special fares

**Accessibility Analyzer**:
- Evaluates physical accessibility features of routes
- Calculates walking distances, stair counts, elevator availability
- Filters routes based on user accessibility requirements
- Provides accessibility summaries for route display

**Business Registry**:
- Manages business registration and listing lifecycle
- Validates business information (name, category, location)
- Handles listing fee payments
- Performs proximity-based business searches along routes
- Ensures neutral, unbiased business ordering

**Navigation Engine**:
- Generates step-by-step instructions from route data
- Formats instructions for text and voice output
- Includes timing, directions, and transfer information

## Components and Interfaces

### Route Planner

```typescript
interface Location {
  latitude: number;
  longitude: number;
  address?: string;
}

interface RoutePreferences {
  prioritizeCost: boolean;
  accessibilityRequirements?: AccessibilityRequirements;
}

interface AccessibilityRequirements {
  maxWalkingDistance?: number; // meters
  avoidStairs: boolean;
  requireElevators: boolean;
  maxTransfers?: number;
}

interface RouteRequest {
  source: Location;
  destination: Location;
  preferences: RoutePreferences;
}

interface Route {
  id: string;
  segments: TransportSegment[];
  totalCost: number;
  totalDuration: number; // minutes
  totalWalkingDistance: number; // meters
  accessibilitySummary: AccessibilitySummary;
  nearbyBusinesses: Business[];
}

interface TransportSegment {
  mode: TransportMode;
  startLocation: Location;
  endLocation: Location;
  startTime?: string;
  endTime?: string;
  duration: number; // minutes
  cost: number;
  routeNumber?: string;
  direction?: string;
  accessibilityFeatures: AccessibilityFeature[];
}

enum TransportMode {
  BUS = "bus",
  TRAIN = "train",
  SUBWAY = "subway",
  TRAM = "tram",
  WALKING = "walking"
}

interface RoutePlanner {
  validateInput(request: RouteRequest): ValidationResult;
  findRoutes(request: RouteRequest): Route[];
  selectOptimalRoute(routes: Route[], preferences: RoutePreferences): Route;
}
```

### Fare Calculator

```typescript
interface FareBreakdown {
  segments: SegmentFare[];
  totalFare: number;
  currency: string;
}

interface SegmentFare {
  segmentId: string;
  baseFare: number;
  transferFee: number;
  zoneFee: number;
  totalSegmentFare: number;
}

interface FareCalculator {
  calculateRouteFare(route: Route): FareBreakdown;
  calculateSegmentFare(segment: TransportSegment): SegmentFare;
}
```

### Accessibility Analyzer

```typescript
interface AccessibilityFeature {
  type: AccessibilityFeatureType;
  value?: number;
  description: string;
}

enum AccessibilityFeatureType {
  STAIRS = "stairs",
  ELEVATOR = "elevator",
  RAMP = "ramp",
  WALKING_DISTANCE = "walking_distance",
  PLATFORM_GAP = "platform_gap",
  WHEELCHAIR_ACCESSIBLE = "wheelchair_accessible"
}

interface AccessibilitySummary {
  totalStairs: number;
  elevatorsAvailable: boolean;
  wheelchairAccessible: boolean;
  totalWalkingDistance: number;
  transferCount: number;
}

interface AccessibilityAnalyzer {
  analyzeRoute(route: Route): AccessibilitySummary;
  meetsRequirements(route: Route, requirements: AccessibilityRequirements): boolean;
  extractFeatures(segment: TransportSegment): AccessibilityFeature[];
}
```

### Business Registry

```typescript
interface Business {
  id: string;
  name: string;
  category: BusinessCategory;
  location: Location;
  listingStatus: ListingStatus;
  registrationDate: string;
  expirationDate: string;
}

enum BusinessCategory {
  RESTAURANT = "restaurant",
  CAFE = "cafe",
  RETAIL = "retail",
  PHARMACY = "pharmacy",
  GROCERY = "grocery",
  SERVICE = "service",
  OTHER = "other"
}

enum ListingStatus {
  ACTIVE = "active",
  INACTIVE = "inactive",
  PENDING_PAYMENT = "pending_payment",
  EXPIRED = "expired"
}

interface BusinessRegistration {
  name: string;
  category: BusinessCategory;
  location: Location;
  contactInfo?: ContactInfo;
}

interface ContactInfo {
  email?: string;
  phone?: string;
}

interface BusinessRegistry {
  registerBusiness(registration: BusinessRegistration): ValidationResult;
  processPayment(businessId: string, amount: number): PaymentResult;
  activateListing(businessId: string): void;
  findBusinessesNearRoute(route: Route, proximityThreshold: number): Business[];
  updateBusiness(businessId: string, updates: Partial<BusinessRegistration>): ValidationResult;
  getBusiness(businessId: string): Business | null;
}

interface PaymentResult {
  success: boolean;
  transactionId?: string;
  error?: string;
}
```

### Navigation Engine

```typescript
interface NavigationInstruction {
  stepNumber: number;
  instruction: string;
  mode: TransportMode;
  duration: number;
  distance?: number;
  location: Location;
}

interface NavigationOutput {
  instructions: NavigationInstruction[];
  textFormat: string;
  voiceFormat: string;
}

interface NavigationEngine {
  generateInstructions(route: Route): NavigationOutput;
  formatForText(instructions: NavigationInstruction[]): string;
  formatForVoice(instructions: NavigationInstruction[]): string;
}
```

### Validation

```typescript
interface ValidationResult {
  valid: boolean;
  errors: ValidationError[];
}

interface ValidationError {
  field: string;
  message: string;
  code: string;
}
```

## Data Models

### Core Data Structures

**Location Model**:
- Represents geographic coordinates
- Includes optional human-readable address
- Used for source, destination, stops, and business locations

**Route Model**:
- Aggregates multiple transport segments
- Contains computed totals (cost, duration, walking distance)
- Includes accessibility summary and nearby businesses
- Immutable once calculated

**Transport Segment Model**:
- Represents single leg of journey
- Contains mode-specific information (route numbers, directions)
- Includes timing and cost data
- Contains accessibility features specific to that segment

**Business Model**:
- Stores business registration information
- Tracks listing status and expiration
- Contains location for proximity searches
- Immutable business ID for tracking

### Data Persistence

**Business Listings**:
- Stored as JSON documents
- Indexed by location for proximity queries
- Indexed by status for active listing retrieval
- Include registration and expiration timestamps

**Transport Data**:
- Routes, schedules, and fares loaded from external data sources
- Cached for performance
- Refreshed periodically to maintain accuracy

**Configuration Data**:
- System settings (proximity thresholds, listing fees)
- Stored as JSON configuration files
- Validated on load

### Data Validation Rules

**Location Validation**:
- Latitude: -90 to 90
- Longitude: -180 to 180
- Coordinates must be within service area

**Business Registration Validation**:
- Name: 1-200 characters, non-empty
- Category: Must be valid BusinessCategory enum value
- Location: Must pass location validation
- Contact info: Email format validation if provided

**Route Request Validation**:
- Source and destination must be different locations
- Source and destination must pass location validation
- Preferences must contain valid accessibility requirements if specified


## Correctness Properties

*A property is a characteristic or behavior that should hold true across all valid executions of a system—essentially, a formal statement about what the system should do. Properties serve as the bridge between human-readable specifications and machine-verifiable correctness guarantees.*

### Route Planning Properties

**Property 1: Valid inputs produce routes**
*For any* valid source and destination locations within the service area, the Route_Planner should return at least one valid public transport route.
**Validates: Requirements 1.1**

**Property 2: Invalid inputs produce descriptive errors**
*For any* invalid location data (out-of-range coordinates, null values, malformed data), the Route_Planner should return a validation error with a descriptive message indicating the specific validation failure.
**Validates: Requirements 1.2, 8.1**

**Property 3: Validation precedes processing**
*For any* route request with invalid inputs, the Route_Planner should reject the request without performing route calculation or producing side effects.
**Validates: Requirements 1.4, 8.4**

### Cost Optimization Properties

**Property 4: Lowest cost route selection**
*For any* set of routes with different total costs, when cost is prioritized, the Route_Planner should select the route with the minimum total fare.
**Validates: Requirements 2.2**

**Property 5: Complete fare breakdown**
*For any* calculated route, the Fare_Calculator should provide a fare breakdown containing entries for each transport segment, with each entry including base fare, transfer fees, and zone charges.
**Validates: Requirements 2.1, 2.3, 2.4**

### Accessibility Properties

**Property 6: Complete accessibility information**
*For any* route, the Accessibility_Analyzer should provide accessibility information including walking distances, stair counts, elevator availability, and transfer requirements for all segments.
**Validates: Requirements 3.1, 3.3**

**Property 7: Accessibility filtering**
*For any* set of routes and user-specified accessibility requirements, all returned routes should meet those requirements (no routes violating the constraints should be included).
**Validates: Requirements 3.2, 3.4**

### Navigation Properties

**Property 8: Sequential instruction generation**
*For any* route, the Navigation_Engine should generate instructions with sequential step numbers (1, 2, 3, ..., n) with no gaps or duplicates.
**Validates: Requirements 4.1**

**Property 9: Complete instruction content**
*For any* route, each navigation instruction should include transport mode, direction, location, and duration information.
**Validates: Requirements 4.2**

**Property 10: Dual format output**
*For any* route, the Navigation_Engine should produce navigation output containing both text format and voice format representations.
**Validates: Requirements 4.3**

**Property 11: Transfer indication**
*For any* route containing multiple transport segments with different modes, the navigation instructions should include explicit transfer steps with walking directions.
**Validates: Requirements 4.4**

### Business Registry Properties

**Property 12: Valid registration creates listing**
*For any* valid business registration (containing name, category, and location), the Business_Registry should create a new business listing with a unique ID.
**Validates: Requirements 5.1**

**Property 13: Incomplete registration rejection**
*For any* business registration missing required fields (name, category, or location), the Business_Registry should reject the registration and return validation errors indicating the specific missing fields.
**Validates: Requirements 5.2, 5.3**

**Property 14: Payment activates listing**
*For any* business listing in pending payment status, successful payment processing should transition the listing to active status.
**Validates: Requirements 5.4**

**Property 15: Proximity-based ordering only**
*For any* route and set of businesses, the returned businesses should be ordered by distance from the route in ascending order, regardless of payment amounts or registration dates.
**Validates: Requirements 6.1, 6.2**

**Property 16: Proximity threshold filtering**
*For any* route and proximity threshold, all businesses within the threshold distance should be included in results, and all businesses beyond the threshold should be excluded.
**Validates: Requirements 6.3**

### Route Display Properties

**Property 17: Complete route output**
*For any* calculated route, the route result should include all transport segments, total travel time, total cost, accessibility summary, and nearby registered businesses.
**Validates: Requirements 7.1, 7.2, 7.3**

### Business Management Properties

**Property 18: Update validation and persistence**
*For any* valid business update (name, category, or location change), the Business_Registry should validate the update, persist the changes, and return the updated business when retrieved.
**Validates: Requirements 9.1, 9.2, 9.3**

**Property 19: Expiration deactivation**
*For any* business listing with an expiration date in the past, the listing status should be inactive or expired.
**Validates: Requirements 9.4**

### Data Persistence Properties

**Property 20: Immediate persistence and retrieval**
*For any* newly created business listing, retrieving the business by ID immediately after creation should return the same business data.
**Validates: Requirements 10.1**

**Property 21: Configuration persistence**
*For any* system configuration change, the configuration should be retrievable after system restart with the same values.
**Validates: Requirements 10.2**

**Property 22: Serialization round-trip**
*For any* valid business listing object, serializing to JSON then deserializing should produce an equivalent object with the same field values.
**Validates: Requirements 10.3, 10.4**

## Error Handling

### Error Categories

**Validation Errors**:
- Invalid location coordinates (out of range)
- Missing required fields
- Malformed input data
- Invalid enum values

**Business Logic Errors**:
- No routes available between locations
- Locations outside service area
- No businesses within proximity threshold

**System Errors**:
- External data source unavailable
- Database connection failure
- Serialization/deserialization failure

### Error Response Format

All errors should follow a consistent structure:

```typescript
interface ErrorResponse {
  success: false;
  errors: ValidationError[];
  message: string;
  code: string;
}
```

### Error Handling Strategies

**Input Validation**:
- Validate all inputs before processing
- Return specific error messages indicating which field failed validation
- Include validation rules in error messages when helpful

**Graceful Degradation**:
- When external data sources are unavailable, return clear error messages
- Suggest alternative actions when no routes are found
- Maintain system stability even when components fail

**Error Logging**:
- Log all errors with context (user input, timestamp, component)
- Include stack traces for system errors
- Track error patterns for monitoring

## Testing Strategy

### Dual Testing Approach

Commutr will use both unit testing and property-based testing to ensure comprehensive coverage:

**Unit Tests**:
- Specific examples demonstrating correct behavior
- Edge cases (empty results, boundary values, single-segment routes)
- Error conditions (invalid inputs, missing data, external failures)
- Integration points between components

**Property-Based Tests**:
- Universal properties that hold for all inputs
- Comprehensive input coverage through randomization
- Validation of correctness properties defined in this document

### Property-Based Testing Configuration

**Library Selection**:
- TypeScript/JavaScript: fast-check
- Minimum 100 iterations per property test
- Each test tagged with feature name and property number

**Test Tagging Format**:
```typescript
// Feature: public-transport-helper, Property 1: Valid inputs produce routes
```

**Property Test Implementation**:
- Each correctness property maps to exactly one property-based test
- Tests generate random valid inputs within constraints
- Tests verify the property holds for all generated inputs

### Test Coverage Goals

**Route Planning**:
- Unit tests: Specific route examples, edge cases (no routes, single route)
- Property tests: Properties 1-3 (valid inputs, invalid inputs, validation order)

**Cost Optimization**:
- Unit tests: Specific fare calculations, edge cases (free routes, complex fares)
- Property tests: Properties 4-5 (cost selection, fare breakdown)

**Accessibility**:
- Unit tests: Specific accessibility scenarios, edge cases (no accessibility data)
- Property tests: Properties 6-7 (accessibility information, filtering)

**Navigation**:
- Unit tests: Specific instruction examples, edge cases (single segment, many transfers)
- Property tests: Properties 8-11 (sequencing, content, formats, transfers)

**Business Registry**:
- Unit tests: Specific registration scenarios, payment flows
- Property tests: Properties 12-16, 18-20 (registration, ordering, updates, persistence)

**Data Persistence**:
- Unit tests: Specific serialization examples
- Property tests: Properties 20-22 (persistence, round-trip)

### Testing Best Practices

**Balance**:
- Avoid writing too many unit tests for cases covered by properties
- Focus unit tests on specific examples and integration points
- Use property tests for comprehensive input coverage

**Isolation**:
- Test components independently with mocked dependencies
- Use integration tests for component interactions
- Separate business logic from external dependencies

**Maintainability**:
- Keep tests simple and focused
- Use descriptive test names referencing requirements
- Update tests when requirements change
