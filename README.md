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
Билет 18
Вопрос 1
Примеры рефакторинга кода для удаления дублирования
Рассмотрим простой пример на Java/C#, где есть дублирование кода для валидации пользователя:
До рефакторинга (Нарушение DRY):
java
```
public void processUserData(User user) {
    if (user.getName() == null || user.getName().isEmpty()) {
        System.out.println("Invalid name.");
        return;
    }
    if (user.getEmail() == null || !user.getEmail().contains("@")) {
        System.out.println("Invalid email.");
        return;
    }
    // Основная логика обработки...
}

public void validateAndSend(User user) {
    if (user.getName() == null || user.getName().isEmpty()) {
        System.out.println("Invalid name.");
        return;
    }
    if (user.getEmail() == null || !user.getEmail().contains("@")) {
        System.out.println("Invalid email.");
        return;
    }
    // Логика отправки...
}
```

После рефакторинга (Соблюдение DRY, извлечение метода):
Мы извлекаем общую логику валидации в отдельный метод isValidUser().
java
```
// Новый, переиспользуемый метод
private boolean isValidUser(User user) {
    if (user.getName() == null || user.getName().isEmpty()) {
        System.out.println("Invalid name.");
        return false;
    }
    if (user.getEmail() == null || !user.getEmail().contains("@")) {
        System.out.println("Invalid email.");
        return false;
    }
    return true;
}

public void processUserData(User user) {
    if (!isValidUser(user)) {
        return;
    }
    // Основная логика обработки...
}

public void validateAndSend(User user) {
    if (!isValidUser(user)) {
        return;
    }
    // Логика отправки...
}
```
Вопрос 2 
Примеры создания форм с различными типами валидации
Пример 1: Простая HTML5 форма с клиентской валидацией
html
```
<form action="/api/register" method="POST">
    <label for="username">Имя пользователя (от 4 до 10 симв.):</label>
    <input type="text" id="username" name="username" required minlength="4" maxlength="10">
    
    <label for="email">Email:</label>
    <!-- type="email" активирует базовую проверку формата на клиенте -->
    <input type="email" id="email" name="email" required>

    <label for="age">Возраст (18 до 99):</label>
    <!-- type="number" с атрибутами min/max -->
    <input type="number" id="age" name="age" min="18" max="99">

    <button type="submit">Зарегистрироваться</button>
</form>
```

Пример 2: Серверная валидация (Концепция на PHP)
Предположим, форма из Примера 1 отправляет данные на сервер.
php
```
// Файл /api/register (PHP)

// Никогда не доверяем данным от клиента, проверяем ВСЁ на сервере
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $username = $_POST['username'] ?? '';
    $email = $_POST['email'] ?? '';
    $age = filter_input(INPUT_POST, 'age', FILTER_VALIDATE_INT); // Безопасное получение числа

    $errors = [];

    // 1. Валидация username
    if (empty($username)) {
        $errors[] = "Имя пользователя обязательно.";
    } elseif (strlen($username) < 4 || strlen($username) > 10) {
        $errors[] = "Имя пользователя должно быть от 4 до 10 символов.";
    }

    // 2. Валидация email
    if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
        $errors[] = "Некорректный формат email.";
    }
    
    // 3. Валидация age
    if ($age === false || $age < 18 || $age > 99) {
        $errors[] = "Возраст должен быть от 18 до 99 лет.";
    }

    // Если ошибок нет, обрабатываем данные (сохраняем в БД)
    if (empty($errors)) {
        // !!! Здесь используем PDO и Prepared Statements для защиты от SQL Injection !!!
        // insert_user_into_db($username, $email, $age); 
        echo "Регистрация успешна!";
    } else {
        // Возвращаем ошибки пользователю
        foreach ($errors as $error) {
            echo "<p>Ошибка: $error</p>";
        }
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
