# State Management: Tracking Change in Programs

## What is State?

State is the current condition or situation of a system at any given moment. In programming, state represents all the information that a program needs to remember between operations.

## Types of State

### Program State
The overall condition of a running program:
- **Variables**: Current values stored in memory
- **Execution context**: Which function is running, where it paused
- **Open resources**: Files, network connections, database links
- **Configuration**: Settings that affect behavior

### Application State
Information about what the application is doing:
- **User session**: Login status, preferences, shopping cart
- **Navigation**: Current page/screen, breadcrumbs
- **Workflow progress**: Step completion in multi-step processes
- **Cache data**: Stored results to avoid recomputation

### System State
The condition of the computer system:
- **File system**: Which files exist, their contents
- **Network connections**: Active links and their status
- **Hardware status**: Battery level, disk space, temperature
- **Running processes**: What programs are active

## State in Algorithms

### Stateful Algorithms
Algorithms that remember information between steps:

```python
def running_average():
    total = 0
    count = 0

    def add_number(number):
        nonlocal total, count  # Access outer variables (state)
        total += number
        count += 1
        return total / count

    return add_number

# Usage
avg_func = running_average()
print(avg_func(10))  # 10.0 (state: total=10, count=1)
print(avg_func(20))  # 15.0 (state: total=30, count=2)
print(avg_func(30))  # 20.0 (state: total=60, count=3)
```

### Stateless Algorithms
Each operation is independent, no memory of previous calls:

```python
def calculate_average(numbers):
    # No state - each call is independent
    if not numbers:
        return 0
    return sum(numbers) / len(numbers)

# Each call starts fresh
print(calculate_average([10, 20, 30]))  # 20.0
print(calculate_average([40, 50]))      # 45.0
print(calculate_average([10, 20, 30]))  # 20.0 (same result)
```

## State Representation

### Variables as State
Simple state using variables:
```python
# Counter state
counter = 0

def increment():
    global counter  # Access global state
    counter += 1
    return counter

# Usage
increment()  # 1
increment()  # 2
```

### Objects as State Containers
Complex state using objects:
```python
class BankAccount:
    def __init__(self, initial_balance=0):
        self.balance = initial_balance  # Account state
        self.transactions = []          # Transaction history state

    def deposit(self, amount):
        if amount > 0:
            self.balance += amount
            self.transactions.append(f"Deposit: +{amount}")
            return True
        return False

    def withdraw(self, amount):
        if 0 < amount <= self.balance:
            self.balance -= amount
            self.transactions.append(f"Withdraw: -{amount}")
            return True
        return False

    def get_balance(self):
        return self.balance

    def get_history(self):
        return self.transactions.copy()

# Usage
account = BankAccount(1000)
account.deposit(500)    # State: balance=1500
account.withdraw(200)   # State: balance=1300
print(account.get_balance())     # 1300
print(account.get_history())     # ['Deposit: +500', 'Withdraw: -200']
```

### State Machines
Formal representation of state transitions:

```python
class TrafficLight:
    def __init__(self):
        self.state = "red"  # Initial state

    def next(self):
        # State transitions
        if self.state == "red":
            self.state = "green"
        elif self.state == "green":
            self.state = "yellow"
        elif self.state == "yellow":
            self.state = "red"

        return self.state

    def get_color(self):
        return self.state

# Usage
light = TrafficLight()
print(light.get_color())  # "red"
light.next()              # "green"
light.next()              # "yellow"
light.next()              # "red"
```

## State Persistence

### Temporary State (RAM)
State exists only while program runs:
```python
# In-memory state
user_data = {"name": "Alice", "score": 100}

# State persists during program execution
user_data["score"] += 50  # State changes
print(user_data["score"]) # 150
```

### Persistent State (Storage)
State survives program restarts:
```python
import json

def save_game_state(player_data):
    with open("game_save.json", "w") as file:
        json.dump(player_data, file)

def load_game_state():
    try:
        with open("game_save.json", "r") as file:
            return json.load(file)
    except FileNotFoundError:
        return {"level": 1, "score": 0, "items": []}

# Usage
player = load_game_state()  # Restore state
player["score"] += 100      # Update state
save_game_state(player)     # Persist state
```

## State Management Challenges

### Race Conditions
Multiple processes accessing state simultaneously:
```python
# Problematic shared state
counter = 0

def increment_counter():
    global counter
    current = counter      # Read
    # Another thread could change counter here
    counter = current + 1  # Write

# Solution: Atomic operations or locks
import threading
lock = threading.Lock()

def safe_increment():
    with lock:
        global counter
        counter += 1
```

### State Inconsistency
Invalid state combinations:
```python
class User:
    def __init__(self):
        self.logged_in = False
        self.session_token = None

    def login(self, token):
        self.logged_in = True
        self.session_token = token

    def logout(self):
        self.logged_in = False
        self.session_token = None  # Clean up state

    # Inconsistent state possible:
    # logged_in = True, session_token = None
```

### State Explosion
Too many possible state combinations:
```python
# Complex state (avoid if possible)
class GameCharacter:
    def __init__(self):
        self.health = 100
        self.mana = 50
        self.position = (0, 0)
        self.inventory = []
        self.quests = []
        self.achievements = []
        self.friends = []
        # ... many more fields

# Better: Group related state
class GameCharacter:
    def __init__(self):
        self.stats = {"health": 100, "mana": 50}
        self.location = Location(0, 0)
        self.inventory = Inventory()
        self.progress = Progress()
```

## State Design Patterns

### Singleton Pattern
Single global state instance:
```python
class Configuration:
    _instance = None

    def __new__(cls):
        if cls._instance is None:
            cls._instance = super().__new__(cls)
        return cls._instance

    def __init__(self):
        if not hasattr(self, 'initialized'):
            self.settings = {}
            self.initialized = True

# Usage
config1 = Configuration()
config2 = Configuration()
config1.settings["theme"] = "dark"
print(config2.settings["theme"])  # "dark" (same instance)
```

### Observer Pattern
State changes notify interested parties:
```python
class Subject:
    def __init__(self):
        self._observers = []
        self._state = None

    def attach(self, observer):
        self._observers.append(observer)

    def set_state(self, state):
        self._state = state
        self._notify_observers()

    def _notify_observers(self):
        for observer in self._observers:
            observer.update(self._state)

class Observer:
    def update(self, state):
        print(f"State changed to: {state}")

# Usage
subject = Subject()
observer = Observer()
subject.attach(observer)

subject.set_state("active")   # Observer notified
subject.set_state("inactive") # Observer notified
```

## State in Different Programming Paradigms

### Imperative Programming
Explicit state management:
```python
# State changes are explicit
balance = 1000
balance = balance - 100  # Explicit state change
balance = balance + 200  # Another explicit change
```

### Functional Programming
Minimize or avoid mutable state:
```python
# Pure functions, no state changes
def withdraw(balance, amount):
    return balance - amount  # Returns new value, doesn't modify

def deposit(balance, amount):
    return balance + amount

# Usage
balance = 1000
balance = withdraw(balance, 100)  # 900
balance = deposit(balance, 200)   # 1100
```

### Object-Oriented Programming
State encapsulated in objects:
```python
class Account:
    def __init__(self, balance):
        self._balance = balance  # Private state

    def deposit(self, amount):
        if amount > 0:
            self._balance += amount
            return True
        return False

    def get_balance(self):
        return self._balance
```

## Key Takeaways

1. **State is memory of past events**: What the system knows at any moment
2. **State management is crucial**: Poor state handling leads to bugs
3. **Different state types**: Program, application, and system state
4. **Persistence matters**: Some state survives program restarts
5. **Design patterns help**: Proper patterns manage complex state

## Further Reading
- Study state machines and automata theory
- Learn about Redux and state management in web applications
- Explore database state management and transactions
- Understand distributed systems and eventual consistency