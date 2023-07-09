### `GET /api/client/servers/:serverId/schedules`

Returns all the schedules belonging to a given server.

### Responses

| Code | Description                  |
| ---- | ---------------------------- |
| 200  | List of schedules for server |

### Example Body

```json
{
  "object": "list",
  "data": [
    {
      "object": "server_schedule",
      "attributes": {
        "id": 1,
        "name": "Sample Schedule",
        "cron": {
          "day_of_week": "1",
          "day_of_month": "15",
          "month": "6",
          "hour": "12",
          "minute": "30"
        },
        "is_active": true,
        "is_processing": false,
        "only_when_online": true,
        "last_run_at": "2023-06-10T14:30:00+00:00",
        "next_run_at": "2023-06-17T12:30:00+00:00",
        "created_at": "2023-06-10T10:00:00+00:00",
        "updated_at": "2023-06-10T10:30:00+00:00",
        "relationships": {
          "tasks": {
            "object": "list",
            "data": [
              {
                "object": "schedule_task",
                "attributes": {
                  "id": 1,
                  "sequence_id": 1,
                  "action": "command",
                  "payload": "say Hello, world!",
                  "time_offset": 10,
                  "is_queued": true,
                  "continue_on_failure": false,
                  "created_at": "2023-06-10T10:00:00+00:00",
                  "updated_at": "2023-06-10T10:30:00+00:00"
                }
              }
            ]
          }
        }
      }
    }
  ]
}
```

### `POST /api/client/servers/:serverId/schedules`

Stores a new schedule for a server.

### Request Body

| Name             | Visibility | Type    | Description                   |
| ---------------- | ---------- | ------- | ----------------------------- |
| name             | Required   | string  | Name of the schedule          |
| day_of_week      | Required   | string  | Day of the week               |
| month            | Required   | string  | Month                         |
| day_of_month     | Required   | string  | Day of the month              |
| hour             | Required   | string  | Hour                          |
| minute           | Required   | string  | Minute                        |
| is_active        | Optional   | boolean | Indicates if it is active     |
| only_when_online | Optional   | boolean | Execute schedule when online. |

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 200  | Created schedule for server |

### `GET /api/client/servers/:serverId/schedules/:scheduleId`

Returns a specific schedule for the server.

### Responses

| Code | Description             |
| ---- | ----------------------- |
| 200  | Schedule for the server |

### Example Body

```json
{
  "object": "server_schedule",
  "attributes": {
    "id": 1,
    "name": "Sample Schedule",
    "cron": {
      "day_of_week": "1",
      "day_of_month": "15",
      "month": "6",
      "hour": "12",
      "minute": "30"
    },
    "is_active": true,
    "is_processing": false,
    "only_when_online": true,
    "last_run_at": "2023-06-10T14:30:00+00:00",
    "next_run_at": "2023-06-17T12:30:00+00:00",
    "created_at": "2023-06-10T10:00:00+00:00",
    "updated_at": "2023-06-10T10:30:00+00:00",
    "relationships": {
      "tasks": {
        "object": "list",
        "data": [
          {
            "object": "schedule_task",
            "attributes": {
              "id": 1,
              "sequence_id": 1,
              "action": "command",
              "payload": "say Hello, world!",
              "time_offset": 10,
              "is_queued": true,
              "continue_on_failure": false,
              "created_at": "2023-06-10T10:00:00+00:00",
              "updated_at": "2023-06-10T10:30:00+00:00"
            }
          }
        ]
      }
    }
  }
}
```

### `POST /api/client/servers/:serverId/schedules/:scheduleId`

Updates a specific schedule with new data provided.

### Request Body

| Name             | Visibility | Type    | Description                   |
| ---------------- | ---------- | ------- | ----------------------------- |
| name             | Required   | string  | Name of the schedule          |
| day_of_week      | Required   | string  | Day of the week               |
| month            | Required   | string  | Month                         |
| day_of_month     | Required   | string  | Day of the month              |
| hour             | Required   | string  | Hour                          |
| minute           | Required   | string  | Minute                        |
| is_active        | Optional   | boolean | Indicates if it is active     |
| only_when_online | Optional   | boolean | Execute schedule when online. |

### Responses

| Code | Description                 |
| ---- | --------------------------- |
| 200  | Updated schedule for server |

### `POST /api/client/servers/:serverId/schedules/:scheduleId/execute`

Executes a given schedule immediately rather than waiting for its normally scheduled time to pass.

### Responses

| Code | Description        |
| ---- | ------------------ |
| 200  | Schedule triggered |

### `DELETE /api/client/servers/:serverId/schedules/:scheduleId`

Deletes a schedule and its associated tasks.

### Responses

| Code | Description      |
| ---- | ---------------- |
| 204  | Schedule deleted |

### `POST /api/client/servers/{server}/schedules/:scheduleId/tasks`

Create a new task for a given schedule and store it in the database.

### Request Parameters

| Name     | Type   | Description        |
| -------- | ------ | ------------------ |
| server   | string | ID of the server   |
| schedule | string | ID of the schedule |

### Body

| Name                | Visibility | Type    | Description              |
| ------------------- | ---------- | ------- | ------------------------ |
| action              | Required   | string  | Action for the task      |
| payload             | Requied    | string  | Payload for the task     |
| time_offset         | Required   | string  | Time offset for the task |
| continue_on_failure | Optional   | boolean | Continue on failure flag |

### Responses

| Code | Description               |
| ---- | ------------------------- |
| 200  | Created task for schedule |
| 403  | Task limit exceeded       |

### Example Response

```json
{
  "object": "schedule_task",
  "attributes": {
    "id": 6,
    "sequence_id": 1,
    "action": "command",
    "payload": "say Hello World",
    "time_offset": 0,
    "is_queued": false,
    "continue_on_failure": true,
    "created_at": "2020-10-29T01:09:03+00:00",
    "updated_at": "2020-10-29T01:09:03+00:00"
  }
}
```

### `POST /api/client/servers/{server}/schedules/:scheduleId/tasks/:taskId`

Updates a given task for a server.

### Request Parameters

| Name     | Type   | Description        |
| -------- | ------ | ------------------ |
| server   | string | ID of the server   |
| schedule | string | ID of the schedule |
| task     | string | ID of the task     |

### Body

| Name                | Visibility | Type    | Description              |
| ------------------- | ---------- | ------- | ------------------------ |
| action              | Required   | string  | Action for the task      |
| payload             | Requied    | string  | Payload for the task     |
| time_offset         | Required   | string  | Time offset for the task |
| continue_on_failure | Optional   | boolean | Continue on failure flag |

### Responses

| Code | Description               |
| ---- | ------------------------- |
| 200  | Updated task for schedule |
| 403  | Task not found or server's backup limit is set to 0. |

### Example Response

```json
{
  "object": "schedule_task",
  "attributes": {
    "id": 6,
    "sequence_id": 1,
    "action": "command",
    "payload": "say Hello World",
    "time_offset": 0,
    "is_queued": false,
    "continue_on_failure": true,
    "created_at": "2020-10-29T01:09:03+00:00",
    "updated_at": "2020-10-29T01:09:03+00:00"
  }
}
```

### `DELETE /api/client/servers/{server}/schedules/:scheduleId/tasks/:taskId`

Deletes a given task for a schedule. If there are subsequent tasks stored in the database for this schedule, their sequence IDs are decremented.

### Request Parameters

| Name     | Type   | Description        |
| -------- | ------ | ------------------ |
| server   | string | ID of the server   |
| schedule | string | ID of the schedule |
| task     | string | ID of the task     |

#### Responses

| Code | Description  |
| ---- | ------------ |
| 204  | Task deleted |
| 403  | Task not found or no permission |
