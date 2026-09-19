#FROM node:22-alpine
#
#WORKDIR /app
#
#COPY package*.json ./
#
#RUN npm install   ## It will create node_modules directory
#
#COPY . .
#
#EXPOSE 5000
#
#CMD ["npm","run","dev"]

##============================= Stage 1

FROM node:22-alpine AS builder

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

#=============================== Stage 2

FROM node:22-alpine AS runner

WORKDIR /app

COPY --from=builder /app ./

RUN npm install --production

EXPOSE 5000

CMD ["npm","start"]
