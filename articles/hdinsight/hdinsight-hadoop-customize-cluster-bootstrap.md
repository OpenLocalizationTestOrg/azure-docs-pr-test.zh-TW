---
title: "使用 Bootstrap 自訂 HDInsight 叢集 - Azure | Microsoft Docs"
description: "了解如何使用 Bootstrap 自訂 HDInsight 叢集。"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ab2ebf0c-e961-4e95-8151-9724ee22d769
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: c7a6fafa90eac66774d564c82c926c662baf784c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="customize-hdinsight-clusters-using-bootstrap"></a><span data-ttu-id="cc349-103">使用 Bootstrap 自訂 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="cc349-103">Customize HDInsight clusters using Bootstrap</span></span>

<span data-ttu-id="cc349-104">有時候，您需要設定包含下列項目的組態檔：</span><span class="sxs-lookup"><span data-stu-id="cc349-104">Sometimes, you want to configure the configuration files, which include:</span></span>

* <span data-ttu-id="cc349-105">clusterIdentity.xml</span><span class="sxs-lookup"><span data-stu-id="cc349-105">clusterIdentity.xml</span></span>
* <span data-ttu-id="cc349-106">core-site.xml</span><span class="sxs-lookup"><span data-stu-id="cc349-106">core-site.xml</span></span>
* <span data-ttu-id="cc349-107">gateway.xml</span><span class="sxs-lookup"><span data-stu-id="cc349-107">gateway.xml</span></span>
* <span data-ttu-id="cc349-108">hbase-env.xml</span><span class="sxs-lookup"><span data-stu-id="cc349-108">hbase-env.xml</span></span>
* <span data-ttu-id="cc349-109">hbase-site.xml</span><span class="sxs-lookup"><span data-stu-id="cc349-109">hbase-site.xml</span></span>
* <span data-ttu-id="cc349-110">hdfs-site.xml</span><span class="sxs-lookup"><span data-stu-id="cc349-110">hdfs-site.xml</span></span>
* <span data-ttu-id="cc349-111">hive-env.xml</span><span class="sxs-lookup"><span data-stu-id="cc349-111">hive-env.xml</span></span>
* <span data-ttu-id="cc349-112">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="cc349-112">hive-site.xml</span></span>
* <span data-ttu-id="cc349-113">mapred-site</span><span class="sxs-lookup"><span data-stu-id="cc349-113">mapred-site</span></span>
* <span data-ttu-id="cc349-114">oozie-site.xml</span><span class="sxs-lookup"><span data-stu-id="cc349-114">oozie-site.xml</span></span>
* <span data-ttu-id="cc349-115">oozie-env.xml</span><span class="sxs-lookup"><span data-stu-id="cc349-115">oozie-env.xml</span></span>
* <span data-ttu-id="cc349-116">storm-site.xml</span><span class="sxs-lookup"><span data-stu-id="cc349-116">storm-site.xml</span></span>
* <span data-ttu-id="cc349-117">tez-site.xml</span><span class="sxs-lookup"><span data-stu-id="cc349-117">tez-site.xml</span></span>
* <span data-ttu-id="cc349-118">webhcat-site.xml</span><span class="sxs-lookup"><span data-stu-id="cc349-118">webhcat-site.xml</span></span>
* <span data-ttu-id="cc349-119">yarn-site.xml</span><span class="sxs-lookup"><span data-stu-id="cc349-119">yarn-site.xml</span></span>

<span data-ttu-id="cc349-120">有三個方法可以使用 Bootstrap：</span><span class="sxs-lookup"><span data-stu-id="cc349-120">There are three methods to use bootstrap:</span></span>

* <span data-ttu-id="cc349-121">使用 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc349-121">Use Azure PowerShell</span></span>
* <span data-ttu-id="cc349-122">使用 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="cc349-122">Use .NET SDK</span></span>
* <span data-ttu-id="cc349-123">使用 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="cc349-123">Use Azure Resource Manager template</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="cc349-124">如需於建立期間在 HDInsight 叢集上安裝其他元件的相關資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="cc349-124">For information on installing additional components on HDInsight cluster during the creation time, see:</span></span>

* [<span data-ttu-id="cc349-125">使用指令碼動作來自訂 HDInsight 叢集| Azure (Linux)</span><span class="sxs-lookup"><span data-stu-id="cc349-125">Customize HDInsight clusters using Script Action (Linux)</span></span>](hdinsight-hadoop-customize-cluster-linux.md)

## <a name="use-azure-powershell"></a><span data-ttu-id="cc349-126">使用 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc349-126">Use Azure PowerShell</span></span>
<span data-ttu-id="cc349-127">下列 PowerShell 程式碼會自訂 Hive 組態：</span><span class="sxs-lookup"><span data-stu-id="cc349-127">The following PowerShell code customizes a Hive configuration:</span></span>

    # hive-site.xml configuration
    $hiveConfigValues = @{ "hive.metastore.client.socket.timeout"="90" }

    $config = New-AzureRmHDInsightClusterConfig `
        | Set-AzureRmHDInsightDefaultStorage `
            -StorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
            -StorageAccountKey $defaultStorageAccountKey `
        | Add-AzureRmHDInsightConfigValues `
            -HiveSite $hiveConfigValues 

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $existingResourceGroupName `
        -ClusterName $clusterName `
        -Location $location `
        -ClusterSizeInNodes $clusterSizeInNodes `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.5" `
        -HttpCredential $httpCredential `
        -Config $config 

<span data-ttu-id="cc349-128">可完整運作的 PowerShell 指令碼可在 [附錄 A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample)中找到。</span><span class="sxs-lookup"><span data-stu-id="cc349-128">A complete working PowerShell script can be found in [Appendix-A](#hdinsight-hadoop-customize-cluster-bootstrap.md/appx-a:-powershell-sample).</span></span>

<span data-ttu-id="cc349-129">**若要確認變更：**</span><span class="sxs-lookup"><span data-stu-id="cc349-129">**To verify the change:**</span></span>

1. <span data-ttu-id="cc349-130">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="cc349-130">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cc349-131">從左功能表中按一下 [HDInsight 叢集]。</span><span class="sxs-lookup"><span data-stu-id="cc349-131">From the left menu, click **HDInsight clusters**.</span></span> <span data-ttu-id="cc349-132">如果您沒有看到，可先按一下 [更多服務]。</span><span class="sxs-lookup"><span data-stu-id="cc349-132">If you don't see it, click **More services** first.</span></span>
3. <span data-ttu-id="cc349-133">按一下您剛才使用 PowerShell 指令碼建立的叢集。</span><span class="sxs-lookup"><span data-stu-id="cc349-133">Click the cluster you just created using the PowerShell script.</span></span>
4. <span data-ttu-id="cc349-134">在刀鋒視窗頂端按一下 [儀表板]  ，以開啟 Ambari UI。</span><span class="sxs-lookup"><span data-stu-id="cc349-134">Click **Dashboard** from the top of the blade to open the Ambari UI.</span></span>
5. <span data-ttu-id="cc349-135">按一下左側功能表中的 [Hive]  。</span><span class="sxs-lookup"><span data-stu-id="cc349-135">Click **Hive** from the left menu.</span></span>
6. <span data-ttu-id="cc349-136">按一下 [Summary (摘要)] 中的 [HiveServer2]。</span><span class="sxs-lookup"><span data-stu-id="cc349-136">Click **HiveServer2** from **Summary**.</span></span>
7. <span data-ttu-id="cc349-137">按一下 [Configs (設定)]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="cc349-137">Click the **Configs** tab.</span></span>
8. <span data-ttu-id="cc349-138">按一下左側功能表中的 [Hive]  。</span><span class="sxs-lookup"><span data-stu-id="cc349-138">Click **Hive** from the left menu.</span></span>
9. <span data-ttu-id="cc349-139">按一下 [Advanced (進階)]  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="cc349-139">Click the **Advanced** tab.</span></span>
10. <span data-ttu-id="cc349-140">向下捲動，然後展開 [Advanced hive-site (進階 Hive 網站)] 。</span><span class="sxs-lookup"><span data-stu-id="cc349-140">Scroll down and then expand **Advanced hive-site**.</span></span>
11. <span data-ttu-id="cc349-141">在此區段中尋找 **hive.metastore.client.socket.timeout** 。</span><span class="sxs-lookup"><span data-stu-id="cc349-141">Look for **hive.metastore.client.socket.timeout** in the section.</span></span>

<span data-ttu-id="cc349-142">以下是更多自訂其他組態檔的範例：</span><span class="sxs-lookup"><span data-stu-id="cc349-142">Some more samples on customizing other configuration files:</span></span>

    # hdfs-site.xml configuration
    $HdfsConfigValues = @{ "dfs.blocksize"="64m" } #default is 128MB in HDI 3.0 and 256MB in HDI 2.1

    # core-site.xml configuration
    $CoreConfigValues = @{ "ipc.client.connect.max.retries"="60" } #default 50

    # mapred-site.xml configuration
    $MapRedConfigValues = @{ "mapreduce.task.timeout"="1200000" } #default 600000

    # oozie-site.xml configuration
    $OozieConfigValues = @{ "oozie.service.coord.normal.default.timeout"="150" }  # default 120

<span data-ttu-id="cc349-143">如需詳細資訊，請參閱 Azim Uddin 的部落格中，標題為「 [自訂 HDInsight 叢集建立](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx)」的文章。</span><span class="sxs-lookup"><span data-stu-id="cc349-143">For more information, see Azim Uddin's blog titled [Customizing HDInsight Cluster creation](http://blogs.msdn.com/b/bigdatasupport/archive/2014/04/15/customizing-hdinsight-cluster-provisioning-via-powershell-and-net-sdk.aspx).</span></span>

## <a name="use-net-sdk"></a><span data-ttu-id="cc349-144">使用 .NET SDK</span><span class="sxs-lookup"><span data-stu-id="cc349-144">Use .NET SDK</span></span>
<span data-ttu-id="cc349-145">請參閱[在 HDInsight 中使用 .NET SDK 建立 Linux 型叢集](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap)。</span><span class="sxs-lookup"><span data-stu-id="cc349-145">See [Create Linux-based clusters in HDInsight using the .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-bootstrap).</span></span>

## <a name="use-resource-manager-template"></a><span data-ttu-id="cc349-146">使用 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="cc349-146">Use Resource Manager template</span></span>
<span data-ttu-id="cc349-147">Resource Manager 範本中，您可以使用啟動程序︰</span><span class="sxs-lookup"><span data-stu-id="cc349-147">You can use bootstrap in Resource Manager template:</span></span>

    "configurations": {
        …
        "hive-site": {
            "hive.metastore.client.connect.retry.delay": "5",
            "hive.execution.engine": "mr",
            "hive.security.authorization.manager": "org.apache.hadoop.hive.ql.security.authorization.DefaultHiveAuthorizationProvider"
        }
    }


![HDInsight Hadoop 自訂叢集 Bootstrap Azure Resource Manager 範本](./media/hdinsight-hadoop-customize-cluster-bootstrap/hdinsight-customize-cluster-bootstrap-arm.png)

## <a name="see-also"></a><span data-ttu-id="cc349-149">另請參閱</span><span class="sxs-lookup"><span data-stu-id="cc349-149">See also</span></span>
* <span data-ttu-id="cc349-150">[在 HDInsight 中建立 Hadoop 叢集][hdinsight-provision-cluster]提供如何使用其他自訂選項建立 HDInsight 叢集的指示。</span><span class="sxs-lookup"><span data-stu-id="cc349-150">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how to create an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="cc349-151">[開發 HDInsight 的指令碼動作指令碼][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="cc349-151">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="cc349-152">[在 HDInsight 叢集上安裝和使用 Spark][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="cc349-152">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="cc349-153">[在 HDInsight 叢集上安裝和使用 R][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="cc349-153">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="cc349-154">[在 HDInsight 叢集上安裝及使用 Solr](hdinsight-hadoop-solr-install.md)。</span><span class="sxs-lookup"><span data-stu-id="cc349-154">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="cc349-155">[在 HDInsight 叢集上安裝及使用 Giraph](hdinsight-hadoop-giraph-install.md)。</span><span class="sxs-lookup"><span data-stu-id="cc349-155">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


<span data-ttu-id="cc349-156">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "叢集建立期間的階段"</span><span class="sxs-lookup"><span data-stu-id="cc349-156">[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Stages during cluster creation"</span></span>

## <a name="appx-a-powershell-sample"></a><span data-ttu-id="cc349-157">附錄 A：PowerShell 範例</span><span class="sxs-lookup"><span data-stu-id="cc349-157">Appx-A: PowerShell sample</span></span>
<span data-ttu-id="cc349-158">此 PowerShell 指令碼會建立 HDInsight 叢集，並自訂 Hive 設定：</span><span class="sxs-lookup"><span data-stu-id="cc349-158">This PowerShell script creates an HDInsight cluster and customizes a Hive setting:</span></span>

    ####################################
    # Set these variables
    ####################################
    #region - used for creating Azure service names
    $nameToken = "<ENTER AN ALIAS>" 
    #endregion

    #region - cluster user accounts
    $httpUserName = "admin"  #HDInsight cluster username
    $httpPassword = "<ENTER A PASSWORD>" #"<Enter a Password>"

    $sshUserName = "sshuser" #HDInsight ssh user name
    $sshPassword = "<ENTER A PASSWORD>" #"<Enter a Password>"
    #endregion

    ####################################
    # Service names and varialbes
    ####################################
    #region - service names
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    $location = "East US 2"
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    ####################################
    # Connect to Azure
    ####################################
    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #endregion

    #region - Create an HDInsight cluster
    ####################################
    # Create dependent components
    ####################################
    Write-Host "Creating a resource group ..." -ForegroundColor Green
    New-AzureRmResourceGroup `
        -Name  $resourceGroupName `
        -Location $location

    Write-Host "Creating the default storage account and default blob container ..."  -ForegroundColor Green
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS

    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageContext #use the cluster name as the container name

    ####################################
    # Create a configuration object
    ####################################
    $hiveConfigValues = @{ "hive.metastore.client.socket.timeout"="90" }

    $config = New-AzureRmHDInsightClusterConfig `
        | Set-AzureRmHDInsightDefaultStorage `
            -StorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
            -StorageAccountKey $defaultStorageAccountKey `
        | Add-AzureRmHDInsightConfigValues `
            -HiveSite $hiveConfigValues 

    ####################################
    # Create an HDInsight cluster
    ####################################
    $httpPW = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$httpPW)

    $sshPW = ConvertTo-SecureString -String $sshPassword -AsPlainText -Force
    $sshCredential = New-Object System.Management.Automation.PSCredential($sshUserName,$sshPW)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -Location $location `
        -ClusterSizeInNodes 1 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.5" `
        -HttpCredential $httpCredential `
        -SshCredential $sshCredential `
        -Config $config

    ####################################
    # Verify the cluster
    ####################################
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName

    #endregion
