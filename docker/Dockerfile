# Stage 1: Build stage
FROM node:20-alpine

WORKDIR /usr/src

# Copy package files
COPY package.json .
COPY packages ./packages
COPY lerna.json .
COPY nx.json .
COPY tsconfig.json .

# Skip downloading Chrome for Puppeteer (saves build time)
ENV PUPPETEER_SKIP_DOWNLOAD=true

# Install runtime dependencies
RUN apk add --no-cache chromium git python3 py3-pip make g++ build-base cairo-dev pango-dev

# Set the environment variable for Puppeteer to find Chromium
ENV PUPPETEER_EXECUTABLE_PATH=/usr/bin/chromium-browser

# Install dependencies and build
RUN npm install
RUN npm run build

# Set environment variables
ENV PORT=8080
ENV HOST=0.0.0.0
ENV EXECUTION_MODE=main

EXPOSE 8080

CMD ["npm", "start"]
