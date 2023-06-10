# Stage 1: Build stage
FROM golang:1.16-alpine AS builder
WORKDIR /app
COPY . .
RUN go build

# Stage 2: Final stage
FROM alpine:3.14
WORKDIR /app
COPY --from=builder /app/internship-2023 .
EXPOSE 9090
CMD ["./internship-2023"]
