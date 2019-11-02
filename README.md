# Vaja-Bob

A micro web framework for [Väja](https://github.com/marteinn/Vaja).

## Example

```
import Bob

let app = \
  Bob.new() \
  |> Bob.addMiddlewares([Bob.debugMiddleware, Bob.rendererMiddleware]) \
  |> Bob.addRoute404(fn(req, _) -> {"status": 404, "body": "Page not found"}) \
  |> Bob.addRoutes([
    [
      Bob.newPath("/artist/([a-z]*)/"),
      fn(req, args) -> Bob.newJSONResponse({"status": 200, "context": {
        "artist": args[0]
      }})
    ]
  ])

Http.createServer() \
|> Http.addHandler(
  app |> Bob.makeHandler()
) \
|> Http.listen(8080)
```


## License
This project is released under the [MIT License](http://www.opensource.org/licenses/MIT).
