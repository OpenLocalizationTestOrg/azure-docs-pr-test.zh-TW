---
title: "在 Azure 中建置 Node.js 和 MongoDB Web 應用程式 | Microsoft Docs"
description: "了解如何取得在 Azure 中運作的 Node.js 應用程式，並利用 MongoDB 連接字串連線到 Cosmos DB 資料庫。"
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
ms.openlocfilehash: 3b309382be8cdf8d48b396207fd482a5dc5ed934
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a><span data-ttu-id="9d38d-103">在 Azure 中建置 Node.js 和 MongoDB Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9d38d-103">Build a Node.js and MongoDB web app in Azure</span></span>

<span data-ttu-id="9d38d-104">Azure Web Apps 提供可高度擴充、自我修復的 Web 主機服務。</span><span class="sxs-lookup"><span data-stu-id="9d38d-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="9d38d-105">本教學課程示範如何在 Azure 中建立 Node.js Web 應用程式，並將它連線到 MongoDB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="9d38d-105">This tutorial shows how to create a Node.js web app in Azure and connect it to a MongoDB database.</span></span> <span data-ttu-id="9d38d-106">完成之後，您的 MEAN 應用程式 (MongoDB、Express、AngularJS 及 Node.js) 將會在 [Azure App Service](app-service-web-overview.md) 中執行。</span><span class="sxs-lookup"><span data-stu-id="9d38d-106">When you're done, you'll have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running in [Azure App Service](app-service-web-overview.md).</span></span> <span data-ttu-id="9d38d-107">為了簡單起見，範例應用程式會使用 [MEAN.js web 架構](http://meanjs.org/)。</span><span class="sxs-lookup"><span data-stu-id="9d38d-107">For simplicity, the sample application uses the [MEAN.js web framework](http://meanjs.org/).</span></span>

![在 Azure App Service 中執行的 MEAN.js 應用程式](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="9d38d-109">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="9d38d-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9d38d-110">在 Azure 中建立 MongoDB 資料庫</span><span class="sxs-lookup"><span data-stu-id="9d38d-110">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="9d38d-111">將 Node.js 應用程式連線至 MongoDB</span><span class="sxs-lookup"><span data-stu-id="9d38d-111">Connect a Node.js app to MongoDB</span></span>
> * <span data-ttu-id="9d38d-112">將應用程式部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="9d38d-112">Deploy the app to Azure</span></span>
> * <span data-ttu-id="9d38d-113">將資料模型更新並將應用程式重新部署</span><span class="sxs-lookup"><span data-stu-id="9d38d-113">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="9d38d-114">來自 Azure 的串流診斷記錄</span><span class="sxs-lookup"><span data-stu-id="9d38d-114">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="9d38d-115">在 Azure 入口網站中管理應用程式</span><span class="sxs-lookup"><span data-stu-id="9d38d-115">Manage the app in the Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d38d-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="9d38d-116">Prerequisites</span></span>

<span data-ttu-id="9d38d-117">若要完成本教學課程：</span><span class="sxs-lookup"><span data-stu-id="9d38d-117">To complete this tutorial:</span></span>

1. [<span data-ttu-id="9d38d-118">安裝 Git</span><span class="sxs-lookup"><span data-stu-id="9d38d-118">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="9d38d-119">安裝 Node.js 和 NPM</span><span class="sxs-lookup"><span data-stu-id="9d38d-119">Install Node.js and NPM</span></span>](https://nodejs.org/)
1. <span data-ttu-id="9d38d-120">[安裝 Gulp.js](http://gulpjs.com/) ([MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started) 的必要項目)</span><span class="sxs-lookup"><span data-stu-id="9d38d-120">[Install Gulp.js](http://gulpjs.com/) (required by [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span></span>
1. [<span data-ttu-id="9d38d-121">安裝及執行 MongoDB Community 版本</span><span class="sxs-lookup"><span data-stu-id="9d38d-121">Install and run MongoDB Community Edition</span></span>](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9d38d-122">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="9d38d-122">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="9d38d-123">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="9d38d-123">Run `az --version` to find the version.</span></span> <span data-ttu-id="9d38d-124">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="9d38d-124">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-mongodb"></a><span data-ttu-id="9d38d-125">測試本機的 MongoDB</span><span class="sxs-lookup"><span data-stu-id="9d38d-125">Test local MongoDB</span></span>

<span data-ttu-id="9d38d-126">開啟終端機視窗，然後 `cd` 至 MongoDB 安裝的 `bin` 目錄。</span><span class="sxs-lookup"><span data-stu-id="9d38d-126">Open the terminal window and `cd` to the `bin` directory of your MongoDB installation.</span></span> <span data-ttu-id="9d38d-127">您可使用這個終端機視窗來執行本教學課程中的所有命令。</span><span class="sxs-lookup"><span data-stu-id="9d38d-127">You can use this terminal window to run all the commands in this tutorial.</span></span>

<span data-ttu-id="9d38d-128">在終端機上執行 `mongo`，以連接到本機的 MongoDB 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9d38d-128">Run `mongo` in the terminal to connect to your local MongoDB server.</span></span>

```bash
mongo
```

<span data-ttu-id="9d38d-129">如果連接成功，則您的 MongoDB 資料庫已在執行中。</span><span class="sxs-lookup"><span data-stu-id="9d38d-129">If your connection is successful, then your MongoDB database is already running.</span></span> <span data-ttu-id="9d38d-130">如果沒有，請確定您的本機 MongoDB 資料庫已遵循[安裝 MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/) 中的步驟來啟動。</span><span class="sxs-lookup"><span data-stu-id="9d38d-130">If not, make sure that your local MongoDB database is started by following the steps at [Install MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span></span> <span data-ttu-id="9d38d-131">MongoDB 通常已安裝，但您仍需要執行 `mongod` 才能將它啟動。</span><span class="sxs-lookup"><span data-stu-id="9d38d-131">Often, MongoDB is installed, but you still need to start it by running `mongod`.</span></span> 

<span data-ttu-id="9d38d-132">當您完成測試 MongoDB 資料庫時，在終端機上輸入 `Ctrl+C`。</span><span class="sxs-lookup"><span data-stu-id="9d38d-132">When you're done testing your MongoDB database, type `Ctrl+C` in the terminal.</span></span> 

## <a name="create-local-nodejs-app"></a><span data-ttu-id="9d38d-133">建立本機的 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="9d38d-133">Create local Node.js app</span></span>

<span data-ttu-id="9d38d-134">在此步驟中，您要設定本機的 Node.js 專案。</span><span class="sxs-lookup"><span data-stu-id="9d38d-134">In this step, you set up the local Node.js project.</span></span>

### <a name="clone-the-sample-application"></a><span data-ttu-id="9d38d-135">複製範例應用程式</span><span class="sxs-lookup"><span data-stu-id="9d38d-135">Clone the sample application</span></span>

<span data-ttu-id="9d38d-136">在終端機視窗中，使用 `cd` 移至工作目錄。</span><span class="sxs-lookup"><span data-stu-id="9d38d-136">In the terminal window, `cd` to a working directory.</span></span>  

<span data-ttu-id="9d38d-137">執行下列命令來複製範例存放庫。</span><span class="sxs-lookup"><span data-stu-id="9d38d-137">Run the following command to clone the sample repository.</span></span> 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

<span data-ttu-id="9d38d-138">此範例存放庫包含 [MEAN.js 存放庫](https://github.com/meanjs/mean)的副本。</span><span class="sxs-lookup"><span data-stu-id="9d38d-138">This sample repository contains a copy of the [MEAN.js repository](https://github.com/meanjs/mean).</span></span> <span data-ttu-id="9d38d-139">若要在 App Service 上執行，會將它做修改 (如需詳細資訊，請參閱 MEAN.js 存放庫[讀我檔案](https://github.com/Azure-Samples/meanjs/blob/master/README.md))。</span><span class="sxs-lookup"><span data-stu-id="9d38d-139">It is modified to run on App Service (for more information, see the MEAN.js repository [README file](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span></span>

### <a name="run-the-application"></a><span data-ttu-id="9d38d-140">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="9d38d-140">Run the application</span></span>

<span data-ttu-id="9d38d-141">執行下列命令以安裝必要的套件，然後啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d38d-141">Run the following commands to install the required packages and start the application.</span></span>

```bash
cd meanjs
npm install
npm start
```

<span data-ttu-id="9d38d-142">當應用程式完全載入時，您會看到類似下列的訊息：</span><span class="sxs-lookup"><span data-stu-id="9d38d-142">When the app is fully loaded, you see something similar to the following message:</span></span>

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

<span data-ttu-id="9d38d-143">在瀏覽器中瀏覽至 http://localhost:3000 。</span><span class="sxs-lookup"><span data-stu-id="9d38d-143">Navigate to http://localhost:3000 in a browser.</span></span> <span data-ttu-id="9d38d-144">按一下上層功能表中的 [註冊]，然後建立測試使用者。</span><span class="sxs-lookup"><span data-stu-id="9d38d-144">Click **Sign Up** in the top menu and create a test user.</span></span> 

<span data-ttu-id="9d38d-145">MEAN.js 範例應用程式會將使用者資料儲存於資料庫中。</span><span class="sxs-lookup"><span data-stu-id="9d38d-145">The MEAN.js sample application stores user data in the database.</span></span> <span data-ttu-id="9d38d-146">如果您成功建立使用者並且登入，則您的應用程式正在將資料寫入本機 MongoDB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="9d38d-146">If you are successful at creating a user and signing in, then your app is writing data to the local MongoDB database.</span></span>

![MEAN.js 成功連線至 MongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

<span data-ttu-id="9d38d-148">選取 [系統管理員] > [管理文章] 來新增一些文章。</span><span class="sxs-lookup"><span data-stu-id="9d38d-148">Select **Admin > Manage Articles** to add some articles.</span></span>

<span data-ttu-id="9d38d-149">如需隨時停止 Node.js，請在終端機上按下 `Ctrl+C`。</span><span class="sxs-lookup"><span data-stu-id="9d38d-149">To stop Node.js at any time, press `Ctrl+C` in the terminal.</span></span> 

## <a name="create-production-mongodb"></a><span data-ttu-id="9d38d-150">建立生產環境 MongoDB</span><span class="sxs-lookup"><span data-stu-id="9d38d-150">Create production MongoDB</span></span>

<span data-ttu-id="9d38d-151">在此步驟中，您要在 Azure 中建立 MongoDB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="9d38d-151">In this step, you create a MongoDB database in Azure.</span></span> <span data-ttu-id="9d38d-152">當您的應用程式部署至 Azure 時，它會使用此雲端資料庫。</span><span class="sxs-lookup"><span data-stu-id="9d38d-152">When your app is deployed to Azure, it uses this cloud database.</span></span>

<span data-ttu-id="9d38d-153">針對 MongoDB，本教學課程使用 [Azure Cosmos DB](/azure/documentdb/)。</span><span class="sxs-lookup"><span data-stu-id="9d38d-153">For MongoDB, this tutorial uses [Azure Cosmos DB](/azure/documentdb/).</span></span> <span data-ttu-id="9d38d-154">Cosmos DB 支援 MongoDB 用戶端連線。</span><span class="sxs-lookup"><span data-stu-id="9d38d-154">Cosmos DB supports MongoDB client connections.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="9d38d-155">登入 Azure</span><span class="sxs-lookup"><span data-stu-id="9d38d-155">Log in to Azure</span></span>

<span data-ttu-id="9d38d-156">您將使用 Azure CLI 2.0 在 Azure 中建立裝載應用程式所需的資源。</span><span class="sxs-lookup"><span data-stu-id="9d38d-156">You'll use the Azure CLI 2.0 to create the resources needed to host your app in Azure.</span></span> <span data-ttu-id="9d38d-157">使用 [az login](/cli/azure/#login) 命令登入 Azure 訂用帳戶並遵循畫面上的指示。</span><span class="sxs-lookup"><span data-stu-id="9d38d-157">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="9d38d-158">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="9d38d-158">Create a resource group</span></span>

<span data-ttu-id="9d38d-159">使用 [az group create](/cli/azure/group#create) 命令來建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="9d38d-159">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="9d38d-160">下列範例會在西歐區域中建立一個資源群組。</span><span class="sxs-lookup"><span data-stu-id="9d38d-160">The following example creates a resource group in the West Europe region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

<span data-ttu-id="9d38d-161">使用 [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI 命令以列出可用的位置。</span><span class="sxs-lookup"><span data-stu-id="9d38d-161">Use the [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command to list available locations.</span></span> 

### <a name="create-a-cosmos-db-account"></a><span data-ttu-id="9d38d-162">建立 Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="9d38d-162">Create a Cosmos DB account</span></span>

<span data-ttu-id="9d38d-163">使用 [az cosmosdb create](/cli/azure/cosmosdb#create) 命令來建立 Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9d38d-163">Create a Cosmos DB account with the [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="9d38d-164">在下列命令中，以唯一的 Cosmos DB 名稱取代 \<cosmosdb_name> 預留位置。</span><span class="sxs-lookup"><span data-stu-id="9d38d-164">In the following command, substitute a unique Cosmos DB name for the *\<cosmosdb_name>* placeholder.</span></span> <span data-ttu-id="9d38d-165">這個名稱會用來作為 Cosmos DB 端點 `https://<cosmosdb_name>.documents.azure.com/` 的一部分，因此，這個名稱在 Azure 中的所有 Cosmos DB 帳戶上必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="9d38d-165">This name is used as the part of the Cosmos DB endpoint, `https://<cosmosdb_name>.documents.azure.com/`, so the name needs to be unique across all Cosmos DB accounts in Azure.</span></span> <span data-ttu-id="9d38d-166">名稱只能包含小寫字母、數字及連字號 (-) 字元，且長度必須為 3 到 50 個字元。</span><span class="sxs-lookup"><span data-stu-id="9d38d-166">The name must contain only lowercase letters, numbers, and the hyphen (-) character, and must be between 3 and 50 characters long.</span></span>

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

<span data-ttu-id="9d38d-167">--kind MongoDB 參數會啟用 MongoDB 用戶端連線。</span><span class="sxs-lookup"><span data-stu-id="9d38d-167">The *--kind MongoDB* parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="9d38d-168">建立 Cosmos DB 帳戶之後，Azure CLI 會顯示類似下列範例的資訊：</span><span class="sxs-lookup"><span data-stu-id="9d38d-168">When the Cosmos DB account is created, the Azure CLI shows information similar to the following example:</span></span>

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

## <a name="connect-app-to-production-mongodb"></a><span data-ttu-id="9d38d-169">將應用程式連線至生產環境 MongoDB</span><span class="sxs-lookup"><span data-stu-id="9d38d-169">Connect app to production MongoDB</span></span>

<span data-ttu-id="9d38d-170">在此步驟中，您要使用 MongoDB 連接字串，將 MEAN.js 範例應用程式連線至您剛才建立的 Cosmos DB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="9d38d-170">In this step, you connect your MEAN.js sample application to the Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

### <a name="retrieve-the-database-key"></a><span data-ttu-id="9d38d-171">擷取資料庫索引鍵</span><span class="sxs-lookup"><span data-stu-id="9d38d-171">Retrieve the database key</span></span>

<span data-ttu-id="9d38d-172">若要連線至 Cosmos DB 資料庫，您需要資料庫金鑰。</span><span class="sxs-lookup"><span data-stu-id="9d38d-172">To connect to the Cosmos DB database, you need the database key.</span></span> <span data-ttu-id="9d38d-173">使用 [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) 命令來擷取主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="9d38d-173">Use the [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command to retrieve the primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

<span data-ttu-id="9d38d-174">Azure CLI 會顯示類似下列範例的資訊：</span><span class="sxs-lookup"><span data-stu-id="9d38d-174">The Azure CLI shows information similar to the following example:</span></span>

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

複製 `primaryMasterKey` 的值。 <span data-ttu-id="9d38d-176">您需要在下一個步驟中用到此資訊。</span><span class="sxs-lookup"><span data-stu-id="9d38d-176">You need this information in the next step.</span></span>

<a name="devconfig"></a>
### <a name="configure-the-connection-string-in-your-nodejs-application"></a><span data-ttu-id="9d38d-177">在 Node.js 應用程式中設定連接字串</span><span class="sxs-lookup"><span data-stu-id="9d38d-177">Configure the connection string in your Node.js application</span></span>

<span data-ttu-id="9d38d-178">在您的 MEAN.js 存放庫中，開啟 _config/env/production.js_。</span><span class="sxs-lookup"><span data-stu-id="9d38d-178">In your MEAN.js repository, open _config/env/production.js_.</span></span>

<span data-ttu-id="9d38d-179">在 `db` 物件中，更新 `uri` 的值：</span><span class="sxs-lookup"><span data-stu-id="9d38d-179">In the `db` object, update the value of `uri`:</span></span>

* <span data-ttu-id="9d38d-180">將兩個 \<cosmosdb_name> 預留位置取代為您的 Cosmos DB 資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="9d38d-180">Replace the two *\<cosmosdb_name>* placeholders with your Cosmos DB database name.</span></span>
* <span data-ttu-id="9d38d-181">將 \<primary_master_key> 預留位置取代為您在上一個步驟中複製的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="9d38d-181">Replace the *\<primary_master_key>* placeholder with the key you copied in the previous step.</span></span>

<span data-ttu-id="9d38d-182">下列程式碼顯示 `db` 物件：</span><span class="sxs-lookup"><span data-stu-id="9d38d-182">The following code shows the `db` object:</span></span>

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

<span data-ttu-id="9d38d-183">需要 `ssl=true` 選項，因為 [Cosmos DB 需要 SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements)。</span><span class="sxs-lookup"><span data-stu-id="9d38d-183">The `ssl=true` option is required because [Cosmos DB requires SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 

<span data-ttu-id="9d38d-184">儲存您的變更。</span><span class="sxs-lookup"><span data-stu-id="9d38d-184">Save your changes.</span></span>

### <a name="test-the-application-in-production-mode"></a><span data-ttu-id="9d38d-185">在生產模式中測試應用程式</span><span class="sxs-lookup"><span data-stu-id="9d38d-185">Test the application in production mode</span></span> 

<span data-ttu-id="9d38d-186">執行下列命令以縮短及組合生產環境的指令碼。</span><span class="sxs-lookup"><span data-stu-id="9d38d-186">Run the following command to minify and bundle scripts for the production environment.</span></span> <span data-ttu-id="9d38d-187">這個流程會產生生產環境所需的檔案。</span><span class="sxs-lookup"><span data-stu-id="9d38d-187">This process generates the files needed by the production environment.</span></span>

```bash
gulp prod
```

<span data-ttu-id="9d38d-188">執行下列命令以使用您在 _config/env/production.js_ 中設定的連接字串。</span><span class="sxs-lookup"><span data-stu-id="9d38d-188">Run the following command to use the connection string you configured in _config/env/production.js_.</span></span>

```bash
NODE_ENV=production node server.js
```

<span data-ttu-id="9d38d-189">`NODE_ENV=production` 會設定環境變數，告知 Node.js 在生產環境中執行。</span><span class="sxs-lookup"><span data-stu-id="9d38d-189">`NODE_ENV=production` sets the environment variable that tells Node.js to run in the production environment.</span></span>  <span data-ttu-id="9d38d-190">`node server.js` 會啟動存放庫根目錄中的 Node.js 伺服器與 `server.js`。</span><span class="sxs-lookup"><span data-stu-id="9d38d-190">`node server.js` starts the Node.js server with `server.js` in your repository root.</span></span> <span data-ttu-id="9d38d-191">這是在 Azure 中載入 Node.js 應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="9d38d-191">This is how your Node.js application is loaded in Azure.</span></span> 

<span data-ttu-id="9d38d-192">載入應用程式之後，請檢查以確定它正在生產環境中執行：</span><span class="sxs-lookup"><span data-stu-id="9d38d-192">When the app is loaded, check to make sure that it's running in the production environment:</span></span>

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

<span data-ttu-id="9d38d-193">在瀏覽器中瀏覽至 http://localhost:8443 。</span><span class="sxs-lookup"><span data-stu-id="9d38d-193">Navigate to http://localhost:8443 in a browser.</span></span> <span data-ttu-id="9d38d-194">按一下上層功能表中的 [註冊]，然後建立測試使用者。</span><span class="sxs-lookup"><span data-stu-id="9d38d-194">Click **Sign Up** in the top menu and create a test user.</span></span> <span data-ttu-id="9d38d-195">如果您成功建立使用者並且登入，則您的應用程式正在將資料寫入 Azure 中的 Cosmos DB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="9d38d-195">If you are successful creating a user and signing in, then your app is writing data to the Cosmos DB database in Azure.</span></span> 

<span data-ttu-id="9d38d-196">在終端機中，輸入 `Ctrl+C` 以停止 Node.js。</span><span class="sxs-lookup"><span data-stu-id="9d38d-196">In the terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

## <a name="deploy-app-to-azure"></a><span data-ttu-id="9d38d-197">將應用程式部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="9d38d-197">Deploy app to Azure</span></span>

<span data-ttu-id="9d38d-198">在此步驟中，您要將已與 MongoDB 連接的 Node.js 應用程式部署至 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="9d38d-198">In this step, you deploy your MongoDB-connected Node.js application to Azure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="9d38d-199">建立應用程式服務方案</span><span class="sxs-lookup"><span data-stu-id="9d38d-199">Create an App Service plan</span></span>

<span data-ttu-id="9d38d-200">使用 [az appservice plan create](/cli/azure/appservice/plan#create) 命令來建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="9d38d-200">Create an App Service plan with the [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="9d38d-201">下列範例會使用**免費**定價層，建立名為 _myAppServicePlan_ 的 App Service 方案：</span><span class="sxs-lookup"><span data-stu-id="9d38d-201">The following example creates an App Service plan named _myAppServicePlan_ using the **FREE** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="9d38d-202">建立 App Service 方案後，Azure CLI 會顯示類似下列範例的資訊：</span><span class="sxs-lookup"><span data-stu-id="9d38d-202">When the App Service plan is created, the Azure CLI shows information similar to the following example:</span></span>

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

### <a name="create-a-web-app"></a><span data-ttu-id="9d38d-203">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9d38d-203">Create a web app</span></span>

<span data-ttu-id="9d38d-204">使用 [az webapp create](/cli/azure/webapp#create) 命令，在 `myAppServicePlan` App Service 方案中建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d38d-204">Create a web app in the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="9d38d-205">Web 應用程式會為您提供裝載空間來部署程式碼，以及提供 URL 讓您能夠檢視已部署的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d38d-205">The web app gives you a hosting space to deploy your code and provides a URL for you to view the deployed application.</span></span> <span data-ttu-id="9d38d-206">用來建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d38d-206">Use  to create the web app.</span></span> 

<span data-ttu-id="9d38d-207">在下列命令中，將 \<app_name> 預留位置取代為唯一的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="9d38d-207">In the following command, replace the *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="9d38d-208">這個名稱是作為 Web 應用程式預設 URL 的一部分，因此，這個名稱在 Azure App Service 的所有應用程式中必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="9d38d-208">This name is used as the part of the default URL for the web app, so the name needs to be unique across all apps in Azure App Service.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="9d38d-209">建立 Web 應用程式後，Azure CLI 會顯示類似下列範例的資訊：</span><span class="sxs-lookup"><span data-stu-id="9d38d-209">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span> 

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

### <a name="configure-an-environment-variable"></a><span data-ttu-id="9d38d-210">設定環境變數</span><span class="sxs-lookup"><span data-stu-id="9d38d-210">Configure an environment variable</span></span>

<span data-ttu-id="9d38d-211">稍早在本教學課程中，您已將資料庫連接字串硬式編碼於 _config/env/production.js_ 中。</span><span class="sxs-lookup"><span data-stu-id="9d38d-211">Earlier in the tutorial, you hardcoded the database connection string in _config/env/production.js_.</span></span> <span data-ttu-id="9d38d-212">基於安全性最佳做法，您會想要將這些敏感性資料保存在您的 Git 存放庫以外的地方。</span><span class="sxs-lookup"><span data-stu-id="9d38d-212">In keeping with security best practice, you want to keep this sensitive data out of your Git repository.</span></span> <span data-ttu-id="9d38d-213">為了在 Azure 中執行應用程式，您將改用環境變數。</span><span class="sxs-lookup"><span data-stu-id="9d38d-213">For your app running in Azure, you'll use an environment variable instead.</span></span>

<span data-ttu-id="9d38d-214">在 App Service 中，您可以使用 [az webapp config appsettings update](/cli/azure/webapp/config/appsettings#update) 命令將環境變數設定為「應用程式設定」。</span><span class="sxs-lookup"><span data-stu-id="9d38d-214">In App Service, you set environment variables as _app settings_ by using the [az webapp config appsettings update](/cli/azure/webapp/config/appsettings#update) command.</span></span> 

<span data-ttu-id="9d38d-215">下列範例會在 Azure Web 應用程式中設定 `MONGODB_URI` 應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="9d38d-215">The following example configures a `MONGODB_URI` app setting in your Azure web app.</span></span> <span data-ttu-id="9d38d-216">取代 \<app_name>、\<cosmosdb_name> 和 \<primary_master_key> 預留位置。</span><span class="sxs-lookup"><span data-stu-id="9d38d-216">Replace the *\<app_name>*, *\<cosmosdb_name>*, and *\<primary_master_key>* placeholders.</span></span>

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

<span data-ttu-id="9d38d-217">在 Node.js 程式碼中，您可以利用 `process.env.MONGODB_URI` 來存取此應用程式設定，就像存取任何環境變數一樣。</span><span class="sxs-lookup"><span data-stu-id="9d38d-217">In Node.js code, you access this app setting with `process.env.MONGODB_URI`, just like you would access any environment variable.</span></span> 

<span data-ttu-id="9d38d-218">現在，使用下列命令，將您的變更復原為 _config/env/production.js_：</span><span class="sxs-lookup"><span data-stu-id="9d38d-218">Now, undo your changes to _config/env/production.js_ with the following command:</span></span>

```bash
git checkout -- .
```

<span data-ttu-id="9d38d-219">再次開啟 _config/env/production.js_。</span><span class="sxs-lookup"><span data-stu-id="9d38d-219">Open _config/env/production.js_ again.</span></span> <span data-ttu-id="9d38d-220">請注意，已經將預設的 MEAN.js 應用程式設定為使用您建立的 `MONGODB_URI` 環境變數。</span><span class="sxs-lookup"><span data-stu-id="9d38d-220">Note that the default MEAN.js app is already configured to use the `MONGODB_URI` environment variable that you created.</span></span>

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a><span data-ttu-id="9d38d-221">設定本機 git 部署</span><span class="sxs-lookup"><span data-stu-id="9d38d-221">Configure local git deployment</span></span> 

<span data-ttu-id="9d38d-222">使用 [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) 命令來建立部署的認證。</span><span class="sxs-lookup"><span data-stu-id="9d38d-222">Use the [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command to create credentials for deployment.</span></span>

<span data-ttu-id="9d38d-223">您可以使用各種方式來將應用程式部署至 Azure App Service，包括 FTP、本機 Git、GitHub、Visual Studio Team Services 和 BitBucket。</span><span class="sxs-lookup"><span data-stu-id="9d38d-223">You can deploy your application to Azure App Service in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="9d38d-224">對於 FTP 和本機 Git，必須在伺服器上設定部署使用者，才能驗證您的部署。</span><span class="sxs-lookup"><span data-stu-id="9d38d-224">For FTP and local Git, it is necessary to have a deployment user configured on the server to authenticate your deployment.</span></span> <span data-ttu-id="9d38d-225">此部署使用者是帳戶層級，與 Azure 訂用帳戶的帳戶不同。</span><span class="sxs-lookup"><span data-stu-id="9d38d-225">This deployment user is account-level and is different from your Azure subscription account.</span></span> <span data-ttu-id="9d38d-226">您只需設定此部署使用者一次。</span><span class="sxs-lookup"><span data-stu-id="9d38d-226">You only need to configure this deployment user once.</span></span>

<span data-ttu-id="9d38d-227">在下列命令中，將 *\<user-name>* 和 *\<password>* 取代為新的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="9d38d-227">In the following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="9d38d-228">使用者名稱必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="9d38d-228">The user name must be unique.</span></span> <span data-ttu-id="9d38d-229">密碼長度必須至少為 8 個字元，包含下列三個元素其中兩個：字母、數字、符號。</span><span class="sxs-lookup"><span data-stu-id="9d38d-229">The password must be at least eight characters long, with two of the following three elements:  letters, numbers, symbols.</span></span> <span data-ttu-id="9d38d-230">如果您收到 ` 'Conflict'. Details: 409` 錯誤，請變更使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="9d38d-230">If you get a ` 'Conflict'. Details: 409` error, change the username.</span></span> <span data-ttu-id="9d38d-231">如果您收到 ` 'Bad Request'. Details: 400` 錯誤，請使用更強的密碼。</span><span class="sxs-lookup"><span data-stu-id="9d38d-231">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="9d38d-232">記下使用者名稱和密碼，以在您部署應用程式的稍後步驟中使用。</span><span class="sxs-lookup"><span data-stu-id="9d38d-232">Record the user name and password for use in later steps when you deploy the app.</span></span>

<span data-ttu-id="9d38d-233">使用 [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) 命令，來設定 Azure Web 應用程式的本機 Git 存取。</span><span class="sxs-lookup"><span data-stu-id="9d38d-233">Use the [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command to configure local Git access to the Azure web app.</span></span> 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

<span data-ttu-id="9d38d-234">設定部署使用者時，Azure CLI 會以下列格式顯示 Azure Web 應用程式的部署 URL：</span><span class="sxs-lookup"><span data-stu-id="9d38d-234">When the deployment user is configured, the Azure CLI shows the deployment URL for your Azure web app in the following format:</span></span>

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

<span data-ttu-id="9d38d-235">複製終端機的輸出，因為下一個步驟中會使用此資訊。</span><span class="sxs-lookup"><span data-stu-id="9d38d-235">Copy the output from the terminal, as it will be used in the next step.</span></span> 

### <a name="push-to-azure-from-git"></a><span data-ttu-id="9d38d-236">從 Git 推送至 Azure</span><span class="sxs-lookup"><span data-stu-id="9d38d-236">Push to Azure from Git</span></span>

<span data-ttu-id="9d38d-237">將 Azure 遠端新增至本機 Git 存放庫。</span><span class="sxs-lookup"><span data-stu-id="9d38d-237">Add an Azure remote to your local Git repository.</span></span> 

```bash
git remote add azure <paste_copied_url_here> 
```

<span data-ttu-id="9d38d-238">推送至 Azure 遠端，以部署您的 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d38d-238">Push to the Azure remote to deploy your Node.js application.</span></span> <span data-ttu-id="9d38d-239">建立部署使用者時，系統會提示您輸入稍早提供的密碼。</span><span class="sxs-lookup"><span data-stu-id="9d38d-239">You will be prompted for the password you supplied earlier as part of the creation of the deployment user.</span></span> 

```bash
git push azure master
```

<span data-ttu-id="9d38d-240">在部署期間，Azure App Service 會與 Git 溝通其進度。</span><span class="sxs-lookup"><span data-stu-id="9d38d-240">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 5, done.
Delta compression using up to 4 threads.
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
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

<span data-ttu-id="9d38d-241">您可能會注意到，部署程序會在 `npm install` 之後執行 [Gulp](http://gulpjs.com/)。</span><span class="sxs-lookup"><span data-stu-id="9d38d-241">You may notice that the deployment process runs [Gulp](http://gulpjs.com/) after `npm install`.</span></span> <span data-ttu-id="9d38d-242">App Service 不會在部署期間執行 Gulp 或 Grunt 工作，因此，這個範例存放庫在其根目錄中有兩個其他檔案可啟用它：</span><span class="sxs-lookup"><span data-stu-id="9d38d-242">App Service does not run Gulp or Grunt tasks during deployment, so this sample repository has two additional files in its root directory to enable it:</span></span> 

- <span data-ttu-id="9d38d-243">_.deployment_ - 此檔案會告訴 App Service，執行 `bash deploy.sh` 以作為自訂部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="9d38d-243">_.deployment_ - This file tells App Service to run `bash deploy.sh` as the custom deployment script.</span></span>
- <span data-ttu-id="9d38d-244">_deploy.sh_ - 自訂部署指令碼。</span><span class="sxs-lookup"><span data-stu-id="9d38d-244">_deploy.sh_ - The custom deployment script.</span></span> <span data-ttu-id="9d38d-245">如果您檢閱檔案，您將看到它會在 `npm install` 和 `bower install` 之後執行 `gulp prod`。</span><span class="sxs-lookup"><span data-stu-id="9d38d-245">If you review the file, you will see that it runs `gulp prod` after `npm install` and `bower install`.</span></span> 

<span data-ttu-id="9d38d-246">您可以使用這種方法，將任何步驟新增至您的 Git 部署。</span><span class="sxs-lookup"><span data-stu-id="9d38d-246">You can use this approach to add any step to your Git-based deployment.</span></span> <span data-ttu-id="9d38d-247">如果您在任一時間點重新啟動 Azure Web 應用程式，App Service 並不會重新執行這些自動化工作。</span><span class="sxs-lookup"><span data-stu-id="9d38d-247">If you restart your Azure web app at any point, App Service doesn't rerun these automation tasks.</span></span>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="9d38d-248">瀏覽至 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9d38d-248">Browse to the Azure web app</span></span> 

<span data-ttu-id="9d38d-249">使用 Web 瀏覽器，瀏覽至已部署的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d38d-249">Browse to the deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
``` 

<span data-ttu-id="9d38d-250">按一下上層功能表中的 [註冊]，然後建立一位虛擬使用者。</span><span class="sxs-lookup"><span data-stu-id="9d38d-250">Click **Sign Up** in the top menu and create a dummy user.</span></span> 

<span data-ttu-id="9d38d-251">如果成功且應用程式會自動登入已建立的使用者，則您在 Azure 中的 MEAN.js 應用程式就已連線到 MongoDB (Cosmos DB) 資料庫。</span><span class="sxs-lookup"><span data-stu-id="9d38d-251">If you are successful and the app automatically signs in to the created user, then your MEAN.js app in Azure has connectivity to the MongoDB (Cosmos DB) database.</span></span> 

![在 Azure App Service 中執行的 MEAN.js 應用程式](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="9d38d-253">選取 [系統管理員] > [管理文章] 來新增一些文章。</span><span class="sxs-lookup"><span data-stu-id="9d38d-253">Select **Admin > Manage Articles** to add some articles.</span></span> 

<span data-ttu-id="9d38d-254">**恭喜！**</span><span class="sxs-lookup"><span data-stu-id="9d38d-254">**Congratulations!**</span></span> <span data-ttu-id="9d38d-255">您正在 Azure App Service 中執行資料驅動的 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d38d-255">You're running a data-driven Node.js app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="9d38d-256">更新資料模型並重新部署</span><span class="sxs-lookup"><span data-stu-id="9d38d-256">Update data model and redeploy</span></span>

<span data-ttu-id="9d38d-257">在此步驟中，您會變更 `article` 資料模型，並將變更發佈至 Azure。</span><span class="sxs-lookup"><span data-stu-id="9d38d-257">In this step, you change the `article` data model and publish your change to Azure.</span></span>

### <a name="update-the-data-model"></a><span data-ttu-id="9d38d-258">更新資料模型</span><span class="sxs-lookup"><span data-stu-id="9d38d-258">Update the data model</span></span>

<span data-ttu-id="9d38d-259">開啟 _modules/articles/server/models/article.server.model.js_。</span><span class="sxs-lookup"><span data-stu-id="9d38d-259">Open _modules/articles/server/models/article.server.model.js_.</span></span>

<span data-ttu-id="9d38d-260">在 `ArticleSchema` 中，新增名為 `comment` 的 `String` 類型。</span><span class="sxs-lookup"><span data-stu-id="9d38d-260">In `ArticleSchema`, add a `String` type called `comment`.</span></span> <span data-ttu-id="9d38d-261">完成時，您的結構描述程式碼應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="9d38d-261">When you're done, your schema code should look like this:</span></span>

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

### <a name="update-the-articles-code"></a><span data-ttu-id="9d38d-262">更新 articles 程式碼</span><span class="sxs-lookup"><span data-stu-id="9d38d-262">Update the articles code</span></span>

<span data-ttu-id="9d38d-263">更新 `articles` 程式碼的其餘部分以使用 `comment`。</span><span class="sxs-lookup"><span data-stu-id="9d38d-263">Update the rest of your `articles` code to use `comment`.</span></span>

<span data-ttu-id="9d38d-264">有五個需要修改的檔案：伺服器控制器和四個用戶端檢視。</span><span class="sxs-lookup"><span data-stu-id="9d38d-264">There are five files you need to modify: the server controller and the four client views.</span></span> 

<span data-ttu-id="9d38d-265">開啟 _modules/articles/server/controllers/articles.server.controller.js_。</span><span class="sxs-lookup"><span data-stu-id="9d38d-265">Open _modules/articles/server/controllers/articles.server.controller.js_.</span></span>

<span data-ttu-id="9d38d-266">在 `update` 函式中，新增 `article.comment` 的指派。</span><span class="sxs-lookup"><span data-stu-id="9d38d-266">In the `update` function, add an assignment for `article.comment`.</span></span> <span data-ttu-id="9d38d-267">下列程式碼會顯示已完成的 `update` 函式：</span><span class="sxs-lookup"><span data-stu-id="9d38d-267">The following code shows the completed `update` function:</span></span>

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

<span data-ttu-id="9d38d-268">開啟 _modules/articles/client/views/view-article.client.view.html_。</span><span class="sxs-lookup"><span data-stu-id="9d38d-268">Open _modules/articles/client/views/view-article.client.view.html_.</span></span>

<span data-ttu-id="9d38d-269">就在結尾 `</section>` 標記的正上方，新增下列程式碼行來顯示 `comment` 以及剩餘的文章資料：</span><span class="sxs-lookup"><span data-stu-id="9d38d-269">Just above the closing `</section>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

<span data-ttu-id="9d38d-270">開啟 _modules/articles/client/views/list-articles.client.view.html_。</span><span class="sxs-lookup"><span data-stu-id="9d38d-270">Open _modules/articles/client/views/list-articles.client.view.html_.</span></span>

<span data-ttu-id="9d38d-271">就在結尾 `</a>` 標記的正上方，新增下列程式碼行來顯示 `comment` 以及剩餘的文章資料：</span><span class="sxs-lookup"><span data-stu-id="9d38d-271">Just above the closing `</a>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

<span data-ttu-id="9d38d-272">開啟 _modules/articles/client/views/admin/list-articles.client.view.html_。</span><span class="sxs-lookup"><span data-stu-id="9d38d-272">Open _modules/articles/client/views/admin/list-articles.client.view.html_.</span></span>

<span data-ttu-id="9d38d-273">在 `<div class="list-group">` 元素內部且就在結尾 `comment` 標記的正上方，新增下列程式碼行來顯示 `</a>` 以及剩餘的文章資料：</span><span class="sxs-lookup"><span data-stu-id="9d38d-273">Inside the `<div class="list-group">` element and just above the closing `</a>` tag, add the following line to display `comment` along with the rest of the article data:</span></span>

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

<span data-ttu-id="9d38d-274">開啟 _modules/articles/client/views/admin/form-article.client.view.html_。</span><span class="sxs-lookup"><span data-stu-id="9d38d-274">Open _modules/articles/client/views/admin/form-article.client.view.html_.</span></span>

<span data-ttu-id="9d38d-275">找到包含提交按鈕的 `<div class="form-group">` 元素，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9d38d-275">Find the `<div class="form-group">` element that contains the submit button, which looks like this:</span></span>

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

<span data-ttu-id="9d38d-276">就在此標記的正上方，新增另一個 `<div class="form-group">` 元素，讓使用者能夠編輯 `comment` 欄位。</span><span class="sxs-lookup"><span data-stu-id="9d38d-276">Just above this tag, add another `<div class="form-group">` element that lets people edit the `comment` field.</span></span> <span data-ttu-id="9d38d-277">新的元素應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="9d38d-277">Your new element should look like this:</span></span>

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="9d38d-278">本機測試您的變更</span><span class="sxs-lookup"><span data-stu-id="9d38d-278">Test your changes locally</span></span>

<span data-ttu-id="9d38d-279">儲存您的所有變更。</span><span class="sxs-lookup"><span data-stu-id="9d38d-279">Save all your changes.</span></span>

<span data-ttu-id="9d38d-280">再次在生產模式中測試您的變更。</span><span class="sxs-lookup"><span data-stu-id="9d38d-280">Test your changes in production mode again.</span></span>

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> <span data-ttu-id="9d38d-281">請記住，您的 _config/env/production.js_ 已還原，`MONGODB_URI` 環境變數只會設定於 Azure Web 應用程式中，而不會設定於本機電腦上。</span><span class="sxs-lookup"><span data-stu-id="9d38d-281">Remember that your _config/env/production.js_ has been reverted, and the `MONGODB_URI` environment variable is only set in your Azure web app and not on your local machine.</span></span> <span data-ttu-id="9d38d-282">如果您查看設定檔，就會發現生產設定預設為使用本機的 MongoDB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="9d38d-282">If you look at the config file, you find that the production configuration defaults to use a local MongoDB database.</span></span> <span data-ttu-id="9d38d-283">如此可確保當您在本機測試程式碼變更時，不會碰觸到生產資料。</span><span class="sxs-lookup"><span data-stu-id="9d38d-283">This makes sure that you don't touch production data when you test your code changes locally.</span></span>

<span data-ttu-id="9d38d-284">在瀏覽器中，瀏覽至 `http://localhost:8443`，並確定您已登入。</span><span class="sxs-lookup"><span data-stu-id="9d38d-284">Navigate to `http://localhost:8443` in a browser and make sure that you're signed in.</span></span>

<span data-ttu-id="9d38d-285">選取 [系統管理員] > [管理文章]，然後選取 [+] 按鈕來新增文章。</span><span class="sxs-lookup"><span data-stu-id="9d38d-285">Select **Admin > Manage Articles**, then add an article by selecting the **+** button.</span></span>

<span data-ttu-id="9d38d-286">您現在會看到新的 `Comment` 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="9d38d-286">You see the new `Comment` textbox now.</span></span>

![已將註解欄位新增到文章中](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

<span data-ttu-id="9d38d-288">在終端機中，輸入 `Ctrl+C` 以停止 Node.js。</span><span class="sxs-lookup"><span data-stu-id="9d38d-288">In the terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

### <a name="publish-changes-to-azure"></a><span data-ttu-id="9d38d-289">將變更發佈至 Azure</span><span class="sxs-lookup"><span data-stu-id="9d38d-289">Publish changes to Azure</span></span>

<span data-ttu-id="9d38d-290">在 Git 中認可您的變更，然後將程式碼變更推送至 Azure。</span><span class="sxs-lookup"><span data-stu-id="9d38d-290">Commit your changes in Git, then push the code changes to Azure.</span></span>

```bash
git commit -am "added article comment"
git push azure master
```

<span data-ttu-id="9d38d-291">完成 `git push` 之後，瀏覽至 Azure Web 應用程式，然後嘗試執行新功能。</span><span class="sxs-lookup"><span data-stu-id="9d38d-291">Once the `git push` is complete, navigate to your Azure web app and try out the new functionality.</span></span>

![發佈至 Azure 的模型和資料庫變更](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

<span data-ttu-id="9d38d-293">如果您先前已新增任何文章，您仍然可以看到它們。</span><span class="sxs-lookup"><span data-stu-id="9d38d-293">If you added any articles earlier, you still can see them.</span></span> <span data-ttu-id="9d38d-294">Cosmos DB 中的現有資料不會遺失。</span><span class="sxs-lookup"><span data-stu-id="9d38d-294">Existing data in your Cosmos DB is not lost.</span></span> <span data-ttu-id="9d38d-295">此外，您的變更會更新至資料結構描述，並讓現有資料保留不變。</span><span class="sxs-lookup"><span data-stu-id="9d38d-295">Also, your updates to the data schema and leaves your existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="9d38d-296">資料流診斷記錄</span><span class="sxs-lookup"><span data-stu-id="9d38d-296">Stream diagnostic logs</span></span> 

<span data-ttu-id="9d38d-297">當 Node.js 應用程式在 Azure App Service 中執行時，您可以使用管線將主控台記錄傳送至終端機。</span><span class="sxs-lookup"><span data-stu-id="9d38d-297">While your Node.js application runs in Azure App Service, you can get the console logs piped to your terminal.</span></span> <span data-ttu-id="9d38d-298">這樣一來，您就能取得相同的診斷訊息，以協助您偵錯應用程式錯誤。</span><span class="sxs-lookup"><span data-stu-id="9d38d-298">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="9d38d-299">請使用 [az webapp log tail](/cli/azure/webapp/log#tail) 命令開始記錄資料流。</span><span class="sxs-lookup"><span data-stu-id="9d38d-299">To start log streaming, use the [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

<span data-ttu-id="9d38d-300">開始記錄資料流之後，重新整理瀏覽器中的 Azure Web 應用程式，以取得部分 Web 流量。</span><span class="sxs-lookup"><span data-stu-id="9d38d-300">Once log streaming has started, refresh your Azure web app in the browser to get some web traffic.</span></span> <span data-ttu-id="9d38d-301">您現在會看到使用管線傳送到終端機的主控台記錄。</span><span class="sxs-lookup"><span data-stu-id="9d38d-301">You now see console logs piped to your terminal.</span></span>

<span data-ttu-id="9d38d-302">您隨時可以輸入 `Ctrl+C` 以停止記錄資料流。</span><span class="sxs-lookup"><span data-stu-id="9d38d-302">Stop log streaming at any time by typing `Ctrl+C`.</span></span> 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="9d38d-303">管理您的 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="9d38d-303">Manage your Azure web app</span></span>

<span data-ttu-id="9d38d-304">請移至 [Azure 入口網站](https://portal.azure.com)，以查看您所建立的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d38d-304">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span>

<span data-ttu-id="9d38d-305">按一下左側功能表中的 [應用程式服務]，然後按一下 Azure Web 應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="9d38d-305">From the left menu, click **App Services**, then click the name of your Azure web app.</span></span>

![入口網站瀏覽至 Azure Web 應用程式](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

<span data-ttu-id="9d38d-307">根據預設，入口網站會顯示 Web 應用程式的 [概觀] 分頁。</span><span class="sxs-lookup"><span data-stu-id="9d38d-307">By default, the portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="9d38d-308">此頁面可讓您檢視應用程式的執行方式。</span><span class="sxs-lookup"><span data-stu-id="9d38d-308">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="9d38d-309">您也可以在這裡執行基本管理工作，像是瀏覽、停止、啟動、重新啟動及刪除。</span><span class="sxs-lookup"><span data-stu-id="9d38d-309">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="9d38d-310">分頁左側的索引標籤會顯示您可開啟的各種設定分頁。</span><span class="sxs-lookup"><span data-stu-id="9d38d-310">The tabs on the left side of the page show the different configuration pages you can open.</span></span>

![Azure 入口網站中的 App Service 頁面](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a><span data-ttu-id="9d38d-312">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9d38d-312">Next steps</span></span>

<span data-ttu-id="9d38d-313">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="9d38d-313">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9d38d-314">在 Azure 中建立 MongoDB 資料庫</span><span class="sxs-lookup"><span data-stu-id="9d38d-314">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="9d38d-315">將 Node.js 應用程式連線至 MongoDB</span><span class="sxs-lookup"><span data-stu-id="9d38d-315">Connect a Node.js app to MongoDB</span></span>
> * <span data-ttu-id="9d38d-316">將應用程式部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="9d38d-316">Deploy the app to Azure</span></span>
> * <span data-ttu-id="9d38d-317">將資料模型更新並將應用程式重新部署</span><span class="sxs-lookup"><span data-stu-id="9d38d-317">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="9d38d-318">將記錄從 Azure 串流到終端機</span><span class="sxs-lookup"><span data-stu-id="9d38d-318">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="9d38d-319">在 Azure 入口網站中管理應用程式</span><span class="sxs-lookup"><span data-stu-id="9d38d-319">Manage the app in the Azure portal</span></span>

<span data-ttu-id="9d38d-320">前往下一個教學課程，了解如何將自訂的 DNS 名稱對應至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9d38d-320">Advance to the next tutorial to learn how to map a custom DNS name to your web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="9d38d-321">將現有的自訂 DNS 名稱對應至 Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="9d38d-321">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
