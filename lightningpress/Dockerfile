FROM wordpress:latest

RUN apt-get update \
&&  apt-get install -y \
    unzip \
    git \
&&  git clone https://github.com/joaodealmeida/woocommerce-gateway-lightning \
    /usr/src/wordpress/wp-content/plugins/woocommerce-gateway-lightning \
&&  curl -L https://github.com/woocommerce/woocommerce/releases/download/3.4.0-beta.1/woocommerce.zip \
    -o woocommerce.zip \
&&  unzip woocommerce.zip -d /usr/src/wordpress/wp-content/plugins \
&&  chown -R www-data:www-data /usr/src/wordpress/wp-content/plugins/

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["apache2-foreground"]
