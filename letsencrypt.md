## Let's Encrypt

> https://letsencrypt.org/

[An Automated Certificate Authority to Encrypt the Entire Web][1]
published for the ACM Conference on Computer and Communications Security
(CCS) in 2019 has more about ISRG and the history of Let's Encrypt.  

[1]:https://www.abetterinternet.org/documents/letsencryptCCS2019.pdf

### Create

```shell
letsencrypt certonly --agree-tos --standalone -d <domain> -d <www.domain>
```

### Renew

```shell
letsencrypt renew
```

### Update

```shell
letsencrypt certificates
```

```shell
letsencrypt certonly --agree-tos --standalone \ 
    --cert-name <certname from certificates> \
    -d <domain> \
    -d <www.domain> \
    -d <new.domain>
```

### Delete

```shell
letsencrypt delete
```

