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

*An important quantifier to note is the `.*`. This is known as a "greedy modifier" as it will try to match as many character as it can. A common fix to this behavior is to change the quantifier to `.*?` as the question mark paired with a quantifier changes the behavior to "not greedy".

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

### Capturing Groups
When a regex matches a string, it assigns that string to a "group". However if there is an alternation `()` present, the matched contents are assigned their own "subgroup". These group can then be referenced in subsequent operations/code.
- `\w{3}(\d{2})\w{2}` is assigned "GROUP 0" and `\d{2}` matches are assigned "GROUP 1"
- Capture groups can be referenced by the syntax `$*group number*` (in find/replace operations) or `\*group number*` (Back Referencing)

### Back Referencing
When we want to reference a capture group within the same regex, we use a back reference.
- `(\d{3})[-.]\1` is a regex that looks for GROUP 1 `\d{3}` followed by a dash or period, followed by the same sequence of GROUP 1.

### Flags
Once we've created a regex, we can finalize its functionality/limits with something called a flag. Flags denote a certain behavior we want the regex to follow. They are places outside the slashes that wrap the regex `/regex/`.
- `g`stands for "global" and will not stop at the first set of characters in a string to match the regex
- `i` stands for "case-insensitive" and ignores case when trying to match characters in a string
- `m` stands for "multi-line" and will search each line of a multi-line string
- flags can be used alone or together