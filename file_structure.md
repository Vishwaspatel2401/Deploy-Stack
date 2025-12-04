# DeployStack - Project File Structure

This document outlines the complete file structure for the DeployStack project. This structure will be implemented as the project progresses.

---

## 📁 Complete Project Structure

```
DeployStack/
│
├── app/                                    # Main application package
│   ├── __init__.py
│   │
│   ├── main.py                            # FastAPI application entry point
│   │
│   ├── config/                            # Configuration management
│   │   ├── __init__.py
│   │   └── settings.py                   # Application settings & environment variables
│   │
│   ├── models/                            # Pydantic data models
│   │   ├── __init__.py
│   │   ├── deployment.py                 # Deployment models (Deployment, DeploymentStatus, etc.)
│   │   ├── build.py                      # Build models (Build, BuildStatus, etc.)
│   │   └── github_deploy.py             # GitHub deployment request/response models
│   │
│   ├── database/                         # Database layer
│   │   ├── __init__.py
│   │   ├── connection.py                 # Database connection & session management
│   │   └── models.py                     # SQLAlchemy ORM models
│   │
│   ├── repositories/                     # Repository pattern implementation
│   │   ├── __init__.py
│   │   ├── base_repository.py            # Abstract base repository
│   │   ├── deployment_repository.py      # Deployment data access
│   │   └── build_repository.py           # Build data access
│   │
│   ├── services/                         # Business logic layer
│   │   ├── __init__.py
│   │   ├── deployment_service.py         # Deployment business logic
│   │   ├── build_service.py              # Build business logic
│   │   ├── cache_service.py              # Redis caching service
│   │   ├── github_service.py             # GitHub API integration
│   │   ├── s3_service.py                 # AWS S3 integration
│   │   └── external_service.py          # Base class for external services
│   │
│   ├── strategies/                       # Strategy pattern for builds
│   │   ├── __init__.py
│   │   ├── base_strategy.py              # Abstract build strategy
│   │   ├── static_strategy.py            # Static HTML/CSS/JS build strategy
│   │   ├── react_strategy.py             # React build strategy
│   │   └── nextjs_strategy.py            # Next.js build strategy
│   │
│   ├── factories/                        # Factory pattern
│   │   ├── __init__.py
│   │   └── build_factory.py              # Factory for creating build strategies
│   │
│   ├── events/                           # Event-driven architecture
│   │   ├── __init__.py
│   │   ├── event_types.py                # Event class definitions
│   │   └── event_bus.py                  # Event bus implementation
│   │
│   ├── listeners/                        # Event listeners
│   │   ├── __init__.py
│   │   ├── deployment_listener.py        # Deployment event handlers
│   │   └── build_listener.py             # Build event handlers
│   │
│   ├── queues/                           # Message queue system
│   │   ├── __init__.py
│   │   ├── build_task.py                 # Build task model
│   │   ├── queue_manager.py              # Queue management (Redis-based)
│   │   └── workers/                      # Background workers
│   │       ├── __init__.py
│   │       └── build_worker.py           # Build worker (consumer)
│   │
│   ├── middleware/                       # Middleware components
│   │   ├── __init__.py
│   │   ├── rate_limiter.py               # Rate limiting middleware
│   │   └── circuit_breaker.py            # Circuit breaker pattern
│   │
│   ├── routers/                          # API route modules
│   │   ├── __init__.py
│   │   ├── deploy.py                     # Deployment routes
│   │   ├── build.py                      # Build routes
│   │   ├── health.py                     # Health check routes
│   │   └── queue.py                      # Queue management routes
│   │
│   ├── utils/                            # Utility functions
│   │   ├── __init__.py
│   │   ├── logger.py                     # Structured logging setup
│   │   └── exceptions.py                 # Custom exception classes
│   │
│   ├── deployments/                      # Deployed projects storage (user projects)
│   │   └── [deployment-id]/              # Each deployment gets unique folder
│   │       └── [user-project-files]/     # User's deployed project files
│   │           # Example: index.html, assets/, styles/, scripts/ (user's frontend)
│   │           # Note: These are NOT DeployStack's frontend code
│   │           # These are the user's projects that get deployed
│   │
│   └── storage/                          # Application storage
│       ├── metadata/                     # File-based metadata (if used)
│       └── database.db                  # SQLite database (if used)
│
├── tests/                                # Test suite
│   ├── __init__.py
│   ├── conftest.py                       # Pytest configuration & fixtures
│   ├── test_deployment_service.py        # Deployment service tests
│   ├── test_build_service.py             # Build service tests
│   ├── test_repositories.py              # Repository tests
│   ├── test_services.py                  # Service layer tests
│   ├── test_middleware.py                # Middleware tests
│   ├── test_strategies.py                # Build strategy tests
│   └── test_integration.py                # Integration tests
│
├── alembic/                              # Database migrations
│   ├── env.py                            # Alembic environment
│   ├── script.py.mako                    # Migration script template
│   └── versions/                         # Migration versions
│       └── [migration_files].py
│
├── frontend/                             # Frontend application (React/Next.js)
│   ├── public/                           # Static assets
│   │   ├── favicon.ico
│   │   ├── logo.svg
│   │   └── images/
│   │
│   ├── src/                              # Source code
│   │   ├── components/                   # Reusable UI components
│   │   │   ├── common/                   # Common components
│   │   │   │   ├── Button.tsx
│   │   │   │   ├── Input.tsx
│   │   │   │   ├── Modal.tsx
│   │   │   │   ├── Card.tsx
│   │   │   │   └── LoadingSpinner.tsx
│   │   │   ├── layout/                   # Layout components
│   │   │   │   ├── Header.tsx
│   │   │   │   ├── Footer.tsx
│   │   │   │   ├── Sidebar.tsx
│   │   │   │   └── Layout.tsx
│   │   │   └── deployment/               # Deployment-specific components
│   │   │       ├── DeploymentCard.tsx
│   │   │       ├── DeploymentList.tsx
│   │   │       ├── DeploymentForm.tsx
│   │   │       └── DeploymentStatus.tsx
│   │   │
│   │   ├── pages/                        # Page components
│   │   │   ├── Home.tsx
│   │   │   ├── Dashboard.tsx
│   │   │   ├── Deployments.tsx
│   │   │   ├── DeploymentDetail.tsx
│   │   │   ├── Builds.tsx
│   │   │   ├── Settings.tsx
│   │   │   └── NotFound.tsx
│   │   │
│   │   ├── services/                     # API service layer
│   │   │   ├── api.ts                    # API client configuration
│   │   │   ├── deploymentService.ts      # Deployment API calls
│   │   │   ├── buildService.ts           # Build API calls
│   │   │   └── authService.ts            # Authentication API calls
│   │   │
│   │   ├── hooks/                        # Custom React hooks
│   │   │   ├── useDeployments.ts
│   │   │   ├── useBuilds.ts
│   │   │   ├── useAuth.ts
│   │   │   └── useApi.ts
│   │   │
│   │   ├── store/                        # State management (Redux/Zustand)
│   │   │   ├── index.ts
│   │   │   ├── slices/                   # Redux slices (if using Redux)
│   │   │   │   ├── deploymentSlice.ts
│   │   │   │   └── buildSlice.ts
│   │   │   └── actions/                  # Action creators
│   │   │
│   │   ├── utils/                        # Utility functions
│   │   │   ├── formatters.ts             # Date, number formatters
│   │   │   ├── validators.ts             # Form validation
│   │   │   └── constants.ts              # Constants
│   │   │
│   │   ├── types/                        # TypeScript type definitions
│   │   │   ├── deployment.ts
│   │   │   ├── build.ts
│   │   │   └── api.ts
│   │   │
│   │   ├── styles/                       # Global styles
│   │   │   ├── globals.css
│   │   │   ├── variables.css             # CSS variables
│   │   │   └── components.css
│   │   │
│   │   ├── App.tsx                       # Main App component
│   │   ├── main.tsx                      # Entry point
│   │   └── router.tsx                    # Routing configuration
│   │
│   ├── package.json                      # Frontend dependencies
│   ├── package-lock.json                 # Dependency lock file
│   ├── tsconfig.json                     # TypeScript configuration
│   ├── vite.config.ts                    # Vite configuration (or webpack.config.js)
│   ├── tailwind.config.js                # Tailwind CSS configuration (if used)
│   ├── .eslintrc.json                    # ESLint configuration
│   └── .env.example                       # Frontend environment variables
│
├── docs/                                 # Additional documentation
│   ├── ARCHITECTURE.md                   # Detailed architecture docs
│   ├── API.md                            # API documentation
│   └── DEPLOYMENT.md                     # Deployment guide
│
├── docker/                               # Docker-related files
│   ├── Dockerfile                         # Backend Docker image
│   ├── Dockerfile.frontend               # Frontend Docker image
│   └── docker-compose.yml                # Multi-container setup
│
├── scripts/                              # Utility scripts
│   ├── setup.sh                          # Project setup script
│   ├── test_api.sh                       # API testing script
│   └── deploy.sh                         # Deployment script
│
├── .env.example                          # Example environment variables
├── .env                                  # Environment variables (gitignored)
├── .gitignore                            # Git ignore rules
├── requirements.txt                      # Python dependencies
├── requirements-dev.txt                  # Development dependencies
├── pytest.ini                            # Pytest configuration
├── README.md                             # Main project documentation
├── README.txt                            # Plain text version of README
├── file_structure.md                     # This file
└── LICENSE                               # License file
```

---

## 📂 Directory Descriptions

### `/app` - Main Application

**Purpose**: Contains all application code organized by layer/pattern.

#### `/app/main.py`
- FastAPI application initialization
- Middleware registration
- Route registration
- Startup/shutdown event handlers

#### `/app/config/`
- **settings.py**: Loads environment variables, provides configuration settings
- Uses `python-dotenv` for `.env` file support

#### `/app/models/`
- Pydantic models for request/response validation
- Data transfer objects (DTOs)
- Enum definitions (DeploymentStatus, BuildStatus)

#### `/app/database/`
- **connection.py**: SQLAlchemy engine, session factory, database initialization
- **models.py**: SQLAlchemy ORM models (DeploymentORM, BuildORM)

#### `/app/repositories/`
- Repository pattern implementation
- Abstracts data access layer
- Interface-based design for easy testing

#### `/app/services/`
- Business logic layer
- Orchestrates repositories, external services, and events
- No direct database access (goes through repositories)

#### `/app/strategies/`
- Strategy pattern for different build types
- Each strategy implements `BaseBuildStrategy`
- Pluggable build system

#### `/app/factories/`
- Factory pattern for creating build strategies
- Auto-detects project type
- Returns appropriate strategy instance

#### `/app/events/`
- Event-driven architecture
- Event type definitions
- Event bus for pub/sub

#### `/app/listeners/`
- Event listeners/handlers
- Reacts to system events
- Decoupled from event publishers

#### `/app/queues/`
- Message queue implementation (Redis-based)
- Task models and queue management
- Background workers for async processing

#### `/app/middleware/`
- Rate limiting
- Circuit breaker
- Request/response middleware

#### `/app/routers/`
- Modular API routes
- Separated by domain (deploy, build, health, etc.)

#### `/app/utils/`
- Utility functions
- Logging setup
- Custom exceptions

#### `/app/deployments/`
- Runtime storage for **user's deployed projects** (not DeployStack's code)
- Each deployment gets unique folder
- Contains extracted/compiled project files from user uploads
- Example: User uploads a React app → gets stored here
- **Note**: This is NOT frontend code for DeployStack itself

#### `/app/storage/`
- Application metadata storage
- Database files (if SQLite)
- Temporary files

---

### `/tests` - Test Suite

**Purpose**: Comprehensive test coverage for all components.

- **conftest.py**: Shared fixtures, test configuration
- **test_*.py**: Unit tests for each module
- **test_integration.py**: End-to-end integration tests

---

### `/alembic` - Database Migrations

**Purpose**: Database schema version control.

- **env.py**: Alembic environment configuration
- **versions/**: Migration scripts
- Tracks database schema changes over time

---

### `/docs` - Documentation

**Purpose**: Additional project documentation.

- Architecture details
- API specifications
- Deployment guides

---

### `/docker` - Containerization

**Purpose**: Docker configuration files.

- **Dockerfile**: Application container image
- **docker-compose.yml**: Multi-service orchestration (app, Redis, PostgreSQL)

---

### `/scripts` - Utility Scripts

**Purpose**: Helper scripts for development and deployment.

- Setup scripts
- Testing scripts
- Deployment automation

---

### `/frontend` - Frontend Application

**Purpose**: User interface for DeployStack platform.

#### `/frontend/src/components/`
- **common/**: Reusable UI components (buttons, inputs, modals)
- **layout/**: Layout components (header, footer, sidebar)
- **deployment/**: Deployment-specific components

#### `/frontend/src/pages/`
- Page-level components for different routes
- Dashboard, Deployments list, Deployment details, etc.

#### `/frontend/src/services/`
- API client layer
- Functions to call backend REST API
- Handles authentication, error handling

#### `/frontend/src/hooks/`
- Custom React hooks
- Data fetching hooks
- Reusable stateful logic

#### `/frontend/src/store/`
- State management (Redux, Zustand, or Context API)
- Global application state
- API response caching

#### `/frontend/src/utils/`
- Helper functions
- Formatters, validators
- Constants

#### `/frontend/src/types/`
- TypeScript type definitions
- Shared types between frontend and backend

**Tech Stack Options:**
- **React** + **TypeScript** + **Vite**
- **Next.js** (if using SSR)
- **Tailwind CSS** or **Material-UI** for styling
- **React Query** or **SWR** for data fetching
- **React Router** for routing
- **Zustand** or **Redux** for state management

---

## 🔄 Data Flow

### Frontend to Backend Flow:
```
User Interaction (Frontend)
    ↓
React Component (frontend/src/pages/)
    ↓
API Service (frontend/src/services/)
    ↓
HTTP Request (REST API)
    ↓
FastAPI Router (app/routers/)
    ↓
Service Layer (app/services/)
    ↓
Repository Layer (app/repositories/)
    ↓
Database (app/database/)
    ↓
Response back to Frontend
```

### Request Flow (Backend):
```
Client Request
    ↓
FastAPI Router (app/routers/)
    ↓
Service Layer (app/services/)
    ↓
Repository Layer (app/repositories/)
    ↓
Database (app/database/)
```

### Build Flow:
```
Upload Request (Frontend or API)
    ↓
Deployment Service
    ↓
Queue Manager (app/queues/)
    ↓
Build Worker (app/queues/workers/)
    ↓
Build Strategy (app/strategies/)
    ↓
Event Bus (app/events/)
    ↓
Event Listeners (app/listeners/)
    ↓
Frontend Updates (via WebSocket or Polling)
```

---

## 📦 Key Files Explained

### `app/main.py`
- Entry point for the FastAPI application
- Registers all routers
- Sets up middleware (rate limiting, circuit breaker)
- Initializes database on startup
- Starts background workers

### `app/config/settings.py`
- Centralized configuration management
- Loads from environment variables
- Provides typed settings access
- Supports different environments (dev, staging, prod)

### `app/services/deployment_service.py`
- Core business logic for deployments
- Creates deployments
- Manages deployment lifecycle
- Integrates with repositories, cache, and events

### `app/strategies/base_strategy.py`
- Abstract base class for build strategies
- Defines interface for all build types
- Ensures consistent build process

### `app/queues/queue_manager.py`
- Redis-based message queue
- Producer: Enqueues build tasks
- Consumer: Build worker consumes tasks
- Handles retries and dead letter queue

### `app/middleware/rate_limiter.py`
- Token bucket algorithm
- Redis-based distributed rate limiting
- Per-client and per-endpoint limits

### `app/middleware/circuit_breaker.py`
- Protects against cascading failures
- Three states: CLOSED, OPEN, HALF_OPEN
- Used for external service calls (GitHub, S3)

---

## 🗂️ File Naming Conventions

- **Python files**: `snake_case.py`
- **Classes**: `PascalCase`
- **Functions/Variables**: `snake_case`
- **Constants**: `UPPER_SNAKE_CASE`
- **Test files**: `test_*.py`
- **Migration files**: `[timestamp]_[description].py`

---

## 📝 Notes

- All directories will have `__init__.py` files to make them Python packages
- Configuration files (`.env`, `database.db`) are gitignored
- Deployment folders are created at runtime
- Tests mirror the application structure for easy navigation
- Documentation is kept separate from code for clarity
- **Important**: `/app/deployments/` contains **user's deployed projects**, NOT DeployStack's frontend code
- `/frontend/` contains the **DeployStack platform's UI** (admin/dashboard interface)
- `/app/deployments/` contains **user's projects** that get deployed (separate from platform UI)
- DeployStack has both: Backend API (`/app/`) and Frontend UI (`/frontend/`)

---

## 🚀 Implementation Order

### Backend Implementation:
1. **Phase 1**: Core structure (`app/`, `app/main.py`, `app/config/`)
2. **Phase 2**: Models and repositories (`app/models/`, `app/repositories/`)
3. **Phase 3**: Services and business logic (`app/services/`)
4. **Phase 4**: Build system (`app/strategies/`, `app/factories/`)
5. **Phase 5**: Events and listeners (`app/events/`, `app/listeners/`)
6. **Phase 6**: Queue system (`app/queues/`)
7. **Phase 7**: Middleware (`app/middleware/`)
8. **Phase 8**: Database integration (`app/database/`, `alembic/`)
9. **Phase 9**: Testing (`tests/`)

### Frontend Implementation:
10. **Phase 10**: Frontend setup (`frontend/`, React/TypeScript setup)
11. **Phase 11**: Core components (`frontend/src/components/common/`)
12. **Phase 12**: Layout components (`frontend/src/components/layout/`)
13. **Phase 13**: API services (`frontend/src/services/`)
14. **Phase 14**: Pages and routing (`frontend/src/pages/`, `frontend/src/router.tsx`)
15. **Phase 15**: State management (`frontend/src/store/`)
16. **Phase 16**: Deployment UI (`frontend/src/components/deployment/`)

### Integration & Deployment:
17. **Phase 17**: Frontend-Backend integration
18. **Phase 18**: Docker and deployment (`docker/`, `scripts/`)
19. **Phase 19**: End-to-end testing
20. **Phase 20**: Production deployment

---

This file structure will be implemented incrementally as the project progresses through the implementation roadmap outlined in the README.

