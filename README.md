# api SuperJob

PHP Фасад для API Super Job (www.superjob.ru)

#### Схема работы API
https://miro.com/app/board/uXjVKHFfUB0=/

#### Реализация
 - API: реализация запросов к api сервису `Head Hunter`
 - Servcie: Фасад для класса API

### Использование Api
```php
use and_y87/api_super_job/ApiSuperJob;
use and_y87/api_super_job/dto/SuperJobApiRequisites;
use and_y87/api_super_job/tools/CacheProvider;

// Add `CacheProvider`
class RedisCacheProvider extends CacheProvider
{
    public function getValue(string $key )
    {
        Yii::$app->redis->get( $key );
    }

    public function setValue( string $key, string $value )
    {
        Yii::$app->redis->set( $key, value );
    }
}

// Create object `CacheProvider`
$redisCacheProvider = new RedisCacheProvider();

// Create object `Requisites`
$superJobApiRequisites = new SuperJobApiRequisites( $client_id, $client_secret );

// Create object `Api`
$apiSuperJob = ApiSuperJob( $superJobApiRequisites, $redisCacheProvider );

// Use `Api`
```

### Исходная документация API `SuperJob`: 
 - https://api.superjob.ru
