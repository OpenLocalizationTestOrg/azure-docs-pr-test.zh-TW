---
title: "hello HDInsight 的 Azure 中的 查詢主控台上 aaaUse Hadoop Hive |Microsoft 文件"
description: "了解如何 toouse hello 網頁查詢主控台 toorun Hive 查詢在 HDInsight Hadoop 叢集從您的瀏覽器。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5ae074b0-f55e-472d-94a7-005b0e79f779
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 621882082c9a07655d34b8dc980b8e47dd04b745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-query-console"></a>執行 Hive 查詢使用 hello 查詢主控台
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

在本文中，您將學習如何 toouse hello HDInsight 查詢主控台 toorun Hive 查詢在 HDInsight Hadoop 叢集從您的瀏覽器。

> [!IMPORTANT]
> hello HDInsight 查詢主控台才可以使用 Windows 為基礎的 HDInsight 叢集上。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。
>
> 針對 HDInsight 3.4 或更新版本，請參閱[在 Ambari Hive 檢視中執行 Hive 查詢](hdinsight-hadoop-use-hive-ambari-view.md)，以取得有關從網頁瀏覽器執行 Hive 查詢的資訊。

## <a id="prereq"></a>必要條件
toocomplete hello 本文中的步驟，您將需要下列 hello。

* Windows 型 HDInsight Hadoop 叢集
* 現代網頁瀏覽器

## <a id="run"></a>執行 Hive 查詢使用 hello 查詢主控台
1. 開啟網頁瀏覽器並瀏覽過**https://CLUSTERNAME.azurehdinsight.net**，其中**CLUSTERNAME** hello 您的 HDInsight 叢集名稱。 如果出現提示，請輸入 hello 使用者名稱和您在建立 hello 叢集時使用的密碼。
2. 從 hello 頁面頂端的 hello hello 連結、 選取**登錄區編輯器**。 這會顯示一個表單，可以是您想 toorun hello HDInsight 叢集中的使用的 tooenter hello HiveQL 陳述式。

    ![hello 登錄區編輯器](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    取代 hello 文字`Select * from hivesampletable`以 hello 下列 HiveQL 陳述式：

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    這些陳述式會執行下列動作的 hello:

   * **DROP TABLE**: hello 資料表已存在時刪除 hello 資料表與 hello 資料檔。
   * **CREATE EXTERNAL TABLE**：在 Hive 中建立新的「外部」資料表。 外部資料表存放區; 只有 hello 資料表定義hello 資料會保留在 hello 原始位置。

     > [!NOTE]
     > 當您預期 hello 基礎資料 toobe 更新由外部來源 （例如自動化的資料上傳程序中） 或另一項 MapReduce 作業，但是您通常想要登錄區查詢 toouse hello 最新的資料，應該使用外部資料表。
     >
     > 卸除的外部資料表沒有**不**刪除 hello 資料、 hello 資料表定義。
     >
     >
   * **資料列格式**: hello 資料格式化的方式會告知 hive 控制檔。 在此情況下，每個記錄檔中的 hello 欄位會以空格分隔。
   * **儲存為文字檔位置**： 告訴 Hive 其中 hello 資料是儲存 （hello 範例/資料目錄），則會儲存為文字
   * **選取**： 選取所有資料列計數其中資料行**t4**包含 hello 值**[錯誤]**。 這應該會傳回值 **3** ，因為有三個資料列包含此值。
   * **INPUT__FILE__NAME LIKE '%.log'** - 告訴 Hive 我們只應該從檔名以 log 結尾的檔案中傳回資料。 這會限制 hello 搜尋 toohello sample.log 檔案，其中包含 hello 資料，並防止從其他範例與 hello 我們所定義的結構描述不相符的資料檔案傳回資料。
3. 按一下 [提交] 。 hello**作業工作階段**在 hello hello 頁面底部應該會顯示 hello 工作的詳細資料。
4. 當 hello**狀態**太欄位變更**已完成**，選取**檢視詳細資料**hello 作業。 在 hello 詳細資料頁面上，hello**作業輸出**包含`[ERROR]    3`。 您可以使用 hello**下載**按鈕在此欄位 toodownload 包含 hello hello 工作輸出的檔案。

## <a id="summary"></a>摘要
如您所見，查詢主控台提供簡單的方式 toorun hello Hive 查詢中的 HDInsight 叢集，監視 hello 作業狀態，並擷取 hello 輸出。

進一步了解使用 Hive 查詢主控台 toorun Hive 工作，toolearn 選取**入門**頂端 hello hello 查詢主控台，然後使用所提供的 hello 範例。 每個範例會引導 hello 程序使用 Hive tooanalyze 資料，包括關於 hello 範例中所使用的 hello HiveQL 陳述式的說明。

## <a id="nextsteps"></a>接續步驟
如需 HDInsight 中 Hive 的一般資訊：

* [搭配使用 Hive 與 HDInsight 上的 Hadoop](hdinsight-use-hive.md)

如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：

* [搭配使用 Pig 與 HDInsight 上的 Hadoop](hdinsight-use-pig.md)
* [搭配使用 MapReduce 與 HDInsight 上的 Hadoop](hdinsight-use-mapreduce.md)

如果您正在使用 Hive Tez，請參閱下列文件的偵錯資訊的 hello:

* [使用 Windows 為基礎的 HDInsight 上的 hello Tez UI](hdinsight-debug-tez-ui.md)
* [使用 hello Ambari Tez 以 Linux 為基礎的 HDInsight 上的檢視](hdinsight-debug-ambari-tez-view.md)

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
