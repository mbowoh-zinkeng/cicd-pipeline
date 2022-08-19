# build stage
FROM node:lts-alpine as build-stage
WORKDIR /app
COPY package*.json ./
RUN npm i
COPY . .

#RUN NODE_OPTIONS=--max-old-space-size=4096 npm run build
# production stage
FROM nginx:stable as deployment
COPY --from=build-stage /app/build /var/www
RUN rm /etc/nginx/conf.d/default.conf
COPY ./nginx.conf /etc/nginx/conf.d/default.conf