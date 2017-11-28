---
title: "aaaUse mongoimport 和 mongorestore 與 hello Azure Cosmos DB API for MongoDB。 |Microsoft 文件"
description: "深入了解如何 toouse mongoimport 和 mongorestore tooimport 資料 tooan API MongoDB 帳戶"
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
ms.openlocfilehash: 921354bc7b09a076a73e0cbf5e4aabcc9e83d5a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-import-mongodb-data"></a><span data-ttu-id="4c158-104">Azure Cosmos DB：匯入 MongoDB 資料</span><span class="sxs-lookup"><span data-stu-id="4c158-104">Azure Cosmos DB: Import MongoDB data</span></span> 

<span data-ttu-id="4c158-105">toomigrate MongoDB tooan hello API 搭配 for MongoDB 的 Azure Cosmos DB 帳戶資料，您必須：</span><span class="sxs-lookup"><span data-stu-id="4c158-105">toomigrate data from MongoDB tooan Azure Cosmos DB account for use with hello API for MongoDB, you must:</span></span>

* <span data-ttu-id="4c158-106">下載任何*mongoimport.exe*或*mongorestore.exe*從 hello [MongoDB 下載中心](https://www.mongodb.com/download-center)。</span><span class="sxs-lookup"><span data-stu-id="4c158-106">Download either *mongoimport.exe* or *mongorestore.exe* from hello [MongoDB Download Center](https://www.mongodb.com/download-center).</span></span>
* <span data-ttu-id="4c158-107">取得[適用於 MongoDB 的 API 連接字串](connect-mongodb-account.md)。</span><span class="sxs-lookup"><span data-stu-id="4c158-107">Get your [API for MongoDB connection string](connect-mongodb-account.md).</span></span>

<span data-ttu-id="4c158-108">如果您要匯入資料從 MongoDB 和計劃 toouse 它與 hello Azure Cosmos DB，您應該使用 hello[資料移轉工具](import-data.md)tooimport 資料。</span><span class="sxs-lookup"><span data-stu-id="4c158-108">If you are importing data from MongoDB and plan toouse it with hello Azure Cosmos DB, you should use hello [Data Migration tool](import-data.md) tooimport data.</span></span>

<span data-ttu-id="4c158-109">本教學課程涵蓋 hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="4c158-109">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4c158-110">擷取連接字串</span><span class="sxs-lookup"><span data-stu-id="4c158-110">Retrieving your connection string</span></span>
> * <span data-ttu-id="4c158-111">使用 mongoimport 匯入 MongoDB 資料</span><span class="sxs-lookup"><span data-stu-id="4c158-111">Importing MongoDB data by using mongoimport</span></span>
> * <span data-ttu-id="4c158-112">使用 mongorestore 匯入 MongoDB 資料</span><span class="sxs-lookup"><span data-stu-id="4c158-112">Importing MongoDB data by using mongorestore</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4c158-113">必要條件</span><span class="sxs-lookup"><span data-stu-id="4c158-113">Prerequisites</span></span>

* <span data-ttu-id="4c158-114">增加輸送量： hello 資料移轉的持續時間取決於 hello 數量輸送量設定您的集合。</span><span class="sxs-lookup"><span data-stu-id="4c158-114">Increase throughput: hello duration of your data migration depends on hello amount of throughput you set up for your collections.</span></span> <span data-ttu-id="4c158-115">為確定 tooincrease hello 輸送量較大的資料移轉。</span><span class="sxs-lookup"><span data-stu-id="4c158-115">Be sure tooincrease hello throughput for larger data migrations.</span></span> <span data-ttu-id="4c158-116">Hello 移轉完成之後，會降低 hello 輸送量 toosave 成本。</span><span class="sxs-lookup"><span data-stu-id="4c158-116">After you've completed hello migration, decrease hello throughput toosave costs.</span></span> <span data-ttu-id="4c158-117">如需有關增加輸送量 hello [Azure 入口網站](https://portal.azure.com)，請參閱[效能層級和定價層，在 Azure Cosmos DB](performance-levels.md)。</span><span class="sxs-lookup"><span data-stu-id="4c158-117">For more information about increasing throughput in hello [Azure portal](https://portal.azure.com), see [Performance levels and pricing tiers in Azure Cosmos DB](performance-levels.md).</span></span>

* <span data-ttu-id="4c158-118">啟用 SSL：Azure Cosmos DB 有嚴格的安全性需求和標準。</span><span class="sxs-lookup"><span data-stu-id="4c158-118">Enable SSL: Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="4c158-119">當您與您的帳戶互動時，是確定 tooenable SSL。</span><span class="sxs-lookup"><span data-stu-id="4c158-119">Be sure tooenable SSL when you interact with your account.</span></span> <span data-ttu-id="4c158-120">hello 文章的 hello 其餘部分中的 hello 程序包括如何 mongoimport 和 mongorestore tooenable SSL。</span><span class="sxs-lookup"><span data-stu-id="4c158-120">hello procedures in hello rest of hello article include how tooenable SSL for mongoimport and mongorestore.</span></span>

## <a name="find-your-connection-string-information-host-port-username-and-password"></a><span data-ttu-id="4c158-121">找到您的連接字串資訊 (主機、連接埠、使用者名稱、密碼)</span><span class="sxs-lookup"><span data-stu-id="4c158-121">Find your connection string information (host, port, username, and password)</span></span>

1. <span data-ttu-id="4c158-122">在 hello [Azure 入口網站](https://portal.azure.com)，在 hello 左的窗格中按一下 hello **Azure Cosmos DB**項目。</span><span class="sxs-lookup"><span data-stu-id="4c158-122">In hello [Azure portal](https://portal.azure.com), in hello left pane, click hello **Azure Cosmos DB** entry.</span></span>
2. <span data-ttu-id="4c158-123">在 [hello**訂閱**] 窗格中，選取您的帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="4c158-123">In hello **Subscriptions** pane, select your account name.</span></span>
3. <span data-ttu-id="4c158-124">在 hello**連接字串**刀鋒視窗中，按一下 **連接字串**。</span><span class="sxs-lookup"><span data-stu-id="4c158-124">In hello **Connection String** blade, click **Connection String**.</span></span>  
<span data-ttu-id="4c158-125">右窗格包含所有您需要 toosuccessfully 的 hello 資訊 hello tooyour 帳戶的連接。</span><span class="sxs-lookup"><span data-stu-id="4c158-125">hello right pane contains all hello information that you need toosuccessfully connect tooyour account.</span></span>

    ![[連接字串] 刀鋒視窗](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-toohello-api-for-mongodb-by-using-mongoimport"></a><span data-ttu-id="4c158-127">使用 mongoimport for MongoDB。 匯入資料 toohello API</span><span class="sxs-lookup"><span data-stu-id="4c158-127">Import data toohello API for MongoDB by using mongoimport</span></span>

<span data-ttu-id="4c158-128">tooimport 資料 tooyour Azure Cosmos DB 帳戶，請使用下列範本的 hello。</span><span class="sxs-lookup"><span data-stu-id="4c158-128">tooimport data tooyour Azure Cosmos DB account, use hello following template.</span></span> <span data-ttu-id="4c158-129">填寫*主機*， *username*，和*密碼*具有特定 tooyour 帳戶 hello 數值。</span><span class="sxs-lookup"><span data-stu-id="4c158-129">Fill in *host*, *username*, and *password* with hello values that are specific tooyour account.</span></span>  

<span data-ttu-id="4c158-130">範本：</span><span class="sxs-lookup"><span data-stu-id="4c158-130">Template:</span></span>

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

<span data-ttu-id="4c158-131">範例：</span><span class="sxs-lookup"><span data-stu-id="4c158-131">Example:</span></span>  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-toohello-api-for-mongodb-by-using-mongorestore"></a><span data-ttu-id="4c158-132">使用 mongorestore for MongoDB。 匯入資料 toohello API</span><span class="sxs-lookup"><span data-stu-id="4c158-132">Import data toohello API for MongoDB by using mongorestore</span></span>

<span data-ttu-id="4c158-133">toorestore 資料 tooyour API MongoDB 帳戶，使用下列範本 tooexecute hello 匯入的 hello。</span><span class="sxs-lookup"><span data-stu-id="4c158-133">toorestore data tooyour API for MongoDB account, use hello following template tooexecute hello import.</span></span> <span data-ttu-id="4c158-134">填寫*主機*， *username*，和*密碼*具有特定 tooyour 帳戶 hello 數值。</span><span class="sxs-lookup"><span data-stu-id="4c158-134">Fill in *host*, *username*, and *password* with hello values that are specific tooyour account.</span></span>

<span data-ttu-id="4c158-135">範本：</span><span class="sxs-lookup"><span data-stu-id="4c158-135">Template:</span></span>

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

<span data-ttu-id="4c158-136">範例：</span><span class="sxs-lookup"><span data-stu-id="4c158-136">Example:</span></span>

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a><span data-ttu-id="4c158-137">成功移轉的指南</span><span class="sxs-lookup"><span data-stu-id="4c158-137">Guide for a successful migration</span></span>

1. <span data-ttu-id="4c158-138">預先建立並調整您的集合：</span><span class="sxs-lookup"><span data-stu-id="4c158-138">Pre-create and scale your collections:</span></span>
        
    * <span data-ttu-id="4c158-139">根據預設，Azure Cosmos DB 會佈建含 1,000 個要求單位 (RU) 的新 MongoDB 集合。</span><span class="sxs-lookup"><span data-stu-id="4c158-139">By default, Azure Cosmos DB provisions a new MongoDB collection with 1,000 request units (RUs).</span></span> <span data-ttu-id="4c158-140">使用 mongoimport、 mongorestore 或 mongomirror 開始 hello 移轉之前，預先建立所有的集合從 hello [Azure 入口網站](https://portal.azure.com)或從 MongoDB 驅動程式和工具。</span><span class="sxs-lookup"><span data-stu-id="4c158-140">Before you start hello migration by using mongoimport, mongorestore, or mongomirror, pre-create all your collections from hello [Azure portal](https://portal.azure.com) or from MongoDB drivers and tools.</span></span> <span data-ttu-id="4c158-141">如果您的集合大於 10 GB，請確定 toocreate[分區化/資料分割集合](partition-data.md)與適當的分區化索引鍵。</span><span class="sxs-lookup"><span data-stu-id="4c158-141">If your collection is greater than 10 GB, make sure toocreate a [sharded/partitioned collection](partition-data.md) with an appropriate shard key.</span></span>

    * <span data-ttu-id="4c158-142">從 hello [Azure 入口網站](https://portal.azure.com)，增加從 1000 RUs 單一分割區集合和 2500 RUs 分區化的集合，只針對 hello 移轉集合的輸送量。</span><span class="sxs-lookup"><span data-stu-id="4c158-142">From hello [Azure portal](https://portal.azure.com), increase your collections' throughput from 1,000 RUs for a single partition collection and 2,500 RUs for a sharded collection just for hello migration.</span></span> <span data-ttu-id="4c158-143">與 hello 較高的輸送量，您可以避免節流，並更少的時間移轉。</span><span class="sxs-lookup"><span data-stu-id="4c158-143">With hello higher throughput, you can avoid throttling and migrate in less time.</span></span> <span data-ttu-id="4c158-144">一小時的計費 Azure Cosmos DB 中，您可以減少 hello 移轉 toosave 成本之後立即 hello 輸送量。</span><span class="sxs-lookup"><span data-stu-id="4c158-144">With hourly billing in Azure Cosmos DB, you can reduce hello throughput immediately after hello migration toosave costs.</span></span>

2. <span data-ttu-id="4c158-145">計算單一文件寫入 hello 近似 RU 的費用：</span><span class="sxs-lookup"><span data-stu-id="4c158-145">Calculate hello approximate RU charge for a single document write:</span></span>

    <span data-ttu-id="4c158-146">a.</span><span class="sxs-lookup"><span data-stu-id="4c158-146">a.</span></span> <span data-ttu-id="4c158-147">從 hello MongoDB Shell 連接 tooyour Azure Cosmos DB MongoDB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="4c158-147">Connect tooyour Azure Cosmos DB MongoDB database from hello MongoDB Shell.</span></span> <span data-ttu-id="4c158-148">您可以找到中的指示[連接 MongoDB 應用程式 tooAzure Cosmos DB](connect-mongodb-account.md)。</span><span class="sxs-lookup"><span data-stu-id="4c158-148">You can find instructions in [Connect a MongoDB application tooAzure Cosmos DB](connect-mongodb-account.md).</span></span>
    
    <span data-ttu-id="4c158-149">b.</span><span class="sxs-lookup"><span data-stu-id="4c158-149">b.</span></span> <span data-ttu-id="4c158-150">使用其中一種範例文件從 hello MongoDB 殼層執行 insert 命令範例：</span><span class="sxs-lookup"><span data-stu-id="4c158-150">Run a sample insert command by using one of your sample documents from hello MongoDB Shell:</span></span>
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    <span data-ttu-id="4c158-151">c.</span><span class="sxs-lookup"><span data-stu-id="4c158-151">c.</span></span> <span data-ttu-id="4c158-152">執行 ```db.runCommand({getLastRequestStatistics: 1})```，您會收到如下的回應：</span><span class="sxs-lookup"><span data-stu-id="4c158-152">Run ```db.runCommand({getLastRequestStatistics: 1})``` and you will receive a response like this one:</span></span>
     
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
        
    <span data-ttu-id="4c158-153">d.</span><span class="sxs-lookup"><span data-stu-id="4c158-153">d.</span></span> <span data-ttu-id="4c158-154">記下 hello 要求費用。</span><span class="sxs-lookup"><span data-stu-id="4c158-154">Take note of hello request charge.</span></span>
    
3. <span data-ttu-id="4c158-155">決定從您的機器 toohello Azure Cosmos DB 雲端服務的 hello 延遲：</span><span class="sxs-lookup"><span data-stu-id="4c158-155">Determine hello latency from your machine toohello Azure Cosmos DB cloud service:</span></span>
    
    <span data-ttu-id="4c158-156">a.</span><span class="sxs-lookup"><span data-stu-id="4c158-156">a.</span></span> <span data-ttu-id="4c158-157">使用此命令，以啟用從 hello MongoDB 殼層的詳細資訊記錄：```setVerboseShell(true)```</span><span class="sxs-lookup"><span data-stu-id="4c158-157">Enable verbose logging from hello MongoDB Shell by using this command: ```setVerboseShell(true)```</span></span>
    
    <span data-ttu-id="4c158-158">b.</span><span class="sxs-lookup"><span data-stu-id="4c158-158">b.</span></span> <span data-ttu-id="4c158-159">對 hello 資料庫執行簡單的查詢： ```db.coll.find().limit(1)```。</span><span class="sxs-lookup"><span data-stu-id="4c158-159">Run a simple query against hello database: ```db.coll.find().limit(1)```.</span></span> <span data-ttu-id="4c158-160">您會收到如下的回應：</span><span class="sxs-lookup"><span data-stu-id="4c158-160">You will receive a response like this one:</span></span>

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. <span data-ttu-id="4c158-161">移除之前沒有重複的文件的 hello 移轉 tooensure hello 插入文件。</span><span class="sxs-lookup"><span data-stu-id="4c158-161">Remove hello inserted document before hello migration tooensure that there are no duplicate documents.</span></span> <span data-ttu-id="4c158-162">您可以使用此命令來移除文件：```db.coll.remove({})```</span><span class="sxs-lookup"><span data-stu-id="4c158-162">You can remove documents by using this command: ```db.coll.remove({})```</span></span>

5. <span data-ttu-id="4c158-163">計算 hello 近似*batchSize*和*numInsertionWorkers*值：</span><span class="sxs-lookup"><span data-stu-id="4c158-163">Calculate hello approximate *batchSize* and *numInsertionWorkers* values:</span></span>

    * <span data-ttu-id="4c158-164">如*batchSize*，除以 hello 總計佈建 RUs 由 hello RUs 從您在步驟 3 中的單一文件寫入取用。</span><span class="sxs-lookup"><span data-stu-id="4c158-164">For *batchSize*, divide hello total provisioned RUs by hello RUs consumed from your single document write in step 3.</span></span>
    
    * <span data-ttu-id="4c158-165">如果 hello 計算*batchSize* < = 24，使用該數字，以您*batchSize*值。</span><span class="sxs-lookup"><span data-stu-id="4c158-165">If hello calculated *batchSize* <= 24, use that number as your *batchSize* value.</span></span>
    
    * <span data-ttu-id="4c158-166">如果 hello 計算*batchSize* > 24、 組 hello *batchSize*值 too24。</span><span class="sxs-lookup"><span data-stu-id="4c158-166">If hello calculated *batchSize* > 24, set hello *batchSize* value too24.</span></span>
    
    * <span data-ttu-id="4c158-167">*numInsertionWorkers* 的算法是使用此方程式：*numInsertionWorkers =  (佈建輸送量 * 延遲秒數) / (批次大小 * 單一寫入花費的 RU 數)*。</span><span class="sxs-lookup"><span data-stu-id="4c158-167">For *numInsertionWorkers*, use this equation:   *numInsertionWorkers =  (provisioned throughput * latency in seconds) / (batch size * consumed RUs for a single write)*.</span></span>
        
    |<span data-ttu-id="4c158-168">屬性</span><span class="sxs-lookup"><span data-stu-id="4c158-168">Property</span></span>|<span data-ttu-id="4c158-169">值</span><span class="sxs-lookup"><span data-stu-id="4c158-169">Value</span></span>|
    |--------|-----|
    |<span data-ttu-id="4c158-170">batchSize</span><span class="sxs-lookup"><span data-stu-id="4c158-170">batchSize</span></span>| <span data-ttu-id="4c158-171">24</span><span class="sxs-lookup"><span data-stu-id="4c158-171">24</span></span> |
    |<span data-ttu-id="4c158-172">佈建的 RU</span><span class="sxs-lookup"><span data-stu-id="4c158-172">RUs provisioned</span></span> | <span data-ttu-id="4c158-173">10000</span><span class="sxs-lookup"><span data-stu-id="4c158-173">10000</span></span> |
    |<span data-ttu-id="4c158-174">延遲</span><span class="sxs-lookup"><span data-stu-id="4c158-174">Latency</span></span> | <span data-ttu-id="4c158-175">0.100 秒</span><span class="sxs-lookup"><span data-stu-id="4c158-175">0.100 s</span></span> |
    |<span data-ttu-id="4c158-176">寫入 1 個文件花費的 RU</span><span class="sxs-lookup"><span data-stu-id="4c158-176">RU charged for 1 doc write</span></span> | <span data-ttu-id="4c158-177">10 RU</span><span class="sxs-lookup"><span data-stu-id="4c158-177">10 RUs</span></span> |
    |<span data-ttu-id="4c158-178">numInsertionWorkers</span><span class="sxs-lookup"><span data-stu-id="4c158-178">numInsertionWorkers</span></span> | <span data-ttu-id="4c158-179">?</span><span class="sxs-lookup"><span data-stu-id="4c158-179">?</span></span> |
    
    <span data-ttu-id="4c158-180">*numInsertionWorkers = (10000 RU x 0.1 s) / (24 x 10 RU) = 4.1666*</span><span class="sxs-lookup"><span data-stu-id="4c158-180">*numInsertionWorkers = (10000 RUs x 0.1 s) / (24 x 10 RUs) = 4.1666*</span></span>

6. <span data-ttu-id="4c158-181">執行 hello 最後的移轉命令：</span><span class="sxs-lookup"><span data-stu-id="4c158-181">Run hello final migration command:</span></span>

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a><span data-ttu-id="4c158-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4c158-182">Next steps</span></span>

<span data-ttu-id="4c158-183">您可以繼續 toohello 下一個教學課程，了解如何 tooquery MongoDB 藉由使用 Azure Cosmos DB 的資料。</span><span class="sxs-lookup"><span data-stu-id="4c158-183">You can proceed toohello next tutorial and learn how tooquery MongoDB data by using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="4c158-184">如何 tooquery MongoDB 資料嗎？</span><span class="sxs-lookup"><span data-stu-id="4c158-184">How tooquery MongoDB data?</span></span>](../cosmos-db/tutorial-query-mongodb.md)
