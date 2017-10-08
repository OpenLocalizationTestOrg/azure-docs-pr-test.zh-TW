---
title: "Node.js web 應用程式的 Azure Cosmos DB aaaBuild |Microsoft 文件"
description: "本教學課程中 Node.js 探討 Azure 網站上裝載 toouse Node.js Express web 應用程式的 Microsoft Azure Cosmos DB toostore 及存取資料的方式。"
keywords: "應用程式開發, 資料庫教學課程, 了解 node.js, node.js 教學課程"
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 9da9e63b-e76a-434e-96dd-195ce2699ef3
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/14/2017
ms.author: mimig
ms.openlocfilehash: 31194dccf37eef69d2219b0d8328a88d434f79b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="_Toc395783175"></a>使用 Azure Cosmos DB 來建置 Node.js Web 應用程式
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

此 Node.js 教學課程會示範如何 toouse Azure Cosmos DB 和 hello DocumentDB API toostore 和存取資料，從 Node.js Express 應用程式裝載在 Azure 網站上。 您會建置一個可供建立、擷取及完成工作的簡單網頁型工作管理應用程式 (待辦事項應用程式)。 hello 工作會儲存為 Azure Cosmos DB 中的 JSON 文件。 本教學課程將引導您完成 hello 建立及部署的 hello 應用程式，並說明每個片段中的情況。

![Hello 這個 Node.js 教學課程中建立的 我的 Todo 清單應用程式的螢幕擷取畫面](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

不會有時間 toocomplete hello 教學課程，而且只想 tooget hello 完整的解決方案嗎？ 不是問題，您可以取得 hello 完整的範例方案，從[GitHub][GitHub]。 只可以讀取 hello[讀我檔案](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md)檔案，如需如何 toorun hello 應用程式的指示。

## <a name="_Toc395783176"></a>必要條件
> [!TIP]
> 本 Node.js 教學課程假設您先前已有些許使用 Node.js 和 Azure 網站的經驗。
> 
> 

這篇文章中的 hello 指示之前，您應該確定您擁有 hello 下列：

* 使用中的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。

   或

   Hello 的本機安裝[Azure Cosmos DB 模擬器](local-emulator.md)(僅限 Windows)。
* [Node.js][Node.js] v0.10.29 版或更高版本。
* [Express 產生器](http://www.expressjs.com/starter/generator.html) (您可以透過 `npm install express-generator -g` 進行安裝)
* [Git][Git]。

## <a name="_Toc395637761"></a>步驟 1：建立 Azure Cosmos DB 資料庫帳戶
我們將從建立 Azure Cosmos DB 帳戶開始著手。 如果您已經有帳戶，或如果您使用 hello Azure Cosmos DB 模擬器本教學課程中，您可以跳過[步驟 2： 建立新的 Node.js 應用程式](#_Toc395783178)。

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <a name="_Toc395783178"></a>步驟 2 - 建立新的 Node.js 應用程式
現在讓我們了解 toocreate 基本的 Hello World Node.js 專案使用 hello [Express](http://expressjs.com/)架構。

1. 開啟您最愛的終端機，例如 hello Node.js 命令提示字元。
2. 瀏覽 toohello 目錄中，您想要 toostore hello 新應用程式。
3. 使用新的應用程式呼叫 hello 快速產生器 toogenerate **todo**。
   
        express todo
4. 開啟您的新 **todo** 目錄並安裝相依性。
   
        cd todo
        npm install
5. 執行新的應用程式。
   
        npm start
6. 您可以檢視新的應用程式瀏覽您的瀏覽器太[http://localhost:3000](http://localhost:3000)。
   
    ![了解 Node.js-hello 瀏覽器視窗中的 Hello World 應用程式的螢幕擷取畫面](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    然後，toostop hello 應用程式，請按 CTRL + C hello terminal 視窗中，然後按一下**y** tooterminate hello 批次作業。

## <a name="_Toc395783179"></a>步驟 3：安裝其他模組
hello **package.json**檔案是建立在 hello hello 專案根目錄中的 hello 檔案的其中一個。 這個檔案包含 Node.js 應用程式所需的其他模組清單。 稍後，當您部署此應用程式 tooAzure 網站時，這個檔案是使用的 toodetermine 哪些模組需要 toobe Azure toosupport 您的應用程式安裝。 我們仍需要 tooinstall 兩個封裝在本教學課程。

1. 在 hello 終端機安裝 hello**非同步**透過 npm 模組。
   
        npm install async --save
2. 安裝 hello **documentdb**透過 npm 模組。 這是其中所有的 hello Azure Cosmos DB magic 發生 hello 模組。
   
        npm install documentdb --save
3. 快速檢查 hello **package.json** hello 應用程式檔案應該會顯示 hello 其他模組。 這個檔案會告訴 Azure 哪些封裝 toodownload，以及執行您的應用程式時安裝。 它應該類似下列的 hello 範例。
   
        {
          "name": "todo",
          "version": "0.0.0",
          "private": true,
          "scripts": {
            "start": "node ./bin/www"
          },
          "dependencies": {
            "async": "^2.1.4",
            "body-parser": "~1.15.2",
            "cookie-parser": "~1.4.3",
            "debug": "~2.2.0",
            "documentdb": "^1.10.0",
            "express": "~4.14.0",
            "jade": "~1.11.0",
            "morgan": "~1.7.0",
            "serve-favicon": "~2.3.0"
          }
        }
   
    這會讓 Node (之後則是 Azure) 知道您的應用程式需要仰賴這些額外模組。

## <a name="_Toc395783180"></a>步驟 4： 使用 node 應用程式中的 hello Azure Cosmos DB 服務
會處理所有 hello 初始安裝和組態，現在讓我們 get toowhy 向我們在這裡，而這就是有些程式碼使用 Azure Cosmos DB toowrite。

### <a name="create-hello-model"></a>建立 hello 模型
1. 在 hello 專案目錄中，建立名為的新目錄**模型**在 hello 與 hello package.json 檔案相同的目錄。
2. 在 hello**模型**目錄中，建立新的檔案命名為**taskDao.js**。 這個檔案會包含我們的應用程式所建立的 hello 工作 hello 模型。
3. 在 hello 相同**模型**目錄中，建立名為另一個新檔案**docdbUtils.js**。 這個檔案會包含一些實用、可重複使用，適用於整個應用程式的程式碼。 
4. 複製 hello 中下列程式碼太**docdbUtils.js**
   
        var DocumentDBClient = require('documentdb').DocumentClient;
   
        var DocDBUtils = {
            getOrCreateDatabase: function (client, databaseId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id= @id',
                    parameters: [{
                        name: '@id',
                        value: databaseId
                    }]
                };
   
                client.queryDatabases(querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        if (results.length === 0) {
                            var databaseSpec = {
                                id: databaseId
                            };
   
                            client.createDatabase(databaseSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            },
   
            getOrCreateCollection: function (client, databaseLink, collectionId, callback) {
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id=@id',
                    parameters: [{
                        name: '@id',
                        value: collectionId
                    }]
                };               
   
                client.queryCollections(databaseLink, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {        
                        if (results.length === 0) {
                            var collectionSpec = {
                                id: collectionId
                            };
   
                            client.createCollection(databaseLink, collectionSpec, function (err, created) {
                                callback(null, created);
                            });
   
                        } else {
                            callback(null, results[0]);
                        }
                    }
                });
            }
        };
   
        module.exports = DocDBUtils;
   
5. 儲存並關閉 hello **docdbUtils.js**檔案。
6. 在 hello hello 開頭**taskDao.js**檔案中加入下列程式碼 tooreference hello hello **DocumentDBClient**和 hello **docdbUtils.js**前面所建立：
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. 接下來，您會加入程式碼 toodefine 以及匯出 hello 工作物件。 這是負責初始化我們工作的物件和設定 hello 資料庫，我們將使用的文件集合。
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. 接下來，新增 hello hello 工作物件，在下列程式碼 toodefine 其他方法可讓 Azure Cosmos DB 中所儲存的資料互動。
   
        TaskDao.prototype = {
            init: function (callback) {
                var self = this;
   
                docdbUtils.getOrCreateDatabase(self.client, self.databaseId, function (err, db) {
                    if (err) {
                        callback(err);
                    } else {
                        self.database = db;
                        docdbUtils.getOrCreateCollection(self.client, self.database._self, self.collectionId, function (err, coll) {
                            if (err) {
                                callback(err);
   
                            } else {
                                self.collection = coll;
                            }
                        });
                    }
                });
            },
   
            find: function (querySpec, callback) {
                var self = this;
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results);
                    }
                });
            },
   
            addItem: function (item, callback) {
                var self = this;
   
                item.date = Date.now();
                item.completed = false;
   
                self.client.createDocument(self.collection._self, item, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, doc);
                    }
                });
            },
   
            updateItem: function (itemId, callback) {
                var self = this;
   
                self.getItem(itemId, function (err, doc) {
                    if (err) {
                        callback(err);
   
                    } else {
                        doc.completed = true;
   
                        self.client.replaceDocument(doc._self, doc, function (err, replaced) {
                            if (err) {
                                callback(err);
   
                            } else {
                                callback(null, replaced);
                            }
                        });
                    }
                });
            },
   
            getItem: function (itemId, callback) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.id = @id',
                    parameters: [{
                        name: '@id',
                        value: itemId
                    }]
                };
   
                self.client.queryDocuments(self.collection._self, querySpec).toArray(function (err, results) {
                    if (err) {
                        callback(err);
   
                    } else {
                        callback(null, results[0]);
                    }
                });
            }
        };
9. 儲存並關閉 hello **taskDao.js**檔案。 

### <a name="create-hello-controller"></a>建立 hello 控制站
1. 在 hello**路由**您專案的目錄建立新的檔案命名為**tasklist.js**。 
2. 新增下列程式碼太 hello**tasklist.js**。 這會載入 hello DocumentDBClient 和非同步模組，可供用**tasklist.js**。 這也會定義 hello **TaskList**函式，會傳遞 hello 的執行個體**工作**我們先前定義的物件：
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. 繼續加入 toohello **tasklist.js**檔案加上使用過的 hello 方法**showTasks，addTask**，和**completeTasks**:
   
        TaskList.prototype = {
            showTasks: function (req, res) {
                var self = this;
   
                var querySpec = {
                    query: 'SELECT * FROM root r WHERE r.completed=@completed',
                    parameters: [{
                        name: '@completed',
                        value: false
                    }]
                };
   
                self.taskDao.find(querySpec, function (err, items) {
                    if (err) {
                        throw (err);
                    }
   
                    res.render('index', {
                        title: 'My ToDo List ',
                        tasks: items
                    });
                });
            },
   
            addTask: function (req, res) {
                var self = this;
                var item = req.body;
   
                self.taskDao.addItem(item, function (err) {
                    if (err) {
                        throw (err);
                    }
   
                    res.redirect('/');
                });
            },
   
            completeTask: function (req, res) {
                var self = this;
                var completedTasks = Object.keys(req.body);
   
                async.forEach(completedTasks, function taskIterator(completedTask, callback) {
                    self.taskDao.updateItem(completedTask, function (err) {
                        if (err) {
                            callback(err);
                        } else {
                            callback(null);
                        }
                    });
                }, function goHome(err) {
                    if (err) {
                        throw err;
                    } else {
                        res.redirect('/');
                    }
                });
            }
        };
4. 儲存並關閉 hello **tasklist.js**檔案。

### <a name="add-configjs"></a>新增 config.js
1. 在您的專案目錄中，建立名為 **config.js**的新檔案。
2. Hello 太之後加入**config.js**。 這會定義組態設定和我們的應用程式所需的值。
   
        var config = {}
   
        config.host = process.env.HOST || "[hello URI value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[hello PRIMARY KEY value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. 在 hello **config.js**檔案，更新 hello 值的主應用程式和使用您的 Azure Cosmos DB 帳戶上 hello hello 金鑰刀鋒視窗中的 hello 值 AUTH_KEY [Microsoft Azure 入口網站](https://portal.azure.com)。
4. 儲存並關閉 hello **config.js**檔案。

### <a name="modify-appjs"></a>修改 app.js
1. 在 hello 專案目錄中，開啟 hello **app.js**檔案。 建立 hello Express web 應用程式時，稍早建立此檔案。
2. 新增下列程式碼 toohello 頂端的 hello **app.js**
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. 此程式碼定義 hello 設定檔 toobe 使用，然後進行 tooread 值超出此檔案置於很快，我們將使用一些變數。
4. 取代下列兩行中的 hello **app.js**檔案：
   
        app.use('/', index);
        app.use('/users', users); 
   
      以下列程式碼片段的 hello:
   
        var docDbClient = new DocumentDBClient(config.host, {
            masterKey: config.authKey
        });
        var taskDao = new TaskDao(docDbClient, config.databaseId, config.collectionId);
        var taskList = new TaskList(taskDao);
        taskDao.init();
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
        app.set('view engine', 'jade');
5. 這幾行定義的新執行個體我們**TaskDao**物件，並將新的連接 tooAzure Cosmos DB (使用 hello 值讀取 hello **config.js**)、 初始化 hello 工作物件，然後再繫結表單動作toomethods 上的我們**TaskList**控制站。 
6. 最後，儲存並關閉 hello **app.js**檔案中，我們即將結束。

## <a name="_Toc395783181"></a>步驟 5：建置使用者介面
現在讓我們來開啟我們注意 toobuilding hello 的使用者介面，讓使用者可以實際互動我們的應用程式。 hello Express 應用程式，我們建立了使用**Jade**做為 hello 檢視引擎。 如需 Jade 的詳細資訊，請參閱太[http://jade-lang.com/](http://jade-lang.com/)。

1. hello **layout.jade**檔案在 hello**檢視**目錄作為全域範本其他**.jade**檔案。 在此步驟中您會修改它 toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap)，這是一項工具組，可讓您輕鬆 toodesign nice 尋找網站。 
2. 開啟 hello **layout.jade**檔案位於 hello**檢視**hello 下列資料夾和取代 hello 內容：

    ```
    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body
        nav.navbar.navbar-inverse.navbar-fixed-top
          div.navbar-header
            a.navbar-brand(href='#') My Tasks
        block content
        script(src='//ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js')
        script(src='//ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js')
    ```

    這實際上會告知 hello **Jade**引擎 toorender 一些 HTML 應用程式，並建立**區塊**呼叫**內容**我們可以在其中提供我們內容 hello 版面配置頁面。

    儲存並關閉此 **layout.jade** 檔案。

3. 現在開啟 hello **index.jade**檔案，供我們的應用程式，並取代 hello 下列中的 hello hello 檔案內容的 hello 檢視：
   
        extends layout
        block content
           h1 #{title}
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
                     td #{task.name}
                     td #{task.category}
                     - var date  = new Date(task.date);
                     - var day   = date.getDate();
                     - var month = date.getMonth() + 1;
                     - var year  = date.getFullYear();
                     td #{month + "/" + day + "/" + year}
                     td
                       input(type="checkbox", name="#{task.id}", value="#{!task.completed}", checked=task.completed)
             button.btn.btn-primary(type="submit") Update tasks
           hr
           form.well(action="/addtask", method="post")
             .form-group
               label(for="name") Item Name:
               input.form-control(name="name", type="textbox")
             .form-group
               label(for="category") Item Category:
               input.form-control(name="category", type="textbox")
             br
             button.btn(type="submit") Add item
   

這會擴充版面配置，並提供 hello 內容**內容**預留位置我們了解在 hello **layout.jade**稍早檔案。
   
在此配置中，我們建立了兩個 HTML 表單。

hello 第一種形式包含資料表的資料和按鈕，讓我們 tooupdate 項目藉由公佈太**/completetask**我們控制站的方法。
    
hello 第二個表單包含兩個輸入的欄位和一個按鈕，讓我們 toocreate 新項目藉由公佈太**/addtask**我們控制站的方法。

這應該是所有我們需要以我們的應用程式 toowork。

## <a name="_Toc395783181"></a>步驟 6：在本機執行您的應用程式
1. tootest hello 應用程式，您的本機電腦上執行`npm start`hello toostart 終端機應用程式，然後重新整理您[http://localhost:3000](http://localhost:3000)瀏覽器頁面。 hello 頁面現在看起來應該像下面的 hello 影像：
   
    ![Hello MyTodo 清單應用程式，在瀏覽器視窗的螢幕擷取畫面](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > 如果您收到 hello layout.jade 檔案或 hello index.jade 檔案中的 hello 縮排的相關錯誤，請確認這兩個檔案中的 hello 前兩行靠左對齊，不含空格。 如果有空格 hello 前兩個行之前，將它們移除，請儲存兩個檔案，然後重新整理瀏覽器視窗。 

2. 使用 hello 項目、 項目名稱和類別目錄欄位 tooenter 新工作，然後按一下**加入項目**。 便會使用這些屬性在 Azure Cosmos DB 中建立文件。 
3. hello 頁面應該更新新建立 hello ToDo 清單中的項目 toodisplay hello。
   
    ![使用新的項目 hello ToDo 清單中的 hello 應用程式的螢幕擷取畫面](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. toocomplete 項工作中，只會檢查 hello 完整資料行中的 hello 核取方塊，然後按一下**更新工作**。 這會更新您已建立的 hello 文件。

5. toostop hello 應用程式中，按 CTRL + C hello terminal 視窗中，然後按一下**Y** tooterminate hello 批次作業。

## <a name="_Toc395783182"></a>步驟 7： 部署您的應用程式開發專案 tooAzure 網站
1. 如果您還沒有這麼做，請為您的 Azure 網站提供一個 Git 儲存機制。 您可以找到指示如何 toodo 這在 hello[應用程式服務的本機 Git 部署 tooAzure](../app-service-web/app-service-deploy-local-git.md)主題。
2. 新增您的 Azure 網站做為 Git 遠端。
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. 藉由推送 toohello 遠端部署。
   
        git push azure master
4. 幾秒後，Git 便會發佈 Web 應用程式並啟動瀏覽器，您可以在瀏覽器中看到您方便好用的應用程式已在 Azure 中執行！

    恭喜！ 您剛才已建置第一個 Node.js Express Web 應用程式使用 Azure Cosmos DB，並發佈它 tooAzure 網站。

    如果您想 toodownload 或 toohello 完整參考的應用程式，請參閱本教學課程中，它可以從下載[GitHub][GitHub]。

## <a name="_Toc395637775"></a>接續步驟

* 想 tooperform 規模和效能測試以 Azure Cosmos DB 嗎？ 請參閱 [Azure Cosmos DB 的效能和規模測試](performance-testing.md)
* 了解如何太[監視 Azure Cosmos DB 帳戶](monitor-accounts.md)。
* 執行查詢，根據我們的範例資料集，在 hello[查詢遊樂場](https://www.documentdb.com/sql/demo)。
* 瀏覽 hello [Azure Cosmos DB 文件集](https://docs.microsoft.com/azure/documentdb/)。

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app

