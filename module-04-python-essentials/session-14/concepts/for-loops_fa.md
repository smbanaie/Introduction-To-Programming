# حلقه‌های for: تکرار روی مجموعه‌ها

## مقدمه حلقه‌های for

حلقه‌های for در پایتون روی دنباله‌ها (مانند لیست‌ها، رشته‌ها، تاپل‌ها) یا سایر اشیای iterable تکرار می‌کنند. آنها به طور خودکار فرآیند تکرار را مدیریت می‌کنند که آنها را ایمن‌تر و راحت‌تر از ایندکس‌گذاری دستی می‌کند.

## نحو پایه حلقه for

### تکرار روی لیست‌ها
```python
# حلقه for پایه
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(f"I like {fruit}")

# Output:
# I like apple
# I like banana
# I like cherry
```

### تکرار روی رشته‌ها
```python
# رشته‌ها دنباله‌ای از کاراکترها هستند
message = "Hello"
for char in message:
    print(char)

# Output:
# H
# e
# l
# l
# o
```

### تکرار روی محدوده‌ها
```python
# استفاده از range() برای اعداد
for i in range(5):  # 0, 1, 2, 3, 4
    print(f"Count: {i}")

# محدوده با شروع و پایان
for num in range(2, 6):  # 2, 3, 4, 5
    print(num)

# محدوده با step
for even in range(0, 10, 2):  # 0, 2, 4, 6, 8
    print(f"Even: {even}")
```

## کار با ایندکس‌ها

### استفاده از enumerate()
```python
# هم ایندکس و هم مقدار را دریافت کن
fruits = ["apple", "banana", "cherry"]
for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")

# Output:
# 0: apple
# 1: banana
# 2: cherry

# شمارش را از 1 شروع کن
for index, fruit in enumerate(fruits, start=1):
    print(f"{index}. {fruit}")

# Output:
# 1. apple
# 2. banana
# 3. cherry
```

### ایندکس‌گذاری دستی (توصیه نمی‌شود)
```python
# کمتر Pythonic، اما ممکن
fruits = ["apple", "banana", "cherry"]
for i in range(len(fruits)):
    print(f"{i}: {fruits[i]}")

# همان output مثال enumerate
```

## تکرار روی دیکشنری‌ها

### فقط کلیدها
```python
person = {"name": "Alice", "age": 25, "city": "New York"}

for key in person:
    print(f"Key: {key}")

# Output:
# Key: name
# Key: age
# Key: city
```

### کلیدها و مقادیر
```python
for key, value in person.items():
    print(f"{key}: {value}")

# Output:
# name: Alice
# age: 25
# city: New York
```

### فقط مقادیر
```python
for value in person.values():
    print(f"Value: {value}")

# Output:
# Value: Alice
# Value: 25
# Value: New York
```

## حلقه‌های for تو در تو

### تو در تو پایه
```python
# جدول ضرب
for i in range(1, 4):  # 1, 2, 3
    for j in range(1, 4):  # 1, 2, 3
        print(f"{i} * {j} = {i * j}")
    print()  # خط خالی بعد از هر ردیف

# Output:
# 1 * 1 = 1
# 1 * 2 = 2
# 1 * 3 = 3
#
# 2 * 1 = 2
# etc.
```

### تکرار روی لیست‌های 2D
```python
# ماتریس (لیستی از لیست‌ها)
matrix = [
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]

for row in matrix:
    for element in row:
        print(element, end=" ")
    print()  # خط جدید بعد از هر ردیف

# Output:
# 1 2 3
# 4 5 6
# 7 8 9
```

## فهم لیست

### فهم پایه
```python
# رویکرد سنتی
numbers = [1, 2, 3, 4, 5]
squares = []
for num in numbers:
    squares.append(num ** 2)

print(squares)  # [1, 4, 9, 16, 25]

# فهم لیست
squares = [num ** 2 for num in numbers]
print(squares)  # همان نتیجه
```

### فهم با شرایط
```python
# فیلتر اعداد زوج
numbers = [1, 2, 3, 4, 5, 6]
evens = [num for num in numbers if num % 2 == 0]
print(evens)  # [2, 4, 6]

# تبدیل با شرط
result = [num * 2 if num > 3 else num for num in numbers]
print(result)  # [1, 2, 3, 8, 10, 12]
```

### فهم‌های تو در تو
```python
# ماتریس را flatten کن
matrix = [[1, 2], [3, 4], [5, 6]]
flattened = [num for row in matrix for num in row]
print(flattened)  # [1, 2, 3, 4, 5, 6]

# جدول ضرب ایجاد کن
table = [[i * j for j in range(1, 4)] for i in range(1, 4)]
print(table)  # [[1, 2, 3], [2, 4, 6], [3, 6, 9]]
```

## تکرار روی فایل‌ها

### خواندن خط‌ها
```python
# همه خط‌ها را بخوان
with open("data.txt", "r") as file:
    for line in file:
        print(line.strip())  # کاراکترهای newline را حذف کن

# خط به خط با شماره خط پردازش کن
with open("data.txt", "r") as file:
    for line_num, line in enumerate(file, start=1):
        print(f"Line {line_num}: {line.strip()}")
```

### پردازش داده‌های CSV-like
```python
# پردازش CSV ساده
data = [
    "Alice,25,Engineer",
    "Bob,30,Designer",
    "Charlie,35,Manager"
]

for row in data:
    name, age, job = row.split(",")
    print(f"{name} is {age} years old and works as {job}")
```

## الگوهای تکرار پیشرفته

### تکرار با zip()
```python
# تکرار موازی
names = ["Alice", "Bob", "Charlie"]
ages = [25, 30, 35]
cities = ["NYC", "LA", "Chicago"]

for name, age, city in zip(names, ages, cities):
    print(f"{name} ({age}) lives in {city}")

# Output:
# Alice (25) lives in NYC
# Bob (30) lives in LA
# Charlie (35) lives in Chicago
```

### تکرار معکوس
```python
# تکرار معکوس
fruits = ["apple", "banana", "cherry"]
for fruit in reversed(fruits):
    print(fruit)

# Output:
# cherry
# banana
# apple

# معکوس با ایندکس‌ها
for i in reversed(range(len(fruits))):
    print(f"{i}: {fruits[i]}")
```

### تکرار با step
```python
# هر عنصر دیگر
numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]

# استفاده از نماد برش
for num in numbers[::2]:  # Start:0, End:len, Step:2
    print(num, end=" ")  # 0 2 4 6 8

print()

# استفاده از range
for i in range(0, len(numbers), 2):
    print(numbers[i], end=" ")  # همان نتیجه
```

## ملاحظات عملکرد

### از تغییر لیست‌ها در طول تکرار اجتناب کن
```python
# مشکل‌دار - تغییر در طول تکرار
numbers = [1, 2, 3, 4, 5]
for num in numbers:
    if num % 2 == 0:
        numbers.remove(num)  # تغییر لیست در طول تکرار

print(numbers)  # [1, 3, 5] - 4 رد شد!

# بهتر - لیست جدید ایجاد کن
numbers = [1, 2, 3, 4, 5]
odds = [num for num in numbers if num % 2 != 0]
print(odds)  # [1, 3, 5]
```

### از ساختارهای داده مناسب استفاده کن
```python
# برای تست عضویت، از مجموعه‌ها استفاده کن
lookup_items = {"apple", "banana", "cherry"}  # مجموعه برای lookup O(1)
fruits = ["apple", "grape", "banana", "orange", "cherry"]

for fruit in fruits:
    if fruit in lookup_items:  # lookup سریع
        print(f"Found: {fruit}")
```

## الگوهای رایج حلقه for

### الگوی accumulator
```python
# جمع همه اعداد
numbers = [1, 2, 3, 4, 5]
total = 0
for num in numbers:
    total += num
print(f"Sum: {total}")  # 15

# شمارش رخدادها
text = "hello world"
letter_counts = {}
for char in text:
    if char != " ":  # فاصله‌ها را رد کن
        letter_counts[char] = letter_counts.get(char, 0) + 1

print(letter_counts)  # {'h': 1, 'e': 1, 'l': 3, 'o': 2, 'w': 1, 'r': 1, 'd': 1}
```

### الگوی find
```python
# حداکثر را پیدا کن
numbers = [3, 7, 2, 9, 5]
maximum = numbers[0] if numbers else None

for num in numbers[1:]:
    if num > maximum:
        maximum = num

print(f"Maximum: {maximum}")  # 9

# اولین تطابق را پیدا کن
fruits = ["apple", "banana", "cherry", "date"]
target = "cherry"
found_index = None

for i, fruit in enumerate(fruits):
    if fruit == target:
        found_index = i
        break  # بعد از اولین تطابق جستجو را متوقف کن

print(f"Found {target} at index {found_index}")
```

### الگوی transform
```python
# به حروف بزرگ تبدیل کن
words = ["hello", "world", "python"]
upper_words = []

for word in words:
    upper_words.append(word.upper())

print(upper_words)  # ['HELLO', 'WORLD', 'PYTHON']

# یا با استفاده از فهم لیست
upper_words = [word.upper() for word in words]
print(upper_words)  # همان نتیجه
```

## iterables در برابر iterators

### درک iterables
```python
# لیست‌ها iterable هستند
fruits = ["apple", "banana", "cherry"]
fruit_iter = iter(fruits)  # iterator ایجاد کن

print(next(fruit_iter))  # "apple"
print(next(fruit_iter))  # "banana"
print(next(fruit_iter))  # "cherry"
# print(next(fruit_iter))  # استثنا StopIteration

# حلقه‌های for این را به طور خودکار مدیریت می‌کنند
for fruit in fruits:  # هر بار iterator جدید ایجاد می‌کند
    print(fruit)
```

### ایجاد iterables سفارشی
```python
class Countdown:
    def __init__(self, start):
        self.start = start

    def __iter__(self):
        return CountdownIterator(self.start)

class CountdownIterator:
    def __init__(self, start):
        self.current = start

    def __iter__(self):
        return self

    def __next__(self):
        if self.current <= 0:
            raise StopIteration
        self.current -= 1
        return self.current + 1

# استفاده
for num in Countdown(5):
    print(num, end=" ")  # 5 4 3 2 1
```

## نکات کلیدی

۱. **حلقه‌های for روی دنباله‌ها تکرار می‌کنند** و فرآیند تکرار را به طور خودکار مدیریت می‌کنند
۲. **از enumerate() استفاده کن** برای دسترسی به هر دو ایندکس و مقادیر
۳. **فهم لیست** روش‌های concise برای ایجاد لیست‌های جدید فراهم می‌کند
۴. **حلقه‌های تو در تو** با داده‌های چندبعدی کار می‌کنند
۵. **مراقب تغییر مجموعه‌ها باش** در طول تکرار
۶. **الگوی تکرار مناسب را انتخاب کن** برای مورد استفاده خود

## مطالعه بیشتر
- پروتکل iterator پایتون و generators
- الگوهای تکرار پیشرفته
- بهینه‌سازی عملکرد برای حلقه‌ها
- جایگزین‌های برنامه‌نویسی تابعی (map، filter، reduce)