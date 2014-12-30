函式(Functions)
---
*Functions* are self-contained chunks of code that perform a specific task. You give a function a name that identifies what it does, and this name is used to “call” the function to perform its task when needed.

*Functions*（函式）本身就是用來執行特定功能的程式碼。每個*FUNCTION*都會給予唯一的命名，在需要的時候，我們透過這個名字來"呼叫"它。 

Swift’s unified function syntax is flexible enough to express anything from a simple C-style function with no parameter names to a complex Objective-C-style method with local and external parameter names for each parameter. Parameters can provide default values to simplify function calls and can be passed as in-out parameters, which modify a passed variable once the function has completed its execution.

Swift unified函式語法具有相當程度的彈性。簡單的像沒有參數的C語言函數，複雜的像具有內部變數和外部變數參數的Object-C函數都可以適用。參數本身有預設值用來簡化函式的呼叫，同時也可以當作傳入參數（pass in）或回傳參數（pass out）使用。 也就是說，當函式結束之後，參數值是會被改變的。

Every function in Swift has a type, consisting of the function’s parameter types and return type. You can use this type like any other type in Swift, which makes it easy to pass functions as parameters to other functions, and to return functions from functions. Functions can also be written within other functions to encapsulate useful functionality within a nested function scope.

Swift中的函式型別是由函式的參數型別和回傳型別所構成的。你可以把這樣的組合當作是一種變數型別，這樣做的好處在於我們把函式當作是普通的參數，可以把函式都做參數傳給其他函式，也可以把函式當作回傳值使用。 Swift函式也支援內嵌函式的寫法，函式的主體可以寫在另一個函式裡面，提供一種封裝的實作方式。 

函式的定義與呼叫  (## Defining and Calling Functions##)

When you define a function, you can optionally define one or more named, typed values that the function takes as input (known as *parameters*), and/or a type of value that the function will pass back as output when it is done (known as its *return type*).

當你要定義函數的時候，你也許要定義一個或多個變數當作是函式的參數，也需要定義回傳值的型別。

Every function has a *function name*, which describes the task that the function performs. To use a function, you “call” that function with its name and pass it input values (known as *arguments*) that match the types of the function’s parameters. A function’s arguments must always be provided in the same order as the function’s parameter list.

每個函式都會有自己的命名，用來表達這個函式的功能或目的。使用的方法是呼叫函式名字和傳入相對應型別的“引數”。注意：傳入引數的順序必須要跟函式中的參數順序一致才可以。

The function in the example below is called `greetingForPerson`, because that’s what it does—it takes a person’s name as input and returns a greeting for that person. To accomplish this, you define one input parameter—a `String` value called `personName`—and a return type of `String`, which will contain a greeting for that person:

以下的例子是叫做 `greetingForPerson`的函式，它做的事情是把傳進來的人名加上歡迎詞然後回傳給呼叫者。為了這個目的，你需要定義一個傳入參數，型別是字串，名字叫做 `personName` ，同時你也需要定義回傳值，型別是字串，回傳值包含人名和歡迎詞。


```swift
func sayHello(personName: String) -> String {
    let greeting = "Hello, " + personName + "!"
    return greeting
}
```

All of this information is rolled up into the function’s *definition*, which is prefixed with the `func` keyword. You indicate the function’s return type with the *return arrow* `->` (a hyphen followed by a right angle bracket), which is followed by the name of the type to return.

函式的定義就是由這些資訊組合的，其中`func`是定義函式的關鍵字。函式的回傳型別則是透過"箭頭"來表達 `->` (一個連字號和右箭頭的組合)，在箭頭後面填的是回傳值的型別定義。


The definition describes what the function does, what it expects to receive, and what it returns when it is done. The definition makes it easy for the function to be called elsewhere in your code in a clear and unambiguous way:

這個定義描述了 1)函式的用途 2)函式的預期輸入，以及函式結束的回傳值。這種定義的方式讓我們在程式碼中的其他位置呼叫函式變得簡單而且清楚。

```swift
println(sayHello("Anna"))
// prints "Hello, Anna!"
println(sayHello("Brian"))
// prints "Hello, Brian!"
```

You call the `sayHello` function by passing it a `String` argument value in parentheses, such as `sayHello("Anna")`. Because the function returns a `String` value, `sayHello` can be wrapped in a call to the `println` function to print that string and see its return value, as shown above.

你可以在呼叫 `sayHello` 函式的時候，在括號內傳入 `String` 型別的變數，例如 `sayHello("Anna")`。由於 `sayHello` 是回傳字串型別的資料，它也可以直接內嵌在  `println` 函式中。結果如上，螢幕會上印出 `sayHello` 的回傳字串。

The body of the `sayHello` function starts by defining a new `String` constant called `greeting` and setting it to a simple greeting message for `personName`. This greeting is then passed back out of the function using the `return` keyword. As soon as `return greeting` is called, the function finishes its execution and returns the current value of `greeting`.

`sayHello` 的函式主體是定義一個字串變數 `greeting` 開始，同時把傳遞進來的 `personName` 加上一句歡迎詞設定給這個 `greeting` 這個變數。我們藉由 `return` 這個關鍵字把設定過的 `greeting` 變數值回傳給呼叫者。也就是說，當 `return greeting` 被執行，這個函式就會結束執行並且回傳`greeting`目前的值。

You can call the `sayHello` function multiple times with different input values. The example above shows what happens if it is called with an input value of `"Anna"`, and an input value of `"Brian"`. The function returns a tailored greeting in each case.

每次呼叫 `sayHello` 函式都可以傳入不同的參數。以上的例子說明當函式的參數分別傳入 `"Anna"` 和 `"Brian"` 會發生什麼事。

To simplify the body of this function, combine the message creation and the return statement into one line:

如果需要簡化函式主體的長度，我們可以把回傳值跟預先建立好的變數合併成一行，例子如下：

```swift
func sayHelloAgain(personName: String) -> String {
    return "Hello again, " + personName + "!"
}
println(sayHelloAgain("Anna"))
// prints "Hello again, Anna!"
```

函式的參數和回傳值（## Function Parameters and Return Values##）

Function parameters and return values are extremely flexible in Swift. You can define anything from a simple utility function with a single unnamed parameter to a complex function with expressive parameter names and different parameter options.

在Swift中，函式的參數和回傳值是相當有彈性的。從只有一個未命名參數的單一功能函式，到複雜功能函式中具有表達意義的參數名以及不同選項的參數，這些都是你可以定義的。

多個傳入參數（### Multiple Input Parameters###）

Functions can have multiple input parameters, which are written within the function’s parentheses, separated by commas.

函式可以有多個傳數參數，參數的位置是放在括號之內，由逗號隔開。

This function takes a start and an end index for a half-open range, and works out how many elements the range contains:

以下的例子是有兩個傳入變數，一組半有效區間的起始索引和結束索引。函式目的是計算這個區間內有多少個有效元素：
```swift
func halfOpenRangeLength(start: Int, end: Int) -> Int {
    return end - start
}
println(halfOpenRangeLength(1, 10))
// prints "9"
```

無輸入參數函式（### Functions Without Parameters###）

Functions are not required to define input parameters. Here’s a function with no input parameters, which always returns the same `String` message whenever it is called:

函式不需要定義輸入參數。以下的例子就是沒有輸入參數的函式，當這個函式被呼叫的時候，永遠都回傳固定的 `String` 訊息：

```swift
func sayHelloWorld() -> String {
    return "hello, world"
}
println(sayHelloWorld())
// prints "hello, world"
```

The function definition still needs parentheses after the function’s name, even though it does not take any parameters. The function name is also followed by an empty pair of parentheses when the function is called.

然而，即使不需要定義輸入參數，函式的命名仍然需要用括號來結尾。函式的呼叫也需要在名字加上一對括號。

不具回傳值的函式（### Functions Without Return Values###）

Functions are not required to define a return type. Here’s a version of the `sayHello` function, called `waveGoodbye`, which prints its own `String` value rather than returning it:

函式也不需要定義回傳值。以下的例子是一個類似　`sayHello` 的函式 －`sayGoodbye`，它會印出函式內的字串變數而不是回傳該字串變數。

```swift
func sayGoodbye(personName: String) {
    println("Goodbye, \(personName)!")
}
sayGoodbye("Dave")
// prints "Goodbye, Dave!"
```

Because it does not need to return a value, the function’s definition does not include the return arrow (`->`) or a return type.

由於函式並沒有回傳值，因此函式定義就不需要回傳箭頭（`->`）或者是回傳值的型別。
> **Note**
>
> Strictly speaking, the `sayGoodbye` function *does* still return a value, even though no return value is defined. Functions without a defined return type return a special value of type `Void`. This is simply an empty tuple, in effect a tuple with zero elements, which can be written as `()`.
>
>嚴格來說， `sayGoodbye` 還是有回傳值，即使在函式中沒有明確定義它。沒有定義回傳型別的函式還是會回傳 `Void` 型別的特殊值。簡單的解釋， `Void` 是一個空集合，一個沒有包含任何元素的集合。

The return value of a function can be ignored when it is called:

函式的回傳值可以被忽略

```swift
func printAndCount(stringToPrint: String) -> Int {
    println(stringToPrint)
    return countElements(stringToPrint)
}
func printWithoutCounting(stringToPrint: String) {
    printAndCount(stringToPrint)
}
printAndCount("hello, world")
// prints "hello, world" and returns a value of 12
printWithoutCounting("hello, world")
// prints "hello, world" but does not return a value
```

The first function, `printAndCount`, prints a string, and then returns its character count as an `Int`. The second function, `printWithoutCounting`, calls the first function, but ignores its return value. When the second function is called, the message is still printed by the first function, but the returned value is not used.

第一個函式 `printAndCount`，印出輸入的字串並且計算總共有幾個字元之後回傳一個 `Int` 型別的回傳值。第二個函式 `printWithoutCounting`，會呼叫第一個函式但是會忽略函式的回傳值。當第二個函式被呼叫的時候，輸入的字串依舊會被第一個函式印出來，但是第一個函式的回傳值並不會被使用。

> **Note**
>
> Return values can be ignored, but a function that says it will return a value must always do so. A function with a defined return type cannot allow control to fall out of the bottom of the function without returning a value, and attempting to do so will result in a compile-time error.
>
>回傳值可以被忽略，但是函式有定義回傳值那就必須要有〝回傳值〞。如果函式有回傳值的定義，那麼在函式主體中的結束部分就不能沒有回傳值，要是你試圖這麼做的話，在COMPILER-TIME的時候會報錯。


多個回傳值的函式　（### Functions with Multiple Return Values###）

You can use a tuple type as the return type for a function to return multiple values as part of one compound return value.
你可以把集合型別的變數都做函式的回值，也就是說函式可以把多個變數的回傳值視為〝一個〞複合變數的回傳值。

The example below defines a function called `count`, which counts the number of vowels, consonants, and other characters in a string, based on the standard set of vowels and consonants used in American English:

以下的例子定義一個叫做 `count` 的函式，它的功能是用來計算傳入的字串中有幾個母音字元，子音字元，以及除了母音和子音之外的其他字元個數。
計算的依據是參考美式英文中定義的母音跟子音：

```swift
func count(string: String) -> (vowels: Int, consonants: Int, others: Int) {
    var vowels = 0, consonants = 0, others = 0
    for character in string {
        switch String(character).lowercaseString {
        case "a", "e", "i", "o", "u":
            ++vowels
        case "b", "c", "d", "f", "g", "h", "j", "k", "l", "m",
        "n", "p", "q", "r", "s", "t", "v", "w", "x", "y", "z":
            ++consonants
        default:
            ++others
        }
    }
    return (vowels, consonants, others)
}
```

You can use this `count` function to count the characters in an arbitrary string, and to retrieve the counted totals as a tuple of three named `Int` values:

你可以使用 `count` 函式來計算任意字串中所包含的字元，對於集合中的個別元素可以用整數型別去存取。

```swift
let total = count("some arbitrary string!")
println("\(total.vowels) vowels and \(total.consonants) consonants")
// prints "6 vowels and 13 consonants"
```

**Note** that the tuple’s members do not need to be named at the point that the tuple is returned from the function, because their names are already specified as part of the function’s return type.

**Note** 集合中的成員不需要在函式回傳的時候去命名，因為它們的命名已經在函式宣告的時候已經定義過了。

函式的參數命名（## Function Parameter Names##）

All of the above functions define *parameter names* for their parameters:

以上所提到的函式都需要替他們的變數定義 `*變數名*`。

```swift
func someFunction(parameterName: Int) {
    // function body goes here, and can use parameterName
    // to refer to the argument value for that parameter
}
```

However, these parameter names are only used within the body of the function itself, and cannot be used when calling the function. These kinds of parameter names are known as *local parameter names*, because they are only available for use within the function’s body.

然而，這些變數名只能在函數主體中使用，不能在函數呼叫的時候被使用。這種變數就是所謂的`*局部變數(local parameter names)*`，因為這些變數只能在函式內部使用而以。

外部變數命名（### External Parameter Names###）

Sometimes it’s useful to name each parameter when you *call* a function, to indicate the purpose of each argument you pass to the function.

If you want users of your function to provide parameter names when they call your function, define an *external parameter name* for each parameter, in addition to the local parameter name. You write an external parameter name before the local parameter name it supports, separated by a space:

```swift
func someFunction(externalParameterName localParameterName: Int) {
    // function body goes here, and can use localParameterName
    // to refer to the argument value for that parameter
}
```

> **Note**
>
> If you provide an external parameter name for a parameter, that external name must *always* be used when calling the function.

As an example, consider the following function, which joins two strings by inserting a third “joiner” string between them:

```swift
func join(s1: String, s2: String, joiner: String) -> String {
    return s1 + joiner + s2
}
```

When you call this function, the purpose of the three strings that you pass to the function is unclear:

```swift
join("hello", "world", ", ")
// returns "hello, world"
```

To make the purpose of these `String` values clearer, define external parameter names for each `join` function parameter:

```swift
func join(string s1: String, toString s2: String, withJoiner joiner: String)
    -> String {
        return s1 + joiner + s2
}
```

In this version of the `join` function, the first parameter has an external name of `string` and a local name of `s1`; the second parameter has an external name of `toString` and a local name of `s2`; and the third parameter has an external name of `withJoiner` and a local name of `joiner`.

You can now use these external parameter names to call the function in a clear and unambiguous way:

```swift
join(string: "hello", toString: "world", withJoiner: ", ")
// returns "hello, world"
```

The use of external parameter names enables this second version of the `join` function to be called in an expressive, sentence-like manner by users of the function, while still providing a function body that is readable and clear in intent.

> **Note**
>
> Consider using external parameter names whenever the purpose of a function’s arguments would be unclear to someone reading your code for the first time. You do not need to specify external parameter names if the purpose of each parameter is clear and unambiguous when the function is called.

### Shorthand External Parameter Names###

If you want to provide an external parameter name for a function parameter, and the local parameter name is already an appropriate name to use, you do not need to write the same name twice for that parameter. Instead, write the name once, and prefix the name with a hash symbol (`#`). This tells Swift to use that name as both the local parameter name and the external parameter name.

This example defines a function called `containsCharacter`, which defines external parameter names for both of its parameters by placing a hash symbol before their local parameter names:

```swift
func containsCharacter(#string: String, #characterToFind: Character) -> Bool {
    for character in string {
        if character == characterToFind {
            return true
        }
    }
    return false
}
```

This function’s choice of parameter names makes for a clear, readable function body, while also enabling the function to be called without ambiguity:

```swift
let containsAVee = containsCharacter(string: "aardvark", characterToFind: "v")
// containsAVee equals true, because "aardvark" contains a "v"
```
### Default Parameter Values###

You can define a *default value* for any parameter as part of a function’s definition. If a default value is defined, you can omit that parameter when calling the function.

> **Note**
>
> Place parameters with default values at the end of a function’s parameter list. This ensures that all calls to the function use the same order for their non-default arguments, and makes it clear that the same function is being called in each case.

Here’s a version of the `join` function from earlier, which provides a default value for its `joiner` parameter:

```swift
func join(string s1: String, toString s2: String,
    withJoiner joiner: String = " ") -> String {
        return s1 + joiner + s2
}
```

If a string value for `joiner` is provided when the `join` function is called, that string value is used to join the two strings together, as before:

```swift
join(string: "hello", toString: "world", withJoiner: "-")
// returns "hello-world"
```

However, if no value of `joiner` is provided when the function is called, the default value of a single space (`" "`) is used instead:

```swift
join(string: "hello", toString: "world")
// returns "hello world"
```

### External Names for Parameters with Default Values###

In most cases, it is useful to provide (and therefore require) an external name for any parameter with a default value. This ensures that the argument for that parameter is clear in purpose if a value is provided when the function is called.

To make this process easier, Swift provides an automatic external name for any defaulted parameter you define, if you do not provide an external name yourself. The automatic external name is the same as the local name, as if you had written a hash symbol before the local name in your code.

Here’s a version of the `join` function from earlier, which does not provide external names for any of its parameters, but still provides a default value for its `joiner` parameter:

```swift
func join(s1: String, s2: String, joiner: String = " ") -> String {
    return s1 + joiner + s2
}
```

In this case, Swift automatically provides an external parameter name of `joiner` for the defaulted parameter. The external name must therefore be provided when calling the function, making the parameter’s purpose clear and unambiguous:

```swift
join("hello", "world", joiner: "-")
// returns "hello-world"
```

> **Note**
>
> You can opt out of this behavior by writing an underscore (`_`) instead of an explicit external name when you define the parameter. However, external names for defaulted parameters are always preferred where appropriate.

## Variadic Parameters##

A *variadic parameter* accepts zero or more values of a specified type. You use a variadic parameter to specify that the parameter can be passed a varying number of input values when the function is called. Write variadic parameters by inserting three period characters (`...`) after the parameter’s type name.

The values passed to a variadic parameter are made available within the function’s body as an array of the appropriate type. For example, a variadic parameter with a name of `numbers` and a type of `Double...` is made available within the function’s body as a constant array called `numbers` of type `Double[]`.

The example below calculates the *arithmetic mean* (also known as the *average*) for a list of numbers of any length:

```swift
func arithmeticMean(numbers: Double...) -> Double {
    var total: Double = 0
    for number in numbers {
        total += number
    }
    return total / Double(numbers.count)
}
arithmeticMean(1, 2, 3, 4, 5)
// returns 3.0, which is the arithmetic mean of these five numbers
arithmeticMean(3, 8, 19)
// returns 10.0, which is the arithmetic mean of these three numbers
```

> **Note**
>
> A function may have at most one variadic parameter, and it must always appear last in the parameter list, to avoid ambiguity when calling the function with multiple parameters.
>
> If your function has one or more parameters with a default value, and also has a variadic parameter, place the variadic parameter after all the defaulted parameters at the very end of the list.

### Constant and Variable Parameters###

Function parameters are constants by default. Trying to change the value of a function parameter from within the body of that function results in a compile-time error. This means that you can’t change the value of a parameter by mistake.

However, sometimes it is useful for a function to have a *variable* copy of a parameter’s value to work with. You can avoid defining a new variable yourself within the function by specifying one or more parameters as *variable parameters* instead. Variable parameters are available as variables rather than as constants, and give a new modifiable copy of the parameter’s value for your function to work with.

Define variable parameters by prefixing the parameter name with the keyword `var`:

```swift
func alignRight(var string: String, count: Int, pad: Character) -> String {
    let amountToPad = count - countElements(string)
    for _ in 1...amountToPad {
        string = pad + string
    }
    return string
}
let originalString = "hello"
let paddedString = alignRight(originalString, 10, "-")
// paddedString is equal to "-----hello"
// originalString is still equal to "hello"
```

This example defines a new function called `alignRight`, which aligns an input string to the right edge of a longer output string. Any space on the left is filled with a specified padding character. In this example, the string `"hello"` is converted to the string `"-----hello"`.

The `alignRight` function defines the input parameter `string` to be a variable parameter. This means that `string` is now available as a local variable, initialized with the passed-in string value, and can be manipulated within the body of the function.

The function starts by working out how many characters need to be added to the left of `string` in order to right-align it within the overall string. This value is stored in a local constant called `amountToPad`. The function then adds `amountToPad` copies of the `pad` character to the left of the existing string and returns the result. It uses the `string` variable parameter for all its string manipulation.

> **Note**
>
> The changes you make to a variable parameter do not persist beyond the end of each call to the function, and are not visible outside the function’s body. The variable parameter only exists for the lifetime of that function call.

### In-Out Parameters###

Variable parameters, as described above, can only be changed within the function itself. If you want a function to modify a parameter’s value, and you want those changes to persist after the function call has ended, define that parameter as an *in-out parameter* instead.

You write an in-out parameter by placing the `inout` keyword at the start of its parameter definition. An in-out parameter has a value that is passed *in* to the function, is modified by the function, and is passed back *out* of the function to replace the original value.

You can only pass a variable as the argument for an in-out parameter. You cannot pass a constant or a literal value as the argument, because constants and literals cannot be modified. You place an ampersand (`&amp;`) directly before a variable’s name when you pass it as an argument to an inout parameter, to indicate that it can be modified by the function.

> **Note**
>
> In-out parameters cannot have default values, and variadic parameters cannot be marked as `inout`. If you mark a parameter as `inout`, it cannot also be marked as `var` or `let`.

Here’s an example of a function called `swapTwoInts`, which has two in-out integer parameters called `a` and `b`:

```swift
func swapTwoInts(inout a: Int, inout b: Int) {
    let temporaryA = a
    a = b
    b = temporaryA
}
```

The `swapTwoInts` function simply swaps the value of `b` into `a`, and the value of `a` into `b`. The function performs this swap by storing the value of `a` in a temporary constant called `temporaryA`, assigning the value of `b` to `a`, and then assigning `temporaryA` to `b`.

You can call the `swapTwoInts` function with two variables of type `Int` to swap their values. **Note** that the names of `someInt` and `anotherInt` are prefixed with an ampersand when they are passed to the `swapTwoInts` function:

```swift
var someInt = 3
var anotherInt = 107
swapTwoInts(&someInt, &anotherInt)
println("someInt is now \(someInt), and anotherInt is now \(anotherInt)")
```

The example above shows that the original values of `someInt` and `anotherInt` are modified by the `swapTwoInts` function, even though they were originally defined outside of the function.

> **Note**
>
> In-out parameters are not the same as returning a value from a function. The `swapTwoInts` example above does not define a return type or return a value, but it still modifies the values of `someInt` and `anotherInt`. In-out parameters are an alternative way for a function to have an effect outside of the scope of its function body.

## Function Types##

Every function has a specific *function type*, made up of the parameter types and the return type of the function.

For example:

```swift
func addTwoInts(a: Int, b: Int) -> Int {
    return a + b
}
func multiplyTwoInts(a: Int, b: Int) -> Int {
    return a * b
}
```

This example defines two simple mathematical functions called `addTwoInts` and `multiplyTwoInts`. These functions each take two `Int` values, and return an `Int` value, which is the result of performing an appropriate mathematical operation.

The type of both of these functions is `(Int, Int) -> Int`. This can be read as:

“A function type that has two parameters, both of type `Int`, and that returns a value of type `Int`.”

Here’s another example, for a function with no parameters or return value:

```swift
func printHelloWorld() {
    println("hello, world")
}
```

The type of this function is `() -> ()`, or “a function that has no parameters, and returns `Void`.” Functions that don’t specify a return value always return `Void`, which is equivalent to an empty tuple in Swift, shown as `()`.

### Using Function Types###

You use function types just like any other types in Swift. For example, you can define a constant or variable to be of a function type and assign an appropriate function to that variable:

```swift
var mathFunction: (Int, Int) -> Int = addTwoInts
```

This can be read as:

“Define a variable called `mathFunction`, which has a type of ‘a function that takes two `Int` values, and returns an `Int` value.’ Set this new variable to refer to the function called `addTwoInts`.”

The `addTwoInts` function has the same type as the `mathFunction` variable, and so this assignment is allowed by Swift’s type-checker.

You can now call the assigned function with the name `mathFunction`:

```swift
println("Result: \(mathFunction(2, 3))")
// prints "Result: 5"
```

A different function with the same matching type can be assigned to the same variable, in the same way as for non-function types:

```swift
mathFunction = multiplyTwoInts
println("Result: \(mathFunction(2, 3))")
// prints "Result: 6"
```

As with any other type, you can leave it to Swift to infer the function type when you assign a function to a constant or variable:

```swift
let anotherMathFunction = addTwoInts
// anotherMathFunction is inferred to be of type (Int, Int) -> Int
```

### Function Types as Parameter Types###

You can use a function type such as `(Int, Int) -> Int` as a parameter type for another function. This enables you to leave some aspects of a function’s implementation for the function’s caller to provide when the function is called.

Here’s an example to print the results of the math functions from above:

```swift
func printMathResult(mathFunction: (Int, Int) -> Int, a: Int, b: Int) {
    println("Result: \(mathFunction(a, b))")
}
printMathResult(addTwoInts, 3, 5)
// prints "Result: 8"
```

This example defines a function called `printMathResult`, which has three parameters. The first parameter is called `mathFunction`, and is of type `(Int, Int) -> Int`. You can pass any function of that type as the argument for this first parameter. The second and third parameters are called `a` and `b`, and are both of type `Int`. These are used as the two input values for the provided math function.

When `printMathResult` is called, it is passed the `addTwoInts` function, and the integer values `3` and `5`. It calls the provided function with the values `3` and `5`, and prints the result of `8`.

The role of `printMathResult` is to print the result of a call to a math function of an appropriate type. It doesn’t matter what that function’s implementation actually does—it matters only that the function is of the correct type. This enables `printMathResult` to hand off some of its functionality to the caller of the function in a type-safe way.

### Function Types as Return Types###

You can use a function type as the return type of another function. You do this by writing a complete function type immediately after the return arrow (`->`) of the returning function.

The next example defines two simple functions called `stepForward` and `stepBackward`. The `stepForward` function returns a value one more than its input value, and the `stepBackward` function returns a value one less than its input value. Both functions have a type of `(Int) -> Int`:

```swift
func stepForward(input: Int) -> Int {
    return input + 1
}
func stepBackward(input: Int) -> Int {
    return input - 1
}
```

Here’s a function called `chooseStepFunction`, whose return type is “a function of type `(Int) -> Int`”. `chooseStepFunction` returns the `stepForward` function or the `stepBackward` function based on a Boolean parameter called `backwards`:

```swift
func chooseStepFunction(backwards: Bool) -> (Int) -> Int {
    return backwards ? stepBackward : stepForward
}
```

You can now use `chooseStepFunction` to obtain a function that will step in one direction or the other:

```swift
var currentValue = 3
let moveNearerToZero = chooseStepFunction(currentValue > 0)
// moveNearerToZero now refers to the stepBackward() function
```

The preceding example works out whether a positive or negative step is needed to move a variable called `currentValue` progressively closer to zero. `currentValue` has an initial value of `3`, which means that `currentValue > 0` returns `true`, causing `chooseStepFunction` to return the `stepBackward` function. A reference to the returned function is stored in a constant called `moveNearerToZero`.

Now that `moveNearerToZero` refers to the correct function, it can be used to count to zero:

```swift
println("Counting to zero:")
// Counting to zero:
while currentValue != 0 {
    println("\(currentValue)... ")
    currentValue = moveNearerToZero(currentValue)
}
println("zero!")
// 3...
// 2...
// 1...
// zero!
```

## Nested Functions##

All of the functions you have encountered so far in this chapter have been examples of *global functions*, which are defined at a global scope. You can also define functions inside the bodies of other functions, known as *nested functions*.

Nested functions are hidden from the outside world by default, but can still be called and used by their enclosing function. An enclosing function can also return one of its nested functions to allow the nested function to be used in another scope.

You can rewrite the `chooseStepFunction` example above to use and return nested functions:

```swift
func chooseStepFunction(backwards: Bool) -> (Int) -> Int {
    func stepForward(input: Int) -> Int { return input + 1 }
    func stepBackward(input: Int) -> Int { return input - 1 }
    return backwards ? stepBackward : stepForward
}
var currentValue = -4
let moveNearerToZero = chooseStepFunction(currentValue > 0)
// moveNearerToZero now refers to the nested stepForward() function
while currentValue != 0 {
    println("\(currentValue)... ")
    currentValue = moveNearerToZero(currentValue)
}
println("zero!")
// -4...
// -3...
// -2...
// -1...
// zero!
```
