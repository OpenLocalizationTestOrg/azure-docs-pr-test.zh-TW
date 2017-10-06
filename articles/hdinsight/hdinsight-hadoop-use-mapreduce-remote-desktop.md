---
title: "aaaMapReduce 和遠端桌面 HDInsight 的 Azure 中的 Hadoop |Microsoft 文件"
description: "深入了解如何 toouse 遠端桌面 tooconnect tooHadoop HDInsight 和執行的 MapReduce 工作上。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9d3a7b34-7def-4c2e-bb6c-52682d30dee8
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: bdbbcf59ca86dd1b170471aa9e12334a04c23667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a>利用遠端桌面在 HDInsight 上的 Hadoop 中使用 MapReduce
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

在本文中，您將學習如何 tooconnect tooa HDInsight 上的 Hadoop 叢集使用遠端桌面，並使用 hello Hadoop 命令，以執行 MapReduce 工作。

> [!IMPORTANT]
> 只有在 Windows 型 HDInsight 叢集上才能使用「遠端桌面」。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。
>
> HDInsight 3.4 或更高，請參閱[透過 SSH 使用 MapReduce](hdinsight-hadoop-use-mapreduce-ssh.md)連接 toohello HDInsight 叢集，並在執行 MapReduce 工作的資訊。

## <a id="prereq"></a>必要條件
toocomplete hello 本文中的步驟，您需要下列 hello:

* Windows 型 HDInsight (HDInsight 上的 Hadoop) 叢集
* 執行 Windows 10、Windows 8 或 Windows 7 的用戶端電腦

## <a id="connect"></a>使用遠端桌面連線
Hello HDInsight 叢集，啟用遠端桌面，然後依照指示 hello 連接 tooit[連接使用 RDP tooHDInsight 叢集](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)。

## <a id="hadoop"></a>使用 hello Hadoop 命令
當您連接的 toohello 桌面 hello HDInsight 叢集，請使用 hello 使用 hello Hadoop 命令遵循步驟 toorun MapReduce 工作：

1. 從 hello HDInsight 桌面啟動 hello **Hadoop 命令列**。 這會開啟新的命令提示字元在 hello **c:\apps\dist\hadoop-&lt;版本號碼 >**目錄。

   > [!NOTE]
   > hello 版本號碼變更為已更新的 Hadoop。 hello **HADOOP_HOME**環境變數可以是使用的 toofind hello 路徑。 例如，`cd %HADOOP_HOME%`變更目錄 toohello Hadoop 目錄中的，而不需要您 tooknow hello 版本號碼。
   >
   >
2. toouse hello **Hadoop**命令 toorun 範例 MapReduce 工作，請使用下列命令的 hello:

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    這會啟動 hello **wordcount**類別，包含在 hello **hadoop-mapreduce-examples.jar** hello 目前目錄中的檔案。 做為輸入，它會使用 hello **wasb://example/data/gutenberg/davinci.txt**文件和輸出儲存在： **wasb: / 範例/資料/WordCountOutput**。

   > [!NOTE]
   > 如需此 MapReduce 作業和 hello 範例資料的詳細資訊，請參閱<a href="hdinsight-use-mapreduce.md">HDInsight Hadoop 中的使用 MapReduce</a>。
   >
   >
3. hello 作業會發出詳細資料，處理時，以及 hello 工作完成時，它會傳回類似 toohello 下列資訊：

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. Hello 工作完成時，使用下列命令 toolist hello 輸出檔案儲存在 hello **wasb://example/data/WordCountOutput**:

        hadoop fs -ls wasb:///example/data/WordCountOutput

    這應該會顯示兩個檔案：**_SUCCESS** 和 **part-r-00000**。 hello**一部分-r-00000**檔案包含這項作業的 hello 輸出。

   > [!NOTE]
   > 某些 MapReduce 工作可能跨多個分割 hello 結果**# # r 一部分 #**檔案。 如果是，使用 hello # # # hello 檔案 tooindicate hello 順序後置詞。
   >
   >
5. 下列命令使用 hello tooview hello 輸出：

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    此顯示中的清單所包含的 hello 文字 hello **wasb://example/data/gutenberg/davinci.txt**檔案，以及發生每個單字的 hello 次數。 hello 以下是將包含在 hello 檔案中的 hello 資料的範例：

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a>摘要
如您所見，hello Hadoop 命令提供簡單的方式 toorun MapReduce 工作的 HDInsight 叢集，然後再檢視 hello 作業輸出。

## <a id="nextsteps"></a>接續步驟
如需 HDInsight 中 MapReduce 工作的一般資訊：

* [在 HDInsight Hadoop 上使用 MapReduce](hdinsight-use-mapreduce.md)

如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：

* [搭配使用 Hive 與 HDInsight 上的 Hadoop](hdinsight-use-hive.md)
* [搭配使用 Pig 與 HDInsight 上的 Hadoop](hdinsight-use-pig.md)
