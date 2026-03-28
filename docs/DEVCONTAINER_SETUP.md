# Development Container Configuration

This document describes the VS Code Dev Container setup with Java, PostgreSQL, and React pre-installed.

## 📁 Configuration Files

- **devcontainer.json** - VS Code Dev Container configuration with image, features, services, and extensions
- **Dockerfile** - Custom Docker image with Java, Node.js, PostgreSQL client, and development tools
- **docker-compose.yml** - Compose file for running services (app + PostgreSQL database)

## Getting Started

### Prerequisites
- VS Code with the "Dev Containers" extension installed
- Docker and Docker Compose installed

### Usage

#### Option 1: Using VS Code Dev Container (Recommended)

1. Open the project in VS Code
2. Press `Ctrl+Shift+P` (or `Cmd+Shift+P` on Mac)
3. Select "Dev Containers: Reopen in Container"
4. VS Code will build and start the container

#### Option 2: Using Docker Compose

```bash
cd .devcontainer
docker-compose up -d
```

This will start both the development environment and PostgreSQL database.

## Available Services & Ports

- **React Dev Server**: `http://localhost:3000`
- **Java Application**: `http://localhost:8080`
- **PostgreSQL**: `localhost:5432`
  - Username: `postgres`
  - Password: `postgres`
  - Database: `myapp`

## Included Tools

- **Java**: OpenJDK 21
- **Node.js**: v18 LTS
- **npm**: Latest version
- **Yarn**: Latest version
- **Maven**: Build tool for Java projects
- **PostgreSQL Client**: Command-line tools for database management
- **Create React App**: CLI for creating React applications
- **Vite**: Next generation frontend tooling

## VS Code Extensions

The following extensions are automatically installed:
- **Extension Pack for Java** - Java development tools
- **ES7+ React/Redux/React-Native Snippets** - React code snippets
- **PostgreSQL** - Database management with elephant icon 🐘

## Environment Variables

Default PostgreSQL credentials are:
- User: `postgres`
- Password: `postgres`
- Database: `myapp`

You can change these in `docker-compose.yml` or `devcontainer.json`

## Common Commands

```bash
# Create a new React app
npx create-react-app my-app

# Create a React app with Vite
npm create vite my-app -- --template react

# Check Java version
java -version

# Connect to PostgreSQL
psql -h postgres -U postgres -d myapp

# Build Java project with Maven
mvn clean install

# Start React dev server
npm start
```

## Troubleshooting

### Container fails to start
- Ensure Docker is running
- Check Docker logs: `docker logs <container_id>`

### Cannot connect to PostgreSQL
- Verify PostgreSQL container is running: `docker ps`
- Check connection settings (user, password, host)

### Port conflicts
- Change port mappings in `docker-compose.yml` or `devcontainer.json`

### Build issues
- Clean up containers: `docker-compose down -v`
- Rebuild: `docker-compose up -d --build`
