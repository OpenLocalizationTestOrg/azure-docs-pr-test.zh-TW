---
title: "aaaSpark BI 使用 Azure HDInsight 上的資料視覺效果工具 |Microsoft 文件"
description: "透過 HDInsight 叢集上的 Apache Spark BI 使用分析的資料視覺效果工具"
keywords: "apache spark bi, spark bi, spark 資料視覺效果, spark 商業智慧"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1448b536-9bc8-46bc-bbc6-d7001623642a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: ba4bfff737ce80ffca5c24f1c2c82a1447f467fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-bi-using-data-visualization-tools-with-azure-hdinsight"></a>使用資料視覺效果工具搭配 Azure HDInsight 的 Apache Spark BI

了解如何 toouse 資料視覺效果工具，例如 Power BI 和 Tableau tooanalyze HDInsight 叢集上使用 Apache Spark BI 未經處理的範例資料集。

> [!NOTE]
> Azure HDInsight 3.6 預覽版的 Spark 2.1 不支援本文所述的 BI 工具連接性。 僅支援 Spark 1.6 版和 2.0 版 (分別是 HDInsight 3.4 版和 3.5 版)。
>

本教學課程也可在 HDInsight Spark 叢集上用來作為 Jupyter Notebook。 hello 筆記本體驗可讓您從本身的 hello 筆記本執行 hello Python 程式碼片段。 tooperform hello 教學課程中的筆記本內建立 Spark 叢集，請啟動 Jupyter 筆記本 (`https://CLUSTERNAME.azurehdinsight.net/jupyter`)，然後執行 hello 筆記本**使用 BI 工具和 Apache Spark 上 HDInsight.ipynb**下 hello **Python**資料夾。

## <a name="prerequisites"></a>必要條件

* HDInsight 上的 Apache Spark 叢集。 如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。


## <a name="hivetable"></a>準備 Spark 資料視覺效果的資料

在本節中，我們使用 hello [Jupyter](https://jupyter.org)筆記本從 HDInsight Spark 叢集 toorun 作業時，處理未經處理的範例資料，並將它儲存為資料表。 上的.csv 檔案 (hvac.csv) 使用預設的所有叢集 hello 範例資料。 一旦您的資料會儲存為資料表，hello 下一節中我們使用 BI 工具 tooconnect toohello 資料表並執行資料視覺效果。

> [!NOTE]
> 如果您要執行 hello 這篇文章中的步驟完成中的 hello 指示之後[HDInsight Spark 叢集上執行的互動式查詢](hdinsight-apache-spark-load-data-run-query.md)，您可以略過 tooStep 8 下方。
>

1. 從 hello [Azure 入口網站](https://portal.azure.com/)，從 hello 開始面板中，按一下 Spark 叢集中的 hello 磚 （如果您釘選它 toohello 開始面板）。 您也可以導覽 tooyour 叢集下的**瀏覽所有** > **HDInsight 叢集**。   

2. 從 hello Spark 叢集刀鋒視窗中，按一下 **叢集儀表板**，然後按一下 **Jupyter 筆記本**。 如果出現提示，請輸入 hello 叢集 hello 系統管理員認證。

   > [!NOTE]
   > 您也可能由下列 URL 在瀏覽器中開啟 hello 叢集到達 hello Jupyter 筆記本。 取代**CLUSTERNAME** hello 名稱，為您的叢集：
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. 建立 Notebook。 按一下 新增，然後按一下PySpark。

    ![建立 Apache Spark BI 的 Jupyter Notebook](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "建立 Apache Spark BI 的 Jupyter Notebook")

4. 建立新的記事本，並開啟 hello 名稱 Untitled.pynb。 按一下頂端 hello hello 筆記本名稱並輸入好記的名稱。

    ![為提供的名稱 hello 筆記本 Apache Spark bi](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "Apache Spark bi 提供 hello 筆記本的名稱")

5. 因為您建立使用 hello PySpark 核心筆記本，您不需要 toocreate 任何內容明確。 hello Spark 和 Hive 內容會自動建立，當您執行 hello 第一個程式碼儲存格。 您可以開始匯入此案例所需的 hello 型別。 toodo，hello 將游標放在位於 hello 儲存格，按**SHIFT + ENTER**。

        from pyspark.sql import *

6. 將範例資料載入暫存資料表。 當您建立 HDInsight，hello 範例資料檔中的 Spark 叢集**hvac.csv**，是儲存體帳戶相關聯的複製的 toohello **\HdiSamples\HdiSamples\SensorSampleData\hvac**。

    在空的資料格，貼上 hello 下列程式碼片段，然後按**SHIFT + ENTER**。 這個程式碼片段會註冊 hello 資料到資料表，稱為**hvac**。

        # Create an RDD from sample data
        hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))

        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. 請確認已成功建立該 hello 資料表。 您可以使用 hello`%%sql`直接 magic toorun Hive 查詢。 如需有關 hello`%%sql`魔法和其他適用於 hello PySpark 核心中，我們看到[Jupyter notebook Spark HDInsight 叢集上可用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)。

        %%sql
        SHOW TABLES

    您會看到如下所示的輸出：

        +---------------+-------------+
        |tableName      |isTemporary  |
        +---------------+-------------+
        |hvactemptable  |true        |
        |hivesampletable|false        |
        |hvac           |false        |
        +---------------+-------------+

    只有 hello 資料表具有在 hello false **isTemporary**資料行所儲存在 hello 中繼存放區，而且可以從 hello BI 工具存取的 hive 資料表。 在本教學課程中，我們連接 toohello **hvac**我們建立的資料表。

8. 請確認該 hello 資料表包含 hello 適合的資料。 在 hello 筆記本中的空資料格，複製 hello 下列程式碼片段，然後按**SHIFT + ENTER**。

        %%sql
        SELECT * FROM hvac LIMIT 10

9. 關閉 hello 筆記本 toorelease hello 資源。 toodo 的話，從 hello**檔案**hello 筆記本功能表按一下**關閉而停止**。

## <a name="powerbi"></a>使用 Spark 資料視覺效果的 Power BI

> [!NOTE]
> 本節只適用於 HDInsight 3.4 上的 Spark 1.6 以及 HDInsight 3.5 上的 Spark 2.0。
>
>

在 hello 資料儲存為資料表後，您可以使用 Power BI tooconnect toohello 資料和 toocreate 報表視覺效果的儀表板，依此類推。

1. 請確定您具有存取 tooPower BI。 您可以從 [http://www.powerbi.com/](http://www.powerbi.com/)取得 Power BI 的免費預覽版訂用帳戶。

2. 登入太[Power BI](http://www.powerbi.com/)。

3. 從 hello hello 左窗格底部，按一下 **取得資料**。

4. 在 hello**取得資料**頁面的 **匯入或連接 tooData**，如**資料庫**，按一下**取得**。

    ![將資料送入 Apache Spark BI 的 Power BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "將資料送入 Apache Spark BI 的 Power BI")

5. Hello 下一個畫面上，按一下**Azure HDInsight 上的 Spark** ，然後按一下**連接**。 出現提示時，請輸入 hello 叢集 URL (`mysparkcluster.azurehdinsight.net`) 和 hello 認證 tooconnect toohello 叢集。

    ![連接 tooApache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "連接 tooApache Spark BI")

    建立 hello 連接之後，Power BI 會開始從 hello HDInsight 上的 Spark 叢集匯入資料。

6. Power BI 匯入 hello 資料，並新增**Spark** hello 資料集**資料集**標題。 按一下 hello 資料集 tooopen 新的工作表 toovisualize hello 資料。 您也可以當做報表儲存 hello 工作表。 工作表，從 hello toosave**檔案**功能表上，按一下 **儲存**。

    ![Power BI 儀表板上的 Apache Spark BI 圖格](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Power BI 儀表板上的 Apache Spark BI 圖格")
7. 請注意該 hello**欄位**hello 右邊的清單會列出 hello **hvac**您稍早建立的資料表。 如先前在筆記本中定義，請展開 hello 資料表 toosee hello 資料表中的 hello 欄位。

      ![列出 Apache Spark BI 儀表板上的資料表](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "列出 Apache Spark BI 儀表板上的資料表")

8. 建置目標溫度和每個建置實際溫度之間的視覺效果 tooshow hello 變異數。 toovisualize 向資料、 選取**區域圖**（顯示為紅色方塊）。 toodefine hello 座標軸，拖放 hello **BuildingID**欄位底下**軸**，和**ActualTemp**/**TargetTemp**欄位底下**值**。

    ![使用 Apache Spark BI 建立 Spark 資料視覺效果](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "使用 Apache Spark BI 建立 Spark 資料視覺效果")

9. 依預設，hello 視覺效果顯示 hello 總和**ActualTemp**和**TargetTemp**。 同時 hello 欄位，從 [hello] 下拉式清單中選取**平均**tooget 實際的平均和這兩個大樓目標溫度。

    ![使用 Apache Spark BI 建立 Spark 資料視覺效果](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "使用 Apache Spark BI 建立 Spark 資料視覺效果")

10. 您的資料視覺效果應該在 hello 螢幕擷取畫面類似 toohello。 將游標 hello 視覺效果 tooget 具有相關資料的工具提示。

    ![使用 Apache Spark BI 建立 Spark 資料視覺效果](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "使用 Apache Spark BI 建立 Spark 資料視覺效果")

11. 按一下**儲存**hello 從最上層功能表，並提供報表的名稱。 您可以也視覺效果釘選 hello。 當您釘選視覺效果時，它會儲存儀表板上，您可以一眼 hello 最新值。

   您可以將許多視覺效果所需要的 hello 相同的資料集，並將其釘選 toohello 儀表板的資料快照集。 此外，在 HDInsight 上的 Spark 叢集會連接的 tooPower BI 直接連接。 這可確保 Power BI 一律具有 hello 大部分從叢集中的最新資料，您不需要 tooschedule 重新整理 hello 資料集。

## <a name="tableau"></a>使用 Spark 資料視覺效果的 Tableau Desktop

> [!NOTE]
> 本節只適用於在 Azure HDInsight 中建立的 Spark 1.5.2 叢集。
>
>

1. 安裝[Tableau 桌面](http://www.tableau.com/products/desktop)hello 執行本教學課程中 Apache Spark BI 所在的電腦上。

2. 確保這部電腦也也安裝 Microsoft Spark ODBC 驅動程式。 您可以安裝 hello 驅動程式從[這裡](http://go.microsoft.com/fwlink/?LinkId=616229)。

1. 啟動 Tableau Desktop。 Hello 左窗格中，從伺服器 tooconnect，hello 清單按一下**Spark SQL**。 如果 hello 左窗格中預設不會列出 Spark SQL，您可以找出它按一下**多伺服器**。
2. 在 [hello Spark SQL 連線] 對話方塊中提供 hello 值 hello 螢幕擷取畫面所示，然後按**確定**。

    ![Apache Spark bi 連接 tooa 叢集](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Apache Spark bi 連接 tooa 叢集")

    hello 驗證下拉式清單**Microsoft Azure HDInsight 服務**的選項，只有當您安裝 hello [Microsoft Spark ODBC 驅動程式](http://go.microsoft.com/fwlink/?LinkId=616229)hello 電腦上。
3. Hello 下一個畫面中，從 hello**結構描述**下拉式清單中，按一下 hello**尋找**圖示，然後再按一下**預設**。

    ![尋找 Apache Spark BI 的結構描述](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "尋找 Apache Spark BI 的結構描述")
4. Hello**資料表**欄位中，按一下 hello**尋找**圖示再次 toolist 所有 hello Hive hello 叢集中可用的資料表。 您應該會看見 hello **hvac**先前使用 hello 筆記本所建立的資料表。

    ![尋找 Apache Spark BI 的資料表](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "尋找 Apache Spark BI 的資料表")
5. 拖放 hello 資料表 toohello 頂端的方塊上 hello 右。 Tableau 匯入 hello 資料，並顯示 hello 紅色方塊以反白顯示 hello 結構描述。

    ![加入資料表 tooTableau Apache Spark bi](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "新增資料表 tooTableau Apache Spark bi")
6. 按一下 hello **Sheet1**在 hello 左下方的索引標籤。 請針對每個日期顯示 hello 平均目標與實際溫度所有建築物的視覺效果。 拖曳**日期**和**建置 ID**太**資料行**和**實際 Temp**/**目標 Temp**太**列**。 在下**標記**，選取**區域**toouse Spark 資料視覺效果的區域對應。

     ![新增 Spark 資料視覺效果的欄位](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "新增 Spark 資料視覺效果的欄位")
7. 根據預設，hello 溫度欄位會顯示為彙總。 若要改為 tooshow hello 平均溫度，您可以從 hello 下拉式清單，如下所示。

    ![採取 Spark 資料視覺效果的平均溫度](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "採取 Spark 資料視覺效果的平均溫度")

8. 您也可以超級-強加一個溫度對應超過 hello 其他 tooget 目標與實際的溫度之間差異的好風格。 移動 hello 較低的區域地圖的 hello 滑鼠 toohello 角，直到您看到 hello 控點圖形中的紅色圓圈反白顯示。 拖曳 hello 對應 toohello hello top 和發行 hello 滑鼠上的其他對應時，您會看到紅色矩形中反白顯示 hello 圖形。

    ![合併 Spark 資料視覺效果的對應圖](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "合併 Spark 資料視覺效果的對應圖")

     您的資料視覺效果應該變更 hello 螢幕擷取畫面所示：

    ![Spark 資料視覺效果的 Tableau 輸出](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Spark 資料視覺效果的 Tableau 輸出")
9. 按一下**儲存**toosave hello 工作表。 您可以建立儀表板，並新增一或多個工作表 tooit。

## <a name="next-steps"></a>後續步驟

到目前為止您學會如何 toocreate 叢集中，建立 Spark 資料框架 tooquery 資料，並從 BI 工具存取該資料。 您現在可以看看如何 toomanage hello 叢集資源和偵錯 HDInsight Spark 叢集中執行的工作上的指示。

* [管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源](hdinsight-apache-spark-resource-manager.md)
* [追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業](hdinsight-apache-spark-job-debugging.md)

