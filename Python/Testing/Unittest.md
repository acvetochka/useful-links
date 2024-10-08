# Модульне тестування (Unit Testing)
Модульне тестування — це підхід, за якого тестуються окремі частини (модулі) програмного забезпечення, щоб перевірити їх роботу ізольовано від інших компонентів. У Python модульне тестування зазвичай реалізується за допомогою вбудованої бібліотеки unittest, або бібліотек сторонніх розробників, таких як pytest.

Основні переваги модульного тестування:
- Швидке виявлення помилок на ранніх етапах.
- Легше підтримувати код і впроваджувати нові зміни.
- Підвищення якості та надійності коду.

## 1. Unittest
   
`unittest` — стандартна бібліотека Python для модульного тестування, подібна до бібліотек у інших мовах, таких як JUnit у Java чи NUnit у C#.
Простий приклад використання unittest:

```python
import unittest

def add(a, b):
    return a + b

class TestMathFunctions(unittest.TestCase):

    def test_add(self):
        self.assertEqual(add(1, 2), 3)
        self.assertEqual(add(-1, 1), 0)

if __name__ == '__main__':
    unittest.main()
```

Основні методи unittest:

`assertEqual(a, b)` — перевірка на рівність a та b.

`assertTrue(x)` — перевірка, що значення x є істинним.

`assertFalse(x)` — перевірка, що значення x є хибним.

`assertRaises(Exception, func, *args)` — перевірка, що функція func викликає виключення типу Exception.

Нижче наведено список часто використовуваних методів assert у класі TestCase. Для отримання додаткової інформації про кожен метод натисніть на вбудоване посилання у наведеному списку.   

- Метод `assertEqual(a, b)` перевіряє, що a == b
- Метод `assertNotEqual(a, b)` перевіряє, що a != b
- Метод `assertTrue(x)` перевіряє, що bool(x) рівний True
- Метод `assertFalse(x)` перевіряє, що bool(x) рівне False
- Метод `assertIs(a, b)` перевіряє, що a є b
- Метод `assertIsNot(a, b)` перевіряє, що a не є b
- Метод `assertIsNone(x)` перевіряє, що x рівний None
- Метод `assertIsNotNone(x)` перевіряє, що x не є None
- Метод `assertIn(a, b)` перевіряє, що a в b
- Метод `assertNotIn(a, b)` перевіряє, що a не входить в b
- Метод `assertIsInstance(a, b)` перевіряє, що isinstance(a, b)
- Метод `assertNotIsInstance(a, b)` перевіряє, що not isinstance(a),  

Ви також можете використовувати методи assert для генерування винятків, попереджень та повідомлень журналу. Наприклад, ще одним важливим методом assert у модульному тестуванні є assertRaises. Він дозволяє перевірити, чи згенеровані виключення, коли вони мають бути, гарантуючи, що ваша програма може обробляти помилки. assertRaises також дозволяє розробникам перевірити, який саме тип виключення згенеровано, гарантуючи правильну обробку помилок.

## 2. Інтерфейс командного рядка
   
Python надає можливість запуску модульних тестів через CLI (Command-Line Interface), що спрощує автоматизацію процесу тестування.

Інтерфейс командного рядка дозволяє взаємодіяти з додатком або програмою через командний рядок операційної системи, термінал або консоль, починаючи код з текстової команди. Коли ви хочете запустити тести в Python, ви можете використовувати модуль unittest з командного рядка для запуску тестів з модулів, класів або навіть окремих методів тестування. Це також дозволяє запускати кілька файлів одночасно.

Приклади запуску тестів з командного рядка:

2.1. Запуск тестів через unittest:

```bash
python -m unittest discover
```
Ця команда автоматично знаходить і запускає всі тести у поточній директорії.

   - Щоб викликати цілий модуль:
    
```bash
python -m unittest test_module1 test_module2 
```
  - Виклик тестового класу:
```bash
python -m unittest test_module.TestClass
```
  - Щоб викликати метод тесту:
```bash
python -m unittest test_module.TestClass.test_method
```
  - Тестові модулі також можна викликати за допомогою шляху до файлу, як описано нижче:
```
python -m unittest tests/test_something.py
```
[джерело](https://docs.python.org/3/library/unittest.html)


У кожному випадку структура команди залишається незмінною, а тестовий клас і тестовий метод додаються до оригінального модуля, який викликається.

Ви також можете використовувати командний рядок для виявлення тестів, для запуску всіх тестів в одному проекті або навіть для запуску лише підмножини тестів.


2.2. Запуск тестів через pytest:

```bash
pytest
```
Ця команда запускає всі тести, виявлені у файлах, що починаються з test_.

Для детальнішої інформації під час запуску тестів можна використовувати опції:

```bash
pytest -v   # Детальний вивід результатів тестування
```

## 3. Патерни проектування модульних тестів
У модульному тестуванні важливо дотримуватись певних шаблонів і принципів, щоб тестовий код був читабельним, підтримуваним та ефективним. Ось кілька ключових патернів:

a. AAA (Arrange-Act-Assert)

Це один із найпоширеніших патернів для організації тестів.

- Arrange (Підготовка): Налаштовуємо всі необхідні дані або об'єкти.
- Act (Дія): Викликаємо тестовану функцію або метод.
- Assert (Перевірка): Перевіряємо результат виконання функції.
Приклад:

```python
import unittest

def add(a, b):
    return a + b

class TestAddFunction(unittest.TestCase):
    
    def test_add(self):
        # Arrange
        a, b = 1, 2
        
        # Act
        result = add(a, b)
        
        # Assert
        self.assertEqual(result, 3)

if __name__ == '__main__':
    unittest.main()
```

b. Mocking (Мокація)

Mocking — це техніка, яка використовується для імітації поведінки об'єктів, функцій або методів. Її використовують для ізоляції тестів від зовнішніх залежностей, таких як база даних, файлові системи або API.

Python надає вбудований модуль unittest.mock для створення мок-об'єктів.

Приклад:

```python
from unittest.mock import patch

def get_data_from_db():
    # Імітуємо підключення до бази даних
    pass

@patch('module_name.get_data_from_db')
def test_function(mock_db):
    mock_db.return_value = {'name': 'John'}
    result = some_function()
    assert result == expected_output
```

c. First Test (Тест спочатку)

Ця методика полягає в тому, щоб спочатку написати тести для майбутнього функціоналу, який ще не реалізований. Це частина методології TDD (Test-Driven Development).

## 4. Набори тестів (Test Suites)
Методи setUp() і tearDown() у модульному тестуванні забезпечують підготовку та очищення тестового середовища перед і після кожного тесту. Це робить тестування більш організованим, особливо коли для виконання тестів потрібна певна ініціалізація, або, навпаки, необхідно звільнити ресурси після тесту.

4.1. Метод setUp()

Метод setUp() викликається перед кожним тестовим методом. Його використовують для налаштування початкових умов, таких як створення об'єктів, налаштування з'єднань із базою даних, відкриття файлів тощо.

Приклад:

```python
import unittest

class TestOperations(unittest.TestCase):
    
    def setUp(self):
        """Ініціалізація, що виконується перед кожним тестом"""
        self.num1 = 10
        self.num2 = 5
    
    def test_add(self):
        result = self.num1 + self.num2
        self.assertEqual(result, 15)
    
    def test_subtract(self):
        result = self.num1 - self.num2
        self.assertEqual(result, 5)

if __name__ == '__main__':
    unittest.main()
```
У цьому прикладі:

Метод setUp() ініціалізує змінні self.num1 і self.num2 перед виконанням кожного тесту. Таким чином, не потрібно дублювати код у кожному тестовому методі.

4.2. Метод tearDown()

Метод tearDown() викликається після кожного тесту для "очищення" середовища. Його використовують для закриття файлів, з'єднань з базою даних або видалення тимчасових даних. Це допомагає уникнути "витоків ресурсів" і робить середовище підготовленим для наступних тестів.

Приклад:

```python
Копіювати код
import unittest

class TestFiles(unittest.TestCase):
    
    def setUp(self):
        """Відкриває файл перед кожним тестом"""
        self.file = open('testfile.txt', 'w')
    
    def test_write_to_file(self):
        """Тест для запису в файл"""
        self.file.write('Hello, world!')
        self.file.seek(0)  # Переміщуємо вказівник на початок файла
        
    def tearDown(self):
        """Закриває файл після кожного тесту"""
        self.file.close()

if __name__ == '__main__':
    unittest.main()
```
У цьому прикладі:

- setUp() відкриває файл перед кожним тестом.
- tearDown() закриває файл після виконання тесту, щоб уникнути витоку ресурсів.

4.3. Переваги використання setUp() і tearDown()

- Зменшення дублювання коду: Код ініціалізації та очищення не повторюється в кожному тесті, що робить тести більш компактними та зручними.
- Ізольоване середовище для тестів: Тестові методи не впливають один на одного, оскільки середовище налаштовується заново перед кожним тестом і очищується після нього.
- Управління ресурсами: Допомагає забезпечити правильне використання ресурсів, таких як файли, мережеві з'єднання або бази даних.

4.4. Набір тестів з використанням setUp() та tearDown()
```python
import unittest

class TestCalculator(unittest.TestCase):
    
    def setUp(self):
        """Ініціалізація калькулятора перед кожним тестом"""
        self.calculator = Calculator()

    def tearDown(self):
        """Очистка після кожного тесту"""
        self.calculator = None

    def test_add(self):
        result = self.calculator.add(2, 3)
        self.assertEqual(result, 5)

    def test_subtract(self):
        result = self.calculator.subtract(5, 3)
        self.assertEqual(result, 2)

if __name__ == '__main__':
    unittest.main()
```
- setUp() створює новий об'єкт Calculator перед кожним тестом.
- tearDown() звільняє ресурси, видаляючи об'єкт Calculator після кожного тесту.

4.5. Методи setUpClass() та tearDownClass()

Якщо вам потрібно налаштувати середовище один раз для всіх тестів у класі, ви можете використовувати методи класу:

- setUpClass() викликається один раз перед виконанням всіх тестів у класі.
- tearDownClass() викликається один раз після завершення всіх тестів у класі.
Приклад:

```python
class TestDatabase(unittest.TestCase):
    
    @classmethod
    def setUpClass(cls):
        """Налаштування перед запуском усіх тестів"""
        cls.connection = connect_to_database()

    @classmethod
    def tearDownClass(cls):
        """Закриття підключення після завершення всіх тестів"""
        cls.connection.close()

    def test_query(self):
        result = self.connection.query('SELECT * FROM users')
        self.assertIsNotNone(result)

if __name__ == '__main__':
    unittest.main()
```

Методи setUp(), tearDown(), а також їхні класові версії setUpClass() і tearDownClass() допомагають забезпечити ефективне управління ресурсами під час тестування. Вони роблять тестування зручнішим і більш надійним, зменшуючи ризик побічних ефектів між тестами та забезпечуючи чисте середовище для кожного тесту.


## 5. Поради щодо модульного тестування
- Малі та ізольовані тести: Пишіть тести, які перевіряють окремі модулі чи функції незалежно від інших.
- Покриття коду: Використовуйте інструменти для аналізу покриття коду тестами, такі як coverage.py.
- Автоматизація тестування: Інтегруйте тести в CI/CD-процеси для автоматичного виконання під час змін у коді.

Модульне тестування — це основний етап забезпечення якості програмного забезпечення, який допомагає виявити та виправити помилки на ранніх етапах розробки. Використовуючи правильні патерни проектування та автоматизацію тестування, можна значно підвищити ефективність розробки.
