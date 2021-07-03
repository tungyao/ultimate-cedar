## 群组方法
群组方法可以一直嵌套，并且也能使用中间件
```go
r.Group("a", func(groups *uc.Groups) {
    groups.Get("b", func(writer uc.ResponseWriter, request uc.Request) {
        writer.Write([]byte("get"))
    })
    groups.Patch("b", func(writer uc.ResponseWriter, request uc.Request) {
        writer.Write([]byte("trace"))
    })
})
```