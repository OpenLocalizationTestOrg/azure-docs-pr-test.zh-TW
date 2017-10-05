---
title: "使用 Linux 上的 Web Apps 建立 Ruby 應用程式 | Microsoft Docs"
description: "了解如何使用 Linux 上的 Azure Web 應用程式來建立 Ruby 應用程式。"
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
ms.openlocfilehash: 17f3f1a2122c508501134a0c43ab6abce412fb44
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a><span data-ttu-id="1fb55-104">使用 Linux 上的 Web Apps 建立 Ruby 應用程式</span><span class="sxs-lookup"><span data-stu-id="1fb55-104">Create a Ruby App with Web Apps on Linux</span></span> 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="1fb55-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) 提供可高度擴充、自我修復的 Web 主機服務。</span><span class="sxs-lookup"><span data-stu-id="1fb55-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="1fb55-106">本快速入門示範如何建立基本的 Ruby on Rails 應用程式，然後將它當作 Linux 上的 Web 應用程式部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="1fb55-106">This quickstart shows you how to create a basic Ruby on Rails application you then deploy it to Azure as a Web App on Linux.</span></span>

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a><span data-ttu-id="1fb55-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="1fb55-108">Prerequisites</span></span>

* <span data-ttu-id="1fb55-109">[Ruby 2.4.1 或更高版本](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller)。</span><span class="sxs-lookup"><span data-stu-id="1fb55-109">[Ruby 2.4.1 or higher](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span></span>
* <span data-ttu-id="1fb55-110">[Git](https://git-scm.com/downloads)。</span><span class="sxs-lookup"><span data-stu-id="1fb55-110">[Git](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="1fb55-111">[有效的 Azure 訂用帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="1fb55-111">An [active Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample"></a><span data-ttu-id="1fb55-112">下載範例</span><span class="sxs-lookup"><span data-stu-id="1fb55-112">Download the sample</span></span>

<span data-ttu-id="1fb55-113">在終端機視窗中執行下列命令，將範例應用程式存放庫複製到本機電腦：</span><span class="sxs-lookup"><span data-stu-id="1fb55-113">In a terminal window, run the following command to clone the sample app repository to your local machine:</span></span>

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-the-application-locally"></a><span data-ttu-id="1fb55-114">在本機執行應用程式</span><span class="sxs-lookup"><span data-stu-id="1fb55-114">Run the application locally</span></span>

<span data-ttu-id="1fb55-115">執行 Rails 伺服器，讓應用程式得以運作。</span><span class="sxs-lookup"><span data-stu-id="1fb55-115">Run the rails server in order for the application to work.</span></span> <span data-ttu-id="1fb55-116">變更為 hello-world 目錄，然後 `rails server` 命令會啟動伺服器。</span><span class="sxs-lookup"><span data-stu-id="1fb55-116">Change to the *hello-world* directory, and the `rails server` command starts the server.</span></span>

```bash
cd hello-world\bin
rails server
```
    
<span data-ttu-id="1fb55-117">使用網頁瀏覽器，瀏覽至 `http://localhost:3000`，在本機測試應用程式。</span><span class="sxs-lookup"><span data-stu-id="1fb55-117">Using your web browser, navigate to `http://localhost:3000` to test the app locally.</span></span>    

![Hello-world](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-to-display-welcome-message"></a><span data-ttu-id="1fb55-119">修改應用程式以顯示歡迎使用訊息</span><span class="sxs-lookup"><span data-stu-id="1fb55-119">Modify app to display welcome message</span></span>

<span data-ttu-id="1fb55-120">修改應用程式，使其顯示歡迎使用訊息。</span><span class="sxs-lookup"><span data-stu-id="1fb55-120">Modify the application so it displays a welcome message.</span></span> <span data-ttu-id="1fb55-121">變更應用程式的控制站，使其將訊息當作 HTML 傳回至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="1fb55-121">Change the application's controller so it returns the message as HTML to the browser.</span></span> 

<span data-ttu-id="1fb55-122">開啟 ~/workspace/hello-world/app/controllers/application_controller.rb 進行編輯。</span><span class="sxs-lookup"><span data-stu-id="1fb55-122">Open *~/workspace/hello-world/app/controllers/application_controller.rb* for editing.</span></span> <span data-ttu-id="1fb55-123">修改 `ApplicationController` 類型，使其看起來類似下列程式碼範例：</span><span class="sxs-lookup"><span data-stu-id="1fb55-123">Modify the `ApplicationController` class to look like the following code sample:</span></span>

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

<span data-ttu-id="1fb55-124">現在已設定好您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1fb55-124">Your app is now configured.</span></span> <span data-ttu-id="1fb55-125">使用網頁瀏覽器，瀏覽至 `http://localhost:3000`，確認根登陸頁面。</span><span class="sxs-lookup"><span data-stu-id="1fb55-125">Using your web browser, navigate to `http://localhost:3000` to confirm the root landing page.</span></span>

![已設定 Hello World](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a><span data-ttu-id="1fb55-127">在 Azure 上建立 Ruby Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="1fb55-127">Create a Ruby web app on Azure</span></span>

<span data-ttu-id="1fb55-128">使用 [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) 命令，建立 Web 應用程式的應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="1fb55-128">Use the [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) command to create an app service plan for your web app.</span></span> 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

<span data-ttu-id="1fb55-129">接下來，發出 [az webapp create](https://docs.microsoft.com/cli/azure/webapp) 命令以建立使用新建服務方案的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1fb55-129">Next, issue the [az webapp create](https://docs.microsoft.com/cli/azure/webapp) command to create the web app that uses the newly created service plan.</span></span> <span data-ttu-id="1fb55-130">請注意，執行階段設定為 `ruby|2.3`。</span><span class="sxs-lookup"><span data-stu-id="1fb55-130">Notice that the runtime is set to `ruby|2.3`.</span></span> <span data-ttu-id="1fb55-131">別忘了以唯一的應用程式名稱取代 `<app name>`。</span><span class="sxs-lookup"><span data-stu-id="1fb55-131">Don't forget to replace `<app name>` with a unique app name.</span></span>

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

<span data-ttu-id="1fb55-132">建立 Web 應用程式後，[概觀] 頁面即可供檢視。</span><span class="sxs-lookup"><span data-stu-id="1fb55-132">Once the web app is created, an **Overview** page is available to view.</span></span> <span data-ttu-id="1fb55-133">瀏覽到該頁面。</span><span class="sxs-lookup"><span data-stu-id="1fb55-133">Navigate to it.</span></span> <span data-ttu-id="1fb55-134">隨即出現下列啟動顯示畫面：</span><span class="sxs-lookup"><span data-stu-id="1fb55-134">The following splash page is displayed:</span></span>

![啟動顯示畫面](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a><span data-ttu-id="1fb55-136">部署應用程式</span><span class="sxs-lookup"><span data-stu-id="1fb55-136">Deploy your application</span></span>

<span data-ttu-id="1fb55-137">使用 Git 將 Ruby 應用程式部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="1fb55-137">Use Git to deploy the Ruby application to Azure.</span></span> <span data-ttu-id="1fb55-138">Web 應用程式已設定 Git 部署。</span><span class="sxs-lookup"><span data-stu-id="1fb55-138">The web app already has a Git deployment configured.</span></span> <span data-ttu-id="1fb55-139">您可以藉由發出 [az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment) 命令來擷取部署 URL。</span><span class="sxs-lookup"><span data-stu-id="1fb55-139">You can retrieve the deployment URL by issuing an [az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment) command.</span></span>  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="1fb55-140">請注意，根據您的 web 應用程式名稱，Git URL 具有下列格式︰</span><span class="sxs-lookup"><span data-stu-id="1fb55-140">Notice that the Git URL has the following form based on your web app name:</span></span>

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

<span data-ttu-id="1fb55-141">執行下列命令，將本機應用程式部署至您的 Azure 網站：</span><span class="sxs-lookup"><span data-stu-id="1fb55-141">Run the following commands to deploy the local application to your Azure website:</span></span>

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="1fb55-142">確認遠端部署作業報告成功。</span><span class="sxs-lookup"><span data-stu-id="1fb55-142">Confirm that the remote deployment operations report success.</span></span> <span data-ttu-id="1fb55-143">此命令會產生類似下列文字的輸出：</span><span class="sxs-lookup"><span data-stu-id="1fb55-143">The commands produce output similar to the following text:</span></span>

```bash
remote: Using sass-rails 5.0.6
remote: Updating files in vendor/cache
remote: Bundle gems are installed into ./vendor/bundle
remote: Updating files in vendor/cache
remote: ~site/repository
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
  579ccb....2ca5f31  master -> master
myuser@ubuntu1234:~workspace/<app name>$
```

<span data-ttu-id="1fb55-144">一旦部署完成後，使用 [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart) 命令來重新啟動 Web 應用程式，部署才會生效，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1fb55-144">Once the deployment has completed, restart your web app for the deployment to take effect by using the [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart) command, as shown here:</span></span>

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="1fb55-145">瀏覽至您的網站並確認結果。</span><span class="sxs-lookup"><span data-stu-id="1fb55-145">Navigate to your site and verify the results.</span></span>

```bash
http://<your web app name>.azurewebsites.net
```
![更新的 Web 應用程式](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> <span data-ttu-id="1fb55-147">當應用程式重新啟動時，嘗試瀏覽網站會導致 HTTP 狀態碼 `Error 503 Server unavailable`。</span><span class="sxs-lookup"><span data-stu-id="1fb55-147">While the app is restarting, attempting to browse the site results in an HTTP status code `Error 503 Server unavailable`.</span></span> <span data-ttu-id="1fb55-148">可能需要幾分鐘才能完全重新啟動。</span><span class="sxs-lookup"><span data-stu-id="1fb55-148">It may take a few minutes to fully restart.</span></span>
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a><span data-ttu-id="1fb55-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1fb55-149">Next steps</span></span>

[<span data-ttu-id="1fb55-150">Linux 上的 Azure App Service Web 應用程式常見問題集</span><span class="sxs-lookup"><span data-stu-id="1fb55-150">Azure App Service Web App on Linux FAQ</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)