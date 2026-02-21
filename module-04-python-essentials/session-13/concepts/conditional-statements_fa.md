# دستورات شرطی تو پایتون: تصمیم‌گیری تو کد

## مقدمه تصمیم‌گیری

دستورات شرطی به برنامه‌ها اجازه می‌دن مسیرهای کد مختلفی رو بر اساس شرایط اجرا کنن. آنها برنامه‌ها رو هوشمند و responsive به موقعیت‌های مختلف می‌کنن.

## دستور if

### دستور if پایه
```python
# شرط ساده
age = 18
if age >= 18:
    print("You can vote!")
    print("You are an adult.")

print("This always executes")  # تورفتگی ندارد
```

### دستور if-else
```python
temperature = 25

if temperature > 30:
    print("It's hot!")
    print("Stay hydrated.")
else:
    print("It's not too hot.")
    print("Enjoy the weather.")
```

### زنجیره if-elif-else
```python
score = 85

if score >= 90:
    grade = "A"
    message = "Excellent work!"
elif score >= 80:
    grade = "B"
    message = "Good job!"
elif score >= 70:
    grade = "C"
    message = "Fair performance."
elif score >= 60:
    grade = "D"
    message = "Needs improvement."
else:
    grade = "F"
    message = "Failed."

print(f"Grade: {grade} - {message}")
```

## مقادیر truthy و falsy

### آنچه پایتون درست/نادرست در نظر می‌گیرد
```python
# مقادیر truthy
if 5:                    # اعداد غیرصفر
    print("5 is truthy")

if "hello":              # رشته‌های غیرخالی
    print("Non-empty string is truthy")

if [1, 2, 3]:           # مجموعه‌های غیرخالی
    print("Non-empty list is truthy")

if {"key": "value"}:     # دیکشنری غیرخالی
    print("Non-empty dict is truthy")

# مقادیر falsy
if not 0:               # صفر
    print("0 is falsy")

if not "":              # رشته خالی
    print("Empty string is falsy")

if not []:              # لیست خالی
    print("Empty list is falsy")

if not {}:              # دیکشنری خالی
    print("Empty dict is falsy")

if not None:            # None
    print("None is falsy")
```

### کاربردهای عملی
```python
# بررسی اینکه آیا متغیر مقدار دارد
name = input("Enter your name: ")
if name:  # رشته خالی falsy است
    print(f"Hello, {name}!")
else:
    print("You didn't enter a name.")

# بررسی اینکه آیا لیست آیتم دارد
shopping_list = []
if shopping_list:
    print("You have items to buy.")
else:
    print("Your shopping list is empty.")
```

## عملگرهای مقایسه در شرط‌ها

### مقایسه‌های عددی
```python
x = 10
y = 20

if x < y:
    print("x is less than y")

if x != y:
    print("x is not equal to y")

if x <= 10:
    print("x is 10 or less")
```

### مقایسه‌های رشته
```python
name = "Alice"

if name == "Alice":
    print("Hello, Alice!")

if name.lower() == "alice":  # case-insensitive
    print("Hello, alice!")

if len(name) > 3:
    print("Long name")
```

### تست‌های عضویت
```python
fruits = ["apple", "banana", "cherry"]

if "apple" in fruits:
    print("Apple is in the list")

if "grape" not in fruits:
    print("Grape is not in the list")

# عضویت رشته
message = "Hello, World!"
if "World" in message:
    print("Found 'World' in message")
```

## عملگرهای منطقی در شرط‌ها

### شرط‌های AND
```python
age = 25
has_license = True

if age >= 18 and has_license:
    print("You can drive!")
else:
    print("You cannot drive.")

# شرط‌های AND متعدد
if age >= 18 and has_license and age <= 80:
    print("You are eligible to drive.")
```

### شرط‌های OR
```python
day = "Saturday"

if day == "Saturday" or day == "Sunday":
    print("It's weekend!")
else:
    print("It's a weekday.")

# شرط‌های OR متعدد
if day in ["Saturday", "Sunday", "Friday"]:
    print("Almost weekend or weekend!")
```

### شرط‌های NOT
```python
is_raining = False

if not is_raining:
    print("No umbrella needed.")
else:
    print("Take an umbrella!")

# شرط‌های NOT پیچیده
user = None
if not user:
    print("Please log in.")
```

### ترکیب عملگرهای منطقی
```python
age = 25
is_student = True
has_discount = False

# شرط پیچیده
if (age < 18 or age > 65) and is_student:
    print("Student discount available")
elif has_discount or age > 60:
    print("Senior discount available")
else:
    print("Full price")
```

## دستورات شرطی تو در تو

### تو در تو پایه
```python
age = 20
has_id = True

if age >= 18:
    if has_id:
        print("You can enter the club.")
    else:
        print("You need ID to enter.")
else:
    print("You are too young to enter.")
```

### سطوح متعدد تو در تو
```python
temperature = 25
weather = "sunny"
is_weekend = True

if temperature > 20:
    if weather == "sunny":
        if is_weekend:
            print("Perfect day for outdoor activities!")
        else:
            print("Nice weather for a walk after work.")
    else:
        print("Warm but not sunny.")
else:
    print("It's cold outside.")
```

### اجتناب از تو در تو عمیق
```python
# سخت برای خواندن - تو در تو عمیق
if user is not None:
    if user.is_active:
        if user.age >= 18:
            if user.has_permission:
                perform_action()
            else:
                print("No permission")
        else:
            print("Too young")
    else:
        print("Inactive user")
else:
    print("No user")

# بهتر - early returns یا بندهای نگهبان
if user is None:
    print("No user")
    return

if not user.is_active:
    print("Inactive user")
    return

if user.age < 18:
    print("Too young")
    return

if not user.has_permission:
    print("No permission")
    return

perform_action()
```

## عبارت‌های شرطی (عملگر سه‌گانه)

### سه‌گانه پایه
```python
# if-else سنتی
age = 20
if age >= 18:
    status = "adult"
else:
    status = "minor"

# معادل سه‌گانه
status = "adult" if age >= 18 else "minor"
print(status)
```

### سه‌گانه تو در تو
```python
score = 85
grade = "A" if score >= 90 else ("B" if score >= 80 else ("C" if score >= 70 else "F"))
print(f"Grade: {grade}")

# نسخه قابل خواندن‌تر
if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"
else:
    grade = "F"
```

### مثال‌های عملی سه‌گانه
```python
# بازگشت تابع
def get_discount_rate(age):
    return 0.5 if age < 18 or age > 65 else 0.0

# list comprehension با شرط
numbers = [1, 2, 3, 4, 5]
result = ["even" if x % 2 == 0 else "odd" for x in numbers]
# ["odd", "even", "odd", "even", "odd"]
```

## مثال‌های دنیای واقعی

### احراز هویت کاربر
```python
def authenticate_user(username, password):
    # شبیه‌سازی پایگاه داده کاربر
    users = {
        "alice": "password123",
        "bob": "secret456"
    }

    if username in users:
        if users[username] == password:
            return "Login successful!"
        else:
            return "Incorrect password."
    else:
        return "User not found."

result = authenticate_user("alice", "password123")
print(result)  # "Login successful!"
```

### تخفیف سبد خرید
```python
def calculate_discount(total, customer_type, first_time):
    discount = 0

    if customer_type == "premium":
        discount = 0.2  # 20% برای premium
    elif customer_type == "regular":
        if total >= 100:
            discount = 0.1  # 10% برای regular با خرید بزرگ
        elif first_time:
            discount = 0.05  # 5% برای first-time regular
    else:
        if first_time and total >= 50:
            discount = 0.05  # 5% برای first-time guest

    return total * discount

total = 120
discount = calculate_discount(total, "regular", True)
final_price = total - discount
print(f"Final price: ${final_price:.2f}")
```

### تصمیم پردازش فایل
```python
def process_file(filename):
    if not filename:
        return "No filename provided"

    if not filename.endswith(('.txt', '.csv', '.json')):
        return "Unsupported file type"

    # شبیه‌سازی پردازش فایل
    if filename.endswith('.txt'):
        return "Processed text file"
    elif filename.endswith('.csv'):
        return "Processed CSV file"
    else:
        return "Processed JSON file"

result = process_file("data.txt")
print(result)
```

## بهترین روش‌ها

### ساختار شرط واضح
```python
# خوب - قصد واضح
if user.is_authenticated and user.has_permission:

# کمتر واضح
if user.is_authenticated == True and user.has_permission == True:
```

### تورفتگی ثابت
```python
# همیشه از 4 فاصله استفاده کن (PEP 8)
if condition:
    do_something()
    if nested_condition:
        do_more()
```

### اجتناب از شرط‌های پیچیده
```python
# پیچیده - سخت برای درک
if (age >= 18 and has_license) or (age >= 16 and has_permit and accompanied_by_adult):

# بهتر - از متغیرها استفاده کن
can_drive_solo = age >= 18 and has_license
can_drive_with_permit = age >= 16 and has_permit and accompanied_by_adult

if can_drive_solo or can_drive_with_permit:
```

### از elif برای شرایط mutually exclusive استفاده کن
```python
# خوب - فقط یک شرط می‌تواند درست باشد
if score >= 90:
    grade = "A"
elif score >= 80:
    grade = "B"
elif score >= 70:
    grade = "C"

# اجتناب کن - همه شرط‌ها چک می‌شوند حتی اگر اولین درست باشد
if score >= 90:
    grade = "A"
if score >= 80:  # این حتی اگر score >= 90 درست باشد اجرا می‌شود
    grade = "B"
```

## اشتباهات رایج

### تخصیص در برابر مقایسه
```python
# اشتباه - تخصیص به جای مقایسه
if age = 18:  # SyntaxError در پایتون
    print("Adult")

# درست
if age == 18:
    print("Exactly 18 years old")
```

### مقایسه‌های اعشاری
```python
# مشکل‌دار
if price == 19.99:
    print("Exact price match")

# بهتر - از epsilon برای اعشاری استفاده کن
if abs(price - 19.99) < 0.01:
    print("Approximately $19.99")
```

### مقایسه‌های None
```python
# اشتباه
if user == None:
    print("No user")

# درست - از 'is' برای None استفاده کن
if user is None:
    print("No user")
```

## نکات کلیدی

۱. **دستورات شرطی جریان برنامه را کنترل می‌کنند** بر اساس شرایط
۲. **زنجیره‌های if-elif-else** موارد متعدد mutually exclusive را مدیریت می‌کنند
۳. **مقادیر truthy/falsy** ارزیابی شرط را تعیین می‌کنند
۴. **عملگرهای منطقی** شرایط متعدد را ترکیب می‌کنند
۵. **شرط‌های تو در تو** درختان تصمیم پیچیده ایجاد می‌کنند
۶. **وضوح اهمیت دارد** - منطق شرطی قابل خواندن بنویس

## مطالعه بیشتر
- منطق بولی و جداول درستی
- الگوهای طراحی برای منطق شرطی
- استراتژی‌های تست برای کد شرطی
- بازسازی شرط‌های پیچیده