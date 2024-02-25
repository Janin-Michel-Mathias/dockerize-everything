FROM node:lts-alpine AS default
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm install
COPY . .
EXPOSE ${PORT}

FROM default AS development
COPY .env.example .env
CMD npm run dev

#PRE-PROD
FROM default AS preview
COPY .env.preview .env
EXPOSE ${PORT}
CMD npm run build && npm run preview

#PROD
FROM default AS production
COPY .env.production .env
RUN npm run build
EXPOSE ${PORT}
CMD node /app/build/index.js