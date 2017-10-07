---
title: "aaaDeploy Sails.js web 應用程式 tooAzure 應用程式服務 |Microsoft 文件"
description: "深入了解如何 toodeploy Node.js 應用程式的 Azure 應用程式服務。 本教學課程會示範如何 toodeploy Sails.js web 應用程式。"
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 8877ddc8-1476-45ae-9e7f-3c75917b4564
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: f5b2518b9c87c040845f7268763862be8c15e83e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-sailsjs-web-app-tooazure-app-service"></a><span data-ttu-id="1b865-104">部署 Sails.js web 應用程式 tooAzure 應用程式服務</span><span class="sxs-lookup"><span data-stu-id="1b865-104">Deploy a Sails.js web app tooAzure App Service</span></span>
<span data-ttu-id="1b865-105">本教學課程示範如何 toodeploy Sails.js 應用程式 tooAzure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="1b865-105">This tutorial shows you how toodeploy a Sails.js app tooAzure App Service.</span></span> <span data-ttu-id="1b865-106">您可以在 hello 過程中，搜集一些有關的一般知識 tooconfigure 您 App Service 中的 Node.js 應用程式 toorun。</span><span class="sxs-lookup"><span data-stu-id="1b865-106">In hello process, you can glean some general knowledge on how tooconfigure your Node.js app toorun in App Service.</span></span>

<span data-ttu-id="1b865-107">在這裡，您將學習有用的技能，例如︰</span><span class="sxs-lookup"><span data-stu-id="1b865-107">Here, you will learn useful skills like:</span></span>

* <span data-ttu-id="1b865-108">設定在 App Service 中執行 Sails.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b865-108">Configure a Sails.js app run in App Service.</span></span>
* <span data-ttu-id="1b865-109">部署應用程式 tooApp 服務從 hello 命令列。</span><span class="sxs-lookup"><span data-stu-id="1b865-109">Deploy an app tooApp Service from hello command line.</span></span>
* <span data-ttu-id="1b865-110">讀取的 stderr 和 stdout 記錄 tootroubleshoot 任何部署的問題。</span><span class="sxs-lookup"><span data-stu-id="1b865-110">Read stderr and stdout logs tootroubleshoot any deployment issues.</span></span>
* <span data-ttu-id="1b865-111">儲存原始檔控制外部的環境變數。</span><span class="sxs-lookup"><span data-stu-id="1b865-111">Store environment variables outside of source control.</span></span>
* <span data-ttu-id="1b865-112">從您的應用程式存取 Azure 環境變數。</span><span class="sxs-lookup"><span data-stu-id="1b865-112">Access Azure environment variables from your app.</span></span>
* <span data-ttu-id="1b865-113">連接 tooa 資料庫 (MongoDB)。</span><span class="sxs-lookup"><span data-stu-id="1b865-113">Connect tooa database (MongoDB).</span></span>

<span data-ttu-id="1b865-114">您應具備 Sails.js 的使用知識。</span><span class="sxs-lookup"><span data-stu-id="1b865-114">You should have working knowledge of Sails.js.</span></span> <span data-ttu-id="1b865-115">本教學課程中不是預期的 toohelp 您問題相關 toorunning Sail.js 一般。</span><span class="sxs-lookup"><span data-stu-id="1b865-115">This tutorial is not intended toohelp you with issues related toorunning Sail.js in general.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="1b865-116">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="1b865-116">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="1b865-117">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="1b865-117">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="1b865-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – 我們 CLI hello 傳統和資源管理部署模型</span><span class="sxs-lookup"><span data-stu-id="1b865-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span>
- <span data-ttu-id="1b865-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) -hello 資源管理部署模型我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="1b865-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b865-120">必要條件</span><span class="sxs-lookup"><span data-stu-id="1b865-120">Prerequisites</span></span>
* [<span data-ttu-id="1b865-121">Node.js</span><span class="sxs-lookup"><span data-stu-id="1b865-121">Node.js</span></span>](https://nodejs.org/)
* [<span data-ttu-id="1b865-122">Sails.js</span><span class="sxs-lookup"><span data-stu-id="1b865-122">Sails.js</span></span>](http://sailsjs.org/get-started)
* [<span data-ttu-id="1b865-123">Git</span><span class="sxs-lookup"><span data-stu-id="1b865-123">Git</span></span>](http://www.git-scm.com/downloads)
* [<span data-ttu-id="1b865-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1b865-124">Azure CLI 2.0</span></span>](/cli/azure/install-az-cli2)
* <span data-ttu-id="1b865-125">Microsoft Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b865-125">A Microsoft Azure account.</span></span> <span data-ttu-id="1b865-126">如果您沒有這類帳戶，可以[註冊免費試用版](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)，或是[啟用自己的 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="1b865-126">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="1b865-127">您可以[試用 App Service](https://azure.microsoft.com/try/app-service/)，而不需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1b865-127">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="1b865-128">建立起始應用程式，並玩的總 tooan 小時-沒有所需的信用卡，任何承諾。</span><span class="sxs-lookup"><span data-stu-id="1b865-128">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a><span data-ttu-id="1b865-129">步驟 1︰在本機建立和設定 Sails.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="1b865-129">Step 1: Create and configure a Sails.js app locally</span></span>
<span data-ttu-id="1b865-130">首先，請執行下列步驟 ，在部署環境中快速建立預設 Sails.js 應用程式︰</span><span class="sxs-lookup"><span data-stu-id="1b865-130">First, quickly create a default Sails.js app in your development environment by following these steps:</span></span>

1. <span data-ttu-id="1b865-131">您選擇的開啟 hello 命令列的終端機和`CD`tooa 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="1b865-131">Open hello command-line terminal of your choice and `CD` tooa working directory.</span></span>
2. <span data-ttu-id="1b865-132">建立 Sails.js 應用程式並加以執行︰</span><span class="sxs-lookup"><span data-stu-id="1b865-132">Create a Sails.js app and run it:</span></span>

        sails new <app_name>
        cd <app_name>
        sails lift

    <span data-ttu-id="1b865-133">請確定您可以瀏覽 toohello http://localhost:1377 在預設首頁。</span><span class="sxs-lookup"><span data-stu-id="1b865-133">Make sure you can navigate toohello default home page at http://localhost:1377.</span></span>

1. <span data-ttu-id="1b865-134">接下來，啟用 Azure 記錄。</span><span class="sxs-lookup"><span data-stu-id="1b865-134">Next, enable logging for Azure.</span></span> <span data-ttu-id="1b865-135">在根目錄中，建立名為的檔案`iisnode.yml`並加入下列兩行 hello:</span><span class="sxs-lookup"><span data-stu-id="1b865-135">In your root directory, create a file called `iisnode.yml` and add hello following two lines:</span></span>

        loggingEnabled: true
        logDirectory: iisnode

    <span data-ttu-id="1b865-136">現在已啟用記錄功能 hello [iisnode](https://github.com/tjanczuk/iisnode) Azure 應用程式服務會使用 toorun Node.js 應用程式的伺服器。</span><span class="sxs-lookup"><span data-stu-id="1b865-136">Logging is now enabled for hello [iisnode](https://github.com/tjanczuk/iisnode) server that Azure App Service uses toorun Node.js apps.</span></span> 
    <span data-ttu-id="1b865-137">如需有關其運作方式的詳細資訊，請參閱[toodebug Node.js web 應用程式在 Azure App Service 中的](web-sites-nodejs-debug.md)。</span><span class="sxs-lookup"><span data-stu-id="1b865-137">For more information on how this works, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

2. <span data-ttu-id="1b865-138">接著，設定 hello Sails.js 應用程式 toouse Azure 環境變數。</span><span class="sxs-lookup"><span data-stu-id="1b865-138">Next, configure hello Sails.js app toouse Azure environment variables.</span></span> <span data-ttu-id="1b865-139">開啟 config/env/production.js tooconfigure 實際執行環境，並設定`port`和`hookTimeout`:</span><span class="sxs-lookup"><span data-stu-id="1b865-139">Open config/env/production.js tooconfigure your production environment, and set `port` and `hookTimeout`:</span></span>

        module.exports = {

            // Use process.env.port toohandle web requests toohello default HTTP port
            port: process.env.port,
            // Increase hooks timout too30 seconds
            // This avoids hello Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    <span data-ttu-id="1b865-140">您可以在 [Sails.js 文件](http://sailsjs.org/documentation/reference/configuration/sails-config)中找到這些組態設定的文件。</span><span class="sxs-lookup"><span data-stu-id="1b865-140">You can find documentation for these configuration settings in the  [Sails.js Documentation](http://sailsjs.org/documentation/reference/configuration/sails-config).</span></span>

4. <span data-ttu-id="1b865-141">接下來，硬 hello Node.js 版本想 toouse。</span><span class="sxs-lookup"><span data-stu-id="1b865-141">Next, hardcode hello Node.js version you want toouse.</span></span> <span data-ttu-id="1b865-142">Package.json，在加入 hello 下列`engines`屬性 tooset hello Node.js 版本 tooone 我們想要的。</span><span class="sxs-lookup"><span data-stu-id="1b865-142">In package.json, add hello following `engines` property tooset hello Node.js version tooone that we want.</span></span>

        "engines": {
            "node": "6.9.1"
        },

5. <span data-ttu-id="1b865-143">最後，初始化 Git 儲存機制，並認可您的檔案。</span><span class="sxs-lookup"><span data-stu-id="1b865-143">Finally, initialize a Git repository and commit your files.</span></span> <span data-ttu-id="1b865-144">在 hello （package.json 所在） 的應用程式根目錄，請執行下列 Git 命令 hello:</span><span class="sxs-lookup"><span data-stu-id="1b865-144">In hello application root (where package.json is), run hello following Git commands:</span></span>

        git init
        git add .
        git commit -m "<your commit message>"

<span data-ttu-id="1b865-145">您的程式碼是準備 toobe 部署。</span><span class="sxs-lookup"><span data-stu-id="1b865-145">Your code is ready toobe deployed.</span></span> 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a><span data-ttu-id="1b865-146">步驟 2︰建立 Azure 應用程式和部署 Sails.js</span><span class="sxs-lookup"><span data-stu-id="1b865-146">Step 2: Create an Azure app and deploy Sails.js</span></span>

<span data-ttu-id="1b865-147">接下來，在 Azure 中建立 hello 應用程式服務資源和部署您 Sails.js 應用程式 tooit。</span><span class="sxs-lookup"><span data-stu-id="1b865-147">Next, create hello App Service resource in Azure and deploy your Sails.js app tooit.</span></span>

1. <span data-ttu-id="1b865-148">登入 tooAzure 就像這樣：</span><span class="sxs-lookup"><span data-stu-id="1b865-148">log in tooAzure like so:</span></span>

        az login

    <span data-ttu-id="1b865-149">請依照瀏覽器與 Microsoft 帳戶具有 Azure 訂用帳戶中的 hello 提示 toocontinue hello 登入。</span><span class="sxs-lookup"><span data-stu-id="1b865-149">Follow hello prompt toocontinue hello login in a browser with a Microsoft account that has your Azure subscription.</span></span>

3. <span data-ttu-id="1b865-150">設定應用程式服務的 hello 部署使用者。</span><span class="sxs-lookup"><span data-stu-id="1b865-150">Set hello deployment user for App Service.</span></span> <span data-ttu-id="1b865-151">稍後您將使用這些認證來部署程式碼。</span><span class="sxs-lookup"><span data-stu-id="1b865-151">You will deploy code using these credentials later.</span></span>
   
        az appservice web deployment user set --user-name <username> --password <password>

3. <span data-ttu-id="1b865-152">使用名稱建立[資源群組](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1b865-152">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with a name.</span></span> <span data-ttu-id="1b865-153">此 Node.js 教學課程中，實際上並不需要 tooknow 它是什麼。</span><span class="sxs-lookup"><span data-stu-id="1b865-153">For this Node.js tutorial, you don't really need tooknow what it is.</span></span>

        az group create --location "<location>" --name my-sailsjs-app-group

    <span data-ttu-id="1b865-154">toosee 何種可能的值，您可以使用`<location>`，使用 hello `az appservice list-locations` CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="1b865-154">toosee what possible values you can use for `<location>`, use hello `az appservice list-locations` CLI command.</span></span>

3. <span data-ttu-id="1b865-155">使用名稱建立「免費」[App Service 方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1b865-155">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) with a name.</span></span> <span data-ttu-id="1b865-156">在此 Node.js 教學課程中，只需知道，您可以免費使用本方案中 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b865-156">For this Node.js tutorial, just know that you won't be charged for web apps in this plan.</span></span>

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. <span data-ttu-id="1b865-157">在 `<app_name>` 中使用唯一名稱建立新的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1b865-157">Create a new web app with a unique name in `<app_name>`.</span></span>

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a><span data-ttu-id="1b865-158">步驟 3︰設定和部署 Sails.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="1b865-158">Step 3: Configure and deploy your Sails.js app</span></span>

1. <span data-ttu-id="1b865-159">設定新的 web 應用程式的本機 Git 部署以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="1b865-159">Configure local Git deployment for your new web app with hello following command:</span></span>

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="1b865-160">您會收到 JSON 輸出就像這樣，這表示該 hello 遠端 Git 儲存機制設定：</span><span class="sxs-lookup"><span data-stu-id="1b865-160">You will get a JSON output like this, which means that hello remote Git repository is configured:</span></span>

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. <span data-ttu-id="1b865-161">將 hello URL hello JSON 中加入 Git 遠端的本機儲存機制 (稱為`azure`為了簡化)。</span><span class="sxs-lookup"><span data-stu-id="1b865-161">Add hello URL in hello JSON as a Git remote for your local repository (called `azure` for simplicity).</span></span>

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. <span data-ttu-id="1b865-162">部署您的範例程式碼 toohello `azure` Git 遠端。</span><span class="sxs-lookup"><span data-stu-id="1b865-162">Deploy your sample code toohello `azure` Git remote.</span></span> <span data-ttu-id="1b865-163">出現提示時，使用您先前設定的 hello 部署認證。</span><span class="sxs-lookup"><span data-stu-id="1b865-163">When prompted, use hello deployment credentials you configured earlier.</span></span>

        git push azure master

7. <span data-ttu-id="1b865-164">最後，只要啟動即時 Azure 應用程式在 hello 瀏覽器中：</span><span class="sxs-lookup"><span data-stu-id="1b865-164">Finally, just launch your live Azure app in hello browser:</span></span>

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="1b865-165">您現在應該會看到 hello 相同 Sails.js 首頁。</span><span class="sxs-lookup"><span data-stu-id="1b865-165">You should now see hello same Sails.js home page.</span></span>

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a><span data-ttu-id="1b865-166">疑難排解您的部署</span><span class="sxs-lookup"><span data-stu-id="1b865-166">Troubleshoot your deployment</span></span>
<span data-ttu-id="1b865-167">如果 Sails.js 應用程式失敗原因，App Service 中，尋找 hello stderr 記錄 toohelp 進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="1b865-167">If your Sails.js application fails for some reason in App Service, find hello stderr logs toohelp troubleshoot it.</span></span>
<span data-ttu-id="1b865-168">如需詳細資訊，請參閱[toodebug Node.js web 應用程式在 Azure App Service 中的](web-sites-nodejs-debug.md)。</span><span class="sxs-lookup"><span data-stu-id="1b865-168">For more information, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>
<span data-ttu-id="1b865-169">Hello 應用程式已順利啟動，如果 hello stdout 記錄應該會顯示您 hello 熟悉訊息：</span><span class="sxs-lookup"><span data-stu-id="1b865-169">If hello app has started successfully, hello stdout log should show you hello familiar message:</span></span>

                   .-..-.
    
       Sails              <|    .-..-.
       v0.12.11            |\
                          /|.\
                         / || \
                       ,'  |'  \
                    .-'.-==|/_--'
                    `--'-------' 
       __---___--___---___--___---___--___
     ____---___--___---___--___---___--___-__

    Server lifted in `D:\home\site\wwwroot`
    toosee your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    tooshut down Sails, press <CTRL> + C at any time.

<span data-ttu-id="1b865-170">您可以控制在 hello hello stdout 記錄檔的資料粒度[config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging)檔案。</span><span class="sxs-lookup"><span data-stu-id="1b865-170">You can control granularity of hello stdout logs in hello [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.</span></span>

## <a name="connect-tooa-database-in-azure"></a><span data-ttu-id="1b865-171">連接 tooa 在 Azure 中的資料庫</span><span class="sxs-lookup"><span data-stu-id="1b865-171">Connect tooa database in Azure</span></span>
<span data-ttu-id="1b865-172">tooconnect tooa 資料庫在 Azure 中，在 Azure 中，例如 Azure SQL Database、 MySQL、 MongoDB、 Azure (Redis) 快取 」 等，建立您所選擇的 hello 資料庫，並使用 hello 對應[資料存放區的配接器](https://github.com/balderdashy/sails#compatibility)tooconnect tooit。</span><span class="sxs-lookup"><span data-stu-id="1b865-172">tooconnect tooa database in Azure, you create hello database of your choice in Azure, such as Azure SQL Database, MySQL, MongoDB, Azure (Redis) Cache, etc., and use hello corresponding [datastore adapter](https://github.com/balderdashy/sails#compatibility) tooconnect tooit.</span></span> <span data-ttu-id="1b865-173">hello 本節中的步驟示範如何使用 tooconnect tooMongoDB [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md)資料庫，可支援 MongoDB 用戶端連線。</span><span class="sxs-lookup"><span data-stu-id="1b865-173">hello steps in this section show you how tooconnect tooMongoDB by using an [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, which can support MongoDB client connections.</span></span>

1. <span data-ttu-id="1b865-174">[建立具有 MongoDB 通訊協定支援的 Cosmos DB 帳戶](../documentdb/documentdb-create-mongodb-account.md)。</span><span class="sxs-lookup"><span data-stu-id="1b865-174">[Create a Cosmos DB account with MongoDB protocol support](../documentdb/documentdb-create-mongodb-account.md).</span></span>
2. <span data-ttu-id="1b865-175">[建立 Cosmos DB 集合和資料庫](../documentdb/documentdb-create-collection.md)。</span><span class="sxs-lookup"><span data-stu-id="1b865-175">[Create a Cosmos DB collection and database](../documentdb/documentdb-create-collection.md).</span></span> <span data-ttu-id="1b865-176">hello hello 集合名稱並不重要，但是當您從 Sails.js 連接時，需要 hello hello 資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="1b865-176">hello name of hello collection doesn't matter, but you need hello name of hello database when you connect from Sails.js.</span></span>
3. <span data-ttu-id="1b865-177">[尋找 hello Cosmos DB 資料庫的連接資訊](../cosmos-db/connect-mongodb-account.md#GetCustomConnection)。</span><span class="sxs-lookup"><span data-stu-id="1b865-177">[Find hello connection information for your Cosmos DB database](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span></span>
2. <span data-ttu-id="1b865-178">從命令列的終端機，安裝 hello MongoDB 配接器：</span><span class="sxs-lookup"><span data-stu-id="1b865-178">From your command-line terminal, install hello MongoDB adapter:</span></span>

        npm install sails-mongo --save

3. <span data-ttu-id="1b865-179">開啟 config/connections.js 並新增下列連線物件 toohello 清單 hello:</span><span class="sxs-lookup"><span data-stu-id="1b865-179">Open config/connections.js and add hello following connection object toohello list:</span></span>

        docDbMongo: {
            adapter: 'sails-mongo',
            user: process.env.dbuser,
            password: process.env.dbpassword,
            host: process.env.dbhost,
            port: process.env.dbport,
            database: process.env.dbname,
            ssl: true
        },

    > [!NOTE] 
    > <span data-ttu-id="1b865-180">hello`ssl: true`選項，請務必因為[Cosmos DB 需要](../cosmos-db/connect-mongodb-account.md#connection-string-requirements)。</span><span class="sxs-lookup"><span data-stu-id="1b865-180">hello `ssl: true` option is important because [Cosmos DB requires it](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 
    >
    >

4. <span data-ttu-id="1b865-181">每個環境變數 (`process.env.*`)，您需要 tooset 在應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="1b865-181">For each environment variable (`process.env.*`), you need tooset it in App Service.</span></span> <span data-ttu-id="1b865-182">toodo 終端機中的下列命令，執行的 hello。</span><span class="sxs-lookup"><span data-stu-id="1b865-182">toodo this, run hello following commands from your terminal.</span></span> <span data-ttu-id="1b865-183">使用您 Cosmos DB hello 連接資訊。</span><span class="sxs-lookup"><span data-stu-id="1b865-183">Use hello connection information for your Cosmos DB.</span></span>

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="1b865-184">將您的設定放在 Azure 應用程式設定中，可讓敏感性資料脫離原始檔控制 (Git)。</span><span class="sxs-lookup"><span data-stu-id="1b865-184">Putting your settings in Azure app settings keeps sensitive data out of your source control (Git).</span></span> <span data-ttu-id="1b865-185">接下來，您將設定您的開發環境 toouse hello 相同的連接資訊。</span><span class="sxs-lookup"><span data-stu-id="1b865-185">Next, you will configure your development environment toouse hello same connection information.</span></span>
5. <span data-ttu-id="1b865-186">開啟 config/local.js 並新增下列連線物件的 hello:</span><span class="sxs-lookup"><span data-stu-id="1b865-186">Open config/local.js and add hello following connections object:</span></span>

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    <span data-ttu-id="1b865-187">此設定會覆寫 config/connections.js 檔 hello 本機環境中的 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="1b865-187">This configuration overrides hello settings in your config/connections.js file for hello local environment.</span></span> <span data-ttu-id="1b865-188">這個檔案會排除 hello 預設.gitignore 在專案中，因此不會儲存在 Git 中。</span><span class="sxs-lookup"><span data-stu-id="1b865-188">This file is excluded by hello default .gitignore in your project, so it will not be stored in Git.</span></span> <span data-ttu-id="1b865-189">現在，您就可以 tooconnect tooyour Cosmos DB (MongoDB) 資料庫，從您的 Azure web 應用程式並從您的本機開發環境。</span><span class="sxs-lookup"><span data-stu-id="1b865-189">Now, you are able tooconnect tooyour Cosmos DB (MongoDB) database both from your Azure web app and from your local development environment.</span></span>
6. <span data-ttu-id="1b865-190">開啟 config/env/production.js tooconfigure 實際執行環境，並加入下列 hello`models`物件：</span><span class="sxs-lookup"><span data-stu-id="1b865-190">Open config/env/production.js tooconfigure your production environment, and add hello following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. <span data-ttu-id="1b865-191">開啟 config/env/development.js tooconfigure 開發環境，並加入下列 hello`models`物件：</span><span class="sxs-lookup"><span data-stu-id="1b865-191">Open config/env/development.js tooconfigure your development environment, and add hello following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    <span data-ttu-id="1b865-192">`migrate: 'alter'`可讓您使用資料庫移轉功能 toocreate 並輕鬆地更新集合資料庫或資料表。</span><span class="sxs-lookup"><span data-stu-id="1b865-192">`migrate: 'alter'` lets you use database migration features toocreate and update database collections or tables easily.</span></span> <span data-ttu-id="1b865-193">不過，`migrate: 'safe'`因為 Sails.js 不允許您 toouse 用於 Azure （生產環境） 環境`migrate: 'alter'`實際執行環境中 (請參閱[Sails.js 文件](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings))。</span><span class="sxs-lookup"><span data-stu-id="1b865-193">However, `migrate: 'safe'` is used for your Azure (production) environment because Sails.js does not allow you toouse `migrate: 'alter'` in a production environment (see [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span></span>
8. <span data-ttu-id="1b865-194">從終端機，hello[產生](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate)Sails.js[藍圖 API](http://sailsjs.org/documentation/concepts/blueprints)像平常，然後執行`sails lift`來建立具有 Sails.js 資料庫移轉 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1b865-194">From hello terminal, [generate](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) a Sails.js [blueprint API](http://sailsjs.org/documentation/concepts/blueprints) like you normally would, then run `sails lift` to create hello database with Sails.js database migration.</span></span> <span data-ttu-id="1b865-195">例如：</span><span class="sxs-lookup"><span data-stu-id="1b865-195">For example:</span></span>

         sails generate api mywidget
         sails lift

    <span data-ttu-id="1b865-196">hello`mywidget`此命令所產生的模型是空的但我們可以使用它 tooshow 我們有資料庫連線。</span><span class="sxs-lookup"><span data-stu-id="1b865-196">hello `mywidget` model generated by this command is empty, but we can use it tooshow that we have database connectivity.</span></span>
    <span data-ttu-id="1b865-197">當您執行`sails lift`，它會建立 hello 遺漏集合和 hello 的資料表模型工作流程應用程式使用。</span><span class="sxs-lookup"><span data-stu-id="1b865-197">When you run `sails lift`, it creates hello missing collections and tables for hello models your app uses.</span></span>
9. <span data-ttu-id="1b865-198">您剛建立 hello 瀏覽器中存取 hello 藍圖 API。</span><span class="sxs-lookup"><span data-stu-id="1b865-198">Access hello blueprint API you just created in hello browser.</span></span> <span data-ttu-id="1b865-199">例如：</span><span class="sxs-lookup"><span data-stu-id="1b865-199">For example:</span></span>

        http://localhost:1337/mywidget/create

    <span data-ttu-id="1b865-200">hello API 應傳回 hello 建立項目後 tooyou 在 hello 瀏覽器視窗中，這表示已順利建立您的集合。</span><span class="sxs-lookup"><span data-stu-id="1b865-200">hello API should return hello created entry back tooyou in hello browser window, which means that your collection is created  successfully.</span></span>

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. <span data-ttu-id="1b865-201">現在，推入您的變更 tooAzure，並瀏覽應用程式 tooyour toomake，仍能運作。</span><span class="sxs-lookup"><span data-stu-id="1b865-201">Now, push your changes tooAzure, and browse tooyour app toomake sure it still works.</span></span>

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. <span data-ttu-id="1b865-202">存取 hello Azure web 應用程式的藍圖 API。</span><span class="sxs-lookup"><span data-stu-id="1b865-202">Access hello blueprint API of your Azure web app.</span></span> <span data-ttu-id="1b865-203">例如：</span><span class="sxs-lookup"><span data-stu-id="1b865-203">For example:</span></span>

         http://<appname>.azurewebsites.net/mywidget/create

     <span data-ttu-id="1b865-204">如果 hello API 傳回另一個新的項目，Azure web 應用程式指 tooyour Cosmos DB (MongoDB) 資料庫。</span><span class="sxs-lookup"><span data-stu-id="1b865-204">If hello API returns another new entry, then your Azure web app is talking tooyour Cosmos DB (MongoDB) database.</span></span>

## <a name="more-resources"></a><span data-ttu-id="1b865-205">其他資源</span><span class="sxs-lookup"><span data-stu-id="1b865-205">More resources</span></span>
* [<span data-ttu-id="1b865-206">在 Azure App Service 中開始使用 Node.js Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="1b865-206">Get started with Node.js web apps in Azure App Service</span></span>](app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="1b865-207">使用 Node.js 模組與 Azure 應用程式搭配</span><span class="sxs-lookup"><span data-stu-id="1b865-207">Using Node.js Modules with Azure applications</span></span>](../nodejs-use-node-modules-azure-apps.md)
