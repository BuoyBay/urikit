# URIKit 0.1.0

Pure Buoy ASCII URI-reference parsing, strict RFC3986 relative resolution and
explicit byte/UTF-8 percent codecs. `Import urikit`. No native or network dependencies.
This fills component/resolution semantics above the existing URLConnection HTTP
transport; it does not make requests or implement browser URL behavior.

## API

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
- `PercentDecodeBytes(sourceText)` decodes exactly once into arbitrary bytes,
  including NUL. `PercentDecodeUTF8(sourceText)` additionally validates UTF-8 and
  rejects NUL because the current Buoy String runtime does not preserve that text
  contract. `+` remains `+`; these are not HTML form codecs. Raw decoder input must
  be printable non-space ASCII; escaped whitespace is permitted.

Parse bounds are configurable in `1..1048576` bytes. Resolution uses the default
65536-byte parse/path limit; percent encoding consumes at most 65536 bytes and
can produce three times that length. Decoding consumes at most 196608 ASCII
characters and produces at most 65536 bytes. Invalid syntax/limits throw
`InvalidArgumentException`; invalid decoded UTF-8 throws `EncodingException`.

## Syntax and compatibility boundaries

URI references use the RFC3986 ASCII grammar, not IRIs: encode Unicode components
explicitly. The parser validates escapes, scheme, component character sets,
userinfo, decimal port syntax, IPv6 literals (including IPv4 tails) and IPvFuture.
Registered names are preserved; no DNS/IDNA normalization or IPv4 address policy
is inferred from a registered-name spelling. IPv6 zone identifiers are unsupported.
Generic opaque scheme paths, such as `urn:example:animal`, parse syntactically;
there is no scheme-specific URN interpretation.

No case folding, default-port removal, percent normalization, query parameter
splitting, origin comparison or browser security equivalence is performed. The
public reference object is immutable; alter components by creating a new URI text.
Inputs with backslashes, raw spaces, control bytes or raw non-ASCII are rejected.
Encoded `%00` is valid URI syntax but needs the byte decoder for lossless access.

Dot-segment removal follows the specification's string-buffer procedure and may
be quadratic for long paths; limits bound it, but this is not a streaming parser.
Do not use this package alone for request allowlists, filesystem path containment
or service-specific URL validation.

## Verification


Maintainers run the private validation suite before release. See the repository README for public build instructions.

