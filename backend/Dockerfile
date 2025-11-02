# -----------------------
# Stage 1: Builder
# -----------------------
FROM node:21-alpine AS builder

WORKDIR /app

# Copy only dependency files first (for better build caching)
COPY package*.json ./

# Install dependencies (include dev dependencies for build tools)
RUN npm install

# Copy all source code
COPY . .

# Optional: build step (if you use TypeScript or a build command)
# RUN npm run build

# -----------------------
# Stage 2: Production
# -----------------------
FROM node:21-alpine AS production

WORKDIR /app

# Copy only package.json files again
COPY package*.json ./

# Install only production dependencies
RUN npm install --omit=dev

# Copy built app (or source if no build step)
COPY --from=builder /app ./

# Set environment variables
ARG PORT=8888
ENV PORT=${PORT}

# Expose the app port
EXPOSE ${PORT}

# Start the app
CMD ["sh", "-c", "npm run setup && npm start"]
