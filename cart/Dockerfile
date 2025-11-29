#Build & Compile your IMAGE
FROM node:20.19.5-alpine3.22 as build
WORKDIR /opt/cart
COPY *.json *.js /opt/cart/
RUN npm install


#Docker code to RUN the container.
FROM node:20.19.5-alpine3.22
# Create same user and group in final stage
RUN addgroup -S roboshop && \
    adduser -S -G roboshop -h /opt/cart -s /sbin/nologin roboshop 
EXPOSE 8080
LABEL project_name="Roboshop" \
      components="cart" \
      created_by="Sindhuja"
WORKDIR /opt/user/
COPY --from=build --chown=roboshop:roboshop /opt/cart/ /opt/cart/
ENV REDIS_HOST="redis" \
    CATALOGUE_HOST="catalogue" \
    CATALOGUE_PORT="8080"
USER roboshop
CMD ["node","/opt/cart/server.js"]

##################################################################################
# FROM node:20
# RUN useradd --system --home /opt/cart/ --shell /sbin/nologin --comment "roboshop system user" roboshop
# USER roboshop
# WORKDIR /opt/cart/
# COPY *.json *.js /opt/cart/
# RUN npm install
# ENV REDIS_HOST="redis" \
#     CATALOGUE_HOST="catalogue" \
#     CATALOGUE_PORT="8080"
# CMD ["node","/opt/cart/server.js"]

