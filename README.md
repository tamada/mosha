# mosha

This project collects data from GitHub based on the concept Project as a City.

## `/api/{USER}/{PROJECT}/population`

This endpoint shows the population metric of the project.

### `POST /api/{USER}/{PROJECT}/population`

#### Response

```js
{
    "id": "process id",
    "key": "PROCESS_KEY",
    "project": "tamada/pochi",
    "metric": "population",
    "status": "queueed",
    "url": "/api/queue/{id}"
}
```

* `status`
    * `queueed` means the process is in queue, or
    * `done` means the process was finished.

### `GET  /api/{USER}/{PROJECT}/population`

#### Query Params

* `period`
    * acceptable values are: `day`, `month`, and `year`
* `start` means start date of `period`.  format: `2006-01-02`.
    * If this parameter did not specified, `mosha` uses the oldest date of the population.

## `/api/{USER}/{PROJECT}/size`

### `POST /api/{USER}/{PROJECT}/size`

#### Response

```js
{
    "id": "process id",
    "key": "PROCESS_KEY",
    "project": "tamada/pochi",
    "metric": "size"
    "status": "queueed"
}
```

* `status`
    * `queueed` means the process is in queue, or
    * `done` means the process was finished.

### `GET  /api/{USER}/{PROJECT}/size`

* `period`
    * acceptable values are: `day`, `month`, and `year`
* `start` means start date of `period`.  format: `2006-01-02`.
    * If this parameter did not specified, `mosha` uses the oldest date of the population.

## `api/{USER}/{PROJECT}/problems`


## `/api/{USER}/{PROJECT}/problemsolving`

## `/api/{USER}/{PROJECT}/capability`

## `/api/queue`

### `GET /api/queue`

#### Response

##### 200

```js
{ "status": "idle", "size": 0 }
```

* `status` represents the status of the background queue.  In `mosha`, all process executing based on queue.
    * `idle`, `executing`, or `waiting`.
        * `idle`: no entries in the queue.
        * `executing`: executing a process.
        * `waiting`: remaining processes in the queue, however, no API requests limit.
* `size` represents the length of processes in the queue.

## `/api/queue/{process_id}`

### `GET /api/queue/{proces_id}`

* returns the status of the specified process.

#### Response

##### 200

```js
{
    "id": "process_id",
    "status": "done",
    "project": "tamada/mosha",
    "metric": "population",
    "last_update": "2006-01-02 03:04:05"
}
```

* `id` shows process id.
* `project` shows target project.
* `metric` means the processing metric type.
* `status`
    * `queueed` means the process is in queue, or
    * `done` means the process was finished.
* `last_update` means last updated date.

##### 404 (specified id did not found)

```js
{
    "id": "process_id",
    "message": "process_id: process id not found"
}
```


### `DELETE /api/queue/{process_id}`

#### Query Parameters

* `key` is shown by requesting `POST` to some endpoints.

#### Response

* Always HTTP 200 OK.

```js
{ "id": "process_id" }
```
