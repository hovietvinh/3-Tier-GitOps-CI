FROM node:18-alpine AS build
WORKDIR /app
COPY package*.json ./
RUN npm ci --ignore-scripts
COPY . .

ARG REACT_APP_API
ENV REACT_APP_API=$REACT_APP_API

RUN npm run build 

FROM nginxinc/nginx-unprivileged:alpine

COPY default.conf /etc/nginx/conf.d/default.conf

COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]