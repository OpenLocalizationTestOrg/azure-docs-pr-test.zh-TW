---
title: "使用 mongoimport 和 mongorestore 搭配適用於 MongoDB 的 Azure Cosmos DB API | Microsoft Docs"
description: "了解如何使用 mongoimport 和 mongorestore 將資料匯入適用於 MongoDB 的 API 帳戶"
keywords: mongoimport, mongorestore
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
ms.date: 06/12/2017
ms.author: anhoh
ms.custom: mvc
ms.openlocfilehash: 1555f13c3ea88b61be0ea240b51218b83f6f9724
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-import-mongodb-data"></a><span data-ttu-id="41b20-104">Azure Cosmos DB：匯入 MongoDB 資料</span><span class="sxs-lookup"><span data-stu-id="41b20-104">Azure Cosmos DB: Import MongoDB data</span></span> 

<span data-ttu-id="41b20-105">若要將資料從 MongoDB 移轉至 Azure Cosmos DB 帳戶以用於 MongoDB 所適用的 API，您必須︰</span><span class="sxs-lookup"><span data-stu-id="41b20-105">To migrate data from MongoDB to an Azure Cosmos DB account for use with the API for MongoDB, you must:</span></span>

* <span data-ttu-id="41b20-106">從 [MongoDB 下載中心](https://www.mongodb.com/download-center)下載 *mongoimport.exe* 或*mongorestore.exe*。</span><span class="sxs-lookup"><span data-stu-id="41b20-106">Download either *mongoimport.exe* or *mongorestore.exe* from the [MongoDB Download Center](https://www.mongodb.com/download-center).</span></span>
* <span data-ttu-id="41b20-107">取得[適用於 MongoDB 的 API 連接字串](connect-mongodb-account.md)。</span><span class="sxs-lookup"><span data-stu-id="41b20-107">Get your [API for MongoDB connection string](connect-mongodb-account.md).</span></span>

<span data-ttu-id="41b20-108">如果您從 MongoDB 匯入資料，而且想要將這些資料用於 Azure Cosmos DB，則必須使用[資料移轉工具](import-data.md)匯入資料。</span><span class="sxs-lookup"><span data-stu-id="41b20-108">If you are importing data from MongoDB and plan to use it with the Azure Cosmos DB, you should use the [Data Migration tool](import-data.md) to import data.</span></span>

<span data-ttu-id="41b20-109">本教學課程涵蓋下列工作：</span><span class="sxs-lookup"><span data-stu-id="41b20-109">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="41b20-110">擷取連接字串</span><span class="sxs-lookup"><span data-stu-id="41b20-110">Retrieving your connection string</span></span>
> * <span data-ttu-id="41b20-111">使用 mongoimport 匯入 MongoDB 資料</span><span class="sxs-lookup"><span data-stu-id="41b20-111">Importing MongoDB data by using mongoimport</span></span>
> * <span data-ttu-id="41b20-112">使用 mongorestore 匯入 MongoDB 資料</span><span class="sxs-lookup"><span data-stu-id="41b20-112">Importing MongoDB data by using mongorestore</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41b20-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="41b20-113">Prerequisites</span></span>

* <span data-ttu-id="41b20-114">增加輸送量︰資料移轉的時間長短取決於您為集合設定的輸送量。</span><span class="sxs-lookup"><span data-stu-id="41b20-114">Increase throughput: The duration of your data migration depends on the amount of throughput you set up for your collections.</span></span> <span data-ttu-id="41b20-115">針對較大資料移轉，請務必增加輸送量。</span><span class="sxs-lookup"><span data-stu-id="41b20-115">Be sure to increase the throughput for larger data migrations.</span></span> <span data-ttu-id="41b20-116">完成移轉之後，再降低輸送量以節省成本。</span><span class="sxs-lookup"><span data-stu-id="41b20-116">After you've completed the migration, decrease the throughput to save costs.</span></span> <span data-ttu-id="41b20-117">如需在 [Azure 入口網站](https://portal.azure.com)增加輸送量的詳細資訊，請參閱 [Azure Cosmos DB 中的效能等級和定價層](performance-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="41b20-117">For more information about increasing throughput in the [Azure portal](https://portal.azure.com), see [Performance levels and pricing tiers in Azure Cosmos DB](performance-levels.md).</span></span>

* <span data-ttu-id="41b20-118">啟用 SSL：Azure Cosmos DB 有嚴格的安全性需求和標準。</span><span class="sxs-lookup"><span data-stu-id="41b20-118">Enable SSL: Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="41b20-119">與您的帳戶互動時，請務必啟用 SSL。</span><span class="sxs-lookup"><span data-stu-id="41b20-119">Be sure to enable SSL when you interact with your account.</span></span> <span data-ttu-id="41b20-120">本文其他部分的程序包括如何針對 mongoimport 和 mongorestore 啟用 SSL。</span><span class="sxs-lookup"><span data-stu-id="41b20-120">The procedures in the rest of the article include how to enable SSL for mongoimport and mongorestore.</span></span>

## <a name="find-your-connection-string-information-host-port-username-and-password"></a><span data-ttu-id="41b20-121">找到您的連接字串資訊 (主機、連接埠、使用者名稱、密碼)</span><span class="sxs-lookup"><span data-stu-id="41b20-121">Find your connection string information (host, port, username, and password)</span></span>

1. <span data-ttu-id="41b20-122">在 [Azure 入口網站](https://portal.azure.com)的左窗格中，按一下 [Azure Cosmos DB] 項目。</span><span class="sxs-lookup"><span data-stu-id="41b20-122">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Cosmos DB** entry.</span></span>
2. <span data-ttu-id="41b20-123">在 [訂用帳戶] 窗格中，選取您的帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="41b20-123">In the **Subscriptions** pane, select your account name.</span></span>
3. <span data-ttu-id="41b20-124">在 [連接字串] 刀鋒視窗中，按一下 [連接字串]。</span><span class="sxs-lookup"><span data-stu-id="41b20-124">In the **Connection String** blade, click **Connection String**.</span></span>  
<span data-ttu-id="41b20-125">右窗格中有您成功連接到您的帳戶所需的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="41b20-125">The right pane contains all the information that you need to successfully connect to your account.</span></span>

    ![[連接字串] 刀鋒視窗](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-to-the-api-for-mongodb-by-using-mongoimport"></a><span data-ttu-id="41b20-127">使用 mongoimport 將資料匯入適用於 MongoDB 的 API</span><span class="sxs-lookup"><span data-stu-id="41b20-127">Import data to the API for MongoDB by using mongoimport</span></span>

<span data-ttu-id="41b20-128">若要將資料匯入您的 Azure Cosmos DB 帳戶，請使用下列範本。</span><span class="sxs-lookup"><span data-stu-id="41b20-128">To import data to your Azure Cosmos DB account, use the following template.</span></span> <span data-ttu-id="41b20-129">填寫專屬於您的帳戶的 [主機]、[使用者名稱]、[密碼] 值。</span><span class="sxs-lookup"><span data-stu-id="41b20-129">Fill in *host*, *username*, and *password* with the values that are specific to your account.</span></span>  

<span data-ttu-id="41b20-130">範本：</span><span class="sxs-lookup"><span data-stu-id="41b20-130">Template:</span></span>

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

<span data-ttu-id="41b20-131">範例：</span><span class="sxs-lookup"><span data-stu-id="41b20-131">Example:</span></span>  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-to-the-api-for-mongodb-by-using-mongorestore"></a><span data-ttu-id="41b20-132">使用 mongorestore 將資料匯入適用於 MongoDB 的 API</span><span class="sxs-lookup"><span data-stu-id="41b20-132">Import data to the API for MongoDB by using mongorestore</span></span>

<span data-ttu-id="41b20-133">若要將資料還原至適用於 MongoDB 的 API 帳戶，請使用下列範本執行匯入。</span><span class="sxs-lookup"><span data-stu-id="41b20-133">To restore data to your API for MongoDB account, use the following template to execute the import.</span></span> <span data-ttu-id="41b20-134">填寫專屬於您的帳戶的 [主機]、[使用者名稱]、[密碼] 值。</span><span class="sxs-lookup"><span data-stu-id="41b20-134">Fill in *host*, *username*, and *password* with the values that are specific to your account.</span></span>

<span data-ttu-id="41b20-135">範本：</span><span class="sxs-lookup"><span data-stu-id="41b20-135">Template:</span></span>

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

<span data-ttu-id="41b20-136">範例：</span><span class="sxs-lookup"><span data-stu-id="41b20-136">Example:</span></span>

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a><span data-ttu-id="41b20-137">成功移轉的指南</span><span class="sxs-lookup"><span data-stu-id="41b20-137">Guide for a successful migration</span></span>

1. <span data-ttu-id="41b20-138">預先建立並調整您的集合：</span><span class="sxs-lookup"><span data-stu-id="41b20-138">Pre-create and scale your collections:</span></span>
        
    * <span data-ttu-id="41b20-139">根據預設，Azure Cosmos DB 會佈建含 1,000 個要求單位 (RU) 的新 MongoDB 集合。</span><span class="sxs-lookup"><span data-stu-id="41b20-139">By default, Azure Cosmos DB provisions a new MongoDB collection with 1,000 request units (RUs).</span></span> <span data-ttu-id="41b20-140">使用 mongoimport、mongorestore 或 mongomirror 開始移轉之前，請從 [Azure 入口網站](https://portal.azure.com)或 MongoDB 驅動程式與工具預先建立您的所有集合。</span><span class="sxs-lookup"><span data-stu-id="41b20-140">Before you start the migration by using mongoimport, mongorestore, or mongomirror, pre-create all your collections from the [Azure portal](https://portal.azure.com) or from MongoDB drivers and tools.</span></span> <span data-ttu-id="41b20-141">如果您的集合大於 10 GB，請務必使用適當的分區金鑰建立[分區/分割集合](partition-data.md)。</span><span class="sxs-lookup"><span data-stu-id="41b20-141">If your collection is greater than 10 GB, make sure to create a [sharded/partitioned collection](partition-data.md) with an appropriate shard key.</span></span>

    * <span data-ttu-id="41b20-142">在 [Azure 入口網站](https://portal.azure.com)，僅針對移轉來增加集合的輸送量，單一分割區集合從 1,000 RU 起，分區集合則從 2,500 RU 起。</span><span class="sxs-lookup"><span data-stu-id="41b20-142">From the [Azure portal](https://portal.azure.com), increase your collections' throughput from 1,000 RUs for a single partition collection and 2,500 RUs for a sharded collection just for the migration.</span></span> <span data-ttu-id="41b20-143">藉由較高的輸送量，您可以避免節流，並花費較少的時間進行移轉。</span><span class="sxs-lookup"><span data-stu-id="41b20-143">With the higher throughput, you can avoid throttling and migrate in less time.</span></span> <span data-ttu-id="41b20-144">由於 Azure Cosmos DB 是以每小時計費，所以您可以在移轉之後立即減少輸送量以節省成本。</span><span class="sxs-lookup"><span data-stu-id="41b20-144">With hourly billing in Azure Cosmos DB, you can reduce the throughput immediately after the migration to save costs.</span></span>

2. <span data-ttu-id="41b20-145">估算單一文件消耗的 RU：</span><span class="sxs-lookup"><span data-stu-id="41b20-145">Calculate the approximate RU charge for a single document write:</span></span>

    <span data-ttu-id="41b20-146">a.</span><span class="sxs-lookup"><span data-stu-id="41b20-146">a.</span></span> <span data-ttu-id="41b20-147">從 MongoDB 殼層連線到您的 Azure Cosmos DB MongoDB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="41b20-147">Connect to your Azure Cosmos DB MongoDB database from the MongoDB Shell.</span></span> <span data-ttu-id="41b20-148">您可以在[將 MongoDB 應用程式連接到 Azure Cosmos DB](connect-mongodb-account.md) 中找到指示。</span><span class="sxs-lookup"><span data-stu-id="41b20-148">You can find instructions in [Connect a MongoDB application to Azure Cosmos DB](connect-mongodb-account.md).</span></span>
    
    <span data-ttu-id="41b20-149">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="41b20-149">b.</span></span> <span data-ttu-id="41b20-150">從 MongoDB 殼層使用其中一個範例文件來執行範例插入命令：</span><span class="sxs-lookup"><span data-stu-id="41b20-150">Run a sample insert command by using one of your sample documents from the MongoDB Shell:</span></span>
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    <span data-ttu-id="41b20-151">c.</span><span class="sxs-lookup"><span data-stu-id="41b20-151">c.</span></span> <span data-ttu-id="41b20-152">執行 ```db.runCommand({getLastRequestStatistics: 1})```，您會收到如下的回應：</span><span class="sxs-lookup"><span data-stu-id="41b20-152">Run ```db.runCommand({getLastRequestStatistics: 1})``` and you will receive a response like this one:</span></span>
     
        ```
        globaldb:PRIMARY> db.runCommand({getLastRequestStatistics: 1})
        {
            "_t": "GetRequestStatisticsResponse",
            "ok": 1,
            "CommandName": "insert",
            "RequestCharge": 10,
            "RequestDurationInMilliSeconds": NumberLong(50)
        }
        ```
        
    <span data-ttu-id="41b20-153">d.</span><span class="sxs-lookup"><span data-stu-id="41b20-153">d.</span></span> <span data-ttu-id="41b20-154">記下要求費用。</span><span class="sxs-lookup"><span data-stu-id="41b20-154">Take note of the request charge.</span></span>
    
3. <span data-ttu-id="41b20-155">判斷從您的電腦到 Azure Cosmos DB 雲端服務的延遲：</span><span class="sxs-lookup"><span data-stu-id="41b20-155">Determine the latency from your machine to the Azure Cosmos DB cloud service:</span></span>
    
    <span data-ttu-id="41b20-156">a.</span><span class="sxs-lookup"><span data-stu-id="41b20-156">a.</span></span> <span data-ttu-id="41b20-157">從 MongoDB 殼層使用此命令，以啟用詳細資訊記錄：```setVerboseShell(true)```</span><span class="sxs-lookup"><span data-stu-id="41b20-157">Enable verbose logging from the MongoDB Shell by using this command: ```setVerboseShell(true)```</span></span>
    
    <span data-ttu-id="41b20-158">b.這是另一個 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="41b20-158">b.</span></span> <span data-ttu-id="41b20-159">對資料庫執行簡單的查詢：```db.coll.find().limit(1)```。</span><span class="sxs-lookup"><span data-stu-id="41b20-159">Run a simple query against the database: ```db.coll.find().limit(1)```.</span></span> <span data-ttu-id="41b20-160">您會收到如下的回應：</span><span class="sxs-lookup"><span data-stu-id="41b20-160">You will receive a response like this one:</span></span>

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. <span data-ttu-id="41b20-161">移轉之前請先移除插入的文件，以確保不會有重複的文件。</span><span class="sxs-lookup"><span data-stu-id="41b20-161">Remove the inserted document before the migration to ensure that there are no duplicate documents.</span></span> <span data-ttu-id="41b20-162">您可以使用此命令來移除文件：```db.coll.remove({})```</span><span class="sxs-lookup"><span data-stu-id="41b20-162">You can remove documents by using this command: ```db.coll.remove({})```</span></span>

5. <span data-ttu-id="41b20-163">估算 *batchSize* 和 *numInsertionWorkers* 值：</span><span class="sxs-lookup"><span data-stu-id="41b20-163">Calculate the approximate *batchSize* and *numInsertionWorkers* values:</span></span>

    * <span data-ttu-id="41b20-164">*batchSize* 的算法是將總佈建的 RU 數，除以步驟 3 中寫入單一文件所花費的 RU 數。</span><span class="sxs-lookup"><span data-stu-id="41b20-164">For *batchSize*, divide the total provisioned RUs by the RUs consumed from your single document write in step 3.</span></span>
    
    * <span data-ttu-id="41b20-165">如果算出的 *batchSize* <= 24，請使用該數字做為您的 *batchSize* 值。</span><span class="sxs-lookup"><span data-stu-id="41b20-165">If the calculated *batchSize* <= 24, use that number as your *batchSize* value.</span></span>
    
    * <span data-ttu-id="41b20-166">如果算出的 *batchSize* > 24，則將 *batchSize* 的值設為 24。</span><span class="sxs-lookup"><span data-stu-id="41b20-166">If the calculated *batchSize* > 24, set the *batchSize* value to 24.</span></span>
    
    * <span data-ttu-id="41b20-167">*numInsertionWorkers* 的算法是使用此方程式：*numInsertionWorkers =  (佈建輸送量 * 延遲秒數) / (批次大小 * 單一寫入花費的 RU 數)*。</span><span class="sxs-lookup"><span data-stu-id="41b20-167">For *numInsertionWorkers*, use this equation:   *numInsertionWorkers =  (provisioned throughput * latency in seconds) / (batch size * consumed RUs for a single write)*.</span></span>
        
    |<span data-ttu-id="41b20-168">屬性</span><span class="sxs-lookup"><span data-stu-id="41b20-168">Property</span></span>|<span data-ttu-id="41b20-169">值</span><span class="sxs-lookup"><span data-stu-id="41b20-169">Value</span></span>|
    |--------|-----|
    |<span data-ttu-id="41b20-170">batchSize</span><span class="sxs-lookup"><span data-stu-id="41b20-170">batchSize</span></span>| <span data-ttu-id="41b20-171">24</span><span class="sxs-lookup"><span data-stu-id="41b20-171">24</span></span> |
    |<span data-ttu-id="41b20-172">佈建的 RU</span><span class="sxs-lookup"><span data-stu-id="41b20-172">RUs provisioned</span></span> | <span data-ttu-id="41b20-173">10000</span><span class="sxs-lookup"><span data-stu-id="41b20-173">10000</span></span> |
    |<span data-ttu-id="41b20-174">延遲</span><span class="sxs-lookup"><span data-stu-id="41b20-174">Latency</span></span> | <span data-ttu-id="41b20-175">0.100 秒</span><span class="sxs-lookup"><span data-stu-id="41b20-175">0.100 s</span></span> |
    |<span data-ttu-id="41b20-176">寫入 1 個文件花費的 RU</span><span class="sxs-lookup"><span data-stu-id="41b20-176">RU charged for 1 doc write</span></span> | <span data-ttu-id="41b20-177">10 RU</span><span class="sxs-lookup"><span data-stu-id="41b20-177">10 RUs</span></span> |
    |<span data-ttu-id="41b20-178">numInsertionWorkers</span><span class="sxs-lookup"><span data-stu-id="41b20-178">numInsertionWorkers</span></span> | <span data-ttu-id="41b20-179">?</span><span class="sxs-lookup"><span data-stu-id="41b20-179">?</span></span> |
    
    <span data-ttu-id="41b20-180">*numInsertionWorkers = (10000 RU x 0.1 s) / (24 x 10 RU) = 4.1666*</span><span class="sxs-lookup"><span data-stu-id="41b20-180">*numInsertionWorkers = (10000 RUs x 0.1 s) / (24 x 10 RUs) = 4.1666*</span></span>

6. <span data-ttu-id="41b20-181">執行最後的移轉命令：</span><span class="sxs-lookup"><span data-stu-id="41b20-181">Run the final migration command:</span></span>

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a><span data-ttu-id="41b20-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="41b20-182">Next steps</span></span>

<span data-ttu-id="41b20-183">您可以繼續進行下一個教學課程，了解如何使用 Azure Cosmos DB 查詢 MongoDB 資料。</span><span class="sxs-lookup"><span data-stu-id="41b20-183">You can proceed to the next tutorial and learn how to query MongoDB data by using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="41b20-184">如何查詢 MongoDB 資料？</span><span class="sxs-lookup"><span data-stu-id="41b20-184">How to query MongoDB data?</span></span>](../cosmos-db/tutorial-query-mongodb.md)
