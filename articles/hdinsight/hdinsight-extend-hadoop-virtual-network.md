---
title: "使用虛擬網路延伸 HDInsight - Azure | Microsoft Docs"
description: "了解如何使用 Azure 虛擬網路將 HDInsight 連接到其他雲端資源或您的資料中心內的資源"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 37b9b600-d7f8-4cb1-a04a-0b3a827c6dcc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: larryfr
ms.openlocfilehash: 380423ec42ad4905c73fcd57501102e9f7062e81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a><span data-ttu-id="b3f53-103">使用 Azure 虛擬網路延伸 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b3f53-103">Extend Azure HDInsight using an Azure Virtual Network</span></span>

<span data-ttu-id="b3f53-104">了解如何搭配使用 HDInsight 與 [Azure 虛擬網路](../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="b3f53-104">Learn how to use HDInsight with an [Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="b3f53-105">使用 Azure 虛擬網路可啟用下列案例：</span><span class="sxs-lookup"><span data-stu-id="b3f53-105">Using an Azure Virtual Network enables the following scenarios:</span></span>

* <span data-ttu-id="b3f53-106">從內部部署網路直接連線至 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="b3f53-106">Connecting to HDInsight directly from an on-premises network.</span></span>

* <span data-ttu-id="b3f53-107">將 HDInsight 連線至 Azure 虛擬網路中的資料存放區。</span><span class="sxs-lookup"><span data-stu-id="b3f53-107">Connecting HDInsight to data stores in an Azure Virtual network.</span></span>

* <span data-ttu-id="b3f53-108">直接存取無法透過網際網路公開使用的 Hadoop 服務。</span><span class="sxs-lookup"><span data-stu-id="b3f53-108">Directly accessing Hadoop services that are not available publicly over the internet.</span></span> <span data-ttu-id="b3f53-109">例如，Kafka API 或 HBase Java API。</span><span class="sxs-lookup"><span data-stu-id="b3f53-109">For example, Kafka APIs or the HBase Java API.</span></span>

> [!WARNING]
> <span data-ttu-id="b3f53-110">本文件中的資訊需要了解 TCP/IP 網路。</span><span class="sxs-lookup"><span data-stu-id="b3f53-110">The information in this document requires an understanding of TCP/IP networking.</span></span> <span data-ttu-id="b3f53-111">如果您不熟悉 TCP/IP 網路，則應該與之前在生產網路中修改的人員合作。</span><span class="sxs-lookup"><span data-stu-id="b3f53-111">If you are not familiar with TCP/IP networking, you should partner with someone who is before making modifications to production networks.</span></span>

## <a name="planning"></a><span data-ttu-id="b3f53-112">規劃</span><span class="sxs-lookup"><span data-stu-id="b3f53-112">Planning</span></span>

<span data-ttu-id="b3f53-113">規劃在虛擬網路中安裝 HDInsight 時，您必須回答的問題如下：</span><span class="sxs-lookup"><span data-stu-id="b3f53-113">The following are the questions that you must answer when planning to install HDInsight in a virtual network:</span></span>

* <span data-ttu-id="b3f53-114">您需要將 HDInsight 安裝到現有虛擬網路嗎？</span><span class="sxs-lookup"><span data-stu-id="b3f53-114">Do you need to install HDInsight into an existing virtual network?</span></span> <span data-ttu-id="b3f53-115">或者，您要建立新的網路嗎？</span><span class="sxs-lookup"><span data-stu-id="b3f53-115">Or are you creating a new network?</span></span>

    <span data-ttu-id="b3f53-116">如果您要使用現有虛擬網路，則可能需要先修改網路設定，才能安裝 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="b3f53-116">If you are using an existing virtual network, you may need to modify the network configuration before you can install HDInsight.</span></span> <span data-ttu-id="b3f53-117">如需詳細資訊，請參閱[將 HDInsight 新增至現有虛擬網路](#existingvnet)一節。</span><span class="sxs-lookup"><span data-stu-id="b3f53-117">For more information, see the [add HDInsight to an existing virtual network](#existingvnet) section.</span></span>

* <span data-ttu-id="b3f53-118">您要將包含 HDInsight 的虛擬網路連線至另一個虛擬網路或內部部署網路嗎？</span><span class="sxs-lookup"><span data-stu-id="b3f53-118">Do you want to connect the virtual network containing HDInsight to another virtual network or your on-premises network?</span></span>

    <span data-ttu-id="b3f53-119">若要輕鬆地跨網路使用資源，您可能需要建立自訂 DNS，並設定 DNS 轉送。</span><span class="sxs-lookup"><span data-stu-id="b3f53-119">To easily work with resources across networks, you may need to create a custom DNS and configure DNS forwarding.</span></span> <span data-ttu-id="b3f53-120">如需詳細資訊，請參閱[連線多個網路](#multinet)一節。</span><span class="sxs-lookup"><span data-stu-id="b3f53-120">For more information, see the [connecting multiple networks](#multinet) section.</span></span>

* <span data-ttu-id="b3f53-121">您要將輸入或輸出流量限制/重新導向至 HDInsight 嗎？</span><span class="sxs-lookup"><span data-stu-id="b3f53-121">Do you want to restrict/redirect inbound or outbound traffic to HDInsight?</span></span>

    <span data-ttu-id="b3f53-122">HDInsight 必須具有 Azure 資料中心內特定 IP 位址的無限制通訊。</span><span class="sxs-lookup"><span data-stu-id="b3f53-122">HDInsight must have unrestricted communication with specific IP addresses in the Azure data center.</span></span> <span data-ttu-id="b3f53-123">另外還有數個連接埠必須允許通過防火牆才能進行用戶端通訊。</span><span class="sxs-lookup"><span data-stu-id="b3f53-123">There are also several ports that must be allowed through firewalls for client communication.</span></span> <span data-ttu-id="b3f53-124">如需詳細資訊，請參閱[控制網路流量](#networktraffic)一節。</span><span class="sxs-lookup"><span data-stu-id="b3f53-124">For more information, see the [controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="b3f53-125"><a id="existingvnet"></a>將 HDInsight 新增至現有虛擬網路</span><span class="sxs-lookup"><span data-stu-id="b3f53-125"><a id="existingvnet"></a>Add HDInsight to an existing virtual network</span></span>

<span data-ttu-id="b3f53-126">使用本節中的步驟，以了解如何將新的 HDInsight 新增至現有 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b3f53-126">Use the steps in this section to discover how to add a new HDInsight to an existing Azure Virtual Network.</span></span>

> [!NOTE]
> <span data-ttu-id="b3f53-127">您無法在虛擬網路中新增現有的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="b3f53-127">You cannot add an existing HDInsight cluster into a virtual network.</span></span>

1. <span data-ttu-id="b3f53-128">您要使用虛擬網路的傳統或 Resource Manager 部署模型嗎？</span><span class="sxs-lookup"><span data-stu-id="b3f53-128">Are you using a classic or Resource Manager deployment model for the virtual network?</span></span>

    <span data-ttu-id="b3f53-129">HDInsight 3.4 和更新版本需要 Resource Manager 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b3f53-129">HDInsight 3.4 and greater requires a Resource Manager virtual network.</span></span> <span data-ttu-id="b3f53-130">舊版 HDInsight 需要傳統虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b3f53-130">Earlier versions of HDInsight required a classic virtual network.</span></span>

    <span data-ttu-id="b3f53-131">如果您的現有網路是傳統虛擬網路，則必須建立 Resource Manager 虛擬網路，然後連線兩者。</span><span class="sxs-lookup"><span data-stu-id="b3f53-131">If your existing network is a classic virtual network, then you must create a Resource Manager virtual network and then connect the two.</span></span> <span data-ttu-id="b3f53-132">[將傳統 VNet 連線至新的 VNet](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="b3f53-132">[Connecting classic VNets to new VNets](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span></span>

    <span data-ttu-id="b3f53-133">加入之後，Resource Manager 網路中所安裝的 HDInsight 就可以與傳統網路中的資源互動。</span><span class="sxs-lookup"><span data-stu-id="b3f53-133">Once joined, HDInsight installed in the Resource Manager network can interact with resources in the classic network.</span></span>

2. <span data-ttu-id="b3f53-134">您使用強制通道嗎？</span><span class="sxs-lookup"><span data-stu-id="b3f53-134">Do you use forced tunneling?</span></span> <span data-ttu-id="b3f53-135">強制通道是一種子網路設定，可強制裝置的輸出網際網路流量以進行檢查和記錄。</span><span class="sxs-lookup"><span data-stu-id="b3f53-135">Forced tunneling is a subnet setting that forces outbound Internet traffic to a device for inspection and logging.</span></span> <span data-ttu-id="b3f53-136">HDInsight 不支援強制通道。</span><span class="sxs-lookup"><span data-stu-id="b3f53-136">HDInsight does not support forced tunneling.</span></span> <span data-ttu-id="b3f53-137">先移除強制通道，再將 HDInsight 安裝至子網路，或建立 HDInsight 的新子網路。</span><span class="sxs-lookup"><span data-stu-id="b3f53-137">Either remove forced tunneling before installing HDInsight into a subnet, or create a new subnet for HDInsight.</span></span>

3. <span data-ttu-id="b3f53-138">您使用網路安全性群組、使用者定義路由或虛擬網路設備來限制傳入或傳出虛擬網路的流量嗎？</span><span class="sxs-lookup"><span data-stu-id="b3f53-138">Do you use network security groups, user-defined routes, or Virtual Network Appliances to restrict traffic into or out of the virtual network?</span></span>

    <span data-ttu-id="b3f53-139">HDInsight 是一個受管理服務，需要 Azure 資料中心內數個 IP 位址的無限制存取權。</span><span class="sxs-lookup"><span data-stu-id="b3f53-139">As a managed service, HDInsight requires unrestricted access to several IP addresses in the Azure data center.</span></span> <span data-ttu-id="b3f53-140">若要允許與這些 IP 位址的通訊，請更新任何現有網路安全性群組或使用者定義路由。</span><span class="sxs-lookup"><span data-stu-id="b3f53-140">To allow communication with these IP addresses, update any existing network security groups or user-defined routes.</span></span>

    <span data-ttu-id="b3f53-141">HDInsight 會裝載多個使用各種連接埠的服務。</span><span class="sxs-lookup"><span data-stu-id="b3f53-141">HDInsight  hosts multiple services, which use a variety of ports.</span></span> <span data-ttu-id="b3f53-142">不會封鎖對這些連接埠的流量。</span><span class="sxs-lookup"><span data-stu-id="b3f53-142">Do not block traffic to these ports.</span></span> <span data-ttu-id="b3f53-143">如需允許通過虛擬設備防火牆的連接埠清單，請參閱[安全性](#security)一節。</span><span class="sxs-lookup"><span data-stu-id="b3f53-143">For a list of ports to allow through virtual appliance firewalls, see the [Security](#security) section.</span></span>

    <span data-ttu-id="b3f53-144">若要尋找現有安全性設定，請使用下列 Azure PowerShell 或 Azure CLI 命令：</span><span class="sxs-lookup"><span data-stu-id="b3f53-144">To find your existing security configuration, use the following Azure PowerShell or Azure CLI commands:</span></span>

    * <span data-ttu-id="b3f53-145">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="b3f53-145">Network security groups</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="b3f53-146">如需詳細資訊，請參閱[為網路安全性群組疑難排解](../virtual-network/virtual-network-nsg-troubleshoot-portal.md)文件。</span><span class="sxs-lookup"><span data-stu-id="b3f53-146">For more information, see the [Troubleshoot network security groups](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) document.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="b3f53-147">會根據規則優先順序依序套用網路安全性群組規則。</span><span class="sxs-lookup"><span data-stu-id="b3f53-147">Network security group rules are applied in order based on rule priority.</span></span> <span data-ttu-id="b3f53-148">會套用第一個符合流量模式的規則，而且未針對該流量套用其他規則。</span><span class="sxs-lookup"><span data-stu-id="b3f53-148">The first rule that matches the traffic pattern is applied, and no others are applied for that traffic.</span></span> <span data-ttu-id="b3f53-149">排序從最寬鬆到最嚴格權限的規則。</span><span class="sxs-lookup"><span data-stu-id="b3f53-149">Order rules from most permissive to least permissive.</span></span> <span data-ttu-id="b3f53-150">如需詳細資訊，請參閱[使用網路安全性群組來篩選網路流量](../virtual-network/virtual-networks-nsg.md)文件。</span><span class="sxs-lookup"><span data-stu-id="b3f53-150">For more information, see the [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    * <span data-ttu-id="b3f53-151">使用者定義的路由</span><span class="sxs-lookup"><span data-stu-id="b3f53-151">User-defined routes</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="b3f53-152">如需詳細資訊，請參閱[為路由疑難排解](../virtual-network/virtual-network-routes-troubleshoot-portal.md)文件。</span><span class="sxs-lookup"><span data-stu-id="b3f53-152">For more information, see the [Troubleshoot routes](../virtual-network/virtual-network-routes-troubleshoot-portal.md) document.</span></span>

4. <span data-ttu-id="b3f53-153">建立 HDInsight 叢集，並在設定期間選擇 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b3f53-153">Create an HDInsight cluster and select the Azure Virtual Network during configuration.</span></span> <span data-ttu-id="b3f53-154">使用下列文件中的步驟，以了解叢集建立程序：</span><span class="sxs-lookup"><span data-stu-id="b3f53-154">Use the steps in the following documents to understand the cluster creation process:</span></span>

    * [<span data-ttu-id="b3f53-155">使用 Azure 入口網站建立 HDInsight</span><span class="sxs-lookup"><span data-stu-id="b3f53-155">Create HDInsight using the Azure portal</span></span>](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [<span data-ttu-id="b3f53-156">使用 Azure PowerShell 建立 HDInsight</span><span class="sxs-lookup"><span data-stu-id="b3f53-156">Create HDInsight using Azure PowerShell</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [<span data-ttu-id="b3f53-157">使用 Azure CLI 1.0 建立 HDInsight</span><span class="sxs-lookup"><span data-stu-id="b3f53-157">Create HDInsight using Azure CLI 1.0</span></span>](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [<span data-ttu-id="b3f53-158">使用 Azure Resource Manager 範本建立 HDInsight</span><span class="sxs-lookup"><span data-stu-id="b3f53-158">Create HDInsight using an Azure Resource Manager template</span></span>](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > <span data-ttu-id="b3f53-159">將 HDInsight 新增至虛擬網路是選擇性的設定步驟。</span><span class="sxs-lookup"><span data-stu-id="b3f53-159">Adding HDInsight to a virtual network is an optional configuration step.</span></span> <span data-ttu-id="b3f53-160">請務必在設定叢集時選取虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b3f53-160">Be sure to select the virtual network when configuring the cluster.</span></span>

## <span data-ttu-id="b3f53-161"><a id="multinet"></a>連線多個網路</span><span class="sxs-lookup"><span data-stu-id="b3f53-161"><a id="multinet"></a>Connecting multiple networks</span></span>

<span data-ttu-id="b3f53-162">多網路設定的最大挑戰是網路之間的名稱解析。</span><span class="sxs-lookup"><span data-stu-id="b3f53-162">The biggest challenge with a multi-network configuration is name resolution between the networks.</span></span>

<span data-ttu-id="b3f53-163">Azure 會針對安裝於虛擬網路中的 Azure 服務提供名稱解析。</span><span class="sxs-lookup"><span data-stu-id="b3f53-163">Azure provides name resolution for Azure services that are installed in a virtual network.</span></span> <span data-ttu-id="b3f53-164">這個內建名稱解析允許 HDInsight 使用完整網域名稱 (FQDN) 連線至下列資源：</span><span class="sxs-lookup"><span data-stu-id="b3f53-164">This built-in name resolution allows HDInsight to connect to the following resources by using a fully qualified domain name (FQDN):</span></span>

* <span data-ttu-id="b3f53-165">網際網路上的任何可用資源。</span><span class="sxs-lookup"><span data-stu-id="b3f53-165">Any resource that is available on the internet.</span></span> <span data-ttu-id="b3f53-166">例如，microsoft.com、google.com。</span><span class="sxs-lookup"><span data-stu-id="b3f53-166">For example, microsoft.com, google.com.</span></span>

* <span data-ttu-id="b3f53-167">相同 Azure 虛擬網路中的任何資源，方法是使用資源的「內部 DNS 名稱」。</span><span class="sxs-lookup"><span data-stu-id="b3f53-167">Any resource that is in the same Azure Virtual Network, by using the __internal DNS name__ of the resource.</span></span> <span data-ttu-id="b3f53-168">例如，使用預設名稱解析時，以下是指派給 HDInsight 背景工作節點的範例內部 DNS 名稱：</span><span class="sxs-lookup"><span data-stu-id="b3f53-168">For example, when using the default name resolution, the following are example internal DNS names assigned to HDInsight worker nodes:</span></span>

    * <span data-ttu-id="b3f53-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="b3f53-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>
    * <span data-ttu-id="b3f53-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="b3f53-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>

    <span data-ttu-id="b3f53-171">這些節點可以使用內部 DNS 名稱彼此直接通訊，以及與 HDInsight 中的其他節點通訊。</span><span class="sxs-lookup"><span data-stu-id="b3f53-171">Both these nodes can communicate directly with each other, and other nodes in HDInsight, by using internal DNS names.</span></span>

<span data-ttu-id="b3f53-172">預設名稱解析「不」允許 HDInsight 解析加入虛擬網路之網路中的資源名稱。</span><span class="sxs-lookup"><span data-stu-id="b3f53-172">The default name resolution does __not__ allow HDInsight to resolve the names of resources in networks that are joined to the virtual network.</span></span> <span data-ttu-id="b3f53-173">例如，通常會將內部部署網路加入虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b3f53-173">For example, it is common to join your on-premises network to the virtual network.</span></span> <span data-ttu-id="b3f53-174">只使用預設名稱解析，HDInsight 無法透過名稱存取內部部署網路中的資源。</span><span class="sxs-lookup"><span data-stu-id="b3f53-174">With only the default name resolution, HDInsight cannot access resources in the on-premises network by name.</span></span> <span data-ttu-id="b3f53-175">反之亦然，內部部署網路中的資源無法透過名稱存取虛擬網路中的資源。</span><span class="sxs-lookup"><span data-stu-id="b3f53-175">The opposite is also true, resources in your on-premises network cannot access resources in the virtual network by name.</span></span>

> [!WARNING]
> <span data-ttu-id="b3f53-176">您必須建立自訂 DNS 伺服器，並設定虛擬網路使用它，再建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="b3f53-176">You must create the custom DNS server and configure the virtual network to use it before creating the HDInsight cluster.</span></span>

<span data-ttu-id="b3f53-177">若要啟用虛擬網路與所加入網路中資源之間的名稱解析，您必須執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="b3f53-177">To enable name resolution between the virtual network and resources in joined networks, you must perform the following actions:</span></span>

1. <span data-ttu-id="b3f53-178">在要安裝 HDInsight 的 Azure 虛擬網路中建立自訂 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b3f53-178">Create a custom DNS server in the Azure Virtual Network where you plan to install HDInsight.</span></span>

2. <span data-ttu-id="b3f53-179">將虛擬網路設定為使用自訂 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b3f53-179">Configure the virtual network to use the custom DNS server.</span></span>

3. <span data-ttu-id="b3f53-180">尋找虛擬網路的 Azure 指派 DNS 尾碼。</span><span class="sxs-lookup"><span data-stu-id="b3f53-180">Find the Azure assigned DNS suffix for your virtual network.</span></span> <span data-ttu-id="b3f53-181">此值與 `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` 類似。</span><span class="sxs-lookup"><span data-stu-id="b3f53-181">This value is similar to `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span></span> <span data-ttu-id="b3f53-182">如需尋找 DNS 尾碼的資訊，請參閱[範例：自訂 DNS](#example-dns) 一節。</span><span class="sxs-lookup"><span data-stu-id="b3f53-182">For information on finding the DNS suffix, see the [Example: Custom DNS](#example-dns) section.</span></span>

4. <span data-ttu-id="b3f53-183">設定 DNS 伺服器之間的轉送。</span><span class="sxs-lookup"><span data-stu-id="b3f53-183">Configure forwarding between the DNS servers.</span></span> <span data-ttu-id="b3f53-184">設定取決於遠端網路類型。</span><span class="sxs-lookup"><span data-stu-id="b3f53-184">The configuration depends on the type of remote network.</span></span>

    * <span data-ttu-id="b3f53-185">如果遠端網路是內部部署網路，請設定 DNS，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b3f53-185">If the remote network is an on-premises network, configure DNS as follows:</span></span>
        
        * <span data-ttu-id="b3f53-186">「自訂 DNS」(在虛擬網路中)：</span><span class="sxs-lookup"><span data-stu-id="b3f53-186">__Custom DNS__ (in the virtual network):</span></span>

            * <span data-ttu-id="b3f53-187">將虛擬網路 DNS 尾碼的要求轉送至 Azure 遞迴解析程式 (168.63.129.16)。</span><span class="sxs-lookup"><span data-stu-id="b3f53-187">Forward requests for the DNS suffix of the virtual network to the Azure recursive resolver (168.63.129.16).</span></span> <span data-ttu-id="b3f53-188">Azure 會處理虛擬網路中資源的要求</span><span class="sxs-lookup"><span data-stu-id="b3f53-188">Azure handles requests for resources in the virtual network</span></span>

            * <span data-ttu-id="b3f53-189">將所有其他要求轉送至內部部署 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b3f53-189">Forward all other requests to the on-premises DNS server.</span></span> <span data-ttu-id="b3f53-190">內部部署 DNS 會處理所有其他名稱解析要求，即使是網際網路資源 (例如 Microsoft.com) 的要求也是一樣。</span><span class="sxs-lookup"><span data-stu-id="b3f53-190">The on-premises DNS handles all other name resolution requests, even requests for internet resources such as Microsoft.com.</span></span>

        * <span data-ttu-id="b3f53-191">內部部署 DNS：將虛擬網路 DNS 尾碼的要求轉送至自訂 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b3f53-191">__On-premises DNS__: Forward requests for the virtual network DNS suffix to the custom DNS server.</span></span> <span data-ttu-id="b3f53-192">自訂 DNS 伺服器接著會轉送至 Azure 遞迴解析程式。</span><span class="sxs-lookup"><span data-stu-id="b3f53-192">The custom DNS server then forwards to the Azure recursive resolver.</span></span>

        <span data-ttu-id="b3f53-193">此設定會將完整網域名稱包含虛擬網路 DNS 尾碼的要求路由傳送至自訂 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b3f53-193">This configuration routes requests for fully qualified domain names that contain the DNS suffix of the virtual network to the custom DNS server.</span></span> <span data-ttu-id="b3f53-194">內部部署 DNS 伺服器會處理所有其他要求 (即使是針對公用網際網路位址)。</span><span class="sxs-lookup"><span data-stu-id="b3f53-194">All other requests (even for public internet addresses) are handled by the on-premises DNS server.</span></span>

    * <span data-ttu-id="b3f53-195">如果遠端網路是另一個 Azure 虛擬網路，請設定 DNS，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b3f53-195">If the remote network is another Azure Virtual Network, configure DNS as follows:</span></span>

        * <span data-ttu-id="b3f53-196">「自訂 DNS」(在每個虛擬網路中)：</span><span class="sxs-lookup"><span data-stu-id="b3f53-196">__Custom DNS__ (in each virtual network):</span></span>

            * <span data-ttu-id="b3f53-197">將虛擬網路 DNS 尾碼的要求轉送至自訂 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b3f53-197">Requests for the DNS suffix of the virtual networks are forwarded to the custom DNS servers.</span></span> <span data-ttu-id="b3f53-198">每個虛擬網路中的 DNS 會負責解析其網路內的資源。</span><span class="sxs-lookup"><span data-stu-id="b3f53-198">The DNS in each virtual network is responsible for resolving resources within its network.</span></span>

            * <span data-ttu-id="b3f53-199">將所有其他要求轉送至 Azure 遞迴解析程式。</span><span class="sxs-lookup"><span data-stu-id="b3f53-199">Forward all other requests to the Azure recursive resolver.</span></span> <span data-ttu-id="b3f53-200">遞迴解析程式負責解析本機和網際網路資源。</span><span class="sxs-lookup"><span data-stu-id="b3f53-200">The recursive resolver is responsible for resolving local and internet resources.</span></span>

        <span data-ttu-id="b3f53-201">根據 DNS 尾碼，每個網路的 DNS 伺服器都會將要求轉送至另一個。</span><span class="sxs-lookup"><span data-stu-id="b3f53-201">The DNS server for each network forwards requests to the other, based on DNS suffix.</span></span> <span data-ttu-id="b3f53-202">其他要求是使用 Azure 遞迴解析程式進行解析。</span><span class="sxs-lookup"><span data-stu-id="b3f53-202">Other requests are resolved using the Azure recursive resolver.</span></span>

    <span data-ttu-id="b3f53-203">如需每個設定的範例，請參閱[範例：自訂 DNS](#example-dns) 一節。</span><span class="sxs-lookup"><span data-stu-id="b3f53-203">For an example of each configuration, see the [Example: Custom DNS](#example-dns) section.</span></span>

<span data-ttu-id="b3f53-204">如需詳細資訊，請參閱 [VM 和角色執行個體的名稱解析](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)文件。</span><span class="sxs-lookup"><span data-stu-id="b3f53-204">For more information, see the [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.</span></span>

## <a name="directly-connect-to-hadoop-services"></a><span data-ttu-id="b3f53-205">直接連線至 Hadoop 服務</span><span class="sxs-lookup"><span data-stu-id="b3f53-205">Directly connect to Hadoop services</span></span>

<span data-ttu-id="b3f53-206">HDInsight 上大部分的文件都假設您透過網際網路擁有叢集存取權。</span><span class="sxs-lookup"><span data-stu-id="b3f53-206">Most documentation on HDInsight assumes that you have access to the cluster over the internet.</span></span> <span data-ttu-id="b3f53-207">例如，您可以連線到 https://CLUSTERNAME.azurehdinsight.net 的叢集。</span><span class="sxs-lookup"><span data-stu-id="b3f53-207">For example, that you can connect to the cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="b3f53-208">這個位址會使用公用閘道，如果您已經使用 NSG 或 UDR 來限制網際網路的存取，則無法使用。</span><span class="sxs-lookup"><span data-stu-id="b3f53-208">This address uses the public gateway, which is not available if you have used NSGs or UDRs to restrict access from the internet.</span></span>

<span data-ttu-id="b3f53-209">若要透過虛擬網路連線至 Ambari 和其他網頁，請使用下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b3f53-209">To connect to Ambari and other web pages through the virtual network, use the following steps:</span></span>

1. <span data-ttu-id="b3f53-210">若要探索 HDInsight 叢集節點的內部完整網域名稱 (FQDN)，請使用下列其中一種方法：</span><span class="sxs-lookup"><span data-stu-id="b3f53-210">To discover the internal fully qualified domain names (FQDN) of the HDInsight cluster nodes, use one of the following methods:</span></span>

    ```powershell
    $resourceGroupName = "The resource group that contains the virtual network used with HDInsight"

    $clusterNICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName | where-object {$_.Name -like "*node*"}

    $nodes = @()
    foreach($nic in $clusterNICs) {
        $node = new-object System.Object
        $node | add-member -MemberType NoteProperty -name "Type" -value $nic.Name.Split('-')[1]
        $node | add-member -MemberType NoteProperty -name "InternalIP" -value $nic.IpConfigurations.PrivateIpAddress
        $node | add-member -MemberType NoteProperty -name "InternalFQDN" -value $nic.DnsSettings.InternalFqdn
        $nodes += $node
    }
    $nodes | sort-object Type
    ```

    ```azurecli
    az network nic list --resource-group <resourcegroupname> --output table --query "[?contains(name,'node')].{NICname:name,InternalIP:ipConfigurations[0].privateIpAddress,InternalFQDN:dnsSettings.internalFqdn}"
    ```

    <span data-ttu-id="b3f53-211">在所傳回的節點清單中，尋找前端節點的 FQDN 並使用這些 FQDN 來連線至 Ambari 和其他 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="b3f53-211">In the list of nodes returned, find the FQDN for the head nodes and use the FQDNs to connect to Ambari and other web services.</span></span> <span data-ttu-id="b3f53-212">例如，使用 `http://<headnode-fqdn>:8080` 存取 Ambari。</span><span class="sxs-lookup"><span data-stu-id="b3f53-212">For example, use `http://<headnode-fqdn>:8080` to access Ambari.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b3f53-213">前端節點上裝載的某些服務一次只會在一個節點上作用。</span><span class="sxs-lookup"><span data-stu-id="b3f53-213">Some services hosted on the head nodes are only active on one node at a time.</span></span> <span data-ttu-id="b3f53-214">如果您嘗試在一個前端節點上存取服務，但傳回 404 錯誤，請切換至其他的前端節點。</span><span class="sxs-lookup"><span data-stu-id="b3f53-214">If you try accessing a service on one head node and it returns a 404 error, switch to the other head node.</span></span>

2. <span data-ttu-id="b3f53-215">若要判斷可提供服務的節點和連接埠，請參閱 [Hadoop 服務在 HDInsight 上所使用的連接埠](./hdinsight-hadoop-port-settings-for-services.md)文件。</span><span class="sxs-lookup"><span data-stu-id="b3f53-215">To determine the node and port that a service is available on, see the [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

## <span data-ttu-id="b3f53-216"><a id="networktraffic"></a> 控制網路流量</span><span class="sxs-lookup"><span data-stu-id="b3f53-216"><a id="networktraffic"></a> Controlling network traffic</span></span>

<span data-ttu-id="b3f53-217">Azure 虛擬網路中的網路流量可以使用下列方法進行控制：</span><span class="sxs-lookup"><span data-stu-id="b3f53-217">Network traffic in an Azure Virtual Networks can be controlled using the following methods:</span></span>

* <span data-ttu-id="b3f53-218">**網路安全性群組** (NSG) 可讓您篩選輸入和輸出網路流量。</span><span class="sxs-lookup"><span data-stu-id="b3f53-218">**Network security groups** (NSG) allow you to filter inbound and outbound traffic to the network.</span></span> <span data-ttu-id="b3f53-219">如需詳細資訊，請參閱[使用網路安全性群組來篩選網路流量](../virtual-network/virtual-networks-nsg.md)文件。</span><span class="sxs-lookup"><span data-stu-id="b3f53-219">For more information, see the [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    > [!WARNING]
    > <span data-ttu-id="b3f53-220">HDInsight 不支援限制輸出流量。</span><span class="sxs-lookup"><span data-stu-id="b3f53-220">HDInsight does not support restricting outbound traffic.</span></span>

* <span data-ttu-id="b3f53-221">**使用者定義路由** (UDR) 定義流量在網路中的資源之間如何流動。</span><span class="sxs-lookup"><span data-stu-id="b3f53-221">**User-defined routes** (UDR) define how traffic flows between resources in the network.</span></span> <span data-ttu-id="b3f53-222">如需詳細資訊，請參閱[使用者定義路由和 IP 轉送](../virtual-network/virtual-networks-udr-overview.md)文件。</span><span class="sxs-lookup"><span data-stu-id="b3f53-222">For more information, see the [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md) document.</span></span>

* <span data-ttu-id="b3f53-223">**網路虛擬設備**會複寫裝置的功能，例如防火牆和路由器。</span><span class="sxs-lookup"><span data-stu-id="b3f53-223">**Network virtual appliances** replicate the functionality of devices such as firewalls and routers.</span></span> <span data-ttu-id="b3f53-224">如需詳細資訊，請參閱[網路設備](https://azure.microsoft.com/solutions/network-appliances)文件。</span><span class="sxs-lookup"><span data-stu-id="b3f53-224">For more information, see the [Network Appliances](https://azure.microsoft.com/solutions/network-appliances) document.</span></span>

<span data-ttu-id="b3f53-225">HDInsight 是一個受管理服務，需要 Azure 雲端中 Azure 健康狀態和管理服務的無限制存取權。</span><span class="sxs-lookup"><span data-stu-id="b3f53-225">As a managed service, HDInsight requires unrestricted access to Azure health and management services in the Azure cloud.</span></span> <span data-ttu-id="b3f53-226">使用 NSG 和 UDR 時，您必須確定這些服務仍然可以與 HDInsight 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="b3f53-226">When using NSGs and UDRs, you must ensure that HDInsight these services can still communicate with HDInsight.</span></span>

<span data-ttu-id="b3f53-227">HDInsight 會在數個連接埠上公開服務。</span><span class="sxs-lookup"><span data-stu-id="b3f53-227">HDInsight exposes services on several ports.</span></span> <span data-ttu-id="b3f53-228">使用虛擬設備防火牆時，您必須允許用於這些服務之連接埠的流量。</span><span class="sxs-lookup"><span data-stu-id="b3f53-228">When using a virtual appliance firewall, you must allow traffic on the ports used for these services.</span></span> <span data-ttu-id="b3f53-229">如需詳細資訊，請參閱[必要連接埠]一節。</span><span class="sxs-lookup"><span data-stu-id="b3f53-229">For more information, see the [Required ports] section.</span></span>

### <span data-ttu-id="b3f53-230"><a id="hdinsight-ip"></a> 具有網路安全性群組和使用者定義路由的 HDInsight</span><span class="sxs-lookup"><span data-stu-id="b3f53-230"><a id="hdinsight-ip"></a> HDInsight with network security groups and user-defined routes</span></span>

<span data-ttu-id="b3f53-231">如果您規劃使用**網路安全性群組**或**使用者定義路由**來控制網路流量，請先執行下列動作，再安裝 HDInsight：</span><span class="sxs-lookup"><span data-stu-id="b3f53-231">If you plan on using **network security groups** or **user-defined routes** to control network traffic, perform the following actions before installing HDInsight:</span></span>

1. <span data-ttu-id="b3f53-232">識別您要用於 HDInsight 的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="b3f53-232">Identify the Azure region that you plan to use for HDInsight.</span></span>

2. <span data-ttu-id="b3f53-233">識別 HDInsight 所需的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b3f53-233">Identify the IP addresses required by HDInsight.</span></span> <span data-ttu-id="b3f53-234">如需詳細資訊，請參閱 [HDInsight 所需的 IP 位址](#hdinsight-ip)一節。</span><span class="sxs-lookup"><span data-stu-id="b3f53-234">For more information, see the [IP Addresses required by HDInsight](#hdinsight-ip) section.</span></span>

3. <span data-ttu-id="b3f53-235">建立或修改您要安裝 HDInsight 之子網路的網路安全性群組或使用者定義路由。</span><span class="sxs-lookup"><span data-stu-id="b3f53-235">Create or modify the network security groups or user-defined routes for the subnet that you plan to install HDInsight into.</span></span>

    * <span data-ttu-id="b3f53-236">__網路安全性群組__：允許連接埠 __443__ 上來自 IP 位址的「輸入」流量。</span><span class="sxs-lookup"><span data-stu-id="b3f53-236">__Network security groups__: allow __inbound__ traffic on port __443__ from the IP addresses.</span></span>
    * <span data-ttu-id="b3f53-237">__使用者定義路由__：建立每個 IP 位址的路由，並將 [下一個躍點類型] 設定為 [網際網路]。</span><span class="sxs-lookup"><span data-stu-id="b3f53-237">__User-defined routes__: create a route to each IP address and set the __Next hop type__ to __Internet__.</span></span>

<span data-ttu-id="b3f53-238">如需網路安全性群組或使用者定義路由的詳細資訊，請參閱下列文件：</span><span class="sxs-lookup"><span data-stu-id="b3f53-238">For more information on network security groups or user-defined routes, see the following documentation:</span></span>

* [<span data-ttu-id="b3f53-239">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="b3f53-239">Network security group</span></span>](../virtual-network/virtual-networks-nsg.md)

* [<span data-ttu-id="b3f53-240">使用者定義路由</span><span class="sxs-lookup"><span data-stu-id="b3f53-240">User-defined routes</span></span>](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a><span data-ttu-id="b3f53-241">強制通道</span><span class="sxs-lookup"><span data-stu-id="b3f53-241">Forced tunneling</span></span>

<span data-ttu-id="b3f53-242">強制通道是一種使用者定義路由設定，其中來自子網路的所有流量都會強制流向特定網路或位置，例如內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="b3f53-242">Forced tunneling is a user-defined routing configuration where all traffic from a subnet is forced to a specific network or location, such as your on-premises network.</span></span> <span data-ttu-id="b3f53-243">HDInsight「不」支援強制通道。</span><span class="sxs-lookup"><span data-stu-id="b3f53-243">HDInsight does __not__ support forced tunneling.</span></span>

## <span data-ttu-id="b3f53-244"><a id="hdinsight-ip"></a> 所需的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="b3f53-244"><a id="hdinsight-ip"></a> Required IP addresses</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b3f53-245">Azure 健康狀態和管理服務必須能夠與 HDInsight 通訊。</span><span class="sxs-lookup"><span data-stu-id="b3f53-245">The Azure health and management services must be able to communicate with HDInsight.</span></span> <span data-ttu-id="b3f53-246">如果您使用網路安全性群組或使用者定義的路由，請允許來自這些服務之 IP 位址的流量到達 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="b3f53-246">If you use network security groups or user-defined routes, allow traffic from the IP addresses for these services to reach HDInsight.</span></span>
>
> <span data-ttu-id="b3f53-247">如果您未使用網路安全性群組或使用者定義的路由來控制流量，可以忽略這個章節。</span><span class="sxs-lookup"><span data-stu-id="b3f53-247">If you do not use network security groups or user-defined routes to control traffic, you can ignore this section.</span></span>

<span data-ttu-id="b3f53-248">如果您是使用網路安全性群組或使用者定義的路由，必須允許來自 Azure 健康情況和管理服務的流量觸達 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="b3f53-248">If you use network security groups or user-defined routes, you must allow traffic from the Azure health and management services to reach HDInsight.</span></span> <span data-ttu-id="b3f53-249">您可以使用下列步驟來尋找必須允許的 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="b3f53-249">Use the following steps to find the IP addresses that must be allowed:</span></span>

1. <span data-ttu-id="b3f53-250">您必須一律允許來自下列 IP 位址的流量：</span><span class="sxs-lookup"><span data-stu-id="b3f53-250">You must always allow traffic from the following IP addresses:</span></span>

    | <span data-ttu-id="b3f53-251">IP 位址</span><span class="sxs-lookup"><span data-stu-id="b3f53-251">IP address</span></span> | <span data-ttu-id="b3f53-252">允許的連接埠</span><span class="sxs-lookup"><span data-stu-id="b3f53-252">Allowed port</span></span> | <span data-ttu-id="b3f53-253">方向</span><span class="sxs-lookup"><span data-stu-id="b3f53-253">Direction</span></span> |
    | ---- | ----- | ----- |
    | <span data-ttu-id="b3f53-254">168.61.49.99</span><span class="sxs-lookup"><span data-stu-id="b3f53-254">168.61.49.99</span></span> | <span data-ttu-id="b3f53-255">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-255">443</span></span> | <span data-ttu-id="b3f53-256">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-256">Inbound</span></span> |
    | <span data-ttu-id="b3f53-257">23.99.5.239</span><span class="sxs-lookup"><span data-stu-id="b3f53-257">23.99.5.239</span></span> | <span data-ttu-id="b3f53-258">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-258">443</span></span> | <span data-ttu-id="b3f53-259">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-259">Inbound</span></span> |
    | <span data-ttu-id="b3f53-260">168.61.48.131</span><span class="sxs-lookup"><span data-stu-id="b3f53-260">168.61.48.131</span></span> | <span data-ttu-id="b3f53-261">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-261">443</span></span> | <span data-ttu-id="b3f53-262">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-262">Inbound</span></span> |
    | <span data-ttu-id="b3f53-263">138.91.141.162</span><span class="sxs-lookup"><span data-stu-id="b3f53-263">138.91.141.162</span></span> | <span data-ttu-id="b3f53-264">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-264">443</span></span> | <span data-ttu-id="b3f53-265">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-265">Inbound</span></span> |

2. <span data-ttu-id="b3f53-266">如果您的 HDInsight 叢集是位於下列其中一個區域中，就必須允許來自針對區域所列的 IP 位址之流量：</span><span class="sxs-lookup"><span data-stu-id="b3f53-266">If your HDInsight cluster is in one of the following regions, then you must allow traffic from the IP addresses listed for the region:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b3f53-267">如果未列出您使用的 Azure 區域，就只能使用步驟 1 中的四個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b3f53-267">If the Azure region you are using is not listed, then only use the four IP addresses from step 1.</span></span>

    | <span data-ttu-id="b3f53-268">國家 (地區)</span><span class="sxs-lookup"><span data-stu-id="b3f53-268">Country</span></span> | <span data-ttu-id="b3f53-269">區域</span><span class="sxs-lookup"><span data-stu-id="b3f53-269">Region</span></span> | <span data-ttu-id="b3f53-270">允許的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="b3f53-270">Allowed IP addresses</span></span> | <span data-ttu-id="b3f53-271">允許的連接埠</span><span class="sxs-lookup"><span data-stu-id="b3f53-271">Allowed port</span></span> | <span data-ttu-id="b3f53-272">方向</span><span class="sxs-lookup"><span data-stu-id="b3f53-272">Direction</span></span> |
    | ---- | ---- | ---- | ---- | ----- |
    | <span data-ttu-id="b3f53-273">亞洲</span><span class="sxs-lookup"><span data-stu-id="b3f53-273">Asia</span></span> | <span data-ttu-id="b3f53-274">東亞</span><span class="sxs-lookup"><span data-stu-id="b3f53-274">East Asia</span></span> | <span data-ttu-id="b3f53-275">23.102.235.122</span><span class="sxs-lookup"><span data-stu-id="b3f53-275">23.102.235.122</span></span></br><span data-ttu-id="b3f53-276">52.175.38.134</span><span class="sxs-lookup"><span data-stu-id="b3f53-276">52.175.38.134</span></span> | <span data-ttu-id="b3f53-277">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-277">443</span></span> | <span data-ttu-id="b3f53-278">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-278">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b3f53-279">東南亞</span><span class="sxs-lookup"><span data-stu-id="b3f53-279">Southeast Asia</span></span> | <span data-ttu-id="b3f53-280">13.76.245.160</span><span class="sxs-lookup"><span data-stu-id="b3f53-280">13.76.245.160</span></span></br><span data-ttu-id="b3f53-281">13.76.136.249</span><span class="sxs-lookup"><span data-stu-id="b3f53-281">13.76.136.249</span></span> | <span data-ttu-id="b3f53-282">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-282">443</span></span> | <span data-ttu-id="b3f53-283">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-283">Inbound</span></span> |
    | <span data-ttu-id="b3f53-284">澳大利亞</span><span class="sxs-lookup"><span data-stu-id="b3f53-284">Australia</span></span> | <span data-ttu-id="b3f53-285">澳洲東部</span><span class="sxs-lookup"><span data-stu-id="b3f53-285">Australia East</span></span> | <span data-ttu-id="b3f53-286">104.210.84.115</span><span class="sxs-lookup"><span data-stu-id="b3f53-286">104.210.84.115</span></span></br><span data-ttu-id="b3f53-287">13.75.152.195</span><span class="sxs-lookup"><span data-stu-id="b3f53-287">13.75.152.195</span></span> | <span data-ttu-id="b3f53-288">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-288">443</span></span> | <span data-ttu-id="b3f53-289">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-289">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b3f53-290">澳大利亞東南部</span><span class="sxs-lookup"><span data-stu-id="b3f53-290">Australia Southeast</span></span> | <span data-ttu-id="b3f53-291">13.77.2.56</span><span class="sxs-lookup"><span data-stu-id="b3f53-291">13.77.2.56</span></span></br><span data-ttu-id="b3f53-292">13.77.2.94</span><span class="sxs-lookup"><span data-stu-id="b3f53-292">13.77.2.94</span></span> | <span data-ttu-id="b3f53-293">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-293">443</span></span> | <span data-ttu-id="b3f53-294">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-294">Inbound</span></span> |
    | <span data-ttu-id="b3f53-295">巴西</span><span class="sxs-lookup"><span data-stu-id="b3f53-295">Brazil</span></span> | <span data-ttu-id="b3f53-296">巴西南部</span><span class="sxs-lookup"><span data-stu-id="b3f53-296">Brazil South</span></span> | <span data-ttu-id="b3f53-297">191.235.84.104</span><span class="sxs-lookup"><span data-stu-id="b3f53-297">191.235.84.104</span></span></br><span data-ttu-id="b3f53-298">191.235.87.113</span><span class="sxs-lookup"><span data-stu-id="b3f53-298">191.235.87.113</span></span> | <span data-ttu-id="b3f53-299">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-299">443</span></span> | <span data-ttu-id="b3f53-300">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-300">Inbound</span></span> |
    | <span data-ttu-id="b3f53-301">加拿大</span><span class="sxs-lookup"><span data-stu-id="b3f53-301">Canada</span></span> | <span data-ttu-id="b3f53-302">加拿大東部</span><span class="sxs-lookup"><span data-stu-id="b3f53-302">Canada East</span></span> | <span data-ttu-id="b3f53-303">52.229.127.96</span><span class="sxs-lookup"><span data-stu-id="b3f53-303">52.229.127.96</span></span></br><span data-ttu-id="b3f53-304">52.229.123.172</span><span class="sxs-lookup"><span data-stu-id="b3f53-304">52.229.123.172</span></span> | <span data-ttu-id="b3f53-305">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-305">443</span></span> | <span data-ttu-id="b3f53-306">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-306">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b3f53-307">加拿大中部</span><span class="sxs-lookup"><span data-stu-id="b3f53-307">Canada Central</span></span> | <span data-ttu-id="b3f53-308">52.228.37.66</span><span class="sxs-lookup"><span data-stu-id="b3f53-308">52.228.37.66</span></span></br><span data-ttu-id="b3f53-309">52.228.45.222</span><span class="sxs-lookup"><span data-stu-id="b3f53-309">52.228.45.222</span></span> | <span data-ttu-id="b3f53-310">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-310">443</span></span> | <span data-ttu-id="b3f53-311">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-311">Inbound</span></span> |
    | <span data-ttu-id="b3f53-312">中國</span><span class="sxs-lookup"><span data-stu-id="b3f53-312">China</span></span> | <span data-ttu-id="b3f53-313">中國北部</span><span class="sxs-lookup"><span data-stu-id="b3f53-313">China North</span></span> | <span data-ttu-id="b3f53-314">42.159.96.170</span><span class="sxs-lookup"><span data-stu-id="b3f53-314">42.159.96.170</span></span></br><span data-ttu-id="b3f53-315">139.217.2.219</span><span class="sxs-lookup"><span data-stu-id="b3f53-315">139.217.2.219</span></span> | <span data-ttu-id="b3f53-316">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-316">443</span></span> | <span data-ttu-id="b3f53-317">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-317">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b3f53-318">中國東部</span><span class="sxs-lookup"><span data-stu-id="b3f53-318">China East</span></span> | <span data-ttu-id="b3f53-319">42.159.198.178</span><span class="sxs-lookup"><span data-stu-id="b3f53-319">42.159.198.178</span></span></br><span data-ttu-id="b3f53-320">42.159.234.157</span><span class="sxs-lookup"><span data-stu-id="b3f53-320">42.159.234.157</span></span> | <span data-ttu-id="b3f53-321">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-321">443</span></span> | <span data-ttu-id="b3f53-322">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-322">Inbound</span></span> |
    | <span data-ttu-id="b3f53-323">歐洲</span><span class="sxs-lookup"><span data-stu-id="b3f53-323">Europe</span></span> | <span data-ttu-id="b3f53-324">北歐</span><span class="sxs-lookup"><span data-stu-id="b3f53-324">North Europe</span></span> | <span data-ttu-id="b3f53-325">52.164.210.96</span><span class="sxs-lookup"><span data-stu-id="b3f53-325">52.164.210.96</span></span></br><span data-ttu-id="b3f53-326">13.74.153.132</span><span class="sxs-lookup"><span data-stu-id="b3f53-326">13.74.153.132</span></span> | <span data-ttu-id="b3f53-327">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-327">443</span></span> | <span data-ttu-id="b3f53-328">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-328">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b3f53-329">西歐</span><span class="sxs-lookup"><span data-stu-id="b3f53-329">West Europe</span></span>| <span data-ttu-id="b3f53-330">52.166.243.90</span><span class="sxs-lookup"><span data-stu-id="b3f53-330">52.166.243.90</span></span></br><span data-ttu-id="b3f53-331">52.174.36.244</span><span class="sxs-lookup"><span data-stu-id="b3f53-331">52.174.36.244</span></span> | <span data-ttu-id="b3f53-332">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-332">443</span></span> | <span data-ttu-id="b3f53-333">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-333">Inbound</span></span> |
    | <span data-ttu-id="b3f53-334">德國</span><span class="sxs-lookup"><span data-stu-id="b3f53-334">Germany</span></span> | <span data-ttu-id="b3f53-335">德國中部</span><span class="sxs-lookup"><span data-stu-id="b3f53-335">Germany Central</span></span> | <span data-ttu-id="b3f53-336">51.4.146.68</span><span class="sxs-lookup"><span data-stu-id="b3f53-336">51.4.146.68</span></span></br><span data-ttu-id="b3f53-337">51.4.146.80</span><span class="sxs-lookup"><span data-stu-id="b3f53-337">51.4.146.80</span></span> | <span data-ttu-id="b3f53-338">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-338">443</span></span> | <span data-ttu-id="b3f53-339">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-339">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b3f53-340">德國東北部</span><span class="sxs-lookup"><span data-stu-id="b3f53-340">Germany Northeast</span></span> | <span data-ttu-id="b3f53-341">51.5.150.132</span><span class="sxs-lookup"><span data-stu-id="b3f53-341">51.5.150.132</span></span></br><span data-ttu-id="b3f53-342">51.5.144.101</span><span class="sxs-lookup"><span data-stu-id="b3f53-342">51.5.144.101</span></span> | <span data-ttu-id="b3f53-343">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-343">443</span></span> | <span data-ttu-id="b3f53-344">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-344">Inbound</span></span> |
    | <span data-ttu-id="b3f53-345">印度</span><span class="sxs-lookup"><span data-stu-id="b3f53-345">India</span></span> | <span data-ttu-id="b3f53-346">印度中部</span><span class="sxs-lookup"><span data-stu-id="b3f53-346">Central India</span></span> | <span data-ttu-id="b3f53-347">52.172.153.209</span><span class="sxs-lookup"><span data-stu-id="b3f53-347">52.172.153.209</span></span></br><span data-ttu-id="b3f53-348">52.172.152.49</span><span class="sxs-lookup"><span data-stu-id="b3f53-348">52.172.152.49</span></span> | <span data-ttu-id="b3f53-349">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-349">443</span></span> | <span data-ttu-id="b3f53-350">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-350">Inbound</span></span> |
    | <span data-ttu-id="b3f53-351">日本</span><span class="sxs-lookup"><span data-stu-id="b3f53-351">Japan</span></span> | <span data-ttu-id="b3f53-352">日本東部</span><span class="sxs-lookup"><span data-stu-id="b3f53-352">Japan East</span></span> | <span data-ttu-id="b3f53-353">13.78.125.90</span><span class="sxs-lookup"><span data-stu-id="b3f53-353">13.78.125.90</span></span></br><span data-ttu-id="b3f53-354">13.78.89.60</span><span class="sxs-lookup"><span data-stu-id="b3f53-354">13.78.89.60</span></span> | <span data-ttu-id="b3f53-355">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-355">443</span></span> | <span data-ttu-id="b3f53-356">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-356">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b3f53-357">日本西部</span><span class="sxs-lookup"><span data-stu-id="b3f53-357">Japan West</span></span> | <span data-ttu-id="b3f53-358">40.74.125.69</span><span class="sxs-lookup"><span data-stu-id="b3f53-358">40.74.125.69</span></span></br><span data-ttu-id="b3f53-359">138.91.29.150</span><span class="sxs-lookup"><span data-stu-id="b3f53-359">138.91.29.150</span></span> | <span data-ttu-id="b3f53-360">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-360">443</span></span> | <span data-ttu-id="b3f53-361">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-361">Inbound</span></span> |
    | <span data-ttu-id="b3f53-362">韓國</span><span class="sxs-lookup"><span data-stu-id="b3f53-362">Korea</span></span> | <span data-ttu-id="b3f53-363">韓國中部</span><span class="sxs-lookup"><span data-stu-id="b3f53-363">Korea Central</span></span> | <span data-ttu-id="b3f53-364">52.231.39.142</span><span class="sxs-lookup"><span data-stu-id="b3f53-364">52.231.39.142</span></span></br><span data-ttu-id="b3f53-365">52.231.36.209</span><span class="sxs-lookup"><span data-stu-id="b3f53-365">52.231.36.209</span></span> | <span data-ttu-id="b3f53-366">433</span><span class="sxs-lookup"><span data-stu-id="b3f53-366">433</span></span> | <span data-ttu-id="b3f53-367">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-367">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b3f53-368">韓國南部</span><span class="sxs-lookup"><span data-stu-id="b3f53-368">Korea South</span></span> | <span data-ttu-id="b3f53-369">52.231.203.16</span><span class="sxs-lookup"><span data-stu-id="b3f53-369">52.231.203.16</span></span></br><span data-ttu-id="b3f53-370">52.231.205.214</span><span class="sxs-lookup"><span data-stu-id="b3f53-370">52.231.205.214</span></span> | <span data-ttu-id="b3f53-371">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-371">443</span></span> | <span data-ttu-id="b3f53-372">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-372">Inbound</span></span>
    | <span data-ttu-id="b3f53-373">英國</span><span class="sxs-lookup"><span data-stu-id="b3f53-373">United Kingdom</span></span> | <span data-ttu-id="b3f53-374">英國西部</span><span class="sxs-lookup"><span data-stu-id="b3f53-374">UK West</span></span> | <span data-ttu-id="b3f53-375">51.141.13.110</span><span class="sxs-lookup"><span data-stu-id="b3f53-375">51.141.13.110</span></span></br><span data-ttu-id="b3f53-376">51.141.7.20</span><span class="sxs-lookup"><span data-stu-id="b3f53-376">51.141.7.20</span></span> | <span data-ttu-id="b3f53-377">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-377">443</span></span> | <span data-ttu-id="b3f53-378">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-378">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b3f53-379">英國南部</span><span class="sxs-lookup"><span data-stu-id="b3f53-379">UK South</span></span> | <span data-ttu-id="b3f53-380">51.140.47.39</span><span class="sxs-lookup"><span data-stu-id="b3f53-380">51.140.47.39</span></span></br><span data-ttu-id="b3f53-381">51.140.52.16</span><span class="sxs-lookup"><span data-stu-id="b3f53-381">51.140.52.16</span></span> | <span data-ttu-id="b3f53-382">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-382">443</span></span> | <span data-ttu-id="b3f53-383">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-383">Inbound</span></span> |
    | <span data-ttu-id="b3f53-384">美國</span><span class="sxs-lookup"><span data-stu-id="b3f53-384">United States</span></span> | <span data-ttu-id="b3f53-385">美國中部</span><span class="sxs-lookup"><span data-stu-id="b3f53-385">Central US</span></span> | <span data-ttu-id="b3f53-386">13.67.223.215</span><span class="sxs-lookup"><span data-stu-id="b3f53-386">13.67.223.215</span></span></br><span data-ttu-id="b3f53-387">40.86.83.253</span><span class="sxs-lookup"><span data-stu-id="b3f53-387">40.86.83.253</span></span> | <span data-ttu-id="b3f53-388">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-388">443</span></span> | <span data-ttu-id="b3f53-389">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-389">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b3f53-390">美國中北部</span><span class="sxs-lookup"><span data-stu-id="b3f53-390">North Central US</span></span> | <span data-ttu-id="b3f53-391">157.56.8.38</span><span class="sxs-lookup"><span data-stu-id="b3f53-391">157.56.8.38</span></span></br><span data-ttu-id="b3f53-392">157.55.213.99</span><span class="sxs-lookup"><span data-stu-id="b3f53-392">157.55.213.99</span></span> | <span data-ttu-id="b3f53-393">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-393">443</span></span> | <span data-ttu-id="b3f53-394">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-394">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b3f53-395">美國中西部</span><span class="sxs-lookup"><span data-stu-id="b3f53-395">West Central US</span></span> | <span data-ttu-id="b3f53-396">52.161.23.15</span><span class="sxs-lookup"><span data-stu-id="b3f53-396">52.161.23.15</span></span></br><span data-ttu-id="b3f53-397">52.161.10.167</span><span class="sxs-lookup"><span data-stu-id="b3f53-397">52.161.10.167</span></span> | <span data-ttu-id="b3f53-398">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-398">443</span></span> | <span data-ttu-id="b3f53-399">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-399">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="b3f53-400">美國西部 2</span><span class="sxs-lookup"><span data-stu-id="b3f53-400">West US 2</span></span> | <span data-ttu-id="b3f53-401">52.175.211.210</span><span class="sxs-lookup"><span data-stu-id="b3f53-401">52.175.211.210</span></span></br><span data-ttu-id="b3f53-402">52.175.222.222</span><span class="sxs-lookup"><span data-stu-id="b3f53-402">52.175.222.222</span></span> | <span data-ttu-id="b3f53-403">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-403">443</span></span> | <span data-ttu-id="b3f53-404">輸入</span><span class="sxs-lookup"><span data-stu-id="b3f53-404">Inbound</span></span> |

    <span data-ttu-id="b3f53-405">如需用於 Azure Government 之 IP 位址的資訊，請參閱 [Azure Government Intelligence + Analytics](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) 文件。</span><span class="sxs-lookup"><span data-stu-id="b3f53-405">For information on the IP addresses to use for Azure Government, see the [Azure Government Intelligence + Analytics](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) document.</span></span>

3. <span data-ttu-id="b3f53-406">如果您搭配使用自訂 DNS 伺服器與虛擬網路，則也必須允許從 __168.63.129.16__ 進行存取。</span><span class="sxs-lookup"><span data-stu-id="b3f53-406">If you use a custom DNS server with your virtual network, you must also allow access from __168.63.129.16__.</span></span> <span data-ttu-id="b3f53-407">此位址是 Azure 遞迴解析程式。</span><span class="sxs-lookup"><span data-stu-id="b3f53-407">This address is Azure's recursive resolver.</span></span> <span data-ttu-id="b3f53-408">如需詳細資訊，請參閱 [VM 和角色執行個體的名稱解析](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)文件。</span><span class="sxs-lookup"><span data-stu-id="b3f53-408">For more information, see the [Name resolution for VMs and Role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.</span></span>

<span data-ttu-id="b3f53-409">如需詳細資訊，請參閱[控制網路流量](#networktraffic)一節。</span><span class="sxs-lookup"><span data-stu-id="b3f53-409">For more information, see the [Controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="b3f53-410"><a id="hdinsight-ports"></a> 所需連接埠</span><span class="sxs-lookup"><span data-stu-id="b3f53-410"><a id="hdinsight-ports"></a> Required ports</span></span>

<span data-ttu-id="b3f53-411">如果您要使用網路**虛擬設備防火牆**來保護虛擬網路，則必須允許下列連接埠的輸出流量：</span><span class="sxs-lookup"><span data-stu-id="b3f53-411">If you plan on using a network **virtual appliance firewall** to secure the virtual network, you must allow outbound traffic on the following ports:</span></span>

* <span data-ttu-id="b3f53-412">53</span><span class="sxs-lookup"><span data-stu-id="b3f53-412">53</span></span>
* <span data-ttu-id="b3f53-413">443</span><span class="sxs-lookup"><span data-stu-id="b3f53-413">443</span></span>
* <span data-ttu-id="b3f53-414">1433</span><span class="sxs-lookup"><span data-stu-id="b3f53-414">1433</span></span>
* <span data-ttu-id="b3f53-415">11000-11999</span><span class="sxs-lookup"><span data-stu-id="b3f53-415">11000-11999</span></span>
* <span data-ttu-id="b3f53-416">14000-14999</span><span class="sxs-lookup"><span data-stu-id="b3f53-416">14000-14999</span></span>

<span data-ttu-id="b3f53-417">如需特定服務的連接埠清單，請參閱 [HDInsight 上 Hadoop 服務所使用的連接埠](hdinsight-hadoop-port-settings-for-services.md)文件。</span><span class="sxs-lookup"><span data-stu-id="b3f53-417">For a list of ports for specific services, see the [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

<span data-ttu-id="b3f53-418">如需虛擬設備防火牆規則的詳細資訊，請參閱[虛擬設備案例](../virtual-network/virtual-network-scenario-udr-gw-nva.md)文件。</span><span class="sxs-lookup"><span data-stu-id="b3f53-418">For more information on firewall rules for virtual appliances, see the [virtual appliance scenario](../virtual-network/virtual-network-scenario-udr-gw-nva.md) document.</span></span>

## <span data-ttu-id="b3f53-419"><a id="hdinsight-nsg"></a>範例：網路安全性群組與 HDInsight</span><span class="sxs-lookup"><span data-stu-id="b3f53-419"><a id="hdinsight-nsg"></a>Example: network security groups with HDInsight</span></span>

<span data-ttu-id="b3f53-420">本節中的範例會示範如何建立網路安全性群組規則，以允許 HDInsight 與 Azure 管理服務進行通訊。</span><span class="sxs-lookup"><span data-stu-id="b3f53-420">The examples in this section demonstrate how to create network security group rules that allow HDInsight to communicate with the Azure management services.</span></span> <span data-ttu-id="b3f53-421">使用範例之前，請調整 IP 位址以符合您要使用之 Azure 區域的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b3f53-421">Before using the examples, adjust the IP addresses to match the ones for the Azure region you are using.</span></span> <span data-ttu-id="b3f53-422">您可以在[具有網路安全性群組和使用者定義路由的 HDInsight](#hdinsight-ip) 一節中找到這項資訊。</span><span class="sxs-lookup"><span data-stu-id="b3f53-422">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-resource-management-template"></a><span data-ttu-id="b3f53-423">Azure 資源管理範本</span><span class="sxs-lookup"><span data-stu-id="b3f53-423">Azure Resource Management template</span></span>

<span data-ttu-id="b3f53-424">下列資源管理範本會建立限制輸入流量的虛擬網路，但允許來自 HDInsight 所需 IP 位址的流量。</span><span class="sxs-lookup"><span data-stu-id="b3f53-424">The following Resource Management template creates a virtual network that restricts inbound traffic, but allows traffic from the IP addresses required by HDInsight.</span></span> <span data-ttu-id="b3f53-425">此範本也會在虛擬網路中建立 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="b3f53-425">This template also creates an HDInsight cluster in the virtual network.</span></span>

* [<span data-ttu-id="b3f53-426">部署安全的 Azure 虛擬網路和 HDInsight Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="b3f53-426">Deploy a secured Azure Virtual Network and an HDInsight Hadoop cluster</span></span>](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> <span data-ttu-id="b3f53-427">建立此範例中使用的 IP 位址，以符合您使用的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="b3f53-427">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="b3f53-428">您可以在[具有網路安全性群組和使用者定義路由的 HDInsight](#hdinsight-ip) 一節中找到這項資訊。</span><span class="sxs-lookup"><span data-stu-id="b3f53-428">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="b3f53-429">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3f53-429">Azure PowerShell</span></span>

<span data-ttu-id="b3f53-430">使用下列 PowerShell 指令碼建立限制輸入流量的虛擬網路，並允許來自北歐區域之 IP 位址的流量。</span><span class="sxs-lookup"><span data-stu-id="b3f53-430">Use the following PowerShell script to create a virtual network that restricts inbound traffic and allows traffic from the IP addresses for the North Europe region.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b3f53-431">建立此範例中使用的 IP 位址，以符合您使用的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="b3f53-431">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="b3f53-432">您可以在[具有網路安全性群組和使用者定義路由的 HDInsight](#hdinsight-ip) 一節中找到這項資訊。</span><span class="sxs-lookup"><span data-stu-id="b3f53-432">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with the resource group the virtual network is in"
$subnetName = "Replace with the name of the subnet that you plan to use for HDInsight"
# Get the Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get the region the Virtual network is in.
$location = $vnet.Location
# Get the subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for the HDInsight health and management services.
$nsg = New-AzureRmNetworkSecurityGroup `
    -Name "hdisecure" `
    -ResourceGroupName $resourceGroupName `
    -Location $location `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -name "hdirule1" `
        -Description "HDI health and management address 52.164.210.96" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "52.164.210.96" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 300 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 13.74.153.132" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "13.74.153.132" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 301 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.49.99" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.49.99" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 302 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 23.99.5.239" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "23.99.5.239" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 303 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 168.61.48.131" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "168.61.48.131" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 304 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "hdirule2" `
        -Description "HDI health and management 138.91.141.162" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "443" `
        -SourceAddressPrefix "138.91.141.162" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Allow `
        -Priority 305 `
        -Direction Inbound `
    | Add-AzureRmNetworkSecurityRuleConfig `
        -Name "blockeverything" `
        -Description "Block everything else" `
        -Protocol "*" `
        -SourcePortRange "*" `
        -DestinationPortRange "*" `
        -SourceAddressPrefix "Internet" `
        -DestinationAddressPrefix "VirtualNetwork" `
        -Access Deny `
        -Priority 500 `
        -Direction Inbound
# Set the changes to the security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply the NSG to the subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> <span data-ttu-id="b3f53-433">此範例示範如何新增規則，以允許所需 IP 位址上的輸入流量。</span><span class="sxs-lookup"><span data-stu-id="b3f53-433">This example demonstrates how to add rules to allow inbound traffic on the required IP addresses.</span></span> <span data-ttu-id="b3f53-434">它不會包含可限制其他來源之輸入存取的規則。</span><span class="sxs-lookup"><span data-stu-id="b3f53-434">It does not contain a rule to restrict inbound access from other sources.</span></span>
>
> <span data-ttu-id="b3f53-435">下列範例示範如何啟用從網際網路進行 SSH 存取：</span><span class="sxs-lookup"><span data-stu-id="b3f53-435">The following example demonstrates how to enable SSH access from the Internet:</span></span>
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a><span data-ttu-id="b3f53-436">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b3f53-436">Azure CLI</span></span>

<span data-ttu-id="b3f53-437">使用下列步驟建立限制輸入流量的虛擬網路，但允許來自 HDInsight 所需 IP 位址的流量。</span><span class="sxs-lookup"><span data-stu-id="b3f53-437">Use the following steps to create a virtual network that restricts inbound traffic, but allows traffic from the IP addresses required by HDInsight.</span></span>

1. <span data-ttu-id="b3f53-438">使用下列命令來建立名為 `hdisecure`的新網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="b3f53-438">Use the following command to create a new network security group named `hdisecure`.</span></span> <span data-ttu-id="b3f53-439">使用包含 Azure 虛擬網路的資源群組來取代 **RESOURCEGROUPNAME**。</span><span class="sxs-lookup"><span data-stu-id="b3f53-439">Replace **RESOURCEGROUPNAME** with the resource group that contains the Azure Virtual Network.</span></span> <span data-ttu-id="b3f53-440">使用群組建立所在的位置 (區域) 來取代 **LOCATION**。</span><span class="sxs-lookup"><span data-stu-id="b3f53-440">Replace **LOCATION** with the location (region) that the group was created in.</span></span>

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    <span data-ttu-id="b3f53-441">建立群組之後，您會收到新群組的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="b3f53-441">Once the group has been created, you receive information on the new group.</span></span>

2. <span data-ttu-id="b3f53-442">使用下列將規則新增至新的網路安全性群組，這些規則允許從 Azure HDInsight 健康狀態和管理服務透過連接埠 443 的輸入通訊。</span><span class="sxs-lookup"><span data-stu-id="b3f53-442">Use the following to add rules to the new network security group that allow inbound communication on port 443 from the Azure HDInsight health and management service.</span></span> <span data-ttu-id="b3f53-443">將 **RESOURCEGROUPNAME** 取代為包含 Azure 虛擬網路的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="b3f53-443">Replace **RESOURCEGROUPNAME** with the name of the resource group that contains the Azure Virtual Network.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b3f53-444">建立此範例中使用的 IP 位址，以符合您使用的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="b3f53-444">Change the IP addresses used in this example to match the Azure region you are using.</span></span> <span data-ttu-id="b3f53-445">您可以在[具有網路安全性群組和使用者定義路由的 HDInsight](#hdinsight-ip) 一節中找到這項資訊。</span><span class="sxs-lookup"><span data-stu-id="b3f53-445">You can find this information in the [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. <span data-ttu-id="b3f53-446">若要擷取此網路安全性群組的唯一識別碼，請使用下列命令：</span><span class="sxs-lookup"><span data-stu-id="b3f53-446">To retrieve the unique identifier for this network security group, use the following command:</span></span>

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    <span data-ttu-id="b3f53-447">此命令會傳回類似下列文字的值：</span><span class="sxs-lookup"><span data-stu-id="b3f53-447">This command returns a value similar to the following text:</span></span>

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    <span data-ttu-id="b3f53-448">如果未獲得預期的結果，請在命令中使用雙引號括住識別碼。</span><span class="sxs-lookup"><span data-stu-id="b3f53-448">Use double-quotes around id in the command if you don't get the expected results.</span></span>

4. <span data-ttu-id="b3f53-449">使用下列命令將網路安全性群組套用至子網路。</span><span class="sxs-lookup"><span data-stu-id="b3f53-449">Use the following command to apply the network security group to a subnet.</span></span> <span data-ttu-id="b3f53-450">使用上一個步驟傳回的值取代 __GUID__ 和 __RESOURCEGROUPNAME__ 的值。</span><span class="sxs-lookup"><span data-stu-id="b3f53-450">Replace the __GUID__ and __RESOURCEGROUPNAME__ values with the ones returned from the previous step.</span></span> <span data-ttu-id="b3f53-451">將 __VNETNAME__ 和 __SUBNETNAME__ 取代為您想要建立的虛擬網路名稱和子網路名稱。</span><span class="sxs-lookup"><span data-stu-id="b3f53-451">Replace __VNETNAME__ and __SUBNETNAME__ with the virtual network name and subnet name that you want to create.</span></span>

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    <span data-ttu-id="b3f53-452">此命令完成之後，您可以將 HDInsight 安裝至虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b3f53-452">Once this command completes, you can install HDInsight into the Virtual Network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b3f53-453">這些步驟只會開啟 Azure 雲端上 HDInsight 健康狀態和管理服務的存取權。</span><span class="sxs-lookup"><span data-stu-id="b3f53-453">These steps only open access to the HDInsight health and management service on the Azure cloud.</span></span> <span data-ttu-id="b3f53-454">任何其他來自虛擬網路外部之對 HDInsight 叢集的存取都會遭到封鎖。</span><span class="sxs-lookup"><span data-stu-id="b3f53-454">Any other access to the HDInsight cluster from outside the Virtual Network is blocked.</span></span> <span data-ttu-id="b3f53-455">若要允許從外部虛擬網路存取，您必須新增額外的網路安全性群組規則。</span><span class="sxs-lookup"><span data-stu-id="b3f53-455">To enable access from outside the virtual network, you must add additional Network Security Group rules.</span></span>
>
> <span data-ttu-id="b3f53-456">下列範例示範如何啟用從網際網路進行 SSH 存取：</span><span class="sxs-lookup"><span data-stu-id="b3f53-456">The following example demonstrates how to enable SSH access from the Internet:</span></span>
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <span data-ttu-id="b3f53-457"><a id="example-dns"></a> 範例：DNS 設定</span><span class="sxs-lookup"><span data-stu-id="b3f53-457"><a id="example-dns"></a> Example: DNS configuration</span></span>

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a><span data-ttu-id="b3f53-458">虛擬網路與已連線內部部署網路之間的名稱解析</span><span class="sxs-lookup"><span data-stu-id="b3f53-458">Name resolution between a virtual network and a connected on-premises network</span></span>

<span data-ttu-id="b3f53-459">此範例做出以下假設：</span><span class="sxs-lookup"><span data-stu-id="b3f53-459">This example makes the following assumptions:</span></span>

* <span data-ttu-id="b3f53-460">您的 Azure 虛擬網路會使用 VPN 閘道連線至內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="b3f53-460">You have an Azure Virtual Network that is connected to an on-premises network using a VPN gateway.</span></span>

* <span data-ttu-id="b3f53-461">虛擬網路中的自訂 DNS 伺服器會執行 Linux 或 Unix 作為作業系統。</span><span class="sxs-lookup"><span data-stu-id="b3f53-461">The custom DNS server in the virtual network is running Linux or Unix as the operating system.</span></span>

* <span data-ttu-id="b3f53-462">[Bind](https://www.isc.org/downloads/bind/) 安裝在自訂 DNS 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="b3f53-462">[Bind](https://www.isc.org/downloads/bind/) is installed on the custom DNS server.</span></span>

<span data-ttu-id="b3f53-463">在虛擬網路的自訂 DNS 伺服器上：</span><span class="sxs-lookup"><span data-stu-id="b3f53-463">On the custom DNS server in the virtual network:</span></span>

1. <span data-ttu-id="b3f53-464">若要尋找虛擬網路的 DNS 尾碼，請使用 Azure PowerShell 或 Azure CLI：</span><span class="sxs-lookup"><span data-stu-id="b3f53-464">Use either Azure PowerShell or Azure CLI to find the DNS suffix of the virtual network:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="b3f53-465">在虛擬網路的自訂 DNS 伺服器上，使用下列文字作為 `/etc/bind/named.conf.local` 檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="b3f53-465">On the custom DNS server for the virtual network, use the following text as the contents of the `/etc/bind/named.conf.local` file:</span></span>

    ```
    // Forward requests for the virtual network suffix to Azure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    <span data-ttu-id="b3f53-466">將 `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` 值取代為虛擬網路的 DNS 尾碼。</span><span class="sxs-lookup"><span data-stu-id="b3f53-466">Replace the `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with the DNS suffix of your virtual network.</span></span>

    <span data-ttu-id="b3f53-467">此設定會將虛擬網路 DNS 尾碼的所有 DNS 要求都路由傳送至 Azure 遞迴解析程式。</span><span class="sxs-lookup"><span data-stu-id="b3f53-467">This configuration routes all DNS requests for the DNS suffix of the virtual network to the Azure recursive resolver.</span></span>

2. <span data-ttu-id="b3f53-468">在虛擬網路的自訂 DNS 伺服器上，使用下列文字作為 `/etc/bind/named.conf.options` 檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="b3f53-468">On the custom DNS server for the virtual network, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients to accept requests from
    // TODO: Add the IP range of the joined network to this list
    acl goodclients {
        10.0.0.0/16; # IP address range of the virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent to the following
            forwarders {
                192.168.0.1; # Replace with the IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform to RFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="b3f53-469">將 `10.0.0.0/16` 值取代為虛擬網路的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="b3f53-469">Replace the `10.0.0.0/16` value with the IP address range of your virtual network.</span></span> <span data-ttu-id="b3f53-470">此項目允許來自此範圍內位址的名稱解析要求。</span><span class="sxs-lookup"><span data-stu-id="b3f53-470">This entry allows name resolution requests addresses within this range.</span></span>

    * <span data-ttu-id="b3f53-471">將內部部署網路的 IP 位址範圍新增至 `acl goodclients { ... }` 區段。</span><span class="sxs-lookup"><span data-stu-id="b3f53-471">Add the IP address range of the on-premises network to the `acl goodclients { ... }` section.</span></span>  <span data-ttu-id="b3f53-472">項目允許來自內部部署網路中資源的名稱解析要求。</span><span class="sxs-lookup"><span data-stu-id="b3f53-472">entry allows name resolution requests from resources in the on-premises network.</span></span>
    
    * <span data-ttu-id="b3f53-473">將 `192.168.0.1` 值取代為內部部署 DNS 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b3f53-473">Replace the value `192.168.0.1` with the IP address of your on-premises DNS server.</span></span> <span data-ttu-id="b3f53-474">此項目會將所有其他 DNS 要求路由傳送至內部部署 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b3f53-474">This entry routes all other DNS requests to the on-premises DNS server.</span></span>

3. <span data-ttu-id="b3f53-475">若要使用設定，請重新啟動 Bind。</span><span class="sxs-lookup"><span data-stu-id="b3f53-475">To use the configuration, restart Bind.</span></span> <span data-ttu-id="b3f53-476">例如： `sudo service bind9 restart`。</span><span class="sxs-lookup"><span data-stu-id="b3f53-476">For example, `sudo service bind9 restart`.</span></span>

4. <span data-ttu-id="b3f53-477">將條件式轉寄站新增至內部部署 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b3f53-477">Add a conditional forwarder to the on-premises DNS server.</span></span> <span data-ttu-id="b3f53-478">設定條件式轉寄站，以將步驟 1 中之 DNS 尾碼的要求傳送至自訂 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b3f53-478">Configure the conditional forwarder to send requests for the DNS suffix from step 1 to the custom DNS server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b3f53-479">如需如何新增條件式轉寄站的詳細資訊，請參閱 DNS 軟體的文件。</span><span class="sxs-lookup"><span data-stu-id="b3f53-479">Consult the documentation for your DNS software for specifics on how to add a conditional forwarder.</span></span>

<span data-ttu-id="b3f53-480">完成這些步驟之後，您可以使用完整網域名稱 (FQDN) 連線至任一虛擬網路中的資源。</span><span class="sxs-lookup"><span data-stu-id="b3f53-480">After completing these steps, you can connect to resources in either network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="b3f53-481">您現在可以將 HDInsight 安裝至虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b3f53-481">You can now install HDInsight into the virtual network.</span></span>

### <a name="name-resolution-between-two-connected-virtual-networks"></a><span data-ttu-id="b3f53-482">兩個已連線虛擬網路之間的名稱解析</span><span class="sxs-lookup"><span data-stu-id="b3f53-482">Name resolution between two connected virtual networks</span></span>

<span data-ttu-id="b3f53-483">此範例做出以下假設：</span><span class="sxs-lookup"><span data-stu-id="b3f53-483">This example makes the following assumptions:</span></span>

* <span data-ttu-id="b3f53-484">您的兩個 Azure 虛擬網路是使用 VPN 閘道或對等進行連線。</span><span class="sxs-lookup"><span data-stu-id="b3f53-484">You have two Azure Virtual Networks that are connected using either a VPN gateway or peering.</span></span>

* <span data-ttu-id="b3f53-485">兩個網路中的自訂 DNS 伺服器會執行 Linux 或 Unix 作為作業系統。</span><span class="sxs-lookup"><span data-stu-id="b3f53-485">The custom DNS server in both networks is running Linux or Unix as the operating system.</span></span>

* <span data-ttu-id="b3f53-486">[Bind](https://www.isc.org/downloads/bind/) 安裝在自訂 DNS 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="b3f53-486">[Bind](https://www.isc.org/downloads/bind/) is installed on the custom DNS servers.</span></span>

1. <span data-ttu-id="b3f53-487">若要尋找這兩個虛擬網路的 DNS 尾碼，請使用 Azure PowerShell 或 Azure CLI：</span><span class="sxs-lookup"><span data-stu-id="b3f53-487">Use either Azure PowerShell or Azure CLI to find the DNS suffix of both virtual networks:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter the resource group that contains the virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter the name of the resource group that contains the virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="b3f53-488">使用下列文字作為自訂 DNS 伺服器上 `/etc/bind/named.config.local` 檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="b3f53-488">Use the following text as the contents of the `/etc/bind/named.config.local` file on the custom DNS server.</span></span> <span data-ttu-id="b3f53-489">在這兩個虛擬網路的自訂 DNS 伺服器上進行這項變更。</span><span class="sxs-lookup"><span data-stu-id="b3f53-489">Make this change on the custom DNS server in both virtual networks.</span></span>

    ```
    // Forward requests for the virtual network suffix to Azure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # The IP address of the DNS server in the other virtual network
    };
    ```

    <span data-ttu-id="b3f53-490">將 `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` 值取代為「其他」虛擬網路的 DNS 尾碼。</span><span class="sxs-lookup"><span data-stu-id="b3f53-490">Replace the `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with the DNS suffix of the __other__ virtual network.</span></span> <span data-ttu-id="b3f53-491">此項目會將遠端網路 DNS 尾碼的要求路由傳送至該網路中的自訂 DNS。</span><span class="sxs-lookup"><span data-stu-id="b3f53-491">This entry routes requests for the DNS suffix of the remote network to the custom DNS in that network.</span></span>

3. <span data-ttu-id="b3f53-492">在這兩個虛擬網路的自訂 DNS 伺服器上，使用下列文字作為 `/etc/bind/named.conf.options` 檔案的內容：</span><span class="sxs-lookup"><span data-stu-id="b3f53-492">On the custom DNS servers in both virtual networks, use the following text as the contents of the `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients to accept requests from
    acl goodclients {
        10.1.0.0/16; # The IP address range of one virtual network
        10.0.0.0/16; # The IP address range of the other virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            forwarders {
            168.63.129.16;   # Azure recursive resolver         
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform to RFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="b3f53-493">將 `10.0.0.0/16` 和 `10.1.0.0/16` 值取代為虛擬網路的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="b3f53-493">Replace the `10.0.0.0/16` and `10.1.0.0/16` values with the IP address ranges of your virtual networks.</span></span> <span data-ttu-id="b3f53-494">此項目允許每個網路中的資源對 DNS 伺服器提出要求。</span><span class="sxs-lookup"><span data-stu-id="b3f53-494">This entry allows resources in each network to make requests of the DNS servers.</span></span>

    <span data-ttu-id="b3f53-495">不適用於虛擬網路 DNS 尾碼 (例如，microsoft.com) 的任何要求都是透過 Azure 遞迴解析程式所處理。</span><span class="sxs-lookup"><span data-stu-id="b3f53-495">Any requests that are not for the DNS suffixes of the virtual networks (for example, microsoft.com) is handled by the Azure recursive resolver.</span></span>

4. <span data-ttu-id="b3f53-496">若要使用設定，請重新啟動 Bind。</span><span class="sxs-lookup"><span data-stu-id="b3f53-496">To use the configuration, restart Bind.</span></span> <span data-ttu-id="b3f53-497">例如，兩部 DNS 伺服器上的 `sudo service bind9 restart`。</span><span class="sxs-lookup"><span data-stu-id="b3f53-497">For example, `sudo service bind9 restart` on both DNS servers.</span></span>

<span data-ttu-id="b3f53-498">完成這些步驟之後，您可以使用完整網域名稱 (FQDN) 連線至虛擬網路中的資源。</span><span class="sxs-lookup"><span data-stu-id="b3f53-498">After completing these steps, you can connect to resources in the virtual network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="b3f53-499">您現在可以將 HDInsight 安裝至虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b3f53-499">You can now install HDInsight into the virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3f53-500">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b3f53-500">Next steps</span></span>

* <span data-ttu-id="b3f53-501">如需設定 HDInsight 連線至內部部署網路的端對端範例，請參閱[將 HDInsight 連線至內部部署網路](./connect-on-premises-network.md)。</span><span class="sxs-lookup"><span data-stu-id="b3f53-501">For an end-to-end example of configuring HDInsight to connect to an on-premises network, see [Connect HDInsight to an on-premises network](./connect-on-premises-network.md).</span></span>

* <span data-ttu-id="b3f53-502">如需 Azure 虛擬網路的詳細資訊，請參閱 [Azure 虛擬網路概觀](../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="b3f53-502">For more information on Azure virtual networks, see the [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="b3f53-503">如需網路安全性群組的詳細資訊，請參閱[網路安全性群組](../virtual-network/virtual-networks-nsg.md)。</span><span class="sxs-lookup"><span data-stu-id="b3f53-503">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="b3f53-504">如需使用者定義路由的詳細資訊，請參閱[使用者定義路由和 IP 轉送](../virtual-network/virtual-networks-udr-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="b3f53-504">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>