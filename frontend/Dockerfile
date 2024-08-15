FROM node:alpine

EXPOSE 5173

WORKDIR /app

ENV VITE_API_URL=http://127.0.0.1:8000

COPY . .

RUN npm i

CMD ["npm", "run", "dev"]

