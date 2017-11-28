### <a name="create-a-nodejs-application"></a><span data-ttu-id="0e3d6-101">建立 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="0e3d6-101">Create a Node.js application</span></span>

<span data-ttu-id="0e3d6-102">新增名為 `sender.js` 的 JavaScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="0e3d6-102">Create a new JavaScript file called `sender.js`.</span></span>

### <a name="add-the-relay-npm-package"></a><span data-ttu-id="0e3d6-103">新增轉送 NPM 套件</span><span class="sxs-lookup"><span data-stu-id="0e3d6-103">Add the Relay NPM package</span></span>

<span data-ttu-id="0e3d6-104">在您的專案資料夾中從 Node 命令提示字元執行 `npm install hyco-ws`。</span><span class="sxs-lookup"><span data-stu-id="0e3d6-104">Run `npm install hyco-ws` from a Node command prompt in your project folder.</span></span>

### <a name="write-some-code-to-send-messages"></a><span data-ttu-id="0e3d6-105">撰寫一些程式碼來傳送訊息</span><span class="sxs-lookup"><span data-stu-id="0e3d6-105">Write some code to send messages</span></span>

1. <span data-ttu-id="0e3d6-106">將下列 `constants` 新增至 `sender.js` 檔案開頭處。</span><span class="sxs-lookup"><span data-stu-id="0e3d6-106">Add the following `constants` to the top of the `sender.js` file.</span></span>
   
    ```js
    const WebSocket = require('hyco-ws');
    const readline = require('readline')
        .createInterface({
            input: process.stdin,
            output: process.stdout
        });;
    ```
2. <span data-ttu-id="0e3d6-107">將下列常數新增至 `sender.js` 檔案，以取得混合式連線詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0e3d6-107">Add the following constants to the `sender.js` file for the hybrid connection details.</span></span> <span data-ttu-id="0e3d6-108">將方括號中的預留位置取代為您在建立混合式連線時所取得的值。</span><span class="sxs-lookup"><span data-stu-id="0e3d6-108">Replace the placeholders in brackets with the values you obtained when you created the hybrid connection.</span></span>
   
   1. <span data-ttu-id="0e3d6-109">`const ns` - 轉送命名空間。</span><span class="sxs-lookup"><span data-stu-id="0e3d6-109">`const ns` - The Relay namespace.</span></span> <span data-ttu-id="0e3d6-110">務必使用完整命名空間名稱；例如，`{namespace}.servicebus.windows.net`。</span><span class="sxs-lookup"><span data-stu-id="0e3d6-110">Be sure to use the fully qualified namespace name; for example, `{namespace}.servicebus.windows.net`.</span></span>
   2. <span data-ttu-id="0e3d6-111">`const path` - 混合式連線的名稱。</span><span class="sxs-lookup"><span data-stu-id="0e3d6-111">`const path` - The name of the hybrid connection.</span></span>
   3. <span data-ttu-id="0e3d6-112">`const keyrule` - SAS 金鑰的名稱。</span><span class="sxs-lookup"><span data-stu-id="0e3d6-112">`const keyrule` - The name of the SAS key.</span></span>
   4. <span data-ttu-id="0e3d6-113">`const key` - SAS 金鑰值。</span><span class="sxs-lookup"><span data-stu-id="0e3d6-113">`const key` - The SAS key value.</span></span>

3. <span data-ttu-id="0e3d6-114">將下列程式碼新增至 `sender.js` 檔案：</span><span class="sxs-lookup"><span data-stu-id="0e3d6-114">Add the following code to the `sender.js` file:</span></span>
   
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
    <span data-ttu-id="0e3d6-115">sender.js 檔案看起來應該會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="0e3d6-115">Here is what your sender.js file should look like:</span></span>
   
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

