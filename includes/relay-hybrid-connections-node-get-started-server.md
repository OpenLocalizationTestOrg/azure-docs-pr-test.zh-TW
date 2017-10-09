### <a name="create-a-nodejs-application"></a>建立 Node.js 應用程式

新增名為 `listener.js` 的 JavaScript 檔案。

### <a name="add-hello-relay-npm-package"></a>新增 hello 轉送 NPM 封裝

在您的專案資料夾中從 Node 命令提示字元執行 `npm install hyco-ws`。

### <a name="write-some-code-tooreceive-messages"></a>撰寫一些程式碼 tooreceive 訊息

1. 新增下列常數 toohello 頂端 hello hello`listener.js`檔案。
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. 新增下列常數 toohello hello `listener.js` hello 混合式連線詳細資料的檔案。 方括號中的 hello 預留位置取代為 hello 建立 hello 混合式連接時取得的值。
   
   1. `const ns`-hello 轉送命名空間。 是確定 toouse hello 完整限定的命名空間名稱。例如， `{namespace}.servicebus.windows.net`。
   2. `const path`-hello hello 混合式連接名稱。
   3. `const keyrule`-hello hello SAS 金鑰名稱。
   4. `const key`-hello SAS 金鑰值。

3. 新增下列程式碼 toohello hello`listener.js`檔案：
   
    ```js
    var wss = WebSocket.createRelayedServer(
    {
        server : WebSocket.createRelayListenUri(ns, path),
        token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
    }, 
    function (ws) {
        console.log('connection accepted');
        ws.onmessage = function (event) {
            console.log(event.data);
        };
        ws.on('close', function () {
            console.log('connection closed');
        });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```
    listener.js 檔案看起來應該會像下面這樣：
   
    ```js
    const WebSocket = require('hyco-ws');
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    var wss = WebSocket.createRelayedServer(
        {
            server : WebSocket.createRelayListenUri(ns, path),
            token: WebSocket.createRelayToken('http://' + ns, keyrule, key)
        }, 
        function (ws) {
            console.log('connection accepted');
            ws.onmessage = function (event) {
                console.log(event.data);
            };
            ws.on('close', function () {
                console.log('connection closed');
            });       
    });
   
    console.log('listening');
   
    wss.on('error', function(err) {
        console.log('error' + err);
    });
    ```

