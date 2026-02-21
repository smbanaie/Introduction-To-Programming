# Modular Design: Building Maintainable Software

## Introduction to Modular Programming

Modular design involves breaking large programs into smaller, independent modules that can be developed, tested, and maintained separately. This approach leads to more maintainable, reusable, and understandable code.

## Functions as Modules

### Single Responsibility Principle
```python
# Bad - one function doing multiple things
def process_user_data(data):
    """This function does too many things."""
    # Validate data
    # Clean data
    # Save to database
    # Send notification
    # Log activity
    pass

# Good - separate functions for each responsibility
def validate_user_data(data):
    """Validate user input data."""
    pass

def clean_user_data(data):
    """Clean and normalize user data."""
    pass

def save_user_to_database(user):
    """Save user to database."""
    pass

def send_welcome_email(user):
    """Send welcome email to user."""
    pass

def log_user_registration(user):
    """Log user registration activity."""
    pass

def register_user(data):
    """Register a new user - orchestrates the process."""
    clean_data = clean_user_data(data)
    user = validate_user_data(clean_data)

    save_user_to_database(user)
    send_welcome_email(user)
    log_user_registration(user)

    return user
```

### Function Composition
```python
def get_text_from_file(filename):
    """Read text from file."""
    with open(filename, 'r') as f:
        return f.read()

def clean_text(text):
    """Clean and normalize text."""
    return text.lower().strip()

def extract_words(text):
    """Extract words from text."""
    import re
    return re.findall(r'\b\w+\b', text)

def count_word_frequency(words):
    """Count word frequencies."""
    from collections import Counter
    return Counter(words)

def get_top_words(filename, n=10):
    """Get most common words from file."""
    text = get_text_from_file(filename)
    cleaned = clean_text(text)
    words = extract_words(cleaned)
    frequencies = count_word_frequency(words)

    return frequencies.most_common(n)

# Usage
top_words = get_top_words("sample.txt", 5)
print(top_words)
```

## Code Organization Principles

### Separation of Concerns
```python
# data_processing.py - Data handling
def load_data(filename):
    """Load data from file."""
    pass

def validate_data(data):
    """Validate data integrity."""
    pass

def clean_data(data):
    """Clean and preprocess data."""
    pass

# database.py - Database operations
def connect_to_database(config):
    """Establish database connection."""
    pass

def save_record(record, connection):
    """Save record to database."""
    pass

def query_records(query, connection):
    """Query database records."""
    pass

# email_service.py - Email functionality
def send_email(to, subject, body):
    """Send email message."""
    pass

def create_welcome_email(user):
    """Create welcome email content."""
    pass

# main.py - Main application logic
def process_new_user(user_data):
    """Process new user registration."""
    # Load and validate data
    data = load_data(user_data)
    if not validate_data(data):
        raise ValueError("Invalid data")

    # Clean data
    clean_user_data = clean_data(data)

    # Save to database
    conn = connect_to_database(db_config)
    save_record(clean_user_data, conn)

    # Send welcome email
    welcome_email = create_welcome_email(clean_user_data)
    send_email(clean_user_data['email'], welcome_email['subject'], welcome_email['body'])
```

### Abstraction Levels
```python
# Low-level functions - detailed implementation
def read_csv_file(filename):
    """Read CSV file and return rows."""
    with open(filename, 'r') as f:
        lines = f.readlines()
        # Parse CSV format
        rows = []
        for line in lines:
            # Split by comma, handle quotes, etc.
            row = parse_csv_line(line)
            rows.append(row)
        return rows

def parse_csv_line(line):
    """Parse single CSV line."""
    # Handle quoted fields, escaped commas, etc.
    pass

def save_to_database(records, table_name):
    """Save records to database table."""
    conn = get_database_connection()
    for record in records:
        # Execute INSERT statement
        # Handle transactions, error recovery, etc.
        pass

# High-level functions - business logic
def import_customer_data(csv_filename):
    """Import customer data from CSV."""
    records = read_csv_file(csv_filename)
    validated_records = validate_customer_records(records)
    save_to_database(validated_records, "customers")
    send_import_notification(len(validated_records))

def validate_customer_records(records):
    """Validate customer data."""
    # Business rule validation
    pass

def send_import_notification(count):
    """Send notification about import completion."""
    pass
```

## Function Interfaces and Contracts

### Clear Function Contracts
```python
def calculate_bmi(weight_kg: float, height_m: float) -> float:
    """
    Calculate Body Mass Index.

    Args:
        weight_kg: Weight in kilograms (must be > 0)
        height_m: Height in meters (must be > 0)

    Returns:
        BMI value as float

    Raises:
        ValueError: If weight or height are not positive
        TypeError: If inputs are not numbers

    Example:
        >>> calculate_bmi(70, 1.75)
        22.857142857142858
    """
    if not isinstance(weight_kg, (int, float)) or not isinstance(height_m, (int, float)):
        raise TypeError("Weight and height must be numbers")

    if weight_kg <= 0 or height_m <= 0:
        raise ValueError("Weight and height must be positive")

    return weight_kg / (height_m ** 2)
```

### Consistent Error Handling
```python
class DataProcessingError(Exception):
    """Custom exception for data processing errors."""
    pass

def process_financial_data(data):
    """Process financial data with consistent error handling."""
    try:
        validated_data = validate_financial_data(data)
        processed_data = calculate_financial_metrics(validated_data)
        save_processed_data(processed_data)
        return processed_data
    except ValueError as e:
        raise DataProcessingError(f"Invalid financial data: {e}")
    except ConnectionError as e:
        raise DataProcessingError(f"Database connection failed: {e}")
    except Exception as e:
        raise DataProcessingError(f"Unexpected error: {e}")

def validate_financial_data(data):
    """Validate financial data."""
    # Validation logic
    pass

def calculate_financial_metrics(data):
    """Calculate financial metrics."""
    # Calculation logic
    pass

def save_processed_data(data):
    """Save processed data."""
    # Saving logic
    pass
```

## Dependency Management

### Loose Coupling
```python
# Tight coupling - hard to test and maintain
class EmailService:
    def send_notification(self, user):
        # Directly depends on database
        db = DatabaseConnection()
        user_data = db.get_user(user.id)
        email_content = self.create_email_content(user_data)

        # Directly depends on email service
        smtp = SMTPClient()
        smtp.send(user.email, email_content)

# Loose coupling - dependencies injected
class NotificationService:
    def __init__(self, database, email_client):
        self.database = database
        self.email_client = email_client

    def send_notification(self, user_id):
        user_data = self.database.get_user(user_id)
        email_content = self.create_email_content(user_data)
        self.email_client.send(user_data['email'], email_content)
```

### Dependency Injection
```python
# Configuration and dependency setup
def create_app(config):
    """Create application with dependencies."""
    database = DatabaseConnection(config['database_url'])
    email_client = SMTPClient(config['smtp_settings'])
    cache = RedisCache(config['redis_url'])

    # Inject dependencies
    user_service = UserService(database, email_client, cache)
    notification_service = NotificationService(database, email_client)

    return {
        'user_service': user_service,
        'notification_service': notification_service
    }

# Usage in tests
def test_user_registration():
    # Create mock dependencies
    mock_db = MockDatabase()
    mock_email = MockEmailClient()
    mock_cache = MockCache()

    # Inject mocks for testing
    user_service = UserService(mock_db, mock_email, mock_cache)

    # Test the service
    user = user_service.register_user(test_data)
    assert user.email == test_data['email']
```

## Testing Modular Code

### Unit Testing Functions
```python
import pytest
from my_module import calculate_bmi, process_financial_data

def test_calculate_bmi():
    """Test BMI calculation."""
    # Normal cases
    assert calculate_bmi(70, 1.75) == pytest.approx(22.857, rel=1e-3)
    assert calculate_bmi(50, 1.60) == pytest.approx(19.531, rel=1e-3)

    # Edge cases
    assert calculate_bmi(1, 1) == 1.0

def test_calculate_bmi_errors():
    """Test BMI calculation error handling."""
    with pytest.raises(ValueError):
        calculate_bmi(-70, 1.75)

    with pytest.raises(ValueError):
        calculate_bmi(70, -1.75)

    with pytest.raises(TypeError):
        calculate_bmi("70", 1.75)

def test_process_financial_data():
    """Test financial data processing."""
    test_data = {
        'transactions': [100, 200, 300],
        'currency': 'USD'
    }

    result = process_financial_data(test_data)

    assert 'total' in result
    assert 'average' in result
    assert result['total'] == 600
    assert result['average'] == 200
```

### Mocking Dependencies
```python
from unittest.mock import Mock, patch

def test_notification_service():
    """Test notification service with mocked dependencies."""
    # Create mocks
    mock_db = Mock()
    mock_db.get_user.return_value = {'email': 'test@example.com', 'name': 'Test User'}

    mock_email = Mock()
    mock_email.send.return_value = True

    # Create service with mocks
    service = NotificationService(mock_db, mock_email)

    # Test the method
    result = service.send_notification(123)

    # Verify interactions
    mock_db.get_user.assert_called_once_with(123)
    mock_email.send.assert_called_once()

    assert result is True
```

## Code Reusability and Libraries

### Creating Reusable Functions
```python
def retry_operation(operation, max_attempts=3, delay=1):
    """Retry an operation with exponential backoff."""
    import time

    for attempt in range(max_attempts):
        try:
            return operation()
        except Exception as e:
            if attempt == max_attempts - 1:
                raise e
            time.sleep(delay * (2 ** attempt))  # Exponential backoff

def safe_file_operation(filename, operation):
    """Perform file operation with error handling."""
    try:
        with open(filename, 'r') as f:
            return operation(f)
    except FileNotFoundError:
        raise FileNotFoundError(f"File not found: {filename}")
    except PermissionError:
        raise PermissionError(f"Permission denied: {filename}")
    except Exception as e:
        raise Exception(f"Error processing file {filename}: {e}")

# Usage
def count_lines(file_obj):
    return len(file_obj.readlines())

line_count = safe_file_operation("data.txt", count_lines)
```

### Function Factories
```python
def create_validator(rules):
    """Create a validator function from rules."""
    def validator(data):
        errors = []
        for rule_name, rule_func in rules.items():
            if not rule_func(data):
                errors.append(f"Failed {rule_name}")
        return errors if errors else None
    return validator

# Define validation rules
user_rules = {
    'email_format': lambda d: '@' in d.get('email', ''),
    'age_range': lambda d: 13 <= d.get('age', 0) <= 120,
    'name_present': lambda d: bool(d.get('name', '').strip())
}

# Create validator
validate_user = create_validator(user_rules)

# Use validator
user_data = {'name': 'Alice', 'email': 'alice@example.com', 'age': 25}
errors = validate_user(user_data)
print(errors)  # None (no errors)

invalid_data = {'name': '', 'email': 'invalid', 'age': 10}
errors = validate_user(invalid_data)
print(errors)  # ['Failed email_format', 'Failed age_range', 'Failed name_present']
```

## Documentation and Code Comments

### Module Documentation
```python
"""
Data Processing Module

This module provides functions for processing various types of data
including text, numbers, and structured data formats.

Classes:
    DataProcessor: Main class for data processing operations

Functions:
    clean_text: Clean and normalize text data
    validate_data: Validate data against schema
    transform_data: Apply transformations to data

Examples:
    >>> processor = DataProcessor()
    >>> clean_data = processor.process(raw_data)
"""

class DataProcessor:
    """Main data processing class."""

    def __init__(self, config=None):
        """Initialize processor with configuration."""
        self.config = config or {}

    def process(self, data):
        """Process input data."""
        cleaned = self.clean_data(data)
        validated = self.validate_data(cleaned)
        transformed = self.transform_data(validated)
        return transformed

    def clean_data(self, data):
        """Clean input data."""
        # Implementation
        pass

    def validate_data(self, data):
        """Validate data integrity."""
        # Implementation
        pass

    def transform_data(self, data):
        """Transform data according to rules."""
        # Implementation
        pass
```

### Inline Comments and Documentation
```python
def complex_calculation(data, parameters):
    """
    Perform complex calculation on data.

    This function applies multiple transformations and calculations
    to the input data based on the provided parameters.
    """
    # Step 1: Validate input data
    if not self.validate_input(data):
        raise ValueError("Invalid input data")

    # Step 2: Apply preprocessing transformations
    preprocessed = self.preprocess_data(data, parameters.get('preprocessing', {}))

    # Step 3: Perform main calculation
    # This is the core algorithm that processes the data
    result = self.perform_calculation(preprocessed, parameters)

    # Step 4: Apply post-processing if requested
    if parameters.get('post_processing', False):
        result = self.post_process_result(result, parameters)

    # Step 5: Validate final result
    self.validate_result(result)

    return result
```

## Performance Considerations

### Function Call Overhead
```python
# For performance-critical code, consider inlining small functions
def is_even(number):
    return number % 2 == 0

# In performance-critical loop
even_numbers = []
for num in large_list:
    if num % 2 == 0:  # Inline the check
        even_numbers.append(num)

# Or use list comprehension for better performance
even_numbers = [num for num in large_list if num % 2 == 0]
```

### Memory Usage in Modular Code
```python
# Avoid creating large intermediate data structures
def process_large_file(filename):
    """Process large file efficiently."""
    results = []

    with open(filename, 'r') as f:
        for line in f:
            # Process line immediately, don't accumulate large lists
            processed_line = process_single_line(line)
            if meets_criteria(processed_line):
                results.append(processed_line)

    return results

# Better - use generators for memory efficiency
def process_large_file_generator(filename):
    """Process large file with generator."""
    with open(filename, 'r') as f:
        for line in f:
            processed_line = process_single_line(line)
            if meets_criteria(processed_line):
                yield processed_line
```

## Key Takeaways

1. **Modular design breaks complex problems** into manageable pieces
2. **Single responsibility principle** keeps functions focused
3. **Clear interfaces and contracts** improve maintainability
4. **Dependency injection** enables testing and flexibility
5. **Comprehensive testing** ensures module reliability
6. **Good documentation** enables code reuse and maintenance

## Further Reading
- SOLID principles of object-oriented design
- Design patterns for modular software
- Test-driven development practices
- Refactoring techniques for legacy code
- Microservices architecture principles