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

```
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
Functions shall be written as follows:

```
dosomething() {
  code here
}
```

Indentation
-----------
Indentation shall be two spaces, no tabs are to be used.

while, for and if
-----------------
Put `; do` and `; then` on the same line as `while`, `for`, or `if`.

Command substitution
--------------------
Use `$(command)` instead of backticks.

Test
----
Use `[`, not `test`.

Comments
--------
If a comment isn't necessary, don't put one there.

When a comment is necessary (something is happening that isn't necessarily evident), use `# comment` before the line that needs explanation.

If a comment is needed inline, use a tab character and use the normal comment formatting.

Quotes
------
Use `'` when no special characters need to be interpreted.

If special characters do need to be interpreted, use `"`. For example, a `${variable}` will need `"` and not `'`.

Structure and readability
-------------------------
A few things can be done to add structure and readability to the script.

Define major parts of the program with `## DESCRIPTION`. This should always have empty lines on the top and bottom of it, and use two hashes, a space, and an all-caps description.

Here's an example:

```

## CONFIGURATION

blue='#0000ff'

```

Split up things into functions that can be run at the end of the script. This improves the modularity of the program and makes it much more readable.

This is a work in progress!
---------------------------
If you see anything in here that just seems downright improper, or you think I'm missing something important, make a pull request!

I'm very open to improving this guide and my own coding style.
