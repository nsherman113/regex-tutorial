# Understanding RegEx Expressions 

RegEx is short for regular expression. A regular expressions is a sequence of characters used to confirm character combinations. In this tutorial, we will review a regularly used regex pattern and separate the regex pattern by each component. 

## Summary

 /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/

 The code above is a regular expression used to match an email. I will break the regular expression into components to better illustrate the syntax and each component. 

## Table of Contents

- [Understanding RegEx Expressions](#understanding-regex-expressions)
  - [Summary](#summary)
  - [Table of Contents](#table-of-contents)
  - [Regex Components](#regex-components)
    - [Anchors](#anchors)
    - [Quantifiers](#quantifiers)
    - [OR Operator](#or-operator)
    - [Character Classes](#character-classes)
    - [Flags](#flags)
    - [Grouping and Capturing](#grouping-and-capturing)
    - [Bracket Expressions](#bracket-expressions)
    - [Greedy and Lazy Match](#greedy-and-lazy-match)
    - [Boundaries](#boundaries)
    - [Back-references](#back-references)
    - [Look-ahead and Look-behind](#look-ahead-and-look-behind)
    - [Look-ahead and Look-behind](#look-ahead-and-look-behind-1)
  - [Author](#author)

## Regex Components

### Anchors

An anchor is a character within the regular expression that allows the user to identify strings that contain specific characters. Below is an example of Anchors: 

- `^` <-- identifies a string based upon its anterior word 
- `$` <-- identifies a string ending with the preceeding word before a given character. 
- Example: 
- ^whats <---- identifies any string beginning with "whats"
- up$ <---- identifies all strings ending with "up"
- ^whats up$ <----- matches the exact string 
- haha <-------- matches all string that have the exact text "haha"

### Quantifiers

A Quantifier is a character within the regex that illustrates how many times a character, group, or class are shown within the input to be matched. See below example: 

- `*` <-- identifies a string with an anterior followed by zero or more of the previous character
- `+` <-- identifies a string with an anterior followed by one or more of the previous character
- `?` <-- identifies a string with an antnerior follwoed by zero or one of the previous character
- `{}` <--  identifies a string with an anterior followed by how ever many the number in the brackets of the previous character in the string
- `()*` <-- identifies a string with any anterior character followed by zero or more duplicates of a given string within the brackets

Below are examples of each symbol in use: 

xyz*        Identifies a string that has xy followed by zero or more z
xyz+        Identifies a string that has xy followed by one or more z
xyz?        Identifies a string that has xy followed by zero or one z
xyz{2}      Identifies a string that has xy followed by 2 z
xyz{2,}     Identifies a string that has xy followed by 2 or more z
xyz{2,5}    Identifies a string that has xy followed by 2 up to 5 z
x(yz)*      Identifies a string that has x followed by zero or more copies of the sequence yz
x(yz){2,5}  Identifies a string that has x followed by 2 up to 5 copies of the sequence yz


### OR Operator

The OR operator connects a choice of a given regular expression 

See below example of OR operators:

- `(|)` <-- matches a string that has any anterior characters followed by the characters on the left or right of the vertical bar
<- `[]` <-- matches a string that has any anterior characters without any characters within the brackets
- Examples: 

x(y|z)  matches a string that has x followed by y or z (and captures y or z)
x[yz]   matches a string that has x, but without capturing b or c

### Character Classes

Character Classes (Character Set) tells the regex engine to match only one out serveral specific characters, such as digits, words, or whitespace

Examples of Character Classes are as follows:

- `\d` <-- matches a single character that is a digit
- `\w` <-- matches a word character (any alphanumeric character plus underscore)
- `\s` <-- matches a whitespace character (including tabs and line brakes)
- `.` <-- matches any character
- the capital case for a aformentioned characters inverses the match

Below are classed in use: 

\d    matches a single any digit 0-9
\w    matches a single any character that is a-z
\s    matches ` `
.     matches any character
\D    matches a single non-digit character
\W    matches a single any non-character that is a-z
\S    matches a single non-` `


### Flags

Flags are optional parameters that we can add to a plain expression to make it search in a different way. Each flag is denoted by a single alphabetic character, and serves different purposes in modifying the expression's searching behavior.

Examples of Flags are as follows:
- `g`<-- Global, does not return after the first match, which restarted any subsequest searches from the end of the previous match (Makes the expression search for all occurences)
- `m`<-- Multi-line, when enabled the Anchors (^ $) will match the start and end of a line, rather than the whole string
- `i`<-- Insensitive, makes the entire expression case-insensitive

Below are examples of each flag in use:

/Hello/g   matches all `Hello` in the test
/Hello/m   matches the beginning and ending of each line with `Hello`, rather than the whole string `Hello` itself
/Hello/i   matches all `hello` despite case (Hello, hEllo, heLlo, hellO, hello, HELLO all match)


### Grouping and Capturing

Grouping unifies a pattern or string so that it is matched in a complete block

Examples of Grouping are as follows:
- `()`<-- parentheses creates a capture group
- `(?:)`<-- using `?:` disables the capturing group
- `(?<>)`<-- using `?<>` puts a name to the group

Below are examples in use:

x(yz)           parentheses create a capturing group with value yz
x(?:yz)*        using ?: we disable the capturing group
x(?<bar>yz)     using ?<bar> we put a name to the group


### Bracket Expressions

Bracket Expressions are characters enclosed by a bracket `[]` matching any single character within the brackets. 
*note: if the first character within the brackets is a `^` then it signifies any chracter **not** in the list, and is unspecified whether it matches an encoding error. 

Examples of Bracket Expressions are as follows: 
- `[]`<-- matching any single character within the brackets
- `[]%`<-- matching the string inside the brackets before the `%`
- `[^]`<-- matching any string that has not a letter from within the brackets (negation of expression)

Below are examples of brackets in use:

[xyz]         matches a string that etiher has x or x y or x z (same as x|y|z)
[x-y]         similar to case above
[u-zU-Z0-9]   a string that represents a single hexadecimal digit, case insensitively
[0-9]%        a string that has a character from 0-9 before a %
[^a-zA-Z]     a string that has not a letter from a to z or from A to Z


### Greedy and Lazy Match

Greedy and/or Lazy Matching are quantifiers that expand the match throughout the text (at it's maximum length possible). 

Examples of Greedy and/or Lazy Matching are as follows:
- `* + {}`<-- any one of these character can be used as a quanitifer for a Greedy or Lazy Match

Below are examples:

<.+?>     matches any character that is one or more times included inside `<` and `>`, and expands as needed.
<[^<>]+>  matches any character expects `<` or `>` one or more times included inside `<` and `>`. 


### Boundaries

Boundaries are the spots between each character. There are two types of Boundaries, 1.) Word and 2.) Non-Word, each denoted by a specific character.

Examples of Boundaries are as follows:
- `\b` <-- A position that bounds a word, or where a word starts or ends. It denotes a place between a word and non-word character, at the start and end of a string.
- `\B` <-- Opposite of a word boundary, the negation of `\b` will match any position a word boundary doesnt. 
- `*`  <--Matches between a word and word character, as well as between a non-word and non-word character.

Below are examples of each boundary in use:

`Hello World` has 12 total Boundaries with 8 Word Boundaries as seen below:
|H|e|l|l|o| |W|o|r|l|d|
^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^ ^
N W W W W N N W W W W N  -  N = Nonword Boundary \ W = Word Boundary
\bxyz\b     matches a "whole words only search" for the string `xyz`
\Bxyz\B     matches only if the pattern is completely surrounded by word characters `txyzt` that match the string `xyz` as it only has word boundaries



### Back-references

As indicated above, grouping is saved in memory for later use. Backreferencing is the reference of a captured match, save in memory, by a captured group.

Examples are as follows:

([xyz])\1              using \1 it identifies the same text that was matched by the original capturing group
([uwx])([yz])\2\1      we can use \2 (\3, \4, etc.) to identify the same text that was matched by the second (and all other) capturing group(s)
(?<bar>[xzy])\k<bar>   we surround the name bar to the group and reference it later (\k<foo>). The result is the same of the first regex

### Look-ahead and Look-behind
Look-ahead and Look-behind (lookaround) are `start and end` zero-length assertions [Anchors](#anchors), though they match characters, then complete the match, returning the result: **Match or No Match**. 
Lookaround allows to simplify regular expressions significantly.



### Look-ahead and Look-behind


h(?=t)       identifies a h only if is followed by t, but t will not be part of the match
(?<=t)h      identifies a h only if is preceded by an t, but t will not be part of the match

NEGATION OPERATOR

h(?!t)       identifies a h only if is not followed by t, but t will not be within the match
(?<!t)h      identifies a h only if is not preceded by an t, but t will not be within the match


## Author

I'm a part-time student at UT Austin Coding Bootcamp in sight to become a Full Stack Developer. When I'm not
working or studying, I enjoy watching live music, traveling, being outdoors, and gaming.

Check out my github below!

https://github.com/nsherman113
