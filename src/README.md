# Menggunakan Phalcon-multi-modules
## Struktur direktori PHALCON SKELETON

```

`apps
    |config
      |-----config.php
      |-----loader.php
      |-----modules.php
      |-----routing.php
      |-----services.php
    |lib
      |-----Phalcon
    |modules
      |----dashboard
           |----- Domain Driven Design
    |.env
    |bootstrap.php
public
    |assets
    |.htaccess
    |index.php
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

dimana routing sudah diatur akan dideklarasikan secara otomatis jika terdapat modul,controller,index,dan paramater yang sesuai di direktori ```apps/modules``` tanpa meregistrasikan lagi pada file ```apps/config/routing.php```

aturan pada routing global adalah 

```host/:namamodules/:namacontroller/:namaaction/:namaparameter```

jadi jika kita mengakses website dengan alamat berikut

```example.phalcon/dashboard/index/index/1```

maka kita akan kita akan diarahkan pada halaman modul ```dashboard``` dengan controller ```index``` yang memiliki action ```index``` dan mendapatkan paramater ```1```



### Models
Untuk Membuat model maka kita perlu membuat folder baru pada module terkait

contoh :

```mkdir apps/modules/dashboard/Presentation/Web/Models```

lalu meregistrasikan autoloader untuk models pada ```apps/config/modules.dashboard/Module.php```

lalu tambahkan ini pada registerNamespacesnya

``` 'Its\Example\Dashboard\Presentation\Web\Models' => __DIR__ . '/Presentation/Web/Models',```

lalu buat models pada direktori **apps/modules/dashboard/Preswentation/Web/Models/**
disini saya membuat models dengan nama **Users.php**

```

<?php

namespace Its\Example\Dashboard\Presentation\Web\Models;

use Phalcon\Mvc\Model;

class Users extends Model
{

public $nama = "Zizki";

}


```

Untuke menggunakan model tersebut pada controller bisa dengan menggunakan 

**use Its\Example\Dashboard\Presentation\Web\Models\Users;**


### Controller
Controller dapat dibuat pada direktori

```apps/modules/namamodules/Presentation/Web/Controller```

misal kita membuat controller dengan nama **CobaController.php**
```
<?php

namespace Its\Example\Dashboard\Presentation\Web\Controller;

use Its\Example\Dashboard\Presentation\Web\Models\Users;
use Phalcon\Mvc\Controller;

class CobaController extends Controller
{
    public function indexAction()
    {
        echo 'coba module';
        $user = new Users();
        
        $this->view->setVars([
                "nama" =>$user->nama



        ]



        );
    }
}
```
setVars() milik IndexController berfungsi untuk
memberikan nilai kepada variabel di halaman view milik IndexAction().

kita membuat variable di view dengan nama ```nama``` yang diisi dengan isi variabel ```$user```

### View
buat folder baru  view

```mkdir apps/modules/dashboard/Presentation/Web/views```

untuk membuat view baru kita dapat membuat folder dengan **nama yang sama** dengan **controller**
misal disini kita membuat folder dengan nama coba di direktori apps/modules/dashboard/Presentation/Web/views

```mkdir coba ```
lalu kita membuat file .volt yang sama dengan nama action pada folder **coba**,misal kita membuat **index.volt** pada folder tersebut

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <h1>Selamat Datang {{ nama }}</h1>
</body>
</html>
</html>
```

lalu kita dapat mengunjungi **example.local/dashboard/coba**
