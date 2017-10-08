---
title: "使用命令列-hello Azure HDInsight aaaCreate Hadoop 叢集 |Microsoft 文件"
description: "了解如何使用 toocreate HDInsight 叢集 hello 跨平台 Azure CLI 1.0。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 50b01483-455c-4d87-b754-2229005a8ab9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 5295b01054b8c23df0e3b75a3e0e8c933ac48b3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-using-hello-azure-cli"></a>建立使用 Azure CLI hello 的 HDInsight 叢集

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

建立使用 Azure CLI 1.0 hello HDInsight 3.5 叢集文件逐步解說中的步驟 hello。

> [!IMPORTANT]
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。


## <a name="prerequisites"></a>必要條件

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。

* **Azure CLI**。 本文件中的 hello 步驟上一次使用 Azure CLI 版本 0.10.14 測試。

    > [!IMPORTANT]
    > 本文件中的 hello 步驟使用 Azure CLI 2.0 無法運作。 Azure CLI 2.0 不支援建立 HDInsight 叢集。

## <a name="log-in-tooyour-azure-subscription"></a>登入 tooyour Azure 訂用帳戶

所述步驟 hello [hello Azure 命令列介面 (Azure CLI) 從連接 tooan Azure 訂用帳戶](../xplat-cli-connect.md)並連接 tooyour 訂用帳戶使用 hello**登入**方法。

## <a name="create-a-cluster"></a>建立叢集

從命令列，例如 PowerShell 或 Bash，應執行下列步驟的 hello。

1. 使用下列命令 tooauthenticate tooyour Azure 訂用帳戶的 hello:

        azure login

    您是提示的 tooprovide，您的名稱和密碼。 如果您有多個 Azure 訂用帳戶，使用`azure account set <subscriptionname>`tooset hello 訂閱 hello Azure CLI 命令使用。

2. 切換使用下列命令的 hello tooAzure Resource Manager 模式：

        azure config mode arm

3. 建立資源群組。 此資源群組包含 hello HDInsight 叢集與儲存體帳戶。

        azure group create groupname location

    * 取代`groupname`與 hello 群組的唯一名稱。

    * 取代`location`與您想要的 toocreate hello 群組中的 hello 地理區域。

       如需清單的有效位置，使用 hello`azure location list`命令，然後再使用其中一種從 hello hello 位置`Name`資料行。

4. 建立儲存體帳戶。 這個儲存體帳戶作為 hello 預設儲存體 hello HDInsight 叢集。

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * 取代`groupname`與 hello hello 先前步驟中建立的 hello 群組名稱。

    * 取代`location`以 hello hello 上一個步驟中使用相同的位置。

    * 取代`storagename`與 hello 儲存體帳戶的唯一名稱。

        > [!NOTE]
        > 如需此命令中使用的 hello 參數的詳細資訊，請使用`azure storage account create -h`tooview 此命令的說明。

5. 擷取 hello 金鑰用 tooaccess hello 儲存體帳戶。

        azure storage account keys list -g groupname storagename

    * 取代`groupname`hello 資源群組名稱。
    * 取代`storagename`與 hello hello 儲存體帳戶名稱。

     在 hello 所傳回的資料，將儲存 hello`key`值`key1`。

6. 建立 HDInsight 叢集。

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * 取代`groupname`hello 資源群組名稱。

    * 取代`Hadoop`與您想 toocreate hello 叢集類型。 例如，`Hadoop`、`HBase`、`Kafka`、`Spark` 或 `Storm`。

     > [!IMPORTANT]
     > HDInsight 叢集有不同的類型，對應 toohello 工作負載或調整為 hello 叢集的技術。 沒有任何支援的方法 toocreate 結合多個類型，例如 Storm 和上一個叢集的 HBase 叢集。

    * 取代`location`以 hello 在先前步驟中使用相同的位置。

    * 取代`storagename`hello 儲存體帳戶名稱。

    * 取代`storagekey`與 hello hello 先前步驟中取得的索引鍵。

    * Hello`--defaultStorageContainer`參數、 相同的名稱，因為您使用 hello 叢集使用 hello。

    * 取代`admin`和`httppassword`hello 名稱和密碼與您想 toouse 透過 HTTPS 存取 hello 叢集時。

    * 取代`sshuser`和`sshuserpassword`hello 使用者名稱和密碼與您想 toouse 時存取使用 SSH hello 叢集

    > [!IMPORTANT]
    > 此範例使用兩個背景工作角色節點建立叢集。 您也可以執行縮放作業，在叢集建立之後變更 hello 背景工作節點數。 如果您規劃使用 32 個以上的背景工作角色節點，則必須選取具有至少 8 個核心和 14 GB RAM 的前端節點大小。 您可以設定 hello 前端節點大小使用 hello`--headNodeSize`在叢集建立期間參數。
    >
    > 如需節點大小和相關成本的詳細資訊，請參閱 [HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。

    可能需要幾分鐘的時間 hello 叢集建立程序 toofinish。 通常大約 15 分鐘。

## <a name="troubleshoot"></a>疑難排解

如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。

## <a name="next-steps"></a>後續步驟

既然您已成功建立使用 Azure CLI hello 的 HDInsight 叢集，請使用 hello 如何遵循 toolearn toowork 與您的叢集：

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
