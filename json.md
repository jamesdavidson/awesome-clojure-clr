# JSON

The web’s data interchange format, for better or worse.

GitHub: [clojure/clr.data.json](https://github.com/clojure/clr.data.json)

NuGet: https://www.nuget.org/packages/clojure.data.json

Csproj: `<PackageReference Include="clojure.data.json" Version="2.5.1" />`

deps: `io.github.clojure/clr.data.json {:git/tag "v2.5.1" :git/sha "f84cb88"}`

## Example 

```clj
(require '[clojure.data.json :as json])
(json/read-str "{\"foo\":[1,2,3]}" :key-fn keyword) ;; {:foo [1 2 3]}
```
