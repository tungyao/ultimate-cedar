## 中间件使用
1. 声明一个中间件方法
> 如果要继续执行， `handlerFunc()` 就需要使用
```go
echoMiddleware := uc.MiddlewareInterceptor(func(writer uc.ResponseWriter, request uc.Request, handlerFunc uc.HandlerFunc) {
	log.Println(request.URL.Query().Get("echo"))
	writer.Data("echo middle").Send()
	handlerFunc(writer, request) // here
})
```
2. 加入到中间件群组
```go
middleware := uc.MiddlewareChain{
	echoMiddleware,
}
```
3. 进行使用，2种方法都能使用
* 普通路由
  ```go
   r.Get("test_middle", middleware.Handler(func(writer uc.ResponseWriter, request uc.Request) {
       writer.Data("hello world").Send()
   }))
   ```
* 普通路由
  ```go
   r.Get("echo", func(writer uc.ResponseWriter, request uc.Request) {
       writer.Data("hello new_middle echo").Send()
   }, middleware)
   ```
* 群组路由
  ```go
   r.Group("new_middle", func(groups *uc.Groups) {
       groups.Get("echo", func(writer uc.ResponseWriter, request uc.Request) {
           writer.Data("hello new_middle echo").Send()
       }, logMiddlewareGroup)
   }, middleware)
   ```