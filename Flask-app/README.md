# Flask App Docker Image

This Docker image contains a simple Flask web application that displays the hostname and IP address of the container. The application consists of an index page and an error page.

## Prerequisites

- Docker installed on your machine ([Install Docker](https://docs.docker.com/get-docker/))

## Building the Docker Image

To build the Docker image, follow these steps:

1. Open a terminal.
2. Navigate to the directory containing your Dockerfile and source code.
3. Run the following command:

    ```bash
    docker build -t your-username/flask-app:latest -f Dockerfile.prod .
    ```

    Replace `your-username` with your DockerHub username or the desired repository name.

## Understanding the Dockerfile

The Dockerfile is designed for a production environment and follows best practices for building a Python Flask application.

### Base Image

We use the official Python 3.11 Alpine image as the base image. This image is lightweight and suitable for production.

### Environment Variables

We set environment variables to configure Python behavior:

- `PYTHONDONTWRITEBYTECODE`: Prevents Python from writing pyc files to disk.
- `PYTHONUNBUFFERED`: Ensures Python output is sent directly to terminal without buffering.

### Working Directory

We create and set the working directory inside the container to `/app`.

### Install Dependencies

We copy only the `requirements.txt` file first to leverage Docker caching and install Python dependencies.

### Copy Source Code

We copy the entire application source code to the working directory.

### Expose Port

We expose port 8080, the port on which the Flask application will run.

### Command to Run

We specify the command to run on container start: `python src/app.py`.

## Pushing the Docker Image to DockerHub

To push the Docker image to DockerHub, run the following command:

```bash
docker push your-username/flask-app:latest
```

Replace `your-username` with your DockerHub username or the desired repository name.

## Running the Docker Container

To run the Docker container, execute the following command:

```bash
docker run -p 8080:8080 your-username/flask-app:latest
```

Visit [http://localhost:8080/](http://localhost:8080/) in your browser to see the Flask app.

Note: You can customize the port and tag as needed.