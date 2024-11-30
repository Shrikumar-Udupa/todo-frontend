# ------------------- Stage 1: Build Stage ------------------------------
    FROM node AS frontend-builder

    # Create a user with UID 1000 (matching Kubernetes runAsUser)
    RUN useradd -u 1000 -m appuser
    
    # Set the working directory to /app
    WORKDIR /app
    
    # Set the user to appuser (with UID 1000)
    USER appuser
    
    # Copy the package.json and package-lock.json for dependency installation
    COPY --chown=appuser:appuser package.json package-lock.json ./
    
    # Install dependencies
    RUN npm install
    
    # Copy the rest of the application code
    COPY --chown=appuser:appuser . ./
    
    # Build the production assets (useful for frontend apps)
    RUN npm run build
    
    # ------------------- Stage 2: Final Stage ------------------------------
    FROM node:current-slim
    
    # Create the same user in the final image
    RUN useradd -u 1000 -m appuser
    
    # Set the working directory to /app
    WORKDIR /app
    
    # Set the user to appuser (with UID 1000)
    USER appuser
    
    # Copy built assets and dependencies from frontend-builder stage
    COPY --from=frontend-builder /app ./
    
    # Expose the application port
    EXPOSE 3000
    
    # Set the default command to run the application
    CMD ["npm", "start", "--loglevel", "verbose"]
    