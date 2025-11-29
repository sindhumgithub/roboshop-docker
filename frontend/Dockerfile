# To create frontend as Normal user 
FROM nginx:1.27-alpine
RUN rm -f /etc/nginx/conf.d/default.conf

#install nginx
RUN mkdir -p /var/cache/nginx/client_temp && \
        mkdir -p /var/cache/nginx/proxy_temp && \
        mkdir -p /var/cache/nginx/fastcgi_temp && \
        mkdir -p /var/cache/nginx/uwsgi_temp && \
        mkdir -p /var/cache/nginx/scgi_temp && \
        chown -R nginx:nginx /var/cache/nginx && \
        chown -R nginx:nginx /etc/nginx/ && \
        chmod -R 755 /etc/nginx/ && \
        chown -R nginx:nginx /var/log/nginx

RUN mkdir -p /etc/nginx/ssl/ && \
    chown -R nginx:nginx /etc/nginx/ssl/ && \
    chmod -R 755 /etc/nginx/ssl/

RUN touch /var/run/nginx.pid && \
        chown -R nginx:nginx /var/run/nginx.pid /run/nginx.pid
COPY nginx.conf /etc/nginx/nginx.conf
COPY static/ /usr/share/nginx/html/
RUN chown -R nginx:nginx /var/cache/nginx /var/log/nginx /var/run/nginx.pid \
    && mkdir -p /etc/nginx/ssl \
    && chown -R nginx:nginx /etc/nginx/ssl
USER nginx
CMD ["nginx", "-g", "daemon off;"]






# FROM nginx:1.24
# RUN rm -rf /usr/share/nginx/html/* && \
#     rm -rf /etc/nginx/conf.d/default.conf && \
#     rm -rf /etc/nginx/nginx.conf
# COPY static/ /usr/share/nginx/html/
# COPY nginx.conf /etc/nginx/nginx.conf