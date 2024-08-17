# Containerizing a React Notes application using Django as backend and Postgres as Database.
A Notes application using authentication system to signup and login with JWT Tokens, using Django as backend which is connected with PostgresSQL to store data and frontend made with React.

![Diagram](https://github.com/Helion55/Django-React-Docker/blob/main/Django-React.jpg?raw=true)

## Tech Stack
- Django 
- React
- Postgres
- Docker - Compose

## Django
The backend is running on port 8000 and connecting with database through the environment variables passed from Dockerfile. Here is the Dockerfile ...
```Dockerfile
FROM python:3.7.3-stretch

ENV PYTHONUNBUFFERED 1

WORKDIR /app

COPY requirements.txt .

RUN pip install -r requirements.txt

COPY . .

EXPOSE 8000

RUN python manage.py makemigrations
```
## React
React is used for the frontend with Vite server, serving on port 5173, Dockerfile for the frontend ...
```Dockerfile
FFROM node:alpine

EXPOSE 3000
EXPOSE 5173

WORKDIR /app

COPY . .

RUN npm ci

CMD ["npx", "vite", "--host"]
```
### Postgres
Postgres is used to store the data, which running on a container running on docker compose stack, running on port 5432 and mounted a volume named ``` postgres_data ```.

### Docker
Whole application stack running on docker compose stack and the Dockerfiles are also created on the directory of frontend and backend, this is the compose file ...
```yaml
services:
  db:
    container_name: db
    image: postgres:12
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
      - POSTGRES_DB=postgres
    ports:
      - "5432:5432"
    volumes:
      - pgdata:/var/lib/postgresql/data
  backend:
    container_name: backend
    build: ./backend
    ports:
      - "8000:8000"
    environment:
      - DB_USER=postgres
      - DB_PWD=postgres
      - DB_DB=postgres
      - DB_HOST=db
      - DB_PORT=5432
    command: python manage.py migrate && python manage.py runserver 0.0.0.0:8000
    depends_on:
      - db
  frontend:
    build: ./frontend
    ports:
      - 5173:5173
      - 3000:3000
    environment:
      - VITE_API_URL= http://0.0.0.0:8000/

    depends_on:
      - backend

volumes:
  pgdata: {}
```
After applying the command
```
docker compose up
```
the whole application stack will start to run. This Docker Images can also be used to deploy on Kubernetes Cluster.

### Contributing 
I will be very glad to any contributions made to this project.