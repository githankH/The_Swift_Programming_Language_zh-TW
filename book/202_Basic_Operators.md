# 基本運算元
---
運算元是一個特殊的符號或標誌，讓您可以檢查、改變或加總數值。舉例來說，加法運算元 (`+`) 會將兩個數字加總 (例如：`let i=1+2`)。比較複雜一點的例子會包含邏輯運算元 (`&&`表示邏輯上的 AND)(例如 `if enteredDoorCode && passedRetinaScan`就是在說明，如果 `enteredDoorCode` 和(`AND`) `passedRetinaScan` 兩個表示式都為真)，跟漸增運算子(`++i`，這個運算子會把 `i` 現有的值加 `1`)。

Swift 支援大部分標準 C 語言的運算子，並且改進了許多運算子的相容性來減少一些常見的
Swift supports most standard C operators and improves several capabilities to eliminate common coding errors. The assignment operator (`=`) does not return a value, to prevent it from being mistakenly used when the equal to operator (`==`) is intended. Arithmetic operators (`+`, `-`, `*`, `/`, `%` and so forth) detect and disallow value overflow, to avoid unexpected results when working with numbers that become larger or smaller than the allowed value range of the type that stores them. You can opt in to value overflow behavior by using Swift’s overflow operators, as described in [Overflow Operators]().

Unlike C, Swift lets you perform remainder (`%`) calculations on floating-point numbers. Swift also provides two range operators (`a..b` and `a...b`) not found in C, as a shortcut for expressing a range of values.

This chapter describes the common operators in Swift. [Advanced Operators]() covers Swift’s advanced operators, and describes how to define your own custom operators and implement the standard operators for your own custom types.

## Terminology

Operators are unary, binary, or ternary:

- Unary operators operate on a single target (such as `-a`). Unary prefix operators appear immediately before their target (such as `!b`), and unary postfix operators appear immediately after their target (such as `i++`).
- Binary operators operate on two targets (such as `2 + 3`) and are infix because they appear in between their two targets.
- Ternary operators operate on three targets. Like C, Swift has only one ternary operator, the ternary conditional operator (`a ? b : c`).

The values that operators affect are operands. In the expression `1 + 2`, the `+` symbol is a binary operator and its two operands are the values `1` and `2`.

## Assignment Operator

The *assignment operator* (`a = b`) initializes or updates the value of `a` with the value of `b`:

```swift
let b = 10
var a = 5
a = b
// a is now equal to 10
```

If the right side of the assignment is a tuple with multiple values, its elements can be decomposed into multiple constants or variables at once:

```swift
let (x, y) = (1, 2)
// x is equal to 1, and y is equal to 2
```

Unlike the assignment operator in C and Objective-C, the assignment operator in Swift does not itself return a value. The following statement is not valid:

```swift
if x = y {
    // this is not valid, because x = y does not return a value
}
```

This feature prevents the assignment operator (`=`) from being used by accident when the equal to operator (`==`) is actually intended. By making `if x = y` invalid, Swift helps you to avoid these kinds of errors in your code.

## Arithmetic Operators

Swift supports the four standard arithmetic operators for all number types:

- Addition (`+`)
- Subtraction (`-`)
- Multiplication (`*`)
- Division (`/`)

```swift
1 + 2       // equals 3
5 - 3       // equals 2
2 * 3       // equals 6
10.0 / 2.5  // equals 4.0
```

Unlike the arithmetic operators in C and Objective-C, the Swift arithmetic operators do not allow values to overflow by default. You can opt in to value overflow behavior by using Swift’s overflow operators (such as `a &+ b`). See [Overflow Operators]().

The addition operator is also supported for `String` concatenation:

```swift
"hello, " + "world"  // equals "hello, world"
```

Two `Character` values, or one `Character` value and one `String` value, can be added together to make a new `String` value:

```swift
let dog: Character = "🐶"
let cow: Character = "🐮"
let dogCow = dog + cow
// dogCow is equal to "🐶🐮"
```

See also [Concatenating Strings and Characters]().

### Remainder Operator

The *remainder operator* (`a % b`) works out how many multiples of `b` will fit inside `a` and returns the value that is left over (known as the *remainder*).

> **NOTE**
>
> The remainder operator (`%`) is also known as a *modulo operator* in other languages. However, its behavior in Swift for negative numbers means that it is, strictly speaking, a remainder rather than a modulo operation.

Here’s how the remainder operator works. To calculate `9 % 4`, you first work out how many `4`s will fit inside `9`:

![Art/remainderInteger_2x.png](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Art/remainderInteger_2x.png "Art/remainderInteger_2x.png")

You can fit two `4`s inside `9`, and the remainder is `1` (shown in orange).

In Swift, this would be written as:

```swift
9 % 4    // equals 1
```

To determine the answer for `a % b`, the `%` operator calculates the following equation and returns `remainder` as its output:

`a` = (`b` × `some multiplier`) + `remainder`

where `some multiplier` is the largest number of multiples of `b` that will fit inside `a`.

Inserting `9` and `4` into this equation yields:

`9` = (`4` × `2`) + `1`

The same method is applied when calculating the remainder for a negative value of a:

```swift
-9 % 4   // equals -1
```

Inserting `-9` and `4` into the equation yields:

`-9` = (`4` × `-2`) + `-1`

giving a remainder value of `-1`.

The sign of `b` is ignored for negative values of `b`. This means that `a % b` and `a % -b` always give the same answer.

### Floating-Point Remainder Calculations

Unlike the remainder operator in C and Objective-C, Swift’s remainder operator can also operate on floating-point numbers:

```swift
8 % 2.5   // equals 0.5
```

In this example, `8` divided by `2.5` equals `3`, with a remainder of `0.5`, so the remainder operator returns a `Double` value of `0.5`.

![Art/remainderFloat_2x.png](https://developer.apple.com/library/prerelease/ios/documentation/Swift/Conceptual/Swift_Programming_Language/Art/remainderFloat_2x.png "Art/remainderFloat_2x.png")

### Increment and Decrement Operators

Like C, Swift provides an *increment operator* (`++`) and a *decrement operator* (`--`) as a shortcut to increase or decrease the value of a numeric variable by `1`. You can use these operators with variables of any integer or floating-point type.

```swift
var i = 0
++i      // i now equals 1
```

Each time you call `++i`, the value of `i` is increased by `1`. Essentially, `++i` is shorthand for saying `i = i + 1`. Likewise, `--i` can be used as shorthand for `i = i - 1`.

The `++` and `--` symbols can be used as prefix operators or as postfix operators. `++i` and `i++` are both valid ways to increase the value of `i` by `1`. Similarly, `--i` and `i--` are both valid ways to decrease the value of `i` by `1`.

Note that these operators modify `i` and also return a value. If you only want to increment or decrement the value stored in `i`, you can ignore the returned value. However, if you do use the returned value, it will be different based on whether you used the prefix or postfix version of the operator, according to the following rules:

- If the operator is written *before* the variable, it increments the variable *before* returning its value.
- If the operator is written *after* the variable, it increments the variable *after* returning its value.

For example:

```swift
var a = 0
let b = ++a
// a and b are now both equal to 1
let c = a++
// a is now equal to 2, but c has been set to the pre-increment value of 1
```

In the example above, `let b = ++a` increments `a` *before* returning its value. This is why both `a` and `b` are equal to to the new value of `1`.

However, `let c = a++` increments `a` *after* returning its value. This means that `c` gets the old value of `1`, and `a` is then updated to equal `2`.

Unless you need the specific behavior of `i++`, it is recommended that you use `++i` and `--i` in all cases, because they have the typical expected behavior of modifying `i` and returning the result.

### Unary Minus Operator

The sign of a numeric value can be toggled using a prefixed `-`, known as the *unary minus operator*:

```swift
let three = 3
let minusThree = -three       // minusThree equals -3
let plusThree = -minusThree   // plusThree equals 3, or "minus minus three"
```

The unary minus operator (`-`) is prepended directly before the value it operates on, without any white space.

### Unary Plus Operator

The *unary plus operator* (`+`) simply returns the value it operates on, without any change:

```swift
let minusSix = -6
let alsoMinusSix = +minusSix  // alsoMinusSix equals -6
```

Although the unary plus operator doesn’t actually do anything, you can use it to provide symmetry in your code for positive numbers when also using the unary minus operator for negative numbers.

## Compound Assignment Operators

Like C, Swift provides *compound assignment operators* that combine assignment (`=`) with another operation. One example is the *addition assignment operator* (`+=`):

```swift
var a = 1
a += 2
// a is now equal to 3
```

The expression `a += 2` is shorthand for `a = a + 2`. Effectively, the addition and the assignment are combined into one operator that performs both tasks at the same time.

> **NOTE**
>
> The compound assignment operators do not return a value. You cannot write `let b = a += 2`, for example. This behavior is different from the increment and decrement operators mentioned above.

A complete list of compound assignment operators can be found in [Expressions]().

## Comparison Operators

Swift supports all standard C *comparison operators*:

- Equal to (`a == b`)
- Not equal to (`a != b`)
- Greater than (`a > b`)
- Less than (`a < b`)
- Greater than or equal to (`a >= b`)
- Less than or equal to (`a <= b`)

> NOTE
>
> Swift also provides *two identity operators* (`===` and `!==`), which you use to test whether two object references both refer to the same object instance. For more information, see [Classes and Structures]().

Each of the comparison operators returns a `Bool` value to indicate whether or not the statement is true:

```swift
1 == 1   // true, because 1 is equal to 1
2 != 1   // true, because 2 is not equal to 1
2 > 1    // true, because 2 is greater than 1
1 < 2    // true, because 1 is less than 2
1 >= 1   // true, because 1 is greater than or equal to 1
2 <= 1   // false, because 2 is not less than or equal to 1
```

Comparison operators are often used in conditional statements, such as the `if` statement:

```swift
let name = "world"
if name == "world" {
    println("hello, world")
} else {
    println("I'm sorry \(name), but I don't recognize you")
}
// prints "hello, world", because name is indeed equal to "world"
```

For more on the `if` statement, see [Control Flow]().

## Ternary Conditional Operator

The *ternary conditional operator* is a special operator with three parts, which takes the form `question ? answer1 : answer2`. It is a shortcut for evaluating one of two expressions based on whether `question` is true or false. If `question` is true, it evaluates `answer1` and returns its value; otherwise, it evaluates `answer2` and returns its value.

The ternary conditional operator is shorthand for the code below:

```swift
if question {
    answer1
} else {
    answer2
}
```

Here’s an example, which calculates the pixel height for a table row. The row height should be 50 pixels taller than the content height if the row has a header, and 20 pixels taller if the row doesn’t have a header:

```swift
let contentHeight = 40
let hasHeader = true
let rowHeight = contentHeight + (hasHeader ? 50 : 20)
// rowHeight is equal to 90
```

The preceding example is shorthand for the code below:

```swift
let contentHeight = 40
let hasHeader = true
var rowHeight = contentHeight
if hasHeader {
    rowHeight = rowHeight + 50
} else {
    rowHeight = rowHeight + 20
}
// rowHeight is equal to 90
```

The first example’s use of the ternary conditional operator means that `rowHeight` can be set to the correct value on a single line of code. This is more concise than the second example, and removes the need for `rowHeight` to be a variable, because its value does not need to be modified within an `if` statement.

The ternary conditional operator provides an efficient shorthand for deciding which of two expressions to consider. Use the ternary conditional operator with care, however. Its conciseness can lead to hard-to-read code if overused. Avoid combining multiple instances of the ternary conditional operator into one compound statement.

## Range Operators

Swift includes two *range operators*, which are shortcuts for expressing a range of values.

### Closed Range Operator

The *closed range operator* (`a...b`) defines a range that runs from `a` to `b`, and includes the values `a` and `b`.

The closed range operator is useful when iterating over a range in which you want all of the values to be used, such as with a `for`-`in` loop:

```swift
for index in 1...5 {
    println("\(index) times 5 is \(index * 5)")
}
// 1 times 5 is 5
// 2 times 5 is 10
// 3 times 5 is 15
// 4 times 5 is 20
// 5 times 5 is 25
```

For more on `for`-`in` loops, see [Control Flow]().

### Half-Closed Range Operator

The *half-closed range operator* (`a..b`) defines a range that runs from `a` to `b`, but does not include `b`. It is said to be *half-closed* because it contains its first value, but not its final value.

Half-closed ranges are particularly useful when you work with zero-based lists such as arrays, where it is useful to count up to (but not including) the length of the list:

```swift
let names = ["Anna", "Alex", "Brian", "Jack"]
let count = names.count
for i in 0..count {
    println("Person \(i + 1) is called \(names[i])")
}
// Person 1 is called Anna
// Person 2 is called Alex
// Person 3 is called Brian
// Person 4 is called Jack
```

Note that the array contains four items, but `0..count` only counts as far as `3` (the index of the last item in the array), because it is a half-closed range. For more on arrays, see [Arrays]().

## Logical Operators

*Logical operators* modify or combine the Boolean logic values `true` and `false`. Swift supports the three standard logical operators found in C-based languages:

- Logical NOT (`!a`)
- Logical AND (`a && b`)
- Logical OR (`a || b`)

### Logical NOT Operator

The *logical NOT operator* (`!a`) inverts a Boolean value so that `true` becomes `false`, and `false` becomes `true`.

The logical NOT operator is a prefix operator, and appears immediately before the value it operates on, without any white space. It can be read as “not `a`”, as seen in the following example:

```swift
let allowedEntry = false
if !allowedEntry {
    println("ACCESS DENIED")
}
// prints "ACCESS DENIED"
```

The phrase `if !allowedEntry` can be read as “if not allowed entry.” The subsequent line is only executed if “not allowed entry” is true; that is, if `allowedEntry` is `false`.

As in this example, careful choice of Boolean constant and variable names can help to keep code readable and concise, while avoiding double negatives or confusing logic statements.

### Logical AND Operator

The *logical AND operator* (`a && b`) creates logical expressions where both values must be `true` for the overall expression to also be `true`.

If either value is `false`, the overall expression will also be `false`. In fact, if the *first* value is `false`, the second value won’t even be evaluated, because it can’t possibly make the overall expression equate to `true`. This is known as *short-circuit evaluation*.

This example considers two `Bool` values and only allows access if both values are `true`:

```swift
let enteredDoorCode = true
let passedRetinaScan = false
if enteredDoorCode && passedRetinaScan {
    println("Welcome!")
} else {
    println("ACCESS DENIED")
}
// prints "ACCESS DENIED"
```

### Logical OR Operator

The *logical OR operator* (`a || b`) is an infix operator made from two adjacent pipe characters. You use it to create logical expressions in which only one of the two values has to be `true` for the overall expression to be `true`.

Like the Logical AND operator above, the Logical OR operator uses short-circuit evaluation to consider its expressions. If the left side of a Logical OR expression is `true`, the right side is not evaluated, because it cannot change the outcome of the overall expression.

In the example below, the first `Bool` value (`hasDoorKey`) is `false`, but the second value (`knowsOverridePassword`) is `true`. Because one value is `true`, the overall expression also evaluates to `true`, and access is allowed:

```swift
let hasDoorKey = false
let knowsOverridePassword = true
if hasDoorKey || knowsOverridePassword {
    println("Welcome!")
} else {
    println("ACCESS DENIED")
}
// prints "Welcome!"
```

### Combining Logical Operators

You can combine multiple logical operators to create longer compound expressions:

```swift
if enteredDoorCode && passedRetinaScan || hasDoorKey || knowsOverridePassword {
    println("Welcome!")
} else {
    println("ACCESS DENIED")
}
// prints "Welcome!"
```

This example uses multiple `&&` and `||` operators to create a longer compound expression. However, the `&&` and `||` operators still operate on only two values, so this is actually three smaller expressions chained together. It can be read as:

If we’ve entered the correct door code and passed the retina scan; or if we have a valid door key; or if we know the emergency override password, then allow access.

Based on the values of `enteredDoorCode`, `passedRetinaScan`, and `hasDoorKey`, the first two mini-expressions are `false`. However, the emergency override password is known, so the overall compound expression still evaluates to `true`.

### Explicit Parentheses

It is sometimes useful to include parentheses when they are not strictly needed, to make the intention of a complex expression easier to read. In the door access example above, it is useful to add parentheses around the first part of the compound expression to make its intent explicit:

```swift
if (enteredDoorCode && passedRetinaScan) || hasDoorKey || knowsOverridePassword {
    println("Welcome!")
} else {
    println("ACCESS DENIED")
}
// prints "Welcome!"
```

The parentheses make it clear that the first two values are considered as part of a separate possible state in the overall logic. The output of the compound expression doesn’t change, but the overall intention is clearer to the reader. Readability is always preferred over brevity; use parentheses where they help to make your intentions clear.
