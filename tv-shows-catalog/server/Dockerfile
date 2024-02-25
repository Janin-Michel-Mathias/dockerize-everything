FROM node:lts-alpine AS default

EXPOSE ${PORT}

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

#DEV
FROM default AS development
CMD npm run start:dev

#PROD
FROM default AS production

RUN npm run build

CMD node /app/dist/main.js