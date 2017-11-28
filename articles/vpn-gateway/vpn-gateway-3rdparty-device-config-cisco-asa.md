---
title: "aaaSample 組態-連接 tooAzure VPN 閘道的 Cisco ASA 裝置 |Microsoft 文件"
description: "本文章提供設定連線 tooAzure VPN 閘道的 Cisco ASA 裝置的範例。"
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: dad13e02afe8dad2379db750eb09602e08e8ea99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a><span data-ttu-id="5b069-103">範例組態：Cisco ASA 裝置 (IKEv2/無 BGP)</span><span class="sxs-lookup"><span data-stu-id="5b069-103">Sample configuration: Cisco ASA device (IKEv2/no BGP)</span></span>
<span data-ttu-id="5b069-104">本文章提供範例設定適用於 Cisco ASA 裝置連接 tooAzure VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="5b069-104">This article provides sample configurations for Cisco ASA devices connecting tooAzure VPN gateways.</span></span>

## <a name="device-at-a-glance"></a><span data-ttu-id="5b069-105">裝置速覽</span><span class="sxs-lookup"><span data-stu-id="5b069-105">Device at a glance</span></span>

|                        |                                   |
| ---                    | ---                               |
| <span data-ttu-id="5b069-106">裝置廠商</span><span class="sxs-lookup"><span data-stu-id="5b069-106">Device vendor</span></span>          | <span data-ttu-id="5b069-107">Cisco</span><span class="sxs-lookup"><span data-stu-id="5b069-107">Cisco</span></span>                             |
| <span data-ttu-id="5b069-108">裝置型號</span><span class="sxs-lookup"><span data-stu-id="5b069-108">Device model</span></span>           | <span data-ttu-id="5b069-109">ASA (Adaptive Security Appliance)</span><span class="sxs-lookup"><span data-stu-id="5b069-109">ASA (Adaptive Security Appliance)</span></span> |
| <span data-ttu-id="5b069-110">目標版本</span><span class="sxs-lookup"><span data-stu-id="5b069-110">Target version</span></span>         | <span data-ttu-id="5b069-111">8.4+</span><span class="sxs-lookup"><span data-stu-id="5b069-111">8.4+</span></span>                              |
| <span data-ttu-id="5b069-112">測試的型號</span><span class="sxs-lookup"><span data-stu-id="5b069-112">Tested model</span></span>           | <span data-ttu-id="5b069-113">ASA 5505</span><span class="sxs-lookup"><span data-stu-id="5b069-113">ASA 5505</span></span>                          |
| <span data-ttu-id="5b069-114">測試的版本</span><span class="sxs-lookup"><span data-stu-id="5b069-114">Tested version</span></span>         | <span data-ttu-id="5b069-115">9.2</span><span class="sxs-lookup"><span data-stu-id="5b069-115">9.2</span></span>                               |
| <span data-ttu-id="5b069-116">IKE 版本</span><span class="sxs-lookup"><span data-stu-id="5b069-116">IKE version</span></span>            | <span data-ttu-id="5b069-117">**IKEv2**</span><span class="sxs-lookup"><span data-stu-id="5b069-117">**IKEv2**</span></span>                         |
| <span data-ttu-id="5b069-118">BGP</span><span class="sxs-lookup"><span data-stu-id="5b069-118">BGP</span></span>                    | <span data-ttu-id="5b069-119">**否**</span><span class="sxs-lookup"><span data-stu-id="5b069-119">**No**</span></span>                            |
| <span data-ttu-id="5b069-120">Azure VPN 閘道類型</span><span class="sxs-lookup"><span data-stu-id="5b069-120">Azure VPN gateway type</span></span> | <span data-ttu-id="5b069-121">**路由式** VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="5b069-121">**Route-based** VPN gateway</span></span>       |
|                        |                                   |

> [!NOTE]
> 1. <span data-ttu-id="5b069-122">下列的 hello 組態連接 Cisco ASA 裝置 tooan Azure**路由式**"UserPolicyBasedTrafficSelectors 」 選項時，使用自訂 IPsec/IKE 原則，如下所示的 VPN 閘道[本文](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="5b069-122">hello configuration below connects a Cisco ASA device tooan Azure **route-based** VPN gateway using custom IPsec/IKE policy with "UserPolicyBasedTrafficSelectors" option, as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>
> 2. <span data-ttu-id="5b069-123">它需要 ASA 裝置 toouse **IKEv2**使用存取清單為基礎的組態，不以 VTI 為基礎。</span><span class="sxs-lookup"><span data-stu-id="5b069-123">It requires ASA devices toouse **IKEv2** with access-list-based configurations, not VTI-based.</span></span>
> 3. <span data-ttu-id="5b069-124">請洽詢您 tooensure hello 原則在內部部署 VPN 裝置支援的 VPN 裝置廠商規格。</span><span class="sxs-lookup"><span data-stu-id="5b069-124">Please consult with your VPN device vendor specifications tooensure hello policy is supported on your on-premises VPN devices.</span></span>

## <a name="vpn-device-requirements"></a><span data-ttu-id="5b069-125">VPN 裝置需求</span><span class="sxs-lookup"><span data-stu-id="5b069-125">VPN device requirements</span></span>
<span data-ttu-id="5b069-126">Azure VPN 閘道使用標準 IPsec/IKE 通訊協定套件 tooestablish S2S VPN 通道。</span><span class="sxs-lookup"><span data-stu-id="5b069-126">Azure VPN gateways use standard IPsec/IKE protocol suites tooestablish S2S VPN tunnels.</span></span> <span data-ttu-id="5b069-127">請參閱太[關於 VPN 裝置](vpn-gateway-about-vpn-devices.md)hello 詳細的 IPsec/IKE 通訊協定參數和 Azure VPN 閘道的預設密碼編譯演算法。</span><span class="sxs-lookup"><span data-stu-id="5b069-127">Refer too[About VPN devices](vpn-gateway-about-vpn-devices.md) for hello detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="5b069-128">中所述，您可以選擇指定的密碼編譯演算法和金鑰長度為特定連線的 hello 確切組合[有關密碼編譯需求](vpn-gateway-about-compliance-crypto.md)。</span><span class="sxs-lookup"><span data-stu-id="5b069-128">You can optionally specify hello exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span> <span data-ttu-id="5b069-129">如果您選取特定密碼編譯演算法和金鑰長度的組合，請確定您使用您的 VPN 裝置 hello 對應規格。</span><span class="sxs-lookup"><span data-stu-id="5b069-129">If you select a specific combination of cryptographic algorithms and key strengths, please make sure you use hello corresponding specifications on your VPN devices.</span></span>

## <a name="single-vpn-tunnel"></a><span data-ttu-id="5b069-130">單一 VPN 通道</span><span class="sxs-lookup"><span data-stu-id="5b069-130">Single VPN tunnel</span></span>
<span data-ttu-id="5b069-131">此拓撲是由 Azure VPN 閘道與您內部部署 VPN 裝置之間的單一 S2S VPN 通道所組成。</span><span class="sxs-lookup"><span data-stu-id="5b069-131">This topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="5b069-132">您可以選擇性地跨 hello VPN 通道設定 BGP。</span><span class="sxs-lookup"><span data-stu-id="5b069-132">You can optionally configure BGP across hello VPN tunnel.</span></span>

![單一通道](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

<span data-ttu-id="5b069-134">請參閱太[單一通道設定](vpn-gateway-3rdparty-device-config-overview.md#singletunnel)如詳細，逐步解說 toobuild hello Azure 組態。</span><span class="sxs-lookup"><span data-stu-id="5b069-134">Refer too[Single tunnel setup](vpn-gateway-3rdparty-device-config-overview.md#singletunnel) for detailed, step-by-step instructions toobuild hello Azure configurations.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="5b069-135">網路和 VPN 閘道資訊</span><span class="sxs-lookup"><span data-stu-id="5b069-135">Network and VPN gateway information</span></span>
<span data-ttu-id="5b069-136">本節列出此範例的 hello hello 參數。</span><span class="sxs-lookup"><span data-stu-id="5b069-136">This section list hello parameters for hello this sample.</span></span>

| <span data-ttu-id="5b069-137">**參數**</span><span class="sxs-lookup"><span data-stu-id="5b069-137">**Parameter**</span></span>                | <span data-ttu-id="5b069-138">**值**</span><span class="sxs-lookup"><span data-stu-id="5b069-138">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="5b069-139">VNet 位址首碼</span><span class="sxs-lookup"><span data-stu-id="5b069-139">VNet address prefixes</span></span>        | <span data-ttu-id="5b069-140">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5b069-140">10.11.0.0/16</span></span><br><span data-ttu-id="5b069-141">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5b069-141">10.12.0.0/16</span></span> |
| <span data-ttu-id="5b069-142">Azure VPN 閘道 IP</span><span class="sxs-lookup"><span data-stu-id="5b069-142">Azure VPN gateway IP</span></span>         | <span data-ttu-id="5b069-143">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="5b069-143">Azure_Gateway_Public_IP</span></span>      |
| <span data-ttu-id="5b069-144">內部部署位址首碼</span><span class="sxs-lookup"><span data-stu-id="5b069-144">On-premises address prefixes</span></span> | <span data-ttu-id="5b069-145">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5b069-145">10.51.0.0/16</span></span><br><span data-ttu-id="5b069-146">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5b069-146">10.52.0.0/16</span></span> |
| <span data-ttu-id="5b069-147">內部部署 VPN 裝置 IP</span><span class="sxs-lookup"><span data-stu-id="5b069-147">On-premises VPN device IP</span></span>    | <span data-ttu-id="5b069-148">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="5b069-148">OnPrem_Device_Public_IP</span></span>     |
| <span data-ttu-id="5b069-149">*VNet BGP ASN</span><span class="sxs-lookup"><span data-stu-id="5b069-149">*VNet BGP ASN</span></span>                | <span data-ttu-id="5b069-150">65010</span><span class="sxs-lookup"><span data-stu-id="5b069-150">65010</span></span>                        |
| <span data-ttu-id="5b069-151">*Azure BGP 對等 IP</span><span class="sxs-lookup"><span data-stu-id="5b069-151">*Azure BGP peer IP</span></span>           | <span data-ttu-id="5b069-152">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="5b069-152">10.12.255.30</span></span>                 |
| <span data-ttu-id="5b069-153">*內部部署 BGP ASN</span><span class="sxs-lookup"><span data-stu-id="5b069-153">*On-premises BGP ASN</span></span>         | <span data-ttu-id="5b069-154">65050</span><span class="sxs-lookup"><span data-stu-id="5b069-154">65050</span></span>                        |
| <span data-ttu-id="5b069-155">*內部部署 BGP 對等 IP</span><span class="sxs-lookup"><span data-stu-id="5b069-155">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="5b069-156">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="5b069-156">10.52.255.254</span></span>                |
|                              |                              |

* <span data-ttu-id="5b069-157">(*) 僅適用於 BGP 的選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="5b069-157">(*) Optional parameters for BGP only.</span></span>

### <a name="ipsecike-policy--parameters"></a><span data-ttu-id="5b069-158">IPsec/IKE 原則與參數</span><span class="sxs-lookup"><span data-stu-id="5b069-158">IPsec/IKE policy & parameters</span></span>

<span data-ttu-id="5b069-159">hello 下表列出 hello IPsec/IKE 演算法和 hello 範例中使用的參數。</span><span class="sxs-lookup"><span data-stu-id="5b069-159">hello table below lists hello IPsec/IKE algorithms and parameters used in hello sample.</span></span> <span data-ttu-id="5b069-160">請參閱您 VPN 裝置規格 toomake 確定您的 VPN 裝置型號和軔體版本支援以上所列的所有演算法。</span><span class="sxs-lookup"><span data-stu-id="5b069-160">Please consult your VPN device specifications toomake sure all algorithms listed above are supported by your VPN device models and firmware versions.</span></span>

| <span data-ttu-id="5b069-161">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="5b069-161">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="5b069-162">**值**</span><span class="sxs-lookup"><span data-stu-id="5b069-162">**Value**</span></span>                            |
| ---              | ---                                  |
| <span data-ttu-id="5b069-163">IKEv2 加密</span><span class="sxs-lookup"><span data-stu-id="5b069-163">IKEv2 Encryption</span></span> | <span data-ttu-id="5b069-164">AES256</span><span class="sxs-lookup"><span data-stu-id="5b069-164">AES256</span></span>                               |
| <span data-ttu-id="5b069-165">IKEv2 完整性</span><span class="sxs-lookup"><span data-stu-id="5b069-165">IKEv2 Integrity</span></span>  | <span data-ttu-id="5b069-166">SHA384</span><span class="sxs-lookup"><span data-stu-id="5b069-166">SHA384</span></span>                               |
| <span data-ttu-id="5b069-167">DH 群組</span><span class="sxs-lookup"><span data-stu-id="5b069-167">DH Group</span></span>         | <span data-ttu-id="5b069-168">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="5b069-168">DHGroup24</span></span>                            |
| <span data-ttu-id="5b069-169">IPsec 加密</span><span class="sxs-lookup"><span data-stu-id="5b069-169">IPsec Encryption</span></span> | <span data-ttu-id="5b069-170">AES256</span><span class="sxs-lookup"><span data-stu-id="5b069-170">AES256</span></span>                               |
| <span data-ttu-id="5b069-171">IPsec 完整性</span><span class="sxs-lookup"><span data-stu-id="5b069-171">IPsec Integrity</span></span>  | <span data-ttu-id="5b069-172">SHA1</span><span class="sxs-lookup"><span data-stu-id="5b069-172">SHA1</span></span>                                 |
| <span data-ttu-id="5b069-173">PFS 群組</span><span class="sxs-lookup"><span data-stu-id="5b069-173">PFS Group</span></span>        | <span data-ttu-id="5b069-174">PFS24</span><span class="sxs-lookup"><span data-stu-id="5b069-174">PFS24</span></span>                                |
| <span data-ttu-id="5b069-175">QM SA 存留期</span><span class="sxs-lookup"><span data-stu-id="5b069-175">QM SA Lifetime</span></span>   | <span data-ttu-id="5b069-176">7200 秒</span><span class="sxs-lookup"><span data-stu-id="5b069-176">7200 seconds</span></span>                         |
| <span data-ttu-id="5b069-177">流量選取器</span><span class="sxs-lookup"><span data-stu-id="5b069-177">Traffic Selector</span></span> | <span data-ttu-id="5b069-178">UsePolicyBasedTrafficSelectors $True</span><span class="sxs-lookup"><span data-stu-id="5b069-178">UsePolicyBasedTrafficSelectors $True</span></span> |
| <span data-ttu-id="5b069-179">預先共用金鑰</span><span class="sxs-lookup"><span data-stu-id="5b069-179">Pre-Shared Key</span></span>   | <span data-ttu-id="5b069-180">PreSharedKey</span><span class="sxs-lookup"><span data-stu-id="5b069-180">PreSharedKey</span></span>                         |
|                  |                                      |

- <span data-ttu-id="5b069-181">(*) 在某些裝置上，如果使用 GCM AES 作為 IPsec 加密演算法，IPsec 完整性就必須為 "null"。</span><span class="sxs-lookup"><span data-stu-id="5b069-181">(*) On some device, IPsec integrity must be "null" if GCM-AES is used as IPsec encryption algorithm.</span></span>

### <a name="device-notes"></a><span data-ttu-id="5b069-182">裝置注意事項</span><span class="sxs-lookup"><span data-stu-id="5b069-182">Device notes</span></span>

>[!NOTE]
>
> 1. <span data-ttu-id="5b069-183">IKEv2 支援需要 ASA 8.4 版及更新版本。</span><span class="sxs-lookup"><span data-stu-id="5b069-183">IKEv2 support requires ASA version 8.4 and above.</span></span>
> 2. <span data-ttu-id="5b069-184">較高的 DH 和 PFS 群組支援 (除了群組 5) 需要 ASA 版本 9.x。</span><span class="sxs-lookup"><span data-stu-id="5b069-184">Higher DH and PFS group support (beyond Group 5) requires ASA version 9.x.</span></span>
> 3. <span data-ttu-id="5b069-185">在較新的 ASA 硬體上，支援透過 AES-GCM 進行的 IPsec 加密及具備 SHA-256、SHA-384、SHA-512 的 IPsec 完整性需要 ASA 版本 9.x；**不**支援 ASA 5505、5510、5520、5540、5550、5580</span><span class="sxs-lookup"><span data-stu-id="5b069-185">IPsec encryption with AES-GCM and IPsec integrity with SHA-256, SHA-384, SHA-512 support requires ASA version 9.x on newer ASA hardware; ASA 5505, 5510, 5520, 5540, 5550, 5580 are **not** supported.</span></span> <span data-ttu-id="5b069-186">（請查看 hello 廠商規格 tooconfirm。）</span><span class="sxs-lookup"><span data-stu-id="5b069-186">(Please check hello vendor specifications tooconfirm.)</span></span>
>


### <a name="sample-device-configurations"></a><span data-ttu-id="5b069-187">範例裝置組態</span><span class="sxs-lookup"><span data-stu-id="5b069-187">Sample device configurations</span></span>
<span data-ttu-id="5b069-188">下列 hello 指令碼提供設定 hello 拓撲為基礎的範例與上面所列的參數。</span><span class="sxs-lookup"><span data-stu-id="5b069-188">hello script below provides a sample configuration based on hello topology and parameters listed above.</span></span> <span data-ttu-id="5b069-189">hello S2S VPN 通道設定包含下列組件的 hello:</span><span class="sxs-lookup"><span data-stu-id="5b069-189">hello S2S VPN tunnel configuration consists of hello following parts:</span></span>

1. <span data-ttu-id="5b069-190">介面與路由</span><span class="sxs-lookup"><span data-stu-id="5b069-190">Interfaces & routes</span></span>
2. <span data-ttu-id="5b069-191">存取清單存取清單</span><span class="sxs-lookup"><span data-stu-id="5b069-191">Access lists</span></span>
3. <span data-ttu-id="5b069-192">IKE 原則和參數 (第 1 階段或主要模式)</span><span class="sxs-lookup"><span data-stu-id="5b069-192">IKE policy and parameters (Phase 1 or Main Mode)</span></span>
4. <span data-ttu-id="5b069-193">IPsec 原則和參數 (第 2 階段或快速模式)</span><span class="sxs-lookup"><span data-stu-id="5b069-193">IPsec policy and parameters (Phase 2 or Quick Mode)</span></span>
5. <span data-ttu-id="5b069-194">其他參數 (TCP MSS 固定等)</span><span class="sxs-lookup"><span data-stu-id="5b069-194">Other parameters (TCP MSS clamping, etc.)</span></span>

>[!IMPORTANT] 
><span data-ttu-id="5b069-195">請確定您完成下面所列的 hello 其他設定，而且 hello 預留位置取代為 hello 實際值：</span><span class="sxs-lookup"><span data-stu-id="5b069-195">Please make sure you complete hello additional configuration listed below and replace hello placeholders with hello actual values:</span></span>
> 
> - <span data-ttu-id="5b069-196">適用於內部和外部介面的介面組態</span><span class="sxs-lookup"><span data-stu-id="5b069-196">Interface configuration for both inside and outside interfaces</span></span>
> - <span data-ttu-id="5b069-197">適用於您內部/私用和外部/公用網路的路由</span><span class="sxs-lookup"><span data-stu-id="5b069-197">Routes for your inside/private and outside/public networks</span></span>
> - <span data-ttu-id="5b069-198">確定所有名稱和原則的數字都是唯一 hello 裝置上</span><span class="sxs-lookup"><span data-stu-id="5b069-198">Ensure all names and policy numbers are unique on hello device</span></span>
> - <span data-ttu-id="5b069-199">請確定您的裝置上支援 hello 密碼編譯演算法</span><span class="sxs-lookup"><span data-stu-id="5b069-199">Ensure hello cryptographic algorithms are supported on your device</span></span>
> - <span data-ttu-id="5b069-200">取代下列預留位置 hello 實際值的 hello</span><span class="sxs-lookup"><span data-stu-id="5b069-200">Replace hello following place holders with hello actual values</span></span>
>   - <span data-ttu-id="5b069-201">外部介面名稱："outside"</span><span class="sxs-lookup"><span data-stu-id="5b069-201">Outside interface name: "outside"</span></span>
>   - <span data-ttu-id="5b069-202">Azure_Gateway_Public_IP</span><span class="sxs-lookup"><span data-stu-id="5b069-202">Azure_Gateway_Public_IP</span></span>
>   - <span data-ttu-id="5b069-203">OnPrem_Device_Public_IP</span><span class="sxs-lookup"><span data-stu-id="5b069-203">OnPrem_Device_Public_IP</span></span>
>   - <span data-ttu-id="5b069-204">IKE Pre_Shared_Key</span><span class="sxs-lookup"><span data-stu-id="5b069-204">IKE Pre_Shared_Key</span></span>
>   - <span data-ttu-id="5b069-205">VNet 與區域網路閘道名稱 (VNetName、LNGName)</span><span class="sxs-lookup"><span data-stu-id="5b069-205">VNet and local network gateway names (VNetName, LNGName)</span></span>
>   - <span data-ttu-id="5b069-206">VNet 和內部部署網路位址首碼</span><span class="sxs-lookup"><span data-stu-id="5b069-206">VNet and on-premises network address prefixes</span></span>
>   - <span data-ttu-id="5b069-207">適當的網路遮罩</span><span class="sxs-lookup"><span data-stu-id="5b069-207">Proper netmasks</span></span>

#### <a name="sample-configuration"></a><span data-ttu-id="5b069-208">範例組態</span><span class="sxs-lookup"><span data-stu-id="5b069-208">Sample configuration</span></span>

```
! Sample ASA configuration for connecting tooAzure VPN gateway
!
! Tested hardware: ASA 5505
! Tested version:  ASA version 9.2(4)
!
! Replace hello following place holders with your actual values:
!   - Interface names - default are "outside" and "inside"
!   - <Azure_Gateway_Public_IP>
!   - <OnPrem_Device_Public_IP>
!   - <Pre_Shared_Key>
!   - <VNetName>*
!   - <LNGName>* ==> LocalNetworkGateway - hello Azure resource that represents the
!     on-premises network, specifies network prefixes, device public IP, BGP info, etc.
!   - <PrivateIPAddress> ==> Replace it with a private IP address if applicable
!   - <Netmask> ==> Replace it with appropriate netmasks
!   - <Nexthop> ==> Replace it with hello actual nexthop IP address
!
! (*) Must be unique names in hello device configuration
!
! ==> Interface & route configurations
!
!     > <OnPrem_Device_Public_IP> address on hello outside interface or vlan
!     > <PrivateIPAddress> on hello inside interface or vlan; e.g., 10.51.0.1/24
!     > Route tooconnect too<Azure_Gateway_Public_IP> address
!
!     > Example:
!
!       interface Ethernet0/0
!        switchport access vlan 2
!       exit
!
!       interface vlan 1
!        nameif inside
!        security-level 100
!        ip address <PrivateIPAddress> <Netmask>
!       exit
!
!       interface vlan 2
!        nameif outside
!        security-level 0
!        ip address <OnPrem_Device_Public_IP> <Netmask>
!       exit
!
!       route outside 0.0.0.0 0.0.0.0 <NextHop IP> 1
!
! ==> Access lists
!
!     > Most firewall devices deny all traffic by default. Create access lists to
!       (1) Allow S2S VPN tunnels between hello ASA and hello Azure gateway public IP address
!       (2) Construct traffic selectors as part of IPsec policy or proposal
!
access-list outside_access_in extended permit ip host <Azure_Gateway_Public_IP> host <OnPrem_Device_Public_IP>
!
!     > Object group that consists of all VNet prefixes (e.g., 10.11.0.0/16 &
!       10.12.0.0/16)
!
object-group network Azure-<VNetName>
 description Azure virtual network <VNetName> prefixes
 network-object 10.11.0.0 255.255.0.0
 network-object 10.12.0.0 255.255.0.0
exit
!
!     > Object group that corresponding toohello <LNGName> prefixes.
!       E.g., 10.51.0.0/16 and 10.52.0.0/16. Note that LNG = "local network gateway".
!       In Azure network resource, a local network gateway defines hello on-premises
!       network properties (address prefixes, VPN device IP, BGP ASN, etc.)
!
object-group network <LNGName>
 description On-Premises network <LNGName> prefixes
 network-object 10.51.0.0 255.255.0.0
 network-object 10.52.0.0 255.255.0.0
exit
!
!     > Specify hello access-list between hello Azure VNet and your on-premises network.
!       This access list defines hello IPsec SA traffic selectors.
!
access-list Azure-<VNetName>-acl extended permit ip object-group <LNGName> object-group Azure-<VNetName>
!
!     > No NAT required between hello on-premises network and Azure VNet
!
nat (inside,outside) source static <LNGName> <LNGName> destination static Azure-<VNetName> Azure-<VNetName>
!
! ==> IKEv2 configuration
!
!     > General IKEv2 configuration - enable IKEv2 for VPN
!
group-policy DfltGrpPolicy attributes
 vpn-tunnel-protocol ikev1 ikev2
exit
!
crypto isakmp identity address
crypto ikev2 enable outside
!
!     > Define IKEv2 Phase 1/Main Mode policy
!       - Make sure hello policy number is not used
!       - integrity and prf must be hello same
!       - DH group 14 and above require ASA version 9.x.
!
crypto ikev2 policy 1
 encryption       aes-256
 integrity        sha384
 prf              sha384
 group            24
 lifetime seconds 86400
exit
!
!     > Set connection type and pre-shared key
!
tunnel-group <Azure_Gateway_Public_IP> type ipsec-l2l
tunnel-group <Azure_Gateway_Public_IP> ipsec-attributes
 ikev2 remote-authentication pre-shared-key <Pre_Shared_Key> 
 ikev2 local-authentication  pre-shared-key <Pre_Shared_Key> 
exit
!
! ==> IPsec configuration
!
!     > IKEv2 Phase 2/Quick Mode proposal
!       - AES-GCM and SHA-2 requires ASA version 9.x on newer ASA models. ASA
!         5505, 5510, 5520, 5540, 5550, 5580 are not supported.
!       - ESP integrity must be null if AES-GCM is configured as ESP encryption
!
crypto ipsec ikev2 ipsec-proposal AES-256
 protocol esp encryption aes-256
 protocol esp integrity  sha-1
exit
!
!     > Set access list & traffic selectors, PFS, IPsec protposal, SA lifetime
!       - This sample uses "Azure-<VNetName>-map" as hello crypto map name
!       - ASA supports only one crypto map per interface, if you already have
!         an existing crypto map assigned tooyour outside interface, you must use
!         hello same crypto map name, but with a different sequence number for
!         this policy
!       - "match address" policy uses hello access-list "Azure-<VNetName>-acl" defined 
!         previously
!       - "ipsec-proposal" uses hello proposal "AES-256" defined previously 
!       - PFS groups 14 and beyond requires ASA version 9.x.
!
crypto map Azure-<VNetName>-map 1 match address Azure-<VNetName>-acl
crypto map Azure-<VNetName>-map 1 set pfs group24
crypto map Azure-<VNetName>-map 1 set peer <Azure_Gateway_Public_IP>
crypto map Azure-<VNetName>-map 1 set ikev2 ipsec-proposal AES-256
crypto map Azure-<VNetName>-map 1 set security-association lifetime seconds 7200
crypto map Azure-<VNetName>-map interface outside
!
! ==> Set TCP MSS too1350
!
sysopt connection tcpmss 1350
!
```

## <a name="simple-debugging-commands"></a><span data-ttu-id="5b069-209">簡單偵錯命令</span><span class="sxs-lookup"><span data-stu-id="5b069-209">Simple debugging commands</span></span>

<span data-ttu-id="5b069-210">以下是一些可基於偵錯用途使用的 ASA 命令：</span><span class="sxs-lookup"><span data-stu-id="5b069-210">Here are some ASA commands for debugging purposes:</span></span>

1. <span data-ttu-id="5b069-211">顯示 hello IPsec 和 IKE SA</span><span class="sxs-lookup"><span data-stu-id="5b069-211">Show hello IPsec and IKE SA's</span></span>
    - <span data-ttu-id="5b069-212">"show crypto ipsec sa"</span><span class="sxs-lookup"><span data-stu-id="5b069-212">"show crypto ipsec sa"</span></span>
    - <span data-ttu-id="5b069-213">"show crypto ikev2 sa"</span><span class="sxs-lookup"><span data-stu-id="5b069-213">"show crypto ikev2 sa"</span></span>
2. <span data-ttu-id="5b069-214">輸入的偵錯模式-這可以取得非常累贅 hello 主控台上</span><span class="sxs-lookup"><span data-stu-id="5b069-214">Entering debug mode - this can get very noisy on hello console</span></span>
    - <span data-ttu-id="5b069-215">"debug crypto ikev2 platform <level>"</span><span class="sxs-lookup"><span data-stu-id="5b069-215">"debug crypto ikev2 platform <level>"</span></span>
    - <span data-ttu-id="5b069-216">"debug crypto ikev2 protocol <level>"</span><span class="sxs-lookup"><span data-stu-id="5b069-216">"debug crypto ikev2 protocol <level>"</span></span>
3. <span data-ttu-id="5b069-217">列出目前的組態</span><span class="sxs-lookup"><span data-stu-id="5b069-217">List current configurations</span></span>
    - <span data-ttu-id="5b069-218">「 顯示執行 」-顯示 hello hello 裝置; 上目前的組態您可以使用 hello 各種子命令 toolist 的特定部分 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="5b069-218">"show run" - shows hello current configurations on hello device; you can use hello various sub-commands toolist specific parts of hello configuration.</span></span> <span data-ttu-id="5b069-219">例如，"show run crypto"、"show run access-list"、"show run tunnel-group" 等。</span><span class="sxs-lookup"><span data-stu-id="5b069-219">E.g., "show run crypto", "show run access-list", "show run tunnel-group", etc.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5b069-220">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5b069-220">Next steps</span></span>
<span data-ttu-id="5b069-221">請參閱[跨單位和 VNet 對 VNet 連線設定主動-主動 VPN 閘道](vpn-gateway-activeactive-rm-powershell.md)步驟 tooconfigure 主動-主動跨單位和 VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="5b069-221">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps tooconfigure active-active cross-premises and VNet-to-VNet connections.</span></span>

