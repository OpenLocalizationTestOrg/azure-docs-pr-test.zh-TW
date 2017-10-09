---
title: "新增多個 VPN 閘道站對站連線 tooa VNet: Azure 入口網站： 資源管理員 |Microsoft 文件"
description: "新增多站台 S2S 連線 tooa VPN 閘道具有現有連線"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f3e8b165-f20a-42ab-afbb-bf60974bb4b1
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: cherylmc
ms.openlocfilehash: b8c9ff454967f509dcef725f8bcec8564fad9b00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection"></a><span data-ttu-id="c0085-103">新增站對站連線 tooa VNet 與現有的 VPN 閘道連線</span><span class="sxs-lookup"><span data-stu-id="c0085-103">Add a Site-to-Site connection tooa VNet with an existing VPN gateway connection</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="c0085-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c0085-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="c0085-105">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="c0085-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
> 

<span data-ttu-id="c0085-106">這篇文章會引導您使用 hello Azure 入口網站 tooadd 站台對站 (S2S) 連線 tooa VPN 閘道具有現有連線。</span><span class="sxs-lookup"><span data-stu-id="c0085-106">This article walks you through using hello Azure portal tooadd Site-to-Site (S2S) connections tooa VPN gateway that has an existing connection.</span></span> <span data-ttu-id="c0085-107">這種類型通常是連接的參照的 tooas"多站台 」 設定。</span><span class="sxs-lookup"><span data-stu-id="c0085-107">This type of connection is often referred tooas a "multi-site" configuration.</span></span> <span data-ttu-id="c0085-108">您可以加入 S2S 連線 tooa VNet 已 S2S 連線、 點對站連線或 VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="c0085-108">You can add a S2S connection tooa VNet that already has a S2S connection, Point-to-Site connection, or VNet-to-VNet connection.</span></span> <span data-ttu-id="c0085-109">新增連線有一些限制。</span><span class="sxs-lookup"><span data-stu-id="c0085-109">There are some limitations when adding connections.</span></span> <span data-ttu-id="c0085-110">檢查 hello[開始之前](#before)此發行項 tooverify 之前啟動您的組態 > 一節。</span><span class="sxs-lookup"><span data-stu-id="c0085-110">Check hello [Before you begin](#before) section in this article tooverify before you start your configuration.</span></span> 

<span data-ttu-id="c0085-111">本文適用於使用 hello Resource Manager 部署模型所建立的 tooVNets 具有 RouteBased VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="c0085-111">This article applies tooVNets created using hello Resource Manager deployment model that have a RouteBased VPN gateway.</span></span> <span data-ttu-id="c0085-112">這些步驟不會套用 tooExpressRoute /-網站共存連接組態。</span><span class="sxs-lookup"><span data-stu-id="c0085-112">These steps do not apply tooExpressRoute/Site-to-Site coexisting connection configurations.</span></span> <span data-ttu-id="c0085-113">如需有關並存連線的資訊，請參閱 [ExpressRoute/S2S 並存連線](../expressroute/expressroute-howto-coexist-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="c0085-113">See [ExpressRoute/S2S coexisting connections](../expressroute/expressroute-howto-coexist-resource-manager.md) for information about coexisting connections.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="c0085-114">部署模型和方法</span><span class="sxs-lookup"><span data-stu-id="c0085-114">Deployment models and methods</span></span>
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="c0085-115">當此組態有新文章和額外工具可以使用時，我們就會更新此資料表。</span><span class="sxs-lookup"><span data-stu-id="c0085-115">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="c0085-116">發行項可用時，我們直接連結 tooit 這個資料表中。</span><span class="sxs-lookup"><span data-stu-id="c0085-116">When an article is available, we link directly tooit from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <span data-ttu-id="c0085-117"><a name="before"></a>開始之前</span><span class="sxs-lookup"><span data-stu-id="c0085-117"><a name="before"></a>Before you begin</span></span>
<span data-ttu-id="c0085-118">請確認下列項目 hello:</span><span class="sxs-lookup"><span data-stu-id="c0085-118">Verify hello following items:</span></span>

* <span data-ttu-id="c0085-119">您尚未建立 ExpressRoute/S2S 並存連線。</span><span class="sxs-lookup"><span data-stu-id="c0085-119">You are not creating an ExpressRoute/S2S coexisting connection.</span></span>
* <span data-ttu-id="c0085-120">您已使用具有現有連線的 hello Resource Manager 部署模型所建立的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c0085-120">You have a virtual network that was created using hello Resource Manager deployment model with an existing connection.</span></span>
* <span data-ttu-id="c0085-121">您的 VNet 的 hello 虛擬網路閘道是 RouteBased。</span><span class="sxs-lookup"><span data-stu-id="c0085-121">hello virtual network gateway for your VNet is RouteBased.</span></span> <span data-ttu-id="c0085-122">如果您有 PolicyBased VPN 閘道，則必須刪除 hello 虛擬網路閘道，並建立新的 VPN 閘道為 RouteBased。</span><span class="sxs-lookup"><span data-stu-id="c0085-122">If you have a PolicyBased VPN gateway, you must delete hello virtual network gateway and create a new VPN gateway as RouteBased.</span></span>
* <span data-ttu-id="c0085-123">沒有任何 hello 位址範圍重疊任何 hello 連接到此 VNet 的 Vnet。</span><span class="sxs-lookup"><span data-stu-id="c0085-123">None of hello address ranges overlap for any of hello VNets that this VNet is connecting to.</span></span>
* <span data-ttu-id="c0085-124">您擁有相容的 VPN 裝置和人能夠 tooconfigure 它。</span><span class="sxs-lookup"><span data-stu-id="c0085-124">You have compatible VPN device and someone who is able tooconfigure it.</span></span> <span data-ttu-id="c0085-125">請參閱 [關於 VPN 裝置](vpn-gateway-about-vpn-devices.md)。</span><span class="sxs-lookup"><span data-stu-id="c0085-125">See [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span> <span data-ttu-id="c0085-126">如果您不熟悉設定 VPN 裝置，或不熟悉 hello IP 位址範圍位於您的內部部署網路組態，您需要 toocoordinate 的人可以為您提供這些詳細資料。</span><span class="sxs-lookup"><span data-stu-id="c0085-126">If you aren't familiar with configuring your VPN device, or are unfamiliar with hello IP address ranges located in your on-premises network configuration, you need toocoordinate with someone who can provide those details for you.</span></span>
* <span data-ttu-id="c0085-127">您的 VPN 裝置有對外開放的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c0085-127">You have an externally facing public IP address for your VPN device.</span></span> <span data-ttu-id="c0085-128">此 IP 位址不能位於 NAT 後方。</span><span class="sxs-lookup"><span data-stu-id="c0085-128">This IP address cannot be located behind a NAT.</span></span>

## <span data-ttu-id="c0085-129"><a name="part1"></a>第 1 部分 - 設定連線</span><span class="sxs-lookup"><span data-stu-id="c0085-129"><a name="part1"></a>Part 1 - Configure a connection</span></span>
1. <span data-ttu-id="c0085-130">從瀏覽器中，瀏覽 toohello [Azure 入口網站](http://portal.azure.com)且如有需要，使用您的 Azure 帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="c0085-130">From a browser, navigate toohello [Azure portal](http://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="c0085-131">按一下**所有資源**並找出您**虛擬網路閘道**hello 清單中的資源，然後按一下它。</span><span class="sxs-lookup"><span data-stu-id="c0085-131">Click **All resources** and locate your **virtual network gateway** from hello list of resources and click it.</span></span>
3. <span data-ttu-id="c0085-132">在 hello**虛擬網路閘道**刀鋒視窗中，按一下 **連線**。</span><span class="sxs-lookup"><span data-stu-id="c0085-132">On hello **Virtual network gateway** blade, click **Connections**.</span></span>
   
    <span data-ttu-id="c0085-133">![連接刀鋒視窗](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "連接刀鋒視窗e")</span><span class="sxs-lookup"><span data-stu-id="c0085-133">![Connections blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")</span></span><br>
4. <span data-ttu-id="c0085-134">在 hello**連線**刀鋒視窗中，按一下  **+ 加**。</span><span class="sxs-lookup"><span data-stu-id="c0085-134">On hello **Connections** blade, click **+Add**.</span></span>
   
    <span data-ttu-id="c0085-135">![新增連接按鈕](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "新增連接按鈕")</span><span class="sxs-lookup"><span data-stu-id="c0085-135">![Add connection button](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")</span></span><br>
5. <span data-ttu-id="c0085-136">在 hello**加入連接**刀鋒視窗中，填寫下列欄位的 hello:</span><span class="sxs-lookup"><span data-stu-id="c0085-136">On hello **Add connection** blade, fill out hello following fields:</span></span>
   
   * <span data-ttu-id="c0085-137">**名稱：** hello 想 toogive toohello 站台，您要建立 hello 連接的名稱。</span><span class="sxs-lookup"><span data-stu-id="c0085-137">**Name:** hello name you want toogive toohello site you are creating hello connection to.</span></span>
   * <span data-ttu-id="c0085-138">**連線類型：**選取 [站對站 (IPSec)]。</span><span class="sxs-lookup"><span data-stu-id="c0085-138">**Connection type:** Select **Site-to-site (IPsec)**.</span></span>
     
     <span data-ttu-id="c0085-139">![新增連接 刀鋒視窗](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "新增連接 刀鋒視窗")</span><span class="sxs-lookup"><span data-stu-id="c0085-139">![Add connection blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection blade")</span></span><br>

## <span data-ttu-id="c0085-140"><a name="part2"></a>第 2 部分 - 新增區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="c0085-140"><a name="part2"></a>Part 2 - Add a local network gateway</span></span>
1. <span data-ttu-id="c0085-141">按一下 [區域網路閘道] > [選擇區域網路閘道]。</span><span class="sxs-lookup"><span data-stu-id="c0085-141">Click **Local network gateway** ***Choose a local network gateway***.</span></span> <span data-ttu-id="c0085-142">這會開啟 hello**選擇區域網路閘道**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c0085-142">This will open hello **Choose local network gateway** blade.</span></span>
   
    <span data-ttu-id="c0085-143">![選擇區域網路閘道](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "選擇區域網路閘道")</span><span class="sxs-lookup"><span data-stu-id="c0085-143">![Choose local network gateway](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")</span></span><br>
2. <span data-ttu-id="c0085-144">按一下**建立新**tooopen hello**建立區域網路閘道**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c0085-144">Click **Create new** tooopen hello **Create local network gateway** blade.</span></span>
   
    <span data-ttu-id="c0085-145">![建立區域網路閘道刀鋒視窗](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "建立區域網路閘道")</span><span class="sxs-lookup"><span data-stu-id="c0085-145">![Create local network gateway blade](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")</span></span><br>
3. <span data-ttu-id="c0085-146">在 hello**建立區域網路閘道**刀鋒視窗中，填寫下列欄位的 hello:</span><span class="sxs-lookup"><span data-stu-id="c0085-146">On hello **Create local network gateway** blade, fill out hello following fields:</span></span>
   
   * <span data-ttu-id="c0085-147">**名稱：** hello 想 toogive toohello 區域網路閘道資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="c0085-147">**Name:** hello name you want toogive toohello local network gateway resource.</span></span>
   * <span data-ttu-id="c0085-148">**IP 位址：** hello hello VPN 裝置，您想要 tooconnect hello 站台上的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c0085-148">**IP address:** hello public IP address of hello VPN device on hello site that you want tooconnect to.</span></span>
   * <span data-ttu-id="c0085-149">**位址空間：** hello 位址空間的 toobe 路由 toohello 新區域網路網站。</span><span class="sxs-lookup"><span data-stu-id="c0085-149">**Address space:** hello address space that you want toobe routed toohello new local network site.</span></span>
4. <span data-ttu-id="c0085-150">按一下**確定**上 hello**建立區域網路閘道**刀鋒視窗 toosave hello 變更。</span><span class="sxs-lookup"><span data-stu-id="c0085-150">Click **OK** on hello **Create local network gateway** blade toosave hello changes.</span></span>

## <span data-ttu-id="c0085-151"><a name="part3"></a>第 3 部分-新增 hello 共用的金鑰，並建立 hello 連線</span><span class="sxs-lookup"><span data-stu-id="c0085-151"><a name="part3"></a>Part 3 - Add hello shared key and create hello connection</span></span>
1. <span data-ttu-id="c0085-152">在 hello**加入連接**刀鋒視窗中，新增您想 toouse toocreate 連線 hello 共用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="c0085-152">On hello **Add connection** blade, add hello shared key that you want toouse toocreate your connection.</span></span> <span data-ttu-id="c0085-153">您可以從您的 VPN 裝置取得 hello 共用的金鑰或組成這裡並再設定您的 VPN 裝置 toouse hello 相同的共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="c0085-153">You can either get hello shared key from your VPN device, or make one up here and then configure your VPN device toouse hello same shared key.</span></span> <span data-ttu-id="c0085-154">重要的是 hello 索引鍵是完全 hello hello 相同。</span><span class="sxs-lookup"><span data-stu-id="c0085-154">hello important thing is that hello keys are exactly hello same.</span></span>
   
    <span data-ttu-id="c0085-155">![共用金鑰](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "共用金鑰")</span><span class="sxs-lookup"><span data-stu-id="c0085-155">![Shared key](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span></span><br>
2. <span data-ttu-id="c0085-156">在 hello hello 刀鋒視窗底部，按一下 **確定**toocreate hello 連線。</span><span class="sxs-lookup"><span data-stu-id="c0085-156">At hello bottom of hello blade, click **OK** toocreate hello connection.</span></span>

## <span data-ttu-id="c0085-157"><a name="part4"></a>第 4 部分-請確認 hello VPN 連線</span><span class="sxs-lookup"><span data-stu-id="c0085-157"><a name="part4"></a>Part 4 - Verify hello VPN connection</span></span>


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="c0085-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c0085-158">Next steps</span></span>

<span data-ttu-id="c0085-159">一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c0085-159">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="c0085-160">請參閱 hello 虛擬機器[學習路徑](https://azure.microsoft.com/documentation/learning-paths/virtual-machines)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="c0085-160">See hello virtual machines [learning path](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) for more information.</span></span>
