# :watermelon: templa

A simple and *very* stupid [template engine](https://en.wikipedia.org/wiki/Template_processor).

It executes **scripts** embedded in **template files** and substitutes their output in-place.

## Principle

*templa* processes **template files** and generate **output files** according to the following principle:

Any segment of a file between a line that starts with `#!` (a *shebang*, possibly indented) and a line that ends with `!#` (or the end of the file) is considered an **embedded script**.

This embedded script is isolated in a temporary file, with the proper amount of indentation removed and the final `!#` stripped, and executed. The standard output of that program is added to the output file, replacing the embedded script.

A literal `#!` can be escaped with `##!`.

## Example

#### Input
```html
<h1>Files</h1>
<ul>
    #!/bin/bash
    for file in *; do
        printf '<li>%s</li>\n' "$file"
    done !#
</ul>
```

#### Output
```html
<h1>Files</h1>
<ul>
    <li>LICENSE</li>
    <li>Makefile</li>
    <li>README.md</li>
    <li>templa</li>
    <li>templates</li>
</ul>
```

----------

To see a live example, check out `templates/README.md`.

## Installing

*templa* requires **Bash version 4** or later, as well as **GNU coreutils**. These should be present on most GNU/Linux systems.

Clone this repository on your system and copy the `templa` executable to some location in your PATH, e.g. `/usr/local/bin` or `~/.bin`.

## Using

    Usage: templa [-hq] templates target
        Render the templates from TEMPLATES to the TARGET directory.
    
    Options:
        -h  Show this help message.
        -q  Quiet mode, don't print anything.

## :balance_scale: License

This software is distributed under the terms of the [GNU GPL v3](https://www.gnu.org/licenses/).  See `LICENSE`.
