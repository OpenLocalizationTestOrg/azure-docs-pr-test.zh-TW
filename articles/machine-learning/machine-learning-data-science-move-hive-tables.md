---
title: "aaaCreate Hive 資料表和資料從 Azure Blob 儲存體載入 |Microsoft 文件"
description: "建立登錄區資料表，並載入 blob toohive 資料表中的資料"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: cff9280d-18ce-4b66-a54f-19f358d1ad90
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 09622972bcac31c2971858393a8340f24e4b7390
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-hive-tables-and-load-data-from-azure-blob-storage"></a>建立 Hive 資料表，並從 Azure Blob 儲存體載入資料
本主題會顯示泛型 Hive 查詢，這類查詢可建立 Hive 資料表，並從 Azure Blob 儲存體載入資料。 在分割區資料表，使用 hello 最佳化的資料列單欄式 (ORC) 格式化 tooimprove 查詢效能，也會提供一些指引。

這**功能表**連結 tootopics 描述 tooingest 資料可以儲存和處理期間 hello 資料的目標環境 hello 小組資料科學程序 (TDSP) 的方式。

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

## <a name="prerequisites"></a>必要條件
本文假設您已經：

* 建立 Azure 儲存體帳戶。 如需相關指示，請參閱[關於 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。
* 自訂的 Hadoop 叢集以 hello HDInsight 服務使用者佈建。  如需指示，請參閱 [自訂適用於進階分析的 Azure HDInsight Hadoop 叢集](machine-learning-data-science-customize-hadoop-cluster.md)。
* 啟用遠端存取 toohello 叢集中，登入，並開啟 hello Hadoop 命令列主控台。 如果您需要的指示，請參閱[存取 hello 的 Hadoop 叢集前端節點](machine-learning-data-science-customize-hadoop-cluster.md#headnode)。

## <a name="upload-data-tooazure-blob-storage"></a>上傳資料 tooAzure blob 儲存體
如果您建立 Azure 虛擬機器中提供的 hello 指示[設定 Azure 虛擬機器執行進階分析](machine-learning-data-science-setup-virtual-machine.md)，此指令碼檔案應該已經下載的 toohello *c:\\使用者\\\<使用者名\>\\文件\\資料科學指令碼*hello 虛擬機器上的目錄。 這些 Hive 查詢只需要您插入您自己的資料結構描述和準備送出 hello 適當欄位 toobe 中的 Azure blob 儲存體設定中。

我們假設 hello Hive 資料表的資料在**未壓縮**表格式格式和 hello 資料已經上傳 toohello 預設 （或其他 tooan） hello hello Hadoop 叢集所使用的儲存體帳戶的容器。

如果您想在 hello toopractice **NYC 計程車路線資料**，您需要：

* **下載**hello 24 [NYC 計程車路線資料](http://www.andresmh.com/nyctaxitrips)檔案 （12 個路線檔案和 12 個價位檔案）
* **解壓縮** 為 .csv 檔案，然後
* **上傳**它們 toohello 預設 （或適當的容器） 的 hello hello hello 中所述的程序所建立的 Azure 儲存體帳戶[自訂 Azure HDInsight Hadoop 叢集以提供進階分析程序和技術](machine-learning-data-science-customize-hadoop-cluster.md)主題。 hello 程序 tooupload hello.csv 檔案 toohello 預設容器 hello 儲存體帳戶上的可以找到此[頁面](machine-learning-data-science-process-hive-walkthrough.md#upload)。

## <a name="submit"></a>如何 toosubmit Hive 查詢
您可以使用下列方法來提交 Hive 查詢：

1. [透過 Hadoop 叢集前端節點中的 Hadoop 命令列提交 Hive 查詢](#headnode)
2. [提交 Hive 查詢以 hello 登錄區編輯器](#hive-editor)
3. [利用 Azure PowerShell 命令提交 Hive 查詢](#ps)

Hive 查詢類似 SQL。 如果您熟悉 SQL，您可能會發現 hello [SQL 使用者小工作表的 Hive](http://hortonworks.com/wp-content/uploads/2013/05/hql_cheat_sheet.pdf)很有用。

當提交 Hive 查詢，您也可以控制 hello 目的地的 Hive 查詢從 hello 輸出無論 hello 螢幕或 tooa 本機檔案上 hello 前端節點或 tooan Azure blob。

### <a name="headnode"></a> 1.透過 Hadoop 叢集前端節點中的 Hadoop 命令列提交 Hive 查詢
如果 hello Hive 查詢就會很複雜，提交直接在 hello hello Hadoop 叢集前端節點通常會導致 toofaster 返回比提交 hive 控制檔的編輯器或 Azure PowerShell 指令碼。

登入 toohello hello Hadoop 叢集前端節點，開啟 hello Hadoop 命令列桌面上 hello hello 前端節點，然後輸入命令`cd %hive_home%\bin`。

Hello Hadoop 命令列中有三種方式 toosubmit Hive 查詢：

* 直接
* 使用 .hql 檔案
* 以 hello Hive 命令主控台

#### <a name="submit-hive-queries-directly-in-hadoop-command-line"></a>在 Hadoop 命令列中直接提交 Hive 查詢。
您可以執行的命令，像`hive -e "<your hive query>;`toosubmit 簡單 Hive 查詢直接在 Hadoop 命令列。 以下是的範例，其中 hello 紅色方塊外框 hello 命令送出 hello Hive 查詢，而 hello hello Hive 查詢的綠色方塊外框 hello 輸出。

![建立工作區](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-1.png)

#### <a name="submit-hive-queries-in-hql-files"></a>提交 .hql 檔案中的 Hive 查詢。
當 hello Hive 查詢較為複雜，而且擁有多行時，並不實用編輯命令列或 Hive 命令主控台中的查詢。 替代方式是 toouse 文字編輯器中的 hello Hadoop 叢集 toosave hello Hive 查詢.hql 檔案中的 hello 前端節點的本機目錄中的 hello 前端節點。 然後可以使用 hello 送出 hello.hql 檔案中的 hello Hive 查詢`-f`引數，如下所示：

    hive -f "<path toohello .hql file>"

![建立工作區](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-3.png)

**隱藏 Hive 查詢的進度狀態畫面顯示**

根據預設，Hive 查詢提交的 Hadoop 命令列中之後, hello hello Map/Reduce 作業進度會列印螢幕上。 toosuppress hello hello Map/Reduce 作業進度的螢幕列印，您可以使用引數`-S`(大寫為"S") 中 hello 命令列，如下所示：

    hive -S -f "<path toohello .hql file>"
.    hive -S -e "<Hive queries>"

#### <a name="submit-hive-queries-in-hive-command-console"></a>在 Hive 命令主控台中提交 Hive 查詢。
您可以執行命令，以也先輸入 hello Hive 命令主控台`hive`在 Hadoop 命令列，然後提交 Hive 命令主控台中的 Hive 查詢。 範例如下。 在此範例中，hello 兩個紅色方塊反白顯示 hello 命令會使用 tooenter hello Hive 命令主控台中，而且 hello Hive 查詢提交 Hive 命令主控台中，分別。 hello 綠色方塊反白顯示 hello hello Hive 查詢的輸出。

![建立工作區](./media/machine-learning-data-science-move-hive-tables/run-hive-queries-2.png)

hello 前面的範例直接輸出畫面上 hello Hive 查詢的結果。 您也可以撰寫 hello 前端節點或 tooan Azure blob 上的 hello 輸出 tooa 本機檔案。 然後，您可以使用其他工具 toofurther 分析 hello 的 Hive 查詢的輸出。

**輸出 Hive 查詢結果 tooa 本機檔案。**
toooutput Hive 查詢結果 tooa 本機目錄 hello 前端節點上的，您有 toosubmit hello Hive 查詢 hello Hadoop 命令列中，如下所示：

    hive -e "<hive query>" > <local path in hello head node>

在下列範例的 hello，Hive 查詢的 hello 輸出寫入檔案`hivequeryoutput.txt`目錄中`C:\apps\temp`。

![建立工作區](./media/machine-learning-data-science-move-hive-tables/output-hive-results-1.png)

**輸出 Hive 查詢的結果 tooan Azure blob**

您也可以輸出 hello Hive 查詢的結果 tooan hello hello Hadoop 叢集的預設容器內的 Azure blob。 這個 hello Hive 查詢如下所示：

    insert overwrite directory wasb:///<directory within hello default container> <select clause from ...>

在下列範例的 hello，Hive 查詢 hello 輸出寫入 tooa blob 目錄`queryoutputdir`hello hello Hadoop 叢集的預設容器內。 在這裡，您只需要 tooprovide hello 目錄名稱，不含 hello blob 名稱。 如果您同時提供目錄和 Blob 名稱 (例如 `wasb:///queryoutputdir/queryoutput.txt`)，則會擲回錯誤。

![建立工作區](./media/machine-learning-data-science-move-hive-tables/output-hive-results-2.png)

如果您開啟 hello 預設容器，使用 Azure 儲存體總管 hello Hadoop 叢集，您可以看到 hello Hive 查詢的 hello 的輸出 hello 遵循圖所示。 您可以套用 hello 篩選器 （以紅色方塊反白顯示） tooonly 擷取 hello blob 名稱中指定的字元。

![建立工作區](./media/machine-learning-data-science-move-hive-tables/output-hive-results-3.png)

### <a name="hive-editor"></a> 2.提交 Hive 查詢以 hello 登錄區編輯器
您也可以輸入 hello 表單的 URL，使用 hello 查詢主控台 （登錄區編輯器） *https://&#60;Hadoop 叢集名稱 >.azurehdinsight.net/Home/HiveEditor*在網頁瀏覽器。 您必須登入 hello，請參閱此主控台，因此您需要以下 Hadoop 叢集認證。

### <a name="ps"></a> 3.利用 Azure PowerShell 命令提交 Hive 查詢
您也可以使用 PowerShell toosubmit Hive 查詢。 如需指示，請參閱 [使用 PowerShell 提交 Hive 工作](../hdinsight/hdinsight-hadoop-use-hive-powershell.md)。

## <a name="create-tables"></a>建立 Hive 資料庫和資料表
hello Hive 查詢中共用 hello [GitHub 儲存機制](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_db_tbls_load_data_generic.hql)而且可以從該處下載。

以下是建立的 Hive 資料表的 hello Hive 查詢。

    create database if not exists <database name>;
    CREATE EXTERNAL TABLE if not exists <database name>.<table name>
    (
        field1 string,
        field2 int,
        field3 float,
        field4 double,
        ...,
        fieldN string
    )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' lines terminated by '<line separator>'
    STORED AS TEXTFILE LOCATION '<storage location>' TBLPROPERTIES("skip.header.line.count"="1");

以下是 hello 的描述，您需要在 tooplug hello 欄位以及其他組態：

* **&#60; 資料庫名稱 >**: hello 的 toocreate hello 資料庫名稱。 如果您只想 toouse hello 預設資料庫，hello 查詢*建立資料庫...*可以省略。
* **&#60; 資料表名稱 >**: hello 的 toocreate hello 指定資料庫中的 hello 資料表名稱。 如果您想 toouse hello 預設資料庫，可以透過直接參考 hello 資料表*&#60; 資料表名稱 >*而不 &#60; 資料庫名稱 >。
* **&#60; 欄位的分隔符號 >**: hello 分隔符號分隔 hello 資料檔案 toobe 中的欄位，上傳 toohello Hive 資料表。
* **&#60; 行分隔符號 >**: hello 分隔符號，用來分隔 hello 資料檔案中的行。
* **&#60; 儲存體位置 >**: hello Azure 儲存體位置 toosave hello 資料的 Hive 資料表。 如果您未指定*位置 &#60; 儲存體位置 >*、 hello 資料庫和 hello 資料表會儲存在*hive/倉儲/*目錄中的 hello Hive 叢集預設 hello 預設容器。 如果您想 toospecify hello 儲存位置，hello 儲存位置有 toobe hello hello 資料庫和資料表的預設容器內。 這個位置已經 toobe 稱為 hello 格式中的 hello 叢集中的位置相對的 toohello 預設容器*'wasb: / / &#60; 目錄 1 > /'*或*' wasb: / / &#60; 目錄 1 > / &#60;目錄 2 > /'*等等。Hello 查詢執行之後，hello 相對目錄會建立 hello 預設容器內。
* **TBLPROPERTIES("skip.header.line.count"="1")**: hello 資料檔案的標頭行，如果您有 tooadd 這個屬性**hello 結尾**的 hello*建立資料表*查詢。 否則，為記錄 toohello 資料表載入 hello 標頭行。 如果 hello 資料檔案沒有標頭行，此設定可省略 hello 查詢中。

## <a name="load-data"></a>載入資料 tooHive 資料表
以下是將資料載入的 Hive 資料表的 hello Hive 查詢。

    LOAD DATA INPATH '<path tooblob data>' INTO TABLE <database name>.<table name>;

* **&#60; 路徑 tooblob 資料 >**： 如果 hello blob 檔案上傳 toobe toohello Hive 資料表中的 hello HDInsight Hadoop 叢集中的 hello 預設容器，hello *（& s) #60; 路徑 tooblob 資料 >* hello 格式應該是*' wasb: / / &#60; 在此容器中的目錄 > / &#60; blob 檔案名稱 >'*。 hello blob 檔案，也可以在 hello HDInsight Hadoop 叢集中的其他容器中。 在此情況下， *&#60; 路徑 tooblob 資料 >* hello 格式應該是*' wasb: / / （& s) #60; 容器名稱 > @ （& s) #60; 儲存體帳戶名稱 >.blob.core.windows.net/ &#60; blob 檔案名稱 >'*.

  > [!NOTE]
  > hello blob 資料上傳 toobe tooHive 資料表有 toobe hello 預設或 hello hello Hadoop 叢集的儲存體帳戶的其他容器中。 否則，hello*將資料載入*抱怨無法存取 hello 資料的查詢失敗。
  >
  >

## <a name="partition-orc"></a>進階主題：資料分割資料表及使用 ORC 格式儲存 Hive 資料
Hello 資料很大，分割 hello 資料表是有幫助，只需要 tooscan hello 資料表的幾個資料分割的查詢。 比方說，它是網站的日期合理 toopartition hello 記錄資料。

在加法 toopartitioning Hive 資料表，也很有幫助 toostore hello Hive 資料 hello 最佳化的資料列單欄式 (ORC) 格式。 如需 ORC 格式的詳細資訊，請參閱<a href="https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC#LanguageManualORC-ORCFiles" target="_blank">在 Hive 讀取、寫入及處理資料時使用 ORC 檔案提升效能</a>。

### <a name="partitioned-table"></a>資料分割資料表
以下是建立資料分割的資料表和資料載入其中的 hello Hive 查詢。

    CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<table name>
    (field1 string,
    ...
    fieldN string
    )
    PARTITIONED BY (<partitionfieldname> vartype) ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
         lines terminated by '<line separator>' TBLPROPERTIES("skip.header.line.count"="1");
    LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<partitioned table name>
        PARTITION (<partitionfieldname>=<partitionfieldvalue>);

查詢時資料分割的資料表，建議在 hello tooadd hello 分割區條件**開頭**的 hello`where`子句，因為這樣可改善 hello 的大幅搜尋的效率。

    select
        field1, field2, ..., fieldN
    from <database name>.<partitioned table name>
    where <partitionfieldname>=<partitionfieldvalue> and ...;

### <a name="orc"></a>使用 ORC 格式儲存 Hive 資料
您無法直接將資料載入從 blob 儲存體以 hello ORC 格式儲存的 Hive 資料表。 以下是 hello 步驟需要 tootake tooload 資料從 Azure 的 hello blob tooHive ORC 格式儲存的資料表。

建立外部資料表**儲存成文字檔**並從 blob 儲存體 toohello 資料表載入資料。

        CREATE EXTERNAL TABLE IF NOT EXISTS <database name>.<external textfile table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>'
            lines terminated by '<line separator>' STORED AS TEXTFILE
            LOCATION 'wasb:///<directory in Azure blob>' TBLPROPERTIES("skip.header.line.count"="1");

        LOAD DATA INPATH '<path toohello source file>' INTO TABLE <database name>.<table name>;

建立內部資料表以 hello 相同結構描述以 hello 相同欄位分隔符號，並將儲存的步驟 1 中的 hello 外部資料表 hello hello ORC 格式的登錄區資料。

        CREATE TABLE IF NOT EXISTS <database name>.<ORC table name>
        (
            field1 string,
            field2 int,
            ...
            fieldN date
        )
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '<field separator>' STORED AS ORC;

在步驟 1 中的 hello 外部資料表選取資料和插入 hello ORC 資料表

        INSERT OVERWRITE TABLE <database name>.<ORC table name>
            SELECT * FROM <database name>.<external textfile table name>;

> [!NOTE]
> 如果 hello 文字檔資料表*&#60; 資料庫名稱 >。 （& s) #60; 外部文字檔資料表名稱 >*有資料分割，在步驟 3 中 hello`SELECT * FROM <database name>.<external textfile table name>`選取 hello 資料分割的變數，在 hello 欄位傳回的資料集的命令。 插入 hello *（& s) #60; 資料庫名稱 >。 （& s) #60; ORC 資料表名稱 >*失敗後*（& s) #60; 資料庫名稱 >。 （& s) #60; ORC 資料表名稱 >*沒有 hello 分割變數hello 資料表結構描述中的欄位。 在此情況下，您需要插入太 toospecifically 選取 hello 欄位 toobe*&#60; 資料庫名稱 >。 &#60; ORC 資料表名稱 >* ，如下所示：
>
>

        INSERT OVERWRITE TABLE <database name>.<ORC table name> PARTITION (<partition variable>=<partition value>)
           SELECT field1, field2, ..., fieldN
           FROM <database name>.<external textfile table name>
           WHERE <partition variable>=<partition value>;

很安全 toodrop hello *&#60; 外部文字檔資料表名稱 >*時使用下列查詢，所有的資料之後 hello 已插入至*（& s) #60; 資料庫名稱 >。 （& s) #60; ORC 資料表名稱 >*:

        DROP TABLE IF EXISTS <database name>.<external textfile table name>;

完成此程序之後，您應該有資料表 hello ORC 格式準備 toouse 中的資料。  
