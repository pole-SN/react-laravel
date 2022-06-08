FROM node:18-alpine

WORKDIR /app/react

RUN apk update && \
    npm install --save prop-types && \
    npm install -g create-react-app

ADD /app-react-frontend/package.json /app/react
RUN npm install