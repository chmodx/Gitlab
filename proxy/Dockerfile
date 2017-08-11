FROM nginx:latest
ARG SSL=non-ssl
ARG LOGIN=testuser
ARG PASSWD=testpasswd
ARG GITLAB_HOST
ARG REGISTRY_HOST
ENV GITLAB $GITLAB_HOST
ENV REGISTRY $REGISTRY_HOST
ENV DOLLAR '$'
RUN apt-get update -y
RUN rm /etc/nginx/conf.d/default.conf
RUN mkdir /cert
RUN apt-get install apache2-utils -y
RUN touch /etc/nginx/conf.d/gitlab.conf /etc/nginx/conf.d/registry.conf
RUN htpasswd -cbd /etc/nginx/conf.d/registry.htpasswd $LOGIN $PASSWD 
COPY ./conf/${SSL}/gitlab.template ./conf/${SSL}/registry.template ./
RUN envsubst < gitlab.template > /etc/nginx/conf.d/gitlab.conf
RUN envsubst < registry.template > /etc/nginx/conf.d/registry.conf
