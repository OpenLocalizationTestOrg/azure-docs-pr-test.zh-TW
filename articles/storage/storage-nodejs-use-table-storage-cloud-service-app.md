---
title: "aaaWeb 應用程式，使用資料表儲存體 (Node.js) |Microsoft 文件"
description: "新增 Azure 儲存體服務和 hello Azure 模組是 hello Web 應用程式快速教學課程為基礎的教學課程。"
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
ms.openlocfilehash: 4eba16f09f8b69cbc135d097e6ca71e08b33733c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-application-using-storage"></a><span data-ttu-id="d0a9e-103">使用儲存體的 Node.js Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="d0a9e-103">Node.js Web Application using Storage</span></span>
## <a name="overview"></a><span data-ttu-id="d0a9e-104">概觀</span><span class="sxs-lookup"><span data-stu-id="d0a9e-104">Overview</span></span>
<span data-ttu-id="d0a9e-105">在本教學課程中，您就可以擴充 hello 應用程式中建立[Node.js Web 應用程式使用快速]hello Microsoft Azure 用戶端程式庫使用 Node.js toowork 與資料管理服務的教學課程。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-105">In this tutorial, you will extend hello application created in the [Node.js Web Application using Express] tutorial by using hello Microsoft Azure Client Libraries for Node.js toowork with data management services.</span></span> <span data-ttu-id="d0a9e-106">您將擴充您的應用程式 toocreate 您可以部署 tooAzure web 為基礎的工作清單應用程式。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-106">You will extend your application toocreate a web-based task-list application that you can deploy tooAzure.</span></span> <span data-ttu-id="d0a9e-107">hello 工作清單可讓使用者擷取工作、 加入新的工作，並將工作標示為已完成。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-107">hello task list allows a user to retrieve tasks, add new tasks, and mark tasks as completed.</span></span>

<span data-ttu-id="d0a9e-108">hello 工作項目會儲存在 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-108">hello task items are stored in Azure Storage.</span></span> <span data-ttu-id="d0a9e-109">Azure 儲存體提供可容錯且高度可用的非結構化資料儲存體。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-109">Azure Storage provides unstructured data storage that is fault-tolerant and highly available.</span></span> <span data-ttu-id="d0a9e-110">Azure 儲存體包含許多資料結構，其中您可以儲存和存取資料，而且您可以利用從 hello 納入 hello Azure SDK for Node.js 或透過 REST Api 的應用程式開發介面的 hello 儲存體服務。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-110">Azure Storage includes several data structures where you can store and access data, and you can leverage hello storage services from hello APIs included in hello Azure SDK for Node.js or via REST APIs.</span></span> <span data-ttu-id="d0a9e-111">如需詳細資訊，請參閱[在 Azure 中儲存和存取資料]。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-111">For more information, see [Storing and Accessing Data in Azure].</span></span>

<span data-ttu-id="d0a9e-112">本教學課程假設您已經完成 hello [Node.js Web 應用程式]和[快速 Node.js][Node.js Web 應用程式使用快速]教學課程。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-112">This tutorial assumes that you have completed hello [Node.js Web Application] and [Node.js with Express][Node.js Web Application using Express] tutorials.</span></span>

<span data-ttu-id="d0a9e-113">您將了解：</span><span class="sxs-lookup"><span data-stu-id="d0a9e-113">You will learn:</span></span>

* <span data-ttu-id="d0a9e-114">如何使用 toowork hello Jade 範本引擎</span><span class="sxs-lookup"><span data-stu-id="d0a9e-114">How toowork with hello Jade template engine</span></span>
* <span data-ttu-id="d0a9e-115">如何與 Azure 資料管理服務 toowork</span><span class="sxs-lookup"><span data-stu-id="d0a9e-115">How toowork with Azure Data Management services</span></span>

<span data-ttu-id="d0a9e-116">底下是完成 hello 應用程式的螢幕擷取畫面：</span><span class="sxs-lookup"><span data-stu-id="d0a9e-116">A screenshot of hello completed application is below:</span></span>

![hello 完成網頁在 internet explorer](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a><span data-ttu-id="d0a9e-118">在 Web.Config 中設定儲存體認證</span><span class="sxs-lookup"><span data-stu-id="d0a9e-118">Setting Storage Credentials in Web.Config</span></span>
<span data-ttu-id="d0a9e-119">tooaccess Azure 儲存體，您需要在儲存體認證 toopass。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-119">tooaccess Azure Storage, you need toopass in storage credentials.</span></span> <span data-ttu-id="d0a9e-120">toodo，運用 web.config 應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-120">toodo this, you utilize web.config application settings.</span></span>
<span data-ttu-id="d0a9e-121">這些設定會傳遞為環境變數 tooNode，然後讀取由 hello Azure SDK。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-121">Those settings will be passed as environment variables tooNode, which are then read by hello Azure SDK.</span></span>

> [!NOTE]
> <span data-ttu-id="d0a9e-122">已部署的 tooAzure hello 應用程式時，才會使用儲存體認證。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-122">Storage credentials are only used when hello application is deployed tooAzure.</span></span> <span data-ttu-id="d0a9e-123">Hello 模擬器中執行時，hello 應用程式會使用 hello 儲存體模擬器。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-123">When running in hello emulator, hello application will use hello storage emulator.</span></span>
>
>

<span data-ttu-id="d0a9e-124">執行下列步驟 tooretrieve hello 儲存體帳戶認證的 hello，並將其新增 toohello web.config 設定：</span><span class="sxs-lookup"><span data-stu-id="d0a9e-124">Perform hello following steps tooretrieve hello storage account credentials and add them toohello web.config settings:</span></span>

1. <span data-ttu-id="d0a9e-125">如果它尚未開啟，請從 hello 啟動 hello Azure PowerShell**啟動**展開功能表**所有程式、 Azure**，以滑鼠右鍵按一下**Azure PowerShell**，然後選取  **系統管理員身分執行**。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-125">If it is not already open, start hello Azure PowerShell from hello **Start** menu by expanding **All Programs, Azure**, right-click **Azure PowerShell**, and then select **Run As Administrator**.</span></span>
2. <span data-ttu-id="d0a9e-126">變更目錄 toohello 資料夾包含您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-126">Change directories toohello folder containing your application.</span></span> <span data-ttu-id="d0a9e-127">例如，C:\\node\\tasklist\\WebRole1。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-127">For example, C:\\node\\tasklist\\WebRole1.</span></span>
3. <span data-ttu-id="d0a9e-128">從 hello Azure Powershell 視窗中，輸入下列 cmdlet tooretrieve hello 儲存體帳戶資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="d0a9e-128">From hello Azure Powershell window enter hello following cmdlet tooretrieve hello storage account information:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   <span data-ttu-id="d0a9e-129">這樣會擷取儲存體帳戶和帳戶與您的託管服務相關聯的索引鍵的 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-129">This retrieves hello list of storage accounts and account keys associated with your hosted service.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d0a9e-130">Hello Azure SDK 會建立儲存體帳戶，當您部署服務時，從部署 hello 先前指南中的應用程式應已經存在於儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-130">Since hello Azure SDK creates a storage account when you deploy a service, a storage account should already exist from deploying your application in hello previous guides.</span></span>
   >
   >
4. <span data-ttu-id="d0a9e-131">開啟 hello **ServiceDefinition.csdef**包含已部署的 tooAzure hello 應用程式時所使用的 hello 環境設定檔案：</span><span class="sxs-lookup"><span data-stu-id="d0a9e-131">Open hello **ServiceDefinition.csdef** file containing hello environment settings that are used when hello application is deployed tooAzure:</span></span>

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. <span data-ttu-id="d0a9e-132">插入 hello 以下區塊下**環境**項目，以取代 {儲存體帳戶} 和 {儲存體存取金鑰} hello 帳戶名稱與 hello 您想要部署 toouse hello 儲存體帳戶的主索引鍵：</span><span class="sxs-lookup"><span data-stu-id="d0a9e-132">Insert hello following block under **Environment** element, substituting {STORAGE ACCOUNT} and {STORAGE ACCESS KEY} with hello account name and hello primary key for hello storage account you want toouse for deployment:</span></span>

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![hello web.cloud.config 檔案內容](./media/storage-nodejs-use-table-storage-cloud-service-app/node37.png)

6. <span data-ttu-id="d0a9e-134">儲存 hello 檔案並關閉 [記事本]。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-134">Save hello file and close notepad.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="d0a9e-135">安裝其他模組</span><span class="sxs-lookup"><span data-stu-id="d0a9e-135">Install additional modules</span></span>
1. <span data-ttu-id="d0a9e-136">使用 hello 遵循命令 tooinstall hello [azure]、 [節點-uuid]，[nconf] 和 [非同步] 模組，在本機以及 toosave 項目，toohello **package.json**檔案：</span><span class="sxs-lookup"><span data-stu-id="d0a9e-136">Use hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules locally as well as toosave an entry for them toohello **package.json** file:</span></span>

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  <span data-ttu-id="d0a9e-137">此命令的 hello 輸出應該看起來類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="d0a9e-137">hello output of this command should appear similar toohello following:</span></span>

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

## <a name="using-hello-table-service-in-a-node-application"></a><span data-ttu-id="d0a9e-138">在 node 應用程式中使用 hello 表格服務</span><span class="sxs-lookup"><span data-stu-id="d0a9e-138">Using hello Table service in a node application</span></span>
<span data-ttu-id="d0a9e-139">這一節中，您將延伸 hello 基本應用程式建立 hello **express**命令藉由新增**task.js**檔案包含您的工作的 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-139">In this section you will extend hello basic application created by hello **express** command by adding a **task.js** file which contains hello model for your tasks.</span></span> <span data-ttu-id="d0a9e-140">您也會修改現有的 hello **app.js**並建立新**tasklist.js**使用 hello 模式的檔案。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-140">You will also modify hello existing **app.js** and create a new **tasklist.js** file that uses hello model.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="d0a9e-141">建立 hello 模型</span><span class="sxs-lookup"><span data-stu-id="d0a9e-141">Create hello model</span></span>
1. <span data-ttu-id="d0a9e-142">在 hello **WebRole1**目錄中，建立名為的新目錄**模型**。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-142">In hello **WebRole1** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="d0a9e-143">在 hello**模型**目錄中，建立新的檔案命名為**task.js**。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-143">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="d0a9e-144">這個檔案會包含您的應用程式所建立的 hello 工作 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-144">This file will contain hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="d0a9e-145">在 hello hello 開頭**task.js**檔案中加入下列程式碼所需的 tooreference 程式庫的 hello:</span><span class="sxs-lookup"><span data-stu-id="d0a9e-145">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. <span data-ttu-id="d0a9e-146">接下來，您會加入程式碼 toodefine 以及匯出 hello 工作物件。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-146">Next, you will add code toodefine and export hello Task object.</span></span> <span data-ttu-id="d0a9e-147">此物件負責連接 toohello 資料表。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-147">This object is responsible for connecting toohello table.</span></span>

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

5. <span data-ttu-id="d0a9e-148">接下來，新增 hello hello 工作物件，在下列程式碼 toodefine 其他方法可讓資料儲存在 hello 資料表之間的互動：</span><span class="sxs-lookup"><span data-stu-id="d0a9e-148">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>

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
    ```

6. <span data-ttu-id="d0a9e-149">儲存並關閉 hello **task.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-149">Save and close hello **task.js** file.</span></span>

### <a name="create-hello-controller"></a><span data-ttu-id="d0a9e-150">建立 hello 控制站</span><span class="sxs-lookup"><span data-stu-id="d0a9e-150">Create hello controller</span></span>
1. <span data-ttu-id="d0a9e-151">在 hello **WebRole1/路由**目錄中，建立新的檔案命名為**tasklist.js**在文字編輯器中開啟它。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-151">In hello **WebRole1/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="d0a9e-152">新增下列程式碼太 hello**tasklist.js**。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-152">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="d0a9e-153">這會載入 hello azure 與非同步模組所使用的**tasklist.js**。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-153">This loads hello azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="d0a9e-154">這也會定義 hello **TaskList**函式，會傳遞 hello 的執行個體**工作**我們先前定義的物件：</span><span class="sxs-lookup"><span data-stu-id="d0a9e-154">This also defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. <span data-ttu-id="d0a9e-155">繼續加入 toohello **tasklist.js**檔案加上使用過的 hello 方法**showTasks**， **addTask**，和**completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="d0a9e-155">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks**, **addTask**, and **completeTasks**:</span></span>

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

4. <span data-ttu-id="d0a9e-156">儲存 hello **tasklist.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-156">Save hello **tasklist.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="d0a9e-157">修改 app.js</span><span class="sxs-lookup"><span data-stu-id="d0a9e-157">Modify app.js</span></span>
1. <span data-ttu-id="d0a9e-158">在 hello **WebRole1**目錄，請開啟 hello **app.js**文字編輯器中的檔案。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-158">In hello **WebRole1** directory, open hello **app.js** file in a text editor.</span></span>
2. <span data-ttu-id="d0a9e-159">在 hello hello 檔案開頭，加入下列 tooload hello azure 模組的 hello 並設定 hello 資料表名稱和資料分割索引鍵：</span><span class="sxs-lookup"><span data-stu-id="d0a9e-159">At hello beginning of hello file, add hello following tooload hello azure module and set hello table name and partition key:</span></span>

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. <span data-ttu-id="d0a9e-160">在 hello app.js 檔案中，向下捲動的 toowhere 您會看到下列行 hello:</span><span class="sxs-lookup"><span data-stu-id="d0a9e-160">In hello app.js file, scroll down toowhere you see hello following line:</span></span>

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    <span data-ttu-id="d0a9e-161">取代 hello 如下所示的程式碼行上方的 hello。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-161">Replace hello above lines with hello code shown below.</span></span> <span data-ttu-id="d0a9e-162">這將會初始化的執行個體<strong>工作</strong>連接 tooyour 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-162">This will initialize an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="d0a9e-163">這會傳遞 toohello <strong>TaskList</strong>，就會使用它 toocommunicate 以 hello 表格服務：</span><span class="sxs-lookup"><span data-stu-id="d0a9e-163">This is passed toohello <strong>TaskList</strong>, which will use it toocommunicate with hello Table service:</span></span>

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. <span data-ttu-id="d0a9e-164">儲存 hello **app.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-164">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="d0a9e-165">修改 hello 索引檢視表</span><span class="sxs-lookup"><span data-stu-id="d0a9e-165">Modify hello index view</span></span>
1. <span data-ttu-id="d0a9e-166">變更目錄 toohello**檢視**目錄，以及開啟 hello **index.jade**文字編輯器中的檔案。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-166">Change directories toohello **views** directory and open hello **index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="d0a9e-167">取代 hello hello 內容**index.jade** hello 的下列程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-167">Replace hello contents of hello **index.jade** file with hello code below.</span></span> <span data-ttu-id="d0a9e-168">這會定義 hello 檢視以顯示現有的工作，以及加入新的工作，並將現有的標記為已完成的表單。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-168">This defines hello view for displaying existing tasks, as well as a form for adding new tasks and marking existing ones as completed.</span></span>

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

3. <span data-ttu-id="d0a9e-169">儲存並關閉 **index.jade** 檔案。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-169">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="d0a9e-170">修改 hello 全域版面配置</span><span class="sxs-lookup"><span data-stu-id="d0a9e-170">Modify hello global layout</span></span>
<span data-ttu-id="d0a9e-171">hello **layout.jade**檔案在 hello**檢視**目錄作為全域範本其他**.jade**檔案。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-171">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="d0a9e-172">在此步驟中您會修改它 toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap)，這是一項工具組，可讓您輕鬆 toodesign nice 尋找網站。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-172">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span>

1. <span data-ttu-id="d0a9e-173">下載並解壓縮 hello 檔案[Twitter Bootstrap](http://getbootstrap.com/)。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-173">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="d0a9e-174">複製 hello **bootstrap.min.css**檔案從 hello**啟動程序\\dist\\css**資料夾 toohello**公用\\樣式表**tasklist 應用程式的目錄。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-174">Copy hello **bootstrap.min.css** file from hello **bootstrap\\dist\\css** folder toohello **public\\stylesheets** directory of your tasklist application.</span></span>
2. <span data-ttu-id="d0a9e-175">從 hello**檢視**資料夾中，開啟 hello **layout.jade** hello 下列您文字編輯器和取代 hello 內容中：</span><span class="sxs-lookup"><span data-stu-id="d0a9e-175">From hello **views** folder, open hello **layout.jade** in your text editor and replace hello contents with hello following:</span></span>

    <span data-ttu-id="d0a9e-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span><span class="sxs-lookup"><span data-stu-id="d0a9e-176">doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content</span></span>

3. <span data-ttu-id="d0a9e-177">儲存 hello **layout.jade**檔案。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-177">Save hello **layout.jade** file.</span></span>

### <a name="running-hello-application-in-hello-emulator"></a><span data-ttu-id="d0a9e-178">在 hello 模擬器中執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="d0a9e-178">Running hello Application in hello Emulator</span></span>
<span data-ttu-id="d0a9e-179">使用下列命令 toostart hello 應用程式在 hello 模擬器中的 hello。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-179">Use hello following command toostart hello application in hello emulator.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

<span data-ttu-id="d0a9e-180">hello 瀏覽器會開啟，並顯示 hello 下列頁面：</span><span class="sxs-lookup"><span data-stu-id="d0a9e-180">hello browser will open and displays hello following page:</span></span>

![網頁標題為 我的工作清單與資料表，其中包含工作和欄位 tooadd 新的工作。](./media/storage-nodejs-use-table-storage-cloud-service-app/node44.png)

<span data-ttu-id="d0a9e-182">使用 hello 表單 tooadd 項目，或移除現有的項目將其標示為已完成。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-182">Use hello form tooadd items, or remove existing items by marking them as completed.</span></span>

## <a name="publishing-hello-application-tooazure"></a><span data-ttu-id="d0a9e-183">發行 hello 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="d0a9e-183">Publishing hello Application tooAzure</span></span>
<span data-ttu-id="d0a9e-184">在 hello Windows PowerShell 視窗中，呼叫下列 cmdlet tooredeploy hello 託管的服務 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-184">In hello Windows PowerShell window, call hello following cmdlet tooredeploy your hosted service tooAzure.</span></span>

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

<span data-ttu-id="d0a9e-185">將 **myuniquename** 取代為此應用程式的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-185">Replace **myuniquename** with a unique name for this application.</span></span> <span data-ttu-id="d0a9e-186">取代**datacentername**與 hello Azure 資料中心名稱，例如**美國西部**。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-186">Replace **datacentername** with hello name of an Azure data center, such as **West US**.</span></span>

<span data-ttu-id="d0a9e-187">Hello 部署完成之後，您應該會看到類似 toohello 後的回應：</span><span class="sxs-lookup"><span data-stu-id="d0a9e-187">After hello deployment is complete, you should see a response similar toohello following:</span></span>

```
  PS C:\node\tasklist> publish-azureserviceproject -servicename tasklist -location "West US"
  WARNING: Publishing tasklist tooMicrosoft Azure. This may take several minutes...
  WARNING: 2:18:42 PM - Preparing runtime deployment for service 'tasklist'
  WARNING: 2:18:42 PM - Verifying storage account 'tasklist'...
  WARNING: 2:18:43 PM - Preparing deployment for tasklist with Subscription ID: 65a1016d-0f67-45d2-b838-b8f373d6d52e...
  WARNING: 2:19:01 PM - Connecting...
  WARNING: 2:19:02 PM - Uploading Package toostorage service larrystore...
  WARNING: 2:19:40 PM - Upgrading...
  WARNING: 2:22:48 PM - Created Deployment ID: b7134ab29b1249ff84ada2bd157f296a.
  WARNING: 2:22:48 PM - Initializing...
  WARNING: 2:22:49 PM - Instance WebRole1_IN_0 of role WebRole1 is ready.
  WARNING: 2:22:50 PM - Created Website URL: http://tasklist.cloudapp.net/.
```

<span data-ttu-id="d0a9e-188">如往常一般，因為指定 hello **-啟動**選項，hello 瀏覽器會開啟並顯示您在發行完成時，在 Azure 中執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-188">As before, because you specified hello **-launch** option, hello browser opens and displays your application running in Azure when publishing is completed.</span></span>

![瀏覽器視窗，顯示 hello [我的工作清單] 頁面。](./media/storage-nodejs-use-table-storage-cloud-service-app/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="d0a9e-191">停止並刪除您的應用程式</span><span class="sxs-lookup"><span data-stu-id="d0a9e-191">Stopping and Deleting Your Application</span></span>
<span data-ttu-id="d0a9e-192">部署後您的應用程式，您可能想的 toodisable 它讓您可以避免成本或建置和部署其他應用程式內 hello 免費試用時間週期。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-192">After deploying your application, you may want toodisable it so you can avoid costs or build and deploy other applications within hello free trial time period.</span></span>

<span data-ttu-id="d0a9e-193">Azure 會對於 Web 角色執行個體的伺服器使用時間時數計費。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-193">Azure bills web role instances per hour of server time consumed.</span></span>
<span data-ttu-id="d0a9e-194">使用伺服器時間為您的應用程式部署之後，即使執行個體未執行而且處於 hello 停止狀態。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-194">Server time is consumed once your application is deployed, even if the instances are not running and are in hello stopped state.</span></span>

<span data-ttu-id="d0a9e-195">hello 下列步驟說明如何 toostop 並刪除您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-195">hello following steps show you how toostop and delete your application.</span></span>

1. <span data-ttu-id="d0a9e-196">在 hello Windows PowerShell 視窗中，停止以 hello 下列 cmdlet 建立 hello 前一節中的 hello 服務部署：</span><span class="sxs-lookup"><span data-stu-id="d0a9e-196">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   <span data-ttu-id="d0a9e-197">停止 hello 服務可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-197">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="d0a9e-198">Hello 服務停止時，您會收到訊息，指出 已停止。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-198">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

2. <span data-ttu-id="d0a9e-199">下列指令程式呼叫 hello toodelete hello 服務：</span><span class="sxs-lookup"><span data-stu-id="d0a9e-199">toodelete hello service, call hello following cmdlet:</span></span>

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   <span data-ttu-id="d0a9e-200">出現提示時，輸入**Y** toodelete hello 服務。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-200">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="d0a9e-201">刪除 hello 服務可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-201">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="d0a9e-202">刪除 hello 服務之後您會收到指出 hello 服務已刪除的訊息。</span><span class="sxs-lookup"><span data-stu-id="d0a9e-202">After hello service has been deleted you receive a message indicating that hello service was deleted.</span></span>

[Node.js Web 應用程式使用快速]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[在 Azure 中儲存和存取資料]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[Node.js Web 應用程式]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


