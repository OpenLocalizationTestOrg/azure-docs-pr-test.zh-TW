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
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a>在 Azure 搜尋服務中建立多種語言的文件索引
> [!div class="op_single_selector"]
>
> * [入口網站](search-language-support.md)
> * [REST](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

Unleashing hello 的語言分析器功能是，只要在 hello 索引定義中可搜尋的欄位上設定一個屬性。 現在您可以執行此步驟在 hello 入口網站。

以下是 hello 的螢幕擷取畫面 Azure 入口網站的刀鋒視窗的 Azure 搜尋可讓使用者 toodefine 索引結構描述。 從這個刀鋒視窗中，使用者可以建立您所有的 hello 欄位和 hello 分析器屬性設定為每個。

> [!IMPORTANT]
> 您只能設定語言分析器期間欄位定義中或加入新欄位 tooan 現有索引時，建立新的索引，從 hello 接地。 請確定您完整指定所有的屬性，包括建立 hello 欄位時的 hello 分析器。 您不會是能 tooedit hello 屬性，或者變更 hello 分析器類型，一旦儲存變更。
>
>

## <a name="define-a-new-field-definition"></a>定義新的欄位定義
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)和您的搜尋服務開啟 hello 服務刀鋒視窗。
2. 按一下**新增索引**在 hello 命令列頂端的 hello 服務儀表板 toostart hello 新的索引，或開啟現有的索引 tooset 上您要加入新欄位分析器 tooan 現有的索引。
3. hello 欄位刀鋒視窗隨即出現，讓您定義 hello hello 索引結構描述的選項包括 hello 分析器 索引標籤用於選擇語言分析器。
4. 在欄位中，從開始的欄位定義中提供的名稱、 選擇 hello 資料型別，以及設定屬性 toomark hello 欄位做為全文檢索可搜尋、 在搜尋結果中，可用於 facet 瀏覽結構，可擷取可排序、 等等。
5. 在繼續 toohello 下一個欄位之前, 開啟 hello**分析器** 索引標籤。

![][1]
*tooselect 分析器 中，按一下 hello hello 欄位刀鋒視窗上的分析師 索引標籤*

## <a name="choose-an-analyzer"></a>選擇分析器
1. 您會定義捲軸 toofind hello 欄位。
2. 如果您未標示為可搜尋的 hello 欄位，按一下 [hello] 核取方塊現在 toomark 為**Searchable**。
3. 按一下 hello 分析器區域 toodisplay hello 清單可用的分析器。
4. 選擇 hello 分析器想 toouse。

![][2]
*選取其中一個 hello 支援每個欄位的分析器*

根據預設，所有可搜尋的欄位使用 hello[標準 Lucene 分析器](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html)即語言無關。 tooview hello 完整的清單支援的分析器，請參閱[Azure 搜尋中支援的語言](https://msdn.microsoft.com/library/azure/dn879793.aspx)。

一旦 hello 語言分析器選取欄位，它會搭配每個索引和搜尋要求，該欄位。 針對多個欄位，使用不同的分析器發出查詢時，hello 查詢將會每個欄位的 hello 右分析器獨立處理。

許多 web 和行動應用程式提供使用不同語言的 hello 全球各地的使用者。 很可能 toodefine 案例索引以這種方式所建立的欄位，每個支援的語言。

![][3]
*每種支援語言都有一個描述欄位的索引定義*

搜尋要求若為已知 hello hello 代理程式發出查詢語言，可以是已設定領域的 tooa 特定欄位使用 hello **searchFields**查詢參數。 hello 下列查詢將只對發出波蘭文 hello 描述：

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

您可以查詢您的索引，從 hello 入口網站中，使用**搜尋總管**toopaste 如上所示的其中一個查詢類似 toohello 中。 使用在 hello 服務刀鋒視窗中的 hello 命令列中搜尋總管。 請參閱[查詢您的 Azure 搜尋索引 hello 入口網站中](search-explorer.md)如需詳細資訊。

有時候 hello hello 代理程式發出查詢的語言是未知，哪些案例 hello 中查詢可以發送給所有欄位同時。 如有需要，可以使用 [評分設定檔](https://msdn.microsoft.com/library/azure/dn798928.aspx)來定義特定語言之結果的喜好設定。 Hello 下列範例中，在英文版的 hello 描述中找到相符項目將計分較高的相對 toomatches 波蘭文和法文：

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

如果您是.NET 開發人員，請注意，您可以設定語言分析器使用 hello [Azure 搜尋.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search)。 hello 最新版本包含 hello Microsoft 語言分析器也支援。

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
