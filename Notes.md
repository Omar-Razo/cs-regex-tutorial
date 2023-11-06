# Regex

- "a sequence of characters that defines a search pattern"
- composed of different kinds of characters

## Character Type: Literal Characters
Literal characters represent the same value they are. 
- `s` stands for "lowercase s" (they are case sensitive)

## Character Type: Meta Characters

#### Single Meta Characters
Single characters that reprsent a more general type of character.
- `\d` stands for any digit (0-9)
- `.` stands any character
- `\w` stands for any chracter found in a word (string?) (A-Za-z0-9_)
- `\s` stands for any whitespace (spaces, tabs, etc)

*The capital version of a meta means the inverse or rather everything not in the meta chracter's range (kinda like `!\d`).

#### Anchors/Position Characters
Special characters that signify things like the start and end of a string (or word).
- `^` stands for beginning of a string/starts with subsequent characters
- `$` stands for end of string/ends with previous characters
- `\b` stands for 'word boundry' and denotes the start or end of a word

#### Quantifiers
Characters that declare/specify an amount/range of the previous character.
- `*` stands for 0 or more of the previous character
- `+` stands for 1 or more of the previous character
- `?` stands for 0 or 1 (think of like "previous character optional")
- `{a, b}` stands for a range (a = min, b = max) (single number = exact amount)

#### Character Classes
A set of characters, denoted by brackets `[*some characters*]`, any of which will achieve a match with an input string. They allow for precise searches. Single character meta characters can be considered character classes.
- `\d` and `\w` are equivalent to `[0-9]` and `[A-Za-z0-9_]` respectively

It's worth noting that there are some interactions between certain meta characters inside character classes.
- `[-.]` looks for either a dash `-` or a period `.` (period loses its stand-in for "any character")
- Additionally, if a dash `-` is the first character in the character class, it is literal. If it is not, its meaning changes to be the range between the character before it and after it (Ex: `[a-z]` means any letter between `a` and `z`).
- `^` inside a character class negates its contents (Ex: `[^a-z]` means any character not `a` through `z`).
*The brackets `[]` and other meta characters can be "escaped" by adding a `\` in front of the character you are intending to be a literal character.

#### Alternations
Another way to group target characters but includes a logical operator (OR expressed as `|`). The characters inside are literal, unless placed within a character class.
- `\.(com|net|gov)` matches an escaped period `\.` and one of the 3-letter combinations inside the alternation

###