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
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a><span data-ttu-id="d5754-103">使用 Azure PowerShell 管理 HDInsight 上的 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="d5754-103">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="d5754-104">Azure PowerShell 是一種強大的指令碼環境，您可以使用 toocontrol 並自動化 hello 部署和管理您在 Azure 中的工作負載。</span><span class="sxs-lookup"><span data-stu-id="d5754-104">Azure PowerShell is a powerful scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="d5754-105">在本文中，您將學習如何在 Azure HDInsight 中使用本機的 Azure PowerShell 主控台，透過 hello 的 toomanage Hadoop 叢集使用的 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="d5754-105">In this article, you will learn how toomanage Hadoop clusters in Azure HDInsight by using a local Azure PowerShell console through hello use of Windows PowerShell.</span></span> <span data-ttu-id="d5754-106">如 hello hello HDInsight PowerShell cmdlet 清單，請參閱[HDInsight cmdlet 參考][hdinsight-powershell-reference]。</span><span class="sxs-lookup"><span data-stu-id="d5754-106">For hello list of hello HDInsight PowerShell cmdlets, see [HDInsight cmdlet reference][hdinsight-powershell-reference].</span></span>

<span data-ttu-id="d5754-107">**必要條件**</span><span class="sxs-lookup"><span data-stu-id="d5754-107">**Prerequisites**</span></span>

<span data-ttu-id="d5754-108">在開始這份文件之前，您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="d5754-108">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="d5754-109">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="d5754-109">**An Azure subscription**.</span></span> <span data-ttu-id="d5754-110">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="d5754-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="d5754-111">安裝 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5754-111">Install Azure PowerShell</span></span>
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="d5754-112">如果您已安裝 Azure PowerShell 0.9 x 版，必須先解除安裝然後再安裝較新版本。</span><span class="sxs-lookup"><span data-stu-id="d5754-112">If you have installed Azure PowerShell version 0.9x, you must uninstall it before installing a newer version.</span></span>

<span data-ttu-id="d5754-113">安裝 PowerShell hello toocheck hello 版本：</span><span class="sxs-lookup"><span data-stu-id="d5754-113">toocheck hello version of hello installed PowerShell:</span></span>

    Get-Module *azure*

<span data-ttu-id="d5754-114">toouninstall hello 較舊版本，在 hello 控制台中執行 程式和功能。</span><span class="sxs-lookup"><span data-stu-id="d5754-114">toouninstall hello older version, run Programs and Features in hello control panel.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="d5754-115">建立叢集</span><span class="sxs-lookup"><span data-stu-id="d5754-115">Create clusters</span></span>
<span data-ttu-id="d5754-116">請參閱 [使用 Azure PowerShell 在 HDInsight 中建立以 Linux 為基礎的叢集](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="d5754-116">See [Create Linux-based clusters in HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="d5754-117">列出叢集</span><span class="sxs-lookup"><span data-stu-id="d5754-117">List clusters</span></span>
<span data-ttu-id="d5754-118">使用下列命令 toolist hello 所有叢集 hello 目前訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="d5754-118">Use hello following command toolist all clusters in hello current subscription:</span></span>

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a><span data-ttu-id="d5754-119">顯示叢集</span><span class="sxs-lookup"><span data-stu-id="d5754-119">Show cluster</span></span>
<span data-ttu-id="d5754-120">使用下列命令 tooshow 詳細資料的特定群集 hello 目前訂用帳戶中的 hello:</span><span class="sxs-lookup"><span data-stu-id="d5754-120">Use hello following command tooshow details of a specific cluster in hello current subscription:</span></span>

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a><span data-ttu-id="d5754-121">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="d5754-121">Delete clusters</span></span>
<span data-ttu-id="d5754-122">使用下列命令 toodelete 叢集中的 hello:</span><span class="sxs-lookup"><span data-stu-id="d5754-122">Use hello following command toodelete a cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

<span data-ttu-id="d5754-123">您也可以藉由移除 hello 資源群組含有 hello 叢集刪除叢集。</span><span class="sxs-lookup"><span data-stu-id="d5754-123">You can also delete a cluster by removing hello resource group that contains hello cluster.</span></span> <span data-ttu-id="d5754-124">請注意，這將刪除 hello 群組包括 hello 預設儲存體帳戶中的所有 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="d5754-124">Please note, this will delete all hello resources in hello group including hello default storage account.</span></span>

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="d5754-125">調整叢集</span><span class="sxs-lookup"><span data-stu-id="d5754-125">Scale clusters</span></span>
<span data-ttu-id="d5754-126">hello 叢集擴充功能可讓您在 Azure HDInsight 中執行而不需要 toore 叢集所用的背景工作節點 toochange hello 數-建立 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="d5754-126">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="d5754-127">只支援使用 HDInsight 3.1.3 版或更高版本的叢集。</span><span class="sxs-lookup"><span data-stu-id="d5754-127">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="d5754-128">如果您不確定您的叢集 hello 版本，您可以檢查 hello 屬性頁面。</span><span class="sxs-lookup"><span data-stu-id="d5754-128">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="d5754-129">請參閱[列出和顯示叢集](hdinsight-administer-use-portal-linux.md#list-and-show-clusters)。</span><span class="sxs-lookup"><span data-stu-id="d5754-129">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="d5754-130">hello 變更造成的影響 hello 支援 HDInsight 叢集的每種類型的資料節點數目：</span><span class="sxs-lookup"><span data-stu-id="d5754-130">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="d5754-131">Hadoop</span><span class="sxs-lookup"><span data-stu-id="d5754-131">Hadoop</span></span>

    <span data-ttu-id="d5754-132">您可以順暢地增加 hello Hadoop 叢集中執行而不會影響任何暫止或執行工作的背景工作節點數。</span><span class="sxs-lookup"><span data-stu-id="d5754-132">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="d5754-133">Hello 作業正在進行時，也可以提交新的作業。</span><span class="sxs-lookup"><span data-stu-id="d5754-133">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="d5754-134">使 hello 叢集一律會保持在運作狀態，是依正常程序處理中縮放作業失敗。</span><span class="sxs-lookup"><span data-stu-id="d5754-134">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>

    <span data-ttu-id="d5754-135">當在 Hadoop 叢集縮小藉由減少 hello 資料節點數時，部分 hello hello 叢集中的服務會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="d5754-135">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="d5754-136">這會導致所有執行和暫止的工作 toofail hello hello 調整大小作業完成時。</span><span class="sxs-lookup"><span data-stu-id="d5754-136">This causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="d5754-137">您可以不過，再重新送出 hello 工作一旦 hello 作業已完成。</span><span class="sxs-lookup"><span data-stu-id="d5754-137">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="d5754-138">HBase</span><span class="sxs-lookup"><span data-stu-id="d5754-138">HBase</span></span>

    <span data-ttu-id="d5754-139">順暢地，您可以新增或移除節點 tooyour HBase 叢集正在執行時。</span><span class="sxs-lookup"><span data-stu-id="d5754-139">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="d5754-140">完成 hello 調整大小作業的幾分鐘內自動平衡地區的伺服器。</span><span class="sxs-lookup"><span data-stu-id="d5754-140">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="d5754-141">不過，您就可以手動平衡 hello 地區的伺服器登入以 toohello 叢集前端節點的叢集和執行 hello 的命令提示字元視窗中的下列命令：</span><span class="sxs-lookup"><span data-stu-id="d5754-141">However, you can also manually balance hello regional servers by logging in toohello headnode of cluster and running hello following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="d5754-142">Storm</span><span class="sxs-lookup"><span data-stu-id="d5754-142">Storm</span></span>

    <span data-ttu-id="d5754-143">順暢地，您可以新增或移除在執行時的資料節點 tooyour Storm 叢集。</span><span class="sxs-lookup"><span data-stu-id="d5754-143">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="d5754-144">但是 hello 調整大小作業順利完成之後, 您將需要 toorebalance hello 拓撲。</span><span class="sxs-lookup"><span data-stu-id="d5754-144">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>

    <span data-ttu-id="d5754-145">您可以使用兩種方式來完成重新平衡作業：</span><span class="sxs-lookup"><span data-stu-id="d5754-145">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="d5754-146">Storm Web UI</span><span class="sxs-lookup"><span data-stu-id="d5754-146">Storm web UI</span></span>
  * <span data-ttu-id="d5754-147">命令列介面 (CLI) 工具</span><span class="sxs-lookup"><span data-stu-id="d5754-147">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="d5754-148">請參閱 toohello [Apache Storm 文件](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d5754-148">Please refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="d5754-149">hello Storm web UI 是在 hello HDInsight 叢集上使用：</span><span class="sxs-lookup"><span data-stu-id="d5754-149">hello Storm web UI is available on hello HDInsight cluster:</span></span>

    ![hdinsight storm scale rebalance](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    <span data-ttu-id="d5754-151">以下是範例如何 toouse hello CLI 命令 toorebalance hello Storm 拓撲：</span><span class="sxs-lookup"><span data-stu-id="d5754-151">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="d5754-152">toochange hello Hadoop 叢集大小，使用 Azure PowerShell，執行下列命令，從用戶端電腦的 hello:</span><span class="sxs-lookup"><span data-stu-id="d5754-152">toochange hello Hadoop cluster size by using Azure PowerShell, run hello following command from a client machine:</span></span>

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a><span data-ttu-id="d5754-153">授與/撤銷存取權</span><span class="sxs-lookup"><span data-stu-id="d5754-153">Grant/revoke access</span></span>
<span data-ttu-id="d5754-154">HDInsight 叢集都有下列 （所有這些服務有 RESTful 端點） 的 HTTP web 服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="d5754-154">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="d5754-155">ODBC</span><span class="sxs-lookup"><span data-stu-id="d5754-155">ODBC</span></span>
* <span data-ttu-id="d5754-156">JDBC</span><span class="sxs-lookup"><span data-stu-id="d5754-156">JDBC</span></span>
* <span data-ttu-id="d5754-157">Ambari</span><span class="sxs-lookup"><span data-stu-id="d5754-157">Ambari</span></span>
* <span data-ttu-id="d5754-158">Oozie</span><span class="sxs-lookup"><span data-stu-id="d5754-158">Oozie</span></span>
* <span data-ttu-id="d5754-159">Templeton</span><span class="sxs-lookup"><span data-stu-id="d5754-159">Templeton</span></span>

<span data-ttu-id="d5754-160">預設會授與這些服務的存取權。</span><span class="sxs-lookup"><span data-stu-id="d5754-160">By default, these services are granted for access.</span></span> <span data-ttu-id="d5754-161">您可以撤銷/授與 hello 存取。</span><span class="sxs-lookup"><span data-stu-id="d5754-161">You can revoke/grant hello access.</span></span> <span data-ttu-id="d5754-162">toorevoke:</span><span class="sxs-lookup"><span data-stu-id="d5754-162">toorevoke:</span></span>

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

<span data-ttu-id="d5754-163">toogrant:</span><span class="sxs-lookup"><span data-stu-id="d5754-163">toogrant:</span></span>

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
> <span data-ttu-id="d5754-164">授與/撤銷 hello 存取權，您將會重設 hello 叢集使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="d5754-164">By granting/revoking hello access, you will reset hello cluster user name and password.</span></span>
>
>

<span data-ttu-id="d5754-165">這也可以透過 hello 入口網站來完成。</span><span class="sxs-lookup"><span data-stu-id="d5754-165">This can also be done via hello Portal.</span></span> <span data-ttu-id="d5754-166">請參閱[管理 HDInsight 使用 hello Azure 入口網站][hdinsight-admin-portal]。</span><span class="sxs-lookup"><span data-stu-id="d5754-166">See [Administer HDInsight by using hello Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="d5754-167">更新 HTTP 使用者認證</span><span class="sxs-lookup"><span data-stu-id="d5754-167">Update HTTP user credentials</span></span>
<span data-ttu-id="d5754-168">它是相同的 hello 與程序[Grant/revoke HTTP 存取](#grant/revoke-access)。如果已授與 hello 叢集 hello HTTP 存取，您必須先撤銷。</span><span class="sxs-lookup"><span data-stu-id="d5754-168">It is hello same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If hello cluster has been granted hello HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="d5754-169">然後授與 hello 存取以新的 HTTP 使用者認證。</span><span class="sxs-lookup"><span data-stu-id="d5754-169">And then grant hello access with new HTTP user credentials.</span></span>

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="d5754-170">找不到 hello 預設儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="d5754-170">Find hello default storage account</span></span>
<span data-ttu-id="d5754-171">hello 下列 Powershell 指令碼示範如何 tooget hello 預設儲存體帳戶名稱和 hello 叢集的預設儲存體帳戶金鑰。</span><span class="sxs-lookup"><span data-stu-id="d5754-171">hello following Powershell script demonstrates how tooget hello default storage account name and hello default storage account key for a cluster.</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-hello-resource-group"></a><span data-ttu-id="d5754-172">找不到 hello 資源群組</span><span class="sxs-lookup"><span data-stu-id="d5754-172">Find hello resource group</span></span>
<span data-ttu-id="d5754-173">在 hello 資源管理員模式中，每個 HDInsight 叢集所屬 tooan Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="d5754-173">In hello Resource Manager mode, each HDInsight cluster belongs tooan Azure resource group.</span></span>  <span data-ttu-id="d5754-174">toofind hello 資源群組：</span><span class="sxs-lookup"><span data-stu-id="d5754-174">toofind hello resource group:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a><span data-ttu-id="d5754-175">提交工作</span><span class="sxs-lookup"><span data-stu-id="d5754-175">Submit jobs</span></span>
<span data-ttu-id="d5754-176">**toosubmit MapReduce 工作**</span><span class="sxs-lookup"><span data-stu-id="d5754-176">**toosubmit MapReduce jobs**</span></span>

<span data-ttu-id="d5754-177">請參閱 [在以 Windows 為基礎的 HDInsight 中執行 Hadoop MapReduce 範例](hdinsight-run-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="d5754-177">See [Run Hadoop MapReduce samples in Windows-based HDInsight](hdinsight-run-samples.md).</span></span>

<span data-ttu-id="d5754-178">**toosubmit Hive 工作**</span><span class="sxs-lookup"><span data-stu-id="d5754-178">**toosubmit Hive jobs**</span></span>

<span data-ttu-id="d5754-179">請參閱 [使用 PowerShell 執行 Hive 查詢](hdinsight-hadoop-use-hive-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="d5754-179">See [Run Hive queries using PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span></span>

<span data-ttu-id="d5754-180">**toosubmit Pig 工作**</span><span class="sxs-lookup"><span data-stu-id="d5754-180">**toosubmit Pig jobs**</span></span>

<span data-ttu-id="d5754-181">請參閱 [使用 PowerShell 執行 Pig 作業](hdinsight-hadoop-use-pig-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="d5754-181">See [Run Pig jobs using PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span></span>

<span data-ttu-id="d5754-182">**toosubmit Sqoop 作業**</span><span class="sxs-lookup"><span data-stu-id="d5754-182">**toosubmit Sqoop jobs**</span></span>

<span data-ttu-id="d5754-183">請參閱 [在 HDInsight 上使用 Sqoop](hdinsight-use-sqoop.md)。</span><span class="sxs-lookup"><span data-stu-id="d5754-183">See [Use Sqoop with HDInsight](hdinsight-use-sqoop.md).</span></span>

<span data-ttu-id="d5754-184">**toosubmit Oozie 工作**</span><span class="sxs-lookup"><span data-stu-id="d5754-184">**toosubmit Oozie jobs**</span></span>

<span data-ttu-id="d5754-185">請參閱[Hadoop toodefine 與執行 HDInsight 中的工作流程使用 Oozie](hdinsight-use-oozie.md)。</span><span class="sxs-lookup"><span data-stu-id="d5754-185">See [Use Oozie with Hadoop toodefine and run a workflow in HDInsight](hdinsight-use-oozie.md).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="d5754-186">上傳資料 tooAzure Blob 儲存體</span><span class="sxs-lookup"><span data-stu-id="d5754-186">Upload data tooAzure Blob storage</span></span>
<span data-ttu-id="d5754-187">請參閱[上傳資料 tooHDInsight][hdinsight-upload-data]。</span><span class="sxs-lookup"><span data-stu-id="d5754-187">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="d5754-188">另請參閱</span><span class="sxs-lookup"><span data-stu-id="d5754-188">See Also</span></span>
* <span data-ttu-id="d5754-189">[HDInsight Cmdlet 參考文件][hdinsight-powershell-reference]</span><span class="sxs-lookup"><span data-stu-id="d5754-189">[HDInsight cmdlet reference documentation][hdinsight-powershell-reference]</span></span>
* <span data-ttu-id="d5754-190">[使用 hello Azure 入口網站來管理 HDInsight][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="d5754-190">[Administer HDInsight by using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="d5754-191">[使用命令列介面管理 HDInsight][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="d5754-191">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="d5754-192">[建立 HDInsight 叢集][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="d5754-192">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="d5754-193">[上傳資料 tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="d5754-193">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="d5754-194">[以程式設計方式提交 Hadoop 工作][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="d5754-194">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="d5754-195">[開始使用 Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="d5754-195">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

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
