---
title: "搜尋多個語言 aaaAzure |Microsoft 文件"
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
ms.openlocfilehash: 9a2e567a82ee563521c12ea320f6c484a8e73f04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a><span data-ttu-id="4ade0-103">在 Azure 搜尋服務中建立多種語言的文件索引</span><span class="sxs-lookup"><span data-stu-id="4ade0-103">Create an index for documents in multiple languages in Azure Search</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="4ade0-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="4ade0-104">Portal</span></span>](search-language-support.md)
> * [<span data-ttu-id="4ade0-105">REST</span><span class="sxs-lookup"><span data-stu-id="4ade0-105">REST</span></span>](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [<span data-ttu-id="4ade0-106">.NET</span><span class="sxs-lookup"><span data-stu-id="4ade0-106">.NET</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

<span data-ttu-id="4ade0-107">Unleashing hello 的語言分析器功能是，只要在 hello 索引定義中可搜尋的欄位上設定一個屬性。</span><span class="sxs-lookup"><span data-stu-id="4ade0-107">Unleashing hello power of language analyzers is as easy as setting one property on a searchable field in hello index definition.</span></span> <span data-ttu-id="4ade0-108">現在您可以執行此步驟在 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="4ade0-108">Now you can do this step in hello portal.</span></span>

<span data-ttu-id="4ade0-109">以下是 hello 的螢幕擷取畫面 Azure 入口網站的刀鋒視窗的 Azure 搜尋可讓使用者 toodefine 索引結構描述。</span><span class="sxs-lookup"><span data-stu-id="4ade0-109">Below are screenshots of hello Azure Portal blades for Azure Search that allow users toodefine an index schema.</span></span> <span data-ttu-id="4ade0-110">從這個刀鋒視窗中，使用者可以建立您所有的 hello 欄位和 hello 分析器屬性設定為每個。</span><span class="sxs-lookup"><span data-stu-id="4ade0-110">From this blade, users can create all of hello fields and set hello analyzer property for each of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ade0-111">您只能設定語言分析器期間欄位定義中或加入新欄位 tooan 現有索引時，建立新的索引，從 hello 接地。</span><span class="sxs-lookup"><span data-stu-id="4ade0-111">You can only set a language analyzer during field definition, as in when creating a new index from hello ground up, or when adding a new field tooan existing index.</span></span> <span data-ttu-id="4ade0-112">請確定您完整指定所有的屬性，包括建立 hello 欄位時的 hello 分析器。</span><span class="sxs-lookup"><span data-stu-id="4ade0-112">Make sure you fully specify all attributes, including hello analyzer, while creating hello field.</span></span> <span data-ttu-id="4ade0-113">您不會是能 tooedit hello 屬性，或者變更 hello 分析器類型，一旦儲存變更。</span><span class="sxs-lookup"><span data-stu-id="4ade0-113">You won't be able tooedit hello attributes or change hello analyzer type once you save your changes.</span></span>
>
>

## <a name="define-a-new-field-definition"></a><span data-ttu-id="4ade0-114">定義新的欄位定義</span><span class="sxs-lookup"><span data-stu-id="4ade0-114">Define a new field definition</span></span>
1. <span data-ttu-id="4ade0-115">登入 toohello [Azure 入口網站](https://portal.azure.com)和您的搜尋服務開啟 hello 服務刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="4ade0-115">Sign in toohello [Azure portal](https://portal.azure.com) and open hello service blade of your search service.</span></span>
2. <span data-ttu-id="4ade0-116">按一下**新增索引**在 hello 命令列頂端的 hello 服務儀表板 toostart hello 新的索引，或開啟現有的索引 tooset 上您要加入新欄位分析器 tooan 現有的索引。</span><span class="sxs-lookup"><span data-stu-id="4ade0-116">Click **Add index** in hello command bar at hello top of hello service dashboard toostart a new index, or open an existing index tooset an analyzer on new fields you're adding tooan existing index.</span></span>
3. <span data-ttu-id="4ade0-117">hello 欄位刀鋒視窗隨即出現，讓您定義 hello hello 索引結構描述的選項包括 hello 分析器 索引標籤用於選擇語言分析器。</span><span class="sxs-lookup"><span data-stu-id="4ade0-117">hello Fields blade appears, giving you options for defining hello schema of hello index, including hello Analyzer tab used for choosing a language analyzer.</span></span>
4. <span data-ttu-id="4ade0-118">在欄位中，從開始的欄位定義中提供的名稱、 選擇 hello 資料型別，以及設定屬性 toomark hello 欄位做為全文檢索可搜尋、 在搜尋結果中，可用於 facet 瀏覽結構，可擷取可排序、 等等。</span><span class="sxs-lookup"><span data-stu-id="4ade0-118">In Fields, start a field definition by providing a name, choosing hello data type, and setting attributes toomark hello field as full text searchable, retrievable in search results, usable in facet navigation structures, sortable, and so forth.</span></span>
5. <span data-ttu-id="4ade0-119">在繼續 toohello 下一個欄位之前, 開啟 hello**分析器** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="4ade0-119">Before moving on toohello next field, open hello **Analyzer** tab.</span></span>

<span data-ttu-id="4ade0-120">![][1]
*tooselect 分析器 中，按一下 hello hello 欄位刀鋒視窗上的分析師 索引標籤*</span><span class="sxs-lookup"><span data-stu-id="4ade0-120">![][1]
*tooselect an analyzer, click hello Analyzer tab on hello Fields blade*</span></span>

## <a name="choose-an-analyzer"></a><span data-ttu-id="4ade0-121">選擇分析器</span><span class="sxs-lookup"><span data-stu-id="4ade0-121">Choose an analyzer</span></span>
1. <span data-ttu-id="4ade0-122">您會定義捲軸 toofind hello 欄位。</span><span class="sxs-lookup"><span data-stu-id="4ade0-122">Scroll toofind hello field you are defining.</span></span>
2. <span data-ttu-id="4ade0-123">如果您未標示為可搜尋的 hello 欄位，按一下 [hello] 核取方塊現在 toomark 為**Searchable**。</span><span class="sxs-lookup"><span data-stu-id="4ade0-123">If you haven't marked hello field as searchable, click hello checkbox now toomark it as **Searchable**.</span></span>
3. <span data-ttu-id="4ade0-124">按一下 hello 分析器區域 toodisplay hello 清單可用的分析器。</span><span class="sxs-lookup"><span data-stu-id="4ade0-124">Click hello Analyzer area toodisplay hello list of available analyzers.</span></span>
4. <span data-ttu-id="4ade0-125">選擇 hello 分析器想 toouse。</span><span class="sxs-lookup"><span data-stu-id="4ade0-125">Choose hello analyzer you want toouse.</span></span>

<span data-ttu-id="4ade0-126">![][2]
*選取其中一個 hello 支援每個欄位的分析器*</span><span class="sxs-lookup"><span data-stu-id="4ade0-126">![][2]
*Select one of hello supported analyzers for each field*</span></span>

<span data-ttu-id="4ade0-127">根據預設，所有可搜尋的欄位使用 hello[標準 Lucene 分析器](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html)即語言無關。</span><span class="sxs-lookup"><span data-stu-id="4ade0-127">By default, all searchable fields use hello [Standard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) which is language agnostic.</span></span> <span data-ttu-id="4ade0-128">tooview hello 完整的清單支援的分析器，請參閱[Azure 搜尋中支援的語言](https://msdn.microsoft.com/library/azure/dn879793.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4ade0-128">tooview hello full list of supported analyzers, see [Language Support in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span></span>

<span data-ttu-id="4ade0-129">一旦 hello 語言分析器選取欄位，它會搭配每個索引和搜尋要求，該欄位。</span><span class="sxs-lookup"><span data-stu-id="4ade0-129">Once hello language analyzer is selected for a field, it will be used with each indexing and search request for that field.</span></span> <span data-ttu-id="4ade0-130">針對多個欄位，使用不同的分析器發出查詢時，hello 查詢將會每個欄位的 hello 右分析器獨立處理。</span><span class="sxs-lookup"><span data-stu-id="4ade0-130">When a query is issued against multiple fields using different analyzers, hello query will be processed independently by hello right analyzers for each field.</span></span>

<span data-ttu-id="4ade0-131">許多 web 和行動應用程式提供使用不同語言的 hello 全球各地的使用者。</span><span class="sxs-lookup"><span data-stu-id="4ade0-131">Many web and mobile applications serve users around hello globe using different languages.</span></span> <span data-ttu-id="4ade0-132">很可能 toodefine 案例索引以這種方式所建立的欄位，每個支援的語言。</span><span class="sxs-lookup"><span data-stu-id="4ade0-132">It’s possible toodefine an index for a scenario like this by creating a field for each language supported.</span></span>

<span data-ttu-id="4ade0-133">![][3]
*每種支援語言都有一個描述欄位的索引定義*</span><span class="sxs-lookup"><span data-stu-id="4ade0-133">![][3]
*Index definition with a description field for each language supported*</span></span>

<span data-ttu-id="4ade0-134">搜尋要求若為已知 hello hello 代理程式發出查詢語言，可以是已設定領域的 tooa 特定欄位使用 hello **searchFields**查詢參數。</span><span class="sxs-lookup"><span data-stu-id="4ade0-134">If hello language of hello agent issuing a query is known, a search request can be scoped tooa specific field using hello **searchFields** query parameter.</span></span> <span data-ttu-id="4ade0-135">hello 下列查詢將只對發出波蘭文 hello 描述：</span><span class="sxs-lookup"><span data-stu-id="4ade0-135">hello following query will be issued only against hello description in Polish:</span></span>

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

<span data-ttu-id="4ade0-136">您可以查詢您的索引，從 hello 入口網站中，使用**搜尋總管**toopaste 如上所示的其中一個查詢類似 toohello 中。</span><span class="sxs-lookup"><span data-stu-id="4ade0-136">You can query your index from hello portal, using **Search explorer** toopaste in a query similar toohello one shown above.</span></span> <span data-ttu-id="4ade0-137">使用在 hello 服務刀鋒視窗中的 hello 命令列中搜尋總管。</span><span class="sxs-lookup"><span data-stu-id="4ade0-137">Search explorer is available from hello command bar in hello service blade.</span></span> <span data-ttu-id="4ade0-138">請參閱[查詢您的 Azure 搜尋索引 hello 入口網站中](search-explorer.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="4ade0-138">See [Query your Azure Search index in hello portal](search-explorer.md) for details.</span></span>

<span data-ttu-id="4ade0-139">有時候 hello hello 代理程式發出查詢的語言是未知，哪些案例 hello 中查詢可以發送給所有欄位同時。</span><span class="sxs-lookup"><span data-stu-id="4ade0-139">Sometimes hello language of hello agent issuing a query is not known, in which case hello query can be issued against all fields simultaneously.</span></span> <span data-ttu-id="4ade0-140">如有需要，可以使用 [評分設定檔](https://msdn.microsoft.com/library/azure/dn798928.aspx)來定義特定語言之結果的喜好設定。</span><span class="sxs-lookup"><span data-stu-id="4ade0-140">If needed, preference for results in a certain language can be defined using [scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span> <span data-ttu-id="4ade0-141">Hello 下列範例中，在英文版的 hello 描述中找到相符項目將計分較高的相對 toomatches 波蘭文和法文：</span><span class="sxs-lookup"><span data-stu-id="4ade0-141">In hello example below, matches found in hello description in English will be scored higher relative toomatches in Polish and French:</span></span>

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

<span data-ttu-id="4ade0-142">如果您是.NET 開發人員，請注意，您可以設定語言分析器使用 hello [Azure 搜尋.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search)。</span><span class="sxs-lookup"><span data-stu-id="4ade0-142">If you're a .NET developer, note that you can configure language analyzers using hello [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span></span> <span data-ttu-id="4ade0-143">hello 最新版本包含 hello Microsoft 語言分析器也支援。</span><span class="sxs-lookup"><span data-stu-id="4ade0-143">hello latest release includes support for hello Microsoft language analyzers as well.</span></span>

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
