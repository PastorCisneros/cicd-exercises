FROM node:lts-alpine3.14

WORKDIR /app-cd

COPY app/ .

RUN npm install

ENV PORT=8084

ENTRYPOINT [ "npm", "start"]