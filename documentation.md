---

# JSONic Programming Language Documentation

---

## Introduction

**JSONic** is a simple, expressive programming language that uses JSON syntax to represent programs. It supports variables, functions, control flow, arithmetic, string and array manipulation, and more—all expressed as structured JSON data. JSONic is designed to be easy to parse, interpret, and extend, making it great for learning about interpreters or embedding programmable logic in JSON-based environments.

---

## Table of Contents

* [Getting Started](#getting-started)
* [Basic Concepts](#basic-concepts)
* [Syntax Reference](#syntax-reference)
* [Built-in Functions](#built-in-functions)
* [Examples](#examples)
* [Error Handling](#error-handling)
* [Extending JSONic](#extending-jsonic)

---

## Getting Started

### How to Run JSONic Programs

JSONic programs are JSON arrays or objects interpreted by the JSONic interpreter. You can run them via:

```bash
python jsonic.py program.json
```

Where `program.json` contains your JSONic code.

---

## Basic Concepts

### Programs

A JSONic program is a JSON array of expressions, each evaluated sequentially.

```json
[
    { "let": ["x", 5] },
    { "call": ["print", "x is", "x"] }
]
```

---

### Expressions

Expressions can be:

* **Literals:** Numbers, strings, booleans
* **Variables:** Referenced by name as strings
* **Objects:** Represent operations or statements (e.g. `"let"`, `"def"`, `"call"`)
* **Arrays:** Lists of expressions, evaluated element-wise

---

## Syntax Reference

### Variable Assignment

```json
{ "let": ["varName", expression] }
```

Assigns the evaluated expression to `varName` in the current environment.

---

### Function Definition

```json
{
  "func": {
    "name": "functionName",
    "params": ["param1", "param2"],
    "body": expression
  }
}
```

Defines a new function accessible globally.

---

### Function Call

```json
{ "call": ["functionName", arg1, arg2] }
```

Calls a function (built-in or user-defined) with arguments.

---

### Return Statement

```json
{ "return": expression }
```

Returns a value from a function.

---

### Control Flow

#### If Statement

```json
{
  "if": {
    "condition": expression,
    "then": expression,
    "else": expression
  }
}
```

Evaluates `condition`; executes `then` if true, else `else`.

---

#### While Loop

```json
{
  "while": {
    "condition": expression,
    "do": expression
  }
}
```

Repeats executing `do` as long as `condition` is true.

---

#### Block Statement

```json
{ "do": [expression1, expression2, ...] }
```

Executes multiple expressions in sequence, returns last result.

---

### Arithmetic Operators

Use objects with keys:

* `"add": [expr1, expr2]` (addition)
* `"sub": [expr1, expr2]` (subtraction)
* `"mul": [expr1, expr2]` (multiplication)
* `"div": [expr1, expr2]` (division)
* `"mod": [expr1, expr2]` (modulus)

Example:

```json
{ "add": [2, 3] }  // evaluates to 5
```

---

### Comparison Operators

* `"eq": [a, b]` — equals
* `"neq": [a, b]` — not equals
* `"gt": [a, b]` — greater than
* `"lt": [a, b]` — less than
* `"gte": [a, b]` — greater or equal
* `"lte": [a, b]` — less or equal

---

### Logical Operators

* `"and": [expr1, expr2]`
* `"or": [expr1, expr2]`
* `"not": expr`

---

### Arrays

* Access element: `{ "get": [arrayExpr, indexExpr] }`
* Set element: `{ "set": [arrayExpr, indexExpr, valueExpr] }`
* Append element: `{ "push": [arrayExpr, valueExpr] }`
* Length: `{ "len": arrayExpr }`

---

### Comments

Use the `"comment"` key to add human-readable comments in code. These are **ignored** during execution.

```json
{ "comment": "This is a comment" }
```

or multiline:

```json
{ "comment": ["Line 1", "Line 2"] }
```

---

## Built-in Functions

* `print(...)` — Prints arguments to console.
* `input(prompt)` — Reads input from the user.
* `len(value)` — Returns length of string, array, or dict.
* `type(value)` — Returns the type name.
* `contains(collection, value)` — Checks if collection contains value.
* Math: `abs`, `min`, `max`, `pow`, `round`, `floor`, `ceil`, `fact`
* String ops: `upper`, `lower`, `strip`, `split`, `join`, `replace`
* File ops: `read_file(path)`, `write_file(path, content)`
* Type conversions: `int`, `float`
---

## Examples

### Doubling a Number

```json
[
    { "comment": "Define a function that doubles a number" },
    {
      "func": {
        "name": "double",
        "params": ["n"],
        "body": { "return": { "mul": ["n", 2] } }
      }
    },
    { "let": ["x", 5] },
    { "let": ["y", { "call": ["double", "x"] }] },
    { "call": ["print", "Double of x is", "y"] }
]
```

---

## Error Handling

* Calling an undefined function raises an error.
* Passing wrong argument counts throws an error.
* Unsupported operations (like `len` on unsupported types) raise exceptions.
* File operations validate file existence or write permission.

---

## Extending JSONic

You can easily add new built-ins by extending the `builtins` dictionary in the interpreter class.

You can also extend the syntax by adding new keys in the `eval()` method for additional operations.

---

## FAQ

**Q:** Why JSON for a programming language?
**A:** JSON’s structure allows easy parsing, transformation, and transport across systems. JSONic leverages this for readability and interoperability.

**Q:** Can I write multiline strings?
**A:** Strings follow JSON rules. Use `\n` for line breaks.

**Q:** How do I debug JSONic code?
**A:** Use `"comment"` to annotate your code and test expressions step-by-step.

---

## License & Contribution

Feel free to fork and contribute! The interpreter is MIT licensed.

---
