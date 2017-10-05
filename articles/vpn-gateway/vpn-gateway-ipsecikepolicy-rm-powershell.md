---
title: "設定 S2S VPN 或 VNet 對 VNet 連線的 IPsec/IKE 原則：Azure Resource Manager：PowerShell | Microsoft Docs"
description: "本文將引導您使用 Azure Resource Manager 和 PowerShell，設定與 Azure VPN 閘道之 S2S 或 VNet 對 VNet 連線的 IPsec/IKE 原則。"
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: yushwang
ms.openlocfilehash: 798014b6e8d4495db99ef2e2d2ea487ae7d02fd0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="configure-ipsecike-policy-for-s2s-vpn-or-vnet-to-vnet-connections"></a><span data-ttu-id="12aa6-103">設定 S2S VPN 或 VNet 對 VNet 連線的 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="12aa6-103">Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections</span></span>

<span data-ttu-id="12aa6-104">本文將逐步引導您使用 Resource Manager 部署模型和 PowerShell，設定站對站 VPN 或 VNet 對 VNet 連線的 IPsec/IKE 原則。</span><span class="sxs-lookup"><span data-stu-id="12aa6-104">This article walks you through the steps to configure IPsec/IKE policy for Site-to-Site VPN or VNet-to-VNet connections using the Resource Manager deployment model and PowerShell.</span></span>

## <span data-ttu-id="12aa6-105"><a name="about"></a>關於 Azure VPN 閘道的 IPsec 和 IKE 原則參數</span><span class="sxs-lookup"><span data-stu-id="12aa6-105"><a name="about"></a>About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="12aa6-106">IPsec 和 IKE 通訊協定標準支援各種不同的密碼編譯演算法的各種組合。</span><span class="sxs-lookup"><span data-stu-id="12aa6-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="12aa6-107">請參閱[關於密碼編譯需求和 Azure VPN 閘道](vpn-gateway-about-compliance-crypto.md)，以查看這如何協助確保跨單位和 VNet 對 VNet 連線滿足合規性或安全性需求。</span><span class="sxs-lookup"><span data-stu-id="12aa6-107">Refer to [About cryptographic requirements and Azure VPN gateways](vpn-gateway-about-compliance-crypto.md) to see how this can help ensuring cross-premises and VNet-to-VNet connectivity satisfy your compliance or security requirements.</span></span>

<span data-ttu-id="12aa6-108">本文提供指示來建立和設定 IPsec/IKE 原則並套用至新的或現有連線：</span><span class="sxs-lookup"><span data-stu-id="12aa6-108">This article provides instructions to create and configure an IPsec/IKE policy and apply to a new or existing connection:</span></span>

* [<span data-ttu-id="12aa6-109">第 1 部分 - 建立和設定 IPsec/IKE 原則的工作流程</span><span class="sxs-lookup"><span data-stu-id="12aa6-109">Part 1 - Workflow to create and set IPsec/IKE policy</span></span>](#workflow)
* [<span data-ttu-id="12aa6-110">第 2 部分 - 支援的密碼編譯演算法和金鑰長度</span><span class="sxs-lookup"><span data-stu-id="12aa6-110">Part 2 - Supported cryptographic algorithms and key strengths</span></span>](#params)
* [<span data-ttu-id="12aa6-111">第 3 部分 - 使用 IPsec/IKE 原則建立新的 S2S VPN 連線</span><span class="sxs-lookup"><span data-stu-id="12aa6-111">Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>](#crossprem)
* [<span data-ttu-id="12aa6-112">第 4 部分 - 使用 IPsec/IKE 原則建立新的 VNet 對 VNet 連線</span><span class="sxs-lookup"><span data-stu-id="12aa6-112">Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>](#vnet2vnet)
* [<span data-ttu-id="12aa6-113">第 5 部分 - 管理 (建立、新增、移除) 連線的 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="12aa6-113">Part 5 - Manage (create, add, remove) IPsec/IKE policy for a connection</span></span>](#managepolicy)

> [!IMPORTANT]
> 1. <span data-ttu-id="12aa6-114">請注意，IPsec/IKE 原則僅適用於下列閘道 SKU：</span><span class="sxs-lookup"><span data-stu-id="12aa6-114">Note that IPsec/IKE policy only works on the following gateway SKUs:</span></span>
>    * <span data-ttu-id="12aa6-115">***VpnGw1、VpnGw2、VpnGw3*** (路由式)</span><span class="sxs-lookup"><span data-stu-id="12aa6-115">***VpnGw1, VpnGw2, VpnGw3*** (route-based)</span></span>
>    * <span data-ttu-id="12aa6-116">***Standard*** 和 ***HighPerformance*** (路由式)</span><span class="sxs-lookup"><span data-stu-id="12aa6-116">***Standard*** and ***HighPerformance*** (route-based)</span></span>
> 2. <span data-ttu-id="12aa6-117">每個給定的連線只能指定***一個***原則組合。</span><span class="sxs-lookup"><span data-stu-id="12aa6-117">You can only specify ***one*** policy combination for a given connection.</span></span>
> 3. <span data-ttu-id="12aa6-118">您必須同時對 IKE (主要模式) 和 IPsec (快速模式) 指定所有的演算法和參數。</span><span class="sxs-lookup"><span data-stu-id="12aa6-118">You must specify all algorithms and parameters for both IKE (Main Mode) and IPsec (Quick Mode).</span></span> <span data-ttu-id="12aa6-119">系統不允許只指定一部分原則。</span><span class="sxs-lookup"><span data-stu-id="12aa6-119">Partial policy specification is not allowed.</span></span>
> 4. <span data-ttu-id="12aa6-120">請確認 VPN 裝置廠商規格，確保內部部署 VPN 裝置支援原則。</span><span class="sxs-lookup"><span data-stu-id="12aa6-120">Consult with your VPN device vendor specifications to ensure the policy is supported on your on-premises VPN devices.</span></span> <span data-ttu-id="12aa6-121">如果原則不相容，則無法建立 S2S 或 VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="12aa6-121">S2S or VNet-to-VNet connections cannot establish if the policies are incompatible.</span></span>

## <span data-ttu-id="12aa6-122"><a name ="workflow"></a>第 1 部分 - 建立和設定 IPsec/IKE 原則的工作流程</span><span class="sxs-lookup"><span data-stu-id="12aa6-122"><a name ="workflow"></a>Part 1 - Workflow to create and set IPsec/IKE policy</span></span>
<span data-ttu-id="12aa6-123">本節所概述的工作流程可在 S2S VPN 或 VNet 對 VNet 連線上建立和更新 IPsec/IKE 原則：</span><span class="sxs-lookup"><span data-stu-id="12aa6-123">This section outlines the workflow to create and update IPsec/IKE policy on a S2S VPN or VNet-to-VNet connection:</span></span>
1. <span data-ttu-id="12aa6-124">建立虛擬網路和 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="12aa6-124">Create a virtual network and a VPN gateway</span></span>
2. <span data-ttu-id="12aa6-125">建立區域網路閘道以進行跨單位連線，或建立另一個虛擬網路和閘道以進行 VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="12aa6-125">Create a local network gateway for cross premises connection, or another virtual network and gateway for VNet-to-VNet connection</span></span>
3. <span data-ttu-id="12aa6-126">使用選取的演算法和參數建立 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="12aa6-126">Create an IPsec/IKE policy with selected algorithms and parameters</span></span>
4. <span data-ttu-id="12aa6-127">使用 IPsec/IKE 原則建立連線 (IPsec 或 VNet2VNet)</span><span class="sxs-lookup"><span data-stu-id="12aa6-127">Create a connection (IPsec or VNet2VNet) with the IPsec/IKE policy</span></span>
5. <span data-ttu-id="12aa6-128">新增/更新/移除現有連線的 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="12aa6-128">Add/update/remove an IPsec/IKE policy for an existing connection</span></span>

<span data-ttu-id="12aa6-129">本文中的指示將會協助您安裝並設定 IPsec/IKE 原則，如圖所示：</span><span class="sxs-lookup"><span data-stu-id="12aa6-129">The instructions in this article helps you set up and configure IPsec/IKE policies as shown in the diagram:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)

## <span data-ttu-id="12aa6-131"><a name ="params"></a>第 2 部分 - 支援的密碼編譯演算法和金鑰長度</span><span class="sxs-lookup"><span data-stu-id="12aa6-131"><a name ="params"></a>Part 2 - Supported cryptographic algorithms & key strengths</span></span>

<span data-ttu-id="12aa6-132">下表列出可供客戶設定的支援密碼編譯演算法和金鑰強度：</span><span class="sxs-lookup"><span data-stu-id="12aa6-132">The following table lists the supported cryptographic algorithms and key strengths configurable by the customers:</span></span>

| <span data-ttu-id="12aa6-133">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="12aa6-133">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="12aa6-134">**選項**</span><span class="sxs-lookup"><span data-stu-id="12aa6-134">**Options**</span></span>    |
| ---  | --- 
| <span data-ttu-id="12aa6-135">IKEv2 加密</span><span class="sxs-lookup"><span data-stu-id="12aa6-135">IKEv2 Encryption</span></span> | <span data-ttu-id="12aa6-136">AES256、AES192、AES128、DES3、DES</span><span class="sxs-lookup"><span data-stu-id="12aa6-136">AES256, AES192, AES128, DES3, DES</span></span>  
| <span data-ttu-id="12aa6-137">IKEv2 完整性</span><span class="sxs-lookup"><span data-stu-id="12aa6-137">IKEv2 Integrity</span></span>  | <span data-ttu-id="12aa6-138">SHA384、SHA256、SHA1、MD5</span><span class="sxs-lookup"><span data-stu-id="12aa6-138">SHA384, SHA256, SHA1, MD5</span></span>  |
| <span data-ttu-id="12aa6-139">DH 群組</span><span class="sxs-lookup"><span data-stu-id="12aa6-139">DH Group</span></span>         | <span data-ttu-id="12aa6-140">DHGroup24、ECP384、ECP256、DHGroup14、DHGroup2048、DHGroup2、DHGroup1、無</span><span class="sxs-lookup"><span data-stu-id="12aa6-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, None</span></span> |
| <span data-ttu-id="12aa6-141">IPsec 加密</span><span class="sxs-lookup"><span data-stu-id="12aa6-141">IPsec Encryption</span></span> | <span data-ttu-id="12aa6-142">GCMAES256、GCMAES192、GCMAES128、AES256、AES192、AES128、DES3、DES、無</span><span class="sxs-lookup"><span data-stu-id="12aa6-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, None</span></span>    |
| <span data-ttu-id="12aa6-143">IPsec 完整性</span><span class="sxs-lookup"><span data-stu-id="12aa6-143">IPsec Integrity</span></span>  | <span data-ttu-id="12aa6-144">GCMASE256、GCMAES192、GCMAES128、SHA256、SHA1、MD5</span><span class="sxs-lookup"><span data-stu-id="12aa6-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span></span> |
| <span data-ttu-id="12aa6-145">PFS 群組</span><span class="sxs-lookup"><span data-stu-id="12aa6-145">PFS Group</span></span>        | <span data-ttu-id="12aa6-146">PFS24、ECP384、ECP256、PFS2048、PFS2、PFS1、無</span><span class="sxs-lookup"><span data-stu-id="12aa6-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, None</span></span> 
| <span data-ttu-id="12aa6-147">QM SA 存留期</span><span class="sxs-lookup"><span data-stu-id="12aa6-147">QM SA Lifetime</span></span>   | <span data-ttu-id="12aa6-148">(**選擇性**：如果未指定，即會使用預設值)</span><span class="sxs-lookup"><span data-stu-id="12aa6-148">(**Optional**: default values are used if not specified)</span></span><br><span data-ttu-id="12aa6-149">秒 (整數；**最小 300**/預設值 27000 秒)</span><span class="sxs-lookup"><span data-stu-id="12aa6-149">Seconds (integer; **min. 300**/default 27000 seconds)</span></span><br><span data-ttu-id="12aa6-150">KB 數 (整數；**最小 1024**/預設值 102400000 KB 數)</span><span class="sxs-lookup"><span data-stu-id="12aa6-150">KBytes (integer; **min. 1024**/default 102400000 KBytes)</span></span>   |
| <span data-ttu-id="12aa6-151">流量選取器</span><span class="sxs-lookup"><span data-stu-id="12aa6-151">Traffic Selector</span></span> | <span data-ttu-id="12aa6-152">UsePolicyBasedTrafficSelectors** ($True/$False；**選擇性**，如果未指定，即為預設的 $False)</span><span class="sxs-lookup"><span data-stu-id="12aa6-152">UsePolicyBasedTrafficSelectors** ($True/$False; **Optional**, default $False if not specified)</span></span>    |
|  |  |

> [!IMPORTANT]
> 1. <span data-ttu-id="12aa6-153">**如果 GCMAES 會用於 IPsec 加密演算法，您必須基於 IPsec 完整性選取相同的 GCMAES 演算法和金鑰長度；例如，針對這兩者使用 GCMAES128**</span><span class="sxs-lookup"><span data-stu-id="12aa6-153">**If GCMAES is used as for IPsec Encryption algorithm, you must select the same GCMAES algorithm and key length for IPsec Integrity; for example, using GCMAES128 for both**</span></span>
> 2. <span data-ttu-id="12aa6-154">Azure VPN 閘道的 IKEv2 主要模式 SA 存留期會固定為 28,800 秒</span><span class="sxs-lookup"><span data-stu-id="12aa6-154">IKEv2 Main Mode SA lifetime is fixed at 28,800 seconds on the Azure VPN gateways</span></span>
> 3. <span data-ttu-id="12aa6-155">在連線上將 "UsePolicyBasedTrafficSelectors" 設定為 $True，將設定 Azure VPN 閘道連線至內部部署的原則式 VPN 防火牆。</span><span class="sxs-lookup"><span data-stu-id="12aa6-155">Setting "UsePolicyBasedTrafficSelectors" to $True on a connection will configure the Azure VPN gateway to connect to policy-based VPN firewall on premises.</span></span> <span data-ttu-id="12aa6-156">如果您啟用 PolicyBasedTrafficSelectors，則必須確定 VPN 裝置的流量選取器已定義內部部署網路 (區域網路閘道) 前置詞往/返 Azure 虛擬網路前置詞的所有組合，而不是任意對任意的組合。</span><span class="sxs-lookup"><span data-stu-id="12aa6-156">If you enable PolicyBasedTrafficSelectors, you need to ensure your VPN device has the matching traffic selectors defined with all combinations of your on-premises network (local network gateway) prefixes to/from the Azure virtual network prefixes, instead of any-to-any.</span></span> <span data-ttu-id="12aa6-157">例如，如果內部部署網路的前置詞為 10.1.0.0/16 和 10.2.0.0/16，而虛擬網路的前置詞為 192.168.0.0/16 和 172.16.0.0/16，則需要指定下列流量選取器︰</span><span class="sxs-lookup"><span data-stu-id="12aa6-157">For example, if your on-premises network prefixes are 10.1.0.0/16 and 10.2.0.0/16, and your virtual network prefixes are 192.168.0.0/16 and 172.16.0.0/16, you need to specify the following traffic selectors:</span></span>
>    * <span data-ttu-id="12aa6-158">10.1.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="12aa6-158">10.1.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="12aa6-159">10.1.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="12aa6-159">10.1.0.0/16 <====> 172.16.0.0/16</span></span>
>    * <span data-ttu-id="12aa6-160">10.2.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="12aa6-160">10.2.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="12aa6-161">10.2.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="12aa6-161">10.2.0.0/16 <====> 172.16.0.0/16</span></span>

<span data-ttu-id="12aa6-162">如需原則式流量選取器的詳細資訊，請參閱[連線多個內部部署原則式 VPN 裝置](vpn-gateway-connect-multiple-policybased-rm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="12aa6-162">For more information regarding policy-based traffic selectors, see [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

<span data-ttu-id="12aa6-163">下表列出自訂原則所支援的對應 Diffie-Hellman 群組：</span><span class="sxs-lookup"><span data-stu-id="12aa6-163">The following table lists the corresponding Diffie-Hellman Groups supported by the custom policy:</span></span>

| <span data-ttu-id="12aa6-164">**Diffie-Hellman 群組**</span><span class="sxs-lookup"><span data-stu-id="12aa6-164">**Diffie-Hellman Group**</span></span>  | <span data-ttu-id="12aa6-165">**DHGroup**</span><span class="sxs-lookup"><span data-stu-id="12aa6-165">**DHGroup**</span></span>              | <span data-ttu-id="12aa6-166">**PFSGroup**</span><span class="sxs-lookup"><span data-stu-id="12aa6-166">**PFSGroup**</span></span> | <span data-ttu-id="12aa6-167">**金鑰長度**</span><span class="sxs-lookup"><span data-stu-id="12aa6-167">**Key length**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="12aa6-168">1</span><span class="sxs-lookup"><span data-stu-id="12aa6-168">1</span></span>                         | <span data-ttu-id="12aa6-169">DHGroup1</span><span class="sxs-lookup"><span data-stu-id="12aa6-169">DHGroup1</span></span>                 | <span data-ttu-id="12aa6-170">PFS1</span><span class="sxs-lookup"><span data-stu-id="12aa6-170">PFS1</span></span>         | <span data-ttu-id="12aa6-171">768 位元 MODP</span><span class="sxs-lookup"><span data-stu-id="12aa6-171">768-bit MODP</span></span>   |
| <span data-ttu-id="12aa6-172">2</span><span class="sxs-lookup"><span data-stu-id="12aa6-172">2</span></span>                         | <span data-ttu-id="12aa6-173">DHGroup2</span><span class="sxs-lookup"><span data-stu-id="12aa6-173">DHGroup2</span></span>                 | <span data-ttu-id="12aa6-174">PFS2</span><span class="sxs-lookup"><span data-stu-id="12aa6-174">PFS2</span></span>         | <span data-ttu-id="12aa6-175">1024 位元 MODP</span><span class="sxs-lookup"><span data-stu-id="12aa6-175">1024-bit MODP</span></span>  |
| <span data-ttu-id="12aa6-176">14</span><span class="sxs-lookup"><span data-stu-id="12aa6-176">14</span></span>                        | <span data-ttu-id="12aa6-177">DHGroup14</span><span class="sxs-lookup"><span data-stu-id="12aa6-177">DHGroup14</span></span><br><span data-ttu-id="12aa6-178">DHGroup2048</span><span class="sxs-lookup"><span data-stu-id="12aa6-178">DHGroup2048</span></span> | <span data-ttu-id="12aa6-179">PFS2048</span><span class="sxs-lookup"><span data-stu-id="12aa6-179">PFS2048</span></span>      | <span data-ttu-id="12aa6-180">2048 位元 MODP</span><span class="sxs-lookup"><span data-stu-id="12aa6-180">2048-bit MODP</span></span>  |
| <span data-ttu-id="12aa6-181">19</span><span class="sxs-lookup"><span data-stu-id="12aa6-181">19</span></span>                        | <span data-ttu-id="12aa6-182">ECP256</span><span class="sxs-lookup"><span data-stu-id="12aa6-182">ECP256</span></span>                   | <span data-ttu-id="12aa6-183">ECP256</span><span class="sxs-lookup"><span data-stu-id="12aa6-183">ECP256</span></span>       | <span data-ttu-id="12aa6-184">256 位元 ECP</span><span class="sxs-lookup"><span data-stu-id="12aa6-184">256-bit ECP</span></span>    |
| <span data-ttu-id="12aa6-185">20</span><span class="sxs-lookup"><span data-stu-id="12aa6-185">20</span></span>                        | <span data-ttu-id="12aa6-186">ECP384</span><span class="sxs-lookup"><span data-stu-id="12aa6-186">ECP384</span></span>                   | <span data-ttu-id="12aa6-187">ECP284</span><span class="sxs-lookup"><span data-stu-id="12aa6-187">ECP284</span></span>       | <span data-ttu-id="12aa6-188">384 位元 ECP</span><span class="sxs-lookup"><span data-stu-id="12aa6-188">384-bit ECP</span></span>    |
| <span data-ttu-id="12aa6-189">24</span><span class="sxs-lookup"><span data-stu-id="12aa6-189">24</span></span>                        | <span data-ttu-id="12aa6-190">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="12aa6-190">DHGroup24</span></span>                | <span data-ttu-id="12aa6-191">PFS24</span><span class="sxs-lookup"><span data-stu-id="12aa6-191">PFS24</span></span>        | <span data-ttu-id="12aa6-192">2048 位元 MODP</span><span class="sxs-lookup"><span data-stu-id="12aa6-192">2048-bit MODP</span></span>  |

<span data-ttu-id="12aa6-193">如需詳細資訊，請參閱 [RFC3526](https://tools.ietf.org/html/rfc3526) 和 [RFC5114](https://tools.ietf.org/html/rfc5114)。</span><span class="sxs-lookup"><span data-stu-id="12aa6-193">Refer to [RFC3526](https://tools.ietf.org/html/rfc3526) and [RFC5114](https://tools.ietf.org/html/rfc5114) for more details.</span></span>

## <span data-ttu-id="12aa6-194"><a name ="crossprem"></a>第 3 部分 - 使用 IPsec/IKE 原則建立新的 S2S VPN 連線</span><span class="sxs-lookup"><span data-stu-id="12aa6-194"><a name ="crossprem"></a>Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>

<span data-ttu-id="12aa6-195">本節將逐步引導您使用 IPsec/IKE 原則建立 S2S VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="12aa6-195">This section walks you through the steps of creating a S2S VPN connection with an IPsec/IKE policy.</span></span> <span data-ttu-id="12aa6-196">下列步驟將建立連線，如圖所示：</span><span class="sxs-lookup"><span data-stu-id="12aa6-196">The following steps create the connection as shown in the diagram:</span></span>

![s2s-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/s2spolicy.png)

<span data-ttu-id="12aa6-198">如需建立 S2S VPN 連線的詳細逐步指示，請參閱[建立 S2S VPN 連線](vpn-gateway-create-site-to-site-rm-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="12aa6-198">See [Create a S2S VPN connection](vpn-gateway-create-site-to-site-rm-powershell.md) for more detailed step-by-step instructions for creating a S2S VPN connection.</span></span>

### <span data-ttu-id="12aa6-199"><a name="before"></a>開始之前</span><span class="sxs-lookup"><span data-stu-id="12aa6-199"><a name="before"></a>Before you begin</span></span>

* <span data-ttu-id="12aa6-200">請確認您有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="12aa6-200">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="12aa6-201">如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="12aa6-201">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="12aa6-202">您必須安裝 Azure Resource Manager PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="12aa6-202">Install the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="12aa6-203">如需安裝 PowerShell Cmdlet 的詳細資訊，請參閱[如何安裝和設定 Azure PowerShell](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="12aa6-203">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span>

### <span data-ttu-id="12aa6-204"><a name="createvnet1"></a>步驟1 - 建立虛擬網路、VPN 閘道和區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="12aa6-204"><a name="createvnet1"></a>Step 1 - Create the virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="12aa6-205">1.宣告變數</span><span class="sxs-lookup"><span data-stu-id="12aa6-205">1. Declare your variables</span></span>

<span data-ttu-id="12aa6-206">對於此練習，我們一開始先宣告我們的變數。</span><span class="sxs-lookup"><span data-stu-id="12aa6-206">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="12aa6-207">請務必在設定生產環境時，使用您自己的值來取代該值。</span><span class="sxs-lookup"><span data-stu-id="12aa6-207">Be sure to replace the values with your own when configuring for production.</span></span>

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```

#### <a name="2-connect-to-your-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="12aa6-208">2.連接至您的訂用帳戶並建立新的資源群組</span><span class="sxs-lookup"><span data-stu-id="12aa6-208">2. Connect to your subscription and create a new resource group</span></span>

<span data-ttu-id="12aa6-209">請確定您切換為 PowerShell 模式以使用資源管理員 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="12aa6-209">Make sure you switch to PowerShell mode to use the Resource Manager cmdlets.</span></span> <span data-ttu-id="12aa6-210">如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與 Resource Manager](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="12aa6-210">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="12aa6-211">開啟 PowerShell 主控台並連接到您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="12aa6-211">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="12aa6-212">使用下列範例來協助您連接：</span><span class="sxs-lookup"><span data-stu-id="12aa6-212">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-the-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="12aa6-213">3.建立虛擬網路、VPN 閘道和區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="12aa6-213">3. Create the virtual network, VPN gateway, and local network gateway</span></span>

<span data-ttu-id="12aa6-214">下列範例會建立有三個子網路的虛擬網路 TestVNet1 和 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="12aa6-214">The following sample creates the virtual network, TestVNet1, with three subnets, and the VPN gateway.</span></span> <span data-ttu-id="12aa6-215">替代值時，務必一律將您的閘道子網路特定命名為 GatewaySubnet。</span><span class="sxs-lookup"><span data-stu-id="12aa6-215">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="12aa6-216">如果您將其命名為其他名稱，閘道建立會失敗。</span><span class="sxs-lookup"><span data-stu-id="12aa6-216">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <span data-ttu-id="12aa6-217"><a name="s2sconnection"></a>步驟 2 - 使用 IPsec/IKE 原則建立 S2S VPN 連線</span><span class="sxs-lookup"><span data-stu-id="12aa6-217"><a name="s2sconnection"></a>Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="12aa6-218">1.建立 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="12aa6-218">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="12aa6-219">下列範例指令碼會使用下列演算法和參數來建立 IPsec/IKE 原則：</span><span class="sxs-lookup"><span data-stu-id="12aa6-219">The following sample script creates an IPsec/IKE policy with the following algorithms and parameters:</span></span>

* <span data-ttu-id="12aa6-220">IKEv2：AES256、SHA384、DHGroup24</span><span class="sxs-lookup"><span data-stu-id="12aa6-220">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="12aa6-221">IPsec：AES256、SHA256、PFS24、SA 存留期 7200 秒和 2048KB</span><span class="sxs-lookup"><span data-stu-id="12aa6-221">IPsec: AES256, SHA256, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

<span data-ttu-id="12aa6-222">如果您針對 IPsec 使用 GCMAES，就必須針對 IPsec 加密和完整性使用相同的 GCMAES 演算法和金鑰長度，例如：</span><span class="sxs-lookup"><span data-stu-id="12aa6-222">If you use GCMAES for IPsec, you must use the same GCMAES algorithm and key length for both IPsec encryption and integrity, for example:</span></span>

* <span data-ttu-id="12aa6-223">IKEv2：AES256、SHA384、DHGroup24</span><span class="sxs-lookup"><span data-stu-id="12aa6-223">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="12aa6-224">IPsec：**GCMAES256、GCMAES256**、PFS24、SA 存留期 7200 秒和 2048KB</span><span class="sxs-lookup"><span data-stu-id="12aa6-224">IPsec: **GCMAES256, GCMAES256**, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption GCMAES256 -IpsecIntegrity GCMAES256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

#### <a name="2-create-the-s2s-vpn-connection-with-the-ipsecike-policy"></a><span data-ttu-id="12aa6-225">2.使用 IPsec/IKE 原則建立 S2S VPN 連線</span><span class="sxs-lookup"><span data-stu-id="12aa6-225">2. Create the S2S VPN connection with the IPsec/IKE policy</span></span>

<span data-ttu-id="12aa6-226">建立 S2S VPN 連線，並套用稍早建立的 IPsec/IKE 原則。</span><span class="sxs-lookup"><span data-stu-id="12aa6-226">Create an S2S VPN connection and apply the IPsec/IKE policy created earlier.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="12aa6-227">您可以選擇性地將 "-UsePolicyBasedTrafficSelectors $True" 新增至建立連線 Cmdlet，讓 Azure VPN 閘道連線至內部部署以原則為基礎的 VPN 裝置，如上所述。</span><span class="sxs-lookup"><span data-stu-id="12aa6-227">You can optionally add "-UsePolicyBasedTrafficSelectors $True" to the create connection cmdlet to enable Azure VPN gateway to connect to policy-based VPN devices on premises, as described above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12aa6-228">在連線上指定 IPsec/IKE 原則之後，Azure VPN 閘道只會傳送或接受該特定連線上的 IPsec/IKE 提案，而提案具有所指定的密碼編譯演算法和金鑰長度。</span><span class="sxs-lookup"><span data-stu-id="12aa6-228">Once an IPsec/IKE policy is specified on a connection, the Azure VPN gateway will only send or accept the IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="12aa6-229">確定連線的內部部署 VPN 裝置使用或接受確切原則組合，否則不會建立 S2S VPN 通道。</span><span class="sxs-lookup"><span data-stu-id="12aa6-229">Make sure your on-premises VPN device for the connection uses or accepts the exact policy combination, otherwise the S2S VPN tunnel will not establish.</span></span>


## <span data-ttu-id="12aa6-230"><a name ="vnet2vnet"></a>第 4 部分 - 使用 IPsec/IKE 原則建立新的 VNet 對 VNet 連線</span><span class="sxs-lookup"><span data-stu-id="12aa6-230"><a name ="vnet2vnet"></a>Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>

<span data-ttu-id="12aa6-231">使用 IPsec/IKE 原則建立 VNet 對 VNet 連線的步驟，與使用 IPsec/IKE 原則建立 S2S VPN 連線的步驟相同。</span><span class="sxs-lookup"><span data-stu-id="12aa6-231">The steps of creating a VNet-to-VNet connection with an IPsec/IKE policy are similar to that of a S2S VPN connection.</span></span> <span data-ttu-id="12aa6-232">下列範例指令碼將建立連線，如圖所示：</span><span class="sxs-lookup"><span data-stu-id="12aa6-232">The following sample scripts create the connection as shown in the diagram:</span></span>

![v2v-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/v2vpolicy.png)

<span data-ttu-id="12aa6-234">如需建立 VNet 對 VNet 連線的詳細步驟，請參閱[建立 VNet 對 VNet 連線](vpn-gateway-vnet-vnet-rm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="12aa6-234">See [Create a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) for more detailed steps for creating a VNet-to-VNet connection.</span></span> <span data-ttu-id="12aa6-235">您必須完成[第 3 部分](#crossprem)，才能建立和設定 TestVNet1 及 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="12aa6-235">You must complete [Part 3](#crossprem) to create and configure TestVNet1 and the VPN Gateway.</span></span>

### <span data-ttu-id="12aa6-236"><a name="createvnet2"></a>步驟 1 - 建立第二個虛擬網路和 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="12aa6-236"><a name="createvnet2"></a>Step 1 - Create the second virtual network and VPN gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="12aa6-237">1.宣告變數</span><span class="sxs-lookup"><span data-stu-id="12aa6-237">1. Declare your variables</span></span>

<span data-ttu-id="12aa6-238">請務必使用您想用於設定的值來取代該值。</span><span class="sxs-lookup"><span data-stu-id="12aa6-238">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG2          = "TestPolicyRG2"
$Location2    = "East US 2"
$VNetName2    = "TestVNet2"
$FESubName2   = "FrontEnd"
$BESubName2   = "Backend"
$GWSubName2   = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$DNS2         = "8.8.8.8"
$GWName2      = "VNet2GW"
$GW2IPName1   = "VNet2GWIP1"
$GW2IPconf1   = "gw2ipconf1"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-the-second-virtual-network-and-vpn-gateway-in-the-new-resource-group"></a><span data-ttu-id="12aa6-239">2.在新的資源群組中建立第二個虛擬網路和 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="12aa6-239">2. Create the second virtual network and VPN gateway in the new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2

$gw2pip1    = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$vnet2      = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1

New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance
```

### <a name="step-2---create-a-vnet-tovnet-connection-with-the-ipsecike-policy"></a><span data-ttu-id="12aa6-240">步驟 2 - 使用 IPsec/IKE 原則建立 VNet 對 VNet 連線</span><span class="sxs-lookup"><span data-stu-id="12aa6-240">Step 2 - Create a VNet-toVNet connection with the IPsec/IKE policy</span></span>

<span data-ttu-id="12aa6-241">與 S2S VPN 連線類似，請建立 IPsec/IKE 原則，然後將原則套用至新的連線。</span><span class="sxs-lookup"><span data-stu-id="12aa6-241">Similar to the S2S VPN connection, create an IPsec/IKE policy then apply to policy to the new connection.</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="12aa6-242">1.建立 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="12aa6-242">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="12aa6-243">下列範例指令碼會使用下列演算法和參數來建立不同的 IPsec/IKE 原則：</span><span class="sxs-lookup"><span data-stu-id="12aa6-243">The following sample script creates a different IPsec/IKE policy with the following algorithms and parameters:</span></span>
* <span data-ttu-id="12aa6-244">IKEv2：AES128、SHA1、DHGroup14</span><span class="sxs-lookup"><span data-stu-id="12aa6-244">IKEv2: AES128, SHA1, DHGroup14</span></span>
* <span data-ttu-id="12aa6-245">IPsec：GCMAES128、GCMAES128、PFS14、SA 存留期 7200 秒和 4096KB</span><span class="sxs-lookup"><span data-stu-id="12aa6-245">IPsec: GCMAES128, GCMAES128, PFS14, SA Lifetime 7200 seconds & 4096KB</span></span>

```powershell
$ipsecpolicy2 = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup PFS14 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 4096
```

#### <a name="2-create-vnet-to-vnet-connections-with-the-ipsecike-policy"></a><span data-ttu-id="12aa6-246">2.使用 IPsec/IKE 原則建立 VNet 對 VNet 連線</span><span class="sxs-lookup"><span data-stu-id="12aa6-246">2. Create VNet-to-VNet connections with the IPsec/IKE policy</span></span>

<span data-ttu-id="12aa6-247">建立 VNet 對 VNet 連線，並套用您建立的 IPsec/IKE 原則。</span><span class="sxs-lookup"><span data-stu-id="12aa6-247">Create a VNet-to-VNet connection and apply the IPsec/IKE policy you created.</span></span> <span data-ttu-id="12aa6-248">在此範例中，兩個閘道位於相同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="12aa6-248">In this example, both gateways are in the same subscription.</span></span> <span data-ttu-id="12aa6-249">因此，可以在相同的 PowerShell 工作階段中建立和設定兩個具有相同 IPsec/IKE 原則的連線。</span><span class="sxs-lookup"><span data-stu-id="12aa6-249">So it is possible to create and configure both connections with the same IPsec/IKE policy in the same PowerShell session.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2  -ResourceGroupName $RG2

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'
```

> [!IMPORTANT]
> <span data-ttu-id="12aa6-250">在連線上指定 IPsec/IKE 原則之後，Azure VPN 閘道只會傳送或接受該特定連線上的 IPsec/IKE 提案，而提案具有所指定的密碼編譯演算法和金鑰長度。</span><span class="sxs-lookup"><span data-stu-id="12aa6-250">Once an IPsec/IKE policy is specified on a connection, the Azure VPN gateway will only send or accept the IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="12aa6-251">確定這兩個連線的 IPsec 原則相同，否則不會建立 VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="12aa6-251">Make sure the IPsec policies for both connections are the same, otherwise the VNet-to-VNet connection will not establish.</span></span>

<span data-ttu-id="12aa6-252">完成這些步驟之後，就會在幾分鐘內建立連線，而且您會有下列網路拓撲，如開頭所示：</span><span class="sxs-lookup"><span data-stu-id="12aa6-252">After completing these steps, the connection is established in a few minutes, and you will have the following network topology as shown in the beginning:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)


## <span data-ttu-id="12aa6-254"><a name ="managepolicy"></a>第 5 部分 - 更新連線的 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="12aa6-254"><a name ="managepolicy"></a>Part 5 - Update IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="12aa6-255">最後一節會說明如何管理現有 S2S 或 VNet 對 VNet 連線的 IPsec/IKE 原則。</span><span class="sxs-lookup"><span data-stu-id="12aa6-255">The last section shows you how to manage IPsec/IKE policy for an existing S2S or VNet-to-VNet connection.</span></span> <span data-ttu-id="12aa6-256">下列練習會引導您在連線上進行下列作業：</span><span class="sxs-lookup"><span data-stu-id="12aa6-256">The exercise below walks you through the following operations on a connection:</span></span>

1. <span data-ttu-id="12aa6-257">顯示連線的 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="12aa6-257">Show the IPsec/IKE policy of a connection</span></span>
2. <span data-ttu-id="12aa6-258">新增或更新連線的 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="12aa6-258">Add or update the IPsec/IKE policy to a connection</span></span>
3. <span data-ttu-id="12aa6-259">移除連線的 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="12aa6-259">Remove the IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="12aa6-260">相同的步驟適用於 S2S 和 VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="12aa6-260">The same steps apply to both S2S and VNet-to-VNet connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12aa6-261">只有 Standard 和 HighPerformance 以路由為基礎的 VPN 閘道才支援 IPsec/IKE 原則。</span><span class="sxs-lookup"><span data-stu-id="12aa6-261">IPsec/IKE policy is supported on *Standard* and *HighPerformance* route-based VPN gateways only.</span></span> <span data-ttu-id="12aa6-262">它不適用於 Basic 閘道 SKU 或以原則為基礎的 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="12aa6-262">It does not work on the Basic gateway SKU or the policy-based VPN gateway.</span></span>

#### <a name="1-show-the-ipsecike-policy-of-a-connection"></a><span data-ttu-id="12aa6-263">1.顯示連線的 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="12aa6-263">1. Show the IPsec/IKE policy of a connection</span></span>

<span data-ttu-id="12aa6-264">下列範例示範如何取得連線上所設定的 IPsec/IKE 原則。</span><span class="sxs-lookup"><span data-stu-id="12aa6-264">The following example shows how to get the IPsec/IKE policy configured on a connection.</span></span> <span data-ttu-id="12aa6-265">指令碼也會從上述練習繼續。</span><span class="sxs-lookup"><span data-stu-id="12aa6-265">The scripts also continue from the exercises above.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="12aa6-266">最後一個命令會列出連線上所設定的目前 IPsec/IKE 原則 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="12aa6-266">The last command lists the current IPsec/IKE policy configured on the connection, if there is any.</span></span> <span data-ttu-id="12aa6-267">下列範例輸出適用於連線：</span><span class="sxs-lookup"><span data-stu-id="12aa6-267">The following sample output is for the connection:</span></span>

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : AES256
IpsecIntegrity      : SHA256
IkeEncryption       : AES256
IkeIntegrity        : SHA384
DhGroup             : DHGroup24
PfsGroup            : PFS24
```

<span data-ttu-id="12aa6-268">如果未設定任何 IPsec/IKE 原則，命令 (PS> $connection6.policy) 會收到空白傳回。</span><span class="sxs-lookup"><span data-stu-id="12aa6-268">If there is no IPsec/IKE policy configured, the command (PS> $connection6.policy) gets an empty return.</span></span> <span data-ttu-id="12aa6-269">這並不表示連線上未設定 IPsec/IKE，而是沒有自訂 IPsec/IKE 原則。</span><span class="sxs-lookup"><span data-stu-id="12aa6-269">It does not mean IPsec/IKE is not configured on the connection, but that there is no custom IPsec/IKE policy.</span></span> <span data-ttu-id="12aa6-270">實際連線會使用內部部署 VPN 裝置與 Azure VPN 閘道之間交涉的預設原則。</span><span class="sxs-lookup"><span data-stu-id="12aa6-270">The actual connection uses the default policy negotiated between your on-premises VPN device and the Azure VPN gateway.</span></span>

#### <a name="2-add-or-update-an-ipsecike-policy-for-a-connection"></a><span data-ttu-id="12aa6-271">2.新增或更新連線的 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="12aa6-271">2. Add or update an IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="12aa6-272">在連線上新增原則或更新現有原則的步驟相同：建立新的原則，然後將新的原則套用至連線。</span><span class="sxs-lookup"><span data-stu-id="12aa6-272">The steps to add a new policy or update an existing policy on a connection are the same: create a new policy then apply the new policy to the connection.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$newpolicy6   = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup None -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6
```

<span data-ttu-id="12aa6-273">若要在連線至內部部署以原則為基礎的 VPN 裝置時啟用 "UsePolicyBasedTrafficSelectors"，請將 "-UsePolicyBaseTrafficSelectors" 參數新增至 Cmdlet，或將它設定為 $False 以停用此選項：</span><span class="sxs-lookup"><span data-stu-id="12aa6-273">To enable "UsePolicyBasedTrafficSelectors" when connecting to an on-premises policy-based VPN device, add the "-UsePolicyBaseTrafficSelectors" parameter to the cmdlet, or set it to $False to disable the option:</span></span>

```powershell
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6 -UsePolicyBasedTrafficSelectors $True
```

<span data-ttu-id="12aa6-274">您可以再次取得連線，以檢查是否已更新原則。</span><span class="sxs-lookup"><span data-stu-id="12aa6-274">You can get the connection again to check if the policy is updated.</span></span>

```powershell
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="12aa6-275">您應該會在最後一行看到輸出，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="12aa6-275">You should see the output from the last line, as shown in the following example:</span></span>

```powershell
SALifeTimeSeconds   : 3600
SADataSizeKilobytes : 2048
IpsecEncryption     : GCMAES128
IpsecIntegrity      : GCMAES128
IkeEncryption       : AES128
IkeIntegrity        : SHA1
DhGroup             : DHGroup14--
PfsGroup            : None
```

#### <a name="3-remove-an-ipsecike-policy-from-a-connection"></a><span data-ttu-id="12aa6-276">3.移除連線的 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="12aa6-276">3. Remove an IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="12aa6-277">移除連線的自訂原則後，Azure VPN 閘道會回復為使用[預設的 IPsec/IKE 提案清單](vpn-gateway-about-vpn-devices.md)，並與內部部署 VPN 裝置重新進行交涉。</span><span class="sxs-lookup"><span data-stu-id="12aa6-277">Once you remove the custom policy from a connection, the Azure VPN gateway reverts back to the [default list of IPsec/IKE proposals](vpn-gateway-about-vpn-devices.md) and renegotiates again with your on-premises VPN device.</span></span>

```powershell
$RG1           = "TestPolicyRG1"
$Connection16  = "VNet1toSite6"
$connection6   = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$currentpolicy = $connection6.IpsecPolicies[0]
$connection6.IpsecPolicies.Remove($currentpolicy)

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6
```

<span data-ttu-id="12aa6-278">您可以使用相同的指令碼，以檢查是否已從連線中移除原則。</span><span class="sxs-lookup"><span data-stu-id="12aa6-278">You can use the same script to check if the policy has been removed from the connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12aa6-279">後續步驟</span><span class="sxs-lookup"><span data-stu-id="12aa6-279">Next steps</span></span>

<span data-ttu-id="12aa6-280">如需以原則為基礎的流量選取器的詳細資訊，請參閱[連線多個內部部署以原則為基礎的 VPN 裝置](vpn-gateway-connect-multiple-policybased-rm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="12aa6-280">See [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) for more details regarding policy-based traffic selectors.</span></span>

<span data-ttu-id="12aa6-281">一旦完成您的連接，就可以將虛擬機器加入您的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="12aa6-281">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="12aa6-282">請參閱 [建立網站的虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 以取得相關步驟。</span><span class="sxs-lookup"><span data-stu-id="12aa6-282">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>