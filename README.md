# httpc
<a href="https://github.com/gleam-lang/httpc/releases"><img src="https://img.shields.io/github/release/gleam-lang/httpc" alt="GitHub release"></a>
<a href="https://discord.gg/Fm8Pwmy"><img src="https://img.shields.io/discord/768594524158427167?color=blue" alt="Discord chat"></a>
![CI](https://github.com/gleam-lang/httpc/workflows/test/badge.svg?branch=main)

Bindings to Erlang's built in HTTP client, `httpc`.

```rust
import gleam/httpc
import gleam/http.{Get}
import gleam/should

pub fn main() {
  // Prepare a HTTP request record
  let req = http.default_req()
    |> http.set_method(Get)
    |> http.set_host("test-api.service.hmrc.gov.uk")
    |> http.set_path("/hello/world")
    |> http.prepend_req_header("accept", "application/vnd.hmrc.1.0+json")

  // Send the HTTP request to the server
  try resp = httpc.send(req)

  // We get a response record back
  resp.status
  |> should.equal(200)

  resp
  |> http.get_resp_header("content-type")
  |> should.equal(Ok("application/json"))

  resp.body
  |> should.equal("{\"message\":\"Hello World\"}")

  Ok(resp)
}
```

## Installation

This package can be installed by adding `gleam_httpc` to your `rebar.config`
dependencies:

```erlang
{deps, [
    gleam_httpc
]}.
```

You may also need to add the `gleam_httpc` OTP application to your `.app.src`
file, depending on how you run your program.

```erlang
{applications, [
    kernel,
    stdlib,
    ssl,
    inets,
    gleam_stdlib,
    gleam_httpc
]},
```
