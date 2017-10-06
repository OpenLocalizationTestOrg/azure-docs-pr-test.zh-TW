---
title: "使用 Socket.io aaaNode.js 應用程式 |Microsoft 文件"
description: "了解 toouse socket.io node.js 應用程式中的裝載在 Azure 上的方式。"
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 7f9435e0-7732-4aa1-a4df-ea0e894b847f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 47c6c4a748938959315b880340f41f31faab4ea9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-chat-application-with-socketio-on-an-azure-cloud-service"></a>在 Azure 雲端服務上使用 Socket.IO 建立 Node.js 交談應用程式
Socket.IO 提供 node.js 伺服器和用戶端之間的即時通訊。 本教學課程引導您將 socket.IO 型交談應用程式裝載於 Azure 上。 如需 Socket.IO 的詳細資訊，請參閱 <http://socket.io/>。

底下是完成 hello 應用程式的螢幕擷取畫面：

![瀏覽器視窗，以顯示裝載於 Azure 的 hello 服務][completed-app]  

## <a name="prerequisites"></a>必要條件
確定該 hello 下列產品和版本會在本文中的已安裝的 toosuccessfully 完成 hello 範例：

* 安裝 [Visual Studio](https://www.visualstudio.com/en-us/downloads/download-visual-studio-vs.aspx)
* 安裝 [Node.js](https://nodejs.org/download/)
* 安裝 [Python 版本 2.7.10](https://www.python.org/)

## <a name="create-a-cloud-service-project"></a>建立雲端服務專案
hello 下列步驟建立 hello 雲端服務專案將裝載 hello Socket.IO 應用程式。

1. 從 hello**開始功能表**或**[開始] 畫面**，搜尋**Windows PowerShell**。 最後，用滑鼠右鍵按一下 [Windows PowerShell]，然後選取 [以系統管理員身分執行]。
   
    ![Azure PowerShell icon][powershell-menu]
2. 建立名為 **c:\\node** 的目錄。 
   
        PS C:\> md node
3. 變更目錄 toohello **c:\\節點**目錄
   
        PS C:\> cd node
4. 輸入下列命令 toocreate 名為新方案的 hello **chatapp**和名為的背景工作角色**WorkerRole1**:
   
        PS C:\node> New-AzureServiceProject chatapp
        PS C:\Node> Add-AzureNodeWorkerRole
   
    您會看到下列回應 hello:
   
    ![hello 的輸出 hello 新 azureservice 和新增 azurenodeworkerrolecmdlets](./media/cloud-services-nodejs-chat-app-socketio/socketio-1.png)

## <a name="download-hello-chat-example"></a>下載 hello 聊天範例
此專案中，我們將使用從 hello hello 聊天範例[Socket.IO GitHub 儲存機制]。 執行下列步驟 toodownload hello 範例 hello，並將它加入您先前建立的 toohello 專案。

1. 建立 hello 儲存機制的本機副本使用 hello**複製** 按鈕。 您也可以使用 hello **ZIP**按鈕 toodownload hello 專案。
   
   ![反白顯示 hello ZIP 下載圖示以檢視 https://github.com/LearnBoost/socket.io/tree/master/examples/chat，在瀏覽器視窗][chat-example-view]
2. 瀏覽 hello hello 本機儲存機制的目錄結構，直到您到達 hello**範例\\聊天**目錄。 將這個目錄 toothe hello 內容複製**c:\\節點\\chatapp\\WorkerRole1**稍早建立的目錄。
   
   ![總管 中，顯示 hello 範例 hello 內容\\從 hello 封存解壓縮的聊天目錄][chat-contents]
   
   hello hello 上方螢幕擷取畫面中反白顯示的項目會從 hello 複製的 hello 檔案**範例\\聊天**目錄
3. 在 hello **c:\\節點\\chatapp\\WorkerRole1**目錄中，刪除 hello**立即轉譯 server.js**檔案，然後再重新命名 hello **app.js**檔案太**立即轉譯 server.js**。 這會移除 hello 預設**立即轉譯 server.js**先前由 hello**新增 AzureNodeWorkerRole**指令程式，並從它與 hello 應用程式檔案的取代 hello 聊天範例。

### <a name="modify-serverjs-and-install-modules"></a>修改 Server.js 和安裝模組
測試 hello 應用之前 hello Azure 模擬器中，我們必須進行一些次要的修改。 執行下列步驟 toothe 立即轉譯 server.js 檔 hello:

1. 開啟 hello**立即轉譯 server.js** Visual Studio 或任何文字編輯器中的檔案。
2. 尋找 hello**模組相依性**區段開頭 hello 立即轉譯 server.js 和變更 hello 列包含**sio = require('..//..lib//socket.io')**太**sio = require('socket.io')**如下所示：
   
       var express = require('express')
         , stylus = require('stylus')
         , nib = require('nib')
       //, sio = require('..//..//lib//socket.io'); //Original
         , sio = require('socket.io');                //Updated
         var port = process.env.PORT || 3000;         //Updated
3. hello 正確的通訊埠上接聽的 tooensure hello 應用程式、 開啟立即轉譯 server.js [記事本] 或您偏好的編輯器，然後變更下列行取代**3000**與**process.env.port**所示如下：
   
       //app.listen(3000, function () {            //Original
       app.listen(process.env.port, function () {  //Updated
         var addr = app.address();
         console.log('   app listening on http://' + addr.address + ':' + addr.port);
       });

儲存 hello 變更太之後**立即轉譯 server.js**使用 hello 下列步驟來安裝所需的模組，然後在 Azure 模擬器中測試 hello 應用程式：

1. 使用**Azure PowerShell**，變更目錄 toohello **c:\\節點\\chatapp\\WorkerRole1**目錄，並使用下列命令 tooinstall hello 的 hello此應用程式所需的模組：
   
       PS C:\node\chatapp\WorkerRole1> npm install
   
   這會安裝在 hello package.json 檔案中列出的 hello 模組。 Hello 命令完成之後，您應該會看到類似 toothe 下列輸出：
   
   ![hello 輸出的 hello npm 安裝命令][The-output-of-the-npm-install-command]
2. 由於本範例原本 hello Socket.IO GitHub 儲存機制的一部分，而且直接由相對路徑參考 hello Socket.IO 程式庫，Socket.IO 中都未參考 hello package.json 檔案，所以我們必須安裝它，藉由發出下列命令的 hello:
   
       PS C:\node\chatapp\WorkerRole1> npm install socket.io --save

### <a name="test-and-deploy"></a>測試和部署
1. 藉由發出下列命令的 hello 啟動 hello 模擬器：
   
       PS C:\node\chatapp\WorkerRole1> Start-AzureEmulator -Launch
   
   > [!NOTE]
   > 如果您在啟動模擬器時遇到問題，例如：Start-AzureEmulator：發生未預期的失敗。  詳細資料： 發生未預期的錯誤 hello 通訊物件 System.ServiceModel.Channels.ServiceChannel 無法用於通訊，因為它處於 Faulted 狀態 hello。
   
      重新安裝 AzureAuthoringTools v 2.7.1 和 AzureComputeEmulator v 2.7 - 請確定版本相符。
   >
   >


2. 開啟瀏覽器並瀏覽過**http://127.0.0.1**。
3. 當 hello 瀏覽器視窗開啟時，輸入別名，然後按 enter 鍵。
   這可讓您 toopost 訊息做為特定的暱稱。 tootest 多使用者功能，開啟其他瀏覽器視窗使用相同的 URL，並輸入不同的暱稱。
   
   ![兩個瀏覽器視窗顯示 User1 和 User2 的交談訊息](./media/cloud-services-nodejs-chat-app-socketio/socketio-8.png)
4. 測試的 hello 應用程式後停止模擬器 hello 發出下列命令：
   
       PS C:\node\chatapp\WorkerRole1> Stop-AzureEmulator
5. toodeploy hello 應用程式 tooAzure，使用**發行 AzureServiceProject** cmdlet。 例如：
   
       PS C:\node\chatapp\WorkerRole1> Publish-AzureServiceProject -ServiceName mychatapp -Location "East US" -Launch
   
   > [!IMPORTANT]
   > 要確定 toouse 唯一的名稱，否則 hello 發佈程序將會失敗。 Hello 部署完成後，hello 瀏覽器會開啟，並瀏覽 toohello 部署服務。
   > 
   > 如果您收到錯誤，表示該 hello 提供訂用帳戶名稱不存在於 hello 匯入發行設定檔，您必須下載並匯入您的訂用帳戶，然後再部署 tooAzure hello 發行設定檔。 請參閱 hello**部署 hello 應用程式 tooAzure**區段[建置和部署 Node.js 應用程式 tooan Azure 雲端服務](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)
   > 
   > 
   
   ![瀏覽器視窗，以顯示裝載於 Azure 的 hello 服務][completed-app]
   
   > [!NOTE]
   > 如果您收到錯誤，表示該 hello 提供訂用帳戶名稱不存在於 hello 匯入發行設定檔，您必須下載並匯入您的訂用帳戶，然後再部署 tooAzure hello 發行設定檔。 請參閱 hello**部署 hello 應用程式 tooAzure**區段[建置和部署 Node.js 應用程式 tooan Azure 雲端服務](https://azure.microsoft.com/develop/nodejs/tutorials/getting-started/)
   > 
   > 

應用程式現在已在 Azure 上執行，且可以使用 Socket.IO 在不同用戶端之間轉送聊天訊息。

> [!NOTE]
> 為了簡單起見，此範例是有限的使用者連接 toohello 之間 toochatting 相同的執行個體。 這表示，如果 hello 雲端服務會建立兩個背景工作角色執行個體，使用者將只能與其他人 toochat 連接 toohello 相同的背景工作角色執行個體。 tooscale hello 與多個角色執行個體的應用程式 toowork，您可以使用一種技術類似 Service Bus tooshare hello Socket.IO 存放區狀態跨執行個體。 如需範例，請參閱 < 在 hello hello Service Bus 佇列和主題使用範例[Azure SDK for Node.js GitHub 儲存機制](https://github.com/WindowsAzure/azure-sdk-for-node)。
> 
> 

## <a name="next-steps"></a>後續步驟
在本教學課程中，您學會如何 toocreate 基本交談應用程式裝載於 Azure 雲端服務。 toolearn 如何 toohost 此應用程式在 Azure 網站，請參閱[Node.js 聊天的建置應用程式 Socket.IO Azure 網站上][chatwebsite]。

如需詳細資訊，請參閱 hello [Node.js 開發人員中心](/develop/nodejs/)。

[chatwebsite]: /develop/nodejs/tutorials/website-using-socketio/

[Azure SLA]: http://www.windowsazure.com/support/sla/
[Azure SDK for Node.js GitHub repository]: https://github.com/WindowsAzure/azure-sdk-for-node
[completed-app]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-10.png
[Azure SDK for Node.js]: https://www.windowsazure.com/develop/nodejs/
[Node.js Web Application]: https://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Socket.IO GitHub 儲存機制]: https://github.com/LearnBoost/socket.io/tree/0.9.14
[Azure Considerations]: #windowsazureconsiderations
[Hosting hello Chat Example in a Worker Role]: #hostingthechatexampleinawebrole
[Summary and Next Steps]: #summary
[powershell-menu]: ./media/cloud-services-nodejs-chat-app-socketio/azure-powershell-start.png

[chat example]: https://github.com/LearnBoost/socket.io/tree/master/examples/chat
[chat-example-view]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-22.png


[chat-contents]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-5.png
[The-output-of-the-npm-install-command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-7.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-chat-app-socketio/socketio-9.png


