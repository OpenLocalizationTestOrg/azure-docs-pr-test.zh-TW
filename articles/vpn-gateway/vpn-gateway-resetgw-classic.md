---
title: "重設 Azure VPN 閘道 tooreestablish IPsec 通道數 |Microsoft 文件"
description: "這篇文章會引導您重設您的 Azure VPN 閘道 tooreestablish IPsec 通道。 hello 文章適用 tooVPN 閘道在傳統，hello 和 hello 資源管理員部署模型。"
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 79d77cb8-d175-4273-93ac-712d7d45b1fe
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: cherylmc
ms.openlocfilehash: 84dd741f0bebd6b18cb235216a68a88da5fe17b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="reset-a-vpn-gateway"></a><span data-ttu-id="c38db-104">重設 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="c38db-104">Reset a VPN Gateway</span></span>

<span data-ttu-id="c38db-105">如果您遺失一或多個站對站 VPN 通道上的跨單位 VPN 連線，重設 Azure VPN 閘道會很有幫助。</span><span class="sxs-lookup"><span data-stu-id="c38db-105">Resetting an Azure VPN gateway is helpful if you lose cross-premises VPN connectivity on one or more Site-to-Site VPN tunnels.</span></span> <span data-ttu-id="c38db-106">在此情況下，您在內部部署 VPN 裝置是所有運作正常，但您不能 tooestablish 與 hello Azure VPN 閘道 IPsec 通道。</span><span class="sxs-lookup"><span data-stu-id="c38db-106">In this situation, your on-premises VPN devices are all working correctly, but are not able tooestablish IPsec tunnels with hello Azure VPN gateways.</span></span> <span data-ttu-id="c38db-107">本文可協助您重設 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="c38db-107">This article helps you reset your VPN gateway.</span></span>

### <a name="what-happens-during-a-reset"></a><span data-ttu-id="c38db-108">重設期間會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="c38db-108">What happens during a reset?</span></span>

<span data-ttu-id="c38db-109">VPN 閘道是由兩個在「作用中-待命」設定中執行的 VM 執行個體所組成。</span><span class="sxs-lookup"><span data-stu-id="c38db-109">A VPN gateway is composed of two VM instances running in an active-standby configuration.</span></span> <span data-ttu-id="c38db-110">當您重設 hello 閘道時，它會重新啟動 hello 閘道，然後重新套用 hello 跨單位組態 tooit。</span><span class="sxs-lookup"><span data-stu-id="c38db-110">When you reset hello gateway, it reboots hello gateway, and then reapplies hello cross-premises configurations tooit.</span></span> <span data-ttu-id="c38db-111">hello 閘道會保留 hello 已經有公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c38db-111">hello gateway keeps hello public IP address it already has.</span></span> <span data-ttu-id="c38db-112">這表示您不需要 tooupdate hello VPN 路由器設定新的公用 IP 位址的 Azure VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="c38db-112">This means you won’t need tooupdate hello VPN router configuration with a new public IP address for Azure VPN gateway.</span></span>

<span data-ttu-id="c38db-113">當您發出 hello 命令 tooreset hello 閘道時，hello 目前作用中的執行個體 hello Azure VPN 閘道立即重新開機。</span><span class="sxs-lookup"><span data-stu-id="c38db-113">When you issue hello command tooreset hello gateway, hello current active instance of hello Azure VPN gateway is rebooted immediately.</span></span> <span data-ttu-id="c38db-114">Hello hello 作用中執行個體 （即將重新開機），toohello 待命執行個體容錯移轉期間會有短暫的間隔。</span><span class="sxs-lookup"><span data-stu-id="c38db-114">There will be a brief gap during hello failover from hello active instance (being rebooted), toohello standby instance.</span></span> <span data-ttu-id="c38db-115">hello 間距應該小於一分鐘。</span><span class="sxs-lookup"><span data-stu-id="c38db-115">hello gap should be less than one minute.</span></span>

<span data-ttu-id="c38db-116">如果未還原 hello 連接 hello 第一次重新開機後，問題 hello 相同命令再次 tooreboot hello 第二個 VM 執行個體 （hello 新使用中的閘道）。</span><span class="sxs-lookup"><span data-stu-id="c38db-116">If hello connection is not restored after hello first reboot, issue hello same command again tooreboot hello second VM instance (hello new active gateway).</span></span> <span data-ttu-id="c38db-117">要求後 tooback hello 兩次重新開機時，會有稍微更長的時間 （作用中與待命） 這兩個 VM 執行個體，即將重新開機。</span><span class="sxs-lookup"><span data-stu-id="c38db-117">If hello two reboots are requested back tooback, there will be a slightly longer period where both VM instances (active and standby) are being rebooted.</span></span> <span data-ttu-id="c38db-118">這會導致較長的間隔上 hello VPN 連線能力，向上 too2 too4 分鐘 Vm toocomplete hello 重新開機。</span><span class="sxs-lookup"><span data-stu-id="c38db-118">This will cause a longer gap on hello VPN connectivity, up too2 too4 minutes for VMs toocomplete hello reboots.</span></span>

<span data-ttu-id="c38db-119">在兩次重新開機之後, 如果仍發生跨單位連線問題，請開啟支援要求從 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="c38db-119">After two reboots, if you are still experiencing cross-premises connectivity problems, please open a support request from hello Azure portal.</span></span>

## <span data-ttu-id="c38db-120"><a name="before"></a>開始之前</span><span class="sxs-lookup"><span data-stu-id="c38db-120"><a name="before"></a>Before you begin</span></span>

<span data-ttu-id="c38db-121">您重設您的閘道之前，請確認以下列出每個 IPsec-網站 (S2S) VPN 通道的 hello 索引鍵的項目。</span><span class="sxs-lookup"><span data-stu-id="c38db-121">Before you reset your gateway, verify hello key items listed below for each IPsec Site-to-Site (S2S) VPN tunnel.</span></span> <span data-ttu-id="c38db-122">Hello 項目中的任何不相符會導致 hello 中斷連線的 S2S VPN 通道。</span><span class="sxs-lookup"><span data-stu-id="c38db-122">Any mismatch in hello items will result in hello disconnect of S2S VPN tunnels.</span></span> <span data-ttu-id="c38db-123">正在驗證及更正您在內部部署和 Azure VPN 閘道的 hello 組態可讓您不需要重新開機，並中斷的 hello hello 閘道上的其他工作連接。</span><span class="sxs-lookup"><span data-stu-id="c38db-123">Verifying and correcting hello configurations for your on-premises and Azure VPN gateways saves you from unnecessary reboots and disruptions for hello other working connections on hello gateways.</span></span>

<span data-ttu-id="c38db-124">請確認下列項目重設您的閘道器之前的 hello:</span><span class="sxs-lookup"><span data-stu-id="c38db-124">Verify hello following items before resetting your gateway:</span></span>

* <span data-ttu-id="c38db-125">hello 網際網路 IP 位址 (Vip) 這兩個 hello Azure VPN 閘道和 hello 內部部署 VPN 閘道已正確設定這兩個 hello 在內部部署 VPN Azure 與 hello 原則中。</span><span class="sxs-lookup"><span data-stu-id="c38db-125">hello Internet IP addresses (VIPs) for both hello Azure VPN gateway and hello on-premises VPN gateway are configured correctly in both hello Azure and hello on-premises VPN policies.</span></span>
* <span data-ttu-id="c38db-126">hello 預先共用的金鑰必須 hello Azure 與內部部署 VPN 閘道上相同。</span><span class="sxs-lookup"><span data-stu-id="c38db-126">hello pre-shared key must be hello same on both Azure and on-premises VPN gateways.</span></span>
* <span data-ttu-id="c38db-127">如果您要套用特定的 IPsec/IKE 組態，例如加密，雜湊演算法和 PFS （完整轉寄密碼），請確定兩者 hello Azure 和內部部署 VPN 閘道具有 hello 相同的組態。</span><span class="sxs-lookup"><span data-stu-id="c38db-127">If you apply specific IPsec/IKE configuration, such as encryption, hashing algorithms, and PFS (Perfect Forward Secrecy), ensure both hello Azure and on-premises VPN gateways have hello same configurations.</span></span>

## <span data-ttu-id="c38db-128"><a name="portal"></a>Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="c38db-128"><a name="portal"></a>Azure portal</span></span>

<span data-ttu-id="c38db-129">您可以重設資源管理員 VPN 閘道使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="c38db-129">You can reset a Resource Manager VPN gateway using hello Azure portal.</span></span> <span data-ttu-id="c38db-130">如果您想 tooreset 傳統的閘道，請參閱 hello [PowerShell](#resetclassic)步驟。</span><span class="sxs-lookup"><span data-stu-id="c38db-130">If you want tooreset a classic gateway, see hello [PowerShell](#resetclassic) steps.</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="c38db-131">資源管理員部署模型。</span><span class="sxs-lookup"><span data-stu-id="c38db-131">Resource Manager deployment model</span></span>

1. <span data-ttu-id="c38db-132">開啟 hello [Azure 入口網站](https://portal.azure.com)並瀏覽您想 tooreset toohello 資源管理員虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="c38db-132">Open hello [Azure portal](https://portal.azure.com) and navigate toohello Resource Manager virtual network gateway that you want tooreset.</span></span>
2. <span data-ttu-id="c38db-133">在 hello 刀鋒視窗中的 hello 虛擬網路閘道，按一下 重設。</span><span class="sxs-lookup"><span data-stu-id="c38db-133">On hello blade for hello virtual network gateway, click 'Reset'.</span></span>

  ![重設 VPN 閘道刀鋒視窗](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. <span data-ttu-id="c38db-135">在 [hello 重刀鋒視窗，請按一下 hello**重設**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c38db-135">On hello Reset blade, click hello **Reset** button.</span></span>

## <span data-ttu-id="c38db-136"><a name="ps"></a>PowerShell</span><span class="sxs-lookup"><span data-stu-id="c38db-136"><a name="ps"></a>PowerShell</span></span>

### <a name="resource-manager-deployment-model"></a><span data-ttu-id="c38db-137">資源管理員部署模型。</span><span class="sxs-lookup"><span data-stu-id="c38db-137">Resource Manager deployment model</span></span>

<span data-ttu-id="c38db-138">重設閘道為 hello cmdlet**重設 AzureRmVirtualNetworkGateway**。</span><span class="sxs-lookup"><span data-stu-id="c38db-138">hello cmdlet for resetting a gateway is **Reset-AzureRmVirtualNetworkGateway**.</span></span> <span data-ttu-id="c38db-139">在之前執行重設，請確定您擁有 hello 最新版本的 hello[資源管理員 PowerShell cmdlet](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0)。</span><span class="sxs-lookup"><span data-stu-id="c38db-139">Before performing a reset, make sure you have hello latest version of hello [Resource Manager PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).</span></span> <span data-ttu-id="c38db-140">hello 下列範例會重設虛擬網路閘道 hello TestRG1 資源群組中名為 VNet1GW:</span><span class="sxs-lookup"><span data-stu-id="c38db-140">hello following example resets a virtual network gateway named VNet1GW in hello TestRG1 resource group:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

<span data-ttu-id="c38db-141">結果︰</span><span class="sxs-lookup"><span data-stu-id="c38db-141">Result:</span></span>

<span data-ttu-id="c38db-142">當您收到傳回的結果時，您可以假設 hello 閘道重設成功。</span><span class="sxs-lookup"><span data-stu-id="c38db-142">When you receive a return result, you can assume hello gateway reset was successful.</span></span> <span data-ttu-id="c38db-143">不過，並沒有明確地指出該 hello 重設成功的 hello 傳回結果中。</span><span class="sxs-lookup"><span data-stu-id="c38db-143">However, there is nothing in hello return result that indicates explicitly that hello reset was successful.</span></span> <span data-ttu-id="c38db-144">如果您想在 hello 記錄 toosee 密切 toolook 完全 hello 閘道重設時發生，您可以檢視該資訊在 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="c38db-144">If you want toolook closely at hello history toosee exactly when hello gateway reset occurred, you can view that information in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c38db-145">在 hello 入口網站中，瀏覽過**'GatewayName'-> 資源健全狀況**。</span><span class="sxs-lookup"><span data-stu-id="c38db-145">In hello portal, navigate too**'GatewayName' -> Resource Health**.</span></span>

### <span data-ttu-id="c38db-146"><a name="resetclassic"></a>傳統部署模型</span><span class="sxs-lookup"><span data-stu-id="c38db-146"><a name="resetclassic"></a>Classic deployment model</span></span>

<span data-ttu-id="c38db-147">重設閘道為 hello cmdlet**重設 AzureVNetGateway**。</span><span class="sxs-lookup"><span data-stu-id="c38db-147">hello cmdlet for resetting a gateway is **Reset-AzureVNetGateway**.</span></span> <span data-ttu-id="c38db-148">在之前執行重設，請確定您擁有 hello 最新版本的 hello[服務管理 (SM) PowerShell cmdlet](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0)。</span><span class="sxs-lookup"><span data-stu-id="c38db-148">Before performing a reset, make sure you have hello latest version of hello [Service Management (SM) PowerShell cmdlets](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0).</span></span> <span data-ttu-id="c38db-149">hello 下列範例會重設虛擬網路，名為"ContosoVNet"hello 閘道：</span><span class="sxs-lookup"><span data-stu-id="c38db-149">hello following example resets hello gateway for a virtual network named "ContosoVNet":</span></span>

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

<span data-ttu-id="c38db-150">結果︰</span><span class="sxs-lookup"><span data-stu-id="c38db-150">Result:</span></span>

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <span data-ttu-id="c38db-151"><a name="cli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c38db-151"><a name="cli"></a>Azure CLI</span></span>

<span data-ttu-id="c38db-152">tooreset hello 閘道，使用 hello [az 網路 vnet 閘道重設](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset)命令。</span><span class="sxs-lookup"><span data-stu-id="c38db-152">tooreset hello gateway, use hello [az network vnet-gateway reset](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) command.</span></span> <span data-ttu-id="c38db-153">hello 下列範例會重設虛擬網路閘道 hello TestRG5 資源群組中名為 VNet5GW:</span><span class="sxs-lookup"><span data-stu-id="c38db-153">hello following example resets a virtual network gateway named VNet5GW in hello TestRG5 resource group:</span></span>

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

<span data-ttu-id="c38db-154">結果︰</span><span class="sxs-lookup"><span data-stu-id="c38db-154">Result:</span></span>

<span data-ttu-id="c38db-155">當您收到傳回的結果時，您可以假設 hello 閘道重設成功。</span><span class="sxs-lookup"><span data-stu-id="c38db-155">When you receive a return result, you can assume hello gateway reset was successful.</span></span> <span data-ttu-id="c38db-156">不過，並沒有明確地指出該 hello 重設成功的 hello 傳回結果中。</span><span class="sxs-lookup"><span data-stu-id="c38db-156">However, there is nothing in hello return result that indicates explicitly that hello reset was successful.</span></span> <span data-ttu-id="c38db-157">如果您想在 hello 記錄 toosee 密切 toolook 完全 hello 閘道重設時發生，您可以檢視該資訊在 hello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="c38db-157">If you want toolook closely at hello history toosee exactly when hello gateway reset occurred, you can view that information in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c38db-158">在 hello 入口網站中，瀏覽過**'GatewayName'-> 資源健全狀況**。</span><span class="sxs-lookup"><span data-stu-id="c38db-158">In hello portal, navigate too**'GatewayName' -> Resource Health**.</span></span>
