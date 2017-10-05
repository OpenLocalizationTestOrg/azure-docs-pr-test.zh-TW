---
title: "針對 Azure 站對站 VPN 連線無法連線進行疑難排解| Microsoft Docs"
description: "了解如何針對突然停止運作且無法重新連線的站對站 VPN 連線進行疑難排解。"
services: vpn-gateway
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/21/2017
ms.author: genli
ms.openlocfilehash: e7a3da64895f0307e5d6c3563672205a2f93a7d2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a><span data-ttu-id="11e17-103">疑難排解：Azure 站對站 VPN 連線無法連線並停止運作</span><span class="sxs-lookup"><span data-stu-id="11e17-103">Troubleshooting: An Azure site-to-site VPN connection cannot connect and stops working</span></span>

<span data-ttu-id="11e17-104">當您在內部部署網路與 Azure 虛擬網路之間設定站對站 VPN 連線之後，該 VPN 連線突然停止運作且無法重新連線。</span><span class="sxs-lookup"><span data-stu-id="11e17-104">After you configure a site-to-site VPN connection between an on-premises network and an Azure virtual network, the VPN connection suddenly stops working and cannot be reconnected.</span></span> <span data-ttu-id="11e17-105">本文提供可協助您解決此問題的疑難排解步驟。</span><span class="sxs-lookup"><span data-stu-id="11e17-105">This article provides troubleshooting steps to help you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="11e17-106">疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="11e17-106">Troubleshooting steps</span></span>

<span data-ttu-id="11e17-107">若要解決此問題，請先嘗試[重設 Azure VPN 閘道](vpn-gateway-resetgw-classic.md)，並從內部部署 VPN 裝置重設通道。</span><span class="sxs-lookup"><span data-stu-id="11e17-107">To resolve the problem, first try to [reset the Azure VPN gateway](vpn-gateway-resetgw-classic.md) and reset the tunnel from the on-premises VPN device.</span></span> <span data-ttu-id="11e17-108">如果問題持續發生，請依照下列步驟執行以找出問題的原因。</span><span class="sxs-lookup"><span data-stu-id="11e17-108">If the problem persists, follow these steps to identify the cause of the problem.</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="11e17-109">必要步驟</span><span class="sxs-lookup"><span data-stu-id="11e17-109">Prerequisite step</span></span>

<span data-ttu-id="11e17-110">檢查 Azure VPN 閘道的類型。</span><span class="sxs-lookup"><span data-stu-id="11e17-110">Check the type of the Azure VPN gateway.</span></span>

1. <span data-ttu-id="11e17-111">移至 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="11e17-111">Go to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="11e17-112">檢查 VPN 閘道的 [概觀] 頁面來取得類型資訊。</span><span class="sxs-lookup"><span data-stu-id="11e17-112">Check the **Overview** page of the VPN gateway for the type information.</span></span>
    
    ![閘道概觀](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-the-on-premises-vpn-device-is-validated"></a><span data-ttu-id="11e17-114">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="11e17-114">Step 1.</span></span> <span data-ttu-id="11e17-115">檢查內部部署 VPN 裝置是否經過驗證</span><span class="sxs-lookup"><span data-stu-id="11e17-115">Check whether the on-premises VPN device is validated</span></span>

1. <span data-ttu-id="11e17-116">檢查您是否使用[經過驗證的 VPN 裝置和作業系統版本](vpn-gateway-about-vpn-devices.md#devicetable)。</span><span class="sxs-lookup"><span data-stu-id="11e17-116">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="11e17-117">如果裝置不是經過驗證的 VPN 裝置，您可能需要連絡裝置製造商，以了解是否有任何相容性問題。</span><span class="sxs-lookup"><span data-stu-id="11e17-117">If the device is not a validated VPN device, you might have to contact the device manufacturer to see if there is a compatibility issue.</span></span>

2. <span data-ttu-id="11e17-118">確定已正確設定 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="11e17-118">Make sure that the VPN device is correctly configured.</span></span> <span data-ttu-id="11e17-119">如需詳細資訊，請參閱[編輯裝置組態範例](/vpn-gateway-about-vpn-devices.md#editing)。</span><span class="sxs-lookup"><span data-stu-id="11e17-119">For more information, see [Edit device configuration samples](/vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-verify-the-shared-key"></a><span data-ttu-id="11e17-120">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="11e17-120">Step 2.</span></span> <span data-ttu-id="11e17-121">確認共用金鑰</span><span class="sxs-lookup"><span data-stu-id="11e17-121">Verify the shared key</span></span>

<span data-ttu-id="11e17-122">比較內部部署 VPN 裝置和 Azure 虛擬網路 VPN 的共用金鑰，以確認金鑰相符合。</span><span class="sxs-lookup"><span data-stu-id="11e17-122">Compare the shared key for the on-premises VPN device to the Azure Virtual Network VPN to make sure that the keys match.</span></span> 

<span data-ttu-id="11e17-123">若要檢視 Azure VPN 連線的共用金鑰，請使用下列其中一個方法：</span><span class="sxs-lookup"><span data-stu-id="11e17-123">To view the shared key for the Azure VPN connection, use one of the following methods:</span></span>

<span data-ttu-id="11e17-124">**Azure 入口網站**</span><span class="sxs-lookup"><span data-stu-id="11e17-124">**Azure portal**</span></span>

1. <span data-ttu-id="11e17-125">移至您建立的 VPN 閘道站對站連線。</span><span class="sxs-lookup"><span data-stu-id="11e17-125">Go to the VPN gateway site-to-site connection that you created.</span></span>

2. <span data-ttu-id="11e17-126">在 [設定] 區段中，按一下 [共用金鑰]。</span><span class="sxs-lookup"><span data-stu-id="11e17-126">In the **Settings** section, click **Shared key**.</span></span>
    
    ![共用金鑰](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

<span data-ttu-id="11e17-128">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="11e17-128">**Azure PowerShell**</span></span>

<span data-ttu-id="11e17-129">針對 Azure Resource Manager 部署模型：</span><span class="sxs-lookup"><span data-stu-id="11e17-129">For the Azure Resource Manager deployment model:</span></span>

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

<span data-ttu-id="11e17-130">針對傳統部署模型：</span><span class="sxs-lookup"><span data-stu-id="11e17-130">For the classic deployment model:</span></span>

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-the-vpn-peer-ips"></a><span data-ttu-id="11e17-131">步驟 3.</span><span class="sxs-lookup"><span data-stu-id="11e17-131">Step 3.</span></span> <span data-ttu-id="11e17-132">確認 VPN 對等互連 IP</span><span class="sxs-lookup"><span data-stu-id="11e17-132">Verify the VPN peer IPs</span></span>

-   <span data-ttu-id="11e17-133">Azure 中「區域網路閘道」物件內的 IP 定義應與內部部署裝置 IP 相符合。</span><span class="sxs-lookup"><span data-stu-id="11e17-133">The IP definition in the **Local Network Gateway** object in Azure should match the on-premises device IP.</span></span>
-   <span data-ttu-id="11e17-134">內部部署裝置上設定的 Azure 閘道 IP 定義應與 Azure 閘道 IP 相符合。</span><span class="sxs-lookup"><span data-stu-id="11e17-134">The Azure gateway IP definition that is set on the on-premises device should match the Azure gateway IP.</span></span>

### <a name="step-4-check-udr-and-nsgs-on-the-gateway-subnet"></a><span data-ttu-id="11e17-135">步驟 4.</span><span class="sxs-lookup"><span data-stu-id="11e17-135">Step 4.</span></span> <span data-ttu-id="11e17-136">檢查閘道子網路上的 UDR 和 NSG</span><span class="sxs-lookup"><span data-stu-id="11e17-136">Check UDR and NSGs on the gateway subnet</span></span>

<span data-ttu-id="11e17-137">檢查並移除閘道子網路上的使用者定義路由 (UDR) 或網路安全性群組 (NSG)，然後測試結果。</span><span class="sxs-lookup"><span data-stu-id="11e17-137">Check for and remove user-defined routing (UDR) or Network Security Groups (NSGs) on the gateway subnet, and then test the result.</span></span> <span data-ttu-id="11e17-138">如果問題已解決，請驗證 UDR 或 NSG 套用的設定。</span><span class="sxs-lookup"><span data-stu-id="11e17-138">If the problem is resolved, validate the settings that UDR or NSG applied.</span></span>

### <a name="step-5-check-the-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="11e17-139">步驟 5。</span><span class="sxs-lookup"><span data-stu-id="11e17-139">Step 5.</span></span> <span data-ttu-id="11e17-140">檢查內部部署 VPN 裝置外部介面位址</span><span class="sxs-lookup"><span data-stu-id="11e17-140">Check the on-premises VPN device external interface address</span></span>

- <span data-ttu-id="11e17-141">如果 Azure 的**區域網路**定義中包含 VPN 裝置的網際網路對應 IP 位址，則您可能偶爾會遇到連線中斷的情況。</span><span class="sxs-lookup"><span data-stu-id="11e17-141">If the Internet-facing IP address of the VPN device is included in the **Local network** definition in Azure, you might experience sporadic disconnections.</span></span>
- <span data-ttu-id="11e17-142">裝置的外部介面必須直接位在網際網路上。</span><span class="sxs-lookup"><span data-stu-id="11e17-142">The device's external interface must be directly on the Internet.</span></span> <span data-ttu-id="11e17-143">網際網路與裝置之間不應該有網路位址轉譯或防火牆。</span><span class="sxs-lookup"><span data-stu-id="11e17-143">There should be no network address translation or firewall between the Internet and the device.</span></span>
- <span data-ttu-id="11e17-144">若要設定防火牆叢集以具有虛擬 IP，您必須解散叢集，並直接將 VPN 設備公開給閘道可介接的公用介面。</span><span class="sxs-lookup"><span data-stu-id="11e17-144">To configure firewall clustering to have a virtual IP, you must break the cluster and expose the VPN appliance directly to a public interface that the gateway can interface with.</span></span>

### <a name="step-6-verify-that-the-subnets-match-exactly-azure-policy-based-gateways"></a><span data-ttu-id="11e17-145">步驟 6.</span><span class="sxs-lookup"><span data-stu-id="11e17-145">Step 6.</span></span> <span data-ttu-id="11e17-146">確認子網路完全相符合 (Azure 原則式閘道)</span><span class="sxs-lookup"><span data-stu-id="11e17-146">Verify that the subnets match exactly (Azure policy-based gateways)</span></span>

-   <span data-ttu-id="11e17-147">確認子網路在 Azure 虛擬網路和 Azure 虛擬網路的內部部署定義之間完全相符合。</span><span class="sxs-lookup"><span data-stu-id="11e17-147">Verify that the subnets match exactly between the Azure virtual network and on-premises definitions for the Azure virtual network.</span></span>
-   <span data-ttu-id="11e17-148">確認子網路在**區域網路閘道**和內部部署網路的內部部署定義之間完全相符合。</span><span class="sxs-lookup"><span data-stu-id="11e17-148">Verify that the subnets match exactly between the **Local Network Gateway** and on-premises definitions for the on-premises network.</span></span>

### <a name="step-7-verify-the-azure-gateway-health-probe"></a><span data-ttu-id="11e17-149">步驟 7.</span><span class="sxs-lookup"><span data-stu-id="11e17-149">Step 7.</span></span> <span data-ttu-id="11e17-150">確認 Azure 閘道健康狀態探查</span><span class="sxs-lookup"><span data-stu-id="11e17-150">Verify the Azure gateway health probe</span></span>

1. <span data-ttu-id="11e17-151">移至[健康狀態探查](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe)。</span><span class="sxs-lookup"><span data-stu-id="11e17-151">Go to the [health probe](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span></span>

2. <span data-ttu-id="11e17-152">按一下以略過憑證警告。</span><span class="sxs-lookup"><span data-stu-id="11e17-152">Click through the certificate warning.</span></span>
3. <span data-ttu-id="11e17-153">如果您收到回應，表示 VPN 閘道的健康狀態良好。</span><span class="sxs-lookup"><span data-stu-id="11e17-153">If you receive a response, the VPN gateway is considered healthy.</span></span> <span data-ttu-id="11e17-154">如果未收到回應，閘道的健康狀態可能有問題，或可能是閘道子網路上的 NSG 造成問題。</span><span class="sxs-lookup"><span data-stu-id="11e17-154">If you don't receive a response, the gateway might not be healthy or an NSG on the gateway subnet is causing the problem.</span></span> <span data-ttu-id="11e17-155">下列文字是回應的範例：</span><span class="sxs-lookup"><span data-stu-id="11e17-155">The following text is a sample response:</span></span>

    <span data-ttu-id="11e17-156">&lt;?xml version="1.0"?> <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">主要執行個體: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span><span class="sxs-lookup"><span data-stu-id="11e17-156">&lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span></span>

### <a name="step-8-check-whether-the-on-premises-vpn-device-has-the-perfect-forward-secrecy-feature-enabled"></a><span data-ttu-id="11e17-157">步驟 8。</span><span class="sxs-lookup"><span data-stu-id="11e17-157">Step 8.</span></span> <span data-ttu-id="11e17-158">檢查內部部署 VPN 裝置是否已啟用完整轉寄密碼功能</span><span class="sxs-lookup"><span data-stu-id="11e17-158">Check whether the on-premises VPN device has the perfect forward secrecy feature enabled</span></span>

<span data-ttu-id="11e17-159">完整轉寄密碼功能可能會造成連線中斷的問題。</span><span class="sxs-lookup"><span data-stu-id="11e17-159">The perfect forward secrecy feature can cause disconnection problems.</span></span> <span data-ttu-id="11e17-160">如果 VPN 裝置已啟用完整轉寄密碼，請停用該功能。</span><span class="sxs-lookup"><span data-stu-id="11e17-160">If the VPN device has perfect forward secrecy enabled, disable the feature.</span></span> <span data-ttu-id="11e17-161">然後更新 VPN 閘道 IPsec 原則。</span><span class="sxs-lookup"><span data-stu-id="11e17-161">Then update the VPN gateway IPsec policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="11e17-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="11e17-162">Next steps</span></span>

-   [<span data-ttu-id="11e17-163">設定對虛擬網路的站對站連線</span><span class="sxs-lookup"><span data-stu-id="11e17-163">Configure a site-to-site connection to a virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [<span data-ttu-id="11e17-164">設定站對站 VPN 連線的 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="11e17-164">Configure an IPsec/IKE policy for site-to-site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)
