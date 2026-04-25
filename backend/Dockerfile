# syntax=docker/dockerfile:1.7

FROM golang:1.22-alpine AS builder

WORKDIR /app

RUN apk add --no-cache ca-certificates tzdata

COPY go.mod go.sum ./
RUN go mod download

COPY . .

RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 \
    go build -ldflags="-s -w" -o /app/backend ./cmd/api


FROM alpine:3.20

WORKDIR /app

RUN addgroup -S appgroup && adduser -S appuser -G appgroup \
    && apk add --no-cache ca-certificates tzdata wget

COPY --from=builder /app/backend /app/backend

RUN chown -R appuser:appgroup /app

USER appuser

EXPOSE 8081

HEALTHCHECK --interval=30s --timeout=5s --start-period=10s --retries=3 \
  CMD wget --spider -q http://127.0.0.1:8081/health || exit 1

ENTRYPOINT ["/app/backend"]
