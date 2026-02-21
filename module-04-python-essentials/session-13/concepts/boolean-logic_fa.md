# منطق بولی: پایه تصمیم‌گیری

## منطق بولی چیست؟

منطق بولی با مقادیر درست/نادرست و عملیات سروکار دارد. این پایه همه تصمیم‌گیری در برنامه‌نویسی است و به کامپیوترها اجازه می‌دهد بر اساس شرایط انتخاب کنند.

## مقادیر بولی

### True و False
```python
# literals بولی
is_active = True
is_deleted = False

# نوع بولی
print(type(True))    # <class 'bool'>
print(type(False))   # <class 'bool'>
```

### ایجاد بولی از انواع دیگر
```python
# از اعداد
bool(0)        # False
bool(1)        # True
bool(-5)       # True (هر غیرصفر)

# از رشته‌ها
bool("")       # False (رشته خالی)
bool("hello")  # True (رشته غیرخالی)

# از مجموعه‌ها
bool([])       # False (لیست خالی)
bool([1, 2])   # True (لیست غیرخالی)
bool({})       # False (دیکشنری خالی)
bool({1: 2})   # True (دیکشنری غیرخالی)

# از None
bool(None)     # False
```

## عملگرهای منطقی

### عملگر NOT
```python
# مقدار درستی را برعکس می‌کند
not True       # False
not False      # True

# مثال‌های عملی
is_logged_in = False
if not is_logged_in:
    print("Please log in")

# منفی مضاعف
not not True   # True (شایع نیست، اما معتبر)
```

### عملگر AND
```python
# True فقط وقتی که هر دو عملوند True باشند
True and True    # True
True and False   # False
False and True   # False
False and False  # False

# ارزیابی کوتاه‌مدت
def expensive_check():
    print("عملیات گران!")
    return True

# عملوند دوم ارزیابی نمی‌شود اگر اولین False باشد
False and expensive_check()  # چاپ نمی‌کند، False برمی‌گرداند

# عملوند دوم ارزیابی می‌شود اگر اولین True باشد
True and expensive_check()   # چاپ می‌کند، True برمی‌گرداند
```

### عملگر OR
```python
# True اگر حداقل یک عملوند True باشد
True or True     # True
True or False    # True
False or True    # True
False or False   # False

# ارزیابی کوتاه‌مدت
False or expensive_check()   # چاپ می‌کند، True برمی‌گرداند
True or expensive_check()    # چاپ نمی‌کند، True برمی‌گرداند
```

## جداول درستی

### جدول درستی NOT
```
P     | NOT P
------|-------
True  | False
False | True
```

### جدول درستی AND
```
P     | Q     | P AND Q
------|-------|---------
True  | True  | True
True  | False | False
False | True  | False
False | False | False
```

### جدول درستی OR
```
P     | Q     | P OR Q
------|-------|--------
True  | True  | True
True  | False | True
False | True  | True
False | False | False
```

## عملگرهای مقایسه

### برابری و نابرابری
```python
# برابر با
5 == 5        # True
5 == 6        # False
"hello" == "hello"  # True
"hello" == "Hello"  # False (case-sensitive)

# نامساوی با
5 != 6        # True
5 != 5        # False
```

### مقایسه‌های ترتیبی
```python
# بزرگ‌تر از
7 > 5         # True
5 > 7         # False

# کوچک‌تر از
3 < 8         # True
8 < 3         # False

# بزرگ‌تر یا مساوی با
5 >= 5        # True
5 >= 3        # True
3 >= 5        # False

# کوچک‌تر یا مساوی با
4 <= 4        # True
4 <= 6        # True
6 <= 4        # False
```

### مقایسه‌های رشته
```python
# ترتیب lexicographic (لغت‌نامه)
"apple" < "banana"    # True ('a' قبل از 'b')
"Apple" < "apple"     # True (حروف بزرگ قبل از کوچک)
"abc" < "abcd"        # True (کوتاه‌تر قبل از بلندتر)
```

## عملگرهای عضویت

### عملگر in
```python
# بررسی اینکه آیا آیتم در مجموعه وجود دارد
5 in [1, 2, 3, 4, 5]        # True
"apple" in ["apple", "banana"]  # True
"a" in "banana"              # True
"z" in "banana"              # False

# عضویت دیکشنری (کلیدها)
"key" in {"key": "value"}    # True
"value" in {"key": "value"}  # False
```

### عملگر not in
```python
# برعکس in
6 not in [1, 2, 3, 4, 5]    # True
"x" not in "hello"          # True
```

## عملگرهای هویت

### عملگر is
```python
# بررسی اینکه آیا دو متغیر به همان شی ارجاع دارند
a = [1, 2, 3]
b = a
c = [1, 2, 3]

a is b      # True (همان شی)
a is c      # False (اشیای مختلف، محتوای یکسان)

# مهم برای چک کردن None
value = None
value is None     # True (روش درست)
value == None     # True (نیز کار می‌کند، اما 'is' ترجیح داده می‌شود)
```

### عملگر is not
```python
a is not c        # True
value is not None # True
```

## ترکیب عبارت‌های بولی

### شرایط پیچیده
```python
age = 25
is_student = True
has_discount = False

# شرایط AND متعدد
eligible = age >= 18 and is_student and not has_discount

# شرایط OR متعدد
can_enter = age >= 21 or (age >= 18 and not is_student)

# عملگرهای مخلوط
special_offer = (age < 18 or age > 65) and is_student
```

### تقدم عملگر
```python
# NOT > AND > OR
not True and False or True    # ((not True) and False) or True = False

# از پرانتز برای وضوح استفاده کن
(not True) and (False or True)  # False and True = False
```

## قوانین جبر بولی

### قوانین جابجایی
```python
# AND جابجایی است
True and False == False and True    # True

# OR جابجایی است
True or False == False or True      # True
```

### قوانین شرکت‌پذیری
```python
# AND شرکت‌پذیر است
(True and False) and True == True and (False and True)  # هر دو False

# OR شرکت‌پذیر است
(True or False) or True == True or (False or True)      # هر دو True
```

### قوانین توزیع‌پذیری
```python
# AND روی OR توزیع می‌شود
A and (B or C) == (A and B) or (A and C)

# OR روی AND توزیع می‌شود
A or (B and C) == (A or B) and (A or C)
```

### قوانین De Morgan
```python
# not (A and B) == (not A) or (not B)
not (True and False) == (not True) or (not False)  # True == True

# not (A or B) == (not A) and (not B)
not (True or False) == (not True) and (not False)  # False == False
```

## کاربردهای عملی

### احراز هویت کاربر
```python
def can_access_admin(username, is_admin, is_logged_in):
    return is_logged_in and is_admin and username != "guest"

# موارد تست
can_access_admin("alice", True, True)    # True
can_access_admin("bob", False, True)     # False
can_access_admin("guest", True, True)    # False
```

### منطق سبد خرید
```python
def calculate_shipping(cost, is_premium, free_shipping_threshold=50):
    if is_premium or cost >= free_shipping_threshold:
        return 0.0  # ارسال رایگان
    elif cost >= 25:
        return 5.99
    else:
        return 9.99

# سناریوهای مختلف را تست کن
calculate_shipping(60, False, 50)   # 0.0 (فراتر از آستانه)
calculate_shipping(30, True, 50)    # 0.0 (premium)
calculate_shipping(30, False, 50)   # 5.99
calculate_shipping(10, False, 50)   # 9.99
```

### اعتبارسنجی فرم
```python
def validate_registration(name, email, age, agree_to_terms):
    name_valid = bool(name.strip())  # خالی نیست بعد از حذف فضای خالی
    email_valid = "@" in email and "." in email  # چک ایمیل پایه
    age_valid = isinstance(age, int) and 13 <= age <= 120
    agreement_valid = agree_to_terms is True

    all_valid = name_valid and email_valid and age_valid and agreement_valid

    if not all_valid:
        issues = []
        if not name_valid:
            issues.append("Name مورد نیاز است")
        if not email_valid:
            issues.append("ایمیل معتبر مورد نیاز است")
        if not age_valid:
            issues.append("Age باید بین 13 و 120 باشد")
        if not agreement_valid:
            issues.append("باید با شرایط موافقت کنید")
        return False, issues

    return True, []

# اعتبارسنجی را تست کن
valid, errors = validate_registration("Alice", "alice@email.com", 25, True)
print(f"Valid: {valid}")  # True

valid, errors = validate_registration("", "invalid", 10, False)
print(f"Valid: {valid}, Errors: {errors}")
# Valid: False, Errors: ['Name مورد نیاز است', 'ایمیل معتبر مورد نیاز است', 'Age باید بین 13 و 120 باشد', 'باید با شرایط موافقت کنید']
```

## پرچم‌های بولی و حالت

### پرچم‌های وضعیت
```python
class UserAccount:
    def __init__(self, username):
        self.username = username
        self.is_active = True
        self.is_verified = False
        self.is_premium = False

    def can_post(self):
        return self.is_active and self.is_verified

    def can_access_premium(self):
        return self.can_post() and self.is_premium

user = UserAccount("alice")
user.is_verified = True

print(user.can_post())          # True
print(user.can_access_premium()) # False

user.is_premium = True
print(user.can_access_premium()) # True
```

### پرچم‌های تنظیمات
```python
class ApplicationConfig:
    def __init__(self):
        self.debug_mode = False
        self.enable_logging = True
        self.use_cache = True
        self.send_emails = False

    def should_log(self, level):
        return self.enable_logging and (
            self.debug_mode or level in ["ERROR", "WARNING"]
        )

config = ApplicationConfig()
config.debug_mode = True

print(config.should_log("DEBUG"))     # True
print(config.should_log("INFO"))      # False
print(config.should_log("ERROR"))     # True
```

## اشتباهات رایج بولی

### اشتباه گرفتن = با ==
```python
# اشتباه
if x = 5:      # تخصیص، نه مقایسه
    print("Equal")

# درست
if x == 5:
    print("Equal")
```

### چک کردن None نادرست
```python
# کار می‌کند اما ترجیح داده نمی‌شود
if user == None:
    pass

# بهتر - از 'is' استفاده کن
if user is None:
    pass
```

### شرایط بیش از حد پیچیده
```python
# سخت برای درک
if not (not a or not b):
    pass

# ساده‌تر
if a and b:
    pass
```

### مقایسه‌های اعشاری
```python
# مشکل‌دار
if price == 19.99:
    print("Exact match")

# بهتر
if abs(price - 19.99) < 0.01:
    print("Approximately $19.99")
```

## بهینه‌سازی عبارت بولی

### مزایای کوتاه‌مدت
```python
# از عملیات گران اجتناب کن
if user_exists and validate_complex_permissions(user):
    grant_access()

# بهتر از همیشه فراخوانی validate_complex_permissions
```

### ساده‌سازی عبارت بولی
```python
# اصلی
if not (x < 5 or y > 10):
    do_something()

# ساده‌سازی شده با استفاده از قانون De Morgan
if x >= 5 and y <= 10:
    do_something()
```

## نکات کلیدی

۱. **منطق بولی پایه همه تصمیم‌گیری در برنامه‌نویسی است**
۲. **مقادیر True/False** از مقایسه‌ها و تبدیل نوع می‌آیند
۳. **عملگرهای منطقی** (AND، OR، NOT) شرایط را ترکیب می‌کنند
۴. **ارزیابی کوتاه‌مدت** می‌تواند عملکرد را بهبود بخشد
۵. **قوانین جبر بولی** به ساده‌سازی عبارت‌های پیچیده کمک می‌کنند
۶. **منطق بولی واضح** کد را قابل نگهداری‌تر می‌کند

## مطالعه بیشتر
- جبر بولی و منطق دیجیتال
- منطق fuzzy و منطق چندمقداری
- طراحی مدار با گیت‌های منطقی
- تأیید رسمی عبارت‌های بولی