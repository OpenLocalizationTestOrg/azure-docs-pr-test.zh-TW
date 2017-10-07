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
# <a name="create-a-php-web-app-in-azure"></a>在 Azure 中建立 PHP Web 應用程式

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 提供可高度擴充、自我修復的 Web 主機服務。  本快速入門教學課程示範如何 toodeploy PHP 應用程式 tooAzure Web 應用程式。 建立 hello web 應用程式使用 hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)在雲端 Shell 中，而且您使用 Git toodeploy 範例 PHP 程式碼 toohello web 應用程式。

![在 Azure 中執行的範例應用程式]](media/app-service-web-get-started-php/hello-world-in-browser.png)

您可以依照下列使用 Mac、 Windows 或 Linux 電腦的 hello 步驟。 一旦安裝 hello 必要條件，花費大約五分鐘 toocomplete hello 步驟。

## <a name="prerequisites"></a>必要條件

toocomplete 本快速入門：

* [安裝 Git](https://git-scm.com/)
* [安裝 PHP](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample-locally"></a>下載本機 hello 範例

在終端機視窗中，執行下列命令的 hello。 這將會複製 hello 範例應用程式 tooyour 本機電腦，並瀏覽 toohello 目錄包含 hello 範例程式碼。

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-hello-app-locally"></a>在本機執行 hello 應用程式

在本機執行 hello 應用程式，開啟終端機視窗，並使用 hello`php`命令 toolaunch hello 內建 PHP web 伺服器。

```bash
php -S localhost:8080
```

開啟網頁瀏覽器，並瀏覽 http://localhost:8080/< toohello 範例應用程式。

您會看到 hello **Hello World ！** hello 範例應用程式中 hello 頁面中所顯示的訊息。

![在本機執行的範例應用程式](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

在終端機視窗中，按**Ctrl + C** tooexit hello web 伺服器。

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![空的 Web 應用程式頁面](media/app-service-web-get-started-php/app-service-web-service-created.png)

您已在 Azure 中建立空的新 Web 應用程式。

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

## <a name="browse-toohello-app-locally"></a>瀏覽本機 toohello 應用程式

瀏覽 toohello 部署使用網頁瀏覽器應用程式。

```bash
http://<app_name>.azurewebsites.net
```

hello PHP 範例程式碼正在執行的 Azure App Service web 應用程式中。

![在 Azure 中執行的範例應用程式](media/app-service-web-get-started-php/hello-world-in-browser.png)

**恭喜！** 您已部署您第一次的 PHP 應用程式 tooApp 服務。

## <a name="update-locally-and-redeploy-hello-code"></a>在本機更新和重新部署 hello 程式碼

使用本機的文字編輯器開啟 hello `index.php` hello PHP 應用程式中的檔案，並進行小幅變更 toohello 內的文字字串 hello 接下來太`echo`:

```php
echo "Hello Azure!";
```

認可您在 Git 中的變更，並接著推送 hello 程式碼變更 tooAzure。

```bash
git commit -am "updated output"
git push azure master
```

部署完成後，請切換後 toohello 瀏覽器視窗開啟在 hello**瀏覽 toohello 應用程式**步驟，並重新整理 hello 頁面。

![在 Azure 中執行的已更新範例應用程式](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a>管理新的 Azure Web 應用程式

移 toohello <a href="https://portal.azure.com" target="_blank">Azure 入口網站</a>toomanage hello web 應用程式所建立。

從 hello 左窗格中，按一下 **應用程式服務**，然後按一下hello Azure web 應用程式名稱。

![入口網站瀏覽 tooAzure web 應用程式](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

您會看到 Web 應用程式的 [概觀] 頁面。 您可以在這裡執行基本管理工作，像是瀏覽、停止、啟動、重新啟動及刪除。

![Azure 入口網站中的 App Service 刀鋒視窗](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

hello 左側的功能表提供不同頁面設定您的應用程式。 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>後續步驟

> [!div class="nextstepaction"]
> [PHP with MySQL](app-service-web-tutorial-php-mysql.md)
