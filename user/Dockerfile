FROM node:20
RUN useradd --system --home /app --shell /sbin/nologin --comment "roboshop system user" roboshop
USER roboshop
WORKDIR /opt/user
COPY --chown=roboshop:roboshop *.json *.js /opt/user
RUN npm install 
ENV MONGO="true" \
    REDIS_URL="redis://redis:6379" \
    MONGO_URL="mongodb://mongodb:27017/users"
CMD ["node","/opt/user/server.js"]