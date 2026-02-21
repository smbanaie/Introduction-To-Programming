# عبارت‌ها و عملگرها: ساخت محاسبات

## عبارت‌ها چیستند؟

عبارت‌ها ترکیب‌هایی از مقادیر، متغیرها و عملگرها هستند که پایتون آن‌ها را ارزیابی می‌کند تا نتیجه‌ای تولید شود. آنها بلوک‌های سازنده محاسبات در برنامه‌نویسی هستند.

## عملگرهای حسابی

### عملیات ریاضی پایه
```python
# جمع
result = 5 + 3  # 8

# تفریق
result = 10 - 4  # 6

# ضرب
result = 6 * 7   # 42

# تقسیم (اعشاری)
result = 15 / 4  # 3.75

# تقسیم صحیح (تقسیم floor)
result = 15 // 4 # 3

# modulo (باقیمانده)
result = 15 % 4  # 3

# توان
result = 2 ** 3  # 8
result = 2 ** 0.5  # 1.4142135623730951 (ریشه دوم)
```

### تقدم عملگر
پایتون از ترتیب عملیات ریاضی پیروی می‌کند:

```python
# PEMDAS: پرانتز، توان، ضرب/تقسیم، جمع/تفریق
result = 2 + 3 * 4       # 14 (ضرب اول)
result = (2 + 3) * 4     # 20 (پرانتز جمع را اول می‌کند)
result = 2 ** 3 * 2      # 16 (توان قبل از ضرب)
result = 10 - 5 + 2      # 7 (چپ به راست برای تقدم یکسان)
```

### عملگرهای تخصیص افزوده
```python
x = 5

x += 3   # x = x + 3 → 8
x -= 2   # x = x - 2 → 6
x *= 4   # x = x * 4 → 24
x /= 2   # x = x / 2 → 12.0
x //= 3  # x = x // 3 → 4.0
x %= 3   # x = x % 3 → 1.0
x **= 2  # x = x ** 2 → 1.0
```

## عملگرهای مقایسه

### مقایسه‌های پایه
```python
# برابر با
result = 5 == 5      # True
result = 5 == 6      # False

# نامساوی با
result = 5 != 6      # True
result = 5 != 5      # False

# بزرگ‌تر از
result = 7 > 5       # True
result = 5 > 7       # False

# کوچک‌تر از
result = 3 < 8       # True
result = 8 < 3       # False

# بزرگ‌تر یا مساوی با
result = 5 >= 5      # True
result = 5 >= 3      # True

# کوچک‌تر یا مساوی با
result = 4 <= 4      # True
result = 4 <= 6      # True
```

### مقایسه‌های رشته
```python
# مقایسه lexicographic (ترتیب لغت‌نامه)
result = "apple" < "banana"    # True ('a' قبل از 'b' می‌آید)
result = "Apple" < "apple"     # True (حروف بزرگ قبل از کوچک)
result = "apple" == "Apple"    # False (case-sensitive)
```

### زنجیر کردن مقایسه‌ها
```python
# مقایسه‌های متعدد
x = 5
result = 3 < x < 10   # True (معادل 3 < x and x < 10)
result = x < 10 > 7   # True (معادل x < 10 and 10 > 7)

# زنجیرهای پیچیده‌تر
age = 25
result = 18 <= age <= 65  # True (سن کاری معتبر)
```

## عملگرهای منطقی

### منطق بولی
```python
# AND: هر دو شرط باید درست باشند
result = True and True    # True
result = True and False   # False
result = (5 > 3) and (10 < 20)  # True

# OR: حداقل یک شرط باید درست باشد
result = True or False    # True
result = False or False   # False
result = (5 < 3) or (10 > 5)  # True

# NOT: مقدار درستی را برعکس می‌کند
result = not True         # False
result = not False        # True
result = not (5 > 3)      # False
```

### ارزیابی کوتاه‌مدت
پایتون ارزیابی را متوقف می‌کند به محض اینکه نتیجه مشخص شود:

```python
# کوتاه‌مدت AND
def check_condition():
    print("Checking condition...")
    return True

# اگر قسمت اول False باشد، قسمت دوم ارزیابی نمی‌شود
result = False and check_condition()  # "Checking condition..." را چاپ نمی‌کند

# کوتاه‌مدت OR
result = True or check_condition()    # "Checking condition..." را چاپ نمی‌کند
```

### عبارت‌های منطقی پیچیده
```python
# اعتبارسنجی کاربر
age = 25
has_id = True
is_student = False

# شرط پیچیده با پرانتز
can_enter = (age >= 18 and has_id) or is_student
print(can_enter)  # True

# شرایط تو در تو
is_eligible = age >= 18 and (has_id or is_student)
print(is_eligible)  # True
```

## عملگرهای بیتی

### عملیات باینری
```python
# AND (&): 1 فقط جایی که هر دو بیت 1 هستند
result = 5 & 3   # 1 (باینری: 101 & 011 = 001)

# OR (|): 1 جایی که هر بیت 1 است
result = 5 | 3   # 7 (باینری: 101 | 011 = 111)

# XOR (^): 1 جایی که بیت‌ها متفاوت هستند
result = 5 ^ 3   # 6 (باینری: 101 ^ 011 = 110)

# NOT (~): همه بیت‌ها را برعکس کن
result = ~5      # -6 (مکمل دو)

# شیفت چپ (<<): بیت‌ها را به چپ حرکت بده
result = 5 << 1  # 10 (باینری: 101 → 1010)

# شیفت راست (>>): بیت‌ها را به راست حرکت بده
result = 10 >> 1 # 5 (باینری: 1010 → 101)
```

### کاربردهای عملی بیتی
```python
# بررسی اینکه آیا عدد زوج است
is_even = (number & 1) == 0

# بررسی اینکه آیا عدد توان ۲ است
is_power_of_2 = (number & (number - 1)) == 0 and number > 0

# استخراج بیت‌های فردی
bit_0 = number & 1
bit_1 = (number >> 1) & 1
bit_2 = (number >> 2) & 1
```

## عملگرهای عضویت و هویت

### عملگرهای عضویت
```python
# in: بررسی اینکه آیا مقدار در مجموعه وجود دارد
result = 5 in [1, 2, 3, 4, 5]        # True
result = "a" in "banana"              # True
result = "z" in "banana"              # False
result = "key" in {"key": "value"}    # True (کلیدها را چک می‌کند)

# not in: برعکس in
result = 6 not in [1, 2, 3, 4, 5]    # True
```

### عملگرهای هویت
```python
# is: بررسی اینکه آیا دو متغیر به همان شی ارجاع دارند
a = [1, 2, 3]
b = a
c = [1, 2, 3]

result = a is b     # True (همان شی)
result = a is c     # False (اشیای مختلف، محتوای یکسان)

# is not: برعکس is
result = a is not c # True

# مهم: از == با None استفاده نکن، از is استفاده کن
result = None is None     # True
result = value is None    # روش درست برای چک کردن None
```

## ترتیب ارزیابی عبارت

### جدول تقدم کامل
از بالاترین به پایین‌ترین تقدم:

```python
# ۱. پرانتز
result = (2 + 3) * 4   # 20

# ۲. توان
result = 2 ** 3 ** 2   # 512 (راست به چپ)

# ۳. عملگرهای unary (+, -, ~)
result = -2 ** 2       # -4 (نه (-2)**2)

# ۴. ضرب، تقسیم، modulo
result = 10 * 2 + 5    # 25 (نه 10*(2+5))

# ۵. جمع، تفریق
result = 10 + 5 * 2    # 20

# ۶. شیفت‌های بیتی
result = 1 << 2 + 1    # 8 (1 << (2 + 1))

# ۷. بیتی AND
result = 5 & 3 | 2     # 2 ((5 & 3) | 2)

# ۸. بیتی XOR
# ۹. بیتی OR

# ۱۰. عملگرهای مقایسه
result = 5 < 10 == True  # False ((5 < 10) == True)

# ۱۱. عملگرهای هویت (is, is not)

# ۱۲. عملگرهای عضویت (in, not in)

# ۱۳. منطقی NOT

# ۱۴. منطقی AND

# ۱۵. منطقی OR
```

### شرکت‌پذیری
```python
# چپ-شرکت‌پذیر (اکثر عملگرها)
result = 10 - 5 - 2   # (10 - 5) - 2 = 3

# راست-شرکت‌پذیر (توان، تخصیص)
result = 2 ** 3 ** 2  # 2 ** (3 ** 2) = 512
x = y = z = 5        # همه متغیرها 5 می‌شوند
```

## عبارت‌های شرطی

### عملگر سه‌گانه
```python
# condition ? true_value : false_value (زبان‌های دیگر)
# نحو پایتون: true_value if condition else false_value

age = 25
status = "adult" if age >= 18 else "minor"
print(status)  # "adult"

# مثال پیچیده‌تر
x = 10
y = 20
maximum = x if x > y else y
print(maximum)  # 20

# سه‌گانه تو در تو
score = 85
grade = "A" if score >= 90 else ("B" if score >= 80 else "C")
print(grade)  # "B"
```

## عبارت‌های lambda

### توابع ناشناس
```python
# تابع عادی
def add(x, y):
    return x + y

# معادل lambda
add_lambda = lambda x, y: x + y

# استفاده
result = add_lambda(3, 5)  # 8

# موارد استفاده رایج
numbers = [1, 2, 3, 4, 5]

# مرتب‌سازی بر اساس کلید سفارشی
sorted_numbers = sorted(numbers, key=lambda x: -x)  # [5, 4, 3, 2, 1]

# فیلتر با شرط
even_numbers = list(filter(lambda x: x % 2 == 0, numbers))  # [2, 4]

# تبدیل عناصر
squared = list(map(lambda x: x ** 2, numbers))  # [1, 4, 9, 16, 25]
```

## بهترین روش‌های عبارت

### خوانایی
```python
# واضح و قابل خواندن
if age >= 18 and has_license:
    can_drive = True

# کمتر قابل خواندن (اما معادل)
can_drive = age >= 18 and has_license

# حتی کمتر قابل خواندن
can_drive = 18 <= age and has_license
```

### اجتناب از اشتباهات رایج
```python
# اشتباه: تخصیص به جای مقایسه
if x = 5:  # SyntaxError در پایتون (برخلاف C/C++)
    print("This won't work")

# درست
if x == 5:
    print("Equal to 5")

# مراقب اعشاری باش
if abs(a - b) < 0.0001:  # از epsilon برای مقایسه float استفاده کن
    print("Approximately equal")

# چک کردن None
if value is None:  # از 'is' برای None استفاده کن
    print("No value")
```

### عبارت‌های پیچیده
```python
# عبارت‌های پیچیده را به قسمت‌ها تقسیم کن
is_valid_user = (
    user is not None and
    user.age >= 18 and
    user.is_active and
    user.email_verified
)

# یا از متغیرهای میانی استفاده کن
user_exists = user is not None
is_adult = user.age >= 18 if user_exists else False
is_active = user.is_active if user_exists else False
is_verified = user.email_verified if user_exists else False

is_valid_user = user_exists and is_adult and is_active and is_verified
```

## ملاحظات عملکرد

### مزایای ارزیابی کوتاه‌مدت
```python
# از عملیات گران هنگامی که ممکن است اجتناب کن
if user_exists and user_has_permission():  # اگر کاربر وجود ندارد، تابع دوم فراخوانی نمی‌شود
    perform_action()
```

### بهینه‌سازی عبارت
```python
# پایتون برخی عبارت‌ها را بهینه‌سازی می‌کند
x = 5
y = x * 2 + 10  # به طور کارآمد محاسبه می‌شود

# اما زود هنگام بیش از حد بهینه‌سازی نکن
# کد قابل خواندن بهتر از کد micro-optimized است
```

## نکات کلیدی

۱. **عبارت‌ها مقادیر و عملگرها را ترکیب می‌کنند** تا نتایج تولید شود
۲. **تقدم عملگر** ترتیب ارزیابی را تعیین می‌کند
۳. **عملگرهای منطقی** شرایط پیچیده را ممکن می‌کنند
۴. **عملگرهای مقایسه** با انواع داده مختلف کار می‌کنند
۵. **عملگرهای بیتی** نمایش‌های باینری را دستکاری می‌کنند
۶. **وضوح اهمیت دارد** بیش از عبارت‌های clever

## مطالعه بیشتر
- مستندات تقدم عملگر پایتون
- منطق بولی و جداول درستی
- تکنیک‌های دستکاری بیت
- برنامه‌نویسی تابعی با عبارت‌های lambda
- استراتژی‌های بهینه‌سازی عبارت