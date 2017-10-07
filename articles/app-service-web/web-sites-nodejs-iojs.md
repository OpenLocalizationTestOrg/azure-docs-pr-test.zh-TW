---
title: "aaaHow toouse io.js 與 Azure App Service Web 應用程式"
description: "深入了解如何 toouse io.js 具有 Azure App Service 中的 web 應用程式。"
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: d6320725-ffcb-4ad7-ba63-fc72fa2f2808
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 5dfdac37546b36bc91ab43d9e0a39c2126b4fa9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-iojs-with-azure-app-service-web-apps"></a>如何使用 Azure App Service Web 應用程式的 toouse io.js
hello 熱門節點分岔[io.js]各種差異 tooJoyent 的 Node.js 專案，包括多開啟的控管模型、 更快的發行週期和新功能和實驗 JavaScript 功能更快速採用的功能。

雖然 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps 有許多預先安裝的 Node.js 版本，但它也允許使用者提供的 Node.js 二進位檔。 本文將討論兩個方法可讓 hello io.js App Service Web 應用程式上使用： hello 使用擴充的部署指令碼，它會自動設定 Azure toouse hello 最新可用 io.js 版本，以及 hello io.js 二進位檔手動上的傳。 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a>使用部署指令碼
部署時的 Node.js 應用程式，App Service Web 應用程式執行小型 hello 環境的 tooensure 已正確設定的命令的數目。 使用部署指令碼，此程序可以是自訂的 tooinclude hello 下載和 io.js 的組態。

hello [io.js 部署指令碼](https://github.com/felixrieseberg/iojs-azure)可在 GitHub 上取得。 web 應用程式上的 tooenable io.js 直接複製**.deployment**， **deploy.cmd**和**IISNode.yml** toohello 根應用程式資料夾的 tooWeb 應用程式並部署。  

hello 第一個檔案， **.deployment**，指示 Web 應用程式 toorun **deploy.cmd**一旦部署之後。 此指令碼執行 Node.js 應用程式的 hello 一般步驟，但也會下載 io.js hello 最新版本。 最後， **IISNode.yml**設定 Web 應用程式 toouse 只是下載的 hello io.js 二進位而不是預先安裝 Node.js 二進位檔。

> [!NOTE]
> tooupdate hello 用於 io.js 二進位檔，只要重新部署應用程式-hello 指令碼會下載新版本的 io.js 每一次 hello 應用程式部署。
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a>使用手動安裝
hello 手動安裝的自訂 io.js 版本包括只有兩個步驟。 首先，下載 hello **win x64**二進位直接從 hello [io.js 發佈]。 需要兩個檔案 - **iojs.exe** 和 **iojs.lib**。 儲存這兩個檔案，tooa 內您 web 應用程式，例如在**bin/iojs**。

tooconfigure Web 應用程式 toouse **iojs.exe**預先安裝的節點版本，您不必建立**IISNode.yml** hello 根應用程式的檔案，然後加入下列行 hello。

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a>後續步驟
在這篇文章您學會如何使用 App Service Web 應用程式，使用這兩個 toouse io.js 提供部署指令碼，以及在手動安裝。 

> [!NOTE]
> io.js 正在密集的開發中，而且比 Node.js 更頻繁地更新。 許多 Node.js 模組可能不適用於 io.js，請參閱 [GitHub 上的 io.js] 以進行疑難排解。
> 
> 

## <a name="whats-changed"></a>變更的項目
* 從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 

[io.js]: https://iojs.org
[io.js 發佈]: https://iojs.org/dist/
[GitHub 上的 io.js]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
