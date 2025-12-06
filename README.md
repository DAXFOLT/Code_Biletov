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
Билет 17
Вопрос 2
Пример на С#
```
using System.IO;
using System.Text;

// ...

string text = "Привет, мир!";
string filePath = "example.txt";

// Запись текста в файл с использованием UTF-8
File.WriteAllText(filePath, text, Encoding.UTF8);

// Чтение текста из файла с явным указанием кодировки UTF-8
string readText = File.ReadAllText(filePath, Encoding.UTF8);

Console.WriteLine(readText); // Вывод: Привет, мир!

// Пример работы с другой кодировкой (Windows-1251)
Encoding windows1251 = Encoding.GetEncoding("windows-1251");
byte[] bytes1251 = windows1251.GetBytes(text);
// Здесь bytes1251 содержат байты в кодировке Windows-1251
```
Пример на Java
```
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Paths;
import java.util.List;

// ...

String text = "Привет, мир!";
String filePath = "example.txt";

// Запись текста в файл с использованием UTF-8
// Files.write требует List<String>
Files.write(Paths.get(filePath), List.of(text), StandardCharsets.UTF_8);

// Чтение текста из файла с использованием UTF-8
List<String> lines = Files.readAllLines(Paths.get(filePath), StandardCharsets.UTF_8);
String readText = String.join("\n", lines);

System.out.println(readText); // Вывод: Привет, мир!

// Пример преобразования строки в байты в другой кодировке (Windows-1251)
byte[] bytes1251 = text.getBytes("Windows-1251");
// Здесь bytes1251 содержат байты в кодировке Windows-1251
```
Вопрос 3

Примеры написания интеграционных тестов для приложения
Рассмотрим пример тестирования сервиса, который взаимодействует с базой данных. Мы используем фреймворк JUnit 5.
Задача: Протестировать, что сервис UserService может корректно сохранить нового пользователя в базу данных и затем найти его.
```
java
import org.junit.jupiter.api.*;
import static org.junit.jupiter.api.Assertions.*;

// Пример использует H2 Database в памяти для имитации реальной БД (это Fake)
public class UserServiceIntegrationTest {

    private UserRepository userRepository;
    private UserService userService;

    @BeforeEach
    public void setUp() {
        // Инициализация репозитория, который подключается к тестовой БД H2
        userRepository = new UserRepositoryInMemoryFake(); 
        userService = new UserService(userRepository);
    }

    @Test
    @DisplayName("Should save user and retrieve it correctly")
    public void testSaveAndFindUser() {
        // 1. Подготовка данных
        String email = "test@example.com";
        String name = "Test User";

        // 2. Действие - сохраняем пользователя
        userService.registerUser(email, name);

        // 3. Проверка - ищем пользователя в базе через тот же сервис/репозиторий
        User foundUser = userService.findUserByEmail(email);

        assertNotNull(foundUser, "User should be found in the database");
        assertEquals(email, foundUser.getEmail(), "Emails should match");
        assertEquals(name, foundUser.getName(), "Names should match");
    }
    
    // @AfterEach можно использовать для очистки данных, 
    // если Fake DB не очищается автоматически
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
