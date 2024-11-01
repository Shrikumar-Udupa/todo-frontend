# ------------------- Stage 1: Build Stage ------------------------------
FROM node:21 AS frontend-builder
# Set the working directory to /app
WORKDIR /app
# Copy the package.json and package-lock.json for dependency installation
COPY package*.json ./
# Install dependencies
RUN npm install
# Copy the rest of the application code
COPY . .

# ------------------- Stage 2: Final Stage ------------------------------
FROM node:21-slim
# Set the working directory to /app
WORKDIR /app
# Use the existing node user and set permissions for the application directory
RUN chown -R node:node /app
# Switch to the non-root user with UID 1000 (node)
USER node
# Expose port 3000 for the Node.js application
EXPOSE 3000
# Copy built assets and dependencies from frontend-builder stage
COPY --from=frontend-builder /app .
# Define the default command to run the application
CMD [ "npm", "start" ]
