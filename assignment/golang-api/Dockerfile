FROM golang:1.23-alpine AS builder

RUN apk update && \
    apk upgrade --no-cache && \
    rm -rf /var/cache/apk/*

WORKDIR /app

COPY main.go .

RUN go mod init hello-api && \
    go get github.com/lib/pq && \
    CGO_ENABLED=0 go build -trimpath -o api main.go

FROM alpine:3.21

RUN apk update && \
    apk upgrade --no-cache && \
    rm -rf /var/cache/apk/*

WORKDIR /app

COPY --from=builder /app/api .

RUN addgroup -S appgroup && adduser -S appuser -G appgroup
USER appuser

EXPOSE 8080

CMD ["./api"]
