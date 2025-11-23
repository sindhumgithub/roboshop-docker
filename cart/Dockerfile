FROM node:20
RUN useradd --system --home /opt/cart/ --shell /sbin/nologin --comment "roboshop system user" roboshop
USER roboshop
WORKDIR /opt/cart/
COPY *.json *.js /opt/cart/
RUN npm install
ENV REDIS_HOST="redis" \
ENV CATALOGUE_HOST="catalogue" \
ENV CATALOGUE_PORT="8080"
CMD ["node","/opt/cart/server.js"]

