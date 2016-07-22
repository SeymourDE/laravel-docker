FROM nginx

RUN apt-get update
RUN apt-get install vim -y

# update config
RUN cp /etc/nginx/conf.d/default.conf /etc/nginx/conf.d/laravel.conf
RUN sed -i 's/localhost/lara.dev/' /etc/nginx/conf.d/default.conf
RUN sed -i '5 s/#charset koi8-r/charset utf-8/' /etc/nginx/conf.d/default.conf
RUN sed -i "9 s/\/usr\/share\/nginx\/html/\/code\/public/" /etc/nginx/conf.d/default.conf
RUN sed -i "10 a \        try_files \$uri \$uri\/ \/index.php\?\$query_string;" /etc/nginx/conf.d/default.conf
RUN sed -i "10 s/;/ index.php;/" /etc/nginx/conf.d/default.conf

RUN sed -i "14 c\    error_page 404 /index.php;" /etc/nginx/conf.d/default.conf
RUN sed -i "18 s/error/#error/" /etc/nginx/conf.d/default.conf
RUN sed -i "20 s/\/usr\/share\/nginx\/html/\/code\/public/" /etc/nginx/conf.d/default.conf
RUN sed -i '31,37 s/#//' /etc/nginx/conf.d/default.conf
RUN sed -i '32 s/html/\/code\/public/' /etc/nginx/conf.d/default.conf
RUN sed -i '33 s/127.0.0.1/devPHP/' /etc/nginx/conf.d/default.conf
RUN sed -i '35 s/\/scripts/$document_root/' /etc/nginx/conf.d/default.conf

EXPOSE 80 443

