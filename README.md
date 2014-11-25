gofigure  [![GoDoc](https://godoc.org/github.com/ian-kent/gofigure?status.svg)](https://godoc.org/github.com/ian-kent/gofigure)
========

Configuration made easy.

- Just define a struct and call Gofigure
- Supports environment variables and command line flags

### Example

`go get github.com/ian-kent/gofigure`

```go
package main

import "github.com/ian-kent/gofigure"

type config struct {
  gofigure interface{} `envPrefix:"MYAPP" order:"cmd,env"`
  RemoteAddr string `env:"REMOTE_ADDR" cmd:"remote-addr"`
  LocalAddr  string `env:"LOCAL_ADDR" cmd:"local-addr"`
}

func main() {
  var cfg config
  err := gofigure.Gofigure(&cfg)
  if err != nil {
    log.Fatal(err)
  }
  // cfg fields should be set
}
```

### gofigure field

The gofigure field is used to configure Gofigure.

The `order` tag is used to set configuration source order, e.g.
environment variables first then command line options second.

Any field matching `camelCase` format will be parsed into `camel`
and `case`, and passed to the source matching `camel`.

For example, the `envPrefix` field is split into `env` and `prefix`,
and the tag value is passed to the environment variable source as
the `prefix` parameter.

### Licence

Copyright ©‎ 2014, Ian Kent (http://www.iankent.eu).

Released under MIT license, see [LICENSE](LICENSE.md) for details.
