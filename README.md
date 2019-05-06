# yii3-jwt

JWT implementation for Yii3

For details see [JWT official website](https://jwt.io/introduction/).

## Installation

To install run:
```
    composer require "xzag/yii3-jwt: ~3.0"
```
Or add this line to *require* section of composer.json:
```
    "xzag/yii3-jwt": "~3.0"
```

## Usage

There is only one trait - *UserTrait* - which gives you 5 methods for
authorization and JWT-management in User model

Set up:

In controller:

```PHP
<?php

// ...

use yii\web\filters\auth\HttpBearerAuth;
use Yiisoft\Yii\Rest\ActiveController;

class BearerAuthController extends ActiveController
{
    public function behaviors()
    {
        return array_merge(parent::behaviors(), [
            'bearerAuth' => [
                'class' => HttpBearerAuth::class
            ]
        ]);
    }
}
```

In User model:

```PHP
<?php

// ...

use yii\activerecord\ActiveRecord;
use yii\web\IdentityInterface;

class User extends ActiveRecord implements IdentityInterface
{
    // Use the trait in your User model
    use xzag\JWT\UserTrait;

    // Override this method
    protected static function getSecretKey()
    {
        return 'someSecretKey';
    }

    // And this one if you wish
    protected static function getHeaderToken()
    {
        return [];
    }

    // ...
}
```
