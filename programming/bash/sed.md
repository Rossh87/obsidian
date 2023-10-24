Stands for 'stream editor'.

By default, writes to an output stream. Pass `-i` to perform updates in-place.

General format is `[address]command[options]`, where address can be any kind of matcher: a numeric line range, a regex test for a single line, or a combination of the two. The `command` is is a single letter, and some `commands` take additional `options`.

`-r` uses [extended regular expressions](https://www.gnu.org/software/sed/manual/html_node/Extended-regexps.html) Only difference is that the conditions in which certain characters are treated as special are reversed.

Always put the instruction set in single quotes so it doesn't be fucked by shell substitution/expansion.

Most of the time, the core instruction will look like this: `s/thing_to_replace/what_to_replace_with/`. 

Access positional regex capturing groups with an escaped integer in the substitution string. 

[Character classes](https://www.gnu.org/software/sed/manual/html_node/Character-Classes-and-Bracket-Expressions.html) are a convenient way to match character 'families'. Note that the bracketed character class must itself be in brackets, e.g.
```bash
# replace all numerals with capital X

# correct
sed 's/[[:digit:]]/X'

# incorrect
sed 's/[:digit:]/X'
```
On the other hand, a bracket expression, e.g. to express a range, only require single brackets. If it is not a range, any single character in the input line will match any single character in the bracket expression. If it *is* a range, any single character that sorts between the two characters of the range will be matched. E.g.
```bash
# match all lowercase letters and replace with numeral 1
sed 's/[a-z]/1'
```

To run multiple commands on the same intput line, place the commands in braces and separate each command with a semicolon, e.g.:
```bash
# Print each line that begins with the string 'foo', then replace it with the string 'replaced'
sed -n '/^foo/{p ; r replaced}'
```