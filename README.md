# URI-reference parse and RFC3986 resolution

Source-only ASCII URI-reference parsing, strict RFC3986 relative resolution and
explicit byte/UTF-8 percent codecs. `Import urikit`. No native or network dependencies.
This fills component/resolution semantics above the existing URLConnection HTTP
transport; it does not make requests or implement browser URL behavior.

## Install

From a Buoy consumer project with BPM installed:

```sh
bpm add urikit --git https://github.com/BuoyBay/urikit.git --rev refs/heads/main
```

BPM records the resolved commit in its lockfile. Keep that lockfile with the
consumer project for reproducible installs.

## API at a glance

- `ParseURI(sourceText, maxBytes = 65536)` or `New URIReference(sourceText, maxBytes)`
  returns an immutable reference. `Text` preserves the exact original spelling.
  String properties: `Scheme`, `Authority`, `UserInfo`, `Host`, `Port`, `Path`,
  `Query`, `Fragment`. Boolean markers: `HasScheme`, `HasAuthority`, `HasUserInfo`,
  `HasPort`, `HasQuery`, `HasFragment`. An absent component and a present empty
  component are distinct. `Port` is decimal text, including possible empty text;
  no service range policy is imposed. `Host` retains brackets for IP literals.
- `ResolveURI(baseText, reference)` returns a `URIReference` using RFC3986 §5.2.
  The base must have a scheme. Query/fragment delimiters are preserved even for
  empty values. Encoded slashes/dots remain encoded during resolution.
- `RemoveURIDotSegments(uriPath)` exposes the RFC3986 encoded-path algorithm.
- `PercentEncodeBytes(data)` encodes opaque bytes; `PercentEncodeUTF8(sourceText)`
  encodes a String's UTF-8 bytes. Only unreserved ASCII remains literal. All other
  bytes are encoded with uppercase hex, including delimiters and spaces.

## Build from source

With the native `build-packages` driver from [devtools](https://github.com/BuoyBay/devtools)
on your `PATH`, run from this checkout:

```sh
build-packages --root "$PWD" --compile-consumer urikit
```

The driver checks source targets and compiles an import consumer. See the
[API guide](docs/API.md) for behavior, limits and any host prerequisites.

## Local Buoy setup

On your own machine, install Buoy and run:

```sh
buoy ai init --both
```

## Contributing

[Contributing](CONTRIBUTING.md) · [License](LICENSE)
