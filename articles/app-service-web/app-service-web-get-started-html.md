---
title: "在 Azure 中建立靜態 HTML Web 應用程式 | Microsoft Docs"
description: "藉由部署靜態 HTML 範例應用程式，了解如何在 Azure App Service 中執行 Web 應用程式。"
services: app-service\web
documentationcenter: 
author: rick-anderson
manager: wpickett
editor: 
ms.assetid: 60495cc5-6963-4bf0-8174-52786d226c26
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/26/2017
ms.author: riande
ms.custom: mvc
ms.openlocfilehash: 42af5b08b8d2ff0c75fd73dcfa61c861647fd2c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-static-html-web-app-in-azure"></a><span data-ttu-id="b1331-103">在 Azure 中建立靜態 HTML Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="b1331-103">Create a static HTML web app in Azure</span></span>

<span data-ttu-id="b1331-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 提供可高度擴充、自我修復的 Web 主機服務。</span><span class="sxs-lookup"><span data-stu-id="b1331-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="b1331-105">本快速入門顯示如何將基本 HTML+CSS 網站部署至 Azure Web Apps。</span><span class="sxs-lookup"><span data-stu-id="b1331-105">This quickstart shows how to deploy a basic HTML+CSS site to Azure Web Apps.</span></span> <span data-ttu-id="b1331-106">您可使用 [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)建立 Web 應用程式，而且使用 Git 將範例 HTML 內容部署至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b1331-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy sample HTML content to the web app.</span></span>

![範例應用程式首頁](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="b1331-108">您可以使用 Mac、Windows 或 Linux 電腦，依照下面步驟操作。</span><span class="sxs-lookup"><span data-stu-id="b1331-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="b1331-109">安裝先決條件後，大約需要 5 分鐘才能完成這些步驟。</span><span class="sxs-lookup"><span data-stu-id="b1331-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b1331-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="b1331-110">Prerequisites</span></span>

<span data-ttu-id="b1331-111">若要完成本快速入門：</span><span class="sxs-lookup"><span data-stu-id="b1331-111">To complete this quickstart:</span></span>

- <span data-ttu-id="b1331-112">[安裝 Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span><span class="sxs-lookup"><span data-stu-id="b1331-112">[Install Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b1331-113">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="b1331-113">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b1331-114">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="b1331-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="b1331-115">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="b1331-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-the-sample"></a><span data-ttu-id="b1331-116">下載範例</span><span class="sxs-lookup"><span data-stu-id="b1331-116">Download the sample</span></span>

<span data-ttu-id="b1331-117">在終端機視窗中執行下列命令，將範例應用程式存放庫複製到本機電腦。</span><span class="sxs-lookup"><span data-stu-id="b1331-117">In a terminal window, run the following command to clone the sample app repository to your local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

<span data-ttu-id="b1331-118">您可使用這個終端機視窗來執行本快速入門中的所有命令。</span><span class="sxs-lookup"><span data-stu-id="b1331-118">You use this terminal window to run all the commands in this quickstart.</span></span>

## <a name="view-the-html"></a><span data-ttu-id="b1331-119">HTML 檢視</span><span class="sxs-lookup"><span data-stu-id="b1331-119">View the HTML</span></span>

<span data-ttu-id="b1331-120">瀏覽至包含範例 HTML 的目錄。</span><span class="sxs-lookup"><span data-stu-id="b1331-120">Navigate to the directory that contains the sample HTML.</span></span> <span data-ttu-id="b1331-121">在瀏覽器中開啟 *index.html* 檔案。</span><span class="sxs-lookup"><span data-stu-id="b1331-121">Open the *index.html* file in your browser.</span></span>

![範例應用程式首頁](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in to Azure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![空的 Web 應用程式頁面](media/app-service-web-get-started-html/app-service-web-service-created.png)

<span data-ttu-id="b1331-124">您已在 Azure 中建立空的新 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b1331-124">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (13/13), 2.07 KiB | 0 bytes/s, done.
Total 13 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'cc39b1e4cb'.
remote: Generating deployment script.
remote: Generating deployment script for Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-to-the-app"></a><span data-ttu-id="b1331-125">瀏覽至應用程式</span><span class="sxs-lookup"><span data-stu-id="b1331-125">Browse to the app</span></span>

<span data-ttu-id="b1331-126">在瀏覽器中，移至 Azure Web 應用程式 URL：</span><span class="sxs-lookup"><span data-stu-id="b1331-126">In a browser, go to the Azure web app URL:</span></span>

```
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="b1331-127">此頁面目前作為 Azure App Service Web 應用程式執行。</span><span class="sxs-lookup"><span data-stu-id="b1331-127">The page is running as an Azure App Service web app.</span></span>

![範例應用程式首頁](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="b1331-129">**恭喜！**</span><span class="sxs-lookup"><span data-stu-id="b1331-129">**Congratulations!**</span></span> <span data-ttu-id="b1331-130">您已將第一個 HTML 應用程式部署至 App Service。</span><span class="sxs-lookup"><span data-stu-id="b1331-130">You've deployed your first HTML app to App Service.</span></span>

## <a name="update-and-redeploy-the-app"></a><span data-ttu-id="b1331-131">更新和重新部署應用程式</span><span class="sxs-lookup"><span data-stu-id="b1331-131">Update and redeploy the app</span></span>

<span data-ttu-id="b1331-132">在文字編輯器中開啟 *index.html* 檔案，並對標記進行變更。</span><span class="sxs-lookup"><span data-stu-id="b1331-132">Open the *index.html* file in a text editor, and make a change to the markup.</span></span> <span data-ttu-id="b1331-133">例如，將 H1 標題從「Azure App Service - 範例靜態 HTML 網站」變更為只剩下「Azure App Service」。</span><span class="sxs-lookup"><span data-stu-id="b1331-133">For example, change the H1 heading from "Azure App Service - Sample Static HTML Site" to just "Azure App Service\`.</span></span>

<span data-ttu-id="b1331-134">在 Git 中認可您的變更，然後將程式碼變更推送至 Azure。</span><span class="sxs-lookup"><span data-stu-id="b1331-134">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated HTML"
git push azure master
```

<span data-ttu-id="b1331-135">完成部署後，重新整理瀏覽器以查看變更。</span><span class="sxs-lookup"><span data-stu-id="b1331-135">Once deployment has completed, refresh your browser to see the changes.</span></span>

![已更新的範例應用程式首頁](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="b1331-137">管理新的 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="b1331-137">Manage your new Azure web app</span></span>

<span data-ttu-id="b1331-138">請移至 <a href="https://portal.azure.com" target="_blank">Azure 入口網站</a>，以管理您所建立的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b1331-138">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="b1331-139">按一下左側功能表中的 [應用程式服務]，然後按一下 Azure Web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="b1331-139">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![入口網站瀏覽至 Azure Web 應用程式](./media/app-service-web-get-started-html/portal1.png)

<span data-ttu-id="b1331-141">您會看到 Web 應用程式的 [概觀] 頁面。</span><span class="sxs-lookup"><span data-stu-id="b1331-141">You see your web app's Overview page.</span></span> <span data-ttu-id="b1331-142">您可以在這裡執行基本管理工作，像是瀏覽、停止、啟動、重新啟動及刪除。</span><span class="sxs-lookup"><span data-stu-id="b1331-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Azure 入口網站中的 App Service 刀鋒視窗](./media/app-service-web-get-started-html/portal2.png)

<span data-ttu-id="b1331-144">左側功能表提供不同的頁面來設定您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b1331-144">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="b1331-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b1331-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b1331-146">對應自訂網域</span><span class="sxs-lookup"><span data-stu-id="b1331-146">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
