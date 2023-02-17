# <a name="wasi_http">World wasi-http</a>


 - Exports:
    - interface `exports`

## <a name="exports">Export interface exports</a>

----

### Types

#### <a name="uri">`type uri`</a>
`string`
<p>The HTTP URI of the current request.

#### <a name="params">`type params`</a>
[`params`](#params)
<p>The HTTP parameter queries, represented as a list of (name, value) pairs.

#### <a name="method">`enum method`</a>

The HTTP method.

##### Enum Cases

- <a name="method.get">`get`</a>
- <a name="method.post">`post`</a>
- <a name="method.put">`put`</a>
- <a name="method.delete">`delete`</a>
- <a name="method.patch">`patch`</a>
- <a name="method.head">`head`</a>
- <a name="method.options">`options`</a>
#### <a name="http_status">`type http-status`</a>
`u16`
<p>The HTTP status code.

#### <a name="http_error">`variant http-error`</a>

HTTP errors returned by the runtime.

##### Variant Cases

- <a name="http_error.invalid_url">`invalid-url`</a>: `string`
- <a name="http_error.timeout_error">`timeout-error`</a>: `string`
- <a name="http_error.protocol_error">`protocol-error`</a>: `string`
- <a name="http_error.status_error">`status-error`</a>: `u16`
- <a name="http_error.unexpected_error">`unexpected-error`</a>: `string`
#### <a name="headers">`type headers`</a>
[`headers`](#headers)
<p>The HTTP headers represented as a list of (name, value) pairs.

#### <a name="body">`type body`</a>
[`body`](#body)
<p>The HTTP body.

#### <a name="response">`record response`</a>

An HTTP response.

##### Record Fields

- <a name="response.status">`status`</a>: [`http-status`](#http_status)
- <a name="response.headers">`headers`</a>: option<[`headers`](#headers)>
- <a name="response.body">`body`</a>: option<[`body`](#body)>
#### <a name="request">`record request`</a>

An HTTP request.

##### Record Fields

- <a name="request.method">`method`</a>: [`method`](#method)
- <a name="request.uri">`uri`</a>: [`uri`](#uri)
- <a name="request.headers">`headers`</a>: [`headers`](#headers)
- <a name="request.params">`params`</a>: [`params`](#params)
- <a name="request.body">`body`</a>: option<[`body`](#body)>
----

### Functions

#### <a name="req">`req: func`</a>


##### Params

- <a name="req.req">`req`</a>: [`request`](#request)

##### Return values

- <a name="req.0"></a> ([`response`](#response), [`http-error`](#http_error))
