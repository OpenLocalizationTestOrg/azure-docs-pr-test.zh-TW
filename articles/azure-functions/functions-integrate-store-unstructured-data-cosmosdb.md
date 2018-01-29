---
title: "使用 Azure Cosmos DB 和 Functions 儲存非結構化資料 | Microsoft Docs"
description: "使用 Azure Functions 和 Cosmos DB 儲存非結構化資料"
services: functions
documentationcenter: functions
author: ggailey777
manager: cfowler
editor: 
tags: 
keywords: "azure functions, 函式, 事件處理, Cosmos DB, 動態計算, 無伺服器架構"
ms.assetid: 
ms.service: functions
ms.devlang: csharp
ms.topic: quickstart
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 09/19/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: b9bb71adf85490fe68bf6b73133017c5e9c377e1
ms.sourcegitcommit: 71fa59e97b01b65f25bcae318d834358fea5224a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/11/2018
---
# <a name="store-unstructured-data-using-azure-functions-and-azure-cosmos-db"></a>使用 Azure Functions 和 Azure Cosmos DB 儲存非結構化資料

[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) 是儲存非結構化和 JSON 資料的好方法。 Cosmos DB 與 Azure Functions 結合，能夠讓儲存資料輕鬆快速，所使用的程式碼比起在關聯式資料庫中儲存資料所需的程式碼更少。

> [!NOTE]
> 此時，Azure Cosmos DB 觸發程序、輸入繫結，以及輸出繫結只會使用 SQL API 和圖形 API 帳戶。

在 Azure Functions 中，輸入和輸出繫結會提供宣告式方法，以便從函式連線到外部服務資料。 在本主題中，了解如何更新現有的 C# 函式，以新增可在 Cosmos DB 文件中儲存非結構化資料的輸出繫結。 

![Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-cosmosdb.png)

## <a name="prerequisites"></a>先決條件

若要完成本教學課程：

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

## <a name="add-an-output-binding"></a>新增輸出繫結

1. 展開函式應用程式和函式。

1. 選取 [整合] 和 [+ 新增輸出]，其位於頁面的右上方。 選擇 [Azure Cosmos DB]，然後按一下 [選取]。

    ![新增 Cosmos DB 輸出繫結](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-add-new-output-binding.png)

3. 使用表格中所指定的 [Azure Cosmos DB 輸出] 設定： 

    ![設定 Cosmos DB 輸出繫結](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-configure-cosmosdb-binding.png)

    | 設定      | 建議的值  | 說明                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | **文件參數名稱** | taskDocument | 該名稱參考程式碼中的 Cosmos DB 物件。 |
    | **資料庫名稱** | taskDatabase | 用於儲存文件的資料庫名稱。 |
    | **集合名稱** | TaskCollection | 資料庫集合的名稱。 |
    | **如果為 true，就會建立 Cosmos DB 資料庫和集合** | 已檢查 | 集合尚未存在，因此加以建立。 |

4. 選取 [Azure Cosmos DB 文件連線] 標籤旁的 [新增]，然後選取 [+ 建立新的]。 

5. 使用表格中所指定的 [新增帳戶] 設定︰ 

    ![設定 Cosmos DB 連線](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-create-CosmosDB.png)

    | 設定      | 建議的值  | 說明                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | **識別碼** | 資料庫名稱 | Azure Cosmos DB 資料庫的唯一識別碼  |
    | **API** | SQL | 選取 SQL API。 此時，Azure Cosmos DB 觸發程序、輸入繫結，以及輸出繫結只會使用 SQL API 和圖形 API 帳戶。 |
    | **訂用帳戶** | Azure 訂閱 | Azure 訂閱  |
    | **資源群組** | myResourceGroup |  使用含有您的函式應用程式的現有資源群組。 |
    | <bpt id="p1">**</bpt>Location<ept id="p1">**</ept>  | WestEurope | 選取您的函式應用程式或其他使用已儲存文件的應用程式附近的位置。  |

6. 按一下 [確定]  以建立資料庫。 建立資料庫可能需要幾分鐘的時間。 建立資料庫之後，資料庫連接字串會儲存為函式應用程式設定。 此應用程式設定的名稱會插入在 **Azure Cosmos DB 帳戶連線**中。 
 
8. 設定連接字串之後，請選取 [儲存] 以建立繫結。

## <a name="update-the-function-code"></a>更新函式程式碼

將現有 C# 函式程式碼取代為下列程式碼：

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
此程式碼範例會讀取 HTTP 要求查詢字串，並將它們指派給 `taskDocument` 物件中的欄位。 `taskDocument` 繫結會從此繫結參數傳送物件資料，以便儲存在繫結的文件資料庫中。 第一次執行函式時會建立資料庫。

## <a name="test-the-function-and-database"></a>測試函式和資料庫

1. 展開右側視窗，然後選取 [測試]。 在 [查詢] 之下，按一下 [+ 新增參數] 並將下列參數新增至查詢字串：

    + `name`
    + `task`
    + `duedate`

2. 按一下 [執行] 並確認會傳回 200 狀態。

    ![設定 Cosmos DB 輸出繫結](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-test-function.png)

1. 在 Azure 入口網站的左側，展開圖示列，在搜尋欄位中輸入 `cosmos`，然後選取 [Azure Cosmos DB]。

    ![搜尋 Cosmos DB 服務](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-search-cosmos-db.png)

2. 選擇您的 Azure Cosmos DB 帳戶，然後選取 [資料總管]。 

3. 展開 [集合] 節點，選取新文件，並確認文件包含您的查詢字串值，以及一些額外的中繼資料。 

    ![確認 Cosmos DB 項目](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-verify-cosmosdb-output.png)

您已將繫結成功新增至可在 Azure Cosmos DB 中儲存非結構化資料的 HTTP 觸發程序。

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>後續步驟

[!INCLUDE [functions-quickstart-next-steps](../../includes/functions-quickstart-next-steps.md)]

如需繫結至 Cosmos DB 資料庫的詳細資訊，請參閱 [Azure Functions Cosmos DB 繫結](functions-bindings-cosmosdb.md)。
