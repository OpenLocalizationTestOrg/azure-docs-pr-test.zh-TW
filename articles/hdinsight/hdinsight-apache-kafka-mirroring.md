---
title: "鏡像 Apache Kafka 主題 - Azure HDInsight | Microsoft Docs"
description: "了解如何使用 Apache Kafka 的鏡像功能，藉由將主題鏡像處理至次要叢集來維護 HDInsight 叢集上的 Kafka 複本。"
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
ms.openlocfilehash: e418cb01e1a9168e3662e8d6242903e052b6047b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="use-mirrormaker-to-replicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a><span data-ttu-id="c7be3-103">使用 MirrorMaker，透過 HDInsight 上的 Kafka 來複寫 Apache Kafka 主題 (預覽)</span><span class="sxs-lookup"><span data-stu-id="c7be3-103">Use MirrorMaker to replicate Apache Kafka topics with Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="c7be3-104">了解如何使用 Apache Kafka 的鏡像功能，將主題複寫至次要叢集。</span><span class="sxs-lookup"><span data-stu-id="c7be3-104">Learn how to use Apache Kafka's mirroring feature to replicate topics to a secondary cluster.</span></span> <span data-ttu-id="c7be3-105">鏡像功能可以當作連續程序執行，或間歇地做為在叢集間移轉資料的方法。</span><span class="sxs-lookup"><span data-stu-id="c7be3-105">Mirroring can be ran as a continuous process, or used intermittently as a method of migrating data from one cluster to another.</span></span>

<span data-ttu-id="c7be3-106">在此範例中，會使用鏡像來複寫兩個 HDInsight 叢集之間的主題。</span><span class="sxs-lookup"><span data-stu-id="c7be3-106">In this example, mirroring is used to replicate topics between two HDInsight clusters.</span></span> <span data-ttu-id="c7be3-107">這兩個叢集是位於相同區域中的 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c7be3-107">Both clusters are in an Azure Virtual Network in the same region.</span></span>

> [!WARNING]
> <span data-ttu-id="c7be3-108">但不能將鏡像功能視為達成容錯的方法。</span><span class="sxs-lookup"><span data-stu-id="c7be3-108">Mirroring should not be considered as a means to achieve fault-tolerance.</span></span> <span data-ttu-id="c7be3-109">主題中的項目位移在來源與目的地叢集之間有所不同，所以用戶端無法交替使用這兩者。</span><span class="sxs-lookup"><span data-stu-id="c7be3-109">The offset to items within a topic are different between the source and destination clusters, so clients cannot use the two interchangeably.</span></span>
>
> <span data-ttu-id="c7be3-110">如果您很擔心容錯，您應該為叢集內的主題設定複寫。</span><span class="sxs-lookup"><span data-stu-id="c7be3-110">If you are concerned about fault tolerance, you should set replication for the topics within your cluster.</span></span> <span data-ttu-id="c7be3-111">如需詳細資訊，請參閱[開始使用 Kafka on HDInsight](hdinsight-apache-kafka-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="c7be3-111">For more information, see [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md).</span></span>

## <a name="how-kafka-mirroring-works"></a><span data-ttu-id="c7be3-112">Kafka 鏡像的運作方式</span><span class="sxs-lookup"><span data-stu-id="c7be3-112">How Kafka mirroring works</span></span>

<span data-ttu-id="c7be3-113">鏡像功能的運作方式是使用 MirrorMaker 工具 (Apache Kafka 的一部分)，取用來源叢集上主題中的記錄，然後在目的地叢集上建立本機複本。</span><span class="sxs-lookup"><span data-stu-id="c7be3-113">Mirroring works by using the MirrorMaker tool (part of Apache Kafka) to consume records from topics on the source cluster and then create a local copy on the destination cluster.</span></span> <span data-ttu-id="c7be3-114">MirrorMaker 會使用一個 (或多個) *取用者*從來源叢集讀取資料，以及使用一個*產生者*來將資料寫入本機 (目的地) 叢集。</span><span class="sxs-lookup"><span data-stu-id="c7be3-114">MirrorMaker uses one (or more) *consumers* that read from the source cluster, and a *producer* that writes to the local (destination) cluster.</span></span>

<span data-ttu-id="c7be3-115">下圖說明鏡像程序：</span><span class="sxs-lookup"><span data-stu-id="c7be3-115">The following diagram illustrates the Mirroring process:</span></span>

![鏡像程序圖表](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

<span data-ttu-id="c7be3-117">Apache Kafka on HDInsight 不提供透過公用網際網路存取 Kafka 服務。</span><span class="sxs-lookup"><span data-stu-id="c7be3-117">Apache Kafka on HDInsight does not provide access to the Kafka service over the public internet.</span></span> <span data-ttu-id="c7be3-118">Kafka 產生者和取用者必須與 Kafka 叢集中之節點位於相同的 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c7be3-118">Kafka producers or consumers must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="c7be3-119">例如，Kafka 來源和目的地叢集均位於 Azure 虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="c7be3-119">For this example, both the Kafka source and destination clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="c7be3-120">下圖顯示叢集之間的通訊流動方式︰</span><span class="sxs-lookup"><span data-stu-id="c7be3-120">The following diagram shows how communication flows between the clusters:</span></span>

![Azure 虛擬網路中的來源和目的地 Kafka 叢集圖表](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

<span data-ttu-id="c7be3-122">來源與目的地叢集的節點與磁碟分割數目可能有所不同，且主題中的位移也會不同。</span><span class="sxs-lookup"><span data-stu-id="c7be3-122">The source and destination clusters can be different in the number of nodes and partitions, and offsets within the topics are different also.</span></span> <span data-ttu-id="c7be3-123">鏡像功能會維護用於資料分割的金鑰值，因此會根據每個金鑰保留記錄順序。</span><span class="sxs-lookup"><span data-stu-id="c7be3-123">Mirroring maintains the key value that is used for partitioning, so record order is preserved on a per-key basis.</span></span>

### <a name="mirroring-across-network-boundaries"></a><span data-ttu-id="c7be3-124">跨網路界限鏡像</span><span class="sxs-lookup"><span data-stu-id="c7be3-124">Mirroring across network boundaries</span></span>

<span data-ttu-id="c7be3-125">如果您需要在不同網路中的 Kafka 叢集之間進行鏡像處理，有下列額外考量︰</span><span class="sxs-lookup"><span data-stu-id="c7be3-125">If you need to mirror between Kafka clusters in different networks, there are the following additional considerations:</span></span>

* <span data-ttu-id="c7be3-126">**閘道**：網路必須能夠在 TCPIP 層級進行通訊。</span><span class="sxs-lookup"><span data-stu-id="c7be3-126">**Gateways**: The networks must be able to communicate at the TCPIP level.</span></span>

* <span data-ttu-id="c7be3-127">**名稱解析**︰每個網路中的 Kafka 叢集必須能夠使用主機名稱彼此連接。</span><span class="sxs-lookup"><span data-stu-id="c7be3-127">**Name resolution**: The Kafka clusters in each network must be able to connect to each other by using hostnames.</span></span> <span data-ttu-id="c7be3-128">這可能會要求每個網路中的網域名稱系統 (DNS) 伺服器設定成將要求轉送到其他網路。</span><span class="sxs-lookup"><span data-stu-id="c7be3-128">This may require a Domain Name System (DNS) server in each network that is configured to forward requests to the other networks.</span></span>

    <span data-ttu-id="c7be3-129">建立 Azure 虛擬網路 (而不是使用網路提供的自動 DNS) 時，您必須指定自訂 DNS 伺服器和伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c7be3-129">When creating an Azure Virtual Network, instead of using the automatic DNS provided with the network, you must specify a custom DNS server and the IP address for the server.</span></span> <span data-ttu-id="c7be3-130">建立虛擬網路之後，您就必須建立使用該 IP 位址的 Azure 虛擬機器，然後在其上安裝和設定 DNS 軟體。</span><span class="sxs-lookup"><span data-stu-id="c7be3-130">After the Virtual Network has been created, you must then create an Azure Virtual Machine that uses that IP address, then install and configure DNS software on it.</span></span>

    > [!WARNING]
    > <span data-ttu-id="c7be3-131">先建立和設定自訂 DNS 伺服器，然後再將 HDInsight 安裝到虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="c7be3-131">Create and configure the custom DNS server before installing HDInsight into the Virtual Network.</span></span> <span data-ttu-id="c7be3-132">HDInsight 不需要進行其他設定，即可使用針對虛擬網路設定的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="c7be3-132">There is no additional configuration required for HDInsight to use the DNS server configured for the Virtual Network.</span></span>

<span data-ttu-id="c7be3-133">如需有關如何連接兩個 Azure 虛擬網路的詳細資訊，請參閱[設定 VNet 對 VNet 連線](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="c7be3-133">For more information on connecting two Azure Virtual Networks, see [Configure a VNet-to-VNet connection](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

## <a name="create-kafka-clusters"></a><span data-ttu-id="c7be3-134">建立 Kafka 叢集</span><span class="sxs-lookup"><span data-stu-id="c7be3-134">Create Kafka clusters</span></span>

<span data-ttu-id="c7be3-135">雖然您可以手動建立 Azure 虛擬網路和 Kafka 叢集，但使用 Azure Resource Manager 範本更輕鬆。</span><span class="sxs-lookup"><span data-stu-id="c7be3-135">While you can create an Azure virtual network and Kafka clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="c7be3-136">使用下列步驟將 Azure 虛擬網路和兩個 Kafka 叢集部署到 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c7be3-136">Use the following steps to deploy an Azure virtual network and two Kafka clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="c7be3-137">使用以下按鈕，在 Azure 入口網站中登入 Azure 並開啟範本。</span><span class="sxs-lookup"><span data-stu-id="c7be3-137">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy to Azure"></a>
   
    <span data-ttu-id="c7be3-138">Azure Resource Manager 範本位於 **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**。</span><span class="sxs-lookup"><span data-stu-id="c7be3-138">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="c7be3-139">若要保證 Kafka 在 HDInsight 上的可用性，您的叢集必須包含至少三個背景工作角色節點。</span><span class="sxs-lookup"><span data-stu-id="c7be3-139">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="c7be3-140">此範本會建立包含三個背景工作角色節點的 Kafka 叢集。</span><span class="sxs-lookup"><span data-stu-id="c7be3-140">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="c7be3-141">使用下列資訊來填入 [自訂部署] 刀鋒視窗上的項目︰</span><span class="sxs-lookup"><span data-stu-id="c7be3-141">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
    
    ![HDInsight 自訂部署](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * <span data-ttu-id="c7be3-143">**資源群組**：建立群組或選取現有的群組。</span><span class="sxs-lookup"><span data-stu-id="c7be3-143">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="c7be3-144">此群組包含 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="c7be3-144">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="c7be3-145">**位置**：選取在地理上靠近您的位置。</span><span class="sxs-lookup"><span data-stu-id="c7be3-145">**Location**: Select a location geographically close to you.</span></span>
     
    * <span data-ttu-id="c7be3-146">**基底叢集名稱**︰此值會做為 Kafka 叢集的基底名稱。</span><span class="sxs-lookup"><span data-stu-id="c7be3-146">**Base Cluster Name**: This value is used as the base name for the Kafka clusters.</span></span> <span data-ttu-id="c7be3-147">例如，輸入 **hdi** 可建立名為 **source-hdi** 和 **dest-hdi** 的叢集。</span><span class="sxs-lookup"><span data-stu-id="c7be3-147">For example, entering **hdi** creates clusters named **source-hdi** and **dest-hdi**.</span></span>

    * <span data-ttu-id="c7be3-148">**叢集登入使用者名稱**：來源和目的地 Kafka 叢集的系統管理員使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="c7be3-148">**Cluster Login User Name**: The admin user name for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="c7be3-149">**叢集登入密碼**：來源和目的地 Kafka 叢集的系統管理員使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="c7be3-149">**Cluster Login Password**: The admin user password for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="c7be3-150">**SSH 使用者名稱**：建立來源和目的地 Kafka 叢集的 SSH 使用者。</span><span class="sxs-lookup"><span data-stu-id="c7be3-150">**SSH User Name**: The SSH user to create for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="c7be3-151">**SSH 密碼**：來源和目的地 Kafka 叢集的 SSH 使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="c7be3-151">**SSH Password**: The password for the SSH user for the source and destination Kafka clusters.</span></span>

3. <span data-ttu-id="c7be3-152">讀取**條款及條件**，然後選取 [我同意上方所述的條款及條件]。</span><span class="sxs-lookup"><span data-stu-id="c7be3-152">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="c7be3-153">最後，核取 [釘選到儀表板]，然後選取 [購買]。</span><span class="sxs-lookup"><span data-stu-id="c7be3-153">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="c7be3-154">大約需要 20 分鐘的時間來建立叢集。</span><span class="sxs-lookup"><span data-stu-id="c7be3-154">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="c7be3-155">建立資源後，您會重新導向至資源群組的刀鋒視窗，其中內含叢集和 Web 儀表板。</span><span class="sxs-lookup"><span data-stu-id="c7be3-155">Once the resources have been created, you are redirected to a blade for the resource group that contains the clusters and web dashboard.</span></span>

![Vnet 和叢集的資源群組刀鋒視窗](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="c7be3-157">請注意，HDInsight 叢集的名稱是 **source-BASENAME** 和 **dest-BASENAME**，其中 BASENAME 是您提供給範本的名稱。</span><span class="sxs-lookup"><span data-stu-id="c7be3-157">Notice that the names of the HDInsight clusters are **source-BASENAME** and **dest-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="c7be3-158">連接到叢集時，您會在稍後步驟中使用這些名稱。</span><span class="sxs-lookup"><span data-stu-id="c7be3-158">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="create-topics"></a><span data-ttu-id="c7be3-159">建立主題</span><span class="sxs-lookup"><span data-stu-id="c7be3-159">Create topics</span></span>

1. <span data-ttu-id="c7be3-160">使用 SSH 連接到**來源**叢集：</span><span class="sxs-lookup"><span data-stu-id="c7be3-160">Connect to the **source** cluster using SSH:</span></span>

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="c7be3-161">將 **sshuser** 替換為建立叢集時所使用的 SSH 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="c7be3-161">Replace **sshuser** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="c7be3-162">將 **BASENAME** 替換為建立叢集時使用的基底名稱。</span><span class="sxs-lookup"><span data-stu-id="c7be3-162">Replace **BASENAME** with the base name used when creating the cluster.</span></span>

    <span data-ttu-id="c7be3-163">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="c7be3-163">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="c7be3-164">使用下列命令為來源叢集尋找 Zookeeper 主機：</span><span class="sxs-lookup"><span data-stu-id="c7be3-164">Use the following commands to find the Zookeeper hosts for the source cluster:</span></span>

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get the zookeeper hosts for the source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with the password for the cluster.

    Replace `$CLUSTERNAME` with the name of the source cluster.

3. To create a topic named `testtopic`, use the following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. <span data-ttu-id="c7be3-165">使用下列命令確認已建立主題：</span><span class="sxs-lookup"><span data-stu-id="c7be3-165">Use the following command to verify that the topic was created:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="c7be3-166">回應包含 `testtopic`。</span><span class="sxs-lookup"><span data-stu-id="c7be3-166">The response contains `testtopic`.</span></span>

4. <span data-ttu-id="c7be3-167">使用下列命令來檢視這個 (**來源**) 叢集的 Zookeeper 主機資訊︰</span><span class="sxs-lookup"><span data-stu-id="c7be3-167">Use the following to view the Zookeeper host information for this (the **source**) cluster:</span></span>

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="c7be3-168">此命令會傳回類似以下文字的資訊：</span><span class="sxs-lookup"><span data-stu-id="c7be3-168">This returns information similar to the following text:</span></span>

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    <span data-ttu-id="c7be3-169">請儲存此資訊。</span><span class="sxs-lookup"><span data-stu-id="c7be3-169">Save this information.</span></span> <span data-ttu-id="c7be3-170">此資訊使用於下一節。</span><span class="sxs-lookup"><span data-stu-id="c7be3-170">It is used in the next section.</span></span>

## <a name="configure-mirroring"></a><span data-ttu-id="c7be3-171">設定鏡像功能</span><span class="sxs-lookup"><span data-stu-id="c7be3-171">Configure mirroring</span></span>

1. <span data-ttu-id="c7be3-172">使用不同的 SSH 工作階段連接到**目的地**叢集：</span><span class="sxs-lookup"><span data-stu-id="c7be3-172">Connect to the **destination** cluster using a different SSH session:</span></span>

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="c7be3-173">將 **sshuser** 替換為建立叢集時所使用的 SSH 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="c7be3-173">Replace **sshuser** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="c7be3-174">將 **BASENAME** 替換為建立叢集時使用的基底名稱。</span><span class="sxs-lookup"><span data-stu-id="c7be3-174">Replace **BASENAME** with the base name used when creating the cluster.</span></span>

    <span data-ttu-id="c7be3-175">如需相關資訊，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md)。</span><span class="sxs-lookup"><span data-stu-id="c7be3-175">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="c7be3-176">使用下列命令來建立 `consumer.properties` 檔案，其中描述如何與**來源**叢集通訊︰</span><span class="sxs-lookup"><span data-stu-id="c7be3-176">Use the following command to create a `consumer.properties` file that describes how to communicate with the **source** cluster:</span></span>

    ```bash
    nano consumer.properties
    ```

    <span data-ttu-id="c7be3-177">使用下列文字做為 `consumer.properties` 檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="c7be3-177">Use the following text as the contents of the `consumer.properties` file:</span></span>

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    <span data-ttu-id="c7be3-178">以**來源**叢集中的 Zookeeper 主機資訊取代 **SOURCE_ZKHOSTS**。</span><span class="sxs-lookup"><span data-stu-id="c7be3-178">Replace **SOURCE_ZKHOSTS** with the Zookeeper hosts information from the **source** cluster.</span></span>

    <span data-ttu-id="c7be3-179">此檔案描述從來源 Kafka 叢集讀取資料時所要使用的取用者資訊。</span><span class="sxs-lookup"><span data-stu-id="c7be3-179">This file describes the consumer information to use when reading from the source Kafka cluster.</span></span> <span data-ttu-id="c7be3-180">如需取用者組態詳細資訊，請參閱 kafka.apache.org 上的[取用者組態](https://kafka.apache.org/documentation#consumerconfigs)。</span><span class="sxs-lookup"><span data-stu-id="c7be3-180">For more information consumer configuration, see [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) at kafka.apache.org.</span></span>

    <span data-ttu-id="c7be3-181">若要儲存檔案，請使用 **Ctrl + X**、**Y** 和 **Enter** 鍵。</span><span class="sxs-lookup"><span data-stu-id="c7be3-181">To save the file, use **Ctrl + X**, **Y**, and then **Enter**.</span></span>

3. <span data-ttu-id="c7be3-182">在設定可與目的地叢集通訊的產生者之前，您必須尋找**目的地**叢集的訊息代理程式主機。</span><span class="sxs-lookup"><span data-stu-id="c7be3-182">Before configuring the producer that communicates with the destination cluster, you must find the broker hosts for the **destination** cluster.</span></span> <span data-ttu-id="c7be3-183">請使用下列命令來擷取此資訊：</span><span class="sxs-lookup"><span data-stu-id="c7be3-183">Use the following commands to retrieve this information:</span></span>

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    <span data-ttu-id="c7be3-184">將 `$PASSWORD` 取代為叢集登入帳戶 (管理員) 的密碼。</span><span class="sxs-lookup"><span data-stu-id="c7be3-184">Replace `$PASSWORD` with the login account (admin) password for the cluster.</span></span>

    <span data-ttu-id="c7be3-185">將 `$CLUSTERNAME` 取代為目的地叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="c7be3-185">Replace `$CLUSTERNAME` with the name of the destination cluster.</span></span>

    <span data-ttu-id="c7be3-186">這些命令會傳回類似以下的資訊：</span><span class="sxs-lookup"><span data-stu-id="c7be3-186">These commands return information similar to the following:</span></span>

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. <span data-ttu-id="c7be3-187">使用下列命令來建立 `producer.properties` 檔案，其中描述如何與**目的地**叢集通訊︰</span><span class="sxs-lookup"><span data-stu-id="c7be3-187">Use the following to create a `producer.properties` file that describes how to communicate with the **destination** cluster:</span></span>

    ```bash
    nano producer.properties
    ```

    <span data-ttu-id="c7be3-188">使用下列文字做為 `producer.properties` 檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="c7be3-188">Use the following text as the contents of the `producer.properties` file:</span></span>

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    <span data-ttu-id="c7be3-189">以上一個步驟中的訊息代理程式資訊取代 **DEST_BROKERS**。</span><span class="sxs-lookup"><span data-stu-id="c7be3-189">Replace **DEST_BROKERS** with the broker information from the previous step.</span></span>

    <span data-ttu-id="c7be3-190">如需產生者組態詳細資訊，請參閱 kafka.apache.org 上的[者組態](https://kafka.apache.org/documentation#producerconfigs)。</span><span class="sxs-lookup"><span data-stu-id="c7be3-190">For more information producer configuration, see [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) at kafka.apache.org.</span></span>

## <a name="start-mirrormaker"></a><span data-ttu-id="c7be3-191">啟動 MirrorMaker</span><span class="sxs-lookup"><span data-stu-id="c7be3-191">Start MirrorMaker</span></span>

1. <span data-ttu-id="c7be3-192">在連往**目的地**叢集的 SSH 連線中，使用下列命令來啟動 MirrorMaker 程序：</span><span class="sxs-lookup"><span data-stu-id="c7be3-192">From the SSH connection to the **destination** cluster, use the following command to start the MirrorMaker process:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    <span data-ttu-id="c7be3-193">此範例中使用的參數：</span><span class="sxs-lookup"><span data-stu-id="c7be3-193">The parameters used in this example are:</span></span>

    * <span data-ttu-id="c7be3-194">**--consumer.config**︰指定包含取用者屬性的檔案。</span><span class="sxs-lookup"><span data-stu-id="c7be3-194">**--consumer.config**: Specifies the file that contains consumer properties.</span></span> <span data-ttu-id="c7be3-195">這些屬性用來建立可從*來源* Kafka 叢集讀取資料的取用者。</span><span class="sxs-lookup"><span data-stu-id="c7be3-195">These properties are used to create a consumer that reads from the *source* Kafka cluster.</span></span>

    * <span data-ttu-id="c7be3-196">**--producer.config**︰指定包含產生者屬性的檔案。</span><span class="sxs-lookup"><span data-stu-id="c7be3-196">**--producer.config**: Specifies the file that contains producer properties.</span></span> <span data-ttu-id="c7be3-197">這些屬性用來建立可寫入*目的地* Kafka 叢集的產生者。</span><span class="sxs-lookup"><span data-stu-id="c7be3-197">These properties are used to create a producer that writes to the *destination* Kafka cluster.</span></span>

    * <span data-ttu-id="c7be3-198">**--whitelist**：MirrorMaker 從來源叢集複寫至目的地的主題清單。</span><span class="sxs-lookup"><span data-stu-id="c7be3-198">**--whitelist**: A list of topics that MirrorMaker replicates from the source cluster to the destination.</span></span>

    * <span data-ttu-id="c7be3-199">**--num.streams**︰要建立的取用者執行緒數目。</span><span class="sxs-lookup"><span data-stu-id="c7be3-199">**--num.streams**: The number of consumer threads to create.</span></span>

 <span data-ttu-id="c7be3-200">啟動時，MirrorMaker 會傳回類似以下文字的資訊：</span><span class="sxs-lookup"><span data-stu-id="c7be3-200">On startup, MirrorMaker returns information similar to the following text:</span></span>

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. <span data-ttu-id="c7be3-201">從連往**來源**叢集的 SSH 連線中，使用下列命令來啟動產生者，然後傳送訊息到主題：</span><span class="sxs-lookup"><span data-stu-id="c7be3-201">From the SSH connection to the **source** cluster, use the following command to start a producer and send messages to the topic:</span></span>

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    <span data-ttu-id="c7be3-202">將 `$PASSWORD` 取代為來源叢集的 (管理員) 密碼。</span><span class="sxs-lookup"><span data-stu-id="c7be3-202">Replace `$PASSWORD` with the login (admin) password for the source cluster.</span></span>

    <span data-ttu-id="c7be3-203">將 `$CLUSTERNAME` 取代為來源叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="c7be3-203">Replace `$CLUSTERNAME` with the name of the source cluster.</span></span>

     <span data-ttu-id="c7be3-204">當您抵達有游標的空白行時，請輸入一些文字訊息。</span><span class="sxs-lookup"><span data-stu-id="c7be3-204">When you arrive at a blank line with a cursor, type in a few text messages.</span></span> <span data-ttu-id="c7be3-205">這些文字會傳送到**來源**叢集上的主題。</span><span class="sxs-lookup"><span data-stu-id="c7be3-205">These are sent to the topic on the **source** cluster.</span></span> <span data-ttu-id="c7be3-206">完成後，使用 **Ctrl + C** 結束產生者程序。</span><span class="sxs-lookup"><span data-stu-id="c7be3-206">When done, use **Ctrl + C** to end the producer process.</span></span>

3. <span data-ttu-id="c7be3-207">在連往**目的地**叢集的 SSH 連線中，使用 **Ctrl + C** 來結束 MirrorMaker 程序。</span><span class="sxs-lookup"><span data-stu-id="c7be3-207">From the SSH connection to the **destination** cluster, use **Ctrl + C** to end the MirrorMaker process.</span></span> <span data-ttu-id="c7be3-208">然後使用下列命令確認已建立 `testtopic` 主題，而且主題中的資料已複寫到這個鏡像︰</span><span class="sxs-lookup"><span data-stu-id="c7be3-208">Then use the following commands to verify that the `testtopic` topic was created, and that data in the topic was replicated to this mirror:</span></span>

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    <span data-ttu-id="c7be3-209">將 `$PASSWORD` 取代為目的地叢集的 (管理員) 密碼。</span><span class="sxs-lookup"><span data-stu-id="c7be3-209">Replace `$PASSWORD` with the login (admin) password for the destination cluster.</span></span>

    <span data-ttu-id="c7be3-210">將 `$CLUSTERNAME` 取代為目的地叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="c7be3-210">Replace `$CLUSTERNAME` with the name of the destination cluster.</span></span>

    <span data-ttu-id="c7be3-211">主題清單現在包含 `testtopic`，它是在 MirrorMaster 將主題從來源叢集鏡射至目的地時所建立。</span><span class="sxs-lookup"><span data-stu-id="c7be3-211">The list of topics now includes `testtopic`, which is created when MirrorMaster mirrors the topic from the source cluster to the destination.</span></span> <span data-ttu-id="c7be3-212">從主題中擷取的訊息與在來源叢集上所輸入的相同。</span><span class="sxs-lookup"><span data-stu-id="c7be3-212">The messages retrieved from the topic are the same as entered on the source cluster.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="c7be3-213">刪除叢集</span><span class="sxs-lookup"><span data-stu-id="c7be3-213">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="c7be3-214">因為本文件中的步驟會在相同的 Azure 資源群組中建立兩個叢集，您可以在 Azure 入口網站中刪除資源群組。</span><span class="sxs-lookup"><span data-stu-id="c7be3-214">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="c7be3-215">刪除資源群組，即可移除依循本文件建立的所有資源、Azure 虛擬網路，以及叢集所使用的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c7be3-215">Deleting the resource group removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c7be3-216">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c7be3-216">Next Steps</span></span>

<span data-ttu-id="c7be3-217">在本文件中，您已學會如何使用 MirrorMaker 建立 Kafka 叢集的複本。</span><span class="sxs-lookup"><span data-stu-id="c7be3-217">In this document, you learned how to use MirrorMaker to create a replica of a Kafka cluster.</span></span> <span data-ttu-id="c7be3-218">使用下列連結來探索使用 Kafka 的其他方式︰</span><span class="sxs-lookup"><span data-stu-id="c7be3-218">Use the following links to discover other ways to work with Kafka:</span></span>

* <span data-ttu-id="c7be3-219">[Apache Kafka MirrorMaker 文件](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) (網址為 cwiki.apache.org)。</span><span class="sxs-lookup"><span data-stu-id="c7be3-219">[Apache Kafka MirrorMaker documentation](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) at cwiki.apache.org.</span></span>
* [<span data-ttu-id="c7be3-220">開始使用 Apache Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7be3-220">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="c7be3-221">使用 Apache Spark 搭配 Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7be3-221">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="c7be3-222">使用 Apache Storm 搭配 Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="c7be3-222">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="c7be3-223">透過 Azure 虛擬網路連線到 Kafka</span><span class="sxs-lookup"><span data-stu-id="c7be3-223">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
