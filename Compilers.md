**Compilers**

- The compiler takes as input just your program and then it produces an executable. And this executable is another program might be assembly language, it might be byte code or it could be in any number of different implementation languages. This can be run separately on your data and that will produce the output. The compiler is offline, meaning that we pre-process the program first. A compiler is essentially a pre-processing step that produces the executable and then we can run that same executable on many many different inputs on many different datasets without having to recompile or do any other processing of the program.

**Interpreters**

- It takes the input of your program that you wrote and whatever data that you want to run the program on and it produces the output directly, meaning that it doesn't do any processing of the program before it executes it on the input. So you just write the program and you invoke the interpreter on the data and the program immediately begins running. We can say that an interpreter is online. Meaning the work that it does is all part of running your program.

---

The most important applications in 1950s were scientific computations and programmers thought in turns of writing down formulas that the machine could execute. John Backus thought that the problem with speed-coding was that the formulas were in fact interpreted and he thought if first the formulas were translated into a form that the machine could execute directly that the code would be faster and while still allowing the programmer to write the programs at a high level and thus was the formula translation project or FORTRAN I born.

It was a very successful project by 1958 over 50% of all code was written in FORTRAN. 

- The first compiler
  
  - Huge impact on CS

- Led to an enormous body of theoretical work

- Modern compilers preserve the outline of FORTRAN I

---

The structure of FORTRAN:

- 1. Lexical Analysis
  
  2. Parsing
  
  3. Semantic Analysis
  
  4. Optimization
  
  5. Code Generation

- Recognize words
  
  - Smallest unit above letters

- Lexical analysis divides program text into "words" or "tokens"

- Once words are understood, the next step is to understand sentence structure

- Parsing = Diagramming Sentences
  
  - The diagram is a tree

- Once sentence structure is understood, we can try to understand "meaning"
  
  - This is too hard for compilers! Actually we don't know how this works for humans.

- Compilers perform limited semantic analysis to catch inconsistencies

- Programming languages define strict rules to avoid ambiguities

- Compilers perform many semantic checks besides variable bindings

- Optimization has no strong counterpart in English
  
  - But a little bit like editing

- Automatically modify programs so that they
  
  - Run faster
  
  - Use less memory

- Produces assembly code (usually)

- A translation into another language
  
  - Analogous to human translation

The proportions have changed since FORTRAN.

If we were to go back to FORTRAN I and look inside of that compiler we would probably see a size and complexity that looks something like this:

We'd have a fairly complex lexical analysis phase, equally complicated parsing phase. A very small semantic analysis phase, a fairly involved optimization phase and another fairly involved code generation phase.

So we'd see a compiler where the complexity was spread fairly evenly throughout except semantic analysis which is very weak in the early days.

Today if we look at a modern compiler you'll see almost nothing in lexical, very little in parsing because we have extremely good tools to help us write those two phases. We would see a fairly involved semantic analysis phase and a very large optimization phase and this is in fact the dominant component of all modern compilers. And a very small code generation phase because again we understand that phase very very well.

---

The application domains for programming have very distinctive and conflicting needs. It's very hard to design one language that would actually do everything in every situation for all programmers.

- Scientific computing:
  
  - good FP
  
  - good arrays
  
  - parallelism

- Business application:
  
  - persistence
  
  - report generation
  
  - data analysis

- Systems programming
  
  - control of resources
  
  - real time constraints

Programmer training is the dominant cost for a programming language.

Maybe 10 to 20 people for a very large compiler project can build quite a good compiler.

- Widely used languages are slow to change.

- It's easy to start a new language.

- Languages adopted to fill a void.

New languages tend to look like old languages.

There is no  universally accepted metric for language design.

---

### Lexical Analysis

Token classes correspond to sets of strings.

- Identifier:
  
  - strings of letters or digits, starting with a letter

- Integer:
  
  - a non-empty string of digits

- Keyword:
  
  - "else" or "if" or "begin" or ...

- Whitespace:
  
  - a non-empty sequence of blanks, newlines, and tabs

- Classify program substrings according to role

- Communicate tokens to the parser

An implementation must do two things:

1. Recognize substrings corresponding to tokens
   
   - The lexemes

2. Identify the token class of each lexeme

FORTRAN rule: Whitespace is insignificant

- VAR1 is the same as VA R1

The goal is to partition the string. This is implemented by reading left-to-right, recognizing one token at a time.

"Lookahead" may be required to decide where one token ends and the next token begins. Lookahead is always needed, but we would like to minimize the amount of look ahead and in fact we'd like to bound it to some constant this because that will simplify the implementation of lexical analyzer quite a bit. Lookahead is something that we always have to worry about.

- C++ template syntax:
  
  - Foo<Bar>

- C++ stream syntax:
  
  - cin >> var;

The goal of lexical analysis is to

- Partition the input string into lexemes

- Identify the token of each lexeme

Left-to-right scan => lookahead sometimes required

Lexical structure = token classes

We must say what set of strings is in a token class

- Use regular languages
  
  - Single character
  
  - Epsilon
  
  - Union
  
  - Concatenation
  
  - Iteration

Def. The regular expressions over ∑ are the smallest set of expressions including

Regular expressions specify regular languages

Five constructs

- Two base cases
  
  - empty and 1-character strings

- Three compound expressions
  
  - union, concatenation, iteration

Def. Let ∑ be a set of characters (an alphabet). 

A language over ∑ is a set of strings of characters drawn from ∑

Meaning function L maps syntax to semantics

Why use a meaning function?

- Makes clear what is syntax, what is semantics.

- Allows us to consider notation as a separate issue

- Because expressions and meanings are not 1-1

Meaning is many to one, never one to many!

Regular expressions describe many useful languages

Regular languages are a language specification

- We still need an implementation

---

### Lexical Specification

- At least one: $A^+$ $\equiv$ $AA^*$

- Union: $A | B $ $\equiv$ $A+B$

- Option: $A?$ $\equiv$ $A + \epsilon$

- Range: '$a$'+'$b$'+...+'$z$' $\equiv$ $[a-z]$

- Excluded range:
  
  complement of $[a-z]$ $\equiv$ [^a-z]
1. Write a rexp for the lexemes of each token class
   
   - Number = digit+
   
   - Keyword = 'if' + 'else' + ...
   
   - Identifier = letter (letter + digit)*
   
   - OpenPar = '('
   
   - ...

2. Construct $R$, matching all lexemes for all tokens
   
   - $R$ = Keyword + Identifier + Number + ...
     
         = $R_1$ + $R_2$ + ...

3. Let input be $x_1$ ... $x_n$
   
   For 1 ≤ i ≤ n check

                    $x_1 ... x_i$ ∈ $L(R)$

4. If success, then we know that
   
         $x_1 ... x_i$ ∈ $L(R_j)$ for some j

5. Remove $x_1 ... x_i$ from input and go to (3)

Regular expressions are a concise notation for string patterns

Use in lexical analysis requires small extensions

- To resolve ambiguities

- To handle errors

Good algorithms known

- Require only single pass over the input

- Few operations per character (table lookup)

Regular expressions = specification

Finite automata = implementation

A finite automaton consists of

- An input alphabet $∑$

- A set of states $S$

- A start state $n$

- A set of accepting states $F ⊆ S$

- A set of transitions $state$ →$^{input}state$

Transition

    $S_1$ → $^{a}S_2$

Is read

    In state $s_1$ on input $a$ go to state $s_2$

If end of input and in accepting state => accept

Otherwise => reject

Finite Automata:

- A finite automaton that accepts only "1"

- A finite automaton accepting any number of 1's followed by a single 0
  
  Alphabet: {0,1}

- Another kind of transition: $\epsilon$-moves

- Deterministic Finite Automata (DFA)
  
  - One transition per input per state
  
  - No $\epsilon$-moves

- Nondeterministic Finite Automata (NFA)
  
  - Can have multiple transitions for one input in a given state
  
  - Can have $\epsilon$-moves

NFAs and DFAs recognize the same set of languages - regular languages

DFAs are faster to execute - There are no choices to consider

NFAs are, in general, smaller

Lexical Specification → Regular expressions → NFA → DFA → Table-driven Implementation of DFA

---

### Parsing

Regular languages

- The weakest formal languages widely used

- Many applications

| Phase  | Input                | Output           |
| ------ | -------------------- | ---------------- |
| Lexer  | String of characters | String of tokens |
| Parser | String of tokens     | Parse tree       |

Not all strings of tokens are programs

Parser must distinguish between valid and invalid strings of tokens

We need

- A language for describing valid strings of tokens

- A method for distinguishing valid from invalid strings of tokens

Programming languages have recursive structure

An EXPR is 

    if EXPR then EXPR else EXPR fi

    while EXPR loop EXPR pool

    ...

Context-free grammars are a natural notation for this recursive structure

A CFG consists of

- A set of terminals

- A set of non-terminals

- A start symbol

- A set of productions

Productions can be read as rules

1. Begin with a string with only the start symbol $S$

2. Replace any non-terminal $X$ in the string by the right-hand side of some production $X$ → $Y_1 ... Y_n$

3. Repeat (2) until there are no non-terminals

The idea of a CFG is a big step. But:

- Membership in a language is "yes" or "no"; also need parse tree of the input

- Must handle errors gracefully

- Need an implementation of CFG's (e.g., bison) 

Form of the grammar is important

- Many grammars generates the same language

- Tools are sensitive to the grammar

A derivation is a sequence of productions

A derivation can be drawn as a tree

- Start symbol is the tree's root

- For a production $X$ → $Y_1 ... Y_n$ add children $Y_1 ... Y_n$ to node $X$

A parse tree has

- Terminals at the leaves

- Non-terminals at the interior nodes

An in-order traversal of the leaves is the original input

The parse tree shows the association of operations, the input string does not

Note that right-most and left-most derivations have the same parse tree

We are not just interested in whether $s ∈ L(G)$

- We need a parse tree for $s$

A derivation defines a parse tree

- But one parse tree may have many derivations

Left-most and right-most derivations are important in parser implementation

There are several ways to handle ambiguity

Most direct method is to rewrite grammar unambiguously

Enforces precedence of * over +

Impossible to convert automatically an ambiguous grammar to an unambiguous one

Used with care, ambiguity can simplify the grammar

- Sometimes allows more natural definitions

- We need disambiguation mechanisms
  
  Instead of rewriting the grammar

- Use the more natural (ambiguous) grammar

- Along with disambiguating declarations

Most tools allow precedence and associativity declarations to disambiguate grammars

**Error Handling**:

Purpose of the compiler is

- To detect non-valid programs

- To translate the valid ones

Many kinds of possible errors (e.g. in C)

| Error kind  | Example                  | Detected by ... |
| ----------- | ------------------------ | --------------- |
| Lexical     | ... $ ...                | Lexer           |
| Syntax      | ... x * % ...            | Parser          |
| Semantic    | ... int x; y = x(3); ... | Type checker    |
| Correctness | your favorite program    | Tester / User   |

Error handler should

- Report errors accurately and clearly

- Recover from an error quickly

- Not slow down compilation of valid code

- Panic mode

- Error productions

- Automatic local or global correction

Panic mode is simplest, most popular method.

When an error is detected:

- Discard tokens until one with a clear role is found

- Continue from there

Looking for synchronizing tokens

- Typically the statement or expression terminators

Error productions

- specify known common mistakes in the grammar

- disadvantage: Complicates the grammar

Error Correction

- Idea: find a correct "nearby" program
  
  - Try token insertions and deletions
  
  - Exhaustive search

Disadvantages:

- Hard to implement

- Slows down parsing of correct programs

- "Nearby" is not necessarily "the intended" program

The best known example of error correction is the compiler PL/C, this is a PL/1 compiler that's the PL part and the C stands for either correction or cornell which is where the compiler was built. PL/C is well known for being to compile absolutely anything you could give. It would print out error messages and it would in the end do correction and produce always a valid running PL/1 program.

Past

- Slow recompilation cycle (even once a day)

- Find as many errors in one cycle as possible

Present

- Quick recompilation cycle

- Users tend to correct one error/cycle

- Complex error recovery is less compelling

**Abstract Syntax Trees**:

A parser traces the derivation of a sequence of tokens

But the rest of the compiler needs a structural representation of the program

Abstract syntax trees

- Like parse trees but ignore some details

- Abbreviated as AST

If a production for non-terminal X succeeds

- Cannot backtrack to try a different production for X later

General recursive-descent algorithms support such "full" backtracking

- Can implement any grammar

Presented recursive descent algorithm is not general

- But is easy to implement by hand

Sufficient for grammars where for any non-terminal at most one production can succeed

Left Recursion:

Recursive descent

- Simple and general parsing strategy

- Left-recursion must be eliminated first

- but that can be done automatically

---

### Predictive Parsing

Like recursive-descent but parser can "predict" which production to use

- By looking at the next few tokens

- No backtracking

Predictive parsers accept LL(k) grammars

**LL(k)**:

- **l**eft-to-right

- **l**eft-most derivation

- **k** tokens lookahead (k = i)

In recursive descent,

- At each step, many choices of production to use

- Backtracking used to undo bad choices

In LL(1),

- At each step, only one choice of production
