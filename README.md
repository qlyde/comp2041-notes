# comp2041-notes

## Usage Statements

* `arg` or `<arg>` required argument
* `[arg]` optional argument
* `[arg...]` any number of arguments
    * `arg...` one or more arguments
* `[arg1 | arg2]` mutually exclusive arguments (optional)
    * `{arg1 | arg2}` mutually exclusive arguments, one of which is required
* `[-n number]` option with operand `number`
* `[-n]` option without operands

## Unix Filters

### `cat`

Concatenate FILE(s) to standard output.

**Usage:** `cat [OPTION]... [FILE]...`

**Useful Options**

* `-A, --show-all` display non-printing characters
* `-n, --number` number all output lines, starting from 1
* `-s, --squeeze-blank` squeeze consecutive blank lines into one
* `-T, --show-tabs` display TAB characters as `^I`

**Other**

* With no `FILE`, or when `FILE` is `-`, read standard input
* `tac` concatenates and prints files in *reverse*

## Regular Expressions

Every regular expression can be written using only `() * | \`.

### Quantifiers

* `*` 0 or more
* `+` 1 or more
* `?` 0 or 1
* `{n}` exactly n
* `{n,}` n or more
* `{n,m}` n to m (inclusive)

### Groups and Ranges

* `.` any character except `\n`
* `(...)` group
* `(a|b)` a or b (**alternation** or OR operand)
* `[abc]` any one of a, b or c
* `[^abc]` any one **not** a, b or c
* `[a-z]` a to z (inclusive)

### Anchors

* `^` start of string/line
* `$` end of string/line
* `\b` word boundary
* `\B` not word boundary

### Character Classes

* `\s` white space
* `\S` not white space
* `\d` digit
* `\D` not digit
* `\w` word
* `\W` not word

### Other

* `\` escape (remove special meaning from) following character
* `[[:upper:]]` upper case letters
* `[[:lower:]]` lower case letters
* `[[:alpha:]]` letters
* `[[:digit:]]` digits
* `[[:alnum:]]` letters and digits
* `[[:blank:]]` space and tab

redirection
pipelines
