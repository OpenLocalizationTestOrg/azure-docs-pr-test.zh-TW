---
title: "與虛擬網路的 Azure HDInsight aaaExtend |Microsoft 文件"
description: "了解如何 toouse Azure 虛擬網路 tooconnect HDInsight tooother 雲端資源或您的資料中心中的資源"
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
ms.openlocfilehash: ba80be4d9f280c6c62fa8acc996ef5f921acdbbd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="extend-azure-hdinsight-using-an-azure-virtual-network"></a><span data-ttu-id="6ffb4-103">使用 Azure 虛擬網路延伸 Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="6ffb4-103">Extend Azure HDInsight using an Azure Virtual Network</span></span>

<span data-ttu-id="6ffb4-104">深入了解如何 toouse HDInsight 與[Azure 虛擬網路](../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-104">Learn how toouse HDInsight with an [Azure Virtual Network](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="6ffb4-105">使用 Azure 虛擬網路可讓 hello 下列案例：</span><span class="sxs-lookup"><span data-stu-id="6ffb4-105">Using an Azure Virtual Network enables hello following scenarios:</span></span>

* <span data-ttu-id="6ffb4-106">直接從內部部署網路連接 tooHDInsight。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-106">Connecting tooHDInsight directly from an on-premises network.</span></span>

* <span data-ttu-id="6ffb4-107">連接 HDInsight toodata 會儲存在 Azure 虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-107">Connecting HDInsight toodata stores in an Azure Virtual network.</span></span>

* <span data-ttu-id="6ffb4-108">直接存取 Hadoop 服務無法使用的公開超過 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-108">Directly accessing Hadoop services that are not available publicly over hello internet.</span></span> <span data-ttu-id="6ffb4-109">例如，Kafka 應用程式開發介面或 hello HBase Java 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-109">For example, Kafka APIs or hello HBase Java API.</span></span>

> [!WARNING]
> <span data-ttu-id="6ffb4-110">本文件中的 hello 資訊需要 TCP/IP 網路中了的解。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-110">hello information in this document requires an understanding of TCP/IP networking.</span></span> <span data-ttu-id="6ffb4-111">如果您不熟悉使用 TCP/IP 網路中，您應該與之前進行修改 tooproduction 網路的人員合作。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-111">If you are not familiar with TCP/IP networking, you should partner with someone who is before making modifications tooproduction networks.</span></span>

## <a name="planning"></a><span data-ttu-id="6ffb4-112">規劃</span><span class="sxs-lookup"><span data-stu-id="6ffb4-112">Planning</span></span>

<span data-ttu-id="6ffb4-113">hello 下面是 hello 規劃 tooinstall HDInsight 中的虛擬網路時，您必須回答的問題：</span><span class="sxs-lookup"><span data-stu-id="6ffb4-113">hello following are hello questions that you must answer when planning tooinstall HDInsight in a virtual network:</span></span>

* <span data-ttu-id="6ffb4-114">您需要 tooinstall HDInsight 到現有的虛擬網路嗎？</span><span class="sxs-lookup"><span data-stu-id="6ffb4-114">Do you need tooinstall HDInsight into an existing virtual network?</span></span> <span data-ttu-id="6ffb4-115">或者，您要建立新的網路嗎？</span><span class="sxs-lookup"><span data-stu-id="6ffb4-115">Or are you creating a new network?</span></span>

    <span data-ttu-id="6ffb4-116">如果您使用現有的虛擬網路，您可能需要 toomodify hello 網路組態，才能安裝 HDInsight。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-116">If you are using an existing virtual network, you may need toomodify hello network configuration before you can install HDInsight.</span></span> <span data-ttu-id="6ffb4-117">如需詳細資訊，請參閱 hello[新增 HDInsight tooan 現有的虛擬網路](#existingvnet)> 一節。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-117">For more information, see hello [add HDInsight tooan existing virtual network](#existingvnet) section.</span></span>

* <span data-ttu-id="6ffb4-118">您想 tooconnect hello 虛擬網路包含 HDInsight tooanother 虛擬網路或內部部署網路嗎？</span><span class="sxs-lookup"><span data-stu-id="6ffb4-118">Do you want tooconnect hello virtual network containing HDInsight tooanother virtual network or your on-premises network?</span></span>

    <span data-ttu-id="6ffb4-119">tooeasily 工作以跨網路資源，您可能需要 toocreate 自訂 DNS，並設定 DNS 轉送。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-119">tooeasily work with resources across networks, you may need toocreate a custom DNS and configure DNS forwarding.</span></span> <span data-ttu-id="6ffb4-120">如需詳細資訊，請參閱 hello[連接多個網路](#multinet)> 一節。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-120">For more information, see hello [connecting multiple networks](#multinet) section.</span></span>

* <span data-ttu-id="6ffb4-121">您想 toorestrict/重新導向輸入或輸出流量 tooHDInsight 嗎？</span><span class="sxs-lookup"><span data-stu-id="6ffb4-121">Do you want toorestrict/redirect inbound or outbound traffic tooHDInsight?</span></span>

    <span data-ttu-id="6ffb4-122">HDInsight 必須具有無限制的 hello Azure 資料中心中的特定 IP 位址的通訊。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-122">HDInsight must have unrestricted communication with specific IP addresses in hello Azure data center.</span></span> <span data-ttu-id="6ffb4-123">另外還有數個連接埠必須允許通過防火牆才能進行用戶端通訊。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-123">There are also several ports that must be allowed through firewalls for client communication.</span></span> <span data-ttu-id="6ffb4-124">如需詳細資訊，請參閱 hello[控制網路流量](#networktraffic)> 一節。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-124">For more information, see hello [controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="6ffb4-125"><a id="existingvnet"></a>新增 HDInsight tooan 現有的虛擬網路</span><span class="sxs-lookup"><span data-stu-id="6ffb4-125"><a id="existingvnet"></a>Add HDInsight tooan existing virtual network</span></span>

<span data-ttu-id="6ffb4-126">如何使用這個區段 toodiscover 中的 hello 步驟 tooadd 新的 HDInsight tooan，現有的 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-126">Use hello steps in this section toodiscover how tooadd a new HDInsight tooan existing Azure Virtual Network.</span></span>

> [!NOTE]
> <span data-ttu-id="6ffb4-127">您無法在虛擬網路中新增現有的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-127">You cannot add an existing HDInsight cluster into a virtual network.</span></span>

1. <span data-ttu-id="6ffb4-128">您使用傳統 」 或 「 資源管理員部署模型 hello 虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="6ffb4-128">Are you using a classic or Resource Manager deployment model for hello virtual network?</span></span>

    <span data-ttu-id="6ffb4-129">HDInsight 3.4 和更新版本需要 Resource Manager 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-129">HDInsight 3.4 and greater requires a Resource Manager virtual network.</span></span> <span data-ttu-id="6ffb4-130">舊版 HDInsight 需要傳統虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-130">Earlier versions of HDInsight required a classic virtual network.</span></span>

    <span data-ttu-id="6ffb4-131">如果您現有的網路是傳統的虛擬網路，您必須建立資源管理員的虛擬網路，然後再連接兩個 hello。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-131">If your existing network is a classic virtual network, then you must create a Resource Manager virtual network and then connect hello two.</span></span> <span data-ttu-id="6ffb4-132">[連接傳統 Vnet toonew Vnet](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-132">[Connecting classic VNets toonew VNets](../vpn-gateway/vpn-gateway-connect-different-deployment-models-portal.md).</span></span>

    <span data-ttu-id="6ffb4-133">一旦加入，HDInsight hello 資源管理員網路中安裝可以互動 hello 傳統網路中的資源。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-133">Once joined, HDInsight installed in hello Resource Manager network can interact with resources in hello classic network.</span></span>

2. <span data-ttu-id="6ffb4-134">您使用強制通道嗎？</span><span class="sxs-lookup"><span data-stu-id="6ffb4-134">Do you use forced tunneling?</span></span> <span data-ttu-id="6ffb4-135">強制通道是子網路設定，會強制檢查的傳出網際網路流量 tooa 裝置和記錄。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-135">Forced tunneling is a subnet setting that forces outbound Internet traffic tooa device for inspection and logging.</span></span> <span data-ttu-id="6ffb4-136">HDInsight 不支援強制通道。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-136">HDInsight does not support forced tunneling.</span></span> <span data-ttu-id="6ffb4-137">先移除強制通道，再將 HDInsight 安裝至子網路，或建立 HDInsight 的新子網路。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-137">Either remove forced tunneling before installing HDInsight into a subnet, or create a new subnet for HDInsight.</span></span>

3. <span data-ttu-id="6ffb4-138">您使用網路安全性群組的相關、 使用者定義的路由或虛擬網路應用裝置 toorestrict 流量傳入或傳出 hello 虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="6ffb4-138">Do you use network security groups, user-defined routes, or Virtual Network Appliances toorestrict traffic into or out of hello virtual network?</span></span>

    <span data-ttu-id="6ffb4-139">為受管理的服務，HDInsight 需要 hello Azure 資料中心中的無限制的存取 tooseveral IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-139">As a managed service, HDInsight requires unrestricted access tooseveral IP addresses in hello Azure data center.</span></span> <span data-ttu-id="6ffb4-140">tooallow 通訊，這些 IP 位址，與更新的任何現有的網路安全性群組或使用者定義的路由。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-140">tooallow communication with these IP addresses, update any existing network security groups or user-defined routes.</span></span>

    <span data-ttu-id="6ffb4-141">HDInsight 會裝載多個使用各種連接埠的服務。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-141">HDInsight  hosts multiple services, which use a variety of ports.</span></span> <span data-ttu-id="6ffb4-142">不會封鎖流量 toothese 連接埠。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-142">Do not block traffic toothese ports.</span></span> <span data-ttu-id="6ffb4-143">如需通過虛擬設備的防火牆連接埠 tooallow 的清單，請參閱 hello[安全性](#security)> 一節。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-143">For a list of ports tooallow through virtual appliance firewalls, see hello [Security](#security) section.</span></span>

    <span data-ttu-id="6ffb4-144">toofind 您現有的安全性組態，使用下列 Azure PowerShell 或 Azure CLI 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6ffb4-144">toofind your existing security configuration, use hello following Azure PowerShell or Azure CLI commands:</span></span>

    * <span data-ttu-id="6ffb4-145">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="6ffb4-145">Network security groups</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermnetworksecuritygroup -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network nsg list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="6ffb4-146">如需詳細資訊，請參閱 hello[疑難排解網路安全性群組](../virtual-network/virtual-network-nsg-troubleshoot-portal.md)文件。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-146">For more information, see hello [Troubleshoot network security groups](../virtual-network/virtual-network-nsg-troubleshoot-portal.md) document.</span></span>

        > [!IMPORTANT]
        > <span data-ttu-id="6ffb4-147">會根據規則優先順序依序套用網路安全性群組規則。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-147">Network security group rules are applied in order based on rule priority.</span></span> <span data-ttu-id="6ffb4-148">hello 符合 hello 流量模式的第一個規則會套用，且沒有其他適用於該流量。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-148">hello first rule that matches hello traffic pattern is applied, and no others are applied for that traffic.</span></span> <span data-ttu-id="6ffb4-149">順序從最寬鬆 tooleast 寬鬆的規則。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-149">Order rules from most permissive tooleast permissive.</span></span> <span data-ttu-id="6ffb4-150">如需詳細資訊，請參閱 hello[篩選網路流量的網路安全性群組](../virtual-network/virtual-networks-nsg.md)文件。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-150">For more information, see hello [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    * <span data-ttu-id="6ffb4-151">使用者定義的路由</span><span class="sxs-lookup"><span data-stu-id="6ffb4-151">User-defined routes</span></span>

        ```powershell
        $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
        get-azurermroutetable -resourcegroupname $resourceGroupName
        ```

        ```azurecli-interactive
        read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
        az network route-table list --resource-group $RESOURCEGROUP
        ```

        <span data-ttu-id="6ffb4-152">如需詳細資訊，請參閱 hello[疑難排解路由](../virtual-network/virtual-network-routes-troubleshoot-portal.md)文件。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-152">For more information, see hello [Troubleshoot routes](../virtual-network/virtual-network-routes-troubleshoot-portal.md) document.</span></span>

4. <span data-ttu-id="6ffb4-153">建立 HDInsight 叢集，並在設定期間選取 hello Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-153">Create an HDInsight cluster and select hello Azure Virtual Network during configuration.</span></span> <span data-ttu-id="6ffb4-154">使用下列文件 toounderstand hello 叢集建立程序的 hello 中 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="6ffb4-154">Use hello steps in hello following documents toounderstand hello cluster creation process:</span></span>

    * [<span data-ttu-id="6ffb4-155">建立 HDInsight 使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6ffb4-155">Create HDInsight using hello Azure portal</span></span>](hdinsight-hadoop-create-linux-clusters-portal.md)
    * [<span data-ttu-id="6ffb4-156">使用 Azure PowerShell 建立 HDInsight</span><span class="sxs-lookup"><span data-stu-id="6ffb4-156">Create HDInsight using Azure PowerShell</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
    * [<span data-ttu-id="6ffb4-157">使用 Azure CLI 1.0 建立 HDInsight</span><span class="sxs-lookup"><span data-stu-id="6ffb4-157">Create HDInsight using Azure CLI 1.0</span></span>](hdinsight-hadoop-create-linux-clusters-azure-cli.md)
    * [<span data-ttu-id="6ffb4-158">使用 Azure Resource Manager 範本建立 HDInsight</span><span class="sxs-lookup"><span data-stu-id="6ffb4-158">Create HDInsight using an Azure Resource Manager template</span></span>](hdinsight-hadoop-create-linux-clusters-arm-templates.md)

  > [!IMPORTANT]
  > <span data-ttu-id="6ffb4-159">新增 HDInsight tooa 虛擬網路是選用設定步驟。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-159">Adding HDInsight tooa virtual network is an optional configuration step.</span></span> <span data-ttu-id="6ffb4-160">設定 hello 叢集時，是確定 tooselect hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-160">Be sure tooselect hello virtual network when configuring hello cluster.</span></span>

## <span data-ttu-id="6ffb4-161"><a id="multinet"></a>連線多個網路</span><span class="sxs-lookup"><span data-stu-id="6ffb4-161"><a id="multinet"></a>Connecting multiple networks</span></span>

<span data-ttu-id="6ffb4-162">hello 與多個網路設定最大的挑戰是 hello 網路之間的名稱解析。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-162">hello biggest challenge with a multi-network configuration is name resolution between hello networks.</span></span>

<span data-ttu-id="6ffb4-163">Azure 會針對安裝於虛擬網路中的 Azure 服務提供名稱解析。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-163">Azure provides name resolution for Azure services that are installed in a virtual network.</span></span> <span data-ttu-id="6ffb4-164">此內建的名稱解析可讓 HDInsight tooconnect toohello 下列使用完整的網域名稱 (FQDN) 的資源：</span><span class="sxs-lookup"><span data-stu-id="6ffb4-164">This built-in name resolution allows HDInsight tooconnect toohello following resources by using a fully qualified domain name (FQDN):</span></span>

* <span data-ttu-id="6ffb4-165">可使用的任何資源 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-165">Any resource that is available on hello internet.</span></span> <span data-ttu-id="6ffb4-166">例如，microsoft.com、google.com。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-166">For example, microsoft.com, google.com.</span></span>

* <span data-ttu-id="6ffb4-167">是在 hello 相同 Azure 虛擬網路，使用 hello 任何資源__內部 DNS 名稱__的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-167">Any resource that is in hello same Azure Virtual Network, by using hello __internal DNS name__ of hello resource.</span></span> <span data-ttu-id="6ffb4-168">例如，當使用 hello 預設名稱解析，hello 如下範例內部 DNS 名稱指派的 tooHDInsight 背景工作節點：</span><span class="sxs-lookup"><span data-stu-id="6ffb4-168">For example, when using hello default name resolution, hello following are example internal DNS names assigned tooHDInsight worker nodes:</span></span>

    * <span data-ttu-id="6ffb4-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="6ffb4-169">wn0-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>
    * <span data-ttu-id="6ffb4-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="6ffb4-170">wn2-hdinsi.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net</span></span>

    <span data-ttu-id="6ffb4-171">這些節點可以使用內部 DNS 名稱彼此直接通訊，以及與 HDInsight 中的其他節點通訊。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-171">Both these nodes can communicate directly with each other, and other nodes in HDInsight, by using internal DNS names.</span></span>

<span data-ttu-id="6ffb4-172">hello 預設名稱解析沒有__不__內聯結的 toohello 虛擬網路的網路中允許 HDInsight tooresolve hello 資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-172">hello default name resolution does __not__ allow HDInsight tooresolve hello names of resources in networks that are joined toohello virtual network.</span></span> <span data-ttu-id="6ffb4-173">比方說，是通用 toojoin 您內部網路 toohello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-173">For example, it is common toojoin your on-premises network toohello virtual network.</span></span> <span data-ttu-id="6ffb4-174">只有 hello 預設名稱解析，HDInsight 無法透過名稱存取 hello 與內部網路中的資源。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-174">With only hello default name resolution, HDInsight cannot access resources in hello on-premises network by name.</span></span> <span data-ttu-id="6ffb4-175">相反的 hello 也是為 true，在內部部署網路中的資源無法透過名稱存取 hello 虛擬網路中的資源。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-175">hello opposite is also true, resources in your on-premises network cannot access resources in hello virtual network by name.</span></span>

> [!WARNING]
> <span data-ttu-id="6ffb4-176">您必須建立 hello 自訂 DNS 伺服器，並設定 hello 虛擬網路 toouse 它之前建立 hello HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-176">You must create hello custom DNS server and configure hello virtual network toouse it before creating hello HDInsight cluster.</span></span>

<span data-ttu-id="6ffb4-177">tooenable hello 虛擬網路之間聯結的網路中的資源名稱解析，您必須執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="6ffb4-177">tooenable name resolution between hello virtual network and resources in joined networks, you must perform hello following actions:</span></span>

1. <span data-ttu-id="6ffb4-178">Hello 您計劃 tooinstall HDInsight 的 Azure 虛擬網路中建立自訂的 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-178">Create a custom DNS server in hello Azure Virtual Network where you plan tooinstall HDInsight.</span></span>

2. <span data-ttu-id="6ffb4-179">Hello 虛擬網路 toouse hello 自訂 DNS 伺服器設定。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-179">Configure hello virtual network toouse hello custom DNS server.</span></span>

3. <span data-ttu-id="6ffb4-180">Azure 虛擬網路的 DNS 尾碼指派給的 hello 中尋找。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-180">Find hello Azure assigned DNS suffix for your virtual network.</span></span> <span data-ttu-id="6ffb4-181">此值就會類似太`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-181">This value is similar too`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`.</span></span> <span data-ttu-id="6ffb4-182">如需尋找 hello DNS 尾碼，請參閱 hello[範例： 自訂 DNS](#example-dns) > 一節。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-182">For information on finding hello DNS suffix, see hello [Example: Custom DNS](#example-dns) section.</span></span>

4. <span data-ttu-id="6ffb4-183">設定 hello DNS 伺服器之間的轉送。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-183">Configure forwarding between hello DNS servers.</span></span> <span data-ttu-id="6ffb4-184">遠端網路 hello 類型 hello 組態而定。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-184">hello configuration depends on hello type of remote network.</span></span>

    * <span data-ttu-id="6ffb4-185">如果 hello 遠端網路與內部網路，設定 DNS，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6ffb4-185">If hello remote network is an on-premises network, configure DNS as follows:</span></span>
        
        * <span data-ttu-id="6ffb4-186">__自訂 DNS__ （hello 虛擬網路中）：</span><span class="sxs-lookup"><span data-stu-id="6ffb4-186">__Custom DNS__ (in hello virtual network):</span></span>

            * <span data-ttu-id="6ffb4-187">轉寄要求 hello hello 虛擬網路 toohello Azure 遞迴解析程式 (168.63.129.16) 的 DNS 尾碼。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-187">Forward requests for hello DNS suffix of hello virtual network toohello Azure recursive resolver (168.63.129.16).</span></span> <span data-ttu-id="6ffb4-188">Azure 會處理 hello 虛擬網路中的資源的要求</span><span class="sxs-lookup"><span data-stu-id="6ffb4-188">Azure handles requests for resources in hello virtual network</span></span>

            * <span data-ttu-id="6ffb4-189">轉寄所有其他要求 toohello 在內部部署 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-189">Forward all other requests toohello on-premises DNS server.</span></span> <span data-ttu-id="6ffb4-190">hello 內部 DNS 會處理所有其他的名稱解析要求，甚至是網際網路資源，例如 Microsoft.com 要求。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-190">hello on-premises DNS handles all other name resolution requests, even requests for internet resources such as Microsoft.com.</span></span>

        * <span data-ttu-id="6ffb4-191">__在內部部署 DNS__: hello 虛擬網路的 DNS 尾碼 toohello 自訂 DNS 伺服器的要求轉送。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-191">__On-premises DNS__: Forward requests for hello virtual network DNS suffix toohello custom DNS server.</span></span> <span data-ttu-id="6ffb4-192">hello 自訂 DNS 伺服器，然後轉送 toohello Azure 遞迴解析程式。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-192">hello custom DNS server then forwards toohello Azure recursive resolver.</span></span>

        <span data-ttu-id="6ffb4-193">此組態路由要求完整網域名稱包含 hello hello 虛擬網路 toohello 自訂 DNS 伺服器的 DNS 尾碼。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-193">This configuration routes requests for fully qualified domain names that contain hello DNS suffix of hello virtual network toohello custom DNS server.</span></span> <span data-ttu-id="6ffb4-194">Hello 在內部部署 DNS 伺服器會處理 （即使是針對公用的網際網路位址） 的所有其他要求。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-194">All other requests (even for public internet addresses) are handled by hello on-premises DNS server.</span></span>

    * <span data-ttu-id="6ffb4-195">如果另一個 Azure 虛擬網路 hello 遠端網路，設定 DNS，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6ffb4-195">If hello remote network is another Azure Virtual Network, configure DNS as follows:</span></span>

        * <span data-ttu-id="6ffb4-196">「自訂 DNS」(在每個虛擬網路中)：</span><span class="sxs-lookup"><span data-stu-id="6ffb4-196">__Custom DNS__ (in each virtual network):</span></span>

            * <span data-ttu-id="6ffb4-197">Hello hello 虛擬網路的 DNS 尾碼的要求都會轉送 toohello 自訂 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-197">Requests for hello DNS suffix of hello virtual networks are forwarded toohello custom DNS servers.</span></span> <span data-ttu-id="6ffb4-198">每個虛擬網路中的 hello DNS 會負責解析其網路內的資源。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-198">hello DNS in each virtual network is responsible for resolving resources within its network.</span></span>

            * <span data-ttu-id="6ffb4-199">轉寄所有其他要求 toohello Azure 遞迴解析程式。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-199">Forward all other requests toohello Azure recursive resolver.</span></span> <span data-ttu-id="6ffb4-200">hello 遞迴解析程式負責解決本機和網際網路資源。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-200">hello recursive resolver is responsible for resolving local and internet resources.</span></span>

        <span data-ttu-id="6ffb4-201">每個網路的 hello DNS 伺服器會將轉送要求 toohello 其他，根據 DNS 尾碼。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-201">hello DNS server for each network forwards requests toohello other, based on DNS suffix.</span></span> <span data-ttu-id="6ffb4-202">其他要求會解析使用 hello Azure 遞迴解析程式。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-202">Other requests are resolved using hello Azure recursive resolver.</span></span>

    <span data-ttu-id="6ffb4-203">如需每個組態的範例，請參閱 hello[範例： 自訂 DNS](#example-dns) > 一節。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-203">For an example of each configuration, see hello [Example: Custom DNS](#example-dns) section.</span></span>

<span data-ttu-id="6ffb4-204">如需詳細資訊，請參閱 hello [Vm 和角色執行個體的名稱解析](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server)文件。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-204">For more information, see hello [Name Resolution for VMs and Role Instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md#name-resolution-using-your-own-dns-server) document.</span></span>

## <a name="directly-connect-toohadoop-services"></a><span data-ttu-id="6ffb4-205">直接連接 tooHadoop 服務</span><span class="sxs-lookup"><span data-stu-id="6ffb4-205">Directly connect tooHadoop services</span></span>

<span data-ttu-id="6ffb4-206">HDInsight 上的大部分文件假設您有存取 toohello 叢集 hello 透過網際網路。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-206">Most documentation on HDInsight assumes that you have access toohello cluster over hello internet.</span></span> <span data-ttu-id="6ffb4-207">例如，您可以連接 https://CLUSTERNAME.azurehdinsight.net toohello 叢集。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-207">For example, that you can connect toohello cluster at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="6ffb4-208">這個位址會使用 hello 公用閘道，如果您已經使用 Nsg，或從 UDRs toorestrict 存取 hello 網際網路，則無法使用此。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-208">This address uses hello public gateway, which is not available if you have used NSGs or UDRs toorestrict access from hello internet.</span></span>

<span data-ttu-id="6ffb4-209">tooconnect tooAmbari 和其他網頁透過 hello 虛擬網路，使用下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6ffb4-209">tooconnect tooAmbari and other web pages through hello virtual network, use hello following steps:</span></span>

1. <span data-ttu-id="6ffb4-210">toodiscover hello 內部的完整的網域名稱 (FQDN) 的 hello HDInsight 叢集節點，使用其中一種 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="6ffb4-210">toodiscover hello internal fully qualified domain names (FQDN) of hello HDInsight cluster nodes, use one of hello following methods:</span></span>

    ```powershell
    $resourceGroupName = "hello resource group that contains hello virtual network used with HDInsight"

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

    <span data-ttu-id="6ffb4-211">在 [hello] 清單中傳回的節點，尋找 hello FQDN hello 前端節點和使用 hello Fqdn tooconnect tooAmbari 及其他 web 服務。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-211">In hello list of nodes returned, find hello FQDN for hello head nodes and use hello FQDNs tooconnect tooAmbari and other web services.</span></span> <span data-ttu-id="6ffb4-212">例如，使用`http://<headnode-fqdn>:8080`tooaccess Ambari。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-212">For example, use `http://<headnode-fqdn>:8080` tooaccess Ambari.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6ffb4-213">某些 hello 前端節點上裝載的服務才一次一個節點上使用中。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-213">Some services hosted on hello head nodes are only active on one node at a time.</span></span> <span data-ttu-id="6ffb4-214">如果您嘗試存取一個前端節點上的服務，它會傳回 404 錯誤，請切換 toohello 其他前端節點。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-214">If you try accessing a service on one head node and it returns a 404 error, switch toohello other head node.</span></span>

2. <span data-ttu-id="6ffb4-215">toodetermine hello 節點和可用通訊埠的服務，請參閱 hello [HDInsight 上的 Hadoop 服務所使用的連接埠](./hdinsight-hadoop-port-settings-for-services.md)文件。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-215">toodetermine hello node and port that a service is available on, see hello [Ports used by Hadoop services on HDInsight](./hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

## <span data-ttu-id="6ffb4-216"><a id="networktraffic"></a> 控制網路流量</span><span class="sxs-lookup"><span data-stu-id="6ffb4-216"><a id="networktraffic"></a> Controlling network traffic</span></span>

<span data-ttu-id="6ffb4-217">您可以使用下列方法 hello 控制 Azure 虛擬網路中的網路流量：</span><span class="sxs-lookup"><span data-stu-id="6ffb4-217">Network traffic in an Azure Virtual Networks can be controlled using hello following methods:</span></span>

* <span data-ttu-id="6ffb4-218">**網路安全性群組**(NSG) toofilter 輸入和輸出流量 toohello 網路可讓您。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-218">**Network security groups** (NSG) allow you toofilter inbound and outbound traffic toohello network.</span></span> <span data-ttu-id="6ffb4-219">如需詳細資訊，請參閱 hello[篩選網路流量的網路安全性群組](../virtual-network/virtual-networks-nsg.md)文件。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-219">For more information, see hello [Filter network traffic with network security groups](../virtual-network/virtual-networks-nsg.md) document.</span></span>

    > [!WARNING]
    > <span data-ttu-id="6ffb4-220">HDInsight 不支援限制輸出流量。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-220">HDInsight does not support restricting outbound traffic.</span></span>

* <span data-ttu-id="6ffb4-221">**使用者定義的路由**(UDR) 定義流量在 hello 網路資源之間流動的方式。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-221">**User-defined routes** (UDR) define how traffic flows between resources in hello network.</span></span> <span data-ttu-id="6ffb4-222">如需詳細資訊，請參閱 hello[使用者定義的路由與 IP 轉送](../virtual-network/virtual-networks-udr-overview.md)文件。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-222">For more information, see hello [User-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md) document.</span></span>

* <span data-ttu-id="6ffb4-223">**網路虛擬裝置**複寫 hello 功能的裝置，例如防火牆和路由器。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-223">**Network virtual appliances** replicate hello functionality of devices such as firewalls and routers.</span></span> <span data-ttu-id="6ffb4-224">如需詳細資訊，請參閱 hello[網路應用裝置](https://azure.microsoft.com/solutions/network-appliances)文件。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-224">For more information, see hello [Network Appliances](https://azure.microsoft.com/solutions/network-appliances) document.</span></span>

<span data-ttu-id="6ffb4-225">為受管理的服務，HDInsight 需要無限制的存取 tooAzure 健全狀況和管理服務在 hello Azure 雲端中。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-225">As a managed service, HDInsight requires unrestricted access tooAzure health and management services in hello Azure cloud.</span></span> <span data-ttu-id="6ffb4-226">使用 NSG 和 UDR 時，您必須確定這些服務仍然可以與 HDInsight 進行通訊。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-226">When using NSGs and UDRs, you must ensure that HDInsight these services can still communicate with HDInsight.</span></span>

<span data-ttu-id="6ffb4-227">HDInsight 會在數個連接埠上公開服務。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-227">HDInsight exposes services on several ports.</span></span> <span data-ttu-id="6ffb4-228">時使用的虛擬設備的防火牆，您必須允許流量 hello 用於這些服務的通訊埠。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-228">When using a virtual appliance firewall, you must allow traffic on hello ports used for these services.</span></span> <span data-ttu-id="6ffb4-229">如需詳細資訊，請參閱 hello [必要的連接埠] 區段。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-229">For more information, see hello [Required ports] section.</span></span>

### <span data-ttu-id="6ffb4-230"><a id="hdinsight-ip"></a> 具有網路安全性群組和使用者定義路由的 HDInsight</span><span class="sxs-lookup"><span data-stu-id="6ffb4-230"><a id="hdinsight-ip"></a> HDInsight with network security groups and user-defined routes</span></span>

<span data-ttu-id="6ffb4-231">如果您計劃使用**網路安全性群組**或**使用者定義的路由**toocontrol 網路流量，請執行下列動作，然後再安裝 HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="6ffb4-231">If you plan on using **network security groups** or **user-defined routes** toocontrol network traffic, perform hello following actions before installing HDInsight:</span></span>

1. <span data-ttu-id="6ffb4-232">識別 hello toouse 規劃 HDInsight 的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-232">Identify hello Azure region that you plan toouse for HDInsight.</span></span>

2. <span data-ttu-id="6ffb4-233">識別所需的 HDInsight hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-233">Identify hello IP addresses required by HDInsight.</span></span> <span data-ttu-id="6ffb4-234">如需詳細資訊，請參閱 hello [HDInsight 所需的 IP 位址](#hdinsight-ip)> 一節。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-234">For more information, see hello [IP Addresses required by HDInsight](#hdinsight-ip) section.</span></span>

3. <span data-ttu-id="6ffb4-235">建立或修改 hello 網路安全性群組或使用者定義您計劃 tooinstall HDInsight hello 子網路的路由到。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-235">Create or modify hello network security groups or user-defined routes for hello subnet that you plan tooinstall HDInsight into.</span></span>

    * <span data-ttu-id="6ffb4-236">__網路安全性群組__： 允許__輸入__連接埠的流量__443__來自 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-236">__Network security groups__: allow __inbound__ traffic on port __443__ from hello IP addresses.</span></span>
    * <span data-ttu-id="6ffb4-237">__使用者定義的路由__： 建立路由 tooeach IP 位址，以及設定 hello__下個躍點類型__too__Internet__。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-237">__User-defined routes__: create a route tooeach IP address and set hello __Next hop type__ too__Internet__.</span></span>

<span data-ttu-id="6ffb4-238">如需網路安全性群組或使用者定義的路由的詳細資訊，請參閱下列文件的 hello:</span><span class="sxs-lookup"><span data-stu-id="6ffb4-238">For more information on network security groups or user-defined routes, see hello following documentation:</span></span>

* [<span data-ttu-id="6ffb4-239">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="6ffb4-239">Network security group</span></span>](../virtual-network/virtual-networks-nsg.md)

* [<span data-ttu-id="6ffb4-240">使用者定義路由</span><span class="sxs-lookup"><span data-stu-id="6ffb4-240">User-defined routes</span></span>](../virtual-network/virtual-networks-udr-overview.md)

#### <a name="forced-tunneling"></a><span data-ttu-id="6ffb4-241">強制通道</span><span class="sxs-lookup"><span data-stu-id="6ffb4-241">Forced tunneling</span></span>

<span data-ttu-id="6ffb4-242">強制通道是其中所有流量子網路都是強制的 tooa 特定網路或位置，例如您在內部部署網路的使用者定義的路由組態。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-242">Forced tunneling is a user-defined routing configuration where all traffic from a subnet is forced tooa specific network or location, such as your on-premises network.</span></span> <span data-ttu-id="6ffb4-243">HDInsight「不」支援強制通道。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-243">HDInsight does __not__ support forced tunneling.</span></span>

## <span data-ttu-id="6ffb4-244"><a id="hdinsight-ip"></a> 所需的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="6ffb4-244"><a id="hdinsight-ip"></a> Required IP addresses</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ffb4-245">hello Azure 的健全狀況並管理服務必須與 HDInsight 無法 toocommunicate。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-245">hello Azure health and management services must be able toocommunicate with HDInsight.</span></span> <span data-ttu-id="6ffb4-246">如果您使用網路安全性群組或使用者定義的路由，允許從 hello 流量這些服務 tooreach HDInsight 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-246">If you use network security groups or user-defined routes, allow traffic from hello IP addresses for these services tooreach HDInsight.</span></span>
>
> <span data-ttu-id="6ffb4-247">如果您不想使用網路安全性群組或使用者定義的路由 toocontrol 流量，您可以忽略此區段。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-247">If you do not use network security groups or user-defined routes toocontrol traffic, you can ignore this section.</span></span>

<span data-ttu-id="6ffb4-248">如果您使用網路安全性群組或使用者定義的路由，您必須允許來自 hello Azure 健康情況與管理服務 tooreach HDInsight 的流量。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-248">If you use network security groups or user-defined routes, you must allow traffic from hello Azure health and management services tooreach HDInsight.</span></span> <span data-ttu-id="6ffb4-249">使用下列步驟 toofind hello 允許的 IP 位址必須是 hello:</span><span class="sxs-lookup"><span data-stu-id="6ffb4-249">Use hello following steps toofind hello IP addresses that must be allowed:</span></span>

1. <span data-ttu-id="6ffb4-250">您永遠必須允許來自下列 IP 位址的 hello 流量：</span><span class="sxs-lookup"><span data-stu-id="6ffb4-250">You must always allow traffic from hello following IP addresses:</span></span>

    | <span data-ttu-id="6ffb4-251">IP 位址</span><span class="sxs-lookup"><span data-stu-id="6ffb4-251">IP address</span></span> | <span data-ttu-id="6ffb4-252">允許的連接埠</span><span class="sxs-lookup"><span data-stu-id="6ffb4-252">Allowed port</span></span> | <span data-ttu-id="6ffb4-253">方向</span><span class="sxs-lookup"><span data-stu-id="6ffb4-253">Direction</span></span> |
    | ---- | ----- | ----- |
    | <span data-ttu-id="6ffb4-254">168.61.49.99</span><span class="sxs-lookup"><span data-stu-id="6ffb4-254">168.61.49.99</span></span> | <span data-ttu-id="6ffb4-255">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-255">443</span></span> | <span data-ttu-id="6ffb4-256">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-256">Inbound</span></span> |
    | <span data-ttu-id="6ffb4-257">23.99.5.239</span><span class="sxs-lookup"><span data-stu-id="6ffb4-257">23.99.5.239</span></span> | <span data-ttu-id="6ffb4-258">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-258">443</span></span> | <span data-ttu-id="6ffb4-259">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-259">Inbound</span></span> |
    | <span data-ttu-id="6ffb4-260">168.61.48.131</span><span class="sxs-lookup"><span data-stu-id="6ffb4-260">168.61.48.131</span></span> | <span data-ttu-id="6ffb4-261">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-261">443</span></span> | <span data-ttu-id="6ffb4-262">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-262">Inbound</span></span> |
    | <span data-ttu-id="6ffb4-263">138.91.141.162</span><span class="sxs-lookup"><span data-stu-id="6ffb4-263">138.91.141.162</span></span> | <span data-ttu-id="6ffb4-264">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-264">443</span></span> | <span data-ttu-id="6ffb4-265">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-265">Inbound</span></span> |

2. <span data-ttu-id="6ffb4-266">如果您的 HDInsight 叢集位於 hello 下列區域的其中一個，您必須允許從 hello hello 地區列出的 IP 位址的流量：</span><span class="sxs-lookup"><span data-stu-id="6ffb4-266">If your HDInsight cluster is in one of hello following regions, then you must allow traffic from hello IP addresses listed for hello region:</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6ffb4-267">如果未列出 hello 您使用的 Azure 區域，則只能使用步驟 1 中的 hello 四個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-267">If hello Azure region you are using is not listed, then only use hello four IP addresses from step 1.</span></span>

    | <span data-ttu-id="6ffb4-268">國家 (地區)</span><span class="sxs-lookup"><span data-stu-id="6ffb4-268">Country</span></span> | <span data-ttu-id="6ffb4-269">區域</span><span class="sxs-lookup"><span data-stu-id="6ffb4-269">Region</span></span> | <span data-ttu-id="6ffb4-270">允許的 IP 位址</span><span class="sxs-lookup"><span data-stu-id="6ffb4-270">Allowed IP addresses</span></span> | <span data-ttu-id="6ffb4-271">允許的連接埠</span><span class="sxs-lookup"><span data-stu-id="6ffb4-271">Allowed port</span></span> | <span data-ttu-id="6ffb4-272">方向</span><span class="sxs-lookup"><span data-stu-id="6ffb4-272">Direction</span></span> |
    | ---- | ---- | ---- | ---- | ----- |
    | <span data-ttu-id="6ffb4-273">亞洲</span><span class="sxs-lookup"><span data-stu-id="6ffb4-273">Asia</span></span> | <span data-ttu-id="6ffb4-274">東亞</span><span class="sxs-lookup"><span data-stu-id="6ffb4-274">East Asia</span></span> | <span data-ttu-id="6ffb4-275">23.102.235.122</span><span class="sxs-lookup"><span data-stu-id="6ffb4-275">23.102.235.122</span></span></br><span data-ttu-id="6ffb4-276">52.175.38.134</span><span class="sxs-lookup"><span data-stu-id="6ffb4-276">52.175.38.134</span></span> | <span data-ttu-id="6ffb4-277">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-277">443</span></span> | <span data-ttu-id="6ffb4-278">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-278">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="6ffb4-279">東南亞</span><span class="sxs-lookup"><span data-stu-id="6ffb4-279">Southeast Asia</span></span> | <span data-ttu-id="6ffb4-280">13.76.245.160</span><span class="sxs-lookup"><span data-stu-id="6ffb4-280">13.76.245.160</span></span></br><span data-ttu-id="6ffb4-281">13.76.136.249</span><span class="sxs-lookup"><span data-stu-id="6ffb4-281">13.76.136.249</span></span> | <span data-ttu-id="6ffb4-282">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-282">443</span></span> | <span data-ttu-id="6ffb4-283">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-283">Inbound</span></span> |
    | <span data-ttu-id="6ffb4-284">澳大利亞</span><span class="sxs-lookup"><span data-stu-id="6ffb4-284">Australia</span></span> | <span data-ttu-id="6ffb4-285">澳洲東部</span><span class="sxs-lookup"><span data-stu-id="6ffb4-285">Australia East</span></span> | <span data-ttu-id="6ffb4-286">104.210.84.115</span><span class="sxs-lookup"><span data-stu-id="6ffb4-286">104.210.84.115</span></span></br><span data-ttu-id="6ffb4-287">13.75.152.195</span><span class="sxs-lookup"><span data-stu-id="6ffb4-287">13.75.152.195</span></span> | <span data-ttu-id="6ffb4-288">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-288">443</span></span> | <span data-ttu-id="6ffb4-289">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-289">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="6ffb4-290">澳大利亞東南部</span><span class="sxs-lookup"><span data-stu-id="6ffb4-290">Australia Southeast</span></span> | <span data-ttu-id="6ffb4-291">13.77.2.56</span><span class="sxs-lookup"><span data-stu-id="6ffb4-291">13.77.2.56</span></span></br><span data-ttu-id="6ffb4-292">13.77.2.94</span><span class="sxs-lookup"><span data-stu-id="6ffb4-292">13.77.2.94</span></span> | <span data-ttu-id="6ffb4-293">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-293">443</span></span> | <span data-ttu-id="6ffb4-294">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-294">Inbound</span></span> |
    | <span data-ttu-id="6ffb4-295">巴西</span><span class="sxs-lookup"><span data-stu-id="6ffb4-295">Brazil</span></span> | <span data-ttu-id="6ffb4-296">巴西南部</span><span class="sxs-lookup"><span data-stu-id="6ffb4-296">Brazil South</span></span> | <span data-ttu-id="6ffb4-297">191.235.84.104</span><span class="sxs-lookup"><span data-stu-id="6ffb4-297">191.235.84.104</span></span></br><span data-ttu-id="6ffb4-298">191.235.87.113</span><span class="sxs-lookup"><span data-stu-id="6ffb4-298">191.235.87.113</span></span> | <span data-ttu-id="6ffb4-299">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-299">443</span></span> | <span data-ttu-id="6ffb4-300">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-300">Inbound</span></span> |
    | <span data-ttu-id="6ffb4-301">加拿大</span><span class="sxs-lookup"><span data-stu-id="6ffb4-301">Canada</span></span> | <span data-ttu-id="6ffb4-302">加拿大東部</span><span class="sxs-lookup"><span data-stu-id="6ffb4-302">Canada East</span></span> | <span data-ttu-id="6ffb4-303">52.229.127.96</span><span class="sxs-lookup"><span data-stu-id="6ffb4-303">52.229.127.96</span></span></br><span data-ttu-id="6ffb4-304">52.229.123.172</span><span class="sxs-lookup"><span data-stu-id="6ffb4-304">52.229.123.172</span></span> | <span data-ttu-id="6ffb4-305">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-305">443</span></span> | <span data-ttu-id="6ffb4-306">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-306">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="6ffb4-307">加拿大中部</span><span class="sxs-lookup"><span data-stu-id="6ffb4-307">Canada Central</span></span> | <span data-ttu-id="6ffb4-308">52.228.37.66</span><span class="sxs-lookup"><span data-stu-id="6ffb4-308">52.228.37.66</span></span></br><span data-ttu-id="6ffb4-309">52.228.45.222</span><span class="sxs-lookup"><span data-stu-id="6ffb4-309">52.228.45.222</span></span> | <span data-ttu-id="6ffb4-310">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-310">443</span></span> | <span data-ttu-id="6ffb4-311">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-311">Inbound</span></span> |
    | <span data-ttu-id="6ffb4-312">中國</span><span class="sxs-lookup"><span data-stu-id="6ffb4-312">China</span></span> | <span data-ttu-id="6ffb4-313">中國北部</span><span class="sxs-lookup"><span data-stu-id="6ffb4-313">China North</span></span> | <span data-ttu-id="6ffb4-314">42.159.96.170</span><span class="sxs-lookup"><span data-stu-id="6ffb4-314">42.159.96.170</span></span></br><span data-ttu-id="6ffb4-315">139.217.2.219</span><span class="sxs-lookup"><span data-stu-id="6ffb4-315">139.217.2.219</span></span> | <span data-ttu-id="6ffb4-316">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-316">443</span></span> | <span data-ttu-id="6ffb4-317">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-317">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="6ffb4-318">中國東部</span><span class="sxs-lookup"><span data-stu-id="6ffb4-318">China East</span></span> | <span data-ttu-id="6ffb4-319">42.159.198.178</span><span class="sxs-lookup"><span data-stu-id="6ffb4-319">42.159.198.178</span></span></br><span data-ttu-id="6ffb4-320">42.159.234.157</span><span class="sxs-lookup"><span data-stu-id="6ffb4-320">42.159.234.157</span></span> | <span data-ttu-id="6ffb4-321">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-321">443</span></span> | <span data-ttu-id="6ffb4-322">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-322">Inbound</span></span> |
    | <span data-ttu-id="6ffb4-323">歐洲</span><span class="sxs-lookup"><span data-stu-id="6ffb4-323">Europe</span></span> | <span data-ttu-id="6ffb4-324">北歐</span><span class="sxs-lookup"><span data-stu-id="6ffb4-324">North Europe</span></span> | <span data-ttu-id="6ffb4-325">52.164.210.96</span><span class="sxs-lookup"><span data-stu-id="6ffb4-325">52.164.210.96</span></span></br><span data-ttu-id="6ffb4-326">13.74.153.132</span><span class="sxs-lookup"><span data-stu-id="6ffb4-326">13.74.153.132</span></span> | <span data-ttu-id="6ffb4-327">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-327">443</span></span> | <span data-ttu-id="6ffb4-328">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-328">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="6ffb4-329">西歐</span><span class="sxs-lookup"><span data-stu-id="6ffb4-329">West Europe</span></span>| <span data-ttu-id="6ffb4-330">52.166.243.90</span><span class="sxs-lookup"><span data-stu-id="6ffb4-330">52.166.243.90</span></span></br><span data-ttu-id="6ffb4-331">52.174.36.244</span><span class="sxs-lookup"><span data-stu-id="6ffb4-331">52.174.36.244</span></span> | <span data-ttu-id="6ffb4-332">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-332">443</span></span> | <span data-ttu-id="6ffb4-333">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-333">Inbound</span></span> |
    | <span data-ttu-id="6ffb4-334">德國</span><span class="sxs-lookup"><span data-stu-id="6ffb4-334">Germany</span></span> | <span data-ttu-id="6ffb4-335">德國中部</span><span class="sxs-lookup"><span data-stu-id="6ffb4-335">Germany Central</span></span> | <span data-ttu-id="6ffb4-336">51.4.146.68</span><span class="sxs-lookup"><span data-stu-id="6ffb4-336">51.4.146.68</span></span></br><span data-ttu-id="6ffb4-337">51.4.146.80</span><span class="sxs-lookup"><span data-stu-id="6ffb4-337">51.4.146.80</span></span> | <span data-ttu-id="6ffb4-338">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-338">443</span></span> | <span data-ttu-id="6ffb4-339">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-339">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="6ffb4-340">德國東北部</span><span class="sxs-lookup"><span data-stu-id="6ffb4-340">Germany Northeast</span></span> | <span data-ttu-id="6ffb4-341">51.5.150.132</span><span class="sxs-lookup"><span data-stu-id="6ffb4-341">51.5.150.132</span></span></br><span data-ttu-id="6ffb4-342">51.5.144.101</span><span class="sxs-lookup"><span data-stu-id="6ffb4-342">51.5.144.101</span></span> | <span data-ttu-id="6ffb4-343">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-343">443</span></span> | <span data-ttu-id="6ffb4-344">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-344">Inbound</span></span> |
    | <span data-ttu-id="6ffb4-345">印度</span><span class="sxs-lookup"><span data-stu-id="6ffb4-345">India</span></span> | <span data-ttu-id="6ffb4-346">印度中部</span><span class="sxs-lookup"><span data-stu-id="6ffb4-346">Central India</span></span> | <span data-ttu-id="6ffb4-347">52.172.153.209</span><span class="sxs-lookup"><span data-stu-id="6ffb4-347">52.172.153.209</span></span></br><span data-ttu-id="6ffb4-348">52.172.152.49</span><span class="sxs-lookup"><span data-stu-id="6ffb4-348">52.172.152.49</span></span> | <span data-ttu-id="6ffb4-349">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-349">443</span></span> | <span data-ttu-id="6ffb4-350">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-350">Inbound</span></span> |
    | <span data-ttu-id="6ffb4-351">日本</span><span class="sxs-lookup"><span data-stu-id="6ffb4-351">Japan</span></span> | <span data-ttu-id="6ffb4-352">日本東部</span><span class="sxs-lookup"><span data-stu-id="6ffb4-352">Japan East</span></span> | <span data-ttu-id="6ffb4-353">13.78.125.90</span><span class="sxs-lookup"><span data-stu-id="6ffb4-353">13.78.125.90</span></span></br><span data-ttu-id="6ffb4-354">13.78.89.60</span><span class="sxs-lookup"><span data-stu-id="6ffb4-354">13.78.89.60</span></span> | <span data-ttu-id="6ffb4-355">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-355">443</span></span> | <span data-ttu-id="6ffb4-356">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-356">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="6ffb4-357">日本西部</span><span class="sxs-lookup"><span data-stu-id="6ffb4-357">Japan West</span></span> | <span data-ttu-id="6ffb4-358">40.74.125.69</span><span class="sxs-lookup"><span data-stu-id="6ffb4-358">40.74.125.69</span></span></br><span data-ttu-id="6ffb4-359">138.91.29.150</span><span class="sxs-lookup"><span data-stu-id="6ffb4-359">138.91.29.150</span></span> | <span data-ttu-id="6ffb4-360">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-360">443</span></span> | <span data-ttu-id="6ffb4-361">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-361">Inbound</span></span> |
    | <span data-ttu-id="6ffb4-362">韓國</span><span class="sxs-lookup"><span data-stu-id="6ffb4-362">Korea</span></span> | <span data-ttu-id="6ffb4-363">韓國中部</span><span class="sxs-lookup"><span data-stu-id="6ffb4-363">Korea Central</span></span> | <span data-ttu-id="6ffb4-364">52.231.39.142</span><span class="sxs-lookup"><span data-stu-id="6ffb4-364">52.231.39.142</span></span></br><span data-ttu-id="6ffb4-365">52.231.36.209</span><span class="sxs-lookup"><span data-stu-id="6ffb4-365">52.231.36.209</span></span> | <span data-ttu-id="6ffb4-366">433</span><span class="sxs-lookup"><span data-stu-id="6ffb4-366">433</span></span> | <span data-ttu-id="6ffb4-367">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-367">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="6ffb4-368">韓國南部</span><span class="sxs-lookup"><span data-stu-id="6ffb4-368">Korea South</span></span> | <span data-ttu-id="6ffb4-369">52.231.203.16</span><span class="sxs-lookup"><span data-stu-id="6ffb4-369">52.231.203.16</span></span></br><span data-ttu-id="6ffb4-370">52.231.205.214</span><span class="sxs-lookup"><span data-stu-id="6ffb4-370">52.231.205.214</span></span> | <span data-ttu-id="6ffb4-371">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-371">443</span></span> | <span data-ttu-id="6ffb4-372">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-372">Inbound</span></span>
    | <span data-ttu-id="6ffb4-373">英國</span><span class="sxs-lookup"><span data-stu-id="6ffb4-373">United Kingdom</span></span> | <span data-ttu-id="6ffb4-374">英國西部</span><span class="sxs-lookup"><span data-stu-id="6ffb4-374">UK West</span></span> | <span data-ttu-id="6ffb4-375">51.141.13.110</span><span class="sxs-lookup"><span data-stu-id="6ffb4-375">51.141.13.110</span></span></br><span data-ttu-id="6ffb4-376">51.141.7.20</span><span class="sxs-lookup"><span data-stu-id="6ffb4-376">51.141.7.20</span></span> | <span data-ttu-id="6ffb4-377">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-377">443</span></span> | <span data-ttu-id="6ffb4-378">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-378">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="6ffb4-379">英國南部</span><span class="sxs-lookup"><span data-stu-id="6ffb4-379">UK South</span></span> | <span data-ttu-id="6ffb4-380">51.140.47.39</span><span class="sxs-lookup"><span data-stu-id="6ffb4-380">51.140.47.39</span></span></br><span data-ttu-id="6ffb4-381">51.140.52.16</span><span class="sxs-lookup"><span data-stu-id="6ffb4-381">51.140.52.16</span></span> | <span data-ttu-id="6ffb4-382">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-382">443</span></span> | <span data-ttu-id="6ffb4-383">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-383">Inbound</span></span> |
    | <span data-ttu-id="6ffb4-384">美國</span><span class="sxs-lookup"><span data-stu-id="6ffb4-384">United States</span></span> | <span data-ttu-id="6ffb4-385">美國中部</span><span class="sxs-lookup"><span data-stu-id="6ffb4-385">Central US</span></span> | <span data-ttu-id="6ffb4-386">13.67.223.215</span><span class="sxs-lookup"><span data-stu-id="6ffb4-386">13.67.223.215</span></span></br><span data-ttu-id="6ffb4-387">40.86.83.253</span><span class="sxs-lookup"><span data-stu-id="6ffb4-387">40.86.83.253</span></span> | <span data-ttu-id="6ffb4-388">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-388">443</span></span> | <span data-ttu-id="6ffb4-389">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-389">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="6ffb4-390">美國中北部</span><span class="sxs-lookup"><span data-stu-id="6ffb4-390">North Central US</span></span> | <span data-ttu-id="6ffb4-391">157.56.8.38</span><span class="sxs-lookup"><span data-stu-id="6ffb4-391">157.56.8.38</span></span></br><span data-ttu-id="6ffb4-392">157.55.213.99</span><span class="sxs-lookup"><span data-stu-id="6ffb4-392">157.55.213.99</span></span> | <span data-ttu-id="6ffb4-393">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-393">443</span></span> | <span data-ttu-id="6ffb4-394">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-394">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="6ffb4-395">美國中西部</span><span class="sxs-lookup"><span data-stu-id="6ffb4-395">West Central US</span></span> | <span data-ttu-id="6ffb4-396">52.161.23.15</span><span class="sxs-lookup"><span data-stu-id="6ffb4-396">52.161.23.15</span></span></br><span data-ttu-id="6ffb4-397">52.161.10.167</span><span class="sxs-lookup"><span data-stu-id="6ffb4-397">52.161.10.167</span></span> | <span data-ttu-id="6ffb4-398">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-398">443</span></span> | <span data-ttu-id="6ffb4-399">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-399">Inbound</span></span> |
    | &nbsp; | <span data-ttu-id="6ffb4-400">美國西部 2</span><span class="sxs-lookup"><span data-stu-id="6ffb4-400">West US 2</span></span> | <span data-ttu-id="6ffb4-401">52.175.211.210</span><span class="sxs-lookup"><span data-stu-id="6ffb4-401">52.175.211.210</span></span></br><span data-ttu-id="6ffb4-402">52.175.222.222</span><span class="sxs-lookup"><span data-stu-id="6ffb4-402">52.175.222.222</span></span> | <span data-ttu-id="6ffb4-403">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-403">443</span></span> | <span data-ttu-id="6ffb4-404">輸入</span><span class="sxs-lookup"><span data-stu-id="6ffb4-404">Inbound</span></span> |

    <span data-ttu-id="6ffb4-405">有關 hello IP 位址 Azure 政府 toouse，請參閱 hello [Azure 政府智慧 + 分析](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics)文件。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-405">For information on hello IP addresses toouse for Azure Government, see hello [Azure Government Intelligence + Analytics](https://docs.microsoft.com/azure/azure-government/documentation-government-services-intelligenceandanalytics) document.</span></span>

3. <span data-ttu-id="6ffb4-406">如果您搭配使用自訂 DNS 伺服器與虛擬網路，則也必須允許從 __168.63.129.16__ 進行存取。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-406">If you use a custom DNS server with your virtual network, you must also allow access from __168.63.129.16__.</span></span> <span data-ttu-id="6ffb4-407">此位址是 Azure 遞迴解析程式。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-407">This address is Azure's recursive resolver.</span></span> <span data-ttu-id="6ffb4-408">如需詳細資訊，請參閱 hello[名稱解析的 Vm 和角色執行個體](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md)文件。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-408">For more information, see hello [Name resolution for VMs and Role instances](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md) document.</span></span>

<span data-ttu-id="6ffb4-409">如需詳細資訊，請參閱 hello[控制網路流量](#networktraffic)> 一節。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-409">For more information, see hello [Controlling network traffic](#networktraffic) section.</span></span>

## <span data-ttu-id="6ffb4-410"><a id="hdinsight-ports"></a> 所需連接埠</span><span class="sxs-lookup"><span data-stu-id="6ffb4-410"><a id="hdinsight-ports"></a> Required ports</span></span>

<span data-ttu-id="6ffb4-411">如果您打算使用網路**虛擬設備防火牆**toosecure hello 虛擬網路，您必須在 hello 下列連接埠上允許輸出流量：</span><span class="sxs-lookup"><span data-stu-id="6ffb4-411">If you plan on using a network **virtual appliance firewall** toosecure hello virtual network, you must allow outbound traffic on hello following ports:</span></span>

* <span data-ttu-id="6ffb4-412">53</span><span class="sxs-lookup"><span data-stu-id="6ffb4-412">53</span></span>
* <span data-ttu-id="6ffb4-413">443</span><span class="sxs-lookup"><span data-stu-id="6ffb4-413">443</span></span>
* <span data-ttu-id="6ffb4-414">1433</span><span class="sxs-lookup"><span data-stu-id="6ffb4-414">1433</span></span>
* <span data-ttu-id="6ffb4-415">11000-11999</span><span class="sxs-lookup"><span data-stu-id="6ffb4-415">11000-11999</span></span>
* <span data-ttu-id="6ffb4-416">14000-14999</span><span class="sxs-lookup"><span data-stu-id="6ffb4-416">14000-14999</span></span>

<span data-ttu-id="6ffb4-417">如需特定的服務連接埠的清單，請參閱 hello [HDInsight 上的 Hadoop 服務所使用的連接埠](hdinsight-hadoop-port-settings-for-services.md)文件。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-417">For a list of ports for specific services, see hello [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md) document.</span></span>

<span data-ttu-id="6ffb4-418">如需有關虛擬應用程式的防火牆規則的詳細資訊，請參閱 hello[虛擬設備案例](../virtual-network/virtual-network-scenario-udr-gw-nva.md)文件。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-418">For more information on firewall rules for virtual appliances, see hello [virtual appliance scenario](../virtual-network/virtual-network-scenario-udr-gw-nva.md) document.</span></span>

## <span data-ttu-id="6ffb4-419"><a id="hdinsight-nsg"></a>範例：網路安全性群組與 HDInsight</span><span class="sxs-lookup"><span data-stu-id="6ffb4-419"><a id="hdinsight-nsg"></a>Example: network security groups with HDInsight</span></span>

<span data-ttu-id="6ffb4-420">本節中的 hello 範例示範如何 toocreate 網路安全性群組規則來允許 HDInsight toocommunicate hello 與 Azure 的管理服務。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-420">hello examples in this section demonstrate how toocreate network security group rules that allow HDInsight toocommunicate with hello Azure management services.</span></span> <span data-ttu-id="6ffb4-421">使用 hello 範例之前，調整 hello IP 位址 toomatch hello 的 hello 您使用的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-421">Before using hello examples, adjust hello IP addresses toomatch hello ones for hello Azure region you are using.</span></span> <span data-ttu-id="6ffb4-422">您可以找到此資訊在 hello[網路安全性群組和使用者定義的路由與 HDInsight](#hdinsight-ip) > 一節。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-422">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-resource-management-template"></a><span data-ttu-id="6ffb4-423">Azure 資源管理範本</span><span class="sxs-lookup"><span data-stu-id="6ffb4-423">Azure Resource Management template</span></span>

<span data-ttu-id="6ffb4-424">hello 下列資源管理範本建立虛擬網路時，限制的輸入的流量，但允許來自 hello HDInsight 所需的 IP 位址的流量。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-424">hello following Resource Management template creates a virtual network that restricts inbound traffic, but allows traffic from hello IP addresses required by HDInsight.</span></span> <span data-ttu-id="6ffb4-425">此範本也會 hello 虛擬網路中建立的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-425">This template also creates an HDInsight cluster in hello virtual network.</span></span>

* [<span data-ttu-id="6ffb4-426">部署安全的 Azure 虛擬網路和 HDInsight Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="6ffb4-426">Deploy a secured Azure Virtual Network and an HDInsight Hadoop cluster</span></span>](https://azure.microsoft.com/resources/templates/101-hdinsight-secure-vnet/)

> [!IMPORTANT]
> <span data-ttu-id="6ffb4-427">變更用於此範例 toomatch hello 您使用的 Azure 區域中的 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-427">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="6ffb4-428">您可以找到此資訊在 hello[網路安全性群組和使用者定義的路由與 HDInsight](#hdinsight-ip) > 一節。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-428">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

### <a name="azure-powershell"></a><span data-ttu-id="6ffb4-429">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6ffb4-429">Azure PowerShell</span></span>

<span data-ttu-id="6ffb4-430">使用下列 PowerShell 指令碼 toocreate 限制的輸入的流量，並允許流量從 hello hello 北歐區域的 IP 位址的虛擬網路的 hello。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-430">Use hello following PowerShell script toocreate a virtual network that restricts inbound traffic and allows traffic from hello IP addresses for hello North Europe region.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ffb4-431">變更用於此範例 toomatch hello 您使用的 Azure 區域中的 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-431">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="6ffb4-432">您可以找到此資訊在 hello[網路安全性群組和使用者定義的路由與 HDInsight](#hdinsight-ip) > 一節。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-432">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

```powershell
$vnetName = "Replace with your virtual network name"
$resourceGroupName = "Replace with hello resource group hello virtual network is in"
$subnetName = "Replace with hello name of hello subnet that you plan toouse for HDInsight"
# Get hello Virtual Network object
$vnet = Get-AzureRmVirtualNetwork `
    -Name $vnetName `
    -ResourceGroupName $resourceGroupName
# Get hello region hello Virtual network is in.
$location = $vnet.Location
# Get hello subnet object
$subnet = $vnet.Subnets | Where-Object Name -eq $subnetName
# Create a Network Security Group.
# And add exemptions for hello HDInsight health and management services.
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
# Set hello changes toohello security group
Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
# Apply hello NSG toohello subnet
Set-AzureRmVirtualNetworkSubnetConfig `
    -VirtualNetwork $vnet `
    -Name $subnetName `
    -AddressPrefix $subnet.AddressPrefix `
    -NetworkSecurityGroup $nsg
```

> [!IMPORTANT]
> <span data-ttu-id="6ffb4-433">此範例示範如何 tooadd 規則 tooallow 輸入 hello 所需的 IP 位址的流量。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-433">This example demonstrates how tooadd rules tooallow inbound traffic on hello required IP addresses.</span></span> <span data-ttu-id="6ffb4-434">它不包含規則 toorestrict 輸入從其他來源的存取。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-434">It does not contain a rule toorestrict inbound access from other sources.</span></span>
>
> <span data-ttu-id="6ffb4-435">hello 下列範例將示範如何從 hello 網際網路存取 tooenable SSH:</span><span class="sxs-lookup"><span data-stu-id="6ffb4-435">hello following example demonstrates how tooenable SSH access from hello Internet:</span></span>
>
> ```powershell
> Add-AzureRmNetworkSecurityRuleConfig -Name "SSH" -Description "SSH" -Protocol "*" -SourcePortRange "*" -DestinationPortRange "22" -SourceAddressPrefix "*" -DestinationAddressPrefix "VirtualNetwork" -Access Allow -Priority 306 -Direction Inbound
> ```

### <a name="azure-cli"></a><span data-ttu-id="6ffb4-436">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6ffb4-436">Azure CLI</span></span>

<span data-ttu-id="6ffb4-437">使用下列步驟 toocreate 限制的輸入的流量，但允許流量從 hello HDInsight 所需的 IP 位址的虛擬網路的 hello。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-437">Use hello following steps toocreate a virtual network that restricts inbound traffic, but allows traffic from hello IP addresses required by HDInsight.</span></span>

1. <span data-ttu-id="6ffb4-438">使用下列命令 toocreate 名為新的網路安全性群組的 hello `hdisecure`。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-438">Use hello following command toocreate a new network security group named `hdisecure`.</span></span> <span data-ttu-id="6ffb4-439">取代**RESOURCEGROUPNAME** hello 包含 hello Azure 虛擬網路的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-439">Replace **RESOURCEGROUPNAME** with hello resource group that contains hello Azure Virtual Network.</span></span> <span data-ttu-id="6ffb4-440">取代**位置**該 hello 群組建立在與 hello 位置 （地區）。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-440">Replace **LOCATION** with hello location (region) that hello group was created in.</span></span>

    ```azurecli
    az network nsg create -g RESOURCEGROUPNAME -n hdisecure -l LOCATION
    ```

    <span data-ttu-id="6ffb4-441">一旦建立 hello 群組之後，您會收到 hello 新群組的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-441">Once hello group has been created, you receive information on hello new group.</span></span>

2. <span data-ttu-id="6ffb4-442">使用下列 tooadd 規則 toohello 新網路安全性群組，允許傳入的通訊連接埠 443 從 hello Azure HDInsight 健全狀況和管理服務的 hello。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-442">Use hello following tooadd rules toohello new network security group that allow inbound communication on port 443 from hello Azure HDInsight health and management service.</span></span> <span data-ttu-id="6ffb4-443">取代**RESOURCEGROUPNAME** hello hello 包含 hello Azure 虛擬網路的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-443">Replace **RESOURCEGROUPNAME** with hello name of hello resource group that contains hello Azure Virtual Network.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6ffb4-444">變更用於此範例 toomatch hello 您使用的 Azure 區域中的 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-444">Change hello IP addresses used in this example toomatch hello Azure region you are using.</span></span> <span data-ttu-id="6ffb4-445">您可以找到此資訊在 hello[網路安全性群組和使用者定義的路由與 HDInsight](#hdinsight-ip) > 一節。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-445">You can find this information in hello [HDInsight with network security groups and user-defined routes](#hdinsight-ip) section.</span></span>

    ```azurecli
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule1 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "52.164.210.96" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 300 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "13.74.153.132" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 301 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.49.99" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 302 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "23.99.5.239" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 303 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "168.61.48.131" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 304 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule2 --protocol "*" --source-port-range "*" --destination-port-range "443" --source-address-prefix "138.91.141.162" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 305 --direction "Inbound"
    az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n block --protocol "*" --source-port-range "*" --destination-port-range "*" --source-address-prefix "Internet" --destination-address-prefix "VirtualNetwork" --access "Deny" --priority 500 --direction "Inbound"
    ```

3. <span data-ttu-id="6ffb4-446">tooretrieve hello 此網路安全性群組的唯一識別碼，請使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="6ffb4-446">tooretrieve hello unique identifier for this network security group, use hello following command:</span></span>

    ```azurecli
    az network nsg show -g RESOURCEGROUPNAME -n hdisecure --query 'id'
    ```

    <span data-ttu-id="6ffb4-447">此命令會傳回值的類似 toohello，下列文字：</span><span class="sxs-lookup"><span data-stu-id="6ffb4-447">This command returns a value similar toohello following text:</span></span>

        "/subscriptions/SUBSCRIPTIONID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"

    <span data-ttu-id="6ffb4-448">如果沒有得到預期的 hello 結果，請使用雙引號括住識別碼 hello 命令中。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-448">Use double-quotes around id in hello command if you don't get hello expected results.</span></span>

4. <span data-ttu-id="6ffb4-449">使用下列命令 tooapply hello 網路安全性群組 tooa 子網路的 hello。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-449">Use hello following command tooapply hello network security group tooa subnet.</span></span> <span data-ttu-id="6ffb4-450">取代 hello __GUID__和__RESOURCEGROUPNAME__ hello 上一個步驟傳回以 hello 的值。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-450">Replace hello __GUID__ and __RESOURCEGROUPNAME__ values with hello ones returned from hello previous step.</span></span> <span data-ttu-id="6ffb4-451">取代__VNETNAME__和__SUBNETNAME__ hello 虛擬網路名稱與您想要 toocreate 的子網路名稱。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-451">Replace __VNETNAME__ and __SUBNETNAME__ with hello virtual network name and subnet name that you want toocreate.</span></span>

    ```azurecli
    az network vnet subnet update -g RESOURCEGROUPNAME --vnet-name VNETNAME --name SUBNETNAME --set networkSecurityGroup.id="/subscriptions/GUID/resourceGroups/RESOURCEGROUPNAME/providers/Microsoft.Network/networkSecurityGroups/hdisecure"
    ```

    <span data-ttu-id="6ffb4-452">此命令完成之後，您可以安裝 HDInsight 中 hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-452">Once this command completes, you can install HDInsight into hello Virtual Network.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6ffb4-453">這些步驟只會開啟存取 toohello HDInsight 健全狀況和管理服務上 hello Azure 雲端。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-453">These steps only open access toohello HDInsight health and management service on hello Azure cloud.</span></span> <span data-ttu-id="6ffb4-454">任何其他存取 toohello HDInsight 叢集從外部 hello 虛擬網路會被封鎖。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-454">Any other access toohello HDInsight cluster from outside hello Virtual Network is blocked.</span></span> <span data-ttu-id="6ffb4-455">tooenable 存取外部 hello 虛擬網路，您必須加入額外的網路安全性群組規則。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-455">tooenable access from outside hello virtual network, you must add additional Network Security Group rules.</span></span>
>
> <span data-ttu-id="6ffb4-456">hello 下列範例將示範如何從 hello 網際網路存取 tooenable SSH:</span><span class="sxs-lookup"><span data-stu-id="6ffb4-456">hello following example demonstrates how tooenable SSH access from hello Internet:</span></span>
>
> ```azurecli
> az network nsg rule create -g RESOURCEGROUPNAME --nsg-name hdisecure -n hdirule5 --protocol "*" --source-port-range "*" --destination-port-range "22" --source-address-prefix "*" --destination-address-prefix "VirtualNetwork" --access "Allow" --priority 306 --direction "Inbound"
> ```

## <span data-ttu-id="6ffb4-457"><a id="example-dns"></a> 範例：DNS 設定</span><span class="sxs-lookup"><span data-stu-id="6ffb4-457"><a id="example-dns"></a> Example: DNS configuration</span></span>

### <a name="name-resolution-between-a-virtual-network-and-a-connected-on-premises-network"></a><span data-ttu-id="6ffb4-458">虛擬網路與已連線內部部署網路之間的名稱解析</span><span class="sxs-lookup"><span data-stu-id="6ffb4-458">Name resolution between a virtual network and a connected on-premises network</span></span>

<span data-ttu-id="6ffb4-459">這個範例會進行下列假設 hello:</span><span class="sxs-lookup"><span data-stu-id="6ffb4-459">This example makes hello following assumptions:</span></span>

* <span data-ttu-id="6ffb4-460">您有 Azure 虛擬網路所使用的 VPN 閘道連線的 tooan 在內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-460">You have an Azure Virtual Network that is connected tooan on-premises network using a VPN gateway.</span></span>

* <span data-ttu-id="6ffb4-461">hello 自訂 DNS 伺服器 hello 虛擬網路中的執行的 Linux 或 Unix hello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-461">hello custom DNS server in hello virtual network is running Linux or Unix as hello operating system.</span></span>

* <span data-ttu-id="6ffb4-462">[繫結](https://www.isc.org/downloads/bind/)hello 自訂 DNS 伺服器上已安裝。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-462">[Bind](https://www.isc.org/downloads/bind/) is installed on hello custom DNS server.</span></span>

<span data-ttu-id="6ffb4-463">Hello 自訂 DNS 伺服器上 hello 虛擬網路中：</span><span class="sxs-lookup"><span data-stu-id="6ffb4-463">On hello custom DNS server in hello virtual network:</span></span>

1. <span data-ttu-id="6ffb4-464">使用 Azure PowerShell 或 Azure CLI toofind hello 的 DNS 尾碼 hello 虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="6ffb4-464">Use either Azure PowerShell or Azure CLI toofind hello DNS suffix of hello virtual network:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="6ffb4-465">Hello 自訂 DNS 伺服器上 hello 虛擬網路，使用下列文字，做為 hello 內容的 hello hello`/etc/bind/named.conf.local`檔案：</span><span class="sxs-lookup"><span data-stu-id="6ffb4-465">On hello custom DNS server for hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.local` file:</span></span>

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {168.63.129.16;}; # Azure recursive resolver
    };
    ```

    <span data-ttu-id="6ffb4-466">取代 hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` hello 的虛擬網路的 DNS 尾碼的值。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-466">Replace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with hello DNS suffix of your virtual network.</span></span>

    <span data-ttu-id="6ffb4-467">此設定會路由傳送 hello hello 虛擬網路 toohello Azure 遞迴解析程式的 DNS 尾碼的所有 DNS 要求。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-467">This configuration routes all DNS requests for hello DNS suffix of hello virtual network toohello Azure recursive resolver.</span></span>

2. <span data-ttu-id="6ffb4-468">Hello 自訂 DNS 伺服器上 hello 虛擬網路，使用下列文字，做為 hello 內容的 hello hello`/etc/bind/named.conf.options`檔案：</span><span class="sxs-lookup"><span data-stu-id="6ffb4-468">On hello custom DNS server for hello virtual network, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients tooaccept requests from
    // TODO: Add hello IP range of hello joined network toothis list
    acl goodclients {
        10.0.0.0/16; # IP address range of hello virtual network
        localhost;
        localnets;
    };

    options {
            directory "/var/cache/bind";

            recursion yes;

            allow-query { goodclients; };

            # All other requests are sent toohello following
            forwarders {
                192.168.0.1; # Replace with hello IP address of your on-premises DNS server
            };

            dnssec-validation auto;

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="6ffb4-469">取代 hello `10.0.0.0/16` hello IP 位址範圍，為您的虛擬網路的值。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-469">Replace hello `10.0.0.0/16` value with hello IP address range of your virtual network.</span></span> <span data-ttu-id="6ffb4-470">此項目允許來自此範圍內位址的名稱解析要求。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-470">This entry allows name resolution requests addresses within this range.</span></span>

    * <span data-ttu-id="6ffb4-471">新增 hello IP 位址範圍的 hello 在內部部署網路 toohello `acl goodclients { ... }` > 一節。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-471">Add hello IP address range of hello on-premises network toohello `acl goodclients { ... }` section.</span></span>  <span data-ttu-id="6ffb4-472">項目允許 hello 與內部網路中的名稱解析要求的資源。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-472">entry allows name resolution requests from resources in hello on-premises network.</span></span>
    
    * <span data-ttu-id="6ffb4-473">取代 hello 值`192.168.0.1`hello 在內部部署 DNS 伺服器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-473">Replace hello value `192.168.0.1` with hello IP address of your on-premises DNS server.</span></span> <span data-ttu-id="6ffb4-474">此項目會路由傳送所有其他 DNS 要求 toohello 在內部部署 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-474">This entry routes all other DNS requests toohello on-premises DNS server.</span></span>

3. <span data-ttu-id="6ffb4-475">toouse hello 組態，重新啟動繫結。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-475">toouse hello configuration, restart Bind.</span></span> <span data-ttu-id="6ffb4-476">例如： `sudo service bind9 restart`。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-476">For example, `sudo service bind9 restart`.</span></span>

4. <span data-ttu-id="6ffb4-477">加入條件式轉寄站 toohello 在內部部署 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-477">Add a conditional forwarder toohello on-premises DNS server.</span></span> <span data-ttu-id="6ffb4-478">Hello 條件轉寄站 toosend 要求設定為從步驟 1 toohello 自訂 DNS 伺服器 hello DNS 尾碼。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-478">Configure hello conditional forwarder toosend requests for hello DNS suffix from step 1 toohello custom DNS server.</span></span>

    > [!NOTE]
    > <span data-ttu-id="6ffb4-479">請參閱您的 DNS 軟體，如需有關的特定資訊 hello 文件 tooadd 條件轉寄站。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-479">Consult hello documentation for your DNS software for specifics on how tooadd a conditional forwarder.</span></span>

<span data-ttu-id="6ffb4-480">完成這些步驟之後，您可以連接 tooresources 使用完整的網域名稱 (FQDN) 是網路中。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-480">After completing these steps, you can connect tooresources in either network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="6ffb4-481">您現在可以安裝 HDInsight 在 hello 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-481">You can now install HDInsight into hello virtual network.</span></span>

### <a name="name-resolution-between-two-connected-virtual-networks"></a><span data-ttu-id="6ffb4-482">兩個已連線虛擬網路之間的名稱解析</span><span class="sxs-lookup"><span data-stu-id="6ffb4-482">Name resolution between two connected virtual networks</span></span>

<span data-ttu-id="6ffb4-483">這個範例會進行下列假設 hello:</span><span class="sxs-lookup"><span data-stu-id="6ffb4-483">This example makes hello following assumptions:</span></span>

* <span data-ttu-id="6ffb4-484">您的兩個 Azure 虛擬網路是使用 VPN 閘道或對等進行連線。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-484">You have two Azure Virtual Networks that are connected using either a VPN gateway or peering.</span></span>

* <span data-ttu-id="6ffb4-485">在兩個網路 hello 自訂 DNS 伺服器正在執行 Linux 或 Unix 做為 hello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-485">hello custom DNS server in both networks is running Linux or Unix as hello operating system.</span></span>

* <span data-ttu-id="6ffb4-486">[繫結](https://www.isc.org/downloads/bind/)hello 自訂 DNS 伺服器上安裝。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-486">[Bind](https://www.isc.org/downloads/bind/) is installed on hello custom DNS servers.</span></span>

1. <span data-ttu-id="6ffb4-487">使用 Azure PowerShell 或 Azure CLI toofind hello DNS 尾碼的這兩個虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="6ffb4-487">Use either Azure PowerShell or Azure CLI toofind hello DNS suffix of both virtual networks:</span></span>

    ```powershell
    $resourceGroupName = Read-Input -Prompt "Enter hello resource group that contains hello virtual network used with HDInsight"
    $NICs = Get-AzureRmNetworkInterface -ResourceGroupName $resourceGroupName
    $NICs[0].DnsSettings.InternalDomainNameSuffix
    ```

    ```azurecli-interactive
    read -p "Enter hello name of hello resource group that contains hello virtual network: " RESOURCEGROUP
    az network nic list --resource-group $RESOURCEGROUP --query "[0].dnsSettings.internalDomainNameSuffix"
    ```

2. <span data-ttu-id="6ffb4-488">使用 hello 文字之後做為 hello 內容的 hello `/etc/bind/named.config.local` hello 自訂 DNS 伺服器上的檔案。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-488">Use hello following text as hello contents of hello `/etc/bind/named.config.local` file on hello custom DNS server.</span></span> <span data-ttu-id="6ffb4-489">這兩個虛擬網路中 hello 自訂 DNS 伺服器上進行這項變更。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-489">Make this change on hello custom DNS server in both virtual networks.</span></span>

    ```
    // Forward requests for hello virtual network suffix tooAzure recursive resolver
    zone "0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net" {
        type forward;
        forwarders {10.0.0.4;}; # hello IP address of hello DNS server in hello other virtual network
    };
    ```

    <span data-ttu-id="6ffb4-490">取代 hello`0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net`值且 hello DNS 尾碼為 hello__其他__虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-490">Replace hello `0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net` value with hello DNS suffix of hello __other__ virtual network.</span></span> <span data-ttu-id="6ffb4-491">此項目會將要求 hello 遠端網路 toohello hello DNS 尾碼的路由網路中的自訂 DNS。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-491">This entry routes requests for hello DNS suffix of hello remote network toohello custom DNS in that network.</span></span>

3. <span data-ttu-id="6ffb4-492">Hello 自訂 DNS 伺服器上在兩個虛擬網路，使用下列文字，做為 hello 內容的 hello hello`/etc/bind/named.conf.options`檔案：</span><span class="sxs-lookup"><span data-stu-id="6ffb4-492">On hello custom DNS servers in both virtual networks, use hello following text as hello contents of hello `/etc/bind/named.conf.options` file:</span></span>

    ```
    // Clients tooaccept requests from
    acl goodclients {
        10.1.0.0/16; # hello IP address range of one virtual network
        10.0.0.0/16; # hello IP address range of hello other virtual network
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

            auth-nxdomain no;    # conform tooRFC1035
            listen-on { any; };
    };
    ```
    
    * <span data-ttu-id="6ffb4-493">取代 hello`10.0.0.0/16`和`10.1.0.0/16`值與 hello IP 位址的虛擬網路的範圍。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-493">Replace hello `10.0.0.0/16` and `10.1.0.0/16` values with hello IP address ranges of your virtual networks.</span></span> <span data-ttu-id="6ffb4-494">此項目可讓每個網路中的資源 toomake hello DNS 伺服器的要求。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-494">This entry allows resources in each network toomake requests of hello DNS servers.</span></span>

    <span data-ttu-id="6ffb4-495">Hello Azure 遞迴解析程式會處理 hello hello 虛擬網路 (例如，microsoft.com) 的 DNS 尾碼不是任何要求。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-495">Any requests that are not for hello DNS suffixes of hello virtual networks (for example, microsoft.com) is handled by hello Azure recursive resolver.</span></span>

4. <span data-ttu-id="6ffb4-496">toouse hello 組態，重新啟動繫結。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-496">toouse hello configuration, restart Bind.</span></span> <span data-ttu-id="6ffb4-497">例如，兩部 DNS 伺服器上的 `sudo service bind9 restart`。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-497">For example, `sudo service bind9 restart` on both DNS servers.</span></span>

<span data-ttu-id="6ffb4-498">完成這些步驟之後，您可以連接 tooresources hello 使用完整的網域名稱 (FQDN) 的虛擬網路中。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-498">After completing these steps, you can connect tooresources in hello virtual network using fully qualified domain names (FQDN).</span></span> <span data-ttu-id="6ffb4-499">您現在可以安裝 HDInsight 在 hello 的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-499">You can now install HDInsight into hello virtual network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ffb4-500">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6ffb4-500">Next steps</span></span>

* <span data-ttu-id="6ffb4-501">設定 HDInsight tooconnect tooan 在內部部署網路的端對端範例，請參閱[連接 HDInsight tooan 在內部部署網路](./connect-on-premises-network.md)。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-501">For an end-to-end example of configuring HDInsight tooconnect tooan on-premises network, see [Connect HDInsight tooan on-premises network](./connect-on-premises-network.md).</span></span>

* <span data-ttu-id="6ffb4-502">如需有關 Azure 虛擬網路的詳細資訊，請參閱 hello [Azure 虛擬網路概觀](../virtual-network/virtual-networks-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-502">For more information on Azure virtual networks, see hello [Azure Virtual Network overview](../virtual-network/virtual-networks-overview.md).</span></span>

* <span data-ttu-id="6ffb4-503">如需網路安全性群組的詳細資訊，請參閱[網路安全性群組](../virtual-network/virtual-networks-nsg.md)。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-503">For more information on network security groups, see [Network security groups](../virtual-network/virtual-networks-nsg.md).</span></span>

* <span data-ttu-id="6ffb4-504">如需使用者定義路由的詳細資訊，請參閱[使用者定義路由和 IP 轉送](../virtual-network/virtual-networks-udr-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6ffb4-504">For more information on user-defined routes, see [USer-defined routes and IP forwarding](../virtual-network/virtual-networks-udr-overview.md).</span></span>