---
title: "aaaAzure 搜尋效能與最佳化考量 |Microsoft 文件"
description: "調整 Azure 搜尋服務效能並設定最佳規模"
services: search
documentationcenter: 
author: LiamCavanagh
manager: pablocas
editor: 
ms.assetid: 4d3cd864-29d2-4921-be0d-a3f1a819de46
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: 725149ba32773ab6b4c9d4b441424aba78db7c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-performance-and-optimization-considerations"></a>Azure 搜尋服務的效能與最佳化考量
絕佳搜尋經驗是索引鍵 toosuccess 許多行動應用程式和 web 應用程式。 不動產，從 tooused 汽車市場 tooonline 目錄、 快速搜尋和相關的結果將會影響 hello 客戶經驗。 本文件是預定的 toohelp 探索如何充分利用 Azure 搜尋中，特別是針對進階案例使用 tooget hello 複雜的延展性、 多重語言支援或自訂的順位需求的最佳作法。  此外，本文件也會概述本質，並涵蓋可在真實世界客戶應用程式中有效率地工作的處理方法。

## <a name="performance-and-scale-tuning-for-search-services"></a>適用於搜尋服務的效能和規模調整
我們為所有使用的 toosearch 引擎等時所提供的 Bing 和 Google 和 hello 高的效能。  因此，當客戶使用您已具備搜尋功能的 Web 或行動應用程式時，他們將期望類似的效能特性。  最佳化搜尋效能、 hello 最佳方法之一時，對延遲，也就是查詢所需 toocomplete 並傳回結果的 hello 時間 toofocus。  針對搜尋延遲進行最佳化時，請務必：

1. 挑選一般搜尋要求應該採取 toocomplete 目標延遲 （或最大時間量）。
2. 建立並測試您的搜尋服務與實際的資料集 toomeasure 實際工作負載這些延遲率。
3. 每秒查詢數 (QPS) 數目最少的開頭，並繼續 tooincrease hello 數目 hello 測試中執行，直到延遲低於 hello hello 查詢定義為目標延遲。  這是您計劃標尺的使用狀況應用程式茁壯重要基準 toohelp。
4. 如果可能，請重複使用 HTTP 連接。  如果您使用 hello Azure 搜尋.NET SDK，這表示您應該重複使用執行個體或[SearchIndexClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.searchindexclient)執行個體，且如果您使用 hello REST API，您應該重複使用單一的 HttpClient。

當建立這些測試工作負載，有個 Azure 搜尋 tookeep 記住一些特性：

1. 很可能 toopush 這麼多的搜尋查詢一次，您的 Azure 搜尋服務中所提供的 hello 資源將會過度負荷。  發生這種情況時，您將會看到 HTTP 503 回應碼。  基於這個理由，是與不同的範圍與延遲率的搜尋要求 toosee hello 差異的最佳 toostart 當您新增更多的搜尋要求。
2. 上傳的內容將會影響搜尋的 tooAzure hello 整體效能和延遲的 hello Azure 搜尋服務。  如果您預期 toosend 資料，使用者會執行搜尋時，很重要 tootake 到此工作負載測試中的帳戶。
3. 並非每個搜尋查詢會在執行 hello 相同的效能層級。  例如，比起具有大量 Facet 和篩選的查詢，文件查閱或搜尋建議的執行速度通常會更快。  它是您預期到 toosee 的各種查詢帳戶建立您的測試時的最佳 tootake hello。  
4. 搜尋要求的變化非常重要，因為如果您持續執行 hello 相同搜尋要求，快取的資料將會開始 toomake 效能尋找優於它可能會比較不同的查詢與設定。

> [!NOTE]
> [Visual Studio 負載測試](https://www.visualstudio.com/docs/test/performance-testing/run-performance-tests-app-before-release)是真的很好的方式 tooperform 您基準測試，因為它可讓您 tooexecute HTTP 要求與您需要對 Azure 搜尋執行查詢，並啟用平行處理的要求。
> 
> 

## <a name="scaling-azure-search-for-high-query-rates-and-throttled-requests"></a>調整 Azure 搜尋服務以提供高速查詢和節流要求
當您收到節流的要求太多或超過您從增加的查詢負載的目標延遲率時，您可以查看 toodecrease 延遲率兩種方式之一：

1. **增加複本：**複本就像是您的資料複本允許對 hello Azure 搜尋 tooload 平衡要求多個複本。  所有的負載平衡和複本之間的資料複寫由 Azure 搜尋管理及您可以變更 hello 隨時為您的服務配置的複本數目。  您可以配置在標準搜尋服務 too12 複本和基本搜尋服務中的 3 個複本。 複本可調整從 hello [Azure 入口網站](search-create-service-portal.md)或[PowerShell](search-manage-powershell.md)。
2. **增加搜尋服務層︰**Azure 搜尋服務來自[層數](https://azure.microsoft.com/pricing/details/search/)，而這其中的每一層都會提供不同等級的效能。  在某些情況下，您可能需要您位於該 hello 層無法提供夠低度延遲率，複本會超量時，即使這麼多的查詢。在此情況下，您可能想 tooconsider 運用 hello Azure 搜尋 S3 層非常適合具有大量的文件和極高的查詢工作負載的情況下，例如 hello 更高搜尋階層的其中一個。

## <a name="scaling-azure-search-for-slow-individual-queries"></a>針對速度較慢的個別查詢調整 Azure 搜尋服務
為什麼延遲速率可能很慢的另一個原因是來自單一查詢花費太長 toocomplete。  在此情況下，新增複本將無法改善延遲率。  在此情況下，有兩個可用選項：

1. **增加分割區** 分割區是一種機制，可分割資料以分散到額外的資源上。  基於這個理由，當您新增第二個分割區時，您的資料就會一分為二。  第三個分割區會將您的索引分成三等份，依此類推。這也有 hello 效果，在某些情況下，緩慢的查詢將會執行得更快到期的計算 toohello 平行化作業。  我們可以在一些範例中看見這個平行處理搭配具有低度選擇性查詢的查詢時運作得非常好。  這包含比對許多文件的查詢或 tooprovide faceting 需要時計算透過大量文件。  因為有大量計算所需的 hello 文件或 toocount hello 的數字的文件，加入額外的資料分割可以幫助 tooprovide 額外計算 tooscore hello 相關性。  
   
   可以在標準搜尋服務中的 12 個資料分割最多和 1 hello 基本搜尋服務中的資料分割。  資料分割可以調整從 hello [Azure 入口網站](search-create-service-portal.md)或[PowerShell](search-manage-powershell.md)。
2. **高基數欄位限制：**高基數欄位所組成的可進行 facet 處理或有大量的唯一值，而且如此一來，就會大量的資源 toocompute 結果的可篩選欄位。   例如，產品識別碼或描述欄位設定為可進行 facet 處理/篩選會使高基數的因為大部分的文件 toodocument hello 值都是唯一。 可能的話，高基數欄位的 hello 數目限制。
3. **增加搜尋層：** tooa 更高版本上移 Azure 搜尋層可以另一個方式 tooimprove 效能緩慢的查詢。  每一個較高的層也會提供更快速的 CPU 和更多記憶體，可以對查詢效能產生正面的影響。

## <a name="scaling-for-availability"></a>調整可用性
複本不僅有助於減少查詢延遲，也可以允許高可用性。  與單一的複本，您應該會定期停機 tooserver 重新開機後軟體更新或其他維護活動，將會出現。  如此一來，它是重要 tooconsider 如果應用程式所需的搜尋 （查詢） 的高可用性和寫入 （索引事件）。  Azure 搜尋會提供所有的 SLA 選項具有下列屬性的 hello hello 付費的搜尋供應項目：

* 針對唯讀工作負載 (查詢)，需有 2 個複本才能達到高可用性
* 針對讀取/寫入工作負載 (查詢和索引) 的高可用性為 3 或更多個複本

如需詳細資訊，在此，請瀏覽 hello [Azure 搜尋服務等級協定](https://azure.microsoft.com/support/legal/sla/search/v1_0/)。

由於複本位於您資料副本，具有多個複本，可讓 Azure 搜尋 toodo 機器重新開機，並維護一個複本，同時允許一次針對查詢 toocontinue toobe 針對執行 hello 其他複本。  基於這個原因，您也必須的 tooconsider 這個停機時間可能會如何影響 hello 現在有 toobe 針對 hello 資料較少複本執行的查詢。

## <a name="scaling-geo-distributed-workloads-and-provide-geo-redundancy"></a>調整異地分散的工作負載並提供異地備援
針對地理分散工作負載，您會發現遠離 hello 資料中心裝載您的 Azure 搜尋服務的使用者會有較高的延遲率。  基於這個理由，通常很重要的 toohave 位於更接近鄰近 toothese 使用者的區域中的多個搜尋服務。  Azure 搜尋目前未提供自動化的方法的地理複寫的 Azure 搜尋索引跨區域，但有一些技術可以使用，可以讓此程序簡單 tooimplement 並管理。 這些述 hello 接下來的章節。

hello 地理分散的一組搜尋服務的目標是 toohave 兩個或多個索引可在兩個或多個區域，將使用者路由傳送 toohello Azure 搜尋服務，可提供 hello 最低延遲，如本範例所示：

   ![依區域交叉分析服務][1]

### <a name="keeping-data-in-sync-across-multiple-azure-search-services"></a>跨多個 Azure 搜尋服務，讓資料維持同步
有兩個選項，將保持在分散式的搜尋服務同步組成使用 hello [Azure 搜尋索引子](search-indexer-overview.md)或 hello 推送 API (也稱為 tooas hello [Azure 搜尋 REST API](https://docs.microsoft.com/rest/api/searchservice/))。  

### <a name="azure-search-indexers"></a>Azure 搜尋服務索引子
如果您使用 hello Azure 搜尋索引子，您已匯入資料的變更集中的資料存放區，例如 Azure SQL DB 或 Azure Cosmos DB。 當您建立新的搜尋服務，您只需也建立了新的 Azure 搜尋索引子，該服務該點 toothis 相同的資料存放區。 這樣一來，每當新的變更進入 hello 資料存放區，則會以編製索引 hello 各種索引子。  

以下範例為該架構所呈現的樣子。

   ![具有分散式索引子和服務組合的單一資料來源][2]

### <a name="push-api"></a>推送 API
如果您使用 hello Azure 搜尋推送 API 太[更新您的 Azure 搜尋索引中的內容](https://docs.microsoft.com/rest/api/searchservice/update-index)，您可以將各種不同的搜尋服務同步推送變更 tooall 搜尋服務，需要更新時。  這項操作時很重要的 toomake 確定 toohandle 情況下更新 tooone 搜尋服務失敗而一或多個更新成功。

## <a name="leveraging-azure-traffic-manager"></a>運用 Azure 流量管理員
[Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md)可讓您 tooroute 要求 toomultiple 地理位置網站，然後由多個 Azure 搜尋服務。  Hello Traffic Manager 的其中一個優點是可以探查是可用的 Azure 搜尋 tooensure 和路由的停機時間的 hello 事件中的使用者 tooalternate 搜尋服務。  此外，如果您要路由傳送 search 要求是透過 Azure Web Sites，Azure Traffic Manager 可讓您 tooload 平衡案例 hello 網站已啟動但不是 Azure 搜尋。  以下是哪一個 hello 架構運用 Traffic Manager 的範例。

   ![利用中央流量管理員依區域交叉分析服務][3]

## <a name="monitoring-performance"></a>監視效能
Azure Search 提供 hello 能力 tooanalyze 和監視器 hello 的效能，您的服務透過[搜尋流量分析 (STA)](search-traffic-analytics.md)。 STA，透過您選擇性地可以在 Power BI 中記錄 hello 個別的搜尋作業，以及彙總度量資訊，然後可以處理的分析或以視覺化方式檢視 tooan Azure 儲存體帳戶。  使用 STA 計量，您可以檢閱效能統計資料，例如查詢或查詢回應時間的平均數目。  此外，hello 作業記錄可讓您 toodrill 為特定的搜尋作業的詳細資料。

STA 是從 Azure 搜尋檢視方塊的寶貴工具 toounderstand 延遲速率。  因為記錄 hello 查詢效能度量依據 hello 時間查詢需要耗費 toobe 完全處理 Azure 搜尋中 （從是送出要求的 toowhen hello 時間），您就可以 toouse 此 toodetermine 如果延遲問題會從 hello Azure 搜尋服務側邊或外部的 hello 服務，例如從網路延遲。  

## <a name="next-steps"></a>後續步驟
請參閱深入了解每個定價層和服務限制的 hello toolearn[服務在 Azure 搜尋中的限制](search-limits-quotas-capacity.md)。

請瀏覽[容量規劃](search-capacity-planning.md)toolearn 更多關於資料分割和複本組合。

向下鑽研更多的效能與本文所討論的 tooimplement hello 最佳化的方式有些示範 toosee，監看下列影片 hello:

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON319/player]
> 
> 

<!--Image references-->
[1]: ./media/search-performance-optimization/geo-redundancy.png
[2]: ./media/search-performance-optimization/scale-indexers.png
[3]: ./media/search-performance-optimization/geo-search-traffic-mgr.png
