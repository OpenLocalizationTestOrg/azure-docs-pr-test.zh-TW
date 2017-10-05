---
title: "刪除虛擬網路閘道：PowerShell：Azure Resource Manager | Microsoft Docs"
description: "在 Resource Manager 部署模型中使用 PowerShell 刪除虛擬網路閘道。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: 
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: cherylmc
ms.openlocfilehash: 4d0f085423d5bd60b24d88649ee1d77bcd1d009f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="delete-a-virtual-network-gateway-using-powershell"></a><span data-ttu-id="4a5ab-103">使用 PowerShell 刪除虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="4a5ab-103">Delete a virtual network gateway using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4a5ab-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="4a5ab-104">Azure portal</span></span>](vpn-gateway-delete-vnet-gateway-portal.md)
> * [<span data-ttu-id="4a5ab-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4a5ab-105">PowerShell</span></span>](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [<span data-ttu-id="4a5ab-106">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="4a5ab-106">PowerShell (classic)</span></span>](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

<span data-ttu-id="4a5ab-107">如果您想要刪除 VPN 閘道組態的虛擬網路閘道，您可以採取幾種不同的方法。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span></span>

- <span data-ttu-id="4a5ab-108">如果您想要刪除所有內容並重頭開始 (例如使用測試環境的情況)，您可以刪除資源群組。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span></span> <span data-ttu-id="4a5ab-109">刪除資源群組時，會一併刪除群組內的所有資源。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-109">When you delete a resource group, it deletes all the resources within the group.</span></span> <span data-ttu-id="4a5ab-110">只有在您不想保留資源群組中的任何資源時，才建議使用此方法。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span></span> <span data-ttu-id="4a5ab-111">您無法使用這種方法，選擇性地只刪除一些資源。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-111">You can't selectively delete only a few resources using this approach.</span></span>

- <span data-ttu-id="4a5ab-112">如果您想要保留資源群組中的部分資源，刪除虛擬網路閘道會變得稍微複雜一點。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span></span> <span data-ttu-id="4a5ab-113">您必須先刪除任何相依於閘道的資源，才可以刪除虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span></span> <span data-ttu-id="4a5ab-114">您遵循的步驟取決於您所建立的連線類型以及每個連線的相依資源。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span></span>

## <a name="before-beginning"></a><span data-ttu-id="4a5ab-115">開始之前</span><span class="sxs-lookup"><span data-stu-id="4a5ab-115">Before beginning</span></span>

### <a name="1-download-the-latest-azure-resource-manager-powershell-cmdlets"></a><span data-ttu-id="4a5ab-116">1.下載最新版的 Azure Resource Manager PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-116">1. Download the latest Azure Resource Manager PowerShell cmdlets.</span></span>

<span data-ttu-id="4a5ab-117">下載並安裝最新版的 Azure Resource Manager PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-117">Download and install the latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="4a5ab-118">如需下載和安裝 PowerShell Cmdlet 的詳細資訊，請參閱[如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-118">For more information about downloading and installing PowerShell cmdlets, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="2-connect-to-your-azure-account"></a><span data-ttu-id="4a5ab-119">2.連線至您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-119">2. Connect to your Azure account.</span></span>

<span data-ttu-id="4a5ab-120">開啟 PowerShell 主控台並連接到您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-120">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="4a5ab-121">使用下列範例來協助您連接：</span><span class="sxs-lookup"><span data-stu-id="4a5ab-121">Use the following example to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="4a5ab-122">檢查帳戶的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-122">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="4a5ab-123">如果您有多個訂用帳戶，請指定您要使用的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-123">If you have more than one subscription, specify the subscription that you want to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <span data-ttu-id="4a5ab-124"><a name="S2S"></a>刪除站對站 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="4a5ab-124"><a name="S2S"></a>Delete a Site-to-Site VPN gateway</span></span>

<span data-ttu-id="4a5ab-125">若要刪除 S2S 組態的虛擬網路閘道，您必須先刪除虛擬網路閘道的每個相關資源。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-125">To delete a virtual network gateway for a S2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="4a5ab-126">由於相依性，您必須依照特定順序刪除資源。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-126">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="4a5ab-127">使用下面的範例時，某些值必須特別指定，而其他值則為輸出結果。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-127">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="4a5ab-128">我們在範例中使用下列特定值，做為示範之用︰</span><span class="sxs-lookup"><span data-stu-id="4a5ab-128">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="4a5ab-129">VNet 名稱︰VNet1</span><span class="sxs-lookup"><span data-stu-id="4a5ab-129">VNet name: VNet1</span></span><br>
<span data-ttu-id="4a5ab-130">資源群組名稱：GW1</span><span class="sxs-lookup"><span data-stu-id="4a5ab-130">Resource Group name: RG1</span></span><br>
<span data-ttu-id="4a5ab-131">虛擬網路閘道名稱：GW1</span><span class="sxs-lookup"><span data-stu-id="4a5ab-131">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="4a5ab-132">下列步驟適用於 Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-132">The following steps apply to the Resource Manager deployment model.</span></span>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="4a5ab-133">1.取得您想要刪除的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-133">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a><span data-ttu-id="4a5ab-134">2.查看虛擬網路閘道是否有任何連線。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-134">2. Check to see if the virtual network gateway has any connections.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
$Conns=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```

### <a name="3-delete-all-connections"></a><span data-ttu-id="4a5ab-135">3.刪除所有連線。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-135">3. Delete all connections.</span></span>

<span data-ttu-id="4a5ab-136">系統可能會提示您確認刪除每個連線。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-136">You may be prompted to confirm the deletion of each of the connections.</span></span>

```powershell
$Conns | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="4-delete-the-virtual-network-gateway"></a><span data-ttu-id="4a5ab-137">4.刪除虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-137">4. Delete the virtual network gateway.</span></span>

<span data-ttu-id="4a5ab-138">系統可能會提示您確認刪除閘道。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-138">You may be prompted to confirm the deletion of the gateway.</span></span> <span data-ttu-id="4a5ab-139">如果除了 S2S 組態，您還擁有此 VNet 適用的 P2S 組態，刪除虛擬網路閘道將自動中斷連接所有的 P2S 用戶端，而不會發出任何警告。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-139">If you have a P2S configuration to this VNet in addition to your S2S configuration, deleting the virtual network gateway will automatically disconnect all P2S clients without warning.</span></span>


```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="4a5ab-140">此時，虛擬網路閘道已經刪除。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-140">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="4a5ab-141">您可以使用後續步驟來刪除不再使用的任何資源。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-141">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="5-delete-the-local-network-gateways"></a><span data-ttu-id="4a5ab-142">5 刪除區域網路閘道。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-142">5 Delete the local network gateways.</span></span>

<span data-ttu-id="4a5ab-143">取得對應區域網路閘道的清單。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-143">Get the list of the corresponding local network gateways.</span></span>

```powershell
$LNG=Get-AzureRmLocalNetworkGateway -ResourceGroupName "RG1" | where-object {$_.Id -In $Conns.LocalNetworkGateway2.Id}
```

<span data-ttu-id="4a5ab-144">刪除區域網路閘道。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-144">Delete the local network gateways.</span></span> <span data-ttu-id="4a5ab-145">系統可能會提示您確認刪除每個區域網路閘道。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-145">You may be prompted to confirm the deletion of each of the local network gateway.</span></span>

```powershell
$LNG | ForEach-Object {Remove-AzureRmLocalNetworkGateway -Name $_.Name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="6-delete-the-public-ip-address-resources"></a><span data-ttu-id="4a5ab-146">6.刪除公用 IP 位址資源。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-146">6. Delete the Public IP address resources.</span></span>

<span data-ttu-id="4a5ab-147">取得虛擬網路閘道的 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-147">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="4a5ab-148">取得用於此虛擬網路閘道的公用 IP 位址資源清單。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-148">Get the list of Public IP address resources used for this virtual network gateway.</span></span> <span data-ttu-id="4a5ab-149">如果虛擬網路閘道為主動-主動，您會看到兩個公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-149">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="4a5ab-150">刪除公用 IP 資源。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-150">Delete the Public IP resources.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "RG1"}
```

### <a name="7-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="4a5ab-151">7.刪除閘道子網路並設定組態。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-151">7. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="4a5ab-152"><a name="v2v"></a>刪除 VNet 對 VNet VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="4a5ab-152"><a name="v2v"></a>Delete a VNet-to-VNet VPN gateway</span></span>

<span data-ttu-id="4a5ab-153">若要刪除 V2V 組態的虛擬網路閘道，您必須先刪除虛擬網路閘道的每個相關資源。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-153">To delete a virtual network gateway for a V2V configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="4a5ab-154">由於相依性，您必須依照特定順序刪除資源。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-154">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="4a5ab-155">使用下面的範例時，某些值必須特別指定，而其他值則為輸出結果。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-155">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="4a5ab-156">我們在範例中使用下列特定值，做為示範之用︰</span><span class="sxs-lookup"><span data-stu-id="4a5ab-156">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="4a5ab-157">VNet 名稱︰VNet1</span><span class="sxs-lookup"><span data-stu-id="4a5ab-157">VNet name: VNet1</span></span><br>
<span data-ttu-id="4a5ab-158">資源群組名稱：GW1</span><span class="sxs-lookup"><span data-stu-id="4a5ab-158">Resource Group name: RG1</span></span><br>
<span data-ttu-id="4a5ab-159">虛擬網路閘道名稱：GW1</span><span class="sxs-lookup"><span data-stu-id="4a5ab-159">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="4a5ab-160">下列步驟適用於 Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-160">The following steps apply to the Resource Manager deployment model.</span></span>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="4a5ab-161">1.取得您想要刪除的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-161">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-check-to-see-if-the-virtual-network-gateway-has-any-connections"></a><span data-ttu-id="4a5ab-162">2.查看虛擬網路閘道是否有任何連線。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-162">2. Check to see if the virtual network gateway has any connections.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
<span data-ttu-id="4a5ab-163">可能屬於不同的資源群組的其他連線至虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-163">There may be other connections to the virtual network gateway that are part of a different resource group.</span></span> <span data-ttu-id="4a5ab-164">檢查其他每個資源群組中的其他連線。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-164">Check for additional connections in each additional resource group.</span></span> <span data-ttu-id="4a5ab-165">在此範例中，我們會檢查來自 RG2 的連線。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-165">In this example, we are checking for connections from RG2.</span></span> <span data-ttu-id="4a5ab-166">針對可能連線至虛擬網路閘道的每個資源群組，執行此作業。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-166">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span></span>

```powershell
get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG2" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
```

### <a name="3-get-the-list-of-connections-in-both-directions"></a><span data-ttu-id="4a5ab-167">3.取得雙向連線清單。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-167">3. Get the list of connections in both directions.</span></span>

<span data-ttu-id="4a5ab-168">因為這是 VNet 對 VNet 組態，所以您需要雙向連線清單。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-168">Because this is a VNet-to-VNet configuration, you need the list of connections in both directions.</span></span>

```powershell
$ConnsL=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "RG1" | where-object {$_.VirtualNetworkGateway1.Id -eq $GW.Id}
```
 
<span data-ttu-id="4a5ab-169">在此範例中，我們會檢查來自 RG2 的連線。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-169">In this example, we are checking for connections from RG2.</span></span> <span data-ttu-id="4a5ab-170">針對可能連線至虛擬網路閘道的每個資源群組，執行此作業。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-170">Run this for each resource group that you have which may have a connection to the virtual network gateway.</span></span>

```powershell
 $ConnsR=get-azurermvirtualnetworkgatewayconnection -ResourceGroupName "<NameOfResourceGroup2>" | where-object {$_.VirtualNetworkGateway2.Id -eq $GW.Id}
 ```

### <a name="4-delete-all-connections"></a><span data-ttu-id="4a5ab-171">4.刪除所有連線。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-171">4. Delete all connections.</span></span>

<span data-ttu-id="4a5ab-172">系統可能會提示您確認刪除每個連線。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-172">You may be prompted to confirm the deletion of each of the connections.</span></span>

```powershell
$ConnsL | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
$ConnsR | ForEach-Object {Remove-AzureRmVirtualNetworkGatewayConnection -Name $_.name -ResourceGroupName $_.ResourceGroupName}
```

### <a name="5-delete-the-virtual-network-gateway"></a><span data-ttu-id="4a5ab-173">5.刪除虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-173">5. Delete the virtual network gateway.</span></span>

<span data-ttu-id="4a5ab-174">系統可能會提示您確認刪除虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-174">You may be prompted to confirm the deletion of the virtual network gateway.</span></span> <span data-ttu-id="4a5ab-175">如果除了 V2V 組態，您還擁有您 VNet 適用的 P2S 組態，刪除虛擬網路閘道將自動中斷連接所有的 P2S 用戶端，而不會發出任何警告。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-175">If you have P2S configurations to your VNets in addition to your V2V configuration, deleting the virtual network gateways will automatically disconnect all P2S clients without warning.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="4a5ab-176">此時，虛擬網路閘道已經刪除。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-176">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="4a5ab-177">您可以使用後續步驟來刪除不再使用的任何資源。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-177">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="6-delete-the-public-ip-address-resources"></a><span data-ttu-id="4a5ab-178">6.刪除公用 IP 位址資源</span><span class="sxs-lookup"><span data-stu-id="4a5ab-178">6. Delete the Public IP address resources</span></span>

<span data-ttu-id="4a5ab-179">取得虛擬網路閘道的 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-179">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="4a5ab-180">取得用於此虛擬網路閘道的公用 IP 位址資源清單。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-180">Get the list of Public IP address resources used for this virtual network gateway.</span></span> <span data-ttu-id="4a5ab-181">如果虛擬網路閘道為主動-主動，您會看到兩個公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-181">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="4a5ab-182">刪除公用 IP 資源。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-182">Delete the Public IP resources.</span></span> <span data-ttu-id="4a5ab-183">系統可能會提示您確認刪除公用 IP。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-183">You may be prompted to confirm the deletion of the Public IP.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="7-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="4a5ab-184">7.刪除閘道子網路並設定組態。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-184">7. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="4a5ab-185"><a name="deletep2s"></a>刪除點對站 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="4a5ab-185"><a name="deletep2s"></a>Delete a Point-to-Site VPN gateway</span></span>

<span data-ttu-id="4a5ab-186">若要刪除 P2S 組態的虛擬網路閘道，您必須先刪除每個與虛擬網路閘道相關的資源。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-186">To delete a virtual network gateway for a P2S configuration, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="4a5ab-187">由於相依性，您必須依照特定順序刪除資源。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-187">Resources must be deleted in a certain order due to dependencies.</span></span> <span data-ttu-id="4a5ab-188">使用下面的範例時，某些值必須特別指定，而其他值則為輸出結果。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-188">When working with the examples below, some of the values must be specified, while other values are an output result.</span></span> <span data-ttu-id="4a5ab-189">我們在範例中使用下列特定值，做為示範之用︰</span><span class="sxs-lookup"><span data-stu-id="4a5ab-189">We use the following specific values in the examples for demonstration purposes:</span></span>

<span data-ttu-id="4a5ab-190">VNet 名稱︰VNet1</span><span class="sxs-lookup"><span data-stu-id="4a5ab-190">VNet name: VNet1</span></span><br>
<span data-ttu-id="4a5ab-191">資源群組名稱：GW1</span><span class="sxs-lookup"><span data-stu-id="4a5ab-191">Resource Group name: RG1</span></span><br>
<span data-ttu-id="4a5ab-192">虛擬網路閘道名稱：GW1</span><span class="sxs-lookup"><span data-stu-id="4a5ab-192">Virtual network gateway name: GW1</span></span><br>

<span data-ttu-id="4a5ab-193">下列步驟適用於 Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-193">The following steps apply to the Resource Manager deployment model.</span></span>


>[!NOTE]
> <span data-ttu-id="4a5ab-194">當您刪除 VPN 閘道時，將中斷所有已連接用戶端與 VNet 的連接，而不會發出任何警告。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-194">When you delete the VPN gateway, all connected clients will be disconnected from the VNet without warning.</span></span>
>
>

### <a name="1-get-the-virtual-network-gateway-that-you-want-to-delete"></a><span data-ttu-id="4a5ab-195">1.取得您想要刪除的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-195">1. Get the virtual network gateway that you want to delete.</span></span>

```powershell
$Gateway=get-azurermvirtualnetworkgateway -Name "GW1" -ResourceGroupName "RG1"
```

### <a name="2-delete-the-virtual-network-gateway"></a><span data-ttu-id="4a5ab-196">2.刪除虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-196">2. Delete the virtual network gateway.</span></span>

<span data-ttu-id="4a5ab-197">系統可能會提示您確認刪除虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-197">You may be prompted to confirm the deletion of the virtual network gateway.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGateway -Name "GW1" -ResourceGroupName "RG1"
```

<span data-ttu-id="4a5ab-198">此時，虛擬網路閘道已經刪除。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-198">At this point, your virtual network gateway has been deleted.</span></span> <span data-ttu-id="4a5ab-199">您可以使用後續步驟來刪除不再使用的任何資源。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-199">You can use the next steps to delete any resources that are no longer being used.</span></span>

### <a name="3-delete-the-public-ip-address-resources"></a><span data-ttu-id="4a5ab-200">3.刪除公用 IP 位址資源</span><span class="sxs-lookup"><span data-stu-id="4a5ab-200">3. Delete the Public IP address resources</span></span>

<span data-ttu-id="4a5ab-201">取得虛擬網路閘道的 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-201">Get the IP configurations of the virtual network gateway.</span></span>

```powershell
$GWIpConfigs = $Gateway.IpConfigurations
```

<span data-ttu-id="4a5ab-202">取得用於此虛擬網路閘道的公用 IP 位址清單。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-202">Get the list of Public IP addresses used for this virtual network gateway.</span></span> <span data-ttu-id="4a5ab-203">如果虛擬網路閘道為主動-主動，您會看到兩個公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-203">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span>

```powershell
$PubIP=Get-AzureRmPublicIpAddress | where-object {$_.Id -In $GWIpConfigs.PublicIpAddress.Id}
```

<span data-ttu-id="4a5ab-204">刪除公用 IP。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-204">Delete the Public IPs.</span></span> <span data-ttu-id="4a5ab-205">系統可能會提示您確認刪除公用 IP。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-205">You may be prompted to confirm the deletion of the Public IP.</span></span>

```powershell
$PubIP | foreach-object {remove-azurermpublicIpAddress -Name $_.Name -ResourceGroupName "<NameOfResourceGroup1>"}
```

### <a name="4-delete-the-gateway-subnet-and-set-the-configuration"></a><span data-ttu-id="4a5ab-206">4.刪除閘道子網路並設定組態。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-206">4. Delete the gateway subnet and set the configuration.</span></span>

```powershell
$GWSub = Get-AzureRmVirtualNetwork -ResourceGroupName "RG1" -Name "VNet1" | Remove-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet"
Set-AzureRmVirtualNetwork -VirtualNetwork $GWSub
```

## <span data-ttu-id="4a5ab-207"><a name="delete"></a>藉由刪除資源群組來刪除 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="4a5ab-207"><a name="delete"></a>Delete a VPN gateway by deleting the resource group</span></span>

<span data-ttu-id="4a5ab-208">如果您不在乎保留資源群組中任何資源，而只想要從頭開始，您可以刪除整個資源群組。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-208">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span></span> <span data-ttu-id="4a5ab-209">這是移除所有項目的快速方法。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-209">This is a quick way to remove everything.</span></span> <span data-ttu-id="4a5ab-210">下列步驟僅適用於 Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-210">The following steps apply only to the Resource Manager deployment model.</span></span>

### <a name="1-get-a-list-of-all-the-resource-groups-in-your-subscription"></a><span data-ttu-id="4a5ab-211">1.取得訂用帳戶中的所有資源群組。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-211">1. Get a list of all the resource groups in your subscription.</span></span>

```powershell
Get-AzureRmResourceGroup
```

### <a name="2-locate-the-resource-group-that-you-want-to-delete"></a><span data-ttu-id="4a5ab-212">2.找出您想要刪除的資源群組。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-212">2. Locate the resource group that you want to delete.</span></span>

<span data-ttu-id="4a5ab-213">找出您想要刪除的資源群組，並檢視該資源群組中的資源清單。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-213">Locate the resource group that you want to delete and view the list of resources in that resource group.</span></span> <span data-ttu-id="4a5ab-214">在此範例中，資源群組的名稱為 RG1。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-214">In the example, the name of the resource group is RG1.</span></span> <span data-ttu-id="4a5ab-215">修改範例，以擷取所有資源的清單。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-215">Modify the example to retrieve a list of all the resources.</span></span>

```powershell
Find-AzureRmResource -ResourceGroupNameContains RG1
```

### <a name="3-verify-the-resources-in-the-list"></a><span data-ttu-id="4a5ab-216">3.確認清單中的資源。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-216">3. Verify the resources in the list.</span></span>

<span data-ttu-id="4a5ab-217">清單傳回後，請加以檢閱，確認您想要刪除資源群組中的所有資源，以及資源群組本身。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-217">When the list is returned, review it to verify that you want to delete all the resources in the resource group, as well as the resource group itself.</span></span> <span data-ttu-id="4a5ab-218">如果您想要保留資源群組中的某些資源，請使用本文先前小節中的步驟來刪除您的閘道。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-218">If you want to keep some of the resources in the resource group, use the steps in the earlier sections of this article to delete your gateway.</span></span>

### <a name="4-delete-the-resource-group-and-resources"></a><span data-ttu-id="4a5ab-219">4.刪除資源群組和資源。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-219">4. Delete the resource group and resources.</span></span>

<span data-ttu-id="4a5ab-220">若要刪除資源群組和資源群組內含的所有資源，請修改範例並執行。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-220">To delete the resource group and all the resource contained in the resource group, modify the example and run.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name RG1
```

### <a name="5-check-the-status"></a><span data-ttu-id="4a5ab-221">5.檢查狀態。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-221">5. Check the status.</span></span>

<span data-ttu-id="4a5ab-222">Azure 需花一些時間刪除所有資源。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-222">It takes some time for Azure to delete all the resources.</span></span> <span data-ttu-id="4a5ab-223">您可以使用 Cmdlet 檢查資源群組的狀態。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-223">You can check the status of your resource group by using this cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -ResourceGroupName RG1
```

<span data-ttu-id="4a5ab-224">傳回的結果顯示「成功」。</span><span class="sxs-lookup"><span data-stu-id="4a5ab-224">The result that is returned shows 'Succeeded'.</span></span>

```
ResourceGroupName : RG1
Location          : eastus
ProvisioningState : Succeeded
```