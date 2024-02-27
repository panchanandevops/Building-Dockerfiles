# Stage 1: builder Image
# Use a specific version of the official Node.js image as the builder image
FROM node:21.5-bullseye-slim AS builder

# Set the working directory inside the container
WORKDIR /usr/src/app

# Copy package.json and package-lock.json to install dependencies efficiently and leverage layer caching
COPY package*.json ./


# Stage 2: Production Image
# Use the builder image as the starting point for the production image
FROM builder as production

# Set the environment variable for Node.js to production
ENV NODE_ENV production

# Set up npm cache in a designated directory to improve caching
RUN --mount=type=cache,target=/usr/src/app/.npm \
    npm set cache /usr/src/app/.npm && \
    npm ci --only=production

# Switch to a non-root user for improved security
USER node

# Copy the application source code to the final image
COPY --chown=node:node . .

# Expose the port that the application will run on
EXPOSE 8080

# Define the command to run the application when the container starts
CMD [ "node", "index.js" ]
