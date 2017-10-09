---
title: "aaaAnalyze 和程序的 JSON 文件在 HDInsight 的 Hive |Microsoft 文件"
description: "了解 toouse JSON 文件，並加以分析使用 HDInsight 中的登錄區。"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e17794e8-faae-4264-9434-67f61ea78f13
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2017
ms.author: jgao
ms.openlocfilehash: b4b20172e8553f91a446615dc52f2ea2ef24cd04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="process-and-analyze-json-documents-using-hive-in-hdinsight"></a>使用 HDInsight 中的 Hive 處理並分析 JSON 文件

深入了解如何 tooprocess 和分析 JSON 檔案使用 HDInsight 中的登錄區。 hello 教學課程中，會使用下列 JSON 文件的 hello:

    {
        "StudentId": "trgfg-5454-fdfdg-4346",
        "Grade": 7,
        "StudentDetails": [
            {
                "FirstName": "Peggy",
                "LastName": "Williams",
                "YearJoined": 2012
            }
        ],
        "StudentClassCollection": [
            {
                "ClassId": "89084343",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "High",
                "Score": 93,
                "PerformedActivity": false
            },
            {
                "ClassId": "78547522",
                "ClassParticipation": "NotSatisfied",
                "ClassParticipationRank": "None",
                "Score": 74,
                "PerformedActivity": false
            },
            {
                "ClassId": "78675563",
                "ClassParticipation": "Satisfied",
                "ClassParticipationRank": "Low",
                "Score": 83,
                "PerformedActivity": true
            }
        ]
    }

hello 檔案，請參閱wasb://processjson@hditutorialdata.blob.core.windows.net/。 如需關於搭配 HDInsight 使用 Azure Blob 儲存體的詳細資訊，請參閱[在 HDInsight 上搭配 Hadoop 使用 HDFS 相容的 Azure Blob 儲存體](hdinsight-hadoop-use-blob-storage.md)。 您可以複製您的叢集的 hello 檔案 toohello 預設容器。

在本教學課程中，您可以使用 hello Hive 主控台。  開啟 hello Hive 主控台的指示，請參閱[的上具有遠端桌面 HDInsight Hadoop Hive 使用](hdinsight-hadoop-use-hive-remote-desktop.md)。

## <a name="flatten-json-documents"></a>簡維 JSON 文件
hello 下一節中所列的 hello 方法需要單一資料列中的 hello JSON 文件。 因此，您必須扁平化 hello JSON 文件 tooa 字串。 如果已扁平化 JSON 文件，可以略過此步驟，並繼續分析 JSON 資料直線 toohello 下一節。

    DROP TABLE IF EXISTS StudentsRaw;
    CREATE EXTERNAL TABLE StudentsRaw (textcol string) STORED AS TEXTFILE LOCATION "wasb://processjson@hditutorialdata.blob.core.windows.net/";

    DROP TABLE IF EXISTS StudentsOneLine;
    CREATE EXTERNAL TABLE StudentsOneLine
    (
      json_body string
    )
    STORED AS TEXTFILE LOCATION '/json/students';

    INSERT OVERWRITE TABLE StudentsOneLine
    SELECT CONCAT_WS(' ',COLLECT_LIST(textcol)) AS singlelineJSON
          FROM (SELECT INPUT__FILE__NAME,BLOCK__OFFSET__INSIDE__FILE, textcol FROM StudentsRaw DISTRIBUTE BY INPUT__FILE__NAME SORT BY BLOCK__OFFSET__INSIDE__FILE) x
          GROUP BY INPUT__FILE__NAME;

    SELECT * FROM StudentsOneLine

hello 未經處理的 JSON 檔案是位於 **wasb://processjson@hditutorialdata.blob.core.windows.net/** 。 hello *StudentsRaw* Hive 資料表點 toohello 原始非扁平化的 JSON 文件。

hello *StudentsOneLine* Hive 資料表將 hello 資料儲存在 hello HDInsight 預設檔案系統 hello */json/學生/*路徑。

hello INSERT 陳述式會填入 hello StudentOneLine 資料表與 hello 扁平化 JSON 資料。

hello SELECT 陳述式應該只傳回一個資料列。

以下是 hello hello SELECT 陳述式的輸出：

![簡維 hello JSON 文件。][image-hdi-hivejson-flatten]

## <a name="analyze-json-documents-in-hive"></a>在 Hive 中分析 JSON 文件
Hive 提供三種不同機制 toorun 查詢 JSON 文件：

* 使用 hello GET\_JSON\_物件 UDF （使用者定義函式）
* 使用 hello JSON_TUPLE UDF
* 使用自訂 SerDe
* 使用 Python 或其他語言撰寫您自己的 UDF。 請參閱[這篇文章][hdinsight-python]，了解如何使用 Hive 執行您自己的 Python 程式碼。

### <a name="use-hello-getjsonobject-udf"></a>使用 hello GET\_JSON_OBJECT UDF
Hive 提供的內建 UDF 稱為 [get json objec](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object)，可在執行階段期間執行 JSON 查詢。 這個方法會採用兩個引數 – hello 資料表名稱和方法名稱，其具有 hello 扁平化 JSON 文件和 hello JSON 欄位需要 toobe 剖析。 讓我們看看此 UDF 的運作方式範例 toosee。

取得 hello 名字和每個學生的姓氏

    SELECT
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.FirstName'),
      GET_JSON_OBJECT(StudentsOneLine.json_body,'$.StudentDetails.LastName')
    FROM StudentsOneLine;

在主控台視窗中執行此查詢時，以下是 hello 輸出。

![get_json_object UDF][image-hdi-hivejson-getjsonobject]

有一些限制的 hello get json_object UDF。

* Hello 查詢中的每個欄位需要重新剖析 hello 查詢，因為它會影響 hello 效能。
* 取得\_JSON_OBJECT() 傳回 hello 陣列的字串表示。 tooconvert 此陣列 tooa Hive 陣列，您有 toouse 規則運算式 tooreplace hello 方括號 '[' 和']'，然後同時呼叫分割 tooget hello 陣列。

這就是為什麼 hello Hive wiki 建議使用 json_tuple。  

### <a name="use-hello-jsontuple-udf"></a>使用 hello JSON_TUPLE UDF
Hive 所提供的另一個 UDF 稱為 [json_tuple](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-json_tuple)，其效能比 [get_ json _object](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-get_json_object) 更高。 這個方法會採用一組索引鍵和 JSON 字串，並使用一個函式傳回值的 tuple。 hello 下列查詢會傳回 hello 學生識別碼以及 hello 等級 hello JSON 文件：

    SELECT q1.StudentId, q1.Grade
      FROM StudentsOneLine jt
      LATERAL VIEW JSON_TUPLE(jt.json_body, 'StudentId', 'Grade') q1
        AS StudentId, Grade;

此指令碼 hello Hive 主控台中的 hello 輸出：

![json_tuple UDF][image-hdi-hivejson-jsontuple]

JSON\_TUPLE 使用 hello[橫向檢視](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView)登錄區，可讓 json 語法\_tuple toocreate 藉由套用 hello UDT 函式 tooeach 資料表的資料列 hello 原始虛擬資料表。  因為重複 hello 變得難以的複雜 Json 使用橫向 檢視。 此外，JSON_TUPLE 無法處理巢狀 JSON。

### <a name="use-custom-serde"></a>使用自訂 SerDe
SerDe hello 剖析巢狀的 JSON 文件的最佳選擇，它可讓您 toodefine hello JSON 結構描述，以及使用 hello 結構描述 tooparse hello 文件。 在本教學課程中，您使用下列其中一個 hello 已開發的常見 SerDe[蘇 Congiu](https://github.com/rcongiu)。

**toouse hello 自訂 SerDe:**

1. 安裝 [Java SE 開發套件 7u55 JDK 1.7.0_55](http://www.oracle.com/technetwork/java/javase/downloads/java-archive-downloads-javase7-521261.html#jdk-7u55-oth-JPR)。 如果您要使用的 HDInsight hello Windows 部署 toobe，選擇 hello Windows X64 版的 hello JDK
   
   > [!WARNING]
   > JDK 1.8 不適用於此 SerDe。
   > 
   > 
   
    Hello 安裝完成之後，加入新的使用者環境變數：
   
   1. 開啟**檢視進階系統設定**從 Windows 囉 」 畫面。
   2. 按一下 [ **環境變數**]。  
   3. 加入新**JAVA_HOME**環境變數指向太**C:\Program Files\Java\jdk1.7.0_55**或 JDK 安裝的任一處。
      
      ![為 JDK 設定正確的組態值][image-hdi-hivejson-jdk]
2. 安裝 [Maven 3.3.1](http://mirror.olnevhost.net/pub/apache/maven/maven-3/3.3.1/binaries/apache-maven-3.3.1-bin.zip)
   
    新增 hello bin 資料夾 tooyour 路徑移 tooControl 面板--> 您帳戶的環境變數的編輯 hello 系統變數。 hello 下列螢幕擷取畫面顯示您如何 toodo 這。
   
    ![設定 Maven][image-hdi-hivejson-maven]
3. 從複製 hello 專案[Hive-JSON-SerDe](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master) github 網站。 您可以按一下 hello"Download Zip 」 按鈕 hello 下列螢幕擷取畫面所示。
   
    ![複製 hello 專案][image-hdi-hivejson-serde]

4： 您已下載此套件，然後類型 「 mvn 封裝 」 go toohello 資料夾。 這應該建立 hello 必要 jar 檔案，然後您可以複製移轉 toohello 叢集。

5: hello hello 封裝的下載程式的根資料夾下，移至 toohello 目標資料夾。 上傳 hello json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar 檔案 toohead 位在叢集的節點。 通常 hello hive 二進位資料夾下將： C:\apps\dist\hive-0.13.0.2.1.11.0-2316\bin 或類似的項目。

6： 在 hello hive 提示字元中輸入 「 新增 jar /path/to/json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar 」。 由於在這個案例中，hello jar hello C:\apps\dist\hive-0.13.x\bin 資料夾中，我可以直接加入 hello jar hello 名稱所示：

    add jar json-serde-1.1.9.9-Hive13-jar-with-dependencies.jar;

   ![加入 JAR tooyour 專案][image-hdi-hivejson-addjar]

現在，您就準備好 toouse hello SerDe toorun 查詢 hello JSON 文件。

陳述式之後的 hello 會具有定義的結構描述中建立資料表：

    DROP TABLE json_table;
    CREATE EXTERNAL TABLE json_table (
      StudentId string,
      Grade int,
      StudentDetails array<struct<
          FirstName:string,
          LastName:string,
          YearJoined:int
          >
      >,
      StudentClassCollection array<struct<
          ClassId:string,
          ClassParticipation:string,
          ClassParticipationRank:string,
          Score:int,
          PerformedActivity:boolean
          >
      >
    ) ROW FORMAT SERDE 'org.openx.data.jsonserde.JsonSerDe'
    LOCATION '/json/students';

toolist hello 名字和姓氏 hello 學生

    SELECT StudentDetails.FirstName, StudentDetails.LastName FROM json_table;

以下是從 hello Hive 主控台 hello 結果。

![SerDe 查詢 1][image-hdi-hivejson-serde_query1]

toocalculate hello 加總的 hello JSON 文件的分數

    SELECT SUM(scores)
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as scores;

上述查詢會使用 hello[橫向檢視分裂](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+LateralView)UDF tooexpand hello 分數的陣列，以便可以加總。

以下是 hello hello Hive 主控台輸出。

![SerDe 查詢 2][image-hdi-hivejson-serde_query2]

這會使指定的學生 toofind 具有計分超過 80 點：

    SELECT  
      jt.StudentClassCollection.ClassId
    FROM json_table jt
      lateral view explode(jt.StudentClassCollection.Score) collection as score  where score > 80;

hello 上述查詢會傳回不同於 get Hive 陣列\_json\_物件，傳回的字串。

![SerDe 查詢 3][image-hdi-hivejson-serde_query3]

如果您想 tooskil 格式不正確的 JSON，再為說明中的 hello [wiki 頁面](https://github.com/sheetaldolas/Hive-JSON-Serde/tree/master)此 SerDe 的一種，輸入下列程式碼的 hello:  

    ALTER TABLE json_table SET SERDEPROPERTIES ( "ignore.malformed.json" = "true");




## <a name="summary"></a>摘要
結論，您所選擇的登錄區中的 JSON 運算子 hello 類型取決於您的案例。 如果您有簡單的 JSON 文件，因此您上只能有一個欄位 toolook-您可以選擇 toouse hello Hive UDF get\_json\_物件。 如果您最多有一個以上的索引鍵 toolook 時，您可以使用 json_tuple。 如果您有巢狀文件時，您應該使用 JSON SerDe hello。

## <a name="next-steps"></a>後續步驟

如需其他相關文章，請參閱

* [在 HDInsight tooanalyze 範例 Apache log4j 檔案中的 Hadoop 使用 Hive 和 HiveQL](hdinsight-use-hive.md)
* [在 HDInsight 中使用 Hive 分析航班延誤資料](hdinsight-analyze-flight-delay-data.md)
* [在 HDInsight 中使用 Hive 分析 Twitter 資料](hdinsight-analyze-twitter-data.md)
* [使用 Azure Cosmos DB 和 HDInsight 執行 Hadoop 工作](../documentdb/documentdb-run-hadoop-with-hdinsight.md)

[hdinsight-python]: hdinsight-python.md

[image-hdi-hivejson-flatten]: ./media/hdinsight-using-json-in-hive/flatten.png
[image-hdi-hivejson-getjsonobject]: ./media/hdinsight-using-json-in-hive/getjsonobject.png
[image-hdi-hivejson-jsontuple]: ./media/hdinsight-using-json-in-hive/jsontuple.png
[image-hdi-hivejson-jdk]: ./media/hdinsight-using-json-in-hive/jdk.png
[image-hdi-hivejson-maven]: ./media/hdinsight-using-json-in-hive/maven.png
[image-hdi-hivejson-serde]: ./media/hdinsight-using-json-in-hive/serde.png
[image-hdi-hivejson-addjar]: ./media/hdinsight-using-json-in-hive/addjar.png
[image-hdi-hivejson-serde_query1]: ./media/hdinsight-using-json-in-hive/serde_query1.png
[image-hdi-hivejson-serde_query2]: ./media/hdinsight-using-json-in-hive/serde_query2.png
[image-hdi-hivejson-serde_query3]: ./media/hdinsight-using-json-in-hive/serde_query3.png
[image-hdi-hivejson-serde_result]: ./media/hdinsight-using-json-in-hive/serde_result.png
