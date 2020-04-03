# Menggunakan Phalcon-multi-modules
## Struktur direktori PHALCON SKELETON

```

`apps
    config
          config.php
          loader.php
          modules.php
          routing.php
          services.php
    lib
         Phalcon
    modules
          dashboard
            Domain Driven Design
    .env
    bootstrap.php
public
    assets
    .htaccess
    index.php
.htaccess
composer.json`

```

## Persiapan

### composer install
jalankan ```composer install``` pada terminal
### Membuat folder cache
Buat folder cache pada direktori apps
``` mkdir apps/cache ```
lalu ubah permision cache,```chmod 777 apps/cache```

### Configurasi apache untuk routing 
<a href="https://medium.com/@sendyivenyulian/cara-mengatasi-error-the-requested-url-was-not-found-apache2-di-linux-981a1b5b2e07">Configurasi untuk pengaturan apache routing</a>

## Panduan 
<a href="https://docs.google.com/document/d/1d7ENZ73SQklmw-sPChPGrMIjGeM-3qLXCtvXpPfXTS8/edit">Untuk panduan bisa dilihat disini</a>
## Project
### Routing
Routing bisa dibedakan menjadi 2 yaitu secara **global** ataupun bisa secara **modul**
untuk routing secara global,untuk routing global bisa dilihat pada direktori
```apps/config/routing.php```
