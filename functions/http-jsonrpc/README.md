# HTTP JSON-RPC Function

The HTTP JSON-RPC function enables you to call remote procedures using the [JSON-RPC 2.0](https://www.jsonrpc.org/specification) protocol over HTTP.  
This function allows workflows to integrate with external services that expose JSON-RPC APIs.

## Parameters

| Name       | Type     | Required | Description |
|:-----------|:--------:|:--------:|:------------|
| `endpoint` | [`endpoint`](https://github.com/serverlessworkflow/specification/blob/main/dsl-reference.md#endpoint) | `yes`    | The HTTP(S) URL of the JSON-RPC service endpoint. Must be a valid URI. |
| `request`  | `request`                                                                                             | `yes`    | The JSON-RPC request object containing the method name, parameters, and message identifier. |

The `request` object has the following properties:

| Name      | Type              | Required | Description |
|:----------|:-----------------:|:--------:|:------------|
| `jsonrpc` | `string`          | `no`     | The JSON-RPC protocol version. Must be `'2.0'`. Defaults to `'2.0'`. |
| `id`      | `string` or `int` | `yes`    | The unique identifier of the JSON-RPC request to perform. |
| `method`  | `string`          | `yes`    | The name of the remote JSON-RPC method to invoke. |
| `params`  | `array` or `map`  | `no`     | Parameters to pass to the remote method. Can be either an array or an object. |

## Usage

Below is an example of how to use the **HTTP JSON-RPC** custom function in a Serverless Workflow:

```yaml
document:
  dsl: '1.0.0'
  namespace: samples
  name: use-http-jsonrpc-function
  version: '1.0.0'
do:
  - call-jsonrpc:
      call: http-jsonrpc:1.0.0                        #could also be called using the function's url instead: https://github.com/serverlessworkflow/catalog/functions/http-jsonrpc/1.0.0
      with:
        endpoint: https://api.example.com/jsonrpc
        request:
          id: 42
          method: multiply
          params:
            - 6
            - 7
```