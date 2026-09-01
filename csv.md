# CSV

The widely used Comma Separated Values. A format loved and loathed.

GitHub: https://github.com/dmiller/data.csv

NuGet: n/a

deps: `io.github.dmiller/data.csv {:git/sha "faa419961f3a74aa113c7c7ef7ec6f1bc6d9458e"}`

## Example

```clj
(require '[clojure.data.csv :as csv])
(require '[clojure.clr.io :as io])
(use 'clojure.pprint)

(with-open [rdr (io/text-reader "input.csv")]
  (doseq [x (csv/read-csv rdr)]
    (pprint x)))
```
