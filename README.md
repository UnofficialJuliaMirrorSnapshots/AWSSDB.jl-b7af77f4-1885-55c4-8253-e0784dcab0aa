# AWSSDB

AWS SimpleDB Interface for Julia

[![Build Status](https://travis-ci.org/samoconnor/AWSSDB.jl.svg)](https://travis-ci.org/samoconnor/AWSSDB.jl)

```julia
using AWSSDB

aws = AWSCore.aws_config()

sdb_create_domain(aws, "my-db")

sdb_put(aws, "my-db", "key1", Pair["a1" => "1", "a2" => "2"])

@test sdb_get(aws, "my-db", "key1") == Pair["a1" => "1", "a2" => "2"]

db = SimpleDB(aws, "my-db")
db["key2"] = Pair["a1" => "1", "a2" => "2"]
@test db["key2"] == Pair["a1" => "1", "a2" => "2"]

for (key, attributes) in sdb_select(aws, "select * from `my_db`")
    println("$key: $attributes"
end

sdb_delete_item(aws, "my-db", "key1")

sdb_delete_domain(aws, "my-db")
```
