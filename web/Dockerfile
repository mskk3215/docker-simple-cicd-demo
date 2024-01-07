FROM node:18 as base
CMD [ "bash" ]

#Build
FROM base AS build
COPY . /workspace
WORKDIR /workspace
ARG REACT_APP_API_SERVER
#npm ciはpackage.jsonをインストールするバーション管理コマンド
RUN npm ci  && npm run build

# Hosting in nginx
FROM nginx:latest AS production
COPY --from=build /workspace/build /var/www
COPY ./nginx.conf /etc/nginx/conf.d/default.conf
