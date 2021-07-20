FROM nginx:1.15.3-alpine

MAINTAINER alex.yao "crazyrico@qq.info"

COPY ./nginx/nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 3001

CMD ["nginx", "-g", "daemon off;"]