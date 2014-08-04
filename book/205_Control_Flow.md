# 控制流程
---
Swift提供所有類似C中常見的控制流程結構；其中包括了處理複數次工作的`for`及`while`迴圈，與根據特定的條件來執行不同的程式分支的`if`與`switch`述句(statements)，以及像是`break`跟`continue`這種能將流程轉移至程式中的其他位置的述句。

除了C語言提供的傳統`for`-`condition`-`increment`迴圈外，Swift增加了`for`-`in`迴圈來讓陣列、字典(dictionaries)、區間(ranges)、字串(strings)及其他序列(sequences)的迭代更加容易。

而Swift裡的`switch`述句也比C語言所提供的更加強大。 Swift裡的`switch`述句裡的case不會”跨越“到下個case，避免一般在C語言因為少寫`break`敘述句而造成的錯誤。Case可以用不同的模式來比對，包括區間、比對, 多元組(tuples)以及轉至特定型別(casts to a specific type)。在`switch`的case中符合的值在case的範圍可以被當作是暫時的常數或變數來使用而且在各個case中複雜的比對條件可以用`where`子句來表示。

## For迴圈

For迴圈是用來將一組程式碼重複執行特定次數。Swift提供兩種`for`迴圈：

- `for`-`in`針對區間、序列、集合(collection)或progression裡的各個項目執行程式。 

- `for`-`condition`-`increment`重複執行程式直到符合特定的條件，通常是在每次迴圈結束時遞增的計數器。

### For-In

你可以使用`for`-`in`迴圈來重複處理集合裡的項目；像是ranges裡的數字、陣列裡的元素或是字串裡的字元。

這個例子印出了前幾個五的倍數。

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

藉著使用封閉區間運算子 (`...`)使得這個集合內的項目也就是包括1到5之間的數字都可以取用。`index`的值被設定為區間內的第一個數字 (`1`)且迴圈內的述句會被執行。在這個例子裡，迴圈內只包含一個述句；它會印出目前`index`的值的5的倍數。在這個述句執行完畢後，`index`的值會被更新為第二個數字(`2`)，並且再次呼叫`println`這個函式。整個過程會一直持續進行直到抵達這個區間的結尾。

在上述的範例中，`index`這個常數的值會在每次迴圈開始時自動被設定。因此，不需要宣告就可以使用它。它在迴圈的宣告中就被簡單的宣告了，而不需要另外使用關鍵字`let`來宣告。

> **備註**
> 
> `index`這個常數只存在於迴圈的範圍之內。如果你想要在迴圈結束之後查看`index`的值或你想把這個值當作變數而不是常數來使用的話，你必須在迴圈開始前先自行宣告。

如果你不需要使用到區間裡的值，你可以藉著在原來變數名稱的位置使用底線來忽略這些值。

```swift
let base = 3
let power = 10
var answer = 1
for _ in 1...power {
    answer *= base
}
println("\(base) to the power of \(power) is \(answer)")
// prints "3 to the power of 10 is 59049"
```

這個例子計算了一個數字的某次方(以這個例子來說是3的10次方)。它利用了從0開始到9結束的半封閉區間，讓乘積從1(也就是3的0次方)開始乘3乘了十次。
整個計算過程中不需要知道每次迴圈的計數器的值—它只需要重複計算正確的次數即可。底線`_`(在原來變數名稱的位置使用)使得每次的值都被忽略而且在每次的迴圈裡也不能存取該值。

針對陣列使用`for`-`in`迴圈來一一處理陣列內的元素：

```swift
let names = ["Anna", "Alex", "Brian", "Jack"]
for name in names {
    println("Hello, \(name)!")
}
// Hello, Anna!
// Hello, Alex!
// Hello, Brian!
// Hello, Jack!
```

你也可以重複存取字典內的key-value。當你迭代處理字典時，他會以`(key, value)` 的tuple形式回傳各個項目；你可以明確的命名`(key, value)` tuple裡的成員給`for`-`in` 迴圈內使用。在這裡，這個字典的鍵被分解到一個叫做`animalName`的常數而值被分解到一個叫做`legCount`的常數：

```swift
let numberOfLegs = ["spider": 8, "ant": 6, "cat": 4]
for (animalName, legCount) in numberOfLegs {
    println("\(animalName)s have \(legCount) legs")
}
// spiders have 8 legs
// ants have 6 legs
// cats have 4 legs
```

字典裡的項目不必然會照著新增的順序迭代。字典的內容在設計上就是無序的，在迭代處理它們時不能夠保證取回的順序。要了解更多與陣列跟字典的資訊請看「集合類型」(204_Collection_Types.html "Collection Types").)

除了陣列跟字典之外，你也可以使用for-in迴圈來迭代處理字串中的字元。

```swift
for character in "Hello" {
    println(character)
}
// H
// e
// l
// l
// o
```

### For-Condition-Increment

除了`for`-`in`迴圈外，Swift還支援傳統C語言的條件遞增型的 `for` 迴圈：

```swift
for var index = 0; index < 3; ++index {
    println("index is \(index)")
}
// index is 0
// index is 1
// index is 2
```

以下是這種for迴圈的一般形式：

```swift
for initialization; condition; increment {
    statements
}
```

就像Ｃ一樣，分號把迴圈的定義區分為三個部分。然而跟Ｃ不一樣的地方是，Swift不需要把“初始化; 條件; 遞增”的區塊用小括號括起來。

這個迴圈的執行方式如下：

- 當第一次進到這個迴圈時，初始化表達式(*initialization expression*)會被執行一次，用以建立任何在這個迴圈所需要的常數或變數。
- 執行條件表達式(*condition expression*) 。如果執行結果是假(`false`)則迴圈結束；然後會繼續執行迴圈的右大括號  (`}`)之後的程式碼。 如果執行結果為真(`true`), 則會繼續執行括號內的述句。
- 在所有的述句都執行完後，遞增表達式(*increment expression*) 會被執行。它可能會增加或減少計數器的值，或者根據某個述句的回傳值來幫計數器建立新的值。 在遞增表達式執行完後，回到第二步驟；並且再一次執行條件表達式。

上面所提到的迴圈的格式與執行步驟，可以以下的方式較為簡易(而且等價)的格式來表達：

```swift
initialization
while condition {
    statements
    increment
}
```

在初始化表達式裡宣告的常數與變數(如`var index = 0`)只在`for` 迴圈自己的範圍內有效。為了在迴圈結束後可以取得`index`最後的數值，你必須在迴圈開始之前就宣告`index`：

```swift
var index: Int
for index = 0; index < 3; ++index {
    println("index is \(index)")
}
// index is 0
// index is 1
// index is 2
println("The loop statements were executed \(index) times")
// prints "The loop statements were executed 3 times"
```

附帶一提，這個迴圈結束時`index`最後的值會是`3`而不是 `2`。最後一次的遞增表達式`++index`被呼叫時，它設定`index`為`3`；這使得`index < 3`的結果為`false`，結束這個迴圈。

## While迴圈

`while`迴圈重複執行述句直到條件變成 `false`。這種類型的迴圈最適合用在在開始執行之前不知道要重覆執行幾次的狀況。Swift提供兩種`while`迴圈：

- `while` 會在每次迴圈的開始時執行條件的判斷。
- `do`-`while` 會在每次迴圈的結束時執行條件的判斷。

### While

`while`會從執行條件判斷開始。如果結果為`true`，數據會被重複執行直到條件為`false`。

以下為常見的`while` 迴圈格式：

```swift
while condition {
    statements
}
```

這個例子是遊玩一個簡單的遊戲：蛇梯棋(*Snakes and Ladders*) (也叫做*Chutes and Ladders*):

![Art/snakesAndLadders_2x.png](https://developer.apple.com/library/prerelease/ios/documentation/swift/conceptual/swift_programming_language/Art/snakesAndLadders_2x.png "Art/snakesAndLadders_2x.png")

遊戲規則如下：

- 棋盤有25個方塊，目的是要抵達第25號方塊。
- 在每一回合，你都要擲一個六面的骰子而且前進該數字的方塊數；沿著如上圖的虛線箭頭往水平方向前進。
- 如果當你回合結束時你位在梯子的下方，你必須移到梯子的上方。
- 如果當你回合結束時你位在蛇的頭部，你必須移到蛇的下方。

這個遊戲的棋盤以整數(`Int`)的陣列來表示。該陣列的大小是基於一個叫做`finalSquare`的常數來決定的；它被用來初始化這個陣列而且在這個例子裡用來檢查勝利條件。 這裡以26個值為零的整數來初始化棋盤而不是25個整數(index包括了0到25)。

```swift
let finalSquare = 25
var board = Int[](count: finalSquare + 1, repeatedValue: 0)
```

之後某些方塊會設定在蛇梯棋遊戲中用到的一些特定數值。在梯子底部的方塊會擁有正數用來讓你往棋盤上方爬；而位在蛇頭的方塊會擁有負數用來讓你落往棋盤下方。

```swift
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
```

方塊3位在梯子的底部所以你可以上昇到方塊11。為了表現出前述的狀況，`board[03]`的值是`+08`，代表整數數值`8` (`3` 與`11`的差值)。 
一元運算子加號(`+i`)跟一元運算子減號相對稱(`-i`)，並且在小於`10`的數字前多加零。(這些做法都不見得是必須的，但他們喜歡整齊的程式。)

玩家會從“方塊零”也就是指棋盤的左下角外開始。玩家第一次擲骰子後就會移動到擲出來的數字那格：

```swift
var square = 0
var diceRoll = 0
while square < finalSquare {
    // roll the dice
    if ++diceRoll == 7 { diceRoll = 1 }
    // move by the rolled amount
    square += diceRoll
    if square < board.count {
        // if we're still on the board, move up or down for a snake or a ladder
        square += board[square]
    }
}
println("Game over!")
```

這個範例使用了非常簡單的方式來模擬擲骰子。 它讓`diceRoll`的值從`0`開始來代替亂數產生器。每次`while`迴圈執行的時候，`diceRoll` 的值會以前置運算子(`++i`)遞增，然後檢查這個值是否變得太大。`++diceRoll`的回傳值相當於`diceRoll`在遞增 *之後*的值。當回傳值等於7的時候，骰子擲出來的數字變得太大便將其值重新設定為`1`。這讓`diceRoll`的值總是會是個`1`, `2`, `3`, `4`, `5`, `6`, `1`, `2`等等以此類推的序列。

擲出骰子後，玩家前進`diceRoll`數的格子。擲出來的結果可能會讓玩家移動到方塊25之後，在這種狀況下即宣告遊戲結束。為了處理這種狀況，在把`board[square]`的值加到`square`的現值讓玩家沿著梯子或蛇上昇或下降之前，程式會檢查`square`的值是否小於`board`這個陣列的`count`屬性。

如果沒有做這項檢查的話，`board[square]`可能會去讀取`board`陣列的範圍之外的值，這會將會出錯。如果`square`等於`26`的話，程式會試著去檢查`board[26]`這個在陣列範圍外的值。

當現在這次`while`迴圈執行結束時，會檢查的迴圈執行條件來判斷是否繼續執行迴圈。如果玩家移到方塊`25`或之後，迴圈的執行條件會回傳 `false`並且結束這個遊戲。

`while`迴圈適合用在這個例子，因為在`while`迴圈執行之前並不知道遊戲會玩多久。相對的，迴圈會一直執行到滿足特定條件為止。

### Do-While

另外一個`while`迴圈的變形也就是大家都知道的 `do`-`while`迴圈，會在判斷迴圈條件*之前* 先執行一次迴圈內的程式。它會持續重複執行直到條件式回傳`false`。

以下是`do`-`while` 迴圈的一般形式：

```swift
do {
    statements
} while condition
```

這裡再次用*蛇梯棋*當作例子，以`do`-`while`代替while迴圈。`finalSquare`．`board`．`square`與`diceRoll`都以與 `while`迴圈版相同的方式初始化：

```swift
let finalSquare = 25
var board = Int[](count: finalSquare + 1, repeatedValue: 0)
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
var square = 0
var diceRoll = 0
```

在遊戲的這個版本，迴圈裡的*第一個*動作是檢查梯子或蛇。棋盤裡沒有梯子會把玩家帶到方塊25，因此不可能借由爬上梯子導致勝利。因此，以檢查梯子或蛇作為迴圈裡的第一個動作是安全的。

在遊戲開始時，玩家為在方塊0。`board[0]`的值總是`0`，因此沒有影響：

```swift
do {
    // move up or down for a snake or ladder
    square += board[square]
    // roll the dice
    if ++diceRoll == 7 { diceRoll = 1 }
    // move by the rolled amount
    square += diceRoll
} while square < finalSquare
println("Game over!")
```

在程式檢查過蛇與梯子後擲出骰子，然後玩家根據`diceRoll`前進。這次的迴圈結束。

這個迴圈的條件 (`while square < finalSquare`)跟前一個範例一樣，但在這次的版本裡會直到迴圈第一次*結束*後才會執行。`do`-`while`迴圈的結構比前例中的`while`迴圈更適合這個遊戲。在上面的`do`-`while`迴圈裡，`square += board[square]` 總是*緊接著*在`while`迴圈的條件判斷之後也就說`square`還在board的範圍內。這個流程省略了遊戲的上個版本中檢查陣列範圍的動作。

## Conditional Statements

It is often useful to execute different pieces of code based on certain conditions. You might want to run an extra piece of code when an error occurs, or to display a message when a value becomes too high or too low. To do this, you make parts of your code *conditional*.

Swift provides two ways to add conditional branches to your code, known as the `if` statement and the `switch` statement. Typically, you use the `if` statement to evaluate simple conditions with only a few possible outcomes. The `switch` statement is better suited to more complex conditions with multiple possible permutations, and is useful in situations where pattern-matching can help select an appropriate code branch to execute.

### If

In its simplest form, the `if` statement has a single `if` condition. It executes a set of statements only if that condition is `true`:

```swift
var temperatureInFahrenheit = 30
if temperatureInFahrenheit <= 32 {
    println("It's very cold. Consider wearing a scarf.")
}
// prints "It's very cold. Consider wearing a scarf."
```

The preceding example checks whether the temperature is less than or equal to 32 degrees Fahrenheit (the freezing point of water). If it is, a message is printed. Otherwise, no message is printed, and code execution continues after the `if` statement’s closing brace.

The `if` statement can provide an alternative set of statements, known as an *else clause*, for when the `if` condition is `false`. These statements are indicated by the `else` keyword:

```swift
temperatureInFahrenheit = 40
if temperatureInFahrenheit <= 32 {
    println("It's very cold. Consider wearing a scarf.")
} else {
    println("It's not that cold. Wear a t-shirt.")
}
// prints "It's not that cold. Wear a t-shirt."
```

One of these two branches is always executed. Because the temperature has increased to `40` degrees Fahrenheit, it is no longer cold enough to advise wearing a scarf, and so the `else` branch is triggered instead.

You can chain multiple `if` statements together, to consider additional clauses:

```swift
temperatureInFahrenheit = 90
if temperatureInFahrenheit <= 32 {
    println("It's very cold. Consider wearing a scarf.")
} else if temperatureInFahrenheit >= 86 {
    println("It's really warm. Don't forget to wear sunscreen.")
} else {
    println("It's not that cold. Wear a t-shirt.")
}
// prints "It's really warm. Don't forget to wear sunscreen."
```

Here, an additional `if` statement is added to respond to particularly warm temperatures. The final `else` clause remains, and prints a response for any temperatures that are neither too warm nor too cold.

The final `else` clause is optional, however, and can be excluded if the set of conditions does not need to be complete:

```swift
temperatureInFahrenheit = 72
if temperatureInFahrenheit <= 32 {
    println("It's very cold. Consider wearing a scarf.")
} else if temperatureInFahrenheit >= 86 {
    println("It's really warm. Don't forget to wear sunscreen.")
}
```

In this example, the temperature is neither too cold nor too warm to trigger the `if` or `else if` conditions, and so no message is printed.

### Switch

A `switch` statement considers a value and compares it against several possible matching patterns. It then executes an appropriate block of code, based on the first pattern that matches successfully. A `switch` statement provides an alternative to the `if` statement for responding to multiple potential states.

In its simplest form, a `switch` statement compares a value against one or more values of the same type:

```swift
switch some value to consider {
case value 1:
    respond to value 1
case value 2,
value 3:
    respond to value 2 or 3
default:
    otherwise, do something else
}
```

Every `switch` statement consists of multiple possible `cases`, each of which begins with the `case` keyword. In addition to comparing against specific values, Swift provides several ways for each case to specify more complex matching patterns. These options are described later in this section.

The body of each `switch` case is a separate branch of code execution, in a similar manner to the branches of an `if` statement. The `switch` statement determines which branch should be selected. This is known as *switching* on the value that is being considered.

Every `switch` statement must be *exhaustive*. That is, every possible value of the type being considered must be matched by one of the `switch` cases. If it is not appropriate to provide a `switch` case for every possible value, you can define a default catch-all case to cover any values that are not addressed explicitly. This catch-all case is indicated by the keyword `default`, and must always appear last.

This example uses a `switch` statement to consider a single lowercase character called `someCharacter`:

```swift
let someCharacter: Character = "e"
switch someCharacter {
case "a", "e", "i", "o", "u":
    println("\(someCharacter) is a vowel")
case "b", "c", "d", "f", "g", "h", "j", "k", "l", "m",
"n", "p", "q", "r", "s", "t", "v", "w", "x", "y", "z":
    println("\(someCharacter) is a consonant")
default:
    println("\(someCharacter) is not a vowel or a consonant")
}
// prints "e is a vowel"
```

The `switch` statement’s first case matches all five lowercase vowels in the English language. Similarly, its second case matches all lowercase English consonants.

It is not practical to write all other possible characters as part of a `switch` case, and so this `switch` statement provides a `default` case to match all other characters that are not vowels or consonants. This provision ensures that the `switch` statement is exhaustive.

#### No Implicit Fallthrough

In contrast with `switch` statements in C and Objective-C, `switch` statements in Swift do not fall through the bottom of each case and into the next one by default. Instead, the entire `switch` statement finishes its execution as soon as the first matching `switch` case is completed, without requiring an explicit `break` statement. This makes the `switch` statement safer and easier to use than in C, and avoids executing more than one `switch` case by mistake.

> **NOTE**
> 
> You can still break out of a matched `switch` case before that case has completed its execution if you need to. See [Break in a Switch Statement](#break-in-a-switch-statement "Break in a Switch Statement") for details.

The body of each case *must* contain at least one executable statement. It is not valid to write the following code, because the first case is empty:

```swift
let anotherCharacter: Character = "a"
switch anotherCharacter {
case "a":
case "A":
    println("The letter A")
default:
    println("Not the letter A")
}
// this will report a compile-time error
```

Unlike a `switch` statement in C, this `switch` statement does not match both `"a"` and `"A"`. Rather, it reports a compile-time error that `case "a"`: does not contain any executable statements. This approach avoids accidental fallthrough from one case to another, and makes for safer code that is clearer in its intent.

Multiple matches for a single `switch` case can be separated by commas, and can be written over multiple lines if the list is long:

```swift
switch some value to consider {
case value 1,
value 2:
    statements
}
```

> NOTE
> 
> To opt in to fallthrough behavior for a particular `switch` case, use the `fallthrough` keyword, as described in [Fallthrough](#fallthrough "Fallthrough").

#### Range Matching

Values in `switch` cases can be checked for their inclusion in a range. This example uses number ranges to provide a natural-language count for numbers of any size:

```swift
let count = 3_000_000_000_000
let countedThings = "stars in the Milky Way"
var naturalCount: String
switch count {
case 0:
    naturalCount = "no"
case 1...3:
    naturalCount = "a few"
case 4...9:
    naturalCount = "several"
case 10...99:
    naturalCount = "tens of"
case 100...999:
    naturalCount = "hundreds of"
case 1000...999_999:
    naturalCount = "thousands of"
default:
    naturalCount = "millions and millions of"
}
println("There are \(naturalCount) \(countedThings).")
// prints "There are millions and millions of stars in the Milky Way."
```

#### Tuples

You can use tuples to test multiple values in the same `switch` statement. Each element of the tuple can be tested against a different value or range of values. Alternatively, use the underscore (`_`) identifier to match any possible value.

The example below takes an (x, y) point, expressed as a simple tuple of type `(Int, Int)`, and categorizes it on the graph that follows the example:

```swift
let somePoint = (1, 1)
switch somePoint {
case (0, 0):
    println("(0, 0) is at the origin")
case (_, 0):
    println("(\(somePoint.0), 0) is on the x-axis")
case (0, _):
    println("(0, \(somePoint.1)) is on the y-axis")
case (-2...2, -2...2):
    println("(\(somePoint.0), \(somePoint.1)) is inside the box")
default:
    println("(\(somePoint.0), \(somePoint.1)) is outside of the box")
}
// prints "(1, 1) is inside the box"
```

![Art/coordinateGraphSimple_2x.png](https://developer.apple.com/library/prerelease/ios/documentation/swift/conceptual/swift_programming_language/Art/coordinateGraphSimple_2x.png "Art/coordinateGraphSimple_2x.png")

The `switch` statement determines if the point is at the origin (0, 0); on the red x-axis; on the orange y-axis; inside the blue 4-by-4 box centered on the origin; or outside of the box.

Unlike C, Swift allows multiple `switch` cases to consider the same value or values. In fact, the point (0, 0) could match all *four* of the cases in this example. However, if multiple matches are possible, the first matching case is always used. The point (0, 0) would match `case (0, 0)` first, and so all other matching cases would be ignored.

#### Value Bindings

A `switch` case can bind the value or values it matches to temporary constants or variables, for use in the body of the case. This is known as *value binding*, because the values are “bound” to temporary constants or variables within the case’s body.

The example below takes an (x, y) point, expressed as a tuple of type `(Int, Int)` and categorizes it on the graph that follows:

```swift
let anotherPoint = (2, 0)
switch anotherPoint {
case (let x, 0):
    println("on the x-axis with an x value of \(x)")
case (0, let y):
    println("on the y-axis with a y value of \(y)")
case let (x, y):
    println("somewhere else at (\(x), \(y))")
}
// prints "on the x-axis with an x value of 2"
```

![Art/coordinateGraphMedium_2x.png](https://developer.apple.com/library/prerelease/ios/documentation/swift/conceptual/swift_programming_language/Art/coordinateGraphMedium_2x.png "Art/coordinateGraphMedium_2x.png")

The `switch` statement determines if the point is on the red x-axis, on the orange y-axis, or elsewhere, on neither axis.

The three `switch` cases declare placeholder constants `x` and `y`, which temporarily take on one or both tuple values from `anotherPoint`. The first case, `case (let x, 0)`, matches any point with a `y` value of `0` and assigns the point’s x value to the temporary constant `x`. Similarly, the second case, `case (0, let y)`, matches any point with an `x` value of `0` and assigns the point’s `y` value to the temporary constant `y`.

Once the temporary constants are declared, they can be used within the case’s code block. Here, they are used as shorthand for printing the values with the `println` function.

Note that this `switch` statement does not have a `default` case. The final case, `case let (x, y)`, declares a tuple of two placeholder constants that can match any value. As a result, it matches all possible remaining values, and a `default` case is not needed to make the `switch` statement exhaustive.

In the example above, `x` and `y` are declared as constants with the `let` keyword, because there is no need to modify their values within the body of the case. However, they could have been declared as variables instead, with the `var` keyword. If this had been done, a temporary variable would have been created and initialized with the appropriate value. Any changes to that variable would only have an effect within the body of the case.

#### Where

A `switch` case can use a `where` clause to check for additional conditions.

The example below categorizes an (x, y) point on the following graph:

```swift
let yetAnotherPoint = (1, -1)
switch yetAnotherPoint {
case let (x, y) where x == y:
    println("(\(x), \(y)) is on the line x == y")
case let (x, y) where x == -y:
    println("(\(x), \(y)) is on the line x == -y")
case let (x, y):
    println("(\(x), \(y)) is just some arbitrary point")
}
// prints "(1, -1) is on the line x == -y"
```

![Art/coordinateGraphComplex_2x.png](https://developer.apple.com/library/prerelease/ios/documentation/swift/conceptual/swift_programming_language/Art/coordinateGraphComplex_2x.png "Art/coordinateGraphComplex_2x.png")

The `switch` statement determines if the point is on the green diagonal line where `x == y`, on the purple diagonal line where `x == -y`, or neither.

The three `switch` cases declare placeholder constants `x` and `y`, which temporarily take on the two tuple values from `point`. These constants are used as part of a `where` clause, to create a dynamic filter. The `switch` case matches the current value of `point` only if the `where` clause’s condition evaluates to `true` for that value.

As in the previous example, the final case matches all possible remaining values, and so a `default` case is not needed to make the `switch` statement exhaustive.

## Control Transfer Statements

*Control transfer statements* change the order in which your code is executed, by transferring control from one piece of code to another. Swift has four control transfer statements:

- continue
- break
- fallthrough
- return

The `control`, `break` and `fallthrough` statements are described below. The `return` statement is described in [Functions](206_Functions.html "Functions").

### Continue

The `continue` statement tells a loop to stop what it is doing and start again at the beginning of the next iteration through the loop. It says “I am done with the current loop iteration” without leaving the loop altogether.

> **NOTE**
> 
> In a `for`-`condition`-`increment` loop, the incrementer is still evaluated after calling the `continue` statement. The loop itself continues to work as usual; only the code within the loop’s body is skipped.

The following example removes all vowels and spaces from a lowercase string to create a cryptic puzzle phrase:

```swift
let puzzleInput = "great minds think alike"
var puzzleOutput = ""
for character in puzzleInput {
    switch character {
    case "a", "e", "i", "o", "u", " ":
        continue
    default:
        puzzleOutput += character
    }
}
println(puzzleOutput)
// prints "grtmndsthnklk"
```

The code above calls the `continue` keyword whenever it matches a vowel or a space, causing the current iteration of the loop to end immediately and to jump straight to the start of the next iteration. This behavior enables the switch block to match (and ignore) only the vowel and space characters, rather than requiring the block to match every character that should get printed.

### Break

The `break` statement ends execution of an entire control flow statement immediately. The `break` statement can be used inside a `switch` statement or loop statement when you want to terminate the execution of the `switch` or loop statement earlier than would otherwise be the case.

#### Break in a Loop Statement

When used inside a loop statement, break ends the loop’s execution immediately, and transfers control to the first line of code after the loop’s closing brace (}). No further code from the current iteration of the loop is executed, and no further iterations of the loop are started.

#### Break in a Switch Statement

When used inside a `switch` statement, `break` causes the `switch` statement to end its execution immediately, and to transfer control to the first line of code after the `switch` statement’s closing brace (}).

This behavior can be used to match and ignore one or more cases in a `switch` statement. Because Swift’s `switch` statement is exhaustive and does not allow empty cases, it is sometimes necessary to deliberately match and ignore a case in order to make your intentions explicit. You do this by writing the `break` statement as the entire body of the case you want to ignore. When that case is matched by the `switch` statement, the `break` statement inside the case ends the `switch` statement’s execution immediately.

> **NOTE**
> 
> A `switch` case that only contains a comment is reported as a compile-time error. Comments are not statements and do not cause a `switch` case to be ignored. Always use a `break` statement to ignore a `switch` case.

The following example switches on a `Character` value and determines whether it represents a number symbol in one of four languages. Multiple values are covered in a single `switch` case for brevity:

```swift
let numberSymbol: Character = "三"  // Simplified Chinese for the number 3
var possibleIntegerValue: Int?
switch numberSymbol {
case "1", "١", "一", "๑":
    possibleIntegerValue = 1
case "2", "٢", "二", "๒":
    possibleIntegerValue = 2
case "3", "٣", "三", "๓":
    possibleIntegerValue = 3
case "4", "٤", "四", "๔":
    possibleIntegerValue = 4
default:
    break
}
if let integerValue = possibleIntegerValue {
    println("The integer value of \(numberSymbol) is \(integerValue).")
} else {
    println("An integer value could not be found for \(numberSymbol).")
}
// prints "The integer value of 三 is 3."
```

This example checks `numberSymbol` to determine whether it is a Latin, Arabic, Chinese, or Thai symbol for the numbers `1` to `4`. If a match is found, one of the `switch` statement’s cases sets an optional `Int?` variable called `possibleIntegerValue` to an appropriate integer value.

After the switch statement completes its execution, the example uses optional binding to determine whether a value was found. The `possibleIntegerValue` variable has an implicit initial value of `nil` by virtue of being an optional type, and so the optional binding will succeed only if `possibleIntegerValue` was set to an actual value by one of the `switch` statement’s first four cases.

It is not practical to list every possible `Character` value in the example above, so a `default` case provides a catchall for any characters that are not matched. This `default` case does not need to perform any action, and so it is written with a single `break` statement as its body. As soon as the `default` statement is matched, the `break` statement ends the `switch` statement’s execution, and code execution continues from the `if let` statement.

### Fallthrough

Switch statements in Swift do not fall through the bottom of each case and into the next one. Instead, the entire switch statement completes its execution as soon as the first matching case is completed. By contrast, C requires you to insert an explicit `break` statement at the end of every `switch` case to prevent fallthrough. Avoiding default fallthrough means that Swift `switch` statements are much more concise and predictable than their counterparts in C, and thus they avoid executing multiple `switch` cases by mistake.

If you really need C-style fallthrough behavior, you can opt in to this behavior on a case-by-case basis with the `fallthrough` keyword. The example below uses `fallthrough` to create a textual description of a number:

```swift
let integerToDescribe = 5
var description = "The number \(integerToDescribe) is"
switch integerToDescribe {
case 2, 3, 5, 7, 11, 13, 17, 19:
    description += " a prime number, and also"
    fallthrough
default:
    description += " an integer."
}
println(description)
// prints "The number 5 is a prime number, and also an integer."
```

This example declares a new `String` variable called `description` and assigns it an initial value. The function then considers the value of `integerToDescribe` using a `switch` statement. If the value of `integerToDescribe` is one of the prime numbers in the list, the function appends text to the end of `description`, to note that the number is prime. It then uses the `fallthrough` keyword to “fall into” the `default` case as well. The `default` case adds some extra text to the end of the description, and the `switch` statement is complete.

If the value of `integerToDescribe` is *not* in the list of known prime numbers, it is not matched by the first `switch` case at all. There are no other specific cases, and so `integerToDescribe` is matched by the catchall `default` case.

After the `switch` statement has finished executing, the number’s description is `printed` using the println function. In this example, the number `5` is correctly identified as a prime number.

> **NOTE**
> 
> The `fallthrough` keyword does not check the case conditions for the `switch` case that it causes execution to fall into. The `fallthrough` keyword simply causes code execution to move directly to the statements inside the next case (or `default` case) block, as in C’s standard `switch` statement behavior.

### Labeled Statements

You can nest loops and `switch` statements inside other loops and `switch` statements in Swift to create complex control flow structures. However, loops and `switch` statements can both use the `break` statement to end their execution prematurely. Therefore, it is sometimes useful to be explicit about which loop or `switch` statement you want a `break` statement to terminate. Similarly, if you have multiple nested loops, it can be useful to be explicit about which loop the `continue` statement should affect.

To achieve these aims, you can mark a loop statement or `switch` statement with a *statement label*, and use this label with the `break` statement or `continue` statement to end or continue the execution of the labeled statement.

A labeled statement is indicated by placing a label on the same line as the statement’s introducer keyword, followed by a colon. Here’s an example of this syntax for a `while` loop, although the principle is the same for all loops and `switch` statements:

```swift
label name: while condition {
    statements
}
```

The following example uses the `break` and `continue` statements with a labeled `while` loop for an adapted version of the *Snakes and Ladders* game that you saw earlier in this chapter. This time around, the game has an extra rule:

- To win, you must land *exactly* on square 25.

If a particular dice roll would take you beyond square 25, you must roll again until you roll the exact number needed to land on square 25.

The game board is the same as before:

![Art/snakesAndLadders_2x.png](https://developer.apple.com/library/prerelease/ios/documentation/swift/conceptual/swift_programming_language/Art/snakesAndLadders_2x.png "Art/snakesAndLadders_2x.png")

The values of `finalSquare`, `board`, `square`, and `diceRoll` are initialized in the same way as before:

```swift
let finalSquare = 25
var board = Int[](count: finalSquare + 1, repeatedValue: 0)
board[03] = +08; board[06] = +11; board[09] = +09; board[10] = +02
board[14] = -10; board[19] = -11; board[22] = -02; board[24] = -08
var square = 0
var diceRoll = 0
```

This version of the game uses a `while` loop and a `switch` statement to implement the game’s logic. The `while` loop has a statement label called `gameLoop`, to indicate that it is the main game loop for the Snakes and Ladders game.

The `while` loop’s condition is `while square != finalSquare`, to reflect that you must land exactly on square 25:

```swift
gameLoop: while square != finalSquare {
    if ++diceRoll == 7 { diceRoll = 1 }
    switch square + diceRoll {
    case finalSquare:
        // diceRoll will move us to the final square, so the game is over
        break gameLoop
    case let newSquare where newSquare > finalSquare:
        // diceRoll will move us beyond the final square, so roll again
        continue gameLoop
    default:
        // this is a valid move, so find out its effect
        square += diceRoll
        square += board[square]
    }
}
println("Game over!")
```

The dice is rolled at the start of each loop. Rather than moving the player immediately, a `switch` statement is used to consider the result of the move, and to work out if the move is allowed:

- If the dice roll will move the player onto the final square, the game is over. The `break gameLoop` statement transfers control to the first line of code outside of the while loop, which ends the game.
- If the dice roll will move the player *beyond* the final square, the move is invalid, and the player needs to roll again. The `continue gameLoop` statement ends the current `while` loop iteration and begins the next iteration of the loop.
- In all other cases, the dice roll is a valid move. The player moves forward by `diceRoll` squares, and the game logic checks for any snakes and ladders. The loop then ends, and control returns to the `while` condition to decide whether another turn is required.

> **NOTE**
> 
> If the `break` statement above did not use the `gameLoop` label, it would break out of the `switch` statement, not the `while` statement. Using the `gameLoop` label makes it clear which control statement should be terminated.
> 
> Note also that it is not strictly necessary to use the `gameLoop` label when calling `continue gameLoop` to jump to the next iteration of the loop. There is only one loop in the game, and so there is no ambiguity as to which loop the `continue` statement will affect. However, there is no harm in using the `gameLoop` label with the `continue` statement. Doing so is consistent with the label’s use alongside the `break` statement, and helps make the game’s logic clearer to read and understand.