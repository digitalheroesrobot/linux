# Linux Commands for Python, C, and Desktop Application Developers
## University Computer Science Course
### Developer CLI — Focused on Python, C/C++, GUI, Native Applications, Debugging, and Build Systems

> **Scope**
>
> This course is for university students and developers building:
>
> - Python applications
> - C applications
> - C++ applications
> - Linux desktop applications
> - GTK applications
> - Qt applications
> - Native GUI applications
> - Command-line applications
> - Shared libraries
> - System-integrated desktop software
>
> This course intentionally avoids duplicating the RPM/DNF package-management course and the Web/Android developer course.
>
> The emphasis here is on:
>
> ```text
> Python runtime
> C/C++ compilation
> GCC/GDB
> Make/CMake
> shared libraries
> ELF binaries
> debugging
> profiling
> GUI applications
> core dumps
> dynamic linking
> build automation
> ```
>
> Package-manager commands are intentionally excluded.

---

# Table of Contents

1. [Developer Mindset](#1-developer-mindset)
2. [Python Runtime Inspection](#2-python-runtime-inspection)
3. [Python Interactive Execution](#3-python-interactive-execution)
4. [Python Modules and Imports](#4-python-modules-and-imports)
5. [Python Virtual Environments](#5-python-virtual-environments)
6. [Python Project Execution](#6-python-project-execution)
7. [Python Debugging](#7-python-debugging)
8. [Python Profiling](#8-python-profiling)
9. [Python Bytecode and Compilation](#9-python-bytecode-and-compilation)
10. [Python Environment Diagnostics](#10-python-environment-diagnostics)
11. [C Compiler Fundamentals](#11-c-compiler-fundamentals)
12. [GCC Compilation](#12-gcc-compilation)
13. [Compilation Stages](#13-compilation-stages)
14. [Preprocessor](#14-preprocessor)
15. [Assembly](#15-assembly)
16. [Object Files](#16-object-files)
17. [Linking](#17-linking)
18. [Static Libraries](#18-static-libraries)
19. [Shared Libraries](#19-shared-libraries)
20. [ELF Executables](#20-elf-executables)
21. [Binary Inspection](#21-binary-inspection)
22. [C Debugging with GDB](#22-c-debugging-with-gdb)
23. [GDB Breakpoints](#23-gdb-breakpoints)
24. [GDB Stack and Memory](#24-gdb-stack-and-memory)
25. [GDB Core Dumps](#25-gdb-core-dumps)
26. [Sanitizers](#26-sanitizers)
27. [Memory Debugging](#27-memory-debugging)
28. [strace](#28-strace)
29. [ltrace](#29-ltrace)
30. [Native Performance Profiling](#30-native-performance-profiling)
31. [Make](#31-make)
32. [Makefile Structure](#32-makefile-structure)
33. [CMake](#33-cmake)
34. [CMake Build Workflow](#34-cmake-build-workflow)
35. [Ninja](#35-ninja)
36. [Compiler Diagnostics](#36-compiler-diagnostics)
37. [C++ Development](#37-c-development)
38. [Desktop GUI Development](#38-desktop-gui-development)
39. [GTK Development](#39-gtk-development)
40. [Qt Development](#40-qt-development)
41. [Desktop Application Execution](#41-desktop-application-execution)
42. [Display and GUI Environment](#42-display-and-gui-environment)
43. [X11 and Wayland Diagnostics](#43-x11-and-wayland-diagnostics)
44. [Desktop Application Debugging](#44-desktop-application-debugging)
45. [Desktop Application Logs](#45-desktop-application-logs)
46. [Configuration and User Data](#46-configuration-and-user-data)
47. [Shared Library Troubleshooting](#47-shared-library-troubleshooting)
48. [Build Reproducibility](#48-build-reproducibility)
49. [Developer Automation](#49-developer-automation)
50. [University Laboratory Exercises](#50-university-laboratory-exercises)
51. [12-Week Course Plan](#51-12-week-course-plan)
52. [Developer Cheat Sheet](#52-developer-cheat-sheet)

---

# 1. Developer Mindset

For Python, C, and desktop application development, Linux is not just an operating system.

It is a complete development platform:

```text
Source Code
    │
    ├── Python interpreter
    │
    ├── C/C++ compiler
    │
    ├── assembler
    │
    ├── linker
    │
    ├── debugger
    │
    ├── profiler
    │
    └── GUI framework
            │
            ▼
       Executable
            │
            ▼
       Linux process
            │
            ├── memory
            ├── files
            ├── libraries
            ├── system calls
            └── GUI/display
```

The important developer question is not:

> "Which command do I type?"

It is:

> "At which layer is my program failing?"

---

# 2. Python Runtime Inspection

Check Python:

```bash
python3 --version
```

Locate executable:

```bash
command -v python3
```

Show Python installation:

```bash
python3 -c 'import sys; print(sys.executable)'
```

Python version:

```bash
python3 -c 'import sys; print(sys.version)'
```

Platform:

```bash
python3 -c 'import platform; print(platform.platform())'
```

Architecture:

```bash
python3 -c 'import platform; print(platform.machine())'
```

---

# 3. Python Interactive Execution

Start interpreter:

```bash
python3
```

Execute one statement:

```bash
python3 -c 'print("Hello Linux")'
```

Execute multiple statements:

```bash
python3 -c 'x=10; y=20; print(x+y)'
```

Execute a module:

```bash
python3 -m module_name
```

This is particularly useful because:

```bash
python3 -m pip
python3 -m venv
python3 -m unittest
```

ensures the module is executed by the selected Python interpreter.

---

# 4. Python Modules and Imports

Check whether a module can be imported:

```bash
python3 -c 'import numpy; print(numpy.__version__)'
```

Show module location:

```bash
python3 -c 'import numpy; print(numpy.__file__)'
```

Show Python search path:

```bash
python3 -c 'import sys; print("\n".join(sys.path))'
```

Inspect module:

```bash
python3 -c 'import os; print(os.__file__)'
```

Find import problems:

```bash
python3 -c 'import problematic_module'
```

The traceback often immediately identifies:

```text
missing module
wrong Python version
wrong environment
import path problem
```

---

# 5. Python Virtual Environments

Create:

```bash
python3 -m venv .venv
```

Activate:

```bash
source .venv/bin/activate
```

Verify:

```bash
python -c 'import sys; print(sys.executable)'
```

Deactivate:

```bash
deactivate
```

A virtual environment is useful because:

```text
Project A
    └── Python environment A

Project B
    └── Python environment B
```

can use different dependencies without mixing them.

---

# 6. Python Project Execution

Run a script:

```bash
python3 app.py
```

Run a module:

```bash
python3 -m myapp
```

Run tests:

```bash
python3 -m unittest
```

Run a specific test:

```bash
python3 -m unittest tests.test_api
```

Compile-check source:

```bash
python3 -m py_compile app.py
```

This detects many syntax errors without running the application.

---

# 7. Python Debugging

Python includes a debugger:

```bash
python3 -m pdb app.py
```

Useful interactive commands include:

```text
break
continue
next
step
where
list
print
quit
```

Example:

```bash
python3 -m pdb app.py
```

At a breakpoint:

```text
(Pdb) list
(Pdb) next
(Pdb) print(variable)
(Pdb) continue
```

---

# 8. Python Profiling

Basic profiling:

```bash
python3 -m cProfile app.py
```

Save profiling data:

```bash
python3 -m cProfile -o profile.out app.py
```

Inspect:

```bash
python3 -m pstats profile.out
```

Sort by cumulative time inside `pstats`:

```text
sort cumulative
stats
```

Profiling answers:

```text
Where does the program spend time?
Which function is called most?
Which functions dominate execution time?
```

---

# 9. Python Bytecode and Compilation

Compile:

```bash
python3 -m compileall .
```

Python bytecode normally appears under:

```text
__pycache__/
```

Inspect:

```bash
find . -type f -name '*.pyc'
```

Disassemble Python bytecode:

```bash
python3 -m dis app.py
```

Or:

```bash
python3 -c 'import dis; dis.dis("x = 1 + 2")'
```

This is useful for advanced Python runtime studies.

---

# 10. Python Environment Diagnostics

Show environment:

```bash
python3 -c 'import sys; print(sys.executable); print(sys.version)'
```

Show installation paths:

```bash
python3 -c 'import site; print(site.getsitepackages())'
```

User site:

```bash
python3 -c 'import site; print(site.getusersitepackages())'
```

Show environment variables visible to Python:

```bash
python3 -c 'import os; print(os.environ.get("PATH"))'
```

---

# 11. C Compiler Fundamentals

A typical C development pipeline is:

```text
hello.c
  │
  ▼
Preprocessor
  │
  ▼
Compiler
  │
  ▼
Assembly
  │
  ▼
Assembler
  │
  ▼
Object file
  │
  ▼
Linker
  │
  ▼
Executable
```

The GNU C compiler driver is:

```bash
gcc
```

Check:

```bash
gcc --version
```

---

# 12. GCC Compilation

Compile:

```bash
gcc hello.c
```

Output defaults to:

```text
a.out
```

Specify output:

```bash
gcc hello.c -o hello
```

Run:

```bash
./hello
```

Compile with warnings:

```bash
gcc -Wall -Wextra hello.c -o hello
```

Debug build:

```bash
gcc -g hello.c -o hello
```

Optimization:

```bash
gcc -O2 hello.c -o hello
```

A useful development command:

```bash
gcc -Wall -Wextra -g -O0 hello.c -o hello
```

---

# 13. Compilation Stages

Compile only to preprocessed output:

```bash
gcc -E hello.c -o hello.i
```

Compile to assembly:

```bash
gcc -S hello.c -o hello.s
```

Compile to object:

```bash
gcc -c hello.c -o hello.o
```

Link:

```bash
gcc hello.o -o hello
```

Therefore:

```text
hello.c
   │
   ├── gcc -E → hello.i
   │
   ├── gcc -S → hello.s
   │
   ├── gcc -c → hello.o
   │
   └── gcc     → hello
```

Understanding these stages is essential for C debugging.

---

# 14. Preprocessor

Inspect preprocessed code:

```bash
gcc -E hello.c
```

Save:

```bash
gcc -E hello.c -o hello.i
```

Show predefined macros:

```bash
gcc -dM -E - < /dev/null
```

Define macro:

```bash
gcc -DDEBUG hello.c -o hello
```

Define value:

```bash
gcc -DVERSION=3 hello.c -o hello
```

This is useful for conditional compilation:

```c
#ifdef DEBUG
...
#endif
```

---

# 15. Assembly

Generate assembly:

```bash
gcc -S hello.c -o hello.s
```

Inspect:

```bash
less hello.s
```

For Intel syntax with GCC:

```bash
gcc -S -masm=intel hello.c -o hello.s
```

Assembly is useful when studying:

```text
function calls
registers
stack frames
optimization
ABI
compiler output
```

---

# 16. Object Files

Compile:

```bash
gcc -c hello.c -o hello.o
```

Inspect:

```bash
file hello.o
```

Symbols:

```bash
nm hello.o
```

Sections:

```bash
objdump -h hello.o
```

Disassemble:

```bash
objdump -d hello.o
```

---

# 17. Linking

Multiple source files:

```text
main.c
math.c
```

Compile:

```bash
gcc -c main.c
gcc -c math.c
```

Link:

```bash
gcc main.o math.o -o calculator
```

One-step:

```bash
gcc main.c math.c -o calculator
```

The linker resolves:

```text
function references
global symbols
libraries
relocations
```

---

# 18. Static Libraries

Create object:

```bash
gcc -c math.c -o math.o
```

Create static library:

```bash
ar rcs libmath.a math.o
```

Inspect:

```bash
ar -t libmath.a
```

Link:

```bash
gcc main.c -L. -lmath -o calculator
```

Meaning:

```text
-L.      search current directory
-lmath   use libmath.a or compatible library
```

---

# 19. Shared Libraries

Compile position-independent code:

```bash
gcc -fPIC -c math.c -o math.o
```

Build shared library:

```bash
gcc -shared -o libmath.so math.o
```

Link application:

```bash
gcc main.c -L. -lmath -o calculator
```

The executable may then depend on:

```text
libmath.so
```

Inspect:

```bash
ldd ./calculator
```

---

# 20. ELF Executables

Linux native executables commonly use:

```text
ELF
```

Check:

```bash
file ./hello
```

Typical output identifies:

```text
ELF
64-bit
architecture
dynamically linked/static
debug information
```

ELF is the executable/object-file format used by Linux on common architectures.

---

# 21. Binary Inspection

## file

```bash
file ./hello
```

## readelf

Headers:

```bash
readelf -h ./hello
```

Sections:

```bash
readelf -S ./hello
```

Program headers:

```bash
readelf -l ./hello
```

Symbols:

```bash
readelf -s ./hello
```

Dynamic section:

```bash
readelf -d ./hello
```

## nm

```bash
nm ./hello
```

Dynamic symbols:

```bash
nm -D ./hello
```

## objdump

Disassemble:

```bash
objdump -d ./hello
```

---

# 22. C Debugging with GDB

Compile with debug symbols:

```bash
gcc -g -O0 main.c -o app
```

Start:

```bash
gdb ./app
```

Run:

```text
(gdb) run
```

Quit:

```text
(gdb) quit
```

---

# 23. GDB Breakpoints

Set breakpoint:

```text
(gdb) break main
```

Run:

```text
(gdb) run
```

Next line:

```text
(gdb) next
```

Step into function:

```text
(gdb) step
```

Continue:

```text
(gdb) continue
```

List source:

```text
(gdb) list
```

Show current function:

```text
(gdb) where
```

---

# 24. GDB Stack and Memory

Backtrace:

```text
(gdb) bt
```

Local variables:

```text
(gdb) info locals
```

Function arguments:

```text
(gdb) info args
```

Print variable:

```text
(gdb) print variable
```

Examine memory:

```text
(gdb) x/16x variable
```

Registers:

```text
(gdb) info registers
```

This is essential for:

```text
segmentation faults
pointer bugs
stack corruption
memory corruption
```

---

# 25. GDB Core Dumps

A core dump records process state after a fatal crash.

Enable:

```bash
ulimit -c unlimited
```

Run the application:

```bash
./app
```

If a core dump is generated, inspect:

```bash
gdb ./app core
```

Then:

```text
(gdb) bt
(gdb) info locals
(gdb) info threads
```

The most useful first command is usually:

```text
bt
```

---

# 26. Sanitizers

Compile with AddressSanitizer:

```bash
gcc -g -fsanitize=address -fno-omit-frame-pointer app.c -o app
```

Run:

```bash
./app
```

ASan can detect problems such as:

```text
buffer overflow
use-after-free
stack overflow
double free
invalid memory access
```

UndefinedBehaviorSanitizer:

```bash
gcc -g -fsanitize=undefined app.c -o app
```

Use both where appropriate:

```bash
gcc -g \
  -fsanitize=address,undefined \
  -fno-omit-frame-pointer \
  app.c -o app
```

---

# 27. Memory Debugging

A common tool is:

```bash
valgrind
```

Run:

```bash
valgrind ./app
```

Memory-checking:

```bash
valgrind --leak-check=full ./app
```

Track origins:

```bash
valgrind --track-origins=yes ./app
```

Valgrind can help identify:

```text
invalid reads
invalid writes
memory leaks
use of uninitialized values
```

For many modern builds, compiler sanitizers are faster and easier for initial debugging.

---

# 28. strace

`strace` traces Linux system calls.

Run:

```bash
strace ./app
```

Save:

```bash
strace -o trace.log ./app
```

Trace file operations:

```bash
strace -e trace=file ./app
```

Trace network calls:

```bash
strace -e trace=network ./app
```

Trace process operations:

```bash
strace -e trace=process ./app
```

This is extremely useful when an application says:

```text
File not found
Permission denied
Cannot open configuration
Cannot connect
```

---

# 29. ltrace

`ltrace` traces many library calls.

Run:

```bash
ltrace ./app
```

This can reveal calls to:

```text
libc
shared libraries
dynamic functions
```

Comparison:

```text
strace → system calls
ltrace → library calls
```

This distinction is important.

---

# 30. Native Performance Profiling

A common Linux profiling tool is:

```bash
perf
```

Record:

```bash
perf record ./app
```

View:

```bash
perf report
```

Statistical sampling:

```bash
perf stat ./app
```

This can report metrics such as:

```text
task-clock
context switches
CPU cycles
instructions
branches
cache behavior
```

---

# 31. Make

A simple project:

```text
main.c
math.c
math.h
```

Compile manually:

```bash
gcc -c main.c
gcc -c math.c
gcc main.o math.o -o calculator
```

Make automates this process.

Run:

```bash
make
```

Clean:

```bash
make clean
```

Force rebuild:

```bash
make -B
```

List targets:

```bash
make -n
```

---

# 32. Makefile Structure

Example:

```make
CC=gcc
CFLAGS=-Wall -Wextra -g

calculator: main.o math.o
	$(CC) $(CFLAGS) main.o math.o -o calculator

main.o: main.c math.h
	$(CC) $(CFLAGS) -c main.c

math.o: math.c math.h
	$(CC) $(CFLAGS) -c math.c

clean:
	rm -f calculator *.o
```

Run:

```bash
make
```

Clean:

```bash
make clean
```

Make's central idea is:

```text
target
  ↓
dependencies
  ↓
commands
```

---

# 33. CMake

CMake generates build-system files.

Check:

```bash
cmake --version
```

Typical project:

```text
project/
├── CMakeLists.txt
├── src/
└── include/
```

Create build directory:

```bash
mkdir build
```

Configure:

```bash
cmake -S . -B build
```

Build:

```bash
cmake --build build
```

Clean/rebuild:

```bash
cmake --build build --clean-first
```

---

# 34. CMake Build Workflow

Recommended out-of-source build:

```bash
cmake -S . -B build
cmake --build build
```

Debug configuration:

```bash
cmake -S . -B build -DCMAKE_BUILD_TYPE=Debug
```

Release:

```bash
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release
```

Run:

```bash
./build/myapp
```

Inspect configuration:

```bash
cmake -S . -B build
```

---

# 35. Ninja

Ninja is a fast build system commonly generated by CMake.

Configure:

```bash
cmake -S . -B build -G Ninja
```

Build:

```bash
ninja -C build
```

Clean:

```bash
ninja -C build clean
```

This is especially useful for:

```text
large C++ projects
GUI applications
incremental builds
```

---

# 36. Compiler Diagnostics

Warnings are extremely important.

Use:

```bash
gcc -Wall -Wextra
```

Additional useful warnings:

```bash
gcc -Wall -Wextra -Wpedantic
```

For C++:

```bash
g++ -Wall -Wextra -Wpedantic
```

Treat warnings as errors:

```bash
gcc -Wall -Wextra -Werror app.c -o app
```

Do this selectively because third-party code may produce warnings that are outside your control.

---

# 37. C++ Development

C++ compiler:

```bash
g++
```

Version:

```bash
g++ --version
```

Compile:

```bash
g++ main.cpp -o app
```

Warnings:

```bash
g++ -Wall -Wextra -Wpedantic main.cpp -o app
```

Debug:

```bash
g++ -g -O0 main.cpp -o app
```

Multiple files:

```bash
g++ main.cpp widget.cpp model.cpp -o app
```

Debug with GDB:

```bash
gdb ./app
```

---

# 38. Desktop GUI Development

Linux desktop applications commonly use:

```text
GTK
Qt
SDL
Dear ImGui
wxWidgets
Electron
Python GUI frameworks
```

This course focuses primarily on native Linux GUI concepts.

Typical architecture:

```text
Application
   │
   ├── GUI toolkit
   │
   ├── graphics subsystem
   │
   ├── display server
   │
   └── Linux process/system calls
```

---

# 39. GTK Development

GTK applications can be built in C.

Typical development commands depend on the installed GTK version.

A project may use:

```text
gcc
pkg-config
cmake
meson
ninja
```

Query GTK compiler flags:

```bash
pkg-config --cflags gtk4
```

Libraries:

```bash
pkg-config --libs gtk4
```

Check whether GTK is discoverable:

```bash
pkg-config --modversion gtk4
```

This is an important desktop-development pattern:

```text
pkg-config
    ↓
compiler flags
    ↓
linker flags
```

---

# 40. Qt Development

Qt applications commonly use:

```text
C++
CMake
qmake
Qt tools
```

CMake-based Qt projects can be configured:

```bash
cmake -S . -B build
```

Build:

```bash
cmake --build build
```

Run:

```bash
./build/myapp
```

Qt projects often produce:

```text
GUI executable
shared libraries
resources
plugins
```

---

# 41. Desktop Application Execution

Run:

```bash
./myapp
```

Run with environment variable:

```bash
QT_DEBUG_PLUGINS=1 ./myapp
```

Run with debug output:

```bash
G_MESSAGES_DEBUG=all ./myapp
```

The exact environment variables depend on the GUI framework.

Redirect output:

```bash
./myapp > app.log 2>&1
```

Separate standard output and errors:

```bash
./myapp > stdout.log 2> stderr.log
```

---

# 42. Display and GUI Environment

Check display environment:

```bash
printf '%s\n' "$DISPLAY"
```

Wayland:

```bash
printf '%s\n' "$WAYLAND_DISPLAY"
```

Desktop session:

```bash
printf '%s\n' "$XDG_SESSION_TYPE"
```

Desktop:

```bash
printf '%s\n' "$XDG_CURRENT_DESKTOP"
```

These variables help explain:

```text
Why GUI application cannot open
Why remote GUI fails
Why application chooses X11 vs Wayland
```

---

# 43. X11 and Wayland Diagnostics

Check session:

```bash
echo "$XDG_SESSION_TYPE"
```

Possible values:

```text
x11
wayland
```

X11 display:

```bash
echo "$DISPLAY"
```

Wayland display:

```bash
echo "$WAYLAND_DISPLAY"
```

GUI applications launched from a terminal inherit these environment variables.

A missing or incorrect display environment is a common cause of:

```text
cannot open display
GUI application does not start
remote GUI problems
```

---

# 44. Desktop Application Debugging

A practical debugging sequence:

```text
1. Can executable start?
2. Is the binary valid?
3. Are shared libraries available?
4. Is the display environment valid?
5. Does the application produce errors?
6. Does it crash?
7. Can GDB reproduce the crash?
8. Can strace identify missing resources?
9. Can sanitizers identify memory bugs?
10. Can profiling identify performance problems?
```

Useful commands:

```bash
file ./myapp
ldd ./myapp
./myapp
strace ./myapp
gdb ./myapp
```

---

# 45. Desktop Application Logs

Capture stdout/stderr:

```bash
./myapp > app.log 2>&1
```

Follow a log:

```bash
tail -f app.log
```

Search:

```bash
grep -i error app.log
```

Search warnings:

```bash
grep -i warning app.log
```

GUI applications may also log through the desktop/system logging infrastructure.

---

# 46. Configuration and User Data

Desktop applications often store user data under:

```text
~/.config/
~/.local/share/
~/.cache/
```

Python applications may use:

```text
~/.config/myapp/
```

Inspect:

```bash
ls -la ~/.config/
```

Application-specific configuration:

```bash
ls -la ~/.config/myapp/
```

Cache:

```bash
ls -la ~/.cache/
```

This is useful when:

```text
application settings are corrupted
GUI state is broken
old configuration survives reinstall
cache causes unexpected behavior
```

---

# 47. Shared Library Troubleshooting

Check:

```bash
ldd ./myapp
```

Look for:

```text
not found
```

Example diagnostic:

```bash
ldd ./myapp | grep 'not found'
```

Inspect dynamic dependencies:

```bash
readelf -d ./myapp
```

Look for required libraries:

```bash
readelf -d ./myapp | grep NEEDED
```

Inspect RPATH/RUNPATH:

```bash
readelf -d ./myapp | grep -E 'RPATH|RUNPATH'
```

This is one of the most important native Linux debugging workflows.

---

# 48. Build Reproducibility

A developer should record:

```text
compiler version
Python version
CMake version
build type
architecture
compiler flags
source revision
```

Compiler:

```bash
gcc --version
```

CMake:

```bash
cmake --version
```

Python:

```bash
python3 --version
```

Architecture:

```bash
uname -m
```

Git revision:

```bash
git rev-parse HEAD
```

A reproducible build should be explainable:

```text
source revision
+
toolchain
+
configuration
=
binary
```

---

# 49. Developer Automation

Run a build:

```bash
cmake --build build
```

Then run tests:

```bash
ctest --test-dir build
```

Then run application:

```bash
./build/myapp
```

A shell script can combine them:

```bash
#!/usr/bin/env bash
set -e

cmake -S . -B build -DCMAKE_BUILD_TYPE=Debug
cmake --build build
ctest --test-dir build
./build/myapp
```

`set -e` makes the script stop when a command fails.

---

# 50. University Laboratory Exercises

## Lab 1 — Python Environment

Students should report:

```bash
python3 --version
python3 -c 'import sys; print(sys.executable)'
python3 -c 'import sys; print(sys.path)'
python3 -c 'import platform; print(platform.platform())'
```

Explain how Python finds modules.

---

## Lab 2 — Python Virtual Environment

Create:

```bash
python3 -m venv .venv
```

Activate:

```bash
source .venv/bin/activate
```

Demonstrate that:

```bash
python -c 'import sys; print(sys.executable)'
```

points into `.venv`.

---

## Lab 3 — Python Debugging

Create a Python program containing a deliberate logic error.

Debug:

```bash
python3 -m pdb app.py
```

Submit:

```text
bug
breakpoint
observed state
root cause
solution
```

---

## Lab 4 — C Compilation Pipeline

Given:

```text
hello.c
```

Produce:

```bash
gcc -E hello.c -o hello.i
gcc -S hello.c -o hello.s
gcc -c hello.c -o hello.o
gcc hello.o -o hello
```

Explain each intermediate file.

---

## Lab 5 — ELF Investigation

Compile:

```bash
gcc -g hello.c -o hello
```

Then:

```bash
file hello
readelf -h hello
readelf -S hello
readelf -d hello
nm hello
objdump -d hello
```

Students should explain:

```text
ELF header
sections
dynamic dependencies
symbols
machine instructions
```

---

## Lab 6 — GDB

Create a C program with a deliberate segmentation fault.

Compile:

```bash
gcc -g -O0 crash.c -o crash
```

Debug:

```bash
gdb ./crash
```

Use:

```text
run
bt
frame
info locals
print
```

Identify the exact source line causing the crash.

---

## Lab 7 — Memory Bug

Create a program with:

```text
buffer overflow
use-after-free
memory leak
```

Test with:

```bash
-fsanitize=address
```

Then compare with:

```bash
valgrind
```

Write a comparison report.

---

## Lab 8 — System Call Investigation

Run:

```bash
strace ./app
```

Then:

```bash
strace -e trace=file ./app
```

Determine:

```text
which files the application opens
which files are missing
which system calls fail
```

---

## Lab 9 — Shared Library

Create:

```text
libmath.so
```

Link an application against it.

Then:

```bash
ldd ./app
readelf -d ./app
```

Explain how Linux finds the shared library.

---

## Lab 10 — CMake Project

Create:

```text
project/
├── CMakeLists.txt
├── src/
└── include/
```

Build:

```bash
cmake -S . -B build
cmake --build build
```

Then:

```bash
ctest --test-dir build
```

---

## Lab 11 — GUI Application

Build a small GTK or Qt application.

Investigate:

```bash
echo "$DISPLAY"
echo "$WAYLAND_DISPLAY"
echo "$XDG_SESSION_TYPE"
```

Run the application and capture logs.

---

## Lab 12 — Final Native Application Debugging Project

Students receive a deliberately broken desktop application.

Possible problems:

```text
Python import failure
C segmentation fault
missing shared library
GUI initialization failure
memory leak
incorrect CMake configuration
runtime configuration problem
```

Students must submit:

```text
symptom
hypothesis
command
evidence
root cause
fix
verification
```

---

# 51. 12-Week Course Plan

## Week 1 — Python Runtime

```text
python3
sys
platform
modules
virtual environments
```

---

## Week 2 — Python Debugging

```text
pdb
tracebacks
profiling
bytecode
```

---

## Week 3 — C Compilation

```text
gcc
preprocessor
compiler
assembly
object files
linker
```

---

## Week 4 — ELF and Libraries

```text
ELF
readelf
nm
objdump
static libraries
shared libraries
ldd
```

---

## Week 5 — GDB

```text
breakpoints
stack
frames
variables
memory
core dumps
```

---

## Week 6 — Memory Debugging

```text
AddressSanitizer
UndefinedBehaviorSanitizer
Valgrind
```

---

## Week 7 — System-Level Debugging

```text
strace
ltrace
system calls
library calls
```

---

## Week 8 — Build Systems

```text
Make
Makefile
dependencies
incremental builds
```

---

## Week 9 — CMake/Ninja

```text
CMake
out-of-source builds
Debug/Release
Ninja
CTest
```

---

## Week 10 — Desktop GUI

```text
GTK
Qt
X11
Wayland
display environment
GUI diagnostics
```

---

## Week 11 — Native Application Performance

```text
perf
CPU profiling
memory profiling
shared libraries
runtime diagnostics
```

---

## Week 12 — Final Project

Build and debug a complete native application:

```text
Python or C/C++
        │
        ▼
GUI
        │
        ▼
Build system
        │
        ▼
Native/Linux runtime
        │
        ├── debugging
        ├── logging
        ├── profiling
        └── packaging-ready artifact
```

---

# 52. Developer Cheat Sheet

## Python

```bash
python3 --version
python3 -c 'import sys; print(sys.executable)'
python3 -c 'import sys; print(sys.path)'
python3 -m venv .venv
source .venv/bin/activate
python3 -m pdb app.py
python3 -m cProfile app.py
python3 -m py_compile app.py
python3 -m compileall .
```

## C

```bash
gcc --version
gcc -Wall -Wextra app.c -o app
gcc -g -O0 app.c -o app
gcc -E app.c -o app.i
gcc -S app.c -o app.s
gcc -c app.c -o app.o
gcc app.o -o app
```

## Libraries

```bash
ar rcs libmath.a math.o
gcc -fPIC -c math.c -o math.o
gcc -shared -o libmath.so math.o
ldd ./app
readelf -d ./app
```

## Binary analysis

```bash
file ./app
readelf -h ./app
readelf -S ./app
readelf -d ./app
readelf -s ./app
nm ./app
objdump -d ./app
```

## GDB

```bash
gdb ./app
```

Inside GDB:

```text
run
break main
next
step
continue
bt
frame
info locals
info args
print variable
info registers
```

## Memory

```bash
gcc -g -fsanitize=address app.c -o app
gcc -g -fsanitize=undefined app.c -o app
valgrind --leak-check=full ./app
```

## System debugging

```bash
strace ./app
strace -e trace=file ./app
strace -e trace=network ./app
ltrace ./app
```

## Performance

```bash
perf stat ./app
perf record ./app
perf report
```

## Make

```bash
make
make clean
make -B
make -n
```

## CMake

```bash
cmake -S . -B build
cmake -S . -B build -DCMAKE_BUILD_TYPE=Debug
cmake --build build
cmake --build build --clean-first
ctest --test-dir build
```

## Ninja

```bash
cmake -S . -B build -G Ninja
ninja -C build
ninja -C build clean
```

## GUI diagnostics

```bash
echo "$DISPLAY"
echo "$WAYLAND_DISPLAY"
echo "$XDG_SESSION_TYPE"
echo "$XDG_CURRENT_DESKTOP"
```

## GTK

```bash
pkg-config --modversion gtk4
pkg-config --cflags gtk4
pkg-config --libs gtk4
```

---

# Final Developer Mental Model

For Python developers:

```text
Python source
    ↓
Interpreter
    ↓
Modules
    ↓
Runtime
    ↓
Debugger / profiler
```

For C/C++ developers:

```text
Source
  ↓
Preprocessor
  ↓
Compiler
  ↓
Assembly
  ↓
Object
  ↓
Linker
  ↓
ELF executable
  ↓
Dynamic libraries
  ↓
Linux process
```

For desktop developers:

```text
Application
    ↓
GUI toolkit
    ↓
X11 / Wayland
    ↓
Graphics/display system
    ↓
Linux process
```

For debugging:

```text
Bug
 ↓
Reproduce
 ↓
Observe
 ↓
Choose layer
 ↓
Choose tool
 ↓
Collect evidence
 ↓
Find root cause
 ↓
Fix
 ↓
Verify
 ↓
Automate
```

The most important commands in this course are therefore not just individual commands.

They form diagnostic toolchains:

```text
Python:
python3 → pdb → cProfile

C:
gcc → gdb → sanitizers → valgrind

Binary:
file → readelf → nm → objdump → ldd

System:
strace → ltrace

Build:
make → cmake → ninja → ctest

GUI:
environment → application → logs → strace → gdb

Performance:
perf → profiling → optimization
```

The goal is to make students capable of answering:

```text
Why did my Python program fail?

Why did my C program crash?

Where is this shared library coming from?

What exactly did the compiler generate?

Why is this executable dynamically linked?

Why does the GUI application fail to start?

Where is the memory corruption?

Which system call is failing?

Why is the application slow?

What exactly does the build system do?

Can I reproduce the same binary and debugging result?
```

That is the core Linux skill for professional Python, C/C++, and desktop application development.
