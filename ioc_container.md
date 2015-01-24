# IoC Container

## Table of Content

* [Introduction](#introduction)
* [Basic Example](#basic-example)
* [References](#references)

## Introduction

The Laravel inversion of control container is a powerful tool for managing class dependencies. Dependency injection is a method of removing hard-coded class dependencies. Instead, the dependencies are injected at run-time, allowing for greater flexibility as dependency implementations may be swapped easily.

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


## References

* [IoC Container Documentation](http://laravel.com/docs/4.2/ioc)
* [Term: IoC Container](https://laracasts.com/lessons/term-ioc-container)
* [When to App::make()](https://laracasts.com/lessons/when-to-app-make)
* [DI Containers](https://laracasts.com/lessons/dependency-injection-containers)
* [The IoC Container](https://laracasts.com/lessons/the-ioc-container)
* [Method Injection](https://laracasts.com/series/whats-new-in-laravel-5/episodes/2)
* [Decoding Laravel's Magic](https://laracasts.com/lessons/decoding-laravels-magic)