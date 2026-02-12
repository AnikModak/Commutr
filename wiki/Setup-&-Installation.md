# Setup & Installation

This guide will help you get Commutr running on your local machine for development.

## Prerequisites

Before you begin, ensure you have the following installed:

### Required

- **Node.js 18+** and **npm**
  ```bash
  node --version  # Should be 18.0.0 or higher
  npm --version   # Should be 8.0.0 or higher
  ```
  Download from: https://nodejs.org/

- **PostgreSQL 14+**
  ```bash
  psql --version  # Should be 14.0 or higher
  ```
  Download from: https://www.postgresql.org/download/

- **Redis 6+**
  ```bash
  redis-server --version  # Should be 6.0.0 or higher
  ```
  Download from: https://redis.io/download

- **Git**
  ```bash
  git --version
  ```
  Download from: https://git-scm.com/downloads

### Optional (for AI features)

- **Python 3.9+** and **pip**
  ```bash
  python --version  # Should be 3.9.0 or higher
  pip --version
  ```
  Download from: https://www.python.org/downloads/

## Step-by-Step Installation

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/commutr.git
cd commutr
```

### 2. Install Dependencies

```bash
# Install Node.js dependencies
npm install

# Install Python dependencies (if using AI features)
cd src/ai
pip install -r requirements.txt
cd ../..
```

### 3. Set Up PostgreSQL Database

```bash
# Create database
createdb commutr

# Install PostGIS extension
psql commutr -c "CREATE EXTENSION postgis;"

# Run migrations
npm run migrate
```

### 4. Set Up Redis

```bash
# Start Redis server (in a separate terminal)
redis-server

# Verify Redis is running
redis-cli ping  # Should return "PONG"
```

### 5. Configure Environment Variables

```bash
# Copy example environment file
cp .env.example .env

# Edit .env with your settings
nano .env  # or use your preferred editor
```

**Required environment variables**:

```env
# API Configuration
API_BASE_URL=http://localhost:3000
API_PORT=3000

# Database
DATABASE_URL=postgresql://localhost:5432/commutr
DATABASE_USER=your_username
DATABASE_PASSWORD=your_password

# Redis
REDIS_URL=redis://localhost:6379

# Transport APIs (get free keys from providers)
TRANSPORT_API_KEY=your_transport_api_key
MAPS_API_KEY=your_mapbox_api_key

# Business Listings
LISTING_FEE_AMOUNT=50.00
PROXIMITY_THRESHOLD_METERS=500

# AI Services (optional)
LLM_API_KEY=your_openai_api_key
LLM_MODEL=gpt-4
```

### 6. Seed the Database (Optional)

```bash
# Load sample transport data and businesses
npm run seed
```

This creates:
- Sample bus and train routes
- Test business listings
- Example accessibility data

### 7. Start the Development Server

```bash
# Start backend server
npm run dev:server

# In a new terminal, start frontend
npm run dev:client

# In another terminal, start AI service (optional)
cd src/ai
python api.py
```

### 8. Verify Installation

Open your browser and navigate to:
- **Frontend**: http://localhost:3000
- **API**: http://localhost:3000/api/health
- **AI Service**: http://localhost:8000/health (if running)

You should see the Commutr interface and be able to search for routes.

## Common Setup Issues

### Issue: PostgreSQL Connection Failed

**Error**: `ECONNREFUSED` or `password authentication failed`

**Solution**:
1. Verify PostgreSQL is running: `pg_isready`
2. Check your DATABASE_URL in `.env`
3. Ensure user has correct permissions:
   ```sql
   GRANT ALL PRIVILEGES ON DATABASE commutr TO your_username;
   ```

### Issue: PostGIS Extension Not Found

**Error**: `extension "postgis" does not exist`

**Solution**:
1. Install PostGIS for your system:
   - **Ubuntu/Debian**: `sudo apt-get install postgis postgresql-14-postgis-3`
   - **macOS**: `brew install postgis`
   - **Windows**: Download from https://postgis.net/windows_downloads/
2. Create extension: `psql commutr -c "CREATE EXTENSION postgis;"`

### Issue: Redis Connection Failed

**Error**: `Redis connection to localhost:6379 failed`

**Solution**:
1. Start Redis: `redis-server`
2. Check if Redis is running: `redis-cli ping`
3. Verify REDIS_URL in `.env`

### Issue: Port Already in Use

**Error**: `EADDRINUSE: address already in use :::3000`

**Solution**:
1. Find process using port: `lsof -i :3000` (macOS/Linux) or `netstat -ano | findstr :3000` (Windows)
2. Kill the process or change API_PORT in `.env`

### Issue: npm install Fails

**Error**: Various npm errors during installation

**Solution**:
1. Clear npm cache: `npm cache clean --force`
2. Delete `node_modules` and `package-lock.json`
3. Run `npm install` again
4. If still failing, check Node.js version: `node --version`

### Issue: TypeScript Compilation Errors

**Error**: Type errors during build

**Solution**:
1. Ensure TypeScript is installed: `npm install -g typescript`
2. Check `tsconfig.json` is present
3. Run `npm run type-check` to see all errors
4. Delete `node_modules` and reinstall if needed

### Issue: Missing API Keys

**Error**: `API key not configured` or `401 Unauthorized`

**Solution**:
1. Get free API keys:
   - **Mapbox**: https://account.mapbox.com/
   - **Transport API**: Check your local transport authority
   - **OpenAI** (optional): https://platform.openai.com/
2. Add keys to `.env` file
3. Restart development server

## Development Workflow

### Running Tests

```bash
# Run all tests
npm test

# Run unit tests only
npm run test:unit

# Run property-based tests
npm run test:property

# Run tests in watch mode
npm run test:watch

# Run tests with coverage
npm run test:coverage
```

### Linting and Formatting

```bash
# Check code style
npm run lint

# Fix auto-fixable issues
npm run lint:fix

# Format code with Prettier
npm run format
```

### Database Management

```bash
# Create a new migration
npm run migrate:create -- --name add_new_table

# Run pending migrations
npm run migrate

# Rollback last migration
npm run migrate:rollback

# Reset database (WARNING: deletes all data)
npm run db:reset
```

### Building for Production

```bash
# Build both client and server
npm run build

# Build client only
npm run build:client

# Build server only
npm run build:server

# Start production server
npm start
```

## Docker Setup (Alternative)

If you prefer using Docker:

```bash
# Build and start all services
docker-compose up

# Run in detached mode
docker-compose up -d

# View logs
docker-compose logs -f

# Stop services
docker-compose down
```

The Docker setup includes:
- Node.js application
- PostgreSQL with PostGIS
- Redis
- Python AI service

## IDE Setup

### VS Code (Recommended)

Install these extensions:
- **ESLint**: Code linting
- **Prettier**: Code formatting
- **TypeScript**: Enhanced TypeScript support
- **PostgreSQL**: Database management
- **Docker**: Container management

Recommended settings (`.vscode/settings.json`):
```json
{
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "typescript.tsdk": "node_modules/typescript/lib"
}
```

### Other IDEs

- **WebStorm**: Built-in TypeScript and Node.js support
- **Vim/Neovim**: Use CoC or LSP with TypeScript language server
- **Emacs**: Use lsp-mode with typescript-language-server

## Next Steps

Now that you have Commutr running:

1. Read the [Usage Guide](Usage-Guide) to learn how to use the platform
2. Check the [System Architecture](System-Architecture) to understand the codebase
3. Review the [Contribution Guide](Contribution-Guide) to start contributing
4. Join discussions on GitHub to ask questions

## Getting Help

If you're stuck:

1. Check this guide again carefully
2. Search existing GitHub Issues
3. Ask in GitHub Discussions
4. Open a new issue with:
   - Your operating system
   - Node.js and npm versions
   - Complete error message
   - Steps you've already tried

---

*Setup working? Great! Head to the [Usage Guide](Usage-Guide) to start using Commutr.*
