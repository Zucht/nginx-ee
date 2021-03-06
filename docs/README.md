# Nginx-EE

## Compile and install the latest nginx releases from source with additional modules with EasyEngine, Plesk Onyx or from scratch

![nginx-ee](https://raw.githubusercontent.com/VirtuBox/nginx-ee/master/nginx-ee.png)

---

## Features

* Compile the latest Nginx Mainline or Stable Release
* Install Nginx or replace Nginx package previously installed
* Additonal modules
* Brotli Support
* TLS v1.3 support

---

## Additional modules

Nginx current mainline release : **v1.15.4**
Nginx current stable release : **v1.14.0**

* ngx_cache_purge
* memcached_nginx_module
* headers-more-nginx-module
* ngx_coolkit
* ngx_brotli
* redis2-nginx-module
* srcache-nginx-module
* ngx_http_substitutions_filter_module
* [nginx_dynamic_tls_records](https://github.com/nginx-modules/ngx_http_tls_dyn_size)
* Openssl 1.1.1
* [ipscrub](http://www.ipscrub.org/)
* ngx_http_auth_pam_module
* [virtual-host-traffic-status](https://github.com/vozlt/nginx-module-vts)

optional modules :

* ngx_pagespeed (latest-beta or latest-stable)
* naxsi WAF
* [nginx-rtmp-module](https://github.com/arut/nginx-rtmp-module)

---

## Compatibility

### Operating System

* Ubuntu 18.04 LTS (Bionic)
* Ubuntu 16.04 LTS (Xenial)
* Debian 8 (Jessie)

### Plesk releases

* 17.5.x
* 17.8.x
* 17.9.x

---

## Usage

### Interactive install

```bash
bash <(wget -qO - https://raw.githubusercontent.com/VirtuBox/nginx-ee/master/nginx-build.sh)
```

### Non interactive install

```bash
bash <(wget -qO - https://raw.githubusercontent.com/VirtuBox/nginx-ee/master/nginx-build.sh) [options] ...
```

#### Options available

Nginx release (required) :

* `--mainline` : compile nginx mainline release
* `--stable` : compile nginx stable release

Additional modules (optional)

* `--pagespeed`: compile nginx with ngx_pagespeed latest-stable
* `--pagespeed-beta`: compile nginx with ngx_pagespeed latest-beta
* `--naxsi` : compile nginx with naxsi
* `--rtmp` : compile nginx with rtmp module

### Example

```bash
bash <(wget -qO - https://raw.githubusercontent.com/VirtuBox/nginx-ee/master/nginx-build.sh) --mainline --pagespeed
```

This command will compile the latest nginx mainline release with ngx_pagespeed module

---

## Troubleshooting

TLS v1.3 do not work or browser show error message `ERR_SSL_VERSION_OR_CIPHER_MISMATCH` :

Update nginx ssl_ciphers in `/etc/nginx/nginx.conf` for EasyEngine servers or `/etc/nginx/conf.d/ssl.conf` for Plesk servers

### TLSv1.2 + TLSv1.3

```nginx
    ##
    # SSL Settings
    ##
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers 'TLS13+AESGCM+AES128:EECDH+AES128';
    ssl_prefer_server_ciphers on;
    ssl_session_cache shared:SSL:50m;
    ssl_session_timeout 1d;
    ssl_session_tickets off;
    ssl_ecdh_curve X25519:sect571r1:secp521r1:secp384r1
```

### TLSv1.0 + TLSv1.1 + TLSv1.2 + TLSv1.3

```nginx
    ##
    # SSL Settings
    ##
    # intermediate configuration. tweak to your needs.
    ssl_protocols TLSv1 TLSv1.1 TLSv1.2 TLSv1.3;
    ssl_ciphers 'TLS13+AESGCM+AES128:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-RSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-RSA-AES256-SHA256:DHE-RSA-AES256-SHA:ECDHE-ECDSA-DES-CBC3-SHA:ECDHE-RSA-DES-CBC3-SHA:EDH-RSA-DES-CBC3-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:DES-CBC3-SHA:!DSS';
    ssl_prefer_server_ciphers on;
    ssl_session_cache shared:SSL:50m;
    ssl_session_timeout 1d;
    ssl_session_tickets off;
    ssl_ecdh_curve X25519:sect571r1:secp521r1:secp384r1;
```

---

## Nginx configurations

* [Wiki](https://github.com/VirtuBox/nginx-ee/wiki)
* [Ubuntu-nginx-web-server](https://github.com/VirtuBox/ubuntu-nginx-web-server/tree/master/etc/nginx)

---

## Roadmap

* [x] Add choice between stable & mainline release
* [x] Add Nginx configuration examples
* [ ] Add Cloudflare HPACK patch
* [x] Add support for servers without EasyEngine
* [x] Add non-interactive installation
* [ ] Add automated update detection
* [x] Add support for Plesk servers

## Credits & Licence

* [ipscrub nginx module](http://ipscrub.org/)

Published & maintained by <a href="https://virtubox.net" title="VirtuBox">VirtuBox</a>