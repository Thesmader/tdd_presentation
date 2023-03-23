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
# Green Bar Patterns

Treat a red bar as a condition to be fixed as quickly as possible. To do that we have following patterns to leverage.

* Fake it (Until you make it)
* Triangulate
* Obvious Implementation 
* One to Many

---

# Fake it (Until you make it)

Say we have a broken test, the quickest way to a green bar is to replace the expression with a constant. Once we confirm on getting a green bar after using a constant, we can then work our way up to converting that into an expression.

~~~java
@Test
public void testLength()
{
	final int result = objectUnderTest.myLength("hello");
	assertEquals(5, result)
}
~~~

---
# What makes "Fake it" a powerful pattern?

* Psychological Effect - Green bar: GOOD, red bar: BAD.
* Scope Control - Starting with something concrete and generalizing stuff from there prevents premature confusion.


PS: Do not confuse the above as a necessary step. The above implies when you wrote an *obvious implementation* and somehow the test did not pass. The you go back to smaller steps and use this pattern. Things probably will not be as simple as the above example.

---

# Triangulate

Abstract only where there are two or more examples. For instance:

~~~java
public void testSum()
{
	assertEquals(4, plus(3,1));
}

private int plus(int augend, int addend)
{
	return 4; //(is this fake it?!)
}
~~~

Now if we were triangulating to the right design, we would write

~~~java 
public testSum()
{
	assertEquals(4, plus(3,1))
	assertEquals(7, plus(3,4))
}
~~~

Which would convert `plus()` eventually into:

~~~java
public plus(int augent, int addend)
{
	return augend+addend;
}
~~~

---

# Obvious Implementation

If you're sure of the exact implementation needed, go right ahead. If your implementation gives red bars, go back to smaller steps/patterns like triangulation or fake it.

This however can be psychologically devastating, becuase you're kind of demanding perfection from yourself. You're solving "clean code" as well as "that works".

PS: Maintain RED, GREEN, REFACTOR rhythm.

---

# One to Many

If there is an operation that needs to handle a collection of objects, implement it without collections first. Then make it work with collections.

For instance, in case we need to work with an array of numbers, we can simply start with just one!!

Here we need to write a function to sum an array of numbers:

~~~java
public void testSum()
{
	assertEquals(5, sum(5));
}

private int sum(int value)
{
	return value;
}
~~~

The above gets converted into

~~~java

public void testSum()
{
	assertEquals(5, sum(new int[] {5}));
}


private int sum(int[] values)
{
	int sum = 0;
	for(int i=0; i<values.length; i++)
	{
		sum+=values[i];
	}
	return sum;
}
~~~
---
# Design Patterns

Applying objects to organize computing is one of the best examples of common internally generated subproblems being solved in common, predictable ways. We can extend the same approach for design to TDD, although with some slight differences.

Following are the design patterns we'll be covering:
* Command
* Value Object
* Null Object
* Template Method
* Pluggable Object

---
# Command

## Brief
Represent the invocation of a computation as an object, not just as a message.

When we need invocation to be just a little more concrete and manipulable than a message, objects give us the answer.
Make an object representing the invocation. Seed it with all the parameters the computation will need. When we're ready to invoke it, use generic protocol, like `run()`. In the implementation of `run()` we can do anything we like.

~~~java
interface Runnable
	public abstract void run();
~~~
---
# Value Object

## Brief
Avoid aliasing problems by making objects whose values never change once created.

If two objects share a reference to a third, and if one object changes the shared object, then the other object better not rely on the state of the shared object.

How to resolve aliasing problems?!
When implementing a Value Object, every operation has to return a fresh object, leaving the original unchanged.
---
# Null Object

## Brief
Represent the base case of a computation by an object.

### Example

~~~java
public boolean setReadOnly() {
	SecurityManager guard = System.getSecurityManager(); 
	if (guard != null) {
		guard.canWrite(path); 
	}
	return fileSystem.setReadOnly(this); 
}
~~~

Say we have multiple places where `guard != null` is being checked. As the number of touch points increase, it becomes increasingly complex to ensure that null checks at every touchpoints are being made.


What's the solution to the above issue?!
An intuitive solution is to create a new class, which does not throw error, like so.

~~~java
public static SecurityManager getSecurityManager() 
{ 
	return security == null ? new LaxSecurity() : security;
}
~~~

~~~java
public boolean setReadOnly() 
{
	SecurityManager security = System.getSecurityManager();
	security.canWrite(path);
	return fileSystem.setReadOnly(this);
}
~~~

---

#Template Method

## Brief
Represent invariant sequences of computation with an abstract method intended to be specialized through inheritance.

In simple words, have a base class which can then be extended to other subclasses as per their specific use case.

### Example


Initial implementation
~~~java
public class worldOfWarcraftLoader(){
	public void load(){
		system.out.println("loading local WoW files");
		// some code
		system.out.println("creating needed WoW objects");
		//some code
		system.out.println("Downloading WoW sounds and videos");
		//some code
		system.out.println("cleaning temp files");
		//some code
		system.out.println("Loading saved WoW profiles");
		//some code
	}
}

public class Diablo(){
	public void load()
	{
		system.out.println("loading local Diablo files");
		//some code
		system.out.println("creating needed diablo objects");
		//some code
		system.out.println("Downloading diable sounds and videos");
		//some code
		system.out.println("cleaning temp files");
		//some code
		system.out.println("Loading saved diablo profiles");
		//some code
	}
}
~~~
---
How to get rid of code duplication here?!

* Break down the steps into a series of methods
* put a series of calls to these method/steps inside a "template method"
* The steps can either be abstract or they can have some default implementation inside the parent class

---

~~~java

public abstract class BaseGameLoader{
	public void load(){
		byte[] data = loadLocalData();
		createObjects(data);
		downloadAdditionalFiles();
		cleanTempFiles();
		initializeProfiles();
	}

	abstract byte[] loadLocalData();
	abstract void createObjects(byte[] data);
	abstract void downloadAdditionalFiles();
	abstract void initializeProfiles();

	protected void cleanTempFiles(){
		// some code
	}
}

The above base class now can be extended to each subclass.

We define the skeleton in the base class and let the subclass override whenever necessary.

~~~

---

# Pluggable Object

## Brief
Represent variation by invoking another object with two or more implementations.

Pluggable objects come in handy when we have to express/demonstrate variation. The simplest/intuitive way for this is to use conditionals, but the caveat here is that conditional can expand and become complex to handle. Also, it's duplication. This is where pluggable objects come in.

### Context
When writing a graphics editor, selection is actually a bit complicated. If you're over a figure when you press the mouse button, then subsequent moves of the mouse move that figure and releasing the mouse button leaves the figure selected. If you're not over a figure, then you are selecting a group of figures, and subsequent moves of the mouse typically resize a rectangle used to select several figures. Releasing the mouse button causes the figures inside the rectangle to be selected. The initial code looks something like this:

#### Duplication Example
~~~java
Figure selected;
public void mouseDown() {
	selected= findFigure(); 
	if (selected != null)
		select(selected); 
}
public void mouseMove() { 
	if (selected != null)
		move(selected); 
	else
		moveSelectionRectangle(); 
}
public void mouseUp() { 
	if (selected == null)
		selectAll(); 
}
~~~

To remove duplication, we can create a pluggable object, a `SelectionMode`, with two implementations, `SingleSelection` and `MultipleSelection`.

<<<<<<< HEAD
=======
~~~java
SelectionMode mode; 
public void mouseDown() 
{
	selected= findFigure(); 
	if (selected != null)
		mode= SingleSelection(selected); 
	else
		mode= MultipleSelection(); 
}

public void mouseMove() 
{ 
	mode.mouseMove();
}

public void mouseUp() 
{
	mode.mouseUp(); 
}

~~~
>>>>>>> 30d053b (final)
---
# Refactoring with TDD

<<<<<<< HEAD
Aim to not do "Leap of Faith" refactoring, unless you can repeat the refactoring mechanically. The strategy should always be to take small steps and have concrete feedback
=======
# Refactoring

Don't do "Leap of Faith" refactoring, unless you can repeat the refactoring mechanically. The strategy should always be to take small steps and have concrete feedback
>>>>>>> 30d053b (final)
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
