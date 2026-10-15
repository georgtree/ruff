# Ruff! documentation generator

Ruff! (Runtime function formatter) is a documentation generation system
for programs written in the Tcl programming language. Ruff! uses runtime
introspection in conjunction with comment analysis to generate reference
documentation for Tcl programs with minimal effort on the programmer's part.

See https://ruff.magicsplat.com for features and reference documentation. Source
repository lives at https://github.com/apnadkarni/ruff.

## Why Ruff!

Ruff! produces documentation that not only requires less duplication
of effort from the programmer, but is also more complete, more
accurate and more maintainable.

* Comments in source code do not have to be reproduced for documentation
purposes.

* Ruff! requires minimal markup in the comments making it lightweight
as well as reducing clutter.

* Supports inline formatting using Markdown syntax.

* Embedded diagrams in multiple formats

* Program elements like command arguments, defaults and
class relationships like inheritance are automatically derived.

* Maintenance is less of a burden as documentation is automatically
updated with source modification such as changes to defaults, addition of
mix-ins etc.

On the output side,

* Ruff! supports multiple output formats (HTML, Markdown, Sphinx, Asciidoc
and nroff).

* Generated documentation can optionally be split across multiple pages.

* Hyperlinks between program elements, and optionally source code,
make navigation easy and efficient.

* A table of contents and optional searchable index permits quick
location of command and class documentation.

* Class relationships are extracted and the full API for a class, with inherited
and mixed-in methods and properties, is flattened and summarized.

* HTML output supports navigation and user-selectable themes with source highlighting.

For additional examples of Ruff! generated documentation, see

[iocp](https://iocp.magicsplat.com),
[cffi](https://cffi.magicsplat.com),
[CAWT](http://www.cawt.tcl3d.org/download/CawtReference.html),
[MAWT](https://www.tcl3d.org/mawt/download/MawtReference.html),
[PAWT](https://www.tcl3d.org/pawt/download/PawtReference.html),
[SpiceGenTcl](https://georgtree.github.io/SpiceGenTcl/),
[apave](https://aplsimple.github.io/en/tcl/pave/apave.html),
[baltip](https://aplsimple.github.io/en/tcl/baltip/baltip.html),
[hl-tcl](https://aplsimple.github.io/en/tcl/hl_tcl/hl_tcl.html),
[tcl-promise](https://tcl-promise.magicsplat.com),
[tomato](https://nico-robert.github.io/tomato/),
[obex](https://tcl-obex.magicsplat.com),
[Woof!](http://woof.sourceforge.net/woof-ug-0.5/html/_woof/woof_manual.html)
and
[tcl-vix](https://tcl-vix.magicsplat.com/).

## Release notes for 3.1.0

* Syntax highlighting support (thanks to Nicolas Robert)

## Release notes for 3.0.4

* Avoid flash when loading dark pages

## Release notes for 3.0.3

Note this is a major release and there may be subtle incompatibilities with
2.x releases in both parsing of input and generated output.

* New output formats reStructuredText (Sphinx) and Asciidoc
* New command `coverage` to list undocumented or partially documented components
* New command line interface *2.x incompatibility*
* Support for numbered lists
* Support for block quotes
* Support for tables
* Support for HTML entities
* Include OO class methods in documentation
* Provision for class preambles, oo::configurable property descriptions and
  Tk-like option documentation via `_ruffClassHook_` (Tcl 9 only)
* Customizable namespace headings
* Customizable per-namespace options
* New `-onlyexports` / `--only-exports` option to only document exported commands
* Order in which class and command sections are displayed is now based
  on the `-include` / `--include` option
* Program elements in navigation pane now use a monospace font.
* Tcl core built-ins are ignored when documenting global namespace (bug fix)
* The `document` command no longer supports supports the `-preeval` option. Do any
  required evaluation in the caller before invoking `document`.
  *2.x incompatibility*

## Release notes for 2.7

* Added a copy button for fenced blocks (thanks to Nicolas Robert).

## Release notes for 2.6

* Added `#ruff includeformatters|excludeformatters` directives to include or
exclude content for specific formatters (thanks to George Yashin).

## Release notes for 2.5

* Better documentation of TclOO properties to include custom
setter/getter descriptions
* Bug fixes in nroff output.

## Release notes for 2.4

* Support for TclOO properties in Tcl 9
* Support for language specifier in fenced blocks

## Release notes for 2.3

* Collapsible details section for procedure description option when
`-compact 1` is specified. Note generated output with `-compact 1` has changed.
* Bug fix. Ensure diagrams fit in page width
* Bug fix. Index page tooltip synopsis visibility in dark themes.

## Release notes for 2.2

* Support for embedded text formatted diagrams (ditaa, PlantUML etc.)
* Alignment and linkable numbered captions for fenced blocks and diagrams.
* Fixed minor display artifacts.

## Release notes for 2.1

This release mainly has cosmetic changes in presentation.

* Ensemble command includes table to subcommands.
* Show command synopsis in navigation pane tooltip.
* Tweaks to themes and navigation.
* Bug fix: broken link to index page.

## Release notes for 2.0

* Added Nroff formatter for Unix manpages.
* Added themes with end-user selection.
* Added end-user control for positioning navigation pane.
* Classes defined with metaclasses are recognized.
* Proc and method synopsis overrides, for example
  to distinguish invocation options.
* Web assets are linked by default (option `-linkassets`) instead
  of being embedded.
* **Incompatibility:** Generated HTML and CSS templates have changed
  and require modern browsers (no Internet Explorer support).
* **Incompatibility:** The `-stylesheets` option is not supported.
* **Incompatibility:** The `-navigation` option only takes `scrolled`
  `sticky` as valid values.
* **Incompatibility:** The `-output` option is not supported. Use
  `-outfile` and `-outdir` instead.
* **Incompatibility:** Output file names use hyphen as a separator
  instead of underscore.
* [Bug fixes](https://github.com/apnadkarni/ruff/issues?q=is%3Aissue+is%3Aclosed+milestone%3Av2.0+label%3Abug)


NOTE 2.0 HAS SEVERAL INCOMPATIBILITIES VIS-A-VIS 1.x IN OPTIONS AND GENERATED
OUTPUT FORMAT. See above Release notes for 2.0.

## Nroff tables

Nroff output renders tables as wrapped Unicode boxes, without requiring `tbl`.
This works in document and namespace preambles, class preambles, procedure
comments and method comments. Use normal Ruff table syntax; separate preamble
conversion or temporary procedure rewriting is unnecessary.

```tcl
ruff::document ::mypackage -format nroff -tablewidth 100
```

`-tablewidth` includes borders and padding and defaults to 120 character columns.
The CLI equivalent is `--nroff-table-width 100`. Cells wrap to fit, and column
alignment markers are honored. Inline code and emphasis become plain text inside
tables; links retain their labels and URLs. Use a UTF-8 manpage reader with a
monospaced font. Widths count Tcl characters, so wide and combining Unicode
characters may not align with terminal display columns.

Run the Tcl regression tests from the repository root:

```sh
tclsh tests/nroff-tables.test
```

Tcllib must be available on `auto_path` or `TCLLIBPATH`. Tcl 9 enables the class
preamble integration test. If `groff` is available, the suite also checks rendered
UTF-8 man output without a table preprocessor.

## Inline math

Append `{math}` directly to a backtick span:

```text
The coordinate `x_1`{math} and ratio `\frac{x_1}{x_2}`{math "x_1/x_2"}.
```

This works in prose, parameter descriptions and tables, including namespace/class
preambles and procedure/method documentation. The optional quoted or braced text
is the nroff fallback; without it, nroff prints the TeX source. Ordinary code spans
and fenced examples remain unchanged.

Sphinx emits `:math:` roles; enable `sphinx.ext.mathjax` or `sphinx.ext.imgmath` in
`conf.py`. Standalone HTML loads MathJax on pages containing inline math; use
`-mathjaxpath` (CLI `--mathjax-path`) to select a local/custom script, or an empty
value to leave script loading to the hosting page. Markdown emits dollar-delimited
math, and AsciiDoc emits LaTeX STEM macros; the consuming renderer must support them.

Run `tclsh tests/inline-math.test` and `tclsh tests/nroff-tables.test` with Tcllib
available. The inline suite also builds Sphinx HTML when `sphinx-build` is on PATH.

## Display math

Use a fenced `math` block containing TeX without surrounding display delimiters:

````text
```math
\Delta x = \frac{x_1}{x_2}
```
````

HTML renders it with MathJax, Markdown emits `$$` blocks, and AsciiDoc emits LaTeX
STEM blocks. Sphinx retains its native `.. math::` output. Standalone HTML uses the
same `-mathjaxpath` option as inline math; Sphinx uses its own `conf.py` settings.

Nroff keeps the TeX as literal text. Use `#ruffopt excludedformats nroff` for the
math block and `#ruffopt includedformats nroff` for your existing text equation,
then restore the enclosing format selection. Other code fences remain unchanged.

Run `tclsh tests/display-math.test` for the display-math regression suite.

## Standalone raw HTML

Standalone HTML blocks are preserved in HTML and Markdown output and emitted as
`.. raw:: html` directives in Sphinx output. Other formatters omit them. Inline
HTML support is unchanged.

For example, the same disclosure markup can be used in a GitHub README and a
Ruff preamble:

```markdown
<details>
<summary>Interactive demonstration</summary>

![Demonstration](images/demo.gif)

</details>
```

A complete opening or closing tag on its own line starts a block; an opening
and closing tag with content on the same line is also accepted. HTML comments
can start blocks too. Blocks end at a blank line or EOF. Keep blank lines around
Markdown content: everything within a raw block is passed through literally.
Ruff does not validate or balance HTML tags. Tags in fenced or indented code
remain examples. Format inclusion guards still apply.

Non-HTML output omits the entire raw block, including summary text. Put any
portable description in a separate Markdown paragraph. Sphinx must allow raw
content for its HTML builder to display it.

Run `tclsh tests/raw-html.test` with Tcllib available. The suite also checks
Sphinx HTML generation and image copying when `sphinx-build` is on PATH.
