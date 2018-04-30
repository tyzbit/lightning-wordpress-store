# lightning-wordpress-store
Quickly spin up a Lightning-enabled Wordpress Store

# Quickstart:

Run this and wait for the containers to come up.
```
docker-compose up -d
```

1. Once started, go to http://127.0.0.1:8080, and run through the WordPress setup.

2. Log into WordPress, go to Plugins and enable WooCommerce Lightning Gateway.

3. Enable WooCommerce and then run through the setup there.

   *I suggest denominating in local currency, and not enabling Stripe or PayPal.*

4. Create a new product, and set a price for it.

5. Go to WooCommerce -> Settings -> Payments and click Set Up on Bitcoin Lightning.

6. Enable the payment method.

7. Change the endpoint to https://lnd:8080

8. Take the output of `docker exec -it lnd xxd -p -c 1000 /root/.lnd/invoice.macaroon`
and paste it into Macaroon Hex

9. Run these commands:
```
docker cp lnd:/root/.lnd/tls.cert tls.cert
docker exec -it lightningpress mkdir /var/www/html/wp-content/plugins/woocommerce-gateway-lightning/tls
docker cp tls.cert lightningpress:/var/www/html/wp-content/plugins/woocommerce-gateway-lightning/tls/tls.cert
docker exec -it lightningpress chown www-data:www-data /var/www/html/wp-content/plugins/woocommerce-gateway-lightning/tls -R
rm tls.cert
```

10. (Optional) Go to Settings -> Reading and set your homepage to the shop.

The next step would be to use Apache or Nginx to reverse proxy to your WordPress site.

Syncing testnet will probably take some hours.
