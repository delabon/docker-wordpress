FROM node:16.20.2-slim

ARG UID=1000
ARG GID=1000

WORKDIR /code

RUN npm install -g pnpm

RUN groupmod -g "${GID}" node && usermod -u "${UID}" -g "${GID}" node

USER node
