---
number: 1
version: 1.0.0
author: FichteFoll
pull_requests: [3]
published: 2021-01-10
last_modified: 2020-11-15
---

# Base Scope

These guidelines apply to a syntax definition's base scope,
which is applied to the entire document
highlighted using that syntax.
Additionally, the scope suffix,
usually based on the base scope,
is explained.


## Areas of Concern

- Base Scope
- Scope suffix


## Rationale

To classify a document type,
every syntax specifies a base scope name,
which is applied to the entire document
highlighted as that syntax.
The base scope can be used
to differentiate between, for example,
(mostly) prose text documents
and documents containing instructions (*source code*).

Furthermore,
to identify which syntax a certain token is matched from (or as),
every scope name should use a semi-unique scope suffix
that is appended as the last sub-scope.


## Guidelines

### Base Scope

The base scope is applied to the entire region
lexed by a syntax definition as the very first scope.
Usually that will be the entire file,
but in the case of an embedded syntax,
a region might have multiple stacked base scopes.
In the context of a file, however,
there will only be a single base scope
which is that of the syntax used to lex it initially.

The base scope must be a specialization
of the following three first-level sub-scopes:

- `text` shall be used
  for syntaxes that contain primarily prose text,
  such as markup languages
  and structured data formats
  with a focus on text.
  Text in such syntaxes is spell-checked
  and auto completion is disabled while typing.

- `source` shall be used
  for programming languages containing
  instructions for a compiler, an interpreter, or similar.
  Text in such syntaxes usually has special meaning,
  is not spell-checked and auto completions are enabled.

- `embedding` is a special use case for syntaxes
   that are embedded later into the file.
   The effect of an `embedding` scope is mostly transparent
   and the text vs. source decision
   is deferred to the following scope name.

The second sub-scope level of the scope name
should be the syntax name itself
in lower-case alphanumeric characters.
A notable exception is `source.c++`.


#### Specialized Base Scopes

When implementing syntax highlighting
for a dialect of a different syntax,
for example a special syntax
for JSON documents
or a Bash-like shell scripting language,
a third-level scope can be introduced
to indicate that a syntax is a specialization of the base.
Examples include Markdown being a specialization of HTML
or Zsh being a specialization of Bash,
resulting in `text.html.markdown`.
If the syntax for the base is known to be specialized,
it may opt to use the `basic` sub-scope
instead of simply omitting it.


### Scope Suffix

A scope suffix is used for individual tokens.
The suffix is appended to every scope name
that is assigned to a token,
but there may only be a single sub-scope suffix per scope name.

It serves two purposes:

1. It allows to differentiate between syntaxes on a token level
   and is thus the more precise way to select a certain token only
   because it still works when two syntaxes are combined.
   Most importantly, it works for embedded sections
   and allows to separate tokens of the base syntax from a specialized syntax.

2. It marks the end of a scope name,
   meaning the scope name does not have any further sub-scopes,
   which allows for more accuracy during testing.

Scope suffixes of specialized syntaxes
either only use the last sub-scope of the base scope,
or the base and the specialized name are joined using a hyphen,
if it would be ambiguous otherwise.
A single syntax definition may use different scope suffixes
when it is a specialization or an extension of another syntax.


## Examples

- **Plain text** without any special syntax uses the base scope `text.plain`.
  Since no lexing is performed for plain text,
  no scope needs to be assigned,
  but if there were any,
  their suffix would be `text`.
  *This is a special case.*

- **HTML** is a text-based markup language and uses `text.html`.
  Because a lot of other markup formats are based on HTML,
  it is further specified as `text.html.basic`
  to allow targeting the base syntax specifically.
  The suffix is `html`.

- **Markdown** is a superset of HTML and uses `text.html.markdown`.
  Further specializations of markdown may add another scope level,
  such as `text.html.markdown.gfm` for [GitHub Flavored Markdown][GFM].
  Depending on which syntax a token or a sequence of tokens is specified in,
  the suffix could be either of `html`, `markdown`, or `gfm`.

[GFM]: https://github.github.com/gfm/

---

- **C** uses a base scope of `source.c`.
  For certain iterations of the language,
  the scope can be further specialized using `source.c.99`.

- **C++** is a different language from C and uses `source.c++`.
  (This is the exception, not the rule.)

- **C#** is a different language from C and C++ and uses `source.cs`.

---

- **PHP** files are essentially HTML files
  with template sequences for inline code execution.
  Because of this,
  `embedding.php` is used as the base scope
  and `text.html.basic` is the next scope name
  immediately pushed onto the stack.
  Embedded PHP segments,
  indicated by `<?` or `<?php`,
  use `source.php.embedded`,
  which results in the following example:

  ```php
  <? echo 'hello worlds'; ?>
  <!-- ^ embedding.php text.html.basic meta.embedded.line.php source.php.embedded … -->
  ```


## Previous Usages

None.


## Unresolved Questions

None.
