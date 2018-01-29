---
title: "Azure 資料表儲存體：建置 Web 應用程式 Node.js | Microsoft Docs"
description: "本教學課程以「使用 Express 的 Web 應用程式」教學課程為基礎，再加上 Azure 儲存體服務和 Azure 模組建置而成。"
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: e90959a2-4cb2-4b19-9bfb-aede15b18b1c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 11/03/2017
ms.author: mimig
ms.openlocfilehash: 9acd197c26e6365e396fd8f6321d764bba7bbb6c
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="azure-table-storage-nodejs-web-application"></a>Azure 資料表儲存體：Node.js Web 應用程式
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

## <a name="overview"></a>概觀
本教學課程會擴充您在[使用 Express 的 Node.js Web 應用程式]教學課程中所建立的應用程式，方法是使用 Microsoft Azure Client Libraries for Node.js 來搭配資料管理服務使用。 您要建立可供部署到 Azure 的 Web 架構工作清單應用程式以擴充您的應用程式。 使用者可透過工作清單來擷取工作、新增工作及將工作標示為已完成。

工作項目會儲存於 Azure 儲存體中。 Azure 儲存體提供可容錯且高度可用的非結構化資料儲存體。 Azure 儲存體包含許多資料結構供您儲存及存取資料。 您可以從包含在 Azure SDK for Node.js 的 API 或透過 REST API 使用儲存體服務。 如需詳細資訊，請參閱[在 Azure 中儲存和存取資料]。

本教學課程假設您已完成 [Node.js Web 應用程式]和[使用 Express 的 Node.js][使用 Express 的 Node.js Web 應用程式]教學課程。

其包含下列資訊：

* 如何使用 Jade 範本引擎
* 如何使用 Azure 資料管理服務

下列螢幕擷取畫面會顯示完成的應用程式：

![The completed web page in internet explorer](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="setting-storage-credentials-in-webconfig"></a>在 Web.Config 中設定儲存體認證
您必須傳入儲存體認證才能存取 Azure 儲存體。 藉由使用 web.config 應用程式設定即可達到此目的。
web.config 設定會以環境變數方式傳遞至 Node，接著再由 Azure SDK 進行讀取。

> [!NOTE]
> 只有當將應用程式部署到 Azure 時，才會用到儲存體認證。 在模擬器中執行時，應用程式會使用儲存體模擬器。
>
>

執行下列步驟以擷取儲存體帳戶認證，並將他們新增至 web.config 設定：

1. 從 [開始] 功能表中啟動 Azure PowerShell (如果尚未開啟的話)，方法是依序展開 [所有程式]、[Azure]，以滑鼠右鍵按一下 [Azure PowerShell]，然後選取 [以系統管理員身份執行]。
2. 將目錄變更到包含應用程式的資料夾。 例如，C:\\node\\tasklist\\WebRole1。
3. 在 [Azure Powershell] 視窗中，輸入下列 Cmdlet 以擷取儲存體帳戶資訊：

    ```powershell
    PS C:\node\tasklist\WebRole1> Get-AzureStorageAccounts
    ```

   前述 Cmdlet 會擷取與託管服務相關的儲存體帳戶和帳戶金鑰清單。

   > [!NOTE]
   > 由於 Azure SDK 會在您部署服務時建立儲存體帳戶，因此，從上一個說明的部署應用程式中應已有儲存體帳戶存在。
   >
   >
4. 開啟包含環境設定 (將應用程式部署到 Azure 時會用到) 的 **ServiceDefinition.csdef** 檔案：

    ```powershell
    PS C:\node\tasklist> notepad ServiceDefinition.csdef
    ```

5. 將下列區塊插入 **Environment** 元素下方，以您要用於部署之儲存體帳戶的帳戶名稱和主要金鑰取代 {儲存體帳戶} 和 {儲存體存取金鑰}：

  <Variable name="AZURE_STORAGE_ACCOUNT" value="{STORAGE ACCOUNT}" />
  <Variable name="AZURE_STORAGE_ACCESS_KEY" value="{STORAGE ACCESS KEY}" />

   ![web.cloud.config 檔案內容](./media/table-storage-cloud-service-nodejs/node37.png)

6. 儲存檔案並關閉記事本。

### <a name="install-additional-modules"></a>安裝其他模組
1. 使用下列命令在本機安裝 [azure]、[node-uuid]、[nconf] 及 [async] 模組，以及將它們的項目儲存至 **package.json** 檔案：

  ```powershell
  PS C:\node\tasklist\WebRole1> npm install azure-storage node-uuid async nconf --save
  ```

  此命令的輸出應類似這樣：

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

## <a name="using-the-table-service-in-a-node-application"></a>在節點應用程式中使用資料表服務
在本節中，您將藉著新增 **task.js** 檔案 (包含工作的模型) 來擴充由 **express** 命令建立的基本應用程式。 修改現有的 **app.js** 檔案並建立新的 **tasklist.js** 檔案，以使用模型。

### <a name="create-the-model"></a>建立模型
1. 在 **WebRole1** 目錄中，建立新目錄 **models**。
2. 在 **models** 目錄中，建立新檔案 **task.js**。 此檔案會包含您的應用程式建立之工作的模型。
3. 在 **task.js** 檔案的開頭加入以下程式碼以參考所需的程式庫：

    ```nodejs
    var azure = require('azure-storage');
    var uuid = require('node-uuid');
    var entityGen = azure.TableUtilities.entityGenerator;
    ```

4. 接下來，新增程式碼以定義和匯出 Task 物件。 Task 物件負責連線至資料表。

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

5. 接下來，新增下列程式碼以定義 Task 物件上的其他方法，允許與資料表中存放的資料互動：

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

6. 儲存並關閉 **task.js** 檔案。

### <a name="create-the-controller"></a>建立控制器
1. 在 **WebRole1/routes** 目錄中建立新檔案 **tasklist.js**，然後在文字編輯器中開啟檔案。
2. 在 **tasklist.js**中加入以下程式碼。 此程式碼會載入 azure 和 async 模組以供 **tasklist.js** 使用，並定義 **TaskList** 函式以在其中傳入我們先前定義之 **Task** 物件的執行個體：

    ```nodejs
    var azure = require('azure-storage');
    var async = require('async');

    module.exports = TaskList;

    function TaskList(task) {
      this.task = task;
    }
    ```

3. 繼續在 **tasklist.js** 檔案中新增用來 **showTasks (顯示工作)**、**addTask (新增工作)** 和 **completeTasks (完成工作)** 的方法：

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

4. 儲存 **tasklist.js** 檔案。

### <a name="modify-appjs"></a>修改 app.js
1. 在 **WebRole1** 目錄中，在文字編輯器中開啟 **app.js** 檔案。
2. 在檔案開頭，加入下列內容以載入 azure 模組，以及設定資料表名稱和資料分割索引鍵：

    ```nodejs
    var azure = require('azure-storage');
    var tableName = 'tasks';
    var partitionKey = 'hometasks';
    ```

3. 在 app.js 檔中，向下捲動到看見此行處：

    ```nodejs
    app.use('/', routes);
    app.use('/users', users);
    ```

    以下列程式碼取代前述幾行。 此程式碼會初始化 <strong>Task</strong> 的執行個體，並連線到您的儲存體帳戶。 <strong>Task</strong> 會傳遞給 <strong>TaskList</strong>，後者會用它來與表格服務通訊：

    ```nodejs
    var TaskList = require('./routes/tasklist');
    var Task = require('./models/task');
    var task = new Task(azure.createTableService(), tableName, partitionKey);
    var taskList = new TaskList(task);

    app.get('/', taskList.showTasks.bind(taskList));
    app.post('/addtask', taskList.addTask.bind(taskList));
    app.post('/completetask', taskList.completeTask.bind(taskList));
    ```

4. 儲存 **app.js** 檔案。

### <a name="modify-the-index-view"></a>修改索引檢視
1. 將目錄變更為 **views** 目錄，在文字編輯器中開啟 **index.jade** 檔案。
2. 以下列程式碼取代 **index.jade** 檔案的內容。 此程式碼會定義用於顯示現有工作的檢視，並定義用於加入新工作及將現有工作標示為完成的表單。

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

### <a name="modify-the-global-layout"></a>修改全域版面配置
**views** 目錄中的 **layout.jade** 檔是用來作為其他 **.jade** 檔案的全域範本。 在此步驟中，修改 **layout.jade** 檔案以使用 [Twitter Bootstrap](https://github.com/twbs/bootstrap)，這個工具組能夠方便設計美觀的網站。

1. 下載並解壓縮 [Twitter Bootstrap](http://getbootstrap.com/)的檔案。 將 **bootstrap.min.css** 檔案從 **bootstrap\\dist\\css** 資料夾複製到您工作清單應用程式的 **public\\stylesheets** 目錄。
2. 從 **views** 資料夾，以文字編輯器開啟 **layout.jade** 檔案，並將內容取代為：

    doctype html  html    head      title= title      link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')      link(rel='stylesheet', href='/stylesheets/style.css')    body.app      nav.navbar.navbar-default        div.navbar-header          a.navbar-brand(href='/') My Tasks      block content

3. 儲存 **layout.jade** 檔案。

### <a name="running-the-application-in-the-emulator"></a>在模擬器中執行應用程式
使用下列命令在模擬器中啟動應用程式。

```powershell
PS C:\node\tasklist\WebRole1> start-azureemulator -launch
```

瀏覽器會開啟並顯示下列頁面：

![A web paged titled My Task List with a table containing tasks and fields to add a new task.](./media/table-storage-cloud-service-nodejs/node44.png)

使用表單新增項目，或將現有的項目標示為已完成以移除它們。

## <a name="publishing-the-application-to-azure"></a>將應用程式發行至 Azure
在 Windows PowerShell 視窗中，呼叫下列 Cmdlet 以將您的託管服務重新部署至 Azure。

```powershell
PS C:\node\tasklist\WebRole1> Publish-AzureServiceProject -name myuniquename -location datacentername -launch
```

將 **myuniquename** 取代為此應用程式的唯一名稱。 將 **datacentername** 取代為 Azure 資料中心的名稱，例如「美國西部」。

部署完成之後，您應該會看到類似這樣的回應：

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

藉由在前面的 Cmdlet 中指定 **-launch** 選項，當發佈完成時，瀏覽器便會開啟並顯示在 Azure 中執行的應用程式。

![顯示 [我的工作清單] 頁面的瀏覽器視窗。 URL 會指出頁面目前由 Azure 所主控。](./media/table-storage-cloud-service-nodejs/getting-started-1.png)

## <a name="stopping-and-deleting-your-application"></a>停止並刪除您的應用程式
在部署應用程式之後，您可能會想要將它停用以避免成本，或在免費試用時間間隔內建置並部署其他應用程式。

Azure 會對於 Web 角色執行個體的伺服器使用時間時數計費。
一旦部署應用程式，即會耗用伺服器時間，即使執行個體不在執行中，並處於停止狀態也一樣。

下列步驟示範如何停止並刪除應用程式。

1. 在 Windows PowerShell 視窗中，使用下列 Cmdlet 停止上一個小節中建立的服務部署：

    ```powershell
    PS C:\node\tasklist\WebRole1> Stop-AzureService
    ```

   停止服務可能需要幾分鐘的時間。 服務停止時，您將收到表示停止的訊息。

2. 若要刪除服務，請呼叫下列 Cmdlet：

    ```powershell
    PS C:\node\tasklist\WebRole1> Remove-AzureService contosotasklist
    ```

   出現提示時，輸入 **Y** 以刪除服務。

   刪除服務可能需要幾分鐘的時間。 刪除服務後，您會收到表示已刪除服務的訊息。

[使用 Express 的 Node.js Web 應用程式]: http://azure.microsoft.com/develop/nodejs/tutorials/web-app-with-express/
[在 Azure 中儲存和存取資料]: http://msdn.microsoft.com/library/azure/gg433040.aspx
[Node.js Web 應用程式]: http://azure.microsoft.com/develop/nodejs/tutorials/getting-started/


