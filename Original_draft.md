# Skyz

# SKYZ — `.Skyz`

## Consolidated Language Architecture and Core Specification

**Skyz** is a statically typed, ahead-of-time compiled native systems programming language built around explicit programmer control over compilation, optimization, graph execution, register use, memory, concurrency, and machine-level behavior.

Skyz combines:

- C-style semantics
- C-style memory
- C-style control flow
- C-style concurrency
- explicit manual optimization
- a custom intermediate representation
- a custom SSA engine
- a diagrammatic graph-based AST
- a machine-intuitive semantic lattice
- programmer-controlled register allocation
- virtual code generation
- reflective object-file emission
- condition-driven sequence concurrency
- tagged accept/reject results
- aggressive compile execution
- five-space structural indentation

Skyz is designed around a simple premise:

> **The programmer understands the problem. The compiler understands the machine. Skyz lets both participate in optimization.**

Its second governing principle is:

> **Anything already known should disappear before runtime whenever safely possible.**

The compiler therefore does not merely translate source code.

It progressively evaluates, folds, collapses, merges, specializes, schedules, allocates, lowers, and emits what still needs to exist when the program actually runs.

---

# 1. Language Identity

Skyz is a native compiled systems language.

It does not depend on LLVM as its compiler backend.

Its core compiler architecture is custom.

The language provides direct access to:

- memory
- pointers
- machine-sized values
- structures
- unions
- arithmetic
- registers
- concurrency
- explicit execution paths
- compile-time computation
- graph dependencies
- optimization decisions

Skyz intentionally keeps the physical machine visible.

High-level constructs are allowed, but they must lower into understandable machine operations.

The language does not require a garbage collector, managed virtual machine, JIT runtime, or heavyweight runtime environment.

---

# 2. Core Compilation Pipeline

The canonical Skyz compilation pipeline is:

```text
.Skyz source
     ↓
Bit-Style Tokenizer
     ↓
QRTG
     ↓
Definer
     ↓
Quantifier
     ↓
Diagrammatic Graph AST
     ↓
Semantic Resolution
     ↓
Machine-Intuitive Semantic Lattice
     ↓
Custom Skyz IR
     ↓
Custom SSA Engine
     ↓
Compile Execution
     ↓
Constant Folding
     ↓
Graph Collapsing
     ↓
Graph Merging
     ↓
Explicit / Automatic Optimization
     ↓
Register Allocation
     ↓
Virtual Code Generator
     ↓
Target Lowering
     ↓
Mirror / Reflective Object Writer
     ↓
COFF / ELF / Mach-O object
     ↓
LD / LLD / MSVC linker
     ↓
Native executable
```

Skyz owns all compiler stages through object-file generation.

External linkers are used only for final program assembly.

---

# 3. Source Structure

Skyz uses indentation as syntax.

One indentation level is exactly:

```text
5 spaces
```

Example:

```skyz
task main() -> int
     int x = 10

     if x > 5
          display(x)

     return 0
```

Tabs are not canonical Skyz indentation.

A compiler may optionally normalize tabs before parsing, but canonical source representation uses spaces.

---

# 4. Tasks

Skyz uses the keyword:

```text
task
```

instead of `function`.

A task is a callable unit of executable work.

A task may represent:

- an ordinary function
- a procedure
- a computation
- a graph node
- a concurrent worker
- a pipeline stage
- a compile-time operation
- a scheduled event
- a fallback handler

Example:

```skyz
task add(int a, int b) -> int
     return a + b
```

A task is therefore broader than a conventional C function while retaining native function semantics where appropriate.

---

# 5. Primitive Declaration Style

Skyz uses C-style declaration ordering:

```text
type identifier
```

Examples:

```skyz
int count
float velocity
double position
char symbol
bool ready
uint64 address
```

Function parameters use the same form:

```skyz
task calculate(int x, float y) -> double
```

Skyz does not use:

```text
identifier: type
```

for ordinary primitive declarations.

---

# 6. Primitive Types

A foundational Skyz implementation may support:

```text
bool

char
byte

int8
uint8

int16
uint16

int32
uint32

int64
uint64

int
uint

float
double

usize
isize

void
```

Platform-neutral fixed-width types retain exact widths.

`int`, `uint`, `usize`, and `isize` may follow target-machine conventions defined by the ABI profile.

---

# 7. Expressions

Expressions produce values.

Examples:

```skyz
x + y
a * b
value == expected
buffer[index]
ptr->member
calculate(a, b)
x > y
```

Expressions may be:

- arithmetic
- logical
- comparative
- pointer-based
- member-access
- call-based
- generic
- range-based
- conditional
- compile-time evaluable

---

# 8. Statements

Statements perform actions.

Examples:

```skyz
int x = 20

x += 1

return x

accept x

reject Error.Invalid

perform fallback

delete task
```

Skyz remains primarily imperative even though its internal representation is graph-oriented.

---

# 9. C-Style Semantics

Skyz preserves a direct machine-oriented semantic model.

Fundamental concepts include:

```text
values
addresses
pointers
arrays
structures
unions
mutation
integer arithmetic
native calls
explicit control flow
memory layout
alignment
machine representation
```

The programmer may reason directly about how values exist in memory and how work maps toward machine execution.

---

# 10. Memory Model

Skyz uses explicit C-style memory.

Pointers are directly representable.

Example:

```skyz
int* ptr
byte* buffer
```

Arrays may use forms such as:

```skyz
int values[64]
byte memory[4096]
```

Dynamic allocation may be provided through compiler intrinsics or standard libraries:

```skyz
byte* data = alloc<byte>(4096)

free(data)
```

Skyz does not require automatic garbage collection.

Memory semantics include:

- stack allocation
- static allocation
- heap allocation
- pointers
- address arithmetic
- explicit freeing
- alignment
- aliasing
- volatile access
- atomic access
- contiguous layout

---

# 11. Structures

Structures use C-style layout semantics unless explicitly modified.

Example:

```skyz
struct Vector
     float x
     float y
     float z
```

Usage:

```skyz
Vector position
position.x = 12.0
```

---

# 12. Unions

Skyz supports unions.

```skyz
union Value
     int i
     float f
     byte b
```

Tagged unions are also used internally and explicitly by higher-level result types.

---

# 13. Generics

Skyz supports compile-time generic specialization.

Example:

```skyz
task max<T>(T a, T b) -> T
     if a > b
          return a

     return b
```

Generics are normally monomorphized.

For example:

```text
max<int>
max<uint64>
max<double>
```

become specialized graph and IR instances.

Generic specialization integrates with:

- constant folding
- collapsing
- merging
- register allocation
- type resolution
- lattice inference

---

# 14. Ranges

Skyz supports explicit inclusive ranges using:

```text
...
```

Both:

```skyz
0...100
```

and:

```skyz
0 ... 100
```

mean:

```text
0 through 100 inclusive
```

Example:

```skyz
for x in 0...100
     display(x)
```

This iterates over:

```text
0
1
2
...
99
100
```

A range is a real semantic value.

Example:

```skyz
range<int> numbers = 0...100
```

---

# 15. Count-Based Ranges

Skyz also supports:

```skyz
range(25)
```

as a count-oriented sequence.

Its canonical meaning is:

```text
0...24
```

This creates a useful distinction:

```skyz
0...25
```

means an explicit interval containing twenty-six values.

While:

```skyz
range(25)
```

means twenty-five sequence positions.

This prevents unnecessary ambiguity in loop construction.

---

# 16. Future Range Forms

The range system may support stepped ranges:

```skyz
0...100 step 5
```

and descending ranges:

```skyz
100...0 step -1
```

These are extensions of the same core range model.

---

# 17. Control Flow

Skyz supports familiar native control flow.

## If

```skyz
if x > y
     display(x)
else
     display(y)
```

## While

```skyz
while x < 25
     display(x)
     x += 1
```

## For

```skyz
for x in range(25)
     display(x)
```

or:

```skyz
for x in 0...100
     display(x)
```

---

# 18. Assignment and Comparison

Normal assignment uses:

```skyz
x = y
```

Ordinary equality comparison uses:

```skyz
x == y
```

However, within dedicated case grammar, single `=` may be interpreted as a match relation because the QRTG already establishes grammatical context.

For example:

```skyz
in case x = y, do nothing
```

means:

```text
match x against y
```

rather than assignment.

This is context-defined syntax rather than general operator overloading.

---

# 19. Case-Oriented Control Flow

Skyz supports ordered, readable case-driven execution.

Case syntax is designed for fallback logic, contingency processing, progressive decision making, and graph delegation.

Example:

```skyz
when conditions exceeded, resort to method ->
     in case x = y, do nothing
     when case x > y, perform z
     unless z < x, in which case perform w
     in case of w < x, perform speculate
     in case speculation fails, perform undefined
     in case undefined fails, delete task
```

This is not merely a replacement for `switch`.

It represents an ordered decision graph.

Conceptually:

```text
primary execution
       ↓
condition exceeded
       ↓
resort to method
       ↓
case x = y
       ↓ otherwise
case x > y
       ↓ otherwise
unless z < x
       ↓ otherwise
w < x
       ↓
speculate
       ↓ failure
undefined
       ↓ failure
delete task
```

---

# 20. `in case`

`in case` introduces a conditional branch inside an ordered fallback structure.

Example:

```skyz
in case x = y, do nothing
```

The branch executes when its matching condition is satisfied.

---

# 21. `when case`

`when case` evaluates an explicit condition in the current decision chain.

```skyz
when case x > y, perform z
```

---

# 22. `unless`

`unless` expresses negative conditional logic.

Example:

```skyz
unless z < x, in which case perform w
```

Conceptually:

```text
if NOT(z < x)
     perform w
```

The precise meaning of `unless` is resolved from its QRTG context.

---

# 23. `perform`

`perform` explicitly executes or delegates an operation.

Example:

```skyz
perform z
```

It may execute:

- a task
- an operation
- a named graph node
- a fallback routine
- a sequence
- a runtime handler
- a compile-time operation

Within a graph, `perform` may represent delegation rather than only a conventional function call.

---

# 24. `resort to`

`resort to` transfers execution from a primary path into a fallback method or contingency graph.

Example:

```skyz
when conditions exceeded, resort to method ->
```

Conceptually:

```text
normal path
     │
     ├── continue
     │
     └── threshold exceeded
               ↓
             method
```

---

# 25. `do nothing`

Skyz explicitly supports:

```skyz
do nothing
```

This represents a semantic no-op.

A no-op may remain temporarily in the graph for structural reasons, then disappear during graph collapsing.

Conceptually:

```text
NOP
 ↓
collapse
 ↓
nothing
```

---

# 26. `speculate`

Skyz supports explicit speculation.

Example:

```skyz
perform speculate
```

Speculation is never implicitly assumed merely because the compiler believes an optimization may work.

The programmer explicitly requests speculative behavior.

A speculative path may resolve into states such as:

```text
accepted
rejected
unresolved
failed
```

Example:

```skyz
in case of w < x, perform speculate
```

---

# 27. Explicit Undefined State

Skyz distinguishes intentional undefined state from accidental compiler undefined behavior.

Example:

```skyz
perform undefined
```

This represents an explicit semantic state or recovery mechanism.

The semantic lattice may distinguish:

```text
known
unknown
undefined
rejected
contradictory
```

An explicit Skyz undefined state is representable and inspectable.

It is not equivalent to arbitrary implementation behavior.

---

# 28. `delete task`

Skyz supports:

```skyz
delete task
```

This means the current task ceases to participate in further execution.

At runtime, this may terminate the current scheduled task.

During compile execution or graph transformation, it may remove a node and any unreachable descendants.

Example:

```skyz
in case undefined fails, delete task
```

---

# 29. Tagged Accept / Reject Results

Skyz uses tagged result semantics.

Example:

```skyz
task divide(int a, int b) -> result<int c, DivideError>
     if b == 0
          reject DivideError.Zero

     accept a / b
```

The return type:

```skyz
result<int c, DivideError>
```

defines:

```text
ACCEPT → int c
REJECT → DivideError
```

Internally, a result is a tagged union.

Conceptually:

```text
┌────────────────┐
│ result tag     │
├────────────────┤
│ int c OR error │
└────────────────┘
```

Accept/reject semantics participate directly in the graph.

```text
            divide
              │
       ┌──────┴──────┐
       │             │
    ACCEPT         REJECT
       │             │
     int c       DivideError
```

---

# 30. Delegation

Skyz is delegation-oriented.

Computation may be represented as connected nodes rather than only deeply nested function calls.

Traditional call model:

```text
A calls B
B calls C
C calls D
```

Skyz graph model:

```text
      validate
      /      \
 input      inspect
      \      /
       normalize
           |
         output
```

A node may delegate work to another node.

Results and conditions determine which graph edge becomes active.

---

# 31. Diagrammatic Graph AST

The Skyz AST is not primarily a conventional nested syntax tree.

It is a diagrammatic execution and dependency graph.

Example:

```text
       input
       /   \
      A     B
       \   /
       merge
         |
      compare
      /     \
 accept     reject
```

The AST records:

- dependencies
- sequencing
- value flow
- conditions
- control edges
- delegation
- acceptance
- rejection
- task boundaries
- sequence relationships
- concurrency relationships

This makes subsequent SSA and optimization passes naturally graph-based.

---

# 32. QRTG

Skyz uses the:

# QRTG — Quick Reference Table Grammar

QRTG is the authoritative compact grammar reference used by the parser architecture.

Rather than making parser implementation details the language specification, QRTG describes language forms declaratively.

Example:

| Construct | Definer Pattern             | Quantity | Produces      |
| --------- | --------------------------- | -------: | ------------- |
| Task      | `task identifier`           |        1 | TaskNode      |
| Parameter | `type identifier`           |     0..N | Parameter     |
| Result    | `result<...>`               |     0..1 | ResultNode    |
| Body      | indentation +5              |     1..N | Region        |
| Accept    | `accept expression`         |     0..1 | AcceptEdge    |
| Reject    | `reject expression`         |     0..1 | RejectEdge    |
| Generic   | `<definition>`              |     0..N | GenericSet    |
| Range     | `expression ... expression` |     0..1 | RangeNode     |
| Case      | `in case condition`         |     0..N | CaseEdge      |
| Sequence  | `sequence identifier`       |     0..N | SequenceGraph |
| Event     | `event identifier`          |     0..N | EventNode     |

QRTG remains readable enough to function as a quick language reference while also guiding parsing.

---

# 33. Bit-Style Tokenizer

Skyz uses a compact token classification system.

Tokens may be classified using bit-like metadata.

Conceptually:

```text
00000001 identifier
00000010 keyword
00000100 operator
00001000 literal
00010000 delimiter
00100000 indentation
01000000 type
10000000 graph/control marker
```

A token may carry multiple semantic properties when appropriate.

The tokenizer is intended to remain lightweight, deterministic, and efficient.

---

# 34. Definer

The Definer determines:

> **What grammatical construct is this?**

Examples:

```text
task       → TaskDeclaration
if         → Conditional
while      → Loop
accept     → AcceptTransition
reject     → RejectTransition
sequence   → SequenceDeclaration
event      → EventDeclaration
```

The Definer identifies structure.

---

# 35. Quantifier

The Quantifier determines:

> **How much source belongs to this construct?**

Examples:

```text
parameter  → 0..N
argument   → 0..N
task body  → 1..N
case       → 0..N
generic    → 0..N
event      → 0..N
```

The parser therefore conceptually follows:

```text
tokens
   ↓
QRTG
   ↓
Definer
   ↓
Quantifier
   ↓
graph construction
```

---

# 36. Semantic Resolution

After graph construction, Skyz resolves:

- identifiers
- types
- generic substitutions
- overloads
- memory semantics
- ranges
- accept/reject contracts
- task boundaries
- case relationships
- sequence conditions
- graph dependencies

This creates the semantic graph used by later stages.

---

# 37. Machine-Intuitive Semantic Lattice

Skyz maintains a semantic lattice describing what is known about each value and operation.

Example:

```text
unknown
   ↓
integer
   ↓
int32
   ↓
positive int32
   ↓
0...255
   ↓
constant 17
```

The lattice may track:

- type
- range
- constantness
- signedness
- alignment
- aliasing
- provenance
- mutability
- memory location
- pointer validity
- atomicity
- overflow properties
- register suitability
- lifetime
- compile-time evaluability
- acceptance state
- rejection state
- sequence readiness

Optimization is driven by established facts rather than blind guessing.

---

# 38. Custom Skyz IR

Skyz lowers into a custom typed intermediate representation.

The IR is:

- graph-based
- typed
- SSA-aware
- register-aware
- memory-aware
- control-aware
- accept/reject aware
- sequence-aware
- optimization-directive aware

Conceptual IR:

```text
%1 = load.i32 %a
%2 = load.i32 %b
%3 = add.checked.i32 %1, %2
return %3
```

Tagged result form:

```text
%3 = div.checked.i32 %a, %b

branch.accept %3 -> block.accept
branch.reject %3 -> block.reject
```

Optimization-directed forms may include:

```text
fold %4
collapse %7
merge %8, %9
bind.reg %12, rax
```

---

# 39. Custom SSA Engine

Skyz contains its own Static Single Assignment engine.

SSA construction follows graph topology.

Example:

```text
        x0
       /  \
     +1    +7
      |     |
     x1    x2
       \   /
       merge
         |
        x3
```

Internally:

```text
x3 = merge(x1, x2)
```

Source code does not need to expose conventional phi syntax.

Skyz merge nodes can naturally express value convergence.

---

# 40. The Programmer as Optimizer

One of Skyz's defining features is that optimization is exposed to the programmer.

Rather than only:

```text
-O0
-O1
-O2
-O3
```

Skyz allows explicit optimization operations.

Potential optimization verbs include:

```text
fold
collapse
merge
inline
specialize
bind
align
assume
flatten
coalesce
delegate
```

The programmer may directly state known optimization intent.

The compiler remains responsible for validating whether that transformation is legal.

Conceptually:

```text
PROGRAMMER
     ↓
optimization request
     ↓
SEMANTIC LATTICE
     ↓
validation
     ↓
CUSTOM IR
     ↓
transformation
```

The programmer does not replace correctness checking.

The programmer gains control over optimization decisions.

---

# 41. Constant Folding

Skyz evaluates compile-time-known expressions.

Example:

```skyz
int x = 10 * 20 + 5
```

becomes:

```skyz
int x = 205
```

before code generation.

Whole tasks may also disappear if their outputs are completely known at compile time.

Example:

```skyz
task dimensions() -> int
     return 20 * 40
```

may reduce to:

```text
800
```

where semantically legal.

---

# 42. Graph Collapsing

Collapsing removes unnecessary graph structure.

Example:

```text
A
↓
temporary
↓
identity
↓
B
```

becomes:

```text
A
↓
B
```

Collapsing operates on graph topology rather than only arithmetic constants.

---

# 43. Graph Merging

Merging combines equivalent or compatible computation.

Example:

```text
load A
load A
```

may become:

```text
 load A
 /    \
use1  use2
```

Merging can reduce duplicated work and improve graph density.

Skyz therefore distinguishes:

```text
FOLD      known values
COLLAPSE  unnecessary structure
MERGE     equivalent computation
```

---

# 44. Compile Execution

Skyz compilation performs execution whenever required information is already known.

The central model is:

```text
source
  ↓
what is already knowable?
  ↓
execute it
  ↓
what is constant?
  ↓
fold it
  ↓
what structure is unnecessary?
  ↓
collapse it
  ↓
what work is equivalent?
  ↓
merge it
  ↓
what remains dynamic?
  ↓
generate code only for that
```

Skyz therefore treats compilation as progressive elimination of runtime work.

---

# 45. Checked Arithmetic

Skyz arithmetic behavior is formally defined by Skyz semantics.

The compiler may implement checked arithmetic internally using C++23 functions and helper routines.

Architecture:

```text
Skyz arithmetic semantics
          ↓
checked arithmetic abstraction
          ↓
C++23 compiler implementation
```

The language does not inherit arbitrary host-language undefined behavior merely because the compiler is implemented in C++23.

---

# 46. Overflow Modes

Skyz may expose explicit arithmetic modes such as:

```text
checked
wrapping
saturating
exact
unchecked
```

Example future syntax:

```skyz
checked int c = a + b
```

The semantic lattice records the applicable arithmetic mode.

---

# 47. Register Allocation

Skyz exposes register allocation to the programmer.

Example conceptual form:

```skyz
bind accumulator -> rax
bind source -> rcx
bind count -> rdx
```

The compiler verifies:

- target register existence
- width compatibility
- ABI restrictions
- calling convention rules
- live-range conflicts
- clobber rules

Skyz also supports automatic allocation.

Conceptually:

```text
register auto
```

and:

```text
register explicit
```

The governing rule is:

> **The compiler may choose by default, but the programmer may take control when necessary.**

---

# 48. Virtual Code Generator

Skyz does not require direct IR-to-target lowering.

It uses a virtual code-generation layer.

Pipeline:

```text
Skyz IR
   ↓
Virtual Instructions
   ↓
Instruction Selection
   ↓
Target Legalization
   ↓
Physical Machine Instructions
```

Example virtual operations:

```text
VLOAD
VSTORE
VADD
VSUB
VMUL
VDIV
VCMP
VBRANCH
VCALL
VRETURN
```

These are compiler-internal virtual operations, not runtime VM bytecode.

There is no requirement for a Skyz virtual machine at runtime.

---

# 49. Target Backends

The virtual code generator may support:

```text
x86-64
AArch64
RISC-V
```

and additional targets over time.

Each backend handles:

- instruction selection
- physical register mapping
- calling conventions
- ABI rules
- stack frames
- relocations
- target-specific instructions

---

# 50. Mirror / Reflective Object Writer

Skyz uses a reflective object writer.

The final generated program is mirrored into an object model containing:

- code sections
- data sections
- symbols
- relocations
- imports
- exports
- alignment
- function boundaries
- unwind metadata
- debug metadata
- target metadata

Conceptually:

```text
Machine Code
     ⇅
Object Mirror
     ⇅
Object File
```

The writer reflects the compiler's internal machine representation into a target object format.

---

# 51. Object Formats

Skyz may emit:

```text
COFF
ELF
Mach-O
```

depending on the target platform.

Examples:

```text
Windows
   ↓
COFF .obj
```

```text
Linux
   ↓
ELF .o
```

```text
macOS
   ↓
Mach-O .o
```

---

# 52. Linkers

Skyz initially relies on mature system linkers.

Supported linking paths may include:

```text
MSVC link.exe
lld-link
LLD
GNU ld
```

The linker is external to the main Skyz compiler architecture.

Skyz remains a custom compiler despite using an external final linker.

---

# 53. C-Style Concurrency

Skyz supports low-level concurrency primitives.

The language may expose:

```text
threads
atomics
mutexes
semaphores
barriers
memory ordering
thread-local storage
shared memory
```

These may initially be implemented through the standard library or platform libraries.

---

# 54. Sequence-Based Concurrency

Skyz additionally supports sequence-based concurrency.

Sequence-based concurrency represents work that is scheduled or registered but does not become executable until explicit conditions are satisfied.

The model is:

```text
scheduled
    ↓
waiting
    ↓
condition satisfied
    ↓
ready
    ↓
triggered
    ↓
executing
```

---

# 55. Sequence Syntax

Example:

```skyz
sequence pipeline
     event load_data
          when source.ready

     event process_data
          when load_data accepted

     event save_result
          when process_data accepted
```

These events exist as part of a sequence graph.

They become executable only when their conditions become true.

---

# 56. Parallel Conditional Events

A sequence may contain multiple waiting events.

Example:

```skyz
sequence workers
     event task_a
          when condition_a

     event task_b
          when condition_b

     event task_c
          when condition_c
```

Conceptually:

```text
             ┌── task_a ← condition_a
SEQUENCE ────┼── task_b ← condition_b
             └── task_c ← condition_c
```

Whichever condition becomes satisfied may become eligible for execution.

This is distinct from strictly sequential function calling.

---

# 57. Sequence Dependencies

Events may depend on:

- values
- time
- external signals
- accept states
- reject states
- other event completion
- atomic conditions
- resource availability
- programmer-defined predicates

Example:

```skyz
event process
     when load accepted
```

The dependency becomes part of the program graph.

---

# 58. Sequence Runtime Strategy

Skyz provides semantic and syntactic support for sequence concurrency directly in the language.

However, the initial implementation may lower sequence operations into a runtime or standard concurrency library.

Example conceptual lowering:

```text
sky_sequence_create(...)
sky_event_add(...)
sky_event_condition(...)
sky_sequence_execute(...)
```

This keeps the compiler implementation manageable without sacrificing language-level semantics.

Later compilers may replace library functionality with direct scheduler integration.

---

# 59. Three Execution Models

Skyz therefore supports three major execution styles.

## Direct Execution

```text
task
 ↓
result
```

## Delegated Graph Execution

```text
node
 ↓
node
 ↓
node
```

## Sequence Execution

```text
scheduled event
      ↓
waiting condition
      ↓
trigger
      ↓
execution
```

These models can coexist inside the same program.

---

# 60. Standard Example

```skyz
task divide(int a, int b) -> result<int c, DivideError>
     if b == 0
          reject DivideError.Zero

     accept a / b
```

---

# 61. Range Example

```skyz
task print_range() -> int
     for x in 0...100
          display(x)

     return 0
```

---

# 62. Count Range Example

```skyz
task print_count() -> int
     for x in range(25)
          display(x)

     return 0
```

---

# 63. Fallback Example

```skyz
task evaluate(int x, int y) -> result<int value, Error>
     when conditions exceeded, resort to method ->
          in case x = y, do nothing
          when case x > y, perform z
          unless z < x, in which case perform w
          in case of w < x, perform speculate
          in case speculation fails, perform undefined
          in case undefined fails, delete task

     accept x
```

---

# 64. Combined Example

```skyz
task process(int x, float y) -> result<int value, ProcessError>
     if x == 0
          reject ProcessError.Invalid

     for i in range(25)
          display(i)

     while x < 25
          display(x)
          x += 1

     when conditions exceeded, resort to fallback ->
          in case x = y, do nothing
          when case x > y, perform recovery
          unless recovery succeeded, in which case perform alternate
          in case alternate fails, perform speculate
          in case speculation fails, perform undefined
          in case undefined fails, delete task

     accept x
```

---

# 65. Sequence Example

```skyz
sequence build_pipeline
     event parse
          when source.ready

     event analyze
          when parse accepted

     event optimize
          when analyze accepted

     event generate
          when optimize accepted

     event emit
          when generate accepted
```

The compiler understands these dependencies as graph edges.

A runtime implementation may handle waiting, signaling, threading, and waking.

---

# 66. Optimization Example

Conceptually:

```skyz
task calculate(int a, int b) -> int
     int c = a + b

     fold constants
     collapse temporary
     merge repeated

     bind c -> rax

     return c
```

Final optimizer syntax may evolve, but Skyz's architecture explicitly reserves language-level forms for manual optimization.

---

# 67. Compiler Responsibility

The compiler is responsible for:

- parsing
- type validation
- graph validation
- semantic resolution
- generic specialization
- lattice construction
- SSA construction
- compile execution
- constant folding
- graph collapsing
- graph merging
- optimization validation
- register conflict checking
- virtual instruction generation
- target lowering
- object generation

The programmer is allowed to direct these processes without bypassing compiler validation by default.

---

# 68. Programmer Responsibility

The programmer controls:

- explicit memory
- pointer use
- low-level concurrency
- optimization hints and commands
- manual register binding
- fallback relationships
- sequence conditions
- speculation
- deliberate undefined states
- explicit task deletion
- graph delegation

Skyz intentionally gives expert programmers substantial authority.

---

# 69. Design Philosophy

Skyz does not ask:

> How clever can the compiler become while hiding everything from the programmer?

Skyz asks:

> What does the programmer already know that the compiler should be allowed to use?

The compiler then verifies, transforms, and lowers that knowledge.

Skyz favors:

```text
explicitness over opacity
knowledge over guessing
graphs over reconstructed relationships
machine reality over abstract illusion
compile execution over unnecessary runtime work
verified control over hidden optimizer heuristics
```

---

# 70. Central Optimization Vocabulary

Skyz uses three especially important transformation concepts:

```text
FOLD
COLLAPSE
MERGE
```

### Fold

Resolve known values.

```text
5 + 5
↓
10
```

### Collapse

Remove unnecessary graph structure.

```text
A → temporary → identity → B
↓
A → B
```

### Merge

Combine equivalent computation.

```text
load X
load X
↓
one load X
```

These concepts are intentionally simple enough for programmers to reason about directly.

---

# 71. What Makes Skyz Distinct

Skyz is not merely C with new keywords.

Its identity comes from the combination of:

1. explicit programmer-driven optimization
2. graph-oriented language semantics
3. custom IR
4. custom SSA
5. machine-intuitive semantic lattice
6. explicit register allocation
7. virtual code generation
8. reflective object writing
9. accept/reject tagged execution
10. delegation-oriented computation
11. aggressive compile execution
12. sequence-based condition-triggered concurrency
13. C-style native memory and machine semantics

---

# 72. Foundational Architecture Summary

```text
                    SKYZ
                      │
       ┌──────────────┼──────────────┐
       │              │              │
    MACHINE         GRAPH        PROGRAMMER
    CONTROL       EXECUTION       CONTROL
       │              │              │
       └──────────────┼──────────────┘
                      │
               SEMANTIC LATTICE
                      │
                  CUSTOM IR
                      │
                  CUSTOM SSA
                      │
            COMPILE EXECUTION
                      │
         FOLD / COLLAPSE / MERGE
                      │
              REGISTER CONTROL
                      │
            VIRTUAL CODEGEN
                      │
               OBJECT MIRROR
                      │
                   LINKER
                      │
              NATIVE PROGRAM
```

---

# 73. Skyz in One Sentence

**Skyz is a native graph-oriented systems programming language where the programmer explicitly collaborates with the compiler to control optimization, execution paths, registers, memory, concurrency, specialization, and lowering while a custom semantic lattice, SSA engine, IR, virtual code generator, and reflective object writer transform the remaining dynamic program into native machine code.**

---

# 74. Core Motto

> **Skyz — Know it. Shape it. Lower it. Run only what remains.**
