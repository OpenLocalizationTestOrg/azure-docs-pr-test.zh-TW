---
title: "Azure Cosmos DB 帳戶的 MongoDB 連接字串 | Microsoft Docs"
description: "了解如何使用 MongoDB 連接字串，將 MongoDB 應用程式連線至 Azure Cosmos DB 帳戶。"
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
ms.openlocfilehash: 5a47001705531d971d3181df9c0aa8f957168845
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-mongodb-application-to-azure-cosmos-db"></a><span data-ttu-id="f740d-104">將 MongoDB 應用程式連接到 Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f740d-104">Connect a MongoDB application to Azure Cosmos DB</span></span>
<span data-ttu-id="f740d-105">了解如何使用 MongoDB 連接字串，將 MongoDB 應用程式連線至 Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f740d-105">Learn how to connect your MongoDB app to an Azure Cosmos DB account by using a MongoDB connection string.</span></span> <span data-ttu-id="f740d-106">您可以使用 Azure Cosmos DB 資料庫作為 MongoDB 應用程式的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="f740d-106">You can then use an Azure Cosmos DB database as the data store for your MongoDB app.</span></span> 

<span data-ttu-id="f740d-107">本教學課程提供兩種方式來擷取連接字串資訊︰</span><span class="sxs-lookup"><span data-stu-id="f740d-107">This tutorial provides two ways to retrieve connection string information:</span></span>

- <span data-ttu-id="f740d-108">[快速啟動方法](#QuickstartConnection)，用來搭配 .NET、Node.js、MongoDB 殼層、Java 和 Python 驅動程式</span><span class="sxs-lookup"><span data-stu-id="f740d-108">[The quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers</span></span>
- <span data-ttu-id="f740d-109">[自訂連接字串方法](#GetCustomConnection)，用來搭配其他驅動程式</span><span class="sxs-lookup"><span data-stu-id="f740d-109">[The custom connection string method](#GetCustomConnection), for use with other drivers</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f740d-110">必要條件</span><span class="sxs-lookup"><span data-stu-id="f740d-110">Prerequisites</span></span>

- <span data-ttu-id="f740d-111">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f740d-111">An Azure account.</span></span> <span data-ttu-id="f740d-112">如果您沒有 Azure 帳戶，可以立即建立一個[免費的 Azure 帳戶](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="f740d-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span></span> 
- <span data-ttu-id="f740d-113">Azure Cosmos DB 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f740d-113">An Azure Cosmos DB account.</span></span> <span data-ttu-id="f740d-114">如需相關指示，請參閱[使用 .NET 和 Azure 入口網站建置 MongoDB API Web 應用程式](create-mongodb-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="f740d-114">For instructions, see [Build a MongoDB API web app with .NET and the Azure portal](create-mongodb-dotnet.md).</span></span>

## <span data-ttu-id="f740d-115"><a id="QuickstartConnection"></a>使用快速入門取得 MongoDB 連接字串</span><span class="sxs-lookup"><span data-stu-id="f740d-115"><a id="QuickstartConnection"></a>Get the MongoDB connection string by using the quick start</span></span>
1. <span data-ttu-id="f740d-116">在網際網路瀏覽器中，登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f740d-116">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f740d-117">在 [Azure Cosmos DB] 刀鋒視窗中，選取 MongoDB 帳戶的 API。</span><span class="sxs-lookup"><span data-stu-id="f740d-117">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span></span> 
3. <span data-ttu-id="f740d-118">在帳戶刀鋒視窗的左窗格中，按一下 [快速入門]。</span><span class="sxs-lookup"><span data-stu-id="f740d-118">In the left pane of the account blade, click **Quick start**.</span></span> 
4. <span data-ttu-id="f740d-119">選擇您的平台 (**.NET**、**Node.js**、**MongoDB 殼層**、**Java**、**Python**)。</span><span class="sxs-lookup"><span data-stu-id="f740d-119">Choose your platform (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span></span> <span data-ttu-id="f740d-120">如果您沒有看到您的驅動程式或工具被列出，別擔心，我們會持續加入更多連線程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="f740d-120">If you don't see your driver or tool listed, don't worry--we continuously document more connection code snippets.</span></span> <span data-ttu-id="f740d-121">請在下面加入您想要看到何種內容的意見。</span><span class="sxs-lookup"><span data-stu-id="f740d-121">Please comment below on what you'd like to see.</span></span> <span data-ttu-id="f740d-122">若要了解如何製作您自己的連線，請閱讀[取得帳戶的連接字串資訊](#GetCustomConnection)。</span><span class="sxs-lookup"><span data-stu-id="f740d-122">To learn how to craft your own connection, read [Get the account's connection string information](#GetCustomConnection).</span></span>
5. <span data-ttu-id="f740d-123">將程式碼片段複製和貼上您的 MongoDB 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f740d-123">Copy and paste the code snippet into your MongoDB app.</span></span>

    ![快速入門刀鋒視窗](./media/connect-mongodb-account/QuickStartBlade.png)

## <span data-ttu-id="f740d-125"><a id="GetCustomConnection"></a> 取得 MongoDB 連接字串以自訂</span><span class="sxs-lookup"><span data-stu-id="f740d-125"><a id="GetCustomConnection"></a> Get the MongoDB connection string to customize</span></span>
1. <span data-ttu-id="f740d-126">在網際網路瀏覽器中，登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="f740d-126">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f740d-127">在 [Azure Cosmos DB] 刀鋒視窗中，選取 MongoDB 帳戶的 API。</span><span class="sxs-lookup"><span data-stu-id="f740d-127">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span></span> 
3. <span data-ttu-id="f740d-128">在帳戶刀鋒視窗的左窗格中，按一下 [連接字串]。</span><span class="sxs-lookup"><span data-stu-id="f740d-128">In the left pane of the account blade, click **Connection String**.</span></span> 
4. <span data-ttu-id="f740d-129">[連接字串] 刀鋒視窗隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="f740d-129">The **Connection String** blade opens.</span></span> <span data-ttu-id="f740d-130">其中包含使用 MongoDB 適用的驅動程式連線至帳戶所需的所有資訊，包括預先建構的連接字串。</span><span class="sxs-lookup"><span data-stu-id="f740d-130">It has all the information necessary to connect to the account by using a driver for MongoDB, including a preconstructed connection string.</span></span>

    ![連接字串刀鋒視窗](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a><span data-ttu-id="f740d-132">連接字串需求</span><span class="sxs-lookup"><span data-stu-id="f740d-132">Connection string requirements</span></span>
> [!Important]
> <span data-ttu-id="f740d-133">Azure Cosmos DB 有嚴格的安全性需求和標準。</span><span class="sxs-lookup"><span data-stu-id="f740d-133">Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="f740d-134">Azure Cosmos DB 帳戶需要驗證和透過 *SSL* 的安全通訊。</span><span class="sxs-lookup"><span data-stu-id="f740d-134">Azure Cosmos DB accounts require authentication and secure communication via *SSL*.</span></span> 
>
>

<span data-ttu-id="f740d-135">Azure Cosmos DB 支援標準 MongoDB 連接字串 URI 格式，有幾個特定需求︰Azure Cosmos DB 帳戶需要驗證和透過 SSL 的安全通訊。</span><span class="sxs-lookup"><span data-stu-id="f740d-135">Azure Cosmos DB supports the standard MongoDB connection string URI format, with a couple of specific requirements: Azure Cosmos DB accounts require authentication and secure communication via SSL.</span></span> <span data-ttu-id="f740d-136">所以，連接字串格式為：</span><span class="sxs-lookup"><span data-stu-id="f740d-136">So, the connection string format is:</span></span>

    mongodb://username:password@host:port/[database]?ssl=true

<span data-ttu-id="f740d-137">在先前顯示的 [連接字串] 刀鋒視窗中可取得此字串的值：</span><span class="sxs-lookup"><span data-stu-id="f740d-137">The values of this string are available in the **Connection String** blade shown earlier:</span></span>

* <span data-ttu-id="f740d-138">使用者名稱 (必要)：Azure Cosmos DB 帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="f740d-138">Username (required): Azure Cosmos DB account name.</span></span>
* <span data-ttu-id="f740d-139">密碼 (必要)：Azure Cosmos DB 帳戶密碼。</span><span class="sxs-lookup"><span data-stu-id="f740d-139">Password (required): Azure Cosmos DB account password.</span></span>
* <span data-ttu-id="f740d-140">主機 (必要)：Azure Cosmos DB 帳戶的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="f740d-140">Host (required): FQDN of the Azure Cosmos DB account.</span></span>
* <span data-ttu-id="f740d-141">連接埠 (必要)：10255。</span><span class="sxs-lookup"><span data-stu-id="f740d-141">Port (required): 10255.</span></span>
* <span data-ttu-id="f740d-142">資料庫 (選用)：連線所使用的資料庫。</span><span class="sxs-lookup"><span data-stu-id="f740d-142">Database (optional): The database that the connection uses.</span></span> <span data-ttu-id="f740d-143">如果未提供資料庫，則預設資料庫是 "test"。</span><span class="sxs-lookup"><span data-stu-id="f740d-143">If no database is provided, the default database is "test."</span></span>
* <span data-ttu-id="f740d-144">ssl=true (必要)</span><span class="sxs-lookup"><span data-stu-id="f740d-144">ssl=true (required)</span></span>

<span data-ttu-id="f740d-145">例如，請考慮 [連接字串] 刀鋒視窗中顯示的帳戶。</span><span class="sxs-lookup"><span data-stu-id="f740d-145">For example, consider the account shown in the **Connection String** blade.</span></span> <span data-ttu-id="f740d-146">有效的連接字串為：</span><span class="sxs-lookup"><span data-stu-id="f740d-146">A valid connection string is:</span></span>

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a><span data-ttu-id="f740d-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f740d-147">Next steps</span></span>
* <span data-ttu-id="f740d-148">了解如何[使用 MongoChef](mongodb-mongochef.md) 搭配 Azure Cosmos DB：適用於 MongoDB 的 API 帳戶</span><span class="sxs-lookup"><span data-stu-id="f740d-148">Learn how to [use MongoChef](mongodb-mongochef.md) with an Azure Cosmos DB API for MongoDB account.</span></span>
* <span data-ttu-id="f740d-149">檢視[範例](mongodb-samples.md)，以瀏覽 MongoDB 適用的 Azure Cosmos DB API。</span><span class="sxs-lookup"><span data-stu-id="f740d-149">Explore the Azure Cosmos DB API for MongoDB by viewing [samples](mongodb-samples.md).</span></span>
