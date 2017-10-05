---
title: "使用 MongoChef 連絡 Azure Cosmos DB | Microsoft Docs"
description: "了解如何使用 MongoChef 搭配 Azure Cosmos DB：適用於 MongoDB 的 API 帳戶"
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
ms.openlocfilehash: 54c9799bd646b827f602e2ea2f9a15a4fc853f00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="dfbfa-104">使用 MongoChef 搭配 Azure Cosmos DB：適用於 MongoDB 的 API 帳戶</span><span class="sxs-lookup"><span data-stu-id="dfbfa-104">Use MongoChef with an Azure Cosmos DB: API for MongoDB account</span></span>

<span data-ttu-id="dfbfa-105">若要連線到 Azure Cosmos DB：適用於 MongoDB 的 API 帳戶，您必須︰</span><span class="sxs-lookup"><span data-stu-id="dfbfa-105">To connect to an Azure Cosmos DB: API for MongoDB account, you must:</span></span>

* <span data-ttu-id="dfbfa-106">下載並安裝 [MongoChef](http://3t.io/mongochef)</span><span class="sxs-lookup"><span data-stu-id="dfbfa-106">Download and install [MongoChef](http://3t.io/mongochef)</span></span>
* <span data-ttu-id="dfbfa-107">具備您的 Azure Cosmos DB：適用於 MongoDB 的 API 帳戶[連接字串](connect-mongodb-account.md)資訊</span><span class="sxs-lookup"><span data-stu-id="dfbfa-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="create-the-connection-in-mongochef"></a><span data-ttu-id="dfbfa-108">在 MongoChef 中建立連接</span><span class="sxs-lookup"><span data-stu-id="dfbfa-108">Create the connection in MongoChef</span></span>
<span data-ttu-id="dfbfa-109">若要將 Azure Cosmos DB：適用於 MongoDB 的 API 帳戶新增至 MongoChef 連線管理員，請執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="dfbfa-109">To add your Azure Cosmos DB: API for MongoDB account to the MongoChef connection manager, perform the following steps.</span></span>

1. <span data-ttu-id="dfbfa-110">使用[這裡](connect-mongodb-account.md)的指示來擷取 Azure Cosmos DB：適用於 MongoDB 的 API 的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="dfbfa-110">Retrieve your Azure Cosmos DB: API for MongoDB connection information using the instructions [here](connect-mongodb-account.md).</span></span>

    ![[連接字串] 刀鋒視窗的螢幕擷取畫面](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. <span data-ttu-id="dfbfa-112">按一下 [連接] 以開啟 [連接管理員]，然後按一下 [新增連線]</span><span class="sxs-lookup"><span data-stu-id="dfbfa-112">Click **Connect** to open the Connection Manager, then click **New Connection**</span></span>

    ![[MongoChef 連接管理員] 的螢幕擷取畫面](./media/mongodb-mongochef/ConnectionManager.png)
3. <span data-ttu-id="dfbfa-114">在 [新增連線]視窗中，在 [伺服器] 索引標籤上輸入 Azure Cosmos DB：適用於 MongoDB 的 API 帳戶的主機 (FQDN) 和連接埠。</span><span class="sxs-lookup"><span data-stu-id="dfbfa-114">In the **New Connection** window, on the **Server** tab, enter the HOST (FQDN) of the Azure Cosmos DB: API for MongoDB account and the PORT.</span></span>

    ![[MongoChef 連接管理員伺服器] 索引標籤的螢幕擷取畫面](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. <span data-ttu-id="dfbfa-116">在 [新增連線] 視窗中，請在 [驗證] 索引標籤上選擇驗證模式 [標準 (MONGODB-CR 或 SCARM-SHA-1)]，並輸入使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="dfbfa-116">In the **New Connection** window, on the **Authentication** tab, choose Authentication Mode **Standard (MONGODB-CR or SCARM-SHA-1)** and enter the USERNAME and PASSWORD.</span></span>  <span data-ttu-id="dfbfa-117">接受預設的驗證資料庫 (管理員)，或提供您自己的值。</span><span class="sxs-lookup"><span data-stu-id="dfbfa-117">Accept the default authentication db (admin) or provide your own value.</span></span>

    ![[MongoChef 連接管理員驗證] 索引標籤的螢幕擷取畫面](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. <span data-ttu-id="dfbfa-119">在 [新增連接] 視窗的 [SSL] 索引標籤上，勾選 [使用 SSL 通訊協定連接] 核取方塊和 [接受自我簽署的 SSL 憑證] 選項按鈕。</span><span class="sxs-lookup"><span data-stu-id="dfbfa-119">In the **New Connection** window, on the **SSL** tab, check the **Use SSL protocol to connect** check box and the **Accept server self-signed SSL certificates** radio button.</span></span>

    ![[MongoChef 連接管理員 SSL] 索引標籤的螢幕擷取畫面](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. <span data-ttu-id="dfbfa-121">按一下 [測試連接] 按鈕以驗證連接資訊，按一下 [確定] 以返回 [新增連線] 視窗，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="dfbfa-121">Click the **Test Connection** button to validate the connection information, click **OK** to return to the New Connection window, and then click **Save**.</span></span>

    ![[MongoChef 測試連接] 視窗的螢幕擷取畫面](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-to-create-a-database-collection-and-documents"></a><span data-ttu-id="dfbfa-123">使用 MongoChef 以建立資料庫、集合和文件</span><span class="sxs-lookup"><span data-stu-id="dfbfa-123">Use MongoChef to create a database, collection, and documents</span></span>
<span data-ttu-id="dfbfa-124">若要使用 MongoChef 建立資料庫、集合和文件，請執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="dfbfa-124">To create a database, collection, and documents using MongoChef, perform the following steps.</span></span>

1. <span data-ttu-id="dfbfa-125">在 [連接管理員] 中，反白顯示連接，然後按一下 [連接]。</span><span class="sxs-lookup"><span data-stu-id="dfbfa-125">In **Connection Manager**, highlight the connection and click **Connect**.</span></span>

    ![[MongoChef 連接管理員] 的螢幕擷取畫面](./media/mongodb-mongochef/ConnectToAccount.png)
2. <span data-ttu-id="dfbfa-127">以滑鼠右鍵按一下主機，然後選擇 [新增資料庫] 。</span><span class="sxs-lookup"><span data-stu-id="dfbfa-127">Right click the host and choose **Add Database**.</span></span>  <span data-ttu-id="dfbfa-128">提供資料庫名稱，然後按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="dfbfa-128">Provide a database name and click **OK**.</span></span>

    ![[MongoChef 新增資料庫] 選項的螢幕擷取畫面](./media/mongodb-mongochef/AddDatabase1.png)
3. <span data-ttu-id="dfbfa-130">以滑鼠右鍵按一下資料庫，然後選擇 [新增集合] 。</span><span class="sxs-lookup"><span data-stu-id="dfbfa-130">Right click the database and choose **Add Collection**.</span></span>  <span data-ttu-id="dfbfa-131">提供集合名稱，然後按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="dfbfa-131">Provide a collection name and click **Create**.</span></span>

    ![[MongoChef 新增集合] 選項的螢幕擷取畫面](./media/mongodb-mongochef/AddCollection.png)
4. <span data-ttu-id="dfbfa-133">按一下 [集合] 功能表項目，然後按一下 [新增文件]。</span><span class="sxs-lookup"><span data-stu-id="dfbfa-133">Click the **Collection** menu item, then click **Add Document**.</span></span>

    ![[MongoChef 新增文件] 功能表項目的螢幕擷取畫面](./media/mongodb-mongochef/AddDocument1.png)
5. <span data-ttu-id="dfbfa-135">在 [新增文件] 對話方塊中，貼上下列項目，然後按一下 [新增文件] 。</span><span class="sxs-lookup"><span data-stu-id="dfbfa-135">In the Add Document dialog, paste the following and then click **Add Document**.</span></span>

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
6. <span data-ttu-id="dfbfa-136">新增其他文件，這次使用下列內容。</span><span class="sxs-lookup"><span data-stu-id="dfbfa-136">Add another document, this time with the following content.</span></span>

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
7. <span data-ttu-id="dfbfa-137">執行範例查詢。</span><span class="sxs-lookup"><span data-stu-id="dfbfa-137">Execute a sample query.</span></span> <span data-ttu-id="dfbfa-138">例如，搜尋姓氏 'Andersen' 的家族，並傳回父母和州欄位。</span><span class="sxs-lookup"><span data-stu-id="dfbfa-138">For example, search for families with the last name 'Andersen' and return the parents and state fields.</span></span>

    ![Mongo Chef 查詢結果的螢幕擷取畫面](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a><span data-ttu-id="dfbfa-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dfbfa-140">Next steps</span></span>
* <span data-ttu-id="dfbfa-141">瀏覽 Azure Cosmos DB：適用於 MongoDB 的 API [範例](mongodb-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="dfbfa-141">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
