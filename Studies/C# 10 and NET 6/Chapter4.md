# Chapter 04: Writing, Debugging and Testing Functions

## Table of contents
- [Writing functions](#writing-functions)
  - [Writing a times table function](#writing-a-times-table-function)
  - [Writing a function that returns a value](#writing-a-function-that-returns-a-value)
  - [Converting numbers from cardinal to ordinal](#converting-numbers-from-cardinal-to-ordinal)
  - [Calculating factorials with recursion](#calculating-factorials-with-recursion)
  - [Documenting functions with XML comments](#documenting-functions-with-xml-comments)
  - [Using lambdas in function implementations](#using-lambdas-in-function-implementations)
- [Debugging during development](#debugging-during-development)
- [Logging during development and runtime](#logging-during-development-and-runtime)
- [Unit testing](#unit-testing)
- [Throwing and catching exceptions in functions](#throwing-and-catching-exceptions-in-functions)
- [Practice](#practice)
  - [Exercise 4.1](#exercise-41)
  - [Exercise 4.2](#exercise-42)

## Writing functions

A fundamental principle of programming is _Don't Repeat Yourself (**DRY**)_.

While programming, if you find yourself writing the same statements over and over again, then turn those statements into a _function_.\
Functions are like tiny programs that complete one small task.

### Writing a times table function

```csharp
using static System.Console;

TimesTable(number: 64);

static void TimesTable(byte number)
{
    WriteLine($"This is the {number} times table:");
    for (int row = 1; row <= 12; row++)
    {
      WriteLine($"{row} x {number} = {row * number}");
    }

    WriteLine();
}
```
> [!NOTE] If a function has one or more parameters where just passing the values may not provide enough meaning, then you can optionally specify the name of the parameter as well as its value.


### Writing a function that returns a value

```csharp
using static System.Console;

decimal taxToPay = CalculateTax(amount: 149, twoLetterRegionCode: "FR");
WriteLine($"You must pay {taxToPay:C} in tax.");

static decimal CalculateTax( decimal amount, string twoLetterRegionCode)
{
    decimal rate = 0.0M;
    switch (twoLetterRegionCode)
    {
         case "CH":
             rate = 0.08M;
         break;

         case "DK":
         case "NO":
             rate = 0.25M;
         break;

         case "GB":
         case "FR":
             rate = 0.2M;
         break;

         case "HU":
             rate = 0.27M;
         break;

         case "OR":
         case "AK":
         case "MT":
             rate = 0.0M;
         break;
  
         case "ND":
         case "WI":
         case "ME":
         case "VA":
             rate = 0.05M;
         break;

         case "CA":
             rate = 0.0825M;
         break;

         default:
             rate = 0.06M;
         break;
    }

  return amount * rate;
}
```


### Converting numbers from cardinal to ordinal

```csharp
using static System.Console;

RunCardinalToOrdinal();

static string CardinalToOrdinal(int number)
{
  switch (number)
  {
    case 11:
    case 12:
    case 13:
      return $"{number}th";

    default:
      int lastDigit = number % 10;
      string suffix = lastDigit switch
      {
        1 => "st",
        2 => "nd",
        3 => "rd",
        _ => "th"
      };
      return $"{number}{suffix}";
  }
}

static void RunCardinalToOrdinal()
{
  for (int number = 1; number <= 40; number++)
  {
    Write($"{CardinalToOrdinal(number)} ");
  }

  WriteLine();
}
```


### Calculating factorials with recursion

```csharp
using static System.Console;

RunFactorial();

static int Factorial(int number)
{
  if (number < 1)
  {
    return 0;
  }
  else if (number == 1)
  {
    return 1;
  }
  else
  {
    checked
    {
      return number * Factorial(number - 1);
    }
  }
}

static void RunFactorial()
{
  for (int i = 1; i < 15; i++)
  {
    try
    {
      WriteLine($"{i}! = {Factorial(i):N0}");
    }
    catch (OverflowException)
    {
      WriteLine($"{i}! is too big for a 32-bit integer.");
    }
  }
}
```
> [!NOTE] Recursion is clever, but it can lead to problems, such as a stack overflow due to too many function calls because memory is used to store data on every function call,and it eventually uses too much.\
> Iteration is a more practical, if less succinct, solution in languages such as C#.


### Documenting functions with XML comments
```csharp
/// <summary>
/// Pass a 32-bit integer and it will be converted into its ordinal equivalent.
/// </summary>
/// <param name="number">Number is a cardinal value e.g. 1, 2, 3, and soon.</param>
/// <returns>Number as an ordinal value e.g. 1st, 2nd, 3rd, and so on.</returns>
```


### Using lambdas in function implementations

Functional languages evolved from _lambda calculus_: a computational system based only on functions.\
The code looks more like mathematical functions than steps in a recipe.\
Some of the important attributes of functional languages are defined in the following list:
- **Modularity**: The same benefit of defining functions in C# applies to functional
languages. Break up a large complex code base into smaller pieces.
- **Immutability**: Variables in the C# sense do not exist. Any data value inside a function
cannot change. Instead, a new data value can be created from an existing one. This
reduces bugs.
- **Maintainability**: Code is cleaner and clearer.

Since C# 6, Microsoft has worked to add features to the language to support a more functional approach.\
In C# 6, Microsoft added support for expression-bodied function members.

_Imperative variant_:
```csharp
using static System.Console;

RunFibImperative();

// ... CardinalToOrdinal() ...

static int FibImperative(int term)
{
  if (term == 1)
  {
    return 0;
  }
  else if (term == 2)
  {
    return 1;
  }
  else
  {
    return FibImperative(term - 1) + FibImperative(term - 2);
  }
}

static void RunFibImperative()
{
  for (int i = 1; i <= 30; i++)
  {
    WriteLine("The {0} term of the Fibonacci sequence is {1:N0}.",
              arg0: CardinalToOrdinal(i),
              arg1: FibImperative(term: i));
  }
}
```

_Functional variant_:
```csharp
using static System.Console;

RunFibFunctional();

// ... CardinalToOrdinal() ...

static int FibFunctional(int term) =>
  term switch
  {
    1 => 0,
    2 => 1,
    _ => FibFunctional(term - 1) + FibFunctional(term - 2)
  };

static void RunFibFunctional()
{
  for (int i = 1; i <= 30; i++)
  {
    WriteLine("The {0} term of the Fibonacci sequence is {1:N0}.",
              arg0: CardinalToOrdinal(i),
              arg1: FibFunctional(term: i));
  }
}
```


## Debugging during development




## Logging during development and runtime




## Unit testing




## Throwing and catching exceptions in functions




## Practice

### Exercise 4.1



### Exercise 4.2
