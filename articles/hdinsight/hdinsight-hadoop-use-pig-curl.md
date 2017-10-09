---
title: "與 HDInsight 的 Azure 中的其餘部分的 Hadoop Pig aaaUse |Microsoft 文件"
description: "了解 toouse REST toorun Pig 拉丁工作在 Hadoop 上的中 Azure HDInsight 叢集的方式。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ed5e10d1-4f47-459c-a0d6-7ff967b468c4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 760139e3caad9103d8c9d34e7f548d476014b5ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a>使用 REST 在 HDInsight 上搭配 Hadoop 執行 Pig 作業

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

了解 toorun Pig 拉丁藉由 REST 要求 tooan Azure HDInsight 叢集的工作。 Curl 是您可以互動方式使用 hello WebHCat REST API 的 HDInsight 的使用的 toodemonstrate。

> [!NOTE]
> 如果您已熟悉使用 linux Hadoop 伺服器，但新 tooHDInsight，請參閱[以 Linux 為基礎的 HDInsight 秘訣](hdinsight-hadoop-linux-information.md)。

## <a id="prereq"></a>必要條件

* Azure HDInsight (HDInsight 上的 Hadoop) 叢集 (Linux 型或 Windows 型)

  > [!IMPORTANT]
  > Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

* [Curl](http://curl.haxx.se/)

* [jq](http://stedolan.github.io/jq/)

## <a id="curl"></a>使用 Curl 執行 Pig 工作

> [!NOTE]
> hello REST API 會透過保護[基本存取驗證](http://en.wikipedia.org/wiki/Basic_access_authentication)。 一律使用安全 HTTP (HTTPS) tooensure 您的認證會安全地傳送 toohello 伺服器提出要求。
>
> 當使用本節中的 hello 命令，來取代`USERNAME`hello 使用者 tooauthenticate toohello 叢集與取代`PASSWORD`hello hello 使用者帳戶的密碼。 取代`CLUSTERNAME`與 hello 叢集的名稱。
>


1. 從命令列使用下列命令，您可以連接 tooyour HDInsight 叢集的 tooverify hello:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    您應該會收到下列 JSON 回應 hello:

        {"status":"ok","version":"v1"}

    此命令中使用的 hello 參數如下所示：

    * **-u**: hello 使用者名稱和密碼使用 tooauthenticate hello 要求
    * **-G**：指出此要求是 GET 要求

     hello 開頭 hello URL **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**，hello 相同的所有要求。 hello 路徑**/status**，表示該 hello 要求 WebHCat (也稱為 Templeton) tooreturn hello 狀態 hello 伺服器。

2. 使用下列程式碼 toosubmit Pig 拉丁作業 toohello 叢集 hello:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    此命令中使用的 hello 參數如下所示：

    * **-d**： 因為`-G`不使用 hello 要求預設 toohello POST 方法。 `-d`指定傳送嗨資料值與 hello 要求。

    * **user.name**: hello 執行使用者的 hello 命令
    * **執行**: hello Pig 拉丁陳述式 tooexecute
    * **statusdir**: hello 的這項作業狀態的 hello 目錄寫入

    > [!NOTE]
    > 請注意會以 hello 取代 Pig 拉丁陳述式中的 hello 空格`+`字元 Curl 搭配使用時。

    此命令應該會傳回可以用的 toocheck hello 狀態 hello 工作，例如作業識別碼：

        {"id":"job_1415651640909_0026"}

3. hello 工作，下列命令使用 hello toocheck hello 狀態

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     取代`JOBID`hello hello 上一個步驟中傳回的值。 例如，如果 hello 傳回值是`{"id":"job_1415651640909_0026"}`，然後`JOBID`是`job_1415651640909_0026`。

    如果 hello 工作已完成，則會 hello 狀態**SUCCEEDED**。

    > [!NOTE]
    > 傳回 JavaScript 物件標記法 (JSON) 文件以 hello 作業和 jq 資訊是使用的 tooretrieve 此 Curl 要求只 hello 狀態值。

## <a id="results"></a>檢視結果

Hello hello 工作狀態變更時太**SUCCEEDED**，您可以擷取 hello hello 作業結果。 hello `statusdir` hello 查詢傳遞的參數包含 hello 位置 hello 輸出檔; 在此情況下， `/example/pigcurl`。

HDInsight 可以使用 Azure 儲存體或 Azure 資料湖存放區為 hello 預設資料儲存區。 有各種方式 tooget hello 根據哪一種您使用的資料。 如需詳細資訊，請參閱 hello 儲存體 區段的 hello[以 Linux 為基礎的 HDInsight 資訊](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store)文件。

## <a id="summary"></a>摘要

本文件中所示範，您可以使用您的 HDInsight 叢集上的未經處理的 HTTP 要求 toorun、 監視器和檢視 hello 結果的 Pig 工作。

如需有關使用本文章中的 hello REST 介面的詳細資訊，請參閱 hello [WebHCat 參考](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference)。

## <a id="nextsteps"></a>接續步驟

如需 HDInsight 上 Pig 的一般資訊：

* [搭配使用 Pig 與 HDInsight 上的 Hadoop](hdinsight-use-pig.md)

如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：

* [搭配使用 Hive 與 HDInsight 上的 Hadoop](hdinsight-use-hive.md)
* [搭配使用 MapReduce 與 HDInsight 上的 Hadoop](hdinsight-use-mapreduce.md)
