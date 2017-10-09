### <a name="create-a-nodejs-application"></a><span data-ttu-id="b1b1b-101">建立 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="b1b1b-101">Create a Node.js application</span></span>

<span data-ttu-id="b1b1b-102">新增名為 `sender.js` 的 JavaScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="b1b1b-102">Create a new JavaScript file called `sender.js`.</span></span>

### <a name="add-hello-relay-npm-package"></a><span data-ttu-id="b1b1b-103">新增 hello 轉送 NPM 封裝</span><span class="sxs-lookup"><span data-stu-id="b1b1b-103">Add hello Relay NPM package</span></span>

<span data-ttu-id="b1b1b-104">在您的專案資料夾中從 Node 命令提示字元執行 `npm install hyco-ws`。</span><span class="sxs-lookup"><span data-stu-id="b1b1b-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-toosend-messages"></a><span data-ttu-id="b1b1b-105">撰寫一些程式碼 toosend 訊息</span><span class="sxs-lookup"><span data-stu-id="b1b1b-105">Write some code toosend messages</span></span>

1. <span data-ttu-id="b1b1b-106">新增下列 hello `constants` toohello 頂端 hello`sender.js`檔案。</span><span class="sxs-lookup"><span data-stu-id="b1b1b-106">Add hello following `constants` toohello top of hello `sender.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. <span data-ttu-id="b1b1b-107">新增下列常數 toohello hello `sender.js` hello 混合式連線詳細資料的檔案。</span><span class="sxs-lookup"><span data-stu-id="b1b1b-107">Add hello following constants toohello `sender.js` file for hello hybrid connection details.</span></span> <span data-ttu-id="b1b1b-108">方括號中的 hello 預留位置取代為 hello 建立 hello 混合式連接時取得的值。</span><span class="sxs-lookup"><span data-stu-id="b1b1b-108">Replace hello placeholders in brackets with hello values you obtained when you created hello hybrid connection.</span></span>
   
   1. <span data-ttu-id="b1b1b-109">`const ns`-hello 轉送命名空間。</span><span class="sxs-lookup"><span data-stu-id="b1b1b-109">`const ns` - hello Relay namespace.</span></span> <span data-ttu-id="b1b1b-110">是確定 toouse hello 完整限定的命名空間名稱。例如， `{namespace}.servicebus.windows.net`。</span><span class="sxs-lookup"><span data-stu-id="b1b1b-110">Be sure toouse hello fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="b1b1b-111">`const path`-hello hello 混合式連接名稱。</span><span class="sxs-lookup"><span data-stu-id="b1b1b-111">`const path` - hello name of hello hybrid connection.</span></span>
   3. <span data-ttu-id="b1b1b-112">`const keyrule`-hello hello SAS 金鑰名稱。</span><span class="sxs-lookup"><span data-stu-id="b1b1b-112">`const keyrule` - hello name of hello SAS key.</span></span>
   4. <span data-ttu-id="b1b1b-113">`const key`-hello SAS 金鑰值。</span><span class="sxs-lookup"><span data-stu-id="b1b1b-113">`const key` - hello SAS key value.</span></span>

3. <span data-ttu-id="b1b1b-114">新增下列程式碼 toohello hello`sender.js`檔案：</span><span class="sxs-lookup"><span data-stu-id="b1b1b-114">Add hello following code toohello `sender.js` file:</span></span>
   
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
    <span data-ttu-id="b1b1b-115">sender.js 檔案看起來應該會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="b1b1b-115">Here is what your sender.js file should look like:</span></span>
   
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

