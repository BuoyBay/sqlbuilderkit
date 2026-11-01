---
title: "SQLBuilderKit getting started"
summary: "Configure and use SQLBuilderKit with explicit input and ownership rules."
category: "Guides"
order: 10
keywords: ["sql", "sqlite", "crud", "parameters"]
related: ["index.md", "api.md", "typed-api.md"]
---

# SQLBuilderKit getting started

Copy sqlbuilderkit into packages and import it. No backend dependency is required to build statements. This example prints a statement and its parameter count without opening a connection or executing SQL.

```buoy
Import sqlbuilderkit

Sub Main()
    Dim statement As BoundSQL = SelectSQL("people", ["id", "name"], ["name"], [DbValue.OfString("Ada O'Brien")])
    Print statement.Text
    Print "Bound parameters: " + String.From(Array.Count(statement.Parameters))
End Sub
```

## Execute through an existing backend

Pass statement.Text and statement.Parameters together to Database.Query. The backend owns binding and execution. Keep your normal connection, row-set cleanup, and transaction policy. Do not concatenate parameter values into Text.

## Predicates and NULL

SELECT may have no predicates. UPDATE and DELETE require at least one equality predicate. Non-NULL predicates generate a bound equality comparison; NULL predicates generate IS NULL and add no parameter. All predicates combine with AND. INSERT and UPDATE assignments bind NULL through ordinary placeholders.

## Validation

Each column list is limited to 1000 entries. Names must be 1–128 ASCII characters, start with a letter/underscore, and continue with letters/digits/underscores. Empty projections/assignments, duplicates ignoring ASCII case, and mismatched value counts throw InvalidArgumentException.

## Read next

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)
