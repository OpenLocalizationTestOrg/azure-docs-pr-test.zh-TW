---
title: "將虛擬網路閘道新增到 ExpressRoute 的 VNet：入口網站：Azure | Microsoft Docs"
description: "本文將逐步引導您完成將虛擬網路閘道新增到已經建立之 ExpressRoute 的 Resource Manager VNet。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: cherylmc
ms.openlocfilehash: 2bd0cf8be87937044ad515a2c6f253b1711bb2bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-the-azure-portal"></a><span data-ttu-id="fb0e5-103">使用 Azure 入口網站為 ExpressRoute 設定虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="fb0e5-103">Configure a virtual network gateway for ExpressRoute using the Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fb0e5-104">Resource Manager - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="fb0e5-104">Resource Manager - Azure portal</span></span>](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [<span data-ttu-id="fb0e5-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb0e5-105">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="fb0e5-106">傳統 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb0e5-106">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="fb0e5-107">影片 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="fb0e5-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="fb0e5-108">本文將逐步引導您完成為既存的 VNet 新增虛擬網路閘道的步驟。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-108">This article walks you through the steps to add a virtual network gateway for a pre-existing VNet.</span></span> <span data-ttu-id="fb0e5-109">本文將逐步引導您完成為既存的 VNet 新增虛擬網路 (VNet) 閘道、調整該閘道大小及移除該閘道的步驟。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-109">This article walks you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="fb0e5-110">此組態的步驟是使用 Resource Manager 部署模型來建立的 VNet 所專用，而在 ExpressRoute 組態中也將使用該部署模型。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-110">The steps for this configuration are specifically for VNets that were created using the Resource Manager deployment model that will be used in an ExpressRoute configuration.</span></span> <span data-ttu-id="fb0e5-111">如需有關 ExpressRoute 之虛擬網路閘道和閘道組態設定的詳細資訊，請參閱[關於 ExpressRoute 的虛擬網路閘道](expressroute-about-virtual-network-gateways.md)。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-111">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span></span> 


## <a name="before-beginning"></a><span data-ttu-id="fb0e5-112">開始之前</span><span class="sxs-lookup"><span data-stu-id="fb0e5-112">Before beginning</span></span>

<span data-ttu-id="fb0e5-113">此工作的步驟會根據下列組態參考清單中的值來使用 VNet。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-113">The steps for this task use a VNet based on the values in the following configuration reference list.</span></span> <span data-ttu-id="fb0e5-114">我們會在範例步驟中使用此清單。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-114">We use this list in our example steps.</span></span> <span data-ttu-id="fb0e5-115">您可以複製清單以供參考，並使用您自己的值來取代其中的值。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-115">You can copy the list to use as a reference, replacing the values with your own.</span></span>

<span data-ttu-id="fb0e5-116">**組態參考清單**</span><span class="sxs-lookup"><span data-stu-id="fb0e5-116">**Configuration reference list**</span></span>

* <span data-ttu-id="fb0e5-117">虛擬網路名稱 = "TestVNet"</span><span class="sxs-lookup"><span data-stu-id="fb0e5-117">Virtual Network Name = "TestVNet"</span></span>
* <span data-ttu-id="fb0e5-118">虛擬網路位址空間 = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="fb0e5-118">Virtual Network address space = 192.168.0.0/16</span></span>
* <span data-ttu-id="fb0e5-119">子網路名稱 = "FrontEnd"</span><span class="sxs-lookup"><span data-stu-id="fb0e5-119">Subnet Name = "FrontEnd"</span></span> 
    * <span data-ttu-id="fb0e5-120">子網路位址空間 = "192.168.1.0/24"</span><span class="sxs-lookup"><span data-stu-id="fb0e5-120">Subnet address space = "192.168.1.0/24"</span></span>
* <span data-ttu-id="fb0e5-121">資源群組 = "TestRG"</span><span class="sxs-lookup"><span data-stu-id="fb0e5-121">Resource Group = "TestRG"</span></span>
* <span data-ttu-id="fb0e5-122">位置 = "美國東部"</span><span class="sxs-lookup"><span data-stu-id="fb0e5-122">Location = "East US"</span></span>
* <span data-ttu-id="fb0e5-123">閘道器子網路名稱："GatewaySubnet"，您必須一律將閘道器子網路命名為 *GatewaySubnet*。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-123">Gateway Subnet name: "GatewaySubnet" You must always name a gateway subnet *GatewaySubnet*.</span></span>
    * <span data-ttu-id="fb0e5-124">閘道子網路位址空間 = "192.168.200.0/26"</span><span class="sxs-lookup"><span data-stu-id="fb0e5-124">Gateway Subnet address space = "192.168.200.0/26"</span></span>
* <span data-ttu-id="fb0e5-125">閘道名稱 = "ERGW"</span><span class="sxs-lookup"><span data-stu-id="fb0e5-125">Gateway Name = "ERGW"</span></span>
* <span data-ttu-id="fb0e5-126">閘道 IP 名稱 = "MyERGWVIP"</span><span class="sxs-lookup"><span data-stu-id="fb0e5-126">Gateway IP Name = "MyERGWVIP"</span></span>
* <span data-ttu-id="fb0e5-127">閘道類型 = "ExpressRoute"，ExpressRoute 組態需要這個類型。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-127">Gateway type = "ExpressRoute" This type is required for an ExpressRoute configuration.</span></span>
* <span data-ttu-id="fb0e5-128">閘道公用 IP 名稱 = "MyERGWVIP"</span><span class="sxs-lookup"><span data-stu-id="fb0e5-128">Gateway Public IP Name = "MyERGWVIP"</span></span>

<span data-ttu-id="fb0e5-129">您可以先檢視這些步驟的[影片](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)，再開始進行設定。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-129">You can view a [Video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network) of these steps before beginning your configuration.</span></span>

## <a name="create-the-gateway-subnet"></a><span data-ttu-id="fb0e5-130">建立閘道子網路</span><span class="sxs-lookup"><span data-stu-id="fb0e5-130">Create the gateway subnet</span></span>

1. <span data-ttu-id="fb0e5-131">在[入口網站](http://portal.azure.com)中，瀏覽至要建立虛擬網路閘道的 Resource Manager 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-131">In the [portal](http://portal.azure.com), navigate to the Resource Manager virtual network for which you want to create a virtual network gateway.</span></span>
2. <span data-ttu-id="fb0e5-132">在 VNet 刀鋒視窗的 [設定] 中，按一下 [子網路] 以展開 [子網路] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-132">In the **Settings** section of your VNet blade, click **Subnets** to expand the Subnets blade.</span></span>
3. <span data-ttu-id="fb0e5-133">在 [子網路] 刀鋒視窗中，按一下 [+閘道子網路] 以開啟 [新增子網路] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-133">On the **Subnets** blade, click **+Gateway subnet** to open the **Add subnet** blade.</span></span> 
   
    <span data-ttu-id="fb0e5-134">![新增閘道子網路](./media/expressroute-howto-add-gateway-portal-resource-manager/addgwsubnet.png "新增閘道子網路")</span><span class="sxs-lookup"><span data-stu-id="fb0e5-134">![Add the gateway subnet](./media/expressroute-howto-add-gateway-portal-resource-manager/addgwsubnet.png "Add the gateway subnet")</span></span>


4. <span data-ttu-id="fb0e5-135">子網路的 [名稱] 會自動填入 'GatewaySubnet' 這個值。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-135">The **Name** for your subnet is automatically filled in with the value 'GatewaySubnet'.</span></span> <span data-ttu-id="fb0e5-136">為了讓 Azure 將此子網路視為閘道子網路，需要有這個值。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-136">This value is required in order for Azure to recognize the subnet as the gateway subnet.</span></span> <span data-ttu-id="fb0e5-137">調整自動填入的 [位址範圍] 值，以符合您的組態需求。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-137">Adjust the auto-filled **Address range** values to match your configuration requirements.</span></span> <span data-ttu-id="fb0e5-138">建議您以 /27 或更大的值 (/26、/25 等) 建立閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-138">We recommend creating a gateway subnet with a /27 or larger (/26, /25, etc.).</span></span> <span data-ttu-id="fb0e5-139">然後，按一下 [確定] 來儲存值並建立閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-139">Then, click **OK** to save the values and create the gateway subnet.</span></span>

    <span data-ttu-id="fb0e5-140">![新增子網路](./media/expressroute-howto-add-gateway-portal-resource-manager/addsubnetgw.png "新增子網路")</span><span class="sxs-lookup"><span data-stu-id="fb0e5-140">![Adding the subnet](./media/expressroute-howto-add-gateway-portal-resource-manager/addsubnetgw.png "Adding the subnet")</span></span>

## <a name="create-the-virtual-network-gateway"></a><span data-ttu-id="fb0e5-141">建立虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="fb0e5-141">Create the virtual network gateway</span></span>

1. <span data-ttu-id="fb0e5-142">在入口網站中，按一下左側的 **+** 並在搜尋中輸入「虛擬網路閘道」。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-142">In the portal, on the left side, click **+** and type 'Virtual Network Gateway' in search.</span></span> <span data-ttu-id="fb0e5-143">在搜尋傳回的結果中找出**虛擬網路閘道**，然後按一下該項目。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-143">Locate **Virtual network gateway** in the search return and click the entry.</span></span> <span data-ttu-id="fb0e5-144">在 [虛擬網路閘道] 刀鋒視窗上，按一下刀鋒視窗底部的 [建立]。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-144">On the **Virtual network gateway** blade, click **Create** at the bottom of the blade.</span></span> <span data-ttu-id="fb0e5-145">這會開啟 [建立虛擬網路閘道] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-145">This opens the **Create virtual network gateway** blade.</span></span>
2. <span data-ttu-id="fb0e5-146">在 [建立虛擬網路閘道] 刀鋒視窗上，填入您虛擬網路閘道的值。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-146">On the **Create virtual network gateway** blade, fill in the values for your virtual network gateway.</span></span>

    <span data-ttu-id="fb0e5-147">![建立虛擬網路閘道刀鋒視窗欄位](./media/expressroute-howto-add-gateway-portal-resource-manager/gw.png "建立虛擬網路閘道刀鋒視窗欄位")</span><span class="sxs-lookup"><span data-stu-id="fb0e5-147">![Create virtual network gateway blade fields](./media/expressroute-howto-add-gateway-portal-resource-manager/gw.png "Create virtual network gateway blade fields")</span></span>
3. <span data-ttu-id="fb0e5-148">**名稱**：為您的閘道命名。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-148">**Name**: Name your gateway.</span></span> <span data-ttu-id="fb0e5-149">這與為閘道子網路命名不同。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-149">This is not the same as naming a gateway subnet.</span></span> <span data-ttu-id="fb0e5-150">這是您要建立之閘道物件的名稱。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-150">It's the name of the gateway object you are creating.</span></span>
4. <span data-ttu-id="fb0e5-151">**閘道類型**︰選取 [ExpressRoute]。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-151">**Gateway type**: Select **ExpressRoute**.</span></span>
5. <span data-ttu-id="fb0e5-152">**SKU**︰從下拉式清單中選取閘道 SKU。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-152">**SKU**: Select the gateway SKU from the dropdown.</span></span>
6. <span data-ttu-id="fb0e5-153">**位置**：調整 [位置] 欄位以指向您的虛擬網路所在的位置。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-153">**Location**: Adjust the **Location** field to point to the location where your virtual network is located.</span></span> <span data-ttu-id="fb0e5-154">如果位置並未指向您的虛擬網路所在的區域，則此虛擬網路不會出現在 [選擇虛擬網路] 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-154">If the location is not pointing to the region where your virtual network resides, the virtual network doesn't appear in the 'Choose a virtual network' dropdown.</span></span>
7. <span data-ttu-id="fb0e5-155">選擇您要新增此閘道的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-155">Choose the virtual network to which you want to add this gateway.</span></span> <span data-ttu-id="fb0e5-156">按一下 [虛擬網路] 以開啟 [選擇擇虛擬網路] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-156">Click **Virtual network** to open the **Choose a virtual network** blade.</span></span> <span data-ttu-id="fb0e5-157">選取 VNet。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-157">Select the VNet.</span></span> <span data-ttu-id="fb0e5-158">如果您沒看到您的 VNet，請確定 [位置] 欄位是指向您的虛擬網路所在的區域。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-158">If you don't see your VNet, make sure the **Location** field is pointing to the region in which your virtual network is located.</span></span>
9. <span data-ttu-id="fb0e5-159">選擇公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-159">Choose a public IP address.</span></span> <span data-ttu-id="fb0e5-160">按一下 [公用 IP 位址] 以開啟 [選擇公用 IP 位址] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-160">Click **Public IP address** to open the **Choose public IP address** blade.</span></span> <span data-ttu-id="fb0e5-161">按一下 [+新建] 以開啟 [建立公用 IP 位址] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-161">Click **+Create New** to open the **Create public IP address blade**.</span></span> <span data-ttu-id="fb0e5-162">輸入公用 IP 位址的名稱。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-162">Input a name for your public IP address.</span></span> <span data-ttu-id="fb0e5-163">此刀鋒視窗會建立將動態獲派公用 IP 位址的公用 IP 位址物件。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-163">This blade creates a public IP address object to which a public IP address will be dynamically assigned.</span></span> <span data-ttu-id="fb0e5-164">按一下 [確定] 將變更儲存至此刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-164">Click **OK** to save your changes to this blade.</span></span>
10. <span data-ttu-id="fb0e5-165">**訂用帳戶**：請確認已選取正確的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-165">**Subscription**: Verify that the correct subscription is selected.</span></span>
11. <span data-ttu-id="fb0e5-166">**資源群組**：此設定取決於您選取的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-166">**Resource group**: This setting is determined by the Virtual Network that you select.</span></span>
12. <span data-ttu-id="fb0e5-167">指定上述設定之後，請勿調整 [位置]。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-167">Don't adjust the **Location** after you've specified the previous settings.</span></span>
13. <span data-ttu-id="fb0e5-168">確認設定。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-168">Verify the settings.</span></span> <span data-ttu-id="fb0e5-169">如果您希望閘道顯示在儀表板上，可以選取刀鋒視窗底部的 [釘選到儀表板]。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-169">If you want your gateway to appear on the dashboard, you can select **Pin to dashboard** at the bottom of the blade.</span></span>
14. <span data-ttu-id="fb0e5-170">按一下 [建立]  即可開始建立閘道。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-170">Click **Create** to begin creating the gateway.</span></span> <span data-ttu-id="fb0e5-171">系統會驗證設定並部署閘道。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-171">The settings are validated and the gateway deploys.</span></span> <span data-ttu-id="fb0e5-172">建立虛擬網路閘道最多可能需要花費 45 分鐘的時間來完成。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-172">Creating virtual network gateway can take up to 45 minutes to complete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fb0e5-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fb0e5-173">Next steps</span></span>
<span data-ttu-id="fb0e5-174">建立 VNet 閘道之後，您可以將 VNet 連結至 ExpressRoute 循環。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-174">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span></span> <span data-ttu-id="fb0e5-175">請參閱 [將虛擬網路連結到 ExpressRoute 循環](expressroute-howto-linkvnet-portal-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="fb0e5-175">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>