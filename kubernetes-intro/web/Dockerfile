FROM nginx:mainline-alpine
RUN rm /etc/nginx/conf.d/*
COPY web-app.conf /etc/nginx/conf.d/
COPY *.html /usr/share/nginx/html
