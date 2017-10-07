---
title: "aaaCommon 使用案例和案例 Azure Cosmos DB |Microsoft 文件"
description: "深入了解 hello 前五個使用案例的 Azure Cosmos DB： 使用者產生的內容、 事件記錄、 目錄資料、 使用者偏好設定資料和物聯網 (IoT)。"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: eca68a58-1a8c-4851-8cf8-6e4d2b889905
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: mimig
ms.openlocfilehash: 115a418e7b18d5033c4d7e64591bf302aea0190b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="common-azure-cosmos-db-use-cases"></a>常見的 Azure Cosmos DB 使用案例
本文提供數個常見的 Azure Cosmos DB 使用案例概觀。  這篇文章中的 hello 建議做為的起點，當您開發以 Cosmos DB 的應用程式。   

閱讀這篇文章之後, 您將會無法 tooanswer hello 下列問題： 

* 什麼是 Azure Cosmos db hello 常見使用案例？
* 零售應用程式使用 Azure Cosmos DB hello 優點有哪些？
* 使用 Azure Cosmos DB 當做資料存放區的物聯網 (IoT) 系統的 hello 優點有哪些？
* 針對 web 和行動應用程式使用 Azure Cosmos DB 的 hello 優點有哪些？

## <a name="introduction"></a>簡介
[Azure Cosmos DB](../cosmos-db/introduction.md) 是 Microsoft 的全域分散式資料庫服務。 hello 服務是設計的 tooallow 客戶 tooelastically （和個別） 比例輸送量與儲存體的地理區域的任何數字。 Azure Cosmos DB hello 第一個全域分散式的資料庫服務處於 hello 市場今日 toooffer 完整[的服務等級協定](https://azure.microsoft.com/support/legal/sla/cosmos-db/)內含輸送量、 延遲、 可用性和一致性。 

hello Azure Cosmos DB 專案啟動 2011年中為 「 專案佛羅倫斯"tooaddress 開發人員痛苦點 Microsoft 內部的大型網際網路規模應用程式時所面對的。 觀察到這些問題不是唯一的 tooMicrosoft 應用程式，我們決定 toomake Azure Cosmos DB 上市 tooexternal 開發人員在 hello 形式 2015年[Azure DocumentDB](https://azure.microsoft.com/blog/documentdb-moving-to-general-availability/)。 hello 服務是普遍內部在 Microsoft 內，而且其中一個快速成長外部 Azure 開發人員所使用之服務的 hello。 

Azure Cosmos DB 是一種全域分散式、多模型資料庫，廣泛用於各種應用程式和使用案例。 它是不錯的選擇任何[無伺服器](http://azure.com/serverless)低的毫秒數的順序回應的時間，並且需要 tooscale 快速和全域的應用程式。 它以原生方式和延伸方式支援多個資料模型 (索引鍵-值、文件、圖形及單欄式) 和許多 API (包括 [MongoDB](mongodb-introduction.md)、[DocumentDB SQL](documentdb-introduction.md)、[Gremlin](graph-introduction.md) 及 [Azure 資料表](table-introduction.md)) 來進行資料存取。 

hello 以下是一些 Azure Cosmos DB 的屬性，使其適合用於具有全域野心的高效能應用程式。

* Azure Cosmos DB 會原生分割您的資料來達到高可用性和延展性。 Azure Cosmos DB 提供可達 99.99% 可用性、輸送量、低延遲及一致性的保證。
* Azure Cosmos DB 具有以 SSD 支持的儲存體，可提供低延遲的毫秒級回應時間。
* Azure Cosmos DB 支援最終、一致前置碼、工作階段及限定過期等一致性層級，因此能提供充分的彈性和高性價比。 沒有資料庫服務可在層級一致性上提供像 Azure Cosmos DB 一樣多的彈性。 
* Azure Cosmos DB 具有彈性的資料友善計價模型，可針對儲存體和輸送量單獨計價。
* Azure Cosmos DB 的保留的輸送量模型可讓您 toothink 讀取/寫入，而不是 CPU/記憶體/IOPs hello 基礎硬體的數量。
* Azure Cosmos DB 的設計可讓您將 toomassive 要求中的磁碟區 hello trillions 是每天要求的順序。

這些屬性很有幫助在 web、 行動、 遊戲，以及需要低回應時間，而且需要大量的讀取和寫入 toohandle IoT 應用程式。

## <a name="iot-and-telematics"></a>IoT 和遠距通訊
IoT 使用案例在如何內嵌、處理和儲存資料方面通常共用一些模式。  首先，這些系統需要資料，從各種不同的地區設定的裝置感應器 tooingest 的暴增。 接著，這些系統處理，並分析資料流資料 tooderive 即時深入資訊。 hello 資料封存 toocold 批次分析的存放裝置。 Microsoft Azure 提供適用於 IoT 使用案例的豐富服務，包括 Azure Cosmos DB、「Azure 事件中樞」、「Azure 串流分析」、「Azure 通知中樞」、「Azure 機器學習服務」、Azure HDInsight 及 PowerBI。 

![Azure Cosmos DB IoT 參考架構](./media/use-cases/iot.png)

Azure 事件中樞可以擷取暴增的資料量，因為它提供高輸送量資料擷取和低延遲。 內嵌需要的資料處理 toobe 即時深入資訊可以 funneled 的 tooAzure 資料流分析進行即時分析。 您可以將資料載入 Azure Cosmos DB 以進行臨機操作查詢。 一旦 hello 資料載入至 Azure Cosmos DB，hello 資料是查詢的準備 toobe。 此外，新的資料變更 tooexisting 資料可以讀取的變更摘要。 變更摘要是持續的只會儲存的記錄變更循序 tooCosmos DB 集合附加。 做為參考資料做為即時分析的一部分，則可能使用所有資料或只變更 toodata Azure Cosmos DB 中的 hello。 此外，可以進一步調整與資料連接 Azure Cosmos DB 資料 tooHDInsight Pig、 Hive 或 Map/Reduce 作業所處理。  然後調整過的資料被載入後 tooAzure Cosmos DB reporting。   

如需使用 Azure Cosmos DB、 EventHubs 和 Storm 範例 IoT 解決方案，請參閱 hello [GitHub 上的 hdinsight-storm-範例儲存機制](https://github.com/hdinsight/hdinsight-storm-examples/)。

IoT Azure 供應項目上的詳細資訊，請參閱[建立 hello 網際網路您聯網](http://www.microsoft.com/server-cloud/internet-of-things.aspx)。 

## <a name="retail-and-marketing"></a>零售和行銷
Azure Cosmos DB 廣泛使用在 Microsoft 自己電子商務平台執行 hello Windows 市集和 XBox Live。 它是也用於 hello 零售產業中儲存目錄資料和事件處理管線的順序執行。

目錄資料使用方式案例涉及儲存和查詢一組實體屬性，例如人員、地點和產品。 目錄資料的一些範例包括使用者帳戶、產品目錄、IoT 裝置註冊及材料表系統。 此資料的屬性而異，而且可能會隨著時間 toofit 應用程式需求變更。

請細想汽車零件供應商產品目錄的範例。 每個組件可能具有自己的屬性，加法 toohello 通用屬性中的所有部分都共用。 此外，特定組件的屬性可以變更下列的年發行新模型時的 hello。 Azure Cosmos DB 支援彈性結構描述和階層式資料，因此很適合用來儲存產品目錄資料。

![Azure Cosmos DB 零售目錄參考架構](./media/use-cases/product-catalog.png)

Azure Cosmos DB 通常用於取得 toopower 事件驅動的架構使用的事件其[變更摘要](change-feed.md)功能。 hello 變更摘要會提供下游 microservices hello 能力 tooreliably 和讀取以累加方式插入，並進行 tooan Azure Cosmos DB 更新 （例如，訂單事件）。 這項功能可以運用的 tooprovide 當做訊息仲介的狀態變更事件及磁碟機之間許多 microservices 訂單處理工作流程的持續性事件存放區 (其中可以實作為[無伺服器的 Azure 函式](http://azure.com/serverless)).

![Azure Cosmos DB 訂購管線參考架構](./media/use-cases/event-sourcing.png)

此外，儲存在 Azure Cosmos DB 中的資料還可以與 HDInsight 整合，以透過 Apache Spark 作業進行巨量資料分析。 如需 hello Azure Cosmos DB 的 Spark 連接器的詳細資訊，請參閱[執行 Cosmos 資料庫與 HDInsight Spark 工作](spark-connector.md)。

## <a name="gaming"></a>玩遊戲
hello 資料庫層是遊戲應用程式的重要元件。 現今的遊戲在行動裝置版/主控台用戶端，執行圖形化處理，但依賴 hello 雲端 toodeliver 自訂和個人化的內容，如遊戲中的統計資料、 社交媒體整合和計分排行榜。 遊戲通常需要單一毫秒延遲的讀取與寫入 tooprovide 更吸引人的遊戲中體驗。 遊戲的資料庫需要 toobe 快速，而是在新的遊戲會啟動和功能更新期間無法 toohandle massive 激增要求率。

Azure Cosmos DB 由類似的遊戲[hello 查核無作用： 沒有人之地](https://azure.microsoft.com/blog/the-walking-dead-no-mans-land-game-soars-to-1-with-azure-documentdb/)由[下一步遊戲](http://www.nextgames.com/)，和[光暈 5： 守護](https://azure.microsoft.com/blog/how-halo-5-guardians-implemented-social-gameplay-using-azure-documentdb/)。 Azure 的 Cosmos DB 會提供下列 hello 有益於 toogame 開發人員：

* Azure 的 Cosmos DB 讓效能 toobe 縮放向上或向下彈性地。 這可讓遊戲 toohandle 更新設定檔和統計資料從數十 toomillions 藉由單一應用程式開發介面呼叫同時玩家正面對決。
* Azure DB Cosmos 支援毫秒讀取和寫入 toohelp 遊戲進行期間避免任何延遲。
* Azure Cosmos DB 的自動索引編製可針對多個不同的屬性進行即時篩選，例如依玩家的內部玩家識別碼、GameCenter、Facebook、Google ID 找出玩家，或根據玩家的公會成員資格進行查詢。 不用建置複雜的索引或分區化基礎結構就可做到這些事。
* 社交功能包括在遊戲中交談的訊息、 player guild 成員資格、 完成的挑戰，計分排行榜和社交圖形會更容易 tooimplement 具有彈性的結構描述。
* Azure Cosmos DB 為受管理的平台做為服務 (PaaS) 所需最少的安裝和管理工作 tooallow 快速的反覆項目，並減少時間 toomarket。

![Azure Cosmos DB 遊戲參考架構](./media/use-cases/gaming.png)

## <a name="web-and-mobile-applications"></a>Web 與行動應用程式
Azure Cosmos DB 常用於 Web 與行動應用程式，而且適合用於建立社交互動模型、與第三方服務整合及建置豐富的個人化體驗。 hello Cosmos DB Sdk 可以使用的建置豐富的 iOS 和 Android 的應用程式使用常用的 hello [Xamarin 架構](mobile-apps-with-xamarin.md)。  

### <a name="social-applications"></a>社交應用程式
用於 Azure Cosmos DB 的常見使用案例是 toostore 和查詢使用者產生的內容 (UGC) 的 web、 行動、 的社交媒體應用程式。 一些 UGC 範例包括對談、推文、部落格文章、評等和註解。 通常，社交媒體應用程式中的 hello UGC 是混合的自由格式文字、 屬性、 標記，以及不固定的結構所繫結的關聯性。 例如聊天室內容，註解和文章可以儲存 Cosmos DB 中而不需要轉換或複雜物件 toorelational 對應層。  可以加入或修改輕鬆 toomatch 需求為開發人員反覆 hello 應用程式程式碼，因此升級快速開發資料屬性。  

與協力廠商的社交網路整合的應用程式必須從這些網路回應 toochanging 結構描述。 根據預設，在 Cosmos DB 自動索引資料，時會準備 toobe 隨時查詢資料。 因此，這些應用程式有 hello 彈性 tooretrieve 投影，根據其各自的需求。

許多 hello 社交應用程式在通用標尺上執行，並可能顯現出無法預期的使用模式。 有彈性地調整 hello 資料存放區很重要，因為 hello 應用程式層縮放 toomatch 使用量需求。  您可以透過在 Cosmos DB 帳戶下新增其他資料分割區來相應放大。  此外，您也可以跨多個區域建立其他 Cosmos DB 帳戶。 如需了解 Cosmos DB 服務區域可用性，請參閱 [Azure 區域](https://azure.microsoft.com/regions/#services)。

![Azure Cosmos DB Web 應用程式參考架構](./media/use-cases/apps-with-global-reach.png)

### <a name="personalization"></a>個人化
現今，現代應用程式具備複雜的檢視和體驗。 這些是通常是動態的承辦宴席類 toouser 喜好設定或情緒的變化和品牌的需求。 因此，應用程式需要 toobe 無法 tooretrieve 個人化設定有效 toorender UI 項目和體驗快速。 

JSON，Cosmos DB 所支援的格式是有效的格式 toorepresent UI 版面配置資料，因為它不是只有輕量型的但也可以輕鬆地解譯的 JavaScript。 Cosmos DB 提供可微調的一致性層級，可允許快速讀取及低延遲寫入。 因此，UI 版面配置資料包括個人化的設定，因為 Cosmos DB 中的 JSON 文件是有效的方式 tooget 將這些資料儲存 hello 網路上。

![Azure Cosmos DB Web 應用程式參考架構](./media/use-cases/personalization.png)

## <a name="next-steps"></a>後續步驟
tooget 開始使用 Azure Cosmos DB，請遵循我們[快速入門](create-documentdb-dotnet.md)，其中逐步引導您建立的帳戶和開始使用 Cosmos DB。 

或者，如果您想要深入了解客戶使用 Cosmos DB tooread，hello 下列客戶劇本可用：

* [Jet.com](https://jet.com)。電子商務挑戰者眼睛 hello 最上層的位置，hello Microsoft 雲端上執行，利用 Cosmos DB 全域的縮放比例。
* [Asos.com](http://www.asos.com/)。Asos.com 是一個英國線上時尚與美妝商店。 Asos 的主要對象為年輕成人，除了自有的服飾與配件之外，還販售超過 850 個品牌的商品。
* [Toyota](https://www.toyota.com/)。 Toyota Motor Corporation 是一個日本汽車製造商。 Toyota 將 Cosmos DB 運用在全球 IoT 應用程式。
* [Citrix](https://customers.microsoft.com/story/citrix)。 Citrix 使用 Azure Service Fabric 和 Azure Cosmos DB 開發單一登入解決方式。
* [TEXA](https://customers.microsoft.com/story/texaspa) TEXA 針對汽車車主推出的革命性 IoT 解決方案不僅可幫助節省時間、金錢、燃料，還可能幫助保命。
* [Domino's Pizza](https://www.dominos.com)。 Domino's Pizza Inc. 是一個美國披薩餐廳連鎖店。
* [Johnson Controls](http://www.johnsoncontrols.com)。 Johnson Controls 是一個全球多樣化技術與多重產業領導者，為超過 150 個國家/地區的客戶提供多種服務。
* [Microsoft Windows、通用市集、Azure IoT 中樞、Xbox Live 及其他網際網路級別的服務](https://azure.microsoft.com/blog/how-azure-documentdb-planet-scale-nosql-helps-run-microsoft-s-own-businesses/)。 Microsoft 如何使用 Azure Cosmos DB 來建置可大幅調整的服務。
* [Microsoft 資料與分析小組](https://customers.microsoft.com/story/microsoftdataandanalytics)。 Microsoft 的「資料與分析」小組使用 Azure Cosmos DB 來達成全球級別的巨量資料收集
* [Sulekha.com](https://customers.microsoft.com/story/sulekha-uses-azure-documentdb-to-connect-customers-and-businesses-across-india)。Sulekha 會使用個印度 Azure Cosmos DB tooconnect 客戶和企業。
* [NewOrbit](https://customers.microsoft.com/story/neworbit-takes-flight-with-azure-documentdb)。 NewOrbit 使用 Azure Cosmos DB 而大展鴻圖。
* [Affinio](https://customers.microsoft.com/doclink/affinio-switches-from-aws-to-azure-documentdb-to-harness-social-data-at-scale)。 Affinio 切換從 AWS tooAzure 大規模 Cosmos DB tooharness 共享資料。
* [Next Games](https://azure.microsoft.com//blog/the-walking-dead-no-mans-land-game-soars-to-1-with-azure-documentdb/)。 hello Walking Dead: No 攔截的土地遊戲 soars 太 #1 支援 Azure Cosmos DB。
* [Halo](https://azure.microsoft.com/blog/how-halo-5-guardians-implemented-social-gameplay-using-azure-documentdb/)。 Halo 5 如何使用 Azure Cosmos DB 來實作社交遊戲。
* [Cortana Analytics 資源庫](https://azure.microsoft.com/blog/cortana-analytics-gallery-a-scalable-community-site-built-on-azure-documentdb/)。 Cortana Analytics 資源庫 - 以 Azure Cosmos DB 為基礎所建置的可調整社群網站。
* [Breeze](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18602)。 只需幾分鐘的時間，前置整合器即可使用富彈性的雲端技術來提供跨國企業的全球資訊分析。
* [News Republic](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18639)。 新增智慧 toohello 新聞 tooprovide 資訊用途嚙合公民。 
* [SGS International](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18653)。 主要品牌的跨 hello 地球一致的色彩，請先將 tooSGS。 將會開啟 tooAzure。
* [Telenor](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18608)。 全域領導者 Telenor 使用 hello 雲端 toomove hello 啟動速度。 
* [XOMNI](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18667)。 hello 未來上執行的快速搜尋和 hello 簡單的資料流量的 hello 存放區。
* [Nucleo](https://customers.microsoft.com/story/azure-based-software-platform-breaks-down-barriers-bet)。 以 Azure 為基礎的軟體平台，將企業與客戶之間的障礙細分
* [Weka](https://customers.microsoft.com/story/weka-smart-fridge-improves-vaccine-management-so-more-people-can-be-protected-against-diseases)。 Weka 的智能冰櫃可改善疫苗管理，讓更多人受到保護免於疾病危害
* [Orange Tribes](https://customers.microsoft.com/story/theres-more-to-that-food-app-than-meets-the-eye-or-the-mouth)。 沒有更多 toothat 食物應用程式比符合 hello 眼睛或 hello 說話。
* [Real Madrid](https://customers.microsoft.com/story/real-madrid-brings-the-stadium-closer-to-450-million-f)。 實際馬德里帶來 hello 場地接近 too450 百萬個風扇周圍 hello 地球，以 hello Microsoft 雲端。
* [Tuku](https://customers.microsoft.com/story/tuku-makes-car-buying-fun-with-help-from-azure-services)。 利用 Azure 服務的協助，TUKU 讓購車有樂趣
