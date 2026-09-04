# core.async

GitHub: [clojure/clr.core.async](https://github.com/clojure/clr.core.async)

NuGet: https://www.nuget.org/packages/clojure.core.async

Csproj: `<PackageReference Include="clojure.core.async" Version="1.9.865" />`

deps: `io.github.clojure/clr.core.async {:git/tag "v1.9.865" :git/sha "2dee16c"}`

## Example

```clj
(ns com.example.task
  (:use clojure.pprint clojure.repl)
  (:import [System.Threading.Tasks Task])
  (:require [clojure.core.async :as async]))

(defn as-channel [^System.Threading.Tasks.Task task]
  (let [ch (async/chan)]
     (.ContinueWith task
       (sys-action [System.Threading.Tasks.Task] [x]
         (when (.IsCompletedSuccessfully x)
           (async/put! ch (.Result x)))
         (async/close! ch)))
     ch))

(comment

(let [t (Task/FromResult (type-args Object) :foo)]
  (async/go
    (let [v (async/<! (as-channel t))]
      (println v))))

(import '[clojure.lang Keyword])

(let [t (Task/FromResult (type-args Keyword) :foo)]
  (async/go
    (let [v (async/<! (as-channel t))]
      (println v))))

)
```
