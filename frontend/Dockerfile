FROM node:14-alpine AS base

WORKDIR /app

COPY package.json .
RUN npm install

EXPOSE 3000

ENTRYPOINT ["npm", "start"]

#--------------------------------------#
FROM base AS builder

COPY . .
RUN npm build

#--------------------------------------#
FROM nginx:alpine
COPY --from=builder /app/build /usr/share/nginx/html