FROM node:alpine
WORKDIR /app
COPY . .
ENV VITE_API_URL=http://127.0.0.1:8000
RUN npm ci
CMD ["npx", "vite", "--host"]
EXPOSE 3000
