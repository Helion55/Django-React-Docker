FROM node:alpine

EXPOSE 3000
EXPOSE 5173

WORKDIR /app

COPY . .

RUN npm ci

CMD ["npx", "vite", "--host"]

