---
title: "hello DocumentDB API 針對 Azure Cosmos DB aaaNode.js 教學課程 |Microsoft 文件"
description: "建立以 hello DocumentDB API Cosmos DB Node.js 教學課程。"
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
ms.openlocfilehash: fce244c6a5f321608e82ca51a2c987e84b98bffa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-tutorial-use-hello-documentdb-api-in-azure-cosmos-db-toocreate-a-nodejs-console-application"></a><span data-ttu-id="f2dc8-104">Node.js 教學課程： Azure Cosmos DB toocreate Node.js 主控台應用程式中的使用 hello DocumentDB API</span><span class="sxs-lookup"><span data-stu-id="f2dc8-104">Node.js tutorial: Use hello DocumentDB API in Azure Cosmos DB toocreate a Node.js console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f2dc8-105">.NET</span><span class="sxs-lookup"><span data-stu-id="f2dc8-105">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="f2dc8-106">.NET Core</span><span class="sxs-lookup"><span data-stu-id="f2dc8-106">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="f2dc8-107">Node.js for MongoDB</span><span class="sxs-lookup"><span data-stu-id="f2dc8-107">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="f2dc8-108">Node.js</span><span class="sxs-lookup"><span data-stu-id="f2dc8-108">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="f2dc8-109">Java</span><span class="sxs-lookup"><span data-stu-id="f2dc8-109">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="f2dc8-110">C++</span><span class="sxs-lookup"><span data-stu-id="f2dc8-110">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="f2dc8-111"> 褖畫惎 toohello hello Azure Cosmos DB Node.js SDK for Node.js 教學課程 ！</span><span class="sxs-lookup"><span data-stu-id="f2dc8-111">Welcome toohello Node.js tutorial for hello Azure Cosmos DB Node.js SDK!</span></span> <span data-ttu-id="f2dc8-112">完成本教學課程之後，您將會有一個主控台應用程式，可用來建立和查詢 Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="f2dc8-113">本文將討論：</span><span class="sxs-lookup"><span data-stu-id="f2dc8-113">We'll cover:</span></span>

* <span data-ttu-id="f2dc8-114">建立及連接 tooan Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="f2dc8-114">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="f2dc8-115">設定您的應用程式</span><span class="sxs-lookup"><span data-stu-id="f2dc8-115">Setting up your application</span></span>
* <span data-ttu-id="f2dc8-116">建立節點資料庫</span><span class="sxs-lookup"><span data-stu-id="f2dc8-116">Creating a node database</span></span>
* <span data-ttu-id="f2dc8-117">建立集合</span><span class="sxs-lookup"><span data-stu-id="f2dc8-117">Creating a collection</span></span>
* <span data-ttu-id="f2dc8-118">建立 JSON 文件</span><span class="sxs-lookup"><span data-stu-id="f2dc8-118">Creating JSON documents</span></span>
* <span data-ttu-id="f2dc8-119">查詢 hello 集合</span><span class="sxs-lookup"><span data-stu-id="f2dc8-119">Querying hello collection</span></span>
* <span data-ttu-id="f2dc8-120">取代文件</span><span class="sxs-lookup"><span data-stu-id="f2dc8-120">Replacing a document</span></span>
* <span data-ttu-id="f2dc8-121">刪除文件</span><span class="sxs-lookup"><span data-stu-id="f2dc8-121">Deleting a document</span></span>
* <span data-ttu-id="f2dc8-122">刪除 hello 節點資料庫</span><span class="sxs-lookup"><span data-stu-id="f2dc8-122">Deleting hello node database</span></span>

<span data-ttu-id="f2dc8-123">沒有時間嗎？</span><span class="sxs-lookup"><span data-stu-id="f2dc8-123">Don't have time?</span></span> <span data-ttu-id="f2dc8-124">別擔心！</span><span class="sxs-lookup"><span data-stu-id="f2dc8-124">Don't worry!</span></span> <span data-ttu-id="f2dc8-125">hello 完整解決方案位於[GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started)。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-125">hello complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span> <span data-ttu-id="f2dc8-126">請參閱[取得 hello 完整解決方案](#GetSolution)快速的指示。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-126">See [Get hello complete solution](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="f2dc8-127">您已經完成 hello Node.js 教學課程之後，請使用 hello 投票按鈕 hello 頂端和底端的這個頁面 toogive 我們意見反應。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-127">After you've completed hello Node.js tutorial, please use hello voting buttons at hello top and bottom of this page toogive us feedback.</span></span> <span data-ttu-id="f2dc8-128">如果您希望我們 toocontact 您直接，認為您的電子郵件地址可用 tooinclude 註解中。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-128">If you'd like us toocontact you directly, feel free tooinclude your email address in your comments.</span></span>

<span data-ttu-id="f2dc8-129">讓我們開始吧！</span><span class="sxs-lookup"><span data-stu-id="f2dc8-129">Now let's get started!</span></span>

## <a name="prerequisites-for-hello-nodejs-tutorial"></a><span data-ttu-id="f2dc8-130">Hello Node.js 教學課程的必要條件</span><span class="sxs-lookup"><span data-stu-id="f2dc8-130">Prerequisites for hello Node.js tutorial</span></span>
<span data-ttu-id="f2dc8-131">請確定您擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="f2dc8-131">Please make sure you have hello following:</span></span>

* <span data-ttu-id="f2dc8-132">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-132">An active Azure account.</span></span> <span data-ttu-id="f2dc8-133">如果您沒有帳戶，您可以註冊 [免費 Azure 試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-133">If you don't have one, you can sign up for a [Free Azure Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
    * <span data-ttu-id="f2dc8-134">或者，您可以使用 hello [Azure Cosmos DB 模擬器](local-emulator.md)本教學課程。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-134">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="f2dc8-135">[Node.js](https://nodejs.org/) v0.10.29 版或更高版本。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-135">[Node.js](https://nodejs.org/) version v0.10.29 or higher.</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="f2dc8-136">步驟 1：建立 Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="f2dc8-136">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="f2dc8-137">讓我們來建立 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-137">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="f2dc8-138">如果您已經有您想要讓 toouse 帳戶，您可以向前跳過[設定 Node.js 應用程式，](#SetupNode)。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-138">If you already have an account you want toouse, you can skip ahead too[Set up your Node.js application](#SetupNode).</span></span> <span data-ttu-id="f2dc8-139">如果您使用 hello Azure Cosmos DB 模擬器，請依照步驟 hello [Azure Cosmos DB 模擬器](local-emulator.md)toosetup hello 模擬器並跳過[設定 Node.js 應用程式，](#SetupNode)。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-139">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Node.js application](#SetupNode).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="f2dc8-140"><a id="SetupNode"></a>步驟 2：設定您的 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="f2dc8-140"><a id="SetupNode"></a>Step 2: Set up your Node.js application</span></span>
1. <span data-ttu-id="f2dc8-141">開啟您偏好的終端機。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-141">Open your favorite terminal.</span></span>
2. <span data-ttu-id="f2dc8-142">找出 hello 資料夾或目錄的 toosave 位置 Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-142">Locate hello folder or directory where you'd like toosave your Node.js application.</span></span>
3. <span data-ttu-id="f2dc8-143">使用下列命令的 hello 中建立兩個空白的 JavaScript 檔案：</span><span class="sxs-lookup"><span data-stu-id="f2dc8-143">Create two empty JavaScript files with hello following commands:</span></span>
   * <span data-ttu-id="f2dc8-144">Windows:</span><span class="sxs-lookup"><span data-stu-id="f2dc8-144">Windows:</span></span>
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * <span data-ttu-id="f2dc8-145">Linux/OS X：</span><span class="sxs-lookup"><span data-stu-id="f2dc8-145">Linux/OS X:</span></span>
     * ```touch app.js```
     * ```touch config.js```
4. <span data-ttu-id="f2dc8-146">透過 npm hello documentdb 模組安裝。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-146">Install hello documentdb module via npm.</span></span> <span data-ttu-id="f2dc8-147">使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="f2dc8-147">Use hello following command:</span></span>
   * ```npm install documentdb --save```

<span data-ttu-id="f2dc8-148">太棒了！</span><span class="sxs-lookup"><span data-stu-id="f2dc8-148">Great!</span></span> <span data-ttu-id="f2dc8-149">現在已完成安裝程式，讓我們開始撰寫一些程式碼。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-149">Now that you've finished setting up, let's start writing some code.</span></span>

## <span data-ttu-id="f2dc8-150"><a id="Config"></a>步驟 3：設定您的應用程式設定</span><span class="sxs-lookup"><span data-stu-id="f2dc8-150"><a id="Config"></a>Step 3: Set your app's configurations</span></span>
<span data-ttu-id="f2dc8-151">在您慣用的文字編輯器中開啟 ```config.js```。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-151">Open ```config.js``` in your favorite text editor.</span></span>

<span data-ttu-id="f2dc8-152">然後、 複製和貼上下列的 hello 程式碼片段，然後```config.endpoint```和```config.primaryKey```tooyour Azure Cosmos DB 端點 uri 與主索引鍵。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-152">Then, copy and paste hello code snippet below and set properties ```config.endpoint``` and ```config.primaryKey``` tooyour Azure Cosmos DB endpoint uri and primary key.</span></span> <span data-ttu-id="f2dc8-153">這兩種這些設定可以在 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-153">Both these configurations can be found in hello [Azure portal](https://portal.azure.com).</span></span>

![Node.js 教學課程-hello 顯示 Azure Cosmos DB 帳戶，與 hello 活躍的 Azure 入口網站的螢幕擷取畫面反白顯示，在 hello Azure Cosmos DB 帳戶刀鋒視窗中，hello URI，主索引鍵和次要金鑰值上 hello 反白顯示反白顯示 hello 金鑰 按鈕索引鍵刀鋒視窗中的節點資料庫][keys]

    // ADD THIS PART tooYOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

<span data-ttu-id="f2dc8-155">複製並貼上 hello ```database id```， ```collection id```，和```JSON documents```tooyour```config```物件下方，設定您```config.endpoint```和```config.authKey```屬性。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-155">Copy and paste hello ```database id```, ```collection id```, and ```JSON documents``` tooyour ```config``` object below where you set your ```config.endpoint``` and ```config.authKey``` properties.</span></span> <span data-ttu-id="f2dc8-156">如果您已經有您想要 toostore 資料庫中的資料，您可以使用 Azure Cosmos DB 的[資料移轉工具](import-data.md)而非新增 hello 文件定義。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-156">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) rather than adding hello document definitions.</span></span>

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

    // ADD THIS PART tooYOUR CODE
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


<span data-ttu-id="f2dc8-157">hello 資料庫、 集合和文件定義做為您的 Azure Cosmos DB ```database id```， ```collection id```，和文件的資料。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-157">hello database, collection, and document definitions will act as your Azure Cosmos DB ```database id```, ```collection id```, and documents' data.</span></span>

<span data-ttu-id="f2dc8-158">最後，匯出您```config```物件，以便您可以在 hello 內參考該```app.js```檔案。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-158">Finally, export your ```config``` object, so that you can reference it within hello ```app.js``` file.</span></span>

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART tooYOUR CODE
    module.exports = config;

## <span data-ttu-id="f2dc8-159"><a id="Connect"></a>步驟 4： 連接 tooan Azure Cosmos DB 帳戶</span><span class="sxs-lookup"><span data-stu-id="f2dc8-159"><a id="Connect"></a> Step 4: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="f2dc8-160">開啟您的空白```app.js```hello 文字編輯器中的檔案。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-160">Open your empty ```app.js``` file in hello text editor.</span></span> <span data-ttu-id="f2dc8-161">複製並貼上下列 tooimport hello 的 hello 程式碼```documentdb```模組，您新建```config```模組。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-161">Copy and paste hello code below tooimport hello ```documentdb``` module and your newly created ```config``` module.</span></span>

    // ADD THIS PART tooYOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

<span data-ttu-id="f2dc8-162">複製並貼上 hello 先前儲存的程式碼 toouse hello```config.endpoint```和```config.primaryKey```toocreate 新 DocumentClient。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-162">Copy and paste hello code toouse hello previously saved ```config.endpoint``` and ```config.primaryKey``` toocreate a new DocumentClient.</span></span>

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART tooYOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

<span data-ttu-id="f2dc8-163">您已經有 hello 程式碼 tooinitialize hello Azure Cosmos DB 用戶端，讓我們看看使用 Azure Cosmos DB 資源。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-163">Now that you have hello code tooinitialize hello Azure Cosmos DB client, let's take a look at working with Azure Cosmos DB resources.</span></span>

## <a name="step-5-create-a-node-database"></a><span data-ttu-id="f2dc8-164">步驟 5：建立節點資料庫</span><span class="sxs-lookup"><span data-stu-id="f2dc8-164">Step 5: Create a Node database</span></span>
<span data-ttu-id="f2dc8-165">將複製並貼 hello tooset hello HTTP 狀態下的程式碼找不到、 hello 資料庫 url 和 hello 集合 url。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-165">Copy and paste hello code below tooset hello HTTP status for Not Found, hello database url, and hello collection url.</span></span> <span data-ttu-id="f2dc8-166">這些 url 會 hello Azure Cosmos DB 用戶端如何找到 hello 正確的資料庫和集合。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-166">These urls are how hello Azure Cosmos DB client will find hello right database and collection.</span></span>

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART tooYOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

<span data-ttu-id="f2dc8-167">A[資料庫](documentdb-resources.md#databases)可以建立使用 hello [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html)函式的 hello **DocumentClient**類別。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-167">A [database](documentdb-resources.md#databases) can be created by using hello [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="f2dc8-168">資料庫是 hello 存放文件分割於各個集合的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-168">A database is hello logical container of document storage partitioned across collections.</span></span>

<span data-ttu-id="f2dc8-169">複製並貼上 hello **getDatabase**函式以 hello hello app.js 檔案中建立新的資料庫```id```hello 中指定```config```物件。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-169">Copy and paste hello **getDatabase** function for creating your new database in hello app.js file with hello ```id``` specified in hello ```config``` object.</span></span> <span data-ttu-id="f2dc8-170">hello 函式檢查時 hello 資料庫以 hello 相同```FamilyRegistry```識別碼不存在。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-170">hello function will check if hello database with hello same ```FamilyRegistry``` id does not already exist.</span></span> <span data-ttu-id="f2dc8-171">如果存在，我們會傳回該資料庫，而不會建立新資料庫。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-171">If it does exist, we'll return that database instead of creating a new one.</span></span>

    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

    // ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="f2dc8-172">複製並貼上下列程式碼 hello，您可以設定 hello **getDatabase**函式 tooadd hello helper 函式**結束**，將會太列印 hello 結束訊息並 hello 呼叫**getDatabase**函式。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-172">Copy and paste hello code below where you set hello **getDatabase** function tooadd hello helper function **exit** that will print hello exit message and hello call too**getDatabase** function.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
    function exit(message) {
        console.log(message);
        console.log('Press any key tooexit');
        process.stdin.setRawMode(true);
        process.stdin.resume();
        process.stdin.on('data', process.exit.bind(process, 0));
    }

    getDatabase()
    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f2dc8-173">在您的終端機中，找出您```app.js```檔，然後執行 hello 命令：```node app.js```</span><span class="sxs-lookup"><span data-stu-id="f2dc8-173">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="f2dc8-174">恭喜！</span><span class="sxs-lookup"><span data-stu-id="f2dc8-174">Congratulations!</span></span> <span data-ttu-id="f2dc8-175">您已成功建立 Azure Cosmos DB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-175">You have successfully created an Azure Cosmos DB database.</span></span>

## <span data-ttu-id="f2dc8-176"><a id="CreateColl"></a>步驟 6：建立集合</span><span class="sxs-lookup"><span data-stu-id="f2dc8-176"><a id="CreateColl"></a>Step 6: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="f2dc8-177">**CreateDocumentCollectionAsync** 會建立具有定價含意的新集合。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-177">**CreateDocumentCollectionAsync** will create a new collection, which has pricing implications.</span></span> <span data-ttu-id="f2dc8-178">如需詳細資訊，請造訪 [定價頁面](https://azure.microsoft.com/pricing/details/cosmos-db/)。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-178">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="f2dc8-179">A[集合](documentdb-resources.md#collections)可以建立使用 hello [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html)函式的 hello **DocumentClient**類別。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-179">A [collection](documentdb-resources.md#collections) can be created by using hello [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="f2dc8-180">集合是 JSON 文件和相關聯 JavaScript 應用程式邏輯的容器。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-180">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="f2dc8-181">複製並貼上 hello **getCollection**函式下方 hello **getDatabase**函式在 hello app.js 檔案 toocreate 您新的集合，以 hello ```id``` hello中指定```config```物件。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-181">Copy and paste hello **getCollection** function underneath hello **getDatabase** function in hello app.js file toocreate your new collection with hello ```id``` specified in hello ```config``` object.</span></span> <span data-ttu-id="f2dc8-182">同樣地，我們會檢查 toomake 確定集合與 hello 相同```FamilyCollection```識別碼不存在。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-182">Again, we'll check toomake sure a collection with hello same ```FamilyCollection``` id does not already exist.</span></span> <span data-ttu-id="f2dc8-183">如果存在，我們會傳回該集合，而不會建立新集合。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-183">If it does exist, we'll return that collection instead of creating a new one.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="f2dc8-184">複製並貼上 hello hello 呼叫下方的程式碼太**getDatabase** tooexecute hello **getCollection**函式。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-184">Copy and paste hello code below hello call too**getDatabase** tooexecute hello **getCollection** function.</span></span>

    getDatabase()

    // ADD THIS PART tooYOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f2dc8-185">在您的終端機中，找出您```app.js```檔，然後執行 hello 命令：```node app.js```</span><span class="sxs-lookup"><span data-stu-id="f2dc8-185">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="f2dc8-186">恭喜！</span><span class="sxs-lookup"><span data-stu-id="f2dc8-186">Congratulations!</span></span> <span data-ttu-id="f2dc8-187">您已成功建立 Azure Cosmos DB 集合。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-187">You have successfully created an Azure Cosmos DB collection.</span></span>

## <span data-ttu-id="f2dc8-188"><a id="CreateDoc"></a>步驟 7：建立文件</span><span class="sxs-lookup"><span data-stu-id="f2dc8-188"><a id="CreateDoc"></a>Step 7: Create a document</span></span>
<span data-ttu-id="f2dc8-189">A[文件](documentdb-resources.md#documents)可以建立使用 hello [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html)函式的 hello **DocumentClient**類別。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-189">A [document](documentdb-resources.md#documents) can be created by using hello [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html) function of hello **DocumentClient** class.</span></span> <span data-ttu-id="f2dc8-190">文件會是使用者定義的 (任意) JSON 內容。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-190">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="f2dc8-191">您現在可以將文件插入 Azure Cosmos DB。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-191">You can now insert a document into Azure Cosmos DB.</span></span>

<span data-ttu-id="f2dc8-192">複製並貼上 hello **getFamilyDocument**函式下方 hello **getCollection**函式建立 hello 文件包含 hello JSON 資料儲存在 hello```config```物件。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-192">Copy and paste hello **getFamilyDocument** function underneath hello **getCollection** function for creating hello documents containing hello JSON data saved in hello ```config``` object.</span></span> <span data-ttu-id="f2dc8-193">同樣地，我們會檢查 toomake 確定文件以 hello 尚未存在相同的識別碼。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-193">Again, we'll check toomake sure a document with hello same id does not already exist.</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="f2dc8-194">複製並貼上 hello hello 呼叫下方的程式碼太**getCollection** tooexecute hello **getFamilyDocument**函式。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-194">Copy and paste hello code below hello call too**getCollection** tooexecute hello **getFamilyDocument** function.</span></span>

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f2dc8-195">在您的終端機中，找出您```app.js```檔，然後執行 hello 命令：```node app.js```</span><span class="sxs-lookup"><span data-stu-id="f2dc8-195">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="f2dc8-196">恭喜！</span><span class="sxs-lookup"><span data-stu-id="f2dc8-196">Congratulations!</span></span> <span data-ttu-id="f2dc8-197">您已成功建立 Azure Cosmos DB 文件。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-197">You have successfully created an Azure Cosmos DB document.</span></span>

![Node.js 教學課程-說明 hello hello 帳戶、 hello 資料庫、 hello 集合和 hello 文件之間的階層式關聯性的圖表-節點資料庫](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <span data-ttu-id="f2dc8-199"><a id="Query"></a>步驟 8︰查詢 Azure Cosmos DB 資源</span><span class="sxs-lookup"><span data-stu-id="f2dc8-199"><a id="Query"></a>Step 8: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="f2dc8-200">Azure Cosmos DB 支援針對儲存於每個集合的 JSON 文件進行[豐富查詢](documentdb-sql-query.md)。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-200">Azure Cosmos DB supports [rich queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span> <span data-ttu-id="f2dc8-201">hello 下列範例程式碼顯示您可以針對 hello 文件集合中執行的查詢。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-201">hello following sample code shows a query that you can run against hello documents in your collection.</span></span>

<span data-ttu-id="f2dc8-202">複製並貼上 hello **queryCollection**函式下方 hello **getFamilyDocument** hello app.js 檔案中的函式。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-202">Copy and paste hello **queryCollection** function underneath hello **getFamilyDocument** function in hello app.js file.</span></span> <span data-ttu-id="f2dc8-203">Azure Cosmos DB 支援類 SQL 查詢，如下所示。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-203">Azure Cosmos DB supports SQL-like queries as shown below.</span></span> <span data-ttu-id="f2dc8-204">如需有關如何建立複雜的查詢的詳細資訊，請參閱 hello[查詢遊樂場](https://www.documentdb.com/sql/demo)和 hello[查詢文件](documentdb-sql-query.md)。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-204">For more information on building complex queries, check out hello [Query Playground](https://www.documentdb.com/sql/demo) and hello [query documentation](documentdb-sql-query.md).</span></span>

                } else {
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
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


<span data-ttu-id="f2dc8-205">hello 下列圖表說明 hello Azure Cosmos DB SQL 查詢語法稱為 hello 集合針對您建立的方式。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-205">hello following diagram illustrates how hello Azure Cosmos DB SQL query syntax is called against hello collection you created.</span></span>

![Node.js 教學課程-圖表說明 hello 範圍和意義 hello 查詢-節點資料庫](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

<span data-ttu-id="f2dc8-207">hello [FROM](documentdb-sql-query.md#FromClause)關鍵字是選擇性的 hello 查詢，因為 Azure Cosmos DB 查詢已設定領域的 tooa 單一集合。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-207">hello [FROM](documentdb-sql-query.md#FromClause) keyword is optional in hello query because Azure Cosmos DB queries are already scoped tooa single collection.</span></span> <span data-ttu-id="f2dc8-208">因此，"FROM Families f" 可以換成 "FROM root r"，或您選擇的任何其他變數名稱。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-208">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="f2dc8-209">Azure Cosmos DB 會推斷家族、 根或 hello 變數名稱您已選擇，依預設參考 hello 目前集合。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-209">Azure Cosmos DB will infer that Families, root, or hello variable name you chose, reference hello current collection by default.</span></span>

<span data-ttu-id="f2dc8-210">複製並貼上 hello hello 呼叫下方的程式碼太**getFamilyDocument** tooexecute hello **queryCollection**函式。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-210">Copy and paste hello code below hello call too**getFamilyDocument** tooexecute hello **queryCollection** function.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART tooYOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f2dc8-211">在您的終端機中，找出您```app.js```檔，然後執行 hello 命令：```node app.js```</span><span class="sxs-lookup"><span data-stu-id="f2dc8-211">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="f2dc8-212">恭喜！</span><span class="sxs-lookup"><span data-stu-id="f2dc8-212">Congratulations!</span></span> <span data-ttu-id="f2dc8-213">您已成功查詢 Azure Cosmos DB 文件。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-213">You have successfully queried Azure Cosmos DB documents.</span></span>

## <span data-ttu-id="f2dc8-214"><a id="ReplaceDocument"></a>步驟 9：取代文件</span><span class="sxs-lookup"><span data-stu-id="f2dc8-214"><a id="ReplaceDocument"></a>Step 9: Replace a document</span></span>
<span data-ttu-id="f2dc8-215">Azure Cosmos DB 支援取代 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-215">Azure Cosmos DB supports replacing JSON documents.</span></span>

<span data-ttu-id="f2dc8-216">複製並貼上 hello **replaceFamilyDocument**函式下方 hello **queryCollection** hello app.js 檔案中的函式。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-216">Copy and paste hello **replaceFamilyDocument** function underneath hello **queryCollection** function in hello app.js file.</span></span>

                    }
                    console.log();
                    resolve(result);
                }
            });
        });
    }

    // ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="f2dc8-217">複製並貼上 hello hello 呼叫下方的程式碼太**queryCollection** tooexecute hello **replaceDocument**函式。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-217">Copy and paste hello code below hello call too**queryCollection** tooexecute hello **replaceDocument** function.</span></span> <span data-ttu-id="f2dc8-218">此外，請加入 hello 程式碼 toocall **queryCollection**再次 tooverify hello 文件已順利變更。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-218">Also, add hello code toocall **queryCollection** again tooverify that hello document had successfully changed.</span></span>

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f2dc8-219">在您的終端機中，找出您```app.js```檔，然後執行 hello 命令：```node app.js```</span><span class="sxs-lookup"><span data-stu-id="f2dc8-219">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="f2dc8-220">恭喜！</span><span class="sxs-lookup"><span data-stu-id="f2dc8-220">Congratulations!</span></span> <span data-ttu-id="f2dc8-221">您已成功取代 Azure Cosmos DB 文件。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-221">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="f2dc8-222"><a id="DeleteDocument"></a>步驟 10︰刪除文件</span><span class="sxs-lookup"><span data-stu-id="f2dc8-222"><a id="DeleteDocument"></a>Step 10: Delete a document</span></span>
<span data-ttu-id="f2dc8-223">Azure Cosmos DB 支援刪除 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-223">Azure Cosmos DB supports deleting JSON documents.</span></span>

<span data-ttu-id="f2dc8-224">複製並貼上 hello **deleteFamilyDocument**函式下方 hello **replaceFamilyDocument**函式。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-224">Copy and paste hello **deleteFamilyDocument** function underneath hello **replaceFamilyDocument** function.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
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

<span data-ttu-id="f2dc8-225">複製並貼上下列 hello 呼叫 toohello 的 hello 程式碼時，第二個**queryCollection** tooexecute hello **deleteDocument**函式。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-225">Copy and paste hello code below hello call toohello second **queryCollection** tooexecute hello **deleteDocument** function.</span></span>

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

<span data-ttu-id="f2dc8-226">在您的終端機中，找出您```app.js```檔，然後執行 hello 命令：```node app.js```</span><span class="sxs-lookup"><span data-stu-id="f2dc8-226">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="f2dc8-227">恭喜！</span><span class="sxs-lookup"><span data-stu-id="f2dc8-227">Congratulations!</span></span> <span data-ttu-id="f2dc8-228">您已成功刪除 Azure Cosmos DB 文件。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-228">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <span data-ttu-id="f2dc8-229"><a id="DeleteDatabase"></a>步驟 11： 刪除 hello 節點資料庫</span><span class="sxs-lookup"><span data-stu-id="f2dc8-229"><a id="DeleteDatabase"></a>Step 11: Delete hello Node database</span></span>
<span data-ttu-id="f2dc8-230">正在刪除 hello 已建立的資料庫將會移除 hello 資料庫和所有子系資源 （集合、 文件）。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-230">Deleting hello created database will remove hello database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="f2dc8-231">複製並貼上 hello**清除**函式下方 hello **deleteFamilyDocument**函式 tooremove hello 資料庫和 hello 子系的所有資源。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-231">Copy and paste hello **cleanup** function underneath hello **deleteFamilyDocument** function tooremove hello database and all hello children resources.</span></span>

                else {
                    resolve(result);
                }
            });
        });
    };

    // ADD THIS PART tooYOUR CODE
    function cleanup() {
        console.log(`Cleaning up by deleting database ${config.database.id}`);

        return new Promise((resolve, reject) => {
            client.deleteDatabase(databaseUrl, (err) => {
                if (err) reject(err)
                else resolve(null);
            });
        });
    }

<span data-ttu-id="f2dc8-232">複製並貼上 hello hello 呼叫下方的程式碼太**deleteFamilyDocument** tooexecute hello**清除**函式。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-232">Copy and paste hello code below hello call too**deleteFamilyDocument** tooexecute hello **cleanup** function.</span></span>

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART tooYOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <span data-ttu-id="f2dc8-233"><a id="Run"></a>步驟 12：一起執行您的 Node.js 應用程式！</span><span class="sxs-lookup"><span data-stu-id="f2dc8-233"><a id="Run"></a>Step 12: Run your Node.js application all together!</span></span>
<span data-ttu-id="f2dc8-234">發生，請呼叫函式的 hello 順序應該看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="f2dc8-234">Altogether, hello sequence for calling your functions should look like this:</span></span>

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

<span data-ttu-id="f2dc8-235">在您的終端機中，找出您```app.js```檔，然後執行 hello 命令：```node app.js```</span><span class="sxs-lookup"><span data-stu-id="f2dc8-235">In your terminal, locate your ```app.js``` file and run hello command: ```node app.js```</span></span>

<span data-ttu-id="f2dc8-236">您應該會看到 hello 取得啟動應用程式的輸出。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-236">You should see hello output of your get started app.</span></span> <span data-ttu-id="f2dc8-237">hello 輸出應符合下列的 hello 範例文字。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-237">hello output should match hello example text below.</span></span>

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
    Press any key tooexit

<span data-ttu-id="f2dc8-238">恭喜！</span><span class="sxs-lookup"><span data-stu-id="f2dc8-238">Congratulations!</span></span> <span data-ttu-id="f2dc8-239">您已建立您已經完成 hello Node.js 教學課程，並將第一個 Azure Cosmos DB 主控台應用程式 ！</span><span class="sxs-lookup"><span data-stu-id="f2dc8-239">You've created you've completed hello Node.js tutorial and have your first Azure Cosmos DB console application!</span></span>

## <span data-ttu-id="f2dc8-240"><a id="GetSolution"></a>取得 hello 完整 Node.js 教學課程解決方案</span><span class="sxs-lookup"><span data-stu-id="f2dc8-240"><a id="GetSolution"></a>Get hello complete Node.js tutorial solution</span></span>
<span data-ttu-id="f2dc8-241">如果您沒有時間 toocomplete hello 步驟在本教學課程中，或只是想 toodownload hello 程式碼，就可以從[GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started)。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-241">If you didn't have time toocomplete hello steps in this tutorial, or just want toodownload hello code, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started).</span></span>

<span data-ttu-id="f2dc8-242">包含所有在本文中的 hello 範例 toorun hello GetStarted 方案，您將需要 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="f2dc8-242">toorun hello GetStarted solution that contains all hello samples in this article, you will need hello following:</span></span>

* <span data-ttu-id="f2dc8-243">[Azure Cosmos DB 帳戶][create-account]。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-243">[Azure Cosmos DB account][create-account].</span></span>
* <span data-ttu-id="f2dc8-244">hello [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) GitHub 上有可用的解決方案。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-244">hello [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="f2dc8-245">安裝 hello **documentdb**透過 npm 模組。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-245">Install hello **documentdb** module via npm.</span></span> <span data-ttu-id="f2dc8-246">使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="f2dc8-246">Use hello following command:</span></span>

* ```npm install documentdb --save```

<span data-ttu-id="f2dc8-247">接下來，在 hello```config.js```檔案，更新 hello config.endpoint 和 config.authKey 值中所述[步驟 3： 設定您的應用程式組態](#Config)。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-247">Next, in hello ```config.js``` file, update hello config.endpoint and config.authKey values as described in [Step 3: Set your app's configurations](#Config).</span></span> 

<span data-ttu-id="f2dc8-248">然後在您的終端機中，找出您```app.js```檔，然後執行 hello 命令： ```node app.js```。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-248">Then in your terminal, locate your ```app.js``` file and run hello command: ```node app.js```.</span></span>

<span data-ttu-id="f2dc8-249">建置就這麼容易，繼續努力！</span><span class="sxs-lookup"><span data-stu-id="f2dc8-249">That's it, build it and you're on your way!</span></span> 

## <a name="next-steps"></a><span data-ttu-id="f2dc8-250">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f2dc8-250">Next steps</span></span>
* <span data-ttu-id="f2dc8-251">需要更複雜的 Node.js 範例嗎？</span><span class="sxs-lookup"><span data-stu-id="f2dc8-251">Want a more complex Node.js sample?</span></span> <span data-ttu-id="f2dc8-252">請參閱[使用 Azure Cosmos DB 來建置 Node.js Web 應用程式](documentdb-nodejs-application.md)。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-252">See [Build a Node.js web application using Azure Cosmos DB](documentdb-nodejs-application.md).</span></span>
* <span data-ttu-id="f2dc8-253">了解如何太[監視 Azure Cosmos DB 帳戶](monitor-accounts.md)。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-253">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="f2dc8-254">執行查詢，根據我們的範例資料集，在 hello[查詢遊樂場](https://www.documentdb.com/sql/demo)。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-254">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="f2dc8-255">深入了解 hello hello hello 開發一節中的程式設計模型[Azure Cosmos DB 文件頁面](https://azure.microsoft.com/documentation/services/documentdb/)。</span><span class="sxs-lookup"><span data-stu-id="f2dc8-255">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
