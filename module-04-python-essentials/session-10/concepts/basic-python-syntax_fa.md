# نحو پایه پایتون: نوشتن اولین کد شما

## اصول نحو پایتون

نحو پایتون برای خوانا و بصری بودن طراحی شده است. از کلمات کلیدی شبیه به انگلیسی استفاده می‌کند و به جای braces یا semicolons به تورفتگی اعتماد دارد.

## ساختار برنامه پایه

### برنامه Hello World
```python
# این یک کامنت است - توسط پایتون نادیده گرفته می‌شود
print("Hello, World!")
```

**خروجی:**
```
Hello, World!
```

### برنامه چند خطی
```python
# برنامه برای سلام به کاربر
name = input("What's your name? ")
print("Hello, " + name + "!")
print("Welcome to Python programming!")
```

## دستورات و عبارات

### دستورات
دستورات دستورالعمل‌های کاملی هستند که اقدامات را انجام می‌دهند:
```python
# دستور انتساب
x = 5

# دستور فراخوانی تابع
print("Hello")

# دستور جریان کنترل
if x > 3:
    print("Big number")
```

### عبارات
عبارات به مقادیر ارزیابی می‌شوند:
```python
# عبارت حسابی
result = 2 + 3 * 4

# عبارت فراخوانی تابع
length = len("hello")

# عبارت مقایسه
is_large = x > 10
```

## متغیرها و انتساب

### نام متغیرها
```python
# نام‌های معتبر
my_variable = 5
user_name = "Alice"
total_count = 100
is_active = True

# نام‌های نامعتبر (خطا ایجاد می‌کنند)
# 2variable = 5      # نمی‌تواند با عدد شروع شود
# my-variable = 10   # بدون خط تیره
# class = "Python"   # کلمه کلیدی رزرو شده
```

### عملگرهای انتساب
```python
# انتساب پایه
x = 5

# انتساب ترکیبی
x += 3    # x = x + 3
x -= 2    # x = x - 2
x *= 4    # x = x * 4
x /= 2    # x = x / 2
x %= 3    # x = x % 3
```

## انواع داده و literals

### اعداد
```python
# اعداد صحیح
age = 25
year = 2024

# اعداد اعشاری
pi = 3.14159
price = 19.99

# نماد علمی
avogadro = 6.022e23
microsecond = 1e-6
```

### رشته‌ها
```python
# گیومه تکی
name = 'Alice'

# گیومه دوتایی
message = "Hello, World!"

# رشته‌های چند خطی
poem = """Roses are red
Violets are blue"""

# دنباله‌های escape
path = "C:\\Users\\file.txt"
quote = "He said \"Hello\""
newline = "Line 1\nLine 2"
```

### بولی‌ها
```python
# مقادیر بولی
is_student = True
has_license = False

# عبارات بولی
is_adult = age >= 18
is_even = number % 2 == 0
```

## عملیات پایه

### عملگرهای حسابی
```python
# جمع
sum = 5 + 3  # 8

# تفریق
diff = 10 - 4  # 6

# ضرب
product = 6 * 7  # 42

# تقسیم
quotient = 15 / 4  # 3.75

# تقسیم صحیح
whole = 15 // 4  # 3

# مدول (باقی‌مانده)
remainder = 15 % 4  # 3

# توان
power = 2 ** 3  # 8
```

### عملگرهای مقایسه
```python
# برابر با
x == y

# نامساوی با
x != y

# بزرگ‌تر از
x > y

# کوچک‌تر از
x < y

# بزرگ‌تر یا مساوی با
x >= y

# کوچک‌تر یا مساوی با
x <= y
```

### عملگرهای منطقی
```python
# AND - هر دو باید درست باشند
is_adult = age >= 18 and has_id

# OR - حداقل یکی باید درست باشد
can_enter = is_member or has_ticket

# NOT - مقدار درستی را برعکس می‌کند
is_minor = not is_adult
```

## جریان کنترل

### دستورات شرطی
```python
# if ساده
if age >= 18:
    print("You can vote")

# if-else
if temperature > 30:
    print("It's hot!")
else:
    print("It's not too hot")

# if-elif-else
if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
else:
    grade = "F"
```

### حلقه‌ها
```python
# حلقه while
count = 1
while count <= 5:
    print(count)
    count += 1

# حلقه for با range
for i in range(1, 6):
    print(i)

# حلقه for با لیست
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)
```

## توابع

### تعریف توابع
```python
def greet_user(name):
    """This function greets a user by name."""
    message = "Hello, " + name + "!"
    return message

# فراخوانی توابع
result = greet_user("Alice")
print(result)  # "Hello, Alice!"
```

### تابع با پارامترهای متعدد
```python
def calculate_area(length, width):
    """Calculate rectangle area."""
    area = length * width
    return area

# فراخوانی با آرگومان‌های موقعیتی
result = calculate_area(5, 3)  # 15

# فراخوانی با آرگومان‌های کلیدواژه
result = calculate_area(length=5, width=3)  # 15
```

## کامنت‌ها و مستندسازی

### کامنت‌های تک خطی
```python
# این یک کامنت است
x = 5  # این عدد ۵ را به x منتسب می‌کند
```

### کامنت‌های چند خطی
```python
"""
این یک کامنت چند خطی است
می‌تواند چندین خط را پوشش دهد
برای مستندسازی تابع استفاده می‌شود
"""

# یا استفاده از کامنت‌های تک خطی متعدد
# این تابع مساحت را محاسبه می‌کند
# مستطیل
def calculate_area(length, width):
    return length * width
```

### Docstringها
```python
def calculate_average(numbers):
    """
    میانگین حسابی لیستی از اعداد را محاسبه می‌کند.

    Args:
        numbers (list): لیستی از مقادیر عددی

    Returns:
        float: مقدار میانگین

    Example:
        >>> calculate_average([1, 2, 3, 4, 5])
        3.0
    """
    if not numbers:
        return 0
    return sum(numbers) / len(numbers)
```

## ورودی و خروجی

### خروجی کنسول
```python
# print ساده
print("Hello")

# print آیتم‌های متعدد
print("Name:", name, "Age:", age)

# خروجی فرمت شده
print(f"My name is {name} and I'm {age} years old")
print("Value: {:.2f}".format(3.14159))
```

### ورودی کنسول
```python
# دریافت ورودی رشته
name = input("Enter your name: ")

# دریافت ورودی عددی (با تبدیل)
age = int(input("Enter your age: "))
height = float(input("Enter your height: "))

# مدیریت خطاهای ورودی
try:
    number = int(input("Enter a number: "))
except ValueError:
    print("That's not a valid number!")
```

## خطاهای نحوی رایج

### خطاهای تورفتگی
```python
# اشتباه - تورفتگی ناسازگار
if x > 5:
    print("Big")
   print("This will cause IndentationError")

# درست
if x > 5:
    print("Big")
    print("This is fine")
```

### دو نقطه گمشده
```python
# اشتباه
if x > 5
    print("Big")  # SyntaxError

# درست
if x > 5:
    print("Big")
```

### عدم تطابق گیومه‌ها
```python
# اشتباه
message = "Hello, world!  # SyntaxError

# اشتباه
message = 'Hello, world!"  # SyntaxError

# درست
message = "Hello, world!"
message = 'Hello, world!'
```

## سبک کد و بهترین روش‌ها

### دستورالعمل‌های PEP 8
```python
# نام متغیرهای خوب
user_name = "Alice"
total_count = 10
is_valid = True

# فاصله‌گذاری ثابت
x = 1 + 2
y = x * 3

# طول خط (حداکثر ۷۹ کاراکتر)
# شکستن خطوط طولانی
result = some_function(argument1, argument2,
                      argument3, argument4)
```

### خوانایی
```python
# سخت برای خواندن
x=1+2;y=x*3;z=y-1

# آسان برای خواندن
x = 1 + 2
y = x * 3
z = y - 1
```

### نام‌های معنادار
```python
# از حروف تک (به جز در حلقه‌ها) اجتناب کنید
# بد
a = calculate_average(scores)
b = find_maximum(values)

# خوب
average_score = calculate_average(scores)
highest_value = find_maximum(values)
```

## اجرای برنامه‌های پایتون

### از خط فرمان
```bash
# اجرای اسکریپت
python3 my_program.py

# اجرای با آرگومان‌ها
python3 script.py arg1 arg2

# دسترسی به آرگومان‌های خط فرمان
import sys
print("Arguments:", sys.argv)
```

### Shebang برای سیستم‌های Unix-like
```python
#!/usr/bin/env python3
# این به سیستم می‌گوید از پایتون ۳ استفاده کند

print("This script can be run directly!")
```

### اجرای مستقیم اسکریپت‌ها
```bash
# اضافه کردن مجوز اجرا
chmod +x my_script.py

# اجرای مستقیم
./my_script.py
```

## نکات کلیدی

۱. **تورفتگی مهم است**: پایتون از تورفتگی برای تعریف بلوک‌های کد استفاده می‌کند
۲. **semicolon نیاز نیست**: دستورات با خط جدید پایان می‌یابند
۳. **تایپ پویا**: متغیرها نیازی به اعلان نوع ندارند
۴. **نحو خوانا**: پایتون بر خوانایی انسانی تأکید دارد
۵. **باتری شامل است**: کتابخانه استاندارد غنی داخلی

## مطالعه بیشتر
- راهنمای سبک PEP 8 (python.org/dev/peps/pep-0008/)
- مرجع زبان پایتون
- مشکلات رایج پایتون و تله‌ها
- بهترین روش‌ها برای توسعه پایتون