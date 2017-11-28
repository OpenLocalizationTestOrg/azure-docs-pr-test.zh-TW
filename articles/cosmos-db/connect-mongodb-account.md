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
# <a name="connect-a-mongodb-application-tooazure-cosmos-db"></a><span data-ttu-id="1bb52-104">連接 MongoDB 應用程式 tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1bb52-104">Connect a MongoDB application tooAzure Cosmos DB</span></span>
<span data-ttu-id="1bb52-105">了解如何 tooconnect 您 MongoDB 應用程式 tooan Azure Cosmos DB 帳戶使用 MongoDB 連接字串。</span><span class="sxs-lookup"><span data-stu-id="1bb52-105">Learn how tooconnect your MongoDB app tooan Azure Cosmos DB account by using a MongoDB connection string.</span></span> <span data-ttu-id="1bb52-106">您接著可以在 hello 資料來使用 Azure Cosmos DB 資料庫儲存 MongoDB 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1bb52-106">You can then use an Azure Cosmos DB database as hello data store for your MongoDB app.</span></span> 

<span data-ttu-id="1bb52-107">本教學課程提供兩種方式 tooretrieve 連接字串資訊：</span><span class="sxs-lookup"><span data-stu-id="1bb52-107">This tutorial provides two ways tooretrieve connection string information:</span></span>

- <span data-ttu-id="1bb52-108">[hello 快速入門方法](#QuickstartConnection)，.NET、 Node.js、 MongoDB 殼層、 Java 和 Python 的驅動程式搭配使用</span><span class="sxs-lookup"><span data-stu-id="1bb52-108">[hello quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers</span></span>
- <span data-ttu-id="1bb52-109">[hello 自訂連接字串方法](#GetCustomConnection)，用於其他驅動程式</span><span class="sxs-lookup"><span data-stu-id="1bb52-109">[hello custom connection string method](#GetCustomConnection), for use with other drivers</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1bb52-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="1bb52-110">Prerequisites</span></span>

- <span data-ttu-id="1bb52-111">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1bb52-111">An Azure account.</span></span> <span data-ttu-id="1bb52-112">如果您沒有 Azure 帳戶，可以立即建立一個[免費的 Azure 帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="1bb52-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span></span> 
- <span data-ttu-id="1bb52-113">Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1bb52-113">An Azure Cosmos DB account.</span></span> <span data-ttu-id="1bb52-114">如需指示，請參閱[建置 MongoDB API web 應用程式的.NET 和 hello Azure 入口網站](create-mongodb-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="1bb52-114">For instructions, see [Build a MongoDB API web app with .NET and hello Azure portal](create-mongodb-dotnet.md).</span></span>

## <span data-ttu-id="1bb52-115"><a id="QuickstartConnection"></a>取得 hello MongoDB 連接字串使用 hello 快速入門</span><span class="sxs-lookup"><span data-stu-id="1bb52-115"><a id="QuickstartConnection"></a>Get hello MongoDB connection string by using hello quick start</span></span>
1. <span data-ttu-id="1bb52-116">在網際網路瀏覽器中登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="1bb52-116">In an Internet browser, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1bb52-117">在 hello **Azure Cosmos DB**刀鋒視窗中，選取 hello API MongoDB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1bb52-117">In hello **Azure Cosmos DB** blade, select hello API for MongoDB account.</span></span> 
3. <span data-ttu-id="1bb52-118">Hello 左窗格中的 hello 帳戶] 刀鋒視窗，按一下 [**快速入門**。</span><span class="sxs-lookup"><span data-stu-id="1bb52-118">In hello left pane of hello account blade, click **Quick start**.</span></span> 
4. <span data-ttu-id="1bb52-119">選擇您的平台 (**.NET**、**Node.js**、**MongoDB 殼層**、**Java**、**Python**)。</span><span class="sxs-lookup"><span data-stu-id="1bb52-119">Choose your platform (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span></span> <span data-ttu-id="1bb52-120">如果您沒有看到您的驅動程式或工具被列出，別擔心，我們會持續加入更多連線程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="1bb52-120">If you don't see your driver or tool listed, don't worry--we continuously document more connection code snippets.</span></span> <span data-ttu-id="1bb52-121">請在您想要的註解以下 toosee。</span><span class="sxs-lookup"><span data-stu-id="1bb52-121">Please comment below on what you'd like toosee.</span></span> <span data-ttu-id="1bb52-122">toolearn toocraft 您自己的連線，讀取方式[取得 hello 帳戶連接字串資訊](#GetCustomConnection)。</span><span class="sxs-lookup"><span data-stu-id="1bb52-122">toolearn how toocraft your own connection, read [Get hello account's connection string information](#GetCustomConnection).</span></span>
5. <span data-ttu-id="1bb52-123">複製並貼入 MongoDB 應用程式中的 hello 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="1bb52-123">Copy and paste hello code snippet into your MongoDB app.</span></span>

    ![快速入門刀鋒視窗](./media/connect-mongodb-account/QuickStartBlade.png)

## <span data-ttu-id="1bb52-125"><a id="GetCustomConnection"></a>取得 hello MongoDB 連接字串 toocustomize</span><span class="sxs-lookup"><span data-stu-id="1bb52-125"><a id="GetCustomConnection"></a> Get hello MongoDB connection string toocustomize</span></span>
1. <span data-ttu-id="1bb52-126">在網際網路瀏覽器中登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="1bb52-126">In an Internet browser, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1bb52-127">在 hello **Azure Cosmos DB**刀鋒視窗中，選取 hello API MongoDB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="1bb52-127">In hello **Azure Cosmos DB** blade, select hello API for MongoDB account.</span></span> 
3. <span data-ttu-id="1bb52-128">Hello 左窗格中的 hello 帳戶] 刀鋒視窗，按一下 [**連接字串**。</span><span class="sxs-lookup"><span data-stu-id="1bb52-128">In hello left pane of hello account blade, click **Connection String**.</span></span> 
4. <span data-ttu-id="1bb52-129">hello**連接字串**刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="1bb52-129">hello **Connection String** blade opens.</span></span> <span data-ttu-id="1bb52-130">它會有所有 hello 資訊必要 tooconnect toohello 帳戶使用 MongoDB，包括 preconstructed 的連接字串的驅動程式。</span><span class="sxs-lookup"><span data-stu-id="1bb52-130">It has all hello information necessary tooconnect toohello account by using a driver for MongoDB, including a preconstructed connection string.</span></span>

    ![[連接字串] 刀鋒視窗](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a><span data-ttu-id="1bb52-132">連接字串需求</span><span class="sxs-lookup"><span data-stu-id="1bb52-132">Connection string requirements</span></span>
> [!Important]
> <span data-ttu-id="1bb52-133">Azure Cosmos DB 有嚴格的安全性需求和標準。</span><span class="sxs-lookup"><span data-stu-id="1bb52-133">Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="1bb52-134">Azure Cosmos DB 帳戶需要驗證和透過 *SSL* 的安全通訊。</span><span class="sxs-lookup"><span data-stu-id="1bb52-134">Azure Cosmos DB accounts require authentication and secure communication via *SSL*.</span></span> 
>
>

<span data-ttu-id="1bb52-135">Azure Cosmos DB 支援 hello 標準 MongoDB 連接字串的 URI 格式的幾個特定的需求： Azure Cosmos DB 帳戶需要驗證，並且透過 SSL 的安全通訊。</span><span class="sxs-lookup"><span data-stu-id="1bb52-135">Azure Cosmos DB supports hello standard MongoDB connection string URI format, with a couple of specific requirements: Azure Cosmos DB accounts require authentication and secure communication via SSL.</span></span> <span data-ttu-id="1bb52-136">因此，hello 連接字串格式如下：</span><span class="sxs-lookup"><span data-stu-id="1bb52-136">So, hello connection string format is:</span></span>

    mongodb://username:password@host:port/[database]?ssl=true

<span data-ttu-id="1bb52-137">hello 值，這個字串的則可以在 hello**連接字串**刀鋒視窗中稍早所示：</span><span class="sxs-lookup"><span data-stu-id="1bb52-137">hello values of this string are available in hello **Connection String** blade shown earlier:</span></span>

* <span data-ttu-id="1bb52-138">使用者名稱 (必要)：Azure Cosmos DB 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="1bb52-138">Username (required): Azure Cosmos DB account name.</span></span>
* <span data-ttu-id="1bb52-139">密碼 (必要)：Azure Cosmos DB 帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="1bb52-139">Password (required): Azure Cosmos DB account password.</span></span>
* <span data-ttu-id="1bb52-140">主機 （必要）： hello Azure Cosmos DB 帳戶的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="1bb52-140">Host (required): FQDN of hello Azure Cosmos DB account.</span></span>
* <span data-ttu-id="1bb52-141">連接埠 (必要)：10255。</span><span class="sxs-lookup"><span data-stu-id="1bb52-141">Port (required): 10255.</span></span>
* <span data-ttu-id="1bb52-142">資料庫 （選擇性）： hello 連線的 hello 資料庫使用。</span><span class="sxs-lookup"><span data-stu-id="1bb52-142">Database (optional): hello database that hello connection uses.</span></span> <span data-ttu-id="1bb52-143">如果未不提供任何資料庫，則 hello 預設資料庫是 「 測試 」。</span><span class="sxs-lookup"><span data-stu-id="1bb52-143">If no database is provided, hello default database is "test."</span></span>
* <span data-ttu-id="1bb52-144">ssl=true (必要)</span><span class="sxs-lookup"><span data-stu-id="1bb52-144">ssl=true (required)</span></span>

<span data-ttu-id="1bb52-145">例如，請考慮 hello 帳戶顯示 hello**連接字串**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1bb52-145">For example, consider hello account shown in hello **Connection String** blade.</span></span> <span data-ttu-id="1bb52-146">有效的連接字串為：</span><span class="sxs-lookup"><span data-stu-id="1bb52-146">A valid connection string is:</span></span>

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a><span data-ttu-id="1bb52-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1bb52-147">Next steps</span></span>
* <span data-ttu-id="1bb52-148">了解如何太[使用 MongoChef](mongodb-mongochef.md)使用 MongoDB 帳戶 Azure Cosmos DB API。</span><span class="sxs-lookup"><span data-stu-id="1bb52-148">Learn how too[use MongoChef](mongodb-mongochef.md) with an Azure Cosmos DB API for MongoDB account.</span></span>
* <span data-ttu-id="1bb52-149">藉由檢視探索 MongoDB hello Azure Cosmos DB API[範例](mongodb-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="1bb52-149">Explore hello Azure Cosmos DB API for MongoDB by viewing [samples](mongodb-samples.md).</span></span>
