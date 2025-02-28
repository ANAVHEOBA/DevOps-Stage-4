# Build stage
FROM golang:1.21.1-alpine AS builder
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o auth-api

# Final stage
FROM alpine:3.18
RUN apk --no-cache add ca-certificates
WORKDIR /root/
COPY --from=builder /app/auth-api .
EXPOSE 8081
ENV AUTH_API_PORT=8081
CMD ["./auth-api"] 