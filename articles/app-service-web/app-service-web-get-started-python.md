---
title: "在 Azure 中建立 Python Web 應用程式 | Microsoft"
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
ms.openlocfilehash: 119f9770097c010cc360e0e204d06a307a268814
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-python-web-app-in-azure"></a><span data-ttu-id="f50c5-103">在 Azure 中建立 Python Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="f50c5-103">Create a Python web app in Azure</span></span>

<span data-ttu-id="f50c5-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 提供可高度擴充、自我修復的 Web 主機服務。</span><span class="sxs-lookup"><span data-stu-id="f50c5-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="f50c5-105">本快速入門逐步解說如何開發 Python 應用程式及部署至 Azure Web Apps。</span><span class="sxs-lookup"><span data-stu-id="f50c5-105">This quickstart walks through how to develop and deploy a Python app to Azure Web Apps.</span></span> <span data-ttu-id="f50c5-106">您可使用 [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)建立 Web 應用程式，而且使用 Git 將範例 Python 程式碼部署至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f50c5-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy sample Python code to the web app.</span></span>

![在 Azure 中執行的範例應用程式](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="f50c5-108">您可以使用 Mac、Windows 或 Linux 電腦，依照下面步驟操作。</span><span class="sxs-lookup"><span data-stu-id="f50c5-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="f50c5-109">安裝先決條件後，大約需要 5 分鐘才能完成這些步驟。</span><span class="sxs-lookup"><span data-stu-id="f50c5-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>
## <a name="prerequisites"></a><span data-ttu-id="f50c5-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f50c5-110">Prerequisites</span></span>

<span data-ttu-id="f50c5-111">若要完成本教學課程：</span><span class="sxs-lookup"><span data-stu-id="f50c5-111">To complete this tutorial:</span></span>

1. [<span data-ttu-id="f50c5-112">安裝 Git</span><span class="sxs-lookup"><span data-stu-id="f50c5-112">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="f50c5-113">安裝 Python</span><span class="sxs-lookup"><span data-stu-id="f50c5-113">Install Python</span></span>](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f50c5-114">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="f50c5-114">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f50c5-115">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="f50c5-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="f50c5-116">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="f50c5-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-the-sample"></a><span data-ttu-id="f50c5-117">下載範例</span><span class="sxs-lookup"><span data-stu-id="f50c5-117">Download the sample</span></span>

<span data-ttu-id="f50c5-118">在終端機視窗中執行下列命令，將範例應用程式存放庫複製到本機電腦。</span><span class="sxs-lookup"><span data-stu-id="f50c5-118">In a terminal window, run the following command to clone the sample app repository to your local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

<span data-ttu-id="f50c5-119">您可使用這個終端機視窗來執行本快速入門中的所有命令。</span><span class="sxs-lookup"><span data-stu-id="f50c5-119">You use this terminal window to run all the commands in this quickstart.</span></span>

<span data-ttu-id="f50c5-120">變更為包含範例程式碼的目錄。</span><span class="sxs-lookup"><span data-stu-id="f50c5-120">Change to the directory that contains the sample code.</span></span>

```bash
cd Python-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="f50c5-121">在本機執行應用程式</span><span class="sxs-lookup"><span data-stu-id="f50c5-121">Run the app locally</span></span>

<span data-ttu-id="f50c5-122">使用 `pip` 安裝必要的套件。</span><span class="sxs-lookup"><span data-stu-id="f50c5-122">Install the required packages using `pip`.</span></span>

```bash
pip install -r requirements.txt
```

<span data-ttu-id="f50c5-123">開啟終端機視窗並使用 `Python` 命令來啟動內建 Python Web 伺服器，以在本機執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="f50c5-123">Run the application locally by opening a terminal window and using the `Python` command to launch the built-in Python web server.</span></span>

```bash
python main.py
```

<span data-ttu-id="f50c5-124">開啟網頁瀏覽器，然後瀏覽至範例應用程式 (位於 http://localhost:5000 )。</span><span class="sxs-lookup"><span data-stu-id="f50c5-124">Open a web browser, and navigate to the sample app at http://localhost:5000.</span></span>

<span data-ttu-id="f50c5-125">您可以看到來自範例應用程式的 **Hello World** 訊息顯示在網頁中。</span><span class="sxs-lookup"><span data-stu-id="f50c5-125">You can see the **Hello World** message from the sample app displayed in the page.</span></span>

![在本機執行的範例應用程式](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

<span data-ttu-id="f50c5-127">在終端機視窗中，按 **Ctrl+C** 結束 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f50c5-127">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

[!INCLUDE [Log in to Azure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![空的 Web 應用程式頁面](media/app-service-web-get-started-python/app-service-web-service-created.png)

<span data-ttu-id="f50c5-129">您已在 Azure 中建立空的新 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f50c5-129">You’ve created an empty new web app in Azure.</span></span>

## <a name="configure-to-use-python"></a><span data-ttu-id="f50c5-130">設定成使用 Python</span><span class="sxs-lookup"><span data-stu-id="f50c5-130">Configure to use Python</span></span>

<span data-ttu-id="f50c5-131">使用 [az webapp config set](/cli/azure/webapp/config#set) 命令將 Web 應用程式設定為使用 Python 版本 `3.4`。</span><span class="sxs-lookup"><span data-stu-id="f50c5-131">Use the [az webapp config set](/cli/azure/webapp/config#set) command to configure the web app to use Python version `3.4`.</span></span>

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


<span data-ttu-id="f50c5-132">以這種方式設定 Python 版本會使用平台所提供的預設容器。</span><span class="sxs-lookup"><span data-stu-id="f50c5-132">Setting the Python version this way uses a default container provided by the platform.</span></span> <span data-ttu-id="f50c5-133">若要使用自己的容器，請參閱 [az webapp config container set](/cli/azure/webapp/config/container#set) 命令的 CLI 參考。</span><span class="sxs-lookup"><span data-stu-id="f50c5-133">To use your own container, see the CLI reference for the [az webapp config container set](/cli/azure/webapp/config/container#set) command.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 18, done.
Delta compression using up to 4 threads.
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
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-to-the-app"></a><span data-ttu-id="f50c5-134">瀏覽至應用程式</span><span class="sxs-lookup"><span data-stu-id="f50c5-134">Browse to the app</span></span>

<span data-ttu-id="f50c5-135">使用 web 瀏覽器瀏覽至已部署的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f50c5-135">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="f50c5-136">Python 範例程式碼正在 Azure App Service Web 應用程式中執行。</span><span class="sxs-lookup"><span data-stu-id="f50c5-136">The Python sample code is running in an Azure App Service web app.</span></span>

![在 Azure 中執行的範例應用程式](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="f50c5-138">**恭喜！**</span><span class="sxs-lookup"><span data-stu-id="f50c5-138">**Congratulations!**</span></span> <span data-ttu-id="f50c5-139">您已將第一個 Python 應用程式部署至 App Service。</span><span class="sxs-lookup"><span data-stu-id="f50c5-139">You've deployed your first Python app to App Service.</span></span>

## <a name="update-and-redeploy-the-code"></a><span data-ttu-id="f50c5-140">更新和重新部署程式碼</span><span class="sxs-lookup"><span data-stu-id="f50c5-140">Update and redeploy the code</span></span>

<span data-ttu-id="f50c5-141">使用本機文字編輯器，在 Python 應用程式中開啟 `main.py` 檔案，並且對 `return` 陳述式旁邊的文字進行小幅變更：</span><span class="sxs-lookup"><span data-stu-id="f50c5-141">Using a local text editor, open the `main.py` file in the Python app, and make a small change to the text next to the `return` statement:</span></span>

```python
return 'Hello, Azure!'
```

<span data-ttu-id="f50c5-142">在 Git 中認可您的變更，然後將程式碼變更推送至 Azure。</span><span class="sxs-lookup"><span data-stu-id="f50c5-142">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="f50c5-143">部署完成後，切換回在[瀏覽至應用程式](#browse-to-the-app)步驟中開啟的瀏覽器視窗，然後重新整理頁面。</span><span class="sxs-lookup"><span data-stu-id="f50c5-143">Once deployment has completed, switch back to the browser window that opened in the [Browse to the app](#browse-to-the-app) step, and refresh the page.</span></span>

![在 Azure 中執行的已更新範例應用程式](media/app-service-web-get-started-python/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="f50c5-145">管理新的 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="f50c5-145">Manage your new Azure web app</span></span>

<span data-ttu-id="f50c5-146">請移至 <a href="https://portal.azure.com" target="_blank">Azure 入口網站</a>，以管理您所建立的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f50c5-146">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="f50c5-147">按一下左側功能表中的 [應用程式服務]，然後按一下 Azure Web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="f50c5-147">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![入口網站瀏覽至 Azure Web 應用程式](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="f50c5-149">您會看到 Web 應用程式的 [概觀] 頁面。</span><span class="sxs-lookup"><span data-stu-id="f50c5-149">You see your web app's Overview page.</span></span> <span data-ttu-id="f50c5-150">您可以在這裡執行基本管理工作，像是瀏覽、停止、啟動、重新啟動及刪除。</span><span class="sxs-lookup"><span data-stu-id="f50c5-150">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Azure 入口網站中的 App Service 刀鋒視窗](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="f50c5-152">左側功能表提供不同的頁面來設定您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f50c5-152">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="f50c5-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f50c5-153">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f50c5-154">Python with PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="f50c5-154">Python with PostgreSQL</span></span>](app-service-web-tutorial-docker-python-postgresql-app.md)
