# شرط‌های تو در تو: درختان تصمیم پیچیده

## مقدمه شرط‌های تو در تو

شرط‌های تو در تو وقتی اتفاق می‌افتند که یک دستور شرطی داخل دیگری قرار گیرد. آنها درختان تصمیم ایجاد می‌کنند که منطق پیچیده را با ارزیابی شرایط متعدد به ترتیب مدیریت می‌کنند.

## ساختارهای تو در تو پایه

### تو در تو ساده
```python
age = 25
has_license = True

if age >= 18:
    print("You are an adult.")
    if has_license:
        print("You can drive.")
    else:
        print("You need a license to drive.")
else:
    print("You are a minor.")
```

### سطوح متعدد
```python
temperature = 75
weather = "sunny"
is_weekend = True

if temperature > 70:
    print("It's warm outside.")
    if weather == "sunny":
        print("Perfect weather!")
        if is_weekend:
            print("Time for outdoor activities.")
        else:
            print("Enjoy after work.")
    else:
        print("Warm but not sunny.")
else:
    print("It's cool outside.")
```

## الگوهای رایج و anti-patternها

### Anti-pattern تیر
```python
# اجتناب کن - سخت برای خواندن و نگهداری
if condition1:
    if condition2:
        if condition3:
            if condition4:
                do_something()
            else:
                handle_case_4()
        else:
            handle_case_3()
    else:
        handle_case_2()
else:
    handle_case_1()
```

### بندهای نگهبان (Early Returns)
```python
# بهتر - موارد خطا را اول مدیریت کن
def process_user(user):
    if user is None:
        return "No user provided"

    if not user.is_active:
        return "User is inactive"

    if not user.is_verified:
        return "User not verified"

    # منطق اصلی اینجا
    return f"Welcome, {user.name}!"

# استفاده
result = process_user(user)
print(result)
```

### الگوی Return Early
```python
def validate_age(age):
    if age < 0:
        return False, "Age cannot be negative"

    if age > 150:
        return False, "Age seems unrealistic"

    if not isinstance(age, int):
        return False, "Age must be a whole number"

    return True, "Age is valid"

is_valid, message = validate_age(25)
print(f"Valid: {is_valid}, Message: {message}")
```

## درختان تصمیم پیچیده

### کنترل دسترسی کاربر
```python
def check_access(user, resource, action):
    # سطح ۱: احراز هویت
    if not user.is_authenticated:
        return False, "User not authenticated"

    # سطح ۲: وضعیت حساب
    if not user.is_active:
        return False, "Account is inactive"

    # سطح ۳: مجوزهای منبع
    if resource.owner_id == user.id:
        return True, "Access granted (owner)"

    # سطح ۴: مجوزهای مبتنی بر نقش
    if user.role == "admin":
        return True, "Access granted (admin)"
    elif user.role == "moderator":
        if action in ["read", "edit"]:
            return True, "Access granted (moderator)"
        else:
            return False, "Moderators cannot delete"
    elif user.role == "user":
        if action == "read":
            return True, "Access granted (read-only)"
        else:
            return False, "Users have read-only access"

    return False, "Access denied"

# سناریوهای مختلف را تست کن
user_admin = type('User', (), {'is_authenticated': True, 'is_active': True, 'role': 'admin', 'id': 1})()
resource = type('Resource', (), {'owner_id': 2})()

granted, message = check_access(user_admin, resource, "delete")
print(message)  # "Access granted (admin)"
```

### منطق قیمت‌گذاری تجارت الکترونیک
```python
def calculate_price(base_price, customer_type, quantity, promo_code=None):
    # اعتبارسنجی قیمت پایه
    if base_price <= 0:
        raise ValueError("Price must be positive")

    final_price = base_price * quantity

    # تخفیف‌های نوع مشتری
    if customer_type == "premium":
        final_price *= 0.8  # 20% تخفیف
    elif customer_type == "regular":
        if quantity >= 10:
            final_price *= 0.9  # 10% تخفیف برای عمده
    else:  # guest
        final_price *= 1.05  # 5% هزینه اضافی

    # مدیریت کد تبلیغاتی
    if promo_code:
        if promo_code == "SAVE10":
            if customer_type in ["premium", "regular"]:
                final_price *= 0.9  # 10% اضافی تخفیف
            else:
                final_price *= 0.95  # 5% تخفیف برای مهمانان
        elif promo_code == "FREESHIP":
            # تخفیف ارسال در جای دیگر مدیریت می‌شود
            pass
        else:
            raise ValueError("Invalid promo code")

    return round(final_price, 2)

# سناریوهای قیمت‌گذاری را تست کن
price = calculate_price(10.0, "regular", 15, "SAVE10")
print(f"Final price: ${price}")  # $10 * 15 * 0.9 * 0.9 = $121.50
```

## عملگرهای منطقی در برابر شرط‌های تو در تو

### استفاده از عملگرهای منطقی
```python
# ساختار flat با عملگرهای منطقی
def can_drive(age, has_license, has_permit, accompanied):
    return (age >= 18 and has_license) or \
           (age >= 16 and has_permit and accompanied)

# موارد تست
print(can_drive(20, True, False, False))   # True (بزرگسال با گواهینامه)
print(can_drive(17, False, True, True))    # True (صغیر با مجوز و بزرگسال)
print(can_drive(15, False, True, False))   # False (خیلی جوان، همراه نیست)
```

### ساختار تو در تو معادل
```python
def can_drive_nested(age, has_license, has_permit, accompanied):
    if age >= 18:
        if has_license:
            return True
        else:
            return False
    elif age >= 16:
        if has_permit and accompanied:
            return True
        else:
            return False
    else:
        return False

# نتایج مشابه نسخه منطقی
print(can_drive_nested(20, True, False, False))   # True
print(can_drive_nested(17, False, True, True))    # True
print(can_drive_nested(15, False, True, False))   # False
```

### چه زمانی از کدام رویکرد استفاده کن
```python
# از عملگرهای منطقی استفاده کن برای:
# - شرایط ساده
# - کد performance-critical (ارزیابی کوتاه‌مدت)
# - قوانین ریاضی یا کسب‌وکار

# از شرط‌های تو در تو استفاده کن برای:
# - اعتبارسنجی پیچیده با پیام‌های خطای مختلف
# - اقدامات مختلف برای دلایل شکست مختلف
# - فرآیندهای تصمیم‌گیری گام به گام
```

## مدیریت خطا با شرط‌های تو در تو

### زنجیره‌های اعتبارسنجی
```python
def validate_user_data(name, email, age):
    errors = []

    # اعتبارسنجی نام
    if not name:
        errors.append("Name is required")
    elif len(name.strip()) < 2:
        errors.append("Name must be at least 2 characters")
    elif not name.replace(" ", "").isalpha():
        errors.append("Name can only contain letters and spaces")

    # اعتبارسنجی ایمیل
    if not email:
        errors.append("Email is required")
    elif "@" not in email:
        errors.append("Email must contain @ symbol")
    elif "." not in email.split("@")[1]:
        errors.append("Email must have a valid domain")

    # اعتبارسنجی سن
    if age is None:
        errors.append("Age is required")
    elif not isinstance(age, int):
        errors.append("Age must be a number")
    elif age < 0:
        errors.append("Age cannot be negative")
    elif age > 150:
        errors.append("Age seems unrealistic")

    return len(errors) == 0, errors

# اعتبارسنجی را تست کن
valid, error_list = validate_user_data("Alice", "alice@email.com", 25)
print(f"Valid: {valid}")  # True

valid, error_list = validate_user_data("", "invalid", -5)
print(f"Valid: {valid}, Errors: {error_list}")
# Valid: False, Errors: ['Name is required', 'Email must have a valid domain', 'Age cannot be negative']
```

## ماشین‌های حالت با شرط‌های تو در تو

### ماشین حالت ساده
```python
def process_order(order_status, payment_received, items_in_stock):
    if order_status == "pending":
        if payment_received:
            if items_in_stock:
                return "shipped", "Order shipped successfully"
            else:
                return "backordered", "Items temporarily out of stock"
        else:
            return "pending", "Waiting for payment"
    elif order_status == "shipped":
        return "shipped", "Order already shipped"
    elif order_status == "cancelled":
        return "cancelled", "Order was cancelled"
    else:
        return "unknown", "Unknown order status"

# حالت‌های مختلف را تست کن
status, message = process_order("pending", True, True)
print(f"Status: {status}, Message: {message}")  # "shipped", "Order shipped successfully"

status, message = process_order("pending", True, False)
print(f"Status: {status}, Message: {message}")  # "backordered", "Items temporarily out of stock"
```

## ملاحظات عملکرد

### ارزیابی کوتاه‌مدت
```python
# شرایط را بر اساس احتمال/هزینه مرتب کن
def is_valid_user(user):
    # شرایط ارزان را اول چک کن
    return (user is not None and
            hasattr(user, 'id') and
            user.is_active and
            user.email_confirmed and
            complex_database_check(user.id))  # چک گران آخر
```

### اجتناب از تو در تو عمیق
```python
# تو در تو عمیق - سخت برای خواندن
def calculate_tax(income, state, filing_status):
    if state == "CA":
        if filing_status == "single":
            if income < 10000:
                return income * 0.05
            elif income < 50000:
                return income * 0.08
            else:
                return income * 0.10
        elif filing_status == "married":
            # شرط‌های تو در تو بیشتر...
    # ایالت‌های بیشتر...

# flattened با early returns
def calculate_tax_better(income, state, filing_status):
    if state != "CA":
        return 0  # ساده‌سازی شده

    base_rate = 0.08 if filing_status == "married" else 0.10

    if income < 10000:
        rate = 0.05
    elif income < 50000:
        rate = base_rate
    else:
        rate = base_rate + 0.02

    return income * rate
```

## تست شرط‌های تو در تو

### پوشش موارد تست
```python
def test_calculate_tax():
    # همه شاخه‌ها را تست کن
    assert calculate_tax_better(5000, "CA", "single") == 250    # < 10000, single
    assert calculate_tax_better(30000, "CA", "single") == 2400  # 10000-50000, single
    assert calculate_tax_better(70000, "CA", "single") == 7200  # > 50000, single
    assert calculate_tax_better(30000, "CA", "married") == 1920 # 10000-50000, married
    assert calculate_tax_better(5000, "NY", "single") == 0      # ایالت غیر CA

    print("All tests passed!")

test_calculate_tax()
```

### تست boundary
```python
def test_boundaries():
    # موارد edge را تست کن
    assert calculate_tax_better(9999, "CA", "single") == 499.95   # دقیقاً زیر 10000
    assert calculate_tax_better(10000, "CA", "single") == 800     # دقیقاً 10000
    assert calculate_tax_better(10001, "CA", "single") == 801     # دقیقاً بالای 10000

test_boundaries()
```

## بازسازی شرط‌های تو در تو

### Extract Method
```python
# قبل: شرط‌های تو در تو در یک روش
def process_payment(amount, card_type, is_international):
    if amount > 0:
        if card_type in ["visa", "mastercard"]:
            if is_international:
                fee = amount * 0.03
            else:
                fee = amount * 0.02
            return amount + fee
        else:
            raise ValueError("Unsupported card type")
    else:
        raise ValueError("Amount must be positive")

# بعد: روش‌های helper استخراج شده
def calculate_fee(amount, card_type, is_international):
    if card_type not in ["visa", "mastercard"]:
        raise ValueError("Unsupported card type")

    rate = 0.03 if is_international else 0.02
    return amount * rate

def process_payment_refactored(amount, card_type, is_international):
    if amount <= 0:
        raise ValueError("Amount must be positive")

    fee = calculate_fee(amount, card_type, is_international)
    return amount + fee
```

### از دیکشنری‌ها برای منطق پیچیده استفاده کن
```python
# شرط‌های تو در تو را با جداول lookup جایگزین کن
def get_shipping_cost(region, weight, expedited):
    # نرخ‌های ارسال را تعریف کن
    rates = {
        "domestic": {
            False: {  # standard
                "light": 5.99,
                "medium": 8.99,
                "heavy": 12.99
            },
            True: {   # expedited
                "light": 12.99,
                "medium": 18.99,
                "heavy": 24.99
            }
        },
        "international": {
            False: {  # standard
                "light": 15.99,
                "medium": 22.99,
                "heavy": 32.99
            },
            True: {   # expedited
                "light": 25.99,
                "medium": 35.99,
                "heavy": 49.99
            }
        }
    }

    # دسته وزن را تعیین کن
    if weight <= 1:
        weight_cat = "light"
    elif weight <= 5:
        weight_cat = "medium"
    else:
        weight_cat = "heavy"

    return rates[region][expedited][weight_cat]

# استفاده
cost = get_shipping_cost("international", 2.5, True)
print(f"Shipping cost: ${cost}")  # $35.99
```

## نکات کلیدی

۱. **شرط‌های تو در تو درختان تصمیم پیچیده ایجاد می‌کنند** اما می‌توانند سخت برای نگهداری شوند
۲. **بندهای نگهبان و early returns** می‌توانند منطق تو در تو را ساده کنند
۳. **عملگرهای منطقی** اغلب جایگزین‌های پاک‌تری نسبت به تو در تو عمیق فراهم می‌کنند
۴. **پوشش تست** برای منطق شرطی پیچیده crucial است
۵. **بازسازی** می‌تواند خوانایی و قابلیت نگهداری را بهبود بخشد
۶. **عملکرد و وضوح** باید انتخاب بین رویکردها را هدایت کند

## مطالعه بیشتر
- الگوهای طراحی برای منطق شرطی
- ماشین‌های حالت و نظریه automata
- تکنیک‌های بازسازی برای کد پیچیده
- توسعه test-driven برای منطق شرطی