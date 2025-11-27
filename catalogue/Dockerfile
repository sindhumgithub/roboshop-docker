#Build & Compile your IMAGE
FROM node:20.19.5-alpine3.22 as build
WORKDIR /opt/catalogue
COPY *.json *.js /opt/catalogue/
RUN npm install

#Docker code to RUN the container.
FROM node:20.19.5-alpine3.22
# Create same user and group in final stage
RUN addgroup -S roboshop && \
    adduser -S -G roboshop -h /opt/catalogue -s /sbin/nologin roboshop 
EXPOSE 8080
LABEL project_name="Roboshop" \
      components="catalogue" \
      created_by="Sindhuja"
WORKDIR /opt/catalogue/
COPY --from=build --chown=roboshop:roboshop /opt/catalogue/ /opt/catalogue/
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
USER roboshop
CMD ["node","/opt/catalogue/server.js"]


###########################################################
# FROM node:20
# RUN useradd --system --home /opt/catalogue/ --shell /sbin/nologin --comment "roboshop system user" roboshop
# USER roboshop
# WORKDIR /opt/catalogue/
# COPY *.json *.js /opt/catalogue/
# RUN npm install 
# ENV MONGO="true" \
#     MONGO_URL="mongodb://mongodb:27017/catalogue"
# CMD ["node","/opt/catalogue/server.js"]


