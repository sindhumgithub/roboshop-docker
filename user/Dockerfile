#Build & Compile your IMAGE
FROM node:20.19.5-alpine3.22 as build
WORKDIR /opt/user
COPY *.json *.js /opt/user/
RUN npm install


#Docker code to RUN the container.
FROM node:20.19.5-alpine3.22
# Create same user and group in final stage
RUN addgroup -S roboshop && \
    adduser -S -G roboshop -h /opt/user -s /sbin/nologin roboshop 
EXPOSE 8080
LABEL project_name="Roboshop" \
      components="user" \
      created_by="Sindhuja"
WORKDIR /opt/user/
COPY --from=build --chown=roboshop:roboshop /opt/user/ /opt/user/
ENV MONGO="true" \
    REDIS_URL="redis://redis:6379" \
    MONGO_URL="mongodb://mongodb:27017/users"
USER roboshop
CMD ["node","/opt/user/server.js"]

###########################################################################
# FROM node:20
# RUN useradd --system --home /opt/user/ --shell /sbin/nologin --comment "roboshop system user" roboshop
# USER roboshop
# WORKDIR /opt/user/
# COPY *.json *.js /opt/user/
# RUN npm install 
# ENV MONGO="true" \
#     REDIS_URL="redis://redis:6379" \
#     MONGO_URL="mongodb://mongodb:27017/users"
# CMD ["node","/opt/user/server.js"]
# EXPOSE 8080