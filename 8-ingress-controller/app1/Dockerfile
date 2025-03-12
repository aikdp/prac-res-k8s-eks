FROM nginx:stable-perl
RUN rm -rf /usr/share/nginx/html
WORKDIR /usr/share/nginx/html/
RUN echo "<h1>Hi I am from APP-1 Using Kubernetes Ingress Resource</h1>" > index.html
CMD ["nginx", "-g", "daemon off;"]