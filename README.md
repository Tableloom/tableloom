# Tableloom

[![Tests](https://github.com/Tableloom/tableloom/actions/workflows/tests.yml/badge.svg)](https://github.com/Tableloom/tableloom/actions/workflows/tests.yml)

**Render tabular data into beautiful, portable HTML.**

Tableloom is a Python library for turning tabular data into presentation-ready HTML, with a particular focus on producing tables that work well in email as well as modern web browsers.

It started as a fork of [`pretty_html_table`](https://github.com/sbi-rviot/ph_table), an MIT-licensed library for generating styled HTML tables from pandas DataFrames. Tableloom is intended to grow beyond that original use case while retaining the simplicity that made the original library useful.

> **Early development:** Tableloom is currently in the 0.0.x series. The API and architecture are expected to evolve.

## Why Tableloom?

HTML tables are deceptively complicated.

A table that looks great in a browser isn't necessarily suitable for an email. A table designed for email often doesn't make sense as a modern web component. And while libraries such as pandas provide powerful HTML styling capabilities, they don't necessarily solve the problem of choosing an appropriate representation for the destination.

Tableloom aims to make that distinction explicit:

```python
from tableloom import build_table

html = build_table(df)
```

The goal is eventually to make the destination a first-class choice:

```python
render(data, target="email")
render(data, target="browser")
```

The same underlying data and presentation intent, rendered appropriately for where it is going.

## Current status

Tableloom is at an early stage.

The initial release focuses on establishing a maintained, modern foundation based on the original `pretty_html_table` implementation.

### Current

* HTML table generation
* Pandas DataFrame support
* Email-friendly styling
* Multiple built-in styles
* Customisable table formatting
* Modern Python packaging
* Automated testing and CI

### Planned

* A unified `render()` API
* Browser-oriented HTML output
* Additional data sources beyond pandas
* Support for sequences, records and arrays
* Separate rendering targets for email and browser
* Improved accessibility
* More flexible themes and styling
* Optional interactive browser output

The roadmap will evolve based on real-world use rather than trying to build every possible table feature up front.

## Installation

```bash
pip install tableloom
```

## Quick start

```python
import pandas as pd
from tableloom import build_table

df = pd.DataFrame(
    {
        "Product": ["Widget A", "Widget B", "Widget C"],
        "Sales": [125, 98, 147],
    }
)

html = build_table(df)
```

The returned HTML can be inserted into an email or included in an HTML document.

For example:

```python
message = f"""
<html>
<body>
<h2>Sales Report</h2>

{html}

</body>
</html>
"""
```

## Email-friendly HTML

One of Tableloom's primary goals is making attractive tables that can be embedded directly into email messages.

Email clients impose significantly more restrictive HTML and CSS constraints than modern browsers. Tableloom therefore treats email rendering as a distinct target rather than assuming that browser-oriented HTML will work everywhere.

## Browser rendering

Browser output is planned as a first-class rendering target.

The intention is not simply to expose the same email HTML in a browser, but to allow Tableloom to produce output appropriate to the capabilities of a modern browser while keeping the simple API that makes the library useful for scripts and automated reports.

## Data sources

Pandas DataFrames are currently the primary supported input.

The longer-term goal is for Tableloom to work with a broader range of tabular data without requiring the user to convert everything into pandas first.

Potential inputs include:

* pandas DataFrames
* sequences of records
* dictionaries
* NumPy arrays
* other dataframe implementations
* Arrow-compatible data

Additional input types will be added where they provide a useful and coherent interface.

## Design goals

Tableloom aims to be:

**Simple**

The common case should require very little code.

**Portable**

Generated output should work in the environment it was designed for.

**Data-source agnostic**

The rendering system should not be unnecessarily coupled to a particular dataframe library.

**Destination-aware**

Email and browser HTML have different requirements. Tableloom should embrace that rather than hiding it.

**Lightweight**

The basic rendering path should not require a web framework or browser runtime.

**Accessible**

Accessibility should be considered part of table rendering rather than something added later.

## Project origins

Tableloom began as a fork of [`pretty_html_table`](https://github.com/sbi-rviot/ph_table) by Renaud Viot.

The original project provided a useful and focused implementation for generating styled HTML tables from pandas DataFrames, particularly for use in email.

Tableloom is an independent project built from that starting point, with the intention of expanding the scope to broader data sources and multiple rendering targets.

The original project and inherited code are distributed under the MIT License.

## Contributing

Tableloom is currently in early development and the API is expected to change.

Issues, bug reports, ideas and pull requests are welcome.

If you're interested in contributing, please open an issue before undertaking a substantial change so that the direction can be discussed first.

## License

Tableloom is released under the MIT License.

See [`LICENSE`](LICENSE) for the full license text.

## Acknowledgements

Tableloom would not exist without the work that went into `pretty_html_table`.

Thank you to Renaud Viot for creating and maintaining the original project.
