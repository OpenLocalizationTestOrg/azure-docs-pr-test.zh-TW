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
# <a name="debugging-apps-in-a-local-docker-container"></a><span data-ttu-id="855cb-103">偵錯本機 Docker 容器中的應用程式</span><span class="sxs-lookup"><span data-stu-id="855cb-103">Debugging apps in a local Docker container</span></span>
## <a name="overview"></a><span data-ttu-id="855cb-104">概觀</span><span class="sxs-lookup"><span data-stu-id="855cb-104">Overview</span></span>
<span data-ttu-id="855cb-105">hello Visual Studio Tools for Docker 會提供一致的方式 toodevelop 中，並驗證 Linux Docker 容器中的本機應用程式。</span><span class="sxs-lookup"><span data-stu-id="855cb-105">hello Visual Studio Tools for Docker provides a consistent way toodevelop in and validate your application locally in a Linux Docker container.</span></span>
<span data-ttu-id="855cb-106">您不需要每次您做變更的程式碼 toorestart hello 容器。</span><span class="sxs-lookup"><span data-stu-id="855cb-106">You don't have toorestart hello container each time you make a code change.</span></span>
<span data-ttu-id="855cb-107">本文說明如何 toouse hello [編輯和重新整理] 功能 toostart ASP.NET Core Web 應用程式在本機的 Docker 容器中，進行任何必要的變更，並再重新整理 hello 瀏覽器 toosee 這些變更。</span><span class="sxs-lookup"><span data-stu-id="855cb-107">This article illustrates how toouse hello "Edit and Refresh" feature toostart an ASP.NET Core Web app in a local Docker container, make any necessary changes, and then refresh hello browser toosee those changes.</span></span>
<span data-ttu-id="855cb-108">本文也將示範如何偵錯 tooset 中斷點。</span><span class="sxs-lookup"><span data-stu-id="855cb-108">This article also shows you how tooset breakpoints for debugging.</span></span>

> [!NOTE]
> <span data-ttu-id="855cb-109">未來版本將支援 Windows 容器</span><span class="sxs-lookup"><span data-stu-id="855cb-109">Windows Container support will be coming in a future release</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="855cb-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="855cb-110">Prerequisites</span></span>
<span data-ttu-id="855cb-111">您必須安裝下列工具 hello。</span><span class="sxs-lookup"><span data-stu-id="855cb-111">hello following tools must be installed.</span></span>

* [<span data-ttu-id="855cb-112">最新版本的 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="855cb-112">Latest version of Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="855cb-113">Microsoft ASP.NET 核心 1.0 SDK</span><span class="sxs-lookup"><span data-stu-id="855cb-113">Microsoft ASP.NET Core 1.0 SDK</span></span>](https://go.microsoft.com/fwlink/?LinkID=809122)

<span data-ttu-id="855cb-114">toorun Docker 容器在本機上，您將需要本機 docker 用戶端。</span><span class="sxs-lookup"><span data-stu-id="855cb-114">toorun Docker containers locally, you'll need a local docker client.</span></span>
<span data-ttu-id="855cb-115">您可以使用 hello [Docker 工具箱](https://www.docker.com/products/docker-toolbox)，需要 HYPER-V toobe 停用，或者您可以使用[Docker for Windows](https://www.docker.com/get-docker)，此方法使用 HYPER-V，並且需要 Windows 10。</span><span class="sxs-lookup"><span data-stu-id="855cb-115">You can use hello [Docker Toolbox](https://www.docker.com/products/docker-toolbox), which requires Hyper-V toobe disabled, or you can use [Docker for Windows](https://www.docker.com/get-docker), which uses Hyper-V, and requires Windows 10.</span></span>

<span data-ttu-id="855cb-116">如果使用 Docker 工具箱，您將需要太[hello Docker 用戶端設定](vs-azure-tools-docker-setup.md)</span><span class="sxs-lookup"><span data-stu-id="855cb-116">If using Docker Toolbox, you'll need too[configure hello Docker client](vs-azure-tools-docker-setup.md)</span></span>

## <a name="1-create-a-web-app"></a><span data-ttu-id="855cb-117">1.建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="855cb-117">1. Create a web app</span></span>
[!INCLUDE [create-aspnet5-app](../includes/create-aspnet5-app.md)]

## <a name="2-add-docker-support"></a><span data-ttu-id="855cb-118">2.新增 Docker 支援</span><span class="sxs-lookup"><span data-stu-id="855cb-118">2. Add Docker support</span></span>
[!INCLUDE [Add docker support](../includes/vs-azure-tools-docker-add-docker-support.md)]

## <a name="3-edit-your-code-and-refresh"></a><span data-ttu-id="855cb-119">3.編輯您的程式碼並重新整理</span><span class="sxs-lookup"><span data-stu-id="855cb-119">3. Edit your code and refresh</span></span>
<span data-ttu-id="855cb-120">tooquickly 逐一查看變更，您可以啟動應用程式內的容器，並繼續 toomake 變更檢視它們，如同使用 IIS Express。</span><span class="sxs-lookup"><span data-stu-id="855cb-120">tooquickly iterate changes, you can start your application within a container, and continue toomake changes, viewing them as you would with IIS Express.</span></span>

1. <span data-ttu-id="855cb-121">設定得 hello 方案組態`Debug`按 **&lt;CTRL + F5 >** toobuild 您的 docker 映像，在本機執行。</span><span class="sxs-lookup"><span data-stu-id="855cb-121">Set hello Solution Configuration too`Debug` and press **&lt;CTRL + F5>** toobuild your docker image and run it locally.</span></span>

    <span data-ttu-id="855cb-122">一旦 hello 容器映像已建置並執行 Docker 容器中，Visual Studio 會啟動預設瀏覽器中的 hello Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="855cb-122">Once hello container image has been built and is running in a Docker container, Visual Studio will launch hello Web app in your default browser.</span></span>
    <span data-ttu-id="855cb-123">如果您使用 hello Microsoft Edge 瀏覽器或否則有錯誤，請參閱[疑難排解](vs-azure-tools-docker-troubleshooting-docker-errors.md)> 一節。</span><span class="sxs-lookup"><span data-stu-id="855cb-123">If you are using hello Microsoft Edge browser or otherwise have errors, see [Troubleshooting](vs-azure-tools-docker-troubleshooting-docker-errors.md) section.</span></span>
2. <span data-ttu-id="855cb-124">移 toohello 有關頁面上，也就是我們會查 toomake 我們變更。</span><span class="sxs-lookup"><span data-stu-id="855cb-124">Go toohello About page, which is where we're going toomake our changes.</span></span>
3. <span data-ttu-id="855cb-125">傳回 tooVisual Studio，並開啟`Views\Home\About.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="855cb-125">Return tooVisual Studio and open `Views\Home\About.cshtml`.</span></span>
4. <span data-ttu-id="855cb-126">新增 hello 遵循 hello 檔案的 HTML 內容 toohello 結尾，並儲存 hello 變更。</span><span class="sxs-lookup"><span data-stu-id="855cb-126">Add hello following HTML content toohello end of hello file and save hello changes.</span></span>

    ```
    <h1>Hello from a Docker Container!</h1>
    ```
5. <span data-ttu-id="855cb-127">完成 hello.NET 建置，而且您會看到這些線條，請檢視 hello 輸出 視窗中，切換後 tooyour 瀏覽器，並重新整理頁面相關的 hello。</span><span class="sxs-lookup"><span data-stu-id="855cb-127">Viewing hello output window, when hello .NET build is completed and you see these lines, switch back tooyour browser and refresh hello About page.</span></span>

   ```
   Now listening on: http://*:80
   Application started. Press Ctrl+C tooshut down
   ```
6. <span data-ttu-id="855cb-128">您的變更已經套用！</span><span class="sxs-lookup"><span data-stu-id="855cb-128">Your changes have been applied!</span></span>

## <a name="4-debug-with-breakpoints"></a><span data-ttu-id="855cb-129">4.使用中斷點進行偵錯</span><span class="sxs-lookup"><span data-stu-id="855cb-129">4. Debug with breakpoints</span></span>
<span data-ttu-id="855cb-130">通常，變更將會需要進一步檢查，利用 hello 偵錯 Visual Studio 的功能。</span><span class="sxs-lookup"><span data-stu-id="855cb-130">Often, changes will need further inspection, leveraging hello debugging features of Visual Studio.</span></span>

1. <span data-ttu-id="855cb-131">傳回 tooVisual Studio，並開啟`Controllers\HomeController.cs`</span><span class="sxs-lookup"><span data-stu-id="855cb-131">Return tooVisual Studio and open `Controllers\HomeController.cs`</span></span>
2. <span data-ttu-id="855cb-132">取代 hello 下列 hello hello about 方法內容：</span><span class="sxs-lookup"><span data-stu-id="855cb-132">Replace hello contents of hello About() method with hello following:</span></span>

   ```
   string message = "Your application description page from within a Container";
   ViewData["Message"] = message;
   ````
3. <span data-ttu-id="855cb-133">設定中斷點 toohello 方 hello `string message`...列。</span><span class="sxs-lookup"><span data-stu-id="855cb-133">Set a breakpoint toohello left of hello `string message`... line.</span></span>
4. <span data-ttu-id="855cb-134">叫用 **&lt;F5 >** toostart 偵錯。</span><span class="sxs-lookup"><span data-stu-id="855cb-134">Hit **&lt;F5>** toostart debugging.</span></span>
5. <span data-ttu-id="855cb-135">有關頁面 toohit toohello 瀏覽您的中斷點。</span><span class="sxs-lookup"><span data-stu-id="855cb-135">Navigate toohello About page toohit your breakpoint.</span></span>
6. <span data-ttu-id="855cb-136">切換 tooVisual Studio tooview hello 中斷點，並檢查 hello 訊息值。</span><span class="sxs-lookup"><span data-stu-id="855cb-136">Switch tooVisual Studio tooview hello breakpoint, and inspect hello value of message.</span></span>

   ![][2]

## <a name="summary"></a><span data-ttu-id="855cb-137">摘要</span><span class="sxs-lookup"><span data-stu-id="855cb-137">Summary</span></span>
<span data-ttu-id="855cb-138">與[Visual Studio 2015 Tools for Docker](https://aka.ms/DockerToolsForVS)，就可以使用在本機開發 Docker 容器中的 hello 生產真實性的 hello 產能。</span><span class="sxs-lookup"><span data-stu-id="855cb-138">With [Visual Studio 2015 Tools for Docker](https://aka.ms/DockerToolsForVS), you can get hello productivity of working locally, with hello production realism of developing within a Docker container.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="855cb-139">疑難排解</span><span class="sxs-lookup"><span data-stu-id="855cb-139">Troubleshooting</span></span>
[<span data-ttu-id="855cb-140">疑難排解 Visual Studio Docker 開發</span><span class="sxs-lookup"><span data-stu-id="855cb-140">Troubleshooting Visual Studio Docker Development</span></span>](vs-azure-tools-docker-troubleshooting-docker-errors.md)

## <a name="more-about-docker-with-visual-studio-windows-and-azure"></a><span data-ttu-id="855cb-141">進一步了解 Docker 與 Visual Studio、Windows 和 Azure</span><span class="sxs-lookup"><span data-stu-id="855cb-141">More about Docker with Visual Studio, Windows, and Azure</span></span>
* <span data-ttu-id="855cb-142">[Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) - 在容器中開發 .NET Core 程式碼</span><span class="sxs-lookup"><span data-stu-id="855cb-142">[Docker Tools for Visual Studio](http://aka.ms/dockertoolsforvs) - Developing your .NET Core code in a container</span></span>
* <span data-ttu-id="855cb-143">[Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) - 建置和部署 Docker 容器</span><span class="sxs-lookup"><span data-stu-id="855cb-143">[Docker Tools for Visual Studio Team Services](http://aka.ms/dockertoolsforvsts) - Build and Deploy docker containers</span></span>
* <span data-ttu-id="855cb-144">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) - 用於編輯 Docker 檔案的語言服務，將推出更多其他 e2e 案例</span><span class="sxs-lookup"><span data-stu-id="855cb-144">[Docker Tools for Visual Studio Code](http://aka.ms/dockertoolsforvscode) - Language services for editing docker files, with more e2e scenarios coming</span></span>
* <span data-ttu-id="855cb-145">[Windows 容器資訊](http://aka.ms/containers)- Windows Server 和 Nano Server 資訊</span><span class="sxs-lookup"><span data-stu-id="855cb-145">[Windows Container Information](http://aka.ms/containers)- Windows Server and Nano Server information</span></span>
* <span data-ttu-id="855cb-146">[Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Azure Container Service 內容](http://aka.ms/AzureContainerService)</span><span class="sxs-lookup"><span data-stu-id="855cb-146">[Azure Container Service](https://azure.microsoft.com/services/container-service/) - [Azure Container Service Content](http://aka.ms/AzureContainerService)</span></span>
* <span data-ttu-id="855cb-147">如需使用 Docker 的範例，請參閱[使用 Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker)從 hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015年連接[示範](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/)。</span><span class="sxs-lookup"><span data-stu-id="855cb-147">For more examples of working with Docker, see [Working with Docker](https://github.com/Microsoft/HealthClinic.biz/wiki/Working-with-Docker) from hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span> <span data-ttu-id="855cb-148">如需從 hello HealthClinic.biz 示範的快速入門，請參閱[Azure 開發人員工具快速入門](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts)。</span><span class="sxs-lookup"><span data-stu-id="855cb-148">For more quickstarts from hello HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>

## <a name="various-docker-tools"></a><span data-ttu-id="855cb-149">各種 Docker 工具</span><span class="sxs-lookup"><span data-stu-id="855cb-149">Various Docker tools</span></span>
[<span data-ttu-id="855cb-150">一些不錯的 Docker 工具 (Steve Lasker 的部落格)</span><span class="sxs-lookup"><span data-stu-id="855cb-150">Some great docker tools (Steve Lasker's blog)</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/03/25/some-great-docker-tools/)

## <a name="good-articles"></a><span data-ttu-id="855cb-151">不錯的文章</span><span class="sxs-lookup"><span data-stu-id="855cb-151">Good articles</span></span>
[<span data-ttu-id="855cb-152">從 NGINX 簡介 tooMicroservices</span><span class="sxs-lookup"><span data-stu-id="855cb-152">Introduction tooMicroservices from NGINX</span></span>](https://www.nginx.com/blog/introduction-to-microservices/)

## <a name="presentations"></a><span data-ttu-id="855cb-153">簡報</span><span class="sxs-lookup"><span data-stu-id="855cb-153">Presentations</span></span>
* [<span data-ttu-id="855cb-154">Steve Lasker：VS Live Las Vegas 2016 - Docker e2e</span><span class="sxs-lookup"><span data-stu-id="855cb-154">Steve Lasker: VS Live Las Vegas 2016 - Docker e2e</span></span>](https://github.com/SteveLasker/Presentations/blob/master/VSLive2016/Vegas/)
* [<span data-ttu-id="855cb-155">@ 組建 2016-其中您在示範簡介 tooASP.NET 核心</span><span class="sxs-lookup"><span data-stu-id="855cb-155">Introduction tooASP.NET Core @ build 2016 - Where You At Demo</span></span>](https://channel9.msdn.com/Events/Build/2016/B810)
* [<span data-ttu-id="855cb-156">開發容器中的 .NET 應用程式 (Channel 9)</span><span class="sxs-lookup"><span data-stu-id="855cb-156">Developing .NET apps in containers, Channel 9</span></span>](https://blogs.msdn.microsoft.com/stevelasker/2016/02/19/developing-asp-net-apps-in-docker-containers/)

[2]: ./media/vs-azure-tools-docker-edit-and-refresh/breakpoint.png
