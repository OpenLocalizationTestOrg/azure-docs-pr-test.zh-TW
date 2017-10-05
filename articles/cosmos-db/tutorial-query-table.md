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
# <a name="azure-cosmos-db-how-to-query-table-data-by-using-the-table-api-preview"></a><span data-ttu-id="72fa8-104">Azure Cosmos DB：如何使用資料表 API (預覽) 來查詢資料表資料？</span><span class="sxs-lookup"><span data-stu-id="72fa8-104">Azure Cosmos DB: How to query table data by using the Table API (preview)?</span></span>

<span data-ttu-id="72fa8-105">Azure Cosmos DB [資料表 API](table-introduction.md) (預覽) 支援對索引鍵/值 (資料表) 資料進行 OData 和 [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) 查詢。</span><span class="sxs-lookup"><span data-stu-id="72fa8-105">The Azure Cosmos DB [Table API](table-introduction.md) (preview) supports OData and [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) queries against key/value (table) data.</span></span>  

<span data-ttu-id="72fa8-106">本文涵蓋下列工作：</span><span class="sxs-lookup"><span data-stu-id="72fa8-106">This article covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="72fa8-107">使用資料表 API 來查詢資料</span><span class="sxs-lookup"><span data-stu-id="72fa8-107">Querying data with the Table API</span></span>

<span data-ttu-id="72fa8-108">本文中的查詢使用下列範例 `People` 資料表：</span><span class="sxs-lookup"><span data-stu-id="72fa8-108">The queries in this article use the following sample `People` table:</span></span>

| <span data-ttu-id="72fa8-109">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="72fa8-109">PartitionKey</span></span> | <span data-ttu-id="72fa8-110">RowKey</span><span class="sxs-lookup"><span data-stu-id="72fa8-110">RowKey</span></span> | <span data-ttu-id="72fa8-111">電子郵件</span><span class="sxs-lookup"><span data-stu-id="72fa8-111">Email</span></span> | <span data-ttu-id="72fa8-112">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="72fa8-112">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="72fa8-113">Harp</span><span class="sxs-lookup"><span data-stu-id="72fa8-113">Harp</span></span> | <span data-ttu-id="72fa8-114">Walter</span><span class="sxs-lookup"><span data-stu-id="72fa8-114">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="72fa8-115">425-555-0101</span><span class="sxs-lookup"><span data-stu-id="72fa8-115">425-555-0101</span></span> |
| <span data-ttu-id="72fa8-116">Smith</span><span class="sxs-lookup"><span data-stu-id="72fa8-116">Smith</span></span> | <span data-ttu-id="72fa8-117">Ben</span><span class="sxs-lookup"><span data-stu-id="72fa8-117">Ben</span></span> | Ben@contoso.com| <span data-ttu-id="72fa8-118">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="72fa8-118">425-555-0102</span></span> |
| <span data-ttu-id="72fa8-119">Smith</span><span class="sxs-lookup"><span data-stu-id="72fa8-119">Smith</span></span> | <span data-ttu-id="72fa8-120">Jeff</span><span class="sxs-lookup"><span data-stu-id="72fa8-120">Jeff</span></span> | Jeff@contoso.com| <span data-ttu-id="72fa8-121">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="72fa8-121">425-555-0104</span></span> | 

<span data-ttu-id="72fa8-122">由於 Azure Cosmos DB 與 Azure 資料表儲存體 API 相容，因此請參閱 [Querying Tables and Entities (查詢資料表和實體)] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities)，以了解有關如何使用資料表 API 進行查詢的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="72fa8-122">Because Azure Cosmos DB is compatible with the Azure Table storage APIs, see [Querying Tables and Entities] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) for details on how to query by using the Table API.</span></span> 

<span data-ttu-id="72fa8-123">如需 Azure Cosmos DB 所提供之進階功能的詳細資訊，請參閱 [Azure Cosmos DB：資料表 API](table-introduction.md) 和[在 .NET 中使用資料表 API 進行開發](tutorial-develop-table-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="72fa8-123">For more information on the premium capabilities that Azure Cosmos DB offers, see [Azure Cosmos DB: Table API](table-introduction.md) and [Develop with the Table API in .NET](tutorial-develop-table-dotnet.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="72fa8-124">必要條件</span><span class="sxs-lookup"><span data-stu-id="72fa8-124">Prerequisites</span></span>

<span data-ttu-id="72fa8-125">若要讓這些查詢能夠運作，您必須具備 Azure Cosmos DB 帳戶，並且在容器中有實體資料。</span><span class="sxs-lookup"><span data-stu-id="72fa8-125">For these queries to work, you must have an Azure Cosmos DB account and have entity data in the container.</span></span> <span data-ttu-id="72fa8-126">不符合上述其中任何一項條件嗎？</span><span class="sxs-lookup"><span data-stu-id="72fa8-126">Don't have any of those?</span></span> <span data-ttu-id="72fa8-127">請完成 [5 分鐘快速入門](https://aka.ms/acdbtnetqs)或[開發人員教學課程](https://aka.ms/acdbtabletut)，以建立帳戶並在資料庫中填入資料。</span><span class="sxs-lookup"><span data-stu-id="72fa8-127">Complete the [five-minute quickstart](https://aka.ms/acdbtnetqs) or the [developer tutorial](https://aka.ms/acdbtabletut) to create an account and populate your database.</span></span>

## <a name="query-on-partitionkey-and-rowkey"></a><span data-ttu-id="72fa8-128">在 PartitionKey 和 RowKey 上執行查詢</span><span class="sxs-lookup"><span data-stu-id="72fa8-128">Query on PartitionKey and RowKey</span></span>
<span data-ttu-id="72fa8-129">由於 PartitionKey 和 RowKey 屬性會構成實體的主索引鍵，因此您可以使用下列特殊語法來識別實體：</span><span class="sxs-lookup"><span data-stu-id="72fa8-129">Because the PartitionKey and RowKey properties form an entity's primary key, you can use the following special syntax to identify the entity:</span></span> 

<span data-ttu-id="72fa8-130">**查詢**</span><span class="sxs-lookup"><span data-stu-id="72fa8-130">**Query**</span></span>

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
<span data-ttu-id="72fa8-131">**結果**</span><span class="sxs-lookup"><span data-stu-id="72fa8-131">**Results**</span></span>

| <span data-ttu-id="72fa8-132">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="72fa8-132">PartitionKey</span></span> | <span data-ttu-id="72fa8-133">RowKey</span><span class="sxs-lookup"><span data-stu-id="72fa8-133">RowKey</span></span> | <span data-ttu-id="72fa8-134">電子郵件</span><span class="sxs-lookup"><span data-stu-id="72fa8-134">Email</span></span> | <span data-ttu-id="72fa8-135">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="72fa8-135">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="72fa8-136">Harp</span><span class="sxs-lookup"><span data-stu-id="72fa8-136">Harp</span></span> | <span data-ttu-id="72fa8-137">Walter</span><span class="sxs-lookup"><span data-stu-id="72fa8-137">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="72fa8-138">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="72fa8-138">425-555-0104</span></span> |

<span data-ttu-id="72fa8-139">或者，您也可以在指定 `$filter` 選項時一併指定這些屬性，如下一節中所示。</span><span class="sxs-lookup"><span data-stu-id="72fa8-139">Alternatively, you can specify these properties as part of the `$filter` option, as shown in the following section.</span></span> <span data-ttu-id="72fa8-140">請注意，索引鍵屬性名稱和常數值有區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="72fa8-140">Note that the key property names and constant values are case-sensitive.</span></span> <span data-ttu-id="72fa8-141">PartitionKey 和 RowKey 屬性的類型都是 String。</span><span class="sxs-lookup"><span data-stu-id="72fa8-141">Both the PartitionKey and RowKey properties are of type String.</span></span> 

## <a name="query-by-using-an-odata-filter"></a><span data-ttu-id="72fa8-142">使用 OData 篩選進行查詢</span><span class="sxs-lookup"><span data-stu-id="72fa8-142">Query by using an OData filter</span></span>
<span data-ttu-id="72fa8-143">建構篩選字串時，請牢記下列規則：</span><span class="sxs-lookup"><span data-stu-id="72fa8-143">When you're constructing a filter string, keep these rules in mind:</span></span> 

* <span data-ttu-id="72fa8-144">使用「OData 通訊協定規格」所定義的邏輯運算子來比較屬性與值。</span><span class="sxs-lookup"><span data-stu-id="72fa8-144">Use the logical operators defined by the OData Protocol Specification to compare a property to a value.</span></span> <span data-ttu-id="72fa8-145">請注意，您無法比較屬性與動態值。</span><span class="sxs-lookup"><span data-stu-id="72fa8-145">Note that you can't compare a property to a dynamic value.</span></span> <span data-ttu-id="72fa8-146">運算式的一端必須是常數。</span><span class="sxs-lookup"><span data-stu-id="72fa8-146">One side of the expression must be a constant.</span></span> 
* <span data-ttu-id="72fa8-147">屬性名稱、運算子及常數值必須以 URL 編碼的空格分隔。</span><span class="sxs-lookup"><span data-stu-id="72fa8-147">The property name, operator, and constant value must be separated by URL-encoded spaces.</span></span> <span data-ttu-id="72fa8-148">空格經 URL 編碼後會變成 `%20`。</span><span class="sxs-lookup"><span data-stu-id="72fa8-148">A space is URL-encoded as `%20`.</span></span> 
* <span data-ttu-id="72fa8-149">篩選字串的所有部分都區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="72fa8-149">All parts of the filter string are case-sensitive.</span></span> 
* <span data-ttu-id="72fa8-150">常數和屬性必須是相同的資料類型，篩選才能傳回有效的結果。</span><span class="sxs-lookup"><span data-stu-id="72fa8-150">The constant value must be of the same data type as the property in order for the filter to return valid results.</span></span> <span data-ttu-id="72fa8-151">如需支援的屬性類型的詳細資訊，請參閱 [了解表格服務資料模型](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model)。</span><span class="sxs-lookup"><span data-stu-id="72fa8-151">For more information about supported property types, see [Understanding the Table Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span></span> 

<span data-ttu-id="72fa8-152">以下是一個範例查詢，說明如如何使用 OData `$filter` 依 PartitionKey 和 Email 屬性進行篩選。</span><span class="sxs-lookup"><span data-stu-id="72fa8-152">Here's an example query that shows how to filter by the PartitionKey and Email properties by using an OData `$filter`.</span></span>

<span data-ttu-id="72fa8-153">**查詢**</span><span class="sxs-lookup"><span data-stu-id="72fa8-153">**Query**</span></span>

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

<span data-ttu-id="72fa8-154">如需如何針對各種資料類型建構篩選條件運算式的詳細資訊，請參閱[查詢資料表和實體](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities)。</span><span class="sxs-lookup"><span data-stu-id="72fa8-154">For more information on how to construct filter expressions for various data types, see [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span></span>

<span data-ttu-id="72fa8-155">**結果**</span><span class="sxs-lookup"><span data-stu-id="72fa8-155">**Results**</span></span>

| <span data-ttu-id="72fa8-156">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="72fa8-156">PartitionKey</span></span> | <span data-ttu-id="72fa8-157">RowKey</span><span class="sxs-lookup"><span data-stu-id="72fa8-157">RowKey</span></span> | <span data-ttu-id="72fa8-158">電子郵件</span><span class="sxs-lookup"><span data-stu-id="72fa8-158">Email</span></span> | <span data-ttu-id="72fa8-159">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="72fa8-159">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="72fa8-160">Ben</span><span class="sxs-lookup"><span data-stu-id="72fa8-160">Ben</span></span> |<span data-ttu-id="72fa8-161">Smith</span><span class="sxs-lookup"><span data-stu-id="72fa8-161">Smith</span></span> | Ben@contoso.com| <span data-ttu-id="72fa8-162">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="72fa8-162">425-555-0102</span></span> |

## <a name="query-by-using-linq"></a><span data-ttu-id="72fa8-163">使用 LINQ 進行查詢</span><span class="sxs-lookup"><span data-stu-id="72fa8-163">Query by using LINQ</span></span> 
<span data-ttu-id="72fa8-164">您也可以使用 LINQ 進行查詢，這會轉譯成對應的 OData 查詢運算式。</span><span class="sxs-lookup"><span data-stu-id="72fa8-164">You can also query by using LINQ, which translates to the corresponding OData query expressions.</span></span> <span data-ttu-id="72fa8-165">以下是一個範例，說明如何使用 .NET SDK 來建置查詢：</span><span class="sxs-lookup"><span data-stu-id="72fa8-165">Here's an example of how to build queries by using the .NET SDK:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="72fa8-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="72fa8-166">Next steps</span></span>

<span data-ttu-id="72fa8-167">在本教學課程中，您已完成下列操作：</span><span class="sxs-lookup"><span data-stu-id="72fa8-167">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="72fa8-168">了解如何使用資料表 API (預覽) 來進行查詢</span><span class="sxs-lookup"><span data-stu-id="72fa8-168">Learned how to query by using the Table API (preview)</span></span> 

<span data-ttu-id="72fa8-169">您現在可以繼續進行到下一個教學課程，以了解如何全域散發您的資料。</span><span class="sxs-lookup"><span data-stu-id="72fa8-169">You can now proceed to the next tutorial to learn how to distribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="72fa8-170">全域散發您的資料</span><span class="sxs-lookup"><span data-stu-id="72fa8-170">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)
