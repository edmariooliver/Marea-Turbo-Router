<p align="center">
    <a href="https://packagist.org/packages/marrios/router"><img src="https://img.shields.io/packagist/dt/marrios/router" alt="Total Downloads"</a>
    <a href="https://packagist.org/packages/marrios/router"><img src="https://img.shields.io/packagist/v/marrios/router" alt="Latest Stable Version"></a>
    <a href="https://packagist.org/packages/marrios/router"><img src="https://img.shields.io/packagist/l/marrios/router" alt="License"></a>
</p>

@MárriosDev
# Marrios/Router


#### HTTP Route Manager for MVC Projects
<br>

## Guide

* ### [Starting](#starting)
* ### [Parameters](#parameters)
* ### [Middlewares](#middlewares)

# Starting

## 0 - Installing

```php
composer require marrios/router
```


## 1 - Using functions


 ```php
    
use Marrios\Router\HttpRouter;

$router = new HttpRouter();

// Set route
$router->get("/helloworld", [function(){ echo "Hello World!";}])->run();
$router->notFound();

 ```
When accessing the /helloworld route
 ```php
    Hello World!
 ```


 <!-- ======================================== -->

## 2 - Using Controllers


 ```php
use App\Controllers\TesteController;

use Marrios\Router\HttpRouter;

$router = new HttpRouter();

// Set route
$router->post("/helloworld", [TesteController::class, "helloWorld"])->run();
$router->notFound();

 ```
When accessing the /helloworld route
 ```php
    Hello World!
 ```


 <!-- ============================= -->



# Parameters
## Using dynamic parameters 
### Dynamic parameters are defined using curly braces { }
### * Note: When defining a dynamic route, you must add a parameter to the callback function or in the controller method

<br>

### Follow the example below using CallBack:

 ```php
use Marrios\Router\HttpRouter;

$router = new HttpRouter();

// Set route
$router->post("/blog/{category}/{id_post}", [ function($param){ echo $param->category;}])->run();
$router->notFound();

 ```
When accessing the /blog/video/1323 route
 ```php
    video
 ```

 <br>

### Follow the example below using Controller:

 ```php
use Marrios\Router\HttpRouter;

$router = new HttpRouter();

// Instantiating the route object
$router = new Router();

// Set route
$router->get("/blog/{category}/{id_post}", [TesteController::class, "helloWorld"])->run();
$router->notFound();

 ```

### Your controller should look like this
```php
class TesteController
{
    public function helloWorld($param)
    {
        echo $param->id_post;
    }
}
```

When accessing the /blog/video/1323 route
 ```php
    1323
 ```

# Middlewares

### Implement middlewares

<hr>

### Middleware 
```php
class Middleware
{
    public function handle() {
        return true;
    }
}
```
```php
use Marrios\Router\HttpRouter;
use Middleware;

$router = new HttpRouter();

// Set route
$router->middleware([Middleware::class])
       ->get("/ok", [function () {echo "OK";}])
       ->run();

```

When accessing the /ok route
 ```php
    OK
 ```
