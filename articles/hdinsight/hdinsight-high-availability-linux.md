---
title: "Hadoop-Azure HDInsight 的 aaaHigh 可用性 |Microsoft 文件"
description: "了解如何使用額外的前端節點，讓 HDInsight 叢集可以提高可靠性和可用性。 了解如何影響 Hadoop 服務，例如 Ambari 和 Hive，以及如何 tooindividually 連接使用 SSH tooeach 前端節點。"
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
keywords: "hadoop 高可用性"
ms.assetid: 99c9f59c-cf6b-4529-99d1-bf060435e8d4
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 07/28/2017
ms.author: larryfr
ms.openlocfilehash: 9ff62afe6b63b241cb984225233157219f8d7411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="0534a-105">HDInsight 上 Hadoop 叢集的可用性和可靠性</span><span class="sxs-lookup"><span data-stu-id="0534a-105">Availability and reliability of Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="0534a-106">HDInsight 叢集提供兩個前端節點 tooincrease hello 可用性和可靠性的 Hadoop 服務及執行的工作。</span><span class="sxs-lookup"><span data-stu-id="0534a-106">HDInsight clusters provide two head nodes tooincrease hello availability and reliability of Hadoop services and jobs running.</span></span>

<span data-ttu-id="0534a-107">Hadoop 藉由在叢集中的多個節點間複寫服務和資料，以達到高可用性和可靠性。</span><span class="sxs-lookup"><span data-stu-id="0534a-107">Hadoop achieves high availability and reliability by replicating services and data across multiple nodes in a cluster.</span></span> <span data-ttu-id="0534a-108">不過 Hadoop 的標準散佈功能通常只能有一個前端節點。</span><span class="sxs-lookup"><span data-stu-id="0534a-108">However standard distributions of Hadoop typically have only a single head node.</span></span> <span data-ttu-id="0534a-109">Hello 單一前端節點的任何中斷可能會導致 hello 叢集 toostop 工作。</span><span class="sxs-lookup"><span data-stu-id="0534a-109">Any outage of hello single head node can cause hello cluster toostop working.</span></span> <span data-ttu-id="0534a-110">HDInsight 提供兩個 headnodes tooimprove Hadoop 的可用性和可靠性。</span><span class="sxs-lookup"><span data-stu-id="0534a-110">HDInsight provides two headnodes tooimprove Hadoop's availability and reliability.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0534a-111">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="0534a-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0534a-112">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="0534a-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="availability-and-reliability-of-nodes"></a><span data-ttu-id="0534a-113">節點的可用性和可靠性</span><span class="sxs-lookup"><span data-stu-id="0534a-113">Availability and reliability of nodes</span></span>

<span data-ttu-id="0534a-114">使用 Azure 虛擬機器在 HDInsight 叢集中的節點實作。</span><span class="sxs-lookup"><span data-stu-id="0534a-114">Nodes in an HDInsight cluster are implemented using Azure Virtual Machines.</span></span> <span data-ttu-id="0534a-115">hello 下列各節討論 hello HDInsight 搭配使用的個別節點型別。</span><span class="sxs-lookup"><span data-stu-id="0534a-115">hello following sections discuss hello individual node types used with HDInsight.</span></span> 

> [!NOTE]
> <span data-ttu-id="0534a-116">並非所有的節點類型都可用於某個叢集類型。</span><span class="sxs-lookup"><span data-stu-id="0534a-116">Not all node types are used for a cluster type.</span></span> <span data-ttu-id="0534a-117">例如，Hadoop 叢集類型就不會有任何 Nimbus 節點。</span><span class="sxs-lookup"><span data-stu-id="0534a-117">For example, a Hadoop cluster type does not have any Nimbus nodes.</span></span> <span data-ttu-id="0534a-118">如需有關節點 HDInsight 叢集類型所使用的詳細資訊，請參閱 hello 叢集類型 > 一節的 hello [HDInsight 叢集建立 Linux Hadoop](hdinsight-hadoop-provision-linux-clusters.md#cluster-types)文件。</span><span class="sxs-lookup"><span data-stu-id="0534a-118">For more information on nodes used by HDInsight cluster types, see hello Cluster types section of hello [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.</span></span>

### <a name="head-nodes"></a><span data-ttu-id="0534a-119">前端節點</span><span class="sxs-lookup"><span data-stu-id="0534a-119">Head nodes</span></span>

<span data-ttu-id="0534a-120">tooensure 高可用性的 Hadoop 服務，HDInsight 提供兩個前端節點。</span><span class="sxs-lookup"><span data-stu-id="0534a-120">tooensure high availability of Hadoop services, HDInsight provides two head nodes.</span></span> <span data-ttu-id="0534a-121">這兩個前端節點會同時為作用中和 hello HDInsight 叢集內執行。</span><span class="sxs-lookup"><span data-stu-id="0534a-121">Both head nodes are active and running within hello HDInsight cluster simultaneously.</span></span> <span data-ttu-id="0534a-122">某些服務，例如 HDFS 或 YARN，在任何給定的時間僅能在其中一個前端節點上為「作用中」。</span><span class="sxs-lookup"><span data-stu-id="0534a-122">Some services, such as HDFS or YARN, are only 'active' on one head node at any given time.</span></span> <span data-ttu-id="0534a-123">例如 HiveServer2 或 Hive 中繼存放區的其他服務為 hello 在兩個前端節點上使用相同的時間。</span><span class="sxs-lookup"><span data-stu-id="0534a-123">Other services such as HiveServer2 or Hive MetaStore are active on both head nodes at hello same time.</span></span>

<span data-ttu-id="0534a-124">前端節點 （和 HDInsight 中的其他節點） 有數值的 hello 節點的 hello 主機名稱的一部分。</span><span class="sxs-lookup"><span data-stu-id="0534a-124">Head nodes (and other nodes in HDInsight) have a numeric value as part of hello hostname of hello node.</span></span> <span data-ttu-id="0534a-125">例如，`hn0-CLUSTERNAME` 或 `hn4-CLUSTERNAME`。</span><span class="sxs-lookup"><span data-stu-id="0534a-125">For example, `hn0-CLUSTERNAME` or `hn4-CLUSTERNAME`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0534a-126">請勿將 hello 數值關聯具有一個節點是主要或次要。</span><span class="sxs-lookup"><span data-stu-id="0534a-126">Do not associate hello numeric value with whether a node is primary or secondary.</span></span> <span data-ttu-id="0534a-127">hello 數值為存在 tooprovide 每個節點的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="0534a-127">hello numeric value is only present tooprovide a unique name for each node.</span></span>

### <a name="nimbus-nodes"></a><span data-ttu-id="0534a-128">Nimbus 節點</span><span class="sxs-lookup"><span data-stu-id="0534a-128">Nimbus Nodes</span></span>

<span data-ttu-id="0534a-129">Nimbus 節點可用於 Storm 叢集。</span><span class="sxs-lookup"><span data-stu-id="0534a-129">Nimbus nodes are available with Storm clusters.</span></span> <span data-ttu-id="0534a-130">hello Nimbus 節點會提供類似功能 toohello Hadoop JobTracker 散發，並監視背景工作節點之間的處理。</span><span class="sxs-lookup"><span data-stu-id="0534a-130">hello Nimbus nodes provide similar functionality toohello Hadoop JobTracker by distributing and monitoring processing across worker nodes.</span></span> <span data-ttu-id="0534a-131">HDInsight 為 Storm 叢集提供兩個 Nimbus 節點</span><span class="sxs-lookup"><span data-stu-id="0534a-131">HDInsight provides two Nimbus nodes for Storm clusters</span></span>

### <a name="zookeeper-nodes"></a><span data-ttu-id="0534a-132">Zookeeper 節點</span><span class="sxs-lookup"><span data-stu-id="0534a-132">Zookeeper nodes</span></span>

<span data-ttu-id="0534a-133">[ZooKeeper](http://zookeeper.apache.org/) 節點用於前端節點上主要服務的前置選擇。</span><span class="sxs-lookup"><span data-stu-id="0534a-133">[ZooKeeper](http://zookeeper.apache.org/) nodes are used for leader election of master services on head nodes.</span></span> <span data-ttu-id="0534a-134">它們也是使用的 tooinsure 服務、 資料 （背景工作角色） 節點，以及閘道知道哪些主要服務為作用中的前端節點。</span><span class="sxs-lookup"><span data-stu-id="0534a-134">They are also used tooinsure that services, data (worker) nodes, and gateways know which head node a master service is active on.</span></span> <span data-ttu-id="0534a-135">根據預設，HDInsight 會提供三個 ZooKeeper 節點。</span><span class="sxs-lookup"><span data-stu-id="0534a-135">By default, HDInsight provides three ZooKeeper nodes.</span></span>

### <a name="worker-nodes"></a><span data-ttu-id="0534a-136">背景工作節點</span><span class="sxs-lookup"><span data-stu-id="0534a-136">Worker nodes</span></span>

<span data-ttu-id="0534a-137">背景工作節點執行 hello 實際的資料分析工作時送出的 toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="0534a-137">Worker nodes perform hello actual data analysis when a job is submitted toohello cluster.</span></span> <span data-ttu-id="0534a-138">如果背景工作節點失敗，它的執行狀況的 hello 工作都是送出的 tooanother 背景工作節點。</span><span class="sxs-lookup"><span data-stu-id="0534a-138">If a worker node fails, hello task that it was performing is submitted tooanother worker node.</span></span> <span data-ttu-id="0534a-139">根據預設，HDInsight 會建立四個背景工作節點。</span><span class="sxs-lookup"><span data-stu-id="0534a-139">By default, HDInsight creates four worker nodes.</span></span> <span data-ttu-id="0534a-140">在和建立叢集之後您可以變更指定這個數字 toosuit 您的需求。</span><span class="sxs-lookup"><span data-stu-id="0534a-140">You can change this number toosuit your needs both during and after cluster creation.</span></span>

### <a name="edge-node"></a><span data-ttu-id="0534a-141">邊緣節點</span><span class="sxs-lookup"><span data-stu-id="0534a-141">Edge node</span></span>

<span data-ttu-id="0534a-142">邊緣節點不會主動參與 hello 叢集內的資料分析。</span><span class="sxs-lookup"><span data-stu-id="0534a-142">An edge node does not actively participate in data analysis within hello cluster.</span></span> <span data-ttu-id="0534a-143">而是由開發人員或資料科學家在使用 Hadoop 時搭配使用。</span><span class="sxs-lookup"><span data-stu-id="0534a-143">It is used by developers or data scientists when working with Hadoop.</span></span> <span data-ttu-id="0534a-144">中的 hello 邊緣節點生活 hello 與 hello 相同 Azure 虛擬網路 hello 叢集中的其他節點，並可以直接存取所有其他節點。</span><span class="sxs-lookup"><span data-stu-id="0534a-144">hello edge node lives in hello same Azure Virtual Network as hello other nodes in hello cluster, and can directly access all other nodes.</span></span> <span data-ttu-id="0534a-145">可以使用 hello 邊緣節點，而不離開關鍵 Hadoop 服務或分析工作的資源。</span><span class="sxs-lookup"><span data-stu-id="0534a-145">hello edge node can be used without taking resources away from critical Hadoop services or analysis jobs.</span></span>

<span data-ttu-id="0534a-146">目前，HDInsight 上的 R 伺服器是 hello 唯一叢集類型，根據預設，提供邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="0534a-146">Currently, R Server on HDInsight is hello only cluster type that provides an edge node by default.</span></span> <span data-ttu-id="0534a-147">HDInsight 上的 R 伺服器，會使用 hello 邊緣節點本機上進行分散式處理 toohello 叢集送出之前 hello 節點測試 R 程式碼。</span><span class="sxs-lookup"><span data-stu-id="0534a-147">For R Server on HDInsight, hello edge node is used test R code locally on hello node before submitting it toohello cluster for distributed processing.</span></span>

<span data-ttu-id="0534a-148">如需使用 R 伺服器以外的叢集類型的邊緣節點資訊，請參閱 hello[使用 HDInsight 中邊緣節點](hdinsight-apps-use-edge-node.md)文件。</span><span class="sxs-lookup"><span data-stu-id="0534a-148">For information on using an edge node with cluster types other than R Server, see hello [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) document.</span></span>

## <a name="accessing-hello-nodes"></a><span data-ttu-id="0534a-149">存取 hello 節點</span><span class="sxs-lookup"><span data-stu-id="0534a-149">Accessing hello nodes</span></span>

<span data-ttu-id="0534a-150">存取 toohello 叢集 hello 透過網際網路提供透過公用閘道。</span><span class="sxs-lookup"><span data-stu-id="0534a-150">Access toohello cluster over hello internet is provided through a public gateway.</span></span> <span data-ttu-id="0534a-151">存取限制的 tooconnecting toohello 前端節點，而且 （如果有的話） hello 邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="0534a-151">Access is limited tooconnecting toohello head nodes and (if one exists) hello edge node.</span></span> <span data-ttu-id="0534a-152">存取 tooservices hello 前端節點上執行不受到具有多個前端節點。</span><span class="sxs-lookup"><span data-stu-id="0534a-152">Access tooservices running on hello head nodes is not effected by having multiple head nodes.</span></span> <span data-ttu-id="0534a-153">hello 公用閘道路由要求 toohello 前端節點裝載 hello 要求的服務。</span><span class="sxs-lookup"><span data-stu-id="0534a-153">hello public gateway routes requests toohello head node that hosts hello requested service.</span></span> <span data-ttu-id="0534a-154">例如，如果 Ambari 目前 hello 次要前端節點上裝載，hello 閘道會路由傳送 Ambari toothat 節點內送要求。</span><span class="sxs-lookup"><span data-stu-id="0534a-154">For example, if Ambari is currently hosted on hello secondary head node, hello gateway routes incoming requests for Ambari toothat node.</span></span>

<span data-ttu-id="0534a-155">443 (HTTPS)、 22 和 23 的有限的 tooport hello 公用閘道上的存取。</span><span class="sxs-lookup"><span data-stu-id="0534a-155">Access over hello public gateway is limited tooport 443 (HTTPS), 22, and 23.</span></span>

* <span data-ttu-id="0534a-156">連接埠__443__是使用的 tooaccess Ambari 和其他 web UI 或 hello 前端節點上裝載的 REST Api。</span><span class="sxs-lookup"><span data-stu-id="0534a-156">Port __443__ is used tooaccess Ambari and other web UI or REST APIs hosted on hello head nodes.</span></span>

* <span data-ttu-id="0534a-157">連接埠__22__使用的 tooaccess hello 的主要前端節點或透過 SSH 的邊緣節點。</span><span class="sxs-lookup"><span data-stu-id="0534a-157">Port __22__ is used tooaccess hello primary head node or edge node with SSH.</span></span>

* <span data-ttu-id="0534a-158">連接埠__23__是使用的 tooaccess hello 次要前端節點使用 SSH。</span><span class="sxs-lookup"><span data-stu-id="0534a-158">Port __23__ is used tooaccess hello secondary head node with SSH.</span></span> <span data-ttu-id="0534a-159">例如，`ssh username@mycluster-ssh.azurehdinsight.net`連接 toohello 主要叢集前端節點 hello 名為**mycluster**。</span><span class="sxs-lookup"><span data-stu-id="0534a-159">For example, `ssh username@mycluster-ssh.azurehdinsight.net` connects toohello primary head node of hello cluster named **mycluster**.</span></span>

<span data-ttu-id="0534a-160">如需有關如何使用 SSH 的詳細資訊，請參閱 hello[搭配使用 SSH 和 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)文件。</span><span class="sxs-lookup"><span data-stu-id="0534a-160">For more information on using SSH, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

### <a name="internal-fully-qualified-domain-names-fqdn"></a><span data-ttu-id="0534a-161">內部完整網域名稱 (FQDN)</span><span class="sxs-lookup"><span data-stu-id="0534a-161">Internal fully qualified domain names (FQDN)</span></span>

<span data-ttu-id="0534a-162">HDInsight 叢集中的節點都有內部 IP 位址及只能存取從 hello 叢集的 FQDN。</span><span class="sxs-lookup"><span data-stu-id="0534a-162">Nodes in an HDInsight cluster have an internal IP address and FQDN that can only be accessed from hello cluster.</span></span> <span data-ttu-id="0534a-163">當存取使用 hello 內部 FQDN 或 IP 位址的 hello 叢集上的服務，您應該使用 Ambari tooverify hello IP 或 FQDN toouse 存取 hello 服務時發生。</span><span class="sxs-lookup"><span data-stu-id="0534a-163">When accessing services on hello cluster using hello internal FQDN or IP address, you should use Ambari tooverify hello IP or FQDN toouse when accessing hello service.</span></span>

<span data-ttu-id="0534a-164">例如，hello 的 Oozie 服務只能執行一個前端節點，並使用 hello`oozie`從的 SSH 工作階段的命令需要 hello URL toohello 服務。</span><span class="sxs-lookup"><span data-stu-id="0534a-164">For example, hello Oozie service can only run on one head node, and using hello `oozie` command from an SSH session requires hello URL toohello service.</span></span> <span data-ttu-id="0534a-165">可以使用下列命令的 hello，從 Ambari 擷取此 URL:</span><span class="sxs-lookup"><span data-stu-id="0534a-165">This URL can be retrieved from Ambari by using hello following command:</span></span>

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

<span data-ttu-id="0534a-166">此命令會傳回下列命令，其中包含以 hello hello 內部 URL toouse 值類似 toohello`oozie`命令：</span><span class="sxs-lookup"><span data-stu-id="0534a-166">This command returns a value similar toohello following command, which contains hello internal URL toouse with hello `oozie` command:</span></span>

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

<span data-ttu-id="0534a-167">如需使用 hello Ambari REST API 的詳細資訊，請參閱[監視和管理 HDInsight 的使用 hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md)。</span><span class="sxs-lookup"><span data-stu-id="0534a-167">For more information on working with hello Ambari REST API, see [Monitor and Manage HDInsight using hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

### <a name="accessing-other-node-types"></a><span data-ttu-id="0534a-168">存取其他節點類型</span><span class="sxs-lookup"><span data-stu-id="0534a-168">Accessing other node types</span></span>

<span data-ttu-id="0534a-169">您可以連接都無法直接存取 over hello 網際網路使用下列方法 hello 的 toonodes:</span><span class="sxs-lookup"><span data-stu-id="0534a-169">You can connect toonodes that are not directly accessible over hello internet by using hello following methods:</span></span>

* <span data-ttu-id="0534a-170">**SSH**： 一旦連接 tooa 前端節點使用 SSH，然後您可以使用 SSH 從 hello 前端節點 tooconnect tooother hello 叢集中的節點。</span><span class="sxs-lookup"><span data-stu-id="0534a-170">**SSH**: Once connected tooa head node using SSH, you can then use SSH from hello head node tooconnect tooother nodes in hello cluster.</span></span> <span data-ttu-id="0534a-171">如需詳細資訊，請參閱 hello[搭配使用 SSH 和 HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)文件。</span><span class="sxs-lookup"><span data-stu-id="0534a-171">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

* <span data-ttu-id="0534a-172">**SSH 通道**： 如果您需要的 tooaccess 裝載的 web 服務的其中一個 hello 節點不是公開 toohello 網際網路，您必須使用 SSH 通道。</span><span class="sxs-lookup"><span data-stu-id="0534a-172">**SSH Tunnel**: If you need tooaccess a web service hosted on one of hello nodes that is not exposed toohello internet, you must use an SSH tunnel.</span></span> <span data-ttu-id="0534a-173">如需詳細資訊，請參閱 hello [HDInsight 搭配使用 SSH 通道](hdinsight-linux-ambari-ssh-tunnel.md)文件。</span><span class="sxs-lookup"><span data-stu-id="0534a-173">For more information, see hello [Use an SSH tunnel with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

* <span data-ttu-id="0534a-174">**Azure 虛擬網路**： 如果您的 HDInsight 叢集的 Azure 虛擬網路上的任何資源屬於 hello 相同虛擬網路可直接存取 hello 叢集中所有節點。</span><span class="sxs-lookup"><span data-stu-id="0534a-174">**Azure Virtual Network**: If your HDInsight cluster is part of an Azure Virtual Network, any resource on hello same Virtual Network can directly access all nodes in hello cluster.</span></span> <span data-ttu-id="0534a-175">如需詳細資訊，請參閱 hello[使用 Azure 虛擬網路的延伸 HDInsight](hdinsight-extend-hadoop-virtual-network.md)文件。</span><span class="sxs-lookup"><span data-stu-id="0534a-175">For more information, see hello [Extend HDInsight using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

## <a name="how-toocheck-on-a-service-status"></a><span data-ttu-id="0534a-176">如何 toocheck 服務狀態</span><span class="sxs-lookup"><span data-stu-id="0534a-176">How toocheck on a service status</span></span>

<span data-ttu-id="0534a-177">toocheck hello 的 hello 前端節點上執行，請使用 hello Ambari Web UI 或 hello Ambari REST API 服務的狀態。</span><span class="sxs-lookup"><span data-stu-id="0534a-177">toocheck hello status of services that run on hello head nodes, use hello Ambari Web UI or hello Ambari REST API.</span></span>

### <a name="ambari-web-ui"></a><span data-ttu-id="0534a-178">Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="0534a-178">Ambari Web UI</span></span>

<span data-ttu-id="0534a-179">hello Ambari Web UI 是可在 https://CLUSTERNAME.azurehdinsight.net 檢視。</span><span class="sxs-lookup"><span data-stu-id="0534a-179">hello Ambari Web UI is viewable at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="0534a-180">取代**CLUSTERNAME**與 hello 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="0534a-180">Replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="0534a-181">如果出現提示，請輸入您的叢集 hello HTTP 使用者認證。</span><span class="sxs-lookup"><span data-stu-id="0534a-181">If prompted, enter hello HTTP user credentials for your cluster.</span></span> <span data-ttu-id="0534a-182">hello 預設 HTTP 使用者名稱是**admin** hello 密碼為 hello 建立 hello 叢集時所輸入的密碼。</span><span class="sxs-lookup"><span data-stu-id="0534a-182">hello default HTTP user name is **admin** and hello password is hello password you entered when creating hello cluster.</span></span>

<span data-ttu-id="0534a-183">當您來到 hello Ambari 頁面上時，安裝 hello 服務會列在 hello hello 頁面左邊。</span><span class="sxs-lookup"><span data-stu-id="0534a-183">When you arrive on hello Ambari page, hello installed services are listed on hello left of hello page.</span></span>

![已安裝的服務](./media/hdinsight-high-availability-linux/services.png)

<span data-ttu-id="0534a-185">有一系列可能會出現 下一步 tooa 服務 tooindicate 狀態的圖示。</span><span class="sxs-lookup"><span data-stu-id="0534a-185">There are a series of icons that may appear next tooa service tooindicate status.</span></span> <span data-ttu-id="0534a-186">可以使用 hello 檢視 tooa 服務相關的任何警示**警示**hello hello 頁頂端的連結。</span><span class="sxs-lookup"><span data-stu-id="0534a-186">Any alerts related tooa service can be viewed using hello **Alerts** link at hello top of hello page.</span></span> <span data-ttu-id="0534a-187">您可以選取每個服務 tooview 詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0534a-187">You can select each service tooview more information on it.</span></span>

<span data-ttu-id="0534a-188">雖然 hello 服務 頁面會提供資訊 hello 狀態和組態的每個服務，它不提供前端節點 hello 服務執行的所在資訊。</span><span class="sxs-lookup"><span data-stu-id="0534a-188">While hello service page provides information on hello status and configuration of each service, it does not provide information on which head node hello service is running on.</span></span> <span data-ttu-id="0534a-189">tooview 此資訊、 使用 hello**主機**hello hello 頁頂端的連結。</span><span class="sxs-lookup"><span data-stu-id="0534a-189">tooview this information, use hello **Hosts** link at hello top of hello page.</span></span> <span data-ttu-id="0534a-190">此頁面會顯示 hello 叢集，包括 hello 前端節點內的主機。</span><span class="sxs-lookup"><span data-stu-id="0534a-190">This page displays hosts within hello cluster, including hello head nodes.</span></span>

![主機清單](./media/hdinsight-high-availability-linux/hosts.png)

<span data-ttu-id="0534a-192">選取 hello 連結的其中一個 hello 前端節點會顯示 hello 服務與該節點上執行的元件。</span><span class="sxs-lookup"><span data-stu-id="0534a-192">Selecting hello link for one of hello head nodes displays hello services and components running on that node.</span></span>

![元件狀態](./media/hdinsight-high-availability-linux/nodeservices.png)

<span data-ttu-id="0534a-194">如需有關使用 Ambari 的詳細資訊，請參閱[監視和管理 HDInsight 使用 hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)。</span><span class="sxs-lookup"><span data-stu-id="0534a-194">For more information on using Ambari, see [Monitor and manage HDInsight using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

### <a name="ambari-rest-api"></a><span data-ttu-id="0534a-195">Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="0534a-195">Ambari REST API</span></span>

<span data-ttu-id="0534a-196">hello Ambari REST API 是透過 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="0534a-196">hello Ambari REST API is available over hello internet.</span></span> <span data-ttu-id="0534a-197">hello HDInsight 公用閘道處理路由要求 toohello 前端節點目前裝載 hello REST API。</span><span class="sxs-lookup"><span data-stu-id="0534a-197">hello HDInsight public gateway handles routing requests toohello head node that is currently hosting hello REST API.</span></span>

<span data-ttu-id="0534a-198">您可以使用下列命令 toocheck hello 狀態 hello Ambari REST API 服務的 hello:</span><span class="sxs-lookup"><span data-stu-id="0534a-198">You can use hello following command toocheck hello state of a service through hello Ambari REST API:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* <span data-ttu-id="0534a-199">取代**密碼**與 hello HTTP 使用者 （管理員） 帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="0534a-199">Replace **PASSWORD** with hello HTTP user (admin) account password.</span></span>
* <span data-ttu-id="0534a-200">取代**CLUSTERNAME** hello hello 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="0534a-200">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
* <span data-ttu-id="0534a-201">取代**SERVICENAME** hello hello 服務名稱與您想 toocheck hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="0534a-201">Replace **SERVICENAME** with hello name of hello service you want toocheck hello status of.</span></span>

<span data-ttu-id="0534a-202">例如，toocheck hello 狀態 hello **HDFS**上名為叢集的服務**mycluster**，密碼是**密碼**，您會使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="0534a-202">For example, toocheck hello status of hello **HDFS** service on a cluster named **mycluster**, with a password of **password**, you would use hello following command:</span></span>

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

<span data-ttu-id="0534a-203">hello 回應是類似 toohello 下列 JSON:</span><span class="sxs-lookup"><span data-stu-id="0534a-203">hello response is similar toohello following JSON:</span></span>

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

<span data-ttu-id="0534a-204">hello URL 告訴我們 hello 服務目前在名為前端節點上執行**hn0 CLUSTERNAME**。</span><span class="sxs-lookup"><span data-stu-id="0534a-204">hello URL tells us that hello service is currently running on a head node named **hn0-CLUSTERNAME**.</span></span>

<span data-ttu-id="0534a-205">hello 狀態告訴我們，目前執行 hello 服務，或**已啟動**。</span><span class="sxs-lookup"><span data-stu-id="0534a-205">hello state tells us that hello service is currently running, or **STARTED**.</span></span>

<span data-ttu-id="0534a-206">如果您不知道 hello 叢集上安裝了哪些服務，您可以使用下列命令 tooretrieve 清單 hello:</span><span class="sxs-lookup"><span data-stu-id="0534a-206">If you do not know what services are installed on hello cluster, you can use hello following command tooretrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

<span data-ttu-id="0534a-207">如需使用 hello Ambari REST API 的詳細資訊，請參閱[監視和管理 HDInsight 的使用 hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md)。</span><span class="sxs-lookup"><span data-stu-id="0534a-207">For more information on working with hello Ambari REST API, see [Monitor and Manage HDInsight using hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

#### <a name="service-components"></a><span data-ttu-id="0534a-208">服務元件</span><span class="sxs-lookup"><span data-stu-id="0534a-208">Service components</span></span>

<span data-ttu-id="0534a-209">服務可能包含您想 toocheck hello 狀態的個別的元件。</span><span class="sxs-lookup"><span data-stu-id="0534a-209">Services may contain components that you wish toocheck hello status of individually.</span></span> <span data-ttu-id="0534a-210">例如，HDFS 包含 hello NameNode 元件。</span><span class="sxs-lookup"><span data-stu-id="0534a-210">For example, HDFS contains hello NameNode component.</span></span> <span data-ttu-id="0534a-211">在元件上的 tooview 資訊，hello 命令會是：</span><span class="sxs-lookup"><span data-stu-id="0534a-211">tooview information on a component, hello command would be:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

<span data-ttu-id="0534a-212">如果您不知道哪些元件所提供的服務，您可以使用下列命令 tooretrieve 清單 hello:</span><span class="sxs-lookup"><span data-stu-id="0534a-212">If you do not know what components are provided by a service, you can use hello following command tooretrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-tooaccess-log-files-on-hello-head-nodes"></a><span data-ttu-id="0534a-213">如何 tooaccess 登 hello 前端節點上的檔案</span><span class="sxs-lookup"><span data-stu-id="0534a-213">How tooaccess log files on hello head nodes</span></span>

### <a name="ssh"></a><span data-ttu-id="0534a-214">SSH</span><span class="sxs-lookup"><span data-stu-id="0534a-214">SSH</span></span>

<span data-ttu-id="0534a-215">透過 SSH 連線的 tooa 前端節點，而記錄檔可以找到下**/var/記錄**。</span><span class="sxs-lookup"><span data-stu-id="0534a-215">While connected tooa head node through SSH, log files can be found under **/var/log**.</span></span> <span data-ttu-id="0534a-216">例如， **/var/log/hadoop-yarn/yarn** 包含 YARN 的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0534a-216">For example, **/var/log/hadoop-yarn/yarn** contain logs for YARN.</span></span>

<span data-ttu-id="0534a-217">每個前端節點可以有唯一的記錄項目，所以您應該檢查 hello 登入同時。</span><span class="sxs-lookup"><span data-stu-id="0534a-217">Each head node can have unique log entries, so you should check hello logs on both.</span></span>

### <a name="sftp"></a><span data-ttu-id="0534a-218">SFTP</span><span class="sxs-lookup"><span data-stu-id="0534a-218">SFTP</span></span>

<span data-ttu-id="0534a-219">您也可以連接 toohello hello SSH 檔案傳輸通訊協定或安全檔案傳輸通訊協定 (SFTP) 所使用的前端節點，並直接下載 hello 的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0534a-219">You can also connect toohello head node using hello SSH File Transfer Protocol or Secure File Transfer Protocol (SFTP), and download hello log files directly.</span></span>

<span data-ttu-id="0534a-220">類似 toousing 連接必須提供 toohello 叢集時將 SSH 用戶端 hello SSH 使用者帳戶名稱和 hello SSH hello 叢集位址。</span><span class="sxs-lookup"><span data-stu-id="0534a-220">Similar toousing an SSH client, when connecting toohello cluster you must provide hello SSH user account name and hello SSH address of hello cluster.</span></span> <span data-ttu-id="0534a-221">例如： `sftp username@mycluster-ssh.azurehdinsight.net`。</span><span class="sxs-lookup"><span data-stu-id="0534a-221">For example, `sftp username@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="0534a-222">Hello 帳戶出現提示時，提供 hello 密碼或提供的公開公鑰使用 hello`-i`參數。</span><span class="sxs-lookup"><span data-stu-id="0534a-222">Provide hello password for hello account when prompted, or provide a public key using hello `-i` parameter.</span></span>

<span data-ttu-id="0534a-223">連線之後，您會看到 `sftp>` 提示。</span><span class="sxs-lookup"><span data-stu-id="0534a-223">Once connected, you are presented with a `sftp>` prompt.</span></span> <span data-ttu-id="0534a-224">您可以從該提示變更目錄、上傳和下載檔案。</span><span class="sxs-lookup"><span data-stu-id="0534a-224">From this prompt, you can change directories, upload, and download files.</span></span> <span data-ttu-id="0534a-225">例如，下列命令的 hello 變更目錄 toohello **/var/log/hadoop/hdfs**目錄，然後再下載 hello 目錄中的所有檔案。</span><span class="sxs-lookup"><span data-stu-id="0534a-225">For example, hello following commands change directories toohello **/var/log/hadoop/hdfs** directory and then download all files in hello directory.</span></span>

    cd /var/log/hadoop/hdfs
    get *

<span data-ttu-id="0534a-226">如需可用命令的清單，請輸入`help`在 hello`sftp>`提示字元。</span><span class="sxs-lookup"><span data-stu-id="0534a-226">For a list of available commands, enter `help` at hello `sftp>` prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="0534a-227">另外還有 toovisualize hello 檔案系統時使用 SFTP 連接可讓您的圖形化介面。</span><span class="sxs-lookup"><span data-stu-id="0534a-227">There are also graphical interfaces that allow you toovisualize hello file system when connected using SFTP.</span></span> <span data-ttu-id="0534a-228">例如， [MobaXTerm](http://mobaxterm.mobatek.net/)可讓您使用介面類似 tooWindows 總管 toobrowse hello 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="0534a-228">For example, [MobaXTerm](http://mobaxterm.mobatek.net/) allows you toobrowse hello file system using an interface similar tooWindows Explorer.</span></span>

### <a name="ambari"></a><span data-ttu-id="0534a-229">Ambari</span><span class="sxs-lookup"><span data-stu-id="0534a-229">Ambari</span></span>

> [!NOTE]
> <span data-ttu-id="0534a-230">tooaccess 記錄檔使用 Ambari，您必須使用 SSH 通道。</span><span class="sxs-lookup"><span data-stu-id="0534a-230">tooaccess log files using Ambari, you must use an SSH tunnel.</span></span> <span data-ttu-id="0534a-231">公開 hello 網際網路上不公開 hello hello 個別服務的 web 介面。</span><span class="sxs-lookup"><span data-stu-id="0534a-231">hello web interfaces for hello individual services are not exposed publicly on hello Internet.</span></span> <span data-ttu-id="0534a-232">如需使用 SSH 通道的資訊，請參閱 hello[使用 SSH 通道](hdinsight-linux-ambari-ssh-tunnel.md)文件。</span><span class="sxs-lookup"><span data-stu-id="0534a-232">For information on using an SSH tunnel, see hello [Use SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="0534a-233">從 hello Ambari Web UI 中，選取您希望 tooview 記錄檔 (例如，YARN) hello 服務。</span><span class="sxs-lookup"><span data-stu-id="0534a-233">From hello Ambari Web UI, select hello service you wish tooview logs for (for example, YARN).</span></span> <span data-ttu-id="0534a-234">然後使用**快速連結**tooselect 的前端節點 tooview hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="0534a-234">Then use **Quick Links** tooselect which head node tooview hello logs for.</span></span>

![使用快速連結 tooview 記錄檔](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-tooconfigure-hello-node-size"></a><span data-ttu-id="0534a-236">Tooconfigure hello 節點大小的方式</span><span class="sxs-lookup"><span data-stu-id="0534a-236">How tooconfigure hello node size</span></span>

<span data-ttu-id="0534a-237">只可以在叢集建立期間選取節點的 hello 大小。</span><span class="sxs-lookup"><span data-stu-id="0534a-237">hello size of a node can only be selected during cluster creation.</span></span> <span data-ttu-id="0534a-238">您可以找到 hello 一份可用的不同 VM 大小 HDInsight 上 hello [HDInsight 定價頁面](https://azure.microsoft.com/pricing/details/hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="0534a-238">You can find a list of hello different VM sizes available for HDInsight on hello [HDInsight pricing page](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="0534a-239">在建立叢集時，您可以指定 hello hello 節點大小。</span><span class="sxs-lookup"><span data-stu-id="0534a-239">When creating a cluster, you can specify hello size of hello nodes.</span></span> <span data-ttu-id="0534a-240">hello 下列資訊提供指引如何 toospecify hello 大小使用 hello [Azure 入口網站][preview-portal]， [Azure PowerShell][azure-powershell]，和 hello [Azure CLI][azure-cli]:</span><span class="sxs-lookup"><span data-stu-id="0534a-240">hello following information provides guidance on how toospecify hello size using hello [Azure portal][preview-portal], [Azure PowerShell][azure-powershell], and hello [Azure CLI][azure-cli]:</span></span>

* <span data-ttu-id="0534a-241">**Azure 入口網站**： 在建立叢集時，您可以設定的 hello 節點 hello 叢集所用的 hello 大小：</span><span class="sxs-lookup"><span data-stu-id="0534a-241">**Azure portal**: When creating a cluster, you can set hello size of hello nodes used by hello cluster:</span></span>

    ![可選取節點大小的 [叢集映像建立精靈]](./media/hdinsight-high-availability-linux/headnodesize.png)

* <span data-ttu-id="0534a-243">**Azure CLI**： 當使用 hello`azure hdinsight cluster create`命令時，您可以設定 hello 大小 hello head、 背景工作，以及動物園管理員節點使用 hello `--headNodeSize`， `--workerNodeSize`，和`--zookeeperNodeSize`參數。</span><span class="sxs-lookup"><span data-stu-id="0534a-243">**Azure CLI**: When using hello `azure hdinsight cluster create` command, you can set hello size of hello head, worker, and ZooKeeper nodes by using hello `--headNodeSize`, `--workerNodeSize`, and `--zookeeperNodeSize` parameters.</span></span>

* <span data-ttu-id="0534a-244">**Azure PowerShell**： 當使用 hello `New-AzureRmHDInsightCluster` cmdlet，您可以設定 hello 大小 hello head、 背景工作，以及動物園管理員節點使用 hello `-HeadNodeVMSize`， `-WorkerNodeSize`，和`-ZookeeperNodeSize`參數。</span><span class="sxs-lookup"><span data-stu-id="0534a-244">**Azure PowerShell**: When using hello `New-AzureRmHDInsightCluster` cmdlet, you can set hello size of hello head, worker, and ZooKeeper nodes by using hello `-HeadNodeVMSize`, `-WorkerNodeSize`, and `-ZookeeperNodeSize` parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0534a-245">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0534a-245">Next steps</span></span>

<span data-ttu-id="0534a-246">使用下列連結 toolearn 更多關於此文件中所述的項目 hello。</span><span class="sxs-lookup"><span data-stu-id="0534a-246">Use hello following links toolearn more about things mentioned in this document.</span></span>

* [<span data-ttu-id="0534a-247">Ambari REST 參考</span><span class="sxs-lookup"><span data-stu-id="0534a-247">Ambari REST Reference</span></span>](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [<span data-ttu-id="0534a-248">安裝和設定 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0534a-248">Install and configure hello Azure CLI</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="0534a-249">安裝並設定 Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0534a-249">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="0534a-250">使用 Ambari 管理 HDInsight</span><span class="sxs-lookup"><span data-stu-id="0534a-250">Manage HDInsight using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="0534a-251">佈建以 Linux 為基礎的 HDInsight 叢集</span><span class="sxs-lookup"><span data-stu-id="0534a-251">Provision Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
