# HTTP Client

Useful little client for development, testing and scripts.

GitHub: [whamtet/clr-http-lite](https://github.com/whamtet/clr-http-lite)

NuGet: n/a

deps: `io.github.whamtet/clr-http-lite {:git/sha "f7a426dd200de727906ea7ca7ff842668c154402"}`

## Example

```clj
(require '[clr-http.lite.client :as client])

(def result
  (client/post
    "https://httpbin.org/post"
    {:basic-auth ["user" "pass"]
     :query-params {"foo" "bar"}
     ;:headers {"Authorization" (format "Bearer %s" token)}
     :body "foo bar baz"}))

(println (:body result))
```
