### 集成方法

* 快速返回，要注意调用顺序
```go
r.Get("ccc", func(writer uc.ResponseWriter, request uc.Request) {
writer.Json.
    ContentType("application/json").
    AddHeader("time", "unix").
    Data(map[string]string{"a": "b"}).
    Status(403).
    Encode("123123").
    Send()
})

```