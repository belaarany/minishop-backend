FROM python:3.9-slim-buster

WORKDIR /app
COPY . .
RUN pip install --upgrade pip
RUN pip install -r ./requirements.txt

CMD sleep 10 && python3 ./src/main.py