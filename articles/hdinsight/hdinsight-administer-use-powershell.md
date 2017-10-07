---
title: "使用 PowerShell 的 Azure HDInsight 叢集 aaaManage Hadoop |Microsoft 文件"
description: "了解如何 tooperform 系統管理工作 hello 中使用 Azure PowerShell HDInsight Hadoop 叢集。"
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: bfdfa754-18e5-4ef9-b0d6-2dbdcebc0283
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 3df082d752fa8c703db82a54b82b740290af6729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a>使用 Azure PowerShell 管理 HDInsight 上的 Hadoop 叢集
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Azure PowerShell 是一種強大的指令碼環境，您可以使用 toocontrol 並自動化 hello 部署和管理您在 Azure 中的工作負載。 在本文中，您將學習如何在 Azure HDInsight 中使用本機的 Azure PowerShell 主控台，透過 hello 的 toomanage Hadoop 叢集使用的 Windows PowerShell。 如 hello hello HDInsight PowerShell cmdlet 清單，請參閱[HDInsight cmdlet 參考][hdinsight-powershell-reference]。

**必要條件**

在開始這份文件之前，您必須擁有 hello 下列：

* **Azure 訂用帳戶**。 請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。

## <a name="install-azure-powershell"></a>安裝 Azure PowerShell
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

如果您已安裝 Azure PowerShell 0.9 x 版，必須先解除安裝然後再安裝較新版本。

安裝 PowerShell hello toocheck hello 版本：

    Get-Module *azure*

toouninstall hello 較舊版本，在 hello 控制台中執行 程式和功能。

## <a name="create-clusters"></a>建立叢集
請參閱 [使用 Azure PowerShell 在 HDInsight 中建立以 Linux 為基礎的叢集](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)

## <a name="list-clusters"></a>列出叢集
使用下列命令 toolist hello 所有叢集 hello 目前訂用帳戶：

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a>顯示叢集
使用下列命令 tooshow 詳細資料的特定群集 hello 目前訂用帳戶中的 hello:

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a>刪除叢集
使用下列命令 toodelete 叢集中的 hello:

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

您也可以藉由移除 hello 資源群組含有 hello 叢集刪除叢集。 請注意，這將刪除 hello 群組包括 hello 預設儲存體帳戶中的所有 hello 資源。

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a>調整叢集
hello 叢集擴充功能可讓您在 Azure HDInsight 中執行而不需要 toore 叢集所用的背景工作節點 toochange hello 數-建立 hello 叢集。

> [!NOTE]
> 只支援使用 HDInsight 3.1.3 版或更高版本的叢集。 如果您不確定您的叢集 hello 版本，您可以檢查 hello 屬性頁面。  請參閱[列出和顯示叢集](hdinsight-administer-use-portal-linux.md#list-and-show-clusters)。
>
>

hello 變更造成的影響 hello 支援 HDInsight 叢集的每種類型的資料節點數目：

* Hadoop

    您可以順暢地增加 hello Hadoop 叢集中執行而不會影響任何暫止或執行工作的背景工作節點數。 Hello 作業正在進行時，也可以提交新的作業。 使 hello 叢集一律會保持在運作狀態，是依正常程序處理中縮放作業失敗。

    當在 Hadoop 叢集縮小藉由減少 hello 資料節點數時，部分 hello hello 叢集中的服務會重新啟動。 這會導致所有執行和暫止的工作 toofail hello hello 調整大小作業完成時。 您可以不過，再重新送出 hello 工作一旦 hello 作業已完成。
* HBase

    順暢地，您可以新增或移除節點 tooyour HBase 叢集正在執行時。 完成 hello 調整大小作業的幾分鐘內自動平衡地區的伺服器。 不過，您就可以手動平衡 hello 地區的伺服器登入以 toohello 叢集前端節點的叢集和執行 hello 的命令提示字元視窗中的下列命令：

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* Storm

    順暢地，您可以新增或移除在執行時的資料節點 tooyour Storm 叢集。 但是 hello 調整大小作業順利完成之後, 您將需要 toorebalance hello 拓撲。

    您可以使用兩種方式來完成重新平衡作業：

  * Storm Web UI
  * 命令列介面 (CLI) 工具

    請參閱 toohello [Apache Storm 文件](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)如需詳細資訊。

    hello Storm web UI 是在 hello HDInsight 叢集上使用：

    ![hdinsight storm scale rebalance](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    以下是範例如何 toouse hello CLI 命令 toorebalance hello Storm 拓撲：

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

toochange hello Hadoop 叢集大小，使用 Azure PowerShell，執行下列命令，從用戶端電腦的 hello:

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a>授與/撤銷存取權
HDInsight 叢集都有下列 （所有這些服務有 RESTful 端點） 的 HTTP web 服務的 hello:

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

預設會授與這些服務的存取權。 您可以撤銷/授與 hello 存取。 toorevoke:

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

toogrant:

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter hello Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter hello HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> 授與/撤銷 hello 存取權，您將會重設 hello 叢集使用者名稱和密碼。
>
>

這也可以透過 hello 入口網站來完成。 請參閱[管理 HDInsight 使用 hello Azure 入口網站][hdinsight-admin-portal]。

## <a name="update-http-user-credentials"></a>更新 HTTP 使用者認證
它是相同的 hello 與程序[Grant/revoke HTTP 存取](#grant/revoke-access)。如果已授與 hello 叢集 hello HTTP 存取，您必須先撤銷。  然後授與 hello 存取以新的 HTTP 使用者認證。

## <a name="find-hello-default-storage-account"></a>找不到 hello 預設儲存體帳戶
hello 下列 Powershell 指令碼示範如何 tooget hello 預設儲存體帳戶名稱和 hello 叢集的預設儲存體帳戶金鑰。

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-hello-resource-group"></a>找不到 hello 資源群組
在 hello 資源管理員模式中，每個 HDInsight 叢集所屬 tooan Azure 資源群組。  toofind hello 資源群組：

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a>提交工作
**toosubmit MapReduce 工作**

請參閱 [在以 Windows 為基礎的 HDInsight 中執行 Hadoop MapReduce 範例](hdinsight-run-samples.md)。

**toosubmit Hive 工作**

請參閱 [使用 PowerShell 執行 Hive 查詢](hdinsight-hadoop-use-hive-powershell.md)。

**toosubmit Pig 工作**

請參閱 [使用 PowerShell 執行 Pig 作業](hdinsight-hadoop-use-pig-powershell.md)。

**toosubmit Sqoop 作業**

請參閱 [在 HDInsight 上使用 Sqoop](hdinsight-use-sqoop.md)。

**toosubmit Oozie 工作**

請參閱[Hadoop toodefine 與執行 HDInsight 中的工作流程使用 Oozie](hdinsight-use-oozie.md)。

## <a name="upload-data-tooazure-blob-storage"></a>上傳資料 tooAzure Blob 儲存體
請參閱[上傳資料 tooHDInsight][hdinsight-upload-data]。

## <a name="see-also"></a>另請參閱
* [HDInsight Cmdlet 參考文件][hdinsight-powershell-reference]
* [使用 hello Azure 入口網站來管理 HDInsight][hdinsight-admin-portal]
* [使用命令列介面管理 HDInsight][hdinsight-admin-cli]
* [建立 HDInsight 叢集][hdinsight-provision]
* [上傳資料 tooHDInsight][hdinsight-upload-data]
* [以程式設計方式提交 Hadoop 工作][hdinsight-submit-jobs]
* [開始使用 Azure HDInsight][hdinsight-get-started]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-ps-provision]: ./media/hdinsight-administer-use-powershell/HDI.PS.Provision.png
