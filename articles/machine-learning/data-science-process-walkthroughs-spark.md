---
title: "在 Azure 上使用 PySpark 和 Scala aaaHDInsight Spark 逐步解說 |Microsoft 文件"
description: "逐步解說 hello hello 小組資料科學程序的範例使用 PySpark 和 Scala Azure HDInsight Spark toodo 預測分析。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: f8b41a8cae414586570761ba4b4eb4c239cbb981
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hdinsight-spark-data-science-walkthroughs-using-pyspark-and-scala-on-azure"></a>在 Azure 上使用 PySpark 和 Scala 的 HDInsight Spark 資料科學逐步解說

這些逐步解說會使用 PySpark 和 Scala Azure Spark 叢集 toodo 預測分析。 它們遵循下列 hello hello 小組資料科學程序中所述的步驟。 如需 hello 小組資料科學程序的概觀，請參閱[資料科學程序](data-science-process-overview.md)。 如需 HDInsight 上的 Spark 的概觀，請參閱[HDInsight 上的簡介 tooSpark](../hdinsight/hdinsight-apache-spark-overview.md)。

執行 hello 資料科學的小組流程的其他資料科學逐步解說會依照 hello**平台**它們使用： 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]

## <a name="predict-taxi-tips-using-pyspark-on-azure-spark"></a>在 Azure Spark 上使用 PySpark 來預測計程車小費

hello[使用 Azure HDInsight 上的 Spark](machine-learning-data-science-spark-overview.md)逐步解說會使用從紐約 taxis toopredict 資料是否付費的秘訣和金額的 hello 範圍應 toobe 付費。 它會使用案例，使用中的 hello 資料科學的小組流程[Azure HDInsight Spark 叢集](https://azure.microsoft.com/services/hdinsight/)toostore，瀏覽和功能從 hello 公開可用 NYC 計程車路線工程資料及再見資料集。 這個概觀主題會設定您 HDInsight Spark 叢集與 hello Jupyter PySpark 筆記本中的 hello 逐步解說的 hello 其餘部分使用。 這些筆記本告訴您如何 tooexplore 您的資料，然後如何 toocreate 和取用模型。 進階資料瀏覽以及如何模型化筆記本顯示 hello tooinclude 交叉驗證，超參數牽涉和模型評估。

### <a name="data-exploration-and-modeling-with-spark"></a>使用 Spark 進行資料探索和模型化 
瀏覽 hello 資料集以及建立、 計分，和透過 hello 工作來評估 hello 機器學習模型[建立資料的二元分類和迴歸模型使用 hello Spark MLlib toolkit](machine-learning-data-science-spark-data-exploration-modeling.md)主題。

### <a name="model-consumption"></a>模型耗用量
toolearn 如何 tooscore hello 分類和迴歸模型建立本主題中，請參閱[分數及評估 Spark 建立機器學習模型](machine-learning-data-science-spark-model-consumption.md)。

### <a name="cross-validation-and-hyperparameter-sweeping"></a>交叉驗證和超參數掃掠
如需如何使用交叉驗證和超參數掃掠訓練模型的相關資訊，請參閱[使用 Spark 進階資料探索和模型化](machine-learning-data-science-spark-advanced-data-exploration-modeling.md)。


## <a name="predict-taxi-tips-using-scala-on-azure-spark"></a>在 Azure Spark 上使用 Scala 來預測計程車小費

hello[與 Azure 上的 Spark 使用 Scala](machine-learning-data-science-process-scala-walkthrough.md)逐步解說會使用從紐約 taxis toopredict 資料是否付費的秘訣和金額的 hello 範圍應 toobe 付費。 它會顯示為受監督的機器學習工作 hello Spark 機器學習程式庫 (MLlib) 與 SparkML toouse Scala Azure HDInsight Spark 叢集上的封裝。 它會引導您完成 hello 工作構成 hello[資料科學程序](http://aka.ms/datascienceprocess)： 擷取資料並探索、 視覺效果、 功能工程、 模型和模型耗用量。 內建的 hello 模型包括羅吉斯和線性迴歸、 隨機樹系和梯度促進式樹狀結構。


## <a name="next-steps"></a>後續步驟

Hello 主要元件組成 hello 資料科學的小組流程的討論，請參閱[小組資料科學程序概觀](data-science-process-overview.md)。

如需您可以使用 toostructure hello 小組資料科學程序生命週期的討論資料科學專案，請參閱[小組資料科學程序生命週期](data-science-process-lifecycle.md)。 hello 生命週期概述 hello 步驟，從開始 toofinish 專案通常會遵循在執行時。 

