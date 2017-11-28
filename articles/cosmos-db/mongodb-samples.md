---
title: "aaaUse MongoDB Api toobuild Azure Cosmos DB 應用程式 |Microsoft 文件"
description: "建立線上資料庫使用 MongoDB hello Azure Cosmos DB Api 教學課程。"
keywords: "mongodb 範例"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: fb38bc53-3561-487d-9e03-20f232319a87
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: anhoh
ms.openlocfilehash: 09be4362fe3aac02e0163325f958210be9598383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-azure-cosmos-db-api-for-mongodb-app-using-nodejs"></a><span data-ttu-id="00b80-104">使用 Node.js 建置 Azure Cosmos DB：適用於 MongoDB 的 API 應用程式</span><span class="sxs-lookup"><span data-stu-id="00b80-104">Build an Azure Cosmos DB: API for MongoDB app using Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="00b80-105">.NET</span><span class="sxs-lookup"><span data-stu-id="00b80-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="00b80-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="00b80-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="00b80-107">Java</span><span class="sxs-lookup"><span data-stu-id="00b80-107">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="00b80-108">Node.js for MongoDB</span><span class="sxs-lookup"><span data-stu-id="00b80-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="00b80-109">Node.js</span><span class="sxs-lookup"><span data-stu-id="00b80-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="00b80-110">C++</span><span class="sxs-lookup"><span data-stu-id="00b80-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
>

<span data-ttu-id="00b80-111">此範例將示範如何 toobuild Azure Cosmos DB： 使用 Node.js MongoDB 主控台應用程式的 API。</span><span class="sxs-lookup"><span data-stu-id="00b80-111">This example shows you how toobuild an Azure Cosmos DB: API for MongoDB console app using Node.js.</span></span>

<span data-ttu-id="00b80-112">toouse 此範例中，您必須：</span><span class="sxs-lookup"><span data-stu-id="00b80-112">toouse this example, you must:</span></span>

* <span data-ttu-id="00b80-113">[建立](create-mongodb-dotnet.md#create-account) Azure Cosmos DB：適用於 MongoDB 的 API 帳戶。</span><span class="sxs-lookup"><span data-stu-id="00b80-113">[Create](create-mongodb-dotnet.md#create-account) an Azure Cosmos DB: API for MongoDB account.</span></span>
* <span data-ttu-id="00b80-114">擷取 MongoDB [連接字串](connect-mongodb-account.md)資訊。</span><span class="sxs-lookup"><span data-stu-id="00b80-114">Retrieve your MongoDB [connection string](connect-mongodb-account.md) information.</span></span>

## <a name="create-hello-app"></a><span data-ttu-id="00b80-115">建立 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="00b80-115">Create hello app</span></span>

1. <span data-ttu-id="00b80-116">建立*app.js*檔以及複製與貼上下列程式碼 hello。</span><span class="sxs-lookup"><span data-stu-id="00b80-116">Create a *app.js* file and copy & paste hello code below.</span></span>

    ```nodejs
    var MongoClient = require('mongodb').MongoClient;
    var assert = require('assert');
    var ObjectId = require('mongodb').ObjectID;
    var url = 'mongodb://<endpoint>:<password>@<endpoint>.documents.azure.com:10255/?ssl=true';

    var insertDocument = function(db, callback) {
    db.collection('families').insertOne( {
            "id": "AndersenFamily",
            "lastName": "Andersen",
            "parents": [
                { "firstName": "Thomas" },
                { "firstName": "Mary Kay" }
            ],
            "children": [
                { "firstName": "John", "gender": "male", "grade": 7 }
            ],
            "pets": [
                { "givenName": "Fluffy" }
            ],
            "address": { "country": "USA", "state": "WA", "city": "Seattle" }
        }, function(err, result) {
        assert.equal(err, null);
        console.log("Inserted a document into hello families collection.");
        callback();
    });
    };
    
    var findFamilies = function(db, callback) {
    var cursor =db.collection('families').find( );
    cursor.each(function(err, doc) {
        assert.equal(err, null);
        if (doc != null) {
            console.dir(doc);
        } else {
            callback();
        }
    });
    };
    
    var updateFamilies = function(db, callback) {
    db.collection('families').updateOne(
        { "lastName" : "Andersen" },
        {
            $set: { "pets": [
                { "givenName": "Fluffy" },
                { "givenName": "Rocky"}
            ] },
            $currentDate: { "lastModified": true }
        }, function(err, results) {
        console.log(results);
        callback();
    });
    };
    
    var removeFamilies = function(db, callback) {
    db.collection('families').deleteMany(
        { "lastName": "Andersen" },
        function(err, results) {
            console.log(results);
            callback();
        }
    );
    };
    
    MongoClient.connect(url, function(err, db) {
    assert.equal(null, err);
    insertDocument(db, function() {
        findFamilies(db, function() {
        updateFamilies(db, function() {
            removeFamilies(db, function() {
                db.close();
            });
        });
        });
    });
    });
    ```

2. <span data-ttu-id="00b80-117">修改下列 hello 中的變數的 hello *app.js*您的帳戶設定之每個檔案 (深入了解如何 toofind 您[連接字串](connect-mongodb-account.md)):</span><span class="sxs-lookup"><span data-stu-id="00b80-117">Modify hello following variables in hello *app.js* file per your account settings (Learn how toofind your [connection string](connect-mongodb-account.md)):</span></span>
   
    ```nodejs
    var url = 'mongodb://<endpoint>:<password>@<endpoint>.documents.azure.com:10255/?ssl=true';
    ```
     
3. <span data-ttu-id="00b80-118">開啟您最愛的終端機，執行 **npm install mongodb --save**，然後使用 **node app.js** 執行您的應用程式</span><span class="sxs-lookup"><span data-stu-id="00b80-118">Open your favorite terminal, run **npm install mongodb --save**, then run your app with **node app.js**</span></span>

## <a name="next-steps"></a><span data-ttu-id="00b80-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="00b80-119">Next steps</span></span>
* <span data-ttu-id="00b80-120">了解如何太[使用 MongoChef](mongodb-mongochef.md)與您 Azure Cosmos DB: MongoDB 帳戶的 API。</span><span class="sxs-lookup"><span data-stu-id="00b80-120">Learn how too[use MongoChef](mongodb-mongochef.md) with your Azure Cosmos DB: API for MongoDB account.</span></span>
