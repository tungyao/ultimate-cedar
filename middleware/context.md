# context

就是原生context，在中间件使用时

```go
logMiddleware := uc.MiddlewareInterceptor(func (writer uc.ResponseWriter, request uc.Request, handlerFunc uc.HandlerFunc) {
    log.Println("log", request.URL.String())
    // add context
	request.Context.Set("member","hello")
    handlerFunc(writer, request)
})
```

在路由中获取时
```go
request.Context.Value(key any)
```