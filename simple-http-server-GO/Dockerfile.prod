# Stage 1: Build Stage
# Use a specific version of the official Golang image as the base image
FROM golang:1.21-bullseye AS build

# Create a non-root user for running the application
RUN useradd -u 1001 nonroot

# Set the working directory inside the container
WORKDIR /app 

# Copy only the go.mod file to install dependencies efficiently and leverage layer caching
COPY go.mod ./

# Set the GIN_MODE environment variable to release
ENV GIN_MODE=release


# Use cache mounts to speed up the installation of existing dependencies
RUN --mount=type=cache,target=/go/pkg/mod \
    --mount=type=cache,target=/root/.cache/go-build \
    go mod download

# Copy the entire application source code
COPY . .

# Compile the application during build and statically link the binary
RUN go build \
    -ldflags="-linkmode external -extldflags -static" \
    -tags netgo \
    -o go-web-server

# Stage 2: Deployable Image
# Use a minimal scratch image as the base image for the final image
FROM scratch

# Copy the /etc/passwd file from the build stage to provide non-root user information
COPY --from=build /etc/passwd /etc/passwd

# Copy the compiled application binary from the build stage to the final image
COPY --from=build /app/go-web-server /go-web-server

# Use the non-root user created in the build stage
USER nonroot

# Expose the port the application will run on
EXPOSE 8080

# Define the command to run the application when the container starts
CMD ["./go-web-server"]
