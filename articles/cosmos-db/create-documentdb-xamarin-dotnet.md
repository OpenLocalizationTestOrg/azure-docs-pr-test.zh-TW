---
title: "Azure CosmosDB︰使用 Xamarin 和 Facebook 驗證建置 Web 應用程式 | Microsoft Docs"
description: "提供.NET 程式碼範例中，您可以使用 tooconnect tooand 查詢 Azure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 5f71dddd2b2f5bd117e481c96c17915fc58d2119
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-web-app-with-net-xamarin-and-facebook-authentication"></a>Azure CosmosDB︰使用 .NET、Xamarin 和 Facebook 驗證建置 Web 應用程式

Azure Cosmos DB 是 Microsoft 的全域分散式多模型資料庫服務。 您可以快速建立與查詢文件、 索引鍵/值，以及 graph 資料庫，全部都是從 hello 全域發佈和核心 Azure Cosmos DB hello 的水平縮放功能獲益。 

本快速入門示範如何 toocreate Azure Cosmos DB 帳戶、 文件的資料庫，以及集合使用 hello Azure 入口網站。 然後會建置並部署 hello 上建置 todo 清單 web 應用程式[DocumentDB.NET API](documentdb-sdk-dotnet.md)， [Xamarin](https://www.xamarin.com/)，和 hello Azure Cosmos DB 授權引擎。 hello todo 清單 web 應用程式實作每個使用者資料的模式，可讓使用者使用 Facebook 驗證的 toologin 和管理他們自己 toodo 項目。

## <a name="prerequisites"></a>必要條件

如果您還沒有安裝 Visual Studio 2017，您可以下載並使用 hello**可用** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)。 請確定您啟用**Azure 開發**hello Visual Studio 安裝期間。

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>建立資料庫帳戶

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>新增集合

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>複製 hello 範例應用程式

現在讓我們從 github，複製 DocumentDB API 應用程式設定 hello 連接字串，並執行它。 您會看到是多麼的輕鬆 toowork 資料以程式設計的方式。 

1. 開啟 git 終端機視窗，例如 git bash 和`cd`tooa 工作目錄。  

2. 執行下列命令 tooclone hello 範例儲存機制的 hello。 

    ```bash
    git clone https://github.com/Azure/azure-documentdb-dotnet.git
    ```

3. 從 Visual Studio 中的 hello samples/xamarin/UserItems/xamarin.forms 資料夾，然後開啟 hello DocumentDBTodo.sln 檔案。 

## <a name="review-hello-code"></a>檢閱 hello 程式碼

hello hello Xamarin 資料夾中的程式碼包含：

* Xamarin 應用程式。 hello 應用程式儲存在名為 UserItems 的分割區集合中的 hello 使用者的 todo 項目。
* 資源權杖訊息代理程式 API。 簡單的 ASP.NET Web API toobroker Azure Cosmos DB 資源語彙基元 toohello 登入的 hello 應用程式的使用者。 資源語彙基元是存留較短的存取權杖，hello 應用程式提供 hello 存取 toohello 登入使用者的資料。

hello 驗證和資料流程以 hello 如下圖所示。

* hello UserItems 集合會透過 hello 資料分割索引鍵 ' / userid'。 指定集合的資料分割索引鍵可讓 Azure Cosmos DB tooscale 無限 hello 數字的使用者和項目會成長。
* hello Xamarin 應用程式可讓使用者 toologin 使用 Facebook 的認證。
* hello Xamarin 應用程式使用 Facebook 存取權杖 tooauthenticate 具有 ResourceTokenBroker 應用程式開發介面
* hello 資源語彙基元 broker API 驗證 hello 要求使用應用程式服務驗證功能，並要求 Azure Cosmos DB 資源權杖的讀取/寫入存取 tooall 文件共用 hello 經驗證的使用者資料分割索引鍵。
* 資源語彙基元 broker 傳回 hello 資源語彙基元 toohello 用戶端應用程式。
* hello 應用程式存取使用 hello 資源語彙基元的 hello 使用者的 todo 項目。

![具有範例資料的待辦事項應用程式](./media/create-documentdb-xamarin-dotnet/tokenbroker.png)
    
## <a name="update-your-connection-string"></a>更新您的連接字串

現在請返回 Azure 入口網站 tooget toohello 您的連接字串資訊並將它複製到 hello 應用程式。

1. 在 hello [Azure 入口網站](http://portal.azure.com/)，在您的 Azure Cosmos DB 帳戶，在左瀏覽的 hello 按一下**金鑰**，然後按一下**讀寫金鑰**。 您將使用 hello 複製按鈕右邊 hello hello 螢幕 toocopy hello URI 和主索引鍵到 hello hello 下一個步驟中的 Web.config 檔案。

    ![檢視及複製 hello Azure 入口網站中的存取金鑰，金鑰刀鋒視窗](./media/create-documentdb-xamarin-dotnet/keys.png)

2. 在 Visual Studio 2017，開啟 hello hello azure-documentdb-dotnet/範例/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker 資料夾中的 Web.config 檔案。 

3. 從 hello （使用 hello [複製] 按鈕） 的入口網站複製 URI 值，並讓它 hello hello accountUrl Web.config 中的值。 

    `<add key="accountUrl" value="{Azure Cosmos DB account URL}"/>`

4. 然後從 hello 入口網站複製您的主索引鍵的值，並讓它 hello hello accountKey Web.congif 中的值。 

    `<add key="accountKey" value="{Azure Cosmos DB secret}"/>`

您現在已更新您的應用程式與它需要與 Azure Cosmos DB toocommunicate 所有 hello 資訊。 

## <a name="build-and-deploy-hello-web-app"></a>建置和部署 hello web 應用程式

1. 在 hello Azure 入口網站，建立應用程式服務網站 toohost hello 資源語彙基元 broker 應用程式開發介面。
2. 在 hello Azure 入口網站，開啟 hello hello 資源語彙基元 broker API 網站的 應用程式設定 刀鋒視窗。 填寫下列應用程式設定的 hello:

    * accountUrl-hello Azure Cosmos DB 帳戶 URL 從您的 Azure Cosmos DB 帳戶 hello 金鑰 索引標籤。
    * accountKey-hello Azure Cosmos DB 帳戶從您的 Azure Cosmos DB 帳戶 hello 金鑰 索引標籤的主要金鑰。
    * 已建立之資料庫和集合的 databaseId 和 collectionId

3. 發行 hello ResourceTokenBroker 方案 tooyour 建立網站。

4. 開啟 hello Xamarin 專案，並瀏覽 tooTodoItemManager.cs。 填寫 accountURL、 collectionId、 databaseId，以及 resourceTokenBrokerURL hello 值為 hello 資源語彙基元 broker 網站 hello 基底的 https url。

5. 完整的 hello[如何 tooconfigure 您 App Service 應用程式 toouse Facebook 登入](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md)教學課程 toosetup Facebook 驗證和設定 hello ResourceTokenBroker 網站。

    執行 hello Xamarin 應用程式。

## <a name="review-slas-in-hello-azure-portal"></a>在 hello Azure 入口網站中檢視 Sla

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>清除資源

如果您不打算 toocontinue toouse 此應用程式，刪除所有資源本快速入門以建立 hello Azure 入口網站以 hello 下列步驟： 

1. Hello Azure 入口網站中的 hello 左側功能表中按一下**資源群組**，然後按一下您剛才建立的 hello 資源的 hello 名稱。 
2. 在資源群組頁面上，按一下 **刪除**，在 hello 文字方塊中，輸入 hello 資源 toodelete hello 名稱，然後按一下**刪除**。

## <a name="next-steps"></a>後續步驟

本快速入門中，您已經學會 toocreate Azure Cosmos DB 帳戶，建立集合，使用 hello 資料總管和建置和部署的 Xamarin 應用程式的方式。 您現在可以匯入的其他資料 tooyour Cosmos DB 帳戶。 

> [!div class="nextstepaction"]
> [將資料匯入到 Azure Cosmos DB](import-data.md)
