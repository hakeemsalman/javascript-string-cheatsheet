# Strings

> *Click &#9733; if you like the project. Your contributions are heartily ♡ welcome.*

<br/>

- the textual data is stored as strings. There is *no separate type* for a single character.

--- 

- [Strings](#strings)
  - [1 Quotes](#1-quotes)
  - [2 Special characters](#2-special-characters)
    - [1. create multiline strings](#1-create-multiline-strings)
  - [String Length](#string-length)
  - [Accessing characters](#accessing-characters)
  - [Iterate](#iterate)
  - [Strings are Immutable](#strings-are-immutable)
  - [Searching for a substring](#searching-for-a-substring)
    - [1. str.indexOf('string')](#1-strindexofstring)
    - [2. str.lastIndexOf(substr, position)](#2-strlastindexofsubstr-position)
    - [3. str.includes('string'):](#3-strincludesstring)
    - [4. str.startsWith('st'):](#4-strstartswithst)
    - [5. str.endsWith('ng'):](#5-strendswithng)
  - [Getting a substring](#getting-a-substring)
    - [1. str.slice:](#1-strslice)
    - [2. str.substring:](#2-strsubstring)
    - [3. str.substr:](#3-strsubstr)
  - [Comparing strings](#comparing-strings)
    - [str.codePointAt(pos)](#strcodepointatpos)
    - [String.fromCodePoint(code)](#stringfromcodepointcode)
  - [Tasks](#tasks)
    - [Uppercase the first character](#uppercase-the-first-character)
    - [Check for spam](#check-for-spam)
    - [Truncate the text](#truncate-the-text)
    - [Extract the money](#extract-the-money)
  - [String Methods](#string-methods)
    - [str.at()](#strat)
    - [str.charAt()](#strcharat)
    - [codePointAt()](#codepointat)
    - [concat()](#concat)
    - [endWith()](#endwith)
    - [match()](#match)
    - [normalize()](#normalize)
    - [padEnd()](#padend)
    - [padStart()](#padstart)
    - [repeat()](#repeat)
    - [replace()](#replace)
    - [replaceAll()](#replaceall)
    - [search()](#search)
    - [split()](#split)
    - [Symbol.iterator](#symboliterator)
    - [How it works:](#how-it-works)
    - [Example (String):](#example-string)


## 1 Quotes

1. Strings can be enclosed within either **single** quotes, **double** quotes or **backticks**:
   1. ```js
      let singleQuote = 'single quoted';
      let doubleQuote = "double quoted";
      let backtick = `backticks`;

      function sum(a, b) {
        return a + b;
      }

      alert(`1 + 2 = ${sum(1, 2)}.`); // 1 + 2 = 3.
      ```
2. Backticks also allow us to specify a **template function** before the first backtick.
3. The syntax is: ``` func `string` ```;
   1. Follow to this [Template literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals#Tagged_templates) for more details.

## 2 Special characters

### 1. create multiline strings

```js
let guestList = "Guests:\n * John\n * Pete\n * Mary";

alert(guestList); // a multiline list of guests, same as above
```

| Character	| Description |
|---|---|
| `\n` | New line |
| `\r` | In Windows text files a combination of two characters `\r\n` represents a new break, <br/> while on non-Windows OS it’s just `\n`. <br/>That’s for historical reasons, most Windows software also understands `\n`. |
| `\`', `\"`, ``` `\` ```	| Quotes |
| `\\` |	Backslash |
| `\t` |	Tab |
| `\b`, `\f`, `\v` |	Backspace, Form Feed, Vertical Tab – mentioned for completeness, coming from old times, <br /> not used nowadays (you can forget them right now). |

## String Length

- The length property has the string length:
    - ```js
      alert( `My\n`.length ); // 3
      ```
> length is a property, `str.length` is a numeric property, **not** a function. 

## Accessing characters

- Use square brackets [pos] or call the method str.at(pos).

```js
let str = `Hello`;

// the first character
alert( str[0] ); // H
alert( str.at(0) ); // H


// the last character
alert( str[str.length - 1] ); // o
alert( str.at(-1) ); // o 
alert( str[-1] ); // undefined 
```

## Iterate

```js
for (let char of "Hello") {
  alert(char); // H,e,l,l,o (char becomes "H", then "e", then "l" etc)
}
```

## Strings are Immutable

- Strings cannot be changed in JavaScript. It is impossible to change a character.

```js
let str = 'Hi';

str[0] = 'h'; // error
alert( str[0] ); // (doesn't work) TypeError: Cannot assign to read only property '0' of string 'Hi'

str = 'h' + str[1]; // replace the string

alert( str ); // hi
```

- Changing the case: Mutable

```js
alert( 'Interface'.toUpperCase() ); // INTERFACE
alert( 'Interface'.toLowerCase() ); // interface
alert( 'Interface'[0].toLowerCase() ); // 'i'
```

## Searching for a substring

### 1. str.indexOf('string')
   
- Parameters: `str.indexOf(string, pos)`

1. It looks for the `substr` in `str`, starting from the given position `pos`, and returns the position where the match was found or `-1` if nothing can be found.
```js
let str = 'Widget with id';

alert( str.indexOf('Widget') ); // 0, because 'Widget' is found at the beginning
alert( str.indexOf('widget') ); // -1, not found, the search is case-sensitive

alert( str.indexOf("id") ); // 1, "id" is found at the position 1 (..idget with id)
```

2. The optional second parameter allows us to start searching from a given position.
 
```js
let str = 'Widget with id';
alert( str.indexOf('id', 2) ) // 12

// WORD SEARCH ALGORITHM
let str = 'As sly as a fox, as strong as an ox';

let target = 'as'; // let's look for it

let pos = 0;
while (true) {
  let foundPos = str.indexOf(target, pos);
  if (foundPos == -1) break;

  alert( `Found at ${foundPos}` ); // 7 17 27 
  pos = foundPos + 1; // continue the search from the next position
}

// SHORT HAND 
let str = "As sly as a fox, as strong as an ox";
let target = "as";

let pos = -1;
while ((pos = str.indexOf(target, pos + 1)) != -1) {
  alert( pos );
}
```
3. Return value when using an empty search string

```js
"hello world".indexOf(""); // returns 0
"hello world".indexOf("", 0); // returns 0
"hello world".indexOf("", 3); // returns 3

// pos > str.length, then returns str.length
"hello world".indexOf("", 11); // returns 11
"hello world".indexOf("", 13); // returns 11
```


### 2. str.lastIndexOf(substr, position)

- It searches from the end of a string to its beginning.
- It searches from right to left in the string.
- If the value is not found, it returns `-1`.
- If empty is passed into params, returns `length of string`.
- You can provide an optional second argument to specify the starting index for the search (the search will stop before this index).

```js
let str = 'As sly as a fox, as strong as an ox';

let target = 'as'; // let's look for it

let pos = str.length; // last index
while (true) {
  let foundPos = str.indexOf(target, pos);
  if (foundPos == -1) break;

  alert( `Found at ${foundPos}` ); // 27 17 7
  pos = foundPos - 1; // continue the search from the previous position
}

let str = "Hello World, Hello!";
let lastIndex = str.lastIndexOf("Hello");  // Result: 13
let emptyIndex = str.lastIndexOf("");      // Result: 26 (length of the string)
```

### 3. str.includes('string'):

- It performs a **case-sensitive** search to determine whether a given string may be found within this string.
- It returns `true` if the substring is found, and `false` if it's not.
- You can provide an optional second argument to specify the index from where the search should start (Defaults to `0`.)

- The more modern method `str.includes(substr, pos)` **returns** `true`/`false` depending on whether `str` contains `substr` within.

- Parameters: `includes(searchString, <position>)`

```js
alert( "Widget with id".includes("Widget") ); // true

alert('World'.includes("world"));   // Result: false (case-sensitive)
alert( "Hello".includes("Bye") ); // false
alert( "Widget".includes("id", 3) ); // false, from position 3 there is no "id"
```

### 4. str.startsWith('st'):
   1. `alert( "Widget".startsWith("Wid") ); // true, "Widget" starts with "Wid"`
### 5. str.endsWith('ng'):
   1. `alert( "Widget".endsWith("get") ); // true, "Widget" ends with "get"`

## Getting a substring

- There are 3 methods in JavaScript to get a substring: `substring`, `substr` and `slice`.


| method |	selects… |	negatives |
|---|---|---|
| `slice(start, end)` |	from start to end (not including `end`) |	allows negatives |
| `substring(start, end)`	| between start and end (not including `end`) | negative values mean `0` |
| `substr(start, length)`	| from start get length characters | allows negative `start` |


### 1. str.slice:

1. Returns the part of the string from `start` to (but not including) `end`.
2. Negative values for `start`/`end` are also **possible**.
    1. ```js
      let str = "stringify";
      alert( str.slice(0, 5) ); // 'strin', the substring from 0 to 5 (not including 5)
      alert( str.slice(0, 1) ); // 's', from 0 to 1, but not including 1, so only character at 0

      // If there is no second argument, then slice goes till the end of the string:
      alert( str.slice(2) ); // 'ringify', from the 2nd position till the end

      // NEGATIVE
      // start at the 4th position from the right, end at the 1st from the right
      alert( str.slice(-4, -1) ); // 'gif'
      ```
            
### 2. str.substring:

1. Returns the part of the string between `start` and `end` (not including `end`).
2. Negative arguments are (unlike slice) **not** supported, they are treated as `0`.
3. This is almost the same as `slice`, but it allows start to be `greater` than `end` (in this case it simply swaps `start` and `end` values).
    1. ```js
        let str = "stringify";

        // these are same for substring
        alert( str.substring(2, 6) ); // "ring"
        alert( str.substring(6, 2) ); // "ring"  (IT SWAPS THE VALUES)

        // ...but not for slice:
        alert( str.slice(2, 6) ); // "ring" (the same)
        alert( str.slice(6, 2) ); // "" (an empty string)
        ```

### 3. str.substr:

1. Returns the part of the string from [`start`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/substr), with the given `length`.
2. this one allows us to specify the `length` instead of the ending position:
3. it’s not recommended to use it. In practice, it’s supported everywhere. (in future <span style="color: red">**DEPRECATED**</span>)
    1. ```js
        let str = "stringify";
        alert( str.substr(2, 4) ); // 'ring', from the 2nd position get 4 characters

        // The first argument may be negative, to count from the end:
        alert( str.substr(-4, 2) ); // 'gi', from the 4th position get 2 characters
        ```


## Comparing strings

1. A lowercase letter is always greater than the uppercase:
   1. ```js
      alert( 'a' > 'Z' ); // true
      ```
2. Letters with diacritical marks are “out of order”:
   1. ```js
      alert( 'Österreich' > 'Zealand' ); // true
      ```

### str.codePointAt(pos)

- Returns a decimal number representing the code for the character at position `pos`:
    - ```js
      // different case letters have different codes
      alert( "Z".codePointAt(0) ); // 90
      alert( "z".codePointAt(0) ); // 122
      alert( "z".codePointAt(0).toString(16) ); // 7a (if we need a hexadecimal value)
      ```
### String.fromCodePoint(code)

- Here `String` is **function**, not a string variable.
- Creates a character by its numeric `code`

```js
alert( String.fromCodePoint(90) ); // Z
alert( String.fromCodePoint(65) ); // A
alert( String.fromCodePoint(0x5a) ); // Z (we can also use a hex value as an argument)
```

<table style="width: 700px" align="center">
<tr>
<td>

```js
let str = '';

for (let i = 65; i <= 220; i++) {
  str += String.fromCodePoint(i);
}
alert( str );
// Output:
// ABCDEFGHIJKLMNOPQRSTUVWXYZ[\]^_`abcdefghijklmnopqrstuvwxyz{|}~
// ¡¢£¤¥¦§¨©ª«¬­®¯°±²³´µ¶·¸¹º»¼½¾¿ÀÁÂÃÄÅÆÇÈÉÊËÌÍÎÏÐÑÒÓÔÕÖ×ØÙÚÛÜ
```

</td>
</tr>
</table>


## Tasks

### Uppercase the first character

- Write a function ucFirst(str) that returns the string str with the uppercased first character, for instance:

```js
ucFirst("john") ==> "John";
```

<details>
<summary>SHOW SOLUTION</summary>

```js
function ucFirst(str) {
  if (!str) return str;

  return str[0].toUpperCase() + str.slice(1);
}

alert( ucFirst("john") ); // John
```

</details>


### Check for spam

- Write a function checkSpam(str) that returns true if str contains ‘viagra’ or ‘XXX’, otherwise false.

```js
checkSpam('buy ViAgRA now') == true
checkSpam('free xxxxx') == true
checkSpam("innocent rabbit") == false
```

<details>
<summary>SHOW SOLUTION</summary>

```js
function checkSpam(str) {
  let lowerStr = str.toLowerCase();

  return lowerStr.includes('viagra') || lowerStr.includes('xxx');
}

alert( checkSpam('buy ViAgRA now') );
alert( checkSpam('free xxxxx') );
alert( checkSpam("innocent rabbit") );
```

</details>



### Truncate the text

- Create a function truncate(str, maxlength) that checks the length of the str and, if it exceeds maxlength – replaces the end of str with the ellipsis character "…", to make its length equal to maxlength.

```js
truncate("What I'd like to tell on this topic is:", 20) == "What I'd like to te…"

truncate("Hi everyone!", 20) == "Hi everyone!"
```

<details>
<summary>SHOW SOLUTION</summary>

```js
function truncate(str, maxlength) {
  return (str.length > maxlength) ? str.slice(0, maxlength - 1) + '…' : str;
}
```

</details>


### Extract the money

- We have a cost in the form "$120". That is: the dollar sign goes first, and then the number.
- Create a function extractCurrencyValue(str) that would extract the numeric value from such string and return it.

```js
alert( extractCurrencyValue('$120') === 120 ); // true
```

<details>
<summary>SHOW SOLUTION</summary>

```js
function extractCurrencyValue(str) {
  return +str.slice(1);
}
```

</details>

## String Methods

### str.at()

- The `at()` method of a `String` takes an integer as input.
- It returns a new string with the single UTF-16 code unit at the specified position.
- Supports both positive and negative integers:
   - Positive integers: Count from the start of the string.
   - Negative integers: Count backward from the end of the string.
- `undefined` returns, if given index not found.

- Parameter: `at(index)`
```js
  'salman'.at(1); // a
```

### str.charAt()

- The `charAt()` method in JavaScript returns the character at a specified index in a string.
- The index is based on zero (0 being the first character).
- Supports only **Positive numbers**
- if given index not found, an **empty string** is returned.

- Parameter: `chatAt(index)`
```js
  'salman'.charAt(1); // a
```

### codePointAt()

> code point = `U+00F1` or `"\u00F1"`

- The `codePointAt()` method returns a non-negative integer, the Unicode code point value at the specified position in a string.
- It can handle characters that are represented by more than one UTF-16 code unit (such as emoji or rare characters).
- If the position is out of range, `undefined` is returned.

- Parameters: `codePointAt(index)`
```js
  "😍".codePointAt(0); // 128525
  "ABC".codePointAt(0); // 65
```

> FUN: You can use this code in HTML as an entity without icon, `&#128525`.


### concat()

- The `concat()` method in JavaScript joins two or more strings together.
- It returns a new string, combining the original string with the specified string(s).
- This method does **not** change the **original** string but creates a **new** one.

- Parameters: `concat(str1, ...,strN)`
```javascript
let str1 = "Hello";
let str2 = "World";
let result = str1.concat(" ", str2);  // Result: "Hello World"
let result = str1.concat(str2);  // Result: "HelloWorld"
```


### endWith()

- The `endsWith()` method in JavaScript checks if a string **ends** with a specified substring.
- It returns `true` if the string ends with the given substring, and `false` otherwise.
- An optional second argument can be provided to treat the string as if it were only a certain length for the check.
  - Defaults to `str.length`.

- Parameters: `endsWith(searchString, <endPosition>)`
```javascript
let str = "Hello World";
let result1 = str.endsWith("World");  // Result: true
let result2 = str.endsWith("Hello");  // Result: false
let result3 = str.endsWith("Hello", 5);  // Result: true (treats the string as "Hello")
```

### match()

- The `match()` method in JavaScript retrieves the result of matching a string against a **regular expression**.
- It returns an array of matches when there are matches, or `null` if no match is found.
- If the regular expression includes the global flag (`/g`), it returns **all matches**; otherwise, it returns only the **first match**.
- When the `regexp` parameter is a string or a number, it is implicitly converted to a [RegExp](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp) by using `new RegExp(regexp)`.
- It may have unexpected results if **special characters** are not properly escaped.

> If you only want the **first match** found, you might want to use [RegExp.prototype.exec()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/exec) instead.

- Parameters: `match(regexp)`
```javascript
let str = "The rain in Spain stays mainly in the plain";
let result1 = str.match(/ain/g);  // Result: ["ain", "ain", "ain"]
let result2 = str.match(/xyz/);   // Result: null (no match found)
let result2 = str.match(/ain/);   // Result: ["ain"]

const str1 = "NaN means not a number. Infinity contains -Infinity and +Infinity in JavaScript.";
str1.match("number"); // "number" is a string. returns ["number"]

console.log("123".match("1.3")); // [ "123" ]
console.log("123".match("1\\.3")); // null

```

### normalize()

- The `normalize()` method in JavaScript returns the Unicode Normalization Form of a given string.
- It can be used to convert different but equivalent Unicode characters into a consistent form.
- There are four normalization forms: `NFC`, `NFD`, `NFKC`, and `NFKD`:
  - **NFC** (default): Combines characters into the composed form.
  - **NFD**: Splits characters into the decomposed form.
  - **NFKC**: Combines characters and applies compatibility transformations.
  - **NFKD**: Decomposes characters and applies compatibility transformations.

- Parameter: `normalize(form)`
```javascript
let str = "e\u0301";  // 'é' as 'e' + combining accent
let normalized = str.normalize();  // Result: "é" (as a single composed character)
```

In this example, the `normalize()` method converts the decomposed form (`e + accent`) into the composed form (`é`).


### padEnd()

- The `padEnd()` method in JavaScript pads the current string with another string (or characters) until the resulting string reaches the specified length.
- The padding is added to the **end** of the original string.
- If the padding length exceeds the specified length, the string is truncated to fit.
- If no padding string is provided, spaces are used by default.

- Params: `padEnd(targetLength, <padString>)`
```javascript
let str = "Hello";
let result1 = str.padEnd(10);         // Result: "Hello     " (adds 5 spaces)
let result2 = str.padEnd(10, ".");    // Result: "Hello....." (adds 5 dots)
let result3 = str.padEnd(8, "123");   // Result: "Hello123" (pads with "123")
```


### padStart()

- The `padStart()` method in JavaScript pads the current string with another string (or characters) until the resulting string reaches the specified length.
- The padding is added to the **beginning** of the original string.
- If the padding length exceeds the specified length, the string is truncated to fit.
- If no padding string is provided, spaces are used by default.


- Params: `padStart(targetLength, <padString>)`
```javascript
let str = "Hello";
let result1 = str.padStart(10);         // Result: "     Hello" (adds 5 spaces)
let result2 = str.padStart(10, ".");    // Result: ".....Hello" (adds 5 dots)
let result3 = str.padStart(8, "123");   // Result: "123Hello" (pads with "123")
```

### repeat()

- The `repeat()` method in JavaScript returns a new string with the original string repeated a specified number of times.
- The number of repetitions must be a positive integer.
- If the repetition count is `0`, an empty string is returned.
- If the count is a decimal, it is automatically rounded down to an integer.
- 
- Params: `repeat(count)`
- Exceptions:
  - `RangeError`: Thrown if `count` is negative or if `count` overflows maximum string length. 
```javascript
let str = "Hello";
let result1 = str.repeat(3);   // Result: "HelloHelloHello"
let result2 = str.repeat(0);   // Result: "" (empty string)
let result2 = str.repeat(-1); // RangeError
let result2 = str.repeat(1 / 0); // RangeError
```

### replace()

- The `replace()` method in JavaScript returns a new string where the **first occurrence** of a **specified value** or **regular expression (regex)** is replaced with a new value.
- It only replaces the first match unless a global (`/g`) flag is used with a regular expression.
- The replacement can be a string or a function to dynamically generate the replacement.
- The original string remains unchanged.

- Params: `replace(pattern, replacement)`
```javascript
let str = "Hello World";
let result1 = str.replace("World", "JavaScript");  // Result: "Hello JavaScript"
let result2 = str.replace(/o/g, "0");              // Result: "Hell0 W0rld" (global replacement)
```

### replaceAll()

- The `replaceAll()` method in JavaScript returns a new string with **all occurrences** of a specified value or regular expression replaced with a new value.
- Unlike `replace()`, it replaces **every match** in the string, not just the first one.
- It can take a string or a regular expression (without the global flag) as the target to replace.
-  The original string is left unchanged.

- Params: `replace(pattern, replacement)`
- Exceptions:
  - `TypeError` : Thrown if the `pattern` is a `regex` that does not have the global (`g`) flag set (its `flags` property does not contain "`g`").

```javascript
let str = "Hello World, Hello Universe";
let result1 = str.replaceAll("Hello", "Hi");    // Result: "Hi World, Hi Universe"
let result2 = str.replaceAll("o", "0");         // Result: "Hell0 W0rld, Hell0 Universe"
```

### search()

- The `search()` method in JavaScript searches for a match between a string and a regular expression.
- It returns the **index of the first match** or `-1` if no match is found.
- Unlike `indexOf()`, `search()` only works with regular expressions, not plain strings.
- It does not support a second argument for specifying the start position.
- The `g` flag of `regexp` has no effect on the `search()` result

> If you need the content of the matched text, use [String.prototype.match()](#match)

- Params: `search(regexp)`
```javascript
let str = "The rain in Spain";
let result1 = str.search(/ain/);   // Result: 5 (first occurrence of "ain")
let result2 = str.search(/xyz/);   // Result: -1 (no match found)
```

### split()

- The [`split()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/split) method in JavaScript divides a string into an array of substrings based on a specified separator.
- The separator can be a string or a regular expression.
- An optional second argument can limit the number of splits.
- The original string remains unchanged.

- Params: `split(separator, limit)`

```javascript
let str = "apple,banana,orange";
let result1 = str.split(",");        // Result: ["apple", "banana", "orange"]
let result2 = str.split(",", 2);     // Result: ["apple", "banana"] (limit to 2 splits)
let result2 = str.split(",", 0);     // Result: [] (empty array, limit to 0 splits)
let result3 = str.split("");         // Result: ["a", "p", "p", "l", "e", ",", ...] (splits every character)
```

<table style="width: 700px; background-color: #321C20;" align="center">
<tr>
<td>

&#9888; **Warning**: When the empty string (`""`) is used as a separator, the string is **not** split by *user-perceived* characters ([grapheme clusters](https://unicode.org/reports/tr29/#Grapheme_Cluster_Boundaries)) or unicode characters (code points), but by UTF-16 code units. This destroys [surrogate pairs](https://unicode.org/faq/utf_bom.html#utf16-2). See this [StackOverflow](https://stackoverflow.com/questions/4547609/how-can-i-get-a-character-array-from-a-string/34717402#34717402) question

</td>
</tr>
</table>

<table style="background-color: #321C20;" align="center">

<tr>
<td>

If `separator` is a `regexp` that matches empty strings, whether the match is split by UTF-16 code units or
Unicode code points depends on if the regex is [Unicode-aware](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/RegExp/unicode#unicode-aware_mode).

```js
"😄😄".split(/(?:)/); // [ "\ud83d", "\ude04", "\ud83d", "\ude04" ]
"😄😄".split(/(?:)/u); // [ "😄", "😄" ]
```

</td>
</tr>
</table>





### Symbol.iterator


- `[Symbol.iterator]()` is a built-in method that allows an object to be iterated, like in `for...of` loops, by returning an iterator.
- For strings, arrays, and many other objects, this method defines the default iteration behavior.
- An object with `[Symbol.iterator]()` can be looped over, as it returns an iterator that produces the values one by one.
- Parameters: **None**.
- 
### How it works:
- The object’s `[Symbol.iterator]()` method must return an iterator object with a `next()` method.
- The `next()` method provides two properties:
  - `value`: The next value in the iteration.
  - `done`: A boolean that indicates whether the iteration is finished.

### Example (String):
```javascript
let str = "Hello";
let iterator = str[Symbol.iterator]();  // Creates an iterator for the string

console.log(iterator.next());  // { value: 'H', done: false }
console.log(iterator.next());  // { value: 'e', done: false }
console.log(iterator.next());  // { value: 'l', done: false }
console.log(iterator.next());  // { value: 'l', done: false }
console.log(iterator.next());  // { value: 'o', done: false }
console.log(iterator.next());  // { value: undefined, done: true } (iteration is complete)
```






