---
title: "指定 Node.js 版本"
description: "了解如何指定 Azure 網站和雲端服務所使用的 Node.js 版本"
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
ms.openlocfilehash: a20179c72b227deb14df442bea7b80cf31728aa7
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="specifying-a-nodejs-version-in-an-azure-application"></a>在 Azure 應用程式中指定 Node.js 版本
裝載 Node.js 應用程式時，您可能會想要確定應用程式是使用特定版本的 Node.js。 有數種方式可以為 Azure 上裝載的應用程式完成這項動作。

## <a name="default-versions"></a>預設版本
Azure 提供的 Node.js 版本會持續進行更新。 除非另有指定，否則將會使用 `WEBSITE_NODE_DEFAULT_VERSION` 環境變數中指定的預設版本。 若要覆寫此預設值，請依照本文下列各節中的步驟來進行

> [!NOTE]
> 如果您要將應用程式裝載在 Azure 雲端服務 (Web 或背景工作角色) 中，而且這是您第一次部署應用程式，只要您安裝在部署環境中的 Node.js 版本符合 Azure 上提供的其中一個預設版本，Azure 就會嘗試使用這個版本。
>
>

## <a name="versioning-with-packagejson"></a>以 package.json 進行版本設定
您可以在 **package.json** 檔案中新增下列內容，以指定要使用的 Node.js 版本。

    "engines":{"node":version}

其中 *version* 是要使用的特定版本號碼。 您可以針對 version 指定較複雜的條件，例如：

    "engines":{"node": "0.6.22 || 0.8.x"}

由於 0.6.22 不是主控環境中已提供的版本，因此將改用 0.8 系列可用的最高版本，也就是 0.8.4 版。

## <a name="versioning-websites-with-app-settings"></a>版本控制網站與應用程式設定
如果您在網站中裝載應用程式，您可以將環境變數 **WEBSITE_NODE_DEFAULT_VERSION** 設定為所需的版本。

## <a name="versioning-cloud-services-with-powershell"></a>以 PowerShell 進行雲端服務版本設定
如果您要將應用程式裝載在雲端服務中，而且要使用 Azure PowerShell 來部署應用程式，您可以使用 **Set-AzureServiceProjectRole** PowerShell Cmdlet 覆寫預設 Node.js 版本。 例如：

    Set-AzureServiceProjectRole WebRole1 Node 0.8.4

請注意上述陳述式的參數會區分大小寫。  您可以檢查角色 **package.json** 中的 **engines** 屬性，確認已選取正確的 Node.js 版本。

您也可以使用 **Get-AzureServiceProjectRoleRuntime** 擷取對於以雲端服務形式裝載的應用程式而言，可用的 Node.js 版本清單。  務必確認您專案所依據的 Node.js 版本列在此清單中。

## <a name="using-a-custom-version-with-azure-websites"></a>對 Azure 網站使用自訂版本
雖然 Azure 提供數個預設 Node.js 版本，不過您可能會想要使用預設未提供的版本。 如果您的應用程式是以 Azure 網站形式裝載，您可以使用 **iisnode.yml** 檔案達到該目的。 下列步驟將逐步引導您對 Azure 網站使用自訂版本的 Node.Js：

1. 建立新目錄，然後在目錄中建立 **server.js** 檔案。 **server.js** 檔案應該包含下列內容：

        var http = require('http');
        http.createServer(function(req,res) {
          res.writeHead(200, {'Content-Type': 'text/html'});
          res.end('Hello from Azure running node version: ' + process.version + '</br>');
        }).listen(process.env.PORT || 3000);

    這將顯示當您瀏覽網站時會使用的 Node.js 版本。
2. 建立新網站並記下網站的名稱。 例如，以下使用 [Azure 命令列工具] 建立新的 Azure 網站 (名稱為 **mywebsite**)，然後編輯該網站的 Git 存放庫。

        azure site create mywebsite --git
3. 建立名稱為 **bin** 的新目錄作為 **server.js** 檔案所在目錄的子目錄。
4. 下載要讓應用程式使用的特定 **node.exe** 版本 (Windows 版本)。 例如，以下使用 **curl** 下載 0.8.1 版。

        curl -O http://nodejs.org/dist/v0.8.1/node.exe

    將 **node.exe** 檔案儲存到先前建立的 **bin** 資料夾中。
5. 在 **server.js** 檔案所在的同一個目錄中建立 **iisnode.yml** 檔案，然後在 **iisnode.yml** 檔案中新增下列內容：

        nodeProcessCommandLine: "D:\home\site\wwwroot\bin\node.exe"

    您將應用程式發行到 Azure 網站後，您專案中的 **node.exe** 檔案將位在這個路徑中。
6. 發行您的應用程式。 例如，由於我稍早是使用 --git 參數建立新的網站，下列命令會將應用程式檔案新增到我的本機 Git 存放庫，然後將這些檔案推播到網站存放庫：

        git add .
        git commit -m "testing node v0.8.1"
        git push azure master

    發行應用程式後，使用瀏覽器開啟網站。 您應該會看見 "Hello from Azure running node version: v0.8.1" 訊息。

## <a name="next-steps"></a>後續步驟
您已了解如何指定應用程式使用的 Node.js 版本，現在請了解如何[使用模組]、[建置並部署 Node.js 網站](app-service/app-service-web-get-started-nodejs.md)和[如何使用適用於 Mac 和 Linux 的 Azure 命令列工具]。

如需詳細資訊，請參閱 [Node.js 開發人員中心](https://azure.microsoft.com/develop/nodejs/)。

[如何使用適用於 Mac 和 Linux 的 Azure 命令列工具]:cli-install-nodejs.md
[Azure 命令列工具]:cli-install-nodejs.md
[使用模組]: nodejs-use-node-modules-azure-apps.md
[build and deploy a Node.js Web Site]: app-service/app-service-web-get-started-nodejs.md
