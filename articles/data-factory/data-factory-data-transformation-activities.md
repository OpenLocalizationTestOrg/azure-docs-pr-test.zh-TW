---
title: "資料轉換︰處理和轉換資料 | Microsoft Docs"
description: "深入了解如何 tootransform 資料或處理使用 Hadoop、 機器學習服務或 Azure Data Lake Analytics 的 Azure Data Factory 中的資料。"
keywords: "資料轉換, 處理資料, 轉換資料, 轉換活動"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: 39786731-1e4b-40a4-81b7-d06e127427aa
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: shlo
ms.openlocfilehash: 917d617259699b0e71de3a0e0c17463d00f2e0a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-in-azure-data-factory"></a>Azure Data Factory 中的資料轉換
> [!div class="op_single_selector"]
> * [Hive](data-factory-hive-activity.md)  
> * [Pig](data-factory-pig-activity.md)  
> * [MapReduce](data-factory-map-reduce.md)  
> * [Hadoop 串流](data-factory-hadoop-streaming-activity.md)
> * [機器學習服務](data-factory-azure-ml-batch-execution-activity.md) 
> * [預存程序](data-factory-stored-proc-activity.md)
> * [Data Lake Analytics U-SQL](data-factory-usql-activity.md)
> * [.NET 自訂](data-factory-use-custom-activities.md)

## <a name="overview"></a>概觀
本文說明您可以使用 tootransform，並將預測和 insights 處理未經處理資料的 Azure Data Factory 中的資料轉換活動。 轉換活動會在計算環境中執行，例如 Azure HDInsight 叢集或 Azure Batch。 它提供連結 tooarticles 並在每個轉換活動的詳細資訊。

Data Factory 支援下列資料轉換的活動太可加入的 hello[管線](data-factory-create-pipelines.md)可以個別或鏈結與另一個活動。

> [!NOTE]
> 如需逐步解說，請參閱 [建立可 Hive 轉換的管線](data-factory-build-your-first-pipeline.md) 。  
> 
> 

## <a name="hdinsight-hive-activity"></a>HDInsight Hive 活動
hello HDInsight Hive 活動 Data Factory 管線中執行您自己的 Hive 查詢或隨 Windows/linux 的 HDInsight 叢集。 如需此活動的詳細資訊，請參閱 [Hive 活動](data-factory-hive-activity.md) 。 

## <a name="hdinsight-pig-activity"></a>HDInsight Pig 活動
hello HDInsight Pig 活動 Data Factory 管線中執行您自己的 Pig 查詢或隨 Windows/linux 的 HDInsight 叢集。 如需此活動的詳細資訊，請參閱 [Pig 活動](data-factory-pig-activity.md) 。 

## <a name="hdinsight-mapreduce-activity"></a>HDInsight MapReduce 活動
hello HDInsight MapReduce 活動 Data Factory 管線中執行您自己的 MapReduce 程式或隨 Windows/linux 的 HDInsight 叢集。 如需此活動的詳細資訊，請參閱 [MapReduce 活動](data-factory-map-reduce.md) 。

## <a name="hdinsight-streaming-activity"></a>HDInsight 串流活動
Data Factory 管線中的 hello HDInsight 串流活動執行您自己的 Hadoop 串流程式或隨 Windows/linux 的 HDInsight 叢集。 如需此活動的詳細資訊，請參閱 [HDInsight 串流活動](data-factory-hadoop-streaming-activity.md) 。

## <a name="hdinsight-spark-activity"></a>HDInsight Spark 活動
hello HDInsight Spark Data Factory 管線中的活動執行您自己的 HDInsight 叢集上的 Spark 程式。 如需詳細資訊，請參閱[從 Azure Data Factory 叫用 Spark 程式](data-factory-spark.md)。 

## <a name="machine-learning-activities"></a>Machine Learning 活動
Azure Data Factory 可讓您 tooeasily 建立管線，使用已發行的 Azure Machine Learning web 服務的預測分析。 使用 hello[批次執行活動](data-factory-azure-ml-batch-execution-activity.md#invoking-a-web-service-using-batch-execution-activity)在 Azure Data Factory 管線中，您可以叫用批次中的 hello 資料機器學習 web 服務 toomake 的預測。

經過一段時間，在 hello 計分實驗需要 toobe 重新定型使用全新的機器學習中的 hello 預測模型的輸入資料集。 您完成定型之後，您會想要計分 web 服務以 hello tooupdate hello 重新定型機器學習模型。 您可以使用 hello[更新資源活動](data-factory-azure-ml-batch-execution-activity.md#updating-models-using-update-resource-activity)tooupdate hello web 服務與 hello 定型新模型。  

如需這些機器學習活動的詳細資料，請參閱 [使用 Machine Learning 活動](data-factory-azure-ml-batch-execution-activity.md) 。 

## <a name="stored-procedure-activity"></a>預存程序活動
您可以使用 Data Factory 管線 tooinvoke 其中一種 hello 下列資料存放區預存程序中的 hello SQL Server 預存程序活動： Azure SQL Database、 Azure SQL 資料倉儲，在您企業中的 SQL Server 資料庫或 Azure VM。 如需詳細資料，請參閱 [預存程序活動](data-factory-stored-proc-activity.md) 。  

## <a name="data-lake-analytics-u-sql-activity"></a>Data Lake Analytics U-SQL 活動
Data Lake Analytics U-SQL 活動會在 Azure Data Lake Analytics 叢集上執行 U-SQL 指令碼。 如需詳細資料，請參閱 [U-SQL 活動](data-factory-usql-activity.md) 。 

## <a name="net-custom-activity"></a>.NET 自訂活動
如果您需要 tootransform 資料不支援的 Data Factory 的方式，您可以建立您自己的資料處理邏輯的自訂活動，並使用 hello 管線中的 hello 活動。 您可以設定 hello 自訂.NET 活動 toorun 使用 Azure Batch 服務或 Azure HDInsight 叢集。 如需詳細資訊請參閱 [使用自訂活動](data-factory-use-custom-activities.md) 。 

您可以建立自訂活動 toorun R 指令碼在您的 HDInsight 叢集上使用 R 安裝。 請參閱 [使用 Azure Data Factory 執行 R 指令碼](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)。 

## <a name="compute-environments"></a>計算環境
您建立連結的服務的 hello 計算環境，然後使用連結的 hello 服務定義轉換活動時。 Data Factory 支援兩種類型的資計算環境。 

1. **視**: hello 運算環境完全在此情況下，管理由資料處理站。 它會自動建立 hello Data Factory 服務作業送出的 tooprocess 資料之前，移除 hello 工作完成時。 您可以設定及控制細微 hello 視運算環境執行的作業、 叢集管理和啟動載入動作的設定。 
2. **攜帶您自己的裝置**：在此情況下，您可以註冊自己的運算環境 (例如 HDInsight 叢集)，做為 Data Factory 中的連結服務。 hello 運算環境由您管理和 hello Data Factory 服務會使用它 tooexecute hello 活動。 

請參閱[計算連結服務](data-factory-compute-linked-services.md)有關的文章 toolearn 計算服務支援的 Data Factory。 

## <a name="summary"></a>摘要
Azure Data Factory 支援 hello 遵循資料轉換活動與 hello hello 活動的運算環境。 hello 轉換活動可以加入的 toopipelines 可以個別或鏈結與另一個活動。

| 資料轉換活動 | 計算環境 |
|:--- |:--- |
| [Hive](data-factory-hive-activity.md) |HDInsight [Hadoop] |
| [Pig](data-factory-pig-activity.md) |HDInsight [Hadoop] |
| [MapReduce](data-factory-map-reduce.md) |HDInsight [Hadoop] |
| [Hadoop 串流](data-factory-hadoop-streaming-activity.md) |HDInsight [Hadoop] |
| [Machine Learning 活動︰批次執行和更新資源](data-factory-azure-ml-batch-execution-activity.md) |Azure VM |
| [預存程序](data-factory-stored-proc-activity.md) |Azure SQL、Azure SQL 資料倉儲或 SQL Server |
| [Data Lake Analytics U-SQL](data-factory-usql-activity.md) |Azure Data Lake Analytics |
| [DotNet](data-factory-use-custom-activities.md) |HDInsight [Hadoop] 或 Azure Batch |

