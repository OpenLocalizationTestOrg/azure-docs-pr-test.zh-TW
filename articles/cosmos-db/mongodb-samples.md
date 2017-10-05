---
title: "使用 MongoDB API 建置 Azure Cosmos DB 應用程式 | Microsoft Docs"
description: "使用適用於 MongoDB 的 Azure Cosmos DB API 建立線上資料庫的教學課程。"
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
ms.openlocfilehash: 433d2e585c884a10e7e923a0b27c179a95410d01
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="build-an-azure-cosmos-db-api-for-mongodb-app-using-nodejs"></a><span data-ttu-id="f3ed0-104">使用 Node.js 建置 Azure Cosmos DB：適用於 MongoDB 的 API 應用程式</span><span class="sxs-lookup"><span data-stu-id="f3ed0-104">Build an Azure Cosmos DB: API for MongoDB app using Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f3ed0-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f3ed0-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="f3ed0-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="f3ed0-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="f3ed0-107">Java</span><span class="sxs-lookup"><span data-stu-id="f3ed0-107">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="f3ed0-108">Node.js for MongoDB</span><span class="sxs-lookup"><span data-stu-id="f3ed0-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="f3ed0-109">Node.js</span><span class="sxs-lookup"><span data-stu-id="f3ed0-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="f3ed0-110">C++</span><span class="sxs-lookup"><span data-stu-id="f3ed0-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
>

<span data-ttu-id="f3ed0-111">此範例將示範如何使用 Node.js 建置 Azure Cosmos DB：適用於 MongoDB 的 API 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3ed0-111">This example shows you how to build an Azure Cosmos DB: API for MongoDB console app using Node.js.</span></span>

<span data-ttu-id="f3ed0-112">若要使用此範例，您必須︰</span><span class="sxs-lookup"><span data-stu-id="f3ed0-112">To use this example, you must:</span></span>

* <span data-ttu-id="f3ed0-113">[建立](create-mongodb-dotnet.md#create-account) Azure Cosmos DB：適用於 MongoDB 的 API 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3ed0-113">[Create](create-mongodb-dotnet.md#create-account) an Azure Cosmos DB: API for MongoDB account.</span></span>
* <span data-ttu-id="f3ed0-114">擷取 MongoDB [連接字串](connect-mongodb-account.md)資訊。</span><span class="sxs-lookup"><span data-stu-id="f3ed0-114">Retrieve your MongoDB [connection string](connect-mongodb-account.md) information.</span></span>

## <a name="create-the-app"></a><span data-ttu-id="f3ed0-115">建立應用程式</span><span class="sxs-lookup"><span data-stu-id="f3ed0-115">Create the app</span></span>

1. <span data-ttu-id="f3ed0-116">建立 *app.js* 檔案，複製並貼上下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="f3ed0-116">Create a *app.js* file and copy & paste the code below.</span></span>

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
        console.log("Inserted a document into the families collection.");
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

2. <span data-ttu-id="f3ed0-117">在 *app.js* 中根據每個帳戶設定 (了解如何尋找您的[連接字串](connect-mongodb-account.md)) 修改下列變數：</span><span class="sxs-lookup"><span data-stu-id="f3ed0-117">Modify the following variables in the *app.js* file per your account settings (Learn how to find your [connection string](connect-mongodb-account.md)):</span></span>
   
    ```nodejs
    var url = 'mongodb://<endpoint>:<password>@<endpoint>.documents.azure.com:10255/?ssl=true';
    ```
     
3. <span data-ttu-id="f3ed0-118">開啟您最愛的終端機，執行 **npm install mongodb --save**，然後使用 **node app.js** 執行您的應用程式</span><span class="sxs-lookup"><span data-stu-id="f3ed0-118">Open your favorite terminal, run **npm install mongodb --save**, then run your app with **node app.js**</span></span>

## <a name="next-steps"></a><span data-ttu-id="f3ed0-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f3ed0-119">Next steps</span></span>
* <span data-ttu-id="f3ed0-120">了解如何[使用 MongoChef](mongodb-mongochef.md) 搭配您的 Azure Cosmos DB：適用於 MongoDB 的 API 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3ed0-120">Learn how to [use MongoChef](mongodb-mongochef.md) with your Azure Cosmos DB: API for MongoDB account.</span></span>
