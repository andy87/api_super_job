# api SuperJob

## IN PROGRESS

PHP Фасад для API Super Job (www.superjob.ru)

#### Схема работы API
https://miro.com/app/board/uXjVKHFfUB0=/

#### Реализация
 - API: реализация запросов к api сервису `Super Job`
 - Servcie: Фасад для класса API

### Использование Api
Методы Api возвращают массив с данными.
```php
use and_y87\api_super_job\ApiSuperJob;
use and_y87\api_super_job\dto\SuperJobApiRequisites;
use and_y87\api_super_job\cache\CacheProvider;

// Add `CacheProvider`
class RedisCacheProvider extends CacheProvider
{
    public function getValue( string $key ): string
    {
        return (string) Yii::$app->redis->get( $key );
    }

    public function setValue( string $key, mixed $value ): bool
    {
        return Yii::$app->redis->set( $key, $value );
    }
}

// Create object `CacheProvider`
$redisCacheProvider = new RedisCacheProvider();

// Create object `Requisites`
$superJobApiRequisites = new SuperJobApiRequisites( $client_id, $client_secret );

// Create object `Api`
$apiSuperJob = ApiSuperJob( $superJobApiRequisites, $redisCacheProvider );

// Use `Api`
$me = $apiSuperJob->me(); // return array
```
### Использование Service
Методы Service возвращают Объекты с данными.
```php
use and_y87\api_super_job\service\AvitoService;

//Вводная часть при использовании сервиса аналогична Api

// Create object `Service`
$superJobService = new SuperJobService($apiSuperJob);

// Use `Service`
$me = $superJobService->me(); // return and_y87\api_super_job\response\Me();
```

#### Схема работы API
![Схема работы API](https://static.andy87.ru/github/api/apiLogivSchema.png)

### Исходная документация API `SuperJob`: 
 - https://api.superjob.ru
