# mathjs_examples
Examples notes(in markdown) including math.js markdown code blocks(tested on Math Mode plugin for Joplin mobile - Android). 

The notes can contain indexes(TOC - table of contents) and KaTeX formulas that don't render in GitHub by default. They render on Joplin with toc and KaTeX features enabled on its settings.

Math.js code is evaluated in a Math.js parser environment and that fact causes some limitations on what can be parsed/evaluated successfully, as opposed to evaluation in a browser environment.

On this kind of environment, MathJS uses 1-based indexing(for indexes and dimensions - that is, they start at 1 instead of 0).

Common dimensions are:

- 1 for Vertical(Rows).
- 2 for Horizontal(Columns).
