---
title: "連接傳統虛擬網路 tooAzure 資源管理員 Vnet： 入口網站 |Microsoft 文件"
description: "深入了解如何 toocreate 傳統 Vnet 和 VPN 閘道與 hello 入口網站所使用的資源管理員 Vnet 之間的 VPN 連線"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 5a90498c-4520-4bd3-a833-ad85924ecaf9
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: bef63b4e829335b2e1a9434a35ebfe33b4fd7373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-hello-portal"></a><span data-ttu-id="b8eea-103">若要從不同的部署模型使用 hello 入口網站連接虛擬網路</span><span class="sxs-lookup"><span data-stu-id="b8eea-103">Connect virtual networks from different deployment models using hello portal</span></span>

<span data-ttu-id="b8eea-104">本文章將示範如何 tooconnect 傳統 Vnet tooResource 管理員 Vnet tooallow hello 位於彼此的 hello 不同的部署模型 toocommunicate 中的資源。</span><span class="sxs-lookup"><span data-stu-id="b8eea-104">This article shows you how tooconnect classic VNets tooResource Manager VNets tooallow hello resources located in hello separate deployment models toocommunicate with each other.</span></span> <span data-ttu-id="b8eea-105">這篇文章中的 hello 步驟主要使用 hello Azure 入口網站，但您也可以建立使用 hello PowerShell hello 文章從此清單中選取此設定。</span><span class="sxs-lookup"><span data-stu-id="b8eea-105">hello steps in this article primarily use hello Azure portal, but you can also create this configuration using hello PowerShell by selecting hello article from this list.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b8eea-106">入口網站</span><span class="sxs-lookup"><span data-stu-id="b8eea-106">Portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="b8eea-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b8eea-107">PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

<span data-ttu-id="b8eea-108">連接傳統的 VNet tooa 資源管理員 VNet 是類似 tooconnecting VNet tooan 在內部部署站台位置。</span><span class="sxs-lookup"><span data-stu-id="b8eea-108">Connecting a classic VNet tooa Resource Manager VNet is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="b8eea-109">這兩種連線類型使用的 VPN 閘道 tooprovide 採用 IPsec/IKE 的安全通道。</span><span class="sxs-lookup"><span data-stu-id="b8eea-109">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="b8eea-110">您可以在不同訂用帳戶和不同區域中的 VNet 之間建立連線。</span><span class="sxs-lookup"><span data-stu-id="b8eea-110">You can create a connection between VNets that are in different subscriptions and in different regions.</span></span> <span data-ttu-id="b8eea-111">只要 hello 閘道設定使用動態或路由為基礎，您也可以連接到已連線 tooon 內部部署網路的 Vnet。</span><span class="sxs-lookup"><span data-stu-id="b8eea-111">You can also connect VNets that already have connections tooon-premises networks, as long as hello gateway that they have been configured with is dynamic or route-based.</span></span> <span data-ttu-id="b8eea-112">如需 VNet 對 VNet 連線的詳細資訊，請參閱 hello [VNet 對 VNet 常見問題集](#faq)hello 本文結尾處。</span><span class="sxs-lookup"><span data-stu-id="b8eea-112">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span> 

<span data-ttu-id="b8eea-113">如果您的 Vnet 中 hello 相同區域中，您可能會想 tooinstead 考慮它們使用對等互連的 VNet 連接。</span><span class="sxs-lookup"><span data-stu-id="b8eea-113">If your VNets are in hello same region, you may want tooinstead consider connecting them using VNet Peering.</span></span> <span data-ttu-id="b8eea-114">VNet 對等互連不會使用 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="b8eea-114">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="b8eea-115">如需詳細資訊，請參閱 [VNet 對等互連](../virtual-network/virtual-network-peering-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="b8eea-115">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="b8eea-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="b8eea-116">Prerequisites</span></span>

* <span data-ttu-id="b8eea-117">這些步驟假設已建立兩個 VNet。</span><span class="sxs-lookup"><span data-stu-id="b8eea-117">These steps assume that both VNets have already been created.</span></span> <span data-ttu-id="b8eea-118">如果您使用這份文件做為練習，而且不需要 Vnet，有連結 hello 步驟 toohelp 在您建立它們。</span><span class="sxs-lookup"><span data-stu-id="b8eea-118">If you are using this article as an exercise and don't have VNets, there are links in hello steps toohelp you create them.</span></span>
* <span data-ttu-id="b8eea-119">請確認個 Vnet 不會彼此重疊的 hello hello 位址範圍，或其他連線閘道可能連接到該 hello 與任何 hello 的重疊範圍。</span><span class="sxs-lookup"><span data-stu-id="b8eea-119">Verify that hello address ranges for hello VNets do not overlap with each other, or overlap with any of hello ranges for other connections that hello gateways may be connected to.</span></span>
* <span data-ttu-id="b8eea-120">安裝資源管理員和服務管理 （傳統） 的 hello 最新版的 PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b8eea-120">Install hello latest PowerShell cmdlets for both Resource Manager and Service Management (classic).</span></span> <span data-ttu-id="b8eea-121">在本文中，我們將使用 hello Azure 入口網站和 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="b8eea-121">In this article, we use both hello Azure portal and PowerShell.</span></span> <span data-ttu-id="b8eea-122">PowerShell 是必要的 toocreate hello 連線從傳統 VNet toohello hello 資源管理員 VNet。</span><span class="sxs-lookup"><span data-stu-id="b8eea-122">PowerShell is required toocreate hello connection from hello classic VNet toohello Resource Manager VNet.</span></span> <span data-ttu-id="b8eea-123">如需詳細資訊，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="b8eea-123">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

### <span data-ttu-id="b8eea-124"><a name="values"></a>設定範例</span><span class="sxs-lookup"><span data-stu-id="b8eea-124"><a name="values"></a>Example settings</span></span>

<span data-ttu-id="b8eea-125">您可以使用這些值 toocreate 測試環境中，或參閱 toothem toobetter 了解這篇文章中的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="b8eea-125">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

<span data-ttu-id="b8eea-126">**傳統 VNet**</span><span class="sxs-lookup"><span data-stu-id="b8eea-126">**Classic VNet**</span></span>

<span data-ttu-id="b8eea-127">VNet 名稱 = ClassicVNet </span><span class="sxs-lookup"><span data-stu-id="b8eea-127">VNet name = ClassicVNet</span></span> <br>
<span data-ttu-id="b8eea-128">位址空間 = 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="b8eea-128">Address space = 10.0.0.0/24</span></span> <br>
<span data-ttu-id="b8eea-129">子網路 1 = 10.0.0.0/27</span><span class="sxs-lookup"><span data-stu-id="b8eea-129">Subnet-1 = 10.0.0.0/27</span></span> <br>
<span data-ttu-id="b8eea-130">資源群組 = ClassicRG</span><span class="sxs-lookup"><span data-stu-id="b8eea-130">Resource Group = ClassicRG</span></span> <br>
<span data-ttu-id="b8eea-131">位置 = West US</span><span class="sxs-lookup"><span data-stu-id="b8eea-131">Location = West US</span></span> <br>
<span data-ttu-id="b8eea-132">GatewaySubnet = 10.0.0.32/28</span><span class="sxs-lookup"><span data-stu-id="b8eea-132">GatewaySubnet = 10.0.0.32/28</span></span> <br>
<span data-ttu-id="b8eea-133">本機站台 = RMVNetLocal</span><span class="sxs-lookup"><span data-stu-id="b8eea-133">Local site = RMVNetLocal</span></span> <br>

<span data-ttu-id="b8eea-134">**Resource Manager VNet**</span><span class="sxs-lookup"><span data-stu-id="b8eea-134">**Resource Manager VNet**</span></span>

<span data-ttu-id="b8eea-135">VNet 名稱 = RMVNet </span><span class="sxs-lookup"><span data-stu-id="b8eea-135">VNet name = RMVNet</span></span> <br>
<span data-ttu-id="b8eea-136">位址空間 = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="b8eea-136">Address space = 192.168.0.0/16</span></span> <br>
<span data-ttu-id="b8eea-137">子網路 1 = 192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="b8eea-137">Subnet-1 = 192.168.1.0/24</span></span> <br>
<span data-ttu-id="b8eea-138">GatewaySubnet = 192.168.0.0/26</span><span class="sxs-lookup"><span data-stu-id="b8eea-138">GatewaySubnet = 192.168.0.0/26</span></span> <br>
<span data-ttu-id="b8eea-139">資源群組 = RG1</span><span class="sxs-lookup"><span data-stu-id="b8eea-139">Resource Group = RG1</span></span> <br>
<span data-ttu-id="b8eea-140">位置 = 美國東部</span><span class="sxs-lookup"><span data-stu-id="b8eea-140">Location = East US</span></span> <br>
<span data-ttu-id="b8eea-141">虛擬網路閘道名稱 = RMGateway</span><span class="sxs-lookup"><span data-stu-id="b8eea-141">Virtual network gateway name = RMGateway</span></span> <br>
<span data-ttu-id="b8eea-142">閘道類型 = VPN</span><span class="sxs-lookup"><span data-stu-id="b8eea-142">Gateway type = VPN</span></span> <br>
<span data-ttu-id="b8eea-143">VPN 類型 = 路由式</span><span class="sxs-lookup"><span data-stu-id="b8eea-143">VPN type = Route-based</span></span> <br>
<span data-ttu-id="b8eea-144">閘道公用 IP 位址名稱 = rmgwpip</span><span class="sxs-lookup"><span data-stu-id="b8eea-144">Gateway Public IP address name = rmgwpip</span></span> <br>
<span data-ttu-id="b8eea-145">區域網路閘道 = ClassicVNetLocal</span><span class="sxs-lookup"><span data-stu-id="b8eea-145">Local network gateway = ClassicVNetLocal</span></span> <br>
<span data-ttu-id="b8eea-146">連線名稱 = RMtoClassic</span><span class="sxs-lookup"><span data-stu-id="b8eea-146">Connection name = RMtoClassic</span></span>

### <a name="connection-overview"></a><span data-ttu-id="b8eea-147">連線概觀</span><span class="sxs-lookup"><span data-stu-id="b8eea-147">Connection overview</span></span>

<span data-ttu-id="b8eea-148">此組態中，您建立 VPN 閘道連線透過 hello 虛擬網路之間的 IPsec/IKE VPN 通道。</span><span class="sxs-lookup"><span data-stu-id="b8eea-148">For this configuration, you create a VPN gateway connection over an IPsec/IKE VPN tunnel between hello virtual networks.</span></span> <span data-ttu-id="b8eea-149">請確定沒有任何 VNet 範圍重疊彼此，或與任何 hello 所連接的區域網路。</span><span class="sxs-lookup"><span data-stu-id="b8eea-149">Make sure that none of your VNet ranges overlap with each other, or with any of hello local networks that they connect to.</span></span>

<span data-ttu-id="b8eea-150">hello 下表顯示 hello 範例 Vnet 和本機站台所定義之範例：</span><span class="sxs-lookup"><span data-stu-id="b8eea-150">hello following table shows an example of how hello example VNets and local sites are defined:</span></span>

| <span data-ttu-id="b8eea-151">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="b8eea-151">Virtual Network</span></span> | <span data-ttu-id="b8eea-152">位址空間</span><span class="sxs-lookup"><span data-stu-id="b8eea-152">Address Space</span></span> | <span data-ttu-id="b8eea-153">區域</span><span class="sxs-lookup"><span data-stu-id="b8eea-153">Region</span></span> | <span data-ttu-id="b8eea-154">Toolocal 網路站台連線</span><span class="sxs-lookup"><span data-stu-id="b8eea-154">Connects toolocal network site</span></span> |
|:--- |:--- |:--- |:--- |
| <span data-ttu-id="b8eea-155">ClassicVNet</span><span class="sxs-lookup"><span data-stu-id="b8eea-155">ClassicVNet</span></span> |<span data-ttu-id="b8eea-156">(10.0.0.0/24)</span><span class="sxs-lookup"><span data-stu-id="b8eea-156">(10.0.0.0/24)</span></span> |<span data-ttu-id="b8eea-157">美國西部</span><span class="sxs-lookup"><span data-stu-id="b8eea-157">West US</span></span> | <span data-ttu-id="b8eea-158">RMVNetLocal (192.168.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="b8eea-158">RMVNetLocal (192.168.0.0/16)</span></span> |
| <span data-ttu-id="b8eea-159">RMVNet</span><span class="sxs-lookup"><span data-stu-id="b8eea-159">RMVNet</span></span> | <span data-ttu-id="b8eea-160">(192.168.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="b8eea-160">(192.168.0.0/16)</span></span> |<span data-ttu-id="b8eea-161">美國東部</span><span class="sxs-lookup"><span data-stu-id="b8eea-161">East US</span></span> |<span data-ttu-id="b8eea-162">ClassicVNetLocal (10.0.0.0/24)</span><span class="sxs-lookup"><span data-stu-id="b8eea-162">ClassicVNetLocal (10.0.0.0/24)</span></span> |

## <span data-ttu-id="b8eea-163"><a name="classicvnet"></a>1.設定 hello 傳統的 VNet 設定</span><span class="sxs-lookup"><span data-stu-id="b8eea-163"><a name="classicvnet"></a>1. Configure hello classic VNet settings</span></span>

<span data-ttu-id="b8eea-164">在本節中，您會建立 hello 區域網路 （本機站台） 和傳統 VNet 的 hello 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="b8eea-164">In this section, you create hello local network (local site) and hello virtual network gateway for your classic VNet.</span></span> <span data-ttu-id="b8eea-165">如果您不需要傳統的 VNet，且正在執行這些步驟，做為練習，您可以使用來建立 VNet[本文](../virtual-network/virtual-networks-create-vnet-classic-pportal.md)和 hello[範例](#values)上述的設定值。</span><span class="sxs-lookup"><span data-stu-id="b8eea-165">If you don't have a classic VNet and are running these steps as an exercise, you can create a VNet by using [this article](../virtual-network/virtual-networks-create-vnet-classic-pportal.md) and hello [Example](#values) settings values from above.</span></span>

<span data-ttu-id="b8eea-166">當使用 hello 入口 toocreate 傳統的虛擬網路時，您必須使用下列步驟，否則 hello 選項 toocreate 傳統的虛擬網路不會出現的 hello 來巡覽 toohello 虛擬網路 刀鋒視窗：</span><span class="sxs-lookup"><span data-stu-id="b8eea-166">When using hello portal toocreate a classic virtual network, you must navigate toohello virtual network blade by using hello following steps, otherwise hello option toocreate a classic virtual network does not appear:</span></span>

1. <span data-ttu-id="b8eea-167">按一下 hello '+' tooopen hello 'New' 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b8eea-167">Click hello '+' tooopen hello 'New' blade.</span></span>
2. <span data-ttu-id="b8eea-168">Hello '搜尋 hello marketplace' 欄位中，輸入 [虛擬網路]。</span><span class="sxs-lookup"><span data-stu-id="b8eea-168">In hello 'Search hello marketplace' field, type 'Virtual Network'.</span></span> <span data-ttu-id="b8eea-169">如果相反地，選取 網路功能-> 虛擬網路，則不會收到 hello 選項 toocreate 傳統的 VNet。</span><span class="sxs-lookup"><span data-stu-id="b8eea-169">If you instead, select Networking -> Virtual Network, you will not get hello option toocreate a classic VNet.</span></span>
3. <span data-ttu-id="b8eea-170">傳回清單中的 hello 從找出 虛擬網路，然後按一下 tooopen hello 虛擬網路 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b8eea-170">Locate 'Virtual Network' from hello returned list and click it tooopen hello Virtual Network blade.</span></span> 
4. <span data-ttu-id="b8eea-171">Hello 虛擬網路] 刀鋒視窗中，選取 [傳統' toocreate 傳統的 VNet。</span><span class="sxs-lookup"><span data-stu-id="b8eea-171">On hello virtual network blade, select 'Classic' toocreate a classic VNet.</span></span> 

<span data-ttu-id="b8eea-172">如果您已經有 VPN 閘道的 VNet，請確認該 hello 閘道，而是動態。</span><span class="sxs-lookup"><span data-stu-id="b8eea-172">If you already have a VNet with a VPN gateway, verify that hello gateway is Dynamic.</span></span> <span data-ttu-id="b8eea-173">如果是靜態，您必須先刪除 hello VPN 閘道，然後繼續進行。</span><span class="sxs-lookup"><span data-stu-id="b8eea-173">If it's Static, you must first delete hello VPN gateway, then proceed.</span></span>

<span data-ttu-id="b8eea-174">已提供螢幕擷取畫面做為範例。</span><span class="sxs-lookup"><span data-stu-id="b8eea-174">Screenshots are provided as examples.</span></span> <span data-ttu-id="b8eea-175">是確定 tooreplace hello 值，以您自己，或使用 hello[範例](#values)值。</span><span class="sxs-lookup"><span data-stu-id="b8eea-175">Be sure tooreplace hello values with your own, or use hello [Example](#values) values.</span></span>

### <a name="part-1---configure-hello-local-site"></a><span data-ttu-id="b8eea-176">第 1 部-設定 hello 本機站台</span><span class="sxs-lookup"><span data-stu-id="b8eea-176">Part 1 - Configure hello local site</span></span>

<span data-ttu-id="b8eea-177">開啟 hello [Azure 入口網站](https://ms.portal.azure.com)並以您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="b8eea-177">Open hello [Azure portal](https://ms.portal.azure.com) and sign in with your Azure account.</span></span>

1. <span data-ttu-id="b8eea-178">瀏覽過**所有資源**並找出 hello **ClassicVNet** hello 清單中。</span><span class="sxs-lookup"><span data-stu-id="b8eea-178">Navigate too**All resources** and locate hello **ClassicVNet** in hello list.</span></span>
2. <span data-ttu-id="b8eea-179">在 hello**概觀**刀鋒視窗中的，在 hello **VPN 連線**區段中，按一下 hello**閘道**圖形 toocreate 閘道。</span><span class="sxs-lookup"><span data-stu-id="b8eea-179">On hello **Overview** blade, in hello **VPN connections** section, click hello **Gateway** graphic toocreate a gateway.</span></span>

    <span data-ttu-id="b8eea-180">![設定 VPN 閘道](./media/vpn-gateway-connect-different-deployment-models-portal/gatewaygraphic.png "設定 VPN 閘道")</span><span class="sxs-lookup"><span data-stu-id="b8eea-180">![Configure a VPN gateway](./media/vpn-gateway-connect-different-deployment-models-portal/gatewaygraphic.png "Configure a VPN gateway")</span></span>
3. <span data-ttu-id="b8eea-181">在 hello**新的 VPN 連線**刀鋒視窗中，針對**連線類型**，選取**站對站**。</span><span class="sxs-lookup"><span data-stu-id="b8eea-181">On hello **New VPN Connection** blade, for **Connection type**, select **Site-to-site**.</span></span>
4. <span data-ttu-id="b8eea-182">針對 [本機站台]，按一下 [設定必要設定]。</span><span class="sxs-lookup"><span data-stu-id="b8eea-182">For **Local site**, click **Configure required settings**.</span></span> <span data-ttu-id="b8eea-183">這會開啟 hello**本機站台**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b8eea-183">This opens hello **Local site** blade.</span></span>
5. <span data-ttu-id="b8eea-184">在 hello**本機站台**刀鋒視窗中，建立名稱 toorefer toohello 資源管理員的 VNet。</span><span class="sxs-lookup"><span data-stu-id="b8eea-184">On hello **Local site** blade, create a name toorefer toohello Resource Manager VNet.</span></span> <span data-ttu-id="b8eea-185">例如，'RMVNetLocal'。</span><span class="sxs-lookup"><span data-stu-id="b8eea-185">For example, 'RMVNetLocal'.</span></span>
6. <span data-ttu-id="b8eea-186">如果 hello 資源管理員 VNet 的 hello VPN 閘道已經有公用 IP 位址，則將 hello 值用於 hello **VPN 閘道 IP 位址**欄位。</span><span class="sxs-lookup"><span data-stu-id="b8eea-186">If hello VPN gateway for hello Resource Manager VNet already has a Public IP address, use hello value for hello **VPN gateway IP address** field.</span></span> <span data-ttu-id="b8eea-187">如果您要執行這些步驟作為練習，或者您的 Resource Manager VNet 還沒有虛擬網路閘道，您可以自行設定預留位置 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8eea-187">If you are doing these steps as an exercise, or don't yet have a virtual network gateway for your Resource Manager VNet, you can make up a placeholder IP address.</span></span> <span data-ttu-id="b8eea-188">請確定 hello 預留位置 IP 位址使用有效的格式。</span><span class="sxs-lookup"><span data-stu-id="b8eea-188">Make sure that hello placeholder IP address uses a valid format.</span></span> <span data-ttu-id="b8eea-189">更新版本中，您可以取代 hello 預留位置 IP 位址以 hello hello 資源管理員虛擬網路閘道的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8eea-189">Later, you replace hello placeholder IP address with hello Public IP address of hello Resource Manager virtual network gateway.</span></span>
7. <span data-ttu-id="b8eea-190">如**用戶端的位址空間**，hello 值用於 hello hello 資源管理員 VNet 的虛擬網路 IP 位址空間。</span><span class="sxs-lookup"><span data-stu-id="b8eea-190">For **Client Address Space**, use hello values for hello virtual network IP address spaces for hello Resource Manager VNet.</span></span> <span data-ttu-id="b8eea-191">這項設定是使用的 toospecify hello 位址空間 tooroute toohello 資源管理員虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b8eea-191">This setting is used toospecify hello address spaces tooroute toohello Resource Manager virtual network.</span></span>
8. <span data-ttu-id="b8eea-192">按一下**確定**toosave hello 值，並傳回 toohello**新的 VPN 連線**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b8eea-192">Click **OK** toosave hello values and return toohello **New VPN Connection** blade.</span></span>

### <a name="part-2---create-hello-virtual-network-gateway"></a><span data-ttu-id="b8eea-193">第 2 部-建立 hello 虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="b8eea-193">Part 2 - Create hello virtual network gateway</span></span>

1. <span data-ttu-id="b8eea-194">在 hello**新的 VPN 連線**刀鋒視窗中，選取 hello**立即建立閘道**核取方塊，按一下 **選擇性閘道組態**tooopen hello **閘道組態**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b8eea-194">On hello **New VPN Connection** blade, select hello **Create gateway immediately** checkbox and click **Optional gateway configuration** tooopen hello **Gateway configuration** blade.</span></span> 

    <span data-ttu-id="b8eea-195">![開啟 [閘道組態] 刀鋒視窗](./media/vpn-gateway-connect-different-deployment-models-portal/optionalgatewayconfiguration.png "開啟 [閘道組態] 刀鋒視窗")</span><span class="sxs-lookup"><span data-stu-id="b8eea-195">![Open gateway configuration blade](./media/vpn-gateway-connect-different-deployment-models-portal/optionalgatewayconfiguration.png "Open gateway configuration blade")</span></span>
2. <span data-ttu-id="b8eea-196">按一下**子網路-設定必要的設定**tooopen hello**加入子網路**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b8eea-196">Click **Subnet - Configure required settings** tooopen hello **Add subnet** blade.</span></span> <span data-ttu-id="b8eea-197">hello**名稱**已經設定使用所需的 hello 值**GatewaySubnet**。</span><span class="sxs-lookup"><span data-stu-id="b8eea-197">hello **Name** is already configured with hello required value **GatewaySubnet**.</span></span>
3. <span data-ttu-id="b8eea-198">hello**位址範圍**hello 閘道子網路的參考 toohello 範圍。</span><span class="sxs-lookup"><span data-stu-id="b8eea-198">hello **Address range** refers toohello range for hello gateway subnet.</span></span> <span data-ttu-id="b8eea-199">雖然您可以使用 /29 位址範圍 (3 個位址) 建立閘道子網路，但是我們建議您建立包含更多 IP 位址的閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="b8eea-199">Although you can create a gateway subnet with a /29 address range (3 addresses), we recommend creating a gateway subnet that contains more IP addresses.</span></span> <span data-ttu-id="b8eea-200">這可以容納未來可能需要更多可用 IP 位址的組態。</span><span class="sxs-lookup"><span data-stu-id="b8eea-200">This will accommodate future configurations that may require more available IP addresses.</span></span> <span data-ttu-id="b8eea-201">可能的話，請使用 /27 或 /28。</span><span class="sxs-lookup"><span data-stu-id="b8eea-201">If possible, use /27 or /28.</span></span> <span data-ttu-id="b8eea-202">如果您使用下列步驟做為練習，您可以參考 toohello[範例](#values)值。</span><span class="sxs-lookup"><span data-stu-id="b8eea-202">If you are using these steps as an exercise, you can refer toohello [Example](#values) values.</span></span> <span data-ttu-id="b8eea-203">按一下**確定**toocreate hello 閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="b8eea-203">Click **OK** toocreate hello gateway subnet.</span></span>
4. <span data-ttu-id="b8eea-204">在 hello**閘道組態**刀鋒視窗中，**大小**參考 toohello 閘道 SKU。</span><span class="sxs-lookup"><span data-stu-id="b8eea-204">On hello **Gateway configuration** blade, **Size** refers toohello gateway SKU.</span></span> <span data-ttu-id="b8eea-205">選取您的 VPN 閘道的 hello 閘道 SKU。</span><span class="sxs-lookup"><span data-stu-id="b8eea-205">Select hello gateway SKU for your VPN gateway.</span></span>
5. <span data-ttu-id="b8eea-206">確認 hello**路由類型**是**動態**，然後按一下**確定**tooreturn toohello**新的 VPN 連線**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b8eea-206">Verify hello **Routing Type** is **Dynamic**, then click **OK** tooreturn toohello **New VPN Connection** blade.</span></span>
6. <span data-ttu-id="b8eea-207">在 hello**新的 VPN 連線**刀鋒視窗中，按一下  **確定** toobegin 建立 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="b8eea-207">On hello **New VPN Connection** blade, click **OK** toobegin creating your VPN gateway.</span></span> <span data-ttu-id="b8eea-208">建立 VPN 閘道，可能會佔用 too45 分鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="b8eea-208">Creating a VPN gateway can take up too45 minutes toocomplete.</span></span>

### <span data-ttu-id="b8eea-209"><a name="ip"></a>第 3-部分複製 hello 虛擬網路閘道的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="b8eea-209"><a name="ip"></a>Part 3 - Copy hello virtual network gateway Public IP address</span></span>

<span data-ttu-id="b8eea-210">建立 hello 虛擬網路閘道之後，您可以檢視 hello 閘道 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8eea-210">After hello virtual network gateway has been created, you can view hello gateway IP address.</span></span> 

1. <span data-ttu-id="b8eea-211">瀏覽 tooyour 傳統的 VNet，然後按一下**概觀**。</span><span class="sxs-lookup"><span data-stu-id="b8eea-211">Navigate tooyour classic VNet, and click **Overview**.</span></span>
2. <span data-ttu-id="b8eea-212">按一下**VPN 連線**tooopen hello VPN 連線刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b8eea-212">Click **VPN connections** tooopen hello VPN connections blade.</span></span> <span data-ttu-id="b8eea-213">在 hello VPN 連線刀鋒視窗中，您可以檢視 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8eea-213">On hello VPN connections blade, you can view hello Public IP address.</span></span> <span data-ttu-id="b8eea-214">這是 hello 分派 tooyour 虛擬網路閘道的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8eea-214">This is hello Public IP address assigned tooyour virtual network gateway.</span></span> 
3. <span data-ttu-id="b8eea-215">請記下或複製 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8eea-215">Write down or copy hello IP address.</span></span> <span data-ttu-id="b8eea-216">當您在稍後的步驟中處理 Resource Manager 區域網路閘道組態設定時，便會用到該 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8eea-216">You use it in later steps when you work with your Resource Manager local network gateway configuration settings.</span></span> <span data-ttu-id="b8eea-217">您也可以檢視您的閘道連線的 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="b8eea-217">You can also view hello status of your gateway connections.</span></span> <span data-ttu-id="b8eea-218">請注意您所建立的 hello 區域網路網站會列為 '連接到'。</span><span class="sxs-lookup"><span data-stu-id="b8eea-218">Notice hello local network site you created is listed as 'Connecting'.</span></span> <span data-ttu-id="b8eea-219">您已建立您的連線之後，hello 狀態會變更。</span><span class="sxs-lookup"><span data-stu-id="b8eea-219">hello status will change after you have created your connections.</span></span>
4. <span data-ttu-id="b8eea-220">複製 hello 閘道 IP 位址之後關閉 hello 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b8eea-220">Close hello blade after copying hello gateway IP address.</span></span>

## <span data-ttu-id="b8eea-221"><a name="rmvnet"></a>2.設定 hello 資源管理員的 VNet 設定</span><span class="sxs-lookup"><span data-stu-id="b8eea-221"><a name="rmvnet"></a>2. Configure hello Resource Manager VNet settings</span></span>

<span data-ttu-id="b8eea-222">本節中，您為資源管理員 VNet 建立 hello 虛擬網路閘道與 hello 區域網路閘道。</span><span class="sxs-lookup"><span data-stu-id="b8eea-222">In this section, you create hello virtual network gateway and hello local network gateway for your Resource Manager VNet.</span></span> <span data-ttu-id="b8eea-223">如果您沒有資源管理員 VNet，且正在執行下列步驟，做為練習，您可以使用來建立 VNet[本文](../virtual-network/virtual-networks-create-vnet-arm-pportal.md)和 hello[範例](#values)上述的設定值。</span><span class="sxs-lookup"><span data-stu-id="b8eea-223">If you don't have a Resource Manager VNet and are running these steps as an exercise, you can create a VNet by using [this article](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) and hello [Example](#values) settings values from above.</span></span>

<span data-ttu-id="b8eea-224">已提供螢幕擷取畫面做為範例。</span><span class="sxs-lookup"><span data-stu-id="b8eea-224">Screenshots are provided as examples.</span></span> <span data-ttu-id="b8eea-225">是確定 tooreplace hello 值，以您自己，或使用 hello[範例](#values)值。</span><span class="sxs-lookup"><span data-stu-id="b8eea-225">Be sure tooreplace hello values with your own, or use hello [Example](#values) values.</span></span>

### <a name="part-1---create-a-gateway-subnet"></a><span data-ttu-id="b8eea-226">第 1 部份 - 建立閘道子網路</span><span class="sxs-lookup"><span data-stu-id="b8eea-226">Part 1 - Create a gateway subnet</span></span>

<span data-ttu-id="b8eea-227">才可建立虛擬網路閘道，您必須先 toocreate hello 閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="b8eea-227">Before creating a virtual network gateway, you first need toocreate hello gateway subnet.</span></span> <span data-ttu-id="b8eea-228">以 /28 或更高的 CIDR 計數建立閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="b8eea-228">Create a gateway subnet with CIDR count of /28 or larger.</span></span> <span data-ttu-id="b8eea-229">(/27、/26 等)</span><span class="sxs-lookup"><span data-stu-id="b8eea-229">(/27, /26, etc.)</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-rm-portal-include.md)]

### <a name="part-2---create-a-virtual-network-gateway"></a><span data-ttu-id="b8eea-230">第 2 部份 - 建立虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="b8eea-230">Part 2 - Create a virtual network gateway</span></span>

[!INCLUDE [vpn-gateway-add-gw-rm-portal](../../includes/vpn-gateway-add-gw-rm-portal-include.md)]

### <span data-ttu-id="b8eea-231"><a name="createlng"></a>第 3 部份 - 建立區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="b8eea-231"><a name="createlng"></a>Part 3 - Create a local network gateway</span></span>

<span data-ttu-id="b8eea-232">hello 區域網路閘道指定 hello 位址範圍，與傳統 VNet 和其虛擬網路閘道相關聯的 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8eea-232">hello local network gateway specifies hello address range and hello Public IP address associated with your classic VNet and its virtual network gateway.</span></span>

<span data-ttu-id="b8eea-233">如果您執行下列步驟做為練習，請參閱 toothese 設定：</span><span class="sxs-lookup"><span data-stu-id="b8eea-233">If you are doing these steps as an exercise, refer toothese settings:</span></span>

| <span data-ttu-id="b8eea-234">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="b8eea-234">Virtual Network</span></span> | <span data-ttu-id="b8eea-235">位址空間</span><span class="sxs-lookup"><span data-stu-id="b8eea-235">Address Space</span></span> | <span data-ttu-id="b8eea-236">區域</span><span class="sxs-lookup"><span data-stu-id="b8eea-236">Region</span></span> | <span data-ttu-id="b8eea-237">Toolocal 網路站台連線</span><span class="sxs-lookup"><span data-stu-id="b8eea-237">Connects toolocal network site</span></span> |<span data-ttu-id="b8eea-238">閘道公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="b8eea-238">Gateway Public IP address</span></span>|
|:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="b8eea-239">ClassicVNet</span><span class="sxs-lookup"><span data-stu-id="b8eea-239">ClassicVNet</span></span> |<span data-ttu-id="b8eea-240">(10.0.0.0/24)</span><span class="sxs-lookup"><span data-stu-id="b8eea-240">(10.0.0.0/24)</span></span> |<span data-ttu-id="b8eea-241">美國西部</span><span class="sxs-lookup"><span data-stu-id="b8eea-241">West US</span></span> | <span data-ttu-id="b8eea-242">RMVNetLocal (192.168.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="b8eea-242">RMVNetLocal (192.168.0.0/16)</span></span> |<span data-ttu-id="b8eea-243">hello 分派 toohello ClassicVNet 閘道的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="b8eea-243">hello Public IP address that is assigned toohello ClassicVNet gateway</span></span>|
| <span data-ttu-id="b8eea-244">RMVNet</span><span class="sxs-lookup"><span data-stu-id="b8eea-244">RMVNet</span></span> | <span data-ttu-id="b8eea-245">(192.168.0.0/16)</span><span class="sxs-lookup"><span data-stu-id="b8eea-245">(192.168.0.0/16)</span></span> |<span data-ttu-id="b8eea-246">美國東部</span><span class="sxs-lookup"><span data-stu-id="b8eea-246">East US</span></span> |<span data-ttu-id="b8eea-247">ClassicVNetLocal (10.0.0.0/24)</span><span class="sxs-lookup"><span data-stu-id="b8eea-247">ClassicVNetLocal (10.0.0.0/24)</span></span> |<span data-ttu-id="b8eea-248">hello 分派 toohello RMVNet 閘道的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8eea-248">hello Public IP address that is assigned toohello RMVNet gateway.</span></span>|

[!INCLUDE [vpn-gateway-add-lng-rm-portal](../../includes/vpn-gateway-add-lng-rm-portal-include.md)]

## <span data-ttu-id="b8eea-249"><a name="modifylng"></a>3.修改 hello 傳統 VNet 本機站台設定</span><span class="sxs-lookup"><span data-stu-id="b8eea-249"><a name="modifylng"></a>3. Modify hello classic VNet local site settings</span></span>

<span data-ttu-id="b8eea-250">在本節中，您會取代 hello 本機站台設定值，指定以 hello 資源管理員 VPN 閘道 IP 位址時所使用的 hello 預留位置 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8eea-250">In this section, you replace hello placeholder IP address that you used when specifying hello local site settings, with hello Resource Manager VPN gateway IP address.</span></span> <span data-ttu-id="b8eea-251">本節使用 hello 傳統 (SM) PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b8eea-251">This section uses hello classic (SM) PowerShell cmdlets.</span></span>

1. <span data-ttu-id="b8eea-252">在 hello Azure 入口網站，瀏覽 toohello 傳統虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b8eea-252">In hello Azure portal, navigate toohello classic virtual network.</span></span>
2. <span data-ttu-id="b8eea-253">在您的虛擬網路的 hello 刀鋒視窗，按一下 **概觀**。</span><span class="sxs-lookup"><span data-stu-id="b8eea-253">On hello blade for your virtual network, click **Overview**.</span></span>
3. <span data-ttu-id="b8eea-254">在 hello **VPN 連線**區段中，按一下 hello hello 圖形中本機網站名稱。</span><span class="sxs-lookup"><span data-stu-id="b8eea-254">In hello **VPN connections** section, click hello name of your local site in hello graphic.</span></span>

    <span data-ttu-id="b8eea-255">![VPN-connections](./media/vpn-gateway-connect-different-deployment-models-portal/vpnconnections.png "VPN 連線")</span><span class="sxs-lookup"><span data-stu-id="b8eea-255">![VPN-connections](./media/vpn-gateway-connect-different-deployment-models-portal/vpnconnections.png "VPN Connections")</span></span>
4. <span data-ttu-id="b8eea-256">在 hello**站對站 VPN 連線**刀鋒視窗中，按一下 hello hello 站台名稱。</span><span class="sxs-lookup"><span data-stu-id="b8eea-256">On hello **Site-to-site VPN connections** blade, click hello name of hello site.</span></span>

    <span data-ttu-id="b8eea-257">![Site-name](./media/vpn-gateway-connect-different-deployment-models-portal/sitetosite3.png "本機站台名稱")</span><span class="sxs-lookup"><span data-stu-id="b8eea-257">![Site-name](./media/vpn-gateway-connect-different-deployment-models-portal/sitetosite3.png "Local site name")</span></span>
5. <span data-ttu-id="b8eea-258">在 hello 連接刀鋒視窗中為您本機的網站，按一下 hello 本機站台 tooopen hello hello 名稱**本機站台**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b8eea-258">On hello connection blade for your local site, click hello name of hello local site tooopen hello **Local site** blade.</span></span>

    <span data-ttu-id="b8eea-259">![Open-local-site](./media/vpn-gateway-connect-different-deployment-models-portal/openlocal.png "開啟本機站台")</span><span class="sxs-lookup"><span data-stu-id="b8eea-259">![Open-local-site](./media/vpn-gateway-connect-different-deployment-models-portal/openlocal.png "Open local site")</span></span>
6. <span data-ttu-id="b8eea-260">在 hello**本機站台**刀鋒視窗中，取代 hello **VPN 閘道 IP 位址**hello hello 資源管理員閘道 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8eea-260">On hello **Local site** blade, replace hello **VPN gateway IP address** with hello IP address of hello Resource Manager gateway.</span></span>

    <span data-ttu-id="b8eea-261">![Gateway-ip-address](./media/vpn-gateway-connect-different-deployment-models-portal/gwipaddress.png "閘道 IP 位址")</span><span class="sxs-lookup"><span data-stu-id="b8eea-261">![Gateway-ip-address](./media/vpn-gateway-connect-different-deployment-models-portal/gwipaddress.png "Gateway IP address")</span></span>
7. <span data-ttu-id="b8eea-262">按一下**確定**tooupdate hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b8eea-262">Click **OK** tooupdate hello IP address.</span></span>

## <span data-ttu-id="b8eea-263"><a name="RMtoclassic"></a>4.建立資源管理員 tooclassic 連線</span><span class="sxs-lookup"><span data-stu-id="b8eea-263"><a name="RMtoclassic"></a>4. Create Resource Manager tooclassic connection</span></span>

<span data-ttu-id="b8eea-264">在這些步驟中，您可以設定 hello 資源管理員 VNet 中的 hello 連接 toohello 傳統的 VNet 使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b8eea-264">In these steps, you configure hello connection from hello Resource Manager VNet toohello classic VNet using hello Azure portal.</span></span>

1. <span data-ttu-id="b8eea-265">在**所有資源**，找出 hello 區域網路閘道。</span><span class="sxs-lookup"><span data-stu-id="b8eea-265">In **All resources**, locate hello local network gateway.</span></span> <span data-ttu-id="b8eea-266">在本例中，為 hello 區域網路閘道**ClassicVNetLocal**。</span><span class="sxs-lookup"><span data-stu-id="b8eea-266">In our example, hello local network gateway is **ClassicVNetLocal**.</span></span>
2. <span data-ttu-id="b8eea-267">按一下**組態**並確認 hello IP 位址的值為 hello 的 hello VPN 閘道傳統的 VNet。</span><span class="sxs-lookup"><span data-stu-id="b8eea-267">Click **Configuration** and verify that hello IP address value is hello VPN gateway for hello classic VNet.</span></span> <span data-ttu-id="b8eea-268">視需要更新，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="b8eea-268">Update, if needed, then click **Save**.</span></span> <span data-ttu-id="b8eea-269">關閉 hello 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b8eea-269">Close hello blade.</span></span>
3. <span data-ttu-id="b8eea-270">在**所有資源**，按一下 hello 區域網路閘道。</span><span class="sxs-lookup"><span data-stu-id="b8eea-270">In **All resources**, click hello local network gateway.</span></span>
4. <span data-ttu-id="b8eea-271">按一下**連線**tooopen hello 連線刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b8eea-271">Click **Connections** tooopen hello Connections blade.</span></span>
5. <span data-ttu-id="b8eea-272">在 hello**連線**刀鋒視窗中，按一下   **+**  tooadd 連接。</span><span class="sxs-lookup"><span data-stu-id="b8eea-272">On hello **Connections** blade, click **+** tooadd a connection.</span></span>
6. <span data-ttu-id="b8eea-273">在 hello**加入連接**刀鋒視窗中，名稱 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="b8eea-273">On hello **Add connection** blade, name hello connection.</span></span> <span data-ttu-id="b8eea-274">例如，'RMtoClassic'。</span><span class="sxs-lookup"><span data-stu-id="b8eea-274">For example, 'RMtoClassic'.</span></span>
7. <span data-ttu-id="b8eea-275">已在此刀鋒視窗中選取 [站對站]。</span><span class="sxs-lookup"><span data-stu-id="b8eea-275">**Site-to-Site** is already selected on this blade.</span></span>
8. <span data-ttu-id="b8eea-276">選取您想要與此站台 tooassociate hello 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="b8eea-276">Select hello virtual network gateway that you want tooassociate with this site.</span></span>
9. <span data-ttu-id="b8eea-277">建立**共用金鑰**。</span><span class="sxs-lookup"><span data-stu-id="b8eea-277">Create a **shared key**.</span></span> <span data-ttu-id="b8eea-278">從傳統 VNet toohello hello 資源管理員 VNet 建立 hello 連接中也使用此金鑰。</span><span class="sxs-lookup"><span data-stu-id="b8eea-278">This key is also used in hello connection that you create from hello classic VNet toohello Resource Manager VNet.</span></span> <span data-ttu-id="b8eea-279">您可以產生 hello 金鑰，或建立一個。</span><span class="sxs-lookup"><span data-stu-id="b8eea-279">You can generate hello key or make one up.</span></span> <span data-ttu-id="b8eea-280">在我們的範例中，我們使用的是 'abc123'，但是您可以(且應該) 使用更為複雜的值。</span><span class="sxs-lookup"><span data-stu-id="b8eea-280">In our example, we use 'abc123', but you can (and should) use something more complex.</span></span>
10. <span data-ttu-id="b8eea-281">按一下**確定**toocreate hello 連線。</span><span class="sxs-lookup"><span data-stu-id="b8eea-281">Click **OK** toocreate hello connection.</span></span>

##<span data-ttu-id="b8eea-282"><a name="classictoRM"></a>5.建立傳統 tooResource Manager 連線</span><span class="sxs-lookup"><span data-stu-id="b8eea-282"><a name="classictoRM"></a>5. Create classic tooResource Manager connection</span></span>

<span data-ttu-id="b8eea-283">在這些步驟中，您可以設定傳統 VNet toohello hello 資源管理員 VNet 中的 hello 連接。</span><span class="sxs-lookup"><span data-stu-id="b8eea-283">In these steps, you configure hello connection from hello classic VNet toohello Resource Manager VNet.</span></span> <span data-ttu-id="b8eea-284">這些步驟需要 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="b8eea-284">These steps require PowerShell.</span></span> <span data-ttu-id="b8eea-285">您無法在 hello 入口網站中建立此連線。</span><span class="sxs-lookup"><span data-stu-id="b8eea-285">You can't create this connection in hello portal.</span></span> <span data-ttu-id="b8eea-286">請確定您已下載並安裝 hello 傳統 (SM) 和資源管理員 (RM) PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="b8eea-286">Make sure you have downloaded and installed both hello classic (SM) and Resource Manager (RM) PowerShell cmdlets.</span></span>

### <a name="1-connect-tooyour-azure-account"></a><span data-ttu-id="b8eea-287">1.連接 tooyour Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="b8eea-287">1. Connect tooyour Azure account</span></span>

<span data-ttu-id="b8eea-288">使用提高的權限開啟 hello PowerShell 主控台，並登入 tooyour Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b8eea-288">Open hello PowerShell console with elevated rights and log in tooyour Azure account.</span></span> <span data-ttu-id="b8eea-289">hello 下列 cmdlet 會提示您輸入 hello 登入認證您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="b8eea-289">hello following cmdlet prompts you for hello login credentials for your Azure Account.</span></span> <span data-ttu-id="b8eea-290">登入之後，使其可用 tooAzure PowerShell，會下載您的帳戶設定。</span><span class="sxs-lookup"><span data-stu-id="b8eea-290">After logging in, your account settings are downloaded so that they are available tooAzure PowerShell.</span></span>

```powershell
Login-AzureRmAccount
```
   
<span data-ttu-id="b8eea-291">如果您有多個訂用帳戶，請取得 Azure 訂用帳戶的清單。</span><span class="sxs-lookup"><span data-stu-id="b8eea-291">Get a list of your Azure subscriptions if you have more than one subscription.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="b8eea-292">指定您想 toouse hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b8eea-292">Specify hello subscription that you want toouse.</span></span> 

```powershell
Select-AzureRmSubscription -SubscriptionName "Name of subscription"
```

<span data-ttu-id="b8eea-293">加入您 Azure 帳戶 toouse hello 傳統 PowerShell cmdlet (SM)。</span><span class="sxs-lookup"><span data-stu-id="b8eea-293">Add your Azure Account toouse hello classic PowerShell cmdlets (SM).</span></span> <span data-ttu-id="b8eea-294">toodo 因此，您可以使用下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="b8eea-294">toodo so, you can use hello following command:</span></span>

```powershell
Add-AzureAccount
```

### <a name="2-view-hello-network-configuration-file-values"></a><span data-ttu-id="b8eea-295">2.檢視 hello 網路組態檔值</span><span class="sxs-lookup"><span data-stu-id="b8eea-295">2. View hello network configuration file values</span></span>

<span data-ttu-id="b8eea-296">當您建立 VNet hello Azure 入口網站中時，不在 hello Azure 入口網站中顯示 hello Azure 會使用的完整名稱。</span><span class="sxs-lookup"><span data-stu-id="b8eea-296">When you create a VNet in hello Azure portal, hello full name that Azure uses is not visible in hello Azure portal.</span></span> <span data-ttu-id="b8eea-297">比方說，VNet 出現 toobe hello Azure 入口網站中名為 'ClassicVNet' 可能 hello 網路組態檔中有多長的名稱。</span><span class="sxs-lookup"><span data-stu-id="b8eea-297">For example, a VNet that appears toobe named 'ClassicVNet' in hello Azure portal may have a much longer name in hello network configuration file.</span></span> <span data-ttu-id="b8eea-298">hello 名稱可能看起來像這樣: ' 群組 ClassicRG ClassicVNet'。</span><span class="sxs-lookup"><span data-stu-id="b8eea-298">hello name might look something like: 'Group ClassicRG ClassicVNet'.</span></span> <span data-ttu-id="b8eea-299">在這些步驟中，您可以下載 hello 網路組態檔和檢視 hello 值。</span><span class="sxs-lookup"><span data-stu-id="b8eea-299">In these steps, you download hello network configuration file and view hello values.</span></span>

<span data-ttu-id="b8eea-300">您的電腦上建立目錄，然後匯出 hello 網路組態檔 toohello 目錄。</span><span class="sxs-lookup"><span data-stu-id="b8eea-300">Create a directory on your computer and then export hello network configuration file toohello directory.</span></span> <span data-ttu-id="b8eea-301">在此範例中，hello 網路組態檔會是匯出的 tooC:\AzureNet。</span><span class="sxs-lookup"><span data-stu-id="b8eea-301">In this example, hello network configuration file is exported tooC:\AzureNet.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="b8eea-302">使用傳統 VNet 的文字編輯器和檢視 hello 名稱開啟 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="b8eea-302">Open hello file with a text editor and view hello name for your classic VNet.</span></span> <span data-ttu-id="b8eea-303">執行 PowerShell cmdlet 時，請使用 hello 網路組態檔中的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="b8eea-303">Use hello names in hello network configuration file when running your PowerShell cmdlets.</span></span>

- <span data-ttu-id="b8eea-304">VNet 名稱會列為 **VirtualNetworkSite name =**</span><span class="sxs-lookup"><span data-stu-id="b8eea-304">VNet names are listed as **VirtualNetworkSite name =**</span></span>
- <span data-ttu-id="b8eea-305">網站名稱會列為 **LocalNetworkSite name=**</span><span class="sxs-lookup"><span data-stu-id="b8eea-305">Site names are listed as **LocalNetworkSite name=**</span></span>

### <a name="3-create-hello-connection"></a><span data-ttu-id="b8eea-306">3.建立 hello 連線</span><span class="sxs-lookup"><span data-stu-id="b8eea-306">3. Create hello connection</span></span>

<span data-ttu-id="b8eea-307">設定 hello 共用的金鑰，並從傳統 VNet toohello hello 資源管理員 VNet 建立 hello 連接。</span><span class="sxs-lookup"><span data-stu-id="b8eea-307">Set hello shared key and create hello connection from hello classic VNet toohello Resource Manager VNet.</span></span> <span data-ttu-id="b8eea-308">您無法設定 hello 使用 hello 入口網站的共用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="b8eea-308">You cannot set hello shared key using hello portal.</span></span> <span data-ttu-id="b8eea-309">請確定您執行這些步驟時使用精簡 hello PowerShell cmdlet hello 登入。</span><span class="sxs-lookup"><span data-stu-id="b8eea-309">Make sure you run these steps while logged in using hello classic version of hello PowerShell cmdlets.</span></span> <span data-ttu-id="b8eea-310">因此，使用 toodo **Add-azureaccount**。</span><span class="sxs-lookup"><span data-stu-id="b8eea-310">toodo so, use **Add-AzureAccount**.</span></span> <span data-ttu-id="b8eea-311">否則，就能 tooset hello '-AzureVNetGatewayKey'。</span><span class="sxs-lookup"><span data-stu-id="b8eea-311">Otherwise, you will not be able tooset hello '-AzureVNetGatewayKey'.</span></span>

- <span data-ttu-id="b8eea-312">在此範例中， **-VNetName** hello 名稱做為傳統 VNet 找到您的網路組態檔中的 hello。</span><span class="sxs-lookup"><span data-stu-id="b8eea-312">In this example, **-VNetName** is hello name of hello classic VNet as found in your network configuration file.</span></span> 
- <span data-ttu-id="b8eea-313">hello **-LocalNetworkSiteName** hello 本機站台上，指定為 hello 名稱位於您的網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="b8eea-313">hello **-LocalNetworkSiteName** is hello name you specified for hello local site, as found in your network configuration file.</span></span>
- <span data-ttu-id="b8eea-314">hello **-SharedKey**是產生及指定的值。</span><span class="sxs-lookup"><span data-stu-id="b8eea-314">hello **-SharedKey** is a value that you generate and specify.</span></span> <span data-ttu-id="b8eea-315">針對此範例，我們使用的是 *abc123*，但是您可以使用更為複雜的值。</span><span class="sxs-lookup"><span data-stu-id="b8eea-315">For this example, we used *abc123*, but you can generate something more complex.</span></span> <span data-ttu-id="b8eea-316">hello 重要件事就是您在此處指定的 hello 該值必須是相同的值，指定建立資源管理員 tooclassic 連接時的 hello。</span><span class="sxs-lookup"><span data-stu-id="b8eea-316">hello important thing is that hello value you specify here must be hello same value that you specified when creating your Resource Manager tooclassic connection.</span></span>

```powershell
Set-AzureVNetGatewayKey -VNetName "Group ClassicRG ClassicVNet" `
-LocalNetworkSiteName "172B9E16_RMVNetLocal" -SharedKey abc123
```

##<span data-ttu-id="b8eea-317"><a name="verify"></a>6.確認您的連線</span><span class="sxs-lookup"><span data-stu-id="b8eea-317"><a name="verify"></a>6. Verify your connections</span></span>

<span data-ttu-id="b8eea-318">您可以確認您使用的連線 hello Azure 入口網站或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="b8eea-318">You can verify your connections by using hello Azure portal or PowerShell.</span></span> <span data-ttu-id="b8eea-319">當驗證，您可能需要 toowait 一兩分鐘 hello 連接所建立。</span><span class="sxs-lookup"><span data-stu-id="b8eea-319">When verifying, you may need toowait a minute or two as hello connection is being created.</span></span> <span data-ttu-id="b8eea-320">當連接成功時，hello 連線狀態變更從 '連接到' too'Connected'。</span><span class="sxs-lookup"><span data-stu-id="b8eea-320">When a connection is successful, hello connectivity state changes from 'Connecting' too'Connected'.</span></span>

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a><span data-ttu-id="b8eea-321">從傳統 VNet tooyour 資源管理員 VNet tooverify hello 連線</span><span class="sxs-lookup"><span data-stu-id="b8eea-321">tooverify hello connection from your classic VNet tooyour Resource Manager VNet</span></span>

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]

###<a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a><span data-ttu-id="b8eea-322">從資源管理員 VNet tooyour tooverify hello 連接傳統的 VNet</span><span class="sxs-lookup"><span data-stu-id="b8eea-322">tooverify hello connection from your Resource Manager VNet tooyour classic VNet</span></span>

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="b8eea-323"><a name="faq"></a>VNet 對 VNet 常見問題集</span><span class="sxs-lookup"><span data-stu-id="b8eea-323"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]
