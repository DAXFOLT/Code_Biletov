# Code_Biletov
Билет 16
Вопрос 3
1. index.php (Точка входа):
```
// index.php
require 'Router.php';
require 'Controller.php';

$router = new Router();

// Определение маршрута: GET /welcome -> Controller::home
$router->addRoute('GET', '/welcome', 'Controller@home');

// Получаем текущий URL и метод
$requestUri = parse_url($_SERVER['REQUEST_URI'], PHP_URL_PATH);
$requestMethod = $_SERVER['REQUEST_METHOD'];

// Диспетчеризация запроса
$router->dispatch($requestMethod, $requestUri);
```
2. Router.php (Маршрутизатор):
```
// Router.php
class Router {
    private $routes = [];

    public function addRoute($method, $uri, $handler) {
        $this->routes[] = compact('method', 'uri', 'handler');
    }

    public function dispatch($method, $uri) {
        foreach ($this->routes as $route) {
            // Очень упрощенная проверка URL без регулярных выражений
            if ($route['method'] === $method && $route['uri'] === $uri) {
                list($controllerClass, $controllerMethod) = explode('@', $route['handler']);
                
                $controller = new $controllerClass();
                $controller->$controllerMethod(); // Вызов нужного метода
                return;
            }
        }
        header("HTTP/1.0 404 Not Found");
        echo "404 Not Found";
    }
}
```

3. Controller.php (Контроллер):
```
// Controller.php
class Controller {
    public function home() {
        echo "<h1>Welcome to my Micro-Framework!</h1>";
    }
}
```
Билет 21 
Вопрос 3
Пример структуры базы данныйх:
```
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50),
    password_hash VARCHAR(255),
    role VARCHAR(20) -- 'admin' или 'editor'
);

CREATE TABLE articles (
    id INT AUTO_INCREMENT PRIMARY KEY,
    title VARCHAR(255),
    content TEXT,
    author_id INT,
    status VARCHAR(20) -- 'draft' или 'published'
);
```
