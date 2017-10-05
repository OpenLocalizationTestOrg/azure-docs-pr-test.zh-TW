---
title: "Azure 儲存體資料表設計指南 | Microsoft Docs"
description: "在 Azure 資料表儲存體中設計可擴充且高效能的資料表"
services: storage
documentationcenter: na
author: jasonnewyork
manager: tadb
editor: tysonn
ms.assetid: 8e228b0c-2998-4462-8101-9f16517393ca
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 02/28/2017
ms.author: jahogg
ms.openlocfilehash: 5ddb234cc97b3113ec865f97195c871b9f2f40d3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-table-design-guide-designing-scalable-and-performant-tables"></a><span data-ttu-id="a06c2-103">Azure 儲存體資料表設計指南：設計可調整且效用佳的資料表</span><span class="sxs-lookup"><span data-stu-id="a06c2-103">Azure Storage Table Design Guide: Designing Scalable and Performant Tables</span></span>
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="a06c2-104">若要設計可擴充且高效能的資料表，您必須考慮許多因素，例如效能、延展性和成本。</span><span class="sxs-lookup"><span data-stu-id="a06c2-104">To design scalable and performant tables you must consider a number of factors such as performance, scalability, and cost.</span></span> <span data-ttu-id="a06c2-105">如果您先前曾設計關聯式資料庫的結構描述，您對這些考量會很熟悉，但在部分 Azure 資料表服務儲存體模型和關聯式模型之間相似時，將會有許多重大差異。</span><span class="sxs-lookup"><span data-stu-id="a06c2-105">If you have previously designed schemas for relational databases, these considerations will be familiar to you, but while there are some similarities between the Azure Table service storage model and relational models, there are also many important differences.</span></span> <span data-ttu-id="a06c2-106">這些差異常會導致非常不同的設計，看起來可能違反直覺性，或讓熟悉關聯式資料庫的人覺得不對勁，但如果您設計的是 NoSQL 索引鍵/值存放區 (例如 Azure 資料表服務)，這就顯得合理了。</span><span class="sxs-lookup"><span data-stu-id="a06c2-106">These differences typically lead to very different designs that may look counter-intuitive or wrong to someone familiar with relational databases, but which do make good sense if you are designing for a NoSQL key/value store such as the Azure Table service.</span></span> <span data-ttu-id="a06c2-107">許多設計差異將會反映表格服務的設計目的是，專門用來支援雲端規模應用程式 (可能包含數十億個資料實體；該實體為關聯式資料庫詞彙中的資料列)，或是支援必須支援極高交易量之資料集的事實：因此，您需要從不同角度思考如何儲存資料，並了解表格服務的運作方式。</span><span class="sxs-lookup"><span data-stu-id="a06c2-107">Many of your design differences will reflect the fact that the Table service is designed to support cloud-scale applications that can contain billions of entities (rows in relational database terminology) of data or for datasets that must support very high transaction volumes: therefore, you need to think differently about how you store your data and understand how the Table service works.</span></span> <span data-ttu-id="a06c2-108">相較於使用關聯式資料庫的方案，設計良好的 NoSQL 資料存放區可以讓您更進一步 (並以較低的成本) 進行調整。</span><span class="sxs-lookup"><span data-stu-id="a06c2-108">A well designed NoSQL data store can enable your solution to scale much further (and at a lower cost) than a solution that uses a relational database.</span></span> <span data-ttu-id="a06c2-109">本指南針對這些主題為您提供協助。</span><span class="sxs-lookup"><span data-stu-id="a06c2-109">This guide helps you with these topics.</span></span>  

## <a name="about-the-azure-table-service"></a><span data-ttu-id="a06c2-110">關於 Azure 資料表服務</span><span class="sxs-lookup"><span data-stu-id="a06c2-110">About the Azure Table service</span></span>
<span data-ttu-id="a06c2-111">本節強調資料表服務的某些重要功能，特別是關於效能和延展性的設計。</span><span class="sxs-lookup"><span data-stu-id="a06c2-111">This section highlights some of the key features of the Table service that are especially relevant to designing for performance and scalability.</span></span> <span data-ttu-id="a06c2-112">如果您是第一次使用 Azure 儲存體和表格服務，請先閱讀 [Microsoft Azure 儲存體簡介](storage-introduction.md)和[以 .NET 開始使用 Azure 表格儲存體](storage-dotnet-how-to-use-tables.md)，再閱讀本文的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="a06c2-112">If you are new to Azure Storage and the Table service, first read [Introduction to Microsoft Azure Storage](storage-introduction.md) and [Get started with Azure Table Storage using .NET](storage-dotnet-how-to-use-tables.md) before reading the remainder of this article.</span></span> <span data-ttu-id="a06c2-113">雖然本指南的焦點是資料表服務，但仍會討論 Azure 佇列和 Blob 服務，以及如何在方案中將它們與資料表服務搭配使用。</span><span class="sxs-lookup"><span data-stu-id="a06c2-113">Although the focus of this guide is on the Table service, it will include some discussion of the Azure Queue and Blob services, and how you might use them along with the Table service in a solution.</span></span>  

<span data-ttu-id="a06c2-114">什麼是資料表服務？</span><span class="sxs-lookup"><span data-stu-id="a06c2-114">What is the Table service?</span></span> <span data-ttu-id="a06c2-115">顧名思義，資料表服務會使用表格格式來儲存資料。</span><span class="sxs-lookup"><span data-stu-id="a06c2-115">As you might expect from the name, the Table service uses a tabular format to store data.</span></span> <span data-ttu-id="a06c2-116">在標準術語中，資料表的每個資料列都代表一個實體，而資料行儲存該實體的各種屬性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-116">In the standard terminology, each row of the table represents an entity, and the columns store the various properties of that entity.</span></span> <span data-ttu-id="a06c2-117">每個實體都有一組金鑰來唯一識別它，且資料表服務會時間戳記資料行追蹤實體上次更新的時間 (這會自動執行，您無法以手動方式用任意值覆寫時間戳記)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-117">Every entity has a pair of keys to uniquely identify it, and a timestamp column that the Table service uses to track when the entity was last updated (this happens automatically and you cannot manually overwrite the timestamp with an arbitrary value).</span></span> <span data-ttu-id="a06c2-118">資料表服務會使用這個上次修改的時間戳記 (LMT) 來管理開放式並行存取。</span><span class="sxs-lookup"><span data-stu-id="a06c2-118">The Table service uses this last-modified timestamp (LMT) to manage optimistic concurrency.</span></span>  

> [!NOTE]
> <span data-ttu-id="a06c2-119">資料表服務 REST API 作業也會傳回它從上次修改的時間戳記 (LMT) 衍生的 **ETag** 值。</span><span class="sxs-lookup"><span data-stu-id="a06c2-119">The Table service REST API operations also return an **ETag** value that it derives from the last-modified timestamp (LMT).</span></span> <span data-ttu-id="a06c2-120">在本文中，我們將交互使用 ETag 和 LMT 詞彙，因為它們參考相同的基礎資料。</span><span class="sxs-lookup"><span data-stu-id="a06c2-120">In this document we will use the terms ETag and LMT interchangeably because they refer to the same underlying data.</span></span>  
> 
> 

<span data-ttu-id="a06c2-121">下列範例說明簡單的資料表設計，用以儲存員工和部門的實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-121">The following example shows a simple table design to store employee and department entities.</span></span> <span data-ttu-id="a06c2-122">本指南稍後說明的許多範例皆以這個簡單的設計為基礎。</span><span class="sxs-lookup"><span data-stu-id="a06c2-122">Many of the examples shown later in this guide are based on this simple design.</span></span>  

<table>
<tr>
<th><span data-ttu-id="a06c2-123">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="a06c2-123">PartitionKey</span></span></th>
<th><span data-ttu-id="a06c2-124">RowKey</span><span class="sxs-lookup"><span data-stu-id="a06c2-124">RowKey</span></span></th>
<th><span data-ttu-id="a06c2-125">Timestamp</span><span class="sxs-lookup"><span data-stu-id="a06c2-125">Timestamp</span></span></th>
<th></th>
</tr>
<tr>
<td><span data-ttu-id="a06c2-126">行銷</span><span class="sxs-lookup"><span data-stu-id="a06c2-126">Marketing</span></span></td>
<td><span data-ttu-id="a06c2-127">00001</span><span class="sxs-lookup"><span data-stu-id="a06c2-127">00001</span></span></td>
<td><span data-ttu-id="a06c2-128">2014-08-22T00:50:32Z</span><span class="sxs-lookup"><span data-stu-id="a06c2-128">2014-08-22T00:50:32Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a06c2-129">FirstName</span><span class="sxs-lookup"><span data-stu-id="a06c2-129">FirstName</span></span></th>
<th><span data-ttu-id="a06c2-130">姓氏</span><span class="sxs-lookup"><span data-stu-id="a06c2-130">LastName</span></span></th>
<th><span data-ttu-id="a06c2-131">年齡</span><span class="sxs-lookup"><span data-stu-id="a06c2-131">Age</span></span></th>
<th><span data-ttu-id="a06c2-132">電子郵件</span><span class="sxs-lookup"><span data-stu-id="a06c2-132">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="a06c2-133">Don</span><span class="sxs-lookup"><span data-stu-id="a06c2-133">Don</span></span></td>
<td><span data-ttu-id="a06c2-134">Hall</span><span class="sxs-lookup"><span data-stu-id="a06c2-134">Hall</span></span></td>
<td><span data-ttu-id="a06c2-135">34</span><span class="sxs-lookup"><span data-stu-id="a06c2-135">34</span></span></td>
<td>donh@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td><span data-ttu-id="a06c2-136">行銷</span><span class="sxs-lookup"><span data-stu-id="a06c2-136">Marketing</span></span></td>
<td><span data-ttu-id="a06c2-137">00002</span><span class="sxs-lookup"><span data-stu-id="a06c2-137">00002</span></span></td>
<td><span data-ttu-id="a06c2-138">2014-08-22T00:50:34Z</span><span class="sxs-lookup"><span data-stu-id="a06c2-138">2014-08-22T00:50:34Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a06c2-139">FirstName</span><span class="sxs-lookup"><span data-stu-id="a06c2-139">FirstName</span></span></th>
<th><span data-ttu-id="a06c2-140">姓氏</span><span class="sxs-lookup"><span data-stu-id="a06c2-140">LastName</span></span></th>
<th><span data-ttu-id="a06c2-141">年齡</span><span class="sxs-lookup"><span data-stu-id="a06c2-141">Age</span></span></th>
<th><span data-ttu-id="a06c2-142">電子郵件</span><span class="sxs-lookup"><span data-stu-id="a06c2-142">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="a06c2-143">Jun</span><span class="sxs-lookup"><span data-stu-id="a06c2-143">Jun</span></span></td>
<td><span data-ttu-id="a06c2-144">Cao</span><span class="sxs-lookup"><span data-stu-id="a06c2-144">Cao</span></span></td>
<td><span data-ttu-id="a06c2-145">47</span><span class="sxs-lookup"><span data-stu-id="a06c2-145">47</span></span></td>
<td>junc@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td><span data-ttu-id="a06c2-146">行銷</span><span class="sxs-lookup"><span data-stu-id="a06c2-146">Marketing</span></span></td>
<td><span data-ttu-id="a06c2-147">系所</span><span class="sxs-lookup"><span data-stu-id="a06c2-147">Department</span></span></td>
<td><span data-ttu-id="a06c2-148">2014-08-22T00:50:30Z</span><span class="sxs-lookup"><span data-stu-id="a06c2-148">2014-08-22T00:50:30Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a06c2-149">DepartmentName</span><span class="sxs-lookup"><span data-stu-id="a06c2-149">DepartmentName</span></span></th>
<th><span data-ttu-id="a06c2-150">EmployeeCount</span><span class="sxs-lookup"><span data-stu-id="a06c2-150">EmployeeCount</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="a06c2-151">行銷</span><span class="sxs-lookup"><span data-stu-id="a06c2-151">Marketing</span></span></td>
<td><span data-ttu-id="a06c2-152">153</span><span class="sxs-lookup"><span data-stu-id="a06c2-152">153</span></span></td>
</tr>
</table>
</td>
</tr>
<tr>
<td><span data-ttu-id="a06c2-153">銷售</span><span class="sxs-lookup"><span data-stu-id="a06c2-153">Sales</span></span></td>
<td><span data-ttu-id="a06c2-154">00010</span><span class="sxs-lookup"><span data-stu-id="a06c2-154">00010</span></span></td>
<td><span data-ttu-id="a06c2-155">2014-08-22T00:50:44Z</span><span class="sxs-lookup"><span data-stu-id="a06c2-155">2014-08-22T00:50:44Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a06c2-156">FirstName</span><span class="sxs-lookup"><span data-stu-id="a06c2-156">FirstName</span></span></th>
<th><span data-ttu-id="a06c2-157">姓氏</span><span class="sxs-lookup"><span data-stu-id="a06c2-157">LastName</span></span></th>
<th><span data-ttu-id="a06c2-158">年齡</span><span class="sxs-lookup"><span data-stu-id="a06c2-158">Age</span></span></th>
<th><span data-ttu-id="a06c2-159">電子郵件</span><span class="sxs-lookup"><span data-stu-id="a06c2-159">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="a06c2-160">Ken</span><span class="sxs-lookup"><span data-stu-id="a06c2-160">Ken</span></span></td>
<td><span data-ttu-id="a06c2-161">Kwok</span><span class="sxs-lookup"><span data-stu-id="a06c2-161">Kwok</span></span></td>
<td><span data-ttu-id="a06c2-162">23</span><span class="sxs-lookup"><span data-stu-id="a06c2-162">23</span></span></td>
<td>kenk@contoso.com</td>
</tr>
</table>
</td>
</tr>
</table>


<span data-ttu-id="a06c2-163">到目前為止，這看起來非常類似於關聯式資料庫中的資料表，主要差異在於必要資料行，並在相同資料表中儲存多個實體類型的能力。</span><span class="sxs-lookup"><span data-stu-id="a06c2-163">So far, this looks very similar to a table in a relational database with the key differences being the mandatory columns, and the ability to store multiple entity types in the same table.</span></span> <span data-ttu-id="a06c2-164">此外，每個使用者定義屬性 (例如**名字**或**年齡**) 皆具有資料類型，例如整數或字串，就像關聯式資料庫中的資料行。</span><span class="sxs-lookup"><span data-stu-id="a06c2-164">In addition, each of the user-defined properties such as **FirstName** or **Age** has a data type, such as integer or string, just like a column in a relational database.</span></span> <span data-ttu-id="a06c2-165">雖然不同於關聯式資料庫，但資料表服務的無結構描述本質意味著一個屬性在每個實體上不需要相同的資料類型。</span><span class="sxs-lookup"><span data-stu-id="a06c2-165">Although unlike in a relational database, the schema-less nature of the Table service means that a property need not have the same data type on each entity.</span></span> <span data-ttu-id="a06c2-166">若要將複雜資料類型儲存在單一屬性中，您必須使用序列化格式，例如 JSON 或 XML。</span><span class="sxs-lookup"><span data-stu-id="a06c2-166">To store complex data types in a single property, you must use a serialized format such as JSON or XML.</span></span> <span data-ttu-id="a06c2-167">如需表格服務 (例如支援的資料類型、支援的日期範圍、命名規則和大小限制) 的詳細資訊，請參閱 [了解表格服務資料模型](http://msdn.microsoft.com/library/azure/dd179338.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-167">For more information about the table service such as supported data types, supported date ranges, naming rules, and size constraints, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="a06c2-168">您將會發現，您所選擇的 **PartitionKey** 和 **RowKey** 是良好資料表設計不可或缺的元素。</span><span class="sxs-lookup"><span data-stu-id="a06c2-168">As you will see, your choice of **PartitionKey** and **RowKey** is fundamental to good table design.</span></span> <span data-ttu-id="a06c2-169">儲存在資料表中的每個實體都必須有一個獨一無二的 **PartitionKey** 和 **RowKey** 組合。</span><span class="sxs-lookup"><span data-stu-id="a06c2-169">Every entity stored in a table must have a unique combination of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="a06c2-170">如同關聯式資料庫資料表中的索引鍵，系統會為 **PartitionKey** 和 **RowKey** 的值編製索引以建立叢集索引，此索引可用於快速查閱；不過，表格服務不會建立任何次要索引，因此已編製索引的屬性就只有這兩個 (稍後說明的某些模式將示範如何解決這項表面上的限制)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-170">As with keys in a relational database table, the **PartitionKey** and **RowKey** values are indexed to create a clustered index that enables fast look-ups; however, the Table service does not create any secondary indexes so these are the only two indexed properties (some of the patterns described later show how you can work around this apparent limitation).</span></span>  

<span data-ttu-id="a06c2-171">資料表由一或多個分割所組成，您將會發現，您所做的許多設計決策都牽涉到必須選擇適合的 **PartitionKey** 和 **RowKey** 以最佳化解決方案。</span><span class="sxs-lookup"><span data-stu-id="a06c2-171">A table is made up of one or more partitions, and as you will see, many of the design decisions you make will be around choosing a suitable **PartitionKey** and **RowKey** to optimize your solution.</span></span> <span data-ttu-id="a06c2-172">方案可以僅由單一資料表組成 (其中組織成資料分割的所有實體)，但方案通常會有多個資料表。</span><span class="sxs-lookup"><span data-stu-id="a06c2-172">A solution could consist of just a single table that contains all your entities organized into partitions, but typically a solution will have multiple tables.</span></span> <span data-ttu-id="a06c2-173">資料表可幫助您以邏輯方式組織您的實體，幫助您使用存取控制清單管理資料的存取，而且您可以使用單一儲存體作業放置整個資料表。</span><span class="sxs-lookup"><span data-stu-id="a06c2-173">Tables help you to logically organize your entities, help you manage access to the data using access control lists, and you can drop an entire table using a single storage operation.</span></span>  

### <a name="table-partitions"></a><span data-ttu-id="a06c2-174">資料表的資料分割</span><span class="sxs-lookup"><span data-stu-id="a06c2-174">Table partitions</span></span>
<span data-ttu-id="a06c2-175">帳戶名稱、資料表名稱和 **PartitionKey** 這三個項目可共同識表格服務儲存實體之儲存體服務中的分割。</span><span class="sxs-lookup"><span data-stu-id="a06c2-175">The account name, table name and **PartitionKey** together identify the partition within the storage service where the table service stores the entity.</span></span> <span data-ttu-id="a06c2-176">分割也同時是實體的定址配置的一部分，可定義交易的範圍 (請參閱下方的 [實體群組交易](#entity-group-transactions) )，並打造表格服務調整方式的基礎。</span><span class="sxs-lookup"><span data-stu-id="a06c2-176">As well as being part of the addressing scheme for entities, partitions define a scope for transactions (see [Entity Group Transactions](#entity-group-transactions) below), and form the basis of how the table service scales.</span></span> <span data-ttu-id="a06c2-177">如需分割的詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](storage-scalability-targets.md)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-177">For more information on partitions see [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span>  

<span data-ttu-id="a06c2-178">在資料表服務中，個別節點可為一或多個完整資料分割提供服務，且服務會透過動態的負載平衡資料分割在節點間進行調整。</span><span class="sxs-lookup"><span data-stu-id="a06c2-178">In the Table service, an individual node services one or more complete partitions and the service scales by dynamically load-balancing partitions across nodes.</span></span> <span data-ttu-id="a06c2-179">如果某節點的負載過大，表格服務可將由該節點提供服務的分割範圍*分割*到不同的節點；當流量變小時，服務可將分割範圍從靜止節點*合併*回單一節點。</span><span class="sxs-lookup"><span data-stu-id="a06c2-179">If a node is under load, the table service can *split* the range of partitions serviced by that node onto different nodes; when traffic subsides, the service can *merge* the partition ranges from quiet nodes back onto a single node.</span></span>  

<span data-ttu-id="a06c2-180">如需表格服務之內部詳細資料的詳細資訊 (特別是服務管理分割的方式)，請參閱文件 [Microsoft Azure 儲存體：具有高度一致性的高可用性雲端儲存體服務](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-180">For more information about the internal details of the Table service, and in particular how the service manages partitions, see the paper [Microsoft Azure Storage: A Highly Available Cloud Storage Service with Strong Consistency](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).</span></span>  

### <a name="entity-group-transactions"></a><span data-ttu-id="a06c2-181">實體群組交易</span><span class="sxs-lookup"><span data-stu-id="a06c2-181">Entity Group Transactions</span></span>
<span data-ttu-id="a06c2-182">在資料表服務中，實體群組交易 (EGT) 是唯一的內建機制，可跨越多個實體執行不可部分完成的更新。</span><span class="sxs-lookup"><span data-stu-id="a06c2-182">In the Table service, Entity Group Transactions (EGTs) are the only built-in mechanism for performing atomic updates across multiple entities.</span></span> <span data-ttu-id="a06c2-183">在某些文件中，EGT 也稱為 *批次交易* 。</span><span class="sxs-lookup"><span data-stu-id="a06c2-183">EGTs are also referred to as *batch transactions* in some documentation.</span></span> <span data-ttu-id="a06c2-184">EGT 只能對儲存在相同資料分割中的實體運作 (共用給定資料表中的相同資料分割索引鍵)，所以每當您需要跨多個實體執行不可部分完成的交易行為時，您必須確保這些實體位於相同的資料分割中。</span><span class="sxs-lookup"><span data-stu-id="a06c2-184">EGTs can only operate on entities stored in the same partition (share the same partition key in a given table), so anytime you need atomic transactional behavior across multiple entities you need to ensure that those entities are in the same partition.</span></span> <span data-ttu-id="a06c2-185">通常就是基於此原因，才需要將多個實體類型放在相同的資料表 (和資料分割) 中，而不讓不同的實體類型使用多個資料表。</span><span class="sxs-lookup"><span data-stu-id="a06c2-185">This is often a reason for keeping multiple entity types in the same table (and partition) and not using multiple tables for different entity types.</span></span> <span data-ttu-id="a06c2-186">單一 EGT 最多可以操作 100 個實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-186">A single EGT can operate on at most 100 entities.</span></span>  <span data-ttu-id="a06c2-187">如果您送出多個並行 EGT 進行處理，請務必確保這些 EGT 不會在 EGT 的通用實體上運作，否則處理可能會延遲。</span><span class="sxs-lookup"><span data-stu-id="a06c2-187">If you submit multiple concurrent EGTs for processing it is important to ensure  those EGTs do not operate on entities that are common across EGTs as otherwise processing can be delayed.</span></span>

<span data-ttu-id="a06c2-188">EGT 也可能讓您必須評估並取捨您的設計：使用多個資料分割會增加應用程式的延展性，因為 Azure 有更多可能在各節點間要求負載平衡，但這可能會限制您的應用程式執行不可部分完成的交易和為資料維護穩固一致性的能力。</span><span class="sxs-lookup"><span data-stu-id="a06c2-188">EGTs also introduce a potential trade-off for you to evaluate in your design: using more partitions will increase the scalability of your application because Azure has more opportunities for load balancing requests across nodes, but this might limit the ability of your application to perform atomic transactions and maintain strong consistency for your data.</span></span> <span data-ttu-id="a06c2-189">此外，磁碟分割層級上有特定的延展性目標可能會限制您使用單一節點時的交易輸送量：如需 Azure 儲存體帳戶和表格服務延展性目標的詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](storage-scalability-targets.md)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-189">Furthermore, there are specific scalability targets at the level of a partition that might limit the throughput of transactions you can expect for a single node: for more information about the scalability targets for Azure storage accounts and the table service, see [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="a06c2-190">本指南後續幾節將討論各種設計策略，以協助您管理這類的權衡，並討論如何根據您用戶端應用程式的特定需求，選擇您的資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="a06c2-190">Later sections of this guide discuss various design strategies that help you manage trade-offs such as this one, and discuss how best to choose your partition key based on the specific requirements of your client application.</span></span>  

### <a name="capacity-considerations"></a><span data-ttu-id="a06c2-191">容量考量</span><span class="sxs-lookup"><span data-stu-id="a06c2-191">Capacity considerations</span></span>
<span data-ttu-id="a06c2-192">下表包含您在設計資料表服務方案時所需注意的某些索引鍵值：</span><span class="sxs-lookup"><span data-stu-id="a06c2-192">The following table includes some of the key values to be aware of when you are designing a Table service solution:</span></span>  

| <span data-ttu-id="a06c2-193">Azure 儲存體帳戶的容量總計</span><span class="sxs-lookup"><span data-stu-id="a06c2-193">Total capacity of an Azure storage account</span></span> | <span data-ttu-id="a06c2-194">500 TB</span><span class="sxs-lookup"><span data-stu-id="a06c2-194">500 TB</span></span> |
| --- | --- |
| <span data-ttu-id="a06c2-195">Azure 儲存體帳戶中的資料表數目</span><span class="sxs-lookup"><span data-stu-id="a06c2-195">Number of tables in an Azure storage account</span></span> |<span data-ttu-id="a06c2-196">僅受限於儲存體帳戶的容量</span><span class="sxs-lookup"><span data-stu-id="a06c2-196">Limited only by the capacity of the storage account</span></span> |
| <span data-ttu-id="a06c2-197">資料表中的資料分割數目</span><span class="sxs-lookup"><span data-stu-id="a06c2-197">Number of partitions in a table</span></span> |<span data-ttu-id="a06c2-198">僅受限於儲存體帳戶的容量</span><span class="sxs-lookup"><span data-stu-id="a06c2-198">Limited only by the capacity of the storage account</span></span> |
| <span data-ttu-id="a06c2-199">資料分割中的實體數目</span><span class="sxs-lookup"><span data-stu-id="a06c2-199">Number of entities in a partition</span></span> |<span data-ttu-id="a06c2-200">僅受限於儲存體帳戶的容量</span><span class="sxs-lookup"><span data-stu-id="a06c2-200">Limited only by the capacity of the storage account</span></span> |
| <span data-ttu-id="a06c2-201">個別實體的大小</span><span class="sxs-lookup"><span data-stu-id="a06c2-201">Size of an individual entity</span></span> |<span data-ttu-id="a06c2-202">最多 1 MB 和 255 個屬性 (包括 **PartitionKey**、**RowKey** 和 **Timestamp**)</span><span class="sxs-lookup"><span data-stu-id="a06c2-202">Up to 1 MB with a maximum of 255 properties (including the **PartitionKey**, **RowKey**, and **Timestamp**)</span></span> |
| <span data-ttu-id="a06c2-203">**PartitionKey**</span><span class="sxs-lookup"><span data-stu-id="a06c2-203">Size of the **PartitionKey**</span></span> |<span data-ttu-id="a06c2-204">大小最多 1 KB 的字串</span><span class="sxs-lookup"><span data-stu-id="a06c2-204">A string up to 1 KB in size</span></span> |
| <span data-ttu-id="a06c2-205">**RowKey**</span><span class="sxs-lookup"><span data-stu-id="a06c2-205">Size of the **RowKey**</span></span> |<span data-ttu-id="a06c2-206">大小最多 1 KB 的字串</span><span class="sxs-lookup"><span data-stu-id="a06c2-206">A string up to 1 KB in size</span></span> |
| <span data-ttu-id="a06c2-207">實體群組交易的大小</span><span class="sxs-lookup"><span data-stu-id="a06c2-207">Size of an Entity Group Transaction</span></span> |<span data-ttu-id="a06c2-208">交易最多可以包含 100 個實體，而承載大小必須小於 4 MB。</span><span class="sxs-lookup"><span data-stu-id="a06c2-208">A transaction can include at most 100 entities and the payload must be less than 4 MB in size.</span></span> <span data-ttu-id="a06c2-209">一個 EGT 只能更新實體一次。</span><span class="sxs-lookup"><span data-stu-id="a06c2-209">An EGT can only update an entity once.</span></span> |

<span data-ttu-id="a06c2-210">如需詳細資訊，請參閱 [了解表格服務資料模型](http://msdn.microsoft.com/library/azure/dd179338.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-210">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>  

### <a name="cost-considerations"></a><span data-ttu-id="a06c2-211">成本考量</span><span class="sxs-lookup"><span data-stu-id="a06c2-211">Cost considerations</span></span>
<span data-ttu-id="a06c2-212">資料表儲存體比較便宜，但您在評估任何會使用資料表服務的方案時，均應將容量使用量和交易數目的成本預估同時納入考量。</span><span class="sxs-lookup"><span data-stu-id="a06c2-212">Table storage is relatively inexpensive, but you should include cost estimates for both capacity usage and the quantity of transactions as part of your evaluation of any solution that uses the Table service.</span></span> <span data-ttu-id="a06c2-213">不過，在許多情況下，儲存反正規化或重複的資料以改善方案的效能或延展性，也是可以採行的有效措施。</span><span class="sxs-lookup"><span data-stu-id="a06c2-213">However, in many scenarios storing denormalized or duplicate data in order to improve the performance or scalability of your solution is a valid approach to take.</span></span> <span data-ttu-id="a06c2-214">如需定價的詳細資訊，請參閱 [Azure 儲存體定價](https://azure.microsoft.com/pricing/details/storage/)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-214">For more information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>  

## <a name="guidelines-for-table-design"></a><span data-ttu-id="a06c2-215">資料表設計指導方針</span><span class="sxs-lookup"><span data-stu-id="a06c2-215">Guidelines for table design</span></span>
<span data-ttu-id="a06c2-216">這些清單摘要了一些設計資料表時應牢記的重要方針，而本指南稍後將會逐一詳細說明。</span><span class="sxs-lookup"><span data-stu-id="a06c2-216">These lists summarize some of the key guidelines you should keep in mind when you are designing your tables, and this guide will address them all in more detail later in.</span></span> <span data-ttu-id="a06c2-217">這些方針與您往常設計關聯式資料庫時遵循的方針非常不同。</span><span class="sxs-lookup"><span data-stu-id="a06c2-217">These guidelines are very different from the guidelines you would typically follow for relational database design.</span></span>  

<span data-ttu-id="a06c2-218">將表格服務解決方案設計為易於 *讀取* ：</span><span class="sxs-lookup"><span data-stu-id="a06c2-218">Designing your Table service solution to be *read* efficient:</span></span>

* <span data-ttu-id="a06c2-219">***設計大量讀取應用程式中的查詢。***</span><span class="sxs-lookup"><span data-stu-id="a06c2-219">***Design for querying in read-heavy applications.***</span></span> <span data-ttu-id="a06c2-220">當您在設計資料表時，請先思考您將執行的查詢 (尤其是較無法容續延遲的查詢)，然後再思考更新實體的方法。</span><span class="sxs-lookup"><span data-stu-id="a06c2-220">When you are designing your tables, think about the queries (especially the latency sensitive ones) that you will execute before you think about how you will update your entities.</span></span> <span data-ttu-id="a06c2-221">透過這樣的方式，通常可造就一個有效率且高效能的解決方案。</span><span class="sxs-lookup"><span data-stu-id="a06c2-221">This typically results in an efficient and performant solution.</span></span>  
* <span data-ttu-id="a06c2-222">***在查詢中同時指定 PartitionKey 和 RowKey。***</span><span class="sxs-lookup"><span data-stu-id="a06c2-222">***Specify both PartitionKey and RowKey in your queries.***</span></span> <span data-ttu-id="a06c2-223">*點查詢* 都是最有效率的表格服務查詢。</span><span class="sxs-lookup"><span data-stu-id="a06c2-223">*Point queries* such as these are the most efficient table service queries.</span></span>  
* <span data-ttu-id="a06c2-224">***考慮儲存重複的實體副本。***</span><span class="sxs-lookup"><span data-stu-id="a06c2-224">***Consider storing duplicate copies of entities.***</span></span> <span data-ttu-id="a06c2-225">資料表儲存體的成本較低，因此請考慮多次儲存相同的實體 (使用不同索引鍵)，以啟用更有效率的查詢。</span><span class="sxs-lookup"><span data-stu-id="a06c2-225">Table storage is cheap so consider storing the same entity multiple times (with different keys) to enable more efficient queries.</span></span>  
* <span data-ttu-id="a06c2-226">***考慮將資料反正規化。***</span><span class="sxs-lookup"><span data-stu-id="a06c2-226">***Consider denormalizing your data.***</span></span> <span data-ttu-id="a06c2-227">資料表儲存體十分便宜，所以建議您考慮將資料反正規化。</span><span class="sxs-lookup"><span data-stu-id="a06c2-227">Table storage is cheap so consider denormalizing your data.</span></span> <span data-ttu-id="a06c2-228">例如儲存摘要實體，可讓彙總資料的查詢只需存取單一實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-228">For example, store summary entities so that queries for aggregate data only need to access a single entity.</span></span>  
* <span data-ttu-id="a06c2-229">***使用複合索引鍵值。***</span><span class="sxs-lookup"><span data-stu-id="a06c2-229">***Use compound key values.***</span></span> <span data-ttu-id="a06c2-230">您只有 **PartitionKey** 和 **RowKey** 這兩個索引鍵。</span><span class="sxs-lookup"><span data-stu-id="a06c2-230">The only keys you have are **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="a06c2-231">例如，使用複合索引鍵值啟用替代的實體索引鍵式存取路徑。</span><span class="sxs-lookup"><span data-stu-id="a06c2-231">For example, use compound key values to enable alternate keyed access paths to entities.</span></span>  
* <span data-ttu-id="a06c2-232">***使用查詢預測。***</span><span class="sxs-lookup"><span data-stu-id="a06c2-232">***Use query projection.***</span></span> <span data-ttu-id="a06c2-233">使用僅選取您所需欄位的查詢，即可減少透過網路傳輸的資料量。</span><span class="sxs-lookup"><span data-stu-id="a06c2-233">You can reduce the amount of data that you transfer over the network by using queries that select just the fields you need.</span></span>  

<span data-ttu-id="a06c2-234">將表格服務解決方案設計為易於 *寫入* ：</span><span class="sxs-lookup"><span data-stu-id="a06c2-234">Designing your Table service solution to be *write* efficient:</span></span>  

* <span data-ttu-id="a06c2-235">***不要建立熱分割。***</span><span class="sxs-lookup"><span data-stu-id="a06c2-235">***Do not create hot partitions.***</span></span> <span data-ttu-id="a06c2-236">選擇可讓您在任何時間點，將要求分散到多個分割上的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="a06c2-236">Choose keys that enable you to spread your requests across multiple partitions at any point of time.</span></span>  
* <span data-ttu-id="a06c2-237">***避免流量尖峰。***</span><span class="sxs-lookup"><span data-stu-id="a06c2-237">***Avoid spikes in traffic.***</span></span> <span data-ttu-id="a06c2-238">將流量平均分散到合理的時段，以避免產生流量尖峰。</span><span class="sxs-lookup"><span data-stu-id="a06c2-238">Smooth the traffic over a reasonable period of time and avoid spikes in traffic.</span></span>
* <span data-ttu-id="a06c2-239">***不一定要為每個實體的類型建立個別的資料表。***</span><span class="sxs-lookup"><span data-stu-id="a06c2-239">***Don't necessarily create a separate table for each type of entity.***</span></span> <span data-ttu-id="a06c2-240">需要跨實體類型執行不可部分完成的交易時，您可以在相同資料表的相同分割中儲存多個實體類型。</span><span class="sxs-lookup"><span data-stu-id="a06c2-240">When you require atomic transactions across entity types, you can store these multiple entity types in the same partition in the same table.</span></span>
* <span data-ttu-id="a06c2-241">***考慮必須達到的最大輸送量。***</span><span class="sxs-lookup"><span data-stu-id="a06c2-241">***Consider the maximum throughput you must achieve.***</span></span> <span data-ttu-id="a06c2-242">您必須留意資料表服務的延展性目標，並確保您的設計不會超過目標。</span><span class="sxs-lookup"><span data-stu-id="a06c2-242">You must be aware of the scalability targets for the Table service and ensure that your design will not cause you to exceed them.</span></span>  

<span data-ttu-id="a06c2-243">當您閱讀本指南時，您會看到將這些原則全都納入實作的範例。</span><span class="sxs-lookup"><span data-stu-id="a06c2-243">As you read this guide, you will see examples that put all of these principles into practice.</span></span>  

## <a name="design-for-querying"></a><span data-ttu-id="a06c2-244">查詢的設計</span><span class="sxs-lookup"><span data-stu-id="a06c2-244">Design for querying</span></span>
<span data-ttu-id="a06c2-245">資料表服務方案可以是讀取密集、寫入密集或兩者混合的方案。</span><span class="sxs-lookup"><span data-stu-id="a06c2-245">Table service solutions may be read intensive, write intensive, or a mix of the two.</span></span> <span data-ttu-id="a06c2-246">本節主要說明您在設計資料表服務以有效地支援讀取作業時應謹記在心的事項。</span><span class="sxs-lookup"><span data-stu-id="a06c2-246">This section focuses on the things to bear in mind when you are designing your Table service to support read operations efficiently.</span></span> <span data-ttu-id="a06c2-247">一般而言，支援有效讀取作業的設計，也可兼顧寫入作業的效率。</span><span class="sxs-lookup"><span data-stu-id="a06c2-247">Typically, a design that supports read operations efficiently is also efficient for write operations.</span></span> <span data-ttu-id="a06c2-248">不過，設計支援寫入作業時還有其他考量必須牢記在心，這將在下一節 [資料修改的設計](#design-for-data-modification)中說明這些考量。</span><span class="sxs-lookup"><span data-stu-id="a06c2-248">However, there are additional considerations to bear in mind when designing to support write operations, discussed in the next section, [Design for data modification](#design-for-data-modification).</span></span>

<span data-ttu-id="a06c2-249">要設計資料表服務方案，讓您能夠有效率地讀取資料，您首先可以自問：「我的應用程式需要執行何種查詢以從資料表服務中擷取它所需要的資料？」</span><span class="sxs-lookup"><span data-stu-id="a06c2-249">A good starting point for designing your Table service solution to enable you to read data efficiently is to ask "What queries will my application need to execute to retrieve the data it needs from the Table service?"</span></span>  

> [!NOTE]
> <span data-ttu-id="a06c2-250">使用資料表服務時，事先做出正確的設計是很重要的，因為事後要更改不僅困難，也很昂貴。</span><span class="sxs-lookup"><span data-stu-id="a06c2-250">With the Table service, it's important to get the design correct up front because it's difficult and expensive to change it later.</span></span> <span data-ttu-id="a06c2-251">例如，在關聯式資料庫中，通常只要藉由將索引新增至現有的資料庫，就可以解決效能問題：這對於資料表服務是行不通的。</span><span class="sxs-lookup"><span data-stu-id="a06c2-251">For example, in a relational database it's often possible to address performance issues simply by adding indexes to an existing database: this is not an option with the Table service.</span></span>  
> 
> 

<span data-ttu-id="a06c2-252">本節主要討論您在設計查詢資料表時所須解決的重要問題。</span><span class="sxs-lookup"><span data-stu-id="a06c2-252">This section focuses on the key issues you must address when you design your tables for querying.</span></span> <span data-ttu-id="a06c2-253">本節所涵蓋的主題包括：</span><span class="sxs-lookup"><span data-stu-id="a06c2-253">The topics covered in this section include:</span></span>

* [<span data-ttu-id="a06c2-254">您選擇的 PartitionKey 和 RowKey 對查詢效能有何影響</span><span class="sxs-lookup"><span data-stu-id="a06c2-254">How your choice of PartitionKey and RowKey impacts query performance</span></span>](#how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance)
* [<span data-ttu-id="a06c2-255">選擇適當的 PartitionKey</span><span class="sxs-lookup"><span data-stu-id="a06c2-255">Choosing an appropriate PartitionKey</span></span>](#choosing-an-appropriate-partitionkey)
* [<span data-ttu-id="a06c2-256">最佳化資料表服務的查詢</span><span class="sxs-lookup"><span data-stu-id="a06c2-256">Optimizing queries for the Table service</span></span>](#optimizing-queries-for-the-table-service)
* [<span data-ttu-id="a06c2-257">在表格服務中排序資料</span><span class="sxs-lookup"><span data-stu-id="a06c2-257">Sorting data in the Table service</span></span>](#sorting-data-in-the-table-service)

### <a name="how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance"></a><span data-ttu-id="a06c2-258">您選擇的 PartitionKey 和 RowKey 對查詢效能有何影響</span><span class="sxs-lookup"><span data-stu-id="a06c2-258">How your choice of PartitionKey and RowKey impacts query performance</span></span>
<span data-ttu-id="a06c2-259">下列範例假設表格服務會以下列結構儲存員工實體 (為求簡潔，大部分的範例皆省略 **Timestamp** 屬性)：</span><span class="sxs-lookup"><span data-stu-id="a06c2-259">The following examples assume the table service is storing employee entities with the following structure (most of the examples omit the **Timestamp** property for clarity):</span></span>  

| <span data-ttu-id="a06c2-260">*資料行名稱*</span><span class="sxs-lookup"><span data-stu-id="a06c2-260">*Column name*</span></span> | <span data-ttu-id="a06c2-261">*資料類型*</span><span class="sxs-lookup"><span data-stu-id="a06c2-261">*Data type*</span></span> |
| --- | --- |
| <span data-ttu-id="a06c2-262">**PartitionKey** (部門名稱)</span><span class="sxs-lookup"><span data-stu-id="a06c2-262">**PartitionKey** (Department Name)</span></span> |<span data-ttu-id="a06c2-263">String</span><span class="sxs-lookup"><span data-stu-id="a06c2-263">String</span></span> |
| <span data-ttu-id="a06c2-264">**RowKey** (員工識別碼)</span><span class="sxs-lookup"><span data-stu-id="a06c2-264">**RowKey** (Employee Id)</span></span> |<span data-ttu-id="a06c2-265">String</span><span class="sxs-lookup"><span data-stu-id="a06c2-265">String</span></span> |
| <span data-ttu-id="a06c2-266">**名字**</span><span class="sxs-lookup"><span data-stu-id="a06c2-266">**FirstName**</span></span> |<span data-ttu-id="a06c2-267">String</span><span class="sxs-lookup"><span data-stu-id="a06c2-267">String</span></span> |
| <span data-ttu-id="a06c2-268">**姓氏**</span><span class="sxs-lookup"><span data-stu-id="a06c2-268">**LastName**</span></span> |<span data-ttu-id="a06c2-269">String</span><span class="sxs-lookup"><span data-stu-id="a06c2-269">String</span></span> |
| <span data-ttu-id="a06c2-270">**年齡**</span><span class="sxs-lookup"><span data-stu-id="a06c2-270">**Age**</span></span> |<span data-ttu-id="a06c2-271">Integer</span><span class="sxs-lookup"><span data-stu-id="a06c2-271">Integer</span></span> |
| <span data-ttu-id="a06c2-272">**EmailAddress**</span><span class="sxs-lookup"><span data-stu-id="a06c2-272">**EmailAddress**</span></span> |<span data-ttu-id="a06c2-273">String</span><span class="sxs-lookup"><span data-stu-id="a06c2-273">String</span></span> |

<span data-ttu-id="a06c2-274">先前的章節＜ [Azure 資料表服務概觀](#overview) ＞說明了某些對查詢設計有直接影響的重要 Azure 表格服務功能。</span><span class="sxs-lookup"><span data-stu-id="a06c2-274">The earlier section [Azure Table service overview](#overview) describes some of the key features of the Azure Table service that have a direct influence on designing for query.</span></span> <span data-ttu-id="a06c2-275">這些功能產生了設計資料表服務查詢的一般指導方針。</span><span class="sxs-lookup"><span data-stu-id="a06c2-275">These result in the following general guidelines for designing Table service queries.</span></span> <span data-ttu-id="a06c2-276">請注意，下列範例中使用的篩選語法來自於表格服務 REST API，如需詳細資訊，請參閱 [查詢實體](http://msdn.microsoft.com/library/azure/dd179421.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-276">Note that the filter syntax used in the examples below is from the Table service REST API, for more information see [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span></span>  

* <span data-ttu-id="a06c2-277">***點查詢***是使用上最有效率的查閱，建議用於高容量查閱或只能容許最低延遲的查閱。</span><span class="sxs-lookup"><span data-stu-id="a06c2-277">A ***Point Query*** is the most efficient lookup to use and is recommended to be used for high-volume lookups or lookups requiring lowest latency.</span></span> <span data-ttu-id="a06c2-278">這類查詢使用索引尋找個別實體的效率極高，方法是同時指定 **PartitionKey** 和 **RowKey** 值。</span><span class="sxs-lookup"><span data-stu-id="a06c2-278">Such a query can use the indexes to locate an individual entity very efficiently by specifying both the **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="a06c2-279">例如：$filter=(PartitionKey eq 'Sales') and (RowKey eq '2')</span><span class="sxs-lookup"><span data-stu-id="a06c2-279">For example: $filter=(PartitionKey eq 'Sales') and (RowKey eq '2')</span></span>  
* <span data-ttu-id="a06c2-280">次佳的是***範圍查詢***，它使用 **PartitionKey**，並篩選特定範圍的 **RowKey** 值，以傳回多個實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-280">Second best is a ***Range Query*** that uses the **PartitionKey** and filters on a range of **RowKey** values to return more than one entity.</span></span> <span data-ttu-id="a06c2-281">**PartitionKey** 值會識別特定的分割，而 **RowKey** 值會識別該分割中實體的子集。</span><span class="sxs-lookup"><span data-stu-id="a06c2-281">The **PartitionKey** value identifies a specific partition, and the **RowKey** values identify a subset of the entities in that partition.</span></span> <span data-ttu-id="a06c2-282">例如：$filter=PartitionKey eq 'Sales' and RowKey ge 'S' and RowKey lt 'T'</span><span class="sxs-lookup"><span data-stu-id="a06c2-282">For example: $filter=PartitionKey eq 'Sales' and RowKey ge 'S' and RowKey lt 'T'</span></span>  
* <span data-ttu-id="a06c2-283">再其次是***分割掃描***，它使用 **PartitionKey**，並篩選另一個非索引鍵的，可傳回多個實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-283">Third best is a ***Partition Scan*** that uses the **PartitionKey** and filters on another non-key property and that may return more than one entity.</span></span> <span data-ttu-id="a06c2-284">**PartitionKey** 值會識別特定的分割，而屬性值會選取該分割中實體的子集。</span><span class="sxs-lookup"><span data-stu-id="a06c2-284">The **PartitionKey** value identifies a specific partition, and the property values select for a subset of the entities in that partition.</span></span> <span data-ttu-id="a06c2-285">例如：$filter=PartitionKey eq 'Sales' and LastName eq 'Smith'</span><span class="sxs-lookup"><span data-stu-id="a06c2-285">For example: $filter=PartitionKey eq 'Sales' and LastName eq 'Smith'</span></span>  
* <span data-ttu-id="a06c2-286">***資料表掃描***不包含 **PartitionKey**，且效率極差，因為它會依序在所有組成資料表的分割中搜尋是否有任何相符的實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-286">A ***Table Scan*** does not include the **PartitionKey** and is very inefficient because it searches all of the partitions that make up your table in turn for any matching entities.</span></span> <span data-ttu-id="a06c2-287">無論您的篩選是否使用 **RowKey**，它都會執行資料表掃描。</span><span class="sxs-lookup"><span data-stu-id="a06c2-287">It will perform a table scan regardless of whether or not your filter uses the **RowKey**.</span></span> <span data-ttu-id="a06c2-288">例如：$filter=LastName eq 'Jones'</span><span class="sxs-lookup"><span data-stu-id="a06c2-288">For example: $filter=LastName eq 'Jones'</span></span>  
* <span data-ttu-id="a06c2-289">傳回多個實體的查詢，在傳回時會以 **PartitionKey** 和 **RowKey** 順序排序。</span><span class="sxs-lookup"><span data-stu-id="a06c2-289">Queries that return multiple entities return them sorted in **PartitionKey** and **RowKey** order.</span></span> <span data-ttu-id="a06c2-290">若要避免重新排序用戶端中的實體，請選擇定義最常見的排序次序的 **RowKey** 。</span><span class="sxs-lookup"><span data-stu-id="a06c2-290">To avoid resorting the entities in the client, choose a **RowKey** that defines the most common sort order.</span></span>  

<span data-ttu-id="a06c2-291">請注意，使用 "**or**" 指定以 **RowKey** 值為基礎的篩選條件，會產生資料分割掃描且不被當作範圍查詢。</span><span class="sxs-lookup"><span data-stu-id="a06c2-291">Note that using an "**or**" to specify a filter based on **RowKey** values results in a partition scan and is not treated as a range query.</span></span> <span data-ttu-id="a06c2-292">因此，您應該避免會使用下列篩選條件的搜尋：例如 $filter=PartitionKey eq 'Sales' and (RowKey eq '121' or RowKey eq '322')</span><span class="sxs-lookup"><span data-stu-id="a06c2-292">Therefore, you should avoid queries that use filters such as: $filter=PartitionKey eq 'Sales' and (RowKey eq '121' or RowKey eq '322')</span></span>  

<span data-ttu-id="a06c2-293">如需使用儲存體用戶端程式庫執行有效率查詢的用戶端程式碼範例，請參閱：</span><span class="sxs-lookup"><span data-stu-id="a06c2-293">For examples of client-side code that use the Storage Client Library to execute efficient queries, see:</span></span>  

* [<span data-ttu-id="a06c2-294">使用儲存體用戶端程式庫執行點查詢</span><span class="sxs-lookup"><span data-stu-id="a06c2-294">Executing a point query using the Storage Client Library</span></span>](#executing-a-point-query-using-the-storage-client-library)
* [<span data-ttu-id="a06c2-295">使用 LINQ 擷取多個實體</span><span class="sxs-lookup"><span data-stu-id="a06c2-295">Retrieving multiple entities using LINQ</span></span>](#retrieving-multiple-entities-using-linq)
* [<span data-ttu-id="a06c2-296">伺服器端預測</span><span class="sxs-lookup"><span data-stu-id="a06c2-296">Server-side projection</span></span>](#server-side-projection)  

<span data-ttu-id="a06c2-297">如需可對儲存在相同資料表中的多個實體類型進行處理的用戶端程式碼範例，請參閱：</span><span class="sxs-lookup"><span data-stu-id="a06c2-297">For examples of client-side code that can handle multiple entity types stored in the same table, see:</span></span>  

* [<span data-ttu-id="a06c2-298">使用異質性實體類型</span><span class="sxs-lookup"><span data-stu-id="a06c2-298">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  

### <a name="choosing-an-appropriate-partitionkey"></a><span data-ttu-id="a06c2-299">選擇適當的 PartitionKey</span><span class="sxs-lookup"><span data-stu-id="a06c2-299">Choosing an appropriate PartitionKey</span></span>
<span data-ttu-id="a06c2-300">您選擇的 **PartitionKey** 應兼顧 EGT 的啟用 (以確保一致性) 和將實體分散到多個資料分割 (以確保可調整的解決方案) 的需求。</span><span class="sxs-lookup"><span data-stu-id="a06c2-300">Your choice of **PartitionKey** should balance the need to enables the use of EGTs (to ensure consistency) against the requirement to distribute your entities across multiple partitions (to ensure a scalable solution).</span></span>  

<span data-ttu-id="a06c2-301">就一個極端而言，您可以在單一磁碟分割儲存您的實體，但這可能會限制方案的延展性，且會妨礙資料表服務的負載平衡要求。</span><span class="sxs-lookup"><span data-stu-id="a06c2-301">At one extreme, you could store all your entities in a single partition, but this may limit the scalability of your solution and would prevent the table service from being able to load-balance requests.</span></span> <span data-ttu-id="a06c2-302">就另一個極端而言，您可以為每個資料分割儲存一個實體以達到高擴充性，並且讓資料表服務可進行負載平衡要求，但這會讓您無法使用實體群組交易。</span><span class="sxs-lookup"><span data-stu-id="a06c2-302">At the other extreme, you could store one entity per partition, which would be highly scalable and which enables the table service to load-balance requests, but which would prevent you from using entity group transactions.</span></span>  

<span data-ttu-id="a06c2-303">理想的 **PartitionKey** 應可讓您使用有效率的查詢，而且具有足夠的資料分割，以確保您的解決方案可進行調整。</span><span class="sxs-lookup"><span data-stu-id="a06c2-303">An ideal **PartitionKey** is one that enables you to use efficient queries and that has sufficient partitions to ensure your solution is scalable.</span></span> <span data-ttu-id="a06c2-304">一般而言，您會發現您的實體將具有適當的屬性，可將您的實體分散到足夠的磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="a06c2-304">Typically, you will find that your entities will have a suitable property that distributes your entities across sufficient partitions.</span></span>

> [!NOTE]
> <span data-ttu-id="a06c2-305">例如，在儲存使用者或員工相關資訊的系統中，UserID 可以是一個良好的 PartitionKey。</span><span class="sxs-lookup"><span data-stu-id="a06c2-305">For example, in a system that stores information about users or employees, UserID may be a good PartitionKey.</span></span> <span data-ttu-id="a06c2-306">您可能需要數個使用指定的 UserID 做為資料分割索引鍵的實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-306">You may have several entities that use a given UserID as the partition key.</span></span> <span data-ttu-id="a06c2-307">儲存使用者相關資料的每個實體會分組到單一資料分割，因此這些實體可透過實體群組交易來存取，同時仍具有高擴充性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-307">Each entity that stores data about a user is grouped into a single partition, and so these entities are accessible via entity group transactions, while still being highly scalable.</span></span>
> 
> 

<span data-ttu-id="a06c2-308">在選擇 **PartitionKey** 時還有其他考量，這牽涉到您如何插入、更新和刪除實體：請參閱後續的 [資料修改的設計](#design-for-data-modification) 一節。</span><span class="sxs-lookup"><span data-stu-id="a06c2-308">There are additional considerations in your choice of **PartitionKey** that relate to how you will insert, update, and delete entities: see the section [Design for data modification](#design-for-data-modification) below.</span></span>  

### <a name="optimizing-queries-for-the-table-service"></a><span data-ttu-id="a06c2-309">最佳化資料表服務的查詢</span><span class="sxs-lookup"><span data-stu-id="a06c2-309">Optimizing queries for the Table service</span></span>
<span data-ttu-id="a06c2-310">資料表服務會使用 **PartitionKey** 和 **RowKey** 值在單一叢集化索引中自動為您的實體編製索引，因此，點查詢在使用上最有效率。</span><span class="sxs-lookup"><span data-stu-id="a06c2-310">The Table service automatically indexes your entities using the **PartitionKey** and **RowKey** values in a single clustered index, hence the reason that point queries are the most efficient to use.</span></span> <span data-ttu-id="a06c2-311">不過除此以外，在 **PartitionKey** 和 **RowKey** 的叢集化索引上並沒有其他索引。</span><span class="sxs-lookup"><span data-stu-id="a06c2-311">However, there are no indexes other than that on the clustered index on the **PartitionKey** and **RowKey**.</span></span>

<span data-ttu-id="a06c2-312">許多設計必須符合需求，才能讓您根據多個準則查閱實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-312">Many designs must meet requirements to enable lookup of entities based on multiple criteria.</span></span> <span data-ttu-id="a06c2-313">比方說，根據電子郵件、員工識別碼或姓氏找出員工實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-313">For example, locating employee entities based on email, employee id, or last name.</span></span> <span data-ttu-id="a06c2-314">[資料表設計模式](#table-design-patterns) 一節的下列模式可因應這些類型的需求，並說明處理資料表服務不提供次要索引的方式：</span><span class="sxs-lookup"><span data-stu-id="a06c2-314">The following patterns in the section [Table Design Patterns](#table-design-patterns) address these types of requirement and describe ways of working around the fact that the Table service does not provide secondary indexes:</span></span>  

* <span data-ttu-id="a06c2-315">[內部資料分割次要索引模式](#intra-partition-secondary-index-pattern) - 為每個實體儲存多個複本且使用不同 **RowKey** 值 (在相同的資料分割內)，透過使用不同的 **RowKey** 值，就能快速且有效率的查閱和替代排序次序。</span><span class="sxs-lookup"><span data-stu-id="a06c2-315">[Intra-partition secondary index pattern](#intra-partition-secondary-index-pattern) - Store multiple copies of each entity using different **RowKey** values (in the same partition) to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="a06c2-316">[間資料分割次要索引模式](#inter-partition-secondary-index-pattern) - 在個別資料分割或個別資料表中為每個實體儲存多個複本且使用不同 RowKey 值，透過使用不同的 **RowKey** 值，就能快速且有效率的查閱和替代排序次序。</span><span class="sxs-lookup"><span data-stu-id="a06c2-316">[Inter-partition secondary index pattern](#inter-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values in separate partitions or in separate tables to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="a06c2-317">[索引實體模式](#index-entities-pattern) - 維護索引實體，啟用有效的搜尋以傳回實體清單。</span><span class="sxs-lookup"><span data-stu-id="a06c2-317">[Index Entities Pattern](#index-entities-pattern) - Maintain index entities to enable efficient searches that return lists of entities.</span></span>  

### <a name="sorting-data-in-the-table-service"></a><span data-ttu-id="a06c2-318">在表格服務中排序資料</span><span class="sxs-lookup"><span data-stu-id="a06c2-318">Sorting data in the Table service</span></span>
<span data-ttu-id="a06c2-319">資料表服務會先根據 **PartitionKey**、再根據 **RowKey** 傳回以遞增方式排序的實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-319">The Table service returns entities sorted in ascending order based on **PartitionKey** and then by **RowKey**.</span></span> <span data-ttu-id="a06c2-320">這些索引鍵是字串值，若要確保能正確排序數字值，您應該將它們轉換成固定長度，並以零填補它們。</span><span class="sxs-lookup"><span data-stu-id="a06c2-320">These keys are string values and to ensure that numeric values sort correctly, you should convert them to a fixed length and pad them with zeroes.</span></span> <span data-ttu-id="a06c2-321">例如，如果您用來做為 **RowKey** 的員工識別碼值是整數值，您應將員工識別碼 **123** 轉換為 **00000123**。</span><span class="sxs-lookup"><span data-stu-id="a06c2-321">For example, if the employee id value you use as the **RowKey** is an integer value, you should convert employee id **123** to **00000123**.</span></span>  

<span data-ttu-id="a06c2-322">許多應用程式都需要使用以不同順序排序的資料：例如，依名稱或加入日期為員工排序。</span><span class="sxs-lookup"><span data-stu-id="a06c2-322">Many applications have requirements to use data sorted in different orders: for example, sorting employees by name, or by joining date.</span></span> <span data-ttu-id="a06c2-323">[資料表設計模式](#table-design-patterns) 一節中的下列模式可因應如何為您的實體取代排序次序：</span><span class="sxs-lookup"><span data-stu-id="a06c2-323">The following patterns in the section [Table Design Patterns](#table-design-patterns) address how to alternate sort orders for your entities:</span></span>  

* <span data-ttu-id="a06c2-324">[內部資料分割次要索引模式](#intra-partition-secondary-index-pattern) - 為每個實體儲存多個複本且使用不同 RowKey 值 (在相同的資料分割內)，透過使用不同的 RowKey 值，就能快速且有效率的查閱和替代排序次序。</span><span class="sxs-lookup"><span data-stu-id="a06c2-324">[Intra-partition secondary index pattern](#intra-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values (in the same partition) to enable fast and efficient lookups and alternate sort orders by using different RowKey values.</span></span>  
* <span data-ttu-id="a06c2-325">[間資料分割次要索引模式](#inter-partition-secondary-index-pattern) - 在個別資料分割或個別資料表中為每個實體儲存多個複本且使用不同 RowKey 值，透過使用不同的 RowKey 值，就能快速且有效率的查閱和替代排序次序。</span><span class="sxs-lookup"><span data-stu-id="a06c2-325">[Inter-partition secondary index pattern](#inter-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values in separate partitions in separate tables to enable fast and efficient lookups and alternate sort orders by using different RowKey values.</span></span>
* <span data-ttu-id="a06c2-326">[記錄結尾模式](#log-tail-pattern) - 透過使用以反向的日期和時間順序排序的 **RowKey** 值，擷取最近新增到分割區的 *n* 個實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-326">[Log tail pattern](#log-tail-pattern) - Retrieve the *n* entities most recently added to a partition by using a **RowKey** value that sorts in reverse date and time order.</span></span>  

## <a name="design-for-data-modification"></a><span data-ttu-id="a06c2-327">資料修改的設計</span><span class="sxs-lookup"><span data-stu-id="a06c2-327">Design for data modification</span></span>
<span data-ttu-id="a06c2-328">本節著重於最佳化插入、更新和刪除的設計考量。</span><span class="sxs-lookup"><span data-stu-id="a06c2-328">This section focuses on the design considerations for optimizing inserts, updates, and deletes.</span></span> <span data-ttu-id="a06c2-329">在某些情況下，您必須在查詢最佳化的設計與資料修改最佳化的設計之間評估取捨，如同您在設計關聯式資料庫時一般 (雖然在關聯式資料庫中用來管理設計取捨的方法有所不同)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-329">In some cases, you will need to evaluate the trade-off between designs that optimize for querying against designs that optimize for data modification just as you do in designs for relational databases (although the techniques for managing the design trade-offs are different in a relational database).</span></span> <span data-ttu-id="a06c2-330">[資料表設計模式](#table-design-patterns) 一節會說明資料表服務的一些詳細設計模式，並強調說明一些相關取捨。</span><span class="sxs-lookup"><span data-stu-id="a06c2-330">The section [Table Design Patterns](#table-design-patterns) describes some detailed design patterns for the Table service and highlights some these trade-offs.</span></span> <span data-ttu-id="a06c2-331">在實務上，您會發現許多針對查詢實體而最佳化的設計也適用於修改實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-331">In practice, you will find that many designs optimized for querying entities also work well for modifying entities.</span></span>  

### <a name="optimizing-the-performance-of-insert-update-and-delete-operations"></a><span data-ttu-id="a06c2-332">最佳化插入、更新和刪除作業的效能</span><span class="sxs-lookup"><span data-stu-id="a06c2-332">Optimizing the performance of insert, update, and delete operations</span></span>
<span data-ttu-id="a06c2-333">若要更新或刪除實體，您必須能夠使用 **PartitionKey** 和 **RowKey** 值加以識別。</span><span class="sxs-lookup"><span data-stu-id="a06c2-333">To update or delete an entity, you must be able to identify it by using the **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="a06c2-334">在這方面，您選擇用來修改實體的 **PartitionKey** 和 **RowKey**，應遵循您在支援點查詢時進行選擇的類似準則，因為您想要盡可能有效率地識別實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-334">In this respect, your choice of **PartitionKey** and **RowKey** for modifying entities should follow similar criteria to your choice to support point queries because you want to identify entities as efficiently as possible.</span></span> <span data-ttu-id="a06c2-335">您不應使用效率不佳的資料分割或資料表掃描來尋找實體以探索 **PartitionKey** 和 **RowKey** 值，而導致您必須加以更新或刪除。</span><span class="sxs-lookup"><span data-stu-id="a06c2-335">You do not want to use an inefficient partition or table scan to locate an entity in order to discover the **PartitionKey** and **RowKey** values you need to update or delete it.</span></span>  

<span data-ttu-id="a06c2-336">[資料表設計模式](#table-design-patterns) 一節中的下列模式可因應最佳化效能或插入、更新和刪除作業：</span><span class="sxs-lookup"><span data-stu-id="a06c2-336">The following patterns in the section [Table Design Patterns](#table-design-patterns) address optimizing the performance or your insert, update, and delete operations:</span></span>  

* <span data-ttu-id="a06c2-337">[大量刪除模式](#high-volume-delete-pattern) - 藉由將所有要同時刪除的實體儲存在其本身的個別資料表中，讓您能夠刪除大量的實體；您可以藉由刪除資料表來刪除實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-337">[High volume delete pattern](#high-volume-delete-pattern) - Enable the deletion of a high volume of entities by storing all the entities for simultaneous deletion in their own separate table; you delete the entities by deleting the table.</span></span>  
* <span data-ttu-id="a06c2-338">[資料序列模式](#data-series-pattern) - 將完整資料序列儲存在單一實體中，以盡可能減少您提出的要求數。</span><span class="sxs-lookup"><span data-stu-id="a06c2-338">[Data series pattern](#data-series-pattern) - Store complete data series in a single entity to minimize the number of requests you make.</span></span>  
* <span data-ttu-id="a06c2-339">[寬型實體模式](#wide-entities-pattern) - 使用多個實際的實體來儲存具有超過 252 個屬性的邏輯實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-339">[Wide entities pattern](#wide-entities-pattern) - Use multiple physical entities to store logical entities with more than 252 properties.</span></span>  
* <span data-ttu-id="a06c2-340">[大型實體模式](#large-entities-pattern) - 使用 Blob 儲存體來儲存大型屬性值。</span><span class="sxs-lookup"><span data-stu-id="a06c2-340">[Large entities pattern](#large-entities-pattern) - Use blob storage to store large property values.</span></span>  

### <a name="ensuring-consistency-in-your-stored-entities"></a><span data-ttu-id="a06c2-341">確保預存實體中的一致性</span><span class="sxs-lookup"><span data-stu-id="a06c2-341">Ensuring consistency in your stored entities</span></span>
<span data-ttu-id="a06c2-342">另一個會在您選擇最佳化資料修改的索引鍵時造成影響的主要因素，是如何使用不可部分完成的交易確保一致性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-342">The other key factor that influences your choice of keys for optimizing data modifications is how to ensure consistency by using atomic transactions.</span></span> <span data-ttu-id="a06c2-343">只有對於儲存在相同資料分割中的實體，才能使用 EGT 來運作。</span><span class="sxs-lookup"><span data-stu-id="a06c2-343">You can only use an EGT to operate on entities stored in the same partition.</span></span>  

<span data-ttu-id="a06c2-344">[資料表設計模式](#table-design-patterns) 一節中的下列模式說明管理一致性：</span><span class="sxs-lookup"><span data-stu-id="a06c2-344">The following patterns in the section [Table Design Patterns](#table-design-patterns) address managing consistency:</span></span>  

* <span data-ttu-id="a06c2-345">[內部資料分割次要索引模式](#intra-partition-secondary-index-pattern) - 為每個實體儲存多個複本且使用不同 **RowKey** 值 (在相同的資料分割內)，透過使用不同的 **RowKey** 值，就能快速且有效率的查閱和替代排序次序。</span><span class="sxs-lookup"><span data-stu-id="a06c2-345">[Intra-partition secondary index pattern](#intra-partition-secondary-index-pattern) - Store multiple copies of each entity using different **RowKey** values (in the same partition) to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="a06c2-346">[間資料分割次要索引模式](#inter-partition-secondary-index-pattern) - 在個別資料分割或個別資料表中為每個實體儲存多個複本且使用不同 RowKey 值，透過使用不同的 **RowKey** 值，就能快速且有效率的查閱和替代排序次序。</span><span class="sxs-lookup"><span data-stu-id="a06c2-346">[Inter-partition secondary index pattern](#inter-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values in separate partitions or in separate tables to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="a06c2-347">[最終一致的交易模式](#eventually-consistent-transactions-pattern) - 使用 Azure 佇列，跨資料分割界限或儲存體系統界限啟用最終一致的行為。</span><span class="sxs-lookup"><span data-stu-id="a06c2-347">[Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) - Enable eventually consistent behavior across partition boundaries or storage system boundaries by using Azure queues.</span></span>
* <span data-ttu-id="a06c2-348">[索引實體模式](#index-entities-pattern) - 維護索引實體，啟用有效的搜尋以傳回實體清單。</span><span class="sxs-lookup"><span data-stu-id="a06c2-348">[Index Entities Pattern](#index-entities-pattern) - Maintain index entities to enable efficient searches that return lists of entities.</span></span>  
* <span data-ttu-id="a06c2-349">[反正規化模式](#denormalization-pattern) - 將相關資料結合在單一實體中，讓您透過單點查詢擷取所有您所需的資料。</span><span class="sxs-lookup"><span data-stu-id="a06c2-349">[Denormalization pattern](#denormalization-pattern) - Combine related data together in a single entity to enable you to retrieve all the data you need with a single point query.</span></span>  
* <span data-ttu-id="a06c2-350">[資料序列模式](#data-series-pattern) - 將完整資料序列儲存在單一實體中，以盡可能減少您提出的要求數。</span><span class="sxs-lookup"><span data-stu-id="a06c2-350">[Data series pattern](#data-series-pattern) - Store complete data series in a single entity to minimize the number of requests you make.</span></span>  

<span data-ttu-id="a06c2-351">如需實體群組交易的相關資訊，請參閱 [實體群組交易](#entity-group-transactions)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-351">For information about entity group transactions, see the section [Entity Group Transactions](#entity-group-transactions).</span></span>  

### <a name="ensuring-your-design-for-efficient-modifications-facilitates-efficient-queries"></a><span data-ttu-id="a06c2-352">確保您針對有效率的修改所做的設計有助於提升查詢效率</span><span class="sxs-lookup"><span data-stu-id="a06c2-352">Ensuring your design for efficient modifications facilitates efficient queries</span></span>
<span data-ttu-id="a06c2-353">在許多情況下，效率查詢的設計都可造就有效的修改，但是您務必要評估這對您的特定案例是否適用。</span><span class="sxs-lookup"><span data-stu-id="a06c2-353">In many cases, a design for efficient querying results in efficient modifications, but you should always evaluate whether this is the case for your specific scenario.</span></span> <span data-ttu-id="a06c2-354">[資料表設計模式](#table-design-patterns) 一節中的某些模式會在查詢和修改實體之間明確評估取捨，您應一律將各種作業類型的數目納入考量。</span><span class="sxs-lookup"><span data-stu-id="a06c2-354">Some of the patterns in the section [Table Design Patterns](#table-design-patterns) explicitly evaluate trade-offs between querying and modifying entities, and you should always take into account the number of each type of operation.</span></span>  

<span data-ttu-id="a06c2-355">[資料表設計模式](#table-design-patterns) 一節中的下列模式可因應如何在有效查詢的設計與有效資料修改的設計之間進行取捨：</span><span class="sxs-lookup"><span data-stu-id="a06c2-355">The following patterns in the section [Table Design Patterns](#table-design-patterns) address trade-offs between designing for efficient queries and designing for efficient data modification:</span></span>  

* <span data-ttu-id="a06c2-356">[複合索引鍵模式](#compound-key-pattern) - 使用複合 **RowKey** 值，讓用戶端可透過單點查詢來查閱相關資料。</span><span class="sxs-lookup"><span data-stu-id="a06c2-356">[Compound key pattern](#compound-key-pattern) - Use compound **RowKey** values to enable a client to lookup related data with a single point query.</span></span>  
* <span data-ttu-id="a06c2-357">[記錄結尾模式](#log-tail-pattern) - 透過使用以反向的日期和時間順序排序的 **RowKey** 值，擷取最近新增到分割區的 *n* 個實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-357">[Log tail pattern](#log-tail-pattern) - Retrieve the *n* entities most recently added to a partition by using a **RowKey** value that sorts in reverse date and time order.</span></span>  

## <a name="encrypting-table-data"></a><span data-ttu-id="a06c2-358">加密資料表的資料</span><span class="sxs-lookup"><span data-stu-id="a06c2-358">Encrypting Table Data</span></span>
<span data-ttu-id="a06c2-359">.NET Azure 儲存體用戶端程式庫支援在插入和取代作業時進行字串實體屬性的加密。</span><span class="sxs-lookup"><span data-stu-id="a06c2-359">The .NET Azure Storage Client Library supports encryption of string entity properties for insert and replace operations.</span></span> <span data-ttu-id="a06c2-360">加密的字串儲存在服務上作為二進位屬性，且解密後會轉換回字串。</span><span class="sxs-lookup"><span data-stu-id="a06c2-360">The encrypted strings are stored on the service as binary properties, and they are converted back to strings after decryption.</span></span>    

<span data-ttu-id="a06c2-361">針對資料表，除了加密原則之外，使用者必須指定要加密的屬性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-361">For tables, in addition to the encryption policy, users must specify the properties to be encrypted.</span></span> <span data-ttu-id="a06c2-362">作法是指定 [EncryptProperty] 屬性 (針對衍生自 TableEntity 的 POCO 實體)，或在要求選項中指定加密解析程式。</span><span class="sxs-lookup"><span data-stu-id="a06c2-362">This can be done by either specifying an [EncryptProperty] attribute (for POCO entities that derive from TableEntity) or an encryption resolver in request options.</span></span> <span data-ttu-id="a06c2-363">加密解析程式是委派，接受資料分割索引鍵、資料列索引鍵和屬性名稱，然後傳回布林值，指出是否應該加密該屬性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-363">An encryption resolver is a delegate that takes a partition key, row key, and property name and returns a Boolean that indicates whether that property should be encrypted.</span></span> <span data-ttu-id="a06c2-364">在加密期間，用戶端程式庫會使用此資訊，決定將屬性在寫到網路時是否應該加密。</span><span class="sxs-lookup"><span data-stu-id="a06c2-364">During encryption, the client library will use this information to decide whether a property should be encrypted while writing to the wire.</span></span> <span data-ttu-id="a06c2-365">委派也提供關於屬性如何加密的可能邏輯。</span><span class="sxs-lookup"><span data-stu-id="a06c2-365">The delegate also provides for the possibility of logic around how properties are encrypted.</span></span> <span data-ttu-id="a06c2-366">(例如，如果 X，則加密屬性 A，否則加密屬性 A 和 B。)請注意，讀取或查詢實體時不需要提供這項資訊。</span><span class="sxs-lookup"><span data-stu-id="a06c2-366">(For example, if X, then encrypt property A; otherwise encrypt properties A and B.) Note that it is not necessary to provide this information while reading or querying entities.</span></span>

<span data-ttu-id="a06c2-367">請注意目前不支援合併。</span><span class="sxs-lookup"><span data-stu-id="a06c2-367">Note that merge is not currently supported.</span></span> <span data-ttu-id="a06c2-368">因為屬性子集先前可能是使用不同的金鑰加密，直接合併新的屬性並更新中繼資料會導致資料遺失。</span><span class="sxs-lookup"><span data-stu-id="a06c2-368">Since a subset of properties may have been encrypted previously using a different key, simply merging the new properties and updating the metadata will result in data loss.</span></span> <span data-ttu-id="a06c2-369">合併可能需要額外的服務呼叫來從服務讀取預先存在的實體，或在每個屬性上都使用新的金鑰，兩者都不利用於效能。</span><span class="sxs-lookup"><span data-stu-id="a06c2-369">Merging either requires making extra service calls to read the pre-existing entity from the service, or using a new key per property, both of which are not suitable for performance reasons.</span></span>     

<span data-ttu-id="a06c2-370">如需加密資料表資料的相關資訊，請參閱 [Microsoft Azure 儲存體的用戶端加密和 Azure 金鑰保存庫](storage-client-side-encryption.md)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-370">For information about encrypting table data, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](storage-client-side-encryption.md).</span></span>  

## <a name="modelling-relationships"></a><span data-ttu-id="a06c2-371">模型化關聯性</span><span class="sxs-lookup"><span data-stu-id="a06c2-371">Modelling relationships</span></span>
<span data-ttu-id="a06c2-372">建置網域模型是設計複雜系統時的關鍵步驟。</span><span class="sxs-lookup"><span data-stu-id="a06c2-372">Building domain models is a key step in the design of complex systems.</span></span> <span data-ttu-id="a06c2-373">一般而言，您可以使用模型化程序來識別實體及其之間的關聯性，藉此了解商業網域，並告知您的系統設計。</span><span class="sxs-lookup"><span data-stu-id="a06c2-373">Typically, you use the modelling process to identify entities and the relationships between them as a way to understand the business domain and inform the design of your system.</span></span> <span data-ttu-id="a06c2-374">本節主要說明如何轉譯網域模型中一些常見的關聯性類型，以設計資料表服務。</span><span class="sxs-lookup"><span data-stu-id="a06c2-374">This section focuses on how you can translate some of the common relationship types found in domain models to designs for the Table service.</span></span> <span data-ttu-id="a06c2-375">從邏輯資料模型對應至實體 NoSQL 架構資料模型的程序，與設計關聯式資料庫時使用的程序非常不同。</span><span class="sxs-lookup"><span data-stu-id="a06c2-375">The process of mapping from a logical data-model to a physical NoSQL based data-model is very different from that used when designing a relational database.</span></span> <span data-ttu-id="a06c2-376">關聯式資料庫設計通常會採用針對最小化備援性而最佳化的資料正規化程序，再搭配宣告式查詢功能以說明如何實作資料庫的運作方式。</span><span class="sxs-lookup"><span data-stu-id="a06c2-376">Relational databases design typically assumes a data normalization process optimized for minimizing redundancy – and a declarative querying capability that abstracts how the implementation of how the database works.</span></span>  

### <a name="one-to-many-relationships"></a><span data-ttu-id="a06c2-377">一對多關聯性</span><span class="sxs-lookup"><span data-stu-id="a06c2-377">One-to-many relationships</span></span>
<span data-ttu-id="a06c2-378">商業網域物件之間常會產生一對多關聯性：例如，一個部門有許多員工。</span><span class="sxs-lookup"><span data-stu-id="a06c2-378">One-to-many relationships between business domain objects occur very frequently: for example, one department has many employees.</span></span> <span data-ttu-id="a06c2-379">有數種方式可用來實作資料表服務中的一對多關聯性，每種方式都有其可能與特定狀況相關的優缺點。</span><span class="sxs-lookup"><span data-stu-id="a06c2-379">There are several ways to implement one-to-many relationships in the Table service each with pros and cons that may be relevant to the particular scenario.</span></span>  

<span data-ttu-id="a06c2-380">舉例來說，假設某家大型跨國公司有數十萬個部門和員工實體，其中每個部門都有許多員工，且每位員工都與一個特定部門相關聯。</span><span class="sxs-lookup"><span data-stu-id="a06c2-380">Consider the example of a large multi-national corporation with tens of thousands of departments and employee entities where every department has many employees and each employee as associated with one specific department.</span></span> <span data-ttu-id="a06c2-381">其中一個方法是儲存個別部門和這些員工實體，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a06c2-381">One approach is to store separate department and employee entities such as these:</span></span>  

![][1]

<span data-ttu-id="a06c2-382">此範例會根據 **PartitionKey** 值說明類型之間的隱含一對多關聯性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-382">This example shows an implicit one-to-many relationship between the types based on the **PartitionKey** value.</span></span> <span data-ttu-id="a06c2-383">每個部門可以有許多員工。</span><span class="sxs-lookup"><span data-stu-id="a06c2-383">Each department can have many employees.</span></span>  

<span data-ttu-id="a06c2-384">此範例也說明相同資料分割中的部門實體及其相關聯的員工實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-384">This example also shows a department entity and its related employee entities in the same partition.</span></span> <span data-ttu-id="a06c2-385">您可以選擇為不同的實體類型使用不同的資料分割、資料表甚或儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a06c2-385">You could choose to use different partitions, tables, or even storage accounts for the different entity types.</span></span>  

<span data-ttu-id="a06c2-386">替代方式是將資料去正規化，並只使用去正規化的部門資料儲存員工實體，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="a06c2-386">An alternative approach is to denormalize your data and store only employee entities with denormalized department data as shown in the following example.</span></span> <span data-ttu-id="a06c2-387">在此特定案例中，如果您需要能夠變更部門經理的詳細資料，這個去正規化方法可能不是最佳選擇，因為此時您必須更新部門中的每一位員工。</span><span class="sxs-lookup"><span data-stu-id="a06c2-387">In this particular scenario, this denormalized approach may not be the best if you have a requirement to be able to change the details of a department manager because to do this you need to update every employee in the department.</span></span>  

![][2]

<span data-ttu-id="a06c2-388">如需詳細資訊，請參閱本指南下半部的 [去正規化模式](#denormalization-pattern) 。</span><span class="sxs-lookup"><span data-stu-id="a06c2-388">For more information, see the [Denormalization pattern](#denormalization-pattern) later in this guide.</span></span>  

<span data-ttu-id="a06c2-389">下表摘要說明前述用來儲存具有一對多關聯性的員工和部門實體的各種方法有何優缺點。</span><span class="sxs-lookup"><span data-stu-id="a06c2-389">The following table summarizes the pros and cons of each of the approaches outlined above for storing employee and department entities that have a one-to-many relationship.</span></span> <span data-ttu-id="a06c2-390">您也應考慮您要執行各種作業的頻率：如果不常執行作業，則使包含高成本作業的設計，或許是可行的。</span><span class="sxs-lookup"><span data-stu-id="a06c2-390">You should also consider how often you expect to perform various operations: it may be acceptable to have a design that includes an expensive operation if that operation only happens infrequently.</span></span>  

<table>
<tr>
<th><span data-ttu-id="a06c2-391">方法</span><span class="sxs-lookup"><span data-stu-id="a06c2-391">Approach</span></span></th>
<th><span data-ttu-id="a06c2-392">優點</span><span class="sxs-lookup"><span data-stu-id="a06c2-392">Pros</span></span></th>
<th><span data-ttu-id="a06c2-393">缺點</span><span class="sxs-lookup"><span data-stu-id="a06c2-393">Cons</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="a06c2-394">個別的實體類型、相同的資料分割、相同的資料表</span><span class="sxs-lookup"><span data-stu-id="a06c2-394">Separate entity types, same partition, same table</span></span></td>
<td>
<ul>
<li><span data-ttu-id="a06c2-395">您可以使用單一作業更新部門實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-395">You can update a department entity with a single operation.</span></span></li>
<li><span data-ttu-id="a06c2-396">如果您需要在每次更新/插入/刪除員工實體時修改部門實體，您可以使用 EGT 來維持一致性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-396">You can use an EGT to maintain consistency if you have a requirement to modify a department entity whenever you update/insert/delete an employee entity.</span></span> <span data-ttu-id="a06c2-397">例如，假設您維護每個部門的部門員工計數。</span><span class="sxs-lookup"><span data-stu-id="a06c2-397">For example if you maintain a departmental employee count for each department.</span></span></li>
</ul>
</td>
<td>
<ul>
<li><span data-ttu-id="a06c2-398">您可能需要針對某些用戶端活動同時擷取員工和部門實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-398">You may need to retrieve both an employee and a department entity for some client activities.</span></span></li>
<li><span data-ttu-id="a06c2-399">儲存作業會在相同資料分割中執行。</span><span class="sxs-lookup"><span data-stu-id="a06c2-399">Storage operations happen in the same partition.</span></span> <span data-ttu-id="a06c2-400">在交易量偏高時，這可能會導致熱點。</span><span class="sxs-lookup"><span data-stu-id="a06c2-400">At high transaction volumes, this may result in a hotspot.</span></span></li>
<li><span data-ttu-id="a06c2-401">您無法使用 EGT 將員工移至新部門。</span><span class="sxs-lookup"><span data-stu-id="a06c2-401">You cannot move an employee to a new department using an EGT.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="a06c2-402">個別的實體類型、不同的資料分割或資料表或儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="a06c2-402">Separate entity types, different partitions or tables or storage accounts</span></span></td>
<td>
<ul>
<li><span data-ttu-id="a06c2-403">您可以使用單一作業更新部門實體或員工實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-403">You can update a department entity or employee entity with a single operation.</span></span></li>
<li><span data-ttu-id="a06c2-404">在交易量偏高時，這可能有助於將負載分散到多個資料分割。</span><span class="sxs-lookup"><span data-stu-id="a06c2-404">At high transaction volumes, this may help spread the load across more partitions.</span></span></li>
</ul>
</td>
<td>
<ul>
<li><span data-ttu-id="a06c2-405">您可能需要針對某些用戶端活動同時擷取員工和部門實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-405">You may need to retrieve both an employee and a department entity for some client activities.</span></span></li>
<li><span data-ttu-id="a06c2-406">當您更新/插入/刪除員工和更新部門時，您無法使用 EGT 維護一致性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-406">You cannot use EGTs to maintain consistency when you update/insert/delete an employee and update a department.</span></span> <span data-ttu-id="a06c2-407">例如，更新某個部門實體中的員工計數。</span><span class="sxs-lookup"><span data-stu-id="a06c2-407">For example, updating an employee count in a department entity.</span></span></li>
<li><span data-ttu-id="a06c2-408">您無法使用 EGT 將員工移至新部門。</span><span class="sxs-lookup"><span data-stu-id="a06c2-408">You cannot move an employee to a new department using an EGT.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="a06c2-409">去正規化為單一實體類型</span><span class="sxs-lookup"><span data-stu-id="a06c2-409">Denormalize into single entity type</span></span></td>
<td>
<ul>
<li><span data-ttu-id="a06c2-410">您可以透過單一要求擷取您所需的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="a06c2-410">You can retrieve all the information you need with a single request.</span></span></li>
</ul>
</td>
<td>
<ul>
<li><span data-ttu-id="a06c2-411">如果您需要更新部門資訊，維持一致性可能會很昂貴 (您可能必須更新部門中的所有員工)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-411">It may be expensive to maintain consistency if you need to update department information (this would require you to update all the employees in a department).</span></span></li>
</ul>
</td>
</tr>
</table>

<span data-ttu-id="a06c2-412">您選擇這些選項的方式及其優缺點是最重要的，這取決於您的應用程式案例。</span><span class="sxs-lookup"><span data-stu-id="a06c2-412">How you choose between these options, and which of the pros and cons are most significant, depends on your specific application scenarios.</span></span> <span data-ttu-id="a06c2-413">例如，您多久修改一次部門實體；您所有的員工查詢是否都需要其他部門資訊；您的磁碟分割或儲存體帳戶有多接近延展性限制？</span><span class="sxs-lookup"><span data-stu-id="a06c2-413">For example, how often do you modify department entities; do all your employee queries need the additional departmental information; how close are you to the scalability limits on your partitions or your storage account?</span></span>  

### <a name="one-to-one-relationships"></a><span data-ttu-id="a06c2-414">一對一關聯性</span><span class="sxs-lookup"><span data-stu-id="a06c2-414">One-to-one relationships</span></span>
<span data-ttu-id="a06c2-415">網域模型的實體之間可能會包含一對一關聯性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-415">Domain models may include one-to-one relationships between entities.</span></span> <span data-ttu-id="a06c2-416">如果您需要在資料表服務中實作一對一關聯性，您在需要同時擷取兩個相關的實體時，也必須選擇如何連結兩者。</span><span class="sxs-lookup"><span data-stu-id="a06c2-416">If you need to implement a one-to-one relationship in the Table service, you must also choose how to link the two related entities when you need to retrieve them both.</span></span> <span data-ttu-id="a06c2-417">此連結可以是隱含的 (根據索引鍵值中的慣例) 或明確的 (藉由以 **PartitionKey** 和 **RowKey** 值的形式，將每個實體中的連結儲存至其相關的實體)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-417">This link can be either implicit, based on a convention in the key values, or explicit by storing a link in the form of **PartitionKey** and **RowKey** values in each entity to its related entity.</span></span> <span data-ttu-id="a06c2-418">如需是否應將相關實體儲存於相同資料分割中的討論，請參閱 [一對多關聯性](#one-to-many-relationships)一節。</span><span class="sxs-lookup"><span data-stu-id="a06c2-418">For a discussion of whether you should store the related entities in the same partition, see the section [One-to-many relationships](#one-to-many-relationships).</span></span>  

<span data-ttu-id="a06c2-419">請注意，有也可能會導致您在資料表服務中實作一對一關聯性的實作考量：</span><span class="sxs-lookup"><span data-stu-id="a06c2-419">Note that there are also implementation considerations that might lead you to implement one-to-one relationships in the Table service:</span></span>  

* <span data-ttu-id="a06c2-420">處理大型實體 (如需詳細資訊，請參閱 [大型實體模式](#large-entities-pattern))。</span><span class="sxs-lookup"><span data-stu-id="a06c2-420">Handling large entities (for more information, see [Large Entities Pattern](#large-entities-pattern)).</span></span>  
* <span data-ttu-id="a06c2-421">實作存取控制 (如需詳細資訊，請參閱 [使用共用存取簽章控制存取](#controlling-access-with-shared-access-signatures))。</span><span class="sxs-lookup"><span data-stu-id="a06c2-421">Implementing access controls (for more information, see [Controlling access with Shared Access Signatures](#controlling-access-with-shared-access-signatures)).</span></span>  

### <a name="join-in-the-client"></a><span data-ttu-id="a06c2-422">用戶端中的聯結</span><span class="sxs-lookup"><span data-stu-id="a06c2-422">Join in the client</span></span>
<span data-ttu-id="a06c2-423">雖然有多種方式可以模型化資料表服務中的關聯性，但您應該記住，使用資料表服務的兩個主要原因是延展性和效能。</span><span class="sxs-lookup"><span data-stu-id="a06c2-423">Although there are ways to model relationships in the Table service, you should not forget that the two prime reasons for using the Table service are scalability and performance.</span></span> <span data-ttu-id="a06c2-424">如果您發現您將許多包含方案的效能和延展性的關聯性模型化，您應該自問是否需要在資料表設計中建置所有的資料關聯性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-424">If you find you are modelling many relationships that compromise the performance and scalability of your solution, you should ask yourself if it is necessary to build all the data relationships into your table design.</span></span> <span data-ttu-id="a06c2-425">如果您讓用戶端應用程式執行任何必要的聯結，或許可以簡化設計並改善方案的效能與延展性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-425">You may be able to simplify the design and improve the scalability and performance of your solution if you let your client application perform any necessary joins.</span></span>  

<span data-ttu-id="a06c2-426">例如，如果您有小型資料表，且其中包含未經常變更的資料，您就可以擷取此資料一次，並在用戶端上加以快取。</span><span class="sxs-lookup"><span data-stu-id="a06c2-426">For example, if you have small tables that contain data that does not change very often, then you can retrieve this data once and cache it on the client.</span></span> <span data-ttu-id="a06c2-427">這可以避免重複擷取相同資料的往返。</span><span class="sxs-lookup"><span data-stu-id="a06c2-427">This can avoid repeated roundtrips to retrieve the same data.</span></span> <span data-ttu-id="a06c2-428">在我們已於本指南中討論的範例中，小型組織中的部門集合很可能較小且不常變更，因此適合做為可由用戶端應用程式下載一次並快取為查閱資料的資料。</span><span class="sxs-lookup"><span data-stu-id="a06c2-428">In the examples we have looked at in this guide, the set of departments in a small organization is likely to be small and change infrequently making it a good candidate for data that client application can download once and cache as look up data.</span></span>  

### <a name="inheritance-relationships"></a><span data-ttu-id="a06c2-429">繼承關聯性</span><span class="sxs-lookup"><span data-stu-id="a06c2-429">Inheritance relationships</span></span>
<span data-ttu-id="a06c2-430">如果您的用戶端應用程式使用一組形成部分繼承關聯性的類別來代表商業實體，您可以輕鬆地在資料表服務中保存這些實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-430">If your client application uses a set of classes that form part of an inheritance relationship to represent business entities, you can easily persist those entities in the Table service.</span></span> <span data-ttu-id="a06c2-431">例如，您可能會在用戶端應用程式中定義下列一組類別，其中 **Person** 是抽象類別。</span><span class="sxs-lookup"><span data-stu-id="a06c2-431">For example, you might have the following set of classes defined in your client application where **Person** is an abstract class.</span></span>

![][3]

<span data-ttu-id="a06c2-432">您可以透過使用實體如下所示的單一 Person 資料表，在資料表服務中保存兩個固定類別的執行個體：</span><span class="sxs-lookup"><span data-stu-id="a06c2-432">You can persist instances of the two concrete classes in the Table service using a single Person table using entities in that look like this:</span></span>  

![][4]

<span data-ttu-id="a06c2-433">如需在用戶端程式碼中於相同資料表上使用多個實體類型的詳細資訊，請參閱本指南稍後的 [使用異質性實體類型](#working-with-heterogeneous-entity-types) 一節。</span><span class="sxs-lookup"><span data-stu-id="a06c2-433">For more information about working with multiple entity types in the same table in client code, see the section [Working with heterogeneous entity types](#working-with-heterogeneous-entity-types) later in this guide.</span></span> <span data-ttu-id="a06c2-434">其中提供如何在用戶端程式碼中辨識實體類型的範例。</span><span class="sxs-lookup"><span data-stu-id="a06c2-434">This provides examples of how to recognize the entity type in client code.</span></span>  

## <a name="table-design-patterns"></a><span data-ttu-id="a06c2-435">資料表設計模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-435">Table Design Patterns</span></span>
<span data-ttu-id="a06c2-436">在前幾節中，您已看到一些關於如何針對使用查詢擷取實體資料和插入、更新及刪除實體資料最佳化您的資料表設計的詳細討論。</span><span class="sxs-lookup"><span data-stu-id="a06c2-436">In previous sections, you have seen some detailed discussions about how to optimize your table design for both retrieving entity data using queries and for inserting, updating, and deleting entity data.</span></span> <span data-ttu-id="a06c2-437">本節將說明一些適用於資料表服務方案的模式。</span><span class="sxs-lookup"><span data-stu-id="a06c2-437">This section describes some patterns appropriate for use with Table service solutions.</span></span> <span data-ttu-id="a06c2-438">此外，您會看到您如何有效處理先前在本指南中提及的一些問題和取捨。</span><span class="sxs-lookup"><span data-stu-id="a06c2-438">In addition, you will see how you can practically address some of the issues and trade-offs raised previously in this guide.</span></span> <span data-ttu-id="a06c2-439">下圖摘要說明不同模式之間的關聯性：</span><span class="sxs-lookup"><span data-stu-id="a06c2-439">The following diagram summarizes the relationships between the different patterns:</span></span>  

![][5]

<span data-ttu-id="a06c2-440">上方的模式圖強調顯示本指南中提及的模式 (藍色) 與反向模式 (橘色) 之間的一些關聯性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-440">The pattern map above highlights some relationships between patterns (blue) and anti-patterns (orange) that are documented in this guide.</span></span> <span data-ttu-id="a06c2-441">當然還有許多其他模式也值得考量。</span><span class="sxs-lookup"><span data-stu-id="a06c2-441">There are of course many other patterns that are worth considering.</span></span> <span data-ttu-id="a06c2-442">例如，表格服務的其中一個主要案例是從[命令查詢責任隔離 (CQRS)](https://msdn.microsoft.com/library/azure/jj554200.aspx) 模式使用[具體化檢視模式](https://msdn.microsoft.com/library/azure/dn589782.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-442">For example, one of the key scenarios for Table Service is to use the [Materialized View Pattern](https://msdn.microsoft.com/library/azure/dn589782.aspx) from the [Command Query Responsibility Segregation (CQRS)](https://msdn.microsoft.com/library/azure/jj554200.aspx) pattern.</span></span>  

### <a name="intra-partition-secondary-index-pattern"></a><span data-ttu-id="a06c2-443">內部資料分割次要索引模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-443">Intra-partition secondary index pattern</span></span>
<span data-ttu-id="a06c2-444">為每個實體儲存多個複本且使用不同 **RowKey** 值 (在相同的資料分割內)，透過使用不同的 **RowKey** 值，就能快速且有效率的查閱和替代排序次序。</span><span class="sxs-lookup"><span data-stu-id="a06c2-444">Store multiple copies of each entity using different **RowKey** values (in the same partition) to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span> <span data-ttu-id="a06c2-445">複本之間的更新可以使用 EGT 保持一致。</span><span class="sxs-lookup"><span data-stu-id="a06c2-445">Updates between copies can be kept consistent using EGT's.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a06c2-446">內容和問題</span><span class="sxs-lookup"><span data-stu-id="a06c2-446">Context and problem</span></span>
<span data-ttu-id="a06c2-447">表格服務會使用 **PartitionKey** 和 **RowKey** 值自動編製實體的索引。</span><span class="sxs-lookup"><span data-stu-id="a06c2-447">The Table service automatically indexes entities using the **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="a06c2-448">這可讓用戶端應用程式使用這些值有效率地擷取實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-448">This enables a client application to retrieve an entity efficiently using these values.</span></span> <span data-ttu-id="a06c2-449">例如，若使用如下的資料表結構，用戶端應用程式將可使用點查詢透過部門名稱和員工識別碼 (**PartitionKey** 和 **RowKey** 值) 來擷取個別員工實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-449">For example, using the table structure shown below, a client application can use a point query to retrieve an individual employee entity by using the department name and the employee id (the **PartitionKey** and **RowKey** values).</span></span> <span data-ttu-id="a06c2-450">用戶端也可以擷取每個部門內以員工識別碼排序的實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-450">A client can also retrieve entities sorted by employee id within each department.</span></span>

![][6]

<span data-ttu-id="a06c2-451">如果您也想能夠根據其他屬性 (例如電子郵件地址) 的值尋找員工實體，您必須使用效率較低的資料分割掃描來尋找相符項目。</span><span class="sxs-lookup"><span data-stu-id="a06c2-451">If you also want to be able to find an employee entity based on the value of another property, such as email address, you must use a less efficient partition scan to find a match.</span></span> <span data-ttu-id="a06c2-452">這是因為資料表服務不會提供次要索引。</span><span class="sxs-lookup"><span data-stu-id="a06c2-452">This is because the table service does not provide secondary indexes.</span></span> <span data-ttu-id="a06c2-453">此外，您無法要求以 **RowKey** 順序以外的不同順序來排序的員工清單。</span><span class="sxs-lookup"><span data-stu-id="a06c2-453">In addition, there is no option to request a list of employees sorted in a different order than **RowKey** order.</span></span>  

#### <a name="solution"></a><span data-ttu-id="a06c2-454">方案</span><span class="sxs-lookup"><span data-stu-id="a06c2-454">Solution</span></span>
<span data-ttu-id="a06c2-455">若要解決缺少次要索引的問題，您可以為每個實體儲存多個複本，且每個複本分別使用不同 **RowKey** 值。</span><span class="sxs-lookup"><span data-stu-id="a06c2-455">To work around the lack of secondary indexes, you can store multiple copies of each entity with each copy using a different **RowKey** value.</span></span> <span data-ttu-id="a06c2-456">如果您使用如下所示的結構來儲存實體，就能夠根據電子郵件地址或員工識別碼，有效率地擷取員工實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-456">If you store an entity with the structures shown below, you can efficiently retrieve employee entities based on email address or employee id.</span></span> <span data-ttu-id="a06c2-457">**RowKey**、"empid_" 及 "email_" 的前置詞值可讓您使用一組電子郵件地址或員工識別碼的範圍，來查詢單一員工或某個範圍內的員工。</span><span class="sxs-lookup"><span data-stu-id="a06c2-457">The prefix values for the **RowKey**, "empid_" and "email_" enable you to query for a single employee or a range of employees by using a range of email addresses or employee ids.</span></span>  

![][7]

<span data-ttu-id="a06c2-458">下列兩個篩選準則 (一個依員工識別碼查閱，另一個依電子郵件地址查閱) 都會指定點查詢：</span><span class="sxs-lookup"><span data-stu-id="a06c2-458">The following two filter criteria (one looking up by employee id and one looking up by email address) both specify point queries:</span></span>  

* <span data-ttu-id="a06c2-459">$filter=(PartitionKey eq 'Sales') and (RowKey eq 'empid_000223')</span><span class="sxs-lookup"><span data-stu-id="a06c2-459">$filter=(PartitionKey eq 'Sales') and (RowKey eq 'empid_000223')</span></span>  
* <span data-ttu-id="a06c2-460">$filter=(PartitionKey eq 'Sales') and (RowKey eq 'email_jonesj@contoso.com')</span><span class="sxs-lookup"><span data-stu-id="a06c2-460">$filter=(PartitionKey eq 'Sales') and (RowKey eq 'email_jonesj@contoso.com')</span></span>  

<span data-ttu-id="a06c2-461">如果您查詢某範圍的員工實體，您可以指定以員工識別碼順序排序的範圍，或藉由查詢在 **RowKey**中有適當前置詞的實體，指定以電子郵件地址順序排序的範圍。</span><span class="sxs-lookup"><span data-stu-id="a06c2-461">If you query for a range of employee entities, you can specify a range sorted in employee id order, or a range sorted in email address order by querying for entities with the appropriate prefix in the **RowKey**.</span></span>  

* <span data-ttu-id="a06c2-462">若要在銷售部門中，找出員工識別碼範圍從 000100 至 000199 的所有員工：請使用 $filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000100') and (RowKey le 'empid_000199')</span><span class="sxs-lookup"><span data-stu-id="a06c2-462">To find all the employees in the Sales department with an employee id in the range 000100 to 000199 use: $filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000100') and (RowKey le 'empid_000199')</span></span>  
* <span data-ttu-id="a06c2-463">若要在銷售部門中，找出電子郵件地址開頭為字母 'a' 的所有員工：請使用 $filter=(PartitionKey eq 'Sales') and (RowKey ge 'email_a') and (RowKey lt 'email_b')</span><span class="sxs-lookup"><span data-stu-id="a06c2-463">To find all the employees in the Sales department with an email address starting with the letter 'a' use: $filter=(PartitionKey eq 'Sales') and (RowKey ge 'email_a') and (RowKey lt 'email_b')</span></span>  
  
  <span data-ttu-id="a06c2-464">請注意，上述範例中使用的篩選語法來自於表格服務 REST API，如需詳細資訊，請參閱 [查詢實體](http://msdn.microsoft.com/library/azure/dd179421.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-464">Note that the filter syntax used in the examples above is from the Table service REST API, for more information see [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a06c2-465">問題和考量</span><span class="sxs-lookup"><span data-stu-id="a06c2-465">Issues and considerations</span></span>
<span data-ttu-id="a06c2-466">當您決定如何實作此模式時，請考慮下列幾點：</span><span class="sxs-lookup"><span data-stu-id="a06c2-466">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a06c2-467">資料表儲存體的使用成本相對較低廉，因此儲存重複資料的成本負擔應該不是主要的考量。</span><span class="sxs-lookup"><span data-stu-id="a06c2-467">Table storage is relatively cheap to use so the cost overhead of storing duplicate data should not be a major concern.</span></span> <span data-ttu-id="a06c2-468">不過，您一律應根據預期的儲存需求評估設計成本，並僅新增重複實體來支援用戶端應用程式將會執行的查詢。</span><span class="sxs-lookup"><span data-stu-id="a06c2-468">However, you should always evaluate the cost of your design based on your anticipated storage requirements and only add duplicate entities to support the queries your client application will execute.</span></span>  
* <span data-ttu-id="a06c2-469">因為次要索引實體儲存在與原始實體相同的磁碟分割中，因此您應該確定不會超過個別資料分割的延展性目標。</span><span class="sxs-lookup"><span data-stu-id="a06c2-469">Because the secondary index entities are stored in the same partition as the original entities, you should ensure that you do not exceed the scalability targets for an individual partition.</span></span>  
* <span data-ttu-id="a06c2-470">您可以將重複實體彼此保持一致，方法是使用 EGT 自動更新實體的兩個複本。</span><span class="sxs-lookup"><span data-stu-id="a06c2-470">You can keep your duplicate entities consistent with each other by using EGTs to update the two copies of the entity atomically.</span></span> <span data-ttu-id="a06c2-471">這表示您應該將實體的所有複本儲存在相同的資料分割中。</span><span class="sxs-lookup"><span data-stu-id="a06c2-471">This implies that you should store all copies of an entity in the same partition.</span></span> <span data-ttu-id="a06c2-472">如需詳細資訊，請參閱 [使用實體群組交易](#entity-group-transactions)一節。</span><span class="sxs-lookup"><span data-stu-id="a06c2-472">For more information, see the section [Using Entity Group Transactions](#entity-group-transactions).</span></span>  
* <span data-ttu-id="a06c2-473">每個實體用於 **RowKey** 的值必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="a06c2-473">The value used for the **RowKey** must be unique for each entity.</span></span> <span data-ttu-id="a06c2-474">請考慮使用複合索引鍵值。</span><span class="sxs-lookup"><span data-stu-id="a06c2-474">Consider using compound key values.</span></span>  
* <span data-ttu-id="a06c2-475">在 **RowKey** 中填補數值 (例如，員工識別碼 000223)，可根據上限與下限正確進行排序和篩選。</span><span class="sxs-lookup"><span data-stu-id="a06c2-475">Padding numeric values in the **RowKey** (for example, the employee id 000223), enables correct sorting and filtering based on upper and lower bounds.</span></span>  
* <span data-ttu-id="a06c2-476">您不一定需要複製實體的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-476">You do not necessarily need to duplicate all the properties of your entity.</span></span> <span data-ttu-id="a06c2-477">例如，如果在 **RowKey** 中使用電子郵件地址查閱實體的查詢永遠都不需要員工的年齡，這些實體可能有下列結構：</span><span class="sxs-lookup"><span data-stu-id="a06c2-477">For example, if the queries that lookup the entities using the email address in the **RowKey** never need the employee's age, these entities could have the following structure:</span></span>

![][8]

* <span data-ttu-id="a06c2-478">一般而言，儲存重複資料並確保您可以透過單一查詢擷取您需要的所有資料，通常會比使用一個查詢來尋找實體並以另一個查閱所需資料更為理想。</span><span class="sxs-lookup"><span data-stu-id="a06c2-478">It is typically better to store duplicate data and ensure that you can retrieve all the data you need with a single query, than to use one query to locate an entity and another to lookup the required data.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a06c2-479">使用此模式的時機</span><span class="sxs-lookup"><span data-stu-id="a06c2-479">When to use this pattern</span></span>
<span data-ttu-id="a06c2-480">當用戶端應用程式需要使用各種不同的索引鍵擷取實體時、當用戶端需要擷取不同排序次序的實體時，以及您可以使用不同的唯一值識別每個實體時，請使用此模式。</span><span class="sxs-lookup"><span data-stu-id="a06c2-480">Use this pattern when your client application needs to retrieve entities using a variety of different keys, when your client needs to retrieve entities in different sort orders, and where you can identify each entity using a variety of unique values.</span></span> <span data-ttu-id="a06c2-481">不過，您應確定在使用不同的 **RowKey** 值執行實體查閱時，您不會超出資料分割延展性限制。</span><span class="sxs-lookup"><span data-stu-id="a06c2-481">However, you should be sure that you do not exceed the partition scalability limits when you are performing entity lookups using the different **RowKey** values.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a06c2-482">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="a06c2-482">Related patterns and guidance</span></span>
<span data-ttu-id="a06c2-483">在實作此模式時，下列模式和指導方針也可能有所關聯：</span><span class="sxs-lookup"><span data-stu-id="a06c2-483">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a06c2-484">間分割次要索引模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-484">Inter-partition secondary index pattern</span></span>](#inter-partition-secondary-index-pattern)
* [<span data-ttu-id="a06c2-485">複合索引鍵模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-485">Compound key pattern</span></span>](#compound-key-pattern)
* [<span data-ttu-id="a06c2-486">實體群組交易</span><span class="sxs-lookup"><span data-stu-id="a06c2-486">Entity Group Transactions</span></span>](#entity-group-transactions)
* [<span data-ttu-id="a06c2-487">使用異質性實體類型</span><span class="sxs-lookup"><span data-stu-id="a06c2-487">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)

### <a name="inter-partition-secondary-index-pattern"></a><span data-ttu-id="a06c2-488">間資料分割次要索引模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-488">Inter-partition secondary index pattern</span></span>
<span data-ttu-id="a06c2-489">在個別資料分割或個別資料表中為每個實體儲存多個複本且使用不同 **RowKey** 值，透過使用不同的 **RowKey** 值，就能快速且有效率的查閱和替代排序次序。</span><span class="sxs-lookup"><span data-stu-id="a06c2-489">Store multiple copies of each entity using different **RowKey** values in separate partitions or in separate tables to enable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a06c2-490">內容和問題</span><span class="sxs-lookup"><span data-stu-id="a06c2-490">Context and problem</span></span>
<span data-ttu-id="a06c2-491">表格服務會使用 **PartitionKey** 和 **RowKey** 值自動編製實體的索引。</span><span class="sxs-lookup"><span data-stu-id="a06c2-491">The Table service automatically indexes entities using the **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="a06c2-492">這可讓用戶端應用程式使用這些值有效率地擷取實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-492">This enables a client application to retrieve an entity efficiently using these values.</span></span> <span data-ttu-id="a06c2-493">例如，若使用如下的資料表結構，用戶端應用程式將可使用點查詢透過部門名稱和員工識別碼 (**PartitionKey** 和 **RowKey** 值) 來擷取個別員工實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-493">For example, using the table structure shown below, a client application can use a point query to retrieve an individual employee entity by using the department name and the employee id (the **PartitionKey** and **RowKey** values).</span></span> <span data-ttu-id="a06c2-494">用戶端也可以擷取每個部門內以員工識別碼排序的實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-494">A client can also retrieve entities sorted by employee id within each department.</span></span>  

![][9]

<span data-ttu-id="a06c2-495">如果您也想能夠根據其他屬性 (例如電子郵件地址) 的值尋找員工實體，您必須使用效率較低的資料分割掃描來尋找相符項目。</span><span class="sxs-lookup"><span data-stu-id="a06c2-495">If you also want to be able to find an employee entity based on the value of another property, such as email address, you must use a less efficient partition scan to find a match.</span></span> <span data-ttu-id="a06c2-496">這是因為資料表服務不會提供次要索引。</span><span class="sxs-lookup"><span data-stu-id="a06c2-496">This is because the table service does not provide secondary indexes.</span></span> <span data-ttu-id="a06c2-497">此外，您無法要求以 **RowKey** 順序以外的不同順序來排序的員工清單。</span><span class="sxs-lookup"><span data-stu-id="a06c2-497">In addition, there is no option to request a list of employees sorted in a different order than **RowKey** order.</span></span>  

<span data-ttu-id="a06c2-498">您預期這些實體會有極大量的交易，而想要為您的用戶端節流以將資料表服務的風險降至最低。</span><span class="sxs-lookup"><span data-stu-id="a06c2-498">You are anticipating a very high volume of transactions against these entities and want to minimize the risk of the Table service throttling your client.</span></span>  

#### <a name="solution"></a><span data-ttu-id="a06c2-499">方案</span><span class="sxs-lookup"><span data-stu-id="a06c2-499">Solution</span></span>
<span data-ttu-id="a06c2-500">若要解決缺少次要索引的問題，您可以為每個實體儲存多個複本，且每個複本分別使用不同的 **PartitionKey** 和 **RowKey** 值。</span><span class="sxs-lookup"><span data-stu-id="a06c2-500">To work around the lack of secondary indexes, you can store multiple copies of each entity with each copy using different **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="a06c2-501">如果您使用如下所示的結構來儲存實體，就能夠根據電子郵件地址或員工識別碼，有效率地擷取員工實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-501">If you store an entity with the structures shown below, you can efficiently retrieve employee entities based on email address or employee id.</span></span> <span data-ttu-id="a06c2-502">**PartitionKey**、"empid_" 及 "email_" 的前置詞值可讓您識別想要用於查詢的索引。</span><span class="sxs-lookup"><span data-stu-id="a06c2-502">The prefix values for the **PartitionKey**, "empid_" and "email_" enable you to identify which index you want to use for a query.</span></span>  

![][10]

<span data-ttu-id="a06c2-503">下列兩個篩選準則 (一個依員工識別碼查閱，另一個依電子郵件地址查閱) 都會指定點查詢：</span><span class="sxs-lookup"><span data-stu-id="a06c2-503">The following two filter criteria (one looking up by employee id and one looking up by email address) both specify point queries:</span></span>  

* <span data-ttu-id="a06c2-504">$filter=(PartitionKey eq 'empid_Sales') and (RowKey eq '000223')</span><span class="sxs-lookup"><span data-stu-id="a06c2-504">$filter=(PartitionKey eq 'empid_Sales') and (RowKey eq '000223')</span></span>
* <span data-ttu-id="a06c2-505">$filter=(PartitionKey eq 'email_Sales') and (RowKey eq 'jonesj@contoso.com')</span><span class="sxs-lookup"><span data-stu-id="a06c2-505">$filter=(PartitionKey eq 'email_Sales') and (RowKey eq 'jonesj@contoso.com')</span></span>  

<span data-ttu-id="a06c2-506">如果您查詢某範圍的員工實體，您可以指定以員工識別碼順序排序的範圍，或藉由查詢在 **RowKey**中有適當前置詞的實體，指定以電子郵件地址順序排序的範圍。</span><span class="sxs-lookup"><span data-stu-id="a06c2-506">If you query for a range of employee entities, you can specify a range sorted in employee id order, or a range sorted in email address order by querying for entities with the appropriate prefix in the **RowKey**.</span></span>  

* <span data-ttu-id="a06c2-507">若要在銷售部門中，找出員工識別碼範圍從 **000100** 至 **000199** 以員工識別碼順序排序的所有員工，請使用：$filter=(PartitionKey eq 'empid_Sales') and (RowKey ge '000100') and (RowKey le '000199')。</span><span class="sxs-lookup"><span data-stu-id="a06c2-507">To find all the employees in the Sales department with an employee id in the range **000100** to **000199** sorted in employee id order use: $filter=(PartitionKey eq 'empid_Sales') and (RowKey ge '000100') and (RowKey le '000199')</span></span>  
* <span data-ttu-id="a06c2-508">若要在銷售部門中，找出電子郵件地址以 'a' 開頭的所有員工，請使用：$filter=(PartitionKey eq 'email_Sales') and (RowKey ge 'a') and (RowKey lt 'b')</span><span class="sxs-lookup"><span data-stu-id="a06c2-508">To find all the employees in the Sales department with an email address that starts with 'a' sorted in email address order use: $filter=(PartitionKey eq 'email_Sales') and (RowKey ge 'a') and (RowKey lt 'b')</span></span>  

<span data-ttu-id="a06c2-509">請注意，上述範例中使用的篩選語法來自於表格服務 REST API，如需詳細資訊，請參閱 [查詢實體](http://msdn.microsoft.com/library/azure/dd179421.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-509">Note that the filter syntax used in the examples above is from the Table service REST API, for more information see [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a06c2-510">問題和考量</span><span class="sxs-lookup"><span data-stu-id="a06c2-510">Issues and considerations</span></span>
<span data-ttu-id="a06c2-511">當您決定如何實作此模式時，請考慮下列幾點：</span><span class="sxs-lookup"><span data-stu-id="a06c2-511">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a06c2-512">您可以讓重複實體彼此之間始終保持一致，方法是使用 [最終一致的交易模式](#eventually-consistent-transactions-pattern) 來維護主要和次要索引實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-512">You can keep your duplicate entities eventually consistent with each other by using the [Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) to maintain the primary and secondary index entities.</span></span>  
* <span data-ttu-id="a06c2-513">資料表儲存體的使用成本相對較低廉，因此儲存重複資料的成本負擔應該不是主要的考量。</span><span class="sxs-lookup"><span data-stu-id="a06c2-513">Table storage is relatively cheap to use so the cost overhead of storing duplicate data should not be a major concern.</span></span> <span data-ttu-id="a06c2-514">不過，您一律應根據預期的儲存需求評估設計成本，並僅新增重複實體來支援用戶端應用程式將會執行的查詢。</span><span class="sxs-lookup"><span data-stu-id="a06c2-514">However, you should always evaluate the cost of your design based on your anticipated storage requirements and only add duplicate entities to support the queries your client application will execute.</span></span>  
* <span data-ttu-id="a06c2-515">每個實體用於 **RowKey** 的值必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="a06c2-515">The value used for the **RowKey** must be unique for each entity.</span></span> <span data-ttu-id="a06c2-516">請考慮使用複合索引鍵值。</span><span class="sxs-lookup"><span data-stu-id="a06c2-516">Consider using compound key values.</span></span>  
* <span data-ttu-id="a06c2-517">在 **RowKey** 中填補數值 (例如，員工識別碼 000223)，可根據上限與下限正確進行排序和篩選。</span><span class="sxs-lookup"><span data-stu-id="a06c2-517">Padding numeric values in the **RowKey** (for example, the employee id 000223), enables correct sorting and filtering based on upper and lower bounds.</span></span>  
* <span data-ttu-id="a06c2-518">您不一定需要複製實體的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-518">You do not necessarily need to duplicate all the properties of your entity.</span></span> <span data-ttu-id="a06c2-519">例如，如果在 **RowKey** 中使用電子郵件地址查閱實體的查詢永遠都不需要員工的年齡，這些實體可能有下列結構：</span><span class="sxs-lookup"><span data-stu-id="a06c2-519">For example, if the queries that lookup the entities using the email address in the **RowKey** never need the employee's age, these entities could have the following structure:</span></span>
  
  ![][11]
* <span data-ttu-id="a06c2-520">一般而言，儲存重複資料並確保您可以透過單一查詢擷取您需要的所有資料，通常會比使用一個查詢透過次要索引尋找實體、並以另一個查詢來查閱主要索引中的所需資料更為理想。</span><span class="sxs-lookup"><span data-stu-id="a06c2-520">It is typically better to store duplicate data and ensure that you can retrieve all the data you need with a single query than to use one query to locate an entity using the secondary index and another to lookup the required data in the primary index.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a06c2-521">使用此模式的時機</span><span class="sxs-lookup"><span data-stu-id="a06c2-521">When to use this pattern</span></span>
<span data-ttu-id="a06c2-522">當用戶端應用程式需要使用各種不同的索引鍵擷取實體時、當用戶端需要擷取不同排序次序的實體時，以及您可以使用不同的唯一值識別每個實體時，請使用此模式。</span><span class="sxs-lookup"><span data-stu-id="a06c2-522">Use this pattern when your client application needs to retrieve entities using a variety of different keys, when your client needs to retrieve entities in different sort orders, and where you can identify each entity using a variety of unique values.</span></span> <span data-ttu-id="a06c2-523">當您使用不同的 **RowKey** 值執行實體查閱時，如果要避免超出資料分割延展性限制，請使用此模式。</span><span class="sxs-lookup"><span data-stu-id="a06c2-523">Use this pattern when you want to avoid exceeding the partition scalability limits when you are performing entity lookups using the different **RowKey** values.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a06c2-524">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="a06c2-524">Related patterns and guidance</span></span>
<span data-ttu-id="a06c2-525">在實作此模式時，下列模式和指導方針也可能有所關聯：</span><span class="sxs-lookup"><span data-stu-id="a06c2-525">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a06c2-526">最終一致的交易模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-526">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  
* [<span data-ttu-id="a06c2-527">內部資料分割次要索引模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-527">Intra-partition secondary index pattern</span></span>](#intra-partition-secondary-index-pattern)  
* [<span data-ttu-id="a06c2-528">複合索引鍵模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-528">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="a06c2-529">實體群組交易</span><span class="sxs-lookup"><span data-stu-id="a06c2-529">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="a06c2-530">使用異質性實體類型</span><span class="sxs-lookup"><span data-stu-id="a06c2-530">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  

### <a name="eventually-consistent-transactions-pattern"></a><span data-ttu-id="a06c2-531">最終一致的交易模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-531">Eventually consistent transactions pattern</span></span>
<span data-ttu-id="a06c2-532">使用 Azure 佇列，跨資料分割界限或儲存體系統界限啟用最終一致的行為。</span><span class="sxs-lookup"><span data-stu-id="a06c2-532">Enable eventually consistent behavior across partition boundaries or storage system boundaries by using Azure queues.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a06c2-533">內容和問題</span><span class="sxs-lookup"><span data-stu-id="a06c2-533">Context and problem</span></span>
<span data-ttu-id="a06c2-534">EGT 可讓您在共用相的資料分割索引鍵的多個實體之間執行不可部分完成的交易。</span><span class="sxs-lookup"><span data-stu-id="a06c2-534">EGTs enable atomic transactions across multiple entities that share the same partition key.</span></span> <span data-ttu-id="a06c2-535">基於效能和擴充性的考量，您可能會決定在個別的磁碟分割或不同的儲存體系統中儲存有一致性需求的實體：在這種情況下，您無法使用 EGT 維護一致性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-535">For performance and scalability reasons, you might decide to store entities that have consistency requirements in separate partitions or in a separate storage system: in such a scenario, you cannot use EGTs to maintain consistency.</span></span> <span data-ttu-id="a06c2-536">例如，您可能必須在下列項目間維護最終一致性：</span><span class="sxs-lookup"><span data-stu-id="a06c2-536">For example, you might have a requirement to maintain eventual consistency between:</span></span>  

* <span data-ttu-id="a06c2-537">儲存在相同資料表的兩個不同資料分割中、不同的資料表中、不同儲存體帳戶中的實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-537">Entities stored in two different partitions in the same table, in different tables, in in different storage accounts.</span></span>  
* <span data-ttu-id="a06c2-538">儲存在資料表服務中的實體和儲存在 Blob 服務中的 Blob。</span><span class="sxs-lookup"><span data-stu-id="a06c2-538">An entity stored in the Table service and a blob stored in the Blob service.</span></span>  
* <span data-ttu-id="a06c2-539">儲存在資料表服務中的實體和檔案系統中的檔案。</span><span class="sxs-lookup"><span data-stu-id="a06c2-539">An entity stored in the Table service and a file in a file system.</span></span>  
* <span data-ttu-id="a06c2-540">儲存在資料表服務中、但使用 Azure 搜尋服務編製索引的實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-540">An entity store in the Table service yet indexed using the Azure Search service.</span></span>  

#### <a name="solution"></a><span data-ttu-id="a06c2-541">方案</span><span class="sxs-lookup"><span data-stu-id="a06c2-541">Solution</span></span>
<span data-ttu-id="a06c2-542">藉由使用 Azure 佇列，您可以實作解決方案，提供跨兩個或多個資料分割或儲存系統的最終一致性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-542">By using Azure queues, you can implement a solution that delivers eventual consistency across two or more partitions or storage systems.</span></span>
<span data-ttu-id="a06c2-543">為了說明這種方法，我們假設您需要能夠封存舊的員工實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-543">To illustrate this approach, assume you have a requirement to be able to archive old employee entities.</span></span> <span data-ttu-id="a06c2-544">舊的員工實體很少受到查詢，應從處理目前員工的任何活動中排除。</span><span class="sxs-lookup"><span data-stu-id="a06c2-544">Old employee entities are rarely queried and should be excluded from any activities that deal with current employees.</span></span> <span data-ttu-id="a06c2-545">若要實作這項需求，您必須將作用中員工儲存在**目前**資料表中，並將舊員工儲存在**封存**資料表中。</span><span class="sxs-lookup"><span data-stu-id="a06c2-545">To implement this requirement you store active employees in the **Current** table and old employees in the **Archive** table.</span></span> <span data-ttu-id="a06c2-546">要封存員工，您必須先從**目前**資料表中刪除實體，並將實體加入**封存**資料表，但您無法使用 EGT 來執行這兩項作業。</span><span class="sxs-lookup"><span data-stu-id="a06c2-546">Archiving an employee requires you to delete the entity from the **Current** table and add the entity to the **Archive** table, but you cannot use an EGT to perform these two operations.</span></span> <span data-ttu-id="a06c2-547">若要避免因失敗而導致實體同時出現或未出現在這兩個資料表中，封存作業必須最終一致。</span><span class="sxs-lookup"><span data-stu-id="a06c2-547">To avoid the risk that a failure causes an entity to appear in both or neither tables, the archive operation must be eventually consistent.</span></span> <span data-ttu-id="a06c2-548">下列順序圖說明此作業的步驟。</span><span class="sxs-lookup"><span data-stu-id="a06c2-548">The following sequence diagram outlines the steps in this operation.</span></span> <span data-ttu-id="a06c2-549">後續文字提供了例外狀況路徑的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a06c2-549">More detail is provided for exception paths in the text following.</span></span>  

![][12]

<span data-ttu-id="a06c2-550">用戶端會藉由將訊息放在 Azure 佇列來起始封存作業，在此範例中會封存員工 #456。</span><span class="sxs-lookup"><span data-stu-id="a06c2-550">A client initiates the archive operation by placing a message on an Azure queue, in this example to archive employee #456.</span></span> <span data-ttu-id="a06c2-551">背景工作角色會輪詢佇列中的新訊息；若找到新訊息，它會讀取訊息，並將隱藏的複本保留在佇列上。</span><span class="sxs-lookup"><span data-stu-id="a06c2-551">A worker role polls the queue for new messages; when it finds one, it reads the message and leaves a hidden copy on the queue.</span></span> <span data-ttu-id="a06c2-552">背景工作角色接著會擷取來自**目前**資料表的實體複本、將複本插入**封存**資料表中，然後從**目前**資料表中刪除原始複本。</span><span class="sxs-lookup"><span data-stu-id="a06c2-552">The worker role next fetches a copy of the entity from the **Current** table, inserts a copy in the **Archive** table, and then deletes the original from the **Current** table.</span></span> <span data-ttu-id="a06c2-553">最後，如果前述步驟沒有任何錯誤，背景工作角色會從佇列中刪除隱藏的訊息。</span><span class="sxs-lookup"><span data-stu-id="a06c2-553">Finally, if there were no errors from the previous steps, the worker role deletes the hidden message from the queue.</span></span>  

<span data-ttu-id="a06c2-554">此範例的步驟 4 會將員工插入 **封存** 資料表。</span><span class="sxs-lookup"><span data-stu-id="a06c2-554">In this example, step 4 inserts the employee into the **Archive** table.</span></span> <span data-ttu-id="a06c2-555">這可以將員工新增至 Blob 服務中的 Blob 或檔案系統中的檔案。</span><span class="sxs-lookup"><span data-stu-id="a06c2-555">It could add the employee to a blob in the Blob service or a file in a file system.</span></span>  

#### <a name="recovering-from-failures"></a><span data-ttu-id="a06c2-556">從失敗復原</span><span class="sxs-lookup"><span data-stu-id="a06c2-556">Recovering from failures</span></span>
<span data-ttu-id="a06c2-557">步驟 **4** 和 **5** 中的作業務必等冪，免得背景工作角色必須重新啟動封存作業。</span><span class="sxs-lookup"><span data-stu-id="a06c2-557">It is important that the operations in steps **4** and **5** must be *idempotent* in case the worker role needs to restart the archive operation.</span></span> <span data-ttu-id="a06c2-558">使用表格服務時，在步驟 **4** 中，您應使用「插入或取代」作業；在步驟 **5** 中，則應在您使用的用戶端程式庫中使用「如果存在即刪除」作業。</span><span class="sxs-lookup"><span data-stu-id="a06c2-558">If you are using the Table service, for step **4** you should use an "insert or replace" operation; for step **5** you should use a "delete if exists" operation in the client library you are using.</span></span> <span data-ttu-id="a06c2-559">如果您使用其他儲存體系統，您必須使用適當的冪等作業。</span><span class="sxs-lookup"><span data-stu-id="a06c2-559">If you are using another storage system, you must use an appropriate idempotent operation.</span></span>  

<span data-ttu-id="a06c2-560">如果背景工作角色一直未完成步驟 **6**，則在逾時後，訊息會重新出現在佇列上，可讓背景工作角色嘗試重新加以處理。</span><span class="sxs-lookup"><span data-stu-id="a06c2-560">If the worker role never completes step **6**, then after a timeout the message reappears on the queue ready for the worker role to try to reprocess it.</span></span> <span data-ttu-id="a06c2-561">背景工作角色可以檢查訊息在佇列上的已讀取次數，如有必要可將其傳送至不同的佇列，以標示為「有害」訊息接受調查。</span><span class="sxs-lookup"><span data-stu-id="a06c2-561">The worker role can check how many times a message on the queue has been read and, if necessary, flag it is a "poison" message for investigation by sending it to a separate queue.</span></span> <span data-ttu-id="a06c2-562">如需讀取佇列訊息及檢查清除佇列計數的詳細資訊，請參閱 [取得訊息](https://msdn.microsoft.com/library/azure/dd179474.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-562">For more information about reading queue messages and checking the dequeue count, see [Get Messages](https://msdn.microsoft.com/library/azure/dd179474.aspx).</span></span>  

<span data-ttu-id="a06c2-563">來自資料表和佇列服務的某些錯誤是暫時性的，用戶端應用程式應包含適當的重試邏輯來處理它們。</span><span class="sxs-lookup"><span data-stu-id="a06c2-563">Some errors from the Table and Queue services are transient errors, and your client application should include suitable retry logic to handle them.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a06c2-564">問題和考量</span><span class="sxs-lookup"><span data-stu-id="a06c2-564">Issues and considerations</span></span>
<span data-ttu-id="a06c2-565">當您決定如何實作此模式時，請考慮下列幾點：</span><span class="sxs-lookup"><span data-stu-id="a06c2-565">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a06c2-566">此方案不提供交易隔離。</span><span class="sxs-lookup"><span data-stu-id="a06c2-566">This solution does not provide for transaction isolation.</span></span> <span data-ttu-id="a06c2-567">例如，用戶端在在背景工作角色介於步驟 **4** 和 **5** 之間時無法讀取**目前**和**封存**資料表，並且會看見不一致的資料檢視。</span><span class="sxs-lookup"><span data-stu-id="a06c2-567">For example, a client could read the **Current** and **Archive** tables when the worker role was between steps **4** and **5**, and see an inconsistent view of the data.</span></span> <span data-ttu-id="a06c2-568">請注意，資料最終將會一致。</span><span class="sxs-lookup"><span data-stu-id="a06c2-568">Note that the data will be consistent eventually.</span></span>  
* <span data-ttu-id="a06c2-569">您必須確定步驟 4 和 5 是等冪，以確保最終一致性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-569">You must be sure that steps 4 and 5 are idempotent in order to ensure eventual consistency.</span></span>  
* <span data-ttu-id="a06c2-570">您可以使用多個佇列和背景工作角色執行個體來調整方案。</span><span class="sxs-lookup"><span data-stu-id="a06c2-570">You can scale the solution by using multiple queues and worker role instances.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a06c2-571">使用此模式的時機</span><span class="sxs-lookup"><span data-stu-id="a06c2-571">When to use this pattern</span></span>
<span data-ttu-id="a06c2-572">如果您想要確保存在於不同磁碟分割或資料表中的實體之間保有最終一致性，請使用此模式。</span><span class="sxs-lookup"><span data-stu-id="a06c2-572">Use this pattern when you want to guarantee eventual consistency between entities that exist in different partitions or tables.</span></span> <span data-ttu-id="a06c2-573">您可以擴充此模式，以確保整個表格服務與 Blob 服務和其他非 Azure 儲存體資料來源 (例如資料庫或檔案系統) 的作業保有最終一致性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-573">You can extend this pattern to ensure eventual consistency for operations across the Table service and the Blob service and other non-Azure Storage data sources such as database or the file system.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a06c2-574">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="a06c2-574">Related patterns and guidance</span></span>
<span data-ttu-id="a06c2-575">在實作此模式時，下列模式和指導方針也可能有所關聯：</span><span class="sxs-lookup"><span data-stu-id="a06c2-575">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a06c2-576">實體群組交易</span><span class="sxs-lookup"><span data-stu-id="a06c2-576">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="a06c2-577">合併或取代</span><span class="sxs-lookup"><span data-stu-id="a06c2-577">Merge or replace</span></span>](#merge-or-replace)  

> [!NOTE]
> <span data-ttu-id="a06c2-578">如果交易隔離對您的方案而言很重要，您應該考慮重新設計，讓您能夠使用 EGT 資料表。</span><span class="sxs-lookup"><span data-stu-id="a06c2-578">If transaction isolation is important to your solution, you should consider redesigning your tables to enable you to use EGTs.</span></span>  
> 
> 

### <a name="index-entities-pattern"></a><span data-ttu-id="a06c2-579">索引實體模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-579">Index Entities Pattern</span></span>
<span data-ttu-id="a06c2-580">維護索引項目，啟用有效的搜尋以傳回實體清單。</span><span class="sxs-lookup"><span data-stu-id="a06c2-580">Maintain index entities to enable efficient searches that return lists of entities.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a06c2-581">內容和問題</span><span class="sxs-lookup"><span data-stu-id="a06c2-581">Context and problem</span></span>
<span data-ttu-id="a06c2-582">表格服務會使用 **PartitionKey** 和 **RowKey** 值自動編製實體的索引。</span><span class="sxs-lookup"><span data-stu-id="a06c2-582">The Table service automatically indexes entities using the **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="a06c2-583">這可讓用戶端應用程式使用點查詢有效率地擷取實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-583">This enables a client application to retrieve an entity efficiently using a point query.</span></span> <span data-ttu-id="a06c2-584">例如，若使用如下的資料表結構，用戶端應用程式將可有效率地透過部門名稱和員工識別碼 (**PartitionKey** 和 **RowKey**) 來擷取個別員工實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-584">For example, using the table structure shown below, a client application can efficiently retrieve an individual employee entity by using the department name and the employee id (the **PartitionKey** and **RowKey**).</span></span>  

![][13]

<span data-ttu-id="a06c2-585">如果您也想能夠根據其他非唯一屬性 (例如其姓氏) 的值擷取員工實體清單，您必須使用效率較低的資料分割掃描來尋找相符項目，而不要使用索引直接加以查閱。</span><span class="sxs-lookup"><span data-stu-id="a06c2-585">If you also want to be able to retrieve a list of employee entities based on the value of another non-unique property, such as their last name, you must use a less efficient partition scan to find matches rather than using an index to look them up directly.</span></span> <span data-ttu-id="a06c2-586">這是因為資料表服務不會提供次要索引。</span><span class="sxs-lookup"><span data-stu-id="a06c2-586">This is because the table service does not provide secondary indexes.</span></span>  

#### <a name="solution"></a><span data-ttu-id="a06c2-587">方案</span><span class="sxs-lookup"><span data-stu-id="a06c2-587">Solution</span></span>
<span data-ttu-id="a06c2-588">若要透過如上所示的實體結構啟用依據姓氏的查閱，您必須維護員工識別碼清單。</span><span class="sxs-lookup"><span data-stu-id="a06c2-588">To enable lookup by last name with the entity structure shown above, you must maintain lists of employee ids.</span></span> <span data-ttu-id="a06c2-589">如果您想要擷取具有特定姓氏 (例如 Jones) 的員工實體，您必須先針對姓氏為 Jones 的員工找出員工識別碼清單，然後擷取這些員工實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-589">If you want to retrieve the employee entities with a particular last name, such as Jones, you must first locate the list of employee ids for employees with Jones as their last name, and then retrieve those employee entities.</span></span> <span data-ttu-id="a06c2-590">有三個主要的選項可儲存員工識別碼清單：</span><span class="sxs-lookup"><span data-stu-id="a06c2-590">There are three main options for storing the lists of employee ids:</span></span>  

* <span data-ttu-id="a06c2-591">使用 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-591">Use blob storage.</span></span>  
* <span data-ttu-id="a06c2-592">在與員工實體相同的磁碟分割中建立索引實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-592">Create index entities in the same partition as the employee entities.</span></span>  
* <span data-ttu-id="a06c2-593">在個別的資料分割或資料表中建立索引實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-593">Create index entities in a separate partition or table.</span></span>  

<span data-ttu-id="a06c2-594"><u>選項 1：使用 Blob 儲存體</u></span><span class="sxs-lookup"><span data-stu-id="a06c2-594"><u>Option #1: Use blob storage</u></span></span>  

<span data-ttu-id="a06c2-595">使用第一個選項時，您會為每個唯一的姓氏建立一個 Blob，並在每個 Blob 中，針對具有該姓氏的員工儲存 **PartitionKey** (部門) 和 **RowKey** (員工識別碼) 值的清單。</span><span class="sxs-lookup"><span data-stu-id="a06c2-595">For the first option, you create a blob for every unique last name, and in each blob store a list of the **PartitionKey** (department) and **RowKey** (employee id) values for employees that have that last name.</span></span> <span data-ttu-id="a06c2-596">當您新增或刪除某位員工時，您應該確保相關的 Blob 內容與員工實體最終一致。</span><span class="sxs-lookup"><span data-stu-id="a06c2-596">When you add or delete an employee you should ensure that the content of the relevant blob is eventually consistent with the employee entities.</span></span>  

<span data-ttu-id="a06c2-597"><u>選項 2：</u>在相同的資料分割中建立索引實體</span><span class="sxs-lookup"><span data-stu-id="a06c2-597"><u>Option #2:</u> Create index entities in the same partition</span></span>  

<span data-ttu-id="a06c2-598">使用第二個選項時，您會使用儲存下列資料的索引實體：</span><span class="sxs-lookup"><span data-stu-id="a06c2-598">For the second option, use index entities that store the following data:</span></span>  

![][14]

<span data-ttu-id="a06c2-599">**EmployeeIDs** 屬性包含姓氏儲存在 **RowKey** 中之員工的員工識別碼清單。</span><span class="sxs-lookup"><span data-stu-id="a06c2-599">The **EmployeeIDs** property contains a list of employee ids for employees with the last name stored in the **RowKey**.</span></span>  

<span data-ttu-id="a06c2-600">下列步驟概述您在使用第二個選項並且要新增員工時所應遵循的程序。</span><span class="sxs-lookup"><span data-stu-id="a06c2-600">The following steps outline the process you should follow when you are adding a new employee if you are using the second option.</span></span> <span data-ttu-id="a06c2-601">在此範例中，我們會新增在銷售部門中識別碼為 000152、且姓氏為 Jones 的員工：</span><span class="sxs-lookup"><span data-stu-id="a06c2-601">In this example, we are adding an employee with Id 000152 and a last name Jones in the Sales department:</span></span>  

1. <span data-ttu-id="a06c2-602">擷取具有 **PartitionKey** 值 "Sales" 和 **RowKey** 值 "Jones" 的索引實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-602">Retrieve the index entity with a **PartitionKey** value "Sales" and the **RowKey** value "Jones."</span></span> <span data-ttu-id="a06c2-603">儲存此實體的 ETag　以在步驟 2 中使用。</span><span class="sxs-lookup"><span data-stu-id="a06c2-603">Save the ETag of this entity to use in step 2.</span></span>  
2. <span data-ttu-id="a06c2-604">建立實體群組交易 (也就是批次作業)，插入新的員工實體 (**PartitionKey** 值 "Sales" 和 **RowKey** 值 "000152")並更新索引實體 (**PartitionKey** 值 "Sales" 和 **RowKey**值 "Jones")，方法是將新員工識別碼加入 EmployeeIDs 欄位中的清單。</span><span class="sxs-lookup"><span data-stu-id="a06c2-604">Create an entity group transaction (that is, a batch operation) that inserts the new employee entity (**PartitionKey** value "Sales" and **RowKey** value "000152"), and updates the index entity (**PartitionKey** value "Sales" and **RowKey** value "Jones") by adding the new employee id to the list in the EmployeeIDs field.</span></span> <span data-ttu-id="a06c2-605">如需實體群組交易的詳細資訊，請參閱 [實體群組交易](#entity-group-transactions)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-605">For more information about entity group transactions, see [Entity Group Transactions](#entity-group-transactions).</span></span>  
3. <span data-ttu-id="a06c2-606">如果實體群組交易因為開放式並行存取錯誤而失敗 (其他人剛修改過索引實體)，您就必須從步驟 1 重新執行。</span><span class="sxs-lookup"><span data-stu-id="a06c2-606">If the entity group transaction fails because of an optimistic concurrency error (someone else has just modified the index entity), then you need to start over at step 1 again.</span></span>  

<span data-ttu-id="a06c2-607">如果您使用第二個選項，您可以使用類似的方法來刪除某位員工。</span><span class="sxs-lookup"><span data-stu-id="a06c2-607">You can use a similar approach to deleting an employee if you are using the second option.</span></span> <span data-ttu-id="a06c2-608">變更員工的姓氏會稍微複雜一點，因為您需要執行會更新三個實體的實體群組交易：員工實體、舊姓氏的索引實體，與新姓氏的索引實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-608">Changing an employee's last name is slightly more complex because you will need to execute an entity group transaction that updates three entities: the employee entity, the index entity for the old last name, and the index entity for the new last name.</span></span> <span data-ttu-id="a06c2-609">您必須先擷取每個實體才能進行變更，以擷取接著可以用來透過開放式並行存取執行更新的 ETag 值。</span><span class="sxs-lookup"><span data-stu-id="a06c2-609">You must retrieve each entity before making any changes in order to retrieve the ETag values that you can then use to perform the updates using optimistic concurrency.</span></span>  

<span data-ttu-id="a06c2-610">下列步驟概述您在使用第二個選項、並需要查閱部門中所有具有給定姓氏的員工時所應遵循的程序。</span><span class="sxs-lookup"><span data-stu-id="a06c2-610">The following steps outline the process you should follow when you need to look up all the employees with a given last name in a department if you are using the second option.</span></span> <span data-ttu-id="a06c2-611">在此範例中，我們會尋找銷售部門中所有姓氏為 Jones 的員工：</span><span class="sxs-lookup"><span data-stu-id="a06c2-611">In this example, we are looking up all the employees with last name Jones in the Sales department:</span></span>  

1. <span data-ttu-id="a06c2-612">擷取具有 **PartitionKey** 值 "Sales" 和 **RowKey** 值 "Jones" 的索引實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-612">Retrieve the index entity with a **PartitionKey** value "Sales" and the **RowKey** value "Jones."</span></span>  
2. <span data-ttu-id="a06c2-613">剖析 EmployeeIDs 欄位中的員工識別碼清單。</span><span class="sxs-lookup"><span data-stu-id="a06c2-613">Parse the list of employee Ids in the EmployeeIDs field.</span></span>  
3. <span data-ttu-id="a06c2-614">如果您需要這些員工的詳細資訊 (例如其電子郵件地址)，請從您在步驟 2 中取得的員工清單使用 **PartitionKey** 值 "Sales" 和 **RowKey** 值來擷取每個員工實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-614">If you need additional information about each of these employees (such as their email addresses), retrieve each of the employee entities using **PartitionKey** value "Sales" and **RowKey** values from the list of employees you obtained in step 2.</span></span>  

<span data-ttu-id="a06c2-615"><u>選項 3：</u>在個別的資料分割或資料表中建立索引實體</span><span class="sxs-lookup"><span data-stu-id="a06c2-615"><u>Option #3:</u> Create index entities in a separate partition or table</span></span>  

<span data-ttu-id="a06c2-616">使用第三個選項時，您會使用儲存下列資料的索引實體：</span><span class="sxs-lookup"><span data-stu-id="a06c2-616">For the third option, use index entities that store the following data:</span></span>  

![][15]

<span data-ttu-id="a06c2-617">**EmployeeIDs** 屬性包含姓氏儲存在 **RowKey** 中之員工的員工識別碼清單。</span><span class="sxs-lookup"><span data-stu-id="a06c2-617">The **EmployeeIDs** property contains a list of employee ids for employees with the last name stored in the **RowKey**.</span></span>  

<span data-ttu-id="a06c2-618">使用第三個選項時，您無法使用 EGT 來維持一致性，因為索引實體位於與員工實體不同的磁碟分割中。</span><span class="sxs-lookup"><span data-stu-id="a06c2-618">With the third option, you cannot use EGTs to maintain consistency because the index entities are in a separate partition from the employee entities.</span></span> <span data-ttu-id="a06c2-619">您應確保索引實體與員工實體最終一致。</span><span class="sxs-lookup"><span data-stu-id="a06c2-619">You should ensure that the index entities are eventually consistent with the employee entities.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a06c2-620">問題和考量</span><span class="sxs-lookup"><span data-stu-id="a06c2-620">Issues and considerations</span></span>
<span data-ttu-id="a06c2-621">當您決定如何實作此模式時，請考慮下列幾點：</span><span class="sxs-lookup"><span data-stu-id="a06c2-621">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a06c2-622">此方案至少需要兩個查詢來擷取相符實體：一個用來查詢索引實體以取得 **RowKey** 值清單，然後查詢以擷取清單中的每個實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-622">This solution requires at least two queries to retrieve matching entities: one to query the index entities to obtain the list of **RowKey** values, and then queries to retrieve each entity in the list.</span></span>  
* <span data-ttu-id="a06c2-623">假設個別實體的大小上限為 1 MB，方案中的選項 2 和選項 3 會假設任何給定姓氏的員工識別碼清單絕不會大於 1 MB。</span><span class="sxs-lookup"><span data-stu-id="a06c2-623">Given that an individual entity has a maximum size of 1 MB, option #2 and option #3 in the solution assume that the list of employee ids for any given last name is never greater than 1 MB.</span></span> <span data-ttu-id="a06c2-624">如果員工識別碼清單的大小可能大於 1 MB，請使用選項 1，並將索引資料儲存在 Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="a06c2-624">If the list of employee ids is likely to be greater than 1 MB in size, use option #1 and store the index data in blob storage.</span></span>  
* <span data-ttu-id="a06c2-625">如果您使用選項 2 (使用 EGT 處理新增和刪除員工以及變更員工姓氏的作業)，您必須評估交易量是否會接近指定資料分割中的延展性限制。</span><span class="sxs-lookup"><span data-stu-id="a06c2-625">If you use option #2 (using EGTs to handle adding and deleting employees, and changing an employee's last name) you must evaluate if the volume of transactions will approach the scalability limits in a given partition.</span></span> <span data-ttu-id="a06c2-626">如果會，您應考慮最終一致方案 (選項 1 或選項 3)，以使用佇列來處理更新要求，並讓您將索引實體儲存在與員工實體不同的個別資料分割中。</span><span class="sxs-lookup"><span data-stu-id="a06c2-626">If this is the case, you should consider an eventually consistent solution (option #1 or option #3) that uses queues to handle the update requests and enables you to store your index entities in a separate partition from the employee entities.</span></span>  
* <span data-ttu-id="a06c2-627">此方案中的選項 2 會假設您想要依姓氏在某部門內進行查閱：例如，您要擷取銷售部門中姓氏為 Jones 的員工清單。</span><span class="sxs-lookup"><span data-stu-id="a06c2-627">Option #2 in this solution assumes that you want to look up by last name within a department: for example, you want to retrieve a list of employees with a last name Jones in the Sales department.</span></span> <span data-ttu-id="a06c2-628">如果您想要能夠查閱整個組織中姓氏為 Jones 的所有員工，請使用選項 1 或選項 3。</span><span class="sxs-lookup"><span data-stu-id="a06c2-628">If you want to be able to look up all the employees with a last name Jones across the whole organization, use either option #1 or option #3.</span></span>
* <span data-ttu-id="a06c2-629">您可以實作可提供最終一致性的佇列型方案 (如需詳細資訊，請參閱 [最終一致的交易模式](#eventually-consistent-transactions-pattern) )。</span><span class="sxs-lookup"><span data-stu-id="a06c2-629">You can implement a queue-based solution that delivers eventual consistency (see the [Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) for more details).</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a06c2-630">使用此模式的時機</span><span class="sxs-lookup"><span data-stu-id="a06c2-630">When to use this pattern</span></span>
<span data-ttu-id="a06c2-631">如果您想要查閱全部共用通用屬性值的一組實體 (例如姓氏為 Jones 的所有員工)，請使用此模式。</span><span class="sxs-lookup"><span data-stu-id="a06c2-631">Use this pattern when you want to lookup a set of entities that all share a common property value, such as all employees with the last name Jones.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a06c2-632">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="a06c2-632">Related patterns and guidance</span></span>
<span data-ttu-id="a06c2-633">在實作此模式時，下列模式和指導方針也可能有所關聯：</span><span class="sxs-lookup"><span data-stu-id="a06c2-633">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a06c2-634">複合索引鍵模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-634">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="a06c2-635">最終一致的交易模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-635">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  
* [<span data-ttu-id="a06c2-636">實體群組交易</span><span class="sxs-lookup"><span data-stu-id="a06c2-636">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="a06c2-637">使用異質性實體類型</span><span class="sxs-lookup"><span data-stu-id="a06c2-637">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  

### <a name="denormalization-pattern"></a><span data-ttu-id="a06c2-638">反正規化模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-638">Denormalization pattern</span></span>
<span data-ttu-id="a06c2-639">將相關資料結合在單一實體中，讓您透過單點查詢擷取所有您所需的資料。</span><span class="sxs-lookup"><span data-stu-id="a06c2-639">Combine related data together in a single entity to enable you to retrieve all the data you need with a single point query.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a06c2-640">內容和問題</span><span class="sxs-lookup"><span data-stu-id="a06c2-640">Context and problem</span></span>
<span data-ttu-id="a06c2-641">在關聯式資料庫中，您通常會將資料正規化，以移除會產生查詢而從多個資料表擷取資料的重複資料。</span><span class="sxs-lookup"><span data-stu-id="a06c2-641">In a relational database, you typically normalize data to remove duplication resulting in queries that retrieve data from multiple tables.</span></span> <span data-ttu-id="a06c2-642">如果您將 Azure 資料表中的資料標準化，您必須從用戶端到伺服器往返多次才能擷取相關的資料。</span><span class="sxs-lookup"><span data-stu-id="a06c2-642">If you normalize your data in Azure tables, you must make multiple round trips from the client to the server to retrieve your related data.</span></span> <span data-ttu-id="a06c2-643">以如下的資料表結構為例，您需要往返兩次才能擷取某部門的詳細資料：其中一個要求是用來擷取包含經理識別碼的部門實體，另一個要求是用來擷取員工實體中的經理詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a06c2-643">For example, with the table structure shown below you need two round trips to retrieve the details for a department: one to fetch the department entity that includes the manager's id, and then another request to fetch the manager's details in an employee entity.</span></span>  

![][16]

#### <a name="solution"></a><span data-ttu-id="a06c2-644">方案</span><span class="sxs-lookup"><span data-stu-id="a06c2-644">Solution</span></span>
<span data-ttu-id="a06c2-645">不要將資料儲存在兩個不同的實體中，而是將資料反正規化，並將管理員詳細資料的複本保存在部門實體中。</span><span class="sxs-lookup"><span data-stu-id="a06c2-645">Instead of storing the data in two separate entities, denormalize the data and keep a copy of the manager's details in the department entity.</span></span> <span data-ttu-id="a06c2-646">例如：</span><span class="sxs-lookup"><span data-stu-id="a06c2-646">For example:</span></span>  

![][17]

<span data-ttu-id="a06c2-647">部門實體連同這些屬性一起儲存後，您現在可以擷取與使用點查詢的部門有關的所有詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a06c2-647">With department entities stored with these properties, you can now retrieve all the details you need about a department using a point query.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a06c2-648">問題和考量</span><span class="sxs-lookup"><span data-stu-id="a06c2-648">Issues and considerations</span></span>
<span data-ttu-id="a06c2-649">當您決定如何實作此模式時，請考慮下列幾點：</span><span class="sxs-lookup"><span data-stu-id="a06c2-649">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a06c2-650">儲存資料兩次還有一些相關的成本負擔。</span><span class="sxs-lookup"><span data-stu-id="a06c2-650">There is some cost overhead associated with storing some data twice.</span></span> <span data-ttu-id="a06c2-651">效能優勢 (因對儲存體服務的要求較少而產生) 通常會高於儲存體成本的邊際增值 (而且這項成本有部分會由擷取部門的詳細資料所需的交易量減少而抵銷)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-651">The performance benefit (resulting from fewer requests to the storage service) typically outweighs the marginal increase in storage costs (and this cost is partially offset by a reduction in the number of transactions you require to fetch the details of a department).</span></span>  
* <span data-ttu-id="a06c2-652">您必須讓儲存管理員相關資訊的兩個實體保有一致性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-652">You must maintain the consistency of the two entities that store information about managers.</span></span> <span data-ttu-id="a06c2-653">您可以使用 EGT 在單一不可部分完成交易中更新多個實體，以處理一致性問題：在此情況下，部門實體和部門經理的員工實體會儲存在相同的資料分割中。</span><span class="sxs-lookup"><span data-stu-id="a06c2-653">You can handle the consistency issue by using EGTs to update multiple entities in a single atomic transaction: in this case, the department entity, and the employee entity for the department manager are stored in the same partition.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a06c2-654">使用此模式的時機</span><span class="sxs-lookup"><span data-stu-id="a06c2-654">When to use this pattern</span></span>
<span data-ttu-id="a06c2-655">如果您經常需要查閱相關資訊，請使用此模式。</span><span class="sxs-lookup"><span data-stu-id="a06c2-655">Use this pattern when you frequently need to look up related information.</span></span> <span data-ttu-id="a06c2-656">此模式可減少用戶端在擷取其所需資料時必須執行的查詢數目。</span><span class="sxs-lookup"><span data-stu-id="a06c2-656">This pattern reduces the number of queries your client must make to retrieve the data it requires.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a06c2-657">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="a06c2-657">Related patterns and guidance</span></span>
<span data-ttu-id="a06c2-658">在實作此模式時，下列模式和指導方針也可能有所關聯：</span><span class="sxs-lookup"><span data-stu-id="a06c2-658">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a06c2-659">複合索引鍵模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-659">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="a06c2-660">實體群組交易</span><span class="sxs-lookup"><span data-stu-id="a06c2-660">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="a06c2-661">使用異質性實體類型</span><span class="sxs-lookup"><span data-stu-id="a06c2-661">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)

### <a name="compound-key-pattern"></a><span data-ttu-id="a06c2-662">複合索引鍵模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-662">Compound key pattern</span></span>
<span data-ttu-id="a06c2-663">使用複合 **RowKey** 值，讓用戶端可透過單點查詢來查閱相關資料。</span><span class="sxs-lookup"><span data-stu-id="a06c2-663">Use compound **RowKey** values to enable a client to lookup related data with a single point query.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a06c2-664">內容和問題</span><span class="sxs-lookup"><span data-stu-id="a06c2-664">Context and problem</span></span>
<span data-ttu-id="a06c2-665">在關聯式資料庫中常會在查詢中使用聯結，將單一查詢中的相關資料片段傳回至用戶端。</span><span class="sxs-lookup"><span data-stu-id="a06c2-665">In a relational database, it is quite natural to use joins in queries to return related pieces of data to the client in a single query.</span></span> <span data-ttu-id="a06c2-666">例如，您可以使用員工識別碼來查閱包含該員工之績效和考核資料的相關實體清單。</span><span class="sxs-lookup"><span data-stu-id="a06c2-666">For example, you might use the employee id to look up a list of related entities that contain performance and review data for that employee.</span></span>  

<span data-ttu-id="a06c2-667">假設您要使用下列結構在資料表服務中儲存員工實體：</span><span class="sxs-lookup"><span data-stu-id="a06c2-667">Assume you are storing employee entities in the Table service using the following structure:</span></span>  

![][18]

<span data-ttu-id="a06c2-668">您也需要儲存該員工在組織中工作各年度的考核和績效相關歷史資料，而且您必須能夠依年份存取這項資訊。</span><span class="sxs-lookup"><span data-stu-id="a06c2-668">You also need to store historical data relating to reviews and performance for each year the employee has worked for your organization and you need to be able to access this information by year.</span></span> <span data-ttu-id="a06c2-669">建立另一個資料表來儲存具有下列結構的實體，是可行選項之一：</span><span class="sxs-lookup"><span data-stu-id="a06c2-669">One option is to create another table that stores entities with the following structure:</span></span>  

![][19]

<span data-ttu-id="a06c2-670">請注意，使用此方法時，您可以選擇在新的實體中重複某些資訊 (例如名字和姓氏)，以便透過單一要求擷取您的資料。</span><span class="sxs-lookup"><span data-stu-id="a06c2-670">Notice that with this approach you may decide to duplicate some information (such as first name and last name) in the new entity to enable you to retrieve your data with a single request.</span></span> <span data-ttu-id="a06c2-671">不過，您無法維護強式一致性，因為您無法使用 EGT 自動更新兩個實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-671">However, you cannot maintain strong consistency because you cannot use an EGT to update the two entities atomically.</span></span>  

#### <a name="solution"></a><span data-ttu-id="a06c2-672">方案</span><span class="sxs-lookup"><span data-stu-id="a06c2-672">Solution</span></span>
<span data-ttu-id="a06c2-673">使用具有下列結構的實體，在您的原始資料表中儲存新的實體類型：</span><span class="sxs-lookup"><span data-stu-id="a06c2-673">Store a new entity type in your original table using entities with the following structure:</span></span>  

![][20]

<span data-ttu-id="a06c2-674">請注意，**RowKey** 現在是由員工識別碼和考核資料年份所組成的複合索引鍵，可讓您透過單一實體的單一要求擷取員工的績效和考核資料。</span><span class="sxs-lookup"><span data-stu-id="a06c2-674">Notice how the **RowKey** is now a compound key made up of the employee id and the year of the review data that enables you to retrieve the employee's performance and review data with a single request for a single entity.</span></span>  

<span data-ttu-id="a06c2-675">下列範例說明如何擷取特定員工的所有考核資料 (例如銷售部門的員工 000123)：</span><span class="sxs-lookup"><span data-stu-id="a06c2-675">The following example outlines how you can retrieve all the review data for a particular employee (such as employee 000123 in the Sales department):</span></span>  

<span data-ttu-id="a06c2-676">$filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000123') and (RowKey lt 'empid_000124')&$select=RowKey,Manager Rating,Peer Rating,Comments</span><span class="sxs-lookup"><span data-stu-id="a06c2-676">$filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000123') and (RowKey lt 'empid_000124')&$select=RowKey,Manager Rating,Peer Rating,Comments</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a06c2-677">問題和考量</span><span class="sxs-lookup"><span data-stu-id="a06c2-677">Issues and considerations</span></span>
<span data-ttu-id="a06c2-678">當您決定如何實作此模式時，請考慮下列幾點：</span><span class="sxs-lookup"><span data-stu-id="a06c2-678">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a06c2-679">您應該使用適當的分隔符號字元以便剖析 **RowKey** 值：例如 **000123_2012**。</span><span class="sxs-lookup"><span data-stu-id="a06c2-679">You should use a suitable separator character that makes it easy to parse the **RowKey** value: for example, **000123_2012**.</span></span>  
* <span data-ttu-id="a06c2-680">您也必須將此實體儲存在與包含相同員工之相關資料的其他實體相同的資料分割中，這表示您可以使用 EGT 來維護強式一致性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-680">You are also storing this entity in the same partition as other entities that contain related data for the same employee, which means you can use EGTs to maintain strong consistency.</span></span>
* <span data-ttu-id="a06c2-681">您應考量您查詢資料的頻率，以判斷此模式是否適用。</span><span class="sxs-lookup"><span data-stu-id="a06c2-681">You should consider how frequently you will query the data to determine whether this pattern is appropriate.</span></span>  <span data-ttu-id="a06c2-682">比方說，如果您不會經常存取考核資料和主要員工資料，則應將其保存為個別的實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-682">For example, if you will access the review data infrequently and the main employee data often you should keep them as separate entities.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a06c2-683">使用此模式的時機</span><span class="sxs-lookup"><span data-stu-id="a06c2-683">When to use this pattern</span></span>
<span data-ttu-id="a06c2-684">如果您需要儲存一或多個您經常查詢的相關實體，請使用此模式。</span><span class="sxs-lookup"><span data-stu-id="a06c2-684">Use this pattern when you need to store one or more related entities that you query frequently.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a06c2-685">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="a06c2-685">Related patterns and guidance</span></span>
<span data-ttu-id="a06c2-686">在實作此模式時，下列模式和指導方針也可能有所關聯：</span><span class="sxs-lookup"><span data-stu-id="a06c2-686">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a06c2-687">實體群組交易</span><span class="sxs-lookup"><span data-stu-id="a06c2-687">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="a06c2-688">使用異質性實體類型</span><span class="sxs-lookup"><span data-stu-id="a06c2-688">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  
* [<span data-ttu-id="a06c2-689">最終一致的交易模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-689">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  

### <a name="log-tail-pattern"></a><span data-ttu-id="a06c2-690">記錄結尾模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-690">Log tail pattern</span></span>
<span data-ttu-id="a06c2-691">透過使用以反向的日期和時間順序排序的 **RowKey** 值，擷取最近加入分割區的 *n* 個實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-691">Retrieve the *n* entities most recently added to a partition by using a **RowKey** value that sorts in reverse date and time order.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a06c2-692">內容和問題</span><span class="sxs-lookup"><span data-stu-id="a06c2-692">Context and problem</span></span>
<span data-ttu-id="a06c2-693">常見的需求是要能夠擷取最近建立的實體，例如員工最近提交的費用請款。</span><span class="sxs-lookup"><span data-stu-id="a06c2-693">A common requirement is be able to retrieve the most recently created entities, for example the ten most recent expense claims submitted by an employee.</span></span> <span data-ttu-id="a06c2-694">資料表查詢支援 **$top** 查詢作業，可從集合中傳回前 *n* 個實體：並沒有對等的查詢作業可傳回集合中最後 n 個實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-694">Table queries support a **$top** query operation to return the first *n* entities from a set: there is no equivalent query operation to return the last n entities in a set.</span></span>  

#### <a name="solution"></a><span data-ttu-id="a06c2-695">方案</span><span class="sxs-lookup"><span data-stu-id="a06c2-695">Solution</span></span>
<span data-ttu-id="a06c2-696">儲存使用可自然以反向的日期/時間順序排序的 **RowKey** 的實體，使最新的項目一律排在資料表中的首位。</span><span class="sxs-lookup"><span data-stu-id="a06c2-696">Store the entities using a **RowKey** that naturally sorts in reverse date/time order by using so the most recent entry is always the first one in the table.</span></span>  

<span data-ttu-id="a06c2-697">比方說，若要能夠擷取某員工最近提交的十筆費用請款，您可以使用衍生自目前日期/時間的反向刻度值。</span><span class="sxs-lookup"><span data-stu-id="a06c2-697">For example, to be able to retrieve the ten most recent expense claims submitted by an employee, you can use a reverse tick value derived from the current date/time.</span></span> <span data-ttu-id="a06c2-698">下列 C# 程式碼範例說明如何針對從最新排序到最舊的 **RowKey** 建立適當的「反向刻度」值：</span><span class="sxs-lookup"><span data-stu-id="a06c2-698">The following C# code sample shows one way to create a suitable "inverted ticks" value for a **RowKey** that sorts from the most recent to the oldest:</span></span>  

`string invertedTicks = string.Format("{0:D19}", DateTime.MaxValue.Ticks - DateTime.UtcNow.Ticks);`  

<span data-ttu-id="a06c2-699">您可以使用下列程式碼回到日期時間值：</span><span class="sxs-lookup"><span data-stu-id="a06c2-699">You can get back to the date time value using the following code:</span></span>  

`DateTime dt = new DateTime(DateTime.MaxValue.Ticks - Int64.Parse(invertedTicks));`  

<span data-ttu-id="a06c2-700">資料表查詢如下所示：</span><span class="sxs-lookup"><span data-stu-id="a06c2-700">The table query looks like this:</span></span>  

`https://myaccount.table.core.windows.net/EmployeeExpense(PartitionKey='empid')?$top=10`  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a06c2-701">問題和考量</span><span class="sxs-lookup"><span data-stu-id="a06c2-701">Issues and considerations</span></span>
<span data-ttu-id="a06c2-702">當您決定如何實作此模式時，請考慮下列幾點：</span><span class="sxs-lookup"><span data-stu-id="a06c2-702">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a06c2-703">您必須為反向刻度值填補前置零，以確保字串值如預期排序。</span><span class="sxs-lookup"><span data-stu-id="a06c2-703">You must pad the reverse tick value with leading zeroes to ensure the string value sorts as expected.</span></span>  
* <span data-ttu-id="a06c2-704">您必須知道資料分割層級的延展性目標。</span><span class="sxs-lookup"><span data-stu-id="a06c2-704">You must be aware of the scalability targets at the level of a partition.</span></span> <span data-ttu-id="a06c2-705">請留意不要建立熱點資料分割。</span><span class="sxs-lookup"><span data-stu-id="a06c2-705">Be careful not create hot spot partitions.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a06c2-706">使用此模式的時機</span><span class="sxs-lookup"><span data-stu-id="a06c2-706">When to use this pattern</span></span>
<span data-ttu-id="a06c2-707">當您需要存取反向日期/時間順序的實體時，或當您需要存取最近新增的實體時，請使用此模式。</span><span class="sxs-lookup"><span data-stu-id="a06c2-707">Use this pattern when you need to access entities in reverse date/time order or when you need to access the most recently added entities.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a06c2-708">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="a06c2-708">Related patterns and guidance</span></span>
<span data-ttu-id="a06c2-709">在實作此模式時，下列模式和指導方針也可能有所關聯：</span><span class="sxs-lookup"><span data-stu-id="a06c2-709">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a06c2-710">在前面加上/附加反向模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-710">Prepend / append anti-pattern</span></span>](#prepend-append-anti-pattern)  
* [<span data-ttu-id="a06c2-711">擷取實體</span><span class="sxs-lookup"><span data-stu-id="a06c2-711">Retrieving entities</span></span>](#retrieving-entities)  

### <a name="high-volume-delete-pattern"></a><span data-ttu-id="a06c2-712">大量刪除模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-712">High volume delete pattern</span></span>
<span data-ttu-id="a06c2-713">藉由將所有要同時刪除的實體儲存在其本身的個別資料表中，讓您能夠刪除大量的實體；您可以藉由刪除資料表來刪除實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-713">Enable the deletion of a high volume of entities by storing all the entities for simultaneous deletion in their own separate table; you delete the entities by deleting the table.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a06c2-714">內容和問題</span><span class="sxs-lookup"><span data-stu-id="a06c2-714">Context and problem</span></span>
<span data-ttu-id="a06c2-715">許多應用程式刪除用戶端應用程式已無需使用的舊資料，或應用程式已封存至其他儲存媒體的舊資料。</span><span class="sxs-lookup"><span data-stu-id="a06c2-715">Many applications delete old data which no longer needs to be available to a client application, or that the application has archived to another storage medium.</span></span> <span data-ttu-id="a06c2-716">一般而言，您可以依日期來識別這類資料：例如，您需要刪除所有存留期超過 60 天之登入要求的記錄。</span><span class="sxs-lookup"><span data-stu-id="a06c2-716">You typically identify such data by a date: for example, you have a requirement to delete records of all login requests that are more than 60 days old.</span></span>  

<span data-ttu-id="a06c2-717">可行的設計之一，就是在 **RowKey**中使用登入要求的日期和時間：</span><span class="sxs-lookup"><span data-stu-id="a06c2-717">One possible design is to use the date and time of the login request in the **RowKey**:</span></span>  

![][21]

<span data-ttu-id="a06c2-718">這個方法可避免產生資料分割熱點，因為應用程式可以在個別的資料分割中插入和刪除每一位使用者的登入實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-718">This approach avoids partition hotspots because the application can insert and delete login entities for each user in a separate partition.</span></span> <span data-ttu-id="a06c2-719">不過如果您有大量的實體，這種方法可能既昂貴又耗時，因為您必須先執行資料表掃描以識別所有要刪除的實體，然後必須刪除每個舊的實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-719">However, this approach may be costly and time consuming if you have a large number of entities because first you need to perform a table scan in order to identify all the entities to delete, and then you must delete each old entity.</span></span> <span data-ttu-id="a06c2-720">請注意，您可以藉由將多個刪除要求批次處理到 EGT 中，以減少刪除舊實體所需的伺服器往返次數。</span><span class="sxs-lookup"><span data-stu-id="a06c2-720">Note that you can reduce the number of round trips to the server required to delete the old entities by batching multiple delete requests into EGTs.</span></span>  

#### <a name="solution"></a><span data-ttu-id="a06c2-721">方案</span><span class="sxs-lookup"><span data-stu-id="a06c2-721">Solution</span></span>
<span data-ttu-id="a06c2-722">為每天的登入嘗試使用個別的資料表。</span><span class="sxs-lookup"><span data-stu-id="a06c2-722">Use a separate table for each day of login attempts.</span></span> <span data-ttu-id="a06c2-723">當您要插入的實體時，您可以使用上述的實體設計來避免熱點，且刪除舊實體目前只不過是每天刪除一個資料表 (單一儲存體作業) 的問題而已，而無須每天尋找和刪除成千上百的個別登入實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-723">You can use the entity design above to avoid hotspots when you are inserting entities, and deleting old entities is now simply a question of deleting one table every day (a single storage operation) instead of finding and deleting hundreds and thousands of individual login entities every day.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a06c2-724">問題和考量</span><span class="sxs-lookup"><span data-stu-id="a06c2-724">Issues and considerations</span></span>
<span data-ttu-id="a06c2-725">當您決定如何實作此模式時，請考慮下列幾點：</span><span class="sxs-lookup"><span data-stu-id="a06c2-725">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a06c2-726">您的設計是否支援應用程式使用資料的其他方式，例如查閱特定實體、連結其他資料或產生彙總資訊？</span><span class="sxs-lookup"><span data-stu-id="a06c2-726">Does your design support other ways your application will use the data such as looking up specific entities, linking with other data, or generating aggregate information?</span></span>  
* <span data-ttu-id="a06c2-727">您的設計在插入新實體時是否可避免產生熱點？</span><span class="sxs-lookup"><span data-stu-id="a06c2-727">Does your design avoid hot spots when you are inserting new entities?</span></span>  
* <span data-ttu-id="a06c2-728">如果您在刪除某個資料表名稱後想要加以重複使用，預期應會有延遲。</span><span class="sxs-lookup"><span data-stu-id="a06c2-728">Expect a delay if you want to reuse the same table name after deleting it.</span></span> <span data-ttu-id="a06c2-729">最好是一律使用唯一的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="a06c2-729">It's better to always use unique table names.</span></span>  
* <span data-ttu-id="a06c2-730">當您第一次使用新的資料表時，若資料表服務可辨識存取模式，並將資料分割散發到各節點，預期應會有節流。</span><span class="sxs-lookup"><span data-stu-id="a06c2-730">Expect some throttling when you first use a new table while the Table service learns the access patterns and distributes the partitions across nodes.</span></span> <span data-ttu-id="a06c2-731">您應考量您需要建立新資料表的頻率。</span><span class="sxs-lookup"><span data-stu-id="a06c2-731">You should consider how frequently you need to create new tables.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a06c2-732">使用此模式的時機</span><span class="sxs-lookup"><span data-stu-id="a06c2-732">When to use this pattern</span></span>
<span data-ttu-id="a06c2-733">如果您有大量的實體必須同時刪除，請使用此模式。</span><span class="sxs-lookup"><span data-stu-id="a06c2-733">Use this pattern when you have a high volume of entities that you must delete at the same time.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a06c2-734">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="a06c2-734">Related patterns and guidance</span></span>
<span data-ttu-id="a06c2-735">在實作此模式時，下列模式和指導方針也可能有所關聯：</span><span class="sxs-lookup"><span data-stu-id="a06c2-735">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a06c2-736">實體群組交易</span><span class="sxs-lookup"><span data-stu-id="a06c2-736">Entity Group Transactions</span></span>](#entity-group-transactions)
* [<span data-ttu-id="a06c2-737">修改實體</span><span class="sxs-lookup"><span data-stu-id="a06c2-737">Modifying entities</span></span>](#modifying-entities)  

### <a name="data-series-pattern"></a><span data-ttu-id="a06c2-738">資料序列模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-738">Data series pattern</span></span>
<span data-ttu-id="a06c2-739">將完整資料序列儲存在單一實體中，以盡可能減少您提出的要求數。</span><span class="sxs-lookup"><span data-stu-id="a06c2-739">Store complete data series in a single entity to minimize the number of requests you make.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a06c2-740">內容和問題</span><span class="sxs-lookup"><span data-stu-id="a06c2-740">Context and problem</span></span>
<span data-ttu-id="a06c2-741">常見的案例是應用程式需一次儲存必須經常擷取的資料序列。</span><span class="sxs-lookup"><span data-stu-id="a06c2-741">A common scenario is for an application to store a series of data that it typically needs to retrieve all at once.</span></span> <span data-ttu-id="a06c2-742">比方說，您的應用程式可能會記錄每一位員工每小時傳送多少 IM 訊息，然後使用這項資訊來繪製每個使用者在過去 24 小時內傳送的訊息數。</span><span class="sxs-lookup"><span data-stu-id="a06c2-742">For example, your application might record how many IM messages each employee sends every hour, and then use this information to plot how many messages each user sent over the preceding 24 hours.</span></span> <span data-ttu-id="a06c2-743">一個設計可為每個員工儲存 24 個實體：</span><span class="sxs-lookup"><span data-stu-id="a06c2-743">One design might be to store 24 entities for each employee:</span></span>  

![][22]

<span data-ttu-id="a06c2-744">採用這種設計，您可以輕鬆地找出並更新實體，以在應用程式需要更新訊息計數值時更新每個員工。</span><span class="sxs-lookup"><span data-stu-id="a06c2-744">With this design, you can easily locate and update the entity to update for each employee whenever the application needs to update the message count value.</span></span> <span data-ttu-id="a06c2-745">不過，若要擷取資訊以繪製過去 24 小時內的活動圖，您必須擷取 24 個實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-745">However, to retrieve the information to plot a chart of the activity for the preceding 24 hours, you must retrieve 24 entities.</span></span>  

#### <a name="solution"></a><span data-ttu-id="a06c2-746">方案</span><span class="sxs-lookup"><span data-stu-id="a06c2-746">Solution</span></span>
<span data-ttu-id="a06c2-747">使用下列具有個別屬性的設計，儲存每個小時的訊息計數：</span><span class="sxs-lookup"><span data-stu-id="a06c2-747">Use the following design with a separate property to store the message count for each hour:</span></span>  

![][23]

<span data-ttu-id="a06c2-748">透過這項設計，您可以使用合併作業來更新員工在特定時段內的訊息計數。</span><span class="sxs-lookup"><span data-stu-id="a06c2-748">With this design, you can use a merge operation to update the message count for an employee for a specific hour.</span></span> <span data-ttu-id="a06c2-749">現在，您可以使用單一實體的要求，擷取您要繪圖所需的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="a06c2-749">Now, you can retrieve all the information you need to plot the chart using a request for a single entity.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a06c2-750">問題和考量</span><span class="sxs-lookup"><span data-stu-id="a06c2-750">Issues and considerations</span></span>
<span data-ttu-id="a06c2-751">當您決定如何實作此模式時，請考慮下列幾點：</span><span class="sxs-lookup"><span data-stu-id="a06c2-751">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a06c2-752">如果您完整資料序列不適用於單一實體 (一個實體可以有 252 個屬性)，請使用替代資料存放區，例如 Blob。</span><span class="sxs-lookup"><span data-stu-id="a06c2-752">If your complete data series does not fit into a single entity (an entity can have up to 252 properties), use an alternative data store such as a blob.</span></span>  
* <span data-ttu-id="a06c2-753">如果您有多個用戶端同時更新實體，您必須使用 **ETag** 實作開放式並行存取。</span><span class="sxs-lookup"><span data-stu-id="a06c2-753">If you have multiple clients updating an entity simultaneously, you will need to use the **ETag** to implement optimistic concurrency.</span></span> <span data-ttu-id="a06c2-754">如果您有許多用戶端，則預期應會有激烈的爭用情況。</span><span class="sxs-lookup"><span data-stu-id="a06c2-754">If you have many clients, you may experience high contention.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a06c2-755">使用此模式的時機</span><span class="sxs-lookup"><span data-stu-id="a06c2-755">When to use this pattern</span></span>
<span data-ttu-id="a06c2-756">如果您需要更新和擷取與個別實體相關聯的資料序列，請使用此模式。</span><span class="sxs-lookup"><span data-stu-id="a06c2-756">Use this pattern when you need to update and retrieve a data series associated with an individual entity.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a06c2-757">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="a06c2-757">Related patterns and guidance</span></span>
<span data-ttu-id="a06c2-758">在實作此模式時，下列模式和指導方針也可能有所關聯：</span><span class="sxs-lookup"><span data-stu-id="a06c2-758">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a06c2-759">大型實體模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-759">Large entities pattern</span></span>](#large-entities-pattern)  
* [<span data-ttu-id="a06c2-760">合併或取代</span><span class="sxs-lookup"><span data-stu-id="a06c2-760">Merge or replace</span></span>](#merge-or-replace)  
* <span data-ttu-id="a06c2-761">[最終一致的交易模式](#eventually-consistent-transactions-pattern) (如果您要將資料數列儲存在 Blob 中)</span><span class="sxs-lookup"><span data-stu-id="a06c2-761">[Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) (if you are storing the data series in a blob)</span></span>  

### <a name="wide-entities-pattern"></a><span data-ttu-id="a06c2-762">寬型實體模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-762">Wide entities pattern</span></span>
<span data-ttu-id="a06c2-763">使用多個實際的實體來儲存具有超過 252 個屬性的邏輯實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-763">Use multiple physical entities to store logical entities with more than 252 properties.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a06c2-764">內容和問題</span><span class="sxs-lookup"><span data-stu-id="a06c2-764">Context and problem</span></span>
<span data-ttu-id="a06c2-765">個別實體可以擁有超過 252 個 (不含必要的系統屬性) 屬性，而且無法儲存總計超過 1 MB 的資料。</span><span class="sxs-lookup"><span data-stu-id="a06c2-765">An individual entity can have no more than 252 properties (excluding the mandatory system properties) and cannot store more than 1 MB of data in total.</span></span> <span data-ttu-id="a06c2-766">在關聯式資料庫中，您會通常可藉由新增資料表並對其施行一對一關聯性，來解決任何資料列的大小限制。</span><span class="sxs-lookup"><span data-stu-id="a06c2-766">In a relational database, you would typically get round any limits on the size of a row by adding a new table and enforcing a 1-to-1 relationship between them.</span></span>  

#### <a name="solution"></a><span data-ttu-id="a06c2-767">方案</span><span class="sxs-lookup"><span data-stu-id="a06c2-767">Solution</span></span>
<span data-ttu-id="a06c2-768">使用資料表服務，可讓您儲存多個實體來代表具有超過 252 個屬性的單一大型商業物件。</span><span class="sxs-lookup"><span data-stu-id="a06c2-768">Using the Table service, you can store multiple entities to represent a single large business object with more than 252 properties.</span></span> <span data-ttu-id="a06c2-769">例如，如果您想要儲存每個員工在 365 天內傳送的 IM 訊息計數，您可以採用下列設計，使用兩個具有不同結構描述的實體：</span><span class="sxs-lookup"><span data-stu-id="a06c2-769">For example, if you want to store a count of the number of IM messages sent by each employee for the last 365 days, you could use the following design that uses two entities with different schemas:</span></span>  

![][24]

<span data-ttu-id="a06c2-770">如果您需要進行必須同時更新兩個實體的變更，讓它們彼此保持同步，您可以使用 EGT。</span><span class="sxs-lookup"><span data-stu-id="a06c2-770">If you need to make a change that requires updating both entities to keep them synchronized with each other you can use an EGT.</span></span> <span data-ttu-id="a06c2-771">否則，您可以使用合併作業來更新某天的訊息計數。</span><span class="sxs-lookup"><span data-stu-id="a06c2-771">Otherwise, you can use a single merge operation to update the message count for a specific day.</span></span> <span data-ttu-id="a06c2-772">若要擷取個別員工的所有資料，您必須都擷取這兩個實體；您可以透過兩個同時使用 **PartitionKey** 和 **RowKey** 值的有效要求來完成此動作。</span><span class="sxs-lookup"><span data-stu-id="a06c2-772">To retrieve all the data for an individual employee you must retrieve both entities, which you can do with two efficient requests that use both a **PartitionKey** and a **RowKey** value.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a06c2-773">問題和考量</span><span class="sxs-lookup"><span data-stu-id="a06c2-773">Issues and considerations</span></span>
<span data-ttu-id="a06c2-774">當您決定如何實作此模式時，請考慮下列幾點：</span><span class="sxs-lookup"><span data-stu-id="a06c2-774">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a06c2-775">擷取完成邏輯實體牽涉到至少兩個儲存體交易：一個用來擷取每個實際的實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-775">Retrieving a complete logical entity involves at least two storage transactions: one to retrieve each physical entity.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a06c2-776">使用此模式的時機</span><span class="sxs-lookup"><span data-stu-id="a06c2-776">When to use this pattern</span></span>
<span data-ttu-id="a06c2-777">如果需要在資料表服務中儲存屬性的大小或數目超過個別實體限制的實體，請使用此模式。</span><span class="sxs-lookup"><span data-stu-id="a06c2-777">Use this pattern when  need to store entities whose size or number of properties exceeds the limits for an individual entity in the Table service.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a06c2-778">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="a06c2-778">Related patterns and guidance</span></span>
<span data-ttu-id="a06c2-779">在實作此模式時，下列模式和指導方針也可能有所關聯：</span><span class="sxs-lookup"><span data-stu-id="a06c2-779">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a06c2-780">實體群組交易</span><span class="sxs-lookup"><span data-stu-id="a06c2-780">Entity Group Transactions</span></span>](#entity-group-transactions)
* [<span data-ttu-id="a06c2-781">合併或取代</span><span class="sxs-lookup"><span data-stu-id="a06c2-781">Merge or replace</span></span>](#merge-or-replace)

### <a name="large-entities-pattern"></a><span data-ttu-id="a06c2-782">大型實體模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-782">Large entities pattern</span></span>
<span data-ttu-id="a06c2-783">使用 Blob 儲存體來儲存大型屬性值。</span><span class="sxs-lookup"><span data-stu-id="a06c2-783">Use blob storage to store large property values.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a06c2-784">內容和問題</span><span class="sxs-lookup"><span data-stu-id="a06c2-784">Context and problem</span></span>
<span data-ttu-id="a06c2-785">個別實體無法儲存總計超過 1 MB 的資料。</span><span class="sxs-lookup"><span data-stu-id="a06c2-785">An individual entity cannot store more than 1 MB of data in total.</span></span> <span data-ttu-id="a06c2-786">如果有一或多個屬性所儲存的值會導致您的實體大小總計超過此值，您將無法在資料表服務中儲存整個實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-786">If one or several of your properties store values that cause the total size of your entity to exceed this value, you cannot store the entire entity in the Table service.</span></span>  

#### <a name="solution"></a><span data-ttu-id="a06c2-787">方案</span><span class="sxs-lookup"><span data-stu-id="a06c2-787">Solution</span></span>
<span data-ttu-id="a06c2-788">如果您的實體因為一或多個屬性包含大量資料而使大小超過 1 MB，您可以將資料儲存在 Blob 服務，然後將 Blob 的位址儲存在實體的屬性中。</span><span class="sxs-lookup"><span data-stu-id="a06c2-788">If your entity exceeds 1 MB in size because one or more properties contain a large amount of data, you can store data in the Blob service and then store the address of the blob in a property in the entity.</span></span> <span data-ttu-id="a06c2-789">比方說，您可以在 Blob 儲存體中儲存員工的相片，並將相片的連結儲存在員工實體的 **Photo** 屬性中：</span><span class="sxs-lookup"><span data-stu-id="a06c2-789">For example, you can store the photo of an employee in blob storage and store a link to the photo in the **Photo** property of your employee entity:</span></span>  

![][25]

#### <a name="issues-and-considerations"></a><span data-ttu-id="a06c2-790">問題和考量</span><span class="sxs-lookup"><span data-stu-id="a06c2-790">Issues and considerations</span></span>
<span data-ttu-id="a06c2-791">當您決定如何實作此模式時，請考慮下列幾點：</span><span class="sxs-lookup"><span data-stu-id="a06c2-791">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a06c2-792">若要讓資料表格服務中的實體與 Blob 服務中的資料之間保有最終一致性，請使用 [最終一致的交易模式](#eventually-consistent-transactions-pattern) 維護您的實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-792">To maintain eventual consistency between the entity in the Table service and the data in the Blob service, use the [Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) to maintain your entities.</span></span>
* <span data-ttu-id="a06c2-793">擷取完整實體牽涉到至少兩個儲存體交易：一個用來擷取實體，另一個擷取 Blob 資料。</span><span class="sxs-lookup"><span data-stu-id="a06c2-793">Retrieving a complete entity involves at least two storage transactions: one to retrieve the entity and one to retrieve the blob data.</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a06c2-794">使用此模式的時機</span><span class="sxs-lookup"><span data-stu-id="a06c2-794">When to use this pattern</span></span>
<span data-ttu-id="a06c2-795">如果需要在資料表服務中儲存大小超過個別實體限制的實體，請使用此模式。</span><span class="sxs-lookup"><span data-stu-id="a06c2-795">Use this pattern when you need to store entities whose size exceeds the limits for an individual entity in the Table service.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a06c2-796">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="a06c2-796">Related patterns and guidance</span></span>
<span data-ttu-id="a06c2-797">在實作此模式時，下列模式和指導方針也可能有所關聯：</span><span class="sxs-lookup"><span data-stu-id="a06c2-797">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a06c2-798">最終一致的交易模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-798">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  
* [<span data-ttu-id="a06c2-799">寬型實體模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-799">Wide entities pattern</span></span>](#wide-entities-pattern)

<a name="prepend-append-anti-pattern"></a>

### <a name="prependappend-anti-pattern"></a><span data-ttu-id="a06c2-800">在前面加上/附加反向模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-800">Prepend/append anti-pattern</span></span>
<span data-ttu-id="a06c2-801">當您有大量插入作業時，請將插入作業分散到多個資料分割之間，請增加延展性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-801">Increase scalability when you have a high volume of inserts by spreading the inserts across multiple partitions.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a06c2-802">內容和問題</span><span class="sxs-lookup"><span data-stu-id="a06c2-802">Context and problem</span></span>
<span data-ttu-id="a06c2-803">在前面加上或附加實體至您已儲存的實體，通常會導致應用程式將新實體新增至資料分割序列的第一個或最後一個資料分割。</span><span class="sxs-lookup"><span data-stu-id="a06c2-803">Prepending or appending entities to your stored entities typically results in the application adding new entities to the first or last partition of a sequence of partitions.</span></span> <span data-ttu-id="a06c2-804">在此情況下，所有在任何給定時間的插入將會在相同的資料分割中執行，而產生使資料表服務無法將插入負載平衡到多個節點間的熱點，且可能會造成您的應用程式達到資料分割的延展性目標。</span><span class="sxs-lookup"><span data-stu-id="a06c2-804">In this case, all of the inserts at any given time are taking place in the same partition, creating a hotspot that prevents the table service from load balancing inserts across multiple nodes, and possibly causing your application to hit the scalability targets for partition.</span></span> <span data-ttu-id="a06c2-805">例如，如果您的應用程式會記錄員工的網路和資源存取，在交易量已達到個別資料分割的延展性目標時，則如下的實體結構可能會導致目前小時的資料分割成為熱點：</span><span class="sxs-lookup"><span data-stu-id="a06c2-805">For example, if you have an application that logs network and resource access by employees, then an entity structure as shown below could result in the current hour's partition becoming a hotspot if the volume of transactions reaches the scalability target for an individual partition:</span></span>  

![][26]

#### <a name="solution"></a><span data-ttu-id="a06c2-806">方案</span><span class="sxs-lookup"><span data-stu-id="a06c2-806">Solution</span></span>
<span data-ttu-id="a06c2-807">下列替代實體結構可在應用程式記錄事件時避免在任何特定資料分割上產生熱點：</span><span class="sxs-lookup"><span data-stu-id="a06c2-807">The following alternative entity structure avoids a hotspot on any particular partition as the application logs events:</span></span>  

![][27]

<span data-ttu-id="a06c2-808">請留意此範例中的 **PartitionKey** 和 **RowKey** 如何成為複合索引鍵。</span><span class="sxs-lookup"><span data-stu-id="a06c2-808">Notice with this example how both the **PartitionKey** and **RowKey** are compound keys.</span></span> <span data-ttu-id="a06c2-809">**PartitionKey** 會同時使用部門和員工識別碼將記錄散發到多個資料分割。</span><span class="sxs-lookup"><span data-stu-id="a06c2-809">The **PartitionKey** uses both the department and employee id to distribute the logging across multiple partitions.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a06c2-810">問題和考量</span><span class="sxs-lookup"><span data-stu-id="a06c2-810">Issues and considerations</span></span>
<span data-ttu-id="a06c2-811">當您決定如何實作此模式時，請考慮下列幾點：</span><span class="sxs-lookup"><span data-stu-id="a06c2-811">Consider the following points when deciding how to implement this pattern:</span></span>  

* <span data-ttu-id="a06c2-812">可避免在插入時產生熱點資料分割的替代索引鍵結構，是否可有效支援用戶端應用程式發出的查詢？</span><span class="sxs-lookup"><span data-stu-id="a06c2-812">Does the alternative key structure that avoids creating hot partitions on inserts efficiently support the queries your client application makes?</span></span>  
* <span data-ttu-id="a06c2-813">您預期的交易量是否表示您很可能會達到個別資料分割的延展性目標，而遭到儲存體服務的節流？</span><span class="sxs-lookup"><span data-stu-id="a06c2-813">Does your anticipated volume of transactions mean that you are likely to reach the scalability targets for an individual partition and be throttled by the storage service?</span></span>  

#### <a name="when-to-use-this-pattern"></a><span data-ttu-id="a06c2-814">使用此模式的時機</span><span class="sxs-lookup"><span data-stu-id="a06c2-814">When to use this pattern</span></span>
<span data-ttu-id="a06c2-815">如果您的交易量在您存取熱點資料分割時很可能會導致儲存體服務執行節流，請避免在前面加上/附加反向模式。</span><span class="sxs-lookup"><span data-stu-id="a06c2-815">Avoid the prepend/append anti-pattern when your volume of transactions is likely to result in throttling by the storage service when you access a hot partition.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="a06c2-816">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="a06c2-816">Related patterns and guidance</span></span>
<span data-ttu-id="a06c2-817">在實作此模式時，下列模式和指導方針也可能有所關聯：</span><span class="sxs-lookup"><span data-stu-id="a06c2-817">The following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="a06c2-818">複合索引鍵模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-818">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="a06c2-819">記錄檔結尾模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-819">Log tail pattern</span></span>](#log-tail-pattern)  
* [<span data-ttu-id="a06c2-820">修改實體</span><span class="sxs-lookup"><span data-stu-id="a06c2-820">Modifying entities</span></span>](#modifying-entities)  

### <a name="log-data-anti-pattern"></a><span data-ttu-id="a06c2-821">記錄資料反向模式</span><span class="sxs-lookup"><span data-stu-id="a06c2-821">Log data anti-pattern</span></span>
<span data-ttu-id="a06c2-822">一般而言，您應該使用 Blob 服務來儲存記錄資料，而不是資料表服務。</span><span class="sxs-lookup"><span data-stu-id="a06c2-822">Typically, you should use the Blob service instead of the Table service to store log data.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="a06c2-823">內容和問題</span><span class="sxs-lookup"><span data-stu-id="a06c2-823">Context and problem</span></span>
<span data-ttu-id="a06c2-824">記錄資料的常見使用案例是要擷取特定日期/時間範圍內的選定記錄項目：例如，您想要尋找應用程式在特定日期的 15:04 到 15:06 之間記錄的所有錯誤和嚴重訊息。</span><span class="sxs-lookup"><span data-stu-id="a06c2-824">A common use case for log data is to retrieve a selection of log entries for a specific date/time range: for example, you want to find all the error and critical messages that your application logged between 15:04 and 15:06 on a specific date.</span></span> <span data-ttu-id="a06c2-825">您不應使用記錄訊息的日期和時間來判斷儲存記錄實體的資料分割：這會產生熱點資料分割，因為在任何給定時間，所有的記錄實體都會共用相同的 **PartitionKey** 值 (請參閱 [在前面加上/附加反向模式](#prepend-append-anti-pattern)一節)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-825">You do not want to use the date and time of the log message to determine the partition you save log entities to: that results in a hot partition because at any given time, all the log entities will share the same **PartitionKey** value (see the section [Prepend/append anti-pattern](#prepend-append-anti-pattern)).</span></span> <span data-ttu-id="a06c2-826">比方說，記錄訊息的下列實體結構描述會產生熱點資料分割，因為應用程式會將目前日期和小時的所有記錄訊息都寫入至資料分割：</span><span class="sxs-lookup"><span data-stu-id="a06c2-826">For example, the following entity schema for a log message results in a hot partition because the application writes all log messages to the partition for the current date and hour:</span></span>  

![][28]

<span data-ttu-id="a06c2-827">在此範例中， **RowKey** 包含記錄訊息的日期和時間，以確保記錄訊息在儲存時會以日期/時間順序排序，且包含訊息識別碼，以便在有多個記錄訊息共用相同日期和時間時參考。</span><span class="sxs-lookup"><span data-stu-id="a06c2-827">In this example, the **RowKey** includes the date and time of the log message to ensure that log messages are stored sorted in date/time order, and includes a message id in case multiple log messages share the same date and time.</span></span>  

<span data-ttu-id="a06c2-828">另一種方法是使用 **PartitionKey** ，以確保應用程式將訊息寫入一個範圍內的資料分割。</span><span class="sxs-lookup"><span data-stu-id="a06c2-828">Another approach is to use a **PartitionKey** that ensures that the application writes messages across a range of partitions.</span></span> <span data-ttu-id="a06c2-829">例如，如果記錄訊息的來源可藉由某方式將訊息散發到許多資料分割，您可以使用下列實體結構描述：</span><span class="sxs-lookup"><span data-stu-id="a06c2-829">For example, if the source of the log message provides a way to distribute messages across many partitions, you could use the following entity schema:</span></span>  

![][29]

<span data-ttu-id="a06c2-830">不過，此結構描述的問題是，若要擷取特定時間範圍內的所有記錄訊息，您必須在資料表中搜尋每個資料分割。</span><span class="sxs-lookup"><span data-stu-id="a06c2-830">However, the problem with this schema is that to retrieve all the log messages for a specific time span you must search every partition in the table.</span></span>

#### <a name="solution"></a><span data-ttu-id="a06c2-831">方案</span><span class="sxs-lookup"><span data-stu-id="a06c2-831">Solution</span></span>
<span data-ttu-id="a06c2-832">上一節加強說明了嘗試使用資料表服務來儲存記錄項目的問題，並提供了兩個無法令人滿意的設計。</span><span class="sxs-lookup"><span data-stu-id="a06c2-832">The previous section highlighted the problem of trying to use the Table service to store log entries and suggested two, unsatisfactory, designs.</span></span> <span data-ttu-id="a06c2-833">一個方案會導致熱點資料分割，且具有寫入記錄檔訊息效能不佳的風險；另一個方案會導致查詢效能不佳，因為必須要掃描資料表中的每個資料分割，才能擷取特定時間範圍內的記錄訊息。</span><span class="sxs-lookup"><span data-stu-id="a06c2-833">One solution led to a hot partition with the risk of poor performance writing log messages; the other solution resulted in poor query performance because of the requirement to scan every partition in the table to retrieve log messages for a specific time span.</span></span> <span data-ttu-id="a06c2-834">Blob 儲存體可為這種類型的案例提供更好的方案，Azure Storage Analytics 就是以此方式來儲存它所收集到的記錄資料。</span><span class="sxs-lookup"><span data-stu-id="a06c2-834">Blob storage offers a better solution for this type of scenario and this is how Azure Storage Analytics stores the log data it collects.</span></span>  

<span data-ttu-id="a06c2-835">本節概述 Storage Analytics 將記錄資料儲存在 Blob 儲存體中的方式，以說明如何以此方法儲存您常會依範圍查詢的資料。</span><span class="sxs-lookup"><span data-stu-id="a06c2-835">This section outlines how Storage Analytics stores log data in blob storage as an illustration of this approach to storing data that you typically query by range.</span></span>  

<span data-ttu-id="a06c2-836">Storage Analytics 會以分隔格式將記錄訊息儲存在多個 Blob 中。</span><span class="sxs-lookup"><span data-stu-id="a06c2-836">Storage Analytics stores log messages in a delimited format in multiple blobs.</span></span> <span data-ttu-id="a06c2-837">分隔格式可方便用戶端應用程式剖析記錄訊息中的資料。</span><span class="sxs-lookup"><span data-stu-id="a06c2-837">The delimited format makes it easy for a client application to parse the data in the log message.</span></span>  

<span data-ttu-id="a06c2-838">Storage Analytics 會為 Blob 使用命名慣例，讓您找出含有您要搜尋之記錄訊息的一或多個 Blob。</span><span class="sxs-lookup"><span data-stu-id="a06c2-838">Storage Analytics uses a naming convention for blobs that enables you to locate the blob (or blobs) that contain the log messages for which you are searching.</span></span> <span data-ttu-id="a06c2-839">例如，名為 "queue/2014/07/31/1800/000001.log" 的 Blob，會包含與始於 2014 年 7 月 31 日 18:00 的佇列服務有關的記錄訊息。</span><span class="sxs-lookup"><span data-stu-id="a06c2-839">For example, a blob named "queue/2014/07/31/1800/000001.log" contains log messages that relate to the queue service for the hour starting at 18:00 on 31 July 2014.</span></span> <span data-ttu-id="a06c2-840">"000001"表示這是這段期間的第一個記錄檔。</span><span class="sxs-lookup"><span data-stu-id="a06c2-840">The "000001" indicates that this is the first log file for this period.</span></span> <span data-ttu-id="a06c2-841">儲存體分析也會記錄在檔案中儲存為 Blob 中繼資料的第一個和最後一個記錄訊息的時間戳記。</span><span class="sxs-lookup"><span data-stu-id="a06c2-841">Storage Analytics also records the timestamps of the first and last log messages stored in the file as part of the blob's metadata.</span></span> <span data-ttu-id="a06c2-842">Blob 儲存體的 API 可讓您根據名稱前置詞找出容器中的 Blob：若要尋找所有內含從 18:00 開始之佇列記錄資料的 Blob，您可以使用前置詞 "queue/2014/07/31/1800"。</span><span class="sxs-lookup"><span data-stu-id="a06c2-842">The API for blob storage enables you locate blobs in a container based on a name prefix: to locate all the blobs that contain queue log data for the hour starting at 18:00, you can use the prefix "queue/2014/07/31/1800."</span></span>  

<span data-ttu-id="a06c2-843">Storage Analytics 會在內部緩衝處理記錄訊息，然後定期更新適當的 Blob，或建立新的 Blob 來容納記錄項目的最新批次。</span><span class="sxs-lookup"><span data-stu-id="a06c2-843">Storage Analytics buffers log messages internally and then periodically updates the appropriate blob or creates a new one with the latest batch of log entries.</span></span> <span data-ttu-id="a06c2-844">這會減少它必須對 Blob 服務執行的寫入數目。</span><span class="sxs-lookup"><span data-stu-id="a06c2-844">This reduces the number of writes it must perform to the blob service.</span></span>  

<span data-ttu-id="a06c2-845">如果您在自己的應用程式中實作類似的方案，您必須考量如何管理可靠性 (在每個記錄項目發生時將其寫入至 Blob 儲存體)、成本和延展性 (在您的應用程式中緩衝處理更新，並將其分批寫入至 Blob 儲存體) 之間的取捨。</span><span class="sxs-lookup"><span data-stu-id="a06c2-845">If you are implementing a similar solution in your own application, you must consider how to manage the trade-off between reliability (writing every log entry to blob storage as it happens) and cost and scalability (buffering updates in your application and writing them to blob storage in batches).</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="a06c2-846">問題和考量</span><span class="sxs-lookup"><span data-stu-id="a06c2-846">Issues and considerations</span></span>
<span data-ttu-id="a06c2-847">當您決定如何儲存記錄資料時，請考慮下列幾點：</span><span class="sxs-lookup"><span data-stu-id="a06c2-847">Consider the following points when deciding how to store log data:</span></span>  

* <span data-ttu-id="a06c2-848">如果您建立的資料表設計可避免產生潛在的熱點資料分割，您可能會發現您無法有效率地存取記錄資料。</span><span class="sxs-lookup"><span data-stu-id="a06c2-848">If you create a table design that avoids potential hot partitions, you may find that you cannot access your log data efficiently.</span></span>  
* <span data-ttu-id="a06c2-849">在處理記錄資料時，用戶端常需要載入多筆記錄。</span><span class="sxs-lookup"><span data-stu-id="a06c2-849">To process log data, a client often needs to load many records.</span></span>  
* <span data-ttu-id="a06c2-850">雖然記錄資料通常是結構化的，Blob 儲存體會是較佳的方案。</span><span class="sxs-lookup"><span data-stu-id="a06c2-850">Although log data is often structured, blob storage may be a better solution.</span></span>  

### <a name="implementation-considerations"></a><span data-ttu-id="a06c2-851">實作考量</span><span class="sxs-lookup"><span data-stu-id="a06c2-851">Implementation considerations</span></span>
<span data-ttu-id="a06c2-852">本節討論您在實作前面幾節說明的模式時應謹記在心的注意事項。</span><span class="sxs-lookup"><span data-stu-id="a06c2-852">This section discusses some of the considerations to bear in mind when you implement the patterns described in the previous sections.</span></span> <span data-ttu-id="a06c2-853">本節中的範例大多是以 C# 撰寫，並使用儲存體用戶端程式庫 (撰寫本文時為 4.3.0 版)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-853">Most of this section uses examples written in C# that use the Storage Client Library (version 4.3.0 at the time of writing).</span></span>  

### <a name="retrieving-entities"></a><span data-ttu-id="a06c2-854">擷取實體</span><span class="sxs-lookup"><span data-stu-id="a06c2-854">Retrieving entities</span></span>
<span data-ttu-id="a06c2-855">如 [查詢的設計](#design-for-querying)一節中所述，最有效率的查詢是點查詢。</span><span class="sxs-lookup"><span data-stu-id="a06c2-855">As discussed in the section [Design for querying](#design-for-querying), the most efficient query is a point query.</span></span> <span data-ttu-id="a06c2-856">但在某些情況下，您可能需要擷取多個實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-856">However, in some scenarios you may need to retrieve multiple entities.</span></span> <span data-ttu-id="a06c2-857">本節說明使用儲存體用戶端程式庫來擷取實體的一些常見方法。</span><span class="sxs-lookup"><span data-stu-id="a06c2-857">This section describes some common approaches to retrieving entities using the Storage Client Library.</span></span>  

#### <a name="executing-a-point-query-using-the-storage-client-library"></a><span data-ttu-id="a06c2-858">使用儲存體用戶端程式庫執行點查詢</span><span class="sxs-lookup"><span data-stu-id="a06c2-858">Executing a point query using the Storage Client Library</span></span>
<span data-ttu-id="a06c2-859">要執行點查詢，最簡單的方式是使用下列 C# 程式碼片段中展示的**擷取**資料表作業，來擷取 **PartitionKey** 值為 "Sales" 和 **RowKey** 值為 "212" 的實體：</span><span class="sxs-lookup"><span data-stu-id="a06c2-859">The easiest way to execute a point query is to use the **Retrieve** table operation as shown in the following C# code snippet that retrieves an entity with a **PartitionKey** of value "Sales" and a **RowKey** of value "212":</span></span>  

```csharp
TableOperation retrieveOperation = TableOperation.Retrieve<EmployeeEntity>("Sales", "212");
var retrieveResult = employeeTable.Execute(retrieveOperation);
if (retrieveResult.Result != null)
{
    EmployeeEntity employee = (EmployeeEntity)retrieveResult.Result;
    ...
}  
```

<span data-ttu-id="a06c2-860">請注意，此範例預期會擷取的實體屬於 **EmployeeEntity**類型。</span><span class="sxs-lookup"><span data-stu-id="a06c2-860">Notice how this example expects the entity it retrieves to be of type **EmployeeEntity**.</span></span>  

#### <a name="retrieving-multiple-entities-using-linq"></a><span data-ttu-id="a06c2-861">使用 LINQ 擷取多個實體</span><span class="sxs-lookup"><span data-stu-id="a06c2-861">Retrieving multiple entities using LINQ</span></span>
<span data-ttu-id="a06c2-862">您可以搭配使用 LINQ 與儲存體用戶端程式庫，並指定具有 **where** 子句的查詢，以擷取多個實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-862">You can retrieve multiple entities by using LINQ with Storage Client Library and specifying a query with a **where** clause.</span></span> <span data-ttu-id="a06c2-863">若要避免資料表掃描，您應一律在 where 子句中加入 **PartitionKey** 值，並盡可能加入 **RowKey** 值，以防止資料表和資料分割掃描。</span><span class="sxs-lookup"><span data-stu-id="a06c2-863">To avoid a table scan, you should always include the **PartitionKey** value in the where clause, and if possible the **RowKey** value to avoid table and partition scans.</span></span> <span data-ttu-id="a06c2-864">資料表服務支援在 where 子句中使用一組有限的比較運算子 (大於、大於或等於、小於、小於或等於、等於和不等於)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-864">The table service supports a limited set of comparison operators (greater than, greater than or equal, less than, less than or equal, equal, and not equal) to use in the where clause.</span></span> <span data-ttu-id="a06c2-865">下列 C# 程式碼片段會在業務部門 (假設 **PartitionKey** 儲存部門名稱) 中，尋找姓氏以 "B" 開頭的所有員工 (假設 **RowKey** 儲存姓氏)：</span><span class="sxs-lookup"><span data-stu-id="a06c2-865">The following C# code snippet finds all the employees whose last name starts with "B" (assuming that the **RowKey** stores the last name) in the sales department (assuming the **PartitionKey** stores the department name):</span></span>  

```csharp
TableQuery<EmployeeEntity> employeeQuery = employeeTable.CreateQuery<EmployeeEntity>();
var query = (from employee in employeeQuery
            where employee.PartitionKey == "Sales" &&
            employee.RowKey.CompareTo("B") >= 0 &&
            employee.RowKey.CompareTo("C") < 0
            select employee).AsTableQuery();
var employees = query.Execute();  
```

<span data-ttu-id="a06c2-866">請注意查詢如何同時指定 **RowKey** 和 **PartitionKey** 以確保更好的效能。</span><span class="sxs-lookup"><span data-stu-id="a06c2-866">Notice how the query specifies both a **RowKey** and a **PartitionKey** to ensure better performance.</span></span>  

<span data-ttu-id="a06c2-867">下列程式碼範例說明使用 Fluent API 的對等功能 (如需 Fluent API 的詳細資訊，請參閱 [設計 Fluent API 的最佳做法](http://visualstudiomagazine.com/articles/2013/12/01/best-practices-for-designing-a-fluent-api.aspx))：</span><span class="sxs-lookup"><span data-stu-id="a06c2-867">The following code sample shows equivalent functionality using the fluent API (for more information about fluent APIs in general, see [Best Practices for Designing a Fluent API](http://visualstudiomagazine.com/articles/2013/12/01/best-practices-for-designing-a-fluent-api.aspx)):</span></span>  

```csharp
TableQuery<EmployeeEntity> employeeQuery = new TableQuery<EmployeeEntity>().Where(
    TableQuery.CombineFilters(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition(
    "PartitionKey", QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.GenerateFilterCondition(
    "RowKey", QueryComparisons.GreaterThanOrEqual, "B")
),
TableOperators.And,
TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "C")
    )
);
var employees = employeeTable.ExecuteQuery(employeeQuery);  
```

> [!NOTE]
> <span data-ttu-id="a06c2-868">此範例內嵌了多個 **CombineFilters** 方法，以納入三個篩選條件。</span><span class="sxs-lookup"><span data-stu-id="a06c2-868">The sample nests multiple **CombineFilters** methods to include the three filter conditions.</span></span>  
> 
> 

#### <a name="retrieving-large-numbers-of-entities-from-a-query"></a><span data-ttu-id="a06c2-869">從查詢擷取大量實體</span><span class="sxs-lookup"><span data-stu-id="a06c2-869">Retrieving large numbers of entities from a query</span></span>
<span data-ttu-id="a06c2-870">最佳查詢會根據 **PartitionKey** 值和 **RowKey** 值傳回個別實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-870">An optimal query returns an individual entity based on a **PartitionKey** value and a **RowKey** value.</span></span> <span data-ttu-id="a06c2-871">但在某些情況下，您可能需要從相同的磁碟分割甚或多個資料分割傳回許多實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-871">However, in some scenarios you may have a requirement to return many entities from the same partition or even from many partitions.</span></span>  

<span data-ttu-id="a06c2-872">在此類情況下，您務必要完整測試應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="a06c2-872">You should always fully test the performance of your application in such scenarios.</span></span>  

<span data-ttu-id="a06c2-873">對資料表服務的查詢一次最多可傳回 1000 個實體，且最長可執行五秒。</span><span class="sxs-lookup"><span data-stu-id="a06c2-873">A query against the table service may return a maximum of 1,000 entities at one time and may execute for a maximum of five seconds.</span></span> <span data-ttu-id="a06c2-874">如果結果集包含超過 1000 個實體，且查詢未於五秒內完成，或者查詢跨越資料分割界限，則資料表服務會傳回接續權杖，讓用戶端應用程式能夠要求下一組實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-874">If the result set contains more than 1,000 entities, if the query did not complete within five seconds, or if the query crosses the partition boundary, the Table service returns a continuation token to enable the client application to request the next set of entities.</span></span> <span data-ttu-id="a06c2-875">如需接續權杖如何運作的詳細資訊，請參閱 [查詢逾時和分頁](http://msdn.microsoft.com/library/azure/dd135718.aspx)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-875">For more information about how continuation tokens work, see [Query Timeout and Pagination](http://msdn.microsoft.com/library/azure/dd135718.aspx).</span></span>  

<span data-ttu-id="a06c2-876">如果您使用儲存體用戶端程式庫，它可以在從資料表服務傳回實體時，自動為您處理接續權杖。</span><span class="sxs-lookup"><span data-stu-id="a06c2-876">If you are using the Storage Client Library, it can automatically handle continuation tokens for you as it returns entities from the Table service.</span></span> <span data-ttu-id="a06c2-877">下列使用儲存體用戶端程式庫的 C# 程式碼範例會在資料表服務於回應中傳回接續權杖時自動處理接續權杖：</span><span class="sxs-lookup"><span data-stu-id="a06c2-877">The following C# code sample using the Storage Client Library automatically handles continuation tokens if the table service returns them in a response:</span></span>  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

var employees = employeeTable.ExecuteQuery(employeeQuery);
foreach (var emp in employees)
{
        ...
}  
```

<span data-ttu-id="a06c2-878">下列 C# 程式碼會明確處理接續權杖：</span><span class="sxs-lookup"><span data-stu-id="a06c2-878">The following C# code handles continuation tokens explicitly:</span></span>  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

TableContinuationToken continuationToken = null;

do
{
        var employees = employeeTable.ExecuteQuerySegmented(
        employeeQuery, continuationToken);
    foreach (var emp in employees)
    {
    ...
    }
    continuationToken = employees.ContinuationToken;
} while (continuationToken != null);  
```

<span data-ttu-id="a06c2-879">藉由明確使用接續權杖，您將可控制應用程式何時會擷取下一個資料區段。</span><span class="sxs-lookup"><span data-stu-id="a06c2-879">By using continuation tokens explicitly, you can control when your application retrieves the next segment of data.</span></span> <span data-ttu-id="a06c2-880">例如，如果用戶端應用程式可讓使用者逐頁查看儲存在資料表中的實體，使用者可以決定不逐頁查看查詢所擷取的所有實體，而在使用者逐頁查看完目前區段中的所有實體時，您的應用程式才會使用接續權杖擷取下一個區段。</span><span class="sxs-lookup"><span data-stu-id="a06c2-880">For example, if your client application enables users to page through the entities stored in a table, a user may decide not to page through all the entities retrieved by the query so your application would only use a continuation token to retrieve the next segment when the user had finished paging through all the entities in the current segment.</span></span> <span data-ttu-id="a06c2-881">這種方法有幾項優點：</span><span class="sxs-lookup"><span data-stu-id="a06c2-881">This approach has several benefits:</span></span>  

* <span data-ttu-id="a06c2-882">它可讓您限制要從資料表服務擷取的資料量，以及在網路上移動的資料量。</span><span class="sxs-lookup"><span data-stu-id="a06c2-882">It enables you to limit the amount of data to retrieve from the Table service and that you move over the network.</span></span>  
* <span data-ttu-id="a06c2-883">它可讓您在 .NET 中執行非同步 IO。</span><span class="sxs-lookup"><span data-stu-id="a06c2-883">It enables you to perform asynchronous IO in .NET.</span></span>  
* <span data-ttu-id="a06c2-884">它可讓您序列化永續性儲存體的接續權杖，以便在應用程式當機時繼續作業。</span><span class="sxs-lookup"><span data-stu-id="a06c2-884">It enables you to serialize the continuation token to persistent storage so you can continue in the event of an application crash.</span></span>  

> [!NOTE]
> <span data-ttu-id="a06c2-885">接續權杖通常會傳回包含 1000 個實體的區段，但也可能較少。</span><span class="sxs-lookup"><span data-stu-id="a06c2-885">A continuation token typically returns a segment containing 1,000 entities, although it may be fewer.</span></span> <span data-ttu-id="a06c2-886">如果您使用 **Take** 傳回符合查閱準則的前 n 個實體，以限制查詢可傳回的實體數，也是如此：表格服務可能會傳回包含少於 n 個實體的區段以及接續權杖，讓您能夠擷取剩餘的實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-886">This is also the case if you limit the number of entries a query returns by using **Take** to return the first n entities that match your lookup criteria: the table service may return a segment containing fewer than n entities along with a continuation token to enable you to retrieve the remaining entities.</span></span>  
> 
> 

<span data-ttu-id="a06c2-887">下列 C# 程式碼說明如何修改區段內傳回的實體數目：</span><span class="sxs-lookup"><span data-stu-id="a06c2-887">The following C# code shows how to modify the number of entities returned inside a segment:</span></span>  

```csharp
employeeQuery.TakeCount = 50;  
```

#### <a name="server-side-projection"></a><span data-ttu-id="a06c2-888">伺服器端預測</span><span class="sxs-lookup"><span data-stu-id="a06c2-888">Server-side projection</span></span>
<span data-ttu-id="a06c2-889">單一實體最多可以有 255 個屬性，且大小上限為 1 MB。</span><span class="sxs-lookup"><span data-stu-id="a06c2-889">A single entity can have up to 255 properties and be up to 1 MB in size.</span></span> <span data-ttu-id="a06c2-890">當您查詢資料表並擷取實體時，您可能不需要所有屬性，並可以避免不必要地傳送資料 (以利降低延遲和成本)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-890">When you query the table and retrieve entities, you may not need all the properties and can avoid transferring data unnecessarily (to help reduce latency and cost).</span></span> <span data-ttu-id="a06c2-891">您可以使用伺服器端預測，僅傳送您需要的屬性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-891">You can use server-side projection to transfer just the properties you need.</span></span> <span data-ttu-id="a06c2-892">下列範例將只會從查詢選取的實體中擷取 **Email** 屬性 (連同 **PartitionKey**、**RowKey**、**Timestamp** 和 **ETag**)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-892">The following example is retrieves just the **Email** property (along with **PartitionKey**, **RowKey**, **Timestamp**, and **ETag**) from the entities selected by the query.</span></span>  

```csharp
string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
List<string> columns = new List<string>() { "Email" };
TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter).Select(columns);

var entities = employeeTable.ExecuteQuery(employeeQuery);
foreach (var e in entities)
{
        Console.WriteLine("RowKey: {0}, EmployeeEmail: {1}", e.RowKey, e.Email);
}  
```

<span data-ttu-id="a06c2-893">請注意， **RowKey** 值即使未包含在要擷取的屬性清單中，也可供使用。</span><span class="sxs-lookup"><span data-stu-id="a06c2-893">Notice how the **RowKey** value is available even though it was not included in the list of properties to retrieve.</span></span>  

### <a name="modifying-entities"></a><span data-ttu-id="a06c2-894">修改實體</span><span class="sxs-lookup"><span data-stu-id="a06c2-894">Modifying entities</span></span>
<span data-ttu-id="a06c2-895">儲存體用戶端程式庫可讓您藉由插入、刪除和更新實體，修改您儲存在資料表服務中的實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-895">The Storage Client Library enables you to modify your entities stored in the table service by inserting, deleting, and updating entities.</span></span> <span data-ttu-id="a06c2-896">您可以使用 EGT 一併批次處理多個插入、更新和刪除作業，以減少所需的往返次數，並改善方案的效能。</span><span class="sxs-lookup"><span data-stu-id="a06c2-896">You can use EGTs to batch multiple insert, update, and delete operations together to reduce the number of round trips required and improve the performance of your solution.</span></span>  

<span data-ttu-id="a06c2-897">請注意，當儲存體用戶端程式庫執行 EGT 時，通常預期會包含造成批次失敗的實體索引。</span><span class="sxs-lookup"><span data-stu-id="a06c2-897">Note that exceptions thrown when the Storage Client Library executes an EGT typically include the index of the entity that caused the batch to fail.</span></span> <span data-ttu-id="a06c2-898">當您偵錯使用 EGT 的程式碼時，這會很有幫助。</span><span class="sxs-lookup"><span data-stu-id="a06c2-898">This is helpful when you are debugging code that uses EGTs.</span></span>  

<span data-ttu-id="a06c2-899">您也應該考量您的設計會如何影響用戶端應用程式處理並行存取和更新作業的方式。</span><span class="sxs-lookup"><span data-stu-id="a06c2-899">You should also consider how your design affects how your client application handles concurrency and update operations.</span></span>  

#### <a name="managing-concurrency"></a><span data-ttu-id="a06c2-900">管理並行存取</span><span class="sxs-lookup"><span data-stu-id="a06c2-900">Managing concurrency</span></span>
<span data-ttu-id="a06c2-901">根據預設，表格服務會在個別實體的層級上，針對**插入**、**合併**和**刪除**作業實作開放式並行存取檢查，雖然用戶端也可以強制表格服務略過這些檢查。</span><span class="sxs-lookup"><span data-stu-id="a06c2-901">By default, the table service implements optimistic concurrency checks at the level of individual entities for **Insert**, **Merge**, and **Delete** operations, although it is possible for a client to force the table service to bypass these checks.</span></span> <span data-ttu-id="a06c2-902">如需表格服務如何管理並行存取的詳細資訊，請參閱[管理 Microsoft Azure 儲存體中的並行存取](storage-concurrency.md)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-902">For more information about how the table service manages concurrency, see  [Managing Concurrency in Microsoft Azure Storage](storage-concurrency.md).</span></span>  

#### <a name="merge-or-replace"></a><span data-ttu-id="a06c2-903">合併或取代</span><span class="sxs-lookup"><span data-stu-id="a06c2-903">Merge or replace</span></span>
<span data-ttu-id="a06c2-904">**TableOperation** 類別的 **Replace** 方法一律會取代表格服務中的完整實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-904">The **Replace** method of the **TableOperation** class always replaces the complete entity in the Table service.</span></span> <span data-ttu-id="a06c2-905">如果您未在要求中包含某個屬性，而該屬性存在於已儲存的實體中，要求將會從已儲存的實體中移除該屬性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-905">If you do not include a property in the request when that property exists in the stored entity, the request removes that property from the stored entity.</span></span> <span data-ttu-id="a06c2-906">除非您想要明確地從已儲存的實體中移除屬性，否則即必須在要求中包含每個屬性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-906">Unless you want to remove a property explicitly from a stored entity, you must include every property in the request.</span></span>  

<span data-ttu-id="a06c2-907">您可以使用 **TableOperation** 類別的 **Merge** 方法，減少您想要更新實體時傳送至表格服務的資料量。</span><span class="sxs-lookup"><span data-stu-id="a06c2-907">You can use the **Merge** method of the **TableOperation** class to reduce the amount of data that you send to the Table service when you want to update an entity.</span></span> <span data-ttu-id="a06c2-908">**Merge** 方法會將已儲存實體中的任何屬性取代為要求中包含之實體的屬性值，但對於未包含在要求中的已儲存實體，則會完整保留其所有的屬性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-908">The **Merge** method replaces any properties in the stored entity with property values from the entity included in the request, but leaves intact any properties in the stored entity that are not included in the request.</span></span> <span data-ttu-id="a06c2-909">如果您有大型實體，而只需要更新要求中的少數屬性，這就非常有用。</span><span class="sxs-lookup"><span data-stu-id="a06c2-909">This is useful if you have large entities and only need to update a small number of properties in a request.</span></span>  

> [!NOTE]
> <span data-ttu-id="a06c2-910">如果實體不存在，**Replace** 和 **Merge** 方法將會失敗。</span><span class="sxs-lookup"><span data-stu-id="a06c2-910">The **Replace** and **Merge** methods fail if the entity does not exist.</span></span> <span data-ttu-id="a06c2-911">如果實體不存在，您可以改用 **InsertOrReplace** 和 **InsertOrMerge** 方法建立新實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-911">As an alternative, you can use the **InsertOrReplace** and **InsertOrMerge** methods that create a new entity if it doesn't exist.</span></span>  
> 
> 

### <a name="working-with-heterogeneous-entity-types"></a><span data-ttu-id="a06c2-912">使用異質性實體類型</span><span class="sxs-lookup"><span data-stu-id="a06c2-912">Working with heterogeneous entity types</span></span>
<span data-ttu-id="a06c2-913">表格服務是 *無結構描述* 資料表存放區，這表示單一資料表可以儲存多種類型的實體，並在您的設計中提供絕佳的彈性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-913">The Table service is a *schema-less* table store that means that a single table can store entities of multiple types providing great flexibility in your design.</span></span> <span data-ttu-id="a06c2-914">下列範例說明用以儲存員工和部門實體的資料表：</span><span class="sxs-lookup"><span data-stu-id="a06c2-914">The following example illustrates a table storing both employee and department entities:</span></span>  

<table>
<tr>
<th><span data-ttu-id="a06c2-915">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="a06c2-915">PartitionKey</span></span></th>
<th><span data-ttu-id="a06c2-916">RowKey</span><span class="sxs-lookup"><span data-stu-id="a06c2-916">RowKey</span></span></th>
<th><span data-ttu-id="a06c2-917">Timestamp</span><span class="sxs-lookup"><span data-stu-id="a06c2-917">Timestamp</span></span></th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a06c2-918">名字</span><span class="sxs-lookup"><span data-stu-id="a06c2-918">FirstName</span></span></th>
<th><span data-ttu-id="a06c2-919">姓氏</span><span class="sxs-lookup"><span data-stu-id="a06c2-919">LastName</span></span></th>
<th><span data-ttu-id="a06c2-920">年齡</span><span class="sxs-lookup"><span data-stu-id="a06c2-920">Age</span></span></th>
<th><span data-ttu-id="a06c2-921">電子郵件</span><span class="sxs-lookup"><span data-stu-id="a06c2-921">Email</span></span></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a06c2-922">名字</span><span class="sxs-lookup"><span data-stu-id="a06c2-922">FirstName</span></span></th>
<th><span data-ttu-id="a06c2-923">姓氏</span><span class="sxs-lookup"><span data-stu-id="a06c2-923">LastName</span></span></th>
<th><span data-ttu-id="a06c2-924">年齡</span><span class="sxs-lookup"><span data-stu-id="a06c2-924">Age</span></span></th>
<th><span data-ttu-id="a06c2-925">電子郵件</span><span class="sxs-lookup"><span data-stu-id="a06c2-925">Email</span></span></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a06c2-926">DepartmentName</span><span class="sxs-lookup"><span data-stu-id="a06c2-926">DepartmentName</span></span></th>
<th><span data-ttu-id="a06c2-927">EmployeeCount</span><span class="sxs-lookup"><span data-stu-id="a06c2-927">EmployeeCount</span></span></th>
</tr>
<tr>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a06c2-928">名字</span><span class="sxs-lookup"><span data-stu-id="a06c2-928">FirstName</span></span></th>
<th><span data-ttu-id="a06c2-929">姓氏</span><span class="sxs-lookup"><span data-stu-id="a06c2-929">LastName</span></span></th>
<th><span data-ttu-id="a06c2-930">年齡</span><span class="sxs-lookup"><span data-stu-id="a06c2-930">Age</span></span></th>
<th><span data-ttu-id="a06c2-931">電子郵件</span><span class="sxs-lookup"><span data-stu-id="a06c2-931">Email</span></span></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

<span data-ttu-id="a06c2-932">請注意，每個實體仍必須要有 **PartitionKey**、**RowKey** 和 **Timestamp** 值，但是可以有任何屬性集。</span><span class="sxs-lookup"><span data-stu-id="a06c2-932">Note that each entity must still have **PartitionKey**, **RowKey**, and **Timestamp** values, but may have any set of properties.</span></span> <span data-ttu-id="a06c2-933">此外，除非您選擇將實體類型資訊儲存在某處，否則將沒有項目會指出此類型。</span><span class="sxs-lookup"><span data-stu-id="a06c2-933">Furthermore, there is nothing to indicate the type of an entity unless you choose to store that information somewhere.</span></span> <span data-ttu-id="a06c2-934">有兩個選項可用來識別實體類型：</span><span class="sxs-lookup"><span data-stu-id="a06c2-934">There are two options for identifying the entity type:</span></span>  

* <span data-ttu-id="a06c2-935">在 **RowKey** (或可能是 **PartitionKey**) 前面加上實體類型。</span><span class="sxs-lookup"><span data-stu-id="a06c2-935">Prepend the entity type to the **RowKey** (or possibly the **PartitionKey**).</span></span> <span data-ttu-id="a06c2-936">例如 **EMPLOYEE_000123**，或以 **DEPARTMENT_SALES** 做為 **RowKey** 值。</span><span class="sxs-lookup"><span data-stu-id="a06c2-936">For example, **EMPLOYEE_000123** or **DEPARTMENT_SALES** as **RowKey** values.</span></span>  
* <span data-ttu-id="a06c2-937">使用個別屬性記錄實體類型，如下表所示。</span><span class="sxs-lookup"><span data-stu-id="a06c2-937">Use a separate property to record the entity type as shown in the table below.</span></span>  

<table>
<tr>
<th><span data-ttu-id="a06c2-938">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="a06c2-938">PartitionKey</span></span></th>
<th><span data-ttu-id="a06c2-939">RowKey</span><span class="sxs-lookup"><span data-stu-id="a06c2-939">RowKey</span></span></th>
<th><span data-ttu-id="a06c2-940">Timestamp</span><span class="sxs-lookup"><span data-stu-id="a06c2-940">Timestamp</span></span></th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a06c2-941">EntityType</span><span class="sxs-lookup"><span data-stu-id="a06c2-941">EntityType</span></span></th>
<th><span data-ttu-id="a06c2-942">名字</span><span class="sxs-lookup"><span data-stu-id="a06c2-942">FirstName</span></span></th>
<th><span data-ttu-id="a06c2-943">姓氏</span><span class="sxs-lookup"><span data-stu-id="a06c2-943">LastName</span></span></th>
<th><span data-ttu-id="a06c2-944">年齡</span><span class="sxs-lookup"><span data-stu-id="a06c2-944">Age</span></span></th>
<th><span data-ttu-id="a06c2-945">電子郵件</span><span class="sxs-lookup"><span data-stu-id="a06c2-945">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="a06c2-946">員工</span><span class="sxs-lookup"><span data-stu-id="a06c2-946">Employee</span></span></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a06c2-947">EntityType</span><span class="sxs-lookup"><span data-stu-id="a06c2-947">EntityType</span></span></th>
<th><span data-ttu-id="a06c2-948">名字</span><span class="sxs-lookup"><span data-stu-id="a06c2-948">FirstName</span></span></th>
<th><span data-ttu-id="a06c2-949">姓氏</span><span class="sxs-lookup"><span data-stu-id="a06c2-949">LastName</span></span></th>
<th><span data-ttu-id="a06c2-950">年齡</span><span class="sxs-lookup"><span data-stu-id="a06c2-950">Age</span></span></th>
<th><span data-ttu-id="a06c2-951">電子郵件</span><span class="sxs-lookup"><span data-stu-id="a06c2-951">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="a06c2-952">員工</span><span class="sxs-lookup"><span data-stu-id="a06c2-952">Employee</span></span></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a06c2-953">EntityType</span><span class="sxs-lookup"><span data-stu-id="a06c2-953">EntityType</span></span></th>
<th><span data-ttu-id="a06c2-954">DepartmentName</span><span class="sxs-lookup"><span data-stu-id="a06c2-954">DepartmentName</span></span></th>
<th><span data-ttu-id="a06c2-955">EmployeeCount</span><span class="sxs-lookup"><span data-stu-id="a06c2-955">EmployeeCount</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="a06c2-956">department</span><span class="sxs-lookup"><span data-stu-id="a06c2-956">Department</span></span></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="a06c2-957">EntityType</span><span class="sxs-lookup"><span data-stu-id="a06c2-957">EntityType</span></span></th>
<th><span data-ttu-id="a06c2-958">名字</span><span class="sxs-lookup"><span data-stu-id="a06c2-958">FirstName</span></span></th>
<th><span data-ttu-id="a06c2-959">姓氏</span><span class="sxs-lookup"><span data-stu-id="a06c2-959">LastName</span></span></th>
<th><span data-ttu-id="a06c2-960">年齡</span><span class="sxs-lookup"><span data-stu-id="a06c2-960">Age</span></span></th>
<th><span data-ttu-id="a06c2-961">電子郵件</span><span class="sxs-lookup"><span data-stu-id="a06c2-961">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="a06c2-962">員工</span><span class="sxs-lookup"><span data-stu-id="a06c2-962">Employee</span></span></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

<span data-ttu-id="a06c2-963">如果兩個不同類型的實體可能有相同的索引鍵值，第一個選項 (在 **RowKey**前面加上實體類型) 可能會很有用。</span><span class="sxs-lookup"><span data-stu-id="a06c2-963">The first option, prepending the entity type to the **RowKey**, is useful if there is a possibility that two entities of different types might have the same key value.</span></span> <span data-ttu-id="a06c2-964">它也會將屬於相同類型的實體分組在資料分割中。</span><span class="sxs-lookup"><span data-stu-id="a06c2-964">It also groups entities of the same type together in the partition.</span></span>  

<span data-ttu-id="a06c2-965">本節討論的方法與本指南稍早的[模型化關聯性](#modelling-relationships)一節，對於[繼承關聯性](#inheritance-relationships)的討論有密切關聯。</span><span class="sxs-lookup"><span data-stu-id="a06c2-965">The techniques discussed in this section are especially relevant to the discussion [Inheritance relationships](#inheritance-relationships) earlier in this guide in the section [Modelling relationships](#modelling-relationships).</span></span>  

> [!NOTE]
> <span data-ttu-id="a06c2-966">您應考慮在實體類型值中包含版本號碼，讓用戶端應用程式能夠演化 POCO 物件，並與不同版本搭配使用。</span><span class="sxs-lookup"><span data-stu-id="a06c2-966">You should consider including a version number in the entity type value to enable client applications to evolve POCO objects and work with different versions.</span></span>  
> 
> 

<span data-ttu-id="a06c2-967">本節的其餘部分說明儲存體用戶端程式庫中一些有助於在相同資料表中使用多個實體類型的功能。</span><span class="sxs-lookup"><span data-stu-id="a06c2-967">The remainder of this section describes some of the features in the Storage Client Library that facilitate working with multiple entity types in the same table.</span></span>  

#### <a name="retrieving-heterogeneous-entity-types"></a><span data-ttu-id="a06c2-968">擷取異質性實體類型</span><span class="sxs-lookup"><span data-stu-id="a06c2-968">Retrieving heterogeneous entity types</span></span>
<span data-ttu-id="a06c2-969">在使用儲存體用戶端程式庫時，有三個選項可供您使用多個實體類型。</span><span class="sxs-lookup"><span data-stu-id="a06c2-969">If you are using the Storage Client Library, you have three options for working with multiple entity types.</span></span>  

<span data-ttu-id="a06c2-970">如果您知道以特定**RowKey** 和 **PartitionKey** 值儲存的實體類型，則在您擷取實體 (如先前兩個擷取實體類型 **EmployeeEntity** 的範例所說明) 時，將可指定實體類型：[使用儲存體用戶端程式庫執行點查詢](#executing-a-point-query-using-the-storage-client-library)和[使用 LINQ 擷取多個實體](#retrieving-multiple-entities-using-linq)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-970">If you know the type of the entity stored with a specific **RowKey** and **PartitionKey** values, then you can specify the entity type when you retrieve the entity as shown in the previous two examples that retrieve entities of type **EmployeeEntity**: [Executing a point query using the Storage Client Library](#executing-a-point-query-using-the-storage-client-library) and [Retrieving multiple entities using LINQ](#retrieving-multiple-entities-using-linq).</span></span>  

<span data-ttu-id="a06c2-971">第二個選項是使用 **DynamicTableEntity** 類型 (屬性包)，而不是具體的 POCO 實體類型 (這個選項也可改善效能，因為不需要將實體序列化和還原序列化成 .NET 類型)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-971">The second option is to use the **DynamicTableEntity** type (a property bag) instead of a concrete POCO entity type (this option may also improve performance because there is no need to serialize and deserialize the entity to .NET types).</span></span> <span data-ttu-id="a06c2-972">下列 C# 程式碼可能會從資料表中擷取多個不同類型的實體，但會傳回所有實體做為 **DynamicTableEntity** 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-972">The following C# code potentially retrieves multiple entities of different types from the table, but returns all entities as **DynamicTableEntity** instances.</span></span> <span data-ttu-id="a06c2-973">然後，它會使用 **EntityType** 屬性來判斷每個實體的類型：</span><span class="sxs-lookup"><span data-stu-id="a06c2-973">It then uses the **EntityType** property to determine the type of each entity:</span></span>  

```csharp
string filter = TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("PartitionKey",
    QueryComparisons.Equal, "Sales"),
    TableOperators.And,
    TableQuery.CombineFilters(
    TableQuery.GenerateFilterCondition("RowKey",
                    QueryComparisons.GreaterThanOrEqual, "B"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey",
        QueryComparisons.LessThan, "F")
    )
);
TableQuery<DynamicTableEntity> entityQuery =
    new TableQuery<DynamicTableEntity>().Where(filter);
var employees = employeeTable.ExecuteQuery(entityQuery);

IEnumerable<DynamicTableEntity> entities = employeeTable.ExecuteQuery(entityQuery);
foreach (var e in entities)
{
EntityProperty entityTypeProperty;
if (e.Properties.TryGetValue("EntityType", out entityTypeProperty))
{
    if (entityTypeProperty.StringValue == "Employee")
    {
        // Use entityTypeProperty, RowKey, PartitionKey, Etag, and Timestamp
        }
    }
}  
```

<span data-ttu-id="a06c2-974">請注意，您必須在 **DynamicTableEntity** 類別的 **Properties** 屬性上使用 **TryGetValue** 方法，才能擷取其他屬性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-974">Note that to retrieve other properties you must use the **TryGetValue** method on the **Properties** property of the **DynamicTableEntity** class.</span></span>  

<span data-ttu-id="a06c2-975">第三個選項是使用 **DynamicTableEntity** 類型和 **EntityResolver** 執行個體進行結合。</span><span class="sxs-lookup"><span data-stu-id="a06c2-975">A third option is to combine using the **DynamicTableEntity** type and an **EntityResolver** instance.</span></span> <span data-ttu-id="a06c2-976">這可讓您解析為相同查詢中的多個 POCO 類型。</span><span class="sxs-lookup"><span data-stu-id="a06c2-976">This enables you to resolve to multiple POCO types in the same query.</span></span> <span data-ttu-id="a06c2-977">在此範例中，**EntityResolver** 委派會使用 **EntityType** 屬性來區別查詢傳回的兩個實體類型。</span><span class="sxs-lookup"><span data-stu-id="a06c2-977">In this example, the **EntityResolver** delegate is using the **EntityType** property to distinguish between the two types of entity that the query returns.</span></span> <span data-ttu-id="a06c2-978">**Resolve** 方法會使用 **resolver** 委派，將 **DynamicTableEntity** 執行個體解析為 **TableEntity** 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-978">The **Resolve** method uses the **resolver** delegate to resolve **DynamicTableEntity** instances to **TableEntity** instances.</span></span>  

```csharp
EntityResolver<TableEntity> resolver = (pk, rk, ts, props, etag) =>
{

        TableEntity resolvedEntity = null;
        if (props["EntityType"].StringValue == "Department")
        {
        resolvedEntity = new DepartmentEntity();
        }
        else if (props["EntityType"].StringValue == "Employee")
        {
        resolvedEntity = new EmployeeEntity();
        }
        else throw new ArgumentException("Unrecognized entity", "props");

        resolvedEntity.PartitionKey = pk;
        resolvedEntity.RowKey = rk;
        resolvedEntity.Timestamp = ts;
        resolvedEntity.ETag = etag;
        resolvedEntity.ReadEntity(props, null);
        return resolvedEntity;
};

string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, "Sales");
TableQuery<DynamicTableEntity> entityQuery =
        new TableQuery<DynamicTableEntity>().Where(filter);

var entities = employeeTable.ExecuteQuery(entityQuery, resolver);
foreach (var e in entities)
{
        if (e is DepartmentEntity)
        {
    ...
        }
        if (e is EmployeeEntity)
        {
    ...
        }
}  
```

#### <a name="modifying-heterogeneous-entity-types"></a><span data-ttu-id="a06c2-979">修改異質性實體類型</span><span class="sxs-lookup"><span data-stu-id="a06c2-979">Modifying heterogeneous entity types</span></span>
<span data-ttu-id="a06c2-980">您不需要知道實體的類型即可加以刪除，而在您插入實體時一定會知道其類型。</span><span class="sxs-lookup"><span data-stu-id="a06c2-980">You do not need to know the type of an entity to delete it, and you always know the type of an entity when you insert it.</span></span> <span data-ttu-id="a06c2-981">不過，您可以使用 **DynamicTableEntity** 類型來更新實體，而不需要知道其類型，且無須使用 POCO 實體類別。</span><span class="sxs-lookup"><span data-stu-id="a06c2-981">However, you can use **DynamicTableEntity** type to update an entity without knowing its type and without using a POCO entity class.</span></span> <span data-ttu-id="a06c2-982">下列程式碼範例會擷取單一實體，並確認 **EmployeeCount** 屬性存在，然後加以更新。</span><span class="sxs-lookup"><span data-stu-id="a06c2-982">The following code sample retrieves a single entity, and checks the **EmployeeCount** property exists before updating it.</span></span>  

```csharp
TableResult result =
        employeeTable.Execute(TableOperation.Retrieve(partitionKey, rowKey));
DynamicTableEntity department = (DynamicTableEntity)result.Result;

EntityProperty countProperty;

if (!department.Properties.TryGetValue("EmployeeCount", out countProperty))
{
        throw new
        InvalidOperationException("Invalid entity, EmployeeCount property not found.");
}
countProperty.Int32Value += 1;
employeeTable.Execute(TableOperation.Merge(department));  
```

### <a name="controlling-access-with-shared-access-signatures"></a><span data-ttu-id="a06c2-983">使用共用存取簽章控制存取</span><span class="sxs-lookup"><span data-stu-id="a06c2-983">Controlling access with Shared Access Signatures</span></span>
<span data-ttu-id="a06c2-984">您可以使用共用存取簽章 (SAS) 權杖讓用戶端應用程式能夠修改 (和查詢) 資料表實體，而不需要直接使用資料表服務進行驗證。</span><span class="sxs-lookup"><span data-stu-id="a06c2-984">You can use Shared Access Signature (SAS) tokens to enable client applications to modify (and query) table entities directly without the need to authenticate directly with the table service.</span></span> <span data-ttu-id="a06c2-985">一般而言，在您的應用程式中使用 SAS 有三大優點：</span><span class="sxs-lookup"><span data-stu-id="a06c2-985">Typically, there are three main benefits to using SAS in your application:</span></span>  

* <span data-ttu-id="a06c2-986">您不需要為了要讓裝置可存取和修改資料表服務中的實體，而將儲存體帳戶金鑰散發至不安全的平台 (例如行動裝置)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-986">You do not need to distribute your storage account key to an insecure platform (such as a mobile device) in order to allow that device to access and modify entities in the Table service.</span></span>  
* <span data-ttu-id="a06c2-987">您可以將 Web 和背景工作角色為了管理實體而執行的某些工作，卸載至使用者電腦和行動裝置之類的用戶端裝置。</span><span class="sxs-lookup"><span data-stu-id="a06c2-987">You can offload some of the work that web and worker roles perform in managing your entities to client devices such as end-user computers and mobile devices.</span></span>  
* <span data-ttu-id="a06c2-988">您可以為用戶端指派受條件約束和時間限制的權限集 (例如允許對特定資源的唯讀存取)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-988">You can assign a constrained and time limited set of permissions to a client (such as allowing read-only access to specific resources).</span></span>  

<span data-ttu-id="a06c2-989">如需搭配使用 SAS 權杖與資料表服務的詳細資訊，請參閱 [使用共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md)。</span><span class="sxs-lookup"><span data-stu-id="a06c2-989">For more information about using SAS tokens with the Table service, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span></span>  

<span data-ttu-id="a06c2-990">不過，您仍必須產生SAS 權杖，讓用戶端應用程式有權使用資料表服務中的實體：您應在可安全存取儲存體帳戶金鑰的環境中執行這個動作。</span><span class="sxs-lookup"><span data-stu-id="a06c2-990">However, you must still generate the SAS tokens that grant a client application to the entities in the table service: you should do this in an environment that has secure access to your storage account keys.</span></span> <span data-ttu-id="a06c2-991">一般而言，您可以使用 Web 或背景工作角色來產生 SAS 權杖，並將其傳送至需要存取您的實體的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="a06c2-991">Typically, you use a web or worker role to generate the SAS tokens and deliver them to the client applications that need access to your entities.</span></span> <span data-ttu-id="a06c2-992">由於產生 SAS 權杖並將其傳遞至用戶端仍會產生額外負荷，因此您應考量怎樣最能降低此負荷，尤其是在大量的案例中。</span><span class="sxs-lookup"><span data-stu-id="a06c2-992">Because there is still an overhead involved in generating and delivering SAS tokens to clients, you should consider how best to reduce this overhead, especially in high-volume scenarios.</span></span>  

<span data-ttu-id="a06c2-993">您可以產生特定 SAS 權杖，使其授與對資料表中的實體子集進行存取的權限。</span><span class="sxs-lookup"><span data-stu-id="a06c2-993">It is possible to generate a SAS token that grants access to a subset of the entities in a table.</span></span> <span data-ttu-id="a06c2-994">根據預設，您會建立適用於整個資料表的 SAS 權杖，但也可以指定 SAS 權杖僅授與存取特定範圍的 **PartitionKey** 值或特定範圍的 **PartitionKey** 和 **RowKey** 值的權限。</span><span class="sxs-lookup"><span data-stu-id="a06c2-994">By default, you create a SAS token for an entire table, but it is also possible to specify that the SAS token grant access to either a range of **PartitionKey** values, or a range of **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="a06c2-995">您可以選擇為系統的個別使用者產生 SAS 權杖，使每位使用者的 SAS 權杖只允許他們在資料表服務中存取自己的實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-995">You might choose to generate SAS tokens for individual users of your system such that each user's SAS token only allows them access to their own entities in the table service.</span></span>  

### <a name="asynchronous-and-parallel-operations"></a><span data-ttu-id="a06c2-996">非同步和平行作業</span><span class="sxs-lookup"><span data-stu-id="a06c2-996">Asynchronous and parallel operations</span></span>
<span data-ttu-id="a06c2-997">假設您要跨多個資料分割分散您的要求，您可以使用非同步或平行查詢來改善輸送量和用戶端的回應性。</span><span class="sxs-lookup"><span data-stu-id="a06c2-997">Provided you are spreading your requests across multiple partitions, you can improve throughput and client responsiveness by using asynchronous or parallel queries.</span></span>
<span data-ttu-id="a06c2-998">例如，您可以用兩個或更多背景工作角色執行個體，以平行方式存取您的資料表。</span><span class="sxs-lookup"><span data-stu-id="a06c2-998">For example, you might have two or more worker role instances accessing your tables in parallel.</span></span> <span data-ttu-id="a06c2-999">您可以讓個別的背景工作角色負責特定的資料分割集，或僅使用多個背景工作角色執行個體，使其分別都能夠存取資料表中的所有資料分割。</span><span class="sxs-lookup"><span data-stu-id="a06c2-999">You could have individual worker roles responsible for particular sets of partitions, or simply have multiple worker role instances, each able to access all the partitions in a table.</span></span>  

<span data-ttu-id="a06c2-1000">在用戶端執行個體中，您可以藉由以非同步方式執行儲存作業來提高輸送量。</span><span class="sxs-lookup"><span data-stu-id="a06c2-1000">Within a client instance, you can improve throughput by executing storage operations asynchronously.</span></span> <span data-ttu-id="a06c2-1001">儲存體用戶端程式庫可讓您輕鬆撰寫非同步查詢並修改。</span><span class="sxs-lookup"><span data-stu-id="a06c2-1001">The Storage Client Library makes it easy to write asynchronous queries and modifications.</span></span> <span data-ttu-id="a06c2-1002">比方說，首先您可以使用同步方法來擷取資料分割中的所有實體，如下列 C# 程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="a06c2-1002">For example, you might start with the synchronous method that retrieves all the entities in a partition as shown in the following C# code:</span></span>  

```csharp
private static void ManyEntitiesQuery(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);

        TableContinuationToken continuationToken = null;

        do
        {
        var employees = employeeTable.ExecuteQuerySegmented(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
    {
        ...
    }
        continuationToken = employees.ContinuationToken;
        } while (continuationToken != null);
}  
```

<span data-ttu-id="a06c2-1003">您可以輕鬆地修改此程式碼，讓查詢以非同步方式執行，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a06c2-1003">You can easily modify this code so that the query runs asynchronously as follows:</span></span>  

```csharp
private static async Task ManyEntitiesQueryAsync(CloudTable employeeTable, string department)
{
        string filter = TableQuery.GenerateFilterCondition(
        "PartitionKey", QueryComparisons.Equal, department);
        TableQuery<EmployeeEntity> employeeQuery =
        new TableQuery<EmployeeEntity>().Where(filter);
        TableContinuationToken continuationToken = null;

        do
        {
        var employees = await employeeTable.ExecuteQuerySegmentedAsync(
                employeeQuery, continuationToken);
        foreach (var emp in employees)
        {
            ...
        }
        continuationToken = employees.ContinuationToken;
            } while (continuationToken != null);
}  
```

<span data-ttu-id="a06c2-1004">在此非同步範例中，您可以看到下列與同步版本不同的變更：</span><span class="sxs-lookup"><span data-stu-id="a06c2-1004">In this asynchronous example, you can see the following changes from the synchronous version:</span></span>  

* <span data-ttu-id="a06c2-1005">方法簽章現在包含 **async** 修飾詞，並且會傳回 **Task** 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-1005">The method signature now includes the **async** modifier and returns a **Task** instance.</span></span>  
* <span data-ttu-id="a06c2-1006">現在方法會呼叫 **ExecuteSegmentedAsync** 方法，並使用 **await** 修飾詞以非同步方式擷取結果，而不會呼叫 **ExecuteSegmented** 方法來擷取結果。</span><span class="sxs-lookup"><span data-stu-id="a06c2-1006">Instead of calling the **ExecuteSegmented** method to retrieve results, the method now calls the **ExecuteSegmentedAsync** method and uses the **await** modifier to retrieve results asynchronously.</span></span>  

<span data-ttu-id="a06c2-1007">用戶端應用程式可以呼叫此方法多次 (使用不同的 **department** 參數值)，且每個查詢將會在個別的執行緒上執行。</span><span class="sxs-lookup"><span data-stu-id="a06c2-1007">The client application can call this method multiple times (with different values for the **department** parameter), and each query will run on a separate thread.</span></span>  

<span data-ttu-id="a06c2-1008">請注意，**TableQuery** 類別中的 **Execute** 方法並沒有非同步版本，因為 **IEnumerable** 介面不支援非同步列舉。</span><span class="sxs-lookup"><span data-stu-id="a06c2-1008">Note that there is no asynchronous version of the **Execute** method in the **TableQuery** class because the **IEnumerable** interface does not support asynchronous enumeration.</span></span>  

<span data-ttu-id="a06c2-1009">您也可以透過非同步方式插入、更新和刪除實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-1009">You can also insert, update, and delete entities asynchronously.</span></span> <span data-ttu-id="a06c2-1010">下列 C# 範例說明如何以簡單的同步方法來插入或取代員工實體：</span><span class="sxs-lookup"><span data-stu-id="a06c2-1010">The following C# example shows a simple, synchronous method to insert or replace an employee entity:</span></span>  

```csharp
private static void SimpleEmployeeUpsert(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = employeeTable
        .Execute(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

<span data-ttu-id="a06c2-1011">您可以輕鬆地修改此程式碼，讓更新以非同步方式執行，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a06c2-1011">You can easily modify this code so that the update runs asynchronously as follows:</span></span>  

```csharp
private static async Task SimpleEmployeeUpsertAsync(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = await employeeTable
        .ExecuteAsync(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

<span data-ttu-id="a06c2-1012">在此非同步範例中，您可以看到下列與同步版本不同的變更：</span><span class="sxs-lookup"><span data-stu-id="a06c2-1012">In this asynchronous example, you can see the following changes from the synchronous version:</span></span>  

* <span data-ttu-id="a06c2-1013">方法簽章現在包含 **async** 修飾詞，並且會傳回 **Task** 執行個體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-1013">The method signature now includes the **async** modifier and returns a **Task** instance.</span></span>  
* <span data-ttu-id="a06c2-1014">現在方法會呼叫 **ExecuteAsync** 方法，並使用 **await** 修飾詞以非同步方式擷取結果，而不會呼叫 **Execute** 方法來更新實體。</span><span class="sxs-lookup"><span data-stu-id="a06c2-1014">Instead of calling the **Execute** method to update the entity, the method now calls the **ExecuteAsync** method and uses the **await** modifier to retrieve results asynchronously.</span></span>  

<span data-ttu-id="a06c2-1015">用戶端應用程式可以呼叫多個此類的非同步方法，每個方法叫用會在個別的執行緒上執行。</span><span class="sxs-lookup"><span data-stu-id="a06c2-1015">The client application can call multiple asynchronous methods like this one, and each method invocation will run on a separate thread.</span></span>  

### <a name="credits"></a><span data-ttu-id="a06c2-1016">學分</span><span class="sxs-lookup"><span data-stu-id="a06c2-1016">Credits</span></span>
<span data-ttu-id="a06c2-1017">我們要感謝下列 Azure 團隊成員所做的貢獻：Dominic Betts、Jason Hogg、Jean Ghanem、Jai Haridas、Jeff Irwin、Vamshidhar Kommineni、Vinay Shah 和 Serdar Ozler，以及來自 Microsoft DX 的 Tom Hollander。</span><span class="sxs-lookup"><span data-stu-id="a06c2-1017">We would like to thank the following members of the Azure team for their contributions: Dominic Betts, Jason Hogg, Jean Ghanem, Jai Haridas, Jeff Irwin, Vamshidhar Kommineni, Vinay Shah and Serdar Ozler as well as  Tom Hollander from Microsoft DX.</span></span> 

<span data-ttu-id="a06c2-1018">我們也要感謝下列 Microsoft MVP 在審閱期間提供了寶貴意見：Igor Papirov 和 Edward Bakker。</span><span class="sxs-lookup"><span data-stu-id="a06c2-1018">We would also like to thank the following Microsoft MVP's for their valuable feedback during review cycles: Igor Papirov and Edward Bakker.</span></span>

[1]: ./media/storage-table-design-guide/storage-table-design-IMAGE01.png
[2]: ./media/storage-table-design-guide/storage-table-design-IMAGE02.png
[3]: ./media/storage-table-design-guide/storage-table-design-IMAGE03.png
[4]: ./media/storage-table-design-guide/storage-table-design-IMAGE04.png
[5]: ./media/storage-table-design-guide/storage-table-design-IMAGE05.png
[6]: ./media/storage-table-design-guide/storage-table-design-IMAGE06.png
[7]: ./media/storage-table-design-guide/storage-table-design-IMAGE07.png
[8]: ./media/storage-table-design-guide/storage-table-design-IMAGE08.png
[9]: ./media/storage-table-design-guide/storage-table-design-IMAGE09.png
[10]: ./media/storage-table-design-guide/storage-table-design-IMAGE10.png
[11]: ./media/storage-table-design-guide/storage-table-design-IMAGE11.png
[12]: ./media/storage-table-design-guide/storage-table-design-IMAGE12.png
[13]: ./media/storage-table-design-guide/storage-table-design-IMAGE13.png
[14]: ./media/storage-table-design-guide/storage-table-design-IMAGE14.png
[15]: ./media/storage-table-design-guide/storage-table-design-IMAGE15.png
[16]: ./media/storage-table-design-guide/storage-table-design-IMAGE16.png
[17]: ./media/storage-table-design-guide/storage-table-design-IMAGE17.png
[18]: ./media/storage-table-design-guide/storage-table-design-IMAGE18.png
[19]: ./media/storage-table-design-guide/storage-table-design-IMAGE19.png
[20]: ./media/storage-table-design-guide/storage-table-design-IMAGE20.png
[21]: ./media/storage-table-design-guide/storage-table-design-IMAGE21.png
[22]: ./media/storage-table-design-guide/storage-table-design-IMAGE22.png
[23]: ./media/storage-table-design-guide/storage-table-design-IMAGE23.png
[24]: ./media/storage-table-design-guide/storage-table-design-IMAGE24.png
[25]: ./media/storage-table-design-guide/storage-table-design-IMAGE25.png
[26]: ./media/storage-table-design-guide/storage-table-design-IMAGE26.png
[27]: ./media/storage-table-design-guide/storage-table-design-IMAGE27.png
[28]: ./media/storage-table-design-guide/storage-table-design-IMAGE28.png
[29]: ./media/storage-table-design-guide/storage-table-design-IMAGE29.png

