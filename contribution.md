## Team Contribution Mapping

This file documents **member-wise work distribution** for each question of the mini-compiler project.

Use placeholders **M1, M2, M3, M4** for team members (replace with real names/IDs in your report).

---

### Mid-Sem Q1 – Lexical Specification & Tokenization

**Goal:** Define tokens, regular expressions, implement a lexical analyzer in Python, and show the token stream and lexical errors for the evaluation program.

- **M1**
  - Listed and classified all token categories from the language specification (keywords, identifiers, literals, operators, delimiters, punctuation).
  - Drafted the initial regular expressions for each token class in Python.
- **M2**
  - Refined the regexes (multi-character operators, distinguishing keywords vs identifiers, `int` vs `float` literals).
  - Designed the `Token` structure (type, lexeme, line, column) and decided the token-stream print format.
- **M3**
  - Implemented the core **lexer module** in Python:
    - Reads the source program,
    - Applies regex rules in priority order,
    - Produces the token sequence.
  - Added lexical error detection and reporting (unexpected characters, malformed tokens) with line/column information.
- **M4**
  - Wrote the **driver script** that:
    - Loads the uniform evaluation program,
    - Runs the lexical analyzer,
    - Prints the full token stream and any lexical errors.
  - Prepared example token-stream output and a short explanation of how source lines map to tokens.

---

### Mid-Sem Q2 – Grammar Design & Syntactic Validation

**Goal:** Design a CFG for the language, implement a parser (initially recursive-descent in Python), and demonstrate leftmost/rightmost derivations and parse trees.

- **M1**
  - Drafted the **context-free grammar (CFG)** covering:
    - Declarations, assignments, arithmetic and boolean expressions,
    - `if–else`, `while`, blocks `{ }`, and `print`.
  - Ensured the grammar can generate the evaluation program without modification.
- **M2**
  - Refined the CFG for **precedence and associativity** (arithmetic > relational > boolean; unary `!` precedence).
  - Implemented a **recursive-descent parser** in Python following the grammar.
- **M3**
  - Extended the parser to build a **parse tree / AST**:
    - Node classes or structures for each nonterminal,
    - Children represent production expansions.
  - Implemented pretty-printing of the parse tree (indented textual tree for demos).
- **M4**
  - Prepared manual **leftmost derivation** and **rightmost derivation** for a non-trivial statement from the evaluation program.
  - Drew and documented the corresponding **parse tree**, and verified it matches parser output on that statement.

---

### Mid-Sem Q3 – Syntax Error Detection

**Goal:** Show that the parser detects and reports syntax errors with meaningful messages.

- **M1**
  - Designed a small suite of **intentional syntax errors** by modifying the evaluation program:
    - Missing semicolons,
    - Unmatched parentheses or braces,
    - Misplaced keywords or operators.
  - Specified the expected type of syntax error for each case.
- **M2**
  - Enhanced the parser to:
    - Detect syntax errors with line/column and offending token,
    - Classify errors (missing token vs unexpected token).
  - Implemented a simple **error-recovery strategy** (e.g. skip to `;` or `}`) so parsing can continue and report multiple errors.
- **M3**
  - Implemented a **test harness** that:
    - Runs the parser on each erroneous test program,
    - Captures and prints all syntax error messages in a readable format.
  - Verified that the correct evaluation program parses successfully (no syntax errors).
- **M4**
  - Documented each test case:
    - Original snippet vs modified erroneous version,
    - Actual error message from the system,
    - Short explanation of what is wrong syntactically.
  - Prepared outputs/screenshots used in the Q3 demo.

---

### Compre Q1 – Symbol Table and Scope Handling

**Goal:** Implement a symbol table in Python with name, type, scope, and memory offset; support nested scopes and show symbol table updates on the evaluation program.

- **M1**
  - Designed the **symbol entry format**:
    - Fields: variable name, type (`int`/`float`), scope level, memory offset.
  - Specified required operations: `insert`, `lookup`, `enter_scope`, `exit_scope`.
- **M2**
  - Implemented the `SymbolTable` class in Python:
    - Internal structures for multiple scopes (e.g. stack of dictionaries),
    - Insert with check for duplicates in the same scope,
    - Lookup searching from innermost to outermost scope.
  - Implemented memory offset management per scope.
- **M3**
  - Integrated the symbol table with the **parse tree / AST traversal**:
    - On declarations, insert into the current scope,
    - On entering `{`, call `enter_scope`; on `}`, call `exit_scope`.
  - Ensured correct handling of variable shadowing in nested blocks.
- **M4**
  - Built a **symbol table trace tool**:
    - Runs the evaluation program through parsing and symbol-table construction,
    - Logs insertions and scope changes step-by-step.
  - Prepared a clean symbol table trace (tables at key points) for viva/presentation.

---

### Compre Q2 – Semantic Analysis

**Goal:** Perform semantic checks (undeclared variables, multiple declarations, type mismatches, invalid boolean conditions) using the parse tree/AST and symbol table.

- **M1**
  - Wrote a short **semantic specification** summarizing rules:
    - Variables must be declared before use,
    - No multiple declarations in same scope,
    - Type rules for expressions and assignments,
    - Boolean conditions for `if`/`while`.
  - Reviewed these rules against the evaluation program.
- **M2**
  - Implemented a **semantic analyzer** that walks the AST:
    - Checks each identifier use against the symbol table,
    - Reports **undeclared variable** and **multiple declaration** errors.
- **M3**
  - Implemented **type inference and checking**:
    - Arithmetic expressions produce `int`/`float`,
    - Relational expressions produce `bool`,
    - Boolean operators require `bool` operands,
    - Assignments require compatible types (with defined promotion rules, e.g. `int` → `float` allowed).
  - Added detailed type-mismatch error messages (expected vs actual type).
- **M4**
  - Created semantic test versions of the evaluation program:
    - Correct program,
    - At least two versions with semantic errors (undeclared variable, wrong types, non-boolean condition).
  - Ran the analyzer on these and documented each reported error with explanation.

---

### Compre Q3 – Parser Implementation (LL(1) / Shift-Reduce / SLR / LR(0))

**Goal:** Upgrade the syntax analyzer to a table-driven parser (e.g. LL(1) or SLR/LR(0)), provide FIRST/FOLLOW sets, parsing table, and parsing stack trace for a non-trivial input.

- **M1**
  - Helped transform the original CFG into a form suitable for **LL(1) / LR parsing** (removed left recursion, applied factoring where needed).
  - Computed FIRST and FOLLOW sets by hand for key nonterminals to cross-check results.
- **M2**
  - Implemented Python utilities to **compute FIRST and FOLLOW sets** automatically from the grammar.
  - Constructed the **parsing table** (LL(1) table or LR action/goto table) and printed it in tabular form.
- **M3**
  - Implemented the **table-driven parser** (LL(1) or LR) in Python:
    - Stack-based algorithm,
    - Reads tokens from the lexer,
    - Consults parsing table to drive shifts/reductions or predictions.
  - Ensured it successfully parses the uniform evaluation program.
- **M4**
  - Selected a **non-trivial input** (e.g. the full `while` loop with nested `if–else` from the evaluation program).
  - Produced a detailed **parsing stack trace**:
    - Sequence of stack contents, remaining input, and actions,
    - Annotated explanation suitable for viva (showing how the parser proceeds step-by-step).

---

### Compre Q4 – Intermediate Code Generation (Three-Address Code)

**Goal:** Generate Three-Address Code (TAC) for the entire evaluation program, including arithmetic, boolean expressions, conditionals, and loops.

- **M1**
  - Defined the TAC instruction format: `(op, arg1, arg2, result, label)` and naming conventions for temporaries (`t1`, `t2`, …) and labels (`L1`, `L2`, …).
  - Sketched TAC patterns for:
    - Arithmetic and boolean operations,
    - `if–else` and `while` control flow.
- **M2**
  - Implemented **expression-to-TAC** generation:
    - Walks AST expression nodes,
    - Emits TAC for arithmetic and relational operations,
    - Returns temporaries representing expression values.
- **M3**
  - Implemented TAC for **control flow**:
    - `if` and `if–else` using conditional jumps and labels,
    - `while` loops with condition evaluation, body, and back jumps.
  - Ensured TAC correctly represents the evaluation program’s control structure.
- **M4**
  - Wrote a **TAC driver** that:
    - Traverses the AST for the evaluation program,
    - Outputs a full, numbered TAC listing.
  - Manually traced key parts (loop and final `if`) to verify the TAC and prepared notes for viva.

---

### Compre Q5 – Optimization and Target Code Generation

**Goal:** Apply at least one basic optimization to the TAC and generate corresponding pseudo-assembly code that preserves program semantics.

- **M1**
  - Chose and specified the **optimization techniques** to implement (e.g. constant folding, dead code elimination, algebraic simplifications).
  - Prepared small before/after TAC examples illustrating each optimization.
- **M2**
  - Implemented the **optimizer module** in Python:
    - Traverses TAC instructions,
    - Applies selected optimizations,
    - Produces optimized TAC.
  - Verified that optimized TAC is semantically equivalent on test inputs.
- **M3**
  - Designed the **pseudo-assembly language** used as target code:
    - Instruction set (LOAD, STORE, ADD, SUB, MUL, DIV, CMP, JUMP, etc.),
    - Notation for registers and memory, label format,
    - Mapping rules from each TAC operation to pseudo-assembly sequences.
- **M4**
  - Implemented the **target code generator** in Python:
    - Translates TAC (original and/or optimized) into pseudo-assembly instructions,
    - Handles labels and branch instructions correctly.
  - Produced the final pseudo-assembly listing for the evaluation program and highlighted where optimization reduced or simplified the code.

---

### Integration & Documentation (Overall)

Across all questions:

- **M1**
  - Coordinated the overall design, ensured consistency of data structures (tokens, AST nodes, symbol entries, TAC instructions).
  - Wrote/maintained the main `compiler` driver that runs all phases in order.
- **M2**
  - Focused on parsing-related components (CFG, recursive-descent, LL(1)/LR table-driven parser).
  - Helped verify correctness of FIRST/FOLLOW sets, parsing tables, and stack traces.
- **M3**
  - Focused on semantic correctness and IR:
    - Symbol table integration,
    - Semantic checks,
    - Expression and control-flow TAC generation.
- **M4**
  - Focused on testing, optimization, and code generation:
    - Test harnesses for each phase,
    - TAC optimization,
    - Pseudo-assembly generation and final demonstration outputs.

