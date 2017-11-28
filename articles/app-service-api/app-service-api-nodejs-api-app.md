---
title: "Azure App Service 中的 aaaNode.js API 應用程式 |Microsoft 文件"
description: "深入了解如何 toocreate Node.js rest 式 API 並將它部署在 Azure App Service 中的 tooan API 應用程式。"
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
ms.openlocfilehash: 3b3229c1453b6ca4d06bef26f476e92afda4e244
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-restful-api-and-deploy-it-tooan-api-app-in-azure"></a><span data-ttu-id="49864-103">建置 Node.js rest 式 API，並將它部署在 Azure 中的 tooan API 應用程式</span><span class="sxs-lookup"><span data-stu-id="49864-103">Build a Node.js RESTful API and deploy it tooan API app in Azure</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="49864-104">本快速入門示範如何使用 Node.js 撰寫 toocreate REST API， [Express](http://expressjs.com/)，並使用[Swagger](http://swagger.io/)定義，並將它做為部署[API 應用程式](app-service-api-apps-why-best-platform.md)在 Azure 上。</span><span class="sxs-lookup"><span data-stu-id="49864-104">This quickstart shows how toocreate a REST API, written with Node.js [Express](http://expressjs.com/), using a [Swagger](http://swagger.io/) definition and deploying it as an [API app](app-service-api-apps-why-best-platform.md) on Azure.</span></span> <span data-ttu-id="49864-105">您建立使用命令列工具的 hello 應用程式、 設定資源以 hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)，及部署使用 Git hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="49864-105">You create hello app using command-line tools, configure resources with hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and deploy hello app using Git.</span></span>  <span data-ttu-id="49864-106">當您完成後，您必須在 Azure 上執行工作範例 REST API。</span><span class="sxs-lookup"><span data-stu-id="49864-106">When you've finished, you have a working sample REST API running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="49864-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="49864-107">Prerequisites</span></span>

* [<span data-ttu-id="49864-108">Git</span><span class="sxs-lookup"><span data-stu-id="49864-108">Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="49864-109"> 安裝 Node.js 和 NPM</span><span class="sxs-lookup"><span data-stu-id="49864-109">Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="49864-110">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="49864-110">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="49864-111">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="49864-111">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="49864-112">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="49864-112">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-your-environment"></a><span data-ttu-id="49864-113">準備您的環境</span><span class="sxs-lookup"><span data-stu-id="49864-113">Prepare your environment</span></span>

1. <span data-ttu-id="49864-114">在終端機視窗中，執行下列命令 tooclone hello 範例 tooyour 本機電腦的 hello。</span><span class="sxs-lookup"><span data-stu-id="49864-114">In a terminal window, run hello following command tooclone hello sample tooyour local machine.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. <span data-ttu-id="49864-115">變更 toohello 目錄，包含 hello 範例程式碼。</span><span class="sxs-lookup"><span data-stu-id="49864-115">Change toohello directory that contains hello sample code.</span></span>

    ```bash
    cd app-service-api-node-contact-list
    ```

3. <span data-ttu-id="49864-116">在本機電腦上安裝 [Swaggerize](https://www.npmjs.com/package/swaggerize-express)。</span><span class="sxs-lookup"><span data-stu-id="49864-116">Install [Swaggerize](https://www.npmjs.com/package/swaggerize-express) on your local machine.</span></span> <span data-ttu-id="49864-117">Swaggerize 是一種工具，可從 Swagger 定義為您的 REST API 產生 Node.js 程式碼。</span><span class="sxs-lookup"><span data-stu-id="49864-117">Swaggerize is a tool that generates Node.js code for your REST API from a Swagger definition.</span></span>

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a><span data-ttu-id="49864-118">產生 Node.js 程式碼</span><span class="sxs-lookup"><span data-stu-id="49864-118">Generate Node.js code</span></span> 

<span data-ttu-id="49864-119">本節 hello 教學課程的模型中的方法，您可以先建立 Swagger 中繼資料，並使用該 tooscaffold API 開發工作流程 （自動產生） hello API 伺服端程式碼。</span><span class="sxs-lookup"><span data-stu-id="49864-119">This section of hello tutorial models an API development workflow in which you create Swagger metadata first and use that tooscaffold (auto-generate) server code for hello API.</span></span> 

<span data-ttu-id="49864-120">變更目錄 toohello*啟動*資料夾，然後執行`yo swaggerize`。</span><span class="sxs-lookup"><span data-stu-id="49864-120">Change directory toohello *start* folder, then run `yo swaggerize`.</span></span> <span data-ttu-id="49864-121">Swaggerize 為您的 API，從 hello Swagger 定義中建立 Node.js 專案*api.json*。</span><span class="sxs-lookup"><span data-stu-id="49864-121">Swaggerize creates a Node.js project for your API from hello Swagger definition in *api.json*.</span></span>

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

<span data-ttu-id="49864-122">當 Swaggerize 要求提供專案名稱時，請使用 ContactList。</span><span class="sxs-lookup"><span data-stu-id="49864-122">When Swaggerize asks for a project name, use *ContactList*.</span></span>
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like toocall this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-hello-project-code"></a><span data-ttu-id="49864-123">自訂 hello 專案程式碼</span><span class="sxs-lookup"><span data-stu-id="49864-123">Customize hello project code</span></span>

1. <span data-ttu-id="49864-124">複製 hello *lib*資料夾 hello *ContactList*所建立的資料夾`yo swaggerize`，然後變更目錄到*ContactList*。</span><span class="sxs-lookup"><span data-stu-id="49864-124">Copy hello *lib* folder into hello *ContactList* folder created by `yo swaggerize`, then change directory into *ContactList*.</span></span>

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. <span data-ttu-id="49864-125">安裝 hello`jsonpath`和`swaggerize-ui`NPM 模組。</span><span class="sxs-lookup"><span data-stu-id="49864-125">Install hello `jsonpath` and `swaggerize-ui` NPM modules.</span></span> 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. <span data-ttu-id="49864-126">Hello 中的 hello 程式碼取代*handlers/contacts.js*以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="49864-126">Replace hello code in hello *handlers/contacts.js* with hello following code:</span></span> 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    <span data-ttu-id="49864-127">此程式碼使用 hello JSON 資料儲存於*lib/contacts.json*由*lib/contactRepository.js*。</span><span class="sxs-lookup"><span data-stu-id="49864-127">This code uses hello JSON data stored in *lib/contacts.json* served by *lib/contactRepository.js*.</span></span> <span data-ttu-id="49864-128">新的 hello *contacts.js*程式碼會傳回所有連絡人 hello 做為 JSON 裝載的儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="49864-128">hello new *contacts.js* code returns all contacts in hello repository as a JSON payload.</span></span> 

4. <span data-ttu-id="49864-129">Hello 中的 hello 程式碼取代**handlers/contacts/{id}.js**檔案以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="49864-129">Replace hello code in hello **handlers/contacts/{id}.js** file with hello following code:</span></span>

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    <span data-ttu-id="49864-130">此程式碼可讓您使用路徑變數 tooreturn 只有 hello 連絡人，並提供指定的識別碼。</span><span class="sxs-lookup"><span data-stu-id="49864-130">This code lets you use a path variable tooreturn only hello contact with a given ID.</span></span>

5. <span data-ttu-id="49864-131">中的 hello 程式碼取代**立即轉譯 server.js**以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="49864-131">Replace hello code in **server.js** with hello following code:</span></span>

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

    <span data-ttu-id="49864-132">這個程式碼可讓它與服務搭配使用 Azure 應用程式部分進行小變更 toolet 並公開 api 的互動的 web 介面。</span><span class="sxs-lookup"><span data-stu-id="49864-132">This code makes some small changes toolet it work with Azure App Service and exposes an interactive web interface for your API.</span></span>

### <a name="test-hello-api-locally"></a><span data-ttu-id="49864-133">測試 hello API 本機</span><span class="sxs-lookup"><span data-stu-id="49864-133">Test hello API locally</span></span>

1. <span data-ttu-id="49864-134">啟動 hello Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="49864-134">Start up hello Node.js app</span></span>
    ```bash
    npm start
    ```
    
2. <span data-ttu-id="49864-135">瀏覽 toohttp://localhost:8000 / 連絡 tooview hello JSON hello 整個連絡人清單。</span><span class="sxs-lookup"><span data-stu-id="49864-135">Browse toohttp://localhost:8000/contacts tooview hello JSON for hello entire contact list.</span></span>
   
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

3. <span data-ttu-id="49864-136">瀏覽 toohttp://localhost:8000/連絡人/2 tooview hello 與連絡`id`兩個。</span><span class="sxs-lookup"><span data-stu-id="49864-136">Browse toohttp://localhost:8000/contacts/2 tooview hello contact with an `id` of two.</span></span>
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. <span data-ttu-id="49864-137">測試 hello API: //localhost: 8000/文件在使用 hello Swagger web 介面。</span><span class="sxs-lookup"><span data-stu-id="49864-137">Test hello API using hello Swagger web interface at http://localhost:8000/docs.</span></span>
   
    ![Swagger Web 介面](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <span data-ttu-id="49864-139"><a id="createapiapp"></a> 建立 API 應用程式</span><span class="sxs-lookup"><span data-stu-id="49864-139"><a id="createapiapp"></a> Create an API App</span></span>

<span data-ttu-id="49864-140">在本節中，您可以使用 hello Azure CLI 2.0 toocreate hello 資源 toohost hello API Azure App Service 上。</span><span class="sxs-lookup"><span data-stu-id="49864-140">In this section, you use hello Azure CLI 2.0 toocreate hello resources toohost hello API on Azure App Service.</span></span> 

1.  <span data-ttu-id="49864-141">登入 Azure 訂用帳戶以 hello tooyour [az 登入](/cli/azure/#login)命令，並遵循螢幕上指示 hello。</span><span class="sxs-lookup"><span data-stu-id="49864-141">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

    ```azurecli-interactive
    az login
    ```

2. <span data-ttu-id="49864-142">如果您有多個 Azure 訂用帳戶時，變更 hello 預設訂用帳戶 toohello 預期其中一個。</span><span class="sxs-lookup"><span data-stu-id="49864-142">If you have multiple Azure subscriptions, change hello default subscription toohello desired one.</span></span>

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-hello-api-with-git"></a><span data-ttu-id="49864-143">部署含 Git 的 hello API</span><span class="sxs-lookup"><span data-stu-id="49864-143">Deploy hello API with Git</span></span>

<span data-ttu-id="49864-144">部署應用程式開發介面應用程式程式碼 toohello 推送認可從您本機 Git 儲存機制 tooAzure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="49864-144">Deploy your code toohello API app by pushing commits from your local Git repository tooAzure App Service.</span></span>

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. <span data-ttu-id="49864-145">初始化新的儲存機制中 hello *ContactList*目錄。</span><span class="sxs-lookup"><span data-stu-id="49864-145">Initialize a new repo in hello *ContactList* directory.</span></span> 

    ```bash
    git init .
    ```

3. <span data-ttu-id="49864-146">排除 hello *node_modules* npm 中先前的步驟從 Git hello 教學課程中建立目錄。</span><span class="sxs-lookup"><span data-stu-id="49864-146">Exclude hello *node_modules* directory created by npm in an earlier step in hello tutorial from Git.</span></span> <span data-ttu-id="49864-147">建立新`.gitignore`hello 目前目錄中檔案，然後加入 hello hello 檔案中的任何位置在新行上下列文字。</span><span class="sxs-lookup"><span data-stu-id="49864-147">Create a new `.gitignore` file in hello current directory and add hello following text on a new line anywhere in hello file.</span></span>

    ```
    node_modules/
    ```
    <span data-ttu-id="49864-148">確認 hello`node_modules`與，正在略過資料夾`git status`。</span><span class="sxs-lookup"><span data-stu-id="49864-148">Confirm hello `node_modules` folder is being ignored with  `git status`.</span></span>

4. <span data-ttu-id="49864-149">認可 hello 變更 toohello 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="49864-149">Commit hello changes toohello repo.</span></span>
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push tooAzure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-hello-api--in-azure"></a><span data-ttu-id="49864-150">在 Azure 中的測試 hello 應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="49864-150">Test hello API  in Azure</span></span>

1. <span data-ttu-id="49864-151">開啟瀏覽器 toohttp://app_name.azurewebsites.net/contacts。</span><span class="sxs-lookup"><span data-stu-id="49864-151">Open a browser toohttp://app_name.azurewebsites.net/contacts.</span></span> <span data-ttu-id="49864-152">您會看到相同的 JSON 做為您進行傳回 hello 要求在本機上稍早在 hello 教學課程中的 hello。</span><span class="sxs-lookup"><span data-stu-id="49864-152">You see hello same JSON returned as when you made hello request locally earlier in hello tutorial.</span></span>

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

2. <span data-ttu-id="49864-153">在瀏覽器，移 toohello`http://app_name.azurewebsites.net/docs`端點 tootry 出 hello Swagger UI 在 Azure 上執行。</span><span class="sxs-lookup"><span data-stu-id="49864-153">In a browser, go toohello `http://app_name.azurewebsites.net/docs` endpoint tootry out hello Swagger UI running on Azure.</span></span>

    ![Swagger Ii](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    <span data-ttu-id="49864-155">您現在可以部署更新 toohello 範例應用程式開發介面 tooAzure 只要推送認可 toohello Azure Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="49864-155">You can now deploy updates toohello sample API tooAzure simply by pushing commits toohello Azure Git repository.</span></span>

## <a name="clean-up"></a><span data-ttu-id="49864-156">清除</span><span class="sxs-lookup"><span data-stu-id="49864-156">Clean up</span></span>

<span data-ttu-id="49864-157">本快速入門，執行下列 Azure CLI 命令的 hello 建立 hello 資源 tooclean:</span><span class="sxs-lookup"><span data-stu-id="49864-157">tooclean up hello resources created in this quickstart, run hello following Azure CLI command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a><span data-ttu-id="49864-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="49864-158">Next step</span></span> 
> [!div class="nextstepaction"]
> [<span data-ttu-id="49864-159">使用 CORS 從 JavaScript 用戶端取用 API 應用程式</span><span class="sxs-lookup"><span data-stu-id="49864-159">Consume API apps from JavaScript clients with CORS</span></span>](app-service-api-cors-consume-javascript.md)

