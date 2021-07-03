### 路由
#### 普通路由
```go
r.Get           ("path",func(writer uc.ResponseWriter, request uc.Request))

r.POST          ("path",func(writer uc.ResponseWriter, request uc.Request))

r.DELETE        ("path",func(writer uc.ResponseWriter, request uc.Request))

r.HEAD          ("path",func(writer uc.ResponseWriter, request uc.Request))

r.OPTIONS       ("path",func(writer uc.ResponseWriter, request uc.Request))

r.PUT           ("path",func(writer uc.ResponseWriter, request uc.Request))

r.PATCH         ("path",func(writer uc.ResponseWriter, request uc.Request))

r.CONNECT       ("path",func(writer uc.ResponseWriter, request uc.Request))
```

#### 匹配模糊路由
```go
r.Get("ab/:id/abc", func(writer uc.ResponseWriter, request uc.Request) {
	
    log.Println(request.Data.Get("id"))
    
})

r.Get("m/:id/:number", func(writer uc.ResponseWriter, request uc.Request) {
	
    log.Println(request.Data.Get("id"))
    
    log.Println(request.Data.Get("number"))
    
})
```