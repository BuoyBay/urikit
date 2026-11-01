# URIKit provenance and scope

Source inspected: [RB-URI](https://github.com/charonn0/RB-URI), commit
`1bb4f75a063443709d807985b8cf5ee5c8c3be51`. Inspected `README.md`, `URI.rbbas`
and `license.md`. The MIT copyright notice is retained in `UPSTREAM-LICENSE.txt`.
The implementation here is independent Buoy code following
[RFC3986](https://www.rfc-editor.org/rfc/rfc3986), especially component grammar
(§3) and resolution examples/algorithm (§5). No upstream code or assets are copied.

RB-URI exposes mutable URL component properties, implicit String conversion and
comparison, helpers and query arguments. Its README explicitly excludes URNs.
URIKit instead exposes immutable generic URI references, explicit formatting,
strict ASCII component validation, optional-component presence markers, RFC
relative resolution and byte-first percent codecs. It does not promise the
upstream mutable API, query dictionary or equivalence rules. Generic opaque
scheme parsing does not implement scheme-specific URN semantics.

Installed Buoy `url-connection.md` supplies HTTP(S) transport and effective URL
reporting. String and Bytes supply underlying text/encoding primitives; neither
page exposes this explicit URI-reference component/resolution API. No compiler
or runtime changes were needed. Runtime String NUL limitations are handled by
preserving arbitrary decoded octets in Bytes and rejecting NUL in text decoding.
