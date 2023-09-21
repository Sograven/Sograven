# Chapter 01: Hello, C#! Welcome, .NET!

## Table of contents
- [Understanding .NET](#understanding-net)
- [Practice](#practice)
  - [Exercise 1.1](#exercise-11)


## Understanding .NET




## Practice

### Exercise 1.1

#### Is Visual Studio 2022 better than Visual Studio Code?
No, it doesn't. These IDEs was developed for different purposes and have own pros and cons.

#### Is NET 6 better than .NET Framework?
In mostly, yes. _.NET framework_ is legacy framework and using it has only one purpose - maintain
legacy applications. _NET 6_ is modern framework with higher perfomance and new features.
Modern frameworks always have precedence over legacy frameworks. 

#### What is .NET Standard and why is it still important?
_NET Standard_ is a unification system for all NET frameworks.
NET Standard indicates which versions of language, compiler and runtime have full compatibility.

#### Why can a programmer use different languages, for example, C# and F#, to write applications that run on .NET?
C# and F# have compiling to _Intermediate Language (**IL**)_,
which is general for both languages, and then IL runs on _Common Language Runtime (**CLR**)_.

#### What is the name of the entry point method of a .NET console application and how should it be declared?
~~The entry point method of a console application is "Main()" method. It can be declared
with command-line arguments "static int Main(string[] args)" and without these "static void Main()".~~\
**Correct**: _The entry point of a .NET console application is the `Main()` method. An optional
string array for command-line arguments and a return type of `int` are recommended,
but they are not required._

#### What is a top-level program and how do you access any command-line arguments?
Top-level program is simple representation of `Main()` method without class and method body.
Command-line arguments can be accessed via `args` array.

#### What do you type at the prompt to build and execute C# source code?
`dotnet run`

#### What are some benefits of using .NET Interactive Notebooks to write C# code?
There is no need to create full application for small pieces of code, faster run and supports
format-rich text.

#### Where would you look for help for a C# keyword?
Microsoft Docs [C# Refernce](https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/).

#### Where would you look for solutions to common programming problems?
[StackOverflow](https://stackoverflow.com/).
