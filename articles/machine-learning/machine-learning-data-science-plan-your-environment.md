---
title: "aaaIdentify 案例和規劃您的分析程序-Azure |Microsoft 文件"
description: "考慮一系列重要問題來規劃進階分析環境。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 421520dd-7728-4d29-889c-ebe6a0a6fb07
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: e445973be0d020a4f9949e5c9d8554fbbd4b515f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooidentify-scenarios-and-plan-for-advanced-analytics-data-processing"></a>Tooidentify 案例和規劃的進階分析資料處理
資源應該您計劃 tooinclude 時設定環境 toodo 進階分析的資料集處理？ 這篇文章會建議一系列的有助於找出 hello 工作和資源相關的問題 tooask 您的案例。 predictive analytics 的高階步驟 hello 順序中所述[hello 小組資料科學程序 (TDSP) 是什麼？](data-science-process-overview.md)。 每個步驟將 hello 工作相關的 tooyour 特定案例需要特定的資源。 hello 重要的問題 tooidentify 您案例考量資料邏輯特性，hello hello 資料集，和 hello 工具和語言偏好 toodo hello 分析的品質。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="logistic-questions-data-locations-and-movement"></a>邏輯問題：資料位置和移動
hello 羅吉斯問題有關的 hello hello 位置**資料來源**，hello**目標目的地**在 Azure 中，與 hello 資料移動的需求，包括 hello 排程、 數量和資源涉及。 hello 資料可能需要 toobe hello 分析程序期間移數次。 常見的案例是到某種形式的 Azure 上儲存體中，然後將 Machine Learning Studio toomove 本機資料。

1. **資料來源是什麼？** 是本機還是 hello 雲端？ 例如：
   
   * 可公開使用的 HTTP 位址在 hello 資料。
   * hello 資料位於本機或網路檔案位置。
   * hello 資料是在 SQL Server 資料庫。
   * hello 資料會儲存在 Azure 儲存體容器
2. **Hello Azure 的目的是什麼？** 其中是否需要 toobe 為處理，或建立模型？ 例如：
   
   * Azure Blob 儲存體
   * SQL Azure 資料庫
   * 在 Azure VM 上的 SQL Server
   * HDInsight (Azure 上的 Hadoop) 或 Hive 資料表
   * Azure Machine Learning
   * 可裝載的 Azure 虛擬硬碟。
3. **您要如何 toomove hello 資料？** hello 下列主題中所述的 hello 程序和資源使用 tooingest 或載入資料到各種不同的儲存和處理環境。
   
   * [將資料載入至儲存體環境以便進行分析](machine-learning-data-science-ingest-data.md)
   * [從各種資料來源將定型資料匯入 Azure Machine Learning Studio](machine-learning-data-science-import-data.md)。
4. **Hello 資料需要定期移動或移轉期間修改 toobe 嗎？** 請考慮使用 Azure 資料處理站 (ADF)，資料需求 toobe 持續在移轉時，尤其是混合式案例，用來存取這兩個內部部署和雲端資源與此有關，或何時 hello 資料交易式或需要修改 toobe 或商務邏輯加入 tooit hello 期間正在移轉。 如需詳細資訊，請參閱[移動資料從內部部署 SQL server tooSQL Azure 與 Azure Data Factory](machine-learning-data-science-move-sql-azure-adf.md)
5. **Hello 資料中有多少是移動 toobe tooAzure？** 非常大的資料集可能會超過特定環境的 hello 儲存容量。 如需範例，請參閱 hello 討論的大小限制為 Machine Learning Studio hello 下一節。 在這種情況下可能 hello 分析期間使用 hello 資料的範例。 如需如何 toodown 範例資料集在各種 Azure 環境的詳細資訊，請參閱[範例 hello 小組資料科學程序中的資料](machine-learning-data-science-sample-data.md)。

## <a name="data-characteristics-questions-type-format-and-size"></a>資料特性問題：類型、格式和大小
這些問題是您的儲存體金鑰 tooplanning 和處理的環境，其中每一個都是適當 toovarious 和每一種類型的資料有一些限制。

1. **Hello 資料類型為何？** 例如：
   
   * 數值
   * 類別
   * 字串
   * Binary
2. **如何將資料格式化？** 例如：
   
   * 逗號分隔 (CSV) 或定位鍵分隔 (TSV) 一般檔案
   * 已壓縮或未壓縮
   * Azure Blob
   * Hadoop Hive 資料表
   * SQL Server 資料表
3. **您的資料大小為何？**
   
   * 小型：小於 2 GB
   * 中型：大於 2 GB 且小於 10 GB
   * 大型：大於 10 GB

Hello Azure Machine Learning Studio 環境為例：

* 如需 hello 資料格式和 Azure Machine Learning Studio 所支援類型的清單，請參閱[資料格式和支援的資料型別](machine-learning-data-science-import-data.md#data-formats-and-data-types-supported)> 一節。
* 如需 Azure Machine Learning Studio 中的資料限制資訊，請參閱 hello**大 hello 資料集可適用於我模組？**區段[匯入及匯出資料的機器學習](machine-learning-faq.md#machine-learning-studio-questions)

Hello 限制 hello 分析程序中使用其他 Azure 服務的詳細資訊，請參閱[Azure 訂用帳戶和服務限制、 配額和條件約束](../azure-subscription-service-limits.md)。

## <a name="data-quality-questions-exploration-and-pre-processing"></a>資料品質問題：探索和前置處理
1. **您對資料的熟悉程度為何？** 瀏覽資料時需要 toogain 了解其基本特性。 資料呈現什麼模式或趨勢、有什麼極端值或遺漏多少值。 這個步驟很重要決定 hello 需要制定假設，藉以而建議 hello 最適當的功能，或輸入的分析，以及制定計劃的其他資料收集的前置處理的程度。 計算描述性統計資料和繪製視覺效果是很有用的資料檢查技術。 如需詳細資訊的方式 tooexplore 資料集在各種 Azure 環境中，請參閱[hello 小組資料科學程序中的資料瀏覽](machine-learning-data-science-explore-data.md)。
2. **Hello 資料需要前置處理，或清除嗎？**
   前置處理和清除資料是很重要的工作，必須先執行這些工作，才能有效地將資料集用於機器學習服務。 未經處理的資料通常會有雜訊且不可靠，還可能會有遺漏值。 使用這類資料進行模型化可能會產生誤導的結果。 如需說明，請參閱[任務 tooprepare 資料增強的機器學習](machine-learning-data-science-prepare-data.md)。

## <a name="tools-and-languages-questions"></a>工具和語言的問題
根據您需要或最喜歡使用的語言和開發環境或工具而定，這裡有許多選項可選擇。

1. **語言怎麼辦偏好 toouse 分析？**  
   
   * R
   * Python
   * SQL
2. **您應該使用哪些工具進行資料分析？**
   
   * [Microsoft Azure Powershell](/powershell/azure/overview) -指令碼語言 tooadminister 您的 Azure 資源中使用指令碼語言。
   * [Azure Machine Learning Studio](machine-learning-what-is-ml-studio.md)
   * [Revolution Analytics](http://www.revolutionanalytics.com/revolution-r-open)
   * [RStudio](http://www.rstudio.com)
   * [Python Tools for Visual Studio](http://microsoft.github.io/PTVS/)
   * [Anaconda](https://www.continuum.io/why-anaconda)
   * [Jupyter 筆記本](http://jupyter.org/)
   * [Microsoft Power BI](http://powerbi.microsoft.com)

## <a name="identify-your-advanced-analytics-scenario"></a>識別您的進階分析案例
一旦您已回答 hello 上一節中的 hello 問題，即準備好 toodetermine 最佳的案例符合您的案例。 hello 範例案例所述[Azure Machine Learning 中的進階分析的案例](machine-learning-data-science-plan-sample-scenarios.md)。

