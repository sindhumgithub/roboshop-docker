#Build & Compile your IMAGE
FROM maven:3.5 as build
WORKDIR /opt/shipping
COPY *.xml /opt/shipping/ 
COPY src /opt/shipping/src/
RUN mvn clean package && \
    mv target/shipping-1.0.jar shipping.jar


#Docker code to RUN the container.
FROM eclipse-temurin:17-jre-alpine
# Create same user and group in final stage
RUN addgroup -S roboshop && \
    adduser -S -G roboshop -h /opt/shipping -s /sbin/nologin roboshop 
USER roboshop
EXPOSE 8080
LABEL project_name="Roboshop" \
      components="shipping" \
      created_by="Sindhuja"
WORKDIR /opt/shipping
COPY --from=build --chown=roboshop:roboshop /opt/shipping/shipping.jar .
ENV CART_ENDPOINT="cart:8080" \
    DB_HOST="mysql"
CMD ["java","-jar","/opt/shipping/shipping.jar"]


##############################################################################
# FROM maven:3.5
# RUN useradd --system --home /opt/shipping/ --shell /sbin/nologin --comment "roboshop system user" roboshop
# USER roboshop
# EXPOSE 8080
# WORKDIR /opt/shipping
# COPY *.xml /opt/shipping/ 
# COPY src /opt/shipping/src/
# RUN mvn clean package && \
#     mv target/shipping-1.0.jar shipping.jar
# ENV CART_ENDPOINT="cart:8080" \
#     DB_HOST="mysql"
# CMD ["java","-jar","/opt/shipping/shipping.jar"]




