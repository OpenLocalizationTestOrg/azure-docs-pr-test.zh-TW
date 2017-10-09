---
title: "虛擬網路-Azure 內 aaaConfigure HBase 叢集複寫 |Microsoft 文件"
description: "深入了解如何 tooconfigure HBase 複寫負載平衡，高可用性、 零停機時間移轉/更新從一個 HDInsight 版本 tooanother 和災害復原。"
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ba1c44f26b7cbf4a7a88159b12b3e064ea9f9a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a><span data-ttu-id="720e6-103">設定虛擬網路中的 HBase 叢集複寫</span><span class="sxs-lookup"><span data-stu-id="720e6-103">Configure HBase cluster replication within virtual networks</span></span>

<span data-ttu-id="720e6-104">深入了解如何 tooconfigure HBase 複寫一個虛擬網路 (VNet) 內，或兩個虛擬網路之間。</span><span class="sxs-lookup"><span data-stu-id="720e6-104">Learn how tooconfigure HBase replication within one virtual network (VNet) or between two virtual networks.</span></span>

<span data-ttu-id="720e6-105">叢集複寫會使用來源推入方法。</span><span class="sxs-lookup"><span data-stu-id="720e6-105">Cluster replication uses a source-push methodology.</span></span> <span data-ttu-id="720e6-106">HBase 叢集可以是來源、目的地，或可同時滿足兩個角色。</span><span class="sxs-lookup"><span data-stu-id="720e6-106">An HBase cluster can be a source or a destination, or it can fulfill both roles at once.</span></span> <span data-ttu-id="720e6-107">複寫是非同步的並複寫 hello 目標是最終一致性。</span><span class="sxs-lookup"><span data-stu-id="720e6-107">Replication is asynchronous, and hello goal of replication is eventual consistency.</span></span> <span data-ttu-id="720e6-108">Hello 來源收到編輯 tooa 資料欄系列已啟用複寫時，編輯時傳播的 tooall 目的地叢集。</span><span class="sxs-lookup"><span data-stu-id="720e6-108">When hello source receives an edit tooa column family with replication enabled, that edit is propagated tooall destination clusters.</span></span> <span data-ttu-id="720e6-109">當資料從一個叢集 tooanother 複寫時，hello 來源叢集與所有已用完 hello 資料的叢集是追蹤的 tooprevent 複寫迴圈。</span><span class="sxs-lookup"><span data-stu-id="720e6-109">When data is replicated from one cluster tooanother, hello source cluster and all clusters that have already consumed hello data are tracked tooprevent replication loops.</span></span>

<span data-ttu-id="720e6-110">在本教學課程中，您將設定來源目的地複寫。</span><span class="sxs-lookup"><span data-stu-id="720e6-110">In this tutorial, you will configure a source-destination replication.</span></span> <span data-ttu-id="720e6-111">若需其他叢集拓撲，請參閱 [Apache HBase 參考指南](http://hbase.apache.org/book.html#_cluster_replication)。</span><span class="sxs-lookup"><span data-stu-id="720e6-111">For other cluster topologies, see [Apache HBase Reference Guide](http://hbase.apache.org/book.html#_cluster_replication).</span></span>

<span data-ttu-id="720e6-112">適用於單一虛擬網路的 HBase 複寫使用案例︰</span><span class="sxs-lookup"><span data-stu-id="720e6-112">HBase replication usage cases for a single virtual network:</span></span>

* <span data-ttu-id="720e6-113">負載平衡-例如，在 hello 目的地叢集上執行掃描或 MapReduce 工作和擷取 hello 來源叢集上的資料</span><span class="sxs-lookup"><span data-stu-id="720e6-113">Load balancing--for example, running scans or MapReduce jobs on hello destination cluster and ingesting data on hello source cluster</span></span>
* <span data-ttu-id="720e6-114">高可用性</span><span class="sxs-lookup"><span data-stu-id="720e6-114">High availability</span></span>
* <span data-ttu-id="720e6-115">從一個 HBase 叢集 tooanother 移轉資料</span><span class="sxs-lookup"><span data-stu-id="720e6-115">Migrating data from one HBase cluster tooanother</span></span>
* <span data-ttu-id="720e6-116">從一個版本 tooanother 升級 Azure HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="720e6-116">Upgrading an Azure HDInsight cluster from one version tooanother</span></span>

<span data-ttu-id="720e6-117">適用於兩個虛擬網路的 HBase 複寫使用案例︰</span><span class="sxs-lookup"><span data-stu-id="720e6-117">HBase replication usage cases for two virtual networks:</span></span>

* <span data-ttu-id="720e6-118">災害復原</span><span class="sxs-lookup"><span data-stu-id="720e6-118">Disaster recovery</span></span>
* <span data-ttu-id="720e6-119">負載平衡和資料分割 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="720e6-119">Load balancing and partitioning hello application</span></span>
* <span data-ttu-id="720e6-120">高可用性</span><span class="sxs-lookup"><span data-stu-id="720e6-120">High availability</span></span>

<span data-ttu-id="720e6-121">您會使用位於 [GitHub (英文)](https://github.com/Azure/hbase-utils/tree/master/replication) 的[指令碼動作](hdinsight-hadoop-customize-cluster-linux.md)指令碼複寫叢集。</span><span class="sxs-lookup"><span data-stu-id="720e6-121">You replicate clusters by using [script action](hdinsight-hadoop-customize-cluster-linux.md) scripts located at [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="720e6-122">必要條件</span><span class="sxs-lookup"><span data-stu-id="720e6-122">Prerequisites</span></span>
<span data-ttu-id="720e6-123">開始進行本教學課程之前，您必須擁有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="720e6-123">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="720e6-124">請參閱[取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="720e6-124">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="configure-hello-environments"></a><span data-ttu-id="720e6-125">設定 hello 環境</span><span class="sxs-lookup"><span data-stu-id="720e6-125">Configure hello environments</span></span>

<span data-ttu-id="720e6-126">有三個可能的設定︰</span><span class="sxs-lookup"><span data-stu-id="720e6-126">There are three possible configurations:</span></span>

- <span data-ttu-id="720e6-127">有兩個 HBase 叢集位於單一 Azure 虛擬網路中</span><span class="sxs-lookup"><span data-stu-id="720e6-127">Two HBase clusters in one Azure virtual network</span></span>
- <span data-ttu-id="720e6-128">兩個不同的虛擬網路中的兩個 HBase 叢集 hello 相同的區域</span><span class="sxs-lookup"><span data-stu-id="720e6-128">Two HBase clusters in two different virtual networks in hello same region</span></span>
- <span data-ttu-id="720e6-129">有兩個 HBase 叢集位於不同區域且不同的兩個虛擬網路中 (異地複寫)</span><span class="sxs-lookup"><span data-stu-id="720e6-129">Two HBase clusters in two different virtual networks in two different regions (geo-replication)</span></span>

<span data-ttu-id="720e6-130">toomake 它更容易 tooconfigure hello 環境中，我們建立了一些[Azure 資源管理員範本](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="720e6-130">toomake it easier tooconfigure hello environments, we have created some [Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="720e6-131">如果您偏好 tooconfigure hello 環境使用其他方法，請參閱：</span><span class="sxs-lookup"><span data-stu-id="720e6-131">If you prefer tooconfigure hello environments by using other methods, see:</span></span>

- [<span data-ttu-id="720e6-132">在 HDInsight 中建立以 Linux 為基礎的 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="720e6-132">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
- [<span data-ttu-id="720e6-133">在 Azure 虛擬網路上建立 HBase 叢集</span><span class="sxs-lookup"><span data-stu-id="720e6-133">Create HBase clusters in Azure Virtual Network</span></span>](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a><span data-ttu-id="720e6-134">設定一個虛擬網路</span><span class="sxs-lookup"><span data-stu-id="720e6-134">Configure one virtual network</span></span>

<span data-ttu-id="720e6-135">按一下下列映像 toocreate 兩個 HBase 叢集在 hello hello 相同虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="720e6-135">Click hello following image toocreate two HBase clusters in hello same virtual network.</span></span> <span data-ttu-id="720e6-136">hello 範本會儲存在[Azure 快速入門範本](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/)。</span><span class="sxs-lookup"><span data-stu-id="720e6-136">hello template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

### <a name="configure-two-virtual-networks-in-hello-same-region"></a><span data-ttu-id="720e6-137">在 hello 中設定兩個虛擬網路相同的區域</span><span class="sxs-lookup"><span data-stu-id="720e6-137">Configure two virtual networks in hello same region</span></span>

<span data-ttu-id="720e6-138">按一下 hello 下列映像 toocreate 兩個虛擬網路與對等互連的 VNet 中 hello 的兩個 HBase 叢集相同的區域。</span><span class="sxs-lookup"><span data-stu-id="720e6-138">Click hello following image toocreate two virtual networks with VNet peering and two HBase clusters in hello same region.</span></span> <span data-ttu-id="720e6-139">hello 範本會儲存在[Azure 快速入門範本](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/)。</span><span class="sxs-lookup"><span data-stu-id="720e6-139">hello template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>



<span data-ttu-id="720e6-140">此案例需要 [VNet 對等互連](../virtual-network/virtual-network-peering-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="720e6-140">This scenario requires [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> <span data-ttu-id="720e6-141">hello 範本可讓對等互連的 VNet。</span><span class="sxs-lookup"><span data-stu-id="720e6-141">hello template enables VNet peering.</span></span>   

<span data-ttu-id="720e6-142">對 HBase 複寫會使用 hello 動物園管理員 Vm 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="720e6-142">HBase replication uses IP addresses of hello ZooKeeper VMs.</span></span> <span data-ttu-id="720e6-143">您必須設定為 hello 目的地 HBase 動物園管理員節點的靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="720e6-143">You must configure static IP addresses for hello destination HBase ZooKeeper nodes.</span></span>

<span data-ttu-id="720e6-144">**tooconfigure 靜態 IP 位址**</span><span class="sxs-lookup"><span data-stu-id="720e6-144">**tooconfigure static IP addresses**</span></span>

1. <span data-ttu-id="720e6-145">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="720e6-145">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="720e6-146">從 hello 左窗格中，按一下 **資源群組**。</span><span class="sxs-lookup"><span data-stu-id="720e6-146">From hello left menu, click **Resource Groups**.</span></span>
3. <span data-ttu-id="720e6-147">按一下您的資源群組，其中包含 hello 目的地 HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="720e6-147">Click your resource group that contains hello destination HBase cluster.</span></span> <span data-ttu-id="720e6-148">這是您指定當您使用 hello 資源管理員範本 toocreate hello 環境的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="720e6-148">This is hello resource group that you specified when you used hello Resource Manager template toocreate hello environment.</span></span> <span data-ttu-id="720e6-149">您可以使用 hello 篩選 toonarrow hello 清單中。</span><span class="sxs-lookup"><span data-stu-id="720e6-149">You can use hello filter toonarrow down hello list.</span></span> <span data-ttu-id="720e6-150">您可以看到包含 hello 兩個虛擬網路資源的清單。</span><span class="sxs-lookup"><span data-stu-id="720e6-150">You can see a list of resources that contains hello two virtual networks.</span></span>
4. <span data-ttu-id="720e6-151">按一下 hello 包含 hello 目的地 HBase 叢集的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="720e6-151">Click hello virtual network that contains hello destination HBase cluster.</span></span> <span data-ttu-id="720e6-152">例如，按一下 [xxxx-vnet2]。</span><span class="sxs-lookup"><span data-stu-id="720e6-152">For example, click **xxxx-vnet2**.</span></span> <span data-ttu-id="720e6-153">您可以看到名稱開頭為 **nic-zookeepermode-** 的三個裝置。</span><span class="sxs-lookup"><span data-stu-id="720e6-153">You can see three devices with names that start with **nic-zookeepermode-**.</span></span> <span data-ttu-id="720e6-154">這些裝置是 hello 三動物園管理員 Vm。</span><span class="sxs-lookup"><span data-stu-id="720e6-154">Those devices are hello three ZooKeeper VMs.</span></span>
5. <span data-ttu-id="720e6-155">按一下其中一個 hello 動物園管理員 Vm。</span><span class="sxs-lookup"><span data-stu-id="720e6-155">Click one of hello ZooKeeper VMs.</span></span>
6. <span data-ttu-id="720e6-156">按一下 [IP 組態]。</span><span class="sxs-lookup"><span data-stu-id="720e6-156">Click **IP configurations**.</span></span>
7. <span data-ttu-id="720e6-157">按一下**ipConfig1**從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="720e6-157">Click **ipConfig1** from hello list.</span></span>
8. <span data-ttu-id="720e6-158">按一下**靜態**，記下 hello 實際 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="720e6-158">Click **Static**, and write down hello actual IP address.</span></span> <span data-ttu-id="720e6-159">當您執行 hello 指令碼動作 tooenable 複寫時，您將需要 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="720e6-159">You will need hello IP address when you run hello script action tooenable replication.</span></span>

  ![HDInsight HBase 複寫 ZooKeeper 靜態 IP](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. <span data-ttu-id="720e6-161">針對 hello 其他兩個動物園管理員節點重複步驟 6 tooset hello 靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="720e6-161">Repeat step 6 tooset hello static IP address for hello other two ZooKeeper nodes.</span></span>

<span data-ttu-id="720e6-162">Hello 跨 VNet 案例中，您必須使用 hello **ip**時呼叫 hello 切換**hdi_enable_replication.sh**指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="720e6-162">For hello cross-VNet scenario, you must use hello **-ip** switch when calling hello **hdi_enable_replication.sh** script action.</span></span>

### <a name="configure-two-virtual-networks-in-two-different-regions"></a><span data-ttu-id="720e6-163">在兩個不同區域中設定兩個虛擬網路</span><span class="sxs-lookup"><span data-stu-id="720e6-163">Configure two virtual networks in two different regions</span></span>

<span data-ttu-id="720e6-164">按一下下列映像 toocreate 兩個虛擬網路在兩個不同區域中的 hello。</span><span class="sxs-lookup"><span data-stu-id="720e6-164">Click hello following image toocreate two virtual networks in two different regions.</span></span> <span data-ttu-id="720e6-165">hello 範本會儲存在公用 Azure Blob 容器。</span><span class="sxs-lookup"><span data-stu-id="720e6-165">hello template is stored in a public Azure Blob container.</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

<span data-ttu-id="720e6-166">建立 hello 兩個虛擬網路之間的 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="720e6-166">Create a VPN gateway between hello two virtual networks.</span></span> <span data-ttu-id="720e6-167">如需指示，請參閱[建立具有站對站連線的 VNet](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="720e6-167">For instructions, see [Create a VNet with a site-to-site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span></span>

<span data-ttu-id="720e6-168">對 HBase 複寫會使用 hello 動物園管理員 Vm 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="720e6-168">HBase replication uses IP addresses of hello ZooKeeper VMs.</span></span> <span data-ttu-id="720e6-169">您必須設定為 hello 目的地 HBase 動物園管理員節點的靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="720e6-169">You must configure static IP addresses for hello destination HBase ZooKeeper nodes.</span></span> <span data-ttu-id="720e6-170">tooconfigure 靜態 IP，請參閱本文中的 hello"中的設定兩個虛擬網路 hello 相同區域 」 一節。</span><span class="sxs-lookup"><span data-stu-id="720e6-170">tooconfigure static IP, see hello "Configure two virtual networks in hello same region" section in this article.</span></span>

<span data-ttu-id="720e6-171">Hello 跨 VNet 案例中，您必須使用 hello **ip**時呼叫 hello 切換**hdi_enable_replication.sh**指令碼動作。</span><span class="sxs-lookup"><span data-stu-id="720e6-171">For hello cross-VNet scenario, you must use hello **-ip** switch when calling hello **hdi_enable_replication.sh** script action.</span></span>

## <a name="load-test-data"></a><span data-ttu-id="720e6-172">載入測試資料</span><span class="sxs-lookup"><span data-stu-id="720e6-172">Load test data</span></span>

<span data-ttu-id="720e6-173">當您複製的叢集時，您必須指定 hello 資料表 tooreplicate。</span><span class="sxs-lookup"><span data-stu-id="720e6-173">When you replicate a cluster, you must specify hello tables tooreplicate.</span></span> <span data-ttu-id="720e6-174">在本節中，您會將一些資料載入 hello 來源叢集。</span><span class="sxs-lookup"><span data-stu-id="720e6-174">In this section, you will load some data into hello source cluster.</span></span> <span data-ttu-id="720e6-175">在 hello 下一步 區段中，您將啟用 hello 兩個叢集之間的複寫。</span><span class="sxs-lookup"><span data-stu-id="720e6-175">In hello next section, you will enable replication between hello two clusters.</span></span>

<span data-ttu-id="720e6-176">請依照下列中的 hello 指示[HBase 教學課程： 開始 linux HDInsight 中的 Hadoop 使用 Apache HBase](hdinsight-hbase-tutorial-get-started-linux.md) toocreate**連絡人**資料表，並將某些資料插入 hello 資料表。</span><span class="sxs-lookup"><span data-stu-id="720e6-176">Follow hello instructions in [HBase tutorial: Get started using Apache HBase with Linux-based Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) toocreate a **Contacts** table and insert some data into hello table.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="720e6-177">啟用複寫</span><span class="sxs-lookup"><span data-stu-id="720e6-177">Enable replication</span></span>

<span data-ttu-id="720e6-178">hello 下列步驟顯示如何 toocall hello hello Azure 入口網站從指令碼動作指令碼。</span><span class="sxs-lookup"><span data-stu-id="720e6-178">hello following steps show how toocall hello script action script from hello Azure portal.</span></span> <span data-ttu-id="720e6-179">使用 Azure PowerShell 及 hello Azure 命令列介面 (CLI) 執行指令碼動作，請參閱[使用指令碼動作以自訂 Linux 為基礎的 HDInsight 叢集](hdinsight-hadoop-customize-cluster-linux.md)。</span><span class="sxs-lookup"><span data-stu-id="720e6-179">For running a script action by using Azure PowerShell and hello Azure command-line interface (CLI), see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="720e6-180">**從 Azure 入口網站 hello tooenable HBase 複寫**</span><span class="sxs-lookup"><span data-stu-id="720e6-180">**tooenable HBase replication from hello Azure portal**</span></span>

1. <span data-ttu-id="720e6-181">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="720e6-181">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="720e6-182">開啟 hello 來源 HBase 叢集。</span><span class="sxs-lookup"><span data-stu-id="720e6-182">Open hello source HBase cluster.</span></span>
3. <span data-ttu-id="720e6-183">從 hello 叢集功能表上，按一下 **指令碼動作**。</span><span class="sxs-lookup"><span data-stu-id="720e6-183">From hello cluster menu, click **Script Actions**.</span></span>
4. <span data-ttu-id="720e6-184">按一下**提交新**從 hello hello 刀鋒視窗的頂端。</span><span class="sxs-lookup"><span data-stu-id="720e6-184">Click **Submit New** from hello top of hello blade.</span></span>
5. <span data-ttu-id="720e6-185">選取或輸入 hello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="720e6-185">Select or enter hello following information:</span></span>

  - <span data-ttu-id="720e6-186">**名稱**：輸入「啟用複寫」。</span><span class="sxs-lookup"><span data-stu-id="720e6-186">**Name**: Enter **Enable replication**.</span></span>
  - <span data-ttu-id="720e6-187">**Bash 指令碼 URL**：輸入 **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**。</span><span class="sxs-lookup"><span data-stu-id="720e6-187">**Bash Script URL**: Enter **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span></span>
  - <span data-ttu-id="720e6-188">**前端**︰已選取。</span><span class="sxs-lookup"><span data-stu-id="720e6-188">**Head**: Selected.</span></span> <span data-ttu-id="720e6-189">清除 hello 其他節點型別。</span><span class="sxs-lookup"><span data-stu-id="720e6-189">Clear hello other node types.</span></span>
  - <span data-ttu-id="720e6-190">**參數**: hello 下列範例參數啟用所有 hello 現有資料表的複寫，並且所有的 hello 資料複製 hello 來源叢集 toohello 目的地叢集：</span><span class="sxs-lookup"><span data-stu-id="720e6-190">**Parameters**: hello following sample parameters enable replication for all hello existing tables and copy all hello data from hello source cluster toohello destination cluster:</span></span>

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. <span data-ttu-id="720e6-191">按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="720e6-191">Click **Create**.</span></span> <span data-ttu-id="720e6-192">hello 指令碼可能需要一些時間，特別是當 hello-copydata 引數用。</span><span class="sxs-lookup"><span data-stu-id="720e6-192">hello script can take some time, especially when hello -copydata argument is used.</span></span>

<span data-ttu-id="720e6-193">必要的引數︰</span><span class="sxs-lookup"><span data-stu-id="720e6-193">Required arguments:</span></span>

|<span data-ttu-id="720e6-194">名稱</span><span class="sxs-lookup"><span data-stu-id="720e6-194">Name</span></span>|<span data-ttu-id="720e6-195">說明</span><span class="sxs-lookup"><span data-stu-id="720e6-195">Description</span></span>|
|----|-----------|
|<span data-ttu-id="720e6-196">-s, --src-cluster</span><span class="sxs-lookup"><span data-stu-id="720e6-196">-s, --src-cluster</span></span> | <span data-ttu-id="720e6-197">指定 hello hello 來源 HBase 叢集 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="720e6-197">Specify hello DNS name of hello source HBase cluster.</span></span> <span data-ttu-id="720e6-198">例如：-s hbsrccluster, --src-cluster=hbsrccluster</span><span class="sxs-lookup"><span data-stu-id="720e6-198">For example: -s hbsrccluster, --src-cluster=hbsrccluster</span></span> |
|<span data-ttu-id="720e6-199">-d, --dst-cluster</span><span class="sxs-lookup"><span data-stu-id="720e6-199">-d, --dst-cluster</span></span> | <span data-ttu-id="720e6-200">指定 hello hello 目的地 （複本） HBase 叢集 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="720e6-200">Specify hello DNS name of hello destination (replica) HBase cluster.</span></span> <span data-ttu-id="720e6-201">例如：-s dsthbcluster, --src-cluster=dsthbcluster</span><span class="sxs-lookup"><span data-stu-id="720e6-201">For example: -s dsthbcluster, --src-cluster=dsthbcluster</span></span> |
|<span data-ttu-id="720e6-202">-sp, --src-ambari-password</span><span class="sxs-lookup"><span data-stu-id="720e6-202">-sp, --src-ambari-password</span></span> | <span data-ttu-id="720e6-203">指定在 hello 來源 HBase 叢集 Ambari hello 系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="720e6-203">Specify hello admin password for Ambari on hello source HBase cluster.</span></span> |
|<span data-ttu-id="720e6-204">-dp, --dst-ambari-password</span><span class="sxs-lookup"><span data-stu-id="720e6-204">-dp, --dst-ambari-password</span></span> | <span data-ttu-id="720e6-205">指定在 hello 目的地 HBase 叢集上 Ambari hello 系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="720e6-205">Specify hello admin password for Ambari on hello destination HBase cluster.</span></span>|

<span data-ttu-id="720e6-206">選擇性的引數︰</span><span class="sxs-lookup"><span data-stu-id="720e6-206">Optional arguments:</span></span>

|<span data-ttu-id="720e6-207">名稱</span><span class="sxs-lookup"><span data-stu-id="720e6-207">Name</span></span>|<span data-ttu-id="720e6-208">說明</span><span class="sxs-lookup"><span data-stu-id="720e6-208">Description</span></span>|
|----|-----------|
|<span data-ttu-id="720e6-209">-su, --src-ambari-user</span><span class="sxs-lookup"><span data-stu-id="720e6-209">-su, --src-ambari-user</span></span> | <span data-ttu-id="720e6-210">指定在 hello 來源 HBase 叢集 Ambari hello 管理員使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="720e6-210">Specify hello admin username for Ambari on hello source HBase cluster.</span></span> <span data-ttu-id="720e6-211">hello 預設值是**admin**。</span><span class="sxs-lookup"><span data-stu-id="720e6-211">hello default value is **admin**.</span></span> |
|<span data-ttu-id="720e6-212">-du, --dst-ambari-user</span><span class="sxs-lookup"><span data-stu-id="720e6-212">-du, --dst-ambari-user</span></span> | <span data-ttu-id="720e6-213">指定在 hello 目的地 HBase 叢集上 Ambari hello 管理員使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="720e6-213">Specify hello admin username for Ambari on hello destination HBase cluster.</span></span> <span data-ttu-id="720e6-214">hello 預設值是**admin**。</span><span class="sxs-lookup"><span data-stu-id="720e6-214">hello default value is **admin**.</span></span> |
|<span data-ttu-id="720e6-215">-t, --table-list</span><span class="sxs-lookup"><span data-stu-id="720e6-215">-t, --table-list</span></span> | <span data-ttu-id="720e6-216">指定 hello 資料表 toobe 複寫。</span><span class="sxs-lookup"><span data-stu-id="720e6-216">Specify hello tables toobe replicated.</span></span> <span data-ttu-id="720e6-217">例如：--table-list="table1;table2;table3"。</span><span class="sxs-lookup"><span data-stu-id="720e6-217">For example: --table-list="table1;table2;table3".</span></span> <span data-ttu-id="720e6-218">如果您未指定資料表，則會複寫所有現有的 HBase 資料表。</span><span class="sxs-lookup"><span data-stu-id="720e6-218">If you don't specify tables, all existing HBase tables are replicated.</span></span>|
|<span data-ttu-id="720e6-219">-m, --machine</span><span class="sxs-lookup"><span data-stu-id="720e6-219">-m, --machine</span></span> | <span data-ttu-id="720e6-220">指定 hello hello 指令碼動作執行所在的前端節點。</span><span class="sxs-lookup"><span data-stu-id="720e6-220">Specify hello head node where hello script action will run.</span></span> <span data-ttu-id="720e6-221">hn1 或 hn0 hello 值。</span><span class="sxs-lookup"><span data-stu-id="720e6-221">hello value is either hn1 or hn0.</span></span> <span data-ttu-id="720e6-222">由於 hn0 通常較忙碌，建議您使用 hn1。</span><span class="sxs-lookup"><span data-stu-id="720e6-222">Because hn0 is usually busier, we recommend using hn1.</span></span> <span data-ttu-id="720e6-223">如果您從 hello HDInsight 入口網站或 Azure PowerShell 指令碼動作執行 hello $0 指令碼，您可以使用此選項。</span><span class="sxs-lookup"><span data-stu-id="720e6-223">You use this option when you're running hello $0 script as a script action from hello HDInsight portal or Azure PowerShell.</span></span>|
|<span data-ttu-id="720e6-224">-ip</span><span class="sxs-lookup"><span data-stu-id="720e6-224">-ip</span></span> | <span data-ttu-id="720e6-225">當您啟用兩個虛擬網路之間的複寫時，需要這個引數。</span><span class="sxs-lookup"><span data-stu-id="720e6-225">This argument is required when you're enabling replication between two virtual networks.</span></span> <span data-ttu-id="720e6-226">這個引數做為參數 toouse hello 靜態 Ip 的動物園管理員來自叢集的節點複本而不是 FQDN 名稱。</span><span class="sxs-lookup"><span data-stu-id="720e6-226">This argument acts as a switch toouse hello static IPs of ZooKeeper nodes from replica clusters instead of FQDN names.</span></span> <span data-ttu-id="720e6-227">hello 靜態 Ip 需要 toobe 預先設定的啟用複寫之前。</span><span class="sxs-lookup"><span data-stu-id="720e6-227">hello static IPs need toobe preconfigured before you enable replication.</span></span> |
|<span data-ttu-id="720e6-228">-cp, -copydata</span><span class="sxs-lookup"><span data-stu-id="720e6-228">-cp, -copydata</span></span> | <span data-ttu-id="720e6-229">啟用 hello hello 已啟用複寫的資料表上的現有資料移轉的功能。</span><span class="sxs-lookup"><span data-stu-id="720e6-229">Enable hello migration of existing data on hello tables where replication is enabled.</span></span> |
|<span data-ttu-id="720e6-230">-rpm, -replicate-phoenix-meta</span><span class="sxs-lookup"><span data-stu-id="720e6-230">-rpm, -replicate-phoenix-meta</span></span> | <span data-ttu-id="720e6-231">在 Phoenix 系統資料表上啟用複寫。</span><span class="sxs-lookup"><span data-stu-id="720e6-231">Enable replication on Phoenix system tables.</span></span> <br><br><span data-ttu-id="720e6-232">*請謹慎使用此選項。*</span><span class="sxs-lookup"><span data-stu-id="720e6-232">*Use this option with caution.*</span></span> <span data-ttu-id="720e6-233">建議您在使用此指令碼前，於複本叢集上重新建立 Phoenix 資料表。</span><span class="sxs-lookup"><span data-stu-id="720e6-233">We recommend that you re-create Phoenix tables on replica clusters before you use this script.</span></span> |
|<span data-ttu-id="720e6-234">-h, --help</span><span class="sxs-lookup"><span data-stu-id="720e6-234">-h, --help</span></span> | <span data-ttu-id="720e6-235">顯示使用資訊。</span><span class="sxs-lookup"><span data-stu-id="720e6-235">Display usage information.</span></span> |

<span data-ttu-id="720e6-236">hello hello print_usage() 區段[指令碼](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh)提供參數的詳細的說明。</span><span class="sxs-lookup"><span data-stu-id="720e6-236">hello print_usage() section of hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) provides a detailed explanation of parameters.</span></span>

<span data-ttu-id="720e6-237">Hello 指令碼動作是成功之後部署，您可以使用 SSH tooconnect toohello 目的地 HBase 叢集，並確認已複寫 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="720e6-237">After hello script action is successfully deployed, you can use SSH tooconnect toohello destination HBase cluster, and verify hello data has been replicated.</span></span>

### <a name="replication-scenarios"></a><span data-ttu-id="720e6-238">複寫案例</span><span class="sxs-lookup"><span data-stu-id="720e6-238">Replication scenarios</span></span>

<span data-ttu-id="720e6-239">hello 下列清單顯示一些一般使用案例和其參數設定：</span><span class="sxs-lookup"><span data-stu-id="720e6-239">hello following list shows you some general usage cases and their parameter settings:</span></span>

- <span data-ttu-id="720e6-240">**Hello 兩個叢集之間的所有資料表上啟用複寫**。</span><span class="sxs-lookup"><span data-stu-id="720e6-240">**Enable replication on all tables between hello two clusters**.</span></span> <span data-ttu-id="720e6-241">此案例不需要 hello 複製/hello 資料表上的現有資料移轉，而且不會使用 in Phoenix 資料表。</span><span class="sxs-lookup"><span data-stu-id="720e6-241">This scenario does not require hello copy/migration of existing data on hello tables, and it does not use Phoenix tables.</span></span> <span data-ttu-id="720e6-242">使用下列參數的 hello:</span><span class="sxs-lookup"><span data-stu-id="720e6-242">Use hello following parameters:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- <span data-ttu-id="720e6-243">**在特定資料表上啟用複寫**。</span><span class="sxs-lookup"><span data-stu-id="720e6-243">**Enable replication on specific tables**.</span></span> <span data-ttu-id="720e6-244">使用下列參數 tooenable 複寫 table1、 table2 和 table3 hello:</span><span class="sxs-lookup"><span data-stu-id="720e6-244">Use hello following parameters tooenable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- <span data-ttu-id="720e6-245">**特定資料表上啟用複寫，而且複製 hello 現有資料**。</span><span class="sxs-lookup"><span data-stu-id="720e6-245">**Enable replication on specific tables and copy hello existing data**.</span></span> <span data-ttu-id="720e6-246">使用下列參數 tooenable 複寫 table1、 table2 和 table3 hello:</span><span class="sxs-lookup"><span data-stu-id="720e6-246">Use hello following parameters tooenable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- <span data-ttu-id="720e6-247">**與從來源 toodestination 複寫 in phoenix 中繼資料的所有資料表上啟用複寫**。</span><span class="sxs-lookup"><span data-stu-id="720e6-247">**Enable replication on all tables with replicating phoenix metadata from source toodestination**.</span></span> <span data-ttu-id="720e6-248">Phoenix 中繼資料複寫並不完美，應謹慎啟用。</span><span class="sxs-lookup"><span data-stu-id="720e6-248">Phoenix metadata replication is not perfect and should be enabled with caution.</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a><span data-ttu-id="720e6-249">複製並移轉資料</span><span class="sxs-lookup"><span data-stu-id="720e6-249">Copy and migrate data</span></span>

<span data-ttu-id="720e6-250">啟用複寫後，有兩個用來複製/移轉資料的個別指令碼動作指令碼：</span><span class="sxs-lookup"><span data-stu-id="720e6-250">There are two separate script action scripts for copying/migrating data after replication is enabled:</span></span>

- <span data-ttu-id="720e6-251">[用於小型資料表的指令碼](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh)（在大小和整體複製數 gb 是預期的 toofinish 中少於一小時）</span><span class="sxs-lookup"><span data-stu-id="720e6-251">[Script for small tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (a few gigabytes in size, and overall copy is expected toofinish in less than one hour)</span></span>

- <span data-ttu-id="720e6-252">[對於大型資料表的指令碼](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh)（預期 tootake 超過一小時 toocopy）</span><span class="sxs-lookup"><span data-stu-id="720e6-252">[Script for large tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (expected tootake longer than one hour toocopy)</span></span>

<span data-ttu-id="720e6-253">您可以遵循相同的程序中的 hello[啟用複寫](#enable-replication)toocall hello 指令碼動作以 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="720e6-253">You can follow hello same procedure in [Enable replication](#enable-replication) toocall hello script action with hello following parameters:</span></span>

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

<span data-ttu-id="720e6-254">hello hello print_usage() 區段[指令碼](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh)提供參數的詳細的描述。</span><span class="sxs-lookup"><span data-stu-id="720e6-254">hello print_usage() section of hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) provides a detailed description of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="720e6-255">案例</span><span class="sxs-lookup"><span data-stu-id="720e6-255">Scenarios</span></span>

- <span data-ttu-id="720e6-256">**針對到目前為止 (目前時間戳記) 所有已編輯的資料列複製特定資料表 (test1、test2 和 test3)**：</span><span class="sxs-lookup"><span data-stu-id="720e6-256">**Copy specific tables (test1, test2, and test3) for all rows edited till now (current time stamp)**:</span></span>

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  <span data-ttu-id="720e6-257">或</span><span class="sxs-lookup"><span data-stu-id="720e6-257">or</span></span>

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- <span data-ttu-id="720e6-258">**以指定時間範圍複製特定資料表**：</span><span class="sxs-lookup"><span data-stu-id="720e6-258">**Copy specific tables with specified time range**:</span></span>

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a><span data-ttu-id="720e6-259">停用複寫</span><span class="sxs-lookup"><span data-stu-id="720e6-259">Disable replication</span></span>

<span data-ttu-id="720e6-260">使用位於另一個指令碼動作指令碼 toodisable 複寫[GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh)。</span><span class="sxs-lookup"><span data-stu-id="720e6-260">toodisable replication, you use another script action script located at [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span></span> <span data-ttu-id="720e6-261">您可以遵循相同的程序中的 hello[啟用複寫](#enable-replication)toocall hello 指令碼動作以 hello 下列參數：</span><span class="sxs-lookup"><span data-stu-id="720e6-261">You can follow hello same procedure in [Enable replication](#enable-replication) toocall hello script action with hello following parameters:</span></span>

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

<span data-ttu-id="720e6-262">hello hello print_usage() 區段[指令碼](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh)提供參數的詳細的說明。</span><span class="sxs-lookup"><span data-stu-id="720e6-262">hello print_usage() section of hello [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) provides a detailed explanation of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="720e6-263">案例</span><span class="sxs-lookup"><span data-stu-id="720e6-263">Scenarios</span></span>

- <span data-ttu-id="720e6-264">**停用所有資料表上的複寫**：</span><span class="sxs-lookup"><span data-stu-id="720e6-264">**Disable replication on all tables**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  <span data-ttu-id="720e6-265">或</span><span class="sxs-lookup"><span data-stu-id="720e6-265">or</span></span>

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- <span data-ttu-id="720e6-266">**停用特定資料表 (table1、table2 和 table3) 上的複寫**：</span><span class="sxs-lookup"><span data-stu-id="720e6-266">**Disable replication on specified tables (table1, table2, and table3)**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a><span data-ttu-id="720e6-267">後續步驟</span><span class="sxs-lookup"><span data-stu-id="720e6-267">Next steps</span></span>

<span data-ttu-id="720e6-268">在本教學課程中，您學到如何 tooconfigure HBase 複寫，跨兩個資料中心。</span><span class="sxs-lookup"><span data-stu-id="720e6-268">In this tutorial, you learned how tooconfigure HBase replication across two datacenters.</span></span> <span data-ttu-id="720e6-269">toolearn 深入了解 HDInsight 和 HBase，請參閱：</span><span class="sxs-lookup"><span data-stu-id="720e6-269">toolearn more about HDInsight and HBase, see:</span></span>

* <span data-ttu-id="720e6-270">[開始使用 HDInsight 中的 Apache HBase][hdinsight-hbase-get-started]</span><span class="sxs-lookup"><span data-stu-id="720e6-270">[Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started]</span></span>
* <span data-ttu-id="720e6-271">[HDInsight HBase 概觀][hdinsight-hbase-overview]</span><span class="sxs-lookup"><span data-stu-id="720e6-271">[HDInsight HBase overview][hdinsight-hbase-overview]</span></span>
* <span data-ttu-id="720e6-272">[在 Azure 虛擬網路上建立 HBase 叢集][hdinsight-hbase-provision-vnet]</span><span class="sxs-lookup"><span data-stu-id="720e6-272">[Create HBase clusters in Azure Virtual Network][hdinsight-hbase-provision-vnet]</span></span>
* <span data-ttu-id="720e6-273">[使用 HBase 分析即時 Twitter 情緒][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="720e6-273">[Analyze real-time Twitter sentiment with HBase][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="720e6-274">[在 HDInsight (Hadoop) 中使用 Storm 和 HBase 分析感應器資料][hdinsight-sensor-data]</span><span class="sxs-lookup"><span data-stu-id="720e6-274">[Analyzing sensor data with Storm and HBase in HDInsight (Hadoop)][hdinsight-sensor-data]</span></span>

[hdinsight-hbase-geo-replication-vnet]: hdinsight-hbase-geo-replication-configure-vnets.md
[hdinsight-hbase-geo-replication-dns]: ../hdinsight-hbase-geo-replication-configure-VNet.md


[img-vnet-diagram]: ./media/hdinsight-hbase-geo-replication/HDInsight.HBase.Replication.Network.diagram.png

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[hdinsight-sensor-data]: hdinsight-storm-sensor-data-analysis.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
