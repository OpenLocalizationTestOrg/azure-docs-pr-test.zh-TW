---
title: "aaaWhat 是小組資料科學程序？  | Microsoft Docs"
description: "hello 小組資料科學程序是用於建置運用進階的分析的智慧型應用程式系統化方法。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a098aa2e-fd79-4543-8e15-9aae9d8b3ee6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/18/2017
ms.author: bradsev
ROBOTS: NOINDEX
redirect_url: data-science-process-overview
redirect_document_id: True
ms.openlocfilehash: 57187be9c884389c13c226eab74aff137f5514a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-team-data-science-process-tdsp"></a>什麼是 hello 小組資料科學程序 (TDSP)？
hello[小組資料科學程序 (TDSP)](data-science-process-overview.md)提供系統化的方法，讓資料科學家 toocollaborate 的小組可以在 hello 活動所需的完整生命週期的有效的 toobuilding 智慧型應用程式tooturn 到產品中，這些應用程式。 hello TDSP 概要說明一系列提供的步驟**指引**上如何 toodefine hello 問題，請設定 hello 工具和環境的需要分析相關的資料，建置和評估預測模型，然後再部署在這些模型企業應用程式。 

以下是中的 hello 步驟**資料科學的小組流程**:  

![CAP 工作流程](./media/machine-learning-data-science-the-cortana-analytics-process/CAP-workflow.png)

hello 程序是**反覆**: hello 程度的了解新的和現有的或因 hello 模型中的發展，而且需要縮短之前已經完成 hello 序列中的步驟。 現有的組織開發和專案計劃程序都**輕鬆地調整**toowork 以 hello TDSP 定義步驟的順序。 

hello hello 程序中的步驟訂位，而且連結 hello [TDSP 學習路徑](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)和下面所述。  

## <a name="preparation-steps"></a>準備步驟
## <a name="p1-plan-hello-analytics-project"></a>P1. 規劃 hello 分析專案
定義您的商業目標和問題，是展開分析專案的第一步。 這些項目會以 **商業需求**的形式指定。 此步驟中的中央目標是 tooidentify hello 重要商務變數 （銷售預測，或例如 hello 機率順序、 詐騙） hello 分析需求 toopredict toosatisfy 這些需求。 額外的規劃是則通常是不可或缺的 toodevelop hello 了解**資料來源**需要 tooaddress hello 從分析的觀點來看 hello 專案的目標。 是很常見的例如，現有的系統需要 toocollect 及記錄其他種類的資料 tooaddress toofind hello 問題達成 hello 專案目標。 如需指引，請參閱[規劃您的環境的 hello 資料科學的小組流程](machine-learning-data-science-plan-your-environment.md)和[Azure Machine Learning 中的進階分析的案例](machine-learning-data-science-plan-sample-scenarios.md)。  

## <a name="p2-setup-analytics-environment"></a>P2. 設定分析環境
分析環境的 hello 小組資料科學程序包含數個元件： 

* **資料工作區**hello 資料進行分析和模型，預備位置 
* **處理基礎結構**前置處理、 瀏覽，和 hello 資料模型化
* **執行階段基礎結構**toooperationalize hello 分析模型及執行使用 hello 模型的 hello 智慧型用戶端應用程式。  

hello 分析基礎結構需要 toobe 安裝程式通常是環境的分開核心作業系統的一部分。 但它通常會運用 hello 企業中的多個系統以及從來源外部 toohello 公司的資料。 hello 分析基礎結構可以單純雲端為基礎，或在內部部署安裝程式或混合 hello 兩個。 選項，請參閱[設定資料科學環境以用於資料科學的小組流程 hello](machine-learning-data-science-environment-setup.md)。

## <a name="analytics-steps"></a>分析步驟：
## <a name="1-ingest-data-into-hello-analytical-environment"></a>1.內嵌資料到 hello 分析環境
hello 第一個步驟是從各種來源，或從內從外部 hello 企業版到可處理 hello 資料分析環境 toobring hello 相關資料。 hello**格式**hello 的資料來源可能會有所不同 hello hello 目的地所需的格式。 因此某些資料轉換也可能會有 toobe hello 擷取工具所完成。 如需選項，請參閱 [將資料載入至儲存體環境進行分析](machine-learning-data-science-ingest-data.md)

加法 toohello 初始擷取，資料的位置表示，在許多的智慧型應用程式會是需要的 toorefresh hello 資料定期持續學習程序的一部分。 這可以透過設定 **資料管線** 或工作流程來完成。 這會形成 hello 反覆 hello 程序的一部分，其中包含重建和重新評估 hello hello 方案部署的 hello 智慧型應用程式所使用的分析模型的一部分。 例如，請參閱[移動資料，從在內部部署 SQL server tooSQL Azure 與 Azure Data Factory](machine-learning-data-science-move-sql-azure-adf.md)。

## <a name="2-explore-and-pre-process-data"></a>2.瀏覽和前置處理資料
hello 下一個步驟是 tooobtain hello 資料更深入瞭解透過調查其**摘要統計資料**，關聯性，也可以使用這類技術**視覺效果**。 這也是處理 **資料品質** 及完整性問題之處，例如遺漏值、資料類型不相符和資料關聯性不一致等。 前置處理的轉換會使用的 tooclean hello 進一步分析之前的原始資料，而且可以進行模型化。 如需說明，請參閱[任務 tooprepare 資料增強的機器學習](machine-learning-data-science-prepare-data.md)。

## <a name="3-develop-features"></a>3.開發特性
資料科學家，在與網域專家，必須識別 hello hello 資料集，該擷取 hello 主要屬性可以最適合使用的 toopredict hello 關鍵商務變數在計劃期間識別的功能。 這些新功能可以衍生自現有資料，或可能需要額外的資料 toobe 收集。 這個程序稱為**功能工程**和是其中一個 hello 建置有效的預測分析系統的主要步驟。 此步驟中需要有創意的網域專業與 hello insights 取自 hello 資料瀏覽步驟組合。 如需指引，請參閱[功能 hello 小組資料科學程序中的工程](machine-learning-data-science-create-features.md)。

## <a name="4-create-predictive-models"></a>4.建立預測模型
資料科學家建立分析模型 toopredict hello 重要變數 hello hello 規劃步驟，使用已清除的資料和特徵化中所定義的商務需求所識別。 機器學習系統支援多個**模型的演算法**所適用的 tooa 各種不同的案例。 如需指引，請參閱[如何 toochoose 小組 Azure 機器學習演算法](machine-learning-algorithm-choice.md)。

資料科學家必須選擇其預測工作的 hello 最適當模型，而且是很常見，來自多個模型的結果必須結合 toobe tooobtain hello 獲得最佳結果。 hello 用於模型化的輸入的資料通常分成隨機三個部分：

* 訓練資料集、 
* 驗證資料集 
* 測試資料集 

建立 hello 模型使用 hello**定型資料集**。 hello （具有參數調整） 的模型的最佳組合已選取執行 hello 模型，並測量 hello 的 hello 預測錯誤**驗證資料集**。 最後 hello**測試資料集**是獨立的資料不是使用的 tootrain hello 選擇模型用的 tooevaluate hello 效能或驗證 hello 模型。  如需程序，請參閱[tooevaluate 建立 Azure Machine Learning 中的效能的模型](machine-learning-evaluate-model-performance.md)。

## <a name="5-deploy-and-consume-models"></a>5.部署和取用模型
一旦我們有一組執行的模型，可以是**實際運作**的其他應用程式 tooconsume。 根據 hello 的商務需求，會進行預測有兩種**即時**或在**批次**為基礎。 實際運作的 toobe hello 模型具有以公開 toobe**開啟 API 介面**，輕鬆地取用來自各種不同的應用程式這類線上網站、 試算表、 儀表板或商務和後端應用程式。 請參閱 [部署 Azure Machine Learning Web 服務](machine-learning-publish-a-machine-learning-web-service.md)。

## <a name="summary-and-next-steps"></a>摘要和後續步驟
hello[資料科學的小組流程](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)塑造成一系列反覆執行的步驟，**提供指引**hello 工作所需的 toouse 進階分析 toobuild 的智慧型應用程式。 每個步驟也會提供有關如何 toouse 各種 Microsoft 技術 toocomplete hello 描述工作的細節。 

雖然 TDSP 事先特定類型的未限定**文件**成品，是最佳作法 toodocument hello 結果 hello 資料瀏覽、 模型和評估，以及 toosave hello 相關的程式碼，因此，hello 分析可反覆執行時所需。 這也讓的 hello 分析工作牽涉到類似的資料和預測工作的其他應用程式上工作時重複使用。

完整的端對端逐步解說示範 hello 程序中的所有 hello 步驟**特定案例**也提供。 例如，請參閱︰

* [在動作中的 hello 小組資料科學程序： 使用 SQL Server](machine-learning-data-science-process-sql-walkthrough.md)
* [在動作中的 hello 小組資料科學程序： 使用 HDInsight Hadoop 叢集](machine-learning-data-science-process-hive-walkthrough.md)。
* [在 Azure HDInsight 上使用 Spark 的資料科學](machine-learning-data-science-spark-overview.md)
* [Azure Data Lake 中的可調整資料科學︰端對端逐步解說](machine-learning-data-science-process-data-lake-walkthrough.md)

