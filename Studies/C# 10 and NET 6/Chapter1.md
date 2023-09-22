# Chapter 01: Hello, C#! Welcome, .NET!

## Table of contents
- [Understanding .NET](#understanding-net)
  - [Understanding .NET Framework](#understanding-net-framework)
  - [Understanding the Mono, Xamarin and Unity projects](#understanding-the-mono-xamarin-and-unity-projects)
  - [Understanding .NET Core](#understanding-net-core)
  - [Understanding the journey to one .NET](#understanding-the-journey-to-one-net)
  - [Understanding .NET support](#understanding-net-support)
  - [Understanding .NET Runtime and .NET SDK versions](#understanding-net-runtime-and-net-sdk-versions)
  - [Understanding .NET Standard](#understanding-net-standard)
  - [Understanding intermediate language](#understanding-intermediate-language)
- [Practice](#practice)
  - [Exercise 1.1](#exercise-11)




## Understanding .NET

_.NET 6_, _.NET Core_, _.NET Framework_, and _Xamarin_ are related and overlapping platforms for
developers used to build applications and services.

### Understanding .NET Framework

_.NET Framework_ is a development platform that includes a _Common Language Runtime
(**CLR**)_, which manages the execution of code, and a _Base Class Library (*BCL*)_, which provides
a rich library of classes to build applications from.

Microsoft originally designed .NET Framework to have the possibility of being cross-platform,
but Microsoft put their implementation effort into making it work best with Windows.

For .NET Framework 4.0 or later, all of the apps on a computer written for .NET Framework
share the same version of the CLR and libraries stored in the _Global Assembly Cache (**GAC**)_,
which can lead to issues if some of them need a specific version for compatibility.

### Understanding the Mono, Xamarin, and Unity projects

Third parties developed a .NET Framework implementation named the _Mono project_. Mono is
cross-platform, but it fell well behind the official implementation of .NET Framework.

Mono has found a niche as the foundation of the _Xamarin_ mobile platform as well as crossplatform
game development platforms like _Unity_.

### Understanding .NET Core

Microsoft has been working on an effort to decouple .NET from its close ties with Windows. While rewriting .NET Framework to be truly cross-platform, they've taken the opportunity to refactor and remove major parts that are no longer considered core.

This new product was branded _.NET Core_ and includes a cross-platform implementation of the CLR known as _CoreCLR_ and a streamlined BCL known as _CoreFX_.

### Understanding the journey to one .NET

.NET Core has been renamed _.NET_ and the major version number has skipped the number
four to avoid confusion with .NET Framework 4.x. Microsoft plans on annual major version
releases every November, rather like Apple does major version number releases of iOS every
September.

### Understanding .NET support

.NET versions are either _Long Term Support (**LTS**)_ or _**Current**_, as described in the following list:

- **LTS** releases are stable and require fewer updates over their lifetime LTS releases will be supported for 3 years after general availability, or 1 year after the next LTS release ships, whichever is longer.
- **Current** releases include features that may change based on feedback. After a 6-month maintenance period, or 18 months after general availability, the previous minor version will no longer be supported.

### Understanding .NET Runtime and .NET SDK versions

_NET Runtime_ versioning follows semantic versioning, that is, a major increment indicates breaking changes, minor increments indicate new features, and patch increments indicate bug fixes.

_.NET SDK_ versioning does not follow semantic versioning. The major and minor version numbers are tied to the runtime version it is matched with. The patch number follows a convention that indicates the major and minor versions of the SDK.

### Understanding .NET Standard

Microsoft defined _.NET Standard_ – a specification for a set of APIs that all .NET platforms could implement to indicate what level of compatibility they have.

With .NET Standard 2.0 and later, Microsoft made all three platforms converge on a modern minimum standard, which made it much easier for developers to share code between any flavor of .NET.

### Understanding intermediate language

The C# compiler (named _**Roslyn**_) used by the `dotnet` CLI tool converts your C# source code into _intermediate language (**IL**)_ code and stores the IL in an _assembly_ (a DLL or EXE file). IL code statements are like assembly language instructions, which are executed by .NET's virtual machine, known as _**CoreCLR**_.

At runtime, CoreCLR loads the IL code from the assembly, the _just-in-time (**JIT**)_ compiler compiles it into native CPU instructions, and then it is executed by the CPU on your machine

Regardless of which language the source code is written in, for example, C#, Visual Basic, or F#, all .NET applications use IL code for their instructions stored in an assembly.




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
