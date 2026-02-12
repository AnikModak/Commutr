# Repository Structure

This page explains the organization of the Commutr codebase and where to find things.

## Top-Level Structure

```
commutr/
├── .github/              # GitHub-specific files
├── .kiro/                # Project specifications and diagrams
├── src/                  # Source code
├── tests/                # Test files
├── public/               # Static assets
├── docs/                 # Additional documentation
├── scripts/              # Build and deployment scripts
├── .env.example          # Environment variable template
├── .gitignore            # Git ignore rules
├── package.json          # Node.js dependencies
├── tsconfig.json         # TypeScript configuration
├── README.md             # Project overview
└── LICENSE               # MIT License
```

## Detailed Breakdown

### `.github/`

GitHub-specific configuration and workflows.

```
.github/
├── workflows/            # GitHub Actions CI/CD
│   ├── test.yml         # Run tests on PR
│   ├── lint.yml         # Code style checks
│   └── deploy.yml       # Deployment pipeline
├── ISSUE_TEMPLATE/      # Issue templates
│   ├── bug_report.md
│   └── feature_request.md
└── PULL_REQUEST_TEMPLATE.md
```

**Purpose**: Automate testing, linting, and deployment. Provide templates for consistent issue reporting.

### `.kiro/`

Project specifications, design documents, and diagrams.

```
.kiro/
├── specs/
│   └── commutr/
│       ├── requirements.md          # User stories and acceptance criteria
│       ├── design.md                # System design and architecture
│       ├── tasks.md                 # Implementation task list
│       ├── system-architecture.jpg  # Architecture diagram
│       ├── process-flow.jpg         # Process flow diagram
│       └── *.dot                    # Graphviz source files
└── settings/
    └── mcp.json                     # MCP server configuration
```

**Purpose**: Document requirements, design decisions, and system architecture. These files guide development and serve as reference documentation.

### `src/`

All application source code.

```
src/
├── client/               # Frontend code
│   ├── components/      # React components
│   │   ├── common/     # Reusable UI components
│   │   ├── route/      # Route planning components
│   │   ├── business/   # Business listing components
│   │   └── navigation/ # Navigation components
│   ├── pages/          # Page-level components
│   ├── hooks/          # Custom React hooks
│   ├── utils/          # Client-side utilities
│   ├── styles/         # Global styles
│   └── App.tsx         # Root component
│
├── server/              # Backend code
│   ├── api/            # API routes
│   │   ├── routes.ts   # Route planning endpoints
│   │   ├── businesses.ts # Business endpoints
│   │   └── navigation.ts # Navigation endpoints
│   ├── services/       # Business logic
│   │   ├── route-planner/
│   │   │   ├── index.ts
│   │   │   ├── validator.ts
│   │   │   ├── finder.ts
│   │   │   └── selector.ts
│   │   ├── fare-calculator/
│   │   │   ├── index.ts
│   │   │   └── calculator.ts
│   │   ├── accessibility-analyzer/
│   │   │   ├── index.ts
│   │   │   └── analyzer.ts
│   │   ├── business-registry/
│   │   │   ├── index.ts
│   │   │   ├── registration.ts
│   │   │   ├── payment.ts
│   │   │   └── proximity.ts
│   │   └── navigation-engine/
│   │       ├── index.ts
│   │       └── generator.ts
│   ├── middleware/     # Express middleware
│   │   ├── auth.ts
│   │   ├── validation.ts
│   │   └── error-handler.ts
│   └── server.ts       # Express app setup
│
├── ai/                  # AI/Intelligence layer
│   ├── reasoning/      # Route reasoning logic
│   ├── nlp/            # Natural language processing
│   └── api.py          # FastAPI server
│
├── models/              # Data models (shared)
│   ├── location.ts
│   ├── route.ts
│   ├── business.ts
│   └── navigation.ts
│
├── database/            # Database code
│   ├── migrations/     # Database migrations
│   ├── seeds/          # Seed data
│   ├── connection.ts   # Database connection
│   └── queries/        # SQL queries
│       ├── routes.ts
│       └── businesses.ts
│
├── config/              # Configuration
│   ├── database.ts
│   ├── redis.ts
│   └── aws.ts
│
└── utils/               # Shared utilities
    ├── logger.ts
    ├── validation.ts
    └── errors.ts
```

**Key Directories**:

- **`client/`**: All frontend React code
- **`server/`**: Backend API and business logic
- **`ai/`**: Python-based AI services
- **`models/`**: TypeScript interfaces shared between client and server
- **`database/`**: Database schema, migrations, and queries
- **`config/`**: Configuration for external services

### `tests/`

All test files, mirroring the `src/` structure.

```
tests/
├── unit/                # Unit tests
│   ├── services/
│   │   ├── route-planner.test.ts
│   │   ├── fare-calculator.test.ts
│   │   ├── accessibility-analyzer.test.ts
│   │   ├── business-registry.test.ts
│   │   └── navigation-engine.test.ts
│   └── utils/
│       └── validation.test.ts
│
├── integration/         # Integration tests
│   ├── api/
│   │   ├── routes.test.ts
│   │   └── businesses.test.ts
│   └── database/
│       └── queries.test.ts
│
├── property/            # Property-based tests
│   ├── route-planning.property.test.ts
│   ├── fare-calculation.property.test.ts
│   ├── accessibility.property.test.ts
│   └── business-registry.property.test.ts
│
├── e2e/                 # End-to-end tests
│   ├── route-search.e2e.test.ts
│   └── business-registration.e2e.test.ts
│
└── fixtures/            # Test data
    ├── routes.json
    ├── businesses.json
    └── locations.json
```

**Test Organization**:

- **Unit tests**: Test individual functions and classes in isolation
- **Integration tests**: Test component interactions
- **Property tests**: Verify correctness properties with random inputs
- **E2E tests**: Test complete user workflows

### `public/`

Static assets served directly to clients.

```
public/
├── images/              # Images and icons
├── fonts/               # Custom fonts
├── favicon.ico          # Site favicon
└── index.html           # HTML template
```

### `docs/`

Additional documentation beyond the Wiki.

```
docs/
├── api/                 # API documentation
│   ├── routes.md
│   ├── businesses.md
│   └── navigation.md
├── algorithms/          # Algorithm explanations
│   ├── route-finding.md
│   └── cost-optimization.md
└── deployment/          # Deployment guides
    ├── aws.md
    └── docker.md
```

### `scripts/`

Build, deployment, and utility scripts.

```
scripts/
├── build.sh             # Production build
├── deploy.sh            # Deployment script
├── seed-db.ts           # Seed database with test data
├── migrate-db.ts        # Run database migrations
└── generate-diagrams.sh # Generate architecture diagrams
```

## Configuration Files

### `package.json`

Node.js project configuration and dependencies.

**Key sections**:
- `dependencies`: Production dependencies
- `devDependencies`: Development tools
- `scripts`: Common commands (test, build, dev)

### `tsconfig.json`

TypeScript compiler configuration.

**Key settings**:
- `strict: true`: Enable all strict type checking
- `target: "ES2020"`: Compile to ES2020
- `module: "commonjs"`: Use CommonJS modules

### `.env.example`

Template for environment variables.

**Required variables**:
```
# API Configuration
API_BASE_URL=http://localhost:3000
API_KEY=your_api_key_here

# Database
DATABASE_URL=postgresql://user:password@localhost:5432/commutr

# Redis
REDIS_URL=redis://localhost:6379

# Transport APIs
TRANSPORT_API_KEY=your_transport_api_key
MAPS_API_KEY=your_maps_api_key

# Business Listings
LISTING_FEE_AMOUNT=50.00
PROXIMITY_THRESHOLD_METERS=500

# AI Services
LLM_API_KEY=your_llm_api_key
LLM_MODEL=gpt-4
```

## Where to Find Things

### Adding a New Feature

1. **Define requirements**: Add to `.kiro/specs/commutr/requirements.md`
2. **Design component**: Update `.kiro/specs/commutr/design.md`
3. **Implement service**: Add to `src/server/services/`
4. **Add API endpoint**: Add to `src/server/api/`
5. **Create UI**: Add to `src/client/components/`
6. **Write tests**: Add to `tests/unit/` and `tests/property/`

### Fixing a Bug

1. **Reproduce**: Write a failing test in `tests/`
2. **Fix**: Modify code in `src/`
3. **Verify**: Ensure test passes
4. **Document**: Update relevant docs in `docs/` if needed

### Updating Configuration

- **Database**: Modify `src/config/database.ts`
- **API**: Modify `src/server/server.ts`
- **Environment**: Update `.env.example` and document in Wiki

### Adding Dependencies

1. **Install**: `npm install <package>`
2. **Document**: Explain choice in [Tech Stack & Tools](Tech-Stack-&-Tools)
3. **Configure**: Add configuration to `src/config/` if needed

## Future Extensions

### Where to Add New Components

- **New transport mode**: Add to `src/server/services/route-planner/`
- **New payment provider**: Add to `src/server/services/business-registry/payment.ts`
- **New map provider**: Add to `src/client/components/common/map/`
- **New language**: Add translations to `src/client/locales/`

### Planned Directories

- `src/mobile/`: Native mobile app code (future)
- `src/workers/`: Background job processors (future)
- `src/websockets/`: Real-time update handlers (future)

---

*Can't find something? Ask in GitHub Discussions or open an issue.*
