FROM node:16-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . ./
RUN npm run build

FROM node:16-alpine AS backend
WORKDIR /app
COPY ./package*.json ./
RUN npm install --omit=dev && npm i pm2 -g
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/ecosystem.config.js .
COPY ./.env ./
CMD ["pm2-runtime", "start", "ecosystem.config.js"]
