---
title: "使用命令列建立 Hadoop 叢集 - Azure HDInsight | Microsoft Docs"
description: "了解如何使用跨平台 Azure CLI 1.0 建立 HDInsight 叢集。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 50b01483-455c-4d87-b754-2229005a8ab9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 8f2fcb46789d000cd66164508f1159338dcae5f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-hdinsight-clusters-using-the-azure-cli"></a><span data-ttu-id="18a3c-103">使用 Azure CLI 建立 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="18a3c-103">Create HDInsight clusters using the Azure CLI</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="18a3c-104">此文件中的步驟詳細說明如何使用 Azure CLI 1.0 建立 HDInsight 3.5 叢集。</span><span class="sxs-lookup"><span data-stu-id="18a3c-104">The steps in this document walk-through creating a HDInsight 3.5 cluster using the Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="18a3c-105">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="18a3c-105">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="18a3c-106">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="18a3c-106">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="18a3c-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="18a3c-107">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="18a3c-108">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="18a3c-108">**An Azure subscription**.</span></span> <span data-ttu-id="18a3c-109">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="18a3c-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="18a3c-110">**Azure CLI**。</span><span class="sxs-lookup"><span data-stu-id="18a3c-110">**Azure CLI**.</span></span> <span data-ttu-id="18a3c-111">這份文件中的步驟最近一次是以 Azure CLI 版本 0.10.14 來測試。</span><span class="sxs-lookup"><span data-stu-id="18a3c-111">The steps in this document were last tested with Azure CLI version 0.10.14.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="18a3c-112">此文件中的步驟不適用於 Azure CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="18a3c-112">The steps in this document do not work with Azure CLI 2.0.</span></span> <span data-ttu-id="18a3c-113">Azure CLI 2.0 不支援建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="18a3c-113">Azure CLI 2.0 does not support creating an HDInsight cluster.</span></span>

## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="18a3c-114">登入您的 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="18a3c-114">Log in to your Azure subscription</span></span>

<span data-ttu-id="18a3c-115">依照 [從 Azure 命令列介面 (Azure CLI) 連接到 Azure 訂用帳戶](../xplat-cli-connect.md) 中記載的步驟，使用 **login** 方法連線到您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="18a3c-115">Follow the steps documented in [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect to your subscription using the **login** method.</span></span>

## <a name="create-a-cluster"></a><span data-ttu-id="18a3c-116">建立叢集</span><span class="sxs-lookup"><span data-stu-id="18a3c-116">Create a cluster</span></span>

<span data-ttu-id="18a3c-117">下列步驟應透過命令列 (如 PowerShell 或 Bash) 執行。</span><span class="sxs-lookup"><span data-stu-id="18a3c-117">The following steps should be performed from a command line, such as PowerShell or Bash.</span></span>

1. <span data-ttu-id="18a3c-118">使用下列命令來驗證您的 Azure 訂用帳戶：</span><span class="sxs-lookup"><span data-stu-id="18a3c-118">Use the following command to authenticate to your Azure subscription:</span></span>

        azure login

    <span data-ttu-id="18a3c-119">系統會提示您提供使用者名稱與密碼。</span><span class="sxs-lookup"><span data-stu-id="18a3c-119">You are prompted to provide your name and password.</span></span> <span data-ttu-id="18a3c-120">如果您有多個 Azure 訂用帳戶，則可以使用 `azure account set <subscriptionname>` 來設定 Azure CLI 命令所使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="18a3c-120">If you have multiple Azure subscriptions, use `azure account set <subscriptionname>` to set the subscription that the Azure CLI commands use.</span></span>

2. <span data-ttu-id="18a3c-121">使用下列命令來切換至 Azure 資源管理員模式︰</span><span class="sxs-lookup"><span data-stu-id="18a3c-121">Switch to Azure Resource Manager mode using the following command:</span></span>

        azure config mode arm

3. <span data-ttu-id="18a3c-122">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="18a3c-122">Create a resource group.</span></span> <span data-ttu-id="18a3c-123">此資源群組包含 HDInsight 叢集和關聯的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="18a3c-123">This resource group contains the HDInsight cluster and associated storage account.</span></span>

        azure group create groupname location

    * <span data-ttu-id="18a3c-124">以群組的唯一名稱取代 `groupname`。</span><span class="sxs-lookup"><span data-stu-id="18a3c-124">Replace `groupname` with a unique name for the group.</span></span>

    * <span data-ttu-id="18a3c-125">以您想要在其中建立群組的地理區域取代 `location`。</span><span class="sxs-lookup"><span data-stu-id="18a3c-125">Replace `location` with the geographic region that you want to create the group in.</span></span>

       <span data-ttu-id="18a3c-126">如需有效位置的清單，請使用 `azure location list` 命令，然後使用 [`Name`] \(名稱\) 欄中的其中一個位置。</span><span class="sxs-lookup"><span data-stu-id="18a3c-126">For a list of valid locations, use the `azure location list` command, and then use one of the locations from the `Name` column.</span></span>

4. <span data-ttu-id="18a3c-127">建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="18a3c-127">Create a storage account.</span></span> <span data-ttu-id="18a3c-128">此儲存體帳戶會用來作為 HDInsight 叢集的預設儲存體。</span><span class="sxs-lookup"><span data-stu-id="18a3c-128">This storage account is used as the default storage for the HDInsight cluster.</span></span>

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * <span data-ttu-id="18a3c-129">以上一個步驟中建立的群組名稱取代 `groupname`。</span><span class="sxs-lookup"><span data-stu-id="18a3c-129">Replace `groupname` with the name of the group created in the previous step.</span></span>

    * <span data-ttu-id="18a3c-130">以與上一個步驟中使用的相同位置取代 `location`。</span><span class="sxs-lookup"><span data-stu-id="18a3c-130">Replace `location` with the same location used in the previous step.</span></span>

    * <span data-ttu-id="18a3c-131">以儲存體帳戶的唯一名稱取代 `storagename`。</span><span class="sxs-lookup"><span data-stu-id="18a3c-131">Replace `storagename` with a unique name for the storage account.</span></span>

        > [!NOTE]
        > <span data-ttu-id="18a3c-132">如需有關此命令中所使用參數的詳細資訊，請使用 `azure storage account create -h` 來檢視此命令的說明。</span><span class="sxs-lookup"><span data-stu-id="18a3c-132">For more information on the parameters used in this command, use `azure storage account create -h` to view help for this command.</span></span>

5. <span data-ttu-id="18a3c-133">擷取用來存取儲存體帳戶的金鑰。</span><span class="sxs-lookup"><span data-stu-id="18a3c-133">Retrieve the key used to access the storage account.</span></span>

        azure storage account keys list -g groupname storagename

    * <span data-ttu-id="18a3c-134">以資源群組名稱取代 `groupname`。</span><span class="sxs-lookup"><span data-stu-id="18a3c-134">Replace `groupname` with the resource group name.</span></span>
    * <span data-ttu-id="18a3c-135">使用儲存體帳戶名稱取代 `storagename`。</span><span class="sxs-lookup"><span data-stu-id="18a3c-135">Replace `storagename` with the name of the storage account.</span></span>

     <span data-ttu-id="18a3c-136">在傳回的資料中，儲存 `key1` 的 `key` 值。</span><span class="sxs-lookup"><span data-stu-id="18a3c-136">In the data that is returned, save the `key` value for `key1`.</span></span>

6. <span data-ttu-id="18a3c-137">建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="18a3c-137">Create an HDInsight cluster.</span></span>

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * <span data-ttu-id="18a3c-138">以資源群組名稱取代 `groupname`。</span><span class="sxs-lookup"><span data-stu-id="18a3c-138">Replace `groupname` with the resource group name.</span></span>

    * <span data-ttu-id="18a3c-139">將 `Hadoop` 取代為您想要建立的叢集類型。</span><span class="sxs-lookup"><span data-stu-id="18a3c-139">Replace `Hadoop` with the cluster type that you wish to create.</span></span> <span data-ttu-id="18a3c-140">例如，`Hadoop`、`HBase`、`Kafka`、`Spark` 或 `Storm`。</span><span class="sxs-lookup"><span data-stu-id="18a3c-140">For example, `Hadoop`, `HBase`, `Kafka`, `Spark`, or `Storm`.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="18a3c-141">HDInsight 叢集有各種不同類型，這些類型各自對應到叢集微調時所針對的工作負載或技術。</span><span class="sxs-lookup"><span data-stu-id="18a3c-141">HDInsight clusters come in various types, which correspond to the workload or technology that the cluster is tuned for.</span></span> <span data-ttu-id="18a3c-142">沒有任何支援方法可建立結合多個類型的叢集，例如在一個叢集上並存 Storm 和 HBase。</span><span class="sxs-lookup"><span data-stu-id="18a3c-142">There is no supported method to create a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span>

    * <span data-ttu-id="18a3c-143">以與前述步驟中使用的相同位置取代 `location`。</span><span class="sxs-lookup"><span data-stu-id="18a3c-143">Replace `location` with the same location used in previous steps.</span></span>

    * <span data-ttu-id="18a3c-144">使用儲存體帳戶名稱取代 `storagename`。</span><span class="sxs-lookup"><span data-stu-id="18a3c-144">Replace `storagename` with the storage account name.</span></span>

    * <span data-ttu-id="18a3c-145">以在上一個步驟中取得的金鑰取代 `storagekey`。</span><span class="sxs-lookup"><span data-stu-id="18a3c-145">Replace `storagekey` with the key obtained in the previous step.</span></span>

    * <span data-ttu-id="18a3c-146">針對 `--defaultStorageContainer` 參數，使用與您用於叢集的相同名稱。</span><span class="sxs-lookup"><span data-stu-id="18a3c-146">For the `--defaultStorageContainer` parameter, use the same name as you are using for the cluster.</span></span>

    * <span data-ttu-id="18a3c-147">以當您透過 HTTPS 存取叢集時所要使用的名稱和密碼取代 `admin` 和 `httppassword`。</span><span class="sxs-lookup"><span data-stu-id="18a3c-147">Replace `admin` and `httppassword` with the name and password you wish to use when accessing the cluster through HTTPS.</span></span>

    * <span data-ttu-id="18a3c-148">以當您使用 SSH 存取叢集時所要使用的使用者名稱和密碼取代 `sshuser` 和 `sshuserpassword`。</span><span class="sxs-lookup"><span data-stu-id="18a3c-148">Replace `sshuser` and `sshuserpassword` with the username and password you wish to use when accessing the cluster using SSH</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="18a3c-149">此範例使用兩個背景工作角色節點建立叢集。</span><span class="sxs-lookup"><span data-stu-id="18a3c-149">This example creates a cluster with two worker notes.</span></span> <span data-ttu-id="18a3c-150">您也可以在叢集建立後執行調整規模作業，以變更背景工作角色節點數。</span><span class="sxs-lookup"><span data-stu-id="18a3c-150">You can also change the number of worker nodes after cluster creation by performing scaling operations.</span></span> <span data-ttu-id="18a3c-151">如果您規劃使用 32 個以上的背景工作角色節點，則必須選取具有至少 8 個核心和 14 GB RAM 的前端節點大小。</span><span class="sxs-lookup"><span data-stu-id="18a3c-151">If you plan on using more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14-GB RAM.</span></span> <span data-ttu-id="18a3c-152">建立叢集期間，您可以使用 `--headNodeSize` 參數來設定前端節點大小。</span><span class="sxs-lookup"><span data-stu-id="18a3c-152">You can set the head node size by using the `--headNodeSize` parameter during cluster creation.</span></span>
    >
    > <span data-ttu-id="18a3c-153">如需節點大小和相關成本的詳細資訊，請參閱 [HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="18a3c-153">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

    <span data-ttu-id="18a3c-154">可能需要數分鐘的時間，才能完成叢集建立程序。</span><span class="sxs-lookup"><span data-stu-id="18a3c-154">It may take several minutes for the cluster creation process to finish.</span></span> <span data-ttu-id="18a3c-155">通常大約 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="18a3c-155">Usually around 15.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="18a3c-156">疑難排解</span><span class="sxs-lookup"><span data-stu-id="18a3c-156">Troubleshoot</span></span>

<span data-ttu-id="18a3c-157">如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="18a3c-157">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="18a3c-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="18a3c-158">Next steps</span></span>

<span data-ttu-id="18a3c-159">既然您已使用 Azure CLI 順利建立 HDInsight 叢集，請使用下列內容來了解如何使用您的叢集：</span><span class="sxs-lookup"><span data-stu-id="18a3c-159">Now that you have successfully created an HDInsight cluster using the Azure CLI, use the following to learn how to work with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="18a3c-160">Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="18a3c-160">Hadoop clusters</span></span>

* [<span data-ttu-id="18a3c-161">〈搭配 HDInsight 使用 Hivet〉</span><span class="sxs-lookup"><span data-stu-id="18a3c-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="18a3c-162">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="18a3c-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="18a3c-163">〈搭配 HDInsight 使用 MapReduce〉</span><span class="sxs-lookup"><span data-stu-id="18a3c-163">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="18a3c-164">HBase 叢集</span><span class="sxs-lookup"><span data-stu-id="18a3c-164">HBase clusters</span></span>

* [<span data-ttu-id="18a3c-165">開始在 HDInsight 上使用 HBase</span><span class="sxs-lookup"><span data-stu-id="18a3c-165">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="18a3c-166">在 HDInsight 上開發適用於 HBase 的 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="18a3c-166">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="18a3c-167">Storm 叢集</span><span class="sxs-lookup"><span data-stu-id="18a3c-167">Storm clusters</span></span>

* [<span data-ttu-id="18a3c-168">在 HDInsight 上開發適用於 Storm 的 Java 拓撲</span><span class="sxs-lookup"><span data-stu-id="18a3c-168">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="18a3c-169">在 HDInsight 上的 Storm 中使用 Python 元件</span><span class="sxs-lookup"><span data-stu-id="18a3c-169">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="18a3c-170">在 HDInsight 上使用 Storm 部署和監視拓撲</span><span class="sxs-lookup"><span data-stu-id="18a3c-170">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
