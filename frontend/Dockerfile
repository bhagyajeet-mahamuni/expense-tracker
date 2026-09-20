#FROM node:22-alpine
#
#WORKDIR /app
#
#ENV NODE_OPTIONS=--max-old-space-size=768
#
#COPY package*.json ./
#
#RUN npm install
#
#COPY . .
#
#RUN npm run build
#
#CMD ["npm","run","dev","--","--host","0.0.0.0"]
#

#==================================== Stage 1

FROM node:22-alpine AS builder

WORKDIR /app 

ENV NODE_OPTIONS=--max-old-space-size=768 

COPY package*.json ./  

RUN npm install    ##  It stores files inside /app/node_modules

COPY . . 

ARG VITE_API_BASE_URL

ENV VITE_API_BASE_URL=$VITE_API_BASE_URL

RUN npm run build  ## It stores file in /app/dist folder

#=======================================Stage 2

FROM node:22-alpine AS runner

WORKDIR /app

COPY --from=builder /app/dist ./dist

COPY --from=builder /app/package*.json ./

#COPY vite.config.js ./vite.config.js


RUN npm install --production   ## This will create new node_modules which will install only prod dependencies.


EXPOSE 4173

CMD ["npm","run","preview","--","--host","0.0.0.0"]

#CMD ["node","./node_modules/.bin/vite", "preview", "--host", "0.0.0.0"]

#CMD ["npm", "exec", "--", "vite", "preview", "--host", "0.0.0.0"]
