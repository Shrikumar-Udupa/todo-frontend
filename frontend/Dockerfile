# ------------------- Stage 1: Build Stage ------------------------------
    FROM node AS frontend-builder

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
    FROM node:current-slim
    
    # Set the working directory to /app
    WORKDIR /app
    
    # Use the existing node user with UID 1000
    USER node
    
    # Copy built assets and dependencies from frontend-builder stage
    COPY --from=frontend-builder --chown=node:node /app ./
    
    # Expose the application port
    EXPOSE 3000
    
    # Set the default command to run the application
    CMD ["npm", "start", "--loglevel", "verbose"]
    