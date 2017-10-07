---
title: "在 Azure 搜尋 aaaHow toomodel 複雜資料型別 |Microsoft 文件"
description: "在 Azure 搜尋服務索引中，可以使用扁平化資料列集和 Collections 資料類型來模型化巢狀或階層式資料結構。"
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: complex data types; compound data types; aggregate data types
ms.assetid: e4bf86b4-497a-4179-b09f-c1b56c3c0bb2
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: b330c5b322f4f33123a454be11733b977684b9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomodel-complex-data-types-in-azure-search"></a><span data-ttu-id="82e20-103">如何 toomodel 複雜資料類型在 Azure 搜尋</span><span class="sxs-lookup"><span data-stu-id="82e20-103">How toomodel complex data types in Azure Search</span></span>
<span data-ttu-id="82e20-104">外部資料集使用的 toopopulate Azure 搜尋索引有時會包括階層式或巢狀執行不細分整齊為表格式資料列集的子結構。</span><span class="sxs-lookup"><span data-stu-id="82e20-104">External datasets used toopopulate an Azure Search index sometimes include hierarchical or nested substructures that do not break down neatly into a tabular rowset.</span></span> <span data-ttu-id="82e20-105">這類結構的範例可能包含單一客戶的多個位置和電話號碼、單一 SKU 的多種色彩和大小、單一書籍的多位作者等等。</span><span class="sxs-lookup"><span data-stu-id="82e20-105">Examples of such structures might include multiple locations and phone numbers for a single customer, multiple colors and sizes for a single SKU, multiple authors of a single book, and so on.</span></span> <span data-ttu-id="82e20-106">在模型化詞彙，您可能會看到這些結構稱為 tooas*複雜資料型別*，*複合資料型別*，*複合資料類型*，或*彙總資料型別*，幾 tooname。</span><span class="sxs-lookup"><span data-stu-id="82e20-106">In modeling terms, you might see these structures referred tooas *complex data types*, *compound data types*, *composite data types*, or *aggregate data types*, tooname a few.</span></span>

<span data-ttu-id="82e20-107">在 Azure 搜尋中，原生不支援複雜資料型別，但是經過證實的因應措施包括扁平化 hello 結構，然後使用兩步驟程序**集合**資料型別 tooreconstitute hello 內部結構。</span><span class="sxs-lookup"><span data-stu-id="82e20-107">Complex data types are not natively supported in Azure Search, but a proven workaround includes a two-step process of flattening hello structure and then using a **Collection** data type tooreconstitute hello interior structure.</span></span> <span data-ttu-id="82e20-108">遵循本文章中所描述的 hello 技術可讓 hello 內容 toobe 搜尋、 多面向，排序和篩選。</span><span class="sxs-lookup"><span data-stu-id="82e20-108">Following hello technique described in this article allows hello content toobe searched, faceted, filtered, and sorted.</span></span>

## <a name="example-of-a-complex-data-structure"></a><span data-ttu-id="82e20-109">複雜資料結構的範例</span><span class="sxs-lookup"><span data-stu-id="82e20-109">Example of a complex data structure</span></span>
<span data-ttu-id="82e20-110">一般而言，有問題的 hello 資料位於為一組 JSON 或 XML 文件或 NoSQL 存放區，例如 Azure Cosmos DB 中的項目。</span><span class="sxs-lookup"><span data-stu-id="82e20-110">Typically, hello data in question resides as a set of JSON or XML documents, or as items in a NoSQL store such as Azure Cosmos DB.</span></span> <span data-ttu-id="82e20-111">從結構來說，hello 挑戰源自於具有多個子項目需要 toobe 搜尋和篩選。</span><span class="sxs-lookup"><span data-stu-id="82e20-111">Structurally, hello challenge stems from having multiple child items that need toobe searched and filtered.</span></span>  <span data-ttu-id="82e20-112">做為起點圖解 hello 因應措施，採取下列 JSON 文件，其中列出一組連絡人做為範例的 hello:</span><span class="sxs-lookup"><span data-stu-id="82e20-112">As a starting point for illustrating hello workaround, take hello following JSON document that lists a set of contacts as an example:</span></span>

~~~~~
[
  {
    "id": "1",
    "name": "John Smith",
    "company": "Adventureworks",
    "locations": [
      {
        "id": "1",
        "description": "Adventureworks Headquarters"
      },
      {
        "id": "2",
        "description": "Home Office"
      }
    ]
  }, 
  {
    "id": "2",
    "name": "Jen Campbell",
    "company": "Northwind",
    "locations": [
      {
        "id": "3",
        "description": "Northwind Headquarter"
      },
      {
        "id": "4",
        "description": "Home Office"
      }
    ]
}]
~~~~~

<span data-ttu-id="82e20-113">雖然 hello 欄位分別名為 'id'，'name' 和 '公司' 可以輕易地對應一對一 Azure 搜尋索引內的欄位，hello 'locations' 欄位包含陣列的位置，這兩個一組的位置識別碼為位置的描述。</span><span class="sxs-lookup"><span data-stu-id="82e20-113">While hello fields named ‘id’, ‘name’ and ‘company’ can easily be mapped one-to-one as fields within an Azure Search index, hello ‘locations’ field contains an array of locations, having both a set of location IDs as well as location descriptions.</span></span> <span data-ttu-id="82e20-114">鑑於 Azure 搜尋並沒有支援的資料類型，我們需要不同的方式 toomodel 這在 Azure 搜尋中。</span><span class="sxs-lookup"><span data-stu-id="82e20-114">Given that Azure Search does not have a data type that supports this, we need a different way toomodel this in Azure Search.</span></span> 

> [!NOTE]
> <span data-ttu-id="82e20-115">這項技術也描述 Kirk Evans 部落格文章中[使用 Azure 搜尋索引的 DocumentDB](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/)，其中顯示稱為 「 簡維 hello 資料 」，讓您必須呼叫欄位的技術`locationsID`和`locationsDescription`兩者都可[集合](https://msdn.microsoft.com/library/azure/dn798938.aspx)（或字串陣列）。</span><span class="sxs-lookup"><span data-stu-id="82e20-115">This technique is also described by Kirk Evans in a blog post [Indexing DocumentDB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), which shows a technique called "flattening hello data", whereby you would have a field called `locationsID` and `locationsDescription` that are both [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span>   
> 
> 

## <a name="part-1-flatten-hello-array-into-individual-fields"></a><span data-ttu-id="82e20-116">第 1 部分： Hello 陣列扁平化成個別的欄位</span><span class="sxs-lookup"><span data-stu-id="82e20-116">Part 1: Flatten hello array into individual fields</span></span>
<span data-ttu-id="82e20-117">toocreate Azure 搜尋索引，此資料集，以提供可建立 hello 巢狀的子結構的個別欄位：`locationsID`和`locationsDescription`資料類型為[集合](https://msdn.microsoft.com/library/azure/dn798938.aspx)（或字串陣列）。</span><span class="sxs-lookup"><span data-stu-id="82e20-117">toocreate an Azure Search index that accommodates this dataset, create individual fields for hello nested substructure: `locationsID` and `locationsDescription` with a data type of [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span> <span data-ttu-id="82e20-118">這些欄位中您會在中的索引 hello 值 '1' 與 '2' hello `locationsID` '3' 和 '4' 到 hello John Smith 和 hello 值欄位`locationsID`Jen Campbell 欄位。</span><span class="sxs-lookup"><span data-stu-id="82e20-118">In these fields you would index hello values ‘1’ and ‘2’ into hello `locationsID` field for John Smith and hello values ‘3’ & ‘4’ into hello `locationsID` field for Jen Campbell.</span></span>  

<span data-ttu-id="82e20-119">Azure 搜尋服務中的資料如下所示︰</span><span class="sxs-lookup"><span data-stu-id="82e20-119">Your data within Azure Search would look like this:</span></span> 

![範例資料，2 個資料列](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-hello-index-definition"></a><span data-ttu-id="82e20-121">第 2 部分： Hello 索引定義中加入的集合欄位</span><span class="sxs-lookup"><span data-stu-id="82e20-121">Part 2: Add a collection field in hello index definition</span></span>
<span data-ttu-id="82e20-122">Hello 的索引結構描述中 hello 欄位定義看起來類似 toothis 範例。</span><span class="sxs-lookup"><span data-stu-id="82e20-122">In hello index schema, hello field definitions might look similar toothis example.</span></span>

~~~~
var index = new Index()
{
    Name = indexName,
    Fields = new[]
    {
        new Field("id", DataType.String) { IsKey = true },
        new Field("name", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("company", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("locationsId", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true },
        new Field("locationsDescription", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true }
    }
};
~~~~

## <a name="validate-search-behaviors-and-optionally-extend-hello-index"></a><span data-ttu-id="82e20-123">驗證搜尋行為，並選擇性地擴充 hello 索引</span><span class="sxs-lookup"><span data-stu-id="82e20-123">Validate search behaviors and optionally extend hello index</span></span>
<span data-ttu-id="82e20-124">假設您建立的 hello 索引和載入的 hello 資料，您現在可以測試 hello 方案 tooverify 搜尋針對查詢執行 hello 資料集。</span><span class="sxs-lookup"><span data-stu-id="82e20-124">Assuming you created hello index and loaded hello data, you can now test hello solution tooverify search query execution against hello dataset.</span></span> <span data-ttu-id="82e20-125">每個 **collection** 欄位都應該**可搜尋**、**可篩選**和**可 Facet 處理**。</span><span class="sxs-lookup"><span data-stu-id="82e20-125">Each **collection** field should be **searchable**, **filterable** and **facetable**.</span></span> <span data-ttu-id="82e20-126">您應該能夠 toorun 查詢：</span><span class="sxs-lookup"><span data-stu-id="82e20-126">You should be able toorun queries like:</span></span>

* <span data-ttu-id="82e20-127">尋找所有在 hello 'Adventureworks 總部' 工作的人。</span><span class="sxs-lookup"><span data-stu-id="82e20-127">Find all people who work at hello ‘Adventureworks Headquarters’.</span></span>
* <span data-ttu-id="82e20-128">取得使用者都會在家庭辦公室 ' 中的 hello 數目計數。</span><span class="sxs-lookup"><span data-stu-id="82e20-128">Get a count of hello number of people who work in a ‘Home Office’.</span></span>  
* <span data-ttu-id="82e20-129">人員在家庭辦公室 ' hello 人員，顯示其運作的每個位置中的 hello 人員計數以及哪些其他辦公室。</span><span class="sxs-lookup"><span data-stu-id="82e20-129">Of hello people who work at a ‘Home Office’, show what other offices they work along with a count of hello people in each location.</span></span>  

<span data-ttu-id="82e20-130">這項技術，不過落的位置是當您需要 toodo 結合 hello 位置識別碼以及 hello 位置描述的搜尋。</span><span class="sxs-lookup"><span data-stu-id="82e20-130">Where this technique falls apart is when you need toodo a search that combines both hello location id as well as hello location description.</span></span> <span data-ttu-id="82e20-131">例如：</span><span class="sxs-lookup"><span data-stu-id="82e20-131">For example:</span></span>

* <span data-ttu-id="82e20-132">尋找所有具有「家庭辦公室」且位置識別碼為 4 的人員。</span><span class="sxs-lookup"><span data-stu-id="82e20-132">Find all people where they have a Home Office AND has a location ID of 4.</span></span>  

<span data-ttu-id="82e20-133">如果您還記得 hello 原始內容看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="82e20-133">If you recall hello original content looked like this:</span></span>

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

<span data-ttu-id="82e20-134">不過，現在，我們有 hello 資料分成個別的欄位中，我們有無從得知如果 hello Jen Campbell 的家庭辦公室與太有關`locationsID 3`或`locationsID 4`。</span><span class="sxs-lookup"><span data-stu-id="82e20-134">However, now that we have separated hello data into separate fields, we have no way of knowing if hello Home Office for Jen Campbell relates too`locationsID 3` or `locationsID 4`.</span></span>  

<span data-ttu-id="82e20-135">toohandle 這種情況下，定義另一個欄位 hello 索引中，將所有 hello 資料結合成單一集合。</span><span class="sxs-lookup"><span data-stu-id="82e20-135">toohandle this case, define another field in hello index that combines all of hello data into a single collection.</span></span>  <span data-ttu-id="82e20-136">範例中，我們會呼叫此欄位`locationsCombined`，我們將不同 hello 內容`||`雖然您可以選擇任何分隔符號，您將會是一組唯一的字元為您的內容。</span><span class="sxs-lookup"><span data-stu-id="82e20-136">For our example, we will call this field `locationsCombined` and we will separate hello content with a `||` although you can choose any separator that you think would be a unique set of characters for your content.</span></span> <span data-ttu-id="82e20-137">例如：</span><span class="sxs-lookup"><span data-stu-id="82e20-137">For example:</span></span> 

![範例資料，含分隔符號的 2 個資料列](./media/search-howto-complex-data-types/sample-data-2.png)

<span data-ttu-id="82e20-139">使用此 `locationsCombined` 欄位中，我們現在即可容納更多查詢，例如︰</span><span class="sxs-lookup"><span data-stu-id="82e20-139">Using this `locationsCombined` field, we can now accommodate even more queries, such as:</span></span>

* <span data-ttu-id="82e20-140">顯示在位置識別碼為 '4' 的「家庭辦公室」工作的人員計數。</span><span class="sxs-lookup"><span data-stu-id="82e20-140">Show a count of people who work at a ‘Home Office’ with location Id of ‘4’.</span></span>  
* <span data-ttu-id="82e20-141">搜尋在位置識別碼為 '4' 的「家庭辦公室」工作的人員。</span><span class="sxs-lookup"><span data-stu-id="82e20-141">Search for people who work at a ‘Home Office’ with location Id ‘4’.</span></span> 

## <a name="limitations"></a><span data-ttu-id="82e20-142">限制</span><span class="sxs-lookup"><span data-stu-id="82e20-142">Limitations</span></span>
<span data-ttu-id="82e20-143">這個技巧可用於許多案例，但並不適用於每個案例。</span><span class="sxs-lookup"><span data-stu-id="82e20-143">This technique is useful for a number of scenarios, but it is not applicable in every case.</span></span>  <span data-ttu-id="82e20-144">例如：</span><span class="sxs-lookup"><span data-stu-id="82e20-144">For example:</span></span>

1. <span data-ttu-id="82e20-145">如果複雜資料型別中沒有一組靜態欄位，而且沒有任何方式 toomap 所有 hello 可能都類型 tooa 單一欄位。</span><span class="sxs-lookup"><span data-stu-id="82e20-145">If you do not have a static set of fields in your complex data type and there was no way toomap all hello possible types tooa single field.</span></span> 
2. <span data-ttu-id="82e20-146">更新 hello 巢狀物件，將需要一些額外的工作 toodetermine 確實需要什麼 toobe hello Azure 搜尋索引中更新</span><span class="sxs-lookup"><span data-stu-id="82e20-146">Updating hello nested objects requires some extra work toodetermine exactly what needs toobe updated in hello Azure Search index</span></span>

## <a name="sample-code"></a><span data-ttu-id="82e20-147">範例程式碼</span><span class="sxs-lookup"><span data-stu-id="82e20-147">Sample code</span></span>
<span data-ttu-id="82e20-148">您可以如何 tooindex 複雜的 JSON 資料設定成 Azure 搜尋中查看範例，並透過此資料集的這個執行的查詢數目[GitHub 儲存機制](https://github.com/liamca/AzureSearchComplexTypes)。</span><span class="sxs-lookup"><span data-stu-id="82e20-148">You can see an example on how tooindex a complex JSON data set into Azure Search and perform a number of queries over this dataset at this [GitHub repo](https://github.com/liamca/AzureSearchComplexTypes).</span></span>

## <a name="next-step"></a><span data-ttu-id="82e20-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="82e20-149">Next step</span></span>
<span data-ttu-id="82e20-150">[複雜資料類型的原生支援的投票](https://feedback.azure.com/forums/263029-azure-search)hello Azure 搜尋 UserVoice 在頁面上，並提供任何其他輸入您想要我們 tooconsider 有關功能的實作。</span><span class="sxs-lookup"><span data-stu-id="82e20-150">[Vote for native support for complex data types](https://feedback.azure.com/forums/263029-azure-search) on hello Azure Search UserVoice page and provide any additional input that you’d like us tooconsider regarding feature implementation.</span></span> <span data-ttu-id="82e20-151">您也可以將與直接在 Twitter 上 toome @liamca。</span><span class="sxs-lookup"><span data-stu-id="82e20-151">You can also reach out toome directly on Twitter at @liamca.</span></span>

