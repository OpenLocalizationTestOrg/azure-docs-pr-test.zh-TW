---
title: "Hadoop、 Spark、 Kafka、 HBase，或 R 伺服器-Azure HDInsight aaaCluster 安裝 |Microsoft 文件"
description: "設定 Hadoop、 Kafka、 Spark、 HBase、 R 伺服器或 Storm 叢集 hdinsight 從瀏覽器、 hello Azure CLI、 Azure PowerShell、 REST 或 SDK。"
keywords: "hadoop 叢集設定、kafka 叢集設定、spark 叢集設定、什麼是 hadoop 中的叢集"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 23a01938-3fe5-4e2e-8e8b-3368e1bbe2ca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/06/2017
ms.author: jgao
ms.openlocfilehash: 80ec59d8a39f7fccb940503fd2dc3ae5afee6bcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-clusters-in-hdinsight-with-hadoop-spark-kafka-and-more"></a>使用 Hadoop、Spark 及 Kafka 等在 HDInsight 中設定叢集

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

深入了解如何 tooset 安裝及設定在 HDInsight Hadoop、 Spark、 Kafka、 互動式 Hive、 HBase、 R 伺服器或 Storm 叢集。 此外，了解 toocustomize 的叢集，並將這些 tooa 網域加入安全性。

Hadoop 叢集由數個虛擬機器 (節點) 組成，可用於分散處理作業。 Azure HDInsight 處理安裝的實作詳細資料和設定個別的節點，因此您只需要 tooprovide 一般組態資訊。 

> [!IMPORTANT]
>一旦建立叢集，並停止刪除 hello 叢集時，就會開始 HDInsight 叢集計費。 計費是以每分鐘按比例計算，因此不再使用時，請一律刪除您的叢集。 了解如何太[刪除叢集。](hdinsight-delete-cluster.md)
>

## <a name="cluster-setup-methods"></a>叢集設定方法
hello 下表顯示 hello 不同的方法可以使用 tooset HDInsight 叢集。

| 叢集建立方法 | Web 瀏覽器 | 命令列 | REST API | SDK | 
| --- |:---:|:---:|:---:|:---:|
| [Azure 入口網站](hdinsight-hadoop-create-linux-clusters-portal.md) |✔ |&nbsp; |&nbsp; |&nbsp; |
| [Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md) |✔ |✔ |✔ |✔ |
| [Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) |&nbsp; |✔ |&nbsp; |&nbsp; |
| [Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md) |&nbsp; |✔ |&nbsp; |&nbsp; |
| [cURL](hdinsight-hadoop-create-linux-clusters-curl-rest.md) |&nbsp; |✔ |✔ |&nbsp; |
| [.NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md) |&nbsp; |&nbsp; |&nbsp; |✔ |
| [Azure 資源管理員範本](hdinsight-hadoop-create-linux-clusters-arm-templates.md) |&nbsp; |✔ |&nbsp; |&nbsp; |

## <a name="quick-create-basic-cluster-setup"></a>快速建立：基本的叢集設定
這篇文章會引導您完成安裝程式在 hello [Azure 入口網站](https://portal.azure.com)，其中您可以建立 HDInsight 叢集使用*快速建立*或*自訂*。 

按照 hello 螢幕 toodo 基本叢集設定中的指示進行。 以下是下列各項的詳細資訊：

* [資源群組名稱](#resource-group-name)
* [叢集類型和設定](#cluster-types) 
* [叢集登入和 SSH 使用者名稱](#cluster-login-and-ssh-username)
* [位置](#location)

> [!IMPORTANT]
> Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。 如需詳細資訊，請參閱 [HDInsight 3.3 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。
>

## <a name="resource-group-name"></a>資源群組名稱 

[Azure 資源管理員](../azure-resource-manager/resource-group-overview.md)可協助您處理 hello 資源群組中，參考 tooas 為應用程式中的 Azure 資源群組。 您可以部署、 更新、 監視或刪除您的應用程式在單一協調作業中的 hello 的所有資源。

## <a name="cluster-types"></a>叢集類型和設定
Azure HDInsight 目前提供 hello 下列叢集類型，各有一組元件 tooprovide 的某些功能。

> [!IMPORTANT]
> HDInsight 叢集有多種類型，每種類型各適合單一工作負載或技術。 沒有任何支援的方法 toocreate 結合多個類型，例如 Storm 和上一個叢集的 HBase 叢集。 如果您的方案要求分散到多個的 HDInsight 叢集類型的技術[Azure 虛擬網路](https://docs.microsoft.com/azure/virtual-network)可以連接所需的 hello 叢集類型。 
>
>

| 叢集類型 | 功能 |
| --- | --- |
| [Hadoop](hdinsight-hadoop-introduction.md) |批次查詢和分析儲存的資料 |
| [HBase](hdinsight-hbase-overview.md) |處理大量無綱要的 NoSQL 資料 |
| [Storm](hdinsight-storm-overview.md) |即時事件處理 |
| [Spark](hdinsight-apache-spark-overview.md) |記憶體內處理、互動式查詢、微批次串流處理 |
| [Kafka (預覽)](hdinsight-apache-kafka-introduction.md) | 分散式的資料流平台可能是使用的 toobuild 即時資料流資料管線和應用程式 |
| [R 伺服器](hdinsight-hadoop-r-server-overview.md) |各種巨量資料統計資料、預測模型和機器學習功能 |
| [互動式 Hive (預覽)](hdinsight-hadoop-use-interactive-hive.md) |更快速之互動式 Hive 查詢的記憶體內快取 |

### <a name="number-of-nodes-for-each-cluster-type"></a>每個叢集類型的節點數目
每個叢集類型都有自己的節點數目、節點術語和預設 VM 大小。 在下表的 hello，hello 每個節點類型的節點數目是在括號中。

| 類型 | 節點 | 圖表 |
| --- | --- | --- |
| Hadoop |前端節點 (2)、資料節點 (1+) |![HDInsight Hadoop 叢集節點](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hadoop-cluster-type-nodes.png) |
| HBase |前端伺服器 (2)、區域伺服器 (1+)、主要/Zookeeper 節點 (3) |![HDInsight HBase 叢集節點](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-hbase-cluster-type-setup.png) |
| Storm |Nimbus 節點 (2)、監督員伺服器 (1+)、Zookeeper 節點 (3) |![HDInsight Storm 叢集節點](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-storm-cluster-type-setup.png) |
| Spark |前端節點 (2)、背景工作角色節點 (1+)、Zookeeper 節點 (3) (A1 Zookeeper VM 大小不限) |![HDInsight Spark 叢集節點](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-spark-cluster-type-setup.png) |

如需詳細資訊，請參閱[預設叢集的節點，以及虛擬機器大小](hdinsight-component-versioning.md#default-node-configuration-and-virtual-machine-sizes-for-clusters)中 「 什麼是 hello Hadoop 元件與 HDInsight 中的版本 」？

### <a name="hdinsight-version"></a>HDInsight 版本
選擇此叢集 HDInsight hello 版本。 如需詳細資訊，請參閱[支援的 HDInsight 版本](hdinsight-component-versioning.md#supported-hdinsight-versions)。

### <a name="cluster-tiers"></a>叢集層：HDInsight 服務層

Azure HDInsight 提供兩個服務層中的 hello 巨量資料雲端方案： Standard 和 Premium。  如需詳細資訊，請參閱 [HDInsight Standard 和 HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium)。

hello 下列螢幕擷取畫面顯示 hello 選擇叢集類型的 Azure 入口網站的資訊。

![HDInsight 進階組態](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-type-configuration.png)


## <a name="cluster-login-and-ssh-user-name"></a>叢集登入和 SSH 使用者名稱
使用 HDInsight 叢集，您可以在建立叢集期間設定兩個使用者帳戶：

* HTTP 使用者： hello 預設使用者名稱是*admin*。它會使用基本組態的 hello hello Azure 入口網站上。 有時稱之為「叢集使用者」。
* SSH 使用者 （Linux 叢集）： 透過 SSH 使用的 tooconnect toohello 叢集。 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

## <a name="location"></a>叢集與儲存體的位置 (區域)

您不需要 toospecify hello 叢集位置明確： hello 叢集處於 hello 與 hello 預設儲存體相同的位置。 如需支援的地區中，按一下 hello**區域**下拉式清單上的[HDInsight 定價](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409)。

## <a name="storage-endpoints-for-clusters"></a>叢集的儲存體端點

雖然在內部部署安裝的 Hadoop 使用 hello Hadoop 分散式檔案系統 (HDFS) hello 叢集上的存放裝置，但在 hello 雲端使用儲存體端點會連接 toocluster。 HDInsight 叢集會使用 [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) 或 [Azure 儲存體中的 Blob](hdinsight-hadoop-use-blob-storage.md)。 使用 Azure 儲存體或資料湖存放區，表示您可以安全地刪除 hello HDInsight 叢集用於計算，同時保留您的資料。 

> [!WARNING]
> 不支援從 hello HDInsight 叢集的不同位置中使用額外的儲存體帳戶。

在設定期間，對於 hello 預設儲存體端點指定 blob 容器的 Azure 儲存體帳戶或資料湖存放區。 hello 預設儲存體包含應用程式與系統記錄檔。 您可以選擇性地指定其他連結的 Azure 儲存體帳戶和 hello 叢集的 Data Lake Store 帳戶可以存取。 hello HDInsight 叢集和 hello 相依的儲存體帳戶必須在 hello 相同的 Azure 位置。

![叢集儲存體設定：HDFS 相容的儲存體端點](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-cluster-creation-storage.png)

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


### <a name="optional-metastores"></a>選擇性中繼存放區
您可以建立選擇性的 Hive 或 Oozie 中繼存放區。 不過，並非所有叢集類型都支援中繼存放區，且 Azure SQL 資料倉儲不相容於中繼存放區。 

> [!IMPORTANT]
> 當您建立自訂的中繼存放區時，不使用連字號、 連字號或空格 hello 資料庫名稱。 這可能會造成 hello 叢集建立程序 toofail。

### <a name="use-hiveoozie-metastore"></a>Hive 中繼存放區

如果您想 tooretain Hive 資料表刪除 HDInsight 叢集之後，，使用自訂的中繼存放區。 然後，您可以附加 hello 中繼存放區 tooanother HDInsight 叢集。

針對某個 HDInsight 叢集版本建立的 HDInsight 中繼存放區，不能在不同的 HDInsight 叢集版本之間共用。 如需 HDInsight 版本清單，請參閱[支援的 HDInsight 版本](hdinsight-component-versioning.md#supported-hdinsight-versions)。

### <a name="oozie-metastore"></a>Oozie 中繼存放區

tooincrease 效能時使用 Oozie，使用自訂的中繼存放區。 刪除您的叢集之後，中繼存放區也可以提供存取 tooOozie 作業資料。 

> [!IMPORTANT]
> 您無法重複使用自訂的 Oozie 中繼存放區。 toouse 自訂的 Oozie 中繼存放區，建立 hello HDInsight 叢集時，必須提供空的 Azure SQL Database。

## <a name="configure-cluster-size"></a>設定叢集大小

您付費的節點使用量，只要 hello 叢集存在。 在叢集建立時並停止刪除 hello 叢集時，就會開始計費。 無法取消配置或保留叢集。

HDInsight 叢集的 hello 成本取決於節點和 hello hello 節點的虛擬機器大小的 hello 數目。 

不同的叢集類型具有不同的節點類型、節點數目和節點大小：
* Hadoop 叢集類型的預設值： 
    * 兩個*前端節點*  
    * 四個*資料節點*
* Storm 叢集類型的預設值： 
    * 兩個 *Nimbus 節點*
    * 三個 *ZooKeeper 節點*
    * 四個*監督員節點* 

如果您只是在試用 HDInsight，建議您使用一個資料節點。 如需關於 HDInsight 定價的詳細資訊，請參閱 [HDInsight 定價](https://go.microsoft.com/fwLink/?LinkID=282635&clcid=0x409)。

> [!NOTE]
> hello 叢集大小限制會因 Azure 訂用帳戶而異。 請連絡[Azure 計費支援](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request)tooincrease hello 限制。
>

當您使用 hello Azure 入口網站 tooconfigure hello 叢集時，hello 節點大小是可透過 hello**節點定價層**刀鋒視窗。 在 hello 入口網站，您也可以查看 hello hello 不同的節點大小與相關聯的成本。 

![HDinsight VM 節點大小](./media/hdinsight-hadoop-provision-linux-clusters/hdinsight-node-sizes.png)

### <a name="virtual-machine-sizes"></a>虛擬機器大小 
當您部署叢集時，選擇基礎的計算資源 hello 解決方案計劃 toodeploy。 下列 Vm 用於 HDInsight 叢集的 hello:
* A 和 D1-4 系列 VM：[一般用途 Linux VM 大小](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-general)
* D11-14 系列 VM：[記憶體最佳化 Linux VM 大小](https://docs.microsoft.com/azure/virtual-machines/linux/sizes-memory)

toofind 出何值您應該使用的 toospecify 時建立叢集使用的 VM 大小 hello 不同的 Sdk，或在使用 Azure PowerShell，請參閱[VM 大小的 HDInsight 叢集的 toouse](../cloud-services/cloud-services-sizes-specs.md#size-tables)。 在此連結的文件，請同時使用 hello 值 hello**大小**hello 資料表的資料行。

> [!IMPORTANT]
> 如果您的叢集需要 32 個以上的背景工作角色節點，則必須選取具有至少 8 個核心和 14 GB RAM 的前端節點大小。
>
>

如需相關資訊，請參閱[虛擬機器的大小](../virtual-machines/windows/sizes.md)。 如需定價的 hello 各種大小資訊，請參閱[HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight)。   

## <a name="custom-cluster-setup"></a>自訂叢集設定
自訂的叢集安裝組建上 hello 快速建立設定，並加入 hello 下列選項︰
- [HDInsight 應用程式](#hdinsight-applications)
- [叢集大小](#cluster-size)
- 進階設定
  - [指令碼動作](#customize-clusters-using-script-action)
  - [虛擬網路](#use-virtual-network)

## <a name="install-hdinsight-applications-on-clusters"></a>在叢集上安裝 HDInsight 應用程式

HDInsight 應用程式是使用者可以在以 Linux 為基礎的 HDInsight 叢集上安裝的應用程式。 您可以使用由 Microsoft、協力廠商所提供或您自己開發的應用程式。 如需詳細資訊，請參閱[在 Azure HDInsight 上安裝第三方 Hadoop 應用程式](hdinsight-apps-install-applications.md)。

大部分的 hello HDInsight 應用程式會安裝空白邊緣節點上。  空白邊緣節點是以相同的用戶端工具安裝並設定與 hello 前端節點的 hello 的 Linux 虛擬機器。 您可以使用 hello 邊緣節點存取 hello 叢集、 測試用戶端應用程式，以及裝載用戶端應用程式。 如需詳細資訊，請參閱 [Use empty edge nodes in HDInsight (在 HDInsight 中使用空白的邊緣節點)](hdinsight-apps-use-edge-node.md)。

## <a name="advanced-settings-script-actions"></a>進階設定：指令碼動作

您可以在建立期間使用指令碼來安裝其他元件或自訂組態。 這類指令碼會透過叫用**指令碼動作**，這是可以在 hello Azure 入口網站、 HDInsight Windows PowerShell cmdlet 或 hello HDInsight.NET SDK 中使用的組態選項。 如需詳細資訊，請參閱 [使用指令碼動作自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。

某些原生 Java 元件，例如砲象兵和 Cascading，可以在 hello 叢集上執行，以 Java 封存檔 (JAR) 檔案。 這些 JAR 檔案可以是分散式的 tooAzure 儲存體，而且與 Hadoop 工作提交機制提交 tooHDInsight 叢集。 如需詳細資訊，請參閱 [以程式設計方式提交 Hadoop 工作](hdinsight-submit-hadoop-jobs-programmatically.md)。

> [!NOTE]
> 如果您有問題部署 JAR 檔案 tooHDInsight 叢集，或呼叫 JAR 檔案，在 HDInsight 叢集，請連絡[Microsoft 支援服務](https://azure.microsoft.com/support/options/)。
>
> Cascading 不受 HDInsight 支援，而且不符合「Microsoft 支援」的資格。 支援的元件清單中，請參閱[hello 叢集版本 HDInsight 所提供的新](hdinsight-component-versioning.md)。
>
>

有時候，您需要下列組態檔案 hello 建立程序期間 tooconfigure hello:

* clusterIdentity.xml
* core-site.xml
* gateway.xml
* hbase-env.xml
* hbase-site.xml
* hdfs-site.xml
* hive-env.xml
* hive-site.xml
* mapred-site
* oozie-site.xml
* oozie-env.xml
* storm-site.xml
* tez-site.xml
* webhcat-site.xml
* yarn-site.xml

如需詳細資訊，請參閱 [使用 Bootstrap 自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-bootstrap.md)。

## <a name="advanced-settings-extend-clusters-with-a-virtual-network"></a>進階設定：使用虛擬網路擴充叢集
如果您的方案要求分散到多個的 HDInsight 叢集類型的技術[Azure 虛擬網路](https://docs.microsoft.com/azure/virtual-network)可以連接所需的 hello 叢集類型。 此設定可讓 hello 叢集，以及部署 toothem 任何程式碼，toodirectly 彼此通訊。

如需如何搭配使用 Azure 虛擬網路與 HDInsight 的詳細資訊，請參閱[使用 Azure 虛擬網路擴充 HDInsight](hdinsight-extend-hadoop-virtual-network.md)。

如需在 Azure 虛擬網路內使用兩個叢集類型的範例，請參閱[使用 Storm 和 HBase 分析感應器資料](hdinsight-storm-sensor-data-analysis.md)。 如需有關使用 HDInsight 與虛擬網路，包括特定組態需求的 hello 虛擬網路，請參閱[擴充 HDInsight 功能，方法是使用 Azure 虛擬網路](hdinsight-extend-hadoop-virtual-network.md)。

## <a name="troubleshoot-access-control-issues"></a>針對存取控制問題進行疑難排解

如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。

## <a name="next-steps"></a>後續步驟

- [HDInsight、 hello Hadoop 生態系統和 Hadoop 叢集為何？](hdinsight-hadoop-introduction.md)
- [開始在 HDInsight 中使用 Hadoop](hdinsight-hadoop-linux-tutorial-get-started.md)
- [從 Windows PC 在 HDInsight 上的 Hadoop 中作業](hdinsight-hadoop-windows-tools.md)
