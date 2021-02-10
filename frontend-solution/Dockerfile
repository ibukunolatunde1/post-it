#Build Stage
FROM node:12 as build

WORKDIR /usr/src/app

COPY package*.json /usr/src/app/

COPY . .

RUN npm ci --only=production

RUN npm run build

#Production Stage

FROM node:12-alpine

ENV NODE_ENV production

WORKDIR /usr/src/app/

RUN npm install -g serve

COPY --from=build /usr/src/app/build/ /usr/src/app/build/

CMD ["serve", "-s", "build"]