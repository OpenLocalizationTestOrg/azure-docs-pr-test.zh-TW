Azure Data Factory 支援 hello 遵循與另一個活動可以是加入的 toopipelines 個別或鏈結轉換活動。

| 資料轉換活動 | 計算環境 |
|:--- |:--- |
| [Hive](../articles/data-factory/data-factory-hive-activity.md) |HDInsight [Hadoop] |
| [Pig](../articles/data-factory/data-factory-pig-activity.md) |HDInsight [Hadoop] |
| [MapReduce](../articles/data-factory/data-factory-map-reduce.md) |HDInsight [Hadoop] |
| [Hadoop 串流](../articles/data-factory/data-factory-hadoop-streaming-activity.md) |HDInsight [Hadoop] |
| [Spark](../articles/data-factory/data-factory-spark.md) | HDInsight [Hadoop] |
| [Machine Learning 活動︰批次執行和更新資源](../articles/data-factory/data-factory-azure-ml-batch-execution-activity.md) |Azure VM |
| [預存程序](../articles/data-factory/data-factory-stored-proc-activity.md) |Azure SQL、Azure SQL 資料倉儲或 SQL Server |
| [Data Lake Analytics U-SQL](../articles/data-factory/data-factory-usql-activity.md) |Azure Data Lake Analytics |
| [DotNet](../articles/data-factory/data-factory-use-custom-activities.md) |HDInsight [Hadoop] 或 Azure Batch |

> [!NOTE]
> 您可以使用 MapReduce 活動 toorun Spark 程式 HDInsight Spark 叢集上。 如需詳細資訊，請參閱 [從 Azure Data Factory 叫用 Spark 程式](../articles/data-factory/data-factory-spark.md) 。
> 您可以建立自訂活動 toorun R 指令碼在您的 HDInsight 叢集上使用 R 安裝。 請參閱 [使用 Azure Data Factory 執行 R 指令碼](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/RunRScriptUsingADFSample)。
> 
> 

