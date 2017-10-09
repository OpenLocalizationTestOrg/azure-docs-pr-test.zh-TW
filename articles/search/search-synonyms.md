---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "Hello 同義字 （預覽） 功能，在 hello Azure 搜尋 REST API 公開的初步文件。"
services: search
documentationCenter: 
authors: mhko
manager: pablocas
editor: 
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/07/2016
ms.author: nateko
ms.openlocfilehash: 2695139d2b298fa2e7c1814715fdf96729f594ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="synonyms-in-azure-search-preview"></a><span data-ttu-id="135ea-102">Azure 搜尋服務的同義字 (預覽)</span><span class="sxs-lookup"><span data-stu-id="135ea-102">Synonyms in Azure Search (preview)</span></span>

<span data-ttu-id="135ea-103">同義字在搜尋引擎中的建立的關聯以隱含方式展開 hello 範圍查詢時，不具有提供 hello 詞彙 tooactually hello 使用者的對等詞彙。</span><span class="sxs-lookup"><span data-stu-id="135ea-103">Synonyms in search engines associate equivalent terms that implicitly expand hello scope of a query, without hello user having tooactually provide hello term.</span></span> <span data-ttu-id="135ea-104">例如，給定的 hello 詞彙"dog"和"canine 」 和 「 小狗"包含"dog"、"canine 」 或 「 小狗"的任何文件的同義字關聯會切換 hello hello 查詢範圍內。</span><span class="sxs-lookup"><span data-stu-id="135ea-104">For example, given hello term "dog" and synonym associations of "canine" and "puppy", any documents containing "dog", "canine" or "puppy" will fall within hello scope of hello query.</span></span>

<span data-ttu-id="135ea-105">在 Azure 搜尋服務中，同義字擴充在查詢同時就已完成。</span><span class="sxs-lookup"><span data-stu-id="135ea-105">In Azure Search, synonym expansion is done at query time.</span></span> <span data-ttu-id="135ea-106">您可以加入同義字地圖 tooa 服務不中斷 tooexisting 作業。</span><span class="sxs-lookup"><span data-stu-id="135ea-106">You can add synonym maps tooa service with no disruption tooexisting operations.</span></span> <span data-ttu-id="135ea-107">您可以加入**synonymMaps**屬性 tooa 欄位定義，而不需要 toorebuild hello 索引。</span><span class="sxs-lookup"><span data-stu-id="135ea-107">You can add a  **synonymMaps** property tooa field definition without having toorebuild hello index.</span></span> <span data-ttu-id="135ea-108">如需詳細資訊，請參閱[更新索引](https://docs.microsoft.com/rest/api/searchservice/update-index)。</span><span class="sxs-lookup"><span data-stu-id="135ea-108">For more information, see [Update Index](https://docs.microsoft.com/rest/api/searchservice/update-index).</span></span>

## <a name="feature-availability"></a><span data-ttu-id="135ea-109">功能可用性</span><span class="sxs-lookup"><span data-stu-id="135ea-109">Feature availability</span></span>

<span data-ttu-id="135ea-110">hello 同義字功能是目前在預覽，並僅支援在 hello 最新預覽的 api 版本 (api 版本 = 2016年-09-01-預覽)。</span><span class="sxs-lookup"><span data-stu-id="135ea-110">hello synonyms feature is currently in preview and only supported in hello latest preview api-version (api-version=2016-09-01-Preview).</span></span> <span data-ttu-id="135ea-111">目前 Azure 入口網站並不支援此功能。</span><span class="sxs-lookup"><span data-stu-id="135ea-111">There is no Azure portal support at this time.</span></span> <span data-ttu-id="135ea-112">因為 hello 要求上指定 hello API 版本，所以可能 toocombine 上市 (GA) 與預覽版 Api hello 中的相同的應用程式。</span><span class="sxs-lookup"><span data-stu-id="135ea-112">Because hello API version is specified on hello request, it's possible toocombine generally available (GA) and preview APIs in hello same app.</span></span> <span data-ttu-id="135ea-113">然而，預覽 API 不受 SLA 約束，且功能可能會變更，因此不建議在生產應用程式中使用。</span><span class="sxs-lookup"><span data-stu-id="135ea-113">However, preview APIs are not under SLA and features may change, so we do not recommend using them in production applications.</span></span>

## <a name="how-toouse-synonyms-in-azure-search"></a><span data-ttu-id="135ea-114">如何在 Azure 中的 toouse 同義字搜尋</span><span class="sxs-lookup"><span data-stu-id="135ea-114">How toouse synonyms in Azure search</span></span>

<span data-ttu-id="135ea-115">在 Azure 搜尋中，同義字支援根據您定義及上傳 tooyour 服務的同義資料表對應。</span><span class="sxs-lookup"><span data-stu-id="135ea-115">In Azure Search, synonym support is based on synonym maps that you define and upload tooyour service.</span></span> <span data-ttu-id="135ea-116">這些地圖由獨立資源構成 (例如索引或資料資源)，且可以在您搜尋服務索引中的任何可搜尋欄位使用。</span><span class="sxs-lookup"><span data-stu-id="135ea-116">These maps constitute an independent resource (like indexes or data sources), and can be used by any searchable field in any index in your search service.</span></span>

<span data-ttu-id="135ea-117">同義字地圖和索引會分開維護。</span><span class="sxs-lookup"><span data-stu-id="135ea-117">Synonym maps and indexes are maintained independently.</span></span> <span data-ttu-id="135ea-118">一旦您定義同義字對應，並將它上傳 tooyour 服務，您可以啟用欄位 hello 同義字功能藉由新增新的屬性稱為**synonymMaps** hello 欄位定義中。</span><span class="sxs-lookup"><span data-stu-id="135ea-118">Once you define a synonym map and upload it tooyour service, you can enable hello synonym feature on a field by adding a new property called **synonymMaps** in hello field definition.</span></span> <span data-ttu-id="135ea-119">建立、 更新和刪除同義字對應一律整個文件的作業，這表示您無法建立，更新，或以累加方式刪除 hello 同義資料表對應的組件。</span><span class="sxs-lookup"><span data-stu-id="135ea-119">Creating, updating, and deleting a synonym map is always a whole-document operation, meaning that you cannot create, update or delete parts of hello synonym map incrementally.</span></span> <span data-ttu-id="135ea-120">即便只是更新一個項目也需要重新載入。</span><span class="sxs-lookup"><span data-stu-id="135ea-120">Updating even a single entry requires a reload.</span></span>

<span data-ttu-id="135ea-121">將同義字整合至您的搜尋應用程式需要兩個步驟：</span><span class="sxs-lookup"><span data-stu-id="135ea-121">Incorporating synonyms into your search application is a two-step process:</span></span>

1.  <span data-ttu-id="135ea-122">新增透過 hello Api 同義字對應 tooyour 搜尋服務。</span><span class="sxs-lookup"><span data-stu-id="135ea-122">Add a synonym map tooyour search service through hello APIs below.</span></span>  

2.  <span data-ttu-id="135ea-123">設定可搜尋欄位 toouse hello 同義字對應 hello 索引定義中。</span><span class="sxs-lookup"><span data-stu-id="135ea-123">Configure a searchable field toouse hello synonym map in hello index definition.</span></span>

### <a name="synonymmaps-resource-apis"></a><span data-ttu-id="135ea-124">SynonymMaps 資源 API</span><span class="sxs-lookup"><span data-stu-id="135ea-124">SynonymMaps Resource APIs</span></span>

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a><span data-ttu-id="135ea-125">使用 POST 或 PUT 在您的服務中新增或更新同義字地圖。</span><span class="sxs-lookup"><span data-stu-id="135ea-125">Add or update a synonym map under your service, using POST or PUT.</span></span>

<span data-ttu-id="135ea-126">同義字對應上傳 toohello 服務透過 POST 或 PUT。</span><span class="sxs-lookup"><span data-stu-id="135ea-126">Synonym maps are uploaded toohello service via POST or PUT.</span></span> <span data-ttu-id="135ea-127">每個規則必須加以分隔 hello 新行字元 ('\n')。</span><span class="sxs-lookup"><span data-stu-id="135ea-127">Each rule must be delimited by hello new line character ('\n').</span></span> <span data-ttu-id="135ea-128">您可以定義 too5、 每個可用的服務中的同義字對應 000 規則和 10,000 規則中其他所有 Sku。</span><span class="sxs-lookup"><span data-stu-id="135ea-128">You can define up too5,000 rules per synonym map in a free service and 10,000 rules in all other SKUs.</span></span> <span data-ttu-id="135ea-129">每個規則可以有向上 too20 展開。</span><span class="sxs-lookup"><span data-stu-id="135ea-129">Each rule can have up too20 expansions.</span></span>

<span data-ttu-id="135ea-130">在此預覽中，同義字對應必須 hello Apache Solr 格式說明如下。</span><span class="sxs-lookup"><span data-stu-id="135ea-130">In this preview, synonym maps must be in hello Apache Solr format which is explained below.</span></span> <span data-ttu-id="135ea-131">如果您有現有的同義字字典格式不同，而且想 toouse 它直接管理，請讓我們知道上[UserVoice](https://feedback.azure.com/forums/263029-azure-search)。</span><span class="sxs-lookup"><span data-stu-id="135ea-131">If you have an existing synonym dictionary in a different format and want toouse it directly, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

<span data-ttu-id="135ea-132">您可以建立新的同義資料表對應，使用 HTTP POST，如 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="135ea-132">You can create a new synonym map using HTTP POST, as in hello following example:</span></span>

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

<span data-ttu-id="135ea-133">或者，您可以使用 PUT，並在 hello URI 上指定 hello 同義資料表對應名稱。</span><span class="sxs-lookup"><span data-stu-id="135ea-133">Alternatively, you can use PUT and specify hello synonym map name on hello URI.</span></span> <span data-ttu-id="135ea-134">如果 hello 同義字對應不存在，則會建立。</span><span class="sxs-lookup"><span data-stu-id="135ea-134">If hello synonym map does not exist, it will be created.</span></span>

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a><span data-ttu-id="135ea-135">Apache Solr 同義字格式</span><span class="sxs-lookup"><span data-stu-id="135ea-135">Apache Solr synonym format</span></span>

<span data-ttu-id="135ea-136">hello Solr 格式支援相等和明確的同義資料表對應。</span><span class="sxs-lookup"><span data-stu-id="135ea-136">hello Solr format supports equivalent and explicit synonym mappings.</span></span> <span data-ttu-id="135ea-137">對應規則遵守 toohello 開放原始碼同義字的 Apache Solr，這份文件中所述的篩選條件規格： [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter)。</span><span class="sxs-lookup"><span data-stu-id="135ea-137">Mapping rules adhere toohello open source synonym filter specification of Apache Solr, described in this document: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter).</span></span> <span data-ttu-id="135ea-138">以下是對等同義字的樣本規則。</span><span class="sxs-lookup"><span data-stu-id="135ea-138">Below is a sample rule for equivalent synonyms.</span></span>
```
              USA, United States, United States of America
```

<span data-ttu-id="135ea-139">與上述規則 hello，搜尋查詢 「 美國 」 將會太展開 「 美國 」 或者 「 美國 」 或者 「 美國 」。</span><span class="sxs-lookup"><span data-stu-id="135ea-139">With hello rule above, a search query "USA" will expand too"USA" OR "United States" OR "United States of America".</span></span>

<span data-ttu-id="135ea-140">明確的對應由箭號「=>」表示。</span><span class="sxs-lookup"><span data-stu-id="135ea-140">Explicit mapping is denoted by an arrow "=>".</span></span> <span data-ttu-id="135ea-141">指定時，符合 hello 左邊的搜尋查詢詞彙序列"= >"會取代右邊 hello hello 替代項目。</span><span class="sxs-lookup"><span data-stu-id="135ea-141">When specified, a term sequence of a search query that matches hello left hand side of "=>" will be replaced with hello alternatives on hello right hand side.</span></span> <span data-ttu-id="135ea-142">指定 hello 規則，搜尋查詢"Washington"，"Wash."</span><span class="sxs-lookup"><span data-stu-id="135ea-142">Given hello rule below, search queries "Washington", "Wash."</span></span> <span data-ttu-id="135ea-143">或"WA"將所有會重新寫入太"WA"。</span><span class="sxs-lookup"><span data-stu-id="135ea-143">or "WA" will all be rewritten too"WA".</span></span> <span data-ttu-id="135ea-144">明確對應只套用在指定的 hello 方向和不太改寫 hello 查詢"WA""Washington"，在此情況下。</span><span class="sxs-lookup"><span data-stu-id="135ea-144">Explicit mapping only applies in hello direction specified and does not rewrite hello query "WA" too"Washington" in this case.</span></span>
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a><span data-ttu-id="135ea-145">您服務中的同義字地圖清單。</span><span class="sxs-lookup"><span data-stu-id="135ea-145">List synonym maps under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a><span data-ttu-id="135ea-146">在您的服務中取得同義字地圖。</span><span class="sxs-lookup"><span data-stu-id="135ea-146">Get a synonym map under your service.</span></span>

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a><span data-ttu-id="135ea-147">刪除您服務中的同義字地圖。</span><span class="sxs-lookup"><span data-stu-id="135ea-147">Delete a synonyms map under your service.</span></span>

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-toouse-hello-synonym-map-in-hello-index-definition"></a><span data-ttu-id="135ea-148">設定可搜尋欄位 toouse hello 同義字對應 hello 索引定義中。</span><span class="sxs-lookup"><span data-stu-id="135ea-148">Configure a searchable field toouse hello synonym map in hello index definition.</span></span>

<span data-ttu-id="135ea-149">新的欄位屬性**synonymMaps**可以是使用的 toospecify 同義字對應 toouse 可搜尋的欄位。</span><span class="sxs-lookup"><span data-stu-id="135ea-149">A new field property **synonymMaps** can be used toospecify a synonym map toouse for a searchable field.</span></span> <span data-ttu-id="135ea-150">同義字對應服務層級的資源，而且可以依索引 hello 服務底下的任何欄位中參考。</span><span class="sxs-lookup"><span data-stu-id="135ea-150">Synonym maps are service level resources and can be referenced by any field of an index under hello service.</span></span>

    POST https://[servicename].search.windows.net/indexes?api-version=2016-09-01-Preview
    api-key: [admin key]

    {
       "name":"myindex",
       "fields":[
          {
             "name":"id",
             "type":"Edm.String",
             "key":true
          },
          {
             "name":"name",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"en.lucene",
             "synonymMaps":[
                "mysynonymmap"
             ]
          },
          {
             "name":"name_jp",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"ja.microsoft",
             "synonymMaps":[
                "japanesesynonymmap"
             ]
          }
       ]
    }

<span data-ttu-id="135ea-151">**synonymMaps**可以指定 hello 型別 'Edm.String' 或 'Collection （edm.string）' 可搜尋的欄位。</span><span class="sxs-lookup"><span data-stu-id="135ea-151">**synonymMaps** can be specified for searchable fields of hello type 'Edm.String' or 'Collection(Edm.String)'.</span></span>

> [!NOTE]
> <span data-ttu-id="135ea-152">在此預覽中，每一個欄位僅能有一個同義字地圖。</span><span class="sxs-lookup"><span data-stu-id="135ea-152">In this preview, you can only have one synonym map per field.</span></span> <span data-ttu-id="135ea-153">如果您想 toouse 多個同義字對應，請讓我們知道上[UserVoice](https://feedback.azure.com/forums/263029-azure-search)。</span><span class="sxs-lookup"><span data-stu-id="135ea-153">If you want toouse multiple synonym maps, please let us know on [UserVoice](https://feedback.azure.com/forums/263029-azure-search).</span></span>

## <a name="impact-of-synonyms-on-other-search-features"></a><span data-ttu-id="135ea-154">同義字對其他搜尋功能的影響</span><span class="sxs-lookup"><span data-stu-id="135ea-154">Impact of synonyms on other search features</span></span>

<span data-ttu-id="135ea-155">hello 同義字功能重寫 hello 原始查詢以 hello OR 運算子的同義字。</span><span class="sxs-lookup"><span data-stu-id="135ea-155">hello synonyms feature rewrites hello original query with synonyms with hello OR operator.</span></span> <span data-ttu-id="135ea-156">基於這個理由，叫用的反白顯示和計分設定檔將 hello 原始詞彙及同義字視為對等項目。</span><span class="sxs-lookup"><span data-stu-id="135ea-156">For this reason, hit highlighting and scoring profiles treat hello original term and synonyms as equivalent.</span></span>

<span data-ttu-id="135ea-157">同義字功能適用於 toosearch 查詢，但不適用於 toofilters 或 facet。</span><span class="sxs-lookup"><span data-stu-id="135ea-157">Synonym feature applies toosearch queries and does not apply toofilters or facets.</span></span> <span data-ttu-id="135ea-158">同樣地，建議根據只 hello 原始詞彙;同義字比對不會出現在 hello 回應。</span><span class="sxs-lookup"><span data-stu-id="135ea-158">Similarly, suggestions are based only on hello original term; synonym matches do not appear in hello response.</span></span>

<span data-ttu-id="135ea-159">同義字擴充不會套用 toowildcard 搜尋詞彙;不展開前置詞，模糊和 regex 條款。</span><span class="sxs-lookup"><span data-stu-id="135ea-159">Synonym expansions do not apply toowildcard search terms; prefix, fuzzy, and regex terms aren't expanded.</span></span>

## <a name="tips-for-building-a-synonym-map"></a><span data-ttu-id="135ea-160">建置同義字地圖的秘訣</span><span class="sxs-lookup"><span data-stu-id="135ea-160">Tips for building a synonym map</span></span>

- <span data-ttu-id="135ea-161">簡潔、 設計良好的同義字地圖比詳盡的可能比對結果清單來得有效率。</span><span class="sxs-lookup"><span data-stu-id="135ea-161">A concise, well-designed synonym map is more efficient than an exhaustive list of possible matches.</span></span> <span data-ttu-id="135ea-162">極大型或複雜的字典需要較長的 tooparse，而且影響 hello 查詢延遲，如果 hello 查詢擴充 toomany 同義字。</span><span class="sxs-lookup"><span data-stu-id="135ea-162">Excessively large or complex dictionaries take longer tooparse and affect hello query latency if hello query expands toomany synonyms.</span></span> <span data-ttu-id="135ea-163">而不是猜測詞彙可能會使用，就可以透過 hello 實際條款[搜尋流量分析報表](search-traffic-analytics.md)。</span><span class="sxs-lookup"><span data-stu-id="135ea-163">Rather than guess at which terms might be used, you can get hello actual terms via a [search traffic analysis report](search-traffic-analytics.md).</span></span>

- <span data-ttu-id="135ea-164">初稿 」 和 「 驗證練習中，為啟用，並使用此報表 tooprecisely 判斷哪些詞彙將受益於同義字比對，然後再繼續 toouse 它做為驗證您的同義資料表對應會產生更好的結果。</span><span class="sxs-lookup"><span data-stu-id="135ea-164">As both a preliminary and validation exercise, enable and then use this report tooprecisely determine which terms will benefit from a synonym match, and then continue toouse it as validation that your synonym map is producing a better outcome.</span></span> <span data-ttu-id="135ea-165">Hello 預先定義的報表中的 hello 磚 「 最常見的搜尋查詢 」 和 「 零結果的搜尋查詢 可讓您 hello 所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="135ea-165">In hello predefined report, hello tiles "Most common search queries" and "Zero-result search queries" will give you hello necessary information.</span></span>

- <span data-ttu-id="135ea-166">您可以為您的搜尋應用程式建立多個同義字地圖 (例如，如果您的應用程式支援多語言的客戶群，您可以建立不同語言的同義字地圖)。</span><span class="sxs-lookup"><span data-stu-id="135ea-166">You can create multiple synonym maps for your search application (for example, by language if your application supports a multi-lingual customer base).</span></span> <span data-ttu-id="135ea-167">目前，一個欄位只能使用一個同義字地圖。</span><span class="sxs-lookup"><span data-stu-id="135ea-167">Currently, a field can only use one of them.</span></span> <span data-ttu-id="135ea-168">您可以隨時更新欄位的 synonymMaps 屬性。</span><span class="sxs-lookup"><span data-stu-id="135ea-168">You can update a field's synonymMaps property at any time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="135ea-169">後續步驟</span><span class="sxs-lookup"><span data-stu-id="135ea-169">Next Steps</span></span>

- <span data-ttu-id="135ea-170">如果您在開發環境中 （非生產環境） 中有現有的索引，試驗小字典 toosee hello 新增同義字如何變更 hello 搜尋經驗，包括計分設定檔、 點擊反白顯示，以及建議的影響。</span><span class="sxs-lookup"><span data-stu-id="135ea-170">If you have an existing index in a development (non-production) environment, experiment with a small dictionary toosee how hello addition of synonyms changes hello search experience, including impact on scoring profiles, hit highlighting, and suggestions.</span></span>

- <span data-ttu-id="135ea-171">[啟用搜尋服務流量分析](search-traffic-analytics.md)和使用 hello 預先定義的 Power BI 報表使用哪些詞彙 toolearn hello 大部分，以及哪些是傳回零個文件。</span><span class="sxs-lookup"><span data-stu-id="135ea-171">[Enable search traffic analytics](search-traffic-analytics.md) and use hello predefined Power BI report toolearn which terms are used hello most, and which ones return zero documents.</span></span> <span data-ttu-id="135ea-172">這些深入資訊為利器，修訂 hello 字典 tooinclude 同義字生產解析 toodocuments 索引中的查詢。</span><span class="sxs-lookup"><span data-stu-id="135ea-172">Armed with these insights, revise hello dictionary tooinclude synonyms for unproductive queries that should be resolving toodocuments in your index.</span></span>
