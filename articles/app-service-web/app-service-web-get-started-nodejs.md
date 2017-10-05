---
title: "在 Azure 中建立 Node.js Web 應用程式"
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
ms.openlocfilehash: ce845da09a7c088b8a2ba29b818a46a3b41aa4e7
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-nodejs-web-app-in-azure"></a><span data-ttu-id="64e15-103">在 Azure 中建立 Node.js Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="64e15-103">Create a Node.js web app in Azure</span></span>

<span data-ttu-id="64e15-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 提供可高度擴充、自我修復的 Web 主機服務。</span><span class="sxs-lookup"><span data-stu-id="64e15-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="64e15-105">本快速入門會顯示如何將 Node.js 應用程式部署至 Azure Web Apps。</span><span class="sxs-lookup"><span data-stu-id="64e15-105">This quickstart shows how to deploy a Node.js app to Azure Web Apps.</span></span> <span data-ttu-id="64e15-106">您可使用 [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)建立 Web 應用程式，而且使用 Git 將範例 Node.js 程式碼部署至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="64e15-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy sample Node.js code to the web app.</span></span>

![在 Azure 中執行的範例應用程式](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="64e15-108">您可以使用 Mac、Windows 或 Linux 電腦，依照下面步驟操作。</span><span class="sxs-lookup"><span data-stu-id="64e15-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="64e15-109">安裝先決條件後，大約需要 5 分鐘才能完成這些步驟。</span><span class="sxs-lookup"><span data-stu-id="64e15-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a><span data-ttu-id="64e15-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="64e15-110">Prerequisites</span></span>

<span data-ttu-id="64e15-111">若要完成本快速入門：</span><span class="sxs-lookup"><span data-stu-id="64e15-111">To complete this quickstart:</span></span>

* [<span data-ttu-id="64e15-112">安裝 Git</span><span class="sxs-lookup"><span data-stu-id="64e15-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="64e15-113">安裝 Node.js 和 NPM</span><span class="sxs-lookup"><span data-stu-id="64e15-113">Install Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="64e15-114">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="64e15-114">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="64e15-115">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="64e15-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="64e15-116">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="64e15-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-the-sample"></a><span data-ttu-id="64e15-117">下載範例</span><span class="sxs-lookup"><span data-stu-id="64e15-117">Download the sample</span></span>

<span data-ttu-id="64e15-118">在終端機視窗中執行下列命令，將範例應用程式存放庫複製到本機電腦。</span><span class="sxs-lookup"><span data-stu-id="64e15-118">In a terminal window, run the following command to clone the sample app repository to your local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

<span data-ttu-id="64e15-119">您可使用這個終端機視窗來執行本快速入門中的所有命令。</span><span class="sxs-lookup"><span data-stu-id="64e15-119">You use this terminal window to run all the commands in this quickstart.</span></span>

<span data-ttu-id="64e15-120">變更為包含範例程式碼的目錄。</span><span class="sxs-lookup"><span data-stu-id="64e15-120">Change to the directory that contains the sample code.</span></span>

```bash
cd nodejs-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="64e15-121">在本機執行應用程式</span><span class="sxs-lookup"><span data-stu-id="64e15-121">Run the app locally</span></span>

<span data-ttu-id="64e15-122">開啟終端機視窗並使用 `npm start` 指令碼來啟動內建 Node.js HTTP 伺服器，以在本機執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="64e15-122">Run the application locally by opening a terminal window and using the `npm start` script to launch the built in Node.js HTTP server.</span></span>

```bash
npm start
```

<span data-ttu-id="64e15-123">開啟網頁瀏覽器，然後瀏覽至範例應用程式 (位於 http://localhost:1337 )。</span><span class="sxs-lookup"><span data-stu-id="64e15-123">Open a web browser, and navigate to the sample app at http://localhost:1337.</span></span>

<span data-ttu-id="64e15-124">您會看到來自範例應用程式的 **Hello World** 訊息顯示在網頁中。</span><span class="sxs-lookup"><span data-stu-id="64e15-124">You see the **Hello World** message from the sample app displayed in the page.</span></span>

![在本機執行的範例應用程式](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

<span data-ttu-id="64e15-126">在終端機視窗中，按 **Ctrl+C** 結束 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="64e15-126">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

[!INCLUDE [Log in to Azure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![空的 Web 應用程式頁面](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="64e15-128">您已在 Azure 中建立空的新 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="64e15-128">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 23, done.
Delta compression using up to 4 threads.
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
remote: Node.js versions available on the platform are: 4.4.7, 4.5.0, 6.2.2, 6.6.0, 6.9.1.
remote: Selected node.js version 6.9.1. Use package.json file to choose a different version.
remote: Selected npm version 3.10.8
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net:443/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-to-the-app"></a><span data-ttu-id="64e15-129">瀏覽至應用程式</span><span class="sxs-lookup"><span data-stu-id="64e15-129">Browse to the app</span></span>

<span data-ttu-id="64e15-130">使用 web 瀏覽器瀏覽至已部署的應用程式。</span><span class="sxs-lookup"><span data-stu-id="64e15-130">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="64e15-131">Node.js 範例程式碼正在 Azure App Service Web 應用程式中執行。</span><span class="sxs-lookup"><span data-stu-id="64e15-131">The Node.js sample code is running in an Azure App Service web app.</span></span>

![在 Azure 中執行的範例應用程式](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="64e15-133">**恭喜！**</span><span class="sxs-lookup"><span data-stu-id="64e15-133">**Congratulations!**</span></span> <span data-ttu-id="64e15-134">您已將第一個 Node.js 應用程式部署至 App Service。</span><span class="sxs-lookup"><span data-stu-id="64e15-134">You've deployed your first Node.js app to App Service.</span></span>

## <a name="update-and-redeploy-the-code"></a><span data-ttu-id="64e15-135">更新和重新部署程式碼</span><span class="sxs-lookup"><span data-stu-id="64e15-135">Update and redeploy the code</span></span>

<span data-ttu-id="64e15-136">使用文字編輯器，開啟 Node.js 應用程式中的 `index.js` 檔案，並且對 `response.end` 呼叫中的文字進行小幅變更：</span><span class="sxs-lookup"><span data-stu-id="64e15-136">Using a text editor, open the `index.js` file in the Node.js app, and make a small change to the text in the call to `response.end`:</span></span>

```nodejs
response.end("Hello Azure!");
```

<span data-ttu-id="64e15-137">在 Git 中認可您的變更，然後將程式碼變更推送至 Azure。</span><span class="sxs-lookup"><span data-stu-id="64e15-137">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="64e15-138">部署完成後，切換回在「瀏覽至應用程式」步驟中開啟的瀏覽器視窗，然後按 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="64e15-138">Once deployment has completed, switch back to the browser window that opened in the **Browse to the app** step, and hit refresh.</span></span>

![在 Azure 中執行的已更新範例應用程式](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="64e15-140">管理新的 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="64e15-140">Manage your new Azure web app</span></span>

<span data-ttu-id="64e15-141">請移至 <a href="https://portal.azure.com" target="_blank">Azure 入口網站</a>，以管理您所建立的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="64e15-141">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="64e15-142">按一下左側功能表中的 [應用程式服務]，然後按一下 Azure Web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="64e15-142">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![入口網站瀏覽至 Azure Web 應用程式](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="64e15-144">您會看到 Web 應用程式的 [概觀] 頁面。</span><span class="sxs-lookup"><span data-stu-id="64e15-144">You see your web app's Overview page.</span></span> <span data-ttu-id="64e15-145">您可以在這裡執行基本管理工作，像是瀏覽、停止、啟動、重新啟動及刪除。</span><span class="sxs-lookup"><span data-stu-id="64e15-145">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Azure 入口網站中的 App Service 刀鋒視窗](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="64e15-147">左側功能表提供不同的頁面來設定您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="64e15-147">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="64e15-148">後續步驟</span><span class="sxs-lookup"><span data-stu-id="64e15-148">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="64e15-149">Node.js with MongoDB</span><span class="sxs-lookup"><span data-stu-id="64e15-149">Node.js with MongoDB</span></span>](app-service-web-tutorial-nodejs-mongodb-app.md)
