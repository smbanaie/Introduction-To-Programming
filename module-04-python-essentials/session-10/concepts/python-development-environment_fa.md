# محیط توسعه پایتون: ابزارها برای برنامه‌نویسی

## ابزارهای ضروری برای توسعه پایتون

یک محیط توسعه خوب برنامه‌نویسی را کارآمدتر و لذت‌بخش‌تر می‌کند. در اینجا آنچه برای شروع برنامه‌نویسی پایتون نیاز دارید آورده شده است.

## نصب پایتون

### بررسی نصب
```bash
# بررسی نصب پایتون
python --version  # یا python3 --version

# بررسی مکان نصب
which python     # یا which python3
```

### نصب رسمی پایتون
۱. **دانلود** از python.org
۲. **اجرای نصب‌کننده** با تنظیمات پیش‌فرض
۳. **اضافه کردن به PATH** (مهم برای ویندوز)
۴. **تأیید** با `python --version`

### توزیع‌های جایگزین

#### Anaconda
```bash
# دانلود از anaconda.com
# نصب با نصب‌کننده گرافیکی
# شامل پایتون + کتابخانه‌های علوم داده
# همراه با مدیریت بسته conda
```

#### Miniconda
```bash
# نسخه سبک Anaconda
# دانلود از conda.io/miniconda
# نصب با خط فرمان
```

### مدیریت‌کنندگان بسته

#### ویندوز (Chocolatey)
```powershell
# ابتدا Chocolatey را نصب کنید
# سپس پایتون را نصب کنید
choco install python
```

#### macOS (Homebrew)
```bash
# ابتدا Homebrew را نصب کنید
# سپس پایتون را نصب کنید
brew install python3
```

#### لینوکس (apt/yum)
```bash
# Ubuntu/Debian
sudo apt update
sudo apt install python3 python3-pip

# CentOS/RHEL
sudo yum install python3 python3-pip
```

## ویرایشگرهای کد و IDEها

### ویرایشگرهای مناسب مبتدیان

#### IDLE (همراه پایتون)
```bash
# راه‌اندازی از خط فرمان
idle

# یا پیدا کردن در منوی برنامه‌ها
```
**ویژگی‌ها:**
- رابط ساده
- برجسته‌سازی نحو
- اشکال‌زدای داخلی
- کامل برای مبتدیان

#### Thonny
```bash
# دانلود از thonny.org
# نصب و اجرا
```
**ویژگی‌ها:**
- تمرکز آموزشی
- کاوشگر متغیر
- اشکال‌زدای گام‌به‌گام
- عالی برای یادگیری

### ویرایشگرهای حرفه‌ای

#### Visual Studio Code (VS Code)
```bash
# دانلود از code.visualstudio.com
# نصب افزونه پایتون
# نصب Pylint/Flake8 برای بررسی کد
```
**ویژگی‌ها:**
- رایگان و قدرتمند
- پشتیبانی عالی از پایتون
- ترمینال یکپارچه
- ادغام Git
- افزونه برای همه چیز

#### Sublime Text
```bash
# دانلود از sublimetext.com
# نصب Package Control
# اضافه کردن بسته‌های پایتون
```
**ویژگی‌ها:**
- سریع و سبک
- چند نشانگر
- جستجو/جایگزینی عالی
- بسیار قابل تنظیم

### محیط‌های توسعه یکپارچه (IDEها)

#### PyCharm Community Edition
```bash
# دانلود از jetbrains.com/pycharm
# Community Edition (رایگان) را انتخاب کنید
```
**ویژگی‌ها:**
- IDE حرفه‌ای پایتون
- تکمیل هوشمند کد
- اشکال‌زدایی پیشرفته
- ابزارهای بازسازی کد
- ترمینال داخلی

#### Spyder
```bash
# نصب با Anaconda
conda install spyder

# یا با pip
pip install spyder
```
**ویژگی‌ها:**
- توسعه پایتون علمی
- کاوشگر متغیر
- رسم یکپارچه
- عالی برای علوم داده

## ابزارهای خط فرمان

### مفسر پایتون
```bash
# شروع حالت تعاملی
python3

# اجرای اسکریپت
python3 script.py

# اجرای با خروجی verbose
python3 -v script.py

# بررسی نحو بدون اجرا
python3 -m py_compile script.py
```

### مدیریت بسته‌ها

#### pip (نصب‌کننده بسته پایتون)
```bash
# نصب بسته
pip install requests

# نصب نسخه خاص
pip install requests==2.25.1

# نصب از فایل requirements
pip install -r requirements.txt

# لیست بسته‌های نصب شده
pip list

# ارتقای بسته
pip install --upgrade requests

# حذف بسته
pip uninstall requests
```

#### محیط‌های مجازی
```bash
# ایجاد محیط مجازی
python3 -m venv myproject

# فعال‌سازی (لینوکس/macOS)
source myproject/bin/activate

# فعال‌سازی (ویندوز)
myproject\Scripts\activate

# نصب بسته‌ها در محیط مجازی
pip install requests flask

# غیرفعال‌سازی
deactivate
```

## کنترل نسخه

### تنظیم Git
```bash
# نصب Git
# ویندوز: دانلود از git-scm.com
# macOS: brew install git
# لینوکس: sudo apt install git

# پیکربندی Git
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# مقداردهی اولیه مخزن
git init

# اضافه کردن فایل‌ها
git add .

# اعمال تغییرات
git commit -m "Initial commit"
```

### ادغام GitHub
```bash
# کلون کردن مخزن
git clone https://github.com/user/repo.git

# push به GitHub
git remote add origin https://github.com/user/repo.git
git push -u origin main
```

## تست و اشکال‌زدایی

### اشکال‌زدای داخلی (pdb)
```python
# اضافه کردن به کد شما
import pdb
pdb.set_trace()  # برنامه اینجا متوقف می‌شود

# دستورات اشکال‌زدای:
# n - خط بعدی
# s - ورود به تابع
# c - ادامه
# l - لیست کد
# p variable - نمایش متغیر
# q - خروج
```

### چارچوب‌های تست
```bash
# نصب pytest
pip install pytest

# ایجاد فایل تست
# test_example.py
def test_addition():
    assert 2 + 2 == 4

def test_subtraction():
    assert 5 - 3 == 2

# اجرای تست‌ها
pytest
```

### بررسی کد و کیفیت کد
```bash
# نصب flake8
pip install flake8

# بررسی سبک کد
flake8 script.py

# نصب black (فرمت‌کننده کد)
pip install black

# فرمت کردن کد
black script.py
```

## مستندسازی و کمک

### کمک داخلی
```python
# دریافت کمک درباره هر شیء
help(str)          # متدهای رشته
help(list.append)  # متد خاص
help(len)          # تابع داخلی

# کمک تعاملی
>>> help()
help> str
```

### منابع آنلاین
- **مستندات پایتون**: docs.python.org
- **Stack Overflow**: stackoverflow.com/questions/tagged/python
- **Python Tutor**: pythontutor.com (تصویرسازی اجرای کد)
- **Real Python**: realpython.com (آموزش‌ها)
- **Python Weekly**: pythonweekly.com (خبرنامه)

### جامعه
- **Reddit**: r/learnpython, r/Python
- **Discord**: جوامع پایتون
- **ملاقات‌های محلی**: Meetup.com گروه‌های پایتون
- **کنفرانس‌ها**: PyCon، کنفرانس‌های منطقه‌ای پایتون

## سازماندهی پروژه

### ساختار دایرکتوری
```
my_project/
├── src/                 # کد منبع
│   ├── __init__.py
│   ├── main.py
│   └── utils.py
├── tests/               # فایل‌های تست
│   ├── __init__.py
│   └── test_main.py
├── docs/                # مستندسازی
├── requirements.txt     # وابستگی‌ها
├── README.md           # توصیف پروژه
├── setup.py            # تنظیم بسته
└── .gitignore         # قوانین نادیده گرفتن Git
```

### فایل Requirements
```
# requirements.txt
requests==2.25.1
flask==2.0.1
pytest==6.2.4
```

### اسکریپت Setup
```python
# setup.py
from setuptools import setup

setup(
    name="my_project",
    version="0.1.0",
    packages=["src"],
    install_requires=[
        "requests",
        "flask",
    ],
)
```

## جریان کاری توسعه

### روال روزانه برنامه‌نویسی
۱. **فعال‌سازی محیط مجازی**
۲. **نوشتن کد در ویرایشگر**
۳. **اجرا و تست مکرر**
۴. **استفاده از کنترل نسخه** (اعمال مکرر)
۵. **نوشتن تست** برای ویژگی‌های جدید
۶. **بررسی کیفیت کد** با linterها

### فرآیند اشکال‌زدایی
۱. **تولید مجدد باگ**
۲. **اضافه کردن printهای اشکال‌زدایی** یا استفاده از اشکال‌زدای
۳. **ایزوله کردن مسئله**
۴. **رفع مسئله**
۵. **تست رفع**
۶. **حذف کد اشکال‌زدایی**

### چک‌لیست بررسی کد
- [ ] کد بدون خطا اجرا می‌شود
- [ ] توابع دارای docstring هستند
- [ ] نام متغیرها توصیفی هستند
- [ ] کد از سبک PEP 8 پیروی می‌کند
- [ ] تست‌ها پاس می‌شوند
- [ ] مقدارهای hardcode شده وجود ندارد
- [ ] مدیریت خطا شامل شده

## ابزارهای عملکرد

### profiling
```python
# زمان اجرای تابع
import time

start = time.time()
# کد شما اینجا
end = time.time()
print(f"Time: {end - start} seconds")

# profiling مفصل
import cProfile
cProfile.run('your_function()')
```

### استفاده از حافظه
```python
# بررسی استفاده از حافظه
import psutil
import os

process = psutil.Process(os.getpid())
print(f"Memory usage: {process.memory_info().rss / 1024 / 1024:.2f} MB")
```

## توسعه چند سکویی

### تشخیص پلتفرم
```python
import platform
import os

# تشخیص سیستم عامل
system = platform.system()  # 'Windows', 'Linux', 'Darwin'

# مسیرهای خاص پلتفرم
if os.name == 'nt':  # Windows
    path_separator = '\\'
else:  # Unix-like
    path_separator = '/'
```

### مدیریت تفاوت‌ها
```python
# مدیریت مسیر چند سکویی
from pathlib import Path

# روی همه پلتفرم‌ها کار می‌کند
data_file = Path("data") / "input.txt"

# پایان خطوط چند سکویی
with open("file.txt", "w", newline='') as f:
    f.write("Line 1\nLine 2\n")  # \r\n را روی ویندوز مدیریت می‌کند
```

## نکات کلیدی

۱. **ابزار مناسب را انتخاب کنید** برای سطح مهارت و نیازهای پروژه شما
۲. **از محیط‌های مجازی استفاده کنید** برای ایزوله کردن وابستگی‌های پروژه
۳. **کنترل نسخه را از ابتدا تمرین کنید**
۴. **کد خود را به طور منظم تست کنید** و از ابزارهای اشکال‌زدایی استفاده کنید
۵. **از استانداردهای برنامه‌نویسی پیروی کنید** و از ابزارهای بررسی کد استفاده کنید
۶. **به جامعه بپیوندید** برای یادگیری و حمایت

## مطالعه بیشتر
- بهترین روش‌های توسعه پایتون
- ویژگی‌های پیشرفته IDE و افزونه‌ها
- ادغام مداوم و استقرار
- جریان‌های کاری توسعه حرفه‌ای