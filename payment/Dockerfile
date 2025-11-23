FROM python:3.10
#RUN useradd --system --home /opt/payment/ --shell /sbin/nologin --comment "roboshop system user" roboshop
# USER roboshop
WORKDIR /opt/payment/
COPY *.py *.ini *.txt /opt/payment/
RUN pip3 install -r requirements.txt
ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    AMQP_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123"
CMD ["uwsgi", "--ini", "payment.ini"]

