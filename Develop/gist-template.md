# Regular Expressions: Your Guide to Pattern Matching and Text Parsing

A regular expression, commonly abbreviated as regex or regexp, is a sequence of characters that defines a search pattern. It often includes capturing groups to extract specific portions of the matched text during a search within a given input text. For instance, when validating user-provided emails using a regular expression, we can check if the input conforms to the standard email structure. An example pattern to validate emails might be `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`. This pattern ensures that the email follows the structure `xxx@xx.xxx`.


## Summary

In this tutorial, I will dissect an email regex, or regular expression designed to match input adhering to fundamental email structure. I will explore the initiation and termination points of the sequence, as well as shedding light on the roles of characters enclosed within parentheses and brackets. This explanation aims to demonstrate how these character groups work collaboratively to define the three essential components of an email.

```
Email Regex: /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/
```

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)

## Regex Components

### Anchors

An anchor within a regular expression is used to define a required position that a string must occupy during pattern recognition. There are two primary types of anchors: 

1. Caret Anchor (^):
- Employed at the beginning of a sequence to designate the beginning of the line

2. Dollor Sign Anchor ($):
- Position at the end of an expression to assert the end of the line

 For example, consider the initial sequence in an email pattern, `^([a-z0-9_.-]+)`, where it asserts the position of lowercase letters, digits, underscores, dots, and hyphens at the beginning of the email address. This ensures strict positioning of the string to match the format of an email. Secondly, the dollar sign anchor, in a regular expression, serves to assert the adherence of input to be positioned at the very end of the sequence. For instance, consider the pattern `([\da-z\.-]+)\.([a-z\.]{2,6})$`, which is used for capturing the format of an email's domain name. In this example, the dollar sign specifies that the pattern of characters preceding it must occur at the very end of the input.

### Quantifiers

Quantifiers in a regular expression serve to specify the number of occurrences of a set of characters within the input string. There are six forms of quantifiers:

1. Asterisk (*)

2. Plus (+)

3. Question Mark (?)

4. Braces with one integer (x{2})

5. Braces with an integer followed by a comma (x{2,})

6. Braces with a range (x{2,6})

 In the specific example of the email expression, the Plus '+' quantifier is utilized twice—once at the beginning of the sequence `^([a-z0-9_\.-]+)`, and again at domain level of the email `@([\da-z\.-]+)`. The Plus quantifier, `used to define "one or more occurrences`," is employed to extend the matching of characters, allowing for any string in the given character classes to pass. This quantifier enables the capture of usernames and domains in the pattern.

### OR Operator

While the `OR operator (|)` is not utilized in the example provided, when incorporated into a regular expression, it `serves to construct a pattern that matches either the left or right side of the operation`. For instance, consider a scenario where you are searching for instances of either 'red' or 'blue' within a sequence. In this case, you could use the regex pattern `/red|blue/`. This grants flexibility in the search process, allowing you to identify occurrences of either 'red' or 'blue' within the given input.

### Character Classes

Character classes, `enclosed by square brackets []`, `serve to designate a range of characters to be matched within the search`. For example, in the email regular expression, `[a-z0-9_.-]` asserts that any lowercase letter `[a-z]`, digit `[0-9]`, underscore `[_]`, dot `[.]` or hyphen `[-]` is eligible within the sequence being searched. This method of defining characters for inclusion allows for a more flexible approach in crafting the desired character set.

### Flags

The email regular expression, although lacking a Flag, can be transformed by appending `[g]` after the sequence to include the `global flag method` `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/g`. This modification would change the pattern of the search to `find all occurences of email format within any given input`, as the topic example only searches for the first occurence of an email. 

```
const emailRegex = /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/

const input = 'For further inquiries please reach out at firstemail@gmail.com or at my second email secondemail@gmail.com'

const emailMatches = input.match(emailRegex);
console.log(emailMatches);

Output: (firstemail@gmail.com)
```

With the absence of the global flag, the console.log would return only the first email in the input variable, as the search breaks upon locating match. However, by including the global flag [g] in the regular expression 

```
const emailRegex = /^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/g

const input = 'For further inquiries please reach out at firstemail@gmail.com or at my second email secondemail@gmail.com'

const emailMatches = input.match(emailRegex);
console.log(emailMatches);

Output: (firstemail@gmail.com, secondemail@gmail.com)
```
 the console.log would return all occurences of email format, such as (kriselijahk1@gmail.com, secondemail@gmail.com).

### Grouping and Capturing

In a regular expression, `grouping and capturing` are `techniques employed to treat classes or multiple characters as a single unit`. This is achieved by `enclosing them in parentheses ()`. These parentheses not only serve as a means of grouping characters but are also utilized to capture matches for later access. By employing this approach, specific parts of a sequence that match a pattern can be gathered and extracted.

For instance, consider the email regular expression, which incorporates three instances of grouping and capturing. At the beginning of the sequence, `([a-z0-9_\.-]+)` is utilized to group the local part of the email address, capturing one or more lowercase letters, digits, underscores, dots, or hyphens. Subsequently, `([\da-z\.-]+)` groups the characters constituting the domain name, capturing one or more digits, lowercase letters, dots, or hyphens. Lastly, `([a-z\.]{2,6})` forms a capturing group for the top-level domain of the email, capturing between 2 and 6 lowercase letters or dots. This meticulous use of grouping and capturing enhances the precision and flexibility of the regular expression.

### Bracket Expressions

Bracket expressions, also known as character classes, are a means of specifying a set of characters that must match within a sequence. For more detailed information, `you can refer to the section on Character Classes`.

### Greedy and Lazy Match

Greedy and lazy in regular expressions `refer to the quantifiers that control how many characters the sequence should match`. Greedy quantifiers consist of 

1. Greedy Quantifiers:
- Asterisks (*)
- Plus (+)
- Question Mark (?)
- Curly Brackets ({})

By default, `these quantifiers will match as many characters as they can`. For example, if we modified the email regular expression to look like `/.*@.*\..*/`, it would match the entire local part of the email address until it reached the entire domain and top-level domain, returning something like `thisemail@gmail.com`. However, with

2. Lazy Quantifiers:
- Asterisks Question Mark (*?)
- Plus Question Mark (+?)
- Two Question Marks (??)
- Curly Brackets Question Mark ({}?)
 
 this `matches as few characters as possible`, and if were to replace our email regular expression as such `/.*?@.*?\..*?/`, an input as simple as t@g.c would match the sequence.

### Boundaries

In a regular expression, boundaries play a crucial role in defining the confines of a sequence. There are two primary forms of boundaries:

1. Word Boundary(\b):
- Defined by a '\b', asserts a position for the beginning and end of a word that is sought to be matched.
- This boundary is useful when trying to retrieve a word as a standalone product.

2. Line Start and End (^ and $);
- ^ marks the Start of a line, while $ desginates the End of a sequenece.
- Line and Start and End boundaries help to ensure that a match must consist of the entire line.

In the example regular expression `/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/`, only line Start and End boundaries are present. This `defines that a match for a sequenece must contain the all capturing groups`, allowing for leftover information to be redacted. For instacne, thisemail@gmail.com would be a match, whereas `thisemail` or `an email @gmail.com` would not, as it consists of addiontal infromation beyond our defined strutcure.

## Author

This tutorial was created by Kristion Kim. You can find more of my work on [GitHub](https://github.com/kimkristion)

