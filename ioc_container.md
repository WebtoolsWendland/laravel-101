# IoC Container

## Table of Content

* [Introduction](#introduction)
* [Basic Example](#basic-example)
* [References](#references)

## [Introduction](id:introduction)

The Laravel inversion of control container is a powerful tool for managing class dependencies. Dependency injection is a method of removing hard-coded class dependencies. Instead, the dependencies are injected at run-time, allowing for greater flexibility as dependency implementations may be swapped easily.

## [Basic Example](id:basic-example)

Hello world.

```php
<?php

interface FuelInterface
{
    public function getPrice();
}
```


## [References](id:references)

* [IoC Container Documentation](http://laravel.com/docs/4.2/ioc)
* [Term: IoC Container](https://laracasts.com/lessons/term-ioc-container)
* [When to App::make()](https://laracasts.com/lessons/when-to-app-make)
* [DI Containers](https://laracasts.com/lessons/dependency-injection-containers)
* [The IoC Container](https://laracasts.com/lessons/the-ioc-container)
* [Method Injection](https://laracasts.com/series/whats-new-in-laravel-5/episodes/2)
* [Decoding Laravel's Magic](https://laracasts.com/lessons/decoding-laravels-magic)