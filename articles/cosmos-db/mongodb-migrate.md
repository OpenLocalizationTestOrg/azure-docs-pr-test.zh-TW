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
# <a name="azure-cosmos-db-import-mongodb-data"></a>Azure Cosmos DB：匯入 MongoDB 資料 

toomigrate MongoDB tooan hello API 搭配 for MongoDB 的 Azure Cosmos DB 帳戶資料，您必須：

* 下載任何*mongoimport.exe*或*mongorestore.exe*從 hello [MongoDB 下載中心](https://www.mongodb.com/download-center)。
* 取得[適用於 MongoDB 的 API 連接字串](connect-mongodb-account.md)。

如果您要匯入資料從 MongoDB 和計劃 toouse 它與 hello Azure Cosmos DB，您應該使用 hello[資料移轉工具](import-data.md)tooimport 資料。

本教學課程涵蓋 hello 下列工作：

> [!div class="checklist"]
> * 擷取連接字串
> * 使用 mongoimport 匯入 MongoDB 資料
> * 使用 mongorestore 匯入 MongoDB 資料

## <a name="prerequisites"></a>必要條件

* 增加輸送量： hello 資料移轉的持續時間取決於 hello 數量輸送量設定您的集合。 為確定 tooincrease hello 輸送量較大的資料移轉。 Hello 移轉完成之後，會降低 hello 輸送量 toosave 成本。 如需有關增加輸送量 hello [Azure 入口網站](https://portal.azure.com)，請參閱[效能層級和定價層，在 Azure Cosmos DB](performance-levels.md)。

* 啟用 SSL：Azure Cosmos DB 有嚴格的安全性需求和標準。 當您與您的帳戶互動時，是確定 tooenable SSL。 hello 文章的 hello 其餘部分中的 hello 程序包括如何 mongoimport 和 mongorestore tooenable SSL。

## <a name="find-your-connection-string-information-host-port-username-and-password"></a>找到您的連接字串資訊 (主機、連接埠、使用者名稱、密碼)

1. 在 hello [Azure 入口網站](https://portal.azure.com)，在 hello 左的窗格中按一下 hello **Azure Cosmos DB**項目。
2. 在 [hello**訂閱**] 窗格中，選取您的帳戶名稱。
3. 在 hello**連接字串**刀鋒視窗中，按一下 **連接字串**。  
右窗格包含所有您需要 toosuccessfully 的 hello 資訊 hello tooyour 帳戶的連接。

    ![[連接字串] 刀鋒視窗](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="import-data-toohello-api-for-mongodb-by-using-mongoimport"></a>使用 mongoimport for MongoDB。 匯入資料 toohello API

tooimport 資料 tooyour Azure Cosmos DB 帳戶，請使用下列範本的 hello。 填寫*主機*， *username*，和*密碼*具有特定 tooyour 帳戶 hello 數值。  

範本：

    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file C:\sample.json

範例：  

    mongoimport.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file C:\Users\anhoh\Desktop\*.json

## <a name="import-data-toohello-api-for-mongodb-by-using-mongorestore"></a>使用 mongorestore for MongoDB。 匯入資料 toohello API

toorestore 資料 tooyour API MongoDB 帳戶，使用下列範本 tooexecute hello 匯入的 hello。 填寫*主機*， *username*，和*密碼*具有特定 tooyour 帳戶 hello 數值。

範本：

    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>

範例：

    mongorestore.exe --host anhoh-host.documents.azure.com:10255 -u anhoh-host -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
    
## <a name="guide-for-a-successful-migration"></a>成功移轉的指南

1. 預先建立並調整您的集合：
        
    * 根據預設，Azure Cosmos DB 會佈建含 1,000 個要求單位 (RU) 的新 MongoDB 集合。 使用 mongoimport、 mongorestore 或 mongomirror 開始 hello 移轉之前，預先建立所有的集合從 hello [Azure 入口網站](https://portal.azure.com)或從 MongoDB 驅動程式和工具。 如果您的集合大於 10 GB，請確定 toocreate[分區化/資料分割集合](partition-data.md)與適當的分區化索引鍵。

    * 從 hello [Azure 入口網站](https://portal.azure.com)，增加從 1000 RUs 單一分割區集合和 2500 RUs 分區化的集合，只針對 hello 移轉集合的輸送量。 與 hello 較高的輸送量，您可以避免節流，並更少的時間移轉。 一小時的計費 Azure Cosmos DB 中，您可以減少 hello 移轉 toosave 成本之後立即 hello 輸送量。

2. 計算單一文件寫入 hello 近似 RU 的費用：

    a. 從 hello MongoDB Shell 連接 tooyour Azure Cosmos DB MongoDB 資料庫。 您可以找到中的指示[連接 MongoDB 應用程式 tooAzure Cosmos DB](connect-mongodb-account.md)。
    
    b. 使用其中一種範例文件從 hello MongoDB 殼層執行 insert 命令範例：
    
        ```db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })```
        
    c. 執行 ```db.runCommand({getLastRequestStatistics: 1})```，您會收到如下的回應：
     
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
        
    d. 記下 hello 要求費用。
    
3. 決定從您的機器 toohello Azure Cosmos DB 雲端服務的 hello 延遲：
    
    a. 使用此命令，以啟用從 hello MongoDB 殼層的詳細資訊記錄：```setVerboseShell(true)```
    
    b. 對 hello 資料庫執行簡單的查詢： ```db.coll.find().limit(1)```。 您會收到如下的回應：

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
4. 移除之前沒有重複的文件的 hello 移轉 tooensure hello 插入文件。 您可以使用此命令來移除文件：```db.coll.remove({})```

5. 計算 hello 近似*batchSize*和*numInsertionWorkers*值：

    * 如*batchSize*，除以 hello 總計佈建 RUs 由 hello RUs 從您在步驟 3 中的單一文件寫入取用。
    
    * 如果 hello 計算*batchSize* < = 24，使用該數字，以您*batchSize*值。
    
    * 如果 hello 計算*batchSize* > 24、 組 hello *batchSize*值 too24。
    
    * *numInsertionWorkers* 的算法是使用此方程式：*numInsertionWorkers =  (佈建輸送量 * 延遲秒數) / (批次大小 * 單一寫入花費的 RU 數)*。
        
    |屬性|值|
    |--------|-----|
    |batchSize| 24 |
    |佈建的 RU | 10000 |
    |延遲 | 0.100 秒 |
    |寫入 1 個文件花費的 RU | 10 RU |
    |numInsertionWorkers | ? |
    
    *numInsertionWorkers = (10000 RU x 0.1 s) / (24 x 10 RU) = 4.1666*

6. 執行 hello 最後的移轉命令：

   ```
   mongoimport.exe --host anhoh-mongodb.documents.azure.com:10255 -u anhoh-mongodb -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```

## <a name="next-steps"></a>後續步驟

您可以繼續 toohello 下一個教學課程，了解如何 tooquery MongoDB 藉由使用 Azure Cosmos DB 的資料。 

> [!div class="nextstepaction"]
>[如何 tooquery MongoDB 資料嗎？](../cosmos-db/tutorial-query-mongodb.md)
