---
id: a42l
title: Basic knowledge of computer programming (common in interviews, 1 hour quick review)
permalink: /common-computer-programming-basics-for-interviews-1-hour-quick-review
date: 2025-05-13 13:17:15
thumbnail: interview/ruby/ruby_1_hour.png
tags: []
---

# Differences Between "Compiled Languages" and "Interpreted Languages"

`Compiled languages` and `interpreted languages` are two major categories of programming languages based on their **execution method**. The main difference lies in the process of code translation and execution.

For example, imagine there's a history book written in ancient Greek (equivalent to code written in Java or Python). You (equivalent to a computer) want to understand it, so it needs to be translated.

- The approach of a `compiled language` (like Java) is to translate the entire book at once and then give it to you (the computer). You can then directly understand (execute) it.
- The approach of an `interpreted language` (like Python) is not to translate the entire book beforehand. Instead, a dedicated translator (the interpreter) sits next to you. For every line encountered, the translator (interpreter) translates it for you (the computer) on the spot, until all the content you care about is translated.

## 1. Translation Timing and Method

| **Type**           | **Compiled Languages** (C, C++, Go) | **Interpreted Languages** (Python, JavaScript) |
|--------------------|------------------------------------|------------------------------------------------|
| **Translation Process** | Generates machine code **all at once** via a compiler | Interprets and executes **line by line** via an interpreter |
| **Output File**    | Can generate a standalone executable file (e.g., .exe) | Does not generate a machine code file          |
| **Execution Method** | Directly runs the compiled machine code | Translates and executes simultaneously         |

## 2. Performance Comparison

- **Compiled Languages**  
  ✅ Fast execution speed (directly runs machine code)
  ❌ Code modifications require recompilation
- **Interpreted Languages**  
  ✅ Convenient for development and debugging (run immediately after modification)  
  ❌ Slower execution speed (requires real-time translation)

## 3. Cross-Platform Compatibility

| **Type**       | **Characteristics**                                                      |
|----------------|--------------------------------------------------------------------------|
| Compiled       | Needs recompilation for different platforms (e.g., compile separately for Windows/Linux) |
| Interpreted    | The same code runs across platforms (just need to install the corresponding interpreter) |

## 4. Error Handling

- **Compiled Languages**: Syntax errors are reported during the compilation phase.
- **Interpreted Languages**: Errors may only be exposed at runtime.

## 5. Typical Language Examples

| **Type**       | **Language Examples**             | **Toolchain**             |
|----------------|-----------------------------------|---------------------------|
| Compiled       | Java, C, C++, Rust, Swift       | GCC, LLVM                 |
| Interpreted    | Python, Ruby, JavaScript (browser) | CPython, V8 engine        |

