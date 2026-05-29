# Index
- [About mathjs_examples](#mathjs_examples).
- [Chatbots and math.js](#chatbots-and-mathjs).
  - [⚙️ Syntax and structure preferences](⚙️syntax-and-structure-preferences).
  - [⚠️ Environment Limitations & Workarounds](environment-limitations-&-workarounds]).
  - [📐 Mathematical and Logic Rules](mathematical-and-logic-rules).


# mathjs_examples
Examples notes(in markdown) containing math.js markdown code blocks(tested on [Math mode plugin](https://github.com/CalebJohn/joplin-math-mode) for Joplin mobile). 

Math.js code is evaluated in a Math.js parser environment and that fact causes some limitations on what can be parsed/evaluated successfully, as opposed to evaluation in a browser environment.

Only expressions and statements(besides math.js methods and constants) may be available(maybe). Standard JS library(incl. types and methods) as well as blocks of any kind like loops and ifs, aren't.
Despite this, it's possible to have functional reuse, as the examples demonstrate.

>[!important]
MathJS uses **1-based indexing**(for indexes and dimensions - that is, they start at 1 instead of 0), at least on this kind of environment.

Common dimensions are:

- 1 for Vertical(Rows).
- 2 for Horizontal(Columns).

>[!tip]
One can type help in a math.js block. Try it with help(help).
help command output is displayed right below its call line, on the math.js block.

>[!note]
The notes can contain indexes(TOC - table of contents) and KaTeX formulas that don't render in GitHub by default. They render on Joplin with toc and KaTeX features enabled on its settings.

# Chatbots and math.js

Instructions for chatbots(or math.js syntax info for you) to make your experience more compliant with math.js parser evaluation and to need less editing.

## ⚙️ Syntax and Structure Preferences

**Code Formatting**:

- No variable modifiers (const, let, var).
- No math. library prefix.
- Single-line assignments only.
- No semicolons (;) at the end of lines.
- Comments must be placed above the relevant line, never to the side.
- No newlines or comments inside data structures (matrices/vectors).

**Indexing**:

- Always use 1-based indexing.

## ⚠️ Environment Limitations & Workarounds

- **Ternary Operator**: The native ?: operator is unsupported. You mandate the use of a custom ternaryOpFn (e.g., ternaryOpFn(cond, iftrue, iffalse) = [iffalse, iftrue][(cond == true) + 1]) to emulate conditional branching through array index selection.
- **Arithmetic Operators**: The + operator is strictly reserved for numeric addition; it does not support string concatenation.
- **Index Ranges**: The : syntax for ranges is not supported; always use the range() function.
- **Dynamic Dispatch**: The apply function does not exist in your environment.
- **Strict Parser**: Dynamic function invocation (e.g., f()(args)) is not supported, which complicates recursion and dynamic dispatch.
- **Libraries**: Do not use standard math.js documentation examples unless specifically requested.

## 📐 Mathematical and Logic Rules

- **Vectors/Matrices**: Prioritize vectorized operations and direct matrix construction.
- **Recursion**: Due to the lack of short-circuiting (lazy evaluation) and the lack of a native ?: operator, deep recursion is prone to stack overflows. Vectorized, non-recursive approaches are preferred.
- **Ranges**: The range function in your environment is inclusive.
