---
title: "aaaMigrate tooAzure 資源管理員工具 hdinsight |Microsoft 文件"
description: "HDInsight 叢集的 toomigrate tooAzure 資源管理員開發工具的方式"
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
ms.openlocfilehash: c087ae63d2544e5badae6be9c258f783aa92e2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-resource-manager-based-development-tools-for-hdinsight-clusters"></a><span data-ttu-id="864f6-103">HDInsight 叢集的移轉 tooAzure 資源管理員為基礎的開發工具</span><span class="sxs-lookup"><span data-stu-id="864f6-103">Migrating tooAzure Resource Manager-based development tools for HDInsight clusters</span></span>

<span data-ttu-id="864f6-104">HDInsight 正在取代以 Azure Service Manager (ASM) 為基礎的工具 (適用於 HDInsight)。</span><span class="sxs-lookup"><span data-stu-id="864f6-104">HDInsight is deprecating Azure Service Manager (ASM)-based tools for HDInsight.</span></span> <span data-ttu-id="864f6-105">如果您已在使用 Azure PowerShell、 Azure CLI 或 hello HDInsight.NET SDK toowork 與 HDInsight 叢集，則建議的 toouse hello Azure 資源管理員 arm 版本的 PowerShell、 CLI 及接下來的.NET SDK。</span><span class="sxs-lookup"><span data-stu-id="864f6-105">If you have been using Azure PowerShell, Azure CLI, or hello HDInsight .NET SDK toowork with HDInsight clusters, you are encouraged toouse hello Azure Resource Manager (ARM)-based versions of PowerShell, CLI, and .NET SDK going forward.</span></span> <span data-ttu-id="864f6-106">這篇文章提供如何指標 toomigrate toohello 新 ARM 架構的方法。</span><span class="sxs-lookup"><span data-stu-id="864f6-106">This article provides pointers on how toomigrate toohello new ARM-based approach.</span></span> <span data-ttu-id="864f6-107">只要適用時，本文也將點出 hello HDInsight 的 hello ASM 和 ARM 方法之間的差異。</span><span class="sxs-lookup"><span data-stu-id="864f6-107">Wherever applicable, this article also points out hello differences between hello ASM and ARM approaches for HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="864f6-108">ASM hello 支援根據 PowerShell、 CLI，並將於中止.NET SDK **2017 年 1 月 1，**。</span><span class="sxs-lookup"><span data-stu-id="864f6-108">hello support for ASM based PowerShell, CLI, and .NET SDK will discontinue on **January 1, 2017**.</span></span>
> 
> 

## <a name="migrating-azure-cli-tooazure-resource-manager"></a><span data-ttu-id="864f6-109">移轉 Azure CLI tooAzure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="864f6-109">Migrating Azure CLI tooAzure Resource Manager</span></span>
<span data-ttu-id="864f6-110">hello Azure CLI 現在預設 tooAzure 資源管理員 (ARM) 模式中，除非您要升級從先前的安裝。在此情況下，您可能需要 toouse hello`azure config mode arm`命令 tooswitch tooARM 模式。</span><span class="sxs-lookup"><span data-stu-id="864f6-110">hello Azure CLI now defaults tooAzure Resource Manager (ARM) mode, unless you are upgrading from a previous installation; in this case, you may need toouse hello `azure config mode arm` command tooswitch tooARM mode.</span></span>

<span data-ttu-id="864f6-111">使用 ARM; 時，該 hello Azure CLI 提供使用 Azure 服務管理 (ASM) 的 HDInsight toowork 是 hello 相同的 hello 基本命令不過有些參數和參數可能會有新名稱，並有許多新的參數使用 ARM 時。</span><span class="sxs-lookup"><span data-stu-id="864f6-111">hello basic commands that hello Azure CLI provided toowork with HDInsight using Azure Service Management (ASM) are hello same when using ARM; however some parameters and switches may have new names, and there are many new parameters available when using ARM.</span></span> <span data-ttu-id="864f6-112">例如，您現在可以使用`azure hdinsight cluster create`toospecify hello Azure 虛擬網路中，應該建立的叢集或 Hive 和 Oozie 中繼存放區資訊。</span><span class="sxs-lookup"><span data-stu-id="864f6-112">For example, you can now use `azure hdinsight cluster create` toospecify hello Azure Virtual Network that a cluster should be created in, or Hive and Oozie metastore information.</span></span>

<span data-ttu-id="864f6-113">透過 Azure Resource Manager 來使用 HDInsight 的基本命令為︰</span><span class="sxs-lookup"><span data-stu-id="864f6-113">Basic commands for working with HDInsight through Azure Resource Manager are:</span></span>

* <span data-ttu-id="864f6-114">`azure hdinsight cluster create` - 建立新的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="864f6-114">`azure hdinsight cluster create` - creates a new HDInsight cluster</span></span>
* <span data-ttu-id="864f6-115">`azure hdinsight cluster delete` - 刪除現有的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="864f6-115">`azure hdinsight cluster delete` - deletes an existing HDInsight cluster</span></span>
* <span data-ttu-id="864f6-116">`azure hdinsight cluster show` - 顯示現有叢集的相關資訊</span><span class="sxs-lookup"><span data-stu-id="864f6-116">`azure hdinsight cluster show` - display information about an existing cluster</span></span>
* <span data-ttu-id="864f6-117">`azure hdinsight cluster list` - 列出適用於您 Azure 訂用帳戶的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="864f6-117">`azure hdinsight cluster list` - lists HDInsight clusters for your Azure subscription</span></span>

<span data-ttu-id="864f6-118">使用 hello`-h`切換 tooinspect hello 參數和每個命令，您可以使用的參數。</span><span class="sxs-lookup"><span data-stu-id="864f6-118">Use hello `-h` switch tooinspect hello parameters and switches available for each command.</span></span>

### <a name="new-commands"></a><span data-ttu-id="864f6-119">新的命令</span><span class="sxs-lookup"><span data-stu-id="864f6-119">New commands</span></span>
<span data-ttu-id="864f6-120">可用於 Azure Resource Manager 的新命令︰</span><span class="sxs-lookup"><span data-stu-id="864f6-120">New commands available with Azure Resource Manager are:</span></span>

* <span data-ttu-id="864f6-121">`azure hdinsight cluster resize`-以動態方式變更 hello hello 叢集中的背景工作節點數</span><span class="sxs-lookup"><span data-stu-id="864f6-121">`azure hdinsight cluster resize` - dynamically changes hello number of worker nodes in hello cluster</span></span>
* <span data-ttu-id="864f6-122">`azure hdinsight cluster enable-http-access`-啟用 HTTPs 存取 toohello 叢集 (在預設情況下)</span><span class="sxs-lookup"><span data-stu-id="864f6-122">`azure hdinsight cluster enable-http-access` - enables HTTPs access toohello cluster (on by default)</span></span>
* <span data-ttu-id="864f6-123">`azure hdinsight cluster disable-http-access`-停用 HTTPs 存取 toohello 叢集</span><span class="sxs-lookup"><span data-stu-id="864f6-123">`azure hdinsight cluster disable-http-access` - disables HTTPs access toohello cluster</span></span>
* <span data-ttu-id="864f6-124">`azure hdinsight script-action` - 在叢集上提供建立/管理指令碼動作的命令</span><span class="sxs-lookup"><span data-stu-id="864f6-124">`azure hdinsight script-action` - provides commands for creating/managing Script Actions on a cluster</span></span>
* <span data-ttu-id="864f6-125">`azure hdinsight config`-提供建立設定檔可與 hello 命令`hdinsight cluster create`命令 tooprovide 組態資訊。</span><span class="sxs-lookup"><span data-stu-id="864f6-125">`azure hdinsight config` - provides commands for creating a configuration file that can be used with hello `hdinsight cluster create` command tooprovide configuration information.</span></span>

### <a name="deprecated-commands"></a><span data-ttu-id="864f6-126">已取代的命令</span><span class="sxs-lookup"><span data-stu-id="864f6-126">Deprecated commands</span></span>
<span data-ttu-id="864f6-127">如果您使用 hello`azure hdinsight job`命令 toosubmit 作業 tooyour HDInsight 叢集，這些不是可透過 hello ARM 命令。</span><span class="sxs-lookup"><span data-stu-id="864f6-127">If you use hello `azure hdinsight job` commands toosubmit jobs tooyour HDInsight cluster, these are not available through hello ARM commands.</span></span> <span data-ttu-id="864f6-128">如果您需要 tooprogrammatically 送出工作 tooHDInsight 從指令碼，您應該改用 hello HDInsight 所提供的 REST Api。</span><span class="sxs-lookup"><span data-stu-id="864f6-128">If you need tooprogrammatically submit jobs tooHDInsight from scripts, you should instead use hello REST APIs provided by HDInsight.</span></span> <span data-ttu-id="864f6-129">如需提交使用 REST Api 作業的詳細資訊，請參閱下列文件的 hello。</span><span class="sxs-lookup"><span data-stu-id="864f6-129">For more information on submitting jobs using REST APIs, see hello following documents.</span></span>

* [<span data-ttu-id="864f6-130">使用 Curl 搭配執行 MapReduce 工作與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="864f6-130">Run MapReduce jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-mapreduce-curl.md)
* [<span data-ttu-id="864f6-131">使用 Curl 搭配執行 Hive 查詢 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="864f6-131">Run Hive queries with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-hive-curl.md)
* [<span data-ttu-id="864f6-132">使用 Curl 搭配執行 Pig 工作與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="864f6-132">Run Pig jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-pig-curl.md)

<span data-ttu-id="864f6-133">如需其他方式 toorun MapReduce，Hive，和 Pig 以互動方式，請參閱[的 HDInsight 上的 Hadoop 使用 MapReduce](hdinsight-use-mapreduce.md)，[的 HDInsight 上的 Hadoop Hive 使用](hdinsight-use-hive.md)，和[的 Hadoop 上搭配使用 PigHDInsight](hdinsight-use-pig.md)。</span><span class="sxs-lookup"><span data-stu-id="864f6-133">For information on other ways toorun MapReduce, Hive, and Pig interactively, see [Use MapReduce with Hadoop on HDInsight](hdinsight-use-mapreduce.md), [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md), and [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

### <a name="examples"></a><span data-ttu-id="864f6-134">範例</span><span class="sxs-lookup"><span data-stu-id="864f6-134">Examples</span></span>
<span data-ttu-id="864f6-135">**建立叢集**</span><span class="sxs-lookup"><span data-stu-id="864f6-135">**Creating a cluster**</span></span>

* <span data-ttu-id="864f6-136">舊的命令 (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="864f6-136">Old command (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>
* <span data-ttu-id="864f6-137">新的命令 (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="864f6-137">New command (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>

<span data-ttu-id="864f6-138">**刪除叢集**</span><span class="sxs-lookup"><span data-stu-id="864f6-138">**Deleting a cluster**</span></span>

* <span data-ttu-id="864f6-139">舊的命令 (ASM) - `azure hdinsight cluster delete myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="864f6-139">Old command (ASM) - `azure hdinsight cluster delete myhdicluster`</span></span>
* <span data-ttu-id="864f6-140">新的命令 (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="864f6-140">New command (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span></span>

<span data-ttu-id="864f6-141">**列出叢集**</span><span class="sxs-lookup"><span data-stu-id="864f6-141">**List clusters**</span></span>

* <span data-ttu-id="864f6-142">舊的命令 (ASM) - `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="864f6-142">Old command (ASM) - `azure hdinsight cluster list`</span></span>
* <span data-ttu-id="864f6-143">新的命令 (ARM) - `azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="864f6-143">New command (ARM) - `azure hdinsight cluster list`</span></span>

> [!NOTE]
> <span data-ttu-id="864f6-144">對於 hello 清單的命令，指定 hello 資源群組使用`-g`會傳回只 hello 叢集 hello 指定的資源群組中。</span><span class="sxs-lookup"><span data-stu-id="864f6-144">For hello list command, specifying hello resource group using `-g` will return only hello clusters in hello specified resource group.</span></span>
> 
> 

<span data-ttu-id="864f6-145">**顯示叢集資訊**</span><span class="sxs-lookup"><span data-stu-id="864f6-145">**Show cluster information**</span></span>

* <span data-ttu-id="864f6-146">舊的命令 (ASM) - `azure hdinsight cluster show myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="864f6-146">Old command (ASM) - `azure hdinsight cluster show myhdicluster`</span></span>
* <span data-ttu-id="864f6-147">新的命令 (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="864f6-147">New command (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span></span>

## <a name="migrating-azure-powershell-tooazure-resource-manager"></a><span data-ttu-id="864f6-148">移轉的 Azure PowerShell tooAzure 資源管理員</span><span class="sxs-lookup"><span data-stu-id="864f6-148">Migrating Azure PowerShell tooAzure Resource Manager</span></span>
<span data-ttu-id="864f6-149">hello 的一般資訊 Azure PowerShell hello Azure 資源管理員 (ARM) 模式中，請參閱[使用 Azure PowerShell 的 Azure Resource Manager](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="864f6-149">hello general information about Azure PowerShell in hello Azure Resource Manager (ARM) mode can be found at [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="864f6-150">hello Azure PowerShell ARM 指令程式可由位並行安裝以 hello ASM cmdlet。</span><span class="sxs-lookup"><span data-stu-id="864f6-150">hello Azure PowerShell ARM cmdlets can be installed side-by-side with hello ASM cmdlets.</span></span> <span data-ttu-id="864f6-151">hello cmdlet 從 hello 兩種模式可以藉由其名稱加以區別。</span><span class="sxs-lookup"><span data-stu-id="864f6-151">hello cmdlets from hello two modes can be distinguished by their names.</span></span>  <span data-ttu-id="864f6-152">hello ARM 模式有*AzureRmHDInsight*太比較 hello cmdlet 名稱中*AzureHDInsight* hello ASM 模式。</span><span class="sxs-lookup"><span data-stu-id="864f6-152">hello ARM mode has *AzureRmHDInsight* in hello cmdlet names comparing too*AzureHDInsight* in hello ASM mode.</span></span>  <span data-ttu-id="864f6-153">例如，「New-AzureRmHDInsightCluster」對比「New-AzureHDInsightCluster」。</span><span class="sxs-lookup"><span data-stu-id="864f6-153">For example, *New-AzureRmHDInsightCluster* vs. *New-AzureHDInsightCluster*.</span></span> <span data-ttu-id="864f6-154">某些參數和切換參數可能會有新的名稱，而且當使用 ARM 時，會有許多新的參數可供使用。</span><span class="sxs-lookup"><span data-stu-id="864f6-154">Parameters and switches may have news names, and there are many new parameters available when using ARM.</span></span>  <span data-ttu-id="864f6-155">例如，數個 Cmdlet 需要名為 -ResourceGroupName 的新切換參數。</span><span class="sxs-lookup"><span data-stu-id="864f6-155">For example, several cmdlets require a new switch called *-ResourceGroupName*.</span></span> 

<span data-ttu-id="864f6-156">您可以使用 hello HDInsight cmdlet 之前，您必須連接 tooyour Azure 帳戶，並建立新的資源群組：</span><span class="sxs-lookup"><span data-stu-id="864f6-156">Before you can use hello HDInsight cmdlets, you must connect tooyour Azure account, and create a new resource group:</span></span>

* <span data-ttu-id="864f6-157">Login-AzureRmAccount 或 [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx)。</span><span class="sxs-lookup"><span data-stu-id="864f6-157">Login-AzureRmAccount or [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span></span> <span data-ttu-id="864f6-158">請參閱 [使用 Azure Resource Manager 驗證服務主體](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span><span class="sxs-lookup"><span data-stu-id="864f6-158">See [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span></span>
* [<span data-ttu-id="864f6-159">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="864f6-159">New-AzureRmResourceGroup</span></span>](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a><span data-ttu-id="864f6-160">重新命名 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="864f6-160">Renamed cmdlets</span></span>
<span data-ttu-id="864f6-161">toolist hello HDInsight ASM cmdlet 在 Windows PowerShell 主控台：</span><span class="sxs-lookup"><span data-stu-id="864f6-161">toolist hello HDInsight ASM cmdlets in Windows PowerShell console:</span></span>

    help *azurermhdinsight*

<span data-ttu-id="864f6-162">hello 下表列出 hello ASM cmdlet 與 hello ARM 模式中的名稱：</span><span class="sxs-lookup"><span data-stu-id="864f6-162">hello following table lists hello ASM cmdlets and their names in hello ARM mode:</span></span>

| <span data-ttu-id="864f6-163">ASM cmdlets</span><span class="sxs-lookup"><span data-stu-id="864f6-163">ASM cmdlets</span></span> | <span data-ttu-id="864f6-164">ARM cmdlets</span><span class="sxs-lookup"><span data-stu-id="864f6-164">ARM cmdlets</span></span> |
| --- | --- |
| <span data-ttu-id="864f6-165">Add-AzureHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="864f6-165">Add-AzureHDInsightConfigValues</span></span> |[<span data-ttu-id="864f6-166">Add-AzureRmHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="864f6-166">Add-AzureRmHDInsightConfigValues</span></span>](https://msdn.microsoft.com/library/mt603530.aspx) |
| <span data-ttu-id="864f6-167">Add-AzureHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="864f6-167">Add-AzureHDInsightMetastore</span></span> |[<span data-ttu-id="864f6-168">Add-AzureRmHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="864f6-168">Add-AzureRmHDInsightMetastore</span></span>](https://msdn.microsoft.com/library/mt603670.aspx) |
| <span data-ttu-id="864f6-169">Add-AzureHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="864f6-169">Add-AzureHDInsightScriptAction</span></span> |[<span data-ttu-id="864f6-170">Add-AzureRmHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="864f6-170">Add-AzureRmHDInsightScriptAction</span></span>](https://msdn.microsoft.com/library/mt603527.aspx) |
| <span data-ttu-id="864f6-171">Add-AzureHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="864f6-171">Add-AzureHDInsightStorage</span></span> |[<span data-ttu-id="864f6-172">Add-AzureRmHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="864f6-172">Add-AzureRmHDInsightStorage</span></span>](https://msdn.microsoft.com/library/mt619445.aspx) |
| <span data-ttu-id="864f6-173">Get-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="864f6-173">Get-AzureHDInsightCluster</span></span> |[<span data-ttu-id="864f6-174">Get AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="864f6-174">Get-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619371.aspx) |
| <span data-ttu-id="864f6-175">Get-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="864f6-175">Get-AzureHDInsightJob</span></span> |[<span data-ttu-id="864f6-176">Get-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="864f6-176">Get-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603590.aspx) |
| <span data-ttu-id="864f6-177">Get-AzureHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="864f6-177">Get-AzureHDInsightJobOutput</span></span> |[<span data-ttu-id="864f6-178">Get-AzureRmHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="864f6-178">Get-AzureRmHDInsightJobOutput</span></span>](https://msdn.microsoft.com/library/mt603793.aspx) |
| <span data-ttu-id="864f6-179">Get-AzureHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="864f6-179">Get-AzureHDInsightProperties</span></span> |[<span data-ttu-id="864f6-180">Get-AzureRmHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="864f6-180">Get-AzureRmHDInsightProperties</span></span>](https://msdn.microsoft.com/library/mt603546.aspx) |
| <span data-ttu-id="864f6-181">Grant-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="864f6-181">Grant-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="864f6-182">Grant-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="864f6-182">Grant-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619407.aspx) |
| <span data-ttu-id="864f6-183">Grant-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="864f6-183">Grant-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="864f6-184">Grant-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="864f6-184">Grant-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603717.aspx) |
| <span data-ttu-id="864f6-185">Invoke-AzureHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="864f6-185">Invoke-AzureHDInsightHiveJob</span></span> |[<span data-ttu-id="864f6-186">Invoke-AzureRmHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="864f6-186">Invoke-AzureRmHDInsightHiveJob</span></span>](https://msdn.microsoft.com/library/mt603593.aspx) |
| <span data-ttu-id="864f6-187">New-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="864f6-187">New-AzureHDInsightCluster</span></span> |[<span data-ttu-id="864f6-188">New-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="864f6-188">New-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619331.aspx) |
| <span data-ttu-id="864f6-189">New-AzureHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="864f6-189">New-AzureHDInsightClusterConfig</span></span> |[<span data-ttu-id="864f6-190">New-AzureRmHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="864f6-190">New-AzureRmHDInsightClusterConfig</span></span>](https://msdn.microsoft.com/library/mt603700.aspx) |
| <span data-ttu-id="864f6-191">New-AzureHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="864f6-191">New-AzureHDInsightHiveJobDefinition</span></span> |[<span data-ttu-id="864f6-192">New-AzureRmHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="864f6-192">New-AzureRmHDInsightHiveJobDefinition</span></span>](https://msdn.microsoft.com/library/mt619448.aspx) |
| <span data-ttu-id="864f6-193">New-AzureHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="864f6-193">New-AzureHDInsightMapReduceJobDefinition</span></span> |[<span data-ttu-id="864f6-194">New-AzureRmHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="864f6-194">New-AzureRmHDInsightMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="864f6-195">New-AzureHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="864f6-195">New-AzureHDInsightPigJobDefinition</span></span> |[<span data-ttu-id="864f6-196">New-AzureRmHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="864f6-196">New-AzureRmHDInsightPigJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603671.aspx) |
| <span data-ttu-id="864f6-197">New-AzureHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="864f6-197">New-AzureHDInsightSqoopJobDefinition</span></span> |[<span data-ttu-id="864f6-198">New-AzureRmHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="864f6-198">New-AzureRmHDInsightSqoopJobDefinition</span></span>](https://msdn.microsoft.com/library/mt608551.aspx) |
| <span data-ttu-id="864f6-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="864f6-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span></span> |[<span data-ttu-id="864f6-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="864f6-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="864f6-201">Remove-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="864f6-201">Remove-AzureHDInsightCluster</span></span> |[<span data-ttu-id="864f6-202">Remove-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="864f6-202">Remove-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619431.aspx) |
| <span data-ttu-id="864f6-203">Revoke-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="864f6-203">Revoke-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="864f6-204">Revoke-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="864f6-204">Revoke-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619375.aspx) |
| <span data-ttu-id="864f6-205">Revoke-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="864f6-205">Revoke-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="864f6-206">Revoke-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="864f6-206">Revoke-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603523.aspx) |
| <span data-ttu-id="864f6-207">Set-AzureHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="864f6-207">Set-AzureHDInsightClusterSize</span></span> |[<span data-ttu-id="864f6-208">Set-AzureRmHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="864f6-208">Set-AzureRmHDInsightClusterSize</span></span>](https://msdn.microsoft.com/library/mt603513.aspx) |
| <span data-ttu-id="864f6-209">Set-AzureHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="864f6-209">Set-AzureHDInsightDefaultStorage</span></span> |[<span data-ttu-id="864f6-210">Set-AzureRmHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="864f6-210">Set-AzureRmHDInsightDefaultStorage</span></span>](https://msdn.microsoft.com/library/mt603486.aspx) |
| <span data-ttu-id="864f6-211">Start-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="864f6-211">Start-AzureHDInsightJob</span></span> |[<span data-ttu-id="864f6-212">Start-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="864f6-212">Start-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603798.aspx) |
| <span data-ttu-id="864f6-213">Stop-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="864f6-213">Stop-AzureHDInsightJob</span></span> |[<span data-ttu-id="864f6-214">Stop-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="864f6-214">Stop-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt619424.aspx) |
| <span data-ttu-id="864f6-215">Use-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="864f6-215">Use-AzureHDInsightCluster</span></span> |[<span data-ttu-id="864f6-216">Use-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="864f6-216">Use-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619442.aspx) |
| <span data-ttu-id="864f6-217">Wait-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="864f6-217">Wait-AzureHDInsightJob</span></span> |[<span data-ttu-id="864f6-218">Wait-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="864f6-218">Wait-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a><span data-ttu-id="864f6-219">新的 Cmdlet</span><span class="sxs-lookup"><span data-stu-id="864f6-219">New cmdlets</span></span>
<span data-ttu-id="864f6-220">hello 如下 hello hello ARM 模式中才有的新 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="864f6-220">hello following are hello new cmdlets that are only available in hello ARM mode.</span></span> 

<span data-ttu-id="864f6-221">**指令碼動作相關的 Cmdlet：**</span><span class="sxs-lookup"><span data-stu-id="864f6-221">**Script action related cmdlets:**</span></span>

* <span data-ttu-id="864f6-222">**Get AzureRmHDInsightPersistedScriptAction**： 取得 hello 保存叢集的指令碼動作，依時間順序列出這些或取得指定的持續性指令碼動作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="864f6-222">**Get-AzureRmHDInsightPersistedScriptAction**: Gets hello persisted script actions for a cluster and lists them in chronological order, or gets details for a specified persisted script action.</span></span> 
* <span data-ttu-id="864f6-223">**Get AzureRmHDInsightScriptActionHistory**： 取得 hello 指令碼動作記錄的叢集和清單以反向的依時間先後順序，或取得先前執行的指令碼動作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="864f6-223">**Get-AzureRmHDInsightScriptActionHistory**: Gets hello script action history for a cluster and lists it in reverse chronological order, or gets details of a previously executed script action.</span></span> 
* <span data-ttu-id="864f6-224">**Remove-AzureRmHDInsightPersistedScriptAction**︰自 HDInsight 叢集移除持續性指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="864f6-224">**Remove-AzureRmHDInsightPersistedScriptAction**: Removes a persisted script action from an HDInsight cluster.</span></span>
* <span data-ttu-id="864f6-225">**設定 AzureRmHDInsightPersistedScriptAction**： 設定先前執行的指令碼動作 toobe 保存的指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="864f6-225">**Set-AzureRmHDInsightPersistedScriptAction**: Sets a previously executed script action toobe a persisted script action.</span></span>
* <span data-ttu-id="864f6-226">**提交 AzureRmHDInsightScriptAction**： 提交新的指令碼動作 tooan Azure HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="864f6-226">**Submit-AzureRmHDInsightScriptAction**: Submits a new script action tooan Azure HDInsight cluster.</span></span> 

<span data-ttu-id="864f6-227">如需關於其他使用方式的詳細資訊，請參閱 [使用指令碼動作自訂以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="864f6-227">For additional usage information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="864f6-228">**叢集身分識別相關的 Cmdlet：**</span><span class="sxs-lookup"><span data-stu-id="864f6-228">**Clsuter identity related cmdlets:**</span></span>

* <span data-ttu-id="864f6-229">**新增 AzureRmHDInsightClusterIdentity**： 新增叢集識別 tooa 叢集組態物件，以便 hello HDInsight 叢集可以存取 Azure 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="864f6-229">**Add-AzureRmHDInsightClusterIdentity**: Adds a cluster identity tooa cluster configuration object so that hello HDInsight cluster can access Azure Data Lake Stores.</span></span> <span data-ttu-id="864f6-230">請參閱 [使用 Azure PowerShell 建立具 Data Lake Store 的 HDInsight 叢集](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="864f6-230">See [Create an HDInsight cluster with Data Lake Store using Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

### <a name="examples"></a><span data-ttu-id="864f6-231">範例</span><span class="sxs-lookup"><span data-stu-id="864f6-231">Examples</span></span>
<span data-ttu-id="864f6-232">**建立叢集**</span><span class="sxs-lookup"><span data-stu-id="864f6-232">**Create cluster**</span></span>

<span data-ttu-id="864f6-233">舊的命令 (ASM)：</span><span class="sxs-lookup"><span data-stu-id="864f6-233">Old command (ASM):</span></span> 

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

<span data-ttu-id="864f6-234">新的命令 (ARM)：</span><span class="sxs-lookup"><span data-stu-id="864f6-234">New command (ARM):</span></span>

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


<span data-ttu-id="864f6-235">**刪除叢集**</span><span class="sxs-lookup"><span data-stu-id="864f6-235">**Delete cluster**</span></span>

<span data-ttu-id="864f6-236">舊的命令 (ASM)：</span><span class="sxs-lookup"><span data-stu-id="864f6-236">Old command (ASM):</span></span>

    Remove-AzureHDInsightCluster -name $clusterName 

<span data-ttu-id="864f6-237">新的命令 (ARM)：</span><span class="sxs-lookup"><span data-stu-id="864f6-237">New command (ARM):</span></span>

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

<span data-ttu-id="864f6-238">**列出叢集**</span><span class="sxs-lookup"><span data-stu-id="864f6-238">**List cluster**</span></span>

<span data-ttu-id="864f6-239">舊的命令 (ASM)：</span><span class="sxs-lookup"><span data-stu-id="864f6-239">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster

<span data-ttu-id="864f6-240">新的命令 (ARM)：</span><span class="sxs-lookup"><span data-stu-id="864f6-240">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster 

<span data-ttu-id="864f6-241">**顯示叢集**</span><span class="sxs-lookup"><span data-stu-id="864f6-241">**Show cluster**</span></span>

<span data-ttu-id="864f6-242">舊的命令 (ASM)：</span><span class="sxs-lookup"><span data-stu-id="864f6-242">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster -Name $clusterName

<span data-ttu-id="864f6-243">新的命令 (ARM)：</span><span class="sxs-lookup"><span data-stu-id="864f6-243">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a><span data-ttu-id="864f6-244">其他範例</span><span class="sxs-lookup"><span data-stu-id="864f6-244">Other samples</span></span>
* [<span data-ttu-id="864f6-245">建立 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="864f6-245">Create HDInsight clusters</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="864f6-246">提交 Hive 工作</span><span class="sxs-lookup"><span data-stu-id="864f6-246">Submit Hive jobs</span></span>](hdinsight-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="864f6-247">提交 Pig 工作</span><span class="sxs-lookup"><span data-stu-id="864f6-247">Submit Pig jobs</span></span>](hdinsight-hadoop-use-pig-powershell.md)
* [<span data-ttu-id="864f6-248">提交 Sqoop 工作</span><span class="sxs-lookup"><span data-stu-id="864f6-248">Submit Sqoop jobs</span></span>](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-toohello-arm-based-hdinsight-net-sdk"></a><span data-ttu-id="864f6-249">移轉 toohello arm HDInsight.NET SDK</span><span class="sxs-lookup"><span data-stu-id="864f6-249">Migrating toohello ARM-based HDInsight .NET SDK</span></span>
<span data-ttu-id="864f6-250">hello Azure 服務管理基礎[(ASM) HDInsight.NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx)現在已被取代。</span><span class="sxs-lookup"><span data-stu-id="864f6-250">hello Azure Service Management-based [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is now deprecated.</span></span> <span data-ttu-id="864f6-251">您會鼓勵的 toouse hello Azure 資源管理基礎[(ARM) HDInsight.NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx)。</span><span class="sxs-lookup"><span data-stu-id="864f6-251">You are encouraged toouse hello Azure Resource Management-based [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span></span> <span data-ttu-id="864f6-252">hello 下列 ASM 為基礎的 HDInsight 套件已被取代。</span><span class="sxs-lookup"><span data-stu-id="864f6-252">hello following ASM-based HDInsight packages are being deprecated.</span></span>

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

<span data-ttu-id="864f6-253">本節提供指標 toomore 資訊如何 tooperform 特定工作使用 hello arm SDK。</span><span class="sxs-lookup"><span data-stu-id="864f6-253">This section provides pointers toomore information on how tooperform certain tasks using hello ARM-based SDK.</span></span>

| <span data-ttu-id="864f6-254">如何...使用 hello arm HDInsight SDK</span><span class="sxs-lookup"><span data-stu-id="864f6-254">How to... using hello ARM-based HDInsight SDK</span></span> | <span data-ttu-id="864f6-255">連結</span><span class="sxs-lookup"><span data-stu-id="864f6-255">Links</span></span> |
| --- | --- |
| <span data-ttu-id="864f6-256">使用 .NET SDK 建立 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="864f6-256">Create HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="864f6-257">請參閱 [使用.NET SDK 來建立 HDInsight 叢集](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="864f6-257">See [Create HDInsight clusters using .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="864f6-258">搭配使用指令碼動作與 .NET SDK 來自訂叢集</span><span class="sxs-lookup"><span data-stu-id="864f6-258">Customize a cluster using Script Action with .NET SDK</span></span> |<span data-ttu-id="864f6-259">請參閱 [使用指令碼動作來自訂 HDInsight Linux 叢集](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span><span class="sxs-lookup"><span data-stu-id="864f6-259">See [Customize HDInsight Linux clusters using Script Action](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span></span> |
| <span data-ttu-id="864f6-260">搭配使用 Azure Active Directory 與 .NET SDK，以互動方式驗證應用程式</span><span class="sxs-lookup"><span data-stu-id="864f6-260">Authenticate applications interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="864f6-261">請參閱 [使用 .NET SDK 執行 Hive 查詢](hdinsight-hadoop-use-hive-dotnet-sdk.md)。</span><span class="sxs-lookup"><span data-stu-id="864f6-261">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span> <span data-ttu-id="864f6-262">本文章中的 hello 程式碼片段會使用 hello 互動式驗證方法。</span><span class="sxs-lookup"><span data-stu-id="864f6-262">hello code snippet in this article uses hello interactive authentication approach.</span></span> |
| <span data-ttu-id="864f6-263">搭配使用 Azure Active Directory 與 .NET SDK，以非互動方式驗證應用程式</span><span class="sxs-lookup"><span data-stu-id="864f6-263">Authenticate applications non-interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="864f6-264">請參閱 [建立 HDInsight 的非互動式應用程式](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span><span class="sxs-lookup"><span data-stu-id="864f6-264">See [Create non-interactive applications for HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span></span> |
| <span data-ttu-id="864f6-265">使用 .NET SDK 提交 Hive 作業</span><span class="sxs-lookup"><span data-stu-id="864f6-265">Submit a Hive job using .NET SDK</span></span> |<span data-ttu-id="864f6-266">請參閱 [提交 Hive 工作](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="864f6-266">See [Submit Hive jobs](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="864f6-267">使用 .NET SDK 提交 Pig 作業</span><span class="sxs-lookup"><span data-stu-id="864f6-267">Submit a Pig job using .NET SDK</span></span> |<span data-ttu-id="864f6-268">請參閱 [提交 Pig 工作](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="864f6-268">See [Submit Pig jobs](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="864f6-269">使用 .NET SDK 提交 Sqoop 作業</span><span class="sxs-lookup"><span data-stu-id="864f6-269">Submit a Sqoop job using .NET SDK</span></span> |<span data-ttu-id="864f6-270">請參閱 [提交 Sqoop 工作](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="864f6-270">See [Submit Sqoop jobs](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="864f6-271">使用 .NET SDK 列出 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="864f6-271">List HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="864f6-272">請參閱 [列出 HDInsight 叢集](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span><span class="sxs-lookup"><span data-stu-id="864f6-272">See [List HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span></span> |
| <span data-ttu-id="864f6-273">使用.NET SDK 調整 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="864f6-273">Scale HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="864f6-274">請參閱 [調整 HDInsight 叢集](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span><span class="sxs-lookup"><span data-stu-id="864f6-274">See [Scale HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span></span> |
| <span data-ttu-id="864f6-275">使用.NET SDK 授與/撤銷存取 tooHDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="864f6-275">Grant/revoke access tooHDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="864f6-276">請參閱[授與/撤銷存取 tooHDInsight 叢集](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span><span class="sxs-lookup"><span data-stu-id="864f6-276">See [Grant/revoke access tooHDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span></span> |
| <span data-ttu-id="864f6-277">使用 .NET SDK 更新 HDInsight 叢集的 HTTP 使用者認證</span><span class="sxs-lookup"><span data-stu-id="864f6-277">Update HTTP user credentials for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="864f6-278">請參閱 [「更新 HDInsight 叢集的 HTTP 使用者認證」](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span><span class="sxs-lookup"><span data-stu-id="864f6-278">See [Update HTTP user credentials for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span></span> |
| <span data-ttu-id="864f6-279">使用.NET SDK 的 HDInsight 叢集的尋找 hello 預設儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="864f6-279">Find hello default storage account for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="864f6-280">請參閱[尋找 HDInsight 叢集的 hello 預設儲存體帳戶](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span><span class="sxs-lookup"><span data-stu-id="864f6-280">See [Find hello default storage account for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span></span> |
| <span data-ttu-id="864f6-281">使用 .NET SDK 刪除 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="864f6-281">Delete HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="864f6-282">請參閱 [「刪除 HDInsight 叢集」](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="864f6-282">See [Delete HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span></span> |

### <a name="examples"></a><span data-ttu-id="864f6-283">範例</span><span class="sxs-lookup"><span data-stu-id="864f6-283">Examples</span></span>
<span data-ttu-id="864f6-284">以下是一些範例上執行作業的方式都使用 hello arm SDK hello ASM 為基礎的 SDK 和 hello 對等的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="864f6-284">Following are some examples on how an operation is performed using hello ASM-based SDK and hello equivalent code snippet for hello ARM-based SDK.</span></span>

<span data-ttu-id="864f6-285">**建立叢集 CRUD 用戶端**</span><span class="sxs-lookup"><span data-stu-id="864f6-285">**Creating a cluster CRUD client**</span></span>

* <span data-ttu-id="864f6-286">舊的命令 (ASM)</span><span class="sxs-lookup"><span data-stu-id="864f6-286">Old command (ASM)</span></span>
  
        //Certificate auth
        //This logs hello application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* <span data-ttu-id="864f6-287">新的命令 (ARM) (服務主體的授權)</span><span class="sxs-lookup"><span data-stu-id="864f6-287">New command (ARM) (Service principal authorization)</span></span>
  
        //Service principal auth
        //This will log hello application in as itself, rather than on behalf of a specific user.
        //For details, including how tooset up hello application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* <span data-ttu-id="864f6-288">新的命令 (ARM) (使用者的授權)</span><span class="sxs-lookup"><span data-stu-id="864f6-288">New command (ARM) (User authorization)</span></span>
  
        //User auth
        //This will log hello application in on behalf of hello user.
        //hello end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

<span data-ttu-id="864f6-289">**建立叢集**</span><span class="sxs-lookup"><span data-stu-id="864f6-289">**Creating a cluster**</span></span>

* <span data-ttu-id="864f6-290">舊的命令 (ASM)</span><span class="sxs-lookup"><span data-stu-id="864f6-290">Old command (ASM)</span></span>
  
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
* <span data-ttu-id="864f6-291">新的命令 (ARM)</span><span class="sxs-lookup"><span data-stu-id="864f6-291">New command (ARM)</span></span>
  
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

<span data-ttu-id="864f6-292">**啟用 HTTP 存取**</span><span class="sxs-lookup"><span data-stu-id="864f6-292">**Enabling HTTP access**</span></span>

* <span data-ttu-id="864f6-293">舊的命令 (ASM)</span><span class="sxs-lookup"><span data-stu-id="864f6-293">Old command (ASM)</span></span>
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* <span data-ttu-id="864f6-294">新的命令 (ARM)</span><span class="sxs-lookup"><span data-stu-id="864f6-294">New command (ARM)</span></span>
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

<span data-ttu-id="864f6-295">**刪除叢集**</span><span class="sxs-lookup"><span data-stu-id="864f6-295">**Deleting a cluster**</span></span>

* <span data-ttu-id="864f6-296">舊的命令 (ASM)</span><span class="sxs-lookup"><span data-stu-id="864f6-296">Old command (ASM)</span></span>
  
        client.DeleteCluster(dnsName);
* <span data-ttu-id="864f6-297">新的命令 (ARM)</span><span class="sxs-lookup"><span data-stu-id="864f6-297">New command (ARM)</span></span>
  
        client.Clusters.Delete(resourceGroup, dnsname);

