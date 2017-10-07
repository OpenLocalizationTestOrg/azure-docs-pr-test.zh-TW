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
# <a name="build-a-nodejs-restful-api-and-deploy-it-tooan-api-app-in-azure"></a>建置 Node.js rest 式 API，並將它部署在 Azure 中的 tooan API 應用程式
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

本快速入門示範如何使用 Node.js 撰寫 toocreate REST API， [Express](http://expressjs.com/)，並使用[Swagger](http://swagger.io/)定義，並將它做為部署[API 應用程式](app-service-api-apps-why-best-platform.md)在 Azure 上。 您建立使用命令列工具的 hello 應用程式、 設定資源以 hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)，及部署使用 Git hello 應用程式。  當您完成後，您必須在 Azure 上執行工作範例 REST API。

## <a name="prerequisites"></a>必要條件

* [Git](https://git-scm.com/)
* [ 安裝 Node.js 和 NPM](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="prepare-your-environment"></a>準備您的環境

1. 在終端機視窗中，執行下列命令 tooclone hello 範例 tooyour 本機電腦的 hello。

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. 變更 toohello 目錄，包含 hello 範例程式碼。

    ```bash
    cd app-service-api-node-contact-list
    ```

3. 在本機電腦上安裝 [Swaggerize](https://www.npmjs.com/package/swaggerize-express)。 Swaggerize 是一種工具，可從 Swagger 定義為您的 REST API 產生 Node.js 程式碼。

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a>產生 Node.js 程式碼 

本節 hello 教學課程的模型中的方法，您可以先建立 Swagger 中繼資料，並使用該 tooscaffold API 開發工作流程 （自動產生） hello API 伺服端程式碼。 

變更目錄 toohello*啟動*資料夾，然後執行`yo swaggerize`。 Swaggerize 為您的 API，從 hello Swagger 定義中建立 Node.js 專案*api.json*。

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

當 Swaggerize 要求提供專案名稱時，請使用 ContactList。
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like toocall this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-hello-project-code"></a>自訂 hello 專案程式碼

1. 複製 hello *lib*資料夾 hello *ContactList*所建立的資料夾`yo swaggerize`，然後變更目錄到*ContactList*。

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. 安裝 hello`jsonpath`和`swaggerize-ui`NPM 模組。 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. Hello 中的 hello 程式碼取代*handlers/contacts.js*以下列程式碼的 hello: 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    此程式碼使用 hello JSON 資料儲存於*lib/contacts.json*由*lib/contactRepository.js*。 新的 hello *contacts.js*程式碼會傳回所有連絡人 hello 做為 JSON 裝載的儲存機制中。 

4. Hello 中的 hello 程式碼取代**handlers/contacts/{id}.js**檔案以下列程式碼的 hello:

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    此程式碼可讓您使用路徑變數 tooreturn 只有 hello 連絡人，並提供指定的識別碼。

5. 中的 hello 程式碼取代**立即轉譯 server.js**以下列程式碼的 hello:

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

    這個程式碼可讓它與服務搭配使用 Azure 應用程式部分進行小變更 toolet 並公開 api 的互動的 web 介面。

### <a name="test-hello-api-locally"></a>測試 hello API 本機

1. 啟動 hello Node.js 應用程式
    ```bash
    npm start
    ```
    
2. 瀏覽 toohttp://localhost:8000 / 連絡 tooview hello JSON hello 整個連絡人清單。
   
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

3. 瀏覽 toohttp://localhost:8000/連絡人/2 tooview hello 與連絡`id`兩個。
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. 測試 hello API: //localhost: 8000/文件在使用 hello Swagger web 介面。
   
    ![Swagger Web 介面](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <a id="createapiapp"></a> 建立 API 應用程式

在本節中，您可以使用 hello Azure CLI 2.0 toocreate hello 資源 toohost hello API Azure App Service 上。 

1.  登入 Azure 訂用帳戶以 hello tooyour [az 登入](/cli/azure/#login)命令，並遵循螢幕上指示 hello。

    ```azurecli-interactive
    az login
    ```

2. 如果您有多個 Azure 訂用帳戶時，變更 hello 預設訂用帳戶 toohello 預期其中一個。

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-hello-api-with-git"></a>部署含 Git 的 hello API

部署應用程式開發介面應用程式程式碼 toohello 推送認可從您本機 Git 儲存機制 tooAzure 應用程式服務。

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. 初始化新的儲存機制中 hello *ContactList*目錄。 

    ```bash
    git init .
    ```

3. 排除 hello *node_modules* npm 中先前的步驟從 Git hello 教學課程中建立目錄。 建立新`.gitignore`hello 目前目錄中檔案，然後加入 hello hello 檔案中的任何位置在新行上下列文字。

    ```
    node_modules/
    ```
    確認 hello`node_modules`與，正在略過資料夾`git status`。

4. 認可 hello 變更 toohello 儲存機制。
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push tooAzure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-hello-api--in-azure"></a>在 Azure 中的測試 hello 應用程式開發介面

1. 開啟瀏覽器 toohttp://app_name.azurewebsites.net/contacts。 您會看到相同的 JSON 做為您進行傳回 hello 要求在本機上稍早在 hello 教學課程中的 hello。

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

2. 在瀏覽器，移 toohello`http://app_name.azurewebsites.net/docs`端點 tootry 出 hello Swagger UI 在 Azure 上執行。

    ![Swagger Ii](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    您現在可以部署更新 toohello 範例應用程式開發介面 tooAzure 只要推送認可 toohello Azure Git 儲存機制。

## <a name="clean-up"></a>清除

本快速入門，執行下列 Azure CLI 命令的 hello 建立 hello 資源 tooclean:

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a>後續步驟 
> [!div class="nextstepaction"]
> [使用 CORS 從 JavaScript 用戶端取用 API 應用程式](app-service-api-cors-consume-javascript.md)

