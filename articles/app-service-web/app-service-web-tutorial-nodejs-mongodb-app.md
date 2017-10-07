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
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a><span data-ttu-id="0f310-103">在 Azure 中建置 Node.js 和 MongoDB Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="0f310-103">Build a Node.js and MongoDB web app in Azure</span></span>

<span data-ttu-id="0f310-104">Azure Web Apps 提供可高度擴充、自我修復的 Web 主機服務。</span><span class="sxs-lookup"><span data-stu-id="0f310-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="0f310-105">本教學課程會示範如何 toocreate Node.js web 應用程式在 Azure 中的，並將它連接 tooa MongoDB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0f310-105">This tutorial shows how toocreate a Node.js web app in Azure and connect it tooa MongoDB database.</span></span> <span data-ttu-id="0f310-106">完成之後，您的 MEAN 應用程式 (MongoDB、Express、AngularJS 及 Node.js) 將會在 [Azure App Service](app-service-web-overview.md) 中執行。</span><span class="sxs-lookup"><span data-stu-id="0f310-106">When you're done, you'll have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running in [Azure App Service](app-service-web-overview.md).</span></span> <span data-ttu-id="0f310-107">為了簡單起見，hello 範例應用程式使用 hello [MEAN.js web 架構](http://meanjs.org/)。</span><span class="sxs-lookup"><span data-stu-id="0f310-107">For simplicity, hello sample application uses hello [MEAN.js web framework](http://meanjs.org/).</span></span>

![在 Azure App Service 中執行的 MEAN.js 應用程式](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="0f310-109">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="0f310-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0f310-110">在 Azure 中建立 MongoDB 資料庫</span><span class="sxs-lookup"><span data-stu-id="0f310-110">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="0f310-111">連接 Node.js 應用程式 tooMongoDB</span><span class="sxs-lookup"><span data-stu-id="0f310-111">Connect a Node.js app tooMongoDB</span></span>
> * <span data-ttu-id="0f310-112">部署 hello 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="0f310-112">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="0f310-113">更新 hello 資料模型，部署 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="0f310-113">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="0f310-114">來自 Azure 的串流診斷記錄</span><span class="sxs-lookup"><span data-stu-id="0f310-114">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="0f310-115">管理 hello hello Azure 入口網站中的應用程式</span><span class="sxs-lookup"><span data-stu-id="0f310-115">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f310-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="0f310-116">Prerequisites</span></span>

<span data-ttu-id="0f310-117">toocomplete 本教學課程：</span><span class="sxs-lookup"><span data-stu-id="0f310-117">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="0f310-118">安裝 Git</span><span class="sxs-lookup"><span data-stu-id="0f310-118">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="0f310-119">安裝 Node.js 和 NPM</span><span class="sxs-lookup"><span data-stu-id="0f310-119">Install Node.js and NPM</span></span>](https://nodejs.org/)
1. <span data-ttu-id="0f310-120">[安裝 Gulp.js](http://gulpjs.com/) ([MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started) 的必要項目)</span><span class="sxs-lookup"><span data-stu-id="0f310-120">[Install Gulp.js](http://gulpjs.com/) (required by [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span></span>
1. [<span data-ttu-id="0f310-121">安裝及執行 MongoDB Community 版本</span><span class="sxs-lookup"><span data-stu-id="0f310-121">Install and run MongoDB Community Edition</span></span>](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="0f310-122">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="0f310-122">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="0f310-123">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="0f310-123">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="0f310-124">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="0f310-124">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-mongodb"></a><span data-ttu-id="0f310-125">測試本機的 MongoDB</span><span class="sxs-lookup"><span data-stu-id="0f310-125">Test local MongoDB</span></span>

<span data-ttu-id="0f310-126">開啟 hello 終端機視窗和`cd`toohello `bin` MongoDB 安裝目錄。</span><span class="sxs-lookup"><span data-stu-id="0f310-126">Open hello terminal window and `cd` toohello `bin` directory of your MongoDB installation.</span></span> <span data-ttu-id="0f310-127">您可以使用這個終端機視窗 toorun hello 的所有命令，在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="0f310-127">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

<span data-ttu-id="0f310-128">執行`mongo`hello 終端機 tooconnect tooyour 本機 MongoDB 伺服器中。</span><span class="sxs-lookup"><span data-stu-id="0f310-128">Run `mongo` in hello terminal tooconnect tooyour local MongoDB server.</span></span>

```bash
mongo
```

<span data-ttu-id="0f310-129">如果連接成功，則您的 MongoDB 資料庫已在執行中。</span><span class="sxs-lookup"><span data-stu-id="0f310-129">If your connection is successful, then your MongoDB database is already running.</span></span> <span data-ttu-id="0f310-130">如果沒有，請確定您的本機 MongoDB 資料庫已啟動在 hello 步驟[安裝 MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/)。</span><span class="sxs-lookup"><span data-stu-id="0f310-130">If not, make sure that your local MongoDB database is started by following hello steps at [Install MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span></span> <span data-ttu-id="0f310-131">通常，MongoDB 已安裝，但您仍然需要 toostart 它藉由執行`mongod`。</span><span class="sxs-lookup"><span data-stu-id="0f310-131">Often, MongoDB is installed, but you still need toostart it by running `mongod`.</span></span> 

<span data-ttu-id="0f310-132">當您完成測試 MongoDB 資料庫中，輸入`Ctrl+C`hello 終端機中。</span><span class="sxs-lookup"><span data-stu-id="0f310-132">When you're done testing your MongoDB database, type `Ctrl+C` in hello terminal.</span></span> 

## <a name="create-local-nodejs-app"></a><span data-ttu-id="0f310-133">建立本機的 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="0f310-133">Create local Node.js app</span></span>

<span data-ttu-id="0f310-134">在此步驟中，您會將設定 hello 本機 Node.js 專案。</span><span class="sxs-lookup"><span data-stu-id="0f310-134">In this step, you set up hello local Node.js project.</span></span>

### <a name="clone-hello-sample-application"></a><span data-ttu-id="0f310-135">複製 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="0f310-135">Clone hello sample application</span></span>

<span data-ttu-id="0f310-136">在 hello 終端機視窗， `cd` tooa 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="0f310-136">In hello terminal window, `cd` tooa working directory.</span></span>  

<span data-ttu-id="0f310-137">執行下列命令 tooclone hello 範例儲存機制的 hello。</span><span class="sxs-lookup"><span data-stu-id="0f310-137">Run hello following command tooclone hello sample repository.</span></span> 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

<span data-ttu-id="0f310-138">這個範例儲存機制包含一份 hello [MEAN.js 儲存機制](https://github.com/meanjs/mean)。</span><span class="sxs-lookup"><span data-stu-id="0f310-138">This sample repository contains a copy of hello [MEAN.js repository](https://github.com/meanjs/mean).</span></span> <span data-ttu-id="0f310-139">它會修改的 toorun App Service 上 (如需詳細資訊，請參閱 hello MEAN.js 儲存機制[讀我檔案](https://github.com/Azure-Samples/meanjs/blob/master/README.md))。</span><span class="sxs-lookup"><span data-stu-id="0f310-139">It is modified toorun on App Service (for more information, see hello MEAN.js repository [README file](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span></span>

### <a name="run-hello-application"></a><span data-ttu-id="0f310-140">執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="0f310-140">Run hello application</span></span>

<span data-ttu-id="0f310-141">執行下列命令 tooinstall hello 所需封裝的 hello 和啟動 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f310-141">Run hello following commands tooinstall hello required packages and start hello application.</span></span>

```bash
cd meanjs
npm install
npm start
```

<span data-ttu-id="0f310-142">完全載入 hello 應用程式時，您會看到下列訊息類似 toohello:</span><span class="sxs-lookup"><span data-stu-id="0f310-142">When hello app is fully loaded, you see something similar toohello following message:</span></span>

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

<span data-ttu-id="0f310-143">瀏覽 toohttp://localhost:3000 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="0f310-143">Navigate toohttp://localhost:3000 in a browser.</span></span> <span data-ttu-id="0f310-144">按一下**註冊**入 hello 上方的功能表，並建立測試使用者。</span><span class="sxs-lookup"><span data-stu-id="0f310-144">Click **Sign Up** in hello top menu and create a test user.</span></span> 

<span data-ttu-id="0f310-145">hello MEAN.js 範例應用程式會將使用者資料儲存在 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0f310-145">hello MEAN.js sample application stores user data in hello database.</span></span> <span data-ttu-id="0f310-146">如果您在建立使用者和登入成功時，您的應用程式會撰寫資料 toohello 本機 MongoDB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0f310-146">If you are successful at creating a user and signing in, then your app is writing data toohello local MongoDB database.</span></span>

![MEAN.js 順利連線 tooMongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

<span data-ttu-id="0f310-148">選取**Admin > 管理文件**tooadd 某些文件。</span><span class="sxs-lookup"><span data-stu-id="0f310-148">Select **Admin > Manage Articles** tooadd some articles.</span></span>

<span data-ttu-id="0f310-149">toostop Node.js，也可以隨時按`Ctrl+C`hello 終端機中。</span><span class="sxs-lookup"><span data-stu-id="0f310-149">toostop Node.js at any time, press `Ctrl+C` in hello terminal.</span></span> 

## <a name="create-production-mongodb"></a><span data-ttu-id="0f310-150">建立生產環境 MongoDB</span><span class="sxs-lookup"><span data-stu-id="0f310-150">Create production MongoDB</span></span>

<span data-ttu-id="0f310-151">在此步驟中，您要在 Azure 中建立 MongoDB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0f310-151">In this step, you create a MongoDB database in Azure.</span></span> <span data-ttu-id="0f310-152">已部署的 tooAzure 您的應用程式時，它會使用此雲端的資料庫。</span><span class="sxs-lookup"><span data-stu-id="0f310-152">When your app is deployed tooAzure, it uses this cloud database.</span></span>

<span data-ttu-id="0f310-153">針對 MongoDB，本教學課程使用 [Azure Cosmos DB](/azure/documentdb/)。</span><span class="sxs-lookup"><span data-stu-id="0f310-153">For MongoDB, this tutorial uses [Azure Cosmos DB](/azure/documentdb/).</span></span> <span data-ttu-id="0f310-154">Cosmos DB 支援 MongoDB 用戶端連線。</span><span class="sxs-lookup"><span data-stu-id="0f310-154">Cosmos DB supports MongoDB client connections.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="0f310-155">登入 tooAzure</span><span class="sxs-lookup"><span data-stu-id="0f310-155">Log in tooAzure</span></span>

<span data-ttu-id="0f310-156">您將在 Azure 中使用 Azure CLI 2.0 hello toocreate hello 所需資源 toohost 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f310-156">You'll use hello Azure CLI 2.0 toocreate hello resources needed toohost your app in Azure.</span></span> <span data-ttu-id="0f310-157">登入 Azure 訂用帳戶以 hello tooyour [az 登入](/cli/azure/#login)命令，並遵循螢幕上指示 hello。</span><span class="sxs-lookup"><span data-stu-id="0f310-157">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="0f310-158">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="0f310-158">Create a resource group</span></span>

<span data-ttu-id="0f310-159">建立資源群組以 hello [az 群組建立](/cli/azure/group#create)命令。</span><span class="sxs-lookup"><span data-stu-id="0f310-159">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="0f310-160">hello 下列範例會建立資源群組中 hello 西歐地區。</span><span class="sxs-lookup"><span data-stu-id="0f310-160">hello following example creates a resource group in hello West Europe region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

<span data-ttu-id="0f310-161">使用 hello [az appservice 列出位置](/cli/azure/appservice#list-locations)Azure CLI 命令 toolist 可用的位置。</span><span class="sxs-lookup"><span data-stu-id="0f310-161">Use hello [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command toolist available locations.</span></span> 

### <a name="create-a-cosmos-db-account"></a><span data-ttu-id="0f310-162">建立 Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="0f310-162">Create a Cosmos DB account</span></span>

<span data-ttu-id="0f310-163">建立以 hello Cosmos DB 帳戶[az cosmosdb 建立](/cli/azure/cosmosdb#create)命令。</span><span class="sxs-lookup"><span data-stu-id="0f310-163">Create a Cosmos DB account with hello [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="0f310-164">在 hello 下列命令，以取代 hello 的唯一 Cosmos DB 名稱 *\<cosmosdb_name >*預留位置。</span><span class="sxs-lookup"><span data-stu-id="0f310-164">In hello following command, substitute a unique Cosmos DB name for hello *\<cosmosdb_name>* placeholder.</span></span> <span data-ttu-id="0f310-165">這個名稱會當做 hello 一部分 hello Cosmos DB 端點， `https://<cosmosdb_name>.documents.azure.com/`，因此 hello 名稱需要 toobe 唯一跨所有 Cosmos DB 帳戶在 Azure 中。</span><span class="sxs-lookup"><span data-stu-id="0f310-165">This name is used as hello part of hello Cosmos DB endpoint, `https://<cosmosdb_name>.documents.azure.com/`, so hello name needs toobe unique across all Cosmos DB accounts in Azure.</span></span> <span data-ttu-id="0f310-166">hello 名稱必須包含小寫字母、 數字和 hello 連字號 （-） 字元，且必須介於 3 到 50 個字元之間。</span><span class="sxs-lookup"><span data-stu-id="0f310-166">hello name must contain only lowercase letters, numbers, and hello hyphen (-) character, and must be between 3 and 50 characters long.</span></span>

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

<span data-ttu-id="0f310-167">hello *-kind MongoDB*參數可啟用 MongoDB 用戶端連線。</span><span class="sxs-lookup"><span data-stu-id="0f310-167">hello *--kind MongoDB* parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="0f310-168">建立 hello Cosmos DB 帳戶時，hello Azure CLI 顯示資訊的類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="0f310-168">When hello Cosmos DB account is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

## <a name="connect-app-tooproduction-mongodb"></a><span data-ttu-id="0f310-169">連接應用程式 tooproduction MongoDB</span><span class="sxs-lookup"><span data-stu-id="0f310-169">Connect app tooproduction MongoDB</span></span>

<span data-ttu-id="0f310-170">在此步驟中，您可以連接 MEAN.js 範例應用程式 toohello Cosmos DB 資料庫您剛剛建立，使用 MongoDB 連接字串。</span><span class="sxs-lookup"><span data-stu-id="0f310-170">In this step, you connect your MEAN.js sample application toohello Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

### <a name="retrieve-hello-database-key"></a><span data-ttu-id="0f310-171">擷取 hello 資料庫金鑰</span><span class="sxs-lookup"><span data-stu-id="0f310-171">Retrieve hello database key</span></span>

<span data-ttu-id="0f310-172">tooconnect toohello Cosmos DB 資料庫，您必須 hello 資料庫金鑰。</span><span class="sxs-lookup"><span data-stu-id="0f310-172">tooconnect toohello Cosmos DB database, you need hello database key.</span></span> <span data-ttu-id="0f310-173">使用 hello [az cosmosdb 清單索引鍵](/cli/azure/cosmosdb#list-keys)命令 tooretrieve hello 主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="0f310-173">Use hello [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command tooretrieve hello primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

<span data-ttu-id="0f310-174">hello Azure CLI 顯示資訊的類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="0f310-174">hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

複製 hello 值`primaryMasterKey`。 <span data-ttu-id="0f310-176">您需要這個 hello 下一個步驟中的資訊。</span><span class="sxs-lookup"><span data-stu-id="0f310-176">You need this information in hello next step.</span></span>

<a name="devconfig"></a>
### <a name="configure-hello-connection-string-in-your-nodejs-application"></a><span data-ttu-id="0f310-177">Node.js 應用程式中設定 hello 連接字串</span><span class="sxs-lookup"><span data-stu-id="0f310-177">Configure hello connection string in your Node.js application</span></span>

<span data-ttu-id="0f310-178">在您的 MEAN.js 存放庫中，開啟 _config/env/production.js_。</span><span class="sxs-lookup"><span data-stu-id="0f310-178">In your MEAN.js repository, open _config/env/production.js_.</span></span>

<span data-ttu-id="0f310-179">在 hello`db`物件，更新 hello 值`uri`:</span><span class="sxs-lookup"><span data-stu-id="0f310-179">In hello `db` object, update hello value of `uri`:</span></span>

* <span data-ttu-id="0f310-180">取代 hello 兩 *\<cosmosdb_name >*預留位置取代您 Cosmos DB 的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="0f310-180">Replace hello two *\<cosmosdb_name>* placeholders with your Cosmos DB database name.</span></span>
* <span data-ttu-id="0f310-181">取代 hello  *\<primary_master_key >*預留位置 hello hello 先前步驟中複製的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="0f310-181">Replace hello *\<primary_master_key>* placeholder with hello key you copied in hello previous step.</span></span>

<span data-ttu-id="0f310-182">hello 下列程式碼顯示 hello`db`物件：</span><span class="sxs-lookup"><span data-stu-id="0f310-182">hello following code shows hello `db` object:</span></span>

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

<span data-ttu-id="0f310-183">hello`ssl=true`選項是必要的因為[Cosmos DB 需要 SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements)。</span><span class="sxs-lookup"><span data-stu-id="0f310-183">hello `ssl=true` option is required because [Cosmos DB requires SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 

<span data-ttu-id="0f310-184">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="0f310-184">Save your changes.</span></span>

### <a name="test-hello-application-in-production-mode"></a><span data-ttu-id="0f310-185">在實際執行模式中測試 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="0f310-185">Test hello application in production mode</span></span> 

<span data-ttu-id="0f310-186">執行下列命令 toominify 和組合指令碼 hello 的生產環境的 hello。</span><span class="sxs-lookup"><span data-stu-id="0f310-186">Run hello following command toominify and bundle scripts for hello production environment.</span></span> <span data-ttu-id="0f310-187">此程序會產生所需的 hello 實際執行環境的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="0f310-187">This process generates hello files needed by hello production environment.</span></span>

```bash
gulp prod
```

<span data-ttu-id="0f310-188">執行下列命令 toouse hello 您在設定連接字串的 hello _config/env/production.js_。</span><span class="sxs-lookup"><span data-stu-id="0f310-188">Run hello following command toouse hello connection string you configured in _config/env/production.js_.</span></span>

```bash
NODE_ENV=production node server.js
```

<span data-ttu-id="0f310-189">`NODE_ENV=production`設定告知 Node.js toorun hello 實際執行環境中的 hello 環境變數。</span><span class="sxs-lookup"><span data-stu-id="0f310-189">`NODE_ENV=production` sets hello environment variable that tells Node.js toorun in hello production environment.</span></span>  <span data-ttu-id="0f310-190">`node server.js`啟動 hello Node.js 伺服器和`server.js`儲存機制根目錄中。</span><span class="sxs-lookup"><span data-stu-id="0f310-190">`node server.js` starts hello Node.js server with `server.js` in your repository root.</span></span> <span data-ttu-id="0f310-191">這是在 Azure 中載入 Node.js 應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="0f310-191">This is how your Node.js application is loaded in Azure.</span></span> 

<span data-ttu-id="0f310-192">載入 hello 應用程式時，請檢查 toomake 確定 hello 實際執行環境中執行它：</span><span class="sxs-lookup"><span data-stu-id="0f310-192">When hello app is loaded, check toomake sure that it's running in hello production environment:</span></span>

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

<span data-ttu-id="0f310-193">瀏覽 toohttp://localhost:8443 瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="0f310-193">Navigate toohttp://localhost:8443 in a browser.</span></span> <span data-ttu-id="0f310-194">按一下**註冊**入 hello 上方的功能表，並建立測試使用者。</span><span class="sxs-lookup"><span data-stu-id="0f310-194">Click **Sign Up** in hello top menu and create a test user.</span></span> <span data-ttu-id="0f310-195">如果您成功建立使用者和登入，您的應用程式會在 Azure 中撰寫資料 toohello Cosmos DB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0f310-195">If you are successful creating a user and signing in, then your app is writing data toohello Cosmos DB database in Azure.</span></span> 

<span data-ttu-id="0f310-196">在終端機 hello，請輸入，Node.js 停止`Ctrl+C`。</span><span class="sxs-lookup"><span data-stu-id="0f310-196">In hello terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

## <a name="deploy-app-tooazure"></a><span data-ttu-id="0f310-197">部署應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="0f310-197">Deploy app tooAzure</span></span>

<span data-ttu-id="0f310-198">在此步驟中，您可以部署您 MongoDB 連接 Node.js 應用程式 tooAzure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="0f310-198">In this step, you deploy your MongoDB-connected Node.js application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="0f310-199">建立應用程式服務方案</span><span class="sxs-lookup"><span data-stu-id="0f310-199">Create an App Service plan</span></span>

<span data-ttu-id="0f310-200">建立應用程式服務方案以 hello [az 應用程式服務方案建立](/cli/azure/appservice/plan#create)命令。</span><span class="sxs-lookup"><span data-stu-id="0f310-200">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="0f310-201">hello 下列範例會建立名為 App Service 方案_myAppServicePlan_使用 hello**免費**定價層：</span><span class="sxs-lookup"><span data-stu-id="0f310-201">hello following example creates an App Service plan named _myAppServicePlan_ using hello **FREE** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="0f310-202">建立 hello 應用程式服務方案時，hello Azure CLI 顯示資訊的類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="0f310-202">When hello App Service plan is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-web-app"></a><span data-ttu-id="0f310-203">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="0f310-203">Create a web app</span></span>

<span data-ttu-id="0f310-204">建立 web 應用程式在 hello`myAppServicePlan`應用程式服務方案以 hello [az webapp 建立](/cli/azure/webapp#create)命令。</span><span class="sxs-lookup"><span data-stu-id="0f310-204">Create a web app in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="0f310-205">hello web 應用程式可讓您裝載空間 toodeploy 您的程式碼和為您提供 URL tooview hello 部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f310-205">hello web app gives you a hosting space toodeploy your code and provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="0f310-206">使用 toocreate hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f310-206">Use  toocreate hello web app.</span></span> 

<span data-ttu-id="0f310-207">在 hello 下列命令，將取代 hello  *\<app_name >*具有唯一的應用程式名稱的預留位置。</span><span class="sxs-lookup"><span data-stu-id="0f310-207">In hello following command, replace hello *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="0f310-208">這個名稱會做為 hello hello 預設 URL 的一部分 hello web 應用程式，因此 hello 名稱需要 toobe 唯一跨 Azure App Service 中的所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f310-208">This name is used as hello part of hello default URL for hello web app, so hello name needs toobe unique across all apps in Azure App Service.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="0f310-209">Hello web 應用程式建立後，hello Azure CLI 顯示資訊的類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="0f310-209">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-an-environment-variable"></a><span data-ttu-id="0f310-210">設定環境變數</span><span class="sxs-lookup"><span data-stu-id="0f310-210">Configure an environment variable</span></span>

<span data-ttu-id="0f310-211">稍早在 hello 教學課程，您硬式編碼 hello 資料庫連接字串中_config/env/production.js_。</span><span class="sxs-lookup"><span data-stu-id="0f310-211">Earlier in hello tutorial, you hardcoded hello database connection string in _config/env/production.js_.</span></span> <span data-ttu-id="0f310-212">為了保持安全性最佳作法，想要 tookeep 這個敏感性資料從您的 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="0f310-212">In keeping with security best practice, you want tookeep this sensitive data out of your Git repository.</span></span> <span data-ttu-id="0f310-213">為了在 Azure 中執行應用程式，您將改用環境變數。</span><span class="sxs-lookup"><span data-stu-id="0f310-213">For your app running in Azure, you'll use an environment variable instead.</span></span>

<span data-ttu-id="0f310-214">在應用程式服務中，您設定環境變數為_應用程式設定_使用 hello [az webapp config appsettings 更新](/cli/azure/webapp/config/appsettings#update)命令。</span><span class="sxs-lookup"><span data-stu-id="0f310-214">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings update](/cli/azure/webapp/config/appsettings#update) command.</span></span> 

<span data-ttu-id="0f310-215">hello 下列範例會設定`MONGODB_URI`Azure web 應用程式中的應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="0f310-215">hello following example configures a `MONGODB_URI` app setting in your Azure web app.</span></span> <span data-ttu-id="0f310-216">取代 hello  *\<app_name >*，  *\<cosmosdb_name >*，和 *\<primary_master_key >*預留位置。</span><span class="sxs-lookup"><span data-stu-id="0f310-216">Replace hello *\<app_name>*, *\<cosmosdb_name>*, and *\<primary_master_key>* placeholders.</span></span>

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

<span data-ttu-id="0f310-217">在 Node.js 程式碼中，您可以利用 `process.env.MONGODB_URI` 來存取此應用程式設定，就像存取任何環境變數一樣。</span><span class="sxs-lookup"><span data-stu-id="0f310-217">In Node.js code, you access this app setting with `process.env.MONGODB_URI`, just like you would access any environment variable.</span></span> 

<span data-ttu-id="0f310-218">現在，復原變更 too_config/env/production.js_ 以 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="0f310-218">Now, undo your changes too_config/env/production.js_ with hello following command:</span></span>

```bash
git checkout -- .
```

<span data-ttu-id="0f310-219">再次開啟 _config/env/production.js_。</span><span class="sxs-lookup"><span data-stu-id="0f310-219">Open _config/env/production.js_ again.</span></span> <span data-ttu-id="0f310-220">請注意該 hello 預設 MEAN.js 應用程式已設定的 toouse hello`MONGODB_URI`您建立的環境變數。</span><span class="sxs-lookup"><span data-stu-id="0f310-220">Note that hello default MEAN.js app is already configured toouse hello `MONGODB_URI` environment variable that you created.</span></span>

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a><span data-ttu-id="0f310-221">設定本機 git 部署</span><span class="sxs-lookup"><span data-stu-id="0f310-221">Configure local git deployment</span></span> 

<span data-ttu-id="0f310-222">使用 hello [az webapp 部署使用者集合](/cli/azure/webapp/deployment/user#set)命令 toocreate 認證進行部署。</span><span class="sxs-lookup"><span data-stu-id="0f310-222">Use hello [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command toocreate credentials for deployment.</span></span>

<span data-ttu-id="0f310-223">您可以部署您的應用程式 tooAzure 應用程式服務，以各種方式，包括 FTP、 本機 Git、 GitHub、 Visual Studio Team Services 和 BitBucket。</span><span class="sxs-lookup"><span data-stu-id="0f310-223">You can deploy your application tooAzure App Service in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="0f310-224">若為 FTP 和本機 Git，則需要您的部署 hello 伺服器 tooauthenticate toohave 部署使用者設定。</span><span class="sxs-lookup"><span data-stu-id="0f310-224">For FTP and local Git, it is necessary toohave a deployment user configured on hello server tooauthenticate your deployment.</span></span> <span data-ttu-id="0f310-225">此部署使用者是帳戶層級，與 Azure 訂用帳戶的帳戶不同。</span><span class="sxs-lookup"><span data-stu-id="0f310-225">This deployment user is account-level and is different from your Azure subscription account.</span></span> <span data-ttu-id="0f310-226">您只需要 tooconfigure 這個部署使用者一次。</span><span class="sxs-lookup"><span data-stu-id="0f310-226">You only need tooconfigure this deployment user once.</span></span>

<span data-ttu-id="0f310-227">下列命令，取代在 hello *\<使用者名稱 >*和*\<密碼 >*與新的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="0f310-227">In hello following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="0f310-228">hello 使用者名稱必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="0f310-228">hello user name must be unique.</span></span> <span data-ttu-id="0f310-229">hello 密碼必須至少為八個字元，以下列三個元素的 hello 的兩個： 字母、 數字、 符號。</span><span class="sxs-lookup"><span data-stu-id="0f310-229">hello password must be at least eight characters long, with two of hello following three elements:  letters, numbers, symbols.</span></span> <span data-ttu-id="0f310-230">如果您收到` 'Conflict'. Details: 409`錯誤，變更 hello 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="0f310-230">If you get a ` 'Conflict'. Details: 409` error, change hello username.</span></span> <span data-ttu-id="0f310-231">如果您收到 ` 'Bad Request'. Details: 400` 錯誤，請使用更強的密碼。</span><span class="sxs-lookup"><span data-stu-id="0f310-231">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="0f310-232">記錄 hello 使用者名稱和密碼，以在稍後的步驟，當您部署的 hello 應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="0f310-232">Record hello user name and password for use in later steps when you deploy hello app.</span></span>

<span data-ttu-id="0f310-233">使用 hello [az webapp 部署來源設定為本機的 git](/cli/azure/webapp/deployment/source#config-local-git)命令 tooconfigure 本機 Git 存取 toohello Azure web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f310-233">Use hello [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command tooconfigure local Git access toohello Azure web app.</span></span> 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

<span data-ttu-id="0f310-234">Hello 部署使用者設定時，Azure CLI hello 會顯示 hello Azure web 應用程式的部署 URL 中 hello 下列格式：</span><span class="sxs-lookup"><span data-stu-id="0f310-234">When hello deployment user is configured, hello Azure CLI shows hello deployment URL for your Azure web app in hello following format:</span></span>

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

<span data-ttu-id="0f310-235">因為它會使用 hello 下一個步驟中複製 hello hello 終端機中，從輸出。</span><span class="sxs-lookup"><span data-stu-id="0f310-235">Copy hello output from hello terminal, as it will be used in hello next step.</span></span> 

### <a name="push-tooazure-from-git"></a><span data-ttu-id="0f310-236">從 Git 推送 tooAzure</span><span class="sxs-lookup"><span data-stu-id="0f310-236">Push tooAzure from Git</span></span>

<span data-ttu-id="0f310-237">新增 Azure 遠端 tooyour 本機 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="0f310-237">Add an Azure remote tooyour local Git repository.</span></span> 

```bash
git remote add azure <paste_copied_url_here> 
```

<span data-ttu-id="0f310-238">推送 toohello Azure 遠端 toodeploy Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f310-238">Push toohello Azure remote toodeploy your Node.js application.</span></span> <span data-ttu-id="0f310-239">安裝程式將會提示您稍早提供一部分 hello hello 部署使用者建立的 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="0f310-239">You will be prompted for hello password you supplied earlier as part of hello creation of hello deployment user.</span></span> 

```bash
git push azure master
```

<span data-ttu-id="0f310-240">在部署期間，Azure App Service 會與 Git 溝通其進度。</span><span class="sxs-lookup"><span data-stu-id="0f310-240">During deployment, Azure App Service communicates its progress with Git.</span></span>

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

<span data-ttu-id="0f310-241">您可能會注意到 hello 部署程序執行[Gulp](http://gulpjs.com/)之後`npm install`。</span><span class="sxs-lookup"><span data-stu-id="0f310-241">You may notice that hello deployment process runs [Gulp](http://gulpjs.com/) after `npm install`.</span></span> <span data-ttu-id="0f310-242">應用程式服務不會在部署期間執行 Gulp 或 grunt 所完成的工作，因此這個範例儲存機制具有兩個額外的檔案其根目錄 tooenable 它：</span><span class="sxs-lookup"><span data-stu-id="0f310-242">App Service does not run Gulp or Grunt tasks during deployment, so this sample repository has two additional files in its root directory tooenable it:</span></span> 

- <span data-ttu-id="0f310-243">_.deployment_ -此檔案會告知應用程式服務 toorun `bash deploy.sh` hello 自訂部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="0f310-243">_.deployment_ - This file tells App Service toorun `bash deploy.sh` as hello custom deployment script.</span></span>
- <span data-ttu-id="0f310-244">_deploy.sh_ -hello 自訂部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="0f310-244">_deploy.sh_ - hello custom deployment script.</span></span> <span data-ttu-id="0f310-245">如果您檢閱 hello 檔案時，您會看到應用程式會執行`gulp prod`之後`npm install`和`bower install`。</span><span class="sxs-lookup"><span data-stu-id="0f310-245">If you review hello file, you will see that it runs `gulp prod` after `npm install` and `bower install`.</span></span> 

<span data-ttu-id="0f310-246">您可以使用此方法 tooadd 任何步驟 tooyour Git 為基礎的部署。</span><span class="sxs-lookup"><span data-stu-id="0f310-246">You can use this approach tooadd any step tooyour Git-based deployment.</span></span> <span data-ttu-id="0f310-247">如果您在任一時間點重新啟動 Azure Web 應用程式，App Service 並不會重新執行這些自動化工作。</span><span class="sxs-lookup"><span data-stu-id="0f310-247">If you restart your Azure web app at any point, App Service doesn't rerun these automation tasks.</span></span>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="0f310-248">瀏覽 toohello Azure web 應用程式</span><span class="sxs-lookup"><span data-stu-id="0f310-248">Browse toohello Azure web app</span></span> 

<span data-ttu-id="0f310-249">瀏覽使用網頁瀏覽器 toohello 部署 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f310-249">Browse toohello deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
``` 

<span data-ttu-id="0f310-250">按一下**註冊**入 hello 上方的功能表，並建立虛擬使用者。</span><span class="sxs-lookup"><span data-stu-id="0f310-250">Click **Sign Up** in hello top menu and create a dummy user.</span></span> 

<span data-ttu-id="0f310-251">如果您為成功，而且 hello 應用程式會自動登入 toohello 在 Azure 中建立使用者，然後 MEAN.js 應用程式都有連線能力 toohello MongoDB (Cosmos DB) 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0f310-251">If you are successful and hello app automatically signs in toohello created user, then your MEAN.js app in Azure has connectivity toohello MongoDB (Cosmos DB) database.</span></span> 

![在 Azure App Service 中執行的 MEAN.js 應用程式](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="0f310-253">選取**Admin > 管理文件**tooadd 某些文件。</span><span class="sxs-lookup"><span data-stu-id="0f310-253">Select **Admin > Manage Articles** tooadd some articles.</span></span> 

<span data-ttu-id="0f310-254">**恭喜！**</span><span class="sxs-lookup"><span data-stu-id="0f310-254">**Congratulations!**</span></span> <span data-ttu-id="0f310-255">您正在 Azure App Service 中執行資料驅動的 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0f310-255">You're running a data-driven Node.js app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="0f310-256">更新資料模型並重新部署</span><span class="sxs-lookup"><span data-stu-id="0f310-256">Update data model and redeploy</span></span>

<span data-ttu-id="0f310-257">在此步驟中，您可以變更 hello`article`資料模型，並發行變更 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="0f310-257">In this step, you change hello `article` data model and publish your change tooAzure.</span></span>

### <a name="update-hello-data-model"></a><span data-ttu-id="0f310-258">更新 hello 資料模型</span><span class="sxs-lookup"><span data-stu-id="0f310-258">Update hello data model</span></span>

<span data-ttu-id="0f310-259">開啟 _modules/articles/server/models/article.server.model.js_。</span><span class="sxs-lookup"><span data-stu-id="0f310-259">Open _modules/articles/server/models/article.server.model.js_.</span></span>

<span data-ttu-id="0f310-260">在 `ArticleSchema` 中，新增名為 `comment` 的 `String` 類型。</span><span class="sxs-lookup"><span data-stu-id="0f310-260">In `ArticleSchema`, add a `String` type called `comment`.</span></span> <span data-ttu-id="0f310-261">完成時，您的結構描述程式碼應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="0f310-261">When you're done, your schema code should look like this:</span></span>

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

### <a name="update-hello-articles-code"></a><span data-ttu-id="0f310-262">更新 hello 文件的程式碼</span><span class="sxs-lookup"><span data-stu-id="0f310-262">Update hello articles code</span></span>

<span data-ttu-id="0f310-263">更新的 hello rest 您`articles`程式碼 toouse `comment`。</span><span class="sxs-lookup"><span data-stu-id="0f310-263">Update hello rest of your `articles` code toouse `comment`.</span></span>

<span data-ttu-id="0f310-264">有五個檔案，您需要 toomodify: hello 伺服器控制器和 hello 四個用戶端檢視。</span><span class="sxs-lookup"><span data-stu-id="0f310-264">There are five files you need toomodify: hello server controller and hello four client views.</span></span> 

<span data-ttu-id="0f310-265">開啟 _modules/articles/server/controllers/articles.server.controller.js_。</span><span class="sxs-lookup"><span data-stu-id="0f310-265">Open _modules/articles/server/controllers/articles.server.controller.js_.</span></span>

<span data-ttu-id="0f310-266">在 hello`update`函式中，新增的指派`article.comment`。</span><span class="sxs-lookup"><span data-stu-id="0f310-266">In hello `update` function, add an assignment for `article.comment`.</span></span> <span data-ttu-id="0f310-267">hello 下列程式碼顯示 hello 完成`update`函式：</span><span class="sxs-lookup"><span data-stu-id="0f310-267">hello following code shows hello completed `update` function:</span></span>

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

<span data-ttu-id="0f310-268">開啟 _modules/articles/client/views/view-article.client.view.html_。</span><span class="sxs-lookup"><span data-stu-id="0f310-268">Open _modules/articles/client/views/view-article.client.view.html_.</span></span>

<span data-ttu-id="0f310-269">正上方 hello 右`</section>`標記中加入下列行 toodisplay hello`comment`連同其他部分 hello hello 發行項資料：</span><span class="sxs-lookup"><span data-stu-id="0f310-269">Just above hello closing `</section>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

<span data-ttu-id="0f310-270">開啟 _modules/articles/client/views/list-articles.client.view.html_。</span><span class="sxs-lookup"><span data-stu-id="0f310-270">Open _modules/articles/client/views/list-articles.client.view.html_.</span></span>

<span data-ttu-id="0f310-271">正上方 hello 右`</a>`標記中加入下列行 toodisplay hello`comment`連同其他部分 hello hello 發行項資料：</span><span class="sxs-lookup"><span data-stu-id="0f310-271">Just above hello closing `</a>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

<span data-ttu-id="0f310-272">開啟 _modules/articles/client/views/admin/list-articles.client.view.html_。</span><span class="sxs-lookup"><span data-stu-id="0f310-272">Open _modules/articles/client/views/admin/list-articles.client.view.html_.</span></span>

<span data-ttu-id="0f310-273">內部 hello`<div class="list-group">`元素與 hello 結尾的正上方`</a>`標記中加入下列行 toodisplay hello`comment`連同其他部分 hello hello 發行項資料：</span><span class="sxs-lookup"><span data-stu-id="0f310-273">Inside hello `<div class="list-group">` element and just above hello closing `</a>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

<span data-ttu-id="0f310-274">開啟 _modules/articles/client/views/admin/form-article.client.view.html_。</span><span class="sxs-lookup"><span data-stu-id="0f310-274">Open _modules/articles/client/views/admin/form-article.client.view.html_.</span></span>

<span data-ttu-id="0f310-275">尋找 hello`<div class="form-group">`包含 hello 送出按鈕，像這樣的項目：</span><span class="sxs-lookup"><span data-stu-id="0f310-275">Find hello `<div class="form-group">` element that contains hello submit button, which looks like this:</span></span>

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

<span data-ttu-id="0f310-276">此標記的正上方加入另一個`<div class="form-group">`項目，可讓人員編輯 hello`comment`欄位。</span><span class="sxs-lookup"><span data-stu-id="0f310-276">Just above this tag, add another `<div class="form-group">` element that lets people edit hello `comment` field.</span></span> <span data-ttu-id="0f310-277">新的元素應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="0f310-277">Your new element should look like this:</span></span>

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="0f310-278">本機測試您的變更</span><span class="sxs-lookup"><span data-stu-id="0f310-278">Test your changes locally</span></span>

<span data-ttu-id="0f310-279">儲存您的所有變更。</span><span class="sxs-lookup"><span data-stu-id="0f310-279">Save all your changes.</span></span>

<span data-ttu-id="0f310-280">再次在生產模式中測試您的變更。</span><span class="sxs-lookup"><span data-stu-id="0f310-280">Test your changes in production mode again.</span></span>

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> <span data-ttu-id="0f310-281">請記住，您_config/env/production.js_已還原，和 hello `MONGODB_URI` Azure web 應用程式中，而不是在本機電腦，才會設定環境變數。</span><span class="sxs-lookup"><span data-stu-id="0f310-281">Remember that your _config/env/production.js_ has been reverted, and hello `MONGODB_URI` environment variable is only set in your Azure web app and not on your local machine.</span></span> <span data-ttu-id="0f310-282">如果您看一下 hello 設定檔，您會發現該 hello production 組態預設值 toouse 本機 MongoDB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="0f310-282">If you look at hello config file, you find that hello production configuration defaults toouse a local MongoDB database.</span></span> <span data-ttu-id="0f310-283">如此可確保當您在本機測試程式碼變更時，不會碰觸到生產資料。</span><span class="sxs-lookup"><span data-stu-id="0f310-283">This makes sure that you don't touch production data when you test your code changes locally.</span></span>

<span data-ttu-id="0f310-284">瀏覽過`http://localhost:8443`瀏覽器中，並確定您已登入。</span><span class="sxs-lookup"><span data-stu-id="0f310-284">Navigate too`http://localhost:8443` in a browser and make sure that you're signed in.</span></span>

<span data-ttu-id="0f310-285">選取**Admin > 管理文件**，然後加入發行項藉由選取 hello  **+**   按鈕。</span><span class="sxs-lookup"><span data-stu-id="0f310-285">Select **Admin > Manage Articles**, then add an article by selecting hello **+** button.</span></span>

<span data-ttu-id="0f310-286">您會看見 hello 新`Comment`現在文字方塊。</span><span class="sxs-lookup"><span data-stu-id="0f310-286">You see hello new `Comment` textbox now.</span></span>

![加入註解欄位 tooArticles](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

<span data-ttu-id="0f310-288">在終端機 hello，請輸入，Node.js 停止`Ctrl+C`。</span><span class="sxs-lookup"><span data-stu-id="0f310-288">In hello terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

### <a name="publish-changes-tooazure"></a><span data-ttu-id="0f310-289">發行變更 tooAzure</span><span class="sxs-lookup"><span data-stu-id="0f310-289">Publish changes tooAzure</span></span>

<span data-ttu-id="0f310-290">認可您的變更在 Git，然後推送 hello 程式碼變更 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="0f310-290">Commit your changes in Git, then push hello code changes tooAzure.</span></span>

```bash
git commit -am "added article comment"
git push azure master
```

<span data-ttu-id="0f310-291">一次 hello`git push`已完成，請瀏覽 tooyour Azure web 應用程式並再試一次 hello 新功能。</span><span class="sxs-lookup"><span data-stu-id="0f310-291">Once hello `git push` is complete, navigate tooyour Azure web app and try out hello new functionality.</span></span>

![發行 tooAzure 模型與資料庫的變更。](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

<span data-ttu-id="0f310-293">如果您先前已新增任何文章，您仍然可以看到它們。</span><span class="sxs-lookup"><span data-stu-id="0f310-293">If you added any articles earlier, you still can see them.</span></span> <span data-ttu-id="0f310-294">Cosmos DB 中的現有資料不會遺失。</span><span class="sxs-lookup"><span data-stu-id="0f310-294">Existing data in your Cosmos DB is not lost.</span></span> <span data-ttu-id="0f310-295">此外，您更新 toohello 資料的結構描述，會保留現有的資料。</span><span class="sxs-lookup"><span data-stu-id="0f310-295">Also, your updates toohello data schema and leaves your existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="0f310-296">資料流診斷記錄</span><span class="sxs-lookup"><span data-stu-id="0f310-296">Stream diagnostic logs</span></span> 

<span data-ttu-id="0f310-297">Node.js 應用程式執行的 Azure 應用程式服務，而您可以取得 hello 主控台記錄檔傳送的 tooyour 終端機。</span><span class="sxs-lookup"><span data-stu-id="0f310-297">While your Node.js application runs in Azure App Service, you can get hello console logs piped tooyour terminal.</span></span> <span data-ttu-id="0f310-298">這樣一來，您可以取得 hello 相同的診斷訊息 toohelp 您偵錯應用程式錯誤。</span><span class="sxs-lookup"><span data-stu-id="0f310-298">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="0f310-299">資料流中，使用 hello toostart 記錄[az webapp 記錄結尾](/cli/azure/webapp/log#tail)命令。</span><span class="sxs-lookup"><span data-stu-id="0f310-299">toostart log streaming, use hello [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

<span data-ttu-id="0f310-300">記錄檔資料流啟動之後，重新整理在 hello 瀏覽器 tooget Azure web 應用程式一些 web 流量。</span><span class="sxs-lookup"><span data-stu-id="0f310-300">Once log streaming has started, refresh your Azure web app in hello browser tooget some web traffic.</span></span> <span data-ttu-id="0f310-301">您現在可以看到主控台記錄檔經由管道輸出 tooyour 終端機。</span><span class="sxs-lookup"><span data-stu-id="0f310-301">You now see console logs piped tooyour terminal.</span></span>

<span data-ttu-id="0f310-302">您隨時可以輸入 `Ctrl+C` 以停止記錄資料流。</span><span class="sxs-lookup"><span data-stu-id="0f310-302">Stop log streaming at any time by typing `Ctrl+C`.</span></span> 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="0f310-303">管理您的 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="0f310-303">Manage your Azure web app</span></span>

<span data-ttu-id="0f310-304">移 toohello [Azure 入口網站](https://portal.azure.com)toosee hello web 應用程式所建立。</span><span class="sxs-lookup"><span data-stu-id="0f310-304">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span>

<span data-ttu-id="0f310-305">從 hello 左窗格中，按一下 **應用程式服務**，然後按一下 hello Azure web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="0f310-305">From hello left menu, click **App Services**, then click hello name of your Azure web app.</span></span>

![入口網站瀏覽 tooAzure web 應用程式](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

<span data-ttu-id="0f310-307">根據預設，hello 入口網站會顯示 web 應用程式的**概觀**頁面。</span><span class="sxs-lookup"><span data-stu-id="0f310-307">By default, hello portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="0f310-308">此頁面可讓您檢視應用程式的執行方式。</span><span class="sxs-lookup"><span data-stu-id="0f310-308">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="0f310-309">您也可以在這裡執行基本管理工作，像是瀏覽、停止、啟動、重新啟動及刪除。</span><span class="sxs-lookup"><span data-stu-id="0f310-309">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="0f310-310">在左邊 hello 頁面 hello hello 索引標籤會顯示 hello 不同的組態頁面，您可以開啟。</span><span class="sxs-lookup"><span data-stu-id="0f310-310">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span>

![Azure 入口網站中的 App Service 頁面](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a><span data-ttu-id="0f310-312">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0f310-312">Next steps</span></span>

<span data-ttu-id="0f310-313">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="0f310-313">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0f310-314">在 Azure 中建立 MongoDB 資料庫</span><span class="sxs-lookup"><span data-stu-id="0f310-314">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="0f310-315">連接 Node.js 應用程式 tooMongoDB</span><span class="sxs-lookup"><span data-stu-id="0f310-315">Connect a Node.js app tooMongoDB</span></span>
> * <span data-ttu-id="0f310-316">部署 hello 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="0f310-316">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="0f310-317">更新 hello 資料模型，部署 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="0f310-317">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="0f310-318">從 Azure tooyour 終端機的資料流記錄檔</span><span class="sxs-lookup"><span data-stu-id="0f310-318">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="0f310-319">管理 hello hello Azure 入口網站中的應用程式</span><span class="sxs-lookup"><span data-stu-id="0f310-319">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="0f310-320">前進 toohello 下一個教學課程 toolearn toomap 自訂的 DNS 名稱 tooyour web 應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="0f310-320">Advance toohello next tutorial toolearn how toomap a custom DNS name tooyour web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="0f310-321">將現有自訂 DNS 名稱 tooAzure Web 應用程式的對應</span><span class="sxs-lookup"><span data-stu-id="0f310-321">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
