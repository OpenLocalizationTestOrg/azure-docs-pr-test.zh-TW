---
title: "HDInsight 的 Azure 中的互動式 Hive aaaUse |Microsoft 文件"
description: "深入了解如何 toouse 互動式在 HDInsight Hive （LLAP 上的登錄區）。"
keywords: 
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0957643c-4936-48a3-84a3-5dc83db4ab1a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 9e751a08091d18bc1b3d070468feef87f6828c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a>在 HDInsight 中使用互動式 Hive (預覽)
互動式 Hive (又稱為. [Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) 為新的 HDInsight [叢集類型](hdinsight-hadoop-provision-linux-clusters.md#cluster-types)。  互動式 Hive 允許記憶體內快取，可讓 Hive 查詢更具互動性且速度更快。 這項新功能讓其中一個 hello HDInsight 世界上大部分高效能、 彈性且開啟巨量資料解決方案 hello 雲端上的記憶體中快取 （使用 Hive 和 Spark） 以及進階分析透過深層整合與 R Services。 

hello 互動式 Hive 叢集與不同 hello Hadoop 叢集。 它只包含 hello 登錄區服務。 

> [!NOTE]
> 很快地，MapReduce、Pig、Sqoop、Oozie 和其他服務便會從這個叢集類型中移除。
> hello hello 互動式 Hive 叢集中的 Hive 服務僅可透過 hello Ambari Hive 檢視、 Beeline 和 Hive ODBC 存取。 無法透過 Hive 主控台、Templeton、Azure CLI 和 Azure PowerShell 存取。 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a>建立互動式 Hive 叢集
只有以 Linux 為基礎的叢集可支援互動式 Hive 叢集。 如需建立 HDInsight 叢集的相關資訊，請參閱[在 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)。

## <a name="execute-hive-from-interactive-hive"></a>從互動式 Hive 執行 Hive
Hive 查詢的執行方式有不同選項可供您選擇︰

* 執行 Hive 使用 hello Ambari 登錄區檢視
  
    Hello 使用 hello Hive 檢視相關的資訊，請參閱[使用 hello HDInsight 中的 Hadoop hive 控制檔的檢視](hdinsight-hadoop-use-hive-ambari-view.md)。
* 使用 Beeline 執行 Hive
  
    在 HDInsight 上使用 Beeline hello 資訊，請參閱[Beeline 與 HDInsight 中的 Hadoop Hive 使用](hdinsight-hadoop-use-hive-beeline.md)。
  
    您可以使用 Beeline hello 叢集前端節點或空白邊緣節點。  我們的建議是從空白邊緣節點使用 Beeline。  如需使用空白邊緣節點建立 HDInsight 叢集的相關資訊，請參閱[在 HDInsight 中使用空白邊緣節點](hdinsight-apps-use-edge-node.md)。
* 使用 Hive ODBC 執行 Hive
  
    使用 Hive ODBC hello 資訊，請參閱[hello Microsoft Hive ODBC 驅動程式連接的 Excel tooHadoop](hdinsight-connect-excel-hive-odbc-driver.md)。

**toofind hello JDBC 連接字串：**

1. 登入使用下列 URL 的 hello tooAmbari: https://<ClusterName>。.Azurehdinsight.net。
2. 按一下**Hive** hello 左側功能表中。
3. 按一下反白顯示 hello 圖示 toocopy hello URL:
   
   ![HDInsight Hadoop 互動式 Hive LLAP JDBC](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a>另請參閱
* [在 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)： 了解互動式 Hive toocreate HDInsight 中的叢集。
* [使用具有 Beeline HDInsight 中的 Hadoop Hive](hdinsight-hadoop-use-hive-beeline.md)： 了解如何 toouse Beeline toosubmit Hive 查詢。
* [Hello Microsoft Hive ODBC 驅動程式連接 Excel tooHadoop](hdinsight-connect-excel-hive-odbc-driver.md)： 了解如何 tooconnect Excel tooHive。

