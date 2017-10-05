---
title: "建置適用於 Azure Cosmos DB 的 Node.js Web 應用程式 | Microsoft Docs"
description: "這個 Node.js 教學課程會探索如何使用 Microsoft Azure Cosmos DB，從 Azure 網站上裝載的 Node.js Express Web 應用程式來儲存和存取資料。"
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
ms.openlocfilehash: 1a98509a98bcd2a5de593eb006f905766fe72966
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <span data-ttu-id="4d8ce-104"><a name="_Toc395783175"></a>使用 Azure Cosmos DB 來建置 Node.js Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4d8ce-104"><a name="_Toc395783175"></a>Build a Node.js web application using Azure Cosmos DB</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4d8ce-105">.NET</span><span class="sxs-lookup"><span data-stu-id="4d8ce-105">.NET</span></span>](documentdb-dotnet-application.md)
> * [<span data-ttu-id="4d8ce-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="4d8ce-106">Node.js</span></span>](documentdb-nodejs-application.md)
> * [<span data-ttu-id="4d8ce-107">Java</span><span class="sxs-lookup"><span data-stu-id="4d8ce-107">Java</span></span>](documentdb-java-application.md)
> * [<span data-ttu-id="4d8ce-108">Python</span><span class="sxs-lookup"><span data-stu-id="4d8ce-108">Python</span></span>](documentdb-python-application.md)
> 
> 

<span data-ttu-id="4d8ce-109">本 Node.js 教學課程說明如何使用 Azure Cosmos DB 和 DocumentDB API，來儲存和存取 Azure 網站上所託管的 Node.js Express 應用程式資料。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-109">This Node.js tutorial shows you how to use Azure Cosmos DB and the DocumentDB API to store and access data from a Node.js Express application hosted on Azure Websites.</span></span> <span data-ttu-id="4d8ce-110">您會建置一個可供建立、擷取及完成工作的簡單網頁型工作管理應用程式 (待辦事項應用程式)。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-110">You build a simple web-based task-management application, a ToDo app, that allows creating, retrieving, and completing tasks.</span></span> <span data-ttu-id="4d8ce-111">在 Azure Cosmos DB 中，這些工作會儲存為 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-111">The tasks are stored as JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="4d8ce-112">本教學課程會逐步引導您建立和部署應用程式，並說明每個程式碼片段中的狀況。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-112">This tutorial walks you through the creation and deployment of the app and explains what's happening in each snippet.</span></span>

![本 Node.js 教學課程所建立的「我的待辦事項清單」應用程式螢幕擷取畫面](./media/documentdb-nodejs-application/cosmos-db-node-js-mytodo.png)

<span data-ttu-id="4d8ce-114">是否沒有時間完成本教學課程，只是想要取得完整的解決方案？</span><span class="sxs-lookup"><span data-stu-id="4d8ce-114">Don't have time to complete the tutorial and just want to get the complete solution?</span></span> <span data-ttu-id="4d8ce-115">沒有問題，您可以從 [GitHub][GitHub] 取得完整的範例解決方案。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-115">Not a problem, you can get the complete sample solution from [GitHub][GitHub].</span></span> <span data-ttu-id="4d8ce-116">如需有關如何執行應用程式的指示，只需閱讀 [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) 檔案即可。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-116">Just read the [Readme](https://github.com/Azure-Samples/documentdb-node-todo-app/blob/master/README.md) file for instructions on how to run the app.</span></span>

## <span data-ttu-id="4d8ce-117"><a name="_Toc395783176"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="4d8ce-117"><a name="_Toc395783176"></a>Prerequisites</span></span>
> [!TIP]
> <span data-ttu-id="4d8ce-118">本 Node.js 教學課程假設您先前已有些許使用 Node.js 和 Azure 網站的經驗。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-118">This Node.js tutorial assumes that you have some prior experience using Node.js and Azure Websites.</span></span>
> 
> 

<span data-ttu-id="4d8ce-119">在依照本文中的指示進行之前，您應先確定備妥下列項目：</span><span class="sxs-lookup"><span data-stu-id="4d8ce-119">Before following the instructions in this article, you should ensure that you have the following:</span></span>

* <span data-ttu-id="4d8ce-120">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-120">An active Azure account.</span></span> <span data-ttu-id="4d8ce-121">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-121">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="4d8ce-122">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-122">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

   <span data-ttu-id="4d8ce-123">或</span><span class="sxs-lookup"><span data-stu-id="4d8ce-123">OR</span></span>

   <span data-ttu-id="4d8ce-124">本機安裝的 [Azure Cosmos DB 模擬器](local-emulator.md) (僅適用於 Windows)。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-124">A local installation of the [Azure Cosmos DB Emulator](local-emulator.md) (Windows only).</span></span>
* <span data-ttu-id="4d8ce-125">[Node.js][Node.js] v0.10.29 版或更高版本。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-125">[Node.js][Node.js] version v0.10.29 or higher.</span></span>
* <span data-ttu-id="4d8ce-126">[Express 產生器](http://www.expressjs.com/starter/generator.html) (您可以透過 `npm install express-generator -g` 進行安裝)</span><span class="sxs-lookup"><span data-stu-id="4d8ce-126">[Express generator](http://www.expressjs.com/starter/generator.html) (you can install this via `npm install express-generator -g`)</span></span>
* <span data-ttu-id="4d8ce-127">[Git][Git]。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-127">[Git][Git].</span></span>

## <span data-ttu-id="4d8ce-128"><a name="_Toc395637761"></a>步驟 1：建立 Azure Cosmos DB 資料庫帳戶</span><span class="sxs-lookup"><span data-stu-id="4d8ce-128"><a name="_Toc395637761"></a>Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="4d8ce-129">我們將從建立 Azure Cosmos DB 帳戶開始著手。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-129">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="4d8ce-130">如果您已經擁有帳戶，或如果您正在使用 Azure Cosmos DB 模擬器來進行本教學課程，可以跳到[步驟 2：建立新的 Node.js 應用程式](#_Toc395783178)。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-130">If you already have an account or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Step 2: Create a new Node.js application](#_Toc395783178).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [cosmos-db-keys](../../includes/cosmos-db-keys.md)]

## <span data-ttu-id="4d8ce-131"><a name="_Toc395783178"></a>步驟 2 - 建立新的 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="4d8ce-131"><a name="_Toc395783178"></a>Step 2: Create a new Node.js application</span></span>
<span data-ttu-id="4d8ce-132">現在，我們來了解如何使用 [Express](http://expressjs.com/) 架構來建立基本的 Hello World Node.js 專案。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-132">Now let's learn to create a basic Hello World Node.js project using the [Express](http://expressjs.com/) framework.</span></span>

1. <span data-ttu-id="4d8ce-133">開啟您喜好的終端機，例如 Node.js 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-133">Open your favorite terminal, such as the Node.js command prompt.</span></span>
2. <span data-ttu-id="4d8ce-134">瀏覽至您想要在其中儲存新應用程式的目錄。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-134">Navigate to the directory in which you'd like to store the new application.</span></span>
3. <span data-ttu-id="4d8ce-135">使用 Express 產生器來產生名為 **todo**的新應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-135">Use the express generator to generate a new application called **todo**.</span></span>
   
        express todo
4. <span data-ttu-id="4d8ce-136">開啟您的新 **todo** 目錄並安裝相依性。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-136">Open your new **todo** directory and install dependencies.</span></span>
   
        cd todo
        npm install
5. <span data-ttu-id="4d8ce-137">執行新的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-137">Run your new application.</span></span>
   
        npm start
6. <span data-ttu-id="4d8ce-138">您可以檢視新的應用程式，請導覽瀏覽器至 [http://localhost:3000/](http://localhost:3000)。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-138">You can view your new application by navigating your browser to [http://localhost:3000](http://localhost:3000).</span></span>
   
    ![了解 Node.js - Hello World 應用程式在瀏覽器視窗中的螢幕擷取畫面](./media/documentdb-nodejs-application/cosmos-db-node-js-express.png)

    <span data-ttu-id="4d8ce-140">然後，若要停止應用程式，請在終端機視窗中按 CTRL+C，然後按一下 **y** 以終止批次作業。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-140">Then, to stop the application, press CTRL+C in the terminal window and then click **y** to terminate the batch job.</span></span>

## <span data-ttu-id="4d8ce-141"><a name="_Toc395783179"></a>步驟 3：安裝其他模組</span><span class="sxs-lookup"><span data-stu-id="4d8ce-141"><a name="_Toc395783179"></a>Step 3: Install additional modules</span></span>
<span data-ttu-id="4d8ce-142">**package.json** 檔案是建立在專案根目錄中的其中一個檔案。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-142">The **package.json** file is one of the files created in the root of the project.</span></span> <span data-ttu-id="4d8ce-143">這個檔案包含 Node.js 應用程式所需的其他模組清單。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-143">This file contains a list of additional modules that are required for your Node.js application.</span></span> <span data-ttu-id="4d8ce-144">之後，當您將此應用程式部署至 Azure 網站時，此檔案可用來決定 Azure 上需要安裝哪些模組才能支援您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-144">Later, when you deploy this application to Azure Websites, this file is used to determine which modules need to be installed on Azure to support your application.</span></span> <span data-ttu-id="4d8ce-145">在本教學課程中，我們還需要再安裝兩個封裝。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-145">We still need to install two more packages for this tutorial.</span></span>

1. <span data-ttu-id="4d8ce-146">返回終端機，透過 npm 安裝 **async** 模組。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-146">Back in the terminal, install the **async** module via npm.</span></span>
   
        npm install async --save
2. <span data-ttu-id="4d8ce-147">透過 npm 安裝 **documentdb** 模組。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-147">Install the **documentdb** module via npm.</span></span> <span data-ttu-id="4d8ce-148">這是 Azure Cosmos DB 發揮所有強大功能的模組。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-148">This is the module where all the Azure Cosmos DB magic happens.</span></span>
   
        npm install documentdb --save
3. <span data-ttu-id="4d8ce-149">快速檢查應用程式的 **package.json** 檔案應該會顯示其他模組。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-149">A quick check of the **package.json** file of the application should show the additional modules.</span></span> <span data-ttu-id="4d8ce-150">這個檔案會告訴 Azure 在執行您的應用程式時要下載及安裝的封裝。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-150">This file will tell Azure which packages to download and install when running your application.</span></span> <span data-ttu-id="4d8ce-151">它看起來應該類似下面的範例。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-151">It should resemble the example below.</span></span>
   
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
   
    <span data-ttu-id="4d8ce-152">這會讓 Node (之後則是 Azure) 知道您的應用程式需要仰賴這些額外模組。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-152">This tells Node (and Azure later) that your application depends on these additional modules.</span></span>

## <span data-ttu-id="4d8ce-153"><a name="_Toc395783180"></a>步驟 4：在節點應用程式中使用 Azure Cosmos DB 服務</span><span class="sxs-lookup"><span data-stu-id="4d8ce-153"><a name="_Toc395783180"></a>Step 4: Using the Azure Cosmos DB service in a node application</span></span>
<span data-ttu-id="4d8ce-154">前面的內容在講述所有初始設定和組態，現在讓我們來了解本教學課程的真正目的，也就是使用 Azure Cosmos DB 撰寫一些程式碼。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-154">That takes care of all the initial setup and configuration, now let’s get down to why we’re here, and that’s to write some code using Azure Cosmos DB.</span></span>

### <a name="create-the-model"></a><span data-ttu-id="4d8ce-155">建立模型</span><span class="sxs-lookup"><span data-stu-id="4d8ce-155">Create the model</span></span>
1. <span data-ttu-id="4d8ce-156">在專案目錄中，請在與 package.json 檔案相同的目錄中建立名為 **models** 的新目錄。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-156">In the project directory, create a new directory named **models** in the same directory as the package.json file.</span></span>
2. <span data-ttu-id="4d8ce-157">在 **models** 目錄中，建立名為 **taskDao.js** 的新檔案。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-157">In the **models** directory, create a new file named **taskDao.js**.</span></span> <span data-ttu-id="4d8ce-158">此檔案將包含應用程式所建立工作的模型。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-158">This file will contain the model for the tasks created by our application.</span></span>
3. <span data-ttu-id="4d8ce-159">在同一個 **models** 目錄中，建立另一個名為 **docdbUtils.js** 的新檔案。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-159">In the same **models** directory, create another new file named **docdbUtils.js**.</span></span> <span data-ttu-id="4d8ce-160">這個檔案會包含一些實用、可重複使用，適用於整個應用程式的程式碼。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-160">This file will contain some useful, reusable, code that we will use throughout our application.</span></span> 
4. <span data-ttu-id="4d8ce-161">將下列程式碼複製到 **docdbUtils.js**</span><span class="sxs-lookup"><span data-stu-id="4d8ce-161">Copy the following code in to **docdbUtils.js**</span></span>
   
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
   
5. <span data-ttu-id="4d8ce-162">儲存並關閉 **docdbUtils.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-162">Save and close the **docdbUtils.js** file.</span></span>
6. <span data-ttu-id="4d8ce-163">在 **taskDao.js** 檔案的開頭加入下列程式碼，以參考我們之前建立的 **DocumentDBClient** 和 **docdbUtils.js**：</span><span class="sxs-lookup"><span data-stu-id="4d8ce-163">At the beginning of the **taskDao.js** file, add the following code to reference the **DocumentDBClient** and the **docdbUtils.js** we created above:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var docdbUtils = require('./docdbUtils');
7. <span data-ttu-id="4d8ce-164">接下來，要加入程式碼以定義和匯出 Task 物件。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-164">Next, you will add code to define and export the Task object.</span></span> <span data-ttu-id="4d8ce-165">這會負責初始化我們的 Task 物件，並設定我們即將使用的資料庫和文件集合。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-165">This is responsible for initializing our Task object and setting up the Database and Document Collection we will use.</span></span>
   
        function TaskDao(documentDBClient, databaseId, collectionId) {
          this.client = documentDBClient;
          this.databaseId = databaseId;
          this.collectionId = collectionId;
   
          this.database = null;
          this.collection = null;
        }
   
        module.exports = TaskDao;
8. <span data-ttu-id="4d8ce-166">接下來，新增下列程式碼以定義 Task 物件上的其他方法，可用來與 Azure Cosmos DB 中存放的資料進行互動。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-166">Next, add the following code to define additional methods on the Task object, which allow interactions with data stored in Azure Cosmos DB.</span></span>
   
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
9. <span data-ttu-id="4d8ce-167">儲存並關閉 **taskDao.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-167">Save and close the **taskDao.js** file.</span></span> 

### <a name="create-the-controller"></a><span data-ttu-id="4d8ce-168">建立控制器</span><span class="sxs-lookup"><span data-stu-id="4d8ce-168">Create the controller</span></span>
1. <span data-ttu-id="4d8ce-169">在專案的 **routes** 目錄中，建立名為 **tasklist.js** 的新檔案。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-169">In the **routes** directory of your project, create a new file named **tasklist.js**.</span></span> 
2. <span data-ttu-id="4d8ce-170">在 **tasklist.js**中加入以下程式碼。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-170">Add the following code to **tasklist.js**.</span></span> <span data-ttu-id="4d8ce-171">這會載入供 **tasklist.js**使用的 DocumentDBClient 和 async 模組。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-171">This loads the DocumentDBClient and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="4d8ce-172">這也會定義 **TaskList** 函式，系統會傳遞我們稍早定義的 **Task** 物件執行個體給它：</span><span class="sxs-lookup"><span data-stu-id="4d8ce-172">This also defined the **TaskList** function, which is passed an instance of the **Task** object we defined earlier:</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var async = require('async');
   
        function TaskList(taskDao) {
          this.taskDao = taskDao;
        }
   
        module.exports = TaskList;
3. <span data-ttu-id="4d8ce-173">繼續在 **tasklist.js** 檔案中新增用來 **showTasks (顯示工作)、addTask (新增工作)** 和 **completeTasks (完成工作)** 的方法：</span><span class="sxs-lookup"><span data-stu-id="4d8ce-173">Continue adding to the **tasklist.js** file by adding the methods used to **showTasks, addTask**, and **completeTasks**:</span></span>
   
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
4. <span data-ttu-id="4d8ce-174">儲存並關閉 **tasklist.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-174">Save and close the **tasklist.js** file.</span></span>

### <a name="add-configjs"></a><span data-ttu-id="4d8ce-175">新增 config.js</span><span class="sxs-lookup"><span data-stu-id="4d8ce-175">Add config.js</span></span>
1. <span data-ttu-id="4d8ce-176">在您的專案目錄中，建立名為 **config.js**的新檔案。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-176">In your project directory create a new file named **config.js**.</span></span>
2. <span data-ttu-id="4d8ce-177">將下列程式碼新增至 **config.js**。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-177">Add the following to **config.js**.</span></span> <span data-ttu-id="4d8ce-178">這會定義組態設定和我們的應用程式所需的值。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-178">This defines configuration settings and values needed for our application.</span></span>
   
        var config = {}
   
        config.host = process.env.HOST || "[the URI value from the Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.authKey = process.env.AUTH_KEY || "[the PRIMARY KEY value from the Azure Cosmos DB Keys blade on http://portal.azure.com]";
        config.databaseId = "ToDoList";
        config.collectionId = "Items";
   
        module.exports = config;
3. <span data-ttu-id="4d8ce-179">在 **config.js** 檔案中，使用 [Microsoft Azure 入口網站](https://portal.azure.com)上 Azure Cosmos DB 帳戶的 [金鑰] 刀鋒視窗中找到的值，更新 HOST 和 AUTH_KEY 的值。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-179">In the **config.js** file, update the values of HOST and AUTH_KEY using the values found in the Keys blade of your Azure Cosmos DB account on the [Microsoft Azure portal](https://portal.azure.com).</span></span>
4. <span data-ttu-id="4d8ce-180">儲存並關閉 **config.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-180">Save and close the **config.js** file.</span></span>

### <a name="modify-appjs"></a><span data-ttu-id="4d8ce-181">修改 app.js</span><span class="sxs-lookup"><span data-stu-id="4d8ce-181">Modify app.js</span></span>
1. <span data-ttu-id="4d8ce-182">在專案目錄中，開啟 **app.js** 檔案。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-182">In the project directory, open the **app.js** file.</span></span> <span data-ttu-id="4d8ce-183">這是稍早建立 Express Web 應用程式時所建立的檔案。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-183">This file was created earlier when the Express web application was created.</span></span>
2. <span data-ttu-id="4d8ce-184">將下列程式碼新增至 **app.js**</span><span class="sxs-lookup"><span data-stu-id="4d8ce-184">Add the following code to the top of **app.js**</span></span>
   
        var DocumentDBClient = require('documentdb').DocumentClient;
        var config = require('./config');
        var TaskList = require('./routes/tasklist');
        var TaskDao = require('./models/taskDao');
3. <span data-ttu-id="4d8ce-185">此程式碼會定義要使用的組態檔，並繼續讀出此檔案中的值到我們即將使用的變數。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-185">This code defines the config file to be used, and proceeds to read values out of this file into some variables we will use soon.</span></span>
4. <span data-ttu-id="4d8ce-186">將 **app.js** 檔案中的下列兩行取代為：</span><span class="sxs-lookup"><span data-stu-id="4d8ce-186">Replace the following two lines in **app.js** file:</span></span>
   
        app.use('/', index);
        app.use('/users', users); 
   
      <span data-ttu-id="4d8ce-187">下列程式碼片段：</span><span class="sxs-lookup"><span data-stu-id="4d8ce-187">with the following snippet:</span></span>
   
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
5. <span data-ttu-id="4d8ce-188">這幾行會定義 **TaskDao** 物件的新執行個體，內含與 Azure Cosmos DB 的新連線 (使用從 **config.js** 中讀取的值)，將 Task 物件初始化，然後將表單動作繫結至 **TaskList** 控制站上的方法。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-188">These lines define a new instance of our **TaskDao** object, with a new connection to Azure Cosmos DB (using the values read from the **config.js**), initialize the task object and then bind form actions to methods on our **TaskList** controller.</span></span> 
6. <span data-ttu-id="4d8ce-189">最後，儲存並關閉 **app.js** 檔案，我們就差不多快完成了。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-189">Finally, save and close the **app.js** file, we're just about done.</span></span>

## <span data-ttu-id="4d8ce-190"><a name="_Toc395783181"></a>步驟 5：建置使用者介面</span><span class="sxs-lookup"><span data-stu-id="4d8ce-190"><a name="_Toc395783181"></a>Step 5: Build a user interface</span></span>
<span data-ttu-id="4d8ce-191">現在，讓我們將注意力轉到建置使用者介面，以便使用者可以實際與我們的應用程式互動。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-191">Now let’s turn our attention to building the user interface so a user can actually interact with our application.</span></span> <span data-ttu-id="4d8ce-192">我們建立的 Express 應用程式使用 **Jade** 做為檢視引擎。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-192">The Express application we created uses **Jade** as the view engine.</span></span> <span data-ttu-id="4d8ce-193">如需 Jade 的詳細資訊，請參閱 [http://jade-lang.com/](http://jade-lang.com/)。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-193">For more information on Jade please refer to [http://jade-lang.com/](http://jade-lang.com/).</span></span>

1. <span data-ttu-id="4d8ce-194">**views** 目錄中的 **layout.jade** 檔是用來作為其他 **.jade** 檔案的全域範本。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-194">The **layout.jade** file in the **views** directory is used as a global template for other **.jade** files.</span></span> <span data-ttu-id="4d8ce-195">在此步驟中，您將修改它以使用 [Twitter Bootstrap](https://github.com/twbs/bootstrap)，這個工具組能夠方便設計美觀的網站。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-195">In this step you will modify it to use [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy to design a nice looking website.</span></span> 
2. <span data-ttu-id="4d8ce-196">開啟在 **views** 資料夾中找到的 **layout.jade** 檔案，並將其中的內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="4d8ce-196">Open the **layout.jade** file found in the **views** folder and replace the contents with the following:</span></span>

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

    <span data-ttu-id="4d8ce-197">這段程式碼實際上會指示 **Jade** 引擎轉譯出我們應用程式的部分 HTML，並建立稱為 **content** 的**區塊**，讓我們能在其中提供內容頁面的配置。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-197">This effectively tells the **Jade** engine to render some HTML for our application and creates a **block** called **content** where we can supply the layout for our content pages.</span></span>

    <span data-ttu-id="4d8ce-198">儲存並關閉此 **layout.jade** 檔案。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-198">Save and close this **layout.jade** file.</span></span>

3. <span data-ttu-id="4d8ce-199">現在，開啟 **index.jade** 檔案 (應用程式即將使用的檢視)，並將檔案中的內容取代為下列內容；</span><span class="sxs-lookup"><span data-stu-id="4d8ce-199">Now open the **index.jade** file, the view that will be used by our application, and replace the content of the file with the following:</span></span>
   
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
   

<span data-ttu-id="4d8ce-200">這個程式碼會擴充配置，並為我們在前面的 **layout.jade** 檔案中看到的 **content** 預留位置提供內容。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-200">This extends layout, and provides content for the **content** placeholder we saw in the **layout.jade** file earlier.</span></span>
   
<span data-ttu-id="4d8ce-201">在此配置中，我們建立了兩個 HTML 表單。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-201">In this layout we created two HTML forms.</span></span>

<span data-ttu-id="4d8ce-202">第一個表單包含資料的表格，以及可讓我們透過張貼到控制器的 **/completetask** 方法來更新項目的按鈕。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-202">The first form contains a table for our data and a button that allows us to update items by posting to **/completetask** method of our controller.</span></span>
    
<span data-ttu-id="4d8ce-203">第二個表單包含兩個輸入欄位，以及可讓我們透過張貼到控制器的 **/addtask** 方法來建立項目的按鈕。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-203">The second form contains two input fields and a button that allows us to create a new item by posting to **/addtask** method of our controller.</span></span>

<span data-ttu-id="4d8ce-204">這應該就是要讓應用程式開始運作所需的所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-204">This should be all that we need for our application to work.</span></span>

## <span data-ttu-id="4d8ce-205"><a name="_Toc395783181"></a>步驟 6：在本機執行您的應用程式</span><span class="sxs-lookup"><span data-stu-id="4d8ce-205"><a name="_Toc395783181"></a>Step 6: Run your application locally</span></span>
1. <span data-ttu-id="4d8ce-206">若要在本機電腦上測試應用程式，請在終端機中執行 `npm start` 以啟動應用程式，然後重新整理 [http://localhost:3000](http://localhost:3000) 瀏覽器頁面。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-206">To test the application on your local machine, run `npm start` in the terminal to start your application, then refresh your [http://localhost:3000](http://localhost:3000) browser page.</span></span> <span data-ttu-id="4d8ce-207">此頁面現在看起來應該類似以下影像：</span><span class="sxs-lookup"><span data-stu-id="4d8ce-207">The page should now look like the image below:</span></span>
   
    ![[我的待辦事項清單] 應用程式在瀏覽器視窗中的螢幕擷取畫面](./media/documentdb-nodejs-application/cosmos-db-node-js-localhost.png)

    > [!TIP]
    > <span data-ttu-id="4d8ce-209">如果您收到有關 layout.jade 檔案或 index.jade 檔案縮排的錯誤，請確定這兩個檔案的前兩行靠左對齊 (沒有空格)。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-209">If you receive an error about the indent in the layout.jade file or the index.jade file, ensure that the first two lines in both files is left justified, with no spaces.</span></span> <span data-ttu-id="4d8ce-210">如果前兩行之前有空格，請將空格移除，儲存這兩個檔案，然後重新整理瀏覽器視窗。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-210">If there are spaces before the first two lines, remove them, save both files, then refresh your browser window.</span></span> 

2. <span data-ttu-id="4d8ce-211">使用 [項目]、[項目名稱] 和 [類別] 欄位來輸入新工作，然後按一下 [新增項目]。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-211">Use the Item, Item Name and Category fields to enter a new task and then click **Add Item**.</span></span> <span data-ttu-id="4d8ce-212">便會使用這些屬性在 Azure Cosmos DB 中建立文件。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-212">This creates a document in Azure Cosmos DB with those properties.</span></span> 
3. <span data-ttu-id="4d8ce-213">系統應該會更新此頁面，以在 [待辦事項] 清單中顯示新建立的項目。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-213">The page should update to display the newly created item in the ToDo list.</span></span>
   
    ![[待辦事項] 清單中包含一個新項目的應用程式螢幕擷取畫面](./media/documentdb-nodejs-application/cosmos-db-node-js-added-task.png)
4. <span data-ttu-id="4d8ce-215">若要完成工作，您只需勾選 [已完成] 資料行中的核取方塊，然後按一下 [更新工作] 。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-215">To complete a task, simply check the checkbox in the Complete column, and then click **Update tasks**.</span></span> <span data-ttu-id="4d8ce-216">這會更新您已建立的文件。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-216">This updates the document you already created.</span></span>

5. <span data-ttu-id="4d8ce-217">若要停止應用程式，請在終端機視窗中按 CTRL+C，然後按一下 **Y** 以終止批次作業。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-217">To stop the application, press CTRL+C in the terminal window and then click **Y** to terminate the batch job.</span></span>

## <span data-ttu-id="4d8ce-218"><a name="_Toc395783182"></a>步驟 7：將應用程式開發專案部署至 Azure 網站</span><span class="sxs-lookup"><span data-stu-id="4d8ce-218"><a name="_Toc395783182"></a>Step 7: Deploy your application development project to Azure Websites</span></span>
1. <span data-ttu-id="4d8ce-219">如果您還沒有這麼做，請為您的 Azure 網站提供一個 Git 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-219">If you haven't already, enable a git repository for your Azure Website.</span></span> <span data-ttu-id="4d8ce-220">您可以在 [Azure App Service 的本機 Git 部署](../app-service-web/app-service-deploy-local-git.md) 主題中找到有關如何執行這項操作的指示。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-220">You can find instructions on how to do this in the [Local Git Deployment to Azure App Service](../app-service-web/app-service-deploy-local-git.md) topic.</span></span>
2. <span data-ttu-id="4d8ce-221">新增您的 Azure 網站做為 Git 遠端。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-221">Add your Azure Website as a git remote.</span></span>
   
        git remote add azure https://username@your-azure-website.scm.azurewebsites.net:443/your-azure-website.git
3. <span data-ttu-id="4d8ce-222">透過推送到遠端進行部署。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-222">Deploy by pushing to the remote.</span></span>
   
        git push azure master
4. <span data-ttu-id="4d8ce-223">幾秒後，Git 便會發佈 Web 應用程式並啟動瀏覽器，您可以在瀏覽器中看到您方便好用的應用程式已在 Azure 中執行！</span><span class="sxs-lookup"><span data-stu-id="4d8ce-223">In a few seconds, git will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>

    <span data-ttu-id="4d8ce-224">恭喜！</span><span class="sxs-lookup"><span data-stu-id="4d8ce-224">Congratulations!</span></span> <span data-ttu-id="4d8ce-225">您剛剛已使用 Azure Cosmos DB 建置您的第一個 Node.js Express Web 應用程式，並將它發佈至 Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-225">You have just built your first Node.js Express Web Application using Azure Cosmos DB and published it to Azure Websites.</span></span>

    <span data-ttu-id="4d8ce-226">如果您想要下載或參考本教學課程的完整參考應用程式，可以從 [GitHub][GitHub] 進行下載。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-226">If you want to download or refer to the complete reference application for this tutorial, it can be downloaded from [GitHub][GitHub].</span></span>

## <span data-ttu-id="4d8ce-227"><a name="_Toc395637775"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="4d8ce-227"><a name="_Toc395637775"></a>Next steps</span></span>

* <span data-ttu-id="4d8ce-228">需要使用 Azure Cosmos DB 來執行規模和效能測試嗎？</span><span class="sxs-lookup"><span data-stu-id="4d8ce-228">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="4d8ce-229">請參閱 [Azure Cosmos DB 的效能和規模測試](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="4d8ce-229">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="4d8ce-230">了解如何[監視 Azure Cosmos DB 帳戶](monitor-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-230">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="4d8ce-231">在 [Query Playground](https://www.documentdb.com/sql/demo)中，針對範例資料集執行查詢。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-231">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="4d8ce-232">探索 [Azure Cosmos DB 文件](https://docs.microsoft.com/azure/documentdb/)。</span><span class="sxs-lookup"><span data-stu-id="4d8ce-232">Explore the [Azure Cosmos DB documentation](https://docs.microsoft.com/azure/documentdb/).</span></span>

[Node.js]: http://nodejs.org/
[Git]: http://git-scm.com/
[GitHub]: https://github.com/Azure-Samples/documentdb-node-todo-app

