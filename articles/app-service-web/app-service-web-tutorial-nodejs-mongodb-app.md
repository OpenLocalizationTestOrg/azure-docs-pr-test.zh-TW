---
title: "aaaBuild Node.js 和 MongoDB web 應用程式在 Azure 中 |Microsoft 文件"
description: "深入了解如何 tooget Node.js 應用程式在 Azure 中工作，與連接 tooa Cosmos DB 資料庫使用 MongoDB 連接字串。"
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 0b4d7d0e-e984-49a1-a57a-3c0caa955f0e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 532251c51ed6f8513e6e366393e889b67a85e5b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a>在 Azure 中建置 Node.js 和 MongoDB Web 應用程式

Azure Web Apps 提供可高度擴充、自我修復的 Web 主機服務。 本教學課程會示範如何 toocreate Node.js web 應用程式在 Azure 中的，並將它連接 tooa MongoDB 資料庫。 完成之後，您的 MEAN 應用程式 (MongoDB、Express、AngularJS 及 Node.js) 將會在 [Azure App Service](app-service-web-overview.md) 中執行。 為了簡單起見，hello 範例應用程式使用 hello [MEAN.js web 架構](http://meanjs.org/)。

![在 Azure App Service 中執行的 MEAN.js 應用程式](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

您將學到什麼：

> [!div class="checklist"]
> * 在 Azure 中建立 MongoDB 資料庫
> * 連接 Node.js 應用程式 tooMongoDB
> * 部署 hello 應用程式 tooAzure
> * 更新 hello 資料模型，部署 hello 應用程式
> * 來自 Azure 的串流診斷記錄
> * 管理 hello hello Azure 入口網站中的應用程式

## <a name="prerequisites"></a>必要條件

toocomplete 本教學課程：

1. [安裝 Git](https://git-scm.com/)
1. [安裝 Node.js 和 NPM](https://nodejs.org/)
1. [安裝 Gulp.js](http://gulpjs.com/) ([MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started) 的必要項目)
1. [安裝及執行 MongoDB Community 版本](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="test-local-mongodb"></a>測試本機的 MongoDB

開啟 hello 終端機視窗和`cd`toohello `bin` MongoDB 安裝目錄。 您可以使用這個終端機視窗 toorun hello 的所有命令，在本教學課程。

執行`mongo`hello 終端機 tooconnect tooyour 本機 MongoDB 伺服器中。

```bash
mongo
```

如果連接成功，則您的 MongoDB 資料庫已在執行中。 如果沒有，請確定您的本機 MongoDB 資料庫已啟動在 hello 步驟[安裝 MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/)。 通常，MongoDB 已安裝，但您仍然需要 toostart 它藉由執行`mongod`。 

當您完成測試 MongoDB 資料庫中，輸入`Ctrl+C`hello 終端機中。 

## <a name="create-local-nodejs-app"></a>建立本機的 Node.js 應用程式

在此步驟中，您會將設定 hello 本機 Node.js 專案。

### <a name="clone-hello-sample-application"></a>複製 hello 範例應用程式

在 hello 終端機視窗， `cd` tooa 工作目錄。  

執行下列命令 tooclone hello 範例儲存機制的 hello。 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

這個範例儲存機制包含一份 hello [MEAN.js 儲存機制](https://github.com/meanjs/mean)。 它會修改的 toorun App Service 上 (如需詳細資訊，請參閱 hello MEAN.js 儲存機制[讀我檔案](https://github.com/Azure-Samples/meanjs/blob/master/README.md))。

### <a name="run-hello-application"></a>執行 hello 應用程式

執行下列命令 tooinstall hello 所需封裝的 hello 和啟動 hello 應用程式。

```bash
cd meanjs
npm install
npm start
```

完全載入 hello 應用程式時，您會看到下列訊息類似 toohello:

```
--
MEAN.JS - Development Environment

Environment:     development
Server:          http://0.0.0.0:3000
Database:        mongodb://localhost/mean-dev
App version:     0.5.0
MEAN.JS version: 0.5.0
--
```

瀏覽 toohttp://localhost:3000 瀏覽器中。 按一下**註冊**入 hello 上方的功能表，並建立測試使用者。 

hello MEAN.js 範例應用程式會將使用者資料儲存在 hello 資料庫。 如果您在建立使用者和登入成功時，您的應用程式會撰寫資料 toohello 本機 MongoDB 資料庫。

![MEAN.js 順利連線 tooMongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

選取**Admin > 管理文件**tooadd 某些文件。

toostop Node.js，也可以隨時按`Ctrl+C`hello 終端機中。 

## <a name="create-production-mongodb"></a>建立生產環境 MongoDB

在此步驟中，您要在 Azure 中建立 MongoDB 資料庫。 已部署的 tooAzure 您的應用程式時，它會使用此雲端的資料庫。

針對 MongoDB，本教學課程使用 [Azure Cosmos DB](/azure/documentdb/)。 Cosmos DB 支援 MongoDB 用戶端連線。

### <a name="log-in-tooazure"></a>登入 tooAzure

您將在 Azure 中使用 Azure CLI 2.0 hello toocreate hello 所需資源 toohost 您的應用程式。 登入 Azure 訂用帳戶以 hello tooyour [az 登入](/cli/azure/#login)命令，並遵循螢幕上指示 hello。

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a>建立資源群組

建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

hello 下列範例會建立資源群組中 hello 西歐地區。

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

使用 hello [az appservice 列出位置](/cli/azure/appservice#list-locations)Azure CLI 命令 toolist 可用的位置。 

### <a name="create-a-cosmos-db-account"></a>建立 Cosmos DB 帳戶

建立以 hello Cosmos DB 帳戶[az cosmosdb 建立](/cli/azure/cosmosdb#create)命令。

在 hello 下列命令，以取代 hello 的唯一 Cosmos DB 名稱 *\<cosmosdb_name >*預留位置。 這個名稱會當做 hello 一部分 hello Cosmos DB 端點， `https://<cosmosdb_name>.documents.azure.com/`，因此 hello 名稱需要 toobe 唯一跨所有 Cosmos DB 帳戶在 Azure 中。 hello 名稱必須包含小寫字母、 數字和 hello 連字號 （-） 字元，且必須介於 3 到 50 個字元之間。

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

hello *-kind MongoDB*參數可啟用 MongoDB 用戶端連線。

建立 hello Cosmos DB 帳戶時，hello Azure CLI 顯示資訊的類似 toohello 下列範例：

```json
{
  "consistencyPolicy":
  {
    "defaultConsistencyLevel": "Session",
    "maxIntervalInSeconds": 5,
    "maxStalenessPrefix": 100
  },
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb_name>.documents.azure.com:443/",
  "failoverPolicies": 
  ...
  < Output truncated for readability >
}
```

## <a name="connect-app-tooproduction-mongodb"></a>連接應用程式 tooproduction MongoDB

在此步驟中，您可以連接 MEAN.js 範例應用程式 toohello Cosmos DB 資料庫您剛剛建立，使用 MongoDB 連接字串。 

### <a name="retrieve-hello-database-key"></a>擷取 hello 資料庫金鑰

tooconnect toohello Cosmos DB 資料庫，您必須 hello 資料庫金鑰。 使用 hello [az cosmosdb 清單索引鍵](/cli/azure/cosmosdb#list-keys)命令 tooretrieve hello 主索引鍵。

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

hello Azure CLI 顯示資訊的類似 toohello 下列範例：

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

複製 hello 值`primaryMasterKey`。 您需要這個 hello 下一個步驟中的資訊。

<a name="devconfig"></a>
### <a name="configure-hello-connection-string-in-your-nodejs-application"></a>Node.js 應用程式中設定 hello 連接字串

在您的 MEAN.js 存放庫中，開啟 _config/env/production.js_。

在 hello`db`物件，更新 hello 值`uri`:

* 取代 hello 兩 *\<cosmosdb_name >*預留位置取代您 Cosmos DB 的資料庫名稱。
* 取代 hello  *\<primary_master_key >*預留位置 hello hello 先前步驟中複製的索引鍵。

hello 下列程式碼顯示 hello`db`物件：

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

hello`ssl=true`選項是必要的因為[Cosmos DB 需要 SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements)。 

儲存您的變更。

### <a name="test-hello-application-in-production-mode"></a>在實際執行模式中測試 hello 應用程式 

執行下列命令 toominify 和組合指令碼 hello 的生產環境的 hello。 此程序會產生所需的 hello 實際執行環境的 hello 檔案。

```bash
gulp prod
```

執行下列命令 toouse hello 您在設定連接字串的 hello _config/env/production.js_。

```bash
NODE_ENV=production node server.js
```

`NODE_ENV=production`設定告知 Node.js toorun hello 實際執行環境中的 hello 環境變數。  `node server.js`啟動 hello Node.js 伺服器和`server.js`儲存機制根目錄中。 這是在 Azure 中載入 Node.js 應用程式的方式。 

載入 hello 應用程式時，請檢查 toomake 確定 hello 實際執行環境中執行它：

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

瀏覽 toohttp://localhost:8443 瀏覽器中。 按一下**註冊**入 hello 上方的功能表，並建立測試使用者。 如果您成功建立使用者和登入，您的應用程式會在 Azure 中撰寫資料 toohello Cosmos DB 資料庫。 

在終端機 hello，請輸入，Node.js 停止`Ctrl+C`。 

## <a name="deploy-app-tooazure"></a>部署應用程式 tooAzure

在此步驟中，您可以部署您 MongoDB 連接 Node.js 應用程式 tooAzure 應用程式服務。

### <a name="create-an-app-service-plan"></a>建立應用程式服務方案

建立應用程式服務方案以 hello [az 應用程式服務方案建立](/cli/azure/appservice/plan#create)命令。 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

hello 下列範例會建立名為 App Service 方案_myAppServicePlan_使用 hello**免費**定價層：

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

建立 hello 應用程式服務方案時，hello Azure CLI 顯示資訊的類似 toohello 下列範例：

```json 
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
```

### <a name="create-a-web-app"></a>建立 Web 應用程式

建立 web 應用程式在 hello`myAppServicePlan`應用程式服務方案以 hello [az webapp 建立](/cli/azure/webapp#create)命令。 

hello web 應用程式可讓您裝載空間 toodeploy 您的程式碼和為您提供 URL tooview hello 部署應用程式。 使用 toocreate hello web 應用程式。 

在 hello 下列命令，將取代 hello  *\<app_name >*具有唯一的應用程式名稱的預留位置。 這個名稱會做為 hello hello 預設 URL 的一部分 hello web 應用程式，因此 hello 名稱需要 toobe 唯一跨 Azure App Service 中的所有應用程式。 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

Hello web 應用程式建立後，hello Azure CLI 顯示資訊的類似 toohello 下列範例： 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-an-environment-variable"></a>設定環境變數

稍早在 hello 教學課程，您硬式編碼 hello 資料庫連接字串中_config/env/production.js_。 為了保持安全性最佳作法，想要 tookeep 這個敏感性資料從您的 Git 儲存機制。 為了在 Azure 中執行應用程式，您將改用環境變數。

在應用程式服務中，您設定環境變數為_應用程式設定_使用 hello [az webapp config appsettings 更新](/cli/azure/webapp/config/appsettings#update)命令。 

hello 下列範例會設定`MONGODB_URI`Azure web 應用程式中的應用程式設定。 取代 hello  *\<app_name >*，  *\<cosmosdb_name >*，和 *\<primary_master_key >*預留位置。

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

在 Node.js 程式碼中，您可以利用 `process.env.MONGODB_URI` 來存取此應用程式設定，就像存取任何環境變數一樣。 

現在，復原變更 too_config/env/production.js_ 以 hello 下列命令：

```bash
git checkout -- .
```

再次開啟 _config/env/production.js_。 請注意該 hello 預設 MEAN.js 應用程式已設定的 toouse hello`MONGODB_URI`您建立的環境變數。

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a>設定本機 git 部署 

使用 hello [az webapp 部署使用者集合](/cli/azure/webapp/deployment/user#set)命令 toocreate 認證進行部署。

您可以部署您的應用程式 tooAzure 應用程式服務，以各種方式，包括 FTP、 本機 Git、 GitHub、 Visual Studio Team Services 和 BitBucket。 若為 FTP 和本機 Git，則需要您的部署 hello 伺服器 tooauthenticate toohave 部署使用者設定。 此部署使用者是帳戶層級，與 Azure 訂用帳戶的帳戶不同。 您只需要 tooconfigure 這個部署使用者一次。

下列命令，取代在 hello *\<使用者名稱 >*和*\<密碼 >*與新的使用者名稱和密碼。 hello 使用者名稱必須是唯一的。 hello 密碼必須至少為八個字元，以下列三個元素的 hello 的兩個： 字母、 數字、 符號。 如果您收到` 'Conflict'. Details: 409`錯誤，變更 hello 使用者名稱。 如果您收到 ` 'Bad Request'. Details: 400` 錯誤，請使用更強的密碼。

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

記錄 hello 使用者名稱和密碼，以在稍後的步驟，當您部署的 hello 應用程式中使用。

使用 hello [az webapp 部署來源設定為本機的 git](/cli/azure/webapp/deployment/source#config-local-git)命令 tooconfigure 本機 Git 存取 toohello Azure web 應用程式。 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

Hello 部署使用者設定時，Azure CLI hello 會顯示 hello Azure web 應用程式的部署 URL 中 hello 下列格式：

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

因為它會使用 hello 下一個步驟中複製 hello hello 終端機中，從輸出。 

### <a name="push-tooazure-from-git"></a>從 Git 推送 tooAzure

新增 Azure 遠端 tooyour 本機 Git 儲存機制。 

```bash
git remote add azure <paste_copied_url_here> 
```

推送 toohello Azure 遠端 toodeploy Node.js 應用程式。 安裝程式將會提示您稍早提供一部分 hello hello 部署使用者建立的 hello 密碼。 

```bash
git push azure master
```

在部署期間，Azure App Service 會與 Git 溝通其進度。

```bash
Counting objects: 5, done.
Delta compression using up too4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 489 bytes | 0 bytes/s, done.
Total 5 (delta 3), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '6c7c716eee'.
remote: Running custom deployment command...
remote: Running deployment command...
remote: Handling node.js deployment.
.
.
.
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

您可能會注意到 hello 部署程序執行[Gulp](http://gulpjs.com/)之後`npm install`。 應用程式服務不會在部署期間執行 Gulp 或 grunt 所完成的工作，因此這個範例儲存機制具有兩個額外的檔案其根目錄 tooenable 它： 

- _.deployment_ -此檔案會告知應用程式服務 toorun `bash deploy.sh` hello 自訂部署指令碼。
- _deploy.sh_ -hello 自訂部署指令碼。 如果您檢閱 hello 檔案時，您會看到應用程式會執行`gulp prod`之後`npm install`和`bower install`。 

您可以使用此方法 tooadd 任何步驟 tooyour Git 為基礎的部署。 如果您在任一時間點重新啟動 Azure Web 應用程式，App Service 並不會重新執行這些自動化工作。

### <a name="browse-toohello-azure-web-app"></a>瀏覽 toohello Azure web 應用程式 

瀏覽使用網頁瀏覽器 toohello 部署 web 應用程式。 

```bash 
http://<app_name>.azurewebsites.net 
``` 

按一下**註冊**入 hello 上方的功能表，並建立虛擬使用者。 

如果您為成功，而且 hello 應用程式會自動登入 toohello 在 Azure 中建立使用者，然後 MEAN.js 應用程式都有連線能力 toohello MongoDB (Cosmos DB) 資料庫。 

![在 Azure App Service 中執行的 MEAN.js 應用程式](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

選取**Admin > 管理文件**tooadd 某些文件。 

**恭喜！** 您正在 Azure App Service 中執行資料驅動的 Node.js 應用程式。

## <a name="update-data-model-and-redeploy"></a>更新資料模型並重新部署

在此步驟中，您可以變更 hello`article`資料模型，並發行變更 tooAzure。

### <a name="update-hello-data-model"></a>更新 hello 資料模型

開啟 _modules/articles/server/models/article.server.model.js_。

在 `ArticleSchema` 中，新增名為 `comment` 的 `String` 類型。 完成時，您的結構描述程式碼應該如下所示：

```javascript
var ArticleSchema = new Schema({
  ...,
  user: {
    type: Schema.ObjectId,
    ref: 'User'
  },
  comment: {
    type: String,
    default: '',
    trim: true
  }
});
```

### <a name="update-hello-articles-code"></a>更新 hello 文件的程式碼

更新的 hello rest 您`articles`程式碼 toouse `comment`。

有五個檔案，您需要 toomodify: hello 伺服器控制器和 hello 四個用戶端檢視。 

開啟 _modules/articles/server/controllers/articles.server.controller.js_。

在 hello`update`函式中，新增的指派`article.comment`。 hello 下列程式碼顯示 hello 完成`update`函式：

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

開啟 _modules/articles/client/views/view-article.client.view.html_。

正上方 hello 右`</section>`標記中加入下列行 toodisplay hello`comment`連同其他部分 hello hello 發行項資料：

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

開啟 _modules/articles/client/views/list-articles.client.view.html_。

正上方 hello 右`</a>`標記中加入下列行 toodisplay hello`comment`連同其他部分 hello hello 發行項資料：

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

開啟 _modules/articles/client/views/admin/list-articles.client.view.html_。

內部 hello`<div class="list-group">`元素與 hello 結尾的正上方`</a>`標記中加入下列行 toodisplay hello`comment`連同其他部分 hello hello 發行項資料：

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

開啟 _modules/articles/client/views/admin/form-article.client.view.html_。

尋找 hello`<div class="form-group">`包含 hello 送出按鈕，像這樣的項目：

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

此標記的正上方加入另一個`<div class="form-group">`項目，可讓人員編輯 hello`comment`欄位。 新的元素應該如下所示：

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a>本機測試您的變更

儲存您的所有變更。

再次在生產模式中測試您的變更。

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> 請記住，您_config/env/production.js_已還原，和 hello `MONGODB_URI` Azure web 應用程式中，而不是在本機電腦，才會設定環境變數。 如果您看一下 hello 設定檔，您會發現該 hello production 組態預設值 toouse 本機 MongoDB 資料庫。 如此可確保當您在本機測試程式碼變更時，不會碰觸到生產資料。

瀏覽過`http://localhost:8443`瀏覽器中，並確定您已登入。

選取**Admin > 管理文件**，然後加入發行項藉由選取 hello  **+**   按鈕。

您會看見 hello 新`Comment`現在文字方塊。

![加入註解欄位 tooArticles](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

在終端機 hello，請輸入，Node.js 停止`Ctrl+C`。 

### <a name="publish-changes-tooazure"></a>發行變更 tooAzure

認可您的變更在 Git，然後推送 hello 程式碼變更 tooAzure。

```bash
git commit -am "added article comment"
git push azure master
```

一次 hello`git push`已完成，請瀏覽 tooyour Azure web 應用程式並再試一次 hello 新功能。

![發行 tooAzure 模型與資料庫的變更。](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

如果您先前已新增任何文章，您仍然可以看到它們。 Cosmos DB 中的現有資料不會遺失。 此外，您更新 toohello 資料的結構描述，會保留現有的資料。

## <a name="stream-diagnostic-logs"></a>資料流診斷記錄 

Node.js 應用程式執行的 Azure 應用程式服務，而您可以取得 hello 主控台記錄檔傳送的 tooyour 終端機。 這樣一來，您可以取得 hello 相同的診斷訊息 toohelp 您偵錯應用程式錯誤。

資料流中，使用 hello toostart 記錄[az webapp 記錄結尾](/cli/azure/webapp/log#tail)命令。

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

記錄檔資料流啟動之後，重新整理在 hello 瀏覽器 tooget Azure web 應用程式一些 web 流量。 您現在可以看到主控台記錄檔經由管道輸出 tooyour 終端機。

您隨時可以輸入 `Ctrl+C` 以停止記錄資料流。 

## <a name="manage-your-azure-web-app"></a>管理您的 Azure Web 應用程式

移 toohello [Azure 入口網站](https://portal.azure.com)toosee hello web 應用程式所建立。

從 hello 左窗格中，按一下 **應用程式服務**，然後按一下 hello Azure web 應用程式名稱。

![入口網站瀏覽 tooAzure web 應用程式](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

根據預設，hello 入口網站會顯示 web 應用程式的**概觀**頁面。 此頁面可讓您檢視應用程式的執行方式。 您也可以在這裡執行基本管理工作，像是瀏覽、停止、啟動、重新啟動及刪除。 在左邊 hello 頁面 hello hello 索引標籤會顯示 hello 不同的組態頁面，您可以開啟。

![Azure 入口網站中的 App Service 頁面](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a>後續步驟

您已了解如何︰

> [!div class="checklist"]
> * 在 Azure 中建立 MongoDB 資料庫
> * 連接 Node.js 應用程式 tooMongoDB
> * 部署 hello 應用程式 tooAzure
> * 更新 hello 資料模型，部署 hello 應用程式
> * 從 Azure tooyour 終端機的資料流記錄檔
> * 管理 hello hello Azure 入口網站中的應用程式

前進 toohello 下一個教學課程 toolearn toomap 自訂的 DNS 名稱 tooyour web 應用程式的方式。

> [!div class="nextstepaction"] 
> [將現有自訂 DNS 名稱 tooAzure Web 應用程式的對應](app-service-web-tutorial-custom-domain.md)
