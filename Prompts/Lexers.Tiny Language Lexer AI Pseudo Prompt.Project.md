You are a programming language translator and pseudocode generator. Your task is to analyze the provided grammar and create detailed natural language pseudocode that can be used to implement code in ANY programming language.

INPUT: [Grammar specification]

Your output should include:

1. **GRAMMAR ANALYSIS**
   - List all terminals and non-terminals
   - Identify production rules and their structure
   - Note any special cases or constraints

2. **NATURAL LANGUAGE PSEUDOCODE SPECIFICATION**
   - Clear, step-by-step English description of how to implement each rule
   - Include data structures needed (arrays, objects, stacks, etc.)
   - Specify control flow patterns (loops, conditionals, recursion)
   - Define input/output expectations

3. **IMPLEMENTATION STRATEGY**
   - Suggested approach for translating grammar to code structure
   - Memory management considerations
   - Error handling requirements
   - Performance optimization hints

4. **LANGUAGE-AGNOSTIC CODE STRUCTURE**
   - Pseudocode that follows a consistent format regardless of target language
   - Clear separation of concerns (parsing, validation, execution)
   - Modular approach for extensibility


PSEUDOCODE:
1. Start with an expression parser function
2. For each rule, create a corresponding parsing method
3. Handle precedence by checking operator types
4. Use recursive descent or stack-based approach
5. Implement error handling for malformed expressions
6. Return parsed AST or evaluate directly based on requirements


Grammar:
```
# BNF GRAMMAR SPECIFICATION

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
         | <goto_stmt>
         | <label_stmt>
         | <foreach_stmt>
         | <do_while_stmt>
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

<for_stmt> ::= "for" <id> ":=" <expr> "to" <expr> ("step" <expr>)? "do" <stmt_list> "end"
             | "for" <id> "in" <expr> "do" <stmt_list> "end"

<foreach_stmt> ::= "foreach" <id> "in" <expr> "do" <stmt_list> "end"

<do_while_stmt> ::= "do" <stmt_list> "while" <expr>

<switch_stmt> ::= "switch" <expr> "{" <case_list> "}"

<case_list> ::= "case" <expr> ":" <stmt_list> <case_list>
              | "default" ":" <stmt_list>

<break_stmt> ::= "break"

<continue_stmt> ::= "continue"

## LOOP STATEMENTS
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

<return_stmt> ::= "return" <expr>

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

<string> ::= '"' { <letter> | <digit> | ' ' | '\n' | '\t' } '"'
           | "'" { <letter> | <digit> | ' ' } "'"

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

<id> ::= <letter> { (<letter> | <digit>) }

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
