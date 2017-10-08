---
title: "Azure Cosmos DB.NET 應用程式使用 aaaBuild hello 表格 API |Microsoft 文件"
description: "使用 .NET 來開始使用 Azure Cosmos DB 的資料表 API"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: 
ms.assetid: 66327041-4d5e-4ce6-a394-fee107c18e59
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/22/2017
ms.author: arramac
ms.openlocfilehash: bdd4f8ec45407962b3d2cb26aa814a20cfc62173
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-table-api"></a>Azure Cosmos DB： 建置使用 hello 表格 API 的.NET 應用程式

Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。 您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。 

本快速入門示範如何 toocreate Azure Cosmos DB 帳戶，並建立該帳戶使用 hello Azure 入口網站內的資料表。 您將撰寫程式碼 tooinsert、 更新和刪除實體，然後執行一些查詢，使用新的 hello [Windows Azure 儲存體 Premium 資料表](https://aka.ms/premiumtablenuget)NuGet 封裝 （預覽）。 此媒體櫃具有 hello 相同的類別和方法簽章為 hello 公用[Windows Azure 儲存體 SDK](https://www.nuget.org/packages/WindowsAzure.Storage)，但也有 hello 能力 tooconnect tooAzure Cosmos DB 帳戶使用 hello[表格 API](table-introduction.md) （預覽）。 

## <a name="prerequisites"></a>必要條件

如果您還沒有安裝 Visual Studio 2017，您可以下載並使用 hello**可用** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)。 請確定您啟用**Azure 開發**hello Visual Studio 安裝期間。

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>建立資料庫帳戶

[!INCLUDE [cosmos-db-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)]

## <a name="add-a-table"></a>新增資料表

[!INCLUDE [cosmos-db-create-table](../../includes/cosmos-db-create-table.md)]

## <a name="add-sample-data"></a>新增範例資料

您現在可以新增資料 tooyour 新資料表使用資料檔案總管 （預覽）。

1. 在資料總管中，展開 **sample-table**，按一下 實體，然後按一下新增實體。

   ![Hello Azure 入口網站中，資料檔案總管中建立新的實體](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-document.png)
2. 現在加入資料 toohello PartitionKey 值 方塊和 RowKey 值 方塊中，並按一下**加入實體**。

   ![設定資料分割索引鍵和新的實體的資料列索引鍵 hello](./media/create-table-dotnet/azure-cosmosdb-data-explorer-new-entity.png)
  
    您現在可以將多個實體 tooyour 資料表加入、 編輯您的實體，或查詢資料的資料總管。 資料總管也是您可以在此調整您的輸送量，並將預存程序、 使用者定義函數和觸發程序 tooyour 資料表。

## <a name="clone-hello-sample-application"></a>複製 hello 範例應用程式

現在讓我們來複製資料表中的應用程式 github 設定 hello 連接字串，並執行它。 您會看到是多麼的輕鬆 toowork 資料以程式設計的方式。 

1. 開啟 git 終端機視窗，例如 git bash 和`cd`tooa 工作目錄。  

2. 執行下列命令 tooclone hello 範例儲存機制的 hello。 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started.git
    ```

3. 然後在 Visual Studio 中開啟 hello 方案檔。 

## <a name="review-hello-code"></a>檢閱 hello 程式碼

讓我們進行快速檢閱 hello 應用程式中的情況。 開啟 hello Program.cs 檔案，而且您會發現這行程式碼建立 hello Azure Cosmos DB 資源。 

* hello CloudTableClient 會初始化。

    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); 
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

* 如果資料表不存在，將會建立資料表。

    ```csharp
    CloudTable table = tableClient.GetTableReference("people");
    table.CreateIfNotExists();
    ```

* 已建立新的資料表容器。 您會注意到此程式碼非常類似 tooregular Azure 資料表儲存體 SDK。 

    ```csharp
    CustomerEntity item = new CustomerEntity()
                {
                    PartitionKey = Guid.NewGuid().ToString(),
                    RowKey = Guid.NewGuid().ToString(),
                    Email = $"{GetRandomString(6)}@contoso.com",
                    PhoneNumber = "425-555-0102",
                    Bio = GetRandomString(1000)
                };
    ```

## <a name="update-your-connection-string"></a>更新您的連接字串

現在我們將更新 hello 連接字串資訊，使您的應用程式可以彼此通訊 tooAzure Cosmos DB。 

1. 在 Visual Studio 中，開啟 hello app.config 檔案。 

2. 在 hello [Azure 入口網站](http://portal.azure.com/)，請在 hello Azure Cosmos DB 左導覽功能表中按一下**連接字串**。 然後在 hello 新窗格中按一下針對 hello 的連接字串 hello [複製] 按鈕。 

    ![檢視及複製在 hello 連接字串 窗格中的 hello 端點和帳戶金鑰](./media/create-table-dotnet/keys.png)

3. Hello 值貼到 hello app.config 檔案，做為 hello PremiumStorageConnectionString hello 值。 

    `<add key="PremiumStorageConnectionString" 
        value="DefaultEndpointsProtocol=https;AccountName=MYSTORAGEACCOUNT;AccountKey=AUTHKEY;TableEndpoint=https://COSMOSDB.documents.azure.com" />`    

    您可以保留 hello StandardStorageConnectionString 原狀。

您現在已更新您的應用程式與它需要與 Azure Cosmos DB toocommunicate 所有 hello 資訊。 

## <a name="run-hello-web-app"></a>執行 hello web 應用程式

1. 在 Visual Studio 中，以滑鼠右鍵按一下 hello **PremiumTableGetStarted**專案中**方案總管 中**，然後按一下**管理 NuGet 封裝**。 

2. 在 hello NuGet**瀏覽**方塊中，輸入*WindowsAzure.Storage PremiumTable*。

3. 檢查 hello**包含發行前版本**方塊。 

4. 從 hello 結果中，安裝 hello **WindowsAzure.Storage PremiumTable**程式庫。 這會安裝 hello 預覽 Azure Cosmos DB 資料表 API 套件，以及所有相依性。 請注意，這不同於 hello Windows Azure 儲存體套件使用的 Azure 資料表儲存體 NuGet 封裝。 

5. 按一下 CTRL + F5 toorun hello 應用程式。

    hello 主控台視窗會顯示 hello 資料加入、 擷取、 查詢、 取代和 hello 資料表中刪除。 Hello 指令碼完成時，請按任何鍵 tooclose hello 主控台視窗。 
    
    ![主控台輸出的 hello 快速入門](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-console-output.png)

6. 如果您想 toosee hello 新中的實體資料總管 中，只是標記為註解中程式碼行 188 208 program.cs，因此這些檔案不刪除，然後再次執行 hello 範例。 

    您現在可以移回 tooData 總管 中，按一下 **重新整理**，依序展開 hello**人員**資料表，並按一下**實體**，，然後使用這項新資料。 

    ![在資料總管中新增實體](./media/create-table-dotnet/azure-cosmosdb-table-quickstart-data-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a>在 hello Azure 入口網站中檢視 Sla

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>清除資源

如果您不打算 toocontinue toouse 此應用程式，刪除所有資源本快速入門以建立 hello Azure 入口網站以 hello 下列步驟： 

1. Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您所建立的 hello 資源的 hello 名稱。 
2. 在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。

## <a name="next-steps"></a>後續步驟

本快速入門中，您學到如何 toocreate Azure Cosmos DB 帳戶，建立使用 hello 資料總管 中，資料表及執行應用程式。  現在您可以查詢資料，可使用 hello 表格 API。  

> [!div class="nextstepaction"]
> [查詢使用 hello 表格 API](tutorial-query-table.md)

