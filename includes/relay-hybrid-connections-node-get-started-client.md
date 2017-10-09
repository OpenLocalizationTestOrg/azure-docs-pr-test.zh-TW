### <a name="create-a-nodejs-application"></a>建立 Node.js 應用程式

新增名為 `sender.js` 的 JavaScript 檔案。

### <a name="add-hello-relay-npm-package"></a>新增 hello 轉送 NPM 封裝

在您的專案資料夾中從 Node 命令提示字元執行 `npm install hyco-ws`。

### <a name="write-some-code-toosend-messages"></a>撰寫一些程式碼 toosend 訊息

1. 新增下列 hello `constants` toohello 頂端 hello`sender.js`檔案。
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. 新增下列常數 toohello hello `sender.js` hello 混合式連線詳細資料的檔案。 方括號中的 hello 預留位置取代為 hello 建立 hello 混合式連接時取得的值。
   
   1. `const ns`-hello 轉送命名空間。 是確定 toouse hello 完整限定的命名空間名稱。例如， `{namespace}.servicebus.windows.net`。
   2. `const path`-hello hello 混合式連接名稱。
   3. `const keyrule`-hello hello SAS 金鑰名稱。
   4. `const key`-hello SAS 金鑰值。

3. 新增下列程式碼 toohello hello`sender.js`檔案：
   
    ```js
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```
    sender.js 檔案看起來應該會像下面這樣：
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
   
    const ns = "{RelayNamespace}";
    const path = "{HybridConnectionName}";
    const keyrule = "{SASKeyName}";
    const key = "{SASKeyValue}";
   
    WebSocket.relayedConnect(
        WebSocket.createRelaySendUri(ns, path),
        WebSocket.createRelayToken('http://'+ns, keyrule, key),
        function (wss) {
            readline.on('line', (input) => {
                wss.send(input, null);
            });
   
            console.log('Started client interval.');
            wss.on('close', function () {
                console.log('stopping client interval');
                process.exit();
            });
        }
    );
    ```

