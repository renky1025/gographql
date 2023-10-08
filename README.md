## Project Setup
Create a directory for project and initialize go modules file:
```shell
go mod init github.com/renky/gographql
go get github.com/99designs/gqlgen

```
after that use ‍‍gqlgen init command to setup a gqlgen project.
```shell
go run github.com/99designs/gqlgen init
```

## download mysql driver

download migrate from https://github.com/golang-migrate/migrate/releases

```shell
go get -u github.com/go-sql-driver/mysql
cd internal/pkg/db/migrations/sql
migrate create -ext sql -dir mysql -seq create_users_table
migrate create -ext sql -dir mysql -seq create_links_table
```

auto create tables from sql files
```shell
 migrate -database "mysql://root:123456@tcp(127.0.0.1:3306)/gographql" -path internel/pkg/db/migrations/sql up
```

## api in files file: graph/schema.graphqls

## interface to be implement in file: graph/schema.resolvers.go

Now run the following command to regenerate files;
```shell
go run github.com/99designs/gqlgen generate
```

## server runnning
```shell
go run server.go
```

post http://localhost:8080/query  with http header Authorization

query body:
``` 
query {
	links{
    title
    address,
    user{
      name
    }
  }
}
```
create/modify body:
```
mutation {
  createLink(input: {title: "real link!", address: "www.graphql.org"}){
    user{
      name
    }
  }
}
```
