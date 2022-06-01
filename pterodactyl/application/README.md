# Application API
This API is for managing a lot of the administrative side of the panel, ranging from control over users, nodes, servers, eggs, and more.

## Access
The `Authorization` header must be present in requests and must be prefixed with "Bearer " followed by the key. Application API keys can be generated in the admin side of the panel. `Content-Type` and `Accept` headers are also required for `POST`, `PATCH`, `PUT` requests.

## Limitations
The default request ratelimit is 240 requests per minute. Response objects will always include the `X-Ratelimit-Limit` and `X-Ratelimit-Remaining` headers, which are both number values corresponding to its use. If you encounter a ratelimit response (status code: 429), the `X-Ratelimit-Reset` and `Retry-After` headers will be sent additionally, with the values being the timestamp to retry requests after and the time in milliseconds to retry after respectively.

## Parameters
These are parameter arguments used in a lot - but not all - endpoints of the application API. Each endpoint will specify the supported parameters, as well as custom ones specific to the endpoint.

Name | Format | Description
-----|--------|------------
filter | `filter[key]=value` | Filters the requested resource by the value of a specified key. This parameter is only used by endpoints that return an array of objects.
include | `include=a,b,c` | A list of objects related to the requested resource to include in the response. Multiple include arguments must be separated by **commas only**, not spaces or other separators.
sort | `sort=key` | Sorts the requested resources according to the specified key. By default the sorted objects are in ascending order, but can be negated by prefixing the key with a dash (e.g. `sort=-id`).
page | `page=1` | The number of the page to retrieve the requested resource from. This works in line with the `per_page` parameter.
per-page | `per_page=50` | The number of objects to return from the requested resource. If the request resource returns more than the specified number, it will overlap onto the next page(s).
