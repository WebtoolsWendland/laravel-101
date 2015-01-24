# IoC Container

## Introduction

The Laravel inversion of control container is a powerful tool for managing class dependencies. Dependency injection is a method of removing hard-coded class dependencies. Instead, the dependencies are injected at run-time, allowing for greater flexibility as dependency implementations may be swapped easily[^1].

## Basic Example

### Project Directory

```
/src
    /CarInterface.php
    /FuelInterface.php
    /Axia.php
    /CivicTypeR.php
    /Ron95.php
    /Ron97.php
/composer.json
```

#### File: composer.json

```json
{
    "autoload": {
        "psr-4": { "": "src/"}
    },
    "require": {
        "illuminate/container": "~5.0"
    }
}
```

#### File: src/CarInterface.php

```php
<?php

interface CarInterface
{
    /**
     * Refuel the car.
     *
     * @param  int|double $litres
     * @return double
     */
    public function refuel($litres);
}
```

#### File: src/FuelInterface.php

```php
<?php

interface FuelInterface
{
    /**
     * Get fuel price.
     *
     * @return double
     */
    public function getPrice();
    
    /**
     * Set fuel price.
     *
     * @param  double  $price
     * @return double
     */
    public function setPrice($price);    
}
```

#### File: src/Axia.php

```php
<?php

class Axia implements CarInterface
{
    /**
     * The implementation of fuel.
     *
     * @var FuelInterface
     */
    protected $fuel;

    /**
     * Construct a new Car implementation.
     *
     * @param FuelInterface $fuel
     */
    public function __construct(Fuel $fuel)
    {
        $this->fuel = $fuel;
    }

    /**
     * Refuel the car.
     *
     * @param  int|double  $litres
     * @return double
     */
    public function refuel($litres)
    {
        return $litres * $this->fuel->getPrice();
    }
}
```

#### File: src/CivicTypeR.php

```php
<?php

class CivicTypeR implements CarInterface
{
    /**
     * The implementation of fuel.
     *
     * @var Ron97
     */
    protected $fuel;

    /**
     * Construct a new Car implementation.
     *
     * @param Ron97 $fuel
     */
    public function __construct(Ron97 $fuel)
    {
        $this->fuel = $fuel;
    }

    /**
     * Refuel the car.
     *
     * @param  int|double  $litres
     * @return double
     */
    public function refuel($litres)
    {
        return $litres * $this->fuel->getPrice();
    }

}
```

#### File: src/Ron95.php

```php
<?php

class Ron95 implements FuelInterface
{
    /**
     * Price value.
     *
     * @var double
     */
    protected $value = 1.91;

    /**
     * Get fuel price.
     *
     * @return double
     */
    public function getPrice()
    {
        return $this->value;
    }

    /**
     * Set fuel price.
     *
     * @param  double  $price
     * @return double
     */
    public function setPrice($price)
    {
        $this->value = $price;
    }

}
```

#### File: src/Ron97.php

```php
<?php

class Ron97 implements FuelInterface
{
    /**
     * Price value.
     *
     * @var double
     */
    protected $value = 2.11;

    /**
     * Get fuel price.
     *
     * @return double
     */
    public function getPrice()
    {
        return $this->value;
    }

    /**
     * Set fuel price.
     *
     * @param  double  $price
     * @return double
     */
    public function setPrice($price)
    {
        $this->value = $price;
    }

}
```

### Traditional Approach

```php
<?php

require_once "vendor/autoload.php";


$axia = new Axia(new Ron95());

echo $axia->refuel(100) . PHP_EOL;

$civic = new CivicTypeR(new Ron97());

echo $civic->refuel(100) . PHP_EOL;
```

Limitation:

* What happen when the fuel price change?
* How do we change the code if `Axia` need to use `Ron97` for any reason?
 
### IoC to the rescue

#### Simple Example

```php
<?php

require_once "vendor/autoload.php";

$app = new Illuminate\Container\Container();

$app->bind('FuelInterface', 'Ron95');

$axia = $app->make('Axia');

echo $axia->refuel(100) . PHP_EOL;

$ron97 = $app->make('Ron97');
$civic = $app->make('CivicTypeR', [$ron97]);

echo $civic->refuel(100) . PHP_EOL;
```

#### GST for Fuel

```php
<?php

require_once "vendor/autoload.php";

$app = new Illuminate\Container\Container();

$app->afterResolving('FuelInterface', function ($fuel) {
    $fuel->setPrice($fuel->getPrice() * 1.06);
});

$axia = $app->make('Axia');

echo $axia->refuel(100) . PHP_EOL;

$civic = $app->make('CivicTypeR');

echo $civic->refuel(100) . PHP_EOL;
```

#### Axia want to try Ron97

```php
<?php

require_once "vendor/autoload.php";

$app = new Illuminate\Container\Container();

$app->when('Axia')->needs('FuelInterface')->give('Ron97');

$axia = $app->make('Axia');

echo $axia->refuel(100) . PHP_EOL;

$civic = $app->make('CivicTypeR');

echo $civic->refuel(100) . PHP_EOL;
```

## References

* [IoC Container Documentation](http://laravel.com/docs/4.2/ioc)
* [Laracast on IoC](https://laracasts.com/search?q=ioc&q-where=lessons)
* [Digging in to Laravel's IoC Container](http://code.tutsplus.com/tutorials/digging-in-to-laravels-ioc-container--cms-22167)
 
[1]: http://laravel.com/docs/4.2/ioc#introduction [Introduction: IoC Container](http://laravel.com/docs/4.2/ioc#introduction) 

