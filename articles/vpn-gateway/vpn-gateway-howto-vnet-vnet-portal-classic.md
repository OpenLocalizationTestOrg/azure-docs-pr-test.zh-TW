---
title: "建立 VNet 之間的連線：傳統：Azure 入口網站 | Microsoft Docs"
description: "如何使用 PowerShell 和 Azure 傳統入口網站將 Azure 虛擬網路連接在一起。"
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
ms.openlocfilehash: 77097d59077cd8e199acdb5dc0d8427369565eea
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="configure-a-vnet-to-vnet-connection-classic"></a><span data-ttu-id="23aed-103">設定 VNet 對 VNet 連線 (傳統)</span><span class="sxs-lookup"><span data-stu-id="23aed-103">Configure a VNet-to-VNet connection (classic)</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

<span data-ttu-id="23aed-104">本文說明如何建立虛擬網路之間的 VPN 閘道連線。</span><span class="sxs-lookup"><span data-stu-id="23aed-104">This article shows you how to create a VPN gateway connection between virtual networks.</span></span> <span data-ttu-id="23aed-105">虛擬網路可位於相同或不同的區域，以及來自相同或不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="23aed-105">The virtual networks can be in the same or different regions, and from the same or different subscriptions.</span></span> <span data-ttu-id="23aed-106">本文中的步驟適用於傳統部署模型和 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="23aed-106">The steps in this article apply to the classic deployment model and the Azure portal.</span></span> <span data-ttu-id="23aed-107">您也可從下列清單中選取不同的選項，以使用不同的部署工具或部署模型來建立此組態：</span><span class="sxs-lookup"><span data-stu-id="23aed-107">You can also create this configuration using a different deployment tool or deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="23aed-108">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="23aed-108">Azure portal</span></span>](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [<span data-ttu-id="23aed-109">PowerShell</span><span class="sxs-lookup"><span data-stu-id="23aed-109">PowerShell</span></span>](vpn-gateway-vnet-vnet-rm-ps.md)
> * [<span data-ttu-id="23aed-110">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="23aed-110">Azure CLI</span></span>](vpn-gateway-howto-vnet-vnet-cli.md)
> * [<span data-ttu-id="23aed-111">Azure 入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="23aed-111">Azure portal (classic)</span></span>](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [<span data-ttu-id="23aed-112">連線不同的部署模型 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="23aed-112">Connect different deployment models - Azure portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="23aed-113">連線不同的部署模型 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="23aed-113">Connect different deployment models - PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

![VNet 對 VNet 連線能力圖表](./media/vpn-gateway-howto-vnet-vnet-portal-classic/v2vclassic.png)

## <a name="about-vnet-to-vnet-connections"></a><span data-ttu-id="23aed-115">關於 VNet 對 VNet 連線</span><span class="sxs-lookup"><span data-stu-id="23aed-115">About VNet-to-VNet connections</span></span>

<span data-ttu-id="23aed-116">在傳統部署模型中使用 VPN 閘道將一個虛擬網路連線到另一個虛擬網路 (VNet 對 VNet)，類似於將虛擬網路連線到內部部署網站位置。</span><span class="sxs-lookup"><span data-stu-id="23aed-116">Connecting a virtual network to another virtual network (VNet-to-VNet) in the classic deployment model using a VPN gateway is similar to connecting a virtual network to an on-premises site location.</span></span> <span data-ttu-id="23aed-117">這兩種連線類型都使用 VPN 閘道提供使用 IPsec/IKE 的安全通道。</span><span class="sxs-lookup"><span data-stu-id="23aed-117">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span>

<span data-ttu-id="23aed-118">您所連線的 Vnet 可位於不同的訂用帳戶和不同的區域。</span><span class="sxs-lookup"><span data-stu-id="23aed-118">The VNets you connect can be in different subscriptions and different regions.</span></span> <span data-ttu-id="23aed-119">您可以將 VNet 對 VNet 通訊與多站台組態結合。</span><span class="sxs-lookup"><span data-stu-id="23aed-119">You can combine VNet to VNet communication with multi-site configurations.</span></span> <span data-ttu-id="23aed-120">這可讓您建立結合了跨單位連線與內部虛擬網路連線的網路拓撲。</span><span class="sxs-lookup"><span data-stu-id="23aed-120">This lets you establish network topologies that combine cross-premises connectivity with inter-virtual network connectivity.</span></span>

![VNet 對 VNet 連線](./media/vpn-gateway-howto-vnet-vnet-portal-classic/aboutconnections.png)

### <span data-ttu-id="23aed-122"><a name="why"></a>為什麼要連線虛擬網路？</span><span class="sxs-lookup"><span data-stu-id="23aed-122"><a name="why"></a>Why connect virtual networks?</span></span>

<span data-ttu-id="23aed-123">針對下列原因，您可能希望連接虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="23aed-123">You may want to connect virtual networks for the following reasons:</span></span>

* <span data-ttu-id="23aed-124">**跨區域的異地備援和異地目前狀態**</span><span class="sxs-lookup"><span data-stu-id="23aed-124">**Cross region geo-redundancy and geo-presence**</span></span>

  * <span data-ttu-id="23aed-125">您可以使用安全連線設定自己的異地複寫或同步處理，而不用查看網際網路對向端點。</span><span class="sxs-lookup"><span data-stu-id="23aed-125">You can set up your own geo-replication or synchronization with secure connectivity without going over Internet-facing endpoints.</span></span>
  * <span data-ttu-id="23aed-126">有了 Azure Load Balancer 和 Microsoft 或第三方叢集技術，您便可以利用跨多個 Azure 區域的異地備援，設定具有高可用性的工作負載。</span><span class="sxs-lookup"><span data-stu-id="23aed-126">With Azure Load Balancer and Microsoft or third-party clustering technology, you can set up highly available workload with geo-redundancy across multiple Azure regions.</span></span> <span data-ttu-id="23aed-127">其中一個重要的範例就是使用分散在多個 Azure 區域的可用性群組來設定 SQL Always On。</span><span class="sxs-lookup"><span data-stu-id="23aed-127">One important example is to set up SQL Always On with Availability Groups spreading across multiple Azure regions.</span></span>
* <span data-ttu-id="23aed-128">**具有嚴密隔離界限的區域性多層式應用程式**</span><span class="sxs-lookup"><span data-stu-id="23aed-128">**Regional multi-tier applications with strong isolation boundary**</span></span>

  * <span data-ttu-id="23aed-129">在相同的區域中，您可以設定既有多個 VNet 相連又有嚴密的隔離及安全的層次間通訊的多層式應用程式。</span><span class="sxs-lookup"><span data-stu-id="23aed-129">Within the same region, you can set up multi-tier applications with multiple VNets connected together with strong isolation and secure inter-tier communication.</span></span>
* <span data-ttu-id="23aed-130">**Azure 中的跨訂用帳戶、組織間通訊**</span><span class="sxs-lookup"><span data-stu-id="23aed-130">**Cross subscription, inter-organization communication in Azure**</span></span>

  * <span data-ttu-id="23aed-131">如果您有多個 Azure 訂用帳戶，您可以將虛擬網路之間不同訂用帳戶的工作負載安全地連接在一起。</span><span class="sxs-lookup"><span data-stu-id="23aed-131">If you have multiple Azure subscriptions, you can connect workloads from different subscriptions together securely between virtual networks.</span></span>
  * <span data-ttu-id="23aed-132">針對企業或服務提供者，您可以在 Azure 中使用安全 VPN 技術啟用跨組織通訊。</span><span class="sxs-lookup"><span data-stu-id="23aed-132">For enterprises or service providers, you can enable cross-organization communication with secure VPN technology within Azure.</span></span>

<span data-ttu-id="23aed-133">如需 VNet 對 VNet 連接的詳細資訊，請參閱本文結尾處的 [VNet 對 VNet 的考量](#faq)。</span><span class="sxs-lookup"><span data-stu-id="23aed-133">For more information about VNet-to-VNet connections, see [VNet-to-VNet considerations](#faq) at the end of this article.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="23aed-134">開始之前</span><span class="sxs-lookup"><span data-stu-id="23aed-134">Before you begin</span></span>

<span data-ttu-id="23aed-135">開始本練習之前，請下載並安裝最新版的 Azure 服務管理 (SM) PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="23aed-135">Before beginning this exercise, download and install the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="23aed-136">如需詳細資訊，請參閱 [如何安裝及設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="23aed-136">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="23aed-137">我們使用入口網站來執行大部分的步驟，但是您必須使用 PowerShell 來建立 Vnet 之間的連線。</span><span class="sxs-lookup"><span data-stu-id="23aed-137">We use the portal for most of the steps, but you must use PowerShell to create the connections between the VNets.</span></span> <span data-ttu-id="23aed-138">您無法使用 Azure 入口網站建立連線。</span><span class="sxs-lookup"><span data-stu-id="23aed-138">You can't create the connections using the Azure portal.</span></span>

## <span data-ttu-id="23aed-139"><a name="plan"></a>步驟 1 - 規劃 IP 位址範圍</span><span class="sxs-lookup"><span data-stu-id="23aed-139"><a name="plan"></a>Step 1 - Plan your IP address ranges</span></span>

<span data-ttu-id="23aed-140">決定將用來設定虛擬網路的範圍相當重要。</span><span class="sxs-lookup"><span data-stu-id="23aed-140">It’s important to decide the ranges that you’ll use to configure your virtual networks.</span></span> <span data-ttu-id="23aed-141">就此組態而言，您必須確定沒有任何 VNet 範圍彼此重疊，或是與其連接的區域網路重疊。</span><span class="sxs-lookup"><span data-stu-id="23aed-141">For this configuration, you must make sure that none of your VNet ranges overlap with each other, or with any of the local networks that they connect to.</span></span>

<span data-ttu-id="23aed-142">下表顯示一個範例，說明如何定義 VNet。</span><span class="sxs-lookup"><span data-stu-id="23aed-142">The following table shows an example of how to define your VNets.</span></span> <span data-ttu-id="23aed-143">範圍僅供作為指導方針。</span><span class="sxs-lookup"><span data-stu-id="23aed-143">Use the ranges as a guideline only.</span></span> <span data-ttu-id="23aed-144">請記下您虛擬網路的範圍。</span><span class="sxs-lookup"><span data-stu-id="23aed-144">Write down the ranges for your virtual networks.</span></span> <span data-ttu-id="23aed-145">稍後的步驟將會需要這項資訊。</span><span class="sxs-lookup"><span data-stu-id="23aed-145">You need this information for later steps.</span></span>

<span data-ttu-id="23aed-146">**範例**</span><span class="sxs-lookup"><span data-stu-id="23aed-146">**Example**</span></span>

| <span data-ttu-id="23aed-147">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="23aed-147">Virtual Network</span></span> | <span data-ttu-id="23aed-148">位址空間</span><span class="sxs-lookup"><span data-stu-id="23aed-148">Address Space</span></span> | <span data-ttu-id="23aed-149">區域</span><span class="sxs-lookup"><span data-stu-id="23aed-149">Region</span></span> | <span data-ttu-id="23aed-150">連接至區域網路站台</span><span class="sxs-lookup"><span data-stu-id="23aed-150">Connects to local network site</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="23aed-151">TestVNet1</span><span class="sxs-lookup"><span data-stu-id="23aed-151">TestVNet1</span></span> |<span data-ttu-id="23aed-152">TestVNet1</span><span class="sxs-lookup"><span data-stu-id="23aed-152">TestVNet1</span></span><br><span data-ttu-id="23aed-153">(10.11.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="23aed-153">(10.11.0.0/16)</span></span><br><span data-ttu-id="23aed-154">(10.12.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="23aed-154">(10.12.0.0/16)</span></span> |<span data-ttu-id="23aed-155">美國東部</span><span class="sxs-lookup"><span data-stu-id="23aed-155">East US</span></span> |<span data-ttu-id="23aed-156">VNet4Local</span><span class="sxs-lookup"><span data-stu-id="23aed-156">VNet4Local</span></span><br><span data-ttu-id="23aed-157">(10.41.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="23aed-157">(10.41.0.0/16)</span></span><br><span data-ttu-id="23aed-158">(10.42.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="23aed-158">(10.42.0.0/16)</span></span> |
| <span data-ttu-id="23aed-159">TestVNet4</span><span class="sxs-lookup"><span data-stu-id="23aed-159">TestVNet4</span></span> |<span data-ttu-id="23aed-160">TestVNet4</span><span class="sxs-lookup"><span data-stu-id="23aed-160">TestVNet4</span></span><br><span data-ttu-id="23aed-161">(10.41.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="23aed-161">(10.41.0.0/16)</span></span><br><span data-ttu-id="23aed-162">(10.42.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="23aed-162">(10.42.0.0/16)</span></span> |<span data-ttu-id="23aed-163">美國西部</span><span class="sxs-lookup"><span data-stu-id="23aed-163">West US</span></span> |<span data-ttu-id="23aed-164">VNet1Local</span><span class="sxs-lookup"><span data-stu-id="23aed-164">VNet1Local</span></span><br><span data-ttu-id="23aed-165">(10.11.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="23aed-165">(10.11.0.0/16)</span></span><br><span data-ttu-id="23aed-166">(10.12.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="23aed-166">(10.12.0.0/16)</span></span> |

## <span data-ttu-id="23aed-167"><a name="vnetvalues"></a>步驟 2 - 建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="23aed-167"><a name="vnetvalues"></a>Step 2 - Create the virtual networks</span></span>

<span data-ttu-id="23aed-168">在 [Azure 入口網站](https://portal.azure.com)中建立兩個虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="23aed-168">Create two virtual networks in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="23aed-169">如需建立傳統虛擬網路的步驟，請參閱[建立傳統虛擬網路](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="23aed-169">For the steps to create classic virtual networks, see [Create a classic virtual network](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).</span></span> 

<span data-ttu-id="23aed-170">使用入口網站建立傳統虛擬網路時，您必須使用下列步驟來瀏覽至 [虛擬網路] 刀鋒視窗，否則建立傳統虛擬網路的選項就不會出現：</span><span class="sxs-lookup"><span data-stu-id="23aed-170">When using the portal to create a classic virtual network, you must navigate to the virtual network blade by using the following steps, otherwise the option to create a classic virtual network does not appear:</span></span>

1. <span data-ttu-id="23aed-171">按一下 [+] 以開啟 [新增] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="23aed-171">Click the '+' to open the 'New' blade.</span></span>
2. <span data-ttu-id="23aed-172">在 [搜尋 Marketplace] 欄位中，輸入「虛擬網路」。</span><span class="sxs-lookup"><span data-stu-id="23aed-172">In the 'Search the marketplace' field, type 'Virtual Network'.</span></span> <span data-ttu-id="23aed-173">如果您改為選取 [網路功能]-> [虛擬網路]，將無法取得建立傳統 VNet 的選項。</span><span class="sxs-lookup"><span data-stu-id="23aed-173">If you instead, select Networking -> Virtual Network, you will not get the option to create a classic VNet.</span></span>
3. <span data-ttu-id="23aed-174">在傳回的清單中找到 [虛擬網路]，然後按一下以開啟 [虛擬網路] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="23aed-174">Locate 'Virtual Network' from the returned list and click it to open the Virtual Network blade.</span></span> 
4. <span data-ttu-id="23aed-175">在 [虛擬網路] 刀鋒視窗中，選取 [傳統] 以建立傳統的 VNet。</span><span class="sxs-lookup"><span data-stu-id="23aed-175">On the virtual network blade, select 'Classic' to create a classic VNet.</span></span> 

<span data-ttu-id="23aed-176">如果您使用這篇文章作為練習，您可以使用下列範例值：</span><span class="sxs-lookup"><span data-stu-id="23aed-176">If you are using this article as an exercise, you can use the following example values:</span></span>

<span data-ttu-id="23aed-177">**TestVNet1 的值**</span><span class="sxs-lookup"><span data-stu-id="23aed-177">**Values for TestVNet1**</span></span>

<span data-ttu-id="23aed-178">名稱︰TestVNet1</span><span class="sxs-lookup"><span data-stu-id="23aed-178">Name: TestVNet1</span></span><br>
<span data-ttu-id="23aed-179">位址空間︰10.11.0.0/16、10.12.0.0/16 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="23aed-179">Address space: 10.11.0.0/16, 10.12.0.0/16 (optional)</span></span><br>
<span data-ttu-id="23aed-180">子網路名稱：default</span><span class="sxs-lookup"><span data-stu-id="23aed-180">Subnet name: default</span></span><br>
<span data-ttu-id="23aed-181">子網路位址範圍：10.11.0.1/24</span><span class="sxs-lookup"><span data-stu-id="23aed-181">Subnet address range: 10.11.0.1/24</span></span><br>
<span data-ttu-id="23aed-182">資源群組：ClassicRG</span><span class="sxs-lookup"><span data-stu-id="23aed-182">Resource group: ClassicRG</span></span><br>
<span data-ttu-id="23aed-183">位置：美國東部</span><span class="sxs-lookup"><span data-stu-id="23aed-183">Location: East US</span></span><br>
<span data-ttu-id="23aed-184">GatewaySubnet：10.11.1.0/27</span><span class="sxs-lookup"><span data-stu-id="23aed-184">GatewaySubnet: 10.11.1.0/27</span></span>

<span data-ttu-id="23aed-185">**TestVNet4 的值**</span><span class="sxs-lookup"><span data-stu-id="23aed-185">**Values for TestVNet4**</span></span>

<span data-ttu-id="23aed-186">名稱︰TestVNet4</span><span class="sxs-lookup"><span data-stu-id="23aed-186">Name: TestVNet4</span></span><br>
<span data-ttu-id="23aed-187">位址空間︰10.41.0.0/16、10.42.0.0/16 (選擇性)</span><span class="sxs-lookup"><span data-stu-id="23aed-187">Address space: 10.41.0.0/16, 10.42.0.0/16 (optional)</span></span><br>
<span data-ttu-id="23aed-188">子網路名稱：default</span><span class="sxs-lookup"><span data-stu-id="23aed-188">Subnet name: default</span></span><br>
<span data-ttu-id="23aed-189">子網路位址範圍：10.41.0.1/24</span><span class="sxs-lookup"><span data-stu-id="23aed-189">Subnet address range: 10.41.0.1/24</span></span><br>
<span data-ttu-id="23aed-190">資源群組：ClassicRG</span><span class="sxs-lookup"><span data-stu-id="23aed-190">Resource group: ClassicRG</span></span><br>
<span data-ttu-id="23aed-191">位置：美國西部</span><span class="sxs-lookup"><span data-stu-id="23aed-191">Location: West US</span></span><br>
<span data-ttu-id="23aed-192">GatewaySubnet：10.41.1.0/27</span><span class="sxs-lookup"><span data-stu-id="23aed-192">GatewaySubnet: 10.41.1.0/27</span></span>

<span data-ttu-id="23aed-193">**在建立 VNet 時，請牢記下列設定︰**</span><span class="sxs-lookup"><span data-stu-id="23aed-193">**When creating your VNets, keep in mind the following settings:**</span></span>

* <span data-ttu-id="23aed-194">**虛擬網路位址空間** – 在 [虛擬網路位址空間] 頁面上，指定您想要用於虛擬網路的位址範圍。</span><span class="sxs-lookup"><span data-stu-id="23aed-194">**Virtual Network Address Spaces** – On the Virtual Network Address Spaces page, specify the address range that you want to use for your virtual network.</span></span> <span data-ttu-id="23aed-195">這些是將指派給 VM 的動態 IP 位址，以及指派給您部署至此虛擬網路之其他角色執行個體的動態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="23aed-195">These are the dynamic IP addresses that will be assigned to the VMs and other role instances that you deploy to this virtual network.</span></span><br><span data-ttu-id="23aed-196">您選取的位址空間不能與任何其他 VNet 的位址空間，或此 VNet 連線之內部部署位置的位址空間重疊。</span><span class="sxs-lookup"><span data-stu-id="23aed-196">The address spaces you select cannot overlap with the address spaces for any of the other VNets or on-premises locations that this VNet will connect to.</span></span>

* <span data-ttu-id="23aed-197">**位置** – 當您建立虛擬網路時，您會將該位置與 Azure 位置 (區域) 產生關聯。</span><span class="sxs-lookup"><span data-stu-id="23aed-197">**Location** – When you create a virtual network, you associate it with an Azure location (region).</span></span> <span data-ttu-id="23aed-198">例如，如果您希望部署到虛擬網路的 VM 實際位於美國西部，請選取該位置。</span><span class="sxs-lookup"><span data-stu-id="23aed-198">For example, if you want your VMs that are deployed to your virtual network to be physically located in West US, select that location.</span></span> <span data-ttu-id="23aed-199">建立關聯之後，您就無法變更與您的虛擬網路相關聯的位置。</span><span class="sxs-lookup"><span data-stu-id="23aed-199">You can’t change the location associated with your virtual network after you create it.</span></span>

<span data-ttu-id="23aed-200">**建立 VNet 之後，您可以新增下列設定︰**</span><span class="sxs-lookup"><span data-stu-id="23aed-200">**After creating your VNets, you can add the following settings:**</span></span>

* <span data-ttu-id="23aed-201">**位址空間** – 此組態不需要額外的位址空間，但是您可以在建立 VNet 之後新增額外的位址空間。</span><span class="sxs-lookup"><span data-stu-id="23aed-201">**Address space** – Additional address space is not required for this configuration, but you can add additional address space after creating the VNet.</span></span>

* <span data-ttu-id="23aed-202">**子網路** – 此組態不需要額外的子網路，但是您可能想要讓您的 VM 位於與其他角色執行個體不同的子網路中。</span><span class="sxs-lookup"><span data-stu-id="23aed-202">**Subnets** – Additional subnets are not required for this configuration, but you might want to have your VMs in a subnet that is separate from your other role instances.</span></span>

* <span data-ttu-id="23aed-203">**DNS 伺服器** – 輸入 DNS 伺服器名稱和 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="23aed-203">**DNS servers** – Enter the DNS server name and IP address.</span></span> <span data-ttu-id="23aed-204">此設定不會建立 DNS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="23aed-204">This setting does not create a DNS server.</span></span> <span data-ttu-id="23aed-205">它可讓您指定要用於此虛擬網路之名稱解析的 DNS 服務。</span><span class="sxs-lookup"><span data-stu-id="23aed-205">It allows you to specify the DNS servers that you want to use for name resolution for this virtual network.</span></span>

<span data-ttu-id="23aed-206">在本節中，您會設定連線類型、本機網站，並建立閘道。</span><span class="sxs-lookup"><span data-stu-id="23aed-206">In this section, you configure the connection type, the local site, and create the gateway.</span></span>

## <span data-ttu-id="23aed-207"><a name="localsite"></a>步驟 3 - 設定本機網站</span><span class="sxs-lookup"><span data-stu-id="23aed-207"><a name="localsite"></a>Step 3 - Configure the local site</span></span>

<span data-ttu-id="23aed-208">Azure 會使用每個區域網路站台中指定的設定，來決定如何路由傳送 VNet 之間的流量。</span><span class="sxs-lookup"><span data-stu-id="23aed-208">Azure uses the settings specified in each local network site to determine how to route traffic between the VNets.</span></span> <span data-ttu-id="23aed-209">每個 VNet 都必須指向要做為流量路由傳送目的地的個別區域網路。</span><span class="sxs-lookup"><span data-stu-id="23aed-209">Each VNet must point to the respective local network that you want to route traffic to.</span></span> <span data-ttu-id="23aed-210">您需決定要用來參考每個區域網路站台的名稱。</span><span class="sxs-lookup"><span data-stu-id="23aed-210">You determine the name you want to use to refer to each local network site.</span></span> <span data-ttu-id="23aed-211">最好使用描述性的項目。</span><span class="sxs-lookup"><span data-stu-id="23aed-211">It's best to use something descriptive.</span></span>

<span data-ttu-id="23aed-212">例如，TestVNet1 會連線到您所建立名為 "VNet4Local" 的區域網路網站。</span><span class="sxs-lookup"><span data-stu-id="23aed-212">For example, TestVNet1 connects to a local network site that you create named 'VNet4Local'.</span></span> <span data-ttu-id="23aed-213">VNet4Local 的設定包含 TestVNet4 位址首碼。</span><span class="sxs-lookup"><span data-stu-id="23aed-213">The settings for VNet4Local contain the address prefixes for TestVNet4.</span></span>

<span data-ttu-id="23aed-214">每個 VNet 的本機網站是其他 VNet。</span><span class="sxs-lookup"><span data-stu-id="23aed-214">The local site for each VNet is the other VNet.</span></span> <span data-ttu-id="23aed-215">在我們的組態中使用下列範例值︰</span><span class="sxs-lookup"><span data-stu-id="23aed-215">The following example values are used for our configuration:</span></span>

| <span data-ttu-id="23aed-216">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="23aed-216">Virtual Network</span></span> | <span data-ttu-id="23aed-217">位址空間</span><span class="sxs-lookup"><span data-stu-id="23aed-217">Address Space</span></span> | <span data-ttu-id="23aed-218">區域</span><span class="sxs-lookup"><span data-stu-id="23aed-218">Region</span></span> | <span data-ttu-id="23aed-219">連接至區域網路站台</span><span class="sxs-lookup"><span data-stu-id="23aed-219">Connects to local network site</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="23aed-220">TestVNet1</span><span class="sxs-lookup"><span data-stu-id="23aed-220">TestVNet1</span></span> |<span data-ttu-id="23aed-221">TestVNet1</span><span class="sxs-lookup"><span data-stu-id="23aed-221">TestVNet1</span></span><br><span data-ttu-id="23aed-222">(10.11.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="23aed-222">(10.11.0.0/16)</span></span><br><span data-ttu-id="23aed-223">(10.12.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="23aed-223">(10.12.0.0/16)</span></span> |<span data-ttu-id="23aed-224">美國東部</span><span class="sxs-lookup"><span data-stu-id="23aed-224">East US</span></span> |<span data-ttu-id="23aed-225">VNet4Local</span><span class="sxs-lookup"><span data-stu-id="23aed-225">VNet4Local</span></span><br><span data-ttu-id="23aed-226">(10.41.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="23aed-226">(10.41.0.0/16)</span></span><br><span data-ttu-id="23aed-227">(10.42.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="23aed-227">(10.42.0.0/16)</span></span> |
| <span data-ttu-id="23aed-228">TestVNet4</span><span class="sxs-lookup"><span data-stu-id="23aed-228">TestVNet4</span></span> |<span data-ttu-id="23aed-229">TestVNet4</span><span class="sxs-lookup"><span data-stu-id="23aed-229">TestVNet4</span></span><br><span data-ttu-id="23aed-230">(10.41.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="23aed-230">(10.41.0.0/16)</span></span><br><span data-ttu-id="23aed-231">(10.42.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="23aed-231">(10.42.0.0/16)</span></span> |<span data-ttu-id="23aed-232">美國西部</span><span class="sxs-lookup"><span data-stu-id="23aed-232">West US</span></span> |<span data-ttu-id="23aed-233">VNet1Local</span><span class="sxs-lookup"><span data-stu-id="23aed-233">VNet1Local</span></span><br><span data-ttu-id="23aed-234">(10.11.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="23aed-234">(10.11.0.0/16)</span></span><br><span data-ttu-id="23aed-235">(10.12.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="23aed-235">(10.12.0.0/16)</span></span> |

1. <span data-ttu-id="23aed-236">在 Azure 入口網站中找出 TestVNet1。</span><span class="sxs-lookup"><span data-stu-id="23aed-236">Locate TestVNet1 in the Azure portal.</span></span> <span data-ttu-id="23aed-237">在刀鋒視窗的 [VPN 連線] 區段中，按一下 [閘道]。</span><span class="sxs-lookup"><span data-stu-id="23aed-237">In the **VPN connections** section of the blade, click **Gateway**.</span></span>

    ![沒有閘道](./media/vpn-gateway-howto-vnet-vnet-portal-classic/nogateway.png)
2. <span data-ttu-id="23aed-239">在 [新增 VPN 連線] 頁面上，選取 [站對站]。</span><span class="sxs-lookup"><span data-stu-id="23aed-239">On the **New VPN Connection** page, select **Site-to-Site**.</span></span>
3. <span data-ttu-id="23aed-240">按一下 [本機網站] 以開啟 [本機網站] 頁面，並且進行設定。</span><span class="sxs-lookup"><span data-stu-id="23aed-240">Click **Local site** to open the Local site page and configure the settings.</span></span>
4. <span data-ttu-id="23aed-241">在 [本機網站] 頁面上，為您的本機網站命名。</span><span class="sxs-lookup"><span data-stu-id="23aed-241">On the **Local site** page, name your local site.</span></span> <span data-ttu-id="23aed-242">在我們的範例中，我們將本機網站命名為 'VNet4Local'。</span><span class="sxs-lookup"><span data-stu-id="23aed-242">In our example, we name the local site 'VNet4Local'.</span></span>
5. <span data-ttu-id="23aed-243">針對 [VPN 閘道 IP 位址]，只要是有效的格式，您可以使用您想要的任何 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="23aed-243">For **VPN gateway IP address**, you can use any IP address that you want, as long as it's in a valid format.</span></span> <span data-ttu-id="23aed-244">一般而言，您會將實際的外部 IP 位址用於 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="23aed-244">Typically, you’d use the actual external IP address for a VPN device.</span></span> <span data-ttu-id="23aed-245">但是針對傳統 VNet 對 VNet 組態，您需使用指派給您 VNet 閘道的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="23aed-245">But, for a classic VNet-to-VNet configuration, you use the public IP address that is assigned to the gateway for your VNet.</span></span> <span data-ttu-id="23aed-246">由於您尚未建立虛擬網路閘道，因此您可以指定任何有效的公用 IP 位址作為預留位置。</span><span class="sxs-lookup"><span data-stu-id="23aed-246">Given that you’ve not yet created the virtual network gateway, you specify any valid public IP address as a placeholder.</span></span><br><span data-ttu-id="23aed-247">請勿將此欄位留白 - 這不是此組態的選擇性欄位。</span><span class="sxs-lookup"><span data-stu-id="23aed-247">Don't leave this blank - it's not optional for this configuration.</span></span> <span data-ttu-id="23aed-248">在稍後的步驟中，您將在 Azure 產生閘道之後，回到這些設定，並使用對應的虛擬網路閘道 IP 位址來進行設定。</span><span class="sxs-lookup"><span data-stu-id="23aed-248">In a later step, you go back into these settings and configure them with the corresponding virtual network gateway IP addresses once Azure generates it.</span></span>
6. <span data-ttu-id="23aed-249">針對 [用戶端位址空間]，使用其他 VNet 的位址空間。</span><span class="sxs-lookup"><span data-stu-id="23aed-249">For **Client Address Space**, use the address space of the other VNet.</span></span> <span data-ttu-id="23aed-250">請參閱您的計劃範例。</span><span class="sxs-lookup"><span data-stu-id="23aed-250">Refer to your planning example.</span></span> <span data-ttu-id="23aed-251">按一下 [確定] 來儲存設定，並且返回 [新增 VPN 連線] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="23aed-251">Click **OK** to save your settings and return back to the **New VPN Connection** blade.</span></span>

    ![本機網站](./media/vpn-gateway-howto-vnet-vnet-portal-classic/localsite.png)

## <span data-ttu-id="23aed-253"><a name="gw"></a>步驟 4 - 建立虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="23aed-253"><a name="gw"></a>Step 4 - Create the virtual network gateway</span></span>

<span data-ttu-id="23aed-254">每個虛擬網路都必須有虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="23aed-254">Each virtual network must have a virtual network gateway.</span></span> <span data-ttu-id="23aed-255">虛擬網路閘道會路由傳送流量並且加密。</span><span class="sxs-lookup"><span data-stu-id="23aed-255">The virtual network gateway routes and encrypts traffic.</span></span>

1. <span data-ttu-id="23aed-256">在 [新增 VPN 連線] 刀鋒視窗上，選取 [立即建立閘道] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="23aed-256">On the **New VPN Connection** blade, select the checkbox **Create gateway immediately**.</span></span>
2. <span data-ttu-id="23aed-257">按一下 [子網路、大小和路由類型]。</span><span class="sxs-lookup"><span data-stu-id="23aed-257">Click **Subnet, size and routing type**.</span></span> <span data-ttu-id="23aed-258">在 [閘道組態] 刀鋒視窗中，按一下 [子網路]。</span><span class="sxs-lookup"><span data-stu-id="23aed-258">On the **Gateway configuration** blade, click **Subnet**.</span></span>
3. <span data-ttu-id="23aed-259">閘道子網路名稱會自動填入必要名稱 'GatewaySubnet'。</span><span class="sxs-lookup"><span data-stu-id="23aed-259">The gateway subnet name is filled in automatically with the required name 'GatewaySubnet'.</span></span> <span data-ttu-id="23aed-260">[位址範圍] 包含配置給 VPN 閘道服務的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="23aed-260">The **Address range** contains the IP addresses that are allocated to the VPN gateway services.</span></span> <span data-ttu-id="23aed-261">某些組態允許閘道子網路 /29，但是最好是使用 /28 或 /27 以容納未來可能需要更多閘道服務 IP 位址的組態。</span><span class="sxs-lookup"><span data-stu-id="23aed-261">Some configurations allow a gateway subnet of /29, but it's best to use a /28 or /27 to accommodate future configurations that may require more IP addresses for the gateway services.</span></span> <span data-ttu-id="23aed-262">在我們的範例設定中，我們會使用 10.11.1.0/27。</span><span class="sxs-lookup"><span data-stu-id="23aed-262">In our example settings, we use 10.11.1.0/27.</span></span> <span data-ttu-id="23aed-263">調整位址空間，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="23aed-263">Adjust the address space, then click **OK**.</span></span>
4. <span data-ttu-id="23aed-264">設定**閘道大小**。</span><span class="sxs-lookup"><span data-stu-id="23aed-264">Configure the **Gateway Size**.</span></span> <span data-ttu-id="23aed-265">此設定表示[閘道 SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku)。</span><span class="sxs-lookup"><span data-stu-id="23aed-265">This setting refers to the [Gateway SKU](vpn-gateway-about-vpn-gateway-settings.md#gwsku).</span></span>
5. <span data-ttu-id="23aed-266">設定**路由類型**。</span><span class="sxs-lookup"><span data-stu-id="23aed-266">Configure the **Routing Type**.</span></span> <span data-ttu-id="23aed-267">此組態的路由類型必須是**動態**。</span><span class="sxs-lookup"><span data-stu-id="23aed-267">The routing type for this configuration must be **Dynamic**.</span></span> <span data-ttu-id="23aed-268">除非您卸除閘道並且建立一個新閘道，否則您無法在稍後變更路由類型。</span><span class="sxs-lookup"><span data-stu-id="23aed-268">You can't change the routing type later unless you tear down the gateway and create a new one.</span></span>
6. <span data-ttu-id="23aed-269">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="23aed-269">Click **OK**.</span></span>
7. <span data-ttu-id="23aed-270">在 [新增 VPN 連線] 刀鋒視窗中，按一下 [確定] 以開始建立虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="23aed-270">On the **New VPN Connection** blade, click **OK** to begin creating the virtual network gateway.</span></span> <span data-ttu-id="23aed-271">建立閘道通常可能需要 45 分鐘或更久，視選取的閘道 SKU 而定。</span><span class="sxs-lookup"><span data-stu-id="23aed-271">Creating a gateway can often take 45 minutes or more, depending on the selected gateway SKU.</span></span>

## <span data-ttu-id="23aed-272"><a name="vnet4settings"></a>步驟 5 - 進行 TestVNet4 設定</span><span class="sxs-lookup"><span data-stu-id="23aed-272"><a name="vnet4settings"></a>Step 5 - Configure TestVNet4 settings</span></span>

<span data-ttu-id="23aed-273">重複 [建立本機網站](#localsite) 和 [建立虛擬網路閘道](#gw) 的步驟以設定 TestVNet4，並且視需要取代值。</span><span class="sxs-lookup"><span data-stu-id="23aed-273">Repeat the steps to [Create a local site](#localsite) and [Create the virtual network gateway](#gw) to configure TestVNet4, substituting the values when necessary.</span></span> <span data-ttu-id="23aed-274">如果您執行這個操作作為練習，請使用[範例值](#vnetvalues)。</span><span class="sxs-lookup"><span data-stu-id="23aed-274">If you are doing this as an exercise, use the [Example values](#vnetvalues).</span></span>

## <span data-ttu-id="23aed-275"><a name="updatelocal"></a>步驟 6 - 更新本機網站</span><span class="sxs-lookup"><span data-stu-id="23aed-275"><a name="updatelocal"></a>Step 6 - Update the local sites</span></span>

<span data-ttu-id="23aed-276">為兩個 VNet 建立虛擬網路閘道之後，您必須調整本機網站 **VPN 閘道 IP 位址**值。</span><span class="sxs-lookup"><span data-stu-id="23aed-276">After your virtual network gateways have been created for both VNets, you must adjust the local sites **VPN gateway IP address** values.</span></span>

|<span data-ttu-id="23aed-277">VNet 名稱</span><span class="sxs-lookup"><span data-stu-id="23aed-277">VNet name</span></span>|<span data-ttu-id="23aed-278">已連線網站</span><span class="sxs-lookup"><span data-stu-id="23aed-278">Connected site</span></span>|<span data-ttu-id="23aed-279">閘道 IP 位址</span><span class="sxs-lookup"><span data-stu-id="23aed-279">Gateway IP address</span></span>|
|:--- |:--- |:--- |
|<span data-ttu-id="23aed-280">TestVNet1</span><span class="sxs-lookup"><span data-stu-id="23aed-280">TestVNet1</span></span>|<span data-ttu-id="23aed-281">VNet4Local</span><span class="sxs-lookup"><span data-stu-id="23aed-281">VNet4Local</span></span>|<span data-ttu-id="23aed-282">TestVNet4 的 VPN 閘道 IP 位址</span><span class="sxs-lookup"><span data-stu-id="23aed-282">VPN gateway IP address for TestVNet4</span></span>|
|<span data-ttu-id="23aed-283">TestVNet4</span><span class="sxs-lookup"><span data-stu-id="23aed-283">TestVNet4</span></span>|<span data-ttu-id="23aed-284">VNet1Local</span><span class="sxs-lookup"><span data-stu-id="23aed-284">VNet1Local</span></span>|<span data-ttu-id="23aed-285">TestVNet1 的 VPN 閘道 IP 位址</span><span class="sxs-lookup"><span data-stu-id="23aed-285">VPN gateway IP address for TestVNet1</span></span>|

### <a name="part-1---get-the-virtual-network-gateway-public-ip-address"></a><span data-ttu-id="23aed-286">第 1 部分 - 取得虛擬網路閘道公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="23aed-286">Part 1 - Get the virtual network gateway public IP address</span></span>

1. <span data-ttu-id="23aed-287">在 Azure 入口網站中找到虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="23aed-287">Locate your virtual network in the Azure portal.</span></span>
2. <span data-ttu-id="23aed-288">按一下以開啟 VNet [概觀] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="23aed-288">Click to open the VNet **Overview** blade.</span></span> <span data-ttu-id="23aed-289">在刀鋒視窗的 [VPN 連線] 中，您可以檢視虛擬網路閘道的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="23aed-289">On the blade, in **VPN connections**, you can view the IP address for your virtual network gateway.</span></span>

  ![公用 IP](./media/vpn-gateway-howto-vnet-vnet-portal-classic/publicIP.png)
3. <span data-ttu-id="23aed-291">複製 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="23aed-291">Copy the IP address.</span></span> <span data-ttu-id="23aed-292">您在下一節將會用到此位址。</span><span class="sxs-lookup"><span data-stu-id="23aed-292">You will use it in the next section.</span></span>
4. <span data-ttu-id="23aed-293">對 TestVNet4 重複執行這些步驟</span><span class="sxs-lookup"><span data-stu-id="23aed-293">Repeat these steps for TestVNet4</span></span>

### <a name="part-2---modify-the-local-sites"></a><span data-ttu-id="23aed-294">第 2 部分 - 修改本機網站</span><span class="sxs-lookup"><span data-stu-id="23aed-294">Part 2 - Modify the local sites</span></span>

1. <span data-ttu-id="23aed-295">在 Azure 入口網站中找到虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="23aed-295">Locate your virtual network in the Azure portal.</span></span>
2. <span data-ttu-id="23aed-296">在 VNet 的 [概觀] 刀鋒視窗中，按一下本機網站。</span><span class="sxs-lookup"><span data-stu-id="23aed-296">On the VNet **Overview** blade, click the local site.</span></span>

  ![建立本機網站](./media/vpn-gateway-howto-vnet-vnet-portal-classic/local.png)
3. <span data-ttu-id="23aed-298">在 [站對站 VPN 連線] 刀鋒視窗中，按一下您想要修改之本機網站的名稱。</span><span class="sxs-lookup"><span data-stu-id="23aed-298">On the **Site-to-Site VPN Connections** blade, click the name of the local site that you want to modify.</span></span>

  ![開啟本機網站](./media/vpn-gateway-howto-vnet-vnet-portal-classic/openlocal.png)
4. <span data-ttu-id="23aed-300">按一下您想要修改的 [本機網站]。</span><span class="sxs-lookup"><span data-stu-id="23aed-300">Click the **Local site** that you want to modify.</span></span>

  ![修改網站](./media/vpn-gateway-howto-vnet-vnet-portal-classic/connections.png)
5. <span data-ttu-id="23aed-302">更新 [VPN 閘道 IP 位址]，然後按一下 [確定] 以儲存設定。</span><span class="sxs-lookup"><span data-stu-id="23aed-302">Update the **VPN gateway IP address** and click **OK** to save the settings.</span></span>

  ![閘道 IP](./media/vpn-gateway-howto-vnet-vnet-portal-classic/gwupdate.png)
6. <span data-ttu-id="23aed-304">關閉其他刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="23aed-304">Close the other blades.</span></span>
7. <span data-ttu-id="23aed-305">對 TestVNet4 重複執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="23aed-305">Repeat these steps for TestVNet4.</span></span>

## <span data-ttu-id="23aed-306"><a name="getvalues"></a>步驟 7 - 從網路組態檔擷取值</span><span class="sxs-lookup"><span data-stu-id="23aed-306"><a name="getvalues"></a>Step 7 - Retrieve values from the network configuration file</span></span>

<span data-ttu-id="23aed-307">當您在 Azure 入口網站中建立傳統 VNet 時，您所檢視的名稱不是在 PowerShell 中使用的完整名稱。</span><span class="sxs-lookup"><span data-stu-id="23aed-307">When you create classic VNets in the Azure portal, the name that you view is not the full name that you use for PowerShell.</span></span> <span data-ttu-id="23aed-308">例如，在入口網站中名稱顯示為 **TestVNet1** 的 VNet，在網路組態檔中的名稱可能更長。</span><span class="sxs-lookup"><span data-stu-id="23aed-308">For example, a VNet that appears to be named **TestVNet1** in the portal, may have a much longer name in the network configuration file.</span></span> <span data-ttu-id="23aed-309">名稱可能如下︰**Group ClassicRG TestVNet1**。</span><span class="sxs-lookup"><span data-stu-id="23aed-309">The name might look something like: **Group ClassicRG TestVNet1**.</span></span> <span data-ttu-id="23aed-310">當您建立連線時，務必使用您在網路組態檔中看到的值。</span><span class="sxs-lookup"><span data-stu-id="23aed-310">When you create your connections, it's important to use the values that you see in the network configuration file.</span></span>

<span data-ttu-id="23aed-311">在下列步驟中，您將會連線到您的 Azure 帳戶，並且下載及檢視網路組態檔，以取得連線的必要值。</span><span class="sxs-lookup"><span data-stu-id="23aed-311">In the following steps, you will connect to your Azure account and download and view the network configuration file to obtain the values that are required for your connections.</span></span>

1. <span data-ttu-id="23aed-312">下載並安裝最新版的 Azure 服務管理 (SM) PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="23aed-312">Download and install the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="23aed-313">如需詳細資訊，請參閱 [如何安裝及設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="23aed-313">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

2. <span data-ttu-id="23aed-314">以提高的權限開啟 PowerShell 主控台並連接到您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="23aed-314">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="23aed-315">使用下列範例來協助您連接：</span><span class="sxs-lookup"><span data-stu-id="23aed-315">Use the following example to help you connect:</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

  <span data-ttu-id="23aed-316">檢查帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="23aed-316">Check the subscriptions for the account.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

  <span data-ttu-id="23aed-317">如果您有多個訂用帳戶，請選取您要使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="23aed-317">If you have more than one subscription, select the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
  ```

  <span data-ttu-id="23aed-318">接下來，使用下列 Cmdlet，將您的 Azure 訂用帳戶新增到 PowerShell，以供傳統部署模型使用。</span><span class="sxs-lookup"><span data-stu-id="23aed-318">Next, use the following cmdlet to add your Azure subscription to PowerShell for the classic deployment model.</span></span>

  ```powershell
  Add-AzureAccount
  ```
3. <span data-ttu-id="23aed-319">匯出並檢視網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="23aed-319">Export and view the network configuration file.</span></span> <span data-ttu-id="23aed-320">在您的電腦上建立目錄，然後將網路組態檔匯出到該目錄。</span><span class="sxs-lookup"><span data-stu-id="23aed-320">Create a directory on your computer and then export the network configuration file to the directory.</span></span> <span data-ttu-id="23aed-321">在此範例中，會將網路組態檔匯出到 **C:\AzureNet**。</span><span class="sxs-lookup"><span data-stu-id="23aed-321">In this example, the network configuration file is exported to **C:\AzureNet**.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
4. <span data-ttu-id="23aed-322">使用文字編輯器開啟檔案，並且檢視 VNet 和網站的名稱。</span><span class="sxs-lookup"><span data-stu-id="23aed-322">Open the file with a text editor and view the names for your VNets and sites.</span></span> <span data-ttu-id="23aed-323">這些名稱是您建立連線時使用的名稱。</span><span class="sxs-lookup"><span data-stu-id="23aed-323">These will be the name you use when you create your connections.</span></span><br><span data-ttu-id="23aed-324">VNet 名稱會列為 **VirtualNetworkSite name =**</span><span class="sxs-lookup"><span data-stu-id="23aed-324">VNet names are listed as **VirtualNetworkSite name =**</span></span><br><span data-ttu-id="23aed-325">網站名稱會列為 **LocalNetworkSiteRef name =**</span><span class="sxs-lookup"><span data-stu-id="23aed-325">Site names are listed as **LocalNetworkSiteRef name =**</span></span>

## <span data-ttu-id="23aed-326"><a name="createconnections"></a>步驟 8 - 建立 VPN 閘道連線</span><span class="sxs-lookup"><span data-stu-id="23aed-326"><a name="createconnections"></a>Step 8 - Create the VPN gateway connections</span></span>

<span data-ttu-id="23aed-327">當所有先前的步驟都已完成時，您可以設定 IPsec/IKE 預先共用金鑰並建立連線。</span><span class="sxs-lookup"><span data-stu-id="23aed-327">When all the previous steps have been completed, you can set the IPsec/IKE pre-shared keys and create the connection.</span></span> <span data-ttu-id="23aed-328">這組步驟會使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="23aed-328">This set of steps uses PowerShell.</span></span> <span data-ttu-id="23aed-329">無法在 Azure 入口網站中設定傳統部署模型的 VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="23aed-329">VNet-to-VNet connections for the classic deployment model cannot be configured in the Azure portal.</span></span>

<span data-ttu-id="23aed-330">在這些範例中，請注意，共用金鑰是完全相同的。</span><span class="sxs-lookup"><span data-stu-id="23aed-330">In the examples, notice that the shared key is exactly the same.</span></span> <span data-ttu-id="23aed-331">共用金鑰必須一律相符。</span><span class="sxs-lookup"><span data-stu-id="23aed-331">The shared key must always match.</span></span> <span data-ttu-id="23aed-332">請務必使用 VNet 和區域網路網站的確切名稱，取代這些範例中的值。</span><span class="sxs-lookup"><span data-stu-id="23aed-332">Be sure to replace the values in these examples with the exact names for your VNets and Local Network Sites.</span></span>

1. <span data-ttu-id="23aed-333">建立 TestVNet1 至 TestVNet4 的連線。</span><span class="sxs-lookup"><span data-stu-id="23aed-333">Create the TestVNet1 to TestVNet4 connection.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet1' `
  -LocalNetworkSiteName '17BE5E2C_VNet4Local' -SharedKey A1b2C3D4
  ```
2. <span data-ttu-id="23aed-334">建立 TestVNet4 至 TestVNet1 的連線。</span><span class="sxs-lookup"><span data-stu-id="23aed-334">Create the TestVNet4 to TestVNet1 connection.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName 'Group ClassicRG TestVNet4' `
  -LocalNetworkSiteName 'F7F7BFC7_VNet1Local' -SharedKey A1b2C3D4
  ```
3. <span data-ttu-id="23aed-335">等待連線初始化。</span><span class="sxs-lookup"><span data-stu-id="23aed-335">Wait for the connections to initialize.</span></span> <span data-ttu-id="23aed-336">一旦閘道初始化，其狀態為「成功」。</span><span class="sxs-lookup"><span data-stu-id="23aed-336">Once the gateway has initialized, the Status is 'Successful'.</span></span>

  ```
  Error          :
  HttpStatusCode : OK
  Id             :
  Status         : Successful
  RequestId      :
  StatusCode     : OK
  ```

## <span data-ttu-id="23aed-337"><a name="faq"></a>傳統 VNet 的 VNet 對 VNet 考量</span><span class="sxs-lookup"><span data-stu-id="23aed-337"><a name="faq"></a>VNet-to-VNet considerations for classic VNets</span></span>
* <span data-ttu-id="23aed-338">虛擬網路可位於相同或不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="23aed-338">The virtual networks can be in the same or different subscriptions.</span></span>
* <span data-ttu-id="23aed-339">虛擬網路可位於相同或不同的 Azure 區域 (位置)。</span><span class="sxs-lookup"><span data-stu-id="23aed-339">The virtual networks can be in the same or different Azure regions (locations).</span></span>
* <span data-ttu-id="23aed-340">即使虛擬網路連接在一起，雲端服務或負載平衡端點也無法跨虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="23aed-340">A cloud service or a load balancing endpoint can't span across virtual networks, even if they are connected together.</span></span>
* <span data-ttu-id="23aed-341">將多個虛擬網路連接在一起並不需要任何 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="23aed-341">Connecting multiple virtual networks together doesn't require any VPN devices.</span></span>
* <span data-ttu-id="23aed-342">VNet 對 VNet 支援連接 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="23aed-342">VNet-to-VNet supports connecting Azure Virtual Networks.</span></span> <span data-ttu-id="23aed-343">它不支援連接未部署到虛擬網路中的虛擬機器或雲端服務。</span><span class="sxs-lookup"><span data-stu-id="23aed-343">It does not support connecting virtual machines or cloud services that are not deployed to a virtual network.</span></span>
* <span data-ttu-id="23aed-344">VNet 對 VNet 需要動態路由閘道。</span><span class="sxs-lookup"><span data-stu-id="23aed-344">VNet-to-VNet requires dynamic routing gateways.</span></span> <span data-ttu-id="23aed-345">不支援 Azure 靜態路由閘道。</span><span class="sxs-lookup"><span data-stu-id="23aed-345">Azure static routing gateways are not supported.</span></span>
* <span data-ttu-id="23aed-346">虛擬網路連線能力可以與多站台 VPN 同時使用。</span><span class="sxs-lookup"><span data-stu-id="23aed-346">Virtual network connectivity can be used simultaneously with multi-site VPNs.</span></span> <span data-ttu-id="23aed-347">一個虛擬網路 VPN 閘道最多可以有 10 條 VPN 通道連接至其他虛擬網路或內部部署站台。</span><span class="sxs-lookup"><span data-stu-id="23aed-347">There is a maximum of 10 VPN tunnels for a virtual network VPN gateway connecting to either other virtual networks, or on-premises sites.</span></span>
* <span data-ttu-id="23aed-348">虛擬網路與內部部署區域網路網站的位址空間不得重疊。</span><span class="sxs-lookup"><span data-stu-id="23aed-348">The address spaces of the virtual networks and on-premises local network sites must not overlap.</span></span> <span data-ttu-id="23aed-349">位址空間重疊會導致建立虛擬網路或上傳 netcfg 組態檔失敗。</span><span class="sxs-lookup"><span data-stu-id="23aed-349">Overlapping address spaces will cause the creation of virtual networks or uploading netcfg configuration files to fail.</span></span>
* <span data-ttu-id="23aed-350">不支援成對虛擬網路之間的備援通道。</span><span class="sxs-lookup"><span data-stu-id="23aed-350">Redundant tunnels between a pair of virtual networks are not supported.</span></span>
* <span data-ttu-id="23aed-351">VNet 的所有 VPN 通道 (包括 P2S VPN) 在 Azure 中皆共用 VPN 閘道的可用頻寬及相同的 VPN 閘道執行時間 SLA。</span><span class="sxs-lookup"><span data-stu-id="23aed-351">All VPN tunnels for the VNet, including P2S VPNs, share the available bandwidth for the VPN gateway, and the same VPN gateway uptime SLA in Azure.</span></span>
* <span data-ttu-id="23aed-352">VNet 對 VNet 流量會經過 Azure 的骨幹。</span><span class="sxs-lookup"><span data-stu-id="23aed-352">VNet-to-VNet traffic travels across the Azure backbone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="23aed-353">後續步驟</span><span class="sxs-lookup"><span data-stu-id="23aed-353">Next steps</span></span>
<span data-ttu-id="23aed-354">確認您的連線。</span><span class="sxs-lookup"><span data-stu-id="23aed-354">Verify your connections.</span></span> <span data-ttu-id="23aed-355">[確認 VPN 閘道連線](vpn-gateway-verify-connection-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="23aed-355">See [Verify a VPN Gateway connection](vpn-gateway-verify-connection-resource-manager.md).</span></span>
