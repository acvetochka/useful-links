# Module CSV
Конспект по модулю csv у Python

Модуль csv у Python використовується для зручної роботи з файлами у форматі CSV (Comma Separated Values), які містять табличні дані. Модуль дозволяє легко читати з CSV файлів, записувати в них, а також працювати з даними як з рядками та стовпцями.

## 1. Імпорт модуля csv
Для використання функцій модуля спочатку його потрібно імпортувати:
```python
import csv
```

## 2. Основні функції модуля csv
### 2.1. Читання з CSV файлів
Для читання CSV файлів використовується клас csv.reader.
- csv.reader(file) — зчитує CSV файл і повертає об'єкт-ітератор, який дозволяє по черзі отримувати рядки з файлу.
Приклад читання CSV файлу:
```python
import csv

with open("data.csv", newline='') as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)
```

Параметр newline='': використовується, щоб коректно читати файли, особливо на Windows, без додаткових порожніх рядків між записами.

Результат: кожен рядок файлу буде виведено у вигляді списку значень.

### 2.2. Читання з CSV файлів з заголовками
Якщо файл CSV містить заголовки (назви стовпців), зручніше використовувати клас csv.DictReader, який перетворює кожен рядок у словник, де ключі — це заголовки стовпців.

Приклад використання csv.DictReader:
```python
import csv

with open("data.csv", newline='') as file:
    reader = csv.DictReader(file)
    for row in reader:
        print(row)
```

Результат: кожен рядок файлу буде виведено як словник, де ключі відповідають назвам стовпців, а значення — елементам рядка.

### 2.3. Запис у CSV файли
Для запису у CSV файли використовується клас csv.writer.
- csv.writer(file) — повертає об'єкт, який дозволяє записувати рядки у файл.

Приклад запису у CSV файл:
python
```
import csv

with open("output.csv", "w", newline='') as file:
    writer = csv.writer(file)
    writer.writerow(["Name", "Age", "City"])
    writer.writerow(["Alice", 30, "New York"])
    writer.writerow(["Bob", 25, "Los Angeles"])
```
- writer.writerow(): записує один рядок у файл.

- writer.writerows(): записує відразу кілька рядків (список списків).

### 2.4. Запис у CSV файли зі словниками
Якщо дані представлені у вигляді словників, зручно використовувати клас csv.DictWriter, який дозволяє записувати дані у вигляді словників.

Приклад використання csv.DictWriter:
```python
import csv

with open("output.csv", "w", newline='') as file:
    fieldnames = ["Name", "Age", "City"]
    writer = csv.DictWriter(file, fieldnames=fieldnames)

    writer.writeheader()  # Записує заголовки стовпців
    writer.writerow({"Name": "Alice", "Age": 30, "City": "New York"})
    writer.writerow({"Name": "Bob", "Age": 25, "City": "Los Angeles"})
```
- writer.writeheader(): записує заголовки стовпців.
- writer.writerow(): записує один рядок даних у вигляді словника.

## 3. Налаштування CSV
Модуль csv підтримує налаштування різних параметрів при читанні та записі файлів, наприклад:

- Дільник (delimiter): визначає символ, який розділяє значення у CSV (наприклад, кома, крапка з комою тощо).
- Кавички (quotechar): визначає символ, який використовується для обрамлення значень, що містять спеціальні символи.
Приклад налаштування параметрів delimiter і quotechar:
```python
import csv

with open("data.csv", newline='') as file:
    reader = csv.reader(file, delimiter=';', quotechar='"')
    for row in reader:
        print(row)
```
- delimiter=';': використовується крапка з комою як дільник між значеннями.
- quotechar='"': використовується подвійна лапка для обрамлення значень.

## 4. Обробка спеціальних випадків
Пропуск порожніх рядків: можна використовувати параметр skipinitialspace=True, щоб ігнорувати початкові пропуски.

Обробка значень з комами: значення, які містять коми, зазвичай обрамляються у лапки, щоб уникнути плутанини з дільником.

## 5. Приклади використання
### 5.1. Читання CSV файлу з користувацькими налаштуваннями
```python
import csv

with open("data.csv", newline='') as file:
    reader = csv.reader(file, delimiter=';', quotechar='"')
    for row in reader:
        print(row)
```

### 5.2. Запис у CSV файл з кількома рядками
```python
import csv

data = [
    ["Name", "Age", "City"],
    ["Alice", 30, "New York"],
    ["Bob", 25, "Los Angeles"]
]

with open("output.csv", "w", newline='') as file:
    writer = csv.writer(file)
    writer.writerows(data)
```

### 5.3. Читання та запис зі словниками
```python
import csv

# Читання CSV як словники
with open("input.csv", newline='') as file:
    reader = csv.DictReader(file)
    for row in reader:
        print(row)

# Запис CSV як словники
with open("output.csv", "w", newline='') as file:
    fieldnames = ["Name", "Age", "City"]
    writer = csv.DictWriter(file, fieldnames=fieldnames)
    writer.writeheader()
    writer.writerows([
        {"Name": "Alice", "Age": 30, "City": "New York"},
        {"Name": "Bob", "Age": 25, "City": "Los Angeles"}
    ])
```

## 6. Висновок
Модуль csv є простим і потужним інструментом для роботи з табличними даними у форматі CSV. Він дозволяє легко читати, обробляти та записувати дані як у вигляді рядків, так і у вигляді словників, що робить його дуже зручним для обробки даних у форматі CSV.