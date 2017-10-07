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
# <a name="create-a-python-web-app-in-azure"></a>在 Azure 中建立 Python Web 應用程式

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 提供可高度擴充、自我修復的 Web 主機服務。  本快速入門逐步解說如何 toodevelop 和部署的 Python 應用程式 tooAzure Web 應用程式。 建立 hello web 應用程式使用 hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)，而且您使用 Git toodeploy 範例 Python 程式碼 toohello web 應用程式。

![在 Azure 中執行的範例應用程式](media/app-service-web-get-started-python/hello-world-in-browser.png)

您可以依照下列使用 Mac、 Windows 或 Linux 電腦的 hello 步驟。 一旦安裝 hello 必要條件，花費大約五分鐘 toocomplete hello 步驟。
## <a name="prerequisites"></a>必要條件

toocomplete 本教學課程：

1. [安裝 Git](https://git-scm.com/)
1. [安裝 Python](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="download-hello-sample"></a>下載 hello 範例

在終端機視窗中，執行下列命令 tooclone hello 範例應用程式儲存機制 tooyour 本機電腦的 hello。

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

您使用這個終端機視窗 toorun 所有 hello 命令本快速入門。

變更 toohello 目錄，包含 hello 範例程式碼。

```bash
cd Python-docs-hello-world
```

## <a name="run-hello-app-locally"></a>在本機執行 hello 應用程式

安裝所需的 hello 封裝使用`pip`。

```bash
pip install -r requirements.txt
```

在本機執行 hello 應用程式，開啟終端機視窗，並使用 hello`Python`命令 toolaunch hello 內建 Python web 伺服器。

```bash
python main.py
```

開啟網頁瀏覽器，並瀏覽在 http://localhost:5000/ toohello 範例應用程式。

您可以看到 hello **Hello World** hello 範例應用程式中 hello 頁面中所顯示的訊息。

![在本機執行的範例應用程式](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

在終端機視窗中，按**Ctrl + C** tooexit hello web 伺服器。

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![空的 Web 應用程式頁面](media/app-service-web-get-started-python/app-service-web-service-created.png)

您已在 Azure 中建立空的新 Web 應用程式。

## <a name="configure-toouse-python"></a>設定 toouse Python

使用 hello [az webapp 組態集](/cli/azure/webapp/config#set)命令 tooconfigure hello web 應用程式 toouse Python 版本`3.4`。

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


這種方式設定 hello Python 版本會使用 hello 平台所提供的預設容器。 toouse 您自己的容器，請參閱 hello hello 的 CLI 參考[az webapp config 容器 set](/cli/azure/webapp/config/container#set)命令。

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

## <a name="browse-toohello-app"></a>瀏覽 toohello 應用程式

瀏覽 toohello 部署使用網頁瀏覽器應用程式。

```bash
http://<app_name>.azurewebsites.net
```

hello Python 範例程式碼正在執行的 Azure App Service web 應用程式中。

![在 Azure 中執行的範例應用程式](media/app-service-web-get-started-python/hello-world-in-browser.png)

**恭喜！** 您已部署您第一次的 Python 應用程式 tooApp 服務。

## <a name="update-and-redeploy-hello-code"></a>更新和重新部署 hello 程式碼

使用本機的文字編輯器開啟 hello `main.py` hello Python 應用程式，在檔案並進行小幅變更 toohello 文字下一步 toohello`return`陳述式：

```python
return 'Hello, Azure!'
```

認可您在 Git 中的變更，並接著推送 hello 程式碼變更 tooAzure。

```bash
git commit -am "updated output"
git push azure master
```

部署完成後，請切換後 toohello 瀏覽器視窗開啟在 hello[瀏覽 toohello 應用程式](#browse-to-the-app)步驟，並重新整理 hello 頁面。

![在 Azure 中執行的已更新範例應用程式](media/app-service-web-get-started-python/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a>管理新的 Azure Web 應用程式

移 toohello <a href="https://portal.azure.com" target="_blank">Azure 入口網站</a>toomanage hello web 應用程式所建立。

從 hello 左窗格中，按一下 **應用程式服務**，然後按一下hello Azure web 應用程式名稱。

![入口網站瀏覽 tooAzure web 應用程式](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

您會看到 Web 應用程式的 [概觀] 頁面。 您可以在這裡執行基本管理工作，像是瀏覽、停止、啟動、重新啟動及刪除。 

![Azure 入口網站中的 App Service 刀鋒視窗](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

hello 左側的功能表提供不同頁面設定您的應用程式。 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [Python with PostgreSQL](app-service-web-tutorial-docker-python-postgresql-app.md)
