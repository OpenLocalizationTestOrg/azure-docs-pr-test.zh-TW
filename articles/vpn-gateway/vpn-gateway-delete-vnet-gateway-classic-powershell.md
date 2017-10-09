---
title: "刪除虛擬網路閘道：PowerShell：Azure 傳統 | Microsoft Docs"
description: "在傳統部署模型中使用 PowerShell 刪除虛擬網路閘道。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: cherylmc
ms.openlocfilehash: b1bc18307227a728e2bc8fd95e30fdc1cbdb8c59
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="delete-a-virtual-network-gateway-using-powershell-classic"></a><span data-ttu-id="861c4-103">使用 PowerShell (傳統) 刪除虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="861c4-103">Delete a virtual network gateway using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="861c4-104">Resource Manager - Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="861c4-104">Resource Manager - Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="861c4-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="861c4-105">Resource Manager - PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="861c4-106">傳統 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="861c4-106">Classic - PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

<span data-ttu-id="861c4-107">本文章會協助您使用 PowerShell 刪除傳統部署模型中的 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="861c4-107">This article helps you delete a VPN gateway in the classic deployment model by using PowerShell.</span></span> <span data-ttu-id="861c4-108">在刪除虛擬網路閘道之後，請修改網路設定檔，以移除您不再使用的項目。</span><span class="sxs-lookup"><span data-stu-id="861c4-108">After the virtual network gateway has been deleted, modify the network configuration file to remove elements that you are no longer using.</span></span>

##<span data-ttu-id="861c4-109"><a name="connect"></a>步驟 1：連線到 Azure</span><span class="sxs-lookup"><span data-stu-id="861c4-109"><a name="connect"></a>Step 1: Connect to Azure</span></span>

### <a name="1-install-the-latest-powershell-cmdlets"></a><span data-ttu-id="861c4-110">1.安裝最新的 PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="861c4-110">1. Install the latest PowerShell cmdlets.</span></span>

<span data-ttu-id="861c4-111">下載並安裝最新版的 Azure 服務管理 (SM) PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="861c4-111">Download and install the latest version of the Azure Service Management (SM) PowerShell cmdlets.</span></span> <span data-ttu-id="861c4-112">如需詳細資訊，請參閱 [如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="861c4-112">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="2-connect-to-your-azure-account"></a><span data-ttu-id="861c4-113">2.連線至您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="861c4-113">2. Connect to your Azure account.</span></span> 

<span data-ttu-id="861c4-114">以提高的權限開啟 PowerShell 主控台並連接到您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="861c4-114">Open your PowerShell console with elevated rights and connect to your account.</span></span> <span data-ttu-id="861c4-115">使用下列範例來協助您連接：</span><span class="sxs-lookup"><span data-stu-id="861c4-115">Use the following example to help you connect:</span></span>

```powershell
Add-AzureAccount
```

## <span data-ttu-id="861c4-116"><a name="export"></a>步驟 2：匯出並檢視網路組態檔</span><span class="sxs-lookup"><span data-stu-id="861c4-116"><a name="export"></a>Step 2: Export and view the network configuration file</span></span>

<span data-ttu-id="861c4-117">在您的電腦上建立目錄，然後將網路組態檔匯出到該目錄。</span><span class="sxs-lookup"><span data-stu-id="861c4-117">Create a directory on your computer and then export the network configuration file to the directory.</span></span> <span data-ttu-id="861c4-118">您可以使用此檔案來檢視目前的組態資訊，也可以修改網路組態。</span><span class="sxs-lookup"><span data-stu-id="861c4-118">You use this file to both view the current configuration information, and also to modify the network configuration.</span></span>

<span data-ttu-id="861c4-119">在此範例中，會將網路組態檔匯出到 C:\AzureNet。</span><span class="sxs-lookup"><span data-stu-id="861c4-119">In this example, the network configuration file is exported to C:\AzureNet.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="861c4-120">使用文字編輯器開啟檔案，並檢視傳統 VNet 的名稱。</span><span class="sxs-lookup"><span data-stu-id="861c4-120">Open the file with a text editor and view the name for your classic VNet.</span></span> <span data-ttu-id="861c4-121">當您在 Azure 入口網站中建立 VNet 時，不會在入口網站中顯示 Azure 所使用的完整名稱。</span><span class="sxs-lookup"><span data-stu-id="861c4-121">When you create a VNet in the Azure portal, the full name that Azure uses is not visible in the portal.</span></span> <span data-ttu-id="861c4-122">例如，在 Azure 入口網站中名稱顯示為 'ClassicVNet1' 的 VNet，在網路組態檔中的名稱可能更長。</span><span class="sxs-lookup"><span data-stu-id="861c4-122">For example, a VNet that appears to be named 'ClassicVNet1' in the Azure portal, may have a much longer name in the network configuration file.</span></span> <span data-ttu-id="861c4-123">名稱可能如下︰'Group ClassicRG1 ClassicVNet1'。</span><span class="sxs-lookup"><span data-stu-id="861c4-123">The name might look something like: 'Group ClassicRG1 ClassicVNet1'.</span></span> <span data-ttu-id="861c4-124">虛擬網路名稱會列為 'VirtualNetworkSite name ='。</span><span class="sxs-lookup"><span data-stu-id="861c4-124">Virtual network names are listed as **'VirtualNetworkSite name ='**.</span></span> <span data-ttu-id="861c4-125">執行 PowerShell Cmdlet 時，請使用網路組態檔中的名稱。</span><span class="sxs-lookup"><span data-stu-id="861c4-125">Use the names in the network configuration file when running your PowerShell cmdlets.</span></span>

## <span data-ttu-id="861c4-126"><a name="delete"></a>步驟 3：刪除虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="861c4-126"><a name="delete"></a>Step 3: Delete the virtual network gateway</span></span>

<span data-ttu-id="861c4-127">當您刪除虛擬網路閘道時，不會中斷連接所有透過閘道的 VNet 連接。</span><span class="sxs-lookup"><span data-stu-id="861c4-127">When you delete a virtual network gateway, all connections to the VNet through the gateway are disconnected.</span></span> <span data-ttu-id="861c4-128">如果您的 P2S 用戶端連接到 VNet，則會將它們中斷連接而不發出警告。</span><span class="sxs-lookup"><span data-stu-id="861c4-128">If you have P2S clients connected to the VNet, they will be disconnected without warning.</span></span>

<span data-ttu-id="861c4-129">這個範例會刪除虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="861c4-129">This example deletes the virtual network gateway.</span></span> <span data-ttu-id="861c4-130">請務必使用網路組態檔中的虛擬網路完整名稱。</span><span class="sxs-lookup"><span data-stu-id="861c4-130">Make sure to use the full name of the virtual network from the network configuration file.</span></span>

```powershell
Remove-AzureVNetGateway -VNetName "Group ClassicRG1 ClassicVNet1"
```

<span data-ttu-id="861c4-131">如果成功，傳回便會顯示：</span><span class="sxs-lookup"><span data-stu-id="861c4-131">If successful, the return shows:</span></span>

```
Status : Successful
```

## <span data-ttu-id="861c4-132"><a name="modify"></a>步驟 4：修改網路組態檔</span><span class="sxs-lookup"><span data-stu-id="861c4-132"><a name="modify"></a>Step 4: Modify the network configuration file</span></span>

<span data-ttu-id="861c4-133">當您刪除虛擬網路閘道時，Cmdlet 不會修改網路設定檔。</span><span class="sxs-lookup"><span data-stu-id="861c4-133">When you delete a virtual network gateway, the cmdlet does not modify the network configuration file.</span></span> <span data-ttu-id="861c4-134">您需要修改檔案，以移除不再使用的項目。</span><span class="sxs-lookup"><span data-stu-id="861c4-134">You need to modify the file to remove the elements that are no longer being used.</span></span> <span data-ttu-id="861c4-135">下列各節可協助修改您所下載的網路組態檔。</span><span class="sxs-lookup"><span data-stu-id="861c4-135">The following sections help you modify the network configuration file that you downloaded.</span></span>

### <span data-ttu-id="861c4-136"><a name="lnsref"></a>區域網路網站參考</span><span class="sxs-lookup"><span data-stu-id="861c4-136"><a name="lnsref"></a>Local Network Site References</span></span>

<span data-ttu-id="861c4-137">若要移除網站參考資訊，請對 **ConnectionsToLocalNetwork/LocalNetworkSiteRef** 進行組態變更。</span><span class="sxs-lookup"><span data-stu-id="861c4-137">To remove site reference information, make configuration changes to **ConnectionsToLocalNetwork/LocalNetworkSiteRef**.</span></span> <span data-ttu-id="861c4-138">移除區域網站參考會觸發 Azure 刪除通道。</span><span class="sxs-lookup"><span data-stu-id="861c4-138">Removing a local site reference triggers Azure to delete a tunnel.</span></span> <span data-ttu-id="861c4-139">根據您所建立的組態而定，您可能並未列出 **LocalNetworkSiteRef**。</span><span class="sxs-lookup"><span data-stu-id="861c4-139">Depending on the configuration that you created, you may not have a **LocalNetworkSiteRef** listed.</span></span>

```
<Gateway>
   <ConnectionsToLocalNetwork>
     <LocalNetworkSiteRef name="D1BFC9CB_Site2">
       <Connection type="IPsec" />
     </LocalNetworkSiteRef>
   </ConnectionsToLocalNetwork>
 </Gateway>
```

<span data-ttu-id="861c4-140">範例：</span><span class="sxs-lookup"><span data-stu-id="861c4-140">Example:</span></span>

```
<Gateway>
   <ConnectionsToLocalNetwork>
   </ConnectionsToLocalNetwork>
 </Gateway>
```

###<span data-ttu-id="861c4-141"><a name="lns"></a>區域網路網站</span><span class="sxs-lookup"><span data-stu-id="861c4-141"><a name="lns"></a>Local Network Sites</span></span>

<span data-ttu-id="861c4-142">移除所有您不再使用的區域網站。</span><span class="sxs-lookup"><span data-stu-id="861c4-142">Remove any local sites that you are no longer using.</span></span> <span data-ttu-id="861c4-143">根據您所建立的組態而定，您可能並未列出 **LocalNetworkSite**。</span><span class="sxs-lookup"><span data-stu-id="861c4-143">Depending on the configuration you created, it is possible that you don't have a **LocalNetworkSite** listed.</span></span>

```
<LocalNetworkSites>
  <LocalNetworkSite name="Site1">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
  </LocalNetworkSite>
  <LocalNetworkSite name="Site3">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>57.179.18.164</VPNGatewayAddress>
  </LocalNetworkSite>
 </LocalNetworkSites>
```

<span data-ttu-id="861c4-144">在此範例中，我們只會移除 Site3。</span><span class="sxs-lookup"><span data-stu-id="861c4-144">In this example, we removed only Site3.</span></span>

```
<LocalNetworkSites>
  <LocalNetworkSite name="Site1">
    <AddressSpace>
      <AddressPrefix>192.168.0.0/16</AddressPrefix>
    </AddressSpace>
    <VPNGatewayAddress>5.4.3.2</VPNGatewayAddress>
  </LocalNetworkSite>
 </LocalNetworkSites>
```

### <span data-ttu-id="861c4-145"><a name="clientaddresss"></a>用戶端 AddressPool</span><span class="sxs-lookup"><span data-stu-id="861c4-145"><a name="clientaddresss"></a>Client AddressPool</span></span>

<span data-ttu-id="861c4-146">如果您擁有連至 VNet 的 P2S 連線，您便會具備 **VPNClientAddressPool**。</span><span class="sxs-lookup"><span data-stu-id="861c4-146">If you had a P2S connection to your VNet, you will have a **VPNClientAddressPool**.</span></span> <span data-ttu-id="861c4-147">移除對應至您已刪除之虛擬網路閘道的用戶端位址集區。</span><span class="sxs-lookup"><span data-stu-id="861c4-147">Remove the client address pools that correspond to the virtual network gateway that you deleted.</span></span>

```
<Gateway>
    <VPNClientAddressPool>
      <AddressPrefix>10.1.0.0/24</AddressPrefix>
    </VPNClientAddressPool>
  <ConnectionsToLocalNetwork />
 </Gateway>
```

<span data-ttu-id="861c4-148">範例：</span><span class="sxs-lookup"><span data-stu-id="861c4-148">Example:</span></span>

```
<Gateway>
  <ConnectionsToLocalNetwork />
 </Gateway>
```

### <span data-ttu-id="861c4-149"><a name="gwsub"></a>GatewaySubnet</span><span class="sxs-lookup"><span data-stu-id="861c4-149"><a name="gwsub"></a>GatewaySubnet</span></span>

<span data-ttu-id="861c4-150">刪除對應至 VNet 的 **GatewaySubnet**。</span><span class="sxs-lookup"><span data-stu-id="861c4-150">Delete the **GatewaySubnet** that corresponds to the VNet.</span></span>

```
<Subnets>
   <Subnet name="FrontEnd">
     <AddressPrefix>10.11.0.0/24</AddressPrefix>
   </Subnet>
   <Subnet name="GatewaySubnet">
     <AddressPrefix>10.11.1.0/29</AddressPrefix>
   </Subnet>
 </Subnets>
```

<span data-ttu-id="861c4-151">範例：</span><span class="sxs-lookup"><span data-stu-id="861c4-151">Example:</span></span>

```
<Subnets>
   <Subnet name="FrontEnd">
     <AddressPrefix>10.11.0.0/24</AddressPrefix>
   </Subnet>
 </Subnets>
```

## <span data-ttu-id="861c4-152"><a name="upload"></a>步驟 5：上傳網路組態檔</span><span class="sxs-lookup"><span data-stu-id="861c4-152"><a name="upload"></a>Step 5: Upload the network configuration file</span></span>

<span data-ttu-id="861c4-153">儲存您的變更並將網路組態檔上傳至 Azure。</span><span class="sxs-lookup"><span data-stu-id="861c4-153">Save your changes and upload the network configuration file to Azure.</span></span> <span data-ttu-id="861c4-154">確定您會視需要變更環境的檔案路徑。</span><span class="sxs-lookup"><span data-stu-id="861c4-154">Make sure you change the file path as necessary for your environment.</span></span>

```powershell
Set-AzureVNetConfig -ConfigurationPath C:\AzureNet\NetworkConfig.xml
```

<span data-ttu-id="861c4-155">如果成功，傳回就會顯示類似此範例的內容：</span><span class="sxs-lookup"><span data-stu-id="861c4-155">If successful, the return shows something similar to this example:</span></span>

```
OperationDescription        OperationId                      OperationStatus                                                
--------------------        -----------                      ---------------                                           
Set-AzureVNetConfig         e0ee6e66-9167-cfa7-a746-7casb9   Succeeded