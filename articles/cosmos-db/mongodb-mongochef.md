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
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="56993-104">使用 MongoChef 搭配 Azure Cosmos DB：適用於 MongoDB 的 API 帳戶</span><span class="sxs-lookup"><span data-stu-id="56993-104">Use MongoChef with an Azure Cosmos DB: API for MongoDB account</span></span>

<span data-ttu-id="56993-105">tooconnect tooan Azure Cosmos DB: MongoDB 帳戶的 API，您必須：</span><span class="sxs-lookup"><span data-stu-id="56993-105">tooconnect tooan Azure Cosmos DB: API for MongoDB account, you must:</span></span>

* <span data-ttu-id="56993-106">下載並安裝 [MongoChef](http://3t.io/mongochef)</span><span class="sxs-lookup"><span data-stu-id="56993-106">Download and install [MongoChef](http://3t.io/mongochef)</span></span>
* <span data-ttu-id="56993-107">具備您的 Azure Cosmos DB：適用於 MongoDB 的 API 帳戶[連接字串](connect-mongodb-account.md)資訊</span><span class="sxs-lookup"><span data-stu-id="56993-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="create-hello-connection-in-mongochef"></a><span data-ttu-id="56993-108">在 MongoChef 中建立 hello 連接</span><span class="sxs-lookup"><span data-stu-id="56993-108">Create hello connection in MongoChef</span></span>
<span data-ttu-id="56993-109">tooadd Azure Cosmos DB: API MongoDB 帳戶 toohello MongoChef 連接管理員 中，執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="56993-109">tooadd your Azure Cosmos DB: API for MongoDB account toohello MongoChef connection manager, perform hello following steps.</span></span>

1. <span data-ttu-id="56993-110">擷取您的 Azure Cosmos DB： 如需使用 hello 指示 MongoDB 連接資訊的應用程式開發介面[這裡](connect-mongodb-account.md)。</span><span class="sxs-lookup"><span data-stu-id="56993-110">Retrieve your Azure Cosmos DB: API for MongoDB connection information using hello instructions [here](connect-mongodb-account.md).</span></span>

    ![Hello 連接字串 刀鋒視窗的螢幕擷取畫面](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. <span data-ttu-id="56993-112">按一下**連接**tooopen hello 連接管理員，然後按一下**新連線**</span><span class="sxs-lookup"><span data-stu-id="56993-112">Click **Connect** tooopen hello Connection Manager, then click **New Connection**</span></span>

    ![Hello MongoChef 連接管理員的螢幕擷取畫面](./media/mongodb-mongochef/ConnectionManager.png)
3. <span data-ttu-id="56993-114">在 hello**新的連接**視窗的 hello**伺服器**索引標籤上，輸入 hello 主機 (FQDN) 的 hello Azure Cosmos DB: MongoDB 帳戶與 hello 通訊埠的應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="56993-114">In hello **New Connection** window, on hello **Server** tab, enter hello HOST (FQDN) of hello Azure Cosmos DB: API for MongoDB account and hello PORT.</span></span>

    ![Hello MongoChef 連接管理員伺服器 索引標籤的螢幕擷取畫面](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. <span data-ttu-id="56993-116">在 hello**新連線**視窗的 hello**驗證**索引標籤上，選擇驗證模式**（MONGODB CR 或 SCARM SHA 1） 的標準**，然後輸入 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="56993-116">In hello **New Connection** window, on hello **Authentication** tab, choose Authentication Mode **Standard (MONGODB-CR or SCARM-SHA-1)** and enter hello USERNAME and PASSWORD.</span></span>  <span data-ttu-id="56993-117">接受 hello 預設驗證 db （管理員），或提供您自己的值。</span><span class="sxs-lookup"><span data-stu-id="56993-117">Accept hello default authentication db (admin) or provide your own value.</span></span>

    ![Hello MongoChef 連線管理員驗證索引標籤的螢幕擷取畫面](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. <span data-ttu-id="56993-119">在 hello**新連線**視窗的 hello **SSL**索引標籤上，檢查 hello**使用 SSL 通訊協定 tooconnect**核取方塊和 hello**接受伺服器自我簽署的 SSL憑證**選項按鈕。</span><span class="sxs-lookup"><span data-stu-id="56993-119">In hello **New Connection** window, on hello **SSL** tab, check hello **Use SSL protocol tooconnect** check box and hello **Accept server self-signed SSL certificates** radio button.</span></span>

    ![Hello MongoChef 連接管理員 SSL 索引標籤的螢幕擷取畫面](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. <span data-ttu-id="56993-121">按一下 hello**測試連接**按鈕 toovalidate hello 連接資訊，請按一下**確定**tooreturn toohello 新連線 視窗，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="56993-121">Click hello **Test Connection** button toovalidate hello connection information, click **OK** tooreturn toohello New Connection window, and then click **Save**.</span></span>

    ![Hello MongoChef 測試連線 視窗的螢幕擷取畫面](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-toocreate-a-database-collection-and-documents"></a><span data-ttu-id="56993-123">使用 MongoChef toocreate 資料庫、 集合和文件</span><span class="sxs-lookup"><span data-stu-id="56993-123">Use MongoChef toocreate a database, collection, and documents</span></span>
<span data-ttu-id="56993-124">toocreate 資料庫、 集合和文件使用 MongoChef，執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="56993-124">toocreate a database, collection, and documents using MongoChef, perform hello following steps.</span></span>

1. <span data-ttu-id="56993-125">在**連線管理員**，反白顯示 hello 連線，然後按一下**連接**。</span><span class="sxs-lookup"><span data-stu-id="56993-125">In **Connection Manager**, highlight hello connection and click **Connect**.</span></span>

    ![Hello MongoChef 連接管理員的螢幕擷取畫面](./media/mongodb-mongochef/ConnectToAccount.png)
2. <span data-ttu-id="56993-127">以滑鼠右鍵按一下 hello 主機，然後選擇**將資料庫加入**。</span><span class="sxs-lookup"><span data-stu-id="56993-127">Right click hello host and choose **Add Database**.</span></span>  <span data-ttu-id="56993-128">提供資料庫名稱，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="56993-128">Provide a database name and click **OK**.</span></span>

    ![Hello MongoChef 新增資料庫選項的螢幕擷取畫面](./media/mongodb-mongochef/AddDatabase1.png)
3. <span data-ttu-id="56993-130">以滑鼠右鍵按一下 hello 資料庫，然後選擇**新增集合**。</span><span class="sxs-lookup"><span data-stu-id="56993-130">Right click hello database and choose **Add Collection**.</span></span>  <span data-ttu-id="56993-131">提供集合名稱，然後按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="56993-131">Provide a collection name and click **Create**.</span></span>

    ![Hello MongoChef 新增集合選項的螢幕擷取畫面](./media/mongodb-mongochef/AddCollection.png)
4. <span data-ttu-id="56993-133">按一下 hello**集合**功能表項目，然後按一下**加入文件**。</span><span class="sxs-lookup"><span data-stu-id="56993-133">Click hello **Collection** menu item, then click **Add Document**.</span></span>

    ![Hello MongoChef 加入文件功能表項目的螢幕擷取畫面](./media/mongodb-mongochef/AddDocument1.png)
5. <span data-ttu-id="56993-135">在 hello 加入文件 對話方塊中，貼上下列 hello，然後按一下**加入文件**。</span><span class="sxs-lookup"><span data-stu-id="56993-135">In hello Add Document dialog, paste hello following and then click **Add Document**.</span></span>

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
6. <span data-ttu-id="56993-136">增加其他文件以 hello 內容之後此時間。</span><span class="sxs-lookup"><span data-stu-id="56993-136">Add another document, this time with hello following content.</span></span>

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
7. <span data-ttu-id="56993-137">執行範例查詢。</span><span class="sxs-lookup"><span data-stu-id="56993-137">Execute a sample query.</span></span> <span data-ttu-id="56993-138">例如，系列 hello 姓氏 'Andersen' 傳回 hello 父系和狀態欄位與搜尋。</span><span class="sxs-lookup"><span data-stu-id="56993-138">For example, search for families with hello last name 'Andersen' and return hello parents and state fields.</span></span>

    ![Mongo Chef 查詢結果的螢幕擷取畫面](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a><span data-ttu-id="56993-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="56993-140">Next steps</span></span>
* <span data-ttu-id="56993-141">瀏覽 Azure Cosmos DB：適用於 MongoDB 的 API [範例](mongodb-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="56993-141">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
