# Session 1: What Is a Computer? How Programs Run

## Session Overview

Welcome to the first session of our introduction to programming course! Today we'll explore the fundamental question: what is a computer? We'll look at the main components that make up a computer system and understand, at a high level, how programs run on these machines. This conceptual foundation will help you understand why programming works the way it does, setting the stage for everything we'll learn in the coming weeks.

## Key Terms

- **CPU (Central Processing Unit)**: The "brain" of the computer that executes instructions
- **RAM (Random Access Memory)**: Temporary storage for data and programs currently in use
- **Storage**: Long-term storage for files and programs (hard drives, SSDs)
- **Input/Output (I/O) devices**: Hardware for getting data into and out of the computer (keyboard, mouse, screen, etc.)
- **Program**: A set of instructions that tells the computer what to do
- **Software**: Programs and data that tell hardware what to do
- **Hardware**: The physical components of a computer system

## Computer Components

### The CPU (Central Processing Unit)
The CPU is often called the "brain" of the computer. It's a small chip (about the size of a postage stamp) that:
- Executes instructions from programs
- Performs calculations and logical operations
- Coordinates all computer activities
- Works extremely fast (billions of operations per second)

Modern CPUs have multiple cores, allowing them to work on several tasks simultaneously.

### Memory (RAM)
RAM is the computer's short-term memory. It:
- Stores data and programs that are currently being used
- Is very fast to access but temporary (data is lost when power is turned off)
- Comes in different sizes (typically 8GB, 16GB, 32GB or more)
- Is different from storage - RAM is for active work, storage is for long-term keeping

### Storage
Storage is the computer's long-term memory. Common types include:
- **Hard Disk Drives (HDD)**: Traditional spinning disks, slower but cheaper
- **Solid State Drives (SSD)**: Flash memory, much faster but more expensive
- Stores the operating system, programs, and your files permanently

### Input and Output Devices
These are how we interact with computers:
- **Input devices**: Keyboard, mouse, touchscreen, microphone, camera
- **Output devices**: Monitor/screen, speakers, printer
- Allow humans to communicate with the computer and receive results

## What Is a Program?

A program is simply a set of instructions that tells a computer what to do. Think of it like a recipe:
- A recipe is a sequence of steps to prepare food
- A program is a sequence of steps to solve a problem or perform a task

Programs can be:
- **System software**: Operating systems, device drivers
- **Application software**: Word processors, games, web browsers
- **Utilities**: Tools for specific tasks

## How a Program Runs

When you click an app icon or run a program, here's what happens at a high level:

1. **The program is loaded** from storage into RAM
2. **The CPU starts executing** the program's instructions one by one
3. **Data flows** between CPU, RAM, and storage as needed
4. **Input/output happens** through devices when the program needs to interact with you
5. **The program finishes** when all instructions are complete

This process happens incredibly fast - millions or billions of instructions per second!

## Hardware vs Software

**Hardware** is the physical stuff you can touch:
- CPU, RAM, hard drive, keyboard, monitor, etc.

**Software** is the instructions and data:
- Operating systems (Windows, macOS, Linux)
- Applications (Chrome, Word, games)
- Your documents, photos, and files

Hardware provides the capability; software tells it what to do.

## Everyday Examples of Programs

Programs surround us in daily life:

- **Phone apps**: Calculator, camera, messaging apps
- **Web browsers**: Chrome, Firefox, Safari
- **Games**: From simple mobile games to complex 3D games
- **Smart devices**: Programs running in your thermostat, car, or refrigerator
- **Banking apps**: Transferring money, checking balances
- **Social media**: Posting, liking, scrolling through feeds

Each of these is a program - a set of instructions that makes the hardware do something useful.

## Why Computers Follow Instructions Exactly

Computers are literal thinkers:
- They do exactly what you tell them, nothing more, nothing less
- If instructions are wrong or incomplete, results will be wrong
- This is both a strength (consistency) and a limitation (no common sense)
- As programmers, we need to be precise and thorough

## From Human Idea to Running Program

The journey from a human idea to a working program involves several steps:

1. **Human has an idea**: "I want to make an app that helps people track their expenses"
2. **Break down the idea**: What features? Who will use it? How will it work?
3. **Write the program**: Using a programming language to express the solution
4. **Test and debug**: Make sure it works correctly
5. **Deploy**: Make it available for others to use

We'll learn each of these steps throughout this course.

## Summary and Checklist

### What We Covered Today
- ✅ Basic computer components (CPU, RAM, storage, I/O)
- ✅ Difference between hardware and software
- ✅ What programs are and how they run
- ✅ Why computers follow instructions literally
- ✅ Examples of programs in everyday life

### Self-Check Questions
- Can you name the four main components of a computer?
- What's the difference between RAM and storage?
- Why do computers need to follow instructions exactly?
- Can you think of 3 programs you used today?

### Key Takeaway
Computers are sophisticated tools that follow our instructions precisely. Understanding how they work helps us write better programs and troubleshoot issues when things go wrong.

## Next Steps

In our next session, we'll explore how human-readable source code gets converted into the 0s and 1s that computers actually understand. This will help you understand why programming languages exist and how they bridge the gap between humans and machines.

## Connection to Future Sessions

This session lays the groundwork for understanding:
- **Session 2**: How source code becomes machine code
- **Session 3**: How information is represented as bits and bytes
- **All future sessions**: Why we program the way we do

## Concepts Materials

This session includes detailed concept articles in the `concepts/` folder to supplement the lecture material:

### 🔄 [Process Lifecycle](concepts/process-lifecycle.md)
Learn how programs come to life as processes, from creation to termination. Understand process states, resource management, and the operating system's role in process coordination.

### 🧠 [Memory Architecture](concepts/memory-architecture.md)
Explore how computers organize and manage memory. Learn about RAM, cache memory, virtual memory, and the memory hierarchy that makes computers efficient.

### 📁 [File System](concepts/file-system.md)
Understand how data is organized on storage devices. Learn about file system structures, directory hierarchies, file operations, and common file system types.

### 🔢 [Binary Format](concepts/binary-format.md)
Discover why computers use binary (0s and 1s) and how all digital information is represented. Learn about binary operations, data encoding, and why binary is fundamental to computing.

### ⚙️ [Operating System](concepts/operating-system.md)
Explore the software that manages your computer. Learn about OS responsibilities, the boot process, system architecture, and how operating systems coordinate hardware and software.

## Further Reading (Optional)

- "Computer Science: An Interdisciplinary Approach" by Sedgewick and Wayne (Chapter 1)
- Khan Academy: "What is a computer?"
- Crash Course Computer Science (YouTube series, Episodes 1-3)