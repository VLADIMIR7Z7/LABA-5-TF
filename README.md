# Лабораторная работа №5  
Построение AST и проверка контекстно-зависимых условий  

**Автор:** 
Петрухно В.К. АП-327

---

## Вариант задания

**Тема:** анализ строк формата  

f"{id:.Ne}";


**Примеры корректных строк:**

f"{number:.2e}";
f"{x:.10e}";
f"{value:.5e}";


---

## Контекстно-зависимые условия

В программе реализованы следующие проверки:

### 1. Использование объявленных идентификаторов
Проверяется, что идентификатор существует в таблице символов.

**Пример:**

f"{abc:.2e}";


**Сообщение:**

Ошибка: идентификатор 'abc' не объявлен

<img width="1182" height="633" alt="image" src="https://github.com/user-attachments/assets/66bd4677-26fd-4d1f-b637-58af24ecb445" />


---

### 2. Совместимость типов
Формат `e` допустим только для числовых типов (`Int`, `Double`, `Float`, `Decimal`).

**Пример:**

f"{name:.2e}";


**Сообщение:**

Ошибка: формат 'e' применим только к числовым типам, найден тип String

<img width="1178" height="807" alt="image" src="https://github.com/user-attachments/assets/fbd959b8-965f-4763-8e4d-f5b13a9c0b6a" />


---

### 3. Допустимые значения (диапазон)
Проверяется, что значение точности находится в диапазоне `0..16`.

**Пример:**

f"{number:.20e}";


**Сообщение:**

Ошибка: значение точности 20 выходит за допустимый диапазон 0..16

<img width="1177" height="807" alt="image" src="https://github.com/user-attachments/assets/45594776-ee91-47f4-9b4e-07e22f289295" />


---

### 4. Повторное использование идентификаторов
Проверяется повторное использование идентификатора в рамках анализа.

**Пример:**

f"{number:.2e}";
f"{number:.3e}";


**Сообщение:**

Ошибка: идентификатор 'number' уже использован в данной области

<img width="1181" height="799" alt="image" src="https://github.com/user-attachments/assets/ba159fd9-19de-4793-a033-2033fcdc835a" />


---

## Структура AST

В программе реализована иерархия узлов:

- `ProgramNode` — корневой узел
- `FormatStringNode` — строка форматирования
- `IdentifierNode` — идентификатор
- `PrecisionNode` — точность
- `FormatNode` — формат

---

## Пример AST

Для строки:

f"{number:.2e}";

Вывод:

<img width="1182" height="807" alt="image" src="https://github.com/user-attachments/assets/3dd8762d-d416-4483-8be3-ce7a05fe6610" />



---

## CST / AST схема

(Добавь сюда изображение из draw.io)

---

## Формат вывода AST

- Дерево выводится в текстовом виде  
- Используются символы `├──`, `└──`  
- Вложенность отражает структуру программы  
- Каждый узел содержит атрибуты  

---

## Тестовые примеры

### Корректные:

f"{number:.2e}";
<img width="821" height="590" alt="image" src="https://github.com/user-attachments/assets/0e69c540-117d-4422-bb08-2ea390be7a0f" />

<img width="728" height="795" alt="image" src="https://github.com/user-attachments/assets/6406e251-b5ad-466f-9732-f7c82bcaab88" />

f"{x:.5e}";
<img width="1102" height="784" alt="image" src="https://github.com/user-attachments/assets/28652aa0-542b-4aa3-8b89-62075b48d0b1" />

<img width="1151" height="802" alt="image" src="https://github.com/user-attachments/assets/b9288098-41c0-41a9-895d-0832fe926435" />


### Семантические ошибки:

f"{abc:.2e}";
<img width="1177" height="783" alt="image" src="https://github.com/user-attachments/assets/290f033d-8960-420d-a86c-23509571d956" />


f"{name:.2e}";
<img width="1181" height="807" alt="image" src="https://github.com/user-attachments/assets/e00fcbf4-9b99-4a73-bcb9-0bdf03742517" />


f"{number:.20e}";
<img width="1178" height="803" alt="image" src="https://github.com/user-attachments/assets/a0ba29f0-d91d-4160-a379-05952adae9ca" />


---

## Инструкция по запуску

1. Открыть проект в Visual Studio  
2. Собрать проект (Build → Build Solution)  
3. Запустить программу (F5)  
4. Ввести строку в редакторе  
5. Нажать кнопку "Анализ"  

---

## ИТОГ

Программа выполняет:

- Лексический анализ  
- Синтаксический анализ  
- Построение AST  
- Семантический анализ  

Результаты отображаются в виде:

- Таблицы лексем  
- Таблицы ошибок  
- AST
