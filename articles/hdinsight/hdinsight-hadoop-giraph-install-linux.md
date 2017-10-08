---
title: "aaaInstall HDInsight (Hadoop)-Azure 上使用 Giraph |Microsoft 文件"
description: "了解如何 tooinstall Giraph 上以 Linux 為基礎的 HDInsight 叢集使用指令碼動作。 指令碼動作可讓您 toocustomize hello 叢集建立期間，可以變更叢集設定或安裝服務和公用程式。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9fcac906-8f06-4002-9fe8-473e42f8fd0f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0f195b65cebf5e24d1808ef33b95b4d362555521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-tooprocess-large-scale-graphs"></a>在 HDInsight Hadoop 叢集上安裝 Giraph 和使用 Giraph tooprocess 大規模圖形

深入了解如何 tooinstall Apache Giraph 在 HDInsight 叢集上的。 HDInsight hello 指令碼動作功能可讓您 toocustomize 您的叢集執行 bash 指令碼。 指令碼和建立叢集之後，可以是使用的 toocustomize 叢集。

> [!IMPORTANT]
> 本文件中的 hello 步驟需要使用 Linux 的 HDInsight 叢集。 Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。

## <a name="whatis"></a>什麼是 Giraph

[Apache Giraph](http://giraph.apache.org/)可讓您使用 Hadoop，處理 tooperform 圖形，並可以搭配 Azure HDInsight。 圖形可以為物件之間的關聯性建立模型。 例如，大型的網路上的路由器之間的 hello 連線，例如 hello 網際網路或社交網路上的使用者之間的關聯性。 圖表處理可讓您 hello 在圖形中，物件之間的關聯性的相關 tooreason 例如：

* 根據目前的人際關係找出可能的朋友。

* 用來識別網路中的兩部電腦之間的 hello 最短路由。

* 計算 hello 頁面順位的網頁。

> [!WARNING]
> 提供與 hello HDInsight 叢集的元件可以完全支援-tooisolate 可協助 Microsoft 支援服務，並解決問題相關的 toothese 元件。
>
> 自訂元件，例如 Giraph，會收到盡商業上合理支援 toohelp 您 toofurther hello 問題進行疑難排解。 Microsoft 支援服務可能無法 tooresolving hello 問題。 如果無法解決，則您必須諮詢開放原始碼社群，以尋求該項技術的深厚專業知識。 例如，有許多社群網站可以使用，像是：[HDInsight 的 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight)、[http://stackoverflow.com](http://stackoverflow.com)。另外，Apache 專案在 [http://apache.org](http://apache.org) 上有專案網站，例如 [Hadoop](http://hadoop.apache.org/)。


## <a name="what-hello-script-does"></a>哪些 hello 指令碼會執行

此指令碼會執行下列動作的 hello:

* 安裝 Giraph 太`/usr/hdp/current/giraph`

* 複製 hello`giraph-examples.jar`檔案 toodefault 儲存體 (WASB) 為您的叢集：`/example/jars/giraph-examples.jar`

## <a name="install"></a>使用指令碼動作安裝 Giraph

範例指令碼 tooinstall Giraph 在 HDInsight 叢集上的將會位於下列位置的 hello:

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

本節提供指示 toouse hello 範例指令碼時使用 hello Azure 入口網站建立 hello 叢集的方式。

> [!NOTE]
> 您可以使用任何下列方法的 hello 套用指令碼動作：
> * Azure PowerShell
> * hello Azure CLI
> * hello HDInsight.NET SDK
> * Azure 資源管理員範本
> 
> 您也可以套用指令碼動作 tooalready 執行中的叢集。 如需詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。

1. 開始使用中的 hello 步驟建立叢集[建立 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-create-linux-clusters-portal.md)，但無法完成建立。

2. 在 hello**選擇性組態**刀鋒視窗中，選取**指令碼動作**，並提供下列資訊的 hello:

   * **名稱**： 輸入 hello 指令碼動作的易記名稱。

   * **指令碼 URI**：https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

   * **HEAD**：勾選此項目

   * **WORKER**：保持不勾選此項目

   * **ZOOKEEPER**：保持不勾選此項目

   * **參數**：將此欄位保留空白

3. 在 hello 底部 hello**指令碼動作**，使用 hello**選取**按鈕 toosave hello 組態。 最後，使用 hello**選取**在 hello hello 底部的按鈕**選擇性組態**刀鋒視窗 toosave hello 選擇性的組態資訊。

4. 繼續中所述建立 hello 叢集[建立 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-create-linux-clusters-portal.md)。

## <a name="usegiraph"></a>如何在 HDInsight 中使用 Giraph？

一旦建立 hello 叢集之後，請使用下列步驟 toorun hello SimpleShortestPathsComputation 範例隨附 Giraph hello。 這個範例會使用 hello basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf)尋找 hello 圖形中的物件之間最短的路徑實作。

1. 連線使用 SSH toohello HDInsight 叢集：

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

2. 使用 hello 下列命令 toocreate 名為**tiny_graph.txt**:

    ```bash
    nano tiny_graph.txt
    ```

    使用 hello hello 這個檔案的內容為下列文字：

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    這項資料會描述一種導向圖形，藉由使用 hello 格式中的物件之間的關聯性`[source_id, source_value,[[dest_id], [edge_value],...]]`。 每一行代表 `source_id` 物件和一或多個 `dest_id` 物件之間的關聯性。 hello`edge_value`可以視為 hello 強度或 hello 連線之間的距離`source_id`和`dest\_id`。

    繪製出，並使用 hello 值 （或加權），做為 hello 物件之間的距離，hello 資料看起來會像下列圖表中的 hello:

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. toosave hello 檔案，使用**Ctrl + X**，然後**Y**，最後再**Enter** tooaccept hello 檔案名稱。

4. 使用下列 toostore hello 資料到您的 HDInsight 叢集的主要儲存體的 hello:

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. 使用下列命令的 hello 執行的 hello SimpleShortestPathsComputation 範例：

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    hello 下表描述此命令搭配使用的 hello 參數：

   | 參數 | 作用 |
   | --- | --- |
   | `jar` |包含 hello 範例 hello jar 檔案。 |
   | `org.apache.giraph.GiraphRunner` |使用 toostart hello 範例 hello 類別。 |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |hello 用的範例。 在此範例中，它會計算 hello 識別碼 1 和 hello 圖形中的所有其他識別碼之間的最短路徑。 |
   | `-ca mapred.job.tracker` |hello 叢集 hello 前端節點。 |
   | `-vif` |hello 輸入的格式 toouse hello 輸入資料。 |
   | `-vip` |hello 輸入的資料檔。 |
   | `-vof` |hello 輸出格式。 在此範例中，識別碼和值是純文字。 |
   | `-op` |hello 輸出位置。 |
   | `-w 2` |hello toouse 背景工作數目。 在此範例中是 2。 |

    如需有關這些錯誤碼和其他 Giraph 範例搭配使用的參數的詳細資訊，請參閱 hello [Giraph 快速入門](http://giraph.apache.org/quick_start.html)。

6. 一旦 hello 工作已完成，hello 結果會儲存在 hello **/example/out/shotestpaths**目錄。 hello 輸出檔案名稱的開頭**一部分-m-** ，而結尾數字，指出 hello 首先，第二，等檔案。 使用下列命令 tooview hello 輸出 hello:

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    hello 輸出應該看起來類似 toohello 下列文字：

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    hello SimpleShortestPathComputation 範例是硬式編碼的 toostart 與物件識別碼為 1，並尋找 hello 最短路徑 tooother 物件。 hello 輸出的格式的 hello`destination_id`和`distance`。 hello`distance`為 hello 值 （或加權） 旅行 hello 邊緣的物件識別碼為 1 與 hello 目標 id。

    視覺化資料，您可以確認 hello 結果識別碼 1 和所有其他物件之間旅行 hello 最短的路徑。 hello 識別碼 1 和識別碼 4 之間的最短路徑為 5。 此值為 hello 總之間的距離<span style="color:orange">識別碼 1 和 3</span>，然後<span style="color:red">ID 為 3 和 4</span>。

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a>後續步驟

* [在 HDInsight 叢集上安裝及使用 Hue](hdinsight-hadoop-hue-linux.md)。

* [在 HDInsight 叢集上安裝 Solr](hdinsight-hadoop-solr-install-linux.md)。
