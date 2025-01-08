# Stage 1: Build stage
FROM node:20.10.0-alpine3.19

# Set working directory
WORKDIR /app

# Copy root package files
COPY ../package.json ./
COPY ../pnpm-workspace.yaml ./
COPY ../pnpm-lock.yaml ./
COPY ../turbo.json ./

# Copy packages directory
COPY ../packages ./packages

# Skip downloading Chrome for Puppeteer (saves build time)
ENV PUPPETEER_SKIP_DOWNLOAD=true

# Install runtime dependencies
RUN apk add --no-cache chromium git python3 py3-pip make g++ build-base cairo-dev pango-dev

# Set the environment variable for Puppeteer to find Chromium
ENV PUPPETEER_EXECUTABLE_PATH=/usr/bin/chromium-browser

# Install pnpm
RUN npm install -g pnpm@8.9.0

# Install dependencies and build
RUN pnpm install --frozen-lockfile
RUN pnpm build

# Set environment variables
ENV PORT=8080
ENV HOST=0.0.0.0
ENV EXECUTION_MODE=main

EXPOSE 8080

CMD ["pnpm", "start"]
