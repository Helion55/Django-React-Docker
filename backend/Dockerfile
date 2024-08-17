# FROM python:3.8-slim-buster
# EXPOSE 8000

# WORKDIR /app

# ENV PYTHONDONTWRITEBYTECODE 1
# ENV PYTHONUNBUFFERED 1

# ENV DB_HOST database
# ENV DB_PORT 5432
# ENV DB_USER django
# ENV DB_NAME django
# ENV DB_PWD django

# COPY ./requirements.txt .
# RUN pip3 install -r requirements.txt

# COPY . .

# # RUN python3 manage.py makemigrations
# RUN python3 manage.py migrate
# CMD [ "python3", "manage.py", "runserver"]



# FROM python:3.11.5-slim-bullseye


# ENV PIP_DISABLE_PIP_VERSION_CHECK 1
# ENV PYTHONDONTWRITEBYTECODE 1
# ENV PYTHONUNBUFFERED 1

# ENV DB_HOST database
# ENV DB_PORT 5432
# ENV DB_USER django
# ENV DB_NAME django
# ENV DB_PWD django


# WORKDIR /code


# COPY ./requirements.txt .
# RUN pip install -r requirements.txt


# COPY . .

# RUN python3 manage.py makemigrations
# RUN python3 manage.py migrate


FROM python:3.7.3-stretch

ENV PYTHONUNBUFFERED 1

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY . .

EXPOSE 8000

# ENTRYPOINT [ "./django.sh" ]
RUN python manage.py makemigrations
# RUN python manage.py migrate
# CMD python manage.py runserver 0.0.0.0:8000
