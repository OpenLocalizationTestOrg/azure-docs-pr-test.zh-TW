---
title: "Azure Cosmos DB 中的日期與 aaaWorking |Microsoft 文件"
description: "深入了解與 toowork Azure Cosmos DB 中的日期。"
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: e587772f-ce9f-498c-a017-a51e7265bb23
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 27ec170e4bef72c0b5b456738f1275ef02543024
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-dates-in-azure-cosmos-db"></a>使用 Azure Cosmos DB 中的日期
Azure Cosmos DB 透過原生 [JSON](http://www.json.org) 資料模型，提供結構描述的彈性和豐富的索引編製功能。 所有 Azure Cosmos DB 資源 (包括資料庫、集合、文件及預存程序) 都會建立模型，並以 JSON 文件的形式儲存。 為了滿足可攜性需求，JSON (和 Azure Cosmos DB) 僅支援一小組基本類型︰字串、數字、布林值、陣列、物件及 Null。 不過，JSON 具有彈性，讓開發人員和架構 toorepresent 更複雜的類型，使用下列基本類型和撰寫它們的物件或陣列。 

在加法 toohello 基本類型中，許多應用程式需要 hello [DateTime](https://msdn.microsoft.com/library/system.datetime(v=vs.110).aspx)輸入 toorepresent 日期和時間戳記。 本文說明如何開發人員可以儲存、 擷取及查詢中使用.NET SDK hello Azure Cosmos DB 的日期。

## <a name="storing-datetimes"></a>儲存 DateTimes
根據預設，hello [Azure Cosmos DB SDK](documentdb-sdk-dotnet.md)序列化 DateTime 值做為[ISO 8601](http://www.iso.org/iso/catalogue_detail?csnumber=40874)字串。 大部分的應用程式可以使用 hello 預設字串表示的 DateTime hello 下列原因：

* 可以比較字串、 和 hello 相對 hello 日期時間值的順序會保留在轉換後的 toostrings 時。 
* 這個方法不需要任何自訂程式碼或屬性來進行 JSON 轉換。
* 儲存在 JSON 中的 hello 日期為人類可讀取。
* 此方法可利用 Azure Cosmos DB 的索引來提升查詢效能。

例如，下列程式碼片段儲存區 hello`Order`物件包含兩個日期時間屬性-`ShipDate`和`OrderDate`做為文件使用 hello.NET SDK:

    public class Order
    {
        [JsonProperty(PropertyName="id")]
        public string Id { get; set; }
        public DateTime OrderDate { get; set; }
        public DateTime ShipDate { get; set; }
        public double Total { get; set; }
    }

    await client.CreateDocumentAsync("/dbs/orderdb/colls/orders", 
        new Order 
        { 
            Id = "09152014101",
            OrderDate = DateTime.UtcNow.AddDays(-30),
            ShipDate = DateTime.UtcNow.AddDays(-14), 
            Total = 113.39
        });

這份文件會在 Azure Cosmos DB 中以下列方式儲存：

    {
        "id": "09152014101",
        "OrderDate": "2014-09-15T23:14:25.7251173Z",
        "ShipDate": "2014-09-30T23:14:25.7251173Z",
        "Total": 113.39
    }
    

或者，您可以儲存 Unix 時間戳記作為 Datetime 也就是為代表 hello 自 1970 年 1 月 1 日後經過的秒數的數字。 Azure Cosmos DB 的內部時間戳記 (`_ts`) 屬性便是使用此方法。 您可以使用 hello [UnixDateTimeConverter](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.unixdatetimeconverter.aspx)類別 tooserialize Datetime as 號碼。 

## <a name="indexing-datetimes-for-range-queries"></a>索引 DateTime 以進行範圍查詢
DateTime 值常用於範圍查詢。 例如，如果您需要 toofind 昨天之後, 建立的所有訂單，或找出貨 hello 前五分鐘的所有訂單，您會都需要 tooperform 範圍查詢。 這些查詢有效率地 tooexecute，您必須設定您範圍索引字串的集合。

    DocumentCollection collection = new DocumentCollection { Id = "orders" };
    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    await client.CreateDocumentCollectionAsync("/dbs/orderdb", collection);

您可以進一步了解如何 tooconfigure 編製索引原則[Azure Cosmos DB 編製索引原則](indexing-policies.md)。

## <a name="querying-datetimes-in-linq"></a>用 LINQ 查詢 DateTime
hello Documentdb.net SDK 會自動支援查詢儲存在 Azure Cosmos DB 透過 LINQ 中的資料。 比方說，hello 下列程式碼片段顯示的 LINQ 查詢該篩選出貨訂單中 hello 三天。

    IQueryable<Order> orders = client.CreateDocumentQuery<Order>("/dbs/orderdb/colls/orders")
        .Where(o => o.ShipDate >= DateTime.UtcNow.AddDays(-3));
          
    // Translated toohello following SQL statement and executed on Azure Cosmos DB
    SELECT * FROM root WHERE (root["ShipDate"] >= "2016-12-18T21:55:03.45569Z")

您可以進一步了解 Azure Cosmos DB 的 SQL 查詢語言和 hello LINQ 提供者在[查詢 Cosmos DB](documentdb-sql-query.md)。

在本文中，我們討論了如何 toostore，索引和查詢 Azure Cosmos DB 中的 Datetime。

## <a name="next-steps"></a>後續步驟
* 下載並執行 hello [GitHub 上的範例程式碼](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples)
* 深入了解 [DocumentDB API 查詢](documentdb-sql-query.md)
* 深入了解 [Azure Cosmos DB 編製索引原則](indexing-policies.md)
