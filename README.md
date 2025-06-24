# Ответы на вопросы по системам программирования и ООП

## 1. Состав системы программирования. Интегрированная среда разработки. Проект, группа проектов

**Состав системы программирования:**
- Интегрированная среда разработки (IDE)
- Компилятор или интерпретатор
- Средства создания и редактирования текстов программ
- Библиотеки стандартных программ и функций
- Отладочные программы
- Дружественная диалоговая среда
- Многооконный режим работы
- Встроенная справочная служба

**IDE** - это одна программа, обеспечивающая весь процесс разработки, в отличие от утилит командной строки (vi, GCC, make).

**Проект** - набор взаимосвязанных процедур и данных. Группа проектов позволяет:
- Доступ к исходному коду всех проектов группы
- Использование одних и тех же библиотек
- Общие настройки компилятора
- Зависимость проектов и автоматическую перекомпиляцию
- Отладку exe+lib/dll

## 2. Текстовый редактор: специальные функции для поддержки программирования

**Специальные функции:**
- **Подсветка синтаксиса** - выделение ключевых слов, комментариев, строк разными цветами
- **Автодополнение** - предложение вариантов завершения кода
- **Проверка синтаксиса** в реальном времени
- **Автоматическое форматирование** и отступы
- **Парное выделение скобок** - подсвечивание соответствующих скобок
- **Сворачивание кода** - возможность скрыть блоки кода
- **Навигация по коду** - быстрый переход к функциям, классам
- **Поиск и замена** с поддержкой регулярных выражений
- **Интеграция с системой контроля версий**

```cpp
// Пример подсветки синтаксиса и автодополнения
#include <iostream>  // системный заголовок - синий
using namespace std; // ключевое слово - фиолетовый

int main() {         // тип данных - зеленый
    cout << "Hello"; // строка - красная
    return 0;        // ключевое слово - фиолетовый
}
// При наборе "cou" редактор предложит "cout"
```

## 3. Преимущества и недостатки компиляторов и интерпретаторов

### Интерпретаторы

**Достоинства:**
- Относительная независимость от платформы исполнения
- Упрощается построчная отладка программы
- Более совершенные средства диагностики ошибок

**Недостатки:**
- Программы выполняются медленнее (декодирование занимает время)
- Требуют больше памяти (программа + данные + интерпретатор + таблица символов)
- Программа не может выполняться без интерпретатора
- Практически нет оптимизации кода

```cpp
// Интерпретируемый код (JavaScript-подобный)
x = 10;              // каждая строка анализируется во время выполнения
if (x > 5) {         // условие проверяется интерпретатором
    print("больше"); // функция ищется в таблице символов
}
// Интерпретатор должен быть установлен для выполнения
```

### Компиляторы

**Достоинства:**
- Быстрое выполнение программы (машинный код)
- Меньше требований к памяти при выполнении
- Автономное выполнение без дополнительных программ
- Возможность оптимизации кода

**Недостатки:**
- Зависимость от платформы
- Более сложная отладка
- Необходимость перекомпиляции при изменениях

```cpp
// Компилируемый код
int x = 10;          // компилятор переводит в машинные команды
if (x > 5) {         // условие становится командой процессора
    printf("больше"); // адрес функции определяется при компиляции
}
// Результат: исполняемый .exe файл, работающий без компилятора
```

## 4. Редактор связей. PE формат: применение, секции. Использование и создание библиотек

**Редактор связей (linker):**
- Принимает объектные модули и собирает исполняемый модуль
- Использует таблицы имен из объектных модулей
- Разрешает ссылки на неопределенные имена

```cpp
// Файл1.cpp
extern int x2;       // неопределенное имя (импорт)
int f2();           // объявление внешней функции
int f1(int a) {     // определенное имя (экспорт)
    x2 = f2();      // использование внешних символов
    return a + x2;
}

// Файл2.cpp  
int x2 = 100;       // определение переменной (экспорт)
int f2() {          // определение функции (экспорт)
    return x2 * 2;
}
// Линкер связывает f1 с f2 и x2
```

**PE (Portable Executable) формат:**
- Произошел из Unix-формата COFF
- Применяется в Windows для EXE, DLL, OBJ, SYS
- **Основные секции:**
  - `.text` - исполняемый код
  - `.data` - инициализированные данные
  - `IAT` - таблица импортируемых адресов
  - `EAT` - таблица экспортируемых адресов
  - `IL` - промежуточный язык (.NET)

**Динамическое связывание:**
```cpp
#include <windows.h>

// Загрузка DLL во время выполнения
HMODULE hLib = LoadLibrary("mymath.dll");
if (hLib != NULL) {
    // Получение адреса функции из DLL
    typedef int (*AddFunc)(int, int);
    AddFunc add = (AddFunc)GetProcAddress(hLib, "add");
    
    if (add != NULL) {
        int result = add(5, 3);  // вызов функции из DLL
        printf("Результат: %d\n", result);
    }
    FreeLibrary(hLib);  // освобождение DLL
}
```

## 5. Отладчик: управление выполнением программы, точки останова, окна

**Управление выполнением:**
- **Run** - запуск программы
- **Step over** - выполнить строку, не заходя в функции
- **Step into** - выполнить строку, заходя в функции
- **Step out** - выйти из текущей функции
- **Run to cursor** - выполнить до позиции курсора
- **Stop/Restart** - остановка и перезапуск

```cpp
int factorial(int n) {
    if (n <= 1)      // [F9] - поставить breakpoint здесь
        return 1;    // [F10] - Step over (не входить в рекурсию)
    return n * factorial(n-1); // [F11] - Step into (войти в рекурсию)
}                    // [Shift+F11] - Step out (выйти из функции)

int main() {
    int x = 5;       // Добавить x в окно Watch
    int result = factorial(x); // [Ctrl+F10] - Run to cursor
    return 0;
}
```

**Точки останова (breakpoints):**
```cpp
int sum = 0;
for (int i = 0; i < 100; i++) {
    sum += i;        // Breakpoint с условием: i == 50
}                    // Breakpoint с счетчиком: остановиться на 10-й итерации

int* ptr = new int[1000];
ptr[500] = 42;       // Data breakpoint: остановиться при записи в ptr[500]
```

**Окна отладчика:**
- **Call stack** - показывает: main() → factorial(5) → factorial(4)
- **Locals** - автоматически показывает локальные переменные: n=4, result=24
- **Watch** - пользовательские выражения: n*2, ptr[i], obj.member
- **Memory** - содержимое памяти в шестнадцатеричном виде

## 6. Парадигма процедурного программирования

**Основная идея:** Программа состоит из функций и процедур, которые оперируют с данными.

**Принципы:**
- Разделение кода на функции/процедуры
- Передача параметров между функциями
- Возврат результатов из функций
- Многократное использование кода через вызовы функций

```cpp
// Процедурный подход - функции работают с глобальными данными
int balance = 1000;    // глобальные данные

void deposit(int amount) {     // процедура изменения данных
    balance += amount;
    printf("Пополнено на %d. Баланс: %d\n", amount, balance);
}

bool withdraw(int amount) {    // функция с возвращаемым значением
    if (balance >= amount) {
        balance -= amount;
        printf("Снято %d. Баланс: %d\n", amount, balance);
        return true;           // успешная операция
    }
    return false;              // недостаточно средств
}

int main() {
    deposit(500);              // вызов процедуры
    bool success = withdraw(200); // вызов функции
    return 0;
}
```

## 7. Парадигма модульного программирования

**Причины появления:**
- Возрастание размера программ
- Работа нескольких программистов над одной программой

**Принцип:** Разделение программы на относительно независимые части (модули).

```cpp
// stack.h - интерфейс модуля (что доступно извне)
#ifndef STACK_H
#define STACK_H

void push(char c);           // публичные функции
char pop();
bool isEmpty();
const int STACK_SIZE = 100;  // публичная константа

#endif

// stack.cpp - реализация модуля (скрытая от пользователя)
#include "stack.h"

static char stack[STACK_SIZE]; // private данные модуля
static int top = 0;            // private переменная

void push(char c) {            // реализация публичной функции
    if (top < STACK_SIZE) {
        stack[top++] = c;
    }
}

char pop() {                   // реализация публичной функции
    if (top > 0) {
        return stack[--top];
    }
    return '\0';
}

// main.cpp - использование модуля
#include "stack.h"             // подключение интерфейса

int main() {
    push('A');                 // используем функции модуля
    push('B');
    char c = pop();            // получаем 'B'
    // stack и top недоступны напрямую - инкапсуляция!
    return 0;
}
```

## 8. Парадигма абстракции данных

**Цель:** Возможность вводить новые понятия - абстрактные типы данных, определенные пользователем.

**Принципы:**
- Определить, какие типы вам нужны
- Предоставить полный набор операций для каждого типа
- Скрыть внутреннее представление данных

```cpp
// Абстрактный тип данных "Комплексное число"
struct Complex {
    double real, imag;         // внутреннее представление
    
    // Конструкторы для создания объектов
    Complex(double r = 0, double i = 0) : real(r), imag(i) {}
    
    // Полный набор операций для типа
    Complex operator+(const Complex& other) const {
        return Complex(real + other.real, imag + other.imag);
    }
    
    Complex operator*(const Complex& other) const {
        return Complex(real * other.real - imag * other.imag,
                      real * other.imag + imag * other.real);
    }
    
    double magnitude() const {
        return sqrt(real * real + imag * imag);
    }
    
    void print() const {
        printf("(%.2f + %.2fi)", real, imag);
    }
};

// Использование как встроенный тип
int main() {
    Complex a(3, 4);           // создание объектов
    Complex b(1, 2);
    Complex c = a + b;         // естественная запись операций
    c.print();                 // (4.00 + 6.00i)
    
    double mag = a.magnitude(); // использование методов
    printf("Модуль: %.2f", mag); // 5.00
    return 0;
}
```

## 9. ООП: класс, инкапсуляция

**Основные концепции ООП:**
- Система состоит из объектов
- Объекты взаимодействуют между собой
- Каждый объект имеет состояние и поведение
- Состояние задается полями данных
- Поведение задается методами

```cpp
class BankAccount {
private:                       // инкапсуляция - скрытие данных
    string owner;              // состояние объекта
    double balance;
    string accountNumber;
    
public:                        // публичный интерфейс
    // Конструктор - инициализация объекта
    BankAccount(const string& name, const string& number) 
        : owner(name), balance(0.0), accountNumber(number) {
        cout << "Счет " << number << " создан для " << name << endl;
    }
    
    // Методы - поведение объекта
    void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            cout << "Пополнено на " << amount << ". Баланс: " << balance << endl;
        }
    }
    
    bool withdraw(double amount) {
        if (amount > 0 && balance >= amount) {
            balance -= amount;
            cout << "Снято " << amount << ". Баланс: " << balance << endl;
            return true;
        }
        cout << "Операция невозможна" << endl;
        return false;
    }
    
    // Геттер для чтения приватных данных
    double getBalance() const { return balance; }
    string getOwner() const { return owner; }
};

int main() {
    BankAccount acc1("Иван Петров", "12345");  // создание объекта
    BankAccount acc2("Мария Сидорова", "67890");
    
    acc1.deposit(1000);        // вызов методов объекта
    acc1.withdraw(300);
    
    // balance недоступен напрямую - инкапсуляция!
    // cout << acc1.balance;   // ОШИБКА!
    cout << acc1.getBalance(); // OK - через публичный метод
    
    return 0;
}
```

## 10. ООП: наследование

**Наследование** - механизм создания нового класса на основе существующего с расширением или изменением функциональности.

```cpp
// Базовый класс (суперкласс)
class Shape {
protected:                     // доступно в наследниках
    double x, y;               // координаты центра
    string color;
    
public:
    Shape(double px, double py, const string& c) 
        : x(px), y(py), color(c) {}
    
    // Виртуальная функция - разная реализация в наследниках
    virtual double area() const = 0;  // чисто виртуальная
    virtual void draw() const {       // виртуальная с реализацией
        cout << "Рисую " << color << " фигуру в (" << x << "," << y << ")";
    }
    
    // Обычная функция - одинакова для всех наследников
    void move(double dx, double dy) {
        x += dx; y += dy;
        cout << "Перемещено на (" << dx << "," << dy << ")" << endl;
    }
};

// Производный класс (подкласс)
class Circle : public Shape {   // наследование от Shape
private:
    double radius;              // дополнительные данные
    
public:
    Circle(double px, double py, double r, const string& c) 
        : Shape(px, py, c), radius(r) {}  // вызов конструктора базового класса
    
    // Переопределение виртуальной функции
    double area() const override {
        return 3.14159 * radius * radius;
    }
    
    // Переопределение виртуальной функции
    void draw() const override {
        Shape::draw();          // вызов базовой версии
        cout << " радиусом " << radius << endl;
    }
    
    // Дополнительный метод только для Circle
    double circumference() const {
        return 2 * 3.14159 * radius;
    }
};

class Rectangle : public Shape {
private:
    double width, height;
    
public:
    Rectangle(double px, double py, double w, double h, const string& c)
        : Shape(px, py, c), width(w), height(h) {}
    
    double area() const override {
        return width * height;
    }
    
    void draw() const override {
        Shape::draw();
        cout << " размером " << width << "x" << height << endl;
    }
};

// Полиморфизм - единый интерфейс для разных типов
int main() {
    // Создание объектов разных классов
    Circle circle(10, 20, 5, "красный");
    Rectangle rect(0, 0, 10, 15, "синий");
    
    // Полиморфизм через указатели на базовый класс
    Shape* shapes[] = {&circle, &rect};
    
    for (int i = 0; i < 2; i++) {
        shapes[i]->draw();      // вызывается правильная версия draw()
        cout << "Площадь: " << shapes[i]->area() << endl;
        shapes[i]->move(5, 5);  // общий метод для всех фигур
        cout << "---" << endl;
    }
    
    // Специфичные методы через приведение типов
    Circle* pCircle = dynamic_cast<Circle*>(shapes[0]);
    if (pCircle) {
        cout << "Длина окружности: " << pCircle->circumference() << endl;
    }
    
    return 0;
}
```

**Парадигма ООП:** "Определите, какой класс вам необходим; предоставьте полный набор операций для каждого класса; общность классов выразите явно с помощью наследования"

## 11. Контроль типа и виртуальные методы. Механизм вызова виртуальных функций

**Контроль типа** - это способность определить реальный тип объекта во время выполнения программы. Есть 4 способа:
1. Ограничить указатель одним типом
2. Добавить поле типа в базовый класс
3. Использовать виртуальные методы
4. Использовать RTTI

**Механизм виртуальных функций:**
- При создании объекта в него помещается указатель на таблицу виртуальных функций (vtable)
- При вызове виртуальной функции компилятор ищет её адрес в этой таблице
- Это позволяет вызывать правильную функцию даже если точный тип неизвестен

```cpp
class Shape {
public:
    virtual void draw() = 0;  // чисто виртуальная
};

class Circle : public Shape {
public:
    void draw() override { cout << "Drawing circle"; }
};

Shape* p = new Circle();
p->draw();  // Вызовется Circle::draw()
```

## 12. Конструкторы и деструкторы

**Конструктор** - специальная функция для инициализации объекта:
- Имеет то же имя, что и класс
- Вызывается автоматически при создании объекта
- Может быть несколько (перегрузка)

**Деструктор** - функция для освобождения ресурсов:
- Имеет имя класса с символом ~ 
- Вызывается автоматически при уничтожении объекта
- Может быть только один

```cpp
class Vector {
    int* data;
    int size;
public:
    Vector(int s) : size(s) {           // конструктор
        data = new int[size];
    }
    
    ~Vector() {                         // деструктор
        delete[] data;
    }
};
```

## 13. Создание и удаление объектов

**Конструкторы вызываются:**
- При объявлении объекта: `Vector v(10);`
- При создании через new: `Vector* p = new Vector(10);`
- При копировании: `Vector v2 = v1;`
- При создании временного объекта

**Деструкторы вызываются:**
- При выходе из области видимости (для локальных объектов)
- При вызове delete (для объектов в куче)
- При завершении программы (для глобальных объектов)

```cpp
void func() {
    Vector v1(5);        // конструктор
    Vector* v2 = new Vector(10);  // конструктор
    
    delete v2;           // деструктор для v2
}                        // деструктор для v1
```

## 14. Иерархия классов, конструкторы производных классов

В производном классе **сначала** вызывается конструктор базового класса, **потом** производного.

При уничтожении - **наоборот**: сначала деструктор производного, потом базового.

```cpp
class Employee {
    char name[128];
    int age;
public:
    Employee(char* n, int a) { /* инициализация */ }
};

class Manager : public Employee {
    int level;
public:
    Manager(char* n, int a, int l) 
        : Employee(n, a), level(l) {  // вызов конструктора базового класса
        // дополнительная инициализация
    }
};
```

## 15. Уточнение имени. Вызов функций базового класса

Когда нужно уточнение имени:
- При конфликте имён
- При обращении к глобальной функции
- При вызове функции базового класса

```cpp
class Base {
public:
    void print() { cout << "Base"; }
};

class Derived : public Base {
public:
    void print() { 
        Base::print();    // вызов функции базового класса
        cout << "Derived";
    }
    
    void func() {
        ::printf("global");  // глобальная функция
        this->print();       // функция этого класса
    }
};
```

## 16. Контроль доступа, друзья

**Уровни доступа:**
- `private` - доступ только внутри класса
- `protected` - доступ внутри класса и производных классов
- `public` - доступ отовсюду

**Friend** - позволяет другому классу или функции получить доступ к приватным членам:

```cpp
class Vector {
    float v[4];
public:
    friend class Matrix;                    // класс-друг
    friend Vector multiply(Matrix*, Vector*); // функция-друг
};

class Matrix {
public:
    void func(Vector& vec) {
        vec.v[0] = 5.0;  // доступ к приватному члену
    }
};
```

## 17. Виртуальные методы. Абстрактные классы

**Виртуальный метод** - может быть переопределён в производных классах:

**Абстрактный класс** - содержит чисто виртуальные функции (= 0):

```cpp
class Shape {  // абстрактный класс
public:
    virtual void draw() = 0;     // чисто виртуальная
    virtual void rotate(int) = 0;
};

class Circle : public Shape {
public:
    void draw() override {       // обязательно переопределить
        // рисование круга
    }
    void rotate(int angle) override {
        // поворот круга
    }
};

// Shape s;     // ОШИБКА! Нельзя создать объект абстрактного класса
Circle c;       // OK
```

## 18. Ссылка на себя (this). Ключевое слово const

**this** - указатель на текущий объект:

```cpp
class MyClass {
    int value;
public:
    void setValue(int value) {
        this->value = value;  // разрешение конфликта имён
    }
    
    MyClass& operator=(const MyClass& other) {
        if (this != &other) {  // проверка самоприсваивания
            value = other.value;
        }
        return *this;  // возврат ссылки на себя
    }
};
```

**const методы** не могут изменять состояние объекта:

```cpp
class Point {
    int x, y;
public:
    int getX() const { return x; }        // const метод
    void setX(int newX) { x = newX; }     // не const
    
    void func(const Point& p) {
        int val = p.getX();  // OK - const метод
        // p.setX(5);        // ОШИБКА - не const метод
    }
};
```

## 19. Вложенные классы

Класс, определённый внутри другого класса. Имеет доступ к приватным членам внешнего класса:

```cpp
class OuterClass {
private:
    int outerData;
    
    class InnerClass {      // вложенный класс
    public:
        void accessOuter(OuterClass& outer) {
            outer.outerData = 10;  // доступ к приватным данным
        }
    };
    
public:
    InnerClass inner;
};

void func() {
    OuterClass outer;
    OuterClass::InnerClass inner;  // создание объекта вложенного класса
}
```

## 20. Выделение памяти для небольших объектов

Для оптимизации можно переопределить операторы new и delete:

```cpp
class SmallObject {
    static const int POOL_SIZE = 100;
    static char memoryPool[POOL_SIZE * sizeof(SmallObject)];
    static bool used[POOL_SIZE];
    
public:
    void* operator new(size_t size) {
        // найти свободный блок в пуле
        for (int i = 0; i < POOL_SIZE; i++) {
            if (!used[i]) {
                used[i] = true;
                return &memoryPool[i * sizeof(SmallObject)];
            }
        }
        return nullptr;  // пул переполнен
    }
    
    void operator delete(void* ptr, size_t size) {
        if (ptr) {
            // найти индекс в пуле и освободить
            char* charPtr = static_cast<char*>(ptr);
            int index = (charPtr - memoryPool) / sizeof(SmallObject);
            used[index] = false;
        }
    }
};

// Инициализация статических членов
char SmallObject::memoryPool[POOL_SIZE * sizeof(SmallObject)];
bool SmallObject::used[POOL_SIZE] = {false};
```

**Преимущества собственного управления памятью:**
- Быстрое выделение/освобождение
- Уменьшение фрагментации
- Контроль над размещением объектов в памяти

## 21. Большие объекты как параметры методов. Указатели на методы

**Большие объекты как параметры:**
При передаче больших объектов в функции нужно избегать копирования, используя ссылки или указатели.

```cpp
class Matrix {
    double m[4][4];
public:
    // Передача по ссылке для избежания копирования
    Matrix operator+(const Matrix& other) const;
    void multiply(const Matrix& a, const Matrix& b);
};
```

**Указатели на методы:**
Позволяют хранить и вызывать методы класса динамически.

```cpp
class Calculator {
public:
    int add(int a, int b) { return a + b; }
    int multiply(int a, int b) { return a * b; }
};

// Указатель на метод
int (Calculator::*operation)(int, int) = &Calculator::add;
Calculator calc;
int result = (calc.*operation)(5, 3); // Вызов через указатель
```

## 22. Множественное наследование в С++

Класс может наследоваться от нескольких базовых классов одновременно.

```cpp
class Temporary {
public:
    bool isTemp() { return true; }
};

class Employee {
protected:
    string name;
public:
    void setName(string n) { name = n; }
};

// Множественное наследование
class TempEmployee : public Temporary, public Employee {
public:
    void work() {
        setName("Temp Worker");
        if (isTemp()) {
            cout << "Working temporarily" << endl;
        }
    }
};
```

**Проблемы:** конфликты имен, ромбовидное наследование.

## 23. Операторные функции в С++

Позволяют переопределить поведение операторов для пользовательских типов.

**Как методы класса:**
```cpp
class Complex {
    double real, imag;
public:
    Complex(double r = 0, double i = 0) : real(r), imag(i) {}
    
    // Оператор как метод класса
    Complex operator+(const Complex& other) const {
        return Complex(real + other.real, imag + other.imag);
    }
};
```

**Как глобальные функции:**
```cpp
// Глобальная функция (обычно friend)
Complex operator*(const Complex& a, const Complex& b) {
    return Complex(a.real * b.real - a.imag * b.imag,
                   a.real * b.imag + a.imag * b.real);
}
```

## 24. Оператор присваивания и инициализация

Это **разные** операции:

```cpp
class Vector {
    int* data;
    int size;
public:
    // Конструктор копирования (инициализация)
    Vector(const Vector& other) : size(other.size) {
        data = new int[size];
        for(int i = 0; i < size; i++) {
            data[i] = other.data[i];
        }
    }
    
    // Оператор присваивания
    Vector& operator=(const Vector& other) {
        if(this != &other) { // Проверка самоприсваивания
            delete[] data;   // Освобождаем старую память
            size = other.size;
            data = new int[size];
            for(int i = 0; i < size; i++) {
                data[i] = other.data[i];
            }
        }
        return *this;
    }
};

// Использование:
Vector v1(10);      // Конструктор
Vector v2 = v1;     // Инициализация (конструктор копирования)
Vector v3(5);
v3 = v1;           // Присваивание (operator=)
```

## 25. Оператор индексации

Позволяет использовать объекты как массивы.

```cpp
class Vector {
    int* data;
    int size;
public:
    // Возвращаем ссылку для возможности изменения
    int& operator[](int index) {
        if(index < 0 || index >= size) {
            throw out_of_range("Index out of bounds");
        }
        return data[index];
    }
    
    // Константная версия
    const int& operator[](int index) const {
        if(index < 0 || index >= size) {
            throw out_of_range("Index out of bounds");
        }
        return data[index];
    }
};

// Использование:
Vector v(10);
v[0] = 42;          // Запись
int x = v[0];       // Чтение
```

## 26. Шаблоны

Позволяют создавать обобщенные классы и функции.

**Определение внутри класса:**
```cpp
template<class T>
class Stack {
    T* data;
    int top, maxSize;
public:
    Stack(int size) : top(0), maxSize(size) {
        data = new T[maxSize];
    }
    
    // Метод определен внутри класса
    void push(const T& item) {
        if(top < maxSize) {
            data[top++] = item;
        }
    }
    
    T pop(); // Объявление метода
};

// Определение вне класса
template<class T>
T Stack<T>::pop() {
    if(top > 0) {
        return data[--top];
    }
    throw runtime_error("Stack is empty");
}

// Использование:
Stack<int> intStack(100);
Stack<string> stringStack(50);
```

## 27. Принципы организации библиотек контейнерных классов

**Основные принципы:**
- **Типизация:** контейнеры хранят элементы определенного типа
- **Итераторы:** единообразный способ обхода элементов
- **Алгоритмы:** независимые от контейнеров функции обработки
- **Распределители памяти:** управление выделением/освобождением памяти

```cpp
// Простой пример контейнера
template<class T>
class SimpleList {
    struct Node {
        T data;
        Node* next;
        Node(const T& d) : data(d), next(nullptr) {}
    };
    
    Node* head;
public:
    class Iterator {
        Node* current;
    public:
        Iterator(Node* node) : current(node) {}
        T& operator*() { return current->data; }
        Iterator& operator++() { current = current->next; return *this; }
        bool operator!=(const Iterator& other) { return current != other.current; }
    };
    
    Iterator begin() { return Iterator(head); }
    Iterator end() { return Iterator(nullptr); }
};
```

## 28. «Классические» способы обработки ошибок

**Основные варианты:**
1. **Завершить программу** (`exit()`, `abort()`)
2. **Возвратить код ошибки** (возвращаемое значение или глобальная переменная)
3. **Возвратить специальное значение** (NULL, -1, etc.)
4. **Вызвать функцию обработки ошибок**

```cpp
// Пример с кодами возврата
enum ErrorCode { SUCCESS = 0, INVALID_INPUT = -1, OUT_OF_MEMORY = -2 };

ErrorCode divide(double a, double b, double& result) {
    if (b == 0) {
        return INVALID_INPUT;
    }
    result = a / b;
    return SUCCESS;
}

// Использование:
double result;
ErrorCode status = divide(10, 0, result);
if (status != SUCCESS) {
    cout << "Error occurred: " << status << endl;
}
```

## 29. Исключения. Преимущества использования исключений

**Исключения** - механизм обработки ошибок, который передает управление специальному обработчику.

```cpp
class DivisionByZeroError {
public:
    string message;
    DivisionByZeroError(const string& msg) : message(msg) {}
};

double divide(double a, double b) {
    if (b == 0) {
        throw DivisionByZeroError("Division by zero!");
    }
    return a / b;
}
```

**Преимущества:**
- **Разделение логики:** код обработки ошибок отделен от основной логики
- **Автоматическая очистка:** деструкторы вызываются автоматически при раскрутке стека
- **Невозможно игнорировать:** исключения нельзя случайно проигнорировать
- **Передача информации:** можно передать подробную информацию об ошибке

## 30. Обработка исключений. Иерархия исключений. Повторный запуск исключений

**Обработка исключений:**
```cpp
try {
    double result = divide(10, 0);
    cout << "Result: " << result << endl;
}
catch (const DivisionByZeroError& e) {
    cout << "Math error: " << e.message << endl;
}
catch (...) {  // Перехват любых исключений
    cout << "Unknown error occurred" << endl;
}
```

**Иерархия исключений:**
```cpp
class MathError {
public:
    virtual string what() const { return "Math error"; }
};

class DivisionByZero : public MathError {
public:
    string what() const override { return "Division by zero"; }
};

class Overflow : public MathError {
public:
    string what() const override { return "Overflow"; }
};

// Обработка:
try {
    // код, который может бросить исключение
}
catch (const DivisionByZero& e) {
    // обработка конкретного типа
}
catch (const MathError& e) {
    // обработка любых математических ошибок
}
```

**Повторный запуск исключений:**
```cpp
void processData() {
    try {
        // некоторые операции
        riskyOperation();
    }
    catch (const MathError& e) {
        // Логирование ошибки
        logError(e.what());
        
        // Повторный запуск того же исключения
        throw;  // передает исключение выше по стеку
    }
}

void mainFunction() {
    try {
        processData();
    }
    catch (const MathError& e) {
        cout << "Final handler: " << e.what() << endl;
    }
}
```

Исключения обеспечивают надежную и элегантную обработку ошибок, делая код более читаемым и менее подверженным ошибкам.

## 31. Исключения в конструкторах

Поскольку конструктор не возвращает значение, которое можно проверить, при ошибке в конструкторе используются исключения.

**Варианты обработки ошибок в конструкторе:**
- Возвратить объект в ненормальном состоянии
- Установить глобальную переменную об ошибке
- **Использовать исключения (рекомендуется)**

```cpp
class Vector {
    int* data;
    int size;
public:
    Vector(int sz) {
        if (sz <= 0) 
            throw std::invalid_argument("Size must be positive");
        data = new int[sz];
        size = sz;
    }
};
```

## 32. Использование конструкторов и деструкторов для выделения и освобождения ресурсов

Принцип RAII (Resource Acquisition Is Initialization) - ресурсы захватываются в конструкторе и освобождаются в деструкторе.

```cpp
class SafeFile {
    FILE* file;
public:
    SafeFile(const char* filename) {
        file = fopen(filename, "r");
        if (!file) throw std::runtime_error("Cannot open file");
    }
    
    ~SafeFile() {
        if (file) fclose(file);
    }
    
    int readInt() {
        int value;
        if (fscanf(file, "%d", &value) != 1)
            throw std::runtime_error("Read error");
        return value;
    }
};
```

## 33. Использование блока finally

В C++ нет блока `finally`, но есть в Java и C#. Блок `finally` выполняется всегда, независимо от того, было ли исключение.

**В Java:**
```java
try {
    // рискованный код
} catch (Exception e) {
    // обработка исключения
} finally {
    // всегда выполняется - освобождение ресурсов
}
```

**В Delphi:**
```pascal
try
    DoSomething();
finally 
    FreeResources(); 
end;
```

В C++ используются деструкторы вместо `finally`.

## 34. Понятие свойства. Отличие свойств от полей объекта

**Свойство** - механизм контролируемого доступа к данным через методы getter/setter.

**Отличия от полей:**
- При обращении к свойству вызываются методы
- Можно контролировать чтение/запись
- Можно выполнять дополнительные действия

**В Delphi:**
```pascal
property Name: string read GetName;  // только чтение
property Address: string read GetAddress write SetAddress;  // чтение и запись
```

**В C# (аналогично):**
```csharp
public string Name { get; private set; }
public string Address { get; set; }
```

## 35. Потоки. Вывод встроенных и пользовательских типов

**Поток** - источник или получатель последовательности байт для ввода-вывода.

```cpp
// Вывод встроенных типов
cout << "Number: " << 42 << endl;

// Для пользовательских типов определяем operator<<
class Complex {
    double re, im;
public:
    friend ostream& operator<<(ostream& os, const Complex& c) {
        return os << "(" << c.re << "+" << c.im << "i)";
    }
};

Complex c(1.0, 2.5);
cout << "Complex: " << c << endl;
```

## 36. Состояние потока. Форматирование. Использование манипуляторов

**Состояние потока:**
- `good()` - поток в порядке
- `eof()` - достигнут конец файла  
- `fail()` - операция неудачна
- `bad()` - поток испорчен

**Форматирование и манипуляторы:**
```cpp
cout << hex << 255 << endl;        // ff
cout << dec << 255 << endl;        // 255
cout << setprecision(2) << 3.14159 << endl;  // 3.14
cout << setw(10) << "hello" << endl;         // "     hello"
```

## 37. RTTI, возможности и область применения

**RTTI (Run-Time Type Information)** - информация о типах во время выполнения.

**Возможности:**
- Определение точного типа объекта
- Безопасное приведение типов
- Получение имени класса

```cpp
class Base { virtual ~Base() {} };
class Derived : public Base {};

Base* ptr = new Derived();

// Проверка типа
if (typeid(*ptr) == typeid(Derived)) {
    cout << "It's Derived" << endl;
}

// Безопасное приведение
Derived* d = dynamic_cast<Derived*>(ptr);
if (d) {
    cout << "Cast successful" << endl;
}

// Имя типа
cout << typeid(*ptr).name() << endl;
```

## 38. Событийно-ориентированное программирование

**Событийно-ориентированное программирование** - парадигма, где программа реагирует на события.

**Структура:**
```
while(true) {
    event = getEvent();
    handleEvent(event);
}
```

**Виды событий:**
- Пользовательские (клики, нажатия клавиш)
- Системные (таймеры, сообщения ОС)
- Программные (завершение операций)

**Обработчики событий** - функции, вызываемые при наступлении события.

**В Delphi:**
```pascal
property OnClick: TNotifyEvent read FOnClick write FOnClick;

// При клике:
if Assigned(FOnClick) then
    FOnClick(Self);
```

## 39. Модели, поддерживающие компонентное программирование

**Компонент** - независимый модуль для повторного использования.

**Основные модели:**

1. **COM (Component Object Model)**
   - Протокол для использования компонентов
   - Между процессами и компьютерами
   - Основа для ActiveX, OLE

2. **Microsoft .NET Framework**
   - Унифицированная интерфейсная часть
   - Независимые составляющие ПО
   - Многократное использование

3. **Java Beans**
   - Стандарт Sun Microsystems
   - Компоненты для Java

4. **CORBA**
   - Архитектура распределенных объектов

## 40. Этапы проектирования и развития программы

**Три основные стадии:**

1. **Анализ** - определение области задачи
2. **Проектирование** - создание структуры системы  
3. **Реализация** - программирование и тестирование

**Все стадии итеративны и включают:**
- Экспериментирование
- Тестирование
- Анализ и реализацию
- Документирование
- Сопровождение

**Принципы Страуструпа:**
- Четко понимать, что создаешь
- Разработка ПО - длительный процесс
- Системы стремятся к пределу сложности
- Эксперимент - необходимая часть разработки
- Проектирование и программирование итеративны

**Парадигма компонентного программирования:**
1. Создать общее описание проекта
2. Выделить стандартные компоненты
3. Подогнать компоненты под проект
4. Создать новые компоненты
5. Составить уточненное описание

**Шаги проектирования:**
- Определение классов
- Определение набора операций
- Указание зависимостей
- Определение интерфейсов
- Перестройка иерархии классов
