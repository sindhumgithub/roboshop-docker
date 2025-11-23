FROM maven:3.5
RUN useradd --system --home /opt/shipping/ --shell /sbin/nologin --comment "roboshop system user" roboshop
USER roboshop
EXPOSE 8080
WORKDIR /opt/shipping
COPY *.xml /opt/shipping/ 
COPY src /opt/shipping/src/
RUN mvn clean package && \
    mv target/shipping-1.0.jar shipping.jar
ENV CART_ENDPOINT="cart:8080" \
    DB_HOST="mysql"
CMD ["java","-jar","/opt/shipping/shipping.jar"]




