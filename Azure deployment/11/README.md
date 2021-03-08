# Creating a Dockerfile for Blitz

Since we want to run this in Azure we need to dockerize the application. Add the following Dockerfile to your application

```dockerfile
FROM node:12 as builder
WORKDIR /app

COPY . .

RUN npm install

ENV NODE_ENV production

RUN npx blitz build

FROM node:slim
WORKDIR /app
RUN apt-get -qy update && apt-get -qy install openssl
COPY --from=builder /app/.blitz ./.blitz
COPY --from=builder /app/.next ./.next
COPY --from=builder /app/package.json ./
COPY --from=builder /app/node_modules/ ./node_modules
COPY --from=builder /app/db ./db

ENV PORT 3000
EXPOSE 3000

CMD npx blitz prisma migrate dev --preview-feature && npx blitz start --production
```

We use a regular node:12 image for building the application, while a slim image for production. This allows us to save some space on the final image.

From the build image we copy the build result stored in the .blitz and .next folders. In addition we need the node_modules, package.json and the db directory.
To reduce the image size we could limit the dependencies to the result of `npm install --production`, but that seems to require that we do the database migration in or GitHub pipeline.
