# متغیرهای پایتون: ذخیره و مدیریت داده‌ها

## متغیرها چیستند؟

متغیرها مکان‌های ذخیره‌سازی نام‌گذاری شده در حافظه هستند که مقادیر داده‌ای را نگه می‌دارند. آنها به برنامه‌ها اجازه می‌دهند تا اطلاعات را در طول اجرا ذخیره، بازیابی و دستکاری کنند.

## اعلام و تخصیص متغیر

### تخصیص پایه
```python
# تخصیص متغیر
age = 25
name = "Alice"
is_student = True
height = 1.75

# تخصیص چندگانه
x, y, z = 1, 2, 3

# مقدار یکسان به چندین متغیر
a = b = c = 0
```

### تایپ پویا
متغیرهای پایتون نیاز به اعلام نوع ندارند:
```python
# متغیر می‌تواند نوع را تغییر دهد
x = 5        # integer
x = "hello"  # string
x = [1, 2, 3]  # list

# نوع در زمان اجرا تعیین می‌شود
print(type(x))  # <class 'list'>
```

## قوانین نام‌گذاری متغیر

### نام‌های معتبر
```python
# نام‌های متغیر خوب
user_name = "Alice"
total_count = 10
is_valid = True
max_value = 100
user_age = 25

# کاراکتر تک (برای حلقه‌ها/شمارنده‌ها)
for i in range(5):
    for j in range(3):
        print(f"i={i}, j={j}")
```

### نام‌های نامعتبر
```python
# نمی‌تواند با عدد شروع شود
# 2variable = 5  # SyntaxError

# بدون فاصله یا کاراکترهای ویژه (به جز زیرخط)
# user-name = "Alice"  # SyntaxError
# user.name = "Alice"  # SyntaxError

# نمی‌توان از کلمات کلیدی پایتون استفاده کرد
# class = "Python"  # SyntaxError
# if = 5           # SyntaxError
```

### قراردادهای نام‌گذاری

#### استانداردهای PEP 8
```python
# متغیرها: snake_case (حروف کوچک با زیرخط)
user_name = "Alice"
total_count = 10
is_active = True

# ثابت‌ها: UPPERCASE_WITH_UNDERSCORES
MAX_CONNECTIONS = 100
DEFAULT_TIMEOUT = 30
PI = 3.14159

# کلاس‌ها: PascalCase
class UserAccount:
    pass

class DataProcessor:
    pass
```

#### نام‌های توصیفی
```python
# بد: هدف نامشخص
x = 25
y = "Alice"
z = True

# خوب: خودتوصیفی
student_age = 25
student_name = "Alice"
is_enrolled = True
```

## حوزه متغیر

### متغیرهای محلی
متغیرهایی که داخل توابع تعریف می‌شوند:
```python
def calculate_area(length, width):
    # متغیرهای محلی
    area = length * width
    return area

# area اینجا قابل دسترسی نیست
# print(area)  # NameError
```

### متغیرهای جهانی
متغیرهایی که در سطح ماژول تعریف می‌شوند:
```python
# متغیر جهانی
counter = 0

def increment_counter():
    global counter  # اعلام می‌کنیم از جهانی استفاده می‌کنیم
    counter += 1
    return counter

increment_counter()  # 1
increment_counter()  # 2
print(counter)       # 2
```

### متغیرهای nonlocal (توابع تو در تو)
```python
def outer_function():
    count = 0

    def inner_function():
        nonlocal count  # دسترسی به متغیر تابع بیرونی
        count += 1
        return count

    return inner_function

counter = outer_function()
print(counter())  # 1
print(counter())  # 2
```

### تفکیک متغیر (قانون LEGB)
پایتون از LEGB (Local، Enclosing، Global، Built-in) برای تفکیک نام پیروی می‌کند:
```python
# Built-in: len، print و غیره
# Global: متغیرهای سطح ماژول
# Enclosing: متغیرها در توابع بیرونی
# Local: متغیرها در تابع فعلی

len = "not the built-in"  # سایه انداختن بر built-in
print(len([1, 2, 3]))     # از متغیر ما استفاده می‌کند، نه built-in
```

## مدیریت حافظه متغیر

### شمارش ارجاع
پایتون تعداد ارجاع‌ها به هر شی را پیگیری می‌کند:
```python
x = [1, 2, 3]  # تعداد ارجاع = 1
y = x          # تعداد ارجاع = 2
z = x          # تعداد ارجاع = 3

del y          # تعداد ارجاع = 2
x = None       # تعداد ارجاع = 1
# وقتی z خارج از حوزه شود، تعداد ارجاع = 0، شی حذف می‌شود
```

### جمع‌آوری زباله
پاک‌سازی خودکار اشیای استفاده نشده:
```python
# ارجاع‌های دایره‌ای توسط جمع‌آور زباله مدیریت می‌شوند
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None

# ایجاد ارجاع دایره‌ای
node1 = Node(1)
node2 = Node(2)
node1.next = node2
node2.next = node1

# بدون جمع‌آور زباله، این حافظه را نشت می‌دهد
del node1
del node2  # اشیا هنوز به هم ارجاع دارند
# جمع‌آور زباله در نهایت پاک‌سازی خواهد کرد
```

## عملیات متغیر

### کپی کردن متغیرها
```python
# کپی سطحی (به همان شی ارجاع می‌دهد)
list1 = [1, 2, 3]
list2 = list1  # هر دو به همان لیست اشاره می‌کنند

list1.append(4)
print(list2)  # [1, 2, 3, 4] - هر دو تغییر کردند!

# کپی عمیق (شی جدید ایجاد می‌کند)
import copy
list3 = copy.deepcopy(list1)  # کپی کاملاً جداگانه ایجاد می‌کند
list1.append(5)
print(list3)  # [1, 2, 3, 4] - بدون تغییر
```

### جابجایی متغیرها
```python
# جابجایی سنتی (نیاز به متغیر temp)
a = 5
b = 10
temp = a
a = b
b = temp

# جابجایی پایتون (باز کردن بسته تاپل)
a = 5
b = 10
a, b = b, a  #优雅!

# جابجایی چندگانه
x, y, z = 1, 2, 3
x, y, z = z, x, y  # چرخش مقادیر
```

## انواع متغیر ویژه

### ثابت‌ها (قرارداد)
```python
# ثابت‌ها فقط متغیر هستند (با قرارداد)
PI = 3.14159
MAX_USERS = 100
DEFAULT_PORT = 8080

# ثابت‌ها را تغییر ندهید
# PI = 3.14  # از نظر فنی مجاز، اما روش بد
```

### متغیرهای خصوصی (قرارداد)
```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance  # متغیر "خصوصی"

    def get_balance(self):
        return self.__balance

# name mangling دسترسی را سخت‌تر می‌کند
account = BankAccount(1000)
# print(account.__balance)  # AttributeError
print(account._BankAccount__balance)  # هنوز قابل دسترسی، اما discouraged
```

## بازرسی و اشکال‌زدایی متغیر

### بازرسی متغیرها
```python
# بررسی نوع متغیر
x = 42
print(type(x))  # <class 'int'>

# بررسی هویت متغیر (آدرس حافظه)
print(id(x))    # شناسه منحصر به فرد

# بررسی اینکه آیا متغیرها به همان شی ارجاع دارند
a = [1, 2, 3]
b = a
c = [1, 2, 3]
print(a is b)   # True (همان شی)
print(a is c)   # False (اشیای مختلف، مقدار یکسان)
```

### بازرسی حوزه متغیر
```python
def test_function():
    local_var = "local"
    print("Local:", local_var)

    # دسترسی به جهانی
    global global_var
    print("Global:", global_var)

global_var = "global"
test_function()
# print(local_var)  # NameError - اینجا قابل دسترسی نیست
```

### استفاده از حافظه
```python
import sys

# بررسی اندازه اشیا
x = 42
print(sys.getsizeof(x))  # اندازه به بایت

y = "hello"
print(sys.getsizeof(y))  # اندازه رشته

z = [1, 2, 3, 4, 5]
print(sys.getsizeof(z))  # اندازه لیست (بدون عناصر)
```

## بهترین روش‌های متغیر

### نام‌گذاری واضح
```python
# از نام‌های توصیفی استفاده کنید
def calculate_total_price(items):
    total = 0
    for item in items:
        total += item.price * item.quantity
    return total

# از حروف تک اجتناب کنید (به جز موارد obvious)
# بد
def calc(t):
    s = 0
    for i in t:
        s += i.p * i.q
    return s
```

### سبک ثابت
```python
# از PEP 8 پیروی کنید
user_name = "Alice"     # snake_case برای متغیرها
UserAccount = "class"   # PascalCase برای کلاس‌ها
MAX_CONNECTIONS = 100   # UPPERCASE برای ثابت‌ها
```

### به حداقل رساندن متغیرهای جهانی
```python
# بد - حالت جهانی
total_sales = 0

def add_sale(amount):
    global total_sales
    total_sales += amount

# بهتر - کپسوله کردن حالت
class SalesTracker:
    def __init__(self):
        self.total_sales = 0

    def add_sale(self, amount):
        self.total_sales += amount

    def get_total(self):
        return self.total_sales
```

### استفاده از پیش‌فرض‌های معنادار
```python
# پیش‌فرض‌های خوب
def connect_database(host="localhost", port=5432, timeout=30):
    # پیاده‌سازی
    pass

# پیش‌فرض‌های بد
def process_data(data=None, flag=True, count=-1):
    # -1 ممکن است با count معتبر اشتباه گرفته شود
    pass
```

## اشتباهات رایج متغیر

### متغیرهای مقداردهی نشده
```python
# خطا
print(unknown_variable)  # NameError

# رفع
unknown_variable = "now defined"
print(unknown_variable)
```

### سایه انداختن متغیر
```python
total = 100

def calculate_total(items):
    total = 0  # سایه انداختن بر متغیر جهانی
    for item in items:
        total += item.price
    return total

print(total)  # هنوز 100 است (جهانی تغییر نکرده)
```

### آرگومان‌های پیش‌فرض قابل تغییر
```python
# مشکل‌دار
def add_item(item, shopping_list=[]):
    shopping_list.append(item)
    return shopping_list

# رفتار غیرمنتظره
list1 = add_item("apple")
list2 = add_item("banana")
print(list1)  # ['apple', 'banana'] - هر دو لیست تحت تأثیر قرار گرفتند!

# رفع
def add_item(item, shopping_list=None):
    if shopping_list is None:
        shopping_list = []
    shopping_list.append(item)
    return shopping_list
```

## نکات کلیدی

۱. **متغیرها ذخیره‌سازی نام‌گذاری شده** برای مقادیر داده‌ای در حافظه هستند
۲. **تایپ پویا** به متغیرها اجازه می‌دهد انواع را تغییر دهند
۳. **حوزه دسترسی** متغیرها را کنترل می‌کند
۴. **قراردادهای نام‌گذاری** خوانایی کد را بهبود می‌بخشند
۵. **مدیریت حافظه** در پایتون خودکار است
۶. **بهترین روش‌ها** اشتباهات رایج را پیشگیری می‌کنند

## مطالعه بیشتر
- مدل داده پایتون و سیستم شی
- حوزه متغیر در زبان‌های مختلف
- تکنیک‌های مدیریت حافظه
- بهترین روش‌ها برای نام‌گذاری و سازماندهی متغیر