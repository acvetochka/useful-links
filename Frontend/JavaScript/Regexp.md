# Регулярні вирази у JavaScript

Що таке регулярні вирази?

Регулярні вирази (RegExp) — це шаблони, які використовуються для пошуку або маніпуляції рядками, базуючись на певних правилах. Вони дозволяють виконувати складні пошуки та заміни у тексті.

## Зміст

- [Створення регулярних виразів](https://github.com/acvetochka/useful/blob/main/Frontend/JavaScript/Regexp.md#%D1%81%D1%82%D0%B2%D0%BE%D1%80%D0%B5%D0%BD%D0%BD%D1%8F-%D1%80%D0%B5%D0%B3%D1%83%D0%BB%D1%8F%D1%80%D0%BD%D0%B8%D1%85-%D0%B2%D0%B8%D1%80%D0%B0%D0%B7%D1%96%D0%B2)
- [Основні елементи синтаксису](https://github.com/acvetochka/useful/blob/main/Frontend/JavaScript/Regexp.md#%D0%BE%D1%81%D0%BD%D0%BE%D0%B2%D0%BD%D1%96-%D0%B5%D0%BB%D0%B5%D0%BC%D0%B5%D0%BD%D1%82%D0%B8-%D1%81%D0%B8%D0%BD%D1%82%D0%B0%D0%BA%D1%81%D0%B8%D1%81%D1%83)
- [Методи для роботи з регулярними виразами](https://github.com/acvetochka/useful/blob/main/Frontend/JavaScript/Regexp.md#%D0%BC%D0%B5%D1%82%D0%BE%D0%B4%D0%B8-%D0%B4%D0%BB%D1%8F-%D1%80%D0%BE%D0%B1%D0%BE%D1%82%D0%B8-%D0%B7-%D1%80%D0%B5%D0%B3%D1%83%D0%BB%D1%8F%D1%80%D0%BD%D0%B8%D0%BC%D0%B8-%D0%B2%D0%B8%D1%80%D0%B0%D0%B7%D0%B0%D0%BC%D0%B8)
- [Захопені групи](https://github.com/acvetochka/useful/blob/main/Frontend/JavaScript/Regexp.md#%D0%B7%D0%B0%D1%85%D0%BE%D0%BF%D0%B5%D0%BD%D1%96-%D0%B3%D1%80%D1%83%D0%BF%D0%B8)
- [Приклади використання](https://github.com/acvetochka/useful/blob/main/Frontend/JavaScript/Regexp.md#%D0%BF%D1%80%D0%B8%D0%BA%D0%BB%D0%B0%D0%B4%D0%B8-%D0%B2%D0%B8%D0%BA%D0%BE%D1%80%D0%B8%D1%81%D1%82%D0%B0%D0%BD%D0%BD%D1%8F)


## Створення регулярних виразів

Регулярні вирази в JavaScript можуть бути створені двома способами:

Літеральний синтаксис:
```javascript
let regex = /abc/; // Шаблон для пошуку "abc"
```

Конструктор RegExp:
```javascript
let regex = new RegExp('abc'); // Також шукає "abc"
```

## Основні елементи синтаксису

- Символи: Для пошуку символів, таких як букви, цифри, або спеціальні символи.

- Метасимволи:

`.` — будь-який символ, крім нового рядка.

`\d` — будь-яка цифра (0-9).

`\D` — будь-який нецифровий символ.

`\w` — будь-який алфавітно-цифровий символ (a-z, A-Z, 0-9, _).

`\W` — будь-який неалфавітно-цифровий символ.

`\s` — пробільний символ (пробіл, табуляція, новий рядок).

`\S` — будь-який не пробільний символ.

- Квантифікатори

Квантифікатори визначають, скільки разів символ чи група можуть повторюватися:

`*` — 0 або більше разів.
  
`+` — 1 або більше разів.
  
`?` — 0 або 1 раз.

`{n}` — рівно n разів.

`{n,}` — n або більше разів.

`{n,m}` — від n до m разів.


## Методи для роботи з регулярними виразами
`test()`: Перевіряє, чи є відповідність.

```javascript
let regex = /abc/;
console.log(regex.test("abcdef")); // true
```

`exec()`: Повертає масив з результатами пошуку або null, якщо відповідності немає.

```javascript
let result = regex.exec("abcdef");
console.log(result[0]); // "abc"
```

Методи рядків:

`String.prototype.match()` — повертає масив з відповідностями.

`String.prototype.replace()` — замінює відповідності.

`String.prototype.search()` — повертає індекс першої відповідності.

`String.prototype.split()` — розділяє рядок за регулярним виразом.


## Захопені групи

Захоплені групи — це механізм у регулярних виразах, який дозволяє виділяти та зберігати частини тексту, що відповідають певному шаблону. Коли регулярний вираз виконує пошук у тексті, захоплені групи дають змогу зберегти конкретні частини цього тексту для подальшого використання, маніпуляцій або аналізу.

Основні особливості:

- Виділення частини тексту: Захоплена група дозволяє взяти частину рядка, що відповідає підшаблону, і зберегти її окремо від всього результату.
  У регулярному виразі захоплені групи визначаються круглими дужками (). Все, що знаходиться між дужками, буде виділено як група.

- Нумерація груп: Кожна група у регулярному виразі автоматично отримує номер, починаючи з першої відкриваючої дужки.
  Це дозволяє легко звертатися до них за допомогою їхнього номера.
  Кожна захоплена група може бути доступною через індекси, починаючи з 1 (оскільки 0 індексується як весь збіг, а не окремі групи).

  Приклад: Для регулярного виразу (\d{3})-(\d{2})-(\d{4}) та рядка 123-45-6789:
  
  -  result[0] поверне весь рядок: 123-45-6789.

  -  result[1] поверне першу захоплену групу: 123.

  -  result[2] поверне другу захоплену групу: 45.

  -  result[3] поверне третю захоплену групу: 6789.

- Повторне використання: Після того, як частину тексту захоплено, її можна використовувати у подальших операціях, наприклад, для заміни, перестановки або перевірки відповідності.

- Захоплення кількох груп: У регулярному виразі можна мати кілька захоплених груп одночасно, що дозволяє працювати з кількома частинами тексту незалежно одна від одної.

У JavaScript для доступу до захоплених груп використовується масив, який повертає методи, такі як `match()` або `exec()`.

📝 Приклад з використанням `exec()`:
```javascript
// Рядок та регулярний вираз з групами
const string = "My phone number is 123-456-7890";
const pattern = /My phone number is (\d{3})-(\d{3})-(\d{4})/;

// Використовуємо exec() для пошуку збігу
const result = pattern.exec(string);

// Виводимо результат
console.log(result[0]);  // Повний збіг: "My phone number is 123-456-7890"
console.log(result[1]);  // Перша захоплена група: "123"
console.log(result[2]);  // Друга захоплена група: "456"
console.log(result[3]);  // Третя захоплена група: "7890"
```

Що відбувається у JavaScript:

Регулярний вираз: `/My phone number is (\d{3})-(\d{3})-(\d{4})/`

`(\d{3})` — захоплює три цифри як першу групу.

`(\d{3})` — друга група.

`(\d{4})` — третя група.

`result[0]`: Повертає повний збіг, який відповідає всьому шаблону: "My phone number is 123-456-7890".

`result[1]`, `result[2]`, і т.д.: Повертають захоплені групи — "123", "456", "7890".


📝 Альтернативний спосіб — `match()`:

Метод match() також може використовуватись для отримання захоплених груп, але результат буде трохи іншим. Якщо не вказати глобальний флаг g, він також повертає масив, де перший елемент — це повний збіг, а наступні елементи — захоплені групи.

```javascript
const result = string.match(/My phone number is (\d{3})-(\d{3})-(\d{4})/);
console.log(result[0]);  // Повний збіг: "My phone number is 123-456-7890"
console.log(result[1]);  // Перша захоплена група: "123"
console.log(result[2]);  // Друга захоплена група: "456"
console.log(result[3]);  // Третя захоплена група: "7890"
```

💡 Різниця між exec() та match():

`exec()`: Повертає масив з результатами та інформацією про збіг, його можна використовувати в циклі для послідовного пошуку збігів.

`match()`: Повертає масив лише для першого знайденого збігу (якщо не використовується флаг g).


## Приклади використання
1. Перевірка формату електронної пошти:

```javascript
let emailRegex = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
console.log(emailRegex.test("example@example.com")); // true
```

2. Заміна всіх пробілів на дефіси:

```javascript
let str = "Hello World";
let newStr = str.replace(/\s+/g, '-');
console.log(newStr); // "Hello-World"
```

3. Виділення чисел з рядка:

```javascript
let str = "There are 123 apples and 456 oranges.";
let numbers = str.match(/\d+/g);
console.log(numbers); // ["123", "456"]
```

## Висновок
Регулярні вирази в JavaScript — потужний інструмент для роботи з текстовими даними. Вони дозволяють виконувати різноманітні операції пошуку, заміни та валідації, роблячи обробку рядків набагато простішою та ефективнішою.

Зрозуміння основних концепцій, таких як метасимволи, квантифікатори та захоплені групи, є ключовим для успішного використання регулярних виразів у ваших JavaScript-додатках.
