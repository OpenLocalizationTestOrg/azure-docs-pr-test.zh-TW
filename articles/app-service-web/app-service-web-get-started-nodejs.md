---
title: "Node.js web 應用程式在 Azure 中 aaaCreate |Microsoft 文件"
description: "短短幾分鐘內在 Azure App Service Web Apps 中部署第一個 Node.js Hello World。"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 582bb3c2-164b-42f5-b081-95bfcb7a502a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/05/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 163edf83b2353755fc9fa2d75aed489038cf7c81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-web-app-in-azure"></a><span data-ttu-id="91ca3-103">在 Azure 中建立 Node.js Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="91ca3-103">Create a Node.js web app in Azure</span></span>

<span data-ttu-id="91ca3-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 提供可高度擴充、自我修復的 Web 主機服務。</span><span class="sxs-lookup"><span data-stu-id="91ca3-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="91ca3-105">本快速入門示範如何 toodeploy Node.js 應用程式 tooAzure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="91ca3-105">This quickstart shows how toodeploy a Node.js app tooAzure Web Apps.</span></span> <span data-ttu-id="91ca3-106">建立 hello web 應用程式使用 hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)，而且您使用 Git toodeploy 範例 Node.js 的程式碼 toohello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="91ca3-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample Node.js code toohello web app.</span></span>

![在 Azure 中執行的範例應用程式](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="91ca3-108">您可以依照下列使用 Mac、 Windows 或 Linux 電腦的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="91ca3-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="91ca3-109">一旦安裝 hello 必要條件，花費大約五分鐘 toocomplete hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="91ca3-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a><span data-ttu-id="91ca3-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="91ca3-110">Prerequisites</span></span>

<span data-ttu-id="91ca3-111">toocomplete 本快速入門：</span><span class="sxs-lookup"><span data-stu-id="91ca3-111">toocomplete this quickstart:</span></span>

* [<span data-ttu-id="91ca3-112">安裝 Git</span><span class="sxs-lookup"><span data-stu-id="91ca3-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="91ca3-113">安裝 Node.js 和 NPM</span><span class="sxs-lookup"><span data-stu-id="91ca3-113">Install Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="91ca3-114">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="91ca3-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="91ca3-115">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="91ca3-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="91ca3-116">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="91ca3-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="91ca3-117">下載 hello 範例</span><span class="sxs-lookup"><span data-stu-id="91ca3-117">Download hello sample</span></span>

<span data-ttu-id="91ca3-118">在終端機視窗中，執行下列命令 tooclone hello 範例應用程式儲存機制 tooyour 本機電腦的 hello。</span><span class="sxs-lookup"><span data-stu-id="91ca3-118">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

<span data-ttu-id="91ca3-119">您使用這個終端機視窗 toorun 所有 hello 命令本快速入門。</span><span class="sxs-lookup"><span data-stu-id="91ca3-119">You use this terminal window toorun all hello commands in this quickstart.</span></span>

<span data-ttu-id="91ca3-120">變更 toohello 目錄，包含 hello 範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="91ca3-120">Change toohello directory that contains hello sample code.</span></span>

```bash
cd nodejs-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="91ca3-121">在本機執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="91ca3-121">Run hello app locally</span></span>

<span data-ttu-id="91ca3-122">在本機執行 hello 應用程式，開啟終端機視窗，並使用 hello `npm start` Node.js HTTP 伺服器內建的指令碼 toolaunch hello。</span><span class="sxs-lookup"><span data-stu-id="91ca3-122">Run hello application locally by opening a terminal window and using hello `npm start` script toolaunch hello built in Node.js HTTP server.</span></span>

```bash
npm start
```

<span data-ttu-id="91ca3-123">開啟網頁瀏覽器，並瀏覽 http://localhost:1337 toohello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="91ca3-123">Open a web browser, and navigate toohello sample app at http://localhost:1337.</span></span>

<span data-ttu-id="91ca3-124">您會看到 hello **Hello World** hello 範例應用程式中 hello 頁面中所顯示的訊息。</span><span class="sxs-lookup"><span data-stu-id="91ca3-124">You see hello **Hello World** message from hello sample app displayed in hello page.</span></span>

![在本機執行的範例應用程式](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

<span data-ttu-id="91ca3-126">在終端機視窗中，按**Ctrl + C** tooexit hello web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="91ca3-126">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![空的 Web 應用程式頁面](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="91ca3-128">您已在 Azure 中建立空的新 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="91ca3-128">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 23, done.
Delta compression using up too4 threads.
Compressing objects: 100% (21/21), done.
Writing objects: 100% (23/23), 3.71 KiB | 0 bytes/s, done.
Total 23 (delta 8), reused 7 (delta 1)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'bf114df591'.
remote: Generating deployment script.
remote: Generating deployment script for node.js Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling node.js deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.js'
remote: Copying file: 'package.json'
remote: Copying file: 'process.json'
remote: Deleting file: 'hostingstart.html'
remote: Ignoring: .git
remote: Using start-up script index.js from package.json.
remote: Node.js versions available on hello platform are: 4.4.7, 4.5.0, 6.2.2, 6.6.0, 6.9.1.
remote: Selected node.js version 6.9.1. Use package.json file toochoose a different version.
remote: Selected npm version 3.10.8
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net:443/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="91ca3-129">瀏覽 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="91ca3-129">Browse toohello app</span></span>

<span data-ttu-id="91ca3-130">瀏覽 toohello 部署使用網頁瀏覽器應用程式。</span><span class="sxs-lookup"><span data-stu-id="91ca3-130">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="91ca3-131">hello Node.js 範例程式碼正在執行的 Azure App Service web 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="91ca3-131">hello Node.js sample code is running in an Azure App Service web app.</span></span>

![在 Azure 中執行的範例應用程式](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="91ca3-133">**恭喜！**</span><span class="sxs-lookup"><span data-stu-id="91ca3-133">**Congratulations!**</span></span> <span data-ttu-id="91ca3-134">您已部署您第一次的 Node.js 應用程式 tooApp 服務。</span><span class="sxs-lookup"><span data-stu-id="91ca3-134">You've deployed your first Node.js app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-code"></a><span data-ttu-id="91ca3-135">更新和重新部署 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="91ca3-135">Update and redeploy hello code</span></span>

<span data-ttu-id="91ca3-136">使用文字編輯器開啟 hello `index.js` hello Node.js 應用程式，在檔案和太 hello 呼叫中進行小變更 toohello 文字`response.end`:</span><span class="sxs-lookup"><span data-stu-id="91ca3-136">Using a text editor, open hello `index.js` file in hello Node.js app, and make a small change toohello text in hello call too`response.end`:</span></span>

```nodejs
response.end("Hello Azure!");
```

<span data-ttu-id="91ca3-137">認可您在 Git 中的變更，並接著推送 hello 程式碼變更 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="91ca3-137">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="91ca3-138">部署完成後，請切換後 toohello 瀏覽器視窗開啟在 hello**瀏覽 toohello 應用程式**逐步執行和點擊 重新整理。</span><span class="sxs-lookup"><span data-stu-id="91ca3-138">Once deployment has completed, switch back toohello browser window that opened in hello **Browse toohello app** step, and hit refresh.</span></span>

![在 Azure 中執行的已更新範例應用程式](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="91ca3-140">管理新的 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="91ca3-140">Manage your new Azure web app</span></span>

<span data-ttu-id="91ca3-141">移 toohello <a href="https://portal.azure.com" target="_blank">Azure 入口網站</a>toomanage hello web 應用程式所建立。</span><span class="sxs-lookup"><span data-stu-id="91ca3-141">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="91ca3-142">從 hello 左窗格中，按一下 **應用程式服務**，然後按一下hello Azure web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="91ca3-142">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![入口網站瀏覽 tooAzure web 應用程式](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="91ca3-144">您會看到 Web 應用程式的 [概觀] 頁面。</span><span class="sxs-lookup"><span data-stu-id="91ca3-144">You see your web app's Overview page.</span></span> <span data-ttu-id="91ca3-145">您可以在這裡執行基本管理工作，像是瀏覽、停止、啟動、重新啟動及刪除。</span><span class="sxs-lookup"><span data-stu-id="91ca3-145">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Azure 入口網站中的 App Service 刀鋒視窗](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="91ca3-147">hello 左側的功能表提供不同頁面設定您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="91ca3-147">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="91ca3-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="91ca3-148">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="91ca3-149">Node.js with MongoDB</span><span class="sxs-lookup"><span data-stu-id="91ca3-149">Node.js with MongoDB</span></span>](app-service-web-tutorial-nodejs-mongodb-app.md)
