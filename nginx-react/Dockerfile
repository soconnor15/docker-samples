# Production build
# multi-stage build using container to build/compile,
# discarding artifacts in node container and only copying code
# to clean nginx container serving static source
FROM node:16.19.1-bullseye-slim AS builder
WORKDIR /opt/myapp
#Install libraries needed to compile code - npm layer - omit dev-dependencies
COPY package*.json ./
RUN npm ci --omit=dev
#Copy source from dev-local to builder image and compile - source layer
COPY . .
RUN npm run build
#Using nginx to serve static client source
FROM nginx:1.22.1
EXPOSE 3000
#Copy nginx configuration file to nginx image
COPY ./my_app.conf /etc/nginx/conf.d/default.conf
#copy compiled source from builder image to nginx image
COPY --from=builder /opt/myapp/build/ /usr/share/nginx/html
# You can optionally build/compile with node/react locally and copy
# into an nginx container instead using dockerfile.buildlocal