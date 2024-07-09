FROM node:20

WORKDIR /app

COPY . .

RUN npm install

EXPOSE 5173

CMD ["npm", "run", "dev", "--", "--host"]

FROM nginx:latest
COPY ./nginx.conf /etc/nginx/conf.d/default.conf