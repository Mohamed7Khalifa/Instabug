FROM golang:1.19 AS builder
WORKDIR /app
COPY go.mod go.sum ./
RUN go mod download
COPY *.go ./
RUN CGO_ENABLED=0 GOOS=linux go build -o /main
#   Stage 2: Final stage
FROM alpine:3.14
WORKDIR /run
COPY *.sh .
COPY --from=builder /main /main
EXPOSE 9090
CMD ["/main"]
