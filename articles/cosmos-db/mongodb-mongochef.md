---
title: "aaaUse for Azure Cosmos DB MongoChef |Microsoft 文件"
description: "深入了解如何搭配 Azure Cosmos DB MongoChef toouse: MongoDB 帳戶的 API"
keywords: MongoChef
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 4b047797b231c34ccc6f2ed02416525c6228d596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a>使用 MongoChef 搭配 Azure Cosmos DB：適用於 MongoDB 的 API 帳戶

tooconnect tooan Azure Cosmos DB: MongoDB 帳戶的 API，您必須：

* 下載並安裝 [MongoChef](http://3t.io/mongochef)
* 具備您的 Azure Cosmos DB：適用於 MongoDB 的 API 帳戶[連接字串](connect-mongodb-account.md)資訊

## <a name="create-hello-connection-in-mongochef"></a>在 MongoChef 中建立 hello 連接
tooadd Azure Cosmos DB: API MongoDB 帳戶 toohello MongoChef 連接管理員 中，執行下列步驟的 hello。

1. 擷取您的 Azure Cosmos DB： 如需使用 hello 指示 MongoDB 連接資訊的應用程式開發介面[這裡](connect-mongodb-account.md)。

    ![Hello 連接字串 刀鋒視窗的螢幕擷取畫面](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. 按一下**連接**tooopen hello 連接管理員，然後按一下**新連線**

    ![Hello MongoChef 連接管理員的螢幕擷取畫面](./media/mongodb-mongochef/ConnectionManager.png)
3. 在 hello**新的連接**視窗的 hello**伺服器**索引標籤上，輸入 hello 主機 (FQDN) 的 hello Azure Cosmos DB: MongoDB 帳戶與 hello 通訊埠的應用程式開發介面。

    ![Hello MongoChef 連接管理員伺服器 索引標籤的螢幕擷取畫面](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. 在 hello**新連線**視窗的 hello**驗證**索引標籤上，選擇驗證模式**（MONGODB CR 或 SCARM SHA 1） 的標準**，然後輸入 hello 使用者名稱和密碼。  接受 hello 預設驗證 db （管理員），或提供您自己的值。

    ![Hello MongoChef 連線管理員驗證索引標籤的螢幕擷取畫面](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. 在 hello**新連線**視窗的 hello **SSL**索引標籤上，檢查 hello**使用 SSL 通訊協定 tooconnect**核取方塊和 hello**接受伺服器自我簽署的 SSL憑證**選項按鈕。

    ![Hello MongoChef 連接管理員 SSL 索引標籤的螢幕擷取畫面](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. 按一下 hello**測試連接**按鈕 toovalidate hello 連接資訊，請按一下**確定**tooreturn toohello 新連線 視窗，然後按一下**儲存**。

    ![Hello MongoChef 測試連線 視窗的螢幕擷取畫面](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-toocreate-a-database-collection-and-documents"></a>使用 MongoChef toocreate 資料庫、 集合和文件
toocreate 資料庫、 集合和文件使用 MongoChef，執行下列步驟的 hello。

1. 在**連線管理員**，反白顯示 hello 連線，然後按一下**連接**。

    ![Hello MongoChef 連接管理員的螢幕擷取畫面](./media/mongodb-mongochef/ConnectToAccount.png)
2. 以滑鼠右鍵按一下 hello 主機，然後選擇**將資料庫加入**。  提供資料庫名稱，然後按一下 [確定] 。

    ![Hello MongoChef 新增資料庫選項的螢幕擷取畫面](./media/mongodb-mongochef/AddDatabase1.png)
3. 以滑鼠右鍵按一下 hello 資料庫，然後選擇**新增集合**。  提供集合名稱，然後按一下 [建立] 。

    ![Hello MongoChef 新增集合選項的螢幕擷取畫面](./media/mongodb-mongochef/AddCollection.png)
4. 按一下 hello**集合**功能表項目，然後按一下**加入文件**。

    ![Hello MongoChef 加入文件功能表項目的螢幕擷取畫面](./media/mongodb-mongochef/AddDocument1.png)
5. 在 hello 加入文件 對話方塊中，貼上下列 hello，然後按一下**加入文件**。

        {
        "_id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
               { "firstName": "Thomas" },
               { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "isRegistered": true
        }
6. 增加其他文件以 hello 內容之後此時間。

        {
        "_id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam",
                 "givenName": "Jesse",
                "gender": "female", "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            {
                "familyName": "Miller",
                 "givenName": "Lisa",
                 "gender": "female",
                 "grade": 8 }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
        }
7. 執行範例查詢。 例如，系列 hello 姓氏 'Andersen' 傳回 hello 父系和狀態欄位與搜尋。

    ![Mongo Chef 查詢結果的螢幕擷取畫面](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a>後續步驟
* 瀏覽 Azure Cosmos DB：適用於 MongoDB 的 API [範例](mongodb-samples.md)。
