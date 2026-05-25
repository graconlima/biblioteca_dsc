FROM python:3.13-slim AS builder

WORKDIR /app

COPY requirements.txt .

RUN pip install --prefix=/install --no-cache-dir -r requirements.txt


FROM python:3.13-slim

WORKDIR /app

COPY --from=builder /install /usr/local

COPY . .

EXPOSE 8000

CMD python manage.py migrate && gunicorn biblioteca.wsgi:application --bind 0.0.0.0:8000 --workers 3