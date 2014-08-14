captcha
====

Middleware captcha a middleware that provides captcha service for [Macaron](https://github.com/Unknwon/macaron).

[API Reference](https://gowalker.org/github.com/macaron-contrib/captcha)

### Installation

	go get github.com/macaron-contrib/captcha
	
## Usage

```go
// main.go
import (
	"github.com/Unknwon/macaron"
	"github.com/macaron-contrib/cache"
	"github.com/macaron-contrib/captcha"
)

func main() {
  	m := macaron.Classic()
	m.Use(cache.Cacher())
	m.Use(captcha.Captchaer())
	
	m.Get("/", func(ctx *macaron.Context, cpt *captcha.Captcha) string {
		if cpt.VerifyReq(ctx.Req) {
			return "valid captcha"
		}
		return "invalid captcha"
	})

	m.Run()
}
```

```html
<!-- templates/hello.tmpl -->
{{.Captcha.CreateHtml}}
```

## Options

`captcha.Captchaer` comes with a variety of configuration options:

```go
// ...
m.Use(captcha.Captchaer(captcha.Options{
	URLPrefix:			"/captcha/", 	// URL prefix of getting captcha pictures.
	FieldIdName:		"captcha_id", 	// Hidden input element ID.
	FieldCaptchaName:	"captcha", 		// User input value element name in request form.
	ChallengeNums:		6, 				// Challenge number.
	Expiration:			600, 			// Captcha expiration time in seconds.
	CachePrefix:		"captcha_", 	// Cache key prefix captcha characters.
}))
// ...
```

## License

This project is under Apache v2 License. See the [LICENSE](LICENSE) file for the full license text.