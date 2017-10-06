---
title: "學習使用 HDInsight 的 Azure 上的 Spark MLlib 範例 aaaMachine |Microsoft 文件"
description: "深入了解如何 toouse Spark MLlib toocreate 分析資料集使用透過羅吉斯迴歸分類的機器學習應用程式。"
keywords: "spark 機器學習, spark 機器學習範例"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c0fd4baa-946d-4e03-ad2c-a03491bd90c8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 5c3b83482de5d8fba224398aaafe07fa67ec1fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-mllib-toobuild-a-machine-learning-application-and-analyze-a-dataset"></a>使用 Spark MLlib toobuild 的機器學習應用程式和分析資料集

深入了解如何 toouse Spark **MLlib** toocreate 的機器學習應用程式 toodo 簡單預測分析開啟資料集。 從 Spark 的內建機器學習程式庫，此範例會透過羅吉斯迴歸使用「分類」。 

> [!TIP]
> 本範例也作為您在 HDInsight 中所建立之 Spark (Linux) 叢集上的 Jupyter Notebook 提供使用。 hello 筆記本體驗可讓您從本身的 hello 筆記本執行 hello Python 程式碼片段。 toofollow hello 教學課程從在筆記本中，建立 Spark 叢集並啟動 Jupyter 筆記本 (`https://CLUSTERNAME.azurehdinsight.net/jupyter`)。 然後，執行 hello 筆記本**Spark Machine Learning 使用 MLlib.ipynb 食物檢查資料的預測分析**下 hello **Python**資料夾。
>
>

MLlib 是核心 Spark 程式庫之一，提供許多可用於機器學習工作的公用程式，包括具有下列用途的公用程式：

* 分類
* 迴歸
* 叢集
* 主題模型化
* 奇異值分解 (SVD) 和主體元件分析 (PCA)
* 假設測試和計算範例統計資料

## <a name="what-are-classification-and-logistic-regression"></a>分類和羅吉斯迴歸為何？
*分類*、 受歡迎的機器學習工作，是將類別目錄排序輸入的資料 hello 程序。 它是 hello 工作的分類演算法 toofigure 出 tooassign 「 標籤 」 tooinput 您提供的資料。 例如，您無法將接受股票資訊做為輸入的機器學習演算法和除以 hello 股票分成兩個類別： 應該銷售的股票和股票的地方。

羅吉斯迴歸是您用於分類的 hello 演算法。 Spark 的羅吉斯迴歸 API 可用於*二元分類*，或用來將輸入資料歸類到兩個群組之一。 如需羅吉斯迴歸的詳細資訊，請參閱 [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression)。

總而言之，羅吉斯迴歸的 hello 程序會產生*羅吉斯函數*可以輸入的向量，屬於一個群組或其他 hello 使用的 toopredict hello 機率。  

## <a name="predictive-analysis-example-on-food-inspection-data"></a>食品檢查資料的預測分析範例
在此範例中，您使用 Spark tooperform 一些預測分析上食物檢查資料 (**Food_Inspections1.csv**)，取得透過 hello[縣 （市） 的芝加哥資料入口網站](https://data.cityofchicago.org/)。 此資料集包含在芝加哥，包括每個建立的相關資訊中所進行的食物建立操作的相關資訊，hello 違規找到 （如果有的話），而且 hello hello 檢查的結果。 hello CSV 資料檔已經在 hello 與 hello 叢集相關聯的儲存體帳戶**/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**。

Hello 步驟，在您開發模型 toosee 它採用 toopass 或食物檢查會失敗。

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a>開始建置 Spark MMLib 機器學習應用程式
1. 從 hello [Azure 入口網站](https://portal.azure.com/)，從 hello 開始面板中，按一下 Spark 叢集中的 hello 磚 （如果您釘選它 toohello 開始面板）。 您也可以導覽 tooyour 叢集下的**瀏覽所有** > **HDInsight 叢集**。   
1. 從 hello Spark 叢集刀鋒視窗中，按一下 **叢集儀表板**，然後按一下 **Jupyter 筆記本**。 如果出現提示，請輸入 hello 叢集 hello 系統管理員認證。

   > [!NOTE]
   > 您也可能由下列 URL 在瀏覽器中開啟 hello 叢集到達 hello Jupyter 筆記本。 取代**CLUSTERNAME** hello 名稱，為您的叢集：
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. 建立 Notebook。 按一下 新增，然後按一下PySpark。

    ![建立 Jupyter Notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "建立新的 Jupyter Notebook")
1. 建立新的記事本，並開啟 hello 名稱 Untitled.pynb。 按一下頂端 hello hello 筆記本名稱並輸入好記的名稱。

    ![提供的名稱 hello 筆記本](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "提供 hello 筆記本的名稱")
1. 因為您建立使用 hello PySpark 核心筆記本，您不需要 toocreate 任何內容明確。 hello Spark 和 Hive 內容會自動建立，當您執行 hello 第一個程式碼儲存格。 您可以開始建置您的機器學習應用程式匯入此案例所需的 hello 型別。 toodo，hello 將游標放在位於 hello 儲存格，按**SHIFT + ENTER**。

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a>建構輸入資料框架
我們可以使用`sqlContext`tooperform 結構化資料的轉換。 hello 第一個工作是 tooload hello 範例資料 ((**Food_Inspections1.csv**)) 到 Spark SQL*資料框架*。

1. 由於 hello 未經處理資料的 CSV 格式，我們需要 toouse hello Spark 內容 toopull hello 檔案的每一行到記憶體為非結構化文字;然後，您使用 Python 的 CSV 文件庫 tooparse 每一行個別。

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. 我們已經為 RDD hello CSV 檔案。  toounderstand hello 結構描述中的 hello 資料，我們會擷取一個資料列從 hello RDD。

        inspections.take(1)

    您應該會看到類似 hello 下列輸出：

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [['413707',
          'LUNA PARK INC',
          'LUNA PARK  DAY CARE',
          '2049789',
          "Children's Services Facility",
          'Risk 1 (High)',
          '3250 W FOSTER AVE ',
          'CHICAGO',
          'IL',
          '60625',
          '09/21/2010',
          'License-Task Force',
          'Fail',
          '24. DISH WASHING FACILITIES: PROPERLY DESIGNED, CONSTRUCTED, MAINTAINED, INSTALLED, LOCATED AND OPERATED - Comments: All dishwashing machines must be of a type that complies with all requirements of hello plumbing section of hello Municipal Code of Chicago and Rules and Regulation of hello Board of Health. OBSEVERD hello 3 COMPARTMENT SINK BACKING UP INTO hello 1ST AND 2ND COMPARTMENT WITH CLEAR WATER AND SLOWLY DRAINING OUT. INST NEED HAVE IT REPAIR. CITATION ISSUED, SERIOUS VIOLATION 7-38-030 H000062369-10 COURT DATE 10-28-10 TIME 1 P.M. ROOM 107 400 W. SURPERIOR. | 36. LIGHTING: REQUIRED MINIMUM FOOT-CANDLES OF LIGHT PROVIDED, FIXTURES SHIELDED - Comments: Shielding tooprotect against broken glass falling into food shall be provided for all artificial lighting sources in preparation, service, and display facilities. LIGHT SHIELD ARE MISSING UNDER HOOD OF  COOKING EQUIPMENT AND NEED tooREPLACE LIGHT UNDER UNIT. 4 LIGHTS ARE OUT IN hello REAR CHILDREN AREA,IN hello KINDERGARDEN CLASS ROOM. 2 LIGHT ARE OUT EAST REAR, LIGHT FRONT WEST ROOM. NEED tooREPLACE ALL LIGHT THAT ARE NOT WORKING. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned. MISSING CEILING TILES WITH STAINS IN WEST,EAST, IN FRONT AREA WEST, AND BY hello 15MOS AREA. NEED tooBE REPLACED. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair. SPLASH GUARDED ARE NEEDED BY hello EXPOSED HAND SINK IN hello KITCHEN AREA | 34. FLOORS: CONSTRUCTED PER CODE, CLEANED, GOOD REPAIR, COVING INSTALLED, DUST-LESS CLEANING METHODS USED - Comments: hello floors shall be constructed per code, be smooth and easily cleaned, and be kept clean and in good repair. INST NEED tooELEVATE ALL FOOD ITEMS 6INCH OFF hello FLOOR 6 INCH AWAY FORM WALL.  ',
          '41.97583445690982',
          '-87.7107455232781',
          '(41.97583445690982, -87.7107455232781)']]
1. hello 上面的輸出為我們提供了解的 hello hello 輸入檔的結構描述。 它包含 hello 名稱每個建立、 hello 型別建立、 hello 位址、 hello 資料 hello 視察和 hello 位置，以及其他項目。 讓我們選取幾個資料行可用於預測分析而且 hello 結果分組的資料框架的我們為則使用 toocreate 暫存資料表。

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. 現在我們已有「資料框架」`df`，可讓我們據以執行分析。 我們也有名為 **CountResults**的暫存資料表。 我們包含了 hello 資料框架中感興趣的四個資料行：**識別碼**，**名稱**，**結果**，和**違規**。

    我們收到 hello 資料的小型範例：

        df.show(5)

    您應該會看到類似 hello 下列輸出：

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +------+--------------------+-------+--------------------+
        |    id|                name|results|          violations|
        +------+--------------------+-------+--------------------+
        |413707|       LUNA PARK INC|   Fail|24. DISH WASHING ...|
        |391234|       CAFE SELMARIE|   Fail|2. FACILITIES too...|
        |413751|          MANCHU WOK|   Pass|33. FOOD AND NON-...|
        |413708|BENCHMARK HOSPITA...|   Pass|                    |
        |413722|           JJ BURGER|   Pass|                    |
        +------+--------------------+-------+--------------------+

## <a name="understand-hello-data"></a>了解 hello 資料
1. 讓我們開始吧 tooget 了解我們的資料集所包含的內容。 什麼是 hello hello 中的不同值，例如**結果**資料行？

        df.select('results').distinct().show()

    您應該會看到類似 hello 下列輸出：

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +--------------------+
        |             results|
        +--------------------+
        |                Fail|
        |Business Not Located|
        |                Pass|
        |  Pass w/ Conditions|
        |     Out of Business|
        +--------------------+
1. 快速的視覺效果可以幫助我們有關 hello 發佈這些結果的原因。 我們在暫存資料表中已經有 hello 資料**CountResults**。 您可以執行下列 SQL 查詢，針對 hello 資料表 tooget hello 進一步了解如何散發 hello 結果。

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    hello `%%sql` magic 後面`-o countResultsdf`可確保 hello 查詢的 hello 輸出保存在本機上 hello Jupyter 伺服器 （通常 hello 叢集的前端節點 hello 叢集）。 hello 輸出會保存為[熊](http://pandas.pydata.org/)資料框架 hello 與指定名稱**countResultsdf**。

    您應該會看到類似 hello 下列輸出：

    ![SQL 查詢輸出](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL 查詢輸出")

    如需有關 hello`%%sql`魔法和其他適用於 hello PySpark 核心中，我們看到[Jupyter notebook Spark HDInsight 叢集上可用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)。
1. 您也可以使用 Matplotlib、 文件庫使用的資料，toocreate 繪圖 tooconstruct 視覺效果。 因為必須從本機 hello 建立 hello 圖保存**countResultsdf**資料框架，hello 程式碼片段必須以 hello 開頭`%%local`識別常數。 這可確保 hello 程式碼在本機執行 hello Jupyter 伺服器上。

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    您應該會看到類似 hello 下列輸出：

    ![Spark 機器學習應用程式輸出 - 包含五個不同檢查結果的圓形圖](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark 機器學習結果輸出")
1. 您可以看到，一項檢查可以有 5 個不同的結果：

   * 找不到該業者
   * 不合格
   * 通過
   * 有條件通過
   * 已結束營業

     讓我們開發模型，可以猜出 hello 結果的食物檢查，給定的 hello 違規。 由於羅吉斯迴歸是二元分類方法，它使意義 toogroup 我們的資料分成兩個類別：**失敗**和**傳遞**。 「 傳遞以條件 」 仍是傳遞，因此我們將 hello 模型定型，當我們認為 hello 兩個結果對等項目。 資料以 hello （「 找不到商務"或"Out of Business"） 的其他結果沒什麼用處，我們從我們的定型集移除。 因為這兩個分類還是將構成 hello 結果非常小的百分比，則這應該是關係。
1. 我們繼續進行，並將現有資料框架 (`df`) 轉換為新的資料框架，其中每項檢查都以一組「標籤-違規」來表示。 在我們的案例中，標籤 `0.0` 代表失敗，標籤 `1.0` 代表成功，標籤 `-1.0` 代表此二者以外的某種結果。 計算 hello 新的資料框架時，我們可以篩選掉的其他結果。

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    toosee 哪些 hello 標示為類似的資料，讓我們來擷取一個資料列。

        labeledData.take(1)

    您應該會看到類似 hello 下列輸出：

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of hello food establishment and all parts of hello property used in connection with hello operation of hello establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF hello FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: hello flow of air discharged from kitchen fans shall always be through a duct tooa point above hello roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT tooDINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT tooOFFICE.")]

## <a name="create-a-logistic-regression-model-from-hello-input-dataframe"></a>從輸入資料框架 hello 建立羅吉斯迴歸模型
我們最後一項工作是 tooconvert hello 標示成可由羅吉斯迴歸分析的格式資料。 hello 輸入的 tooa 羅吉斯迴歸演算法應該是一組*標籤功能向量組*，其中 hello"特徵向量 」 是表示 hello 輸入的點的數字的向量。 因此，我們需要 tooconvert hello"違規 」 資料行是半結構化，並且包含許多機器無法輕鬆地了解實際數字的任意文字 tooan 陣列中的註解。

處理自然語言的其中一個標準的機器學習方法是 tooassign 每個不同的單字"index"，然後將傳遞向量 toohello 機器學習演算法，每個索引值包含該單字的 hello 文字中的 hello 相對頻率字串。

MLlib 提供簡單的方式 tooperform 這項作業。 首先，「 token 化 」 每個違規字串 tooget hello 單字中每個字串。 然後，使用`HashingTF`tooconvert 每個設定的語彙基元接著可以傳遞的 toohello 羅吉斯迴歸演算法 tooconstruct 特徵向量成模型。 我們將使用「管線」循序執行上述所有步驟。

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-hello-model-on-a-separate-test-dataset"></a>評估 hello 模型的個別的測試資料集
我們可以使用我們稍早建立的 hello 模型太*預測*新操作的結果將會根據所觀察到的 hello 違規哪些 hello。 我們來定型此模型 hello 資料集上的**Food_Inspections1.csv**。 讓我們使用第二個資料集， **Food_Inspections2.csv**也*評估*hello 這個模式對新資料的強度。 此第二個資料集 (**Food_Inspections2.csv**) 應該已經很 hello 與 hello 叢集相關聯的預設儲存體容器中。

1. hello 下列程式碼片段會建立新的資料框架， **predictionsDf**包含 hello hello 模型所產生的預測。 hello 片段也會建立名為的暫存資料表**預測**hello 資料框架為基礎。

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    您應該會看到類似 hello 下列輸出：

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        ['id',
         'name',
         'results',
         'violations',
         'words',
         'features',
         'rawPrediction',
         'probability',
         'prediction']
1. 查看其中一個 hello 預測。 執行此程式碼片段：

        predictionsDf.take(1)

   沒有 hello hello 測試資料集中的第一個項目的預測。
1. hello`model.transform()`方法適用於 hello 相同轉換 tooany 新的資料與 hello 相同的結構描述，並且已到達 tooclassify hello 資料的方式來預測。 我們可以執行一些簡單的統計資料 tooget 我們預測的精確度如何了解：

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    hello 輸出看起來像下列 hello:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    使用羅吉斯迴歸與 Spark 提供精確的模型，以英文違規描述與給定的商務是否會傳遞或失敗食物檢查之間的 hello 關聯性。

## <a name="create-a-visual-representation-of-hello-prediction"></a>建立 hello 預測的視覺表示法
我們現在可以建構最終的視覺效果 toohelp 我們理解 hello 的這項測試的結果。

1. 我們一開始擷取 hello 不同預測和結果 hello**預測**稍早建立的暫存資料表。 hello 下列查詢不同的 hello 輸出為*true_positive*， *false_positive*， *true_negative*，和*false_negative*。 Hello 在查詢中以下，我們關閉視覺效果使用`-q`並也儲存 hello 輸出 (使用`-o`) 做為資料框架，然後可與 hello`%%local`識別常數。

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. 最後，使用下列程式碼片段 toogenerate hello 繪圖使用 hello **Matplotlib**。

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    您應該會看到下列輸出的 hello:

    ![Spark 機器學習應用程式輸出 - 包含失敗食品檢查百分比的圓形圖。](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark 機器學習結果輸出")

    在此圖中，「 正面 」 的結果是指失敗 toohello 食物檢查，而負的結果則是指 tooa 傳遞檢查。

## <a name="shut-down-hello-notebook"></a>關閉 hello 筆記本
當您完成執行 hello 應用程式之後，您應該關閉 hello 筆記本 toorelease hello 資源。 toodo 的話，從 hello**檔案**hello 筆記本功能表按一下**關閉而停止**。 這關閉，並關閉 hello 筆記型電腦。

## <a name="seealso"></a>另請參閱
* [概觀：Azure HDInsight 上的 Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>案例
* [Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析](hdinsight-apache-spark-use-bi-tools.md)
* [Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式](hdinsight-apache-spark-eventhub-streaming.md)
* [使用 HDInsight 中的 Spark 進行網站記錄分析](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>建立及執行應用程式
* [使用 Scala 建立獨立應用程式](hdinsight-apache-spark-create-standalone-application.md)
* [利用 Livy 在 Spark 叢集上遠端執行作業](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>工具和擴充功能
* [HDInsight 工具外掛程式用於 IntelliJ 概念 toocreate 並提交 Spark Scala 應用程式](hdinsight-apache-spark-intellij-tool-plugin.md)
* [從遠端使用 HDInsight Tools 外掛程式 IntelliJ 概念 toodebug Spark 應用程式](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [搭配 Jupyter Notebook 使用外部套件](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>管理資源
* [管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源](hdinsight-apache-spark-resource-manager.md)
* [追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業](hdinsight-apache-spark-job-debugging.md)
