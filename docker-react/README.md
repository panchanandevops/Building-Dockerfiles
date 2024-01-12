
# Your React App Docker Image

This Docker image contains a simple React application created using create-react-app. The application displays a "Hello, World!" message and includes basic configurations for a progressive web app.

## Prerequisites

- Docker installed on your machine ([Install Docker](https://docs.docker.com/get-docker/))

## Building the Docker Image

To build the Docker image, follow these steps:

1. Open a terminal.
2. Navigate to the directory containing your Dockerfile and source code.
3. Run the following command:

    ```bash
    docker build -t your-username/react-app:latest -f Dockerfile.prod .
    ```

    Replace `your-username` with your DockerHub username or the desired repository name.

## Understanding the Dockerfile

The Dockerfile is designed in two stages: Build Stage and Deployable Image.

### Build Stage

In the build stage, we use an official Node.js image to set up the working directory, copy package files, and the entire application source code. We then run the build command to generate production-ready artifacts.

- **Working Directory:** `/usr/src/app`
- **Copy package files:** Copy package.json and package-lock.json to install dependencies efficiently.
- **Set up npm cache:** Improve caching by setting up npm cache in a designated directory.
- **Install Dependencies:** Run `npm install` to install dependencies.
- **Copy Source Code:** Copy the entire application source code.
- **Run Build Command:** Run `npm run build` to generate production-ready artifacts.

### Deployable Image

In the deployable image stage, we use an official Nginx image to serve the React app. We copy the built artifacts from the build stage to the Nginx HTML directory.

- **Base Image:** Nginx official image with unprivileged user (`nginxinc/nginx-unprivileged:1.24-bullseye-perl`).
- **Expose Port:** Expose the port that the Nginx server will listen on.
- **Copy Artifacts:** Copy the built artifacts from the build stage to the Nginx HTML directory.

## Pushing the Docker Image to DockerHub

To push the Docker image to DockerHub, run the following command:

```bash
docker push your-username/react-app:latest
```

Replace `your-username` with your DockerHub username or the desired repository name.

## Running the Docker Container

To run the Docker container, execute the following command:

```bash
docker run -p 8080:8080 your-username/react-app:latest
```

Visit [http://localhost:8080/](http://localhost:8080/) in your browser to see the React app.

Note: You can customize the port and tag as needed.
