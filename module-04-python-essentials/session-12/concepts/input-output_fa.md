# ورودی و خروجی تو پایتون: ارتباط با برنامه‌ها

## ارتباط برنامه

برنامه‌ها نیاز دارن با کاربران، فایل‌ها و سیستم‌های دیگه تعامل کنن. عملیات ورودی و خروجی این ارتباط رو ممکن می‌کنن و به برنامه‌ها اجازه می‌دن داده‌ها رو دریافت کنن و نتایج رو ارسال نمایند.

## ورودی کنسول

### ورودی پایه با input()
```python
# ورودی کاربر را به عنوان رشته دریافت کن
name = input("Enter your name: ")
print(f"Hello, {name}!")

# ورودی با prompt
age = input("How old are you? ")
print(f"You are {age} years old.")
```

### تبدیل نوع برای ورودی
```python
# ورودی را به اعداد تبدیل کن
age = int(input("Enter your age: "))
height = float(input("Enter your height in meters: "))
weight = float(input("Enter your weight in kg: "))

# محاسبه BMI
bmi = weight / (height ** 2)
print(f"Your BMI is: {bmi:.1f}")
```

### مدیریت خطاهای ورودی
```python
# ورودی عددی امن
def get_number(prompt):
    while True:
        try:
            return float(input(prompt))
        except ValueError:
            print("Please enter a valid number.")

age = get_number("Enter your age: ")
print(f"You entered: {age}")
```

### ورودی‌های متعدد
```python
# چندین مقدار را در یک ورودی دریافت کن
coordinates = input("Enter x,y coordinates: ")
x_str, y_str = coordinates.split(',')
x = float(x_str.strip())
y = float(y_str.strip())
print(f"Point: ({x}, {y})")
```

## خروجی کنسول

### خروجی پایه با print()
```python
# خروجی متن ساده
print("Hello, World!")

# آرگومان‌های متعدد
name = "Alice"
age = 25
print("Name:", name, "Age:", age)

# سرکوب newline
print("Hello", end="")
print(" World!")  # Output: "Hello World!"
```

### خروجی قالب‌بندی شده
```python
# f-stringها (پایتون ۳.۶+)
name = "Alice"
age = 25
print(f"My name is {name} and I am {age} years old.")

# روش format()
print("My name is {} and I am {} years old.".format(name, age))

# placeholderهای نام‌گذاری شده
print("Hello {name}, you are {age}.".format(name="Bob", age=30))

# قالب‌بندی % (سبک قدیمی‌تر)
print("My name is %s and I am %d years old." % (name, age))
```

### قالب‌بندی پیشرفته
```python
# قالب‌بندی اعداد
pi = 3.14159265359
print(f"Pi to 2 decimal places: {pi:.2f}")
print(f"Pi in scientific notation: {pi:.2e}")

# عرض فیلد و تراز
names = ["Alice", "Bob", "Catherine"]
for name in names:
    print(f"{name:<10} | {len(name):>2} chars")
# Output:
# Alice      |  5 chars
# Bob        |  3 chars
# Catherine  | 10 chars
```

## ورودی/خروجی فایل

### خواندن فایل‌ها
```python
# باز کردن و خواندن کل فایل
with open("data.txt", "r") as file:
    content = file.read()
    print(content)

# خط به خط خواندن
with open("data.txt", "r") as file:
    for line in file:
        print(line.strip())  # کاراکترهای newline را حذف کن

# خواندن تعداد کاراکترهای خاص
with open("data.txt", "r") as file:
    chunk = file.read(100)  # ۱۰۰ کاراکتر اول را بخوان
    print(chunk)
```

### نوشتن فایل‌ها
```python
# نوشتن در فایل (محتوای موجود را بازنویسی می‌کند)
with open("output.txt", "w") as file:
    file.write("Hello, World!\n")
    file.write("This is a test file.\n")

# اضافه کردن به فایل
with open("log.txt", "a") as file:
    file.write("Program started\n")

# نوشتن چندین خط
lines = ["Line 1", "Line 2", "Line 3"]
with open("lines.txt", "w") as file:
    for line in lines:
        file.write(line + "\n")
```

### حالت‌های فایل
```python
# حالت‌های خواندن
"r"   # Read (پیش‌فرض)
"rb"  # Read binary

# حالت‌های نوشتن
"w"   # Write (بازنویسی می‌کند)
"wb"  # Write binary
"a"   # Append
"ab"  # Append binary

# حالت‌های universal
"r+"  # Read and write
"w+"  # Read and write (بازنویسی می‌کند)
"a+"  # Read and append
```

### مدیریت خطاهای فایل
```python
def safe_read_file(filename):
    try:
        with open(filename, "r") as file:
            return file.read()
    except FileNotFoundError:
        print(f"File '{filename}' not found.")
        return None
    except PermissionError:
        print(f"No permission to read '{filename}'.")
        return None
    except Exception as e:
        print(f"Error reading file: {e}")
        return None

content = safe_read_file("myfile.txt")
if content:
    print(content)
```

## کار با مسیرهای فایل

### مدیریت مسیر
```python
import os

# دایرکتوری کاری فعلی
current_dir = os.getcwd()
print(f"Current directory: {current_dir}")

# تغییر دایرکتوری
os.chdir("/path/to/directory")

# اتصال مسیرها (cross-platform)
filepath = os.path.join("folder", "subfolder", "file.txt")
# Windows: folder\subfolder\file.txt
# Unix: folder/subfolder/file.txt

# بررسی وجود فایل
if os.path.exists("file.txt"):
    print("File exists")

# دریافت اطلاعات فایل
file_size = os.path.getsize("file.txt")
print(f"File size: {file_size} bytes")
```

### ماژول pathlib (پایتون ۳.۴+)
```python
from pathlib import Path

# ایجاد اشیای Path
file_path = Path("data") / "input.txt"
print(file_path)  # data/input.txt

# بررسی ویژگی‌های فایل
if file_path.exists():
    print(f"File size: {file_path.stat().st_size} bytes")
    print(f"Last modified: {file_path.stat().st_mtime}")

# خواندن و نوشتن به راحتی
content = file_path.read_text()
file_path.write_text("New content")
```

## ورودی/خروجی فایل باینری

### خواندن فایل‌های باینری
```python
# خواندن فایل باینری
with open("image.jpg", "rb") as file:
    data = file.read()
    print(f"Read {len(data)} bytes")

# پردازش داده باینری
header = data[:10]  # ۱۰ بایت اول
print(f"Header: {header.hex()}")
```

### نوشتن فایل‌های باینری
```python
# نوشتن داده باینری
binary_data = bytes([0x48, 0x65, 0x6C, 0x6C, 0x6F])  # "Hello" در بایت‌ها

with open("output.bin", "wb") as file:
    file.write(binary_data)
```

## کدگذاری رشته

### مبانی کدگذاری متن
```python
# نوشتن متن با کدگذاری خاص
text = "Hello, 世界"

with open("utf8_file.txt", "w", encoding="utf-8") as file:
    file.write(text)

# خواندن متن با کدگذاری
with open("utf8_file.txt", "r", encoding="utf-8") as file:
    content = file.read()
    print(content)
```

### مدیریت خطاهای کدگذاری
```python
# تعیین مدیریت خطا
with open("file.txt", "r", encoding="utf-8", errors="replace") as file:
    content = file.read()  # کاراکترهای نامعتبر را با � جایگزین می‌کند

# نادیده گرفتن خطاهای کدگذاری
with open("file.txt", "r", encoding="utf-8", errors="ignore") as file:
    content = file.read()  # کاراکترهای نامعتبر را رد می‌کند
```

## تکنیک‌های ورودی/خروجی پیشرفته

### خواندن فایل‌های بزرگ
```python
# پردازش فایل بزرگ خط به خط
def process_large_file(filename):
    with open(filename, "r") as file:
        for line_number, line in enumerate(file, 1):
            # هر خط را پردازش کن
            if "ERROR" in line:
                print(f"Error on line {line_number}: {line.strip()}")

process_large_file("large_log.txt")
```

### context managerها
```python
# context manager سفارشی
class FileHandler:
    def __init__(self, filename, mode):
        self.filename = filename
        self.mode = mode
        self.file = None

    def __enter__(self):
        self.file = open(self.filename, self.mode)
        return self.file

    def __exit__(self, exc_type, exc_val, exc_tb):
        if self.file:
            self.file.close()

# استفاده
with FileHandler("data.txt", "r") as file:
    content = file.read()
# فایل به طور خودکار بسته می‌شود
```

### ورودی/خروجی بافر شده
```python
import io

# خواندن بافر شده برای عملکرد
with open("large_file.txt", "r", buffering=8192) as file:
    for line in file:
        process_line(line)

# بافر رشته
string_buffer = io.StringIO()
string_buffer.write("Hello")
string_buffer.write(" World!")
content = string_buffer.getvalue()  # "Hello World!"
```

## جریان‌های استاندارد

### stdin, stdout, stderr
```python
import sys

# خواندن از ورودی استاندارد
user_input = sys.stdin.read()

# نوشتن در خروجی استاندارد
sys.stdout.write("Hello\n")

# نوشتن در خطای استاندارد
sys.stderr.write("Error: Something went wrong\n")

# تغییر مسیر خروجی
original_stdout = sys.stdout
with open("output.txt", "w") as file:
    sys.stdout = file
    print("This goes to file")
sys.stdout = original_stdout
```

## برنامه‌های تعاملی

### برنامه‌های menu-driven
```python
def show_menu():
    print("\n=== Calculator Menu ===")
    print("1. Add numbers")
    print("2. Subtract numbers")
    print("3. Multiply numbers")
    print("4. Divide numbers")
    print("5. Exit")

def get_numbers():
    a = float(input("Enter first number: "))
    b = float(input("Enter second number: "))
    return a, b

def main():
    while True:
        show_menu()
        choice = input("Choose an option (1-5): ")

        if choice == "1":
            a, b = get_numbers()
            print(f"Result: {a + b}")
        elif choice == "2":
            a, b = get_numbers()
            print(f"Result: {a - b}")
        elif choice == "3":
            a, b = get_numbers()
            print(f"Result: {a * b}")
        elif choice == "4":
            a, b = get_numbers()
            if b != 0:
                print(f"Result: {a / b}")
            else:
                print("Error: Division by zero")
        elif choice == "5":
            print("Goodbye!")
            break
        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
```

## نکات کلیدی

۱. **توابع ورودی** مانند `input()` داده‌ها را از کاربران دریافت می‌کنند
۲. **توابع خروجی** مانند `print()` اطلاعات را نمایش می‌دهند
۳. **عملیات فایل** از `open()` با context managerها برای امنیت استفاده می‌کنند
۴. **مدیریت خطا** از خرابی‌های ورودی یا فایل‌های نامعتبر جلوگیری می‌کند
۵. **آگاهی از کدگذاری** مدیریت مناسب متن را تضمین می‌کند

## مطالعه بیشتر
- مستندات ورودی/خروجی پایتون
- بهترین روش‌های مدیریت فایل
- استانداردهای کدگذاری کاراکتر
- طراحی رابط خط فرمان
- logging و قالب‌بندی خروجی