---
title: "指定預測的能源 aaaCortana 智慧方案範本腳本 |Microsoft 文件"
description: "使用 Microsoft Cortana Intelligence 的解決方案範本，協助預測能源公共事業公司的需求。"
services: cortana-analytics
documentationcenter: 
author: ilanr9
manager: ilanr9
editor: yijichen
ms.assetid: 8855dbb9-8543-45b9-b4c6-aa743a04d547
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/24/2016
ms.author: ilanr9;yijichen;garye
ms.openlocfilehash: 32fc6ece7e24ced34282baf107548039694a38b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-solution-template-playbook-for-demand-forecasting-of-energy"></a>能源需求預測的 Cortana Intelligence 解決方案範本教戰守則
## <a name="executive-summary"></a>執行摘要
在過去幾年來，物聯網 (IoT)，hello 替代能源來源和巨量資料有合併的 toocreate vast 機會 hello 公用程式 」 和 「 能源網域中。 在 [hello 相同的時間、 hello 公用程式和 hello 整個能源磁區過簡維取用者要求 (demand) 更好的方式 toocontrol 他們使用的能源耗用量。 因此，hello 公用程式和智慧方格公司都非常需要 tooinnovate 中更新本身。 此外，許多的電源和公用程式格線變得過時且代價昂貴 toomaintain 和管理。 Hello 去年，期間 hello 團隊目前正在 hello 能源網域內的作業數目。 這些合作期間，我們發現很多情況下中的 hello 公用程式或 Isv （獨立軟體廠商） 有已想要預測未來的能源指定。 這些預測其目前和未來的企業中扮演著重要角色，並已成為不同使用案例中的 hello foundation。 其中包括短期與長期的電力負載預測、交易、負載平衡、電網最佳化等。巨量資料和進階分析 (AA) 方法，例如機器學習 (ML) 是 hello 關鍵推動者，以便產生精確又可靠的預測。  

在這個腳本中，我們擬定 hello 的商務和分析成功開發所需的指導方針，以及部署的能源需求預測方案。 這些建議的指導方針可協助公共事業、資料科學家和資料工程師建立全面運作、以雲端為基礎的需求預測解決方案。 對公司來說就是啟動其巨量資料和進階的分析歷程，這類解決方案可以代表其長期智慧方格策略中的 hello 初始種子。

> [!TIP]
> toodownload 的圖表提供此範本的架構概觀，請參閱[Cortana 智慧方案的範本架構需求預測的能源](cortana-analytics-architecture-demand-forecasting-energy.md)。  
> 
> 

## <a name="overview"></a>概觀
本文件涵蓋 hello 商務、 資料和使用 Cortana 智慧及在特定 Azure 機器學習 (AML) hello 實作和能源預測方案部署的技術層面。 hello 文件包含三個主要部分：  

1. 了解商務  
2. 了解資料  
3. 技術實作

hello**商務了解**一部分外框 hello 商務層面一個需求 toounderstand 並考慮先前 toomaking 投資決策。 它會說明如何 tooqualify hello 在手 tooensure 預測分析和機器學習會確實有效且適用的商務問題。 hello 文件進一步說明 hello 的機器學習和它的方式使用的 tooaddress 能源預測問題的基本概念。 本文將概述 hello 必要條件和 hello 限定性條件準則的使用案例。 另外也提供一些範例使用案例和商務案例。

資料是 hello 的任何機器學習解決方案的主要因素。 hello**資料了解**本文件涵蓋 hello 資料的一些重要特性。 本文將概述 hello 種類的所需的能源預測、 資料品質需求，以及何種資料來源通常存在的資料。 我們也會說明 hello 未經處理資料的實際磁碟機 hello 模型組件的使用的 tooprepare 資料功能的方式。

hello hello 文件的第三個部分涵蓋 hello**技術實作**解決方案的外觀。 特徵設計和模型位於 [hello 核心 hello 資料科學程序，並因此討論在詳細資料。 它涵蓋了 hello web 服務概念，也就是雲端部署的預測分析解決方案的重要工具。 我們也會概述端對端運作解決方案的一般架構。

此外，hello 文件包含許多參考資料，您可以使用 toogain hello 網域和技術的進一步了解。

我們想要 toocover 此文件 hello 更深入的資料科學程序中的數學和技術方面的重要 toonote 它。 您可以在 [Azure ML 文件](http://azure.microsoft.com/services/machine-learning/)和[部落格](http://blogs.microsoft.com/blog/tag/azure-machine-learning/)找到這些詳細資料。

### <a name="target-audience"></a>目標對象
hello 本文件的目標對象是商務和技術的人員希望 toogain 知識，以及了解的機器學習解決方案與這些使用的方式特別在 hello 能源預測網域內。

資料科學家也可以讀取此文件 toogain 進一步了解 hello 高的層級程序的磁碟機 hello 預測方案能源的部署中獲益。 它也可以在此內容中是使用的 tooestablish 的理想基準和起始點，如需詳細資訊和詳細進階資料。

### <a name="industry-trends"></a>產業趨勢
Hello 過去幾年來，在 IoT、 替代的能源來源和巨量資料有 hello 公用程式與能源空間合併 toocreate vast 的機會。 在 [hello 相同的時間、 hello 公用程式以及 hello 整個能源磁區過簡維取用者要求 (demand) 更好的方式 toocontrol 他們使用的能源耗用量。

許多公用程式和智慧能源公司有已 pioneering hello[智慧方格](https://en.wikipedia.org/wiki/Smart_grid)進行的情況下使用 hello 方格產生的 hello 資料的部署數目使用。 許多的使用情況下為中心的電力生產環境的 hello 固有特性： 其不可為累積或擱置在一旁存為存貨。 因此，生產出來就必須用掉，別無選擇。 想 toobecome 更有效率的公用程式只需要 tooforecast 功率耗用量，可讓它們更太因為**平衡供需**，因此防止能源 wastage**減少 greenhouse氣體發出**，並控制成本。

提到成本時，還有另一個重點，就是價格。 公用程式之間的新功能 tootrade 電源太帶入非常需要**預測未來的要求和未來的電力價格**。 這有助於公司決定他們的產量。

當我們使用 「 智慧型 」 的 hello 文字時，我們實際上是參考 tooa 方格，可以深入了解，然後進行預測。 它可以預測季節性的用電量變化，以及預知暫時性超載情況並自動調整 。 藉由從遠端調整耗用量 （與 hello 協助這些智慧公尺），可以處理當地語系化的多載的情況。 **第一次預測，然後做**，hello 方格讓自己更聰明經過一段時間。

這份文件，我們將著重於特定的使用案例涵蓋預測未來，系列 hello 其餘短期和長期的能源需求。 我們已在這些區域中使用幾個月，得到一些知識和技術可讓我們 tooproduce 業界等級結果。 將附近未來 hello hello 文件中也涵蓋其他使用案例。

## <a name="business-understanding"></a>了解商務
### <a name="business-goals"></a>商務目標
hello**能源示範**的目標是 toodemonstrate 典型的預測分析和機器學習解決方案，可部署非常短的時間範圍內。 具體來說，我們目前的焦點是推動能源需求預測解決方案，以快速實現並運用其商業價值。 在這個腳本中的 hello 資訊可協助完成下列目標 hello hello 客戶：

* 簡短時間 toovalue 機器學習架構方案
* 能力 tooexpand 試驗的使用案例的 tooother 使用案例或 tooa 更廣泛的範圍，根據其商務需求
* 快速獲得 Cortana Intelligence Suite 產品知識

使用這些目標謹記在心，這個腳本旨在傳送 hello 的商務和技術的知識可協助達成這些目標。

### <a name="power-load-and-demand-forecasting"></a>電力負載和需求預測
內 hello 能源磁區，可能有許多方面的需求預測可協助解決重要的商務問題。 事實上，需求預測可以視為多核心的使用案例 hello 產業中的 hello foundation。 一般而言，我們會考慮兩種能源需求預測︰短期和長期。 各有不同的用途並採用不同的方法。 hello hello 兩個之間的主要差異在於 hello 預測水平，這表示成 hello 未來的時間，我們會預測 hello 範圍。

#### <a name="short-term-load-forecasting"></a>短期負載預測
在 hello 內容中的能源需求，簡短詞彙載入預測 (STLF) 會定義為 hello 預測 hello 附近未來 hello 方格 （或整個 hello 方格） 的各個部分中的彙總負載。 在此內容中短期是定義的 toobe hello 範圍在 1 小時 too24 小時的時間範圍界限。 在某些情況下，範圍也可能長達 48 小時。 因此，STLF 是在 hello 格線的操作的使用案例中很常見。 以下是 STLF 導向的使用案例的一些例子：

* 供需平衡
* 電力交易支援
* 造市 (訂定電價)
* 電網運作最佳化
* [需求回應](https://en.wikipedia.org/wiki/Demand_response)
* 尖峰需求預測
* 需求面管理
* 負載平衡和預防超載
* 長期負載預測
* 故障和異常偵測
* 尖峰限電/調節 

STLF 模型主要是根據 hello 接近 （最後一天或週） 超過消耗資料，並使用預測的重要預測因數為溫度。 取得預測下一個小時 hello 和 too24 時數的精確溫度變得更少的一項挑戰現在天。 這些模型是敏感性較低的 tooseasonal 模式或長期的耗電量趨勢。

SLTF 解決方案也是可能 toogenerate 高容量的預測呼叫 （服務要求） 因為它們會被叫用每小時，並在某些情況下即使有較高的頻率。 它也是很常見的 toosee implantation 其中每個個別分站或轉換程式以獨立模型，因此 hello 磁碟區的預測要求更高。

#### <a name="long-term-load-forecasting"></a>長期負載預測
hello 目標的長詞彙負載預測 (LTLF) 是範圍從 1 週 toomultiple 月 （和在某些情況下的年數） 的時間範圍界限 tooforecast 電源需求。 此時間範圍最適用於規劃和投資使用案例。

長期的情況下，它是重要的 toohave 高品質資料所涵蓋的範圍的多個年份 （最小的 3 年）。 這些模型會通常季節性模式從擷取 hello 歷程記錄資料，並利用外部 predicators 這類位天氣和氣候模式。

這是很重要 hello 長 hello 預測水平的 tooclarify，可能是較不精確的 hello 預報 hello。 因此，這是重要 tooproduce 預測實際的 hello 以及一些信心間隔，讓人類的規劃程序至 toofactor hello 可能變化。

由於大部分規劃 LTLF hello 耗用量的案例，我們可以預期量較低的預測磁碟區 （做為比較 tooSTLF)。 我們通常會看到這些內嵌至視覺化工具，例如 Excel 或 power Bi 的預測，並可手動叫用由 hello 使用者。

### <a name="short-term-vs-long-term-prediction"></a>短期與長期預測
下表中的 hello 比較 STLF 和 LTLF 尊重 toohello 最重要的屬性中：

| 屬性 | 短期負載預測 | 長期負載預測 |
| --- | --- | --- |
| 預測時間範圍 |從 1 小時 too48 小時 |從 1 too6 月或更多 |
| 資料細微度 |每小時 |每小時或每日 |
| 一般使用案例 |<ul><li>供需平衡</li><li>尖峰時間預測</li><li>需求回應</li></ul> |<ul><li>長期規劃</li><li>電網資產規劃</li><li>資源規劃</li></ul> |
| 一般預測因子 |<ul><li>日或週</li><li>時</li><li>每小時溫度</li></ul> |<ul><li>月</li><li>日</li><li>長期溫度和氣候</li></ul> |
| 歷史資料範圍 |兩個 toothree 年的資料量 |五 too10 年的資料量 |
| 一般精確度 |5% 或更低的 MAPE* |25% 或更低的 MAPE* |
| 預測頻率 |每小時或每 24 小時產生一次 |每月、每季或每年產生一次 |

\*[MAPE](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error) – 百分比錯誤平均數

可以看到這個資料表中，是相當重要 toodistinguish 簡短的 hello 與 hello 長期預測的案例，因為這些代表不同的商務需求可能會有不同的部署和使用模式。

### <a name="example-use-case-1-esmart-systems--overload-optimization"></a>範例使用案例 1：Esmart Systems – 超載最佳化
重要的角色[智慧方格](https://en.wikipedia.org/wiki/Smart_grid)是 toodynamically 不斷地最佳化，並調整 hello 變更消耗模式。 用電量可能受到短期變化所影響，主要是溫度變動所造成 (例如，空調或暖氣的用電增加)。 在 hello 相同時間、 電源耗用量也會受到長期趨勢。 其中包括季節性效應、國定假日、長期用電量成長，甚至是經濟因素，例如消費者指數、石油價格和 GDP。

在此使用情況下， [eSmart](http://www.esmartsystems.com/)想 toodeploy 以雲端為基礎的解決方案，可讓預測 hello 傾向的 hello 方格的多載的情況在任何給定分站上。 特別是，eSmart 希望 tooidentify substations 所可能 toooverload hello 內下一個小時，因此可以採取 tooavoid 立即採取行動，或解決這種情況下使用。

為了精確和快速預測，必須實作三種預測模型︰

* 長時間詞彙模型，可讓預測的每個分站期間的電源消耗的 hello 下一步幾週或月數
* 短期模型，可讓在給定分站 hello 下一小時期間的多載情況的預測
* 在多個案例上提供未來溫度預測的溫度模型

hello 目標 hello 長期模型會是由 （要有其電源傳輸容量） 其傾向 toooverload toorank hello substations 期間 hello 下週或月。 這可讓 hello 建立之 substations 會做為輸入 hello 短期預測的簡短清單。 如同溫度 hello 長期模型的重要預測因數，沒有需要 tooconstantly 產生多案例溫度預測，而且這些摘要作為 toohello 長期模型的輸入。 然後叫用的 hello 短期預測的 toopredict 哪些分站位於可能 toooverload hello 個小時之內。

每個每個分站個別部署 hello 短期和長期的模型。 因此，這些模型 hello 實際執行需要大量的協調流程。 toogain 高預測精確度的 hello 短期而言，更細微的模型專用的 hello 一天的每個小時。 所有這些模型每小時執行和完成幾分鐘的時間 tooallow 足夠時間 toorespond 內執行，並採取預防動作，如有需要。 這個集合的模型所期刊定型使用 hello 最新的資料保持最新狀態。

[這裡](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18945)提供此使用案例的詳細資訊。

#### <a name="use-case-qualification-criteria--prerequisites"></a>使用案例檢定準則 – 必要條件
Cortana 智慧 hello 主要強度是其功能強大的能力 toodeploy 與標尺機器學習中心方案中。 它是設計的 toosupport 數以千計的同時執行的預測。 它可以自動調整 toomeet 變更的耗用量模式。 因此，解決方案的重點是精確度和運算效能。 例如，公用程式的公司有興趣產生精確的能源需求預測下一個小時，hello 和 hello 一天的每個小時。 在 [hello 另一方面，我們是較不感興趣的原狀 hello 需求為何預測的 toobe hello 問題要回答 （hello 模型本身會處理）。

因此，這是重要 toorealize 並非所有使用案例，以及商務問題可以有效地解決使用機器學習。

Cortana 智慧和機器學習服務可能是非常有效解決特定的商務問題，當符合下列準則的 hello:

* hello 手邊的商務問題是**預測**的本質。 預測的使用案例的範例是一個公用程式公司想要指定分站 toopredict 電源負載期間 hello 個小時之內。 在 [hello 另一方面、 分析和排名的歷程記錄需求的驅動程式將會是**描述性**的本質，因此較不適用。
* 沒有明確的**動作路徑**toobe 採取一次 hello 預測為止。 例如，預測分站上的多載 hello 下一小時期間可以觸發減少該分站相關聯的負載，並因此可能會防止多載的主動式動作。
* hello 使用案例表示**問題的一般型別**使得時解決它可以 pave hello 方式 toosolving 其他相似的使用案例。
* hello 客戶可以設定**量化和質化目標**toodemonstrate 成功的方案實作。 比方說，能源需求預測良好量化的目標是 hello 需要的精確度臨界值 (*例如*，向上 too5 允許 %s 錯誤) 或預測分站多載則 hello 有效位數 （真肯定率） 和指定的臨界值應該重新叫用 （真肯定的範圍）。 這些目標應該從客戶 hello 的商務目標。
* 沒有明確的**整合案例**與 hello 公司的商務流程。 例如，hello 分站負載預測可以整合到 hello 方格控制項中心 tooallow 多載防止活動。
* hello 客戶已準備好 toouse**具有足夠的品質的資料**toosupport hello 使用大小寫 (請參閱 hello 下一節中的多個**資料品質**，這個腳本的)。
* hello 客戶環節雲端資料中心架構或**以雲端為基礎的機器學習**，包括 Azure ML 和其他 Cortana 智慧套件的元件。
* hello 客戶是願意 tooestablish**端 tooend 資料流程**設備 hello 交付攸關 hello 雲端的資料，而且願意太**實施**hello 方案。
* hello 客戶太好**有專屬的資源**誰會主動執行期間 hello 初始試驗實作使知識和 hello 方案的擁有權可以轉移 toohello 客戶在成功時完成。
* hello 客戶資源應該**熟悉資料專業人員**，最好是資料科學家。

限定性條件的使用案例，根據上述條件的 hello 可以大幅改善 hello 成功率的使用案例，並建立 hello 實作的未來的使用情況良好攻擊。

### <a name="cloud-based-solutions"></a>以雲端為基礎的解決方案
在 Azure 上的 Cortana 智慧套件是位於 hello 雲端整合式的環境。 hello 部署的雲端環境中的進階的分析解決方案包含適用於企業的實質優點，並在 hello 相同的時間可能表示公司的最大的改變，仍然使用內部部署 IT 解決方案。 Hello 能源磁區中沒有清楚的趨勢的 hello 雲端運算的漸進式移轉。 變成手手中，這種趨勢以及 hello 智慧方格的 hello 開發如上所述，在**產業的趨勢**。 為這個腳本著重於雲端為基礎的解決方案 hello 能源網域中，很重要的 tooexplain hello 優點和部署的雲端式解決方案的其他考量。

或許 hello 的雲端式解決方案的最大優點是 hello 成本。 由於解決方案使用雲端部署的元件，因此不需要前期成本或相關的 COGS (銷貨成本) 元件成本。 這表示，沒有硬體、 軟體和 IT 維護，不需要 tooinvest，因而大幅降低商業風險。

另一個重要優點是雲端式解決方案 hello 隨用隨付成本結構。 做為計算或儲存用途的以雲端為基礎的伺服器，可以視需要而部署及調整。 這代表 hello 成本效率利用雲端架構的解決方案。

最後，不是需要投資 IT 維護或未來的基礎結構開發中，因為所有這是屬於 hello 雲端式供應項目。 toothat 範圍內，Cortana 智慧套件包括 hello 最佳中的服務類別，其路段圖地圖會持續發展。 新的特性、元件和功能持續地推出和演進。

才剛啟動轉換為 hello 雲端的公司中,，我們強烈建議 tootake 漸進的方法藉由實作雲端移轉路段圖地圖。 我們相信 utilities and hello 能源網域中的公司，hello 這個腳本中討論的使用案例代表試驗 hello 雲端中的預測分析解決方案的絕佳機會。

#### <a name="business-case-justification-considerations"></a>商務案例理由考量
在許多情況下，hello 客戶可能會想要建立讓特定的使用案例，以雲端為基礎的方案和機器學習是重要的元件的業務理由。 不同於在內部部署方案，在雲端為基礎的解決方案的案例中 hello hello 前置成本元件是最小而且大部分的 hello 成本項目都是實際的使用量與相關聯。 說 toodeploying 能源預測 Cortana Intelligence 的 suite 解決方案，可與單一的一般成本結構整合多個服務。 例如，資料庫 (*例如*，SQL Azure) 可以是使用的 toostore hello 未經處理資料，然後的 hello 實際預測 Azure ML 使用的 toohost hello 預測的服務。 在此範例中，hello 成本結構可能包含儲存體和交易式元件。

在 hello 相反地，其中一個應該深入了解運作預測 （短期或長期詞彙） 能源需求的 hello 商業價值。 事實上，很重要的 toorealize hello 商務價值，每個預測的作業。 例如，精確地預測 hello 的電源負載未來 24 小時內可以防止 overproduction 或有助於防止在 hello 方格上的多載以及這可以根據每日的財務節省定量。

基本公式來計算要求的 hello 財務利益預測解決方案將會是：![基本公式來計算要求的 hello 財務利益預測方案](media/cortana-analytics-playbook-demand-forecasting-energy/financial-benefit-formula.png)

Cortana 智慧套件提供隨用隨付計價模式，因為沒有需要支付固定的成本元件 toothis 公式。 每日、每月或每年都可以計算此公式。

[這裡](http://azure.microsoft.com/pricing/details/machine-learning/)提供 Cortana Intelligence Suite 和 Azure ML 目前的價格方案。

### <a name="solution-development-process"></a>解決方法開發程序
hello 開發週期的預測方案通常牽涉到全部都是我們在的 4 個階段的能源要求使用的雲端架構技術和服務內 hello Cortana 智慧套件。

Hello 下列圖表所示：

![智慧電網週期](media/cortana-analytics-playbook-demand-forecasting-energy/smart-grid-cycle.png)

hello 下列段落說明這 4 個步驟的程序：

1. **資料收集** – 任何以進階分析為基礎的解決方案都仰賴資料 (請參閱**了解資料**)。 具體來說，toopredictive 分析和預測時，我們依賴進行中的動態資料流。 中的能源需求預測 hello 案例中，此資料可以來自直接從智慧公尺來測量，或已由內部部署資料庫上彙總。 我們也依賴其他外部資料來源，例如天氣和溫度。 這個持續的資料流必須協調、排程及儲存。 [Azure Data Factory](http://azure.microsoft.com/services/data-factory/) (ADF) 是我們完成這項工作的主力工具。
2. **模型化**– 其中一個必須精確又可靠的能源預測的開發 （訓練） 和維持絕佳的模型，可使用 hello 歷程記錄資料，以及擷取 hello 意義並預測模式 hello 資料。 hello 區域的機器學習 (ML) 具有快速成長例行地開發所更進階的演算法。 Azure ML Studio 提供絕佳的使用者體驗，可協助利用 hello 最進階 ML 內完成工作流程的演算法。 該工作流程直覺式的流程圖所示，並包含 hello 資料準備、 擷取特徵、 模型和模型評估。 hello 使用者可以提取數百個包含在此環境中的各種模型。 這個階段中的 hello 結尾的資料科學家會具有完整評估並準備好進行部署的工作模型。
   
   下列圖表中的 hello 是一般的工作流程的說明：
   
   ![模型化工作流程](media/cortana-analytics-playbook-demand-forecasting-energy/modeling-workflow.png)
3. **部署**– 工作模型以 hello 下一個步驟是部署的手中。 這裡 hello 模型會轉換成 web 服務會公開 rest 式 API，可以從多種耗用用戶端 hello 網際網路上同時叫用。 Azure ML 提供簡易的方式直接從 hello Azure ML Studio 只要按一下按鈕的部署模型。 hello 幕後進行 hello 整個部署程序。 這個解決方案可以自動調整 toomeet 所需的 hello 耗用量。
4. **耗用量**– 在此階段中，我們實際將使用的預測模型 tooproduce 預測 hello。 可從使用者應用程式驅動 hello 耗用量 (*例如*，儀表板)，或直接從這類作業的系統需求/提供平衡系統或方格最佳化解決方案。 單一模型可以控管多個使用案例。

## <a name="data-understanding"></a>了解資料
之後涵蓋 hello 商務的考量 (請參閱**商務了解**) 的預測方案能源需求，我們正在準備 toodiscuss hello 資料組件。 任何預測性分析解決方案都仰賴可靠的資料。 在能源需求預測方面，我們依賴不同細微程度的用電量歷史資料。 作為 hello 原料的歷程記錄資料。 它將會進行詳細分析中的 hello 資料科學家會識別可以放入最後將會產生所需的 hello 預報一個模型的預測值 （也參考的 tooas 功能）。

在本章節 hello 其餘部分，我們將說明 hello 各種步驟和考量了解 hello 資料以及如何 toobring 它 tooa 可用的格式。

### <a name="hello-model-development-cycle"></a>hello 模型開發週期
需要仔細準備和規劃才能產生良好的預測模型。 細分 hello 模型分成多個步驟的程序，並將焦點放在一個步驟一次無法大幅改善 hello hello 整個程序結果。

hello 下列圖表說明如何 hello 模型程序無法分解成多個步驟：

![模型開發週期](media/cortana-analytics-playbook-demand-forecasting-energy/model-development-cycle.png)

做為可看到 hello 循環包含六個步驟：

* 問題編寫
* 資料擷取和資料探索
* 資料準備和特徵設計
* 模型化
* 模型評估
* 開發

在 [hello 本節其餘部分中，我們將說明 hello 個別步驟和項目 tooconsider 在每個步驟。

### <a name="problem-formulation"></a>問題編寫
Hello 最重要的第一個步驟需要時 tootake 先前 tooimplementing 任何預測分析解決方案，我們可以假設 hello 問題編寫。 我們會在這裡轉換 hello 商務問題，並將它分解 toospecific 項目所使用的資料和模型化技巧就可以解決。 這是很好的作法 tooformulate hello 問題為一組問題，我們都希望 tooanswer。 以下是一些可能的問題可能適用於能源需求預測 hello 範圍內：

* 在下一個小時或天 hello 個別分站 hello 預期負載是什麼？
* 執行 hello 一天的時間將方格遇到尖峰需求？
* 可能是我方格 toosustain hello 預期尖峰負載？
* Hello 電源站產生 hello 一天的每個小時期間的多少電力？

制定這些問題，讓我們 toofocus 上取得 hello 正確的資料和實作完全對齊手邊 hello 商務問題的解決方案。 此外，我們可以再設定可讓我們 tooevaluate hello 效能 hello 模型的一些重要指標。 比方說，正確度如何應該 hello 預測會和 hello 錯誤仍會依 hello 公司可接受的範圍是什麼？

### <a name="data-sources"></a>資料來源
hello 現代智慧方格收集各種組件和元件 hello 方格的資料。 這項資料代表 hello 作業的各個層面和 hello 的使用率 hello 電源方格。 Hello 在範圍內的預測 hello 能源需求，我們會限制 hello 反映 hello 實際需求耗用量的資料來源上的討論。 能源消耗量的重要來源之一是智慧型電表。 Hello 地球周圍的公用程式用於其取用者快速地部署智慧公尺。 智慧公尺記錄 hello 實際功率耗用量，並持續轉送此資料回復 toohello 公用程式的公司。 資料收集及傳送回在固定的間隔中，範圍從每 5 分鐘 too1 小時。 從遠端進行程式設計更進階的智慧公尺 toocontrol 並平衡 hello 家庭成員內的實際耗用量。 智慧型電表資料相當可靠，而且包含時間戳記。 因此成為需求預測的重要元素。 計量資料可以彙總 （加總） hello 方格拓樸內的各個層級： transformer、 分站、 區域，*等*。我們接著可以挑選所需的 hello 彙總層級 toobuild 預測模型它。 比方說，如果 hello 公用程式的公司會像 tooforecast 未來載入其方格 substations 的每個上所有計量資料可以是彙總的每個個別分站，然後用於預測模型的 hello 做為輸入。 我們 toosmart 公尺做為內部的資料來源。

可靠的能源需求預測也依賴其他外部資料來源。 Hello 天氣或更精確地說 hello 溫度一個重要的因素會影響功率耗用量。 歷史資料顯示室外溫度和用電量之間有很大的關聯性。 熱 summer 天內，讓取用者使用的其空中氣溫和加熱系統 hello 冬季開機期間。 可靠的來源歷程記錄的溫度在 hello 格線位置為因此索引鍵。 此外，我們也依賴精確預測的溫度當作用電量的預測因子。

其他外部資料來源也有助於建立能源需求預測模型。 其中可能包括長期氣候變化、經濟指標 (例如GDP) 等。 本文中不討論其他這些資料來源。

### <a name="data-structure"></a>資料結構
識別 hello 所需的資料來源之後，我們會像是已收集的未經處理資料，包括 hello tooensure 更正資料功能。 toobuild 可靠要求預測模型中，我們需要 tooensure hello 收集資料，包括資料元素，可協助預測 hello 未來的要求。 以下是一些有關 hello 資料 （結構描述） hello 未經處理資料結構的基本需求。

hello 未經處理資料是由資料列和資料行所組成。 每個度量單位以單一資料列表示。 每個資料列包含多個資料行 （也參考的 tooas 功能或欄位）。

1. **時間戳記**– hello 時間戳記欄位代表 hello hello 度量錄製時的實際時間。 它應該符合其中一種 hello 一般日期/時間格式。 應該同時包含日期和時間部分。 在大部分情況下，您就不必 hello 時間 toobe 記錄到 hello 第二個資料粒度層級。 它是在其中記錄 hello 資料的重要 toospecify hello 時區。
2. **測量識別碼**-這個欄位會識別 hello 百分比或是 hello 測量裝置。 它是分類變數，可以是數字和字元的組合。
3. **耗用量值**– 這是在指定的日期/時間的 hello 實際耗用量。 hello 耗用量可以測量 kwh (kilowatt-hour) 或任何其他慣用單位。 請務必 hello 度量單位的 toonote 跨 hello 資料中的所有度量均必須維持一致。 在某些情況下，可能分成 3 個電源階段來供應用電量。 在此情況下我們需要 toocollect hello 獨立耗用量的所有階段。
4. **溫度**– hello 溫度通常會收集從獨立的來源。 不過，它應該與 hello 耗用量資料相容。 它應該包含時間戳記 （如上所述），以允許它 toobe 同步處理與 hello 實際的耗電量資料。 hello 溫度值攝氏或華氏中都可以指定，但是應該保持一致跨所有量值。
5. **位置 –** hello 位置欄位是通常 hello 已收集 hello 溫度資料的位置與相關聯。 它可以用郵遞區號或經緯度 (lat/long) 格式表示。

下表中的 hello 顯示理想的耗用量和溫度資料格式的範例：

| <bpt id="p1">**</bpt>Date<ept id="p1">**</ept> | <bpt id="p1">**</bpt>Time<ept id="p1">**</ept> | <bpt id="p1">**</bpt>Meter ID<ept id="p1">**</ept> | <bpt id="p1">**</bpt>Phase 1<ept id="p1">**</ept> | <bpt id="p1">**</bpt>Phase 2<ept id="p1">**</ept> | <bpt id="p1">**</bpt>Phase 3<ept id="p1">**</ept> |
| --- | --- | --- | --- | --- | --- |
| 7/1/2015 |10:00:00 |ABC1234 |7.0 |2.1 |5.3 |
| 7/1/2015 |10:00:01 |ABC1234 |7.1 |2.2 |4.3 |
| 7/1/2015 |10:00:02 |ABC1234 |6.0 |2.1 |4.0 |

| **Date** | <bpt id="p1">**</bpt>Time<ept id="p1">**</ept> | <bpt id="p1">**</bpt>Location<ept id="p1">**</ept> | <bpt id="p1">**</bpt>Temperature<ept id="p1">**</ept> |
| --- | --- | --- | --- |
| 7/1/2015 |10:00:00 |11242 |24.4 |
| 7/1/2015 |10:00:01 |11242 |24.4 |
| 7/1/2015 |10:00:02 |11242 |24.5 |

從上面可以看出，這個範例包含與 3 電源階段相關聯的 3 個不同用電量值。 另外請注意會分隔 hello 日期和時間的欄位，不過它們也可以結合成單一資料行。 在此情況下 hello 位置資料行被表示的 5 位數郵遞區號格式和 hello 溫度為攝氏溫度格式中。

### <a name="data-format"></a>資料格式
Cortana 智慧套件可以支援 hello 最常見資料格式，例如 CSV、 TSV、 JSON、*等*。請務必該 hello 資料格式的 hello 整個專案生命週期 hello 維持一致。

### <a name="data-ingestion"></a>資料擷取
因為能源需求預測經常與經常預測，所以我們必須確定 hello 未經處理資料透過實心而且可靠的資料擷取程序流動。 hello 擷取程序必須保證 hello 未經處理的資料可用於預測程序所需的 hello 次 hello。 這表示 hello 資料擷取頻率應大於 hello 預測的頻率。

例如： 如果預測方案會產生每日上午 8:00 的新預測，則我們需要上次 hello 所有都 hello 資料期間所收集的 tooensure 我們需要 24 小時內有已完全內嵌到該點為止，而且擁有包含都 hello tooeven過去一小時的資料。

若要 tooaccomplish，Cortana 智慧套件提供的各種方式 toosupport 可靠的資料擷取程序。 這將會進一步討論在 hello**部署**本文件一節。

### <a name="data-quality"></a>資料品質
hello，才能執行可靠且正確的要求預測的原始資料來源必須符合一些基本的資料品質準則。 雖然進階的統計方法是使用的 toocompensate 一些可能的資料品質問題，我們仍需要 tooensure 擷取新的資料時，我們會跨越某些基底的資料品質臨界值。 以下是關於原始資料品質的一些考量︰

* **遺漏值**– 這是指 toohello 情況下，當未收集特定的度量單位。 這裡 hello 基本的要求就是遺漏值比率該 hello 不應該大於 10%的任何給定的時間間隔。 如果遺漏單一值，應該以預先定義的值 (例如：'9999') 表示，而不是可能為有效度量的 '0'。
* **測量精確度**– hello 耗用量或溫度的實際值的記錄應該正確。 不正確的測量會產生不正確的預測。 一般而言，hello 測量錯誤應該低於 1%相對 toohello true 值。
* **時間的度量**– 需要該 hello 實際時間戳記 hello 所收集的資料將不偏離超過 10 秒的 hello 實際度量相對 toohello true 時間。
* **同步處理** – 使用多個資料來源時 (例如，用電量和溫度)，必須確保它們之間沒有時間同步化的問題。 這表示，任何兩個獨立的資料來源的 hello 收集時間戳記之間的差異不應超過 10 秒以上 hello 時間。
* **延遲** - 如上所述，在**資料擷取**中，我們依賴可靠的資料流和擷取程序。 toocontrol，我們必須確定我們控制 hello 資料延遲。 這被指定為 hello hello 實際度量以來所的 hello 時間與時差 hello 時間，在已載入 hello Cortana 智慧套件儲存至並且可供使用。 負載短期預測的 hello 總延遲時間不應該超過 30 分鐘。 長期負載預測 hello 總延遲時間不應該大於 1 天。

### <a name="data-preparation-and-feature-engineering"></a>資料準備和特徵設計
一旦 hello 未經處理的資料已被內嵌 (請參閱**資料擷取**) 且已安全地儲存，它會準備 toobe 處理。 hello 資料準備階段是基本上取得 hello 未經處理資料並將轉換 （轉換，才可遏制） 到模型化階段 hello 的表單。 可能包含簡單的作業，例如使用 hello 未經處理資料資料行是使用其實際的測量的值、 標準化的值、 更複雜的作業例如[時間延遲](https://en.wikipedia.org/wiki/Lag_operator)，和其他人。 hello 新建立的資料行參考的 tooas 資料功能和 hello 程序產生這些是參考的 tooas 功能工程團隊。 Hello 結束此程序中，我們會有取自 hello 未經處理資料，並可用於模型化新的資料集。 此外，hello 資料準備階段必須 tootake care of 遺漏值 (請參閱**資料品質**) 並為其進行補救。 在某些情況下，我們還需要所有值都都表示 toonormalize hello 資料 tooensure hello 相同的標尺。

本章節內容，我們列出了一些 hello 一般資料功能隨附的 hello 能源需求預測模型。

**時間驅動功能：**這些功能衍生自 hello 日期/時間戳記資料。 這些在擷取後會轉換成類別特徵，例如︰

* 時間一天 – 這是採用值從 0 too23 hello 當日 hello 小時
* 一天一週 – 這代表 hello 星期幾 hello 及接受從 1 （星期日） too7 （星期六） 的值
* 日期的月 – 這代表 hello 實際日期，並可以接受從 1 too31 值
* 月份的年份 – 這代表 hello 月份和接受從 1 （一月） too12 （十二月） 的值
* 週末 – 這是所需的值是 0 hello 工作日或 1 週末的二進位值功能
* 假日-這是採用一般的日次或 1 的 hello 的值是 0，假日的二進位值的功能
* 傅立葉條款 – hello 的傅立葉條款將會衍生自 hello 時間戳記的加權和 hello 資料中的使用的 toocapture hello 季節性 （循環）。 因為資料中可能有多個季節，我們可能需要多個傅立葉項。 例如，需求值可能有每年、每週和每日季節/週期，所以需要 3 個傅立葉項。

**獨立的度量功能：** hello 獨立功能包括所有 hello 資料元素，我們想 toouse 預測指標為在我們的模型。 這裡我們排除 hello 相依功能我們會需要 toopredict。

* Lag 功能 – 這些是時間移位 hello 實際要求的值。 比方說，延隔時間 1 功能會保留在 hello （假設每小時的資料） 的前一小時相對 toohello 目前時間戳記的 hello 要求值。 同樣地，我們可以加入延隔 2，延遲 3，*等*。 可用的 lag 功能 hello 實際組合取決於 hello 模型化階段期間評估 hello 模型的結果。
* 長期趨勢 – 這項功能代表 hello 線性成長年份間的需求。

**相依的功能：** hello 相依的功能是，我們都希望 hello 資料資料行我們模型 toopredict。 與[受監督的機器學習](https://en.wikipedia.org/wiki/Supervised_learning)，我們需要先使用來定型 hello 模型 hello 相依的功能 （這也是參考的 tooas 標籤）。 這可以讓 hello 模型 toolearn hello 模式 hello 與 hello 相依功能相關聯的資料。 預測的能源需求通常會想 toopredict hello 實際需求，因此我們會做 hello 相依的功能。

**遺漏值的處理：** hello 資料準備階段，我們需要 toodetermine hello 最佳策略 toohandle 遺漏值。 這是大部分完成使用 hello 各種統計[資料插補法](https://en.wikipedia.org/wiki/Imputation_\(statistics\))。 中的能源需求預測 hello 案例中，我們通常推算遺漏值使用從先前可用的資料點的移動平均。

**資料正規化：**資料正規化是另一種轉換，也就是使用的 toobring 所有數值資料，例如要求預測到類似的規模。 這通常有助於改善 hello 模型的精確度和有效位數。 我們通常需要執行此動作 hello 實際值除以 hello hello 資料範圍。
這會向下調整 hello 原始值，為較小的範圍，通常介於-1 和 1 之間。

## <a name="modeling"></a>模型化
hello 模型化階段是 hello 資料到模型 hello 轉換發生的位置。 在 [hello 那里此程序的核心被進階掃描 hello 歷程記錄資料 （訓練資料）、 擷取模式，並建立模型的演算法。 該模型可以稍後使用的 toopredict 但尚未使用的 toobuild hello 模型的新資料。

我們擁有可運作的可靠一旦模型，就可以利用它為結構化的 tooinclude hello tooscore 新資料所需功能 (X)。 hello 評分程序將使用 hello 保存模型 (object hello 訓練階段)，以及預測由 Ŷ 所表示的 hello 目標變數。

### <a name="demand-forecasting-modeling-techniques"></a>需求預測模型化技巧
在 hello 的預測，我們不提供要求的情況下使用的時間來排序歷程記錄資料。 我們通常會參考包含 hello 時間維度作為 toodata[時間序列](https://en.wikipedia.org/wiki/Time_series)。 hello 目標的時間序列模型是相關的 toofind 時間作趨勢、 季節性、 自動相互關聯 （經過一段時間相互關聯），並制定這些模型。

近年來進階的演算法已開發的 tooaccommodate 時間序列預測和 tooimprove 預測精確度。 在此我們簡短討論其中一部分。

> [!NOTE]
> 本節不是用來做為機器學習和預測概觀而不是模型常用於需求預測的技術的簡短問卷調查用預定的 toobe。 如需詳細資訊和教育有關時間序列預測的資料，強烈建議 hello 線上書店[預測： 原則和作法](https://www.otexts.org/book/fpp)。
> 
> 

#### <a name="ma-moving-averagehttpswwwotextsorgfpp62"></a>[**MA (移動平均)**](https://www.otexts.org/fpp/6/2)
移動平均是 hello 第一次分析的技術曾經用於時間序列預測的其中一個，它仍然是目前為止的 hello 最常使用的技術之一。 它也是 hello 基礎更進階的預測技術。 與移動平均我們，以減低 hello K 最新的點，其中 K 代表移動平均的 hello hello 順序透過預測 hello 下一個資料點。

hello 移動平均技術 hello 作用的 hello 預測平滑化，因此無法處理也有大波動愈高 hello 資料中。

#### <a name="ets-exponential-smoothinghttpswwwotextsorgfpp75"></a>[**ETS (指數平滑法)**](https://www.otexts.org/fpp/7/5)
指數平滑效果 (ETS) 是一系列的順序 toopredict hello 下一個資料點中使用的最新的資料點的加權的平均值的各種方法。 hello 概念是 tooassign 更高的加權 toomore 新的值，並逐漸降低此加權較舊的測量值。 有不同的方法與這個家族的數字，其中包含這類處理 hello 資料中的季節性的[被 Winters 季節性方法](https://www.otexts.org/fpp/7/5)。

其中某些方法也會納入 hello 季節性的 hello 資料。

#### <a name="arima-auto-regression-integrated-moving-averagehttpswwwotextsorgfpp8"></a>[**ARIMA (自迴歸整合移動平均)**](https://www.otexts.org/fpp/8)
自迴歸整合移動平均 (ARIMA) 是常用於時間序列預測的另一系列的方法。 實際上是結合自迴歸方法與移動平均。 自動迴歸方法擷取上一個時間序列值順序 toocompute hello 下一個日期點中，藉此使用迴歸模型。 ARIMA 方法也適用於差異包括計算 hello 資料點之間的差異，以及使用這些 hello 原始測量值的方法。 最後，ARIMA 也利用 hello 移動平均上面所討論的技術。 hello 所有這些方法，以各種方式是什麼建構 hello 系列的 ARIMA 方法。

ETS 和 ARIMA 現在廣泛用於能源需求預測和其他許多的預測問題。 在許多情況下這會結合在一起 toodeliver 非常精確的結果。

**一般的多個迴歸**迴歸模型可能是機器學習和統計資料的 hello 網域內 hello 最重要模型化方法。 在時間序列的 hello 內容中，我們使用迴歸 toopredict hello 未來值 (*例如*，視需要的)。 在迴歸，我們需要 hello 預測值的線性組合，hello 定型程序期間了解這些預測量的 hello 加權 （也參考的 tooas 係數）。 hello 目標是 tooproduce 迴歸線，將預測我們預測的值。 迴歸方法，就適合 hello 目標變數是數值，因此也符合時間序列預測。 有各種不同的迴歸方法，包括非常簡單的迴歸模型，例如[線性迴歸](https://en.wikipedia.org/wiki/Linear_regression)，還有更進階的迴歸方法，例如決策樹、[隨機樹系](https://en.wikipedia.org/wiki/Random_forest)、[類神經網路](https://en.wikipedia.org/wiki/Artificial_neural_network)和推進式決策樹。

建構能源需求預測為迴歸問題，讓我們很大的彈性在 hello 實際要求時間序列資料與外部因素，例如溫度選取我們可合併的資料功能。 Hello 工程功能中會討論 hello 選取功能的詳細資訊 (請參閱**資料準備和功能工程**) 這個腳本的區段。

從我們的實作及能源需求預測試驗部署經驗，我們找到了 hello Azure ML 中可用的進階的迴歸模型傾向 tooproduce hello 獲得最佳結果，我們請加以使用。

## <a name="model-evaluation"></a>模型評估
模型評估具有重要的角色內 hello**模型開發週期**。 在這個步驟會採用驗證 hello 模型和其效能以真實資料。 Hello 模型步驟期間針對 hello 模型定型使用 hello 可用資料的一部分。 Hello 評估階段中，我們採用 hello hello 資料 tootest hello 模型部分。 實際上這表示我們放入 hello 模型的新資料經過重新編排，且包含的 hello 相同功能與 hello 訓練資料集。 不過，在 hello 驗證過程中，我們使用 hello 模型 toopredict hello 目標變數而非提供 hello 可用的目標變數。 通常我們 toothis 處理序做為模型評分。 然後我們將會使用 hello，則為 true 的目標值和比較它們與 hello 的預測。 hello 現在的目標是 toomeasure 和 hello 預測錯誤時，這表示 hello hello 預測與 hello true 值差異降到最低。 量化 hello 錯誤度量是索引鍵，因為我們會喜歡 toofine 微調 hello 模型，並驗證是否實際減少 hello 錯誤。 藉由修改模型的參數，以控制 hello 學習程序，或藉由新增或移除資料功能，就可以完成微調 hello 模型 (稱為 tooas[參數掃掠](https://channel9.msdn.com/Blogs/Azure/Data-Science-Series-Building-an-Optimal-Model-With-Parameter-Sweep))。 實際上，表示我們可能需要 tooiterate 之間 hello 特徵設計，建立模型和模型評估階段多次，直到我們可以 tooreduce hello 錯誤 toohello 所需層級。

這是很重要 tooemphasis hello 預測錯誤絕對不會有零永遠不會完全可以預測每個結果的模型。 不過，沒有的特定範圍的 hello 企業可接受的錯誤。 在 hello 驗證過程中，我們希望 tooensure 我們模型的預測錯誤位於 hello 層級或優於 hello 商務容錯層級。 因此是重要的 hello hello 開頭的 hello 可容忍錯誤 tooset hello 層級循環期間 hello**問題編寫**階段。

### <a name="typical-evaluation-techniques"></a>一般評估技術
有各種方法可測量和量化預測誤差。 這一節中，我們將著重 hello 討論在評估技術相關 tootime 序列和預測的能源需求的特定。

#### <a name="mapehttpsenwikipediaorgwikimeanabsolutepercentageerror"></a>[**MAPE**](https://en.wikipedia.org/wiki/Mean_absolute_percentage_error)
MAPE (Mean Absolute Percentage Error) 代表「平均絕對百分比誤差」。 與 MAPE 我們會計算每個預測的點與 hello 該點的實際值之間的 hello 差異。 然後，我們量化 hello 錯誤，每個點所計算的 hello 差異相對 toohello 實際值的 hello 比例。 在最後一個步驟中，我們計算這些值的平均。 用於 MAPE hello 數學公式是 hello 下列：

![MAPE 公式](media/cortana-analytics-playbook-demand-forecasting-energy/mape-formula.png)
*其中 A<sub>t</sub>是 hello 實際值，F<sub>t</sub>是 hello 預測的值，而 n 為 hello 預測水平。*

## <a name="deployment"></a>部署
一旦我們已經向 hello 模型化階段固定和驗證 hello 模型效能很好 toogo 進入 hello 部署階段。 在此內容中，部署表示啟用 hello 客戶 tooconsume hello 模型上它的大規模執行實際的預測。 部署的 hello 概念是在 Azure ML 中的索引鍵，因為我們的主要目標是 tooconstantly 叫用為相對於 toojust 取得 hello 深入了解從 hello 資料的預測。 hello 部署階段是 hello 部分，我們在此啟用 hello 模型 toobe 耗用大的規模。

在 hello 內容中的預測能源需求，我們的目標，請同時確保資料供 hello 模型，而且該 hello 預測的資料會傳送後 toohello 耗用用戶端是 tooinvoke 連續和定期預測。

### <a name="web-services-deployment"></a>Web 服務部署
hello 主要部署建置組塊在 Azure ML 是 hello web 服務。 這是 hello 最有效方式 tooenable 耗用量的 hello 雲端中的預測模型。 hello Web 服務封裝 hello 模型，並將其包裝以[RESTful](http://www.restapitutorial.com/) API （應用程式開發介面）。 hello API 可用來當做 hello 如下圖所示的任何用戶端程式碼的一部分。

![Web 服務部署和取用](media/cortana-analytics-playbook-demand-forecasting-energy/web-service-deployment-and-consumption.png)

可以看出 hello 和 web 服務部署在 hello Cortana 智慧套件雲端可透過其公開 REST API 端點叫用。 同時叫用不同類型的用戶端跨各種網域 hello hello Web API 服務。 hello web 服務也可以調整為支援數千個並行呼叫。

### <a name="a-typical-solution-architecture"></a>典型的解決方案架構
部署時，預測方案能源需求，我們有興趣部署結束 tooend 方案，超出 hello 預測 web 服務，並加速 hello 整個資料流。 在我們叫用新的預測 hello 階段，我們需要 toomake 確定該 hello 模型會送入的最新資料的功能。 這表示該 hello 新收集未經處理的資料會不斷地內嵌、 處理以及轉換成 hello 建置哪一個 hello 模型上設定必要的功能。 在 hello 相同時間，我們想要 toomake hello 預測的資料可供 hello 結束耗用用戶端。 範例資料流循環 （或資料管線） 如下所示 hello 圖：

![能源需求預測結束 tooEnd 資料流程](media/cortana-analytics-playbook-demand-forecasting-energy/energy-demand-forecase-end-data-flow.png)

這些是 hello 能源需求預測週期的一部分進行的 hello 步驟：

1. 數百萬個已部署的資料計量器不斷地即時產生用電量資料。
2. 這項資料收集後上傳至雲端儲存機制 (例如Azure Blob)。
3. 然後再開始處理 hello 未經處理資料是彙總的 tooa 分站或 hello 的商務所定義的區域層級。
4. hello 功能處理 (請參閱**資料準備和功能處理**) 再進行，因此會產生 hello 資料所需的模型定型或計分-hello 功能集的資料儲存在資料庫 (*例如*，SQL Azure)。
5. hello 重新定型集服務會叫用 toore 定型 hello 預測模型-更新版本的 hello 模型會保存，以便供 hello 計分 web 服務。
6. hello 計分 web 服務會叫用的排程，符合所需的 hello 預測的頻率。
7. hello 預測的資料會儲存在 hello 端耗用用戶端可以存取資料庫。
8. hello 耗用用戶端擷取 hello 預報、 套用回 hello 方格中，並根據所需的 hello 使用案例是使用它。

重要 toonote，這整個週期全面自動化並排程執行它。 此資料週期的 hello 整個協調流程可藉由使用工具，例如[Azure Data Factory](http://azure.microsoft.com/services/data-factory/)。

### <a name="end-tooend-deployment-architecture"></a>結束 tooEnd 部署架構
在順序 toopractically 部署能源需求預測的方案上 Cortana 智慧，我們需要 tooensure hello 所需的元件會建立並正確設定。

hello 下列圖表說明典型的 Cortana 智慧基礎架構實作，而且會協調上面所述的 hello 資料流程週期：

![結束 tooEnd 部署架構](media/cortana-analytics-playbook-demand-forecasting-energy/architecture.png)

如需每個 hello 元件和 hello 整個架構的詳細資訊，請參閱 toohello 能源方案範本。

