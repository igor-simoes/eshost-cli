## eshost-cli

eshost-cli makes it easy to run and compare ECMAScript code uniformly across a number of runtimes. Support for runtimes is provided by the library [eshost](https://github.com/bterlson/eshost). Every host is initialized with the [eshost runtime API](https://github.com/bterlson/eshost#runtime-library) available which provides a uniform way to print, create realms, and eval code. 

See eshost's [supported hosts](https://github.com/bterlson/eshost#supported-hosts) for a list of hosts, download/build locations, and other information.

### Usage

See `--help` output for the full details. Basic usage:

* Add hosts using `eshost --add <host name> <host type> <host path> --args <optional arguments>`.
* Automatically configure [`jsvu`](https://github.com/GoogleChromeLabs/jsvu)-installed hosts using `eshost --configure-jsvu`.
* Eval an expression using `eshost -e [1,2,3].length`.
* Execute a script using `eshost path/to/script.js`.

#### Examples

```
$ npm install -g eshost-cli
$ eshost --help
$ eshost --add <name> <type> <path to host executable> --args <optional arguments>
$ eshost -e "Map.length"

## chakra-es6
0

## d8
0

## chakra
0

## spidermonkey
1

## node
0

$ eshost --configure-jsvu --jsvu-prefix jsvu
$ eshost --tags jsvu-web -itsx "let a = 40+2; print(a)"

## Source
let a = 40+2; print(a)

┌──────────┬────┐
│ jsvu-ch  │ 42 │
│ jsvu-jsc │    │
│ jsvu-sm  │    │
│ jsvu-v8  │    │
└──────────┴────┘
```

### Managing Hosts

You can `--list`, `--add`, `--edit`, and `--delete` hosts. Adding a host requires a name, type, and path to the runtime executable. You can optionally pass arguments using `--args`. The same host can be added multiple times with different `--args` which makes it easy to compare the output of runtimes given different options (e.g. by turning language features on and off).

Console hosts are either provided by the browser vendors or, more likely, built from source. [The `jsvu` CLI](https://github.com/GoogleChromeLabs/jsvu) makes it easy to install and update the most common JavaScript engine binaries.

Host types are [those provided by eshost](https://github.com/bterlson/eshost#supported-hosts), namely:

* `node`
* `ch`
* `d8`
* `jsshell`
* `jsc`
* `xs`
* `nashorn`
* `edge`
* `chrome`
* `firefox`
* `safari`
