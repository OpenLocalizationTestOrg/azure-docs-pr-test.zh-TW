---
title: "aaaCreate Python web 應用程式在 Azure 中 |Microsoft 文件"
description: "短短幾分鐘內在 Azure App Service Web 應用程式中部署第一個 Python Hello World。"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 928ee2e5-6143-4c0c-8546-366f5a3d80ce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 03/17/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 42178d490d8aa8eaf93710667aad598794c62c8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-python-web-app-in-azure"></a><span data-ttu-id="96262-103">在 Azure 中建立 Python Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="96262-103">Create a Python web app in Azure</span></span>

<span data-ttu-id="96262-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 提供可高度擴充、自我修復的 Web 主機服務。</span><span class="sxs-lookup"><span data-stu-id="96262-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="96262-105">本快速入門逐步解說如何 toodevelop 和部署的 Python 應用程式 tooAzure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="96262-105">This quickstart walks through how toodevelop and deploy a Python app tooAzure Web Apps.</span></span> <span data-ttu-id="96262-106">建立 hello web 應用程式使用 hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)，而且您使用 Git toodeploy 範例 Python 程式碼 toohello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="96262-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample Python code toohello web app.</span></span>

![在 Azure 中執行的範例應用程式](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="96262-108">您可以依照下列使用 Mac、 Windows 或 Linux 電腦的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="96262-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="96262-109">一旦安裝 hello 必要條件，花費大約五分鐘 toocomplete hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="96262-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>
## <a name="prerequisites"></a><span data-ttu-id="96262-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="96262-110">Prerequisites</span></span>

<span data-ttu-id="96262-111">toocomplete 本教學課程：</span><span class="sxs-lookup"><span data-stu-id="96262-111">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="96262-112">安裝 Git</span><span class="sxs-lookup"><span data-stu-id="96262-112">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="96262-113">安裝 Python</span><span class="sxs-lookup"><span data-stu-id="96262-113">Install Python</span></span>](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="96262-114">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="96262-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="96262-115">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="96262-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="96262-116">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="96262-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="96262-117">下載 hello 範例</span><span class="sxs-lookup"><span data-stu-id="96262-117">Download hello sample</span></span>

<span data-ttu-id="96262-118">在終端機視窗中，執行下列命令 tooclone hello 範例應用程式儲存機制 tooyour 本機電腦的 hello。</span><span class="sxs-lookup"><span data-stu-id="96262-118">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

<span data-ttu-id="96262-119">您使用這個終端機視窗 toorun 所有 hello 命令本快速入門。</span><span class="sxs-lookup"><span data-stu-id="96262-119">You use this terminal window toorun all hello commands in this quickstart.</span></span>

<span data-ttu-id="96262-120">變更 toohello 目錄，包含 hello 範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="96262-120">Change toohello directory that contains hello sample code.</span></span>

```bash
cd Python-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="96262-121">在本機執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="96262-121">Run hello app locally</span></span>

<span data-ttu-id="96262-122">安裝所需的 hello 封裝使用`pip`。</span><span class="sxs-lookup"><span data-stu-id="96262-122">Install hello required packages using `pip`.</span></span>

```bash
pip install -r requirements.txt
```

<span data-ttu-id="96262-123">在本機執行 hello 應用程式，開啟終端機視窗，並使用 hello`Python`命令 toolaunch hello 內建 Python web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="96262-123">Run hello application locally by opening a terminal window and using hello `Python` command toolaunch hello built-in Python web server.</span></span>

```bash
python main.py
```

<span data-ttu-id="96262-124">開啟網頁瀏覽器，並瀏覽在 http://localhost:5000/ toohello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="96262-124">Open a web browser, and navigate toohello sample app at http://localhost:5000.</span></span>

<span data-ttu-id="96262-125">您可以看到 hello **Hello World** hello 範例應用程式中 hello 頁面中所顯示的訊息。</span><span class="sxs-lookup"><span data-stu-id="96262-125">You can see hello **Hello World** message from hello sample app displayed in hello page.</span></span>

![在本機執行的範例應用程式](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

<span data-ttu-id="96262-127">在終端機視窗中，按**Ctrl + C** tooexit hello web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="96262-127">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![空的 Web 應用程式頁面](media/app-service-web-get-started-python/app-service-web-service-created.png)

<span data-ttu-id="96262-129">您已在 Azure 中建立空的新 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="96262-129">You’ve created an empty new web app in Azure.</span></span>

## <a name="configure-toouse-python"></a><span data-ttu-id="96262-130">設定 toouse Python</span><span class="sxs-lookup"><span data-stu-id="96262-130">Configure toouse Python</span></span>

<span data-ttu-id="96262-131">使用 hello [az webapp 組態集](/cli/azure/webapp/config#set)命令 tooconfigure hello web 應用程式 toouse Python 版本`3.4`。</span><span class="sxs-lookup"><span data-stu-id="96262-131">Use hello [az webapp config set](/cli/azure/webapp/config#set) command tooconfigure hello web app toouse Python version `3.4`.</span></span>

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


<span data-ttu-id="96262-132">這種方式設定 hello Python 版本會使用 hello 平台所提供的預設容器。</span><span class="sxs-lookup"><span data-stu-id="96262-132">Setting hello Python version this way uses a default container provided by hello platform.</span></span> <span data-ttu-id="96262-133">toouse 您自己的容器，請參閱 hello hello 的 CLI 參考[az webapp config 容器 set](/cli/azure/webapp/config/container#set)命令。</span><span class="sxs-lookup"><span data-stu-id="96262-133">toouse your own container, see hello CLI reference for hello [az webapp config container set](/cli/azure/webapp/config/container#set) command.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 18, done.
Delta compression using up too4 threads.
Compressing objects: 100% (16/16), done.
Writing objects: 100% (18/18), 4.31 KiB | 0 bytes/s, done.
Total 18 (delta 4), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '44e74fe7dd'.
remote: Generating deployment script.
remote: Generating deployment script for python Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling python deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'main.py'
remote: Copying file: 'README.md'
remote: Copying file: 'requirements.txt'
remote: Copying file: 'virtualenv_proxy.py'
remote: Copying file: 'web.2.7.config'
remote: Copying file: 'web.3.4.config'
remote: Detected requirements.txt.  You can skip Python specific steps with a .skipPythonDeployment file.
remote: Detecting Python runtime from site configuration
remote: Detected python-3.4
remote: Creating python-3.4 virtual environment.
remote: .................................
remote: Pip install requirements.
remote: Successfully installed Flask click itsdangerous Jinja2 Werkzeug MarkupSafe
remote: Cleaning up...
remote: .
remote: Overwriting web.config with web.3.4.config
remote:         1 file(s) copied.
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="96262-134">瀏覽 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="96262-134">Browse toohello app</span></span>

<span data-ttu-id="96262-135">瀏覽 toohello 部署使用網頁瀏覽器應用程式。</span><span class="sxs-lookup"><span data-stu-id="96262-135">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="96262-136">hello Python 範例程式碼正在執行的 Azure App Service web 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="96262-136">hello Python sample code is running in an Azure App Service web app.</span></span>

![在 Azure 中執行的範例應用程式](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="96262-138">**恭喜！**</span><span class="sxs-lookup"><span data-stu-id="96262-138">**Congratulations!**</span></span> <span data-ttu-id="96262-139">您已部署您第一次的 Python 應用程式 tooApp 服務。</span><span class="sxs-lookup"><span data-stu-id="96262-139">You've deployed your first Python app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-code"></a><span data-ttu-id="96262-140">更新和重新部署 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="96262-140">Update and redeploy hello code</span></span>

<span data-ttu-id="96262-141">使用本機的文字編輯器開啟 hello `main.py` hello Python 應用程式，在檔案並進行小幅變更 toohello 文字下一步 toohello`return`陳述式：</span><span class="sxs-lookup"><span data-stu-id="96262-141">Using a local text editor, open hello `main.py` file in hello Python app, and make a small change toohello text next toohello `return` statement:</span></span>

```python
return 'Hello, Azure!'
```

<span data-ttu-id="96262-142">認可您在 Git 中的變更，並接著推送 hello 程式碼變更 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="96262-142">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="96262-143">部署完成後，請切換後 toohello 瀏覽器視窗開啟在 hello[瀏覽 toohello 應用程式](#browse-to-the-app)步驟，並重新整理 hello 頁面。</span><span class="sxs-lookup"><span data-stu-id="96262-143">Once deployment has completed, switch back toohello browser window that opened in hello [Browse toohello app](#browse-to-the-app) step, and refresh hello page.</span></span>

![在 Azure 中執行的已更新範例應用程式](media/app-service-web-get-started-python/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="96262-145">管理新的 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="96262-145">Manage your new Azure web app</span></span>

<span data-ttu-id="96262-146">移 toohello <a href="https://portal.azure.com" target="_blank">Azure 入口網站</a>toomanage hello web 應用程式所建立。</span><span class="sxs-lookup"><span data-stu-id="96262-146">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="96262-147">從 hello 左窗格中，按一下 **應用程式服務**，然後按一下hello Azure web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="96262-147">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![入口網站瀏覽 tooAzure web 應用程式](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="96262-149">您會看到 Web 應用程式的 [概觀] 頁面。</span><span class="sxs-lookup"><span data-stu-id="96262-149">You see your web app's Overview page.</span></span> <span data-ttu-id="96262-150">您可以在這裡執行基本管理工作，像是瀏覽、停止、啟動、重新啟動及刪除。</span><span class="sxs-lookup"><span data-stu-id="96262-150">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Azure 入口網站中的 App Service 刀鋒視窗](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="96262-152">hello 左側的功能表提供不同頁面設定您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="96262-152">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="96262-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="96262-153">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="96262-154">Python with PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="96262-154">Python with PostgreSQL</span></span>](app-service-web-tutorial-docker-python-postgresql-app.md)
