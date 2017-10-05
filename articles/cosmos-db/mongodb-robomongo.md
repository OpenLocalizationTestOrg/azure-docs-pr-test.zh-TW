---
title: "使用 Robomongo 連絡 Azure Cosmos DB | Microsoft Docs"
description: "了解如何使用 Robomongo 搭配 Azure Cosmos DB：適用於 MongoDB 的 API 帳戶"
keywords: robomongo
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
ms.openlocfilehash: 8983594776a1bbe413a6d7cf2cd518f0e327648a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="d49be-104">使用 Robomongo 搭配 Azure Cosmos DB：適用於 MongoDB 的 API 帳戶</span><span class="sxs-lookup"><span data-stu-id="d49be-104">Use Robomongo with an Azure Cosmos DB: API for MongoDB account</span></span>
<span data-ttu-id="d49be-105">若要使用 Robomongo 連線到 Azure Cosmos DB：適用於 MongoDB 的 API 帳戶，您必須︰</span><span class="sxs-lookup"><span data-stu-id="d49be-105">To connect to an Azure Cosmos DB: API for MongoDB account using Robomongo, you must:</span></span>

* <span data-ttu-id="d49be-106">下載並安裝 [Robomongo](https://robomongo.org/)</span><span class="sxs-lookup"><span data-stu-id="d49be-106">Download and install [Robomongo](https://robomongo.org/)</span></span>
* <span data-ttu-id="d49be-107">具備您的 Azure Cosmos DB：適用於 MongoDB 的 API 帳戶[連接字串](connect-mongodb-account.md)資訊</span><span class="sxs-lookup"><span data-stu-id="d49be-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="connect-using-robomongo"></a><span data-ttu-id="d49be-108">使用 Robomongo 來連接</span><span class="sxs-lookup"><span data-stu-id="d49be-108">Connect using Robomongo</span></span>
<span data-ttu-id="d49be-109">若要將 Azure Cosmos DB：適用於 MongoDB 的 API 帳戶新增至 Robomongo MongoDB 連線，請執行下列步驟。</span><span class="sxs-lookup"><span data-stu-id="d49be-109">To add your Azure Cosmos DB: API for MongoDB account to the Robomongo MongoDB Connections, perform the following steps.</span></span>

1. <span data-ttu-id="d49be-110">使用[這裡](connect-mongodb-account.md)的指示來擷取 Azure Cosmos DB：適用於 MongoDB 的 API 帳戶的連線資訊。</span><span class="sxs-lookup"><span data-stu-id="d49be-110">Retrieve your Azure Cosmos DB: API for MongoDB account connection information using the instructions [here](connect-mongodb-account.md).</span></span>

    ![[連接字串] 刀鋒視窗的螢幕擷取畫面](./media/mongodb-robomongo/connectionstringblade.png)
2. <span data-ttu-id="d49be-112">執行 *Robomongo.exe*</span><span class="sxs-lookup"><span data-stu-id="d49be-112">Run *Robomongo.exe*</span></span>

3. <span data-ttu-id="d49be-113">按一下 [檔案] 下的 [連接] 按鈕來管理您的連接。</span><span class="sxs-lookup"><span data-stu-id="d49be-113">Click the connection button under **File** to manage your connections.</span></span> <span data-ttu-id="d49be-114">然後，按一下 [MongoDB 連接] 視窗中的 [建立]，將會開啟 [連接設定] 視窗。</span><span class="sxs-lookup"><span data-stu-id="d49be-114">Then, click **Create** in the **MongoDB Connections** window, which will open up the **Connection Settings** window.</span></span>

4. <span data-ttu-id="d49be-115">在 [連接設定] 視窗中，選擇名稱。</span><span class="sxs-lookup"><span data-stu-id="d49be-115">In the **Connection Settings** window, choose a name.</span></span> <span data-ttu-id="d49be-116">然後，從步驟 1 的連接資訊中，找出 [主機] 和 [連接埠]，分別輸入至 [位址] 和 [連接埠]。</span><span class="sxs-lookup"><span data-stu-id="d49be-116">Then, find the **Host** and **Port** from your connection information in Step 1 and enter them into **Address** and **Port**, respectively.</span></span>

    ![Robomongo 管理連線的螢幕擷取畫面](./media/mongodb-robomongo/manageconnections.png)
5. <span data-ttu-id="d49be-118">在 [驗證] 索引標籤上，按一下 [執行驗證]。</span><span class="sxs-lookup"><span data-stu-id="d49be-118">On the **Authentication** tab, click **Perform authentication**.</span></span> <span data-ttu-id="d49be-119">然後，輸入您的 [資料庫] \(預設值是 *Admin*)、[使用者名稱] 和 [密碼]。</span><span class="sxs-lookup"><span data-stu-id="d49be-119">Then, enter your Database (default is *Admin*), **User Name** and **Password**.</span></span>
<span data-ttu-id="d49be-120">在步驟 1 的連接資訊中，可以找到 [使用者名稱] 和 [密碼]。</span><span class="sxs-lookup"><span data-stu-id="d49be-120">Both **User Name** and **Password** can be found in your connection information in Step 1.</span></span>

    ![Robomongo 驗證索引標籤的螢幕擷取畫面](./media/mongodb-robomongo/authentication.png)
6. <span data-ttu-id="d49be-122">在 [SSL] 索引標籤上，勾選 [使用 SSL 通訊協定]，然後將 [驗證方法] 變更為 [自我簽署憑證]。</span><span class="sxs-lookup"><span data-stu-id="d49be-122">On the **SSL** tab, check **Use SSL protocol**, then change the **Authentication Method** to **Self-signed Certificate**.</span></span>

    ![Robomongo SSL 索引標籤的螢幕擷取畫面](./media/mongodb-robomongo/SSL.png)
7. <span data-ttu-id="d49be-124">最後，按一下 [測試] 以確認您能夠連接，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="d49be-124">Finally, click **Test** to verify that you are able to connect, then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d49be-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d49be-125">Next steps</span></span>
* <span data-ttu-id="d49be-126">瀏覽 Azure Cosmos DB：適用於 MongoDB 的 API [範例](mongodb-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="d49be-126">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
