---
title: "在 HDInsight Hadoop Pig aaaUse |Microsoft 文件"
description: "深入了解與 HDInsight 上的 Hadoop Pig toouse 的方式。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: acfeb52b-4b81-4a7d-af77-3e9908407404
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 90850f2c742b8954c66ce277127e01b14fc3906f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a>搭配使用 Pig 與 HDInsight 上的 Hadoop

深入了解如何 toouse [Apache Pig](http://pig.apache.org/)與 HDInsight...

Pig 是一個平台，可使用稱為 *Pig Latin*的程序性語言建立 Hadoop 的程式。 Pig 是建立替代 tooJava *MapReduce*方案和其隨附於 Azure HDInsight。 使用下列資料表 toodiscover hello Pig 可以搭配 HDInsight 的各種方式 hello:

| **使用此方法**  | ...一個 **互動式** 殼層 | ...**批次** 處理 | ...搭配此 **叢集作業系統** | ...從此 **用戶端作業系統** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-hadoop-use-pig-ssh.md) |✔ |✔ |Linux |Linux、Unix、Mac OS X 或 Windows |
| [REST API](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |✔ |Linux 或 Windows |Linux、Unix、Mac OS X 或 Windows |
| [.NET SDK for Hadoop](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |✔ |Linux 或 Windows |Windows (目前) |
| [Windows PowerShell](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |✔ |Linux 或 Windows |Windows |
| [遠端桌面](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 和 3.3) |✔ |✔ |Windows |Windows |

> [!IMPORTANT]
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

## <a id="why"></a>為何要使用 Pig

Hello 挑戰之一使用 MapReduce Hadoop 中處理資料使用只對應和縮減函式來實作處理邏輯。 複雜的處理，您通常會有 toobreak 處理成多個 MapReduce 作業的鏈結在一起 tooachieve hello 預期結果。

Pig 可讓您 toodefine 處理為一系列的 hello 資料流經 tooproduce hello 預期輸出的轉換。

hello Pig 拉丁語言可讓您 toodescribe hello 資料流程從原始的輸入，透過一或多個轉換，tooproduce hello 預期輸出。 Pig Latin 程式遵循此一般模式：

* **負載**： 讀取資料 toobe hello 檔案系統和操作

* **轉換**： 操作 hello 資料

* **傾印或儲存**： 輸出資料 toohello 螢幕，或將它儲存為處理

### <a name="user-defined-functions"></a>使用者定義函式

Pig 拉丁也支援使用者定義函數 (UDF)，可讓您實作邏輯，會在 Pig 拉丁困難 toomodel tooinvoke 外部元件。

如需 Pig Latin 的詳細資訊，請參閱 [Pig Latin 參考手冊 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) (英文) 和 [Pig Latin 參考手冊 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html) (英文)。

使用 Pig Udf 的範例，請參閱下列文件的 hello:

* [在 HDInsight 中搭配使用 DataFu 與 Pig](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu 是由 Apach 維護的 UDF 實用集合
* [在 HDInsight 中使用 Python 搭配 Pig 和 Hive](hdinsight-python.md)
* [在 HDInsight 中搭配 Hive 與 Pig 使用 C#](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <a id="data"></a>範例資料

HDInsight 提供各種範例資料集，其中會儲存在 hello`/example/data`和`/HdiSamples`目錄。 這些目錄位於 hello 預設儲存體叢集。 本文件中的 hello Pig 範例會使用 hello *log4j*檔案從`/example/data/sample.log`。

Hello 檔案內的每個記錄檔所組成的欄位包含的那一行`[LOG LEVEL]`欄位 tooshow hello 類型和 hello 嚴重性，例如：

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

Hello 上述範例中，在 hello 記錄層級會是錯誤。

> [!NOTE]
> 您也可以產生 log4j 檔案使用 hello [Apache Log4j](http://en.wikipedia.org/wiki/Log4j)記錄工具，然後再上傳該檔案 tooyour blob。 請參閱[上傳資料 tooHDInsight](hdinsight-upload-data.md)如需相關指示。 如需關於如何搭配 HDInsight 使用 Azure 儲存體 Blob 的詳細資訊，請參閱 [搭配 HDInsight 使用 Azure Blob 儲存體](hdinsight-hadoop-use-blob-storage.md)。

## <a id="job"></a>範例作業

hello 以下的 Pig 拉丁工作載入 hello `sample.log` hello 預設儲存體檔案針對您的 HDInsight 叢集。 然後它會執行一系列轉換所產生的計數方式的多次每個記錄層級發生在 hello 輸入的資料。 hello 結果會寫入 tooSTDOUT。

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

hello 下列影像顯示哪些每個轉換就會執行 toohello 資料的摘要。

![Hello 轉換圖形表示法][image-hdi-pig-data-transformation]

## <a id="run"></a>執行 hello 拉丁 Pig 工作

HDInsight 可以使用各種方法執行 Pig Latin 工作。 使用下列資料表 toodecide 哪一種方法是最適合您，hello，然後遵循逐步解說中的 hello 連結。

| **使用此方法**  | ...一個 **互動式** 殼層 | ...**批次** 處理 | ...搭配此 **叢集作業系統** | ...從這個**用戶端** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-hadoop-use-pig-ssh.md) |✔ |✔ |Linux |Linux、Unix、Mac OS X 或 Windows |
| [Curl](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |✔ |Linux 或 Windows |Linux、Unix、Mac OS X 或 Windows |
| [.NET SDK for Hadoop](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |✔ |Linux 或 Windows |Windows (目前) |
| [Windows PowerShell](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |✔ |Linux 或 Windows |Windows |
| [遠端桌面](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 和 3.3) |✔ |✔ |Windows |Windows |

> [!IMPORTANT]
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

## <a name="pig-and-sql-server-integration-services"></a>Pig 和 SQL Server Integration Services

您可以使用 SQL Server Integration Services (SSIS) toorun Pig 工作。 hello Azure Feature Pack for SSIS 提供 hello 遵循使用 Pig 工作，在 HDInsight 的元件。

* [Azure HDInsight Pig 工作][pigtask]

* [Azure 訂用帳戶連接管理員][connectionmanager]

深入了解 hello Azure Feature Pack for SSIS[這裡][ssispack]。

## <a id="nextsteps"></a>接續步驟
既然您已經學會如何 toouse 與 HDInsight，下列使用 hello Pig 會連結 tooexplore Azure HDInsight 以其他方式 toowork。

* [上傳資料 tooHDInsight][hdinsight-upload-data]
* [搭配 HDInsight 使用 Hivet][hdinsight-use-hive]
* [搭配 HDInsight 使用 Sqoop](hdinsight-use-sqoop.md)
* [在 HDInsight 上使用 Oozie](hdinsight-use-oozie.md)
* [搭配 HDInsight 使用 MapReduce 作業][hdinsight-use-mapreduce]

[apachepig-home]: http://pig.apache.org/
[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
[curl]: http://curl.haxx.se/
[pigtask]: http://msdn.microsoft.com/library/mt146781(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx


[hdinsight-upload-data]: hdinsight-upload-data.md

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md#mapreduce-sdk

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx


[image-hdi-pig-data-transformation]: ./media/hdinsight-use-pig/HDI.DataTransformation.gif
