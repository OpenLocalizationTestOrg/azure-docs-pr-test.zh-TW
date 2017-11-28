---
title: "建立 VNet 之間的連線：傳統：Azure 入口網站 | Microsoft Docs"
description: "如何 tooconnect Azure 虛擬網路一起使用 PowerShell 和 hello Azure 傳統入口網站。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: f29c3c091d049ff96cf59f4c28ab86a100bcb5fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-connection-classic"></a><span data-ttu-id="2440b-103">設定 VNet 對 VNet 連線 (傳統)</span><span class="sxs-lookup"><span data-stu-id="2440b-103">Configure a VNet-to-VNet connection (classic)</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

<span data-ttu-id="2440b-104">本文章將示範如何 toocreate 虛擬網路之間的 VPN 閘道連線。</span><span class="sxs-lookup"><span data-stu-id="2440b-104">This article shows you how toocreate a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="2440b-105">hello 虛擬網路可在 hello 相同或不同區域，並從 hello 相同或不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2440b-105">hello virtual networks can be in hello same or different regions, and from hello same or different subscriptions.</span></span> <span data-ttu-id="2440b-106">本文章中的 hello 步驟適用於 toohello 傳統部署模型和 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="2440b-106">hello steps in this article apply toohello classic deployment model and hello Azure portal.</span></span> <span data-ttu-id="2440b-107">您也可以建立此組態使用不同的部署工具或部署模型，從下列清單中的 hello 選取不同的選項：</span><span class="sxs-lookup"><span data-stu-id="2440b-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="2440b-108">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="2440b-108">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="2440b-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2440b-109">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="2440b-110">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2440b-110">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="2440b-111">Azure 入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="2440b-111">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="2440b-112">連線不同的部署模型 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="2440b-112">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="2440b-113">連線不同的部署模型 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="2440b-113">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![VNet tooVNet 連線能力圖表](./media/vpn-gateway-howto-vnet-vnet-portal-classic/v2vclassic.png)

## <a name="about-vnet-to-vnet-connections"></a><span data-ttu-id="2440b-115">關於 VNet 對 VNet 連線</span><span class="sxs-lookup"><span data-stu-id="2440b-115">About VNet-to-VNet connections</span></span>

<span data-ttu-id="2440b-116">在 hello 傳統部署模型中使用的 VPN 閘道連接虛擬網路 tooanother 虛擬網路 (VNet 對 VNet) 是類似 tooconnecting 虛擬網路 tooan 在內部部署站台位置。</span><span class="sxs-lookup"><span data-stu-id="2440b-116">Connecting a virtual network tooanother virtual network (VNet-to-VNet) in hello classic deployment model using a VPN gateway is similar tooconnecting a virtual network tooan on-premises site location.</span></span> <span data-ttu-id="2440b-117">這兩種連線類型使用的 VPN 閘道 tooprovide 採用 IPsec/IKE 的安全通道。</span><span class="sxs-lookup"><span data-stu-id="2440b-117">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span>

<span data-ttu-id="2440b-118">hello 您連接的 Vnet 可位於不同的訂用帳戶和不同的區域。</span><span class="sxs-lookup"><span data-stu-id="2440b-118">hello VNets you connect can be in different subscriptions and different regions.</span></span> <span data-ttu-id="2440b-119">您可以結合 VNet tooVNet 通訊與多網站組態。</span><span class="sxs-lookup"><span data-stu-id="2440b-119">You can combine VNet tooVNet communication with multi-site configurations.</span></span> <span data-ttu-id="2440b-120">這可讓您建立結合了跨單位連線與內部虛擬網路連線的網路拓撲。</span><span class="sxs-lookup"><span data-stu-id="2440b-120">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity.</span></span>

![VNet tooVNet 連線](./media/vpn-gateway-howto-vnet-vnet-portal-classic/aboutconnections.png)

### <span data-ttu-id="2440b-122"><a name="why"></a>為什麼要連線虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="2440b-122"><a name="why"></a>Why connect virtual networks?</span></span>

<span data-ttu-id="2440b-123">您可以遵循原因 hello tooconnect 虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="2440b-123">You may want tooconnect virtual networks for hello following reasons:</span></span>

* <span data-ttu-id="2440b-124">**跨區域的異地備援和異地目前狀態**</span><span class="sxs-lookup"><span data-stu-id="2440b-124">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="2440b-125">您可以使用安全連線設定自己的異地複寫或同步處理，而不用查看網際網路對向端點。</span><span class="sxs-lookup"><span data-stu-id="2440b-125">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="2440b-126">有了 Azure Load Balancer 和 Microsoft 或第三方叢集技術，您便可以利用跨多個 Azure 區域的異地備援，設定具有高可用性的工作負載。</span><span class="sxs-lookup"><span data-stu-id="2440b-126">With Azure Load Balancer and Microsoft or third-party clustering technology, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="2440b-127">重要的一個例子是 tooset 設定 SQL Always On 與分配到多個 Azure 區域的可用性群組。</span><span class="sxs-lookup"><span data-stu-id="2440b-127">One important example is tooset up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="2440b-128">**具有嚴密隔離界限的區域性多層式應用程式**</span><span class="sxs-lookup"><span data-stu-id="2440b-128">**Regional multi-tier applications with strong isolation boundary**</span></span>

  * <span data-ttu-id="2440b-129">在 hello 相同區域中，您可以設定多層應用程式與多個 Vnet 連接以及嚴密隔離和安全層級間通訊。</span><span class="sxs-lookup"><span data-stu-id="2440b-129">Within hello same region, you can set up multi-tier applications with multiple VNets connected together with strong isolation and secure inter-tier communication.</span></span>
* <span data-ttu-id="2440b-130">**Azure 中的跨訂用帳戶、組織間通訊**</span><span class="sxs-lookup"><span data-stu-id="2440b-130">**Cross subscription, inter-organization communication in Azure**</span></span>

  * <span data-ttu-id="2440b-131">如果您有多個 Azure 訂用帳戶，您可以將虛擬網路之間不同訂用帳戶的工作負載安全地連接在一起。</span><span class="sxs-lookup"><span data-stu-id="2440b-131">If you have multiple Azure subscriptions, you can connect workloads from different subscriptions together securely between virtual networks.</span></span>
  * <span data-ttu-id="2440b-132">針對企業或服務提供者，您可以在 Azure 中使用安全 VPN 技術啟用跨組織通訊。</span><span class="sxs-lookup"><span data-stu-id="2440b-132">For enterprises or service providers, you can enable cross-organization communication with secure VPN technology within Azure.</span></span>

<span data-ttu-id="2440b-133">如需 VNet 對 VNet 連線的詳細資訊，請參閱[VNet 對 VNet 考量](#faq)hello 本文結尾處。</span><span class="sxs-lookup"><span data-stu-id="2440b-133">For more information about VNet-to-VNet connections, see [VNet-to-VNet considerations](#faq) at hello end of this article.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="2440b-134">開始之前</span><span class="sxs-lookup"><span data-stu-id="2440b-134">Before you begin</span></span>

<span data-ttu-id="2440b-135">開始這個練習中前, 下載並安裝 hello 的 hello Azure 服務管理 (SM) PowerShell cmdlet 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="2440b-135">Before beginning this exercise, download and install hello latest version of hello Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="2440b-136">如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="2440b-136">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="2440b-137">我們會將大部分的 hello 步驟 hello 入口網站，但您必須使用 PowerShell toocreate hello 連線 hello Vnet 之間。</span><span class="sxs-lookup"><span data-stu-id="2440b-137">We use hello portal for most of hello steps, but you must use PowerShell toocreate hello connections between hello VNets.</span></span> <span data-ttu-id="2440b-138">您無法建立 hello 連線使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="2440b-138">You can't create hello connections using hello Azure portal.</span></span>

## <span data-ttu-id="2440b-139"><a name="plan"></a>步驟 1 - 規劃 IP 位址範圍</span><span class="sxs-lookup"><span data-stu-id="2440b-139"><a name="plan"></a>Step 1 - Plan your IP address ranges</span></span>

<span data-ttu-id="2440b-140">它是您將使用 tooconfigure 您的虛擬網路的重要 toodecide hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="2440b-140">It’s important toodecide hello ranges that you’ll use tooconfigure your virtual networks.</span></span> <span data-ttu-id="2440b-141">此組態中，您必須確定沒有任何 VNet 範圍重疊彼此，或與任何 hello 所連接的區域網路。</span><span class="sxs-lookup"><span data-stu-id="2440b-141">For this configuration, you must make sure that none of your VNet ranges overlap with each other, or with any of hello local networks that they connect to.</span></span>

<span data-ttu-id="2440b-142">hello 下表顯示的範例 toodefine Vnet。</span><span class="sxs-lookup"><span data-stu-id="2440b-142">hello following table shows an example of how toodefine your VNets.</span></span> <span data-ttu-id="2440b-143">使用 hello 範圍僅供參考。</span><span class="sxs-lookup"><span data-stu-id="2440b-143">Use hello ranges as a guideline only.</span></span> <span data-ttu-id="2440b-144">記下您的虛擬網路的 hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="2440b-144">Write down hello ranges for your virtual networks.</span></span> <span data-ttu-id="2440b-145">稍後的步驟將會需要這項資訊。</span><span class="sxs-lookup"><span data-stu-id="2440b-145">You need this information for later steps.</span></span>

<span data-ttu-id="2440b-146">**範例**</span><span class="sxs-lookup"><span data-stu-id="2440b-146">**Example**</span></span>

| <span data-ttu-id="2440b-147">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="2440b-147">Virtual Network</span></span> | <span data-ttu-id="2440b-148">位址空間</span><span class="sxs-lookup"><span data-stu-id="2440b-148">Address Space</span></span> | <span data-ttu-id="2440b-149">區域</span><span class="sxs-lookup"><span data-stu-id="2440b-149">Region</span></span> | <span data-ttu-id="2440b-150">Toolocal 網路站台連線</span><span class="sxs-lookup"><span data-stu-id="2440b-150">Connects toolocal network site</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2440b-151">TestVNet1</span><span class="sxs-lookup"><span data-stu-id="2440b-151">TestVNet1</span></span> |<span data-ttu-id="2440b-152">TestVNet1</span><span class="sxs-lookup"><span data-stu-id="2440b-152">TestVNet1</span></span><br><span data-ttu-id="2440b-153">(10.11.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="2440b-153">(10.11.0.0/16)</span></span><br><span data-ttu-id="2440b-154">(10.12.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="2440b-154">(10.12.0.0/16)</span></span> |<span data-ttu-id="2440b-155">美國東部</span><span class="sxs-lookup"><span data-stu-id="2440b-155">East US</span></span> |<span data-ttu-id="2440b-156">VNet4Local</span><span class="sxs-lookup"><span data-stu-id="2440b-156">VNet4Local</span></span><br><span data-ttu-id="2440b-157">(10.41.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="2440b-157">(10.41.0.0/16)</span></span><br><span data-ttu-id="2440b-158">(10.42.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="2440b-158">(10.42.0.0/16)</span></span> |
| <span data-ttu-id="2440b-159">TestVNet4</span><span class="sxs-lookup"><span data-stu-id="2440b-159">TestVNet4</span></span> |<span data-ttu-id="2440b-160">TestVNet4</span><span class="sxs-lookup"><span data-stu-id="2440b-160">TestVNet4</span></span><br><span data-ttu-id="2440b-161">(10.41.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="2440b-161">(10.41.0.0/16)</span></span><br><span data-ttu-id="2440b-162">(10.42.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="2440b-162">(10.42.0.0/16)</span></span> |<span data-ttu-id="2440b-163">美國西部</span><span class="sxs-lookup"><span data-stu-id="2440b-163">West US</span></span> |<span data-ttu-id="2440b-164">VNet1Local</span><span class="sxs-lookup"><span data-stu-id="2440b-164">VNet1Local</span></span><br><span data-ttu-id="2440b-165">(10.11.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="2440b-165">(10.11.0.0/16)</span></span><br><span data-ttu-id="2440b-166">(10.12.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="2440b-166">(10.12.0.0/16)</span></span> |

## <span data-ttu-id="2440b-167"><a name="vnetvalues"></a>步驟 2-建立虛擬網路，hello</span><span class="sxs-lookup"><span data-stu-id="2440b-167"><a name="vnetvalues"></a>Step 2 - Create hello virtual networks</span></span>

<span data-ttu-id="2440b-168">建立兩個虛擬網路中 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="2440b-168">Create two virtual networks in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2440b-169">Hello 步驟 toocreate 傳統虛擬網路，請參閱[建立傳統的虛擬網路](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="2440b-169">For hello steps toocreate classic virtual networks, see [Create a classic virtual network](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span> 

<span data-ttu-id="2440b-170">當使用 hello 入口 toocreate 傳統的虛擬網路時，您必須使用下列步驟，否則 hello 選項 toocreate 傳統的虛擬網路不會出現的 hello 來巡覽 toohello 虛擬網路 刀鋒視窗：</span><span class="sxs-lookup"><span data-stu-id="2440b-170">When using hello portal toocreate a classic virtual network, you must navigate toohello virtual network blade by using hello following steps, otherwise hello option toocreate a classic virtual network does not appear:</span></span>

1. <span data-ttu-id="2440b-171">按一下 hello '+' tooopen hello 'New' 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2440b-171">Click hello '+' tooopen hello 'New' blade.</span></span>
2. <span data-ttu-id="2440b-172">Hello '搜尋 hello marketplace' 欄位中，輸入 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="2440b-172">In hello 'Search hello marketplace' field, type 'Virtual Network'.</span></span> <span data-ttu-id="2440b-173">如果相反地，選取 網路功能-> 虛擬網路，則不會收到 hello 選項 toocreate 傳統的 VNet。</span><span class="sxs-lookup"><span data-stu-id="2440b-173">If you instead, select Networking -> Virtual Network, you will not get hello option toocreate a classic VNet.</span></span>
3. <span data-ttu-id="2440b-174">傳回清單中的 hello 從找出 虛擬網路，然後按一下 tooopen hello 虛擬網路 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2440b-174">Locate 'Virtual Network' from hello returned list and click it tooopen hello Virtual Network blade.</span></span> 
4. <span data-ttu-id="2440b-175">Hello 虛擬網路] 刀鋒視窗中，選取 [傳統' toocreate 傳統的 VNet。</span><span class="sxs-lookup"><span data-stu-id="2440b-175">On hello virtual network blade, select 'Classic' toocreate a classic VNet.</span></span> 

<span data-ttu-id="2440b-176">如果您使用這份文件做為練習，您可以使用下列範例值 hello:</span><span class="sxs-lookup"><span data-stu-id="2440b-176">If you are using this article as an exercise, you can use hello following example values:</span></span>

<span data-ttu-id="2440b-177">**TestVNet1 的值**</span><span class="sxs-lookup"><span data-stu-id="2440b-177">**Values for TestVNet1**</span></span>

<span data-ttu-id="2440b-178">名稱︰TestVNet1</span><span class="sxs-lookup"><span data-stu-id="2440b-178">Name: TestVNet1</span></span><br>
<span data-ttu-id="2440b-179">位址空間︰10.11.0.0/16、10.12.0.0/16 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="2440b-179">Address space: 10.11.0.0/16, 10.12.0.0/16 (optional)</span></span><br>
<span data-ttu-id="2440b-180">子網路名稱：default</span><span class="sxs-lookup"><span data-stu-id="2440b-180">Subnet name: default</span></span><br>
<span data-ttu-id="2440b-181">子網路位址範圍：10.11.0.1/24</span><span class="sxs-lookup"><span data-stu-id="2440b-181">Subnet address range: 10.11.0.1/24</span></span><br>
<span data-ttu-id="2440b-182">資源群組：ClassicRG</span><span class="sxs-lookup"><span data-stu-id="2440b-182">Resource group: ClassicRG</span></span><br>
<span data-ttu-id="2440b-183">位置：美國東部</span><span class="sxs-lookup"><span data-stu-id="2440b-183">Location: East US</span></span><br>
<span data-ttu-id="2440b-184">GatewaySubnet：10.11.1.0/27</span><span class="sxs-lookup"><span data-stu-id="2440b-184">GatewaySubnet: 10.11.1.0/27</span></span>

<span data-ttu-id="2440b-185">**TestVNet4 的值**</span><span class="sxs-lookup"><span data-stu-id="2440b-185">**Values for TestVNet4**</span></span>

<span data-ttu-id="2440b-186">名稱︰TestVNet4</span><span class="sxs-lookup"><span data-stu-id="2440b-186">Name: TestVNet4</span></span><br>
<span data-ttu-id="2440b-187">位址空間︰10.41.0.0/16、10.42.0.0/16 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="2440b-187">Address space: 10.41.0.0/16, 10.42.0.0/16 (optional)</span></span><br>
<span data-ttu-id="2440b-188">子網路名稱：default</span><span class="sxs-lookup"><span data-stu-id="2440b-188">Subnet name: default</span></span><br>
<span data-ttu-id="2440b-189">子網路位址範圍：10.41.0.1/24</span><span class="sxs-lookup"><span data-stu-id="2440b-189">Subnet address range: 10.41.0.1/24</span></span><br>
<span data-ttu-id="2440b-190">資源群組：ClassicRG</span><span class="sxs-lookup"><span data-stu-id="2440b-190">Resource group: ClassicRG</span></span><br>
<span data-ttu-id="2440b-191">位置：美國西部</span><span class="sxs-lookup"><span data-stu-id="2440b-191">Location: West US</span></span><br>
<span data-ttu-id="2440b-192">GatewaySubnet：10.41.1.0/27</span><span class="sxs-lookup"><span data-stu-id="2440b-192">GatewaySubnet: 10.41.1.0/27</span></span>

<span data-ttu-id="2440b-193">**在建立 Vnet 時，請記得 hello 下列設定：**</span><span class="sxs-lookup"><span data-stu-id="2440b-193">**When creating your VNets, keep in mind hello following settings:**</span></span>

* <span data-ttu-id="2440b-194">**虛擬網路位址空間**– 在 hello 虛擬網路位址空間頁面上，指定您想 toouse，虛擬網路的 hello 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="2440b-194">**Virtual Network Address Spaces** – On hello Virtual Network Address Spaces page, specify hello address range that you want toouse for your virtual network.</span></span> <span data-ttu-id="2440b-195">這些是 hello 動態 IP 位址將指派 toohello Vm，而您將部署 toothis 虛擬網路的其他角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="2440b-195">These are hello dynamic IP addresses that will be assigned toohello VMs and other role instances that you deploy toothis virtual network.</span></span><br><span data-ttu-id="2440b-196">您選取的空間不能與 hello 位址空間重疊任何 hello 位址 hello 此 VNet 將會連接到其他 Vnet 或內部部署位置。</span><span class="sxs-lookup"><span data-stu-id="2440b-196">hello address spaces you select cannot overlap with hello address spaces for any of hello other VNets or on-premises locations that this VNet will connect to.</span></span>

* <span data-ttu-id="2440b-197">**位置** – 當您建立虛擬網路時，您會將該位置與 Azure 位置 (區域) 產生關聯。</span><span class="sxs-lookup"><span data-stu-id="2440b-197">**Location** – When you create a virtual network, you associate it with an Azure location (region).</span></span> <span data-ttu-id="2440b-198">例如，如果您想為您 Vm 部署實體上位於美國西部 tooyour 虛擬網路 toobe，選取該位置。</span><span class="sxs-lookup"><span data-stu-id="2440b-198">For example, if you want your VMs that are deployed tooyour virtual network toobe physically located in West US, select that location.</span></span> <span data-ttu-id="2440b-199">您無法變更您在建立之後，您的虛擬網路與相關聯的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="2440b-199">You can’t change hello location associated with your virtual network after you create it.</span></span>

<span data-ttu-id="2440b-200">**建立 Vnet 之後, 您可以新增下列設定的 hello:**</span><span class="sxs-lookup"><span data-stu-id="2440b-200">**After creating your VNets, you can add hello following settings:**</span></span>

* <span data-ttu-id="2440b-201">**位址空間**– 其他位址空間不需要此設定，但您可以建立 hello VNet 之後加入其他位址空間。</span><span class="sxs-lookup"><span data-stu-id="2440b-201">**Address space** – Additional address space is not required for this configuration, but you can add additional address space after creating hello VNet.</span></span>

* <span data-ttu-id="2440b-202">**子網路**– 不需要針對此設定，其他子網路，但是您可能想 toohave 中與其他角色執行個體位於不同子網路的 Vm。</span><span class="sxs-lookup"><span data-stu-id="2440b-202">**Subnets** – Additional subnets are not required for this configuration, but you might want toohave your VMs in a subnet that is separate from your other role instances.</span></span>

* <span data-ttu-id="2440b-203">**DNS 伺服器**– 輸入 hello DNS 伺服器名稱和 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2440b-203">**DNS servers** – Enter hello DNS server name and IP address.</span></span> <span data-ttu-id="2440b-204">此設定不會建立 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="2440b-204">This setting does not create a DNS server.</span></span> <span data-ttu-id="2440b-205">它可讓您為此虛擬網路的名稱解析需 toouse toospecify hello DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="2440b-205">It allows you toospecify hello DNS servers that you want toouse for name resolution for this virtual network.</span></span>

<span data-ttu-id="2440b-206">在本節中，您可以設定 hello 連接類型，hello 本機站台，並建立 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="2440b-206">In this section, you configure hello connection type, hello local site, and create hello gateway.</span></span>

## <span data-ttu-id="2440b-207"><a name="localsite"></a>步驟 3-設定 hello 本機站台</span><span class="sxs-lookup"><span data-stu-id="2440b-207"><a name="localsite"></a>Step 3 - Configure hello local site</span></span>

<span data-ttu-id="2440b-208">Azure 會使用 hello 中指定的設定每個區域網路網站 toodetermine tooroute hello Vnet 之間的流量。</span><span class="sxs-lookup"><span data-stu-id="2440b-208">Azure uses hello settings specified in each local network site toodetermine how tooroute traffic between hello VNets.</span></span> <span data-ttu-id="2440b-209">每個 VNet 必須指向 toohello 個別區域網路，您想讓 tooroute 流量。</span><span class="sxs-lookup"><span data-stu-id="2440b-209">Each VNet must point toohello respective local network that you want tooroute traffic to.</span></span> <span data-ttu-id="2440b-210">您決定要 toouse toorefer tooeach 區域網路網站的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="2440b-210">You determine hello name you want toouse toorefer tooeach local network site.</span></span> <span data-ttu-id="2440b-211">它是最佳 toouse 描述性項目。</span><span class="sxs-lookup"><span data-stu-id="2440b-211">It's best toouse something descriptive.</span></span>

<span data-ttu-id="2440b-212">比方說，TestVNet1 tooa 區域網路的站台連線，您建立名為 'VNet4Local'。</span><span class="sxs-lookup"><span data-stu-id="2440b-212">For example, TestVNet1 connects tooa local network site that you create named 'VNet4Local'.</span></span> <span data-ttu-id="2440b-213">VNet4Local hello 設定包含 TestVNet4 hello 位址前置詞。</span><span class="sxs-lookup"><span data-stu-id="2440b-213">hello settings for VNet4Local contain hello address prefixes for TestVNet4.</span></span>

<span data-ttu-id="2440b-214">hello 本機站台的每個 VNet 是 hello 另一個 VNet。</span><span class="sxs-lookup"><span data-stu-id="2440b-214">hello local site for each VNet is hello other VNet.</span></span> <span data-ttu-id="2440b-215">下列範例值 hello 適用於我們的設定：</span><span class="sxs-lookup"><span data-stu-id="2440b-215">hello following example values are used for our configuration:</span></span>

| <span data-ttu-id="2440b-216">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="2440b-216">Virtual Network</span></span> | <span data-ttu-id="2440b-217">位址空間</span><span class="sxs-lookup"><span data-stu-id="2440b-217">Address Space</span></span> | <span data-ttu-id="2440b-218">區域</span><span class="sxs-lookup"><span data-stu-id="2440b-218">Region</span></span> | <span data-ttu-id="2440b-219">Toolocal 網路站台連線</span><span class="sxs-lookup"><span data-stu-id="2440b-219">Connects toolocal network site</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="2440b-220">TestVNet1</span><span class="sxs-lookup"><span data-stu-id="2440b-220">TestVNet1</span></span> |<span data-ttu-id="2440b-221">TestVNet1</span><span class="sxs-lookup"><span data-stu-id="2440b-221">TestVNet1</span></span><br><span data-ttu-id="2440b-222">(10.11.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="2440b-222">(10.11.0.0/16)</span></span><br><span data-ttu-id="2440b-223">(10.12.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="2440b-223">(10.12.0.0/16)</span></span> |<span data-ttu-id="2440b-224">美國東部</span><span class="sxs-lookup"><span data-stu-id="2440b-224">East US</span></span> |<span data-ttu-id="2440b-225">VNet4Local</span><span class="sxs-lookup"><span data-stu-id="2440b-225">VNet4Local</span></span><br><span data-ttu-id="2440b-226">(10.41.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="2440b-226">(10.41.0.0/16)</span></span><br><span data-ttu-id="2440b-227">(10.42.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="2440b-227">(10.42.0.0/16)</span></span> |
| <span data-ttu-id="2440b-228">TestVNet4</span><span class="sxs-lookup"><span data-stu-id="2440b-228">TestVNet4</span></span> |<span data-ttu-id="2440b-229">TestVNet4</span><span class="sxs-lookup"><span data-stu-id="2440b-229">TestVNet4</span></span><br><span data-ttu-id="2440b-230">(10.41.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="2440b-230">(10.41.0.0/16)</span></span><br><span data-ttu-id="2440b-231">(10.42.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="2440b-231">(10.42.0.0/16)</span></span> |<span data-ttu-id="2440b-232">美國西部</span><span class="sxs-lookup"><span data-stu-id="2440b-232">West US</span></span> |<span data-ttu-id="2440b-233">VNet1Local</span><span class="sxs-lookup"><span data-stu-id="2440b-233">VNet1Local</span></span><br><span data-ttu-id="2440b-234">(10.11.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="2440b-234">(10.11.0.0/16)</span></span><br><span data-ttu-id="2440b-235">(10.12.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="2440b-235">(10.12.0.0/16)</span></span> |

1. <span data-ttu-id="2440b-236">尋找 TestVNet1 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="2440b-236">Locate TestVNet1 in hello Azure portal.</span></span> <span data-ttu-id="2440b-237">在 hello **VPN 連線**> 一節的 hello 刀鋒視窗中，按一下 **閘道**。</span><span class="sxs-lookup"><span data-stu-id="2440b-237">In hello **VPN connections** section of hello blade, click **Gateway**.</span></span>

    ![沒有閘道](./media/vpn-gateway-howto-vnet-vnet-portal-classic/nogateway.png)
2. <span data-ttu-id="2440b-239">在 hello**新的 VPN 連線**頁面上，選取**站對站**。</span><span class="sxs-lookup"><span data-stu-id="2440b-239">On hello **New VPN Connection** page, select **Site-to-Site**.</span></span>
3. <span data-ttu-id="2440b-240">按一下**本機站台**tooopen hello 本機站台頁面並 hello 的設定。</span><span class="sxs-lookup"><span data-stu-id="2440b-240">Click **Local site** tooopen hello Local site page and configure hello settings.</span></span>
4. <span data-ttu-id="2440b-241">在 hello**本機站台**頁面上，您的本機站台的名稱。</span><span class="sxs-lookup"><span data-stu-id="2440b-241">On hello **Local site** page, name your local site.</span></span> <span data-ttu-id="2440b-242">在本例中，我們命名 hello 本機站台 'VNet4Local'。</span><span class="sxs-lookup"><span data-stu-id="2440b-242">In our example, we name hello local site 'VNet4Local'.</span></span>
5. <span data-ttu-id="2440b-243">針對 [VPN 閘道 IP 位址]，只要是有效的格式，您可以使用您想要的任何 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2440b-243">For **VPN gateway IP address**, you can use any IP address that you want, as long as it's in a valid format.</span></span> <span data-ttu-id="2440b-244">一般而言，您會使用 VPN 裝置 hello 實際外部 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2440b-244">Typically, you’d use hello actual external IP address for a VPN device.</span></span> <span data-ttu-id="2440b-245">但是，傳統的 VNet 對 VNet 組態，您可以使用 hello 公用 IP 位址指派給您的 VNet toohello 閘道。</span><span class="sxs-lookup"><span data-stu-id="2440b-245">But, for a classic VNet-to-VNet configuration, you use hello public IP address that is assigned toohello gateway for your VNet.</span></span> <span data-ttu-id="2440b-246">假設您已尚未建立 hello 虛擬網路閘道，您可以指定任何有效的公用 IP 位址做為預留位置。</span><span class="sxs-lookup"><span data-stu-id="2440b-246">Given that you’ve not yet created hello virtual network gateway, you specify any valid public IP address as a placeholder.</span></span><br><span data-ttu-id="2440b-247">請勿將此欄位留白 - 這不是此組態的選擇性欄位。</span><span class="sxs-lookup"><span data-stu-id="2440b-247">Don't leave this blank - it's not optional for this configuration.</span></span> <span data-ttu-id="2440b-248">在稍後步驟中，您會返回這些設定，並設定它們與 hello 對應虛擬網路閘道的 IP 位址，Azure 會產生它之後。</span><span class="sxs-lookup"><span data-stu-id="2440b-248">In a later step, you go back into these settings and configure them with hello corresponding virtual network gateway IP addresses once Azure generates it.</span></span>
6. <span data-ttu-id="2440b-249">如**用戶端的位址空間**，使用另一個 VNet hello hello 位址空間。</span><span class="sxs-lookup"><span data-stu-id="2440b-249">For **Client Address Space**, use hello address space of hello other VNet.</span></span> <span data-ttu-id="2440b-250">Tooyour 規劃範例，請參閱。</span><span class="sxs-lookup"><span data-stu-id="2440b-250">Refer tooyour planning example.</span></span> <span data-ttu-id="2440b-251">按一下**確定**toosave 您的設定和傳回後 toohello**新的 VPN 連線**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2440b-251">Click **OK** toosave your settings and return back toohello **New VPN Connection** blade.</span></span>

    ![本機網站](./media/vpn-gateway-howto-vnet-vnet-portal-classic/localsite.png)

## <span data-ttu-id="2440b-253"><a name="gw"></a>步驟 4-建立 hello 虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="2440b-253"><a name="gw"></a>Step 4 - Create hello virtual network gateway</span></span>

<span data-ttu-id="2440b-254">每個虛擬網路都必須有虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="2440b-254">Each virtual network must have a virtual network gateway.</span></span> <span data-ttu-id="2440b-255">hello 虛擬網路閘道路由，並加密流量。</span><span class="sxs-lookup"><span data-stu-id="2440b-255">hello virtual network gateway routes and encrypts traffic.</span></span>

1. <span data-ttu-id="2440b-256">在 hello**新的 VPN 連線**刀鋒視窗中，選取 hello 核取方塊**立即建立閘道**。</span><span class="sxs-lookup"><span data-stu-id="2440b-256">On hello **New VPN Connection** blade, select hello checkbox **Create gateway immediately**.</span></span>
2. <span data-ttu-id="2440b-257">按一下 [子網路、大小和路由類型]。</span><span class="sxs-lookup"><span data-stu-id="2440b-257">Click **Subnet, size and routing type**.</span></span> <span data-ttu-id="2440b-258">在 hello**閘道組態**刀鋒視窗中，按一下 **子網路**。</span><span class="sxs-lookup"><span data-stu-id="2440b-258">On hello **Gateway configuration** blade, click **Subnet**.</span></span>
3. <span data-ttu-id="2440b-259">與 hello 需要名稱為 'GatewaySubnet'，就會自動填入 hello 閘道子網路名稱。</span><span class="sxs-lookup"><span data-stu-id="2440b-259">hello gateway subnet name is filled in automatically with hello required name 'GatewaySubnet'.</span></span> <span data-ttu-id="2440b-260">hello**位址範圍**包含 hello 配置 toohello VPN 閘道服務的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2440b-260">hello **Address range** contains hello IP addresses that are allocated toohello VPN gateway services.</span></span> <span data-ttu-id="2440b-261">某些設定可讓閘道子網路/29，但它的最佳 toouse/28 或 /27 tooaccommodate 未來組態可能需要多個 IP 位址的 hello 閘道服務。</span><span class="sxs-lookup"><span data-stu-id="2440b-261">Some configurations allow a gateway subnet of /29, but it's best toouse a /28 or /27 tooaccommodate future configurations that may require more IP addresses for hello gateway services.</span></span> <span data-ttu-id="2440b-262">在我們的範例設定中，我們會使用 10.11.1.0/27。</span><span class="sxs-lookup"><span data-stu-id="2440b-262">In our example settings, we use 10.11.1.0/27.</span></span> <span data-ttu-id="2440b-263">調整 hello 位址空間，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="2440b-263">Adjust hello address space, then click **OK**.</span></span>
4. <span data-ttu-id="2440b-264">設定 hello**閘道大小**。</span><span class="sxs-lookup"><span data-stu-id="2440b-264">Configure hello **Gateway Size**.</span></span> <span data-ttu-id="2440b-265">此設定表示 toohello[閘道 SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku)。</span><span class="sxs-lookup"><span data-stu-id="2440b-265">This setting refers toohello [Gateway SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>
5. <span data-ttu-id="2440b-266">設定 hello**路由類型**。</span><span class="sxs-lookup"><span data-stu-id="2440b-266">Configure hello **Routing Type**.</span></span> <span data-ttu-id="2440b-267">hello 路由類型，此設定必須是**動態**。</span><span class="sxs-lookup"><span data-stu-id="2440b-267">hello routing type for this configuration must be **Dynamic**.</span></span> <span data-ttu-id="2440b-268">除非您終止 hello 閘道，並建立新的連線，您無法稍後變更 hello 路由類型。</span><span class="sxs-lookup"><span data-stu-id="2440b-268">You can't change hello routing type later unless you tear down hello gateway and create a new one.</span></span>
6. <span data-ttu-id="2440b-269">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="2440b-269">Click **OK**.</span></span>
7. <span data-ttu-id="2440b-270">在 hello**新的 VPN 連線**刀鋒視窗中，按一下**確定**toobegin 建立 hello 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="2440b-270">On hello **New VPN Connection** blade, click **OK** toobegin creating hello virtual network gateway.</span></span> <span data-ttu-id="2440b-271">建立閘道可以通常要花費 45 分鐘以上，視 hello 選取的閘道 SKU。</span><span class="sxs-lookup"><span data-stu-id="2440b-271">Creating a gateway can often take 45 minutes or more, depending on hello selected gateway SKU.</span></span>

## <span data-ttu-id="2440b-272"><a name="vnet4settings"></a>步驟 5 - 進行 TestVNet4 設定</span><span class="sxs-lookup"><span data-stu-id="2440b-272"><a name="vnet4settings"></a>Step 5 - Configure TestVNet4 settings</span></span>

<span data-ttu-id="2440b-273">重覆步驟 hello[建立本機網站](#localsite)和[建立 hello 虛擬網路閘道](#gw)tooconfigure TestVNet4，替代 hello 值只有在必要時。</span><span class="sxs-lookup"><span data-stu-id="2440b-273">Repeat hello steps too[Create a local site](#localsite) and [Create hello virtual network gateway](#gw) tooconfigure TestVNet4, substituting hello values when necessary.</span></span> <span data-ttu-id="2440b-274">如果您進行練習，請使用 hello[範例值](#vnetvalues)。</span><span class="sxs-lookup"><span data-stu-id="2440b-274">If you are doing this as an exercise, use hello [Example values](#vnetvalues).</span></span>

## <span data-ttu-id="2440b-275"><a name="updatelocal"></a>步驟 6-更新 hello 本機站台</span><span class="sxs-lookup"><span data-stu-id="2440b-275"><a name="updatelocal"></a>Step 6 - Update hello local sites</span></span>

<span data-ttu-id="2440b-276">這兩個 vnet 建立虛擬網路閘道之後，您必須調整 hello 本機站台**VPN 閘道 IP 位址**值。</span><span class="sxs-lookup"><span data-stu-id="2440b-276">After your virtual network gateways have been created for both VNets, you must adjust hello local sites **VPN gateway IP address** values.</span></span>

|<span data-ttu-id="2440b-277">VNet 名稱</span><span class="sxs-lookup"><span data-stu-id="2440b-277">VNet name</span></span>|<span data-ttu-id="2440b-278">已連線網站</span><span class="sxs-lookup"><span data-stu-id="2440b-278">Connected site</span></span>|<span data-ttu-id="2440b-279">閘道 IP 位址</span><span class="sxs-lookup"><span data-stu-id="2440b-279">Gateway IP address</span></span>|
|:--- |:--- |:--- |
|<span data-ttu-id="2440b-280">TestVNet1</span><span class="sxs-lookup"><span data-stu-id="2440b-280">TestVNet1</span></span>|<span data-ttu-id="2440b-281">VNet4Local</span><span class="sxs-lookup"><span data-stu-id="2440b-281">VNet4Local</span></span>|<span data-ttu-id="2440b-282">TestVNet4 的 VPN 閘道 IP 位址</span><span class="sxs-lookup"><span data-stu-id="2440b-282">VPN gateway IP address for TestVNet4</span></span>|
|<span data-ttu-id="2440b-283">TestVNet4</span><span class="sxs-lookup"><span data-stu-id="2440b-283">TestVNet4</span></span>|<span data-ttu-id="2440b-284">VNet1Local</span><span class="sxs-lookup"><span data-stu-id="2440b-284">VNet1Local</span></span>|<span data-ttu-id="2440b-285">TestVNet1 的 VPN 閘道 IP 位址</span><span class="sxs-lookup"><span data-stu-id="2440b-285">VPN gateway IP address for TestVNet1</span></span>|

### <a name="part-1---get-hello-virtual-network-gateway-public-ip-address"></a><span data-ttu-id="2440b-286">組件 1-取得 hello 虛擬網路閘道的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="2440b-286">Part 1 - Get hello virtual network gateway public IP address</span></span>

1. <span data-ttu-id="2440b-287">Hello Azure 入口網站中，找出您的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="2440b-287">Locate your virtual network in hello Azure portal.</span></span>
2. <span data-ttu-id="2440b-288">按一下 tooopen hello VNet**概觀**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2440b-288">Click tooopen hello VNet **Overview** blade.</span></span> <span data-ttu-id="2440b-289">Hello 刀鋒視窗，在**VPN 連線**，您可以檢視您的虛擬網路閘道 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2440b-289">On hello blade, in **VPN connections**, you can view hello IP address for your virtual network gateway.</span></span>

  ![公用 IP](./media/vpn-gateway-howto-vnet-vnet-portal-classic/publicIP.png)
3. <span data-ttu-id="2440b-291">複製 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2440b-291">Copy hello IP address.</span></span> <span data-ttu-id="2440b-292">您可以將 hello 下一節。</span><span class="sxs-lookup"><span data-stu-id="2440b-292">You will use it in hello next section.</span></span>
4. <span data-ttu-id="2440b-293">對 TestVNet4 重複執行這些步驟</span><span class="sxs-lookup"><span data-stu-id="2440b-293">Repeat these steps for TestVNet4</span></span>

### <a name="part-2---modify-hello-local-sites"></a><span data-ttu-id="2440b-294">第 2 部分-修改 hello 本機站台</span><span class="sxs-lookup"><span data-stu-id="2440b-294">Part 2 - Modify hello local sites</span></span>

1. <span data-ttu-id="2440b-295">Hello Azure 入口網站中，找出您的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="2440b-295">Locate your virtual network in hello Azure portal.</span></span>
2. <span data-ttu-id="2440b-296">在 hello VNet**概觀**刀鋒視窗中，按一下 hello 本機站台。</span><span class="sxs-lookup"><span data-stu-id="2440b-296">On hello VNet **Overview** blade, click hello local site.</span></span>

  ![建立本機網站](./media/vpn-gateway-howto-vnet-vnet-portal-classic/local.png)
3. <span data-ttu-id="2440b-298">在 hello**站對站 VPN 連線**刀鋒視窗中，按一下您想 toomodify hello 本機站台 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="2440b-298">On hello **Site-to-Site VPN Connections** blade, click hello name of hello local site that you want toomodify.</span></span>

  ![開啟本機網站](./media/vpn-gateway-howto-vnet-vnet-portal-classic/openlocal.png)
4. <span data-ttu-id="2440b-300">按一下 hello**本機站台**想 toomodify。</span><span class="sxs-lookup"><span data-stu-id="2440b-300">Click hello **Local site** that you want toomodify.</span></span>

  ![修改網站](./media/vpn-gateway-howto-vnet-vnet-portal-classic/connections.png)
5. <span data-ttu-id="2440b-302">更新 hello **VPN 閘道 IP 位址**按一下**確定**toosave hello 設定。</span><span class="sxs-lookup"><span data-stu-id="2440b-302">Update hello **VPN gateway IP address** and click **OK** toosave hello settings.</span></span>

  ![閘道 IP](./media/vpn-gateway-howto-vnet-vnet-portal-classic/gwupdate.png)
6. <span data-ttu-id="2440b-304">關閉 hello 其他刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2440b-304">Close hello other blades.</span></span>
7. <span data-ttu-id="2440b-305">對 TestVNet4 重複執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="2440b-305">Repeat these steps for TestVNet4.</span></span>

## <span data-ttu-id="2440b-306"><a name="getvalues"></a>步驟 7: hello 網路組態檔中的擷取值</span><span class="sxs-lookup"><span data-stu-id="2440b-306"><a name="getvalues"></a>Step 7 - Retrieve values from hello network configuration file</span></span>

<span data-ttu-id="2440b-307">當您在 hello Azure 入口網站中建立傳統的 Vnet 時，您檢視的 hello 名稱不是您使用 PowerShell 的 hello 完整名稱。</span><span class="sxs-lookup"><span data-stu-id="2440b-307">When you create classic VNets in hello Azure portal, hello name that you view is not hello full name that you use for PowerShell.</span></span> <span data-ttu-id="2440b-308">例如，出現 toobe 名為 VNet **TestVNet1**在 hello 入口網站中，可能會有多長的名稱 hello 網路組態檔中。</span><span class="sxs-lookup"><span data-stu-id="2440b-308">For example, a VNet that appears toobe named **TestVNet1** in hello portal, may have a much longer name in hello network configuration file.</span></span> <span data-ttu-id="2440b-309">hello 名稱可能看起來像這樣：**群組 ClassicRG TestVNet1**。</span><span class="sxs-lookup"><span data-stu-id="2440b-309">hello name might look something like: **Group ClassicRG TestVNet1**.</span></span> <span data-ttu-id="2440b-310">當您建立您的連線時，是您在 hello 網路組態檔中看到的重要 toouse hello 值。</span><span class="sxs-lookup"><span data-stu-id="2440b-310">When you create your connections, it's important toouse hello values that you see in hello network configuration file.</span></span>

<span data-ttu-id="2440b-311">在 hello 下列步驟，您將連接 tooyour Azure 帳戶然後下載並檢視 hello 網路組態檔 tooobtain hello 值所需的連線。</span><span class="sxs-lookup"><span data-stu-id="2440b-311">In hello following steps, you will connect tooyour Azure account and download and view hello network configuration file tooobtain hello values that are required for your connections.</span></span>

1. <span data-ttu-id="2440b-312">下載並安裝 hello 的 hello Azure 服務管理 (SM) PowerShell cmdlet 的最新版本。</span><span class="sxs-lookup"><span data-stu-id="2440b-312">Download and install hello latest version of hello Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="2440b-313">如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="2440b-313">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

2. <span data-ttu-id="2440b-314">使用提高的權限開啟 PowerShell 主控台和 tooyour 帳戶連接。</span><span class="sxs-lookup"><span data-stu-id="2440b-314">Open your PowerShell console with elevated rights and connect tooyour account.</span></span> <span data-ttu-id="2440b-315">使用下列範例 toohelp 您連接的 hello:</span><span class="sxs-lookup"><span data-stu-id="2440b-315">Use hello following example toohelp you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="2440b-316">請檢查 hello hello 帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2440b-316">Check hello subscriptions for hello account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="2440b-317">如果您有多個訂閱，選取您想 toouse hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2440b-317">If you have more than one subscription, select hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
  ```

  <span data-ttu-id="2440b-318">接下來，使用下列 cmdlet tooadd hello Azure 訂用帳戶 tooPowerShell hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="2440b-318">Next, use hello following cmdlet tooadd your Azure subscription tooPowerShell for hello classic deployment model.</span></span>

  ```powershell
  Add-AzureAccount
  ```
3. <span data-ttu-id="2440b-319">匯出並檢視 hello 網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="2440b-319">Export and view hello network configuration file.</span></span> <span data-ttu-id="2440b-320">您的電腦上建立目錄，然後匯出 hello 網路組態檔 toohello 目錄。</span><span class="sxs-lookup"><span data-stu-id="2440b-320">Create a directory on your computer and then export hello network configuration file toohello directory.</span></span> <span data-ttu-id="2440b-321">在此範例中，hello 網路組態檔匯出太**C:\AzureNet**。</span><span class="sxs-lookup"><span data-stu-id="2440b-321">In this example, hello network configuration file is exported too**C:\AzureNet**.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
4. <span data-ttu-id="2440b-322">開啟 hello 檔案，並為您的 Vnet 和站台的文字編輯器和檢視 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="2440b-322">Open hello file with a text editor and view hello names for your VNets and sites.</span></span> <span data-ttu-id="2440b-323">這些會是建立您的連線時所使用的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="2440b-323">These will be hello name you use when you create your connections.</span></span><br><span data-ttu-id="2440b-324">VNet 名稱會列為 **VirtualNetworkSite name =**</span><span class="sxs-lookup"><span data-stu-id="2440b-324">VNet names are listed as **VirtualNetworkSite name =**</span></span><br><span data-ttu-id="2440b-325">網站名稱會列為 **LocalNetworkSiteRef name =**</span><span class="sxs-lookup"><span data-stu-id="2440b-325">Site names are listed as **LocalNetworkSiteRef name =**</span></span>

## <span data-ttu-id="2440b-326"><a name="createconnections"></a>步驟 8-建立 hello VPN 閘道連線</span><span class="sxs-lookup"><span data-stu-id="2440b-326"><a name="createconnections"></a>Step 8 - Create hello VPN gateway connections</span></span>

<span data-ttu-id="2440b-327">當 hello 上述所有步驟都完成時，您可以將 hello IPsec/IKE 預先共用的金鑰，並建立 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="2440b-327">When all hello previous steps have been completed, you can set hello IPsec/IKE pre-shared keys and create hello connection.</span></span> <span data-ttu-id="2440b-328">這組步驟會使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="2440b-328">This set of steps uses PowerShell.</span></span> <span data-ttu-id="2440b-329">無法在 hello Azure 入口網站中設定 hello 傳統部署模型的 VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="2440b-329">VNet-to-VNet connections for hello classic deployment model cannot be configured in hello Azure portal.</span></span>

<span data-ttu-id="2440b-330">在 hello 範例中，請注意，hello 共用的金鑰是完全 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="2440b-330">In hello examples, notice that hello shared key is exactly hello same.</span></span> <span data-ttu-id="2440b-331">一定要相符 hello 共用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="2440b-331">hello shared key must always match.</span></span> <span data-ttu-id="2440b-332">為確定 tooreplace hello hello 確切名稱，您的 Vnet 與區域網路網站與這些範例中的值。</span><span class="sxs-lookup"><span data-stu-id="2440b-332">Be sure tooreplace hello values in these examples with hello exact names for your VNets and Local Network Sites.</span></span>

1. <span data-ttu-id="2440b-333">建立 hello TestVNet1 tooTestVNet4 連線。</span><span class="sxs-lookup"><span data-stu-id="2440b-333">Create hello TestVNet1 tooTestVNet4 connection.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet1' `
  -LocalNetworkSiteName '17BE5E2C_VNet4Local' -SharedKey A1b2C3D4
  ```
2. <span data-ttu-id="2440b-334">建立 hello TestVNet4 tooTestVNet1 連線。</span><span class="sxs-lookup"><span data-stu-id="2440b-334">Create hello TestVNet4 tooTestVNet1 connection.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet4' `
  -LocalNetworkSiteName 'F7F7BFC7_VNet1Local' -SharedKey A1b2C3D4
  ```
3. <span data-ttu-id="2440b-335">等候 hello 連線 tooinitialize。</span><span class="sxs-lookup"><span data-stu-id="2440b-335">Wait for hello connections tooinitialize.</span></span> <span data-ttu-id="2440b-336">一旦 hello 閘道完成初始化，hello 狀態會是 '成功'。</span><span class="sxs-lookup"><span data-stu-id="2440b-336">Once hello gateway has initialized, hello Status is 'Successful'.</span></span>

  ```
  Error          :
  HttpStatusCode : OK
  Id             :
  Status         : Successful
  RequestId      :
  StatusCode     : OK
  ```

## <span data-ttu-id="2440b-337"><a name="faq"></a>傳統 VNet 的 VNet 對 VNet 考量</span><span class="sxs-lookup"><span data-stu-id="2440b-337"><a name="faq"></a>VNet-to-VNet considerations for classic VNets</span></span>
* <span data-ttu-id="2440b-338">hello 虛擬網路可位於 hello 相同或不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="2440b-338">hello virtual networks can be in hello same or different subscriptions.</span></span>
* <span data-ttu-id="2440b-339">hello 虛擬網路可位於 hello 相同或不同 Azure 區域 （位置）。</span><span class="sxs-lookup"><span data-stu-id="2440b-339">hello virtual networks can be in hello same or different Azure regions (locations).</span></span>
* <span data-ttu-id="2440b-340">即使虛擬網路連接在一起，雲端服務或負載平衡端點也無法跨虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="2440b-340">A cloud service or a load balancing endpoint can't span across virtual networks, even if they are connected together.</span></span>
* <span data-ttu-id="2440b-341">將多個虛擬網路連接在一起並不需要任何 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="2440b-341">Connecting multiple virtual networks together doesn't require any VPN devices.</span></span>
* <span data-ttu-id="2440b-342">VNet 對 VNet 支援連接 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="2440b-342">VNet-to-VNet supports connecting Azure Virtual Networks.</span></span> <span data-ttu-id="2440b-343">不支援連接的虛擬機器或雲端服務不會部署 tooa 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="2440b-343">It does not support connecting virtual machines or cloud services that are not deployed tooa virtual network.</span></span>
* <span data-ttu-id="2440b-344">VNet 對 VNet 需要動態路由閘道。</span><span class="sxs-lookup"><span data-stu-id="2440b-344">VNet-to-VNet requires dynamic routing gateways.</span></span> <span data-ttu-id="2440b-345">不支援 Azure 靜態路由閘道。</span><span class="sxs-lookup"><span data-stu-id="2440b-345">Azure static routing gateways are not supported.</span></span>
* <span data-ttu-id="2440b-346">虛擬網路連線能力可以與多站台 VPN 同時使用。</span><span class="sxs-lookup"><span data-stu-id="2440b-346">Virtual network connectivity can be used simultaneously with multi-site VPNs.</span></span> <span data-ttu-id="2440b-347">沒有最多 10 個 VPN 通道連線 tooeither 其他虛擬網路或在內部部署網站虛擬網路 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="2440b-347">There is a maximum of 10 VPN tunnels for a virtual network VPN gateway connecting tooeither other virtual networks, or on-premises sites.</span></span>
* <span data-ttu-id="2440b-348">hello hello 虛擬網路及內部部署區域網路網站不能重疊位址空間。</span><span class="sxs-lookup"><span data-stu-id="2440b-348">hello address spaces of hello virtual networks and on-premises local network sites must not overlap.</span></span> <span data-ttu-id="2440b-349">重疊的位址空間會導致 hello 建立虛擬網路或上傳的 netcfg 組態檔 toofail。</span><span class="sxs-lookup"><span data-stu-id="2440b-349">Overlapping address spaces will cause hello creation of virtual networks or uploading netcfg configuration files toofail.</span></span>
* <span data-ttu-id="2440b-350">不支援成對虛擬網路之間的備援通道。</span><span class="sxs-lookup"><span data-stu-id="2440b-350">Redundant tunnels between a pair of virtual networks are not supported.</span></span>
* <span data-ttu-id="2440b-351">所有 VPN 通道 hello VNet，包括 P2S Vpn、 共用 hello hello VPN 閘道，可用的頻寬，以及 hello 相同 azure VPN 閘道執行時間 SLA。</span><span class="sxs-lookup"><span data-stu-id="2440b-351">All VPN tunnels for hello VNet, including P2S VPNs, share hello available bandwidth for hello VPN gateway, and hello same VPN gateway uptime SLA in Azure.</span></span>
* <span data-ttu-id="2440b-352">VNet 對 VNet 流量會透過 hello Azure 骨幹。</span><span class="sxs-lookup"><span data-stu-id="2440b-352">VNet-to-VNet traffic travels across hello Azure backbone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2440b-353">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2440b-353">Next steps</span></span>
<span data-ttu-id="2440b-354">確認您的連線。</span><span class="sxs-lookup"><span data-stu-id="2440b-354">Verify your connections.</span></span> <span data-ttu-id="2440b-355">[確認 VPN 閘道連線](vpn-gateway-verify-connection-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="2440b-355">See [Verify a VPN Gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>
