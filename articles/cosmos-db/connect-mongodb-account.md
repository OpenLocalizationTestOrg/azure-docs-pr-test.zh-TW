---
title: "aaaMongoDB Azure Cosmos DB 帳戶的連接字串 |Microsoft 文件"
description: "了解如何 tooconnect 您 MongoDB 應用程式 tooan Azure Cosmos DB 帳戶使用 MongoDB 連接字串。"
keywords: "mongodb 連接字串"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: e36f7375-9329-403b-afd1-4ab49894f75e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.openlocfilehash: c0b81cb49a10e09e3f02411b91731c7f980ec47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-mongodb-application-tooazure-cosmos-db"></a>連接 MongoDB 應用程式 tooAzure Cosmos DB
了解如何 tooconnect 您 MongoDB 應用程式 tooan Azure Cosmos DB 帳戶使用 MongoDB 連接字串。 您接著可以在 hello 資料來使用 Azure Cosmos DB 資料庫儲存 MongoDB 應用程式。 

本教學課程提供兩種方式 tooretrieve 連接字串資訊：

- [hello 快速入門方法](#QuickstartConnection)，.NET、 Node.js、 MongoDB 殼層、 Java 和 Python 的驅動程式搭配使用
- [hello 自訂連接字串方法](#GetCustomConnection)，用於其他驅動程式

## <a name="prerequisites"></a>必要條件

- 一個 Azure 帳戶。 如果您沒有 Azure 帳戶，可以立即建立一個[免費的 Azure 帳戶](https://azure.microsoft.com/free/)。 
- Azure Cosmos DB 帳戶。 如需指示，請參閱[建置 MongoDB API web 應用程式的.NET 和 hello Azure 入口網站](create-mongodb-dotnet.md)。

## <a id="QuickstartConnection"></a>取得 hello MongoDB 連接字串使用 hello 快速入門
1. 在網際網路瀏覽器中登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello **Azure Cosmos DB**刀鋒視窗中，選取 hello API MongoDB 帳戶。 
3. Hello 左窗格中的 hello 帳戶] 刀鋒視窗，按一下 [**快速入門**。 
4. 選擇您的平台 (**.NET**、**Node.js**、**MongoDB 殼層**、**Java**、**Python**)。 如果您沒有看到您的驅動程式或工具被列出，別擔心，我們會持續加入更多連線程式碼片段。 請在您想要的註解以下 toosee。 toolearn toocraft 您自己的連線，讀取方式[取得 hello 帳戶連接字串資訊](#GetCustomConnection)。
5. 複製並貼入 MongoDB 應用程式中的 hello 程式碼片段。

    ![快速入門刀鋒視窗](./media/connect-mongodb-account/QuickStartBlade.png)

## <a id="GetCustomConnection"></a>取得 hello MongoDB 連接字串 toocustomize
1. 在網際網路瀏覽器中登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 在 hello **Azure Cosmos DB**刀鋒視窗中，選取 hello API MongoDB 帳戶。 
3. Hello 左窗格中的 hello 帳戶] 刀鋒視窗，按一下 [**連接字串**。 
4. hello**連接字串**刀鋒視窗隨即開啟。 它會有所有 hello 資訊必要 tooconnect toohello 帳戶使用 MongoDB，包括 preconstructed 的連接字串的驅動程式。

    ![[連接字串] 刀鋒視窗](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a>連接字串需求
> [!Important]
> Azure Cosmos DB 有嚴格的安全性需求和標準。 Azure Cosmos DB 帳戶需要驗證和透過 *SSL* 的安全通訊。 
>
>

Azure Cosmos DB 支援 hello 標準 MongoDB 連接字串的 URI 格式的幾個特定的需求： Azure Cosmos DB 帳戶需要驗證，並且透過 SSL 的安全通訊。 因此，hello 連接字串格式如下：

    mongodb://username:password@host:port/[database]?ssl=true

hello 值，這個字串的則可以在 hello**連接字串**刀鋒視窗中稍早所示：

* 使用者名稱 (必要)：Azure Cosmos DB 帳戶名稱。
* 密碼 (必要)：Azure Cosmos DB 帳戶密碼。
* 主機 （必要）： hello Azure Cosmos DB 帳戶的 FQDN。
* 連接埠 (必要)：10255。
* 資料庫 （選擇性）： hello 連線的 hello 資料庫使用。 如果未不提供任何資料庫，則 hello 預設資料庫是 「 測試 」。
* ssl=true (必要)

例如，請考慮 hello 帳戶顯示 hello**連接字串**刀鋒視窗。 有效的連接字串為：

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a>後續步驟
* 了解如何太[使用 MongoChef](mongodb-mongochef.md)使用 MongoDB 帳戶 Azure Cosmos DB API。
* 藉由檢視探索 MongoDB hello Azure Cosmos DB API[範例](mongodb-samples.md)。
