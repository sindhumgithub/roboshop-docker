#Build & Compile your IMAGE
FROM python:3.9.25-alpine3.21 AS builder
WORKDIR /opt/payment
# Build deps for uwsgi & friends
RUN apk add --no-cache \
    build-base \
    linux-headers \
    pcre-dev
# Only requirements first for caching
COPY requirements.txt .
# Install into /install (just like you did)
RUN pip3 install --prefix=/install -r requirements.txt


#Docker code to RUN the container.
FROM python:3.9.25-alpine3.21
EXPOSE 8080
WORKDIR /opt/payment/
# Runtime deps only
RUN apk add --no-cache pcre libstdc++
# Create normal user.
RUN addgroup -S roboshop && \
    adduser -S -G roboshop -h /opt/catalogue -s /sbin/nologin roboshop 
USER roboshop
# Copy installed packages from build stage
COPY --from=builder /install /usr/local
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

