FROM mhart/alpine-node:11 AS builder
WORKDIR /app/web
COPY web/package.json .
RUN yarn install --pure-lockfile
COPY web .

FROM mhart/alpine-node:11
WORKDIR /app/web
COPY --from=builder /app/web .
EXPOSE 3000
