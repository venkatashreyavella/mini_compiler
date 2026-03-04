## Mini Compiler – CS F363 (Python)

This is a small compiler project for the CS F363 Compiler Construction course.  
The goal is to build the full pipeline step by step:

- **Lexical analysis (Q1)**
- **Syntax analysis (Q2, Q3)**
- **Semantic analysis + symbol table (Compre Q1, Q2)**
- **Intermediate code (TAC) (Compre Q4)**
- **Basic optimisation + pseudo assembly (Compre Q5)**

Right now (Week 1 / Midsem Q1) only the **lexer** is implemented and working.

---

### Project layout

- **`compiler.py`** – main script. For now it only runs lexical analysis on an input file.
- **`evaluation_program.txt`** – the uniform test program given in the assignment.
- **`contribution.md`** – member-wise work distribution (M1–M4) for all questions.
- **`mini_compiler/`**
  - **`__init__.py`** – marks this as a package.
  - **`tokens.py`** – token kinds (`TokenType`), `Token`, and `LexicalError`.
  - **`lexer.py`** – regex-based lexer used for Q1.
  - **`grammar.py`** – placeholder for the CFG and parsing helpers (to be filled in Q2 / Compre).
  - **`parser_rd.py`** – placeholder for the recursive-descent parser.
  - **`ast.py`** – placeholder for AST node classes.
  - **`symbol_table.py`** – placeholder for the symbol table.
  - **`semantic.py`** – placeholder for semantic checks.
  - **`parser_ll1.py`** – placeholder for LL(1) / table-driven parser.
  - **`ir.py`** – placeholder for three-address code (TAC) generation.
  - **`optimizer.py`** – placeholder for TAC optimisation.
  - **`codegen.py`** – placeholder for pseudo assembly generation.

---

### How to run (Q1 – lexical analysis)

From the project folder:

```bash
python compiler.py
```

This will:

- Read `evaluation_program.txt`,
- Run the lexer,
- Print any **lexical errors**,
- Print the full **token stream** (token type, lexeme, line, column).

You can also pass a different source file:

```bash
python compiler.py some_other_program.txt
```

---

### Planned extensions (later weeks)

These will be added on top of the existing code without rewriting Q1:

- **Q2 / Midsem:** fill `grammar.py`, `parser_rd.py`, `ast.py` and extend `compiler.py` to run the parser.
- **Midsem Q3:** add syntax error reporting and small test inputs with intentional errors.
- **Compre Q1–Q5:** implement the symbol table, semantic checks, TAC, optimisation, and pseudo assembly, each in its own module under `mini_compiler/`, and call them in order from `compiler.py`.

