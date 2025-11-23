FROM node:20
RUN useradd --system --home /opt/catalogue/ --shell /sbin/nologin --comment "roboshop system user" roboshop
USER roboshop
WORKDIR /opt/catalogue/
COPY *.json *.js /opt/catalogue/
RUN npm install 
ENV MONGO="true" \
    MONGO_URL="mongodb://mongodb:27017/catalogue"
CMD ["node","/opt/catalogue/server.js"]


