---
title: "aaaStore 非結構化的資料，使用 Azure 函式和 Cosmos DB"
description: "使用 Azure Functions 和 Cosmos DB 儲存非結構化資料"
services: functions
documentationcenter: functions
author: rachelappel
manager: erikre
editor: 
tags: 
keywords: "azure functions, 函式, 事件處理, Cosmos DB, 動態計算, 無伺服器架構"
ms.assetid: 
ms.service: functions
ms.devlang: csharp
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 08/03/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: 48d6899c20d3e6f6b062725fca329972ead3c696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="store-unstructured-data-using-azure-functions-and-cosmos-db"></a><span data-ttu-id="a958d-104">使用 Azure Functions 和 Cosmos DB 儲存非結構化資料</span><span class="sxs-lookup"><span data-stu-id="a958d-104">Store unstructured data using Azure Functions and Cosmos DB</span></span>

<span data-ttu-id="a958d-105">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)是很好的方法 toostore 非結構化和 JSON 資料。</span><span class="sxs-lookup"><span data-stu-id="a958d-105">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is a great way toostore unstructured and JSON data.</span></span> <span data-ttu-id="a958d-106">Cosmos DB 與 Azure Functions 結合，能夠讓儲存資料輕鬆快速，所使用的程式碼比起在關聯式資料庫中儲存資料所需的程式碼更少。</span><span class="sxs-lookup"><span data-stu-id="a958d-106">Combined with Azure Functions, Cosmos DB makes storing data quick and easy with much less code than required for storing data in a relational database.</span></span>

<span data-ttu-id="a958d-107">在 Azure 功能中，輸入和輸出繫結會提供從您的函式宣告的方式來 tooconnect tooexternal 服務資料。</span><span class="sxs-lookup"><span data-stu-id="a958d-107">In Azure Functions, input and output bindings provide a declarative way tooconnect tooexternal service data from your function.</span></span> <span data-ttu-id="a958d-108">本主題中，了解 tooupdate 現有的 C# 的運作狀況如何 tooadd Cosmos DB 文件中儲存非結構化的資料的輸出繫結。</span><span class="sxs-lookup"><span data-stu-id="a958d-108">In this topic, learn how tooupdate an existing C# function tooadd an output binding that stores unstructured data in a Cosmos DB document.</span></span> 

![Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-cosmosdb.png)

## <a name="prerequisites"></a><span data-ttu-id="a958d-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="a958d-110">Prerequisites</span></span>

<span data-ttu-id="a958d-111">toocomplete 本教學課程：</span><span class="sxs-lookup"><span data-stu-id="a958d-111">toocomplete this tutorial:</span></span>

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

## <a name="add-an-output-binding"></a><span data-ttu-id="a958d-112">新增輸出繫結</span><span class="sxs-lookup"><span data-stu-id="a958d-112">Add an output binding</span></span>

1. <span data-ttu-id="a958d-113">展開函式應用程式和函式。</span><span class="sxs-lookup"><span data-stu-id="a958d-113">Expand both your function app and your function.</span></span>

1. <span data-ttu-id="a958d-114">選取**整合**和**+ 新輸出**，這是在 hello hello 頁面的右上方。</span><span class="sxs-lookup"><span data-stu-id="a958d-114">Select **Integrate** and **+ New Output**, which is at hello top right of hello page.</span></span> <span data-ttu-id="a958d-115">選擇 [Azure Cosmos DB]，然後按一下 [選取]。</span><span class="sxs-lookup"><span data-stu-id="a958d-115">Choose **Azure Cosmos DB**, and click **Select**.</span></span>

    ![新增 Cosmos DB 輸出繫結](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-add-new-output-binding.png)

3. <span data-ttu-id="a958d-117">使用 hello **Azure Cosmos DB 輸出**hello 資料表中所指定的設定：</span><span class="sxs-lookup"><span data-stu-id="a958d-117">Use hello **Azure Cosmos DB output** settings as specified in hello table:</span></span> 

    ![設定 Cosmos DB 輸出繫結](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-configure-cosmosdb-binding.png)

    | <span data-ttu-id="a958d-119">設定</span><span class="sxs-lookup"><span data-stu-id="a958d-119">Setting</span></span>      | <span data-ttu-id="a958d-120">建議的值</span><span class="sxs-lookup"><span data-stu-id="a958d-120">Suggested value</span></span>  | <span data-ttu-id="a958d-121">說明</span><span class="sxs-lookup"><span data-stu-id="a958d-121">Description</span></span>                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | <span data-ttu-id="a958d-122">**文件參數名稱**</span><span class="sxs-lookup"><span data-stu-id="a958d-122">**Document parameter name**</span></span> | <span data-ttu-id="a958d-123">taskDocument</span><span class="sxs-lookup"><span data-stu-id="a958d-123">taskDocument</span></span> | <span data-ttu-id="a958d-124">參考程式碼中的 toohello Cosmos DB 物件的名稱。</span><span class="sxs-lookup"><span data-stu-id="a958d-124">Name that refers toohello Cosmos DB object in code.</span></span> |
    | <span data-ttu-id="a958d-125">**資料庫名稱**</span><span class="sxs-lookup"><span data-stu-id="a958d-125">**Database name**</span></span> | <span data-ttu-id="a958d-126">taskDatabase</span><span class="sxs-lookup"><span data-stu-id="a958d-126">taskDatabase</span></span> | <span data-ttu-id="a958d-127">資料庫 toosave 文件的名稱。</span><span class="sxs-lookup"><span data-stu-id="a958d-127">Name of database toosave documents.</span></span> |
    | <span data-ttu-id="a958d-128">**集合名稱**</span><span class="sxs-lookup"><span data-stu-id="a958d-128">**Collection name**</span></span> | <span data-ttu-id="a958d-129">TaskCollection</span><span class="sxs-lookup"><span data-stu-id="a958d-129">TaskCollection</span></span> | <span data-ttu-id="a958d-130">Cosmos DB 資料庫的集合名稱。</span><span class="sxs-lookup"><span data-stu-id="a958d-130">Name of collection of Cosmos DB databases.</span></span> |
    | <span data-ttu-id="a958d-131">**如果為 true，就會建立 hello Cosmos DB 資料庫與集合**</span><span class="sxs-lookup"><span data-stu-id="a958d-131">**If true, creates hello Cosmos DB database and collection**</span></span> | <span data-ttu-id="a958d-132">已檢查</span><span class="sxs-lookup"><span data-stu-id="a958d-132">Checked</span></span> | <span data-ttu-id="a958d-133">hello 集合不存在，因此請建立它。</span><span class="sxs-lookup"><span data-stu-id="a958d-133">hello collection doesn't already exist, so create it.</span></span> |

4. <span data-ttu-id="a958d-134">選取**新增**下一步 toohello **Cosmos DB 文件連接**加上標籤，然後選取**+ Create new**。</span><span class="sxs-lookup"><span data-stu-id="a958d-134">Select **New** next toohello **Cosmos DB document connection** label, and select **+ Create new**.</span></span> 

5. <span data-ttu-id="a958d-135">使用 hello**新帳戶**hello 資料表中所指定的設定：</span><span class="sxs-lookup"><span data-stu-id="a958d-135">Use hello **New account** settings as specified in hello table:</span></span> 

    ![設定 Cosmos DB 連線](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-create-CosmosDB.png)

    | <span data-ttu-id="a958d-137">設定</span><span class="sxs-lookup"><span data-stu-id="a958d-137">Setting</span></span>      | <span data-ttu-id="a958d-138">建議的值</span><span class="sxs-lookup"><span data-stu-id="a958d-138">Suggested value</span></span>  | <span data-ttu-id="a958d-139">說明</span><span class="sxs-lookup"><span data-stu-id="a958d-139">Description</span></span>                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | <span data-ttu-id="a958d-140">**識別碼**</span><span class="sxs-lookup"><span data-stu-id="a958d-140">**ID**</span></span> | <span data-ttu-id="a958d-141">資料庫名稱</span><span class="sxs-lookup"><span data-stu-id="a958d-141">Name of database</span></span> | <span data-ttu-id="a958d-142">Hello Cosmos DB 資料庫的唯一識別碼</span><span class="sxs-lookup"><span data-stu-id="a958d-142">Unique ID for hello Cosmos DB database</span></span>  |
    | <span data-ttu-id="a958d-143">**API**</span><span class="sxs-lookup"><span data-stu-id="a958d-143">**API**</span></span> | <span data-ttu-id="a958d-144">SQL (DocumentDB)</span><span class="sxs-lookup"><span data-stu-id="a958d-144">SQL (DocumentDB)</span></span> | <span data-ttu-id="a958d-145">選取 hello 文件資料庫 API。</span><span class="sxs-lookup"><span data-stu-id="a958d-145">Select hello document database API.</span></span>  |
    | <span data-ttu-id="a958d-146">**訂用帳戶**</span><span class="sxs-lookup"><span data-stu-id="a958d-146">**Subscription**</span></span> | <span data-ttu-id="a958d-147">Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="a958d-147">Azure Subscription</span></span> | <span data-ttu-id="a958d-148">Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="a958d-148">Azure Subscription</span></span>  |
    | <span data-ttu-id="a958d-149">**資源群組**</span><span class="sxs-lookup"><span data-stu-id="a958d-149">**Resource Group**</span></span> | <span data-ttu-id="a958d-150">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a958d-150">myResourceGroup</span></span> |  <span data-ttu-id="a958d-151">使用 hello 現有的資源群組，其中包含應用程式函式。</span><span class="sxs-lookup"><span data-stu-id="a958d-151">Use hello existing resource group that contains your function app.</span></span> |
    | <span data-ttu-id="a958d-152">**位置**</span><span class="sxs-lookup"><span data-stu-id="a958d-152">**Location**</span></span>  | <span data-ttu-id="a958d-153">WestEurope</span><span class="sxs-lookup"><span data-stu-id="a958d-153">WestEurope</span></span> | <span data-ttu-id="a958d-154">您的函式應用程式或使用 hello 儲存文件的 tooother 應用程式，請選取 tooeither 附近的位置。</span><span class="sxs-lookup"><span data-stu-id="a958d-154">Select a location near tooeither your function app or tooother apps that use hello stored documents.</span></span>  |

6. <span data-ttu-id="a958d-155">按一下**確定**toocreate hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="a958d-155">Click **OK** toocreate hello database.</span></span> <span data-ttu-id="a958d-156">可能需要幾分鐘的時間 toocreate hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="a958d-156">It may take a few minutes toocreate hello database.</span></span> <span data-ttu-id="a958d-157">建立 hello 資料庫後，hello 資料庫連接字串會儲存為函式應用程式設定中。</span><span class="sxs-lookup"><span data-stu-id="a958d-157">After hello database is created, hello database connection string is stored as a function app setting.</span></span> <span data-ttu-id="a958d-158">此應用程式設定的 hello 名稱會插入在**Cosmos DB 帳戶連接**。</span><span class="sxs-lookup"><span data-stu-id="a958d-158">hello name of this app setting is inserted in **Cosmos DB account connection**.</span></span> 
 
8. <span data-ttu-id="a958d-159">設定 hello 連接字串之後，請選取**儲存**toocreate hello 繫結。</span><span class="sxs-lookup"><span data-stu-id="a958d-159">After hello connection string is set, select **Save** toocreate hello binding.</span></span>

## <a name="update-hello-function-code"></a><span data-ttu-id="a958d-160">更新 hello 函式程式碼</span><span class="sxs-lookup"><span data-stu-id="a958d-160">Update hello function code</span></span>

<span data-ttu-id="a958d-161">Hello 現有 C# 函式程式碼取代下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="a958d-161">Replace hello existing C# function code with hello following code:</span></span>

```csharp
using System.Net;

public static HttpResponseMessage Run(HttpRequestMessage req, out object taskDocument, TraceWriter log)
{
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    string task = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "task", true) == 0)
        .Value;

    string duedate = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "duedate", true) == 0)
        .Value;

    taskDocument = new {
        name = name,
        duedate = duedate.ToString(),
        task = task
    };

    if (name != "" && task != "") {
        return req.CreateResponse(HttpStatusCode.OK);
    }
    else {
        return req.CreateResponse(HttpStatusCode.BadRequest);
    }
}

```
<span data-ttu-id="a958d-162">此程式碼範例讀取 hello HTTP 要求查詢字串，並將它們指派在 hello toofields`taskDocument`物件。</span><span class="sxs-lookup"><span data-stu-id="a958d-162">This code sample reads hello HTTP Request query strings and assigns them toofields in hello `taskDocument` object.</span></span> <span data-ttu-id="a958d-163">hello`taskDocument`繫結從 hello 繫結的文件資料庫中儲存此繫結參數 toobe 傳送嗨物件資料。</span><span class="sxs-lookup"><span data-stu-id="a958d-163">hello `taskDocument` binding sends hello object data from this binding parameter toobe stored in hello bound document database.</span></span> <span data-ttu-id="a958d-164">hello 資料庫會建立 hello hello 函式會執行第一次。</span><span class="sxs-lookup"><span data-stu-id="a958d-164">hello database is created hello first time hello function runs.</span></span>

## <a name="test-hello-function-and-database"></a><span data-ttu-id="a958d-165">測試 hello 函式和資料庫</span><span class="sxs-lookup"><span data-stu-id="a958d-165">Test hello function and database</span></span>

1. <span data-ttu-id="a958d-166">展開 hello 右側視窗，然後選取**測試**。</span><span class="sxs-lookup"><span data-stu-id="a958d-166">Expand hello right window and select **Test**.</span></span> <span data-ttu-id="a958d-167">在下**查詢**，按一下  **+ 加入參數**並加入下列參數 toohello 查詢字串 hello:</span><span class="sxs-lookup"><span data-stu-id="a958d-167">Under **Query**, click **+ Add parameter** and add hello following parameters toohello query string:</span></span>

    + `name`
    + `task`
    + `duedate`

2. <span data-ttu-id="a958d-168">按一下 [執行] 並確認會傳回 200 狀態。</span><span class="sxs-lookup"><span data-stu-id="a958d-168">Click **Run** and verify that a 200 status is returned.</span></span>

    ![設定 Cosmos DB 輸出繫結](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-test-function.png)

1. <span data-ttu-id="a958d-170">在 hello hello Azure 入口網站的左側，展開 hello 圖示列中，型別`cosmos`hello 中搜尋的欄位，然後選取**Azure Cosmos DB**。</span><span class="sxs-lookup"><span data-stu-id="a958d-170">On hello left side of hello Azure portal, expand hello icon bar, type `cosmos` in hello search field, and select **Azure Cosmos DB**.</span></span>

    ![搜尋 hello Cosmos 資料庫服務](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-search-cosmos-db.png)

2. <span data-ttu-id="a958d-172">選取 hello 您建立的資料庫，然後選取**資料總管**。</span><span class="sxs-lookup"><span data-stu-id="a958d-172">Select hello database you created, then select **Data Explorer**.</span></span> <span data-ttu-id="a958d-173">展開 hello**集合**節點，選取 hello 新文件，並確認該 hello 文件包含您的查詢字串值，以及一些其他的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="a958d-173">Expand hello **Collections** nodes, select hello new document, and confirm that hello document contains your query string values, along with some additional metadata.</span></span> 

    ![確認 Cosmos DB 項目](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-verify-cosmosdb-output.png)

<span data-ttu-id="a958d-175">您已成功加入的繫結 tooyour HTTP 觸發程序 Cosmos DB 資料庫中儲存非結構化的資料。</span><span class="sxs-lookup"><span data-stu-id="a958d-175">You have successfully added a binding tooyour HTTP trigger that stores unstructured data in a Cosmos DB database.</span></span>

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="a958d-176">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a958d-176">Next steps</span></span>

[!INCLUDE [functions-quickstart-next-steps](../../includes/functions-quickstart-next-steps.md)]

<span data-ttu-id="a958d-177">如需繫結 tooa Cosmos DB 資料庫的詳細資訊，請參閱[Azure 函式 Cosmos DB 繫結](functions-bindings-documentdb.md)。</span><span class="sxs-lookup"><span data-stu-id="a958d-177">For more information about binding tooa Cosmos DB database, see [Azure Functions Cosmos DB bindings](functions-bindings-documentdb.md).</span></span>
