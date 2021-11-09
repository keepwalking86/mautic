FROM nginx:1.13

COPY default.conf /etc/nginx/conf.d/default.conf

#VOLUME /var/log/nginx/mautic

WORKDIR /var/www

#RUN chown -R nginx:nginx /var/www/mautic

#Change nginx uid & gid
RUN usermod -u 1000 nginx && groupmod -g 1000 nginx

CMD ["nginx", "-g", "daemon off;"]

EXPOSE 80
