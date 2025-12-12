#stage 1: build react
FROM node:16 AS BUILD
WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build 

#stage 2: serve with nginx
FROM nginx:stable
COPY --from=BUILD /app/build /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]