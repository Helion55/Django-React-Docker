FROM python:3.8-slim-buster
EXPOSE 8000

WORKDIR /app

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

ENV DB_HOST database
ENV DB_PORT 5432
ENV DB_USER django
ENV DB_NAME django
ENV DB_PWD django

COPY ./requirements.txt .
RUN pip3 install -r requirements.txt

COPY . .

RUN python3 manage.py makemigrations
RUN python3 manage.py migrate
CMD [ "python3", "manage.py", "runserver"]

