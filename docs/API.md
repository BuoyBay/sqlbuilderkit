# SQLBuilderKit 0.1.0

Small, pure Buoy CRUD statement builders inspired by
[SQLBuilder_MTC](https://github.com/ktekinay/xojo-sqlbuilder). `Import sqlbuilderkit`
provides `BoundSQL`, `QuoteSQLIdentifier`, `SelectSQL`, `InsertSQL`, `UpdateSQL`
and `DeleteSQL`. The package has no database/backend dependency; callers execute
the result using Buoy's existing `Database.Query(statement.Text, statement.Parameters)`.

This version targets SQLite SQL and positional `?` binding. Runtime verification
uses the bundled `sqlite3` package. PostgreSQL and other engines have not been
tested; no cross-dialect conversion is supplied.

## API

| Function | Behavior |
| --- | --- |
| `QuoteSQLIdentifier(name)` | Double-quotes one validated simple identifier |
| `SelectSQL(table, columns, whereColumns, whereValues)` | Explicit projection and optional AND equality predicates |
| `InsertSQL(table, columns, values)` | One row, values bound positionally |
| `UpdateSQL(table, columns, values, whereColumns, whereValues)` | Assignments followed by required AND equality predicates |
| `DeleteSQL(table, whereColumns, whereValues)` | Required AND equality predicates |

All columns are arrays of String, all values arrays of `DbValue`. Every builder
returns a `BoundSQL` with get-only `Text` and `Parameters`. Input values and
returned parameter arrays are copied so array edits do not change a statement.
`BoundSQL(text, values)` is also public for applications that already own SQL;
the constructor does not validate arbitrary SQL text.

An empty predicate list is accepted for SELECT. UPDATE and DELETE require at
least one predicate. Predicate values with `DbValue.KindNull` generate `IS NULL`
without consuming a placeholder. Other predicates generate `= ?`; all predicates
are combined with AND. INSERT and UPDATE assignments bind NULL with a placeholder.
UPDATE bindings contain assignment values first, then non-NULL predicate values.

Identifiers must be 1..128 ASCII characters, start with a letter or underscore,
and continue with letters, underscores or digits. The package deliberately
rejects SQL expressions, dots/schema qualification, wildcard projections,
embedded quotes and Unicode identifiers. Reserved words work because names are
quoted. Each list is limited to 1000 columns; empty projections/assignments,
duplicate column names ignoring ASCII case, and mismatched value counts reject
with `InvalidArgumentException`. Duplicate detection is O(n²) within that bound.

Values are never interpolated into SQL. Callers must still decide which tables,
columns and operations their application permits; syntactic validation is not
authorization. SQL execution, transactions and connection ownership stay with
the existing database APIs.

## Example and verification

Bind user-supplied values separately from SQL, including values containing apostrophes.

No joins, CTEs, OR predicates, arithmetic/raw expressions, sorting, paging,
aggregates, returning clauses or upstream fluent interfaces are implemented.
Buoy already supports raw parameterized SQL and `@DatabaseRecord` mapping; this
package is an optional convenience layer rather than a replacement ORM.
