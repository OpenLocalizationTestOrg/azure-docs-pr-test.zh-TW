---
title: "aaaCreate Node.js 交談應用程式與 Azure App Service 中 Socket.IO"
description: "示範在裝載於 Azure 的 node.js Web 應用程式中使用 socket.io 的教學課程。"
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c4c4af36-3ecf-4619-b586-ca90d53ce35b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 3bd7867ccc297dc0a21c7a00cc9db06358877f5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a>在 Azure App Service 中使用 Socket.IO 建立 Node.js 聊天應用程式
Socket.IO 使用 WebSocket 提供 node.js 伺服器與用戶端之間的即時通訊。 它也支援使用舊的瀏覽器的後援 tooother 傳輸 （例如長輪詢）。 本教學課程將逐步引導您完成裝載為 Azure web 應用程式的基礎 Socket.IO 交談應用程式，並顯示您 tooscale hello 應用程式使用[Azure Redis 快取]。 如需 Socket.IO 的詳細資訊，請參閱 <http://socket.io/>。

> [!NOTE]
> 在這項工作的 hello 程序適用於太[App Service Web 應用程式]; 的雲端服務，請參閱[Azure 雲端服務上建置含有 Socket.IO 的 Node.js 交談應用程式]。
> 
> 

## <a name="download-hello-chat-example"></a>下載 hello 聊天範例
此專案中，我們將使用從 hello hello 聊天範例[Socket.IO GitHub 儲存機制]。 執行下列步驟 toodownload hello 範例 hello，並將它加入您先前建立的 toohello 專案。

1. 下載[ZIP 或 GZ 封存發行]的 hello Socket.IO 專案 （版本 1.3.5 已用於此文件）
2. 擷取 hello 封存及複製 hello**範例\\聊天**目錄 tooa 新位置。 例如，**\\node\\chat**。

## <a name="modify-appjs-and-install-modules"></a>修改 App.js 和安裝模組
1. 重新命名 hello **index.js**檔案太**app.js**。 這可讓 Azure toodetect： 這是一個 Node.js 應用程式。
2. 開啟 hello **app.js**文字編輯器中的檔案。 變更 hello 列包含`var io = require('../..')(server);`如下所示：
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. 開啟 hello **package.json**檔案，然後加入下的參考 toosocket.io `dependencies`，如下所示：
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. 從命令列 hello 變更 toohello **\\節點\\聊天**目錄和使用 npm tooinstall hello 模組所需的此應用程式：
   
        npm install
   
    這將會安裝至名為的子資料夾的 hello 模組**node_modules**。

## <a name="create-an-azure-web-app"></a>建立 Azure Web 應用程式
請遵循這些步驟 toocreate Azure web 應用程式、 啟用 Git 發行功能，然後再啟用 WebSocket 支援 hello web 應用程式。

> [!NOTE]
> toocomplete 本教學課程中，您需要 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure 免費試用</a>。
> 
> 

1. 安裝 hello Azure 命令列介面 (Azure CLI) 和連接 tooyour Azure 訂用帳戶。 請參閱[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)。
2. 如果這是您第一次設定 Azure 中的儲存機制，您會需要 toocreate 登入認證。 從 hello Azure CLI，請輸入下列命令的 hello:
   
        azure site deployment user set [username] [password]
3. 變更 toohello  **\\node\chat**目錄和使用 hello 下列命令 toocreate 新的 Azure web 應用程式和本機 Git 儲存機制。 這個命令也會建立名為 'azure' 的 Git 遠端。
   
        azure site create mysitename --git
   
    您必須將 'mysitename' 改成您的 Web 應用程式的唯一名稱。
4. 使用下列命令的 hello 認可 hello 現有檔案 toohello 本機儲存機制：
   
        git add .
        git commit -m "Initial commit"
5. 推送 hello 檔案 toohello Azure Web 應用程式儲存機制以 hello 下列命令：
   
        git push azure master
   
    系統出現提示時，請輸入步驟 2 中的認證。 Hello 伺服器上匯入模組時，您會收到狀態訊息。 此程序完成後，請將 Azure web 應用程式上裝載 hello 應用程式。
   
   > [!NOTE]
   > 模組在安裝期間，您可能會注意到錯誤的 ' hello 匯入的專案...找不到 '。 請放心忽略這項錯誤訊息。
   > 
   > 
6. Socket.IO 使用 WebSockets (在 Azure 上依預設不會啟用)。 tooenable web 通訊端，使用下列命令的 hello:
   
        azure site set -w
   
    如果出現提示，請輸入 hello hello web 應用程式名稱。
   
   > [!NOTE]
   > hello azure 站台設定-w 命令將會工作只會與版本 0.7.4 （含） 以上的 hello Azure 命令列介面。 您也可以啟用 WebSocket 支援使用 hello [Azure 入口網站](https://portal.azure.com)。
   > 
   > tooenable WebSockets 使用 hello Azure 入口網站，按一下 hello web 應用程式的 hello Web 應用程式 刀鋒視窗，按一下**所有設定** > **應用程式設定**。 在 [Web 通訊端] 下方，按一下 [開啟]。 然後按一下 [儲存] 。
   > 
   > 
7. 在 Azure，使用 hello 下列 tooview hello web 應用程式命令 toolaunch 網頁瀏覽器，然後瀏覽 toohello 裝載 web 應用程式：
   
        azure site browse

您的應用程式現在已在 Azure 上執行，而且可以使用 Socket.IO 在不同用戶端之間轉送聊天訊息。

## <a name="scale-out"></a>相應放大
Socket.IO 應用程式可以向外延展使用**配接器**toodistribute 訊息和多個應用程式執行個體之間的事件。 有數個配接器，hello [socket.io redis]配接器可以輕鬆地與 hello Azure Redis 快取功能搭配使用。

> [!NOTE]
> 橫向擴充 Socket.IO 解決方案的額外需求是支援黏性工作階段。 Azure Web Apps 的黏性工作階段預設是透過 Azure 要求路由來啟用。 如需詳細資訊，請參閱 [Azure 網站的執行個體同質性]。
> 
> 

### <a name="create-a-redis-cache"></a>建立 Redis 快取
執行中的 hello 步驟[在 Azure Redis 快取建立快取]toocreate 新的快取。

> [!NOTE]
> 儲存 hello**主機名稱**和**主索引鍵**快取，因為這些會需要 hello 接下來的步驟。
> 
> 

### <a name="add-hello-redis-and-socketio-redis-modules"></a>新增 hello redis 和 socket.io redis 模組
1. 從命令列，變更 toohello **\\節點\\聊天**目錄，並使用下列命令的 hello。
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > 此命令中指定的 hello 版本是使用測試本文時的 hello 版本。
   > 
   > 
2. 修改 hello **app.js**檔案 tooadd hello 下列各行後面`var io = require('socket.io')(server);`
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    取代**redishostname**和**rediskey** hello 主機名稱與您的 Redis 快取索引鍵。
   
    這會建立發佈和訂閱用戶端 toohello 先前建立的 Redis 快取。 hello 用戶端再搭配 hello 配接器 tooconfigure Socket.IO toouse hello Redis 快取的應用程式的執行個體之間傳遞訊息和事件
   
   > [!NOTE]
   > Hello 時**socket.io redis**配接器可以直接通訊 tooRedis、 hello 目前版本不支援 hello Azure Redis 快取所需的驗證。 因此會使用 hello 建立 hello 初始連接**redis**模組，然後 hello 用戶端會傳遞 toohello **socket.io redis**配接器。
   > 
   > 雖然 Azure Redis 快取支援使用連接埠 6380 的安全連線，使用在此範例中的 hello 模組不支援從 2014 年 7 月 14 日開始的安全連線。 hello，上述程式碼會使用 hello 預設為不安全的連接埠的 6379。
   > 
   > 
3. 修改儲存 hello **app.js**

### <a name="commit-changes-and-redeploy"></a>認可變更並重新部署
從命令列中 hello hello **\\節點\\聊天**目錄中，使用下列命令 toocommit 變更 hello 和重新部署 hello 應用程式。

    git add .
    git commit -m "implementing scale out"
    git push azure master

一旦已推入 hello 變更 toohello 伺服器，您可以跨多個執行個體調整您的網站，使用下列命令的 hello。

    azure site scale instances --instances #

其中 **#** 是 hello toocreate 執行個體數目。

您可以從多個訊息會正確傳送 tooall 用戶端瀏覽器或電腦 tooverify 連接 tooyour web 應用程式。

## <a name="troubleshooting"></a>疑難排解
### <a name="connection-limits"></a>連線限制
Azure Web 應用程式可在多個 Sku，判定 hello 資源可用 tooyour 站台。 這包括 hello 允許的 WebSocket 連線的數目。 如需詳細資訊，請參閱 hello [Web 應用程式定價頁面]。

### <a name="messages-arent-being-sent-using-websockets"></a>使用 WebSockets 而未傳送的訊息
如果用戶端瀏覽器保留回到 toolong 輪詢而不使用 WebSockets，它可能是因為 hello 下列其中一種。

* **請試著限制 hello 傳輸 toojust WebSockets**
  
    為了讓 Socket.IO toouse 為傳訊傳輸的 hello WebSockets，hello 伺服器和用戶端必須支援 WebSockets。 如果一或其他 hello 不存在，將會在 Socket.IO 交涉另一個傳輸，例如長輪詢。 hello Socket.IO 所使用的傳輸預設清單是` websocket, htmlfile, xhr-polling, jsonp-polling`。 您可以強制執行 tooonly 使用 WebSockets 加上下列程式碼 toohello hello **app.js**後 hello 行包含的檔案， `, nicknames = {};`。
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > 請注意，舊的瀏覽器不支援 WebSockets 不將能 tooconnect toohello 網站 hello 上述程式碼作用中時，因為它會限制只有通訊 tooWebSockets。
  > 
  > 
* **使用 SSL**
  
    WebSockets 依賴一些較小者使用 HTTP 標頭，例如 hello**升級**標頭。 某些中繼網路裝置，例如 Web Proxy，可能會移除這些標頭。 tooavoid 這個問題，您可以透過 SSL 來建立 hello WebSocket 連線。
  
    輕鬆 tooaccomplish 這太 tooconfigure Socket.IO`match origin protocol`。 這會指示 Socket.IO toosecure WebSockets 通訊 hello hello 網頁相同 hello 來自 HTTP/HTTPS 要求。 如果瀏覽器使用您的網站的 HTTPS URL toovisit，透過 Socket.IO 後續的 WebSocket 通訊將會透過 SSL 來保護。
  
    toomodify 此範例 tooenable 此組態中，加入下列程式碼 toohello hello **app.js**後 hello 列包含檔案`, nicknames = {};`。
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* **確認 web.config 設定**
  
    裝載 Node.js 應用程式的 azure web 應用程式使用 hello **web.config**檔案 tooroute 連入要求 toohello Node.js 應用程式。 WebSockets toofunction 正確使用 Node.js 應用程式，如 hello **web.config**必須包含下列項目 hello。
  
        <webSocket enabled="false"/>
  
    這會停用 hello IIS Websocket 模組包含它自己實作 WebSockets 以及衝突 Socket.IO 例如 Node.js 特定 WebSocket 模組。 如果這一行不存在，或設定得`true`，這可能是 hello 原因 hello WebSocket 傳輸未使用應用程式。
  
    通常 Node.js 應用程式並不包含 **web.config** 檔案，因此 Azure 網站會在部署 Node.js 應用程式時自動建立此一檔案。 由於這個檔案自動產生 hello 伺服器上，您必須使用 hello FTP 或 FTPS URL 的網站 tooview 這個檔案。 您可以尋找 hello FTP 和 FTPS Url 為您的網站 hello 傳統入口網站中選取您的 web 應用程式，並接著 hello**儀表板**連結。 hello Url 會顯示在 hello**快速概覽**> 一節。
  
  > [!NOTE]
  > hello **web.config**檔案才會產生 Azure 網站的應用程式不提供。 如果您提供**web.config**檔案 hello 在根目錄中的應用程式專案，它會使用由 Azure Web 應用程式。
  > 
  > 
  
    如果 hello 項目不存在，或設定 tooa 值`true`，那麼您應該建立**web.config**在 hello Node.js 應用程式的根目錄，並指定其值為`false`。  參考，hello 下列預設值是**web.config**應用程式使用**app.js**為 hello 進入點。
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used toorun node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that hello server.js file is a node.js web app toobe handled by hello iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether hello incoming URL matches a physical file in hello /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped toohello node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using hello following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes toorestart hello server
                * node_env: will be propagated toonode as NODE_ENV environment variable
                * debuggingEnabled - controls whether hello built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    如果您的應用程式中使用的進入點以外**app.js**，您必須取代所有出現之**app.js** hello 包含正確的進入點。 例如，將 **app.js** 取代為 **server.js**。

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務]，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 

## <a name="next-steps"></a>後續步驟
在本教學課程中，您學會如何 toocreate 交談應用程式裝載於 Azure web 應用程式。 您也可以將此應用程式交由 Azure 雲端服務託管。 如需有關如何步驟 tooaccomplish 這個，請參閱[Azure 雲端服務上建置含有 Socket.IO 的 Node.js 交談應用程式]。

如需詳細資訊，請參閱 hello [Node.js 開發人員中心]。

## <a name="whats-changed"></a>變更的項目
* 從網站 tooApp 服務變更如指南 toohello: [Azure App Service 與現有的 Azure 服務及其影響]。

<!-- URL List -->

[Azure Redis 快取]: /documentation/services/redis-cache/
[App Service Web 應用程式]: http://go.microsoft.com/fwlink/?LinkId=529714
[Web 應用程式定價頁面]: http://go.microsoft.com/fwlink/?LinkId=511643
[Azure 雲端服務上建置含有 Socket.IO 的 Node.js 交談應用程式]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure hello Azure CLI]: ../cli-install-nodejs.md
[Azure App Service 與現有的 Azure 服務及其影響]: http://go.microsoft.com/fwlink/?LinkId=529714
[Node.js 開發人員中心]: /develop/nodejs/
[再試一次應用程式服務]: https://azure.microsoft.com/try/app-service/
[Azure 網站的執行個體同質性]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[在 Azure Redis 快取建立快取]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[socket.io redis]: https://github.com/socketio/socket.io-redis
[Socket.IO GitHub 儲存機制]: https://github.com/socketio/socket.io
[ZIP 或 GZ 封存發行]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
