# Books API
Простое REST API для управления библиотекой книг (CRUD).

## Зависимости
1) python 3.12+
2) postgresql 16+
3) nginx

## Локальный запуск без docker
1) Склонировать репозиторий `git clone $git_url`
2) Установить postgres
3) Создать БД
```sql
CREATE DATABASE library;
CREATE USER appuser WITH PASSWORD 'secretpass';
ALTER DATABASE library OWNER TO appuser;

```
4) Запустить приложение
```bash
pip install -r requirements.txt
cp .env.example .env
uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload
```
5) Настроить nginx как прокси (см конфиг nginx/books.conf)

## Проверка
```bash
# проверка живости приложения
curl http://localhost/health

# добавить книгу
curl -X POST http://localhost/books/ \
  -H "Content-Type: application/json" \
  -d '{"title":"1984","author":"George Orwell","isbn":"978-0451524935","year":1949}'

# посмотреть список книг
curl http://localhost/books/?limit=5
```