# Stage 1: Build the application
FROM node:16 as build

# Set the working directory in the container
WORKDIR /app

# Copy package.json and package-lock.json to the container
COPY package*.json ./

# Install project dependencies
RUN npm install --production

# Copy the rest of the application code to the container
COPY . .

# Build the application (replace 'npm run build' with your build command)
RUN npm run build

# Stage 2: Create the final image
FROM node:16-alpine

# Set the working directory in the final image
WORKDIR /app

# Copy the built application from the previous stage
COPY --from=build /app/build ./dist
COPY --from=build /app/node_modules ./node_modules
COPY --from=build /app/package.json ./

# Expose the port that your application will run on (if needed)
EXPOSE 9001

# Start your application
CMD ["node", "dist/app.js"]