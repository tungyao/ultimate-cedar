# websocket
> https://datatracker.ietf.org/doc/html/rfc6455#section-5.3
## template

```go

func TestWebsocket(t *testing.T) {
	r := uc.NewRouter()
	// r.Debug()
	r.Get("/ws", func(writer uc.ResponseWriter, request uc.Request) {
		uc.WebsocketSwitchProtocol(writer, request, "123", func(value *uc.CedarWebSocketBuffReader) {
			log.Println(value)
		})
	})
	r.Post("/ws/push", func(writer uc.ResponseWriter, request uc.Request) {
		uc.WebsocketSwitchPush("123", 0x1, []byte("hello world"))
	})
	http.ListenAndServe(":8080", r)
}

```

### explain
在每秒20次READ ,且在 2048byte 下有良好的表现 ,推荐使用的方法
#### client端连接 ,server进行推送
### 方法
#### WebsocketSwitchProtocol

```go
// CedarWebSocketBuffReader 读取websocket协议,这里的websocket主要针对 4086byte 的文本格式
// Data 读取的文本载荷
// Length 文本[]byte长度
type CedarWebSocketBuffReader struct {
    Data   []byte
    Length int
    cedarWebsocketBuffScan
}

uc.WebsocketSwitchProtocol(uc.ResponseWriter,uc.Request, key string, fn func(value *uc.CedarWebSocketBuffReader))
```

### 解释
* key 用于推送的唯一凭证
* fn 在client端连接后 ,收取到消息后 ,执行的方法

### 方法
#### WebsocketSwitchPush

```go
WebsocketSwitchPush(key string, op int, data []byte) error
```

### 解释
* key 用于推送的唯一凭证
* op websocket的op标识
* data 载荷
