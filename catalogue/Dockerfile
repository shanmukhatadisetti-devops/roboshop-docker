# FROM node:20
# WORKDIR /opt/server
# EXPOSE 8080
# COPY package.json .
# COPY *.js .
# RUN npm install
# ENV MONGO=true \
#     MONGO_URL="mongodb://mongodb:27017/catalogue"
# CMD ["node","server.js"]

FROM node:20.20.2-alpine3.22 AS builder 
WORKDIR /opt/server 
COPY package.json .
COPY *.js .
RUN npm install

FROM node:20.20.2-alpine3.22
WORKDIR /opt/server
EXPOSE 8080
LABEL project="roboshop" \
      component="catalogue"
ENV MONGO=true \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
RUN chown -R roboshop:roboshop /opt/server
COPY --from=builder /opt/server /opt/server
USER roboshop
CMD [ "server.js" ]
ENTRYPOINT [ "node" ] 