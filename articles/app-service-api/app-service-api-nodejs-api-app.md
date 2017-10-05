---
title: "Azure App Service 中的 Node.js API 應用程式 | Microsoft Docs"
description: "了解如何建立 Node.js RESTful API，並將其部署至 Azure App Service 中的 API 應用程式。"
services: app-service\api
documentationcenter: node
author: bradygaster
manager: erikre
editor: 
ms.assetid: a820e400-06af-4852-8627-12b3db4a8e70
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: get-started-article
ms.date: 06/13/2017
ms.author: rachelap
ms.openlocfilehash: 806585edd43b9d2d678bfa41523e4d9d40af8cba
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-nodejs-restful-api-and-deploy-it-to-an-api-app-in-azure"></a><span data-ttu-id="aa72b-103">建置 Node.js RESTful API 並將它部署至 Azure 中的 API 應用程式</span><span class="sxs-lookup"><span data-stu-id="aa72b-103">Build a Node.js RESTful API and deploy it to an API app in Azure</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="aa72b-104">本快速入門示範如何在 Azure 上使用 [Swagger](http://swagger.io/) 定義並將其部署為 [API 應用程式](app-service-api-apps-why-best-platform.md)，建立 REST API (以 Node.js [Express](http://expressjs.com/) 撰寫。</span><span class="sxs-lookup"><span data-stu-id="aa72b-104">This quickstart shows how to create a REST API, written with Node.js [Express](http://expressjs.com/), using a [Swagger](http://swagger.io/) definition and deploying it as an [API app](app-service-api-apps-why-best-platform.md) on Azure.</span></span> <span data-ttu-id="aa72b-105">您可使用命令列工具建立應用程式、使用 [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) 設定資源，以及使用 Git 部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa72b-105">You create the app using command-line tools, configure resources with the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and deploy the app using Git.</span></span>  <span data-ttu-id="aa72b-106">當您完成後，您必須在 Azure 上執行工作範例 REST API。</span><span class="sxs-lookup"><span data-stu-id="aa72b-106">When you've finished, you have a working sample REST API running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa72b-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="aa72b-107">Prerequisites</span></span>

* [<span data-ttu-id="aa72b-108">Git</span><span class="sxs-lookup"><span data-stu-id="aa72b-108">Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="aa72b-109"> 安裝 Node.js 和 NPM</span><span class="sxs-lookup"><span data-stu-id="aa72b-109">Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="aa72b-110">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="aa72b-110">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="aa72b-111">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="aa72b-111">Run `az --version` to find the version.</span></span> <span data-ttu-id="aa72b-112">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="aa72b-112">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-your-environment"></a><span data-ttu-id="aa72b-113">準備您的環境</span><span class="sxs-lookup"><span data-stu-id="aa72b-113">Prepare your environment</span></span>

1. <span data-ttu-id="aa72b-114">在終端機視窗中執行下列命令，將範例複製到本機電腦。</span><span class="sxs-lookup"><span data-stu-id="aa72b-114">In a terminal window, run the following command to clone the sample to your local machine.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. <span data-ttu-id="aa72b-115">變更為包含範例程式碼的目錄。</span><span class="sxs-lookup"><span data-stu-id="aa72b-115">Change to the directory that contains the sample code.</span></span>

    ```bash
    cd app-service-api-node-contact-list
    ```

3. <span data-ttu-id="aa72b-116">在本機電腦上安裝 [Swaggerize](https://www.npmjs.com/package/swaggerize-express)。</span><span class="sxs-lookup"><span data-stu-id="aa72b-116">Install [Swaggerize](https://www.npmjs.com/package/swaggerize-express) on your local machine.</span></span> <span data-ttu-id="aa72b-117">Swaggerize 是一種工具，可從 Swagger 定義為您的 REST API 產生 Node.js 程式碼。</span><span class="sxs-lookup"><span data-stu-id="aa72b-117">Swaggerize is a tool that generates Node.js code for your REST API from a Swagger definition.</span></span>

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a><span data-ttu-id="aa72b-118">產生 Node.js 程式碼</span><span class="sxs-lookup"><span data-stu-id="aa72b-118">Generate Node.js code</span></span> 

<span data-ttu-id="aa72b-119">在教學課程的這一節當中，會建立 API 開發工作流程的模型，以供您在其中先建立 Swagger 中繼資料，再以此建立 (自動產生) API 伺服器程式碼的結構。</span><span class="sxs-lookup"><span data-stu-id="aa72b-119">This section of the tutorial models an API development workflow in which you create Swagger metadata first and use that to scaffold (auto-generate) server code for the API.</span></span> 

<span data-ttu-id="aa72b-120">將目錄變更為 change 資料夾，然後執行 `yo swaggerize`。</span><span class="sxs-lookup"><span data-stu-id="aa72b-120">Change directory to the *start* folder, then run `yo swaggerize`.</span></span> <span data-ttu-id="aa72b-121">Swaggerize 可從 api.json 中的 Swagger 定義，為您的 API 建立 Node.js 專案。</span><span class="sxs-lookup"><span data-stu-id="aa72b-121">Swaggerize creates a Node.js project for your API from the Swagger definition in *api.json*.</span></span>

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

<span data-ttu-id="aa72b-122">當 Swaggerize 要求提供專案名稱時，請使用 ContactList。</span><span class="sxs-lookup"><span data-stu-id="aa72b-122">When Swaggerize asks for a project name, use *ContactList*.</span></span>
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like to call this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-the-project-code"></a><span data-ttu-id="aa72b-123">自訂專案程式碼</span><span class="sxs-lookup"><span data-stu-id="aa72b-123">Customize the project code</span></span>

1. <span data-ttu-id="aa72b-124">將 lib 資料夾複製到 `yo swaggerize` 所建立的 ContactList 資料夾，然後將目錄變更為 ContactList。</span><span class="sxs-lookup"><span data-stu-id="aa72b-124">Copy the *lib* folder into the *ContactList* folder created by `yo swaggerize`, then change directory into *ContactList*.</span></span>

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. <span data-ttu-id="aa72b-125">安裝 `jsonpath` 和 `swaggerize-ui` NPM 模組。</span><span class="sxs-lookup"><span data-stu-id="aa72b-125">Install the `jsonpath` and `swaggerize-ui` NPM modules.</span></span> 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. <span data-ttu-id="aa72b-126">以下列程式碼取代 handlers/contacts.js 中的程式碼：</span><span class="sxs-lookup"><span data-stu-id="aa72b-126">Replace the code in the *handlers/contacts.js* with the following code:</span></span> 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    <span data-ttu-id="aa72b-127">此程式碼會使用 lib/contactRepository.js 所提供的 lib/contacts.json 中儲存的 JSON 資料。</span><span class="sxs-lookup"><span data-stu-id="aa72b-127">This code uses the JSON data stored in *lib/contacts.json* served by *lib/contactRepository.js*.</span></span> <span data-ttu-id="aa72b-128">新的 contacts.js 程式碼會傳回存放庫中的所有連絡人作為 JSON 酬載。</span><span class="sxs-lookup"><span data-stu-id="aa72b-128">The new *contacts.js* code returns all contacts in the repository as a JSON payload.</span></span> 

4. <span data-ttu-id="aa72b-129">以下列程式碼取代 **handlers/contacts/{id}.js** 檔案中的程式碼：</span><span class="sxs-lookup"><span data-stu-id="aa72b-129">Replace the code in the **handlers/contacts/{id}.js** file with the following code:</span></span>

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    <span data-ttu-id="aa72b-130">此程式碼可讓您使用路徑變數，只傳回具有指定之識別碼的連絡人。</span><span class="sxs-lookup"><span data-stu-id="aa72b-130">This code lets you use a path variable to return only the contact with a given ID.</span></span>

5. <span data-ttu-id="aa72b-131">以下列程式碼取代 **server.js** 中的程式碼：</span><span class="sxs-lookup"><span data-stu-id="aa72b-131">Replace the code in **server.js** with the following code:</span></span>

    ```javascript
    'use strict';

    var port = process.env.PORT || 8000; 

    var http = require('http');
    var express = require('express');
    var bodyParser = require('body-parser');
    var swaggerize = require('swaggerize-express');
    var swaggerUi = require('swaggerize-ui'); 
    var path = require('path');
    var fs = require("fs");
    
    fs.existsSync = fs.existsSync || require('path').existsSync;

    var app = express();

    var server = http.createServer(app);

    app.use(bodyParser.json());

    app.use(swaggerize({
        api: path.resolve('./config/swagger.json'),
        handlers: path.resolve('./handlers'),
        docspath: '/swagger' 
    }));

    // change four
    app.use('/docs', swaggerUi({
        docs: '/swagger'  
    }));

    server.listen(port, function () { 
    });
    ```   

    <span data-ttu-id="aa72b-132">此程式碼會進行一些小變更，讓它能與 Azure App Service 搭配運作，並為您的 API 公開互動式 Web 介面。</span><span class="sxs-lookup"><span data-stu-id="aa72b-132">This code makes some small changes to let it work with Azure App Service and exposes an interactive web interface for your API.</span></span>

### <a name="test-the-api-locally"></a><span data-ttu-id="aa72b-133">在本機測試 API</span><span class="sxs-lookup"><span data-stu-id="aa72b-133">Test the API locally</span></span>

1. <span data-ttu-id="aa72b-134">啟動 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="aa72b-134">Start up the Node.js app</span></span>
    ```bash
    npm start
    ```
    
2. <span data-ttu-id="aa72b-135">瀏覽至 http://localhost:8000/contacts 以檢視整份連絡人清單的 JSON。</span><span class="sxs-lookup"><span data-stu-id="aa72b-135">Browse to http://localhost:8000/contacts to view the JSON for the entire contact list.</span></span>
   
   ```json
    {
        "id": 1,
        "name": "Barney Poland",
        "email": "barney@contoso.com"
    },
    {
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    },
    {
        "id": 3,
        "name": "Lora Riggs",
        "email": "lora@contoso.com"
    }
   ```

3. <span data-ttu-id="aa72b-136">瀏覽至 http://localhost:8000/contacts/2 以檢視 `id` 為 2 的連絡人。</span><span class="sxs-lookup"><span data-stu-id="aa72b-136">Browse to http://localhost:8000/contacts/2 to view the contact with an `id` of two.</span></span>
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. <span data-ttu-id="aa72b-137">使用 Swagger Web 介面 (位於 http://localhost:8000/docs) 測試 API。</span><span class="sxs-lookup"><span data-stu-id="aa72b-137">Test the API using the Swagger web interface at http://localhost:8000/docs.</span></span>
   
    ![Swagger Web 介面](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <span data-ttu-id="aa72b-139"><a id="createapiapp"></a> 建立 API 應用程式</span><span class="sxs-lookup"><span data-stu-id="aa72b-139"><a id="createapiapp"></a> Create an API App</span></span>

<span data-ttu-id="aa72b-140">在本節中，您會使用 Azure CLI 2.0 建立資源，以在 Azure App Service 上裝載 API。</span><span class="sxs-lookup"><span data-stu-id="aa72b-140">In this section, you use the Azure CLI 2.0 to create the resources to host the API on Azure App Service.</span></span> 

1.  <span data-ttu-id="aa72b-141">使用 [az login](/cli/azure/#login) 命令登入 Azure 訂用帳戶並遵循畫面上的指示。</span><span class="sxs-lookup"><span data-stu-id="aa72b-141">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

    ```azurecli-interactive
    az login
    ```

2. <span data-ttu-id="aa72b-142">如果您有多個 Azure 訂用帳戶，請將預設訂用帳戶變更為所需的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="aa72b-142">If you have multiple Azure subscriptions, change the default subscription to the desired one.</span></span>

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-the-api-with-git"></a><span data-ttu-id="aa72b-143">使用 Git 部署 API</span><span class="sxs-lookup"><span data-stu-id="aa72b-143">Deploy the API with Git</span></span>

<span data-ttu-id="aa72b-144">將認可從本機 Git 存放庫推送至 Azure App Service，以將您的程式碼部署到 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="aa72b-144">Deploy your code to the API app by pushing commits from your local Git repository to Azure App Service.</span></span>

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. <span data-ttu-id="aa72b-145">在 *ContactList* 目錄中初始化新的存放庫。</span><span class="sxs-lookup"><span data-stu-id="aa72b-145">Initialize a new repo in the *ContactList* directory.</span></span> 

    ```bash
    git init .
    ```

3. <span data-ttu-id="aa72b-146">排除 npm 在本教學課程的先前步驟中從 Git 建立的 *node_modules* 目錄。</span><span class="sxs-lookup"><span data-stu-id="aa72b-146">Exclude the *node_modules* directory created by npm in an earlier step in the tutorial from Git.</span></span> <span data-ttu-id="aa72b-147">在目前的目錄中建立新的 `.gitignore` 檔案，並在檔案中任意新的一行上新增下列文字。</span><span class="sxs-lookup"><span data-stu-id="aa72b-147">Create a new `.gitignore` file in the current directory and add the following text on a new line anywhere in the file.</span></span>

    ```
    node_modules/
    ```
    <span data-ttu-id="aa72b-148">使用 `git status` 確認忽略 `node_modules` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="aa72b-148">Confirm the `node_modules` folder is being ignored with  `git status`.</span></span>

4. <span data-ttu-id="aa72b-149">認可對存放庫所做的變更。</span><span class="sxs-lookup"><span data-stu-id="aa72b-149">Commit the changes to the repo.</span></span>
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push to Azure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-the-api--in-azure"></a><span data-ttu-id="aa72b-150">在 Azure 中測試 API</span><span class="sxs-lookup"><span data-stu-id="aa72b-150">Test the API  in Azure</span></span>

1. <span data-ttu-id="aa72b-151">將瀏覽器開啟至 http://app_name.azurewebsites.net/contacts。</span><span class="sxs-lookup"><span data-stu-id="aa72b-151">Open a browser to http://app_name.azurewebsites.net/contacts.</span></span> <span data-ttu-id="aa72b-152">您會看到傳回的 JSON 與您稍早在本教學課程中於本機所做的要求相同。</span><span class="sxs-lookup"><span data-stu-id="aa72b-152">You see the same JSON returned as when you made the request locally earlier in the tutorial.</span></span>

   ```json
   {
       "id": 1,
       "name": "Barney Poland",
       "email": "barney@contoso.com"
   },
   {
       "id": 2,
       "name": "Lacy Barrera",
       "email": "lacy@contoso.com"
   },
   {
       "id": 3,
       "name": "Lora Riggs",
       "email": "lora@contoso.com"
   }
   ```

2. <span data-ttu-id="aa72b-153">在瀏覽器中移至 `http://app_name.azurewebsites.net/docs` 端點，試試在 Azure 上執行的 Swagger UI。</span><span class="sxs-lookup"><span data-stu-id="aa72b-153">In a browser, go to the `http://app_name.azurewebsites.net/docs` endpoint to try out the Swagger UI running on Azure.</span></span>

    ![Swagger Ii](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    <span data-ttu-id="aa72b-155">現在只要將認可推送至 Azure Git 存放庫，即可將範例 API 的更新部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="aa72b-155">You can now deploy updates to the sample API to Azure simply by pushing commits to the Azure Git repository.</span></span>

## <a name="clean-up"></a><span data-ttu-id="aa72b-156">清除</span><span class="sxs-lookup"><span data-stu-id="aa72b-156">Clean up</span></span>

<span data-ttu-id="aa72b-157">若要移除在本快速入門中建立的資源，請執行下列 Azure CLI 命令︰</span><span class="sxs-lookup"><span data-stu-id="aa72b-157">To clean up the resources created in this quickstart, run the following Azure CLI command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a><span data-ttu-id="aa72b-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aa72b-158">Next step</span></span> 
> [!div class="nextstepaction"]
> [<span data-ttu-id="aa72b-159">使用 CORS 從 JavaScript 用戶端取用 API 應用程式</span><span class="sxs-lookup"><span data-stu-id="aa72b-159">Consume API apps from JavaScript clients with CORS</span></span>](app-service-api-cors-consume-javascript.md)

