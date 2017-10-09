---
title: "使用 Node.js MongoDB 應用程式 tooAzure Cosmos DB aaaConnect |Microsoft 文件"
description: "深入了解如何 tooconnect 現有的 Node.js MongoDB 應用程式 tooAzure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 06/19/2017
ms.author: mimig
ms.openlocfilehash: 4bc4f17a31d8c18d1ce5e3f002462f4d48eeb1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-migrate-an-existing-nodejs-mongodb-web-app"></a>Azure Cosmos DB︰移轉現有的 Node.js MongoDB Web 應用程式 

Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。 您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。 

本快速入門示範如何將現有的 toouse [MongoDB](mongodb-introduction.md)撰寫 Node.js 應用程式並將它連接 tooyour Azure Cosmos DB 資料庫支援 MongoDB 用戶端連線。 換句話說，Node.js 應用程式只知道它連接 tooa 資料庫使用 MongoDB Api。 是透明 toohello hello 資料的應用程式會儲存在 Azure Cosmos DB。

完成之後，您的 MEAN 應用程式 (MongoDB、Express、AngularJS 及 Node.js) 將會在 [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 上執行。 

![在 Azure App Service 中執行的 MEAN.js 應用程式](./media/create-mongodb-nodejs/meanjs-in-azure.png)


[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。 執行`az --version`toofind hello 版本。 如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。 

## <a name="prerequisites"></a>必要條件 
此外 tooAzure CLI，您需要[Node.js](https://nodejs.org/)和[Git](http://www.git-scm.com/downloads)本機安裝 toorun`npm`和`git`命令。

您應具備 Node.js 的使用知識。 本快速入門不是預期的 toohelp 您一般開發 Node.js 應用程式。

## <a name="clone-hello-sample-application"></a>複製 hello 範例應用程式

開啟 git 終端機視窗，例如 git bash 和`cd`tooa 工作目錄。  

執行下列命令 tooclone hello 範例儲存機制的 hello。 這個範例儲存機制包含 hello 預設[MEAN.js](http://meanjs.org/)應用程式。 

```bash
git clone https://github.com/prashanthmadi/mean
```

## <a name="run-hello-application"></a>執行 hello 應用程式

安裝所需的 hello 封裝並啟動 hello 應用程式。

```bash
cd mean
npm install
npm start
```

## <a name="log-in-tooazure"></a>登入 tooAzure

如果您使用已安裝的 Azure CLI，登入 Azure 訂用帳戶以 hello tooyour [az 登入](/cli/azure/#login)命令，並遵循螢幕上指示 hello。 如果您使用 hello Azure 雲端殼層，您可以略過此步驟。

```azurecli
az login 
``` 
   
## <a name="add-hello-azure-cosmos-db-module"></a>新增 hello Azure Cosmos DB 模組

如果您使用已安裝的 Azure CLI，請檢查 toosee 如果 hello`cosmosdb`元件是否已安裝執行 hello`az`命令。 如果`cosmosdb`是在 hello 基底的命令清單，請繼續 toohello 下一個命令。 如果您使用 hello Azure 雲端殼層，您可以略過此步驟。

如果`cosmosdb`不在 hello 基底的命令清單，請重新安裝[Azure CLI 2.0]( /cli/azure/install-azure-cli)。

## <a name="create-a-resource-group"></a>建立資源群組

建立[資源群組](../azure-resource-manager/resource-group-overview.md)以 hello [az 群組建立](/cli/azure/group#create)。 Azure 資源群組是在其中部署與管理 Azure 資源 (如 Web 應用程式、資料庫和儲存體帳戶) 的邏輯容器。 

hello 下列範例會建立資源群組中 hello 西歐地區。 選擇 hello 資源群組的唯一名稱。

如果您使用 Azure 雲端殼層，請按一下**試試**，請遵循 hello 螢幕上的提示 toologin，然後將 hello 命令複製到 hello 命令提示字元。

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

## <a name="create-an-azure-cosmos-db-account"></a>建立 Azure Cosmos DB 帳戶

建立 Azure Cosmos DB 帳戶以 hello [az cosmosdb 建立](/cli/azure/cosmosdb#create)命令。

Hello 中下列命令，請將替換成您自己唯一 Azure Cosmos DB 帳戶名稱，您會看到 hello`<cosmosdb-name>`預留位置。 這個唯一名稱將用於 Azure Cosmos DB 端點的一部分 (`https://<cosmosdb-name>.documents.azure.com/`)，因此 hello 名稱需要 toobe 唯一在 Azure 中的所有 Azure Cosmos DB 帳號。 

```azurecli-interactive
az cosmosdb create --name <cosmosdb-name> --resource-group myResourceGroup --kind MongoDB
```

hello`--kind MongoDB`參數可啟用 MongoDB 用戶端連線。

建立 hello Azure Cosmos DB 帳戶時，hello Azure CLI 顯示資訊的類似 toohello 下列範例。 

> [!NOTE]
> 這個範例會使用 JSON 做為 hello Azure CLI 輸出格式，這是 hello 預設值。 toouse 另一個輸出格式，請參閱[輸出格式之 Azure CLI 2.0 命令](https://docs.microsoft.com/cli/azure/format-output-azure-cli)。

```json
{
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb-name>.documents.azure.com:443/",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Document
DB/databaseAccounts/<cosmosdb-name>",
  "kind": "MongoDB",
  "location": "West Europe",
  "name": "<cosmosdb-name>",
  "readLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ],
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.DocumentDB/databaseAccounts",
  "writeLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ]
} 
```

## <a name="connect-your-nodejs-application-toohello-database"></a>Node.js 應用程式 toohello 資料庫的連接

在此步驟中，您可以連接 MEAN.js 範例應用程式 tooan Azure Cosmos DB 資料庫您剛剛建立，使用 MongoDB 連接字串。 

<a name="devconfig"></a>
## <a name="configure-hello-connection-string-in-your-nodejs-application"></a>Node.js 應用程式中設定 hello 連接字串

在您的 MEAN.js 存放庫中，開啟 `config/env/local-development.js`。

取代下列程式碼的 hello hello 這個檔案的內容。 請務必 tooalso 取代 hello 兩`<cosmosdb-name>`預留位置取代您的 Azure Cosmos DB 帳戶名稱。

```javascript
'use strict';

module.exports = {
  db: {
    uri: 'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean-dev?ssl=true&sslverifycertificate=false'
  }
};
```

## <a name="retrieve-hello-key"></a>擷取 hello 金鑰

在訂單 tooconnect tooan Azure Cosmos DB 資料庫中，您需要 hello 資料庫金鑰。 使用 hello [az cosmosdb 清單索引鍵](/cli/azure/cosmosdb#list-keys)命令 tooretrieve hello 主索引鍵。

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb-name> --resource-group myResourceGroup --query "primaryMasterKey"
```

hello Azure CLI 輸出資訊類似 toohello 下列範例。 

```json
"RUayjYjixJDWG5xTqIiXjC..."
```

複製 hello 值`primaryMasterKey`。 貼上透過 hello`<primary_master_key>`中`local-development.js`。

儲存您的變更。

### <a name="run-hello-application-again"></a>Hello 再次執行應用程式。

再次執行 `npm start`。 

```bash
npm start
```

主控台訊息現在應該告知您該 hello 開發環境已啟動並執行。 

瀏覽過`http://localhost:3000`瀏覽器中。 按一下**註冊**hello 最上層功能表，然後再次嘗試 toocreate 中兩個虛擬使用者。 

hello MEAN.js 範例應用程式會將使用者資料儲存在 hello 資料庫。 如果您為成功，而且 MEAN.js 自動登入 hello 建立使用者，則 Azure Cosmos DB 連線運作正常。 

![MEAN.js 順利連線 tooMongoDB](./media/create-mongodb-nodejs/mongodb-connect-success.png)

## <a name="view-data-in-data-explorer"></a>在資料總管中檢視資料

儲存資料供 Azure Cosmos DB 是可用 tooview、 查詢和執行的商務邏輯上 hello Azure 入口網站中。

tooview，查詢和處理 hello 使用者資料建立在 hello 先前步驟中，登入 toohello [Azure 入口網站](https://portal.azure.com)web 瀏覽器中。

Hello 頂端搜尋 方塊中，輸入 Azure Cosmos DB。 當您的 Cosmos DB 帳戶刀鋒視窗開啟時，選取您的 Cosmos DB 帳戶。 在左瀏覽 hello，按一下 [資料總管]。 展開您在 hello 集合 窗格中的集合，然後您可以檢視 hello 文件在 hello 集合中，查詢 hello 資料，以及甚至建立及執行預存程序、 觸發程序和 Udf。 

![在 hello Azure 入口網站中的資料總管](./media/create-mongodb-nodejs/cosmosdb-connect-mongodb-data-explorer.png)


## <a name="deploy-hello-nodejs-application-tooazure"></a>部署 hello Node.js 應用程式 tooAzure

在此步驟中，您可以部署您 MongoDB 連接 Node.js 應用程式 tooAzure Cosmos DB。

您可能已注意到您稍早變更該 hello 設定檔是 hello 開發環境 (`/config/env/local-development.js`)。 當您部署您的應用程式 tooApp 服務時，它會預設執行 hello 實際執行環境中。 現在，您需要 toomake hello 相同變更 toohello 個別設定檔。

在您的 MEAN.js 存放庫中，開啟 `config/env/production.js`。

在 hello`db`物件，以取代 hello 值`uri`如示 hello 下列範例。 為確定 tooreplace hello 預留位置為之前。

```javascript
'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean?ssl=true&sslverifycertificate=false',
```

> [!NOTE] 
> hello`ssl=true`選項，請務必因為[Azure Cosmos DB 需要 SSL](connect-mongodb-account.md#connection-string-requirements)。 
>
>

在終端機 hello，所有您將變更認可至 Git。 您可以複製這兩個命令 toorun 一起。

```bash
git add .
git commit -m "configured MongoDB connection string"
```
## <a name="clean-up-resources"></a>清除資源

如果您不打算 toocontinue toouse 此應用程式，刪除所有資源本快速入門以建立 hello Azure 入口網站以 hello 下列步驟：

1. Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。 
2. 在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。

## <a name="next-steps"></a>後續步驟

本快速入門中，您學到如何 toocreate Azure Cosmos DB 帳戶，並建立使用 hello 資料總管 MongoDB 集合。 您現在可以移轉您 MongoDB 資料 tooAzure Cosmos DB。  

> [!div class="nextstepaction"]
> [將 MongoDB 資料匯入到 Azure Cosmos DB](mongodb-migrate.md)
