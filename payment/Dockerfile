#Build & Compile your IMAGE
FROM python:3.9.25-alpine3.21 AS build
WORKDIR /opt/payment/
# Copy requirements first (best for caching)
COPY requirements.txt .
RUN pip install --no-cache-dir --user -r requirements.txt


#Docker code to RUN the container.
FROM python:3.9.25-alpine3.21
# Install only the runtime binary of uWSGI (very small)
RUN apk add --no-cache uwsgi uwsgi-python3
EXPOSE 8080
RUN addgroup -S roboshop && \
    adduser -S -G roboshop -h /opt/catalogue -s /sbin/nologin roboshop 
USER roboshop
WORKDIR /opt/payment/
# Copy installed Python packages from build stage
COPY --from=build --chown=roboshop:roboshop \
     /root/.local /home/roboshop/.local
COPY --chown=roboshop:roboshop *.py *.ini *.txt /opt/payment/
ENV CART_HOST="cart" \
    CART_PORT="8080" \
    USER_HOST="user" \
    USER_PORT="8080" \
    AMQP_HOST="rabbitmq" \
    AMQP_USER="roboshop" \
    AMQP_PASS="roboshop123"
CMD ["uwsgi", "--ini", "payment.ini"]




###############################################################################################
# FROM python:3.10
# #RUN useradd --system --home /opt/payment/ --shell /sbin/nologin --comment "roboshop system user" roboshop
# # USER roboshop
# WORKDIR /opt/payment/
# COPY *.py *.ini *.txt /opt/payment/
# RUN pip3 install -r requirements.txt
# ENV CART_HOST="cart" \
#     CART_PORT="8080" \
#     USER_HOST="user" \
#     USER_PORT="8080" \
#     AMQP_HOST="rabbitmq" \
#     AMQP_USER="roboshop" \
#     AMQP_PASS="roboshop123"
# CMD ["uwsgi", "--ini", "payment.ini"]

