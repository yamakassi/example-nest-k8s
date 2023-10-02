FROM node:18-alpine3.17 AS development

WORKDIR ./app

# Установить зависимости
COPY package*.json ./
RUN npm i -g @nestjs/cli
RUN npm install

COPY . .

RUN npm run build

# образ для production 
FROM node:18-alpine3.17 AS production

ARG NODE_ENV=production
ENV NODE_ENV=${NODE_ENV}

WORKDIR ./app

COPY package*.json ./
RUN npm install --only=production
COPY . .
COPY --from=development ./app/dist ./dist

CMD ["node", "dist/main"]