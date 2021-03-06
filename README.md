# depstar

<img src="./depstar_logo.png" />

a clj-based uberjarrer (forked from [healthfinch/depstar](https://github.com/healthfinch/depstar) and enhanced)

# Usage

Install this tool to an alias in `$PROJECT/deps.edn` or `$HOME/.clojure/deps.edn`:

```clj
{
  :aliases {:depstar
              {:extra-deps
                 {seancorfield/depstar {:mvn/version "0.1.6"}}}}
}
```

Create an uberjar by invoking `depstar` with the desired jar name:

```bash
clojure -A:depstar -m hf.depstar.uberjar MyProject.jar
```

Create a (library) jar by invoking `depstar` with the desired jar name:

```bash
clojure -A:depstar -m hf.depstar.jar MyLib.jar
```

`depstar` uses the classpath computed by `clojure`.
For example, add web assets into an uberjar by including an alias in your `deps.edn`:

```clj
{:paths ["src"]
 :aliases {:webassets {:extra-paths ["public-html"]}}}
```

Then invoke `depstar` with the chosen aliases:

```bash
clojure -A:depstar:webassets -m hf.depstar.uberjar MyProject.jar
```

Note that `depstar` does no AOT compilation and does not add a manifest to the jar file. You can run the uberjar as follows
(assuming `project.core` is your main namespace):

```bash
java -cp MyProject.jar clojure.main -m project.core
```

# Changes

* 0.1.6 -- Mar 10, 2019 -- Fix for JARs containing `data_readers.clj` (do not close input stream!); supports `-Ddepstar.debug=true` and `DEPSTAR_DEBUG=true` to be more verbose.
* 0.1.5 -- Oct 24, 2018 -- Fix for timestamp preservation.
* 0.1.2 -- Oct 23, 2018 -- Initial fork with (incorrect) fix for exception from JARs containing `data_readers.clj`; `hf.depstar.jar` namespace added.

# License

The use and distribution terms for this software are covered by the
[Eclipse Public License 2.0](https://www.eclipse.org/org/documents/epl-2.0/EPL-2.0.html)
