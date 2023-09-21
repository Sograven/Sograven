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
