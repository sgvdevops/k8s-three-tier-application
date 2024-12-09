# FROM node:14
# WORKDIR /usr/src/app
# COPY package*.json ./
# RUN npm install
# COPY . .
# CMD [ "npm", "start" ]



# Use the official Node.js image from the Docker Hub as a base
FROM node:14

# Set a non-root user and group for security
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# Set working directory
WORKDIR /app

# Copy only necessary files first to leverage caching
COPY package*.json ./

# Install dependencies with the production flag to avoid unnecessary dev dependencies
RUN npm ci

# Copy the application code into the container
COPY . .

# Change ownership of the app directory to the non-root user
RUN chown -R appuser:appgroup /app

# Switch to non-root user for the rest of the image build
USER appuser

# Expose the port the app will run on (make sure to match the port in your app)
EXPOSE 3000

# Start the application
CMD ["node", "start"]
