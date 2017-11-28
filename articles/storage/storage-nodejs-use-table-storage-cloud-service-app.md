---
title: "使用資料表儲存體的 Web 應用程式 (Node.js) | Microsoft Docs"
description: "本教學課程以「使用 Express 的 Web 應用程式」教學課程為基礎，再加上 Azure 儲存體服務和 Azure 模組建置而成。"
services: cloud-services, storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e90959a2-4cb2-4b19-9bfb-aede15b18b1c
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 5d7ee2f529b5127ee60ec8b4f5acaa49e75ddf39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="db09e-103">使用儲存體的 Node.js Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="db09e-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="db09e-104">概觀</span><span class="sxs-lookup"><span data-stu-id="db09e-104">Overview</span></span>
<span data-ttu-id="db09e-105">在本教學課程中，您將擴充在[使用 Express 的 Node.js Web 應用程式]教學課程中所建立的應用程式，方法是使用 Microsoft Azure Client Libraries for Node.js 來搭配資料管理服務使用。</span><span class="sxs-lookup"><span data-stu-id="db09e-105">In this tutorial, you will extend the application created in the [Node.js Web Application using Express] tutorial by using the Microsoft Azure Client Libraries for Node.js to work with data management services.</span></span> <span data-ttu-id="db09e-106">您將擴充您的應用程式，以建立一個可部署到 Azure 的 Web 架構工作清單應用程式。</span><span class="sxs-lookup"><span data-stu-id="db09e-106">You will extend your application to create a web-based task-list application that you can deploy to Azure.</span></span> <span data-ttu-id="db09e-107">使用者可透過工作清單來擷取工作、新增工作及將工作標示為已完成。</span><span class="sxs-lookup"><span data-stu-id="db09e-107">The task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="db09e-108">工作項目會儲存於 Azure 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="db09e-108">The task items are stored in Azure Storage.</span></span> <span data-ttu-id="db09e-109">Azure 儲存體提供可容錯且高度可用的非結構化資料儲存體。</span><span class="sxs-lookup"><span data-stu-id="db09e-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="db09e-110">Azure 儲存體包括數種可儲存和存取資料的資料結構，並且您可以從 Azure SDK for Node.js 中所隨附的 API 或透過 REST API 來運用儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="db09e-110">Azure Storage includes several data structures where you can store and access data, and you can leverage the storage services from the APIs included in the Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="db09e-111">如需詳細資訊，請參閱[在 Azure 中儲存和存取資料]。</span><span class="sxs-lookup"><span data-stu-id="db09e-111">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="db09e-112">本教學課程假設您已完成 [Node.js Web 應用程式]和[使用 Express 的 Node.js][使用 Express 的 Node.js Web 應用程式]教學課程。</span><span class="sxs-lookup"><span data-stu-id="db09e-112">This tutorial assumes that you have completed the [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="db09e-113">您將了解：</span><span class="sxs-lookup"><span data-stu-id="db09e-113">You will learn:</span></span>

* <span data-ttu-id="db09e-114">如何使用 Jade 範本引擎</span><span class="sxs-lookup"><span data-stu-id="db09e-114">How to work with the Jade template engine</span></span>
* <span data-ttu-id="db09e-115">如何使用 Azure 資料管理服務</span><span class="sxs-lookup"><span data-stu-id="db09e-115">How to work with Azure Data Management services</span></span>

<span data-ttu-id="db09e-116">完成之應用程式的螢幕擷取畫面如下：</span><span class="sxs-lookup"><span data-stu-id="db09e-116">A screenshot of the completed application is below:</span></span>

![The completed web page in internet explorer](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="db09e-118">在 Web.Config 中設定儲存體認證</span><span class="sxs-lookup"><span data-stu-id="db09e-118">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="db09e-119">若要存取 Azure 儲存體，您必須傳入儲存體認證。</span><span class="sxs-lookup"><span data-stu-id="db09e-119">To access Azure Storage, you need to pass in storage credentials.</span></span> <span data-ttu-id="db09e-120">若要這樣做，您必須使用 web.config 應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="db09e-120">To do this, you utilize web.config application settings.</span></span>
<span data-ttu-id="db09e-121">這些設定會以環境變數方式傳遞至 Node，接著再由 Azure SDK 進行讀取。</span><span class="sxs-lookup"><span data-stu-id="db09e-121">Those settings will be passed as environment variables to Node, which are then read by the Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="db09e-122">只有當將應用程式部署到 Azure 時，才會用到儲存體認證。</span><span class="sxs-lookup"><span data-stu-id="db09e-122">Storage credentials are only used when the application is deployed to Azure.</span></span> <span data-ttu-id="db09e-123">在模擬器中執行時，應用程式將使用儲存體模擬器。</span><span class="sxs-lookup"><span data-stu-id="db09e-123">When running in the emulator, the application will use the storage emulator.</span></span>
>
>

<span data-ttu-id="db09e-124">執行下列步驟以擷取儲存體帳戶認證，並將他們新增至 web.config 設定：</span><span class="sxs-lookup"><span data-stu-id="db09e-124">Perform the following steps to retrieve the storage account credentials and add them to the web.config settings:</span></span>

1. <span data-ttu-id="db09e-125">從 [開始] 功能表中啟動 Azure PowerShell (如果尚未開啟的話)，方法是依序展開 [所有程式]、[Azure]，以滑鼠右鍵按一下 [Azure PowerShell]，然後選取 [以系統管理員身份執行]。</span><span class="sxs-lookup"><span data-stu-id="db09e-125">If it is not already open, start the Azure PowerShell from the **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="db09e-126">將目錄變更到包含應用程式的資料夾。</span><span class="sxs-lookup"><span data-stu-id="db09e-126">Change directories to the folder containing your application.</span></span> <span data-ttu-id="db09e-127">例如，C:\\node\\tasklist\\WebRole1。</span><span class="sxs-lookup"><span data-stu-id="db09e-127">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="db09e-128">在 [Azure Powershell] 視窗中，輸入下列 Cmdlet 以擷取儲存體帳戶資訊：</span><span class="sxs-lookup"><span data-stu-id="db09e-128">From the Azure Powershell window enter the following cmdlet to retrieve the storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="db09e-129">這會擷取與託管服務相關的儲存體帳戶和帳戶金鑰清單。</span><span class="sxs-lookup"><span data-stu-id="db09e-129">This retrieves the list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="db09e-130">由於 Azure SDK 會在您部署服務時建立儲存體帳戶，因此，從上一個說明的部署應用程式中應已有儲存體帳戶存在。</span><span class="sxs-lookup"><span data-stu-id="db09e-130">Since the Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in the previous guides.</span></span>
   >
   >
4. <span data-ttu-id="db09e-131">開啟包含環境設定 (將應用程式部署到 Azure 時會用到) 的 **ServiceDefinition.csdef** 檔案：</span><span class="sxs-lookup"><span data-stu-id="db09e-131">Open the **ServiceDefinition.csdef** file containing the environment settings that are used when the application is deployed to Azure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="db09e-132">將下列區塊插入 **Environment** 元素下方，以您要用於部署之儲存體帳戶的帳戶名稱和主要金鑰取代 {儲存體帳戶} 和 {儲存體存取金鑰}：</span><span class="sxs-lookup"><span data-stu-id="db09e-132">Insert the following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with the account name and the primary key for the storage account you want to use for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![web.cloud.config 檔案內容](./media/storage-nodejs-use-table-storage-cloud-service-app/node37.png)

6. <span data-ttu-id="db09e-134">儲存檔案並關閉記事本。</span><span class="sxs-lookup"><span data-stu-id="db09e-134">Save the file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="db09e-135">安裝其他模組</span><span class="sxs-lookup"><span data-stu-id="db09e-135">Install additional modules</span></span>
1. <span data-ttu-id="db09e-136">使用下列命令在本機安裝 [azure]、[node-uuid]、[nconf] 及 [async] 模組，以及將它們的項目儲存至 **package.json** 檔案：</span><span class="sxs-lookup"><span data-stu-id="db09e-136">Use the following command to install the [azure], [node-uuid], [nconf] and [async] modules locally as well as to save an entry for them to the **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="db09e-137">此命令的輸出應類似這樣：</span><span class="sxs-lookup"><span data-stu-id="db09e-137">The output of this command should appear similar to the following:</span></span>

  ```
  node-uuid@1.4.1 node_modules\node-uuid

  nconf@0.6.9 node_modules\nconf
  ├── ini@1.1.0
  ├── async@0.2.9
  └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.8)

  azure-storage@0.1.0 node_modules\azure-storage
  ├── extend@1.2.1
  ├── xmlbuilder@0.4.3
  ├── mime@1.2.11
  ├── underscore@1.4.4
  ├── validator@3.1.0
  ├── node-uuid@1.4.1
  ├── xml2js@0.2.7 (sax@0.5.2)
  └── request@2.27.0 (json-stringify-safe@5.0.0, tunnel-agent@0.3.0, aws-sign@0.3.0, forever-agent@0.5.2, qs@0.6.6, oauth-sign@0.3.0, cookie-jar@0.3.0, hawk@1.0.0, form-data@0.1.3, http-signature@0.10.0)
  ```

## <a name="using-the-table-service-in-a-node-application"></a><span data-ttu-id="db09e-138">在節點應用程式中使用資料表服務</span><span class="sxs-lookup"><span data-stu-id="db09e-138">Using the Table service in a node application</span></span>
<span data-ttu-id="db09e-139">在本節中，您將藉著新增 **task.js** 檔案的方式擴充由 **express** 命令建立的基本應用程式 (task.js 檔案包含工作的模型)。</span><span class="sxs-lookup"><span data-stu-id="db09e-139">In this section you will extend the basic application created by the **express** command by adding a **task.js** file which contains the model for your tasks.</span></span> <span data-ttu-id="db09e-140">您也將修改現有 **app.js** 及建立新的 **tasklist.js** 檔案，以使用模型。</span><span class="sxs-lookup"><span data-stu-id="db09e-140">You will also modify the existing **app.js** and create a new **tasklist.js** file that uses the model.</span></span>

### <a name="create-the-model"></a><span data-ttu-id="db09e-141">建立模型</span><span class="sxs-lookup"><span data-stu-id="db09e-141">Create the model</span></span>
1. <span data-ttu-id="db09e-142">在 **WebRole1** 目錄中，建立新目錄 **models**。</span><span class="sxs-lookup"><span data-stu-id="db09e-142">In the **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="db09e-143">在 **models** 目錄中，建立新檔案 **task.js**。</span><span class="sxs-lookup"><span data-stu-id="db09e-143">In the **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="db09e-144">此檔案將包含您的應用程式建立之工作的模型。</span><span class="sxs-lookup"><span data-stu-id="db09e-144">This file will contain the model for the tasks created by your application.</span></span>
3. <span data-ttu-id="db09e-145">在 **task.js** 檔案的開頭加入以下程式碼以參考所需的程式庫：</span><span class="sxs-lookup"><span data-stu-id="db09e-145">At the beginning of the **task.js** file, add the following code to reference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="db09e-146">接下來，要加入程式碼以定義和匯出 Task 物件。</span><span class="sxs-lookup"><span data-stu-id="db09e-146">Next, you will add code to define and export the Task object.</span></span> <span data-ttu-id="db09e-147">此物件負責連接至資料表。</span><span class="sxs-lookup"><span data-stu-id="db09e-147">This object is responsible for connecting to the table.</span></span>

    ```nodejs
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
    ```

5. <span data-ttu-id="db09e-148">接下來，新增下列程式碼以定義 Task 物件上的其他方法，允許與資料表中存放的資料互動：</span><span class="sxs-lookup"><span data-stu-id="db09e-148">Next, add the following code to define additional methods on the Task object, which allow interactions with data stored in the table:</span></span>

    ```nodejs
    Task.prototype = {
      find: function(query, callback) {
        self = this;
        self.storageClient.queryEntities(query, function entitiesQueried(error, result) {
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
    ```

6. <span data-ttu-id="db09e-149">儲存並關閉 **task.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="db09e-149">Save and close the **task.js** file.</span></span>

### <a name="create-the-controller"></a><span data-ttu-id="db09e-150">建立控制器</span><span class="sxs-lookup"><span data-stu-id="db09e-150">Create the controller</span></span>
1. <span data-ttu-id="db09e-151">在 **WebRole1/routes** 目錄中建立新檔案 **tasklist.js**，然後在文字編輯器中開啟檔案。</span><span class="sxs-lookup"><span data-stu-id="db09e-151">In the **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="db09e-152">在 **tasklist.js**中加入以下程式碼。</span><span class="sxs-lookup"><span data-stu-id="db09e-152">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="db09e-153">這會載入 azure 和 async 模組，它們是由 **tasklist.js**所使用。</span><span class="sxs-lookup"><span data-stu-id="db09e-153">This loads the azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="db09e-154">這也會定義 **TaskList** 函式，系統會傳遞我們稍早定義的 **Task** 物件執行個體給它：</span><span class="sxs-lookup"><span data-stu-id="db09e-154">This also defines the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="db09e-155">繼續在 **tasklist.js** 檔案中新增用來 **showTasks (顯示工作)**、**addTask (新增工作)** 和 **completeTasks (完成工作)** 的方法：</span><span class="sxs-lookup"><span data-stu-id="db09e-155">Continue adding to the **tasklist.js** file by adding the methods used to **showTasks**, **addTask**, and **completeTasks**:</span></span>

    ```nodejs
    TaskList.prototype = {
      showTasks: function(req, res) {
        self = this;
        var query = azure.TableQuery()
          .where('completed eq ?', false);
        self.task.find(query, function itemsFound(error, items) {
          res.render('index',{title: 'My ToDo List ', tasks: items});
        });
      },

      addTask: function(req,res) {
        var self = this
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
    ```

4. <span data-ttu-id="db09e-156">儲存 **tasklist.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="db09e-156">Save the **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="db09e-157">修改 app.js</span><span class="sxs-lookup"><span data-stu-id="db09e-157">Modify app.js</span></span>
1. <span data-ttu-id="db09e-158">在 **WebRole1** 目錄中，在文字編輯器中開啟 **app.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="db09e-158">In the **WebRole1** directory, open the **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="db09e-159">在檔案開頭，加入下列內容以載入 azure 模組，以及設定資料表名稱和資料分割索引鍵：</span><span class="sxs-lookup"><span data-stu-id="db09e-159">At the beginning of the file, add the following to load the azure module and set the table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="db09e-160">在 app.js 檔中，向下捲動到看見此行處：</span><span class="sxs-lookup"><span data-stu-id="db09e-160">In the app.js file, scroll down to where you see the following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="db09e-161">將以上幾行取代為以下顯示的程式碼。</span><span class="sxs-lookup"><span data-stu-id="db09e-161">Replace the above lines with the code shown below.</span></span> <span data-ttu-id="db09e-162">這會初始化 <strong>Task</strong> 的執行個體，並連接到您的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="db09e-162">This will initialize an instance of <strong>Task</strong> with a connection to your storage account.</span></span> <span data-ttu-id="db09e-163">這會傳遞給 <strong>TaskList</strong>，它將用來與表格服務通訊：</span><span class="sxs-lookup"><span data-stu-id="db09e-163">This is passed to the <strong>TaskList</strong>, which will use it to communicate with the Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="db09e-164">儲存 **app.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="db09e-164">Save the **app.js** file.</span></span>

### <a name="modify-the-index-view"></a><span data-ttu-id="db09e-165">修改索引檢視</span><span class="sxs-lookup"><span data-stu-id="db09e-165">Modify the index view</span></span>
1. <span data-ttu-id="db09e-166">將目錄變更為 **views** 目錄，在文字編輯器中開啟 **index.jade** 檔案。</span><span class="sxs-lookup"><span data-stu-id="db09e-166">Change directories to the **views** directory and open the **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="db09e-167">以下列程式碼取代 **index.jade** 檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="db09e-167">Replace the contents of the **index.jade** file with the code below.</span></span> <span data-ttu-id="db09e-168">這會定義用於顯示現有工作的檢視，以及用於加入新工作及將現有工作標示為完成的表單。</span><span class="sxs-lookup"><span data-stu-id="db09e-168">This defines the view for displaying existing tasks, as well as a form for adding new tasks and marking existing ones as completed.</span></span>

    ```
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
          if tasks != []
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
    ```

3. <span data-ttu-id="db09e-169">儲存並關閉 **index.jade** 檔案。</span><span class="sxs-lookup"><span data-stu-id="db09e-169">Save and close **index.jade** file.</span></span>

### <a name="modify-the-global-layout"></a><span data-ttu-id="db09e-170">修改全域版面配置</span><span class="sxs-lookup"><span data-stu-id="db09e-170">Modify the global layout</span></span>
<span data-ttu-id="db09e-171">**views** 目錄中的 **layout.jade** 檔是用來作為其他 **.jade** 檔案的全域範本。</span><span class="sxs-lookup"><span data-stu-id="db09e-171">The **layout.jade** file in the **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="db09e-172">在此步驟中，您將修改它以使用 [Twitter Bootstrap](https://github.com/twbs/bootstrap)，這個工具組能夠方便設計美觀的網站。</span><span class="sxs-lookup"><span data-stu-id="db09e-172">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking website.</span></span>

1. <span data-ttu-id="db09e-173">下載並解壓縮 [Twitter Bootstrap](http://getbootstrap.com/)的檔案。</span><span class="sxs-lookup"><span data-stu-id="db09e-173">Download and extract the files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="db09e-174">將 **bootstrap.min.css** 檔案從 **bootstrap\\dist\\css** 資料夾複製到您工作清單應用程式的 **public\\stylesheets** 目錄。</span><span class="sxs-lookup"><span data-stu-id="db09e-174">Copy the **bootstrap.min.css** file from the **bootstrap\\dist\\css** folder to the **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="db09e-175">從 **views** 資料夾，以文字編輯器開啟 **layout.jade**，並將內容取代為：</span><span class="sxs-lookup"><span data-stu-id="db09e-175">From the **views** folder, open the **layout.jade** in your text editor and replace the contents with the following:</span></span>

    <span data-ttu-id="db09e-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span><span class="sxs-lookup"><span data-stu-id="db09e-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="db09e-177">儲存 **layout.jade** 檔案。</span><span class="sxs-lookup"><span data-stu-id="db09e-177">Save the **layout.jade** file.</span></span>

### <a name="running-the-application-in-the-emulator"></a><span data-ttu-id="db09e-178">在模擬器中執行應用程式</span><span class="sxs-lookup"><span data-stu-id="db09e-178">Running the Application in the Emulator</span></span>
<span data-ttu-id="db09e-179">使用下列命令在模擬器中啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="db09e-179">Use the following command to start the application in the emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="db09e-180">瀏覽器會開啟並顯示下列頁面：</span><span class="sxs-lookup"><span data-stu-id="db09e-180">The browser will open and displays the following page:</span></span>

![A web paged titled My Task List with a table containing tasks and fields to add a new task.](./media/storage-nodejs-use-table-storage-cloud-service-app/node44.png)

<span data-ttu-id="db09e-182">使用表單新增項目，或將現有的項目標示為已完成以移除它們。</span><span class="sxs-lookup"><span data-stu-id="db09e-182">Use the form to add items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-the-application-to-azure"></a><span data-ttu-id="db09e-183">將應用程式發行至 Azure</span><span class="sxs-lookup"><span data-stu-id="db09e-183">Publishing the Application to Azure</span></span>
<span data-ttu-id="db09e-184">在 Windows PowerShell 視窗中，呼叫下列 Cmdlet 以將您的託管服務重新部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="db09e-184">In the Windows PowerShell window, call the following cmdlet to redeploy your hosted service to Azure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="db09e-185">將 **myuniquename** 取代為此應用程式的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="db09e-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="db09e-186">將 **datacentername** 取代為 Azure 資料中心的名稱，例如「美國西部」。</span><span class="sxs-lookup"><span data-stu-id="db09e-186">Replace **datacentername** with the name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="db09e-187">部署完成之後，您應該會看到類似這樣的回應：</span><span class="sxs-lookup"><span data-stu-id="db09e-187">After the deployment is complete, you should see a response similar to the following:</span></span>

```
  PS C:\node\tasklist> publish-azureserviceproject -servicename tasklist -location "West US"
  WARNING: Publishing tasklist to Microsoft Azure. This may take several minutes...
  WARNING: 2:18:42 PM - Preparing runtime deployment for service 'tasklist'
  WARNING: 2:18:42 PM - Verifying storage account 'tasklist'...
  WARNING: 2:18:43 PM - Preparing deployment for tasklist with Subscription ID: 65a1016d-0f67-45d2-b838-b8f373d6d52e...
  WARNING: 2:19:01 PM - Connecting...
  WARNING: 2:19:02 PM - Uploading Package to storage service larrystore...
  WARNING: 2:19:40 PM - Upgrading...
  WARNING: 2:22:48 PM - Created Deployment ID: b7134ab29b1249ff84ada2bd157f296a.
  WARNING: 2:22:48 PM - Initializing...
  WARNING: 2:22:49 PM - Instance WebRole1_IN_0 of role WebRole1 is ready.
  WARNING: 2:22:50 PM - Created Website URL: http://tasklist.cloudapp.net/.
```

<span data-ttu-id="db09e-188">和之前一樣，因為您指定 **-launch** 選項，所以當發佈完成時，瀏覽器便會開啟並顯示在 Azure 中執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="db09e-188">As before, because you specified the **-launch** option, the browser opens and displays your application running in Azure when publishing is completed.</span></span>

![顯示 [我的工作清單] 頁面的瀏覽器視窗。](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="db09e-191">停止並刪除您的應用程式</span><span class="sxs-lookup"><span data-stu-id="db09e-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="db09e-192">在部署應用程式之後，您可能會想要將它停用以避免成本，或在免費試用時間間隔內建置並部署其他應用程式。</span><span class="sxs-lookup"><span data-stu-id="db09e-192">After deploying your application, you may want to disable it so you can avoid costs or build and deploy other applications within the free trial time period.</span></span>

<span data-ttu-id="db09e-193">Azure 會對於 Web 角色執行個體的伺服器使用時間時數計費。</span><span class="sxs-lookup"><span data-stu-id="db09e-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="db09e-194">一旦部署應用程式，即會耗用伺服器時間，即使執行個體不在執行中，並處於停止狀態也一樣。</span><span class="sxs-lookup"><span data-stu-id="db09e-194">Server time is consumed once your application is deployed, even if the instances are not running and are in the stopped state.</span></span>

<span data-ttu-id="db09e-195">下列步驟示範如何停止並刪除應用程式。</span><span class="sxs-lookup"><span data-stu-id="db09e-195">The following steps show you how to stop and delete your application.</span></span>

1. <span data-ttu-id="db09e-196">在 Windows PowerShell 視窗中，使用下列 Cmdlet 停止上一個小節中建立的服務部署：</span><span class="sxs-lookup"><span data-stu-id="db09e-196">In the Windows PowerShell window, stop the service deployment created in the previous section with the following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="db09e-197">停止服務可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="db09e-197">Stopping the service may take several minutes.</span></span> <span data-ttu-id="db09e-198">服務停止時，您將收到表示停止的訊息。</span><span class="sxs-lookup"><span data-stu-id="db09e-198">When the service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="db09e-199">若要刪除服務，請呼叫下列 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="db09e-199">To delete the service, call the following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="db09e-200">出現提示時，輸入 **Y** 以刪除服務。</span><span class="sxs-lookup"><span data-stu-id="db09e-200">When prompted, enter **Y** to delete the service.</span></span>

   <span data-ttu-id="db09e-201">刪除服務可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="db09e-201">Deleting the service may take several minutes.</span></span> <span data-ttu-id="db09e-202">刪除服務後，您將收到表示已刪除服務的訊息。</span><span class="sxs-lookup"><span data-stu-id="db09e-202">After the service has been deleted you receive a message indicating that the service was deleted.</span></span>

<span data-ttu-id="db09e-203">[使用 Express 的 Node.js Web 應用程式]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/</span><span class="sxs-lookup"><span data-stu-id="db09e-203">[Node.js Web Application using Express]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/</span></span>
<span data-ttu-id="db09e-204">[在 Azure 中儲存和存取資料]: http://msdn.microsoft.com/library/azure/gg433040.aspx</span><span class="sxs-lookup"><span data-stu-id="db09e-204">[Storing and Accessing Data in Azure]: http://msdn.microsoft.com/library/azure/gg433040.aspx</span></span>
<span data-ttu-id="db09e-205">[Node.js Web 應用程式]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/</span><span class="sxs-lookup"><span data-stu-id="db09e-205">[Node.js Web Application]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/</span></span>


