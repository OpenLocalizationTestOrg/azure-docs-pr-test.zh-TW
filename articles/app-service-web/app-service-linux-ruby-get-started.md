---
title: "aaaCreate Ruby 應用程式與 Linux 上的 Web 應用程式 |Microsoft 文件"
description: "了解 toocreate Ruby 使用 Azure web wpp on Linux 應用程式。"
keywords: azure app service, linux, oss
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 6d00c73c-13cb-446f-8926-923db4101afa
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: wesmc;rachelap
ms.openlocfilehash: 99ce3b5ee16703a147787387bb02973defce8190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a>使用 Linux 上的 Web Apps 建立 Ruby 應用程式 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 提供可高度擴充、自我修復的 Web 主機服務。 本快速入門示範如何 toocreate 滑軌應用程式上的基本 Ruby 您再將它部署為 Web 應用程式在 Linux 上 tooAzure。

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a>必要條件

* [Ruby 2.4.1 或更高版本](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller)。
* [Git](https://git-scm.com/downloads)。
* [有效的 Azure 訂用帳戶](https://azure.microsoft.com/pricing/free-trial/)。

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a>下載 hello 範例

在終端機視窗中，執行下列命令 tooclone hello 範例應用程式儲存機制 tooyour 本機電腦的 hello:

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-hello-application-locally"></a>在本機執行 hello 應用程式

為了讓 hello 應用程式 toowork 執行 hello 滑軌伺服器。 變更 toohello *hello world*目錄和 hello`rails server`啟動 hello 伺服器的命令。

```bash
cd hello-world\bin
rails server
```
    
使用網頁瀏覽器，巡覽太`http://localhost:3000`tootest hello 應用程式在本機。  

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-toodisplay-welcome-message"></a>修改應用程式 toodisplay 歡迎訊息

因此它會顯示歡迎訊息，請修改 hello 應用程式。 變更 hello 應用程式的控制站，以便傳回 hello 訊息和 HTML 的 toohello 瀏覽器。 

開啟 ~/workspace/hello-world/app/controllers/application_controller.rb 進行編輯。 修改 hello`ApplicationController`類別 toolook 類似下列程式碼範例的 hello:

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

現在已設定好您的應用程式。 使用網頁瀏覽器，巡覽太`http://localhost:3000`tooconfirm hello 根登陸頁面。

![已設定 Hello World](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a>在 Azure 上建立 Ruby Web 應用程式

使用 hello [az 應用程式服務方案建立](https://docs.microsoft.com/cli/azure/appservice/plan#create)命令 toocreate web 應用程式的應用程式服務方案。 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

接下來，發出 hello [az webapp 建立](https://docs.microsoft.com/cli/azure/webapp)命令 toocreate hello web 應用程式使用 hello 新建立的服務方案。 請注意該 hello 執行階段設定得`ruby|2.3`。 別忘了 tooreplace`<app name>`具有唯一的應用程式名稱。

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

一旦建立 hello web 應用程式，**概觀**頁面是可用 tooview。 瀏覽 tooit。 hello 下列開頭顯示頁面會顯示：

![啟動顯示畫面](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a>部署應用程式

使用 Git toodeploy hello Ruby 應用程式 tooAzure。 hello web 應用程式已經有 Git 部署，設定。 您可以藉由發出擷取 hello 部署 URL [az webapp 部署](https://docs.microsoft.com/cli/azure/webapp/deployment)命令。  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

請注意，hello Git URL 具有下列根據您的 web 應用程式名稱的 hello:

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

執行下列命令 toodeploy hello 本機應用程式 tooyour Azure 網站的 hello:

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

確認 hello 遠端部署作業報告成功。 hello 命令產生輸出類似 toohello 下列文字：

```bash
remote: Using sass-rails 5.0.6
remote: Updating files in vendor/cache
remote: Bundle gems are installed into ./vendor/bundle
remote: Updating files in vendor/cache
remote: ~site/repository
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<your web app name>.scm.azurewebsites.net/<your web app name>.git
  579ccb....2ca5f31  master -> master
myuser@ubuntu1234:~workspace/<app name>$
```

Hello 部署完成後，請使用重新啟動您的 web 應用程式，hello 部署 tootake 效果 hello [az webapp 重新啟動](https://docs.microsoft.com/cli/azure/webapp#restart)命令，如下所示：

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

瀏覽 tooyour 站台，並確認 hello 結果。

```bash
http://<your web app name>.azurewebsites.net
```
![更新的 Web 應用程式](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> Hello 應用程式正在重新啟動，嘗試 toobrowse hello 站台會導致 HTTP 狀態碼`Error 503 Server unavailable`。 可能需要幾分鐘的時間 toofully 重新啟動。
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a>後續步驟

[Linux 上的 Azure App Service Web 應用程式常見問題集](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)