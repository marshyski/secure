# secure

## Example

See the [example](example/example.go).

DefaultConfig returns a Configuration with strict security settings

```
SSLRedirect:           true
IsDevelopment: 		   false
STSSeconds:            315360000
STSIncludeSubdomains:  true
FrameDeny:             true
ContentTypeNosniff:    true
BrowserXssFilter:      true
ContentSecurityPolicy: "default-src 'self'"
```

```go
package main

import (
	"github.com/gin-contrib/secure"
	"gopkg.in/gin-gonic/gin.v1"
)

func main() {
	router := gin.Default()

	router.Use(secure.New(secure.Config{
		AllowedHosts:          []string{"example.com", "ssl.example.com"},
		SSLRedirect:           true,
		SSLHost:               "ssl.example.com",
		STSSeconds:            315360000,
		STSIncludeSubdomains:  true,
		FrameDeny:             true,
		ContentTypeNosniff:    true,
		BrowserXssFilter:      true,
		ContentSecurityPolicy: "default-src 'self'",
	}))

	router.GET("/ping", func(c *gin.Context) {
		c.String(200, "pong")
	})

	// Listen and Server in 0.0.0.0:8080
	router.Run()
}


```