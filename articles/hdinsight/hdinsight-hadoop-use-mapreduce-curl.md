---
title: "aaaUse MapReduce 和 Curl HDInsight 的 Azure 中的 Hadoop |Microsoft 文件"
description: "了解如何 tooremotely 執行 MapReduce 工作的 Hadoop HDInsight 上使用 Curl。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: bc6daf37-fcdc-467a-a8a8-6fb2f0f773d1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 16920205bacf9699f88090568099e0508a172b3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a>使用 REST 搭配 HDInsight 上的 Hadoop 執行 MapReduce 作業

了解 HDInsight 叢集上的 Hadoop 上 toouse hello WebHCat REST API toorun MapReduce 作業的方式。 Curl 是使用的 toodemonstrate 如何您可以使用與互動 HDInsight 未經處理的 HTTP 要求 toorun MapReduce 工作。

> [!NOTE]
> 如果您已熟悉使用 linux Hadoop 伺服器，但是您新 tooHDInsight，請參閱 hello[配備 HDInsight 上的 Linux Hadoop 有關 tooknow](hdinsight-hadoop-linux-information.md)文件。


## <a id="prereq"></a>必要條件

* 一個 Hadoop on HDInsight 叢集
* [Curl](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a id="curl"></a>使用 Curl 執行 MapReduce 工作

> [!NOTE]
> 當您 WebHCat 的情況下，使用 Curl 或任何其他的 REST 通訊時，您必須藉由提供 hello HDInsight 叢集系統管理員使用者名稱和密碼驗證 hello 要求。 您必須使用 hello 叢集名稱做為 hello 使用的 toosend hello 要求 toohello 伺服器 URI 的一部分。
>
> 本章節中的 hello 命令，請將**USERNAME**與 hello 使用者 tooauthenticate toohello 叢集和**密碼**hello hello 使用者帳戶的密碼。 取代**CLUSTERNAME**與 hello 叢集的名稱。
>
> hello REST API 會受到使用[基本存取驗證](http://en.wikipedia.org/wiki/Basic_access_authentication)。 您永遠應該使用您的認證會安全地傳送 toohello 伺服器的 HTTPS tooensure 提出要求。


1. 從命令列使用下列命令，您可以連接 tooyour HDInsight 叢集的 tooverify hello:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    您應該會收到下列 JSON 回應類似 toohello:

        {"status":"ok","version":"v1"}

    此命令中使用的 hello 參數如下所示：

   * **-u**： 指出使用 tooauthenticate hello 要求 hello 使用者名稱和密碼
   * **-G**：指出此作業是 GET 要求

     hello 開頭的 URI，hello **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**，hello 相同的所有要求。

2. toosubmit MapReduce 工作，請使用下列命令的 hello:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    hello 結尾 hello URI (/ mapreduce/jar) 會告知 WebHCat 此要求會啟動 MapReduce 工作，從 jar 檔案中的類別。 此命令中使用的 hello 參數如下所示：

   * **-d**:`-G`未使用，所以 hello 要求預設 toohello POST 方法。 `-d`指定傳送嗨資料值與 hello 要求。
    * **user.name**: hello 執行使用者的 hello 命令
    * **jar**: hello jar 檔案的包含類別 toobe hello 位置執行
    * **類別**: hello 包含 hello MapReduce 邏輯類別
    * **arg**: hello 引數 toobe 傳遞 toohello MapReduce 工作。 Hello 在此情況下，輸入用於 hello 輸出的文字檔案和 hello 目錄

     此命令應該會傳回可以用的 toocheck hello hello 工作狀態的作業識別碼：

       {"id":"job_1415651640909_0026"}

3. hello 工作，下列命令使用 hello toocheck hello 狀態：

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    取代 hello **JOBID** hello hello 上一個步驟中傳回的值。 例如，如果 hello 傳回值是`{"id":"job_1415651640909_0026"}`，然後將 JOBID hello `job_1415651640909_0026`。

    如果 hello 作業已完成，傳回是 hello 狀態`SUCCEEDED`。

   > [!NOTE]
   > 此 Curl 要求傳回 JSON 文件以 hello 工作的相關資訊。 使用 Jq tooretrieve 只 hello 狀態值。

4. Hello hello 工作狀態變更時太`SUCCEEDED`，您可以從 Azure Blob 儲存體擷取 hello hello 作業結果。 hello `statusdir` hello 查詢傳遞的參數包含 hello hello 輸出檔位置。 在此範例中，是 hello 位置`/example/curl`。 此位址在 hello 叢集預設儲存體中儲存 hello 工作的 hello 輸出`/example/curl`。

您可以列出並下載這些檔案使用 hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli)。 如需使用 Azure CLI hello 從 blob 的詳細資訊，請參閱 hello[使用 hello 與 Azure 儲存體的 Azure CLI 2.0](../storage/common/storage-azure-cli.md#create-and-manage-blobs)文件。

## <a id="nextsteps"></a>接續步驟

如需 HDInsight 中 MapReduce 工作的一般資訊：

* [搭配使用 MapReduce 與 HDInsight 上的 Hadoop](hdinsight-use-mapreduce.md)

如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：

* [搭配使用 Hive 與 HDInsight 上的 Hadoop](hdinsight-use-hive.md)
* [搭配使用 Pig 與 HDInsight 上的 Hadoop](hdinsight-use-pig.md)

如需有關使用本文章中的 hello REST 介面的詳細資訊，請參閱 hello [WebHCat 參考](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference)。
