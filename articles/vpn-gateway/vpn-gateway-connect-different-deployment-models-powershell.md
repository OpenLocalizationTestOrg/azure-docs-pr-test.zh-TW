---
title: "連接傳統虛擬網路 tooAzure 資源管理員 Vnet: PowerShell |Microsoft 文件"
description: "深入了解如何 toocreate 傳統 Vnet 和資源管理員使用 VPN 閘道和 PowerShell 的 Vnet 之間的 VPN 連線"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: f17c3bf0-5cc9-4629-9928-1b72d0c9340b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: cherylmc
ms.openlocfilehash: 8b1cf6ae4becf1829fa99961c5dd09a422fcc1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a><span data-ttu-id="0d7e4-103">使用 PowerShell 從不同的部署模型連接虛擬網路</span><span class="sxs-lookup"><span data-stu-id="0d7e4-103">Connect virtual networks from different deployment models using PowerShell</span></span>



<span data-ttu-id="0d7e4-104">本文章將示範如何 tooconnect 傳統 Vnet tooResource 管理員 Vnet tooallow hello 位於彼此的 hello 不同的部署模型 toocommunicate 中的資源。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-104">This article shows you how tooconnect classic VNets tooResource Manager VNets tooallow hello resources located in hello separate deployment models toocommunicate with each other.</span></span> <span data-ttu-id="0d7e4-105">這篇文章中的 hello 步驟使用 PowerShell，但您也可以建立這個 hello Azure 入口網站使用此清單中選取 hello 發行項的組態。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-105">hello steps in this article use PowerShell, but you can also create this configuration using hello Azure portal by selecting hello article from this list.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0d7e4-106">入口網站</span><span class="sxs-lookup"><span data-stu-id="0d7e4-106">Portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="0d7e4-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d7e4-107">PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

<span data-ttu-id="0d7e4-108">連接傳統的 VNet tooa 資源管理員 VNet 是類似 tooconnecting VNet tooan 在內部部署站台位置。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-108">Connecting a classic VNet tooa Resource Manager VNet is similar tooconnecting a VNet tooan on-premises site location.</span></span> <span data-ttu-id="0d7e4-109">這兩種連線類型使用的 VPN 閘道 tooprovide 採用 IPsec/IKE 的安全通道。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-109">Both connectivity types use a VPN gateway tooprovide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="0d7e4-110">您可以在不同訂用帳戶和不同區域中的 VNet 之間建立連線。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-110">You can create a connection between VNets that are in different subscriptions and in different regions.</span></span> <span data-ttu-id="0d7e4-111">只要 hello 閘道設定使用動態或路由為基礎，您也可以連接到已連線 tooon 內部部署網路的 Vnet。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-111">You can also connect VNets that already have connections tooon-premises networks, as long as hello gateway that they have been configured with is dynamic or route-based.</span></span> <span data-ttu-id="0d7e4-112">如需 VNet 對 VNet 連線的詳細資訊，請參閱 hello [VNet 對 VNet 常見問題集](#faq)hello 本文結尾處。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-112">For more information about VNet-to-VNet connections, see hello [VNet-to-VNet FAQ](#faq) at hello end of this article.</span></span> 

<span data-ttu-id="0d7e4-113">如果您的 Vnet 中 hello 相同區域中，您可能會想 tooinstead 考慮它們使用對等互連的 VNet 連接。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-113">If your VNets are in hello same region, you may want tooinstead consider connecting them using VNet Peering.</span></span> <span data-ttu-id="0d7e4-114">VNet 對等互連不會使用 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-114">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="0d7e4-115">如需詳細資訊，請參閱 [VNet 對等互連](../virtual-network/virtual-network-peering-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-115">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> 

## <a name="before-beginning"></a><span data-ttu-id="0d7e4-116">開始之前</span><span class="sxs-lookup"><span data-stu-id="0d7e4-116">Before beginning</span></span>

<span data-ttu-id="0d7e4-117">hello 下列步驟引導您完成 hello 設定必要 tooconfigure 動態或路由型閘道的每個 VNet 和建立 hello 閘道之間的 VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-117">hello following steps walk you through hello settings necessary tooconfigure a dynamic or route-based gateway for each VNet and create a VPN connection between hello gateways.</span></span> <span data-ttu-id="0d7e4-118">此組態不支援靜態或路由式閘道。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-118">This configuration does not support static or policy-based gateways.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="0d7e4-119">必要條件</span><span class="sxs-lookup"><span data-stu-id="0d7e4-119">Prerequisites</span></span>

* <span data-ttu-id="0d7e4-120">已建立兩個 Vnet。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-120">Both VNets have already been created.</span></span>
* <span data-ttu-id="0d7e4-121">hello 的位址範圍 hello Vnet 不彼此重疊或重疊的任何 hello hello 閘道可能連接到其他連接的範圍。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-121">hello address ranges for hello VNets do not overlap with each other, or overlap with any of hello ranges for other connections that hello gateways may be connected to.</span></span>
* <span data-ttu-id="0d7e4-122">您已安裝 hello 最新版的 PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-122">You have installed hello latest PowerShell cmdlets.</span></span> <span data-ttu-id="0d7e4-123">請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-123">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span> <span data-ttu-id="0d7e4-124">請確定您安裝服務管理 (SM) hello 和 hello 資源管理員 (RM) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-124">Make sure you install both hello Service Management (SM) and hello Resource Manager (RM) cmdlets.</span></span> 

### <span data-ttu-id="0d7e4-125"><a name="exampleref"></a>設定範例</span><span class="sxs-lookup"><span data-stu-id="0d7e4-125"><a name="exampleref"></a>Example settings</span></span>

<span data-ttu-id="0d7e4-126">您可以使用這些值 toocreate 測試環境中，或參閱 toothem toobetter 了解這篇文章中的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-126">You can use these values toocreate a test environment, or refer toothem toobetter understand hello examples in this article.</span></span>

<span data-ttu-id="0d7e4-127">**傳統 VNet 設定**</span><span class="sxs-lookup"><span data-stu-id="0d7e4-127">**Classic VNet settings**</span></span>

<span data-ttu-id="0d7e4-128">VNet 名稱 = ClassicVNet </span><span class="sxs-lookup"><span data-stu-id="0d7e4-128">VNet Name = ClassicVNet</span></span> <br>
<span data-ttu-id="0d7e4-129">位置 = West US</span><span class="sxs-lookup"><span data-stu-id="0d7e4-129">Location = West US</span></span> <br>
<span data-ttu-id="0d7e4-130">虛擬網路位址空間 = 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="0d7e4-130">Virtual Network Address Spaces = 10.0.0.0/24</span></span> <br>
<span data-ttu-id="0d7e4-131">子網路 1 = 10.0.0.0/27</span><span class="sxs-lookup"><span data-stu-id="0d7e4-131">Subnet-1 = 10.0.0.0/27</span></span> <br>
<span data-ttu-id="0d7e4-132">GatewaySubnet = 10.0.0.32/29</span><span class="sxs-lookup"><span data-stu-id="0d7e4-132">GatewaySubnet = 10.0.0.32/29</span></span> <br>
<span data-ttu-id="0d7e4-133">區域網路名稱 = RMVNetLocal</span><span class="sxs-lookup"><span data-stu-id="0d7e4-133">Local Network Name = RMVNetLocal</span></span> <br>
<span data-ttu-id="0d7e4-134">GatewayType = DynamicRouting</span><span class="sxs-lookup"><span data-stu-id="0d7e4-134">GatewayType = DynamicRouting</span></span>

<span data-ttu-id="0d7e4-135">**Resource Manager VNet 設定**</span><span class="sxs-lookup"><span data-stu-id="0d7e4-135">**Resource Manager VNet settings**</span></span>

<span data-ttu-id="0d7e4-136">VNet 名稱 = RMVNet </span><span class="sxs-lookup"><span data-stu-id="0d7e4-136">VNet Name = RMVNet</span></span> <br>
<span data-ttu-id="0d7e4-137">資源群組 = RG1</span><span class="sxs-lookup"><span data-stu-id="0d7e4-137">Resource Group = RG1</span></span> <br>
<span data-ttu-id="0d7e4-138">虛擬網路的 IP 位址空間 = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="0d7e4-138">Virtual Network IP Address Spaces = 192.168.0.0/16</span></span> <br>
<span data-ttu-id="0d7e4-139">子網路 1 = 192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="0d7e4-139">Subnet-1 = 192.168.1.0/24</span></span> <br>
<span data-ttu-id="0d7e4-140">GatewaySubnet = 192.168.0.0/26</span><span class="sxs-lookup"><span data-stu-id="0d7e4-140">GatewaySubnet = 192.168.0.0/26</span></span> <br>
<span data-ttu-id="0d7e4-141">位置 = 美國東部</span><span class="sxs-lookup"><span data-stu-id="0d7e4-141">Location = East US</span></span> <br>
<span data-ttu-id="0d7e4-142">閘道公用 IP 名稱 = gwpip</span><span class="sxs-lookup"><span data-stu-id="0d7e4-142">Gateway public IP name = gwpip</span></span> <br>
<span data-ttu-id="0d7e4-143">區域網路閘道 = ClassicVNetLocal</span><span class="sxs-lookup"><span data-stu-id="0d7e4-143">Local Network Gateway = ClassicVNetLocal</span></span> <br>
<span data-ttu-id="0d7e4-144">虛擬網路閘道名稱 = RMGateway</span><span class="sxs-lookup"><span data-stu-id="0d7e4-144">Virtual Network Gateway name = RMGateway</span></span> <br>
<span data-ttu-id="0d7e4-145">閘道 IP 位址組態 = gwipconfig</span><span class="sxs-lookup"><span data-stu-id="0d7e4-145">Gateway IP addressing configuration = gwipconfig</span></span>

## <span data-ttu-id="0d7e4-146"><a name="createsmgw"></a>區段 1-設定 hello 傳統的 VNet</span><span class="sxs-lookup"><span data-stu-id="0d7e4-146"><a name="createsmgw"></a>Section 1 - Configure hello classic VNet</span></span>
### <a name="part-1---download-your-network-configuration-file"></a><span data-ttu-id="0d7e4-147">第 1 部份 - 下載您的網路組態檔</span><span class="sxs-lookup"><span data-stu-id="0d7e4-147">Part 1 - Download your network configuration file</span></span>
1. <span data-ttu-id="0d7e4-148">登入 tooyour hello PowerShell 主控台中的 Azure 帳戶使用提升權限的權限。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-148">Log in tooyour Azure account in hello PowerShell console with elevated rights.</span></span> <span data-ttu-id="0d7e4-149">hello 下列 cmdlet 會提示您輸入 hello 登入認證您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-149">hello following cmdlet prompts you for hello login credentials for your Azure Account.</span></span> <span data-ttu-id="0d7e4-150">登入之後，它會下載您的帳戶設定，使其可用 tooAzure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-150">After logging in, it downloads your account settings so that they are available tooAzure PowerShell.</span></span> <span data-ttu-id="0d7e4-151">使用 hello SM PowerShell cmdlet toocomplete hello 組態的這個部分。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-151">You use hello SM PowerShell cmdlets toocomplete this part of hello configuration.</span></span>

  ```powershell
  Add-AzureAccount
  ```
2. <span data-ttu-id="0d7e4-152">藉由執行下列命令的 hello 匯出您的 Azure 網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-152">Export your Azure network configuration file by running hello following command.</span></span> <span data-ttu-id="0d7e4-153">您可以變更 hello hello 檔 tooexport tooa 不同位置的必要的位置。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-153">You can change hello location of hello file tooexport tooa different location if necessary.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. <span data-ttu-id="0d7e4-154">開啟 hello.xml 檔案下載 tooedit 它。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-154">Open hello .xml file that you downloaded tooedit it.</span></span> <span data-ttu-id="0d7e4-155">如需 hello 網路組態檔的範例，請參閱 hello[網路組態結構描述](https://msdn.microsoft.com/library/jj157100.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-155">For an example of hello network configuration file, see hello [Network Configuration Schema](https://msdn.microsoft.com/library/jj157100.aspx).</span></span>

### <a name="part-2--verify-hello-gateway-subnet"></a><span data-ttu-id="0d7e4-156">組件 2-確認 hello 閘道子網路</span><span class="sxs-lookup"><span data-stu-id="0d7e4-156">Part 2 -Verify hello gateway subnet</span></span>
<span data-ttu-id="0d7e4-157">在 hello **Netcfg**項目，如果其中一個已尚未建立加入閘道子網路 tooyour VNet。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-157">In hello **VirtualNetworkSites** element, add a gateway subnet tooyour VNet if one has not already been created.</span></span> <span data-ttu-id="0d7e4-158">當使用 hello 網路組態檔，hello 閘道子網路必須命名為"GatewaySubnet 」 或 Azure 無法辨識，並將它當做閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-158">When working with hello network configuration file, hello gateway subnet MUST be named "GatewaySubnet" or Azure cannot recognize and use it as a gateway subnet.</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="0d7e4-159">**範例：**</span><span class="sxs-lookup"><span data-stu-id="0d7e4-159">**Example:**</span></span>

    <VirtualNetworkSites>
      <VirtualNetworkSite name="ClassicVNet" Location="West US">
        <AddressSpace>
          <AddressPrefix>10.0.0.0/24</AddressPrefix>
        </AddressSpace>
        <Subnets>
          <Subnet name="Subnet-1">
            <AddressPrefix>10.0.0.0/27</AddressPrefix>
          </Subnet>
          <Subnet name="GatewaySubnet">
            <AddressPrefix>10.0.0.32/29</AddressPrefix>
          </Subnet>
        </Subnets>
      </VirtualNetworkSite>
    </VirtualNetworkSites>

### <a name="part-3---add-hello-local-network-site"></a><span data-ttu-id="0d7e4-160">第 3 部分-加入 hello 區域網路網站</span><span class="sxs-lookup"><span data-stu-id="0d7e4-160">Part 3 - Add hello local network site</span></span>
<span data-ttu-id="0d7e4-161">hello 區域網路網站，您將加入代表 hello RM VNet toowhich 想 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-161">hello local network site you add represents hello RM VNet toowhich you want tooconnect.</span></span> <span data-ttu-id="0d7e4-162">新增**LocalNetworkSites**元素 toohello 檔案如果還不存在。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-162">Add a **LocalNetworkSites** element toohello file if one doesn't already exist.</span></span> <span data-ttu-id="0d7e4-163">此時在 hello 組態 hello VPNGatewayAddress 可以是任何有效的公用 IP 位址因為我們尚未建立 hello hello 資源管理員 VNet 閘道。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-163">At this point in hello configuration, hello VPNGatewayAddress can be any valid public IP address because we haven't yet created hello gateway for hello Resource Manager VNet.</span></span> <span data-ttu-id="0d7e4-164">一旦我們建立 hello 閘道時，我們將在 hello 正確公用 IP 位址已指派 toohello RM 閘道以取代此預留位置 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-164">Once we create hello gateway, we replace this placeholder IP address with hello correct public IP address that has been assigned toohello RM gateway.</span></span>

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-hello-vnet-with-hello-local-network-site"></a><span data-ttu-id="0d7e4-165">第 4 部分-將 hello VNet 與 hello 區域網路網站產生關聯</span><span class="sxs-lookup"><span data-stu-id="0d7e4-165">Part 4 - Associate hello VNet with hello local network site</span></span>
<span data-ttu-id="0d7e4-166">在本節中，我們在此指定您想 tooconnect hello 區域網路網站 hello VNet 對。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-166">In this section, we specify hello local network site that you want tooconnect hello VNet to.</span></span> <span data-ttu-id="0d7e4-167">在此情況下，它為 hello 稍早所參考的資源管理員 VNet。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-167">In this case, it is hello Resource Manager VNet that you referenced earlier.</span></span> <span data-ttu-id="0d7e4-168">請確定 hello 名稱相符。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-168">Make sure hello names match.</span></span> <span data-ttu-id="0d7e4-169">此步驟不會建立閘道。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-169">This step does not create a gateway.</span></span> <span data-ttu-id="0d7e4-170">它會指定將連線 hello hello 閘道的區域網路。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-170">It specifies hello local network that hello gateway will connect to.</span></span>

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-hello-file-and-upload"></a><span data-ttu-id="0d7e4-171">第 5-儲存 hello 檔案並上傳</span><span class="sxs-lookup"><span data-stu-id="0d7e4-171">Part 5 - Save hello file and upload</span></span>
<span data-ttu-id="0d7e4-172">儲存 hello 檔案，然後將它匯入 tooAzure 藉由執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-172">Save hello file, then import it tooAzure by running hello following command.</span></span> <span data-ttu-id="0d7e4-173">請確定您變更視您環境的 hello 檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-173">Make sure you change hello file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="0d7e4-174">您會看到類似的結果顯示 hello 匯入成功。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-174">You will see a similar result showing that hello import succeeded.</span></span>

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-hello-gateway"></a><span data-ttu-id="0d7e4-175">第 6-建立 hello 閘道</span><span class="sxs-lookup"><span data-stu-id="0d7e4-175">Part 6 - Create hello gateway</span></span>

<span data-ttu-id="0d7e4-176">執行此範例之前，請參閱 toohello hello 的確切名稱，Azure，您所下載的網路組態檔必須要有 toosee。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-176">Before running this example, refer toohello network configuration file that you downloaded for hello exact names that Azure expects toosee.</span></span> <span data-ttu-id="0d7e4-177">hello 網路組態檔包含傳統的虛擬網路的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-177">hello network configuration file contains hello values for your classic virtual networks.</span></span> <span data-ttu-id="0d7e4-178">有時傳統時會建立傳統的 VNet 設定中變更 Vnet hello 網路組態檔中的 hello 名稱 hello Azure 入口網站，因為 toohello hello 部署模型的差異。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-178">Sometimes hello names for classic VNets are changed in hello network configuration file when creating classic VNet settings in hello Azure portal due toohello differences in hello deployment models.</span></span> <span data-ttu-id="0d7e4-179">例如，如果您使用傳統的 VNet 名為 ' 傳統 VNet' 並建立名為 'ClassicRG' 的資源群組中的 Azure 入口網站 toocreate hello，hello 網路組態檔中包含的 hello 名稱會是轉換的 too'Group ClassicRG 傳統 VNet'。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-179">For example, if you used hello Azure portal toocreate a classic VNet named 'Classic VNet' and created it in a resource group named 'ClassicRG', hello name that is contained in hello network configuration file is converted too'Group ClassicRG Classic VNet'.</span></span> <span data-ttu-id="0d7e4-180">指定時 hello 名稱包含空格的 VNet，請使用引號括住 hello 值。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-180">When specifying hello name of a VNet that contains spaces, use quotation marks around hello value.</span></span>


<span data-ttu-id="0d7e4-181">使用下列範例 toocreate 動態路由閘道的 hello:</span><span class="sxs-lookup"><span data-stu-id="0d7e4-181">Use hello following example toocreate a dynamic routing gateway:</span></span>

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

<span data-ttu-id="0d7e4-182">您可以查看 hello 狀態 hello 閘道使用 hello **Get AzureVNetGateway** cmdlet。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-182">You can check hello status of hello gateway by using hello **Get-AzureVNetGateway** cmdlet.</span></span>

## <span data-ttu-id="0d7e4-183"><a name="creatermgw"></a>區段 2： 設定 hello RM VNet 閘道</span><span class="sxs-lookup"><span data-stu-id="0d7e4-183"><a name="creatermgw"></a>Section 2: Configure hello RM VNet gateway</span></span>
<span data-ttu-id="0d7e4-184">toocreate hello RM VNet VPN 閘道，請遵循下列指示的 hello。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-184">toocreate a VPN gateway for hello RM VNet, follow hello following instructions.</span></span> <span data-ttu-id="0d7e4-185">在擷取 hello 傳統 VNet 的閘道 hello 公用 IP 位址之後，不要開始 hello 步驟，直到。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-185">Don't start hello steps until after you have retrieved hello public IP address for hello classic VNet's gateway.</span></span> 

1. <span data-ttu-id="0d7e4-186">登入 tooyour hello PowerShell 主控台中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-186">Log in tooyour Azure account in hello PowerShell console.</span></span> <span data-ttu-id="0d7e4-187">hello 下列 cmdlet 會提示您輸入 hello 登入認證您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-187">hello following cmdlet prompts you for hello login credentials for your Azure Account.</span></span> <span data-ttu-id="0d7e4-188">登入之後，使其可用 tooAzure PowerShell，會下載您的帳戶設定。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-188">After logging in, your account settings are downloaded so that they are available tooAzure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  <span data-ttu-id="0d7e4-189">如果您有多個訂用帳戶，請取得 Azure 訂用帳戶的清單。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-189">Get a list of your Azure subscriptions if you have more than one subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
   
  <span data-ttu-id="0d7e4-190">指定您想 toouse hello 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-190">Specify hello subscription that you want toouse.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="0d7e4-191">建立區域網路閘道。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-191">Create a local network gateway.</span></span> <span data-ttu-id="0d7e4-192">在虛擬網路中，hello 區域網路閘道通常是指 tooyour 在內部部署位置。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-192">In a virtual network, hello local network gateway typically refers tooyour on-premises location.</span></span> <span data-ttu-id="0d7e4-193">在此情況下，hello 區域網路閘道是指 tooyour 傳統的 VNet。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-193">In this case, hello local network gateway refers tooyour Classic VNet.</span></span> <span data-ttu-id="0d7e4-194">指定的名稱之 Azure，請參閱 tooit，和也指定 hello 位址空間前置詞。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-194">Give it a name by which Azure can refer tooit, and also specify hello address space prefix.</span></span> <span data-ttu-id="0d7e4-195">Azure 會使用您指定哪些流量 toosend tooyour 內部部署位置 tooidentify hello IP 位址首碼。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-195">Azure uses hello IP address prefix you specify tooidentify which traffic toosend tooyour on-premises location.</span></span> <span data-ttu-id="0d7e4-196">如果您需要 tooadjust hello 資訊之後，再建立您的閘道，您可以修改 hello 值和執行的 hello 範例一次。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-196">If you need tooadjust hello information here later, before creating your gateway, you can modify hello values and run hello sample again.</span></span>
   
   <span data-ttu-id="0d7e4-197">**-名稱**是您希望 tooassign toorefer toohello 區域網路閘道的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-197">**-Name** is hello name you want tooassign toorefer toohello local network gateway.</span></span><br><span data-ttu-id="0d7e4-198">
   **-AddressPrefix**為 hello 傳統 VNet 位址空間。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-198">
   **-AddressPrefix** is hello Address Space for your classic VNet.</span></span><br><span data-ttu-id="0d7e4-199">
**-GatewayIpAddress** hello 公用 IP 位址的 hello 傳統 VNet 的閘道。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-199">
**-GatewayIpAddress** is hello public IP address of hello classic VNet's gateway.</span></span> <span data-ttu-id="0d7e4-200">請務必 toochange hello 以下的範例 tooreflect hello 正確的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-200">Be sure toochange hello following sample tooreflect hello correct IP address.</span></span><br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. <span data-ttu-id="0d7e4-201">要求的公用 IP 位址 toobe 配置的 toohello 虛擬網路閘道 hello 資源管理員的 VNet。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-201">Request a public IP address toobe allocated toohello virtual network gateway for hello Resource Manager VNet.</span></span> <span data-ttu-id="0d7e4-202">您無法指定您想 toouse hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-202">You can't specify hello IP address that you want toouse.</span></span> <span data-ttu-id="0d7e4-203">hello IP 位址是以動態方式配置 toohello 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-203">hello IP address is dynamically allocated toohello virtual network gateway.</span></span> <span data-ttu-id="0d7e4-204">不過，這不表示 hello 的 IP 位址變更。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-204">However, this does not mean hello IP address changes.</span></span> <span data-ttu-id="0d7e4-205">hello 虛擬網路閘道的 IP 位址變更為當 hello 閘道 hello 才會刪除並重新建立。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-205">hello only time hello virtual network gateway IP address changes is when hello gateway is deleted and recreated.</span></span> <span data-ttu-id="0d7e4-206">它不會在調整大小、 重設，或其他內部維護/升級 hello 閘道的變更。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-206">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of hello gateway.</span></span>

  <span data-ttu-id="0d7e4-207">在此步驟中，我們也會設定用於後續步驟中的變數。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-207">In this step, we also set a variable that is used in a later step.</span></span>

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. <span data-ttu-id="0d7e4-208">確認您的虛擬網路有閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-208">Verify that your virtual network has a gateway subnet.</span></span> <span data-ttu-id="0d7e4-209">如果閘道器子網路不存在，請新增一個。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-209">If no gateway subnet exists, add one.</span></span> <span data-ttu-id="0d7e4-210">請確定名為 hello 閘道子網路*GatewaySubnet*。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-210">Make sure hello gateway subnet is named *GatewaySubnet*.</span></span>
5. <span data-ttu-id="0d7e4-211">擷取用於 hello 閘道，藉由執行下列命令的 hello hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-211">Retrieve hello subnet used for hello gateway by running hello following command.</span></span> <span data-ttu-id="0d7e4-212">在此步驟中，我們也會設定變數的 toobe hello 下一個步驟中所使用。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-212">In this step, we also set a variable toobe used in hello next step.</span></span>
   
   <span data-ttu-id="0d7e4-213">**-名稱**hello 的 VNet 的資源管理員的名稱。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-213">**-Name** is hello name of your Resource Manager VNet.</span></span><br><span data-ttu-id="0d7e4-214">
   **-ResourceGroupName**為 hello 資源群組 VNet 相關聯的 hello。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-214">
**-ResourceGroupName** is hello resource group that hello VNet is associated with.</span></span> <span data-ttu-id="0d7e4-215">hello 閘道子網路用於此 VNet 必須已經存在，以及必須命名為*GatewaySubnet* toowork 正確。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-215">hello gateway subnet must already exist for this VNet and must be named *GatewaySubnet* toowork properly.</span></span><br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. <span data-ttu-id="0d7e4-216">建立 hello 閘道 IP 位址組態。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-216">Create hello gateway IP addressing configuration.</span></span> <span data-ttu-id="0d7e4-217">hello 閘道組態會定義 hello 子網路和公用 IP 位址 toouse hello。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-217">hello gateway configuration defines hello subnet and hello public IP address toouse.</span></span> <span data-ttu-id="0d7e4-218">使用下列範例 toocreate hello 閘道設定。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-218">Use hello following sample toocreate your gateway configuration.</span></span>

  <span data-ttu-id="0d7e4-219">在此步驟中，hello **-SubnetId**和**-PublicIpAddressId**參數必須傳遞 hello id 屬性從 hello 子網路和 IP 位址的物件，分別。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-219">In this step, hello **-SubnetId** and **-PublicIpAddressId** parameters must be passed hello id property from hello subnet, and IP address objects, respectively.</span></span> <span data-ttu-id="0d7e4-220">您無法使用簡單的字串。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-220">You can't use a simple string.</span></span> <span data-ttu-id="0d7e4-221">這些變數會設定在 hello 步驟 toorequest 公用 IP 並 hello 步驟 tooretrieve hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-221">These variables are set in hello step toorequest a public IP and hello step tooretrieve hello subnet.</span></span>

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. <span data-ttu-id="0d7e4-222">執行下列命令的 hello 建立 hello 資源管理員虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-222">Create hello Resource Manager virtual network gateway by running hello following command.</span></span> <span data-ttu-id="0d7e4-223">hello`-VpnType`必須*RouteBased*。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-223">hello `-VpnType` must be *RouteBased*.</span></span> <span data-ttu-id="0d7e4-224">可能需要 45 分鐘或更 hello 閘道 toocreate。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-224">It can take 45 minutes or more for hello gateway toocreate.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. <span data-ttu-id="0d7e4-225">一旦建立 hello VPN 閘道，請複製 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-225">Copy hello public IP address once hello VPN gateway has been created.</span></span> <span data-ttu-id="0d7e4-226">您使用它時設定傳統 VNet 的 hello 區域網路設定。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-226">You use it when you configure hello local network settings for your Classic VNet.</span></span> <span data-ttu-id="0d7e4-227">您可以使用下列 cmdlet tooretrieve hello 公用 IP 位址的 hello。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-227">You can use hello following cmdlet tooretrieve hello public IP address.</span></span> <span data-ttu-id="0d7e4-228">hello 公用 IP 位址會列示在 hello 做為傳回*IpAddress*。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-228">hello public IP address is listed in hello return as *IpAddress*.</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-hello-classic-vnet-local-site-settings"></a><span data-ttu-id="0d7e4-229">第 3 節： 修改 hello 傳統 VNet 本機站台設定</span><span class="sxs-lookup"><span data-stu-id="0d7e4-229">Section 3: Modify hello classic VNet local site settings</span></span>

<span data-ttu-id="0d7e4-230">在本節中，您使用 hello 傳統的 VNet。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-230">In this section, you work with hello classic VNet.</span></span> <span data-ttu-id="0d7e4-231">您要取代指定 hello 本機站台設定，將會使用的 tooconnect toohello 資源管理員 VNet 閘道時所使用的 hello 預留位置 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-231">You replace hello placeholder IP address that you used when specifying hello local site settings that will be used tooconnect toohello Resource Manager VNet gateway.</span></span> 

1. <span data-ttu-id="0d7e4-232">匯出 hello 網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-232">Export hello network configuration file.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. <span data-ttu-id="0d7e4-233">使用文字編輯器，修改 VPNGatewayAddress hello 值。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-233">Using a text editor, modify hello value for VPNGatewayAddress.</span></span> <span data-ttu-id="0d7e4-234">Hello 預留位置 IP 位址取代 hello 資源管理員閘道的 hello 公用 IP 位址，然後儲存 hello 的變更。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-234">Replace hello placeholder IP address with hello public IP address of hello Resource Manager gateway and then save hello changes.</span></span>

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. <span data-ttu-id="0d7e4-235">匯入 hello 修改網路設定檔 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-235">Import hello modified network configuration file tooAzure.</span></span>

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <span data-ttu-id="0d7e4-236"><a name="connect"></a>區段 4： 建立 hello 閘道之間的連接</span><span class="sxs-lookup"><span data-stu-id="0d7e4-236"><a name="connect"></a>Section 4: Create a connection between hello gateways</span></span>
<span data-ttu-id="0d7e4-237">建立 hello 閘道之間的連線需要 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-237">Creating a connection between hello gateways requires PowerShell.</span></span> <span data-ttu-id="0d7e4-238">您可能需要 tooadd 您 Azure 帳戶 toouse hello 精簡 hello PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-238">You may need tooadd your Azure Account toouse hello classic version of hello  PowerShell cmdlets.</span></span> <span data-ttu-id="0d7e4-239">因此，使用 toodo **Add-azureaccount**。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-239">toodo so, use **Add-AzureAccount**.</span></span>

1. <span data-ttu-id="0d7e4-240">在 hello PowerShell 主控台中，設定您的共用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-240">In hello PowerShell console, set your shared key.</span></span> <span data-ttu-id="0d7e4-241">在執行之前 hello 指令程式，請參閱 toohello hello 的確切名稱，Azure，您所下載的網路組態檔必須要有 toosee。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-241">Before running hello cmdlets, refer toohello network configuration file that you downloaded for hello exact names that Azure expects toosee.</span></span> <span data-ttu-id="0d7e4-242">在指定 hello 名稱包含空格的 VNet，使用單一引號括住 hello 值。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-242">When specifying hello name of a VNet that contains spaces, use single quotation marks around hello value.</span></span><br><br><span data-ttu-id="0d7e4-243">在下列範例中， **-VNetName** hello hello 名稱傳統 VNet 和**-LocalNetworkSiteName** hello 您為 hello 區域網路網站指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-243">In following example, **-VNetName** is hello name of hello classic VNet and **-LocalNetworkSiteName** is hello name you specified for hello local network site.</span></span> <span data-ttu-id="0d7e4-244">hello **-SharedKey**是產生及指定的值。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-244">hello **-SharedKey** is a value that you generate and specify.</span></span> <span data-ttu-id="0d7e4-245">在 hello 範例中，我們使用 'abc123'，但您可以產生並使用更複雜的項目。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-245">In hello example, we used 'abc123', but you can generate and use something more complex.</span></span> <span data-ttu-id="0d7e4-246">hello 重要件事就是您在此處指定的 hello 該值必須是相同的值建立您的連線時，指定 hello 下一個步驟中的 hello。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-246">hello important thing is that hello value you specify here must be hello same value that you specify in hello next step when you create your connection.</span></span> <span data-ttu-id="0d7e4-247">應該會顯示 hello 傳回**狀態： 成功**。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-247">hello return should show **Status: Successful**.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. <span data-ttu-id="0d7e4-248">執行下列命令的 hello 建立 hello VPN 連線：</span><span class="sxs-lookup"><span data-stu-id="0d7e4-248">Create hello VPN connection by running hello following commands:</span></span>
   
  <span data-ttu-id="0d7e4-249">設定 hello 變數。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-249">Set hello variables.</span></span>

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  <span data-ttu-id="0d7e4-250">建立 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-250">Create hello connection.</span></span> <span data-ttu-id="0d7e4-251">請注意該 hello **-ConnectionType**是 IPsec 不 Vnet2Vnet。</span><span class="sxs-lookup"><span data-stu-id="0d7e4-251">Notice that hello **-ConnectionType** is IPsec, not Vnet2Vnet.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a><span data-ttu-id="0d7e4-252">第 5 節︰驗證您的連線</span><span class="sxs-lookup"><span data-stu-id="0d7e4-252">Section 5: Verify your connections</span></span>

### <a name="tooverify-hello-connection-from-your-classic-vnet-tooyour-resource-manager-vnet"></a><span data-ttu-id="0d7e4-253">從傳統 VNet tooyour 資源管理員 VNet tooverify hello 連線</span><span class="sxs-lookup"><span data-stu-id="0d7e4-253">tooverify hello connection from your classic VNet tooyour Resource Manager VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="0d7e4-254">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d7e4-254">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="0d7e4-255">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0d7e4-255">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="tooverify-hello-connection-from-your-resource-manager-vnet-tooyour-classic-vnet"></a><span data-ttu-id="0d7e4-256">從資源管理員 VNet tooyour tooverify hello 連接傳統的 VNet</span><span class="sxs-lookup"><span data-stu-id="0d7e4-256">tooverify hello connection from your Resource Manager VNet tooyour classic VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="0d7e4-257">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0d7e4-257">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="0d7e4-258">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0d7e4-258">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="0d7e4-259"><a name="faq"></a>VNet 對 VNet 常見問題集</span><span class="sxs-lookup"><span data-stu-id="0d7e4-259"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

