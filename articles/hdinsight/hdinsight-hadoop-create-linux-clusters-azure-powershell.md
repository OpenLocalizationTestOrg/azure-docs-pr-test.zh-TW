---
title: "使用 PowerShell 的 Azure HDInsight aaaCreate Hadoop 叢集 |Microsoft 文件"
description: "了解如何 toocreate Hadoop、 HBase、 風暴或 Spark 叢集，在 Linux 上的 HDInsight 使用 Azure PowerShell。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4208deca-d64a-45e1-8948-2673d5d7678c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 53afe4702f6b61a0720ceda48a4a34d7fa8797d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a>使用 Azure PowerShell 在 HDInsight 中建立以 Linux 為基礎的叢集

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Azure PowerShell 是一種強大的指令碼環境，您可以使用 toocontrol 並自動化 hello 部署和管理您在 Microsoft Azure 中的工作負載。 本文件提供如何使用 Azure PowerShell toocreate 以 Linux 為基礎的 HDInsight 叢集的相關資訊。 其中也包含一個範例指令碼。

> [!NOTE]
> Azure PowerShell 僅適用於 Windows 用戶端。 如果您使用 Linux、 Unix 或 Mac OS X 用戶端，請參閱[建立以 Linux 為基礎的 HDInsight 叢集使用 Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md)使用 hello Azure CLI toocreate 叢集相關資訊。

## <a name="prerequisites"></a>必要條件
您必須在開始此程序之前的 hello 下列：

* Azure 訂用帳戶。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。
* [Azure PowerShell](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > 使用 Azure Service Manager 管理 HDInsight 資源的 Azure PowerShell 支援已**被取代**，並已在 2017 年 1 月 1 日移除。 此文件使用 hello 新 HDInsight 的 cmdlet 可與 Azure 資源管理員中的步驟 hello。
    >
    > 請依照中的 hello 步驟[安裝 AzurePowershell</](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello 最新版的 Azure PowerShell。 如果您有指令碼的需要 toobe 修改 toouse hello 新的 cmdlet 可與 Azure 資源管理員，請參閱[移轉 tooAzure 資源管理員為基礎的開發工具的 HDInsight 叢集](hdinsight-hadoop-development-using-azure-resource-manager.md)如需詳細資訊。

## <a name="create-cluster"></a>建立叢集

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

toocreate 使用 Azure PowerShell HDInsight 叢集，您必須完成下列程序的 hello:

* 建立 Azure 資源群組
* 建立 Azure 儲存體帳戶
* 建立 Azure Blob 容器
* 建立 HDInsight 叢集

hello 下列指令碼示範如何 toocreate 新叢集：

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]

您指定給 hello 叢集登入的 hello 值是使用的 toocreate hello hello 叢集的 Hadoop 使用者帳戶。 使用此帳戶 tooconnect tooservices，例如 web Ui 或 REST Api 的 hello 叢集上裝載。

您為 hello SSH 使用者指定的 hello 值為 hello 叢集使用的 toocreate hello SSH 使用者。 使用此帳戶在 hello 叢集 toostart 遠端的 SSH 工作階段，並執行工作。 如需詳細資訊，請參閱 hello[搭配使用 SSH 和 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)文件。

> [!IMPORTANT]
> 如果您計劃 toouse 32 個以上的背景工作節點 （在建立叢集，或調整 hello 叢集建立之後），您也必須指定至少 8 核心，14 GB 的 RAM 與前端節點大小。
>
> 如需節點大小和相關成本的詳細資訊，請參閱 [HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。

它可能會佔用 too20 分鐘 toocreate 叢集。

## <a name="create-cluster-configuration-object"></a>建立叢集：設定物件

您也可以使用 `New-AzureRmHDInsightClusterConfig` Cmdlet 建立 HDInsight 設定物件。 然後，您就可以修改此組態物件 tooenable 其他設定選項為您的叢集。 最後，使用 hello `-Config` hello 參數`New-AzureRmHDInsightCluster`cmdlet toouse hello 組態。

hello 下列指令碼組態物件 tooconfigure R 伺服器上建立 HDInsight 叢集類型。 hello 組態可讓邊緣節點、 RStudio、 和額外的儲存體帳戶。

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]

> [!WARNING]
> 不支援在 hello HDInsight 叢集以外的不同位置中使用的儲存體帳戶。 使用此範例中，當建立 hello 額外的儲存體帳戶中 hello 與 hello 伺服器相同的位置。

## <a name="customize-clusters"></a>自訂叢集

* 請參閱 [使用 Bootstrap 自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell)。
* 請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。

## <a name="delete-hello-cluster"></a>刪除 hello 叢集

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>疑難排解

如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。

## <a name="next-steps"></a>後續步驟

現在您已成功建立的 HDInsight 叢集，使用下列資源 toolearn 如何 hello toowork 與您的叢集。

### <a name="hadoop-clusters"></a>Hadoop 叢集

* [〈搭配 HDInsight 使用 Hivet〉](hdinsight-use-hive.md)
* [搭配 HDInsight 使用 Pig](hdinsight-use-pig.md)
* [〈搭配 HDInsight 使用 MapReduce〉](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>HBase 叢集

* [開始在 HDInsight 上使用 HBase](hdinsight-hbase-tutorial-get-started-linux.md)
* [在 HDInsight 上開發適用於 HBase 的 Java 應用程式](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Storm 叢集

* [在 HDInsight 上開發適用於 Storm 的 Java 拓撲](hdinsight-storm-develop-java-topology.md)
* [在 HDInsight 上的 Storm 中使用 Python 元件](hdinsight-storm-develop-python-topology.md)
* [在 HDInsight 上使用 Storm 部署和監視拓撲](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a>Spark 叢集

* [使用 Scala 來建立獨立的應用程式](hdinsight-apache-spark-create-standalone-application.md)
* [利用 Livy 在 Spark 叢集上遠端執行工作](hdinsight-apache-spark-livy-rest-interface.md)
* [Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析](hdinsight-apache-spark-use-bi-tools.md)
* [機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式](hdinsight-apache-spark-eventhub-streaming.md)

