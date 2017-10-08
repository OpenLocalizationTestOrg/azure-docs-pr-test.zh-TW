---
title: "在 Azure Cosmos DB aaaHow tooquery 資料表資料嗎？ | Microsoft Docs"
description: "了解在 Azure Cosmos DB tooquery 資料表資料"
services: cosmos-db
documentationcenter: 
author: kanshiG
manager: jhubbard
editor: 
tags: 
ms.assetid: 14bcb94e-583c-46f7-9ea8-db010eb2ab43
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: govindk
ms.openlocfilehash: 32526c3488c589c5be3a4a2f174aa769570f0c0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-how-tooquery-table-data-by-using-hello-table-api-preview"></a>Azure Cosmos DB： 使用 tooquery 資料表資料如何 hello 表格 API （預覽）？

hello Azure Cosmos DB[表格 API](table-introduction.md) （預覽） 支援 OData 和[LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service)針對索引鍵/值 （資料表） 資料的查詢。  

本文涵蓋下列工作的 hello: 

> [!div class="checklist"]
> * 查詢以 hello 表格 API 的資料

hello 查詢本文中的使用下列範例中的 hello`People`資料表：

| PartitionKey | RowKey | 電子郵件 | PhoneNumber |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0101 |
| Smith | Ben | Ben@contoso.com| 425-555-0102 |
| Smith | Jeff | Jeff@contoso.com| 425-555-0104 | 

因為 Azure Cosmos DB 與 hello Azure 資料表儲存體 Api 相容，請參閱 [查詢資料表和實體] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) 如需如何使用 tooquery hello 詳細資料應用程式開發介面的資料表。 

如需有關 Azure Cosmos DB 所提供的 hello 高階功能的詳細資訊，請參閱[Azure Cosmos DB： 表格 API](table-introduction.md)和[以 hello 表格 API 在.NET 開發](tutorial-develop-table-dotnet.md)。 

## <a name="prerequisites"></a>必要條件

這些查詢 toowork，您必須擁有 Azure Cosmos DB 帳戶，而且具有 hello 容器中的實體資料。 不符合上述其中任何一項條件嗎？ 完整的 hello[五分鐘快速入門](https://aka.ms/acdbtnetqs)或 hello[開發人員教學課程](https://aka.ms/acdbtabletut)toocreate 帳戶，並填入您的資料庫。

## <a name="query-on-partitionkey-and-rowkey"></a>在 PartitionKey 和 RowKey 上執行查詢
因為 hello PartitionKey 和 RowKey 屬性會構成實體主索引鍵，您可以使用下列特殊語法 tooidentify hello 實體 hello: 

**查詢**

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
**結果**

| PartitionKey | RowKey | 電子郵件 | PhoneNumber |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0104 |

或者，您可以指定這些屬性一部分 hello`$filter`選項，hello 之後 > 一節中所示。 請注意 hello 索引鍵屬性名稱和常數值會區分大小寫。 Hello PartitionKey 和 RowKey 屬性為字串類型。 

## <a name="query-by-using-an-odata-filter"></a>使用 OData 篩選進行查詢
建構篩選字串時，請牢記下列規則： 

* 使用 hello hello OData 通訊協定規格 toocompare 屬性 tooa 值所定義的邏輯運算子。 請注意您無法比較屬性 tooa 動態值。 Hello 運算式的一端必須是常數。 
* hello 屬性名稱、 運算子和常數值都必須以 URL 編碼的空格分隔。 空格經 URL 編碼後會變成 `%20`。 
* Hello 篩選字串的所有部分都都區分大小寫的。 
* hello hello 常值必須是相同的資料類型作為 hello 篩選 tooreturn 有效結果的順序中的 hello 屬性。 如需支援的屬性類型的詳細資訊，請參閱[了解 hello 表格服務資料模型](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model)。 

以下是一個範例查詢示範如何透過 toofilter hello PartitionKey，和使用 OData 的電子郵件內容`$filter`。

**查詢**

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

如需有關如何 tooconstruct 篩選運算式的各種資料類型的詳細資訊，請參閱[查詢資料表和實體](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities)。

**結果**

| PartitionKey | RowKey | 電子郵件 | PhoneNumber |
| --- | --- | --- | --- |
| Ben |Smith | Ben@contoso.com| 425-555-0102 |

## <a name="query-by-using-linq"></a>使用 LINQ 進行查詢 
您也可以藉由將轉譯 toohello 相對應的 OData 查詢運算式的 LINQ 查詢。 以下是如何利用 toobuild 查詢 hello.NET SDK 的範例：

```csharp
CloudTableClient tableClient = account.CreateCloudTableClient();
CloudTable table = tableClient.GetTableReference("people");

TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
    .Where(
        TableQuery.CombineFilters(
            TableQuery.GenerateFilterCondition(PartitionKey, QueryComparisons.Equal, "Smith"),
            TableOperators.And,
            TableQuery.GenerateFilterCondition(Email, QueryComparisons.Equal,"Ben@contoso.com")
    ));

await table.ExecuteQuerySegmentedAsync<CustomerEntity>(query, null);
```

## <a name="next-steps"></a>後續步驟

在本教學課程中，您們 hello 下列：

> [!div class="checklist"]
> * 了解如何使用 tooquery hello 表格 API （預覽） 

您現在可以如何繼續 toohello 下一個教學課程 toolearn toodistribute 資料全域。

> [!div class="nextstepaction"]
> [全域散發您的資料](tutorial-global-distribution-documentdb.md)
