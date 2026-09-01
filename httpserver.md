# HTTP Server

Neat little HTTP server. No dependency injection required! Not production ready but super useful for development and testing.

GitHub: [anderseknert/ring-clr](https://github.com/anderseknert/ring-clr)

NuGet: n/a

deps: `io.github.anderseknert/ring-clr {:git/sha "656d74a4d7db6ebb531e7c81e4a2a988469e9dd4"}`

## Example

```clj
(ns com.example.webserver
   (:require [ring-clr.adapter.httplistener :as httplistener])
   (:require [clojure.clr.io :as io]
             [clojure.string :as string]))

(defn handler [request]
  {:status 200
   :headers {"content-type" "text/plain"}
   :body "{\"hello\":\"world\"}"})

(defonce listener
  (let [l (System.Net.HttpListener.)]
    (.Add (.Prefixes l) "http://127.0.0.1:8080/")
    (.Start l)
    l))

(alter-meta! #'httplistener/->ring-request dissoc :private)
(alter-meta! #'httplistener/status! dissoc :private)
(alter-meta! #'httplistener/headers! dissoc :private)
(alter-meta! #'httplistener/body! dissoc :private)

(defonce server
  (future
    (while (.IsListening listener)
      (try
        (let [context (.GetContext listener)]
          (future
            (let [response     (.Response context)
                  request-map  (-> context .Request httplistener/->ring-request)
                  response-map (#'handler request-map)]
              (-> response
                  (httplistener/status!  response-map)
                  (httplistener/headers! response-map)
                  (httplistener/body!    response-map)))))
        (catch System.Net.HttpListenerException e
          (println "HttpListenerException" e))
        (catch Exception e
          (println "Exception" e))))))
```
