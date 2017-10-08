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
# <span data-ttu-id="f3c8e-104"><a name="_Toc395783175"></a>使用 Azure Cosmos DB 來建置 Node.js Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="f3c8e-104"><a name="_Toc395783175"></a>Build a Node.js web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f3c8e-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f3c8e-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="f3c8e-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="f3c8e-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="f3c8e-107">Java</span><span class="sxs-lookup"><span data-stu-id="f3c8e-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="f3c8e-108">Python</span><span class="sxs-lookup"><span data-stu-id="f3c8e-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="f3c8e-109">此 Node.js 教學課程會示範如何 toouse Azure Cosmos DB 和 hello DocumentDB API toostore 和存取資料，從 Node.js Express 應用程式裝載在 Azure 網站上。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-109">This Node.js tutorial shows you how toouse Azure Cosmos DB and hello DocumentDB API toostore and access data from a Node.js Express application hosted on Azure Websites.</span></span> <span data-ttu-id="f3c8e-110">您會建置一個可供建立、擷取及完成工作的簡單網頁型工作管理應用程式 (待辦事項應用程式)。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-110">You build a simple web-based task-management application, a ToDo app, that allows creating, retrieving, and completing tasks.</span></span> <span data-ttu-id="f3c8e-111">hello 工作會儲存為 Azure Cosmos DB 中的 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-111">hello tasks are stored as JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="f3c8e-112">本教學課程將引導您完成 hello 建立及部署的 hello 應用程式，並說明每個片段中的情況。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-112">This tutorial walks you through hello creation and deployment of hello app and explains what's happening in each snippet.</span></span>

![Hello 這個 Node.js 教學課程中建立的 我的 Todo 清單應用程式的螢幕擷取畫面](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

<span data-ttu-id="f3c8e-114">不會有時間 toocomplete hello 教學課程，而且只想 tooget hello 完整的解決方案嗎？</span><span class="sxs-lookup"><span data-stu-id="f3c8e-114">Don't have time toocomplete hello tutorial and just want tooget hello complete solution?</span></span> <span data-ttu-id="f3c8e-115">不是問題，您可以取得 hello 完整的範例方案，從[GitHub][GitHub]。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-115">Not a problem, you can get hello complete sample solution from [GitHub][GitHub].</span></span> <span data-ttu-id="f3c8e-116">只可以讀取 hello[讀我檔案](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md)檔案，如需如何 toorun hello 應用程式的指示。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-116">Just read hello [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) file for instructions on how toorun hello app.</span></span>

## <span data-ttu-id="f3c8e-117"><a name="_Toc395783176"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="f3c8e-117"><a name="_Toc395783176"></a>Prerequisites</span></span>
> [!TIP]
> <span data-ttu-id="f3c8e-118">本 Node.js 教學課程假設您先前已有些許使用 Node.js 和 Azure 網站的經驗。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-118">This Node.js tutorial assumes that you have some prior experience using Node.js and Azure Websites.</span></span>
> 
> 

<span data-ttu-id="f3c8e-119">這篇文章中的 hello 指示之前，您應該確定您擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="f3c8e-119">Before following hello instructions in this article, you should ensure that you have hello following:</span></span>

* <span data-ttu-id="f3c8e-120">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-120">An active Azure account.</span></span> <span data-ttu-id="f3c8e-121">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="f3c8e-122">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

   <span data-ttu-id="f3c8e-123">或</span><span class="sxs-lookup"><span data-stu-id="f3c8e-123">OR</span></span>

   <span data-ttu-id="f3c8e-124">Hello 的本機安裝[Azure Cosmos DB 模擬器](local-emulator.md)(僅限 Windows)。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-124">A local installation of hello [Azure Cosmos DB Emulator](local-emulator.md) (Windows only).</span></span>
* <span data-ttu-id="f3c8e-125">[Node.js][Node.js] v0.10.29 版或更高版本。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-125">[Node.js][Node.js] version v0.10.29 or higher.</span></span>
* <span data-ttu-id="f3c8e-126">[Express 產生器](http://www.expressjs.com/starter/generator.html) (您可以透過 `npm install express-generator -g` 進行安裝)</span><span class="sxs-lookup"><span data-stu-id="f3c8e-126">[Express generator](http://www.expressjs.com/starter/generator.html) (you can install this via `npm install express-generator -g`)</span></span>
* <span data-ttu-id="f3c8e-127">[Git][Git]。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-127">[Git][Git].</span></span>

## <span data-ttu-id="f3c8e-128"><a name="_Toc395637761"></a>步驟 1：建立 Azure Cosmos DB 資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="f3c8e-128"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="f3c8e-129">我們將從建立 Azure Cosmos DB 帳戶開始著手。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-129">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="f3c8e-130">如果您已經有帳戶，或如果您使用 hello Azure Cosmos DB 模擬器本教學課程中，您可以跳過[步驟 2： 建立新的 Node.js 應用程式](#_Toc395783178)。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-130">If you already have an account or if you are using hello Azure Cosmos DB Emulator for this tutorial, you can skip too[Step 2: Create a new Node.js application](#_Toc395783178).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="f3c8e-131"><a name="_Toc395783178"></a>步驟 2 - 建立新的 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="f3c8e-131"><a name="_Toc395783178"></a>Step 2: Create a new Node.js application</span></span>
<span data-ttu-id="f3c8e-132">現在讓我們了解 toocreate 基本的 Hello World Node.js 專案使用 hello [Express](http://expressjs.com/)架構。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-132">Now let's learn toocreate a basic Hello World Node.js project using hello [Express](http://expressjs.com/) framework.</span></span>

1. <span data-ttu-id="f3c8e-133">開啟您最愛的終端機，例如 hello Node.js 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-133">Open your favorite terminal, such as hello Node.js command prompt.</span></span>
2. <span data-ttu-id="f3c8e-134">瀏覽 toohello 目錄中，您想要 toostore hello 新應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-134">Navigate toohello directory in which you'd like toostore hello new application.</span></span>
3. <span data-ttu-id="f3c8e-135">使用新的應用程式呼叫 hello 快速產生器 toogenerate **todo**。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-135">Use hello express generator toogenerate a new application called **todo**.</span></span>
   
        express todo
4. <span data-ttu-id="f3c8e-136">開啟您的新 **todo** 目錄並安裝相依性。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-136">Open your new **todo** directory and install dependencies.</span></span>
   
        cd todo
        npm install
5. <span data-ttu-id="f3c8e-137">執行新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-137">Run your new application.</span></span>
   
        npm start
6. <span data-ttu-id="f3c8e-138">您可以檢視新的應用程式瀏覽您的瀏覽器太[http://localhost:3000](http://localhost:3000)。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-138">You can view your new application by navigating your browser too[http://localhost:3000](http://localhost:3000).</span></span>
   
    ![了解 Node.js-hello 瀏覽器視窗中的 Hello World 應用程式的螢幕擷取畫面](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    <span data-ttu-id="f3c8e-140">然後，toostop hello 應用程式，請按 CTRL + C hello terminal 視窗中，然後按一下**y** tooterminate hello 批次作業。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-140">Then, toostop hello application, press CTRL+C in hello terminal window and then click **y** tooterminate hello batch job.</span></span>

## <span data-ttu-id="f3c8e-141"><a name="_Toc395783179"></a>步驟 3：安裝其他模組</span><span class="sxs-lookup"><span data-stu-id="f3c8e-141"><a name="_Toc395783179"></a>Step 3: Install additional modules</span></span>
<span data-ttu-id="f3c8e-142">hello **package.json**檔案是建立在 hello hello 專案根目錄中的 hello 檔案的其中一個。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-142">hello **package.json** file is one of hello files created in hello root of hello project.</span></span> <span data-ttu-id="f3c8e-143">這個檔案包含 Node.js 應用程式所需的其他模組清單。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-143">This file contains a list of additional modules that are required for your Node.js application.</span></span> <span data-ttu-id="f3c8e-144">稍後，當您部署此應用程式 tooAzure 網站時，這個檔案是使用的 toodetermine 哪些模組需要 toobe Azure toosupport 您的應用程式安裝。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-144">Later, when you deploy this application tooAzure Websites, this file is used toodetermine which modules need toobe installed on Azure toosupport your application.</span></span> <span data-ttu-id="f3c8e-145">我們仍需要 tooinstall 兩個封裝在本教學課程。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-145">We still need tooinstall two more packages for this tutorial.</span></span>

1. <span data-ttu-id="f3c8e-146">在 hello 終端機安裝 hello**非同步**透過 npm 模組。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-146">Back in hello terminal, install hello **async** module via npm.</span></span>
   
        npm install async --save
2. <span data-ttu-id="f3c8e-147">安裝 hello **documentdb**透過 npm 模組。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-147">Install hello **documentdb** module via npm.</span></span> <span data-ttu-id="f3c8e-148">這是其中所有的 hello Azure Cosmos DB magic 發生 hello 模組。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-148">This is hello module where all hello Azure Cosmos DB magic happens.</span></span>
   
        npm install documentdb --save
3. <span data-ttu-id="f3c8e-149">快速檢查 hello **package.json** hello 應用程式檔案應該會顯示 hello 其他模組。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-149">A quick check of hello **package.json** file of hello application should show hello additional modules.</span></span> <span data-ttu-id="f3c8e-150">這個檔案會告訴 Azure 哪些封裝 toodownload，以及執行您的應用程式時安裝。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-150">This file will tell Azure which packages toodownload and install when running your application.</span></span> <span data-ttu-id="f3c8e-151">它應該類似下列的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-151">It should resemble hello example below.</span></span>
   
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
   
    <span data-ttu-id="f3c8e-152">這會讓 Node (之後則是 Azure) 知道您的應用程式需要仰賴這些額外模組。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-152">This tells Node (and Azure later) that your application depends on these additional modules.</span></span>

## <span data-ttu-id="f3c8e-153"><a name="_Toc395783180"></a>步驟 4： 使用 node 應用程式中的 hello Azure Cosmos DB 服務</span><span class="sxs-lookup"><span data-stu-id="f3c8e-153"><a name="_Toc395783180"></a>Step 4: Using hello Azure Cosmos DB service in a node application</span></span>
<span data-ttu-id="f3c8e-154">會處理所有 hello 初始安裝和組態，現在讓我們 get toowhy 向我們在這裡，而這就是有些程式碼使用 Azure Cosmos DB toowrite。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-154">That takes care of all hello initial setup and configuration, now let’s get down toowhy we’re here, and that’s toowrite some code using Azure Cosmos DB.</span></span>

### <a name="create-hello-model"></a><span data-ttu-id="f3c8e-155">建立 hello 模型</span><span class="sxs-lookup"><span data-stu-id="f3c8e-155">Create hello model</span></span>
1. <span data-ttu-id="f3c8e-156">在 hello 專案目錄中，建立名為的新目錄**模型**在 hello 與 hello package.json 檔案相同的目錄。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-156">In hello project directory, create a new directory named **models** in hello same directory as hello package.json file.</span></span>
2. <span data-ttu-id="f3c8e-157">在 hello**模型**目錄中，建立新的檔案命名為**taskDao.js**。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-157">In hello **models** directory, create a new file named **taskDao.js**.</span></span> <span data-ttu-id="f3c8e-158">這個檔案會包含我們的應用程式所建立的 hello 工作 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-158">This file will contain hello model for hello tasks created by our application.</span></span>
3. <span data-ttu-id="f3c8e-159">在 hello 相同**模型**目錄中，建立名為另一個新檔案**docdbUtils.js**。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-159">In hello same **models** directory, create another new file named **docdbUtils.js**.</span></span> <span data-ttu-id="f3c8e-160">這個檔案會包含一些實用、可重複使用，適用於整個應用程式的程式碼。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-160">This file will contain some useful, reusable, code that we will use throughout our application.</span></span> 
4. <span data-ttu-id="f3c8e-161">複製 hello 中下列程式碼太**docdbUtils.js**</span><span class="sxs-lookup"><span data-stu-id="f3c8e-161">Copy hello following code in too**docdbUtils.js**</span></span>
   
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
   
5. <span data-ttu-id="f3c8e-162">儲存並關閉 hello **docdbUtils.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-162">Save and close hello **docdbUtils.js** file.</span></span>
6. <span data-ttu-id="f3c8e-163">在 hello hello 開頭**taskDao.js**檔案中加入下列程式碼 tooreference hello hello **DocumentDBClient**和 hello **docdbUtils.js**前面所建立：</span><span class="sxs-lookup"><span data-stu-id="f3c8e-163">At hello beginning of hello **taskDao.js** file, add hello following code tooreference hello **DocumentDBClient** and hello **docdbUtils.js** we created above:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. <span data-ttu-id="f3c8e-164">接下來，您會加入程式碼 toodefine 以及匯出 hello 工作物件。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-164">Next, you will add code toodefine and export hello Task object.</span></span> <span data-ttu-id="f3c8e-165">這是負責初始化我們工作的物件和設定 hello 資料庫，我們將使用的文件集合。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-165">This is responsible for initializing our Task object and setting up hello Database and Document Collection we will use.</span></span>
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. <span data-ttu-id="f3c8e-166">接下來，新增 hello hello 工作物件，在下列程式碼 toodefine 其他方法可讓 Azure Cosmos DB 中所儲存的資料互動。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-166">Next, add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in Azure Cosmos DB.</span></span>
   
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
9. <span data-ttu-id="f3c8e-167">儲存並關閉 hello **taskDao.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-167">Save and close hello **taskDao.js** file.</span></span> 

### <a name="create-hello-controller"></a><span data-ttu-id="f3c8e-168">建立 hello 控制站</span><span class="sxs-lookup"><span data-stu-id="f3c8e-168">Create hello controller</span></span>
1. <span data-ttu-id="f3c8e-169">在 hello**路由**您專案的目錄建立新的檔案命名為**tasklist.js**。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-169">In hello **routes** directory of your project, create a new file named **tasklist.js**.</span></span> 
2. <span data-ttu-id="f3c8e-170">新增下列程式碼太 hello**tasklist.js**。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-170">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="f3c8e-171">這會載入 hello DocumentDBClient 和非同步模組，可供用**tasklist.js**。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-171">This loads hello DocumentDBClient and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="f3c8e-172">這也會定義 hello **TaskList**函式，會傳遞 hello 的執行個體**工作**我們先前定義的物件：</span><span class="sxs-lookup"><span data-stu-id="f3c8e-172">This also defined hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. <span data-ttu-id="f3c8e-173">繼續加入 toohello **tasklist.js**檔案加上使用過的 hello 方法**showTasks，addTask**，和**completeTasks**:</span><span class="sxs-lookup"><span data-stu-id="f3c8e-173">Continue adding toohello **tasklist.js** file by adding hello methods used too**showTasks, addTask**, and **completeTasks**:</span></span>
   
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
4. <span data-ttu-id="f3c8e-174">儲存並關閉 hello **tasklist.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-174">Save and close hello **tasklist.js** file.</span></span>

### <a name="add-configjs"></a><span data-ttu-id="f3c8e-175">新增 config.js</span><span class="sxs-lookup"><span data-stu-id="f3c8e-175">Add config.js</span></span>
1. <span data-ttu-id="f3c8e-176">在您的專案目錄中，建立名為 **config.js**的新檔案。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-176">In your project directory create a new file named **config.js**.</span></span>
2. <span data-ttu-id="f3c8e-177">Hello 太之後加入**config.js**。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-177">Add hello following too**config.js**.</span></span> <span data-ttu-id="f3c8e-178">這會定義組態設定和我們的應用程式所需的值。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-178">This defines configuration settings and values needed for our application.</span></span>
   
        var config = {}
   
        config.host = process.env.HOST || "[hello URI value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[hello PRIMARY KEY value from hello Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. <span data-ttu-id="f3c8e-179">在 hello **config.js**檔案，更新 hello 值的主應用程式和使用您的 Azure Cosmos DB 帳戶上 hello hello 金鑰刀鋒視窗中的 hello 值 AUTH_KEY [Microsoft Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-179">In hello **config.js** file, update hello values of HOST and AUTH_KEY using hello values found in hello Keys blade of your Azure Cosmos DB account on hello [Microsoft Azure portal](https://portal.azure.com).</span></span>
4. <span data-ttu-id="f3c8e-180">儲存並關閉 hello **config.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-180">Save and close hello **config.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="f3c8e-181">修改 app.js</span><span class="sxs-lookup"><span data-stu-id="f3c8e-181">Modify app.js</span></span>
1. <span data-ttu-id="f3c8e-182">在 hello 專案目錄中，開啟 hello **app.js**檔案。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-182">In hello project directory, open hello **app.js** file.</span></span> <span data-ttu-id="f3c8e-183">建立 hello Express web 應用程式時，稍早建立此檔案。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-183">This file was created earlier when hello Express web application was created.</span></span>
2. <span data-ttu-id="f3c8e-184">新增下列程式碼 toohello 頂端的 hello **app.js**</span><span class="sxs-lookup"><span data-stu-id="f3c8e-184">Add hello following code toohello top of **app.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. <span data-ttu-id="f3c8e-185">此程式碼定義 hello 設定檔 toobe 使用，然後進行 tooread 值超出此檔案置於很快，我們將使用一些變數。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-185">This code defines hello config file toobe used, and proceeds tooread values out of this file into some variables we will use soon.</span></span>
4. <span data-ttu-id="f3c8e-186">取代下列兩行中的 hello **app.js**檔案：</span><span class="sxs-lookup"><span data-stu-id="f3c8e-186">Replace hello following two lines in **app.js** file:</span></span>
   
        app.use('/', index);
        app.use('/users', users); 
   
      <span data-ttu-id="f3c8e-187">以下列程式碼片段的 hello:</span><span class="sxs-lookup"><span data-stu-id="f3c8e-187">with hello following snippet:</span></span>
   
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
5. <span data-ttu-id="f3c8e-188">這幾行定義的新執行個體我們**TaskDao**物件，並將新的連接 tooAzure Cosmos DB (使用 hello 值讀取 hello **config.js**)、 初始化 hello 工作物件，然後再繫結表單動作toomethods 上的我們**TaskList**控制站。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-188">These lines define a new instance of our **TaskDao** object, with a new connection tooAzure Cosmos DB (using hello values read from hello **config.js**), initialize hello task object and then bind form actions toomethods on our **TaskList** controller.</span></span> 
6. <span data-ttu-id="f3c8e-189">最後，儲存並關閉 hello **app.js**檔案中，我們即將結束。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-189">Finally, save and close hello **app.js** file, we're just about done.</span></span>

## <span data-ttu-id="f3c8e-190"><a name="_Toc395783181"></a>步驟 5：建置使用者介面</span><span class="sxs-lookup"><span data-stu-id="f3c8e-190"><a name="_Toc395783181"></a>Step 5: Build a user interface</span></span>
<span data-ttu-id="f3c8e-191">現在讓我們來開啟我們注意 toobuilding hello 的使用者介面，讓使用者可以實際互動我們的應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-191">Now let’s turn our attention toobuilding hello user interface so a user can actually interact with our application.</span></span> <span data-ttu-id="f3c8e-192">hello Express 應用程式，我們建立了使用**Jade**做為 hello 檢視引擎。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-192">hello Express application we created uses **Jade** as hello view engine.</span></span> <span data-ttu-id="f3c8e-193">如需 Jade 的詳細資訊，請參閱太[http://jade-lang.com/](http://jade-lang.com/)。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-193">For more information on Jade please refer too[http://jade-lang.com/](http://jade-lang.com/).</span></span>

1. <span data-ttu-id="f3c8e-194">hello **layout.jade**檔案在 hello**檢視**目錄作為全域範本其他**.jade**檔案。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-194">hello **layout.jade** file in hello **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="f3c8e-195">在此步驟中您會修改它 toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap)，這是一項工具組，可讓您輕鬆 toodesign nice 尋找網站。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-195">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking website.</span></span> 
2. <span data-ttu-id="f3c8e-196">開啟 hello **layout.jade**檔案位於 hello**檢視**hello 下列資料夾和取代 hello 內容：</span><span class="sxs-lookup"><span data-stu-id="f3c8e-196">Open hello **layout.jade** file found in hello **views** folder and replace hello contents with hello following:</span></span>

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

    <span data-ttu-id="f3c8e-197">這實際上會告知 hello **Jade**引擎 toorender 一些 HTML 應用程式，並建立**區塊**呼叫**內容**我們可以在其中提供我們內容 hello 版面配置頁面。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-197">This effectively tells hello **Jade** engine toorender some HTML for our application and creates a **block** called **content** where we can supply hello layout for our content pages.</span></span>

    <span data-ttu-id="f3c8e-198">儲存並關閉此 **layout.jade** 檔案。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-198">Save and close this **layout.jade** file.</span></span>

3. <span data-ttu-id="f3c8e-199">現在開啟 hello **index.jade**檔案，供我們的應用程式，並取代 hello 下列中的 hello hello 檔案內容的 hello 檢視：</span><span class="sxs-lookup"><span data-stu-id="f3c8e-199">Now open hello **index.jade** file, hello view that will be used by our application, and replace hello content of hello file with hello following:</span></span>
   
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
   

<span data-ttu-id="f3c8e-200">這會擴充版面配置，並提供 hello 內容**內容**預留位置我們了解在 hello **layout.jade**稍早檔案。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-200">This extends layout, and provides content for hello **content** placeholder we saw in hello **layout.jade** file earlier.</span></span>
   
<span data-ttu-id="f3c8e-201">在此配置中，我們建立了兩個 HTML 表單。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-201">In this layout we created two HTML forms.</span></span>

<span data-ttu-id="f3c8e-202">hello 第一種形式包含資料表的資料和按鈕，讓我們 tooupdate 項目藉由公佈太**/completetask**我們控制站的方法。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-202">hello first form contains a table for our data and a button that allows us tooupdate items by posting too**/completetask** method of our controller.</span></span>
    
<span data-ttu-id="f3c8e-203">hello 第二個表單包含兩個輸入的欄位和一個按鈕，讓我們 toocreate 新項目藉由公佈太**/addtask**我們控制站的方法。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-203">hello second form contains two input fields and a button that allows us toocreate a new item by posting too**/addtask** method of our controller.</span></span>

<span data-ttu-id="f3c8e-204">這應該是所有我們需要以我們的應用程式 toowork。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-204">This should be all that we need for our application toowork.</span></span>

## <span data-ttu-id="f3c8e-205"><a name="_Toc395783181"></a>步驟 6：在本機執行您的應用程式</span><span class="sxs-lookup"><span data-stu-id="f3c8e-205"><a name="_Toc395783181"></a>Step 6: Run your application locally</span></span>
1. <span data-ttu-id="f3c8e-206">tootest hello 應用程式，您的本機電腦上執行`npm start`hello toostart 終端機應用程式，然後重新整理您[http://localhost:3000](http://localhost:3000)瀏覽器頁面。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-206">tootest hello application on your local machine, run `npm start` in hello terminal toostart your application, then refresh your [http://localhost:3000](http://localhost:3000) browser page.</span></span> <span data-ttu-id="f3c8e-207">hello 頁面現在看起來應該像下面的 hello 影像：</span><span class="sxs-lookup"><span data-stu-id="f3c8e-207">hello page should now look like hello image below:</span></span>
   
    ![Hello MyTodo 清單應用程式，在瀏覽器視窗的螢幕擷取畫面](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > <span data-ttu-id="f3c8e-209">如果您收到 hello layout.jade 檔案或 hello index.jade 檔案中的 hello 縮排的相關錯誤，請確認這兩個檔案中的 hello 前兩行靠左對齊，不含空格。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-209">If you receive an error about hello indent in hello layout.jade file or hello index.jade file, ensure that hello first two lines in both files is left justified, with no spaces.</span></span> <span data-ttu-id="f3c8e-210">如果有空格 hello 前兩個行之前，將它們移除，請儲存兩個檔案，然後重新整理瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-210">If there are spaces before hello first two lines, remove them, save both files, then refresh your browser window.</span></span> 

2. <span data-ttu-id="f3c8e-211">使用 hello 項目、 項目名稱和類別目錄欄位 tooenter 新工作，然後按一下**加入項目**。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-211">Use hello Item, Item Name and Category fields tooenter a new task and then click **Add Item**.</span></span> <span data-ttu-id="f3c8e-212">便會使用這些屬性在 Azure Cosmos DB 中建立文件。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-212">This creates a document in Azure Cosmos DB with those properties.</span></span> 
3. <span data-ttu-id="f3c8e-213">hello 頁面應該更新新建立 hello ToDo 清單中的項目 toodisplay hello。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-213">hello page should update toodisplay hello newly created item in hello ToDo list.</span></span>
   
    ![使用新的項目 hello ToDo 清單中的 hello 應用程式的螢幕擷取畫面](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. <span data-ttu-id="f3c8e-215">toocomplete 項工作中，只會檢查 hello 完整資料行中的 hello 核取方塊，然後按一下**更新工作**。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-215">toocomplete a task, simply check hello checkbox in hello Complete column, and then click **Update tasks**.</span></span> <span data-ttu-id="f3c8e-216">這會更新您已建立的 hello 文件。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-216">This updates hello document you already created.</span></span>

5. <span data-ttu-id="f3c8e-217">toostop hello 應用程式中，按 CTRL + C hello terminal 視窗中，然後按一下**Y** tooterminate hello 批次作業。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-217">toostop hello application, press CTRL+C in hello terminal window and then click **Y** tooterminate hello batch job.</span></span>

## <span data-ttu-id="f3c8e-218"><a name="_Toc395783182"></a>步驟 7： 部署您的應用程式開發專案 tooAzure 網站</span><span class="sxs-lookup"><span data-stu-id="f3c8e-218"><a name="_Toc395783182"></a>Step 7: Deploy your application development project tooAzure Websites</span></span>
1. <span data-ttu-id="f3c8e-219">如果您還沒有這麼做，請為您的 Azure 網站提供一個 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-219">If you haven't already, enable a git repository for your Azure Website.</span></span> <span data-ttu-id="f3c8e-220">您可以找到指示如何 toodo 這在 hello[應用程式服務的本機 Git 部署 tooAzure](../app-service-web/app-service-deploy-local-git.md)主題。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-220">You can find instructions on how toodo this in hello [Local Git Deployment tooAzure App Service](../app-service-web/app-service-deploy-local-git.md) topic.</span></span>
2. <span data-ttu-id="f3c8e-221">新增您的 Azure 網站做為 Git 遠端。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-221">Add your Azure Website as a git remote.</span></span>
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. <span data-ttu-id="f3c8e-222">藉由推送 toohello 遠端部署。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-222">Deploy by pushing toohello remote.</span></span>
   
        git push azure master
4. <span data-ttu-id="f3c8e-223">幾秒後，Git 便會發佈 Web 應用程式並啟動瀏覽器，您可以在瀏覽器中看到您方便好用的應用程式已在 Azure 中執行！</span><span class="sxs-lookup"><span data-stu-id="f3c8e-223">In a few seconds, git will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>

    <span data-ttu-id="f3c8e-224">恭喜！</span><span class="sxs-lookup"><span data-stu-id="f3c8e-224">Congratulations!</span></span> <span data-ttu-id="f3c8e-225">您剛才已建置第一個 Node.js Express Web 應用程式使用 Azure Cosmos DB，並發佈它 tooAzure 網站。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-225">You have just built your first Node.js Express Web Application using Azure Cosmos DB and published it tooAzure Websites.</span></span>

    <span data-ttu-id="f3c8e-226">如果您想 toodownload 或 toohello 完整參考的應用程式，請參閱本教學課程中，它可以從下載[GitHub][GitHub]。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-226">If you want toodownload or refer toohello complete reference application for this tutorial, it can be downloaded from [GitHub][GitHub].</span></span>

## <span data-ttu-id="f3c8e-227"><a name="_Toc395637775"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="f3c8e-227"><a name="_Toc395637775"></a>Next steps</span></span>

* <span data-ttu-id="f3c8e-228">想 tooperform 規模和效能測試以 Azure Cosmos DB 嗎？</span><span class="sxs-lookup"><span data-stu-id="f3c8e-228">Want tooperform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="f3c8e-229">請參閱 [Azure Cosmos DB 的效能和規模測試](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="f3c8e-229">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="f3c8e-230">了解如何太[監視 Azure Cosmos DB 帳戶](monitor-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-230">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="f3c8e-231">執行查詢，根據我們的範例資料集，在 hello[查詢遊樂場](https://www.documentdb.com/sql/demo)。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-231">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="f3c8e-232">瀏覽 hello [Azure Cosmos DB 文件集](https://docs.microsoft.com/azure/documentdb/)。</span><span class="sxs-lookup"><span data-stu-id="f3c8e-232">Explore hello [Azure Cosmos DB documentation](https://docs.microsoft.com/azure/documentdb/).</span></span>

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app

