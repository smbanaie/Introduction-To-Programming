# Session 9: Pseudocode & Control Structures

## Lecture Overview
**Duration**: 90 minutes
**Objectives**: Students will learn to write algorithms in pseudocode with control structures
**Materials**: Whiteboard, pseudocode templates, control structure flowchart symbols

---

## I. Introduction (15 minutes)

### Review and Hook (5 minutes)
- **Quick Review**: What are the key characteristics of algorithms?
- **Hook Activity**: Show messy code vs clean pseudocode
- **Question**: "How can we write algorithms that computers AND humans can understand?"

### Learning Goals (5 minutes)
By the end of this session, you will be able to:
- Write clear pseudocode algorithms
- Use control structures (sequence, selection, iteration)
- Convert problems to structured pseudocode
- Understand pseudocode as programming preparation

### Agenda Overview (5 minutes)
1. Introduction to pseudocode
2. Control structures fundamentals
3. Writing pseudocode algorithms
4. Practice and application

---

## II. Main Content (50 minutes)

### A. Pseudocode Fundamentals (15 minutes)

#### What is Pseudocode?
- **Pseudocode**: Structured English for writing algorithms
- **Not code**: Not programming language syntax
- **Readable**: Easy for humans to understand
- **Precise**: Clear enough for computer translation

#### Pseudocode Principles
- **Natural language**: Use English words and phrases
- **Structured format**: Consistent indentation and formatting
- **Clear operations**: Unambiguous actions described
- **Modular design**: Break complex tasks into smaller steps

#### Pseudocode Example
```
Algorithm: Calculate Average Grade
INPUT: List of student grades
OUTPUT: Average grade

total = 0
count = 0
FOR EACH grade IN grades DO
    total = total + grade
    count = count + 1
END FOR

IF count > 0 THEN
    average = total / count
    DISPLAY average
ELSE
    DISPLAY "No grades entered"
END IF
```

### B. Control Structures (20 minutes)

#### Three Fundamental Structures

##### 1. Sequence (Straight Line)
```
Statement 1
Statement 2
Statement 3
```
- **Purpose**: Execute steps in order
- **Example**: Following a recipe step-by-step

##### 2. Selection (Decision Making)
```
IF condition THEN
    action1
ELSE
    action2
END IF
```
- **Purpose**: Choose between alternatives
- **Example**: "If it rains, take umbrella, else wear sunglasses"

##### 3. Iteration (Looping)
```
WHILE condition DO
    action
END WHILE

OR

FOR counter FROM start TO end DO
    action
END FOR
```
- **Purpose**: Repeat actions until condition met
- **Example**: "Keep stirring until mixture thickens"

#### Control Structure Symbols
```
Sequence: → (straight arrow)
Selection: ◇ (diamond for decision)
Iteration: ○ (circle for loop)
```

#### Complex Control Structures
- **Nested IF**: Decisions inside decisions
- **Nested loops**: Loops inside loops
- **Combined structures**: Mix sequence, selection, iteration

### C. Writing Pseudocode Algorithms (15 minutes)

#### Problem to Pseudocode Process
1. **Understand problem**: What input? What output?
2. **Identify steps**: Break into sequence
3. **Add decisions**: Where choices needed?
4. **Add loops**: Where repetition needed?
5. **Test mentally**: Walk through with sample data

#### Pseudocode Templates

**Decision Template:**
```
IF condition THEN
    true_actions
ELSE
    false_actions
END IF
```

**Loop Template:**
```
WHILE condition DO
    repeated_actions
END WHILE
```

**Function Template:**
```
FUNCTION function_name(parameters)
    statements
    RETURN result
END FUNCTION
```

#### Common Pseudocode Keywords
- **Input/Output**: READ, DISPLAY, INPUT, OUTPUT
- **Assignment**: =, ←
- **Control**: IF/THEN/ELSE, WHILE/DO, FOR/TO
- **Logic**: AND, OR, NOT
- **Comparison**: =, ≠, <, >, ≤, ≥

---

## III. Interactive Activities (15 minutes)

### Pseudocode Translation (10 minutes)
- **Groups**: Convert plain English instructions to pseudocode
- **Examples**: Daily routines, game rules, math problems
- **Focus**: Use proper control structures and formatting

### Algorithm Debugging (5 minutes)
- **Activity**: Review pseudocode for clarity and correctness
- **Check**: Are control structures used properly? Is logic sound?
- **Improve**: Suggest clearer alternatives

---

## IV. Wrap-Up and Assessment (10 minutes)

### Key Takeaways (5 minutes)
1. **Pseudocode bridges thinking and coding**: Human-readable algorithm representation
2. **Control structures provide logic**: Sequence, selection, iteration cover all programming needs
3. **Structured format improves clarity**: Consistent indentation and keywords
4. **Practice makes perfect**: Writing pseudocode develops algorithmic thinking

### Exit Ticket Questions (3 minutes)
Students write answers to:
1. What is pseudocode and why use it?
2. Name the three control structures
3. Write pseudocode for "Count to 10"

### Preview of Next Module (2 minutes)
"Next module we'll start learning Python - turning algorithms into real programs!"

---

## Additional Resources
- **Visual Aid**: Control structure flowchart symbols
- **Handout**: Pseudocode keyword reference
- **Homework**: Write pseudocode for a simple game

**Session Time Check**: Intro (15) + Main (50) + Activities (15) + Wrap-up (10) = 90 minutes