---
title: "在與 Azure-Cortana 智慧方案範本太空 aaaPredictive 維護 |Microsoft 文件"
description: "航太、公用事業和運輸中預測性維護的 Microsoft Cortana Intelligence 解決方案範本。"
services: cortana-analytics
documentationcenter: 
author: fboylu
manager: jhubbard
editor: cgronlun
ms.assetid: 2e8b66db-91eb-432b-b305-6abccca25620
ms.service: cortana-analytics
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: fboylu
ms.openlocfilehash: da863a89d2409a8b56b23066f15b4da13e1cd3d0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-solution-template-playbook-for-predictive-maintenance-in-aerospace-and-other-businesses"></a>航太與其他業務中預測性維護的 Cortana Intelligence 解決方案範本的腳本
## <a name="executive-summary"></a>執行摘要
預測性維護一個 hello 最 unarguable 好處包括極大的節省成本要求的預測分析的應用程式。 這個腳本旨在 hello 強調主要使用案例的預測性維護方案中提供的參考。
已備妥的 toogive hello 讀取器瞭解 hello 最常見商務案例的預測性維護，合格這類方案的商務問題的挑戰，必須有資料 toosolve 這些商務問題，預測模型使用這類的資料和最佳作法與範例方案架構的技術 toobuild 解決方案。
它也會描述 hello 細節的 hello 例如特徵設計開發預測的模型，模型開發和效能評估。 基本上，此腳本結合 hello 的商務和分析成功的開發和部署的預測性維護方案所需的指導方針。 已備妥的 toohelp hello 觀眾建立初始解決方案使用 Cortana 智慧套件，並特別 Azure Machine Learning 作為起點點其長期預測的維護策略這些指導方針。 hello 關於 Cortana Intelligence 的 Suite 和 Azure Machine Learning 文件位於[Cortana 分析](http://www.microsoft.com/server-cloud/cortana-analytics-suite/overview.aspx)和[Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/)頁面。

> [!TIP]
> 技術指南 tooimplementing 此解決方案範本，請參閱[預測性維護的技術指南 toohello Cortana 智慧方案範本](cortana-analytics-technical-guide-predictive-maintenance.md)。
> toodownload 的圖表提供此範本的架構概觀，請參閱[hello Cortana 智慧方案範本進行預測性維護的架構](cortana-analytics-architecture-predictive-maintenance.md)。
> 
> 

## <a name="playbook-overview-and-target-audience"></a>腳本概觀和適用對象
這個腳本是組織的 toobenefit 技術性和非技術性的對象，使用不同的背景和興趣預測性維護空間中的。 hello 腳本涵蓋 hello 不同類型的預測性維護方案和詳細資料請參閱這兩個高階層面 tooimplement 它們。 hello 內容平衡，符合這兩個 toohello 讀者只想要了解解決方案空間和 hello 類型的應用程式，以及那些要尋找 tooimplement 這些解決方案，因此感興趣的技術詳細資料。

大部分的 hello 這個腳本中的內容不會假設之前的資料科學知識或專業技術。 不過，hello 腳本的某些部分會稍微需要熟悉資料科學概念 toobe 無法依照實作詳細資料。 簡介的層級資料科學技術會需要這些章節中的 hello 材料 toofully 從中獲益。

hello 腳本的 hello 前半涵蓋簡介 toopredictive 維護應用程式、 如何 tooqualify 預測性維護方案，常用的集合案例與 hello 的商務問題的詳細資料，hello 圍繞這些使用的資料案例和實作這些預測性維護方案 hello 商業優勢。 這些區段不需要任何 hello 的預測分析網域中的技術知識。

在 hello 腳本 hello 下半年出爐，我們將討論 hello 類型的預測性維護應用程式以及如何實作這些瀏覽 hello 前半 hello 腳本 hello 中所述的使用案例的範例模型的預測模型技術。 因此文中逐步解說資料前處理的步驟，例如資料標記和特徵設計、模型選取、訓練/測試和效能評估最佳作法。 下列各節適合於技術讀者。

## <a name="predictive-maintenance-in-iot"></a>IoT 中的預測性維護
hello 的未排程的設備停機時間的影響可以是適用於企業極破壞性。 它是關鍵 tookeep 欄位設備執行順序 toomaximize 使用量和效能和成本、 未排程的停機時間降至最低。 只要，等候 hello 失敗 toooccur 不合理今天的商務作業場景中。 tooremain 競爭，公司尋找新方法 toomaximize 資產效能藉由使用 hello 資料收集來自各種不同的通道。 一個重要的差異 tooanalyze 之類的資訊是 tooutilize 預測分析的技術使用歷程記錄的模式 toopredict 未來結果。 Hello 最常用的這些解決方案是在呼叫其中一個預測性維護，這通常定義為但不是限於的 toopredicting 可能會失敗，在未來，所以資產可以是該 hello 監視 tooproactively 附近 hello 資產的識別失敗和 hello 失敗發生之前採取動作。 這些解決方案會偵測失敗模式 toodetermine 資產 hello 失敗的最大的風險。 早期找出問題有助於以更符合成本效益的方式部署有限的維護資源，並增強品質和供應鏈流程。

與 hello 崛起 hello 物聯網 (IoT) 應用程式，預測獲得維護 hello 產業 hello 資料收集中的增加注意和處理技術日趨成熟足夠 toogenerate，傳輸、 儲存及分析所有種類的批次或即時資料。 這類技術可讓您輕鬆開發和使用端對端解決方案的部署進階分析解決方案，與預測性維護方案提供論證 hello 最大的好處。

在高操作的風險，因為 toounexpected 失敗和有限深入了解複雜的商務環境中的問題 hello 根本原因的 hello 預測性維護網域範圍的商務問題。 hello 大部分這些問題可分類的 toofall 下 hello 遵循商務問題：

* 設備失敗的 hello 附近未來 hello 機率是什麼？
* Hello 剩餘有用的生命週期的 hello 設備是什麼？
* 什麼是 hello 原因失敗，而且維護動作應該執行的 toofix 這些問題？

藉由使用預測性維護 tooanswer 這些問題，企業可以：

* 在故障發生前發現故障情況，以降低營運風險並提高資產報酬率
* 減少不必要的以時間為基礎的維護作業並控制維護成本
* 改善整體品牌形象、消除不良名聲以及客戶流失所造成的銷售損失
* 藉由預測再訂購點來降低庫存量，進而降低庫存成本
* 探索模式連接的 toovarious 維護問題

預測性維護方案可以提供企業關鍵效能指標，例如健全狀況分數 toomonitor 即時資產條件，估計剩餘壽命的資產，針對主動式維護活動提供建議的 hello 和估計的訂單日期，以取代組件。

## <a name="qualification-criteria-for-predictive-maintenance"></a>預測性維護的限定準則
並非所有使用案例，或只要預測性維護可以有效地解決商務問題的重要 tooemphasize 它。 重要限定性條件準則包括 hello 問題的本質，存在於清除動作的路徑中順序 tooprevent 失敗，但它們在事先，最重要的是，會偵測到的預測是否具有足夠的品質 toosupport hello 資料使用的大小寫使用。 在這裡，我們會著重於建立成功的預測性維護方案 hello 資料需求。

當建置預測模型，我們會使用歷程記錄資料 tootrain hello 模型可再識別隱藏的模式，並進一步識別這些模式中 hello 未來的資料。 這些模型會使用其功能和預測的 hello 目標所描述的範例將定型。 hello 定型的模型是 hello 目標上的預期的 toomake 預測只會查看 hello 功能 hello 新的範例。 它是很重要的 hello 模型擷取 hello 之間關聯性的功能，並 hello 預測的目標。 為了有效的機器學習模型，我們需要定型資料，其中包含的功能，實際上朝向 hello 目標的預測意義 hello 資料的預測能力 tootrain 應該相關 toohello 精確的預測目標 tooexpect預測。

例如，如果 hello 目標是定型滾輪 toopredict 失敗，hello 培訓資料應包含滾輪相關功能 （例如遙測反映車輪、 hello 里程數、 汽車負載等 hello 健全狀況狀態。）。 不過，如果 hello 目標 toopredict 定型引擎失敗，我們可能需要另一組定型資料具有相關的引擎功能。 之前建置預測模型，我們預期 hello 商務專家 toounderstand hello 資料相關性需求，並提供所需的 tooselect hello 分析的資料子集相關 hello 定義域知識。

有三個重要的資料來源，我們查看符合資格商務問題 toobe 適用於預測性維護方案時：

1. 故障歷程記錄：在預測性維護應用程式中，故障事件通常非常罕見。 不過，當建置預測模型的預測失敗，hello 演算法需要 toolearn hello 正常作業模式，以及透過 hello 定型程序的 hello 失敗模式。 因此，很重要 hello 定型資料包含足夠數目的範例，在這兩個類別目錄中的順序 toolearn 這兩種不同的模式。 基於這個理由，我們要求資料有足量的故障事件。 維護記錄和組件取代歷程記錄或中資料也可用為 hello 網域專家識別失敗的 hello 定型的異常狀況中可以找到失敗事件。
2. 維護/修復歷程記錄： 基本資料來源的預測性維護方案 hello hello 資產包含取代 hello 元件的相關資訊的詳細的維護歷程記錄、 執行等，就會啟動預防性維護。它是極為重要 toocapture 這些事件中的當做這些影響 hello 降低模式和缺少這項資訊會造成誤導的結果。
3. 電腦的條件： 順序 toopredict 中多少天 （小時、 英哩、 交易等） 的電腦會持續之前失敗，我們假設 hello 電腦的健全狀況狀態隨著時間逐漸降低其作業期間。 因此，我們預期 hello 資料 toocontain 時間不同功能，擷取此過時模式，並且會導致 toodegradation 任何異常狀況。 在 IoT 應用程式，hello 遙測資料從不同的感應器會代表一個良好範例。 在訂單 toopredict 如果機器將會在時間內 toofail 理想的情況下 hello 資料應該擷取降低趨勢這個 hello 實際的失敗事件之前的時間範圍內。

此外，我們需要資料是直接相關 toohello 作業系統條件的 hello 目標資產的預測。 目標的 hello 決策根據這兩個商務需求與資料可用性。 製作 hello 訓練滾輪失敗預測，例如，我們可能會預測"如果 hello 滾輪是進行 toohave 失敗 」 或 「 hello 整個定型即將發生失敗的狀況 」。 hello 第一次一個目標更特定的元件而第二個為目標的 hello 定型失敗。 hello 第二個是需要比 hello 遠超過分散的資料元素的第一個，因此更難 toobuild 模型的一般問題。 相反地，只要查看 hello 高層級的訓練條件資料嘗試 toopredict 滾輪失敗可能無法將包含 hello 元件層級的資訊。 一般情況下，它會比一般更合理 toopredict 特定失敗事件。

通常會要求有關失敗的歷程記錄資料的一個常見問題是 「 如何許多失敗事件而需要的 tootrain 模型多少都會被視為 「 足夠 」？ 有許多的預測分析案例沒有清除回應 toothat 問題，通常是 hello 規定什麼是可接受的 hello 資料品質。 如果 hello 資料集不包含相關 toofailure 預測的功能，然後即使有許多失敗事件，請建立好模型可能不可能。 不過，hello 的經驗法則為 hello 詳細 hello 失敗事件 hello 更佳 hello 模型是，以及多少失敗範例所需的概略估計非常內容和資料而定的量值。 我們用來提出方法 toocope hello 解決問題的不具有足夠的失敗處理不平衡的資料集的 hello 章節中會討論此問題。

## <a name="sample-use-cases"></a>範例使用案例
本節著重於好幾個產業 (如航太、公用事業和運輸) 的各種預測性維護使用案例。 每個小節向下的切入到 hello 使用案例收集從這些區域，並討論商務問題、 hello 資料周圍 hello 商務問題和 hello 預測性維護方案的優點。

### <a name="aerospace"></a>航太
#### <a name="use-case-1-flight-delay-and-cancellations"></a>使用案例 1：航班延誤和取消
##### <a name="business-problem-and-data-sources"></a>*商務問題和資料來源*
Hello airlines 朝是 hello 大量成本，會因為 toomechanical 問題而延遲班機與相關聯的主要的商務問題的其中一個。 如果無法修復 hello 機械失敗，可能甚至會取消班機。 這會付出極大的代價，因為延誤會造成排程和作業問題、導致信譽不佳和客戶不滿，以及其衍生他許多問題。 航空公司對於事先預測這類機械故障特別感興趣，讓他們可以減少航班延誤或取消情況。 在這些情況下 hello 預測性維護方案 hello 目標是 toopredict hello 機率飛機，延遲或取消，例如維護歷程記錄和飛行路由資訊的相關資料來源為基礎。 此使用案例的 hello 兩個主要資料來源是 hello 飛行邊與頁面記錄檔。 飛行腳資料包含 hello 飛行路由詳細資料，例如離開和抵達離開和抵達機場、 等等的 hello 日期和時間的相關資料。頁面記錄資料會包含一系列的 hello 維護人員所記錄的錯誤和維護程式碼。

##### <a name="business-value-of-hello-predictive-model"></a>*商務價值，hello 預測模型*
使用 hello 可用的歷程記錄資料，預測模型是使用建立的機械問題會導致延遲或取消班機 hello 內未來 24 小時內的多分類演算法 toopredict hello 類型。 藉由進行這項預測，需要維護動作可以採取 toomitigate hello 風險飛機正在接受服務時，並因此防止可能的延遲或取消作業。 使用 Azure Machine Learning web 服務，hello 預測模型可以順暢地輕鬆整合到 airlines' 的現有作業系統平台。 

#### <a name="use-case-2-aircraft-component-failure"></a>使用案例 2：飛機零組件故障
##### <a name="business-problem-and-data-sources"></a>*商務問題和資料來源*
飛機引擎是非常重要又昂貴片段設備和引擎的一部分取代為在 hello 航空公司 hello 最常見維護工作。 航空公司的維護解決方案需要審慎管理零組件存貨的可用性、遞送和規劃。 正在元件的可靠性無法 toogather 智慧導致 toosubstantial 減少上投資成本。 hello 主要資料來源，針對這個使用案例是在 hello 條件的 hello 飛機上收集來自數個 hello 飛機提供資訊中的感應器的遙測資料。 維護記錄也是使用的 tooidentify，當發生元件失敗，並取代。

##### <a name="business-value-of-hello-predictive-model"></a>商務價值，hello 預測模型
多級分類模型所建立的失敗機率的預測到期 tooa hello 下個月內的特定元件。 航空公司可以運用這些解決方案，來降低零組件維修成本、改善零組件存貨可用性、降低相關資產的庫存量及改善維護計劃。

### <a name="utilities"></a>公用事業
#### <a name="use-case-1-atm-cash-dispense-failure"></a>使用案例 1：ATM 現金提領失敗
##### <a name="business-problem-and-data-sources"></a>*商務問題和資料來源*
資產狀態通常的大量產業的主管主要的作業風險 tootheir 企業是其資產的未預期的失敗。 舉例而說，機器故障 (例如銀行業的 ATM) 是經常發生的常見問題。 這幾種問題讓這類機器的操作人員非常渴望擁有預測性維護解決方案。 在此使用案例中預測問題是 toocalculate hello 機率 ATM 現金提款交易取得中斷到期 hello 現金分配程式，例如紙張夾在 tooa 失敗或部分失敗。 這個案例的主要資料來源是在提領現金鈔票時會收集測量數據的感應器讀數，以及收集一段時間的維護記錄。 感應器資料包含完成的每筆交易的感應器讀數，以及提領的每張鈔票的感應器讀數。 hello 感應器讀數提供度量，例如備忘稿粗細間之間距，請注意抵達距離等等。維護資料包含錯誤代碼與維修資訊。 這些是已使用的 tooidentify 失敗情況。

##### <a name="business-value-of-hello-predictive-model"></a>*商務價值，hello 預測模型*
兩個預測模型所建置 toopredict hello 現金提款交易失敗和 hello 分配在交易期間的個別便箋中的失敗。 事先因無法 toopredict 交易失敗，提款機可以是服務的主動 tooprevent 失敗發生。 此外，與注意失敗的預測，如果交易可能 toofail tooa 注意因為完成之前分配失敗，它可能是最佳的 toostop hello 程序並不完整的交易的 hello 客戶，而不是等待 hello 維護服務，即發出警告tooarrive 之後 hello 錯誤就會發生這可能導致 toolarger 客戶不滿。

#### <a name="use-case-2-wind-turbine-failures"></a>使用案例 2：風力渦輪機故障
##### <a name="business-problem-and-data-sources"></a>*商務問題和資料來源*
與環境感知的 hello 引發，wind 渦輪機已經 hello 能源層代的主要來源之一，它們通常成本數百萬美元。 Wind 渦輪機 hello 重要元件是 hello 產生器馬達的配有許多的感應器，可協助 toomonitor 渦輪機條件和狀態。 hello 感應器讀數包含重要資訊，它可以是使用的 toobuild 預測模型 toopredict 例如 hello 渦輪機元件的平均時間 toofailure 的重要關鍵效能指標 (Kpi)。 這個使用案例的資料來自位於三個不同廠區位置的多部風力渦輪機。 從度量關閉的 tooa 數百個感應器，從每個渦輪機記錄期間為一年每隔 10 秒。 這些讀數包括一些測量數據，例如溫度、發電機速度、渦輪機電力和發電機繞組。

##### <a name="business-value-of-hello-predictive-model"></a>*商務價值，hello 預測模型*
預測模型建置 tooestimate 剩餘有用的生命週期的產生器和溫度感應器。 透過預測故障，維護技術人員可以專注於很快就會有可能 toofail 的可疑渦輪機 hello 機率 toocomplement 以時間為基礎的維護制度。
此外，預測模型將深入了解 toohello 層級的失敗，它可以幫助商務 toohave hello 根進一步了解的問題會造成不同的因素 toohello 可能性比重。

#### <a name="use-case-3-circuit-breaker-failures"></a>使用案例 3：斷路器故障
##### <a name="business-problem-and-data-sources"></a>*商務問題和資料來源*
電力和天然氣的作業，包括產生、 發佈和銷售的電能需要大量的維護，以確保電源線可完全正常運作時間的能源 toohouseholds tooguarantee 傳遞。 幾乎每個實體受到電源問題發生的 hello 區域中，則會在這類作業的失敗。 斷路器而言非常重要的這類作業以其發生的任何損毀 toopower 行剪下發生問題與 short 電路 tooprevent 電流的設備。 此使用案例的商務問題是已知維護記錄檔、 命令歷程記錄和技術規格 toopredict 斷路器失敗。

此案例的三個主要資料來源是維護記錄，包括更正、 預防和系統化的動作、 操作資料，包括自動和手動命令傳送這類的開啟和關閉動作和技術的 toocircuit 詞工具屬性的每個斷路器，例如所做的年、 位置、 模型等相關規格資料。

##### <a name="business-value-of-hello-predictive-model"></a>*商務價值，hello 預測模型*
預測性維護方案可協助減少修復成本並增加的設備，例如斷路器的 hello 生命週期。 這些模型也有助於改善 hello 電源網路 hello 品質，因為模型提供事先減少 toofewer 中斷 toohello 服務會導致非預期的失敗的警告。

#### <a name="use-case-4-elevator-door-failures"></a>使用案例 4：電梯門故障
##### <a name="business-problem-and-data-sources"></a>*商務問題和資料來源*
大多數的大型電梯公司通常會有數百萬個電梯 hello 世界各地執行。 toogain 競爭優勢，其焦點在於這是重要的事情大部分 tootheir 客戶的可靠性。 Hello，甚至可能 hello 物聯網上繪製連線其電梯 toohello 雲端，並從電梯感應器及系統，收集資料是重要的商業智慧可大幅改善作業可以 tootransform 資料供應項目預測和先佔式維護，不是，還可用 toohello 競爭對手。 此案例的 hello 商務需求是的 tooprovide 預測潛在 hello 知識庫預測應用程式的媒體櫃門失敗所造成。 此實作中的資料包含三個部分電梯靜態功能 （例如識別項，合約維護頻率、 建置型別等），其使用方式資訊 （例如數字的媒體櫃門循環、 平均門關閉時間等） 所需的 hello 和失敗的記錄 （也就是失敗的歷程記錄和其原因）。

多級羅吉斯迴歸模型所建立與 Azure Machine Learning toosolve hello 預測問題，以 hello 整合靜態功能和功能，以及 hello 原因的歷程記錄的失敗記錄為類別標籤的使用方式資料。 使用此預測模型欄位技術人員所使用的行動裝置應用程式所 toohelp 提升工作效率。 當上站台 toorepair 電梯準備技術人員時，他可以參照 toothis 應用程式建議的原因和最佳課程的維護動作 toofix hello 電梯門盡快。

### <a name="transportation-and-logistics"></a>運輸和物流
#### <a name="use-case-1-brake-disc-failures"></a>使用案例 1：煞車碟盤故障
##### <a name="business-problem-and-data-sources"></a>*商務問題和資料來源*
車輛的一般維護原則包括校正性和預防性維護。 更正維護表示該 hello vehicle 修復後的失敗而導致嚴重的不便 toohello 驅動程式上造訪 toomechanic 浪費意外故障和 hello 時間的結果。 大部分的車輛也是主體 tooa 預防性維護原則，而這需要執行某些操作不會將帳戶 hello 實際條件 hello 汽車子系統的排程。 這些方法均無法成功地完全排除問題。 hello 特定使用案例是根據透過感應器安裝在其追蹤的歷程記錄驅動模式汽車的 hello tire 系統所收集的資料剎車組光碟失敗預測，並公開給其他 hello 汽車的條件。 此案例的 hello 最重要資料來源是測量，比方說，加速，煞車模式，推動距離、 速度等的 hello 感應器資料。這項資訊若搭配其他靜態資訊 (如汽車特徵)，有助於建置一組可用於預測性模型中的理想預測值。 另一組必要的資訊是推斷部分順序資料庫中的 hello 失敗資料 （當做 tookeep hello 備用的部分順序 dates 和 quantities 汽車正在服務中 hello 經銷商）。

##### <a name="business-value-of-hello-predictive-model"></a>*商務價值，hello 預測模型*
hello 商務價值，以預測的方法相當高。 預測性維護系統可以排程為基礎的預測模型的瀏覽 toohello 業者。 hello 模型可以根據感應式代表 hello hello 汽車和 hello 開車歷程記錄的目前狀況的資訊。 這種方法可以 hello 的非預期的失敗，可能也會發生之前 hello 下一步的定期維護的風險降至最低。
它也可減少不必要的預防性維護的 hello 數量。 驅動程式可以主動收到通知，部分變更可能需要幾週和供應 hello 經銷商具有相關資訊。 hello 經銷商然後無法事先準備個別維護封裝 hello 驅動程式。

#### <a name="use-case-2-subway-train-door-failures"></a>使用案例 2：地鐵列車門故障
##### <a name="business-problem-and-data-sources"></a>*商務問題和資料來源*
Hello 的延遲和捷運作業上的問題的主要原因之一是定型汽車的媒體櫃門失敗。 預測如果媒體櫃門失敗，或無法 tooforecast hello 天數 hello 下一步 door 失敗，直到，可能必須定型汽車是極為重要的遠見。 它提供 hello 機會 toooptimize 定型門服務，並減少 hello 定型的停機時間。

#### <a name="data-sources"></a>資料來源
此使用案例中有三個資料來源 

* **事件資料來定型**，這是 hello 的定型事件的歷程記錄 
* **維護資料** ，例如維護類型、工單類型和優先順序代碼，  
* **故障記錄**。

##### <a name="business-value-of-hello-predictive-model"></a>*商務價值，hello 預測模型*
兩個模型建置 toopredict 下一步天失敗機率使用二元分類和天後達到使用迴歸的失敗。 類似於 hello 較早的情況下，hello 模型建立服務的絕佳機會 tooimprove 品質，並由補充 hello 定期維護制度，進而提升客戶滿意度。

## <a name="data-preparation"></a>資料準備
### <a name="data-sources"></a>資料來源
hello 通用資料項目預測性維護問題可以摘要如下：

* 失敗記錄： hello 失敗記錄的電腦或 hello 機器內的元件。
* 維護記錄： hello 修復歷程記錄的電腦，例如錯誤碼、 上一個維護活動或元件取代。
* 電腦的條件和使用方式： hello 作業系統條件，例如資料的機器收集從感應器。
* 電腦的功能： hello 功能的電腦，例如引擎大小的製造商和型號，就會有位置。
* 運算子的功能： hello 功能 hello 運算子，例如性別、 過去的經驗。

它也可能通常 hello 案例，例如特殊的錯誤代碼或零件的訂單日期的 hello 表單中的維護歷程記錄中包含失敗的歷程記錄。 在這些情況下，可以從 hello 維護資料中擷取失敗。 此外，不同的商業領域可能有各種會影響故障模式的其他資料來源，這裡並未一一列出。 查閱 hello 網域專家，建置預測模型時，應該識別這些。

上述使用案例中的某些資料元素範例包括：

故障歷程記錄：航班延誤日期、飛機零組件故障日期和類型、ATM 現金提款交易失敗、列車/電梯門故障、煞車碟盤更換訂單日期、風力渦輪機故障日期和斷路器命令失敗。

維護歷程記錄：航班錯誤記錄檔、ATM 交易錯誤記錄檔、列車維護記錄 (包括維護類型、簡短描述等) 和斷路器維護記錄。

機器狀況和使用量：飛行路線和時間、從飛機引擎收集的感應器資料、ATM 交易的感應器讀數、列車事件資料、從風力渦輪機、電梯和連線汽車收集的感應器讀數。

機器特徵：斷路器技術規格 (例如電壓等級)、地理位置或汽車特徵 (例如廠牌、型號、引擎大小、輪胎類型、生產設備等)。

上述資料來源中的 hello，hello 預測性維護網域中我們觀察兩個主要的資料類型為暫存資料和靜態資料。
失敗記錄，機器條件修復記錄、 使用量記錄幾乎都提供時間戳記指出 hello 時間集合的每個資料片段。 機器的功能和運算子的功能一般是靜態的因為它們通常會描述 hello 技術規格的機器或運算子的屬性。 這些功能 toochange 可能會隨時間如果所以他們應該被視為加上時間戳記資料來源。

### <a name="merging-data-sources"></a>合併資料來源
任何類型的特徵設計或標籤的程序之前，我們需要 toofirst 準備我們 hello 必要表單 toocreate 功能中的資料。 hello 最終目標為的 toogenerate 送入 hello 機器學習演算法的每個資產，其功能和標籤 toobe 與每個時間單位的記錄。 在清除最終資料集的順序 tooprepare，應該採取一些前置處理的步驟。 第一個步驟是為每一筆記錄所屬 tooa 資產的時間單位的時間單位的資料收集 toodivide hello 持續時間。 也可以將資料收集分割成其他動作，例如單位，不過為了簡化使用時間單位 hello 說明 hello 其餘部分。

秒、 分鐘、 小時、 天、 月份、 循環、 英哩或根據 hello 效率的資料準備和其他或其他時間單位 toohello hello 資產 hello 條件中觀察到的 hello 變更的交易可以是時間的 hello 度量單位因素特定 toohello 網域。 換句話說，hello 時間單位沒有 toobe hello 與許多案例資料的資料收集頻率可能不會顯示任何差異的一個單位 toohello 其他如 hello 相同。 例如，如果溫度值已收集每隔 10 秒鐘，挑選 hello 整個分析時間為 10 秒的時間單位 「 充氣 」 hello 的一些範例不提供任何額外的資訊。 更好的策略是 toouse 平均一小時做為範例。

Hello 可能資料來源的範例一般資料結構描述所述 hello 是前一節：

維護記錄： 這些是 hello 記錄維護執行的動作。 hello 原始維護資料通常會隨附資產識別碼，而且已在該時間執行維護活動的相關資訊的時間戳記。 發生這類未經處理資料，維護活動需要 toobe 轉譯成類別資料行，與每個類別對應 tooa 維護動作類型。 維護記錄 hello 基本資料結構描述會包含資產識別碼、 時間和維護動作的資料行。

失敗記錄： 這些是屬於 toohello 預測目標的失敗或失敗的原因，我們稱為 hello 記錄。 這些可以是依特定商務狀況所定義的特定錯誤代碼或故障事件。 在某些情況下，資料會包括其中某些對應 toofailures 感興趣的多個錯誤代碼。 並非所有的錯誤是預測，因此通常是其他錯誤的目標使用 tooconstruct 功能可能會相互關聯，但失敗。 如果原因是可用，hello 失敗記錄的基本資料結構描述會包含資產識別碼、 時間和失敗或失敗原因的資料行。

電腦的條件： 這些是最好是即時監視 hello 作業系統條件的 hello 資料的相關資料。 比方說，門失敗開啟機門營業和打烊時間是有關 hello 門目前狀況的良好指標。 hello 機器條件的基本資料結構描述會包含資產識別碼、 時間和條件值的資料行。

電腦和運算子的資料： 電腦和運算子的資料可以合併到一個結構描述 tooidentify 資產由哪個運算子以及資產和運算子的屬性。 例如，汽車通常是由駕駛所擁有，其屬性包含年齡、駕駛經驗等。如果此資料會隨著時間改變，這項資料也應該包含時間資料行，並應視為不同的功能產生的資料的時間。 資產識別碼、 資產功能、 運算子識別碼和運算子的功能包括 hello 機器條件的基本資料結構描述。

hello 之前標籤及功能產生最後的資料表可以產生失敗記錄在資產識別碼和時間欄位上使用的機器條件資料表聯結的左方。 然後這個資料表會與資產識別碼和時間欄位上的維修記錄聯結，最後再與資產識別碼上的機器和操作者特徵聯結。 hello 的第一個左的聯結離開失敗的資料行的 null 值，當電腦是在正常作業中，這些可以正常運作的指標值所計算。 此失敗的資料行是使用的 toocreate hello 預測模型的標籤。

### <a name="feature-engineering"></a>特徵設計
在模型中的 hello 第一個步驟是功能工程團隊。 功能產生 hello 概念是 tooconceptually 描述，並在指定的時間，使用向上 toothat 點收集時間的歷程記錄資料抽象機器的健康情況。 Hello 下一節，我們提供的 hello 型別可以用於預測性維護和如何 hello 標記是為每個技術的技術的概觀。 hello 確切技術，應該使用取決於 hello 資料和商務問題。 不過，如下所述的 hello 特徵工程方法可以用於做為基準建立功能。 下面我們將討論應該建構資料來源的時間戳記以及靜態靜態的資料來源建立的功能，提供從 hello 範例使用案例的延隔時間功能。

#### <a name="lag-features"></a>延隔時間特徵
如先前所述，在預測性維護，歷程記錄資料通常會指出集合的每個資料片段 hello 時間之時間戳記。 有許多方法可從隨附加上資料的 hello 資料建立特徵。 在這一節中，我們會討論用於預測性維護的其中一些方法。 不過，我們不會只受限於這些方法。 由於特徵設計會視為預測模型的下列其中一個 hello 最創意區域 toobe，可能會有許多其他功能的方式 toocreate。 我們在此提供了某些一般技巧。

##### <a name="rolling-aggregates"></a>*滾動彙總*
資產的每一筆記錄，我們挑選大小"W"，這是我們想要對 toocompute 歷程記錄的彙總的時間單位的 hello 數目的循環視窗。 我們計算輪流使用 hello W 下降 hello 日期之前的該記錄的彙總功能。 滾動彙總的範例包括：滾動計數、平均值、標準差、以標準差為基礎的離群值、CUSUM 量值、時段的最小和最大值。 另一個有趣的技巧是 toocapture 趨勢的變更，如果看到爆增情形和層級變更使用中資料使用異常偵測演算法偵測異常行為的演算法。

如需示範，請參閱圖 1 我們用來代表每一單位的時間與記錄資產的感應器值 hello 藍線，並將標示 hello t 的滾動平均功能計算 W = 3 hello 記錄<sub>1</sub>和 t<sub>2</sub>這以橙色和綠色群組分別。

![圖 1. 滾動彙總特徵](media/cortana-analytics-playbook-predictive-maintenance/rolling-aggregate-features.png)

圖 1. 滾動彙總特徵

做為範例，飛機元件失敗，從上一週、 三天和最後一天的感應器值已使用的 toocreate 循環方式、 標準差和加總功能。 同樣地，ATM 故障時，則會使用原始感應器值和滾動平均值、中間值、值域、標準差、超過三個標準差的離群值數目、CUMSUM 上限和下限特徵。

航班誤點預測，從過去一週的錯誤碼的計數是使用的 toocreate 功能。 定型門失敗，hello hello 上的事件計數最後一天，次數的事件 hello 透過先前 2 週和變異數計數的 hello 事件前 15 天的已使用的 toocreate 延隔時間功能。 維護相關事件採用了相同的計算方式。

此外，透過挑選非常大的 W (例如， 年），很可能在 hello 整個歷程記錄的資產，例如計算所有維護 toolook 記錄，失敗等。 截至 hello hello 記錄時間。 這個方法用於計算 hello 的斷路器失敗過去三年。 也針對定型失敗，所有的維護事件已計算 toocreate 功能 toocapture hello 長期維護效果。

##### <a name="tumbling-aggregates"></a>*輪轉彙總*
每個標記為記錄的資產，我們挑選大小的視窗 「 W-<sub>k</sub>"其中 k 是 hello 數字或我們想要 toocreate 大小"W"的 windows 延隔的功能。 "k"可挑選為大型數字 toocapture 長期降低模式或小數值 toocapture 短期效果。 接著將利用 k 輪轉視窗 W-<sub>k</sub> ，W-<sub>(k-1)</sub>，...，W-<sub>2</sub> ，W-<sub>1</sub> toocreate hello hello 資料錄之前長一段時間的彙總功能（請參閱圖 2） 的日期和時間。 這些也 windows hello 記錄層級的輪流時間單位不會擷取它在圖 2 中，但 hello 概念是 hello 如圖 1 所示的相同位置 t<sub>2</sub>也使用的 toodemonstrate hello 正在作用。

![圖 2. 輪轉彙總特徵](media/cortana-analytics-playbook-predictive-maintenance/tumbling-aggregate-features.png)

圖 2. 輪轉彙總特徵

例如，wind 渦輪機、 W = 1 和 k = 3 個月 hello 的每個使用上方和下方的極端值的前 3 個月已使用的 toocreate 延隔時間功能。

#### <a name="static-features"></a>靜態特徵
這些是 hello 設備，例如製造日期、 型號、 位置等等的技術規格。大部分的本質數值延隔功能時，靜態功能通常會變成 hello 模型中的類別變數。 舉例來說，會使用斷路器屬性 (例如電壓、電流和電力規則以及變壓器類型、電源等)。 剎車組光碟失敗，hello tire 滾輪這類的類型，如同它們是合金或鋼做為部分 hello 靜態功能。

在特徵產生期間，應執行其他一些重要步驟，例如處理遺失值和正規化。 遺失值插補和資料正規化的方法都有很多種，此處將不會加以討論。 不過，如果可預測的效能提升是有幫助 tootry 不同的方法 toosee。

hello 最後在功能資料表功能工程 hello 所述的步驟之後前一節應該類似下列範例中的資料結構描述時的時間單位是一天的 hello:

| 資產識別碼 | 時間 | 特徵資料行 | 標籤 |
| --- | --- | --- | --- |
| 1 |第 1 天 | | |
| 1 |第 2 天 | | |
| ... |... | | |
| 2 |第 1 天 | | |
| 2 |第 2 天 | | |
| ... |... | | |

## <a name="modeling-techniques"></a>模型化技巧
預測性維護是 hello 的一個非常豐富的網域，通常採用可能接近從許多不同的角度的預測模型檢視方塊的商務問題。 在 hello 下一步 區段中，我們提供可預測性維護方案與回應的使用的 toomodel 不同的商務問題的主要技術。 雖有相似之處，但每個模型都有自己用來建構標籤 (後面詳加說明) 的方法。 為隨附的資源，您可以參考 toohello 預測性維護範本包含在 Azure Machine Learning 中所提供的 hello 範例實驗。 hello 資源 > 一節將提供此範本的 hello 連結 toohello 線上資料。 您可以查看如何套用一些 hello 功能工程上面所討論的技術和模型化技巧 hello 下一節中所述的 hello toopredict 飛機引擎使用 Azure Machine Learning 的失敗。

### <a name="binary-classification-for-predictive-maintenance"></a>預測性維護的二元分類
二元分類的預測性維護時，使用的 toopredict hello 在未來的時間內失敗的設備。 是取決於 hello 時間週期，並且根據商務規則和手邊 hello 資料。 某些共同的時間週期為最小的負責人所需時間 toopurchase 零件 tooreplace 可能 toodamage 元件或時間必要的 toodeploy 維護資源 tooperform 維護常式 toofix hello 問題的可能 toooccur 內，一段時間。 我們將這個未來水平期間稱為 "X"。

在訂單 toouse 二進位分類中，我們需要 tooidentify 兩種類型的範例，我們稱為正數和負數。 每個範例是屬於 tooa 資產在概念上說明，以及擷取其作業的條件向上 toothat 透過特徵設計使用稍早所述的歷程記錄和其他資料來源的時間單位的時間單位的記錄。 在 hello 內容中的二元分類的預測性維護，正值的型別表示失敗 （標籤 1） 和負的型別表示正常作業 (標籤 = 0) 的類別類型的標籤。 hello 目標是時間的 toofind 識別每個新的範例為可能 toofail 或正常運作，接下來 X 單位的 hello 內的模型。

#### <a name="label-construction"></a>標籤建構
順序 toocreate 預測模型 tooanswer hello 中提出問題是什麼 hello hello 接下來 X 的時間單位中的資產失敗的 hello 機率？ 」、 標記由函式 X 記錄先前 toohello 失敗，資產以及如 「 關於 toofail"加上標籤 (標籤 = 1)同時標示為 「 標準 」 的所有其他記錄 (標籤 = 0)。 在此方法中，標籤為類別變數 (請參閱圖 3)。

![圖 3. 二元分類的標記方式](media/cortana-analytics-playbook-predictive-maintenance/labelling-for-binary-classification.png)

圖 3. 二元分類的標記方式

飛行延遲和取消作業，X 可挑選為一天 hello toopredict 延遲 24 小時。 故障前 24 小時內的所有航班已都標記為 1。 ATM 現金分配失敗，兩個二元分類模型所建置的交易中 hello toopredict hello 失敗機率接下來的 10 分鐘而失敗 toopredict hello 機率也 hello 100 備忘稿分配。 發生在 hello hello 失敗的過去 10 分鐘內的所有交易都標示為 1 hello 第一個模型。 和所有的便箋內 hello 分配最後一個失敗的 100 備忘稿已標示為 1 hello 第二個模型。 斷路器失敗 hello 工作是 hello 下一個斷路器命令的 toopredict hello 機率失敗 X 會在此情況下選擇 toobe 一個未來的命令。 定型門失敗，hello 二元分類模型，建立 hello 的 toopredict 失敗未來 7 天。 對於風力渦輪機故障，已選擇 3 個月做為 X。

Wind 渦輪機及定型門的情況下也會使用針對迴歸分析 toopredict 剩餘有用的生命週期使用 hello 相同的資料，但藉由使用不同的標籤策略 hello 下一節中會有說明。

### <a name="regression-for-predictive-maintenance"></a>預測性維護的迴歸
迴歸模型中預測性維護定義為 hello 下一個失敗發生之前，hello hello 資產量是時間的操作資產是時間的使用的 toocompute 剩餘有用的生命週期 (RUL)。 與相同，二元分類，每個範例是記錄所屬的資產 tooa 時間單位"Y"。 不過，在 hello 內容中的迴歸，hello 目標是範例的 toofind 計算 hello 剩餘有用的生命週期的每個新與 hello hello 失敗前的剩餘時間段是範例的連續數字的模型。 我們將這段期間 Y 的某些倍數。每個範例中也有其他有用的生命週期的計算方式是測量 hello 對於該範例 hello 下一步失敗前的剩餘的時間量。

#### <a name="label-construction"></a>標籤建構
指定 「 什麼是 hello 剩餘有用生命週期 hello 設備 hello 問題？
"，可以建構 hello 迴歸模型，每一項記錄先前 toohello 失敗，以及藉由計算多少時間單位保持 hello 下一步失敗前加上標籤的標籤。 在此方法中，標籤為連續變數 (請參閱圖 4)。

![圖 4. 迴歸的標記方式](media/cortana-analytics-playbook-predictive-maintenance/labelling-for-regression.png)

圖 4. 迴歸的標記方式

不同於二元分類，迴歸，無任何錯誤 hello 資料中的資產無法用於模型化標籤是在參考 tooa 失敗點，且其計算也不可能不需要知道多久 hello 資產之前未被失敗。 這個問題可由另一個稱為「存活分析」的統計技巧來得到最妥善的解決。
我們不會因為 hello 潛在的錯亂套用 hello 技術 toopredictive 維護時可能會發生這個腳本中 toodiscuss 求生分析使用案例牽涉到頻繁的間隔與時間變化的資料。

### <a name="multi-class-classification-for-predictive-maintenance"></a>預測性維護的多類別分類
預測性維護的多類別分類可用來預測兩種未來結果。 hello 第一次是 tooassign hello 的資產 tooone 時間 toogive 的每個資產的時間 toofailure 範圍的多個可能的週期。 hello 第二個是在未來的週期期限失敗 tooidentify hello 可能性 tooone hello 的多個根本原因。 可讓維護人員，以預先處理 hello 問題配備這項知識。 另一個多類別模型化技巧著重於判斷 hello 最有可能根本原因提供失敗。 這可讓建議 toobe 給 hello 前的維護動作 toobe 採取順序 toofix 中失敗。
由於具備根原因的排名清單及其相關聯的修復動作，  
技術人員可以更有效率地在失敗之後採取其第一個修復動作。

#### <a name="label-construction"></a>標籤建構
指定 hello 兩個問題，也就是 「 hello 機率資產失敗的 hello 下一步"aZ"時間單位是什麼其中"a"是 hello 期數"和"何謂 hello 資產的 hello 機率在接下來 X 的時間單位的 hello 失敗到期 tooproblem"P<sub>我</sub>"其中"i"可能的根本原因，標示的 hello 數目會進行下列方法，讓這些 tootechniques hello。

Hello 第一個問題，標籤動作的方式是取得 aZ 資產的 hello 失敗之前的記錄，並加上標籤時標記為 「 標準 」 的所有其他記錄，使用值區的時間 （3Z、 2Z，Z） 為其標籤 (標籤 = 0)。 在此方法中，標籤為類別變數 (請參閱圖 5)。

![圖 5. 故障時間預測的多類別分類標記方式](media/cortana-analytics-playbook-predictive-maintenance/labelling-for-multiclass-classification-for-failure-time-prediction.png)

圖 5. 故障時間預測的多類別分類標記方式

Hello 第二個問題，標籤由 hello 資產和標籤它們做為失敗之前的函式 X 記錄 」 相關問題造成 P toofail<sub>我</sub>"(標籤 = P<sub>我</sub>) 同時標示為所有其他的記錄 」標準 」 (標籤 = 0)。 在此方法中，標籤為類別變數 (請參閱圖 6)。

![圖 6. 根本原因預測的多類別分類標記方式](media/cortana-analytics-playbook-predictive-maintenance/labelling-for-multiclass-classification-for-root-cause-prediction.png)

圖 6. 根本原因預測的多類別分類標記方式

hello 模型指派的失敗機率到期 tooeach P<sub>我</sub>以及 hello 的任何失敗的機率。 這些機率可以依照 hello 問題，則最有可能在未來的 hello toooccur 的量級 tooallow 預測來排序。 飛機零組件故障使用案例已結構化為多類別分類問題。 這可讓 hello 的失敗，因為 tootwo 不同壓力閥元件 hello 中發生的下個月的 hello 機率的預測。

針對在失敗之後，建議以維護動作，標記不需要挑選未來的水平 toobe。 這是因為 hello 模型不預測未來的 hello 失敗，但一旦 hello 失敗已經發生，它只預測 hello 最可能的根本原因。 電梯門失敗歸類到 hello 目標是 toopredict hello 第三個案例指定作業系統條件的歷程記錄資料的 hello 失敗的原因。 接著會使用這個模型 toopredict hello 最有可能根本原因之後發生失敗。 此模型的一個主要優點是經驗的它有助於熟悉的技術人員 tooeasily 診斷與修正問題，否則需要年的價值。

## <a name="training-validation-and-testing-methods-in-predictive-maintenance"></a>預測性維護中的訓練、驗證及測試方法
預測性維護，類似 tooany 中包含的資料加上其他方案空間，hello 一般定型和測試不同的層面 toobetter 常式需求 tootake 帳戶 hello 時間一般化上看不見未來的資料。

### <a name="cross-validation"></a>交叉驗證
許多機器學習演算法相依於可大幅改變模型效能的超參數數目。 hello 最佳的這些超參數的值不時自動計算培訓 hello 模型，但應該資料科學家所指定。 尋找良好超參數值的方法有好幾種。 hello 最常見的原因是"k 摺疊交叉驗證 」 可將 hello 範例隨機分割成"k"摺疊。 對於每組超參數值，學習演算法會執行 k 次。 在每個反覆項目，驗證設定為使用 hello 目前折疊中的 hello 範例，hello 範例 hello 其餘部分會做為定型集。 hello 演算法定型透過定型範例，並透過驗證範例計算 hello 效能度量。 在 hello 這個迴圈每一組 hyperparameter 值的結尾，我們會計算 hello k 效能度量值的平均值，然後選擇具有 hello 最佳的平均效能的 hyperparameter 值。

如先前所述，在預測性維護問題中，會將資料記錄成來自數個資料來源之事件的時間序列。 這些記錄可以根據標示記錄或範例的 toohello 時間來排序。 因此，如果我們分割 hello 資料集隨機成定型和驗證設定，某些 hello 定型範例是晚的時間部分驗證的範例。 這會導致預估未來的 hyperparameter 值根據 hello 資料到達之前來定型模型的效能。 這些估計可能過於樂觀，尤其是在時間序列不固定並隨著時間改變其行為的時候。 因此，所選的超參數值可能不是最理想的。

尋找良好的超參數值的更好的方式，toosplit hello 範例成定型和驗證設定與時間相關的方式，這類所有驗證範例都包括所有的定型範例比稍後的時間。 然後，針對每個值的超集我們訓練 hello 演算法，透過定型集，透過相同的驗證設定，然後選擇 顯示 hello 達到最佳效能的 hyperparameter 值 hello 測量模型的效能。 當時間序列資料不固定，而且經過一段時間的發展時，hello hyperparameter 值選擇的訓練/驗證分割負責人 tooa 更好的未來"模型的效能比使用交叉驗證會隨機選擇的 hello 值。

hello 最終模型會使用 hello 最佳 hyperparameter 找到的值會使用訓練/驗證分割 」 或 「 交叉驗證的整個資料上定型的學習演算法來產生。

### <a name="testing-for-model-performance"></a>測試模型效能
建立模型之後我們需要 tooestimate 未來效能上新的資料。 hello 簡單估計 hello 模型的 hello 效能會比 hello 定型資料。 但是，這項預估是過於樂觀的因為模型是使用的 tooestimate 效能量身訂做的 toohello 資料。 效能標準的 hyperparameter 值計算出 hello 驗證集或從交叉驗證計算平均效能度量，可能是較佳估計值。 但 hello 相同的理由，如前所述，這些估計仍過於樂觀。 我們需要更實際的方法來測量模型效能。

其中一個方法是 toosplit hello 資料隨機定型、 驗證和測試集。 hello 定型和驗證設定會使用的 tooselect 超及定型 hello 模型與其值。 hello 效能模型被以 hello 測試資料集。

這是相關 toopredictive 維護，toosplit 另一種方式為定型，驗證和測試集時間相依的方式，使所有測試範例的範例是晚的時間所有定型和驗證的範例。 Hello 分割之後，完成模型的產生和效能度量 hello 稍早所述相同。

當時間序列不動簡便 toopredict 這兩種方法會產生類似估計的未來的效能。 但是，非固定和/或硬 toopredict 時間序列時，hello 第二種方法會產生更逼真預估的未來的效能比 hello 第一個。

### <a name="time-dependent-split"></a>時間相依分割
最好的作法是，我們會在這一節中深入探討如何實作時間相依分割。 我們將描述定型和測試集，不過完全 hello 相同邏輯應該套用時間相依分割為定型和驗證設定之間的時間相依雙向分割。

假設我們有一連串的時間戳記事件，例如來自各種感應器的測量資料。 系統會針對包含多個事件的時間範圍，定義訓練和測試範例的特徵以及其標籤。
例如，二進位分類，功能工程和模型化技巧章節中所述功能會根據建立 hello 過去事件和標籤會根據建立未來事件內"X"hello 中的時間單位未來。 因此，標記範例的時間範圍的 hello 急然後 hello 其功能的時間範圍。 對於時間相依分岔，我們選取的時間點的定型的模型與微調超使用 toothat 點歷程記錄資料的時間。 未來超出 hello 訓練截止到定型資料的標籤 tooprevent 外洩，我們選擇最新的時間範圍內 toolabel hello 訓練範例 toobe X 單位 hello 訓練截止日期之前。 圖 7 穩固的每個圓圈表示 hello 最終功能的資料集的 hello 功能和標籤都計算根據上面所述的 toothe 方法中的資料列。 因此，hello 圖會顯示 hello 記錄應該移入定型和測試集實作時間相依分割 X = 2，W = 3 時：

![圖 7. 二元分類的時間相依分割](media/cortana-analytics-playbook-predictive-maintenance/time-dependent-split-for-binary-classification.png)

圖 7. 二元分類的時間相依分割

hello 綠色方塊表示 hello 記錄會用於定型的 toohello 時間單位。 藉由查看稍早所述的每個訓練範例 hello 最終會產生功能資料表超過 3 的功能產生和 2 未來的期間，用於標示定型天截止之前的期間。 我們不會將 hello 定型集時 hello 的任何部分對於該範例 2 未來的期超出 hello 訓練截止由於我們假設，我們不需要超過定型截止的可見性的範例。 由於 toothat 條件約束，黑色的範例代表 hello 的 hello 最終標示為不應用於 hello 定型資料集的資料集的記錄。 這些記錄不會用於測試的資料是因為它們是之前 hello 訓練截止，而其標籤的時間範圍部分取決於 hello 定型時間範圍內應該不是 hello 案例，我們都希望 toocompletely 分隔標記的時間範圍定型集和測試 tooprevent 標籤資訊外洩。

這項技術可讓您用來定型與測試範例，會關閉 toothe 訓練截止之間的功能產生的 hello 資料重疊。 根據資料的可用性，而更嚴重的區隔可以達成不使用任何 hello 中的範例測試集內的 hello 訓練截止 W 時間單位。

從工作中，我們發現 hello 外洩問題更造成嚴重影響用來預測剩餘有用的生命週期的迴歸模型，並使用隨機分割會導致 tooextreme 過度配適。 同樣地，在迴歸問題，hello 分割應該屬於資產，但定型切斷之前失敗的記錄應該使用定型集和 hello 截止應該用於測試集之後發生失敗的資產。

做為一般的方法，另一個重要的最佳作法，將用於定型和測試資料分割，toouse 資產識別碼分割沒有任何定型中所使用的 hello 資產用於測試因為測試的概念是確定 toomake，使用新的資產時 toomake 預測，hello 模型會提供實際的結果。

### <a name="handling-imbalanced-data"></a>處理不平衡的資料
分類的問題，如果有多個範例的 hello 一級比其他資料的 hello 說 toobe 不平衡。 在理想情況下，我們都希望 toohave 不足，無法代表 hello 定型資料 toobe 無法 toodifferentiate 不同類別間中的每個類別。 如果一個類別是低於 10%的 hello 資料，我們可以說出 hello 資料不平衡，而且我們呼叫 hello 低於適當比例資料集中少數類別。 有很大，在許多情況下我們找到平衡資料集其中一個類別是嚴重 underrepresented 比較的 tooothers 例如由只從屬 0.001%的 hello 資料點。 類別不平衡是在多網域包括詐騙偵測 」、 「 網路入侵 」 和 「 預測性維護失敗，是很少見的項目在 hello 存留期的 hello 資產組成 hello 少數類別範例的問題。

如果類別不平衡，大部分的標準學習演算法的效能受到因為它們是用 toominimize hello 整體錯誤率。 例如，在具有 99% 否定類別範例和 1% 肯定類別範例的資料集中，我們只需將所有執行個體標記為否定，即可取得 99% 的精確度。 不過，這利用所有正數的範例，因此 hello 演算法並不適合雖然 hello 精確度度量是非常高。 因此，傳統評估計量資訊 (例如錯誤率的整體精確度) 還不足以進行不平衡的學習。 其他度量，例如有效位數、 選出、 F1 分數和調整的 ROC 曲線用於評估 hello 評估度量 > 一節中有討論平衡資料集時的成本。

不過，有一些方法可協助矯正類別不平衡問題。 hello 兩個主要的取樣技術和成本機密學習。

#### <a name="sampling-methods"></a>取樣方法
hello 使用取樣方法不平衡的了解組成修改 hello 資料集的順序 tooprovide 中一些機制平衡資料集。 雖然有許多不同的取樣技巧，但最直接的取樣方法是隨機超取樣和低取樣。

只要指定、 隨機超取樣少數類別，複寫這些範例並將它們加入 tootraining 資料集從選取隨機取樣。 這會增加 hello 總計中的範例數目少數類別，並最終平衡 hello 數目不同類別的範例。 一個危險的超取樣是多個執行個體的特定範例，可能會導致 hello 分類 toobecome 太特定前置 toooverfitting。
這會導致高訓練精確度，但看不見的測試資料的效能可能很差。 相反地，隨機低取樣就是從多數類別中選取一個隨機樣本，並從訓練資料集中移除這些範例。 不過，移除少數類別範例可能會導致 hello 分類 toomiss 重要的概念有關 toohello 少數類別。 其中少數類別 oversampled 和少數類別底下進行取樣的混合式取樣 hello 同時在另一個可行的方法。 其他還有許多更複雜的取樣技巧可使用，而適用於類別不平衡的有效取樣方法是很熱門的研究領域，經常受到各方的注意和貢獻。 使用不同的技術來決定的 hello 最有效的是通常是左的 toohello 資料科學家 tooresearch 並試驗和大多取決 hello 資料屬性。 此外，務必確定取樣方法是套用只有 toohello 訓練 toomake 設定，但不是 hello 測試集。

#### <a name="cost-sensitive-learning"></a>成本導向學習
在預測性維護，構成 hello 少數類別失敗感興趣的多個比一般的範例，因此 hello 焦點在效能上的 hello 演算法的失敗通常是 hello 焦點。 這通常稱為將不同類別的元素歸類錯誤的不平等損失或不對稱成本，其中將肯定錯誤地預測為否定的成本比將否定錯誤地預測為肯定的成本還要高。 hello 所需的分類器應該會無法 toogive 高的預測精確度 hello 少數類別，而不會造成嚴重危害 hello 少數類別的 hello 精確度。

有數種方法能夠達成此目的。 所指派的 hello 少數的錯誤分類成本最高類別，而嘗試 toominimize 失去的整體成本不等於 hello 問題可以有效地處理。 有些機器學習演算法原本就會使用此概念，例如 SVM(支援向量機器)，其在訓練期間可以合併肯定和否定範例的成本。 同樣地，使用提升 (Boosting) 方法通常會在資料不平衡的情況中顯示良好的效能，例如促進式決策樹演算法。

## <a name="evaluation-metrics"></a>評估計量
如先前所述，類別不平衡會導致效能不佳，因為演算法通常 tooclassify 更好的少數類別案例的費用為 hello 總錯誤分類錯誤更改進時正確地標示為少數類別的大部分類別範例。 這會導致低重新叫用比率，false 警示 toohello 商務 hello 成本很高時，會變成較大的問題。 精確度是 hello 最受歡迎的標準，用來描述分類器的效能。 精確度無效以上所述但並不會反映 hello 的分類器功能的實際效能，所以非常敏感 toodata 分佈。 相反地，其他的評估度量資訊是使用的 tooassess 平衡學習問題。 在這些情況下，有效位數、 選出和 F1 分數應該會在 hello 初始度量 toolook 評估預測性維護模型效能時。 在預測性維護，重新叫用比率表示多少 hello hello 測試集合中的失敗已正確識別 hello 模型。 較高的重新叫用比率表示成功攔截 hello true 失敗 hello 模型。 Hello 率較低的有效位數速率其中對應至較高的錯誤警示的錯誤警示與相關精確度度量。 F1 分數認為精確度和召回率的最佳值是 1，最差值是 0。

此外，在二元分類中，評估效能時，十分位數資料表和增益圖都非常有幫助。 它們只著重於正類別 （失敗），且提供的演算法效能比查看剛才固定的作業點 hello （接收器操作特徵） ROC 曲線上看到更複雜的圖片。
Decile 資料表所取得排序 hello 測試範例根據失敗之前 hello 最後一個標籤上的閾值 toodecide hello 模型所計算的及其預測機率。 hello 排序範例都十分位數 （亦即 hello 10%範例與最大機率，然後 20%、 30%等） 中分組。 其中一個可以藉由計算的每個 decile true 正數速率與隨機基準 （也就是 0.1、 0.2 …） 之間的 hello 比率估計 hello 演算法效能如何在每個 decile 變更。 增益圖會使用的 tooplot decile 值繪製 decile true 正數的速率與所有十分位數的隨機，則為 true 的正數速率組。 通常，hello 第一個十分位數是 hello 焦點的 hello 結果，因為我們在這裡看到的最大的提升。 此外，第一個十分位數使用於預測性維護時，也可被視為「有風險」的代表性資料。

## <a name="sample-solution-architecture"></a>範例解決方案架構
部署預測性維護方案時，我們有興趣提供連續循環的擷取資料、 將資料儲存為模型定型、 產生功能、 預測和視覺效果的 hello 結果連同端點 tooend 解決方案機制，例如監視儀表板的資產會產生警示。 我們想要以連續自動化方式提供未來 insights toohello 使用者在資料管線。 下面圖 8 說明這類 IoT 資料管線的範例預測性維護架構。 在此架構中，即時遙測資料會收集到可儲存串流資料的事件中樞。 此資料會經由串流分析擷取，以便進行即時資料處理，例如產生特徵。 hello 功能則會使用 toocall hello 預測模型的 web 服務和結果會顯示 hello 儀表板上。 在 hello 相同時間、 內嵌的資料也儲存在歷程記錄的資料庫，並合併與外部資料來源，例如在內部部署資料基底 toocreate 定型範例的模型。
相同的資料倉儲可以用於批次計分的 hello 範例與 hello 結果可再次使用的 tooprovide 預測報表 hello 儀表板上的儲存。

![圖 8. 預測性維護的範例解決方案架構](media/cortana-analytics-playbook-predictive-maintenance/example-solution-architecture-for-predictive-maintenance.png)

圖 8. 預測性維護的範例解決方案架構

如需有關每個 hello 元件的 hello 架構，請參閱太[Azure](https://azure.microsoft.com/)文件。

