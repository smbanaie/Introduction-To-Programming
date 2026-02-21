# Session 21: Mini-Project: Data Processing

## Lecture Overview
**Duration**: 120 minutes (extended for project work)
**Objectives**: Students will build a complete data processing application integrating all concepts
**Materials**: Sample data files, project requirements, code templates

---

## I. Introduction (15 minutes)

### Review and Hook (5 minutes)
- **Quick Review**: How do you organize code into modules?
- **Hook Activity**: Show project demo - data processing application
- **Question**: "How can we apply everything we've learned to solve a real problem?"

### Learning Goals (5 minutes)
By the end of this session, you will be able to:
- Design and implement a complete program
- Integrate multiple programming concepts
- Handle real-world data processing tasks
- Apply best practices in code organization

### Agenda Overview (5 minutes)
1. Project requirements and design
2. Implementation planning
3. Coding and testing
4. Project review and improvements

---

## II. Project Overview (20 minutes)

### Data Processing Application Requirements

#### Core Functionality
- **Data Import**: Read data from CSV/text files
- **Data Processing**: Clean, filter, and transform data
- **Data Analysis**: Calculate statistics and insights
- **Data Export**: Save processed results to files
- **User Interface**: Command-line menu system

#### Sample Use Case: Student Grade Processor
```
Features:
- Load student data from file
- Calculate grades and statistics
- Generate reports
- Handle missing/invalid data
- Export processed results
```

#### Project Structure
```
grade_processor/
├── main.py              # Main program entry point
├── data_loader.py       # File reading and parsing
├── data_processor.py    # Data cleaning and calculations
├── report_generator.py  # Report creation and export
├── utils.py            # Helper functions
├── config.py           # Configuration settings
└── sample_data.csv     # Sample input data
```

---

## III. Implementation Planning (25 minutes)

### Step 1: Data Format Design
```python
# Sample data format (CSV)
# student_id,name,assignment1,assignment2,exam,participation
# 1001,Alice Johnson,85,92,88,95
# 1002,Bob Smith,78,85,,90
# 1003,Charlie Brown,92,88,90,85

# Processed data structure
students = [
    {
        "id": 1001,
        "name": "Alice Johnson",
        "grades": [85, 92, 88, 95],
        "average": 90.0,
        "letter_grade": "A"
    },
    # ... more students
]
```

### Step 2: Function Design
```python
# data_loader.py
def load_students_from_csv(filename):
    """Load student data from CSV file."""
    pass

def validate_student_data(student_data):
    """Validate and clean student data."""
    pass

# data_processor.py
def calculate_student_average(grades):
    """Calculate average grade for a student."""
    pass

def assign_letter_grade(average):
    """Convert numeric grade to letter grade."""
    pass

def calculate_class_statistics(students):
    """Calculate class-wide statistics."""
    pass

# report_generator.py
def generate_student_report(student):
    """Generate report for individual student."""
    pass

def generate_class_summary(students):
    """Generate class summary report."""
    pass

def export_to_file(data, filename):
    """Export data to file."""
    pass
```

### Step 3: User Interface Design
```
Student Grade Processor v1.0

Main Menu:
1. Load student data
2. View all students
3. View student details
4. Generate class report
5. Export data
6. Exit

Choose option (1-6):
```

---

## IV. Guided Implementation (45 minutes)

### Phase 1: Data Loading (15 minutes)
```python
# data_loader.py
import csv

def load_students_from_csv(filename):
    """Load student data from CSV file."""
    students = []

    try:
        with open(filename, 'r') as file:
            reader = csv.DictReader(file)
            for row in reader:
                student = {
                    'id': int(row['student_id']),
                    'name': row['name'],
                    'grades': []
                }

                # Handle potentially empty grade fields
                for key in ['assignment1', 'assignment2', 'exam', 'participation']:
                    if row.get(key, '').strip():
                        try:
                            student['grades'].append(float(row[key]))
                        except ValueError:
                            print(f"Warning: Invalid grade '{row[key]}' for {student['name']}")

                students.append(student)

    except FileNotFoundError:
        print(f"Error: File '{filename}' not found")
        return []
    except Exception as e:
        print(f"Error loading file: {e}")
        return []

    return students

def validate_student_data(students):
    """Validate student data and add calculated fields."""
    for student in students:
        if not student['grades']:
            student['average'] = 0
            student['letter_grade'] = 'N/A'
        else:
            student['average'] = sum(student['grades']) / len(student['grades'])
            student['letter_grade'] = assign_letter_grade(student['average'])

    return students
```

### Phase 2: Data Processing (15 minutes)
```python
# data_processor.py
def calculate_student_average(grades):
    """Calculate average grade, handling empty grades."""
    if not grades:
        return 0.0
    return sum(grades) / len(grades)

def assign_letter_grade(average):
    """Convert numeric grade to letter grade."""
    if average >= 90:
        return 'A'
    elif average >= 80:
        return 'B'
    elif average >= 70:
        return 'C'
    elif average >= 60:
        return 'D'
    else:
        return 'F'

def calculate_class_statistics(students):
    """Calculate class-wide statistics."""
    if not students:
        return {}

    averages = [s['average'] for s in students if s['grades']]
    if not averages:
        return {}

    return {
        'total_students': len(students),
        'students_with_grades': len(averages),
        'class_average': sum(averages) / len(averages),
        'highest_average': max(averages),
        'lowest_average': min(averages),
        'grade_distribution': {
            'A': len([s for s in students if s.get('letter_grade') == 'A']),
            'B': len([s for s in students if s.get('letter_grade') == 'B']),
            'C': len([s for s in students if s.get('letter_grade') == 'C']),
            'D': len([s for s in students if s.get('letter_grade') == 'D']),
            'F': len([s for s in students if s.get('letter_grade') == 'F'])
        }
    }
```

### Phase 3: Report Generation (15 minutes)
```python
# report_generator.py
def generate_student_report(student):
    """Generate detailed report for a student."""
    report = f"""
Student Report: {student['name']} (ID: {student['id']})
{'='*50}
Individual Grades: {', '.join(map(str, student['grades']))}
Average Grade: {student['average']:.1f}
Letter Grade: {student['letter_grade']}

Performance Analysis:
"""

    if student['grades']:
        max_grade = max(student['grades'])
        min_grade = min(student['grades'])
        report += f"- Highest grade: {max_grade}\n"
        report += f"- Lowest grade: {min_grade}\n"
        report += f"- Grade range: {max_grade - min_grade}\n"
    else:
        report += "- No grades available\n"

    return report

def generate_class_summary(students):
    """Generate class summary report."""
    stats = calculate_class_statistics(students)

    if not stats:
        return "No data available for class summary."

    report = f"""
Class Summary Report
{'='*30}
Total Students: {stats['total_students']}
Students with Grades: {stats['students_with_grades']}
Class Average: {stats['class_average']:.1f}
Highest Average: {stats['highest_average']:.1f}
Lowest Average: {stats['lowest_average']:.1f}

Grade Distribution:
"""

    for grade, count in stats['grade_distribution'].items():
        percentage = (count / stats['total_students']) * 100
        report += f"{grade}: {count} students ({percentage:.1f}%)\n"

    return report

def export_to_file(data, filename, format_type='text'):
    """Export data to file in specified format."""
    try:
        with open(filename, 'w') as file:
            if format_type == 'csv':
                # Export as CSV
                if isinstance(data, list) and data:
                    # Write header
                    header = list(data[0].keys())
                    file.write(','.join(header) + '\n')

                    # Write data
                    for item in data:
                        row = [str(item.get(key, '')) for key in header]
                        file.write(','.join(row) + '\n')
            else:
                # Export as text
                file.write(str(data))

        print(f"Data exported to {filename}")
        return True

    except Exception as e:
        print(f"Error exporting data: {e}")
        return False
```

---

## V. User Interface and Testing (15 minutes)

### Main Program
```python
# main.py
import data_loader
import data_processor
import report_generator
from data_processor import calculate_class_statistics

def display_menu():
    """Display main menu."""
    print("\n" + "="*40)
    print("Student Grade Processor v1.0")
    print("="*40)
    print("1. Load student data")
    print("2. View all students")
    print("3. View student details")
    print("4. Generate class report")
    print("5. Export data")
    print("6. Exit")
    print("="*40)

def main():
    students = []

    while True:
        display_menu()
        choice = input("Choose option (1-6): ").strip()

        if choice == "1":
            # Load data
            filename = input("Enter CSV filename: ").strip()
            if not filename:
                filename = "sample_data.csv"
            students = data_loader.load_students_from_csv(filename)
            students = data_loader.validate_student_data(students)
            print(f"Loaded {len(students)} students")

        elif choice == "2":
            # View all students
            if not students:
                print("No student data loaded.")
                continue

            print("\nAll Students:")
            print("-" * 50)
            for student in students:
                print(f"ID: {student['id']}, Name: {student['name']}, "
                      f"Average: {student['average']:.1f}, Grade: {student['letter_grade']}")

        elif choice == "3":
            # View student details
            if not students:
                print("No student data loaded.")
                continue

            student_id = input("Enter student ID: ").strip()
            try:
                student_id = int(student_id)
                student = next((s for s in students if s['id'] == student_id), None)
                if student:
                    print(report_generator.generate_student_report(student))
                else:
                    print("Student not found.")
            except ValueError:
                print("Invalid student ID.")

        elif choice == "4":
            # Generate class report
            if not students:
                print("No student data loaded.")
                continue

            report = report_generator.generate_class_summary(students)
            print(report)

        elif choice == "5":
            # Export data
            if not students:
                print("No student data loaded.")
                continue

            filename = input("Enter export filename: ").strip()
            if not filename:
                filename = "exported_data.txt"

            format_choice = input("Export format (text/csv): ").strip().lower()
            if format_choice not in ['text', 'csv']:
                format_choice = 'text'

            if format_choice == 'text':
                data = report_generator.generate_class_summary(students)
            else:
                data = students

            report_generator.export_to_file(data, filename, format_choice)

        elif choice == "6":
            print("Goodbye!")
            break

        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
```

---

## VI. Wrap-Up and Assessment (10 minutes)

### Key Takeaways (5 minutes)
1. **Integration matters**: Combining all concepts creates powerful programs
2. **Modular design**: Separate concerns improve maintainability
3. **Error handling**: Robust programs handle edge cases gracefully
4. **User experience**: Good interfaces make programs usable

### Project Review Questions (3 minutes)
Students discuss:
1. What was the most challenging part?
2. How did modular design help?
3. What would you improve next time?

### Preview of Next Session (2 minutes)
"Final session: Review everything and create capstone projects!"

---

## Additional Resources
- **Sample data file**: sample_data.csv with test data
- **Project template**: Skeleton code to start with
- **Rubric**: Project evaluation criteria

**Session Time Check**: Intro (15) + Overview (20) + Planning (25) + Implementation (45) + UI/Testing (15) + Wrap-up (10) = 130 minutes (extended session)