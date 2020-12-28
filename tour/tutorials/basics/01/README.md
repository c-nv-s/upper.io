# Connect to a Database

## 1. Get a Database Adapter

To connect to a database you need an adapter. Use `go get` to get one, like
this:

```
go get -u github.com/upper/db/v4/adapter/{$ADAPTER}
```

Where `$ADAPTER` could be any of the following:

* `cockroachdb`: for [CockroachDB](https://www.cockroachlabs.com/product/)
* `mongo`: for [MongoDB](https://www.mongodb.com/)
* `mysql`: for [MySQL](https://www.mysql.com/)
* `postgresql`: for [PostgreSQL](https://www.postgresql.org/)
* `ql`: for [QL](https://pkg.go.dev/modernc.org/ql)
* `sqlite`: for [SQLite](https://www.sqlite.org/index.html)

For instace, if you'd like to use the `cockroachdb` adapter you'd first run:

```
go get -u github.com/upper/db/v4/adapter/cockroachdb
```

to get the adapter, and then you can include it in the source code of your
project:

```go
import (
  "github.com/upper/db/v4/adapter/cockroachdb"
)
```

## 2. Configure a Database Connection

Set the database credentials using the `ConnectionURL` type provided by the
adapter:

```go
import (
  "github.com/upper/v4/adapter/cockroachdb"
)

var settings = cockroachdb.ConnectionURL{
  Database: `booktown`,
  Host:     `cockroachdb.demo.upper.io`,
  User:     `demouser`,
  Password: `demop4ss`,
}
```

Note that the `ConnectionURL` (which satisfies the [db.ConnectionURL][1]
interface) varies from one database engine to another. The connection
properties required by each adapter are explained in detail
[here](https://upper.io/docs/adapters).


## 3. Attempt to Establish a Connection

Use the `Open` function to establish a connection with the database server:

```go
sess, err := cockroachdb.Open(settings)
...
```

## 4. Set the Connection to Close

Set the database connection to close automatically after completing all tasks.
Use `Close` and `defer`:

```
defer sess.Close()
```

[1]: https://pkg.go.dev/github.com/upper/db/v4#ConnectionURL
