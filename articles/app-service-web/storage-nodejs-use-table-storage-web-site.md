---
title: "aaaNode.js 使用 hello Azure 表格服務的 web 應用程式"
description: "本教學課程將教導您如何 toouse hello Azure 資料表服務 toostore Node.js 應用程式裝載於 Azure App Service Web 應用程式的資料。"
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
ms.openlocfilehash: f6e08335b4c7f62f7b3994287edd586860cb7135
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-using-hello-azure-table-service"></a><span data-ttu-id="77fe4-103">Node.js web 應用程式使用 hello Azure 資料表服務</span><span class="sxs-lookup"><span data-stu-id="77fe4-103">Node.js web app using hello Azure Table Service</span></span>
## <a name="overview"></a><span data-ttu-id="77fe4-104">概觀</span><span class="sxs-lookup"><span data-stu-id="77fe4-104">Overview</span></span>
<span data-ttu-id="77fe4-105">此教學課程會示範如何 toouse 表格服務提供的 Azure 資料管理 toostore 及存取資料，從[節點]應用程式裝載於[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="77fe4-105">This tutorial shows you how toouse Table service provided by Azure Data Management toostore and access data from a [node] application hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="77fe4-106">本教學課程假設您先前有過一些使用節點及 [Git]的經驗。</span><span class="sxs-lookup"><span data-stu-id="77fe4-106">This tutorial assumes that you have some prior experience using node and [Git].</span></span>

<span data-ttu-id="77fe4-107">您將了解：</span><span class="sxs-lookup"><span data-stu-id="77fe4-107">You will learn:</span></span>

* <span data-ttu-id="77fe4-108">如何 toouse npm （node 封裝管理員） tooinstall hello 節點模組</span><span class="sxs-lookup"><span data-stu-id="77fe4-108">How toouse npm (node package manager) tooinstall hello node modules</span></span>
* <span data-ttu-id="77fe4-109">如何使用 toowork hello Azure 資料表服務</span><span class="sxs-lookup"><span data-stu-id="77fe4-109">How toowork with hello Azure Table service</span></span>
* <span data-ttu-id="77fe4-110">如何 toouse hello Azure CLI toocreate web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="77fe4-110">How toouse hello Azure CLI toocreate a web app.</span></span>

<span data-ttu-id="77fe4-111">依照本教學課程的指示，您將組建一個簡單的網頁型「待辦事項清單」應用程式，用於建立、擷取、完成工作。</span><span class="sxs-lookup"><span data-stu-id="77fe4-111">By following this tutorial, you will build a simple web-based "to-do list" application that allows creating, retrieving and completing tasks.</span></span> <span data-ttu-id="77fe4-112">hello 工作會儲存在 hello 表格服務。</span><span class="sxs-lookup"><span data-stu-id="77fe4-112">hello tasks are stored in hello Table service.</span></span>

<span data-ttu-id="77fe4-113">以下是 hello 完成應用程式：</span><span class="sxs-lookup"><span data-stu-id="77fe4-113">Here is hello completed application:</span></span>

![顯示空白工作清單的網頁][node-table-finished]

> [!NOTE]
> <span data-ttu-id="77fe4-115">如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="77fe4-115">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="77fe4-116">不需要信用卡；沒有承諾。</span><span class="sxs-lookup"><span data-stu-id="77fe4-116">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="77fe4-117">必要條件</span><span class="sxs-lookup"><span data-stu-id="77fe4-117">Prerequisites</span></span>
<span data-ttu-id="77fe4-118">之前遵循這篇文章中的 hello 指示，請確定您擁有 hello 安裝下列項目：</span><span class="sxs-lookup"><span data-stu-id="77fe4-118">Before following hello instructions in this article, ensure that you have hello following installed:</span></span>

* <span data-ttu-id="77fe4-119">[節點] 版本 0.10.24 或更高版本</span><span class="sxs-lookup"><span data-stu-id="77fe4-119">[node] version 0.10.24 or higher</span></span>
* <span data-ttu-id="77fe4-120">[Git]</span><span class="sxs-lookup"><span data-stu-id="77fe4-120">[Git]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a><span data-ttu-id="77fe4-121">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="77fe4-121">Create a storage account</span></span>
<span data-ttu-id="77fe4-122">建立 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="77fe4-122">Create an Azure storage account.</span></span> <span data-ttu-id="77fe4-123">hello 應用程式會使用此帳戶 toostore hello 待辦項目。</span><span class="sxs-lookup"><span data-stu-id="77fe4-123">hello app will use this account toostore hello to-do items.</span></span>

1. <span data-ttu-id="77fe4-124">登入 hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="77fe4-124">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="77fe4-125">按一下 hello**新增**hello 下方圖示左邊 hello 入口網站，請按一下 **資料 + 儲存體** > **儲存體**。</span><span class="sxs-lookup"><span data-stu-id="77fe4-125">Click hello **New** icon on hello bottom left of hello portal, then click **Data + Storage** > **Storage**.</span></span> <span data-ttu-id="77fe4-126">提供 hello 儲存體帳戶的唯一名稱，並建立新[資源群組](../azure-resource-manager/resource-group-overview.md)它。</span><span class="sxs-lookup"><span data-stu-id="77fe4-126">Give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![新增按鈕](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    <span data-ttu-id="77fe4-128">Hello 儲存體帳戶建立後，hello**通知** 按鈕會閃爍綠色**成功**且 hello 儲存體帳戶的刀鋒視窗已開啟 tooshow 其所屬 toohello 新資源群組建立。</span><span class="sxs-lookup"><span data-stu-id="77fe4-128">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="77fe4-129">在 hello 儲存體帳戶的刀鋒視窗中，按一下 **設定** > **金鑰**。</span><span class="sxs-lookup"><span data-stu-id="77fe4-129">In hello storage account's blade, click **Settings** > **Keys**.</span></span> <span data-ttu-id="77fe4-130">將複製 hello 主要存取金鑰 toohello 剪貼簿。</span><span class="sxs-lookup"><span data-stu-id="77fe4-130">Copy hello primary access key toohello clipboard.</span></span>
   
    ![存取金鑰][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a><span data-ttu-id="77fe4-132">安裝模組及產生樣板</span><span class="sxs-lookup"><span data-stu-id="77fe4-132">Install modules and generate scaffolding</span></span>
<span data-ttu-id="77fe4-133">本節中，您會建立新的 Node 應用程式，並使用 npm tooadd 模組封裝。</span><span class="sxs-lookup"><span data-stu-id="77fe4-133">In this section you will create a new Node application and use npm tooadd module packages.</span></span> <span data-ttu-id="77fe4-134">此應用程式中，您將使用 hello [Express]和[Azure]模組。</span><span class="sxs-lookup"><span data-stu-id="77fe4-134">For this application you will use hello [Express] and [Azure] modules.</span></span> <span data-ttu-id="77fe4-135">hello Express 模組提供節點的模型檢視控制器 」 架構，同時 hello Azure 模組提供連接 toohello 資料表服務。</span><span class="sxs-lookup"><span data-stu-id="77fe4-135">hello Express module provides a Model View Controller framework for node, while hello Azure modules provides connectivity toohello Table service.</span></span>

### <a name="install-express-and-generate-scaffolding"></a><span data-ttu-id="77fe4-136">安裝 Express 及產生樣板</span><span class="sxs-lookup"><span data-stu-id="77fe4-136">Install express and generate scaffolding</span></span>
1. <span data-ttu-id="77fe4-137">從 hello 命令列，建立名為的新目錄**tasklist**和交換器 toothat 目錄。</span><span class="sxs-lookup"><span data-stu-id="77fe4-137">From hello command line, create a new directory named **tasklist** and switch toothat directory.</span></span>  
2. <span data-ttu-id="77fe4-138">輸入下列命令 tooinstall hello Express 模組 hello。</span><span class="sxs-lookup"><span data-stu-id="77fe4-138">Enter hello following command tooinstall hello Express module.</span></span>
   
        npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="77fe4-139">根據 hello 的作業系統，您可能需要 tooput 'sudo' hello 命令之前：</span><span class="sxs-lookup"><span data-stu-id="77fe4-139">Depending on hello operating system, you may need tooput 'sudo' before hello command:</span></span>
   
        sudo npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="77fe4-140">下列範例類似 toohello 出現 hello 輸出：</span><span class="sxs-lookup"><span data-stu-id="77fe4-140">hello output appears similar toohello following example:</span></span>
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > <span data-ttu-id="77fe4-141">hello '-g' 參數全域安裝 hello 模組。</span><span class="sxs-lookup"><span data-stu-id="77fe4-141">hello '-g' parameter installs hello module globally.</span></span> <span data-ttu-id="77fe4-142">這樣一來，我們可以使用**express** toogenerate web 應用程式 scaffolding，而不需要 tootype 中的額外路徑資訊。</span><span class="sxs-lookup"><span data-stu-id="77fe4-142">That way, we can use **express** toogenerate web app scaffolding without having tootype in additional path information.</span></span>
   > 
   > 
3. <span data-ttu-id="77fe4-143">toocreate hello scaffolding hello 應用程式中，輸入 hello **express**命令：</span><span class="sxs-lookup"><span data-stu-id="77fe4-143">toocreate hello scaffolding for hello application, enter hello **express** command:</span></span>
   
        express
   
    <span data-ttu-id="77fe4-144">hello 這個命令的輸出會出現類似下列範例的 toohello:</span><span class="sxs-lookup"><span data-stu-id="77fe4-144">hello output of this command appears similar toohello following example:</span></span>
   
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
   
           run hello app:
             $ DEBUG=my-application ./bin/www
   
    <span data-ttu-id="77fe4-145">您現在有數個新的目錄和檔案在 hello **tasklist**目錄。</span><span class="sxs-lookup"><span data-stu-id="77fe4-145">You now have several new directories and files in hello **tasklist** directory.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="77fe4-146">安裝其他模組</span><span class="sxs-lookup"><span data-stu-id="77fe4-146">Install additional modules</span></span>
<span data-ttu-id="77fe4-147">其中一個 hello 檔案， **express**建立是**package.json**。</span><span class="sxs-lookup"><span data-stu-id="77fe4-147">One of hello files that **express** creates is **package.json**.</span></span> <span data-ttu-id="77fe4-148">此檔案包含模組相依性清單。</span><span class="sxs-lookup"><span data-stu-id="77fe4-148">This file contains a list of module dependencies.</span></span> <span data-ttu-id="77fe4-149">更新版本中，當您部署 hello 應用程式 tooApp Service Web 應用程式時，此檔案會決定哪一個模組必須安裝在 Azure 上的 toobe。</span><span class="sxs-lookup"><span data-stu-id="77fe4-149">Later, when you deploy hello application tooApp Service Web Apps, this file determines which modules need toobe installed on Azure.</span></span>

<span data-ttu-id="77fe4-150">從命令列的 hello，輸入下列命令 tooinstall hello 模組 hello 中所述的 hello **package.json**檔案。</span><span class="sxs-lookup"><span data-stu-id="77fe4-150">From hello command-line, enter hello following command tooinstall hello modules described in hello **package.json** file.</span></span> <span data-ttu-id="77fe4-151">您可能需要 toouse 'sudo'。</span><span class="sxs-lookup"><span data-stu-id="77fe4-151">You may need toouse 'sudo'.</span></span>

    npm install

<span data-ttu-id="77fe4-152">hello 這個命令的輸出會出現類似下列範例的 toohello:</span><span class="sxs-lookup"><span data-stu-id="77fe4-152">hello output of this command appears similar toohello following example:</span></span>

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


<span data-ttu-id="77fe4-153">接下來，輸入下列命令 tooinstall hello hello [azure]，[節點 uuid]， [nconf]和[非同步]模組：</span><span class="sxs-lookup"><span data-stu-id="77fe4-153">Next, enter hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules:</span></span>

    npm install azure-storage node-uuid async nconf --save

<span data-ttu-id="77fe4-154">hello **-儲存**旗標加入這些模組 toohello 項目**package.json**檔案。</span><span class="sxs-lookup"><span data-stu-id="77fe4-154">hello **--save** flag adds entries for these modules toohello **package.json** file.</span></span>

<span data-ttu-id="77fe4-155">hello 這個命令的輸出會出現類似下列範例的 toohello:</span><span class="sxs-lookup"><span data-stu-id="77fe4-155">hello output of this command appears similar toohello following example:</span></span>

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-hello-application"></a><span data-ttu-id="77fe4-156">建立 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="77fe4-156">Create hello application</span></span>
<span data-ttu-id="77fe4-157">現在我們已經準備好 toobuild hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="77fe4-157">Now we're ready toobuild hello application.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="77fe4-158">建立模型</span><span class="sxs-lookup"><span data-stu-id="77fe4-158">Create a model</span></span>
<span data-ttu-id="77fe4-159">A*模型*是代表您的應用程式中的 hello 資料的物件。</span><span class="sxs-lookup"><span data-stu-id="77fe4-159">A *model* is an object that represents hello data in your application.</span></span> <span data-ttu-id="77fe4-160">Hello 應用程式，hello 僅限模型是工作物件，代表 hello 待辦事項清單中的項目。</span><span class="sxs-lookup"><span data-stu-id="77fe4-160">For hello application, hello only model is a task object, which represents an item in hello to-do list.</span></span> <span data-ttu-id="77fe4-161">工作將會擁有 hello 下列欄位：</span><span class="sxs-lookup"><span data-stu-id="77fe4-161">Tasks will have hello following fields:</span></span>

* <span data-ttu-id="77fe4-162">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="77fe4-162">PartitionKey</span></span>
* <span data-ttu-id="77fe4-163">RowKey</span><span class="sxs-lookup"><span data-stu-id="77fe4-163">RowKey</span></span>
* <span data-ttu-id="77fe4-164">name (字串)</span><span class="sxs-lookup"><span data-stu-id="77fe4-164">name (string)</span></span>
* <span data-ttu-id="77fe4-165">category (字串)</span><span class="sxs-lookup"><span data-stu-id="77fe4-165">category (string)</span></span>
* <span data-ttu-id="77fe4-166">completed (布林值)</span><span class="sxs-lookup"><span data-stu-id="77fe4-166">completed (Boolean)</span></span>

<span data-ttu-id="77fe4-167">**PartitionKey**和**RowKey** hello 表格服務所使用做為資料表的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="77fe4-167">**PartitionKey** and **RowKey** are used by hello Table Service as table keys.</span></span> <span data-ttu-id="77fe4-168">如需詳細資訊，請參閱[了解 hello 表格服務資料模型](https://msdn.microsoft.com/library/azure/dd179338.aspx)。</span><span class="sxs-lookup"><span data-stu-id="77fe4-168">For more information, see [Understanding hello Table Service data model](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

1. <span data-ttu-id="77fe4-169">在 hello **tasklist**目錄中，建立名為的新目錄**模型**。</span><span class="sxs-lookup"><span data-stu-id="77fe4-169">In hello **tasklist** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="77fe4-170">在 hello**模型**目錄中，建立新的檔案命名為**task.js**。</span><span class="sxs-lookup"><span data-stu-id="77fe4-170">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="77fe4-171">這個檔案會包含您的應用程式所建立的 hello 工作 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="77fe4-171">This file will contain hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="77fe4-172">在 hello hello 開頭**task.js**檔案中加入下列程式碼所需的 tooreference 程式庫的 hello:</span><span class="sxs-lookup"><span data-stu-id="77fe4-172">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. <span data-ttu-id="77fe4-173">加入 hello 下列程式碼 toodefine 和匯出 hello 工作物件。</span><span class="sxs-lookup"><span data-stu-id="77fe4-173">Add hello following code toodefine and export hello Task object.</span></span> <span data-ttu-id="77fe4-174">此物件負責連接 toohello 資料表。</span><span class="sxs-lookup"><span data-stu-id="77fe4-174">This object is responsible for connecting toohello table.</span></span>
   
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
5. <span data-ttu-id="77fe4-175">加入 hello hello 工作物件，在下列程式碼 toodefine 其他方法可讓資料儲存在 hello 資料表之間的互動：</span><span class="sxs-lookup"><span data-stu-id="77fe4-175">Add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>
   
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
            // use entityGenerator tooset types
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
6. <span data-ttu-id="77fe4-176">儲存並關閉 hello **task.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="77fe4-176">Save and close hello **task.js** file.</span></span>

### <a name="create-a-controller"></a><span data-ttu-id="77fe4-177">建立控制器</span><span class="sxs-lookup"><span data-stu-id="77fe4-177">Create a controller</span></span>
<span data-ttu-id="77fe4-178">A*控制器*處理 HTTP 要求並呈現 hello HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="77fe4-178">A *controller* handles HTTP requests and renders hello HTML response.</span></span>

1. <span data-ttu-id="77fe4-179">在 hello **tasklist/路由**目錄中，建立新的檔案命名為**tasklist.js**在文字編輯器中開啟它。</span><span class="sxs-lookup"><span data-stu-id="77fe4-179">In hello **tasklist/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="77fe4-180">新增下列程式碼太 hello**tasklist.js**。</span><span class="sxs-lookup"><span data-stu-id="77fe4-180">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="77fe4-181">這會載入 hello azure 與非同步模組所使用的**tasklist.js**。</span><span class="sxs-lookup"><span data-stu-id="77fe4-181">This loads hello azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="77fe4-182">這也會定義 hello **TaskList**函式，會傳遞 hello 的執行個體**工作**我們先前定義的物件：</span><span class="sxs-lookup"><span data-stu-id="77fe4-182">This also defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. <span data-ttu-id="77fe4-183">定義 **TaskList** 物件。</span><span class="sxs-lookup"><span data-stu-id="77fe4-183">Define a **TaskList** object.</span></span>
   
        function TaskList(task) {
          this.task = task;
        }
4. <span data-ttu-id="77fe4-184">新增下列方法太 hello**TaskList**:</span><span class="sxs-lookup"><span data-stu-id="77fe4-184">Add hello following methods too**TaskList**:</span></span>
   
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

### <a name="modify-appjs"></a><span data-ttu-id="77fe4-185">修改 app.js</span><span class="sxs-lookup"><span data-stu-id="77fe4-185">Modify app.js</span></span>
1. <span data-ttu-id="77fe4-186">從 hello **tasklist**目錄，請開啟 hello **app.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="77fe4-186">From hello **tasklist** directory, open hello **app.js** file.</span></span> <span data-ttu-id="77fe4-187">這個檔案稍早建立的執行 hello **express**命令。</span><span class="sxs-lookup"><span data-stu-id="77fe4-187">This file was created earlier by running hello **express** command.</span></span>
2. <span data-ttu-id="77fe4-188">在 hello hello 檔案開頭，加入下列 tooload hello azure 模組、 設定 hello 資料表名稱、 資料分割索引鍵和此範例所使用的設定 hello 儲存體認證的 hello:</span><span class="sxs-lookup"><span data-stu-id="77fe4-188">At hello beginning of hello file, add hello following tooload hello azure module, set hello table name, partition key, and set hello storage credentials used by this example:</span></span>
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > <span data-ttu-id="77fe4-189">nconf 會從環境變數或 hello 載入 hello 組態值**config.json**我們將在稍後建立的檔案。</span><span class="sxs-lookup"><span data-stu-id="77fe4-189">nconf will load hello configuration values from either environment variables or hello **config.json** file, which we will create later.</span></span>
   > 
   > 
3. <span data-ttu-id="77fe4-190">在 hello app.js 檔案中，向下捲動的 toowhere 您會看到下列行 hello:</span><span class="sxs-lookup"><span data-stu-id="77fe4-190">In hello app.js file, scroll down toowhere you see hello following line:</span></span>
   
        app.use('/', routes);
        app.use('/users', users);
   
    <span data-ttu-id="77fe4-191">取代 hello 如下所示的程式碼行上方的 hello。</span><span class="sxs-lookup"><span data-stu-id="77fe4-191">Replace hello above lines with hello code shown below.</span></span> <span data-ttu-id="77fe4-192">這將會初始化的執行個體<strong>工作</strong>連接 tooyour 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="77fe4-192">This will initialize an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="77fe4-193">這會傳遞 toohello <strong>TaskList</strong>，就會使用它 toocommunicate 以 hello 表格服務：</span><span class="sxs-lookup"><span data-stu-id="77fe4-193">This is passed toohello <strong>TaskList</strong>, which will use it toocommunicate with hello Table service:</span></span>
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. <span data-ttu-id="77fe4-194">儲存 hello **app.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="77fe4-194">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="77fe4-195">修改 hello 索引檢視表</span><span class="sxs-lookup"><span data-stu-id="77fe4-195">Modify hello index view</span></span>
1. <span data-ttu-id="77fe4-196">開啟 hello **tasklist/views/index.jade**文字編輯器中的檔案。</span><span class="sxs-lookup"><span data-stu-id="77fe4-196">Open hello **tasklist/views/index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="77fe4-197">取代下列程式碼的 hello hello 整個 hello 檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="77fe4-197">Replace hello entire contents of hello file with hello following code.</span></span> <span data-ttu-id="77fe4-198">這會定義顯示現有工作的檢視，並且包括加入新工作及將現有工作標示為完成的表單。</span><span class="sxs-lookup"><span data-stu-id="77fe4-198">This defines a view that displays existing tasks and includes a form for adding new tasks and marking existing ones as completed.</span></span>
   
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
3. <span data-ttu-id="77fe4-199">儲存並關閉 **index.jade** 檔案。</span><span class="sxs-lookup"><span data-stu-id="77fe4-199">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="77fe4-200">修改 hello 全域版面配置</span><span class="sxs-lookup"><span data-stu-id="77fe4-200">Modify hello global layout</span></span>
<span data-ttu-id="77fe4-201">hello **layout.jade**檔案在 hello**檢視**目錄是全域範本的其他**.jade**檔案。</span><span class="sxs-lookup"><span data-stu-id="77fe4-201">hello **layout.jade** file in hello **views** directory is a global template for other **.jade** files.</span></span> <span data-ttu-id="77fe4-202">在此步驟中您會修改它 toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap)，也就是可讓您輕鬆 toodesign nice 尋找 web 應用程式的工具組。</span><span class="sxs-lookup"><span data-stu-id="77fe4-202">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking web app.</span></span>

<span data-ttu-id="77fe4-203">下載並解壓縮 hello 檔案[Twitter Bootstrap](http://getbootstrap.com/)。</span><span class="sxs-lookup"><span data-stu-id="77fe4-203">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="77fe4-204">複製 hello **bootstrap.min.css** hello 啟動程序從檔案**css**資料夾 hello**公用/樣式表**應用程式的目錄。</span><span class="sxs-lookup"><span data-stu-id="77fe4-204">Copy hello **bootstrap.min.css** file from hello Bootstrap **css** folder into hello **public/stylesheets** directory of your application.</span></span>

<span data-ttu-id="77fe4-205">從 hello**檢視**資料夾中，開啟**layout.jade**並取代 hello 下列中的 hello 整個內容：</span><span class="sxs-lookup"><span data-stu-id="77fe4-205">From hello **views** folder, open **layout.jade** and replace hello entire contents with hello following:</span></span>

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

### <a name="create-a-config-file"></a><span data-ttu-id="77fe4-206">建立組態檔</span><span class="sxs-lookup"><span data-stu-id="77fe4-206">Create a config file</span></span>
<span data-ttu-id="77fe4-207">toorun hello 應用程式在本機，我們會將 Azure 儲存體認證放在組態檔。</span><span class="sxs-lookup"><span data-stu-id="77fe4-207">toorun hello app locally, we'll put Azure Storage credentials into a config file.</span></span> <span data-ttu-id="77fe4-208">建立名為 **config.json* * 以下列 JSON hello:</span><span class="sxs-lookup"><span data-stu-id="77fe4-208">Create a file named **config.json* *with hello following JSON:</span></span>

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="77fe4-209">取代**儲存體帳戶名稱**hello hello 儲存體名稱與您稍早建立帳戶，並取代**儲存體存取金鑰**與 hello 儲存體帳戶的主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="77fe4-209">Replace **storage account name** with hello name of hello storage account you created earlier, and replace **storage access key** with hello primary access key for your storage account.</span></span> <span data-ttu-id="77fe4-210">例如：</span><span class="sxs-lookup"><span data-stu-id="77fe4-210">For example:</span></span>

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="77fe4-211">儲存這個檔案*一個目錄層級較高*比 hello **tasklist**目錄下，像這樣：</span><span class="sxs-lookup"><span data-stu-id="77fe4-211">Save this file *one directory level higher* than hello **tasklist** directory, like this:</span></span>

    parent/
      |-- config.json
      |-- tasklist/

<span data-ttu-id="77fe4-212">執行此作業的 hello 原因是 tooavoid 簽入原始檔控制 hello 組態檔位置可能會變成公用。</span><span class="sxs-lookup"><span data-stu-id="77fe4-212">hello reason for doing this is tooavoid checking hello config file into source control, where it might become public.</span></span> <span data-ttu-id="77fe4-213">當我們將部署 hello 應用程式 tooAzure 時，我們將使用環境變數，而不是在組態檔。</span><span class="sxs-lookup"><span data-stu-id="77fe4-213">When we deploy hello app tooAzure, we will use environment variables instead of a config file.</span></span>

## <a name="run-hello-application-locally"></a><span data-ttu-id="77fe4-214">在本機執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="77fe4-214">Run hello application locally</span></span>
<span data-ttu-id="77fe4-215">tootest hello 應用程式在本機電腦，執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="77fe4-215">tootest hello application on your local machine, perform hello following steps:</span></span>

1. <span data-ttu-id="77fe4-216">從命令列的 hello，變更目錄 toohello **tasklist**目錄。</span><span class="sxs-lookup"><span data-stu-id="77fe4-216">From hello command-line, change directories toohello **tasklist** directory.</span></span>
2. <span data-ttu-id="77fe4-217">使用下列命令 toolaunch hello 本機應用程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="77fe4-217">Use hello following command toolaunch hello application locally:</span></span>
   
        npm start
3. <span data-ttu-id="77fe4-218">開啟網頁瀏覽器並瀏覽 toohttp://127.0.0.1:3000。</span><span class="sxs-lookup"><span data-stu-id="77fe4-218">Open a web browser and navigate toohttp://127.0.0.1:3000.</span></span>
   
    <span data-ttu-id="77fe4-219">下列範例網頁類似 toohello 隨即出現。</span><span class="sxs-lookup"><span data-stu-id="77fe4-219">A web page similar toohello following example appears.</span></span>
   
    ![A webpage displaying an empty tasklist][node-table-finished]
4. <span data-ttu-id="77fe4-221">toocreate 新的待辦項目中，輸入名稱和類別目錄，然後按一下**加入項目**。</span><span class="sxs-lookup"><span data-stu-id="77fe4-221">toocreate a new to-do item, enter a name and category and click **Add Item**.</span></span> 
5. <span data-ttu-id="77fe4-222">工作完成時，請檢查 toomark**完成**按一下**更新工作**。</span><span class="sxs-lookup"><span data-stu-id="77fe4-222">toomark a task as complete, check **Complete** and click **Update Tasks**.</span></span>
   
    ![項目的影像 hello 新 hello 清單中的工作][node-table-list-items]

<span data-ttu-id="77fe4-224">即使在本機執行 hello 應用程式，它會儲存 hello 資料 hello Azure 表格服務中。</span><span class="sxs-lookup"><span data-stu-id="77fe4-224">Even though hello application is running locally, it is storing hello data in hello Azure Table service.</span></span>

## <a name="deploy-your-application-tooazure"></a><span data-ttu-id="77fe4-225">部署應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="77fe4-225">Deploy your application tooAzure</span></span>
<span data-ttu-id="77fe4-226">本節中的 hello 步驟使用 App Service 中的 hello Azure 命令列工具 toocreate 新的 web 應用程式，然後再使用 Git toodeploy 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="77fe4-226">hello steps in this section use hello Azure command-line tools toocreate a new web app in App Service, and then use Git toodeploy your application.</span></span> <span data-ttu-id="77fe4-227">tooperform 這些步驟，您必須具有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="77fe4-227">tooperform these steps you must have an Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="77fe4-228">也可以使用 hello 執行這些步驟[Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="77fe4-228">These steps can also be performed by using hello [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="77fe4-229">請參閱 [在 Azure App Service 中建置和部署 Node.js Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="77fe4-229">See [Build and deploy a Node.js web app in Azure App Service].</span></span>
> 
> <span data-ttu-id="77fe4-230">如果這是您已建立 hello 第一個 web 應用程式，您必須使用 hello Azure 入口網站 toodeploy 此應用程式。</span><span class="sxs-lookup"><span data-stu-id="77fe4-230">If this is hello first web app you have created, you must use hello Azure Portal toodeploy this application.</span></span>
> 
> 

<span data-ttu-id="77fe4-231">tooget 啟動，安裝 hello [Azure CLI]輸入 hello hello 命令列中的下列命令：</span><span class="sxs-lookup"><span data-stu-id="77fe4-231">tooget started, install hello [Azure CLI] by entering hello following command from hello command line:</span></span>

    npm install azure-cli -g

### <a name="import-publishing-settings"></a><span data-ttu-id="77fe4-232">匯入發佈設定</span><span class="sxs-lookup"><span data-stu-id="77fe4-232">Import publishing settings</span></span>
<span data-ttu-id="77fe4-233">在此步驟中，您將會下載包含您訂用帳戶相關資訊的檔案。</span><span class="sxs-lookup"><span data-stu-id="77fe4-233">In this step, you will download a file containing information about your subscription.</span></span>

1. <span data-ttu-id="77fe4-234">輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="77fe4-234">Enter hello following command:</span></span>
   
        azure login
   
    <span data-ttu-id="77fe4-235">此命令會啟動瀏覽器並瀏覽 toohello 下載頁面。</span><span class="sxs-lookup"><span data-stu-id="77fe4-235">This command launches a browser and navigates toohello download page.</span></span> <span data-ttu-id="77fe4-236">如果出現提示，請登入與您 Azure 訂用帳戶相關聯的 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="77fe4-236">If prompted, log in with hello account associated with your Azure subscription.</span></span>
   
    <!-- ![hello download page][download-publishing-settings] -->
   
    <span data-ttu-id="77fe4-237">hello 檔案下載，而開始如果不存在，您可以按一下 hello hello hello 頁面 toomanually 下載 hello 檔案開頭處的連結。</span><span class="sxs-lookup"><span data-stu-id="77fe4-237">hello file download begins automatically; if it does not, you can click hello link at hello beginning of hello page toomanually download hello file.</span></span> <span data-ttu-id="77fe4-238">儲存 hello 檔案並註記 hello 檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="77fe4-238">Save hello file and note hello file path.</span></span>
2. <span data-ttu-id="77fe4-239">輸入下列命令 tooimport hello 設定 hello:</span><span class="sxs-lookup"><span data-stu-id="77fe4-239">Enter hello following command tooimport hello settings:</span></span>
   
        azure account import <path-to-file>
   
    <span data-ttu-id="77fe4-240">指定 hello hello hello 上一個步驟中發佈您下載的設定檔的路徑和檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="77fe4-240">Specify hello path and file name of hello publishing settings file you downloaded in hello previous step.</span></span>
3. <span data-ttu-id="77fe4-241">匯入 hello 設定之後，刪除 hello 的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="77fe4-241">After hello settings are imported, delete hello publish settings file.</span></span> <span data-ttu-id="77fe4-242">這個檔案已經不再需要，而且包含與 Azure 訂用帳戶相關的機密資訊。</span><span class="sxs-lookup"><span data-stu-id="77fe4-242">It is no longer needed, and contains sensitive information regarding your Azure subscription.</span></span>

### <a name="create-an-app-service-web-app"></a><span data-ttu-id="77fe4-243">建立 App Service Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="77fe4-243">Create an App Service web app</span></span>
1. <span data-ttu-id="77fe4-244">從命令列的 hello，變更目錄 toohello **tasklist**目錄。</span><span class="sxs-lookup"><span data-stu-id="77fe4-244">From hello command-line, change directories toohello **tasklist** directory.</span></span>
2. <span data-ttu-id="77fe4-245">使用下列命令 toocreate 新的 web 應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="77fe4-245">Use hello following command toocreate a new web app.</span></span>
   
        azure site create --git
   
    <span data-ttu-id="77fe4-246">系統會提示您 hello web 應用程式名稱和位置。</span><span class="sxs-lookup"><span data-stu-id="77fe4-246">You will be prompted for hello web app name and location.</span></span> <span data-ttu-id="77fe4-247">提供唯一的名稱，然後選取 hello 與 Azure 儲存體帳戶相同的地理位置。</span><span class="sxs-lookup"><span data-stu-id="77fe4-247">Provide a unique name and select hello same geographical location as your Azure Storage account.</span></span>
   
    <span data-ttu-id="77fe4-248">hello`--git`參數在 Azure 上建立 Git 儲存機制，此 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="77fe4-248">hello `--git` parameter creates a Git repository on Azure for this web app.</span></span> <span data-ttu-id="77fe4-249">它也會初始化 hello 目前目錄中的 Git 儲存機制有無存在，以及新增[Git 遠端]名為 'azure'，這是使用的 toopublish hello 應用程式 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="77fe4-249">It also initializes a Git repository in hello current directory if none exists, and adds a [Git remote] named 'azure', which is used toopublish hello application tooAzure.</span></span> <span data-ttu-id="77fe4-250">最後，它會建立**web.config**檔案，其中包含 Azure toohost 節點應用程式所使用的設定。</span><span class="sxs-lookup"><span data-stu-id="77fe4-250">Finally, it creates a **web.config** file, which contains settings used by Azure toohost node applications.</span></span> <span data-ttu-id="77fe4-251">如果您省略 hello`--git`參數，但 hello 目錄中包含的 Git 儲存機制、 hello 命令仍會建立 'azure' hello 遠端。</span><span class="sxs-lookup"><span data-stu-id="77fe4-251">If you omit hello `--git` parameter but hello directory contains a Git repository, hello command will still create hello 'azure' remote.</span></span>
   
    <span data-ttu-id="77fe4-252">此命令完成後，您會看到類似 toohello 下列輸出。</span><span class="sxs-lookup"><span data-stu-id="77fe4-252">Once this command has completed, you will see output similar toohello following.</span></span> <span data-ttu-id="77fe4-253">請注意該 hello 行首**網站端建立**包含 hello hello web 應用程式的 URL。</span><span class="sxs-lookup"><span data-stu-id="77fe4-253">Note that hello line beginning with **Website created at** contains hello URL for hello web app.</span></span>
   
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
   > <span data-ttu-id="77fe4-254">如果這是 hello 第一個 App Service web 應用程式為您的訂用帳戶，您將會指示 toouse hello Azure 入口網站 toocreate hello web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="77fe4-254">If this is hello first App Service web app for your subscription, you will be instructed toouse hello Azure Portal toocreate hello web app.</span></span> <span data-ttu-id="77fe4-255">如需詳細資訊，請參閱 [在 Azure App Service 中建置和部署 Node.js Web 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="77fe4-255">For more information, see [Build and deploy a Node.js web app in Azure App Service].</span></span>
   > 
   > 

### <a name="set-environment-variables"></a><span data-ttu-id="77fe4-256">設定環境變數</span><span class="sxs-lookup"><span data-stu-id="77fe4-256">Set environment variables</span></span>
<span data-ttu-id="77fe4-257">在此步驟中，您將加入在 Azure 上的環境變數 tooyour web 應用程式組態。</span><span class="sxs-lookup"><span data-stu-id="77fe4-257">In this step, you will add environment variables tooyour web app configuration on Azure.</span></span>
<span data-ttu-id="77fe4-258">從 hello 命令列中，輸入 hello 下列內容：</span><span class="sxs-lookup"><span data-stu-id="77fe4-258">From hello command line, enter hello following:</span></span>

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


<span data-ttu-id="77fe4-259">取代 **<storage account name>**  hello hello 儲存體名稱與您稍早建立帳戶，並取代 **<storage access key>** 與 hello 儲存體帳戶的主要存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="77fe4-259">Replace **<storage account name>** with hello name of hello storage account you created earlier, and replace **<storage access key>** with hello primary access key for your storage account.</span></span> <span data-ttu-id="77fe4-260">（您稍早建立的 hello config.json 檔案使用相同值的 hello）。</span><span class="sxs-lookup"><span data-stu-id="77fe4-260">(Use hello same values as hello config.json file that you created earlier.)</span></span>

<span data-ttu-id="77fe4-261">或者，您可以設定環境變數中 hello [Azure 入口網站](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="77fe4-261">Alternatively, you can set environment variables in hello [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="77fe4-262">開啟 hello web 應用程式的刀鋒視窗中，依序按一下**瀏覽** > **Web 應用程式**> web 應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="77fe4-262">Open hello web app's blade by clicking **Browse** > **Web Apps** > your web app name.</span></span>
2. <span data-ttu-id="77fe4-263">在您的 Web 應用程式刀鋒視窗中，按一下 [所有設定]  >  [應用程式設定]。</span><span class="sxs-lookup"><span data-stu-id="77fe4-263">In your web app's blade, click **All Settings** > **Application Settings**.</span></span>
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. <span data-ttu-id="77fe4-264">捲動 toohello**應用程式設定**區段，並新增 hello 索引鍵/值組。</span><span class="sxs-lookup"><span data-stu-id="77fe4-264">Scroll down toohello **App settings** section and add hello key/value pairs.</span></span>
   
     ![應用程式設定](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. <span data-ttu-id="77fe4-266">按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="77fe4-266">Click **SAVE**.</span></span>

### <a name="publish-hello-application"></a><span data-ttu-id="77fe4-267">發行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="77fe4-267">Publish hello application</span></span>
<span data-ttu-id="77fe4-268">toopublish hello 應用程式時，認可 hello 程式碼檔案 tooGit，並接著推送 tooazure/master。</span><span class="sxs-lookup"><span data-stu-id="77fe4-268">toopublish hello app, commit hello code files tooGit and then push tooazure/master.</span></span>

1. <span data-ttu-id="77fe4-269">設定您的部署認證。</span><span class="sxs-lookup"><span data-stu-id="77fe4-269">Set your deployment credentials.</span></span>
   
        azure site deployment user set <name> <password>
2. <span data-ttu-id="77fe4-270">新增並認可您的應用程式檔案。</span><span class="sxs-lookup"><span data-stu-id="77fe4-270">Add and commit your application files.</span></span>
   
        git add .
        git commit -m "adding files"
3. <span data-ttu-id="77fe4-271">推送 hello 認可 toohello App Service web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="77fe4-271">Push hello commit toohello App Service web app:</span></span>
   
        git push azure master
   
    <span data-ttu-id="77fe4-272">使用**主要**為 hello 目標分支。</span><span class="sxs-lookup"><span data-stu-id="77fe4-272">Use **master** as hello target branch.</span></span> <span data-ttu-id="77fe4-273">在 hello 部署的 hello 結束時，您會看到陳述式的類似 toohello，下列範例：</span><span class="sxs-lookup"><span data-stu-id="77fe4-273">At hello end of hello deployment, you see a statement similar toohello following example:</span></span>
   
        toohttps://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. <span data-ttu-id="77fe4-274">Hello 推入作業完成後，請瀏覽先前由 hello toohello web 應用程式 URL`azure create site`命令 tooview 您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="77fe4-274">Once hello push operation has completed, browse toohello web app URL returned previously by hello `azure create site` command tooview your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77fe4-275">後續步驟</span><span class="sxs-lookup"><span data-stu-id="77fe4-275">Next steps</span></span>
<span data-ttu-id="77fe4-276">雖然這篇文章中的 hello 步驟說明使用 hello 表格服務 toostore 資訊，您也可以使用[MongoDB](https://mlab.com/azure/)。</span><span class="sxs-lookup"><span data-stu-id="77fe4-276">While hello steps in this article describe using hello Table Service toostore information, you can also use [MongoDB](https://mlab.com/azure/).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="77fe4-277">其他資源</span><span class="sxs-lookup"><span data-stu-id="77fe4-277">Additional resources</span></span>
<span data-ttu-id="77fe4-278">[Azure CLI]</span><span class="sxs-lookup"><span data-stu-id="77fe4-278">[Azure CLI]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="77fe4-279">變更的項目</span><span class="sxs-lookup"><span data-stu-id="77fe4-279">What's changed</span></span>
* <span data-ttu-id="77fe4-280">從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="77fe4-280">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- URLs -->

[在 Azure App Service 中建置和部署 Node.js Web 應用程式]: app-service-web-get-started-nodejs.md
[Azure Developer Center]: /develop/nodejs/

[節點]: http://nodejs.org
[Git]: http://git-scm.com
[Express]: http://expressjs.com
[for free]: http://windowsazure.com
[Git 遠端]: http://git-scm.com/docs/git-remote

[Azure CLI]:../cli-install-nodejs.md

[azure]: https://github.com/Azure/azure-sdk-for-node
[節點 uuid]: https://www.npmjs.com/package/node-uuid
[nconf]: https://www.npmjs.com/package/nconf
[非同步]: https://www.npmjs.com/package/async

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application tooan Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
