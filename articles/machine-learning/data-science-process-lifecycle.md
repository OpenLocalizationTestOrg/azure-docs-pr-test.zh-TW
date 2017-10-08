---
title: "aaaAzure 小組資料科學程序生命週期 |Microsoft 文件"
description: "所需的步驟 tooexecute 資料科學專案。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b1f677bb-eef5-4acb-9b3b-8a5819fb0e78
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev;
ms.openlocfilehash: 58114a1c2d3289d1c4b2781219d0bf9647dbccd1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="team-data-science-process-lifecycle"></a>Team Data Science Process 生命週期

hello 小組資料科學程序 (TDSP) 提供建議的生命週期，您可以使用 toostructure 資料科學專案。 hello 生命週期概述 hello 步驟，從開始 toofinish 專案通常會遵循在執行時。 如果您使用另一個資料科學生命週期，例如[CRISP-DM](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining)， [KDD](https://wikipedia.org/wiki/Data_mining#Process)或您組織本身的自訂程序，您仍然可以使用 hello 以工作為基礎的 TDSP 與這些開發週期。 

已針對資料科學專案一部分的智慧型應用程式所預期的 tooship 設計這個生命週期。 這些應用程式會部署機器學習服務或人工智慧模型來做預測性分析。 探勘資料科學專案和臨機操作分析專案也可以從使用此程序而獲益。 但是，在這種情況下，可能不需要所述的某些步驟。    

以下是 hello 的視覺表示法**小組資料科學程序生命週期**。 

![TDSP-Lifecycle](./media/data-science-process-overview/tdsp-lifecycle.png) 

hello TDSP 生命週期是反覆執行的五個主要階段所組成。 其中包含：

* **了解商務**
* **資料取得與認知**
* **模型化**
* **部署**
* **客戶接受度**

每個階段中，我們提供下列資訊的 hello:

* **目標**: hello 的特定目標。
* **如何 toodo 它**: hello 所述的特定工作和提供完成這些指導方針。
* **成品**: hello 交付項目和 hello 支援，以便產生它們。


## <a name="1-business-understanding"></a>1.了解商務

### <a name="goals"></a>目標
* hello**金鑰變數**tooserve hello 與所指定**模型目標**，並用其相關的度量決定 hello 專案 hello 成功。
* hello 相關**資料來源**hello 公司都有存取 tooor 需求 tooobtain 識別。

### <a name="how-toodo-it"></a>如何 toodo 它
此階段會解決兩項主要工作︰ 

* **定義目標**： 使用您的客戶和其他專案關係人 toounderstand 並找出 hello 的商務問題。 制訂定義 hello 業務目標和資料科學技術可鎖定目標的問題。
* **識別資料來源**： 尋找 hello 相關資料，可協助您回答 hello 定義 hello hello 專案目標。

#### <a name="11-define-objectives"></a>1.1 定義目標

1. 此步驟中的中央目標是 tooidentify hello 金鑰**商務變數**hello 分析需要 toopredict。 這些變數會參照的 tooas hello**模型目標**和與其相關聯的 hello 度量資訊是使用的 toodetermine hello 專案成功的 hello。 被詐騙的銷售預測或 hello 機率是訂單的兩個例子這類目標。

2. 定義 hello**專案目標**要求並精簡"尖銳"問題相關和特定模稜兩可。 資料科學是 hello 程序使用的名稱，與數字 tooanswer 這類問題。 詢問尖問題的詳細資訊，請參閱[如何 toodo 資料科學](https://blogs.technet.microsoft.com/machinelearning/2016/03/28/how-to-do-data-science/)部落格。 資料科學 / 機器學習服務是常用的 tooanswer 五種類型的問題：
 
   * 有多少？ (迴歸)
   * 什麼類別？ (分類)
   * 哪個群組？ (叢集)
   * 這很奇怪嗎？ (異常偵測)
   * 應採用哪個選項？ (建議)

    決定這些問題中要詢問哪些，以及如何解答以達到商務目標。

3. 定義 hello**專案小組**藉由指定 hello 角色和其成員的責任。 在發現更多資訊時，開發可逐一查看的高階里程碑計劃。  

4. **定義成功標準**。 例如： hello 結尾這 3 個月的專案，以達到客戶變換預測精確度的 0x %，讓我們可以提供促銷 tooreduce 變換。 必須是 hello 度量**智慧**: 
   * **S**pecific (具體) 
   * **M**easurable (可測量)
   * **A**chievable (可達成) 
   * **R**elevant (具有相關性) 
   * **T**ime-bound (有時限) 

#### <a name="12-identify-data-sources"></a>1.2 識別資料來源
識別包含已知的答案 tooyour 尖問題範例的資料來源。 尋找 hello 下列資料：

* 資料**相關**toohello 問題。 我們有 hello 目標和功能的相關的 toohello 目標量的值嗎？
* 資料**精確的量值**的感興趣的模型目標和 hello 功能。

是很常見的例如，現有的系統需要 toocollect 及記錄其他種類的資料 tooaddress toofind hello 問題達成 hello 專案目標。 在此情況下，您可能想要在 toolook 外部資料來源或更新您的系統 toocollect 新資料。

### <a name="artifacts"></a>構件
以下是此階段中的 hello 交付項目：

* [**文件教授**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Project/Charter.md): hello TDSP 專案結構定義中提供標準的範本。 這是進行新的探索和商務需求變更時，會將整個 hello 專案更新即時文件。 在本文件中，加入更多詳細資料，當您逐步 hello 探索程序時 tooiterate hello 金鑰。 保留 hello 客戶和其他專案關係人參與 hello 變更，並清楚地傳達 hello 變更 toothem hello 原因。  
* [**資料來源**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/Data%20Defintion.md#raw-data-sources)： 這是 hello**未經處理的資料來源**區段 hello**資料定義**位於 hello TDSP 專案的報表**資料報表**資料夾。 它會指定 hello 原始和 hello 未經處理資料的目的地位置。 在稍後階段，您填入類似指令碼 toomove hello 資料 tooyour 分析環境的其他詳細資料。  
* [**資料字典**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/tree/master/Docs/DataDictionaries)： 本文件提供 hello 資料 hello 用戶端所提供的描述。 這些說明包括 hello 結構描述 （資料類型，有關驗證規則，如果有的話） 的相關資訊，以及 hello 實體關聯性圖表，如果有的話。


## <a name="2-data-acquisition-and-understanding"></a>2.資料取得與認知

### <a name="goals"></a>目標
* 全新的高品質的資料集可了解其關聯 toohello 目標變數位於 hello 適當分析環境中，準備好 toomodel。
* 解決方案架構的 hello 資料管線 toorefresh 和分數資料定期已經開發了。

### <a name="how-toodo-it"></a>如何 toodo 它
此階段會解決三項主要工作︰

* **內嵌 hello 資料**hello 目標分析環境。
* **瀏覽 hello 資料**toodetermine hello 資料品質是否足夠 tooanswer hello 問題。 
* **設定在資料管線**tooscore new 或定期重新整理資料。

#### <a name="21-ingest-hello-data"></a>2.1 內嵌 hello 資料
設定 hello 處理 toomove hello 資料從來源位置等分析作業的定型和預測所執行的 toobe toohello 目標位置。 技術詳細資料和選項如何 toodo 這有各種 Azure 資料服務，請參閱[資料載入至儲存體環境以供分析](machine-learning-data-science-ingest-data.md)。 

#### <a name="22-explore-hello-data"></a>2.2 瀏覽 hello 資料
定型模型之前，您會需要 toodevelop hello 資料徹底了解。 真實的資料集通常會有雜訊、遺漏值或具有許多不一致之處。 資料摘要和視覺效果可使用的 tooaudit hello 品質的資料，並提供 hello 資訊所需 tooprocess hello 資料之前準備用於模型化。 此程序通常會反覆進行。

TDSP 提供自動化的公用程式，稱為[IDEAR](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/DataReport-Utils) toohelp hello 資料視覺化，並準備資料的摘要報表。 我們建議您從 IDEAR 第一個 tooexplore hello 資料 toohelp 開發初始資料的了解，以互動方式與任何程式碼，然後撰寫自訂程式碼進行資料探索和視覺效果。 如需清潔 hello 資料的指引，請參閱[任務 tooprepare 資料增強的機器學習](machine-learning-data-science-prepare-data.md)。  

一旦您滿意 hello hello 清理資料品質，hello 下一個步驟是 toobetter 了解 hello 模式固有 hello 資料可協助您選擇和開發適當的預測模型，為您的目標。 尋找證據程度連接的 hello 資料是 toohello 目標以及是否有足夠資料 toomove 向前與 hello 模型下一步。 同樣地，此程序通常會反覆進行。 您可能需要 toofind 新的資料來源與更精確或更多相關資料 tooaugment hello 集最初 hello 上一個階段中識別。  

#### <a name="23-set-up-a-data-pipeline"></a>2.3 設定資料管線
此外 toohello 初始擷取和清除的 hello 資料，您通常需要 tooset 處理 tooscore 新資料或重新整理 hello 資料定期持續學習程序的一部分。 這可以透過設定資料管線或工作流程來完成。 以下是[範例](machine-learning-data-science-move-sql-azure-adf.md)方式的總具有管線 tooset [Azure Data Factory](https://azure.microsoft.com/services/data-factory/)。 

在這個階段中，被開發 hello 資料管線中的方案架構。 以 hello 遵循 hello 資料科學專案階段同時也被開發 hello 管線。 hello 管線可能批次式或資料流/即時-單次或混合式根據您的業務需要和 hello 這個解決方案整合到您現有系統的條件約束。 

### <a name="artifacts"></a>構件
hello 以下是此階段中的 hello 交付項目。

* [**資料品質報表**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/DataSummaryReport.md)： 這份報表包含資料摘要中，每個屬性和目標、 排名等 hello 變數之間的關聯性[IDEAR](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/DataReport-Utils)當成可快速產生 TDSP 一部分提供的工具此報表上的 CSV 檔案或關聯式資料表等任何表格式資料集。 
* **解決方案架構**： 這一旦您已建立的模型可以是圖表或您的資料使用管線 toorun 計分或預測新資料的描述。 它也包含 hello 管線 tooretrain 您的模型根據新資料。 hello 文件會儲存在 hello[專案](https://github.com/Azure/Azure-TDSP-ProjectTemplate/tree/master/Docs/Project)目錄時使用 hello TDSP 目錄結構的範本。
* **檢查點決策**： 完整特徵設計和模型建置開始之前，您可以重新評估 hello 專案 toodetermine 預期的 hello 值是否足夠 toocontinue 追求它。 例如，您可能會準備 tooproceed，需要 toocollect 更多資料，或因為 hello 資料不存在 tooanswer hello 問題放棄 hello 專案。


## <a name="3-modeling"></a>3.模型化

### <a name="goals"></a>目標
* Hello 機器學習模型的最佳資料功能。
* 具有資訊價值 ML 模型，以最精確地預測 hello 目標。
* 適用於生產環境的 ML 模型。

### <a name="how-toodo-it"></a>如何 toodo 它
此階段會解決三項主要工作︰

* **功能工程**: hello 未經處理資料 toofacilitate 模型定型中建立資料的功能。
* **模型定型**： 找出 hello 模型該答案 hello 問題最能精確藉由比較其成功度量。
* 判斷您的模型是否**適用於生產環境**。

#### <a name="31-feature-engineering"></a>3.1 功能設計
特徵設計牽涉到包含、 彙總和轉換的原始變數 toocreate hello hello 分析中使用的功能。 如果您想深入了解什麼驅動的模型，然後您需要 toounderstand 功能有其他相關的 tooeach 和 hello 機器學習演算法時，toouse 如何這些功能。 此步驟需要創意網域專業知識和 insights 取自 hello 資料瀏覽步驟的組合。 這可平衡參考變數的尋找及納入，同時避免有太多不相關的變數。 具有資訊價值變數改善我們的結果。不相關的變數中導入 hello 模型不必要的干擾。 您也需要 toogenerate 這些功能的計分期間取得的任何新資料。 因此 hello 層代，這些功能可能只會相依於目前使用 hello 計分的資料。 如需技術指引特徵設計使用各種不同的 Azure 資料技術時的詳細資訊，請參閱[功能 hello 資料科學程序中的工程](machine-learning-data-science-create-features.md)。 

#### <a name="32-model-training"></a>3.2 模型訓練
根據您嘗試回答的問題類型，會有許多可用的模型化演算法。 如需有關選擇 hello 演算法的指引，請參閱[如何 toochoose 演算法為 Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md)。 雖然這篇文章針對 Azure 機器學習所撰寫，hello 它提供可用於任何機器學習服務專案的指引。 

hello 模型定型程序包含下列步驟的 hello: 

* **資料分割 hello 輸入**隨機的定型資料集和測試資料集的模型。
* **建立 hello 模型**使用 hello 定型資料集。
* **評估**（定型和測試資料集） 一系列的競爭的機器學習演算法以及 hello 各種相關聯微調參數 （稱為參數掃掠） 專為回答 hello 以 hello 感興趣的問題。目前的資料。
* **決定 hello 「 最佳 」 解決方案**tooanswer hello 問題，藉由比較 hello 成功度量之間的替代方法。

> [!NOTE]
> **避免洩漏的情況**： 從外部 hello 定型資料集，可讓模型或機器學習演算法 toomake 洩密良好預測 hello 內含的資料可能造成資料外洩。 外洩是資料科學家為什麼收到外人取得看起來太好 toobe 的預測結果，則為 true 時的常見原因。 這些相依性可以是永久 toodetect。 tooavoid 外洩通常需要逐一查看之間建立分析資料集、 建立模型，以及評估 hello 精確度。 
> 
> 

我們提供[自動化模型和報告工具](https://github.com/Azure/Azure-TDSP-Utilities/blob/master/DataScienceUtilities/Modeling)TDSP，為可以 toorun 透過多個演算法，而參數掃掠 tooproduce 基準模型。 它也會產生基準模型報告，摘要說明每個模型和參數組合的效能 (包括變數重要性)。 此程序也會反覆進行，因為這可促成進一步的功能設計。 

### <a name="artifacts"></a>構件
在這個階段中產生的 hello 成品包括：

* [**功能集**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/DataReport/Data%20Defintion.md#feature-sets): hello 模型化開發的 hello 功能詳述於 hello**功能集**區段 hello**資料定義**報表。 它包含指標 toohello 程式碼 toogenerate hello 功能和有關如何產生 hello 功能說明。
* [**模型報表**](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Model/Model%201/Model%20Report.md)：每個嘗試過的模型，都會產生標準的範本型報表，提供每項實驗的詳細資料。
* **檢查點決策**： 評估是否 hello 模型執行也足夠 toodeploy 它 tooa 生產系統。 某些重要的問題 tooask 如下：
  * 有足夠的信心地 hello 模型回應 hello 問題是否指定 hello 測試資料？ 
  * 應該嘗試任何替代方法︰收集其他資料、進行更多功能設計，或試驗其他演算法？


## <a name="4-deployment"></a>4.部署

### <a name="goal"></a>目標
* 在資料管線中使用的模型是已部署的 tooa 生產或最後一個使用者接受度的類似實際執行環境。 

### <a name="how-toodo-it"></a>如何 toodo 它
在這個階段中處理 hello 的主要工作：

* **實施 hello 模型**: hello 模型和管線 tooa 生產環境或應用程式耗用的類似實際執行環境部署。

#### <a name="41-operationalize-a-model"></a>4.1 實作模型
一組執行的模型之後，它們可以用於其他應用程式 tooconsume operationalized 它。 根據 hello 的商務需求，即時或批次為基礎進行預測。 實際運作的 toobe hello 模型具有 toobe 公開，輕鬆地取用來自各種不同的應用程式，例如線上網站、 試算表、 儀表板或商務和後端應用程式開啟 API 介面。 如需使用 Azure Machine Learning Web 服務實作模型的範例，請參閱[部署 Azure Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。 它也是最佳的作法 toobuild 遙測和監視分成 hello 生產模型和資料部署的管線 toohelp hello 與後續的系統狀態報告和疑難排解。  

### <a name="artifacts"></a>構件
* 系統健康狀態和重要度量的狀態儀表板。
* 具有部署詳細資料的最終模型報告。
* 最終的方案架構文件。

## <a name="5-customer-acceptance"></a>5.客戶接受度

### <a name="goal"></a>目標
* **完成 hello 專案的交付項目**： 確認 hello 管線、 hello 模型，以及其部署在生產環境中都能滿足客戶的目標。

### <a name="how-toodo-it"></a>如何 toodo 它
此階段會解決兩項主要工作︰

* **系統驗證**： 確認部署的 hello 模型和管線有符合客戶需求。
* **專案遞交**: toohello 是 toorun hello 系統在生產環境中的實體。

hello 客戶應該驗證 hello 系統符合其商務需求，和 hello 答案 hello 問題與可接受的精確度 toodeploy hello 系統 tooproduction 供其用戶端應用程式。 所有的 hello 文件已完成，並檢閱。 遞交的 hello 專案 toohello 實體，負責作業已完成。 例如，此實體可能是 IT 或客戶資料科學團隊會負責執行 hello 系統在生產環境中的 hello 客戶的代理程式。 

### <a name="artifacts"></a>構件
產生此最後一個階段中的 hello 主要成品為 hello**結束報表的客戶專案**。 這是 hello 技術報表包含有關該有用 toolearn hello 專案的所有詳細資料，而且運作 hello 系統。 TDSP 會提供[結束報表](https://github.com/Azure/Azure-TDSP-ProjectTemplate/blob/master/Docs/Project/Exit%20Report.md)範本供您依原狀使用，或經過自訂以符合特定用戶端需求。 

## <a name="summary"></a>摘要
hello[小組資料科學程序生命週期](http://aka.ms/datascienceprocess)一系列反覆執行提供的指引 hello 工作的步驟視 toouse 預測模型建立模型。 這些模型可以部署在實際執行環境 toobe 運用 toobuild 智慧型應用程式。 這個程序生命週期 hello 目標是 toocontinue toomove 資料科學專案向前向清除 engagement 結束點。 資料科學是一項工作中參考資料，並探索，所能 tooclearly 通訊的這些工作 tooyour 小組和客戶使用一組妥善定義的員工標準化的範本可協助的成品，則為 true 時避免誤解和增加的複雜資料科學專案成功完成的 hello 機會。

## <a name="next-steps"></a>後續步驟
完整的端對端逐步解說示範 hello 程序中的所有 hello 步驟**特定案例**也提供。 列出並與 hello 中的縮圖描述連結[小組資料科學程序的逐步解說](data-science-process-walkthroughs.md)主題。

