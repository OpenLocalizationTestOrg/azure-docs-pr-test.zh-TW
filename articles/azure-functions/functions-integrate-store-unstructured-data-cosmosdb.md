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
# <a name="store-unstructured-data-using-azure-functions-and-cosmos-db"></a>使用 Azure Functions 和 Cosmos DB 儲存非結構化資料

[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)是很好的方法 toostore 非結構化和 JSON 資料。 Cosmos DB 與 Azure Functions 結合，能夠讓儲存資料輕鬆快速，所使用的程式碼比起在關聯式資料庫中儲存資料所需的程式碼更少。

在 Azure 功能中，輸入和輸出繫結會提供從您的函式宣告的方式來 tooconnect tooexternal 服務資料。 本主題中，了解 tooupdate 現有的 C# 的運作狀況如何 tooadd Cosmos DB 文件中儲存非結構化的資料的輸出繫結。 

![Cosmos DB](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-cosmosdb.png)

## <a name="prerequisites"></a>必要條件

toocomplete 本教學課程：

[!INCLUDE [Previous quickstart note](../../includes/functions-quickstart-previous-topics.md)]

## <a name="add-an-output-binding"></a>新增輸出繫結

1. 展開函式應用程式和函式。

1. 選取**整合**和**+ 新輸出**，這是在 hello hello 頁面的右上方。 選擇 [Azure Cosmos DB]，然後按一下 [選取]。

    ![新增 Cosmos DB 輸出繫結](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-add-new-output-binding.png)

3. 使用 hello **Azure Cosmos DB 輸出**hello 資料表中所指定的設定： 

    ![設定 Cosmos DB 輸出繫結](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-integrate-tab-configure-cosmosdb-binding.png)

    | 設定      | 建議的值  | 說明                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | **文件參數名稱** | taskDocument | 參考程式碼中的 toohello Cosmos DB 物件的名稱。 |
    | **資料庫名稱** | taskDatabase | 資料庫 toosave 文件的名稱。 |
    | **集合名稱** | TaskCollection | Cosmos DB 資料庫的集合名稱。 |
    | **如果為 true，就會建立 hello Cosmos DB 資料庫與集合** | 已檢查 | hello 集合不存在，因此請建立它。 |

4. 選取**新增**下一步 toohello **Cosmos DB 文件連接**加上標籤，然後選取**+ Create new**。 

5. 使用 hello**新帳戶**hello 資料表中所指定的設定： 

    ![設定 Cosmos DB 連線](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-create-CosmosDB.png)

    | 設定      | 建議的值  | 說明                                |
    | ------------ | ---------------- | ------------------------------------------ |
    | **識別碼** | 資料庫名稱 | Hello Cosmos DB 資料庫的唯一識別碼  |
    | **API** | SQL (DocumentDB) | 選取 hello 文件資料庫 API。  |
    | **訂用帳戶** | Azure 訂閱 | Azure 訂閱  |
    | **資源群組** | myResourceGroup |  使用 hello 現有的資源群組，其中包含應用程式函式。 |
    | **位置**  | WestEurope | 您的函式應用程式或使用 hello 儲存文件的 tooother 應用程式，請選取 tooeither 附近的位置。  |

6. 按一下**確定**toocreate hello 資料庫。 可能需要幾分鐘的時間 toocreate hello 資料庫。 建立 hello 資料庫後，hello 資料庫連接字串會儲存為函式應用程式設定中。 此應用程式設定的 hello 名稱會插入在**Cosmos DB 帳戶連接**。 
 
8. 設定 hello 連接字串之後，請選取**儲存**toocreate hello 繫結。

## <a name="update-hello-function-code"></a>更新 hello 函式程式碼

Hello 現有 C# 函式程式碼取代下列程式碼的 hello:

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
此程式碼範例讀取 hello HTTP 要求查詢字串，並將它們指派在 hello toofields`taskDocument`物件。 hello`taskDocument`繫結從 hello 繫結的文件資料庫中儲存此繫結參數 toobe 傳送嗨物件資料。 hello 資料庫會建立 hello hello 函式會執行第一次。

## <a name="test-hello-function-and-database"></a>測試 hello 函式和資料庫

1. 展開 hello 右側視窗，然後選取**測試**。 在下**查詢**，按一下  **+ 加入參數**並加入下列參數 toohello 查詢字串 hello:

    + `name`
    + `task`
    + `duedate`

2. 按一下 [執行] 並確認會傳回 200 狀態。

    ![設定 Cosmos DB 輸出繫結](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-test-function.png)

1. 在 hello hello Azure 入口網站的左側，展開 hello 圖示列中，型別`cosmos`hello 中搜尋的欄位，然後選取**Azure Cosmos DB**。

    ![搜尋 hello Cosmos 資料庫服務](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-search-cosmos-db.png)

2. 選取 hello 您建立的資料庫，然後選取**資料總管**。 展開 hello**集合**節點，選取 hello 新文件，並確認該 hello 文件包含您的查詢字串值，以及一些其他的中繼資料。 

    ![確認 Cosmos DB 項目](./media/functions-integrate-store-unstructured-data-cosmosdb/functions-verify-cosmosdb-output.png)

您已成功加入的繫結 tooyour HTTP 觸發程序 Cosmos DB 資料庫中儲存非結構化的資料。

[!INCLUDE [Clean-up section](../../includes/clean-up-section-portal.md)]

## <a name="next-steps"></a>後續步驟

[!INCLUDE [functions-quickstart-next-steps](../../includes/functions-quickstart-next-steps.md)]

如需繫結 tooa Cosmos DB 資料庫的詳細資訊，請參閱[Azure 函式 Cosmos DB 繫結](functions-bindings-documentdb.md)。
