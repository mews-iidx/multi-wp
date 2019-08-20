# multi wp

nginx reverse proxy and multiple workdpress.

# example domains
| domain name   | domain type  |
| -----------   | -----------  |
| hoge.com      | A record     |
| fuga.hoge.com | CNAME record |
fix your domain.

# clone repository
```sh
git clone https://github.com/mews-iidx/multi-wp
```

# Get Let's Encrypt CERT
## install certbot
```sh
apt install certbot
```

## veryfication
```sh
certbot certonly --webroot -w /usr/share/nginx/html -d hoge.com -d fuga.hoge.com
```
## copy and rename
```sh
cp /etc/letsencrypt/live/hoge.com/privkey.pem  ~/hoge.com/hoge.com.key
cp /etc/letsencrypt/live/hoge.com/fullchain.pem  ~/hoge.com/hoge.com.crt
```

# up nginx reverse proxy

```sh
cd multi-wp/proxy
docker-compose up -d
```
## optional: customizing
fix ``.env`` file.
```sh
CERT_PATH=~/hoge.com  #FIX
NETWORK_NAME=mynetwork
```

# up hoge.com and fuga.hoge.com

```sh
cd hoge.com
docker-compose up -d

cd fuga.hoge.com
docker-compose up -d
```
## optional: customizing 
fix ``.env`` file.
```sh
WP_CONTAINER_NAME=hoge-container-wp
DB_CONTAINER_NAME=hoge-container-db
WP_DBNAME=my-wp
DB_USER=admin
DB_PASSWORD=user_password
DB_ROOT_PASSWORD=root_password
DOMAIN=hoge.com
NETWORK_NAME=mynetwork
```
# enjoy!
open ``https://hoge.com`` and ``https://fuga.hoge.com``
