---
title: "在 HDInsight 叢集的 Azure 上 aaaUse 透過 SSH 的 Hadoop Pig |Microsoft 文件"
description: "深入了解如何使用 SSH 的連接 tooa linux Hadoop 叢集，然後使用 hello Pig 命令 toorun Pig 拉丁陳述式，以互動方式或以批次作業。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b646a93b-4c51-4ba4-84da-3275d9124ebe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 1da303e239b537e6b331b1d33010058582718c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-hello-pig-command-ssh"></a>Pig 工作在叢集上執行 linux 與 hello Pig 命令 (SSH)

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

了解 toointeractively 從 SSH 連線 tooyour HDInsight 叢集中執行 Pig 工作的方式。 hello Pig 拉丁程式設計語言，可讓您輸入的套用的 toohello 資料 tooproduce hello 預期輸出 toodescribe 轉換。

> [!IMPORTANT]
> hello 本文件中的步驟需要以 Linux 為基礎的 HDInsight 叢集。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

## <a id="ssh"></a>使用 SSH 連線

使用 SSH tooconnect tooyour HDInsight 叢集。 hello 下列範例會連接名為 tooa 叢集**myhdinsight** hello 帳戶命名為**sshuser**:

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

**如果您提供的 SSH 驗證憑證金鑰**當您建立 hello HDInsight 叢集，您可能需要 toospecify hello 位置 hello 私密金鑰的用戶端系統上。

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

**如果您提供密碼 SSH 驗證**建立 hello HDInsight 叢集，提供 hello 密碼提示。

如需搭配 HDInsight 使用 SSH 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

## <a id="pig"></a>使用 hello Pig 命令

1. 一旦連接之後，請使用下列命令的 hello 啟動 hello Pig 命令列介面 (CLI):

        pig

    隨後，您應該會看到 `grunt>` 提示字元。

2. 輸入下列陳述式的 hello:

        LOGS = LOAD '/example/data/sample.log';

    此命令會載入記錄檔中的 hello hello sample.log 檔案內容。 您可以使用下列陳述式的 hello 檢視 hello hello 檔案內容：

        DUMP LOGS;

3. 接下來，從每一筆記錄套用的規則運算式 tooextract 只有 hello 記錄層級，使用下列陳述式的 hello 轉換 hello 資料：

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    您可以使用**傾印**tooview hello hello 轉換後的資料。 在此案例中，請使用 `DUMP LEVELS;`。

4. 繼續使用 hello 下表中的 hello 陳述式來套用轉換：

    | Pig Latin 陳述式 | 哪些 hello 陳述式會執行 |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | 移除包含 hello 記錄層級的 null 值的資料列，並將結果 hello `FILTEREDLEVELS`。 |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | 群組 hello 記錄層級的資料列，並會儲存成 hello 結果`GROUPEDLEVELS`。 |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | 建立一組資料，其中包含每個唯一記錄層級值和其發生次數。 hello 資料集就會儲存至`FREQUENCIES`。 |
    | `RESULT = order FREQUENCIES by COUNT desc;` | 依計數 （遞減） 排序 hello 記錄層級，並且將儲存到`RESULT`。 |

    > [!TIP]
    > 使用`DUMP`tooview hello 結果的每個步驟之後的 hello 轉換。

5. 您也可以儲存轉換的 hello 結果使用 hello`STORE`陳述式。 例如，陳述式之後的 hello 儲存 hello `RESULT` toohello `/example/data/pigout` hello 預設儲存體叢集上的目錄：

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > hello 資料會儲存在名為的檔案中的 hello 指定目錄`part-nnnnn`。 如果 hello 目錄已經存在，您會收到錯誤。

6. tooexit hello 提示字元中，grunt 輸入陳述式之後的 hello:

        QUIT;

### <a name="pig-latin-batch-files"></a>Pig Latin 批次檔

您也可以使用 hello Pig 命令 toorun Pig 拉丁包含在檔案中。

1. 結束 hello grunt 提示字元後, 使用 hello 下列命令到名為 toopipe STDIN `pigbatch.pig`。 此檔案會建立 hello hello SSH 使用者帳戶的主目錄中。

        cat > ~/pigbatch.pig

2. 輸入或貼上 hello 下列行，然後再使用 Ctrl + D 完成。

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. 使用 hello 下列命令 toorun hello`pigbatch.pig`使用 hello Pig 命令的檔案。

        pig ~/pigbatch.pig

    一旦 hello 批次工作完成時，您會看見 hello 下列輸出：

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <a id="nextsteps"></a>接續步驟

Pig HDInsight 中的一般資訊，請參閱下列文件的 hello:

* [搭配使用 Pig 與 HDInsight 上的 Hadoop](hdinsight-use-pig.md)

如需有關其他方式 toowork Hadoop HDInsight 上使用，請參閱下列文件的 hello:

* [搭配使用 Hive 與 HDInsight 上的 Hadoop](hdinsight-use-hive.md)
* [搭配使用 MapReduce 與 HDInsight 上的 Hadoop](hdinsight-use-mapreduce.md)
