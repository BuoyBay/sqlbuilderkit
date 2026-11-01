---
title: "sqlbuilderkit typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["BoundSQL"]
dependencies: []
symbols: ["BoundSQL"]
related: ["api.md", "getting-started.md", "index.md"]
---

# sqlbuilderkit typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## BoundSQL

`Public Class BoundSQL`

A SQL string and its separately bound values. Arrays are defensive copies.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Text` | `String` | Yes | No | — | — |
| `Parameters` | `Array Of DbValue` | Yes | No | — | — |

### Constructor

`Public Sub Constructor(text As String, values As Array Of DbValue)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `text` | `String` | `ByVal` | Required |
| `values` | `Array Of DbValue` | `ByVal` | Required |

Returns: no value.

## SQLBuilderKit functions

### QuoteSQLIdentifier

`Public Function QuoteSQLIdentifier(name As String) As String`

Quote a simple ASCII identifier; expressions and qualified names reject.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `name` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `String` |

### SelectSQL

`Public Function SelectSQL(table As String, columns As Array Of String, whereColumns As Array Of String, whereValues As Array Of DbValue) As BoundSQL`

SELECT an explicit column list with optional AND equality predicates.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `table` | `String` | `ByVal` | Required |
| `columns` | `Array Of String` | `ByVal` | Required |
| `whereColumns` | `Array Of String` | `ByVal` | Required |
| `whereValues` | `Array Of DbValue` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `BoundSQL` |

### InsertSQL

`Public Function InsertSQL(table As String, columns As Array Of String, values As Array Of DbValue) As BoundSQL`

INSERT one row; all values, including NULL, use bound placeholders.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `table` | `String` | `ByVal` | Required |
| `columns` | `Array Of String` | `ByVal` | Required |
| `values` | `Array Of DbValue` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `BoundSQL` |

### UpdateSQL

`Public Function UpdateSQL(table As String, columns As Array Of String, values As Array Of DbValue, whereColumns As Array Of String, whereValues As Array Of DbValue) As BoundSQL`

UPDATE one or more rows; at least one equality predicate is required.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `table` | `String` | `ByVal` | Required |
| `columns` | `Array Of String` | `ByVal` | Required |
| `values` | `Array Of DbValue` | `ByVal` | Required |
| `whereColumns` | `Array Of String` | `ByVal` | Required |
| `whereValues` | `Array Of DbValue` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `BoundSQL` |

### DeleteSQL

`Public Function DeleteSQL(table As String, whereColumns As Array Of String, whereValues As Array Of DbValue) As BoundSQL`

DELETE with at least one equality predicate; no unbounded-delete shortcut.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `table` | `String` | `ByVal` | Required |
| `whereColumns` | `Array Of String` | `ByVal` | Required |
| `whereValues` | `Array Of DbValue` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `BoundSQL` |
