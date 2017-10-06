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
# <a name="nodejs-tutorial-use-hello-documentdb-api-in-azure-cosmos-db-toocreate-a-nodejs-console-application"></a>Node.js 教學課程： Azure Cosmos DB toocreate Node.js 主控台應用程式中的使用 hello DocumentDB API
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js for MongoDB](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

 褖畫惎 toohello hello Azure Cosmos DB Node.js SDK for Node.js 教學課程 ！ 完成本教學課程之後，您將會有一個主控台應用程式，可用來建立和查詢 Azure Cosmos DB 資源。

本文將討論：

* 建立及連接 tooan Azure Cosmos DB 帳戶
* 設定您的應用程式
* 建立節點資料庫
* 建立集合
* 建立 JSON 文件
* 查詢 hello 集合
* 取代文件
* 刪除文件
* 刪除 hello 節點資料庫

沒有時間嗎？ 別擔心！ hello 完整解決方案位於[GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started)。 請參閱[取得 hello 完整解決方案](#GetSolution)快速的指示。

您已經完成 hello Node.js 教學課程之後，請使用 hello 投票按鈕 hello 頂端和底端的這個頁面 toogive 我們意見反應。 如果您希望我們 toocontact 您直接，認為您的電子郵件地址可用 tooinclude 註解中。

讓我們開始吧！

## <a name="prerequisites-for-hello-nodejs-tutorial"></a>Hello Node.js 教學課程的必要條件
請確定您擁有 hello 下列：

* 使用中的 Azure 帳戶。 如果您沒有帳戶，您可以註冊 [免費 Azure 試用](https://azure.microsoft.com/pricing/free-trial/)。
    * 或者，您可以使用 hello [Azure Cosmos DB 模擬器](local-emulator.md)本教學課程。
* [Node.js](https://nodejs.org/) v0.10.29 版或更高版本。

## <a name="step-1-create-an-azure-cosmos-db-account"></a>步驟 1：建立 Azure Cosmos DB 帳戶
讓我們來建立 Azure Cosmos DB 帳戶。 如果您已經有您想要讓 toouse 帳戶，您可以向前跳過[設定 Node.js 應用程式，](#SetupNode)。 如果您使用 hello Azure Cosmos DB 模擬器，請依照步驟 hello [Azure Cosmos DB 模擬器](local-emulator.md)toosetup hello 模擬器並跳過[設定 Node.js 應用程式，](#SetupNode)。

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupNode"></a>步驟 2：設定您的 Node.js 應用程式
1. 開啟您偏好的終端機。
2. 找出 hello 資料夾或目錄的 toosave 位置 Node.js 應用程式。
3. 使用下列命令的 hello 中建立兩個空白的 JavaScript 檔案：
   * Windows:
     * ```fsutil file createnew app.js 0```
     * ```fsutil file createnew config.js 0```
   * Linux/OS X：
     * ```touch app.js```
     * ```touch config.js```
4. 透過 npm hello documentdb 模組安裝。 使用下列命令的 hello:
   * ```npm install documentdb --save```

太棒了！ 現在已完成安裝程式，讓我們開始撰寫一些程式碼。

## <a id="Config"></a>步驟 3：設定您的應用程式設定
在您慣用的文字編輯器中開啟 ```config.js```。

然後、 複製和貼上下列的 hello 程式碼片段，然後```config.endpoint```和```config.primaryKey```tooyour Azure Cosmos DB 端點 uri 與主索引鍵。 這兩種這些設定可以在 hello [Azure 入口網站](https://portal.azure.com)。

![Node.js 教學課程-hello 顯示 Azure Cosmos DB 帳戶，與 hello 活躍的 Azure 入口網站的螢幕擷取畫面反白顯示，在 hello Azure Cosmos DB 帳戶刀鋒視窗中，hello URI，主索引鍵和次要金鑰值上 hello 反白顯示反白顯示 hello 金鑰 按鈕索引鍵刀鋒視窗中的節點資料庫][keys]

    // ADD THIS PART tooYOUR CODE
    var config = {}

    config.endpoint = "~your Azure Cosmos DB endpoint uri here~";
    config.primaryKey = "~your primary key here~";

複製並貼上 hello ```database id```， ```collection id```，和```JSON documents```tooyour```config```物件下方，設定您```config.endpoint```和```config.authKey```屬性。 如果您已經有您想要 toostore 資料庫中的資料，您可以使用 Azure Cosmos DB 的[資料移轉工具](import-data.md)而非新增 hello 文件定義。

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


hello 資料庫、 集合和文件定義做為您的 Azure Cosmos DB ```database id```， ```collection id```，和文件的資料。

最後，匯出您```config```物件，以便您可以在 hello 內參考該```app.js```檔案。

            },
            "isRegistered": false
        }
    };

    // ADD THIS PART tooYOUR CODE
    module.exports = config;

## <a id="Connect"></a>步驟 4： 連接 tooan Azure Cosmos DB 帳戶
開啟您的空白```app.js```hello 文字編輯器中的檔案。 複製並貼上下列 tooimport hello 的 hello 程式碼```documentdb```模組，您新建```config```模組。

    // ADD THIS PART tooYOUR CODE
    "use strict";

    var documentClient = require("documentdb").DocumentClient;
    var config = require("./config");
    var url = require('url');

複製並貼上 hello 先前儲存的程式碼 toouse hello```config.endpoint```和```config.primaryKey```toocreate 新 DocumentClient。

    var config = require("./config");
    var url = require('url');

    // ADD THIS PART tooYOUR CODE
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

您已經有 hello 程式碼 tooinitialize hello Azure Cosmos DB 用戶端，讓我們看看使用 Azure Cosmos DB 資源。

## <a name="step-5-create-a-node-database"></a>步驟 5：建立節點資料庫
將複製並貼 hello tooset hello HTTP 狀態下的程式碼找不到、 hello 資料庫 url 和 hello 集合 url。 這些 url 會 hello Azure Cosmos DB 用戶端如何找到 hello 正確的資料庫和集合。

    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });

    // ADD THIS PART tooYOUR CODE
    var HttpStatusCodes = { NOTFOUND: 404 };
    var databaseUrl = `dbs/${config.database.id}`;
    var collectionUrl = `${databaseUrl}/colls/${config.collection.id}`;

A[資料庫](documentdb-resources.md#databases)可以建立使用 hello [createDatabase](https://azure.github.io/azure-documentdb-node/DocumentClient.html)函式的 hello **DocumentClient**類別。 資料庫是 hello 存放文件分割於各個集合的邏輯容器。

複製並貼上 hello **getDatabase**函式以 hello hello app.js 檔案中建立新的資料庫```id```hello 中指定```config```物件。 hello 函式檢查時 hello 資料庫以 hello 相同```FamilyRegistry```識別碼不存在。 如果存在，我們會傳回該資料庫，而不會建立新資料庫。

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

複製並貼上下列程式碼 hello，您可以設定 hello **getDatabase**函式 tooadd hello helper 函式**結束**，將會太列印 hello 結束訊息並 hello 呼叫**getDatabase**函式。

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

在您的終端機中，找出您```app.js```檔，然後執行 hello 命令：```node app.js```

恭喜！ 您已成功建立 Azure Cosmos DB 資料庫。

## <a id="CreateColl"></a>步驟 6：建立集合
> [!WARNING]
> **CreateDocumentCollectionAsync** 會建立具有定價含意的新集合。 如需詳細資訊，請造訪 [定價頁面](https://azure.microsoft.com/pricing/details/cosmos-db/)。
> 
> 

A[集合](documentdb-resources.md#collections)可以建立使用 hello [createCollection](https://azure.github.io/azure-documentdb-node/DocumentClient.html)函式的 hello **DocumentClient**類別。 集合是 JSON 文件和相關聯 JavaScript 應用程式邏輯的容器。

複製並貼上 hello **getCollection**函式下方 hello **getDatabase**函式在 hello app.js 檔案 toocreate 您新的集合，以 hello ```id``` hello中指定```config```物件。 同樣地，我們會檢查 toomake 確定集合與 hello 相同```FamilyCollection```識別碼不存在。 如果存在，我們會傳回該集合，而不會建立新集合。

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

複製並貼上 hello hello 呼叫下方的程式碼太**getDatabase** tooexecute hello **getCollection**函式。

    getDatabase()

    // ADD THIS PART tooYOUR CODE
    .then(() => getCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

在您的終端機中，找出您```app.js```檔，然後執行 hello 命令：```node app.js```

恭喜！ 您已成功建立 Azure Cosmos DB 集合。

## <a id="CreateDoc"></a>步驟 7：建立文件
A[文件](documentdb-resources.md#documents)可以建立使用 hello [createDocument](https://azure.github.io/azure-documentdb-node/DocumentClient.html)函式的 hello **DocumentClient**類別。 文件會是使用者定義的 (任意) JSON 內容。 您現在可以將文件插入 Azure Cosmos DB。

複製並貼上 hello **getFamilyDocument**函式下方 hello **getCollection**函式建立 hello 文件包含 hello JSON 資料儲存在 hello```config```物件。 同樣地，我們會檢查 toomake 確定文件以 hello 尚未存在相同的識別碼。

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

複製並貼上 hello hello 呼叫下方的程式碼太**getCollection** tooexecute hello **getFamilyDocument**函式。

    getDatabase()
    .then(() => getCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

在您的終端機中，找出您```app.js```檔，然後執行 hello 命令：```node app.js```

恭喜！ 您已成功建立 Azure Cosmos DB 文件。

![Node.js 教學課程-說明 hello hello 帳戶、 hello 資料庫、 hello 集合和 hello 文件之間的階層式關聯性的圖表-節點資料庫](./media/documentdb-nodejs-get-started/node-js-tutorial-cosmos-db-account.png)

## <a id="Query"></a>步驟 8︰查詢 Azure Cosmos DB 資源
Azure Cosmos DB 支援針對儲存於每個集合的 JSON 文件進行[豐富查詢](documentdb-sql-query.md)。 hello 下列範例程式碼顯示您可以針對 hello 文件集合中執行的查詢。

複製並貼上 hello **queryCollection**函式下方 hello **getFamilyDocument** hello app.js 檔案中的函式。 Azure Cosmos DB 支援類 SQL 查詢，如下所示。 如需有關如何建立複雜的查詢的詳細資訊，請參閱 hello[查詢遊樂場](https://www.documentdb.com/sql/demo)和 hello[查詢文件](documentdb-sql-query.md)。

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


hello 下列圖表說明 hello Azure Cosmos DB SQL 查詢語法稱為 hello 集合針對您建立的方式。

![Node.js 教學課程-圖表說明 hello 範圍和意義 hello 查詢-節點資料庫](./media/documentdb-nodejs-get-started/node-js-tutorial-collection-documents.png)

hello [FROM](documentdb-sql-query.md#FromClause)關鍵字是選擇性的 hello 查詢，因為 Azure Cosmos DB 查詢已設定領域的 tooa 單一集合。 因此，"FROM Families f" 可以換成 "FROM root r"，或您選擇的任何其他變數名稱。 Azure Cosmos DB 會推斷家族、 根或 hello 變數名稱您已選擇，依預設參考 hello 目前集合。

複製並貼上 hello hello 呼叫下方的程式碼太**getFamilyDocument** tooexecute hello **queryCollection**函式。

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))

    // ADD THIS PART tooYOUR CODE
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

在您的終端機中，找出您```app.js```檔，然後執行 hello 命令：```node app.js```

恭喜！ 您已成功查詢 Azure Cosmos DB 文件。

## <a id="ReplaceDocument"></a>步驟 9：取代文件
Azure Cosmos DB 支援取代 JSON 文件。

複製並貼上 hello **replaceFamilyDocument**函式下方 hello **queryCollection** hello app.js 檔案中的函式。

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

複製並貼上 hello hello 呼叫下方的程式碼太**queryCollection** tooexecute hello **replaceDocument**函式。 此外，請加入 hello 程式碼 toocall **queryCollection**再次 tooverify hello 文件已順利變更。

    .then(() => getFamilyDocument(config.documents.Andersen))
    .then(() => getFamilyDocument(config.documents.Wakefield))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

在您的終端機中，找出您```app.js```檔，然後執行 hello 命令：```node app.js```

恭喜！ 您已成功取代 Azure Cosmos DB 文件。

## <a id="DeleteDocument"></a>步驟 10︰刪除文件
Azure Cosmos DB 支援刪除 JSON 文件。

複製並貼上 hello **deleteFamilyDocument**函式下方 hello **replaceFamilyDocument**函式。

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

複製並貼上下列 hello 呼叫 toohello 的 hello 程式碼時，第二個**queryCollection** tooexecute hello **deleteDocument**函式。

    .then(() => queryCollection())
    .then(() => replaceFamilyDocument(config.documents.Andersen))
    .then(() => queryCollection())

    // ADD THIS PART tooYOUR CODE
    .then(() => deleteFamilyDocument(config.documents.Andersen))
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

在您的終端機中，找出您```app.js```檔，然後執行 hello 命令：```node app.js```

恭喜！ 您已成功刪除 Azure Cosmos DB 文件。

## <a id="DeleteDatabase"></a>步驟 11： 刪除 hello 節點資料庫
正在刪除 hello 已建立的資料庫將會移除 hello 資料庫和所有子系資源 （集合、 文件）。

複製並貼上 hello**清除**函式下方 hello **deleteFamilyDocument**函式 tooremove hello 資料庫和 hello 子系的所有資源。

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

複製並貼上 hello hello 呼叫下方的程式碼太**deleteFamilyDocument** tooexecute hello**清除**函式。

    .then(() => deleteFamilyDocument(config.documents.Andersen))

    // ADD THIS PART tooYOUR CODE
    .then(() => cleanup())
    // ENDS HERE

    .then(() => { exit(`Completed successfully`); })
    .catch((error) => { exit(`Completed with error ${JSON.stringify(error)}`) });

## <a id="Run"></a>步驟 12：一起執行您的 Node.js 應用程式！
發生，請呼叫函式的 hello 順序應該看起來像這樣：

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

在您的終端機中，找出您```app.js```檔，然後執行 hello 命令：```node app.js```

您應該會看到 hello 取得啟動應用程式的輸出。 hello 輸出應符合下列的 hello 範例文字。

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

恭喜！ 您已建立您已經完成 hello Node.js 教學課程，並將第一個 Azure Cosmos DB 主控台應用程式 ！

## <a id="GetSolution"></a>取得 hello 完整 Node.js 教學課程解決方案
如果您沒有時間 toocomplete hello 步驟在本教學課程中，或只是想 toodownload hello 程式碼，就可以從[GitHub](https://github.com/Azure-Samples/documentdb-node-getting-started)。

包含所有在本文中的 hello 範例 toorun hello GetStarted 方案，您將需要 hello 下列：

* [Azure Cosmos DB 帳戶][create-account]。
* hello [GetStarted](https://github.com/Azure-Samples/documentdb-node-getting-started) GitHub 上有可用的解決方案。

安裝 hello **documentdb**透過 npm 模組。 使用下列命令的 hello:

* ```npm install documentdb --save```

接下來，在 hello```config.js```檔案，更新 hello config.endpoint 和 config.authKey 值中所述[步驟 3： 設定您的應用程式組態](#Config)。 

然後在您的終端機中，找出您```app.js```檔，然後執行 hello 命令： ```node app.js```。

建置就這麼容易，繼續努力！ 

## <a name="next-steps"></a>後續步驟
* 需要更複雜的 Node.js 範例嗎？ 請參閱[使用 Azure Cosmos DB 來建置 Node.js Web 應用程式](documentdb-nodejs-application.md)。
* 了解如何太[監視 Azure Cosmos DB 帳戶](monitor-accounts.md)。
* 執行查詢，根據我們的範例資料集，在 hello[查詢遊樂場](https://www.documentdb.com/sql/demo)。
* 深入了解 hello hello hello 開發一節中的程式設計模型[Azure Cosmos DB 文件頁面](https://azure.microsoft.com/documentation/services/documentdb/)。

[create-account]: create-documentdb-dotnet.md#create-account
[keys]: media/documentdb-nodejs-get-started/node-js-tutorial-keys.png
