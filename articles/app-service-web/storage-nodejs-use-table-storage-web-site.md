---
title: "使用 Azure 表格服務的 Node.js Web 應用程式"
description: "本教學課程說明如何使用 Azure 表格服務，儲存 Azure App Service Web Apps 代管的 Node.js 應用程式資料。"
tags: azure-portal
services: app-service\web, storage
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 029e6f46-f586-4309-adbf-71c7b8d537d4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 3252914934c1084a165fa39ee983d3039e04d567
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="nodejs-web-app-using-the-azure-table-service"></a><span data-ttu-id="8df1f-103">使用 Azure 表格服務的 Node.js Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="8df1f-103">Node.js web app using the Azure Table Service</span></span>
## <a name="overview"></a><span data-ttu-id="8df1f-104">Overview</span><span class="sxs-lookup"><span data-stu-id="8df1f-104">Overview</span></span>
<span data-ttu-id="8df1f-105">本教學課程說明如何使用 Azure 資料管理所提供的表格服務，儲存及存取 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps 代管的 [node] 應用程式資料。</span><span class="sxs-lookup"><span data-stu-id="8df1f-105">This tutorial shows you how to use Table service provided by Azure Data Management to store and access data from a [node] application hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="8df1f-106">本教學課程假設您先前有過一些使用節點及 [Git]的經驗。</span><span class="sxs-lookup"><span data-stu-id="8df1f-106">This tutorial assumes that you have some prior experience using node and [Git].</span></span>

<span data-ttu-id="8df1f-107">您將了解：</span><span class="sxs-lookup"><span data-stu-id="8df1f-107">You will learn:</span></span>

* <span data-ttu-id="8df1f-108">如何使用 npm (節點封裝管理員) 來安裝節點模組</span><span class="sxs-lookup"><span data-stu-id="8df1f-108">How to use npm (node package manager) to install the node modules</span></span>
* <span data-ttu-id="8df1f-109">如何使用 Azure 表格服務</span><span class="sxs-lookup"><span data-stu-id="8df1f-109">How to work with the Azure Table service</span></span>
* <span data-ttu-id="8df1f-110">如何使用 Azure CLI 建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8df1f-110">How to use the Azure CLI to create a web app.</span></span>

<span data-ttu-id="8df1f-111">依照本教學課程的指示，您將組建一個簡單的網頁型「待辦事項清單」應用程式，用於建立、擷取、完成工作。</span><span class="sxs-lookup"><span data-stu-id="8df1f-111">By following this tutorial, you will build a simple web-based "to-do list" application that allows creating, retrieving and completing tasks.</span></span> <span data-ttu-id="8df1f-112">工作存放於資料表服務中。</span><span class="sxs-lookup"><span data-stu-id="8df1f-112">The tasks are stored in the Table service.</span></span>

<span data-ttu-id="8df1f-113">以下是完成的應用程式：</span><span class="sxs-lookup"><span data-stu-id="8df1f-113">Here is the completed application:</span></span>

![顯示空白工作清單的網頁][node-table-finished]

> [!NOTE]
> <span data-ttu-id="8df1f-115">如果您想在註冊 Azure 帳戶前開始使用 Azure App Service，請移至 [試用 App Service](https://azure.microsoft.com/try/app-service/)，即可在 App Service 中立即建立短期入門 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8df1f-115">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="8df1f-116">不需要信用卡；無需承諾。</span><span class="sxs-lookup"><span data-stu-id="8df1f-116">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="8df1f-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="8df1f-117">Prerequisites</span></span>
<span data-ttu-id="8df1f-118">在依照本文中的指示進行之前，請確定已安裝下列項目：</span><span class="sxs-lookup"><span data-stu-id="8df1f-118">Before following the instructions in this article, ensure that you have the following installed:</span></span>

* <span data-ttu-id="8df1f-119">[node] 版本 0.10.24 或更高版本</span><span class="sxs-lookup"><span data-stu-id="8df1f-119">[node] version 0.10.24 or higher</span></span>
* <span data-ttu-id="8df1f-120">[Git]</span><span class="sxs-lookup"><span data-stu-id="8df1f-120">[Git]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a><span data-ttu-id="8df1f-121">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="8df1f-121">Create a storage account</span></span>
<span data-ttu-id="8df1f-122">建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8df1f-122">Create an Azure storage account.</span></span> <span data-ttu-id="8df1f-123">應用程式會使用此帳戶來儲存待辦事項。</span><span class="sxs-lookup"><span data-stu-id="8df1f-123">The app will use this account to store the to-do items.</span></span>

1. <span data-ttu-id="8df1f-124">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="8df1f-124">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8df1f-125">按一下入口網站左下方的 [新增] 圖示，然後按一下 [資料 + 儲存體]  >  [儲存體]。</span><span class="sxs-lookup"><span data-stu-id="8df1f-125">Click the **New** icon on the bottom left of the portal, then click **Data + Storage** > **Storage**.</span></span> <span data-ttu-id="8df1f-126">為儲存體帳戶指定唯一名稱，並為它建立新的[資源群組](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="8df1f-126">Give the storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![新增按鈕](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    <span data-ttu-id="8df1f-128">建立儲存體帳戶後，[通知] 按鈕便會閃爍綠色 [成功]，儲存體帳戶的刀鋒視窗會開啟，顯示它屬於您所建立的新資源群組。</span><span class="sxs-lookup"><span data-stu-id="8df1f-128">When the storage account has been created, the **Notifications** button will flash a green **SUCCESS** and the storage account's blade is open to show that it belongs to the new resource group you created.</span></span>
3. <span data-ttu-id="8df1f-129">在儲存體帳戶的刀鋒視窗中，按一下 [設定]  >  [金鑰]。</span><span class="sxs-lookup"><span data-stu-id="8df1f-129">In the storage account's blade, click **Settings** > **Keys**.</span></span> <span data-ttu-id="8df1f-130">將主要存取金鑰複製到剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="8df1f-130">Copy the primary access key to the clipboard.</span></span>
   
    ![存取金鑰][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a><span data-ttu-id="8df1f-132">安裝模組及產生樣板</span><span class="sxs-lookup"><span data-stu-id="8df1f-132">Install modules and generate scaffolding</span></span>
<span data-ttu-id="8df1f-133">在本節中，您將建立新的 Node 應用程式，並使用 npm 來新增模組封裝。</span><span class="sxs-lookup"><span data-stu-id="8df1f-133">In this section you will create a new Node application and use npm to add module packages.</span></span> <span data-ttu-id="8df1f-134">針對此應用程式，您將使用 [Express] 和 [Azure] 模組。</span><span class="sxs-lookup"><span data-stu-id="8df1f-134">For this application you will use the [Express] and [Azure] modules.</span></span> <span data-ttu-id="8df1f-135">Express 模組提供節點的模型檢視控制器架構，Azure 模組則提供資料表服務的連線。</span><span class="sxs-lookup"><span data-stu-id="8df1f-135">The Express module provides a Model View Controller framework for node, while the Azure modules provides connectivity to the Table service.</span></span>

### <a name="install-express-and-generate-scaffolding"></a><span data-ttu-id="8df1f-136">安裝 Express 及產生樣板</span><span class="sxs-lookup"><span data-stu-id="8df1f-136">Install express and generate scaffolding</span></span>
1. <span data-ttu-id="8df1f-137">從命令列中，建立名為 **tasklist** 的新目錄，並切換至該目錄。</span><span class="sxs-lookup"><span data-stu-id="8df1f-137">From the command line, create a new directory named **tasklist** and switch to that directory.</span></span>  
2. <span data-ttu-id="8df1f-138">輸入下列命令以安裝 Express 模組。</span><span class="sxs-lookup"><span data-stu-id="8df1f-138">Enter the following command to install the Express module.</span></span>
   
        npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="8df1f-139">視作業系統而定，您可能需要在命令之前加上 'sudo'：</span><span class="sxs-lookup"><span data-stu-id="8df1f-139">Depending on the operating system, you may need to put 'sudo' before the command:</span></span>
   
        sudo npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="8df1f-140">此輸出看起來類似下列範例：</span><span class="sxs-lookup"><span data-stu-id="8df1f-140">The output appears similar to the following example:</span></span>
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > <span data-ttu-id="8df1f-141">'-g' 參數會全域安裝模組。</span><span class="sxs-lookup"><span data-stu-id="8df1f-141">The '-g' parameter installs the module globally.</span></span> <span data-ttu-id="8df1f-142">這樣我們就可以使用 **express** 來產生 Web 應用程式樣板，而不需額外輸入路徑資訊。</span><span class="sxs-lookup"><span data-stu-id="8df1f-142">That way, we can use **express** to generate web app scaffolding without having to type in additional path information.</span></span>
   > 
   > 
3. <span data-ttu-id="8df1f-143">若要建立應用程式的樣板，請輸入 **express** 命令：</span><span class="sxs-lookup"><span data-stu-id="8df1f-143">To create the scaffolding for the application, enter the **express** command:</span></span>
   
        express
   
    <span data-ttu-id="8df1f-144">這個命令的輸出看起來類似下列範例：</span><span class="sxs-lookup"><span data-stu-id="8df1f-144">The output of this command appears similar to the following example:</span></span>
   
           create : .
           create : ./package.json
           create : ./app.js
           create : ./public
           create : ./public/images
           create : ./routes
           create : ./routes/index.js
           create : ./routes/users.js
           create : ./public/stylesheets
           create : ./public/stylesheets/style.css
           create : ./views
           create : ./views/index.jade
           create : ./views/layout.jade
           create : ./views/error.jade
           create : ./public/javascripts
           create : ./bin
           create : ./bin/www
   
           install dependencies:
             $ cd . && npm install
   
           run the app:
             $ DEBUG=my-application ./bin/www
   
    <span data-ttu-id="8df1f-145">您現在於 **tasklist** 目錄中有幾個新的目錄和檔案。</span><span class="sxs-lookup"><span data-stu-id="8df1f-145">You now have several new directories and files in the **tasklist** directory.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="8df1f-146">安裝其他模組</span><span class="sxs-lookup"><span data-stu-id="8df1f-146">Install additional modules</span></span>
<span data-ttu-id="8df1f-147">**express** 建立的其中一個檔案是 **package.json**。</span><span class="sxs-lookup"><span data-stu-id="8df1f-147">One of the files that **express** creates is **package.json**.</span></span> <span data-ttu-id="8df1f-148">此檔案包含模組相依性清單。</span><span class="sxs-lookup"><span data-stu-id="8df1f-148">This file contains a list of module dependencies.</span></span> <span data-ttu-id="8df1f-149">之後，當您將應用程式部署至 App Service Web Apps 時，此檔案將決定 Azure 上需要安裝哪些模組。</span><span class="sxs-lookup"><span data-stu-id="8df1f-149">Later, when you deploy the application to App Service Web Apps, this file determines which modules need to be installed on Azure.</span></span>

<span data-ttu-id="8df1f-150">從命令列中，輸入下列命令安裝 **package.json** 檔案中所指出的模組。</span><span class="sxs-lookup"><span data-stu-id="8df1f-150">From the command-line, enter the following command to install the modules described in the **package.json** file.</span></span> <span data-ttu-id="8df1f-151">您可能需要使用 'sudo'。</span><span class="sxs-lookup"><span data-stu-id="8df1f-151">You may need to use 'sudo'.</span></span>

    npm install

<span data-ttu-id="8df1f-152">這個命令的輸出看起來類似下列範例：</span><span class="sxs-lookup"><span data-stu-id="8df1f-152">The output of this command appears similar to the following example:</span></span>

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


<span data-ttu-id="8df1f-153">接著，輸入下列命令安裝 [azure]、[node-uuid]、[nconf] 和 [async] 模組：</span><span class="sxs-lookup"><span data-stu-id="8df1f-153">Next, enter the following command to install the [azure], [node-uuid], [nconf] and [async] modules:</span></span>

    npm install azure-storage node-uuid async nconf --save

<span data-ttu-id="8df1f-154">**--save** 旗標會將這些模組的項目新增至 **package.json** 檔案。</span><span class="sxs-lookup"><span data-stu-id="8df1f-154">The **--save** flag adds entries for these modules to the **package.json** file.</span></span>

<span data-ttu-id="8df1f-155">這個命令的輸出看起來類似下列範例：</span><span class="sxs-lookup"><span data-stu-id="8df1f-155">The output of this command appears similar to the following example:</span></span>

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-the-application"></a><span data-ttu-id="8df1f-156">建立應用程式</span><span class="sxs-lookup"><span data-stu-id="8df1f-156">Create the application</span></span>
<span data-ttu-id="8df1f-157">接下來我們要建置應用程式。</span><span class="sxs-lookup"><span data-stu-id="8df1f-157">Now we're ready to build the application.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="8df1f-158">建立模型</span><span class="sxs-lookup"><span data-stu-id="8df1f-158">Create a model</span></span>
<span data-ttu-id="8df1f-159">「模型」  是代表您應用程式中資料的物件。</span><span class="sxs-lookup"><span data-stu-id="8df1f-159">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="8df1f-160">對於應用程式，唯一的模型是工作物件，代表待辦事項清單中的項目。</span><span class="sxs-lookup"><span data-stu-id="8df1f-160">For the application, the only model is a task object, which represents an item in the to-do list.</span></span> <span data-ttu-id="8df1f-161">工作將會有下列欄位：</span><span class="sxs-lookup"><span data-stu-id="8df1f-161">Tasks will have the following fields:</span></span>

* <span data-ttu-id="8df1f-162">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="8df1f-162">PartitionKey</span></span>
* <span data-ttu-id="8df1f-163">RowKey</span><span class="sxs-lookup"><span data-stu-id="8df1f-163">RowKey</span></span>
* <span data-ttu-id="8df1f-164">name (字串)</span><span class="sxs-lookup"><span data-stu-id="8df1f-164">name (string)</span></span>
* <span data-ttu-id="8df1f-165">category (字串)</span><span class="sxs-lookup"><span data-stu-id="8df1f-165">category (string)</span></span>
* <span data-ttu-id="8df1f-166">completed (布林值)</span><span class="sxs-lookup"><span data-stu-id="8df1f-166">completed (Boolean)</span></span>

<span data-ttu-id="8df1f-167">**PartitionKey** 和 **RowKey** 由表格服務用來做為資料表索引鍵。</span><span class="sxs-lookup"><span data-stu-id="8df1f-167">**PartitionKey** and **RowKey** are used by the Table Service as table keys.</span></span> <span data-ttu-id="8df1f-168">如需詳細資訊，請參閱 [了解表格服務資料模型](https://msdn.microsoft.com/library/azure/dd179338.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8df1f-168">For more information, see [Understanding the Table Service data model](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

1. <span data-ttu-id="8df1f-169">在 **tasklist** 目錄中，建立新目錄 **models**。</span><span class="sxs-lookup"><span data-stu-id="8df1f-169">In the **tasklist** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="8df1f-170">在 **models** 目錄中，建立新檔案 **task.js**。</span><span class="sxs-lookup"><span data-stu-id="8df1f-170">In the **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="8df1f-171">此檔案將包含您的應用程式建立之工作的模型。</span><span class="sxs-lookup"><span data-stu-id="8df1f-171">This file will contain the model for the tasks created by your application.</span></span>
3. <span data-ttu-id="8df1f-172">在 **task.js** 檔案的開頭加入以下程式碼以參考所需的程式庫：</span><span class="sxs-lookup"><span data-stu-id="8df1f-172">At the beginning of the **task.js** file, add the following code to reference required libraries:</span></span>
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. <span data-ttu-id="8df1f-173">新增下列程式碼以定義和匯出 Task 物件。</span><span class="sxs-lookup"><span data-stu-id="8df1f-173">Add the following code to define and export the Task object.</span></span> <span data-ttu-id="8df1f-174">此物件負責連接至資料表。</span><span class="sxs-lookup"><span data-stu-id="8df1f-174">This object is responsible for connecting to the table.</span></span>
   
          module.exports = Task;
   
        function Task(storageClient, tableName, partitionKey) {
          this.storageClient = storageClient;
          this.tableName = tableName;
          this.partitionKey = partitionKey;
          this.storageClient.createTableIfNotExists(tableName, function tableCreated(error) {
            if(error) {
              throw error;
            }
          });
        };
5. <span data-ttu-id="8df1f-175">新增下列程式碼以定義 Task 物件上的其他方法，允許與資料表中存放的資料互動：</span><span class="sxs-lookup"><span data-stu-id="8df1f-175">Add the following code to define additional methods on the Task object, which allow interactions with data stored in the table:</span></span>
   
        Task.prototype = {
          find: function(query, callback) {
            self = this;
            self.storageClient.queryEntities(this.tableName, query, null, function entitiesQueried(error, result) {
              if(error) {
                callback(error);
              } else {
                callback(null, result.entries);
              }
            });
          },
   
          addItem: function(item, callback) {
            self = this;
            // use entityGenerator to set types
            // NOTE: RowKey must be a string type, even though
            // it contains a GUID in this example.
            var itemDescriptor = {
              PartitionKey: entityGen.String(self.partitionKey),
              RowKey: entityGen.String(uuid()),
              name: entityGen.String(item.name),
              category: entityGen.String(item.category),
              completed: entityGen.Boolean(false)
            };
            self.storageClient.insertEntity(self.tableName, itemDescriptor, function entityInserted(error) {
              if(error){  
                callback(error);
              }
              callback(null);
            });
          },
   
          updateItem: function(rKey, callback) {
            self = this;
            self.storageClient.retrieveEntity(self.tableName, self.partitionKey, rKey, function entityQueried(error, entity) {
              if(error) {
                callback(error);
              }
              entity.completed._ = true;
              self.storageClient.updateEntity(self.tableName, entity, function entityUpdated(error) {
                if(error) {
                  callback(error);
                }
                callback(null);
              });
            });
          }
        }
6. <span data-ttu-id="8df1f-176">儲存並關閉 **task.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="8df1f-176">Save and close the **task.js** file.</span></span>

### <a name="create-a-controller"></a><span data-ttu-id="8df1f-177">建立控制器</span><span class="sxs-lookup"><span data-stu-id="8df1f-177">Create a controller</span></span>
<span data-ttu-id="8df1f-178">「控制器」  處理 HTTP 要求並呈現 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="8df1f-178">A *controller* handles HTTP requests and renders the HTML response.</span></span>

1. <span data-ttu-id="8df1f-179">在 **tasklist/routes** 目錄中建立新檔案 **tasklist.js**，然後在文字編輯器中開啟檔案。</span><span class="sxs-lookup"><span data-stu-id="8df1f-179">In the **tasklist/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="8df1f-180">在 **tasklist.js**中加入以下程式碼。</span><span class="sxs-lookup"><span data-stu-id="8df1f-180">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="8df1f-181">這會載入 azure 和 async 模組，它們是由 **tasklist.js**所使用。</span><span class="sxs-lookup"><span data-stu-id="8df1f-181">This loads the azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="8df1f-182">這也會定義 **TaskList** 函式，系統會傳遞我們稍早定義的 **Task** 物件執行個體給它：</span><span class="sxs-lookup"><span data-stu-id="8df1f-182">This also defines the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. <span data-ttu-id="8df1f-183">定義 **TaskList** 物件。</span><span class="sxs-lookup"><span data-stu-id="8df1f-183">Define a **TaskList** object.</span></span>
   
        function TaskList(task) {
          this.task = task;
        }
4. <span data-ttu-id="8df1f-184">將下列方法新增至 **TaskList**：</span><span class="sxs-lookup"><span data-stu-id="8df1f-184">Add the following methods to **TaskList**:</span></span>
   
        TaskList.prototype = {
          showTasks: function(req, res) {
            self = this;
            var query = new azure.TableQuery()
              .where('completed eq ?', false);
            self.task.find(query, function itemsFound(error, items) {
              res.render('index',{title: 'My ToDo List ', tasks: items});
            });
          },
   
          addTask: function(req,res) {
            var self = this;
            var item = req.body.item;
            self.task.addItem(item, function itemAdded(error) {
              if(error) {
                throw error;
              }
              res.redirect('/');
            });
          },
   
          completeTask: function(req,res) {
            var self = this;
            var completedTasks = Object.keys(req.body);
            async.forEach(completedTasks, function taskIterator(completedTask, callback) {
              self.task.updateItem(completedTask, function itemsUpdated(error) {
                if(error){
                  callback(error);
                } else {
                  callback(null);
                }
              });
            }, function goHome(error){
              if(error) {
                throw error;
              } else {
               res.redirect('/');
              }
            });
          }
        }

### <a name="modify-appjs"></a><span data-ttu-id="8df1f-185">修改 app.js</span><span class="sxs-lookup"><span data-stu-id="8df1f-185">Modify app.js</span></span>
1. <span data-ttu-id="8df1f-186">在 **tasklist** 目錄中，開啟 **app.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="8df1f-186">From the **tasklist** directory, open the **app.js** file.</span></span> <span data-ttu-id="8df1f-187">此檔案是稍早執行 **express** 命令所建立。</span><span class="sxs-lookup"><span data-stu-id="8df1f-187">This file was created earlier by running the **express** command.</span></span>
2. <span data-ttu-id="8df1f-188">在檔案開頭，加入下列內容以載入 azure 模組、設定資料表名稱、資料分割索引鍵，以及設定此範例所使用的儲存體認證：</span><span class="sxs-lookup"><span data-stu-id="8df1f-188">At the beginning of the file, add the following to load the azure module, set the table name, partition key, and set the storage credentials used by this example:</span></span>
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > <span data-ttu-id="8df1f-189">nconf 會從環境變數或 **config.json** 檔案 (我們稍後會建立) 載入組態值。</span><span class="sxs-lookup"><span data-stu-id="8df1f-189">nconf will load the configuration values from either environment variables or the **config.json** file, which we will create later.</span></span>
   > 
   > 
3. <span data-ttu-id="8df1f-190">在 app.js 檔中，向下捲動到看見此行處：</span><span class="sxs-lookup"><span data-stu-id="8df1f-190">In the app.js file, scroll down to where you see the following line:</span></span>
   
        app.use('/', routes);
        app.use('/users', users);
   
    <span data-ttu-id="8df1f-191">將以上幾行取代為以下顯示的程式碼。</span><span class="sxs-lookup"><span data-stu-id="8df1f-191">Replace the above lines with the code shown below.</span></span> <span data-ttu-id="8df1f-192">這會初始化 <strong>Task</strong> 的執行個體，並連接到您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="8df1f-192">This will initialize an instance of <strong>Task</strong> with a connection to your storage account.</span></span> <span data-ttu-id="8df1f-193">這會傳遞給 <strong>TaskList</strong>，它將用來與表格服務通訊：</span><span class="sxs-lookup"><span data-stu-id="8df1f-193">This is passed to the <strong>TaskList</strong>, which will use it to communicate with the Table service:</span></span>
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. <span data-ttu-id="8df1f-194">儲存 **app.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="8df1f-194">Save the **app.js** file.</span></span>

### <a name="modify-the-index-view"></a><span data-ttu-id="8df1f-195">修改索引檢視</span><span class="sxs-lookup"><span data-stu-id="8df1f-195">Modify the index view</span></span>
1. <span data-ttu-id="8df1f-196">以文字編輯器開啟 **tasklist/views/index.jade** 檔案。</span><span class="sxs-lookup"><span data-stu-id="8df1f-196">Open the **tasklist/views/index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="8df1f-197">將檔案的整個內容取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="8df1f-197">Replace the entire contents of the file with the following code.</span></span> <span data-ttu-id="8df1f-198">這會定義顯示現有工作的檢視，並且包括加入新工作及將現有工作標示為完成的表單。</span><span class="sxs-lookup"><span data-stu-id="8df1f-198">This defines a view that displays existing tasks and includes a form for adding new tasks and marking existing ones as completed.</span></span>
   
        extends layout
   
        block content
          h1= title
          br
   
          form(action="/completetask", method="post")
            table.table.table-striped.table-bordered
              tr
                td Name
                td Category
                td Date
                td Complete
              if (typeof tasks === "undefined")
                tr
                  td
              else
                each task in tasks
                  tr
                    td #{task.name._}
                    td #{task.category._}
                    - var day   = task.Timestamp._.getDate();
                    - var month = task.Timestamp._.getMonth() + 1;
                    - var year  = task.Timestamp._.getFullYear();
                    td #{month + "/" + day + "/" + year}
                    td
                      input(type="checkbox", name="#{task.RowKey._}", value="#{!task.completed._}", checked=task.completed._)
            button.btn(type="submit") Update tasks
          hr
          form.well(action="/addtask", method="post")
            label Item Name:
            input(name="item[name]", type="textbox")
            label Item Category:
            input(name="item[category]", type="textbox")
            br
            button.btn(type="submit") Add item
3. <span data-ttu-id="8df1f-199">儲存並關閉 **index.jade** 檔案。</span><span class="sxs-lookup"><span data-stu-id="8df1f-199">Save and close **index.jade** file.</span></span>

### <a name="modify-the-global-layout"></a><span data-ttu-id="8df1f-200">修改全域版面配置</span><span class="sxs-lookup"><span data-stu-id="8df1f-200">Modify the global layout</span></span>
<span data-ttu-id="8df1f-201">**views** 目錄中的 **layout.jade** 檔案是其他 **.jade** 檔案的全域範本。</span><span class="sxs-lookup"><span data-stu-id="8df1f-201">The **layout.jade** file in the **views** directory is a global template for other **.jade** files.</span></span> <span data-ttu-id="8df1f-202">在此步驟中，您將修改它以使用 [Twitter Bootstrap](https://github.com/twbs/bootstrap)，這個工具組能夠方便設計美觀的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8df1f-202">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking web app.</span></span>

<span data-ttu-id="8df1f-203">下載並解壓縮 [Twitter Bootstrap](http://getbootstrap.com/)的檔案。</span><span class="sxs-lookup"><span data-stu-id="8df1f-203">Download and extract the files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="8df1f-204">將 **bootstrap.min.css** 檔案從 Bootstrap **css** 資料夾複製到您應用程式的 **public/stylesheets** 目錄。</span><span class="sxs-lookup"><span data-stu-id="8df1f-204">Copy the **bootstrap.min.css** file from the Bootstrap **css** folder into the **public/stylesheets** directory of your application.</span></span>

<span data-ttu-id="8df1f-205">從 **views** 資料夾，開啟 **layout.jade**，並將全部內容取代為：</span><span class="sxs-lookup"><span data-stu-id="8df1f-205">From the **views** folder, open **layout.jade** and replace the entire contents with the following:</span></span>

    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body.app
        nav.navbar.navbar-default
          div.navbar-header
          a.navbar-brand(href='/') My Tasks
        block content

### <a name="create-a-config-file"></a><span data-ttu-id="8df1f-206">建立組態檔</span><span class="sxs-lookup"><span data-stu-id="8df1f-206">Create a config file</span></span>
<span data-ttu-id="8df1f-207">為了在本機執行應用程式，我們會將 Azure 儲存體認證放入組態檔。</span><span class="sxs-lookup"><span data-stu-id="8df1f-207">To run the app locally, we'll put Azure Storage credentials into a config file.</span></span> <span data-ttu-id="8df1f-208">使用下列 JSON 建立名為 **config.json** 的檔案：</span><span class="sxs-lookup"><span data-stu-id="8df1f-208">Create a file named **config.json* *with the following JSON:</span></span>

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="8df1f-209">將 **儲存體帳戶名稱**取代為您先前建立的儲存體帳戶名稱，並將**儲存體存取金鑰**取代為您儲存體帳戶的主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="8df1f-209">Replace **storage account name** with the name of the storage account you created earlier, and replace **storage access key** with the primary access key for your storage account.</span></span> <span data-ttu-id="8df1f-210">例如：</span><span class="sxs-lookup"><span data-stu-id="8df1f-210">For example:</span></span>

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="8df1f-211">將此檔案儲存在比 *tasklist* 目錄 **高一個目錄層級** 的位置，像這樣：</span><span class="sxs-lookup"><span data-stu-id="8df1f-211">Save this file *one directory level higher* than the **tasklist** directory, like this:</span></span>

    parent/
      |-- config.json
      |-- tasklist/

<span data-ttu-id="8df1f-212">執行此動作的原因是為了避免將組態檔簽入原始檔控制而成為公用。</span><span class="sxs-lookup"><span data-stu-id="8df1f-212">The reason for doing this is to avoid checking the config file into source control, where it might become public.</span></span> <span data-ttu-id="8df1f-213">當我們將應用程式部署至 Azure 時，我們會使用環境變數而不用組態檔。</span><span class="sxs-lookup"><span data-stu-id="8df1f-213">When we deploy the app to Azure, we will use environment variables instead of a config file.</span></span>

## <a name="run-the-application-locally"></a><span data-ttu-id="8df1f-214">在本機執行應用程式</span><span class="sxs-lookup"><span data-stu-id="8df1f-214">Run the application locally</span></span>
<span data-ttu-id="8df1f-215">若要在本機電腦測試應用程式，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8df1f-215">To test the application on your local machine, perform the following steps:</span></span>

1. <span data-ttu-id="8df1f-216">使用命令列變更目錄至 **tasklist** 目錄。</span><span class="sxs-lookup"><span data-stu-id="8df1f-216">From the command-line, change directories to the **tasklist** directory.</span></span>
2. <span data-ttu-id="8df1f-217">使用下列命令在本機啟動應用程式：</span><span class="sxs-lookup"><span data-stu-id="8df1f-217">Use the following command to launch the application locally:</span></span>
   
        npm start
3. <span data-ttu-id="8df1f-218">開啟瀏覽器，導覽至 http://127.0.0.1:3000 。</span><span class="sxs-lookup"><span data-stu-id="8df1f-218">Open a web browser and navigate to http://127.0.0.1:3000.</span></span>
   
    <span data-ttu-id="8df1f-219">類似下列的範例網頁隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="8df1f-219">A web page similar to the following example appears.</span></span>
   
    ![A webpage displaying an empty tasklist][node-table-finished]
4. <span data-ttu-id="8df1f-221">若要建立新的待辦事項，請輸入名稱和類別目錄，然後按一下 [新增項目]。</span><span class="sxs-lookup"><span data-stu-id="8df1f-221">To create a new to-do item, enter a name and category and click **Add Item**.</span></span> 
5. <span data-ttu-id="8df1f-222">若要將工作標示為完成，請核取 [完成] 並且按一下 [更新工作]。</span><span class="sxs-lookup"><span data-stu-id="8df1f-222">To mark a task as complete, check **Complete** and click **Update Tasks**.</span></span>
   
    ![An image of the new item in the list of tasks][node-table-list-items]

<span data-ttu-id="8df1f-224">雖然應用程式是在本機執行，但是它會將資料儲存在 Azure 表格服務中。</span><span class="sxs-lookup"><span data-stu-id="8df1f-224">Even though the application is running locally, it is storing the data in the Azure Table service.</span></span>

## <a name="deploy-your-application-to-azure"></a><span data-ttu-id="8df1f-225">將應用程式部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="8df1f-225">Deploy your application to Azure</span></span>
<span data-ttu-id="8df1f-226">本節的步驟使用 Azure 命令列工具在 App Service 中建立新的 Web 應用程式，然後使用 Git 部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="8df1f-226">The steps in this section use the Azure command-line tools to create a new web app in App Service, and then use Git to deploy your application.</span></span> <span data-ttu-id="8df1f-227">若要執行這些步驟，必須有 Azure 定用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8df1f-227">To perform these steps you must have an Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="8df1f-228">您也可以使用 [Azure 入口網站](https://portal.azure.com/)執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="8df1f-228">These steps can also be performed by using the [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="8df1f-229">請參閱 [在 Azure App Service 中建置和部署 Node.js Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8df1f-229">See [Build and deploy a Node.js web app in Azure App Service].</span></span>
> 
> <span data-ttu-id="8df1f-230">如果這是您建立的第一個 Web 應用程式，您必須使用 Azure 入口網站部署此應用程式。</span><span class="sxs-lookup"><span data-stu-id="8df1f-230">If this is the first web app you have created, you must use the Azure Portal to deploy this application.</span></span>
> 
> 

<span data-ttu-id="8df1f-231">若要開始，請安裝 [Azure CLI] ，方法是從命令列輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="8df1f-231">To get started, install the [Azure CLI] by entering the following command from the command line:</span></span>

    npm install azure-cli -g

### <a name="import-publishing-settings"></a><span data-ttu-id="8df1f-232">匯入發佈設定</span><span class="sxs-lookup"><span data-stu-id="8df1f-232">Import publishing settings</span></span>
<span data-ttu-id="8df1f-233">在此步驟中，您將會下載包含您訂用帳戶相關資訊的檔案。</span><span class="sxs-lookup"><span data-stu-id="8df1f-233">In this step, you will download a file containing information about your subscription.</span></span>

1. <span data-ttu-id="8df1f-234">輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="8df1f-234">Enter the following command:</span></span>
   
        azure login
   
    <span data-ttu-id="8df1f-235">此命令會啟動瀏覽器並瀏覽至下載頁面。</span><span class="sxs-lookup"><span data-stu-id="8df1f-235">This command launches a browser and navigates to the download page.</span></span> <span data-ttu-id="8df1f-236">若出現提示，請使用與您的 Azure 訂用帳戶相關聯的帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="8df1f-236">If prompted, log in with the account associated with your Azure subscription.</span></span>
   
    <!-- ![The download page][download-publishing-settings] -->
   
    <span data-ttu-id="8df1f-237">檔案下載會自動開始；如果沒有，您可以按一下頁面頂端的連結，以手動下載檔案。</span><span class="sxs-lookup"><span data-stu-id="8df1f-237">The file download begins automatically; if it does not, you can click the link at the beginning of the page to manually download the file.</span></span> <span data-ttu-id="8df1f-238">儲存檔案，並記下檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="8df1f-238">Save the file and note the file path.</span></span>
2. <span data-ttu-id="8df1f-239">輸入下列命令以匯入設定：</span><span class="sxs-lookup"><span data-stu-id="8df1f-239">Enter the following command to import the settings:</span></span>
   
        azure account import <path-to-file>
   
    <span data-ttu-id="8df1f-240">指定前一個步驟下載之發佈設定檔案的路徑和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="8df1f-240">Specify the path and file name of the publishing settings file you downloaded in the previous step.</span></span>
3. <span data-ttu-id="8df1f-241">匯入設定之後，刪除發佈設定檔案。</span><span class="sxs-lookup"><span data-stu-id="8df1f-241">After the settings are imported, delete the publish settings file.</span></span> <span data-ttu-id="8df1f-242">這個檔案已經不再需要，而且包含與 Azure 訂用帳戶相關的機密資訊。</span><span class="sxs-lookup"><span data-stu-id="8df1f-242">It is no longer needed, and contains sensitive information regarding your Azure subscription.</span></span>

### <a name="create-an-app-service-web-app"></a><span data-ttu-id="8df1f-243">建立 App Service Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="8df1f-243">Create an App Service web app</span></span>
1. <span data-ttu-id="8df1f-244">使用命令列變更目錄至 **tasklist** 目錄。</span><span class="sxs-lookup"><span data-stu-id="8df1f-244">From the command-line, change directories to the **tasklist** directory.</span></span>
2. <span data-ttu-id="8df1f-245">使用下列命令建立新的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8df1f-245">Use the following command to create a new web app.</span></span>
   
        azure site create --git
   
    <span data-ttu-id="8df1f-246">系統會提示您輸入 Web 應用程式名稱和位置。</span><span class="sxs-lookup"><span data-stu-id="8df1f-246">You will be prompted for the web app name and location.</span></span> <span data-ttu-id="8df1f-247">請提供唯一的名稱，並且選取與您的 Azure 儲存體帳戶相同的地理位置。</span><span class="sxs-lookup"><span data-stu-id="8df1f-247">Provide a unique name and select the same geographical location as your Azure Storage account.</span></span>
   
    <span data-ttu-id="8df1f-248">`--git` 參數會在 Azure 上建立此 Web 應用程式的 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="8df1f-248">The `--git` parameter creates a Git repository on Azure for this web app.</span></span> <span data-ttu-id="8df1f-249">它也會在目前的目錄中初始化 Git 儲存機制 (如果不存在)，並且新增名為 'azure' 的 [Git 遠端] ，用來將應用程式發佈至 Azure。</span><span class="sxs-lookup"><span data-stu-id="8df1f-249">It also initializes a Git repository in the current directory if none exists, and adds a [Git remote] named 'azure', which is used to publish the application to Azure.</span></span> <span data-ttu-id="8df1f-250">最後，它會建立 **web.config** 檔案，其中包含 Azure 代管 node 應用程式所使用的設定。</span><span class="sxs-lookup"><span data-stu-id="8df1f-250">Finally, it creates a **web.config** file, which contains settings used by Azure to host node applications.</span></span> <span data-ttu-id="8df1f-251">如果您省略 `--git` 參數，但該目錄仍包含 Git 儲存機制，則此命令仍會建立 'azure' 遠端。</span><span class="sxs-lookup"><span data-stu-id="8df1f-251">If you omit the `--git` parameter but the directory contains a Git repository, the command will still create the 'azure' remote.</span></span>
   
    <span data-ttu-id="8df1f-252">一旦此命令完成，您將會看到類似以下的輸出。</span><span class="sxs-lookup"><span data-stu-id="8df1f-252">Once this command has completed, you will see output similar to the following.</span></span> <span data-ttu-id="8df1f-253">請注意， **Website created at** 開頭的這一行包含 Web 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="8df1f-253">Note that the line beginning with **Website created at** contains the URL for the web app.</span></span>
   
        info:   Executing command site create
        help:   Need a site name
        Name: TableTasklist
        info:   Using location southcentraluswebspace
        info:   Executing `git init`
        info:   Creating default .gitignore file
        info:   Creating a new web site
        info:   Created web site at  tabletasklist.azurewebsites.net
        info:   Initializing repository
        info:   Repository initialized
        info:   Executing `git remote add azure https://username@tabletasklist.azurewebsites.net/TableTasklist.git`
        info:   site create command OK
   
   > [!NOTE]
   > <span data-ttu-id="8df1f-254">如果這是您訂用帳戶的第一個 App Service Web 應用程式，系統將指示您使用 Azure 入口網站來建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8df1f-254">If this is the first App Service web app for your subscription, you will be instructed to use the Azure Portal to create the web app.</span></span> <span data-ttu-id="8df1f-255">如需詳細資訊，請參閱 [在 Azure App Service 中建置和部署 Node.js Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="8df1f-255">For more information, see [Build and deploy a Node.js web app in Azure App Service].</span></span>
   > 
   > 

### <a name="set-environment-variables"></a><span data-ttu-id="8df1f-256">設定環境變數</span><span class="sxs-lookup"><span data-stu-id="8df1f-256">Set environment variables</span></span>
<span data-ttu-id="8df1f-257">在此步驟中，您會新增環境變數至您在 Azure 上的 Web 應用程式組態。</span><span class="sxs-lookup"><span data-stu-id="8df1f-257">In this step, you will add environment variables to your web app configuration on Azure.</span></span>
<span data-ttu-id="8df1f-258">從命令列中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="8df1f-258">From the command line, enter the following:</span></span>

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


<span data-ttu-id="8df1f-259">將 **<storage account name>** 取代為您先前建立的儲存體帳戶名稱，並將 **<storage access key>** 取代為您儲存體帳戶的主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="8df1f-259">Replace **<storage account name>** with the name of the storage account you created earlier, and replace **<storage access key>** with the primary access key for your storage account.</span></span> <span data-ttu-id="8df1f-260">(使用與您稍早建立的 config.json 檔案相同的值)。</span><span class="sxs-lookup"><span data-stu-id="8df1f-260">(Use the same values as the config.json file that you created earlier.)</span></span>

<span data-ttu-id="8df1f-261">或者，您可以在 [Azure 入口網站](https://portal.azure.com/)中設定環境變數：</span><span class="sxs-lookup"><span data-stu-id="8df1f-261">Alternatively, you can set environment variables in the [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="8df1f-262">依序按一下 [瀏覽]  >  [Web 應用程式] > Web 應用程式名稱，開啟 Web 應用程式的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8df1f-262">Open the web app's blade by clicking **Browse** > **Web Apps** > your web app name.</span></span>
2. <span data-ttu-id="8df1f-263">在您的 Web 應用程式刀鋒視窗中，按一下 [所有設定]  >  [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="8df1f-263">In your web app's blade, click **All Settings** > **Application Settings**.</span></span>
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. <span data-ttu-id="8df1f-264">向下捲動至 [應用程式設定]  區段，並新增金鑰/值組。</span><span class="sxs-lookup"><span data-stu-id="8df1f-264">Scroll down to the **App settings** section and add the key/value pairs.</span></span>
   
     ![應用程式設定](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. <span data-ttu-id="8df1f-266">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="8df1f-266">Click **SAVE**.</span></span>

### <a name="publish-the-application"></a><span data-ttu-id="8df1f-267">發佈應用程式</span><span class="sxs-lookup"><span data-stu-id="8df1f-267">Publish the application</span></span>
<span data-ttu-id="8df1f-268">若要發佈應用程式，請將程式碼檔案認可到 Git，然後推送至 azure/master。</span><span class="sxs-lookup"><span data-stu-id="8df1f-268">To publish the app, commit the code files to Git and then push to azure/master.</span></span>

1. <span data-ttu-id="8df1f-269">設定您的部署認證。</span><span class="sxs-lookup"><span data-stu-id="8df1f-269">Set your deployment credentials.</span></span>
   
        azure site deployment user set <name> <password>
2. <span data-ttu-id="8df1f-270">新增並認可您的應用程式檔案。</span><span class="sxs-lookup"><span data-stu-id="8df1f-270">Add and commit your application files.</span></span>
   
        git add .
        git commit -m "adding files"
3. <span data-ttu-id="8df1f-271">將認可推送至 App Service Web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="8df1f-271">Push the commit to the App Service web app:</span></span>
   
        git push azure master
   
    <span data-ttu-id="8df1f-272">使用 **master** 做為目標分支。</span><span class="sxs-lookup"><span data-stu-id="8df1f-272">Use **master** as the target branch.</span></span> <span data-ttu-id="8df1f-273">在部署結束時，您會看到類似下列範例中的陳述式：</span><span class="sxs-lookup"><span data-stu-id="8df1f-273">At the end of the deployment, you see a statement similar to the following example:</span></span>
   
        To https://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. <span data-ttu-id="8df1f-274">完成推送作業後，瀏覽至先前由 `azure create site` 命令傳回的 Web 應用程式 URL 以檢視您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8df1f-274">Once the push operation has completed, browse to the web app URL returned previously by the `azure create site` command to view your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8df1f-275">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8df1f-275">Next steps</span></span>
<span data-ttu-id="8df1f-276">雖然本文的步驟說明如何使用資料表服務來存放資訊，您也可以使用 [MongoDB](https://mlab.com/azure/)。</span><span class="sxs-lookup"><span data-stu-id="8df1f-276">While the steps in this article describe using the Table Service to store information, you can also use [MongoDB](https://mlab.com/azure/).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="8df1f-277">其他資源</span><span class="sxs-lookup"><span data-stu-id="8df1f-277">Additional resources</span></span>
<span data-ttu-id="8df1f-278">[Azure CLI]</span><span class="sxs-lookup"><span data-stu-id="8df1f-278">[Azure CLI]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="8df1f-279">變更的項目</span><span class="sxs-lookup"><span data-stu-id="8df1f-279">What's changed</span></span>
* <span data-ttu-id="8df1f-280">如需從網站變更為 App Service 的指南，請參閱： [Azure App Service 及其對現有 Azure 服務的影響](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="8df1f-280">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- URLs -->

<span data-ttu-id="8df1f-281">[在 Azure App Service 中建置和部署 Node.js Web 應用程式]: app-service-web-get-started-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="8df1f-281">[Build and deploy a Node.js web app in Azure App Service]: app-service-web-get-started-nodejs.md</span></span>
[Azure Developer Center]: /develop/nodejs/

<span data-ttu-id="8df1f-282">[node]: http://nodejs.org</span><span class="sxs-lookup"><span data-stu-id="8df1f-282">[node]: http://nodejs.org</span></span>
<span data-ttu-id="8df1f-283">[Git]: http://git-scm.com</span><span class="sxs-lookup"><span data-stu-id="8df1f-283">[Git]: http://git-scm.com</span></span>
<span data-ttu-id="8df1f-284">[Express]: http://expressjs.com</span><span class="sxs-lookup"><span data-stu-id="8df1f-284">[Express]: http://expressjs.com</span></span>
[for free]: http://windowsazure.com
<span data-ttu-id="8df1f-285">[Git 遠端]: http://git-scm.com/docs/git-remote</span><span class="sxs-lookup"><span data-stu-id="8df1f-285">[Git remote]: http://git-scm.com/docs/git-remote</span></span>

<span data-ttu-id="8df1f-286">[Azure CLI]:../cli-install-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="8df1f-286">[Azure CLI]:../cli-install-nodejs.md</span></span>

<span data-ttu-id="8df1f-287">[azure]: https://github.com/Azure/azure-sdk-for-node</span><span class="sxs-lookup"><span data-stu-id="8df1f-287">[azure]: https://github.com/Azure/azure-sdk-for-node</span></span>
<span data-ttu-id="8df1f-288">[node-uuid]: https://www.npmjs.com/package/node-uuid</span><span class="sxs-lookup"><span data-stu-id="8df1f-288">[node-uuid]: https://www.npmjs.com/package/node-uuid</span></span>
<span data-ttu-id="8df1f-289">[nconf]: https://www.npmjs.com/package/nconf</span><span class="sxs-lookup"><span data-stu-id="8df1f-289">[nconf]: https://www.npmjs.com/package/nconf</span></span>
<span data-ttu-id="8df1f-290">[async]: https://www.npmjs.com/package/async</span><span class="sxs-lookup"><span data-stu-id="8df1f-290">[async]: https://www.npmjs.com/package/async</span></span>

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application to an Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
