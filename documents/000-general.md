---
number:
version: 1.0.0-rfc.0
author: FichteFoll
pull_requests:
first_released:
last_modified: 2020-02-12
---

# General Guidelines

These guidelines apply to every syntax
and syntactic construct.


## Areas of Concern

- Base Scope
- Scope suffix
- Embedding


## Rationale

<!-- TODO Do we need a rationale? For this document in particular or all? -->


## Guidelines

### Base Scope

The base scope is applied to the entire region
lexed by a syntax definition as the very first scope.
Usually that will be the entire file,
but in the case of an embedded syntax
a region might have multiple stacked base scopes.
In the context of a file, however,
there will only be a single base scope
which is that of the syntax used to lex it initially.

The base scope must be a specialization
of the following three first-level sub-scopes:

- `text` shall be used
  for syntaxes that contain primarily prose text,
  such as markup languages
  and structured data formats.
  Text in such syntaxes is spell-checked
  and auto completion is disabled while typing.

- `source` shall be used
  for programming languages containing
  instructions for a compiler, an interpreter, or similar.
  Text in such syntaxes usually has special meaning,
  is not spell-checked and auto completions are enabled

- `embedding` special use case for syntaxes
   that are embedded later into the file.
   The effect of an `embedding` scope is mostly transparent
   and the text vs. source decision
   is deferred to the following scope name.

The second sub-scope level of the scope name
should be based on the
Alphanumeric representations should be preferred.
A notable exception is `source.c++`.

### Scope Suffix

<!-- TODO -->

### Embedding

<!-- TODO -->


## Examples

- **Plain text** without any special syntax uses the base scope `text.plain`.
- **HTML** is a text-based markup language and uses `text.html`.
  Because a lot of other markup formats are based on HTML,
  it is further specified as `text.html.basic`
  to allow targeting the base syntax specifically.
- **Markdown** is a superset of HTML and uses `text.html.markdown`.
  Further specializations of markdown may add another scope level,
  such as `text.html.markdown.gfm`.

---

For the C programming language, the base scope should be `source.c` and for certain iterations of the language, the scope can be further specialized using `source.c.99`.
C++ is a different language and uses `source.c++`.

---

Php files are essentially HTML files
with template sequences for inline code execution.
Because of this,
`embedding.php` is used as the base scope
and `text.html.basic` is the next scope name
immediately pushed onto the stack.
Embedded Php segments,
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

- What should the opening and closing punctuation of Php tags be scoped as?
  Should it be scoped as `source.php`?
- Where do we mention that scope names are lower-case
  and use hyphens to separate words?
  What about numeric sub-scopes?
