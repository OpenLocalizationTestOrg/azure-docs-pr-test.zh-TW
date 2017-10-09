---
title: "aaaWhat 是 Azure 搜尋 |Microsoft 文件"
description: "Azure 搜尋服務是受完整管理的託管雲端搜尋服務。 深入了解此功能概觀。"
services: search
manager: jhubbard
author: ashmaka
documentationcenter: 
ms.assetid: 50bed849-b716-4cc9-bbbc-b5b34e2c6153
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/26/2017
ms.author: ashmaka
ms.openlocfilehash: b38a7e93a7f0e0d5f8a3779858032271b3883778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-search"></a>何謂 Azure 搜尋服務？
Azure 搜尋服務是搜尋即服務雲端解決方案，可為開發人員提供 API 和工具，以透過資料在 Web、行動和企業應用程式中增添豐富的搜尋體驗。

透過簡單公開功能[REST API](/rest/api/searchservice/)或[.NET SDK](search-howto-dotnet-sdk.md) ，遮罩 hello 搜尋技術的固有的複雜性。 在加法 tooAPIs hello Azure 入口網站會提供系統管理及原型支援。 Microsoft 會管理基礎結構和可用性。

<a name="feature-drilldown"></a>

## <a name="feature-summary"></a>功能摘要

| 類別 | 特性 |
|----------|----------|
|全文檢索搜尋和文字分析 | [**全文檢索搜尋**](search-lucene-query-architecture.md)是大部分以搜尋為基礎之應用程式的主要使用案例。 您可以使用 Azure 搜尋服務支援的語法制訂查詢： <br/><br/>[**簡單查詢語法**](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) (英文) 可提供邏輯運算子、片語搜尋運算子、後置運算子、優先順序運算子。<br/><br/>[**Lucene 查詢語法**](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) (英文) 除提供所有簡單查詢支援之運算子之外，還可提供模糊搜尋、鄰近搜尋、字詞提升及規則運算式。| 
| 資料整合 | Azure 搜尋服務索引接受以 JSON 資料結構格式提交的任何來源。 <br/><br/> （選擇性） 在 Azure 中支援的資料來源，您可以使用[**索引子**](search-indexer-overview.md) tooautomatically 搜耙[Azure SQL Database](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)， [Azure Cosmos DB](search-howto-index-documentdb.md)，或[Azure Blob 儲存體](search-howto-indexing-azure-blob-storage.md)toosync 搜尋索引的內容與您的主要資料存放區。 Azure Blob 索引子可執行文件破解以[檢索主要檔案格式](search-howto-indexing-azure-blob-storage.md)，包括 Microsoft Office、PDF 和 HTML 文件。 |
| 搜尋分析 | [**自訂語彙分析器**](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) (英文) 適用於使用語音比對和規則運算式的複雜搜尋查詢。 |
| 語言支援 | [**語言分析器**](https://docs.microsoft.com/rest/api/searchservice/language-support) Lucene，以及 Microsoft 的自然語言處理器提供不同的語言 56 toointelligently 控制代碼特定語言的 linguistics 包括動詞時態、 性別、 異常的複數形式解除複合、 斷詞 （如需語言不含空格），以及更多的名詞 （例如，' 滑鼠' 與 'mice'），斷。 |
| 地區搜尋 | Azure 搜尋服務以智慧方式處理、篩選和顯示地理位置。 它可以讓使用者 tooexplore 資料根據 hello 鄰近搜尋結果 tooa 實體位置。 [觀賞此視訊](https://channel9.msdn.com/Shows/Data-Exposed/Azure-Search-and-Geospatial-Data)或[檢閱此範例](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs)toolearn 更多。 |
| 使用者體驗功能 | 您可以在搜尋列中針對預先輸入的查詢啟用[**搜尋建議**](https://docs.microsoft.com/rest/api/searchservice/suggesters) (英文)。 使用者輸入部分搜尋關鍵字時，搜尋引擎便會列出索引中實際的文件作為可能搜尋對象。 <br/><br/>透過單一查詢參數便可啟用[**多面向導覽**](https://docs.microsoft.com/azure/search/search-faceted-navigation) (英文)。 Azure 搜尋會傳回您可以使用 hello 類別 清單中後面的程式碼做為自我引導篩選 （例如，toofilter 類別目錄項目依價格範圍或品牌） 的多面向導覽結構。 <br/><br/> [**篩選**](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search)可以是使用的 tooincorporate 多面向導覽至您的應用程式 UI、 加強查詢公式和篩選器會根據使用者或開發人員指定的準則。 建立使用 hello OData 語法的篩選。<br/><br/> [**叫用反白顯示**](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)適用於 visual 表單 atting tooa 比對搜尋結果中的關鍵字。 您可以選擇哪些欄位傳回醒目提示的文字片段。<br/><br/>[**排序**](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)提供透過 hello 索引結構描述的多個欄位，並在查詢階段的單一搜尋參數然後切換。<br/><br/> [**分頁**](search-pagination-page-layout.md)和節流設定您的搜尋結果會直接與 Azure 搜尋提供透過您的搜尋結果的要更為精確的 hello 控制項。  
| 相關性 | [**簡單評分**](/rest/api/searchservice/add-scoring-profiles-to-a-search-index)是 Azure 搜尋服務的主要優點。 計分設定檔是使用的 toomodel 相關性 hello 中值的函式文件本身。 例如，您可能需要較新的產品或產品 tooappear hello 搜尋結果中較高的折扣。 您也可以根據您所追蹤並個別儲存的客戶搜尋喜好設定，使用標記進行個人化計分來建置計分設定檔。 |
| 監視和報告 | [**搜尋服務流量分析**](search-traffic-analytics.md)會收集和分析 toounlock 了解使用者正在輸入 hello 搜尋方塊中。 <br/><br/>自動會擷取每秒查詢次數、延遲和節流的計量，並在入口網站頁面中報告，不需要其他設定。 您也可以輕鬆地監視索引和文件計數，以便視需要調整容量。 如需詳細資訊，請參閱[服務管理](search-manage.md) |
| 用於原型設計和檢查的工具 | 在 hello 入口網站中，您可以使用 hello [**匯入資料精靈**](search-import-data-portal.md) tooconfigure 索引子，索引的索引，向上的設計工具 toostand 和[**搜尋總管**](search-explorer.md) tootest 查詢並精簡計分設定檔。 您也可以開啟任何索引 tooview 其結構描述。 |
| 基礎結構 | hello**高可用性的平台**確保相當穩定的搜尋服務的體驗。 經過適當的調整， [Azure 搜尋服務可提供 99.9% SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/)。<br/><br/> Azure 搜尋服務是**受到完整管理和可調整的**端對端解決方案，完全不需要基礎結構管理。 您的服務可以藉由在兩個維度 toohandle 縮放，更多文件儲存空間、 較高查詢負載，或兩者都是量身訂做的 tooyour 需求。

## <a name="how-it-works"></a>運作方式
### <a name="step-1-provision-service"></a>步驟 1：佈建服務
您可以加速在 Azure 搜尋服務中 hello [Azure 入口網站](https://portal.azure.com/)或透過 hello [Azure 資源管理 API](/rest/api/searchmanagement/)。 您可以選擇其中一個 hello 可用的服務與其他 「 訂閱者 」 共用或[付費層](https://azure.microsoft.com/pricing/details/search/)，dedicates 只能由您的服務所使用的資源。 若選擇付費層，您可以從兩方面調整服務︰ 

- 加入複本 toogrow 載入您容量 toohandle 繁重的查詢。   
- 新增更多文件的資料分割 toogrow 存放裝置。 

將文件儲存體和查詢輸送量分開處理，可讓您根據生產需求而校正資源分配。

### <a name="step-2-create-index"></a>步驟 2：建立索引
您必須先定義 Azure 搜尋服務索引，才能上傳可搜尋的內容。 索引就像是資料庫資料表，其中保存您的資料並可接受搜尋查詢。 您可以定義 hello 索引結構描述 toomap tooreflect hello 結構想 toosearch，類似 toofields 資料庫中的 hello 文件。

結構描述可由 hello Azure 入口網站，或以程式設計方式使用 hello [.NET SDK](search-howto-dotnet-sdk.md)或[REST API](/rest/api/searchservice/)。

### <a name="step-3-index-data"></a>步驟 3︰索引資料
定義索引之後，您便準備好 tooupload 內容。 您可以使用推送或提取模型。

hello 提取模型會從外部資料來源擷取資料。 這可透過*索引子*而達成，索引子可簡化和自動化資料擷取的各層面，例如連線至、讀取和序列化資料。 [索引子](/rest/api/searchservice/Indexer-operations)適用於 Azure Cosmos DB、Azure SQL Database、Azure Blob 儲存體和 Azure VM 中裝載的 SQL Server。 您可以重新整理隨需或排定的資料以設定索引子。

hello 發送模型會透過 SDK 或 REST Api，用來傳送更新的文件 tooan 索引 hello 提供。 您可以將資料推送從幾乎任何使用 hello JSON 格式的資料集。 請參閱[新增、 更新或刪除文件](/rest/api/searchservice/addupdate-or-delete-documents)或[toouse hello.NET SDK 的方式)](search-howto-dotnet-sdk.md)上載入資料的指引。

### <a name="step-4-search"></a>步驟 4︰搜尋
擴展索引之後, 您就能[發出搜尋查詢](/rest/api/searchservice/Search-Documents)tooyour 服務端點使用簡單的 HTTP 要求的 REST API 或 hello.NET SDK。

## <a name="how-it-compares"></a>比較的結果

客戶經常問到 [Azure 搜尋服務中的全文檢索搜尋](search-lucene-query-architecture.md)和其資料庫產品中的[全文檢索搜尋](https://en.wikipedia.org/wiki/Full_text_search)有何差別。 我們回應會是個更豐富且更具彈性，以支援 Lucene 查詢、 從 Lucene 和 Microsoft、 語音或其他特殊輸入的自訂分析器的語言分析器和 hello 能力 toomerge 資料從 Azure 搜尋語言功能hello 搜尋索引中的多個來源。 

另一個的轉折點是搜尋解決方案位址 hello 整個搜尋經驗。 例如，您想要有自訂的結果計分、多面向導覽以自行篩選、命中項目醒目提示和自動提示查詢建議。 

是否有工具可監視和了解查詢活動，也可以作為決定搜尋解決方案時的考慮因素。 例如，Azure 搜尋服務支援[搜尋流量分析](search-traffic-analytics.md)，可分析點選率、前幾名的搜尋、未點選的搜尋等計量。 在其中搜尋是附加元件的產品，您不太可能 toofind 這些功能。

資源使用率是另一項考量。 自然語言搜尋通常會耗用大量運算資源。 某些客戶卸載搜尋作業 tooAzure 搜尋做為在交易處理的方式 toopreserve 機器資源。 具體化的搜尋，您可以輕鬆地調整標尺 toomatch 查詢磁碟區。

一旦您決定 toogo 使用專用的搜尋，您的下一個決策就是雲端服務或在內部部署伺服器之間。 雲端服務是 hello 正確的選擇，如果您想[周全方案中的使用產生最低負擔和維護，以及可調整延展](#cloud-service-advantage)。

Hello 雲端開發架構，在數個提供者會提供可比較的基準功能，全文檢索搜尋、 地理搜尋與 hello 能力 toohandle 特定層級的搜尋輸入中的模稜兩可。 通常，它具有[特定的功能](#feature-drilldown)，或 hello 輕鬆與整體的應用程式開發介面、 工具和管理會決定 hello 適合的簡易性。

在雲端提供者中，針對主要依賴搜尋來擷取資訊和導覽內容的應用程式來說，Azure 搜尋服務在 Azure 上的內容存放區和資料庫處理全文檢索搜尋工作負載時，功能最強大。 主要優點包括︰

+ 在 hello 索引層級的 azure 資料整合 （尋檢程式）
+ 集中管理的 Azure 入口網站
+ Azure 調整性、可靠性和世界級的可用性
+ 語言和自訂分析，還有分析器提供可靠的全文檢索搜尋，支援 56 種語言
+ [核心功能的常見 toosearch 為主的應用程式](#feature-drilldown)： 計分、 faceting、 建議、 同義字、 地理搜尋等等。

> [!Note]
> toobe 清楚、 非 Azure 的資料來源完全支援，但依賴更大量的程式碼的推播方法，而不是索引子。 使用我們的 Api，您可以使用管線傳送任何 JSON 文件集合 tooan Azure 搜尋索引。

在我們的客戶之間這些無法 tooleverage hello 最大範圍的 Azure 搜尋中的功能包括線上類別目錄、 業務的程式和文件探索應用程式。

## <a name="rest-api--net-sdk"></a>REST API | .Net SDK

雖然在 hello 入口網站，就可以執行許多工作，Azure 搜尋適用於開發人員想要 toointegrate 搜尋功能加入現有的應用程式。 使用下列程式設計介面的 hello。

|平台 |說明 |
|-----|------------|
|[REST](/rest/api/searchservice/) | 任何程式設計平台和語言 (包括 Xamarin、Java 和 JavaScript) 支援的 HTTP 指令|
|[.NET SDK](search-howto-dotnet-sdk.md) | Hello REST API 的.NET 包裝函式提供了有效率地在 C# 中撰寫程式碼和其他 managed 程式碼語言，目標 hello.NET Framework |

## <a name="free-trial"></a>免費試用
Azure 的訂閱者可以[佈建 hello 免費層中的服務](search-create-service-portal.md)。

如果您不是訂閱者，可以[免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。 您會獲得信用額度來試用 Azure 付費服務。 它們用完之後，您可以讓 hello 的帳戶，並使用[免費的 Azure 服務](https://azure.microsoft.com/free/)。 除非您明確地變更您的設定，並詢問 toobe 收費，永遠不會收取您的信用卡。

或者，您也可以[啟用 MSDN 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)：您的 MSDN 訂用帳戶每月會提供您額度，您可以用在 Azure 付費服務。 

## <a name="how-tooget-started"></a>如何啟動 tooget

1. 建立服務在 hello[免費層](search-create-service-portal.md)。

2. 逐步執行一個或多個下列教學課程的 hello。 

  + [如何 toouse hello.NET SDK](search-howto-dotnet-sdk.md)示範 managed 程式碼中的 hello 主要步驟。  
  + [開始使用 REST API hello](https://github.com/Azure-Samples/search-rest-api-getting-started)顯示 hello 相同步驟使用 hello REST API。  
  + [在 hello 入口網站中建立您的第一個索引](search-get-started-portal.md)示範 hello 入口網站的內建的索引和原型功能。   

搜尋引擎會 hello 常見驅動程式的行動裝置應用程式，在 hello web 和公司資料存放區中的資訊擷取。 Azure Search 提供您工具建立搜尋體驗類似 toothose 大型商業網站上。

在程式管理員 Liam Cavanagh 主講的這段 9 分鐘影片中，您可以了解應用程式如何經由整合搜尋引擎而受益。 這段簡短的示範涵蓋了 Azure 搜尋服務中的主要功能，以及一般工作流程的樣貌。 

>[!VIDEO https://channel9.msdn.com/Events/Connect/2016/138/player]
 
+ 0-3 分鐘涵蓋主要功能和使用案例。
+ 3-4 分鐘涵蓋服務佈建。 
+ 4-6 分鐘內涵蓋的資料匯入精靈用 toocreate 使用 hello 內建不動產資料集的索引。
+ 6-9 分鐘涵蓋「搜尋總管」和各種查詢。


