## Table

### info

Query information about the fate table (real storage address, number, schema, etc.)

```bash
flow table info [options]
```

**Options**

| parameter name | required | type | description
| :-------- | :--- | :----- | -------------- |
| name | yes | string | fate table name |
| namespace | yes | string | fate table namespace |

**return parameters** 

| parameter name | type | description |
| :------ | :----- | -------- |
| retcode | int | return code |
| retmsg | string | return message |
| data | object | return data |

Sample

```json
{
    "data": {
        "address": {
            "home": null,
            "name": "breast_hetero_guest",
            "namespace": "experiment"
        },
        "count": 569,
        "exists": 1,
        "namespace": "experiment",
        "partition": 4,
        "schema": {
            "header": "y,x0,x1,x2,x3,x4,x5,x6,x7,x8,x9",
            "sid": "id"
        },
        "table_name": "breast_hetero_guest"
    },
    "retcode": 0,
    "retmsg": "success"
}
```

### delete

You can delete table data with table delete

```bash
flow table delete [options]
```

**Options**

| parameter name | required | type | description |
| :-------- | :--- | :----- | -------------- |
| name | yes | string | fate table name |
| namespace | yes | string | fate table namespace |

**return parameters** 

| parameter name | type | description |
| :------ | :----- | -------- |
| retcode | int | return code |
| retmsg | string | return message |
| data | object | return data |

Sample

```json
{
    "data": {
        "namespace": "xxx",
        "table_name": "xxx"
    },
    "retcode": 0,
    "retmsg": "success"
}
```

### bind

Real storage addresses can be mapped to fate storage tables via table bind

```bash
flow table bind [options]
```

Note: conf_path is the parameter path, the specific parameters are as follows

**Options**

| parameter name | required | type | description |
| :------------- | :--- | :----- | ------------------------------------- |
| name | yes | string | fate table name |
| namespace | yes | string | fate table namespace |
| engine | yes | string | storage engine, supports "HDFS", "MYSQL", "PATH" |
| yes | object | real storage address |
| drop | no | int | Overwrite previous information |
| head | no | int | Whether there is a data table header |
| id_delimiter | no | string | Data separator |
| id_column | no | string | id field |
| feature_column | no | array | feature_field |

**Example** 

- hdfs

```json
{
    "namespace": "experiment",
    "name": "breast_hetero_guest",
    "engine": "HDFS",
    "address": {
        "name_node": "hdfs://fate-cluster",
        "path": "/data/breast_hetero_guest.csv"
    },
    "id_delimiter": ",",
    "head": 1,
    "partitions": 10
}
```

- mysql

```json
{
  "engine": "MYSQL",
  "address": {
    "user": "fate",
    "passwd": "fate",
    "host": "127.0.0.1",
    "port": 3306,
    "db": "experiment",
    "name": "breast_hetero_guest"
  },
  "namespace": "experiment",
  "name": "breast_hetero_guest",
  "head": 1,
  "id_delimiter": ",",
  "partitions": 10,
  "id_column": "id",
  "feature_column": "y,x0,x1,x2,x3,x4,x5,x6,x7,x8,x9"
}
```

- PATH

```json
{
    "namespace": "xxx",
    "name": "xxx",
    "engine": "PATH",
    "address": {
        "path": "xxx"
    }
}
```
**return parameters** 

| parameter name | type | description |
| :------ | :----- | -------- |
| retcode | int | return code |
| retmsg | string | return message |
| data | object | return data |

Sample

```json
{
    "data": {
        "namespace": "xxx",
        "table_name": "xxx"
    },
    "retcode": 0,
    "retmsg": "success"
}
```