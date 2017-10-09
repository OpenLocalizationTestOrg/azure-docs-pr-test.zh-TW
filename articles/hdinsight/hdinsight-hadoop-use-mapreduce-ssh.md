---
title: "aaaMapReduce 和 SSH 連線，HDInsight 的 Azure 中的 Hadoop |Microsoft 文件"
description: "了解如何 toouse SSH toorun MapReduce 作業使用 HDInsight Hadoop。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 844678ba-1e1f-4fda-b9ef-34df4035d547
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 9626577687fc5cc119a39d65a9c45298f57f81c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a>搭配使用 MapReduce 與 HDInsight 上的 Hadoop 和 SSH

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

了解從安全殼層 (SSH) 連線 tooHDInsight toosubmit MapReduce 作業的方式。

> [!NOTE]
> 如果您已經熟悉使用 linux Hadoop 伺服器，但您新 tooHDInsight 資訊，請參閱[以 Linux 為基礎的 HDInsight 秘訣](hdinsight-hadoop-linux-information.md)。

## <a id="prereq"></a>必要條件

* Linux 型 HDInsight (HDInsight 上的 Hadoop) 叢集

  > [!IMPORTANT]
  > Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

* SSH 用戶端。 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)

## <a id="ssh"></a>使用 SSH 連線

Toohello 叢集使用 SSH 連線。 比方說，下列命令的 hello 連接名為 tooa 叢集**myhdinsight**:

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

**如果您使用的 SSH 驗證的憑證金鑰**，您可能需要在用戶端系統上，hello 私用金鑰 toospecify hello 位置，例如：

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

**如果您使用的密碼 SSH 驗證**，您需要 tooprovide hello 密碼提示。

如需搭配 HDInsight 使用 SSH 的詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

## <a id="hadoop"></a>使用 Hadoop 命令

1. 連接的 toohello HDInsight 叢集後，請使用下列命令 toostart MapReduce 工作的 hello:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    此命令會啟動 hello`wordcount`類別，包含在 hello`hadoop-mapreduce-examples.jar`檔案。 它會使用 hello`/example/data/gutenberg/davinci.txt`做為輸入，並輸出文件儲存在`/example/data/WordCountOutput`。

    > [!NOTE]
    > 如需此 MapReduce 作業和 hello 範例資料的詳細資訊，請參閱[在 HDInsight 上的 Hadoop 使用 MapReduce](hdinsight-use-mapreduce.md)。

2. hello 作業處理，以及它會傳回資訊的類似 toohello hello 作業完成時，下列文字，會發出詳細資料：

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. Hello 作業完成時，請使用下列命令 toolist hello 輸出檔案的 hello:

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    此命令會顯示兩個檔案︰`_SUCCESS` 和 `part-r-00000`。 hello`part-r-00000`檔案包含這項作業的 hello 輸出。

    > [!NOTE]
    > 某些 MapReduce 工作可能跨多個分割 hello 結果**# # r 一部分 #**檔案。 如果是，使用 hello # # # hello 檔案 tooindicate hello 順序後置詞。

4. 下列命令使用 hello tooview hello 輸出：

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    此命令會顯示一份所包含的 hello 文字中 hello **wasb://example/data/gutenberg/davinci.txt**檔案和 hello 的每個單字發生次數。 hello 下列文字是包含在 hello 檔案中的 hello 資料的範例：

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a>摘要

如您所見，Hadoop 命令也提供簡單的方式 toorun MapReduce 工作的 HDInsight 叢集，然後檢視 hello 作業輸出。

## <a id="nextsteps"></a>接續步驟

如需 HDInsight 中 MapReduce 工作的一般資訊：

* [在 HDInsight Hadoop 上使用 MapReduce](hdinsight-use-mapreduce.md)

如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：

* [搭配使用 Hive 與 HDInsight 上的 Hadoop](hdinsight-use-hive.md)
* [搭配使用 Pig 與 HDInsight 上的 Hadoop](hdinsight-use-pig.md)
