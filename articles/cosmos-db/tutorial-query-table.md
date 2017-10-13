---
title: "如何在 Azure Cosmos DB 中查詢資料表資料？ | Microsoft Docs"
description: "了解如何在 Azure Cosmos DB 中查詢資料表資料"
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
ms.openlocfilehash: e59cfa85c6bf584e44bdc6e88cc19d67df390041
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-how-to-query-table-data-by-using-the-table-api-preview"></a>Azure Cosmos DB：如何使用資料表 API (預覽) 來查詢資料表資料？

Azure Cosmos DB [資料表 API](table-introduction.md) (預覽) 支援對索引鍵/值 (資料表) 資料進行 OData 和 [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) 查詢。  

本文涵蓋下列工作： 

> [!div class="checklist"]
> * 使用資料表 API 來查詢資料

本文中的查詢使用下列範例 `People` 資料表：

| PartitionKey | RowKey | 電子郵件 | PhoneNumber |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0101 |
| Smith | Ben | Ben@contoso.com| 425-555-0102 |
| Smith | Jeff | Jeff@contoso.com| 425-555-0104 | 

由於 Azure Cosmos DB 與 Azure 資料表儲存體 API 相容，因此請參閱 [Querying Tables and Entities (查詢資料表和實體)] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities)，以了解有關如何使用資料表 API 進行查詢的詳細資料。 

如需 Azure Cosmos DB 所提供之進階功能的詳細資訊，請參閱 [Azure Cosmos DB：資料表 API](table-introduction.md) 和[在 .NET 中使用資料表 API 進行開發](tutorial-develop-table-dotnet.md)。 

## <a name="prerequisites"></a>必要條件

若要讓這些查詢能夠運作，您必須具備 Azure Cosmos DB 帳戶，並且在容器中有實體資料。 不符合上述其中任何一項條件嗎？ 請完成 [5 分鐘快速入門](https://aka.ms/acdbtnetqs)或[開發人員教學課程](https://aka.ms/acdbtabletut)，以建立帳戶並在資料庫中填入資料。

## <a name="query-on-partitionkey-and-rowkey"></a>在 PartitionKey 和 RowKey 上執行查詢
由於 PartitionKey 和 RowKey 屬性會構成實體的主索引鍵，因此您可以使用下列特殊語法來識別實體： 

**查詢**

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
**結果**

| PartitionKey | RowKey | 電子郵件 | PhoneNumber |
| --- | --- | --- | --- |
| Harp | Walter | Walter@contoso.com| 425-555-0104 |

或者，您也可以在指定 `$filter` 選項時一併指定這些屬性，如下一節中所示。 請注意，索引鍵屬性名稱和常數值有區分大小寫。 PartitionKey 和 RowKey 屬性的類型都是 String。 

## <a name="query-by-using-an-odata-filter"></a>使用 OData 篩選進行查詢
建構篩選字串時，請牢記下列規則： 

* 使用「OData 通訊協定規格」所定義的邏輯運算子來比較屬性與值。 請注意，您無法比較屬性與動態值。 運算式的一端必須是常數。 
* 屬性名稱、運算子及常數值必須以 URL 編碼的空格分隔。 空格經 URL 編碼後會變成 `%20`。 
* 篩選字串的所有部分都區分大小寫。 
* 常數和屬性必須是相同的資料類型，篩選才能傳回有效的結果。 如需支援的屬性類型的詳細資訊，請參閱 [了解表格服務資料模型](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model)。 

以下是一個範例查詢，說明如如何使用 OData `$filter` 依 PartitionKey 和 Email 屬性進行篩選。

**查詢**

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

如需如何針對各種資料類型建構篩選條件運算式的詳細資訊，請參閱[查詢資料表和實體](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities)。

**結果**

| PartitionKey | RowKey | 電子郵件 | PhoneNumber |
| --- | --- | --- | --- |
| Ben |Smith | Ben@contoso.com| 425-555-0102 |

## <a name="query-by-using-linq"></a>使用 LINQ 進行查詢 
您也可以使用 LINQ 進行查詢，這會轉譯成對應的 OData 查詢運算式。 以下是一個範例，說明如何使用 .NET SDK 來建置查詢：

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

在本教學課程中，您已完成下列操作：

> [!div class="checklist"]
> * 了解如何使用資料表 API (預覽) 來進行查詢 

您現在可以繼續進行到下一個教學課程，以了解如何全域散發您的資料。

> [!div class="nextstepaction"]
> [全域散發您的資料](tutorial-global-distribution-documentdb.md)
