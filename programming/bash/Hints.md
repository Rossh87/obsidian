## Finding or listing files and directories
Doing this manually is tricky due to edge cases with links, permissions, etc. In scripts, it is often better to use `find` command and tune it to include/omit whatever you desire. For example, the following command will recursively list all subdirectories that are not named `__pycache__`, and are not descendants of a directory named `__pycache__`. The output can then be piped to other commands:
```bash
find "$1" -type d -not \( -name "__pycache__" -prune\)
```

## Checking for existence of files/directories
Further info:
https://linuxize.com/post/bash-check-if-file-exists/

The operators `-e`, `-d` and `-f` evaluate to a boolean. `-e` is `true` if anything (file or directory) exists at the tested path. The other two check specifically for file or directory. Pass these operators inside of a `test` statement, i.e. in single or double brackets. Negate with a bang: `!`. E.g.
```bash
$FILE = /etc/resolv.conf

# print if file exists
if [ -f "$FILE" ]; then
	echo "File exists"
fi
```

## Reading input line-by-line
Pipe to a `while read somevar`  loop. E.g.
```bash
# pass the second column of each line in some file to a processor
< "$1" awk '{print $2}' | while read columnvar
do
	process("$columnvar")
done
```