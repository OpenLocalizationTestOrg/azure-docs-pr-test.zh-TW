---
title: "使用指令碼動作來自訂 HDInsight 叢集 - Azure | Microsoft Docs"
description: "深入了解使用指令碼動作來自訂 HDInsight 叢集。"
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
ms.openlocfilehash: ec95b6d66c71b4278dd1e16807fcc75f5e8b1c36
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="c191d-103">使用指令碼動作自訂 Windows 型 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="c191d-103">Customize Windows-based HDInsight clusters using Script Action</span></span>
<span data-ttu-id="c191d-104">**指令碼動作** 可用來叫用 [自訂指令碼](hdinsight-hadoop-script-actions.md) 。</span><span class="sxs-lookup"><span data-stu-id="c191d-104">**Script Action** can be used to invoke [custom scripts](hdinsight-hadoop-script-actions.md) during the cluster creation process for installing additional software on a cluster.</span></span>

<span data-ttu-id="c191d-105">本文的資訊是針對以 Windows 為基礎的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="c191d-105">The information in this article is specific to Windows-based HDInsight clusters.</span></span> <span data-ttu-id="c191d-106">如果是以 Linux 為基礎的叢集，請參閱 [使用指令碼動作自訂 Linux 型 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="c191d-106">For Linux-based clusters, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c191d-107">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="c191d-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c191d-108">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="c191d-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="c191d-109">您也可以使用多種其他方法來自訂 HDInsight 叢集，例如包括額外的 Azure 儲存體帳戶、變更 Hadoop 組態檔 (core-site.xml、hive-site.xml 等)，或是將共用程式庫 (例如 Hive、Oozie) 加入至叢集中的共同位置。</span><span class="sxs-lookup"><span data-stu-id="c191d-109">HDInsight clusters can be customized in a variety of other ways as well, such as including additional Azure Storage accounts, changing the Hadoop configuration files (core-site.xml, hive-site.xml, etc.), or adding shared libraries (e.g., Hive, Oozie) into common locations in the cluster.</span></span> <span data-ttu-id="c191d-110">這些自訂可以透過 Azure PowerShell、Azure HDInsight .NET SDK 或 Azure 入口網站來完成。</span><span class="sxs-lookup"><span data-stu-id="c191d-110">These customizations can be done through Azure PowerShell, the Azure HDInsight .NET SDK, or the Azure portal.</span></span> <span data-ttu-id="c191d-111">如需詳細資訊，請參閱[在 HDInsight 中建立 Hadoop 叢集][hdinsight-provision-cluster]。</span><span class="sxs-lookup"><span data-stu-id="c191d-111">For more information, see [Create Hadoop clusters in HDInsight][hdinsight-provision-cluster].</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-the-cluster-creation-process"></a><span data-ttu-id="c191d-112">叢集建立程序中的指令碼動作</span><span class="sxs-lookup"><span data-stu-id="c191d-112">Script Action in the cluster creation process</span></span>
<span data-ttu-id="c191d-113">只有正在建立叢集時，才會使用「指令碼動作」。</span><span class="sxs-lookup"><span data-stu-id="c191d-113">Script Action is only used while a cluster is in the process of being created.</span></span> <span data-ttu-id="c191d-114">下圖說明在建立程序期間執行指令碼動作的時間：</span><span class="sxs-lookup"><span data-stu-id="c191d-114">The following diagram illustrates when Script Action is executed during the creation process:</span></span>

<span data-ttu-id="c191d-115">![HDInsight 叢集自訂和叢集建立期間的階段][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="c191d-115">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="c191d-116">當指令碼執行時，叢集會進入 **ClusterCustomization** 階段。</span><span class="sxs-lookup"><span data-stu-id="c191d-116">When the script is running, the cluster enters the **ClusterCustomization** stage.</span></span> <span data-ttu-id="c191d-117">在此階段，指令碼會在系統管理員帳戶下，以平行方式在叢集中所有指定的節點上執行，而在節點上提供完整的系統管理員權限。</span><span class="sxs-lookup"><span data-stu-id="c191d-117">At this stage, the script is run under the system admin account, in parallel on all the specified nodes in the cluster, and provides full admin privileges on the nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="c191d-118">因為您在 **ClusterCustomization** 階段中於叢集節點上擁有系統管理員權限，所以您可以使用指令碼來執行作業，例如停止和啟動服務，包括 Hadoop 相關服務。</span><span class="sxs-lookup"><span data-stu-id="c191d-118">Because you have admin privileges on the cluster nodes during the **ClusterCustomization** stage, you can use the script to perform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="c191d-119">因此，在指令碼中，您必須在指令碼完成執行之前，確定 Ambari 服務及其他 Hadoop 相關服務已啟動並且正在執行。</span><span class="sxs-lookup"><span data-stu-id="c191d-119">So, as part of the script, you must ensure that the Ambari services and other Hadoop-related services are up and running before the script finishes running.</span></span> <span data-ttu-id="c191d-120">這些服務必須在叢集建立時，成功地確定叢集的健康情況和狀態。</span><span class="sxs-lookup"><span data-stu-id="c191d-120">These services are required to successfully ascertain the health and state of the cluster while it is being created.</span></span> <span data-ttu-id="c191d-121">如果您變更叢集上的任何會影響這些服務的組態，就必須使用所提供的協助程式函式。</span><span class="sxs-lookup"><span data-stu-id="c191d-121">If you change any configuration on the cluster that affects these services, you must use the helper functions that are provided.</span></span> <span data-ttu-id="c191d-122">如需 Helper 函式的詳細資訊，請參閱[開發 HDInsight 的指令碼動作指令碼][hdinsight-write-script]。</span><span class="sxs-lookup"><span data-stu-id="c191d-122">For more information about helper functions, see [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>
>
>

<span data-ttu-id="c191d-123">指令碼的輸出和錯誤記錄檔會儲存在您為叢集指定的預設儲存體帳戶中。</span><span class="sxs-lookup"><span data-stu-id="c191d-123">The output and the error logs for the script are stored in the default Storage account you specified for the cluster.</span></span> <span data-ttu-id="c191d-124">記錄檔是以 **u<\cluster-name-fragment><\time-stamp>setuplog** 的名稱儲存在資料表中。</span><span class="sxs-lookup"><span data-stu-id="c191d-124">The logs are stored in a table with the name **u<\cluster-name-fragment><\time-stamp>setuplog**.</span></span> <span data-ttu-id="c191d-125">這些是從叢集中所有節點上 (前端節點和背景工作節點) 執行之指令碼彙總的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c191d-125">These are aggregate logs from the script run on all the nodes (head node and worker nodes) in the cluster.</span></span>

<span data-ttu-id="c191d-126">每個叢集可接受多個指令碼動作，這些指令碼會依其指定順序被叫用。</span><span class="sxs-lookup"><span data-stu-id="c191d-126">Each cluster can accept multiple script actions that are invoked in the order in which they are specified.</span></span> <span data-ttu-id="c191d-127">指令碼可在前端節點、背景工作節點或同時在兩者執行。</span><span class="sxs-lookup"><span data-stu-id="c191d-127">A script can be ran on the head node, the worker nodes, or both.</span></span>

<span data-ttu-id="c191d-128">HDInsight 提供數個指令碼在 HDInsight 叢集上安裝下列元件：</span><span class="sxs-lookup"><span data-stu-id="c191d-128">HDInsight provides several scripts to install the following components on HDInsight clusters:</span></span>

| <span data-ttu-id="c191d-129">名稱</span><span class="sxs-lookup"><span data-stu-id="c191d-129">Name</span></span> | <span data-ttu-id="c191d-130">指令碼</span><span class="sxs-lookup"><span data-stu-id="c191d-130">Script</span></span> |
| --- | --- |
| <span data-ttu-id="c191d-131">**安裝 Spark**</span><span class="sxs-lookup"><span data-stu-id="c191d-131">**Install Spark**</span></span> |<span data-ttu-id="c191d-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1。</span><span class="sxs-lookup"><span data-stu-id="c191d-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="c191d-133">請參閱[在 HDInsight 叢集上安裝和使用 Spark][hdinsight-install-spark]。</span><span class="sxs-lookup"><span data-stu-id="c191d-133">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="c191d-134">**安裝 R**</span><span class="sxs-lookup"><span data-stu-id="c191d-134">**Install R**</span></span> |<span data-ttu-id="c191d-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1。</span><span class="sxs-lookup"><span data-stu-id="c191d-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="c191d-136">請參閱[在 HDInsight 叢集上安裝和使用 R][hdinsight-install-r]。</span><span class="sxs-lookup"><span data-stu-id="c191d-136">See [Install and use R on HDInsight clusters][hdinsight-install-r].</span></span> |
| <span data-ttu-id="c191d-137">**安裝 Solr**</span><span class="sxs-lookup"><span data-stu-id="c191d-137">**Install Solr**</span></span> |<span data-ttu-id="c191d-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1。</span><span class="sxs-lookup"><span data-stu-id="c191d-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="c191d-139">請參閱 [在 HDInsight 叢集上安裝及使用 Solr](hdinsight-hadoop-solr-install.md)。</span><span class="sxs-lookup"><span data-stu-id="c191d-139">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="c191d-140">- **安裝 Giraph**</span><span class="sxs-lookup"><span data-stu-id="c191d-140">- **Install Giraph**</span></span> |<span data-ttu-id="c191d-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1。</span><span class="sxs-lookup"><span data-stu-id="c191d-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="c191d-142">請參閱 [在 HDInsight 叢集上安裝及使用 Giraph](hdinsight-hadoop-giraph-install.md)。</span><span class="sxs-lookup"><span data-stu-id="c191d-142">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |
| <span data-ttu-id="c191d-143">**預先載入 Hive 程式庫**</span><span class="sxs-lookup"><span data-stu-id="c191d-143">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="c191d-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1。</span><span class="sxs-lookup"><span data-stu-id="c191d-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span></span> <span data-ttu-id="c191d-145">請參閱 [在 HDInsight 叢集上新增 Hive 程式庫](hdinsight-hadoop-add-hive-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="c191d-145">See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md)</span></span> |

## <a name="call-scripts-using-the-azure-portal"></a><span data-ttu-id="c191d-146">使用 Azure 入口網站來呼叫指令碼</span><span class="sxs-lookup"><span data-stu-id="c191d-146">Call scripts using the Azure portal</span></span>
<span data-ttu-id="c191d-147">**從 Azure 入口網站**</span><span class="sxs-lookup"><span data-stu-id="c191d-147">**From the Azure portal**</span></span>

1. <span data-ttu-id="c191d-148">依[在 HDInsight 建立 Hadoop 叢集](hdinsight-hadoop-provision-linux-clusters.md)中的描述開始建立叢集。</span><span class="sxs-lookup"><span data-stu-id="c191d-148">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
2. <span data-ttu-id="c191d-149">在 [選擇性組態] 下方的 [指令碼動作] 刀鋒視窗中，按一下 [加入指令碼動作] 以提供有關指令碼動作的詳細資料，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c191d-149">Under Optional Configuration, for the **Script Actions** blade, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="c191d-150">![使用指令碼動作以自訂叢集](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "使用指令碼動作以自訂叢集")</span><span class="sxs-lookup"><span data-stu-id="c191d-150">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="c191d-151">屬性</span><span class="sxs-lookup"><span data-stu-id="c191d-151">Property</span></span></th><th><span data-ttu-id="c191d-152">值</span><span class="sxs-lookup"><span data-stu-id="c191d-152">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="c191d-153">名稱</span><span class="sxs-lookup"><span data-stu-id="c191d-153">Name</span></span></td>
            <td><span data-ttu-id="c191d-154">指定指令碼動作的名稱。</span><span class="sxs-lookup"><span data-stu-id="c191d-154">Specify a name for the script action.</span></span></td></tr>
        <tr><td><span data-ttu-id="c191d-155">指令碼 URI</span><span class="sxs-lookup"><span data-stu-id="c191d-155">Script URI</span></span></td>
            <td><span data-ttu-id="c191d-156">對自訂叢集所叫用的指令碼指定 URI。</span><span class="sxs-lookup"><span data-stu-id="c191d-156">Specify the URI to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="c191d-157">s</span><span class="sxs-lookup"><span data-stu-id="c191d-157">s</span></span></td></tr>
        <tr><td><span data-ttu-id="c191d-158">Head/Worker</span><span class="sxs-lookup"><span data-stu-id="c191d-158">Head/Worker</span></span></td>
            <td><span data-ttu-id="c191d-159">指定執行自訂指令碼的節點 (**Head** 或 **Worker**)。</b></span><span class="sxs-lookup"><span data-stu-id="c191d-159">Specify the nodes (**Head** or **Worker**) on which the customization script is run.</b>.</span></span>
        <tr><td><span data-ttu-id="c191d-160">參數</span><span class="sxs-lookup"><span data-stu-id="c191d-160">Parameters</span></span></td>
            <td><span data-ttu-id="c191d-161">如果指令碼要求，請指定參數。</span><span class="sxs-lookup"><span data-stu-id="c191d-161">Specify the parameters, if required by the script.</span></span></td></tr>
    </table>

    <span data-ttu-id="c191d-162">請按 ENTER 加入一個以上的指令碼動作，以在叢集上安裝多個元件。</span><span class="sxs-lookup"><span data-stu-id="c191d-162">Press ENTER to add more than one script action to install multiple components on the cluster.</span></span>
3. <span data-ttu-id="c191d-163">按一下 [ **選取** ] 以儲存指令碼動作組態，並繼續建立叢集。</span><span class="sxs-lookup"><span data-stu-id="c191d-163">Click **Select** to save the script action configuration and continue with cluster creation.</span></span>

## <a name="call-scripts-using-azure-powershell"></a><span data-ttu-id="c191d-164">使用 Azure PowerShell 呼叫指令碼</span><span class="sxs-lookup"><span data-stu-id="c191d-164">Call scripts using Azure PowerShell</span></span>
<span data-ttu-id="c191d-165">接下來的這個 PowerShell 指令碼示範如何在以 Windows 為基礎的 HDInsight 叢集上安裝 Spark。</span><span class="sxs-lookup"><span data-stu-id="c191d-165">This following PowerShell script demonstrates how to install Spark on Windows based HDInsight cluster.</span></span>  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" to list IDs.

    $nameToken = "<Enter A Name Token>"  # The token is use to create Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect to Azure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare the dependent components
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

    # Specify the configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action to the cluster configuration
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


<span data-ttu-id="c191d-166">若要安裝其他軟體，您必須取代指令碼中的指令碼檔案：</span><span class="sxs-lookup"><span data-stu-id="c191d-166">To install other software, you will need to replace the script file in the script:</span></span>

<span data-ttu-id="c191d-167">出現提示時，請輸入叢集的認證。</span><span class="sxs-lookup"><span data-stu-id="c191d-167">When prompted, enter the credentials for the cluster.</span></span> <span data-ttu-id="c191d-168">建立叢集可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="c191d-168">It can take several minutes before the cluster is created.</span></span>

## <a name="call-scripts-using-net-sdk"></a><span data-ttu-id="c191d-169">使用 .NET SDK 呼叫指令碼</span><span class="sxs-lookup"><span data-stu-id="c191d-169">Call scripts using .NET SDK</span></span>
<span data-ttu-id="c191d-170">下列範例示範如何在以 Windows 為基礎的 HDInsight 叢集上安裝 Spark。</span><span class="sxs-lookup"><span data-stu-id="c191d-170">The following sample demonstrates how to install Spark on Windows based HDInsight cluster.</span></span> <span data-ttu-id="c191d-171">若要安裝其他軟體，您必須取代程式碼中的指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="c191d-171">To install other software, you will need to replace the script file in the code.</span></span>

<span data-ttu-id="c191d-172">**使用 Spark 建立 HDInsight 叢集**</span><span class="sxs-lookup"><span data-stu-id="c191d-172">**To create an HDInsight cluster with Spark**</span></span>

1. <span data-ttu-id="c191d-173">在 Visual Studio 建立 C# 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="c191d-173">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="c191d-174">從 NuGet Package Manager Console 執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="c191d-174">From the Nuget Package Manager Console, run the following command.</span></span>

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. <span data-ttu-id="c191d-175">在 Program.cs 檔案中使用下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="c191d-175">Use the following using statements in the Program.cs file:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. <span data-ttu-id="c191d-176">使用下列命令將程式碼放置在類別中：</span><span class="sxs-lookup"><span data-stu-id="c191d-176">Place the code in the class with the following:</span></span>

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is the GUID for the PowerShell client. Used for interactive logins in this example.
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
        /// Authenticate to an Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">The AAD tenant ID</param>
        /// <param name="ClientId">The AAD client ID</param>
        /// <param name="SubscriptionId">The Azure subscription ID</param>
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
            // Create a client for the Resource manager and set the subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register the HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. <span data-ttu-id="c191d-177">按 **F5** 鍵執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="c191d-177">Press **F5** to run the application.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="c191d-178">支援在 HDInsight 叢集上使用開放原始碼軟體</span><span class="sxs-lookup"><span data-stu-id="c191d-178">Support for open-source software used on HDInsight clusters</span></span>
<span data-ttu-id="c191d-179">Microsoft Azure HDInsight 服務是彈性的平台，可讓您使用以 Hadoop 形成之開放原始碼技術的生態系統，在雲端中建置巨量資料應用程式。</span><span class="sxs-lookup"><span data-stu-id="c191d-179">The Microsoft Azure HDInsight service is a flexible platform that enables you to build big-data applications in the cloud by using an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="c191d-180">Microsoft Azure 提供對開放原始碼技術的一般層級支援，如 **Azure 支援常見問題集網站** 的＜ <a href="http://azure.microsoft.com/support/faq/" target="_blank">支援範圍</a>＞章節中所述。</span><span class="sxs-lookup"><span data-stu-id="c191d-180">Microsoft Azure provides a general level of support for open-source technologies, as discussed in the **Support Scope** section of the <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure Support FAQ website</a>.</span></span> <span data-ttu-id="c191d-181">HDInsight 服務對於某些元件提供額外層級的支援，如下所述。</span><span class="sxs-lookup"><span data-stu-id="c191d-181">The HDInsight service provides an additional level of support for some of the components, as described below.</span></span>

<span data-ttu-id="c191d-182">HDInsight 服務中有兩種類型的開放原始碼元件可用：</span><span class="sxs-lookup"><span data-stu-id="c191d-182">There are two types of open-source components that are available in the HDInsight service:</span></span>

* <span data-ttu-id="c191d-183">**內建元件** - 這些元件預先安裝在 HDInsight 叢集上，並且提供叢集的核心功能。</span><span class="sxs-lookup"><span data-stu-id="c191d-183">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of the cluster.</span></span> <span data-ttu-id="c191d-184">例如，YARN ResourceManager、Hive 查詢語言 (HiveQL) 及 Mahout 程式庫都屬於這個類別。</span><span class="sxs-lookup"><span data-stu-id="c191d-184">For example, YARN ResourceManager, the Hive query language (HiveQL), and the Mahout library belong to this category.</span></span> <span data-ttu-id="c191d-185">叢集元件的完整清單可於 [HDInsight 所提供 Hadoop 叢集版本的新功能](hdinsight-component-versioning.md)中取得</a>。</span><span class="sxs-lookup"><span data-stu-id="c191d-185">A full list of cluster components is available in [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md)</a>.</span></span>
* <span data-ttu-id="c191d-186">**自訂元件** - 身為叢集使用者的您可以安裝社群中可用或是您建立的任何元件，或者在工作負載中使用。</span><span class="sxs-lookup"><span data-stu-id="c191d-186">**Custom components** - You, as a user of the cluster, can install or use in your workload any component available in the community or created by you.</span></span>

<span data-ttu-id="c191d-187">內建元件受到完整支援，且 Microsoft 支援服務將會協助釐清與解決這些元件的相關問題。</span><span class="sxs-lookup"><span data-stu-id="c191d-187">Built-in components are fully supported, and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>

> [!WARNING]
> <span data-ttu-id="c191d-188">透過 HDInsight 叢集提供的元件會受到完整支援，且 Microsoft 支援服務將協助釐清與解決這些元件的相關問題。</span><span class="sxs-lookup"><span data-stu-id="c191d-188">Components provided with the HDInsight cluster are fully supported and Microsoft Support will help to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="c191d-189">自訂元件則獲得商務上合理的支援，協助您進一步疑難排解問題。</span><span class="sxs-lookup"><span data-stu-id="c191d-189">Custom components receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="c191d-190">如此可能會進而解決問題，或要求您利用可用管道，以找出開放原始碼技術，從中了解該技術的深度專業知識。</span><span class="sxs-lookup"><span data-stu-id="c191d-190">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="c191d-191">例如，有許多社群網站可以使用，像是：[HDInsight 的 MSDN 論壇](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight)、[http://stackoverflow.com](http://stackoverflow.com)。</span><span class="sxs-lookup"><span data-stu-id="c191d-191">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="c191d-192">另外，Apache 專案在 [http://apache.org](http://apache.org) 上有專案網站，例如：[Hadoop](http://hadoop.apache.org/)、[Spark](http://spark.apache.org/)。</span><span class="sxs-lookup"><span data-stu-id="c191d-192">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span></span>
>
>

<span data-ttu-id="c191d-193">HDInsight 服務提供數種方式以使用自訂元件。</span><span class="sxs-lookup"><span data-stu-id="c191d-193">The HDInsight service provides several ways to use custom components.</span></span> <span data-ttu-id="c191d-194">無論元件如何使用或如何安裝在叢集上，都適用相同層級的支援。</span><span class="sxs-lookup"><span data-stu-id="c191d-194">Regardless of how a component is used or installed on the cluster, the same level of support applies.</span></span> <span data-ttu-id="c191d-195">以下是自訂元件可用於 HDInsight 叢集之最常見方式的清單：</span><span class="sxs-lookup"><span data-stu-id="c191d-195">Below is a list of the most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="c191d-196">工作提交 - Hadoop 或其他類型的工作，執行或使用可以提交給叢集的自訂元件。</span><span class="sxs-lookup"><span data-stu-id="c191d-196">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted to the cluster.</span></span>
2. <span data-ttu-id="c191d-197">叢集自訂 - 在叢集建立期間，您可以指定額外設定和將會安裝在叢集節點上的自訂元件。</span><span class="sxs-lookup"><span data-stu-id="c191d-197">Cluster customization - During cluster creation, you can specify additional settings and custom components that will be installed on the cluster nodes.</span></span>
3. <span data-ttu-id="c191d-198">範例 - 對於熱門自訂元件，Microsoft 和其他提供者可能會提供如何在 HDInsight 叢集上使用這些元件的範例。</span><span class="sxs-lookup"><span data-stu-id="c191d-198">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on the HDInsight clusters.</span></span> <span data-ttu-id="c191d-199">提供這些範例，但是沒有支援。</span><span class="sxs-lookup"><span data-stu-id="c191d-199">These samples are provided without support.</span></span>

## <a name="develop-script-action-scripts"></a><span data-ttu-id="c191d-200">開發指令碼動作指令碼</span><span class="sxs-lookup"><span data-stu-id="c191d-200">Develop Script Action scripts</span></span>
<span data-ttu-id="c191d-201">請參閱[開發 HDInsight 的指令碼動作指令碼][hdinsight-write-script]。</span><span class="sxs-lookup"><span data-stu-id="c191d-201">See [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>

## <a name="see-also"></a><span data-ttu-id="c191d-202">另請參閱</span><span class="sxs-lookup"><span data-stu-id="c191d-202">See also</span></span>
* <span data-ttu-id="c191d-203">[在 HDInsight 中建立 Hadoop 叢集][hdinsight-provision-cluster]提供如何使用其他自訂選項建立 HDInsight 叢集的指示。</span><span class="sxs-lookup"><span data-stu-id="c191d-203">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how to create an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="c191d-204">[開發 HDInsight 的指令碼動作指令碼][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="c191d-204">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="c191d-205">[在 HDInsight 叢集上安裝和使用 Spark][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="c191d-205">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="c191d-206">[在 HDInsight 叢集上安裝和使用 R][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="c191d-206">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="c191d-207">[在 HDInsight 叢集上安裝及使用 Solr](hdinsight-hadoop-solr-install.md)。</span><span class="sxs-lookup"><span data-stu-id="c191d-207">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="c191d-208">[在 HDInsight 叢集上安裝及使用 Giraph](hdinsight-hadoop-giraph-install.md)。</span><span class="sxs-lookup"><span data-stu-id="c191d-208">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


<span data-ttu-id="c191d-209">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "叢集建立期間的階段"</span><span class="sxs-lookup"><span data-stu-id="c191d-209">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Stages during cluster creation"</span></span>