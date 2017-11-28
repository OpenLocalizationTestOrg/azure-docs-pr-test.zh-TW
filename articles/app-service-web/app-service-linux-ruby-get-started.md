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
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a><span data-ttu-id="9bf89-104">使用 Linux 上的 Web Apps 建立 Ruby 應用程式</span><span class="sxs-lookup"><span data-stu-id="9bf89-104">Create a Ruby App with Web Apps on Linux</span></span> 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="9bf89-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 提供可高度擴充、自我修復的 Web 主機服務。</span><span class="sxs-lookup"><span data-stu-id="9bf89-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="9bf89-106">本快速入門示範如何 toocreate 滑軌應用程式上的基本 Ruby 您再將它部署為 Web 應用程式在 Linux 上 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="9bf89-106">This quickstart shows you how toocreate a basic Ruby on Rails application you then deploy it tooAzure as a Web App on Linux.</span></span>

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a><span data-ttu-id="9bf89-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="9bf89-108">Prerequisites</span></span>

* <span data-ttu-id="9bf89-109">[Ruby 2.4.1 或更高版本](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller)。</span><span class="sxs-lookup"><span data-stu-id="9bf89-109">[Ruby 2.4.1 or higher](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span></span>
* <span data-ttu-id="9bf89-110">[Git](https://git-scm.com/downloads)。</span><span class="sxs-lookup"><span data-stu-id="9bf89-110">[Git](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="9bf89-111">[有效的 Azure 訂用帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="9bf89-111">An [active Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a><span data-ttu-id="9bf89-112">下載 hello 範例</span><span class="sxs-lookup"><span data-stu-id="9bf89-112">Download hello sample</span></span>

<span data-ttu-id="9bf89-113">在終端機視窗中，執行下列命令 tooclone hello 範例應用程式儲存機制 tooyour 本機電腦的 hello:</span><span class="sxs-lookup"><span data-stu-id="9bf89-113">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine:</span></span>

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-hello-application-locally"></a><span data-ttu-id="9bf89-114">在本機執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="9bf89-114">Run hello application locally</span></span>

<span data-ttu-id="9bf89-115">為了讓 hello 應用程式 toowork 執行 hello 滑軌伺服器。</span><span class="sxs-lookup"><span data-stu-id="9bf89-115">Run hello rails server in order for hello application toowork.</span></span> <span data-ttu-id="9bf89-116">變更 toohello *hello world*目錄和 hello`rails server`啟動 hello 伺服器的命令。</span><span class="sxs-lookup"><span data-stu-id="9bf89-116">Change toohello *hello-world* directory, and hello `rails server` command starts hello server.</span></span>

```bash
cd hello-world\bin
rails server
```
    
<span data-ttu-id="9bf89-117">使用網頁瀏覽器，巡覽太`http://localhost:3000`tootest hello 應用程式在本機。</span><span class="sxs-lookup"><span data-stu-id="9bf89-117">Using your web browser, navigate too`http://localhost:3000` tootest hello app locally.</span></span>  

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-toodisplay-welcome-message"></a><span data-ttu-id="9bf89-119">修改應用程式 toodisplay 歡迎訊息</span><span class="sxs-lookup"><span data-stu-id="9bf89-119">Modify app toodisplay welcome message</span></span>

<span data-ttu-id="9bf89-120">因此它會顯示歡迎訊息，請修改 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9bf89-120">Modify hello application so it displays a welcome message.</span></span> <span data-ttu-id="9bf89-121">變更 hello 應用程式的控制站，以便傳回 hello 訊息和 HTML 的 toohello 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="9bf89-121">Change hello application's controller so it returns hello message as HTML toohello browser.</span></span> 

<span data-ttu-id="9bf89-122">開啟 ~/workspace/hello-world/app/controllers/application_controller.rb 進行編輯。</span><span class="sxs-lookup"><span data-stu-id="9bf89-122">Open *~/workspace/hello-world/app/controllers/application_controller.rb* for editing.</span></span> <span data-ttu-id="9bf89-123">修改 hello`ApplicationController`類別 toolook 類似下列程式碼範例的 hello:</span><span class="sxs-lookup"><span data-stu-id="9bf89-123">Modify hello `ApplicationController` class toolook like hello following code sample:</span></span>

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

<span data-ttu-id="9bf89-124">現在已設定好您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9bf89-124">Your app is now configured.</span></span> <span data-ttu-id="9bf89-125">使用網頁瀏覽器，巡覽太`http://localhost:3000`tooconfirm hello 根登陸頁面。</span><span class="sxs-lookup"><span data-stu-id="9bf89-125">Using your web browser, navigate too`http://localhost:3000` tooconfirm hello root landing page.</span></span>

![已設定 Hello World](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a><span data-ttu-id="9bf89-127">在 Azure 上建立 Ruby Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9bf89-127">Create a Ruby web app on Azure</span></span>

<span data-ttu-id="9bf89-128">使用 hello [az 應用程式服務方案建立](https://docs.microsoft.com/cli/azure/appservice/plan#create)命令 toocreate web 應用程式的應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="9bf89-128">Use hello [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) command toocreate an app service plan for your web app.</span></span> 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

<span data-ttu-id="9bf89-129">接下來，發出 hello [az webapp 建立](https://docs.microsoft.com/cli/azure/webapp)命令 toocreate hello web 應用程式使用 hello 新建立的服務方案。</span><span class="sxs-lookup"><span data-stu-id="9bf89-129">Next, issue hello [az webapp create](https://docs.microsoft.com/cli/azure/webapp) command toocreate hello web app that uses hello newly created service plan.</span></span> <span data-ttu-id="9bf89-130">請注意該 hello 執行階段設定得`ruby|2.3`。</span><span class="sxs-lookup"><span data-stu-id="9bf89-130">Notice that hello runtime is set too`ruby|2.3`.</span></span> <span data-ttu-id="9bf89-131">別忘了 tooreplace`<app name>`具有唯一的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="9bf89-131">Don't forget tooreplace `<app name>` with a unique app name.</span></span>

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

<span data-ttu-id="9bf89-132">一旦建立 hello web 應用程式，**概觀**頁面是可用 tooview。</span><span class="sxs-lookup"><span data-stu-id="9bf89-132">Once hello web app is created, an **Overview** page is available tooview.</span></span> <span data-ttu-id="9bf89-133">瀏覽 tooit。</span><span class="sxs-lookup"><span data-stu-id="9bf89-133">Navigate tooit.</span></span> <span data-ttu-id="9bf89-134">hello 下列開頭顯示頁面會顯示：</span><span class="sxs-lookup"><span data-stu-id="9bf89-134">hello following splash page is displayed:</span></span>

![啟動顯示畫面](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a><span data-ttu-id="9bf89-136">部署應用程式</span><span class="sxs-lookup"><span data-stu-id="9bf89-136">Deploy your application</span></span>

<span data-ttu-id="9bf89-137">使用 Git toodeploy hello Ruby 應用程式 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="9bf89-137">Use Git toodeploy hello Ruby application tooAzure.</span></span> <span data-ttu-id="9bf89-138">hello web 應用程式已經有 Git 部署，設定。</span><span class="sxs-lookup"><span data-stu-id="9bf89-138">hello web app already has a Git deployment configured.</span></span> <span data-ttu-id="9bf89-139">您可以藉由發出擷取 hello 部署 URL [az webapp 部署](https://docs.microsoft.com/cli/azure/webapp/deployment)命令。</span><span class="sxs-lookup"><span data-stu-id="9bf89-139">You can retrieve hello deployment URL by issuing an [az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment) command.</span></span>  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="9bf89-140">請注意，hello Git URL 具有下列根據您的 web 應用程式名稱的 hello:</span><span class="sxs-lookup"><span data-stu-id="9bf89-140">Notice that hello Git URL has hello following form based on your web app name:</span></span>

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

<span data-ttu-id="9bf89-141">執行下列命令 toodeploy hello 本機應用程式 tooyour Azure 網站的 hello:</span><span class="sxs-lookup"><span data-stu-id="9bf89-141">Run hello following commands toodeploy hello local application tooyour Azure website:</span></span>

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="9bf89-142">確認 hello 遠端部署作業報告成功。</span><span class="sxs-lookup"><span data-stu-id="9bf89-142">Confirm that hello remote deployment operations report success.</span></span> <span data-ttu-id="9bf89-143">hello 命令產生輸出類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="9bf89-143">hello commands produce output similar toohello following text:</span></span>

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

<span data-ttu-id="9bf89-144">Hello 部署完成後，請使用重新啟動您的 web 應用程式，hello 部署 tootake 效果 hello [az webapp 重新啟動](https://docs.microsoft.com/cli/azure/webapp#restart)命令，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9bf89-144">Once hello deployment has completed, restart your web app for hello deployment tootake effect by using hello [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart) command, as shown here:</span></span>

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="9bf89-145">瀏覽 tooyour 站台，並確認 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="9bf89-145">Navigate tooyour site and verify hello results.</span></span>

```bash
http://<your web app name>.azurewebsites.net
```
![更新的 Web 應用程式](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> <span data-ttu-id="9bf89-147">Hello 應用程式正在重新啟動，嘗試 toobrowse hello 站台會導致 HTTP 狀態碼`Error 503 Server unavailable`。</span><span class="sxs-lookup"><span data-stu-id="9bf89-147">While hello app is restarting, attempting toobrowse hello site results in an HTTP status code `Error 503 Server unavailable`.</span></span> <span data-ttu-id="9bf89-148">可能需要幾分鐘的時間 toofully 重新啟動。</span><span class="sxs-lookup"><span data-stu-id="9bf89-148">It may take a few minutes toofully restart.</span></span>
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a><span data-ttu-id="9bf89-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9bf89-149">Next steps</span></span>

[<span data-ttu-id="9bf89-150">Linux 上的 Azure App Service Web 應用程式常見問題集</span><span class="sxs-lookup"><span data-stu-id="9bf89-150">Azure App Service Web App on Linux FAQ</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)