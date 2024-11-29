# ------------------- Stage 1: Build Stage ------------------------------

# Stage 1: Builder
FROM node AS builder

# Set the working directory to /app
WORKDIR /app

# Copy the package.json and package-lock.json for dependency installation
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . ./

# Build the production assets (useful for frontend apps)
RUN npm run build


# ------------------- Stage 2: Final Stage ------------------------------
# Stage 2: Runner
FROM node:current-slim

# Set the working directory to /app
WORKDIR /app

# Copy built assets and dependencies from frontend-builder stage
COPY --from=builder /app ./

# Expose the application port
EXPOSE 3000

# Define the default command to run the application
CMD ["npm", "start"]
