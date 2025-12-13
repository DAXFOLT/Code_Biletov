# Код билетов
## Содержание:
 [3 билет](#3-билет)
   - [1 вопрос](#3-билет-1-вопрос)
        - [Слой представления](#1-слой-представления-presentation-layer)
        - [Слой бизнес-логики](#2-слой-бизнес-логики-business-logic-layer)
        - [Слой данных](#3-слой-данных-data-access-layer)
   - [2 вопрос](#3-билет----2-вопрос)
      - [Основные команды Git]()
      - [Разработка простой фичи в команде с Git]()








## 3 билет
### 3 билет 1 вопрос
Слой представления (Presentation Layer)
Пример реализации (ASP.NET Core MVC):
#### 1. Слой представления (Presentation Layer)
Что делает: Взаимодействие с пользователем

```
// Пример: Форма заказа в мобильном приложении
public class CoffeeOrderForm
{
    public void ShowMenu()
    {
        Console.WriteLine("=== МЕНЮ ===");
        Console.WriteLine("1. Американо - 150 руб.");
        Console.WriteLine("2. Капучино - 200 руб.");
        Console.WriteLine("3. Латте - 220 руб.");
    }
    
    public OrderRequest GetOrder()
    {
        Console.Write("Выберите напиток (1-3): ");
        var drinkId = int.Parse(Console.ReadLine());
        
        Console.Write("Укажите количество: ");
        var quantity = int.Parse(Console.ReadLine());
        
        Console.Write("Ваше имя: ");
        var customerName = Console.ReadLine();
        
        return new OrderRequest
        {
            DrinkId = drinkId,
            Quantity = quantity,
            CustomerName = customerName
        };
    }
    
    public void ShowReceipt(Order order)
    {
        Console.WriteLine("\n=== ВАШ ЧЕК ===");
        Console.WriteLine($"Номер заказа: {order.Id}");
        Console.WriteLine($"Напиток: {order.DrinkName}");
        Console.WriteLine($"Количество: {order.Quantity}");
        Console.WriteLine($"Итого: {order.TotalPrice} руб.");
        Console.WriteLine($"Статус: {order.Status}");
    }
}
```
#### 2. Слой бизнес-логики (Business Logic Layer)
Что делает: Обработка заказа по правилам кофейни
```
// Простой сервис заказов
public class CoffeeOrderService
{
    public Order ProcessOrder(OrderRequest request)
    {
        // 1. Валидация
        if (request.Quantity <= 0)
            throw new Exception("Количество должно быть больше 0!");
        
        if (string.IsNullOrEmpty(request.CustomerName))
            throw new Exception("Укажите ваше имя!");
        
        // 2. Рассчитываем цену
        var price = GetPrice(request.DrinkId);
        var totalPrice = price * request.Quantity;
        
        // 3. Применяем скидку для постоянных клиентов
        if (IsRegularCustomer(request.CustomerName))
        {
            totalPrice *= 0.9m; // 10% скидка
        }
        
        // 4. Создаем заказ
        var order = new Order
        {
            Id = GenerateOrderId(),
            DrinkId = request.DrinkId,
            DrinkName = GetDrinkName(request.DrinkId),
            Quantity = request.Quantity,
            CustomerName = request.CustomerName,
            TotalPrice = totalPrice,
            Status = "Принят",
            CreatedDate = DateTime.Now
        };
        
        // 5. Проверяем ингредиенты на складе
        CheckIngredients(request.DrinkId, request.Quantity);
        
        return order;
    }
    
    private decimal GetPrice(int drinkId)
    {
        return drinkId switch
        {
            1 => 150m,  // Американо
            2 => 200m,  // Капучино
            3 => 220m,  // Латте
            _ => throw new Exception("Неизвестный напиток")
        };
    }
    
    private bool IsRegularCustomer(string name)
    {
        // Простая проверка - если имя в списке постоянных клиентов
        var regulars = new List<string> { "Анна", "Иван", "Мария" };
        return regulars.Contains(name);
    }
    
    private void CheckIngredients(int drinkId, int quantity)
    {
        // Проверяем, хватит ли кофе, молока и т.д.
        // Если нет - бросаем исключение
    }
}
```
#### 3. Слой данных (Data Access Layer)
Что делает: Сохранение и загрузка данных
```
// Простой репозиторий для работы с заказами
public class OrderRepository
{
    private List<Order> _orders = new List<Order>();
    private int _nextId = 1;
    
    // Сохранить заказ
    public void SaveOrder(Order order)
    {
        order.Id = _nextId++;
        _orders.Add(order);
        
        Console.WriteLine($"Заказ #{order.Id} сохранен в базе");
    }
    
    // Найти заказ по номеру
    public Order FindOrder(int orderId)
    {
        return _orders.FirstOrDefault(o => o.Id == orderId);
    }
    
    // Получить все заказы клиента
    public List<Order> GetCustomerOrders(string customerName)
    {
        return _orders
            .Where(o => o.CustomerName == customerName)
            .ToList();
    }
    
    // Обновить статус заказа
    public void UpdateOrderStatus(int orderId, string newStatus)
    {
        var order = FindOrder(orderId);
        if (order != null)
        {
            order.Status = newStatus;
            Console.WriteLine($"Статус заказа #{orderId} изменен на '{newStatus}'");
        }
    }
}

// Модель данных
public class Order
{
    public int Id { get; set; }
    public int DrinkId { get; set; }
    public string DrinkName { get; set; }
    public int Quantity { get; set; }
    public string CustomerName { get; set; }
    public decimal TotalPrice { get; set; }
    public string Status { get; set; }
    public DateTime CreatedDate { get; set; }
}
```

### 3 билет 2 вопрос
#### Основные команды Git
```markdown
### 2 вопрос

## Работа с изменениями

### Добавление файлов
```bash
git add filename.txt        # Конкретный файл
git add *.js                # Все JS файлы
git add .                   # Все изменения
```

#### Отмена изменений
```bash
git checkout -- filename.txt  # Отмена локальных изменений
git reset HEAD filename.txt   # Вывод из staging area
```

#### Просмотр различий
```bash
git diff                    # Неиндексированные изменения
git diff --staged           # Индексированные изменения
git diff main..feature      # Различия между ветками
```

### Работа с историей

#### Просмотр истории
```bash
git log --oneline --graph --all  # График всех веток
git log --since="2024-01-01"
git log --author="John"
```

#### Навигация по истории
```bash
git checkout a1b2c3d      # Переключение на конкретный коммит
git checkout HEAD~1       # Предыдущий коммит
```

#### Отмена коммитов
```bash
git revert a1b2c3d        # Создает новый коммит, отменяющий изменения
git reset --soft HEAD~1   # Удаляет последний коммит, сохраняя изменения
git reset --hard HEAD~1   # Полное удаление коммита и изменений (опасно!)
```

### Работа с удаленным репозиторием

#### Настройка удаленного репозитория
```bash
git remote add origin https://github.com/user/project.git
git remote -v              # Просмотр удаленных репозиториев
```

#### Отправка изменений
```bash
git push origin main              # Отправка ветки main
git push origin feature/login     # Отправка feature ветки
```

#### Получение изменений
```bash
git pull origin main       # Fetch + merge
git fetch origin           # Только загрузка изменений
git merge origin/main      # Слияние с удаленной веткой
```

#### Синхронизация
```bash
git fetch --prune          # Удаление устаревших ссылок на ветки
```

### Полезные команды

#### Временное сохранение изменений
```bash
git stash                  # Сохранить незакоммиченные изменения
git stash list             # Список stash'ей
git stash pop              # Применить последний stash и удалить его
```

#### Поиск в истории
```bash
git grep "TODO"            # Поиск текста в файлах
git log -S "functionName"  # Поиск по изменениям кода
```

#### Очистка
```bash
git clean -fd              # Удаление неотслеживаемых файлов и директорий
```

### Разработка простой фичи в команде с Git

**Задача**: _«Добавить кнопку "Нравится" к статье»_

#### Шаг 1: Получение задачи и создание ветки
```bash
# Переходим на основную ветку и обновляемся
git checkout main
git pull origin main

# Создаем ветку для задачи
git checkout -b feature/add-like-button
```

#### Шаг 2: Разработка
```bash
# 1. Добавляем кнопку в HTML
git add article.html
git commit -m "feat: add like button to article template"

# 2. Добавляем обработчик клика
git add script.js
git commit -m "feat: implement like button click handler"

# 3. Добавляем стили
git add styles.css
git commit -m "style: add like button styling"

# 4. Пишем простой тест
git add test-like-button.js
git commit -m "test: add basic like button test"
```

#### Шаг 3: Отправка на ревью
```bash
# Отправляем ветку на GitHub/GitLab
git push origin feature/add-like-button
```

**Создаем Pull Request (через веб-интерфейс)**

> **Описание в Pull Request:**
> ```
> Добавление кнопки "Нравится"
> 
> Изменения:
> - Добавлена кнопка "Нравится" под статьей
> - Реализован подсчет лайков
> - Добавлены стили для кнопки
> - Написан базовый тест
> 
> Как работает:
> 1. Пользователь кликает на кнопку ❤️
> 2. Счетчик увеличивается
> 3. Кнопка меняет цвет
> 4. Данные сохраняются локально
> 
> Closes #45
> ```

### Шаг 4: Получаем комментарии от коллег
В Pull Request коллеги пишут:
- _«Нужно добавить анимацию при клике»_
- _«Используй `const` вместо `let` в `script.js`»_

### Шаг 5: Вносим правки
```bash
# Исправляем замечания
git add script.js styles.css
git commit -m "fix: add animation and use const"

# Обновляем PR
git push origin feature/add-like-button
```

### Шаг 6: Слияние
После approval:
1. Нажимаем **«Merge pull request»** в GitHub  
2. Выбираем **«Squash and merge»** (объединяем все коммиты в один)  
3. Удаляем ветку

### Шаг 7: Локальная уборка
```bash
# Обновляем основную ветку
git checkout main
git pull origin main

# Удаляем локальную ветку
git branch -d feature/add-like-button
```
```

---

✅ Такой формат:
- Сохраняет ваши якоря (`## 3 билет` и `### 2 вопрос` — вы их добавите сами сверху/снизу),
- Использует правильную подсветку для `bash`,
- Разбивает информацию на логические блоки,
- Читается легко даже на мобильном,
- Поддерживает оформление Pull Request как цитату.

Если вы добавите это внутрь существующего `## 3 билет` → `### 2 вопрос`, всё будет работать идеально.

Нужно, чтобы я встроил это прямо в полный `README.md` с оглавлением? Готов помочь! 😊

## Билет 16
### Вопрос 3
#### 1. index.php (Точка входа):
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
#### 2. Router.php (Маршрутизатор):
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

#### 3. Controller.php (Контроллер):
```
// Controller.php
class Controller {
    public function home() {
        echo "<h1>Welcome to my Micro-Framework!</h1>";
    }
}
```
## Билет 17
### Вопрос 2
#### Пример на С#
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
### Вопрос 3

#### Примеры написания интеграционных тестов для приложения
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
## Билет 18
### Вопрос 1
#### Примеры рефакторинга кода для удаления дублирования
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
### Вопрос 2 
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

#### Пример 2: Серверная валидация (Концепция на PHP)
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
### Вопрос 3
Пример структурированного лога в JSON:
```
{
  "timestamp": "2025-12-08T10:00:00Z",
  "level": "ERROR",
  "service": "user-service",
  "transactionId": "abc-123",
  "message": "Failed to create user",
  "details": {
    "userId": 456,
    "errorType": "DatabaseException"
  }
}
```
## Билет 19
### Вопрос 3
Примеры настройки email отправки
#### Пример на Java (с использованием Jakarta Mail API)
Требуется добавить зависимость jakarta.mail-api и реализацию (например, angus-mail или jakarta.mail) в Maven/Gradle.
```
import javax.mail.*;
import javax.mail.internet.*;
import java.util.Properties;

public class EmailSender {

    public void sendMail(String recipientEmail, String subject, String body) throws MessagingException {
        final String username = "your_smtp_username";
        final String password = "your_smtp_password";
        final String host = "smtp.mailgun.org";

        Properties props = new Properties();
        props.put("mail.smtp.auth", "true");
        props.put("mail.smtp.starttls.enable", "true"); // Используем STARTTLS
        props.put("mail.smtp.host", host);
        props.put("mail.smtp.port", "587");

        Session session = Session.getInstance(props, new Authenticator() {
            protected PasswordAuthentication getPasswordAuthentication() {
                return new PasswordAuthentication(username, password);
            }
        });

        Message message = new MimeMessage(session);
        message.setFrom(new InternetAddress("sender@yourapp.com"));
        message.setRecipients(Message.RecipientType.TO, InternetAddress.parse(recipientEmail));
        message.setSubject(subject);
        message.setText(body);

        Transport.send(message);
        System.out.println("Email sent successfully!");
    }
}
```

#### Пример на C# (с использованием MailKit)
Требуется установить NuGet-пакет MailKit.
```
using MimeKit;
using MailKit.Net.Smtp;
using MailKit.Security;
using System.Threading.Tasks;

public class MailKitEmailSender
{
    public static async Task SendEmailAsync(string recipientEmail, string subject, string body)
    {
        var message = new MimeMessage();
        message.From.Add(new MailboxAddress("Your App Name", "noreply@yourapp.com"));
        message.To.Add(new MailboxAddress("", recipientEmail));
        message.Subject = subject;

        message.Body = new TextPart("plain") { Text = body };

        using (var client = new SmtpClient())
        {
            try
            {
                await client.ConnectAsync("smtp.sendgrid.net", 587, SecureSocketOptions.StartTls);
                await client.AuthenticateAsync("sendgrid_username", "sendgrid_password");
                await client.SendAsync(message);
                await client.DisconnectAsync(true);
                Console.WriteLine("Email sent successfully!");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error sending email: {ex.Message}");
                // Здесь должна быть логика логирования или повторных попыток
            }
        }
    }
}
```
## Билет 20
### Вопрос 3
#### Шаг 1: Определение ViewModel (MainViewModel.cs)
Этот класс будет содержать всю логику приложения: свойства для хранения введенных данных (сумма счета, процент чаевых) и вычисленный результат (общая сумма). Он также реализует интерфейс INotifyPropertyChanged для уведомления UI об изменениях.
```
// Для простоты примера, класс ViewModelBase и реализация INotifyPropertyChanged 
// опущены, но в реальном приложении они обязательны для работы привязок.
// Предполагаем, что у нас есть базовый класс ObservableObject

public class MainViewModel : ObservableObject 
{
    private decimal _billAmount;
    private int _tipPercentage = 15;
    private decimal _totalAmount;

    public decimal BillAmount
    {
        get => _billAmount;
        set
        {
            if (SetProperty(ref _billAmount, value))
            {
                CalculateTotal();
            }
        }
    }

    public int TipPercentage
    {
        get => _tipPercentage;
        set
        {
            if (SetProperty(ref _tipPercentage, value))
            {
                CalculateTotal();
            }
        }
    }

    public decimal TotalAmount
    {
        get => _totalAmount;
        // Только чтение из View, обновление происходит внутри ViewModel
        set => SetProperty(ref _totalAmount, value); 
    }

    private void CalculateTotal()
    {
        if (BillAmount > 0)
        {
            decimal tip = BillAmount * TipPercentage / 100;
            TotalAmount = BillAmount + tip;
        }
    }
}
```

#### Шаг 2: Разработка Представления (MainWindow.xaml)
Здесь мы создаем пользовательский интерфейс с использованием XAML и привязываем элементы UI к свойствам нашей ViewModel.
```
<!-- MainWindow.xaml -->
<Window x:Class="WpfTipCalculator.MainWindow"
        xmlns="schemas.microsoft.com"
        xmlns:x="schemas.microsoft.com"
        xmlns:local="clr-namespace:WpfTipCalculator"
        Title="Калькулятор чаевых" Height="250" Width="350">
    
    <!-- Устанавливаем DataContext окна на нашу ViewModel -->
    <Window.DataContext>
        <local:MainViewModel/>
    </Window.DataContext>

    <Grid Margin="10">
        <Grid.RowDefinitions>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
            <RowDefinition Height="Auto"/>
        </Grid.RowDefinitions>
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="*"/>
            <ColumnDefinition Width="*"/>
        </Grid.ColumnDefinitions>

        <!-- Сумма счета -->
        <Label Content="Сумма счета:" Grid.Row="0" Grid.Column="0"/>
        <TextBox Grid.Row="0" Grid.Column="1"
                 Text="{Binding BillAmount, Mode=TwoWay, UpdateSourceTrigger=PropertyChanged}"/>

        <!-- Процент чаевых -->
        <Label Content="Процент чаевых:" Grid.Row="1" Grid.Column="0"/>
        <TextBox Grid.Row="1" Grid.Column="1"
                 Text="{Binding TipPercentage, Mode=TwoWay, UpdateSourceTrigger=PropertyChanged}"/>
        
        <!-- Линия-разделитель -->
        <Separator Grid.Row="2" Grid.Column="0" Grid.ColumnSpan="2" Margin="0,10,0,10"/>

        <!-- Общая сумма -->
        <Label Content="ИТОГО:" Grid.Row="3" Grid.Column="0" FontWeight="Bold"/>
        <!-- Привязка TotalAmount (Mode по умолчанию OneWay - только отображение) -->
        <TextBlock Grid.Row="3" Grid.Column="1" FontWeight="Bold" FontSize="16"
                   Text="{Binding TotalAmount, StringFormat=C}"/> 
        
    </Grid>
</Window>
```

#### Шаг 3: Настройка запуска (Code-behind)
Файл MainWindow.xaml.cs остается чистым, так как вся логика находится в ViewModel.
```
// MainWindow.xaml.cs
using System.Windows;

namespace WpfTipCalculator
{
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
            // DataContext уже установлен в XAML, код здесь не требуется.
        }
    }
}
```
## Билет 21 
### Вопрос 3
Пример структуры базы данных:
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
