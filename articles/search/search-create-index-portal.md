---
title: "aaa\"建立索引 （入口網站的 Azure 搜尋） |Microsoft 文件 」"
description: "建立使用 hello Azure 入口網站的索引。"
services: search
manager: jhubbard
author: heidisteen
documentationcenter: 
ms.assetid: 
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/20/2017
ms.author: heidist
ms.openlocfilehash: 4c5d663499bf73a8883690aa9482b6ba59d1ddf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-azure-portal"></a>建立 Azure 搜尋索引使用 hello Azure 入口網站
> [!div class="op_single_selector"]
> * [概觀](search-what-is-an-index.md)
> * [入口網站](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

在 Azure 入口網站 tooprototype 使用 hello 內建的索引設計工具，或建立[搜尋索引](search-what-is-an-index.md)toorun 上您的 Azure 搜尋服務。 

## <a name="prerequisites"></a>必要條件

本文採用 [Azure 訂用帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)和 [Azure 搜尋服務](search-create-service-portal.md)。  

## <a name="find-your-search-service"></a>尋找您的搜尋服務
1. 登入 Azure 入口網站頁面 toohello 並檢閱 hello[搜尋服務的訂用帳戶](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)
2. 選取您的 Azure 搜尋服務。

## <a name="name-hello-index"></a>名稱 hello 索引

1. 按一下 hello**新增索引**hello 頁面頂端的 hello hello 命令列中的按鈕。
2. 為 Azure 搜尋服務索引命名。 
   * 以字母開頭。
   * 僅使用小寫字母、數字或連字號 ("-")。
   * 限制 hello 名稱 too60 字元。

  hello 索引名稱會變成用於連線 toohello 索引和 HTTP 要求傳送 hello Azure 搜尋 REST API 中的 hello 端點 URL 的一部分。

## <a name="define-hello-fields-of-your-index"></a>定義索引的 hello 欄位

包含索引組合*欄位集合*，定義索引中的 hello 可搜尋的資料。 更具體來說，它會指定 hello 分別上傳的文件結構。 hello 欄位集合包含必要與選用欄位，名為和型別，與索引屬性 toodetermine hello 欄位使用方式。

1. 在 hello **Add Index**刀鋒視窗中，按一下**欄位 >** tooslide 開啟 hello 欄位定義刀鋒視窗。 

2. 接受 hello 產生*金鑰*Edm.String 型別的欄位。 根據預設，名為 hello 欄位*識別碼*但您可以重新命名它，只要 hello 字串滿足[命名規則](https://docs.microsoft.com/rest/api/searchservice/Naming-rules)。 對於每個 Azure 搜尋服務索引而言，索引鍵欄位是必要的且必須為字串。

3. 加入的欄位 toofully 指定您要上傳的 hello 文件。 如果文件包含*識別碼*，*飯店名稱*，*位址*，*縣 （市)*，和*區域*，建立hello 索引中的每一個欄位對應。 檢閱 hello[設計 hello 一節中的指引](#design)中設定屬性的說明。

4. (選擇性) 新增任何要在篩選運算式內部使用的欄位。 Hello 欄位上的屬性可以設定 tooexclude 欄位從搜尋作業。

5. 完成後，請按一下**確定**toosave 建立 hello 的索引。

## <a name="tips-for-adding-fields"></a>新增欄位的秘訣

Hello 入口網站中建立索引是需要大量的鍵盤。 請遵循此工作流程以將步驟數降至最低：

1. 首先，輸入名稱和設定資料類型建置 hello 欄位清單。

2. 接下來，使用 hello 核取方塊上方的每個屬性 toobulk hello 啟用 hello 設定針對所有欄位，然後再選擇性地清除方塊 hello 不需要的幾個欄位。 例如，字串欄位通常是可搜尋的。 因此，您可以按一下**Retrievable**和**Searchable** hello tooboth 傳回 hello 值欄位中搜尋結果，以及允許 hello 欄位上的全文檢索搜尋。 

<a name="design"></a>
## <a name="design-guidance-for-setting-attributes"></a>設定屬性的設計指導方針

雖然您可以隨時加入新欄位，現有的欄位定義會鎖定 hello 索引 hello 存留期間。 基於這個理由，開發人員通常會建立簡單的索引、 測試概念，或使用設定的 hello 入口網站頁面 toolook 使用 hello 入口網站。 頻繁的反覆項目，透過索引設計是如果您遵循程式碼為基礎的方法，好讓您可以輕鬆地重建 hello 索引更有效率。

Hello 索引會在儲存之前，會與欄位相關聯分析器和建議工具。 為確定 tooclick 透過每個索引標籤式的頁面 tooadd 語言分析器 」 或 「 建議工具 tooyour 索引定義。

字串欄位通常會標示為 [可搜尋] 和 [可擷取]。

使用欄位 toonarrow 搜尋結果包括**Sortable**， **Filterable**，和**Facetable**。

欄位屬性會決定欄位的使用方式，例如，是否將它用於全文檢索搜尋、多面向導覽、排序作業等。 hello 下表說明每個屬性。

|屬性|說明|  
|---------------|-----------------|  
|**searchable**|全文檢索搜尋，主旨 toolexical 分析，例如編製索引期間的斷詞。 如果您設定可搜尋欄位 tooa 值類似"sunny day"，在內部它將會分割成 hello 個別語彙基元"sunny"和"day"。 如需詳細資訊，請參閱[全文檢索搜尋如何運作](search-lucene-query-architecture.md)。|  
|**filterable**|在 **$filter** 查詢中加以參考。 類型 `Edm.String` 或 `Collection(Edm.String)` 的可篩選欄位不會執行斷字功能，因此，只會針對完全相符的項目進行比較。 例如，如果您將 f 這類的欄位太"sunny day"，`$filter=f eq 'sunny'`會尋找相符的項目，但`$filter=f eq 'sunny day'`會。 |  
|**sortable**|Hello 系統預設分數，排序結果，但您可以設定在 hello 文件中的欄位為基礎的排序。 類型 `Collection(Edm.String)` 的欄位不能是 **sortable**。 |  
|**facetable**|通常用來呈現搜尋結果，其中包含依類別的叫用次數 (例如，特定城市中的旅館)。 此選項無法與類型 `Edm.GeographyPoint`的欄位搭配使用。 類型為 `Edm.String` 的欄位 (其為 **filterable**、**sortable** 或 **facetable**) 長度最多可達 32 KB。 如需詳細資訊，請參閱[建立索引 (REST API)](https://docs.microsoft.com/rest/api/searchservice/create-index)。|  
|**key**|Hello 索引內的文件的唯一識別碼。 只有一個欄位必須被選為 hello 索引鍵欄位，它必須是型別`Edm.String`。|  
|**retrievable**|決定是否可以在搜尋結果中傳回 hello 欄位。 當您想 toouse 欄位時，這是很有用 (例如*獲利率*) 做為篩選、 排序或計分機制，但是不要不想 hello 欄位 toobe 可見 toohello 終端使用者。 針對 `true` for `key` 。|  

## <a name="create-hello-hotels-index-used-in-example-api-sections"></a>建立範例應用程式開發介面 」 一節中所用的 hello 旅館索引

Azure 搜尋服務 API 文件包含具有簡單 hotels 索引功能的程式碼範例。 在 hello 以下螢幕擷取畫面，您可以看到 hello 索引定義，包括 hello 法文語言分析器指定在索引定義中，您可以為練習，hello 入口網站中重新建立它。

![](./media/search-create-index-portal/field-definitions.png)

![](./media/search-create-index-portal/set-analyzer.png)

## <a name="next-steps"></a>後續步驟

建立 Azure 搜尋索引之後, 您可以移動 toohello 下一個步驟：[可搜尋的資料上傳到 hello 索引](search-what-is-data-import.md)。

或者，您可能也需要深入探討索引。 此外 toohello 欄位集合中，索引也會指定分析器，建議工具、 計分設定檔和 CORS 設定。 hello 入口網站提供索引標籤式的頁面來定義 hello 最常見的項目： 欄位、 分析器及建議工具。 toocreate 或修改其他項目，您可以使用 hello REST API 或.NET SDK。

## <a name="see-also"></a>另請參閱

 [全文檢索搜尋如何運作](search-lucene-query-architecture.md)  
 [搜尋服務 REST API](https://docs.microsoft.com/rest/api/searchservice/) [.NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/search?view=azure-dotnet)

