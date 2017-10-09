---
title: "在本機的 Docker 容器中的 aaaDebugging 應用程式 |Microsoft 文件"
description: "了解 toomodify 在本機的 Docker 容器中，執行的應用程式重新整理 hello 容器透過編輯和重新整理，並設定偵錯中斷點"
services: azure-container-service
documentationcenter: na
author: mlearned
manager: douge
editor: 
ms.assetid: 480e3062-aae7-48ef-9701-e4f9ea041382
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 07/22/2016
ms.author: mlearned
ms.openlocfilehash: ff64e62fbb93901a29b5496bd5e17d2c4ea5ca99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debugging-apps-in-a-local-docker-container"></a>偵錯本機 Docker 容器中的應用程式
## <a name="overview"></a>概觀
hello Visual Studio Tools for Docker 會提供一致的方式 toodevelop 中，並驗證 Linux Docker 容器中的本機應用程式。
您不需要每次您做變更的程式碼 toorestart hello 容器。
本文說明如何 toouse hello [編輯和重新整理] 功能 toostart ASP.NET Core Web 應用程式在本機的 Docker 容器中，進行任何必要的變更，並再重新整理 hello 瀏覽器 toosee 這些變更。
本文也將示範如何偵錯 tooset 中斷點。

> [!NOTE]
> 未來版本將支援 Windows 容器
>
>

## <a name="prerequisites"></a>必要條件
您必須安裝下列工具 hello。

* [最新版本的 Visual Studio](https://www.visualstudio.com/downloads/)
* [Microsoft ASP.NET 核心 1.0 SDK](https://go.microsoft.com/fwlink/?LinkID=809122)

toorun Docker 容器在本機上，您將需要本機 docker 用戶端。
您可以使用 hello [Docker 工具箱](https://www.docker.com/products/docker-toolbox)，需要 HYPER-V toobe 停用，或者您可以使用[Docker for Windows](https://www.docker.com/get-docker)，此方法使用 HYPER-V，並且需要 Windows 10。

如果使用 Docker 工具箱，您將需要太[hello Docker 用戶端設定](vs-azure-tools-docker-setup.md)

## <a name="1-create-a-web-app"></a>1.建立 Web 應用程式
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a>2.新增 Docker 支援
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a>3.編輯您的程式碼並重新整理
tooquickly 逐一查看變更，您可以啟動應用程式內的容器，並繼續 toomake 變更檢視它們，如同使用 IIS Express。

1. 設定得 hello 方案組態`Debug`按 **&lt;CTRL + F5 >** toobuild 您的 docker 映像，在本機執行。

    一旦 hello 容器映像已建置並執行 Docker 容器中，Visual Studio 會啟動預設瀏覽器中的 hello Web 應用程式。
    如果您使用 hello Microsoft Edge 瀏覽器或否則有錯誤，請參閱[疑難排解](vs-azure-tools-docker-troubleshooting-docker-errors.md)> 一節。
2. 移 toohello 有關頁面上，也就是我們會查 toomake 我們變更。
3. 傳回 tooVisual Studio，並開啟`Views\Home\About.cshtml`。
4. 新增 hello 遵循 hello 檔案的 HTML 內容 toohello 結尾，並儲存 hello 變更。

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. 完成 hello.NET 建置，而且您會看到這些線條，請檢視 hello 輸出 視窗中，切換後 tooyour 瀏覽器，並重新整理頁面相關的 hello。

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C tooshut down
   ```
6. 您的變更已經套用！

## <a name="4-debug-with-breakpoints"></a>4.使用中斷點進行偵錯
通常，變更將會需要進一步檢查，利用 hello 偵錯 Visual Studio 的功能。

1. 傳回 tooVisual Studio，並開啟`Controllers\HomeController.cs`
2. 取代 hello 下列 hello hello about 方法內容：

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. 設定中斷點 toohello 方 hello `string message`...列。
4. 叫用 **&lt;F5 >** toostart 偵錯。
5. 有關頁面 toohit toohello 瀏覽您的中斷點。
6. 切換 tooVisual Studio tooview hello 中斷點，並檢查 hello 訊息值。

   ![][2]

## <a name="summary"></a>摘要
與[Visual Studio 2015 Tools for Docker](https://aka.ms/DockerToolsForVS)，就可以使用在本機開發 Docker 容器中的 hello 生產真實性的 hello 產能。

## <a name="troubleshooting"></a>疑難排解
[疑難排解 Visual Studio Docker 開發](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a>進一步了解 Docker 與 Visual Studio、Windows 和 Azure
* [Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) - 在容器中開發 .NET Core 程式碼
* [Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) - 建置和部署 Docker 容器
* [Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) - 用於編輯 Docker 檔案的語言服務，將推出更多其他 e2e 案例
* [Windows 容器資訊](http://aka.ms/containers)- Windows Server 和 Nano Server 資訊
* [Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Azure Container Service 內容](http://aka.ms/AzureContainerService)
* 如需使用 Docker 的範例，請參閱[使用 Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker)從 hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015年連接[示範](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/)。 如需從 hello HealthClinic.biz 示範的快速入門，請參閱[Azure 開發人員工具快速入門](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts)。

## <a name="various-docker-tools"></a>各種 Docker 工具
[一些不錯的 Docker 工具 (Steve Lasker 的部落格)](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a>不錯的文章
[從 NGINX 簡介 tooMicroservices](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a>簡報
* [Steve Lasker：VS Live Las Vegas 2016 - Docker e2e](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [@ 組建 2016-其中您在示範簡介 tooASP.NET 核心](https://channel9.msdn.com/Events/Build/2016/B810)
* [開發容器中的 .NET 應用程式 (Channel 9)](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
