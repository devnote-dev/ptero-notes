# Contributing

This guide covers the specifications for structuring and documenting endpoints and resources for APIs and API libraries.

### Contents

- [Document Hierarchy](#document-hierarchy)
- [Document Structure](#document-structure)
- - [Endpoints](#endpoints)
- - [Semantic Structure](#semantic-structure)
- - [Example Structure](#example-structure)
- [Components](#components)
- - [Parameter Table](#parameter-table)
- - [Status Code Table](#status-code-table)
- - [Important Blockquote](#important-blockquote)
- - [Note Blockquote](#note-blockquote)
- - [Warning Blockquote](#warning-blockquote)

## Document Hierarchy

Endpoint scoping starts at the software level: if it is an API-related library, the documents belong under `libraries/`. Pterodactyl **panel-specific** endpoints belong under `pterodactyl/`, and Pterodactyl **Wings-specific** endpoints under the `wings/` directory/ Endpoint directories should be scoped under the endpoint path namespaces. For example, endpoints prefixed with `/api/application/users` should be placed in the `pterodactyl/application/users.md` file.

## Document Structure

Supplementary information scoping the endpoints in the document may be specified at the start of the document with the necessary directives to indicate what they apply to. This is useful for endpoints that have specific terminology, grouped functionality or reference other documents/endpoints. Endpoint-specific supplementary information deviating this must be explicitly stated in the endpoint.

A "Contents" heading specifying list of available endpoints ordered by position in the document must follow supplementary information, or be placed at the top of the document if no such information is included. These must be hyperlinks to the document endpoints referenced by the endpoint title, **not** the endpoint path.

### Endpoints

Endpoints must start off with a short title for the endpoint in a level 2 heading and the HTTP method with the full endpoint path in a level 3 heading, wrapped in backticks. Path parameters must be prefixed with a colon followed by an identifier for the parameter. Below the heading a description of the endpoint should be provided, keeping to a short and concise paragraph where possible. Endpoints with extensive functionality must be documented accordingly and formatted in appropriate paragraphs. Backticks must be used when referencing object/resource fields or identifiers. Information that is not necessarily required for the endpoint but is relevant and useful to it may be included as a [Note Blockquote](#note-blockquote). Information that is critical about the endpoint or its usage must be highlighted in bold text or included as a [Warning Blockquote](#warning-blockquote).

If the endpoint accepts a request body, its body structure must be documented accordingly. Endpoints that accept a JSON body must be formatted using a [Parameter Table](#parameter-table) including any composite object types which should have their own parameter tables defined below the request body parameter table. For non-JSON request bodies, a paragraph detailing the request body format may be used.

If the endpoint can return multiple unique responses, a [Status Code Table](#status-code-table) must be used summarising the cause of the response. Note that this does apply for broad covering statuses like 401 (unauthorized) and 403 (forbidden) unless there is a special case for that endpoint. If the endpoint response also contains a body, an example of the response body must also be included following the status code table under an "Example Response" heading.

Sources that the endpoint information is derived from must be included as an ordered list of hyperlinks below the "Sources" heading, using the file name and line hash as the hyperlink name. Source URLs must be **permanent links** to prevent continuous resource changes unless sucha change is warranted by the upstream source (which would be the panel and Wings repositories).

### Semantic Structure

Fields in `<>` are required and fields in `[]` are optional.

```
## <endpoint-title>

### <http-method> <endpoint-path>

<endpoint-description>

[
  ### Parameters

  <request-url parameters-table>
]

[
  ### Body

  <request-body parameter-table>

  [request body composite objects parameter-tables]
]

### Responses

<status-code-table>

[
  ### Example Response

  <example-response-body>
]

### Sources

<sources unordered-list>
```

### Example Structure

````markdown
## Update User

### `PATCH /api/application/users/:id`

Updates a user by its `id`. Note that this is the numeric ID, not the string identifier or external identifier.

### Body

| Field       | Visibility | Type    | Description                                                               |
| ----------- | ---------- | ------- | ------------------------------------------------------------------------- |
| email       | required   | string  | The email of the user.                                                    |
| external_id | optional   | string  | An external identifier to the user.                                       |
| first_name  | required   | string  | The first name of the user.                                               |
| language    | optional   | string  | A language ISO code (defaults to "en").                                   |
| last_name   | required   | string  | The last name of the user.                                                |
| password    | optional   | string  | A password for the user.                                                  |
| root_admin  | optional   | boolean | Whether the user will have administrative privileges (defaults to false). |
| username    | required   | string  | A username for the user.                                                  |

### Responses

| Code | Description                            |
| ---- | -------------------------------------- |
| 200  | The user was updated.                  |
| 400  | The request body could not be decoded. |
| 422  | One or more validation rules failed.   |

### Example Response

```json
{
  "object": "user",
  "attributes": {
    "2fa": true,
    "created_at": "2023-08-16T00:08:04+00:00",
    "email": "sudowoodo@example.com",
    "external_id": null,
    "first_name": "sudo",
    "id": 5,
    "language": "en",
    "last_name": "woodo",
    "root_admin": true,
    "updated_at": "2023-06-14T00:14:11+00:00",
    "username": "sudowoodo",
    "uuid": "31ba4cba-cbfb-472a-a688-701e2d91444f"
  }
}
```

### Sources

- [UpdateUserRequest.php#L7](https://github.com/pterodactyl/panel/blob/9b35a55eea1ddff8a4f4c0232096bf761c74322f/app/Http/Requests/Api/Application/Users/UpdateUserRequest.php#L7)
- [UserController.php#L99](https://github.com/pterodactyl/panel/blob/9b35a55eea1ddff8a4f4c0232096bf761c74322f/app/Http/Controllers/Api/Application/Users/UserController.php#L99)
````

## Components

This section contains descriptions for common document components that are used throughout the documentation.

### Parameter Table

Parameter tables are a uniformed way of describing resource objects for request query parameters and request bodies. They intentionally do not include default field information as part of the structure which should be placed in the description or referenced in detail at the request query paramater or body description.

| Field          | Visibility      | Type       | Description          |
| -------------- | --------------- | ---------- | -------------------- |
| the field name | visibility kind | value type | A short description. |

#### Field

The name of the field. This should be in the exact casing and format that is depicted from the API, not a canonicalised form.

#### Visibility

The visibility kind of the field. This can be either "required" or "optional".

#### Type

The actual value type of the field. This can be a "string", "number", "boolean", "null", a composite object which should have a codeblock representation at the description of the parameter table, or an "array\[type]" where "type" is one of the aformentioned. Fields that accept multiple types can be expressed using "or", for example, "string or null".

#### Description

A short description of the field. Detailed information may be specified at the description of the parameter table, not inside the table itself.

### Status Code Table

Status Code tables are a short and simple way to summarise the state of specific responses from an endpoint.

| Code     | Description                            |
| -------- | -------------------------------------- |
| the code | A summary of the reason for that code. |

### Important Blockquote

An important blockquote is a blockquote containing important information that requires highlighting or distinction from a paragraph. This is ideal for long texts of information that would otherwise not fit well as a bolded paragraph. Some markdown renderers and websites (namely GitHub) support Important blockquotes as a specific block style separate to normal blockquotes.

> **Important**
> Important information goes here.

```
> **Information**
> Important information goes here.
```

### Note Blockquote

A note blockquote is quite simply, a blockquote containing information that should be taken note of pertaining to the resource it is used in. Some markdown renderers and websites (namely GitHub) support Note blockquotes as a specific block style separate to normal blockquotes.

> **Note**
> Note description goes here.

```
> **Note**
> Note description goes here.
```

### Warning Blockquote

A warning blockquote is a blockquote containing information that is critical to the resource it is used in. They should accurately highlight the information including any relevant references or source links. Like Note blockquotes, some markdown renderers and websites (namely GitHub) support Warning blockquotes as a specific block style separate to normal blockquotes.

> **Warning**
> Warning description goes here.

```
> **Warning**
> Warning description goes here.
```
