# DevOps Тестовое задание

## Описание
Веб-приложение с обратным прокси на Nginx и бекендом на Go.

## Архитектура
Пользователь отправляет запрос на Nginx (порт 80). Nginx выступает в роли reverse-proxy и перенаправляет запросы на бекенд (порт 8080). Бекенд запущен на Go и возвращает ответ "Hello from Effective Mobile!". Бекенд недоступен напрямую с хоста, только через Nginx внутри Docker сети.

## Стек технологий
- Go 1.21
- Nginx 1.25
- Docker (я использовал Podman из-за особенностей прав в Linux, но суть одна)
- Docker Compose

## Требования
- Docker >= 20.10
- Docker Compose >= 2.0

## Запуск проекта

```bash
# 1. Клонировать репозиторий
git clone https://github.com/PhosFactum/effective-mobile-test-devops.git
cd effective-mobile-test-devops

# 2. Запустить проект
docker-compose up -d --build

# 3. Проверить статус контейнеров
docker-compose ps

# 4. Проверить health-check
curl http://localhost/health

# 5. Проверить работоспособность
curl http://localhost
```

## Ожидаемый ответ по пункту 4 будет следующим:
### \{"status":"ok","timestamp":"YYYY-MM-DDTHH:MM:SSZ"\}

## Ожидаемый ответ по пункту 5, будет, собственно, сообщением вида:
### Hello from Effective Mobile!
