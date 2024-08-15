# Containerizing a React Notes application using Django as backend and Postgres as Database.
A Notes application using authentication system to signup and login with JWT Tokens, using Django as backend which is connected with PostgresSQL to store data and frontend made with React.
## Tech Stack
- Django
- React
- Postgres
- Docker - Compose

## Django
The backend is running on port 8000 and connecting with database through the environment variables passed from Dockerfile. Here is the Dockerfile ...
```Dockerfile
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
```
## React
React is used for the frontend with Vite server, serving on port 5173, Dockerfile for the frontend ...
```Dockerfile
FROM node:alpine

EXPOSE 5173

WORKDIR /app

ENV VITE_API_URL=http://127.0.0.1:8000

COPY . .

RUN npm i

CMD ["npm", "run", "dev"]
```
### Postgres
Postgres is used to store the data, which running on a container running on docker compose stack, running on port 5432 and mounted a volume named ``` postgres_data ```.

### Docker
Whole application stack running on docker compose stack and the Dockerfiles are also created on the directory of frontend and backend, this is the compose file ...
```Dockerfile
version: '3.9'

services:
  database:
    image: postgres
    volumes:
      - postgres_data:/var/lib/postgresql/data
    environment:
      - POSTGRES_DB=django
      - POSTGRES_USER=django
      - POSTGRES_PASSWORD=django
  backend:
    build: ./backend
    command: python manage.py runserver 
    ports:
      - "8000:8000"
    depends_on:
      - database

  frontend:
    build: ./frontend
    ports:
      - 5173:5173
    depends_on:
      - backend

volumes:
   postgres_data:
```
After applying the command,
```shell
docker compose up
```
the whole application stack will start to run. This Docker Images can also be used to deploy on Kubernetes Cluster.

### Contributing 
I will be very glad to any contributions made to this project.
