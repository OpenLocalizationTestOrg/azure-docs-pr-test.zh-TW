---
title: "aaaWeb 應用程式，使用資料表儲存體 (Node.js) |Microsoft 文件"
description: "新增 Azure 儲存體服務和 hello Azure 模組是 hello Web 應用程式快速教學課程為基礎的教學課程。"
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: e90959a2-4cb2-4b19-9bfb-aede15b18b1c
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 7eefc09baab61cf44c98183135abe572b11812e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-application-using-storage"></a>使用儲存體的 Node.js Web 應用程式
## <a name="overview"></a>概觀
在本教學課程，hello 應用程式中建立[Node.js Web 應用程式使用快速]教學課程會擴充 hello Microsoft Azure 用戶端程式庫用於 Node.js toowork 與資料管理服務。 您建立的網頁型的工作清單應用程式，您可以部署 tooAzure 來擴充您的應用程式。 hello 工作清單可讓使用者擷取工作、 加入新的工作，並將工作標示為已完成。

hello 工作項目會儲存在 Azure 儲存體。 Azure 儲存體提供可容錯且高度可用的非結構化資料儲存體。 Azure 儲存體包含許多資料結構供您儲存及存取資料。 您可以使用從 hello 納入 hello Azure SDK for Node.js 或透過 REST Api 的應用程式開發介面的 hello 儲存體服務。 如需詳細資訊，請參閱[在 Azure 中儲存和存取資料]。

本教學課程假設您已經完成 hello [Node.js Web 應用程式]和[快速 Node.js][Node.js Web 應用程式使用快速]教學課程。

它包含下列資訊的 hello:

* 如何使用 toowork hello Jade 範本引擎
* 如何與 Azure 資料管理服務 toowork

下列螢幕擷取畫面的 hello 顯示 hello 完成應用程式：

![hello 完成網頁在 internet explorer](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a>在 Web.Config 中設定儲存體認證
您必須傳遞儲存體認證 tooaccess Azure 儲存體中。 這是藉由使用 hello web.config 應用程式設定。
hello web.config 設定會傳遞做為環境變數 tooNode，以供然後讀取 hello Azure SDK。

> [!NOTE]
> 已部署的 tooAzure hello 應用程式時，才會使用儲存體認證。 Hello 模擬器中執行時，hello 應用程式會使用 hello 儲存體模擬器。
>
>

執行下列步驟 tooretrieve hello 儲存體帳戶認證的 hello，並將其新增 toohello web.config 設定：

1. 如果它尚未開啟，請從 hello 啟動 hello Azure PowerShell**啟動**展開功能表**所有程式、 Azure**，以滑鼠右鍵按一下**Azure PowerShell**，然後選取  **系統管理員身分執行**。
2. 變更目錄 toohello 資料夾包含您的應用程式。 例如，C:\\node\\tasklist\\WebRole1。
3. 從 hello Azure Powershell 視窗中，輸入下列 cmdlet tooretrieve hello 儲存體帳戶資訊的 hello:

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   hello 前述的 cmdlet 會擷取 hello 清單的儲存體帳戶及託管服務相關聯的帳戶金鑰。

   > [!NOTE]
   > Hello Azure SDK 會建立儲存體帳戶，當您部署服務時，從部署 hello 先前指南中的應用程式應已經存在於儲存體帳戶。
   >
   >
4. 開啟 hello **ServiceDefinition.csdef**包含已部署的 tooAzure hello 應用程式時所使用的 hello 環境設定檔案：

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. 插入 hello 以下區塊下**環境**項目，以取代 {儲存體帳戶} 和 {儲存體存取金鑰} hello 帳戶名稱與 hello 您想要部署 toouse hello 儲存體帳戶的主索引鍵：

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![hello web.cloud.config 檔案內容](./media/table-storage-cloud-service-nodejs/node37.png)

6. 儲存 hello 檔案並關閉 [記事本]。

### <a name="install-additional-modules"></a>安裝其他模組
1. 使用 hello 遵循命令 tooinstall hello [azure]、 [節點-uuid]，[nconf] 和 [非同步] 模組，在本機以及 toosave 項目，toohello **package.json**檔案：

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  此命令的 hello 輸出應該看起來類似 toohello 下列：

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

## <a name="using-hello-table-service-in-a-node-application"></a>在 node 應用程式中使用 hello 表格服務
在本節中的 hello hello 所建立的基本應用程式**express**藉由新增延伸命令**task.js**內含您的工作的 hello 模型檔。 修改現有的 hello **app.js**檔案並建立新**tasklist.js**使用 hello 模式的檔案。

### <a name="create-hello-model"></a>建立 hello 模型
1. 在 hello **WebRole1**目錄中，建立名為的新目錄**模型**。
2. 在 hello**模型**目錄中，建立新的檔案命名為**task.js**。 此檔案包含您的應用程式所建立的 hello 工作 hello 模型。
3. 在 hello hello 開頭**task.js**檔案中加入下列程式碼所需的 tooreference 程式庫的 hello:

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. 接下來，加入程式碼 toodefine 並匯出 hello 工作物件。 hello 工作物件會負責連接 toohello 資料表。

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

5. 接下來，新增 hello hello 工作物件，在下列程式碼 toodefine 其他方法可讓資料儲存在 hello 資料表之間的互動：

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

6. 儲存並關閉 hello **task.js**檔案。

### <a name="create-hello-controller"></a>建立 hello 控制站
1. 在 hello **WebRole1/路由**目錄中，建立新的檔案命名為**tasklist.js**在文字編輯器中開啟它。
2. 新增下列程式碼太 hello**tasklist.js**。 此程式碼會載入 hello azure 和非同步模組所使用的**tasklist.js**並定義 hello **TaskList**函式，會傳遞 hello 的執行個體**工作**我們物件先前定義：

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. 繼續加入 toohello **tasklist.js**檔案加上使用過的 hello 方法**showTasks**， **addTask**，和**completeTasks**:

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

4. 儲存 hello **tasklist.js**檔案。

### <a name="modify-appjs"></a>修改 app.js
1. 在 hello **WebRole1**目錄，請開啟 hello **app.js**文字編輯器中的檔案。
2. 在 hello hello 檔案開頭，加入下列 tooload hello azure 模組的 hello 並設定 hello 資料表名稱和資料分割索引鍵：

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. 在 hello app.js 檔案中，向下捲動的 toowhere 您會看到下列行 hello:

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    取代 hello 前面以 hello 下列程式碼行。 這個程式碼初始化的執行個體<strong>工作</strong>連接 tooyour 儲存體帳戶。 hello<strong>工作</strong>傳遞 toohello <strong>TaskList</strong>，它會使用它 toocommunicate hello 表格服務：

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. 儲存 hello **app.js**檔案。

### <a name="modify-hello-index-view"></a>修改 hello 索引檢視表
1. 變更目錄 toohello**檢視**目錄，以及開啟 hello **index.jade**文字編輯器中的檔案。
2. 取代 hello hello 內容**index.jade** hello 下列程式碼檔案。 此程式碼定義 hello 檢視以顯示現有的工作，並定義用來加入新的工作，並將現有的標記為已完成的表單。

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

3. 儲存並關閉 **index.jade** 檔案。

### <a name="modify-hello-global-layout"></a>修改 hello 全域版面配置
hello **layout.jade**檔案在 hello**檢視**目錄作為全域範本其他**.jade**檔案。 在此步驟中，修改 hello **layout.jade**檔案 toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap)，這是一項工具組，可讓您輕鬆 toodesign nice 尋找網站。

1. 下載並解壓縮 hello 檔案[Twitter Bootstrap](http://getbootstrap.com/)。 複製 hello **bootstrap.min.css**檔案從 hello**啟動程序\\dist\\css**資料夾 toohello**公用\\樣式表**tasklist 應用程式的目錄。
2. 從 hello**檢視**資料夾中，開啟 hello **layout.jade**檔案文字編輯器中，並取代 hello 下列中的 hello 內容：

    doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content

3. 儲存 hello **layout.jade**檔案。

### <a name="running-hello-application-in-hello-emulator"></a>在 hello 模擬器中執行 hello 應用程式
使用下列命令 toostart hello 應用程式在 hello 模擬器中的 hello。

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

hello 瀏覽器會開啟，並顯示 hello 下列頁面：

![網頁標題為 我的工作清單與資料表，其中包含工作和欄位 tooadd 新的工作。](./media/table-storage-cloud-service-nodejs/node44.png)

使用 hello 表單 tooadd 項目，或移除現有的項目將其標示為已完成。

## <a name="publishing-hello-application-tooazure"></a>發行 hello 應用程式 tooAzure
在 hello Windows PowerShell 視窗中，呼叫下列 cmdlet tooredeploy hello 託管的服務 tooAzure。

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

將 **myuniquename** 取代為此應用程式的唯一名稱。 取代**datacentername**與 hello Azure 資料中心名稱，例如**美國西部**。

Hello 部署完成之後，您應該會看到類似 toohello 後的回應：

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

藉由指定 hello **-啟動**hello 前一個 cmdlet，hello 瀏覽器中的選項會開啟並顯示您在發行完成時，在 Azure 中執行的應用程式。

![瀏覽器視窗，顯示 hello [我的工作清單] 頁面。 hello URL 表示 hello 頁面現在會裝載於 Azure。](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a>停止並刪除您的應用程式
部署後您的應用程式，您可能想的 toodisable 它讓您可以避免成本或建置和部署其他應用程式內 hello 免費試用時間週期。

Azure 會對於 Web 角色執行個體的伺服器使用時間時數計費。
使用伺服器時間為您的應用程式部署之後，即使執行個體未執行而且處於 hello 停止狀態。

hello 下列步驟說明如何 toostop 並刪除您的應用程式。

1. 在 hello Windows PowerShell 視窗中，停止以 hello 下列 cmdlet 建立 hello 前一節中的 hello 服務部署：

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   停止 hello 服務可能需要幾分鐘的時間。 Hello 服務停止時，您會收到訊息，指出 已停止。

2. 下列指令程式呼叫 hello toodelete hello 服務：

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   出現提示時，輸入**Y** toodelete hello 服務。

   刪除 hello 服務可能需要幾分鐘的時間。 Hello 服務刪除之後，您會收到指出 hello 服務已刪除訊息。

[Node.js Web 應用程式使用快速]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[在 Azure 中儲存和存取資料]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[Node.js Web 應用程式]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


