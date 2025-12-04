ARG NODE_VERSION=20
ARG NGINX_VERSION=alpine

FROM node:${NODE_VERSION} AS build-stage

WORKDIR /app

COPY package*.json ./

RUN npm ci --legacy-peer-deps || npm install --legacy-peer-deps

COPY . .

ENV NODE_ENV=production
RUN npm run build

FROM nginx:${NGINX_VERSION} AS production-stage

RUN rm -rf /usr/share/nginx/html

COPY --from=build-stage /app/dist /usr/share/nginx/html

COPY nginx.conf /etc/nginx/conf.d/default.conf

CMD ["nginx", "-g", "daemon off;"]