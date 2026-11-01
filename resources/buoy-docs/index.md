---
title: "SQLBuilderKit"
summary: "Build narrow CRUD statements with validated identifiers and separately bound DbValue parameters."
category: "Overview"
order: 0
keywords: ["sql", "sqlite", "crud", "parameters"]
related: ["getting-started.md", "api.md", "typed-api.md"]
---

# SQLBuilderKit

SQLBuilderKit builds a small set of CRUD statement shapes in pure Buoy. It returns a BoundSQL object containing SQL text and separate DbValue parameters; it does not open a database, execute statements, or own transactions.

## Dialect and scope

This version targets SQLite-style quoted identifiers and positional question-mark binding. Runtime behavior has been checked with SQLite; cross-dialect conversion has not been established. The library is an optional convenience over existing parameterized Database operations, not a replacement ORM.

Identifiers are deliberately narrow ASCII names rather than SQL expressions. Values are never interpolated into SQL. Applications still decide which tables, columns, and operations a user may access: syntactic validation is not authorization.

## Provenance

This is newly written Buoy code informed by SQLBuilder_MTC, with a smaller fixed CRUD surface. It does not port the upstream fluent interface, prepared-statement adapters, or general cross-database dialect selection.

## Read next

- [Overview](index.md)
- [Getting started](getting-started.md)
- [API reference](api.md)
