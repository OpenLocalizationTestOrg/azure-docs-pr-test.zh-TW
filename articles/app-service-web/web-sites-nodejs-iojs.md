---
title: "如何搭配使用 io.js 和 Azure App Service Web Apps"
description: "了解如何搭配使用 Azure App Service 中的 Web 應用程式和 io.js。"
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
ms.openlocfilehash: 4800504e1939a46842d15e8c9d4279a4b9cae787
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-iojs-with-azure-app-service-web-apps"></a>如何搭配使用 io.js 和 Azure App Service Web Apps
受歡迎的 Node 會將 [io.js] 功能的各種差異分散至 Joyent 的 Node.js 專案，包括更開放的控管模型、更快速的發行週期，以及更快速地採用全新和實驗性的 JavaScript 功能。

雖然 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps 有許多預先安裝的 Node.js 版本，但它也允許使用者提供的 Node.js 二進位檔。 本文討論兩種方法可用來啟用 App Service Web Apps 上的 io.js：使用擴充的部署指令碼(其會自動設定 Azure 來使用最新的可用 io.js 版本)，以及手動上傳 io.js 二進位檔。 

<a id="deploymentscript"></a>

## <a name="using-a-deployment-script"></a>使用部署指令碼
部署 Node.js 應用程式時，App Service Web Apps 會執行一些小型命令，以確保會正確設定環境。 使用部署指令碼，可自訂此程序來加入 io.js 的下載和組態。

[Io.js 部署指令碼](https://github.com/felixrieseberg/iojs-azure) 可在 GitHub 上取得。 若要在 Web 應用程式上啟用 io.js，只要將**.deployment**、**deploy.cmd** 和 **IISNode.yml** 複製到應用程式資料夾的根目錄，以及部署至 Web Apps。  

第一個檔案 **.deployment** 會在部署時指示 Web Apps 執行 **deploy.cmd**。 此指令碼會針對 Node.js 應用程式執行所有一般步驟，但也會下載最新版的 io.js。 最後， **IISNode.yml** 會設定 Web Apps 使用剛才下載的 io.js 二進位檔，而不是預先安裝的 Node.js 二進位檔。

> [!NOTE]
> 若要更新使用的 io.js 二進位檔，只要重新部署應用程式即可；每次部署應用程式時，指令碼都會下載新版 io.js。
> 
> 

<a id="manualinstallation"></a>

## <a name="using-manual-installation"></a>使用手動安裝
手動安裝的自訂 io.js 版本只包括兩個步驟。 首先，直接從 **io.js 散發** 下載 [win-x64]二進位檔。 需要兩個檔案 - **iojs.exe** 和 **iojs.lib**。 將這兩個檔案儲存至 Web 應用程式內的資料夾，例如儲存在 **bin/iojs**。

若要設定 Web Apps 使用 **iojs.exe**，而不是預先安裝的 Node 版本，請在應用程式的根目錄建立 **IISNode.yml** 檔案並加入下一行。

    nodeProcessCommandLine: "D:\home\site\wwwroot\bin\iojs\iojs.exe"

<a id="nextsteps"></a>

## <a name="next-steps"></a>後續步驟
在本文中，您學到如何搭配使用 io.js 與 App Service Web Apps、使用這兩個提供的部署指令碼，以及手動安裝。 

> [!NOTE]
> io.js 正在密集的開發中，而且比 Node.js 更頻繁地更新。 許多 Node.js 模組可能不適用於 io.js，請參閱 [GitHub 上的 io.js] 以進行疑難排解。
> 
> 

## <a name="whats-changed"></a>變更的項目
* 如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)

> [!NOTE]
> 如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。 不需要信用卡；無需承諾。
> 
> 

[io.js]: https://iojs.org
[win-x64]: https://iojs.org/dist/
[GitHub 上的 io.js]: https://github.com/iojs/io.js
[io.js Deployment Script]: https://github.com/felixrieseberg/iojs-azure
