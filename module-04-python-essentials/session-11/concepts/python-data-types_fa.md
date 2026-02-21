# انواع داده تو پایتون: سازماندهی اطلاعات

## انواع داده چی هستن؟

انواع داده مشخص می‌کنن که یک متغیر چه مقادیری می‌تونه نگه داره و چه عملیاتی می‌تونیم روش اعمال کنیم. پایتون چندین نوع داده داخلی داره که هر کدوم برای انواع مختلفی از داده‌ها مناسبه.

## انواع عددی

### اعداد صحیح (int)
اعداد کامل، مثبت یا منفی:
```python
# اعداد صحیح پایه
age = 25
temperature = -5
year = 2024

# اعداد صحیح بزرگ (بدون محدودیت اندازه تو پایتون ۳)
very_large = 123456789012345678901234567890
print(type(very_large))  # <class 'int'>

# پایه‌های مختلف
decimal = 42        # دهدهی (پایه ۱۰)
binary = 0b101010   # باینری (پایه ۲)
octal = 0o52        # octal (پایه ۸)
hexadecimal = 0x2A  # hexadecimal (پایه ۱۶)
```

### اعداد اعشاری (float)
اعداد با نقطه اعشار:
```python
# floatهای پایه
pi = 3.14159
price = 19.99
weight = 65.5

# نماد علمی
avogadro = 6.022e23  # 6.022 × 10²³
microsecond = 1e-6   # 1 × 10⁻⁶

# مقادیر float ویژه
positive_infinity = float('inf')
negative_infinity = float('-inf')
not_a_number = float('nan')

# محدودیت‌های دقت
print(0.1 + 0.2)  # 0.30000000000000004 (دقیقاً 0.3 نیست!)
```

### اعداد مختلط (complex)
اعداد با قسمت حقیقی و موهومی:
```python
# ایجاد عدد مختلط
z1 = 3 + 4j      # حقیقی: 3، موهومی: 4
z2 = complex(2, 5)  # با استفاده از تابع complex()

# عملیات مختلط
print(z1 + z2)   # (5+9j)
print(z1 * z2)   # (-14+23j)
print(z1.real)   # 3.0
print(z1.imag)   # 4.0
print(abs(z1))   # 5.0 (قدر مطلق)
```

## نوع متنی

### رشته‌ها (str)
دنباله‌ای از کاراکترها:
```python
# ایجاد رشته
name = "Alice"
message = 'Hello, World!'
multiline = """این یک رشته
چندخطی است"""

# ویژگی‌های رشته
text = "Python"
print(len(text))      # 6 (طول)
print(text[0])        # 'P' (اولین کاراکتر)
print(text[-1])       # 'n' (آخرین کاراکتر)

# رشته‌ها غیرقابل تغییر هستند
# text[0] = 'J'  # TypeError!
```

### عملیات رشته
```python
text = "Hello, World!"

# اتصال
greeting = "Hello" + " " + "Alice"  # "Hello Alice"

# تکرار
divider = "=" * 50  # "=================================================="

# عضویت
print("Hello" in text)   # True
print("Python" in text)  # False

# برش
print(text[0:5])    # "Hello"
print(text[7:])     # "World!"
print(text[::-1])   # "!dlroW ,olleH" (معکوس شده)
```

### روش‌های رشته
```python
text = "hello world"

# تبدیل حالت
print(text.upper())       # "HELLO WORLD"
print(text.lower())       # "hello world"
print(text.capitalize())  # "Hello world"
print(text.title())       # "Hello World"

# جستجو
print(text.find("world"))    # 6
print(text.count("l"))       # 3
print(text.startswith("hello"))  # True

# تغییر
print(text.replace("world", "Python"))  # "hello Python"
words = text.split()        # ["hello", "world"]
joined = " ".join(words)    # "hello world"

# تست
print(text.isalpha())   # False (شامل فاصله)
print(text.islower())   # True
print(text.isdigit())   # False
```

## نوع بولی

### بولی‌ها (bool)
مقادیر درست/نادرست:
```python
# literals بولی
is_active = True
is_deleted = False

# بولی از مقایسه‌ها
age = 25
is_adult = age >= 18      # True
is_senior = age >= 65     # False

# بولی از انواع دیگر
print(bool(0))        # False
print(bool(1))        # True
print(bool(""))       # False (رشته خالی)
print(bool("hello"))  # True
print(bool([]))       # False (لیست خالی)
print(bool([1, 2]))   # True
```

### عملیات بولی
```python
# منطقی AND
result = True and False  # False
result = True and True   # True

# منطقی OR
result = True or False   # True
result = False or False  # False

# منطقی NOT
result = not True        # False
result = not False       # True

# ارزیابی کوتاه‌مدت
def expensive_operation():
    print("این گران است!")
    return True

# AND در اولین False متوقف می‌شود
result = False and expensive_operation()  # expensive_operation() را فراخوانی نمی‌کند

# OR در اولین True متوقف می‌شود
result = True or expensive_operation()    # expensive_operation() را فراخوانی نمی‌کند
```

## انواع دنباله

### لیست‌ها (list)
دنباله‌های مرتب و قابل تغییر:
```python
# ایجاد لیست
numbers = [1, 2, 3, 4, 5]
names = ["Alice", "Bob", "Charlie"]
mixed = [1, "hello", True, 3.14]

# لیست خالی
empty = []
empty = list()

# عملیات لیست
numbers.append(6)        # [1, 2, 3, 4, 5, 6]
numbers.insert(0, 0)     # [0, 1, 2, 3, 4, 5, 6]
numbers.remove(3)        # [0, 1, 2, 4, 5, 6]
last = numbers.pop()     # 6، لیست به [0, 1, 2, 4, 5] تبدیل می‌شود

# ایندکس‌گذاری و برش
print(numbers[0])        # 0
print(numbers[-1])       # 5
print(numbers[1:4])      # [1, 2, 4]

# روش‌های لیست
numbers.sort()           # [0, 1, 2, 4, 5]
numbers.reverse()        # [5, 4, 2, 1, 0]
length = len(numbers)    # 5
```

### تاپل‌ها (tuple)
دنباله‌های مرتب و غیرقابل تغییر:
```python
# ایجاد تاپل
coordinates = (10, 20)
person = ("Alice", 25, "Engineer")

# تاپل تک عنصری
single = (42,)  # کاما را فراموش نکنید!

# تاپل خالی
empty = ()
empty = tuple()

# عملیات تاپل (مشابه لیست‌ها)
print(coordinates[0])    # 10
print(len(coordinates))  # 2

# تاپل‌ها غیرقابل تغییر هستند
# coordinates[0] = 15  # TypeError!

# باز کردن بسته
x, y = coordinates
name, age, job = person
```

### محدوده‌ها (range)
دنباله‌های غیرقابل تغییر از اعداد:
```python
# ایجاد محدوده
numbers = range(5)          # 0, 1, 2, 3, 4
even_numbers = range(0, 10, 2)  # 0, 2, 4, 6, 8

# محدوده به لیست
list(range(5))              # [0, 1, 2, 3, 4]
list(range(2, 8))           # [2, 3, 4, 5, 6, 7]
list(range(10, 0, -1))      # [10, 9, 8, 7, 6, 5, 4, 3, 2, 1]

# ویژگی‌های محدوده
r = range(0, 100, 5)
print(r.start)     # 0
print(r.stop)      # 100
print(r.step)      # 5
print(len(r))      # 20
print(25 in r)     # True
```

## نوع نگاشت

### دیکشنری‌ها (dict)
جفت‌های کلید-مقدار:
```python
# ایجاد دیکشنری
person = {
    "name": "Alice",
    "age": 25,
    "city": "New York"
}

# دیکشنری خالی
empty = {}
empty = dict()

# ایجاد جایگزین
person2 = dict(name="Bob", age=30, city="London")

# دسترسی به مقادیر
print(person["name"])       # "Alice"
print(person.get("age"))    # 25
print(person.get("salary", "مشخص نشده"))  # "مشخص نشده"

# تغییر دیکشنری‌ها
person["age"] = 26          # بروزرسانی موجود
person["job"] = "Engineer"  # اضافه کردن جدید
del person["city"]          # حذف

# روش‌های دیکشنری
print(person.keys())        # dict_keys(['name', 'age', 'job'])
print(person.values())      # dict_values(['Alice', 26, 'Engineer'])
print(person.items())       # dict_items([('name', 'Alice'), ('age', 26), ('job', 'Engineer')])

# تست عضویت
print("name" in person)     # True (کلید وجود دارد)
print("Alice" in person)    # False (مقدار وجود دارد، اما کلیدها را چک می‌کنیم)
```

## انواع مجموعه

### مجموعه‌ها (set)
مجموعه‌های نامرتب از عناصر منحصر به فرد:
```python
# ایجاد مجموعه
fruits = {"apple", "banana", "cherry"}
numbers = set([1, 2, 3, 3, 4])  # {1, 2, 3, 4} (تکراری‌ها حذف شدند)

# مجموعه خالی
empty = set()  # نه {} که دیکشنری ایجاد می‌کند!

# عملیات مجموعه
fruits.add("date")          # {"apple", "banana", "cherry", "date"}
fruits.remove("banana")     # {"apple", "cherry", "date"}
fruits.discard("grape")     # اگر عنصر وجود ندارد خطا نمی‌دهد

# عملیات ریاضی مجموعه
set1 = {1, 2, 3, 4}
set2 = {3, 4, 5, 6}

print(set1 | set2)  # اجتماع: {1, 2, 3, 4, 5, 6}
print(set1 & set2)  # اشتراک: {3, 4}
print(set1 - set2)  # تفاضل: {1, 2}
print(set1 ^ set2)  # تفاضل متقارن: {1, 2, 5, 6}
```

### مجموعه‌های منجمد (frozenset)
مجموعه‌های غیرقابل تغییر:
```python
# ایجاد مجموعه منجمد
immutable_set = frozenset([1, 2, 3, 4])

# می‌توان به عنوان کلید دیکشنری استفاده کرد
coordinates = {(1, 2): "نقطه A", (3, 4): "نقطه B"}
# لیست‌ها نمی‌توانند کلید باشند، اما frozensetها می‌توانند
```

## نوع None

### NoneType
نمایانگر نبود مقدار:
```python
# literal None
result = None

# توابعی که مقداری برنمی‌گردانند
def print_message(message):
    print(message)
    # هیچ دستور return = None برمی‌گرداند

result = print_message("Hello")
print(result)  # None

# چک کردن None
if result is None:
    print("مقداری برگردانده نشده")

# None در برابر False در برابر 0 در برابر رشته خالی
print(None == False)    # False
print(None == 0)        # False
print(None == "")       # False
print(None is None)     # True (از 'is' برای None استفاده کنید)
```

## تبدیل نوع

### تبدیل ضمنی (Coercion)
پایتون به طور خودکار انواع را در برخی موارد تبدیل می‌کند:
```python
# coercion عددی
result = 5 + 3.2  # 8.2 (int + float = float)

# اتصال رشته
message = "شمارش: " + str(5)  # باید int را به رشته تبدیل کنیم
```

### تبدیل صریح (Casting)
به طور دستی بین انواع تبدیل کنید:
```python
# به رشته
str(42)        # "42"
str(3.14)      # "3.14"
str(True)      # "True"

# به عدد صحیح
int("42")      # 42
int(3.14)      # 3 (قطع می‌کند)
int(True)      # 1

# به عدد اعشاری
float("3.14")  # 3.14
float(42)      # 42.0
float(True)    # 1.0

# به بولی
bool(0)        # False
bool(1)        # True
bool("")       # False
bool("hello")  # True
bool([])       # False
bool([1, 2])   # True

# به لیست/تاپل
list("hello")  # ['h', 'e', 'l', 'l', 'o']
tuple([1, 2, 3])  # (1, 2, 3)

# به مجموعه
set([1, 2, 2, 3])  # {1, 2, 3}
```

### تبدیل امن
```python
# مدیریت خطاهای تبدیل
def safe_int_conversion(value):
    try:
        return int(value)
    except ValueError:
        return None

print(safe_int_conversion("42"))    # 42
print(safe_int_conversion("hello")) # None
```

## بررسی نوع

### بررسی نوع زمان اجرا
```python
# بررسی نوع متغیر
x = 42
print(type(x))        # <class 'int'>
print(isinstance(x, int))   # True
print(isinstance(x, str))   # False

# بررسی چندین نوع
def is_numeric(value):
    return isinstance(value, (int, float, complex))

print(is_numeric(42))      # True
print(is_numeric("42"))    # False
print(is_numeric(3.14))    # True
```

## نکات کلیدی

۱. **پایتون انواع داده داخلی** برای انواع مختلف اطلاعات دارد
۲. **انواع داده تعیین می‌کنند** چه عملیاتی موجود است
۳. **تبدیل نوع** اجازه کار با انواع مختلف را می‌دهد
۴. **مجموعه‌ها** (لیست‌ها، تاپل‌ها، دیکشنری‌ها، مجموعه‌ها) چندین مقدار را سازماندهی می‌کنند
۵. **None نمایانگر** نبود مقدار است
۶. **بررسی نوع** استفاده درست را تضمین می‌کند

## مطالعه بیشتر
- مستندات مدل داده پایتون
- مفاهیم برنامه‌نویسی شی‌گرا
- نکات نوع و حاشیه‌نویسی‌ها (پایتون ۳.۵+)
- ساختارهای داده پیشرفته (ماژول collections)