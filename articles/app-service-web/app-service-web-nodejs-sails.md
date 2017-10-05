---
title: "將 Sails.js Web 應用程式部署至 Azure App Service | Microsoft Docs"
description: "了解如何將 Node.js 應用程式部署到 Azure App Service。 本教學課程示範如何部署 Sails.js Web 應用程式。"
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
ms.openlocfilehash: e36fc5f5273f98c3cca91973db9910f32443ec7c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-a-sailsjs-web-app-to-azure-app-service"></a><span data-ttu-id="9434c-104">將 Sails.js Web 應用程式部署至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="9434c-104">Deploy a Sails.js web app to Azure App Service</span></span>
<span data-ttu-id="9434c-105">本教學課程示範如何將 Sails.js 應用程式部署至 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="9434c-105">This tutorial shows you how to deploy a Sails.js app to Azure App Service.</span></span> <span data-ttu-id="9434c-106">過程中，您可以搜集一些如何設定 Node.js 應用程式以在 App Service 中執行的一般知識。</span><span class="sxs-lookup"><span data-stu-id="9434c-106">In the process, you can glean some general knowledge on how to configure your Node.js app to run in App Service.</span></span>

<span data-ttu-id="9434c-107">在這裡，您將學習有用的技能，例如︰</span><span class="sxs-lookup"><span data-stu-id="9434c-107">Here, you will learn useful skills like:</span></span>

* <span data-ttu-id="9434c-108">設定在 App Service 中執行 Sails.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9434c-108">Configure a Sails.js app run in App Service.</span></span>
* <span data-ttu-id="9434c-109">從命令列將應用程式部署至 App Service。</span><span class="sxs-lookup"><span data-stu-id="9434c-109">Deploy an app to App Service from the command line.</span></span>
* <span data-ttu-id="9434c-110">讀取 stderr 和 stdout 記錄來疑難排解任何部署問題。</span><span class="sxs-lookup"><span data-stu-id="9434c-110">Read stderr and stdout logs to troubleshoot any deployment issues.</span></span>
* <span data-ttu-id="9434c-111">儲存原始檔控制外部的環境變數。</span><span class="sxs-lookup"><span data-stu-id="9434c-111">Store environment variables outside of source control.</span></span>
* <span data-ttu-id="9434c-112">從您的應用程式存取 Azure 環境變數。</span><span class="sxs-lookup"><span data-stu-id="9434c-112">Access Azure environment variables from your app.</span></span>
* <span data-ttu-id="9434c-113">連接到資料庫 (MongoDB)。</span><span class="sxs-lookup"><span data-stu-id="9434c-113">Connect to a database (MongoDB).</span></span>

<span data-ttu-id="9434c-114">您應具備 Sails.js 的使用知識。</span><span class="sxs-lookup"><span data-stu-id="9434c-114">You should have working knowledge of Sails.js.</span></span> <span data-ttu-id="9434c-115">本教學課程的目的不是協助您了解一般執行 Sail.js 的相關問題。</span><span class="sxs-lookup"><span data-stu-id="9434c-115">This tutorial is not intended to help you with issues related to running Sail.js in general.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="9434c-116">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="9434c-116">CLI versions to complete the task</span></span>

<span data-ttu-id="9434c-117">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="9434c-117">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="9434c-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – 適用於傳統和資源管理部署模型的 CLI</span><span class="sxs-lookup"><span data-stu-id="9434c-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span>
- <span data-ttu-id="9434c-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - 適用於資源管理部署模型的新一代 CLI</span><span class="sxs-lookup"><span data-stu-id="9434c-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9434c-120">必要條件</span><span class="sxs-lookup"><span data-stu-id="9434c-120">Prerequisites</span></span>
* [<span data-ttu-id="9434c-121">Node.js</span><span class="sxs-lookup"><span data-stu-id="9434c-121">Node.js</span></span>](https://nodejs.org/)
* [<span data-ttu-id="9434c-122">Sails.js</span><span class="sxs-lookup"><span data-stu-id="9434c-122">Sails.js</span></span>](http://sailsjs.org/get-started)
* [<span data-ttu-id="9434c-123">Git</span><span class="sxs-lookup"><span data-stu-id="9434c-123">Git</span></span>](http://www.git-scm.com/downloads)
* [<span data-ttu-id="9434c-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9434c-124">Azure CLI 2.0</span></span>](/cli/azure/install-az-cli2)
* <span data-ttu-id="9434c-125">Microsoft Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9434c-125">A Microsoft Azure account.</span></span> <span data-ttu-id="9434c-126">如果您沒有這類帳戶，可以[註冊免費試用版](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)，或是[啟用自己的 Visual Studio 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="9434c-126">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="9434c-127">您可以[試用 App Service](https://azure.microsoft.com/try/app-service/)，而不需要 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9434c-127">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="9434c-128">建立入門 App，並試用長達一小時。不需要信用卡，也不需簽定合約。</span><span class="sxs-lookup"><span data-stu-id="9434c-128">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a><span data-ttu-id="9434c-129">步驟 1︰在本機建立和設定 Sails.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="9434c-129">Step 1: Create and configure a Sails.js app locally</span></span>
<span data-ttu-id="9434c-130">首先，請執行下列步驟 ，在部署環境中快速建立預設 Sails.js 應用程式︰</span><span class="sxs-lookup"><span data-stu-id="9434c-130">First, quickly create a default Sails.js app in your development environment by following these steps:</span></span>

1. <span data-ttu-id="9434c-131">開啟您選擇的命令列終端機，並 `CD` 到工作目錄。</span><span class="sxs-lookup"><span data-stu-id="9434c-131">Open the command-line terminal of your choice and `CD` to a working directory.</span></span>
2. <span data-ttu-id="9434c-132">建立 Sails.js 應用程式並加以執行︰</span><span class="sxs-lookup"><span data-stu-id="9434c-132">Create a Sails.js app and run it:</span></span>

        sails new <app_name>
        cd <app_name>
        sails lift

    <span data-ttu-id="9434c-133">請確定您可以瀏覽到 http://localhost:1377 上的預設首頁。</span><span class="sxs-lookup"><span data-stu-id="9434c-133">Make sure you can navigate to the default home page at http://localhost:1377.</span></span>

1. <span data-ttu-id="9434c-134">接下來，啟用 Azure 記錄。</span><span class="sxs-lookup"><span data-stu-id="9434c-134">Next, enable logging for Azure.</span></span> <span data-ttu-id="9434c-135">在根目錄中，建立名為 `iisnode.yml` 的檔案並新增下列兩行︰</span><span class="sxs-lookup"><span data-stu-id="9434c-135">In your root directory, create a file called `iisnode.yml` and add the following two lines:</span></span>

        loggingEnabled: true
        logDirectory: iisnode

    <span data-ttu-id="9434c-136">現在已啟用 Azure App Service 用來執行 Node.js 應用程式的 [iisnode](https://github.com/tjanczuk/iisnode) 伺服器記錄功能。</span><span class="sxs-lookup"><span data-stu-id="9434c-136">Logging is now enabled for the [iisnode](https://github.com/tjanczuk/iisnode) server that Azure App Service uses to run Node.js apps.</span></span> 
    <span data-ttu-id="9434c-137">如需有關運作方式的詳細資訊，請參閱 [如何在 Azure App Service 中針對 Node.js Web 應用程式進行偵錯](web-sites-nodejs-debug.md)。</span><span class="sxs-lookup"><span data-stu-id="9434c-137">For more information on how this works, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

2. <span data-ttu-id="9434c-138">接下來，設定 Sails.js 應用程式以使用 Azure 環境變數。</span><span class="sxs-lookup"><span data-stu-id="9434c-138">Next, configure the Sails.js app to use Azure environment variables.</span></span> <span data-ttu-id="9434c-139">開啟 config/env/production.js 來設定您的生產環境，並設定 `port` 和 `hookTimeout`：</span><span class="sxs-lookup"><span data-stu-id="9434c-139">Open config/env/production.js to configure your production environment, and set `port` and `hookTimeout`:</span></span>

        module.exports = {

            // Use process.env.port to handle web requests to the default HTTP port
            port: process.env.port,
            // Increase hooks timout to 30 seconds
            // This avoids the Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    <span data-ttu-id="9434c-140">您可以在 [Sails.js 文件](http://sailsjs.org/documentation/reference/configuration/sails-config)中找到這些組態設定的文件。</span><span class="sxs-lookup"><span data-stu-id="9434c-140">You can find documentation for these configuration settings in the  [Sails.js Documentation](http://sailsjs.org/documentation/reference/configuration/sails-config).</span></span>

4. <span data-ttu-id="9434c-141">接下來，硬式編碼您要使用的 Node.js 版本。</span><span class="sxs-lookup"><span data-stu-id="9434c-141">Next, hardcode the Node.js version you want to use.</span></span> <span data-ttu-id="9434c-142">在 package.json 中新增以下 `engines` 屬性，以將 Node.js 版本設定為我們需要的版本。</span><span class="sxs-lookup"><span data-stu-id="9434c-142">In package.json, add the following `engines` property to set the Node.js version to one that we want.</span></span>

        "engines": {
            "node": "6.9.1"
        },

5. <span data-ttu-id="9434c-143">最後，初始化 Git 儲存機制，並認可您的檔案。</span><span class="sxs-lookup"><span data-stu-id="9434c-143">Finally, initialize a Git repository and commit your files.</span></span> <span data-ttu-id="9434c-144">在應用程式根目錄中 (在 package.json 的所在位置)，執行下列 Git 命令︰</span><span class="sxs-lookup"><span data-stu-id="9434c-144">In the application root (where package.json is), run the following Git commands:</span></span>

        git init
        git add .
        git commit -m "<your commit message>"

<span data-ttu-id="9434c-145">您的程式碼已準備好進行部署。</span><span class="sxs-lookup"><span data-stu-id="9434c-145">Your code is ready to be deployed.</span></span> 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a><span data-ttu-id="9434c-146">步驟 2︰建立 Azure 應用程式和部署 Sails.js</span><span class="sxs-lookup"><span data-stu-id="9434c-146">Step 2: Create an Azure app and deploy Sails.js</span></span>

<span data-ttu-id="9434c-147">接下來，在 Azure 中建立 App Service 資源，並將您的 Sails.js 應用程式部署至其中。</span><span class="sxs-lookup"><span data-stu-id="9434c-147">Next, create the App Service resource in Azure and deploy your Sails.js app to it.</span></span>

1. <span data-ttu-id="9434c-148">如下所示，登入 Azure：</span><span class="sxs-lookup"><span data-stu-id="9434c-148">log in to Azure like so:</span></span>

        az login

    <span data-ttu-id="9434c-149">依照提示，在瀏覽器中繼續使用具有 Azure 訂用帳戶的 Microsoft 帳戶進行登入。</span><span class="sxs-lookup"><span data-stu-id="9434c-149">Follow the prompt to continue the login in a browser with a Microsoft account that has your Azure subscription.</span></span>

3. <span data-ttu-id="9434c-150">設定 App Service 的部署使用者。</span><span class="sxs-lookup"><span data-stu-id="9434c-150">Set the deployment user for App Service.</span></span> <span data-ttu-id="9434c-151">稍後您將使用這些認證來部署程式碼。</span><span class="sxs-lookup"><span data-stu-id="9434c-151">You will deploy code using these credentials later.</span></span>
   
        az appservice web deployment user set --user-name <username> --password <password>

3. <span data-ttu-id="9434c-152">使用名稱建立[資源群組](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="9434c-152">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with a name.</span></span> <span data-ttu-id="9434c-153">在此 Node.js 教學課程中，您真的不需要知道它是什麼。</span><span class="sxs-lookup"><span data-stu-id="9434c-153">For this Node.js tutorial, you don't really need to know what it is.</span></span>

        az group create --location "<location>" --name my-sailsjs-app-group

    <span data-ttu-id="9434c-154">若要查看您可用於 `<location>` 的可能值，請使用 `az appservice list-locations`CLI 命令。</span><span class="sxs-lookup"><span data-stu-id="9434c-154">To see what possible values you can use for `<location>`, use the `az appservice list-locations` CLI command.</span></span>

3. <span data-ttu-id="9434c-155">使用名稱建立「免費」[App Service 方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="9434c-155">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) with a name.</span></span> <span data-ttu-id="9434c-156">在此 Node.js 教學課程中，只需知道，您可以免費使用本方案中 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9434c-156">For this Node.js tutorial, just know that you won't be charged for web apps in this plan.</span></span>

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. <span data-ttu-id="9434c-157">在 `<app_name>` 中使用唯一名稱建立新的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9434c-157">Create a new web app with a unique name in `<app_name>`.</span></span>

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a><span data-ttu-id="9434c-158">步驟 3︰設定和部署 Sails.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="9434c-158">Step 3: Configure and deploy your Sails.js app</span></span>

1. <span data-ttu-id="9434c-159">使用下列命令，設定新 Web 應用程式的本機 Git 部署︰</span><span class="sxs-lookup"><span data-stu-id="9434c-159">Configure local Git deployment for your new web app with the following command:</span></span>

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="9434c-160">您會取得如下所示的 JSON 輸出，這表示已設定遠端 Git 儲存機制︰</span><span class="sxs-lookup"><span data-stu-id="9434c-160">You will get a JSON output like this, which means that the remote Git repository is configured:</span></span>

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. <span data-ttu-id="9434c-161">將 JSON 中的 URL 新增為本機儲存機制的 Git 遠端 (為了簡單起見，稱為 `azure`)。</span><span class="sxs-lookup"><span data-stu-id="9434c-161">Add the URL in the JSON as a Git remote for your local repository (called `azure` for simplicity).</span></span>

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. <span data-ttu-id="9434c-162">將您的範例程式碼部署至 `azure` Git 遠端。</span><span class="sxs-lookup"><span data-stu-id="9434c-162">Deploy your sample code to the `azure` Git remote.</span></span> <span data-ttu-id="9434c-163">出現提示時，使用您稍早設定的部署認證。</span><span class="sxs-lookup"><span data-stu-id="9434c-163">When prompted, use the deployment credentials you configured earlier.</span></span>

        git push azure master

7. <span data-ttu-id="9434c-164">最後，在瀏覽器中只要啟動即時 Azure 應用程式︰</span><span class="sxs-lookup"><span data-stu-id="9434c-164">Finally, just launch your live Azure app in the browser:</span></span>

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="9434c-165">您現在應該會看到相同的 Sails.js 首頁。</span><span class="sxs-lookup"><span data-stu-id="9434c-165">You should now see the same Sails.js home page.</span></span>

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a><span data-ttu-id="9434c-166">疑難排解您的部署</span><span class="sxs-lookup"><span data-stu-id="9434c-166">Troubleshoot your deployment</span></span>
<span data-ttu-id="9434c-167">如果 Sails.js 應用程式在 App Service 中因為某些原因而失敗，請尋找 stderr 記錄，以協助進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="9434c-167">If your Sails.js application fails for some reason in App Service, find the stderr logs to help troubleshoot it.</span></span>
<span data-ttu-id="9434c-168">如需詳細資訊，請參閱[如何在 Azure App Service 中針對 Node.js Web 應用程式進行偵錯](web-sites-nodejs-debug.md)。</span><span class="sxs-lookup"><span data-stu-id="9434c-168">For more information, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>
<span data-ttu-id="9434c-169">如果應用程式已順利啟動，stdout 記錄應該會顯示您熟悉的訊息︰</span><span class="sxs-lookup"><span data-stu-id="9434c-169">If the app has started successfully, the stdout log should show you the familiar message:</span></span>

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
    To see your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    To shut down Sails, press <CTRL> + C at any time.

<span data-ttu-id="9434c-170">您可以在 [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) 檔案中控制 stdout 記錄檔的細微度。</span><span class="sxs-lookup"><span data-stu-id="9434c-170">You can control granularity of the stdout logs in the [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.</span></span>

## <a name="connect-to-a-database-in-azure"></a><span data-ttu-id="9434c-171">連接到 Azure 中的資料庫</span><span class="sxs-lookup"><span data-stu-id="9434c-171">Connect to a database in Azure</span></span>
<span data-ttu-id="9434c-172">若要連接到 Azure 中的資料庫，您可以在 Azure 中建立所選擇的資料庫，例如 Azure SQL Database、MySQL、MongoDB、Azure (Redis) 快取等，並使用對應的 [資料存放區配接器](https://github.com/balderdashy/sails#compatibility) 連接到它。</span><span class="sxs-lookup"><span data-stu-id="9434c-172">To connect to a database in Azure, you create the database of your choice in Azure, such as Azure SQL Database, MySQL, MongoDB, Azure (Redis) Cache, etc., and use the corresponding [datastore adapter](https://github.com/balderdashy/sails#compatibility) to connect to it.</span></span> <span data-ttu-id="9434c-173">本章節中的步驟示範如何使用可支援 MongoDB 用戶端連線的 [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) 資料庫連線至 MongoDB。</span><span class="sxs-lookup"><span data-stu-id="9434c-173">The steps in this section show you how to connect to MongoDB by using an [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, which can support MongoDB client connections.</span></span>

1. <span data-ttu-id="9434c-174">[建立具有 MongoDB 通訊協定支援的 Cosmos DB 帳戶](../documentdb/documentdb-create-mongodb-account.md)。</span><span class="sxs-lookup"><span data-stu-id="9434c-174">[Create a Cosmos DB account with MongoDB protocol support](../documentdb/documentdb-create-mongodb-account.md).</span></span>
2. <span data-ttu-id="9434c-175">[建立 Cosmos DB 集合和資料庫](../documentdb/documentdb-create-collection.md)。</span><span class="sxs-lookup"><span data-stu-id="9434c-175">[Create a Cosmos DB collection and database](../documentdb/documentdb-create-collection.md).</span></span> <span data-ttu-id="9434c-176">集合的名稱並不重要，但是當您從 Sails.js 連線時，需要資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="9434c-176">The name of the collection doesn't matter, but you need the name of the database when you connect from Sails.js.</span></span>
3. <span data-ttu-id="9434c-177">[尋找您 Cosmos DB 資料庫的連線資訊](../cosmos-db/connect-mongodb-account.md#GetCustomConnection)。</span><span class="sxs-lookup"><span data-stu-id="9434c-177">[Find the connection information for your Cosmos DB database](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span></span>
2. <span data-ttu-id="9434c-178">從命令列終端機安裝 MongoDB 配接器︰</span><span class="sxs-lookup"><span data-stu-id="9434c-178">From your command-line terminal, install the MongoDB adapter:</span></span>

        npm install sails-mongo --save

3. <span data-ttu-id="9434c-179">開啟 config/connections.js 並將下列連接物件加入至清單︰</span><span class="sxs-lookup"><span data-stu-id="9434c-179">Open config/connections.js and add the following connection object to the list:</span></span>

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
    > <span data-ttu-id="9434c-180">`ssl: true` 選項很重要，因為 [Cosmos DB 需要](../cosmos-db/connect-mongodb-account.md#connection-string-requirements)。</span><span class="sxs-lookup"><span data-stu-id="9434c-180">The `ssl: true` option is important because [Cosmos DB requires it](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 
    >
    >

4. <span data-ttu-id="9434c-181">針對每個環境變數 (`process.env.*`)，您需要在 App Service 中加以設定。</span><span class="sxs-lookup"><span data-stu-id="9434c-181">For each environment variable (`process.env.*`), you need to set it in App Service.</span></span> <span data-ttu-id="9434c-182">若要執行此動作，可從您的終端機執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="9434c-182">To do this, run the following commands from your terminal.</span></span> <span data-ttu-id="9434c-183">使用您 Cosmos DB 的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="9434c-183">Use the connection information for your Cosmos DB.</span></span>

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="9434c-184">將您的設定放在 Azure 應用程式設定中，可讓敏感性資料脫離原始檔控制 (Git)。</span><span class="sxs-lookup"><span data-stu-id="9434c-184">Putting your settings in Azure app settings keeps sensitive data out of your source control (Git).</span></span> <span data-ttu-id="9434c-185">接下來，您將設定開發環境，以便使用相同的連接資訊。</span><span class="sxs-lookup"><span data-stu-id="9434c-185">Next, you will configure your development environment to use the same connection information.</span></span>
5. <span data-ttu-id="9434c-186">開啟 config/local.js 並新增下列連接物件︰</span><span class="sxs-lookup"><span data-stu-id="9434c-186">Open config/local.js and add the following connections object:</span></span>

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    <span data-ttu-id="9434c-187">此組態會覆寫 config/connections.js 檔案中本機環境的設定。</span><span class="sxs-lookup"><span data-stu-id="9434c-187">This configuration overrides the settings in your config/connections.js file for the local environment.</span></span> <span data-ttu-id="9434c-188">您專案中的預設 .gitignore 會排除這個檔案，因此不會儲存在 Git 中。</span><span class="sxs-lookup"><span data-stu-id="9434c-188">This file is excluded by the default .gitignore in your project, so it will not be stored in Git.</span></span> <span data-ttu-id="9434c-189">現在，您可以從 Azure Web 應用程式和從本機開發環境，連線至您的 Cosmos DB (MongoDB) 資料庫。</span><span class="sxs-lookup"><span data-stu-id="9434c-189">Now, you are able to connect to your Cosmos DB (MongoDB) database both from your Azure web app and from your local development environment.</span></span>
6. <span data-ttu-id="9434c-190">開啟 config/env/production.js 來設定您的生產環境，並加入下列 `models` 物件：</span><span class="sxs-lookup"><span data-stu-id="9434c-190">Open config/env/production.js to configure your production environment, and add the following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. <span data-ttu-id="9434c-191">開啟 config/env/development.js 來設定您的開發環境，並加入下列 `models` 物件：</span><span class="sxs-lookup"><span data-stu-id="9434c-191">Open config/env/development.js to configure your development environment, and add the following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    <span data-ttu-id="9434c-192">`migrate: 'alter'` 可讓您使用資料庫移轉功能，輕鬆地建立和更新資料庫集合或資料表。</span><span class="sxs-lookup"><span data-stu-id="9434c-192">`migrate: 'alter'` lets you use database migration features to create and update database collections or tables easily.</span></span> <span data-ttu-id="9434c-193">不過，要針對您的 Azure (生產) 環境使用 `migrate: 'safe'`，因為 Sails.js 不允許您在生產環境中使用 `migrate: 'alter'` (請參閱 [Sails.js 文件](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings))。</span><span class="sxs-lookup"><span data-stu-id="9434c-193">However, `migrate: 'safe'` is used for your Azure (production) environment because Sails.js does not allow you to use `migrate: 'alter'` in a production environment (see [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span></span>
8. <span data-ttu-id="9434c-194">從終端機中，[產生](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) Sails.js [藍圖 API](http://sailsjs.org/documentation/concepts/blueprints) (就像您平常所做的一樣)，然後執行 `sails lift` 以使用 Sails.js 資料庫移轉來建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="9434c-194">From the terminal, [generate](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) a Sails.js [blueprint API](http://sailsjs.org/documentation/concepts/blueprints) like you normally would, then run `sails lift` to create the database with Sails.js database migration.</span></span> <span data-ttu-id="9434c-195">例如：</span><span class="sxs-lookup"><span data-stu-id="9434c-195">For example:</span></span>

         sails generate api mywidget
         sails lift

    <span data-ttu-id="9434c-196">此命令所產生的 `mywidget` 模型是空的，但我們可以用它來顯示我們有資料庫連線能力。</span><span class="sxs-lookup"><span data-stu-id="9434c-196">The `mywidget` model generated by this command is empty, but we can use it to show that we have database connectivity.</span></span>
    <span data-ttu-id="9434c-197">當您執行 `sails lift`時，它會針對應用程式所使用的模型建立遺漏的集合和資料表。</span><span class="sxs-lookup"><span data-stu-id="9434c-197">When you run `sails lift`, it creates the missing collections and tables for the models your app uses.</span></span>
9. <span data-ttu-id="9434c-198">存取您剛剛在瀏覽器中建立的藍圖 API。</span><span class="sxs-lookup"><span data-stu-id="9434c-198">Access the blueprint API you just created in the browser.</span></span> <span data-ttu-id="9434c-199">例如：</span><span class="sxs-lookup"><span data-stu-id="9434c-199">For example:</span></span>

        http://localhost:1337/mywidget/create

    <span data-ttu-id="9434c-200">此 API 應該會在瀏覽器視窗中將建立的項目傳回給您，這表示您的集合建立成功。</span><span class="sxs-lookup"><span data-stu-id="9434c-200">The API should return the created entry back to you in the browser window, which means that your collection is created  successfully.</span></span>

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. <span data-ttu-id="9434c-201">現在，將變更推送至 Azure，並瀏覽至您的應用程式以確定它仍能運作。</span><span class="sxs-lookup"><span data-stu-id="9434c-201">Now, push your changes to Azure, and browse to your app to make sure it still works.</span></span>

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. <span data-ttu-id="9434c-202">存取 Azure Web 應用程式的藍圖 API。</span><span class="sxs-lookup"><span data-stu-id="9434c-202">Access the blueprint API of your Azure web app.</span></span> <span data-ttu-id="9434c-203">例如：</span><span class="sxs-lookup"><span data-stu-id="9434c-203">For example:</span></span>

         http://<appname>.azurewebsites.net/mywidget/create

     <span data-ttu-id="9434c-204">如果此 API 傳回另一個新項目，則您的 Azure Web 應用程式會與您的 Cosmos DB (MongoDB) 資料庫通訊。</span><span class="sxs-lookup"><span data-stu-id="9434c-204">If the API returns another new entry, then your Azure web app is talking to your Cosmos DB (MongoDB) database.</span></span>

## <a name="more-resources"></a><span data-ttu-id="9434c-205">其他資源</span><span class="sxs-lookup"><span data-stu-id="9434c-205">More resources</span></span>
* [<span data-ttu-id="9434c-206">在 Azure App Service 中開始使用 Node.js Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9434c-206">Get started with Node.js web apps in Azure App Service</span></span>](app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="9434c-207">使用 Node.js 模組與 Azure 應用程式搭配</span><span class="sxs-lookup"><span data-stu-id="9434c-207">Using Node.js Modules with Azure applications</span></span>](../nodejs-use-node-modules-azure-apps.md)
