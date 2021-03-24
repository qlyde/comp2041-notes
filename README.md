# comp2041-notes

WIP!

## Table of Contents

1. [Usage Statements](#usage-statements)
2. [Unix Filters](#unix-filters)
    - [`cat`](#cat)
    - [`grep`](#grep)
    - [`wc`](#wc)
    - [`tr`](#tr)
    - [`head`](#head)
    - [`tail`](#tail)
    - [`cut`](#cut)
    - [`sort`](#sort)
3. [Regular Expressions](#regular-expressions)

## Usage Statements

* `arg` or `<arg>` required argument
* `[arg]` optional argument
* `arg...` one or more repetitions of `arg`
* `[arg]...` any number of repetitions of `arg`
* `[arg1 | arg2]` mutually exclusive arguments (optional)
* `{arg1 | arg2}` mutually exclusive arguments, one (and only one) of which is required
* `[-n number]` option with operand `number`
* `[-n]` option without operands

## Unix Filters

### `cat`

Concatenate file(s) to standard output.

**Usage:** `cat [OPTION]... [FILE]...`

**Useful Options**

* `-A, --show-all` display non-printing characters
* `-n, --number` number all output lines, starting from 1
* `-b, --number-nonblank` number non-empty output lines, overrides `-n`
* `-s, --squeeze-blank` squeeze consecutive blank lines into one

### `grep`

Print lines that match pattern(s).

**Usage:** `grep [OPTION]... PATTERNS [FILE]...` or `grep [OPTION]... -f PATTERN_FILE [FILE]...`

* Typically, `PATTERNS` should be **single-quoted** to avoid misinterpretation
* Variant programs `egrep`, `fgrep` and `rgrep` are deprecated, instead use `-E`, `-F` and `-r` respectively

**Useful Options**

*Pattern Syntax*

* `-G, --basic-regexp` interpret `PATTERNS` as basic regex (default)
    - In basic regular expressions, characters `? + | {} ()` lose their special meaning
* `-E, --extended-regexp` interpret `PATTERNS` as extended regex (`egrep`)
* `-F, --fixed-strings` interpret `PATTERNS` as fixed strings, not regex (`fgrep`)
* `-P, --perl-regexp` interpret `PATTERNS` as Perl-compatible regex

*Matching Control*

* `-f FILE, --file=FILE` obtain patterns from `FILE`, one per line
* `-i, --ignore-case` ignore case distinctions in patterns and input data
* `-v, --invert-match` invert matching to select non-matching lines only
* `-w, --word-regexp` select only lines containing matches that form whole words
* `-x, --line-regexp` select only those matches that match the whole line
    - Equivalent to wrapping a regular expression pattern with `^(...)$`

*General Output Control*

* `-c, --count` print only the count of matching lines
* `-L, --files-without-match` print only the name of each file with no matches
* `-l, --files-with-matches` print only the name of each file with matches
* `-o, --only-matching` print only the matched parts of a matching line
* `-q, --quiet, --silent` do not write to standard output and immediately exit with status 0 if match found

*Output Line Prefix Control*

* `-H, --with-filename` print also the filename for each match
* `-n, --line-number` prefix each output line with 1-based line number

*File and Directory Selection*

* `-a, --text` process a binary file as if it were text
* `-r, --recursive` read all files under each directory recursively (cwd if none specified) (`rgrep`)

### `wc`

Print newline, word and byte counts for each file (and total counts if multiple files).

**Usage:** `wc [OPTION]... [FILE]...`

**Useful Options**

* `-c, --bytes` print byte counts
    - UTF-8 uses 1-4 bytes per character, ASCII uses 1 byte per character
* `-m, --chars` print character counts
* `-l, --lines` print newline counts
* `-w, --words` print word counts
* `-L, --max-line-length` print maximum line length

### `tr`

Translate, squeeze and/or delete characters from (**only**) standard input.

**Usage:** `tr [OPTION]... SET1 [SET2]`

* Each character in `SET1` is translated/mapped to the **corresponding** character in `SET2`
    - `tr 'abc' 'xyz'` maps 'a' to 'x', 'b' to 'y' and 'c' to 'z'
* If `SET2` is shorter than `SET1`, then the last character in `SET2` is used to map the remainder of `SET1`
* If `SET2` is longer than `SET1`, then excess characters in `SET2` are ignored
* Sets interpret certain sequences:
    - `\\` backslash
    - `a-z` is 'a' to 'z'
    - `[a*]` in `SET2` copies 'a' until length of `SET1`
    - `[:upper:]`, `[:lower:]`, etc

**Useful Options**

* `-c, -C, --complement` use the complement of `SET1`
* `-d, --delete` delete characters in `SET1` instead of translating
* `-s, --squeeze-repeats` squeeze (after translation/deletion) repeated characters in last specified set into one

### `head`

Print the first 10 lines of each file to standard output.

**Usage:** `head [OPTION]... [FILE]...`

**Useful Options**

* `-n NUM, --lines=NUM` print the first `NUM` lines instead of the first 10

### `tail`

Print the last 10 lines of each file to standard output.

**Usage:** `tail [OPTION]... [FILE]...`

**Useful Options**

* `-n NUM, --lines=NUM` print the last `NUM` lines instead of the last 10

### `cut`

Print selected parts of lines from each file to standard output.

**Usage:** `cut OPTION... [FILE]...`

* Use only **one** of `-f` or `-c`

**Useful Options**

* `-d DELIM, --delimiter=DELIM` use `DELIM` instead of TAB to delimit fields
    - `DELIM` should be single-quoted to avoid misinterpretation
* `-f LIST, --fields=LIST` select only these fields
    - `-fN` select field `N`
    - `-fN-` select field `N` and onward
    - `-f-N` select fields 1 to `N`
    - `-fN-M` select fields `N` to `M`
    - `-fN,M` select fields `N` and `M`
* `-c LIST, --characters=LIST` select only these characters
    - `-cN` select character `N`
    - `-cN-` select character `N` and onward
    - `-c-N` select characters 1 to `N`
    - `-cN-M` select characters `N` to `M`
    - `-cN,M` select characters `N` and `M`
* `--complement` print the complement of selected characters/fields
* `-s, --only-delimited` do not print lines not containing delimiters
* `--output-delimiter=STRING` use `STRING` as the output delimiter instead of the input delimiter

### `sort`

Write sorted concatenation of all file(s) to standard output.

**Usage:** `sort [OPTION]... [FILE]...`

**Useful Options**

* `-n, --numeric-sort` sort numerically instead of lexicographically
    - 1, 10, 2 is sorted lexicographically but 1, 2, 10 is sorted numerically
* `-r, --reverse` reverse result of comparisons
* `-k KEYDEF, --key=KEYDEF` sort via a key
    - `KEYDEF` is `F[.C][OPTS][,F[.C][OPTS]]`
    - `F` is a field number
    - `C` is a character position in the field
* `-t SEP, --field-separator=SEP` use SEP instead of non-blank to blank transition
    - `SEP` should be single-quoted to avoid misinterpretation, eg. `-t|` fails but `-t'|'` does not
* `-d, --dictionary-order` only consider blanks and alphanumeric characters
* `-f, --ignore-case` ignore case when sorting
* `-b, --ignore-leading-blanks` ignore leading blanks when sorting
* `-R, --random-sort` shuffle

## Regular Expressions

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
* `(a|b)` a or b (**alternation**)
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
* `[[:blank:]]` space and TAB

redirection
pipelines
which whereis whatis find locate
