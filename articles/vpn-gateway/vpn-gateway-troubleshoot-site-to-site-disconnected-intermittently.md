---
title: "Azure 站台對站台 VPN 或間歇性中斷的 aaaTroubleshoot |Microsoft 文件"
description: "了解如何 tootroubleshoot hello 中斷定期的 hello 站對站 VPN 連接的問題。"
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
ms.openlocfilehash: 1ce3c4ff9d8f650312e45f33b760ebcc6597fc13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a><span data-ttu-id="6db1e-103">疑難排解：Azure 站對站 VPN 間歇性中斷</span><span class="sxs-lookup"><span data-stu-id="6db1e-103">Troubleshooting: Azure Site-to-Site VPN disconnects intermittently</span></span>

<span data-ttu-id="6db1e-104">您可能會遇到新的或現有的 Microsoft Azure 點對站 VPN 連線可能會不穩定或中斷定期的 hello 問題。</span><span class="sxs-lookup"><span data-stu-id="6db1e-104">You might experience hello problem that a new or existing Microsoft Azure Point-to-Site VPN connection is not stable or disconnects regularly.</span></span> <span data-ttu-id="6db1e-105">本文章提供疑難排解步驟 toohelp 您識別及解決 hello hello 問題原因。</span><span class="sxs-lookup"><span data-stu-id="6db1e-105">This article provides troubleshoot steps toohelp you identify and resolve hello cause of hello problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="6db1e-106">疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="6db1e-106">Troubleshooting steps</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="6db1e-107">必要步驟</span><span class="sxs-lookup"><span data-stu-id="6db1e-107">Prerequisite step</span></span>

<span data-ttu-id="6db1e-108">Azure 虛擬網路閘道的核取 hello 類型：</span><span class="sxs-lookup"><span data-stu-id="6db1e-108">Check hello type of Azure  virtual network gateway:</span></span>

1. <span data-ttu-id="6db1e-109">跳過[Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="6db1e-109">Go too[Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="6db1e-110">檢查 hello**概觀**hello hello 型別資訊的虛擬網路閘道的頁面。</span><span class="sxs-lookup"><span data-stu-id="6db1e-110">Check hello **Overview** page of hello virtual network gateway for hello type information.</span></span>
    
    ![hello 閘道的 hello 概觀](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a><span data-ttu-id="6db1e-112">步驟 1 檢查是否 hello 內部部署 VPN 裝置會進行驗證</span><span class="sxs-lookup"><span data-stu-id="6db1e-112">Step 1 Check whether hello on-premises VPN device is validated</span></span>

1. <span data-ttu-id="6db1e-113">檢查您是否使用[經過驗證的 VPN 裝置和作業系統版本](vpn-gateway-about-vpn-devices.md#devicetable)。</span><span class="sxs-lookup"><span data-stu-id="6db1e-113">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="6db1e-114">如果 hello VPN 裝置未經過驗證，您可能需要 toocontact hello 裝置製造商 toosee，如果有任何相容性問題。</span><span class="sxs-lookup"><span data-stu-id="6db1e-114">If hello VPN device is not validated, you may have toocontact hello device manufacturer toosee if there is any compatibility issue.</span></span>
2. <span data-ttu-id="6db1e-115">請確定已正確設定該 hello VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="6db1e-115">Make sure that hello VPN device is correctly configured.</span></span> <span data-ttu-id="6db1e-116">如需詳細資訊，請參閱[編輯裝置組態範例](vpn-gateway-about-vpn-devices.md#editing)。</span><span class="sxs-lookup"><span data-stu-id="6db1e-116">For more information, see [Editing device configuration samples](vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-check-hello-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a><span data-ttu-id="6db1e-117">步驟 2 檢查 hello （適用於以原則為基礎的 Azure 虛擬網路閘道） 的安全性關聯設定</span><span class="sxs-lookup"><span data-stu-id="6db1e-117">Step 2 Check hello Security Association settings(for policy-based Azure virtual network gateways)</span></span>

1. <span data-ttu-id="6db1e-118">請確定該 hello 虛擬網路，子網路和範圍中 hello**區域網路閘道**Microsoft Azure 中的定義會與 hello hello 在內部部署 VPN 裝置上的設定相同。</span><span class="sxs-lookup"><span data-stu-id="6db1e-118">Make sure that hello virtual network, subnets and, ranges in hello **Local network gateway** definition in Microsoft Azure are same as hello configuration on hello on-premises VPN device.</span></span>
2. <span data-ttu-id="6db1e-119">請確認該 hello 安全性關聯的設定相符。</span><span class="sxs-lookup"><span data-stu-id="6db1e-119">Verify that hello Security Association settings match.</span></span>

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a><span data-ttu-id="6db1e-120">步驟 3：檢查閘道子網路上使用者定義的路由或網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="6db1e-120">Step 3 Check for User-Defined Routes or Network Security Groups on Gateway Subnet</span></span>

<span data-ttu-id="6db1e-121">Hello 閘道子網路的使用者定義路由可能會限制一些流量，並允許其他流量。</span><span class="sxs-lookup"><span data-stu-id="6db1e-121">A user-defined route on hello gateway subnet may be restricting some traffic and allowing other traffic.</span></span> <span data-ttu-id="6db1e-122">這使得出現 hello VPN 連線的一些流量不可靠且適用於其他人。</span><span class="sxs-lookup"><span data-stu-id="6db1e-122">This makes it appear that hello VPN connection is unreliable for some traffic and good for others.</span></span> 

### <a name="step-4-check-hello-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="6db1e-123">步驟 4 核取 hello"一個 VPN 通道每組子網路 」 設定 （適用於以原則為基礎的虛擬網路閘道）</span><span class="sxs-lookup"><span data-stu-id="6db1e-123">Step 4 Check hello "one VPN Tunnel per Subnet Pair" setting (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="6db1e-124">請確定該 hello 內部部署 VPN 裝置設定 toohave**一個每組子網路的 VPN 通道**以原則為基礎的虛擬網路閘道。</span><span class="sxs-lookup"><span data-stu-id="6db1e-124">Make sure that hello on-premises VPN device is set toohave **one VPN tunnel per subnet pair** for policy-based virtual network gateways.</span></span>

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="6db1e-125">步驟 5：檢查安全性關聯限制 (適用於原則式虛擬網路閘道)</span><span class="sxs-lookup"><span data-stu-id="6db1e-125">Step 5 Check for Security Association Limitation (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="6db1e-126">hello 以原則為基礎的虛擬網路閘道的上限為 200 的子網路的安全性關聯組。</span><span class="sxs-lookup"><span data-stu-id="6db1e-126">hello Policy-based virtual network gateway has limit of 200 subnet Security Association pairs.</span></span> <span data-ttu-id="6db1e-127">如果 Azure 虛擬網路子網路的 hello 數目乘以時間 hello 的本機子網路的數字會大於 200，您會看到偶爾中斷連線的子網路。</span><span class="sxs-lookup"><span data-stu-id="6db1e-127">If hello number of Azure virtual network subnets multiplied times by hello number of local subnets is greater than 200, you see sporadic subnets disconnecting.</span></span>

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="6db1e-128">步驟 6：檢查內部部署 VPN 裝置外部介面位址</span><span class="sxs-lookup"><span data-stu-id="6db1e-128">Step 6 Check on-premises VPN device external interface address</span></span>

- <span data-ttu-id="6db1e-129">如果 hello 網際網路對向 hello VPN 裝置 IP 位址會包含在 hello**區域網路閘道**定義在 Azure 中，您可能會遇到偶發的連線中斷。</span><span class="sxs-lookup"><span data-stu-id="6db1e-129">If hello Internet facing IP address of hello VPN device is included in hello **Local network gateway** definition in Azure, you may experience sporadic disconnections.</span></span>
- <span data-ttu-id="6db1e-130">hello 裝置的外部介面必須直接在 hello 網際網路上。</span><span class="sxs-lookup"><span data-stu-id="6db1e-130">hello device's external interface must be directly on hello Internet.</span></span> <span data-ttu-id="6db1e-131">應該沒有網路位址轉譯 (NAT) 或網際網路 hello 與 hello 裝置之間的防火牆。</span><span class="sxs-lookup"><span data-stu-id="6db1e-131">There should be no Network Address Translation (NAT) or firewall between hello Internet and hello device.</span></span>
-  <span data-ttu-id="6db1e-132">如果您設定防火牆叢集 toohave 虛擬 IP，您必須中斷 hello 叢集，而且可與互動 tooa hello 閘道的公用介面直接公開 hello VPN 應用裝置。</span><span class="sxs-lookup"><span data-stu-id="6db1e-132">If you configure Firewall Clustering toohave a virtual IP, you must break hello cluster and expose hello VPN appliance directly tooa public interface that hello gateway can interface with.</span></span>

### <a name="step-7-check-whether-hello-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a><span data-ttu-id="6db1e-133">步驟 7 的核取是否 hello 內部部署 VPN 裝置有完整轉寄密碼啟用</span><span class="sxs-lookup"><span data-stu-id="6db1e-133">Step 7 Check whether hello on-premises VPN device has Perfect Forward Secrecy enabled</span></span>

<span data-ttu-id="6db1e-134">hello**完整轉寄密碼**功能造成 hello 中斷連線的問題。</span><span class="sxs-lookup"><span data-stu-id="6db1e-134">hello **Perfect Forward Secrecy** feature can cause hello disconnection problems.</span></span> <span data-ttu-id="6db1e-135">如果 hello VPN 裝置有**完整轉寄密碼**啟用、 停用 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="6db1e-135">If hello VPN device has **Perfect forward Secrecy** enabled, disable hello feature.</span></span> <span data-ttu-id="6db1e-136">然後[更新 hello 虛擬網路閘道 IPsec 原則](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy)。</span><span class="sxs-lookup"><span data-stu-id="6db1e-136">Then [update hello virtual network gateway IPsec policy](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6db1e-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6db1e-137">Next steps</span></span>

- [<span data-ttu-id="6db1e-138">設定站對站連線 tooa 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="6db1e-138">Configure a Site-to-Site connection tooa virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [<span data-ttu-id="6db1e-139">設定站對站 VPN 連線的 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="6db1e-139">Configure IPsec/IKE policy for Site-to-Site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)

