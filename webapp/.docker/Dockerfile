FROM node:16-alpine as dev-stage
WORKDIR /app
COPY package*.json yarn.lock ./
RUN yarn global add @quasar/cli@latest
RUN yarn global add pm2@latest
COPY . .

FROM dev-stage as local-deps-stage
RUN yarn

FROM local-deps-stage as build-stage
RUN quasar build -m ssr
CMD ["pm2-runtime", "dist/ssr/index.js"]
