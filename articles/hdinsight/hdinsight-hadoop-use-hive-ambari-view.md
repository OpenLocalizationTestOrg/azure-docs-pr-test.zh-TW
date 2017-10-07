---
title: "與 HDInsight (Hadoop)-Azure 上的登錄區 aaaUse Ambari 檢視 toowork |Microsoft 文件"
description: "了解 toouse hello Hive 檢視從您網頁瀏覽器 toosubmit Hive 查詢的方式。 hello hive 控制檔的檢視是的 hello Ambari Web UI 隨附以 Linux 為基礎的 HDInsight 叢集的一部分。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1abe9104-f4b2-41b9-9161-abbc43de8294
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: f9a77b652e70d34a0ff9165fbb8c2e16d3401ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-hive-view-with-hadoop-in-hdinsight"></a>使用 hello HDInsight 中的 Hadoop hive 控制檔的檢視

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

了解如何 toorun Hive 查詢使用 Ambari hive 控制檔的檢視。 Ambari 是隨著以 Linux 為基礎的 HDInsight 叢集提供的管理和監視公用程式。 Ambari 透過提供的 hello 功能之一是 Web UI，它可以是使用的 toorun Hive 查詢。

> [!NOTE]
> Ambari 有許多本文未討論到的功能。 如需詳細資訊，請參閱[管理 HDInsight 叢集使用 hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)。

## <a name="prerequisites"></a>必要條件

* 以 Linux 為基礎的 HDInsight 叢集。 如需建立叢集的相關資訊，請參閱[開始使用以 Linux 為基礎的 HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)。

> [!IMPORTANT]
> 本文件中的 hello 步驟需要使用 Linux 的 HDInsight 叢集。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

## <a name="open-hello-hive-view"></a>開啟 hello 登錄區檢視

您可以從 Azure 入口網站; hello 的 Ambari 檢視選取您的 HDInsight 叢集，然後選取**Ambari 檢視**從 hello**快速連結**> 一節。

![hello 入口網站的快速連結 區段](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

從 hello 清單中的檢視，選取 hello __Hive 檢視__。

![hello 所選取的登錄區檢視](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> 在存取 Ambari，即提示的 tooauthenticate toohello 站台。 輸入 hello admin (預設`admin`) 帳戶名稱和您建立時使用的密碼 hello 叢集。

您應該會看到下列映像頁面類似 toohello:

![Hello hello 登錄區檢視的查詢工作表的映像](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <a name="hivequery"></a>執行查詢

toorun hive 查詢，使用 hello hello 登錄區檢視中的下列步驟。

1. 從 hello__查詢__索引標籤中，貼上下列 HiveQL 陳述式 hello 工作表中的 hello:

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    這些陳述式會執行下列動作的 hello:

   * `DROP TABLE`-刪除 hello 資料表與 hello 資料檔，萬一 hello 資料表已經存在。

   * `CREATE EXTERNAL TABLE` - 在 Hive 中建立新的「外部」資料表。
   外部資料表儲存區中的 hello 資料表定義。 hello 資料會保留在 hello 原始位置。

   * `ROW FORMAT`的 hello 資料格式化方式。 在此情況下，每個記錄檔中的 hello 欄位會以空格分隔。

   * `STORED AS TEXTFILE LOCATION`-Hello 儲存資料，並儲存成文字。

   * `SELECT`-選取其中的資料行 t4 包含 hello 值 [錯誤] 的所有資料列計數。

     > [!NOTE]
     > 當您希望產生 hello 由外部來源更新基礎資料 toobe，應該使用外部資料表。 例如，自動化的資料上傳程序，或透過其他 MapReduce 作業。 卸除的外部資料表沒有*不*刪除 hello 資料、 hello 資料表定義。

    > [!IMPORTANT]
    > 保留 hello__資料庫__選取項目在__預設__。 本文件中的 hello 範例會使用隨附 HDInsight hello 預設資料庫。

2. toostart hello 查詢，使用 hello **Execute**下方 hello 工作表 按鈕。 會呈現橙色和 hello 文字變更太**停止**。

3. Hello 查詢完成時，一旦 hello**結果**索引標籤會顯示 hello hello 作業結果。 下列文字的 hello 是 hello hello 查詢結果：

        sev       cnt
        [ERROR]   3

    hello**記錄** 索引標籤可以是使用的 tooview hello 工作所建立的 hello 記錄資訊。

   > [!TIP]
   > hello**將結果儲存**中 hello 上方的下拉式清單對話方塊方 hello**查詢程序結果**區段可讓您 toodownload 或儲存結果。

4. 選取 hello 前四行的這項查詢，然後選取**Execute**。 請注意，沒有結果 hello 作業完成時。 使用 hello **Execute**按鈕時 hello 查詢的一部分時，才執行 hello 選陳述式選取。 在此情況下，hello 選取範圍沒有包含 hello 最終的陳述式會從 hello 資料表擷取資料列。 如果您選取只在該行，並使用**Execute**，您應該會看到 hello 預期結果。

5. tooadd 工作表中，使用 hello**新工作表**在 hello hello 底部的按鈕**查詢編輯器**。 Hello 新工作表中輸入下列 HiveQL 陳述式的 hello:

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  這些陳述式會執行下列動作的 hello:

   * **CREATE TABLE IF NOT EXISTS** - 建立資料表 (如果不存在)。 因為 hello**外部**不是關鍵字，會建立內部資料表。 內部資料表會儲存在 hello Hive 資料倉儲和 Hive 完全管理。 不同於外部資料表，卸除內部資料表，將會刪除 hello 基礎資料。

   * **儲存 AS ORC** -hello 資料儲存最佳化的資料列單欄式 (ORC) 格式。 ORC 是高度最佳化且有效率的 Hive 資料儲存格式。

   * **INSERT OVERWRITE ...選取**-選取資料列從 hello **log4jLogs**包含資料表`[ERROR]`，然後插入 hello 資料到 hello 和**錯誤記錄檔**資料表。

     使用 hello **Execute**按鈕 toorun 此查詢。 hello**結果**hello 查詢傳回零個資料列時 索引標籤不包含任何資訊。 hello 狀態應顯示為**SUCCEEDED** hello 查詢完成後。

### <a name="visual-explain"></a>視覺解說

toodisplay 視覺效果的 hello 查詢計畫中，選取 hello **Visual 說明**下方 hello 工作表的索引標籤。

hello **Visual 說明**hello 查詢的檢視可能有助於瞭解 hello 流向複雜的查詢。 您可以檢視此檢視的文字對等項目使用 hello**解釋**hello 查詢編輯器中的按鈕。

### <a name="tez-ui"></a>Tez UI

toodisplay hello Tez UI hello 查詢中，選取 hello **Tez**下方 hello 工作表的索引標籤。

> [!IMPORTANT]
> Tez 是未使用的 tooresolve 所有查詢。 您不需要使用 Tez 便可解析許多查詢。 

如果 Tez 使用的 tooresolve hello 查詢導向非循環圖 (DAG) 會顯示的 hello。 如果您需要 tooview hello DAG 的查詢，您已在過去，hello 執行或偵錯 hello Tez 程序，使用 hello [Tez 檢視](hdinsight-debug-ambari-tez-view.md)改為。

## <a name="view-job-history"></a>檢視工作歷程記錄

hello__作業__索引標籤會顯示的 Hive 查詢歷程記錄。

![Hello 作業歷程記錄的映像](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a>資料庫資料表

您可以使用 hello__資料表__toowork Hive 資料庫內的資料表與索引標籤上。

![Hello 資料表索引標籤的映像](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a>儲存的查詢

從 hello 查詢索引標籤上，您可以選擇儲存查詢。 儲存之後，您可以重複使用 hello 查詢從 hello__儲存查詢__ 索引標籤。

![[儲存的查詢] 索引標籤影像](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a>使用者定義函式

您也可以透過使用者定義函數 (UDF) 擴充 Hive。 UDF 可讓您 tooimplement 功能或 HiveQL 不容易模型化的邏輯。

hello UDF 索引標籤頂端的 hello Hive 檢視 hello 可讓您 toodeclare 和儲存一組的 Udf。 這些 Udf 可以搭配 hello**查詢編輯器**。

![[UDF] 索引標籤影像](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

一旦您加入 UDF toohello hive 控制檔 檢視中，**插入 udf**按鈕會出現在 hello 底部 hello**查詢編輯器**。 選取此項目會顯示 hello hello hive 控制檔 檢視中定義的 Udf 的下拉式清單。 選取的 UDF 會加入下列 HiveQL 陳述式 tooyour 查詢 tooenable hello UDF。

例如，如果您已經定義 UDF 以 hello 下列屬性：

* 資源名稱：myudfs

* 資源路徑︰/myudfs.jar

* UDF 名稱：myawesomeudf

* UDF 類別名稱：com.myudfs.Awesome

使用 hello**插入 udf**按鈕會顯示名為的項目**myudfs**，與另一個下拉式清單的每個 UDF 定義該資源。 在此案例中為 **myawesomeudf**。 選取此項目就會加入下列 toohello 開頭 hello 查詢 hello:

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

然後，您可以在查詢中使用 hello UDF。 例如： `SELECT myawesomeudf(name) FROM people;`。

如需有關如何使用 Udf 與 HDInsight 上的登錄區的詳細資訊，請參閱下列文件的 hello:

* [在 HDInsight 中搭配 Hive 與 Pig 使用 Python](hdinsight-python.md)
* [如何自訂的 Hive UDF tooHDInsight tooadd](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a>Hive 設定

設定可以是使用的 toochange Hive 的各種設定。 例如，變更 Hive 從 Tez （hello 預設值） tooMapReduce hello 執行引擎。

## <a id="nextsteps"></a>接續步驟

如需 HDInsight 中 Hive 的一般資訊：

* [搭配使用 Hive 與 HDInsight 上的 Hadoop](hdinsight-use-hive.md)

如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：

* [搭配使用 Pig 與 HDInsight 上的 Hadoop](hdinsight-use-pig.md)
* [搭配使用 MapReduce 與 HDInsight 上的 Hadoop](hdinsight-use-mapreduce.md)
