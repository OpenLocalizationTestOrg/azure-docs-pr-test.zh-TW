---
title: "Azure 搜尋服務多種語言 | Microsoft Docs"
description: "Azure 搜尋服務支援 56 種語言，運用來自 Lucene 的語言分析器和來自 Microsoft 的自然語言處理技術。"
services: search
documentationcenter: 
author: yahnoosh
manager: pablocas
editor: 
ms.assetid: 55a00b44-804d-41bb-9c96-e6ea498616f5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: jlembicz
ms.openlocfilehash: dbbab31bac66ce73dbf9883992713a2c16581e19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a><span data-ttu-id="09f30-103">在 Azure 搜尋服務中建立多種語言的文件索引</span><span class="sxs-lookup"><span data-stu-id="09f30-103">Create an index for documents in multiple languages in Azure Search</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="09f30-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="09f30-104">Portal</span></span>](search-language-support.md)
> * [<span data-ttu-id="09f30-105">REST</span><span class="sxs-lookup"><span data-stu-id="09f30-105">REST</span></span>](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [<span data-ttu-id="09f30-106">.NET</span><span class="sxs-lookup"><span data-stu-id="09f30-106">.NET</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

<span data-ttu-id="09f30-107">揭開語言分析器的強大功能，就如同在索引定義中的可搜尋欄位上設定一個屬性一樣簡單。</span><span class="sxs-lookup"><span data-stu-id="09f30-107">Unleashing the power of language analyzers is as easy as setting one property on a searchable field in the index definition.</span></span> <span data-ttu-id="09f30-108">您現在可以在入口網站中執行這個步驟。</span><span class="sxs-lookup"><span data-stu-id="09f30-108">Now you can do this step in the portal.</span></span>

<span data-ttu-id="09f30-109">以下是 Azure 搜尋服務的 Azure 入口網站刀鋒視窗螢幕擷取畫面，可供使用者定義索引結構描述。</span><span class="sxs-lookup"><span data-stu-id="09f30-109">Below are screenshots of the Azure Portal blades for Azure Search that allow users to define an index schema.</span></span> <span data-ttu-id="09f30-110">在這個刀鋒視窗中，使用者可以建立所有欄位並設定各欄位的分析器屬性。</span><span class="sxs-lookup"><span data-stu-id="09f30-110">From this blade, users can create all of the fields and set the analyzer property for each of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09f30-111">如同在從頭建立新索引時，或將新欄位加入至現有索引時，您只能在欄位定義期間設定語言分析器。</span><span class="sxs-lookup"><span data-stu-id="09f30-111">You can only set a language analyzer during field definition, as in when creating a new index from the ground up, or when adding a new field to an existing index.</span></span> <span data-ttu-id="09f30-112">確保您建立欄位時完全指定所有的屬性 (包括分析器)。</span><span class="sxs-lookup"><span data-stu-id="09f30-112">Make sure you fully specify all attributes, including the analyzer, while creating the field.</span></span> <span data-ttu-id="09f30-113">儲存變更後，您將無法編輯屬性或變更分析器類型。</span><span class="sxs-lookup"><span data-stu-id="09f30-113">You won't be able to edit the attributes or change the analyzer type once you save your changes.</span></span>
>
>

## <a name="define-a-new-field-definition"></a><span data-ttu-id="09f30-114">定義新的欄位定義</span><span class="sxs-lookup"><span data-stu-id="09f30-114">Define a new field definition</span></span>
1. <span data-ttu-id="09f30-115">登入 [Azure 入口網站](https://portal.azure.com) 並開啟您的搜尋服務的服務刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="09f30-115">Sign in to the [Azure portal](https://portal.azure.com) and open the service blade of your search service.</span></span>
2. <span data-ttu-id="09f30-116">在服務儀表板頂端的命令列中按一下 [新增索引]  即可開始新的索引，或開啟現有索引以在您加入至現有索引的新欄位上設定分析器。</span><span class="sxs-lookup"><span data-stu-id="09f30-116">Click **Add index** in the command bar at the top of the service dashboard to start a new index, or open an existing index to set an analyzer on new fields you're adding to an existing index.</span></span>
3. <span data-ttu-id="09f30-117">[欄位] 刀鋒視窗隨即出現，顯示可供您定義索引結構描述的選項，包括用於選擇語言分析器的 [分析器] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="09f30-117">The Fields blade appears, giving you options for defining the schema of the index, including the Analyzer tab used for choosing a language analyzer.</span></span>
4. <span data-ttu-id="09f30-118">在 [欄位] 中，藉由提供名稱、選擇資料類型，以及設定屬性來開始欄位定義，進而將欄位標示為可全文檢索搜尋、可在搜尋結果中擷取，可用於 facet 導覽結構中、可排序等等。</span><span class="sxs-lookup"><span data-stu-id="09f30-118">In Fields, start a field definition by providing a name, choosing the data type, and setting attributes to mark the field as full text searchable, retrievable in search results, usable in facet navigation structures, sortable, and so forth.</span></span>
5. <span data-ttu-id="09f30-119">在移到下一個欄位之前，開啟 [分析器]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="09f30-119">Before moving on to the next field, open the **Analyzer** tab.</span></span>

<span data-ttu-id="09f30-120">![][1]
*若要選取分析器，請按一下 [欄位] 刀鋒視窗上的 [分析器] 索引標籤*</span><span class="sxs-lookup"><span data-stu-id="09f30-120">![][1]
*To select an analyzer, click the Analyzer tab on the Fields blade*</span></span>

## <a name="choose-an-analyzer"></a><span data-ttu-id="09f30-121">選擇分析器</span><span class="sxs-lookup"><span data-stu-id="09f30-121">Choose an analyzer</span></span>
1. <span data-ttu-id="09f30-122">捲動以尋找您要定義的欄位。</span><span class="sxs-lookup"><span data-stu-id="09f30-122">Scroll to find the field you are defining.</span></span>
2. <span data-ttu-id="09f30-123">如果您沒有將此欄位標示為搜尋，請立即按一下此核取方塊將其標示為 **Searchable**。</span><span class="sxs-lookup"><span data-stu-id="09f30-123">If you haven't marked the field as searchable, click the checkbox now to mark it as **Searchable**.</span></span>
3. <span data-ttu-id="09f30-124">按一下 [分析器] 區域以顯示可用的分析器清單。</span><span class="sxs-lookup"><span data-stu-id="09f30-124">Click the Analyzer area to display the list of available analyzers.</span></span>
4. <span data-ttu-id="09f30-125">選擇您要使用的分析器。</span><span class="sxs-lookup"><span data-stu-id="09f30-125">Choose the analyzer you want to use.</span></span>

<span data-ttu-id="09f30-126">![][2]
*為每個欄位選取其中一個支援的分析器*</span><span class="sxs-lookup"><span data-stu-id="09f30-126">![][2]
*Select one of the supported analyzers for each field*</span></span>

<span data-ttu-id="09f30-127">根據預設，所有可搜尋的欄位都可使用 [標準 Lucene 分析器](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) (語言中立)。</span><span class="sxs-lookup"><span data-stu-id="09f30-127">By default, all searchable fields use the [Standard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) which is language agnostic.</span></span> <span data-ttu-id="09f30-128">若要檢視支援分析器的完整清單，請參閱 [Azure 搜尋服務的語言支援](https://msdn.microsoft.com/library/azure/dn879793.aspx)。</span><span class="sxs-lookup"><span data-stu-id="09f30-128">To view the full list of supported analyzers, see [Language Support in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span></span>

<span data-ttu-id="09f30-129">一旦針對某個欄位選取語言分析器，它將用於該欄位的每個索引和搜尋要求。</span><span class="sxs-lookup"><span data-stu-id="09f30-129">Once the language analyzer is selected for a field, it will be used with each indexing and search request for that field.</span></span> <span data-ttu-id="09f30-130">使用不同的分析器針對多個欄位發出查詢時，查詢將由每個欄位的右分析器獨立處理。</span><span class="sxs-lookup"><span data-stu-id="09f30-130">When a query is issued against multiple fields using different analyzers, the query will be processed independently by the right analyzers for each field.</span></span>

<span data-ttu-id="09f30-131">許多 Web 和行動應用程式使用不同的語言來服務世界各地的使用者。</span><span class="sxs-lookup"><span data-stu-id="09f30-131">Many web and mobile applications serve users around the globe using different languages.</span></span> <span data-ttu-id="09f30-132">有可能藉由為每種支援語言建立一個欄位，以定義這類案例的索引。</span><span class="sxs-lookup"><span data-stu-id="09f30-132">It’s possible to define an index for a scenario like this by creating a field for each language supported.</span></span>

<span data-ttu-id="09f30-133">![][3]
*每種支援語言都有一個描述欄位的索引定義*</span><span class="sxs-lookup"><span data-stu-id="09f30-133">![][3]
*Index definition with a description field for each language supported*</span></span>

<span data-ttu-id="09f30-134">如果已知發出查詢之代理程式的語言，則可使用 **searchFields** 查詢參數將搜尋要求的範圍限制為特定欄位。</span><span class="sxs-lookup"><span data-stu-id="09f30-134">If the language of the agent issuing a query is known, a search request can be scoped to a specific field using the **searchFields** query parameter.</span></span> <span data-ttu-id="09f30-135">下列查詢只會針對波蘭文描述發出：</span><span class="sxs-lookup"><span data-stu-id="09f30-135">The following query will be issued only against the description in Polish:</span></span>

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

<span data-ttu-id="09f30-136">您可以使用 [搜尋總管]  貼上類似上述的查詢，便可從入口網站查詢您的索引。</span><span class="sxs-lookup"><span data-stu-id="09f30-136">You can query your index from the portal, using **Search explorer** to paste in a query similar to the one shown above.</span></span> <span data-ttu-id="09f30-137">從服務刀鋒視窗的命令列可以存取搜尋總管。</span><span class="sxs-lookup"><span data-stu-id="09f30-137">Search explorer is available from the command bar in the service blade.</span></span> <span data-ttu-id="09f30-138">如需詳細資料，請參閱 [在入口網站查詢 Azure 搜尋服務索引](search-explorer.md) 。</span><span class="sxs-lookup"><span data-stu-id="09f30-138">See [Query your Azure Search index in the portal](search-explorer.md) for details.</span></span>

<span data-ttu-id="09f30-139">有時候不知道發出查詢之代理程式的語言，在此情況下，可以針對所有欄位同時發出查詢。</span><span class="sxs-lookup"><span data-stu-id="09f30-139">Sometimes the language of the agent issuing a query is not known, in which case the query can be issued against all fields simultaneously.</span></span> <span data-ttu-id="09f30-140">如有需要，可以使用 [評分設定檔](https://msdn.microsoft.com/library/azure/dn798928.aspx)來定義特定語言之結果的喜好設定。</span><span class="sxs-lookup"><span data-stu-id="09f30-140">If needed, preference for results in a certain language can be defined using [scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span> <span data-ttu-id="09f30-141">在下面範例中，相對於波蘭文和法文的相符項目，在英文描述中找到的相符項目會有較高的評分：</span><span class="sxs-lookup"><span data-stu-id="09f30-141">In the example below, matches found in the description in English will be scored higher relative to matches in Polish and French:</span></span>

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

<span data-ttu-id="09f30-142">如果您是 .NET 開發人員，請注意您可以使用 [Azure 搜尋服務 .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search)來設定語言分析器。</span><span class="sxs-lookup"><span data-stu-id="09f30-142">If you're a .NET developer, note that you can configure language analyzers using the [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span></span> <span data-ttu-id="09f30-143">最新版本包含對 Microsoft 語言分析器的支援。</span><span class="sxs-lookup"><span data-stu-id="09f30-143">The latest release includes support for the Microsoft language analyzers as well.</span></span>

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
