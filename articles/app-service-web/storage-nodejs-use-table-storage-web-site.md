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
# <a name="nodejs-web-app-using-hello-azure-table-service"></a>Node.js web 應用程式使用 hello Azure 資料表服務
## <a name="overview"></a>概觀
此教學課程會示範如何 toouse 表格服務提供的 Azure 資料管理 toostore 及存取資料，從[節點]應用程式裝載於[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web 應用程式。 本教學課程假設您先前有過一些使用節點及 [Git]的經驗。

您將了解：

* 如何 toouse npm （node 封裝管理員） tooinstall hello 節點模組
* 如何使用 toowork hello Azure 資料表服務
* 如何 toouse hello Azure CLI toocreate web 應用程式。

依照本教學課程的指示，您將組建一個簡單的網頁型「待辦事項清單」應用程式，用於建立、擷取、完成工作。 hello 工作會儲存在 hello 表格服務。

以下是 hello 完成應用程式：

![顯示空白工作清單的網頁][node-table-finished]

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](https://azure.microsoft.com/try/app-service/)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 

## <a name="prerequisites"></a>必要條件
之前遵循這篇文章中的 hello 指示，請確定您擁有 hello 安裝下列項目：

* [節點] 版本 0.10.24 或更高版本
* [Git]

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a>建立儲存體帳戶
建立 Azure 儲存體帳戶。 hello 應用程式會使用此帳戶 toostore hello 待辦項目。

1. 登入 hello [Azure 入口網站](https://portal.azure.com/)。
2. 按一下 hello**新增**hello 下方圖示左邊 hello 入口網站，請按一下 **資料 + 儲存體** > **儲存體**。 提供 hello 儲存體帳戶的唯一名稱，並建立新[資源群組](../azure-resource-manager/resource-group-overview.md)它。
   
      ![新增按鈕](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    Hello 儲存體帳戶建立後，hello**通知** 按鈕會閃爍綠色**成功**且 hello 儲存體帳戶的刀鋒視窗已開啟 tooshow 其所屬 toohello 新資源群組建立。
3. 在 hello 儲存體帳戶的刀鋒視窗中，按一下 **設定** > **金鑰**。 將複製 hello 主要存取金鑰 toohello 剪貼簿。
   
    ![存取金鑰][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a>安裝模組及產生樣板
本節中，您會建立新的 Node 應用程式，並使用 npm tooadd 模組封裝。 此應用程式中，您將使用 hello [Express]和[Azure]模組。 hello Express 模組提供節點的模型檢視控制器 」 架構，同時 hello Azure 模組提供連接 toohello 資料表服務。

### <a name="install-express-and-generate-scaffolding"></a>安裝 Express 及產生樣板
1. 從 hello 命令列，建立名為的新目錄**tasklist**和交換器 toothat 目錄。  
2. 輸入下列命令 tooinstall hello Express 模組 hello。
   
        npm install express-generator@4.2.0 -g
   
    根據 hello 的作業系統，您可能需要 tooput 'sudo' hello 命令之前：
   
        sudo npm install express-generator@4.2.0 -g
   
    下列範例類似 toohello 出現 hello 輸出：
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > hello '-g' 參數全域安裝 hello 模組。 這樣一來，我們可以使用**express** toogenerate web 應用程式 scaffolding，而不需要 tootype 中的額外路徑資訊。
   > 
   > 
3. toocreate hello scaffolding hello 應用程式中，輸入 hello **express**命令：
   
        express
   
    hello 這個命令的輸出會出現類似下列範例的 toohello:
   
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
   
    您現在有數個新的目錄和檔案在 hello **tasklist**目錄。

### <a name="install-additional-modules"></a>安裝其他模組
其中一個 hello 檔案， **express**建立是**package.json**。 此檔案包含模組相依性清單。 更新版本中，當您部署 hello 應用程式 tooApp Service Web 應用程式時，此檔案會決定哪一個模組必須安裝在 Azure 上的 toobe。

從命令列的 hello，輸入下列命令 tooinstall hello 模組 hello 中所述的 hello **package.json**檔案。 您可能需要 toouse 'sudo'。

    npm install

hello 這個命令的輸出會出現類似下列範例的 toohello:

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


接下來，輸入下列命令 tooinstall hello hello [azure]，[節點 uuid]， [nconf]和[非同步]模組：

    npm install azure-storage node-uuid async nconf --save

hello **-儲存**旗標加入這些模組 toohello 項目**package.json**檔案。

hello 這個命令的輸出會出現類似下列範例的 toohello:

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-hello-application"></a>建立 hello 應用程式
現在我們已經準備好 toobuild hello 應用程式。

### <a name="create-a-model"></a>建立模型
A*模型*是代表您的應用程式中的 hello 資料的物件。 Hello 應用程式，hello 僅限模型是工作物件，代表 hello 待辦事項清單中的項目。 工作將會擁有 hello 下列欄位：

* PartitionKey
* RowKey
* name (字串)
* category (字串)
* completed (布林值)

**PartitionKey**和**RowKey** hello 表格服務所使用做為資料表的索引鍵。 如需詳細資訊，請參閱[了解 hello 表格服務資料模型](https://msdn.microsoft.com/library/azure/dd179338.aspx)。

1. 在 hello **tasklist**目錄中，建立名為的新目錄**模型**。
2. 在 hello**模型**目錄中，建立新的檔案命名為**task.js**。 這個檔案會包含您的應用程式所建立的 hello 工作 hello 模型。
3. 在 hello hello 開頭**task.js**檔案中加入下列程式碼所需的 tooreference 程式庫的 hello:
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. 加入 hello 下列程式碼 toodefine 和匯出 hello 工作物件。 此物件負責連接 toohello 資料表。
   
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
5. 加入 hello hello 工作物件，在下列程式碼 toodefine 其他方法可讓資料儲存在 hello 資料表之間的互動：
   
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
6. 儲存並關閉 hello **task.js**檔案。

### <a name="create-a-controller"></a>建立控制器
A*控制器*處理 HTTP 要求並呈現 hello HTML 回應。

1. 在 hello **tasklist/路由**目錄中，建立新的檔案命名為**tasklist.js**在文字編輯器中開啟它。
2. 新增下列程式碼太 hello**tasklist.js**。 這會載入 hello azure 與非同步模組所使用的**tasklist.js**。 這也會定義 hello **TaskList**函式，會傳遞 hello 的執行個體**工作**我們先前定義的物件：
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. 定義 **TaskList** 物件。
   
        function TaskList(task) {
          this.task = task;
        }
4. 新增下列方法太 hello**TaskList**:
   
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

### <a name="modify-appjs"></a>修改 app.js
1. 從 hello **tasklist**目錄，請開啟 hello **app.js**檔案。 這個檔案稍早建立的執行 hello **express**命令。
2. 在 hello hello 檔案開頭，加入下列 tooload hello azure 模組、 設定 hello 資料表名稱、 資料分割索引鍵和此範例所使用的設定 hello 儲存體認證的 hello:
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > nconf 會從環境變數或 hello 載入 hello 組態值**config.json**我們將在稍後建立的檔案。
   > 
   > 
3. 在 hello app.js 檔案中，向下捲動的 toowhere 您會看到下列行 hello:
   
        app.use('/', routes);
        app.use('/users', users);
   
    取代 hello 如下所示的程式碼行上方的 hello。 這將會初始化的執行個體<strong>工作</strong>連接 tooyour 儲存體帳戶。 這會傳遞 toohello <strong>TaskList</strong>，就會使用它 toocommunicate 以 hello 表格服務：
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. 儲存 hello **app.js**檔案。

### <a name="modify-hello-index-view"></a>修改 hello 索引檢視表
1. 開啟 hello **tasklist/views/index.jade**文字編輯器中的檔案。
2. 取代下列程式碼的 hello hello 整個 hello 檔案的內容。 這會定義顯示現有工作的檢視，並且包括加入新工作及將現有工作標示為完成的表單。
   
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
3. 儲存並關閉 **index.jade** 檔案。

### <a name="modify-hello-global-layout"></a>修改 hello 全域版面配置
hello **layout.jade**檔案在 hello**檢視**目錄是全域範本的其他**.jade**檔案。 在此步驟中您會修改它 toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap)，也就是可讓您輕鬆 toodesign nice 尋找 web 應用程式的工具組。

下載並解壓縮 hello 檔案[Twitter Bootstrap](http://getbootstrap.com/)。 複製 hello **bootstrap.min.css** hello 啟動程序從檔案**css**資料夾 hello**公用/樣式表**應用程式的目錄。

從 hello**檢視**資料夾中，開啟**layout.jade**並取代 hello 下列中的 hello 整個內容：

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

### <a name="create-a-config-file"></a>建立組態檔
toorun hello 應用程式在本機，我們會將 Azure 儲存體認證放在組態檔。 建立名為 **config.json* * 以下列 JSON hello:

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

取代**儲存體帳戶名稱**hello hello 儲存體名稱與您稍早建立帳戶，並取代**儲存體存取金鑰**與 hello 儲存體帳戶的主要存取金鑰。 例如：

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

儲存這個檔案*一個目錄層級較高*比 hello **tasklist**目錄下，像這樣：

    parent/
      |-- config.json
      |-- tasklist/

執行此作業的 hello 原因是 tooavoid 簽入原始檔控制 hello 組態檔位置可能會變成公用。 當我們將部署 hello 應用程式 tooAzure 時，我們將使用環境變數，而不是在組態檔。

## <a name="run-hello-application-locally"></a>在本機執行 hello 應用程式
tootest hello 應用程式在本機電腦，執行下列步驟的 hello:

1. 從命令列的 hello，變更目錄 toohello **tasklist**目錄。
2. 使用下列命令 toolaunch hello 本機應用程式的 hello:
   
        npm start
3. 開啟網頁瀏覽器並瀏覽 toohttp://127.0.0.1:3000。
   
    下列範例網頁類似 toohello 隨即出現。
   
    ![A webpage displaying an empty tasklist][node-table-finished]
4. toocreate 新的待辦項目中，輸入名稱和類別目錄，然後按一下**加入項目**。 
5. 工作完成時，請檢查 toomark**完成**按一下**更新工作**。
   
    ![項目的影像 hello 新 hello 清單中的工作][node-table-list-items]

即使在本機執行 hello 應用程式，它會儲存 hello 資料 hello Azure 表格服務中。

## <a name="deploy-your-application-tooazure"></a>部署應用程式 tooAzure
本節中的 hello 步驟使用 App Service 中的 hello Azure 命令列工具 toocreate 新的 web 應用程式，然後再使用 Git toodeploy 您的應用程式。 tooperform 這些步驟，您必須具有 Azure 訂用帳戶。

> [!NOTE]
> 也可以使用 hello 執行這些步驟[Azure 入口網站](https://portal.azure.com/)。 請參閱 [在 Azure App Service 中建置和部署 Node.js Web 應用程式]。
> 
> 如果這是您已建立 hello 第一個 web 應用程式，您必須使用 hello Azure 入口網站 toodeploy 此應用程式。
> 
> 

tooget 啟動，安裝 hello [Azure CLI]輸入 hello hello 命令列中的下列命令：

    npm install azure-cli -g

### <a name="import-publishing-settings"></a>匯入發佈設定
在此步驟中，您將會下載包含您訂用帳戶相關資訊的檔案。

1. 輸入下列命令的 hello:
   
        azure login
   
    此命令會啟動瀏覽器並瀏覽 toohello 下載頁面。 如果出現提示，請登入與您 Azure 訂用帳戶相關聯的 hello 帳戶。
   
    <!-- ![hello download page][download-publishing-settings] -->
   
    hello 檔案下載，而開始如果不存在，您可以按一下 hello hello hello 頁面 toomanually 下載 hello 檔案開頭處的連結。 儲存 hello 檔案並註記 hello 檔案路徑。
2. 輸入下列命令 tooimport hello 設定 hello:
   
        azure account import <path-to-file>
   
    指定 hello hello hello 上一個步驟中發佈您下載的設定檔的路徑和檔案名稱。
3. 匯入 hello 設定之後，刪除 hello 的發行設定檔。 這個檔案已經不再需要，而且包含與 Azure 訂用帳戶相關的機密資訊。

### <a name="create-an-app-service-web-app"></a>建立 App Service Web 應用程式
1. 從命令列的 hello，變更目錄 toohello **tasklist**目錄。
2. 使用下列命令 toocreate 新的 web 應用程式的 hello。
   
        azure site create --git
   
    系統會提示您 hello web 應用程式名稱和位置。 提供唯一的名稱，然後選取 hello 與 Azure 儲存體帳戶相同的地理位置。
   
    hello`--git`參數在 Azure 上建立 Git 儲存機制，此 web 應用程式。 它也會初始化 hello 目前目錄中的 Git 儲存機制有無存在，以及新增[Git 遠端]名為 'azure'，這是使用的 toopublish hello 應用程式 tooAzure。 最後，它會建立**web.config**檔案，其中包含 Azure toohost 節點應用程式所使用的設定。 如果您省略 hello`--git`參數，但 hello 目錄中包含的 Git 儲存機制、 hello 命令仍會建立 'azure' hello 遠端。
   
    此命令完成後，您會看到類似 toohello 下列輸出。 請注意該 hello 行首**網站端建立**包含 hello hello web 應用程式的 URL。
   
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
   > 如果這是 hello 第一個 App Service web 應用程式為您的訂用帳戶，您將會指示 toouse hello Azure 入口網站 toocreate hello web 應用程式。 如需詳細資訊，請參閱 [在 Azure App Service 中建置和部署 Node.js Web 應用程式]。
   > 
   > 

### <a name="set-environment-variables"></a>設定環境變數
在此步驟中，您將加入在 Azure 上的環境變數 tooyour web 應用程式組態。
從 hello 命令列中，輸入 hello 下列內容：

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


取代 **<storage account name>**  hello hello 儲存體名稱與您稍早建立帳戶，並取代 **<storage access key>** 與 hello 儲存體帳戶的主要存取金鑰。 （您稍早建立的 hello config.json 檔案使用相同值的 hello）。

或者，您可以設定環境變數中 hello [Azure 入口網站](https://portal.azure.com/):

1. 開啟 hello web 應用程式的刀鋒視窗中，依序按一下**瀏覽** > **Web 應用程式**> web 應用程式名稱。
2. 在您的 Web 應用程式刀鋒視窗中，按一下 [所有設定]  >  [應用程式設定]。
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. 捲動 toohello**應用程式設定**區段，並新增 hello 索引鍵/值組。
   
     ![應用程式設定](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. 按一下 [儲存] 。

### <a name="publish-hello-application"></a>發行 hello 應用程式
toopublish hello 應用程式時，認可 hello 程式碼檔案 tooGit，並接著推送 tooazure/master。

1. 設定您的部署認證。
   
        azure site deployment user set <name> <password>
2. 新增並認可您的應用程式檔案。
   
        git add .
        git commit -m "adding files"
3. 推送 hello 認可 toohello App Service web 應用程式：
   
        git push azure master
   
    使用**主要**為 hello 目標分支。 在 hello 部署的 hello 結束時，您會看到陳述式的類似 toohello，下列範例：
   
        toohttps://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. Hello 推入作業完成後，請瀏覽先前由 hello toohello web 應用程式 URL`azure create site`命令 tooview 您的應用程式。

## <a name="next-steps"></a>後續步驟
雖然這篇文章中的 hello 步驟說明使用 hello 表格服務 toostore 資訊，您也可以使用[MongoDB](https://mlab.com/azure/)。 

## <a name="additional-resources"></a>其他資源
[Azure CLI]

## <a name="whats-changed"></a>變更的項目
* 從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)

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
