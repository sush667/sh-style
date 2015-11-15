jschx's sh style guide
======================

This is sort of an experiment in standardizing my coding style.

I'm going to try to follow this from now on with all of my scripts.

Parts of this guide are based off of the [Google Shell Style Guide](https://google-styleguide.googlecode.com/svn/trunk/shell.xml).

What should I script with?
--------------------------
Preferably POSIX sh. Avoid bashisms.

File extensions
---------------
No file extensions shall be used.

Header formatting
-----------------
Example header formatting:

```sh
#!/bin/sh
#
# barstatus - output info in a lemonbar-readable format
#
```

The first line is the shebang, which will preferably use /bin/sh.

If bash is needed, use `#!/usr/bin/env bash` instead.

The next line will be a single #.

The third line will have the name of the script, a dash (-), and then a short description of what the script is intended to do.

Functions
---------
Functions shall be written using parentheses instead of using the `function` prefix. Example:
```sh
# Good
my_function() {
  # code here
}

# Bad
function my_function {
  # code here
}

# Bad again
function my_function() {
  # code here
}
```

Indentation
-----------
Indentation shall be two spaces, no tabs are to be used. Example:
```sh
# Good
error() {
  echo "$*" >&2
}

# Bad
error() {
        echo "$*" >&2
}
``` 

while, for and if
-----------------
Put `; do` and `; then` on the same line as `while`, `for`, or `if`. For example:
```sh
# Good
while true; do
  echo 'foo'
done

# Bad
while true
do
  echo 'foo'
done
```

case
----
Case options should be indented two spaces. If the option's function is only one line, put it on the same line as the option, and follow it with the standard double semicolons on that line as well. If it is two or more lines, start a new line and indent two more spaces. The two semicolons will be on the last line of the function. Example:

```sh
case "${opt}" in
    f) ful='true' ;;
    h)
      usage
      exit 0 ;;
    s) sel='true' ;;
    *)
      usage
      exit 1 ;;
esac
```

Command substitution
--------------------
Use `$(command)` instead of backticks. Example:
```sh
# Good
echo "Today is $(date +%x)"

# Bad
echo "Today is `date +%x`"
```
This allows for more readable nesting of command substitution, because you need to escape nested backticks. Example:
```sh
# Good
command_one $(command_two) $(command_three))

# Bad
command_one `command_two \`command_three\``
```

Test
----
Use brackets, a.k.a: `[` instead of `test`. Use the enhanced double brackets `[[` if you're using bash. Example:
```sh
# Bash
[[ -f FILE1 && -f FILE2 ]] && echo 'The files are there!'

# Good
[ -f FILE1 ] && [ -f FILE2 ]] && echo 'The files are there!'

# Bad
test -f FILE1 && test -f FILE2 && echo 'The files are there!'
```

Comments
--------
If a comment isn't necessary, don't put one there.

When a comment is necessary (something is happening that isn't necessarily evident), use `# comment` before the line that needs explanation.

If a comment is needed inline, use a tab character and use the normal comment formatting.

Quotes
------
Use single quotation marks `'` if variable interpolation isn't being used.

If interpolation is being used, double quotation marks `"` are necessary . For example, a `${variable}` will need to be quoted around `"` instead of `'`. Example:
```sh
VAR=5

echo "The number is ${VAR}"
# The number is 5

echo 'The number is ${VAR}'
# The number is ${VAR}
```

Structure and readability
-------------------------
A few things can be done to add structure and readability to the script.

Define major parts of the program with `## DESCRIPTION`. This should always have empty lines on the top and bottom of it, and use two hashes, a space, and an all-caps description.

Here's an example:

```sh

## CONFIGURATION

blue='#0000ff'

```

Split up things into functions that can be run at the end of the script. This improves the modularity of the program and makes it much more readable.

This is a work in progress!
---------------------------
If you see anything in here that just seems downright improper, or you think I'm missing something important, make a pull request!

I'm very open to improving this guide and my own coding style.
