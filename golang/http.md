# Golang http

## HTTPクライアントの作成

- リクエストの作成にはGET,Head,Post,PostFormが使える
- 受け取ったレスポンスのボディは使用後は必ずCloseする
- ヘッダの設定をする場合にはClientを使う

```golang
resp, err := http.Get("http://example.com/")
if err != nil {
    // handle error
}
defer resp.Body.Close()

// do something
```

## HTTPサーバの作成

- サーバの作成にはhttp.ListenAndServeを使う
- ハンドラの登録にはhttp.Handle、http.HandleFuncを使う
- より細かな設定を行うにはServerを作成する

```golang
http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
 fmt.Fprin(w, "Hello, World!")
})

log.Fatal(http.ListenAndServe(":8080", nil))
```
