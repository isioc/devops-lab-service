FROM python:3.12.3-slim AS base

# предотвращает буферизацию потока вывода и ошибок питона чтобы не крашилось без логов
ENV PYTHONUNBUFFERED=1 

WORKDIR /lab4
RUN mkdir app

# создаем юзера под которым будет работать апп
RUN adduser \
    --disabled-password \
    --gecos "" \
    --home "/nonexistent" \
    --shell "/sbin/nologin" \
    --no-create-home \
    --uid "1000" \
    appuser

# 1 - путь на хосте; 2 - путь внутри контейнера относительно рабочей директории
COPY ./app ./app
RUN python -m pip install -r ./app/requirements.txt

USER appuser

EXPOSE 8000

CMD uvicorn app.main:app --host 0.0.0.0 --port 8000

