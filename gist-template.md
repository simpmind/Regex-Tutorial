# Learn Regex

## Summary

> A regular expression is a pattern matched against a subject string from
left to right. Regular expressions can replace text within a string, 
validate forms, extract a substring from a string based on a pattern match. You can call it "regex" in short. 
Regex is supported in all the scripting languages including Javascript

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)

## Regex Components

## Anchors

> Anchors have special meaning in regular expressions. They do not match any character. Instead, they match a position before or after characters:

Use the `^` anchor to match the beginning of the text.

```
let mess = 'foo';
console.log(/^f/.test(mess));
```

Output:

```
true
```

The `/^f/` match any text that starts with the letter f. It returns true.

Use the `$` anchor to match the end of the text.

the following example returns true because the string bar ends with the letter r:

```
let mess = 'bar';
console.log(/r$/.test(mess));
```

Output:

```
true
```
## Quantifiers

> Quantifiers determine how often a part of your regular expression should be repeated. Suppose you want to repeat something in a regex (an individual character, a character class, or a sub-expression). In that case, you can write a quantifier after it to specify how many times it should be repeated.

Here are common quantifiers: `?`, `*`, `+`, `{N}`, `{N,M}`.

### +

> The quantifier `{1,}` means one or more, with the shorthand as `+.` For example, the `\d+` searches for numbers:

```
let phone = "+1-(123)-456-7890";
let result = phone.match(/\d+/g);

console.log(result);
```
Output:
```
["1", "123", "456", "7890"]
```
### ?

> The quantifier `?` means zero or one. It is the same as `{0,1}`. For example, `/favou?r/` will match both favor and favour: 

```
let message = 'Is this favor or favour?';
let result = message.match(/favou?r/g);

console.log(result);
```
Output:
```
["favor", "favour"]
```
### *

The quantifier `*` means zero or more. It is the same as `{0,}`.
```
let test = 'Hamburger is not from Ham';
let compare = /Ham\w*/g

let results = test.match(compare);

console.log(results);
```

Output:
```
["Hamburger", "Ham"]
```


## Grouping Constructs

Suppose you have the following path:
```
resource/id
```
For example:

posts/1
In the path, the resource is posts and id is 1. To match the path, use the following regular expression:
```
/\w+\/\d+/
```
In this pattern:

`\w+` is a word character set with a quantifier `(+)` that matches one or more word characters.

`/` matches the forward slash `(/).` The backslash `(\)` escapes the forward slash,

`\d+` is the combination of the digit character set and a quantifier `(+),` which matches one or more digits.


### Multiple capturing groups

To capture both the resource (posts) and id (1) of the path (post/1), you use multiple capturing groups in the regular expression as follows:
```
/(\w+)\/(\d+)/
```

The regex has two capturing groups one for `\w+` and the other for `\d+` .


### Named capturing groups

To access a subgroup in a match, you use an index. However, you may want to access a subgroup by a meaningful name to make it more convenient.

To do that, you use the named capturing group to assign a name to a group. The following shows the syntax for assigning a name to a capturing group:
```
(?<name>rule)
```
In this syntax:

`()` indicates a capturing group.

`?<name>` specifies the name of the capturing group.

`rule` is a rule in the pattern.

## Bracket Expressions
### [ ]
Brackets indicate a set of characters to match. Any individual character between the brackets will match, and you can also use a hyphen to define a set.

```
'ant'.match(/[abcd]/) // -> matches 'a'
```
You can use the `^` metacharacter to negate what is between the brackets.
```
'heyo'.match(/[^abcd]/) // -> matches 'o'
```

### { }
Curly braces specify an exact amount of things to match after an expression: `\la{2}\` will only match `‘la’` exactly twice.

```
'shalama'.match(/la{2}/) // -> no match
'shalala'.match(/la{2}/) // -> matches 'lala'
```

### ( )
Parentheses represent remembered matches which helps find and replace operations or any time you need to do something with part of the match. You can use `$n` to refer to a match, starting with `$1` up to `$9`, or with `$&` to refer to the entire match.

```
'Marcol Polo'.match(/([A-Za-z]+)\s([A-Za-z]+)/) // -> matches 'Marco Polo' with 'Marcol' remembered as $1 and 'Polo' as $2

```

## Character Classes

> A character class allows you to match any symbol from a certain character set. A character class is also called a character set. Suppose that you have a phone number like this:

```
+1-(123)-456-7890
```

And you want to turn it into a plain number:
```
11234567890
```

Character classes in regular expressions can help you to do this.

Let’s explore the digit character class first. The digit character class is denoted by \d which matches any single digit:

```
\d
```

The following example uses the \d to match the first number in the phone number:
```
let phone = '+1-(123)-456-7890';
let re = /\d/;

console.log(phone.match(re));
```

Output:
```
["1"]
```


## The OR Operator

Using logical operators to combine multiple conditions in a conditional expression. The `|` metacharacter is similar to logical OR with regular expressions. The regexp will match if the expressions separated by `|` are satisfied. Each of these alternations is an entire regexp. For example, anchors are specific to that particular alternation.
```
// match either 'foo' or 'bar'
> const test = /foo|bar/
> test.test('heres foos')
< true
> test.test('heres bars')
< true
> test.test('baloons')
< false

```

## Flags

>A flag is an optional parameter to a regex that modifies its behavior of searching. 
A flag changes the default searching behavior of a regular expression. It makes a regex search in a different way.

A flag is denoted using a single lowercase alphabetic character.

In JavaScript regex, there are 6 flags:

|Flag|Name|Modification|
|:----:|----|----|
|i|Ignore Casing|Makes the expression search case-insensitively.|
|g|	Global|Makes the expression search for all occurrences.|
|s|	Dot All|Makes the wild character . match newlines as well.|
|m|	Multiline|Makes the boundary characters ^ and $ match the beginning and ending of every single line instead of the beginning and ending of the whole string.|
|y|	Sticky|Makes the expression start its searching from the index indicated in its lastIndex property.|
|u|	Unicode|Makes the expression assume individual characters as code points, not code units, and thus match 32-bit characters as well.|


For an expression created literally, i.e. using the forward slashes `//`, flags comes after the second slash. In general notation we can expression this as follows:
```
/pattern/flags
```
Similarly, for an expression created using RegExp(), flags go as a string in the second argument, as shown below:
```
new RegExp('pattern', 'flags')
```


## Character Escapes

A backslash `\` is used to denote character classes, e.g., `\d`which is a special character in regexps

There are other special characters have special meaning in a regexp like `[ ] { } ( ) \ ^ $ . | ? * +`

### Escaping

In order to find a dot. Not “any character”, but just a dot.

To use a special character as a regular one, prepend it with a backslash: `\..`

That’s also called “escaping a character”.

For example:
```
alert( "your grade is 9.5".match(/\d\.\d/) ); // 5.1 (match!)
alert( "course 905".match(/\d\.\d/) ); // null (looking for a real dot \.)
```

### A slash

A slash symbol `'/'` in JavaScript is used to open and close the regexp: `/...pattern.../`, so we should escape it too.

Here’s what a search for a slash `'/'` looks like:
```
 alert( "/".match(/\//) ); // '/'
```

### new RegExp

If we are creating a regular expression with `new RegExp`, then we don’t have to escape `/`, but need to do some other escaping.

For instance, consider this:
```
 let regexp = new RegExp("\d\.\d");

alert( "your grade is 9.5".match(regexp) ); // null
```


## Author

Github: [https://github.com/simpmind](https://github.com/simpmind)

Email: <tengfai97@gmail.com>

