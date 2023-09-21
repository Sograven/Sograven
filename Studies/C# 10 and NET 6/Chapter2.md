# Chapter 02: Speaking C#

## Table of contents
- [Introducing the c# language](#introducing-the-c-language)
- [Understanding C# grammar and vocabulary](#understanding-c-grammar-and-vocabulary)
- [Working with variables](#working-with-variables)
- [Exploring more about console applications](#exploring-more-about-console-applications)
- [Practice](#practice)
  - [Exercise 2.1](#exercise-21)
  - [Exercise 2.2](#exercise-22)
  - [Exercise 2.3](#exercise-23)



## Introducing the C# language




## Understanding C# grammar and vocabulary




## Working with variables




## Exploring more about console applications




## Practice

### Exercise 2.1

#### What statement can you type in a C# file to discover the compiler and language version?
`#error version`.

#### What are the two types of comments in C#?
One-line comments `/` and mult-line comments `\* *\`.

#### What is the difference between a verbatim string and an interpolated string?
_Verbatim string_ stores literal as is without special symbols. _Interpolated string_ can contain variables and statements.

#### Why should you be careful when using float and double values?
Never check for equality `float` and `double` values. Only compare.

#### How can you determine how many bytes a type like `double` uses in memory?
`sizeof()`.

#### When should you use the var keyword?
When declaring a type.

#### What is the newest way to create an instance of a class like `XmlDocument`?
`XmlDocument document = new();`.

#### Why should you be careful when using the `dynamic` type?
Errors only in runtime.

#### How do you right-align a format string?
`{0, 1:N0}`.

#### What character separates arguments for a console application?
Space.


### Exercise 2.2

| Data type                                                     | Variable type       |
| ------------------------------------------------------------- | ------------------- |
| Telephone number                                              | `string`            |
| Height                                                        | `float` or `double` |
| Age                                                           | `int` or `byte`     |
| Salary                                                        | `decimal`           |
| ISBN                                                          | `string`            |
| Price                                                         | `decimal`           |
| Shipping weight                                               | `float` or `double` |
| Country population                                            | `uint`              |
| The number of stars in the universe                           | `ulong`             |
| Number of employees in each of the small or medium businesses | `ushort`            |



### Exercise 2.3

```csharp
using static System.Console;

WriteLine("------------------------------------------------------------------------------");
WriteLine("{0, 0} {1, 10} {2, 10} {3, 30}", "Type", "Size", "MinValue", "MaxValue");
WriteLine("------------------------------------------------------------------------------");
WriteLine("{0, -10} {1, -6} {2, -30} {3, -25}", "sbyte", sizeof(sbyte), sbyte.MinValue, sbyte.MaxValue);
WriteLine("{0, -10} {1, -6} {2, -30} {3, -25}", "byte", sizeof(byte), byte.MinValue, byte.MaxValue);
WriteLine("{0, -10} {1, -6} {2, -30} {3, -25}", "ushort", sizeof(ushort), ushort.MinValue, ushort.MaxValue);
WriteLine("{0, -10} {1, -6} {2, -30} {3, -25}", "short", sizeof(short), short.MinValue, short.MaxValue);
WriteLine("{0, -10} {1, -6} {2, -30} {3, -25}", "int", sizeof(int), int.MinValue, int.MaxValue);
WriteLine("{0, -10} {1, -6} {2, -30} {3, -25}", "uint", sizeof(uint), uint.MinValue, uint.MaxValue);
WriteLine("{0, -10} {1, -6} {2, -30} {3, -25}", "long", sizeof(long), long.MinValue, long.MaxValue);
WriteLine("{0, -10} {1, -6} {2, -30} {3, -25}", "ulong", sizeof(ulong), ulong.MinValue, ulong.MaxValue);
WriteLine("{0, -10} {1, -6} {2, -30} {3, -25}", "float", sizeof(float), float.MinValue, float.MaxValue);
WriteLine("{0, -10} {1, -6} {2, -30} {3, -25}", "double", sizeof(double), double.MinValue, double.MaxValue);
WriteLine("{0, -10} {1, -6} {2, -30} {3, -25}", "decimal", sizeof(decimal), decimal.MinValue, decimal.MaxValue);
WriteLine("------------------------------------------------------------------------------");
```
