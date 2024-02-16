FROM node:lts

EXPOSE 3000/tcp

WORKDIR /app

COPY . .

RUN npm install

RUN npm run build

CMD node /app/dist/main.js