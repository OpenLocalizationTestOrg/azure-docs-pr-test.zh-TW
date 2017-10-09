---
title: "從 Windows 為基礎的 HDInsight aaaMigrate tooLinux 為基礎的 HDInsight 的 Azure |Microsoft 文件"
description: "了解如何從 Windows 為基礎的 HDInsight toomigrate 叢集 tooa 以 Linux 為基礎的 HDInsight 叢集。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: ff35be59-bae3-42fd-9edc-77f0041bab93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 7e5e536e8672d7e7c3086c6860cec062d05eda65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-from-a-windows-based-hdinsight-cluster-tooa-linux-based-cluster"></a>從 Windows 為基礎的 HDInsight 叢集 tooa Linux 為基礎的叢集移轉

本文件提供 Windows 和 Linux 的 HDInsight 和指引的 hello 差異的詳細資料 toomigrate 現有工作負載 tooa linux 叢集。

雖然 Windows 為基礎的 HDInsight 提供簡單的方式 toouse Hadoop hello 雲端中，您可能需要 toomigrate tooa linux 叢集。 例如，tootake 利用以 Linux 為基礎的工具和技術所需的方案。 Hello Hadoop 生態系統中的許多項目會以 Linux 為基礎的系統上開發，並可能無法使用以 Windows 為基礎的 HDInsight 的使用。 除此之外，許多針對 Hadoop 的書籍、影片及其他訓練材料，都會假設您正在使用 Linux 系統。

> [!NOTE]
> HDInsight 叢集會使用 Ubuntu 長期支援 (LTS) 做為 hello 作業系統 hello hello 叢集中的節點。 如需其他元件的版本控制資訊與 HDInsight，可用的 Ubuntu hello 版本資訊，請參閱[HDInsight 元件版本](hdinsight-component-versioning.md)。

## <a name="migration-tasks"></a>移轉工作

如下所示為 hello 移轉的一般工作流程。

![移轉工作流程圖表](./media/hdinsight-migrate-from-windows-to-linux/workflow.png)

1. 讀取這份文件的每個區段 toounderstand 變更時，可能會需要移轉您現有的工作流程、 作業、 等 tooa linux 叢集。

2. 建立以 Linux 為基礎的叢集做為測試/品質保證環境。 如需建立以 Linux 為基礎之叢集的詳細資訊，請參閱 [在 HDInsight 中建立以 Linux 為基礎的叢集](hdinsight-hadoop-provision-linux-clusters.md)。

3. 現有的作業、 資料來源和接收器 toohello 新環境的複本。

4. 執行驗證測試 toomake 確定您作業的工作，如預期般 hello 新叢集上。

一旦您已確認一切運作正常，排程 hello 移轉停機的時間。 在這個停機時間，執行下列動作的 hello:

1. 備份儲存在本機 hello 叢集節點上的任何暫時性資料。 例如，如果您的資料是直接儲存在前端節點上。

2. 刪除 hello windows 叢集。

3. 建立以 Linux 為基礎的叢集使用的 hello 相同預設 hello Windows 為基礎的叢集使用的資料存放區。 hello Linux 架構叢集可以繼續使用現有的實際執行資料。

4. 匯入任何已備份的暫時性資料。

5. 開始作業/仍會繼續處理使用 hello 新叢集。

### <a name="copy-data-toohello-test-environment"></a>複製資料 toohello 測試環境

有許多方法 toocopy hello 資料和作業，兩個 hello 但是本節所討論 hello 最簡單方法 toodirectly 移動檔案 tooa 測試叢集。

#### <a name="hdfs-copy"></a>HDFS 複製

使用 hello hello 實際執行叢集 toohello 測試叢集的下列步驟 toocopy 資料。 這些步驟使用 hello`hdfs dfs`隨附 HDInsight 的公用程式。

1. 尋找 hello 儲存體帳戶與預設容器資訊為您現有的叢集。 hello 下列範例會使用 PowerShell tooretrieve 這項資訊：

    ```powershell
    $clusterName="Your existing HDInsight cluster name"
    $clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    write-host "Storage account name: $clusterInfo.DefaultStorageAccount.split('.')[0]"
    write-host "Default container: $clusterInfo.DefaultStorageContainer"
    ```

2. toocreate 測試環境中，步驟 hello HDInsight 文件中的 hello 建立 linux 叢集。 建立 hello 叢集之前停止，而是選取**選擇性組態**。

3. 從 hello 選擇性組態刀鋒視窗中，選取**連結儲存體帳戶**。

4. 選取**新增儲存體金鑰**，並出現提示時，選取 hello hello 在步驟 1 中的 PowerShell 指令碼傳回的儲存體帳戶。 在每個刀鋒視窗上按一下 [選取]。 最後，建立 hello 叢集。

5. 一旦建立 hello 叢集之後，使用 tooit 連接**SSH。** 如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

6. 從 hello SSH 工作階段，使用 hello hello 連結儲存體帳戶 toohello 新預設儲存體帳戶中的下列命令 toocopy 檔案。 取代 PowerShell 傳回 hello 容器資訊的容器。 取代__帳戶__hello 帳戶名稱。 Hello 路徑 toodata 取代 hello 路徑 tooa 資料檔案。

    ```bash
    hdfs dfs -cp wasb://CONTAINER@ACCOUNT.blob.core.windows.net/path/to/old/data /path/to/new/location
    ```

    > [!NOTE]
    > 如果 hello 目錄結構，其中包含 hello 資料不存在於 hello 測試環境中，您可以建立使用 hello 下列命令：

    ```bash
    hdfs dfs -mkdir -p /new/path/to/create
    ```

    hello`-p`參數可讓 hello 建立 hello 路徑中的所有目錄。

#### <a name="direct-copy-between-blobs-in-azure-storage"></a>在 Azure 儲存體中的 Blob 之間直接複製

或者，您可能想 toouse hello`Start-AzureStorageBlobCopy`之間 HDInsight 之外的儲存體帳戶的 Azure PowerShell cmdlet toocopy blob。 如需詳細資訊，請參閱 hello 如何 toomanage 與 Azure 儲存體使用 Azure PowerShell 的 Azure Blob > 一節。

## <a name="client-side-technologies"></a>用戶端技術

用戶端技術，例如[Azure PowerShell cmdlet](/powershell/azureps-cmdlets-docs)， [Azure CLI](../cli-install-nodejs.md)，或使用 hello [Hadoop 的.NET SDK](https://hadoopsdk.codeplex.com/)繼續 toowork linux 叢集。 這些技術依賴 REST hello 相同跨兩個叢集作業系統類型的 Api。

## <a name="server-side-technologies"></a>伺服器端技術

下表中的 hello 移轉是 Windows 特定的伺服器端元件提供指引。

| 如果您正在使用這項技術... | 請執行此動作... |
| --- | --- |
| **PowerShell** (伺服器端指令碼，包含於叢集建立期間使用的指令碼動作) |重寫為 Bash 指令碼。 針對指令碼動作，請參閱[使用指令碼動作自訂 Linux 型 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)和[以 Linux 為基礎之 HDInsight 的指令碼動作開發](hdinsight-hadoop-script-actions-linux.md)。 |
| **Azure CLI** (伺服器端指令碼) |Hello Azure CLI Linux 上的可用時，它不會顯示預先安裝在 hello HDInsight 叢集前端節點上。 如需有關如何安裝 hello Azure CLI 的詳細資訊，請參閱[開始使用 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)。 |
| **.NET 元件** |以 Linux 為基礎的 HDInsight 透過 [Mono](https://mono-project.com) 支援 .NET。 如需詳細資訊，請參閱[移轉.NET 方案 tooLinux 為基礎的 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)。 |
| **Win32 元件或其他僅限 Windows 的技術** |指引取決於 hello 元件或技術。 您可能無法 toofind 與 Linux 相容的版本，或您可能需要 toofind 替代解決方案，或重寫此元件。 |

> [!IMPORTANT]
> hello HDInsight 管理 SDK 不是與 單聲道完全相容。 它不應為方案的一部分已 toohello HDInsight 叢集部署在這個階段。

## <a name="cluster-creation"></a>叢集建立

本節將提供叢集建立之差異的資訊。

### <a name="ssh-user"></a>SSH 使用者

以 Linux 為基礎的 HDInsight 叢集使用 hello**安全殼層 (SSH)**通訊協定 tooprovide 遠端存取 toohello 叢集節點。 不同於以 Windows 為基礎之叢集的遠端桌面，大部分的 SSH 用戶端不提供圖形化使用者體驗。 相反地，SSH 用戶端提供可讓您在 hello 叢集的 toorun 命令的命令列。 某些用戶端 (例如[MobaXterm](http://mobaxterm.mobatek.net/)) 提供圖形化的檔案系統瀏覽器加法 tooa 遠端命令列中。

在叢集建立期間，您必須提供 SSH 使用者，以及**密碼**或**公開金鑰憑證**以進行驗證。

我們建議使用公開金鑰憑證，因為它比密碼更安全。 憑證驗證的運作方式產生帶正負號的 public/private 金鑰組，然後建立 hello 叢集時，提供 hello 公開金鑰。 連接時使用 SSH toohello 伺服器，hello hello 用戶端上的私用金鑰提供 hello 連線的驗證。

如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。

### <a name="cluster-customization"></a>叢集自訂

**指令碼動作** 必須以 Bash 指令碼撰寫。 雖然您可以使用指令碼動作在叢集建立期間，以 Linux 為基礎的叢集，也可以使用的 tooperform 自訂之後叢集已啟動和執行。 如需詳細資訊，請參閱[使用指令碼動作自訂 Linux 型 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)和[以 Linux 為基礎之 HDInsight 的指令碼動作開發](hdinsight-hadoop-script-actions-linux.md)。

另一個自訂功能是 **bootstrap**。 適用於 Windows 叢集，這項功能可讓您 toospecify hello 位置的登錄區搭配使用的其他程式庫。 叢集建立之後，這些程式庫會自動提供用於 Hive 查詢沒有 hello 需要 toouse `ADD JAR`。

hello 啟動程序以 Linux 為基礎的叢集功能不提供這項功能。 請改為使用 [在叢集建立期間新增 Hive 程式庫](hdinsight-hadoop-add-hive-libraries.md)中所記錄的指令碼動作。

### <a name="virtual-networks"></a>虛擬網路

以 Windows 為基礎的 HDInsight 僅支援傳統虛擬網路，而以 Linux 為基礎的 HDInsight 則需要資源管理員虛擬網路。 如果您在資源 hello Linux HDInsight 叢集的傳統的虛擬網路必須連接到，請參閱[連接傳統虛擬網路 tooa 資源管理員虛擬網路](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md)。

如需搭配 HDInsight 使用 Azure 虛擬網路之設定需求的詳細資訊，請參閱 [使用虛擬網路延伸 HDInsight 功能](hdinsight-extend-hadoop-virtual-network.md)。

## <a name="management-and-monitoring"></a>管理與監視

許多的 hello web Ui，您可能已經使用以 Windows 為基礎的 HDInsight，例如作業歷程記錄或 Yarn UI 都可透過 Ambari。 此外，hello Ambari Hive 檢視提供方式 toorun 使用網頁瀏覽器的 Hive 查詢。 在 https://CLUSTERNAME.azurehdinsight.net 以 Linux 為基礎的叢集上使用 hello Ambari Web UI。

如需使用 Ambari 的詳細資訊，請參閱下列文件的 hello:

* [Ambari Web](hdinsight-hadoop-manage-ambari.md)
* [Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md)

### <a name="ambari-alerts"></a>Ambari 警示

Ambari 有可以告訴您 hello 叢集中的潛在問題的警示系統。 不過，您也可以擷取它們透過 hello REST API，警示會顯示為紅色或黃色中 hello Ambari Web UI 中的項目。

> [!IMPORTANT]
> Ambari 警示代表「可能有」問題，而不表示「已發生」問題。 例如，您可能會收到無法存取 HiveServer2 的警示，但實際上您仍然可以正常存取它。
>
> 許多警示都是針對某項服務實作為以間隔為基礎的查詢，並會預期在特定的時間範圍內收到回應。 因此 hello 警示並不一定表示 hello 服務已關閉，它未傳回預期的 hello 時間範圍內的結果。

您應先評估某個警示是否已長時間持續發生，或者是否與使用者所回報的某個問題有關，再對它採取動作。

## <a name="file-system-locations"></a>檔案系統位置

hello Linux 叢集檔案系統的方式不同於 Windows 為基礎的 HDInsight 叢集配置。 使用下列資料表 toofind 常用檔案 hello。

| 我需要 toofind... | 它位於... |
| --- | --- |
| 組態 |`/etc`。 例如， `/etc/hadoop/conf/core-site.xml` |
| 記錄檔 |`/var/logs` |
| Hortonworks Data Platform (HDP) |`/usr/hdp`.有兩個目錄位在此處，其中是目前 HDP 版本 hello 和`current`。 hello`current`目錄包含符號連結 toofiles 和 hello 版本號碼的目錄中的目錄。 hello`current`目錄已提供作為便利的方式存取自 hello 變更版本號碼為 hello HDP HDP 檔案的版本會更新。 |
| hadoop-streaming.jar |`/usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar` |

一般情況下，如果您知道 hello hello 檔案名稱，您可以使用 hello SSH 工作階段 toofind hello 檔案路徑中的下列命令：

    find / -name FILENAME 2>/dev/null

您也可以使用萬用字元 hello 檔案名稱。 例如，`find / -name *streaming*.jar 2>/dev/null`傳回 hello 路徑 tooany jar 檔案包含 hello 字 '串流' hello 檔案名稱的一部分。

## <a name="hive-pig-and-mapreduce"></a>Hive、Pig 及 MapReduce

Pig 和 MapReduce 工作負載在 Linux 為基礎的叢集上很相似。 不過，您可以使用較新版本的 Hadoop、Hive 和 Pig 建立以 Linux 為基礎的 HDInsight 叢集。 這些版本的差異可能會對您現有方案的運作方式造成變更。 Hello 版本的元件，包含在 HDInsight 上的詳細資訊，請參閱[HDInsight 的元件版本控制](hdinsight-component-versioning.md)。

以 Linux 為基礎的 HDInsight 不提供遠端桌面功能。 相反地，您可以使用 SSH tooremotely 連接 toohello 叢集前端節點。 如需詳細資訊，請參閱下列文件的 hello:

* [搭配 SSH 使用 Hive](hdinsight-hadoop-use-hive-ssh.md)
* [搭配 SSH 使用 Pig](hdinsight-hadoop-use-pig-ssh.md)
* [搭配 SSH 使用 MapReduce](hdinsight-hadoop-use-mapreduce-ssh.md)

### <a name="hive"></a>Hive

> [!IMPORTANT]
> 如果您使用外部的 Hive 中繼存放區，您應該備份之前使用 linux 的 HDInsight hello 中繼存放區。 以 Linux 為基礎的 HDInsight 可搭配較新版本的 Hive 使用，但可能會與舊版建立的中繼存放區不相容。

hello 下列圖表會提供有關移轉您的登錄區工作負載的指引。

| 以 Windows 為基礎時，我是使用... | 以 Linux 為基礎時... |
| --- | --- |
| **Hive 編輯器** |[Ambari 中的 Hive 檢視](hdinsight-hadoop-use-hive-ambari-view.md) |
| `set hive.execution.engine=tez;`tooenable Tez |Tez hello linux 叢集的預設執行引擎，因此 hello 設定陳述式已不再需要。 |
| C# 使用者定義函數 | 驗證 C# 元件，以 Linux 為基礎的 HDInsight 上的資訊，請參閱[移轉.NET 方案 tooLinux 為基礎的 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| CMD 檔案或登錄區工作的一部分叫用的 hello 伺服器上的指令碼 |使用 Bash 指令碼 |
| `hive` 命令 |使用 [Beeline](hdinsight-hadoop-use-hive-beeline.md) 或是[來自 SSH 工作階段的 Hive](hdinsight-hadoop-use-hive-ssh.md) |

### <a name="pig"></a>Pig

| 以 Windows 為基礎時，我是使用... | 以 Linux 為基礎時... |
| --- | --- |
| C# 使用者定義函數 | 驗證 C# 元件，以 Linux 為基礎的 HDInsight 上的資訊，請參閱[移轉.NET 方案 tooLinux 為基礎的 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| CMD 檔案或 hello 叫用 Pig 工作的一部分的伺服器上的指令碼 |使用 Bash 指令碼 |

### <a name="mapreduce"></a>MapReduce

| 以 Windows 為基礎時，我是使用... | 以 Linux 為基礎時... |
| --- | --- |
| C# 對應器和歸納器元件 | 驗證 C# 元件，以 Linux 為基礎的 HDInsight 上的資訊，請參閱[移轉.NET 方案 tooLinux 為基礎的 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md) |
| CMD 檔案或登錄區工作的一部分叫用的 hello 伺服器上的指令碼 |使用 Bash 指令碼 |

## <a name="oozie"></a>Oozie

> [!IMPORTANT]
> 如果您使用外部的 Oozie 中繼存放區，您應該備份之前使用 linux 的 HDInsight hello 中繼存放區。 以 Linux 為基礎的 HDInsight 可搭配較新版本的 Oozie 使用，但可能會與舊版建立的中繼存放區不相容。

Oozie 工作流程允許殼層動作。 殼層動作會使用 hello 預設殼層的 hello 作業系統 toorun 命令列命令。 如果您擁有 hello Windows shell 所依賴的 Oozie 工作流程時，您必須重新撰寫 hello 工作流程 toorely hello Linux shell 環境 (Bash)。 如需使用 Oozie 殼層動作的詳細資訊，請參閱 [Oozie 殼層動作擴充功能](http://oozie.apache.org/docs/3.3.0/DG_ShellActionExtension.html)。

如果您有依賴 C# 應用程式 (透過殼層動作叫用) 的 Oozie 工作流程，您必須在 Linux 環境中驗證這些應用程式。 如需詳細資訊，請參閱[移轉.NET 方案 tooLinux 為基礎的 HDInsight](hdinsight-hadoop-migrate-dotnet-to-linux.md)。

## <a name="storm"></a>Storm

| 以 Windows 為基礎時，我是使用... | 以 Linux 為基礎時... |
| --- | --- |
| Storm Dashboard |hello Storm 儀表板就無法使用。 請參閱[以 Linux 為基礎的 HDInsight 上的部署和管理 Storm 拓撲](hdinsight-storm-deploy-monitor-topology-linux.md)方式 toosubmit 拓撲 |
| Storm UI |hello Storm UI 位於 https://CLUSTERNAME.azurehdinsight.net/stormui |
| Visual Studio toocreate，部署和管理 C# 或混合式拓撲 |Visual Studio 可以是使用的 toocreate、 部署和管理 C# (SCP.NET) 或 2016 年 10 月 28 之後建立的 HDInsight 叢集上的 linux Storm 上的混合式拓撲。 |

## <a name="hbase"></a>HBase

以 Linux 為基礎的叢集上 HBase hello znode 父系是`/hbase-unsecure`。 使用原生 HBase Java 應用程式開發介面的任何 Java 用戶端應用程式的 hello 組態中設定此值。

如需設定此值的範例用戶端，請參閱 [建置以 Java 為基礎的 HBase 應用程式](hdinsight-hbase-build-java-maven.md) 。

## <a name="spark"></a>Spark

Spark 叢集可以在 Windows 叢集預覽期間取得。 Spark GA 只適用於以 Linux 為基礎的叢集。 沒有從 Windows 型的 Spark 預覽叢集 tooa 版本以 Linux 為基礎的 Spark 叢集移轉路徑。

## <a name="known-issues"></a>已知問題

### <a name="azure-data-factory-custom-net-activities"></a>Azure Data Factory 自訂 .NET 活動

Azure Data Factory 自訂 .NET 活動目前並不受以 Linux 為基礎的 HDInsight 叢集所支援。 相反地，您應該使用其中一個 hello 遵循方法 tooimplement 自訂活動做為 ADF 管線的一部分。

* 在 Azure Batch 集區上執行 .NET 活動。 請參閱 hello 使用 Azure Batch 連結服務區段[Azure Data Factory 管線中使用自訂活動](../data-factory/data-factory-use-custom-activities.md)
* 實作 MapReduce 活動與 hello 活動。 如需詳細資訊，請參閱[從 Data Factory 叫用 MapReduce 程式](../data-factory/data-factory-map-reduce.md)。

### <a name="line-endings"></a>行尾結束符號

通常來說，以 Windows 為基礎之系統上的行尾結束符號是使用 CRLF，而以 Linux 為基礎的系統則使用 LF。 如果您產生，或預期的方式，與 CRLF 行尾結束符號的資料，您可能需要 toomodify hello 產生者或消費者 toowork 與 hello LF 行尾結束符號。

比方說，HDInsight 在 Windows 叢集上的使用 Azure PowerShell tooquery 傳回 CRLF 與資料。 hello 與 linux 叢集的同一個查詢傳回 LF。 如果 hello 行尾結束符號會導致您 solutuion 問題移轉之前，您應該測試 toosee tooa linux 叢集。

如果您有直接在 hello Linux 叢集節點執行的指令碼，您應該一律使用 LF 為 hello 行尾結束符號。 如果您使用 CRLF，您可能以 Linux 為基礎的叢集上執行 hello 指令碼時發現錯誤。

如果您知道 hello 指令碼不會包含具有內嵌 CR 字元的字串，您就可以大量變更 hello 行尾使用其中一種 hello 下列方法：

* **上傳 toohello 叢集之前**： 使用 hello CRLF tooLF 中的下列 PowerShell 陳述式 toochange hello 行尾結束符號，再上傳 hello 指令碼 toohello 叢集。

    ```powershell
    $original_file ='c:\path\to\script.py'
    $text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
    [IO.File]::WriteAllText($original_file, $text)
    ```

* **上傳 toohello 叢集後**： 使用 hello 下列命令從 SSH 工作階段 toohello linux 叢集 toomodify hello 指令碼。

    ```bash
    hdfs dfs -get wasb:///path/to/script.py oldscript.py
    tr -d '\r' < oldscript.py > script.py
    hdfs dfs -put -f script.py wasb:///path/to/script.py
    ```

## <a name="next-steps"></a>後續步驟

* [了解如何 toocreate 以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)
* [使用 SSH tooconnect tooHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)
* [使用 Ambari 管理 Linux 型叢集](hdinsight-hadoop-manage-ambari.md)
