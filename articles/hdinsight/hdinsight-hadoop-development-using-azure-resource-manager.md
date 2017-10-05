---
title: "移轉至 HDInsight 的 Azure Resource Manager 工具 | Microsoft Docs"
description: "如何移轉至 HDInsight 叢集的 Azure Resource Manager 開發工具"
services: hdinsight
editor: cgronlun
manager: jhubbard
author: nitinme
documentationcenter: 
ms.assetid: 05efedb5-6456-4552-87ff-156d77fbe2e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 708d22b9ce53d4dbc07c6bcde0c46dcd238291bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="migrating-to-azure-resource-manager-based-development-tools-for-hdinsight-clusters"></a><span data-ttu-id="dc646-103">移轉至以 Azure Resource Manager 為基礎的開發工具 (適用於 HDInsight 叢集)</span><span class="sxs-lookup"><span data-stu-id="dc646-103">Migrating to Azure Resource Manager-based development tools for HDInsight clusters</span></span>

<span data-ttu-id="dc646-104">HDInsight 正在取代以 Azure Service Manager (ASM) 為基礎的工具 (適用於 HDInsight)。</span><span class="sxs-lookup"><span data-stu-id="dc646-104">HDInsight is deprecating Azure Service Manager (ASM)-based tools for HDInsight.</span></span> <span data-ttu-id="dc646-105">如果您已搭配使用 Azure PowerShell、Azure CLI 或 HDInsight.NET SDK 與 HDInsight 叢集，建議您可以使用以 Azure Resource Manager (ARM) 為基礎的 PowerShell、CLI 和.NET SDK 版本。</span><span class="sxs-lookup"><span data-stu-id="dc646-105">If you have been using Azure PowerShell, Azure CLI, or the HDInsight .NET SDK to work with HDInsight clusters, you are encouraged to use the Azure Resource Manager (ARM)-based versions of PowerShell, CLI, and .NET SDK going forward.</span></span> <span data-ttu-id="dc646-106">本文章提供有關如何移轉至以 ARM 為基礎的新方法指標。</span><span class="sxs-lookup"><span data-stu-id="dc646-106">This article provides pointers on how to migrate to the new ARM-based approach.</span></span> <span data-ttu-id="dc646-107">只要適用，本文也將點出 HDInsight ASM 和 ARM 之間在方法上的差異。</span><span class="sxs-lookup"><span data-stu-id="dc646-107">Wherever applicable, this article also points out the differences between the ASM and ARM approaches for HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dc646-108">對以 ASM 為基礎的 PowerShell CLI 和.NET SDK 的支援將於 **2017 年 1 月 1 日**中止。</span><span class="sxs-lookup"><span data-stu-id="dc646-108">The support for ASM based PowerShell, CLI, and .NET SDK will discontinue on **January 1, 2017**.</span></span>
> 
> 

## <a name="migrating-azure-cli-to-azure-resource-manager"></a><span data-ttu-id="dc646-109">將 Azure CLI 移轉至 Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dc646-109">Migrating Azure CLI to Azure Resource Manager</span></span>
<span data-ttu-id="dc646-110">現在 Azure CLI 是預設為 Azure Resource Manager (ARM) 模式，除非您是自先前的安裝版本升級；在此情況下，您可能需要使用 `azure config mode arm` 命令以切換到 ARM 模式。</span><span class="sxs-lookup"><span data-stu-id="dc646-110">The Azure CLI now defaults to Azure Resource Manager (ARM) mode, unless you are upgrading from a previous installation; in this case, you may need to use the `azure config mode arm` command to switch to ARM mode.</span></span>

<span data-ttu-id="dc646-111">Azure CLI 提供用來搭配使用 Azure Service Management (ASM) 與 HDInsight 的基本命令，和使用 ARM 時相同；不過某些參數和切換參數可能會有新的名稱，而且當使用 ARM 時，會有許多新的參數可供使用。</span><span class="sxs-lookup"><span data-stu-id="dc646-111">The basic commands that the Azure CLI provided to work with HDInsight using Azure Service Management (ASM) are the same when using ARM; however some parameters and switches may have new names, and there are many new parameters available when using ARM.</span></span> <span data-ttu-id="dc646-112">例如，您現在可以使用 `azure hdinsight cluster create` 來指定建立叢集所在的 Azure 虛擬網路，或是 Hive 和 Oozie 的中繼存放區資訊。</span><span class="sxs-lookup"><span data-stu-id="dc646-112">For example, you can now use `azure hdinsight cluster create` to specify the Azure Virtual Network that a cluster should be created in, or Hive and Oozie metastore information.</span></span>

<span data-ttu-id="dc646-113">透過 Azure Resource Manager 來使用 HDInsight 的基本命令為︰</span><span class="sxs-lookup"><span data-stu-id="dc646-113">Basic commands for working with HDInsight through Azure Resource Manager are:</span></span>

* <span data-ttu-id="dc646-114">`azure hdinsight cluster create` - 建立新的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="dc646-114">`azure hdinsight cluster create` - creates a new HDInsight cluster</span></span>
* <span data-ttu-id="dc646-115">`azure hdinsight cluster delete` - 刪除現有的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="dc646-115">`azure hdinsight cluster delete` - deletes an existing HDInsight cluster</span></span>
* <span data-ttu-id="dc646-116">`azure hdinsight cluster show` - 顯示現有叢集的相關資訊</span><span class="sxs-lookup"><span data-stu-id="dc646-116">`azure hdinsight cluster show` - display information about an existing cluster</span></span>
* <span data-ttu-id="dc646-117">`azure hdinsight cluster list` - 列出適用於您 Azure 訂用帳戶的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="dc646-117">`azure hdinsight cluster list` - lists HDInsight clusters for your Azure subscription</span></span>

<span data-ttu-id="dc646-118">使用 `-h` 切換參數來檢查每個命令可用的參數和切換參數。</span><span class="sxs-lookup"><span data-stu-id="dc646-118">Use the `-h` switch to inspect the parameters and switches available for each command.</span></span>

### <a name="new-commands"></a><span data-ttu-id="dc646-119">新的命令</span><span class="sxs-lookup"><span data-stu-id="dc646-119">New commands</span></span>
<span data-ttu-id="dc646-120">可用於 Azure Resource Manager 的新命令︰</span><span class="sxs-lookup"><span data-stu-id="dc646-120">New commands available with Azure Resource Manager are:</span></span>

* <span data-ttu-id="dc646-121">`azure hdinsight cluster resize` - 在叢集中動態變更背景工作節點數目</span><span class="sxs-lookup"><span data-stu-id="dc646-121">`azure hdinsight cluster resize` - dynamically changes the number of worker nodes in the cluster</span></span>
* <span data-ttu-id="dc646-122">`azure hdinsight cluster enable-http-access` - 啟用 HTTP 對叢集的存取 (預設為開啟)</span><span class="sxs-lookup"><span data-stu-id="dc646-122">`azure hdinsight cluster enable-http-access` - enables HTTPs access to the cluster (on by default)</span></span>
* <span data-ttu-id="dc646-123">`azure hdinsight cluster disable-http-access` - 停用 HTTP 對叢集的存取</span><span class="sxs-lookup"><span data-stu-id="dc646-123">`azure hdinsight cluster disable-http-access` - disables HTTPs access to the cluster</span></span>
* <span data-ttu-id="dc646-124">`azure hdinsight script-action` - 在叢集上提供建立/管理指令碼動作的命令</span><span class="sxs-lookup"><span data-stu-id="dc646-124">`azure hdinsight script-action` - provides commands for creating/managing Script Actions on a cluster</span></span>
* <span data-ttu-id="dc646-125">`azure hdinsight config` -提供可用於建立組態檔的命令，該組態檔可與 `hdinsight cluster create` 命令一起使用，以提供組態資訊。</span><span class="sxs-lookup"><span data-stu-id="dc646-125">`azure hdinsight config` - provides commands for creating a configuration file that can be used with the `hdinsight cluster create` command to provide configuration information.</span></span>

### <a name="deprecated-commands"></a><span data-ttu-id="dc646-126">已取代的命令</span><span class="sxs-lookup"><span data-stu-id="dc646-126">Deprecated commands</span></span>
<span data-ttu-id="dc646-127">如果您使用 `azure hdinsight job` 命令將工作提交至 HDInsight 叢集，便無法透過 ARM 的命令來使用。</span><span class="sxs-lookup"><span data-stu-id="dc646-127">If you use the `azure hdinsight job` commands to submit jobs to your HDInsight cluster, these are not available through the ARM commands.</span></span> <span data-ttu-id="dc646-128">如果您需要以程式設計方式，自指令碼將工作提交至 HDInsight，您應該改用 HDInsight 所提供的 REST API。</span><span class="sxs-lookup"><span data-stu-id="dc646-128">If you need to programmatically submit jobs to HDInsight from scripts, you should instead use the REST APIs provided by HDInsight.</span></span> <span data-ttu-id="dc646-129">如需有關如何使用 REST API 提交工作的詳細資訊，請參閱下列文件。</span><span class="sxs-lookup"><span data-stu-id="dc646-129">For more information on submitting jobs using REST APIs, see the following documents.</span></span>

* [<span data-ttu-id="dc646-130">使用 Curl 搭配執行 MapReduce 工作與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="dc646-130">Run MapReduce jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-mapreduce-curl.md)
* [<span data-ttu-id="dc646-131">使用 Curl 搭配執行 Hive 查詢 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="dc646-131">Run Hive queries with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-hive-curl.md)
* [<span data-ttu-id="dc646-132">使用 Curl 搭配執行 Pig 工作與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="dc646-132">Run Pig jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-pig-curl.md)

<span data-ttu-id="dc646-133">如需有關執行 MapReduce、Hive 和 Pig 互動方式的其他方法，請參閱[搭配使用 MapReduce 與 HDInsight 上的 Hadoop](hdinsight-use-mapreduce.md)、[搭配使用 Hive 與 HDInsight 上的 Hadoop](hdinsight-use-hive.md) 和[搭配使用 Pig 與 HDInsight 上的 Hadoop](hdinsight-use-pig.md)。</span><span class="sxs-lookup"><span data-stu-id="dc646-133">For information on other ways to run MapReduce, Hive, and Pig interactively, see [Use MapReduce with Hadoop on HDInsight](hdinsight-use-mapreduce.md), [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md), and [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

### <a name="examples"></a><span data-ttu-id="dc646-134">範例</span><span class="sxs-lookup"><span data-stu-id="dc646-134">Examples</span></span>
<span data-ttu-id="dc646-135">**建立叢集**</span><span class="sxs-lookup"><span data-stu-id="dc646-135">**Creating a cluster**</span></span>

* <span data-ttu-id="dc646-136">舊的命令 (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="dc646-136">Old command (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>
* <span data-ttu-id="dc646-137">新的命令 (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="dc646-137">New command (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>

<span data-ttu-id="dc646-138">**刪除叢集**</span><span class="sxs-lookup"><span data-stu-id="dc646-138">**Deleting a cluster**</span></span>

* <span data-ttu-id="dc646-139">舊的命令 (ASM) - `azure hdinsight cluster delete myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="dc646-139">Old command (ASM) - `azure hdinsight cluster delete myhdicluster`</span></span>
* <span data-ttu-id="dc646-140">新的命令 (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="dc646-140">New command (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span></span>

<span data-ttu-id="dc646-141">**列出叢集**</span><span class="sxs-lookup"><span data-stu-id="dc646-141">**List clusters**</span></span>

* <span data-ttu-id="dc646-142">舊的命令 (ASM) - `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="dc646-142">Old command (ASM) - `azure hdinsight cluster list`</span></span>
* <span data-ttu-id="dc646-143">新的命令 (ARM) - `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="dc646-143">New command (ARM) - `azure hdinsight cluster list`</span></span>

> [!NOTE]
> <span data-ttu-id="dc646-144">針對清單命令，當使用 `-g` 來指定資源群組，將只會傳回在指定資源群組中的叢集。</span><span class="sxs-lookup"><span data-stu-id="dc646-144">For the list command, specifying the resource group using `-g` will return only the clusters in the specified resource group.</span></span>
> 
> 

<span data-ttu-id="dc646-145">**顯示叢集資訊**</span><span class="sxs-lookup"><span data-stu-id="dc646-145">**Show cluster information**</span></span>

* <span data-ttu-id="dc646-146">舊的命令 (ASM) - `azure hdinsight cluster show myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="dc646-146">Old command (ASM) - `azure hdinsight cluster show myhdicluster`</span></span>
* <span data-ttu-id="dc646-147">新的命令 (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="dc646-147">New command (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span></span>

## <a name="migrating-azure-powershell-to-azure-resource-manager"></a><span data-ttu-id="dc646-148">將 Azure PowerShell 移轉至 Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dc646-148">Migrating Azure PowerShell to Azure Resource Manager</span></span>
<span data-ttu-id="dc646-149">有關 Azure PowerShell 在 Azure Resource Manager (ARM) 模式中的一般資訊，請參閱 [搭配使用 Azure PowerShell 與 Azure Resource Manager](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="dc646-149">The general information about Azure PowerShell in the Azure Resource Manager (ARM) mode can be found at [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="dc646-150">Azure PowerShell ARM Cmdlet 可與 ASM Cmdlet 並存安裝。</span><span class="sxs-lookup"><span data-stu-id="dc646-150">The Azure PowerShell ARM cmdlets can be installed side-by-side with the ASM cmdlets.</span></span> <span data-ttu-id="dc646-151">來自兩種模式的 Cmdlet 可依其名稱來區分。</span><span class="sxs-lookup"><span data-stu-id="dc646-151">The cmdlets from the two modes can be distinguished by their names.</span></span>  <span data-ttu-id="dc646-152">ARM 模式的 Cmdlet 名稱中有「AzureRmHDInsight」，對比 ASM 模式中的「AzureHDInsight」。</span><span class="sxs-lookup"><span data-stu-id="dc646-152">The ARM mode has *AzureRmHDInsight* in the cmdlet names comparing to *AzureHDInsight* in the ASM mode.</span></span>  <span data-ttu-id="dc646-153">例如，「New-AzureRmHDInsightCluster」對比「New-AzureHDInsightCluster」。</span><span class="sxs-lookup"><span data-stu-id="dc646-153">For example, *New-AzureRmHDInsightCluster* vs. *New-AzureHDInsightCluster*.</span></span> <span data-ttu-id="dc646-154">某些參數和切換參數可能會有新的名稱，而且當使用 ARM 時，會有許多新的參數可供使用。</span><span class="sxs-lookup"><span data-stu-id="dc646-154">Parameters and switches may have news names, and there are many new parameters available when using ARM.</span></span>  <span data-ttu-id="dc646-155">例如，數個 Cmdlet 需要名為 -ResourceGroupName 的新切換參數。</span><span class="sxs-lookup"><span data-stu-id="dc646-155">For example, several cmdlets require a new switch called *-ResourceGroupName*.</span></span> 

<span data-ttu-id="dc646-156">在您可以使用 HDInsight Cmdlet 之前，必須連線到您的 Azure 帳戶，並建立新的資源群組︰</span><span class="sxs-lookup"><span data-stu-id="dc646-156">Before you can use the HDInsight cmdlets, you must connect to your Azure account, and create a new resource group:</span></span>

* <span data-ttu-id="dc646-157">Login-AzureRmAccount 或 [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx)。</span><span class="sxs-lookup"><span data-stu-id="dc646-157">Login-AzureRmAccount or [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span></span> <span data-ttu-id="dc646-158">請參閱 [使用 Azure Resource Manager 驗證服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span><span class="sxs-lookup"><span data-stu-id="dc646-158">See [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span></span>
* [<span data-ttu-id="dc646-159">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="dc646-159">New-AzureRmResourceGroup</span></span>](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a><span data-ttu-id="dc646-160">重新命名 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="dc646-160">Renamed cmdlets</span></span>
<span data-ttu-id="dc646-161">若要在 Windows PowerShell 主控台中列出 HDInsight ASM Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="dc646-161">To list the HDInsight ASM cmdlets in Windows PowerShell console:</span></span>

    help *azurermhdinsight*

<span data-ttu-id="dc646-162">下表列出 ASM Cmdlet 和其在 ARM 模式中的名稱︰</span><span class="sxs-lookup"><span data-stu-id="dc646-162">The following table lists the ASM cmdlets and their names in the ARM mode:</span></span>

| <span data-ttu-id="dc646-163">ASM cmdlets</span><span class="sxs-lookup"><span data-stu-id="dc646-163">ASM cmdlets</span></span> | <span data-ttu-id="dc646-164">ARM cmdlets</span><span class="sxs-lookup"><span data-stu-id="dc646-164">ARM cmdlets</span></span> |
| --- | --- |
| <span data-ttu-id="dc646-165">Add-AzureHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="dc646-165">Add-AzureHDInsightConfigValues</span></span> |[<span data-ttu-id="dc646-166">Add-AzureRmHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="dc646-166">Add-AzureRmHDInsightConfigValues</span></span>](https://msdn.microsoft.com/library/mt603530.aspx) |
| <span data-ttu-id="dc646-167">Add-AzureHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="dc646-167">Add-AzureHDInsightMetastore</span></span> |[<span data-ttu-id="dc646-168">Add-AzureRmHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="dc646-168">Add-AzureRmHDInsightMetastore</span></span>](https://msdn.microsoft.com/library/mt603670.aspx) |
| <span data-ttu-id="dc646-169">Add-AzureHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="dc646-169">Add-AzureHDInsightScriptAction</span></span> |[<span data-ttu-id="dc646-170">Add-AzureRmHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="dc646-170">Add-AzureRmHDInsightScriptAction</span></span>](https://msdn.microsoft.com/library/mt603527.aspx) |
| <span data-ttu-id="dc646-171">Add-AzureHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="dc646-171">Add-AzureHDInsightStorage</span></span> |[<span data-ttu-id="dc646-172">Add-AzureRmHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="dc646-172">Add-AzureRmHDInsightStorage</span></span>](https://msdn.microsoft.com/library/mt619445.aspx) |
| <span data-ttu-id="dc646-173">Get-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="dc646-173">Get-AzureHDInsightCluster</span></span> |[<span data-ttu-id="dc646-174">Get AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="dc646-174">Get-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619371.aspx) |
| <span data-ttu-id="dc646-175">Get-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="dc646-175">Get-AzureHDInsightJob</span></span> |[<span data-ttu-id="dc646-176">Get-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="dc646-176">Get-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603590.aspx) |
| <span data-ttu-id="dc646-177">Get-AzureHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="dc646-177">Get-AzureHDInsightJobOutput</span></span> |[<span data-ttu-id="dc646-178">Get-AzureRmHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="dc646-178">Get-AzureRmHDInsightJobOutput</span></span>](https://msdn.microsoft.com/library/mt603793.aspx) |
| <span data-ttu-id="dc646-179">Get-AzureHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="dc646-179">Get-AzureHDInsightProperties</span></span> |[<span data-ttu-id="dc646-180">Get-AzureRmHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="dc646-180">Get-AzureRmHDInsightProperties</span></span>](https://msdn.microsoft.com/library/mt603546.aspx) |
| <span data-ttu-id="dc646-181">Grant-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="dc646-181">Grant-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="dc646-182">Grant-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="dc646-182">Grant-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619407.aspx) |
| <span data-ttu-id="dc646-183">Grant-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="dc646-183">Grant-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="dc646-184">Grant-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="dc646-184">Grant-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603717.aspx) |
| <span data-ttu-id="dc646-185">Invoke-AzureHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="dc646-185">Invoke-AzureHDInsightHiveJob</span></span> |[<span data-ttu-id="dc646-186">Invoke-AzureRmHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="dc646-186">Invoke-AzureRmHDInsightHiveJob</span></span>](https://msdn.microsoft.com/library/mt603593.aspx) |
| <span data-ttu-id="dc646-187">New-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="dc646-187">New-AzureHDInsightCluster</span></span> |[<span data-ttu-id="dc646-188">New-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="dc646-188">New-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619331.aspx) |
| <span data-ttu-id="dc646-189">New-AzureHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="dc646-189">New-AzureHDInsightClusterConfig</span></span> |[<span data-ttu-id="dc646-190">New-AzureRmHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="dc646-190">New-AzureRmHDInsightClusterConfig</span></span>](https://msdn.microsoft.com/library/mt603700.aspx) |
| <span data-ttu-id="dc646-191">New-AzureHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="dc646-191">New-AzureHDInsightHiveJobDefinition</span></span> |[<span data-ttu-id="dc646-192">New-AzureRmHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="dc646-192">New-AzureRmHDInsightHiveJobDefinition</span></span>](https://msdn.microsoft.com/library/mt619448.aspx) |
| <span data-ttu-id="dc646-193">New-AzureHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="dc646-193">New-AzureHDInsightMapReduceJobDefinition</span></span> |[<span data-ttu-id="dc646-194">New-AzureRmHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="dc646-194">New-AzureRmHDInsightMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="dc646-195">New-AzureHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="dc646-195">New-AzureHDInsightPigJobDefinition</span></span> |[<span data-ttu-id="dc646-196">New-AzureRmHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="dc646-196">New-AzureRmHDInsightPigJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603671.aspx) |
| <span data-ttu-id="dc646-197">New-AzureHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="dc646-197">New-AzureHDInsightSqoopJobDefinition</span></span> |[<span data-ttu-id="dc646-198">New-AzureRmHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="dc646-198">New-AzureRmHDInsightSqoopJobDefinition</span></span>](https://msdn.microsoft.com/library/mt608551.aspx) |
| <span data-ttu-id="dc646-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="dc646-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span></span> |[<span data-ttu-id="dc646-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="dc646-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="dc646-201">Remove-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="dc646-201">Remove-AzureHDInsightCluster</span></span> |[<span data-ttu-id="dc646-202">Remove-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="dc646-202">Remove-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619431.aspx) |
| <span data-ttu-id="dc646-203">Revoke-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="dc646-203">Revoke-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="dc646-204">Revoke-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="dc646-204">Revoke-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619375.aspx) |
| <span data-ttu-id="dc646-205">Revoke-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="dc646-205">Revoke-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="dc646-206">Revoke-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="dc646-206">Revoke-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603523.aspx) |
| <span data-ttu-id="dc646-207">Set-AzureHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="dc646-207">Set-AzureHDInsightClusterSize</span></span> |[<span data-ttu-id="dc646-208">Set-AzureRmHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="dc646-208">Set-AzureRmHDInsightClusterSize</span></span>](https://msdn.microsoft.com/library/mt603513.aspx) |
| <span data-ttu-id="dc646-209">Set-AzureHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="dc646-209">Set-AzureHDInsightDefaultStorage</span></span> |[<span data-ttu-id="dc646-210">Set-AzureRmHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="dc646-210">Set-AzureRmHDInsightDefaultStorage</span></span>](https://msdn.microsoft.com/library/mt603486.aspx) |
| <span data-ttu-id="dc646-211">Start-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="dc646-211">Start-AzureHDInsightJob</span></span> |[<span data-ttu-id="dc646-212">Start-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="dc646-212">Start-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603798.aspx) |
| <span data-ttu-id="dc646-213">Stop-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="dc646-213">Stop-AzureHDInsightJob</span></span> |[<span data-ttu-id="dc646-214">Stop-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="dc646-214">Stop-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt619424.aspx) |
| <span data-ttu-id="dc646-215">Use-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="dc646-215">Use-AzureHDInsightCluster</span></span> |[<span data-ttu-id="dc646-216">Use-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="dc646-216">Use-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619442.aspx) |
| <span data-ttu-id="dc646-217">Wait-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="dc646-217">Wait-AzureHDInsightJob</span></span> |[<span data-ttu-id="dc646-218">Wait-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="dc646-218">Wait-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a><span data-ttu-id="dc646-219">新的 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="dc646-219">New cmdlets</span></span>
<span data-ttu-id="dc646-220">下列是只在 ARM 模式中使用的新 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="dc646-220">The following are the new cmdlets that are only available in the ARM mode.</span></span> 

<span data-ttu-id="dc646-221">**指令碼動作相關的 Cmdlet：**</span><span class="sxs-lookup"><span data-stu-id="dc646-221">**Script action related cmdlets:**</span></span>

* <span data-ttu-id="dc646-222">**Get-AzureRmHDInsightPersistedScriptAction**︰取得叢集的持續性指令碼動作，並依時間先後順序列出，或取得有關指定持續性指令碼動作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="dc646-222">**Get-AzureRmHDInsightPersistedScriptAction**: Gets the persisted script actions for a cluster and lists them in chronological order, or gets details for a specified persisted script action.</span></span> 
* <span data-ttu-id="dc646-223">**Get AzureRmHDInsightScriptActionHistory**︰ 取得叢集的指令碼動作記錄，並依反向的時間先後順序列出，或取得有關先前執行指令碼動作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="dc646-223">**Get-AzureRmHDInsightScriptActionHistory**: Gets the script action history for a cluster and lists it in reverse chronological order, or gets details of a previously executed script action.</span></span> 
* <span data-ttu-id="dc646-224">**Remove-AzureRmHDInsightPersistedScriptAction**︰自 HDInsight 叢集移除持續性指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="dc646-224">**Remove-AzureRmHDInsightPersistedScriptAction**: Removes a persisted script action from an HDInsight cluster.</span></span>
* <span data-ttu-id="dc646-225">**Set-AzureRmHDInsightPersistedScriptAction**︰將先前執行的指令碼動作設定為持續性指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="dc646-225">**Set-AzureRmHDInsightPersistedScriptAction**: Sets a previously executed script action to be a persisted script action.</span></span>
* <span data-ttu-id="dc646-226">**Submit-AzureRmHDInsightScriptAction**︰將新的指令碼動作提交至 Azure HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="dc646-226">**Submit-AzureRmHDInsightScriptAction**: Submits a new script action to an Azure HDInsight cluster.</span></span> 

<span data-ttu-id="dc646-227">如需關於其他使用方式的詳細資訊，請參閱 [使用指令碼動作自訂以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="dc646-227">For additional usage information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="dc646-228">**叢集身分識別相關的 Cmdlet：**</span><span class="sxs-lookup"><span data-stu-id="dc646-228">**Clsuter identity related cmdlets:**</span></span>

* <span data-ttu-id="dc646-229">**Add-AzureRmHDInsightClusterIdentity**︰將叢集身分識別新增至叢集組態物件，以便讓 HDInsight 叢集可以存取 Azure Data Lake 存放區。</span><span class="sxs-lookup"><span data-stu-id="dc646-229">**Add-AzureRmHDInsightClusterIdentity**: Adds a cluster identity to a cluster configuration object so that the HDInsight cluster can access Azure Data Lake Stores.</span></span> <span data-ttu-id="dc646-230">請參閱 [使用 Azure PowerShell 建立具 Data Lake Store 的 HDInsight 叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="dc646-230">See [Create an HDInsight cluster with Data Lake Store using Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

### <a name="examples"></a><span data-ttu-id="dc646-231">範例</span><span class="sxs-lookup"><span data-stu-id="dc646-231">Examples</span></span>
<span data-ttu-id="dc646-232">**建立叢集**</span><span class="sxs-lookup"><span data-stu-id="dc646-232">**Create cluster**</span></span>

<span data-ttu-id="dc646-233">舊的命令 (ASM)：</span><span class="sxs-lookup"><span data-stu-id="dc646-233">Old command (ASM):</span></span> 

    New-AzureHDInsightCluster `
        -Name $clusterName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainerName $containerName `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -Credential $httpCredential `
        -SshCredential $sshCredential

<span data-ttu-id="dc646-234">新的命令 (ARM)：</span><span class="sxs-lookup"><span data-stu-id="dc646-234">New command (ARM):</span></span>

    New-AzureRmHDInsightCluster `
        -ClusterName $clusterName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainer $containerName  `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -HttpCredential $httpcredentials `
        -SshCredential $sshCredentials


<span data-ttu-id="dc646-235">**刪除叢集**</span><span class="sxs-lookup"><span data-stu-id="dc646-235">**Delete cluster**</span></span>

<span data-ttu-id="dc646-236">舊的命令 (ASM)：</span><span class="sxs-lookup"><span data-stu-id="dc646-236">Old command (ASM):</span></span>

    Remove-AzureHDInsightCluster -name $clusterName 

<span data-ttu-id="dc646-237">新的命令 (ARM)：</span><span class="sxs-lookup"><span data-stu-id="dc646-237">New command (ARM):</span></span>

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

<span data-ttu-id="dc646-238">**列出叢集**</span><span class="sxs-lookup"><span data-stu-id="dc646-238">**List cluster**</span></span>

<span data-ttu-id="dc646-239">舊的命令 (ASM)：</span><span class="sxs-lookup"><span data-stu-id="dc646-239">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster

<span data-ttu-id="dc646-240">新的命令 (ARM)：</span><span class="sxs-lookup"><span data-stu-id="dc646-240">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster 

<span data-ttu-id="dc646-241">**顯示叢集**</span><span class="sxs-lookup"><span data-stu-id="dc646-241">**Show cluster**</span></span>

<span data-ttu-id="dc646-242">舊的命令 (ASM)：</span><span class="sxs-lookup"><span data-stu-id="dc646-242">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster -Name $clusterName

<span data-ttu-id="dc646-243">新的命令 (ARM)：</span><span class="sxs-lookup"><span data-stu-id="dc646-243">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a><span data-ttu-id="dc646-244">其他範例</span><span class="sxs-lookup"><span data-stu-id="dc646-244">Other samples</span></span>
* [<span data-ttu-id="dc646-245">建立 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="dc646-245">Create HDInsight clusters</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="dc646-246">提交 Hive 工作</span><span class="sxs-lookup"><span data-stu-id="dc646-246">Submit Hive jobs</span></span>](hdinsight-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="dc646-247">提交 Pig 工作</span><span class="sxs-lookup"><span data-stu-id="dc646-247">Submit Pig jobs</span></span>](hdinsight-hadoop-use-pig-powershell.md)
* [<span data-ttu-id="dc646-248">提交 Sqoop 工作</span><span class="sxs-lookup"><span data-stu-id="dc646-248">Submit Sqoop jobs</span></span>](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-to-the-arm-based-hdinsight-net-sdk"></a><span data-ttu-id="dc646-249">移轉至以 ARM 為基礎的 HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="dc646-249">Migrating to the ARM-based HDInsight .NET SDK</span></span>
<span data-ttu-id="dc646-250">以 Azure Service Management (ASM) 為基礎的 [HDInsight.NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) 現在已被取代。</span><span class="sxs-lookup"><span data-stu-id="dc646-250">The Azure Service Management-based [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is now deprecated.</span></span> <span data-ttu-id="dc646-251">建議您使用以 Azure Resource Management (ARM) 為基礎的 [HDInsight.NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx)。</span><span class="sxs-lookup"><span data-stu-id="dc646-251">You are encouraged to use the Azure Resource Management-based [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span></span> <span data-ttu-id="dc646-252">下列以 ASM 為基礎的 HDInsight 封裝會被取代。</span><span class="sxs-lookup"><span data-stu-id="dc646-252">The following ASM-based HDInsight packages are being deprecated.</span></span>

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

<span data-ttu-id="dc646-253">本節提供有關如何使用以 ARM 為基礎的 SDK 來執行特定工作的詳細資訊指標。</span><span class="sxs-lookup"><span data-stu-id="dc646-253">This section provides pointers to more information on how to perform certain tasks using the ARM-based SDK.</span></span>

| <span data-ttu-id="dc646-254">如何...使用以 ARM 為基礎的 HDInsight SDK</span><span class="sxs-lookup"><span data-stu-id="dc646-254">How to... using the ARM-based HDInsight SDK</span></span> | <span data-ttu-id="dc646-255">連結</span><span class="sxs-lookup"><span data-stu-id="dc646-255">Links</span></span> |
| --- | --- |
| <span data-ttu-id="dc646-256">使用 .NET SDK 建立 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="dc646-256">Create HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="dc646-257">請參閱 [使用.NET SDK 來建立 HDInsight 叢集](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="dc646-257">See [Create HDInsight clusters using .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="dc646-258">搭配使用指令碼動作與 .NET SDK 來自訂叢集</span><span class="sxs-lookup"><span data-stu-id="dc646-258">Customize a cluster using Script Action with .NET SDK</span></span> |<span data-ttu-id="dc646-259">請參閱 [使用指令碼動作來自訂 HDInsight Linux 叢集](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span><span class="sxs-lookup"><span data-stu-id="dc646-259">See [Customize HDInsight Linux clusters using Script Action](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span></span> |
| <span data-ttu-id="dc646-260">搭配使用 Azure Active Directory 與 .NET SDK，以互動方式驗證應用程式</span><span class="sxs-lookup"><span data-stu-id="dc646-260">Authenticate applications interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="dc646-261">請參閱 [使用 .NET SDK 執行 Hive 查詢](hdinsight-hadoop-use-hive-dotnet-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="dc646-261">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span> <span data-ttu-id="dc646-262">在本文中的程式碼片段會使用互動式驗證方法。</span><span class="sxs-lookup"><span data-stu-id="dc646-262">The code snippet in this article uses the interactive authentication approach.</span></span> |
| <span data-ttu-id="dc646-263">搭配使用 Azure Active Directory 與 .NET SDK，以非互動方式驗證應用程式</span><span class="sxs-lookup"><span data-stu-id="dc646-263">Authenticate applications non-interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="dc646-264">請參閱 [建立 HDInsight 的非互動式應用程式](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span><span class="sxs-lookup"><span data-stu-id="dc646-264">See [Create non-interactive applications for HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span></span> |
| <span data-ttu-id="dc646-265">使用 .NET SDK 提交 Hive 作業</span><span class="sxs-lookup"><span data-stu-id="dc646-265">Submit a Hive job using .NET SDK</span></span> |<span data-ttu-id="dc646-266">請參閱 [提交 Hive 工作](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="dc646-266">See [Submit Hive jobs](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="dc646-267">使用 .NET SDK 提交 Pig 作業</span><span class="sxs-lookup"><span data-stu-id="dc646-267">Submit a Pig job using .NET SDK</span></span> |<span data-ttu-id="dc646-268">請參閱 [提交 Pig 工作](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="dc646-268">See [Submit Pig jobs](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="dc646-269">使用 .NET SDK 提交 Sqoop 作業</span><span class="sxs-lookup"><span data-stu-id="dc646-269">Submit a Sqoop job using .NET SDK</span></span> |<span data-ttu-id="dc646-270">請參閱 [提交 Sqoop 工作](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="dc646-270">See [Submit Sqoop jobs](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="dc646-271">使用 .NET SDK 列出 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="dc646-271">List HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="dc646-272">請參閱 [列出 HDInsight 叢集](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span><span class="sxs-lookup"><span data-stu-id="dc646-272">See [List HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span></span> |
| <span data-ttu-id="dc646-273">使用.NET SDK 調整 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="dc646-273">Scale HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="dc646-274">請參閱 [調整 HDInsight 叢集](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span><span class="sxs-lookup"><span data-stu-id="dc646-274">See [Scale HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span></span> |
| <span data-ttu-id="dc646-275">使用.NET SDK 授與/撤銷存取至 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="dc646-275">Grant/revoke access to HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="dc646-276">請參閱 [「授與/撤銷存取至 HDInsight 叢集」](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span><span class="sxs-lookup"><span data-stu-id="dc646-276">See [Grant/revoke access to HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span></span> |
| <span data-ttu-id="dc646-277">使用 .NET SDK 更新 HDInsight 叢集的 HTTP 使用者認證</span><span class="sxs-lookup"><span data-stu-id="dc646-277">Update HTTP user credentials for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="dc646-278">請參閱 [「更新 HDInsight 叢集的 HTTP 使用者認證」](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span><span class="sxs-lookup"><span data-stu-id="dc646-278">See [Update HTTP user credentials for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span></span> |
| <span data-ttu-id="dc646-279">尋找使用.NET SDK 的 HDInsight 叢集預設儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="dc646-279">Find the default storage account for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="dc646-280">請參閱 [「尋找 HDInsight 叢集預設的儲存體帳戶」](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span><span class="sxs-lookup"><span data-stu-id="dc646-280">See [Find the default storage account for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span></span> |
| <span data-ttu-id="dc646-281">使用 .NET SDK 刪除 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="dc646-281">Delete HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="dc646-282">請參閱 [「刪除 HDInsight 叢集」](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="dc646-282">See [Delete HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span></span> |

### <a name="examples"></a><span data-ttu-id="dc646-283">範例</span><span class="sxs-lookup"><span data-stu-id="dc646-283">Examples</span></span>
<span data-ttu-id="dc646-284">下列是關於如何使用以 ASM 為基礎的 SDK 和以 ARM 為基礎的 SDK 的對等程式碼片段，來執行作業的一些範例。</span><span class="sxs-lookup"><span data-stu-id="dc646-284">Following are some examples on how an operation is performed using the ASM-based SDK and the equivalent code snippet for the ARM-based SDK.</span></span>

<span data-ttu-id="dc646-285">**建立叢集 CRUD 用戶端**</span><span class="sxs-lookup"><span data-stu-id="dc646-285">**Creating a cluster CRUD client**</span></span>

* <span data-ttu-id="dc646-286">舊的命令 (ASM)</span><span class="sxs-lookup"><span data-stu-id="dc646-286">Old command (ASM)</span></span>
  
        //Certificate auth
        //This logs the application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* <span data-ttu-id="dc646-287">新的命令 (ARM) (服務主體的授權)</span><span class="sxs-lookup"><span data-stu-id="dc646-287">New command (ARM) (Service principal authorization)</span></span>
  
        //Service principal auth
        //This will log the application in as itself, rather than on behalf of a specific user.
        //For details, including how to set up the application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* <span data-ttu-id="dc646-288">新的命令 (ARM) (使用者的授權)</span><span class="sxs-lookup"><span data-stu-id="dc646-288">New command (ARM) (User authorization)</span></span>
  
        //User auth
        //This will log the application in on behalf of the user.
        //The end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

<span data-ttu-id="dc646-289">**建立叢集**</span><span class="sxs-lookup"><span data-stu-id="dc646-289">**Creating a cluster**</span></span>

* <span data-ttu-id="dc646-290">舊的命令 (ASM)</span><span class="sxs-lookup"><span data-stu-id="dc646-290">Old command (ASM)</span></span>
  
        var clusterInfo = new ClusterCreateParameters
                    {
                        Name = dnsName,
                        DefaultStorageAccountKey = key,
                        DefaultStorageContainer = defaultStorageContainer,
                        DefaultStorageAccountName = storageAccountDnsName,
                        ClusterSizeInNodes = 1,
                        ClusterType = type,
                        Location = "West US",
                        UserName = "admin",
                        Password = "*******",
                        Version = version,
                        HeadNodeSize = NodeVMSize.Large,
                    };
        clusterInfo.CoreConfiguration.Add(new KeyValuePair<string, string>("config1", "value1"));
        client.CreateCluster(clusterInfo);
* <span data-ttu-id="dc646-291">新的命令 (ARM)</span><span class="sxs-lookup"><span data-stu-id="dc646-291">New command (ARM)</span></span>
  
        var clusterCreateParameters = new ClusterCreateParameters
            {
                Location = "West US",
                ClusterType = "Hadoop",
                Version = "3.1",
                OSType = OSType.Linux,
                DefaultStorageAccountName = "mystorage.blob.core.windows.net",
                DefaultStorageAccountKey =
                    "O9EQvp3A3AjXq/W27rst1GQfLllhp0gUeiUUn2D8zX2lU3taiXSSfqkZlcPv+nQcYUxYw==",
                UserName = "hadoopuser",
                Password = "*******",
                HeadNodeSize = "ExtraLarge",
                RdpUsername = "hdirp",
                RdpPassword = ""*******",
                RdpAccessExpiry = new DateTime(2025, 3, 1),
                ClusterSizeInNodes = 5
            };
        var coreConfigs = new Dictionary<string, string> {{"config1", "value1"}};
        clusterCreateParameters.Configurations.Add(ConfigurationKey.CoreSite, coreConfigs);

<span data-ttu-id="dc646-292">**啟用 HTTP 存取**</span><span class="sxs-lookup"><span data-stu-id="dc646-292">**Enabling HTTP access**</span></span>

* <span data-ttu-id="dc646-293">舊的命令 (ASM)</span><span class="sxs-lookup"><span data-stu-id="dc646-293">Old command (ASM)</span></span>
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* <span data-ttu-id="dc646-294">新的命令 (ARM)</span><span class="sxs-lookup"><span data-stu-id="dc646-294">New command (ARM)</span></span>
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

<span data-ttu-id="dc646-295">**刪除叢集**</span><span class="sxs-lookup"><span data-stu-id="dc646-295">**Deleting a cluster**</span></span>

* <span data-ttu-id="dc646-296">舊的命令 (ASM)</span><span class="sxs-lookup"><span data-stu-id="dc646-296">Old command (ASM)</span></span>
  
        client.DeleteCluster(dnsName);
* <span data-ttu-id="dc646-297">新的命令 (ARM)</span><span class="sxs-lookup"><span data-stu-id="dc646-297">New command (ARM)</span></span>
  
        client.Clusters.Delete(resourceGroup, dnsname);

