---
title: "針對 Azure 站對站 VPN 間歇性中斷問題進行疑難排解| Microsoft Docs"
description: "了解如何針對 Azure 站對站 VPN 連線間歇性中斷問題進行疑難排解。"
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
ms.openlocfilehash: 99a790617baa65116bfba976cd9279627e8775f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a><span data-ttu-id="fbbe3-103">疑難排解：Azure 站對站 VPN 間歇性中斷</span><span class="sxs-lookup"><span data-stu-id="fbbe3-103">Troubleshooting: Azure Site-to-Site VPN disconnects intermittently</span></span>

<span data-ttu-id="fbbe3-104">您可能會遇到新的或現有的 Microsoft Azure 站對站 VPN 連線不穩定或間歇地中斷。</span><span class="sxs-lookup"><span data-stu-id="fbbe3-104">You might experience the problem that a new or existing Microsoft Azure Point-to-Site VPN connection is not stable or disconnects regularly.</span></span> <span data-ttu-id="fbbe3-105">本文提供疑難排解步驟，可協助您找出原因並解決問題。</span><span class="sxs-lookup"><span data-stu-id="fbbe3-105">This article provides troubleshoot steps to help you identify and resolve the cause of the problem.</span></span> 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a><span data-ttu-id="fbbe3-106">疑難排解步驟</span><span class="sxs-lookup"><span data-stu-id="fbbe3-106">Troubleshooting steps</span></span>

### <a name="prerequisite-step"></a><span data-ttu-id="fbbe3-107">必要步驟</span><span class="sxs-lookup"><span data-stu-id="fbbe3-107">Prerequisite step</span></span>

<span data-ttu-id="fbbe3-108">檢查 Azure 虛擬網路閘道的類型：</span><span class="sxs-lookup"><span data-stu-id="fbbe3-108">Check the type of Azure  virtual network gateway:</span></span>

1. <span data-ttu-id="fbbe3-109">移至 [Azure 入口網站 ](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="fbbe3-109">Go to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="fbbe3-110">檢查虛擬網路閘道的 [概觀] 頁面來取得類型資訊。</span><span class="sxs-lookup"><span data-stu-id="fbbe3-110">Check the **Overview** page of the virtual network gateway for the type information.</span></span>
    
    ![閘道概觀](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-the-on-premises-vpn-device-is-validated"></a><span data-ttu-id="fbbe3-112">步驟 1：檢查內部部署 VPN 裝置是否經過驗證</span><span class="sxs-lookup"><span data-stu-id="fbbe3-112">Step 1 Check whether the on-premises VPN device is validated</span></span>

1. <span data-ttu-id="fbbe3-113">檢查您是否使用[經過驗證的 VPN 裝置和作業系統版本](vpn-gateway-about-vpn-devices.md#devicetable)。</span><span class="sxs-lookup"><span data-stu-id="fbbe3-113">Check whether you are using a [validated VPN device and operating system version](vpn-gateway-about-vpn-devices.md#devicetable).</span></span> <span data-ttu-id="fbbe3-114">如果 VPN 裝置未經驗證，您可能需要連絡裝置製造商，以了解是否有任何相容性問題。</span><span class="sxs-lookup"><span data-stu-id="fbbe3-114">If the VPN device is not validated, you may have to contact the device manufacturer to see if there is any compatibility issue.</span></span>
2. <span data-ttu-id="fbbe3-115">確定已正確設定 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="fbbe3-115">Make sure that the VPN device is correctly configured.</span></span> <span data-ttu-id="fbbe3-116">如需詳細資訊，請參閱[編輯裝置組態範例](vpn-gateway-about-vpn-devices.md#editing)。</span><span class="sxs-lookup"><span data-stu-id="fbbe3-116">For more information, see [Editing device configuration samples](vpn-gateway-about-vpn-devices.md#editing).</span></span>

### <a name="step-2-check-the-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a><span data-ttu-id="fbbe3-117">步驟 2：檢查安全性關聯設定 (適用於原則式 Azure 虛擬網路閘道)</span><span class="sxs-lookup"><span data-stu-id="fbbe3-117">Step 2 Check the Security Association settings(for policy-based Azure virtual network gateways)</span></span>

1. <span data-ttu-id="fbbe3-118">確定 Microsoft Azure 中的「區域網路閘道」定義中的虛擬網路、子網路和範圍皆與內部部署 VPN 裝置上的設定相同。</span><span class="sxs-lookup"><span data-stu-id="fbbe3-118">Make sure that the virtual network, subnets and, ranges in the **Local network gateway** definition in Microsoft Azure are same as the configuration on the on-premises VPN device.</span></span>
2. <span data-ttu-id="fbbe3-119">確認安全性關聯設定相符合。</span><span class="sxs-lookup"><span data-stu-id="fbbe3-119">Verify that the Security Association settings match.</span></span>

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a><span data-ttu-id="fbbe3-120">步驟 3：檢查閘道子網路上使用者定義的路由或網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="fbbe3-120">Step 3 Check for User-Defined Routes or Network Security Groups on Gateway Subnet</span></span>

<span data-ttu-id="fbbe3-121">閘道子網路上的使用者定義路由可能會限制某些流量並允許其他流量。</span><span class="sxs-lookup"><span data-stu-id="fbbe3-121">A user-defined route on the gateway subnet may be restricting some traffic and allowing other traffic.</span></span> <span data-ttu-id="fbbe3-122">這可能會讓某些流量認為 VPN 連線不穩定，而其他流量覺得它穩定。</span><span class="sxs-lookup"><span data-stu-id="fbbe3-122">This makes it appear that the VPN connection is unreliable for some traffic and good for others.</span></span> 

### <a name="step-4-check-the-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="fbbe3-123">步驟 4：檢查「每個子網路配一個 VPN 通道」設定 (適用於原則式虛擬網路閘道)</span><span class="sxs-lookup"><span data-stu-id="fbbe3-123">Step 4 Check the "one VPN Tunnel per Subnet Pair" setting (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="fbbe3-124">確定已針對原則式虛擬網路閘道將內部部署 VPN 裝置設定為「每個子網路配一個 VPN 通道」。</span><span class="sxs-lookup"><span data-stu-id="fbbe3-124">Make sure that the on-premises VPN device is set to have **one VPN tunnel per subnet pair** for policy-based virtual network gateways.</span></span>

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a><span data-ttu-id="fbbe3-125">步驟 5：檢查安全性關聯限制 (適用於原則式虛擬網路閘道)</span><span class="sxs-lookup"><span data-stu-id="fbbe3-125">Step 5 Check for Security Association Limitation (for policy-based virtual network gateways)</span></span>

<span data-ttu-id="fbbe3-126">原則式虛擬網路閘道有 200 個子網路安全性關聯組的限制。</span><span class="sxs-lookup"><span data-stu-id="fbbe3-126">The Policy-based virtual network gateway has limit of 200 subnet Security Association pairs.</span></span> <span data-ttu-id="fbbe3-127">如果 Azure 虛擬網路子網路數目乘以區域子網路數目的結果大於 200，則您會遇到子網路偶爾連線中斷的情況。</span><span class="sxs-lookup"><span data-stu-id="fbbe3-127">If the number of Azure virtual network subnets multiplied times by the number of local subnets is greater than 200, you see sporadic subnets disconnecting.</span></span>

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a><span data-ttu-id="fbbe3-128">步驟 6：檢查內部部署 VPN 裝置外部介面位址</span><span class="sxs-lookup"><span data-stu-id="fbbe3-128">Step 6 Check on-premises VPN device external interface address</span></span>

- <span data-ttu-id="fbbe3-129">如果 Azure 的「區域網路閘道」定義中包含 VPN 裝置對網際網路的 IP 位址，則您可能會遇到偶爾連線中斷的情況。</span><span class="sxs-lookup"><span data-stu-id="fbbe3-129">If the Internet facing IP address of the VPN device is included in the **Local network gateway** definition in Azure, you may experience sporadic disconnections.</span></span>
- <span data-ttu-id="fbbe3-130">裝置的外部介面必須直接位在網際網路上。</span><span class="sxs-lookup"><span data-stu-id="fbbe3-130">The device's external interface must be directly on the Internet.</span></span> <span data-ttu-id="fbbe3-131">網際網路與裝置之間不應該有網路位址轉譯 (NAT) 或防火牆。</span><span class="sxs-lookup"><span data-stu-id="fbbe3-131">There should be no Network Address Translation (NAT) or firewall between the Internet and the device.</span></span>
-  <span data-ttu-id="fbbe3-132">如果您將防火牆叢集設定為具有虛擬 IP，則您必須解散叢集，並直接將 VPN 設備公開給閘道可介接的公用介面。</span><span class="sxs-lookup"><span data-stu-id="fbbe3-132">If you configure Firewall Clustering to have a virtual IP, you must break the cluster and expose the VPN appliance directly to a public interface that the gateway can interface with.</span></span>

### <a name="step-7-check-whether-the-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a><span data-ttu-id="fbbe3-133">步驟 7：檢查內部部署 VPN 裝置是否已啟用「完整轉寄密碼」</span><span class="sxs-lookup"><span data-stu-id="fbbe3-133">Step 7 Check whether the on-premises VPN device has Perfect Forward Secrecy enabled</span></span>

<span data-ttu-id="fbbe3-134">「完整轉寄密碼」功能可能會造成連線中斷的問題。</span><span class="sxs-lookup"><span data-stu-id="fbbe3-134">The **Perfect Forward Secrecy** feature can cause the disconnection problems.</span></span> <span data-ttu-id="fbbe3-135">如果 VPN 裝置已啟用「完整轉寄密碼」，請停用該功能。</span><span class="sxs-lookup"><span data-stu-id="fbbe3-135">If the VPN device has **Perfect forward Secrecy** enabled, disable the feature.</span></span> <span data-ttu-id="fbbe3-136">然後[更新虛擬網路閘道 IPsec 原則](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy)。</span><span class="sxs-lookup"><span data-stu-id="fbbe3-136">Then [update the virtual network gateway IPsec policy](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fbbe3-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fbbe3-137">Next steps</span></span>

- [<span data-ttu-id="fbbe3-138">設定對虛擬網路的站對站連線</span><span class="sxs-lookup"><span data-stu-id="fbbe3-138">Configure a Site-to-Site connection to a virtual network</span></span>](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [<span data-ttu-id="fbbe3-139">設定站對站 VPN 連線的 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="fbbe3-139">Configure IPsec/IKE policy for Site-to-Site VPN connections</span></span>](vpn-gateway-ipsecikepolicy-rm-powershell.md)

