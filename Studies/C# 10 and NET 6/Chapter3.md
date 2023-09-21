# Chapter 03: Controlling Flow, Converting Types and Handling Exceptions

## Table of contents
- [Operating on variables](#operating-on-variables)
- [Understanding selection statements](#understanding-selection-statements)
- [Understanding iteration statements](#understanding-iteration-statements)
- [Casting and converting between types](#casting-and-converting-between-types)
- [Handling exceptions](#handling-exceptions)
- [Checking for overflow](#checking-for-overflow)
- [Practice](#practice)
  - [Exercise 3.1](#exercise-31)
  - [Exercise 3.2](#exercise-32)
  - [Exercise 3.3](#exercise-33)
  - [Exercise 3.4](#exercise-34)



## Operating on variables




## Understanding selection statements




## Understanding iteration statements




## Casting and converting between types




## Handling exceptions




## Checking for overflow



## Practice

### Exercise 3.1

#### What happens when you divide an `int` variable by 0?
Program will throw _DivideByZero_ exception.

#### What happens when you divide a `double` variable by 0?
It results in positive infinity, negative infinity, or not a number (NaN).

#### What happens when you overflow an `int` variable, that is, set it to a value beyond its range?
~~If the overflow over higher bound of range, then it returns minimum value of variable type. If the overflow below lower bound of range, then it returns maximum value of variable type.~~\
**Correct**: *It will loop unless you wrap the statement in a checked block, in which case, _OverflowException_ will be thrown.*

#### What is the difference between `x = y++;` and `x = ++y;`?
The difference that `y++` is postfix unary operator, which increases variable after assignment, whereas `++y` is prefix unary operator, which increases variable before assignment.

#### What is the difference between `break`, `continue`, and `return` when used inside a loop statement?
We use `break` statement to stop execution of the loop and continue execution of statements after loop body, `return` to stop execution of the method and return a value and `continue` to skip current stage of cycle.

#### What are the three parts of a `for` statement and which of them are required?
There are three parts of `for` statement.
First is declaration and assignment of loop variable.
Second is an execution condition of the loop.
Third is increment or decrement.
Required part is only an execution condition, others are optional.

#### What is the difference between the = and == operators?
The `=` is an assignment operator whereas `==` is an equality checking operator.

#### Does the `for ( ; true; )` statement compile? 
Yes, it does cause `for` loop requires only execution condition.

#### What does the underscore represent in a `switch` expression?
The underscore represents the default return value.

#### What interface must an object implement to be enumerated over by using the `foreach` statement?
`IEnumerable` including all methods.


### Exercise 3.2

```csharp
using static System.Console;

int max = 500;
checked
{
    for (byte i = 0; i < max; i++)
    {
        WriteLine(i);
    }
}
```


### Exercise 3.3

```csharp
using static System.Console;

Write("Enter a number between 0 and 255: ");
string? number = ReadLine();
Write("Enter another number between 0 and 255: ");
string? anotherNumber = ReadLine();

try
{
    #nullable disable
    byte dividend = byte.Parse(number);
    byte divider = byte.Parse(anotherNumber);

    int quotient = dividend / divider;

    WriteLine($"{dividend} divided by {divider} is {quotient}");
}
catch (Exception e)
{
    WriteLine($"{e.GetType().Name}: {e.Message}");
}
```

### Exercise 3.4
