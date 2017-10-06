---
title: "在 Azure 資料湖存放區中的 Apache Spark tooanalyze 資料 aaaUse |Microsoft 文件"
description: "執行 Spark 作業 tooanalyze 資料儲存在 Azure 資料湖存放區"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 1f174323-c17b-428c-903d-04f0e272784c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 3b7f628f7a8114d2ca6f3f9219ce107905f1c818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-spark-cluster-tooanalyze-data-in-data-lake-store"></a>使用中 Data Lake Store 的 HDInsight Spark 叢集 tooanalyze 資料

在本教學課程中，您可以使用 Jupyter 筆記本可用與 HDInsight Spark 叢集 toorun 從 Data Lake Store 帳戶讀取資料的工作。

## <a name="prerequisites"></a>必要條件

* Azure Data Lake Store 帳戶。 請遵循指示 hello[開始使用 Azure 資料湖存放區使用 hello Azure 入口網站](../data-lake-store/data-lake-store-get-started-portal.md)。

* 以 Data Lake Store 做為儲存體的 Azure HDInsight Spark 叢集。 請遵循指示 hello[建立與使用 Azure 入口網站的 Data Lake Store 的 HDInsight 叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)。

    
## <a name="prepare-hello-data"></a>準備 hello 資料

> [!NOTE]
> 您不需要 tooperform 此步驟中如果您已經建立 hello HDInsight 叢集具有做為預設儲存體的資料湖存放區。 hello 叢集建立程序在您建立 hello 叢集時所指定的 hello Data Lake Store 帳戶新增一些範例資料。 略過 toohello 區段[資料湖存放區的使用 HDInsight Spark 叢集](#use-an-hdinsight-spark-cluster-with-data-lake-store)。
>
>

如果您的 HDInsight 叢集與資料湖存放區做為建立額外的儲存體和 Azure 儲存體 Blob 做為預設儲存體，您應該先複製某些範例資料 toohello Data Lake Store 帳戶。 您可以使用 hello hello 與 hello HDInsight 叢集相關聯的 Azure 儲存體 Blob 的取樣資料。 您可以使用 hello [ADLCopy 工具](http://aka.ms/downloadadlcopy)toodo 如此。 下載並安裝 hello 工具從 hello 連結。

1. 開啟命令提示字元並瀏覽 toohello AdlCopy 安裝的目錄，通常`%HOMEPATH%\Documents\adlcopy`。

2. 從 hello 來源容器 tooa 資料湖存放區執行下列命令 toocopy hello 特定的 blob:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    複製 hello **HVAC.csv**範例資料檔案儲存在**/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello Azure Data Lake Store 帳戶。 hello 程式碼片段看起來應該像：

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > 請確定 hello 檔案和路徑名稱會出現在 hello 適當的大小寫。
   >
   >
3. 您將會提示的 tooenter hello 認證 hello 您擁有的 Data Lake Store 帳戶所在的 Azure 訂用帳戶。 您會看到類似 toohello 下列輸出：

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    hello 資料檔 (**HVAC.csv**) 將會複製資料夾下**/hvac** hello Data Lake Store 帳戶中。

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a>使用具有 Data Lake Store 的 HDInsight Spark 叢集

1. 從 hello [Azure 入口網站](https://portal.azure.com/)，從 hello 開始面板中，按一下 Spark 叢集中的 hello 磚 （如果您釘選它 toohello 開始面板）。 您也可以導覽 tooyour 叢集下的**瀏覽所有** > **HDInsight 叢集**。

2. 從 hello Spark 叢集刀鋒視窗中，按一下 **快速連結**，然後從 hello**叢集儀表板**刀鋒視窗中，按一下  **Jupyter 筆記本**。 如果出現提示，請輸入 hello 叢集 hello 系統管理員認證。

   > [!NOTE]
   > 您也可能由下列 URL 在瀏覽器中開啟 hello 叢集到達 hello Jupyter 筆記本。 取代**CLUSTERNAME** hello 名稱，為您的叢集：
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. 建立新的 Notebook。 按一下 新增，然後按一下PySpark。

    ![建立新的 Jupyter Notebook](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "建立新的 Jupyter Notebook")

4. 因為您建立使用 hello PySpark 核心筆記本，您不需要 toocreate 任何內容明確。 hello Spark 和 Hive 內容將會自動為您建立執行 hello 第一個程式碼儲存格時。 您可以開始匯入此案例所需的 hello 型別。 toodo，貼上下列程式碼片段中的資料格和按 hello **SHIFT + ENTER**。

        from pyspark.sql.types import *

    每次您在 Jupyter 執行作業，將會顯示您的 web 瀏覽器視窗標題**（忙碌）**狀態以及 hello 筆記本標題。 您也會看到實心圓的下一個 toohello **PySpark** hello 右上角中的文字。 Hello 作業完成之後，這會變更 tooa 空心圓圈。

     ![Jupyter Notebook 作業的狀態](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Jupyter Notebook 作業的狀態")

5. 範例資料載入暫存資料表使用 hello **HVAC.csv**複製 toohello Data Lake Store 帳戶的檔案。 您可以存取 hello 資料中使用下列的 URL 模式的 hello hello Data Lake Store 帳戶。

    * 如果您有做為預設儲存體的資料湖存放區，HVAC.csv 會在 hello 路徑類似 toohello 下列 URL:

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        或者，您也可以使用縮短的格式，例如 hello 下列：

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * 如果您有額外的存放裝置與資料湖存放區，HVAC.csv 會在 hello 複製的位置，例如：

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     空白儲存格，下列程式碼範例中，貼上 hello 取代**MYDATALAKESTORE**與您的 Data Lake Store 帳戶名稱，請按**SHIFT + ENTER**。 這個程式碼範例會註冊 hello 資料至暫存資料表稱為**hvac**。

            # Load hello data. hello path below assumes Data Lake Store is default storage for hello Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create hello schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse hello data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register hello data fram as a table toorun queries against
            hvacdf.registerTempTable("hvac")

6. 因為您使用 PySpark 核心，您現在可以直接執行 SQL 查詢 hello 暫存資料表上**hvac**您剛才所建立的使用 hello`%%sql`識別常數。 如需有關 hello`%%sql`識別常數，以及其他適用於 hello PySpark 核心中，我們看到[Jupyter notebook Spark HDInsight 叢集上可用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)。

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. 一旦 hello 工作順利完成時，預設會顯示 hello 遵循表格式輸出。

      ![查詢結果的資料表輸出](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "查詢結果的資料表輸出")

     您也可以查看其他視覺效果中的 hello 結果。 例如，區域圖相同的輸出會如下 hello 示 hello。

     ![查詢結果的區域圖](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "查詢結果的區域圖")

8. 當您完成執行 hello 應用程式之後，您應該關閉 hello 筆記本 toorelease hello 資源。 toodo 的話，從 hello**檔案**hello 筆記本功能表按一下**關閉而停止**。 這將會關機並關閉 hello 筆記本。


## <a name="next-steps"></a>後續步驟

* [Apache Spark 叢集上建立獨立 Scala 應用程式 toorun](hdinsight-apache-spark-create-standalone-application.md)
* [在 Azure Toolkit for HDInsight Spark Linux 叢集的 IntelliJ toocreate Spark 應用程式中使用 HDInsight Tools](hdinsight-apache-spark-intellij-tool-plugin.md)
* [在 Azure Toolkit for Eclipse HDInsight Spark Linux 叢集 toocreate Spark 應用程式中使用 HDInsight Tools](hdinsight-apache-spark-eclipse-tool-plugin.md)
