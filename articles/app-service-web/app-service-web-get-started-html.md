---
title: "在 Azure 中的靜態 HTML aaaCreate web 應用程式 |Microsoft 文件"
description: "了解如何 toorun web 應用程式在 Azure App Service 中的部署靜態 HTML 的範例應用程式。"
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
ms.openlocfilehash: efd8c8189a3aa1ac35602b688eeb31bff6f5a373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-static-html-web-app-in-azure"></a>在 Azure 中建立靜態 HTML Web 應用程式

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 提供可高度擴充、自我修復的 Web 主機服務。  本快速入門示範如何 toodeploy 基本 HTML + CSS 站台 tooAzure Web 應用程式。 建立 hello web 應用程式使用 hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)，而且您使用 Git toodeploy 範例 HTML 內容 toohello web 應用程式。

![範例應用程式首頁](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

您可以依照下列使用 Mac、 Windows 或 Linux 電腦的 hello 步驟。 一旦安裝 hello 必要條件，花費大約五分鐘 toocomplete hello 步驟。

## <a name="prerequisites"></a>必要條件

toocomplete 本快速入門：

- [安裝 Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="download-hello-sample"></a>下載 hello 範例

在終端機視窗中，執行下列命令 tooclone hello 範例應用程式儲存機制 tooyour 本機電腦的 hello。

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

您使用這個終端機視窗 toorun 所有 hello 命令本快速入門。

## <a name="view-hello-html"></a>檢視 hello HTML

瀏覽包含 hello 範例 HTML toohello 目錄。 開啟 hello *index.html*瀏覽器中的檔案。

![範例應用程式首頁](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![空的 Web 應用程式頁面](media/app-service-web-get-started-html/app-service-web-service-created.png)

您已在 Azure 中建立空的新 Web 應用程式。

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up too4 threads.
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
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a>瀏覽 toohello 應用程式

在瀏覽器，移 toohello Azure web 應用程式 URL:

```
http://<app_name>.azurewebsites.net
```

hello 頁面 Azure App Service web 應用程式形式執行。

![範例應用程式首頁](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

**恭喜！** 您已部署您第一次的 HTML 應用程式 tooApp 服務。

## <a name="update-and-redeploy-hello-app"></a>更新和重新部署 hello 應用程式

開啟 hello *index.html*檔案在文字編輯器中，並製作變更 toohello 標記。 例如，變更 「 Azure 應用程式服務-範例靜態 HTML 網站 」 toojust hello H1 標題 「 Azure App Service'。

認可您在 Git 中的變更，並接著推送 hello 程式碼變更 tooAzure。

```bash
git commit -am "updated HTML"
git push azure master
```

部署完成後，請重新整理瀏覽器 toosee hello 做的變更。

![已更新的範例應用程式首頁](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a>管理新的 Azure Web 應用程式

移 toohello <a href="https://portal.azure.com" target="_blank">Azure 入口網站</a>toomanage hello web 應用程式所建立。

從 hello 左窗格中，按一下 **應用程式服務**，然後按一下hello Azure web 應用程式名稱。

![入口網站瀏覽 tooAzure web 應用程式](./media/app-service-web-get-started-html/portal1.png)

您會看到 Web 應用程式的 [概觀] 頁面。 您可以在這裡執行基本管理工作，像是瀏覽、停止、啟動、重新啟動及刪除。 

![Azure 入口網站中的 App Service 刀鋒視窗](./media/app-service-web-get-started-html/portal2.png)

hello 左側的功能表提供不同頁面設定您的應用程式。 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [對應自訂網域](app-service-web-tutorial-custom-domain.md)
