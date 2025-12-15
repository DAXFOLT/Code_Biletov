# Код билетов
## Содержание:
[1 билет](1-билет)
   - [2 вопрос](#2-вопрос)
        - [Пример Инкапусляция на C#](#пример-инкапусляция-на-c)
        - [Пример Наследование на С#](#пример-наследование-на-с)
        - [Пример Полиморфизм на C#](#пример-полиморфизм-на-c)
        - [Пример Абстракция на C#](#пример-абстракция-на-c)

[2 билет](#2-билет)
   - [1 вопрос](#2-билет-1-вопрос)
      - [Singlton (одиночка, _instance)](#singlton-одиночка-_instance)
      - [Factory Method (Фабричный, CreateProduct)](#factory-method-фабричный-createproduct)
      - [Abstract Factory](#abstract-factory)
   - [3 вопрос](#2-билет-3-вопрос)
        - [Иерархия исключений и пример](#иерархия-исключений)
        - [Блок try catch-finally](#блок-try-catch-finally)

[3 билет](#3-билет)
   - [1 вопрос](#3-билет-1-вопрос)
        - [Слой представления](#1-слой-представления-presentation-layer)
        - [Слой бизнес-логики](#2-слой-бизнес-логики-business-logic-layer)
        - [Слой данных](#3-слой-данных-data-access-layer)
   - [2 вопрос](#3-билет-2-вопрос)
      - [Основные команды Git](#основные-команды-git)
      - [Разработка простой фичи в команде с Git](#разработка-простой-фичи-в-команде-с-git)
      
[4 билет](#4-билет)
  - [1 вопрос](#4-билет-1-вопрос)
  - [3 вопрос](#4-билет-1-вопрос)

[8 билет](билет-8)
   - [2 вопрос](#билет-8-вопрос-2)
   - [3 вопрос](#вопрос-3)

[9 билет](#билет-9)
   - [1 вопрос](#билет-9-вопрос-1)
   - [2 вопрос](#вопрос-2-использование-в-коде-java)

[10 билет](#билет-10)
   - [2 вопрос](#билет-10-вопрос-2)
   - [3 вопрос](#вопрос-3-1)

[12 билет](#билет-12)
   - [1 вопрос](#билет-12-вопрос-1)
   - [2 вопрос](#билет-12-вопрос-2)

[13 билет](#билет-13)
   - [1 вопрос](#вопрос-1)
   - [2 вопрос](#вопрос-2)
   - [3 вопрос](#вопрос-3-3)

[14 билет](#билет-14)
   - [2 вопрос](#вопрос-2-1)
   - [3 вопрос](#вопрос-3-4)

[15 билет](#билет-15)
   - [2 вопрос](#вопрос-2-2)
   - [3 вопрос](#вопрос-3-5)

[16 билет](#билет-16)
  - [3 вопрос](#вопрос-3)
      - [indexphp точка входа](#1-indexphp-точка-входа)
      - [routerphp маршрутизатор](#2-routerphp-маршрутизатор)
      - [controllerphp контроллер](#3-controllerphp-контроллер)

[17 билет](#билет-17)
 - [2 вопрос](#вопрос-2)
 - [3 вопрос](#вопрос-3-1)

[18 билет](#билет-18)
 - [1 вопрос](#вопрос-1)
 - [2 вопрос](#вопрос-2-1)
 - [3 вопрос](#вопрос-3-2)

[19 билет](#билет-19)
 - [3 вопрос](#вопрос-3-3)
     - [Пример на C# с использованием mailkit](#пример-на-c-с-использованием-mailkit)

[20 билет](#билет-20)
 - [3 вопрос](#вопрос-3-4)
     - [Шаг 1: Определение ViewModel (MainViewModel.cs)](#шаг-1-определение-viewmodel-mainviewmodelcs)
     - [Шаг 2: Разработка Представления (MainWindow.xaml)](#шаг-2-разработка-представления-mainwindowxaml)
     - [Шаг 3: Настройка запуска (Code-behind)](#шаг-3-настройка-запуска-code-behind)

 [21 билет](#билет-21)
 - [3 вопрос](#вопрос-3-5)

## 1 билет
### 2 вопрос
#### Пример Инкапусляция на C#
```
using System;

// Пример: "Кофе-машина"
public class CoffeeMachine
{
    // Внутр. данные, скрыты от пользователя
    private int _WaterAmount = 1000;
    private int _CoffeeBeans = 500;
    private bool _isOn = false;

    // Публичный интерфейс - только то, что нужно пользователю

    public void TurnOn()
    {
        _isOn = true;
        Console.WriteLine("Кофе-машина включена");
    }

    public void MakeCoffee()
    {
        if (!_isOn)
        {
            Console.WriteLine("Сначала включите!");
            return;
        }
        if (_WaterAmount < 100)
        {
            Console.WriteLine("Недостаточно воды");
            return;
        }
        _WaterAmount -= 100;
        _CoffeeBeans -= 20;
        Console.WriteLine("Кофе готов!");
    }

    public void ShowStatus()
    {
        Console.WriteLine($"Вода: {_WaterAmount} мл.");
    }
}

// Использование
class Program
{
    static void Main()
    {
        CoffeeMachine machine = new CoffeeMachine();
        machine.TurnOn();
        machine.MakeCoffee();
        machine.ShowStatus();
    }
}
```
#### Пример Наследование на С#
```
// Базовый класс
public class Vehicle
{
    public string Brand { get; set; }
    public int MaxSpeed { get; set; }
    public void StartEngine()
    {
        Console.WriteLine($"Brand: {Brand}, MaxSpeed: {MaxSpeed}");
    }
}

// Наследник 1
public class Car : Vehicle
{
    public int DoorsCount { get; set; }
    public void Honk()
    {
        Console.WriteLine("Бип");
    }
}

// Использование
class Program
{
    static void Main()
    {
        Car myCar = new Car();
        myCar.Brand = "Toyota";
        myCar.MaxSpeed = 180;
        myCar.DoorsCount = 4;
        myCar.StartEngine(); // Выводит: Brand: Toyota, MaxSpeed: 180
        myCar.Honk(); // Выводит: Бип
    }
}
```

#### Пример Полиморфизм на C#
```
using System;

// Базовый класс для форм
public abstract class BoxingForm
{
    public string Name { get; set; }

    // Конструктор по умолчанию
    public BoxingForm()
    {
        Name = "no-boxing instance";
    }

    // Абстрактный метод, который должен быть реализован в производных классах
    public abstract void Battle();

    // Виртуальный метод, который можно переопределить
    public virtual void Gracese()
    {
        Console.WriteLine($"I'm {Name}!");
    }
}

// Производный класс RoundForm
public class RoundForm : BoxingForm
{
    public override void Battle()
    {
        Console.WriteLine($"{Name} is doing 3 days of training!");
    }
}

// Производный класс SquareForm
public class SquareForm : BoxingForm
{
    public override void Battle()
    {
        Console.WriteLine($"{Name} is doing hyper training!");
    }
}

// Класс программы
class Program
{
    static void Main()
    {
        // Создаем массив объектов базового типа
        BoxingForm[] forms =
        {
            new RoundForm { Name = "Борьба" },
            new SquareForm { Name = "Квадратная фигура" }
        };

        // Перебираем все формы и вызываем их методы
        foreach (var form in forms)
        {
            form.Gracese();   // Вызываем виртуальный метод
            form.Battle();    // Вызываем абстрактный метод
            Console.WriteLine(); // Пустая строка для разделения вывода
        }
    }
}
```

#### Пример Абстракция на C#
```
using System;

// Абстрактный базовый класс для пульта управления
public abstract class RemoteControl
{
    // Свойство для хранения бренда
    public string Brand { get; set; }

    // Конструктор по умолчанию
    public RemoteControl()
    {
        Brand = "no-brand";
    }

    // Абстрактные методы, которые должны быть реализованы в производных классах
    public abstract void TurnOn();
    public abstract void TurnOff();
    public abstract void VolumeUp();

    // Виртуальный метод, который можно переопределить
    public virtual void ShowBrand()
    {
        Console.WriteLine($"Текущий бренд: {Brand}");
    }
}

// Производный класс для телевизионного пульта
public class TVRemote : RemoteControl
{
    public override void TurnOn()
    {
        Console.WriteLine("Телевизор включен");
    }

    public override void TurnOff()
    {
        Console.WriteLine("Телевизор выключен");
    }

    public override void VolumeUp()
    {
        Console.WriteLine("Громкость увеличена");
    }

    // Переопределяем виртуальный метод
    public override void ShowBrand()
    {
        Console.WriteLine($"Текущий бренд телевизора: {Brand}");
    }
}

// Класс программы
class Program
{
    static void Main()
    {
        // Использование
        RemoteControl tvRemote = new TVRemote { Brand = "Samsung" };

        // Использование объектов
        tvRemote.ShowBrand(); // Вызов виртуального метода
        tvRemote.TurnOn();    // Вызов абстрактного метода
        tvRemote.VolumeUp();  // Вызов абстрактного метода
        Console.WriteLine();  // Пустая строка для разделения вывода
    }
}
```
[Содержание](#содержание)
## 2 билет
### 2 билет 1 вопрос
#### Singlton (одиночка, _instance)
```
using System;

// Публичный статический класс Database
public static class Database
{
    // Приватное статическое поле для хранения единственного экземпляра
    private static Database _instance;

    // Приватный конструктор, чтобы предотвратить создание экземпляров извне
    private Database()
    {
        // Инициализация базы данных может происходить здесь.
        Console.WriteLine("База данных инициализирована.");
    }

    // Публичное статическое свойство для получения экземпляра
    public static Database Instance
    {
        get
        {
            // Если экземпляр еще не создан, создаем его
            if (_instance == null)
            {
                _instance = new Database();
            }
            // Возвращаем существующий или только что созданный экземпляр
            return _instance;
        }
    }

    // Пример метода, который можно вызвать через экземпляр
    public void DoSomething()
    {
        Console.WriteLine("Выполняется какое-то действие с базой данных.");
    }
}

// Пример использования
class Program
{
    static void Main()
    {
        // Получаем единственный экземпляр базы данных
        var db = Database.Instance;
        // Вызываем метод
        db.DoSomething();

        // Попробуем получить еще один экземпляр
        var db2 = Database.Instance;
        // Сравним ссылки: они должны быть одинаковыми
        Console.WriteLine($"db и db2 — это один и тот же объект? {ReferenceEquals(db, db2)}");
    }
}
```

#### Factory Method (Фабричный, CreateProduct)
```
using System;

// Абстрактный продукт
abstract class Document
{
    // Здесь могут быть общие свойства и методы для всех документов
    public abstract void Open();
    public abstract void Save();
}

// Конкретный продукт 1
class WordDoc : Document
{
    public override void Open()
    {
        Console.WriteLine("Открывается документ Word.");
    }

    public override void Save()
    {
        Console.WriteLine("Документ Word сохранен.");
    }
}

// Конкретный продукт 2
class PdfDoc : Document
{
    public override void Open()
    {
        Console.WriteLine("Открывается документ PDF.");
    }

    public override void Save()
    {
        Console.WriteLine("Документ PDF сохранен.");
    }
}

// Абстрактный создатель (Creator)
abstract class Creator
{
    // Фабричный метод: возвращает абстрактный продукт
    public abstract Document CreateDocument();
}

// Конкретный создатель 1
class WordCreator : Creator
{
    public override Document CreateDocument()
    {
        return new WordDoc(); // Создает конкретный продукт WordDoc
    }
}

// Конкретный создатель 2
class PdfCreator : Creator
{
    public override Document CreateDocument()
    {
        return new PdfDoc(); // Создает конкретный продукт PdfDoc
    }
}

// Пример использования
class Program
{
    static void Main()
    {
        // Создаем фабрику для Word-документов
        Creator wordCreator = new WordCreator();
        Document wordDoc = wordCreator.CreateDocument();
        wordDoc.Open();
        wordDoc.Save();

        Console.WriteLine();

        // Создаем фабрику для PDF-документов
        Creator pdfCreator = new PdfCreator();
        Document pdfDoc = pdfCreator.CreateDocument();
        pdfDoc.Open();
        pdfDoc.Save();
    }
}
```
#### Abstract Factory
```
using System;

// Абстрактные продукты (интерфейсы)
interface IButton
{
    void Render();
}

interface ITextBox
{
    void Render();
}

// Конкретные продукты для Windows
class WinButton : IButton
{
    public void Render()
    {
        Console.WriteLine("Рендеринг кнопки Windows.");
    }
}

class WinTextBox : ITextBox
{
    public void Render()
    {
        Console.WriteLine("Рендеринг текстового поля Windows.");
    }
}

// Конкретные продукты для Mac
class MacButton : IButton
{
    public void Render()
    {
        Console.WriteLine("Рендеринг кнопки Mac.");
    }
}

class MacTextBox : ITextBox
{
    public void Render()
    {
        Console.WriteLine("Рендеринг текстового поля Mac.");
    }
}

// Абстрактная фабрика
interface IUIFactory
{
    IButton CreateButton();
    ITextBox CreateTextBox();
}

// Конкретная фабрика для Windows
class WinFactory : IUIFactory
{
    public IButton CreateButton()
    {
        return new WinButton();
    }

    public ITextBox CreateTextBox()
    {
        return new WinTextBox();
    }
}

// Конкретная фабрика для Mac
class MacFactory : IUIFactory
{
    public IButton CreateButton()
    {
        return new MacButton();
    }

    public ITextBox CreateTextBox()
    {
        return new MacTextBox();
    }
}

// Пример использования
class Program
{
    static void Main()
    {
        // Создаем фабрику для Windows
        IUIFactory winFactory = new WinFactory();

        // Используем фабрику для создания семейства продуктов
        IButton winButton = winFactory.CreateButton();
        ITextBox winTextBox = winFactory.CreateTextBox();

        winButton.Render();  // Вывод: Рендеринг кнопки Windows.
        winTextBox.Render(); // Вывод: Рендеринг текстового поля Windows.

        Console.WriteLine();

        // Создаем фабрику для Mac
        IUIFactory macFactory = new MacFactory();

        // Используем фабрику для создания другого семейства продуктов
        IButton macButton = macFactory.CreateButton();
        ITextBox macTextBox = macFactory.CreateTextBox();

        macButton.Render();  // Вывод: Рендеринг кнопки Mac.
        macTextBox.Render(); // Вывод: Рендеринг текстового поля Mac.
    }
}
```
### 2 билет 3 вопрос
#### Иерархия исключений
```
using System;

// Иерархия исключений в .NET (упрощенная версия)
//
// System.Object
//     |
//     +-- System.Exception (Базовый класс для всех исключений)
//             |
//             +-- System.SystemException (Исключения, генерируемые системой)
//             |       |
//             |       +-- System.DivideByZeroException (Попытка деления на ноль)
//             |       +-- System.NullReferenceException (Попытка доступа к члену объекта, равного null)
//             |       +-- System.ArgumentOutOfRangeException (Аргумент выходит за допустимый диапазон)
//             |       +-- System.IndexOutOfRangeException (Индекс выходит за границы массива или коллекции)
//             |       +-- System.InvalidOperationException (Недопустимая операция в текущем состоянии)
//             |       +-- System.Reflection.TargetInvocationException (Ошибка при вызове метода через рефлексию)
//             |       +-- System.FormatException (Строка не имеет правильного формата)
//             |
//             +-- System.ApplicationException (Исключения, генерируемые приложением)
//                     |
//                     +-- (Ваши собственные пользовательские исключения)

// Пример использования: создание и выброс пользовательского исключения
public class MyCustomException : ApplicationException
{
    public MyCustomException(string message) : base(message) { }
}

class Program
{
    static void Main()
    {
        try
        {
            // Пример, который может вызвать DivideByZeroException
            int a = 10;
            int b = 0;
            int result = a / b; // Это вызовет исключение

            // Пример, который может вызвать NullReferenceException
            string str = null;
            int length = str.Length; // Это вызовет исключение
        }
        catch (DivideByZeroException ex)
        {
            Console.WriteLine($"Обработка деления на ноль: {ex.Message}");
        }
        catch (NullReferenceException ex)
        {
            Console.WriteLine($"Обработка обращения к null: {ex.Message}");
        }
        catch (Exception ex) // Общий обработчик для всех остальных исключений
        {
            Console.WriteLine($"Неизвестное исключение: {ex.Message}");
        }
        finally
        {
            Console.WriteLine("Блок finally выполняется всегда.");
        }
    }
}
```
#### Блок try catch-finally
```
using System;

// Пользовательское исключение для отрицательного возраста
public class NegativeAgeException : Exception
{
    // Конструктор, принимающий сообщение об ошибке
    public NegativeAgeException(string message) : base(message) { }
}

class Program
{
    static void Main()
    {
        try
        {
            Console.WriteLine("Введите первое число (a): ");
            int a = int.Parse(Console.ReadLine());

            Console.WriteLine("Введите второе число (b): ");
            int b = int.Parse(Console.ReadLine());

            // Попытка деления. Может вызвать DivideByZeroException.
            int result = a / b;
            Console.WriteLine($"Результат деления: {result}");
        }
        catch (DivideByZeroException ex)
        {
            // Обработка конкретного исключения деления на ноль
            Console.WriteLine("Ошибка: Нельзя делить на ноль!");
            Console.WriteLine($"Детали: {ex.Message}");
        }
        catch (FormatException ex)
        {
            // Обработка исключения формата (если введено не число)
            Console.WriteLine("Ошибка: Введено некорректное значение. Пожалуйста, введите целое число.");
            Console.WriteLine($"Детали: {ex.Message}");
        }
        catch (Exception ex)
        {
            // Общий обработчик для всех остальных исключений
            Console.WriteLine($"Неизвестная ошибка: {ex.Message}");
        }
        finally
        {
            // Блок finally выполняется всегда, независимо от того, было ли исключение или нет.
            // Используется для освобождения ресурсов (например, закрытия файлов, соединений).
            Console.WriteLine("Блок finally выполнен.");
        }

        // Пример использования пользовательского исключения
        try
        {
            Person person = new Person();
            Console.Write("Введите возраст: ");
            int age = int.Parse(Console.ReadLine());
            person.SetAge(age); // Этот метод может выбросить NegativeAgeException
        }
        catch (NegativeAgeException ex)
        {
            Console.WriteLine($"Пользовательское исключение: {ex.Message}");
        }
        catch (FormatException)
        {
            Console.WriteLine("Ошибка: Введите корректное число для возраста.");
        }
    }
}

// Класс Person, который использует пользовательское исключение
class Person
{
    private int _age;

    public int Age
    {
        get { return _age; }
        set
        {
            if (value < 0)
            {
                // Выбрасываем пользовательское исключение, если возраст отрицательный
                throw new NegativeAgeException("Возраст не может быть отрицательным!");
            }
            _age = value;
        }
    }

    // Метод-сеттер, который также может выбрасывать исключение
    public void SetAge(int age)
    {
        if (age < 0)
        {
            throw new NegativeAgeException("Возраст не может быть отрицательным!");
        }
        this._age = age;
    }
}
```
[Содержание](#содержание)
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

#### Работа с историей

##### Просмотр истории
```bash
git log --oneline --graph --all  # График всех веток
git log --since="2024-01-01"
git log --author="John"
```

##### Навигация по истории
```bash
git checkout a1b2c3d      # Переключение на конкретный коммит
git checkout HEAD~1       # Предыдущий коммит
```

##### Отмена коммитов
```bash
git revert a1b2c3d        # Создает новый коммит, отменяющий изменения
git reset --soft HEAD~1   # Удаляет последний коммит, сохраняя изменения
git reset --hard HEAD~1   # Полное удаление коммита и изменений (опасно!)
```

#### Работа с удаленным репозиторием

##### Настройка удаленного репозитория
```bash
git remote add origin https://github.com/user/project.git
git remote -v              # Просмотр удаленных репозиториев
```

##### Отправка изменений
```bash
git push origin main              # Отправка ветки main
git push origin feature/login     # Отправка feature ветки
```

##### Получение изменений
```bash
git pull origin main       # Fetch + merge
git fetch origin           # Только загрузка изменений
git merge origin/main      # Слияние с удаленной веткой
```

##### Синхронизация
```bash
git fetch --prune          # Удаление устаревших ссылок на ветки
```

#### Полезные команды

##### Временное сохранение изменений
```bash
git stash                  # Сохранить незакоммиченные изменения
git stash list             # Список stash'ей
git stash pop              # Применить последний stash и удалить его
```

##### Поиск в истории
```bash
git grep "TODO"            # Поиск текста в файлах
git log -S "functionName"  # Поиск по изменениям кода
```

##### Очистка
```bash
git clean -fd              # Удаление неотслеживаемых файлов и директорий
```

#### Разработка простой фичи в команде с Git

**Задача**: _«Добавить кнопку "Нравится" к статье»_

##### Шаг 1: Получение задачи и создание ветки
```bash
# Переходим на основную ветку и обновляемся
git checkout main
git pull origin main

# Создаем ветку для задачи
git checkout -b feature/add-like-button
```

##### Шаг 2: Разработка
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

##### Шаг 3: Отправка на ревью
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

##### Шаг 4: Получаем комментарии от коллег
В Pull Request коллеги пишут:
- _«Нужно добавить анимацию при клике»_
- _«Используй `const` вместо `let` в `script.js`»_

##### Шаг 5: Вносим правки
```bash
# Исправляем замечания
git add script.js styles.css
git commit -m "fix: add animation and use const"

# Обновляем PR
git push origin feature/add-like-button
```

##### Шаг 6: Слияние
После approval:
1. Нажимаем **«Merge pull request»** в GitHub  
2. Выбираем **«Squash and merge»** (объединяем все коммиты в один)  
3. Удаляем ветку

##### Шаг 7: Локальная уборка
```bash
# Обновляем основную ветку
git checkout main
git pull origin main

# Удаляем локальную ветку
git branch -d feature/add-like-button
```
[Содержание](#содержание)
## 4 билет
### 4 билет 1 вопрос
```markdown
## Примеры временной сложности

- **O(1) — константное время**  
  Операция выполняется за фиксированное количество шагов, независимо от размера данных.
  ```python
  def get_first(arr):
      return arr[0]  # всегда один шаг
  ```

- **O(n) — линейное время**  
  Время растёт прямо пропорционально размеру входных данных.
  ```python
  def find_max(arr):
      max_val = arr[0]
      for x in arr:  # n шагов
          if x > max_val:
              max_val = x
      return max_val
  ```

- **O(n²) — квадратичное время**  
  Часто возникает при вложенных циклах.
  ```python
  def has_duplicate(arr):
      for i in range(len(arr)):
          for j in range(len(arr)):  # n × n = n²
              if i != j and arr[i] == arr[j]:
                  return True
      return False
  ```

- **O(log n) — логарифмическое время (бинарный поиск)**  
  На каждом шаге отбрасывается половина данных.
  ```python
  def binary_search(arr, target):
      left, right = 0, len(arr) - 1
      while left <= right:
          mid = (left + right) // 2
          if arr[mid] == target:
              return mid
          elif arr[mid] < target:
              left = mid + 1
          else:
              right = mid - 1
      return -1
  ```

- **O(n log n) — сортировка слиянием**  
  Рекурсивное деление (`log n` уровней) + линейное слияние (`O(n)`) на каждом уровне.
  ```python
  def merge_sort(arr):
      if len(arr) <= 1:
          return arr
      mid = len(arr) // 2
      left = merge_sort(arr[:mid])   # рекурсия: log n уровней
      right = merge_sort(arr[mid:])
      return merge(left, right)      # слияние: O(n) на каждом уровне → итого O(n log n)
  ```

#### Пространственная сложность

Помимо времени выполнения, важно учитывать потребление памяти:

- **O(1)** — алгоритм использует фиксированное количество дополнительной памяти (например, только несколько переменных).
- **O(n)** — объём используемой памяти растёт линейно с размером входных данных (например, создание нового массива или неоптимизированная рекурсия).
- **Рекурсивные алгоритмы** часто потребляют **O(n)** памяти из-за стека вызовов (глубина рекурсии = n).

### 4 билет 3 вопрос
```markdown
## Пример 1: Race Condition

```csharp
using System;
using System.Threading;

class Program
{
    private static int counter = 0;
    private static readonly object lockObj = new object();

    static void Main()
    {
        Thread t1 = new Thread(IncrementCounter);
        Thread t2 = new Thread(IncrementCounter);

        t1.Start();
        t2.Start();

        t1.Join();
        t2.Join();

        Console.WriteLine($"Ожидаем: 200000, Получили: {counter}");
    }

    static void IncrementCounter()
    {
        for (int i = 0; i < 100000; i++)
        {
            // Без синхронизации — race condition!
            counter++; // НЕАТОМАРНАЯ операция: прочитать → увеличить → записать
        }
    }
}
```

**Результат**: часто выводит значение **меньше 200000** (например, `165320`), потому что операции чтения/записи пересекаются между потоками.

✅ **Решение — использовать `lock`**:

```csharp
static void IncrementCounter()
{
    for (int i = 0; i < 100000; i++)
    {
        lock (lockObj)
        {
            counter++;
        }
    }
}
```

Теперь операция атомарна относительно блокировки → результат всегда будет `200000`.

---

#### Пример 2: Deadlock

**Взаимоблокировка (deadlock)** возникает, когда два или более потока удерживают ресурсы и ждут высвобождения других.

```csharp
using System;
using System.Threading;

class DeadlockExample
{
    private static readonly object lockA = new object();
    private static readonly object lockB = new object();

    static void Main()
    {
        Thread t1 = new Thread(() => MethodA());
        Thread t2 = new Thread(() => MethodB());

        t1.Start();
        t2.Start();

        t1.Join();
        t2.Join();
    }

    static void MethodA()
    {
        lock (lockA)
        {
            Console.WriteLine("MethodA: захватил lockA");
            Thread.Sleep(100); // даём время MethodB захватить lockB
            lock (lockB)
            {
                Console.WriteLine("MethodA: захватил lockB");
            }
        }
    }

    static void MethodB()
    {
        lock (lockB)
        {
            Console.WriteLine("MethodB: захватил lockB");
            Thread.Sleep(100);
            lock (lockA)
            {
                Console.WriteLine("MethodB: захватил lockA");
            }
        }
    }
}
```

#### Что происходит:

- `t1` захватывает `lockA`, затем засыпает.
- `t2` захватывает `lockB`, затем засыпает.
- `t1` пытается захватить `lockB` → **ожидает**.
- `t2` пытается захватить `lockA` → **ожидает**.
- ⚠️ **Deadlock!** Программа зависает навсегда.

✅ **Способы избежать deadlock**:

- **Всегда захватывать блокировки в одном и том же порядке** (например, сначала `lockA`, потом `lockB` — во всех методах).
- Использовать `Monitor.TryEnter(lock, timeout)` с тайм-аутом, чтобы избежать бесконечного ожидания.
- Минимизировать использование вложенных блокировок.
- Рассмотреть альтернативы: `SemaphoreSlim`, `lock-free` структуры, `async/await` вместо блокирующих вызовов.
[Содержание](#содержание)
## Билет 8
### Билет 8 вопрос 2
Примеры форматов:
Текст — просто строка.

CSV — таблица: имя,возраст\nАлиса,25.

JSON — структурированные данные: {"name": "Алиса", "age": 25}.

XML — разметка: <user><name>Алиса</name></user>.

Пример на Java (чтение JSON):
```
// Используем библиотеку Jackson
ObjectMapper mapper = new ObjectMapper();
User user = mapper.readValue(new File("user.json"), User.class);
```

### Вопрос 3
Интеграция внешнего API:

Изучить документацию (эндпоинты, формат запросов).
Получить API-ключ (если требуется).
Отправить HTTPS-запрос (например, с помощью HttpClient в C# или fetch в JS).
Обработать ответ (обычно в JSON).
Пример: интеграция Twilio для SMS (на Java):
Twilio.init(ACCOUNT_SID, AUTH_TOKEN);
```
Message message = Message.creator(
    new PhoneNumber("+1234567890"),
    new PhoneNumber("+1987654321"),
    "Привет из вашего приложения!"
).create();
```
[Содержание](#содержание)
## Билет 9
### БИЛЕТ 9 ВОПРОС 1
Основные техники:

Извлечение метода: вынести кусок кода в отдельную функцию с понятным именем.
Переименование: x → userAge.
Упрощение условий: заменить if (a == true) на if (a).
Удаление дублирования: одинаковый код в нескольких местах → вынести в функцию.
Пример (до и после):
// До
```
double price = quantity * 10;
if (quantity > 10) price = price * 0.9;
if (customer.isVip()) price = price * 0.95;
```

```
// После
double calculatePrice(int quantity, Customer customer) {
    double basePrice = quantity * 10;
    double discount = calculateDiscount(quantity, customer);
    return basePrice * (1 - discount);
}
```

### Вопрос 2 Использование в коде (Java):
```
String email = "test@example.com";
boolean isValid = email.matches("^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}$");
```
[Содержание](#содержание)
## Билет 10
### Билет 10 вопрос 2 
пример на c#

```
public async Task<string> GetUserEmailAsync(int userId)
{
    try
    {
        var user = await _dbContext.Users.FindAsync(userId);
        return user?.Email ?? "not found";
    }
    catch (Exception ex)
    {
        _logger.LogError(ex, "Ошибка при получении email");
        throw;
    }
}
```

### Вопрос 3
```
paths:
  /api/v1/projects/{id}:
    get:
      summary: Получить проект по ID
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: integer
      responses:
        '200':
          description: Успешно
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Project'
        '404':
          description: Проект не найден
```
[Содержание](#содержание)
## Билет 12
### Билет 12 Вопрос 1
Observer (Наблюдатель)
Код джава
```
interface Observer { void update(String news); }
class NewsAgency {
    private List<Observer> observers = new ArrayList<>();
    public void addObserver(Observer o) { observers.add(o); }
    public void publishNews(String news) {
        observers.forEach(o -> o.update(news));
    }
}
Strategy (Стратегия)

interface SortStrategy { void sort(List<Item> items); }
class PriceSort implements SortStrategy { ... }
class RatingSort implements SortStrategy { ... }
class Catalog {
    private SortStrategy strategy;
    public void setSortStrategy(SortStrategy s) { this.strategy = s; }
    public void display() { strategy.sort(items); ... }
}

Command (Команда)

interface Command { void execute(); void undo(); }
class LightOnCommand implements Command {
    public void execute() { light.turnOn(); }
    public void undo() { light.turnOff(); }
}
```

### Билет 12 Вопрос 2
Переопределение для окружений:

Использовать отдельные файлы: appsettings.Development.json, appsettings.Production.json.
Или переменные окружения: DB_HOST=prod-db.
Пример (C#):
```
// appsettings.Production.json
{
  "ConnectionStrings": {
    "Default": "Server=prod-db;..."
  },
  "ApiKeys": {
    "PaymentService": "..." // лучше брать из Key Vault!
  }
}
```
### Вопрос 3
```
public class PaymentService
{
    public async Task<string> CreatePaymentIntent(decimal amount)
    {
        var options = new PaymentIntentCreateOptions { Amount = (long)(amount * 100), Currency = "usd" };
        var service = new PaymentIntentService();
        var intent = await service.CreateAsync(options);
        return intent.ClientSecret; // передаётся клиенту
    }

    public void HandleWebhook(string json, string signature)
    {
        var stripeEvent = EventUtility.ConstructEvent(json, signature, webhookSecret);
        if (stripeEvent.Type == Events.PaymentIntentSucceeded)
        {
            var paymentIntent = stripeEvent.Data.Object as PaymentIntent;
            // Обновить заказ в БД
        }
    }
}
```
[Содержание](#содержание)
## Билет 13 
### Вопрос 1
Когда что использовать?

Нужен быстрый поиск по индексу → ArrayList.
Часто вставляете в начало/середину → LinkedList.
Нужен уникальный набор без порядка → HashSet.
Нужны уникальные элементы в сортированном виде → TreeSet.
Нужны уникальные элементы в порядке добавления → LinkedHashSet.
Пример на Java:
```
List<String> tasks = new ArrayList<>();
tasks.add("Купить хлеб");
tasks.add("Сделать домашку");

Set<String> uniqueTags = new HashSet<>();
uniqueTags.add("urgent");
uniqueTags.add("urgent"); // не добавится второй раз

Map<Integer, String> userIdToName = new HashMap<>();
userIdToName.put(1, "Алиса");
```
### Вопрос 2 
Зачем нужно?

Для фреймворков: сериализация (JSON → объект), ORM (Entity Framework), dependency injection.
Для тестовых фреймворков (JUnit).
Для плагинов и динамической загрузки кода.
Пример на Java:
```
Class<?> clazz = Class.forName("com.example.User");
Object obj = clazz.getDeclaredConstructor().newInstance();

Method method = clazz.getMethod("getName");
String name = (String) method.invoke(obj); // вызов метода
```

### Вопрос 3
Пример CRUD (Spring Boot):

Model: Product (сущность JPA).
Controller:
@GetMapping("/products")
```
public String list(Model model) {
    model.addAttribute("products", productService.findAll());
    return "products/list"; // имя шаблона View
}
```
[Содержание](#содержание)
## Билет 14 
### Вопрос 2
JSON — лёгкий текстовый формат:
```
{ "name": "Алиса", "age": 25, "active": true }
```
XML — более многословный, с тегами:
```
<user>
  <name>Алиса</name>
  <age>25</age>
</user>
```
### Вопрос 3
Пример (WPF + C#):

ViewModel:
```
public class MainViewModel : INotifyPropertyChanged
{
    private string _message = "Привет!";
    public string Message { 
        get => _message; 
        set { _message = value; OnPropertyChanged(); } 
    }
}
```
View (XAML):
<TextBlock Text="{Binding Message}" />
Пример на C# (JSON):
```
var user = new { Name = "Алиса", Age = 25 };
string json = JsonSerializer.Serialize(user);
var restored = JsonSerializer.Deserialize<User>(json);
```
[Содержание](#содержание)
## Билет 15 
### Вопрос 2
Пример на C#:
```
int retryCount = 0;
while (retryCount < 3)
{
    try
    {
        var response = await httpClient.GetAsync(url);
        return response;
    }
    catch (HttpRequestException)
    {
        await Task.Delay(TimeSpan.FromSeconds(Math.Pow(2, retryCount)));
        retryCount++;
    }
}
```

### Вопрос 3
Пример To-Do на React:
```
function TodoApp() {
  const [tasks, setTasks] = useState([]);
  const [input, setInput] = useState('');

  const addTask = () => {
    if (input.trim()) {
      setTasks([...tasks, { id: Date.now(), text: input, done: false }]);
      setInput('');
    }
  };

  return (
    <div>
      <input value={input} onChange={e => setInput(e.target.value)} />
      <button onClick={addTask}>Добавить</button>
      <ul>
        {tasks.map(task => (
          <li key={task.id}>{task.text}</li>
        ))}
      </ul>
    </div>
  );
}
```
[Содержание](#содержание)
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
[Содержание](#содержание)
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
[Содержание](#содержание)
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
[Содержание](#содержание)
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
[Содержание](#содержание)
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
[Содержание](#содержание)
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


[Содержание](#содержание)
## Билет 22
### Вопрос 1
Пример в package.json (npm):
```
{
  "dependencies": {
    "axios": "^1.6.0"
  }
}
```
### Вопрос 2
Пример оптимизации:
Сайт загружал style.css при каждом визите. После добавления:
```
Cache-Control: public, max-age=31536000, immutable
```
...и переименования файла в style.a1b2c3.css, браузер стал загружать его только один раз — даже при обновлении страницы. Это сократило время загрузки на 300 мс и уменьшило трафик на 80%.
Пример конфигурации (Nginx):
```
# Долгосрочное кэширование для ассетов
location ~* \.(js|css|png|jpg|svg)$ {
    expires 1y;
    add_header Cache-Control "public, immutable";
}

# Отключить кэш для HTML
location ~* \.html$ {
    add_header Cache-Control "no-cache, no-store, must-revalidate";
}
```
### Вопрос 3
Пример: авторизация через GitHub в веб-приложении на C# (ASP.NET Core)

Регистрация приложения на GitHub Developer Settings → создаём OAuth App, указываем Homepage URL и Authorization callback URL (https://localhost:5001/signin-github).
В коде настраиваем провайдера:
```
// Program.cs
builder.Services.AddAuthentication(options =>
{
    options.DefaultScheme = "Cookies";
    options.DefaultChallengeScheme = "GitHub";
})
.AddCookie("Cookies")
.AddGitHub("GitHub", options =>
{
    options.ClientId = "ваш_client_id";
    options.ClientSecret = "ваш_client_secret";
    options.Scope.Add("user:email"); // чтобы получить email
});
```
В контроллере — перенаправление и обработка:
```
[HttpGet("login")]
public IActionResult Login()
{
    return Challenge(new AuthenticationProperties(), "GitHub");
}

// После возврата с GitHub, ASP.NET Core автоматически:
// - получит код,
// - обменяет его на токен,
// - вызовет API /user и /user/emails,
// - создаст claims-принципала.
```


[Содержание](#содержание)
## Билет 23
### Вопрос 2
Основное правило: всегда используйте await при вызове асинхронного метода, если вы хотите поймать исключение. Тогда try-catch работает так же, как и в синхронном коде. Например, в C#:
```
try
{
    await DataService.LoadUserDataAsync();
}
catch (HttpRequestException ex)
{
    // обработка ошибки сети
}
```
...
....
...
Пример правильной обработки (C#):
```
public async Task ProcessOrdersAsync()
{
    try
    {
        var orders = await _orderService.GetPendingOrdersAsync();
        foreach (var order in orders)
        {
            try
            {
                await _paymentService.ProcessAsync(order);
            }
            catch (PaymentFailedException ex)
            {
                _logger.LogWarning(ex, "Payment failed for order {OrderId}", order.Id);
                // продолжить обработку других заказов
            }
        }
    }
    catch (Exception ex)
    {
        _logger.LogError(ex, "Critical failure in order processing");
        throw; // пробросить наверх, если это фатальная ошибка
    }
}
```
### Вопрос 3
Пример кода (на Python, упрощённо):
```
def get_similar_items(target_item, all_items, top_n=3):
    target_tags = set(target_item['tags'])
    scores = []
    for item in all_items:
        if item['id'] == target_item['id']:
            continue
        common = len(target_tags & set(item['tags']))
        scores.append((item['id'], common))
    return sorted(scores, key=lambda x: x[1], reverse=True)[:top_n]
```


[Содержание](#содержание)
## Билет 24
### Вопрос 1
####Примеры кода:
####Неизменяемый класс в C# (с record):
```
public record Person(string Name, int Age);
// После создания: var p = new Person("Alice", 30); — изменить нельзя
```
####Неизменяемый класс в Java:
```
public final class Person {
    private final String name;
    private final int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() { return name; }
    public int getAge() { return age; }
    // нет сеттеров!
}
```
### Вопрос 2
Примеры кода:
Форматирование и парсинг даты в C#
```
// Форматирование
string formatted = DateTime.Now.ToString("dd.MM.yyyy");

// Безопасный парсинг
if (DateTime.TryParse("31.12.2025", out DateTime date))
{
    Console.WriteLine(date);
}
```
Форматирование и парсинг в Java:
```
// Форматирование
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd.MM.yyyy");
String formatted = LocalDate.now().format(formatter);

// Парсинг с обработкой ошибки
try {
    LocalDate date = LocalDate.parse("31.12.2025", formatter);
} catch (DateTimeParseException ex) {
    System.err.println("Неверный формат даты");
}
```


[Содержание](#содержание)
## Билет 24
### Вопрос 3
Пример (C#):
Общий интерфейс (в основном приложении):
```
public interface IPlugin
{
    string Name { get; }
    void Execute();
}
```
Загрузка плагинов:
```
var plugins = new List<IPlugin>();
string pluginPath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "plugins");

foreach (string file in Directory.GetFiles(pluginPath, "*.dll"))
{
    var assembly = Assembly.LoadFrom(file);
    foreach (Type type in assembly.GetTypes())
    {
        if (typeof(IPlugin).IsAssignableFrom(type) && !type.IsInterface)
        {
            var instance = (IPlugin)Activator.CreateInstance(type);
            plugins.Add(instance);
        }
    }
}

// Запуск
foreach (var plugin in plugins)
{
    Console.WriteLine($"Запуск: {plugin.Name}");
    plugin.Execute();
}
```
Плагин (в отдельной сборке):
```
public class HelloPlugin : IPlugin
{
    public string Name => "Hello Plugin";
    public void Execute() => Console.WriteLine("Привет от плагина!");
}   
```


[Содержание](#содержание)
## Билет 25
### Вопрос 1
Пример рефакторинга:
До:
```
public class OrderProcessor
{
    public void ProcessOrder(Order order)
    {
        // 1. Сохранить в БД
        SaveToDatabase(order);
        // 2. Отправить email
        SendEmail(order.CustomerEmail, "Заказ принят");
        // 3. Сгенерировать PDF
        GeneratePdf(order);
    }
}
```
После (разделение по SRP):
```
public class OrderService
{
    private readonly IOrderRepository _repo;
    private readonly IEmailService _email;
    private readonly IPdfGenerator _pdf;

    public void ProcessOrder(Order order)
    {
        _repo.Save(order);
        _email.Send(order.CustomerEmail, "Заказ принят");
        _pdf.Generate(order);
    }
}
```
### Вопрос 2
Пример настройки Maven (pom.xml):
```
<profiles>
  <profile>
    <id>prod</id>
    <activation><activeByDefault>false</activeByDefault></activation>
    <properties>
      <log.level>WARN</log.level>
    </properties>
  </profile>
</profiles>

<dependencies>
  <dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-api</artifactId>
    <version>2.0.7</version>
  </dependency>
</dependencies>
```
Пример Gradle (Kotlin DSL):
```
dependencies {
    implementation("org.slf4j:slf4j-api:2.0.7")
    testImplementation("junit:junit:4.13.2")
}

tasks.named<Test>("test") {
    useJUnit()
}
```
### Вопрос 3
Пример (веб, CSS):
```
:root {
  --bg: #ffffff;
  --text: #000000;
}

body.dark {
  --bg: #121212;
  --text: #ffffff;
}

body {
  background: var(--bg);
  color: var(--text);
}
```
Пример (WPF, XAML):
```
<!-- LightTheme.xaml -->
<ResourceDictionary>
  <SolidColorBrush x:Key="WindowBackground" Color="White"/>
  <SolidColorBrush x:Key="TextForeground" Color="Black"/>
</ResourceDictionary>

<!-- В коде (C#) -->
void SwitchToLightTheme()
{
    var theme = new ResourceDictionary { Source = new Uri("LightTheme.xaml", UriKind.Relative) };
    Application.Current.Resources.MergedDictionaries.Clear();
    Application.Current.Resources.MergedDictionaries.Add(theme);
}
```



[Содержание](#содержание)
## Билет 26
### Вопрос 1
Пример (C#):
```
public class BankAccount
{
    private decimal _balance;

    // Инвариант: _balance >= 0 (проверяем в начале и конце каждого метода)

    public void Withdraw(decimal amount)
    {
        // Предусловие
        if (amount <= 0)
            throw new ArgumentException("Сумма должна быть положительной", nameof(amount));
        if (amount > _balance)
            throw new InvalidOperationException("Недостаточно средств");

        var oldBalance = _balance;
        _balance -= amount;

        // Постусловие + инвариант
        if (_balance < 0)
            throw new InvalidOperationException("Баланс не может быть отрицательным");
    }
}
```
### Вопрос 2
Пример безопасного хранения пароля (Java с Spring Security):
```
// При регистрации
String hashedPassword = passwordEncoder.encode(rawPassword); // bcrypt по умолчанию
userRepository.save(new User(email, hashedPassword));

// При входе
User user = userRepository.findByEmail(email);
if (passwordEncoder.matches(rawPassword, user.getHashedPassword())) {
    // успех
}
```
### Вопрос 2
Пример линейного графика на Chart.js (HTML/JS):
```
<canvas id="salesChart"></canvas>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script>
const ctx = document.getElementById('salesChart').getContext('2d');
new Chart(ctx, {
  type: 'line',
  data: {
    labels: ['Янв', 'Фев', 'Мар'],
    datasets: [{
      label: 'Продажи, тыс. руб.',
      data: [12, 19, 15],
      borderColor: 'blue'
    }]
  }
});
</script>
```
Пример круговой диаграммы (Chart.js):
```
new Chart(ctx, {
  type: 'pie',
  data: {
    labels: ['Продукт A', 'Продукт B', 'Продукт C'],
    datasets: [{
      data: [30, 50, 20],
      backgroundColor: ['#ff6384', '#36a2eb', '#cc65fe']
    }]
  }
});
```
Пример географической карты (Leaflet + OpenStreetMap):
```
<div id="map" style="height: 400px;"></div>
<script src="https://unpkg.com/leaflet@1.9.4/dist/leaflet.js"></script>
<link rel="stylesheet" href="https://unpkg.com/leaflet@1.9.4/dist/leaflet.css" />
<script>
const map = L.map('map').setView([55.75, 37.62], 10);
L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png').addTo(map);
L.marker([55.75, 37.62]).addTo(map).bindPopup('Москва');
</script>
```



[Содержание](#содержание)
## Билет 27
### Вопрос 2
Пример (отправка push через FCM в C#):
```
var message = new Message()
{
    Token = userDeviceToken,
    Notification = new Notification
    {
        Title = "Новый заказ",
        Body = "Ваш заказ №123 принят"
    }
};

await FirebaseMessaging.DefaultInstance.SendAsync(message);
```
Пример (отправка email через SendGrid в Java):
```
Email from = new Email("noreply@myapp.com");
Email to = new Email(user.getEmail());
Content content = new Content("text/plain", "Ваш заказ обработан");
Mail mail = new Mail(from, "Статус заказа", to, content);
SendGrid sg = new SendGrid("API_KEY");
Request request = new Request();
request.setMethod(Method.POST);
request.setEndpoint("mail/send");
request.setBody(mail.build());
sg.api(request);
```
### Вопрос3
Пример экспорта в CSV (C# + ASP.NET Core):
```
[HttpGet("export-csv")]
public IActionResult ExportCsv()
{
    var records = _db.Orders.Select(o => new { o.Id, o.Total }).ToList();
    using var writer = new StringWriter();
    using var csv = new CsvWriter(writer, CultureInfo.InvariantCulture);
    csv.WriteRecords(records);
    
    return File(Encoding.UTF8.GetBytes(writer.ToString()), 
                "text/csv", 
                "orders.csv");
}
```
Пример экспорта в PDF (Java + iText):
```
@GetMapping("/export-pdf")
public void exportPdf(HttpServletResponse response) throws IOException {
    response.setContentType("application/pdf");
    response.setHeader("Content-Disposition", "attachment; filename=report.pdf");

    PdfWriter writer = new PdfWriter(response.getOutputStream());
    PdfDocument pdf = new PdfDocument(writer);
    Document document = new Document(pdf);
    document.add(new Paragraph("Отчёт по продажам"));
    document.close();
}
```
Пример экспорта в Excel (C# + EPPlus):
```
using var package = new ExcelPackage();
var worksheet = package.Workbook.Worksheets.Add("Orders");
worksheet.Cells["A1"].Value = "ID";
worksheet.Cells["B1"].Value = "Total";
// ... заполнение данных
return File(package.GetAsByteArray(), "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet", "orders.xlsx");
```



[Содержание](#содержание)
## Билет 28
### Вопрос 2
Пример (Elasticsearch):

1.Индексация документа:
```
POST /products/_doc
{
  "name": "Беспроводная мышь Logitech",
  "description": "Удобная мышь для работы и игр"
}
```
2.Поиск:
```
GET /products/_search
{
  "query": {
    "match": {
      "name": "беспроводная мышь"
    }
  }
}
```
Elasticsearch вернёт результаты, отсортированные по релевантности, даже если пользователь введёт «мышки беспроводные».

Пример на стороне приложения (C#):
```
var response = await elasticClient.SearchAsync<Product>(s => s
    .Query(q => q
        .Match(m => m
            .Field(f => f.Name)
            .Query(searchTerm)
        )
    )
);
```
### Вопрос 3
Пример мобильного эндпоинта (REST):
```
GET /api/v1/news?fields=id,title,preview&limit=10
```
Ответ:
```
{
  "data": [
    {
      "id": 101,
      "title": "Новость дня",
      "preview": "Краткое содержание..."
    }
  ],
  "meta": {
    "next_cursor": "abc123"
  }
}
```
Пример на стороне клиента (Android, Kotlin):
```
// Использование Retrofit + OkHttp с автоматическим кэшированием
val okHttpClient = OkHttpClient.Builder()
    .cache(Cache(context.cacheDir, 10 * 1024 * 1024)) // 10 МБ кэша
    .build()

val retrofit = Retrofit.Builder()
    .baseUrl("https://api.myapp.com/")
    .client(okHttpClient)
    .addConverterFactory(GsonConverterFactory.create())
    .build()
```



[Содержание](#содержание)
## Билет 29
### Вопрос 1
Примеры:
Сценарий 1: Ожидаемая ошибка (логин)
```
// Лучше вернуть Result, а не бросать исключение
if (!userService.ValidateCredentials(login, password))
    return BadRequest("Invalid credentials");
```
Сценарий 2: Неожиданная ошибка (БД недоступна)
```
try
{
    var user = await _db.Users.FindAsync(id);
}
catch (SqlException ex)
{
    _logger.LogError(ex, "Database unreachable");
    throw new ServiceUnavailableException("Try again later", ex);
}
```
Сценарий 3: Правильный проброс
```
try
{
    // ...
}
catch (Exception)
{
    _logger.LogWarning("Partial failure");
    throw; // сохраняет стек, а не throw ex;
}
```
### Вопрос 2
Пример реализации кэша с TTL на C# (встроенный MemoryCache):
```
public class ProductService
{
    private readonly IMemoryCache _cache;
    private readonly IDbService _db;

    public ProductService(IMemoryCache cache, IDbService db)
    {
        _cache = cache;
        _db = db;
    }

    public async Task<Product> GetProductAsync(int id)
    {
        // Попытка получить из кэша
        if (_cache.TryGetValue($"product_{id}", out Product product))
            return product;

        // Иначе — из БД
        product = await _db.GetProductByIdAsync(id);
        
        // Сохранить в кэш на 10 минут
        _cache.Set($"product_{id}", product, TimeSpan.FromMinutes(10));
        return product;
    }
}
```
Пример на Java с Caffeine (LRU + TTL):
```
Cache<Integer, Product> cache = Caffeine.newBuilder()
    .maximumSize(1000)          // макс. 1000 элементов
    .expireAfterWrite(10, TimeUnit.MINUTES)
    .build();

public Product getProduct(int id) {
    return cache.get(id, this::loadFromDatabase);
}
```
### Вопрос 3
Пример (C# + AutoUpdater.NET):

1.На сервере размещается XML-файл:
```
<item>
  <version>2.1.0</version>
  <url>https://myapp.com/installer.exe</url>
</item>
```
2.В приложении:
```
// При запуске
AutoUpdater.Start("https://myapp.com/version.xml");
// Библиотека автоматически проверит, скачает и предложит установить обновление
```
Пример (Android — проверка версии):
```
// Запрос к API
val response = apiService.getLatestVersion()
if (Version.compare(response.latest, BuildConfig.VERSION_NAME) > 0) {
    // Показать диалог "Доступна новая версия"
    startActivity(Intent(Intent.ACTION_VIEW, Uri.parse("market://details?id=com.myapp")))
}
```



[Содержание](#содержание)
## Билет 30
### Вопрос 1
Пример (C# — сериализация с атрибутами):
```
public class User
{
    [JsonProperty("user_id")]
    public int Id { get; set; }

    [JsonIgnore]
    public string Password { get; set; }
}
// Библиотека Json.NET читает атрибуты и формирует JSON автоматически.
```
Пример (Java — валидация через аннотации):
```
public class User {
    @NotBlank
    @Email
    private String email;
    
    @Min(18)
    private int age;
}
// Hibernate Validator проверяет объект при вызове validator.validate(user).
```
### Вопрос 2
Пример интеграции (Java + Spring Boot + OpenTelemetry):

1.Добавить зависимости:
```
<dependency>
  <groupId>io.opentelemetry.instrumentation</groupId>
  <artifactId>opentelemetry-spring-boot-starter</artifactId>
</dependency>
```
2.Настроить экспорт в Jaeger:
```
otel.traces.exporter: jaeger
otel.exporter.jaeger.endpoint: http://jaeger:14250
```
