# Source study and differences

- Source: [ktekinay/xojo-sqlbuilder](https://github.com/ktekinay/xojo-sqlbuilder).
- Resolved HEAD inspected: `e8b137f2ae2b5f6d7f8d0566b09ef731e4d59efa`.
- Downloaded master archive SHA-256:
  `e462511f1484371af21a409eb1687a743247e7d19e829226e285e50fefe17084`.
- Inspected `README.md`, `LICENSE.md`, `SQLBuilder_MTC/Statement.xojo_code`,
  `SelectClause.xojo_code`, `WhereClause.xojo_code` and repository layout.
- Upstream license: MIT, copyright 2015 Kem Tekinay, MacTechnologies Consulting;
  the exact notice is retained in `UPSTREAM-LICENSE.txt`.

The implementation is fresh Buoy code. No Xojo source was mechanically converted.
The upstream library is a broader fluent SQL builder with SELECT/FROM/WHERE,
joins, CTEs, HAVING, grouping, LIMIT and compound statements, plus database-specific
prepared-statement adapters. It tracks parameters and adapts placeholders to the
selected engine. Its documented NULL comparison handling inspired the explicit
NULL predicate behavior here.

SQLBuilderKit keeps a narrower fixed set of CRUD shapes and validates every
identifier. It supplies `DbValue` arrays to Buoy's existing binding interface;
it does not port the original Variant-based prepared-statement layer. Its `?`
syntax and double-quoted identifier behavior have been executed against SQLite
only. Preserving the original cross-database dialect selection, general SQL
expressions and fluent API remains future work, not established compatibility.

The installed `database.md` and `database-record.md` references were used to
confirm `Database.Query(sql, Array Of DbValue)`, the `DbValue` types and existing
typed mapping. The example uses `Import sqlite3`, as existing Buoy samples do.
The Linux host's compiler does not discover its bundled SQLite archive from an
isolated temporary project automatically. The runner copies the installed archive
into that project's `packages` directory before checking/building.
