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
# <a name="azure-cosmos-db-migrate-an-existing-nodejs-mongodb-web-app"></a><span data-ttu-id="0440a-103">Azure Cosmos DB︰移轉現有的 Node.js MongoDB Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="0440a-103">Azure Cosmos DB: Migrate an existing Node.js MongoDB web app</span></span> 

<span data-ttu-id="0440a-104">Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="0440a-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="0440a-105">您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。</span><span class="sxs-lookup"><span data-stu-id="0440a-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="0440a-106">本快速入門示範如何將現有的 toouse [MongoDB](mongodb-introduction.md)撰寫 Node.js 應用程式並將它連接 tooyour Azure Cosmos DB 資料庫支援 MongoDB 用戶端連線。</span><span class="sxs-lookup"><span data-stu-id="0440a-106">This quickstart demonstrates how toouse an existing [MongoDB](mongodb-introduction.md) app written in Node.js and connect it tooyour Azure Cosmos DB database, which supports MongoDB client connections.</span></span> <span data-ttu-id="0440a-107">換句話說，Node.js 應用程式只知道它連接 tooa 資料庫使用 MongoDB Api。</span><span class="sxs-lookup"><span data-stu-id="0440a-107">In other words, your Node.js application only knows that it's connecting tooa database using MongoDB APIs.</span></span> <span data-ttu-id="0440a-108">是透明 toohello hello 資料的應用程式會儲存在 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="0440a-108">It is transparent toohello application that hello data is stored in Azure Cosmos DB.</span></span>

<span data-ttu-id="0440a-109">完成之後，您的 MEAN 應用程式 (MongoDB、Express、AngularJS 及 Node.js) 將會在 [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 上執行。</span><span class="sxs-lookup"><span data-stu-id="0440a-109">When you are done, you will have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running on [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> 

![在 Azure App Service 中執行的 MEAN.js 應用程式](./media/create-mongodb-nodejs/meanjs-in-azure.png)


[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0440a-111">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="0440a-111">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0440a-112">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="0440a-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="0440a-113">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="0440a-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0440a-114">必要條件</span><span class="sxs-lookup"><span data-stu-id="0440a-114">Prerequisites</span></span> 
<span data-ttu-id="0440a-115">此外 tooAzure CLI，您需要[Node.js](https://nodejs.org/)和[Git](http://www.git-scm.com/downloads)本機安裝 toorun`npm`和`git`命令。</span><span class="sxs-lookup"><span data-stu-id="0440a-115">In addition tooAzure CLI, you need [Node.js](https://nodejs.org/) and [Git](http://www.git-scm.com/downloads) installed locally toorun `npm` and `git` commands.</span></span>

<span data-ttu-id="0440a-116">您應具備 Node.js 的使用知識。</span><span class="sxs-lookup"><span data-stu-id="0440a-116">You should have working knowledge of Node.js.</span></span> <span data-ttu-id="0440a-117">本快速入門不是預期的 toohelp 您一般開發 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0440a-117">This quickstart is not intended toohelp you with developing Node.js applications in general.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="0440a-118">複製 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="0440a-118">Clone hello sample application</span></span>

<span data-ttu-id="0440a-119">開啟 git 終端機視窗，例如 git bash 和`cd`tooa 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="0440a-119">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

<span data-ttu-id="0440a-120">執行下列命令 tooclone hello 範例儲存機制的 hello。</span><span class="sxs-lookup"><span data-stu-id="0440a-120">Run hello following commands tooclone hello sample repository.</span></span> <span data-ttu-id="0440a-121">這個範例儲存機制包含 hello 預設[MEAN.js](http://meanjs.org/)應用程式。</span><span class="sxs-lookup"><span data-stu-id="0440a-121">This sample repository contains hello default [MEAN.js](http://meanjs.org/) application.</span></span> 

```bash
git clone https://github.com/prashanthmadi/mean
```

## <a name="run-hello-application"></a><span data-ttu-id="0440a-122">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="0440a-122">Run hello application</span></span>

<span data-ttu-id="0440a-123">安裝所需的 hello 封裝並啟動 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0440a-123">Install hello required packages and start hello application.</span></span>

```bash
cd mean
npm install
npm start
```

## <a name="log-in-tooazure"></a><span data-ttu-id="0440a-124">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="0440a-124">Log in tooAzure</span></span>

<span data-ttu-id="0440a-125">如果您使用已安裝的 Azure CLI，登入 Azure 訂用帳戶以 hello tooyour [az 登入](/cli/azure/#login)命令，並遵循螢幕上指示 hello。</span><span class="sxs-lookup"><span data-stu-id="0440a-125">If you are using an installed Azure CLI, log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> <span data-ttu-id="0440a-126">如果您使用 hello Azure 雲端殼層，您可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="0440a-126">You can skip this step if you're using hello Azure Cloud Shell.</span></span>

```azurecli
az login 
``` 
   
## <a name="add-hello-azure-cosmos-db-module"></a><span data-ttu-id="0440a-127">新增 hello Azure Cosmos DB 模組</span><span class="sxs-lookup"><span data-stu-id="0440a-127">Add hello Azure Cosmos DB module</span></span>

<span data-ttu-id="0440a-128">如果您使用已安裝的 Azure CLI，請檢查 toosee 如果 hello`cosmosdb`元件是否已安裝執行 hello`az`命令。</span><span class="sxs-lookup"><span data-stu-id="0440a-128">If you are using an installed Azure CLI, check toosee if hello `cosmosdb` component is already installed by running hello `az` command.</span></span> <span data-ttu-id="0440a-129">如果`cosmosdb`是在 hello 基底的命令清單，請繼續 toohello 下一個命令。</span><span class="sxs-lookup"><span data-stu-id="0440a-129">If `cosmosdb` is in hello list of base commands, proceed toohello next command.</span></span> <span data-ttu-id="0440a-130">如果您使用 hello Azure 雲端殼層，您可以略過此步驟。</span><span class="sxs-lookup"><span data-stu-id="0440a-130">You can skip this step if you're using hello Azure Cloud Shell.</span></span>

<span data-ttu-id="0440a-131">如果`cosmosdb`不在 hello 基底的命令清單，請重新安裝[Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="0440a-131">If `cosmosdb` is not in hello list of base commands, reinstall [Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="0440a-132">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="0440a-132">Create a resource group</span></span>

<span data-ttu-id="0440a-133">建立[資源群組](../azure-resource-manager/resource-group-overview.md)以 hello [az 群組建立](/cli/azure/group#create)。</span><span class="sxs-lookup"><span data-stu-id="0440a-133">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="0440a-134">Azure 資源群組是在其中部署與管理 Azure 資源 (如 Web 應用程式、資料庫和儲存體帳戶) 的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="0440a-134">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="0440a-135">hello 下列範例會建立資源群組中 hello 西歐地區。</span><span class="sxs-lookup"><span data-stu-id="0440a-135">hello following example creates a resource group in hello West Europe region.</span></span> <span data-ttu-id="0440a-136">選擇 hello 資源群組的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="0440a-136">Choose a unique name for hello resource group.</span></span>

<span data-ttu-id="0440a-137">如果您使用 Azure 雲端殼層，請按一下**試試**，請遵循 hello 螢幕上的提示 toologin，然後將 hello 命令複製到 hello 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="0440a-137">If you are using Azure Cloud Shell, click **Try It**, follow hello onscreen prompts toologin, then copy hello command into hello command prompt.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="0440a-138">建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="0440a-138">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="0440a-139">建立 Azure Cosmos DB 帳戶以 hello [az cosmosdb 建立](/cli/azure/cosmosdb#create)命令。</span><span class="sxs-lookup"><span data-stu-id="0440a-139">Create an Azure Cosmos DB account with hello [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="0440a-140">Hello 中下列命令，請將替換成您自己唯一 Azure Cosmos DB 帳戶名稱，您會看到 hello`<cosmosdb-name>`預留位置。</span><span class="sxs-lookup"><span data-stu-id="0440a-140">In hello following command, please substitute your own unique Azure Cosmos DB account name where you see hello `<cosmosdb-name>` placeholder.</span></span> <span data-ttu-id="0440a-141">這個唯一名稱將用於 Azure Cosmos DB 端點的一部分 (`https://<cosmosdb-name>.documents.azure.com/`)，因此 hello 名稱需要 toobe 唯一在 Azure 中的所有 Azure Cosmos DB 帳號。</span><span class="sxs-lookup"><span data-stu-id="0440a-141">This unique name will be used as part of your Azure Cosmos DB endpoint (`https://<cosmosdb-name>.documents.azure.com/`), so hello name needs toobe unique across all Azure Cosmos DB accounts in Azure.</span></span> 

```azurecli-interactive
az cosmosdb create --name <cosmosdb-name> --resource-group myResourceGroup --kind MongoDB
```

<span data-ttu-id="0440a-142">hello`--kind MongoDB`參數可啟用 MongoDB 用戶端連線。</span><span class="sxs-lookup"><span data-stu-id="0440a-142">hello `--kind MongoDB` parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="0440a-143">建立 hello Azure Cosmos DB 帳戶時，hello Azure CLI 顯示資訊的類似 toohello 下列範例。</span><span class="sxs-lookup"><span data-stu-id="0440a-143">When hello Azure Cosmos DB account is created, hello Azure CLI shows information similar toohello following example.</span></span> 

> [!NOTE]
> <span data-ttu-id="0440a-144">這個範例會使用 JSON 做為 hello Azure CLI 輸出格式，這是 hello 預設值。</span><span class="sxs-lookup"><span data-stu-id="0440a-144">This example uses JSON as hello Azure CLI output format, which is hello default.</span></span> <span data-ttu-id="0440a-145">toouse 另一個輸出格式，請參閱[輸出格式之 Azure CLI 2.0 命令](https://docs.microsoft.com/cli/azure/format-output-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="0440a-145">toouse another output format, see [Output formats for Azure CLI 2.0 commands](https://docs.microsoft.com/cli/azure/format-output-azure-cli).</span></span>

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

## <a name="connect-your-nodejs-application-toohello-database"></a><span data-ttu-id="0440a-146">Node.js 應用程式 toohello 資料庫的連接</span><span class="sxs-lookup"><span data-stu-id="0440a-146">Connect your Node.js application toohello database</span></span>

<span data-ttu-id="0440a-147">在此步驟中，您可以連接 MEAN.js 範例應用程式 tooan Azure Cosmos DB 資料庫您剛剛建立，使用 MongoDB 連接字串。</span><span class="sxs-lookup"><span data-stu-id="0440a-147">In this step, you connect your MEAN.js sample application tooan Azure Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

<a name="devconfig"></a>
## <a name="configure-hello-connection-string-in-your-nodejs-application"></a><span data-ttu-id="0440a-148">Node.js 應用程式中設定 hello 連接字串</span><span class="sxs-lookup"><span data-stu-id="0440a-148">Configure hello connection string in your Node.js application</span></span>

<span data-ttu-id="0440a-149">在您的 MEAN.js 存放庫中，開啟 `config/env/local-development.js`。</span><span class="sxs-lookup"><span data-stu-id="0440a-149">In your MEAN.js repository, open `config/env/local-development.js`.</span></span>

<span data-ttu-id="0440a-150">取代下列程式碼的 hello hello 這個檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="0440a-150">Replace hello content of this file with hello following code.</span></span> <span data-ttu-id="0440a-151">請務必 tooalso 取代 hello 兩`<cosmosdb-name>`預留位置取代您的 Azure Cosmos DB 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="0440a-151">Be sure tooalso replace hello two `<cosmosdb-name>` placeholders with your Azure Cosmos DB account name.</span></span>

```javascript
'use strict';

module.exports = {
  db: {
    uri: 'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean-dev?ssl=true&sslverifycertificate=false'
  }
};
```

## <a name="retrieve-hello-key"></a><span data-ttu-id="0440a-152">擷取 hello 金鑰</span><span class="sxs-lookup"><span data-stu-id="0440a-152">Retrieve hello key</span></span>

<span data-ttu-id="0440a-153">在訂單 tooconnect tooan Azure Cosmos DB 資料庫中，您需要 hello 資料庫金鑰。</span><span class="sxs-lookup"><span data-stu-id="0440a-153">In order tooconnect tooan Azure Cosmos DB database, you need hello database key.</span></span> <span data-ttu-id="0440a-154">使用 hello [az cosmosdb 清單索引鍵](/cli/azure/cosmosdb#list-keys)命令 tooretrieve hello 主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="0440a-154">Use hello [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command tooretrieve hello primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb-name> --resource-group myResourceGroup --query "primaryMasterKey"
```

<span data-ttu-id="0440a-155">hello Azure CLI 輸出資訊類似 toohello 下列範例。</span><span class="sxs-lookup"><span data-stu-id="0440a-155">hello Azure CLI outputs information similar toohello following example.</span></span> 

```json
"RUayjYjixJDWG5xTqIiXjC..."
```

<span data-ttu-id="0440a-156">複製 hello 值`primaryMasterKey`。</span><span class="sxs-lookup"><span data-stu-id="0440a-156">Copy hello value of `primaryMasterKey`.</span></span> <span data-ttu-id="0440a-157">貼上透過 hello`<primary_master_key>`中`local-development.js`。</span><span class="sxs-lookup"><span data-stu-id="0440a-157">Paste this over hello  `<primary_master_key>` in `local-development.js`.</span></span>

<span data-ttu-id="0440a-158">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="0440a-158">Save your changes.</span></span>

### <a name="run-hello-application-again"></a><span data-ttu-id="0440a-159">Hello 再次執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="0440a-159">Run hello application again.</span></span>

<span data-ttu-id="0440a-160">再次執行 `npm start`。</span><span class="sxs-lookup"><span data-stu-id="0440a-160">Run `npm start` again.</span></span> 

```bash
npm start
```

<span data-ttu-id="0440a-161">主控台訊息現在應該告知您該 hello 開發環境已啟動並執行。</span><span class="sxs-lookup"><span data-stu-id="0440a-161">A console message should now tell you that hello development environment is up and running.</span></span> 

<span data-ttu-id="0440a-162">瀏覽過`http://localhost:3000`瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="0440a-162">Navigate too`http://localhost:3000` in a browser.</span></span> <span data-ttu-id="0440a-163">按一下**註冊**hello 最上層功能表，然後再次嘗試 toocreate 中兩個虛擬使用者。</span><span class="sxs-lookup"><span data-stu-id="0440a-163">Click **Sign Up** in hello top menu and try toocreate two dummy users.</span></span> 

<span data-ttu-id="0440a-164">hello MEAN.js 範例應用程式會將使用者資料儲存在 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0440a-164">hello MEAN.js sample application stores user data in hello database.</span></span> <span data-ttu-id="0440a-165">如果您為成功，而且 MEAN.js 自動登入 hello 建立使用者，則 Azure Cosmos DB 連線運作正常。</span><span class="sxs-lookup"><span data-stu-id="0440a-165">If you are successful and MEAN.js automatically signs into hello created user, then your Azure Cosmos DB connection is working.</span></span> 

![MEAN.js 順利連線 tooMongoDB](./media/create-mongodb-nodejs/mongodb-connect-success.png)

## <a name="view-data-in-data-explorer"></a><span data-ttu-id="0440a-167">在資料總管中檢視資料</span><span class="sxs-lookup"><span data-stu-id="0440a-167">View data in Data Explorer</span></span>

<span data-ttu-id="0440a-168">儲存資料供 Azure Cosmos DB 是可用 tooview、 查詢和執行的商務邏輯上 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="0440a-168">Data stored by an Azure Cosmos DB is available tooview, query, and run business-logic on in hello Azure portal.</span></span>

<span data-ttu-id="0440a-169">tooview，查詢和處理 hello 使用者資料建立在 hello 先前步驟中，登入 toohello [Azure 入口網站](https://portal.azure.com)web 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="0440a-169">tooview, query, and work with hello user data created in hello previous step, login toohello [Azure portal](https://portal.azure.com) in your web browser.</span></span>

<span data-ttu-id="0440a-170">Hello 頂端搜尋 方塊中，輸入 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="0440a-170">In hello top Search box, type Azure Cosmos DB.</span></span> <span data-ttu-id="0440a-171">當您的 Cosmos DB 帳戶刀鋒視窗開啟時，選取您的 Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0440a-171">When your Cosmos DB account blade opens, select your Cosmos DB account.</span></span> <span data-ttu-id="0440a-172">在左瀏覽 hello，按一下 [資料總管]。</span><span class="sxs-lookup"><span data-stu-id="0440a-172">In hello left navigation, click Data Explorer.</span></span> <span data-ttu-id="0440a-173">展開您在 hello 集合 窗格中的集合，然後您可以檢視 hello 文件在 hello 集合中，查詢 hello 資料，以及甚至建立及執行預存程序、 觸發程序和 Udf。</span><span class="sxs-lookup"><span data-stu-id="0440a-173">Expand your collection in hello Collections pane, and then you can view hello documents in hello collection, query hello data, and even create and run stored procedures, triggers, and UDFs.</span></span> 

![在 hello Azure 入口網站中的資料總管](./media/create-mongodb-nodejs/cosmosdb-connect-mongodb-data-explorer.png)


## <a name="deploy-hello-nodejs-application-tooazure"></a><span data-ttu-id="0440a-175">部署 hello Node.js 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="0440a-175">Deploy hello Node.js application tooAzure</span></span>

<span data-ttu-id="0440a-176">在此步驟中，您可以部署您 MongoDB 連接 Node.js 應用程式 tooAzure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="0440a-176">In this step, you deploy your MongoDB-connected Node.js application tooAzure Cosmos DB.</span></span>

<span data-ttu-id="0440a-177">您可能已注意到您稍早變更該 hello 設定檔是 hello 開發環境 (`/config/env/local-development.js`)。</span><span class="sxs-lookup"><span data-stu-id="0440a-177">You may have noticed that hello configuration file that you changed earlier is for hello development environment (`/config/env/local-development.js`).</span></span> <span data-ttu-id="0440a-178">當您部署您的應用程式 tooApp 服務時，它會預設執行 hello 實際執行環境中。</span><span class="sxs-lookup"><span data-stu-id="0440a-178">When you deploy your application tooApp Service, it will run in hello production environment by default.</span></span> <span data-ttu-id="0440a-179">現在，您需要 toomake hello 相同變更 toohello 個別設定檔。</span><span class="sxs-lookup"><span data-stu-id="0440a-179">So now, you need toomake hello same change toohello respective configuration file.</span></span>

<span data-ttu-id="0440a-180">在您的 MEAN.js 存放庫中，開啟 `config/env/production.js`。</span><span class="sxs-lookup"><span data-stu-id="0440a-180">In your MEAN.js repository, open `config/env/production.js`.</span></span>

<span data-ttu-id="0440a-181">在 hello`db`物件，以取代 hello 值`uri`如示 hello 下列範例。</span><span class="sxs-lookup"><span data-stu-id="0440a-181">In hello `db` object, replace hello value of `uri` as show in hello following example.</span></span> <span data-ttu-id="0440a-182">為確定 tooreplace hello 預留位置為之前。</span><span class="sxs-lookup"><span data-stu-id="0440a-182">Be sure tooreplace hello placeholders as before.</span></span>

```javascript
'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean?ssl=true&sslverifycertificate=false',
```

> [!NOTE] 
> <span data-ttu-id="0440a-183">hello`ssl=true`選項，請務必因為[Azure Cosmos DB 需要 SSL](connect-mongodb-account.md#connection-string-requirements)。</span><span class="sxs-lookup"><span data-stu-id="0440a-183">hello `ssl=true` option is important because [Azure Cosmos DB requires SSL](connect-mongodb-account.md#connection-string-requirements).</span></span> 
>
>

<span data-ttu-id="0440a-184">在終端機 hello，所有您將變更認可至 Git。</span><span class="sxs-lookup"><span data-stu-id="0440a-184">In hello terminal, commit all your changes into Git.</span></span> <span data-ttu-id="0440a-185">您可以複製這兩個命令 toorun 一起。</span><span class="sxs-lookup"><span data-stu-id="0440a-185">You can copy both commands toorun them together.</span></span>

```bash
git add .
git commit -m "configured MongoDB connection string"
```
## <a name="clean-up-resources"></a><span data-ttu-id="0440a-186">清除資源</span><span class="sxs-lookup"><span data-stu-id="0440a-186">Clean up resources</span></span>

<span data-ttu-id="0440a-187">如果您不打算 toocontinue toouse 此應用程式，刪除所有資源本快速入門以建立 hello Azure 入口網站以 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="0440a-187">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="0440a-188">Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="0440a-188">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="0440a-189">在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。</span><span class="sxs-lookup"><span data-stu-id="0440a-189">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0440a-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0440a-190">Next steps</span></span>

<span data-ttu-id="0440a-191">本快速入門中，您學到如何 toocreate Azure Cosmos DB 帳戶，並建立使用 hello 資料總管 MongoDB 集合。</span><span class="sxs-lookup"><span data-stu-id="0440a-191">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and create a MongoDB collection using hello Data Explorer.</span></span> <span data-ttu-id="0440a-192">您現在可以移轉您 MongoDB 資料 tooAzure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="0440a-192">You can now migrate your MongoDB data tooAzure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="0440a-193">將 MongoDB 資料匯入到 Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="0440a-193">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)
