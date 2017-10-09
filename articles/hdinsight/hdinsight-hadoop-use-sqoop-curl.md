---
title: "使用 Curl HDInsight 的 Azure 中的 Hadoop Sqoop aaaUse |Microsoft 文件"
description: "了解如何 tooremotely 提交 Sqoop 作業 tooHDInsight 使用 Curl。"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 39798321-78ca-428c-bcfe-322e49af4059
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: d9c09a6704ab6c5f48be50ed6d6314ec406df8ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a>使用 Curl 在 HDInsight 中以 Hadoop 執行 Sqoop 作業
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

了解 HDInsight 中 toouse Curl toorun Sqoop 工作在 Hadoop 叢集的方式。

Curl 是使用的 toodemonstrate 如何您可以使用與互動 HDInsight 未經處理的 HTTP 要求 toorun、 監視器和 Sqoop 作業擷取 hello 結果。 這是利用 hello WebHCat 提供 REST API （先前稱為 Templeton） 您的 HDInsight 叢集來運作。

> [!NOTE]
> 如果您已熟悉使用 linux Hadoop 伺服器，但新 tooHDInsight，請參閱[資訊使用 on Linux 的 HDInsight](hdinsight-hadoop-linux-information.md)。
> 
> 

## <a name="prerequisites"></a>必要條件
toocomplete hello 本文中的步驟，您需要下列 hello:

* HDInsight 叢集上的 Hadoop (Linux 或 Windows 型)
* [Curl](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a>使用 Curl 提交 Sqoop 作業
> [!NOTE]
> 當使用 WebHCat Curl 或任何其他的 REST 通訊，您必須驗證 hello 要求藉由提供 hello 使用者名稱和 hello HDInsight 叢集系統管理員密碼。 Hello 統一資源識別元 (URI) 的一部分使用 toosend hello 要求 toohello 伺服器，您也必須使用 hello 叢集名稱。
> 
> 本章節中的 hello 命令，請將**USERNAME** hello 使用者 tooauthenticate toohello 叢集與取代**密碼**hello hello 使用者帳戶的密碼。 取代**CLUSTERNAME**與 hello 叢集的名稱。
> 
> hello REST API 會透過保護[基本驗證](http://en.wikipedia.org/wiki/Basic_access_authentication)。 您永遠應該利用安全 HTTP (HTTPS) toohelp 確保您的認證會安全地傳送 toohello 伺服器提出要求。
> 
> 

1. 從命令列使用下列命令，您可以連接 tooyour HDInsight 叢集的 tooverify hello:
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    您應該會收到類似 toohello 後的回應：
   
        {"status":"ok","version":"v1"}
   
    此命令中使用的 hello 參數如下所示：
   
   * **-u** -使用 tooauthenticate hello 要求 hello 使用者名稱和密碼。
   * **-G** - 指出這是 GET 要求。
     
     hello 開頭 hello URL **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**，將會針對所有要求 hello 相同。 hello 路徑**/status**，表示該 hello 要求 tooreturn WebHCat (也稱為 Templeton) 狀態 hello 伺服器。 
2. 使用下列 toosubmit sqoop 工作 hello:

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    此命令中使用的 hello 參數如下所示：

    * **-d** -自`-G`不使用 hello 要求預設 toohello POST 方法。 `-d`指定傳送嗨資料值與 hello 要求。

        * **user.name** -hello 使用者執行 hello 命令。

        * **命令**-hello Sqoop 命令 tooexecute。

        * **statusdir** -hello 為此工作狀態的 hello 目錄寫入。

    此命令應該會傳回可以用的 toocheck hello hello 工作狀態的作業識別碼。

        {"id":"job_1415651640909_0026"}

1. hello 工作，下列命令使用 hello toocheck hello 狀態。 取代**JOBID** hello hello 上一個步驟中傳回的值。 例如，如果 hello 傳回值是`{"id":"job_1415651640909_0026"}`，然後**JOBID**會`job_1415651640909_0026`。
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    如果 hello 工作已完成，將會 hello 狀態**SUCCEEDED**。
   
   > [!NOTE]
   > 此 Curl 要求會傳回 JavaScript 物件標記法 (JSON) 文件以 hello 工作; 的相關資訊使用 jq tooretrieve 只 hello 狀態值。
   > 
   > 
2. 一旦 hello hello 作業狀態已變更過**SUCCEEDED**，您可以從 Azure Blob 儲存體擷取 hello hello 作業結果。 hello `statusdir` hello 查詢傳遞的參數包含 hello 位置 hello 輸出檔; 在此情況下， **wasb: / 範例/curl**。 此地址將 hello 工作的 hello 輸出儲存在 hello**範例/curl**目錄 hello HDInsight 叢集所用的預設儲存體容器。
   
    您可以列出並下載這些檔案使用 hello [Azure CLI](../cli-install-nodejs.md)。 Toolist 中的檔案，例如**範例/curl**，使用下列命令的 hello:
   
        azure storage blob list <container-name> example/curl
   
    toodownload 檔案，使用下列 hello:
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > 您必須指定 hello 使用 hello 包含 hello blob 儲存體帳戶名稱`-a`和`-k`參數或使用組 hello **AZURE\_儲存體\_帳戶**和**AZURE\_儲存體\_存取\_金鑰**環境變數。 如需詳細資訊，請參閱 <a href="hdinsight-upload-data.md" target="_blank"。
   > 
   > 

## <a name="limitations"></a>限制
* 大量匯出的以 Linux 為基礎的 HDInsight、 hello Sqoop 使用連接器 tooexport 資料 tooMicrosoft SQL Server 或 Azure SQL Database 目前不支援大量插入。
* 批次處理-與 linux 的 HDInsight，當使用 hello`-batch`切換時執行插入、 Sqoop 會執行多個的插入，而不是批次處理 hello 插入作業。

## <a name="summary"></a>摘要
如本文所示，您可以使用 HDInsight 叢集上的未經處理的 HTTP 要求 toorun、 監視器和檢視 hello 結果的 Sqoop 工作。

如需有關使用本文章中的 hello REST 介面的詳細資訊，請參閱 hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API 指南</a>。

## <a name="next-steps"></a>後續步驟
Hive 與 HDInsight 搭配使用的一般資訊：

* [在 HDInsight 上將 Sqoop 與 Hadoop 搭配使用](hdinsight-use-sqoop.md)

如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：

* [搭配使用 Hive 與 HDInsight 上的 Hadoop](hdinsight-use-hive.md)
* [搭配 HDInsight 上的 Hadoop 使用 Pig](hdinsight-use-pig.md)
* [搭配使用 MapReduce 與 HDInsight 上的 Hadoop](hdinsight-use-mapreduce.md)

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




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


