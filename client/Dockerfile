FROM node:16-alpine as builder
RUN addgroup app && adduser -S -G app app
RUN mkdir /app && chown app:app /app
USER app
WORKDIR '/app'
COPY ./package.json ./
RUN npm config set unsafe-perm true
RUN npm install --unsafe-perm=true --allow-root
COPY --chown=app:app . .
RUN npm run build

FROM nginx
EXPOSE 3000
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf
COPY --from=builder /app/build /usr/share/nginx/html