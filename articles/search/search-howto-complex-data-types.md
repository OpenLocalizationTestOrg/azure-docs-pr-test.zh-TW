---
title: "如何在 Azure 搜尋服務中模型化複雜資料類型 | Microsoft Docs"
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
ms.openlocfilehash: d576fd7bb267ae7a100589413185b595e3b2be42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-model-complex-data-types-in-azure-search"></a><span data-ttu-id="7edb5-103">如何在 Azure 搜尋服務中模型化複雜資料類型</span><span class="sxs-lookup"><span data-stu-id="7edb5-103">How to model complex data types in Azure Search</span></span>
<span data-ttu-id="7edb5-104">用來填入 Azure 搜尋服務索引的外部資料集，有時包含不會整齊細分成表格式資料列集的階層式或巢狀子結構。</span><span class="sxs-lookup"><span data-stu-id="7edb5-104">External datasets used to populate an Azure Search index sometimes include hierarchical or nested substructures that do not break down neatly into a tabular rowset.</span></span> <span data-ttu-id="7edb5-105">這類結構的範例可能包含單一客戶的多個位置和電話號碼、單一 SKU 的多種色彩和大小、單一書籍的多位作者等等。</span><span class="sxs-lookup"><span data-stu-id="7edb5-105">Examples of such structures might include multiple locations and phone numbers for a single customer, multiple colors and sizes for a single SKU, multiple authors of a single book, and so on.</span></span> <span data-ttu-id="7edb5-106">就模型化而論，您可能會看到這些結構稱之為「複雜資料類型」、「複合資料類型」、「合成資料類型」或「彙總資料類型」等等。</span><span class="sxs-lookup"><span data-stu-id="7edb5-106">In modeling terms, you might see these structures referred to as *complex data types*, *compound data types*, *composite data types*, or *aggregate data types*, to name a few.</span></span>

<span data-ttu-id="7edb5-107">Azure 搜尋服務中原先不支援複雜資料類型，但經過實證的因應措施包括結構扁平化的程序 (包含兩個步驟)，然後使用 **Collection** 資料類型來重新構成內部結構。</span><span class="sxs-lookup"><span data-stu-id="7edb5-107">Complex data types are not natively supported in Azure Search, but a proven workaround includes a two-step process of flattening the structure and then using a **Collection** data type to reconstitute the interior structure.</span></span> <span data-ttu-id="7edb5-108">遵循本文所述的技巧，以便搜尋、Facet 處理、篩選和排序內容。</span><span class="sxs-lookup"><span data-stu-id="7edb5-108">Following the technique described in this article allows the content to be searched, faceted, filtered, and sorted.</span></span>

## <a name="example-of-a-complex-data-structure"></a><span data-ttu-id="7edb5-109">複雜資料結構的範例</span><span class="sxs-lookup"><span data-stu-id="7edb5-109">Example of a complex data structure</span></span>
<span data-ttu-id="7edb5-110">一般而言，有問題的資料會以一組 JSON 或 XML 文件的形式存在，或以項目形式存在於 NoSQL 存放區 (例如 Azure Cosmos DB)。</span><span class="sxs-lookup"><span data-stu-id="7edb5-110">Typically, the data in question resides as a set of JSON or XML documents, or as items in a NoSQL store such as Azure Cosmos DB.</span></span> <span data-ttu-id="7edb5-111">在結構上，挑戰源自於有多個需要搜尋和篩選的子項目。</span><span class="sxs-lookup"><span data-stu-id="7edb5-111">Structurally, the challenge stems from having multiple child items that need to be searched and filtered.</span></span>  <span data-ttu-id="7edb5-112">在說明因應措施時，請首先採用下列 JSON 文件，其中列出一組連絡人做為範例︰</span><span class="sxs-lookup"><span data-stu-id="7edb5-112">As a starting point for illustrating the workaround, take the following JSON document that lists a set of contacts as an example:</span></span>

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

<span data-ttu-id="7edb5-113">雖然名為 ‘id’、‘name’ 和 ‘company’ 的欄位可以輕易地逐一對應成 Azure 搜尋服務索引中的欄位，但 ‘locations’ 欄位包含位置陣列，並有一組位置識別碼以及位置描述。</span><span class="sxs-lookup"><span data-stu-id="7edb5-113">While the fields named ‘id’, ‘name’ and ‘company’ can easily be mapped one-to-one as fields within an Azure Search index, the ‘locations’ field contains an array of locations, having both a set of location IDs as well as location descriptions.</span></span> <span data-ttu-id="7edb5-114">假設 Azure 搜尋服務沒有支援此方法的資料類型，我們需要在 Azure 搜尋服務中進行模型化的不同方法。</span><span class="sxs-lookup"><span data-stu-id="7edb5-114">Given that Azure Search does not have a data type that supports this, we need a different way to model this in Azure Search.</span></span> 

> [!NOTE]
> <span data-ttu-id="7edb5-115">Kirk Evans 也會在部落格文章 [Indexing DocumentDB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/) 中說明這個技巧，文中顯示稱為「資料扁平化」的技巧，因此您會有稱為 `locationsID` 和 `locationsDescription` 的欄位 (兩者皆為 [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (或字串陣列))。</span><span class="sxs-lookup"><span data-stu-id="7edb5-115">This technique is also described by Kirk Evans in a blog post [Indexing DocumentDB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), which shows a technique called "flattening the data", whereby you would have a field called `locationsID` and `locationsDescription` that are both [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span>   
> 
> 

## <a name="part-1-flatten-the-array-into-individual-fields"></a><span data-ttu-id="7edb5-116">第 1 部分︰將陣列壓平成為個別的欄位</span><span class="sxs-lookup"><span data-stu-id="7edb5-116">Part 1: Flatten the array into individual fields</span></span>
<span data-ttu-id="7edb5-117">若要建立可容納此資料集的 Azure 搜尋服務索引，請為巢狀子結構建立個別的欄位︰資料類型為 [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (或字串陣列) 的 `locationsID` 和 `locationsDescription`。</span><span class="sxs-lookup"><span data-stu-id="7edb5-117">To create an Azure Search index that accommodates this dataset, create individual fields for the nested substructure: `locationsID` and `locationsDescription` with a data type of [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span> <span data-ttu-id="7edb5-118">在這些欄位中，您會將值 '1' 和 '2' 的索引編製成 John Smith 的 `locationsID` 欄位，將值 '3' 和 '4' 的索引編製成 Jen Campbell 的 `locationsID` 欄位。</span><span class="sxs-lookup"><span data-stu-id="7edb5-118">In these fields you would index the values ‘1’ and ‘2’ into the `locationsID` field for John Smith and the values ‘3’ & ‘4’ into the `locationsID` field for Jen Campbell.</span></span>  

<span data-ttu-id="7edb5-119">Azure 搜尋服務中的資料如下所示︰</span><span class="sxs-lookup"><span data-stu-id="7edb5-119">Your data within Azure Search would look like this:</span></span> 

![範例資料，2 個資料列](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-the-index-definition"></a><span data-ttu-id="7edb5-121">第 2 部分︰在索引定義中加入 collection 欄位</span><span class="sxs-lookup"><span data-stu-id="7edb5-121">Part 2: Add a collection field in the index definition</span></span>
<span data-ttu-id="7edb5-122">在索引結構描述中，欄位定義看起來類似此範例。</span><span class="sxs-lookup"><span data-stu-id="7edb5-122">In the index schema, the field definitions might look similar to this example.</span></span>

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

## <a name="validate-search-behaviors-and-optionally-extend-the-index"></a><span data-ttu-id="7edb5-123">驗證搜尋行為並選擇性地擴充索引</span><span class="sxs-lookup"><span data-stu-id="7edb5-123">Validate search behaviors and optionally extend the index</span></span>
<span data-ttu-id="7edb5-124">假設您已建立索引並載入資料，您現在即可測試解決方案，以驗證對資料集執行的搜尋查詢。</span><span class="sxs-lookup"><span data-stu-id="7edb5-124">Assuming you created the index and loaded the data, you can now test the solution to verify search query execution against the dataset.</span></span> <span data-ttu-id="7edb5-125">每個 **collection** 欄位都應該**可搜尋**、**可篩選**和**可 Facet 處理**。</span><span class="sxs-lookup"><span data-stu-id="7edb5-125">Each **collection** field should be **searchable**, **filterable** and **facetable**.</span></span> <span data-ttu-id="7edb5-126">您應該能夠執行下列查詢︰</span><span class="sxs-lookup"><span data-stu-id="7edb5-126">You should be able to run queries like:</span></span>

* <span data-ttu-id="7edb5-127">尋找所有在 ‘Adventureworks Headquarters’ 工作的人員。</span><span class="sxs-lookup"><span data-stu-id="7edb5-127">Find all people who work at the ‘Adventureworks Headquarters’.</span></span>
* <span data-ttu-id="7edb5-128">取得在「家庭辦公室」工作的人員計數。</span><span class="sxs-lookup"><span data-stu-id="7edb5-128">Get a count of the number of people who work in a ‘Home Office’.</span></span>  
* <span data-ttu-id="7edb5-129">在「家庭辦公室」工作的人員中，顯示他們在其他哪些辦公室工作以及每個位置的人員計數。</span><span class="sxs-lookup"><span data-stu-id="7edb5-129">Of the people who work at a ‘Home Office’, show what other offices they work along with a count of the people in each location.</span></span>  

<span data-ttu-id="7edb5-130">當您需要進行結合位置識別碼和位置描述的搜尋時，這個技巧就不管用。</span><span class="sxs-lookup"><span data-stu-id="7edb5-130">Where this technique falls apart is when you need to do a search that combines both the location id as well as the location description.</span></span> <span data-ttu-id="7edb5-131">例如：</span><span class="sxs-lookup"><span data-stu-id="7edb5-131">For example:</span></span>

* <span data-ttu-id="7edb5-132">尋找所有具有「家庭辦公室」且位置識別碼為 4 的人員。</span><span class="sxs-lookup"><span data-stu-id="7edb5-132">Find all people where they have a Home Office AND has a location ID of 4.</span></span>  

<span data-ttu-id="7edb5-133">如果您還記得原始內容看起來如下︰</span><span class="sxs-lookup"><span data-stu-id="7edb5-133">If you recall the original content looked like this:</span></span>

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

<span data-ttu-id="7edb5-134">不過，既然我們已將資料分成個別的欄位，我們便無法得知 Jen Campbell 的家庭辦公室是否與 `locationsID 3` 或 `locationsID 4` 相關。</span><span class="sxs-lookup"><span data-stu-id="7edb5-134">However, now that we have separated the data into separate fields, we have no way of knowing if the Home Office for Jen Campbell relates to `locationsID 3` or `locationsID 4`.</span></span>  

<span data-ttu-id="7edb5-135">若要處理這種情況，請在索引中定義另一個可將所有資料結合成單一集合的欄位。</span><span class="sxs-lookup"><span data-stu-id="7edb5-135">To handle this case, define another field in the index that combines all of the data into a single collection.</span></span>  <span data-ttu-id="7edb5-136">此範例中，我們將此欄位稱為 `locationsCombined` 並將以 `||` 分隔內容，雖然您可以為您的內容選擇任何您認為是一組獨特字元的分隔符號。</span><span class="sxs-lookup"><span data-stu-id="7edb5-136">For our example, we will call this field `locationsCombined` and we will separate the content with a `||` although you can choose any separator that you think would be a unique set of characters for your content.</span></span> <span data-ttu-id="7edb5-137">例如：</span><span class="sxs-lookup"><span data-stu-id="7edb5-137">For example:</span></span> 

![範例資料，含分隔符號的 2 個資料列](./media/search-howto-complex-data-types/sample-data-2.png)

<span data-ttu-id="7edb5-139">使用此 `locationsCombined` 欄位中，我們現在即可容納更多查詢，例如︰</span><span class="sxs-lookup"><span data-stu-id="7edb5-139">Using this `locationsCombined` field, we can now accommodate even more queries, such as:</span></span>

* <span data-ttu-id="7edb5-140">顯示在位置識別碼為 '4' 的「家庭辦公室」工作的人員計數。</span><span class="sxs-lookup"><span data-stu-id="7edb5-140">Show a count of people who work at a ‘Home Office’ with location Id of ‘4’.</span></span>  
* <span data-ttu-id="7edb5-141">搜尋在位置識別碼為 '4' 的「家庭辦公室」工作的人員。</span><span class="sxs-lookup"><span data-stu-id="7edb5-141">Search for people who work at a ‘Home Office’ with location Id ‘4’.</span></span> 

## <a name="limitations"></a><span data-ttu-id="7edb5-142">限制</span><span class="sxs-lookup"><span data-stu-id="7edb5-142">Limitations</span></span>
<span data-ttu-id="7edb5-143">這個技巧可用於許多案例，但並不適用於每個案例。</span><span class="sxs-lookup"><span data-stu-id="7edb5-143">This technique is useful for a number of scenarios, but it is not applicable in every case.</span></span>  <span data-ttu-id="7edb5-144">例如：</span><span class="sxs-lookup"><span data-stu-id="7edb5-144">For example:</span></span>

1. <span data-ttu-id="7edb5-145">如果您的複雜資料類型中沒有一組靜態欄位，而且沒有辦法將所有可能的類型對應至單一欄位。</span><span class="sxs-lookup"><span data-stu-id="7edb5-145">If you do not have a static set of fields in your complex data type and there was no way to map all the possible types to a single field.</span></span> 
2. <span data-ttu-id="7edb5-146">更新巢狀物件時需要一些額外的工作，才能精確地判斷需要在 Azure 搜尋服務索引中更新的內容</span><span class="sxs-lookup"><span data-stu-id="7edb5-146">Updating the nested objects requires some extra work to determine exactly what needs to be updated in the Azure Search index</span></span>

## <a name="sample-code"></a><span data-ttu-id="7edb5-147">範例程式碼</span><span class="sxs-lookup"><span data-stu-id="7edb5-147">Sample code</span></span>
<span data-ttu-id="7edb5-148">您可以看到範例說明如何在 Azure 搜尋服務中編製複雜 JSON 資料集的索引，並且在 [GitHub 儲存機制](https://github.com/liamca/AzureSearchComplexTypes)對此資料集執行多項查詢。</span><span class="sxs-lookup"><span data-stu-id="7edb5-148">You can see an example on how to index a complex JSON data set into Azure Search and perform a number of queries over this dataset at this [GitHub repo](https://github.com/liamca/AzureSearchComplexTypes).</span></span>

## <a name="next-step"></a><span data-ttu-id="7edb5-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7edb5-149">Next step</span></span>
<span data-ttu-id="7edb5-150">[票選複雜資料類型的原生支援](https://feedback.azure.com/forums/263029-azure-search) ，並提供您希望我們對於功能實作考量的任何其他輸入。</span><span class="sxs-lookup"><span data-stu-id="7edb5-150">[Vote for native support for complex data types](https://feedback.azure.com/forums/263029-azure-search) on the Azure Search UserVoice page and provide any additional input that you’d like us to consider regarding feature implementation.</span></span> <span data-ttu-id="7edb5-151">您也可以直接在 Twitter 上透過 @liamca 聯繫我。</span><span class="sxs-lookup"><span data-stu-id="7edb5-151">You can also reach out to me directly on Twitter at @liamca.</span></span>

