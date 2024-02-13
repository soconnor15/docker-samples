#production build node
FROM node:16.19.1-alpine
WORKDIR /opt/app
EXPOSE 5000
#Version must be defined
RUN apk add build-base=0.5-r3 && rm -rf /var/lib/apt/lists/*
COPY package*.json ./
RUN npm ci --omit=dev
COPY . .
# server start; you could alternately use an entrypoint
CMD ["node", "./bin/www"]