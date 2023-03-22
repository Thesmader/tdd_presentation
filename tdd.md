# Test-Driven Development Patterns
Points covered, 
1. what do we mean by testing?
2. when do we test?
3. How do we choose what logic to test?
4. How do we choose what data to test?

Lets see an example of a Sam an employee who's not aligned with TDD.
Once he starts to feel more stress, the less testing he'll do, the less testing he do, the more errors he'll make, the more error's you make the more stress he'll feel. This loop is inevitable.

Lets see an example of a Peter an employee who is aligned with TDD.
Once he/ she starts to feel more stress, the more tests he'll write, Running the tests immediately gives him more confidence, it reduces the errors made, which further reduces the stress.

A mistake when implementing a low level feature which could potentially crash the development environment resulting in rollback to the initial point.  --> reason to why testing shows its importance.

how to do testing?
First, make the tests so fast to run that you could run then yourself.
Second, Seek test at a smaller scale then the whole application, tests should be able to ignore one another completely.
sometimes you'll need to work hard to break your problem into little orthogonal dimensions ( fragments ), so the environment for each test will be easy. 
This method encourages you to isolate tests and compose solutions out of many highly cohesive, loosely coupled objects.


Note: The first part of our approach to dealing with programming stress is never to take a step forward unless we know where out foot is at.
Stop keeping things all in your head, 
Because the more experience you get -> the more things you know that might need to be done, 
The more things you need to be done -> the less attention you get for what you are doing,
The less attention you get for what you are doing -> the less you accomplished
The less you accomplish -> the more things you knew that needs to be done.
In the end you are left with your very own soulmate -> STRESS!!


One method you could try:
Writing down everything you want to accomplish over the next few hours. 
If a new item comes up, quickly and conciously decide whether it belonged in 'now' list or 'later' list, or whether it didnt really need to be done at all.

TDD:
Write down all the tests that corresponds to the feature.
Start with a test that will teach you something, but you are certain you'll get it quickly and get it passed, add action items to refactor list
If you are working in the application for nth time, pick something that will have one or two operations.
refactor the implementation and move on to the next test.

---
# Things that developers should avoid when practicing TDD:
1. Writing tests that are too complex.
2. Writing tests that duplicate functionality: Developers should avoid writing tests that duplicate functionality already covered by other tests, as this can lead to redundancy and make the test suite more difficult to manage.
3. Writing too much code before writing tests: TDD emphasizes writing tests before writing production code. Developers should avoid writing large amounts of production code before writing tests, as this can make it more difficult to test the code and can lead to a less effective test suite.
4. Neglecting to refactor code: TDD involves continuously refactoring code to make it cleaner, more maintainable, and easier to understand.
5. Neglecting collaboration with stakeholders: TDD emphasizes collaboration between developers, testers, and business stakeholders to ensure that software is meeting the needs of its users. Developers should avoid neglecting collaboration with stakeholders, as this can lead to misunderstandings, missed requirements, and software that doesn't meet user needs.

---
# Recommended first steps for developers who want to start using TDD:
1. Start with a small project: If you're new to TDD, it's a good idea to start with a small project to get familiar with the approach. Choose a project that you can complete in a short amount of time, such as a simple utility or a small feature of a larger application.
2. Identify the requirements: Before you start writing any code, identify the requirements for the project. What problem are you trying to solve? What functionality do you need to implement? What inputs and outputs are involved?
3. Write a failing test: Once you have identified the requirements, write a failing test that captures those requirements. The test should be small, focused, and easy to understand.
4. Write the minimum amount of code to pass the test: Once you have a failing test, write the minimum amount of code necessary to make the test pass. Don't worry about making the code perfect at this point - you'll have a chance to refactor it later.
5. Refactor the code: After you have written the minimum amount of code to pass the test, take some time to refactor the code. Make it cleaner, more maintainable, and easier to understand. You may also want to add additional test cases at this point to ensure that the code is working as intended.
6. Repeat the process: Once you have refactored the code, go back to step 3 and repeat the process. Write another failing test, write the minimum amount of code to make it pass, and refactor the code. Keep repeating this process until you have implemented all of the required functionality.

By following these steps, you can start to get a sense of how TDD works and how it can help you to build better software. Over time, you can refine your TDD skills and become more proficient at using this approach to develop high-quality, maintainable code.

---
# Refactoring with TDD

Aim to not do "Leap of Faith" refactoring, unless you can repeat the refactoring mechanically. The strategy should always be to take small steps and have concrete feedback
(tests help with that).

---
# Encourages safer changes:

With TDD when you are writing tests before you write the code, you will have a clear idea of what the code needs to do and how it should
behave. If you have good tests covering the existing code, you can make changes confidently, as the tests will detect any regressions

---
# Facilitate better design decisions

A core principle of TDD is to make small, incermental additions/changes to the code when you need it. This allows you to focus on
breaking down large, complex pieces of code into smaller, more manageable components. This leads to having more flexible code in
the long run

---
# Promotes collaboration while refactoring

Tests can promote team members to work together on refactoring code. Tests can help build a shared understanding of the requirement
and behavior of the code. When team members are familiar with the tests covering a piece of code and what they're testing for,
it becomes easier to work together for refactoring.

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

---
## TDD leads to frameworks
Test driving development leaves you with frameworks that are good at expressing exactly the necessary spots to accomodate a variation. Once you've been test driving
development long enough, you can recover from most of your mistakes faster than you can recognize you've made them.

---
## Can you test drive enormous systems?

If you're following TDD correctly, the amount of functionality in the system doesn't seem to have a bearing on the effectiveness of TDD.
By eliminating duplication, creating smaller objects, breaking a feature in to smaller parts and separating them, 
all these different entities can be tested in isolation. The most important factor here is that the code be written with tests
in mind
