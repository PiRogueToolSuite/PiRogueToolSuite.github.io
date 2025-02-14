---
title: "Make the dashboard accessible from the Internet"
---

Here, we assume :
 * a DNS record exists already, pointing to the public IP address of the
PiRogue.
 * port `80` and `443` from your public IP address fully translate to your server respectives ports

Requesting a certificate and adjusting the web server configuration can be done this way:

```shell
pirogue-admin-client external-network enable-public-access --domain pirogue.example.org --email contact@example.org
```

Once done, you can access to the dashboard on `https://pirogue.example.org/dashboard`. Make sure you replace `pirogue.example.org` with the domain name you have configured for your server and replace `contact@example.org` with your email address to be shared with Let's Encrypt.

