# `wasi-http`

A proposed [WebAssembly System Interface](https://github.com/WebAssembly/WASI)
API to add native http client support.

### Current Phase

Phase 1

### Champions

- [Brendan Burns](https://github.com/brendandburns)

### Phase 4 Advancement Criteria

_TODO before entering Phase 2._

## Table of Contents

- [Introduction](#introduction)
- [Goals](#goals)
- [Non-goals](#non-goals)
- [API walk-through](#api-walk-through)
  - [Use case: support various languages](#use-case-support-various-languages)
- [Detailed design discussion](#detailed-design-discussion)
- [Considered alternatives](#considered-alternatives)
  - [Alternative: sockets](#alternative-sockets)
- [Stakeholder Interest & Feedback](#stakeholder-interest--feedback)
- [References & acknowledgements](#references--acknowledgements)

### Introduction
This proposal looks to provide a standard API for http clients. This proposal
intends to add an HTTP API in addition to a Socket API so that there can
be a sandbox boundary around the L7 application layer protocol which
allows more rich controls than an L4 based sandbox.

### Goals
- __Http Client support__: the goal of this proposal is to add the missing
  functions that are required to make core HTTP requests from WebAssembly
  programs.

- __browser polyfills__: for browsers, we aim to provide a way to polyfill this
  API using Web Workers providing similar functionality to what exists in
  browsers today.



### Non-goals
- __Streaming HTTP__: this API will not be compatible (for now) with WebSockets
  or http/2 streaming.

- __HTTP Serving__: this API is currently only concerned with HTTP client
  requests, not building an HTTP server.



### API walk-through

The API consists of a single function. In pseudo-code:

```C
void req(request_t *req, response_error_tuple_t *ret);
```

This will execute a single web request and return either an error or a response from the server.

#### Use case: support various languages

Using this API, it should be possible to implement idiomatic http clients in languages like:
- __C__, (e.g. libcurl)
- __Dotnet__, (e.g. HttpClient class)
- __Golang__, (e.g. Http)


### Detailed design discussion

### Considered alternatives

#### Alternative: Sockets

There is a proposal to add Berkely Socket support to WASI. We believe that this effort is complimentary.
While it is feasible to implement standard HTTP clients in terms of sockets, there is not much value
in doing this in WASI/WebAssembly. There are many existing, sophisticated HTTP clients, and implementing
yet another client doesn't add much to the ecosystem. Additionally, there is nothing in this proposal
the precludes someone choosing to implement an HTTP client in WebAssembly over sockets. This proposal
enables us to support a common use case easily and securely using a host implementation that uses
existing, production-grade HTTP clients.

### Stakeholder Interest & Feedback

TODO before entering Phase 3.

<!-- [This should include a list of implementers who have expressed interest in
implementing the proposal] -->


### References & acknowledgements

There have been various previous efforts in this space:
* https://github.com/deislabs/wasi-experimental-http
* https://github.com/deislabs/spiderlightning