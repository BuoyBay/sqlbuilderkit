---
title: "SQLBuilderKit API"
summary: "Public types, functions, validation, and ownership rules for SQLBuilderKit."
category: "Reference"
order: 20
keywords: ["sql", "sqlite", "crud", "parameters"]
symbols: ["BoundSQL", "BoundSQL.Text", "BoundSQL.Parameters", "QuoteSQLIdentifier", "SelectSQL", "InsertSQL", "UpdateSQL", "DeleteSQL"]
related: ["index.md", "getting-started.md", "typed-api.md"]
---

# SQLBuilderKit API

| API | Contract |
| --- | --- |
| BoundSQL(text, values) | Copy caller-owned parameters; arbitrary SQL text is not validated by this constructor. |
| BoundSQL.Text | Get-only SQL String. |
| BoundSQL.Parameters | Get-only defensive copy of Array Of DbValue. |
| QuoteSQLIdentifier(name) | Validate one simple identifier and double-quote it. |
| SelectSQL(table, columns, whereColumns, whereValues) | Explicit projection and optional AND equality predicates. |
| InsertSQL(table, columns, values) | One row with positional bound values. |
| UpdateSQL(table, columns, values, whereColumns, whereValues) | Assignments plus required predicates. |
| DeleteSQL(table, whereColumns, whereValues) | Required predicates; no unbounded-delete shortcut. |

## Parameter ordering

UPDATE binds assignment values first, then non-NULL predicate values. INSERT binds every value. SELECT/DELETE bind non-NULL predicates in column order. Returned parameter-array edits do not alter a statement's stored parameters.

## Unsupported shapes

Schema-qualified names, dots, wildcard projections, Unicode identifiers, embedded quotes, and raw expressions reject. No joins, CTEs, OR predicates, arithmetic expressions, sorting, paging, aggregates, or RETURNING clauses are built. Use the existing raw parameterized database API when those shapes are needed.

## Read next

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)


[Full typed API: properties, parameters, defaults, and returns](typed-api.md)
