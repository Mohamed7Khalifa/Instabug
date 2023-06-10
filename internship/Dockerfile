# Start with a base Go image
FROM golang:alpine AS builder
WORKDIR /app
ADD go.mod .
COPY . .
RUN go build -o main .

FROM alpine:latest
# ENV MYSQL_USER=root \
#     MYSQL_PASS=passwd@123 \
#     MYSQL_HOST=db \
#     MYSQL_PORT=3306

RUN apk --no-cache add mysql-client
COPY --from=builder /app/main /app/main
WORKDIR /app
EXPOSE 9090
CMD ["./main"]
