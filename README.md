
---

# URL Shortener API

Простой сервис для сокращения ссылок с REST API и редиректом по короткому коду.

---

## 🔹 Технологии

* Python 3.13
* Django 5.x
* Django REST Framework
* SQLite (по умолчанию, можно заменить на PostgreSQL)
* drf-spectacular (Swagger/OpenAPI документация)

---

## 🔹 API Endpoints

### CRUD ссылок

| Method    | URL                  | Описание              |
| --------- | -------------------- | --------------------- |
| GET       | `/api/shorten/`      | Список всех ссылок    |
| POST      | `/api/shorten/`      | Создание новой ссылки |
| GET       | `/api/shorten/{id}/` | Детали ссылки         |
| PUT/PATCH | `/api/shorten/{id}/` | Обновление ссылки     |
| DELETE    | `/api/shorten/{id}/` | Удаление ссылки       |

### Редирект по короткому коду

```
GET /r/<short_code>/
```

* Если ссылка активна и не истекла → редирект на оригинальный URL
* Если ссылка истекла или недействительна → 404

---

## 🔹 Пример запроса на создание

```json
POST /api/shorten/
{
  "original_url": "https://example.com/some/long/url"
}
```

Ответ:

```json
{
  "id": "uuid",
  "original_url": "https://example.com/some/long/url",
  "short_code": "a1B2c3",
  "clicks": 0,
  "expires_at": "2025-09-10T22:50:00Z",
  "is_active": true,
  "created_at": "2025-09-10T22:48:00Z"
}
```

---

## 🔹 Особенности

* Короткий код генерируется автоматически (6 символов)
* Ссылки по умолчанию действуют 15 минуты
* Подсчет кликов автоматически
* Можно указать кастомный `short_code`

---

