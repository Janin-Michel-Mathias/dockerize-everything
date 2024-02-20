FROM node:lts

EXPOSE 3000/tcp

WORKDIR /app

COPY . .

COPY .env.example .env

RUN npm install

RUN npm run build

CMD node /app/build/index.js