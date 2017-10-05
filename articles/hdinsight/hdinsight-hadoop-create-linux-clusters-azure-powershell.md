---
title: "使用 PowerShell 建立 Hadoop 叢集 - Azure HDInsight | Microsoft Docs"
description: "了解如何在 Linux 上使用 Azure PowerShell 為 HDInsight 建立 Hadoop、HBase、Storm 或 Spark 叢集。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4208deca-d64a-45e1-8948-2673d5d7678c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ca75974e6ec4f60739137d4cb5458bbfd735de3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a><span data-ttu-id="e8821-103">使用 Azure PowerShell 在 HDInsight 中建立以 Linux 為基礎的叢集</span><span class="sxs-lookup"><span data-stu-id="e8821-103">Create Linux-based clusters in HDInsight using Azure PowerShell</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="e8821-104">Azure PowerShell 是功能強大的指令碼環境，可讓您在 Microsoft Azure 中控制和自動化工作量的部署與管理。</span><span class="sxs-lookup"><span data-stu-id="e8821-104">Azure PowerShell is a powerful scripting environment that you can use to control and automate the deployment and management of your workloads in Microsoft Azure.</span></span> <span data-ttu-id="e8821-105">本文件提供如何使用 Azure PowerShell 建立以 Linux 為基礎之 HDInsight 叢集的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e8821-105">This document provides information about how to create a Linux-based HDInsight cluster by using Azure PowerShell.</span></span> <span data-ttu-id="e8821-106">其中也包含一個範例指令碼。</span><span class="sxs-lookup"><span data-stu-id="e8821-106">It also includes an example script.</span></span>

> [!NOTE]
> <span data-ttu-id="e8821-107">Azure PowerShell 僅適用於 Windows 用戶端。</span><span class="sxs-lookup"><span data-stu-id="e8821-107">Azure PowerShell is only available on Windows clients.</span></span> <span data-ttu-id="e8821-108">如果您使用 Linux、Unix 或 Mac OS X 用戶端，請參閱 [使用 Azure CLI 建立以 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-create-linux-clusters-azure-cli.md) ，以取得使用 Azure CLI 建立叢集的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e8821-108">If you are using a Linux, Unix, or Mac OS X client, see [Create a Linux-based HDInsight cluster using Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) for information about using the Azure CLI to create a cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e8821-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="e8821-109">Prerequisites</span></span>
<span data-ttu-id="e8821-110">開始進行此程序之前，您必須先具備下列項目：</span><span class="sxs-lookup"><span data-stu-id="e8821-110">You must have the following before starting this procedure:</span></span>

* <span data-ttu-id="e8821-111">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e8821-111">An Azure subscription.</span></span> <span data-ttu-id="e8821-112">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="e8821-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* [<span data-ttu-id="e8821-113">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8821-113">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > <span data-ttu-id="e8821-114">使用 Azure Service Manager 管理 HDInsight 資源的 Azure PowerShell 支援已**被取代**，並已在 2017 年 1 月 1 日移除。</span><span class="sxs-lookup"><span data-stu-id="e8821-114">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="e8821-115">本文件中的步驟會使用可與 Azure Resource Manager 搭配使用的新 HDInsight Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="e8821-115">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="e8821-116">請遵循[安裝 Azure PowerShell (英文)](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) 中的步驟來安裝最新版的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="e8821-116">Please follow the steps in [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="e8821-117">如果您需要修改指令碼才能使用適用於 Azure Resource Manager 的新 Cmdlet，請參閱 [移轉至以 Azure Resource Manager 為基礎的開發工具 (適用於 HDInsight 叢集)](hdinsight-hadoop-development-using-azure-resource-manager.md) ，以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="e8821-117">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

## <a name="create-cluster"></a><span data-ttu-id="e8821-118">建立叢集</span><span class="sxs-lookup"><span data-stu-id="e8821-118">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="e8821-119">若要使用 Azure PowerShell 建立 HDInsight 叢集，您必須完成下列程序：</span><span class="sxs-lookup"><span data-stu-id="e8821-119">To create an HDInsight cluster by using Azure PowerShell, you must complete the following procedures:</span></span>

* <span data-ttu-id="e8821-120">建立 Azure 資源群組</span><span class="sxs-lookup"><span data-stu-id="e8821-120">Create an Azure resource group</span></span>
* <span data-ttu-id="e8821-121">建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="e8821-121">Create an Azure Storage account</span></span>
* <span data-ttu-id="e8821-122">建立 Azure Blob 容器</span><span class="sxs-lookup"><span data-stu-id="e8821-122">Create an Azure Blob container</span></span>
* <span data-ttu-id="e8821-123">建立 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="e8821-123">Create an HDInsight cluster</span></span>

<span data-ttu-id="e8821-124">下列指令碼示範如何建立新叢集：</span><span class="sxs-lookup"><span data-stu-id="e8821-124">The following script demonstrates how to create a new cluster:</span></span>

<span data-ttu-id="e8821-125">[!code-powershell[主要](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]</span><span class="sxs-lookup"><span data-stu-id="e8821-125">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]</span></span>

<span data-ttu-id="e8821-126">您為叢集登入指定的值會用來建立叢集的 Hadoop 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="e8821-126">The values you specify for the cluster login are used to create the Hadoop user account for the cluster.</span></span> <span data-ttu-id="e8821-127">請使用此帳戶來連線叢集上裝載的服務，像是 web UI 或 REST API。</span><span class="sxs-lookup"><span data-stu-id="e8821-127">Use this account to connect to services hosted on the cluster such as web UIs or REST APIs.</span></span>

<span data-ttu-id="e8821-128">您為 SSH 使用者指定的值會用來建立叢集的 SSH 使用者。</span><span class="sxs-lookup"><span data-stu-id="e8821-128">The values you specify for the SSH user are used to create the SSH user for the cluster.</span></span> <span data-ttu-id="e8821-129">使用此帳戶在叢集上啟動遠端 SSH 工作階段並執行工作。</span><span class="sxs-lookup"><span data-stu-id="e8821-129">Use this account to start a remote SSH session on the cluster and run jobs.</span></span> <span data-ttu-id="e8821-130">如需詳細資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md) 文件。</span><span class="sxs-lookup"><span data-stu-id="e8821-130">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e8821-131">如果您規劃使用 32 個以上的背景工作角色節點 (在建立叢集時或在建立後調整叢集時)，則您也必須指定具有至少 8 個核心和 14 GB RAM 的前端節點大小。</span><span class="sxs-lookup"><span data-stu-id="e8821-131">If you plan to use more than 32 worker nodes (either at cluster creation or by scaling the cluster after creation), you must also specify a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
> <span data-ttu-id="e8821-132">如需節點大小和相關成本的詳細資訊，請參閱 [HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="e8821-132">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="e8821-133">建立叢集可能需要花費 20 分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="e8821-133">It can take up to 20 minutes to create a cluster.</span></span>

## <a name="create-cluster-configuration-object"></a><span data-ttu-id="e8821-134">建立叢集：設定物件</span><span class="sxs-lookup"><span data-stu-id="e8821-134">Create cluster: Configuration object</span></span>

<span data-ttu-id="e8821-135">您也可以使用 `New-AzureRmHDInsightClusterConfig` Cmdlet 建立 HDInsight 設定物件。</span><span class="sxs-lookup"><span data-stu-id="e8821-135">You can also create an HDInsight configuration object using `New-AzureRmHDInsightClusterConfig` cmdlet.</span></span> <span data-ttu-id="e8821-136">然後，您可以修改此設定物件來啟用叢集的其他設定選項。</span><span class="sxs-lookup"><span data-stu-id="e8821-136">You can then modify this configuration object to enable additional configuration options for your cluster.</span></span> <span data-ttu-id="e8821-137">最後，請使用 `New-AzureRmHDInsightCluster` Cmdlet 的 `-Config` 參數以使用設定。</span><span class="sxs-lookup"><span data-stu-id="e8821-137">Finally, use the `-Config` parameter of the `New-AzureRmHDInsightCluster` cmdlet to use the configuration.</span></span>

<span data-ttu-id="e8821-138">下列指令碼會建立可在 HDInsight 叢集類型上設定 R 伺服器的設定物件。</span><span class="sxs-lookup"><span data-stu-id="e8821-138">The following script creates a configuration object to configure an R Server on HDInsight cluster type.</span></span> <span data-ttu-id="e8821-139">此設定可啟用邊緣節點、RStudio 和其他儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e8821-139">The configuration enables an edge node, RStudio, and an additional storage account.</span></span>

<span data-ttu-id="e8821-140">[!code-powershell[主要](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]</span><span class="sxs-lookup"><span data-stu-id="e8821-140">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]</span></span>

> [!WARNING]
> <span data-ttu-id="e8821-141">不支援在與 HDInsight 叢集不同的位置中使用儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e8821-141">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span> <span data-ttu-id="e8821-142">使用此範例時，請在與伺服器相同的位置建立其他儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e8821-142">When using this example, create the additional storage account in the same location as the server.</span></span>

## <a name="customize-clusters"></a><span data-ttu-id="e8821-143">自訂叢集</span><span class="sxs-lookup"><span data-stu-id="e8821-143">Customize clusters</span></span>

* <span data-ttu-id="e8821-144">請參閱 [使用 Bootstrap 自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="e8821-144">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span></span>
* <span data-ttu-id="e8821-145">請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="e8821-145">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="e8821-146">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="e8821-146">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="e8821-147">疑難排解</span><span class="sxs-lookup"><span data-stu-id="e8821-147">Troubleshoot</span></span>

<span data-ttu-id="e8821-148">如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="e8821-148">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e8821-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e8821-149">Next steps</span></span>

<span data-ttu-id="e8821-150">既然您已成功建立 HDInsight 叢集，請使用下列資源來了解如何使用您的叢集。</span><span class="sxs-lookup"><span data-stu-id="e8821-150">Now that you have successfully created an HDInsight cluster, use the following resources to learn how to work with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="e8821-151">Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="e8821-151">Hadoop clusters</span></span>

* [<span data-ttu-id="e8821-152">〈搭配 HDInsight 使用 Hivet〉</span><span class="sxs-lookup"><span data-stu-id="e8821-152">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="e8821-153">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="e8821-153">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="e8821-154">〈搭配 HDInsight 使用 MapReduce〉</span><span class="sxs-lookup"><span data-stu-id="e8821-154">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="e8821-155">HBase 叢集</span><span class="sxs-lookup"><span data-stu-id="e8821-155">HBase clusters</span></span>

* [<span data-ttu-id="e8821-156">開始在 HDInsight 上使用 HBase</span><span class="sxs-lookup"><span data-stu-id="e8821-156">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="e8821-157">在 HDInsight 上開發適用於 HBase 的 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="e8821-157">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="e8821-158">Storm 叢集</span><span class="sxs-lookup"><span data-stu-id="e8821-158">Storm clusters</span></span>

* [<span data-ttu-id="e8821-159">在 HDInsight 上開發適用於 Storm 的 Java 拓撲</span><span class="sxs-lookup"><span data-stu-id="e8821-159">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="e8821-160">在 HDInsight 上的 Storm 中使用 Python 元件</span><span class="sxs-lookup"><span data-stu-id="e8821-160">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="e8821-161">在 HDInsight 上使用 Storm 部署和監視拓撲</span><span class="sxs-lookup"><span data-stu-id="e8821-161">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="e8821-162">Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="e8821-162">Spark clusters</span></span>

* [<span data-ttu-id="e8821-163">使用 Scala 來建立獨立的應用程式</span><span class="sxs-lookup"><span data-stu-id="e8821-163">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="e8821-164">利用 Livy 在 Spark 叢集上遠端執行工作</span><span class="sxs-lookup"><span data-stu-id="e8821-164">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="e8821-165">Spark 和 BI：搭配 BI 工具來使用 HDInsight 中的 Spark 以執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="e8821-165">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="e8821-166">Spark 和機器學習：使用 HDInsight 中的 Spark 來預測食物檢查結果</span><span class="sxs-lookup"><span data-stu-id="e8821-166">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="e8821-167">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="e8821-167">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

