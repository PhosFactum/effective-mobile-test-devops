# Сборку по мультистейджу делаем (в два этапа)

# 1. Сборка первоначального образа
FROM golang:1.21-alpine AS builder

RUN apk add --no-cache git ca-certificates

WORKDIR /app

COPY go.mod ./

RUN go mod download

COPY main.go .

# Сборка с оптимизациями:
RUN CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build \
    -ldflags="-w -s -extldflags '-static'" \
    -o app main.go

# 2. Финальный образ собираем
FROM alpine:latest

RUN apk add --no-cache ca-certificates tzdata

# Создаем непривилегированного пользователя
RUN addgroup -g 1001 appgroup && \
    adduser -u 1001 -G appgroup -s /bin/sh -D appuser

WORKDIR /app

COPY --from=builder /app/app .

# Устанавливаем права на владельца
RUN chown -R appuser:appgroup /app

# Переключаемся на непривилегированного пользователя
USER appuser

EXPOSE 8080

CMD ["./app"]
