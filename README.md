# comp2041-notes

WIP!

## Table of Contents

1. [Usage Statements](#usage-statements)
2. [Unix Filters](#unix-filters)
    * [`cat`](#cat)
    * [`grep`](#grep)
    * [`wc`](#wc)
    * [`tr`](#tr)
3. [Regular Expressions](#regular-expressions)

## Usage Statements

* `arg` or `<arg>` required argument
* `[arg]` optional argument
* `[arg]...` any number of arguments
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

### `grep`

Print lines that match a regular expression.

**Usage:** `grep [OPTION]... PATTERNS [FILE]...`

**Variations**

* `-G, --basic-regexp` interpret PATTERNS as basic regex (default)
* `-E, --extended-regexp` interpret PATTERNS as extended regex (`egrep`)
* `-F, --fixed-strings` interpret PATTERNS as fixed strings, not regex (`fgrep`)
* `-P, --perl-regexp` interpret PATTERNS as Perl-compatible regex
* `-r, --recursive` read all files under each directory recursively (`rgrep`)

**Useful Options**

* `-i, --ignore-case` ignore case in patterns
* `-v, --invert-match` invert matching to select non-matching lines only
* `-w, --word-regexp` select only lines containing matches that form whole words
* `-c, --count` print only the count of matching lines
* `-o, --only-matching` print only the matched parts of a matching line
* `-q, --quiet, --silent` do not write anything to standard output and immediately exit with status 0 if match found
* `-H, --with-filename` print also the file name for each match
* `-n, --line-number` prefix each output line with 1-based line number
* `-a, --text` process a binary file as if it were text
* `-f FILE, --file=FILE` obtain patterns from FILE, one per line

**Other**

* In basic regular expressions, characters `? + | {} ()` lose their special meaning
* Exit status is 0 if a match is found, otherwise it is 1
* Typically, PATTERNS should be **single quoted**
* If no FILE given, `rgrep` or `grep -r` or `grep -R` recursively searches the working directory
* `-L, --files-without-match` print only the name of each file with no matches
* `-l, --files-with-matches` print only the name of each file with matches

### `wc`

Print newline, word and byte counts for each file (and total counts if multiple files).

**Usage:** `wc [OPTION]... [FILE]...`

**Useful Options**

* `-c, --bytes` print byte counts (UTF-8 uses 1-4 bytes, ASCII uses 1 byte)
* `-m, --chars` print character counts
* `-l, --lines` print newline counts
* `-w, --words` print word counts
* `-L, --max-line-length` print maximum line length

### `tr`

Translate, squeeze and/or delete characters from (**only**) standard input.

**Usage:** `tr [OPTION]... SET1 [SET2]`

**Useful Options**

* ``
* ``
* ``

**Other**

*

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
