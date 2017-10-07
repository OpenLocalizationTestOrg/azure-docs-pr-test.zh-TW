---
title: "使用 PowerShell 的 Azure HDInsight aaaCreate Hadoop 叢集 |Microsoft 文件"
description: "了解如何 toocreate Hadoop、 HBase、 風暴或 Spark 叢集，在 Linux 上的 HDInsight 使用 Azure PowerShell。"
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
ms.openlocfilehash: 53afe4702f6b61a0720ceda48a4a34d7fa8797d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a><span data-ttu-id="de07b-103">使用 Azure PowerShell 在 HDInsight 中建立以 Linux 為基礎的叢集</span><span class="sxs-lookup"><span data-stu-id="de07b-103">Create Linux-based clusters in HDInsight using Azure PowerShell</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="de07b-104">Azure PowerShell 是一種強大的指令碼環境，您可以使用 toocontrol 並自動化 hello 部署和管理您在 Microsoft Azure 中的工作負載。</span><span class="sxs-lookup"><span data-stu-id="de07b-104">Azure PowerShell is a powerful scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Microsoft Azure.</span></span> <span data-ttu-id="de07b-105">本文件提供如何使用 Azure PowerShell toocreate 以 Linux 為基礎的 HDInsight 叢集的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="de07b-105">This document provides information about how toocreate a Linux-based HDInsight cluster by using Azure PowerShell.</span></span> <span data-ttu-id="de07b-106">其中也包含一個範例指令碼。</span><span class="sxs-lookup"><span data-stu-id="de07b-106">It also includes an example script.</span></span>

> [!NOTE]
> <span data-ttu-id="de07b-107">Azure PowerShell 僅適用於 Windows 用戶端。</span><span class="sxs-lookup"><span data-stu-id="de07b-107">Azure PowerShell is only available on Windows clients.</span></span> <span data-ttu-id="de07b-108">如果您使用 Linux、 Unix 或 Mac OS X 用戶端，請參閱[建立以 Linux 為基礎的 HDInsight 叢集使用 Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md)使用 hello Azure CLI toocreate 叢集相關資訊。</span><span class="sxs-lookup"><span data-stu-id="de07b-108">If you are using a Linux, Unix, or Mac OS X client, see [Create a Linux-based HDInsight cluster using Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) for information about using hello Azure CLI toocreate a cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de07b-109">必要條件</span><span class="sxs-lookup"><span data-stu-id="de07b-109">Prerequisites</span></span>
<span data-ttu-id="de07b-110">您必須在開始此程序之前的 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="de07b-110">You must have hello following before starting this procedure:</span></span>

* <span data-ttu-id="de07b-111">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="de07b-111">An Azure subscription.</span></span> <span data-ttu-id="de07b-112">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="de07b-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* [<span data-ttu-id="de07b-113">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="de07b-113">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > <span data-ttu-id="de07b-114">使用 Azure Service Manager 管理 HDInsight 資源的 Azure PowerShell 支援已**被取代**，並已在 2017 年 1 月 1 日移除。</span><span class="sxs-lookup"><span data-stu-id="de07b-114">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="de07b-115">此文件使用 hello 新 HDInsight 的 cmdlet 可與 Azure 資源管理員中的步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="de07b-115">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="de07b-116">請依照中的 hello 步驟[安裝 AzurePowershell</](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello 最新版的 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="de07b-116">Please follow hello steps in [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="de07b-117">如果您有指令碼的需要 toobe 修改 toouse hello 新的 cmdlet 可與 Azure 資源管理員，請參閱[移轉 tooAzure 資源管理員為基礎的開發工具的 HDInsight 叢集](hdinsight-hadoop-development-using-azure-resource-manager.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="de07b-117">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

## <a name="create-cluster"></a><span data-ttu-id="de07b-118">建立叢集</span><span class="sxs-lookup"><span data-stu-id="de07b-118">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="de07b-119">toocreate 使用 Azure PowerShell HDInsight 叢集，您必須完成下列程序的 hello:</span><span class="sxs-lookup"><span data-stu-id="de07b-119">toocreate an HDInsight cluster by using Azure PowerShell, you must complete hello following procedures:</span></span>

* <span data-ttu-id="de07b-120">建立 Azure 資源群組</span><span class="sxs-lookup"><span data-stu-id="de07b-120">Create an Azure resource group</span></span>
* <span data-ttu-id="de07b-121">建立 Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="de07b-121">Create an Azure Storage account</span></span>
* <span data-ttu-id="de07b-122">建立 Azure Blob 容器</span><span class="sxs-lookup"><span data-stu-id="de07b-122">Create an Azure Blob container</span></span>
* <span data-ttu-id="de07b-123">建立 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="de07b-123">Create an HDInsight cluster</span></span>

<span data-ttu-id="de07b-124">hello 下列指令碼示範如何 toocreate 新叢集：</span><span class="sxs-lookup"><span data-stu-id="de07b-124">hello following script demonstrates how toocreate a new cluster:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]

<span data-ttu-id="de07b-125">您指定給 hello 叢集登入的 hello 值是使用的 toocreate hello hello 叢集的 Hadoop 使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="de07b-125">hello values you specify for hello cluster login are used toocreate hello Hadoop user account for hello cluster.</span></span> <span data-ttu-id="de07b-126">使用此帳戶 tooconnect tooservices，例如 web Ui 或 REST Api 的 hello 叢集上裝載。</span><span class="sxs-lookup"><span data-stu-id="de07b-126">Use this account tooconnect tooservices hosted on hello cluster such as web UIs or REST APIs.</span></span>

<span data-ttu-id="de07b-127">您為 hello SSH 使用者指定的 hello 值為 hello 叢集使用的 toocreate hello SSH 使用者。</span><span class="sxs-lookup"><span data-stu-id="de07b-127">hello values you specify for hello SSH user are used toocreate hello SSH user for hello cluster.</span></span> <span data-ttu-id="de07b-128">使用此帳戶在 hello 叢集 toostart 遠端的 SSH 工作階段，並執行工作。</span><span class="sxs-lookup"><span data-stu-id="de07b-128">Use this account toostart a remote SSH session on hello cluster and run jobs.</span></span> <span data-ttu-id="de07b-129">如需詳細資訊，請參閱 hello[搭配使用 SSH 和 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)文件。</span><span class="sxs-lookup"><span data-stu-id="de07b-129">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="de07b-130">如果您計劃 toouse 32 個以上的背景工作節點 （在建立叢集，或調整 hello 叢集建立之後），您也必須指定至少 8 核心，14 GB 的 RAM 與前端節點大小。</span><span class="sxs-lookup"><span data-stu-id="de07b-130">If you plan toouse more than 32 worker nodes (either at cluster creation or by scaling hello cluster after creation), you must also specify a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
> <span data-ttu-id="de07b-131">如需節點大小和相關成本的詳細資訊，請參閱 [HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="de07b-131">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="de07b-132">它可能會佔用 too20 分鐘 toocreate 叢集。</span><span class="sxs-lookup"><span data-stu-id="de07b-132">It can take up too20 minutes toocreate a cluster.</span></span>

## <a name="create-cluster-configuration-object"></a><span data-ttu-id="de07b-133">建立叢集：設定物件</span><span class="sxs-lookup"><span data-stu-id="de07b-133">Create cluster: Configuration object</span></span>

<span data-ttu-id="de07b-134">您也可以使用 `New-AzureRmHDInsightClusterConfig` Cmdlet 建立 HDInsight 設定物件。</span><span class="sxs-lookup"><span data-stu-id="de07b-134">You can also create an HDInsight configuration object using `New-AzureRmHDInsightClusterConfig` cmdlet.</span></span> <span data-ttu-id="de07b-135">然後，您就可以修改此組態物件 tooenable 其他設定選項為您的叢集。</span><span class="sxs-lookup"><span data-stu-id="de07b-135">You can then modify this configuration object tooenable additional configuration options for your cluster.</span></span> <span data-ttu-id="de07b-136">最後，使用 hello `-Config` hello 參數`New-AzureRmHDInsightCluster`cmdlet toouse hello 組態。</span><span class="sxs-lookup"><span data-stu-id="de07b-136">Finally, use hello `-Config` parameter of hello `New-AzureRmHDInsightCluster` cmdlet toouse hello configuration.</span></span>

<span data-ttu-id="de07b-137">hello 下列指令碼組態物件 tooconfigure R 伺服器上建立 HDInsight 叢集類型。</span><span class="sxs-lookup"><span data-stu-id="de07b-137">hello following script creates a configuration object tooconfigure an R Server on HDInsight cluster type.</span></span> <span data-ttu-id="de07b-138">hello 組態可讓邊緣節點、 RStudio、 和額外的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="de07b-138">hello configuration enables an edge node, RStudio, and an additional storage account.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]

> [!WARNING]
> <span data-ttu-id="de07b-139">不支援在 hello HDInsight 叢集以外的不同位置中使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="de07b-139">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span> <span data-ttu-id="de07b-140">使用此範例中，當建立 hello 額外的儲存體帳戶中 hello 與 hello 伺服器相同的位置。</span><span class="sxs-lookup"><span data-stu-id="de07b-140">When using this example, create hello additional storage account in hello same location as hello server.</span></span>

## <a name="customize-clusters"></a><span data-ttu-id="de07b-141">自訂叢集</span><span class="sxs-lookup"><span data-stu-id="de07b-141">Customize clusters</span></span>

* <span data-ttu-id="de07b-142">請參閱 [使用 Bootstrap 自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="de07b-142">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span></span>
* <span data-ttu-id="de07b-143">請參閱[使用指令碼動作來自訂 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="de07b-143">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="de07b-144">刪除 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="de07b-144">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="de07b-145">疑難排解</span><span class="sxs-lookup"><span data-stu-id="de07b-145">Troubleshoot</span></span>

<span data-ttu-id="de07b-146">如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="de07b-146">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="de07b-147">後續步驟</span><span class="sxs-lookup"><span data-stu-id="de07b-147">Next steps</span></span>

<span data-ttu-id="de07b-148">現在您已成功建立的 HDInsight 叢集，使用下列資源 toolearn 如何 hello toowork 與您的叢集。</span><span class="sxs-lookup"><span data-stu-id="de07b-148">Now that you have successfully created an HDInsight cluster, use hello following resources toolearn how toowork with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="de07b-149">Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="de07b-149">Hadoop clusters</span></span>

* [<span data-ttu-id="de07b-150">〈搭配 HDInsight 使用 Hivet〉</span><span class="sxs-lookup"><span data-stu-id="de07b-150">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="de07b-151">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="de07b-151">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="de07b-152">〈搭配 HDInsight 使用 MapReduce〉</span><span class="sxs-lookup"><span data-stu-id="de07b-152">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="de07b-153">HBase 叢集</span><span class="sxs-lookup"><span data-stu-id="de07b-153">HBase clusters</span></span>

* [<span data-ttu-id="de07b-154">開始在 HDInsight 上使用 HBase</span><span class="sxs-lookup"><span data-stu-id="de07b-154">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="de07b-155">在 HDInsight 上開發適用於 HBase 的 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="de07b-155">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="de07b-156">Storm 叢集</span><span class="sxs-lookup"><span data-stu-id="de07b-156">Storm clusters</span></span>

* [<span data-ttu-id="de07b-157">在 HDInsight 上開發適用於 Storm 的 Java 拓撲</span><span class="sxs-lookup"><span data-stu-id="de07b-157">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="de07b-158">在 HDInsight 上的 Storm 中使用 Python 元件</span><span class="sxs-lookup"><span data-stu-id="de07b-158">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="de07b-159">在 HDInsight 上使用 Storm 部署和監視拓撲</span><span class="sxs-lookup"><span data-stu-id="de07b-159">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="de07b-160">Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="de07b-160">Spark clusters</span></span>

* [<span data-ttu-id="de07b-161">使用 Scala 來建立獨立的應用程式</span><span class="sxs-lookup"><span data-stu-id="de07b-161">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="de07b-162">利用 Livy 在 Spark 叢集上遠端執行工作</span><span class="sxs-lookup"><span data-stu-id="de07b-162">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="de07b-163">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="de07b-163">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="de07b-164">機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark</span><span class="sxs-lookup"><span data-stu-id="de07b-164">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="de07b-165">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="de07b-165">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

