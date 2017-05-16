# dsinfra

Configuration for my personal infrastructure. Terraform manages AWS resources
and performs some simple bootstrapping with cloud-init (adds user + SSH keys).
Ansible then provisions instances.

## spark
 - [Gogs](https://gogs.io/)

## TODO

### Mutual SSL

Generate keys

    openssl req -x509 -nodes -newkey rsa:4096 -keyout client.key -out client.crt

Put client key on webserver at `/etc/nginx/ssl/trust/client.crt`

Nginx conf:

    server {
        ...

        ssl_client_certificate /etc/nginx/ssl/trust/client.crt;
        ssl_verify_client on;

        ...
    }

Firefox wants a PKCS#12 archive:

    openssl pkcs12 -export -in ~/client.crt -inkey ~/client.key -name "Adhoc" -out adhoc.p12
    # adhoc.p12 can be imported into the browser
    rm client.key
