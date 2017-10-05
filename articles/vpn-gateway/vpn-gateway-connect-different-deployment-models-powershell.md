---
title: "將傳統虛擬網路連接到 Azure Resource Manager VNet：PowerShell | Microsoft Docs"
description: "了解如何使用 VPN 閘道和 PowerShell 在傳統 VNet 和 Resource Manager VNet 之間建立 VPN 連線"
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
ms.openlocfilehash: 842a32e5304977af92706cdda464286983122247
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-virtual-networks-from-different-deployment-models-using-powershell"></a><span data-ttu-id="f103b-103">使用 PowerShell 從不同的部署模型連接虛擬網路</span><span class="sxs-lookup"><span data-stu-id="f103b-103">Connect virtual networks from different deployment models using PowerShell</span></span>



<span data-ttu-id="f103b-104">本文說明如何將傳統 VNet 連線到 Resource Manager VNet，以允許位於不同部署模型中的資源彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="f103b-104">This article shows you how to connect classic VNets to Resource Manager VNets to allow the resources located in the separate deployment models to communicate with each other.</span></span> <span data-ttu-id="f103b-105">本文中的步驟使用 PowerShell，但您也可以選取這份清單中的文章，進而使用 Azure 入口網站建立此組態。</span><span class="sxs-lookup"><span data-stu-id="f103b-105">The steps in this article use PowerShell, but you can also create this configuration using the Azure portal by selecting the article from this list.</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="f103b-106">入口網站</span><span class="sxs-lookup"><span data-stu-id="f103b-106">Portal</span></span>](vpn-gateway-connect-different-deployment-models-portal.md)
> * [<span data-ttu-id="f103b-107">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f103b-107">PowerShell</span></span>](vpn-gateway-connect-different-deployment-models-powershell.md)
> 
> 

<span data-ttu-id="f103b-108">將傳統 VNet 連線至 Resource Manager VNet，類似於將 VNet 連線至內部部署網站位置。</span><span class="sxs-lookup"><span data-stu-id="f103b-108">Connecting a classic VNet to a Resource Manager VNet is similar to connecting a VNet to an on-premises site location.</span></span> <span data-ttu-id="f103b-109">這兩種連線類型都使用 VPN 閘道提供使用 IPsec/IKE 的安全通道。</span><span class="sxs-lookup"><span data-stu-id="f103b-109">Both connectivity types use a VPN gateway to provide a secure tunnel using IPsec/IKE.</span></span> <span data-ttu-id="f103b-110">您可以在不同訂用帳戶和不同區域中的 VNet 之間建立連線。</span><span class="sxs-lookup"><span data-stu-id="f103b-110">You can create a connection between VNets that are in different subscriptions and in different regions.</span></span> <span data-ttu-id="f103b-111">只要設定的閘道是動態或路由式，您也可以連接已連線到內部部署網路的 Vnet。</span><span class="sxs-lookup"><span data-stu-id="f103b-111">You can also connect VNets that already have connections to on-premises networks, as long as the gateway that they have been configured with is dynamic or route-based.</span></span> <span data-ttu-id="f103b-112">如需 VNet 對 VNet 連線的詳細資訊，請參閱本文結尾處的 [VNet 對 VNet 常見問題集](#faq) 。</span><span class="sxs-lookup"><span data-stu-id="f103b-112">For more information about VNet-to-VNet connections, see the [VNet-to-VNet FAQ](#faq) at the end of this article.</span></span> 

<span data-ttu-id="f103b-113">如果您的 VNet 位在相同區域，可以會改為考慮使用 VNet 對等互連進行連線。</span><span class="sxs-lookup"><span data-stu-id="f103b-113">If your VNets are in the same region, you may want to instead consider connecting them using VNet Peering.</span></span> <span data-ttu-id="f103b-114">VNet 對等互連不會使用 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="f103b-114">VNet peering does not use a VPN gateway.</span></span> <span data-ttu-id="f103b-115">如需詳細資訊，請參閱 [VNet 對等互連](../virtual-network/virtual-network-peering-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f103b-115">For more information, see [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> 

## <a name="before-beginning"></a><span data-ttu-id="f103b-116">開始之前</span><span class="sxs-lookup"><span data-stu-id="f103b-116">Before beginning</span></span>

<span data-ttu-id="f103b-117">下列步驟引導您完成為每個 VNet 設定動態或路由式閘道，以及建立閘道之間的 VPN 連線所需的設定。</span><span class="sxs-lookup"><span data-stu-id="f103b-117">The following steps walk you through the settings necessary to configure a dynamic or route-based gateway for each VNet and create a VPN connection between the gateways.</span></span> <span data-ttu-id="f103b-118">此組態不支援靜態或路由式閘道。</span><span class="sxs-lookup"><span data-stu-id="f103b-118">This configuration does not support static or policy-based gateways.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="f103b-119">必要條件</span><span class="sxs-lookup"><span data-stu-id="f103b-119">Prerequisites</span></span>

* <span data-ttu-id="f103b-120">已建立兩個 Vnet。</span><span class="sxs-lookup"><span data-stu-id="f103b-120">Both VNets have already been created.</span></span>
* <span data-ttu-id="f103b-121">Vnet 的位址範圍不會彼此重疊，或與閘道可能連接的任何其他連線範圍重疊。</span><span class="sxs-lookup"><span data-stu-id="f103b-121">The address ranges for the VNets do not overlap with each other, or overlap with any of the ranges for other connections that the gateways may be connected to.</span></span>
* <span data-ttu-id="f103b-122">您已安裝最新的 PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f103b-122">You have installed the latest PowerShell cmdlets.</span></span> <span data-ttu-id="f103b-123">如需詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview) 。</span><span class="sxs-lookup"><span data-stu-id="f103b-123">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span> <span data-ttu-id="f103b-124">確定安裝服務管理 (SM) 和 Resource Manager (RM) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f103b-124">Make sure you install both the Service Management (SM) and the Resource Manager (RM) cmdlets.</span></span> 

### <span data-ttu-id="f103b-125"><a name="exampleref"></a>設定範例</span><span class="sxs-lookup"><span data-stu-id="f103b-125"><a name="exampleref"></a>Example settings</span></span>

<span data-ttu-id="f103b-126">您可以使用這些值來建立測試環境，或參考這些值，進一步了解本文中的範例。</span><span class="sxs-lookup"><span data-stu-id="f103b-126">You can use these values to create a test environment, or refer to them to better understand the examples in this article.</span></span>

<span data-ttu-id="f103b-127">**傳統 VNet 設定**</span><span class="sxs-lookup"><span data-stu-id="f103b-127">**Classic VNet settings**</span></span>

<span data-ttu-id="f103b-128">VNet 名稱 = ClassicVNet </span><span class="sxs-lookup"><span data-stu-id="f103b-128">VNet Name = ClassicVNet</span></span> <br>
<span data-ttu-id="f103b-129">位置 = West US</span><span class="sxs-lookup"><span data-stu-id="f103b-129">Location = West US</span></span> <br>
<span data-ttu-id="f103b-130">虛擬網路位址空間 = 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="f103b-130">Virtual Network Address Spaces = 10.0.0.0/24</span></span> <br>
<span data-ttu-id="f103b-131">子網路 1 = 10.0.0.0/27</span><span class="sxs-lookup"><span data-stu-id="f103b-131">Subnet-1 = 10.0.0.0/27</span></span> <br>
<span data-ttu-id="f103b-132">GatewaySubnet = 10.0.0.32/29</span><span class="sxs-lookup"><span data-stu-id="f103b-132">GatewaySubnet = 10.0.0.32/29</span></span> <br>
<span data-ttu-id="f103b-133">區域網路名稱 = RMVNetLocal</span><span class="sxs-lookup"><span data-stu-id="f103b-133">Local Network Name = RMVNetLocal</span></span> <br>
<span data-ttu-id="f103b-134">GatewayType = DynamicRouting</span><span class="sxs-lookup"><span data-stu-id="f103b-134">GatewayType = DynamicRouting</span></span>

<span data-ttu-id="f103b-135">**Resource Manager VNet 設定**</span><span class="sxs-lookup"><span data-stu-id="f103b-135">**Resource Manager VNet settings**</span></span>

<span data-ttu-id="f103b-136">VNet 名稱 = RMVNet </span><span class="sxs-lookup"><span data-stu-id="f103b-136">VNet Name = RMVNet</span></span> <br>
<span data-ttu-id="f103b-137">資源群組 = RG1</span><span class="sxs-lookup"><span data-stu-id="f103b-137">Resource Group = RG1</span></span> <br>
<span data-ttu-id="f103b-138">虛擬網路的 IP 位址空間 = 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="f103b-138">Virtual Network IP Address Spaces = 192.168.0.0/16</span></span> <br>
<span data-ttu-id="f103b-139">子網路 1 = 192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="f103b-139">Subnet-1 = 192.168.1.0/24</span></span> <br>
<span data-ttu-id="f103b-140">GatewaySubnet = 192.168.0.0/26</span><span class="sxs-lookup"><span data-stu-id="f103b-140">GatewaySubnet = 192.168.0.0/26</span></span> <br>
<span data-ttu-id="f103b-141">位置 = 美國東部</span><span class="sxs-lookup"><span data-stu-id="f103b-141">Location = East US</span></span> <br>
<span data-ttu-id="f103b-142">閘道公用 IP 名稱 = gwpip</span><span class="sxs-lookup"><span data-stu-id="f103b-142">Gateway public IP name = gwpip</span></span> <br>
<span data-ttu-id="f103b-143">區域網路閘道 = ClassicVNetLocal</span><span class="sxs-lookup"><span data-stu-id="f103b-143">Local Network Gateway = ClassicVNetLocal</span></span> <br>
<span data-ttu-id="f103b-144">虛擬網路閘道名稱 = RMGateway</span><span class="sxs-lookup"><span data-stu-id="f103b-144">Virtual Network Gateway name = RMGateway</span></span> <br>
<span data-ttu-id="f103b-145">閘道 IP 位址組態 = gwipconfig</span><span class="sxs-lookup"><span data-stu-id="f103b-145">Gateway IP addressing configuration = gwipconfig</span></span>

## <span data-ttu-id="f103b-146"><a name="createsmgw"></a>區段 1 - 設定傳統 VNet</span><span class="sxs-lookup"><span data-stu-id="f103b-146"><a name="createsmgw"></a>Section 1 - Configure the classic VNet</span></span>
### <a name="part-1---download-your-network-configuration-file"></a><span data-ttu-id="f103b-147">第 1 部份 - 下載您的網路組態檔</span><span class="sxs-lookup"><span data-stu-id="f103b-147">Part 1 - Download your network configuration file</span></span>
1. <span data-ttu-id="f103b-148">在 PowerShell 主控台中以提高的權限登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f103b-148">Log in to your Azure account in the PowerShell console with elevated rights.</span></span> <span data-ttu-id="f103b-149">下列 Cmdlet 會提示您輸入 Azure 帳戶的登入認證。</span><span class="sxs-lookup"><span data-stu-id="f103b-149">The following cmdlet prompts you for the login credentials for your Azure Account.</span></span> <span data-ttu-id="f103b-150">登入之後，它會下載您的帳戶設定以供 Azure PowerShell 使用。</span><span class="sxs-lookup"><span data-stu-id="f103b-150">After logging in, it downloads your account settings so that they are available to Azure PowerShell.</span></span> <span data-ttu-id="f103b-151">您可以使用 SM PowerShell Cmdlet 來完成這個部分的設定。</span><span class="sxs-lookup"><span data-stu-id="f103b-151">You use the SM PowerShell cmdlets to complete this part of the configuration.</span></span>

  ```powershell
  Add-AzureAccount
  ```
2. <span data-ttu-id="f103b-152">執行下列命令以匯出 Azure 網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="f103b-152">Export your Azure network configuration file by running the following command.</span></span> <span data-ttu-id="f103b-153">您可以視需要變更此檔案的位置，以匯出至不同的位置。</span><span class="sxs-lookup"><span data-stu-id="f103b-153">You can change the location of the file to export to a different location if necessary.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
3. <span data-ttu-id="f103b-154">開啟您下載的 .xml 檔案加以編輯。</span><span class="sxs-lookup"><span data-stu-id="f103b-154">Open the .xml file that you downloaded to edit it.</span></span> <span data-ttu-id="f103b-155">如需網路組態檔的範例，請參閱 [網路組態結構描述](https://msdn.microsoft.com/library/jj157100.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f103b-155">For an example of the network configuration file, see the [Network Configuration Schema](https://msdn.microsoft.com/library/jj157100.aspx).</span></span>

### <a name="part-2--verify-the-gateway-subnet"></a><span data-ttu-id="f103b-156">第 2 部份 - 驗證閘道子網路</span><span class="sxs-lookup"><span data-stu-id="f103b-156">Part 2 -Verify the gateway subnet</span></span>
<span data-ttu-id="f103b-157">在 **VirtualNetworkSites** 元素中，將閘道子網路 (若已建立) 加入至您的 VNet。</span><span class="sxs-lookup"><span data-stu-id="f103b-157">In the **VirtualNetworkSites** element, add a gateway subnet to your VNet if one has not already been created.</span></span> <span data-ttu-id="f103b-158">使用網路組態檔時，閘道子網路必須命名為 "GatewaySubnet"，否則 Azure 無法辨識並將它當作閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="f103b-158">When working with the network configuration file, the gateway subnet MUST be named "GatewaySubnet" or Azure cannot recognize and use it as a gateway subnet.</span></span>

[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

<span data-ttu-id="f103b-159">**範例：**</span><span class="sxs-lookup"><span data-stu-id="f103b-159">**Example:**</span></span>

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

### <a name="part-3---add-the-local-network-site"></a><span data-ttu-id="f103b-160">步驟 3 - 新增區域網路站台</span><span class="sxs-lookup"><span data-stu-id="f103b-160">Part 3 - Add the local network site</span></span>
<span data-ttu-id="f103b-161">您新增的區域網路站台代表您要連接的 RM VNet。</span><span class="sxs-lookup"><span data-stu-id="f103b-161">The local network site you add represents the RM VNet to which you want to connect.</span></span> <span data-ttu-id="f103b-162">將 **LocalNetworkSites** 元素 (如果尚未存在) 加入至檔案。</span><span class="sxs-lookup"><span data-stu-id="f103b-162">Add a **LocalNetworkSites** element to the file if one doesn't already exist.</span></span> <span data-ttu-id="f103b-163">此時在組態中，VPNGatewayAddress 可以是任何有效的公用 IP 位址，因為我們尚未建立 Resource Manager VNet 的閘道。</span><span class="sxs-lookup"><span data-stu-id="f103b-163">At this point in the configuration, the VPNGatewayAddress can be any valid public IP address because we haven't yet created the gateway for the Resource Manager VNet.</span></span> <span data-ttu-id="f103b-164">一旦建立閘道，我們會以指派給 RM 閘道的正確公用 IP 位址取代此預留位置 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f103b-164">Once we create the gateway, we replace this placeholder IP address with the correct public IP address that has been assigned to the RM gateway.</span></span>

    <LocalNetworkSites>
      <LocalNetworkSite name="RMVNetLocal">
        <AddressSpace>
          <AddressPrefix>192.168.0.0/16</AddressPrefix>
        </AddressSpace>
        <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
      </LocalNetworkSite>
    </LocalNetworkSites>

### <a name="part-4---associate-the-vnet-with-the-local-network-site"></a><span data-ttu-id="f103b-165">第 4 部份 – 建立 VNet 與區域網路站台的關聯</span><span class="sxs-lookup"><span data-stu-id="f103b-165">Part 4 - Associate the VNet with the local network site</span></span>
<span data-ttu-id="f103b-166">在此區段中，我們會指定您要 VNet 連接的區域網路站台。</span><span class="sxs-lookup"><span data-stu-id="f103b-166">In this section, we specify the local network site that you want to connect the VNet to.</span></span> <span data-ttu-id="f103b-167">在此例中，這是您稍早參考的 Resource Manager VNet。</span><span class="sxs-lookup"><span data-stu-id="f103b-167">In this case, it is the Resource Manager VNet that you referenced earlier.</span></span> <span data-ttu-id="f103b-168">確定名稱相符。</span><span class="sxs-lookup"><span data-stu-id="f103b-168">Make sure the names match.</span></span> <span data-ttu-id="f103b-169">此步驟不會建立閘道。</span><span class="sxs-lookup"><span data-stu-id="f103b-169">This step does not create a gateway.</span></span> <span data-ttu-id="f103b-170">它會指定閘道將要連接的區域網路。</span><span class="sxs-lookup"><span data-stu-id="f103b-170">It specifies the local network that the gateway will connect to.</span></span>

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="RMVNetLocal">
              <Connection type="IPsec" />
            </LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

### <a name="part-5---save-the-file-and-upload"></a><span data-ttu-id="f103b-171">第 5 部份 - 儲存檔案並上傳</span><span class="sxs-lookup"><span data-stu-id="f103b-171">Part 5 - Save the file and upload</span></span>
<span data-ttu-id="f103b-172">儲存檔案，然後執行下列命令，將它匯入至 Azure。</span><span class="sxs-lookup"><span data-stu-id="f103b-172">Save the file, then import it to Azure by running the following command.</span></span> <span data-ttu-id="f103b-173">確定您會視需要變更環境的檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="f103b-173">Make sure you change the file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="f103b-174">您將會看到顯示已成功匯入的相似結果。</span><span class="sxs-lookup"><span data-stu-id="f103b-174">You will see a similar result showing that the import succeeded.</span></span>

        OperationDescription        OperationId                      OperationStatus                                                
        --------------------        -----------                      ---------------                                                
        Set-AzureVNetConfig        e0ee6e66-9167-cfa7-a746-7casb9    Succeeded 

### <a name="part-6---create-the-gateway"></a><span data-ttu-id="f103b-175">第 6 部分 - 建立閘道</span><span class="sxs-lookup"><span data-stu-id="f103b-175">Part 6 - Create the gateway</span></span>

<span data-ttu-id="f103b-176">執行此範例之前，請參閱您針對 Azure 預期看到的確切名稱所下載的網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="f103b-176">Before running this example, refer to the network configuration file that you downloaded for the exact names that Azure expects to see.</span></span> <span data-ttu-id="f103b-177">網路組態檔包含傳統虛擬網路的值。</span><span class="sxs-lookup"><span data-stu-id="f103b-177">The network configuration file contains the values for your classic virtual networks.</span></span> <span data-ttu-id="f103b-178">因為部署模型中的差異，當在 Azure 入口網站中建立傳統 VNet 設定時，有時候傳統 VNet 的名稱會變更。</span><span class="sxs-lookup"><span data-stu-id="f103b-178">Sometimes the names for classic VNets are changed in the network configuration file when creating classic VNet settings in the Azure portal due to the differences in the deployment models.</span></span> <span data-ttu-id="f103b-179">例如，如果您使用 Azure 入口網站在名稱為 'ClassicRG' 的資源群組中，建立一個名稱為 'Classic VNet' 的傳統 VNet，網路組態檔中所包含的名稱會轉換為 'Group ClassicRG Classic VNet'。</span><span class="sxs-lookup"><span data-stu-id="f103b-179">For example, if you used the Azure portal to create a classic VNet named 'Classic VNet' and created it in a resource group named 'ClassicRG', the name that is contained in the network configuration file is converted to 'Group ClassicRG Classic VNet'.</span></span> <span data-ttu-id="f103b-180">當指定包含空格的 VNet 名稱時，請使用引號括住值。</span><span class="sxs-lookup"><span data-stu-id="f103b-180">When specifying the name of a VNet that contains spaces, use quotation marks around the value.</span></span>


<span data-ttu-id="f103b-181">使用以下範例來建立動態路由閘道︰</span><span class="sxs-lookup"><span data-stu-id="f103b-181">Use the following example to create a dynamic routing gateway:</span></span>

```powershell
New-AzureVNetGateway -VNetName ClassicVNet -GatewayType DynamicRouting
```

<span data-ttu-id="f103b-182">您可以使用 **Get-AzureVNetGateway** Cmdlet 檢查閘道的狀態。</span><span class="sxs-lookup"><span data-stu-id="f103b-182">You can check the status of the gateway by using the **Get-AzureVNetGateway** cmdlet.</span></span>

## <span data-ttu-id="f103b-183"><a name="creatermgw"></a>區段 2 - 設定 RM VNet 閘道</span><span class="sxs-lookup"><span data-stu-id="f103b-183"><a name="creatermgw"></a>Section 2: Configure the RM VNet gateway</span></span>
<span data-ttu-id="f103b-184">若要建立 ARM VNet 的 VPN 閘道，請遵循下列指示。</span><span class="sxs-lookup"><span data-stu-id="f103b-184">To create a VPN gateway for the RM VNet, follow the following instructions.</span></span> <span data-ttu-id="f103b-185">直到您已擷取傳統 VNet 閘道的公用 IP 位址以後，才可開始下列步驟。</span><span class="sxs-lookup"><span data-stu-id="f103b-185">Don't start the steps until after you have retrieved the public IP address for the classic VNet's gateway.</span></span> 

1. <span data-ttu-id="f103b-186">在 PowerShell 主控台中登入您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="f103b-186">Log in to your Azure account in the PowerShell console.</span></span> <span data-ttu-id="f103b-187">下列 Cmdlet 會提示您輸入 Azure 帳戶的登入認證。</span><span class="sxs-lookup"><span data-stu-id="f103b-187">The following cmdlet prompts you for the login credentials for your Azure Account.</span></span> <span data-ttu-id="f103b-188">登入之後，便會下載您的帳戶設定，以供 Azure PowerShell 使用。</span><span class="sxs-lookup"><span data-stu-id="f103b-188">After logging in, your account settings are downloaded so that they are available to Azure PowerShell.</span></span>

  ```powershell
  Login-AzureRmAccount
  ``` 
   
  <span data-ttu-id="f103b-189">如果您有多個訂用帳戶，請取得 Azure 訂用帳戶的清單。</span><span class="sxs-lookup"><span data-stu-id="f103b-189">Get a list of your Azure subscriptions if you have more than one subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```
   
  <span data-ttu-id="f103b-190">指定您要使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f103b-190">Specify the subscription that you want to use.</span></span>

  ```powershell
  Select-AzureRmSubscription -SubscriptionName "Name of subscription"
  ```
2. <span data-ttu-id="f103b-191">建立區域網路閘道。</span><span class="sxs-lookup"><span data-stu-id="f103b-191">Create a local network gateway.</span></span> <span data-ttu-id="f103b-192">在虛擬網路中，區域網路閘道通常是指您的內部部署位置。</span><span class="sxs-lookup"><span data-stu-id="f103b-192">In a virtual network, the local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="f103b-193">在此例中，區域網路閘道會參考您的傳統 VNet。</span><span class="sxs-lookup"><span data-stu-id="f103b-193">In this case, the local network gateway refers to your Classic VNet.</span></span> <span data-ttu-id="f103b-194">賦予它一個可供 Azure 參考的名稱，並且指定位址空間前置詞。</span><span class="sxs-lookup"><span data-stu-id="f103b-194">Give it a name by which Azure can refer to it, and also specify the address space prefix.</span></span> <span data-ttu-id="f103b-195">Azure 會使用您指定的 IP 位址前置詞來識別要傳送至內部部署位置的流量。</span><span class="sxs-lookup"><span data-stu-id="f103b-195">Azure uses the IP address prefix you specify to identify which traffic to send to your on-premises location.</span></span> <span data-ttu-id="f103b-196">如果您稍後需要先在此調整資訊，再建立您的閘道，您可以修改下列值並再次執行範例。</span><span class="sxs-lookup"><span data-stu-id="f103b-196">If you need to adjust the information here later, before creating your gateway, you can modify the values and run the sample again.</span></span>
   
   <span data-ttu-id="f103b-197">**-Name** 是您要指派給區域網路閘道的參考名稱。</span><span class="sxs-lookup"><span data-stu-id="f103b-197">**-Name** is the name you want to assign to refer to the local network gateway.</span></span><br><span data-ttu-id="f103b-198">
   **-AddressPrefix** 是傳統 VNet 的位址空間。</span><span class="sxs-lookup"><span data-stu-id="f103b-198">
   **-AddressPrefix** is the Address Space for your classic VNet.</span></span><br><span data-ttu-id="f103b-199">
**-GatewayIpAddress** 是傳統 VNet 閘道的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f103b-199">
**-GatewayIpAddress** is the public IP address of the classic VNet's gateway.</span></span> <span data-ttu-id="f103b-200">請務必變更下列範例，以反映正確的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f103b-200">Be sure to change the following sample to reflect the correct IP address.</span></span><br>

  ```powershell
  New-AzureRmLocalNetworkGateway -Name ClassicVNetLocal `
  -Location "West US" -AddressPrefix "10.0.0.0/24" `
  -GatewayIpAddress "n.n.n.n" -ResourceGroupName RG1
  ```
3. <span data-ttu-id="f103b-201">要求將公用 IP 位址配置到 Resource Manager VNet 的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="f103b-201">Request a public IP address to be allocated to the virtual network gateway for the Resource Manager VNet.</span></span> <span data-ttu-id="f103b-202">您無法指定想要使用的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f103b-202">You can't specify the IP address that you want to use.</span></span> <span data-ttu-id="f103b-203">IP 位址是動態地配置到虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="f103b-203">The IP address is dynamically allocated to the virtual network gateway.</span></span> <span data-ttu-id="f103b-204">但是，這不代表 IP 位址會變更。</span><span class="sxs-lookup"><span data-stu-id="f103b-204">However, this does not mean the IP address changes.</span></span> <span data-ttu-id="f103b-205">只有在刪除及重新建立閘道時，虛擬網路閘道 IP 位址才會變更。</span><span class="sxs-lookup"><span data-stu-id="f103b-205">The only time the virtual network gateway IP address changes is when the gateway is deleted and recreated.</span></span> <span data-ttu-id="f103b-206">它不會因為重新調整、重設或閘道的其他內部維護/升級而變更。</span><span class="sxs-lookup"><span data-stu-id="f103b-206">It doesn't change across resizing, resetting, or other internal maintenance/upgrades of the gateway.</span></span>

  <span data-ttu-id="f103b-207">在此步驟中，我們也會設定用於後續步驟中的變數。</span><span class="sxs-lookup"><span data-stu-id="f103b-207">In this step, we also set a variable that is used in a later step.</span></span>

  ```powershell
  $ipaddress = New-AzureRmPublicIpAddress -Name gwpip `
  -ResourceGroupName RG1 -Location 'EastUS' `
  -AllocationMethod Dynamic
  ```

4. <span data-ttu-id="f103b-208">確認您的虛擬網路有閘道子網路。</span><span class="sxs-lookup"><span data-stu-id="f103b-208">Verify that your virtual network has a gateway subnet.</span></span> <span data-ttu-id="f103b-209">如果閘道器子網路不存在，請新增一個。</span><span class="sxs-lookup"><span data-stu-id="f103b-209">If no gateway subnet exists, add one.</span></span> <span data-ttu-id="f103b-210">確定閘道子網路命名為 GatewaySubnet 。</span><span class="sxs-lookup"><span data-stu-id="f103b-210">Make sure the gateway subnet is named *GatewaySubnet*.</span></span>
5. <span data-ttu-id="f103b-211">擷取用於閘道的子網路。</span><span class="sxs-lookup"><span data-stu-id="f103b-211">Retrieve the subnet used for the gateway by running the following command.</span></span> <span data-ttu-id="f103b-212">在此步驟中，我們也會設定要用於下一個步驟中的變數。</span><span class="sxs-lookup"><span data-stu-id="f103b-212">In this step, we also set a variable to be used in the next step.</span></span>
   
   <span data-ttu-id="f103b-213">**-Name** 是 Resource Manager VNet 的名稱。</span><span class="sxs-lookup"><span data-stu-id="f103b-213">**-Name** is the name of your Resource Manager VNet.</span></span><br><span data-ttu-id="f103b-214">
   **-ResourceGroupName** 與 VNet 相關聯的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f103b-214">
**-ResourceGroupName** is the resource group that the VNet is associated with.</span></span> <span data-ttu-id="f103b-215">此閘道子網路必須已為此 VNet 存在且命名為 GatewaySubnet  ，才能正常運作。</span><span class="sxs-lookup"><span data-stu-id="f103b-215">The gateway subnet must already exist for this VNet and must be named *GatewaySubnet* to work properly.</span></span><br>

  ```powershell
  $subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name GatewaySubnet `
  -VirtualNetwork (Get-AzureRmVirtualNetwork -Name RMVNet -ResourceGroupName RG1)
  ``` 

6. <span data-ttu-id="f103b-216">建立閘道器 IP 位址組態。</span><span class="sxs-lookup"><span data-stu-id="f103b-216">Create the gateway IP addressing configuration.</span></span> <span data-ttu-id="f103b-217">閘道器組態定義要使用的子網路和公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f103b-217">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="f103b-218">使用下列範例來建立閘道組態。</span><span class="sxs-lookup"><span data-stu-id="f103b-218">Use the following sample to create your gateway configuration.</span></span>

  <span data-ttu-id="f103b-219">在本步驟中，**-SubnetId** 和 **-PublicIpAddressId** 參數必須各自從子網路和 IP 位址物件傳遞識別碼屬性。</span><span class="sxs-lookup"><span data-stu-id="f103b-219">In this step, the **-SubnetId** and **-PublicIpAddressId** parameters must be passed the id property from the subnet, and IP address objects, respectively.</span></span> <span data-ttu-id="f103b-220">您無法使用簡單的字串。</span><span class="sxs-lookup"><span data-stu-id="f103b-220">You can't use a simple string.</span></span> <span data-ttu-id="f103b-221">這些變數設定於要求公用 IP 的步驟以及擷取子網路的步驟中。</span><span class="sxs-lookup"><span data-stu-id="f103b-221">These variables are set in the step to request a public IP and the step to retrieve the subnet.</span></span>

  ```powershell
  $gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig `
  -Name gwipconfig -SubnetId $subnet.id `
  -PublicIpAddressId $ipaddress.id
  ```
7. <span data-ttu-id="f103b-222">透過執行下列命令建立 Resource Manager 虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="f103b-222">Create the Resource Manager virtual network gateway by running the following command.</span></span> <span data-ttu-id="f103b-223">`-VpnType` 必須為 *RouteBased*。</span><span class="sxs-lookup"><span data-stu-id="f103b-223">The `-VpnType` must be *RouteBased*.</span></span> <span data-ttu-id="f103b-224">閘道建立作業可能需要花費 45 分鐘以上的時間。</span><span class="sxs-lookup"><span data-stu-id="f103b-224">It can take 45 minutes or more for the gateway to create.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1 `
  -Location "EastUS" -GatewaySKU Standard -GatewayType Vpn `
  -IpConfigurations $gwipconfig `
  -EnableBgp $false -VpnType RouteBased
  ```
8. <span data-ttu-id="f103b-225">一旦 VPN 閘道建立好後，複製公用 IP 位址 。</span><span class="sxs-lookup"><span data-stu-id="f103b-225">Copy the public IP address once the VPN gateway has been created.</span></span> <span data-ttu-id="f103b-226">您會在進行傳統 VNet 的區域網路設定時用到它。</span><span class="sxs-lookup"><span data-stu-id="f103b-226">You use it when you configure the local network settings for your Classic VNet.</span></span> <span data-ttu-id="f103b-227">您可以使用下列 Cmdlet 來擷取公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f103b-227">You can use the following cmdlet to retrieve the public IP address.</span></span> <span data-ttu-id="f103b-228">公用 IP 位址會在傳回資料中列為 IpAddress 。</span><span class="sxs-lookup"><span data-stu-id="f103b-228">The public IP address is listed in the return as *IpAddress*.</span></span>

  ```powershell
  Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName RG1
  ```

## <a name="section-3-modify-the-classic-vnet-local-site-settings"></a><span data-ttu-id="f103b-229">第 3 節：修改傳統 VNet 本機站台設定</span><span class="sxs-lookup"><span data-stu-id="f103b-229">Section 3: Modify the classic VNet local site settings</span></span>

<span data-ttu-id="f103b-230">在本節中，您會處理傳統 VNet。</span><span class="sxs-lookup"><span data-stu-id="f103b-230">In this section, you work with the classic VNet.</span></span> <span data-ttu-id="f103b-231">您會取代您在指定本機站台設定 (將用於連線至 Resource Manager VNet 閘道) 時所使用的預留位置 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f103b-231">You replace the placeholder IP address that you used when specifying the local site settings that will be used to connect to the Resource Manager VNet gateway.</span></span> 

1. <span data-ttu-id="f103b-232">匯出網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="f103b-232">Export the network configuration file.</span></span>

  ```powershell
  Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
  ```
2. <span data-ttu-id="f103b-233">使用文字編輯器修改 VPNGatewayAddress 的值。</span><span class="sxs-lookup"><span data-stu-id="f103b-233">Using a text editor, modify the value for VPNGatewayAddress.</span></span> <span data-ttu-id="f103b-234">使用 Resource Manager 閘道的公用 IP 位址取代預留位置 IP 位址，然後儲存變更。</span><span class="sxs-lookup"><span data-stu-id="f103b-234">Replace the placeholder IP address with the public IP address of the Resource Manager gateway and then save the changes.</span></span>

  ```
  <VPNGatewayAddress>13.68.210.16</VPNGatewayAddress>
  ```
3. <span data-ttu-id="f103b-235">將修改過的網路組態檔匯入至 Azure。</span><span class="sxs-lookup"><span data-stu-id="f103b-235">Import the modified network configuration file to Azure.</span></span>

  ```powershell
  Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
  ```

## <span data-ttu-id="f103b-236"><a name="connect"></a>區段 4：在閘道之間建立連線</span><span class="sxs-lookup"><span data-stu-id="f103b-236"><a name="connect"></a>Section 4: Create a connection between the gateways</span></span>
<span data-ttu-id="f103b-237">在閘道之間建立連線需要 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="f103b-237">Creating a connection between the gateways requires PowerShell.</span></span> <span data-ttu-id="f103b-238">您可能需要新增 Azure 帳戶，才能使用傳統版本的 PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f103b-238">You may need to add your Azure Account to use the classic version of the  PowerShell cmdlets.</span></span> <span data-ttu-id="f103b-239">若要這樣做，請使用 **Add-azureaccount**。</span><span class="sxs-lookup"><span data-stu-id="f103b-239">To do so, use **Add-AzureAccount**.</span></span>

1. <span data-ttu-id="f103b-240">在 PowerShell 主控台中，設定您的共用金鑰。</span><span class="sxs-lookup"><span data-stu-id="f103b-240">In the PowerShell console, set your shared key.</span></span> <span data-ttu-id="f103b-241">執行 Cmdlet 之前，請參閱您針對 Azure 預期看到的確切名稱所下載的網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="f103b-241">Before running the cmdlets, refer to the network configuration file that you downloaded for the exact names that Azure expects to see.</span></span> <span data-ttu-id="f103b-242">當指定包含空格的 VNet 名稱時，請使用單引號括住值。</span><span class="sxs-lookup"><span data-stu-id="f103b-242">When specifying the name of a VNet that contains spaces, use single quotation marks around the value.</span></span><br><br><span data-ttu-id="f103b-243">在下列範例中，**-VNetName** 是傳統 VNet 的名稱，**-LocalNetworkSiteName** 是您為區域網路網站指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="f103b-243">In following example, **-VNetName** is the name of the classic VNet and **-LocalNetworkSiteName** is the name you specified for the local network site.</span></span> <span data-ttu-id="f103b-244">**-SharedKey** 是您產生和指定的值。</span><span class="sxs-lookup"><span data-stu-id="f103b-244">The **-SharedKey** is a value that you generate and specify.</span></span> <span data-ttu-id="f103b-245">在範例中，我們使用的是 'abc123'，但是您可以產生並使用更為複雜的值。</span><span class="sxs-lookup"><span data-stu-id="f103b-245">In the example, we used 'abc123', but you can generate and use something more complex.</span></span> <span data-ttu-id="f103b-246">重要的是，您在此指定的值必須與您在下一個步驟中建立連線時指定的值相同。</span><span class="sxs-lookup"><span data-stu-id="f103b-246">The important thing is that the value you specify here must be the same value that you specify in the next step when you create your connection.</span></span> <span data-ttu-id="f103b-247">傳回應顯示 [狀態: 成功]。</span><span class="sxs-lookup"><span data-stu-id="f103b-247">The return should show **Status: Successful**.</span></span>

  ```powershell
  Set-AzureVNetGatewayKey -VNetName ClassicVNet `
  -LocalNetworkSiteName RMVNetLocal -SharedKey abc123
  ```
2. <span data-ttu-id="f103b-248">執行下列命令來建立 VPN 連線：</span><span class="sxs-lookup"><span data-stu-id="f103b-248">Create the VPN connection by running the following commands:</span></span>
   
  <span data-ttu-id="f103b-249">設定變數。</span><span class="sxs-lookup"><span data-stu-id="f103b-249">Set the variables.</span></span>

  ```powershell
  $vnet01gateway = Get-AzureRMLocalNetworkGateway -Name ClassicVNetLocal -ResourceGroupName RG1
  $vnet02gateway = Get-AzureRmVirtualNetworkGateway -Name RMGateway -ResourceGroupName RG1
  ```
   
  <span data-ttu-id="f103b-250">建立連線。</span><span class="sxs-lookup"><span data-stu-id="f103b-250">Create the connection.</span></span> <span data-ttu-id="f103b-251">請注意，**-ConnectionType** 是 IPsec，而不是 Vnet2Vnet。</span><span class="sxs-lookup"><span data-stu-id="f103b-251">Notice that the **-ConnectionType** is IPsec, not Vnet2Vnet.</span></span>

  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name RM-Classic -ResourceGroupName RG1 `
  -Location "East US" -VirtualNetworkGateway1 `
  $vnet02gateway -LocalNetworkGateway2 `
  $vnet01gateway -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

## <a name="section-5-verify-your-connections"></a><span data-ttu-id="f103b-252">第 5 節︰驗證您的連線</span><span class="sxs-lookup"><span data-stu-id="f103b-252">Section 5: Verify your connections</span></span>

### <a name="to-verify-the-connection-from-your-classic-vnet-to-your-resource-manager-vnet"></a><span data-ttu-id="f103b-253">驗證從傳統 VNet 到 Resource Manager VNet 的連線</span><span class="sxs-lookup"><span data-stu-id="f103b-253">To verify the connection from your classic VNet to your Resource Manager VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="f103b-254">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f103b-254">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-connection-ps-classic](../../includes/vpn-gateway-verify-connection-ps-classic-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="f103b-255">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f103b-255">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-azureportal-classic](../../includes/vpn-gateway-verify-connection-azureportal-classic-include.md)]


### <a name="to-verify-the-connection-from-your-resource-manager-vnet-to-your-classic-vnet"></a><span data-ttu-id="f103b-256">驗證從 Resource Manager VNet 到傳統 VNet 的連線</span><span class="sxs-lookup"><span data-stu-id="f103b-256">To verify the connection from your Resource Manager VNet to your classic VNet</span></span>

#### <a name="powershell"></a><span data-ttu-id="f103b-257">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f103b-257">PowerShell</span></span>

[!INCLUDE [vpn-gateway-verify-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

#### <a name="azure-portal"></a><span data-ttu-id="f103b-258">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="f103b-258">Azure portal</span></span>

[!INCLUDE [vpn-gateway-verify-connection-portal-rm](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <span data-ttu-id="f103b-259"><a name="faq"></a>VNet 對 VNet 常見問題集</span><span class="sxs-lookup"><span data-stu-id="f103b-259"><a name="faq"></a>VNet-to-VNet FAQ</span></span>

[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

