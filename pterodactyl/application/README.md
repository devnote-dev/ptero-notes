# Application API
This API is for managing a lot of the administrative side of the panel, ranging from control over users, nodes, servers, eggs, and more.

## Access
The `Authorization` header must be present in requests and must be prefixed with "Bearer " followed by the key. Application API keys can be generated in the admin side of the panel. `Content-Type` and `Accept` headers are also required for `POST`, `PATCH`, `PUT` requests. Requests that require a body should be in the format of a **JSON string**, not a literal object. Sending a literal object in the body will cause unexpected errors.

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

## Statuses
All possible status codes that can be received from the application API. Note that this only includes status code 500 from the 5xx group, the rest of the status codes are not directly related to the API.

Code | Description
-----|------------
200  | The request was successful.
201  | The resource was created, usually for POST requests.
202  | The request was accepted but has not been completed yet (does not include a response body).
204  | The request was successful with no response body.
400  | The request failed, this could be due to invalid request headers, an invalid request body or something else.
401  | The API key you are using to access the endpoint is invalid.
403  | The API key you are using does not have the necessary permissions to access the endpoint.
404  | The requested endpoint was not found.
405  | The request method you are using for the endpoint is not allowed.
409  | The request conflicts with another resource or requirement (check the response body).
422  | One or more fields in the request body were not present or failed to meet the requirements.
429  | You have exceeded the allowed limits for requests per minute.
500  | The API failed to process the request. This is usually sent if the request body is in an invalid format.
