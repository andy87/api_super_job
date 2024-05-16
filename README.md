# api SuperJob

## IN PROGRESS

PHP Фасад для API Super Job (www.superjob.ru)

#### Реализация
 - API: реализация запросов к api сервису `Super Job`
 - Servcie: Фасад для класса API

### Использование Api
Методы Api возвращают массив с данными.
```php
use and_y87\api_super_job\ApiSuperJob;
use and_y87\api_super_job\dto\SuperJobApiRequisites;
use and_y87\api_super_job\cache\CacheProvider;

// Создание класса `CacheProvider`
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

// Создание экземпляра класса `CacheProvider`
$redisCacheProvider = new RedisCacheProvider();

// Создание экземпляра класса `Requisites`
$superJobApiRequisites = new SuperJobApiRequisites( $client_id, $client_secret );

// Создание экземпляра класса `Api`
$apiSuperJob = ApiSuperJob( $superJobApiRequisites, $redisCacheProvider );

// Использование `Api`
$me = $apiSuperJob->me(); // return array

echo $me['name']; // получение значения массива по ключу (hardcode)
```
### Использование Service
Методы Service возвращают объекты(экзмпляры классов) содержащие актуальные для endpoint свойства, согласно документации сервиса.
```php
use and_y87\api_super_job\service\AvitoService;

//Вводная часть при использовании сервиса аналогична Api

// Создание экземпляра класса `Service`
$superJobService = new SuperJobService($apiSuperJob);

// Использование `Service`
$me = $superJobService->myInfo(); // return and_y87\api_super_job\response\Me();

echo $me->name; // Получение значение из объекта через обращение к свойству
```

#### Схема работы API
![Схема работы API](https://static.andy87.ru/github/api/apiLogivSchema.png?v=3)

### Исходная документация API `SuperJob`: 
 - https://api.superjob.ru
