
# Your Node.js Express App Docker Image

This Docker image contains a simple Node.js Express application. The default behavior is to respond with "Hello, World!" when accessed at the root.

## Prerequisites

- Docker installed on your machine ([Install Docker](https://docs.docker.com/get-docker/))

## Building the Docker Image

To build the Docker image, follow these steps:

1. Open a terminal.
2. Navigate to the directory containing your Dockerfile and source code.
3. Run the following command:

    ```bash
    docker build -t your-username/node-express-app:latest -f Dockerfile.prod .
    ```

    Replace `your-username` with your DockerHub username or the desired repository name.

## Understanding the Dockerfile

The Dockerfile is designed in two stages: Base Image and Production Image.

### Base Image

In the base image stage, we use an official Node.js image to set up the working directory, copy package files, and the entire application source code.

- **Working Directory:** `/usr/src/app`
- **Copy package files:** Copy package.json and package-lock.json to install dependencies efficiently.
- **Copy Source Code:** Copy the entire application source code.

### Production Image

In the production image stage, we use the base image as the starting point and set up the environment for production.

- **Environment Variable:** Set NODE_ENV to production.
- **Set up npm cache:** Improve caching by setting up npm cache in a designated directory.
- **Install Dependencies:** Run `npm ci --only=production` to install production dependencies efficiently.
- **Switch to Non-root User:** Switch to a non-root user for improved security.
- **Expose Port:** Expose the port that the application will run on.
- **Define Command:** Define the command to run the application when the container starts.

## Pushing the Docker Image to DockerHub

To push the Docker image to DockerHub, run the following command:

```bash
docker push your-username/node-express-app:latest
```

Replace `your-username` with your DockerHub username or the desired repository name.

## Running the Docker Container

To run the Docker container, execute the following command:

```bash
docker run -p 8080:8080 your-username/node-express-app:latest
```

Visit [http://localhost:8080/](http://localhost:8080/) in your browser to see the message "Hello, World!"

Note: You can customize the port and tag as needed.
