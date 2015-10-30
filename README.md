# gluatemplate

Text template for [gopher-lua](https://github.com/yuin/gopher-lua)

This product is based on [Go Text Template](https://golang.org/pkg/text/template/).
If you are not familiar with the syntax, please read the documentation.

## Installation

```
go get github.com/kohkimakimoto/gluatemplate
```

## API

* `template.dostring(text, table)`
* `template.dofile(file, table)`

## Usage

```go
package main

import (
    "github.com/yuin/gopher-lua"
    "github.com/kohkimakimoto/gluatemplate"
)

func main() {
    L := lua.NewState()
    defer L.Close()

    L.PreloadModule("template", gluatemplate.Loader)
    if err := L.DoString(`
local template = require("template")

local text = template.dostring([[
This is a text template library.
Created by {{.first_name}} {{.last_name}}
]], {
	first_name = "kohki",
	last_name = "makimoto",
})

print(text)
--
-- This is a text template library.
-- Created by kohki makimoto
--
`); err != nil {
        panic(err)
    }
}
```
