---
title: "aaaSpecifying Node.js 版本"
description: "了解如何 toospecify hello Node.js 的 Azure 網站和雲端服務所使用的版本"
services: 
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d0e15278-2ab4-4ec8-8256-913839c6d5ef
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 09c27bfc43c132b6d66f9a2943179e06ee75bedc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a>在 Azure 應用程式中指定 Node.js 版本
當裝載 Node.js 應用程式，您可能想 tooensure 應用程式使用特定版本的 Node.js。 有數種方式 tooaccomplish 這在 Azure 上裝載的應用程式。

## <a name="default-versions"></a>預設版本
Azure 提供的 hello Node.js 版本會經常更新。 除非另行指定，hello hello 中所指定的預設版本`WEBSITE_NODE_DEFAULT_VERSION`將使用環境變數。 toooverride 此預設值，遵循本文章的下列各節中的 hello 步驟

> [!NOTE]
> 如果您要裝載您的應用程式在 Azure 雲端服務 （web 或背景工作角色） 為 hello hello 應用程式部署的第一次，Azure 會嘗試 toouse hello 相同版本的 Node.js，因為您已安裝在開發環境上如果它比對其中一個在 Azure 上可用的 hello 預設版本。
>
>

## <a name="versioning-with-packagejson"></a>以 package.json 進行版本設定
您可以指定使用新增下列 tooyour hello Node.js toobe hello 版本**package.json**檔案：

    "engines":{"node":version}

其中*版本*是 hello 特定版本號碼 toouse。 您可以針對 version 指定較複雜的條件，例如：

    "engines":{"node": "0.6.22 || 0.8.x"}

因為 0.6.22 不是其中一個用於裝載環境的 hello hello 版本，hello 最新軟體版本的 hello 0.8 是可用的數列將會改用-0.8.4。

## <a name="versioning-websites-with-app-settings"></a>版本控制網站與應用程式設定
如果您裝載在網站中的 hello 應用程式，您可以設定 hello 環境變數**WEBSITE_NODE_DEFAULT_VERSION** toohello 所需的版本。

## <a name="versioning-cloud-services-with-powershell"></a>以 PowerShell 進行雲端服務版本設定
如果您正在裝載在雲端服務中，hello 應用程式，而且部署 hello 應用程式使用 Azure PowerShell，您可以使用覆寫 hello 預設 Node.js 版本 hello**組 AzureServiceProjectRole** PowerShell cmdlet。 例如：

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

請注意 hello 上述陳述式中的 hello 參數會區分大小寫。  您可以確認已選取 hello 正確版本的 Node.js 藉由檢查 hello**引擎**中角色的屬性**package.json**。

您也可以使用 hello **Get AzureServiceProjectRoleRuntime** tooretrieve Node.js 版本適用於裝載的雲端服務的應用程式的清單。  一定要驗證 hello Node.js 取決於您的專案版本在此清單中。

## <a name="using-a-custom-version-with-azure-websites"></a>對 Azure 網站使用自訂版本
雖然 Azure 提供的 Node.js 的數個預設版本，您可能想 toouse 並非預設提供的版本。 如果您的應用程式裝載為 Azure 網站中，您可以完成這項作業使用 hello **iisnode.yml**檔案。 hello 下列步驟逐步解說使用自訂版本 Node.Js 的 Azure 網站中的 hello 程序：

1. 建立新的目錄，然後再建立**立即轉譯 server.js** hello 目錄內的檔案。 hello**立即轉譯 server.js**檔案應包含 hello 下列：

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    這會顯示當您瀏覽 hello 網站所使用的 hello Node.js 版本。
2. 建立新的網站和附註 hello hello 站台名稱。 例如，hello 下列方式使用 hello [Azure 命令列工具]toocreate 名為新的 Azure 網站**mywebsite**，然後再啟用 hello 網站的 Git 儲存機制。

        azure site create mywebsite --git
3. 建立新的目錄名稱為**bin**做為子系包含 hello hello 目錄**立即轉譯 server.js**檔案。
4. 下載 hello 特定版本**node.exe** （hello Windows 版本），您會希望 toouse 與您的應用程式。 例如，下列使用 hello **curl** toodownload 版本 0.8.1:

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    儲存 hello **node.exe**檔案 hello **bin**先前建立的資料夾。
5. 建立**iisnode.yml**相同檔案中 hello 目錄為 hello**立即轉譯 server.js**檔案，然後再加入下列內容 toohello hello **iisnode.yml**檔案：

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    這個路徑是在 hello **node.exe**一旦發行您的應用程式 toohello Azure 網站中您的專案檔案會位於位置。
6. 發行您的應用程式。 比方說，因為我建立新的網站與 hello-git 參數之前，hello 下列命令會新增 hello 應用程式檔案 toomy 本機 Git 儲存機制，並再將其推送 toohello 網站儲存機制：

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    Hello 應用程式具有發行之後，請在瀏覽器中開啟 hello 網站。 您應該會看見 "Hello from Azure running node version: v0.8.1" 訊息。

## <a name="next-steps"></a>後續步驟
既然您了解 toospecify hello 版本的 Node.js 應用程式所使用的方式，了解如何太[模組使用]，[建置和部署 Node.js 的網站](app-service-web/app-service-web-get-started-nodejs.md)，和[toouse hello Azure 的方式適用於 Mac 和 Linux 的命令列工具]。

如需詳細資訊，請參閱 hello [Node.js 開發人員中心](https://azure.microsoft.com/develop/nodejs/)。

[toouse hello Azure 的方式適用於 Mac 和 Linux 的命令列工具]:cli-install-nodejs.md
[Azure 命令列工具]:cli-install-nodejs.md
[模組使用]: nodejs-use-node-modules-azure-apps.md
[build and deploy a Node.js Web Site]: app-service-web/app-service-web-get-started-nodejs.md
