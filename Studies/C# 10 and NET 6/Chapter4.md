# [Chapter 04: Writing, Debugging and Testing Functions](Source/Chapter04/WritingFunctions.cs)

## Table of contents
- [Writing functions](#writing-functions)
  - [Writing a times table function](#writing-a-times-table-function)
  - [Writing a function that returns a value](#writing-a-function-that-returns-a-value)
  - [Converting numbers from cardinal to ordinal](#converting-numbers-from-cardinal-to-ordinal)
  - [Calculating factorials with recursion](#calculating-factorials-with-recursion)
  - [Documenting functions with XML comments](#documenting-functions-with-xml-comments)
  - [Using lambdas in function implementations](#using-lambdas-in-function-implementations)
- [Logging during development and runtime](#logging-during-development-and-runtime)
  - [Understanding logging options](#understanding-logging-options)
  - [Instrumenting with Debug and Trace](#instrumenting-with-debug-and-trace)
  - [Configuring trace listeners](#configuring-trace-listeners)
  - [Switching trace levels](#switching-trace-levels)
- [Unit testing](#unit-testing)
- [Throwing and catching exceptions in functions](#throwing-and-catching-exceptions-in-functions)
  - [Understanding usage errors and execution errors](#understanding-usage-errors-and-execution-errors)
  - [Commonly thrown exceptions in functions](#commonly-thrown-exceptions-in-functions)
  - [Understanding the call stack](#understanding-the-call-stack)
  - [Where to catch exceptions](#where-to-catch-exceptions)
  - [Implementing the tester-doer pattern](#implementing-the-tester-doer-pattern)
  - [Problems with the tester-doer pattern](#problems-with-the-tester-doer-pattern)
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
> If a function has one or more parameters where just passing the values may not provide enough meaning, then you can optionally specify the name of the parameter as well as its value.


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
> Recursion is clever, but it can lead to problems, such as a stack overflow due to too many function calls because memory is used to store data on every function call,and it eventually uses too much.\
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



## Logging during development and runtime

No code is ever bug free, and during runtime unexpected errors can occur.\
End users are notoriously bad at remembering, admitting to, and then accurately describing
what they were doing when an error occurred, so you should not rely on them accurately
providing useful information to reproduce the problem to understand what caused the
problem and then fix it.
Instead, you can instrument your code, which means _logging events of interest_.

> Add code throughout your application to log what is
happening, and especially when exceptions occur, so that you can review the
logs and use them to trace the issue and fix the problem.


### Understanding logging options

.NET includes some built-in ways to instrument your code by adding logging capabilities.
But logging is an area where third parties have created a rich ecosystem of powerful solutions
that extend what Microsoft provides.\
List of some logging frameworks:
- **Apache log4net**
- **NLog**
- **Serilog**


### Instrumenting with Debug and Trace

The _Debug class_ is used to add logging that gets written only during development.

The _Trace class_ is used to add logging that gets written during both development and
runtime.

The Debug and Trace classes write to any trace listener. A _trace listener_ is a type that can be configured to write output anywhere you like when the WriteLine method is called. There are several trace listeners provided by .NET, including one that outputs to the console, and you can even make your own by inheriting from the _TraceListener_ type.

```csharp
using System.Diagnostics;

Debug.WriteLine("Debug says, I am watching!");
Trace.WriteLine("Trace says, I am watching!");
```


### Configuring trace listeners
```csharp
Trace.Listeners.Add(new TextWriterTraceListener(
    File.CreateText(Path.Combine(Environment.GetFolderPath(
        Environment.SpecialFolder.DesktopDirectory), "log.txt"))));

Trace.AutoFlush = true;
```


### Switching trace levels
```csharp
using Microsoft.Extensions.Configuration;

ConfigurationBuilder builder = new();
builder.SetBasePath(Directory.GetCurrentDirectory())
    .AddJsonFile("appsettings.json", optional: true, reloadOnChange: true);

IConfigurationRoot configuration = builder.Build();

TraceSwitch ts = new(
    displayName: "PacktSwitch",
    description: "This switch is set via a JSON config.");

configuration.GetSection("PacktSwitch").Bind(ts);

Trace.WriteLineIf(ts.TraceError, "Trace error");
Trace.WriteLineIf(ts.TraceWarning, "Trace warning");
Trace.WriteLineIf(ts.TraceInfo, "Trace information");
Trace.WriteLineIf(ts.TraceVerbose, "Trace verbose");
```



## Unit testing




## Throwing and catching exceptions in functions

### Understanding usage errors and execution errors

- _**Usage errors**_ are when a programmer misuses a function, typically by passing invalid values as parameters.\
  They could be avoided by that programmer changing their code to pass valid values.\
  Usage errors should all be fixed before production runtime.
- _**Execution errors**_ are when something happens at runtime that cannot be fixed by writing «better» code.\
  Execution errors can be split into:
  - _Program errors_. Can be programmatically fixed by writing smart code.
  - _System errors_. Often cannot be fixed programmatically.


### Commonly thrown exceptions in functions

Very rarely should you define new types of exceptions to indicate usage errors. .NET already defines many that you should use.\
When defining your own functions with parameters, your code should check the parameter values and throw exceptions if they have values that will prevent your function from properly functioning.\
For example, if a parameter should not be `null`, throw `ArgumentNullException`.\
For other problems, throw `ArgumentException`, `NotSupportedException`, or `InvalidOperationException`.\
For any exception, include a message that describes the problem for whoever will have to read it:
```csharp
static void Withdraw(string accountName, decimal amount)
{
  if (accountName is null)
  {
    throw new ArgumentNullException(paramName: nameof(accountName));
  }

  if (amount < 0)
  {
    throw new ArgumentException(
      message: $"{nameof(amount)} cannot be less than zero.");
  }
  ...
}
```
> If a function cannot successfully perform its operation, you should consider that a function failure and report it by throwing an exception.

You **should never** need to write a try-catch statement to catch these usage type errors. You want the application to terminate. These exceptions should cause the programmer who is calling the function to fix their code to prevent the problem. They should be fixed before production deployment. That does not mean that your code does not need to throw usage error type exceptions. _**You should—to force other programmers to call your functions correctly**_!


### Understanding the call stack

The `Main` method will call other methods, that call other methods, and so on, and these methods could be in the current project or in referenced projects and NuGet packages.\
Class library:
```csharp
using static System.Console;

namespace Packt;

public class Calculator
{
  public static void Gamma()
  {
    WriteLine("In Gamma");
    Delta();
  }

  private static void Delta()
  {
    WriteLine("In Delta");
    File.OpenText("bad file path");
  }
}
```
Program:
```csharp
using Packt;

using static System.Console;

WriteLine("In Main");
Alpha();

static void Alpha()
{
  WriteLine("In Alpha");
  Beta();
}
```
The call stack is upside-down. Starting from the bottom, you see:
- The first call is to the `Main` entry point function in the auto-generated Program class. This is where arguments are passed in as a `string` array.
- The second call is to the `Alpha` function.
- The third call is to the `Beta` function.
- The fourth call is to the `Gamma` function.
- The fifth call is to the `Delta` function.\
  This function attempts to open a file by passing a bad file path.\
  This causes an exception to be thrown. Any function with a try-catch statement could catch this exception.\
  If they do not, it is automatically passed up the call stack until it reaches the top, where .NET outputs the exception (and the details of this call stack).


### Where to catch exceptions

Programmers can decide if they want to catch an exception near the failure point, or centralized higher up the call stack. This allows your code to be simplified and standardized. You do not need to handle all types of exceptions at the current point in the call stack.

Sometimes you want to catch an exception, log it, and then rethrow it.\
There are three ways to rethrow an exception inside a catch block:
1. To throw the caught exception with its original call stack, call `throw`.
2. To throw the caught exception as if it was thrown at the current level in the call stack, call `throw` with the caught exception, for example, `throw ex`. This is usually poor practice because you have lost some potentially useful information for debugging.
3. To wrap the caught exception in another exception that can include more information in a message that might help the caller understand the problem, throw a new exception and pass the caught exception as the `innerException` parameter.

If an error could occur when we call the `Gamma` function then we could catch the exception and then perform one of the three techniques of rethrowing an exception:
```csharp
try
{
  Gamma();
}
catch (IOException ex)
{
  LogException(ex);

  // First way.
  throw;

  // Second way.
  throw ex;
  
  // Third way.
  throw new InvalidOperationException(
    message: "Calculation had invalid values. See inner exception for why.",
    innerException: ex);
}
```


### Implementing the tester-doer pattern

The _tester-doer pattern_ can avoid some thrown exceptions (but not eliminate them completely). This pattern uses pairs of functions: one to perform a test, the other to perform an action that would fail if the test is not passed.

.NET implements this pattern itself. For example, before adding an item to a collection by calling the `Add` method, you can test to see if it is read-only, which would cause `Add` to fail and therefore throw an exception.

For example, before withdrawing money from a bank account, you might test that the account is not overdrawn:
```csharp
if (!bankAccount.IsOverdrawn())
{
  bankAccount.Withdraw(amount);
}
```


### Problems with the tester-doer pattern

The tester-doer pattern can add performance overhead, so you can also implement the try pattern, which in effect combines the test and do parts into a single function, as we saw with `TryParse`.

Another problem with the tester-doer pattern occurs when you are using multiple threads.\
In this scenario, one thread could call the test function and it returns okay.\
But then another thread executes that changes the state. Then the original thread continues executing assuming everything is fine, but it is not fine.

If you implement your own try pattern function and it fails, remember to set the `out` parameter to the default value of its type and then return `false`:
```csharp
static bool TryParse(string? input, out Person value)
{
  if (someFailure)
  {
    value = default(Person);
    return false;
  }

  value = new Person() { ... };
  return true;
}
```



## Practice

### Exercise 4.1



### Exercise 4.2
