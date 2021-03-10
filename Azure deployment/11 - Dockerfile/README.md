# Creating a Dockerfile for Blitz

Since we want to run this in Azure we need to dockerize the application. Add the following Dockerfile to your application

```dockerfile
FROM node:12 as builder
WORKDIR /app

COPY . .

RUN npm install --production
RUN cp -r node_modules/ /tmp/prod_modules/

RUN npm install
ENV NODE_ENV production

RUN npx blitz build

FROM node:slim as prod
WORKDIR /app
RUN apt-get -qy update && apt-get -qy install openssl
COPY --from=builder /app/.blitz ./.blitz
COPY --from=builder /tmp/prod_modules/ ./node_modules
COPY --from=builder /app/.next ./.next
COPY --from=builder /app/package.json ./

ENV PORT 3000
EXPOSE 3000

CMD npx blitz start --production
```

We use a regular node:12 image for building the application, while a slim image for production. This allows us to save some space on the final image.

From the build image we copy the build result stored in the .blitz and .next folders. In addition we need the node_modules for production, package.json and the db directory.
