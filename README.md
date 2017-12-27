# recepies_proxy
A simple docker-compose file to tie all the recipe services together

## Generate self signed SSL certificate
```
openssl req -x509 -newkey rsa:4096 -keyout recepies.local.key -out recepies.local.crt -days 365 -subj '/CN=recepies.local' -nodes
```
