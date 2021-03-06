---
layout: php
title: "PHP composer"
breadcrumb:
- composer
---

# 04. PSR-4
---
PSR4는 오토로딩에 대한 규약입니다.

<br>

## 04.1 namespace and Autoload
---
composer.json 파일의 추가 필드 중에 autoload가 있습니다. 여기서 PSR-4를 설정할 수 있습니다.

```json
"autoload": {
"psr-4": {

},
"files": [
],
"classmap": [
]        
},
"autoload-dev": {

}
```


프로젝트에 페키지와 별개로 `/app/controller` 과 같은 새로운 폴더를 하나 만들어 그안에 클래스 파일을 하나 만든다고 생각해 봅니다.


App\Controllers\UsersController.php
```
<?php

namespace App\Controllers;
class UsersController
{
    function __construct()
    {
        echo __CLASS__."가 생성이 되었습니다.<br>";
    }
}
```

App\Models\User.php
```
<?php

namespace App\Models;
class User
{
    function __construct()
    {
        echo __CLASS__."가 생성이 되었습니다.<br>";
    }
}
```

Psr4.php
```
<?php

require "app/controllers/UsersController.php";
require "app/models/User.php";

$users = new UsersController;
$user = new User;
```

네임스페이스를 추가합니다.
네임스페이스를 통하여 컴포저의 PSR-4 오토로드를 연결합니다.

```json
"autoload": {
        "psr-4": {
            "App\\": "app"
        }       
    }
```
를 추가합니다. 그리고 composer dumpautoload 를 실행해서 갱신해 줍니다.

```
d:\htdocs\composer>composer dumpautoload
Generating autoload files
```

이렇게 하면 /vendor/composer/autoload_psr4.php 파일이 갱신되게 됩니다.
```
<?php

// autoload_psr4.php @generated by Composer

$vendorDir = dirname(dirname(__FILE__));
$baseDir = dirname($vendorDir);

return array(
    'Symfony\\Polyfill\\Mbstring\\' => array($vendorDir . '/symfony/polyfill-mbstring'),
    'Symfony\\Component\\Translation\\' => array($vendorDir . '/symfony/translation'),
    'Psr\\SimpleCache\\' => array($vendorDir . '/psr/simple-cache/src'),
    'Psr\\Container\\' => array($vendorDir . '/psr/container/src'),
    'Illuminate\\Support\\' => array($vendorDir . '/illuminate/support'),
    'Illuminate\\Contracts\\' => array($vendorDir . '/illuminate/contracts'),
    'Illuminate\\Container\\' => array($vendorDir . '/illuminate/container'),
    'Doctrine\\Common\\Inflector\\' => array($vendorDir . '/doctrine/inflector/lib/Doctrine/Common/Inflector'),
    'App\\' => array($baseDir . '/app'),
    '' => array($vendorDir . '/nesbot/carbon/src'),
);
```

네임스페이스 App 부분 관련해서 추가된 모습을 보실 수 있습니다.

psr4.php
```
<?php

require "vendor/autoload.php";

$users = new \App\Controllers\UsersController;
$user = new App\Models\User;
```

결과
```
App\Controllers\UsersController가 생성이 되었습니다.
App\Models\User가 생성이 되었습니다.
```

