# fasthttp-prometheus

Prometheus metrics exporter for go fasthttp/router 

## Installation

`$ go get github.com/Mnwa/fasthttprouter-prometheus`

## Usage

```go
package main

import (
    "fmt"
    "github.com/fasthttp/router"
    "github.com/valyala/fasthttp"
    "github.com/Mnwa/fasthttprouter-prometheus"
    "log"
)

func Index(ctx *fasthttp.RequestCtx) {
    fmt.Fprint(ctx, "Welcome!\n")
}

func main() {
    r := router.New()
    APIregist(r)

    p := fasthttprouter_prometheus.NewPrometheus("fasthttp")
    fastpHandler := p.WrapHandler(r)

    log.Fatal(fasthttp.ListenAndServe(":8080", fastpHandler))
}

func APIregist(r *fasthttprouter.Router) {
    r.GET("/", Index)
}
```

## Related Project

* [fasthttp](https://github.com/valyala/fasthttp)
* [fasthttp/router](https://github.com/fasthttp/router)

## Inspired by

* [go-gin-prometheus](https://github.com/zsais/go-gin-prometheus)
* [gin-prometheus](https://github.com/DanielHeckrath/gin-prometheus)