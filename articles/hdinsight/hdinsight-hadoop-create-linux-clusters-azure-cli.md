---
title: "使用命令列-hello Azure HDInsight aaaCreate Hadoop 叢集 |Microsoft 文件"
description: "了解如何使用 toocreate HDInsight 叢集 hello 跨平台 Azure CLI 1.0。"
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
ms.openlocfilehash: 5295b01054b8c23df0e3b75a3e0e8c933ac48b3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-using-hello-azure-cli"></a><span data-ttu-id="859b5-103">建立使用 Azure CLI hello 的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="859b5-103">Create HDInsight clusters using hello Azure CLI</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="859b5-104">建立使用 Azure CLI 1.0 hello HDInsight 3.5 叢集文件逐步解說中的步驟 hello。</span><span class="sxs-lookup"><span data-stu-id="859b5-104">hello steps in this document walk-through creating a HDInsight 3.5 cluster using hello Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="859b5-105">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="859b5-105">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="859b5-106">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="859b5-106">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="859b5-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="859b5-107">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="859b5-108">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="859b5-108">**An Azure subscription**.</span></span> <span data-ttu-id="859b5-109">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="859b5-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="859b5-110">**Azure CLI**。</span><span class="sxs-lookup"><span data-stu-id="859b5-110">**Azure CLI**.</span></span> <span data-ttu-id="859b5-111">本文件中的 hello 步驟上一次使用 Azure CLI 版本 0.10.14 測試。</span><span class="sxs-lookup"><span data-stu-id="859b5-111">hello steps in this document were last tested with Azure CLI version 0.10.14.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="859b5-112">本文件中的 hello 步驟使用 Azure CLI 2.0 無法運作。</span><span class="sxs-lookup"><span data-stu-id="859b5-112">hello steps in this document do not work with Azure CLI 2.0.</span></span> <span data-ttu-id="859b5-113">Azure CLI 2.0 不支援建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="859b5-113">Azure CLI 2.0 does not support creating an HDInsight cluster.</span></span>

## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="859b5-114">登入 tooyour Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="859b5-114">Log in tooyour Azure subscription</span></span>

<span data-ttu-id="859b5-115">所述步驟 hello [hello Azure 命令列介面 (Azure CLI) 從連接 tooan Azure 訂用帳戶](../xplat-cli-connect.md)並連接 tooyour 訂用帳戶使用 hello**登入**方法。</span><span class="sxs-lookup"><span data-stu-id="859b5-115">Follow hello steps documented in [Connect tooan Azure subscription from hello Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect tooyour subscription using hello **login** method.</span></span>

## <a name="create-a-cluster"></a><span data-ttu-id="859b5-116">建立叢集</span><span class="sxs-lookup"><span data-stu-id="859b5-116">Create a cluster</span></span>

<span data-ttu-id="859b5-117">從命令列，例如 PowerShell 或 Bash，應執行下列步驟的 hello。</span><span class="sxs-lookup"><span data-stu-id="859b5-117">hello following steps should be performed from a command line, such as PowerShell or Bash.</span></span>

1. <span data-ttu-id="859b5-118">使用下列命令 tooauthenticate tooyour Azure 訂用帳戶的 hello:</span><span class="sxs-lookup"><span data-stu-id="859b5-118">Use hello following command tooauthenticate tooyour Azure subscription:</span></span>

        azure login

    <span data-ttu-id="859b5-119">您是提示的 tooprovide，您的名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="859b5-119">You are prompted tooprovide your name and password.</span></span> <span data-ttu-id="859b5-120">如果您有多個 Azure 訂用帳戶，使用`azure account set <subscriptionname>`tooset hello 訂閱 hello Azure CLI 命令使用。</span><span class="sxs-lookup"><span data-stu-id="859b5-120">If you have multiple Azure subscriptions, use `azure account set <subscriptionname>` tooset hello subscription that hello Azure CLI commands use.</span></span>

2. <span data-ttu-id="859b5-121">切換使用下列命令的 hello tooAzure Resource Manager 模式：</span><span class="sxs-lookup"><span data-stu-id="859b5-121">Switch tooAzure Resource Manager mode using hello following command:</span></span>

        azure config mode arm

3. <span data-ttu-id="859b5-122">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="859b5-122">Create a resource group.</span></span> <span data-ttu-id="859b5-123">此資源群組包含 hello HDInsight 叢集與儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="859b5-123">This resource group contains hello HDInsight cluster and associated storage account.</span></span>

        azure group create groupname location

    * <span data-ttu-id="859b5-124">取代`groupname`與 hello 群組的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="859b5-124">Replace `groupname` with a unique name for hello group.</span></span>

    * <span data-ttu-id="859b5-125">取代`location`與您想要的 toocreate hello 群組中的 hello 地理區域。</span><span class="sxs-lookup"><span data-stu-id="859b5-125">Replace `location` with hello geographic region that you want toocreate hello group in.</span></span>

       <span data-ttu-id="859b5-126">如需清單的有效位置，使用 hello`azure location list`命令，然後再使用其中一種從 hello hello 位置`Name`資料行。</span><span class="sxs-lookup"><span data-stu-id="859b5-126">For a list of valid locations, use hello `azure location list` command, and then use one of hello locations from hello `Name` column.</span></span>

4. <span data-ttu-id="859b5-127">建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="859b5-127">Create a storage account.</span></span> <span data-ttu-id="859b5-128">這個儲存體帳戶作為 hello 預設儲存體 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="859b5-128">This storage account is used as hello default storage for hello HDInsight cluster.</span></span>

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * <span data-ttu-id="859b5-129">取代`groupname`與 hello hello 先前步驟中建立的 hello 群組名稱。</span><span class="sxs-lookup"><span data-stu-id="859b5-129">Replace `groupname` with hello name of hello group created in hello previous step.</span></span>

    * <span data-ttu-id="859b5-130">取代`location`以 hello hello 上一個步驟中使用相同的位置。</span><span class="sxs-lookup"><span data-stu-id="859b5-130">Replace `location` with hello same location used in hello previous step.</span></span>

    * <span data-ttu-id="859b5-131">取代`storagename`與 hello 儲存體帳戶的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="859b5-131">Replace `storagename` with a unique name for hello storage account.</span></span>

        > [!NOTE]
        > <span data-ttu-id="859b5-132">如需此命令中使用的 hello 參數的詳細資訊，請使用`azure storage account create -h`tooview 此命令的說明。</span><span class="sxs-lookup"><span data-stu-id="859b5-132">For more information on hello parameters used in this command, use `azure storage account create -h` tooview help for this command.</span></span>

5. <span data-ttu-id="859b5-133">擷取 hello 金鑰用 tooaccess hello 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="859b5-133">Retrieve hello key used tooaccess hello storage account.</span></span>

        azure storage account keys list -g groupname storagename

    * <span data-ttu-id="859b5-134">取代`groupname`hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="859b5-134">Replace `groupname` with hello resource group name.</span></span>
    * <span data-ttu-id="859b5-135">取代`storagename`與 hello hello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="859b5-135">Replace `storagename` with hello name of hello storage account.</span></span>

     <span data-ttu-id="859b5-136">在 hello 所傳回的資料，將儲存 hello`key`值`key1`。</span><span class="sxs-lookup"><span data-stu-id="859b5-136">In hello data that is returned, save hello `key` value for `key1`.</span></span>

6. <span data-ttu-id="859b5-137">建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="859b5-137">Create an HDInsight cluster.</span></span>

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * <span data-ttu-id="859b5-138">取代`groupname`hello 資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="859b5-138">Replace `groupname` with hello resource group name.</span></span>

    * <span data-ttu-id="859b5-139">取代`Hadoop`與您想 toocreate hello 叢集類型。</span><span class="sxs-lookup"><span data-stu-id="859b5-139">Replace `Hadoop` with hello cluster type that you wish toocreate.</span></span> <span data-ttu-id="859b5-140">例如，`Hadoop`、`HBase`、`Kafka`、`Spark` 或 `Storm`。</span><span class="sxs-lookup"><span data-stu-id="859b5-140">For example, `Hadoop`, `HBase`, `Kafka`, `Spark`, or `Storm`.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="859b5-141">HDInsight 叢集有不同的類型，對應 toohello 工作負載或調整為 hello 叢集的技術。</span><span class="sxs-lookup"><span data-stu-id="859b5-141">HDInsight clusters come in various types, which correspond toohello workload or technology that hello cluster is tuned for.</span></span> <span data-ttu-id="859b5-142">沒有任何支援的方法 toocreate 結合多個類型，例如 Storm 和上一個叢集的 HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="859b5-142">There is no supported method toocreate a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span>

    * <span data-ttu-id="859b5-143">取代`location`以 hello 在先前步驟中使用相同的位置。</span><span class="sxs-lookup"><span data-stu-id="859b5-143">Replace `location` with hello same location used in previous steps.</span></span>

    * <span data-ttu-id="859b5-144">取代`storagename`hello 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="859b5-144">Replace `storagename` with hello storage account name.</span></span>

    * <span data-ttu-id="859b5-145">取代`storagekey`與 hello hello 先前步驟中取得的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="859b5-145">Replace `storagekey` with hello key obtained in hello previous step.</span></span>

    * <span data-ttu-id="859b5-146">Hello`--defaultStorageContainer`參數、 相同的名稱，因為您使用 hello 叢集使用 hello。</span><span class="sxs-lookup"><span data-stu-id="859b5-146">For hello `--defaultStorageContainer` parameter, use hello same name as you are using for hello cluster.</span></span>

    * <span data-ttu-id="859b5-147">取代`admin`和`httppassword`hello 名稱和密碼與您想 toouse 透過 HTTPS 存取 hello 叢集時。</span><span class="sxs-lookup"><span data-stu-id="859b5-147">Replace `admin` and `httppassword` with hello name and password you wish toouse when accessing hello cluster through HTTPS.</span></span>

    * <span data-ttu-id="859b5-148">取代`sshuser`和`sshuserpassword`hello 使用者名稱和密碼與您想 toouse 時存取使用 SSH hello 叢集</span><span class="sxs-lookup"><span data-stu-id="859b5-148">Replace `sshuser` and `sshuserpassword` with hello username and password you wish toouse when accessing hello cluster using SSH</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="859b5-149">此範例使用兩個背景工作角色節點建立叢集。</span><span class="sxs-lookup"><span data-stu-id="859b5-149">This example creates a cluster with two worker notes.</span></span> <span data-ttu-id="859b5-150">您也可以執行縮放作業，在叢集建立之後變更 hello 背景工作節點數。</span><span class="sxs-lookup"><span data-stu-id="859b5-150">You can also change hello number of worker nodes after cluster creation by performing scaling operations.</span></span> <span data-ttu-id="859b5-151">如果您規劃使用 32 個以上的背景工作角色節點，則必須選取具有至少 8 個核心和 14 GB RAM 的前端節點大小。</span><span class="sxs-lookup"><span data-stu-id="859b5-151">If you plan on using more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14-GB RAM.</span></span> <span data-ttu-id="859b5-152">您可以設定 hello 前端節點大小使用 hello`--headNodeSize`在叢集建立期間參數。</span><span class="sxs-lookup"><span data-stu-id="859b5-152">You can set hello head node size by using hello `--headNodeSize` parameter during cluster creation.</span></span>
    >
    > <span data-ttu-id="859b5-153">如需節點大小和相關成本的詳細資訊，請參閱 [HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="859b5-153">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

    <span data-ttu-id="859b5-154">可能需要幾分鐘的時間 hello 叢集建立程序 toofinish。</span><span class="sxs-lookup"><span data-stu-id="859b5-154">It may take several minutes for hello cluster creation process toofinish.</span></span> <span data-ttu-id="859b5-155">通常大約 15 分鐘。</span><span class="sxs-lookup"><span data-stu-id="859b5-155">Usually around 15.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="859b5-156">疑難排解</span><span class="sxs-lookup"><span data-stu-id="859b5-156">Troubleshoot</span></span>

<span data-ttu-id="859b5-157">如果您在建立 HDInsight 叢集時遇到問題，請參閱[存取控制需求](hdinsight-administer-use-portal-linux.md#create-clusters)。</span><span class="sxs-lookup"><span data-stu-id="859b5-157">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="859b5-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="859b5-158">Next steps</span></span>

<span data-ttu-id="859b5-159">既然您已成功建立使用 Azure CLI hello 的 HDInsight 叢集，請使用 hello 如何遵循 toolearn toowork 與您的叢集：</span><span class="sxs-lookup"><span data-stu-id="859b5-159">Now that you have successfully created an HDInsight cluster using hello Azure CLI, use hello following toolearn how toowork with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="859b5-160">Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="859b5-160">Hadoop clusters</span></span>

* [<span data-ttu-id="859b5-161">〈搭配 HDInsight 使用 Hivet〉</span><span class="sxs-lookup"><span data-stu-id="859b5-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="859b5-162">搭配 HDInsight 使用 Pig</span><span class="sxs-lookup"><span data-stu-id="859b5-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="859b5-163">〈搭配 HDInsight 使用 MapReduce〉</span><span class="sxs-lookup"><span data-stu-id="859b5-163">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="859b5-164">HBase 叢集</span><span class="sxs-lookup"><span data-stu-id="859b5-164">HBase clusters</span></span>

* [<span data-ttu-id="859b5-165">開始在 HDInsight 上使用 HBase</span><span class="sxs-lookup"><span data-stu-id="859b5-165">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="859b5-166">在 HDInsight 上開發適用於 HBase 的 Java 應用程式</span><span class="sxs-lookup"><span data-stu-id="859b5-166">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="859b5-167">Storm 叢集</span><span class="sxs-lookup"><span data-stu-id="859b5-167">Storm clusters</span></span>

* [<span data-ttu-id="859b5-168">在 HDInsight 上開發適用於 Storm 的 Java 拓撲</span><span class="sxs-lookup"><span data-stu-id="859b5-168">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="859b5-169">在 HDInsight 上的 Storm 中使用 Python 元件</span><span class="sxs-lookup"><span data-stu-id="859b5-169">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="859b5-170">在 HDInsight 上使用 Storm 部署和監視拓撲</span><span class="sxs-lookup"><span data-stu-id="859b5-170">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
