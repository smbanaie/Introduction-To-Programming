# ترتیب ارزیابی و تقدم: پردازش عبارت

## پایتون چگونه عبارت‌ها را ارزیابی می‌کند

درک اینکه پایتون چگونه عبارت‌ها را پردازش می‌کند برای نوشتن کد درست و قابل پیش‌بینی بسیار مهم است. ارزیابی عبارت از قوانین strict تقدم و شرکت‌پذیری پیروی می‌کند.

## سلسله مراتب تقدم عملگر

پایتون عملگرها را به ترتیب خاصی ارزیابی می‌کند، از بالاترین به پایین‌ترین تقدم:

### ۱. پرانتز (گروه‌بندی)
```python
# پرانتز همه تقدم‌های دیگر را نادیده می‌گیرد
result = (2 + 3) * 4     # 20 (جمع اول اتفاق می‌افتد)
result = 2 + (3 * 4)     # 14 (ضرب اول اتفاق می‌افتد)

# پرانتزهای تو در تو
result = ((2 + 3) * 4) - 1  # 19
```

### ۲. فراخوانی تابع و دسترسی به attribute
```python
# فراخوانی تابع تقدم بسیار بالایی دارد
result = len("hello") + 5  # 10 (len("hello") = 5، سپس + 5)

# فراخوانی روش
result = "hello".upper().count('L')  # 2

# دسترسی به attribute
result = math.pi * 2  # ابتدا pi را دسترسی پیدا کن، سپس ضرب کن
```

### ۳. توان
```python
# راست-شرکت‌پذیر
result = 2 ** 3 ** 2      # 512 (2^(3^2) = 2^9 = 512)
result = (2 ** 3) ** 2    # 64 (8^2 = 64)

# مخلوط با عملگرهای دیگر
result = 2 * 3 ** 2       # 18 (3^2 = 9، سپس 2*9)
```

### ۴. عملگرهای unary
```python
# مثبت، منفی، بیتی NOT
result = -2 ** 2          # -4 (نه (-2)**2)
result = -(2 ** 2)        # -4 (همان بالا)
result = ~5 + 3           # -3 (بیتی NOT اول، سپس جمع)

# منطقی NOT
result = not True or False  # False (not اول، سپس or)
```

### ۵. ضرب، تقسیم، modulo
```python
# چپ-شرکت‌پذیر، سطح تقدم یکسان
result = 10 * 2 / 5       # 4.0 (10*2=20، 20/5=4.0)
result = 10 / 2 * 5       # 25.0 (10/2=5.0، 5.0*5=25.0)

# تقسیم صحیح و modulo
result = 17 // 3 % 2      # 1 ((17//3)=5، 5%2=1)
```

### ۶. جمع و تفریق
```python
# چپ-شرکت‌پذیر
result = 10 - 5 + 2       # 7 ((10-5)=5، 5+2=7)
result = 10 + 5 - 2       # 13 ((10+5)=15، 15-2=13)
```

### ۷. شیفت‌های بیتی
```python
# شیفت چپ و راست
result = 8 >> 1 + 1       # 2 (1+1=2، سپس 8>>2)
result = (8 >> 1) + 1     # 5 (8>>1=4، 4+1=5)
```

### ۸. بیتی AND
```python
result = 5 & 3 | 2        # 2 ((5&3)=1، 1|2=2)
```

### ۹. بیتی XOR
```python
result = 5 ^ 3 | 2        # 7 ((5^3)=6، 6|2=7)
```

### ۱۰. بیتی OR
```python
result = 5 | 3 & 2        # 7 ((3&2)=2، 5|2=7)
```

### ۱۱. عملگرهای مقایسه
```python
# همه تقدم یکسانی دارند، چپ-شرکت‌پذیر
result = 5 < 10 == True   # False ((5<10)=True، True==True، اما زنجیر شده متفاوت)

result = 5 < 10 and 10 == 10  # True (مقایسه قبل از منطقی)
```

### ۱۲. عملگرهای هویت (is, is not)
```python
# بعد از مقایسه‌ها
result = x is None or x == 0  # ابتدا هویت را چک کن
```

### ۱۳. عملگرهای عضویت (in, not in)
```python
result = x in [1, 2, 3] and x > 0
```

### ۱۴. منطقی NOT
```python
result = not x > 5 and y < 10
```

### ۱۵. منطقی AND
```python
result = x > 5 and y < 10 or z == 0
```

### ۱۶. منطقی OR
```python
result = x or y and z  # معادل x or (y and z)
```

## قوانین شرکت‌پذیری

### عملگرهای چپ-شرکت‌پذیر
اکثر عملگرها از چپ به راست گروه‌بندی می‌شوند:
```python
# جمع/تفریق
result = 10 - 5 - 2     # (10 - 5) - 2 = 3

# ضرب/تقسیم
result = 10 / 2 * 5     # (10 / 2) * 5 = 25.0

# مقایسه‌ها (زنجیر شده)
result = 1 < 2 < 3      # (1 < 2) and (2 < 3) = True
```

### عملگرهای راست-شرکت‌پذیر
تعداد کمی از عملگرها از راست به چپ گروه‌بندی می‌شوند:
```python
# توان
result = 2 ** 3 ** 2    # 2 ** (3 ** 2) = 512

# عملگرهای تخصیص
x = y = z = 5          # z = 5، سپس y = z، سپس x = y
```

## ارزیابی کوتاه‌مدت

### عملگرهای منطقی
پایتون ارزیابی را متوقف می‌کند به محض اینکه نتیجه مشخص شود:

```python
# AND: در اولین False متوقف می‌شود
def expensive_check():
    print("عملیات گران!")
    return True

result = False and expensive_check()  # expensive_check() را فراخوانی نمی‌کند
result = True and expensive_check()   # expensive_check() را فراخوانی می‌کند

# OR: در اولین True متوقف می‌شود
result = True or expensive_check()    # expensive_check() را فراخوانی نمی‌کند
result = False or expensive_check()   # expensive_check() را فراخوانی می‌کند
```

### کاربردهای عملی
```python
# تقسیم امن
def safe_divide(a, b):
    return b != 0 and a / b

result = safe_divide(10, 0)   # False (بدون تقسیم بر صفر)
result = safe_divide(10, 2)   # 5.0

# دسترسی امن به attribute
user = None
name = user and user.name  # None (.name را روی None دسترسی پیدا نمی‌کند)
```

## زمینه ارزیابی

### ارزیابی Eager در برابر Lazy
```python
# پایتون از ارزیابی eager استفاده می‌کند (همه آرگومان‌ها را ارزیابی می‌کند)
def add(a, b):
    return a + b

result = add(2 * 3, 4 + 5)  # 6 و 9 را ارزیابی می‌کند، سپس جمع می‌کند

# اما عملگرهای منطقی lazy هستند
result = True or expensive_function()  # expensive_function فراخوانی نمی‌شود
```

### list comprehensions
```python
# همه عبارت‌ها به طور eager ارزیابی می‌شوند
squares = [x**2 for x in range(1, 6)]  # [1, 4, 9, 16, 25]

# generator expressions (lazy)
squares_gen = (x**2 for x in range(1, 6))  # هنوز ارزیابی نشده
list(squares_gen)  # [1, 4, 9, 16, 25] - اکنون ارزیابی می‌شود
```

## اشتباهات رایج تقدم

### عبارت‌های ریاضی
```python
# اشتباه رایج
result = 3 + 4 * 2     # 11 (نه 14)
# درک درست
result = 3 + (4 * 2)   # 11

# اشتباه دیگر
result = 10 / 2 * 3    # 15.0 (نه 1.666...)
# درست: (10 / 2) * 3 = 15.0
```

### زنجیر مقایسه‌ها
```python
# رفتار غیرمنتظره
result = 5 < 10 == True  # False!
# چون: (5 < 10) == True → True == True → True
# اما زنجیر شده به صورت: 5 < 10 and 10 == True → False

# روش درست
result = 5 < 10 and 10 == 10  # True
```

### عملگرهای بیتی و منطقی
```python
# بیتی تقدم بالاتری نسبت به مقایسه دارد
result = x & y == 0     # (x & y) == 0
result = x & (y == 0)   # معمولاً چیزی که نمی‌خواهی

# منطقی AND تقدم پایین‌تری نسبت به مقایسه دارد
result = x > 5 and y < 10  # درست
result = x > 5 & y < 10    # بیتی AND! احتمالاً اشتباه
```

## بهترین روش‌ها برای وضوح عبارت

### از پرانتز برای وضوح استفاده کن
```python
# قصد واضح
if (age >= 18) and (has_license or has_permit):
    can_drive = True

# نامشخص (اما معادل)
if age >= 18 and has_license or has_permit:
    can_drive = True  # اشتباه! OR تقدم پایین‌تری دارد
```

### عبارت‌های پیچیده را تقسیم کن
```python
# سخت برای خواندن
if x > 0 and y > 0 and z > 0 and x + y + z < 100:

# بهتر
coordinates_valid = x > 0 and y > 0 and z > 0
sum_valid = x + y + z < 100
if coordinates_valid and sum_valid:
```

### از عبارت‌های بیش از حد پیچیده اجتناب کن
```python
# بیش از حد پیچیده - سخت برای debug
result = (a if condition1 else b) + (c if condition2 else d) * (e if condition3 else f)

# بهتر - از متغیرهای میانی استفاده کن
first_value = a if condition1 else b
second_value = c if condition2 else d
third_value = e if condition3 else f
result = first_value + second_value * third_value
```

## تأثیرات عملکرد

### بهینه‌سازی عبارت
```python
# پایتون برخی عبارت‌ها را در زمان کامپایل بهینه‌سازی می‌کند
x = 2 + 3  # constant folding: تبدیل به 5 می‌شود

# اما عبارت‌های پویا در زمان اجرا ارزیابی می‌شوند
x = a + b  # هر بار ارزیابی می‌شود
```

### مزایای کوتاه‌مدت
```python
# از عملیات گران اجتناب کن
if user_exists and validate_user_permissions(user):
    grant_access()

# بهتر از
if user_exists:
    if validate_user_permissions(user):
        grant_access()
```

## اشکال‌زدایی ارزیابی عبارت

### اشکال‌زدایی print
```python
# عبارت‌های پیچیده را debug کن
x, y, z = 5, 10, 15
result = x + y * z / 2

# debug print اضافه کن
print(f"x = {x}, y = {y}, z = {z}")
print(f"y * z = {y * z}")
print(f"(y * z) / 2 = {(y * z) / 2}")
print(f"x + ((y * z) / 2) = {result}")
```

### استفاده از AST پایتون
```python
import ast

# عبارت را برای دیدن ساختار parse کن
expression = "x + y * z / 2"
tree = ast.parse(expression, mode='eval')
print(ast.dump(tree, indent=2))
```

## نکات کلیدی

۱. **تقدم ترتیب ارزیابی را تعیین می‌کند** - عملگرهای تقدم بالاتر اول
۲. **شرکت‌پذیری** عملگرهای تقدم یکسان را حل می‌کند (معمولاً چپ به راست)
۳. **پرانتز تقدم را نادیده می‌گیرد** - برای وضوح استفاده کن
۴. **ارزیابی کوتاه‌مدت** می‌تواند عملکرد را بهبود بخشد
۵. **عبارت‌های پیچیده** باید برای خوانایی تقسیم شوند

## مطالعه بیشتر
- مرجع زبان پایتون درباره عبارت‌ها
- تکنیک‌های بهینه‌سازی کامپایلر
- استراتژی‌های ارزیابی برنامه‌نویسی تابعی
- تجزیه عبارت و abstract syntax trees