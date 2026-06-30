FROM maven:3.9.11 AS builder
WORKDIR /opt/server
COPY src ./src
COPY pom.xml .
RUN mvn clean package 
RUN mv target/shipping-1.0.jar shipping.jar 

FROM eclipse-temurin:17-jre-alpine
WORKDIR /opt/server
EXPOSE 8080
LABEL project="roboshop" \
      component="shipping"
ENV CART_ENDPOINT="cart:8080"\
    DB_HOST="mysql"
RUN addgroup -S roboshop && adduser -S roboshop -G roboshop
COPY --from=builder --chown=roboshop:roboshop /opt/server/shipping.jar .
USER roboshop
ENTRYPOINT [ "java", "-jar", "shipping.jar" ]
# FROM maven:3.9.11
# WORKDIR /opt/server
# EXPOSE 8080
# COPY src ./src
# COPY pom.xml .
# RUN mvn clean package 
# RUN mv target/shipping-1.0.jar shipping.jar 
# ENV CART_ENDPOINT="cart:8080"\
#     DB_HOST="mysql"
# CMD ["java", "-jar", "shipping.jar"]