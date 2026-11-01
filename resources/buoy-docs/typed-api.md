---
title: "urikit typed API"
summary: "Source-derived public signatures, properties, parameters, defaults, and return values."
category: "Reference"
order: 21
types: ["URIReference"]
dependencies: []
symbols: ["URIReference"]
related: ["api.md", "getting-started.md", "index.md"]
---

# urikit typed API

Generated from the package source declarations. Platform guards are shown where present; inherited members are documented on the base type. See the [API contracts](api.md) for behavior and limitations.

## URIReference

`Public Class URIReference`

Immutable ASCII URI reference, preserving spelling and empty component markers.

### Properties

| Name | Type | Read-Only | Shared | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `Text` | `String` | Yes | No | — | — |
| `Scheme` | `String` | Yes | No | — | — |
| `Authority` | `String` | Yes | No | — | — |
| `Path` | `String` | Yes | No | — | — |
| `Query` | `String` | Yes | No | — | — |
| `Fragment` | `String` | Yes | No | — | — |
| `Host` | `String` | Yes | No | — | — |
| `Port` | `String` | Yes | No | — | — |
| `UserInfo` | `String` | Yes | No | — | — |
| `HasScheme` | `Boolean` | Yes | No | — | — |
| `HasAuthority` | `Boolean` | Yes | No | — | — |
| `HasQuery` | `Boolean` | Yes | No | — | — |
| `HasFragment` | `Boolean` | Yes | No | — | — |
| `HasPort` | `Boolean` | Yes | No | — | — |
| `HasUserInfo` | `Boolean` | Yes | No | — | — |

### Constructor

`Public Sub Constructor(sourceText As String, maxBytes As Integer = 65536)`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `sourceText` | `String` | `ByVal` | Required |
| `maxBytes` | `Integer` | `ByVal` | `65536` |

Returns: no value.

## URIKit functions

### ParseURI

`Public Function ParseURI(sourceText As String, maxBytes As Integer = 65536) As URIReference`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `sourceText` | `String` | `ByVal` | Required |
| `maxBytes` | `Integer` | `ByVal` | `65536` |

#### Returns

| Type |
| --- |
| `URIReference` |

### RemoveURIDotSegments

`Public Function RemoveURIDotSegments(uriPath As String) As String`

RFC3986 section 5.2.4, operating on encoded uriPath segments only.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `uriPath` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `String` |

### ResolveURI

`Public Function ResolveURI(baseText As String, reference As String) As URIReference`

Strict RFC3986 resolution. Base must be absolute; spelling is not normalized.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `baseText` | `String` | `ByVal` | Required |
| `reference` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `URIReference` |

### PercentEncodeBytes

`Public Function PercentEncodeBytes(data As Bytes) As String`

Encode one opaque component: preserve unreserved ASCII, encode all other octets.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `data` | `Bytes` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `String` |

### PercentEncodeUTF8

`Public Function PercentEncodeUTF8(sourceText As String) As String`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `sourceText` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `String` |

### PercentDecodeBytes

`Public Function PercentDecodeBytes(sourceText As String) As Bytes`

Decode escapes exactly once; raw input must be printable ASCII. Plus stays plus.

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `sourceText` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `Bytes` |

### PercentDecodeUTF8

`Public Function PercentDecodeUTF8(sourceText As String) As String`

#### Parameters

| Name | Type | Passing | Default |
| --- | --- | --- | --- |
| `sourceText` | `String` | `ByVal` | Required |

#### Returns

| Type |
| --- |
| `String` |
