
# Your Go Web Server Docker Image

This Docker image contains a simple Go web server that serves static content and handles form submissions. The default behavior is to display "Your Docker Image is Running!" when accessed at the root.

## Prerequisites

- Docker installed on your machine ([Install Docker](https://docs.docker.com/get-docker/))

## Building the Docker Image

To build the Docker image, follow these steps:

1. Open a terminal.
2. Navigate to the directory containing your Dockerfile and source code.
3. Run the following command:

    ```bash
    docker build -t your-username/go-web-server:latest -f Dockerfile .
    ```

    Replace `your-username` with your DockerHub username or the desired repository name.

## Understanding the Dockerfile

The Dockerfile is designed in two stages: Build Stage and Deployable Image.

### Build Stage

In the build stage, we use an official Golang image to compile the Go application and statically link the binary. We also create a non-root user for running the application.

- **Working Directory:** `/app`
- **Copy go.mod:** Install dependencies efficiently and leverage layer caching.
- **Cache Mounts:** Use cache mounts to speed up the installation of existing dependencies.
- **Copy Source Code:** Copy the entire application source code.
- **Build Application:** Compile the application during build and statically link the binary.

### Deployable Image

In the deployable image stage, we use a minimal scratch image and copy only essential files from the build stage.

- **Environment Variable:** Set GIN_MODE environment variable to release.
- **Working Directory:** `/`
- **Copy User Information:** Copy the /etc/passwd file from the build stage to provide non-root user information.
- **Copy Application Binary:** Copy the compiled application binary from the build stage.
- **Use Non-root User:** Use the non-root user created in the build stage.
- **Expose Port:** Expose the port the application will run on.
- **Command:** Define the command to run the application when the container starts.

## Pushing the Docker Image to DockerHub

To push the Docker image to DockerHub, run the following command:

```bash
docker push your-username/go-web-server:latest
```

Replace `your-username` with your DockerHub username or the desired repository name.

## Running the Docker Container

To run the Docker container, execute the following command:

```bash
docker run -p 8080:8080 your-username/go-web-server:latest
```

Visit [http://localhost:8080/](http://localhost:8080/) in your browser to see the message "Your Docker Image is Running!"

Note: You can customize the port and tag as needed.
