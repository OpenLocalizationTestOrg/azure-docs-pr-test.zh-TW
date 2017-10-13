---
title: "連接虛擬網路 toomultiple 的站台，使用 VPN 閘道和 PowerShell： 傳統 |Microsoft 文件"
description: "本文將引導您完成連接多個本機內部部署站台 tooa 虛擬網路 VPN 閘道用於 hello 傳統部署模型。"
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/20/2017
ms.author: yushwang
ms.openlocfilehash: 5404b1c55ed3453b4dbc94dfd93e47c0812025f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-site-to-site-connection-tooa-vnet-with-an-existing-vpn-gateway-connection-classic"></a><span data-ttu-id="bf9b5-103">新增站對站連線 tooa VNet 與現有的 VPN 閘道連線 （傳統）</span><span class="sxs-lookup"><span data-stu-id="bf9b5-103">Add a Site-to-Site connection tooa VNet with an existing VPN gateway connection (classic)</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bf9b5-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="bf9b5-104">Azure portal</span></span>](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [<span data-ttu-id="bf9b5-105">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="bf9b5-105">PowerShell (classic)</span></span>](vpn-gateway-multi-site.md)
>
>

<span data-ttu-id="bf9b5-106">這篇文章會引導您使用 PowerShell tooadd 站台對站 (S2S) 連線 tooa VPN 閘道具有現有連線。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-106">This article walks you through using PowerShell tooadd Site-to-Site (S2S) connections tooa VPN gateway that has an existing connection.</span></span> <span data-ttu-id="bf9b5-107">這種類型通常是連接的參照的 tooas"多站台 」 設定。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-107">This type of connection is often referred tooas a "multi-site" configuration.</span></span> <span data-ttu-id="bf9b5-108">hello 本文章中的步驟適用於使用 hello 傳統部署模型 （也稱為服務管理） 建立 toovirtual 網路。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-108">hello steps in this article apply toovirtual networks created using hello classic deployment model (also known as Service Management).</span></span> <span data-ttu-id="bf9b5-109">這些步驟不會套用 tooExpressRoute /-網站共存連接組態。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-109">These steps do not apply tooExpressRoute/Site-to-Site coexisting connection configurations.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="bf9b5-110">部署模型和方法</span><span class="sxs-lookup"><span data-stu-id="bf9b5-110">Deployment models and methods</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="bf9b5-111">當此組態有新文章和額外工具可以使用時，我們就會更新此資料表。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-111">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="bf9b5-112">發行項可用時，我們直接連結 tooit 這個資料表中。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-112">When an article is available, we link directly tooit from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a><span data-ttu-id="bf9b5-113">關於連線</span><span class="sxs-lookup"><span data-stu-id="bf9b5-113">About connecting</span></span>

<span data-ttu-id="bf9b5-114">您可以連接多個內部部署站台 tooa 單一虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-114">You can connect multiple on-premises sites tooa single virtual network.</span></span> <span data-ttu-id="bf9b5-115">這對建立混合式雲端解決方案特別具有吸引力。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-115">This is especially attractive for building hybrid cloud solutions.</span></span> <span data-ttu-id="bf9b5-116">建立多網站連線 tooyour Azure 虛擬網路閘道是類似 toocreating 其他站台對站連線。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-116">Creating a multi-site connection tooyour Azure virtual network gateway is similar toocreating other Site-to-Site connections.</span></span> <span data-ttu-id="bf9b5-117">事實上，您可以使用現有的 Azure VPN 閘道，只要是動態的 hello 閘道 （路由式）。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-117">In fact, you can use an existing Azure VPN gateway, as long as hello gateway is dynamic (route-based).</span></span>

<span data-ttu-id="bf9b5-118">如果您已經有靜態閘道連接的 tooyour 虛擬網路，您可以變更 hello 閘道類型 toodynamic 無須 toorebuild hello 虛擬網路中的順序 tooaccommodate 多站台。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-118">If you already have a static gateway connected tooyour virtual network, you can change hello gateway type toodynamic without needing toorebuild hello virtual network in order tooaccommodate multi-site.</span></span> <span data-ttu-id="bf9b5-119">在變更之前 hello 路由類型，請確定您在內部部署 VPN 閘道支援路由式 VPN 組態。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-119">Before changing hello routing type, make sure that your on-premises VPN gateway supports route-based VPN configurations.</span></span>

<span data-ttu-id="bf9b5-120">![多重網站圖表](./media/vpn-gateway-multi-site/multisite.png "多重網站")</span><span class="sxs-lookup"><span data-stu-id="bf9b5-120">![multi-site diagram](./media/vpn-gateway-multi-site/multisite.png "multi-site")</span></span>

## <a name="points-tooconsider"></a><span data-ttu-id="bf9b5-121">點 tooconsider</span><span class="sxs-lookup"><span data-stu-id="bf9b5-121">Points tooconsider</span></span>

<span data-ttu-id="bf9b5-122">**您必須能夠 toouse hello 入口 toomake 變更 toothis 虛擬網路。**</span><span class="sxs-lookup"><span data-stu-id="bf9b5-122">**You won't be able toouse hello portal toomake changes toothis virtual network.**</span></span> <span data-ttu-id="bf9b5-123">您需要 toomake 變更 toohello 網路組態檔而不是使用 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-123">You need toomake changes toohello network configuration file instead of using hello portal.</span></span> <span data-ttu-id="bf9b5-124">如果您在 hello 入口網站中進行變更，他們將會覆寫您對此虛擬網路的多網站參考設定。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-124">If you make changes in hello portal, they'll overwrite your multi-site reference settings for this virtual network.</span></span>

<span data-ttu-id="bf9b5-125">您應該可以放心使用 hello 時間 hello 網路組態檔完成 hello 多網站程序。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-125">You should feel comfortable using hello network configuration file by hello time you've completed hello multi-site procedure.</span></span> <span data-ttu-id="bf9b5-126">不過，如果您有多人使用您的網路設定，您必須先 toomake 確定每個人都知悉這項限制。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-126">However, if you have multiple people working on your network configuration, you'll need toomake sure that everyone knows about this limitation.</span></span> <span data-ttu-id="bf9b5-127">這並不表示您無法完全使用 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-127">This doesn't mean that you can't use hello portal at all.</span></span> <span data-ttu-id="bf9b5-128">您可以使用它的一切，除了進行組態變更 toothis 特定虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-128">You can use it for everything else, except making configuration changes toothis particular virtual network.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bf9b5-129">開始之前</span><span class="sxs-lookup"><span data-stu-id="bf9b5-129">Before you begin</span></span>

<span data-ttu-id="bf9b5-130">開始設定之前，請確認您擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="bf9b5-130">Before you begin configuration, verify that you have hello following:</span></span>

* <span data-ttu-id="bf9b5-131">每個內部部署位置都有相容的 VPN 硬體。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-131">Compatible VPN hardware for each on-premises location.</span></span> <span data-ttu-id="bf9b5-132">請檢查[關於 VPN 裝置的虛擬網路連線](vpn-gateway-about-vpn-devices.md)tooverify 如果您想 toouse hello 裝置已知 toobe 相容。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-132">Check [About VPN Devices for Virtual Network Connectivity](vpn-gateway-about-vpn-devices.md) tooverify if hello device that you want toouse is something that is known toobe compatible.</span></span>
* <span data-ttu-id="bf9b5-133">每個 VPN 裝置都有對外的公用 IPv4 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-133">An externally facing public IPv4 IP address for each VPN device.</span></span> <span data-ttu-id="bf9b5-134">hello IP 位址不得位於 NAT 後方。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-134">hello IP address cannot be located behind a NAT.</span></span> <span data-ttu-id="bf9b5-135">這是必要條件。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-135">This is requirement.</span></span>
* <span data-ttu-id="bf9b5-136">您將需要 tooinstall hello 最新版本的 hello Azure PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-136">You'll need tooinstall hello latest version of hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="bf9b5-137">請確定您安裝 hello 服務管理 (SM) 版本中加入 toohello 資源管理員版本。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-137">Make sure you install hello Service Management (SM) version in addition toohello Resource Manager version.</span></span> <span data-ttu-id="bf9b5-138">請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-138">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="bf9b5-139">熟悉如何設定 VPN 硬體的人員。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-139">Someone who is proficient at configuring your VPN hardware.</span></span> <span data-ttu-id="bf9b5-140">您將了解 toohave 強式如何 tooconfigure 您的 VPN 裝置或沒有人使用。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-140">You'll have toohave a strong understanding of how tooconfigure your VPN device, or work with someone who does.</span></span>
* <span data-ttu-id="bf9b5-141">hello （如果您尚未建立一個） toouse 想在虛擬網路 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-141">hello IP address ranges that you want toouse for your virtual network (if you haven't already created one).</span></span>
* <span data-ttu-id="bf9b5-142">hello IP 位址範圍的每個您將要連接到的 hello 區域網路網站。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-142">hello IP address ranges for each of hello local network sites that you'll be connecting to.</span></span> <span data-ttu-id="bf9b5-143">您將需要 toomake 確定 hello IP 位址範圍的每個您想 tooconnect toodo 不重疊的 hello 區域網路網站。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-143">You'll need toomake sure that hello IP address ranges for each of hello local network sites that you want tooconnect toodo not overlap.</span></span> <span data-ttu-id="bf9b5-144">否則，hello 入口網站或 hello REST API 將會拒絕上傳的 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-144">Otherwise, hello portal or hello REST API will reject hello configuration being uploaded.</span></span><br><span data-ttu-id="bf9b5-145">例如，如果您有兩個區域網路網站都包含 hello IP 位址範圍 10.2.3.0/24，您必須具有目的地位址 10.2.3.3 的套件，Azure 可能不知道要 toosend hello 封裝 toobecause hello 位址範圍是哪一個站的台重疊。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-145">For example, if you have two local network sites that both contain hello IP address range 10.2.3.0/24 and you have a package with a destination address 10.2.3.3, Azure wouldn't know which site you want toosend hello package toobecause hello address ranges are overlapping.</span></span> <span data-ttu-id="bf9b5-146">tooprevent 路由問題，Azure 不允許您 tooupload 具有重疊範圍的組態檔。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-146">tooprevent routing issues, Azure doesn't allow you tooupload a configuration file that has overlapping ranges.</span></span>

## <a name="1-create-a-site-to-site-vpn"></a><span data-ttu-id="bf9b5-147">1.建立站對站 VPN</span><span class="sxs-lookup"><span data-stu-id="bf9b5-147">1. Create a Site-to-Site VPN</span></span>
<span data-ttu-id="bf9b5-148">如已有動態路由閘道的站對站 VPN，太棒了！</span><span class="sxs-lookup"><span data-stu-id="bf9b5-148">If you already have a Site-to-Site VPN with a dynamic routing gateway, great!</span></span> <span data-ttu-id="bf9b5-149">您可以繼續在太[hello 虛擬網路組態設定匯出](#export)。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-149">You can proceed too[Export hello virtual network configuration settings](#export).</span></span> <span data-ttu-id="bf9b5-150">如果沒有，請不要 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="bf9b5-150">If not, do hello following:</span></span>

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a><span data-ttu-id="bf9b5-151">如果您已經有站對站虛擬網路，但其有靜態 (原則式) 路由閘道：</span><span class="sxs-lookup"><span data-stu-id="bf9b5-151">If you already have a Site-to-Site virtual network, but it has a static (policy-based) routing gateway:</span></span>
1. <span data-ttu-id="bf9b5-152">變更您閘道類型 toodynamic 路由。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-152">Change your gateway type toodynamic routing.</span></span> <span data-ttu-id="bf9b5-153">多網站 VPN 需要動態 (亦稱作路由式) 路由閘道。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-153">A multi-site VPN requires a dynamic (also known as route-based) routing gateway.</span></span> <span data-ttu-id="bf9b5-154">toochange 您的閘道類型，您將需要 toofirst 刪除 hello 現有閘道，然後建立一個新。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-154">toochange your gateway type, you'll need toofirst delete hello existing gateway, then create a new one.</span></span> <span data-ttu-id="bf9b5-155">如需指示，請參閱[toochange 如何 hello VPN 閘道的路由類型](vpn-gateway-configure-vpn-gateway-mp.md)。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-155">For instructions, see [How toochange hello VPN routing type for your gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span>  
2. <span data-ttu-id="bf9b5-156">設定新的閘道，並建立 VPN 通道。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-156">Configure your new gateway and create your VPN tunnel.</span></span> <span data-ttu-id="bf9b5-157">如需指示，請參閱[hello Azure 傳統入口網站中設定 VPN 閘道](vpn-gateway-configure-vpn-gateway-mp.md)。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-157">For instructions, see [Configure a VPN Gateway in hello Azure Classic Portal](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="bf9b5-158">首先，變更您閘道類型 toodynamic 路由。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-158">First, change your gateway type toodynamic routing.</span></span>

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a><span data-ttu-id="bf9b5-159">如果您沒有站對站虛擬網路：</span><span class="sxs-lookup"><span data-stu-id="bf9b5-159">If you don't have a Site-to-Site virtual network:</span></span>
1. <span data-ttu-id="bf9b5-160">建立站對站虛擬網路使用下列指示： [hello Azure 傳統入口網站中的站對站 VPN 連線建立虛擬網路](vpn-gateway-site-to-site-create.md)。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-160">Create your Site-to-Site virtual network using these instructions: [Create a Virtual Network with a Site-to-Site VPN Connection in hello Azure Classic Portal](vpn-gateway-site-to-site-create.md).</span></span>  
2. <span data-ttu-id="bf9b5-161">使用下列指示設定動態路由閘道： [設定 VPN 閘道](vpn-gateway-configure-vpn-gateway-mp.md)。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-161">Configure a dynamic routing gateway using these instructions: [Configure a VPN Gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="bf9b5-162">要確定 tooselect**動態路由**適用於您的閘道類型。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-162">Be sure tooselect **dynamic routing** for your gateway type.</span></span>

## <span data-ttu-id="bf9b5-163"><a name="export"></a>2.匯出 hello 網路組態檔</span><span class="sxs-lookup"><span data-stu-id="bf9b5-163"><a name="export"></a>2. Export hello network configuration file</span></span>
<span data-ttu-id="bf9b5-164">藉由執行下列命令的 hello 匯出您的 Azure 網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-164">Export your Azure network configuration file by running hello following command.</span></span> <span data-ttu-id="bf9b5-165">您可以變更 hello hello 檔 tooexport tooa 不同位置的必要的位置。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-165">You can change hello location of hello file tooexport tooa different location if necessary.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-hello-network-configuration-file"></a><span data-ttu-id="bf9b5-166">3.開啟 hello 網路組態檔</span><span class="sxs-lookup"><span data-stu-id="bf9b5-166">3. Open hello network configuration file</span></span>
<span data-ttu-id="bf9b5-167">Hello 最後一個步驟中，開啟您所下載的 hello 網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-167">Open hello network configuration file that you downloaded in hello last step.</span></span> <span data-ttu-id="bf9b5-168">使用您喜歡的任何 xml 編輯器。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-168">Use any xml editor that you like.</span></span> <span data-ttu-id="bf9b5-169">hello 檔案應該看起來類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="bf9b5-169">hello file should look similar toohello following:</span></span>

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a><span data-ttu-id="bf9b5-170">4.新增多個網站參考</span><span class="sxs-lookup"><span data-stu-id="bf9b5-170">4. Add multiple site references</span></span>
<span data-ttu-id="bf9b5-171">當您新增或移除網站參考資訊時，您要進行組態變更 toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-171">When you add or remove site reference information, you'll make configuration changes toohello ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span></span> <span data-ttu-id="bf9b5-172">Azure toocreate 加入新的本機網站參考會觸發新的通道。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-172">Adding a new local site reference triggers Azure toocreate a new tunnel.</span></span> <span data-ttu-id="bf9b5-173">Hello 下列範例中，在 hello 網路組態僅適用於單一站台連線。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-173">In hello example below, hello network configuration is for a single-site connection.</span></span> <span data-ttu-id="bf9b5-174">一旦您完成變更後，請儲存 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-174">Save hello file once you have finished making your changes.</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

<span data-ttu-id="bf9b5-175">tooadd 其他網站參考資料 （建立多網站組態），只要加入其他"LocalNetworkSiteRef"字行，如以下 hello 範例所示：</span><span class="sxs-lookup"><span data-stu-id="bf9b5-175">tooadd additional site references (create a multi-site configuration), simply add additional "LocalNetworkSiteRef" lines, as shown in hello example below:</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-hello-network-configuration-file"></a><span data-ttu-id="bf9b5-176">5.匯入 hello 網路組態檔</span><span class="sxs-lookup"><span data-stu-id="bf9b5-176">5. Import hello network configuration file</span></span>
<span data-ttu-id="bf9b5-177">匯入 hello 網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-177">Import hello network configuration file.</span></span> <span data-ttu-id="bf9b5-178">當您匯入具有 hello 變更這個檔案時，將會加入 hello 新通道。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-178">When you import this file with hello changes, hello new tunnels will be added.</span></span> <span data-ttu-id="bf9b5-179">hello 通道會使用您稍早建立的 hello 動態閘道。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-179">hello tunnels will use hello dynamic gateway that you created earlier.</span></span> <span data-ttu-id="bf9b5-180">您可以使用 hello 傳統入口網站或 PowerShell tooimport hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-180">You can either use hello classic portal, or PowerShell tooimport hello file.</span></span>

## <a name="6-download-keys"></a><span data-ttu-id="bf9b5-181">6.下載金鑰</span><span class="sxs-lookup"><span data-stu-id="bf9b5-181">6. Download keys</span></span>
<span data-ttu-id="bf9b5-182">一旦新的通道新增之後，使用每個通道 hello PowerShell cmdlet ' Get AzureVNetGatewayKey' tooget hello IPsec/IKE 預先共用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-182">Once your new tunnels have been added, use hello PowerShell cmdlet 'Get-AzureVNetGatewayKey' tooget hello IPsec/IKE pre-shared keys for each tunnel.</span></span>

<span data-ttu-id="bf9b5-183">例如：</span><span class="sxs-lookup"><span data-stu-id="bf9b5-183">For example:</span></span>

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

<span data-ttu-id="bf9b5-184">如果您想要的話，您也可以使用 hello*取得虛擬網路閘道共用金鑰*REST API tooget hello 預先共用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-184">If you prefer, you can also use hello *Get Virtual Network Gateway Shared Key* REST API tooget hello pre-shared keys.</span></span>

## <a name="7-verify-your-connections"></a><span data-ttu-id="bf9b5-185">7.確認您的連線</span><span class="sxs-lookup"><span data-stu-id="bf9b5-185">7. Verify your connections</span></span>
<span data-ttu-id="bf9b5-186">檢查 hello 多網站通道狀態。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-186">Check hello multi-site tunnel status.</span></span> <span data-ttu-id="bf9b5-187">下載每個通道的 hello 金鑰之後, 您會想 tooverify 連線。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-187">After downloading hello keys for each tunnel, you'll want tooverify connections.</span></span> <span data-ttu-id="bf9b5-188">請使用 ' Get AzureVnetConnection' tooget 通道連接的虛擬網路清單，hello 下面範例所示。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-188">Use 'Get-AzureVnetConnection' tooget a list of virtual network tunnels, as shown in hello example below.</span></span> <span data-ttu-id="bf9b5-189">VNet1 是 hello VNet hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-189">VNet1 is hello name of hello VNet.</span></span>

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

<span data-ttu-id="bf9b5-190">範例傳回：</span><span class="sxs-lookup"><span data-stu-id="bf9b5-190">Example return:</span></span>

```
    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site1' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : hello connectivity state for hello local network site 'Site2' changed from Not Connected tooConnected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded
```

## <a name="next-steps"></a><span data-ttu-id="bf9b5-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bf9b5-191">Next steps</span></span>

<span data-ttu-id="bf9b5-192">toolearn 深入了解 VPN 閘道，請參閱[有關 VPN 閘道](vpn-gateway-about-vpngateways.md)。</span><span class="sxs-lookup"><span data-stu-id="bf9b5-192">toolearn more about VPN Gateways, see [About VPN Gateways](vpn-gateway-about-vpngateways.md).</span></span>