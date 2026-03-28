# Use Ubuntu with Java pre-installed
FROM mcr.microsoft.com/devcontainers/java:21-bullseye

# Remove problematic Yarn repository
RUN rm -f /etc/apt/sources.list.d/yarn.list

# Install Node.js, PostgreSQL client, and other tools
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    gnupg \
    postgresql-client \
    maven \
    && rm -rf /var/lib/apt/lists/*

# Install Node.js from NodeSource
RUN curl -sL https://deb.nodesource.com/setup_18.x | bash - && \
    apt-get install -y --no-install-recommends nodejs && \
    rm -rf /var/lib/apt/lists/*

# Install global npm packages for React development
RUN npm install -g create-react-app vite

# Set working directory
WORKDIR /workspace
