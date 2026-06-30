FROM node:20.20.2-alpine3.22 AS builder 
WORKDIR /opt/server 
COPY package.json .
COPY *.js .
RUN npm install

FROM node:20.20.2-alpine3.22
WORKDIR /opt/server
EXPOSE 8080
LABEL project="roboshop" \
      component="user"
ENV MONGO=true \
    REDIS_URL="redis://redis:6379" \
    MONGO_URL="mongodb://mongodb:27017/users"
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
RUN chown -R roboshop:roboshop /opt/server
COPY --from=builder /opt/server /opt/server
USER roboshop
CMD [ "server.js" ]
ENTRYPOINT [ "node" ] 

# FROM node:20 
# WORKDIR /opt/server
# EXPOSE 8080
# COPY package.json .
# COPY *.js .
# RUN npm install
# ENV MONGO=true \
#     REDIS_URL="redis://redis:6379" \
#     MONGO_URL="mongodb://mongodb:27017/users"
# CMD ["node", "server.js"]