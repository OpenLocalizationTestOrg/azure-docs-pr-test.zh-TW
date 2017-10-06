---
title: "aaaWeb 快速 (Node.js) 的應用程式 |Microsoft 文件"
description: "教學課程會建置 hello 雲端服務的教學課程，並示範如何 toouse hello Express 模組。"
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 24f8e7ef-e90d-4554-9b1e-a9b31d5824e5
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 91921bfbe137eeca9a110d4cb18eb57b46b0060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-web-application-using-express-on-an-azure-cloud-service"></a>在 Azure 雲端服務上使用 Express 建立 Node.js Web 應用程式
Node.js hello 核心執行階段中包含的最少的功能。
開發人員在開發 Node.js 應用程式時，通常會使用第 3 個合作對象模組 tooprovide 額外的功能。 在本教學課程中，您將建立新的應用程式使用 hello [Express] [ Express]模組，可讓 MVC 架構建立 Node.js web 應用程式。

底下是完成 hello 應用程式的螢幕擷取畫面：

![在 Azure 中顯示 歡迎使用 tooExpress 網頁瀏覽器](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="create-a-cloud-service-project"></a>建立雲端服務專案
[!INCLUDE [install-dev-tools](../../includes/install-dev-tools.md)]

執行 hello 下列步驟 toocreate 新的雲端服務專案名為 'expressapp':

1. 從 hello**開始功能表**或**[開始] 畫面**，搜尋**Windows PowerShell**。 最後，用滑鼠右鍵按一下 [Windows PowerShell]，然後選取 [以系統管理員身分執行]。
   
    ![Azure PowerShell icon](./media/cloud-services-nodejs-develop-deploy-express-app/azure-powershell-start.png)
2. 變更目錄 toohello **c:\\節點**目錄，然後輸入下列命令 toocreate 名為新方案的 hello **expressapp**和名為 web 角色**WebRole1**:
   
        PS C:\node> New-AzureServiceProject expressapp
        PS C:\Node\expressapp> Add-AzureNodeWebRole
        PS C:\Node\expressapp> Set-AzureServiceProjectRole WebRole1 Node 0.10.21
   
    > [!NOTE]
    > **Add-AzureNodeWebRole** 預設會使用較舊版的 Node.js。 hello**組 AzureServiceProjectRole**上述陳述式會指示 Azure toouse v0.10.21 的節點。  請注意 hello 參數會區分大小寫。  您可以確認已選取 hello 正確版本的 Node.js 藉由檢查 hello**引擎**屬性**WebRole1\package.json**。
    > 
    > 

## <a name="install-express"></a>安裝 Express
1. 藉由發出下列命令的 hello 安裝 hello Express 產生器：
   
        PS C:\node\expressapp> npm install express-generator -g
   
    hello hello npm 命令輸出應該看起來類似下列的 toohello 結果。 
   
    ![Windows PowerShell 顯示 hello 輸出的 hello npm 安裝 express 命令。](./media/cloud-services-nodejs-develop-deploy-express-app/express-g.png)
2. 變更目錄 toohello **WebRole1**目錄並用 hello express 命令 toogenerate 新的應用程式：
   
        PS C:\node\expressapp\WebRole1> express
   
    您將會提示的 toooverwrite 早的應用程式。 輸入**y**或**是**toocontinue。 Express 將會產生 hello app.js 檔案和建置您的應用程式的資料夾結構。
   
    ![hello hello express 命令輸出](./media/cloud-services-nodejs-develop-deploy-express-app/node23.png)
3. tooinstall hello package.json 檔中定義的其他相依性輸入 hello 下列命令：
   
       PS C:\node\expressapp\WebRole1> npm install
   
   ![hello 輸出的 hello npm 安裝命令](./media/cloud-services-nodejs-develop-deploy-express-app/node26.png)
4. 使用 hello 下列命令 toocopy hello **bin w**檔案太**立即轉譯 server.js**。 這是讓 hello 雲端服務可以找到 hello 進入點為此應用程式。
   
       PS C:\node\expressapp\WebRole1> copy bin/www server.js
   
   此命令完成之後，您應該有**立即轉譯 server.js** hello WebRole1 目錄中的檔案。
5. 修改 hello**立即轉譯 server.js** tooremove hello 的其中一個 '。 ' hello 以下的字元。
   
       var app = require('../app');
   
   進行這項修改後, hello 行應該顯示如下。
   
       var app = require('./app');
   
   這項變更是必要的因為我們將 hello 檔案移 (先前稱為**bin w**，) toohello hello 應用程式檔案需要同一個目錄。 變更之後，儲存 hello**立即轉譯 server.js**檔案。
6. 使用下列命令 toorun hello 應用程式在 hello Azure 模擬器中的 hello:
   
       PS C:\node\expressapp\WebRole1> Start-AzureEmulator -launch
   
    ![包含  褖畫惎 tooexpress 的網頁。](./media/cloud-services-nodejs-develop-deploy-express-app/node28.png)

## <a name="modifying-hello-view"></a>修改 hello 檢視
現在修改 hello 檢視 toodisplay hello 訊息 「 在 Azure 中的 歡迎使用 tooExpress"。

1. 輸入下列命令 tooopen hello index.jade 檔 hello:
   
       PS C:\node\expressapp\WebRole1> notepad views/index.jade
   
   ![hello hello index.jade 檔案內容。](./media/cloud-services-nodejs-develop-deploy-express-app/getting-started-19.png)
   
   Jade 是 hello Express 應用程式所使用的預設檢視引擎。 如需有關 hello Jade 檢視引擎的詳細資訊，請參閱[http://jade-lang.com][http://jade-lang.com]。
2. 修改 hello 最後一行的文字，藉由附加**在 Azure 中**。
   
   ![hello index.jade 檔案，hello 最後一行讀取： p 太歡迎\#{t} 在 Azure 中](./media/cloud-services-nodejs-develop-deploy-express-app/node31.png)
3. 儲存 hello 檔案並結束 [記事本]。
4. 重新整理瀏覽器，您將會看到變更。
   
   ![瀏覽器視窗中，hello 頁面包含在 Azure 中的 歡迎使用 tooExpress](./media/cloud-services-nodejs-develop-deploy-express-app/node32.png)

測試的 hello 應用程式後使用 hello**停止 AzureEmulator** cmdlet toostop hello 模擬器。

## <a name="publishing-hello-application-tooazure"></a>發行 hello 應用程式 tooAzure
在 hello Azure PowerShell 視窗中，使用 hello**發行 AzureServiceProject** cmdlet toodeploy hello 應用程式 tooa 雲端服務

    PS C:\node\expressapp\WebRole1> Publish-AzureServiceProject -ServiceName myexpressapp -Location "East US" -Launch

Hello 部署作業完成之後，您的瀏覽器會開啟並顯示 hello 的網頁。

![網頁瀏覽器顯示 hello Express 頁面。 hello URL 表示它現在裝載於 Azure。](./media/cloud-services-nodejs-develop-deploy-express-app/node36.png)

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱 hello [Node.js 開發人員中心](/develop/nodejs/)。

[Node.js Web Application]: http://www.windowsazure.com/develop/nodejs/tutorials/getting-started/
[Express]: http://expressjs.com/
[http://jade-lang.com]: http://jade-lang.com


