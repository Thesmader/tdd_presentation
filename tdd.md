# Refactoring

Don't do "Leap of Faith" refactoring, unless you can repeat the refactoring mechanically. The strategy should always be to take small steps and have concrete feedback
(tests help with that).

## Approaches to refactoring:
- Isolate Changes: Try to isolate the parts where you're making changes while refactoring. And make sure the system as a whole is still works
- Migrate Data (gradually):
- Extracting methods: Q. How do you make a long, complicated method easier to read?
A. Turn a small part of it into a separate method and call the new method. Keep doing this until you can make sense of the longer method. Extracting parts of the long method
into smaller ones helps to understand what is happening there.
  -
- Inline method:

---
# Mastering TDD

## How large should the steps be?
There are 2 broad approaches to this: 
1. You can write tests so they each encourage the addition of a single line of logic and a handful of refactorings
2. You can write tests so they each encourage the addition of hundreds of lines of logic and hours of refactorings

Q. What should you go with?
A. You should be able to do either. When you're starting with a feature or refactoring, be prepared to take lots of tiny steps. As you progress, experiment with leaving out some
steps when you're comfortable thinking ahead about the feature or have done the refactoring enough times

---
## Automated refactoring accelerates refactoring enormously.
Look for opportunities to automate refactorings. If you can automate something that would have taken you 20 manaual steps, you can do it much faster. When you know this
you become much more aggressive in your refactorings.

---
## What should you not test?
Simple answer would be: Only test business logic.
Going a little deeper: Test business logic, but test only what you've written. Unless you've reason to distrust code written by someone else, don't test code from others

---
## How to know if you have good tests?
- Tests should not have very long setup code or processes
- Setup must not be duplicated everywhere. If you have to duplicate setup and cannot have common setup code where you think you should be able to. The code is probably
badly designed.
- Tests should not take long to run.
- Tests don't break when you don't expect them to

---
## TDD leads to frameworks
Test driving development leaves you with frameworks that are good at expressing exactly the necessary spots to accomodate a variation. Once you've been test driving
development long enough, you can recover from most of your mistakes faster than you can recognize you've made them.

---
## How much feedback do you need?
AKA, how many tests should you write?

There's no correct answer to this. Be smart about it. Take the following problem as an example:

Given 3 integers representing the length of sides of a triangle, return:
- 1 if the triangle is equilateral
- 2 if the triangle is isosceles
- 3 if the triangle is scalene
- throw an exception if the triangle is invalid

This is one of the examples in a book, and the author wrote 65 tests for the same problem. The tests also include cases like the values overflowing MAXINT. This case
has to do with how much memory you have. While building such a feature, do you expect such values to come up? If you're never going to get anywhere close to that value,
there's no point of writing this test. Writing or not writing a test for this case, doesn't affect the robustness of the program much in your context.

Tests are here for us to have confidence in the code we write. If your knowledge of the implementation, gives confidence even without a test, then you can choose to ignore
the test.
