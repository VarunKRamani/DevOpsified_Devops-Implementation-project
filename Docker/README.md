# Containerization of the application 

Containerizing of Go application with Muilt-stage build 


**Docker File** 

```
# Containerize the go application that we have created
# This is the Dockerfile that we will using to build the image and run the container

# Stage 1 - Starting with a base image
FROM golang:1.21 as base

# Setting the working directory inside the container
WORKDIR /app

# Copy the go.mod and go.sum files to the working directory
COPY go.mod ./

# Download all the dependencies
RUN go mod download

# Copy the source code to the working directory
COPY . .

# Build the application
RUN go build -o main .

------------------------------------------------------------
# Stage 2 - Reduce the image size using multi-stage builds.

# We are using a distroless image to run the application
FROM gcr.io/distroless/base

# Copy the binary from the previous stage
COPY --from=base /app/main .

# Copy the static files from the previous stage
COPY --from=base /app/static ./static

# Expose the port on which the application will run
EXPOSE 8080

# Run the application
CMD ["./main"]

```
**Explanation**

`gcr.io/distroless/base`? --> It is a minimal Docker base image crea0ted by Google (GoogleContainerTools) that contains only our application's runtime dependencies, package managers, and debugging utilities.
Eliminating unused binaries and package managers drastically reduces the number of Common Vulnerabilities and Exposures (CVEs) flagged by security scanners, and leaves attackers with nothing to use if they breach the container.
It is significantly leaner than full Linux distribution images (like Ubuntu or Debian) or even Alpine Linux, leading to faster image pulls and deployments.

`./static` --> why copy static files ? --> It is copying a folder containing static web assets that our application needs to serve to users.

## HandsON
<img width="932" height="617" alt="image" src="https://github.com/user-attachments/assets/fa653eff-75b3-4995-9169-4b89e2f8b9fc" />
