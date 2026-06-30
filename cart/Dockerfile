FROM node:20.20.2-alpine3.22 AS builder 
WORKDIR /opt/server 
COPY package.json .
COPY *.js .
RUN npm install

FROM node:20.20.2-alpine3.22
WORKDIR /opt/server
EXPOSE 8080
LABEL project="roboshop" \
      component="cart"
ENV REDIS_HOST=redis \
    CATALOGUE_HOST=catalogue \
    CATALOGUE_PORT=8080
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
# ENV REDIS_HOST=redis \
#     CATALOGUE_HOST=catalogue \
#     CATALOGUE_PORT=8080
# CMD ["node", "server.js"]