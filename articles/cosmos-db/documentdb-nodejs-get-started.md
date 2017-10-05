---
title: "適用於 Azure Cosmos DB 的 DocumentDB API 之 Node.js 教學課程 | Microsoft Docs"
description: "使用 DocumentDB API 所建立的 Cosmos DB 之 Node.js 教學課程。"
keywords: "node.js 教學課程，節點資料庫"
services: cosmos-db
documentationcenter: node.js
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: 14d52110-1dce-4ac0-9dd9-f936afccd550
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: node
ms.topic: article
ms.date: 08/14/2017
ms.author: anhoh
ms.openlocfilehash: 6510e0270bb2efa252a2b2ad40014c5d26b74a81
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="nodejs-tutorial-use-the-documentdb-api-in-azure-cosmos-db-to-create-a-nodejs-console-application"></a><span data-ttu-id="5bdee-104">Node.js 教學課程：使用 Azure Cosmos DB 中的 DocumentDB API 以建立 Node.js 主控台應用程式</span><span class="sxs-lookup"><span data-stu-id="5bdee-104">Node.js tutorial: Use the DocumentDB API in Azure Cosmos DB to create a Node.js console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5bdee-105">.NET</span><span class="sxs-lookup"><span data-stu-id="5bdee-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="5bdee-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="5bdee-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="5bdee-107">Node.js for MongoDB</span><span class="sxs-lookup"><span data-stu-id="5bdee-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="5bdee-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="5bdee-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="5bdee-109">Java</span><span class="sxs-lookup"><span data-stu-id="5bdee-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="5bdee-110">C++</span><span class="sxs-lookup"><span data-stu-id="5bdee-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="5bdee-111">歡迎使用 Azure Cosmos DB Node.js SDK 的 Node.js 教學課程！</span><span class="sxs-lookup"><span data-stu-id="5bdee-111">Welcome to the Node.js tutorial for the Azure Cosmos DB Node.js SDK!</span></span> <span data-ttu-id="5bdee-112">完成本教學課程之後，您將會有一個主控台應用程式，可用來建立和查詢 Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="5bdee-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="5bdee-113">本文將討論：</span><span class="sxs-lookup"><span data-stu-id="5bdee-113">We'll cover:</span></span>

* <span data-ttu-id="5bdee-114">建立及連線至 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="5bdee-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="5bdee-115">設定您的應用程式</span><span class="sxs-lookup"><span data-stu-id="5bdee-115">Setting up your application</span></span>
* <span data-ttu-id="5bdee-116">建立節點資料庫</span><span class="sxs-lookup"><span data-stu-id="5bdee-116">Creating a node database</span></span>
* <span data-ttu-id="5bdee-117">建立集合</span><span class="sxs-lookup"><span data-stu-id="5bdee-117">Creating a collection</span></span>
* <span data-ttu-id="5bdee-118">建立 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="5bdee-118">Creating JSON documents</span></span>
* <span data-ttu-id="5bdee-119">查詢集合</span><span class="sxs-lookup"><span data-stu-id="5bdee-119">Querying the collection</span></span>
* <span data-ttu-id="5bdee-120">取代文件</span><span class="sxs-lookup"><span data-stu-id="5bdee-120">Replacing a document</span></span>
* <span data-ttu-id="5bdee-121">刪除文件</span><span class="sxs-lookup"><span data-stu-id="5bdee-121">Deleting a document</span></span>
* <span data-ttu-id="5bdee-122">刪除節點資料庫</span><span class="sxs-lookup"><span data-stu-id="5bdee-122">Deleting the node database</span></span>

<span data-ttu-id="5bdee-123">沒有時間嗎？</span><span class="sxs-lookup"><span data-stu-id="5bdee-123">Don't have time?</span></span> <span data-ttu-id="5bdee-124">別擔心！</span><span class="sxs-lookup"><span data-stu-id="5bdee-124">Don't worry!</span></span> <span data-ttu-id="5bdee-125">您可以在 [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started)上找到完整的方案。</span><span class="sxs-lookup"><span data-stu-id="5bdee-125">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span> <span data-ttu-id="5bdee-126">請參閱 [取得完整的解決方案](#GetSolution) ，以取得簡要指示。</span><span class="sxs-lookup"><span data-stu-id="5bdee-126">See [Get the complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="5bdee-127">完成 Node.js 教學課程之後，請使用此頁面頂端和底部的投票按鈕來提供意見。</span><span class="sxs-lookup"><span data-stu-id="5bdee-127">After you've completed the Node.js tutorial, please use the voting buttons at the top and bottom of this page to give us feedback.</span></span> <span data-ttu-id="5bdee-128">如果想要我們直接與您連絡，歡迎在留言中留下電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="5bdee-128">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="5bdee-129">讓我們開始吧！</span><span class="sxs-lookup"><span data-stu-id="5bdee-129">Now let's get started!</span></span>

## <a name="prerequisites-for-the-nodejs-tutorial"></a><span data-ttu-id="5bdee-130">Node.js 教學課程的必要條件</span><span class="sxs-lookup"><span data-stu-id="5bdee-130">Prerequisites for the Node.js tutorial</span></span>
<span data-ttu-id="5bdee-131">請確定您具有下列項目：</span><span class="sxs-lookup"><span data-stu-id="5bdee-131">Please make sure you have the following:</span></span>

* <span data-ttu-id="5bdee-132">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bdee-132">An active Azure account.</span></span> <span data-ttu-id="5bdee-133">如果您沒有帳戶，您可以註冊 [免費 Azure 試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="5bdee-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
    * <span data-ttu-id="5bdee-134">或者，您可以使用 [Azure Cosmos DB 模擬器](local-emulator.md)來進行本教學課程。</span><span class="sxs-lookup"><span data-stu-id="5bdee-134">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="5bdee-135">[Node.js](https://nodejs.org/) v0.10.29 版或更高版本。</span><span class="sxs-lookup"><span data-stu-id="5bdee-135">[Node.js](https://nodejs.org/) version v0.10.29 or higher.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="5bdee-136">步驟 1：建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="5bdee-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="5bdee-137">讓我們來建立 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5bdee-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="5bdee-138">如果您已經擁有想要使用的帳戶，就可以直接跳到[設定您的 Node.js 應用程式](#SetupNode)。</span><span class="sxs-lookup"><span data-stu-id="5bdee-138">If you already have an account you want to use, you can skip ahead to [Set up your Node.js application](#SetupNode).</span></span> <span data-ttu-id="5bdee-139">如果您是使用「Azure Cosmos DB 模擬器」，請依照 [Azure Cosmos DB 模擬器](local-emulator.md)的步驟來設定模擬器，然後直接跳到[設定您的 Node.js 應用程式](#SetupNode)。</span><span class="sxs-lookup"><span data-stu-id="5bdee-139">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Node.js application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="5bdee-140"><a id="SetupNode"></a>步驟 2：設定您的 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="5bdee-140"><a id="SetupNode"></a>Step 2: Set up your Node.js application</span></span>
1. <span data-ttu-id="5bdee-141">開啟您偏好的終端機。</span><span class="sxs-lookup"><span data-stu-id="5bdee-141">Open your favorite terminal.</span></span>
2. <span data-ttu-id="5bdee-142">找出您想儲存 Node.js 應用程式的資料夾或目錄位置。</span><span class="sxs-lookup"><span data-stu-id="5bdee-142">Locate the folder or directory where you'd like to save your Node.js application.</span></span>
3. <span data-ttu-id="5bdee-143">使用下列命令，建立兩個空白的 JavaScript 檔案：</span><span class="sxs-lookup"><span data-stu-id="5bdee-143">Create two empty JavaScript files with the following commands:</span></span>
   * <span data-ttu-id="5bdee-144">Windows:</span><span class="sxs-lookup"><span data-stu-id="5bdee-144">Windows:</span></span>
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * <span data-ttu-id="5bdee-145">Linux/OS X：</span><span class="sxs-lookup"><span data-stu-id="5bdee-145">Linux/OS X:</span></span>
     * ```touch app.js```
     * ```touch config.js```
4. <span data-ttu-id="5bdee-146">透過 npm 安裝 documentdb 模組。</span><span class="sxs-lookup"><span data-stu-id="5bdee-146">Install the documentdb module via npm.</span></span> <span data-ttu-id="5bdee-147">使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="5bdee-147">Use the following command:</span></span>
   * ```npm install documentdb --save```

<span data-ttu-id="5bdee-148">太棒了！</span><span class="sxs-lookup"><span data-stu-id="5bdee-148">Great!</span></span> <span data-ttu-id="5bdee-149">現在已完成安裝程式，讓我們開始撰寫一些程式碼。</span><span class="sxs-lookup"><span data-stu-id="5bdee-149">Now that you've finished setting up, let's start writing some code.</span></span>

## <span data-ttu-id="5bdee-150"><a id="Config"></a>步驟 3：設定您的應用程式設定</span><span class="sxs-lookup"><span data-stu-id="5bdee-150"><a id="Config"></a>Step 3: Set your app's configurations</span></span>
<span data-ttu-id="5bdee-151">在您慣用的文字編輯器中開啟 ```config.js```。</span><span class="sxs-lookup"><span data-stu-id="5bdee-151">Open ```config.js``` in your favorite text editor.</span></span>

<span data-ttu-id="5bdee-152">然後，複製並貼上以下的程式碼片段，以及將屬性 ```config.endpoint``` 和 ```config.primaryKey``` 設定為您的 Azure Cosmos DB 端點 uri 和主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="5bdee-152">Then, copy and paste the code snippet below and set properties ```config.endpoint``` and ```config.primaryKey``` to your Azure Cosmos DB endpoint uri and primary key.</span></span> <span data-ttu-id="5bdee-153">您可以在 [Azure 入口網站](https://portal.azure.com)找到這些設定。</span><span class="sxs-lookup"><span data-stu-id="5bdee-153">Both these configurations can be found in the [Azure portal](https://portal.azure.com).</span></span>

![node.js 教學課程 - 顯示 Azure Cosmos DB 帳戶的 Azure 入口網站螢幕擷取畫面，內含反白顯示的 [主動式] 集線器、[Azure Cosmos DB 帳戶] 刀鋒視窗上反白顯示的 [金鑰] 按鈕、[金鑰] 刀鋒視窗上反白顯示的 [URI]、[主要金鑰] 和 [次要金鑰] 值 - 節點資料庫][keys]

    // ADD THIS PART TO YOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

<span data-ttu-id="5bdee-155">在您設定 ```config.endpoint``` 和 ```config.authKey``` 屬性的位置下面，複製 ```database id```、```collection id``` 和 ```JSON documents``` 並貼到您的 ```config``` 物件。</span><span class="sxs-lookup"><span data-stu-id="5bdee-155">Copy and paste the ```database id```, ```collection id```, and ```JSON documents``` to your ```config``` object below where you set your ```config.endpoint``` and ```config.authKey``` properties.</span></span> <span data-ttu-id="5bdee-156">如果您已經有想要儲存於資料庫中的資料，就可以使用 Azure Cosmos DB 的 [資料移轉工具](import-data.md)，而不用新增文件定義。</span><span class="sxs-lookup"><span data-stu-id="5bdee-156">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) rather than adding the document definitions.</span></span>

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

    // ADD THIS PART TO YOUR CODE
    config.database = {
        "id": "FamilyDB"
    };

    config.collection = {
        "id": "FamilyColl"
    };

    config.documents = {
        "Andersen": {
            "id": "Anderson.1",
            "lastName": "Andersen",
            "parents": [{
                "firstName": "Thomas"
            }, {
                    "firstName": "Mary Kay"
                }],
            "children": [{
                "firstName": "Henriette Thaulow",
                "gender": "female",
                "grade": 5,
                "pets": [{
                    "givenName": "Fluffy"
                }]
            }],
            "address": {
                "state": "WA",
                "county": "King",
                "city": "Seattle"
            }
        },
        "Wakefield": {
            "id": "Wakefield.7",
            "parents": [{
                "familyName": "Wakefield",
                "firstName": "Robin"
            }, {
                    "familyName": "Miller",
                    "firstName": "Ben"
                }],
            "children": [{
                "familyName": "Merriam",
                "firstName": "Jesse",
                "gender": "female",
                "grade": 8,
                "pets": [{
                    "givenName": "Goofy"
                }, {
                        "givenName": "Shadow"
                    }]
            }, {
                    "familyName": "Miller",
                    "firstName": "Lisa",
                    "gender": "female",
                    "grade": 1
                }],
            "address": {
                "state": "NY",
                "county": "Manhattan",
                "city": "NY"
            },
            "isRegistered": false
        }
    };


<span data-ttu-id="5bdee-157">資料庫、集合和文件定義將作為您 Azure Cosmos DB 的 ```database id```、```collection id``` 和文件的資料。</span><span class="sxs-lookup"><span data-stu-id="5bdee-157">The database, collection, and document definitions will act as your Azure Cosmos DB ```database id```, ```collection id```, and documents' data.</span></span>

<span data-ttu-id="5bdee-158">最後，匯出您的 ```config``` 物件，如此就可以在 ```app.js``` 檔案中參考它。</span><span class="sxs-lookup"><span data-stu-id="5bdee-158">Finally, export your ```config``` object, so that you can reference it within the ```app.js``` file.</span></span>

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART TO YOUR CODE
    module.exports = config;

## <span data-ttu-id="5bdee-159"><a id="Connect"></a>步驟 4：連線至 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="5bdee-159"><a id="Connect"></a> Step 4: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="5bdee-160">在文字編輯器中開啟您的空白 ```app.js``` 檔案。</span><span class="sxs-lookup"><span data-stu-id="5bdee-160">Open your empty ```app.js``` file in the text editor.</span></span> <span data-ttu-id="5bdee-161">複製並貼上以下的程式碼，以匯入 ```documentdb``` 模組和新建的 ```config``` 模組。</span><span class="sxs-lookup"><span data-stu-id="5bdee-161">Copy and paste the code below to import the ```documentdb``` module and your newly created ```config``` module.</span></span>

    // ADD THIS PART TO YOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

<span data-ttu-id="5bdee-162">複製並貼上以下的程式碼，以使用先前儲存的 ```config.endpoint``` 和 ```config.primaryKey``` 來建立新的 DocumentClient。</span><span class="sxs-lookup"><span data-stu-id="5bdee-162">Copy and paste the code to use the previously saved ```config.endpoint``` and ```config.primaryKey``` to create a new DocumentClient.</span></span>

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART TO YOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

<span data-ttu-id="5bdee-163">您現在具有程式碼，可將 Azure Cosmos DB 用戶端初始化，讓我們看看如何使用 Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="5bdee-163">Now that you have the code to initialize the Azure Cosmos DB client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <a name="step-5-create-a-node-database"></a><span data-ttu-id="5bdee-164">步驟 5：建立節點資料庫</span><span class="sxs-lookup"><span data-stu-id="5bdee-164">Step 5: Create a Node database</span></span>
<span data-ttu-id="5bdee-165">複製並貼上以下的程式碼，以設定 [找不到] 的HTTP 狀態、資料庫 url 和集合 url。</span><span class="sxs-lookup"><span data-stu-id="5bdee-165">Copy and paste the code below to set the HTTP status for Not Found, the database url, and the collection url.</span></span> <span data-ttu-id="5bdee-166">這些 url 可讓 Azure Cosmos DB 用戶端尋找正確的資料庫和集合。</span><span class="sxs-lookup"><span data-stu-id="5bdee-166">These urls are how the Azure Cosmos DB client will find the right database and collection.</span></span>

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART TO YOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

<span data-ttu-id="5bdee-167">可以使用 **DocumentClient** 類別的 [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) 函式來建立[資料庫](documentdb-resources.md#databases)。</span><span class="sxs-lookup"><span data-stu-id="5bdee-167">A [database](documentdb-resources.md#databases) can be created by using the [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span></span> <span data-ttu-id="5bdee-168">資料庫是分割給多個集合之文件儲存體的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="5bdee-168">A database is the logical container of document storage partitioned across collections.</span></span>

<span data-ttu-id="5bdee-169">複製並貼上 **getDatabase** 函式，以 ```config``` 物件中指定的 ```id```，在 app.js 檔案中加入建立新資料庫的函式。</span><span class="sxs-lookup"><span data-stu-id="5bdee-169">Copy and paste the **getDatabase** function for creating your new database in the app.js file with the ```id``` specified in the ```config``` object.</span></span> <span data-ttu-id="5bdee-170">此函數會檢查具有相同 ```FamilyRegistry``` 識別碼的資料庫不存在。</span><span class="sxs-lookup"><span data-stu-id="5bdee-170">The function will check if the database with the same ```FamilyRegistry``` id does not already exist.</span></span> <span data-ttu-id="5bdee-171">如果存在，我們會傳回該資料庫，而不會建立新資料庫。</span><span class="sxs-lookup"><span data-stu-id="5bdee-171">If it does exist, we'll return that database instead of creating a new one.</span></span>

    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

    // ADD THIS PART TO YOUR CODE
    function getDatabase() {
        console.log(`Getting database:\n${config.database.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDatabase(databaseUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDatabase(config.database, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

<span data-ttu-id="5bdee-172">複製並貼上以下的程式碼，以設定 **getDatabase** 函式來加入協助程式函式 **exit**，該函式會列印結束訊息和呼叫 **getDatabase** 函式。</span><span class="sxs-lookup"><span data-stu-id="5bdee-172">Copy and paste the code below where you set the **getDatabase** function to add the helper function **exit** that will print the exit message and the call to **getDatabase** function.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
    function exit(message) {
        console.log(message);
        console.log('Press any key to exit');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', process.exit.bind(process, 0));
    }

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="5bdee-173">在終端機中，找到您的 ```app.js``` 檔案並執行命令：```node app.js```</span><span class="sxs-lookup"><span data-stu-id="5bdee-173">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="5bdee-174">恭喜！</span><span class="sxs-lookup"><span data-stu-id="5bdee-174">Congratulations!</span></span> <span data-ttu-id="5bdee-175">您已成功建立 Azure Cosmos DB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="5bdee-175">You have successfully created an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="5bdee-176"><a id="CreateColl"></a>步驟 6：建立集合</span><span class="sxs-lookup"><span data-stu-id="5bdee-176"><a id="CreateColl"></a>Step 6: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="5bdee-177">**CreateDocumentCollectionAsync** 會建立具有定價含意的新集合。</span><span class="sxs-lookup"><span data-stu-id="5bdee-177">**CreateDocumentCollectionAsync** will create a new collection, which has pricing implications.</span></span> <span data-ttu-id="5bdee-178">如需詳細資訊，請造訪 [定價頁面](https://azure.microsoft.com/pricing/details/cosmos-db/)。</span><span class="sxs-lookup"><span data-stu-id="5bdee-178">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="5bdee-179">可以使用 **DocumentClient** 類別的 [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) 函式建立[集合](documentdb-resources.md#collections)。</span><span class="sxs-lookup"><span data-stu-id="5bdee-179">A [collection](documentdb-resources.md#collections) can be created by using the [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span></span> <span data-ttu-id="5bdee-180">集合是 JSON 文件和相關聯 JavaScript 應用程式邏輯的容器。</span><span class="sxs-lookup"><span data-stu-id="5bdee-180">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="5bdee-181">將 **getCollection** 函式複製並貼到 app.js 檔案中的 **getDatabase** 函式之下，以 ```config``` 物件中指定的 ```id``` 建立新的集合。</span><span class="sxs-lookup"><span data-stu-id="5bdee-181">Copy and paste the **getCollection** function underneath the **getDatabase** function in the app.js file to create your new collection with the ```id``` specified in the ```config``` object.</span></span> <span data-ttu-id="5bdee-182">同樣地，我們會檢查確定具有相同 ```FamilyCollection``` 識別碼的集合不存在。</span><span class="sxs-lookup"><span data-stu-id="5bdee-182">Again, we'll check to make sure a collection with the same ```FamilyCollection``` id does not already exist.</span></span> <span data-ttu-id="5bdee-183">如果存在，我們會傳回該集合，而不會建立新集合。</span><span class="sxs-lookup"><span data-stu-id="5bdee-183">If it does exist, we'll return that collection instead of creating a new one.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
    function getCollection() {
        console.log(`Getting collection:\n${config.collection.id}\n`);

        return new Promise((resolve, reject) => {
            client.readCollection(collectionUrl, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    }

<span data-ttu-id="5bdee-184">將以下的程式碼複製並貼到對 **getDatabase** 的呼叫之下，以執行 **getCollection** 函式。</span><span class="sxs-lookup"><span data-stu-id="5bdee-184">Copy and paste the code below the call to **getDatabase** to execute the **getCollection** function.</span></span>

    getDatabase()

    // ADD THIS PART TO YOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="5bdee-185">在終端機中，找到您的 ```app.js``` 檔案並執行命令：```node app.js```</span><span class="sxs-lookup"><span data-stu-id="5bdee-185">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="5bdee-186">恭喜！</span><span class="sxs-lookup"><span data-stu-id="5bdee-186">Congratulations!</span></span> <span data-ttu-id="5bdee-187">您已成功建立 Azure Cosmos DB 集合。</span><span class="sxs-lookup"><span data-stu-id="5bdee-187">You have successfully created an Azure Cosmos DB collection.</span></span>

## <span data-ttu-id="5bdee-188"><a id="CreateDoc"></a>步驟 7：建立文件</span><span class="sxs-lookup"><span data-stu-id="5bdee-188"><a id="CreateDoc"></a>Step 7: Create a document</span></span>
<span data-ttu-id="5bdee-189">可以使用 **DocumentClient** 類別的 [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) 函式來建立[文件](documentdb-resources.md#documents)。</span><span class="sxs-lookup"><span data-stu-id="5bdee-189">A [document](documentdb-resources.md#documents) can be created by using the [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of the **DocumentClient** class.</span></span> <span data-ttu-id="5bdee-190">文件會是使用者定義的 (任意) JSON 內容。</span><span class="sxs-lookup"><span data-stu-id="5bdee-190">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="5bdee-191">您現在可以將文件插入 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="5bdee-191">You can now insert a document into Azure Cosmos DB.</span></span>

<span data-ttu-id="5bdee-192">將 **getFamilyDocument** 函式複製並貼到 **getCollection** 函式之下，以便建立包含 ```config``` 物件中儲存之 JSON 資料文件。</span><span class="sxs-lookup"><span data-stu-id="5bdee-192">Copy and paste the **getFamilyDocument** function underneath the **getCollection** function for creating the documents containing the JSON data saved in the ```config``` object.</span></span> <span data-ttu-id="5bdee-193">同樣地，我們會檢查以確定具有相同識別碼的文件不存在。</span><span class="sxs-lookup"><span data-stu-id="5bdee-193">Again, we'll check to make sure a document with the same id does not already exist.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
    function getFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Getting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.readDocument(documentUrl, { partitionKey: document.district }, (err, result) => {
                if (err) {
                    if (err.code == HttpStatusCodes.NOTFOUND) {
                        client.createDocument(collectionUrl, document, (err, created) => {
                            if (err) reject(err)
                            else resolve(created);
                        });
                    } else {
                        reject(err);
                    }
                } else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="5bdee-194">將以下的程式碼複製並貼到對 **getCollection** 的呼叫之下，以執行 **getFamilyDocument** 函式。</span><span class="sxs-lookup"><span data-stu-id="5bdee-194">Copy and paste the code below the call to **getCollection** to execute the **getFamilyDocument** function.</span></span>

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="5bdee-195">在終端機中，找到您的 ```app.js``` 檔案並執行命令：```node app.js```</span><span class="sxs-lookup"><span data-stu-id="5bdee-195">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="5bdee-196">恭喜！</span><span class="sxs-lookup"><span data-stu-id="5bdee-196">Congratulations!</span></span> <span data-ttu-id="5bdee-197">您已成功建立 Azure Cosmos DB 文件。</span><span class="sxs-lookup"><span data-stu-id="5bdee-197">You have successfully created an Azure Cosmos DB document.</span></span>

![node.js 教學課程 - 說明帳戶、資料庫、集合和文件之間階層式關聯性的圖表 - 節點資料庫](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <span data-ttu-id="5bdee-199"><a id="Query"></a>步驟 8︰查詢 Azure Cosmos DB 資源</span><span class="sxs-lookup"><span data-stu-id="5bdee-199"><a id="Query"></a>Step 8: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="5bdee-200">Azure Cosmos DB 支援針對儲存於每個集合的 JSON 文件進行[豐富查詢](documentdb-sql-query.md)。</span><span class="sxs-lookup"><span data-stu-id="5bdee-200">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="5bdee-201">下列範例程式碼示範您可以針對集合中之文件執行的查詢。</span><span class="sxs-lookup"><span data-stu-id="5bdee-201">The following sample code shows a query that you can run against the documents in your collection.</span></span>

<span data-ttu-id="5bdee-202">將 **queryCollection** 函式複製並貼到 app.js 檔案中的 **getFamilyDocument** 函式之下。</span><span class="sxs-lookup"><span data-stu-id="5bdee-202">Copy and paste the **queryCollection** function underneath the **getFamilyDocument** function in the app.js file.</span></span> <span data-ttu-id="5bdee-203">Azure Cosmos DB 支援類 SQL 查詢，如下所示。</span><span class="sxs-lookup"><span data-stu-id="5bdee-203">Azure Cosmos DB supports SQL-like queries as shown below.</span></span> <span data-ttu-id="5bdee-204">如需建立複雜查詢的詳細資訊，請參閱[查詢遊樂場](https://www.documentdb.com/sql/demo)和[查詢文件](documentdb-sql-query.md)。</span><span class="sxs-lookup"><span data-stu-id="5bdee-204">For more information on building complex queries, check out the [Query Playground](https://www.documentdb.com/sql/demo) and the [query documentation](documentdb-sql-query.md).</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
    function queryCollection() {
        console.log(`Querying collection through index:\n${config.collection.id}`);

        return new Promise((resolve, reject) => {
            client.queryDocuments(
                collectionUrl,
                'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
            ).toArray((err, results) => {
                if (err) reject(err)
                else {
                    for (var queryResult of results) {
                        let resultString = JSON.stringify(queryResult);
                        console.log(`\tQuery returned ${resultString}`);
                    }
                    console.log();
                    resolve(results);
                }
            });
        });
    };


<span data-ttu-id="5bdee-205">下圖說明如何針對您所建立的集合呼叫 Azure Cosmos DB SQL 查詢語法。</span><span class="sxs-lookup"><span data-stu-id="5bdee-205">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created.</span></span>

![node.js 教學課程 - 說明查詢範圍和意義的圖表 - 節點資料庫](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

<span data-ttu-id="5bdee-207">因為 Azure Cosmos DB 查詢已侷限於單一集合，所以查詢中的 [FROM](documentdb-sql-query.md#FromClause) 關鍵字是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="5bdee-207">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="5bdee-208">因此，"FROM Families f" 可以換成 "FROM root r"，或您選擇的任何其他變數名稱。</span><span class="sxs-lookup"><span data-stu-id="5bdee-208">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="5bdee-209">依預設，Azure Cosmos DB 會推斷該 Families、root 或您選擇的變數名稱來參考目前的集合。</span><span class="sxs-lookup"><span data-stu-id="5bdee-209">Azure Cosmos DB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

<span data-ttu-id="5bdee-210">將以下的程式碼複製並貼到對 **getFamilyDocument** 的呼叫之下，以執行 **queryCollection** 函式。</span><span class="sxs-lookup"><span data-stu-id="5bdee-210">Copy and paste the code below the call to **getFamilyDocument** to execute the **queryCollection** function.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART TO YOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="5bdee-211">在終端機中，找到您的 ```app.js``` 檔案並執行命令：```node app.js```</span><span class="sxs-lookup"><span data-stu-id="5bdee-211">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="5bdee-212">恭喜！</span><span class="sxs-lookup"><span data-stu-id="5bdee-212">Congratulations!</span></span> <span data-ttu-id="5bdee-213">您已成功查詢 Azure Cosmos DB 文件。</span><span class="sxs-lookup"><span data-stu-id="5bdee-213">You have successfully queried Azure Cosmos DB documents.</span></span>

## <span data-ttu-id="5bdee-214"><a id="ReplaceDocument"></a>步驟 9：取代文件</span><span class="sxs-lookup"><span data-stu-id="5bdee-214"><a id="ReplaceDocument"></a>Step 9: Replace a document</span></span>
<span data-ttu-id="5bdee-215">Azure Cosmos DB 支援取代 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="5bdee-215">Azure Cosmos DB supports replacing JSON documents.</span></span>

<span data-ttu-id="5bdee-216">將 **replaceFamilyDocument** 函式複製並貼到 app.js 檔案中的 **queryCollection** 函式之下。</span><span class="sxs-lookup"><span data-stu-id="5bdee-216">Copy and paste the **replaceFamilyDocument** function underneath the **queryCollection** function in the app.js file.</span></span>

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART TO YOUR CODE
    function replaceFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Replacing document:\n${document.id}\n`);
        document.children[0].grade = 6;

        return new Promise((resolve, reject) => {
            client.replaceDocument(documentUrl, document, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="5bdee-217">將以下的程式碼複製並貼到對 **queryCollection** 的呼叫之下，以執行 **replaceDocument** 函式。</span><span class="sxs-lookup"><span data-stu-id="5bdee-217">Copy and paste the code below the call to **queryCollection** to execute the **replaceDocument** function.</span></span> <span data-ttu-id="5bdee-218">此外，再次將此程式碼加入至 **queryCollection** 呼叫，確認已成功變更文件。</span><span class="sxs-lookup"><span data-stu-id="5bdee-218">Also, add the code to call **queryCollection** again to verify that the document had successfully changed.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="5bdee-219">在終端機中，找到您的 ```app.js``` 檔案並執行命令：```node app.js```</span><span class="sxs-lookup"><span data-stu-id="5bdee-219">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="5bdee-220">恭喜！</span><span class="sxs-lookup"><span data-stu-id="5bdee-220">Congratulations!</span></span> <span data-ttu-id="5bdee-221">您已成功取代 Azure Cosmos DB 文件。</span><span class="sxs-lookup"><span data-stu-id="5bdee-221">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="5bdee-222"><a id="DeleteDocument"></a>步驟 10︰刪除文件</span><span class="sxs-lookup"><span data-stu-id="5bdee-222"><a id="DeleteDocument"></a>Step 10: Delete a document</span></span>
<span data-ttu-id="5bdee-223">Azure Cosmos DB 支援刪除 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="5bdee-223">Azure Cosmos DB supports deleting JSON documents.</span></span>

<span data-ttu-id="5bdee-224">將 **deleteFamilyDocument** 函式複製並貼到 **replaceFamilyDocument** 函式之下。</span><span class="sxs-lookup"><span data-stu-id="5bdee-224">Copy and paste the **deleteFamilyDocument** function underneath the **replaceFamilyDocument** function.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART TO YOUR CODE
    function deleteFamilyDocument(document) {
        let documentUrl = `${collectionUrl}/docs/${document.id}`;
        console.log(`Deleting document:\n${document.id}\n`);

        return new Promise((resolve, reject) => {
            client.deleteDocument(documentUrl, (err, result) => {
                if (err) reject(err);
                else {
                    resolve(result);
                }
            });
        });
    };

<span data-ttu-id="5bdee-225">將以下的程式碼複製並貼到對 **queryCollection** 的呼叫之下，以執行 **deleteDocument** 函式。</span><span class="sxs-lookup"><span data-stu-id="5bdee-225">Copy and paste the code below the call to the second **queryCollection** to execute the **deleteDocument** function.</span></span>

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART TO YOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="5bdee-226">在終端機中，找到您的 ```app.js``` 檔案並執行命令：```node app.js```</span><span class="sxs-lookup"><span data-stu-id="5bdee-226">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="5bdee-227">恭喜！</span><span class="sxs-lookup"><span data-stu-id="5bdee-227">Congratulations!</span></span> <span data-ttu-id="5bdee-228">您已成功將 Azure Cosmos DB 文件刪除。</span><span class="sxs-lookup"><span data-stu-id="5bdee-228">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="5bdee-229"><a id="DeleteDatabase"></a>步驟 11：刪除節點資料庫</span><span class="sxs-lookup"><span data-stu-id="5bdee-229"><a id="DeleteDatabase"></a>Step 11: Delete the Node database</span></span>
<span data-ttu-id="5bdee-230">刪除已建立的資料庫將會移除資料庫和所有子系資源 (集合、文件等)。</span><span class="sxs-lookup"><span data-stu-id="5bdee-230">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="5bdee-231">將 **cleanup** 函式複製並貼到 **deleteFamilyDocument** 函式之下，以移除資料庫和所有子系資源。</span><span class="sxs-lookup"><span data-stu-id="5bdee-231">Copy and paste the **cleanup** function underneath the **deleteFamilyDocument** function to remove the database and all the children resources.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART TO YOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${config.database.id}`);

        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    }

<span data-ttu-id="5bdee-232">將以下的程式碼複製並貼到對 **deleteFamilyDocument** 的呼叫之下，以執行 **cleanup** 函式。</span><span class="sxs-lookup"><span data-stu-id="5bdee-232">Copy and paste the code below the call to **deleteFamilyDocument** to execute the **cleanup** function.</span></span>

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART TO YOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <span data-ttu-id="5bdee-233"><a id="Run"></a>步驟 12：一起執行您的 Node.js 應用程式！</span><span class="sxs-lookup"><span data-stu-id="5bdee-233"><a id="Run"></a>Step 12: Run your Node.js application all together!</span></span>
<span data-ttu-id="5bdee-234">總之，呼叫您的函數的順序應如下所示︰</span><span class="sxs-lookup"><span data-stu-id="5bdee-234">Altogether, the sequence for calling your functions should look like this:</span></span>

    getDatabase()
    .then(() => getCollection())
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    .then(() => cleanup())
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="5bdee-235">在終端機中，找到您的 ```app.js``` 檔案並執行命令：```node app.js```</span><span class="sxs-lookup"><span data-stu-id="5bdee-235">In your terminal, locate your ```app.js``` file and run the command: ```node app.js```</span></span>

<span data-ttu-id="5bdee-236">您應該可以看到入門應用程式的輸出。</span><span class="sxs-lookup"><span data-stu-id="5bdee-236">You should see the output of your get started app.</span></span> <span data-ttu-id="5bdee-237">輸出應該會與下列範例文字相符。</span><span class="sxs-lookup"><span data-stu-id="5bdee-237">The output should match the example text below.</span></span>

    Getting database:
    FamilyDB

    Getting collection:
    FamilyColl

    Getting document:
    Anderson.1

    Getting document:
    Wakefield.7

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":5,"pets":[{"givenName":"Fluffy"}]}]

    Replacing document:
    Anderson.1

    Querying collection through index:
    FamilyColl
        Query returned [{"firstName":"Henriette Thaulow","gender":"female","grade":6,"pets":[{"givenName":"Fluffy"}]}]

    Deleting document:
    Anderson.1

    Cleaning up by deleting database FamilyDB
    Completed successfully
    Press any key to exit

<span data-ttu-id="5bdee-238">恭喜！</span><span class="sxs-lookup"><span data-stu-id="5bdee-238">Congratulations!</span></span> <span data-ttu-id="5bdee-239">您已完成 Node.js 教學課程，並擁有您的第一個 Azure Cosmos DB 主控台應用程式！</span><span class="sxs-lookup"><span data-stu-id="5bdee-239">You've created you've completed the Node.js tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="5bdee-240"><a id="GetSolution"></a>取得完整的 Node.js 教學課程方案</span><span class="sxs-lookup"><span data-stu-id="5bdee-240"><a id="GetSolution"></a>Get the complete Node.js tutorial solution</span></span>
<span data-ttu-id="5bdee-241">如果您沒有時間完成本教學課程中的步驟，或只想要下載程式碼，您可以從 [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started) 取得程式碼。</span><span class="sxs-lookup"><span data-stu-id="5bdee-241">If you didn't have time to complete the steps in this tutorial, or just want to download the code, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span>

<span data-ttu-id="5bdee-242">若要執行包含本文中所有範例的 GetStarted 方案，您將需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="5bdee-242">To run the GetStarted solution that contains all the samples in this article, you will need the following:</span></span>

* <span data-ttu-id="5bdee-243">[Azure Cosmos DB 帳戶][create-account]。</span><span class="sxs-lookup"><span data-stu-id="5bdee-243">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="5bdee-244">您可以在 GitHub 上找到 [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) 方案。</span><span class="sxs-lookup"><span data-stu-id="5bdee-244">The [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="5bdee-245">透過 npm 安裝 **documentdb** 模組。</span><span class="sxs-lookup"><span data-stu-id="5bdee-245">Install the **documentdb** module via npm.</span></span> <span data-ttu-id="5bdee-246">使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="5bdee-246">Use the following command:</span></span>

* ```npm install documentdb --save```

<span data-ttu-id="5bdee-247">接下來，將 ```config.js``` 檔案中的 config.endpoint 和 config.authKey 的值更新為如 [步驟 3：設定您的應用程式組態](#Config)中所述。</span><span class="sxs-lookup"><span data-stu-id="5bdee-247">Next, in the ```config.js``` file, update the config.endpoint and config.authKey values as described in [Step 3: Set your app's configurations](#Config).</span></span> 

<span data-ttu-id="5bdee-248">然後在終端機，找到您的 ```app.js``` 檔案並執行命令：```node app.js```。</span><span class="sxs-lookup"><span data-stu-id="5bdee-248">Then in your terminal, locate your ```app.js``` file and run the command: ```node app.js```.</span></span>

<span data-ttu-id="5bdee-249">建置就這麼容易，繼續努力！</span><span class="sxs-lookup"><span data-stu-id="5bdee-249">That's it, build it and you're on your way!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5bdee-250">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5bdee-250">Next steps</span></span>
* <span data-ttu-id="5bdee-251">需要更複雜的 Node.js 範例嗎？</span><span class="sxs-lookup"><span data-stu-id="5bdee-251">Want a more complex Node.js sample?</span></span> <span data-ttu-id="5bdee-252">請參閱[使用 Azure Cosmos DB 來建置 Node.js Web 應用程式](documentdb-nodejs-application.md)。</span><span class="sxs-lookup"><span data-stu-id="5bdee-252">See [Build a Node.js web application using Azure Cosmos DB](documentdb-nodejs-application.md).</span></span>
* <span data-ttu-id="5bdee-253">了解如何[監視 Azure Cosmos DB 帳戶](monitor-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="5bdee-253">Learn how to [monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="5bdee-254">在 [Query Playground](https://www.documentdb.com/sql/demo)中，針對範例資料集執行查詢。</span><span class="sxs-lookup"><span data-stu-id="5bdee-254">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="5bdee-255">如需深入了解程式設計模型，請參閱 [Azure Cosmos DB 文件頁面](https://azure.microsoft.com/documentation/services/documentdb/)中的＜開發＞一節。</span><span class="sxs-lookup"><span data-stu-id="5bdee-255">Learn more about the programming model in the Develop section of the [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
