## General

- (__Item:2__) Follow PEP8
    - use in line negation (`if a is not b`) instead of negation of postive expressions (if not a is b)
    - try to reduce level of `nesting` using `classes`, `generators`, `etc.`
    - imports should be in a section in the following order: `standard library` modules, `third-party` modules, `your` own modules. Each subsection should have imports in alphabetical order
    - in loops use `_` for unused variables
    - try to return function instead of calling function and then returning it
    - try combining exception handling
    - try to make your function generalizable as possible
    - use `long` and descriptive variable names 
    - optimize `if` statements to ensure failure occurs as quickly as possible
- (__Item 5__) Write `Helper Functions` Instead of Complex Expressions
- (__Item 6__): Perfer Multiple Assignment `Unpacking` over Indexing
- (__Item 7__): Perfer `enumerate` over `range`
- (__Item 8__): Use `zip` top process Iterators in Parallel
- (__Item 9__): Avoid `else` Blocks After `for` and `while` Loops
- (__Item 10__): Prevent Repetition with Assignment Expressions / `Walrus Operator`

## Lists and Dictionaries

- (__Item 12:__) Avoid `Striding` and `Slicing` in a Signle Expression
    - If you need all three parameters, consider doing two assignments (one to stride and another to slice) or using `islice` from the `itertools`
- (__Item 13:__) Perfer `Catch-All` Unpacking Over Slicing (`*unpacking`) 
- (__Item: 14__) Sort by `Complex` Criteria Using the `Key` Parameter
    - tuples have built in `__it__` and you can compare them
    - sort(key=lambda x: (x.weight, -x.name)
- (__Item: 16__) Perfer `get` Over `in` and `KeyError` to Handle Missing Dictionary Keys 
- (__Item: 17__) Perfer `defaultdict` Over `setdefault` to Handle Missing Items in Internal State
    - try to use `if (names := votes.get(key)) is None:`
- (__Item: 18__) Know How to Construct Key-Dependent Default Values with `__missing__`

## Functions

- (__Item: 19__) Never Unpack More Than Three Variables from Functions
- (__Item: 20__) Perfer Raising Exceptions to Returning `None`
- (__Item: 22__) Reduce Visual Noise with Variable Positional Arguments (`*args`)
    - not good pratice to use this with generators
- (__Item: 23__) Provide Optional Behavior with Keyword Arguments (`**kwargs`)
- (__Item: 24__) Use `None` and Docstrings to Specify Dynamic Default Arguments
    -  during function definition at module load time. This can cause odd behaviors for dynamic values (like {}, [], or datetime.now())
- (__Item: 25__) Enforce Clarity with Keyword-Only and Positional-Only Arguments
    - `safe_division_d(x, y, /, *, found=False, ignore=False)`
- (__Item: 26__) Define Function Decorators with `functools.wraps`

## Comprehensions and Generators

- (__Item: 27__) Use Comprehensions Instead of `map` and `filter`
- (__Item: 28__) Avoid More Than Two Control Subexpressions in Comprehension
    - meaning have two `for` loops or one for loop and one `if`
- (__Item: 29__) Avoid Repeated Work in Comprehensions by Using Assignment Expression
- (__Item: 30__) Consider `Generators` Instead of Returning `Lists`
- (__Item: 31__) Be Denfensive when Iterative Over `Arguments`
- (__Item: 32__) Consider `Generator Expressions` for Large `Lists` Comprehensions
    - Generator expressions execute very quickly when chained together and are memory efficient
- (__Item: 33__) Compose Multiple Generators with `yeild from`
- (__Item: 35__) Avoid Causing State Transitions in Generators with `throw
- (__Item: 36__) Consider `itertools` foe working with iterators and generators
    - `chain`, `repeat`, `cycle`, `tee`, `zip_longest`, `islice`, `takewhile`, `dropwhile`, ``, `filterfalse`, `accumulate`, `product`, `permutations`, `combinations`

## Classes and Interfaces

- (__Item: 37__) Compose Classes Instead of Nesting Many Levels of Built-in Types
    - bascially if you have to futher then one level of nesting, i.e, a dictionay in a tuple or a tuple in a dictionary , re-think aprpoach 
    - it is time to use classes to create a layer of abstraction between your interfaces and concrete implementations
    - use `namedtuple` for lightweight immutable data containers before you need the flexibility of a full class
   - move your code to using multiple classes when you internal state dictionaries get complicated
- (__Item: 38__) Accept Functions instead of Classes for Simple Interfaces
    - you can pass fuction or class methods to functions as API hooks
    - using a helper class to provide the behavior of a stateful closure is clearner
    -  when you need a function to maintain state, consider defining a class that provides the` __cal__` method instead of defining a stateful closure
- (__Item: 39__) Use `@classmethod` Polymorphism to Construct Objects Generically
    - Use `@classmethod` to define alternative constructors for your classes
    - Use class method polymorphism to provide generic ways to build and connect many concrete subclasses
    - essentially what this will allow you to do is generically connect and initialize things like `mapreduce`
- (__Item: 40__) Initialize Parent Classes with `super`
    - use `.mro()` to see order of function calls
- (__Item: 41__) Consider Composing Functionality with Mixin Classes
- (__Item: 42__) Perfer Public Attributes over Private Ones
    - Use documentation of protected fields to guide subclasses instead of trying to force access control with private attributes.
- (__Item: 43__) Iherit from `collections.abc` for Custom Container Types

## Metaclasses and Attributes

- (__Item: 44__) Use Plain Attributes Instead of `Sette`r and `Getter` Methods 
    - Use `@property` to define special behavior when attributes are `geters` and `seters`
    - Ensure that `@property` methods are fast; for slow or complex work— especially involving I/O or causing side effects—use normal methods instead
- (__Item: 45__) Consider `@property` Instead of Refactoring Attributes
    - dont overuse `@property`. When you keep extending @property, it’s time to refactor the class
- (__Item: 46__) Use Descriptors for Reusable `@property` methods
    - the problem with the @property is reuse; the methods `@property` decorates cant be reused for multiple attributes of the same or unrelated class
    - Reuse the behavior od @property methods by defining your own `descriptor protocol` classes with `__get__` and `__set__`
    - Use WeakKeyDictionary to ensure that your descriptor classes don’t cause memory leaks
- (__Item: 47__) Use `__getattr__`. `__getattribute__` and `__setattr__` for Lazy Attributes
    - Use `__getattr__` and `__setattr__` to lazily load and save attributes
    - `__getattribute__` is more advance then `__getattr__` and will be called on every call even if attribute is set
    - there is considerable overhead added; use `super()` to avoid infinite recursion for an object
- (__Item: 48__) Validate Subclasses with `__init_subclass__`
    - Metaclasses can be used to inspect or modify a class after it’s defined but before it’s created, but they’re often more heavyweight than what you need
    - Use `__init_subclass__` to ensure that subclasses are well formed at the time they are defined, before objects of their type are constructed and does not require `metaclasses` or `type` inheritane
- (__Item: 49__) Register Class Existence with `__init_subclass__`
    - class registration is a helpful pattern for building modular Python programs
    - `metaclasses` let you run registration code automatically each time a base class is subclassed in a program
- (__Item: 50__) Annotate Class Attributes with `__set_name__`
    - `metaclasses` enable you to modify a class's attributes before the class is fully defined
    - define `set_name__` on your descriptor classes to allow them to take into account their surrounding class and its property names
    - avoid memory leaks and the `weakref` module by having descriptors store data they manipulate directly withing a class's instance dictionary
- (__Item: 51__) Perfer Class Decorators Over Metaclasses for Composable Class Extensions
    - A class decorator is a simple function that receives a class instance as a parameter and returns either a new class or a modified version of the original class
    - Class decorators are useful when you want to modify every method or attribute of a class 

## Robustness and Performance

- (__Item: 65__) Take Advantage of Each Block in `try`/`except`/`else`/`finally`
    - use `try`/`finally` when you want exceptions to propagate up but also want to run cleanup code even when exceptions occur
    - use `try`/`else` to make it clear which excaptions will be handled by your code and which exceptions will propagate up
- (__Item: 66__) Consider `contextlib` and `with` Statements for Reusable `try`/`finally` Behavior
    - The `contextlib` built-in module provides a `contextmanager` decorator that makes it easy to use your own functions in `with` statements
    - The value `yielded` by context managers is supplied to the `as` part of the with statement.  your code an directly access the cause of a special context
- (__Item: 67__) Use `datetime` Instead of `time` for Local Clocks
- (__Item: 68__) Make `pickle` Reliable with `copyreg`
- (__Item: 69__) Use `decimal` or `fraction` when Precision is Paramount
- (__Item: 70__) Profile Before Optimizing
    - use `cProfiler` over `Profiler`
    - `Stats` lets you select what data you want to see
- (__Item: 71__) Perfer `deque` for Producer-Consumer Queues
- (__Item: 72__) Consider Searching Sorted Sequences with `bisect`
- (__Item: 73__) Know How to Use `heapq` for Priority Queues 
    -  To use heapq, the items being prioritized must have a natural sort order, which requires special methods like __lt__ to be defined for classes
- (__Item: 74__) Consider `memoryview` and `bytearray` for zero-copy interactions

## Testing and Debugging

- (__Item: 75__) Using `repr` Strings for Debugging Output 
    - `repr` can be used to type-check
    - you can reach into the object instance dictionary, which is stored in the __dict__ attribute
- (__Item: 76__) Verify Related Behaviors in `TestCase` Subclasses
    - use `help(TeseCase)` to find methods like `assertEqual` or `assertTrue`
    -  consider writing data-driven tests using the subTest helper method in order to reduce boilerplate
- (__Item: 77__) Isolate Tests from Each Other with `setUp`, `tearDown`, `setUpModule` and `tearDownModule`
    - it’s important to write both `unit tests` (for isolated functionality) and `integration tests` (for modules that interact with each other)
- (__Item: 78__) Use Mocks to Test Code with Complex Dependencies
    -  use `ANY` to indicate any value is ok for an argument
    - use `call` to test how many times a function was called
- (__Item: 79__) Encapsulate Dependencies to Facilitate Mocking and Testing
- (__Item: 80__) Consider Interactive Debugging with `pdb` 
    - The pdb module can be used for debug exceptions after they happen in independent Python programs (using `python -m pdb -c continue <program path>`) or the interactive Python interpreter (using import `pdb; pdb.pm()`)
- (__Item: 81__) Use `tracemalloc` to Understand Memory Usage and Leaks 
- `gc` module can help you understand which object exist
- `tracemalloc` helps to understanding the source of memeory usage

## Collaboration

- (__Item: 84__) Write Docstrings for Every `Function`, `Class` and `Module`
- (__Item: 85__) Use Packages to Organize Modules and Provide Stable `APIs` 
- (__Item: 87__) Define a Root `Exception` to Insulate Callers from APIs
- (__Item: 88__) Know How to Break Circular Dependencies
- (__Item: 89__) Consider `Warnings` to Refactor and Migrate Usage
- (__Item: 90__) Consider Static Analysis via typing to Obviate Bugs
