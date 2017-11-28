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
# <a name="azure-cosmos-db-how-tooquery-table-data-by-using-hello-table-api-preview"></a><span data-ttu-id="7a94f-104">Azure Cosmos DB： 使用 tooquery 資料表資料如何 hello 表格 API （預覽）？</span><span class="sxs-lookup"><span data-stu-id="7a94f-104">Azure Cosmos DB: How tooquery table data by using hello Table API (preview)?</span></span>

<span data-ttu-id="7a94f-105">hello Azure Cosmos DB[表格 API](table-introduction.md) （預覽） 支援 OData 和[LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service)針對索引鍵/值 （資料表） 資料的查詢。</span><span class="sxs-lookup"><span data-stu-id="7a94f-105">hello Azure Cosmos DB [Table API](table-introduction.md) (preview) supports OData and [LINQ](https://docs.microsoft.com/rest/api/storageservices/fileservices/writing-linq-queries-against-the-table-service) queries against key/value (table) data.</span></span>  

<span data-ttu-id="7a94f-106">本文涵蓋下列工作的 hello:</span><span class="sxs-lookup"><span data-stu-id="7a94f-106">This article covers hello following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="7a94f-107">查詢以 hello 表格 API 的資料</span><span class="sxs-lookup"><span data-stu-id="7a94f-107">Querying data with hello Table API</span></span>

<span data-ttu-id="7a94f-108">hello 查詢本文中的使用下列範例中的 hello`People`資料表：</span><span class="sxs-lookup"><span data-stu-id="7a94f-108">hello queries in this article use hello following sample `People` table:</span></span>

| <span data-ttu-id="7a94f-109">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="7a94f-109">PartitionKey</span></span> | <span data-ttu-id="7a94f-110">RowKey</span><span class="sxs-lookup"><span data-stu-id="7a94f-110">RowKey</span></span> | <span data-ttu-id="7a94f-111">電子郵件</span><span class="sxs-lookup"><span data-stu-id="7a94f-111">Email</span></span> | <span data-ttu-id="7a94f-112">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="7a94f-112">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7a94f-113">Harp</span><span class="sxs-lookup"><span data-stu-id="7a94f-113">Harp</span></span> | <span data-ttu-id="7a94f-114">Walter</span><span class="sxs-lookup"><span data-stu-id="7a94f-114">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="7a94f-115">425-555-0101</span><span class="sxs-lookup"><span data-stu-id="7a94f-115">425-555-0101</span></span> |
| <span data-ttu-id="7a94f-116">Smith</span><span class="sxs-lookup"><span data-stu-id="7a94f-116">Smith</span></span> | <span data-ttu-id="7a94f-117">Ben</span><span class="sxs-lookup"><span data-stu-id="7a94f-117">Ben</span></span> | Ben@contoso.com| <span data-ttu-id="7a94f-118">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="7a94f-118">425-555-0102</span></span> |
| <span data-ttu-id="7a94f-119">Smith</span><span class="sxs-lookup"><span data-stu-id="7a94f-119">Smith</span></span> | <span data-ttu-id="7a94f-120">Jeff</span><span class="sxs-lookup"><span data-stu-id="7a94f-120">Jeff</span></span> | Jeff@contoso.com| <span data-ttu-id="7a94f-121">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="7a94f-121">425-555-0104</span></span> | 

<span data-ttu-id="7a94f-122">因為 Azure Cosmos DB 與 hello Azure 資料表儲存體 Api 相容，請參閱 [查詢資料表和實體] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) 如需如何使用 tooquery hello 詳細資料應用程式開發介面的資料表。</span><span class="sxs-lookup"><span data-stu-id="7a94f-122">Because Azure Cosmos DB is compatible with hello Azure Table storage APIs, see [Querying Tables and Entities] (https://docs.microsoft.com/rest/api/storageservices/fileservices/querying-tables-and-entities) for details on how tooquery by using hello Table API.</span></span> 

<span data-ttu-id="7a94f-123">如需有關 Azure Cosmos DB 所提供的 hello 高階功能的詳細資訊，請參閱[Azure Cosmos DB： 表格 API](table-introduction.md)和[以 hello 表格 API 在.NET 開發](tutorial-develop-table-dotnet.md)。</span><span class="sxs-lookup"><span data-stu-id="7a94f-123">For more information on hello premium capabilities that Azure Cosmos DB offers, see [Azure Cosmos DB: Table API](table-introduction.md) and [Develop with hello Table API in .NET](tutorial-develop-table-dotnet.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7a94f-124">必要條件</span><span class="sxs-lookup"><span data-stu-id="7a94f-124">Prerequisites</span></span>

<span data-ttu-id="7a94f-125">這些查詢 toowork，您必須擁有 Azure Cosmos DB 帳戶，而且具有 hello 容器中的實體資料。</span><span class="sxs-lookup"><span data-stu-id="7a94f-125">For these queries toowork, you must have an Azure Cosmos DB account and have entity data in hello container.</span></span> <span data-ttu-id="7a94f-126">不符合上述其中任何一項條件嗎？</span><span class="sxs-lookup"><span data-stu-id="7a94f-126">Don't have any of those?</span></span> <span data-ttu-id="7a94f-127">完整的 hello[五分鐘快速入門](https://aka.ms/acdbtnetqs)或 hello[開發人員教學課程](https://aka.ms/acdbtabletut)toocreate 帳戶，並填入您的資料庫。</span><span class="sxs-lookup"><span data-stu-id="7a94f-127">Complete hello [five-minute quickstart](https://aka.ms/acdbtnetqs) or hello [developer tutorial](https://aka.ms/acdbtabletut) toocreate an account and populate your database.</span></span>

## <a name="query-on-partitionkey-and-rowkey"></a><span data-ttu-id="7a94f-128">在 PartitionKey 和 RowKey 上執行查詢</span><span class="sxs-lookup"><span data-stu-id="7a94f-128">Query on PartitionKey and RowKey</span></span>
<span data-ttu-id="7a94f-129">因為 hello PartitionKey 和 RowKey 屬性會構成實體主索引鍵，您可以使用下列特殊語法 tooidentify hello 實體 hello:</span><span class="sxs-lookup"><span data-stu-id="7a94f-129">Because hello PartitionKey and RowKey properties form an entity's primary key, you can use hello following special syntax tooidentify hello entity:</span></span> 

<span data-ttu-id="7a94f-130">**查詢**</span><span class="sxs-lookup"><span data-stu-id="7a94f-130">**Query**</span></span>

```
https://<mytableendpoint>/People(PartitionKey='Harp',RowKey='Walter')  
```
<span data-ttu-id="7a94f-131">**結果**</span><span class="sxs-lookup"><span data-stu-id="7a94f-131">**Results**</span></span>

| <span data-ttu-id="7a94f-132">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="7a94f-132">PartitionKey</span></span> | <span data-ttu-id="7a94f-133">RowKey</span><span class="sxs-lookup"><span data-stu-id="7a94f-133">RowKey</span></span> | <span data-ttu-id="7a94f-134">電子郵件</span><span class="sxs-lookup"><span data-stu-id="7a94f-134">Email</span></span> | <span data-ttu-id="7a94f-135">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="7a94f-135">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7a94f-136">Harp</span><span class="sxs-lookup"><span data-stu-id="7a94f-136">Harp</span></span> | <span data-ttu-id="7a94f-137">Walter</span><span class="sxs-lookup"><span data-stu-id="7a94f-137">Walter</span></span> | Walter@contoso.com| <span data-ttu-id="7a94f-138">425-555-0104</span><span class="sxs-lookup"><span data-stu-id="7a94f-138">425-555-0104</span></span> |

<span data-ttu-id="7a94f-139">或者，您可以指定這些屬性一部分 hello`$filter`選項，hello 之後 > 一節中所示。</span><span class="sxs-lookup"><span data-stu-id="7a94f-139">Alternatively, you can specify these properties as part of hello `$filter` option, as shown in hello following section.</span></span> <span data-ttu-id="7a94f-140">請注意 hello 索引鍵屬性名稱和常數值會區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="7a94f-140">Note that hello key property names and constant values are case-sensitive.</span></span> <span data-ttu-id="7a94f-141">Hello PartitionKey 和 RowKey 屬性為字串類型。</span><span class="sxs-lookup"><span data-stu-id="7a94f-141">Both hello PartitionKey and RowKey properties are of type String.</span></span> 

## <a name="query-by-using-an-odata-filter"></a><span data-ttu-id="7a94f-142">使用 OData 篩選進行查詢</span><span class="sxs-lookup"><span data-stu-id="7a94f-142">Query by using an OData filter</span></span>
<span data-ttu-id="7a94f-143">建構篩選字串時，請牢記下列規則：</span><span class="sxs-lookup"><span data-stu-id="7a94f-143">When you're constructing a filter string, keep these rules in mind:</span></span> 

* <span data-ttu-id="7a94f-144">使用 hello hello OData 通訊協定規格 toocompare 屬性 tooa 值所定義的邏輯運算子。</span><span class="sxs-lookup"><span data-stu-id="7a94f-144">Use hello logical operators defined by hello OData Protocol Specification toocompare a property tooa value.</span></span> <span data-ttu-id="7a94f-145">請注意您無法比較屬性 tooa 動態值。</span><span class="sxs-lookup"><span data-stu-id="7a94f-145">Note that you can't compare a property tooa dynamic value.</span></span> <span data-ttu-id="7a94f-146">Hello 運算式的一端必須是常數。</span><span class="sxs-lookup"><span data-stu-id="7a94f-146">One side of hello expression must be a constant.</span></span> 
* <span data-ttu-id="7a94f-147">hello 屬性名稱、 運算子和常數值都必須以 URL 編碼的空格分隔。</span><span class="sxs-lookup"><span data-stu-id="7a94f-147">hello property name, operator, and constant value must be separated by URL-encoded spaces.</span></span> <span data-ttu-id="7a94f-148">空格經 URL 編碼後會變成 `%20`。</span><span class="sxs-lookup"><span data-stu-id="7a94f-148">A space is URL-encoded as `%20`.</span></span> 
* <span data-ttu-id="7a94f-149">Hello 篩選字串的所有部分都都區分大小寫的。</span><span class="sxs-lookup"><span data-stu-id="7a94f-149">All parts of hello filter string are case-sensitive.</span></span> 
* <span data-ttu-id="7a94f-150">hello hello 常值必須是相同的資料類型作為 hello 篩選 tooreturn 有效結果的順序中的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="7a94f-150">hello constant value must be of hello same data type as hello property in order for hello filter tooreturn valid results.</span></span> <span data-ttu-id="7a94f-151">如需支援的屬性類型的詳細資訊，請參閱[了解 hello 表格服務資料模型](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model)。</span><span class="sxs-lookup"><span data-stu-id="7a94f-151">For more information about supported property types, see [Understanding hello Table Service Data Model](https://docs.microsoft.com/rest/api/storageservices/understanding-the-table-service-data-model).</span></span> 

<span data-ttu-id="7a94f-152">以下是一個範例查詢示範如何透過 toofilter hello PartitionKey，和使用 OData 的電子郵件內容`$filter`。</span><span class="sxs-lookup"><span data-stu-id="7a94f-152">Here's an example query that shows how toofilter by hello PartitionKey and Email properties by using an OData `$filter`.</span></span>

<span data-ttu-id="7a94f-153">**查詢**</span><span class="sxs-lookup"><span data-stu-id="7a94f-153">**Query**</span></span>

```
https://<mytableapi-endpoint>/People()?$filter=PartitionKey%20eq%20'Smith'%20and%20Email%20eq%20'Ben@contoso.com'
```

<span data-ttu-id="7a94f-154">如需有關如何 tooconstruct 篩選運算式的各種資料類型的詳細資訊，請參閱[查詢資料表和實體](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities)。</span><span class="sxs-lookup"><span data-stu-id="7a94f-154">For more information on how tooconstruct filter expressions for various data types, see [Querying Tables and Entities](https://docs.microsoft.com/rest/api/storageservices/querying-tables-and-entities).</span></span>

<span data-ttu-id="7a94f-155">**結果**</span><span class="sxs-lookup"><span data-stu-id="7a94f-155">**Results**</span></span>

| <span data-ttu-id="7a94f-156">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="7a94f-156">PartitionKey</span></span> | <span data-ttu-id="7a94f-157">RowKey</span><span class="sxs-lookup"><span data-stu-id="7a94f-157">RowKey</span></span> | <span data-ttu-id="7a94f-158">電子郵件</span><span class="sxs-lookup"><span data-stu-id="7a94f-158">Email</span></span> | <span data-ttu-id="7a94f-159">PhoneNumber</span><span class="sxs-lookup"><span data-stu-id="7a94f-159">PhoneNumber</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="7a94f-160">Ben</span><span class="sxs-lookup"><span data-stu-id="7a94f-160">Ben</span></span> |<span data-ttu-id="7a94f-161">Smith</span><span class="sxs-lookup"><span data-stu-id="7a94f-161">Smith</span></span> | Ben@contoso.com| <span data-ttu-id="7a94f-162">425-555-0102</span><span class="sxs-lookup"><span data-stu-id="7a94f-162">425-555-0102</span></span> |

## <a name="query-by-using-linq"></a><span data-ttu-id="7a94f-163">使用 LINQ 進行查詢</span><span class="sxs-lookup"><span data-stu-id="7a94f-163">Query by using LINQ</span></span> 
<span data-ttu-id="7a94f-164">您也可以藉由將轉譯 toohello 相對應的 OData 查詢運算式的 LINQ 查詢。</span><span class="sxs-lookup"><span data-stu-id="7a94f-164">You can also query by using LINQ, which translates toohello corresponding OData query expressions.</span></span> <span data-ttu-id="7a94f-165">以下是如何利用 toobuild 查詢 hello.NET SDK 的範例：</span><span class="sxs-lookup"><span data-stu-id="7a94f-165">Here's an example of how toobuild queries by using hello .NET SDK:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="7a94f-166">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a94f-166">Next steps</span></span>

<span data-ttu-id="7a94f-167">在本教學課程中，您們 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="7a94f-167">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7a94f-168">了解如何使用 tooquery hello 表格 API （預覽）</span><span class="sxs-lookup"><span data-stu-id="7a94f-168">Learned how tooquery by using hello Table API (preview)</span></span> 

<span data-ttu-id="7a94f-169">您現在可以如何繼續 toohello 下一個教學課程 toolearn toodistribute 資料全域。</span><span class="sxs-lookup"><span data-stu-id="7a94f-169">You can now proceed toohello next tutorial toolearn how toodistribute your data globally.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7a94f-170">全域散發您的資料</span><span class="sxs-lookup"><span data-stu-id="7a94f-170">Distribute your data globally</span></span>](tutorial-global-distribution-documentdb.md)
