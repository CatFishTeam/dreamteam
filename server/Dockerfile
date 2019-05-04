FROM mhart/alpine-node:11 AS builder
WORKDIR /app/server
COPY server/package.json ./
RUN yarn install --ignore-scripts
COPY server .

FROM mhart/alpine-node:11
WORKDIR /app/server
COPY --from=builder /app/server .
EXPOSE 4000
