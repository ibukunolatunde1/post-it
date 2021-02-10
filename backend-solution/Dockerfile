#Build Stage
FROM node:12 as build

WORKDIR /usr/src/app

COPY package*.json /usr/src/app/

RUN npm ci --only=production

#Production Stage

FROM node:lts-alpine

ENV NODE_ENV production
 
# ENV DB_URL mongodb://admin:password@mongodb:27017/test?authSource=admin

# ENV SECRET somesupersecret
#Add other envs

USER node

WORKDIR /usr/src/app

COPY --chown=node:node --from=build /usr/src/app/node_modules/ /usr/src/app/node_modules/

COPY --chown=node:node . /usr/src/app/

CMD ["npm", "start"]