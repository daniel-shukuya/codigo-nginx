FROM registry.access.redhat.com/ubi8/nginx-118

# Add application sources
ADD nginx/nginx.conf "${NGINX_CONF_PATH}"
ADD nginx/nginx-default-cfg/*.conf "${NGINX_DEFAULT_CONF_PATH}"
ADD nginx/nginx-cfg/*.conf "${NGINX_CONFIGURATION_PATH}"
ADD nginx/index.html .
# prueba (agrego poster)
ADD nginx/1.jpg ./provider/amzn/1.jpg
ADD nginx/2.jpg ./provider/amzn/2.jpg
# esta linea es para el montaje en openshift (ya que hay que copiar el contenido despues de montar el pvc. Igual me parece que no es necesario ya que las imagenes suben por otro lado)
ADD nginx/index.html /app/index.html

RUN mkdir -p /tmp/nginx/cache/amzn
RUN mkdir -p /tmp/nginx/cache/pmnt

RUN chgrp -R 0 /tmp/nginx/cache && chmod -R g=u /tmp/nginx/cache

USER 0
# modifico carpeta de compartidos
RUN chgrp -R 0 ./provider && chmod -R g=u ./provider
USER 1001
# Run script uses standard ways to run the application
CMD nginx -g "daemon off;"
