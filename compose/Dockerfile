FROM python:3.8-slim-buster

EXPOSE 5000

ENV PYTHONDONTWRITEBYTECODE=1

ENV PYTHONBUFFERED=1

ENV FLASK_APP=app.py

ENV FLASK_RUN_HOST=0.0.0.0

WORKDIR /app

# RUN apk add --no-cache gcc musl-dev linux-headers

COPY requirements.txt requirements.txt

RUN pip install -r requirements.txt

COPY . .

CMD ["flask", "run"]