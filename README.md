# Icalia Python Praxis

Code style Conventions, defaults, etc for our python projects

## Before you continue reading

This document (and repo) is meant to follow up / add to the
[Icalia Guides](https://github.com/IcaliaLabs/guides). Please read it first,
until we figure out how to merge this info back to the guides project.

## General Considerations (all languages)

Code is meant to be read and understood by humans, and coding is (still) a human
process after all. Therefore, the first and foremost priority for **all** code
being done in Icalia Labs must be **readable** so it's easy to understand. This
goal takes precedence over any other consideration. There are a lot of sources
on how to make good, readable code. I'd recommend a book called
[The Art of Readable Code](https://www.amazon.com/dp/0596802293).

There are *some* aspects of good readable code that can be detected/checked for
with tools called "Static Code Analyzers". We will be using codeclimate CLI to
check our code before submitting a pull request for review.

There are some tools that can be added (or be already present in) to a project -
such as Rubocop, flake8, eslint, etc. We will prefer using codeclimate CLI as
the main code-checking tool, as it is platform-independent, performs
language-independent checks, and in most cases the other tools are available as
plugins within codeclimate.

### Maintainability

We should always avoid the following maintainability issues, regardless of the
project's language and/or framework:

* **High Argument Count (Max: 4):** Methods or functions defined with a high
  number of arguments.
* **Complex logic (Max: 4):** Boolean logic that may be hard to understand
* **File length (Max: 250):** Excessive lines of code within a single file. Does
  not apply to automatically-generated code (i.e. schema.rb, etc)
* **Method complexity (Max: 5):** Functions or methods that may be hard to
  understand - see [Cognitive Complexity](https://docs.codeclimate.com/docs/cognitive-complexity)
* **Method count (Max: 20):** Classes defined with a high number of functions or
  methods. When a class has a higher method count, it usually indicates an
  encapsulation problem (your class does too much), which leads to
  harder-to-scale code.
* **Method length (Max: 25):** Excessive lines of code within a single function
  or method. Be aware that smaller method line counts will encourage better
  encapsulation practices, and it can always be overriden *downwards* by other
  engines (i.e. Rubocop, where it's common to have a maximum count of 5 per
  method)
* **Nested control flow (Max: 4):** Deeply nested control structures like `if`
  or `case`
* **Return statements (Max: 4):** Functions or methods with a high number of
  return statements
* **Identical blocks of code (Max: per-language):** We avoid duplicated code, as
  it leads to hard-to-debug situations ("I already fixed that! Why it's still
  wrong?").
* **Similar blocks of code (Max: per-language):** Duplicate code which is not
  identical but shares the same structure (e.g. variable names may differ). This
  issue indicates code may be improved through encapsulation.

These issues are checked-for using codeclimate CLI by default. However, we are
not restricting ourselves to these 10 checks, as we actually add more rules by
using external engines, depending on the language and/or development platform.

### Churn rate on project files

The impact of maintainability issues will be greater on files that change
frequently. The rate at which any given file changes over time is called "Churn
rate". Files with a big churn rate and big issue count are candidates for
splitting into smaller files.

## Python-specific considerations

Besides the maintainability checks described before, we'll also run additional
checks on python code:

* pep8:
