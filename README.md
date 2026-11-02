# Bound SQLite CRUD

Small source-only CRUD statement builders inspired by
[SQLBuilder_MTC](https://github.com/ktekinay/xojo-sqlbuilder). `Import sqlbuilderkit`
provides `BoundSQL`, `QuoteSQLIdentifier`, `SelectSQL`, `InsertSQL`, `UpdateSQL`
and `DeleteSQL`. The package has no database/backend dependency; callers execute
the result using the existing `Database.Query(statement.Text, statement.Parameters)`.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add sqlbuilderkit --git https://github.com/BuoyBay/sqlbuilderkit.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## Example

```basic
Import sqlbuilderkit

Sub Main()
    Dim statement As BoundSQL = SelectSQL("people", ["id", "name"], ["name"], [DbValue.OfString("Ada O'Brien")])
    Print statement.Text
    Print "Bound parameters: " + String.From(Array.Count(statement.Parameters))
End Sub
```

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer sqlbuilderkit
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
