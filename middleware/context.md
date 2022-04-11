# context

就是原生context，在中间件使用时，context要重新赋予回去，并且要调用`handlerFunc`方法

```go
logMiddleware := uc.MiddlewareInterceptor(func (writer uc.ResponseWriter, request uc.Request, handlerFunc uc.HandlerFunc) {
    log.Println("log", request.URL.String())
    // add context
    request.Context = context.WithValue(request.Context, "member", "hello")
    handlerFunc(writer, request)
})
```