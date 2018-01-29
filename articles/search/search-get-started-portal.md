---
title: "使用入口網站進行編製索引、查詢和篩選的 Azure 搜尋服務教學課程 | Microsoft Docs"
description: "在 Azure 入口網站中，使用預先定義的範例資料在 Azure 搜尋服務中產生索引。 探索全文檢索搜尋、篩選器、面向、模糊搜尋、地理搜尋功能等等。"
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.date: 12/04/2017
ms.author: heidist
ms.openlocfilehash: 098faa777746ac23ce7e88aa01fc727f88d4259c
ms.sourcegitcommit: a48e503fce6d51c7915dd23b4de14a91dd0337d8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2017
---
# <a name="create-query-and-filter-an-azure-search-index-in-the-portal"></a>在入口網站中建立、查詢和篩選 Azure 搜尋服務索引

在 Azure 入口網站中，從預先定義的範例資料集著手，使用 [匯入資料] 精靈快速產生 Azure 搜尋服務索引。 使用**搜尋總管**探索全文檢索搜尋、篩選器、面向、模糊搜尋和地理搜尋功能。  

此無程式碼的簡介，讓您從預先定義的資料著手，以便立即撰寫有趣的查詢。 雖然入口網站工具無法取代程式碼，但您可能發現它適合用於下列工作︰

+ 產品量產時間最短的實際操作學習
+ 在 [匯入資料] 中撰寫程式碼前，先設定索引的原型
+ 在 [搜尋總管] 中測試查詢和剖析器語法
+ 檢視已發佈至您服務的現有索引並查詢其屬性

**估計時間︰**大約 15 分鐘，但如果還需要註冊帳戶或服務，則時間較長。 

另外，加強使用 [.NET 中程式設計 Azure 搜尋服務的程式碼型簡介](search-howto-dotnet-sdk.md)。

## <a name="prerequisites"></a>必要條件

本教學課程會採用 [Azure 訂用帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)和 [Azure 搜尋服務](search-create-service-portal.md)。 

如果您不想要立即佈建服務，您可以觀看本教學課程中 6 分鐘的步驟示範 (大約在此 [Azure 搜尋服務概觀影片](https://channel9.msdn.com/Events/Connect/2016/138)中開始的三分鐘處)。

## <a name="find-your-service"></a>尋找您的服務
1. 登入 [Azure 入口網站](https://portal.azure.com)。
2. 開啟 Azure 搜尋服務的服務儀表板。 如果您並未將服務圖格釘選至儀表板，可以用以下方式找到您的服務︰ 
   
   * 在 Jumpbar 中，按一下左側導覽窗格底部的 [更多服務]。
   * 在搜尋方塊中，輸入 search 以取得訂用帳戶的搜尋服務清單。 您的服務應該會出現在清單中。 

## <a name="check-for-space"></a>檢查空間
許多客戶開始使用此免費服務。 此版本的限制為三個索引、三個資料來源，以及三個索引子。 開始之前，請先確定您有空間可容納額外的項目。 本教學課程會建立各一個物件。 

> [!TIP] 
> 服務儀表板上的圖格會顯示您已經有多少個索引、索引子和資料來源。 [索引子] 圖格可顯示成功與失敗指標。 按一下此圖格以檢視索引子計數。 
>
> ![索引子和資料來源的圖格][1]
>

## <a name="create-index"></a> 建立索引和載入資料
搜尋查詢會逐一查看索引  ，其中包含用來最佳化特定搜尋行為的可搜尋資料、中繼資料及建構。

為了讓這項工作以入口網站為基礎，我們使用可以透過 [匯入資料] 精靈使用索引子搜耙的內建範例資料集。 

#### <a name="step-1-start-the-import-data-wizard"></a>步驟 1︰啟動匯入資料精靈
1. 在 Azure 搜尋服務儀表板上，按一下命令列中的 [匯入資料]  來啟動可建立及填入索引的精靈。
   
    ![匯入資料命令][2]

2. 在精靈中，按一下 [資料來源] > [範例] >  [realestate-us-sample]。 此資料來源已預先設定名稱、類型和連線資訊。 一旦建立，就會變成可在其他匯入作業中重複使用的「現有資料來源」。

    ![選取範例資料集][9]

3. 按一下 [確定] 加以使用。

#### <a name="step-2-define-the-index"></a>步驟 2：定義索引
建立索引通常是以手動和程式碼為基礎，但是精靈可以為其可搜耙的任何資料來源產生索引。 索引至少需要有名稱和欄位的集合，而其中一個欄位會標示為文件索引鍵，以便唯一識別每份文件。

欄位具有資料類型和屬性。 上方的核取方塊為「索引屬性」，可控制欄位的使用方式。 

*  表示它會出現在搜尋結果清單中。 例如當欄位僅使用於篩選運算式時，您可以清除此核取方塊，將個別欄位標記為關閉搜尋結果的限制。 
* [可篩選]、[可排序] 和 [可面向化] 判斷欄位是否可以用於篩選、排序或多面向導覽結構。 
*  表示欄位包含在全文檢索搜尋中。 字串可以搜尋。 數字欄位和布林值欄位通常會標示為不可搜尋。 

根據預設，精靈會掃描資料來源中的唯一識別碼做為索引鍵欄位的基礎。 字串具有可擷取和可搜尋的特性。 整數具有可擷取、可篩選、可排序和可 Fact 處理的特性。

  ![產生的 realestate 索引][3]

按一下 [確定] 以建立索引。

#### <a name="step-3-define-the-indexer"></a>步驟 3：定義索引子
同樣在 [匯入資料] 精靈中，按一下 [索引子] > [名稱]，並且鍵入索引子的名稱。 

此物件定義可執行的程序。 您就可以將其放入週期性排程，但現在請先按一下 [確定]，立即使用預設選項執行索引子一次。  

  ![realestate 索引子][8]

## <a name="check-progress"></a>檢查進度
若要監視資料匯入，請回到服務儀表板，向下捲動，然後按兩下 [索引子] 圖格以開啟索引子清單。 您應該會在清單中看到新建立的索引子，其狀態指出「進行中」或成功，以及已編製索引的文件數目。

   ![索引子進度訊息][4]

## <a name="query-index"></a> 查詢索引
您現在有準備好要查詢的搜尋索引。  是入口網站內建的查詢工具。 它會提供搜尋方塊，以便確認搜尋結果是否如您所預期。 

> [!TIP]
> 在 [Azure 搜尋服務概觀影片](https://channel9.msdn.com/Events/Connect/2016/138)中，下列步驟會在影片的 6 分 08 秒處示範。
>

1. 按一下命令列上的 [搜尋總管]  。

   ![搜尋總管命令][5]

2. 按一下命令列上的 [變更索引] 以切換到 realestate-us-sample。

   ![索引和 API 命令][6]

3. 按一下命令列上的 [設定 API 版本] 以查看可用的 REST API。 預覽 API 可讓您存取尚未公開發行的新功能。 對於下列查詢，除非另有指示，否則使用公開上市版本 (2016-09-01)。 

    > [!NOTE]
    > [Azure 搜尋服務 REST API](https://docs.microsoft.com/rest/api/searchservice/search-documents) 和 [.NET 程式庫](search-howto-dotnet-sdk.md#core-scenarios)完全相等，但**搜尋總管**只能用於處理 REST 呼叫。 它可接受[簡單查詢語法](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)和[完整 Lucene 查詢剖析器](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)的語法，以及[搜尋文件](https://docs.microsoft.com/rest/api/searchservice/search-documents)作業中可用的所有搜尋參數。
    > 

4. 在搜尋列中，輸入下列查詢字串，然後按一下 [搜尋]。

  ![搜尋查詢範例][7]

**`search=seattle`**

+ **search** 參數用來輸入可供全文檢索搜尋的關鍵字搜尋，在此例中，會傳回華盛頓州金郡的清單，並且在文件的任何可搜尋欄位中包含 Seattle。 

+ **搜尋總管**會以 JSON 傳回結果，這是詳細資訊，而如果文件的結構很密集則難以閱讀。 視您的文件而定，您可能需要撰寫程式碼來搜尋結果，以擷取重要的元素。 

+ 文件是由索引中標記為可擷取的所有欄位組成。 若要在入口網站中檢視索引屬性，請按一下 [索引] 圖格中的 realestate-us-sample。

**`search=seattle&$count=true&$top=100`**

+ **&** 符號用來附加搜尋參數 (可依任何順序指定)。 

+  **$count=true** 參數會傳回所有已傳回文件的總和計數。 您可以藉由監視 **$count=true** 所報告的變更來驗證篩選查詢。 

+ **$top=100** 會傳回所有文件中最高順位的 100 份文件。 根據預設，Azure 搜尋服務會傳回前 50 個最相符項目。 您可以透過 **$top** 來增加或減少數量。


## <a name="filter-query"></a> 篩選查詢

當您附加 **$filter** 參數時，篩選器會包含在搜尋要求中。 

**`search=seattle&$filter=beds gt 3`**

+ **$filter** 參數會傳回符合您提供之準則的結果。 在此情況下，房間大於 3 間。 

+ 篩選語法是 OData 建構。 如需詳細資訊，請參閱[篩選 OData 語法](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search)。

## <a name="facet-query"></a> 將查詢面向化

Facet 篩選器會包含在搜尋要求中。 您可以使用 facet 參數，傳回符合您所提供之 facet 值的文件彙總計數。 

**`search=*&facet=city&$top=2`**

+ **search=*** 是空的搜尋。 空的搜尋會搜尋所有一切。 提交空查詢的其中一個原因是為了篩選一組完整的文件或使其面向化。 例如，您希望多面向導覽結構包含索引中的所有城市。

+  **facet** 會傳回您可傳遞至 UI 控制項的導覽結構。 它會傳回一些類別和一個計數。 在此情況下，類別是以城市數目為基礎。 在 Azure 搜尋服務中沒有彙總功能，但您可以透過 `facet` 模擬彙總，其可提供各類別中的文件計數。

+ **$top=2** 會傳回兩份文件，這表示您可以使用 `top` 來減少或增加結果。

**`search=seattle&facet=beds`**

+ 此查詢是 beds 的面向，以 Seattle 的文字搜尋為基礎。 可以將 beds 字詞指定為一個面向，因為該欄位標示為可在索引中擷取、篩選及面向化 (1 到 5 的數值)，適合用於將清單分類 (包含 3 個房間、4 個房間的清單)。 

+ 只有可篩選的欄位可以面向化。 只有可擷取的欄位可以在結果中傳回。

## <a name="highlight-query"></a> 新增醒目提示

命中項目醒目提示是指關鍵字文字比對的格式設定，前提是在特定欄位中找到相符項目。 如果您的搜尋字詞深藏在描述中，您可以新增命中項目醒目提示功能，更輕鬆地發現所搜尋的字詞。 

**`search=granite countertops&highlight=description`**

+ 在此範例中，格式化片語 granite countertops 可在描述欄位中更容易找出。

**`search=mice&highlight=description`**

+ 全文檢索搜尋會尋找具有類似語意的文字形式。 在受老鼠侵擾家庭的這個案例中，搜尋結果包含 "mouse" 的醒目提示文字，以回應 "mice" 關鍵字搜尋。 因為語言分析的緣故，結果中可能會出現同一個字的不同形式。 

+ Azure 搜尋服務支援 Microsoft 和 Lucene 所提供的 56 個分析器。 Azure 搜尋服務預設使用標準 Lucene 分析器。 

## <a name="fuzzy-search"></a> 使用模糊搜尋

拼錯的字 (如 samamish 是指 Seattle 地區的 Samammish 高原) 無法在一般搜尋中傳回相符項目。 若要處理拼字錯誤，您可以使用下一個範例中所述的模糊搜尋。

**`search=samamish`**

+ 此範例將 Seattle 地區的鄰近地區拼錯。

**`search=samamish~&queryType=full`**

+ 當您在指定 **~** 符號並使用完整查詢剖析器時可啟用模糊搜尋，它會解譯並正確地剖析 **~** 語法。 

+ 當您選擇使用完整查詢剖析器時可使用模糊搜尋，其發生於當您設定 **queryType=full** 時。 如需完整查詢剖析器所啟用查詢案例的詳細資訊，請參閱 [Azure 搜尋服務中的 Lucene 查詢語法](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)。

+ 若未指定 **queryType**，則會使用預設的簡單查詢剖析器。 簡單查詢剖析器的速度較快，但如果您需要模糊搜尋、規則運算式、鄰近搜尋或其他進階的查詢類型，則需要完整的語法。 

## <a name="geo-search"></a> 嘗試地理空間搜尋

地理空間搜尋是透過含有座標之欄位上的 [edm.GeographyPoint 資料類型](https://docs.microsoft.com/rest/api/searchservice/supported-data-types)提供支援。 地理搜尋是在[篩選 OData 語法](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search)中指定的一種篩選器。 

**`search=*&$count=true&$filter=geo.distance(location,geography'POINT(-122.121513 47.673988)') le 5`**

+ 範例查詢會篩選所有結果中的位置資料，而結果是小於距離指定點 (以緯度和經度座標指定) 5 公里。 藉由新增 **$count**，您可以看到當您變更距離或座標時傳回多少筆結果。 

+ 如果搜尋應用程式有「尋找附近地點」功能或使用地圖導航功能，地理空間搜尋便很實用。 不過，並不是全文檢索搜尋。 如果使用者有需要依照名稱搜尋城市或國家/地區，則除了座標以外，請新增包含城市或國家/地區名稱的欄位。

## <a name="next-steps"></a>後續步驟

+ 修改您剛建立的任何物件。 在您執行精靈一次之後，您可以返回並檢視或修改個別的元件︰索引、索引子或資料來源。 在索引上不允許進行某些編輯 (例如變更欄位資料類型)，但大部分的屬性和設定都可修改。

  若要檢視個別元件，請按一下儀表板上的 [索引]、[索引子] 或 [資料來源] 圖格，以顯示現有物件的清單。 若要深入了解不需要重建的索引編輯動作，請參閱[更新索引 (Azure 搜尋服務 REST API)](https://docs.microsoft.com/rest/api/searchservice/update-index)。

+ 請對其他資料來源試用工具和步驟。 範例資料集 (`realestate-us-sample`) 來自 Azure 搜尋服務可以搜耙的 Azure SQL Database。 除了 Azure SQL Database，Azure 搜尋服務可以從 Azure 表格儲存體、Blob 儲存體、Azure VM 上的 SQL Server 及 Azure Cosmos DB 中的一般資料結構搜耙及推斷索引。 精靈不支援上述所有資料來源。 在程式碼中，您可以使用「索引子」輕鬆地填入索引。

+ 透過推送模型可支援所有其他的非索引子資料來源，您的程式碼可在其中將 JSON 中新的和已變更的資料列集推送至您的索引。 如需詳細資訊，請參閱[在 Azure 搜尋服務中新增、更新或刪除文件](https://docs.microsoft.com/rest/api/searchservice/addupdate-or-delete-documents)。

若要深入了解本文提到的其他功能，請造訪下列連結︰

* [索引子概觀](search-indexer-overview.md)
* [建立索引 (包含索引屬性的詳細說明)](https://docs.microsoft.com/rest/api/searchservice/create-index)
* [搜尋總管](search-explorer.md)
* [搜尋文件 (包含查詢語法範例)](https://docs.microsoft.com/rest/api/searchservice/search-documents)


<!--Image references-->
[1]: ./media/search-get-started-portal/tiles-indexers-datasources2.png
[2]: ./media/search-get-started-portal/import-data-cmd2.png
[3]: ./media/search-get-started-portal/realestateindex2.png
[4]: ./media/search-get-started-portal/indexers-inprogress2.png
[5]: ./media/search-get-started-portal/search-explorer-cmd2.png
[6]: ./media/search-get-started-portal/search-explorer-changeindex-se2.png
[7]: ./media/search-get-started-portal/search-explorer-query2.png
[8]: ./media/search-get-started-portal/realestate-indexer2.png
[9]: ./media/search-get-started-portal/import-datasource-sample2.png