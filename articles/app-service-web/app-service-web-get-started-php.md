---
title: "aaaCreate PHP web 應用程式在 Azure 中的 |Microsoft 文件"
description: "短短幾分鐘內在 Azure App Service Web Apps 中部署第一個 PHP Hello World。"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 07/21/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 8e1022889ca162f8f15ce7435cc9393cc6efef06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-web-app-in-azure"></a><span data-ttu-id="3f109-103">在 Azure 中建立 PHP Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="3f109-103">Create a PHP web app in Azure</span></span>

<span data-ttu-id="3f109-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 提供可高度擴充、自我修復的 Web 主機服務。</span><span class="sxs-lookup"><span data-stu-id="3f109-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="3f109-105">本快速入門教學課程示範如何 toodeploy PHP 應用程式 tooAzure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f109-105">This quickstart tutorial shows how toodeploy a PHP app tooAzure Web Apps.</span></span> <span data-ttu-id="3f109-106">建立 hello web 應用程式使用 hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)在雲端 Shell 中，而且您使用 Git toodeploy 範例 PHP 程式碼 toohello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f109-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) in Cloud Shell, and you use Git toodeploy sample PHP code toohello web app.</span></span>

<span data-ttu-id="3f109-107">![在 Azure 中執行的範例應用程式]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span><span class="sxs-lookup"><span data-stu-id="3f109-107">![Sample app running in Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span></span>

<span data-ttu-id="3f109-108">您可以依照下列使用 Mac、 Windows 或 Linux 電腦的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="3f109-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="3f109-109">一旦安裝 hello 必要條件，花費大約五分鐘 toocomplete hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="3f109-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f109-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="3f109-110">Prerequisites</span></span>

<span data-ttu-id="3f109-111">toocomplete 本快速入門：</span><span class="sxs-lookup"><span data-stu-id="3f109-111">toocomplete this quickstart:</span></span>

* [<span data-ttu-id="3f109-112">安裝 Git</span><span class="sxs-lookup"><span data-stu-id="3f109-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="3f109-113">安裝 PHP</span><span class="sxs-lookup"><span data-stu-id="3f109-113">Install PHP</span></span>](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample-locally"></a><span data-ttu-id="3f109-114">下載本機 hello 範例</span><span class="sxs-lookup"><span data-stu-id="3f109-114">Download hello sample locally</span></span>

<span data-ttu-id="3f109-115">在終端機視窗中，執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="3f109-115">In a terminal window, run hello following commands.</span></span> <span data-ttu-id="3f109-116">這將會複製 hello 範例應用程式 tooyour 本機電腦，並瀏覽 toohello 目錄包含 hello 範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="3f109-116">This will clone hello sample application tooyour local machine, and navigate toohello directory containing hello sample code.</span></span>

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="3f109-117">在本機執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="3f109-117">Run hello app locally</span></span>

<span data-ttu-id="3f109-118">在本機執行 hello 應用程式，開啟終端機視窗，並使用 hello`php`命令 toolaunch hello 內建 PHP web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="3f109-118">Run hello application locally by opening a terminal window and using hello `php` command toolaunch hello built-in PHP web server.</span></span>

```bash
php -S localhost:8080
```

<span data-ttu-id="3f109-119">開啟網頁瀏覽器，並瀏覽 http://localhost:8080/< toohello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f109-119">Open a web browser, and navigate toohello sample app at http://localhost:8080.</span></span>

<span data-ttu-id="3f109-120">您會看到 hello **Hello World ！**</span><span class="sxs-lookup"><span data-stu-id="3f109-120">You see hello **Hello World!**</span></span> <span data-ttu-id="3f109-121">hello 範例應用程式中 hello 頁面中所顯示的訊息。</span><span class="sxs-lookup"><span data-stu-id="3f109-121">message from hello sample app displayed in hello page.</span></span>

![在本機執行的範例應用程式](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

<span data-ttu-id="3f109-123">在終端機視窗中，按**Ctrl + C** tooexit hello web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="3f109-123">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![空的 Web 應用程式頁面](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="3f109-125">您已在 Azure 中建立空的新 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f109-125">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 2, done.
Delta compression using up too4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 352 bytes | 0 bytes/s, done.
Total 2 (delta 1), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '25f18051e9'.
remote: Generating deployment script.
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.php'
remote: Ignoring: .git
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
   cc39b1e..25f1805  master -> master
```

## <a name="browse-toohello-app-locally"></a><span data-ttu-id="3f109-126">瀏覽本機 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="3f109-126">Browse toohello app locally</span></span>

<span data-ttu-id="3f109-127">瀏覽 toohello 部署使用網頁瀏覽器應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f109-127">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="3f109-128">hello PHP 範例程式碼正在執行的 Azure App Service web 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="3f109-128">hello PHP sample code is running in an Azure App Service web app.</span></span>

![在 Azure 中執行的範例應用程式](media/app-service-web-get-started-php/hello-world-in-browser.png)

<span data-ttu-id="3f109-130">**恭喜！**</span><span class="sxs-lookup"><span data-stu-id="3f109-130">**Congratulations!**</span></span> <span data-ttu-id="3f109-131">您已部署您第一次的 PHP 應用程式 tooApp 服務。</span><span class="sxs-lookup"><span data-stu-id="3f109-131">You've deployed your first PHP app tooApp Service.</span></span>

## <a name="update-locally-and-redeploy-hello-code"></a><span data-ttu-id="3f109-132">在本機更新和重新部署 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="3f109-132">Update locally and redeploy hello code</span></span>

<span data-ttu-id="3f109-133">使用本機的文字編輯器開啟 hello `index.php` hello PHP 應用程式中的檔案，並進行小幅變更 toohello 內的文字字串 hello 接下來太`echo`:</span><span class="sxs-lookup"><span data-stu-id="3f109-133">Using a local text editor, open hello `index.php` file within hello PHP app, and make a small change toohello text within hello string next too`echo`:</span></span>

```php
echo "Hello Azure!";
```

<span data-ttu-id="3f109-134">認可您在 Git 中的變更，並接著推送 hello 程式碼變更 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="3f109-134">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="3f109-135">部署完成後，請切換後 toohello 瀏覽器視窗開啟在 hello**瀏覽 toohello 應用程式**步驟，並重新整理 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="3f109-135">Once deployment has completed, switch back toohello browser window that opened in hello **Browse toohello app** step, and refresh hello page.</span></span>

![在 Azure 中執行的已更新範例應用程式](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="3f109-137">管理新的 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="3f109-137">Manage your new Azure web app</span></span>

<span data-ttu-id="3f109-138">移 toohello <a href="https://portal.azure.com" target="_blank">Azure 入口網站</a>toomanage hello web 應用程式所建立。</span><span class="sxs-lookup"><span data-stu-id="3f109-138">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="3f109-139">從 hello 左窗格中，按一下 **應用程式服務**，然後按一下hello Azure web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="3f109-139">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![入口網站瀏覽 tooAzure web 應用程式](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

<span data-ttu-id="3f109-141">您會看到 Web 應用程式的 [概觀] 頁面。</span><span class="sxs-lookup"><span data-stu-id="3f109-141">You see your web app's Overview page.</span></span> <span data-ttu-id="3f109-142">您可以在這裡執行基本管理工作，像是瀏覽、停止、啟動、重新啟動及刪除。</span><span class="sxs-lookup"><span data-stu-id="3f109-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span>

![Azure 入口網站中的 App Service 刀鋒視窗](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

<span data-ttu-id="3f109-144">hello 左側的功能表提供不同頁面設定您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3f109-144">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="3f109-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3f109-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3f109-146">PHP with MySQL</span><span class="sxs-lookup"><span data-stu-id="3f109-146">PHP with MySQL</span></span>](app-service-web-tutorial-php-mysql.md)
