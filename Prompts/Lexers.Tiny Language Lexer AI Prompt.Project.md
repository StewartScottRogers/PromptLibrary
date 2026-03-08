# Lexers: Tiny Language Lexer AI Prompt
------------------------------------------------------------------------------------------------------------------------
- **.NET Version Requirements**: 
  - Create a complete .NET 10.0 Solution.
  - Create supporting Solution files.
  - Create supporting Project files.
  - All solution coding will be C#. 
  - Solution must be usable in Visual Studio 2022.
  - Ensure the solution is fully compilable and executable without additional coding.
  - Do not use Implicit Usings.
  - Do not use Nullable.

- **Coding Style**:
	- Never use leading underscores for any variable.
	- Use only explicit types.
	- Local variables should use lowerCamelCase.
	- Member variables should use UpperCamelCase.
	- Class properties should use UpperCamelCase.
	- Class names should use UpperCamelCase.
	- Interface names should use UpperCamelCase.
	- Enumeration names should use UpperCamelCase.
	- Record names should use UpperCamelCase.
	- Struct names should use UpperCamelCase.
	- Method names should use UpperCamelCase.
	- All Tuples should be named from the returning method.
	- All Tuples must be Post Fixed with the word 'Tuple'.
	- All Tuples must use a var type.
	- use a readonly on all variables whenever possible.
	- Local Variables should be named with complete nouns, appending a prefix or postfix for clarification if required.
	- Member Variables should be named with complete nouns, appending a prefix or postfix for clarification if required.
	- Properties should be named with complete nouns, appending a prefix or postfix for clarification if required.
	- Methods should be named with complete nouns, appending a prefix or postfix for clarification if required.
	- Classes should be named with complete nouns, appending a prefix or postfix for clarification if required.
	- Interfaces should be named with complete nouns, appending a prefix or postfix for clarification if required.
	- Structs should be named with complete nouns, appending a prefix or postfix for clarification if required.

- **Library Usage**:
	- Use only the Microsoft Basic Component Library.
	- Use defined value types from the Basic Component Library.
	- Use defined reference types from the Basic Component Library.

- **Programming Constructs**:
	- Favor use of Tuples for returning multiple values from a method rather than Classes or Structs, or Records
	- Use var types for Tuples.
	- Favor Records over Classes.

- **File System Structure**:
	- Create separate files for each class.
	- Create separate files for each interface.
	- Create separate files for each enumeration.
	- Create separate files for each record.

- **Architecture**:
	- Implement the Interpreter using the Visitor pattern. Create an INodeVisitor
	  interface with a Visit method for every AST node type. Do not use a single
	  large if-else or switch chain to dispatch node types.
	- Implement a scope chain for variable resolution. Each block (function body,
	  loop body, if branch) must create a child scope that delegates unresolved
	  names upward to its parent. Use a linked-list of Dictionaries, not a flat
	  copy of the environment.
	- Variables declared inside a loop or if block must NOT leak into the
	  enclosing scope when the block exits.
	- Function environments must be isolated — a function call must not inherit
	  variables from its call site. It may only see globally declared variables
	  and its own parameters.
	- Closures are out of scope — lambdas capture no variables from the
	  enclosing scope.

- **Runtime Error Policy**:
	- Referencing an undefined variable must throw a descriptive runtime
	  exception that names the variable and includes the source line number.
	- Store the source line number in every AST node so that runtime errors
	  can report exactly where in the source the fault occurred.
	- Enforce a maximum call stack depth of 500 frames. Exceeding it must throw
	  a descriptive exception (e.g. "Stack overflow: maximum call depth of 500
	  exceeded") rather than crashing the process.
	- Division by zero for `/`, `//`, and `%` must always throw a descriptive
	  DivideByZeroException regardless of operand types.
	- Type mismatches (e.g. arithmetic on a non-numeric value) must throw a
	  descriptive exception rather than silently coercing to zero.
	- Silent no-ops are forbidden. Any grammar feature that is parsed but not
	  yet interpreted must throw "Feature not yet implemented: <name>" at runtime.

- **Type System**:
	- The language has three numeric types: Integer (64-bit signed long),
	  Float (64-bit double), and Bool. Arithmetic follows these promotion rules:
	    - Integer op Integer → Integer, except `/` which returns Float when the
	      result has a fractional part.
	    - Integer op Float → Float.
	    - Float op Float → Float.
	- `//` (floor division) must use integer arithmetic when both operands are
	  Integer and must never convert to Float internally.
	- `**` with two Integer operands and a non-negative integer exponent must
	  return Integer. With a Float operand or a negative exponent it returns Float.
	- `%` (modulo) operates on Integers only. Applying it to a Float is a
	  type error.
	- `&` is string concatenation only. Applying it to non-string values
	  converts both sides to their string representations first.
	- `+` is numeric addition unless one operand is already a String, in which
	  case both sides are converted to strings and concatenated.
	- Truthiness rules:
	    - null     → false
	    - Integer 0 → false, all other integers → true
	    - Float 0.0 → false, all other floats → true
	    - Empty string "" → false, all other strings → true
	    - Bool: as-is

- **Built-in Functions**:
	- The following built-in functions must be implemented in the Interpreter.
	  They require no function definition in source code and may not be
	  redefined by user code. No other built-ins are permitted.

	  | Name      | Parameter     | Returns                              |
	  |-----------|---------------|--------------------------------------|
	  | print(v)  | any value     | void — writes line to Console.Out    |
	  | len(v)    | string or list| Integer length                       |
	  | str(v)    | any value     | String representation                |
	  | int(v)    | string/float/bool | Integer (truncates float)        |
	  | float(v)  | string/int/bool   | Float                            |
	  | bool(v)   | any value     | Boolean (applies truthiness rules)   |

- **Feature Implementation Status**:
	- Every grammar feature must be either fully implemented or raise a
	  descriptive "Feature not yet implemented: <name>" exception at runtime.
	  Silent no-ops (parsing succeeds, nothing happens at runtime) are forbidden.

	  Features that must be FULLY implemented:
	    - All assignment and declaration forms (let, var, const)
	    - All control flow (if, while, for, foreach, do-while, switch, break, continue)
	    - Functions (definition, call, recursion, default parameters, return)
	    - Arrays (declare, read element, element assignment, foreach iteration)
	    - Exception handling (try, catch, finally, throw)
	    - Annotations (parse and pass through — the wrapped statement executes normally)
	    - All expression operators and all literal types

	  Features that may raise "not yet implemented" at runtime (parse only):
	    - Classes and objects
	    - Modules, imports, exports
	    - Pattern matching (match / when)
	    - List comprehension array syntax
	    - Lambda invocation (lambdas may be stored as values but calling them is not required)
	    - Cast expressions, type-check (is), type-assert (as)

 - **Code Documentation**:
	- Add comments to explain complex code structures or logic in a way accessible to business analysts or entry-level programmers.

- **Console Application**:
	- The console application must run a suite of demonstration programs that
	  together exercise every FULLY IMPLEMENTED feature listed above.
	- For each demo, print a labelled header, the source code, and the output.
	- At the end, print the summary line: "All demos completed successfully."
	- The application must exit with code 0 on success and code 1 on any error,
	  writing the error message and source line number to Console.Error.

- **Unit Testing**:
	- Use only the Microsoft Unit Test Framework.
	- Do not use XUnit or NUnit.
	- Unit Test all bounding conditions.
	- Apply the BNF Grammar Verification Strategy defined below.


------------------------------------------------------------------------------------------------------------------------

# BNF Grammar Verification Strategy

Every production rule in the BNF must be verified at three independent layers:
the Lexer, the Parser, and the Interpreter. Work through the BNF top-to-bottom
and produce at least one test per layer per production rule. Tests are organised
into four test classes, each in its own file.

## Layer 1 — Lexer Coverage (`LexerGrammarTests.cs`)

For every terminal symbol and keyword in the grammar, verify that the Lexer
produces the correct TokenType and Lexeme.

For each production rule that introduces a new terminal, write a test that:
- Feeds the minimal source string for that terminal to the Lexer.
- Asserts the expected TokenType on the first token.
- Asserts the Lexeme string is exactly correct.
- Asserts the EndOfFile token follows immediately.

Required terminal coverage:
- Every keyword (`let`, `var`, `const`, `if`, `then`, `else`, `end`, `while`,
  `do`, `for`, `to`, `step`, `in`, `foreach`, `switch`, `case`, `default`,
  `break`, `continue`, `function`, `return`, `class`, `extends`, `implements`,
  `new`, `module`, `import`, `as`, `export`, `try`, `catch`, `finally`,
  `throw`, `match`, `when`, `print`, `input`, `not`, `and`, `or`, `is`,
  `static`, `Constructor`, `enum`, `true`, `false`, `null`, `void`,
  `int`, `float`, `string`, `bool`, `array`, `object`, `map`)
- Every operator (`:=`, `+`, `-`, `*`, `/`, `%`, `**`, `//`, `&`,
  `==`, `!=`, `<`, `>`, `<=`, `>=`, `&&`, `||`, `->`, `=>`, `?`, `:`,
  `.`, `,`, `;`, `@`)
- Every delimiter (`(`, `)`, `{`, `}`, `[`, `]`)
- All number literal forms: decimal integer, decimal float, `0b` binary,
  `0o` octal, `0x` hex
- Double-quoted string literal
- Single-quoted string literal
- String with each supported escape sequence (`\n`, `\t`, `\\`, `\"`, `\'`)
- Identifier (starts with letter, may contain digits and underscores)
- Line comment (`#`) — verify the comment text does NOT appear in the token list
- Unknown/invalid character — verify TokenType.Unknown is produced
- Line and column numbers — verify they increment correctly across newlines
- Multi-token sequences — verify adjacent tokens are each correctly identified

## Layer 2 — Parser Coverage (`ParserGrammarTests.cs`)

For every non-terminal production rule in the BNF, verify that the Parser
produces the correct AST node type and structure.

For each production rule, write a test that:
- Lexes a minimal source string that exercises exactly that production.
- Parses the token list into an AST.
- Asserts the root node is the expected type.
- Asserts child nodes are the expected types, in the expected order.
- For optional elements (`?`), write one test with the element present
  and one test with it absent.
- For alternating productions (`|`), write one test per alternative.

Required production coverage:

**Program structure**
- `<program>` with only a statement list
- `<program>` opening with a function definition
- `<program>` opening with a class definition

**Assignment and declaration**
- `<assign_stmt>` — simple assignment
- `<var_declare_stmt>` — `let` form without type annotation
- `<var_declare_stmt>` — `var` form with type annotation
- `<type_declare_stmt>` — all three forms (`let`, `var`, `const` with type)
- `<const_declare_stmt>` — without type annotation
- `<const_declare_stmt>` — with type annotation
- `<const_declare_stmt>` — `enum` form with value list
- `<enum_value>` — bare identifier form
- `<enum_value>` — identifier with assigned expression

**Control flow**
- `<if_stmt>` — without else branch
- `<if_stmt>` — with else branch
- `<while_stmt>`
- `<for_stmt>` — without step
- `<for_stmt>` — with step
- `<foreach_stmt>`
- `<do_while_stmt>` — single statement body
- `<do_while_stmt>` — multi-statement body
- `<switch_stmt>` — with one case
- `<switch_stmt>` — with multiple cases and a default
- `<break_stmt>`
- `<continue_stmt>`

**IO**
- `<print_stmt>`
- `<input_stmt>`

**Functions**
- `<function_def>` — no parameters, no return type
- `<function_def>` — with parameters and return type
- `<param>` — bare identifier form
- `<param>` — with type annotation
- `<param>` — with default value
- `<param>` — with type annotation and default value
- `<function_call_stmt>` — with no arguments
- `<function_call_stmt>` — with multiple arguments
- `<return_stmt>` — with expression
- `<return_stmt>` — bare return (no expression)

**OOP**
- `<object_declare_stmt>`
- `<object_call_stmt>`
- `<class_def>` — minimal (no extends, no implements)
- `<class_def>` — with extends
- `<class_def>` — with implements
- `<constructor_def>`
- `<field_declare_stmt>` — each of the four forms

**Expressions (verify precedence and associativity)**
- `<ternary_expr>` — condition ? then : else
- `<expr>` with `&&` — logical and
- `<expr>` with `||` — logical or
- `<expr>` with `==` and `!=`
- `<expr>` with `<`, `>`, `<=`, `>=`
- `<expr>` with `+`, `-`, `&`
- `<term>` with `*`, `/`, `%`, `//`
- `<factor>` with `**` — verify right-associativity: `2 ** 3 ** 2` parses as `2 ** (3 ** 2)`
- Unary `-` and `not`
- Operator precedence: `2 + 3 * 4` must parse as `2 + (3 * 4)`, not `(2 + 3) * 4`
- Parenthesised expression overrides precedence

**Arrays**
- `<array_assign_stmt>` — element assignment
- `<array_declare_stmt>` — literal list form
- `<array_access>` — read element by index

**Lambda**
- `<lambda_expr>` — statement body form ending with `end`

**Exception handling**
- `<try_stmt>` — with catch, no finally
- `<try_stmt>` — with catch and finally
- `<catch_clause>` — bare identifier form
- `<catch_clause>` — typed form with parentheses
- `<throw_stmt>`

**Annotations**
- `<annotated_stmt>` — annotation with no parameters
- `<annotated_stmt>` — annotation with one parameter (`name = value`)
- `<annotated_stmt>` — annotation with multiple parameters

**Types**
- Each primitive type keyword (`int`, `float`, `string`, `bool`, `void`, `null`)
- Array type `<type> "[" "]"`
- Map type `"map" "<" <type> "," <type> ">"`
- Nullable type `<type> "?"`

**Literals**
- Integer, float, binary, octal, hex literals resolve to correct AST values
- Boolean literals `true` / `false`
- Null literal
- Both string delimiter forms

**Parser error cases**
- Missing `end` keyword after if block — expect parse exception
- Missing `do` keyword in while loop — expect parse exception
- Malformed `:=` (using `=` instead) — expect parse exception

## Layer 3 — Interpreter Coverage (`InterpreterGrammarTests.cs`)

For every executable production rule, verify that the Interpreter produces
the correct runtime result.

For each production rule, write a test that:
- Composes a complete source string exercising that production.
- Runs it through Lexer → Parser → Interpreter.
- Captures printed output and asserts expected values.
- For rules that produce a value (expressions), stores the result in a
  variable and prints it for assertion.

Required execution coverage:

**Variables and assignment**
- `let` declaration — verify value is stored and retrievable
- `var` declaration with type annotation — verify value
- `const` declaration — verify value
- Assignment (`id := expr`) — verify updated value

**Arithmetic correctness**
- Integer addition, subtraction, multiplication, integer division
- Float promotion: integer op float returns float
- Modulo (`%`)
- Floor division (`//`) — verify `7 // 2 = 3`, `-7 // 2 = -4`
- Power (`**`) — verify `2 ** 10 = 1024`, `2 ** 3 ** 2 = 512`
- String concatenation with `&`
- String concatenation with `+` when one operand is a string

**Comparison and boolean**
- All six comparison operators with both true and false outcomes
- `&&` short-circuits: right side not evaluated if left is false
- `||` short-circuits: right side not evaluated if left is true
- `not` negation
- `and` / `or` keyword synonyms for `&&` / `||`
- Ternary expression: true branch and false branch

**Control flow**
- `if` true branch executes, false branch does not
- `if/else` — correct branch executes
- `while` loop — body executes correct number of times
- `while` with `break` — exits early
- `while` with `continue` — skips remainder of body iteration
- `for` loop — iterates correct range inclusive
- `for` loop with `step` — iterates with custom step
- `for` loop with negative step — counts down
- `foreach` over a list — visits each element in order
- `foreach` over a string — visits each character
- `do...while` — body executes at least once when condition is initially false
- `do...while` — body executes multiple times while condition is true
- `switch` — matching case body executes
- `switch` — non-matching case body does not execute
- `switch` — default executes when no case matches
- `switch` with `break` — exits after matched case

**Functions**
- Function with no parameters returns correct value
- Function with multiple parameters receives correct argument values
- Recursive function — factorial or fibonacci
- Function with default parameter — called with and without that argument
- Bare `return` in void function — does not crash

**Arrays**
- Array literal is created with correct elements
- Array element read by index
- Array element assignment mutates the array
- Out-of-bounds index returns null without crashing

**Exception handling**
- `try/catch` — catch block executes on thrown exception
- `try/catch` — catch variable holds the exception message
- `try/catch/finally` — finally always executes (both normal and exception paths)
- `throw` — message propagates to enclosing catch
- Division by zero is caught by try/catch
- `try` with no exception — catch block does not execute, finally does

**Annotations**
- Annotated statement executes its wrapped statement normally

**Number literals**
- Binary literal evaluates to correct integer value
- Octal literal evaluates to correct integer value
- Hex literal evaluates to correct integer value
- Float literal retains decimal precision

**Truthiness rules**
- `null` is falsy
- `0` and `0.0` are falsy
- Empty string `""` is falsy
- Non-zero number is truthy
- Non-empty string is truthy

## Layer 4 — Integration Coverage (`IntegrationGrammarTests.cs`)

Write end-to-end programs that combine multiple grammar features and verify
the complete output. Each test must use at least three distinct production
rules together.

Required integration scenarios:
- FizzBuzz (1–20): combines for loop, if/else, modulo, print, string literals
- Fibonacci sequence (first 10 terms): recursive function, for loop, print
- Bubble sort of a list: foreach, array assignment, while, swap logic
- String builder: foreach over string, concatenation, function, return
- Calculator: switch statement, functions, arithmetic, print
- Exception safety: nested try/catch/finally, throw, variable mutation
- Accumulator with do-while: proves multi-statement do-while body works
- Mixed number bases: binary + octal + hex in a single expression, print result
- Annotation passthrough: annotated function call still executes and prints
- Nested control flow: for inside while inside if — verify all levels interact correctly

## Verification Checklist

After generating all code and tests, confirm every item below before
reporting the work complete. Do not report complete if any item is unchecked.

**Lexer**
- [ ] Every keyword in the grammar has at least one lexer test
- [ ] Every operator in the grammar has at least one lexer test
- [ ] Every delimiter has at least one lexer test
- [ ] All number literal formats (decimal int, float, 0b, 0o, 0x) are tested
- [ ] Both string delimiters and all five escape sequences are tested
- [ ] Line comment (`#`) is tested — comment text must not appear in token list
- [ ] Line and column tracking are tested across a multi-line source string
- [ ] Unknown/invalid character produces TokenType.Unknown — tested
- [ ] Bare `=` produces TokenType.SingleEqual, not Unknown — tested

**Parser**
- [ ] Every non-terminal production rule has at least one parser test
- [ ] Every `|` alternative in every production has its own parser test
- [ ] Every optional element (`?`) has a test with the element and without it
- [ ] do-while with a multi-statement body parses without error
- [ ] Bare `return` (no expression) parses without error
- [ ] Annotation with parameters using `=` parses without error
- [ ] Array element assignment (`id[expr] := expr`) produces ArrayElementAssignNode
- [ ] At least three deliberate parser error cases are tested and throw

**Interpreter**
- [ ] Every fully-implemented production has at least one interpreter test
- [ ] Scope isolation: variable declared in a loop body does not leak to parent
- [ ] Scope isolation: variable declared in an if body does not leak to parent
- [ ] Scope isolation: function cannot read call-site variables
- [ ] Undefined variable reference throws a descriptive exception
- [ ] Call stack depth limit (500) is enforced — tested with infinite recursion
- [ ] Integer `//` Integer returns Integer, not Float
- [ ] Integer `**` Integer (non-negative) returns Integer, not Float
- [ ] `%` on Float operands throws a type error
- [ ] Division by zero throws for `/`, `//`, and `%`
- [ ] Array element assignment mutates the list in-place
- [ ] foreach over string iterates characters
- [ ] foreach over null throws
- [ ] All six built-in functions (print, len, str, int, float, bool) are tested
- [ ] Every "not yet implemented" feature throws the correct message at runtime
- [ ] Silent no-ops are absent — every parsed node either executes or throws

**Integration**
- [ ] Every integration scenario produces fully asserted, deterministic output
- [ ] At least one integration test combines functions + loops + arrays
- [ ] At least one integration test exercises try/catch/finally with throw
- [ ] The do-while multi-statement accumulator integration test passes

**Code quality**
- [ ] Interpreter uses the Visitor pattern (INodeVisitor) — no large if-else chain
- [ ] Variable resolution uses a scope chain — no flat Dictionary copy
- [ ] All tests use `[TestClass]` and `[TestMethod]` — no XUnit or NUnit
- [ ] All tests pass with 0 failures
- [ ] No test uses `Assert.IsTrue(true)` or other vacuous assertions
- [ ] Console application prints all demo headers, outputs, and the final
      summary line "All demos completed successfully."
- [ ] Solution builds with 0 errors and 0 warnings


------------------------------------------------------------------------------------------------------------------------

# Application Description

	- Create a Class Library to Lexer the Grammar listed below.

	- Generate a Lexer for the Abstract Syntax Tree.
	- Generate a Abstract Syntax Tree Pretty Printer.
	- Generate all nodes in the Abstract Syntaxes Tree.
	- Apply the BNF Grammar Verification Strategy above to generate all unit tests.
    - Generate an Interpreter for the Abstract Syntax Tree.
    - Generate a Console application to run the Interpreter.


Grammar:
```
# BNF GRAMMAR SPECIFICATION

## COMMENTS
<comment> ::= "#" { <any_char> } <newline>
# Comments begin with # and run to end of line. They are ignored by the lexer.
# Note: "//" is floor-division (an operator), NOT a line comment.

## IMPLEMENTATION NOTES
# These resolve ambiguities the BNF alone does not settle.
# The AI must follow these rules exactly — do not invent alternatives.
#
# 1. COMMENT CHARACTER
#    "#" starts a line comment. "//" is ALWAYS the floor-division operator.
#    It is never treated as a comment under any circumstances.
#
# 2. ASSIGNMENT OPERATORS
#    ":=" is the only assignment operator for variables and declarations.
#    "=" is only valid inside annotation parameter lists: @ann(key = value).
#    A bare "=" anywhere else is a lexer Unknown token and a parse error.
#
# 3. DO-WHILE TERMINATION
#    "do <stmt_list> while <expr>" has no trailing "end".
#    The parser must use the "while" keyword as the stop signal for the
#    body's statement list. ParseStatementList must accept an optional
#    extra stop token for this purpose.
#
# 4. BARE RETURN
#    "return" followed immediately by a block terminator (end, else, catch,
#    finally, }), a semicolon, or end-of-file returns null.
#    Parsing "return" must not unconditionally demand an expression.
#
# 5. KEYWORDS AS IDENTIFIERS
#    No keyword may be used as a variable or function name under any
#    circumstances. The lexer always produces the keyword token type,
#    never Identifier, for every reserved word in the keyword table.
#
# 6. FOREACH OVER STRING
#    Iterating a string with foreach yields each character as a
#    single-character string, in order. Iterating null must throw.
#    Iterating any other non-list, non-string type must throw.
#
# 7. ARRAY ELEMENT ASSIGNMENT
#    "arr[i] := v" is structurally distinct from "arr := [...]".
#    It must be represented as its own AST node type (ArrayElementAssignNode)
#    and must mutate the existing list object in-place.
#    It must NOT be encoded as a hack inside AssignStatementNode.
#
# 8. SCOPE CHAIN
#    Variable lookup walks from the innermost scope outward to global.
#    Assignment (":=") updates the variable in the scope where it was
#    declared, not always the innermost scope.
#    "let" and "var" declarations always create a new binding in the
#    current (innermost) scope.
#
# 9. FUNCTION SCOPE
#    A function call creates a fresh scope containing only the global
#    scope as its parent plus the parameter bindings.
#    Variables from the call site are never visible inside the function.
#
# 10. OPERATOR TYPES
#    Integer ** Integer (non-negative exponent) → Integer.
#    Any other ** combination → Float.
#    Integer // Integer → Integer (no float conversion).
#    Float // anything or anything // Float → Float.
#    % operates on Integer operands only — applying to Float is a type error.

## PROGRAM STRUCTURE
<program> ::= <stmt_list>
          | <function_def> <stmt_list>
          | <class_def> <stmt_list>
          | <module_def> <stmt_list>
          | <const_declare_stmt> <stmt_list>

<stmt_list> ::= <stmt> ";" <stmt_list>
              | <stmt>

<stmt> ::= <assign_stmt>
         | <var_declare_stmt>
         | <if_stmt>
         | <while_stmt>
         | <for_stmt>
         | <foreach_stmt>
         | <do_while_stmt>
         | <print_stmt>
         | <input_stmt>
         | <array_assign_stmt>
         | <array_declare_stmt>
         | <function_call_stmt>
         | <return_stmt>
         | <switch_stmt>
         | <break_stmt>
         | <continue_stmt>
         | <try_stmt>
         | <throw_stmt>
         | <object_declare_stmt>
         | <object_call_stmt>
         | <lambda_expr>
         | <type_declare_stmt>
         | <const_declare_stmt>
         | <conditional_expr>
         | <annotated_stmt>

## ASSIGNMENT AND DECLARATION STATEMENTS
<assign_stmt> ::= <id> ":=" <expr>

<var_declare_stmt> ::= "let" <id> ":=" <expr>
                     | "var" <id> ":" <type> ":=" <expr>

<type_declare_stmt> ::= "let" <id> ":" <type> ":=" <expr>
                      | "var" <id> ":" <type> ":=" <expr>
                      | "const" <id> ":" <type> ":=" <expr>

<const_declare_stmt> ::= "const" <id> ":=" <expr>
                       | "const" <id> ":" <type> ":=" <expr>
                       | "enum" <id> "{" <enum_value_list> "}"

<enum_value_list> ::= <enum_value> "," <enum_value_list>
                    | <enum_value>

<enum_value> ::= <id>
               | <id> "=" <expr>

## CONTROL FLOW STATEMENTS
<if_stmt> ::= "if" <expr> "then" <stmt_list> ("else" <stmt_list>)? "end"

<while_stmt> ::= "while" <expr> "do" <stmt_list> "end"

# "for" with range — iterates a numeric range
<for_stmt> ::= "for" <id> ":=" <expr> "to" <expr> ("step" <expr>)? "do" <stmt_list> "end"

# "foreach" iterates over a list or string (character by character for strings)
<foreach_stmt> ::= "foreach" <id> "in" <expr> "do" <stmt_list> "end"

# "do...while" has no trailing "end" — the "while" keyword terminates the body
<do_while_stmt> ::= "do" <stmt_list> "while" <expr>

<switch_stmt> ::= "switch" <expr> "{" <case_list> "}"

<case_list> ::= "case" <expr> ":" <stmt_list> <case_list>
              | "default" ":" <stmt_list>

<break_stmt> ::= "break"

<continue_stmt> ::= "continue"

## IO STATEMENTS
<print_stmt> ::= "print" <expr>

<input_stmt> ::= "input" <id>

## FUNCTION AND METHOD DEFINITIONS
<function_def> ::= "function" <id> "(" <param_list> ")" ("->" <type>)? <stmt_list> "end"

<method_def> ::= "function" <id> "(" <param_list> ")" ("->" <type>)? <stmt_list> "end"
               | "static function" <id> "(" <param_list> ")" ("->" <type>)? <stmt_list> "end"

<param_list> ::= <param> "," <param_list>
               | <param>

<param> ::= <id>
        | <id> ":=" <expr>
        | <id> ":" <type>
        | <id> ":" <type> ":=" <expr>

<function_call_stmt> ::= <id> "(" <arg_list> ")"

# expr is optional — bare "return" returns null (used in void functions)
<return_stmt> ::= "return" (<expr>)?

## OBJECT ORIENTED PROGRAMMING
<object_declare_stmt> ::= "new" <id> ":=" <id> "(" <arg_list> ")"

<object_call_stmt> ::= <expr> "." <id> "(" <arg_list> ")"

<class_def> ::= "class" <id> ("extends" <id>)? ("implements" <id_list>)? "{" <member_list> "}"
              | "static class" <id> ("extends" <id>)? ("implements" <id_list>)? "{" <member_list> "}"

<member_list> ::= <member> <member_list>
                | <member>

<member> ::= <method_def>
           | <field_declare_stmt>
           | <const_declare_stmt>
           | <constructor_def>

<field_declare_stmt> ::= "let" <id> ":=" <expr>
                       | "let" <id> ":" <type> ":=" <expr>
                       | "var" <id> ":" <type> ":=" <expr>
                       | "const" <id> ":=" <expr>

<constructor_def> ::= "Constructor" "(" <param_list> ")" <stmt_list> "end"

<id_list> ::= <id> "," <id_list>
            | <id>

## MODULE SYSTEM
<module_def> ::= "module" <id> "{" <stmt_list> "}"
               | "module" <id> "import" <import_list> "{" <stmt_list> "}"

<import_list> ::= <import_stmt> "," <import_list>
                | <import_stmt>

<import_stmt> ::= "import" <id>
                | "import" <id> "as" <id>

<export_stmt> ::= "export" <id>

## EXPRESSIONS
<expr> ::= <term> ("+" | "-" | "&") <expr>
         | <ternary_expr>
         | <expr> "&&" <expr>
         | <expr> "||" <expr>
         | <expr> "==" <expr>
         | <expr> "!=" <expr>
         | <expr> "<" <expr>
         | <expr> ">" <expr>
         | <expr> "<=" <expr>
         | <expr> ">=" <expr>

<term> ::= <factor> ("*" | "/" | "%" | "//") <term>
         | <factor>

<factor> ::= <id>
           | <number>
           | <string>
           | <boolean>
           | "(" <expr> ")"
           | <array_access>
           | <function_call>
           | "-" <factor>
           | "not" <factor>
           | <expr> "**" <expr>
           | <member_access>
           | <method_call>
           | <cast_expr>
           | <type_check>
           | <type_assert>

<ternary_expr> ::= <bool_expr> "?" <expr> ":" <expr>

<bool_expr> ::= <bool_term> ("or" | "||") <bool_expr>
              | <bool_term>

<bool_term> ::= <bool_factor> ("and" | "&&") <bool_term>
              | <bool_factor>

<bool_factor> ::= "not" <bool_factor>
                | "(" <bool_expr> ")"
                | <expr> ("<" | ">" | "<=" | ">=" | "==" | "!=") <expr>

## ARRAYS AND COLLECTIONS
<array_assign_stmt> ::= <id> "[" <expr> "]" ":=" <expr>

<array_declare_stmt> ::= <id> ":=" "[" <expr_list> "]"
                       # NOTE: list comprehension form below is defined but not yet implemented
                       | <id> ":=" "[" <expr> "for" <id> "in" <expr> "]"

<expr_list> ::= <expr> "," <expr_list>
              | <expr>

<arg_list> ::= <expr> "," <arg_list>
             | <expr>

## LAMBDA EXPRESSIONS
<lambda_expr> ::= "function" "(" <param_list> ")" ("->" <type>)? <expr>
                | "function" "(" <param_list> ")" ("->" <type>)? <stmt_list> "end"

## EXCEPTION HANDLING
<try_stmt> ::= "try" <stmt_list> <catch_clause> ("finally" <stmt_list>)? "end"

<catch_clause> ::= "catch" <id> <stmt_list>
                 | "catch" "(" <id> ":" <type> ")" <stmt_list>

<throw_stmt> ::= "throw" <expr>

## PATTERN MATCHING
<pattern_match> ::= "match" <expr> "{" <pattern_case_list> "}"

<pattern_case_list> ::= <pattern_case> <pattern_case_list>
                      | <pattern_case>

<pattern_case> ::= <pattern> "=>" <stmt_list>
                 | <pattern> "when" <expr> "=>" <stmt_list>

<pattern> ::= <id>
            | <number>
            | <string>
            | <boolean>
            | "null"
            | "_"
            | <id> "(" <pattern_list> ")"
            | "[" <pattern_list> "]"
            | <id> "{" <field_pattern_list> "}"
            | <pattern> "|" <pattern>

<pattern_list> ::= <pattern> "," <pattern_list>
                 | <pattern>

<field_pattern_list> ::= <id> ":" <pattern> "," <field_pattern_list>
                       | <id> ":" <pattern>

## ANNOTATIONS
<annotation> ::= "@" <id>
               | "@" <id> "(" <annotation_param_list> ")"

<annotation_param_list> ::= <annotation_param> "," <annotation_param_list>
                          | <annotation_param>

<annotation_param> ::= <id> "=" <expr>

<annotated_stmt> ::= <annotation> <stmt>

## TYPE SYSTEM
<type> ::= "int"
         | "float"
         | "string"
         | "bool"
         | "array"
         | "object"
         | "null"
         | "void"
         | <id>
         | <id> "[" "]"
         | <id> "<" <type_list> ">"
         | <array_type>
         | <map_type>
         | <nullable_type>

<type_list> ::= <type> "," <type_list>
              | <type>

<array_type> ::= <type> "[" "]"

<map_type> ::= "map" "<" <type> "," <type> ">"

<nullable_type> ::= <type> "?"

## CASTING AND TYPE OPERATIONS
<cast_expr> ::= "(" <type> ")" <expr>

<type_check> ::= <expr> "is" <type>

<type_assert> ::= <expr> "as" <type>

## CONDITIONAL EXPRESSIONS
<conditional_expr> ::= "if" <expr> "then" <expr> "else" <expr>

## LITERALS AND IDENTIFIERS
<boolean> ::= "true"
            | "false"

<string> ::= '"' { <string_char> } '"'
           | "'" { <string_char> } "'"

# Strings support escape sequences: \n \t \\ \" \'
<string_char> ::= <letter> | <digit> | ' ' | "\\" <escape_seq>
<escape_seq>  ::= 'n' | 't' | '\\' | '"' | "'"

<array_access> ::= <id> "[" <expr> "]"
                 | <expr> "[" <expr> "]"

<member_access> ::= <expr> "." <id>

<method_call> ::= <expr> "." <id> "(" <arg_list> ")"

<number> ::= <digit> { <digit> } "." <digit> { <digit> }
           | <digit> { <digit> }
           | <binary_number>
           | <octal_number>
           | <hex_number>

<binary_number> ::= "0b" <binary_digit> { <binary_digit> }

<octal_number> ::= "0o" <octal_digit> { <octal_digit> }

<hex_number> ::= "0x" <hex_digit> { <hex_digit> }

<binary_digit> ::= '0' | '1'

<octal_digit> ::= '0' | '1' | '2' | '3' | '4' | '5' | '6' | '7'

<hex_digit> ::= <digit> | 'a' | 'b' | 'c' | 'd' | 'e' | 'f'
              | 'A' | 'B' | 'C' | 'D' | 'E' | 'F'

# Identifiers may contain underscores but must not start with one (coding style rule)
<id> ::= <letter> { (<letter> | <digit> | '_') }

<letter> ::= 'a'...'z' | 'A'...'Z'

<digit> ::= '0'...'9'

## TERMINAL SYMBOLS
<terminal> ::= <id>
             | <number>
             | <string>
             | <boolean>
             | <type>
             | keyword
             | operator
```
