## Services

### Web services

#### Nginx

Nginx is an HTTP and reverse proxy server, a mail proxy server, and a generic TCP/UDP proxy server, originally written by [Igor Sysoev](http://sysoev.ru/en/).
It's used worldwide, and is one of best tools at what it does. Default configuration that comes with it, however, is not very security oriented, and it requires some work to set it up properly. That's what this section aims to help you with.

[Source](https://nginx.org/en/)

#### :eight_pointed_black_star: Files and directories permissions

Usually setting directories permissions to `0755` and file permissions to `0644` is a good practise.
`0755` permissions for directories allows nginx user to access files in the folder, however you don't want to grant same type of permissions to a file, as granting execution permissions to a file is not a good idea, especially on a publicly exposed server.

Script for setting all directories permissions to `0755` (here we assume that webserver directory path is `/var/www/html`):

```bash
find /var/www/html -type d -exec chmod 755 {} \;
```

Script for setting all files permissions to `0644`:

```bash
find /var/www/html -type f -exec chmod 644 {} \;
```

Whatever you do, never grant `0777` permissions to files, nor folders.

#### :eight_pointed_black_star: Use HTTPS

In this day and age, with services like [Let's Encrypt](https://letsencrypt.org/), there's no excuse not to use HTTPS for your website.

This example configuration also includes stronger cihper suite, ssl session adjustments, HSTS header, stronger DHE parameter, and OSCP Stapling.

**Example of a config with HTTP to HTTPS redirection:**

```
server {
        listen 80 default_server;
        listen [::]:80 default_server;
        server_name example.com;

        return 301 https://$host$request_uri;
        server_tokens off;
}

server {
        listen 443 ssl default_server;
        listen [::]:443 ssl;

        server_name example.com;
        server_tokens off;

        ssl     on;
        ssl_certificate /etc/nginx/ssl/ssl-bundle.crt;
        ssl_certificate_key /etc/nginx/ssl/cert.key;
        ssl_session_timeout 1d;
        ssl_session_cache shared:SSL:50m;
        ssl_session_tickets off;
        ssl_protocols TLSv1.2;
        ssl_ciphers 'ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA:ECDHE-RSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-RSA-AES256-SHA256:DHE-RSA-AES256-SHA:ECDHE-ECDSA-DES-CBC3-SHA:ECDHE-RSA-DES-CBC3-SHA:EDH-RSA-DES-CBC3-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:DES-CBC3-SHA:!DSS';
        ssl_prefer_server_ciphers on;
        ssl_stapling on;
        ssl_stapling_verify on;
        ssl_dhparam /etc/nginx/ssl/dhparam-4096.pem;
}
```

[Source](https://mozilla.github.io/server-side-tls/ssl-config-generator/)

#### :eight_pointed_black_star: Enable HTTP/2

HTTP/2 is a replacement for how HTTP is expressed “on the wire.” It is not a ground-up rewrite of the protocol; HTTP methods, status codes and semantics are the same, and it should be possible to use the same APIs as HTTP/1.x (possibly with some small additions) to represent the protocol.

[Source](https://http2.github.io/)

**Differences between HTTP/2 and HTTP/1.1:**

At a high level, HTTP/2:

<ul>
  <li>is binary, instead of textual</li>
  <li>is fully multiplexed, instead of ordered and blocking</li>
  <li>can therefore use one connection for parallelism</li>
  <li>uses header compression to reduce overhead</li>
  <li>allows servers to “push” responses proactively into client caches</li>
</ul>

[Source](https://http2.github.io/faq/#what-are-the-key-differences-to-http1x)

**Example config that enables HTTP/2:**

```
server {
        listen 80 default_server;
        listen [::]:80 default_server;
        server_name example.com;

        return 301 https://$host$request_uri;
        server_tokens off;
}

server {
        listen 443 ssl http2 default_server;
        listen [::]:443 ssl http2;

        server_name example.com;
        server_tokens off;

        ssl     on;
        ssl_certificate /etc/nginx/ssl/ssl-bundle.crt;
        ssl_certificate_key /etc/nginx/ssl/cert.key;
}
```

#### :eight_pointed_black_star: Separate domains

In case you have more than one website you'd like to serve from your server, nginx allows you to that.

In this example we'll have 2 different websites, with 2 different domains, served from same virtual machine.

**Example config that allows you to serve two websites with two different domains:**

```
server {
        listen 80;
        listen [::]:80;
        server_name first-example.com;

        root /var/www/html/website1;
        index index.html;
        server_tokens off;

        location / {
          try_files $uri $uri/ =404;
        }

}

server {
        listen 80;
        listen [::]:80;
        server_name second-example.com;

        root /var/www/html/website2;
        index index.html;
        server_tokens off;

        location / {
          try_files $uri $uri/ =404;
        }
}
```

#### :eight_pointed_black_star: Redirect all unencrypted traffic to HTTPS

This config entry is responsible for permanently redirecting all HTTP traffic to HTTPS. It will redirect all visitors that try to access website through HTTP on port 80, to HTTPS on port 443:

`return 301 https://$host$request_uri;`

**Example config:**

```
server {
        listen 80 default_server;
        listen [::]:80 default_server;
        server_name example.com;

        return 301 https://$host$request_uri;
        server_tokens off;
}

server {
        listen 443 ssl http2 default_server;
        listen [::]:443 ssl http2;

        server_name example.com;
        server_tokens off;

        ssl     on;
        ssl_certificate /etc/nginx/ssl/ssl-bundle.crt;
        ssl_certificate_key /etc/nginx/ssl/cert.key;
}
```

#### :eight_pointed_black_star: Enable HTTP Strict Transport Security

**What is HSTS?**

HTTPS (HTTP encrypted with SSL or TLS) is an essential part of the measures to secure traffic to a website, making it very difficult for an attacker to intercept, modify, or fake traffic between a user and the website.

When a user enters a web domain manually (providing the domain name without the http:// or https:// prefix) or follows a plain http:// link, the first request to the website is sent unencrypted, using plain HTTP. Most secured websites immediately send back a redirect to upgrade the user to an HTTPS connection, but a well‑placed attacker can mount a man‑in‑the‑middle (MITM) attack to intercept the initial HTTP request and can control the user’s session from then on.

[Source](https://www.nginx.com/blog/http-strict-transport-security-hsts-and-nginx/)

Config entry :

```bash
add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
```

**Example config**

```bash
server {
        listen 80 default_server;
        listen [::]:80 default_server;
        server_name example.com;

        return 301 https://$host$request_uri;
        server_tokens off;
}

server {
        listen 443 ssl http2 default_server;
        listen [::]:443 ssl http2;

        server_name example.com;
        server_tokens off;

        ssl     on;
        ssl_certificate /etc/nginx/ssl/ssl-bundle.crt;
        ssl_certificate_key /etc/nginx/ssl/cert.key;

        add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
}
```

#### :eight_pointed_black_star: Diffie Hellman Ephemeral Parameter

All versions of nginx as of 1.4.4 rely on OpenSSL for input parameters to Diffie-Hellman (DH). Unfortunately, this means that Ephemeral Diffie-Hellman (DHE) will use OpenSSL's defaults, which include a 1024-bit key for the key-exchange.
This example aims to generate stronger DHE parameter:

```bash
cd /etc/nginx/ssl/
openssl dhparam -out dhparam-4096.pem 4096
```

Then add it to your nginx config with this config entry:

```bash
ssl_dhparam /etc/nginx/ssl/dhparam-4096.pem;
```
[Source](https://raymii.org/s/tutorials/Strong_SSL_Security_On_nginx.html)

#### :eight_pointed_black_star: Security related headers

_Cross-site scripting (XSS) protection:_

Helps with preventing XSS attacks, it's enabling cross-site scripting filter built into modern browsers.

```bash
add_header x-xss-protection "1; mode=block" always;
```

_X-Frame-Options:_

Prevents iframe loading from different websites:

```bash
add_header x-frame-options "SAMEORIGIN" always;
```

_X-Content-Type-Options:_

It helps reducing drive-by downloads:

```bash
add_header X-Content-Type-Options "nosniff" always;
```

_HTTP Strict Transport Security (HSTS):_

When a browser sees this header from an HTTPS website, it “learns” that this domain must only be accessed using HTTPS (SSL or TLS). It caches this information for the max-age period (typically 31,536,000 seconds, equal to about 1 year).

```bash
add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
```

[Source 1](https://www.nginx.com/blog/http-strict-transport-security-hsts-and-nginx/)
[Source 2](https://www.owasp.org/index.php/OWASP_Secure_Headers_Project)
