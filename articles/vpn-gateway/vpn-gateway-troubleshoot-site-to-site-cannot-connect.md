---
title: "aaaTroubleshoot 無法連線 Azure 站台對站 VPN 連線 |Microsoft 文件"
description: "深入了解如何 tootroubleshoot 站對站 VPN 連線的突然停止運作，而且無法重新連接。"
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
ms.openlocfilehash: 632c75bfcfb93a532eeead2855d43e6614569a99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a><span data-ttu-id="7c451-103">疑難排解：Azure 站對站 VPN 連線無法連線並停止運作</span><span class="sxs-lookup"><span data-stu-id="7c451-103">Troubleshooting: An Azure site-to-site VPN connection cannot connect and stops working</span></span>

<span data-ttu-id="7c451-104">您設定站對站 VPN 連接內部部署網路與 Azure 虛擬網路之間之後，hello VPN 連線突然停止運作，而且無法重新連接。</span><span class="sxs-lookup"><span data-stu-id="7c451-104">After you configure a site-to-site VPN connection between an on-premises network and an Azure virtual network, hello VPN connection suddenly stops working and cannot be reconnected.</span></span> <span data-ttu-id="7c451-105">本文章提供疑難排解步驟 toohelp 解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="7c451-105">This article provides troubleshooting steps toohelp you resolve this problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="7c451-106">疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="7c451-106">Troubleshooting steps</span></span>

<span data-ttu-id="7c451-107">tooresolve hello 問題，請先嘗試過[重設 hello Azure VPN 閘道](vpn-gateway-resetgw-classic.md)並重設 hello 在內部部署 VPN 裝置 hello 通道。</span><span class="sxs-lookup"><span data-stu-id="7c451-107">tooresolve hello problem, first try too[reset hello Azure VPN gateway](vpn-gateway-resetgw-classic.md) and reset hello tunnel from hello on-premises VPN device.</span></span> <span data-ttu-id="7c451-108">如果 hello 問題持續發生，請遵循這些步驟 tooidentify hello 問題的原因 hello。</span><span class="sxs-lookup"><span data-stu-id="7c451-108">If hello problem persists, follow these steps tooidentify hello cause of hello problem.</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="7c451-109">必要步驟</span><span class="sxs-lookup"><span data-stu-id="7c451-109">Prerequisite step</span></span>

<span data-ttu-id="7c451-110">請檢查 hello hello Azure VPN 閘道類型。</span><span class="sxs-lookup"><span data-stu-id="7c451-110">Check hello type of hello Azure VPN gateway.</span></span>

1. <span data-ttu-id="7c451-111">移 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="7c451-111">Go toohello [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="7c451-112">檢查 hello**概觀**hello hello 類型資訊的 VPN 閘道的頁面。</span><span class="sxs-lookup"><span data-stu-id="7c451-112">Check hello **Overview** page of hello VPN gateway for hello type information.</span></span>
    
    ![Hello 閘道的概觀](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a><span data-ttu-id="7c451-114">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="7c451-114">Step 1.</span></span> <span data-ttu-id="7c451-115">檢查是否已驗證 hello 在內部部署 VPN 裝置</span><span class="sxs-lookup"><span data-stu-id="7c451-115">Check whether hello on-premises VPN device is validated</span></span>

1. <span data-ttu-id="7c451-116">檢查您是否使用[經過驗證的 VPN 裝置和作業系統版本](vpn-gateway-about-vpn-devices.md#devicetable)。</span><span class="sxs-lookup"><span data-stu-id="7c451-116">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="7c451-117">如果 hello 裝置不是已驗證的 VPN 裝置，您可能必須 toocontact hello 裝置製造商 toosee，如有相容性問題。</span><span class="sxs-lookup"><span data-stu-id="7c451-117">If hello device is not a validated VPN device, you might have toocontact hello device manufacturer toosee if there is a compatibility issue.</span></span>

2. <span data-ttu-id="7c451-118">請確定已正確設定該 hello VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="7c451-118">Make sure that hello VPN device is correctly configured.</span></span> <span data-ttu-id="7c451-119">如需詳細資訊，請參閱[編輯裝置組態範例](/vpn-gateway-about-vpn-devices.md#editing)。</span><span class="sxs-lookup"><span data-stu-id="7c451-119">For more information, see [Edit device configuration samples](/vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-verify-hello-shared-key"></a><span data-ttu-id="7c451-120">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="7c451-120">Step 2.</span></span> <span data-ttu-id="7c451-121">確認 hello 共用的金鑰</span><span class="sxs-lookup"><span data-stu-id="7c451-121">Verify hello shared key</span></span>

<span data-ttu-id="7c451-122">比較 hello 在內部部署 VPN 裝置 toohello Azure 虛擬網路 VPN toomake 確定 hello 索引鍵相符的 hello 共用的金鑰。</span><span class="sxs-lookup"><span data-stu-id="7c451-122">Compare hello shared key for hello on-premises VPN device toohello Azure Virtual Network VPN toomake sure that hello keys match.</span></span> 

<span data-ttu-id="7c451-123">tooview hello 共用的金鑰 hello Azure VPN 連線，使用其中一種 hello 下列方法：</span><span class="sxs-lookup"><span data-stu-id="7c451-123">tooview hello shared key for hello Azure VPN connection, use one of hello following methods:</span></span>

<span data-ttu-id="7c451-124">**Azure 入口網站**</span><span class="sxs-lookup"><span data-stu-id="7c451-124">**Azure portal**</span></span>

1. <span data-ttu-id="7c451-125">移 toohello VPN 閘道站對站連線，您所建立。</span><span class="sxs-lookup"><span data-stu-id="7c451-125">Go toohello VPN gateway site-to-site connection that you created.</span></span>

2. <span data-ttu-id="7c451-126">在 hello**設定**區段中，按一下**共用金鑰**。</span><span class="sxs-lookup"><span data-stu-id="7c451-126">In hello **Settings** section, click **Shared key**.</span></span>
    
    ![共用金鑰](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

<span data-ttu-id="7c451-128">**Azure PowerShell**</span><span class="sxs-lookup"><span data-stu-id="7c451-128">**Azure PowerShell**</span></span>

<span data-ttu-id="7c451-129">Hello Azure Resource Manager 部署模型：</span><span class="sxs-lookup"><span data-stu-id="7c451-129">For hello Azure Resource Manager deployment model:</span></span>

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

<span data-ttu-id="7c451-130">Hello 傳統部署模型：</span><span class="sxs-lookup"><span data-stu-id="7c451-130">For hello classic deployment model:</span></span>

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-hello-vpn-peer-ips"></a><span data-ttu-id="7c451-131">步驟 3.</span><span class="sxs-lookup"><span data-stu-id="7c451-131">Step 3.</span></span> <span data-ttu-id="7c451-132">確認 hello VPN 對等 Ip</span><span class="sxs-lookup"><span data-stu-id="7c451-132">Verify hello VPN peer IPs</span></span>

-   <span data-ttu-id="7c451-133">hello IP 定義在 hello**本機網路閘道**在 Azure 中的物件應該符合 hello 在內部部署裝置的 IP。</span><span class="sxs-lookup"><span data-stu-id="7c451-133">hello IP definition in hello **Local Network Gateway** object in Azure should match hello on-premises device IP.</span></span>
-   <span data-ttu-id="7c451-134">hello Azure 閘道 IP 定義 hello 上所設定內部部署裝置應符合 hello Azure 閘道 IP。</span><span class="sxs-lookup"><span data-stu-id="7c451-134">hello Azure gateway IP definition that is set on hello on-premises device should match hello Azure gateway IP.</span></span>

### <a name="step-4-check-udr-and-nsgs-on-hello-gateway-subnet"></a><span data-ttu-id="7c451-135">步驟 4.</span><span class="sxs-lookup"><span data-stu-id="7c451-135">Step 4.</span></span> <span data-ttu-id="7c451-136">檢查 UDR 和 Nsg hello 閘道子網路</span><span class="sxs-lookup"><span data-stu-id="7c451-136">Check UDR and NSGs on hello gateway subnet</span></span>

<span data-ttu-id="7c451-137">檢查和移除 hello 閘道子網路上的使用者定義路由 (UDR) 或網路安全性群組 (Nsg)，然後測試 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="7c451-137">Check for and remove user-defined routing (UDR) or Network Security Groups (NSGs) on hello gateway subnet, and then test hello result.</span></span> <span data-ttu-id="7c451-138">如果 hello 問題已經解決，驗證 hello UDR 或 NSG 套用的設定。</span><span class="sxs-lookup"><span data-stu-id="7c451-138">If hello problem is resolved, validate hello settings that UDR or NSG applied.</span></span>

### <a name="step-5-check-hello-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="7c451-139">步驟 5。</span><span class="sxs-lookup"><span data-stu-id="7c451-139">Step 5.</span></span> <span data-ttu-id="7c451-140">核取 hello 內部部署 VPN 裝置的外部介面位址</span><span class="sxs-lookup"><span data-stu-id="7c451-140">Check hello on-premises VPN device external interface address</span></span>

- <span data-ttu-id="7c451-141">如果 hello hello VPN 裝置的網際網路對向的 IP 位址包含在 hello**區域網路**定義在 Azure 中，您可能會遇到偶發的連線中斷。</span><span class="sxs-lookup"><span data-stu-id="7c451-141">If hello Internet-facing IP address of hello VPN device is included in hello **Local network** definition in Azure, you might experience sporadic disconnections.</span></span>
- <span data-ttu-id="7c451-142">hello 裝置的外部介面必須直接在 hello 網際網路上。</span><span class="sxs-lookup"><span data-stu-id="7c451-142">hello device's external interface must be directly on hello Internet.</span></span> <span data-ttu-id="7c451-143">應該沒有網路位址轉譯 」 或 「 hello 網際網路與 hello 裝置之間的防火牆。</span><span class="sxs-lookup"><span data-stu-id="7c451-143">There should be no network address translation or firewall between hello Internet and hello device.</span></span>
- <span data-ttu-id="7c451-144">tooconfigure 防火牆群集 toohave 虛擬 IP，您必須中斷 hello 叢集，並公開 （expose） hello VPN 應用裝置直接 tooa 公用介面該 hello 閘道可與互動。</span><span class="sxs-lookup"><span data-stu-id="7c451-144">tooconfigure firewall clustering toohave a virtual IP, you must break hello cluster and expose hello VPN appliance directly tooa public interface that hello gateway can interface with.</span></span>

### <a name="step-6-verify-that-hello-subnets-match-exactly-azure-policy-based-gateways"></a><span data-ttu-id="7c451-145">步驟 6.</span><span class="sxs-lookup"><span data-stu-id="7c451-145">Step 6.</span></span> <span data-ttu-id="7c451-146">確認 hello 子網路完全相符 （Azure 以原則為基礎的閘道）</span><span class="sxs-lookup"><span data-stu-id="7c451-146">Verify that hello subnets match exactly (Azure policy-based gateways)</span></span>

-   <span data-ttu-id="7c451-147">確認 hello Azure 虛擬網路與內部定義 hello Azure 虛擬網路之間的完全符合 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="7c451-147">Verify that hello subnets match exactly between hello Azure virtual network and on-premises definitions for hello Azure virtual network.</span></span>
-   <span data-ttu-id="7c451-148">請確認 hello 子網路相符完全之間 hello**本機網路閘道**和內部部署的 hello 與內部網路定義。</span><span class="sxs-lookup"><span data-stu-id="7c451-148">Verify that hello subnets match exactly between hello **Local Network Gateway** and on-premises definitions for hello on-premises network.</span></span>

### <a name="step-7-verify-hello-azure-gateway-health-probe"></a><span data-ttu-id="7c451-149">步驟 7.</span><span class="sxs-lookup"><span data-stu-id="7c451-149">Step 7.</span></span> <span data-ttu-id="7c451-150">確認 hello Azure 閘道健全狀況探查</span><span class="sxs-lookup"><span data-stu-id="7c451-150">Verify hello Azure gateway health probe</span></span>

1. <span data-ttu-id="7c451-151">移 toohello[健全狀況探查](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe)。</span><span class="sxs-lookup"><span data-stu-id="7c451-151">Go toohello [health probe](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe).</span></span>

2. <span data-ttu-id="7c451-152">按一下瀏覽 hello 憑證警告。</span><span class="sxs-lookup"><span data-stu-id="7c451-152">Click through hello certificate warning.</span></span>
3. <span data-ttu-id="7c451-153">如果您收到的回應，hello VPN 閘道會被視為狀況良好。</span><span class="sxs-lookup"><span data-stu-id="7c451-153">If you receive a response, hello VPN gateway is considered healthy.</span></span> <span data-ttu-id="7c451-154">如果您沒有收到回應，hello 閘道可能不是狀況良好或 NSG hello 閘道子網路上的造成 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="7c451-154">If you don't receive a response, hello gateway might not be healthy or an NSG on hello gateway subnet is causing hello problem.</span></span> <span data-ttu-id="7c451-155">下列文字的 hello 是範例回應：</span><span class="sxs-lookup"><span data-stu-id="7c451-155">hello following text is a sample response:</span></span>

    <span data-ttu-id="7c451-156">&lt;?xml version="1.0"?> <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">主要執行個體: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span><span class="sxs-lookup"><span data-stu-id="7c451-156">&lt;?xml version="1.0"?>  <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">Primary Instance: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;</span></span>

### <a name="step-8-check-whether-hello-on-premises-vpn-device-has-hello-perfect-forward-secrecy-feature-enabled"></a><span data-ttu-id="7c451-157">步驟 8。</span><span class="sxs-lookup"><span data-stu-id="7c451-157">Step 8.</span></span> <span data-ttu-id="7c451-158">檢查是否 hello 內部部署 VPN 裝置已啟用的 hello 完整轉寄密碼功能</span><span class="sxs-lookup"><span data-stu-id="7c451-158">Check whether hello on-premises VPN device has hello perfect forward secrecy feature enabled</span></span>

<span data-ttu-id="7c451-159">hello 完整轉寄密碼功能可能會造成中斷連線問題。</span><span class="sxs-lookup"><span data-stu-id="7c451-159">hello perfect forward secrecy feature can cause disconnection problems.</span></span> <span data-ttu-id="7c451-160">Hello VPN 裝置已啟用完整轉寄密碼，如果停用 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="7c451-160">If hello VPN device has perfect forward secrecy enabled, disable hello feature.</span></span> <span data-ttu-id="7c451-161">然後更新 hello VPN 閘道 IPsec 原則。</span><span class="sxs-lookup"><span data-stu-id="7c451-161">Then update hello VPN gateway IPsec policy.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c451-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7c451-162">Next steps</span></span>

-   [<span data-ttu-id="7c451-163">設定站對站連線 tooa 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="7c451-163">Configure a site-to-site connection tooa virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [<span data-ttu-id="7c451-164">設定站對站 VPN 連線的 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="7c451-164">Configure an IPsec/IKE policy for site-to-site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)
