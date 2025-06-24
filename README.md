# Ответы на вопросы по системам программирования и ООП

## 1) Состав системы программирования. Интегрированная среда разработки. Проект, группа проектов

### Состав системы программирования

Система программирования представляет собой комплексный набор инструментов для разработки программного обеспечения на определенном языке программирования. Основные компоненты включают:

- **Интегрированная среда разработки (IDE)**
- **Компилятор или интерпретатор** - для преобразования исходного кода в исполняемую форму
- **Текстовый редактор** с поддержкой синтаксиса языка программирования
- **Библиотеки** стандартных функций и графические библиотеки
- **Отладочные программы (debugger)** для поиска и исправления ошибок
- **Система справки** и документация
- **Утилиты** для работы с проектами и файлами

### Интегрированная среда разработки (IDE)

IDE объединяет все необходимые инструменты в одной программе, обеспечивая весь цикл разработки. В отличие от использования отдельных утилит командной строки (например, vi + GCC + make), IDE предоставляет:

- Единый интерфейс для всех операций
- Многооконный режим работы
- Автоматизацию процессов сборки
- Интеграцию с системами контроля версий

Примеры популярных IDE: Visual Studio, Code::Blocks, CLion, Dev-C++.

### Проект и группа проектов

**Проект** - это логическая единица, содержащая набор исходных файлов, настроек компиляции и ресурсов для создания одного исполняемого файла или библиотеки.

**Группа проектов (Solution)** объединяет несколько связанных проектов и обеспечивает:
- Совместный доступ к исходному коду всех проектов
- Использование общих библиотек и настроек
- Управление зависимостями между проектами
- Автоматическую перекомпиляцию при изменениях
- Возможность отладки всей группы проектов

```cpp
// Пример структуры группы проектов:
// Solution "MyApplication"
//   ├── Project "MathLibrary" (статическая библиотека)
//   ├── Project "MainApp" (исполняемый файл)
//   └── Project "Tests" (тестирование)

// В проекте MathLibrary:
// math_utils.h
#ifndef MATH_UTILS_H
#define MATH_UTILS_H

class Calculator {
public:
    static int add(int a, int b);
    static int multiply(int a, int b);
};

#endif

// math_utils.cpp
#include "math_utils.h"

int Calculator::add(int a, int b) {
    return a + b;
}

int Calculator::multiply(int a, int b) {
    return a * b;
}

// В проекте MainApp:
// main.cpp
#include <iostream>
#include "../MathLibrary/math_utils.h"

int main() {
    int result = Calculator::add(5, 3);
    std::cout << "5 + 3 = " << result << std::endl;
    return 0;
}
```

## 2) Текстовый редактор: специальные функции для поддержки программирования

Текстовые редакторы в системах программирования обладают расширенной функциональностью для работы с кодом:

### Основные функции поддержки программирования:

1. **Подсветка синтаксиса (Syntax Highlighting)**
   - Цветовое выделение ключевых слов, строк, комментариев
   - Различные цвета для типов данных, функций, переменных

2. **Автодополнение кода (IntelliSense/Code Completion)**
   - Предложение вариантов завершения идентификаторов
   - Показ параметров функций и методов

3. **Автоматическое форматирование**
   - Выравнивание отступов
   - Автоматическая расстановка скобок

4. **Навигация по коду**
   - Переход к определению функции/переменной
   - Поиск всех использований символа
   - Структурное представление кода (outline)

5. **Рефакторинг**
   - Переименование переменных/функций
   - Извлечение методов
   - Реорганизация кода

6. **Проверка ошибок на лету**
   - Подчеркивание синтаксических ошибок
   - Предупреждения о потенциальных проблемах

```cpp
// Пример использования возможностей редактора:
#include <iostream>
#include <vector>

class DataProcessor {
private:
    std::vector<int> data;
    
public:
    // IDE подсвечивает ключевые слова синим,
    // типы данных - зеленым, строки - красным
    void addData(int value) {
        data.push_back(value); // Автодополнение предложит методы vector
    }
    
    // При наведении на функцию IDE покажет её сигнатуру
    double calculateAverage() const {
        if (data.empty()) return 0.0;
        
        int sum = 0;
        // IDE может предупредить о неиспользуемых переменных
        for (const auto& item : data) { // Автоформатирование отступов
            sum += item;
        }
        
        return static_cast<double>(sum) / data.size();
    }
};
```

## 3) Преимущества и недостатки компиляторов и интерпретаторов

### Компилируемые языки (C++, C, Pascal, Delphi)

**Преимущества:**
- **Высокая скорость выполнения** - код преобразован в машинные инструкции
- **Оптимизация кода** - компилятор может применять различные оптимизации
- **Независимость от среды выполнения** - программа может работать без дополнительного ПО
- **Защищенность кода** - исходный код недоступен в исполняемом файле
- **Меньшее потребление памяти** во время выполнения

**Недостатки:**
- **Длительный цикл разработки** - необходимость перекомпиляции при каждом изменении
- **Платформозависимость** - нужна отдельная компиляция для каждой архитектуры
- **Сложность отладки** - труднее отслеживать выполнение на уровне исходного кода

### Интерпретируемые языки (JavaScript, Python, BASIC)

**Преимущества:**
- **Кроссплатформенность** - один код работает на разных системах при наличии интерпретатора
- **Быстрый цикл разработки** - изменения видны сразу без перекомпиляции
- **Упрощенная отладка** - пошаговое выполнение по исходному коду
- **Динамические возможности** - изменение кода во время выполнения
- **Лучшая диагностика ошибок** с указанием на конкретные строки кода

**Недостатки:**
- **Низкая скорость выполнения** - интерпретация команд требует времени
- **Большое потребление памяти** - нужна память для интерпретатора и промежуточного представления
- **Зависимость от интерпретатора** - программа не может работать без него
- **Отсутствие оптимизации** - код выполняется "как есть"

### Промежуточные решения (Java, C#)

Используют компиляцию в промежуточный код (bytecode, IL), который затем интерпретируется или компилируется "на лету" (JIT-компиляция), сочетая преимущества обоих подходов.

```cpp
// Пример C++ кода, демонстрирующего преимущества компиляции:
#include <iostream>
#include <chrono>
#include <vector>

int main() {
    auto start = std::chrono::high_resolution_clock::now();
    
    // Высокоскоростные вычисления, оптимизированные компилятором
    std::vector<int> numbers(1000000);
    for (int i = 0; i < 1000000; ++i) {
        numbers[i] = i * i + 2 * i + 1; // Компилятор может оптимизировать это выражение
    }
    
    auto end = std::chrono::high_resolution_clock::now();
    auto duration = std::chrono::duration_cast<std::chrono::milliseconds>(end - start);
    
    std::cout << "Время выполнения: " << duration.count() << " мс" << std::endl;
    
    return 0;
}
```

## 4) Редактор связей: назначение и принцип работы. PE формат: применение, секции и их предназначение. Использование и создание библиотек

### Редактор связей (Linker)

**Назначение:** Редактор связей объединяет один или несколько объектных модулей (.obj, .o файлы) в единый исполняемый файл (.exe) или библиотеку (.dll, .lib).

**Принцип работы:**
1. **Анализ таблиц имен** в каждом объектном модуле
2. **Разрешение ссылок** - связывание неопределенных имен с их определениями
3. **Размещение кода и данных** в памяти
4. **Создание исполняемого файла** с корректными адресами

### Таблицы импорта и экспорта

```cpp
// Модуль 1 (main.cpp)
#include <iostream>

// Объявляем внешние функции и переменные
extern int global_counter;     // Импортируемая переменная
extern int calculate_sum(int a, int b);  // Импортируемая функция

// Функция, которую мы экспортируем
int display_result(int value) {
    std::cout << "Результат: " << value << std::endl;
    return value;
}

int main() {
    global_counter = 10;
    int result = calculate_sum(5, 3);
    display_result(result);
    return 0;
}

// После компиляции модуль 1 будет:
// Экспортировать: display_result, main
// Импортировать: global_counter, calculate_sum

// Модуль 2 (math_module.cpp)
int global_counter = 0;  // Определяем переменную

int calculate_sum(int a, int b) {  // Определяем функцию
    global_counter++;
    return a + b;
}

// После компиляции модуль 2 будет:
// Экспортировать: global_counter, calculate_sum
// Импортировать: (ничего)
```

### PE (Portable Executable) формат

**Применение:** PE формат используется в Windows для:
- Исполняемых файлов (.exe)
- Динамических библиотек (.dll)
- Объектных файлов (.obj)
- Системных драйверов (.sys)
- Файлов .NET сборок

**Основные секции PE файла:**

1. **.text** - содержит исполняемый код программы
2. **.data** - инициализированные глобальные переменные
3. **.bss** - неинициализированные данные
4. **.rdata** - константы только для чтения
5. **IAT (Import Address Table)** - таблица адресов импортируемых функций
6. **EAT (Export Address Table)** - таблица экспортируемых функций
7. **.IL** - промежуточный код .NET (в управляемых сборках)

### Работа с библиотеками

**Статические библиотеки (.lib):**
```cpp
// Создание статической библиотеки
// mymath.h
#ifndef MYMATH_H
#define MYMATH_H

namespace MyMath {
    double power(double base, int exponent);
    double factorial(int n);
}

#endif

// mymath.cpp
#include "mymath.h"

double MyMath::power(double base, int exponent) {
    double result = 1.0;
    for (int i = 0; i < exponent; ++i) {
        result *= base;
    }
    return result;
}

double MyMath::factorial(int n) {
    if (n <= 1) return 1.0;
    return n * factorial(n - 1);
}

// Компиляция в статическую библиотеку:
// g++ -c mymath.cpp -o mymath.o
// ar rcs libmymath.a mymath.o

// Использование статической библиотеки:
// main.cpp
#include <iostream>
#include "mymath.h"

int main() {
    double result = MyMath::power(2.0, 8);
    std::cout << "2^8 = " << result << std::endl;
    return 0;
}

// Линковка: g++ main.cpp -L. -lmymath -o main.exe
```

**Динамические библиотеки (.dll):**
```cpp
// Создание DLL
// mathlib.h
#ifdef MATHLIB_EXPORTS
#define MATHLIB_API __declspec(dllexport)
#else
#define MATHLIB_API __declspec(dllimport)
#endif

extern "C" {
    MATHLIB_API int add_numbers(int a, int b);
    MATHLIB_API int multiply_numbers(int a, int b);
}

// mathlib.cpp
#define MATHLIB_EXPORTS
#include "mathlib.h"

extern "C" {
    MATHLIB_API int add_numbers(int a, int b) {
        return a + b;
    }
    
    MATHLIB_API int multiply_numbers(int a, int b) {
        return a * b;
    }
}

// Динамическая загрузка DLL:
#include <windows.h>
#include <iostream>

typedef int (*AddFunc)(int, int);
typedef int (*MultiplyFunc)(int, int);

int main() {
    HMODULE hLib = LoadLibrary(L"mathlib.dll");
    if (hLib == NULL) {
        std::cout << "Не удалось загрузить библиотеку" << std::endl;
        return 1;
    }
    
    AddFunc add = (AddFunc)GetProcAddress(hLib, "add_numbers");
    MultiplyFunc multiply = (MultiplyFunc)GetProcAddress(hLib, "multiply_numbers");
    
    if (add && multiply) {
        int sum = add(10, 20);
        int product = multiply(5, 6);
        std::cout << "10 + 20 = " << sum << std::endl;
        std::cout << "5 * 6 = " << product << std::endl;
    }
    
    FreeLibrary(hLib);
    return 0;
}
```

## 5) Отладчик: управление выполнением программы, точки останова, окна

### Управление выполнением программы

Отладчик предоставляет следующие команды для контроля выполнения:

1. **Run (F5)** - запуск программы до следующей точки останова
2. **Step Over (F10)** - выполнение текущей строки, без входа в функции
3. **Step Into (F11)** - выполнение с входом в вызываемые функции  
4. **Step Out (Shift+F11)** - выход из текущей функции
5. **Run to Cursor** - выполнение до позиции курсора
6. **Stop/Restart** - остановка и перезапуск программы

### Точки останова (Breakpoints)

Точки останова позволяют остановить выполнение программы при определенных условиях:

**Типы условий:**
- **По позиции** - остановка на определенной строке кода
- **По условию** - когда логическое выражение становится истинным
- **По изменению** - когда переменная меняет значение
- **По доступу к памяти** - при чтении/записи в определенный адрес
- **По счетчику** - на N-ом проходе через точку

**Действия точек останова:**
- Остановка выполнения
- Вывод сообщения в лог
- Вычисление и вывод выражения
- Выполнение макроса
- Управление другими точками останова

```cpp
#include <iostream>
#include <vector>

void process_array(std::vector<int>& arr) {
    for (size_t i = 0; i < arr.size(); ++i) {
        // Точка останова здесь с условием: i == 5
        arr[i] = arr[i] * 2;
        
        // Точка останова с действием: печать значения arr[i]
        if (arr[i] > 100) {
            // Условная точка останова: arr[i] > 100
            std::cout << "Большое значение: " << arr[i] << std::endl;
        }
    }
}

int main() {
    std::vector<int> numbers = {1, 5, 10, 25, 50, 75, 100, 125};
    
    // Точка останова здесь для начала отладки
    process_array(numbers);
    
    for (const auto& num : numbers) {
        std::cout << num << " ";
    }
    std::cout << std::endl;
    
    return 0;
}
```

### Окна отладчика

**1. Call Stack (Стек вызовов)**
- Показывает последовательность вызовов функций
- Позволяет переходить между уровнями вызовов
- Отображает параметры функций

**2. Variables/Watches (Переменные и наблюдения)**
- **Locals** - локальные переменные текущей функции
- **Autos** - автоматически определяемые релевантные переменные  
- **Watches** - пользовательские выражения для наблюдения
- **Immediate** - окно для вычисления выражений на лету

**3. Registers (Регистры)**
- Содержимое регистров процессора
- Флаги состояния процессора

**4. Memory (Память)**
- Просмотр содержимого памяти по адресам
- Hex и ASCII представление

**5. Threads (Потоки)**
- Список всех потоков программы
- Переключение между потоками для отладки

**6. Processes (Процессы)**
- Список процессов для присоединения отладчика
- Информация о загруженных модулях

```cpp
#include <iostream>
#include <thread>
#include <vector>
#include <mutex>

std::mutex mtx;
int shared_counter = 0;

void worker_thread(int thread_id) {
    for (int i = 0; i < 5; ++i) {
        {
            std::lock_guard<std::mutex> lock(mtx);
            // Точка останова здесь для отладки многопоточности
            shared_counter++;
            std::cout << "Thread " << thread_id 
                      << " increment: " << shared_counter << std::endl;
        }
        std::this_thread::sleep_for(std::chrono::milliseconds(100));
    }
}

int main() {
    std::vector<std::thread> threads;
    
    // Создаем несколько потоков
    for (int i = 0; i < 3; ++i) {
        // Точка останова для отслеживания создания потоков
        threads.emplace_back(worker_thread, i + 1);
    }
    
    // Ожидаем завершения всех потоков
    for (auto& t : threads) {
        t.join();
    }
    
    std::cout << "Итоговое значение счетчика: " << shared_counter << std::endl;
    return 0;
}
```

### Практические советы по отладке

1. **Используйте логические точки останова** для отслеживания изменений состояния
2. **Watch-выражения** помогают следить за сложными объектами
3. **Call Stack** незаменим для понимания потока выполнения
4. **Step Into/Over** позволяют контролировать детализацию отладки
5. **Conditional breakpoints** экономят время при отладке циклов

Современные отладчики также предоставляют возможности:
- Визуализации структур данных
- Профилирования производительности  
- Анализа утечек памяти
- Отладки на удаленных машинах
- Интеграции с системами контроля версий

## 6) Парадигма процедурного программирования

**Процедурное программирование** - это парадигма, основанная на концепции процедур (функций), которые выполняют операции над данными. Программа представляет собой последовательность вызовов процедур.

### Основные принципы:

1. **Модульность** - разбиение программы на отдельные процедуры
2. **Структурированность** - использование управляющих конструкций (if, while, for)
3. **Разделение данных и операций** - данные и функции существуют отдельно
4. **Нисходящее проектирование** - декомпозиция сложной задачи на простые

### Преимущества:
- Простота понимания и реализации
- Естественное отражение алгоритмического подхода
- Легкость отладки и тестирования отдельных процедур
- Возможность повторного использования процедур

### Недостатки:
- Сложность сопровождения больших программ
- Слабая защищенность данных
- Трудности при модификации структур данных

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

// Процедурный подход для работы с массивом студентов
struct Student {
    std::string name;
    int age;
    double gpa;
};

// Процедуры для работы с данными
void initStudent(Student& student, const std::string& name, int age, double gpa) {
    student.name = name;
    student.age = age;
    student.gpa = gpa;
}

void printStudent(const Student& student) {
    std::cout << "Имя: " << student.name 
              << ", Возраст: " << student.age 
              << ", Средний балл: " << student.gpa << std::endl;
}

double calculateAverageGPA(const std::vector<Student>& students) {
    if (students.empty()) return 0.0;
    
    double sum = 0.0;
    for (const auto& student : students) {
        sum += student.gpa;
    }
    return sum / students.size();
}

void sortStudentsByGPA(std::vector<Student>& students) {
    std::sort(students.begin(), students.end(), 
              [](const Student& a, const Student& b) {
                  return a.gpa > b.gpa;
              });
}

void printAllStudents(const std::vector<Student>& students) {
    for (const auto& student : students) {
        printStudent(student);
    }
}

// Главная процедура
int main() {
    std::vector<Student> students(3);
    
    // Инициализация данных через процедуры
    initStudent(students[0], "Иван", 20, 4.5);
    initStudent(students[1], "Мария", 19, 4.8);
    initStudent(students[2], "Петр", 21, 3.9);
    
    std::cout << "Исходный список студентов:" << std::endl;
    printAllStudents(students);
    
    std::cout << "\nСредний балл группы: " << calculateAverageGPA(students) << std::endl;
    
    sortStudentsByGPA(students);
    std::cout << "\nСтуденты, отсортированные по среднему баллу:" << std::endl;
    printAllStudents(students);
    
    return 0;
}
```

## 7) Парадигма модульного программирования

**Модульное программирование** развивает процедурный подход, организуя код в отдельные модули (файлы) с четко определенными интерфейсами.

### Основные принципы:

1. **Инкапсуляция на уровне модуля** - скрытие внутренней реализации
2. **Четкие интерфейсы** - определение того, что доступно извне
3. **Слабая связанность** между модулями
4. **Сильная связность** внутри модуля
5. **Повторное использование** модулей

### Преимущества:
- Улучшенная организация кода
- Возможность раздельной компиляции
- Упрощение командной разработки
- Лучшая поддерживаемость

### Недостатки:
- Сложность управления зависимостями
- Необходимость продумывания интерфейсов
- Потенциальные проблемы с глобальными данными

```cpp
// math_operations.h - интерфейс модуля
#ifndef MATH_OPERATIONS_H
#define MATH_OPERATIONS_H

#include <vector>

namespace MathOperations {
    // Публичный интерфейс модуля
    double calculateMean(const std::vector<double>& data);
    double calculateStandardDeviation(const std::vector<double>& data);
    std::vector<double> normalizeData(const std::vector<double>& data);
    
    // Статистические функции
    double findMin(const std::vector<double>& data);
    double findMax(const std::vector<double>& data);
}

#endif

// math_operations.cpp - реализация модуля
#include "math_operations.h"
#include <algorithm>
#include <cmath>
#include <stdexcept>

namespace MathOperations {
    // Приватная (внутренняя) функция модуля
    static bool isValidData(const std::vector<double>& data) {
        return !data.empty();
    }
    
    double calculateMean(const std::vector<double>& data) {
        if (!isValidData(data)) {
            throw std::invalid_argument("Пустой вектор данных");
        }
        
        double sum = 0.0;
        for (double value : data) {
            sum += value;
        }
        return sum / data.size();
    }
    
    double calculateStandardDeviation(const std::vector<double>& data) {
        if (!isValidData(data)) {
            throw std::invalid_argument("Пустой вектор данных");
        }
        
        double mean = calculateMean(data);
        double sum = 0.0;
        
        for (double value : data) {
            sum += (value - mean) * (value - mean);
        }
        
        return std::sqrt(sum / data.size());
    }
    
    std::vector<double> normalizeData(const std::vector<double>& data) {
        double mean = calculateMean(data);
        double stdDev = calculateStandardDeviation(data);
        
        std::vector<double> normalized;
        normalized.reserve(data.size());
        
        for (double value : data) {
            normalized.push_back((value - mean) / stdDev);
        }
        
        return normalized;
    }
    
    double findMin(const std::vector<double>& data) {
        if (!isValidData(data)) {
            throw std::invalid_argument("Пустой вектор данных");
        }
        return *std::min_element(data.begin(), data.end());
    }
    
    double findMax(const std::vector<double>& data) {
        if (!isValidData(data)) {
            throw std::invalid_argument("Пустой вектор данных");
        }
        return *std::max_element(data.begin(), data.end());
    }
}

// main.cpp - использование модуля
#include <iostream>
#include "math_operations.h"

int main() {
    std::vector<double> data = {1.2, 2.5, 3.8, 1.9, 4.1, 2.7, 3.3, 2.1};
    
    try {
        std::cout << "Исходные данные: ";
        for (double value : data) {
            std::cout << value << " ";
        }
        std::cout << std::endl;
        
        // Использование функций модуля
        std::cout << "Среднее значение: " << MathOperations::calculateMean(data) << std::endl;
        std::cout << "Стандартное отклонение: " << MathOperations::calculateStandardDeviation(data) << std::endl;
        std::cout << "Минимум: " << MathOperations::findMin(data) << std::endl;
        std::cout << "Максимум: " << MathOperations::findMax(data) << std::endl;
        
        auto normalized = MathOperations::normalizeData(data);
        std::cout << "Нормализованные данные: ";
        for (double value : normalized) {
            std::cout << value << " ";
        }
        std::cout << std::endl;
        
    } catch (const std::exception& e) {
        std::cerr << "Ошибка: " << e.what() << std::endl;
    }
    
    return 0;
}
```

## 8) Парадигма абстракции данных

**Абстракция данных** - это парадигма, при которой тип данных определяется через множество операций, которые можно над ним выполнять, скрывая детали внутреннего представления.

### Основные принципы:

1. **Инкапсуляция данных** - сокрытие внутреннего представления
2. **Интерфейс операций** - определение допустимых операций
3. **Инвариантность** - поддержание корректного состояния
4. **Абстрактные типы данных (АТД)** - описание поведения без реализации

### Преимущества:
- Надежность - невозможность некорректного изменения данных
- Гибкость - возможность изменения реализации без изменения интерфейса
- Модульность - четкое разделение интерфейса и реализации
- Возможность создания библиотек

### Недостатки:
- Потенциальные проблемы с производительностью
- Сложность проектирования интерфейса
- Ограниченная расширяемость

```cpp
#include <iostream>
#include <vector>
#include <stdexcept>

// Абстрактный тип данных: Стек
class Stack {
private:
    // Скрытое представление данных
    std::vector<int> data;
    static const size_t MAX_SIZE = 100;
    
    // Приватные методы для поддержания инвариантов
    bool isFull() const {
        return data.size() >= MAX_SIZE;
    }
    
    bool isEmpty() const {
        return data.empty();
    }
    
public:
    // Публичный интерфейс - операции над АТД
    
    // Конструктор - создание пустого стека
    Stack() {
        data.reserve(MAX_SIZE);
    }
    
    // Добавление элемента на вершину стека
    void push(int value) {
        if (isFull()) {
            throw std::overflow_error("Стек переполнен");
        }
        data.push_back(value);
    }
    
    // Удаление и возврат элемента с вершины стека
    int pop() {
        if (isEmpty()) {
            throw std::underflow_error("Стек пуст");
        }
        int value = data.back();
        data.pop_back();
        return value;
    }
    
    // Просмотр элемента на вершине без удаления
    int top() const {
        if (isEmpty()) {
            throw std::underflow_error("Стек пуст");
        }
        return data.back();
    }
    
    // Проверка состояния стека
    size_t size() const {
        return data.size();
    }
    
    bool empty() const {
        return isEmpty();
    }
    
    bool full() const {
        return isFull();
    }
    
    // Очистка стека
    void clear() {
        data.clear();
    }
    
    // Вывод содержимого стека (для демонстрации)
    void print() const {
        std::cout << "Стек (снизу вверх): ";
        for (size_t i = 0; i < data.size(); ++i) {
            std::cout << data[i] << " ";
        }
        std::cout << "<- вершина" << std::endl;
    }
};

// Пример использования АТД
int main() {
    Stack myStack;
    
    try {
        // Демонстрация операций со стеком
        std::cout << "Добавляем элементы в стек:" << std::endl;
        for (int i = 1; i <= 5; ++i) {
            myStack.push(i * 10);
            std::cout << "Добавлен элемент " << (i * 10) << std::endl;
            myStack.print();
        }
        
        std::cout << "\nРазмер стека: " << myStack.size() << std::endl;
        std::cout << "Элемент на вершине: " << myStack.top() << std::endl;
        
        std::cout << "\nИзвлекаем элементы из стека:" << std::endl;
        while (!myStack.empty()) {
            int value = myStack.pop();
            std::cout << "Извлечен элемент " << value << std::endl;
            if (!myStack.empty()) {
                myStack.print();
            }
        }
        
        std::cout << "\nСтек пуст. Размер: " << myStack.size() << std::endl;
        
        // Попытка извлечения из пустого стека
        std::cout << "\nПопытка извлечения из пустого стека:" << std::endl;
        myStack.pop(); // Это вызовет исключение
        
    } catch (const std::exception& e) {
        std::cerr << "Ошибка: " << e.what() << std::endl;
    }
    
    return 0;
}

// Альтернативная реализация стека с другим внутренним представлением
class LinkedStack {
private:
    struct Node {
        int data;
        Node* next;
        Node(int value, Node* nextNode = nullptr) : data(value), next(nextNode) {}
    };
    
    Node* topNode;
    size_t stackSize;
    
public:
    LinkedStack() : topNode(nullptr), stackSize(0) {}
    
    ~LinkedStack() {
        clear();
    }
    
    void push(int value) {
        topNode = new Node(value, topNode);
        stackSize++;
    }
    
    int pop() {
        if (empty()) {
            throw std::underflow_error("Стек пуст");
        }
        
        Node* oldTop = topNode;
        int value = oldTop->data;
        topNode = oldTop->next;
        delete oldTop;
        stackSize--;
        
        return value;
    }
    
    int top() const {
        if (empty()) {
            throw std::underflow_error("Стек пуст");
        }
        return topNode->data;
    }
    
    bool empty() const {
        return topNode == nullptr;
    }
    
    size_t size() const {
        return stackSize;
    }
    
    void clear() {
        while (!empty()) {
            pop();
        }
    }
};
```

## 9) ООП: класс, инкапсуляция

**Класс** - это пользовательский тип данных, объединяющий данные (поля) и операции над ними (методы). Класс служит шаблоном для создания объектов.

**Инкапсуляция** - это принцип ООП, предполагающий сокрытие внутреннего устройства класса и предоставление контролируемого доступа к его функциональности через публичный интерфейс.

### Уровни доступа в C++:

1. **private** - доступ только внутри класса
2. **protected** - доступ внутри класса и его наследников
3. **public** - доступ откуда угодно

### Преимущества инкапсуляции:
- Защита данных от некорректного использования
- Возможность изменения внутренней реализации без изменения интерфейса
- Контроль над состоянием объекта
- Упрощение использования класса

```cpp
#include <iostream>
#include <string>
#include <stdexcept>

// Пример класса с полной инкапсуляцией
class BankAccount {
private:
    // Скрытые данные (инкапсулированы)
    std::string accountNumber;
    std::string ownerName;
    double balance;
    double interestRate;
    
    // Приватные методы для внутренней логики
    bool isValidAmount(double amount) const {
        return amount > 0;
    }
    
    void logTransaction(const std::string& operation, double amount) const {
        std::cout << "[Лог] " << operation << " на сумму " << amount 
                  << " для счета " << accountNumber << std::endl;
    }

protected:
    // Защищенные методы для наследников
    virtual void updateInterest() {
        balance += balance * interestRate / 100;
    }

public:
    // Публичный интерфейс класса
    
    // Конструктор
    BankAccount(const std::string& accNum, const std::string& owner, 
                double initialBalance = 0.0, double rate = 1.5) 
        : accountNumber(accNum), ownerName(owner), balance(initialBalance), interestRate(rate) {
        
        if (initialBalance < 0) {
            throw std::invalid_argument("Начальный баланс не может быть отрицательным");
        }
    }
    
    // Методы доступа (геттеры)
    std::string getAccountNumber() const { return accountNumber; }
    std::string getOwnerName() const { return ownerName; }
    double getBalance() const { return balance; }
    double getInterestRate() const { return interestRate; }
    
    // Методы изменения (сеттеры) с контролем
    void setInterestRate(double rate) {
        if (rate >= 0 && rate <= 100) {
            interestRate = rate;
        } else {
            throw std::invalid_argument("Процентная ставка должна быть от 0 до 100");
        }
    }
    
    // Основные операции счета
    virtual void deposit(double amount) {
        if (!isValidAmount(amount)) {
            throw std::invalid_argument("Сумма депозита должна быть положительной");
        }
        
        balance += amount;
        logTransaction("Депозит", amount);
        std::cout << "Депозит успешен. Новый баланс: " << balance << std::endl;
    }
    
    virtual bool withdraw(double amount) {
        if (!isValidAmount(amount)) {
            throw std::invalid_argument("Сумма снятия должна быть положительной");
        }
        
        if (amount > balance) {
            std::cout << "Недостаточно средств для снятия " << amount << std::endl;
            return false;
        }
        
        balance -= amount;
        logTransaction("Снятие", amount);
        std::cout << "Снятие успешно. Новый баланс: " << balance << std::endl;
        return true;
    }
    
    virtual void applyInterest() {
        double oldBalance = balance;
        updateInterest();
        std::cout << "Проценты начислены. Баланс увеличился с " 
                  << oldBalance << " до " << balance << std::endl;
    }
    
    // Перегрузка операторов для удобства использования
    BankAccount& operator+=(double amount) {
        deposit(amount);
        return *this;
    }
    
    BankAccount& operator-=(double amount) {
        withdraw(amount);
        return *this;
    }
    
    // Виртуальный деструктор для корректного наследования
    virtual ~BankAccount() = default;
    
    // Дружественная функция для доступа к приватным данным
    friend std::ostream& operator<<(std::ostream& os, const BankAccount& account);
};

// Реализация дружественной функции
std::ostream& operator<<(std::ostream& os, const BankAccount& account) {
    os << "Счет: " << account.accountNumber 
       << ", Владелец: " << account.ownerName 
       << ", Баланс: " << account.balance 
       << ", Ставка: " << account.interestRate << "%";
    return os;
}

// Пример нарушения инкапсуляции через struct (по умолчанию все public)
struct UnsafeAccount {
    std::string accountNumber;  // Публичный доступ к данным
    double balance;             // Можно изменить напрямую!
    
    void deposit(double amount) { balance += amount; }
    void withdraw(double amount) { balance -= amount; } // Без проверок!
};

int main() {
    try {
        // Использование правильно инкапсулированного класса
        BankAccount account("12345", "Иван Иванов", 1000.0, 2.0);
        
        std::cout << "Информация о счете:" << std::endl;
        std::cout << account << std::endl << std::endl;
        
        // Контролируемые операции через публичный интерфейс
        account.deposit(500.0);
        account.withdraw(200.0);
        account.applyInterest();
        
        std::cout << "\nИтоговое состояние:" << std::endl;
        std::cout << account << std::endl;
        
        // Использование перегруженных операторов
        account += 100.0;  // Эквивалентно account.deposit(100.0)
        account -= 50.0;   // Эквивалентно account.withdraw(50.0)
        
        std::cout << "\nПосле операций с перегруженными операторами:" << std::endl;
        std::cout << "Баланс: " << account.getBalance() << std::endl;
        
        // Попытка некорректных операций
        std::cout << "\nПопытка некорректных операций:" << std::endl;
        account.withdraw(10000.0);  // Недостаточно средств
        
        // account.balance = -1000; // ОШИБКА КОМПИЛЯЦИИ - приватное поле
        
    } catch (const std::exception& e) {
        std::cerr << "Ошибка: " << e.what() << std::endl;
    }
    
    // Демонстрация проблем с нарушением инкапсуляции
    std::cout << "\n--- Пример нарушения инкапсуляции ---" << std::endl;
    UnsafeAccount unsafe;
    unsafe.accountNumber = "UNSAFE";
    unsafe.balance = 1000.0;
    
    // Прямое изменение данных без контроля
    unsafe.balance = -500.0;  // Отрицательный баланс!
    unsafe.withdraw(1000.0);  // Уйдем еще глубже в минус
    
    std::cout << "Небезопасный счет: баланс = " << unsafe.balance << std::endl;
    std::cout << "Проблема: нет контроля над состоянием объекта!" << std::endl;
    
    return 0;
}
```

## 10) ООП: наследование

**Наследование** - это механизм ООП, позволяющий создавать новые классы на основе существующих, наследуя их свойства и методы, и при необходимости дополняя или изменяя их.

### Типы наследования в C++:

1. **public наследование** - is-a relationship (отношение "является")
2. **protected наследование** - ограниченный доступ
3. **private наследование** - has-a relationship (отношение "содержит")

### Преимущества наследования:
- Повторное использование кода
- Создание иерархий классов
- Полиморфизм
- Расширяемость системы

### Недостатки:
- Увеличение сложности
- Тесная связанность классов
- Потенциальные проблемы с множественным наследованием

```cpp
#include <iostream>
#include <string>
#include <vector>
#include <memory>

// Базовый класс - общие свойства всех сотрудников
class Employee {
protected:
    std::string name;
    int id;
    std::string department;
    double baseSalary;
    
public:
    Employee(const std::string& empName, int empId, 
             const std::string& dept, double salary)
        : name(empName), id(empId), department(dept), baseSalary(salary) {}
    
    // Виртуальные методы для переопределения в наследниках
    virtual double calculateSalary() const {
        return baseSalary;
    }
    
    virtual void displayInfo() const {
        std::cout << "ID: " << id << ", Имя: " << name 
                  << ", Отдел: " << department 
                  << ", Базовая зарплата: " << baseSalary << std::endl;
    }
    
    virtual std::string getPosition() const {
        return "Сотрудник";
    }
    
    // Геттеры
    std::string getName() const { return name; }
    int getId() const { return id; }
    std::string getDepartment() const { return department; }
    
    // Виртуальный деструктор для корректного полиморфного удаления
    virtual ~Employee() = default;
};

// Производный класс - обычный сотрудник
class RegularEmployee : public Employee {
private:
    double bonus;
    
public:
    RegularEmployee(const std::string& name, int id, 
                   const std::string& dept, double salary, double empBonus = 0.0)
        : Employee(name, id, dept, salary), bonus(empBonus) {}
    
    // Переопределение метода расчета зарплаты
    double calculateSalary() const override {
        return baseSalary + bonus;
    }
    
    void displayInfo() const override {
        Employee::displayInfo(); // Вызов метода базового класса
        std::cout << "Бонус: " << bonus << ", Итого к выплате: " 
                  << calculateSalary() << std::endl;
    }
    
    std::string getPosition() const override {
        return "Обычный сотрудник";
    }
    
    void setBonus(double newBonus) { bonus = newBonus; }
    double getBonus() const { return bonus; }
};

// Производный класс - менеджер
class Manager : public Employee {
private:
    std::vector<std::shared_ptr<Employee>> subordinates;
    double managementBonus;
    
public:
    Manager(const std::string& name, int id, 
            const std::string& dept, double salary, double mgmtBonus = 0.0)
        : Employee(name, id, dept, salary), managementBonus(mgmtBonus) {}
    
    double calculateSalary() const override {
        // Зарплата = базовая + бонус за управление + бонус за количество подчиненных
        return baseSalary + managementBonus + (subordinates.size() * 500.0);
    }
    
    void displayInfo() const override {
        Employee::displayInfo();
        std::cout << "Бонус за управление: " << managementBonus 
                  << ", Количество подчиненных: " << subordinates.size()
                  << ", Итого к выплате: " << calculateSalary() << std::endl;
    }
    
    std::string getPosition() const override {
        return "Менеджер";
    }
    
    // Специфические методы менеджера
    void addSubordinate(std::shared_ptr<Employee> employee) {
        subordinates.push_back(employee);
        std::cout << "Добавлен подчиненный: " << employee->getName() << std::endl;
    }
    
    void removeSubordinate(int employeeId) {
        auto it = std::remove_if(subordinates.begin(), subordinates.end(),
            [employeeId](const std::shared_ptr<Employee>& emp) {
                return emp->getId() == employeeId;
            });
        
        if (it != subordinates.end()) {
            std::cout << "Удален подчиненный: " << (*it)->getName() << std::endl;
            subordinates.erase(it, subordinates.end());
        }
    }
    
    void listSubordinates() const {
        std::cout << "Подчиненные менеджера " << name << ":" << std::endl;
        for (const auto& emp : subordinates) {
            std::cout << "  - " << emp->getName() << " (" << emp->getPosition() << ")" << std::endl;
        }
    }
};

// Еще один производный класс - разработчик
class Developer : public
