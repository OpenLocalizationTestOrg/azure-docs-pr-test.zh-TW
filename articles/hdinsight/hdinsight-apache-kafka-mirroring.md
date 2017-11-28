---
title: "aaaMirror Apache Kafka 主題 Azure HDInsight |Microsoft 文件"
description: "深入了解 toouse Apache Kafka 的鏡像功能鏡像主題 tooa 次要叢集 toomaintain Kafka HDInsight 叢集上的複本。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 015d276e-f678-4f2b-9572-75553c56625b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: 5ace0251d7402d4d7d9b28726e253ce7091a87ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-mirrormaker-tooreplicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a><span data-ttu-id="b5f86-103">使用 HDInsight （預覽） 上的 Kafka MirrorMaker tooreplicate Apache Kafka 主題</span><span class="sxs-lookup"><span data-stu-id="b5f86-103">Use MirrorMaker tooreplicate Apache Kafka topics with Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="b5f86-104">了解如何 toouse Apache Kafka 的鏡像功能 tooreplicate 主題 tooa 次要叢集。</span><span class="sxs-lookup"><span data-stu-id="b5f86-104">Learn how toouse Apache Kafka's mirroring feature tooreplicate topics tooa secondary cluster.</span></span> <span data-ttu-id="b5f86-105">鏡像可執行做為連續的處理序或間歇性使用，做為移轉的方法資料從某個叢集 tooanother。</span><span class="sxs-lookup"><span data-stu-id="b5f86-105">Mirroring can be ran as a continuous process, or used intermittently as a method of migrating data from one cluster tooanother.</span></span>

<span data-ttu-id="b5f86-106">在此範例中，鏡像是兩個的 HDInsight 叢集之間使用的 tooreplicate 主題。</span><span class="sxs-lookup"><span data-stu-id="b5f86-106">In this example, mirroring is used tooreplicate topics between two HDInsight clusters.</span></span> <span data-ttu-id="b5f86-107">這兩個叢集會在 hello Azure 虛擬網路中相同的區域。</span><span class="sxs-lookup"><span data-stu-id="b5f86-107">Both clusters are in an Azure Virtual Network in hello same region.</span></span>

> [!WARNING]
> <span data-ttu-id="b5f86-108">鏡像應該不會被視為與表示 tooachieve 容錯。</span><span class="sxs-lookup"><span data-stu-id="b5f86-108">Mirroring should not be considered as a means tooachieve fault-tolerance.</span></span> <span data-ttu-id="b5f86-109">hello 主題內的位移的 tooitems 之間的有所差異 hello 來源和目的地叢集，因此用戶端無法使用兩個 hello 交換使用。</span><span class="sxs-lookup"><span data-stu-id="b5f86-109">hello offset tooitems within a topic are different between hello source and destination clusters, so clients cannot use hello two interchangeably.</span></span>
>
> <span data-ttu-id="b5f86-110">如果您擔心容錯功能，您應該在您的叢集內設定 hello 主題的複寫。</span><span class="sxs-lookup"><span data-stu-id="b5f86-110">If you are concerned about fault tolerance, you should set replication for hello topics within your cluster.</span></span> <span data-ttu-id="b5f86-111">如需詳細資訊，請參閱[開始使用 Kafka on HDInsight](hdinsight-apache-kafka-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="b5f86-111">For more information, see [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md).</span></span>

## <a name="how-kafka-mirroring-works"></a><span data-ttu-id="b5f86-112">Kafka 鏡像的運作方式</span><span class="sxs-lookup"><span data-stu-id="b5f86-112">How Kafka mirroring works</span></span>

<span data-ttu-id="b5f86-113">鏡像的運作方式是使用 hello MirrorMaker 工具 （Apache Kafka 的一部分） tooconsume hello 來源叢集上的主題中的記錄，然後再建立 hello 目的地叢集上的 本機複本。</span><span class="sxs-lookup"><span data-stu-id="b5f86-113">Mirroring works by using hello MirrorMaker tool (part of Apache Kafka) tooconsume records from topics on hello source cluster and then create a local copy on hello destination cluster.</span></span> <span data-ttu-id="b5f86-114">MirrorMaker 使用其中一個 （或以上）*取用者*hello 來源叢集上，從讀取和*生產者*寫入 toohello 本機 （目的地） 叢集。</span><span class="sxs-lookup"><span data-stu-id="b5f86-114">MirrorMaker uses one (or more) *consumers* that read from hello source cluster, and a *producer* that writes toohello local (destination) cluster.</span></span>

<span data-ttu-id="b5f86-115">hello 下列圖表說明 hello 鏡像處理序：</span><span class="sxs-lookup"><span data-stu-id="b5f86-115">hello following diagram illustrates hello Mirroring process:</span></span>

![Hello 鏡像處理序的圖表](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

<span data-ttu-id="b5f86-117">Apache Kafka HDInsight 上不提供存取 toohello Kafka 服務 hello 透過公用網際網路。</span><span class="sxs-lookup"><span data-stu-id="b5f86-117">Apache Kafka on HDInsight does not provide access toohello Kafka service over hello public internet.</span></span> <span data-ttu-id="b5f86-118">Kafka 產生者或取用者必須在 hello 與 hello hello Kafka 叢集節點的相同 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b5f86-118">Kafka producers or consumers must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="b5f86-119">針對此範例中，hello Kafka 來源與目的地叢集位於 Azure 的虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="b5f86-119">For this example, both hello Kafka source and destination clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="b5f86-120">hello 下圖顯示 hello 叢集之間通訊流動的方式：</span><span class="sxs-lookup"><span data-stu-id="b5f86-120">hello following diagram shows how communication flows between hello clusters:</span></span>

![Azure 虛擬網路中的來源和目的地 Kafka 叢集圖表](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

<span data-ttu-id="b5f86-122">hello 來源和目的地叢集可以在 hello 節點與資料分割的不同，而且 hello 主題內的位移也會不同。</span><span class="sxs-lookup"><span data-stu-id="b5f86-122">hello source and destination clusters can be different in hello number of nodes and partitions, and offsets within hello topics are different also.</span></span> <span data-ttu-id="b5f86-123">鏡像會維護 hello 金鑰值以用於資料分割，因此會保留每個索引鍵為基礎的記錄順序。</span><span class="sxs-lookup"><span data-stu-id="b5f86-123">Mirroring maintains hello key value that is used for partitioning, so record order is preserved on a per-key basis.</span></span>

### <a name="mirroring-across-network-boundaries"></a><span data-ttu-id="b5f86-124">跨網路界限鏡像</span><span class="sxs-lookup"><span data-stu-id="b5f86-124">Mirroring across network boundaries</span></span>

<span data-ttu-id="b5f86-125">如果您需要 toomirror Kafka 不同的網路中的叢集之間，有下列其他考量 hello:</span><span class="sxs-lookup"><span data-stu-id="b5f86-125">If you need toomirror between Kafka clusters in different networks, there are hello following additional considerations:</span></span>

* <span data-ttu-id="b5f86-126">**閘道**: hello 網路必須能夠 toocommunicate 在 hello TCPIP 層級。</span><span class="sxs-lookup"><span data-stu-id="b5f86-126">**Gateways**: hello networks must be able toocommunicate at hello TCPIP level.</span></span>

* <span data-ttu-id="b5f86-127">**名稱解析**: hello Kafka 叢集在每個網路必須能夠 tooconnect tooeach 其他使用主機名稱。</span><span class="sxs-lookup"><span data-stu-id="b5f86-127">**Name resolution**: hello Kafka clusters in each network must be able tooconnect tooeach other by using hostnames.</span></span> <span data-ttu-id="b5f86-128">這可能需要為每個網路中的網域名稱系統 (DNS) 伺服器設定 tooforward 要求 toohello 其他網路。</span><span class="sxs-lookup"><span data-stu-id="b5f86-128">This may require a Domain Name System (DNS) server in each network that is configured tooforward requests toohello other networks.</span></span>

    <span data-ttu-id="b5f86-129">建立 Azure 虛擬網路，而不是使用 DNS 自動提供的 hello 與 hello 網路時，您必須指定自訂 DNS 伺服器和 hello 伺服器 IP 位址 hello。</span><span class="sxs-lookup"><span data-stu-id="b5f86-129">When creating an Azure Virtual Network, instead of using hello automatic DNS provided with hello network, you must specify a custom DNS server and hello IP address for hello server.</span></span> <span data-ttu-id="b5f86-130">Hello 已建立虛擬網路之後, 您就必須建立 Azure 虛擬機器使用該 IP 位址，然後安裝並在其上設定 DNS 軟體。</span><span class="sxs-lookup"><span data-stu-id="b5f86-130">After hello Virtual Network has been created, you must then create an Azure Virtual Machine that uses that IP address, then install and configure DNS software on it.</span></span>

    > [!WARNING]
    > <span data-ttu-id="b5f86-131">建立並設定自訂 DNS 伺服器 hello 再安裝 HDInsight 到 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b5f86-131">Create and configure hello custom DNS server before installing HDInsight into hello Virtual Network.</span></span> <span data-ttu-id="b5f86-132">沒有 HDInsight toouse hello DNS 伺服器設定為 hello 虛擬網路所需的其他設定。</span><span class="sxs-lookup"><span data-stu-id="b5f86-132">There is no additional configuration required for HDInsight toouse hello DNS server configured for hello Virtual Network.</span></span>

<span data-ttu-id="b5f86-133">如需有關如何連接兩個 Azure 虛擬網路的詳細資訊，請參閱[設定 VNet 對 VNet 連線](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="b5f86-133">For more information on connecting two Azure Virtual Networks, see [Configure a VNet-to-VNet connection](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

## <a name="create-kafka-clusters"></a><span data-ttu-id="b5f86-134">建立 Kafka 叢集</span><span class="sxs-lookup"><span data-stu-id="b5f86-134">Create Kafka clusters</span></span>

<span data-ttu-id="b5f86-135">雖然您可以建立 Azure 虛擬網路和 Kafka 叢集以手動方式，很容易 toouse Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="b5f86-135">While you can create an Azure virtual network and Kafka clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="b5f86-136">Azure 虛擬網路和兩個 Kafka 叢集 tooyour Azure 訂用帳戶，請使用下列步驟 toodeploy hello。</span><span class="sxs-lookup"><span data-stu-id="b5f86-136">Use hello following steps toodeploy an Azure virtual network and two Kafka clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="b5f86-137">使用下列按鈕 toosign 中 tooAzure 和開啟 hello 範本 hello Azure 入口網站中的 hello。</span><span class="sxs-lookup"><span data-stu-id="b5f86-137">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    <span data-ttu-id="b5f86-138">hello Azure Resource Manager 範本位於**https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**。</span><span class="sxs-lookup"><span data-stu-id="b5f86-138">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="b5f86-139">HDInsight 上 Kafka tooguarantee 可用性，您的叢集必須包含至少三個背景工作節點。</span><span class="sxs-lookup"><span data-stu-id="b5f86-139">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="b5f86-140">此範本會建立包含三個背景工作角色節點的 Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="b5f86-140">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="b5f86-141">使用下列資訊 toopopulate hello 項目上 hello 的 hello**自訂部署**刀鋒視窗中：</span><span class="sxs-lookup"><span data-stu-id="b5f86-141">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
    
    ![HDInsight 自訂部署](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * <span data-ttu-id="b5f86-143">**資源群組**：建立群組或選取現有的群組。</span><span class="sxs-lookup"><span data-stu-id="b5f86-143">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="b5f86-144">此群組包含 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="b5f86-144">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="b5f86-145">**位置**： 選取位置的地理位置關閉 tooyou。</span><span class="sxs-lookup"><span data-stu-id="b5f86-145">**Location**: Select a location geographically close tooyou.</span></span>
     
    * <span data-ttu-id="b5f86-146">**基底叢集名稱**: hello Kafka 叢集 hello 基底名稱為使用此值。</span><span class="sxs-lookup"><span data-stu-id="b5f86-146">**Base Cluster Name**: This value is used as hello base name for hello Kafka clusters.</span></span> <span data-ttu-id="b5f86-147">例如，輸入 **hdi** 可建立名為 **source-hdi** 和 **dest-hdi** 的叢集。</span><span class="sxs-lookup"><span data-stu-id="b5f86-147">For example, entering **hdi** creates clusters named **source-hdi** and **dest-hdi**.</span></span>

    * <span data-ttu-id="b5f86-148">**叢集登入使用者名稱**: hello 系統管理員使用者名稱 hello 來源與目的 Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="b5f86-148">**Cluster Login User Name**: hello admin user name for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="b5f86-149">**叢集登入密碼**: hello 來源與目的 hello 管理使用者的密碼 Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="b5f86-149">**Cluster Login Password**: hello admin user password for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="b5f86-150">**SSH 使用者名稱**: hello SSH 使用者 toocreate hello 來源與目的 Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="b5f86-150">**SSH User Name**: hello SSH user toocreate for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="b5f86-151">**SSH 密碼**: hello hello hello 來源和目的地的 SSH 使用者密碼 Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="b5f86-151">**SSH Password**: hello password for hello SSH user for hello source and destination Kafka clusters.</span></span>

3. <span data-ttu-id="b5f86-152">讀取 hello**條款和條件**，然後選取**toohello 條款和條件前面所述，即表示我同意**。</span><span class="sxs-lookup"><span data-stu-id="b5f86-152">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="b5f86-153">最後，檢查**Pin toodashboard** ，然後選取 **購買**。</span><span class="sxs-lookup"><span data-stu-id="b5f86-153">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="b5f86-154">它會採用約 20 分鐘 toocreate hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="b5f86-154">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="b5f86-155">一旦已建立 hello 資源，您已重新導向的 tooa 刀鋒視窗中的 hello 資源群組含有 hello 叢集和 web 儀表板。</span><span class="sxs-lookup"><span data-stu-id="b5f86-155">Once hello resources have been created, you are redirected tooa blade for hello resource group that contains hello clusters and web dashboard.</span></span>

![Hello vnet 與叢集資源群組 刀鋒視窗](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="b5f86-157">請注意，hello hello HDInsight 叢集名稱**來源 BASENAME**和**目的地 BASENAME**，其中 BASENAME 是 hello 提供 toohello 範本的名稱。</span><span class="sxs-lookup"><span data-stu-id="b5f86-157">Notice that hello names of hello HDInsight clusters are **source-BASENAME** and **dest-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="b5f86-158">連接 toohello 叢集時，您可以使用在稍後步驟中的這些名稱。</span><span class="sxs-lookup"><span data-stu-id="b5f86-158">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="create-topics"></a><span data-ttu-id="b5f86-159">建立主題</span><span class="sxs-lookup"><span data-stu-id="b5f86-159">Create topics</span></span>

1. <span data-ttu-id="b5f86-160">連接 toohello**來源**叢集使用 SSH:</span><span class="sxs-lookup"><span data-stu-id="b5f86-160">Connect toohello **source** cluster using SSH:</span></span>

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="b5f86-161">取代**sshuser** hello 建立 hello 叢集時所使用的 SSH 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="b5f86-161">Replace **sshuser** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="b5f86-162">取代**BASENAME** hello 建立 hello 叢集時所使用的基底名稱。</span><span class="sxs-lookup"><span data-stu-id="b5f86-162">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

    <span data-ttu-id="b5f86-163">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="b5f86-163">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="b5f86-164">使用 hello 下列命令 toofind hello 動物園管理員主機 hello 來源叢集：</span><span class="sxs-lookup"><span data-stu-id="b5f86-164">Use hello following commands toofind hello Zookeeper hosts for hello source cluster:</span></span>

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get hello zookeeper hosts for hello source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with hello password for hello cluster.

    Replace `$CLUSTERNAME` with hello name of hello source cluster.

3. toocreate a topic named `testtopic`, use hello following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. <span data-ttu-id="b5f86-165">已建立下列 hello 主題的命令 tooverify 使用 hello:</span><span class="sxs-lookup"><span data-stu-id="b5f86-165">Use hello following command tooverify that hello topic was created:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="b5f86-166">hello 回應包含`testtopic`。</span><span class="sxs-lookup"><span data-stu-id="b5f86-166">hello response contains `testtopic`.</span></span>

4. <span data-ttu-id="b5f86-167">遵循這個 tooview hello 動物園管理員主機資訊的使用 hello (hello**來源**) 叢集：</span><span class="sxs-lookup"><span data-stu-id="b5f86-167">Use hello following tooview hello Zookeeper host information for this (hello **source**) cluster:</span></span>

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="b5f86-168">這會傳回資訊的類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="b5f86-168">This returns information similar toohello following text:</span></span>

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    <span data-ttu-id="b5f86-169">請儲存此資訊。</span><span class="sxs-lookup"><span data-stu-id="b5f86-169">Save this information.</span></span> <span data-ttu-id="b5f86-170">它用於 hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="b5f86-170">It is used in hello next section.</span></span>

## <a name="configure-mirroring"></a><span data-ttu-id="b5f86-171">設定鏡像功能</span><span class="sxs-lookup"><span data-stu-id="b5f86-171">Configure mirroring</span></span>

1. <span data-ttu-id="b5f86-172">連接 toohello**目的地**叢集使用不同的 SSH 工作階段：</span><span class="sxs-lookup"><span data-stu-id="b5f86-172">Connect toohello **destination** cluster using a different SSH session:</span></span>

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="b5f86-173">取代**sshuser** hello 建立 hello 叢集時所使用的 SSH 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="b5f86-173">Replace **sshuser** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="b5f86-174">取代**BASENAME** hello 建立 hello 叢集時所使用的基底名稱。</span><span class="sxs-lookup"><span data-stu-id="b5f86-174">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

    <span data-ttu-id="b5f86-175">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="b5f86-175">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="b5f86-176">使用 hello 下列命令 toocreate`consumer.properties`檔案，其中描述如何以 hello toocommunicate**來源**叢集：</span><span class="sxs-lookup"><span data-stu-id="b5f86-176">Use hello following command toocreate a `consumer.properties` file that describes how toocommunicate with hello **source** cluster:</span></span>

    ```bash
    nano consumer.properties
    ```

    <span data-ttu-id="b5f86-177">使用 hello 文字之後做為 hello 內容的 hello`consumer.properties`檔案：</span><span class="sxs-lookup"><span data-stu-id="b5f86-177">Use hello following text as hello contents of hello `consumer.properties` file:</span></span>

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    <span data-ttu-id="b5f86-178">取代**SOURCE_ZKHOSTS**以 hello 動物園管理員裝載資訊從 hello**來源**叢集。</span><span class="sxs-lookup"><span data-stu-id="b5f86-178">Replace **SOURCE_ZKHOSTS** with hello Zookeeper hosts information from hello **source** cluster.</span></span>

    <span data-ttu-id="b5f86-179">讀取 hello 來源 Kafka 叢集時，此檔案會描述 hello 取用者資訊 toouse。</span><span class="sxs-lookup"><span data-stu-id="b5f86-179">This file describes hello consumer information toouse when reading from hello source Kafka cluster.</span></span> <span data-ttu-id="b5f86-180">如需取用者組態詳細資訊，請參閱 kafka.apache.org 上的[取用者組態](https://kafka.apache.org/documentation#consumerconfigs)。</span><span class="sxs-lookup"><span data-stu-id="b5f86-180">For more information consumer configuration, see [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) at kafka.apache.org.</span></span>

    <span data-ttu-id="b5f86-181">toosave hello 檔案，使用**Ctrl + X**， **Y**，然後**Enter**。</span><span class="sxs-lookup"><span data-stu-id="b5f86-181">toosave hello file, use **Ctrl + X**, **Y**, and then **Enter**.</span></span>

3. <span data-ttu-id="b5f86-182">在設定之前進行通訊的 hello 生產者與 hello 目的地叢集，您必須尋找 hello broker 主機 hello**目的地**叢集。</span><span class="sxs-lookup"><span data-stu-id="b5f86-182">Before configuring hello producer that communicates with hello destination cluster, you must find hello broker hosts for hello **destination** cluster.</span></span> <span data-ttu-id="b5f86-183">使用下列命令 tooretrieve hello 這項資訊：</span><span class="sxs-lookup"><span data-stu-id="b5f86-183">Use hello following commands tooretrieve this information:</span></span>

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    <span data-ttu-id="b5f86-184">取代`$PASSWORD`與 hello 叢集 hello 登入帳戶 （管理員） 的密碼。</span><span class="sxs-lookup"><span data-stu-id="b5f86-184">Replace `$PASSWORD` with hello login account (admin) password for hello cluster.</span></span>

    <span data-ttu-id="b5f86-185">取代`$CLUSTERNAME`hello hello 目的地叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="b5f86-185">Replace `$CLUSTERNAME` with hello name of hello destination cluster.</span></span>

    <span data-ttu-id="b5f86-186">這些命令會傳回類似 toohello 下列資訊：</span><span class="sxs-lookup"><span data-stu-id="b5f86-186">These commands return information similar toohello following:</span></span>

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. <span data-ttu-id="b5f86-187">使用 hello 遵循 toocreate`producer.properties`檔案，其中描述如何以 hello toocommunicate**目的地**叢集：</span><span class="sxs-lookup"><span data-stu-id="b5f86-187">Use hello following toocreate a `producer.properties` file that describes how toocommunicate with hello **destination** cluster:</span></span>

    ```bash
    nano producer.properties
    ```

    <span data-ttu-id="b5f86-188">使用 hello 文字之後做為 hello 內容的 hello`producer.properties`檔案：</span><span class="sxs-lookup"><span data-stu-id="b5f86-188">Use hello following text as hello contents of hello `producer.properties` file:</span></span>

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    <span data-ttu-id="b5f86-189">取代**DEST_BROKERS** hello broker hello 上一個步驟的資訊。</span><span class="sxs-lookup"><span data-stu-id="b5f86-189">Replace **DEST_BROKERS** with hello broker information from hello previous step.</span></span>

    <span data-ttu-id="b5f86-190">如需產生者組態詳細資訊，請參閱 kafka.apache.org 上的[者組態](https://kafka.apache.org/documentation#producerconfigs)。</span><span class="sxs-lookup"><span data-stu-id="b5f86-190">For more information producer configuration, see [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) at kafka.apache.org.</span></span>

## <a name="start-mirrormaker"></a><span data-ttu-id="b5f86-191">啟動 MirrorMaker</span><span class="sxs-lookup"><span data-stu-id="b5f86-191">Start MirrorMaker</span></span>

1. <span data-ttu-id="b5f86-192">從 hello SSH 連線 toohello**目的地**叢集，請使用下列命令 toostart hello MirrorMaker 程序的 hello:</span><span class="sxs-lookup"><span data-stu-id="b5f86-192">From hello SSH connection toohello **destination** cluster, use hello following command toostart hello MirrorMaker process:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    <span data-ttu-id="b5f86-193">此範例中使用的 hello 參數如下：</span><span class="sxs-lookup"><span data-stu-id="b5f86-193">hello parameters used in this example are:</span></span>

    * <span data-ttu-id="b5f86-194">**-consumer.config**： 指定包含取用者屬性的 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="b5f86-194">**--consumer.config**: Specifies hello file that contains consumer properties.</span></span> <span data-ttu-id="b5f86-195">這些屬性是使用的 toocreate hello 可讀取的取用者*來源*Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="b5f86-195">These properties are used toocreate a consumer that reads from hello *source* Kafka cluster.</span></span>

    * <span data-ttu-id="b5f86-196">**-producer.config**： 指定包含生產者屬性 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="b5f86-196">**--producer.config**: Specifies hello file that contains producer properties.</span></span> <span data-ttu-id="b5f86-197">這些屬性是使用的 toocreate 寫入 toohello 生產者*目的地*Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="b5f86-197">These properties are used toocreate a producer that writes toohello *destination* Kafka cluster.</span></span>

    * <span data-ttu-id="b5f86-198">**-白名單**: MirrorMaker 複寫的 hello 來源叢集 toohello 目的地的主題清單。</span><span class="sxs-lookup"><span data-stu-id="b5f86-198">**--whitelist**: A list of topics that MirrorMaker replicates from hello source cluster toohello destination.</span></span>

    * <span data-ttu-id="b5f86-199">**-num.streams**: hello 的取用者執行緒 toocreate 數目。</span><span class="sxs-lookup"><span data-stu-id="b5f86-199">**--num.streams**: hello number of consumer threads toocreate.</span></span>

 <span data-ttu-id="b5f86-200">在啟動時，MirrorMaker 傳回資訊的類似 toohello 下列文字：</span><span class="sxs-lookup"><span data-stu-id="b5f86-200">On startup, MirrorMaker returns information similar toohello following text:</span></span>

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. <span data-ttu-id="b5f86-201">從 hello SSH 連線 toohello**來源**叢集，使用下列命令 toostart 生產者 hello 和傳送訊息 toohello 主題：</span><span class="sxs-lookup"><span data-stu-id="b5f86-201">From hello SSH connection toohello **source** cluster, use hello following command toostart a producer and send messages toohello topic:</span></span>

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    <span data-ttu-id="b5f86-202">取代`$PASSWORD`hello 來源叢集的 hello （管理員） 登入密碼。</span><span class="sxs-lookup"><span data-stu-id="b5f86-202">Replace `$PASSWORD` with hello login (admin) password for hello source cluster.</span></span>

    <span data-ttu-id="b5f86-203">取代`$CLUSTERNAME`hello hello 來源叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="b5f86-203">Replace `$CLUSTERNAME` with hello name of hello source cluster.</span></span>

     <span data-ttu-id="b5f86-204">當您抵達有游標的空白行時，請輸入一些文字訊息。</span><span class="sxs-lookup"><span data-stu-id="b5f86-204">When you arrive at a blank line with a cursor, type in a few text messages.</span></span> <span data-ttu-id="b5f86-205">這些系統會傳送 hello toohello 主題**來源**叢集。</span><span class="sxs-lookup"><span data-stu-id="b5f86-205">These are sent toohello topic on hello **source** cluster.</span></span> <span data-ttu-id="b5f86-206">完成後，使用**Ctrl + C** tooend hello 生產者程序。</span><span class="sxs-lookup"><span data-stu-id="b5f86-206">When done, use **Ctrl + C** tooend hello producer process.</span></span>

3. <span data-ttu-id="b5f86-207">從 hello SSH 連線 toohello**目的地**叢集，請使用**Ctrl + C** tooend hello MirrorMaker 程序。</span><span class="sxs-lookup"><span data-stu-id="b5f86-207">From hello SSH connection toohello **destination** cluster, use **Ctrl + C** tooend hello MirrorMaker process.</span></span> <span data-ttu-id="b5f86-208">然後使用 hello 下列命令 tooverify 該 hello`testtopic`主題建立，而且已 hello 主題中的資料已複寫的 toothis 鏡像：</span><span class="sxs-lookup"><span data-stu-id="b5f86-208">Then use hello following commands tooverify that hello `testtopic` topic was created, and that data in hello topic was replicated toothis mirror:</span></span>

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    <span data-ttu-id="b5f86-209">取代`$PASSWORD`hello 目的地叢集 hello （管理員） 登入密碼。</span><span class="sxs-lookup"><span data-stu-id="b5f86-209">Replace `$PASSWORD` with hello login (admin) password for hello destination cluster.</span></span>

    <span data-ttu-id="b5f86-210">取代`$CLUSTERNAME`hello hello 目的地叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="b5f86-210">Replace `$CLUSTERNAME` with hello name of hello destination cluster.</span></span>

    <span data-ttu-id="b5f86-211">hello 的主題清單現在包含`testtopic`，這在建立時 MirrorMaster 鏡像處理 hello 來源叢集 toohello 目的地從 hello 主題。</span><span class="sxs-lookup"><span data-stu-id="b5f86-211">hello list of topics now includes `testtopic`, which is created when MirrorMaster mirrors hello topic from hello source cluster toohello destination.</span></span> <span data-ttu-id="b5f86-212">擷取從 hello 主題的 hello 訊息是 hello 與 hello 來源叢集上輸入相同。</span><span class="sxs-lookup"><span data-stu-id="b5f86-212">hello messages retrieved from hello topic are hello same as entered on hello source cluster.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="b5f86-213">刪除 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="b5f86-213">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="b5f86-214">因為這份文件中的 hello 步驟建立這兩者中的叢集 hello 相同的 Azure 資源群組，您可以刪除 hello hello Azure 入口網站中的資源群組。</span><span class="sxs-lookup"><span data-stu-id="b5f86-214">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="b5f86-215">正在刪除 hello 資源群組中移除依照此文件、 hello Azure 虛擬網路和 hello 叢集所使用的儲存體帳戶建立的所有資源。</span><span class="sxs-lookup"><span data-stu-id="b5f86-215">Deleting hello resource group removes all resources created by following this document, hello Azure Virtual Network, and storage account used by hello clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5f86-216">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b5f86-216">Next Steps</span></span>

<span data-ttu-id="b5f86-217">在本文件中，您學會如何 toouse MirrorMaker toocreate Kafka 複本叢集。</span><span class="sxs-lookup"><span data-stu-id="b5f86-217">In this document, you learned how toouse MirrorMaker toocreate a replica of a Kafka cluster.</span></span> <span data-ttu-id="b5f86-218">使用下列連結 toodiscover hello 其他方式 toowork 與 Kafka:</span><span class="sxs-lookup"><span data-stu-id="b5f86-218">Use hello following links toodiscover other ways toowork with Kafka:</span></span>

* <span data-ttu-id="b5f86-219">[Apache Kafka MirrorMaker 文件](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) (網址為 cwiki.apache.org)。</span><span class="sxs-lookup"><span data-stu-id="b5f86-219">[Apache Kafka MirrorMaker documentation](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) at cwiki.apache.org.</span></span>
* [<span data-ttu-id="b5f86-220">開始使用 Apache Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="b5f86-220">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="b5f86-221">使用 Apache Spark 搭配 Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="b5f86-221">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="b5f86-222">使用 Apache Storm 搭配 HDInsight 上的 Kafka</span><span class="sxs-lookup"><span data-stu-id="b5f86-222">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="b5f86-223">透過 Azure 虛擬網路連線 tooKafka</span><span class="sxs-lookup"><span data-stu-id="b5f86-223">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
