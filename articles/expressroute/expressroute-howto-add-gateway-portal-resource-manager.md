---
title: "新增虛擬網路閘道 tooa VNet expressroute： 入口網站： Azure |Microsoft 文件"
description: "這篇文章會引導您完成新增虛擬網路閘道 tooan 已經建立 ExpressRoute 的資源管理員 VNet。"
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
ms.openlocfilehash: 9e922af1f3676eeebc569b57c3ae3a22d4e0b395
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-hello-azure-portal"></a><span data-ttu-id="8832d-103">Expressroute 使用 hello Azure 入口網站設定虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="8832d-103">Configure a virtual network gateway for ExpressRoute using hello Azure portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8832d-104">Resource Manager - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8832d-104">Resource Manager - Azure portal</span></span>](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [<span data-ttu-id="8832d-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="8832d-105">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="8832d-106">傳統 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="8832d-106">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="8832d-107">影片 - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="8832d-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="8832d-108">本文將引導您完成 hello 步驟 tooadd 虛擬網路閘道已存在的 VNet。</span><span class="sxs-lookup"><span data-stu-id="8832d-108">This article walks you through hello steps tooadd a virtual network gateway for a pre-existing VNet.</span></span> <span data-ttu-id="8832d-109">本文將引導您完成 hello 步驟 tooadd、 調整大小，並移除虛擬網路 (VNet) 閘道預先存在的 vnet。</span><span class="sxs-lookup"><span data-stu-id="8832d-109">This article walks you through hello steps tooadd, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="8832d-110">此組態的 hello 步驟是特別針對使用將用於 ExpressRoute 組態中的 hello Resource Manager 部署模型所建立的 Vnet。</span><span class="sxs-lookup"><span data-stu-id="8832d-110">hello steps for this configuration are specifically for VNets that were created using hello Resource Manager deployment model that will be used in an ExpressRoute configuration.</span></span> <span data-ttu-id="8832d-111">如需有關 ExpressRoute 之虛擬網路閘道和閘道組態設定的詳細資訊，請參閱[關於 ExpressRoute 的虛擬網路閘道](expressroute-about-virtual-network-gateways.md)。</span><span class="sxs-lookup"><span data-stu-id="8832d-111">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span></span> 


## <a name="before-beginning"></a><span data-ttu-id="8832d-112">開始之前</span><span class="sxs-lookup"><span data-stu-id="8832d-112">Before beginning</span></span>

<span data-ttu-id="8832d-113">此工作會使用 VNet 的 hello 步驟 hello 下列組態的參考清單中的 hello 值為基礎。</span><span class="sxs-lookup"><span data-stu-id="8832d-113">hello steps for this task use a VNet based on hello values in hello following configuration reference list.</span></span> <span data-ttu-id="8832d-114">我們會在範例步驟中使用此清單。</span><span class="sxs-lookup"><span data-stu-id="8832d-114">We use this list in our example steps.</span></span> <span data-ttu-id="8832d-115">您可以複製 hello 清單 toouse，做為參考，取代您自己 hello 值。</span><span class="sxs-lookup"><span data-stu-id="8832d-115">You can copy hello list toouse as a reference, replacing hello values with your own.</span></span>

<span data-ttu-id="8832d-116">**組態參考清單**</span><span class="sxs-lookup"><span data-stu-id="8832d-116">**Configuration reference list**</span></span>

* <span data-ttu-id="8832d-117">虛擬網路名稱 = "TestVNet"</span><span class="sxs-lookup"><span data-stu-id="8832d-117">Virtual Network Name = "TestVNet"</span></span>
* <span data-ttu-id="8832d-118">虛擬網路位址空間 = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="8832d-118">Virtual Network address space = 192.168.0.0/16</span></span>
* <span data-ttu-id="8832d-119">子網路名稱 = "FrontEnd"</span><span class="sxs-lookup"><span data-stu-id="8832d-119">Subnet Name = "FrontEnd"</span></span> 
    * <span data-ttu-id="8832d-120">子網路位址空間 = "192.168.1.0/24"</span><span class="sxs-lookup"><span data-stu-id="8832d-120">Subnet address space = "192.168.1.0/24"</span></span>
* <span data-ttu-id="8832d-121">資源群組 = "TestRG"</span><span class="sxs-lookup"><span data-stu-id="8832d-121">Resource Group = "TestRG"</span></span>
* <span data-ttu-id="8832d-122">位置 = "美國東部"</span><span class="sxs-lookup"><span data-stu-id="8832d-122">Location = "East US"</span></span>
* <span data-ttu-id="8832d-123">閘道器子網路名稱："GatewaySubnet"，您必須一律將閘道器子網路命名為 *GatewaySubnet*。</span><span class="sxs-lookup"><span data-stu-id="8832d-123">Gateway Subnet name: "GatewaySubnet" You must always name a gateway subnet *GatewaySubnet*.</span></span>
    * <span data-ttu-id="8832d-124">閘道子網路位址空間 = "192.168.200.0/26"</span><span class="sxs-lookup"><span data-stu-id="8832d-124">Gateway Subnet address space = "192.168.200.0/26"</span></span>
* <span data-ttu-id="8832d-125">閘道名稱 = "ERGW"</span><span class="sxs-lookup"><span data-stu-id="8832d-125">Gateway Name = "ERGW"</span></span>
* <span data-ttu-id="8832d-126">閘道 IP 名稱 = "MyERGWVIP"</span><span class="sxs-lookup"><span data-stu-id="8832d-126">Gateway IP Name = "MyERGWVIP"</span></span>
* <span data-ttu-id="8832d-127">閘道類型 = "ExpressRoute"，ExpressRoute 組態需要這個類型。</span><span class="sxs-lookup"><span data-stu-id="8832d-127">Gateway type = "ExpressRoute" This type is required for an ExpressRoute configuration.</span></span>
* <span data-ttu-id="8832d-128">閘道公用 IP 名稱 = "MyERGWVIP"</span><span class="sxs-lookup"><span data-stu-id="8832d-128">Gateway Public IP Name = "MyERGWVIP"</span></span>

<span data-ttu-id="8832d-129">您可以先檢視這些步驟的[影片](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)，再開始進行設定。</span><span class="sxs-lookup"><span data-stu-id="8832d-129">You can view a [Video](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network) of these steps before beginning your configuration.</span></span>

## <a name="create-hello-gateway-subnet"></a><span data-ttu-id="8832d-130">建立 hello 閘道子網路</span><span class="sxs-lookup"><span data-stu-id="8832d-130">Create hello gateway subnet</span></span>

1. <span data-ttu-id="8832d-131">在 hello[入口網站](http://portal.azure.com)，瀏覽您想要的虛擬網路閘道 toocreate toohello 資源管理員虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="8832d-131">In hello [portal](http://portal.azure.com), navigate toohello Resource Manager virtual network for which you want toocreate a virtual network gateway.</span></span>
2. <span data-ttu-id="8832d-132">在 hello**設定**> 一節的 VNet 刀鋒視窗中，按一下 **子網路**tooexpand hello 子網路 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8832d-132">In hello **Settings** section of your VNet blade, click **Subnets** tooexpand hello Subnets blade.</span></span>
3. <span data-ttu-id="8832d-133">在 hello**子網路**刀鋒視窗中，按一下  **+ 閘道子網路**tooopen hello**加入子網路**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8832d-133">On hello **Subnets** blade, click **+Gateway subnet** tooopen hello **Add subnet** blade.</span></span> 
   
    <span data-ttu-id="8832d-134">![加入 hello 閘道子網路](./media/expressroute-howto-add-gateway-portal-resource-manager/addgwsubnet.png "加入 hello 閘道子網路")</span><span class="sxs-lookup"><span data-stu-id="8832d-134">![Add hello gateway subnet](./media/expressroute-howto-add-gateway-portal-resource-manager/addgwsubnet.png "Add hello gateway subnet")</span></span>


4. <span data-ttu-id="8832d-135">hello**名稱**對於您的子網路會自動填入 hello 值 'GatewaySubnet'。</span><span class="sxs-lookup"><span data-stu-id="8832d-135">hello **Name** for your subnet is automatically filled in with hello value 'GatewaySubnet'.</span></span> <span data-ttu-id="8832d-136">為了讓 Azure toorecognize hello 子網路時需要這個值為 hello 閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="8832d-136">This value is required in order for Azure toorecognize hello subnet as hello gateway subnet.</span></span> <span data-ttu-id="8832d-137">調整自動填滿的 hello**位址範圍**值 toomatch 組態需求。</span><span class="sxs-lookup"><span data-stu-id="8832d-137">Adjust hello auto-filled **Address range** values toomatch your configuration requirements.</span></span> <span data-ttu-id="8832d-138">建議您以 /27 或更大的值 (/26、/25 等) 建立閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="8832d-138">We recommend creating a gateway subnet with a /27 or larger (/26, /25, etc.).</span></span> <span data-ttu-id="8832d-139">然後，按一下 **確定**toosave hello 值，並建立 hello 閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="8832d-139">Then, click **OK** toosave hello values and create hello gateway subnet.</span></span>

    <span data-ttu-id="8832d-140">![加入 hello 子網路](./media/expressroute-howto-add-gateway-portal-resource-manager/addsubnetgw.png "加入 hello 子網路")</span><span class="sxs-lookup"><span data-stu-id="8832d-140">![Adding hello subnet](./media/expressroute-howto-add-gateway-portal-resource-manager/addsubnetgw.png "Adding hello subnet")</span></span>

## <a name="create-hello-virtual-network-gateway"></a><span data-ttu-id="8832d-141">建立 hello 虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="8832d-141">Create hello virtual network gateway</span></span>

1. <span data-ttu-id="8832d-142">在 hello 入口網站，在 hello 左邊，按一下   **+** 在搜尋中輸入虛擬網路閘道 '。</span><span class="sxs-lookup"><span data-stu-id="8832d-142">In hello portal, on hello left side, click **+** and type 'Virtual Network Gateway' in search.</span></span> <span data-ttu-id="8832d-143">找出**虛擬網路閘道**hello 搜尋中傳回，並按一下 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="8832d-143">Locate **Virtual network gateway** in hello search return and click hello entry.</span></span> <span data-ttu-id="8832d-144">在 hello**虛擬網路閘道**刀鋒視窗中，按一下 **建立**在 hello hello 刀鋒視窗的底部。</span><span class="sxs-lookup"><span data-stu-id="8832d-144">On hello **Virtual network gateway** blade, click **Create** at hello bottom of hello blade.</span></span> <span data-ttu-id="8832d-145">這會開啟 hello**建立虛擬網路閘道**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8832d-145">This opens hello **Create virtual network gateway** blade.</span></span>
2. <span data-ttu-id="8832d-146">在 hello**建立虛擬網路閘道**刀鋒視窗中，您的虛擬網路閘道的 hello 值中的填滿。</span><span class="sxs-lookup"><span data-stu-id="8832d-146">On hello **Create virtual network gateway** blade, fill in hello values for your virtual network gateway.</span></span>

    <span data-ttu-id="8832d-147">![建立虛擬網路閘道刀鋒視窗欄位](./media/expressroute-howto-add-gateway-portal-resource-manager/gw.png "建立虛擬網路閘道刀鋒視窗欄位")</span><span class="sxs-lookup"><span data-stu-id="8832d-147">![Create virtual network gateway blade fields](./media/expressroute-howto-add-gateway-portal-resource-manager/gw.png "Create virtual network gateway blade fields")</span></span>
3. <span data-ttu-id="8832d-148">**名稱**：為您的閘道命名。</span><span class="sxs-lookup"><span data-stu-id="8832d-148">**Name**: Name your gateway.</span></span> <span data-ttu-id="8832d-149">這不是 hello 與命名閘道子網路相同。</span><span class="sxs-lookup"><span data-stu-id="8832d-149">This is not hello same as naming a gateway subnet.</span></span> <span data-ttu-id="8832d-150">它的 hello 您所建立的 hello 閘道物件名稱。</span><span class="sxs-lookup"><span data-stu-id="8832d-150">It's hello name of hello gateway object you are creating.</span></span>
4. <span data-ttu-id="8832d-151">**閘道類型**︰選取 [ExpressRoute]。</span><span class="sxs-lookup"><span data-stu-id="8832d-151">**Gateway type**: Select **ExpressRoute**.</span></span>
5. <span data-ttu-id="8832d-152">**SKU**： 從 hello 下拉式清單中選取 hello 閘道 SKU。</span><span class="sxs-lookup"><span data-stu-id="8832d-152">**SKU**: Select hello gateway SKU from hello dropdown.</span></span>
6. <span data-ttu-id="8832d-153">**位置**： 調整 hello**位置**欄位 toopoint toohello 位置虛擬網路所在的位置。</span><span class="sxs-lookup"><span data-stu-id="8832d-153">**Location**: Adjust hello **Location** field toopoint toohello location where your virtual network is located.</span></span> <span data-ttu-id="8832d-154">Hello 位置並未指向 toohello 區域虛擬網路所在的位置，如果 hello 虛擬網路不會出現在下拉式清單中 「 選擇虛擬網路' hello。</span><span class="sxs-lookup"><span data-stu-id="8832d-154">If hello location is not pointing toohello region where your virtual network resides, hello virtual network doesn't appear in hello 'Choose a virtual network' dropdown.</span></span>
7. <span data-ttu-id="8832d-155">選擇 hello 虛擬網路 toowhich 想 tooadd 此閘道。</span><span class="sxs-lookup"><span data-stu-id="8832d-155">Choose hello virtual network toowhich you want tooadd this gateway.</span></span> <span data-ttu-id="8832d-156">按一下**虛擬網路**tooopen hello**選擇虛擬網路**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8832d-156">Click **Virtual network** tooopen hello **Choose a virtual network** blade.</span></span> <span data-ttu-id="8832d-157">選取 hello VNet。</span><span class="sxs-lookup"><span data-stu-id="8832d-157">Select hello VNet.</span></span> <span data-ttu-id="8832d-158">如果您沒有看到您的 VNet，請確定 hello**位置**欄位指向您的虛擬網路所在的 toohello 區域。</span><span class="sxs-lookup"><span data-stu-id="8832d-158">If you don't see your VNet, make sure hello **Location** field is pointing toohello region in which your virtual network is located.</span></span>
9. <span data-ttu-id="8832d-159">選擇公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8832d-159">Choose a public IP address.</span></span> <span data-ttu-id="8832d-160">按一下**公用 IP 位址**tooopen hello**選擇公用 IP 位址**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8832d-160">Click **Public IP address** tooopen hello **Choose public IP address** blade.</span></span> <span data-ttu-id="8832d-161">按一下**+ 建立新**tooopen hello**建立公用 IP 位址 刀鋒視窗**。</span><span class="sxs-lookup"><span data-stu-id="8832d-161">Click **+Create New** tooopen hello **Create public IP address blade**.</span></span> <span data-ttu-id="8832d-162">輸入公用 IP 位址的名稱。</span><span class="sxs-lookup"><span data-stu-id="8832d-162">Input a name for your public IP address.</span></span> <span data-ttu-id="8832d-163">此刀鋒視窗中建立的公用 IP 位址動態指派公用 IP 位址物件 toowhich。</span><span class="sxs-lookup"><span data-stu-id="8832d-163">This blade creates a public IP address object toowhich a public IP address will be dynamically assigned.</span></span> <span data-ttu-id="8832d-164">按一下**確定**toosave 您變更 toothis 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="8832d-164">Click **OK** toosave your changes toothis blade.</span></span>
10. <span data-ttu-id="8832d-165">**訂用帳戶**： 確認該 hello 正確選取訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8832d-165">**Subscription**: Verify that hello correct subscription is selected.</span></span>
11. <span data-ttu-id="8832d-166">**資源群組**： 此設定由 hello 您選取的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="8832d-166">**Resource group**: This setting is determined by hello Virtual Network that you select.</span></span>
12. <span data-ttu-id="8832d-167">不會調整 hello**位置**您所指定 hello 先前的設定之後。</span><span class="sxs-lookup"><span data-stu-id="8832d-167">Don't adjust hello **Location** after you've specified hello previous settings.</span></span>
13. <span data-ttu-id="8832d-168">請確認 hello 設定。</span><span class="sxs-lookup"><span data-stu-id="8832d-168">Verify hello settings.</span></span> <span data-ttu-id="8832d-169">如果您希望您的閘道 tooappear hello 儀表板上，您可以選取**Pin toodashboard**在 hello hello 刀鋒視窗的底部。</span><span class="sxs-lookup"><span data-stu-id="8832d-169">If you want your gateway tooappear on hello dashboard, you can select **Pin toodashboard** at hello bottom of hello blade.</span></span>
14. <span data-ttu-id="8832d-170">按一下**建立**toobegin 建立 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="8832d-170">Click **Create** toobegin creating hello gateway.</span></span> <span data-ttu-id="8832d-171">hello 設定會進行驗證，並將部署的 hello 閘道。</span><span class="sxs-lookup"><span data-stu-id="8832d-171">hello settings are validated and hello gateway deploys.</span></span> <span data-ttu-id="8832d-172">建立虛擬網路閘道可能佔用 too45 分鐘 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="8832d-172">Creating virtual network gateway can take up too45 minutes toocomplete.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8832d-173">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8832d-173">Next steps</span></span>
<span data-ttu-id="8832d-174">建立 hello VNet 閘道之後，您可以連結您的 VNet tooan ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="8832d-174">After you have created hello VNet gateway, you can link your VNet tooan ExpressRoute circuit.</span></span> <span data-ttu-id="8832d-175">請參閱[連結 ExpressRoute 電路的虛擬網路 tooan](expressroute-howto-linkvnet-portal-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="8832d-175">See [Link a Virtual Network tooan ExpressRoute circuit](expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>
