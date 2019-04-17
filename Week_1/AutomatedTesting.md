# Automated Testing

## Unit Testing

Unit testing is the practice of testing mall pieces of code, typically individual functions, alone and isolated.

A unit tests should essentially just give the function that's tested some inputs, and then check what the function outputs is correct.

When should you use unit testing? Ideally all the time, by applying test-driven development.


## Integration Testing

As the name suggests, in integration testing the idea is to test how parts of the system work together - the integration of the parts.
Integration tests are similar to unit tests, but there's one big difference: while unit tests are isolated from other components, integration tests are not.

You should have fewer integrations tests than unit tests.


## Functional Testing

Functional testing is also sometimes called E2E testing, or browser testing.
Functional testing is defined as the testing of complete functionality of some application.

While you can have hundreds of unit tests, you usually want to have only a small amount of functional tests.

## ->IN CLOSING<-

Unit tests should be your main focus when testing JavaScript code. They are the easiest to write and maintain, and provide many benefits beyond reducing bugs.

Integration and functional tests should be in a supporting role, for where unit tests are not suitable.


# The Happy Path

The happy path is the path through a system where everything works, the data is correct, the system stays up, and the users are well-behaved.

It doesn't take too long to test the happy path. It takes forever to test everything off the happy path. You need to spend a lot of time wandering away from the happy path, and maybe there is a reverse rule for testing:
20% of your time on the happy path
80% of your time off of it.


# Test Drive Development - TDD

In essence you follow three simple steps repeatedly:
* Write a test for the next but of functionality you want to add.
* Write the functional code until the test passes.
* Refactor both new and old code to make it well structured.

This provides two main benefits

1. Most obviously it's a way to get SelfTestingCode, since you can only write some functional code in response to making a test pass.
2. The second benefit is that thinking about the test first forces you to think about the interface to the code first.

# Behavior-Driven Development - BDD

BDD combines the general techniques and principles of TDD with ideas from domain-driven design and object-oriented analysis and design to provite software development and management teams with shared tools and a shared process to collaborate on software development.

# Stubbing and Mocking

## Stubbing
Means replacing a method, function or an entire object with a version that produces hard-coded responses.
This is typically used to isolate components from each other, and your code from the  outside world.

## Mocking
Is a form of testing that involves verifying behaviour by checking which methods are called during a test.

