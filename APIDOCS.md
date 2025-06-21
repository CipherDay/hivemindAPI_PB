# 1.`/api/client` Endpoint:
## a. POST `/register` :
- **Description:** Add a client to the hive.
- **Method:** `POST`.
- **Content-Type:** `application/json`.
### a.1 Request:
#### a.1.1 Headers:

| Key              | Value              | Required |
|------------------|--------------------|----------|
| `Content-Type`   | `application/json` | TRUE     |
| `x-hivemind-key` | `API-KEY`          | TRUE     |
#### a.1.2 Body:
```
{
uuid:"XXXXXXXXXX"
}
```

### a.2 Response:
#### a.2.1 Success(200):
```
{
status:true,
data:{
      uuid:"XXXXXXXXXX"
     }
}

```
#### a.2.2 Error(500):
```
{
status:false,
message:"error message",
error:ZodError[]
}
```

# 2. `/api/worker` Endpoint:
## a. POST `/register` :
- **Description:** Add a worker to the hive.
- **Method:** `POST`.
- **Content-Type:** `application/json`.
### a.1 Request:
#### a.1.1 Headers:

| Key              | Value              | Required |
|------------------|--------------------|----------|
| `Content-Type`   | `application/json` | TRUE     |
| `x-hivemind-key` | `API-KEY`          | TRUE     |
#### a.1.2 Body:
```
{
uuid:"XXXXXXXXXX",
name:"..."
}
```

### a.2 Response:
#### a.2.1 Success(200):
```
{
status:true,
data:{
      uuid:"XXXXXXXXXX",
      name:"..."
     }
}

```
#### a.2.2 Error(500):
```
{
status:false,
message:"error message",
error:ZodError[]
}
```

## a. GET `/:uuid/jobs` :
- **Description:** View available jobs to the specified worker.
- **Method:** `GET`.
- **Content-Type:** `application/json`.
### Path Parameters:

| Parameter | Type   | Description                  | Required |
|-----------|--------|------------------------------|----------|
| `uuid`    | string | The unique id for the worker | TRUE     |

### a.1 Request:
#### a.1.1 Headers:

| Key              | Value     | Required |
|------------------|-----------|----------|
| `x-hivemind-key` | `API-KEY` | TRUE     |
### a.2 Response:
#### a.2.1 Success(200):
```
{
status:true,
data:{
      uuid:"XXXXXXXXXX",  
	  clientuuid:"XXXXXXXXXX",  
	  workeruuid:"XXXXXXXXXX",  
      state:"working",  
      job:"...."
     }
}

```
#### a.2.2 Error(500):
```
{
status:false,
message:"Can't find job",
}
```
#### a.2.3 Error(404):
```
{
status:false,
message:"Can't find worker with this uuid.",
}
```
#### a.2.3 Error(400):
```
{
status:false,
message:"There No Jobs.",
}
```
# 3. `/api/job` Endpoint:
## a. POST `/request :
- **Description:** Add a job to the poll.
- **Method:** `POST`.
- **Content-Type:** `application/json`.
### a.1 Request:
#### a.1.1 Headers:

| Key              | Value              | Required |
|------------------|--------------------|----------|
| `Content-Type`   | `application/json` | TRUE     |
| `x-hivemind-key` | `API-KEY`          | TRUE     |
#### a.1.2 Body:
```
{
uuid:"XXXXXXXXXX",  
clientuuid:"XXXXXXXXXX",  
workeruuid:NULL,
state:"waiting",  
job:"...."
}
```

### a.2 Response:
#### a.2.1 Success(200):
```
{
status:true,
data:{
      uuid:"XXXXXXXXXX",  
      clientuuid:"XXXXXXXXXX",  
      workeruuid:NULL,
      state:"waiting",  
      job:"...."
     }
}
```
#### a.2.2 Error(500):
```
{
status:false,
message:"error message",
error:ZodError[]
}
```
#### a.2.3 Error(404):
```
{
status:false,
message:"Could not find client uuid.",
}
```

## a. GET `/:uuid` :
- **Description:** View available jobs to the specified worker.
- **Method:** `GET`.
- **Content-Type:** `application/json`.
### Path Parameters:

| Parameter | Type   | Description               | Required |
|-----------|--------|---------------------------|----------|
| `uuid`    | string | The unique id for the job | TRUE     |

### a.1 Request:
#### a.1.1 Headers:

| Key              | Value     | Required |
|------------------|-----------|----------|
| `x-hivemind-key` | `API-KEY` | FALSE    |
### a.2 Response:
#### a.2.1 Success(200):
```
{
status:true,
data:{
      uuid:"XXXXXXXXXX",  
	  clientuuid:"XXXXXXXXXX",  
	  workeruuid:"XXXXXXXXXX",  
      state:"waiting" or "working" or "done",  
      job:"....",
      result?:"...."
     }
}

```
#### a.2.2 Error(500):
```
{
status:false,
message:"error message",
error?:ZodError[]
}
```
#### a.2.3 Error(404):
```
{
status:false,
message:"Can't find job.",
}
```
## a.POST `/:uuid/done`:
- **Description:** Mark the `uuid`specified job as done.
- **Method:** `POST`.
- **Content-Type:** `application/json`.
### Path Parameters:

| Parameter | Type   | Description               | Required |
|-----------|--------|---------------------------|----------|
| `uuid`    | string | The unique id for the job | TRUE     |

### a.1 Request:
#### a.1.1 Headers:

| Key              | Value     | Required |
|------------------|-----------|----------|
| `x-hivemind-key` | `API-KEY` | TRUE     |
### a.2 Request:
#### a.2.1 Body:
```
{
uuid:"XXXXXXXX",  
clientuuid:"XXXXXXX",  
workeruuid:"XXXXXXX",  
result:"...",
}
```

### a.3 Response:
#### a.3.1 Success(200):
```
{
status:true,
data:{
      uuid:"XXXXXXXXXX",  
	  clientuuid:"XXXXXXXXXX",  
	  workeruuid:"XXXXXXXXXX",  
      state:"done",  
      job:"....",
      result:"..."
     }
}

```
#### a.3.2 Error(500):
```
{
status:false,
message:"error message",
error?:ZodError[]
}
```
#### a.3.3 Error(404):
```
{
status:false,
message:"Can't find the job.",
}
```
#### a.3.4 Error(400):
```
{
status:false,
message:"Can't find the client or worker with this job.",
}
```