# syntax=docker/dockerfile:1
FROM node:20-alpine

WORKDIR /app

# Solo dependencias de producción dentro de la imagen final
COPY package*.json ./
RUN npm ci --only=production

COPY . .

EXPOSE 3000
ENV PORT=3000

CMD ["node", "server.js"]
