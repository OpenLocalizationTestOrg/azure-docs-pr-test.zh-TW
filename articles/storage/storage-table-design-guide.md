---
title: "儲存體資料表設計指南 aaaAzure |Microsoft 文件"
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
ms.openlocfilehash: bbac5e83fe994c1ba1408dd43367fbcfca6a2148
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-table-design-guide-designing-scalable-and-performant-tables"></a><span data-ttu-id="15f93-103">Azure 儲存體資料表設計指南：設計可調整且效用佳的資料表</span><span class="sxs-lookup"><span data-stu-id="15f93-103">Azure Storage Table Design Guide: Designing Scalable and Performant Tables</span></span>
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="15f93-104">toodesign 可擴充和高效能的資料表，您必須考慮許多因素，例如效能、 延展性和成本。</span><span class="sxs-lookup"><span data-stu-id="15f93-104">toodesign scalable and performant tables you must consider a number of factors such as performance, scalability, and cost.</span></span> <span data-ttu-id="15f93-105">如果您先前所設計的關聯式資料庫結構描述，這些考量會熟悉 tooyou，但有一些 hello Azure 表格服務的儲存體模型和關聯式模型之間的相似之處，另外還有許多重要差異。</span><span class="sxs-lookup"><span data-stu-id="15f93-105">If you have previously designed schemas for relational databases, these considerations will be familiar tooyou, but while there are some similarities between hello Azure Table service storage model and relational models, there are also many important differences.</span></span> <span data-ttu-id="15f93-106">這些差異通常會導致 toovery 不同的設計，看起來可能違反直覺或錯誤 toosomeone 熟悉關聯式資料庫，但其執行進行不錯的方法，如果您要設計的 NoSQL 索引鍵/值存放區，例如 hello Azure 表格服務。</span><span class="sxs-lookup"><span data-stu-id="15f93-106">These differences typically lead toovery different designs that may look counter-intuitive or wrong toosomeone familiar with relational databases, but which do make good sense if you are designing for a NoSQL key/value store such as hello Azure Table service.</span></span> <span data-ttu-id="15f93-107">許多設計差異將會反映 hello 事實 hello 表格服務是設計的 toosupport 雲端規模應用程式可以包含數十億個實體 （在關聯式資料庫詞彙中的資料列） 的資料，或是必須支援極高的資料集交易量： 因此，您需要以不同的方式，需將資料的儲存 toothink 及了解 hello 表格服務的運作方式。</span><span class="sxs-lookup"><span data-stu-id="15f93-107">Many of your design differences will reflect hello fact that hello Table service is designed toosupport cloud-scale applications that can contain billions of entities (rows in relational database terminology) of data or for datasets that must support very high transaction volumes: therefore, you need toothink differently about how you store your data and understand how hello Table service works.</span></span> <span data-ttu-id="15f93-108">更進一步 （和較低的成本），設計良好的 NoSQL 資料存放區可以啟用方案 tooscale 比使用關聯式資料庫的解決方案。</span><span class="sxs-lookup"><span data-stu-id="15f93-108">A well designed NoSQL data store can enable your solution tooscale much further (and at a lower cost) than a solution that uses a relational database.</span></span> <span data-ttu-id="15f93-109">本指南針對這些主題為您提供協助。</span><span class="sxs-lookup"><span data-stu-id="15f93-109">This guide helps you with these topics.</span></span>  

## <a name="about-hello-azure-table-service"></a><span data-ttu-id="15f93-110">關於 hello Azure 資料表服務</span><span class="sxs-lookup"><span data-stu-id="15f93-110">About hello Azure Table service</span></span>
<span data-ttu-id="15f93-111">本章節強調一些 hello 關鍵功能 hello 表格服務會特別相關 toodesigning 的效能和延展性。</span><span class="sxs-lookup"><span data-stu-id="15f93-111">This section highlights some of hello key features of hello Table service that are especially relevant toodesigning for performance and scalability.</span></span> <span data-ttu-id="15f93-112">如果您是新 tooAzure 儲存體和 hello 表格服務，先閱讀[簡介 tooMicrosoft Azure 儲存體](storage-introduction.md)和[開始使用適用於.NET 的 Azure 資料表儲存體使用](storage-dotnet-how-to-use-tables.md)再讀取這個 hello 餘數發行項。</span><span class="sxs-lookup"><span data-stu-id="15f93-112">If you are new tooAzure Storage and hello Table service, first read [Introduction tooMicrosoft Azure Storage](storage-introduction.md) and [Get started with Azure Table Storage using .NET](storage-dotnet-how-to-use-tables.md) before reading hello remainder of this article.</span></span> <span data-ttu-id="15f93-113">雖然本指南的 hello 焦點是 hello 表格服務，它會包含一些 hello Azure 佇列和 Blob 服務，以及您如何使用這些以及 hello 方案中的表格服務的討論。</span><span class="sxs-lookup"><span data-stu-id="15f93-113">Although hello focus of this guide is on hello Table service, it will include some discussion of hello Azure Queue and Blob services, and how you might use them along with hello Table service in a solution.</span></span>  

<span data-ttu-id="15f93-114">什麼是 hello 表格服務？</span><span class="sxs-lookup"><span data-stu-id="15f93-114">What is hello Table service?</span></span> <span data-ttu-id="15f93-115">如您預期從 hello 名稱，hello 表格服務會使用表格式格式 toostore 資料。</span><span class="sxs-lookup"><span data-stu-id="15f93-115">As you might expect from hello name, hello Table service uses a tabular format toostore data.</span></span> <span data-ttu-id="15f93-116">在 hello 標準術語，hello 資料表的每個資料列代表實體，而 hello 資料行存放區 hello 該實體的各種屬性。</span><span class="sxs-lookup"><span data-stu-id="15f93-116">In hello standard terminology, each row of hello table represents an entity, and hello columns store hello various properties of that entity.</span></span> <span data-ttu-id="15f93-117">每個實體有一組索引鍵 toouniquely 識別它，並用 hello 表格服務的時間戳記資料行 tootrack hello 實體上次更新時 （這會自動與您無法以手動方式覆寫 hello 時間戳記任意值）。</span><span class="sxs-lookup"><span data-stu-id="15f93-117">Every entity has a pair of keys toouniquely identify it, and a timestamp column that hello Table service uses tootrack when hello entity was last updated (this happens automatically and you cannot manually overwrite hello timestamp with an arbitrary value).</span></span> <span data-ttu-id="15f93-118">hello 表格服務會使用這個上次修改時間戳記 (LMT) toomanage 開放式並行存取。</span><span class="sxs-lookup"><span data-stu-id="15f93-118">hello Table service uses this last-modified timestamp (LMT) toomanage optimistic concurrency.</span></span>  

> [!NOTE]
> <span data-ttu-id="15f93-119">hello 表格服務 REST API 作業還會傳回**ETag** hello 上次修改時間戳記 (LMT) 從它衍生的值。</span><span class="sxs-lookup"><span data-stu-id="15f93-119">hello Table service REST API operations also return an **ETag** value that it derives from hello last-modified timestamp (LMT).</span></span> <span data-ttu-id="15f93-120">我們將使用這份文件中 hello 條款 ETag 和 LMT 交換因為兩者參考 toohello 相同基礎資料。</span><span class="sxs-lookup"><span data-stu-id="15f93-120">In this document we will use hello terms ETag and LMT interchangeably because they refer toohello same underlying data.</span></span>  
> 
> 

<span data-ttu-id="15f93-121">hello 下列範例顯示簡單的資料表設計 toostore employee 和 department 實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-121">hello following example shows a simple table design toostore employee and department entities.</span></span> <span data-ttu-id="15f93-122">許多 hello 範例所示稍後在本指南根據這個簡單的設計。</span><span class="sxs-lookup"><span data-stu-id="15f93-122">Many of hello examples shown later in this guide are based on this simple design.</span></span>  

<table>
<tr>
<th><span data-ttu-id="15f93-123">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="15f93-123">PartitionKey</span></span></th>
<th><span data-ttu-id="15f93-124">RowKey</span><span class="sxs-lookup"><span data-stu-id="15f93-124">RowKey</span></span></th>
<th><span data-ttu-id="15f93-125">Timestamp</span><span class="sxs-lookup"><span data-stu-id="15f93-125">Timestamp</span></span></th>
<th></th>
</tr>
<tr>
<td><span data-ttu-id="15f93-126">行銷</span><span class="sxs-lookup"><span data-stu-id="15f93-126">Marketing</span></span></td>
<td><span data-ttu-id="15f93-127">00001</span><span class="sxs-lookup"><span data-stu-id="15f93-127">00001</span></span></td>
<td><span data-ttu-id="15f93-128">2014-08-22T00:50:32Z</span><span class="sxs-lookup"><span data-stu-id="15f93-128">2014-08-22T00:50:32Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="15f93-129">FirstName</span><span class="sxs-lookup"><span data-stu-id="15f93-129">FirstName</span></span></th>
<th><span data-ttu-id="15f93-130">姓氏</span><span class="sxs-lookup"><span data-stu-id="15f93-130">LastName</span></span></th>
<th><span data-ttu-id="15f93-131">年齡</span><span class="sxs-lookup"><span data-stu-id="15f93-131">Age</span></span></th>
<th><span data-ttu-id="15f93-132">電子郵件</span><span class="sxs-lookup"><span data-stu-id="15f93-132">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="15f93-133">Don</span><span class="sxs-lookup"><span data-stu-id="15f93-133">Don</span></span></td>
<td><span data-ttu-id="15f93-134">Hall</span><span class="sxs-lookup"><span data-stu-id="15f93-134">Hall</span></span></td>
<td><span data-ttu-id="15f93-135">34</span><span class="sxs-lookup"><span data-stu-id="15f93-135">34</span></span></td>
<td>donh@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td><span data-ttu-id="15f93-136">行銷</span><span class="sxs-lookup"><span data-stu-id="15f93-136">Marketing</span></span></td>
<td><span data-ttu-id="15f93-137">00002</span><span class="sxs-lookup"><span data-stu-id="15f93-137">00002</span></span></td>
<td><span data-ttu-id="15f93-138">2014-08-22T00:50:34Z</span><span class="sxs-lookup"><span data-stu-id="15f93-138">2014-08-22T00:50:34Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="15f93-139">FirstName</span><span class="sxs-lookup"><span data-stu-id="15f93-139">FirstName</span></span></th>
<th><span data-ttu-id="15f93-140">姓氏</span><span class="sxs-lookup"><span data-stu-id="15f93-140">LastName</span></span></th>
<th><span data-ttu-id="15f93-141">年齡</span><span class="sxs-lookup"><span data-stu-id="15f93-141">Age</span></span></th>
<th><span data-ttu-id="15f93-142">電子郵件</span><span class="sxs-lookup"><span data-stu-id="15f93-142">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="15f93-143">Jun</span><span class="sxs-lookup"><span data-stu-id="15f93-143">Jun</span></span></td>
<td><span data-ttu-id="15f93-144">Cao</span><span class="sxs-lookup"><span data-stu-id="15f93-144">Cao</span></span></td>
<td><span data-ttu-id="15f93-145">47</span><span class="sxs-lookup"><span data-stu-id="15f93-145">47</span></span></td>
<td>junc@contoso.com</td>
</tr>
</table>
</tr>
<tr>
<td><span data-ttu-id="15f93-146">行銷</span><span class="sxs-lookup"><span data-stu-id="15f93-146">Marketing</span></span></td>
<td><span data-ttu-id="15f93-147">系所</span><span class="sxs-lookup"><span data-stu-id="15f93-147">Department</span></span></td>
<td><span data-ttu-id="15f93-148">2014-08-22T00:50:30Z</span><span class="sxs-lookup"><span data-stu-id="15f93-148">2014-08-22T00:50:30Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="15f93-149">DepartmentName</span><span class="sxs-lookup"><span data-stu-id="15f93-149">DepartmentName</span></span></th>
<th><span data-ttu-id="15f93-150">EmployeeCount</span><span class="sxs-lookup"><span data-stu-id="15f93-150">EmployeeCount</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="15f93-151">行銷</span><span class="sxs-lookup"><span data-stu-id="15f93-151">Marketing</span></span></td>
<td><span data-ttu-id="15f93-152">153</span><span class="sxs-lookup"><span data-stu-id="15f93-152">153</span></span></td>
</tr>
</table>
</td>
</tr>
<tr>
<td><span data-ttu-id="15f93-153">銷售</span><span class="sxs-lookup"><span data-stu-id="15f93-153">Sales</span></span></td>
<td><span data-ttu-id="15f93-154">00010</span><span class="sxs-lookup"><span data-stu-id="15f93-154">00010</span></span></td>
<td><span data-ttu-id="15f93-155">2014-08-22T00:50:44Z</span><span class="sxs-lookup"><span data-stu-id="15f93-155">2014-08-22T00:50:44Z</span></span></td>
<td>
<table>
<tr>
<th><span data-ttu-id="15f93-156">FirstName</span><span class="sxs-lookup"><span data-stu-id="15f93-156">FirstName</span></span></th>
<th><span data-ttu-id="15f93-157">姓氏</span><span class="sxs-lookup"><span data-stu-id="15f93-157">LastName</span></span></th>
<th><span data-ttu-id="15f93-158">年齡</span><span class="sxs-lookup"><span data-stu-id="15f93-158">Age</span></span></th>
<th><span data-ttu-id="15f93-159">電子郵件</span><span class="sxs-lookup"><span data-stu-id="15f93-159">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="15f93-160">Ken</span><span class="sxs-lookup"><span data-stu-id="15f93-160">Ken</span></span></td>
<td><span data-ttu-id="15f93-161">Kwok</span><span class="sxs-lookup"><span data-stu-id="15f93-161">Kwok</span></span></td>
<td><span data-ttu-id="15f93-162">23</span><span class="sxs-lookup"><span data-stu-id="15f93-162">23</span></span></td>
<td>kenk@contoso.com</td>
</tr>
</table>
</td>
</tr>
</table>


<span data-ttu-id="15f93-163">目前為止，這會非常類似 tooa 資料表關聯式資料庫中尋找具有 hello 正在 hello 強制的資料行的主要差異和 hello 能力 toostore 多個實體中的型別 hello 相同的資料表。</span><span class="sxs-lookup"><span data-stu-id="15f93-163">So far, this looks very similar tooa table in a relational database with hello key differences being hello mandatory columns, and hello ability toostore multiple entity types in hello same table.</span></span> <span data-ttu-id="15f93-164">此外，每個這類 hello 使用者定義的屬性**FirstName**或**年齡**具有資料類型，例如整數或字串，就像關聯式資料庫中的資料行。</span><span class="sxs-lookup"><span data-stu-id="15f93-164">In addition, each of hello user-defined properties such as **FirstName** or **Age** has a data type, such as integer or string, just like a column in a relational database.</span></span> <span data-ttu-id="15f93-165">雖然不同於在關聯式資料庫中，屬性不需要的資料表服務表示 hello hello 無結構描述性質 hello 相同資料型別上的每個實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-165">Although unlike in a relational database, hello schema-less nature of hello Table service means that a property need not have hello same data type on each entity.</span></span> <span data-ttu-id="15f93-166">toostore 複雜資料型別，在單一屬性中的，您必須使用序列化的格式，例如 JSON 或 XML。</span><span class="sxs-lookup"><span data-stu-id="15f93-166">toostore complex data types in a single property, you must use a serialized format such as JSON or XML.</span></span> <span data-ttu-id="15f93-167">如需 hello 資料表服務，例如支援資料類型、 支援的日期範圍、 命名規則和大小限制的詳細資訊，請參閱[了解 hello 表格服務資料模型](http://msdn.microsoft.com/library/azure/dd179338.aspx)。</span><span class="sxs-lookup"><span data-stu-id="15f93-167">For more information about hello table service such as supported data types, supported date ranges, naming rules, and size constraints, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="15f93-168">如您所見，您所選擇的**PartitionKey**和**RowKey**是基本 toogood 資料表設計。</span><span class="sxs-lookup"><span data-stu-id="15f93-168">As you will see, your choice of **PartitionKey** and **RowKey** is fundamental toogood table design.</span></span> <span data-ttu-id="15f93-169">儲存在資料表中的每個實體都必須有一個獨一無二的 **PartitionKey** 和 **RowKey** 組合。</span><span class="sxs-lookup"><span data-stu-id="15f93-169">Every entity stored in a table must have a unique combination of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="15f93-170">如同關聯式資料庫資料表中的索引鍵，hello **PartitionKey**和**RowKey**的值是索引的 toocreate，可讓快速查閱叢集索引，不過，hello 表格服務不會建立任何次要索引，使這些都是 hello 只有兩個索引的屬性 （稍後說明的 hello 模式的某些顯示您可以解決此明顯的限制）。</span><span class="sxs-lookup"><span data-stu-id="15f93-170">As with keys in a relational database table, hello **PartitionKey** and **RowKey** values are indexed toocreate a clustered index that enables fast look-ups; however, hello Table service does not create any secondary indexes so these are hello only two indexed properties (some of hello patterns described later show how you can work around this apparent limitation).</span></span>  

<span data-ttu-id="15f93-171">資料表由一或多個資料分割所組成，如您所見，hello 的許多設計的決策，您就會選擇適合周圍**PartitionKey**和**RowKey** toooptimize 您的方案。</span><span class="sxs-lookup"><span data-stu-id="15f93-171">A table is made up of one or more partitions, and as you will see, many of hello design decisions you make will be around choosing a suitable **PartitionKey** and **RowKey** toooptimize your solution.</span></span> <span data-ttu-id="15f93-172">方案可以僅由單一資料表組成 (其中組織成資料分割的所有實體)，但方案通常會有多個資料表。</span><span class="sxs-lookup"><span data-stu-id="15f93-172">A solution could consist of just a single table that contains all your entities organized into partitions, but typically a solution will have multiple tables.</span></span> <span data-ttu-id="15f93-173">資料表可幫助您 toologically 組織您的實體，協助您管理存取權 toohello 資料來使用存取控制清單，您可以卸除整個資料表，使用單一儲存體作業。</span><span class="sxs-lookup"><span data-stu-id="15f93-173">Tables help you toologically organize your entities, help you manage access toohello data using access control lists, and you can drop an entire table using a single storage operation.</span></span>  

### <a name="table-partitions"></a><span data-ttu-id="15f93-174">資料表的資料分割</span><span class="sxs-lookup"><span data-stu-id="15f93-174">Table partitions</span></span>
<span data-ttu-id="15f93-175">hello 帳戶名稱、 資料表名稱和**PartitionKey**一起找出 hello hello hello 表格服務儲存 hello 實體的儲存體服務中的資料分割。</span><span class="sxs-lookup"><span data-stu-id="15f93-175">hello account name, table name and **PartitionKey** together identify hello partition within hello storage service where hello table service stores hello entity.</span></span> <span data-ttu-id="15f93-176">正在 hello 定址配置之實體的一部分，以及資料分割定義交易的範圍 (請參閱[實體群組交易](#entity-group-transactions)下方)，以及表單的 hello 表格服務的可調整的 hello 基準。</span><span class="sxs-lookup"><span data-stu-id="15f93-176">As well as being part of hello addressing scheme for entities, partitions define a scope for transactions (see [Entity Group Transactions](#entity-group-transactions) below), and form hello basis of how hello table service scales.</span></span> <span data-ttu-id="15f93-177">如需分割的詳細資訊，請參閱 [Azure 儲存體延展性和效能目標](storage-scalability-targets.md)。</span><span class="sxs-lookup"><span data-stu-id="15f93-177">For more information on partitions see [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span>  

<span data-ttu-id="15f93-178">Hello 表格服務，在個別節點服務一個或多個完成資料分割並且 hello 服務標尺的動態負載平衡節點間的資料分割。</span><span class="sxs-lookup"><span data-stu-id="15f93-178">In hello Table service, an individual node services one or more complete partitions and hello service scales by dynamically load-balancing partitions across nodes.</span></span> <span data-ttu-id="15f93-179">如果節點是在負載之下，hello 表格服務可以*分割*到不同節點上的該節點所服務的 hello 範圍的資料分割; 當流量 subsides，hello 服務可以*合併*hello 資料分割的範圍是從無訊息的節點備份到單一節點上。</span><span class="sxs-lookup"><span data-stu-id="15f93-179">If a node is under load, hello table service can *split* hello range of partitions serviced by that node onto different nodes; when traffic subsides, hello service can *merge* hello partition ranges from quiet nodes back onto a single node.</span></span>  

<span data-ttu-id="15f93-180">如需有關 hello 的 hello 內部詳細資料表格服務，以及特別是如何 hello 服務管理資料分割，請參閱 hello 紙張[Microsoft Azure 儲存體： 高可用雲端儲存體服務具有強式一致性](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).</span><span class="sxs-lookup"><span data-stu-id="15f93-180">For more information about hello internal details of hello Table service, and in particular how hello service manages partitions, see hello paper [Microsoft Azure Storage: A Highly Available Cloud Storage Service with Strong Consistency](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx).</span></span>  

### <a name="entity-group-transactions"></a><span data-ttu-id="15f93-181">實體群組交易</span><span class="sxs-lookup"><span data-stu-id="15f93-181">Entity Group Transactions</span></span>
<span data-ttu-id="15f93-182">在 hello 表格服務中，實體群組交易 (EGTs) 會是 hello 只有內建的機制，跨多個實體執行不可部分完成的更新。</span><span class="sxs-lookup"><span data-stu-id="15f93-182">In hello Table service, Entity Group Transactions (EGTs) are hello only built-in mechanism for performing atomic updates across multiple entities.</span></span> <span data-ttu-id="15f93-183">EGTs 也會參照的 tooas*批次交易*某些文件中。</span><span class="sxs-lookup"><span data-stu-id="15f93-183">EGTs are also referred tooas *batch transactions* in some documentation.</span></span> <span data-ttu-id="15f93-184">EGTs 僅能對儲存在 hello 的實體相同的資料分割 (共用 hello 給定資料表中的相同資料分割索引鍵)，所以每當您需要跨多個實體的不可部分完成的交易行為您需要這些實體是位於 hello 的 tooensure 相同的資料分割。</span><span class="sxs-lookup"><span data-stu-id="15f93-184">EGTs can only operate on entities stored in hello same partition (share hello same partition key in a given table), so anytime you need atomic transactional behavior across multiple entities you need tooensure that those entities are in hello same partition.</span></span> <span data-ttu-id="15f93-185">這通常是將多個實體類型保留在 hello 相同資料表 （和資料分割），並且不使用不同的實體類型的多個資料表的原因。</span><span class="sxs-lookup"><span data-stu-id="15f93-185">This is often a reason for keeping multiple entity types in hello same table (and partition) and not using multiple tables for different entity types.</span></span> <span data-ttu-id="15f93-186">單一 EGT 最多可以操作 100 個實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-186">A single EGT can operate on at most 100 entities.</span></span>  <span data-ttu-id="15f93-187">如果您送出多個並行 EGTs 處理是重要的 tooensure 這些 EGTs 不會被操作上是常見跨 EGTs 否則處理可能會因為延遲的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-187">If you submit multiple concurrent EGTs for processing it is important tooensure  those EGTs do not operate on entities that are common across EGTs as otherwise processing can be delayed.</span></span>

<span data-ttu-id="15f93-188">EGTs 也會導入 tooevaluate 在設計中潛在的取捨： 使用多個資料分割會增加應用程式的 hello 延展性，因為 Azure 有更多的機會，負載平衡要求到節點，但這可能會限制 hello您的應用程式 tooperform 不可部分完成交易的能力和維護您資料的強式一致性。</span><span class="sxs-lookup"><span data-stu-id="15f93-188">EGTs also introduce a potential trade-off for you tooevaluate in your design: using more partitions will increase hello scalability of your application because Azure has more opportunities for load balancing requests across nodes, but this might limit hello ability of your application tooperform atomic transactions and maintain strong consistency for your data.</span></span> <span data-ttu-id="15f93-189">此外，有特定的延展性目標層級 hello 的磁碟分割，可能會限制 hello 輸送量的交易，您可以預期會發生的單一節點： 如需有關 hello Azure 儲存體帳戶和 hello 資料表的延展性目標服務，請參閱[Azure 儲存體延展性和效能目標](storage-scalability-targets.md)。</span><span class="sxs-lookup"><span data-stu-id="15f93-189">Furthermore, there are specific scalability targets at hello level of a partition that might limit hello throughput of transactions you can expect for a single node: for more information about hello scalability targets for Azure storage accounts and hello table service, see [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md).</span></span> <span data-ttu-id="15f93-190">本指南稍後的章節討論各種設計策略，協助您管理此類，取捨，並討論如何 toochoose 您的資料分割索引鍵根據 hello 特定需求的用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="15f93-190">Later sections of this guide discuss various design strategies that help you manage trade-offs such as this one, and discuss how best toochoose your partition key based on hello specific requirements of your client application.</span></span>  

### <a name="capacity-considerations"></a><span data-ttu-id="15f93-191">容量考量</span><span class="sxs-lookup"><span data-stu-id="15f93-191">Capacity considerations</span></span>
<span data-ttu-id="15f93-192">hello 下表包含一些 hello 索引鍵值 toobe 注意當您設計的資料表服務方案：</span><span class="sxs-lookup"><span data-stu-id="15f93-192">hello following table includes some of hello key values toobe aware of when you are designing a Table service solution:</span></span>  

| <span data-ttu-id="15f93-193">Azure 儲存體帳戶的容量總計</span><span class="sxs-lookup"><span data-stu-id="15f93-193">Total capacity of an Azure storage account</span></span> | <span data-ttu-id="15f93-194">500 TB</span><span class="sxs-lookup"><span data-stu-id="15f93-194">500 TB</span></span> |
| --- | --- |
| <span data-ttu-id="15f93-195">Azure 儲存體帳戶中的資料表數目</span><span class="sxs-lookup"><span data-stu-id="15f93-195">Number of tables in an Azure storage account</span></span> |<span data-ttu-id="15f93-196">僅限於 hello hello 儲存體帳戶容量</span><span class="sxs-lookup"><span data-stu-id="15f93-196">Limited only by hello capacity of hello storage account</span></span> |
| <span data-ttu-id="15f93-197">資料表中的資料分割數目</span><span class="sxs-lookup"><span data-stu-id="15f93-197">Number of partitions in a table</span></span> |<span data-ttu-id="15f93-198">僅限於 hello hello 儲存體帳戶容量</span><span class="sxs-lookup"><span data-stu-id="15f93-198">Limited only by hello capacity of hello storage account</span></span> |
| <span data-ttu-id="15f93-199">資料分割中的實體數目</span><span class="sxs-lookup"><span data-stu-id="15f93-199">Number of entities in a partition</span></span> |<span data-ttu-id="15f93-200">僅限於 hello hello 儲存體帳戶容量</span><span class="sxs-lookup"><span data-stu-id="15f93-200">Limited only by hello capacity of hello storage account</span></span> |
| <span data-ttu-id="15f93-201">個別實體的大小</span><span class="sxs-lookup"><span data-stu-id="15f93-201">Size of an individual entity</span></span> |<span data-ttu-id="15f93-202">向上 too1 MB，最多 255 個屬性 (包括 hello **PartitionKey**， **RowKey**，和**時間戳記**)</span><span class="sxs-lookup"><span data-stu-id="15f93-202">Up too1 MB with a maximum of 255 properties (including hello **PartitionKey**, **RowKey**, and **Timestamp**)</span></span> |
| <span data-ttu-id="15f93-203">大小的 hello **PartitionKey**</span><span class="sxs-lookup"><span data-stu-id="15f93-203">Size of hello **PartitionKey**</span></span> |<span data-ttu-id="15f93-204">向上 too1 KB 大小的字串</span><span class="sxs-lookup"><span data-stu-id="15f93-204">A string up too1 KB in size</span></span> |
| <span data-ttu-id="15f93-205">大小的 hello **RowKey**</span><span class="sxs-lookup"><span data-stu-id="15f93-205">Size of hello **RowKey**</span></span> |<span data-ttu-id="15f93-206">向上 too1 KB 大小的字串</span><span class="sxs-lookup"><span data-stu-id="15f93-206">A string up too1 KB in size</span></span> |
| <span data-ttu-id="15f93-207">實體群組交易的大小</span><span class="sxs-lookup"><span data-stu-id="15f93-207">Size of an Entity Group Transaction</span></span> |<span data-ttu-id="15f93-208">交易可以包含最多 100 個實體，而且 hello 承載必須小於 4 MB 的大小。</span><span class="sxs-lookup"><span data-stu-id="15f93-208">A transaction can include at most 100 entities and hello payload must be less than 4 MB in size.</span></span> <span data-ttu-id="15f93-209">一個 EGT 只能更新實體一次。</span><span class="sxs-lookup"><span data-stu-id="15f93-209">An EGT can only update an entity once.</span></span> |

<span data-ttu-id="15f93-210">如需詳細資訊，請參閱[了解 hello 表格服務資料模型](http://msdn.microsoft.com/library/azure/dd179338.aspx)。</span><span class="sxs-lookup"><span data-stu-id="15f93-210">For more information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>  

### <a name="cost-considerations"></a><span data-ttu-id="15f93-211">成本考量</span><span class="sxs-lookup"><span data-stu-id="15f93-211">Cost considerations</span></span>
<span data-ttu-id="15f93-212">資料表儲存體比較便宜，但您應該包含這兩個容量使用方式與 hello 數量的交易的成本估計值做為評估版的 hello 表格服務會使用任何解決方案的一部分。</span><span class="sxs-lookup"><span data-stu-id="15f93-212">Table storage is relatively inexpensive, but you should include cost estimates for both capacity usage and hello quantity of transactions as part of your evaluation of any solution that uses hello Table service.</span></span> <span data-ttu-id="15f93-213">不過，在許多案例中將反正規化或重複的資料儲存在順序 tooimprove hello 效能或延展性，您是方案的有效的方法 tootake。</span><span class="sxs-lookup"><span data-stu-id="15f93-213">However, in many scenarios storing denormalized or duplicate data in order tooimprove hello performance or scalability of your solution is a valid approach tootake.</span></span> <span data-ttu-id="15f93-214">如需定價的詳細資訊，請參閱 [Azure 儲存體定價](https://azure.microsoft.com/pricing/details/storage/)。</span><span class="sxs-lookup"><span data-stu-id="15f93-214">For more information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/storage/).</span></span>  

## <a name="guidelines-for-table-design"></a><span data-ttu-id="15f93-215">資料表設計指導方針</span><span class="sxs-lookup"><span data-stu-id="15f93-215">Guidelines for table design</span></span>
<span data-ttu-id="15f93-216">這些清單摘要的一些 hello 主要的方針，您應該記住當您要設計您的資料表，與本指南會解決所有中更詳細地更新版本。</span><span class="sxs-lookup"><span data-stu-id="15f93-216">These lists summarize some of hello key guidelines you should keep in mind when you are designing your tables, and this guide will address them all in more detail later in.</span></span> <span data-ttu-id="15f93-217">這些方針有非常不同於您通常會依照關聯式資料庫設計的 hello 指導方針。</span><span class="sxs-lookup"><span data-stu-id="15f93-217">These guidelines are very different from hello guidelines you would typically follow for relational database design.</span></span>  

<span data-ttu-id="15f93-218">設計您的資料表服務方案 toobe*讀取*有效率：</span><span class="sxs-lookup"><span data-stu-id="15f93-218">Designing your Table service solution toobe *read* efficient:</span></span>

* <span data-ttu-id="15f93-219">***設計大量讀取應用程式中的查詢。***</span><span class="sxs-lookup"><span data-stu-id="15f93-219">***Design for querying in read-heavy applications.***</span></span> <span data-ttu-id="15f93-220">當您在設計您的資料表時，思考 hello 查詢 （特別是 hello 延遲敏感的），以執行您的想法方式，就會更新您的實體之前。</span><span class="sxs-lookup"><span data-stu-id="15f93-220">When you are designing your tables, think about hello queries (especially hello latency sensitive ones) that you will execute before you think about how you will update your entities.</span></span> <span data-ttu-id="15f93-221">透過這樣的方式，通常可造就一個有效率且高效能的解決方案。</span><span class="sxs-lookup"><span data-stu-id="15f93-221">This typically results in an efficient and performant solution.</span></span>  
* <span data-ttu-id="15f93-222">***在查詢中同時指定 PartitionKey 和 RowKey。***</span><span class="sxs-lookup"><span data-stu-id="15f93-222">***Specify both PartitionKey and RowKey in your queries.***</span></span> <span data-ttu-id="15f93-223">*點查詢*之類這些 hello 最有效率的資料表服務查詢。</span><span class="sxs-lookup"><span data-stu-id="15f93-223">*Point queries* such as these are hello most efficient table service queries.</span></span>  
* <span data-ttu-id="15f93-224">***考慮儲存重複的實體副本。***</span><span class="sxs-lookup"><span data-stu-id="15f93-224">***Consider storing duplicate copies of entities.***</span></span> <span data-ttu-id="15f93-225">資料表儲存體是廉價因此請考慮儲存 hello 同一個實體多次 （具有不同索引鍵） tooenable 更有效率的查詢。</span><span class="sxs-lookup"><span data-stu-id="15f93-225">Table storage is cheap so consider storing hello same entity multiple times (with different keys) tooenable more efficient queries.</span></span>  
* <span data-ttu-id="15f93-226">***考慮將資料反正規化。***</span><span class="sxs-lookup"><span data-stu-id="15f93-226">***Consider denormalizing your data.***</span></span> <span data-ttu-id="15f93-227">資料表儲存體十分便宜，所以建議您考慮將資料反正規化。</span><span class="sxs-lookup"><span data-stu-id="15f93-227">Table storage is cheap so consider denormalizing your data.</span></span> <span data-ttu-id="15f93-228">例如，儲存摘要實體的彙總資料的查詢只需要 tooaccess 單一實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-228">For example, store summary entities so that queries for aggregate data only need tooaccess a single entity.</span></span>  
* <span data-ttu-id="15f93-229">***使用複合索引鍵值。***</span><span class="sxs-lookup"><span data-stu-id="15f93-229">***Use compound key values.***</span></span> <span data-ttu-id="15f93-230">hello 只有您所擁有的索引鍵是**PartitionKey**和**RowKey**。</span><span class="sxs-lookup"><span data-stu-id="15f93-230">hello only keys you have are **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="15f93-231">例如，使用複合的索引鍵值 tooenable 替代索引鍵的存取路徑 tooentities。</span><span class="sxs-lookup"><span data-stu-id="15f93-231">For example, use compound key values tooenable alternate keyed access paths tooentities.</span></span>  
* <span data-ttu-id="15f93-232">***使用查詢預測。***</span><span class="sxs-lookup"><span data-stu-id="15f93-232">***Use query projection.***</span></span> <span data-ttu-id="15f93-233">您可以減少 hello 您使用查詢，選取剛才 hello 欄位，您需要傳送 hello 網路上的資料量。</span><span class="sxs-lookup"><span data-stu-id="15f93-233">You can reduce hello amount of data that you transfer over hello network by using queries that select just hello fields you need.</span></span>  

<span data-ttu-id="15f93-234">設計您的資料表服務方案 toobe*寫入*有效率：</span><span class="sxs-lookup"><span data-stu-id="15f93-234">Designing your Table service solution toobe *write* efficient:</span></span>  

* <span data-ttu-id="15f93-235">***不要建立熱分割。***</span><span class="sxs-lookup"><span data-stu-id="15f93-235">***Do not create hot partitions.***</span></span> <span data-ttu-id="15f93-236">選擇您的要求 toospread 可讓您的索引鍵之間的任何時間點上的多個資料分割。</span><span class="sxs-lookup"><span data-stu-id="15f93-236">Choose keys that enable you toospread your requests across multiple partitions at any point of time.</span></span>  
* <span data-ttu-id="15f93-237">***避免流量尖峰。***</span><span class="sxs-lookup"><span data-stu-id="15f93-237">***Avoid spikes in traffic.***</span></span> <span data-ttu-id="15f93-238">平滑 hello 流量透過合理的時間，並避免的流量尖峰。</span><span class="sxs-lookup"><span data-stu-id="15f93-238">Smooth hello traffic over a reasonable period of time and avoid spikes in traffic.</span></span>
* <span data-ttu-id="15f93-239">***不一定要為每個實體的類型建立個別的資料表。***</span><span class="sxs-lookup"><span data-stu-id="15f93-239">***Don't necessarily create a separate table for each type of entity.***</span></span> <span data-ttu-id="15f93-240">當您在實體類型之間都需要不可部分完成交易時，您可以儲存這些多個實體類型中相同資料分割中 hello hello 相同的資料表。</span><span class="sxs-lookup"><span data-stu-id="15f93-240">When you require atomic transactions across entity types, you can store these multiple entity types in hello same partition in hello same table.</span></span>
* <span data-ttu-id="15f93-241">***請考慮 hello 必須達到的最大輸送量。***</span><span class="sxs-lookup"><span data-stu-id="15f93-241">***Consider hello maximum throughput you must achieve.***</span></span> <span data-ttu-id="15f93-242">您必須留意 hello hello 表格服務的延展性目標，並確保您的設計將不會造成您 tooexceed 它們。</span><span class="sxs-lookup"><span data-stu-id="15f93-242">You must be aware of hello scalability targets for hello Table service and ensure that your design will not cause you tooexceed them.</span></span>  

<span data-ttu-id="15f93-243">當您閱讀本指南時，您會看到將這些原則全都納入實作的範例。</span><span class="sxs-lookup"><span data-stu-id="15f93-243">As you read this guide, you will see examples that put all of these principles into practice.</span></span>  

## <a name="design-for-querying"></a><span data-ttu-id="15f93-244">查詢的設計</span><span class="sxs-lookup"><span data-stu-id="15f93-244">Design for querying</span></span>
<span data-ttu-id="15f93-245">需要大量、 密集寫入的磁碟或 hello 兩者的混合，可能會讀取資料表服務解決方案。</span><span class="sxs-lookup"><span data-stu-id="15f93-245">Table service solutions may be read intensive, write intensive, or a mix of hello two.</span></span> <span data-ttu-id="15f93-246">在設計您的資料表服務 toosupport 有效率地讀取作業時，本節將著重於 hello 事項 toobear 記住。</span><span class="sxs-lookup"><span data-stu-id="15f93-246">This section focuses on hello things toobear in mind when you are designing your Table service toosupport read operations efficiently.</span></span> <span data-ttu-id="15f93-247">一般而言，支援有效讀取作業的設計，也可兼顧寫入作業的效率。</span><span class="sxs-lookup"><span data-stu-id="15f93-247">Typically, a design that supports read operations efficiently is also efficient for write operations.</span></span> <span data-ttu-id="15f93-248">不過，有其他考量 toobear 記住當設計 toosupport 寫入作業，hello 下一節中討論[設計用於資料修改](#design-for-data-modification)。</span><span class="sxs-lookup"><span data-stu-id="15f93-248">However, there are additional considerations toobear in mind when designing toosupport write operations, discussed in hello next section, [Design for data modification](#design-for-data-modification).</span></span>

<span data-ttu-id="15f93-249">設計您的資料表服務方案 tooenable 很好的起點 tooread 資料有效率地為 tooask"何種查詢將我的應用程式需要 tooexecute tooretrieve hello 資料需要從 hello 表格服務 」？</span><span class="sxs-lookup"><span data-stu-id="15f93-249">A good starting point for designing your Table service solution tooenable you tooread data efficiently is tooask "What queries will my application need tooexecute tooretrieve hello data it needs from hello Table service?"</span></span>  

> [!NOTE]
> <span data-ttu-id="15f93-250">以 hello 表格服務，請務必 tooget hello 正確設計最前面位置，所以它會發生困難而且昂貴 toochange 於稍後。</span><span class="sxs-lookup"><span data-stu-id="15f93-250">With hello Table service, it's important tooget hello design correct up front because it's difficult and expensive toochange it later.</span></span> <span data-ttu-id="15f93-251">例如，在關聯式資料庫中通常很可能 tooaddress 效能問題，只要加入索引 tooan 現有資料庫： 這不是以 hello 表格服務的選項。</span><span class="sxs-lookup"><span data-stu-id="15f93-251">For example, in a relational database it's often possible tooaddress performance issues simply by adding indexes tooan existing database: this is not an option with hello Table service.</span></span>  
> 
> 

<span data-ttu-id="15f93-252">本節著重於 hello 設計來查詢資料表時，您必須解決的重要問題。</span><span class="sxs-lookup"><span data-stu-id="15f93-252">This section focuses on hello key issues you must address when you design your tables for querying.</span></span> <span data-ttu-id="15f93-253">本章節涵蓋的 hello 主題包括：</span><span class="sxs-lookup"><span data-stu-id="15f93-253">hello topics covered in this section include:</span></span>

* [<span data-ttu-id="15f93-254">您選擇的 PartitionKey 和 RowKey 對查詢效能有何影響</span><span class="sxs-lookup"><span data-stu-id="15f93-254">How your choice of PartitionKey and RowKey impacts query performance</span></span>](#how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance)
* [<span data-ttu-id="15f93-255">選擇適當的 PartitionKey</span><span class="sxs-lookup"><span data-stu-id="15f93-255">Choosing an appropriate PartitionKey</span></span>](#choosing-an-appropriate-partitionkey)
* [<span data-ttu-id="15f93-256">最佳化 hello 表格服務的查詢</span><span class="sxs-lookup"><span data-stu-id="15f93-256">Optimizing queries for hello Table service</span></span>](#optimizing-queries-for-the-table-service)
* [<span data-ttu-id="15f93-257">在 hello 表格服務中排序資料</span><span class="sxs-lookup"><span data-stu-id="15f93-257">Sorting data in hello Table service</span></span>](#sorting-data-in-the-table-service)

### <a name="how-your-choice-of-partitionkey-and-rowkey-impacts-query-performance"></a><span data-ttu-id="15f93-258">您選擇的 PartitionKey 和 RowKey 對查詢效能有何影響</span><span class="sxs-lookup"><span data-stu-id="15f93-258">How your choice of PartitionKey and RowKey impacts query performance</span></span>
<span data-ttu-id="15f93-259">hello 下列範例會假設 hello 表格服務會儲存員工實體具有下列結構的 hello (大部分 hello 範例省略 hello**時間戳記**為了清楚起見屬性):</span><span class="sxs-lookup"><span data-stu-id="15f93-259">hello following examples assume hello table service is storing employee entities with hello following structure (most of hello examples omit hello **Timestamp** property for clarity):</span></span>  

| <span data-ttu-id="15f93-260">*資料行名稱*</span><span class="sxs-lookup"><span data-stu-id="15f93-260">*Column name*</span></span> | <span data-ttu-id="15f93-261">*資料類型*</span><span class="sxs-lookup"><span data-stu-id="15f93-261">*Data type*</span></span> |
| --- | --- |
| <span data-ttu-id="15f93-262">**PartitionKey** (部門名稱)</span><span class="sxs-lookup"><span data-stu-id="15f93-262">**PartitionKey** (Department Name)</span></span> |<span data-ttu-id="15f93-263">String</span><span class="sxs-lookup"><span data-stu-id="15f93-263">String</span></span> |
| <span data-ttu-id="15f93-264">**RowKey** (員工識別碼)</span><span class="sxs-lookup"><span data-stu-id="15f93-264">**RowKey** (Employee Id)</span></span> |<span data-ttu-id="15f93-265">String</span><span class="sxs-lookup"><span data-stu-id="15f93-265">String</span></span> |
| <span data-ttu-id="15f93-266">**名字**</span><span class="sxs-lookup"><span data-stu-id="15f93-266">**FirstName**</span></span> |<span data-ttu-id="15f93-267">String</span><span class="sxs-lookup"><span data-stu-id="15f93-267">String</span></span> |
| <span data-ttu-id="15f93-268">**姓氏**</span><span class="sxs-lookup"><span data-stu-id="15f93-268">**LastName**</span></span> |<span data-ttu-id="15f93-269">String</span><span class="sxs-lookup"><span data-stu-id="15f93-269">String</span></span> |
| <span data-ttu-id="15f93-270">**年齡**</span><span class="sxs-lookup"><span data-stu-id="15f93-270">**Age**</span></span> |<span data-ttu-id="15f93-271">Integer</span><span class="sxs-lookup"><span data-stu-id="15f93-271">Integer</span></span> |
| <span data-ttu-id="15f93-272">**EmailAddress**</span><span class="sxs-lookup"><span data-stu-id="15f93-272">**EmailAddress**</span></span> |<span data-ttu-id="15f93-273">String</span><span class="sxs-lookup"><span data-stu-id="15f93-273">String</span></span> |

<span data-ttu-id="15f93-274">hello 前一節[Azure 資料表服務概觀](#overview)描述一些 hello 的主要功能 hello Azure 表格服務具有直接影響查詢的設計。</span><span class="sxs-lookup"><span data-stu-id="15f93-274">hello earlier section [Azure Table service overview](#overview) describes some of hello key features of hello Azure Table service that have a direct influence on designing for query.</span></span> <span data-ttu-id="15f93-275">這是因為在 hello 設計資料表服務查詢的一般指導方針。</span><span class="sxs-lookup"><span data-stu-id="15f93-275">These result in hello following general guidelines for designing Table service queries.</span></span> <span data-ttu-id="15f93-276">請注意，用在 hello 以下範例中的 hello 篩選語法與 hello 表格服務 REST API 的詳細資訊，請參閱[查詢實體](http://msdn.microsoft.com/library/azure/dd179421.aspx)。</span><span class="sxs-lookup"><span data-stu-id="15f93-276">Note that hello filter syntax used in hello examples below is from hello Table service REST API, for more information see [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span></span>  

* <span data-ttu-id="15f93-277">A***點查詢***hello 最有效查閱 toouse，而且建議 toobe 用於高容量查閱或需要最低延遲的查閱。</span><span class="sxs-lookup"><span data-stu-id="15f93-277">A ***Point Query*** is hello most efficient lookup toouse and is recommended toobe used for high-volume lookups or lookups requiring lowest latency.</span></span> <span data-ttu-id="15f93-278">這類查詢可以非常有效率的方式使用 hello 索引 toolocate 個別的實體，藉由指定 兩者 hello **PartitionKey**和**RowKey**值。</span><span class="sxs-lookup"><span data-stu-id="15f93-278">Such a query can use hello indexes toolocate an individual entity very efficiently by specifying both hello **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="15f93-279">例如：$filter=(PartitionKey eq 'Sales') and (RowKey eq '2')</span><span class="sxs-lookup"><span data-stu-id="15f93-279">For example: $filter=(PartitionKey eq 'Sales') and (RowKey eq '2')</span></span>  
* <span data-ttu-id="15f93-280">第二個最是***範圍查詢***使用 hello **PartitionKey**和篩選的範圍上**RowKey**值 tooreturn 多個實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-280">Second best is a ***Range Query*** that uses hello **PartitionKey** and filters on a range of **RowKey** values tooreturn more than one entity.</span></span> <span data-ttu-id="15f93-281">hello **PartitionKey**值，識別特定的資料分割，以及 hello **RowKey**值會識別該資料分割中的 hello 實體的子集。</span><span class="sxs-lookup"><span data-stu-id="15f93-281">hello **PartitionKey** value identifies a specific partition, and hello **RowKey** values identify a subset of hello entities in that partition.</span></span> <span data-ttu-id="15f93-282">例如：$filter=PartitionKey eq 'Sales' and RowKey ge 'S' and RowKey lt 'T'</span><span class="sxs-lookup"><span data-stu-id="15f93-282">For example: $filter=PartitionKey eq 'Sales' and RowKey ge 'S' and RowKey lt 'T'</span></span>  
* <span data-ttu-id="15f93-283">第三個最佳是***資料分割掃描***使用 hello **PartitionKey**和另一個非索引鍵屬性，而且該篩選可能會傳回一個以上的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-283">Third best is a ***Partition Scan*** that uses hello **PartitionKey** and filters on another non-key property and that may return more than one entity.</span></span> <span data-ttu-id="15f93-284">hello **PartitionKey**值會識別特定資料分割，以及 hello 屬性值，則選取該資料分割中的 hello 實體的子集。</span><span class="sxs-lookup"><span data-stu-id="15f93-284">hello **PartitionKey** value identifies a specific partition, and hello property values select for a subset of hello entities in that partition.</span></span> <span data-ttu-id="15f93-285">例如：$filter=PartitionKey eq 'Sales' and LastName eq 'Smith'</span><span class="sxs-lookup"><span data-stu-id="15f93-285">For example: $filter=PartitionKey eq 'Sales' and LastName eq 'Smith'</span></span>  
* <span data-ttu-id="15f93-286">A***資料表掃描***不包含 hello **PartitionKey**和就非常沒有效率，因為它會搜尋所有組成您的資料表，接著的所有相符實體的 hello 磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="15f93-286">A ***Table Scan*** does not include hello **PartitionKey** and is very inefficient because it searches all of hello partitions that make up your table in turn for any matching entities.</span></span> <span data-ttu-id="15f93-287">它會執行資料表掃描，不論您的篩選器是否使用 hello **RowKey**。</span><span class="sxs-lookup"><span data-stu-id="15f93-287">It will perform a table scan regardless of whether or not your filter uses hello **RowKey**.</span></span> <span data-ttu-id="15f93-288">例如：$filter=LastName eq 'Jones'</span><span class="sxs-lookup"><span data-stu-id="15f93-288">For example: $filter=LastName eq 'Jones'</span></span>  
* <span data-ttu-id="15f93-289">傳回多個實體的查詢，在傳回時會以 **PartitionKey** 和 **RowKey** 順序排序。</span><span class="sxs-lookup"><span data-stu-id="15f93-289">Queries that return multiple entities return them sorted in **PartitionKey** and **RowKey** order.</span></span> <span data-ttu-id="15f93-290">選擇 tooavoid hello client 中的，就可以做到 hello 實體**RowKey**定義 hello 最常見的排序次序。</span><span class="sxs-lookup"><span data-stu-id="15f93-290">tooavoid resorting hello entities in hello client, choose a **RowKey** that defines hello most common sort order.</span></span>  

<span data-ttu-id="15f93-291">請注意，使用"**或**"篩選器根據的 toospecify **RowKey**值產生資料分割掃描並不會被視為範圍查詢。</span><span class="sxs-lookup"><span data-stu-id="15f93-291">Note that using an "**or**" toospecify a filter based on **RowKey** values results in a partition scan and is not treated as a range query.</span></span> <span data-ttu-id="15f93-292">因此，您應該避免會使用下列篩選條件的搜尋：例如 $filter=PartitionKey eq 'Sales' and (RowKey eq '121' or RowKey eq '322')</span><span class="sxs-lookup"><span data-stu-id="15f93-292">Therefore, you should avoid queries that use filters such as: $filter=PartitionKey eq 'Sales' and (RowKey eq '121' or RowKey eq '322')</span></span>  

<span data-ttu-id="15f93-293">如需使用 hello 儲存體用戶端程式庫 tooexecute 有效率的查詢的用戶端程式碼範例，請參閱：</span><span class="sxs-lookup"><span data-stu-id="15f93-293">For examples of client-side code that use hello Storage Client Library tooexecute efficient queries, see:</span></span>  

* [<span data-ttu-id="15f93-294">執行點查詢使用 hello 儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="15f93-294">Executing a point query using hello Storage Client Library</span></span>](#executing-a-point-query-using-the-storage-client-library)
* [<span data-ttu-id="15f93-295">使用 LINQ 擷取多個實體</span><span class="sxs-lookup"><span data-stu-id="15f93-295">Retrieving multiple entities using LINQ</span></span>](#retrieving-multiple-entities-using-linq)
* [<span data-ttu-id="15f93-296">伺服器端預測</span><span class="sxs-lookup"><span data-stu-id="15f93-296">Server-side projection</span></span>](#server-side-projection)  

<span data-ttu-id="15f93-297">如需範例，可以處理多個實體的用戶端程式碼的型別儲存在 hello 相同資料表中，請參閱：</span><span class="sxs-lookup"><span data-stu-id="15f93-297">For examples of client-side code that can handle multiple entity types stored in hello same table, see:</span></span>  

* [<span data-ttu-id="15f93-298">使用異質性實體類型</span><span class="sxs-lookup"><span data-stu-id="15f93-298">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  

### <a name="choosing-an-appropriate-partitionkey"></a><span data-ttu-id="15f93-299">選擇適當的 PartitionKey</span><span class="sxs-lookup"><span data-stu-id="15f93-299">Choosing an appropriate PartitionKey</span></span>
<span data-ttu-id="15f93-300">您所選擇的**PartitionKey**應該平衡 hello 需要 tooenables hello 使用 EGTs （tooensure 一致性） hello 需求 toodistribute 對您的實體之間的多個資料分割 (tooensure 靈活的解決方案)。</span><span class="sxs-lookup"><span data-stu-id="15f93-300">Your choice of **PartitionKey** should balance hello need tooenables hello use of EGTs (tooensure consistency) against hello requirement toodistribute your entities across multiple partitions (tooensure a scalable solution).</span></span>  

<span data-ttu-id="15f93-301">其中一種方式，您可以在單一磁碟分割，儲存您的實體，但這可能會限制您的方案 hello 延展性，並可避免 hello 表格服務進行可以 tooload 平衡要求。</span><span class="sxs-lookup"><span data-stu-id="15f93-301">At one extreme, you could store all your entities in a single partition, but this may limit hello scalability of your solution and would prevent hello table service from being able tooload-balance requests.</span></span> <span data-ttu-id="15f93-302">在 hello 其他極端的做法是，您可以儲存一個實體，每個資料分割，這會是可高度擴充和讓 hello 資料表服務 tooload 平衡要求，但這會讓您無法使用實體群組交易。</span><span class="sxs-lookup"><span data-stu-id="15f93-302">At hello other extreme, you could store one entity per partition, which would be highly scalable and which enables hello table service tooload-balance requests, but which would prevent you from using entity group transactions.</span></span>  

<span data-ttu-id="15f93-303">最理想的**PartitionKey**是指 toouse 有效率的查詢可讓您和您的方案具有足夠的磁碟分割 tooensure 延展性功能。</span><span class="sxs-lookup"><span data-stu-id="15f93-303">An ideal **PartitionKey** is one that enables you toouse efficient queries and that has sufficient partitions tooensure your solution is scalable.</span></span> <span data-ttu-id="15f93-304">一般而言，您會發現您的實體將具有適當的屬性，可將您的實體分散到足夠的磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="15f93-304">Typically, you will find that your entities will have a suitable property that distributes your entities across sufficient partitions.</span></span>

> [!NOTE]
> <span data-ttu-id="15f93-305">例如，在儲存使用者或員工相關資訊的系統中，UserID 可以是一個良好的 PartitionKey。</span><span class="sxs-lookup"><span data-stu-id="15f93-305">For example, in a system that stores information about users or employees, UserID may be a good PartitionKey.</span></span> <span data-ttu-id="15f93-306">您可能需要數個指定的使用者識別碼做為 hello 資料分割索引鍵的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-306">You may have several entities that use a given UserID as hello partition key.</span></span> <span data-ttu-id="15f93-307">儲存使用者相關資料的每個實體會分組到單一資料分割，因此這些實體可透過實體群組交易來存取，同時仍具有高擴充性。</span><span class="sxs-lookup"><span data-stu-id="15f93-307">Each entity that stores data about a user is grouped into a single partition, and so these entities are accessible via entity group transactions, while still being highly scalable.</span></span>
> 
> 

<span data-ttu-id="15f93-308">還有其他考量，在您選擇的**PartitionKey** toohow 會插入、 更新和刪除實體相關的： hello 參閱[設計用於資料修改](#design-for-data-modification)下方。</span><span class="sxs-lookup"><span data-stu-id="15f93-308">There are additional considerations in your choice of **PartitionKey** that relate toohow you will insert, update, and delete entities: see hello section [Design for data modification](#design-for-data-modification) below.</span></span>  

### <a name="optimizing-queries-for-hello-table-service"></a><span data-ttu-id="15f93-309">最佳化 hello 表格服務的查詢</span><span class="sxs-lookup"><span data-stu-id="15f93-309">Optimizing queries for hello Table service</span></span>
<span data-ttu-id="15f93-310">hello 表格服務會自動索引您的實體使用 hello **PartitionKey**和**RowKey**值中的單一叢集索引，因此 hello 點查詢是 hello toouse 最有效率的原因.</span><span class="sxs-lookup"><span data-stu-id="15f93-310">hello Table service automatically indexes your entities using hello **PartitionKey** and **RowKey** values in a single clustered index, hence hello reason that point queries are hello most efficient toouse.</span></span> <span data-ttu-id="15f93-311">不過，有一些 hello hello 上的叢集索引沒有索引以外， **PartitionKey**和**RowKey**。</span><span class="sxs-lookup"><span data-stu-id="15f93-311">However, there are no indexes other than that on hello clustered index on hello **PartitionKey** and **RowKey**.</span></span>

<span data-ttu-id="15f93-312">許多設計必須符合需求 tooenable 查閱的多個準則為基礎的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-312">Many designs must meet requirements tooenable lookup of entities based on multiple criteria.</span></span> <span data-ttu-id="15f93-313">比方說，根據電子郵件、員工識別碼或姓氏找出員工實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-313">For example, locating employee entities based on email, employee id, or last name.</span></span> <span data-ttu-id="15f93-314">下列 hello > 一節中的模式 hello[資料表設計模式](#table-design-patterns)解決這些類型的需求，並描述的 hello 事實 hello 表格服務不會提供次要索引的解決方式：</span><span class="sxs-lookup"><span data-stu-id="15f93-314">hello following patterns in hello section [Table Design Patterns](#table-design-patterns) address these types of requirement and describe ways of working around hello fact that hello Table service does not provide secondary indexes:</span></span>  

* <span data-ttu-id="15f93-315">[內部資料分割的次要索引模式](#intra-partition-secondary-index-pattern)-儲存多個複本的每一個實體使用不同**RowKey**值 (hello 中相同的資料分割) tooenable 快速又有效率查閱和替代排序所使用的訂單不同**RowKey**值。</span><span class="sxs-lookup"><span data-stu-id="15f93-315">[Intra-partition secondary index pattern](#intra-partition-secondary-index-pattern) - Store multiple copies of each entity using different **RowKey** values (in hello same partition) tooenable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="15f93-316">[間的資料分割的次要索引模式](#inter-partition-secondary-index-pattern)-儲存多個複本的每個實體使用不同 RowKey 值在不同的磁碟分割或個別的資料表 tooenable 快速並有效查閱和替代排序訂單使用不同的**RowKey**值。</span><span class="sxs-lookup"><span data-stu-id="15f93-316">[Inter-partition secondary index pattern](#inter-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values in separate partitions or in separate tables tooenable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="15f93-317">[索引實體模式](#index-entities-pattern)-維護索引實體 tooenable 有效率的搜尋傳回的實體清單。</span><span class="sxs-lookup"><span data-stu-id="15f93-317">[Index Entities Pattern](#index-entities-pattern) - Maintain index entities tooenable efficient searches that return lists of entities.</span></span>  

### <a name="sorting-data-in-hello-table-service"></a><span data-ttu-id="15f93-318">在 hello 表格服務中排序資料</span><span class="sxs-lookup"><span data-stu-id="15f93-318">Sorting data in hello Table service</span></span>
<span data-ttu-id="15f93-319">hello 表格服務會傳回以遞增方式排序依據的實體**PartitionKey**再依據**RowKey**。</span><span class="sxs-lookup"><span data-stu-id="15f93-319">hello Table service returns entities sorted in ascending order based on **PartitionKey** and then by **RowKey**.</span></span> <span data-ttu-id="15f93-320">這些金鑰為字串值和數字值正確地排序的 tooensure 應該 tooa 固定長度轉換成，它們填補零。</span><span class="sxs-lookup"><span data-stu-id="15f93-320">These keys are string values and tooensure that numeric values sort correctly, you should convert them tooa fixed length and pad them with zeroes.</span></span> <span data-ttu-id="15f93-321">例如，如果 hello 員工識別碼值您做 hello **RowKey**是整數值，您應將轉換成員工識別碼**123**太**00000123**。</span><span class="sxs-lookup"><span data-stu-id="15f93-321">For example, if hello employee id value you use as hello **RowKey** is an integer value, you should convert employee id **123** too**00000123**.</span></span>  

<span data-ttu-id="15f93-322">許多應用程式有 toouse 資料排序順序不同的需求： 例如，排序員工，依名稱，或加入日期。</span><span class="sxs-lookup"><span data-stu-id="15f93-322">Many applications have requirements toouse data sorted in different orders: for example, sorting employees by name, or by joining date.</span></span> <span data-ttu-id="15f93-323">下列 hello > 一節中的模式 hello[資料表設計模式](#table-design-patterns)定址實體 tooalternate 排序順序的方式：</span><span class="sxs-lookup"><span data-stu-id="15f93-323">hello following patterns in hello section [Table Design Patterns](#table-design-patterns) address how tooalternate sort orders for your entities:</span></span>  

* <span data-ttu-id="15f93-324">[內部資料分割的次要索引模式](#intra-partition-secondary-index-pattern)-儲存每個實體使用不同 RowKey 值的多個複本 (hello 中相同的資料分割) tooenable 快速又有效率查閱和替代排序訂單使用的不同 RowKey 值。</span><span class="sxs-lookup"><span data-stu-id="15f93-324">[Intra-partition secondary index pattern](#intra-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values (in hello same partition) tooenable fast and efficient lookups and alternate sort orders by using different RowKey values.</span></span>  
* <span data-ttu-id="15f93-325">[間的資料分割的次要索引模式](#inter-partition-secondary-index-pattern)-存放區使用不同 RowKey 值快速 tooenable 個別的資料表中的個別資料分割中每個實體的多個複本，並使用不同 RowKey 的有效率查閱和替代排序訂單值。</span><span class="sxs-lookup"><span data-stu-id="15f93-325">[Inter-partition secondary index pattern](#inter-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values in separate partitions in separate tables tooenable fast and efficient lookups and alternate sort orders by using different RowKey values.</span></span>
* <span data-ttu-id="15f93-326">[記錄檔結尾模式](#log-tail-pattern)-擷取 hello  *n* 實體最近加入 tooa 資料分割使用**RowKey**以反向的日期和時間順序排序的值。</span><span class="sxs-lookup"><span data-stu-id="15f93-326">[Log tail pattern](#log-tail-pattern) - Retrieve hello *n* entities most recently added tooa partition by using a **RowKey** value that sorts in reverse date and time order.</span></span>  

## <a name="design-for-data-modification"></a><span data-ttu-id="15f93-327">資料修改的設計</span><span class="sxs-lookup"><span data-stu-id="15f93-327">Design for data modification</span></span>
<span data-ttu-id="15f93-328">本節著重於 hello 設計考量最佳化插入、 更新和刪除。</span><span class="sxs-lookup"><span data-stu-id="15f93-328">This section focuses on hello design considerations for optimizing inserts, updates, and deletes.</span></span> <span data-ttu-id="15f93-329">在某些情況下，您需要針對查詢最佳化的資料修改，就像您一樣的關聯式資料庫設計 （雖然 hello 方法來管理 hello 設計的設計最佳化的設計之間 tooevaluate hello 取捨缺點是關聯式資料庫中不同）。</span><span class="sxs-lookup"><span data-stu-id="15f93-329">In some cases, you will need tooevaluate hello trade-off between designs that optimize for querying against designs that optimize for data modification just as you do in designs for relational databases (although hello techniques for managing hello design trade-offs are different in a relational database).</span></span> <span data-ttu-id="15f93-330">hello 區段[資料表設計模式](#table-design-patterns)描述 hello 表格服務的一些詳細的設計模式，並強調一些這些取捨當中。</span><span class="sxs-lookup"><span data-stu-id="15f93-330">hello section [Table Design Patterns](#table-design-patterns) describes some detailed design patterns for hello Table service and highlights some these trade-offs.</span></span> <span data-ttu-id="15f93-331">在實務上，您會發現許多針對查詢實體而最佳化的設計也適用於修改實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-331">In practice, you will find that many designs optimized for querying entities also work well for modifying entities.</span></span>  

### <a name="optimizing-hello-performance-of-insert-update-and-delete-operations"></a><span data-ttu-id="15f93-332">Hello 效能最佳化的 insert、 update 和 delete 作業</span><span class="sxs-lookup"><span data-stu-id="15f93-332">Optimizing hello performance of insert, update, and delete operations</span></span>
<span data-ttu-id="15f93-333">tooupdate 或刪除實體，您必須是能夠 tooidentify 它使用 hello **PartitionKey**和**RowKey**值。</span><span class="sxs-lookup"><span data-stu-id="15f93-333">tooupdate or delete an entity, you must be able tooidentify it by using hello **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="15f93-334">在這一方面，您所選擇的**PartitionKey**和**RowKey**修改實體應該遵循的類似準則 tooyour 選擇 toosupport 點查詢，因為您想要為 tooidentify 實體盡可能有效率地。</span><span class="sxs-lookup"><span data-stu-id="15f93-334">In this respect, your choice of **PartitionKey** and **RowKey** for modifying entities should follow similar criteria tooyour choice toosupport point queries because you want tooidentify entities as efficiently as possible.</span></span> <span data-ttu-id="15f93-335">您不想 toouse 效率不佳的磁碟分割或資料表掃描 toolocate 順序 toodiscover hello 中的實體**PartitionKey**和**RowKey**值需要 tooupdate，或將它刪除。</span><span class="sxs-lookup"><span data-stu-id="15f93-335">You do not want toouse an inefficient partition or table scan toolocate an entity in order toodiscover hello **PartitionKey** and **RowKey** values you need tooupdate or delete it.</span></span>  

<span data-ttu-id="15f93-336">下列 hello > 一節中的模式 hello[資料表設計模式](#table-design-patterns)解決 hello，最佳化效能，或插入、 更新和刪除作業：</span><span class="sxs-lookup"><span data-stu-id="15f93-336">hello following patterns in hello section [Table Design Patterns](#table-design-patterns) address optimizing hello performance or your insert, update, and delete operations:</span></span>  

* <span data-ttu-id="15f93-337">[高容量刪除模式](#high-volume-delete-pattern)-啟用 hello 刪除大量實體藉由在自己的個別資料表中儲存為同時刪除所有 hello 實體; 您刪除 hello 實體 hello 資料表中刪除。</span><span class="sxs-lookup"><span data-stu-id="15f93-337">[High volume delete pattern](#high-volume-delete-pattern) - Enable hello deletion of a high volume of entities by storing all hello entities for simultaneous deletion in their own separate table; you delete hello entities by deleting hello table.</span></span>  
* <span data-ttu-id="15f93-338">[資料序列模式](#data-series-pattern)-存放區完整的資料數列中要求您進行的單一實體 toominimize hello 數字。</span><span class="sxs-lookup"><span data-stu-id="15f93-338">[Data series pattern](#data-series-pattern) - Store complete data series in a single entity toominimize hello number of requests you make.</span></span>  
* <span data-ttu-id="15f93-339">[寬實體模式](#wide-entities-pattern)-以上 252 屬性搭配使用多個實體的實體 toostore 邏輯實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-339">[Wide entities pattern](#wide-entities-pattern) - Use multiple physical entities toostore logical entities with more than 252 properties.</span></span>  
* <span data-ttu-id="15f93-340">[大型實體模式](#large-entities-pattern)-使用 blob 儲存體 toostore 大型屬性值。</span><span class="sxs-lookup"><span data-stu-id="15f93-340">[Large entities pattern](#large-entities-pattern) - Use blob storage toostore large property values.</span></span>  

### <a name="ensuring-consistency-in-your-stored-entities"></a><span data-ttu-id="15f93-341">確保預存實體中的一致性</span><span class="sxs-lookup"><span data-stu-id="15f93-341">Ensuring consistency in your stored entities</span></span>
<span data-ttu-id="15f93-342">hello 其他的最佳化資料修改會影響您所選擇的索引鍵的關鍵因素如何 tooensure 使用不可部分完成交易的一致性。</span><span class="sxs-lookup"><span data-stu-id="15f93-342">hello other key factor that influences your choice of keys for optimizing data modifications is how tooensure consistency by using atomic transactions.</span></span> <span data-ttu-id="15f93-343">您只能使用實體儲存在 hello EGT toooperate 相同的資料分割。</span><span class="sxs-lookup"><span data-stu-id="15f93-343">You can only use an EGT toooperate on entities stored in hello same partition.</span></span>  

<span data-ttu-id="15f93-344">下列 hello > 一節中的模式 hello[資料表設計模式](#table-design-patterns)管理一致性的位址：</span><span class="sxs-lookup"><span data-stu-id="15f93-344">hello following patterns in hello section [Table Design Patterns](#table-design-patterns) address managing consistency:</span></span>  

* <span data-ttu-id="15f93-345">[內部資料分割的次要索引模式](#intra-partition-secondary-index-pattern)-儲存多個複本的每一個實體使用不同**RowKey**值 (hello 中相同的資料分割) tooenable 快速又有效率查閱和替代排序所使用的訂單不同**RowKey**值。</span><span class="sxs-lookup"><span data-stu-id="15f93-345">[Intra-partition secondary index pattern](#intra-partition-secondary-index-pattern) - Store multiple copies of each entity using different **RowKey** values (in hello same partition) tooenable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="15f93-346">[間的資料分割的次要索引模式](#inter-partition-secondary-index-pattern)-儲存多個複本的每個實體使用不同 RowKey 值在不同的磁碟分割或個別的資料表 tooenable 快速並有效查閱和替代排序訂單使用不同的**RowKey**值。</span><span class="sxs-lookup"><span data-stu-id="15f93-346">[Inter-partition secondary index pattern](#inter-partition-secondary-index-pattern) - Store multiple copies of each entity using different RowKey values in separate partitions or in separate tables tooenable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  
* <span data-ttu-id="15f93-347">[最終一致的交易模式](#eventually-consistent-transactions-pattern) - 使用 Azure 佇列，跨資料分割界限或儲存體系統界限啟用最終一致的行為。</span><span class="sxs-lookup"><span data-stu-id="15f93-347">[Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) - Enable eventually consistent behavior across partition boundaries or storage system boundaries by using Azure queues.</span></span>
* <span data-ttu-id="15f93-348">[索引實體模式](#index-entities-pattern)-維護索引實體 tooenable 有效率的搜尋傳回的實體清單。</span><span class="sxs-lookup"><span data-stu-id="15f93-348">[Index Entities Pattern](#index-entities-pattern) - Maintain index entities tooenable efficient searches that return lists of entities.</span></span>  
* <span data-ttu-id="15f93-349">[非正規化模式](#denormalization-pattern)-合併的相關資料一起在單一實體 tooenable 您 tooretrieve 所有 hello 您需要使用單點查詢的資料。</span><span class="sxs-lookup"><span data-stu-id="15f93-349">[Denormalization pattern](#denormalization-pattern) - Combine related data together in a single entity tooenable you tooretrieve all hello data you need with a single point query.</span></span>  
* <span data-ttu-id="15f93-350">[資料序列模式](#data-series-pattern)-存放區完整的資料數列中要求您進行的單一實體 toominimize hello 數字。</span><span class="sxs-lookup"><span data-stu-id="15f93-350">[Data series pattern](#data-series-pattern) - Store complete data series in a single entity toominimize hello number of requests you make.</span></span>  

<span data-ttu-id="15f93-351">如需實體群組交易資訊，請參閱 hello 節[實體群組交易](#entity-group-transactions)。</span><span class="sxs-lookup"><span data-stu-id="15f93-351">For information about entity group transactions, see hello section [Entity Group Transactions](#entity-group-transactions).</span></span>  

### <a name="ensuring-your-design-for-efficient-modifications-facilitates-efficient-queries"></a><span data-ttu-id="15f93-352">確保您針對有效率的修改所做的設計有助於提升查詢效率</span><span class="sxs-lookup"><span data-stu-id="15f93-352">Ensuring your design for efficient modifications facilitates efficient queries</span></span>
<span data-ttu-id="15f93-353">在許多情況下，有效率的查詢結果中有效的修改，但您的設計應該一律評估是否這是您的特定案例的 hello 狀況。</span><span class="sxs-lookup"><span data-stu-id="15f93-353">In many cases, a design for efficient querying results in efficient modifications, but you should always evaluate whether this is hello case for your specific scenario.</span></span> <span data-ttu-id="15f93-354">某些 hello > 一節中的 hello 模式[資料表設計模式](#table-design-patterns)明確評估查詢及修改實體之間的利弊得失，您應該一律納入帳戶 hello 數目每種作業類型。</span><span class="sxs-lookup"><span data-stu-id="15f93-354">Some of hello patterns in hello section [Table Design Patterns](#table-design-patterns) explicitly evaluate trade-offs between querying and modifying entities, and you should always take into account hello number of each type of operation.</span></span>  

<span data-ttu-id="15f93-355">下列 hello > 一節中的模式 hello[資料表設計模式](#table-design-patterns)位址之間的有效率的查詢設計和設計有效率的資料修改的利弊得失：</span><span class="sxs-lookup"><span data-stu-id="15f93-355">hello following patterns in hello section [Table Design Patterns](#table-design-patterns) address trade-offs between designing for efficient queries and designing for efficient data modification:</span></span>  

* <span data-ttu-id="15f93-356">[複合索引鍵模式](#compound-key-pattern)-使用複合**RowKey**值 tooenable 用戶端 toolookup 相關資料的單一點查詢。</span><span class="sxs-lookup"><span data-stu-id="15f93-356">[Compound key pattern](#compound-key-pattern) - Use compound **RowKey** values tooenable a client toolookup related data with a single point query.</span></span>  
* <span data-ttu-id="15f93-357">[記錄檔結尾模式](#log-tail-pattern)-擷取 hello  *n* 實體最近加入 tooa 資料分割使用**RowKey**以反向的日期和時間順序排序的值。</span><span class="sxs-lookup"><span data-stu-id="15f93-357">[Log tail pattern](#log-tail-pattern) - Retrieve hello *n* entities most recently added tooa partition by using a **RowKey** value that sorts in reverse date and time order.</span></span>  

## <a name="encrypting-table-data"></a><span data-ttu-id="15f93-358">加密資料表的資料</span><span class="sxs-lookup"><span data-stu-id="15f93-358">Encrypting Table Data</span></span>
<span data-ttu-id="15f93-359">hello.NET Azure 儲存體用戶端程式庫支援加密的字串插入的實體屬性和取代作業。</span><span class="sxs-lookup"><span data-stu-id="15f93-359">hello .NET Azure Storage Client Library supports encryption of string entity properties for insert and replace operations.</span></span> <span data-ttu-id="15f93-360">hello 加密字串 hello 服務上儲存為二進位屬性，而它們會轉換後 toostrings 解密之後。</span><span class="sxs-lookup"><span data-stu-id="15f93-360">hello encrypted strings are stored on hello service as binary properties, and they are converted back toostrings after decryption.</span></span>    

<span data-ttu-id="15f93-361">對於資料表，此外 toohello 加密原則，使用者必須指定 hello 屬性 toobe 加密。</span><span class="sxs-lookup"><span data-stu-id="15f93-361">For tables, in addition toohello encryption policy, users must specify hello properties toobe encrypted.</span></span> <span data-ttu-id="15f93-362">作法是指定 [EncryptProperty] 屬性 (針對衍生自 TableEntity 的 POCO 實體)，或在要求選項中指定加密解析程式。</span><span class="sxs-lookup"><span data-stu-id="15f93-362">This can be done by either specifying an [EncryptProperty] attribute (for POCO entities that derive from TableEntity) or an encryption resolver in request options.</span></span> <span data-ttu-id="15f93-363">加密解析程式是委派，接受資料分割索引鍵、資料列索引鍵和屬性名稱，然後傳回布林值，指出是否應該加密該屬性。</span><span class="sxs-lookup"><span data-stu-id="15f93-363">An encryption resolver is a delegate that takes a partition key, row key, and property name and returns a Boolean that indicates whether that property should be encrypted.</span></span> <span data-ttu-id="15f93-364">在加密期間，是否應該加密屬性，同時寫入 toohello 網路 hello 用戶端程式庫時，會使用此資訊 toodecide。</span><span class="sxs-lookup"><span data-stu-id="15f93-364">During encryption, hello client library will use this information toodecide whether a property should be encrypted while writing toohello wire.</span></span> <span data-ttu-id="15f93-365">hello 委派也提供 hello 可能性的邏輯屬性加密的方式。</span><span class="sxs-lookup"><span data-stu-id="15f93-365">hello delegate also provides for hello possibility of logic around how properties are encrypted.</span></span> <span data-ttu-id="15f93-366">(例如，如果 X，則加密屬性 A，否則加密屬性 A 和 B。)請注意，就是不必要的 tooprovide 讀取或查詢實體時此資訊。</span><span class="sxs-lookup"><span data-stu-id="15f93-366">(For example, if X, then encrypt property A; otherwise encrypt properties A and B.) Note that it is not necessary tooprovide this information while reading or querying entities.</span></span>

<span data-ttu-id="15f93-367">請注意目前不支援合併。</span><span class="sxs-lookup"><span data-stu-id="15f93-367">Note that merge is not currently supported.</span></span> <span data-ttu-id="15f93-368">屬性的子集可能已加密先前使用不同的金鑰，因為只要合併 hello 新內容，並更新 hello 中繼資料會導致資料遺失。</span><span class="sxs-lookup"><span data-stu-id="15f93-368">Since a subset of properties may have been encrypted previously using a different key, simply merging hello new properties and updating hello metadata will result in data loss.</span></span> <span data-ttu-id="15f93-369">合併 需要進行額外的服務從 hello 服務呼叫 tooread hello 預先存在的實體，或使用每個屬性的新機碼，這兩者都不適用基於效能的考量。</span><span class="sxs-lookup"><span data-stu-id="15f93-369">Merging either requires making extra service calls tooread hello pre-existing entity from hello service, or using a new key per property, both of which are not suitable for performance reasons.</span></span>     

<span data-ttu-id="15f93-370">如需加密資料表資料的相關資訊，請參閱 [Microsoft Azure 儲存體的用戶端加密和 Azure 金鑰保存庫](storage-client-side-encryption.md)。</span><span class="sxs-lookup"><span data-stu-id="15f93-370">For information about encrypting table data, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](storage-client-side-encryption.md).</span></span>  

## <a name="modelling-relationships"></a><span data-ttu-id="15f93-371">模型化關聯性</span><span class="sxs-lookup"><span data-stu-id="15f93-371">Modelling relationships</span></span>
<span data-ttu-id="15f93-372">建立網域模型是 hello 設計複雜系統的關鍵步驟。</span><span class="sxs-lookup"><span data-stu-id="15f93-372">Building domain models is a key step in hello design of complex systems.</span></span> <span data-ttu-id="15f93-373">一般而言，使用模型處理程序 tooidentify 實體 hello 和 hello 商務網域 hello 兩者為方法 toounderstand 間的關聯性，並通知 hello 設計您的系統。</span><span class="sxs-lookup"><span data-stu-id="15f93-373">Typically, you use hello modelling process tooidentify entities and hello relationships between them as a way toounderstand hello business domain and inform hello design of your system.</span></span> <span data-ttu-id="15f93-374">本節著重於轉譯 hello hello 表格服務的網域模型 toodesigns 中找到常見關聯性類型。</span><span class="sxs-lookup"><span data-stu-id="15f93-374">This section focuses on how you can translate some of hello common relationship types found in domain models toodesigns for hello Table service.</span></span> <span data-ttu-id="15f93-375">從邏輯資料模型 tooa 實體基礎的 NoSQL 資料模型對應 hello 程序是設計在關聯式資料庫時使用與非常不同。</span><span class="sxs-lookup"><span data-stu-id="15f93-375">hello process of mapping from a logical data-model tooa physical NoSQL based data-model is very different from that used when designing a relational database.</span></span> <span data-ttu-id="15f93-376">關聯式資料庫設計通常會假設資料正規化的程序，針對最小化備援 – 和宣告式的查詢功能的摘要方式 hello 實作 hello 資料庫的運作方式的最佳化。</span><span class="sxs-lookup"><span data-stu-id="15f93-376">Relational databases design typically assumes a data normalization process optimized for minimizing redundancy – and a declarative querying capability that abstracts how hello implementation of how hello database works.</span></span>  

### <a name="one-to-many-relationships"></a><span data-ttu-id="15f93-377">一對多關聯性</span><span class="sxs-lookup"><span data-stu-id="15f93-377">One-to-many relationships</span></span>
<span data-ttu-id="15f93-378">商業網域物件之間常會產生一對多關聯性：例如，一個部門有許多員工。</span><span class="sxs-lookup"><span data-stu-id="15f93-378">One-to-many relationships between business domain objects occur very frequently: for example, one department has many employees.</span></span> <span data-ttu-id="15f93-379">表格服務每個與專業人員和可能相關 toohello 特定案例的優缺點 hello 中有數種方式 tooimplement 一對多關聯性。</span><span class="sxs-lookup"><span data-stu-id="15f93-379">There are several ways tooimplement one-to-many relationships in hello Table service each with pros and cons that may be relevant toohello particular scenario.</span></span>  

<span data-ttu-id="15f93-380">請考慮數以萬計的部門和員工實體，其中每個部門各有許多員工以及每位員工與一個特定部門相關聯的大型多國 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="15f93-380">Consider hello example of a large multi-national corporation with tens of thousands of departments and employee entities where every department has many employees and each employee as associated with one specific department.</span></span> <span data-ttu-id="15f93-381">其中一個方法是 toostore 不同部門 」 和 「 員工實體，這類：</span><span class="sxs-lookup"><span data-stu-id="15f93-381">One approach is toostore separate department and employee entities such as these:</span></span>  

![][1]

<span data-ttu-id="15f93-382">這個範例會示範根據 hello hello 型別之間隱含的一對多關聯性**PartitionKey**值。</span><span class="sxs-lookup"><span data-stu-id="15f93-382">This example shows an implicit one-to-many relationship between hello types based on hello **PartitionKey** value.</span></span> <span data-ttu-id="15f93-383">每個部門可以有許多員工。</span><span class="sxs-lookup"><span data-stu-id="15f93-383">Each department can have many employees.</span></span>  

<span data-ttu-id="15f93-384">此範例也示範 department 實體，並在其相關的員工實體 hello 相同的資料分割。</span><span class="sxs-lookup"><span data-stu-id="15f93-384">This example also shows a department entity and its related employee entities in hello same partition.</span></span> <span data-ttu-id="15f93-385">您可以選擇 toouse 不同資料分割、 資料表或甚至 hello 不同的實體類型的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="15f93-385">You could choose toouse different partitions, tables, or even storage accounts for hello different entity types.</span></span>  

<span data-ttu-id="15f93-386">另一個方法是 toodenormalize 資料與存放區唯一的員工實體未標準化的部門資料 hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="15f93-386">An alternative approach is toodenormalize your data and store only employee entities with denormalized department data as shown in hello following example.</span></span> <span data-ttu-id="15f93-387">在特定案例中，這個反正規化的方法可能無法最佳 hello 如果您需要部門經理需求 toobe 無法 toochange hello 詳細資料，因為 toodo 這需要 tooupdate hello 部門中的每一位員工。</span><span class="sxs-lookup"><span data-stu-id="15f93-387">In this particular scenario, this denormalized approach may not be hello best if you have a requirement toobe able toochange hello details of a department manager because toodo this you need tooupdate every employee in hello department.</span></span>  

![][2]

<span data-ttu-id="15f93-388">如需詳細資訊，請參閱 hello[非正規化模式](#denormalization-pattern)本指南稍後的。</span><span class="sxs-lookup"><span data-stu-id="15f93-388">For more information, see hello [Denormalization pattern](#denormalization-pattern) later in this guide.</span></span>  

<span data-ttu-id="15f93-389">hello 下表摘要說明 hello 優缺點的每個儲存員工和部門有一對多關聯性的實體的上述 hello 方法。</span><span class="sxs-lookup"><span data-stu-id="15f93-389">hello following table summarizes hello pros and cons of each of hello approaches outlined above for storing employee and department entities that have a one-to-many relationship.</span></span> <span data-ttu-id="15f93-390">您也應該考慮您預期的頻率 tooperform 各種作業： 可能是可接受 toohave 包括昂貴的作業，如果該作業只會發生不常的設計。</span><span class="sxs-lookup"><span data-stu-id="15f93-390">You should also consider how often you expect tooperform various operations: it may be acceptable toohave a design that includes an expensive operation if that operation only happens infrequently.</span></span>  

<table>
<tr>
<th><span data-ttu-id="15f93-391">方法</span><span class="sxs-lookup"><span data-stu-id="15f93-391">Approach</span></span></th>
<th><span data-ttu-id="15f93-392">優點</span><span class="sxs-lookup"><span data-stu-id="15f93-392">Pros</span></span></th>
<th><span data-ttu-id="15f93-393">缺點</span><span class="sxs-lookup"><span data-stu-id="15f93-393">Cons</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="15f93-394">個別的實體類型、相同的資料分割、相同的資料表</span><span class="sxs-lookup"><span data-stu-id="15f93-394">Separate entity types, same partition, same table</span></span></td>
<td>
<ul>
<li><span data-ttu-id="15f93-395">您可以使用單一作業更新部門實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-395">You can update a department entity with a single operation.</span></span></li>
<li><span data-ttu-id="15f93-396">如果您有需求 toomodify department 實體，您可以使用 EGT toomaintain 一致性每當您更新/插入/刪除的員工實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-396">You can use an EGT toomaintain consistency if you have a requirement toomodify a department entity whenever you update/insert/delete an employee entity.</span></span> <span data-ttu-id="15f93-397">例如，假設您維護每個部門的部門員工計數。</span><span class="sxs-lookup"><span data-stu-id="15f93-397">For example if you maintain a departmental employee count for each department.</span></span></li>
</ul>
</td>
<td>
<ul>
<li><span data-ttu-id="15f93-398">可能需要 tooretrieve 同時使用 employee 和 department 實體，對於某些用戶端活動。</span><span class="sxs-lookup"><span data-stu-id="15f93-398">You may need tooretrieve both an employee and a department entity for some client activities.</span></span></li>
<li><span data-ttu-id="15f93-399">儲存體作業中發生 hello 相同資料分割。</span><span class="sxs-lookup"><span data-stu-id="15f93-399">Storage operations happen in hello same partition.</span></span> <span data-ttu-id="15f93-400">在交易量偏高時，這可能會導致熱點。</span><span class="sxs-lookup"><span data-stu-id="15f93-400">At high transaction volumes, this may result in a hotspot.</span></span></li>
<li><span data-ttu-id="15f93-401">您無法移動使用 EGT 員工的 tooa 新部門。</span><span class="sxs-lookup"><span data-stu-id="15f93-401">You cannot move an employee tooa new department using an EGT.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="15f93-402">個別的實體類型、不同的資料分割或資料表或儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="15f93-402">Separate entity types, different partitions or tables or storage accounts</span></span></td>
<td>
<ul>
<li><span data-ttu-id="15f93-403">您可以使用單一作業更新部門實體或員工實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-403">You can update a department entity or employee entity with a single operation.</span></span></li>
<li><span data-ttu-id="15f93-404">在大量交易的磁碟區，這可能有助於在多個資料分割之間散佈 hello 負載。</span><span class="sxs-lookup"><span data-stu-id="15f93-404">At high transaction volumes, this may help spread hello load across more partitions.</span></span></li>
</ul>
</td>
<td>
<ul>
<li><span data-ttu-id="15f93-405">可能需要 tooretrieve 同時使用 employee 和 department 實體，對於某些用戶端活動。</span><span class="sxs-lookup"><span data-stu-id="15f93-405">You may need tooretrieve both an employee and a department entity for some client activities.</span></span></li>
<li><span data-ttu-id="15f93-406">您無法使用 EGTs toomaintain 一致性時您更新/插入/刪除員工和更新的部門。</span><span class="sxs-lookup"><span data-stu-id="15f93-406">You cannot use EGTs toomaintain consistency when you update/insert/delete an employee and update a department.</span></span> <span data-ttu-id="15f93-407">例如，更新某個部門實體中的員工計數。</span><span class="sxs-lookup"><span data-stu-id="15f93-407">For example, updating an employee count in a department entity.</span></span></li>
<li><span data-ttu-id="15f93-408">您無法移動使用 EGT 員工的 tooa 新部門。</span><span class="sxs-lookup"><span data-stu-id="15f93-408">You cannot move an employee tooa new department using an EGT.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="15f93-409">去正規化為單一實體類型</span><span class="sxs-lookup"><span data-stu-id="15f93-409">Denormalize into single entity type</span></span></td>
<td>
<ul>
<li><span data-ttu-id="15f93-410">您可以擷取與單一要求所需的所有 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="15f93-410">You can retrieve all hello information you need with a single request.</span></span></li>
</ul>
</td>
<td>
<ul>
<li><span data-ttu-id="15f93-411">如果您需要 tooupdate 部門資訊 （這需要您 tooupdate 所有 hello 員工在部門），可能高度耗費資源的 toomaintain 一致性。</span><span class="sxs-lookup"><span data-stu-id="15f93-411">It may be expensive toomaintain consistency if you need tooupdate department information (this would require you tooupdate all hello employees in a department).</span></span></li>
</ul>
</td>
</tr>
</table>

<span data-ttu-id="15f93-412">如何選擇這些選項，與其中一個 hello 專業人員之間及缺點是最重要的是，取決於特定應用程式案例。</span><span class="sxs-lookup"><span data-stu-id="15f93-412">How you choose between these options, and which of hello pros and cons are most significant, depends on your specific application scenarios.</span></span> <span data-ttu-id="15f93-413">例如，頻率您修改部門實體;您的所有員工查詢都需要 hello 其他部門資訊; 嗎如何關閉是否 toohello 分割區或儲存體帳戶的延展性限制？</span><span class="sxs-lookup"><span data-stu-id="15f93-413">For example, how often do you modify department entities; do all your employee queries need hello additional departmental information; how close are you toohello scalability limits on your partitions or your storage account?</span></span>  

### <a name="one-to-one-relationships"></a><span data-ttu-id="15f93-414">一對一關聯性</span><span class="sxs-lookup"><span data-stu-id="15f93-414">One-to-one relationships</span></span>
<span data-ttu-id="15f93-415">網域模型的實體之間可能會包含一對一關聯性。</span><span class="sxs-lookup"><span data-stu-id="15f93-415">Domain models may include one-to-one relationships between entities.</span></span> <span data-ttu-id="15f93-416">如果您需要 tooimplement hello 表格服務中的一對一關聯性，您也必須選擇在需要時 tooretrieve 這兩個 toolink hello 兩個相關的實體的方式。</span><span class="sxs-lookup"><span data-stu-id="15f93-416">If you need tooimplement a one-to-one relationship in hello Table service, you must also choose how toolink hello two related entities when you need tooretrieve them both.</span></span> <span data-ttu-id="15f93-417">這個連結可以是隱含、 根據慣例，以在 hello 索引鍵值，或明確 hello 形式儲存連結**PartitionKey**和**RowKey**中每個實體 tooits 值相關實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-417">This link can be either implicit, based on a convention in hello key values, or explicit by storing a link in hello form of **PartitionKey** and **RowKey** values in each entity tooits related entity.</span></span> <span data-ttu-id="15f93-418">如需您是否應該儲存 hello 的討論相關實體在 hello 相同的資料分割，請參閱 hello 節[一對多關聯性](#one-to-many-relationships)。</span><span class="sxs-lookup"><span data-stu-id="15f93-418">For a discussion of whether you should store hello related entities in hello same partition, see hello section [One-to-many relationships](#one-to-many-relationships).</span></span>  

<span data-ttu-id="15f93-419">請注意，有也可能會導致您 tooimplement 一對一關聯性中 hello 表格服務的實作考量：</span><span class="sxs-lookup"><span data-stu-id="15f93-419">Note that there are also implementation considerations that might lead you tooimplement one-to-one relationships in hello Table service:</span></span>  

* <span data-ttu-id="15f93-420">處理大型實體 (如需詳細資訊，請參閱 [大型實體模式](#large-entities-pattern))。</span><span class="sxs-lookup"><span data-stu-id="15f93-420">Handling large entities (for more information, see [Large Entities Pattern](#large-entities-pattern)).</span></span>  
* <span data-ttu-id="15f93-421">實作存取控制 (如需詳細資訊，請參閱 [使用共用存取簽章控制存取](#controlling-access-with-shared-access-signatures))。</span><span class="sxs-lookup"><span data-stu-id="15f93-421">Implementing access controls (for more information, see [Controlling access with Shared Access Signatures](#controlling-access-with-shared-access-signatures)).</span></span>  

### <a name="join-in-hello-client"></a><span data-ttu-id="15f93-422">加入在 hello 用戶端</span><span class="sxs-lookup"><span data-stu-id="15f93-422">Join in hello client</span></span>
<span data-ttu-id="15f93-423">雖然 hello 表格服務有方式 toomodel 關聯性，您應該記住 hello 兩個主要的原因 hello 表格服務的使用是延展性和效能。</span><span class="sxs-lookup"><span data-stu-id="15f93-423">Although there are ways toomodel relationships in hello Table service, you should not forget that hello two prime reasons for using hello Table service are scalability and performance.</span></span> <span data-ttu-id="15f93-424">如果您發現模型許多危害 hello 效能和延展性的方案的關聯性，您應該請詢問自己是否必要 toobuild 所有 hello 到資料表設計的資料關聯性。</span><span class="sxs-lookup"><span data-stu-id="15f93-424">If you find you are modelling many relationships that compromise hello performance and scalability of your solution, you should ask yourself if it is necessary toobuild all hello data relationships into your table design.</span></span> <span data-ttu-id="15f93-425">您可能是無法 toosimplify hello 設計，並且改善 hello 延展性和效能的方案，如果您讓用戶端應用程式執行任何必要的聯結。</span><span class="sxs-lookup"><span data-stu-id="15f93-425">You may be able toosimplify hello design and improve hello scalability and performance of your solution if you let your client application perform any necessary joins.</span></span>  

<span data-ttu-id="15f93-426">比方說，如果您有小型的資料表，其中包含不經常變更的資料，然後您可以使用一次擷取這項資料而 hello 用戶端上快取它。</span><span class="sxs-lookup"><span data-stu-id="15f93-426">For example, if you have small tables that contain data that does not change very often, then you can retrieve this data once and cache it on hello client.</span></span> <span data-ttu-id="15f93-427">這樣做可避免重複的往返 tooretrieve hello 相同的資料。</span><span class="sxs-lookup"><span data-stu-id="15f93-427">This can avoid repeated roundtrips tooretrieve hello same data.</span></span> <span data-ttu-id="15f93-428">在 hello 範例中我們已經探討本指南中，hello 組的小型組織中的部門可可能 toobe 小且不常很適合做為用戶端應用程式可以下載一次的資料和快取做為查閱資料的變更。</span><span class="sxs-lookup"><span data-stu-id="15f93-428">In hello examples we have looked at in this guide, hello set of departments in a small organization is likely toobe small and change infrequently making it a good candidate for data that client application can download once and cache as look up data.</span></span>  

### <a name="inheritance-relationships"></a><span data-ttu-id="15f93-429">繼承關聯性</span><span class="sxs-lookup"><span data-stu-id="15f93-429">Inheritance relationships</span></span>
<span data-ttu-id="15f93-430">如果用戶端應用程式使用一組形成部分繼承關聯性 toorepresent 商務實體的類別，您可以輕鬆地保存 hello 表格服務中的這些實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-430">If your client application uses a set of classes that form part of an inheritance relationship toorepresent business entities, you can easily persist those entities in hello Table service.</span></span> <span data-ttu-id="15f93-431">例如，您可能必須遵循一組類別定義在用戶端應用程式中的 hello 其中**人員**是 abstract 類別。</span><span class="sxs-lookup"><span data-stu-id="15f93-431">For example, you might have hello following set of classes defined in your client application where **Person** is an abstract class.</span></span>

![][3]

<span data-ttu-id="15f93-432">您可以保存 hello 兩個實體的類別在 hello 使用單一的 Person 資料表，使用實體中看起來像這樣的表格服務的執行個體：</span><span class="sxs-lookup"><span data-stu-id="15f93-432">You can persist instances of hello two concrete classes in hello Table service using a single Person table using entities in that look like this:</span></span>  

![][4]

<span data-ttu-id="15f93-433">如需使用的 hello 相同用戶端程式碼中的資料表中的多個實體類型的詳細資訊，請參閱 hello 節[使用異質實體類型](#working-with-heterogeneous-entity-types)本指南稍後的。</span><span class="sxs-lookup"><span data-stu-id="15f93-433">For more information about working with multiple entity types in hello same table in client code, see hello section [Working with heterogeneous entity types](#working-with-heterogeneous-entity-types) later in this guide.</span></span> <span data-ttu-id="15f93-434">這會提供如何 toorecognize hello 用戶端程式碼中的實體類型的範例。</span><span class="sxs-lookup"><span data-stu-id="15f93-434">This provides examples of how toorecognize hello entity type in client code.</span></span>  

## <a name="table-design-patterns"></a><span data-ttu-id="15f93-435">資料表設計模式</span><span class="sxs-lookup"><span data-stu-id="15f93-435">Table Design Patterns</span></span>
<span data-ttu-id="15f93-436">在先前章節中，您已經知道某些詳細的討論如何 toooptimize 資料表設計這兩個擷取的實體資料，使用查詢與插入、 更新和刪除實體資料。</span><span class="sxs-lookup"><span data-stu-id="15f93-436">In previous sections, you have seen some detailed discussions about how toooptimize your table design for both retrieving entity data using queries and for inserting, updating, and deleting entity data.</span></span> <span data-ttu-id="15f93-437">本節將說明一些適用於資料表服務方案的模式。</span><span class="sxs-lookup"><span data-stu-id="15f93-437">This section describes some patterns appropriate for use with Table service solutions.</span></span> <span data-ttu-id="15f93-438">此外，您會看到您可以實際上定址方式的一些 hello 問題和缺點引發先前在本指南中。</span><span class="sxs-lookup"><span data-stu-id="15f93-438">In addition, you will see how you can practically address some of hello issues and trade-offs raised previously in this guide.</span></span> <span data-ttu-id="15f93-439">hello 圖摘要說明 hello hello 不同模式之間的關聯性：</span><span class="sxs-lookup"><span data-stu-id="15f93-439">hello following diagram summarizes hello relationships between hello different patterns:</span></span>  

![][5]

<span data-ttu-id="15f93-440">上面的 hello 模式對應反白顯示的某些模式 （藍色） 與本指南中所述的反向模式 （橘色） 之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="15f93-440">hello pattern map above highlights some relationships between patterns (blue) and anti-patterns (orange) that are documented in this guide.</span></span> <span data-ttu-id="15f93-441">當然還有許多其他模式也值得考量。</span><span class="sxs-lookup"><span data-stu-id="15f93-441">There are of course many other patterns that are worth considering.</span></span> <span data-ttu-id="15f93-442">例如，表格服務的 hello 重要案例的其中一個是 toouse hello[具體化檢視模式](https://msdn.microsoft.com/library/azure/dn589782.aspx)從 hello[命令查詢責任隔離 (CQRS)](https://msdn.microsoft.com/library/azure/jj554200.aspx)模式。</span><span class="sxs-lookup"><span data-stu-id="15f93-442">For example, one of hello key scenarios for Table Service is toouse hello [Materialized View Pattern](https://msdn.microsoft.com/library/azure/dn589782.aspx) from hello [Command Query Responsibility Segregation (CQRS)](https://msdn.microsoft.com/library/azure/jj554200.aspx) pattern.</span></span>  

### <a name="intra-partition-secondary-index-pattern"></a><span data-ttu-id="15f93-443">內部資料分割次要索引模式</span><span class="sxs-lookup"><span data-stu-id="15f93-443">Intra-partition secondary index pattern</span></span>
<span data-ttu-id="15f93-444">儲存多個複本的每一個實體使用不同**RowKey**值 (hello 中相同的資料分割) 使用不同的訂單 tooenable 快速又有效率查閱和替代排序**RowKey**值。</span><span class="sxs-lookup"><span data-stu-id="15f93-444">Store multiple copies of each entity using different **RowKey** values (in hello same partition) tooenable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span> <span data-ttu-id="15f93-445">複本之間的更新可以使用 EGT 保持一致。</span><span class="sxs-lookup"><span data-stu-id="15f93-445">Updates between copies can be kept consistent using EGT's.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="15f93-446">內容和問題</span><span class="sxs-lookup"><span data-stu-id="15f93-446">Context and problem</span></span>
<span data-ttu-id="15f93-447">hello 表格服務會自動索引使用 hello 實體**PartitionKey**和**RowKey**值。</span><span class="sxs-lookup"><span data-stu-id="15f93-447">hello Table service automatically indexes entities using hello **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="15f93-448">這可讓用戶端應用程式 tooretrieve 有效率地使用這些值的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-448">This enables a client application tooretrieve an entity efficiently using these values.</span></span> <span data-ttu-id="15f93-449">例如，使用 hello 資料表結構，如下所示，用戶端應用程式可以使用點查詢 tooretrieve 個別員工實體使用 hello 部門名稱和 hello 員工識別碼 (hello **PartitionKey**和**RowKey**值)。</span><span class="sxs-lookup"><span data-stu-id="15f93-449">For example, using hello table structure shown below, a client application can use a point query tooretrieve an individual employee entity by using hello department name and hello employee id (hello **PartitionKey** and **RowKey** values).</span></span> <span data-ttu-id="15f93-450">用戶端也可以擷取每個部門內以員工識別碼排序的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-450">A client can also retrieve entities sorted by employee id within each department.</span></span>

![][6]

<span data-ttu-id="15f93-451">如果您也想 toobe 無法 toofind 根據 hello 另一個屬性值，例如電子郵件地址的員工實體，您必須使用效率較低的資料分割掃描 toofind 相符項目。</span><span class="sxs-lookup"><span data-stu-id="15f93-451">If you also want toobe able toofind an employee entity based on hello value of another property, such as email address, you must use a less efficient partition scan toofind a match.</span></span> <span data-ttu-id="15f93-452">這是因為 hello 表格服務不會提供次要索引。</span><span class="sxs-lookup"><span data-stu-id="15f93-452">This is because hello table service does not provide secondary indexes.</span></span> <span data-ttu-id="15f93-453">此外，沒有任何選項 toorequest 以不同順序排序的員工清單**RowKey**順序。</span><span class="sxs-lookup"><span data-stu-id="15f93-453">In addition, there is no option toorequest a list of employees sorted in a different order than **RowKey** order.</span></span>  

#### <a name="solution"></a><span data-ttu-id="15f93-454">方案</span><span class="sxs-lookup"><span data-stu-id="15f93-454">Solution</span></span>
<span data-ttu-id="15f93-455">toowork 周圍 hello 缺乏次要索引，您可以儲存多個複本的每個實體，以使用不同的每個複本**RowKey**值。</span><span class="sxs-lookup"><span data-stu-id="15f93-455">toowork around hello lack of secondary indexes, you can store multiple copies of each entity with each copy using a different **RowKey** value.</span></span> <span data-ttu-id="15f93-456">如果您儲存實體 hello 結構如下所示，您就可以有效率地擷取根據電子郵件地址或員工識別碼的員工實體。hello hello 的前置詞值**RowKey**，"empid_"和"email_ 」 可讓您 tooquery 一位員工或員工的範圍使用的電子郵件地址或員工識別碼範圍。</span><span class="sxs-lookup"><span data-stu-id="15f93-456">If you store an entity with hello structures shown below, you can efficiently retrieve employee entities based on email address or employee id. hello prefix values for hello **RowKey**, "empid_" and "email_" enable you tooquery for a single employee or a range of employees by using a range of email addresses or employee ids.</span></span>  

![][7]

<span data-ttu-id="15f93-457">下列兩個 （一個查閱的員工識別碼和一個依電子郵件地址查閱） 的篩選準則的 hello 同時指定點查詢：</span><span class="sxs-lookup"><span data-stu-id="15f93-457">hello following two filter criteria (one looking up by employee id and one looking up by email address) both specify point queries:</span></span>  

* <span data-ttu-id="15f93-458">$filter=(PartitionKey eq 'Sales') and (RowKey eq 'empid_000223')</span><span class="sxs-lookup"><span data-stu-id="15f93-458">$filter=(PartitionKey eq 'Sales') and (RowKey eq 'empid_000223')</span></span>  
* <span data-ttu-id="15f93-459">$filter=(PartitionKey eq 'Sales') and (RowKey eq 'email_jonesj@contoso.com')</span><span class="sxs-lookup"><span data-stu-id="15f93-459">$filter=(PartitionKey eq 'Sales') and (RowKey eq 'email_jonesj@contoso.com')</span></span>  

<span data-ttu-id="15f93-460">如果您查詢某一範圍的員工實體，您可以指定範圍依員工識別碼排序或藉由查詢的實體中 hello hello 適當的前置詞以電子郵件地址順序排序的範圍**RowKey**。</span><span class="sxs-lookup"><span data-stu-id="15f93-460">If you query for a range of employee entities, you can specify a range sorted in employee id order, or a range sorted in email address order by querying for entities with hello appropriate prefix in hello **RowKey**.</span></span>  

* <span data-ttu-id="15f93-461">toofind hello 具有所有員工 hello 銷售部門的員工識別碼 hello 範圍 000100 too000199 中都使用： $filter = (PartitionKey eq 'Sales') 與 (RowKey ge 'empid_000100') 和 (RowKey le 'empid_000199')</span><span class="sxs-lookup"><span data-stu-id="15f93-461">toofind all hello employees in hello Sales department with an employee id in hello range 000100 too000199 use: $filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000100') and (RowKey le 'empid_000199')</span></span>  
* <span data-ttu-id="15f93-462">所有電子郵件地址開頭為 hello 與 hello hello 銷售部門的員工 toofind 字母 'a' 的使用： $filter = (PartitionKey eq 'Sales') 與 (RowKey ge 'email_a') 和 (RowKey lt 'email_b')</span><span class="sxs-lookup"><span data-stu-id="15f93-462">toofind all hello employees in hello Sales department with an email address starting with hello letter 'a' use: $filter=(PartitionKey eq 'Sales') and (RowKey ge 'email_a') and (RowKey lt 'email_b')</span></span>  
  
  <span data-ttu-id="15f93-463">請注意，上述的 hello 範例中使用的 hello 篩選語法與 hello 表格服務 REST API 的詳細資訊，請參閱[查詢實體](http://msdn.microsoft.com/library/azure/dd179421.aspx)。</span><span class="sxs-lookup"><span data-stu-id="15f93-463">Note that hello filter syntax used in hello examples above is from hello Table service REST API, for more information see [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="15f93-464">問題和考量</span><span class="sxs-lookup"><span data-stu-id="15f93-464">Issues and considerations</span></span>
<span data-ttu-id="15f93-465">請考慮 hello 時決定下列點如何 tooimplement 這種模式：</span><span class="sxs-lookup"><span data-stu-id="15f93-465">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="15f93-466">資料表儲存體是相對低廉 toouse 因此 hello 成本負擔的儲存重複的資料不應該是主要的考量。</span><span class="sxs-lookup"><span data-stu-id="15f93-466">Table storage is relatively cheap toouse so hello cost overhead of storing duplicate data should not be a major concern.</span></span> <span data-ttu-id="15f93-467">不過，您應該一定會評估 hello 成本您根據您的的儲存需求的設計，並只能新增重複的實體 toosupport hello 查詢將會執行用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="15f93-467">However, you should always evaluate hello cost of your design based on your anticipated storage requirements and only add duplicate entities toosupport hello queries your client application will execute.</span></span>  
* <span data-ttu-id="15f93-468">由於 hello 次要索引的實體儲存在 hello 相同資料分割以 hello 原始實體中，您應確定不會超過 hello 個別的資料分割的延展性目標。</span><span class="sxs-lookup"><span data-stu-id="15f93-468">Because hello secondary index entities are stored in hello same partition as hello original entities, you should ensure that you do not exceed hello scalability targets for an individual partition.</span></span>  
* <span data-ttu-id="15f93-469">您可以將重複的實體彼此一致以不可分割方式使用 EGTs tooupdate hello 兩份 hello 實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-469">You can keep your duplicate entities consistent with each other by using EGTs tooupdate hello two copies of hello entity atomically.</span></span> <span data-ttu-id="15f93-470">這表示，您應該將實體的所有複本都存放在 hello 相同的資料分割。</span><span class="sxs-lookup"><span data-stu-id="15f93-470">This implies that you should store all copies of an entity in hello same partition.</span></span> <span data-ttu-id="15f93-471">如需詳細資訊，請參閱 hello 節[使用實體群組交易](#entity-group-transactions)。</span><span class="sxs-lookup"><span data-stu-id="15f93-471">For more information, see hello section [Using Entity Group Transactions](#entity-group-transactions).</span></span>  
* <span data-ttu-id="15f93-472">hello 值為 hello **RowKey**必須是唯一的每個實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-472">hello value used for hello **RowKey** must be unique for each entity.</span></span> <span data-ttu-id="15f93-473">請考慮使用複合索引鍵值。</span><span class="sxs-lookup"><span data-stu-id="15f93-473">Consider using compound key values.</span></span>  
* <span data-ttu-id="15f93-474">填補數值 hello **RowKey** （例如 hello 員工識別碼 000223），可讓更正排序和篩選依據的上下限之間。</span><span class="sxs-lookup"><span data-stu-id="15f93-474">Padding numeric values in hello **RowKey** (for example, hello employee id 000223), enables correct sorting and filtering based on upper and lower bounds.</span></span>  
* <span data-ttu-id="15f93-475">您不一定需要 tooduplicate 所有 hello 屬性的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-475">You do not necessarily need tooduplicate all hello properties of your entity.</span></span> <span data-ttu-id="15f93-476">例如，如果 hello 查閱 hello 實體使用 hello 電子郵件的查詢以處理 hello **RowKey**永遠都不需要 hello 員工的年齡，這些實體可能會有下列結構的 hello:</span><span class="sxs-lookup"><span data-stu-id="15f93-476">For example, if hello queries that lookup hello entities using hello email address in hello **RowKey** never need hello employee's age, these entities could have hello following structure:</span></span>

![][8]

* <span data-ttu-id="15f93-477">通常更好的 toostore 重複的資料，並確保您可以擷取您需要使用單一查詢的所有 hello 資料，比 toouse 一個查詢 toolocate 實體和另一個 toolookup hello 所需的資料。</span><span class="sxs-lookup"><span data-stu-id="15f93-477">It is typically better toostore duplicate data and ensure that you can retrieve all hello data you need with a single query, than toouse one query toolocate an entity and another toolookup hello required data.</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="15f93-478">當 toouse 此模式</span><span class="sxs-lookup"><span data-stu-id="15f93-478">When toouse this pattern</span></span>
<span data-ttu-id="15f93-479">當用戶端應用程式需要使用各種不同的金鑰，當您的用戶端需要不同排序順序中的 tooretrieve 實體 tooretrieve 實體以及您可以識別每個使用不同的唯一值的實體，請使用此模式。</span><span class="sxs-lookup"><span data-stu-id="15f93-479">Use this pattern when your client application needs tooretrieve entities using a variety of different keys, when your client needs tooretrieve entities in different sort orders, and where you can identify each entity using a variety of unique values.</span></span> <span data-ttu-id="15f93-480">不過，您應該確定您要執行 hello 不同實體查閱時請不要超過 hello 資料分割的延展性限制**RowKey**值。</span><span class="sxs-lookup"><span data-stu-id="15f93-480">However, you should be sure that you do not exceed hello partition scalability limits when you are performing entity lookups using hello different **RowKey** values.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="15f93-481">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="15f93-481">Related patterns and guidance</span></span>
<span data-ttu-id="15f93-482">hello 下列模式和指導方針也可能是相關實作此模式時：</span><span class="sxs-lookup"><span data-stu-id="15f93-482">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="15f93-483">間分割次要索引模式</span><span class="sxs-lookup"><span data-stu-id="15f93-483">Inter-partition secondary index pattern</span></span>](#inter-partition-secondary-index-pattern)
* [<span data-ttu-id="15f93-484">複合索引鍵模式</span><span class="sxs-lookup"><span data-stu-id="15f93-484">Compound key pattern</span></span>](#compound-key-pattern)
* [<span data-ttu-id="15f93-485">實體群組交易</span><span class="sxs-lookup"><span data-stu-id="15f93-485">Entity Group Transactions</span></span>](#entity-group-transactions)
* [<span data-ttu-id="15f93-486">使用異質性實體類型</span><span class="sxs-lookup"><span data-stu-id="15f93-486">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)

### <a name="inter-partition-secondary-index-pattern"></a><span data-ttu-id="15f93-487">間資料分割次要索引模式</span><span class="sxs-lookup"><span data-stu-id="15f93-487">Inter-partition secondary index pattern</span></span>
<span data-ttu-id="15f93-488">儲存多個複本的每一個實體使用不同**RowKey**值不同的磁碟分割或個別資料表 tooenable 快速又有效率查閱，以及使用不同的替代排序次序**RowKey**值。</span><span class="sxs-lookup"><span data-stu-id="15f93-488">Store multiple copies of each entity using different **RowKey** values in separate partitions or in separate tables tooenable fast and efficient lookups and alternate sort orders by using different **RowKey** values.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="15f93-489">內容和問題</span><span class="sxs-lookup"><span data-stu-id="15f93-489">Context and problem</span></span>
<span data-ttu-id="15f93-490">hello 表格服務會自動索引使用 hello 實體**PartitionKey**和**RowKey**值。</span><span class="sxs-lookup"><span data-stu-id="15f93-490">hello Table service automatically indexes entities using hello **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="15f93-491">這可讓用戶端應用程式 tooretrieve 有效率地使用這些值的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-491">This enables a client application tooretrieve an entity efficiently using these values.</span></span> <span data-ttu-id="15f93-492">例如，使用 hello 資料表結構，如下所示，用戶端應用程式可以使用點查詢 tooretrieve 個別員工實體使用 hello 部門名稱和 hello 員工識別碼 (hello **PartitionKey**和**RowKey**值)。</span><span class="sxs-lookup"><span data-stu-id="15f93-492">For example, using hello table structure shown below, a client application can use a point query tooretrieve an individual employee entity by using hello department name and hello employee id (hello **PartitionKey** and **RowKey** values).</span></span> <span data-ttu-id="15f93-493">用戶端也可以擷取每個部門內以員工識別碼排序的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-493">A client can also retrieve entities sorted by employee id within each department.</span></span>  

![][9]

<span data-ttu-id="15f93-494">如果您也想 toobe 無法 toofind 根據 hello 另一個屬性值，例如電子郵件地址的員工實體，您必須使用效率較低的資料分割掃描 toofind 相符項目。</span><span class="sxs-lookup"><span data-stu-id="15f93-494">If you also want toobe able toofind an employee entity based on hello value of another property, such as email address, you must use a less efficient partition scan toofind a match.</span></span> <span data-ttu-id="15f93-495">這是因為 hello 表格服務不會提供次要索引。</span><span class="sxs-lookup"><span data-stu-id="15f93-495">This is because hello table service does not provide secondary indexes.</span></span> <span data-ttu-id="15f93-496">此外，沒有任何選項 toorequest 以不同順序排序的員工清單**RowKey**順序。</span><span class="sxs-lookup"><span data-stu-id="15f93-496">In addition, there is no option toorequest a list of employees sorted in a different order than **RowKey** order.</span></span>  

<span data-ttu-id="15f93-497">您會預期極大量的交易，針對這些實體，而且想 toominimize hello 風險的 hello 節流設定您的用戶端的表格服務。</span><span class="sxs-lookup"><span data-stu-id="15f93-497">You are anticipating a very high volume of transactions against these entities and want toominimize hello risk of hello Table service throttling your client.</span></span>  

#### <a name="solution"></a><span data-ttu-id="15f93-498">方案</span><span class="sxs-lookup"><span data-stu-id="15f93-498">Solution</span></span>
<span data-ttu-id="15f93-499">toowork 周圍 hello 缺乏次要索引，您可以儲存多個複本的每個實體，每個複本使用不同**PartitionKey**和**RowKey**值。</span><span class="sxs-lookup"><span data-stu-id="15f93-499">toowork around hello lack of secondary indexes, you can store multiple copies of each entity with each copy using different **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="15f93-500">如果您儲存實體 hello 結構如下所示，您就可以有效率地擷取根據電子郵件地址或員工識別碼的員工實體。hello hello 的前置詞值**PartitionKey**，"empid_"和"email_ 」 可讓您 tooidentify 索引您要查詢 toouse。</span><span class="sxs-lookup"><span data-stu-id="15f93-500">If you store an entity with hello structures shown below, you can efficiently retrieve employee entities based on email address or employee id. hello prefix values for hello **PartitionKey**, "empid_" and "email_" enable you tooidentify which index you want toouse for a query.</span></span>  

![][10]

<span data-ttu-id="15f93-501">下列兩個 （一個查閱的員工識別碼和一個依電子郵件地址查閱） 的篩選準則的 hello 同時指定點查詢：</span><span class="sxs-lookup"><span data-stu-id="15f93-501">hello following two filter criteria (one looking up by employee id and one looking up by email address) both specify point queries:</span></span>  

* <span data-ttu-id="15f93-502">$filter=(PartitionKey eq 'empid_Sales') and (RowKey eq '000223')</span><span class="sxs-lookup"><span data-stu-id="15f93-502">$filter=(PartitionKey eq 'empid_Sales') and (RowKey eq '000223')</span></span>
* <span data-ttu-id="15f93-503">$filter=(PartitionKey eq 'email_Sales') and (RowKey eq 'jonesj@contoso.com')</span><span class="sxs-lookup"><span data-stu-id="15f93-503">$filter=(PartitionKey eq 'email_Sales') and (RowKey eq 'jonesj@contoso.com')</span></span>  

<span data-ttu-id="15f93-504">如果您查詢某一範圍的員工實體，您可以指定範圍依員工識別碼排序或藉由查詢的實體中 hello hello 適當的前置詞以電子郵件地址順序排序的範圍**RowKey**。</span><span class="sxs-lookup"><span data-stu-id="15f93-504">If you query for a range of employee entities, you can specify a range sorted in employee id order, or a range sorted in email address order by querying for entities with hello appropriate prefix in hello **RowKey**.</span></span>  

* <span data-ttu-id="15f93-505">所有 hello 中的員工的 toofind hello 與員工識別碼 hello 範圍中的銷售部門**000100**太**000199**依照員工識別碼順序使用： $filter = (PartitionKey eq ' empid_Sales') 和 (RowKey ge '000100') 和 (RowKey le '000199')</span><span class="sxs-lookup"><span data-stu-id="15f93-505">toofind all hello employees in hello Sales department with an employee id in hello range **000100** too**000199** sorted in employee id order use: $filter=(PartitionKey eq 'empid_Sales') and (RowKey ge '000100') and (RowKey le '000199')</span></span>  
* <span data-ttu-id="15f93-506">toofind hello 開頭為 'a' 以電子郵件地址的銷售部門的所有 hello 員工電子都郵件地址順序使用： $filter = (PartitionKey eq ' email_Sales') 和 (RowKey ge 'a') 和 (RowKey lt 'b')</span><span class="sxs-lookup"><span data-stu-id="15f93-506">toofind all hello employees in hello Sales department with an email address that starts with 'a' sorted in email address order use: $filter=(PartitionKey eq 'email_Sales') and (RowKey ge 'a') and (RowKey lt 'b')</span></span>  

<span data-ttu-id="15f93-507">請注意，上述的 hello 範例中使用的 hello 篩選語法與 hello 表格服務 REST API 的詳細資訊，請參閱[查詢實體](http://msdn.microsoft.com/library/azure/dd179421.aspx)。</span><span class="sxs-lookup"><span data-stu-id="15f93-507">Note that hello filter syntax used in hello examples above is from hello Table service REST API, for more information see [Query Entities](http://msdn.microsoft.com/library/azure/dd179421.aspx).</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="15f93-508">問題和考量</span><span class="sxs-lookup"><span data-stu-id="15f93-508">Issues and considerations</span></span>
<span data-ttu-id="15f93-509">請考慮 hello 時決定下列點如何 tooimplement 這種模式：</span><span class="sxs-lookup"><span data-stu-id="15f93-509">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="15f93-510">您可以保留重複的實體彼此最終一致使用 hello[最終保持一致的交易模式](#eventually-consistent-transactions-pattern)toomaintain hello 主要和次要索引實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-510">You can keep your duplicate entities eventually consistent with each other by using hello [Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) toomaintain hello primary and secondary index entities.</span></span>  
* <span data-ttu-id="15f93-511">資料表儲存體是相對低廉 toouse 因此 hello 成本負擔的儲存重複的資料不應該是主要的考量。</span><span class="sxs-lookup"><span data-stu-id="15f93-511">Table storage is relatively cheap toouse so hello cost overhead of storing duplicate data should not be a major concern.</span></span> <span data-ttu-id="15f93-512">不過，您應該一定會評估 hello 成本您根據您的的儲存需求的設計，並只能新增重複的實體 toosupport hello 查詢將會執行用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="15f93-512">However, you should always evaluate hello cost of your design based on your anticipated storage requirements and only add duplicate entities toosupport hello queries your client application will execute.</span></span>  
* <span data-ttu-id="15f93-513">hello 值為 hello **RowKey**必須是唯一的每個實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-513">hello value used for hello **RowKey** must be unique for each entity.</span></span> <span data-ttu-id="15f93-514">請考慮使用複合索引鍵值。</span><span class="sxs-lookup"><span data-stu-id="15f93-514">Consider using compound key values.</span></span>  
* <span data-ttu-id="15f93-515">填補數值 hello **RowKey** （例如 hello 員工識別碼 000223），可讓更正排序和篩選依據的上下限之間。</span><span class="sxs-lookup"><span data-stu-id="15f93-515">Padding numeric values in hello **RowKey** (for example, hello employee id 000223), enables correct sorting and filtering based on upper and lower bounds.</span></span>  
* <span data-ttu-id="15f93-516">您不一定需要 tooduplicate 所有 hello 屬性的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-516">You do not necessarily need tooduplicate all hello properties of your entity.</span></span> <span data-ttu-id="15f93-517">例如，如果 hello 查閱 hello 實體使用 hello 電子郵件的查詢以處理 hello **RowKey**永遠都不需要 hello 員工的年齡，這些實體可能會有下列結構的 hello:</span><span class="sxs-lookup"><span data-stu-id="15f93-517">For example, if hello queries that lookup hello entities using hello email address in hello **RowKey** never need hello employee's age, these entities could have hello following structure:</span></span>
  
  ![][11]
* <span data-ttu-id="15f93-518">這是通常較佳的 toostore 重複的資料，並確認您可以擷取非實體使用 toouse 一個查詢 toolocate hello 次要索引，您必須使用單一查詢的所有 hello 資料，而且另一個 toolookup hello hello 主索引中的必要的資料。</span><span class="sxs-lookup"><span data-stu-id="15f93-518">It is typically better toostore duplicate data and ensure that you can retrieve all hello data you need with a single query than toouse one query toolocate an entity using hello secondary index and another toolookup hello required data in hello primary index.</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="15f93-519">當 toouse 此模式</span><span class="sxs-lookup"><span data-stu-id="15f93-519">When toouse this pattern</span></span>
<span data-ttu-id="15f93-520">當用戶端應用程式需要使用各種不同的金鑰，當您的用戶端需要不同排序順序中的 tooretrieve 實體 tooretrieve 實體以及您可以識別每個使用不同的唯一值的實體，請使用此模式。</span><span class="sxs-lookup"><span data-stu-id="15f93-520">Use this pattern when your client application needs tooretrieve entities using a variety of different keys, when your client needs tooretrieve entities in different sort orders, and where you can identify each entity using a variety of unique values.</span></span> <span data-ttu-id="15f93-521">使用此模式，當您想要執行 hello 不同實體查閱時超過 hello 資料分割的延展性限制 tooavoid **RowKey**值。</span><span class="sxs-lookup"><span data-stu-id="15f93-521">Use this pattern when you want tooavoid exceeding hello partition scalability limits when you are performing entity lookups using hello different **RowKey** values.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="15f93-522">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="15f93-522">Related patterns and guidance</span></span>
<span data-ttu-id="15f93-523">hello 下列模式和指導方針也可能是相關實作此模式時：</span><span class="sxs-lookup"><span data-stu-id="15f93-523">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="15f93-524">最終一致的交易模式</span><span class="sxs-lookup"><span data-stu-id="15f93-524">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  
* [<span data-ttu-id="15f93-525">內部資料分割次要索引模式</span><span class="sxs-lookup"><span data-stu-id="15f93-525">Intra-partition secondary index pattern</span></span>](#intra-partition-secondary-index-pattern)  
* [<span data-ttu-id="15f93-526">複合索引鍵模式</span><span class="sxs-lookup"><span data-stu-id="15f93-526">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="15f93-527">實體群組交易</span><span class="sxs-lookup"><span data-stu-id="15f93-527">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="15f93-528">使用異質性實體類型</span><span class="sxs-lookup"><span data-stu-id="15f93-528">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  

### <a name="eventually-consistent-transactions-pattern"></a><span data-ttu-id="15f93-529">最終一致的交易模式</span><span class="sxs-lookup"><span data-stu-id="15f93-529">Eventually consistent transactions pattern</span></span>
<span data-ttu-id="15f93-530">使用 Azure 佇列，跨資料分割界限或儲存體系統界限啟用最終一致的行為。</span><span class="sxs-lookup"><span data-stu-id="15f93-530">Enable eventually consistent behavior across partition boundaries or storage system boundaries by using Azure queues.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="15f93-531">內容和問題</span><span class="sxs-lookup"><span data-stu-id="15f93-531">Context and problem</span></span>
<span data-ttu-id="15f93-532">EGTs 跨多個實體以共用 hello 啟用不可部分完成的交易相同的資料分割索引鍵。</span><span class="sxs-lookup"><span data-stu-id="15f93-532">EGTs enable atomic transactions across multiple entities that share hello same partition key.</span></span> <span data-ttu-id="15f93-533">效能和延展性的原因，您可能會決定 toostore 實體具有一致性需求，在不同的磁碟分割或不同的儲存體系統中： 在此案例中，您無法使用 EGTs toomaintain 一致性。</span><span class="sxs-lookup"><span data-stu-id="15f93-533">For performance and scalability reasons, you might decide toostore entities that have consistency requirements in separate partitions or in a separate storage system: in such a scenario, you cannot use EGTs toomaintain consistency.</span></span> <span data-ttu-id="15f93-534">例如，您可能必須之間的需求 toomaintain 最終一致性：</span><span class="sxs-lookup"><span data-stu-id="15f93-534">For example, you might have a requirement toomaintain eventual consistency between:</span></span>  

* <span data-ttu-id="15f93-535">儲存在相同的資料表，在不同的資料表中不同的儲存體帳戶中的 hello 中兩個不同的資料分割的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-535">Entities stored in two different partitions in hello same table, in different tables, in in different storage accounts.</span></span>  
* <span data-ttu-id="15f93-536">Blob 儲存在 Blob 服務的 hello 而且儲存在 hello 表格服務中的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-536">An entity stored in hello Table service and a blob stored in hello Blob service.</span></span>  
* <span data-ttu-id="15f93-537">實體檔案系統中儲存在 hello 表格服務和檔案。</span><span class="sxs-lookup"><span data-stu-id="15f93-537">An entity stored in hello Table service and a file in a file system.</span></span>  
* <span data-ttu-id="15f93-538">實體在 hello 表格服務中儲存，但使用 hello Azure 搜尋服務編製索引。</span><span class="sxs-lookup"><span data-stu-id="15f93-538">An entity store in hello Table service yet indexed using hello Azure Search service.</span></span>  

#### <a name="solution"></a><span data-ttu-id="15f93-539">方案</span><span class="sxs-lookup"><span data-stu-id="15f93-539">Solution</span></span>
<span data-ttu-id="15f93-540">藉由使用 Azure 佇列，您可以實作解決方案，提供跨兩個或多個資料分割或儲存系統的最終一致性。</span><span class="sxs-lookup"><span data-stu-id="15f93-540">By using Azure queues, you can implement a solution that delivers eventual consistency across two or more partitions or storage systems.</span></span>
<span data-ttu-id="15f93-541">這個方法 tooillustrate，假設您有需求 toobe 無法 tooarchive 舊員工實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-541">tooillustrate this approach, assume you have a requirement toobe able tooarchive old employee entities.</span></span> <span data-ttu-id="15f93-542">舊的員工實體很少受到查詢，應從處理目前員工的任何活動中排除。</span><span class="sxs-lookup"><span data-stu-id="15f93-542">Old employee entities are rarely queried and should be excluded from any activities that deal with current employees.</span></span> <span data-ttu-id="15f93-543">tooimplement 在職員工存放 hello 這項需求**目前**資料表和舊的員工的 hello**封存**資料表。</span><span class="sxs-lookup"><span data-stu-id="15f93-543">tooimplement this requirement you store active employees in hello **Current** table and old employees in hello **Archive** table.</span></span> <span data-ttu-id="15f93-544">封存員工會要求您從 hello toodelete hello 實體**目前**資料表，並新增 hello 實體 toohello**封存**資料表，但是您無法使用 EGT tooperform 這兩項操作。</span><span class="sxs-lookup"><span data-stu-id="15f93-544">Archiving an employee requires you toodelete hello entity from hello **Current** table and add hello entity toohello **Archive** table, but you cannot use an EGT tooperform these two operations.</span></span> <span data-ttu-id="15f93-545">tooavoid 失敗會導致實體 tooappear，這兩個或兩資料表中的 hello 風險，hello 保存作業必須是最終保持一致。</span><span class="sxs-lookup"><span data-stu-id="15f93-545">tooavoid hello risk that a failure causes an entity tooappear in both or neither tables, hello archive operation must be eventually consistent.</span></span> <span data-ttu-id="15f93-546">hello 順序圖概述此作業中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="15f93-546">hello following sequence diagram outlines hello steps in this operation.</span></span> <span data-ttu-id="15f93-547">例外狀況的路徑中的 hello 文字後面提供更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="15f93-547">More detail is provided for exception paths in hello text following.</span></span>  

![][12]

<span data-ttu-id="15f93-548">用戶端會將訊息放在 Azure 佇列，在此範例 tooarchive 員工 #456 起始 hello 封存作業。</span><span class="sxs-lookup"><span data-stu-id="15f93-548">A client initiates hello archive operation by placing a message on an Azure queue, in this example tooarchive employee #456.</span></span> <span data-ttu-id="15f93-549">背景工作角色輪詢 hello 佇列的新訊息。發現，它會讀取 hello 訊息，並會隱藏的複本保留 hello 佇列上。</span><span class="sxs-lookup"><span data-stu-id="15f93-549">A worker role polls hello queue for new messages; when it finds one, it reads hello message and leaves a hidden copy on hello queue.</span></span> <span data-ttu-id="15f93-550">hello 背景工作角色旁的 hello 實體複本會從提取 hello**目前**資料表中，將複本插入 hello**封存**資料表，然後按一下 刪除 hello hello 從原始**目前**資料表。</span><span class="sxs-lookup"><span data-stu-id="15f93-550">hello worker role next fetches a copy of hello entity from hello **Current** table, inserts a copy in hello **Archive** table, and then deletes hello original from hello **Current** table.</span></span> <span data-ttu-id="15f93-551">最後，如果沒有任何錯誤 hello 先前步驟中的，hello 背景工作角色會從 hello 佇列刪除 hello 隱藏的訊息。</span><span class="sxs-lookup"><span data-stu-id="15f93-551">Finally, if there were no errors from hello previous steps, hello worker role deletes hello hidden message from hello queue.</span></span>  

<span data-ttu-id="15f93-552">在此範例中，步驟 4 中插入 hello 員工 hello**封存**資料表。</span><span class="sxs-lookup"><span data-stu-id="15f93-552">In this example, step 4 inserts hello employee into hello **Archive** table.</span></span> <span data-ttu-id="15f93-553">它可以在檔案系統中新增 hello Blob 服務中的 hello 員工 tooa blob 或檔案。</span><span class="sxs-lookup"><span data-stu-id="15f93-553">It could add hello employee tooa blob in hello Blob service or a file in a file system.</span></span>  

#### <a name="recovering-from-failures"></a><span data-ttu-id="15f93-554">從失敗復原</span><span class="sxs-lookup"><span data-stu-id="15f93-554">Recovering from failures</span></span>
<span data-ttu-id="15f93-555">很重要的 hello 中步驟的作業**4**和**5**必須*等冪*當 hello 背景工作角色需要 toorestart hello 封存作業。</span><span class="sxs-lookup"><span data-stu-id="15f93-555">It is important that hello operations in steps **4** and **5** must be *idempotent* in case hello worker role needs toorestart hello archive operation.</span></span> <span data-ttu-id="15f93-556">如果您使用 hello 表格服務，如步驟**4**您應該使用 「 插入或取代 」 作業; 步驟**5**應該使用 「 如果刪除存在"hello 您使用的用戶端程式庫中的作業。</span><span class="sxs-lookup"><span data-stu-id="15f93-556">If you are using hello Table service, for step **4** you should use an "insert or replace" operation; for step **5** you should use a "delete if exists" operation in hello client library you are using.</span></span> <span data-ttu-id="15f93-557">如果您使用其他儲存體系統，您必須使用適當的冪等作業。</span><span class="sxs-lookup"><span data-stu-id="15f93-557">If you are using another storage system, you must use an appropriate idempotent operation.</span></span>  

<span data-ttu-id="15f93-558">如果 hello 背景工作角色一直沒有完成步驟**6**，然後將逾時 hello 訊息會重新出現在 hello 佇列之後隨時可供 hello 背景工作角色 tootry tooreprocess 它。</span><span class="sxs-lookup"><span data-stu-id="15f93-558">If hello worker role never completes step **6**, then after a timeout hello message reappears on hello queue ready for hello worker role tootry tooreprocess it.</span></span> <span data-ttu-id="15f93-559">hello 背景工作角色可以檢查 hello 佇列的訊息已讀取的次數，而且，如果有必要，請傳送 tooa 是 「 滯礙 」 訊息以便調查的旗標來區隔佇列。</span><span class="sxs-lookup"><span data-stu-id="15f93-559">hello worker role can check how many times a message on hello queue has been read and, if necessary, flag it is a "poison" message for investigation by sending it tooa separate queue.</span></span> <span data-ttu-id="15f93-560">如需有關讀取訊息排入佇列，並檢查 hello 清除佇列計數，請參閱[Get Messages](https://msdn.microsoft.com/library/azure/dd179474.aspx)。</span><span class="sxs-lookup"><span data-stu-id="15f93-560">For more information about reading queue messages and checking hello dequeue count, see [Get Messages](https://msdn.microsoft.com/library/azure/dd179474.aspx).</span></span>  

<span data-ttu-id="15f93-561">從資料表和佇列服務的 hello 有些錯誤是暫時性的錯誤，和用戶端應用程式應包含適當的重試邏輯 toohandle 它們。</span><span class="sxs-lookup"><span data-stu-id="15f93-561">Some errors from hello Table and Queue services are transient errors, and your client application should include suitable retry logic toohandle them.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="15f93-562">問題和考量</span><span class="sxs-lookup"><span data-stu-id="15f93-562">Issues and considerations</span></span>
<span data-ttu-id="15f93-563">請考慮 hello 時決定下列點如何 tooimplement 這種模式：</span><span class="sxs-lookup"><span data-stu-id="15f93-563">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="15f93-564">此方案不提供交易隔離。</span><span class="sxs-lookup"><span data-stu-id="15f93-564">This solution does not provide for transaction isolation.</span></span> <span data-ttu-id="15f93-565">比方說，用戶端無法讀取 hello**目前**和**封存**資料表 hello 背景工作角色的時間步驟之間**4**和**5**，並請參閱hello 資料不一致檢視。</span><span class="sxs-lookup"><span data-stu-id="15f93-565">For example, a client could read hello **Current** and **Archive** tables when hello worker role was between steps **4** and **5**, and see an inconsistent view of hello data.</span></span> <span data-ttu-id="15f93-566">請注意，hello 資料能維持一致最後。</span><span class="sxs-lookup"><span data-stu-id="15f93-566">Note that hello data will be consistent eventually.</span></span>  
* <span data-ttu-id="15f93-567">您必須確定步驟 4 和 5 會在順序 tooensure 最終一致性等冪。</span><span class="sxs-lookup"><span data-stu-id="15f93-567">You must be sure that steps 4 and 5 are idempotent in order tooensure eventual consistency.</span></span>  
* <span data-ttu-id="15f93-568">您可以藉由使用多個佇列和背景工作角色執行個體調整 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="15f93-568">You can scale hello solution by using multiple queues and worker role instances.</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="15f93-569">當 toouse 此模式</span><span class="sxs-lookup"><span data-stu-id="15f93-569">When toouse this pattern</span></span>
<span data-ttu-id="15f93-570">當您想 tooguarantee 存在於不同的磁碟分割或資料表中的實體之間的最終一致性時，請使用此模式。</span><span class="sxs-lookup"><span data-stu-id="15f93-570">Use this pattern when you want tooguarantee eventual consistency between entities that exist in different partitions or tables.</span></span> <span data-ttu-id="15f93-571">您可以延伸 hello 表格服務以及 hello Blob 服務和其他非 Azure 儲存體資料來源，例如資料庫或 hello 檔案系統作業此模式 tooensure 最終一致性。</span><span class="sxs-lookup"><span data-stu-id="15f93-571">You can extend this pattern tooensure eventual consistency for operations across hello Table service and hello Blob service and other non-Azure Storage data sources such as database or hello file system.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="15f93-572">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="15f93-572">Related patterns and guidance</span></span>
<span data-ttu-id="15f93-573">hello 下列模式和指導方針也可能是相關實作此模式時：</span><span class="sxs-lookup"><span data-stu-id="15f93-573">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="15f93-574">實體群組交易</span><span class="sxs-lookup"><span data-stu-id="15f93-574">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="15f93-575">合併或取代</span><span class="sxs-lookup"><span data-stu-id="15f93-575">Merge or replace</span></span>](#merge-or-replace)  

> [!NOTE]
> <span data-ttu-id="15f93-576">如果交易隔離是重要的 tooyour 解決方案，您應該考慮重新設計資料表 tooenable 您 toouse EGTs。</span><span class="sxs-lookup"><span data-stu-id="15f93-576">If transaction isolation is important tooyour solution, you should consider redesigning your tables tooenable you toouse EGTs.</span></span>  
> 
> 

### <a name="index-entities-pattern"></a><span data-ttu-id="15f93-577">索引實體模式</span><span class="sxs-lookup"><span data-stu-id="15f93-577">Index Entities Pattern</span></span>
<span data-ttu-id="15f93-578">維護索引實體 tooenable 有效率的搜尋傳回的實體清單。</span><span class="sxs-lookup"><span data-stu-id="15f93-578">Maintain index entities tooenable efficient searches that return lists of entities.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="15f93-579">內容和問題</span><span class="sxs-lookup"><span data-stu-id="15f93-579">Context and problem</span></span>
<span data-ttu-id="15f93-580">hello 表格服務會自動索引使用 hello 實體**PartitionKey**和**RowKey**值。</span><span class="sxs-lookup"><span data-stu-id="15f93-580">hello Table service automatically indexes entities using hello **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="15f93-581">這可讓用戶端應用程式 tooretrieve 有效率地使用點查詢的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-581">This enables a client application tooretrieve an entity efficiently using a point query.</span></span> <span data-ttu-id="15f93-582">例如，使用 hello 資料表結構，如下所示，用戶端應用程式可以有效率地擷取個別員工實體使用 hello 部門名稱和 hello 員工識別碼 (hello **PartitionKey**和**RowKey**).</span><span class="sxs-lookup"><span data-stu-id="15f93-582">For example, using hello table structure shown below, a client application can efficiently retrieve an individual employee entity by using hello department name and hello employee id (hello **PartitionKey** and **RowKey**).</span></span>  

![][13]

<span data-ttu-id="15f93-583">如果您也想 toobe 無法 tooretrieve 員工實體的清單會根據 hello 另一個非唯一屬性值，例如其最後一個名稱，您必須使用效率較低的資料分割掃描 toofind 相符項目，而不是使用索引 toolook 它們直接啟動。</span><span class="sxs-lookup"><span data-stu-id="15f93-583">If you also want toobe able tooretrieve a list of employee entities based on hello value of another non-unique property, such as their last name, you must use a less efficient partition scan toofind matches rather than using an index toolook them up directly.</span></span> <span data-ttu-id="15f93-584">這是因為 hello 表格服務不會提供次要索引。</span><span class="sxs-lookup"><span data-stu-id="15f93-584">This is because hello table service does not provide secondary indexes.</span></span>  

#### <a name="solution"></a><span data-ttu-id="15f93-585">方案</span><span class="sxs-lookup"><span data-stu-id="15f93-585">Solution</span></span>
<span data-ttu-id="15f93-586">依姓氏與 hello 實體結構，如上所示，您必須維護的員工識別碼清單的 tooenable 查閱。</span><span class="sxs-lookup"><span data-stu-id="15f93-586">tooenable lookup by last name with hello entity structure shown above, you must maintain lists of employee ids.</span></span> <span data-ttu-id="15f93-587">如果您想 tooretrieve hello 員工實體具有特定的最後一個名稱，例如 Jones，您必須先找出 Jones 做為其最後一個名稱，與員工的員工識別碼 hello 清單，然後再擷取這些員工實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-587">If you want tooretrieve hello employee entities with a particular last name, such as Jones, you must first locate hello list of employee ids for employees with Jones as their last name, and then retrieve those employee entities.</span></span> <span data-ttu-id="15f93-588">有三個主要的選項，可儲存的員工識別碼 hello 清單：</span><span class="sxs-lookup"><span data-stu-id="15f93-588">There are three main options for storing hello lists of employee ids:</span></span>  

* <span data-ttu-id="15f93-589">使用 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="15f93-589">Use blob storage.</span></span>  
* <span data-ttu-id="15f93-590">索引中建立實體 hello 相同資料分割以 hello 員工實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-590">Create index entities in hello same partition as hello employee entities.</span></span>  
* <span data-ttu-id="15f93-591">在個別的資料分割或資料表中建立索引實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-591">Create index entities in a separate partition or table.</span></span>  

<span data-ttu-id="15f93-592"><u>選項 1：使用 Blob 儲存體</u></span><span class="sxs-lookup"><span data-stu-id="15f93-592"><u>Option #1: Use blob storage</u></span></span>  

<span data-ttu-id="15f93-593">Hello 第一個選項，您建立的每個唯一的姓氏，以及每個 blob 存放區中的 blob 清單的 hello **PartitionKey** （部門） 和**RowKey** （員工識別碼），最後，在員工的值名稱。</span><span class="sxs-lookup"><span data-stu-id="15f93-593">For hello first option, you create a blob for every unique last name, and in each blob store a list of hello **PartitionKey** (department) and **RowKey** (employee id) values for employees that have that last name.</span></span> <span data-ttu-id="15f93-594">當您新增或刪除員工就應該確保 hello 相關 blob hello 內容是最終與 hello 員工實體保持一致。</span><span class="sxs-lookup"><span data-stu-id="15f93-594">When you add or delete an employee you should ensure that hello content of hello relevant blob is eventually consistent with hello employee entities.</span></span>  

<span data-ttu-id="15f93-595"><u>選項 2:</u>中的建立索引實體 hello 相同的資料分割</span><span class="sxs-lookup"><span data-stu-id="15f93-595"><u>Option #2:</u> Create index entities in hello same partition</span></span>  

<span data-ttu-id="15f93-596">Hello 第二個選項，使用索引的實體儲存 hello 下列資料：</span><span class="sxs-lookup"><span data-stu-id="15f93-596">For hello second option, use index entities that store hello following data:</span></span>  

![][14]

<span data-ttu-id="15f93-597">hello **EmployeeIDs**屬性包含員工的員工識別碼的清單，hello 最後一個名稱儲存在 hello **RowKey**。</span><span class="sxs-lookup"><span data-stu-id="15f93-597">hello **EmployeeIDs** property contains a list of employee ids for employees with hello last name stored in hello **RowKey**.</span></span>  

<span data-ttu-id="15f93-598">hello 下列步驟概述您要加入新的員工，如果您使用 hello 第二個選項時所應遵循的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="15f93-598">hello following steps outline hello process you should follow when you are adding a new employee if you are using hello second option.</span></span> <span data-ttu-id="15f93-599">在此範例中，我們新增識別碼 000152 且最後一個名稱 Jones hello 銷售部門的員工：</span><span class="sxs-lookup"><span data-stu-id="15f93-599">In this example, we are adding an employee with Id 000152 and a last name Jones in hello Sales department:</span></span>  

1. <span data-ttu-id="15f93-600">擷取與 hello 索引實體**PartitionKey**實值 「 銷售 」 與 hello **RowKey**值"Jones。 」</span><span class="sxs-lookup"><span data-stu-id="15f93-600">Retrieve hello index entity with a **PartitionKey** value "Sales" and hello **RowKey** value "Jones."</span></span> <span data-ttu-id="15f93-601">儲存在步驟 2 中的 hello 這個實體 toouse 的 ETag。</span><span class="sxs-lookup"><span data-stu-id="15f93-601">Save hello ETag of this entity toouse in step 2.</span></span>  
2. <span data-ttu-id="15f93-602">建立實體群組交易 （也就是說，批次作業），將新員工實體 hello (**PartitionKey**值 「 銷售 」 和**RowKey**值"000152")，並更新 hello 索引實體 (**PartitionKey**值 「 銷售 」 和**RowKey**值"Jones") 在 hello EmployeeIDs 欄位中加入 hello 新員工識別碼 toohello 清單。</span><span class="sxs-lookup"><span data-stu-id="15f93-602">Create an entity group transaction (that is, a batch operation) that inserts hello new employee entity (**PartitionKey** value "Sales" and **RowKey** value "000152"), and updates hello index entity (**PartitionKey** value "Sales" and **RowKey** value "Jones") by adding hello new employee id toohello list in hello EmployeeIDs field.</span></span> <span data-ttu-id="15f93-603">如需實體群組交易的詳細資訊，請參閱 [實體群組交易](#entity-group-transactions)。</span><span class="sxs-lookup"><span data-stu-id="15f93-603">For more information about entity group transactions, see [Entity Group Transactions](#entity-group-transactions).</span></span>  
3. <span data-ttu-id="15f93-604">如果 hello 實體群組交易失敗，因為開放式並行存取錯誤 （其他人就已修改 hello 索引實體），則您需要 toostart 透過在步驟 1 一次。</span><span class="sxs-lookup"><span data-stu-id="15f93-604">If hello entity group transaction fails because of an optimistic concurrency error (someone else has just modified hello index entity), then you need toostart over at step 1 again.</span></span>  

<span data-ttu-id="15f93-605">如果您使用 hello 第二個選項，您可以使用類似的方法 toodeleting 員工。</span><span class="sxs-lookup"><span data-stu-id="15f93-605">You can use a similar approach toodeleting an employee if you are using hello second option.</span></span> <span data-ttu-id="15f93-606">變更員工的姓氏會稍微複雜，因為您將需要更新三個實體的實體群組交易 tooexecute: hello 員工實體、 hello 索引實體 hello 舊的最後一個名稱，與 hello 索引實體 hello 新的最後一個名稱。</span><span class="sxs-lookup"><span data-stu-id="15f93-606">Changing an employee's last name is slightly more complex because you will need tooexecute an entity group transaction that updates three entities: hello employee entity, hello index entity for hello old last name, and hello index entity for hello new last name.</span></span> <span data-ttu-id="15f93-607">您必須再進行任何變更順序，然後您可以使用 tooperform hello 更新使用開放式並行存取 tooretrieve hello ETag 值擷取每個實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-607">You must retrieve each entity before making any changes in order tooretrieve hello ETag values that you can then use tooperform hello updates using optimistic concurrency.</span></span>  

<span data-ttu-id="15f93-608">hello 下列步驟將概略說明當您需要 toolook 上所有的 hello 員工，具有給定部門中最後一個名稱，如果您使用 hello 第二個選項時，您應該遵循的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="15f93-608">hello following steps outline hello process you should follow when you need toolook up all hello employees with a given last name in a department if you are using hello second option.</span></span> <span data-ttu-id="15f93-609">在此範例中，我們會查閱姓氏 Jones hello 銷售部門的所有 hello 員工：</span><span class="sxs-lookup"><span data-stu-id="15f93-609">In this example, we are looking up all hello employees with last name Jones in hello Sales department:</span></span>  

1. <span data-ttu-id="15f93-610">擷取與 hello 索引實體**PartitionKey**實值 「 銷售 」 與 hello **RowKey**值"Jones。 」</span><span class="sxs-lookup"><span data-stu-id="15f93-610">Retrieve hello index entity with a **PartitionKey** value "Sales" and hello **RowKey** value "Jones."</span></span>  
2. <span data-ttu-id="15f93-611">剖析員工識別碼 hello EmployeeIDs 欄位中的 hello 的清單。</span><span class="sxs-lookup"><span data-stu-id="15f93-611">Parse hello list of employee Ids in hello EmployeeIDs field.</span></span>  
3. <span data-ttu-id="15f93-612">如果您需要每個這些員工 （例如電子郵件地址） 的其他資訊，擷取每個使用 hello 員工實體**PartitionKey**值 「 銷售 」 和**RowKey**中的值您在步驟 2 中取得的員工 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="15f93-612">If you need additional information about each of these employees (such as their email addresses), retrieve each of hello employee entities using **PartitionKey** value "Sales" and **RowKey** values from hello list of employees you obtained in step 2.</span></span>  

<span data-ttu-id="15f93-613"><u>選項 3：</u>在個別的資料分割或資料表中建立索引實體</span><span class="sxs-lookup"><span data-stu-id="15f93-613"><u>Option #3:</u> Create index entities in a separate partition or table</span></span>  

<span data-ttu-id="15f93-614">Hello 第三個選項，使用索引的實體儲存 hello 下列資料：</span><span class="sxs-lookup"><span data-stu-id="15f93-614">For hello third option, use index entities that store hello following data:</span></span>  

![][15]

<span data-ttu-id="15f93-615">hello **EmployeeIDs**屬性包含員工的員工識別碼的清單，hello 最後一個名稱儲存在 hello **RowKey**。</span><span class="sxs-lookup"><span data-stu-id="15f93-615">hello **EmployeeIDs** property contains a list of employee ids for employees with hello last name stored in hello **RowKey**.</span></span>  

<span data-ttu-id="15f93-616">Hello 第三個選項時，您無法使用 EGTs toomaintain 一致性，因為 hello 索引實體是位於不同的磁碟分割，從 hello 員工實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-616">With hello third option, you cannot use EGTs toomaintain consistency because hello index entities are in a separate partition from hello employee entities.</span></span> <span data-ttu-id="15f93-617">您應該確保 hello 索引實體最終與 hello 員工實體保持一致。</span><span class="sxs-lookup"><span data-stu-id="15f93-617">You should ensure that hello index entities are eventually consistent with hello employee entities.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="15f93-618">問題和考量</span><span class="sxs-lookup"><span data-stu-id="15f93-618">Issues and considerations</span></span>
<span data-ttu-id="15f93-619">請考慮 hello 時決定下列點如何 tooimplement 這種模式：</span><span class="sxs-lookup"><span data-stu-id="15f93-619">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="15f93-620">此解決方案需要比對實體的至少兩個查詢 tooretrieve： 有一個 tooquery hello 索引實體 tooobtain hello 清單**RowKey**值，然後再來是查詢 tooretrieve hello 清單中的每個實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-620">This solution requires at least two queries tooretrieve matching entities: one tooquery hello index entities tooobtain hello list of **RowKey** values, and then queries tooretrieve each entity in hello list.</span></span>  
* <span data-ttu-id="15f93-621">鑑於個別的實體大小上限為 1 MB，選項 #2 和 hello 方案中的選項 #3 假設 hello 清單的任何特定姓氏的員工識別碼絕不會是大於 1 MB。</span><span class="sxs-lookup"><span data-stu-id="15f93-621">Given that an individual entity has a maximum size of 1 MB, option #2 and option #3 in hello solution assume that hello list of employee ids for any given last name is never greater than 1 MB.</span></span> <span data-ttu-id="15f93-622">如果員工識別碼 hello 清單可能 toobe 大於 1 MB 的大小，使用選項 #1，並儲存在 blob 儲存體中的 hello 索引資料。</span><span class="sxs-lookup"><span data-stu-id="15f93-622">If hello list of employee ids is likely toobe greater than 1 MB in size, use option #1 and store hello index data in blob storage.</span></span>  
* <span data-ttu-id="15f93-623">如果您使用選項 #2 （使用 EGTs toohandle 加入和刪除員工，以及變更員工的姓氏） 您必須評估 hello 磁碟區的交易將會很接近給定資料分割中的 hello 延展性限制。</span><span class="sxs-lookup"><span data-stu-id="15f93-623">If you use option #2 (using EGTs toohandle adding and deleting employees, and changing an employee's last name) you must evaluate if hello volume of transactions will approach hello scalability limits in a given partition.</span></span> <span data-ttu-id="15f93-624">在 hello 情況下，您應該考慮使用佇列 toohandle hello update 最終一致方案 （#1 選項或選項 #3） 要求，並可讓您 toostore 索引實體在不同的磁碟分割，從 hello 員工實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-624">If this is hello case, you should consider an eventually consistent solution (option #1 or option #3) that uses queues toohandle hello update requests and enables you toostore your index entities in a separate partition from hello employee entities.</span></span>  
* <span data-ttu-id="15f93-625">此解決方案中的選項 #2 會假設您想 toolook 向上依部門中的最後一個名稱： 例如，您想 tooretrieve 姓氏 Jones hello 銷售部門的員工清單。</span><span class="sxs-lookup"><span data-stu-id="15f93-625">Option #2 in this solution assumes that you want toolook up by last name within a department: for example, you want tooretrieve a list of employees with a last name Jones in hello Sales department.</span></span> <span data-ttu-id="15f93-626">如果您想 toobe 無法 toolook 向上所有 hello 員工姓氏 Jones hello 整個組織內，使用 #1 選項或選項 #3。</span><span class="sxs-lookup"><span data-stu-id="15f93-626">If you want toobe able toolook up all hello employees with a last name Jones across hello whole organization, use either option #1 or option #3.</span></span>
* <span data-ttu-id="15f93-627">您可以實作以佇列為基礎的解決方案，提供最終一致性 (請參閱 hello[最終保持一致的交易模式](#eventually-consistent-transactions-pattern)如需詳細資訊)。</span><span class="sxs-lookup"><span data-stu-id="15f93-627">You can implement a queue-based solution that delivers eventual consistency (see hello [Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) for more details).</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="15f93-628">當 toouse 此模式</span><span class="sxs-lookup"><span data-stu-id="15f93-628">When toouse this pattern</span></span>
<span data-ttu-id="15f93-629">當您想 toolookup 的所有共用通用的屬性值，例如 hello 姓氏 Jones 具有所有員工的實體集時，請使用此模式。</span><span class="sxs-lookup"><span data-stu-id="15f93-629">Use this pattern when you want toolookup a set of entities that all share a common property value, such as all employees with hello last name Jones.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="15f93-630">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="15f93-630">Related patterns and guidance</span></span>
<span data-ttu-id="15f93-631">hello 下列模式和指導方針也可能是相關實作此模式時：</span><span class="sxs-lookup"><span data-stu-id="15f93-631">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="15f93-632">複合索引鍵模式</span><span class="sxs-lookup"><span data-stu-id="15f93-632">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="15f93-633">最終一致的交易模式</span><span class="sxs-lookup"><span data-stu-id="15f93-633">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  
* [<span data-ttu-id="15f93-634">實體群組交易</span><span class="sxs-lookup"><span data-stu-id="15f93-634">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="15f93-635">使用異質性實體類型</span><span class="sxs-lookup"><span data-stu-id="15f93-635">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  

### <a name="denormalization-pattern"></a><span data-ttu-id="15f93-636">反正規化模式</span><span class="sxs-lookup"><span data-stu-id="15f93-636">Denormalization pattern</span></span>
<span data-ttu-id="15f93-637">合併相關的資料集中單一實體 tooenable 您 tooretrieve 所有 hello 您需要使用單點查詢的資料。</span><span class="sxs-lookup"><span data-stu-id="15f93-637">Combine related data together in a single entity tooenable you tooretrieve all hello data you need with a single point query.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="15f93-638">內容和問題</span><span class="sxs-lookup"><span data-stu-id="15f93-638">Context and problem</span></span>
<span data-ttu-id="15f93-639">在關聯式資料庫中，您通常會正規化資料 tooremove 重複導致多個資料表中擷取資料的查詢。</span><span class="sxs-lookup"><span data-stu-id="15f93-639">In a relational database, you typically normalize data tooremove duplication resulting in queries that retrieve data from multiple tables.</span></span> <span data-ttu-id="15f93-640">如果您在 Azure 資料表中的將資料標準化您，您必須先從 hello 用戶端 toohello 伺服器 tooretrieve 多次往返相關的資料。</span><span class="sxs-lookup"><span data-stu-id="15f93-640">If you normalize your data in Azure tables, you must make multiple round trips from hello client toohello server tooretrieve your related data.</span></span> <span data-ttu-id="15f93-641">例如下, 面顯示 hello 資料表結構需要兩個四捨五入部門的往返 tooretrieve hello 詳細資料： 一個 toofetch hello department 實體中員工包含 hello 經理識別碼和另一個要求 toofetch hello 管理員的詳細資料實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-641">For example, with hello table structure shown below you need two round trips tooretrieve hello details for a department: one toofetch hello department entity that includes hello manager's id, and then another request toofetch hello manager's details in an employee entity.</span></span>  

![][16]

#### <a name="solution"></a><span data-ttu-id="15f93-642">方案</span><span class="sxs-lookup"><span data-stu-id="15f93-642">Solution</span></span>
<span data-ttu-id="15f93-643">而是 hello 資料存放在兩個不同的實體，反正規化 hello 資料並在 hello department 實體中保留一份 hello 管理員詳細資料。</span><span class="sxs-lookup"><span data-stu-id="15f93-643">Instead of storing hello data in two separate entities, denormalize hello data and keep a copy of hello manager's details in hello department entity.</span></span> <span data-ttu-id="15f93-644">例如：</span><span class="sxs-lookup"><span data-stu-id="15f93-644">For example:</span></span>  

![][17]

<span data-ttu-id="15f93-645">與部門實體儲存含有這些屬性，您現在可以擷取您需要使用點查詢的部門相關的所有 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="15f93-645">With department entities stored with these properties, you can now retrieve all hello details you need about a department using a point query.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="15f93-646">問題和考量</span><span class="sxs-lookup"><span data-stu-id="15f93-646">Issues and considerations</span></span>
<span data-ttu-id="15f93-647">請考慮 hello 時決定下列點如何 tooimplement 這種模式：</span><span class="sxs-lookup"><span data-stu-id="15f93-647">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="15f93-648">儲存資料兩次還有一些相關的成本負擔。</span><span class="sxs-lookup"><span data-stu-id="15f93-648">There is some cost overhead associated with storing some data twice.</span></span> <span data-ttu-id="15f93-649">hello 獲益 （造成較少的要求 toohello 儲存體服務） 通常超過 hello 臨界增加儲存成本 (此成本部分的位移和交易的 hello 數目減少您需要 toofetch hello 詳細資料部門）。</span><span class="sxs-lookup"><span data-stu-id="15f93-649">hello performance benefit (resulting from fewer requests toohello storage service) typically outweighs hello marginal increase in storage costs (and this cost is partially offset by a reduction in hello number of transactions you require toofetch hello details of a department).</span></span>  
* <span data-ttu-id="15f93-650">您必須維護 hello hello 儲存經理的相關資訊的兩個實體一致性。</span><span class="sxs-lookup"><span data-stu-id="15f93-650">You must maintain hello consistency of hello two entities that store information about managers.</span></span> <span data-ttu-id="15f93-651">您可以處理 hello 一致性問題使用 EGTs tooupdate 單一不可部分完成交易中的多個實體： 在此情況下，hello department 實體和 hello hello 部門經理的員工實體會儲存在 hello 相同的資料分割。</span><span class="sxs-lookup"><span data-stu-id="15f93-651">You can handle hello consistency issue by using EGTs tooupdate multiple entities in a single atomic transaction: in this case, hello department entity, and hello employee entity for hello department manager are stored in hello same partition.</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="15f93-652">當 toouse 此模式</span><span class="sxs-lookup"><span data-stu-id="15f93-652">When toouse this pattern</span></span>
<span data-ttu-id="15f93-653">當您經常需要 toolook 相關資訊，請使用此模式。</span><span class="sxs-lookup"><span data-stu-id="15f93-653">Use this pattern when you frequently need toolook up related information.</span></span> <span data-ttu-id="15f93-654">此模式會減少您的用戶端必須讓它需要的 tooretrieve hello 資料查詢的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="15f93-654">This pattern reduces hello number of queries your client must make tooretrieve hello data it requires.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="15f93-655">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="15f93-655">Related patterns and guidance</span></span>
<span data-ttu-id="15f93-656">hello 下列模式和指導方針也可能是相關實作此模式時：</span><span class="sxs-lookup"><span data-stu-id="15f93-656">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="15f93-657">複合索引鍵模式</span><span class="sxs-lookup"><span data-stu-id="15f93-657">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="15f93-658">實體群組交易</span><span class="sxs-lookup"><span data-stu-id="15f93-658">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="15f93-659">使用異質性實體類型</span><span class="sxs-lookup"><span data-stu-id="15f93-659">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)

### <a name="compound-key-pattern"></a><span data-ttu-id="15f93-660">複合索引鍵模式</span><span class="sxs-lookup"><span data-stu-id="15f93-660">Compound key pattern</span></span>
<span data-ttu-id="15f93-661">使用複合**RowKey**值 tooenable 用戶端 toolookup 相關資料的單一點查詢。</span><span class="sxs-lookup"><span data-stu-id="15f93-661">Use compound **RowKey** values tooenable a client toolookup related data with a single point query.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="15f93-662">內容和問題</span><span class="sxs-lookup"><span data-stu-id="15f93-662">Context and problem</span></span>
<span data-ttu-id="15f93-663">在關聯式資料庫中，它是在查詢中的自然 toouse 聯結 tooreturn 相關資料 toohello 用戶端，單一查詢中的部分。</span><span class="sxs-lookup"><span data-stu-id="15f93-663">In a relational database, it is quite natural toouse joins in queries tooreturn related pieces of data toohello client in a single query.</span></span> <span data-ttu-id="15f93-664">例如，您可能會使用 hello 員工識別碼 toolook 相關實體，其包含的效能，並且該員工來檢閱資料的清單。</span><span class="sxs-lookup"><span data-stu-id="15f93-664">For example, you might use hello employee id toolook up a list of related entities that contain performance and review data for that employee.</span></span>  

<span data-ttu-id="15f93-665">假設您使用下列結構的 hello hello 資料表服務中儲存員工實體：</span><span class="sxs-lookup"><span data-stu-id="15f93-665">Assume you are storing employee entities in hello Table service using hello following structure:</span></span>  

![][18]

<span data-ttu-id="15f93-666">您也需要相關 tooreviews toostore 歷程記錄資料和每年 hello 位員工的效能，曾為您的組織，而且您需要 toobe 無法 tooaccess 依年度的這項資訊。</span><span class="sxs-lookup"><span data-stu-id="15f93-666">You also need toostore historical data relating tooreviews and performance for each year hello employee has worked for your organization and you need toobe able tooaccess this information by year.</span></span> <span data-ttu-id="15f93-667">其中一個選項是 toocreate 儲存實體具有下列結構的 hello 的另一個資料表：</span><span class="sxs-lookup"><span data-stu-id="15f93-667">One option is toocreate another table that stores entities with hello following structure:</span></span>  

![][19]

<span data-ttu-id="15f93-668">請注意，這會很接近您可能會決定 tooduplicate hello 新實體 tooenable 部分資訊 （例如名字和姓氏） 您 tooretrieve 單一要求您的資料。</span><span class="sxs-lookup"><span data-stu-id="15f93-668">Notice that with this approach you may decide tooduplicate some information (such as first name and last name) in hello new entity tooenable you tooretrieve your data with a single request.</span></span> <span data-ttu-id="15f93-669">不過，您無法維護強式一致性，因為您不能以不可分割方式使用 EGT tooupdate hello 兩個實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-669">However, you cannot maintain strong consistency because you cannot use an EGT tooupdate hello two entities atomically.</span></span>  

#### <a name="solution"></a><span data-ttu-id="15f93-670">方案</span><span class="sxs-lookup"><span data-stu-id="15f93-670">Solution</span></span>
<span data-ttu-id="15f93-671">將新的實體類型儲存在原始資料表使用實體具有下列結構的 hello:</span><span class="sxs-lookup"><span data-stu-id="15f93-671">Store a new entity type in your original table using entities with hello following structure:</span></span>  

![][20]

<span data-ttu-id="15f93-672">請注意如何 hello **RowKey**現在的組合索引鍵所組成的 hello 員工識別碼和 hello 年度 hello 檢閱資料，可讓您 tooretrieve hello 員工的效能，並檢閱與單一實體的單一要求的資料。</span><span class="sxs-lookup"><span data-stu-id="15f93-672">Notice how hello **RowKey** is now a compound key made up of hello employee id and hello year of hello review data that enables you tooretrieve hello employee's performance and review data with a single request for a single entity.</span></span>  

<span data-ttu-id="15f93-673">下列範例中的 hello 概要說明如何擷取所有 hello 檢閱資料 （例如 employee 000123 hello 銷售部門) 的特定員工的：</span><span class="sxs-lookup"><span data-stu-id="15f93-673">hello following example outlines how you can retrieve all hello review data for a particular employee (such as employee 000123 in hello Sales department):</span></span>  

<span data-ttu-id="15f93-674">$filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000123') and (RowKey lt 'empid_000124')&$select=RowKey,Manager Rating,Peer Rating,Comments</span><span class="sxs-lookup"><span data-stu-id="15f93-674">$filter=(PartitionKey eq 'Sales') and (RowKey ge 'empid_000123') and (RowKey lt 'empid_000124')&$select=RowKey,Manager Rating,Peer Rating,Comments</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="15f93-675">問題和考量</span><span class="sxs-lookup"><span data-stu-id="15f93-675">Issues and considerations</span></span>
<span data-ttu-id="15f93-676">請考慮 hello 時決定下列點如何 tooimplement 這種模式：</span><span class="sxs-lookup"><span data-stu-id="15f93-676">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="15f93-677">您應該使用適當的分隔字元，可讓您輕鬆 tooparse hello **RowKey**值： 例如， **000123_2012**。</span><span class="sxs-lookup"><span data-stu-id="15f93-677">You should use a suitable separator character that makes it easy tooparse hello **RowKey** value: for example, **000123_2012**.</span></span>  
* <span data-ttu-id="15f93-678">您也在相同資料分割包含 hello 的相關的資料的其他實體的 hello 儲存此實體相同的員工，這表示您可以使用 EGTs toomaintain 強式一致性。</span><span class="sxs-lookup"><span data-stu-id="15f93-678">You are also storing this entity in hello same partition as other entities that contain related data for hello same employee, which means you can use EGTs toomaintain strong consistency.</span></span>
* <span data-ttu-id="15f93-679">您應該考慮頻率您將查詢 hello 資料 toodetermine 此模式是否適當。</span><span class="sxs-lookup"><span data-stu-id="15f93-679">You should consider how frequently you will query hello data toodetermine whether this pattern is appropriate.</span></span>  <span data-ttu-id="15f93-680">例如，如果您將存取不常 hello 檢閱資料和 hello 主要員工資料通常您應該讓它們保持為不同的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-680">For example, if you will access hello review data infrequently and hello main employee data often you should keep them as separate entities.</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="15f93-681">當 toouse 此模式</span><span class="sxs-lookup"><span data-stu-id="15f93-681">When toouse this pattern</span></span>
<span data-ttu-id="15f93-682">當您需要 toostore 其中一個或多個相關實體您查詢經常會使用這個模式。</span><span class="sxs-lookup"><span data-stu-id="15f93-682">Use this pattern when you need toostore one or more related entities that you query frequently.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="15f93-683">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="15f93-683">Related patterns and guidance</span></span>
<span data-ttu-id="15f93-684">hello 下列模式和指導方針也可能是相關實作此模式時：</span><span class="sxs-lookup"><span data-stu-id="15f93-684">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="15f93-685">實體群組交易</span><span class="sxs-lookup"><span data-stu-id="15f93-685">Entity Group Transactions</span></span>](#entity-group-transactions)  
* [<span data-ttu-id="15f93-686">使用異質性實體類型</span><span class="sxs-lookup"><span data-stu-id="15f93-686">Working with heterogeneous entity types</span></span>](#working-with-heterogeneous-entity-types)  
* [<span data-ttu-id="15f93-687">最終一致的交易模式</span><span class="sxs-lookup"><span data-stu-id="15f93-687">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  

### <a name="log-tail-pattern"></a><span data-ttu-id="15f93-688">記錄結尾模式</span><span class="sxs-lookup"><span data-stu-id="15f93-688">Log tail pattern</span></span>
<span data-ttu-id="15f93-689">擷取 hello  *n* 實體最近加入 tooa 資料分割使用**RowKey**以反向的日期和時間順序排序的值。</span><span class="sxs-lookup"><span data-stu-id="15f93-689">Retrieve hello *n* entities most recently added tooa partition by using a **RowKey** value that sorts in reverse date and time order.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="15f93-690">內容和問題</span><span class="sxs-lookup"><span data-stu-id="15f93-690">Context and problem</span></span>
<span data-ttu-id="15f93-691">常見的需求是能夠 tooretrieve hello 最近建立的實體，例如 hello 十個最新費用報銷送出的員工。</span><span class="sxs-lookup"><span data-stu-id="15f93-691">A common requirement is be able tooretrieve hello most recently created entities, for example hello ten most recent expense claims submitted by an employee.</span></span> <span data-ttu-id="15f93-692">資料表查詢支援**$top**第一次查詢作業 tooreturn hello  *n* 從一組實體： 集合中沒有任何對等查詢作業 tooreturn hello 最後 n 個實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-692">Table queries support a **$top** query operation tooreturn hello first *n* entities from a set: there is no equivalent query operation tooreturn hello last n entities in a set.</span></span>  

#### <a name="solution"></a><span data-ttu-id="15f93-693">方案</span><span class="sxs-lookup"><span data-stu-id="15f93-693">Solution</span></span>
<span data-ttu-id="15f93-694">使用的存放區 hello 實體**RowKey** ，自然反向排序日期/時間順序使用，因此 hello 最新的項目永遠都是 hello hello 資料表中的第一個。</span><span class="sxs-lookup"><span data-stu-id="15f93-694">Store hello entities using a **RowKey** that naturally sorts in reverse date/time order by using so hello most recent entry is always hello first one in hello table.</span></span>  

<span data-ttu-id="15f93-695">例如，toobe 無法 tooretrieve hello 員工所提交的十個最新費用報銷，您可以使用衍生自 hello 目前日期/時間反向刻度值。</span><span class="sxs-lookup"><span data-stu-id="15f93-695">For example, toobe able tooretrieve hello ten most recent expense claims submitted by an employee, you can use a reverse tick value derived from hello current date/time.</span></span> <span data-ttu-id="15f93-696">hello 下列 C# 程式碼範例會示範其中一種方式 toocreate 適當"反轉刻度"的值為**RowKey**從 hello 最近 toohello 最舊的排序：</span><span class="sxs-lookup"><span data-stu-id="15f93-696">hello following C# code sample shows one way toocreate a suitable "inverted ticks" value for a **RowKey** that sorts from hello most recent toohello oldest:</span></span>  

`string invertedTicks = string.Format("{0:D19}", DateTime.MaxValue.Ticks - DateTime.UtcNow.Ticks);`  

<span data-ttu-id="15f93-697">您可以取得使用下列程式碼的 hello toohello 日期時間值：</span><span class="sxs-lookup"><span data-stu-id="15f93-697">You can get back toohello date time value using hello following code:</span></span>  

`DateTime dt = new DateTime(DateTime.MaxValue.Ticks - Int64.Parse(invertedTicks));`  

<span data-ttu-id="15f93-698">hello 資料表查詢看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="15f93-698">hello table query looks like this:</span></span>  

`https://myaccount.table.core.windows.net/EmployeeExpense(PartitionKey='empid')?$top=10`  

#### <a name="issues-and-considerations"></a><span data-ttu-id="15f93-699">問題和考量</span><span class="sxs-lookup"><span data-stu-id="15f93-699">Issues and considerations</span></span>
<span data-ttu-id="15f93-700">請考慮 hello 時決定下列點如何 tooimplement 這種模式：</span><span class="sxs-lookup"><span data-stu-id="15f93-700">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="15f93-701">您必須對 hello 反向刻度值加上前置零進行填補 tooensure hello 字串值排序如預期般。</span><span class="sxs-lookup"><span data-stu-id="15f93-701">You must pad hello reverse tick value with leading zeroes tooensure hello string value sorts as expected.</span></span>  
* <span data-ttu-id="15f93-702">您必須留意的 hello 在 hello 層級資料分割的延展性目標。</span><span class="sxs-lookup"><span data-stu-id="15f93-702">You must be aware of hello scalability targets at hello level of a partition.</span></span> <span data-ttu-id="15f93-703">請留意不要建立熱點資料分割。</span><span class="sxs-lookup"><span data-stu-id="15f93-703">Be careful not create hot spot partitions.</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="15f93-704">當 toouse 此模式</span><span class="sxs-lookup"><span data-stu-id="15f93-704">When toouse this pattern</span></span>
<span data-ttu-id="15f93-705">使用此模式需要反向的日期/時間順序 tooaccess 實體時，或當您需要 tooaccess hello 是最近加入的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-705">Use this pattern when you need tooaccess entities in reverse date/time order or when you need tooaccess hello most recently added entities.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="15f93-706">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="15f93-706">Related patterns and guidance</span></span>
<span data-ttu-id="15f93-707">hello 下列模式和指導方針也可能是相關實作此模式時：</span><span class="sxs-lookup"><span data-stu-id="15f93-707">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="15f93-708">在前面加上/附加反向模式</span><span class="sxs-lookup"><span data-stu-id="15f93-708">Prepend / append anti-pattern</span></span>](#prepend-append-anti-pattern)  
* [<span data-ttu-id="15f93-709">擷取實體</span><span class="sxs-lookup"><span data-stu-id="15f93-709">Retrieving entities</span></span>](#retrieving-entities)  

### <a name="high-volume-delete-pattern"></a><span data-ttu-id="15f93-710">大量刪除模式</span><span class="sxs-lookup"><span data-stu-id="15f93-710">High volume delete pattern</span></span>
<span data-ttu-id="15f93-711">藉由將同時刪除所有 hello 實體都儲存在他們自己的個別資料表; 中啟用 hello 刪除大量實體您刪除 hello 實體 hello 資料表中刪除。</span><span class="sxs-lookup"><span data-stu-id="15f93-711">Enable hello deletion of a high volume of entities by storing all hello entities for simultaneous deletion in their own separate table; you delete hello entities by deleting hello table.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="15f93-712">內容和問題</span><span class="sxs-lookup"><span data-stu-id="15f93-712">Context and problem</span></span>
<span data-ttu-id="15f93-713">許多應用程式刪除舊的資料不再需要 toobe 可用 tooa 用戶端應用程式，或該 hello 應用程式已封存 tooanother 儲存媒體。</span><span class="sxs-lookup"><span data-stu-id="15f93-713">Many applications delete old data which no longer needs toobe available tooa client application, or that hello application has archived tooanother storage medium.</span></span> <span data-ttu-id="15f93-714">您通常可以依日期識別這類資料： 例如，您有需求 toodelete 記錄是 60 天以前的所有登入要求。</span><span class="sxs-lookup"><span data-stu-id="15f93-714">You typically identify such data by a date: for example, you have a requirement toodelete records of all login requests that are more than 60 days old.</span></span>  

<span data-ttu-id="15f93-715">一個可能的設計是 toouse hello 日期和時間在 hello hello 登入要求**RowKey**:</span><span class="sxs-lookup"><span data-stu-id="15f93-715">One possible design is toouse hello date and time of hello login request in hello **RowKey**:</span></span>  

![][21]

<span data-ttu-id="15f93-716">這個方法可避免分割區的作用，因為 hello 應用程式可以插入和刪除不同的磁碟分割中每個使用者的登入實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-716">This approach avoids partition hotspots because hello application can insert and delete login entities for each user in a separate partition.</span></span> <span data-ttu-id="15f93-717">不過，這種方法可能會很耗費資源和耗時如果您有大量的實體，因為先 tooperform 資料表掃描順序 tooidentify 中所有的 hello 實體 toodelete，而且則必須刪除舊的每個實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-717">However, this approach may be costly and time consuming if you have a large number of entities because first you need tooperform a table scan in order tooidentify all hello entities toodelete, and then you must delete each old entity.</span></span> <span data-ttu-id="15f93-718">請注意，您可以藉由批次處理多個刪除要求到 EGTs 減少 hello 往返 toohello 需要 server toodelete hello 舊的實體數目。</span><span class="sxs-lookup"><span data-stu-id="15f93-718">Note that you can reduce hello number of round trips toohello server required toodelete hello old entities by batching multiple delete requests into EGTs.</span></span>  

#### <a name="solution"></a><span data-ttu-id="15f93-719">方案</span><span class="sxs-lookup"><span data-stu-id="15f93-719">Solution</span></span>
<span data-ttu-id="15f93-720">為每天的登入嘗試使用個別的資料表。</span><span class="sxs-lookup"><span data-stu-id="15f93-720">Use a separate table for each day of login attempts.</span></span> <span data-ttu-id="15f93-721">當您要插入的實體，並刪除舊的實體是現在只要刪除一個資料表的每一天的問題，您可以使用上述 tooavoid 熱點 hello 實體設計 （單一儲存體作業） 而不是尋找及刪除上百和無數每日的個別登入實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-721">You can use hello entity design above tooavoid hotspots when you are inserting entities, and deleting old entities is now simply a question of deleting one table every day (a single storage operation) instead of finding and deleting hundreds and thousands of individual login entities every day.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="15f93-722">問題和考量</span><span class="sxs-lookup"><span data-stu-id="15f93-722">Issues and considerations</span></span>
<span data-ttu-id="15f93-723">請考慮 hello 時決定下列點如何 tooimplement 這種模式：</span><span class="sxs-lookup"><span data-stu-id="15f93-723">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="15f93-724">您的設計是否支援其他應用程式將使用 hello 資料，例如查閱特定實體、 連結和其他資料或產生的彙總資訊的方式？</span><span class="sxs-lookup"><span data-stu-id="15f93-724">Does your design support other ways your application will use hello data such as looking up specific entities, linking with other data, or generating aggregate information?</span></span>  
* <span data-ttu-id="15f93-725">您的設計在插入新實體時是否可避免產生熱點？</span><span class="sxs-lookup"><span data-stu-id="15f93-725">Does your design avoid hot spots when you are inserting new entities?</span></span>  
* <span data-ttu-id="15f93-726">預期的延遲，如果您想 tooreuse hello 相同後刪除的資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="15f93-726">Expect a delay if you want tooreuse hello same table name after deleting it.</span></span> <span data-ttu-id="15f93-727">它是較佳的 tooalways 使用唯一資料表名稱。</span><span class="sxs-lookup"><span data-stu-id="15f93-727">It's better tooalways use unique table names.</span></span>  
* <span data-ttu-id="15f93-728">預期某些節流，當您第一次使用新的資料表，而 hello 表格服務會學習 hello 存取模式和節點之間分配 hello 資料分割。</span><span class="sxs-lookup"><span data-stu-id="15f93-728">Expect some throttling when you first use a new table while hello Table service learns hello access patterns and distributes hello partitions across nodes.</span></span> <span data-ttu-id="15f93-729">您應該考慮您需要 toocreate 新資料表的頻率。</span><span class="sxs-lookup"><span data-stu-id="15f93-729">You should consider how frequently you need toocreate new tables.</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="15f93-730">當 toouse 此模式</span><span class="sxs-lookup"><span data-stu-id="15f93-730">When toouse this pattern</span></span>
<span data-ttu-id="15f93-731">使用此模式，當您有大量的實體，您必須刪除 hello 在相同的時間。</span><span class="sxs-lookup"><span data-stu-id="15f93-731">Use this pattern when you have a high volume of entities that you must delete at hello same time.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="15f93-732">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="15f93-732">Related patterns and guidance</span></span>
<span data-ttu-id="15f93-733">hello 下列模式和指導方針也可能是相關實作此模式時：</span><span class="sxs-lookup"><span data-stu-id="15f93-733">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="15f93-734">實體群組交易</span><span class="sxs-lookup"><span data-stu-id="15f93-734">Entity Group Transactions</span></span>](#entity-group-transactions)
* [<span data-ttu-id="15f93-735">修改實體</span><span class="sxs-lookup"><span data-stu-id="15f93-735">Modifying entities</span></span>](#modifying-entities)  

### <a name="data-series-pattern"></a><span data-ttu-id="15f93-736">資料序列模式</span><span class="sxs-lookup"><span data-stu-id="15f93-736">Data series pattern</span></span>
<span data-ttu-id="15f93-737">存放區中單一實體 toominimize hello 的許多要求您進行完整的資料數列。</span><span class="sxs-lookup"><span data-stu-id="15f93-737">Store complete data series in a single entity toominimize hello number of requests you make.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="15f93-738">內容和問題</span><span class="sxs-lookup"><span data-stu-id="15f93-738">Context and problem</span></span>
<span data-ttu-id="15f93-739">常見的案例是針對應用程式 toostore 一系列的資料，它通常需要 tooretrieve 一次。</span><span class="sxs-lookup"><span data-stu-id="15f93-739">A common scenario is for an application toostore a series of data that it typically needs tooretrieve all at once.</span></span> <span data-ttu-id="15f93-740">例如，您的應用程式可能會記錄每個員工傳送每小時的 IM 訊息數目，然後使用 每位使用者透過傳送的訊息數目 hello 上述 24 小時內的這個資訊 tooplot。</span><span class="sxs-lookup"><span data-stu-id="15f93-740">For example, your application might record how many IM messages each employee sends every hour, and then use this information tooplot how many messages each user sent over hello preceding 24 hours.</span></span> <span data-ttu-id="15f93-741">一個設計可能會為每位員工的 toostore 24 實體：</span><span class="sxs-lookup"><span data-stu-id="15f93-741">One design might be toostore 24 entities for each employee:</span></span>  

![][22]

<span data-ttu-id="15f93-742">與這個設計中，可以輕鬆地找到並更新每一位員工的 hello 實體 tooupdate 只要 hello 應用程式需要 tooupdate hello 訊息計數值。</span><span class="sxs-lookup"><span data-stu-id="15f93-742">With this design, you can easily locate and update hello entity tooupdate for each employee whenever hello application needs tooupdate hello message count value.</span></span> <span data-ttu-id="15f93-743">不過，tooretrieve hello 資訊 tooplot hello 前 24 小時的 hello 活動的圖表，您必須擷取 24 的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-743">However, tooretrieve hello information tooplot a chart of hello activity for hello preceding 24 hours, you must retrieve 24 entities.</span></span>  

#### <a name="solution"></a><span data-ttu-id="15f93-744">方案</span><span class="sxs-lookup"><span data-stu-id="15f93-744">Solution</span></span>
<span data-ttu-id="15f93-745">使用下列的設計，含有個別屬性 toostore hello 訊息計數每小時的 hello:</span><span class="sxs-lookup"><span data-stu-id="15f93-745">Use hello following design with a separate property toostore hello message count for each hour:</span></span>  

![][23]

<span data-ttu-id="15f93-746">與這個設計中，您可以使用合併作業 tooupdate hello 訊息計數員工的特定小時。</span><span class="sxs-lookup"><span data-stu-id="15f93-746">With this design, you can use a merge operation tooupdate hello message count for an employee for a specific hour.</span></span> <span data-ttu-id="15f93-747">現在，您可以擷取您需要使用要求的單一實體 tooplot hello 圖表的所有 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="15f93-747">Now, you can retrieve all hello information you need tooplot hello chart using a request for a single entity.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="15f93-748">問題和考量</span><span class="sxs-lookup"><span data-stu-id="15f93-748">Issues and considerations</span></span>
<span data-ttu-id="15f93-749">請考慮 hello 時決定下列點如何 tooimplement 這種模式：</span><span class="sxs-lookup"><span data-stu-id="15f93-749">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="15f93-750">完整的資料數列不符合單一實體 （實體最多可以有 too252 屬性），如果使用替代的資料存放區，例如 blob。</span><span class="sxs-lookup"><span data-stu-id="15f93-750">If your complete data series does not fit into a single entity (an entity can have up too252 properties), use an alternative data store such as a blob.</span></span>  
* <span data-ttu-id="15f93-751">如果您有多個用戶端同時更新實體，您將需要 toouse hello **ETag** tooimplement 開放式並行存取。</span><span class="sxs-lookup"><span data-stu-id="15f93-751">If you have multiple clients updating an entity simultaneously, you will need toouse hello **ETag** tooimplement optimistic concurrency.</span></span> <span data-ttu-id="15f93-752">如果您有許多用戶端，則預期應會有激烈的爭用情況。</span><span class="sxs-lookup"><span data-stu-id="15f93-752">If you have many clients, you may experience high contention.</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="15f93-753">當 toouse 此模式</span><span class="sxs-lookup"><span data-stu-id="15f93-753">When toouse this pattern</span></span>
<span data-ttu-id="15f93-754">當您需要 tooupdate 並擷取個別實體與相關聯的資料數列時，請使用此模式。</span><span class="sxs-lookup"><span data-stu-id="15f93-754">Use this pattern when you need tooupdate and retrieve a data series associated with an individual entity.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="15f93-755">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="15f93-755">Related patterns and guidance</span></span>
<span data-ttu-id="15f93-756">hello 下列模式和指導方針也可能是相關實作此模式時：</span><span class="sxs-lookup"><span data-stu-id="15f93-756">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="15f93-757">大型實體模式</span><span class="sxs-lookup"><span data-stu-id="15f93-757">Large entities pattern</span></span>](#large-entities-pattern)  
* [<span data-ttu-id="15f93-758">合併或取代</span><span class="sxs-lookup"><span data-stu-id="15f93-758">Merge or replace</span></span>](#merge-or-replace)  
* <span data-ttu-id="15f93-759">[最終一致性的交易模式](#eventually-consistent-transactions-pattern)（如果您 hello 資料數列在儲存 blob）</span><span class="sxs-lookup"><span data-stu-id="15f93-759">[Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) (if you are storing hello data series in a blob)</span></span>  

### <a name="wide-entities-pattern"></a><span data-ttu-id="15f93-760">寬型實體模式</span><span class="sxs-lookup"><span data-stu-id="15f93-760">Wide entities pattern</span></span>
<span data-ttu-id="15f93-761">使用多個實體的實體 toostore 邏輯實體具有多個 252 的屬性。</span><span class="sxs-lookup"><span data-stu-id="15f93-761">Use multiple physical entities toostore logical entities with more than 252 properties.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="15f93-762">內容和問題</span><span class="sxs-lookup"><span data-stu-id="15f93-762">Context and problem</span></span>
<span data-ttu-id="15f93-763">個別實體可以擁有 252 個以上的屬性 （不含 hello 強制系統屬性），而且無法將超過 1 MB 的資料儲存在總計。</span><span class="sxs-lookup"><span data-stu-id="15f93-763">An individual entity can have no more than 252 properties (excluding hello mandatory system properties) and cannot store more than 1 MB of data in total.</span></span> <span data-ttu-id="15f93-764">在關聯式資料庫中，您通常得到 round hello 大小之資料列的任何限制，加入新的資料表，以及強制執行它們之間的 1 對 1 關聯性。</span><span class="sxs-lookup"><span data-stu-id="15f93-764">In a relational database, you would typically get round any limits on hello size of a row by adding a new table and enforcing a 1-to-1 relationship between them.</span></span>  

#### <a name="solution"></a><span data-ttu-id="15f93-765">方案</span><span class="sxs-lookup"><span data-stu-id="15f93-765">Solution</span></span>
<span data-ttu-id="15f93-766">使用 hello 表格服務，您可以儲存多個實體 toorepresent 252 多個屬性的單一大型的商務物件。</span><span class="sxs-lookup"><span data-stu-id="15f93-766">Using hello Table service, you can store multiple entities toorepresent a single large business object with more than 252 properties.</span></span> <span data-ttu-id="15f93-767">比方說，如果您想 toostore hello IM 傳送之訊息的每個員工的 hello 過去 365 天內的數字計數，您可以使用下列兩個實體使用不同的結構描述的設計 hello:</span><span class="sxs-lookup"><span data-stu-id="15f93-767">For example, if you want toostore a count of hello number of IM messages sent by each employee for hello last 365 days, you could use hello following design that uses two entities with different schemas:</span></span>  

![][24]

<span data-ttu-id="15f93-768">如果您需要 toomake 需要更新它們彼此同步處理兩個實體 tookeep 的變更，您可以使用 EGT。</span><span class="sxs-lookup"><span data-stu-id="15f93-768">If you need toomake a change that requires updating both entities tookeep them synchronized with each other you can use an EGT.</span></span> <span data-ttu-id="15f93-769">否則，您可以使用單一合併作業 tooupdate hello 訊息計數的特定日期。</span><span class="sxs-lookup"><span data-stu-id="15f93-769">Otherwise, you can use a single merge operation tooupdate hello message count for a specific day.</span></span> <span data-ttu-id="15f93-770">所有您必須擷取這兩個實體，您可以使用兩個同時使用的有效要求執行個別員工的 hello 資料 tooretrieve **PartitionKey**和**RowKey**值。</span><span class="sxs-lookup"><span data-stu-id="15f93-770">tooretrieve all hello data for an individual employee you must retrieve both entities, which you can do with two efficient requests that use both a **PartitionKey** and a **RowKey** value.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="15f93-771">問題和考量</span><span class="sxs-lookup"><span data-stu-id="15f93-771">Issues and considerations</span></span>
<span data-ttu-id="15f93-772">請考慮 hello 時決定下列點如何 tooimplement 這種模式：</span><span class="sxs-lookup"><span data-stu-id="15f93-772">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="15f93-773">擷取完成的邏輯實體牽涉到兩個以上的儲存體交易： 一個 tooretrieve 實際實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-773">Retrieving a complete logical entity involves at least two storage transactions: one tooretrieve each physical entity.</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="15f93-774">當 toouse 此模式</span><span class="sxs-lookup"><span data-stu-id="15f93-774">When toouse this pattern</span></span>
<span data-ttu-id="15f93-775">當需要 toostore 實體其大小或屬性的數目超過 hello 限制個別實體中 hello 表格服務，請使用此模式。</span><span class="sxs-lookup"><span data-stu-id="15f93-775">Use this pattern when  need toostore entities whose size or number of properties exceeds hello limits for an individual entity in hello Table service.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="15f93-776">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="15f93-776">Related patterns and guidance</span></span>
<span data-ttu-id="15f93-777">hello 下列模式和指導方針也可能是相關實作此模式時：</span><span class="sxs-lookup"><span data-stu-id="15f93-777">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="15f93-778">實體群組交易</span><span class="sxs-lookup"><span data-stu-id="15f93-778">Entity Group Transactions</span></span>](#entity-group-transactions)
* [<span data-ttu-id="15f93-779">合併或取代</span><span class="sxs-lookup"><span data-stu-id="15f93-779">Merge or replace</span></span>](#merge-or-replace)

### <a name="large-entities-pattern"></a><span data-ttu-id="15f93-780">大型實體模式</span><span class="sxs-lookup"><span data-stu-id="15f93-780">Large entities pattern</span></span>
<span data-ttu-id="15f93-781">使用 blob 儲存體 toostore 大型屬性值。</span><span class="sxs-lookup"><span data-stu-id="15f93-781">Use blob storage toostore large property values.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="15f93-782">內容和問題</span><span class="sxs-lookup"><span data-stu-id="15f93-782">Context and problem</span></span>
<span data-ttu-id="15f93-783">個別實體無法儲存總計超過 1 MB 的資料。</span><span class="sxs-lookup"><span data-stu-id="15f93-783">An individual entity cannot store more than 1 MB of data in total.</span></span> <span data-ttu-id="15f93-784">如果一或多個屬性的儲存值，這個值會導致實體 tooexceed hello 總大小，您無法儲存整個實體的 hello hello 表格服務中。</span><span class="sxs-lookup"><span data-stu-id="15f93-784">If one or several of your properties store values that cause hello total size of your entity tooexceed this value, you cannot store hello entire entity in hello Table service.</span></span>  

#### <a name="solution"></a><span data-ttu-id="15f93-785">方案</span><span class="sxs-lookup"><span data-stu-id="15f93-785">Solution</span></span>
<span data-ttu-id="15f93-786">如果實體的大小超過 1 MB，因為一個或多個屬性包含大量的資料，您可以在 hello Blob 服務中儲存資料，然後將 hello hello blob 位址儲存在 hello 實體中的屬性。</span><span class="sxs-lookup"><span data-stu-id="15f93-786">If your entity exceeds 1 MB in size because one or more properties contain a large amount of data, you can store data in hello Blob service and then store hello address of hello blob in a property in hello entity.</span></span> <span data-ttu-id="15f93-787">比方說，您可以在 hello 之員工的相片儲存在 blob 儲存體，並將連結 toohello 相片儲存在 hello**相片**員工實體的屬性：</span><span class="sxs-lookup"><span data-stu-id="15f93-787">For example, you can store hello photo of an employee in blob storage and store a link toohello photo in hello **Photo** property of your employee entity:</span></span>  

![][25]

#### <a name="issues-and-considerations"></a><span data-ttu-id="15f93-788">問題和考量</span><span class="sxs-lookup"><span data-stu-id="15f93-788">Issues and considerations</span></span>
<span data-ttu-id="15f93-789">請考慮 hello 時決定下列點如何 tooimplement 這種模式：</span><span class="sxs-lookup"><span data-stu-id="15f93-789">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="15f93-790">toomaintain 最終一致性 hello 表格服務中的 hello 實體與 hello Blob 服務中的 hello 資料之間使用 hello[最終保持一致的交易模式](#eventually-consistent-transactions-pattern)toomaintain 您的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-790">toomaintain eventual consistency between hello entity in hello Table service and hello data in hello Blob service, use hello [Eventually consistent transactions pattern](#eventually-consistent-transactions-pattern) toomaintain your entities.</span></span>
* <span data-ttu-id="15f93-791">擷取完整實體牽涉到兩個以上的儲存體交易： 一個 tooretrieve hello 實體和一個 tooretrieve hello blob 資料。</span><span class="sxs-lookup"><span data-stu-id="15f93-791">Retrieving a complete entity involves at least two storage transactions: one tooretrieve hello entity and one tooretrieve hello blob data.</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="15f93-792">當 toouse 此模式</span><span class="sxs-lookup"><span data-stu-id="15f93-792">When toouse this pattern</span></span>
<span data-ttu-id="15f93-793">當您需要其大小超過個別實體 hello 表格服務中的 hello 限制 toostore 實體時，請使用此模式。</span><span class="sxs-lookup"><span data-stu-id="15f93-793">Use this pattern when you need toostore entities whose size exceeds hello limits for an individual entity in hello Table service.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="15f93-794">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="15f93-794">Related patterns and guidance</span></span>
<span data-ttu-id="15f93-795">hello 下列模式和指導方針也可能是相關實作此模式時：</span><span class="sxs-lookup"><span data-stu-id="15f93-795">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="15f93-796">最終一致的交易模式</span><span class="sxs-lookup"><span data-stu-id="15f93-796">Eventually consistent transactions pattern</span></span>](#eventually-consistent-transactions-pattern)  
* [<span data-ttu-id="15f93-797">寬型實體模式</span><span class="sxs-lookup"><span data-stu-id="15f93-797">Wide entities pattern</span></span>](#wide-entities-pattern)

<a name="prepend-append-anti-pattern"></a>

### <a name="prependappend-anti-pattern"></a><span data-ttu-id="15f93-798">在前面加上/附加反向模式</span><span class="sxs-lookup"><span data-stu-id="15f93-798">Prepend/append anti-pattern</span></span>
<span data-ttu-id="15f93-799">您的跨多個資料分割分配 hello 插入大量插入時，增加延展性。</span><span class="sxs-lookup"><span data-stu-id="15f93-799">Increase scalability when you have a high volume of inserts by spreading hello inserts across multiple partitions.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="15f93-800">內容和問題</span><span class="sxs-lookup"><span data-stu-id="15f93-800">Context and problem</span></span>
<span data-ttu-id="15f93-801">前面加上或附加的實體儲存 tooyour 實體通常會導致第一次加入新的實體 toohello hello 應用程式或最後一個資料分割的資料分割的順序。</span><span class="sxs-lookup"><span data-stu-id="15f93-801">Prepending or appending entities tooyour stored entities typically results in hello application adding new entities toohello first or last partition of a sequence of partitions.</span></span> <span data-ttu-id="15f93-802">在此情況下，所有在任何指定時間的 hello 插入 hello 跨多個節點，插入相同的資料分割，建立負載平衡時，防止 hello 表格服務的作用中未進行，而且可能會造成您的應用程式 toohit hello 延展性資料分割的目標。</span><span class="sxs-lookup"><span data-stu-id="15f93-802">In this case, all of hello inserts at any given time are taking place in hello same partition, creating a hotspot that prevents hello table service from load balancing inserts across multiple nodes, and possibly causing your application toohit hello scalability targets for partition.</span></span> <span data-ttu-id="15f93-803">例如，如果您的應用程式記錄檔的網路與資源存取的員工，然後如下所示的實體結構可能會導致 hello 目前的小時資料分割成為作用點，如果交易 hello 量分別達到 hello 的延展性目標個別的資料分割：</span><span class="sxs-lookup"><span data-stu-id="15f93-803">For example, if you have an application that logs network and resource access by employees, then an entity structure as shown below could result in hello current hour's partition becoming a hotspot if hello volume of transactions reaches hello scalability target for an individual partition:</span></span>  

![][26]

#### <a name="solution"></a><span data-ttu-id="15f93-804">方案</span><span class="sxs-lookup"><span data-stu-id="15f93-804">Solution</span></span>
<span data-ttu-id="15f93-805">hello 下列替代實體結構可避免任何特定資料分割的作用區為 hello 應用程式記錄檔事件：</span><span class="sxs-lookup"><span data-stu-id="15f93-805">hello following alternative entity structure avoids a hotspot on any particular partition as hello application logs events:</span></span>  

![][27]

<span data-ttu-id="15f93-806">請注意此範例如何同時 hello **PartitionKey**和**RowKey**是複合的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="15f93-806">Notice with this example how both hello **PartitionKey** and **RowKey** are compound keys.</span></span> <span data-ttu-id="15f93-807">hello **PartitionKey**橫跨多個資料分割使用 hello 部門和員工識別碼 toodistribute hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="15f93-807">hello **PartitionKey** uses both hello department and employee id toodistribute hello logging across multiple partitions.</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="15f93-808">問題和考量</span><span class="sxs-lookup"><span data-stu-id="15f93-808">Issues and considerations</span></span>
<span data-ttu-id="15f93-809">請考慮 hello 時決定下列點如何 tooimplement 這種模式：</span><span class="sxs-lookup"><span data-stu-id="15f93-809">Consider hello following points when deciding how tooimplement this pattern:</span></span>  

* <span data-ttu-id="15f93-810">沒有 hello 替代索引鍵結構可避免熱資料分割上建立插入有效率地支援 hello 查詢可讓用戶端應用程式嗎？</span><span class="sxs-lookup"><span data-stu-id="15f93-810">Does hello alternative key structure that avoids creating hot partitions on inserts efficiently support hello queries your client application makes?</span></span>  
* <span data-ttu-id="15f93-811">您預期的磁碟區的交易表示，您可能 tooreach hello 個別的資料分割的延展性目標而進行節流處理 hello 儲存體服務？</span><span class="sxs-lookup"><span data-stu-id="15f93-811">Does your anticipated volume of transactions mean that you are likely tooreach hello scalability targets for an individual partition and be throttled by hello storage service?</span></span>  

#### <a name="when-toouse-this-pattern"></a><span data-ttu-id="15f93-812">當 toouse 此模式</span><span class="sxs-lookup"><span data-stu-id="15f93-812">When toouse this pattern</span></span>
<span data-ttu-id="15f93-813">您的磁碟區的交易時可能 tooresult 中節流 hello 儲存體服務，當您存取熱資料分割時，請避免 hello 前面加上/附加反面模式。</span><span class="sxs-lookup"><span data-stu-id="15f93-813">Avoid hello prepend/append anti-pattern when your volume of transactions is likely tooresult in throttling by hello storage service when you access a hot partition.</span></span>  

#### <a name="related-patterns-and-guidance"></a><span data-ttu-id="15f93-814">相關的模式和指導方針</span><span class="sxs-lookup"><span data-stu-id="15f93-814">Related patterns and guidance</span></span>
<span data-ttu-id="15f93-815">hello 下列模式和指導方針也可能是相關實作此模式時：</span><span class="sxs-lookup"><span data-stu-id="15f93-815">hello following patterns and guidance may also be relevant when implementing this pattern:</span></span>  

* [<span data-ttu-id="15f93-816">複合索引鍵模式</span><span class="sxs-lookup"><span data-stu-id="15f93-816">Compound key pattern</span></span>](#compound-key-pattern)  
* [<span data-ttu-id="15f93-817">記錄檔結尾模式</span><span class="sxs-lookup"><span data-stu-id="15f93-817">Log tail pattern</span></span>](#log-tail-pattern)  
* [<span data-ttu-id="15f93-818">修改實體</span><span class="sxs-lookup"><span data-stu-id="15f93-818">Modifying entities</span></span>](#modifying-entities)  

### <a name="log-data-anti-pattern"></a><span data-ttu-id="15f93-819">記錄資料反向模式</span><span class="sxs-lookup"><span data-stu-id="15f93-819">Log data anti-pattern</span></span>
<span data-ttu-id="15f93-820">一般而言，您應該使用 hello Blob 服務，而不是 hello 資料表服務 toostore 記錄檔資料。</span><span class="sxs-lookup"><span data-stu-id="15f93-820">Typically, you should use hello Blob service instead of hello Table service toostore log data.</span></span>  

#### <a name="context-and-problem"></a><span data-ttu-id="15f93-821">內容和問題</span><span class="sxs-lookup"><span data-stu-id="15f93-821">Context and problem</span></span>
<span data-ttu-id="15f93-822">一般使用案例記錄的資料是 tooretrieve 的特定日期/時間範圍的記錄項目選取： 例如，您想的 toofind 所有 hello 錯誤和嚴重訊息 15:04 15:06 在特定日期之間的應用程式記錄。</span><span class="sxs-lookup"><span data-stu-id="15f93-822">A common use case for log data is tooretrieve a selection of log entries for a specific date/time range: for example, you want toofind all hello error and critical messages that your application logged between 15:04 and 15:06 on a specific date.</span></span> <span data-ttu-id="15f93-823">您不想 toouse hello 日期和時間 hello 記錄訊息 toodetermine hello 磁碟分割的儲存記錄檔項目，:，熱資料分割中的結果因為在任何時候，會共用所有 hello 記錄實體 hello 相同**PartitionKey**值 (請參閱 hello 節[前面加上/附加反面模式](#prepend-append-anti-pattern))。</span><span class="sxs-lookup"><span data-stu-id="15f93-823">You do not want toouse hello date and time of hello log message toodetermine hello partition you save log entities to: that results in a hot partition because at any given time, all hello log entities will share hello same **PartitionKey** value (see hello section [Prepend/append anti-pattern](#prepend-append-anti-pattern)).</span></span> <span data-ttu-id="15f93-824">例如，下列實體記錄檔訊息的結構描述的 hello 會導致熱資料分割因為 hello 應用程式會寫入所有的記錄訊息 toohello hello 目前的日期和小時的資料分割：</span><span class="sxs-lookup"><span data-stu-id="15f93-824">For example, hello following entity schema for a log message results in a hot partition because hello application writes all log messages toohello partition for hello current date and hour:</span></span>  

![][28]

<span data-ttu-id="15f93-825">在此範例中，hello **RowKey**包括 hello 記錄訊息 tooensure 記錄訊息會儲存日期/時間順序排列的 hello 日期和時間，並包含訊息識別碼，如果多個記錄檔訊息共用相同的日期和時間的 hello。</span><span class="sxs-lookup"><span data-stu-id="15f93-825">In this example, hello **RowKey** includes hello date and time of hello log message tooensure that log messages are stored sorted in date/time order, and includes a message id in case multiple log messages share hello same date and time.</span></span>  

<span data-ttu-id="15f93-826">另一個方法是 toouse **PartitionKey**這可確保 hello 應用程式將訊息寫入一個範圍內的資料分割。</span><span class="sxs-lookup"><span data-stu-id="15f93-826">Another approach is toouse a **PartitionKey** that ensures that hello application writes messages across a range of partitions.</span></span> <span data-ttu-id="15f93-827">比方說，如果 hello 記錄檔訊息的 hello 來源提供跨多個資料分割方式 toodistribute 訊息，您可以使用下列項目結構描述的 hello:</span><span class="sxs-lookup"><span data-stu-id="15f93-827">For example, if hello source of hello log message provides a way toodistribute messages across many partitions, you could use hello following entity schema:</span></span>  

![][29]

<span data-ttu-id="15f93-828">不過，與此結構描述的 hello 問題是所有 hello 必須搜尋的記錄檔訊息的特定時間範圍為該 tooretrieve hello 資料表中的每個資料分割。</span><span class="sxs-lookup"><span data-stu-id="15f93-828">However, hello problem with this schema is that tooretrieve all hello log messages for a specific time span you must search every partition in hello table.</span></span>

#### <a name="solution"></a><span data-ttu-id="15f93-829">方案</span><span class="sxs-lookup"><span data-stu-id="15f93-829">Solution</span></span>
<span data-ttu-id="15f93-830">hello 前一個區段反白顯示的 hello 問題嘗試 toouse 的 hello 資料表服務 toostore 記錄項目和建議的兩個，令人滿意，設計。</span><span class="sxs-lookup"><span data-stu-id="15f93-830">hello previous section highlighted hello problem of trying toouse hello Table service toostore log entries and suggested two, unsatisfactory, designs.</span></span> <span data-ttu-id="15f93-831">其中一種解決方案導致 tooa 熱資料分割的記錄檔訊息; 寫入的效能不佳的 hello 風險hello 其他解決方案導致查詢效能不佳因為 hello 需求 tooscan hello 資料表 tooretrieve 記錄檔訊息的特定時間範圍中每個資料分割。</span><span class="sxs-lookup"><span data-stu-id="15f93-831">One solution led tooa hot partition with hello risk of poor performance writing log messages; hello other solution resulted in poor query performance because of hello requirement tooscan every partition in hello table tooretrieve log messages for a specific time span.</span></span> <span data-ttu-id="15f93-832">Blob 儲存體提供更好的解決方案，這種案例，這是 Azure 儲存體分析存放區 hello 記錄資料收集。</span><span class="sxs-lookup"><span data-stu-id="15f93-832">Blob storage offers a better solution for this type of scenario and this is how Azure Storage Analytics stores hello log data it collects.</span></span>  

<span data-ttu-id="15f93-833">本節將概述如何儲存體分析記錄檔將資料儲存在 blob 儲存體當做此方法 toostoring 資料，您通常查詢範圍的說明。</span><span class="sxs-lookup"><span data-stu-id="15f93-833">This section outlines how Storage Analytics stores log data in blob storage as an illustration of this approach toostoring data that you typically query by range.</span></span>  

<span data-ttu-id="15f93-834">Storage Analytics 會以分隔格式將記錄訊息儲存在多個 Blob 中。</span><span class="sxs-lookup"><span data-stu-id="15f93-834">Storage Analytics stores log messages in a delimited format in multiple blobs.</span></span> <span data-ttu-id="15f93-835">hello 分隔的格式可輕鬆用戶端應用程式 tooparse hello 資料 hello 記錄檔訊息中。</span><span class="sxs-lookup"><span data-stu-id="15f93-835">hello delimited format makes it easy for a client application tooparse hello data in hello log message.</span></span>  

<span data-ttu-id="15f93-836">儲存體分析會使用命名慣例，可讓您 toolocate hello blob （或 blob） 包含您要搜尋的 hello 記錄檔訊息的 blob。</span><span class="sxs-lookup"><span data-stu-id="15f93-836">Storage Analytics uses a naming convention for blobs that enables you toolocate hello blob (or blobs) that contain hello log messages for which you are searching.</span></span> <span data-ttu-id="15f93-837">例如，名為"queue/2014/07/31/1800/000001.log"blob 包含相關 toohello hello 小時 18:00 31 自 2014 年 7 月開始的佇列服務的記錄檔訊息。</span><span class="sxs-lookup"><span data-stu-id="15f93-837">For example, a blob named "queue/2014/07/31/1800/000001.log" contains log messages that relate toohello queue service for hello hour starting at 18:00 on 31 July 2014.</span></span> <span data-ttu-id="15f93-838">hello"000001"表示這是第一個記錄檔 hello 這段期間的。</span><span class="sxs-lookup"><span data-stu-id="15f93-838">hello "000001" indicates that this is hello first log file for this period.</span></span> <span data-ttu-id="15f93-839">儲存體分析也會記錄第一次的 hello hello 時間戳記和訊息在 hello blob 的中繼資料儲存在 hello 檔案中的最後一個記錄。</span><span class="sxs-lookup"><span data-stu-id="15f93-839">Storage Analytics also records hello timestamps of hello first and last log messages stored in hello file as part of hello blob's metadata.</span></span> <span data-ttu-id="15f93-840">針對 blob 儲存體可讓您尋找 blob 的名稱前置詞為基礎的容器中的 hello API: toolocate 包含佇列的所有 hello blob 都記錄資料 hello 小時 18:00 開始，您可以使用 hello 前置詞"佇列/2014年/07/31/1800。 」</span><span class="sxs-lookup"><span data-stu-id="15f93-840">hello API for blob storage enables you locate blobs in a container based on a name prefix: toolocate all hello blobs that contain queue log data for hello hour starting at 18:00, you can use hello prefix "queue/2014/07/31/1800."</span></span>  

<span data-ttu-id="15f93-841">儲存體分析內部緩衝區記錄訊息和定期更新 hello 適當 blob 或建立一個新 hello 最新批次的記錄項目。</span><span class="sxs-lookup"><span data-stu-id="15f93-841">Storage Analytics buffers log messages internally and then periodically updates hello appropriate blob or creates a new one with hello latest batch of log entries.</span></span> <span data-ttu-id="15f93-842">這可減少 hello 數目的寫入它必須執行 toohello blob 服務。</span><span class="sxs-lookup"><span data-stu-id="15f93-842">This reduces hello number of writes it must perform toohello blob service.</span></span>  

<span data-ttu-id="15f93-843">如果您在自己的應用程式中實作類似方案，您必須考慮如何 toomanage hello （情形，請撰寫每個記錄項目 tooblob 儲存體） 的可靠性及成本和延展性之間的取捨 (在您的應用程式中緩衝處理更新，撰寫這些 tooblob 儲存批次）。</span><span class="sxs-lookup"><span data-stu-id="15f93-843">If you are implementing a similar solution in your own application, you must consider how toomanage hello trade-off between reliability (writing every log entry tooblob storage as it happens) and cost and scalability (buffering updates in your application and writing them tooblob storage in batches).</span></span>  

#### <a name="issues-and-considerations"></a><span data-ttu-id="15f93-844">問題和考量</span><span class="sxs-lookup"><span data-stu-id="15f93-844">Issues and considerations</span></span>
<span data-ttu-id="15f93-845">請考慮下列點決定 toostore 資料的記錄時的 hello:</span><span class="sxs-lookup"><span data-stu-id="15f93-845">Consider hello following points when deciding how toostore log data:</span></span>  

* <span data-ttu-id="15f93-846">如果您建立的資料表設計可避免產生潛在的熱點資料分割，您可能會發現您無法有效率地存取記錄資料。</span><span class="sxs-lookup"><span data-stu-id="15f93-846">If you create a table design that avoids potential hot partitions, you may find that you cannot access your log data efficiently.</span></span>  
* <span data-ttu-id="15f93-847">tooprocess 記錄資料，用戶端通常需要 tooload 多筆記錄。</span><span class="sxs-lookup"><span data-stu-id="15f93-847">tooprocess log data, a client often needs tooload many records.</span></span>  
* <span data-ttu-id="15f93-848">雖然記錄資料通常是結構化的，Blob 儲存體會是較佳的方案。</span><span class="sxs-lookup"><span data-stu-id="15f93-848">Although log data is often structured, blob storage may be a better solution.</span></span>  

### <a name="implementation-considerations"></a><span data-ttu-id="15f93-849">實作考量</span><span class="sxs-lookup"><span data-stu-id="15f93-849">Implementation considerations</span></span>
<span data-ttu-id="15f93-850">當您實作 hello 先前章節所述的 hello 模式時，本節會討論一些 hello 考量 toobear 記住。</span><span class="sxs-lookup"><span data-stu-id="15f93-850">This section discusses some of hello considerations toobear in mind when you implement hello patterns described in hello previous sections.</span></span> <span data-ttu-id="15f93-851">本章節的大部分會使用以 C# 撰寫的範例使用 hello 儲存體用戶端程式庫 （4.3.0 版 hello 撰寫本文時）。</span><span class="sxs-lookup"><span data-stu-id="15f93-851">Most of this section uses examples written in C# that use hello Storage Client Library (version 4.3.0 at hello time of writing).</span></span>  

### <a name="retrieving-entities"></a><span data-ttu-id="15f93-852">擷取實體</span><span class="sxs-lookup"><span data-stu-id="15f93-852">Retrieving entities</span></span>
<span data-ttu-id="15f93-853">Hello > 一節中所述[設計查詢](#design-for-querying)，hello 最有效率的查詢是點查詢。</span><span class="sxs-lookup"><span data-stu-id="15f93-853">As discussed in hello section [Design for querying](#design-for-querying), hello most efficient query is a point query.</span></span> <span data-ttu-id="15f93-854">不過，在某些情況下您可能需要 tooretrieve 多個實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-854">However, in some scenarios you may need tooretrieve multiple entities.</span></span> <span data-ttu-id="15f93-855">本章節描述使用儲存體用戶端程式庫 hello 一些常見方法 tooretrieving 實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-855">This section describes some common approaches tooretrieving entities using hello Storage Client Library.</span></span>  

#### <a name="executing-a-point-query-using-hello-storage-client-library"></a><span data-ttu-id="15f93-856">執行點查詢使用 hello 儲存體用戶端程式庫</span><span class="sxs-lookup"><span data-stu-id="15f93-856">Executing a point query using hello Storage Client Library</span></span>
<span data-ttu-id="15f93-857">最簡單方式 tooexecute hello 點查詢為 toouse hello**擷取**資料表作業，如下列 C# 程式碼片段的 hello 擷取與實體中所示**PartitionKey**值 「 銷售 」 和**RowKey**的值"212":</span><span class="sxs-lookup"><span data-stu-id="15f93-857">hello easiest way tooexecute a point query is toouse hello **Retrieve** table operation as shown in hello following C# code snippet that retrieves an entity with a **PartitionKey** of value "Sales" and a **RowKey** of value "212":</span></span>  

```csharp
TableOperation retrieveOperation = TableOperation.Retrieve<EmployeeEntity>("Sales", "212");
var retrieveResult = employeeTable.Execute(retrieveOperation);
if (retrieveResult.Result != null)
{
    EmployeeEntity employee = (EmployeeEntity)retrieveResult.Result;
    ...
}  
```

<span data-ttu-id="15f93-858">請注意此範例預期 hello 實體的方式，它會擷取的型別 toobe **EmployeeEntity**。</span><span class="sxs-lookup"><span data-stu-id="15f93-858">Notice how this example expects hello entity it retrieves toobe of type **EmployeeEntity**.</span></span>  

#### <a name="retrieving-multiple-entities-using-linq"></a><span data-ttu-id="15f93-859">使用 LINQ 擷取多個實體</span><span class="sxs-lookup"><span data-stu-id="15f93-859">Retrieving multiple entities using LINQ</span></span>
<span data-ttu-id="15f93-860">您可以搭配使用 LINQ 與儲存體用戶端程式庫，並指定具有 **where** 子句的查詢，以擷取多個實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-860">You can retrieve multiple entities by using LINQ with Storage Client Library and specifying a query with a **where** clause.</span></span> <span data-ttu-id="15f93-861">tooavoid 資料表掃描，您應該永遠包含 hello **PartitionKey**中 hello 值其中子句，並盡可能 hello **RowKey**值 tooavoid 資料表和資料分割掃描。</span><span class="sxs-lookup"><span data-stu-id="15f93-861">tooavoid a table scan, you should always include hello **PartitionKey** value in hello where clause, and if possible hello **RowKey** value tooavoid table and partition scans.</span></span> <span data-ttu-id="15f93-862">hello 表格服務支援一組有限的比較運算子 （大於、 大於或等於、 小於、 小於或等於、 等於、 且不等於） toouse hello 其中子句。</span><span class="sxs-lookup"><span data-stu-id="15f93-862">hello table service supports a limited set of comparison operators (greater than, greater than or equal, less than, less than or equal, equal, and not equal) toouse in hello where clause.</span></span> <span data-ttu-id="15f93-863">hello 下列 C# 程式碼片段會尋找所有 hello 員工開頭的"B"與 (假設該 hello **RowKey**存放區 hello 姓氏) hello 銷售部門 (假設 hello **PartitionKey**儲存 hello 部門名稱）：</span><span class="sxs-lookup"><span data-stu-id="15f93-863">hello following C# code snippet finds all hello employees whose last name starts with "B" (assuming that hello **RowKey** stores hello last name) in hello sales department (assuming hello **PartitionKey** stores hello department name):</span></span>  

```csharp
TableQuery<EmployeeEntity> employeeQuery = employeeTable.CreateQuery<EmployeeEntity>();
var query = (from employee in employeeQuery
            where employee.PartitionKey == "Sales" &&
            employee.RowKey.CompareTo("B") >= 0 &&
            employee.RowKey.CompareTo("C") < 0
            select employee).AsTableQuery();
var employees = query.Execute();  
```

<span data-ttu-id="15f93-864">請注意如何 hello 查詢同時指定**RowKey**和**PartitionKey** tooensure 更佳的效能。</span><span class="sxs-lookup"><span data-stu-id="15f93-864">Notice how hello query specifies both a **RowKey** and a **PartitionKey** tooensure better performance.</span></span>  

<span data-ttu-id="15f93-865">hello 下列程式碼範例示範相當於使用 hello fluent API 的功能 (如需 fluent Api 一般情況下，請參閱[設計 fluent 應用程式開發的應用程式開發介面的最佳作法](http://visualstudiomagazine.com/articles/2013/12/01/best-practices-for-designing-a-fluent-api.aspx)):</span><span class="sxs-lookup"><span data-stu-id="15f93-865">hello following code sample shows equivalent functionality using hello fluent API (for more information about fluent APIs in general, see [Best Practices for Designing a Fluent API](http://visualstudiomagazine.com/articles/2013/12/01/best-practices-for-designing-a-fluent-api.aspx)):</span></span>  

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
> <span data-ttu-id="15f93-866">hello 範例會建立多個**CombineFilters**方法 tooinclude hello 三個篩選條件。</span><span class="sxs-lookup"><span data-stu-id="15f93-866">hello sample nests multiple **CombineFilters** methods tooinclude hello three filter conditions.</span></span>  
> 
> 

#### <a name="retrieving-large-numbers-of-entities-from-a-query"></a><span data-ttu-id="15f93-867">從查詢擷取大量實體</span><span class="sxs-lookup"><span data-stu-id="15f93-867">Retrieving large numbers of entities from a query</span></span>
<span data-ttu-id="15f93-868">最佳查詢會根據 **PartitionKey** 值和 **RowKey** 值傳回個別實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-868">An optimal query returns an individual entity based on a **PartitionKey** value and a **RowKey** value.</span></span> <span data-ttu-id="15f93-869">不過，在某些情況下您可能必須需求 tooreturn hello 相同分割區，或甚至從多個資料分割從多個實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-869">However, in some scenarios you may have a requirement tooreturn many entities from hello same partition or even from many partitions.</span></span>  

<span data-ttu-id="15f93-870">您應該一律會完整測試 hello 應用程式的效能，在這類案例。</span><span class="sxs-lookup"><span data-stu-id="15f93-870">You should always fully test hello performance of your application in such scenarios.</span></span>  

<span data-ttu-id="15f93-871">針對 hello 表格服務的查詢可能會傳回 1,000 個實體最多一次，而且執行五秒的最大值。</span><span class="sxs-lookup"><span data-stu-id="15f93-871">A query against hello table service may return a maximum of 1,000 entities at one time and may execute for a maximum of five seconds.</span></span> <span data-ttu-id="15f93-872">如果 hello 結果集包含超過 1,000 個實體，但如果 hello 查詢未於五秒，內完成，或者如果 hello 查詢跨越 hello 資料分割界限，hello 表格服務會傳回接續 token 的 tooenable hello 用戶端應用程式 toorequest hello下一個實體的集合。</span><span class="sxs-lookup"><span data-stu-id="15f93-872">If hello result set contains more than 1,000 entities, if hello query did not complete within five seconds, or if hello query crosses hello partition boundary, hello Table service returns a continuation token tooenable hello client application toorequest hello next set of entities.</span></span> <span data-ttu-id="15f93-873">如需接續權杖如何運作的詳細資訊，請參閱 [查詢逾時和分頁](http://msdn.microsoft.com/library/azure/dd135718.aspx)。</span><span class="sxs-lookup"><span data-stu-id="15f93-873">For more information about how continuation tokens work, see [Query Timeout and Pagination](http://msdn.microsoft.com/library/azure/dd135718.aspx).</span></span>  

<span data-ttu-id="15f93-874">如果您使用 hello 儲存體用戶端程式庫，它可以自動處理接續 token，因為它從 hello 表格服務會傳回實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-874">If you are using hello Storage Client Library, it can automatically handle continuation tokens for you as it returns entities from hello Table service.</span></span> <span data-ttu-id="15f93-875">hello 下列 C# 程式碼範例使用 hello 儲存體用戶端程式庫會自動處理接續 token 如果 hello 表格服務在回應中傳回：</span><span class="sxs-lookup"><span data-stu-id="15f93-875">hello following C# code sample using hello Storage Client Library automatically handles continuation tokens if hello table service returns them in a response:</span></span>  

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

<span data-ttu-id="15f93-876">下列 C# 程式碼的 hello 明確地處理接續 token:</span><span class="sxs-lookup"><span data-stu-id="15f93-876">hello following C# code handles continuation tokens explicitly:</span></span>  

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

<span data-ttu-id="15f93-877">藉由明確使用接續 token，您可以控制您的應用程式時擷取 hello 下一個區段的資料。</span><span class="sxs-lookup"><span data-stu-id="15f93-877">By using continuation tokens explicitly, you can control when your application retrieves hello next segment of data.</span></span> <span data-ttu-id="15f93-878">例如，如果用戶端應用程式可讓使用者透過儲存在資料表中的 hello 實體的 toopage，使用者可以決定不 toopage 透過讓您的應用程式只會使用接續 token tooretrieve hello 接下來，由 hello 查詢所擷取的所有 hello 實體當 hello 使用者已完成透過 hello 目前區段中的所有 hello 實體分頁區段。</span><span class="sxs-lookup"><span data-stu-id="15f93-878">For example, if your client application enables users toopage through hello entities stored in a table, a user may decide not toopage through all hello entities retrieved by hello query so your application would only use a continuation token tooretrieve hello next segment when hello user had finished paging through all hello entities in hello current segment.</span></span> <span data-ttu-id="15f93-879">這種方法有幾項優點：</span><span class="sxs-lookup"><span data-stu-id="15f93-879">This approach has several benefits:</span></span>  

* <span data-ttu-id="15f93-880">它可讓您從 hello 表格服務資料 tooretrieve toolimit hello 數量和移 hello 網路。</span><span class="sxs-lookup"><span data-stu-id="15f93-880">It enables you toolimit hello amount of data tooretrieve from hello Table service and that you move over hello network.</span></span>  
* <span data-ttu-id="15f93-881">它可讓您 tooperform 非同步 IO.NET 中。</span><span class="sxs-lookup"><span data-stu-id="15f93-881">It enables you tooperform asynchronous IO in .NET.</span></span>  
* <span data-ttu-id="15f93-882">它可讓您 tooserialize hello 接續權杖 toopersistent 儲存體，您可以繼續在 hello 事件中的應用程式當機。</span><span class="sxs-lookup"><span data-stu-id="15f93-882">It enables you tooserialize hello continuation token toopersistent storage so you can continue in hello event of an application crash.</span></span>  

> [!NOTE]
> <span data-ttu-id="15f93-883">接續權杖通常會傳回包含 1000 個實體的區段，但也可能較少。</span><span class="sxs-lookup"><span data-stu-id="15f93-883">A continuation token typically returns a segment containing 1,000 entities, although it may be fewer.</span></span> <span data-ttu-id="15f93-884">這也是如果您限制 hello 使用的查詢傳回的項目數目 hello 案例**採取**tooreturn hello 第 n 個實體符合查閱準則： hello 表格服務可能會傳回包含少於一個沿著 n 個實體的區段使用接續 token 的 tooenable 您 tooretrieve hello 剩餘的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-884">This is also hello case if you limit hello number of entries a query returns by using **Take** tooreturn hello first n entities that match your lookup criteria: hello table service may return a segment containing fewer than n entities along with a continuation token tooenable you tooretrieve hello remaining entities.</span></span>  
> 
> 

<span data-ttu-id="15f93-885">hello 下列 C# 程式碼會示範區段內傳回的實體 toomodify hello 數目的方式：</span><span class="sxs-lookup"><span data-stu-id="15f93-885">hello following C# code shows how toomodify hello number of entities returned inside a segment:</span></span>  

```csharp
employeeQuery.TakeCount = 50;  
```

#### <a name="server-side-projection"></a><span data-ttu-id="15f93-886">伺服器端預測</span><span class="sxs-lookup"><span data-stu-id="15f93-886">Server-side projection</span></span>
<span data-ttu-id="15f93-887">單一實體可以有 too255 內容，並是 up too1 MB 的大小。</span><span class="sxs-lookup"><span data-stu-id="15f93-887">A single entity can have up too255 properties and be up too1 MB in size.</span></span> <span data-ttu-id="15f93-888">查詢 hello 資料表擷取實體時，您可能不需要所有的 hello 屬性，並可避免不必要地傳送資料 （toohelp 降低延遲和成本）。</span><span class="sxs-lookup"><span data-stu-id="15f93-888">When you query hello table and retrieve entities, you may not need all hello properties and can avoid transferring data unnecessarily (toohelp reduce latency and cost).</span></span> <span data-ttu-id="15f93-889">您可以使用您所需要的伺服器端投影 tootransfer 只 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="15f93-889">You can use server-side projection tootransfer just hello properties you need.</span></span> <span data-ttu-id="15f93-890">hello 下列範例是擷取只 hello**電子郵件**屬性 (連同**PartitionKey**， **RowKey**，**時間戳記**，和**ETag**) 從 hello hello 查詢所選取的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-890">hello following example is retrieves just hello **Email** property (along with **PartitionKey**, **RowKey**, **Timestamp**, and **ETag**) from hello entities selected by hello query.</span></span>  

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

<span data-ttu-id="15f93-891">請注意如何 hello **RowKey**值為止，即使它不包含屬性 tooretrieve hello 清單中。</span><span class="sxs-lookup"><span data-stu-id="15f93-891">Notice how hello **RowKey** value is available even though it was not included in hello list of properties tooretrieve.</span></span>  

### <a name="modifying-entities"></a><span data-ttu-id="15f93-892">修改實體</span><span class="sxs-lookup"><span data-stu-id="15f93-892">Modifying entities</span></span>
<span data-ttu-id="15f93-893">hello 儲存體用戶端程式庫可讓您 toomodify 所插入、 刪除和更新的實體儲存 hello 表格服務中的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-893">hello Storage Client Library enables you toomodify your entities stored in hello table service by inserting, deleting, and updating entities.</span></span> <span data-ttu-id="15f93-894">您可以使用 EGTs toobatch 多個插入、 更新和刪除作業所需一起 tooreduce hello 的往返次數，並改善 hello 效能，您的方案。</span><span class="sxs-lookup"><span data-stu-id="15f93-894">You can use EGTs toobatch multiple insert, update, and delete operations together tooreduce hello number of round trips required and improve hello performance of your solution.</span></span>  

<span data-ttu-id="15f93-895">請注意 hello 儲存體用戶端程式庫通常執行 EGT 時擲回例外狀況包含 hello 造成 hello 批次 toofail hello 實體的索引。</span><span class="sxs-lookup"><span data-stu-id="15f93-895">Note that exceptions thrown when hello Storage Client Library executes an EGT typically include hello index of hello entity that caused hello batch toofail.</span></span> <span data-ttu-id="15f93-896">當您偵錯使用 EGT 的程式碼時，這會很有幫助。</span><span class="sxs-lookup"><span data-stu-id="15f93-896">This is helpful when you are debugging code that uses EGTs.</span></span>  

<span data-ttu-id="15f93-897">您也應該考量您的設計會如何影響用戶端應用程式處理並行存取和更新作業的方式。</span><span class="sxs-lookup"><span data-stu-id="15f93-897">You should also consider how your design affects how your client application handles concurrency and update operations.</span></span>  

#### <a name="managing-concurrency"></a><span data-ttu-id="15f93-898">管理並行存取</span><span class="sxs-lookup"><span data-stu-id="15f93-898">Managing concurrency</span></span>
<span data-ttu-id="15f93-899">根據預設，hello 表格服務會實作開放式並行存取檢查等級的個別實體的 hello**插入**，**合併**，和**刪除**作業，雖然您可以針對用戶端 tooforce hello 資料表服務 toobypass 這些檢查。</span><span class="sxs-lookup"><span data-stu-id="15f93-899">By default, hello table service implements optimistic concurrency checks at hello level of individual entities for **Insert**, **Merge**, and **Delete** operations, although it is possible for a client tooforce hello table service toobypass these checks.</span></span> <span data-ttu-id="15f93-900">如需如何 hello 表格服務會管理並行存取的詳細資訊，請參閱[管理 Microsoft Azure 儲存體中的並行存取](storage-concurrency.md)。</span><span class="sxs-lookup"><span data-stu-id="15f93-900">For more information about how hello table service manages concurrency, see  [Managing Concurrency in Microsoft Azure Storage](storage-concurrency.md).</span></span>  

#### <a name="merge-or-replace"></a><span data-ttu-id="15f93-901">合併或取代</span><span class="sxs-lookup"><span data-stu-id="15f93-901">Merge or replace</span></span>
<span data-ttu-id="15f93-902">hello**取代**方法 hello **TableOperation**類別一律會取代 hello 表格服務中的 hello 完整實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-902">hello **Replace** method of hello **TableOperation** class always replaces hello complete entity in hello Table service.</span></span> <span data-ttu-id="15f93-903">如果您未包含屬性 hello 要求中儲存的 hello 實體中存在該屬性時，會移除 hello 要求屬性從 hello 儲存實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-903">If you do not include a property in hello request when that property exists in hello stored entity, hello request removes that property from hello stored entity.</span></span> <span data-ttu-id="15f93-904">除非您想 tooremove 明確來自預存的實體的屬性，您必須在 hello 要求中包含的每個屬性。</span><span class="sxs-lookup"><span data-stu-id="15f93-904">Unless you want tooremove a property explicitly from a stored entity, you must include every property in hello request.</span></span>  

<span data-ttu-id="15f93-905">您可以使用 hello**合併**方法 hello **TableOperation**類別 tooreduce hello 您傳送給 toohello 表格服務時要 tooupdate 實體的資料量。</span><span class="sxs-lookup"><span data-stu-id="15f93-905">You can use hello **Merge** method of hello **TableOperation** class tooreduce hello amount of data that you send toohello Table service when you want tooupdate an entity.</span></span> <span data-ttu-id="15f93-906">hello**合併**方法會取代 hello 實體 hello 要求中包含的屬性值中的 hello 儲存實體中的任何屬性，但保留不變 hello 中的任何屬性儲存 hello 要求中未包含的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-906">hello **Merge** method replaces any properties in hello stored entity with property values from hello entity included in hello request, but leaves intact any properties in hello stored entity that are not included in hello request.</span></span> <span data-ttu-id="15f93-907">如果您有大型的實體，且只需 tooupdate 少數的要求中的屬性，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="15f93-907">This is useful if you have large entities and only need tooupdate a small number of properties in a request.</span></span>  

> [!NOTE]
> <span data-ttu-id="15f93-908">hello**取代**和**合併**方法都失敗 hello 實體不存在。</span><span class="sxs-lookup"><span data-stu-id="15f93-908">hello **Replace** and **Merge** methods fail if hello entity does not exist.</span></span> <span data-ttu-id="15f93-909">或者，您可以使用 hello **InsertOrReplace**和**InsertOrMerge**建立新的實體，如果不存在的方法。</span><span class="sxs-lookup"><span data-stu-id="15f93-909">As an alternative, you can use hello **InsertOrReplace** and **InsertOrMerge** methods that create a new entity if it doesn't exist.</span></span>  
> 
> 

### <a name="working-with-heterogeneous-entity-types"></a><span data-ttu-id="15f93-910">使用異質性實體類型</span><span class="sxs-lookup"><span data-stu-id="15f93-910">Working with heterogeneous entity types</span></span>
<span data-ttu-id="15f93-911">hello 表格服務是*無結構描述*資料表存放區，它表示單一資料表可以儲存多個類型，提供更多的彈性設計的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-911">hello Table service is a *schema-less* table store that means that a single table can store entities of multiple types providing great flexibility in your design.</span></span> <span data-ttu-id="15f93-912">hello 下列範例說明儲存同時使用 employee 和 department 實體的資料表：</span><span class="sxs-lookup"><span data-stu-id="15f93-912">hello following example illustrates a table storing both employee and department entities:</span></span>  

<table>
<tr>
<th><span data-ttu-id="15f93-913">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="15f93-913">PartitionKey</span></span></th>
<th><span data-ttu-id="15f93-914">RowKey</span><span class="sxs-lookup"><span data-stu-id="15f93-914">RowKey</span></span></th>
<th><span data-ttu-id="15f93-915">Timestamp</span><span class="sxs-lookup"><span data-stu-id="15f93-915">Timestamp</span></span></th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="15f93-916">名字</span><span class="sxs-lookup"><span data-stu-id="15f93-916">FirstName</span></span></th>
<th><span data-ttu-id="15f93-917">姓氏</span><span class="sxs-lookup"><span data-stu-id="15f93-917">LastName</span></span></th>
<th><span data-ttu-id="15f93-918">年齡</span><span class="sxs-lookup"><span data-stu-id="15f93-918">Age</span></span></th>
<th><span data-ttu-id="15f93-919">電子郵件</span><span class="sxs-lookup"><span data-stu-id="15f93-919">Email</span></span></th>
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
<th><span data-ttu-id="15f93-920">名字</span><span class="sxs-lookup"><span data-stu-id="15f93-920">FirstName</span></span></th>
<th><span data-ttu-id="15f93-921">姓氏</span><span class="sxs-lookup"><span data-stu-id="15f93-921">LastName</span></span></th>
<th><span data-ttu-id="15f93-922">年齡</span><span class="sxs-lookup"><span data-stu-id="15f93-922">Age</span></span></th>
<th><span data-ttu-id="15f93-923">電子郵件</span><span class="sxs-lookup"><span data-stu-id="15f93-923">Email</span></span></th>
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
<th><span data-ttu-id="15f93-924">DepartmentName</span><span class="sxs-lookup"><span data-stu-id="15f93-924">DepartmentName</span></span></th>
<th><span data-ttu-id="15f93-925">EmployeeCount</span><span class="sxs-lookup"><span data-stu-id="15f93-925">EmployeeCount</span></span></th>
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
<th><span data-ttu-id="15f93-926">名字</span><span class="sxs-lookup"><span data-stu-id="15f93-926">FirstName</span></span></th>
<th><span data-ttu-id="15f93-927">姓氏</span><span class="sxs-lookup"><span data-stu-id="15f93-927">LastName</span></span></th>
<th><span data-ttu-id="15f93-928">年齡</span><span class="sxs-lookup"><span data-stu-id="15f93-928">Age</span></span></th>
<th><span data-ttu-id="15f93-929">電子郵件</span><span class="sxs-lookup"><span data-stu-id="15f93-929">Email</span></span></th>
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

<span data-ttu-id="15f93-930">請注意，每個實體仍必須要有 **PartitionKey**、**RowKey** 和 **Timestamp** 值，但是可以有任何屬性集。</span><span class="sxs-lookup"><span data-stu-id="15f93-930">Note that each entity must still have **PartitionKey**, **RowKey**, and **Timestamp** values, but may have any set of properties.</span></span> <span data-ttu-id="15f93-931">此外，沒有任何實體的型別 tooindicate hello，除非您選擇 toostore 某處該資訊。</span><span class="sxs-lookup"><span data-stu-id="15f93-931">Furthermore, there is nothing tooindicate hello type of an entity unless you choose toostore that information somewhere.</span></span> <span data-ttu-id="15f93-932">有兩種方式來識別 hello 實體類型：</span><span class="sxs-lookup"><span data-stu-id="15f93-932">There are two options for identifying hello entity type:</span></span>  

* <span data-ttu-id="15f93-933">在前面加上 hello 實體型別 toohello **RowKey** (或可能是 hello **PartitionKey**)。</span><span class="sxs-lookup"><span data-stu-id="15f93-933">Prepend hello entity type toohello **RowKey** (or possibly hello **PartitionKey**).</span></span> <span data-ttu-id="15f93-934">例如 **EMPLOYEE_000123**，或以 **DEPARTMENT_SALES** 做為 **RowKey** 值。</span><span class="sxs-lookup"><span data-stu-id="15f93-934">For example, **EMPLOYEE_000123** or **DEPARTMENT_SALES** as **RowKey** values.</span></span>  
* <span data-ttu-id="15f93-935">使用的個別屬性 toorecord hello 實體類型 hello 下表所示。</span><span class="sxs-lookup"><span data-stu-id="15f93-935">Use a separate property toorecord hello entity type as shown in hello table below.</span></span>  

<table>
<tr>
<th><span data-ttu-id="15f93-936">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="15f93-936">PartitionKey</span></span></th>
<th><span data-ttu-id="15f93-937">RowKey</span><span class="sxs-lookup"><span data-stu-id="15f93-937">RowKey</span></span></th>
<th><span data-ttu-id="15f93-938">Timestamp</span><span class="sxs-lookup"><span data-stu-id="15f93-938">Timestamp</span></span></th>
<th></th>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td>
<table>
<tr>
<th><span data-ttu-id="15f93-939">EntityType</span><span class="sxs-lookup"><span data-stu-id="15f93-939">EntityType</span></span></th>
<th><span data-ttu-id="15f93-940">名字</span><span class="sxs-lookup"><span data-stu-id="15f93-940">FirstName</span></span></th>
<th><span data-ttu-id="15f93-941">姓氏</span><span class="sxs-lookup"><span data-stu-id="15f93-941">LastName</span></span></th>
<th><span data-ttu-id="15f93-942">年齡</span><span class="sxs-lookup"><span data-stu-id="15f93-942">Age</span></span></th>
<th><span data-ttu-id="15f93-943">電子郵件</span><span class="sxs-lookup"><span data-stu-id="15f93-943">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="15f93-944">員工</span><span class="sxs-lookup"><span data-stu-id="15f93-944">Employee</span></span></td>
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
<th><span data-ttu-id="15f93-945">EntityType</span><span class="sxs-lookup"><span data-stu-id="15f93-945">EntityType</span></span></th>
<th><span data-ttu-id="15f93-946">名字</span><span class="sxs-lookup"><span data-stu-id="15f93-946">FirstName</span></span></th>
<th><span data-ttu-id="15f93-947">姓氏</span><span class="sxs-lookup"><span data-stu-id="15f93-947">LastName</span></span></th>
<th><span data-ttu-id="15f93-948">年齡</span><span class="sxs-lookup"><span data-stu-id="15f93-948">Age</span></span></th>
<th><span data-ttu-id="15f93-949">電子郵件</span><span class="sxs-lookup"><span data-stu-id="15f93-949">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="15f93-950">員工</span><span class="sxs-lookup"><span data-stu-id="15f93-950">Employee</span></span></td>
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
<th><span data-ttu-id="15f93-951">EntityType</span><span class="sxs-lookup"><span data-stu-id="15f93-951">EntityType</span></span></th>
<th><span data-ttu-id="15f93-952">DepartmentName</span><span class="sxs-lookup"><span data-stu-id="15f93-952">DepartmentName</span></span></th>
<th><span data-ttu-id="15f93-953">EmployeeCount</span><span class="sxs-lookup"><span data-stu-id="15f93-953">EmployeeCount</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="15f93-954">department</span><span class="sxs-lookup"><span data-stu-id="15f93-954">Department</span></span></td>
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
<th><span data-ttu-id="15f93-955">EntityType</span><span class="sxs-lookup"><span data-stu-id="15f93-955">EntityType</span></span></th>
<th><span data-ttu-id="15f93-956">名字</span><span class="sxs-lookup"><span data-stu-id="15f93-956">FirstName</span></span></th>
<th><span data-ttu-id="15f93-957">姓氏</span><span class="sxs-lookup"><span data-stu-id="15f93-957">LastName</span></span></th>
<th><span data-ttu-id="15f93-958">年齡</span><span class="sxs-lookup"><span data-stu-id="15f93-958">Age</span></span></th>
<th><span data-ttu-id="15f93-959">電子郵件</span><span class="sxs-lookup"><span data-stu-id="15f93-959">Email</span></span></th>
</tr>
<tr>
<td><span data-ttu-id="15f93-960">員工</span><span class="sxs-lookup"><span data-stu-id="15f93-960">Employee</span></span></td>
<td></td>
<td></td>
<td></td>
<td></td>
</tr>
</table>
</td>
</tr>
</table>

<span data-ttu-id="15f93-961">hello 第一個選項，前面加上 hello 實體型別 toohello **RowKey**，適合不同類型的兩個實體可能有 hello 可能是否相同機碼值。</span><span class="sxs-lookup"><span data-stu-id="15f93-961">hello first option, prepending hello entity type toohello **RowKey**, is useful if there is a possibility that two entities of different types might have hello same key value.</span></span> <span data-ttu-id="15f93-962">它也會群組相同的型別一起 hello 資料分割中的 hello 的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-962">It also groups entities of hello same type together in hello partition.</span></span>  

<span data-ttu-id="15f93-963">hello 本章節所討論的技術是特別有關 toohello 討論[繼承關聯性](#inheritance-relationships)hello > 一節中本指南前面提及[模型的關聯性](#modelling-relationships)。</span><span class="sxs-lookup"><span data-stu-id="15f93-963">hello techniques discussed in this section are especially relevant toohello discussion [Inheritance relationships](#inheritance-relationships) earlier in this guide in hello section [Modelling relationships](#modelling-relationships).</span></span>  

> [!NOTE]
> <span data-ttu-id="15f93-964">您應該考慮 hello 實體型別值 tooenable 用戶端應用程式 tooevolve POCO 物件中加入版本編號，並使用不同版本。</span><span class="sxs-lookup"><span data-stu-id="15f93-964">You should consider including a version number in hello entity type value tooenable client applications tooevolve POCO objects and work with different versions.</span></span>  
> 
> 

<span data-ttu-id="15f93-965">hello 本節其餘部分描述的一些 hello 儲存體用戶端程式庫中的 hello 功能來協助使用多個實體類型中 hello 相同資料表。</span><span class="sxs-lookup"><span data-stu-id="15f93-965">hello remainder of this section describes some of hello features in hello Storage Client Library that facilitate working with multiple entity types in hello same table.</span></span>  

#### <a name="retrieving-heterogeneous-entity-types"></a><span data-ttu-id="15f93-966">擷取異質性實體類型</span><span class="sxs-lookup"><span data-stu-id="15f93-966">Retrieving heterogeneous entity types</span></span>
<span data-ttu-id="15f93-967">如果您使用 hello 儲存體用戶端程式庫，您必須使用多個實體類型的三個選項。</span><span class="sxs-lookup"><span data-stu-id="15f93-967">If you are using hello Storage Client Library, you have three options for working with multiple entity types.</span></span>  

<span data-ttu-id="15f93-968">如果您知道 hello hello 實體儲存與特定類型**RowKey**和**PartitionKey**值，那麼當您擷取 hello 前兩個範例所示的 hello 實體時，您可以指定 hello 實體類型擷取型別實體**EmployeeEntity**:[執行點查詢使用儲存體用戶端程式庫 hello](#executing-a-point-query-using-the-storage-client-library)和[擷取多個實體使用 LINQ](#retrieving-multiple-entities-using-linq).</span><span class="sxs-lookup"><span data-stu-id="15f93-968">If you know hello type of hello entity stored with a specific **RowKey** and **PartitionKey** values, then you can specify hello entity type when you retrieve hello entity as shown in hello previous two examples that retrieve entities of type **EmployeeEntity**: [Executing a point query using hello Storage Client Library](#executing-a-point-query-using-the-storage-client-library) and [Retrieving multiple entities using LINQ](#retrieving-multiple-entities-using-linq).</span></span>  

<span data-ttu-id="15f93-969">hello 第二個選項為 toouse hello **DynamicTableEntity**類型 （屬性包），而不是具象的 POCO 實體類型 （這個選項可能也改善效能，因為沒有任何需要 tooserialize 和還原序列化 hello 實體太。網路類型）。</span><span class="sxs-lookup"><span data-stu-id="15f93-969">hello second option is toouse hello **DynamicTableEntity** type (a property bag) instead of a concrete POCO entity type (this option may also improve performance because there is no need tooserialize and deserialize hello entity too.NET types).</span></span> <span data-ttu-id="15f93-970">hello 下列 C# 程式碼可能 hello 資料表中擷取多個不同類型的實體，但是會傳回所有的實體做**DynamicTableEntity**執行個體。</span><span class="sxs-lookup"><span data-stu-id="15f93-970">hello following C# code potentially retrieves multiple entities of different types from hello table, but returns all entities as **DynamicTableEntity** instances.</span></span> <span data-ttu-id="15f93-971">然後它會使用 hello **EntityType**屬性 toodetermine hello 類型的每個實體：</span><span class="sxs-lookup"><span data-stu-id="15f93-971">It then uses hello **EntityType** property toodetermine hello type of each entity:</span></span>  

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

<span data-ttu-id="15f93-972">請注意該 tooretrieve 其他屬性，您必須使用 hello **TryGetValue**方法上 hello**屬性**屬性 hello **DynamicTableEntity**類別。</span><span class="sxs-lookup"><span data-stu-id="15f93-972">Note that tooretrieve other properties you must use hello **TryGetValue** method on hello **Properties** property of hello **DynamicTableEntity** class.</span></span>  

<span data-ttu-id="15f93-973">第三個選項是使用 hello toocombine **DynamicTableEntity**型別和**EntityResolver**執行個體。</span><span class="sxs-lookup"><span data-stu-id="15f93-973">A third option is toocombine using hello **DynamicTableEntity** type and an **EntityResolver** instance.</span></span> <span data-ttu-id="15f93-974">這可讓您在 hello tooresolve toomultiple POCO 類型相同的查詢。</span><span class="sxs-lookup"><span data-stu-id="15f93-974">This enables you tooresolve toomultiple POCO types in hello same query.</span></span> <span data-ttu-id="15f93-975">在此範例中，hello **EntityResolver**委派使用 hello **EntityType**屬性 toodistinguish hello 查詢所傳回的 hello 兩個類型的實體之間。</span><span class="sxs-lookup"><span data-stu-id="15f93-975">In this example, hello **EntityResolver** delegate is using hello **EntityType** property toodistinguish between hello two types of entity that hello query returns.</span></span> <span data-ttu-id="15f93-976">hello**解決**方法會使用 hello**解析程式**委派 tooresolve **DynamicTableEntity**執行個體太**TableEntity**執行個體。</span><span class="sxs-lookup"><span data-stu-id="15f93-976">hello **Resolve** method uses hello **resolver** delegate tooresolve **DynamicTableEntity** instances too**TableEntity** instances.</span></span>  

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

#### <a name="modifying-heterogeneous-entity-types"></a><span data-ttu-id="15f93-977">修改異質性實體類型</span><span class="sxs-lookup"><span data-stu-id="15f93-977">Modifying heterogeneous entity types</span></span>
<span data-ttu-id="15f93-978">您不需要實體 toodelete tooknow hello 類型，以及您一律知道 hello 類型的實體，當您將它插入。</span><span class="sxs-lookup"><span data-stu-id="15f93-978">You do not need tooknow hello type of an entity toodelete it, and you always know hello type of an entity when you insert it.</span></span> <span data-ttu-id="15f93-979">不過，您可以使用**DynamicTableEntity**輸入 tooupdate 實體，而不需要知道它的類型和不使用 POCO 實體類別。</span><span class="sxs-lookup"><span data-stu-id="15f93-979">However, you can use **DynamicTableEntity** type tooupdate an entity without knowing its type and without using a POCO entity class.</span></span> <span data-ttu-id="15f93-980">hello 下列程式碼範例會擷取單一實體，並檢查 hello **EmployeeCount**屬性存在，然後再更新它。</span><span class="sxs-lookup"><span data-stu-id="15f93-980">hello following code sample retrieves a single entity, and checks hello **EmployeeCount** property exists before updating it.</span></span>  

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

### <a name="controlling-access-with-shared-access-signatures"></a><span data-ttu-id="15f93-981">使用共用存取簽章控制存取</span><span class="sxs-lookup"><span data-stu-id="15f93-981">Controlling access with Shared Access Signatures</span></span>
<span data-ttu-id="15f93-982">您可以使用共用存取簽章 (SAS) 權杖 tooenable 用戶端應用程式 toomodify （和查詢） 直接不直接與 hello 表格服務的 hello 需要 tooauthenticate 資料表實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-982">You can use Shared Access Signature (SAS) tokens tooenable client applications toomodify (and query) table entities directly without hello need tooauthenticate directly with hello table service.</span></span> <span data-ttu-id="15f93-983">一般而言，有三個主要優點在於 toousing SAS 應用程式中：</span><span class="sxs-lookup"><span data-stu-id="15f93-983">Typically, there are three main benefits toousing SAS in your application:</span></span>  

* <span data-ttu-id="15f93-984">您不需要 toodistribute 您的儲存體帳戶金鑰 tooan 不安全平台 （例如行動裝置） 順序 tooallow 該裝置 tooaccess 和修改 hello 表格服務中的實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-984">You do not need toodistribute your storage account key tooan insecure platform (such as a mobile device) in order tooallow that device tooaccess and modify entities in hello Table service.</span></span>  
* <span data-ttu-id="15f93-985">您可以將某些 hello 工作卸載該 web 和背景工作角色執行中管理您的實體 tooclient 裝置，例如終端使用者電腦和行動裝置。</span><span class="sxs-lookup"><span data-stu-id="15f93-985">You can offload some of hello work that web and worker roles perform in managing your entities tooclient devices such as end-user computers and mobile devices.</span></span>  
* <span data-ttu-id="15f93-986">您可以指派受條件約束和時間限制組的使用權限 tooa 用戶端 （例如 toospecific 資源允許唯讀存取）。</span><span class="sxs-lookup"><span data-stu-id="15f93-986">You can assign a constrained and time limited set of permissions tooa client (such as allowing read-only access toospecific resources).</span></span>  

<span data-ttu-id="15f93-987">如需 hello 表格服務搭配使用 SAS 權杖的詳細資訊，請參閱[使用共用存取簽章 (SAS)](storage-dotnet-shared-access-signature-part-1.md)。</span><span class="sxs-lookup"><span data-stu-id="15f93-987">For more information about using SAS tokens with hello Table service, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span></span>  

<span data-ttu-id="15f93-988">不過，您仍必須產生 hello SAS 權杖來授與用戶端 hello 表格服務中的應用程式 toohello 實體： 您應該這麼做有 tooyour 儲存體帳戶金鑰安全存取的環境中。</span><span class="sxs-lookup"><span data-stu-id="15f93-988">However, you must still generate hello SAS tokens that grant a client application toohello entities in hello table service: you should do this in an environment that has secure access tooyour storage account keys.</span></span> <span data-ttu-id="15f93-989">一般而言，您可以使用 web 或背景工作角色 toogenerate hello SAS 權杖，然後傳遞 toohello 用戶端應用程式需要存取 tooyour 實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-989">Typically, you use a web or worker role toogenerate hello SAS tokens and deliver them toohello client applications that need access tooyour entities.</span></span> <span data-ttu-id="15f93-990">因為仍有負荷參與產生與傳遞 SAS 權杖 tooclients，您應該考慮如何最佳 tooreduce 這種負荷，尤其是在大量狀況。</span><span class="sxs-lookup"><span data-stu-id="15f93-990">Because there is still an overhead involved in generating and delivering SAS tokens tooclients, you should consider how best tooreduce this overhead, especially in high-volume scenarios.</span></span>  

<span data-ttu-id="15f93-991">很可能 toogenerate SAS 權杖授與存取的資料表中的 hello 實體 tooa 子集。</span><span class="sxs-lookup"><span data-stu-id="15f93-991">It is possible toogenerate a SAS token that grants access tooa subset of hello entities in a table.</span></span> <span data-ttu-id="15f93-992">根據預設，您會建立 SAS 權杖的一整個資料表，但也可能 toospecify 多種該 hello SAS 權杖授與存取 tooeither **PartitionKey**值或一系列**PartitionKey**和**RowKey**值。</span><span class="sxs-lookup"><span data-stu-id="15f93-992">By default, you create a SAS token for an entire table, but it is also possible toospecify that hello SAS token grant access tooeither a range of **PartitionKey** values, or a range of **PartitionKey** and **RowKey** values.</span></span> <span data-ttu-id="15f93-993">您可能會選擇 toogenerate SAS 權杖，針對個別使用者的系統，每個使用者的 SAS 權杖只允許它們存取 tootheir 自己實體在 hello 表格服務。</span><span class="sxs-lookup"><span data-stu-id="15f93-993">You might choose toogenerate SAS tokens for individual users of your system such that each user's SAS token only allows them access tootheir own entities in hello table service.</span></span>  

### <a name="asynchronous-and-parallel-operations"></a><span data-ttu-id="15f93-994">非同步和平行作業</span><span class="sxs-lookup"><span data-stu-id="15f93-994">Asynchronous and parallel operations</span></span>
<span data-ttu-id="15f93-995">假設您要跨多個資料分割分散您的要求，您可以使用非同步或平行查詢來改善輸送量和用戶端的回應性。</span><span class="sxs-lookup"><span data-stu-id="15f93-995">Provided you are spreading your requests across multiple partitions, you can improve throughput and client responsiveness by using asynchronous or parallel queries.</span></span>
<span data-ttu-id="15f93-996">例如，您可以用兩個或更多背景工作角色執行個體，以平行方式存取您的資料表。</span><span class="sxs-lookup"><span data-stu-id="15f93-996">For example, you might have two or more worker role instances accessing your tables in parallel.</span></span> <span data-ttu-id="15f93-997">您無法個別的背景工作角色負責特定集合的資料分割，或只需要多個背景工作角色執行個體，每個無法 tooaccess 所有 hello 資料表中的資料分割。</span><span class="sxs-lookup"><span data-stu-id="15f93-997">You could have individual worker roles responsible for particular sets of partitions, or simply have multiple worker role instances, each able tooaccess all hello partitions in a table.</span></span>  

<span data-ttu-id="15f93-998">在用戶端執行個體中，您可以藉由以非同步方式執行儲存作業來提高輸送量。</span><span class="sxs-lookup"><span data-stu-id="15f93-998">Within a client instance, you can improve throughput by executing storage operations asynchronously.</span></span> <span data-ttu-id="15f93-999">hello 儲存體用戶端程式庫可讓您輕鬆 toowrite 非同步查詢的修改。</span><span class="sxs-lookup"><span data-stu-id="15f93-999">hello Storage Client Library makes it easy toowrite asynchronous queries and modifications.</span></span> <span data-ttu-id="15f93-1000">例如，您可能會開始 hello 同步方法，可擷取所有資料分割中的 hello 實體 hello 下列 C# 程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="15f93-1000">For example, you might start with hello synchronous method that retrieves all hello entities in a partition as shown in hello following C# code:</span></span>  

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

<span data-ttu-id="15f93-1001">因此該 hello 查詢執行以非同步方式，如下所示，您可以輕鬆地修改這段程式碼：</span><span class="sxs-lookup"><span data-stu-id="15f93-1001">You can easily modify this code so that hello query runs asynchronously as follows:</span></span>  

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

<span data-ttu-id="15f93-1002">在非同步範例中，您可以看到從 hello 同步版本的 hello 下列變更：</span><span class="sxs-lookup"><span data-stu-id="15f93-1002">In this asynchronous example, you can see hello following changes from hello synchronous version:</span></span>  

* <span data-ttu-id="15f93-1003">hello 方法簽章現在包含 hello**非同步**修飾詞，並傳回**工作**執行個體。</span><span class="sxs-lookup"><span data-stu-id="15f93-1003">hello method signature now includes hello **async** modifier and returns a **Task** instance.</span></span>  
* <span data-ttu-id="15f93-1004">而不是呼叫 hello **ExecuteSegmented**方法 tooretrieve 結果、 hello 方法現在呼叫 hello **ExecuteSegmentedAsync**方法，並使用 hello **await**修飾詞tooretrieve 會以非同步方式產生。</span><span class="sxs-lookup"><span data-stu-id="15f93-1004">Instead of calling hello **ExecuteSegmented** method tooretrieve results, hello method now calls hello **ExecuteSegmentedAsync** method and uses hello **await** modifier tooretrieve results asynchronously.</span></span>  

<span data-ttu-id="15f93-1005">hello 用戶端應用程式可以呼叫這個方法多次 (具有不同的值為 hello**部門**參數)，每個查詢將會在另一個執行緒上執行。</span><span class="sxs-lookup"><span data-stu-id="15f93-1005">hello client application can call this method multiple times (with different values for hello **department** parameter), and each query will run on a separate thread.</span></span>  

<span data-ttu-id="15f93-1006">請注意，沒有任何非同步版的 hello **Execute**方法在 hello **TableQuery**類別，因為 hello **IEnumerable**介面不支援非同步列舉型別。</span><span class="sxs-lookup"><span data-stu-id="15f93-1006">Note that there is no asynchronous version of hello **Execute** method in hello **TableQuery** class because hello **IEnumerable** interface does not support asynchronous enumeration.</span></span>  

<span data-ttu-id="15f93-1007">您也可以透過非同步方式插入、更新和刪除實體。</span><span class="sxs-lookup"><span data-stu-id="15f93-1007">You can also insert, update, and delete entities asynchronously.</span></span> <span data-ttu-id="15f93-1008">hello 下列 C# 範例會示範簡單的同步方法 tooinsert 或取代員工實體：</span><span class="sxs-lookup"><span data-stu-id="15f93-1008">hello following C# example shows a simple, synchronous method tooinsert or replace an employee entity:</span></span>  

```csharp
private static void SimpleEmployeeUpsert(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = employeeTable
        .Execute(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

<span data-ttu-id="15f93-1009">您可以輕鬆地修改這段程式碼，使 hello 更新會以非同步方式，如下所示執行：</span><span class="sxs-lookup"><span data-stu-id="15f93-1009">You can easily modify this code so that hello update runs asynchronously as follows:</span></span>  

```csharp
private static async Task SimpleEmployeeUpsertAsync(CloudTable employeeTable,
        EmployeeEntity employee)
{
        TableResult result = await employeeTable
        .ExecuteAsync(TableOperation.InsertOrReplace(employee));
        Console.WriteLine("HTTP Status: {0}", result.HttpStatusCode);
}  
```

<span data-ttu-id="15f93-1010">在非同步範例中，您可以看到從 hello 同步版本的 hello 下列變更：</span><span class="sxs-lookup"><span data-stu-id="15f93-1010">In this asynchronous example, you can see hello following changes from hello synchronous version:</span></span>  

* <span data-ttu-id="15f93-1011">hello 方法簽章現在包含 hello**非同步**修飾詞，並傳回**工作**執行個體。</span><span class="sxs-lookup"><span data-stu-id="15f93-1011">hello method signature now includes hello **async** modifier and returns a **Task** instance.</span></span>  
* <span data-ttu-id="15f93-1012">而不是呼叫 hello **Execute**方法 tooupdate hello 實體、 hello 方法現在呼叫 hello **ExecuteAsync**方法，並使用 hello **await** tooretrieve 修飾詞以非同步方式產生。</span><span class="sxs-lookup"><span data-stu-id="15f93-1012">Instead of calling hello **Execute** method tooupdate hello entity, hello method now calls hello **ExecuteAsync** method and uses hello **await** modifier tooretrieve results asynchronously.</span></span>  

<span data-ttu-id="15f93-1013">hello 用戶端應用程式可以呼叫這類，多個非同步方法，而且每個方法引動過程會在個別的執行緒上執行。</span><span class="sxs-lookup"><span data-stu-id="15f93-1013">hello client application can call multiple asynchronous methods like this one, and each method invocation will run on a separate thread.</span></span>  

### <a name="credits"></a><span data-ttu-id="15f93-1014">學分</span><span class="sxs-lookup"><span data-stu-id="15f93-1014">Credits</span></span>
<span data-ttu-id="15f93-1015">我們想要遵循的 hello Azure 團隊的成員 toothank hello: Dominic Betts、 Jason Hogg、 Jean Ghanem、 Jai Haridas、 Jeff Irwin、 Vamshidhar Kommineni、 Vinay Shah Serdar Ozler 以及 Microsoft DX 從 Tom Hollander。</span><span class="sxs-lookup"><span data-stu-id="15f93-1015">We would like toothank hello following members of hello Azure team for their contributions: Dominic Betts, Jason Hogg, Jean Ghanem, Jai Haridas, Jeff Irwin, Vamshidhar Kommineni, Vinay Shah and Serdar Ozler as well as  Tom Hollander from Microsoft DX.</span></span> 

<span data-ttu-id="15f93-1016">我們也想依照其寶貴的意見反應檢閱循環期間 Microsoft MVP toothank hello: Igor Papirov 和 Edward Bakker。</span><span class="sxs-lookup"><span data-stu-id="15f93-1016">We would also like toothank hello following Microsoft MVP's for their valuable feedback during review cycles: Igor Papirov and Edward Bakker.</span></span>

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

