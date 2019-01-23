# goroyale
[![GoDoc](https://godoc.org/github.com/jegfish/goroyale?status.svg)](https://godoc.org/github.com/jegfish/goroyale)
[![Go report](https://goreportcard.com/badge/github.com/jegfish/goroyale)](https://goreportcard.com/report/github.com/jegfish/goroyale)

A Golang wrapper for the Clash Royale API at https://royaleapi.com/.

## Installing
If you have Go installed you can run this command.
```sh
go get github.com/jegfish/goroyale
```
## Obtaining token
A token can be obtained using one of two methods
1. Visit https://developer.clashroyale.com, create an account and generate a token
2. Visit https://discord.me/royaleapi then go to the #developer-key channel and request a generated token.

## Example
```golang
package main

import (
	"fmt"

	"github.com/jegfish/goroyale"
)

var token = ""

func main() {
	c, err := goroyale.New(token, 0) // 0 will use the default request timeout of 10 seconds
	if err != nil {
		fmt.Println(err)
		return
	}

	ver, err := c.APIVersion()
	if err != nil {
		fmt.Println(err)
	} else {
		fmt.Println("API Version:", ver)
	}

	params := map[string][]string{
		"exclude": {"name"},
	}
	p, err := c.Player("8L9L9GL", params)
	if err != nil {
		fmt.Println(err)
	} else {
		// will just print "Name:" as p.Name is "" because it was excluded
		// more info about this at https://docs.royaleapi.com/#/field_filter
		fmt.Println("Name:", p.Name)

		fmt.Println("Tag:", p.Tag)
		fmt.Println("Clan:", p.Clan.Name)
	}
}
```
