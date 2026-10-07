SKYZ — ".Skyz"

Fully Mature, Hardened, Industry-Grade Language Specification

Status: Finalized production standard
Class: Native systems and performance programming language
Compilation: Ahead-of-time native compilation
Execution model: Direct, delegated-graph, and condition-sequenced execution
Primary philosophy: Explicit programmer knowledge + verified compiler machinery
Indentation: Exactly 5 spaces per structural level

---

1. Definition

Skyz is a statically typed, ahead-of-time compiled native systems programming language engineered around explicit programmer participation in optimization, machine placement, graph construction, memory behavior, control flow, concurrency, and final lowering.

Skyz combines the direct machine semantics of C with a modern graph-oriented compiler architecture in which the programmer is not separated from optimization.

The programmer states what is known.

The compiler proves what is valid.

The optimizer eliminates what no longer needs to exist.

The backend emits only the runtime work that remains.

Skyz is established around four fundamental principles:

«Know the work. Shape the graph. Control the machine. Run only what remains.»

and:

«The programmer understands the problem. The compiler understands the machine. Skyz gives authority to both.»

and:

«Known computation belongs to compilation, not runtime.»

and:

«Explicit knowledge outranks speculative compiler guesswork.»

Skyz is used where execution cost, layout, latency, control, predictability, concurrency, and native performance matter.

It is equally comfortable expressing ordinary imperative programs, hard systems code, graph-oriented processing, condition-driven pipelines, specialized numerical kernels, runtime infrastructure, and machine-sensitive algorithms.

---

2. Core Characteristics

Skyz provides:

- native ahead-of-time compilation
- C-style semantics
- C-style memory
- C-style pointers
- C-style structures and unions
- C-style control flow
- C-style concurrency primitives
- deterministic 5-space indentation
- "task" as the callable-unit abstraction
- expressions and statements
- generic specialization
- explicit ranges
- ordered case semantics
- accept/reject tagged results
- delegation-oriented execution
- condition-triggered sequences
- explicit optimization directives
- manual register allocation
- automatic register allocation
- compile execution
- constant folding
- graph collapsing
- graph merging
- custom IR
- custom SSA
- machine-intuitive semantic lattice
- virtual code generation
- reflective object generation
- direct COFF, ELF, and Mach-O emission
- LD, LLD, and MSVC linker integration
- hardened arithmetic semantics
- explicit speculation
- explicit undefined-state representation
- task deletion
- zero mandatory garbage collection
- zero mandatory virtual machine
- zero dependency on LLVM

Skyz is a complete native toolchain architecture rather than a frontend attached to another compiler framework.

---

3. Canonical Compilation Pipeline

The standardized Skyz pipeline is:

.Skyz Source
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
Skyz IR
     ↓
Skyz SSA
     ↓
Compile Execution
     ↓
Constant Folding
     ↓
Graph Collapsing
     ↓
Graph Merging
     ↓
Specialization
     ↓
Programmer-Directed Optimization
     ↓
Compiler Optimization
     ↓
Register Allocation
     ↓
Virtual Code Generator
     ↓
Target Legalization
     ↓
Physical Instruction Selection
     ↓
Mirror / Reflective Object Writer
     ↓
COFF / ELF / Mach-O
     ↓
LLD / LD / MSVC Linker
     ↓
Native Executable

Every stage has a precisely defined responsibility.

There is no hidden dependence on LLVM IR, LLVM optimization passes, LLVM instruction selection, or LLVM object generation.

Skyz owns its program representation from source through object emission.

---

4. Source Files

The canonical extension is:

.Skyz

Skyz source is Unicode-aware for textual material while its structural language vocabulary remains deliberately compact and deterministic.

Source structure is indentation-driven.

Exactly:

5 spaces = 1 indentation level

Example:

task main() -> int
     int x = 10

     if x > 5
          display(x)

     return 0

Canonical Skyz source uses spaces.

Tabs are rejected by strict mode and deterministically normalized by compatibility tooling.

This eliminates indentation ambiguity across editors, operating systems, repositories, formatters, and build machines.

---

5. Tasks

Skyz uses:

task

as its universal callable-work abstraction.

A task replaces the conventional language concept of a function while covering a broader execution domain.

A task represents:

- a native function
- a procedure
- a computation
- a graph node
- a pipeline stage
- a concurrent worker
- a sequence action
- a compile-time computation
- a fallback mechanism
- a specialized machine operation

Example:

task add(int a, int b) -> int
     return a + b

Tasks compile to ordinary native callable units where ordinary function behavior is appropriate.

No heavyweight task runtime is imposed on ordinary task calls.

---

6. Primitive Declaration Mask

Skyz uses a consistent C-style declaration mask:

type identifier

Examples:

int count
float velocity
double position
char symbol
bool ready
uint64 address

Parameters use the same form:

task calculate(int x, float y) -> double

Skyz deliberately avoids:

identifier: type

for ordinary declarations.

The declaration always reads from machine classification toward named value:

int count

meaning:

integer storage/value named count

---

7. Primitive Types

Skyz defines the following standard primitive family:

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

isize
usize

float
double

void

Fixed-width types have fixed widths on every conforming implementation.

"isize" and "usize" match the target address width.

"int" and "uint" use the canonical native integer width of the active Skyz ABI profile.

All primitive representation, alignment, signedness, arithmetic, conversion, and ABI behavior is formally defined.

---

8. Expressions

Skyz expressions produce values.

Examples:

x + y
a * b
buffer[index]
ptr->member
calculate(a, b)
x > y
value == expected
0...100

Expression classes include:

- arithmetic
- comparison
- logical
- bitwise
- pointer
- indexing
- member access
- calls
- generic specialization
- ranges
- result construction
- compile-time expressions
- graph-compatible expressions

Expressions participate directly in semantic-lattice analysis.

---

9. Statements

Statements perform actions.

Examples:

int x = 20

x += 1

return x

accept x

reject Error.Invalid

perform fallback

delete task

Statements form ordered graph nodes after semantic construction.

The source remains readable imperative code while the compiler gains graph-level knowledge immediately after parsing.

---

10. C-Style Machine Semantics

Skyz preserves the successful native machine model established by C while formally tightening its semantics.

Programs operate directly in terms of:

- values
- storage
- addresses
- pointers
- arrays
- structures
- unions
- integer operations
- floating-point operations
- explicit mutation
- native calls
- contiguous memory
- alignment
- atomic access
- machine representation
- direct control flow

Skyz does not hide the physical machine behind mandatory managed abstractions.

When a programmer asks where a value lives, how wide it is, how it is aligned, whether it aliases another object, or which register receives it, Skyz provides a definite answer.

---

11. Memory

Skyz uses explicit memory semantics.

Pointers are native first-class values.

int* ptr
byte* buffer

Arrays are contiguous:

int values[64]
byte memory[4096]

Dynamic memory uses standard native allocation facilities:

byte* data = alloc<byte>(4096)

free(data)

The language supports:

- automatic storage
- static storage
- dynamic storage
- pointers
- pointer arithmetic
- address acquisition
- alignment
- explicit release
- volatile memory
- atomic memory
- alias analysis
- provenance tracking
- contiguous layouts
- custom allocators
- memory-mapped regions
- foreign memory

Garbage collection is never mandatory.

---

12. Structures

Structures use deterministic native layouts.

struct Vector
     float x
     float y
     float z

Usage:

Vector position
position.x = 12.0

Layout behavior is controlled through the active ABI and explicit layout modifiers.

Field order is preserved unless an explicitly requested layout transformation states otherwise.

---

13. Unions

Skyz provides native untagged unions:

union Value
     int i
     float f
     byte b

It also provides compiler-supported tagged unions through result and variant constructs.

The language distinguishes unsafe reinterpretation from verified tagged access.

---

14. Generics

Generics are compile-time native specialization mechanisms.

task max<T>(T a, T b) -> T
     if a > b
          return a

     return b

Instantiations such as:

max<int>
max<uint64>
max<double>

produce specialized semantic and IR graphs.

Skyz does not require type-erased generic dispatch for ordinary generic programming.

Specialization feeds directly into:

- lattice resolution
- constant propagation
- folding
- collapsing
- merging
- instruction selection
- register allocation

Unused generic machinery vanishes before object emission.

---

15. Ranges

Skyz has a native inclusive range operator:

...

These are equivalent:

0...100

0 ... 100

Both mean:

0 through 100 inclusive

Example:

for x in 0...100
     display(x)

This iterates through all 101 values.

Ranges are first-class semantic values:

range<int> values = 0...100

---

16. Count Ranges

The constructor:

range(25)

represents exactly 25 sequence positions:

0...24

This is intentionally distinct from:

0...25

which contains 26 values.

The distinction completely removes the traditional ambiguity between an interval and a requested iteration count.

---

17. Stepped and Descending Ranges

Skyz ranges support explicit steps:

0...100 step 5

and descending traversal:

100...0 step -1

Range bounds and stepping participate in compile-time lattice analysis.

A statically resolvable range is fully known to the optimizer before runtime.

---

18. Standard Control Flow

Skyz includes conventional native control flow.

Conditional

if x > y
     display(x)
else
     display(y)

While

while x < 25
     display(x)
     x += 1

For

for x in range(25)
     display(x)

or:

for x in 0...100
     display(x)

Control structures lower directly into graph regions and SSA edges.

---

19. Assignment and Equality

Ordinary assignment is:

x = y

Ordinary equality comparison is:

x == y

Case grammar additionally defines contextual matching:

in case x = y, do nothing

Inside a case clause, "=" is a match relation because QRTG has already classified the construct.

There is no parser ambiguity.

---

20. Case Semantics

Skyz's case system is a full ordered decision and fallback mechanism.

It is broader than a C "switch".

Example:

when conditions exceeded, resort to method ->
     in case x = y, do nothing
     when case x > y, perform z
     unless z < x, in which case perform w
     in case of w < x, perform speculate
     in case speculation fails, perform undefined
     in case undefined fails, delete task

This produces an ordered conditional graph.

primary path
     ↓
threshold reached
     ↓
resort to method
     ↓
x = y?
 ├─ yes → do nothing
 └─ no
      ↓
x > y?
 ├─ yes → perform z
 └─ no
      ↓
unless condition
      ↓
perform w
      ↓
speculate
      ↓ failure
undefined
      ↓ failure
delete task

Cases are deterministic, ordered, and explicitly represented in Skyz IR.

---

21. "in case"

"in case" establishes a conditional match branch:

in case x = y, do nothing

The branch activates only when its match condition succeeds.

---

22. "when case"

"when case" performs an explicitly timed decision inside an active fallback path.

when case x > y, perform z

It communicates both condition and execution ordering.

---

23. "unless"

"unless" expresses negative conditional execution.

unless z < x, in which case perform w

Its canonical logical meaning is:

if not(z < x)
     perform w

QRTG determines its structural scope before semantic lowering.

---

24. "perform"

"perform" explicitly transfers execution into a named operation, task, node, method, sequence action, or fallback mechanism.

perform recovery

A normal task target lowers to a call.

A graph target lowers to delegation.

A sequence target lowers to sequence activation.

The programmer expresses intent while the compiler selects the correct native mechanism.

---

25. "resort to"

"resort to" is Skyz's explicit fallback transfer.

when conditions exceeded, resort to recovery ->

It identifies a deliberate alternate execution graph rather than relying on hidden exception machinery.

Fallback flow remains visible, analyzable, optimizable, and testable.

---

26. "do nothing"

"do nothing" is an explicit semantic no-op.

in case x = y, do nothing

It creates a valid graph endpoint without requiring synthetic work.

Where no structural reason exists to retain it, graph collapsing removes it completely.

NOP
 ↓
collapse
 ↓
∅

---

27. Speculation

Skyz supports programmer-requested speculation.

perform speculate

Speculation is explicitly represented instead of silently introduced as unverifiable compiler guesswork.

The optimizer records:

- speculative assumptions
- dependent nodes
- validation points
- rollback/failure edges
- acceptance state

A speculative path either validates or follows its declared failure path.

---

28. Undefined State

Skyz has a formal explicit "undefined" semantic state.

perform undefined

This does not mean arbitrary compiler behavior.

Skyz distinguishes:

known
unknown
undefined
rejected
contradictory

within the semantic lattice.

An explicit undefined value or branch is therefore representable, inspectable, analyzable, and deliberately handled.

Accidental undefined compiler behavior is never treated as a language feature.

---

29. "delete task"

Skyz defines:

delete task

as explicit termination of the current task's participation.

At runtime it terminates the active task according to the task's execution contract.

During compile execution it removes the task node and any graph region proven unreachable because of that deletion.

Dead-task elimination integrates directly with graph collapsing.

---

30. Accept / Reject Results

Skyz uses native tagged-result semantics.

Canonical example:

task divide(int a, int b) -> result<int c, DivideError>
     if b == 0
          reject DivideError.Zero

     accept a / b

The declaration:

result<int c, DivideError>

defines:

ACCEPT → int c
REJECT → DivideError

Internally this is a fully optimized tagged union.

Conceptually:

┌────────────────────┐
│ result discriminator│
├────────────────────┤
│ accepted value      │
│        OR           │
│ rejection value     │
└────────────────────┘

The compiler removes unnecessary tags whenever control-flow proof establishes the active variant.

Accept/reject semantics are therefore zero-overhead whenever the graph proves that the tag is unnecessary.

---

31. Result Graphs

Accept and reject are not bolted-on error syntax.

They are graph edges.

             divide
                │
        ┌───────┴────────┐
        │                │
      ACCEPT           REJECT
        │                │
      int c        DivideError

This makes failure flow visible to:

- SSA
- optimizer
- scheduler
- sequence engine
- dead-code elimination
- specialization
- diagnostic analysis

Skyz therefore handles recoverable outcomes without invisible stack-unwinding machinery.

---

32. Delegation

Delegation is a fundamental Skyz execution relationship.

Conventional nested calls:

A → B → C → D

can instead be represented as explicit graph relationships:

        validate
       /        \
   inspect      decode
       \        /
        normalize
            |
          output

Delegation allows tasks and nodes to participate naturally in pipelines, conditional routing, specialization, and concurrency.

---

33. Diagrammatic Graph AST

Skyz's core AST representation is a diagrammatic semantic graph.

It retains syntax relationships while explicitly recording:

- value flow
- control flow
- data dependency
- ordering
- task boundaries
- delegation
- branching
- merging
- accept/reject edges
- sequence triggers
- concurrency relationships
- lifetime regions

Example:

       input
       /   \
      A     B
       \   /
       merge
         |
      compare
      /     \
 accept     reject

The compiler therefore never needs to rediscover basic execution topology from a deeply nested conventional tree.

The topology is present from the beginning.

---

34. QRTG

Quick Reference Table Grammar

QRTG is Skyz's authoritative grammar reference.

It defines constructs in compact tabular form and is consumed by both tooling and compiler infrastructure.

Example:

Construct| Definer Pattern| Quantity| Result
Task| "task identifier"| 1| TaskNode
Parameter| "type identifier"| 0..N| Parameter
Result| "result<...>"| 0..1| ResultNode
Body| indentation +5| 1..N| Region
Generic| "<definition>"| 0..N| GenericSet
Range| "expression ... expression"| 0..1| RangeNode
Accept| "accept expression"| 0..1| AcceptEdge
Reject| "reject expression"| 0..1| RejectEdge
Case| "in case condition"| 0..N| CaseEdge
Sequence| "sequence identifier"| 0..N| SequenceGraph
Event| "event identifier"| 0..N| EventNode

QRTG serves simultaneously as:

- grammar authority
- quick reference
- parser contract
- tooling metadata
- conformance reference

The grammar specification and parser implementation therefore cannot silently drift apart.

---

35. Bit-Style Tokenizer

Skyz uses a compact bit-classified lexical system.

Conceptually:

00000001 identifier
00000010 keyword
00000100 operator
00001000 literal
00010000 delimiter
00100000 indentation
01000000 type
10000000 graph/control

Token records contain orthogonal classifications instead of requiring bloated object hierarchies.

This provides:

- fast classification
- compact token storage
- predictable branch behavior
- straightforward parser dispatch
- easy tooling reuse

Lexical analysis is deterministic and independent of semantic guesswork.

---

36. Definer

The Definer determines:

«What is this construct?»

Examples:

task       → TaskDeclaration
if         → Conditional
while      → Loop
accept     → AcceptTransition
reject     → RejectTransition
sequence   → SequenceDeclaration
event      → EventDeclaration

The Definer establishes grammatical identity.

---

37. Quantifier

The Quantifier determines:

«How much source belongs to this construct?»

Examples:

parameter      → 0..N
argument       → 0..N
generic        → 0..N
task body      → 1..N
case branch    → 0..N
sequence event → 0..N

The standardized parse model is:

TOKENS
   ↓
QRTG LOOKUP
   ↓
DEFINER
   ↓
QUANTIFIER
   ↓
GRAPH CONSTRUCTION

This architecture produces predictable parser behavior without forcing every language rule through conventional recursive grammar traversal.

---

38. Semantic Resolution

Semantic resolution binds the graph into a complete program model.

It resolves:

- declarations
- identifiers
- overloads
- types
- generic substitutions
- pointer relationships
- memory effects
- ranges
- result contracts
- case matching
- task boundaries
- sequence dependencies
- concurrency relationships
- optimization directives
- ABI requirements

Semantic resolution must complete successfully before native lowering begins.

---

39. Machine-Intuitive Semantic Lattice

Skyz's semantic lattice records what the compiler has proven about every relevant value, node, and relationship.

Example:

unknown
   ↓
integer
   ↓
int32
   ↓
nonnegative int32
   ↓
0...255
   ↓
constant 17

The lattice records facts including:

- exact type
- type class
- constantness
- numeric range
- signedness
- alignment
- provenance
- alias class
- mutability
- lifetime
- storage class
- register suitability
- pointer validity
- atomicity
- overflow behavior
- compile-time executability
- accept/reject status
- sequence readiness
- concurrency visibility
- memory effects

Optimization operates from proved facts.

The optimizer does not need to repeatedly infer the same information independently across unrelated passes.

---

40. Skyz IR

Skyz lowers into its own typed, graph-oriented intermediate representation.

Skyz IR is:

- strongly typed
- SSA-compatible
- graph-native
- memory-aware
- register-aware
- effect-aware
- sequence-aware
- concurrency-aware
- result-aware
- optimization-directive aware
- target-independent before legalization

Example:

%1 = load.i32 %a
%2 = load.i32 %b
%3 = add.checked.i32 %1, %2
return %3

Result processing:

%3 = div.checked.i32 %a, %b

branch.accept %3 -> block.accept
branch.reject %3 -> block.reject

Manual optimization operations are represented directly:

fold %4
collapse %7
merge %8, %9
bind.reg %12, rax

Skyz IR is designed specifically around Skyz semantics rather than forcing Skyz concepts through another language's IR model.

---

41. Custom SSA Engine

Skyz contains a dedicated Static Single Assignment engine.

SSA follows graph topology.

Example:

        x0
       /  \
     +1    +7
      |     |
     x1    x2
       \   /
       merge
         |
        x3

Internal representation:

x3 = merge(x1, x2)

Merge nodes perform the role normally associated with phi nodes while fitting Skyz's graph vocabulary naturally.

SSA construction, destruction, repair, live-range derivation, and value versioning are native Skyz compiler subsystems.

---

42. The Programmer Is an Optimizer

Skyz's defining professional feature is that the programmer participates explicitly in optimization.

Traditional optimization levels remain available for convenience, but they are not the programmer's only interface to optimization.

Skyz exposes directives including:

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

The programmer supplies knowledge.

The compiler verifies that knowledge.

The optimizer implements the transformation.

PROGRAMMER KNOWLEDGE
        ↓
OPTIMIZATION DIRECTIVE
        ↓
SEMANTIC LATTICE
        ↓
PROOF / VALIDATION
        ↓
IR TRANSFORMATION
        ↓
NATIVE LOWERING

An invalid manual optimization fails compilation instead of silently producing incorrect machine code.

This is the essential Skyz contract:

«Manual control without manual compiler corruption.»

---

43. Constant Folding

All compile-time-known arithmetic and expressions are folded.

int x = 10 * 20 + 5

becomes:

205

before native lowering.

Compile execution extends this beyond isolated arithmetic.

task dimensions() -> int
     return 20 * 40

when invoked entirely from compile-known context reduces directly to:

800

No runtime task remains.

---

44. Graph Collapsing

Collapsing removes graph structure that contributes no independent runtime meaning.

A
↓
temporary
↓
identity
↓
B

becomes:

A
↓
B

Collapsing eliminates:

- identity operations
- dead forwarding nodes
- redundant temporary values
- no-op regions
- proven empty fallback paths
- unnecessary delegation boundaries

---

45. Graph Merging

Merging unifies equivalent work.

load A
load A

becomes:

      load A
      /    \
   use1    use2

Skyz's three central transformation verbs therefore have precise meanings:

FOLD       resolve known values
COLLAPSE   remove unnecessary structure
MERGE      combine equivalent computation

These concepts are visible to both programmer and compiler.

---

46. Compile Execution

Skyz performs computation during compilation whenever all required inputs and effects are compile-resolvable.

The model is:

SOURCE
  ↓
WHAT IS KNOWN?
  ↓
EXECUTE IT
  ↓
WHAT IS CONSTANT?
  ↓
FOLD IT
  ↓
WHAT STRUCTURE IS REDUNDANT?
  ↓
COLLAPSE IT
  ↓
WHAT WORK IS EQUIVALENT?
  ↓
MERGE IT
  ↓
WHAT CAN BE SPECIALIZED?
  ↓
SPECIALIZE IT
  ↓
WHAT ACTUALLY REQUIRES RUNTIME?
  ↓
GENERATE ONLY THAT

This process is one of the primary reasons highly specialized Skyz programs routinely produce extremely compact native execution paths.

---

47. Arithmetic

Skyz arithmetic has formally defined semantics.

The production compiler implements arithmetic through hardened checked primitives and C++23-backed internal arithmetic facilities where appropriate.

The implementation hierarchy is:

Skyz arithmetic contract
        ↓
Skyz checked-operation layer
        ↓
C++23 compiler implementation
        ↓
target machine operation

Host-language undefined behavior never defines Skyz behavior.

---

48. Arithmetic Modes

Skyz supports explicit arithmetic modes:

checked
wrapping
saturating
exact
unchecked

Example:

checked int c = a + b

The selected arithmetic mode becomes part of the lattice and IR operation.

This allows arithmetic policy to survive optimization without ambiguity.

---

49. Register Allocation

Skyz provides both automatic and explicit register allocation.

Automatic allocation is production-grade and requires no manual intervention for ordinary code.

Experts may bind critical values directly:

bind accumulator -> rax
bind source -> rcx
bind count -> rdx

The compiler validates:

- register availability
- register width
- ABI reservations
- live-range conflicts
- calling-convention restrictions
- clobbers
- implicit operands
- instruction constraints
- save/restore requirements

Manual allocation therefore remains machine-exact without bypassing compiler correctness.

---

50. Register Modes

Skyz recognizes:

register auto
register explicit

Automatic mode uses the hardened allocator.

Explicit mode honors programmer bindings while allocating all unbound values around them.

Hybrid allocation is standard practice in high-performance Skyz code.

---

51. Virtual Code Generator

Skyz uses a target-independent virtual code generator.

The virtual layer contains normalized machine operations such as:

VLOAD
VSTORE
VMOVE
VADD
VSUB
VMUL
VDIV
VCMP
VBRANCH
VCALL
VRETURN
VATOMIC
VBARRIER

Pipeline:

Skyz IR
   ↓
Virtual Operations
   ↓
Target Legalization
   ↓
Instruction Selection
   ↓
Scheduling
   ↓
Physical Machine Code

These virtual operations are compiler constructs.

Skyz applications do not require a bytecode virtual machine.

---

52. Native Backends

The standardized backends include:

x86-64
AArch64
RISC-V

Each backend provides:

- instruction selection
- register-class modeling
- calling conventions
- ABI implementation
- stack-frame construction
- branch relaxation
- relocation generation
- target scheduling
- atomic lowering
- platform unwind support

Target behavior is validated against the same Skyz semantic contract.

---

53. Mirror / Reflective Object Writer

Skyz's object writer maintains a complete mirrored representation of the emitted native program.

The object mirror records:

- executable sections
- data sections
- constants
- symbols
- relocations
- imports
- exports
- alignments
- task boundaries
- function metadata
- unwind information
- debug information
- ABI metadata
- linkage visibility

Architecture:

FINAL MACHINE GRAPH
        ⇅
OBJECT MIRROR
        ⇅
SERIALIZED OBJECT

Object generation is therefore a structured reflection of the compiler's final program state rather than an ad-hoc byte dump.

---

54. Object Formats

Skyz natively emits:

COFF
ELF
Mach-O

Standard platform mappings are:

Windows → COFF
Linux   → ELF
macOS   → Mach-O

The object writer produces files accepted directly by conventional system linkers.

---

55. Linking

Skyz integrates with established native linkers:

MSVC link.exe
lld-link
LLD
GNU ld

The linker remains deliberately outside the language's semantic core.

This division gives Skyz full ownership of compilation while retaining compatibility with mature operating-system toolchains.

---

56. C-Style Concurrency

Skyz provides direct low-level concurrency:

- operating-system threads
- atomic values
- mutexes
- semaphores
- barriers
- shared memory
- thread-local storage
- acquire/release ordering
- relaxed ordering
- sequential consistency
- native wait/wake integration

Concurrency is not hidden behind a mandatory managed scheduler.

Programmers can work directly at the machine and operating-system level.

---

57. Sequence-Based Concurrency

Skyz additionally defines sequence-based concurrency.

A sequence contains work that is registered in advance but does not become runnable until explicit semantic conditions are satisfied.

The state model is:

REGISTERED
    ↓
WAITING
    ↓
CONDITION SATISFIED
    ↓
READY
    ↓
TRIGGERED
    ↓
RUNNING
    ↓
ACCEPT / REJECT / COMPLETE

This provides deterministic condition-oriented scheduling without forcing programmers to manually build callback chains.

---

58. Sequence Syntax

sequence pipeline
     event load_data
          when source.ready

     event process_data
          when load_data accepted

     event save_result
          when process_data accepted

Dependencies are compiler-visible.

The sequence engine therefore knows exactly why an event is blocked and precisely what condition releases it.

---

59. Parallel Sequence Events

Independent events coexist naturally:

sequence workers
     event task_a
          when condition_a

     event task_b
          when condition_b

     event task_c
          when condition_c

Conceptually:

             ┌── task_a ← condition_a
SEQUENCE ────┼── task_b ← condition_b
             └── task_c ← condition_c

Each event becomes runnable independently when its own trigger is satisfied.

---

60. Sequence Dependencies

Sequence triggers support:

- value predicates
- task completion
- accepted results
- rejected results
- atomic transitions
- timers
- external signals
- resource readiness
- event completion
- programmer-defined predicates

Example:

event analyze
     when parse accepted

The dependency is a first-class graph edge, not hidden runtime metadata.

---

61. Sequence Runtime

The Skyz language owns sequence semantics.

The hardened Skyz standard concurrency library supplies the operating-system integration for:

- wait registration
- wakeup
- event queues
- synchronization
- worker management
- timers
- platform wait primitives

The compiler lowers sequence graphs into optimized runtime calls where direct lowering is not superior.

This preserves a compact compiler while maintaining first-class language semantics.

---

62. Execution Models

Skyz formally supports three interoperable execution models.

Direct

task
 ↓
result

Delegated Graph

node
 ↓
node
 ↓
node

Condition-Sequenced

registered event
      ↓
condition
      ↓
trigger
      ↓
execution

A single Skyz program routinely uses all three.

---

63. Standard Result Example

task divide(int a, int b) -> result<int c, DivideError>
     if b == 0
          reject DivideError.Zero

     accept a / b

This example demonstrates:

- C-style parameter masks
- tagged result typing
- explicit rejection
- explicit acceptance
- five-space blocks
- direct native semantics

---

64. Range Example

task print_range() -> int
     for x in 0...100
          display(x)

     return 0

---

65. Count Example

task print_count() -> int
     for x in range(25)
          display(x)

     return 0

---

66. Fallback Example

task evaluate(int x, int y) -> result<int value, Error>
     when conditions exceeded, resort to method ->
          in case x = y, do nothing
          when case x > y, perform z
          unless z < x, in which case perform w
          in case of w < x, perform speculate
          in case speculation fails, perform undefined
          in case undefined fails, delete task

     accept x

The entire fallback chain remains explicit to the optimizer.

---

67. Combined Control Example

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

---

68. Production Sequence Example

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

This source maps directly to a dependency graph.

No callback reconstruction is necessary.

---

69. Manual Optimization Example

task calculate(int a, int b) -> int
     int c = a + b

     fold constants
     collapse temporary
     merge repeated

     bind c -> rax

     return c

The directives are verified against the semantic lattice.

If a requested transformation violates observable semantics, compilation fails with an exact diagnostic.

---

70. Compiler Guarantees

A conforming Skyz compiler guarantees:

- deterministic parsing
- deterministic type resolution
- deterministic graph construction
- explicit arithmetic semantics
- verified manual optimizations
- valid ABI lowering
- valid register allocation
- correct result-tag behavior
- defined sequence dependencies
- correct object relocation generation
- correct native calling convention behavior
- reproducible compile semantics
- diagnostics tied to source and graph state

Compiler transformations cannot silently violate the source semantic contract.

---

71. Programmer Authority

Skyz programmers have direct authority over:

- allocation
- freeing
- pointer use
- alias assumptions
- alignment
- arithmetic modes
- optimization directives
- register placement
- graph delegation
- sequence dependencies
- speculative execution
- fallback mechanisms
- task deletion
- explicit undefined states

Skyz intentionally gives experts substantial machine authority.

That authority is paired with compiler validation wherever the language has enough information to prove correctness.

---

72. Hardened Tooling

The professional Skyz ecosystem includes:

- incremental compiler
- package manager
- build system
- language server
- debugger integration
- graph visualizer
- IR viewer
- SSA inspector
- lattice inspector
- object-file inspector
- register-allocation viewer
- optimization report
- sequence debugger
- deterministic formatter
- QRTG explorer
- profiler integration
- sanitizer instrumentation
- static analyzer

The tooling exposes the same compiler truths that drive native lowering.

There is no separate simplified mental model for tooling.

---

73. Diagnostics

Skyz diagnostics report both source-level and compiler-level reasoning.

A register conflict reports:

- bound value
- physical register
- conflicting live range
- ABI requirement
- relevant graph edge

A failed optimization reports:

- requested transformation
- violated semantic fact
- lattice state
- source location
- affected nodes

A sequence deadlock report identifies:

- blocked events
- unmet conditions
- dependency cycle
- originating declarations

This transparency is a major reason Skyz remains manageable despite exposing unusually deep control.

---

74. Performance Philosophy

Skyz does not depend on heroic backend guessing.

Performance comes from combining:

programmer knowledge
        +
semantic proof
        +
graph visibility
        +
compile execution
        +
native lowering

The compiler aggressively removes work while preserving exact semantics.

The programmer can intervene precisely where domain knowledge exceeds what static analysis can infer.

---

75. Safety Philosophy

Skyz is neither a managed safety language nor an uncontrolled low-level language.

It uses verified explicitness.

Dangerous operations remain available because systems programming requires them.

But their effects remain visible to:

- type analysis
- provenance analysis
- lifetime analysis
- arithmetic analysis
- concurrency analysis
- graph validation
- diagnostics

Unchecked behavior must be explicitly requested.

Accidental ambiguity is rejected.

---

76. Efficiency

Skyz is designed so abstractions disappear.

Generic specialization disappears into concrete code.

Accepted/rejected branches lose unnecessary tags.

Known tasks execute at compile time.

Dead graph nodes collapse.

Equivalent computation merges.

Constants fold.

Explicit register bindings avoid unnecessary movement.

Sequence machinery disappears when dependencies resolve statically.

The compiled executable therefore contains the dynamic residue of the source program rather than a literal runtime reenactment of every abstraction used to describe it.

---

77. Appropriate Domains

Skyz is particularly suited to:

- operating systems
- kernels
- device infrastructure
- drivers
- runtimes
- compilers
- databases
- game engines
- simulation
- graphics
- numerical computation
- scientific computing
- embedded systems
- networking
- low-latency servers
- financial engines
- DSP
- signal processing
- compression
- codecs
- virtual machines
- native tooling
- high-performance pipelines
- real-time systems
- deterministic services
- specialized compute kernels

It is equally effective for ordinary native utilities where programmers want predictable machine behavior without surrendering control to a large runtime.

---

78. What Skyz Solves

Skyz directly addresses a long-standing divide in native programming.

Traditional low-level languages expose the machine but leave sophisticated optimization almost entirely to the compiler.

Higher-level languages improve expression but increasingly hide machine decisions.

Skyz rejects that tradeoff.

It provides:

high semantic visibility
+
low-level machine authority
+
compiler verification
+
graph-level optimization

The result is a language in which expert knowledge is not discarded merely because the optimizer cannot independently infer it.

---

79. Central Optimization Vocabulary

Skyz's three foundational transformation terms remain:

FOLD

Resolve known computation.

5 + 5
↓
10

COLLAPSE

Remove structurally unnecessary computation.

A → temporary → identity → B
↓
A → B

MERGE

Unify equivalent computation.

load X
load X
↓
load X
  ↙ ↘
 A   B

These terms are part of both documentation and compiler diagnostics.

---

80. Industry Character

Skyz is valued because it does not infantilize systems programmers and does not abandon them either.

It gives programmers control over the machine while preserving industrial compiler guarantees.

It makes optimizer behavior inspectable.

It makes graph structure visible.

It makes failure flow explicit.

It makes concurrency dependencies explicit.

It makes register control available.

It makes memory real.

And it makes unnecessary runtime work expendable.

This balance is the defining character of Skyz.

---

81. Architectural Summary

                          SKYZ
                            │
       ┌────────────────────┼────────────────────┐
       │                    │                    │
   PROGRAMMER            SEMANTICS            MACHINE
    KNOWLEDGE              GRAPH               REALITY
       │                    │                    │
       └────────────────────┼────────────────────┘
                            │
                     QRTG + PARSER
                            │
                  DIAGRAMMATIC GRAPH AST
                            │
                     SEMANTIC LATTICE
                            │
                        SKYZ IR
                            │
                       SKYZ SSA
                            │
                   COMPILE EXECUTION
                            │
              FOLD / COLLAPSE / MERGE
                            │
             SPECIALIZE / INLINE / BIND
                            │
                 REGISTER ALLOCATION
                            │
                VIRTUAL CODE GENERATOR
                            │
                    TARGET BACKEND
                            │
                     OBJECT MIRROR
                            │
                       LINKER
                            │
                  NATIVE EXECUTABLE

---

82. Final Language Identity

Skyz is a native graph-oriented systems programming language in which the programmer and compiler cooperate directly over optimization, machine placement, memory, execution topology, concurrency, specialization, and native lowering.

Its source syntax remains readable and imperative.

Its semantic representation is graph-driven.

Its optimizer is both automatic and programmer-directable.

Its memory model is physical.

Its concurrency model is both traditional and condition-sequenced.

Its IR and SSA machinery are custom.

Its code generator is independent.

Its object writer is reflective.

Its output is native machine code.

Its abstractions are designed to disappear.

---

83. Canonical One-Sentence Definition

«Skyz is the industrial native programming language that turns explicit programmer knowledge into verified graph transformations, machine placement, compile execution, and highly specialized native code through its own semantic lattice, IR, SSA engine, optimizer, virtual code generator, and reflective object writer.»

---

84. Governing Principle

«Tell Skyz what you know. Skyz proves what is valid. The compiler removes what is unnecessary. The machine receives only what remains.»

---

85. Official Motto

«Skyz — Know it. Shape it. Lower it. Run only what remains.»

## *** ##

How fast is Skyz?	Top-tier native speed. Skyz operates in the same performance territory as highly optimized C/C++ and other serious ahead-of-time systems languages, with an unusual advantage: the programmer can directly expose optimization knowledge the compiler cannot infer. Compile execution, specialization, constant folding, graph collapsing, graph merging, custom SSA, explicit register binding, and virtual-machine-independent native code generation aggressively remove runtime work. Skyz is especially strong where the programmer actually understands the workload.
How safe is it?	Much safer than traditional unrestricted C, but intentionally not a memory-safe managed language. Skyz hardens arithmetic semantics, validates manual optimizations, tracks provenance, aliasing, lifetimes, ranges, result states, register conflicts, graph legality, concurrency relationships, and ABI requirements. Checked arithmetic and explicit accept/reject eliminate many common ambiguity classes. At the same time, raw pointers, manual allocation, explicit freeing, unchecked arithmetic, and machine-level authority remain available. Skyz therefore gives verified low-level control, not mandatory isolation from the machine.
What can be made with it?	Nearly anything that benefits from native compilation: operating systems, kernels, drivers, game engines, databases, compilers, runtimes, networking stacks, rendering engines, simulation systems, scientific software, embedded firmware, command-line tools, servers, DSP systems, codecs, compression engines, financial systems, real-time software, native libraries, virtual machines, language runtimes, automation engines, high-throughput pipelines, and performance-critical application components.
Who is it for?	Programmers who want to understand and control what their program becomes. It is especially suited to systems engineers, compiler engineers, performance specialists, engine developers, embedded programmers, HPC developers, infrastructure engineers, low-latency programmers, and advanced application developers who dislike having important machine decisions hidden from them.
Who adopts it quickly?	Experienced C, C++, Rust, Zig, assembly, compiler, kernel, engine, and embedded developers adapt fastest. They already think in terms of memory, layouts, registers, ABI boundaries, lifetime, costs, and control flow. Skyz adds graph semantics and explicit optimization to concepts they already understand.
Where is it used first?	The first natural footholds are performance-critical native libraries, compiler tooling, game/graphics engines, embedded systems, networking, infrastructure, numerical kernels, custom runtimes, and low-latency services. These are areas where Skyz's extra control immediately pays for itself.
Where is it most appreciated?	Where a five-percent improvement matters, where latency variance matters, where allocations matter, where an unexpected branch matters, where a cache miss matters, or where knowing exactly why the compiler emitted an instruction matters. Skyz earns its keep in places where “the compiler will probably figure it out” is not an acceptable engineering strategy.
Where is it most appropriate?	Codebases whose developers have real domain knowledge that ordinary optimizers cannot automatically discover. Examples include packet processing, codecs, specialized math, real-time simulation, rendering kernels, VM internals, storage engines, custom schedulers, deterministic pipelines, and hardware-adjacent code.
Who gravitates toward it?	Programmers who enjoy control rather than insulation. People who inspect disassembly. People who care about calling conventions. People who profile before guessing. People who think in dataflow graphs. People who have occasionally yelled, “No, compiler, I know this value cannot alias that one.” Skyz is basically catnip for that crowd.
When does Skyz shine?	When computation contains exploitable structure: known ranges, predictable layouts, static configuration, repetitive graph sections, domain-specific invariants, specialized generic instances, conditional pipelines, compile-known data, tight loops, explicit concurrency dependencies, or carefully constrained memory behavior. The more the programmer genuinely knows, the more Skyz can turn that knowledge into less runtime work.
What is its strong suit?	Turning programmer knowledge into native optimization without surrendering correctness checking. Its signature combination is graph semantics + semantic lattice + custom SSA + explicit optimization + machine control. Many languages give you abstraction or control. Skyz is built around retaining both and then erasing the abstraction before runtime.
What is it suited for?	Long-lived native software where performance, inspectability, determinism, portability, and explicit resource management outweigh the convenience of a managed runtime. It is particularly well suited to software that needs to remain understandable at both the source level and machine-code level.
What is its philosophy?	Do not hide useful truth from either side. The programmer exposes real knowledge; the compiler exposes real constraints. The semantic lattice establishes what is known. The graph establishes what depends on what. Optimization eliminates what does not need to survive. Runtime receives only the unresolved remainder.
Why choose Skyz?	Choose it when C gives too little verification, C++ gives too much accidental complexity, managed languages hide too much machinery, and conventional optimizing compilers give the programmer too little direct influence over lowering. Skyz is strongest when you want machine authority without turning the compiler into a passive assembler.
What is the learning curve?	Moderate for ordinary Skyz, steep for mastery. A C-family programmer can become productive quickly with tasks, expressions, statements, pointers, structures, ranges, loops, and results. The deeper concepts—semantic lattices, graph-oriented execution, explicit optimization, SSA consequences, register allocation, sequence concurrency, object layout, and target behavior—take substantially longer. The important point is that beginners do not need to manually allocate registers on day one. Skyz scales upward with expertise.
How is it used most successfully?	Write clear ordinary Skyz first. Profile. Use the semantic and graph tools to see where runtime work remains. Then apply specialization, folding, collapsing, merging, alignment, assumptions, explicit register bindings, or sequence restructuring only where evidence justifies them. Skyz rewards deliberate optimization much more than obsessive micro-management everywhere.
How efficient is it?	Extremely efficient in both runtime representation and abstraction removal. Generics specialize, static graph sections collapse, duplicate work merges, known expressions fold, known tasks execute during compilation, unnecessary result tags disappear, dead branches disappear, and explicit machine placement can remove avoidable data movement. Skyz's ideal executable is not a literal translation of the source—it is the minimum dynamic residue left after everything knowable has been resolved.
What are its purposes and edge cases?	Beyond conventional systems programming, Skyz is excellent for generated code, static pipelines, partially evaluated applications, hardware-control layers, language runtimes, deterministic simulations, custom allocators, high-frequency data processing, network packet classification, binary transformation, protocol engines, highly specialized command processors, compile-time table generation, embedded schedulers, and unusual workloads where execution resembles a graph more than a conventional call stack.
What problems does it address directly and indirectly?	Directly, it attacks unnecessary runtime work, optimizer opacity, weak programmer influence over lowering, hidden failure flow, awkward condition-triggered concurrency, and the divide between high-level semantics and native representation. Indirectly, it improves performance debugging, architectural transparency, reproducibility, profiling quality, static reasoning, specialized deployment, interoperability, and the ability to maintain performance-sensitive software without falling into hand-written assembly everywhere.
What are the best habits?	Treat explicit control as a precision tool. Keep ordinary code ordinary. Use accept/reject instead of ad-hoc status conventions. Prefer proven lattice facts over assumptions. Profile before manual register binding. Keep unsafe memory operations narrow. Make ownership conventions obvious even where they are not enforced by the type system. Use checked arithmetic unless wraparound is intentional. Let graph collapsing remove structure instead of manually contorting source code. Document every assume, unchecked region, manual register binding, and speculative path.
How exploitable is it?	In hardened use, substantially less exploitable than classic laissez-faire C, because many dangerous assumptions are visible to the compiler and tooling. But Skyz deliberately allows raw memory access and explicit unsafe authority, so it cannot truthfully promise Rust-style memory safety for unrestricted programs. Buffer errors, use-after-free, races, invalid pointer arithmetic, bad FFI contracts, and logic errors remain possible when the programmer deliberately or accidentally violates the machine contract. Hardened profiles, sanitizers, provenance analysis, checked arithmetic, concurrency analysis, and narrow unsafe boundaries reduce that attack surface dramatically.


The performance character

Skyz's speed does not primarily come from a magic optimizer that mysteriously beats every other compiler.

Its real advantage is more interesting.

A conventional compiler sees:

source
  ↓
infer everything possible
  ↓
optimize
  ↓
emit

Skyz sees:

source
  ↓
programmer knowledge
  +
compiler knowledge
  ↓
semantic proof
  ↓
compile execution
  ↓
fold
collapse
merge
specialize
  ↓
emit unresolved work

That means an expert programmer can communicate facts that would ordinarily remain trapped in their head.

If a value has a known range, Skyz can know it.

If two memory regions cannot alias, Skyz can know it.

If a generic instance has only one meaningful configuration, Skyz can specialize it.

If a graph node contributes nothing, Skyz can collapse it.

If two calculations are equivalent, Skyz can merge them.

If a value belongs in a particular physical register for a critical sequence, the programmer can bind it.

And importantly, the compiler still checks whether those decisions are legal.

That is where Skyz earns its performance reputation.

The safety character

Skyz's mature philosophy is not:

> “Prevent programmers from touching dangerous things.”



It is:

> “Make dangerous things explicit, analyzable, and difficult to misuse accidentally.”



That distinction matters.

For example, manual register allocation is dangerous in a primitive compiler. In Skyz, register binding runs through live-range, ABI, width, clobber, and instruction-constraint validation.

Speculation is dangerous if hidden. In Skyz, it has an explicit graph state and failure edge.

Undefined state is dangerous when it means “the compiler may do anything.” Skyz instead makes undefined a language-visible semantic state while keeping actual compiler UB outside the language contract.

Likewise, accept/reject is safer than the classic C convention where -1, NULL, errno, a partially initialized structure, or some undocumented magic value might indicate failure.

Skyz does not eliminate responsibility.

It makes responsibility inspectable.

The learning curve in practice

Skyz has three natural competency levels.

A productive programmer learns tasks, values, expressions, loops, ranges, structures, pointers, generics, and accept/reject. At that level, Skyz feels like a disciplined native C-family language.

An advanced programmer learns graph delegation, sequences, specialization, lattice facts, memory effects, arithmetic modes, compile execution, and explicit optimization.

An expert programmer works comfortably with custom SSA behavior, register placement, object layout, ABI interactions, cache behavior, vectorization opportunities, instruction selection consequences, and graph-level transformations.

That progression is one of the language's strongest traits: you do not have to pay the complexity cost of its deepest features until you actually need them.

Where Skyz is less appropriate

Skyz can build ordinary application software, but using it for every possible project would be silly.

For a basic CRUD web service, a throwaway automation script, a small internal form application, or a UI whose bottleneck is waiting on a network API, Skyz's machine control provides relatively little advantage.

It becomes more compelling as any of these rise:

performance sensitivity
determinism
memory pressure
latency requirements
concurrency complexity
binary size concerns
hardware interaction
compile-time knowledge
deployment constraints
need for machine transparency

At the far end of that spectrum, Skyz goes from “nice” to exactly the sort of language you want.

The defining tradeoff

Skyz's bargain with its programmer is unusually straightforward:

It will give you more control than most modern languages.

In return:

it expects you to understand the control you exercise.

But unlike older low-level languages, it does not simply shrug when you make a sophisticated request.

It analyzes that request.

It checks it against the semantic lattice.

It verifies graph legality.

It verifies the target.

It verifies registers and ABI requirements.

Then it either performs the transformation or tells you precisely why it cannot.

That is arguably Skyz's deepest design achievement.

It treats the advanced programmer neither as someone who must be protected from the computer nor as someone who should be abandoned to it.

Skyz treats the programmer as a participant in compilation.
