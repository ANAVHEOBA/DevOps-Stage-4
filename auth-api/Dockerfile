# Build stage
FROM golang:1.21.1-alpine AS builder

# Install build dependencies
RUN apk add --no-cache \
    git \
    make \
    build-base

WORKDIR /app

# Copy and download dependencies first (better caching)
COPY go.mod go.sum ./
RUN go mod download

# Copy the rest and build
COPY . .
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o auth-api

# Final stage
FROM alpine:3.18

# Add CA certificates and timezone data
RUN apk add --no-cache \
    ca-certificates \
    tzdata

WORKDIR /app

# Copy binary from builder
COPY --from=builder /app/auth-api .

# Expose port
EXPOSE 8081

# Set environment variables
ENV AUTH_API_PORT=8081

# Run the service
CMD ["./auth-api"]