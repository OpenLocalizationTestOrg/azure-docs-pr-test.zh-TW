---
title: "HDInsight toocustomize 叢集 Azure 中的 R aaaUse |Microsoft 文件"
description: "深入了解如何使用 tooinstall R 指令碼動作，並使用 R 的 HDInsight 叢集上。"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: be851270-afa5-4af0-a69e-2d343a4deeb7
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bf5adf2e18dc43a743b29fd1567fad731b9c3ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a>在 HDInsight Hadoop 叢集上安裝和使用 R

了解如何 toocustomize Windows HDInsight 叢集以使用指令碼動作的 R 和 toouse R HDInsight 上的叢集。 hello [HDInsight 供應項目](https://azure.microsoft.com/pricing/details/hdinsight/)包含 R 伺服器做為您的 HDInsight 叢集的一部分。 這可讓 R 指令碼 toouse MapReduce 和 Spark toorun 分散式計算。 如需詳細資訊，請參閱[開始使用 HDInsight 上的 R 伺服器](hdinsight-hadoop-r-server-get-started.md)。 如需搭配以 Linux 為基礎的叢集使用 R 的詳細資訊，請參閱[在 HDInsight Hadoop 叢集上安裝和使用 R (Linux)](hdinsight-hadoop-r-scripts-linux.md)。

您也可以使用「指令碼動作」，在 Azure HDInsight 的任一類型的叢集 (Hadoop、Storm、HBase、Spark) 上安裝 R。 範例指令碼 tooinstall R 在 HDInsight 叢集上的都可從唯讀的 Azure 儲存體 blob [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1)。

**相關文章**

* [在 HDInsight Hadoop 叢集上安裝和使用 R (Linux)](hdinsight-hadoop-r-scripts-linux.md)
* [在 HDInsight 中建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)：有關建立 HDInsight 叢集的一般資訊
* [使用指令碼動作來自訂 HDInsight 叢集][hdinsight-cluster-customize]：有關使用指令碼動作來自訂 HDInsight 叢集的一般資訊。
* [開發 HDInsight 的指令碼動作指令碼](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a>什麼是 R？
hello <a href="http://www.r-project.org/" target="_blank">for Statistical Computing 的 R 專案</a>是開放原始碼語言和統計計算環境。 R 提供數百個內建的統計函數及它自己的程式設計語言，此語言結合了函數型和物件導向程式設計的層面。 它也提供廣泛的圖形功能。 R 是 hello 慣用的程式設計環境最專業統計學家也不斷和科學家在各種不同的欄位。

R 與 Azure Blob 儲存體 (WASB) 相容，因此便可在 HDInsight 上使用 R 來處理儲存在該處的資料。  

## <a name="install-r"></a>安裝 R
A[範例指令碼](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1)tooinstall R 在 HDInsight 叢集上的可從 Azure 儲存體中的 blob 唯讀狀態。 本節提供有關如何 toouse hello 建立 hello 叢集使用 hello Azure 入口網站時的範例指令碼的指示。

> [!NOTE]
> HDInsight 叢集版本 3.1 被引進 hello 範例指令碼。 如需 HDInsight 叢集版本的詳細資訊，請參閱 [HDInsight 叢集版本](hdinsight-component-versioning.md)。
>
>

1. 當您從 hello 入口網站中建立的 HDInsight 叢集時，按一下 **選擇性組態**，然後按一下**指令碼動作**。
2. 在 hello**指令碼動作**頁面上，輸入下列值的 hello:

    ![使用指令碼動作 toocustomize 叢集](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "使用指令碼動作 toocustomize 叢集")

    <table border='1'>
        <tr><th>屬性</th><th>值</th></tr>
        <tr><td>名稱</td>
            <td>為指定名稱 hello 指令碼動作，例如<b>安裝 R</b>。</td></tr>
        <tr><td>指令碼 URI</td>
            <td>指定 hello URI toohello 指令碼，例如，會叫用的 toocustomize hello 叢集中， <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></td></tr>
        <tr><td>節點類型</td>
            <td>指定 hello hello 自訂指令碼執行所在的節點。 您可以選擇 [所有節點]<b></b>、[僅限前端節點]<b></b> 或 [僅限背景工作節點]<b></b>。
        <tr><td>參數</td>
            <td>指定 hello 參數，如果 hello 指令碼所需。 不過，hello 指令碼 tooinstall R 不需要任何參數，因此您可以讓此處空白。</td></tr>
    </table>

    您可以在 hello 叢集上新增多個指令碼動作 tooinstall 多個元件。 加入 hello 指令碼之後，按一下來建立 hello 叢集 hello 核取記號 toostart。

您也可以使用 Azure PowerShell 或 hello HDInsight.NET SDK，在 HDInsight 上使用 hello 指令碼 tooinstall R。 此文章稍後會提供這些程序的指示。

## <a name="run-r-scripts"></a>執行 R 指令碼
本章節描述 toorun R 指令碼的 hello Hadoop 與 HDInsight 叢集的方式。

1. **建立遠端桌面連線 toohello 叢集**: hello 入口網站，從 R 安裝，以建立 hello 叢集啟用遠端桌面，然後連接 toohello 叢集。 如需指示，請參閱[連接使用 RDP tooHDInsight 叢集](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)。
2. **開啟 hello R 主控台**: hello R 安裝會將桌面上 hello hello 前端節點的連結 toohello R 主控台。 按一下以 tooopen hello R 主控台。
3. **執行 hello R 指令碼**: hello R 指令碼可以直接從 hello R 主控台執行貼上它，選取它，並按 ENTER 鍵。 以下是簡單的範例指令碼會產生 hello 數字 1 too100，然後將其乘以 2。

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

hello 前兩行呼叫 hello RHadoop 文件庫以 r 安裝的 hello 最後一行沖印 hello 結果 toohello 主控台。 hello 輸出應該看起來像這樣：

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a>使用 Azure PowerShell 安裝 R
請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)。  hello 範例會示範如何使用 Azure PowerShell 的 Spark tooinstall。 您需要 toocustomize hello 指令碼 toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1)。

## <a name="install-r-using-net-sdk"></a>使用 .NET SDK 安裝 R
請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell)。 hello 範例會示範如何 tooinstall Spark 使用 hello.NET SDK。 您需要 toocustomize hello 指令碼 toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11)。

## <a name="see-also"></a>另請參閱
* [在 HDInsight Hadoop 叢集上安裝和使用 R (Linux)](hdinsight-hadoop-r-scripts-linux.md)
* [在 HDInsight 中建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)：有關建立 HDInsight 叢集的一般資訊
* [使用指令碼動作來自訂 HDInsight 叢集][hdinsight-cluster-customize]：有關使用指令碼動作來自訂 HDInsight 叢集的一般資訊。
* [開發 HDInsight 的指令碼動作指令碼](hdinsight-hadoop-script-actions.md)
* [在 HDInsight 叢集上安裝和使用 Spark][hdinsight-install-spark]：有關安裝 Spark 的指令碼動作範例
* [在 HDInsight 叢集上安裝 Giraph](hdinsight-hadoop-giraph-install.md)：有關安裝 Giraph 的指令碼動作範例
* [在 HDInsight 叢集上安裝 Solr](hdinsight-hadoop-solr-install-linux.md)：有關安裝 Solr 的指令碼動作範例。

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md
