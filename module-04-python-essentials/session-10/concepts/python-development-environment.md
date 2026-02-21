# Python Development Environment: Tools for Coding

## Essential Tools for Python Development

A good development environment makes coding more efficient and enjoyable. Here's what you need to start programming in Python.

## Python Installation

### Checking Installation
```bash
# Check if Python is installed
python --version  # or python3 --version

# Check installation location
which python     # or which python3
```

### Official Python Installation
1. **Download** from python.org
2. **Run installer** with default settings
3. **Add to PATH** (important for Windows)
4. **Verify** with `python --version`

### Alternative Distributions

#### Anaconda
```bash
# Download from anaconda.com
# Install with graphical installer
# Includes Python + data science libraries
# Comes with conda package manager
```

#### Miniconda
```bash
# Lightweight version of Anaconda
# Download from conda.io/miniconda
# Install with command line
```

### Package Managers

#### Windows (Chocolatey)
```powershell
# Install Chocolatey first
# Then install Python
choco install python
```

#### macOS (Homebrew)
```bash
# Install Homebrew first
# Then install Python
brew install python3
```

#### Linux (apt/yum)
```bash
# Ubuntu/Debian
sudo apt update
sudo apt install python3 python3-pip

# CentOS/RHEL
sudo yum install python3 python3-pip
```

## Code Editors and IDEs

### Beginner-Friendly Editors

#### IDLE (Included with Python)
```bash
# Launch from command line
idle

# Or find in applications menu
```
**Features:**
- Simple interface
- Syntax highlighting
- Built-in debugger
- Perfect for beginners

#### Thonny
```bash
# Download from thonny.org
# Install and run
```
**Features:**
- Educational focus
- Variable explorer
- Step-by-step debugger
- Great for learning

### Professional Editors

#### Visual Studio Code (VS Code)
```bash
# Download from code.visualstudio.com
# Install Python extension
# Install Pylint/Flake8 for linting
```
**Features:**
- Free and powerful
- Excellent Python support
- Integrated terminal
- Git integration
- Extensions for everything

#### Sublime Text
```bash
# Download from sublimetext.com
# Install Package Control
# Add Python packages
```
**Features:**
- Fast and lightweight
- Multiple cursors
- Excellent search/replace
- Highly customizable

### Integrated Development Environments (IDEs)

#### PyCharm Community Edition
```bash
# Download from jetbrains.com/pycharm
# Choose Community Edition (free)
```
**Features:**
- Professional Python IDE
- Intelligent code completion
- Advanced debugging
- Refactoring tools
- Built-in terminal

#### Spyder
```bash
# Install with Anaconda
conda install spyder

# Or with pip
pip install spyder
```
**Features:**
- Scientific Python development
- Variable explorer
- Integrated plotting
- Great for data science

## Command Line Tools

### Python Interpreter
```bash
# Start interactive mode
python3

# Run script
python3 script.py

# Run with verbose output
python3 -v script.py

# Check syntax without running
python3 -m py_compile script.py
```

### Package Management

#### pip (Python Package Installer)
```bash
# Install package
pip install requests

# Install specific version
pip install requests==2.25.1

# Install from requirements file
pip install -r requirements.txt

# List installed packages
pip list

# Upgrade package
pip install --upgrade requests

# Uninstall package
pip uninstall requests
```

#### Virtual Environments
```bash
# Create virtual environment
python3 -m venv myproject

# Activate (Linux/macOS)
source myproject/bin/activate

# Activate (Windows)
myproject\Scripts\activate

# Install packages in virtual environment
pip install requests flask

# Deactivate
deactivate
```

## Version Control

### Git Setup
```bash
# Install Git
# Windows: Download from git-scm.com
# macOS: brew install git
# Linux: sudo apt install git

# Configure Git
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Initialize repository
git init

# Add files
git add .

# Commit changes
git commit -m "Initial commit"
```

### GitHub Integration
```bash
# Clone repository
git clone https://github.com/user/repo.git

# Push to GitHub
git remote add origin https://github.com/user/repo.git
git push -u origin main
```

## Testing and Debugging

### Built-in Debugger (pdb)
```python
# Add to your code
import pdb
pdb.set_trace()  # Program pauses here

# Debugger commands:
# n - next line
# s - step into function
# c - continue
# l - list code
# p variable - print variable
# q - quit
```

### Testing Frameworks
```bash
# Install pytest
pip install pytest

# Create test file
# test_example.py
def test_addition():
    assert 2 + 2 == 4

def test_subtraction():
    assert 5 - 3 == 2

# Run tests
pytest
```

### Linting and Code Quality
```bash
# Install flake8
pip install flake8

# Check code style
flake8 script.py

# Install black (code formatter)
pip install black

# Format code
black script.py
```

## Documentation and Help

### Built-in Help
```python
# Get help on any object
help(str)          # String methods
help(list.append)  # Specific method
help(len)          # Built-in function

# Interactive help
>>> help()
help> str
```

### Online Resources
- **Python Documentation**: docs.python.org
- **Stack Overflow**: stackoverflow.com/questions/tagged/python
- **Python Tutor**: pythontutor.com (visualize code execution)
- **Real Python**: realpython.com (tutorials)
- **Python Weekly**: pythonweekly.com (newsletter)

### Community
- **Reddit**: r/learnpython, r/Python
- **Discord**: Python communities
- **Local meetups**: Meetup.com Python groups
- **Conferences**: PyCon, regional Python conferences

## Project Organization

### Directory Structure
```
my_project/
├── src/                 # Source code
│   ├── __init__.py
│   ├── main.py
│   └── utils.py
├── tests/               # Test files
│   ├── __init__.py
│   └── test_main.py
├── docs/                # Documentation
├── requirements.txt     # Dependencies
├── README.md           # Project description
├── setup.py            # Package setup
└── .gitignore         # Git ignore rules
```

### Requirements File
```
# requirements.txt
requests==2.25.1
flask==2.0.1
pytest==6.2.4
```

### Setup Script
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

## Development Workflow

### Daily Coding Routine
1. **Activate virtual environment**
2. **Write code in editor**
3. **Run and test frequently**
4. **Use version control** (commit often)
5. **Write tests** for new features
6. **Check code quality** with linters

### Debugging Process
1. **Reproduce the bug**
2. **Add debug prints** or use debugger
3. **Isolate the problem**
4. **Fix the issue**
5. **Test the fix**
6. **Remove debug code**

### Code Review Checklist
- [ ] Code runs without errors
- [ ] Functions have docstrings
- [ ] Variable names are descriptive
- [ ] Code follows PEP 8 style
- [ ] Tests pass
- [ ] No hardcoded values
- [ ] Error handling included

## Performance Tools

### Profiling
```python
# Time function execution
import time

start = time.time()
# Your code here
end = time.time()
print(f"Time: {end - start} seconds")

# Detailed profiling
import cProfile
cProfile.run('your_function()')
```

### Memory Usage
```python
# Check memory usage
import psutil
import os

process = psutil.Process(os.getpid())
print(f"Memory usage: {process.memory_info().rss / 1024 / 1024:.2f} MB")
```

## Cross-Platform Development

### Platform Detection
```python
import platform
import os

# Detect operating system
system = platform.system()  # 'Windows', 'Linux', 'Darwin'

# Platform-specific paths
if os.name == 'nt':  # Windows
    path_separator = '\\'
else:  # Unix-like
    path_separator = '/'
```

### Handling Differences
```python
# Cross-platform path handling
from pathlib import Path

# Works on all platforms
data_file = Path("data") / "input.txt"

# Cross-platform line endings
with open("file.txt", "w", newline='') as f:
    f.write("Line 1\nLine 2\n")  # Handles \r\n on Windows
```

## Key Takeaways

1. **Choose the right tools** for your skill level and project needs
2. **Use virtual environments** to isolate project dependencies
3. **Practice version control** from the beginning
4. **Test your code** regularly and use debugging tools
5. **Follow coding standards** and use linting tools
6. **Join the community** for learning and support

## Further Reading
- Python development best practices
- Advanced IDE features and plugins
- Continuous integration and deployment
- Professional development workflows