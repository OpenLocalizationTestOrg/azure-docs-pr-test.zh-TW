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
# <a name="synonyms-in-azure-search-preview"></a>Azure 搜尋服務的同義字 (預覽)

同義字在搜尋引擎中的建立的關聯以隱含方式展開 hello 範圍查詢時，不具有提供 hello 詞彙 tooactually hello 使用者的對等詞彙。 例如，給定的 hello 詞彙"dog"和"canine 」 和 「 小狗"包含"dog"、"canine 」 或 「 小狗"的任何文件的同義字關聯會切換 hello hello 查詢範圍內。

在 Azure 搜尋服務中，同義字擴充在查詢同時就已完成。 您可以加入同義字地圖 tooa 服務不中斷 tooexisting 作業。 您可以加入**synonymMaps**屬性 tooa 欄位定義，而不需要 toorebuild hello 索引。 如需詳細資訊，請參閱[更新索引](https://docs.microsoft.com/rest/api/searchservice/update-index)。

## <a name="feature-availability"></a>功能可用性

hello 同義字功能是目前在預覽，並僅支援在 hello 最新預覽的 api 版本 (api 版本 = 2016年-09-01-預覽)。 目前 Azure 入口網站並不支援此功能。 因為 hello 要求上指定 hello API 版本，所以可能 toocombine 上市 (GA) 與預覽版 Api hello 中的相同的應用程式。 然而，預覽 API 不受 SLA 約束，且功能可能會變更，因此不建議在生產應用程式中使用。

## <a name="how-toouse-synonyms-in-azure-search"></a>如何在 Azure 中的 toouse 同義字搜尋

在 Azure 搜尋中，同義字支援根據您定義及上傳 tooyour 服務的同義資料表對應。 這些地圖由獨立資源構成 (例如索引或資料資源)，且可以在您搜尋服務索引中的任何可搜尋欄位使用。

同義字地圖和索引會分開維護。 一旦您定義同義字對應，並將它上傳 tooyour 服務，您可以啟用欄位 hello 同義字功能藉由新增新的屬性稱為**synonymMaps** hello 欄位定義中。 建立、 更新和刪除同義字對應一律整個文件的作業，這表示您無法建立，更新，或以累加方式刪除 hello 同義資料表對應的組件。 即便只是更新一個項目也需要重新載入。

將同義字整合至您的搜尋應用程式需要兩個步驟：

1.  新增透過 hello Api 同義字對應 tooyour 搜尋服務。  

2.  設定可搜尋欄位 toouse hello 同義字對應 hello 索引定義中。

### <a name="synonymmaps-resource-apis"></a>SynonymMaps 資源 API

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a>使用 POST 或 PUT 在您的服務中新增或更新同義字地圖。

同義字對應上傳 toohello 服務透過 POST 或 PUT。 每個規則必須加以分隔 hello 新行字元 ('\n')。 您可以定義 too5、 每個可用的服務中的同義字對應 000 規則和 10,000 規則中其他所有 Sku。 每個規則可以有向上 too20 展開。

在此預覽中，同義字對應必須 hello Apache Solr 格式說明如下。 如果您有現有的同義字字典格式不同，而且想 toouse 它直接管理，請讓我們知道上[UserVoice](https://feedback.azure.com/forums/263029-azure-search)。

您可以建立新的同義資料表對應，使用 HTTP POST，如 hello 下列範例所示：

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

或者，您可以使用 PUT，並在 hello URI 上指定 hello 同義資料表對應名稱。 如果 hello 同義字對應不存在，則會建立。

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a>Apache Solr 同義字格式

hello Solr 格式支援相等和明確的同義資料表對應。 對應規則遵守 toohello 開放原始碼同義字的 Apache Solr，這份文件中所述的篩選條件規格： [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter)。 以下是對等同義字的樣本規則。
```
              USA, United States, United States of America
```

與上述規則 hello，搜尋查詢 「 美國 」 將會太展開 「 美國 」 或者 「 美國 」 或者 「 美國 」。

明確的對應由箭號「=>」表示。 指定時，符合 hello 左邊的搜尋查詢詞彙序列"= >"會取代右邊 hello hello 替代項目。 指定 hello 規則，搜尋查詢"Washington"，"Wash." 或"WA"將所有會重新寫入太"WA"。 明確對應只套用在指定的 hello 方向和不太改寫 hello 查詢"WA""Washington"，在此情況下。
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a>您服務中的同義字地圖清單。

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a>在您的服務中取得同義字地圖。

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a>刪除您服務中的同義字地圖。

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-toouse-hello-synonym-map-in-hello-index-definition"></a>設定可搜尋欄位 toouse hello 同義字對應 hello 索引定義中。

新的欄位屬性**synonymMaps**可以是使用的 toospecify 同義字對應 toouse 可搜尋的欄位。 同義字對應服務層級的資源，而且可以依索引 hello 服務底下的任何欄位中參考。

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

**synonymMaps**可以指定 hello 型別 'Edm.String' 或 'Collection （edm.string）' 可搜尋的欄位。

> [!NOTE]
> 在此預覽中，每一個欄位僅能有一個同義字地圖。 如果您想 toouse 多個同義字對應，請讓我們知道上[UserVoice](https://feedback.azure.com/forums/263029-azure-search)。

## <a name="impact-of-synonyms-on-other-search-features"></a>同義字對其他搜尋功能的影響

hello 同義字功能重寫 hello 原始查詢以 hello OR 運算子的同義字。 基於這個理由，叫用的反白顯示和計分設定檔將 hello 原始詞彙及同義字視為對等項目。

同義字功能適用於 toosearch 查詢，但不適用於 toofilters 或 facet。 同樣地，建議根據只 hello 原始詞彙;同義字比對不會出現在 hello 回應。

同義字擴充不會套用 toowildcard 搜尋詞彙;不展開前置詞，模糊和 regex 條款。

## <a name="tips-for-building-a-synonym-map"></a>建置同義字地圖的秘訣

- 簡潔、 設計良好的同義字地圖比詳盡的可能比對結果清單來得有效率。 極大型或複雜的字典需要較長的 tooparse，而且影響 hello 查詢延遲，如果 hello 查詢擴充 toomany 同義字。 而不是猜測詞彙可能會使用，就可以透過 hello 實際條款[搜尋流量分析報表](search-traffic-analytics.md)。

- 初稿 」 和 「 驗證練習中，為啟用，並使用此報表 tooprecisely 判斷哪些詞彙將受益於同義字比對，然後再繼續 toouse 它做為驗證您的同義資料表對應會產生更好的結果。 Hello 預先定義的報表中的 hello 磚 「 最常見的搜尋查詢 」 和 「 零結果的搜尋查詢 可讓您 hello 所需的資訊。

- 您可以為您的搜尋應用程式建立多個同義字地圖 (例如，如果您的應用程式支援多語言的客戶群，您可以建立不同語言的同義字地圖)。 目前，一個欄位只能使用一個同義字地圖。 您可以隨時更新欄位的 synonymMaps 屬性。

## <a name="next-steps"></a>後續步驟

- 如果您在開發環境中 （非生產環境） 中有現有的索引，試驗小字典 toosee hello 新增同義字如何變更 hello 搜尋經驗，包括計分設定檔、 點擊反白顯示，以及建議的影響。

- [啟用搜尋服務流量分析](search-traffic-analytics.md)和使用 hello 預先定義的 Power BI 報表使用哪些詞彙 toolearn hello 大部分，以及哪些是傳回零個文件。 這些深入資訊為利器，修訂 hello 字典 tooinclude 同義字生產解析 toodocuments 索引中的查詢。
