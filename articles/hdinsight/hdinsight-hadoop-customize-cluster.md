---
title: "aaaCustomize HDInsight 叢集使用的指令碼動作-Azure |Microsoft 文件"
description: "了解如何 toocustomize HDInsight 叢集使用指令碼動作。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3a63e216-4163-40c1-aa04-6b42fd0162ad
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 076fff23e016db47bc7e9963582a545ad638e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="265be-103">使用指令碼動作自訂 Windows 型 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="265be-103">Customize Windows-based HDInsight clusters using Script Action</span></span>
<span data-ttu-id="265be-104">**指令碼動作**可以是使用的 tooinvoke[自訂指令碼](hdinsight-hadoop-script-actions.md)hello 叢集建立程序期間在叢集上安裝其他軟體。</span><span class="sxs-lookup"><span data-stu-id="265be-104">**Script Action** can be used tooinvoke [custom scripts](hdinsight-hadoop-script-actions.md) during hello cluster creation process for installing additional software on a cluster.</span></span>

<span data-ttu-id="265be-105">本文章中的 hello 資訊是特定 tooWindows 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="265be-105">hello information in this article is specific tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="265be-106">如果是以 Linux 為基礎的叢集，請參閱 [使用指令碼動作自訂 Linux 型 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="265be-106">For Linux-based clusters, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="265be-107">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="265be-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="265be-108">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="265be-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="265be-109">HDInsight 叢集可以自訂各種不同的其他方式，例如包括額外的 Azure 儲存體帳戶、 變更 hello Hadoop 組態檔 （core-site.xml、 hive-site.xml 等），或加入到共用程式庫 （例如 Hive、 Oozie）一般 hello 叢集中的位置。</span><span class="sxs-lookup"><span data-stu-id="265be-109">HDInsight clusters can be customized in a variety of other ways as well, such as including additional Azure Storage accounts, changing hello Hadoop configuration files (core-site.xml, hive-site.xml, etc.), or adding shared libraries (e.g., Hive, Oozie) into common locations in hello cluster.</span></span> <span data-ttu-id="265be-110">這些自訂可以透過 Azure PowerShell，hello Azure HDInsight.NET SDK 或 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="265be-110">These customizations can be done through Azure PowerShell, hello Azure HDInsight .NET SDK, or hello Azure portal.</span></span> <span data-ttu-id="265be-111">如需詳細資訊，請參閱[在 HDInsight 中建立 Hadoop 叢集][hdinsight-provision-cluster]。</span><span class="sxs-lookup"><span data-stu-id="265be-111">For more information, see [Create Hadoop clusters in HDInsight][hdinsight-provision-cluster].</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-hello-cluster-creation-process"></a><span data-ttu-id="265be-112">Hello 叢集建立程序中的指令碼動作</span><span class="sxs-lookup"><span data-stu-id="265be-112">Script Action in hello cluster creation process</span></span>
<span data-ttu-id="265be-113">Hello 程序所建立的叢集時，才會使用指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="265be-113">Script Action is only used while a cluster is in hello process of being created.</span></span> <span data-ttu-id="265be-114">hello 下列圖表說明 hello 建立程序期間執行指令碼動作時：</span><span class="sxs-lookup"><span data-stu-id="265be-114">hello following diagram illustrates when Script Action is executed during hello creation process:</span></span>

<span data-ttu-id="265be-115">![HDInsight 叢集自訂和叢集建立期間的階段][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="265be-115">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="265be-116">Hello 叢集 hello 指令碼執行時，進入 hello **ClusterCustomization**階段。</span><span class="sxs-lookup"><span data-stu-id="265be-116">When hello script is running, hello cluster enters hello **ClusterCustomization** stage.</span></span> <span data-ttu-id="265be-117">在這個階段，hello 指令碼 hello 系統管理員帳戶下執行，以平行方式在所有 hello 指定 hello 叢集中的節點並可提供完整的系統管理員權限 hello 節點上。</span><span class="sxs-lookup"><span data-stu-id="265be-117">At this stage, hello script is run under hello system admin account, in parallel on all hello specified nodes in hello cluster, and provides full admin privileges on hello nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="265be-118">因為在 hello 期間的叢集節點上的系統管理員權限**ClusterCustomization**階段中，您可以使用 hello 指令碼 tooperform 作業，例如停止和啟動服務，包括 Hadoop 相關服務。</span><span class="sxs-lookup"><span data-stu-id="265be-118">Because you have admin privileges on hello cluster nodes during the **ClusterCustomization** stage, you can use hello script tooperform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="265be-119">因此 hello 指令碼的一部分，您必須確定該 hello Ambari 服務和其他相關的 Hadoop 服務正在執行 hello 指令碼完成執行之前完成。</span><span class="sxs-lookup"><span data-stu-id="265be-119">So, as part of hello script, you must ensure that hello Ambari services and other Hadoop-related services are up and running before hello script finishes running.</span></span> <span data-ttu-id="265be-120">這些服務所需 toosuccessfully 確定 hello 健全狀況和狀態 hello 叢集在建立時。</span><span class="sxs-lookup"><span data-stu-id="265be-120">These services are required toosuccessfully ascertain hello health and state of hello cluster while it is being created.</span></span> <span data-ttu-id="265be-121">如果您變更會影響這些服務的叢集上的任何設定，您必須使用所提供的 hello helper 函式。</span><span class="sxs-lookup"><span data-stu-id="265be-121">If you change any configuration on the cluster that affects these services, you must use hello helper functions that are provided.</span></span> <span data-ttu-id="265be-122">如需 Helper 函式的詳細資訊，請參閱[開發 HDInsight 的指令碼動作指令碼][hdinsight-write-script]。</span><span class="sxs-lookup"><span data-stu-id="265be-122">For more information about helper functions, see [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>
>
>

<span data-ttu-id="265be-123">hello 輸出和 hello hello 指令碼的錯誤記錄檔會儲存在您指定給 hello 叢集 hello 預設儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="265be-123">hello output and hello error logs for hello script are stored in hello default Storage account you specified for hello cluster.</span></span> <span data-ttu-id="265be-124">hello 記錄檔會儲存在資料表中具有 hello 名稱**u < \cluster-name-fragment >< \time-stamp > setuplog**。</span><span class="sxs-lookup"><span data-stu-id="265be-124">hello logs are stored in a table with hello name **u<\cluster-name-fragment><\time-stamp>setuplog**.</span></span> <span data-ttu-id="265be-125">這些是從所有節點上執行 hello （前端節點和背景工作角色節點） hello 叢集中的 hello 指令碼的彙總記錄檔。</span><span class="sxs-lookup"><span data-stu-id="265be-125">These are aggregate logs from hello script run on all hello nodes (head node and worker nodes) in hello cluster.</span></span>

<span data-ttu-id="265be-126">每個叢集可以接受多個會指定中的 hello 順序叫用的指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="265be-126">Each cluster can accept multiple script actions that are invoked in hello order in which they are specified.</span></span> <span data-ttu-id="265be-127">在 hello 前端節點、 hello 背景工作節點，或兩者，就可以執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="265be-127">A script can be ran on hello head node, hello worker nodes, or both.</span></span>

<span data-ttu-id="265be-128">HDInsight 提供下列元件在 HDInsight 叢集上的數個指令碼 tooinstall hello:</span><span class="sxs-lookup"><span data-stu-id="265be-128">HDInsight provides several scripts tooinstall hello following components on HDInsight clusters:</span></span>

| <span data-ttu-id="265be-129">名稱</span><span class="sxs-lookup"><span data-stu-id="265be-129">Name</span></span> | <span data-ttu-id="265be-130">指令碼</span><span class="sxs-lookup"><span data-stu-id="265be-130">Script</span></span> |
| --- | --- |
| <span data-ttu-id="265be-131">**安裝 Spark**</span><span class="sxs-lookup"><span data-stu-id="265be-131">**Install Spark**</span></span> |<span data-ttu-id="265be-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1。</span><span class="sxs-lookup"><span data-stu-id="265be-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="265be-133">請參閱[在 HDInsight 叢集上安裝和使用 Spark][hdinsight-install-spark]。</span><span class="sxs-lookup"><span data-stu-id="265be-133">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="265be-134">**安裝 R**</span><span class="sxs-lookup"><span data-stu-id="265be-134">**Install R**</span></span> |<span data-ttu-id="265be-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1。</span><span class="sxs-lookup"><span data-stu-id="265be-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="265be-136">請參閱[在 HDInsight 叢集上安裝和使用 R][hdinsight-install-r]。</span><span class="sxs-lookup"><span data-stu-id="265be-136">See [Install and use R on HDInsight clusters][hdinsight-install-r].</span></span> |
| <span data-ttu-id="265be-137">**安裝 Solr**</span><span class="sxs-lookup"><span data-stu-id="265be-137">**Install Solr**</span></span> |<span data-ttu-id="265be-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1。</span><span class="sxs-lookup"><span data-stu-id="265be-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="265be-139">請參閱 [在 HDInsight 叢集上安裝及使用 Solr](hdinsight-hadoop-solr-install.md)。</span><span class="sxs-lookup"><span data-stu-id="265be-139">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="265be-140">- **安裝 Giraph**</span><span class="sxs-lookup"><span data-stu-id="265be-140">- **Install Giraph**</span></span> |<span data-ttu-id="265be-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1。</span><span class="sxs-lookup"><span data-stu-id="265be-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="265be-142">請參閱 [在 HDInsight 叢集上安裝及使用 Giraph](hdinsight-hadoop-giraph-install.md)。</span><span class="sxs-lookup"><span data-stu-id="265be-142">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |
| <span data-ttu-id="265be-143">**預先載入 Hive 程式庫**</span><span class="sxs-lookup"><span data-stu-id="265be-143">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="265be-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1。</span><span class="sxs-lookup"><span data-stu-id="265be-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span></span> <span data-ttu-id="265be-145">請參閱 [在 HDInsight 叢集上新增 Hive 程式庫](hdinsight-hadoop-add-hive-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="265be-145">See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md)</span></span> |

## <a name="call-scripts-using-hello-azure-portal"></a><span data-ttu-id="265be-146">呼叫使用 hello Azure 入口網站的指令碼</span><span class="sxs-lookup"><span data-stu-id="265be-146">Call scripts using hello Azure portal</span></span>
<span data-ttu-id="265be-147">**從 hello Azure 入口網站**</span><span class="sxs-lookup"><span data-stu-id="265be-147">**From hello Azure portal**</span></span>

1. <span data-ttu-id="265be-148">依[在 HDInsight 建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)中的描述開始建立叢集。</span><span class="sxs-lookup"><span data-stu-id="265be-148">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
2. <span data-ttu-id="265be-149">根據選擇性的設定，如 hello**指令碼動作**刀鋒視窗中，按一下 **加入指令碼動作**tooprovide 詳細 hello 指令碼動作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="265be-149">Under Optional Configuration, for hello **Script Actions** blade, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="265be-150">![使用指令碼動作 toocustomize 叢集](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "使用指令碼動作 toocustomize 叢集")</span><span class="sxs-lookup"><span data-stu-id="265be-150">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="265be-151">屬性</span><span class="sxs-lookup"><span data-stu-id="265be-151">Property</span></span></th><th><span data-ttu-id="265be-152">值</span><span class="sxs-lookup"><span data-stu-id="265be-152">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="265be-153">名稱</span><span class="sxs-lookup"><span data-stu-id="265be-153">Name</span></span></td>
            <td><span data-ttu-id="265be-154">指定 hello 指令碼動作的名稱。</span><span class="sxs-lookup"><span data-stu-id="265be-154">Specify a name for hello script action.</span></span></td></tr>
        <tr><td><span data-ttu-id="265be-155">指令碼 URI</span><span class="sxs-lookup"><span data-stu-id="265be-155">Script URI</span></span></td>
            <td><span data-ttu-id="265be-156">指定 hello URI toohello 指令碼會叫用的 toocustomize hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="265be-156">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="265be-157">s</span><span class="sxs-lookup"><span data-stu-id="265be-157">s</span></span></td></tr>
        <tr><td><span data-ttu-id="265be-158">Head/Worker</span><span class="sxs-lookup"><span data-stu-id="265be-158">Head/Worker</span></span></td>
            <td><span data-ttu-id="265be-159">指定 hello 節點 (**Head**或**工作者**) 執行哪些 hello 自訂指令碼。</b>。</span><span class="sxs-lookup"><span data-stu-id="265be-159">Specify hello nodes (**Head** or **Worker**) on which hello customization script is run.</b>.</span></span>
        <tr><td><span data-ttu-id="265be-160">參數</span><span class="sxs-lookup"><span data-stu-id="265be-160">Parameters</span></span></td>
            <td><span data-ttu-id="265be-161">指定 hello 參數，如果 hello 指令碼所需。</span><span class="sxs-lookup"><span data-stu-id="265be-161">Specify hello parameters, if required by hello script.</span></span></td></tr>
    </table>

    <span data-ttu-id="265be-162">按下 ENTER tooadd 以上的一個指令碼動作 tooinstall 多個元件 hello 叢集上。</span><span class="sxs-lookup"><span data-stu-id="265be-162">Press ENTER tooadd more than one script action tooinstall multiple components on hello cluster.</span></span>
3. <span data-ttu-id="265be-163">按一下**選取**toosave hello 指令碼動作組態，並繼續建立叢集。</span><span class="sxs-lookup"><span data-stu-id="265be-163">Click **Select** toosave hello script action configuration and continue with cluster creation.</span></span>

## <a name="call-scripts-using-azure-powershell"></a><span data-ttu-id="265be-164">使用 Azure PowerShell 呼叫指令碼</span><span class="sxs-lookup"><span data-stu-id="265be-164">Call scripts using Azure PowerShell</span></span>
<span data-ttu-id="265be-165">此下列 PowerShell 指令碼示範如何在 Windows 上的 Spark tooinstall 基礎 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="265be-165">This following PowerShell script demonstrates how tooinstall Spark on Windows based HDInsight cluster.</span></span>  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" toolist IDs.

    $nameToken = "<Enter A Name Token>"  # hello token is use toocreate Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect tooAzure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare hello dependent components
    #############################################################

    # Create resource group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext

    #############################################################
    # Create cluster with ApacheSpark
    #############################################################

    # Specify hello configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action toohello cluster configuration
    $config = Add-AzureRmHDInsightScriptAction `
                -Config $config `
                -Name "Install Spark" `
                -NodeType HeadNode `
                -Uri https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1 `

    # Start creating a cluster with Spark installed
    New-AzureRmHDInsightCluster `
            -ResourceGroupName $resourceGroupName `
            -ClusterName $hdinsightClusterName `
            -Location $location `
            -ClusterSizeInNodes 2 `
            -ClusterType Hadoop `
            -OSType Windows `
            -DefaultStorageContainer $defaultBlobContainerName `
            -Config $config


<span data-ttu-id="265be-166">tooinstall 其他軟體，您將需要 tooreplace hello 指令碼檔案中 hello 指令碼：</span><span class="sxs-lookup"><span data-stu-id="265be-166">tooinstall other software, you will need tooreplace hello script file in hello script:</span></span>

<span data-ttu-id="265be-167">出現提示時，輸入 hello 叢集 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="265be-167">When prompted, enter hello credentials for hello cluster.</span></span> <span data-ttu-id="265be-168">可能需要幾分鐘後才建立 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="265be-168">It can take several minutes before hello cluster is created.</span></span>

## <a name="call-scripts-using-net-sdk"></a><span data-ttu-id="265be-169">使用 .NET SDK 呼叫指令碼</span><span class="sxs-lookup"><span data-stu-id="265be-169">Call scripts using .NET SDK</span></span>
<span data-ttu-id="265be-170">hello 下列範例會示範如何在 Windows 上的 Spark tooinstall 基礎 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="265be-170">hello following sample demonstrates how tooinstall Spark on Windows based HDInsight cluster.</span></span> <span data-ttu-id="265be-171">tooinstall 其他軟體，您必須在 hello 程式碼中的 tooreplace hello 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="265be-171">tooinstall other software, you will need tooreplace hello script file in hello code.</span></span>

<span data-ttu-id="265be-172">**toocreate Spark 與 HDInsight 叢集**</span><span class="sxs-lookup"><span data-stu-id="265be-172">**toocreate an HDInsight cluster with Spark**</span></span>

1. <span data-ttu-id="265be-173">在 Visual Studio 建立 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="265be-173">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="265be-174">從 hello Nuget 封裝管理員主控台中，執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="265be-174">From hello Nuget Package Manager Console, run hello following command.</span></span>

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. <span data-ttu-id="265be-175">使用下列陳述式使用 hello Program.cs 檔案中的 hello:</span><span class="sxs-lookup"><span data-stu-id="265be-175">Use hello following using statements in hello Program.cs file:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. <span data-ttu-id="265be-176">Hello 程式碼置於 hello hello 下列類別：</span><span class="sxs-lookup"><span data-stu-id="265be-176">Place hello code in hello class with hello following:</span></span>

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";
        private const string ResourceGroupName = "<ExistingAzureResourceGroupName>";
        private const string NewClusterName = "<NewAzureHDInsightClusterName>";
        private const int NewClusterNumWorkerNodes = 2;
        private const string NewClusterLocation = "East US";
        private const string NewClusterVersion = "3.2";
        private const string ExistingStorageName = "<ExistingAzureStorageAccountName>";
        private const string ExistingStorageKey = "<ExistingAzureStorageAccountKey>";
        private const string ExistingContainer = "<ExistingAzureBlobStorageContainer>";
        private const string NewClusterType = "Hadoop";
        private const OSType NewClusterOSType = OSType.Windows;
        private const string NewClusterUsername = "<HttpUserName>";
        private const string NewClusterPassword = "<HttpUserPassword>";

        static void Main(string[] args)
        {
            System.Console.WriteLine("Running");

            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            CreateCluster();
        }

        private static void CreateCluster()
        {
            var parameters = new ClusterCreateParameters
            {
                ClusterSizeInNodes = NewClusterNumWorkerNodes,
                Location = NewClusterLocation,
                ClusterType = NewClusterType,
                OSType = NewClusterOSType,
                Version = NewClusterVersion,
                DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingContainer),
                UserName = NewClusterUsername,
                Password = NewClusterPassword,
            };

            ScriptAction sparkScriptAction = new ScriptAction("Install Spark",
                new Uri("https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1"), "");

            parameters.ScriptActions.Add(ClusterNodeType.HeadNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });
            parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });

            _hdiManagementClient.Clusters.Create(ResourceGroupName, NewClusterName, parameters);
        }

        /// <summary>
        /// Authenticate tooan Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">hello AAD tenant ID</param>
        /// <param name="ClientId">hello AAD client ID</param>
        /// <param name="SubscriptionId">hello Azure subscription ID</param>
        /// <returns></returns>
        static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
        {
            var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
            var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/",
                ClientId,
                new Uri("urn:ietf:wg:oauth:2.0:oob"),
                PromptBehavior.Always,
                UserIdentifier.AnyUser);
            return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
        }
        /// <summary>
        /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
        /// </summary>
        /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
        /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
        /// <param name="authToken">An authentication token for your Azure subscription</param>
        static void EnableHDInsight(TokenCloudCredentials authToken)
        {
            // Create a client for hello Resource manager and set hello subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register hello HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. <span data-ttu-id="265be-177">按**F5** toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="265be-177">Press **F5** toorun hello application.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="265be-178">支援在 HDInsight 叢集上使用開放原始碼軟體</span><span class="sxs-lookup"><span data-stu-id="265be-178">Support for open-source software used on HDInsight clusters</span></span>
<span data-ttu-id="265be-179">hello Microsoft Azure HDInsight 服務是彈性的平台，可讓您使用的開放原始碼技術 Hadoop 周圍形成的生態系統的 hello 定域機組中的 toobuild 巨量資料應用程式。</span><span class="sxs-lookup"><span data-stu-id="265be-179">hello Microsoft Azure HDInsight service is a flexible platform that enables you toobuild big-data applications in hello cloud by using an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="265be-180">Microsoft Azure 會提供適用於開放原始碼技術，支援一般層級述 hello**支援範圍**區段 hello <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure 支援常見問題集網站</a>。</span><span class="sxs-lookup"><span data-stu-id="265be-180">Microsoft Azure provides a general level of support for open-source technologies, as discussed in hello **Support Scope** section of hello <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure Support FAQ website</a>.</span></span> <span data-ttu-id="265be-181">hello HDInsight 服務會提供額外一層的部分 hello 元件的支援，如下所述。</span><span class="sxs-lookup"><span data-stu-id="265be-181">hello HDInsight service provides an additional level of support for some of hello components, as described below.</span></span>

<span data-ttu-id="265be-182">有兩種可用在 hello HDInsight 服務的開放原始碼元件類型：</span><span class="sxs-lookup"><span data-stu-id="265be-182">There are two types of open-source components that are available in hello HDInsight service:</span></span>

* <span data-ttu-id="265be-183">**內建元件**-HDInsight 叢集上已預先安裝這些元件，並提供 hello 叢集的核心功能。</span><span class="sxs-lookup"><span data-stu-id="265be-183">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of hello cluster.</span></span> <span data-ttu-id="265be-184">例如，YARN ResourceManager、 hello Hive 查詢語言 (HiveQL) 及 hello 砲象兵程式庫屬於 toothis 類別目錄。</span><span class="sxs-lookup"><span data-stu-id="265be-184">For example, YARN ResourceManager, hello Hive query language (HiveQL), and hello Mahout library belong toothis category.</span></span> <span data-ttu-id="265be-185">叢集元件的完整清單位於[hello HDInsight 所提供的 Hadoop 叢集版本中最新消息？](hdinsight-component-versioning.md)</a>.</span><span class="sxs-lookup"><span data-stu-id="265be-185">A full list of cluster components is available in [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md)</a>.</span></span>
* <span data-ttu-id="265be-186">**自訂元件**-您為 hello 叢集的使用者可以安裝或使用您的工作負載中用於 hello 社群或您所建立的任何元件。</span><span class="sxs-lookup"><span data-stu-id="265be-186">**Custom components** - You, as a user of hello cluster, can install or use in your workload any component available in hello community or created by you.</span></span>

<span data-ttu-id="265be-187">完全支援內建的元件，而且 Microsoft 支援服務將會說明 tooisolate 及解決問題的相關的 toothese 元件。</span><span class="sxs-lookup"><span data-stu-id="265be-187">Built-in components are fully supported, and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>

> [!WARNING]
> <span data-ttu-id="265be-188">完全支援隨附 hello HDInsight 叢集的元件，而且 Microsoft 支援服務將會說明 tooisolate 及解決問題的相關的 toothese 元件。</span><span class="sxs-lookup"><span data-stu-id="265be-188">Components provided with hello HDInsight cluster are fully supported and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="265be-189">自訂元件會收到盡商業上合理支援 toohelp 您 toofurther hello 問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="265be-189">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="265be-190">這可能會導致解決 hello 問題，或詢問您 tooengage hello 可用的頻道開啟原始碼技術找到深層的專業知識，針對該項技術。</span><span class="sxs-lookup"><span data-stu-id="265be-190">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="265be-191">例如，有許多社群網站可以使用，像是：[HDInsight 的 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight)、[http://stackoverflow.com](http://stackoverflow.com)。另外，Apache 專案在 [http://apache.org](http://apache.org) 上有專案網站，例如：[Hadoop](http://hadoop.apache.org/)、[Spark](http://spark.apache.org/)。</span><span class="sxs-lookup"><span data-stu-id="265be-191">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span></span>
>
>

<span data-ttu-id="265be-192">hello HDInsight 服務提供數種方式 toouse 自訂元件。</span><span class="sxs-lookup"><span data-stu-id="265be-192">hello HDInsight service provides several ways toouse custom components.</span></span> <span data-ttu-id="265be-193">不論如何元件為使用 hello 叢集上安裝，hello 的支援相同層級套用。</span><span class="sxs-lookup"><span data-stu-id="265be-193">Regardless of how a component is used or installed on hello cluster, hello same level of support applies.</span></span> <span data-ttu-id="265be-194">以下是 hello 最常用的方式，自訂元件，可用在 HDInsight 叢集上的清單：</span><span class="sxs-lookup"><span data-stu-id="265be-194">Below is a list of hello most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="265be-195">提交作業-Hadoop 或其他類型的執行，或使用自訂元件的工作可以提交的 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="265be-195">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted toohello cluster.</span></span>
2. <span data-ttu-id="265be-196">叢集自訂-叢集建立期間，您可以指定其他設定及自訂將 hello 叢集節點安裝的元件。</span><span class="sxs-lookup"><span data-stu-id="265be-196">Cluster customization - During cluster creation, you can specify additional settings and custom components that will be installed on hello cluster nodes.</span></span>
3. <span data-ttu-id="265be-197">範例-常用的自訂元件、 Microsoft 和其他人可能會提供如何使用這些元件在 hello HDInsight 叢集上的範例。</span><span class="sxs-lookup"><span data-stu-id="265be-197">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on hello HDInsight clusters.</span></span> <span data-ttu-id="265be-198">提供這些範例，但是沒有支援。</span><span class="sxs-lookup"><span data-stu-id="265be-198">These samples are provided without support.</span></span>

## <a name="develop-script-action-scripts"></a><span data-ttu-id="265be-199">開發指令碼動作指令碼</span><span class="sxs-lookup"><span data-stu-id="265be-199">Develop Script Action scripts</span></span>
<span data-ttu-id="265be-200">請參閱[開發 HDInsight 的指令碼動作指令碼][hdinsight-write-script]。</span><span class="sxs-lookup"><span data-stu-id="265be-200">See [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>

## <a name="see-also"></a><span data-ttu-id="265be-201">另請參閱</span><span class="sxs-lookup"><span data-stu-id="265be-201">See also</span></span>
* <span data-ttu-id="265be-202">[建立在 HDInsight Hadoop 叢集][ hdinsight-provision-cluster] toocreate 在 HDInsight 叢集使用其他自訂選項的方式提供的指示。</span><span class="sxs-lookup"><span data-stu-id="265be-202">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how toocreate an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="265be-203">[開發 HDInsight 的指令碼動作指令碼][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="265be-203">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="265be-204">[在 HDInsight 叢集上安裝和使用 Spark][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="265be-204">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="265be-205">[在 HDInsight 叢集上安裝和使用 R][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="265be-205">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="265be-206">[在 HDInsight 叢集上安裝及使用 Solr](hdinsight-hadoop-solr-install.md)。</span><span class="sxs-lookup"><span data-stu-id="265be-206">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="265be-207">[在 HDInsight 叢集上安裝及使用 Giraph](hdinsight-hadoop-giraph-install.md)。</span><span class="sxs-lookup"><span data-stu-id="265be-207">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "叢集建立期間的階段"
