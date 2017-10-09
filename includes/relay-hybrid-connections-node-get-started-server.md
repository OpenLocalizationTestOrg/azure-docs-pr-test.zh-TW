### <a name="create-a-nodejs-application"></a><span data-ttu-id="f8e32-101">建立 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="f8e32-101">Create a Node.js application</span></span>

<span data-ttu-id="f8e32-102">新增名為 `listener.js` 的 JavaScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="f8e32-102">Create a new JavaScript file called `listener.js`.</span></span>

### <a name="add-hello-relay-npm-package"></a><span data-ttu-id="f8e32-103">新增 hello 轉送 NPM 封裝</span><span class="sxs-lookup"><span data-stu-id="f8e32-103">Add hello Relay NPM package</span></span>

<span data-ttu-id="f8e32-104">在您的專案資料夾中從 Node 命令提示字元執行 `npm install hyco-ws`。</span><span class="sxs-lookup"><span data-stu-id="f8e32-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-tooreceive-messages"></a><span data-ttu-id="f8e32-105">撰寫一些程式碼 tooreceive 訊息</span><span class="sxs-lookup"><span data-stu-id="f8e32-105">Write some code tooreceive messages</span></span>

1. <span data-ttu-id="f8e32-106">新增下列常數 toohello 頂端 hello hello`listener.js`檔案。</span><span class="sxs-lookup"><span data-stu-id="f8e32-106">Add hello following constant toohello top of hello `listener.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    ```
2. <span data-ttu-id="f8e32-107">新增下列常數 toohello hello `listener.js` hello 混合式連線詳細資料的檔案。</span><span class="sxs-lookup"><span data-stu-id="f8e32-107">Add hello following constants toohello `listener.js` file for hello hybrid connection details.</span></span> <span data-ttu-id="f8e32-108">方括號中的 hello 預留位置取代為 hello 建立 hello 混合式連接時取得的值。</span><span class="sxs-lookup"><span data-stu-id="f8e32-108">Replace hello placeholders in brackets with hello values you obtained when you created hello hybrid connection.</span></span>
   
   1. <span data-ttu-id="f8e32-109">`const ns`-hello 轉送命名空間。</span><span class="sxs-lookup"><span data-stu-id="f8e32-109">`const ns` - hello Relay namespace.</span></span> <span data-ttu-id="f8e32-110">是確定 toouse hello 完整限定的命名空間名稱。例如， `{namespace}.servicebus.windows.net`。</span><span class="sxs-lookup"><span data-stu-id="f8e32-110">Be sure toouse hello fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="f8e32-111">`const path`-hello hello 混合式連接名稱。</span><span class="sxs-lookup"><span data-stu-id="f8e32-111">`const path` - hello name of hello hybrid connection.</span></span>
   3. <span data-ttu-id="f8e32-112">`const keyrule`-hello hello SAS 金鑰名稱。</span><span class="sxs-lookup"><span data-stu-id="f8e32-112">`const keyrule` - hello name of hello SAS key.</span></span>
   4. <span data-ttu-id="f8e32-113">`const key`-hello SAS 金鑰值。</span><span class="sxs-lookup"><span data-stu-id="f8e32-113">`const key` - hello SAS key value.</span></span>

3. <span data-ttu-id="f8e32-114">新增下列程式碼 toohello hello`listener.js`檔案：</span><span class="sxs-lookup"><span data-stu-id="f8e32-114">Add hello following code toohello `listener.js` file:</span></span>
   
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
    <span data-ttu-id="f8e32-115">listener.js 檔案看起來應該會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="f8e32-115">Here is what your listener.js file should look like:</span></span>
   
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

