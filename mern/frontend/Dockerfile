# Stage 1: Build the Node.js application
FROM node:18-alpine AS build

# Set the working directory inside the container
WORKDIR /app

# Copy the package.json and package-lock.json (if available)
COPY package*.json ./

# Install the dependencies
RUN npm install --production

# Copy the rest of the application source code
COPY . .

# Build the application (for example, if it's a React app or other built app)
RUN npm run build

# Stage 2: Production environment
FROM node:18-alpine AS production

# Set the working directory inside the container
WORKDIR /app

# Copy only the required files from the build stage
COPY --from=build /app /app

# Expose the application port (e.g., if it's listening on port 3000)
EXPOSE 3000

# Start the Node.js application
CMD ["npm", "start"]
