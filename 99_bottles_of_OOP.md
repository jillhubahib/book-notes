# 99 Bottles of OOP by Sandi Metz and Katrina Owen

## Introduction

This book creates a simple solution to the "[99 Bottles of Beer](https://www.youtube.com/watch?v=u-lV0vrEWXw)" song problem, and then applies a series of refactorings to improve the design of the code.

Writing code is the process of working your way to the next stable end point, not the end point itself. You don’t know the answer in advance, but instead, you are seeking it.

The authors cheerfully stipulate the fact that you are unlikely to encounter the "99 Bottles of Beer" song in your daily work, and that problems of similar size are best solved very simply. For the purposes of this book, "99 Bottles" is convenient because it’s simultaneously easily understandable and surprisingly complex, and so provides an expedient stand-in for larger problems. Once you understand the solutions here, you’ll be able to apply them to the much larger real world.

## 1. Rediscover Simplicity

- Object-Oriented Design is about picking the right abstractions. If you choose well, your code will be expressive, understandable and flexible, and everyone will love both it and you. However, if you get the abstractions wrong, your code will be convoluted, confusing, and costly, and your programming peers will hate you.

- Abstractions are hard, and even with the best of intentions, it’s easy to get them wrong. Well-meaning programmers tend to over-anticipate abstractions, inferring them prematurely from incomplete information. Early abstractions are often not quite right, and therefore they create a catch-22. You can’t create the right abstraction until you fully understand the code, but the existence of the wrong abstraction may prevent you from ever doing so. This suggests that you should not reach for abstractions, but instead, you should resist them until they absolutely insist upon being created.

### 1.1 Simplifying Code

- The code you write should meet two often-contradictory goals. It must remain concrete enough to be understood while simultaneously being abstract enough to allow for change.

  Imagine a continuum with "most concrete" at one end and "most abstract" at the other. Code at the concrete end might be expressed as a single long procedure full of
if statements. Code at the abstract end might consist of many classes, each with one method containing a single line of code.

  The best solution for most problems lies not at the extremes of this continuum, but somewhere in the middle. There’s a sweet spot that represents the perfect compromise between comprehension and changeability, and it’s your job as a programmer to find it.

#### Value/Cost Questions
1. How difficult was it to write?
2. How hard is it to understand?
3. How expensive will it be to change?

#### Domain Questions
1. How many verse variants are there?
2. Which verses are most alike? In what way?
3. Which vreses are most different, and in what way?
4. What is the rule to determine which verse comes next?

#### Solutions to 99 Bottles of Beer song
  - [Incomprehensibly Concise](https://github.com/sandimetz/99bottles/blob/2687ffc8e26f2ecd885a6a8e8771287627c83144/lib/bottles.rb) - Problems with consistency, duplication, and naming consipire to make this code likely costly
  - [Speculatively General](https://github.com/sandimetz/99bottles/blob/0a7b2f42765c3a920086dd79f1f16c1174bd3ca6/lib/bottles.rb) - harder to understand without being easier to change, the additional complexity does not pay off
  - [Concretely Abstract](https://github.com/sandimetz/99bottles/blob/ae028ca8c430a158ae488422f1a69a0fc3142d1d/lib/bottles.rb) - DRY yet expensive to change, method name are named by how it behave rather than its concept e.g. beer instead of beverage
  - [Shameless Green](https://github.com/sandimetz/99bottles/blob/27377c586c9a5477e363f2e0f258d1c0ce9e9f45/lib/bottles.rb) - easy to understand, although it duplicates strings and not object oriented

### 1.2 Judging Code
- Based on opinion statements:
  > I like my code to be elegant and efficient. - Bjarne Stroustrup (inventor of  C++)

  > Clean code is ... full of crisp abstractions ... - Grady Booch (author of Object Oriented Analysis and Design with Applications)

  > Clean code was written by someone who cares. - Michael Feathers (author of Working Effectively with Legacy Code)

  #### Cons
  - Multitude of definitions, no concrete guidance to achieve
  - Qualitative not quantitative
  - Fruitless arguments

- Based on Facts
  #### Metrics
  - **Source Lines of Code** (SLOC or LOC) - used to predict 1. total effort, 2. measure productivity and 3. cost of maintenance. SLOC alone is not enough to predict code quality.
  - **Cyclomatic Complexity** - published by Thomas J. McCabe in 1976. It is an algorithm that counts the number of unique execution paths through a body of source code. Think of this algorithm as a little machine that ponders your code and then maps out all the possible routes through every combination of every branch of every conditional. A method with many deeply nested conditionals would score very high, while a method with no conditionals at all would score 0. **Usage**: compare code, limit overall complexity, determine if you've written enough tests. Cyclomatic complexity views the world of code through a narrow lens, doesn't take everything into account.
  - **Assignments, Branches, and Conditions** (ABC) Metric - twenty-one years after the unveiling of cyclomatic complexity, Jerry Fitzpatrick published this in 1997 in which he describes a metric that does consider more than conditionals. His ABC stands for assignments, branches and conditions, where:
    - Assignments is a count of variable assignments.
    - Branches counts not branches of an if statement (as one could forgivably infer) but branches of control, meaning function calls or message sends.
    - Conditions counts conditional logic.
    The most popular tool for generating ABC scores for Ruby code is Ryan Davis’s [Flog](http://ruby.sadi.st/Flog.html).

There’s something beyond complexity — a higher level of simplicity