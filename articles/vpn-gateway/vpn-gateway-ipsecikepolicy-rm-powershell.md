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
ms.openlocfilehash: f8d2e29276efdec7071f2aa0d463b1abd64a5253
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ipsecike-policy-for-s2s-vpn-or-vnet-to-vnet-connections"></a><span data-ttu-id="5a6b3-103">設定 S2S VPN 或 VNet 對 VNet 連線的 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="5a6b3-103">Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections</span></span>

<span data-ttu-id="5a6b3-104">這篇文章會引導您 hello 步驟 tooconfigure 使用 hello Resource Manager 部署模型和 PowerShell 的站對站 VPN 或 VNet 對 VNet 連線的 IPsec/IKE 原則。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-104">This article walks you through hello steps tooconfigure IPsec/IKE policy for Site-to-Site VPN or VNet-to-VNet connections using hello Resource Manager deployment model and PowerShell.</span></span>

## <span data-ttu-id="5a6b3-105"><a name="about"></a>關於 Azure VPN 閘道的 IPsec 和 IKE 原則參數</span><span class="sxs-lookup"><span data-stu-id="5a6b3-105"><a name="about"></a>About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="5a6b3-106">IPsec 和 IKE 通訊協定標準支援各種不同的密碼編譯演算法的各種組合。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="5a6b3-107">請參閱太[有關密碼編譯需求和 Azure VPN 閘道](vpn-gateway-about-compliance-crypto.md)toosee 這如何可協助確保跨單位和 VNet 對 VNet 連線能力滿足您的相容性或安全性需求。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-107">Refer too[About cryptographic requirements and Azure VPN gateways](vpn-gateway-about-compliance-crypto.md) toosee how this can help ensuring cross-premises and VNet-to-VNet connectivity satisfy your compliance or security requirements.</span></span>

<span data-ttu-id="5a6b3-108">這篇文章會提供指示 toocreate 和設定 IPsec/IKE 原則並套用 tooa 新的或現有的連接：</span><span class="sxs-lookup"><span data-stu-id="5a6b3-108">This article provides instructions toocreate and configure an IPsec/IKE policy and apply tooa new or existing connection:</span></span>

* [<span data-ttu-id="5a6b3-109">組件 1-工作流程 toocreate 而且設定 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="5a6b3-109">Part 1 - Workflow toocreate and set IPsec/IKE policy</span></span>](#workflow)
* [<span data-ttu-id="5a6b3-110">第 2 部分 - 支援的密碼編譯演算法和金鑰長度</span><span class="sxs-lookup"><span data-stu-id="5a6b3-110">Part 2 - Supported cryptographic algorithms and key strengths</span></span>](#params)
* [<span data-ttu-id="5a6b3-111">第 3 部分 - 使用 IPsec/IKE 原則建立新的 S2S VPN 連線</span><span class="sxs-lookup"><span data-stu-id="5a6b3-111">Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>](#crossprem)
* [<span data-ttu-id="5a6b3-112">第 4 部分 - 使用 IPsec/IKE 原則建立新的 VNet 對 VNet 連線</span><span class="sxs-lookup"><span data-stu-id="5a6b3-112">Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>](#vnet2vnet)
* [<span data-ttu-id="5a6b3-113">第 5 部分 - 管理 (建立、新增、移除) 連線的 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="5a6b3-113">Part 5 - Manage (create, add, remove) IPsec/IKE policy for a connection</span></span>](#managepolicy)

> [!IMPORTANT]
> 1. <span data-ttu-id="5a6b3-114">請注意，IPsec/IKE 原則僅適用於下列閘道 Sku 的 hello:</span><span class="sxs-lookup"><span data-stu-id="5a6b3-114">Note that IPsec/IKE policy only works on hello following gateway SKUs:</span></span>
>    * <span data-ttu-id="5a6b3-115">***VpnGw1、VpnGw2、VpnGw3*** (路由式)</span><span class="sxs-lookup"><span data-stu-id="5a6b3-115">***VpnGw1, VpnGw2, VpnGw3*** (route-based)</span></span>
>    * <span data-ttu-id="5a6b3-116">***Standard*** 和 ***HighPerformance*** (路由式)</span><span class="sxs-lookup"><span data-stu-id="5a6b3-116">***Standard*** and ***HighPerformance*** (route-based)</span></span>
> 2. <span data-ttu-id="5a6b3-117">每個給定的連線只能指定***一個***原則組合。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-117">You can only specify ***one*** policy combination for a given connection.</span></span>
> 3. <span data-ttu-id="5a6b3-118">您必須同時對 IKE (主要模式) 和 IPsec (快速模式) 指定所有的演算法和參數。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-118">You must specify all algorithms and parameters for both IKE (Main Mode) and IPsec (Quick Mode).</span></span> <span data-ttu-id="5a6b3-119">系統不允許只指定一部分原則。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-119">Partial policy specification is not allowed.</span></span>
> 4. <span data-ttu-id="5a6b3-120">請洽詢您 tooensure hello 原則在內部部署 VPN 裝置支援的 VPN 裝置廠商規格。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-120">Consult with your VPN device vendor specifications tooensure hello policy is supported on your on-premises VPN devices.</span></span> <span data-ttu-id="5a6b3-121">S2S 或 VNet 對 VNet 連線無法建立是否 hello 原則不相容。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-121">S2S or VNet-to-VNet connections cannot establish if hello policies are incompatible.</span></span>

## <span data-ttu-id="5a6b3-122"><a name ="workflow"></a>組件 1-工作流程 toocreate 而且設定 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="5a6b3-122"><a name ="workflow"></a>Part 1 - Workflow toocreate and set IPsec/IKE policy</span></span>
<span data-ttu-id="5a6b3-123">本節將概述 hello 工作流程 toocreate 和 update IPsec/IKE 原則 S2S VPN 或 VNet 對 VNet 連線：</span><span class="sxs-lookup"><span data-stu-id="5a6b3-123">This section outlines hello workflow toocreate and update IPsec/IKE policy on a S2S VPN or VNet-to-VNet connection:</span></span>
1. <span data-ttu-id="5a6b3-124">建立虛擬網路和 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="5a6b3-124">Create a virtual network and a VPN gateway</span></span>
2. <span data-ttu-id="5a6b3-125">建立區域網路閘道以進行跨單位連線，或建立另一個虛擬網路和閘道以進行 VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-125">Create a local network gateway for cross premises connection, or another virtual network and gateway for VNet-to-VNet connection</span></span>
3. <span data-ttu-id="5a6b3-126">使用選取的演算法和參數建立 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="5a6b3-126">Create an IPsec/IKE policy with selected algorithms and parameters</span></span>
4. <span data-ttu-id="5a6b3-127">使用 hello IPsec/IKE 原則建立連線 （IPsec 或 VNet2VNet）</span><span class="sxs-lookup"><span data-stu-id="5a6b3-127">Create a connection (IPsec or VNet2VNet) with hello IPsec/IKE policy</span></span>
5. <span data-ttu-id="5a6b3-128">新增/更新/移除現有連線的 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="5a6b3-128">Add/update/remove an IPsec/IKE policy for an existing connection</span></span>

<span data-ttu-id="5a6b3-129">這篇文章中的 hello 指示可協助您安裝及設定 IPsec/IKE 原則 hello 圖表所示：</span><span class="sxs-lookup"><span data-stu-id="5a6b3-129">hello instructions in this article helps you set up and configure IPsec/IKE policies as shown in hello diagram:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)

## <span data-ttu-id="5a6b3-131"><a name ="params"></a>第 2 部分 - 支援的密碼編譯演算法和金鑰長度</span><span class="sxs-lookup"><span data-stu-id="5a6b3-131"><a name ="params"></a>Part 2 - Supported cryptographic algorithms & key strengths</span></span>

<span data-ttu-id="5a6b3-132">hello 下表列出支援的 hello 密碼編譯演算法和金鑰長度可設定 hello 客戶：</span><span class="sxs-lookup"><span data-stu-id="5a6b3-132">hello following table lists hello supported cryptographic algorithms and key strengths configurable by hello customers:</span></span>

| <span data-ttu-id="5a6b3-133">**IPsec/IKEv2**</span><span class="sxs-lookup"><span data-stu-id="5a6b3-133">**IPsec/IKEv2**</span></span>  | <span data-ttu-id="5a6b3-134">**選項**</span><span class="sxs-lookup"><span data-stu-id="5a6b3-134">**Options**</span></span>    |
| ---  | --- 
| <span data-ttu-id="5a6b3-135">IKEv2 加密</span><span class="sxs-lookup"><span data-stu-id="5a6b3-135">IKEv2 Encryption</span></span> | <span data-ttu-id="5a6b3-136">AES256、AES192、AES128、DES3、DES</span><span class="sxs-lookup"><span data-stu-id="5a6b3-136">AES256, AES192, AES128, DES3, DES</span></span>  
| <span data-ttu-id="5a6b3-137">IKEv2 完整性</span><span class="sxs-lookup"><span data-stu-id="5a6b3-137">IKEv2 Integrity</span></span>  | <span data-ttu-id="5a6b3-138">SHA384、SHA256、SHA1、MD5</span><span class="sxs-lookup"><span data-stu-id="5a6b3-138">SHA384, SHA256, SHA1, MD5</span></span>  |
| <span data-ttu-id="5a6b3-139">DH 群組</span><span class="sxs-lookup"><span data-stu-id="5a6b3-139">DH Group</span></span>         | <span data-ttu-id="5a6b3-140">DHGroup24、ECP384、ECP256、DHGroup14、DHGroup2048、DHGroup2、DHGroup1、無</span><span class="sxs-lookup"><span data-stu-id="5a6b3-140">DHGroup24, ECP384, ECP256, DHGroup14, DHGroup2048, DHGroup2, DHGroup1, None</span></span> |
| <span data-ttu-id="5a6b3-141">IPsec 加密</span><span class="sxs-lookup"><span data-stu-id="5a6b3-141">IPsec Encryption</span></span> | <span data-ttu-id="5a6b3-142">GCMAES256、GCMAES192、GCMAES128、AES256、AES192、AES128、DES3、DES、無</span><span class="sxs-lookup"><span data-stu-id="5a6b3-142">GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, None</span></span>    |
| <span data-ttu-id="5a6b3-143">IPsec 完整性</span><span class="sxs-lookup"><span data-stu-id="5a6b3-143">IPsec Integrity</span></span>  | <span data-ttu-id="5a6b3-144">GCMASE256、GCMAES192、GCMAES128、SHA256、SHA1、MD5</span><span class="sxs-lookup"><span data-stu-id="5a6b3-144">GCMASE256, GCMAES192, GCMAES128, SHA256, SHA1, MD5</span></span> |
| <span data-ttu-id="5a6b3-145">PFS 群組</span><span class="sxs-lookup"><span data-stu-id="5a6b3-145">PFS Group</span></span>        | <span data-ttu-id="5a6b3-146">PFS24、ECP384、ECP256、PFS2048、PFS2、PFS1、無</span><span class="sxs-lookup"><span data-stu-id="5a6b3-146">PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, None</span></span> 
| <span data-ttu-id="5a6b3-147">QM SA 存留期</span><span class="sxs-lookup"><span data-stu-id="5a6b3-147">QM SA Lifetime</span></span>   | <span data-ttu-id="5a6b3-148">(**選擇性**：如果未指定，即會使用預設值)</span><span class="sxs-lookup"><span data-stu-id="5a6b3-148">(**Optional**: default values are used if not specified)</span></span><br><span data-ttu-id="5a6b3-149">秒 (整數；**最小 300**/預設值 27000 秒)</span><span class="sxs-lookup"><span data-stu-id="5a6b3-149">Seconds (integer; **min. 300**/default 27000 seconds)</span></span><br><span data-ttu-id="5a6b3-150">KB 數 (整數；**最小 1024**/預設值 102400000 KB 數)</span><span class="sxs-lookup"><span data-stu-id="5a6b3-150">KBytes (integer; **min. 1024**/default 102400000 KBytes)</span></span>   |
| <span data-ttu-id="5a6b3-151">流量選取器</span><span class="sxs-lookup"><span data-stu-id="5a6b3-151">Traffic Selector</span></span> | <span data-ttu-id="5a6b3-152">UsePolicyBasedTrafficSelectors** ($True/$False；**選擇性**，如果未指定，即為預設的 $False)</span><span class="sxs-lookup"><span data-stu-id="5a6b3-152">UsePolicyBasedTrafficSelectors** ($True/$False; **Optional**, default $False if not specified)</span></span>    |
|  |  |

> [!IMPORTANT]
> 1. <span data-ttu-id="5a6b3-153">**如果 GCMAES 會用於 IPsec 加密演算法，您必須選取 hello IPsec 完整性; 相同的 GCMAES 演算法和金鑰長度例如，兩個使用 GCMAES128**</span><span class="sxs-lookup"><span data-stu-id="5a6b3-153">**If GCMAES is used as for IPsec Encryption algorithm, you must select hello same GCMAES algorithm and key length for IPsec Integrity; for example, using GCMAES128 for both**</span></span>
> 2. <span data-ttu-id="5a6b3-154">IKEv2 主要模式 SA 存留期會固定為 28,800 秒 hello Azure VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="5a6b3-154">IKEv2 Main Mode SA lifetime is fixed at 28,800 seconds on hello Azure VPN gateways</span></span>
> 3. <span data-ttu-id="5a6b3-155">設定"UsePolicyBasedTrafficSelectors 」 太 $True 的連接上會設定 hello Azure VPN 閘道 tooconnect toopolicy 型 VPN 防火牆在內部部署。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-155">Setting "UsePolicyBasedTrafficSelectors" too$True on a connection will configure hello Azure VPN gateway tooconnect toopolicy-based VPN firewall on premises.</span></span> <span data-ttu-id="5a6b3-156">如果您啟用 PolicyBasedTrafficSelectors，您需要的 tooensure VPN 裝置已定義從 hello Azure 虛擬網路的前置詞，您在內部部署網路 （區域網路閘道） 前置詞的所有組合的 hello 相符流量選取器而不是任何-到-any。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-156">If you enable PolicyBasedTrafficSelectors, you need tooensure your VPN device has hello matching traffic selectors defined with all combinations of your on-premises network (local network gateway) prefixes to/from hello Azure virtual network prefixes, instead of any-to-any.</span></span> <span data-ttu-id="5a6b3-157">例如，如果您在內部部署網路的前置詞為 10.1.0.0/16 和 10.2.0.0/16，而且您虛擬網路的前置詞為 192.168.0.0/16 和 172.16.0.0/16，您需要下列流量選取器 toospecify hello:</span><span class="sxs-lookup"><span data-stu-id="5a6b3-157">For example, if your on-premises network prefixes are 10.1.0.0/16 and 10.2.0.0/16, and your virtual network prefixes are 192.168.0.0/16 and 172.16.0.0/16, you need toospecify hello following traffic selectors:</span></span>
>    * <span data-ttu-id="5a6b3-158">10.1.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5a6b3-158">10.1.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="5a6b3-159">10.1.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5a6b3-159">10.1.0.0/16 <====> 172.16.0.0/16</span></span>
>    * <span data-ttu-id="5a6b3-160">10.2.0.0/16 <====> 192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5a6b3-160">10.2.0.0/16 <====> 192.168.0.0/16</span></span>
>    * <span data-ttu-id="5a6b3-161">10.2.0.0/16 <====> 172.16.0.0/16</span><span class="sxs-lookup"><span data-stu-id="5a6b3-161">10.2.0.0/16 <====> 172.16.0.0/16</span></span>

<span data-ttu-id="5a6b3-162">如需原則式流量選取器的詳細資訊，請參閱[連線多個內部部署原則式 VPN 裝置](vpn-gateway-connect-multiple-policybased-rm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-162">For more information regarding policy-based traffic selectors, see [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

<span data-ttu-id="5a6b3-163">下表將列出 hello hello 對應 hello 自訂原則所支援的 Diffie-hellman 群組：</span><span class="sxs-lookup"><span data-stu-id="5a6b3-163">hello following table lists hello corresponding Diffie-Hellman Groups supported by hello custom policy:</span></span>

| <span data-ttu-id="5a6b3-164">**Diffie-Hellman 群組**</span><span class="sxs-lookup"><span data-stu-id="5a6b3-164">**Diffie-Hellman Group**</span></span>  | <span data-ttu-id="5a6b3-165">**DHGroup**</span><span class="sxs-lookup"><span data-stu-id="5a6b3-165">**DHGroup**</span></span>              | <span data-ttu-id="5a6b3-166">**PFSGroup**</span><span class="sxs-lookup"><span data-stu-id="5a6b3-166">**PFSGroup**</span></span> | <span data-ttu-id="5a6b3-167">**金鑰長度**</span><span class="sxs-lookup"><span data-stu-id="5a6b3-167">**Key length**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5a6b3-168">1</span><span class="sxs-lookup"><span data-stu-id="5a6b3-168">1</span></span>                         | <span data-ttu-id="5a6b3-169">DHGroup1</span><span class="sxs-lookup"><span data-stu-id="5a6b3-169">DHGroup1</span></span>                 | <span data-ttu-id="5a6b3-170">PFS1</span><span class="sxs-lookup"><span data-stu-id="5a6b3-170">PFS1</span></span>         | <span data-ttu-id="5a6b3-171">768 位元 MODP</span><span class="sxs-lookup"><span data-stu-id="5a6b3-171">768-bit MODP</span></span>   |
| <span data-ttu-id="5a6b3-172">2</span><span class="sxs-lookup"><span data-stu-id="5a6b3-172">2</span></span>                         | <span data-ttu-id="5a6b3-173">DHGroup2</span><span class="sxs-lookup"><span data-stu-id="5a6b3-173">DHGroup2</span></span>                 | <span data-ttu-id="5a6b3-174">PFS2</span><span class="sxs-lookup"><span data-stu-id="5a6b3-174">PFS2</span></span>         | <span data-ttu-id="5a6b3-175">1024 位元 MODP</span><span class="sxs-lookup"><span data-stu-id="5a6b3-175">1024-bit MODP</span></span>  |
| <span data-ttu-id="5a6b3-176">14</span><span class="sxs-lookup"><span data-stu-id="5a6b3-176">14</span></span>                        | <span data-ttu-id="5a6b3-177">DHGroup14</span><span class="sxs-lookup"><span data-stu-id="5a6b3-177">DHGroup14</span></span><br><span data-ttu-id="5a6b3-178">DHGroup2048</span><span class="sxs-lookup"><span data-stu-id="5a6b3-178">DHGroup2048</span></span> | <span data-ttu-id="5a6b3-179">PFS2048</span><span class="sxs-lookup"><span data-stu-id="5a6b3-179">PFS2048</span></span>      | <span data-ttu-id="5a6b3-180">2048 位元 MODP</span><span class="sxs-lookup"><span data-stu-id="5a6b3-180">2048-bit MODP</span></span>  |
| <span data-ttu-id="5a6b3-181">19</span><span class="sxs-lookup"><span data-stu-id="5a6b3-181">19</span></span>                        | <span data-ttu-id="5a6b3-182">ECP256</span><span class="sxs-lookup"><span data-stu-id="5a6b3-182">ECP256</span></span>                   | <span data-ttu-id="5a6b3-183">ECP256</span><span class="sxs-lookup"><span data-stu-id="5a6b3-183">ECP256</span></span>       | <span data-ttu-id="5a6b3-184">256 位元 ECP</span><span class="sxs-lookup"><span data-stu-id="5a6b3-184">256-bit ECP</span></span>    |
| <span data-ttu-id="5a6b3-185">20</span><span class="sxs-lookup"><span data-stu-id="5a6b3-185">20</span></span>                        | <span data-ttu-id="5a6b3-186">ECP384</span><span class="sxs-lookup"><span data-stu-id="5a6b3-186">ECP384</span></span>                   | <span data-ttu-id="5a6b3-187">ECP284</span><span class="sxs-lookup"><span data-stu-id="5a6b3-187">ECP284</span></span>       | <span data-ttu-id="5a6b3-188">384 位元 ECP</span><span class="sxs-lookup"><span data-stu-id="5a6b3-188">384-bit ECP</span></span>    |
| <span data-ttu-id="5a6b3-189">24</span><span class="sxs-lookup"><span data-stu-id="5a6b3-189">24</span></span>                        | <span data-ttu-id="5a6b3-190">DHGroup24</span><span class="sxs-lookup"><span data-stu-id="5a6b3-190">DHGroup24</span></span>                | <span data-ttu-id="5a6b3-191">PFS24</span><span class="sxs-lookup"><span data-stu-id="5a6b3-191">PFS24</span></span>        | <span data-ttu-id="5a6b3-192">2048 位元 MODP</span><span class="sxs-lookup"><span data-stu-id="5a6b3-192">2048-bit MODP</span></span>  |

<span data-ttu-id="5a6b3-193">請參閱太[RFC3526](https://tools.ietf.org/html/rfc3526)和[RFC5114](https://tools.ietf.org/html/rfc5114)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-193">Refer too[RFC3526](https://tools.ietf.org/html/rfc3526) and [RFC5114](https://tools.ietf.org/html/rfc5114) for more details.</span></span>

## <span data-ttu-id="5a6b3-194"><a name ="crossprem"></a>第 3 部分 - 使用 IPsec/IKE 原則建立新的 S2S VPN 連線</span><span class="sxs-lookup"><span data-stu-id="5a6b3-194"><a name ="crossprem"></a>Part 3 - Create a new S2S VPN connection with IPsec/IKE policy</span></span>

<span data-ttu-id="5a6b3-195">本節將引導您完成建立 S2S VPN 連線的 IPsec/IKE 原則 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-195">This section walks you through hello steps of creating a S2S VPN connection with an IPsec/IKE policy.</span></span> <span data-ttu-id="5a6b3-196">hello 下列步驟建立 hello 連線 hello 圖表所示：</span><span class="sxs-lookup"><span data-stu-id="5a6b3-196">hello following steps create hello connection as shown in hello diagram:</span></span>

![s2s-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/s2spolicy.png)

<span data-ttu-id="5a6b3-198">如需建立 S2S VPN 連線的詳細逐步指示，請參閱[建立 S2S VPN 連線](vpn-gateway-create-site-to-site-rm-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-198">See [Create a S2S VPN connection](vpn-gateway-create-site-to-site-rm-powershell.md) for more detailed step-by-step instructions for creating a S2S VPN connection.</span></span>

### <span data-ttu-id="5a6b3-199"><a name="before"></a>開始之前</span><span class="sxs-lookup"><span data-stu-id="5a6b3-199"><a name="before"></a>Before you begin</span></span>

* <span data-ttu-id="5a6b3-200">請確認您有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-200">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="5a6b3-201">如果您還沒有 Azure 訂用帳戶，則可以啟用 [MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)或註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-201">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5a6b3-202">安裝 hello Azure 資源管理員 PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-202">Install hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="5a6b3-203">請參閱[Azure PowerShell 概觀](/powershell/azure/overview)如需安裝 hello PowerShell cmdlet 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-203">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <span data-ttu-id="5a6b3-204"><a name="createvnet1"></a>步驟 1-建立 hello 虛擬網路、 VPN 閘道與區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="5a6b3-204"><a name="createvnet1"></a>Step 1 - Create hello virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="5a6b3-205">1.宣告變數</span><span class="sxs-lookup"><span data-stu-id="5a6b3-205">1. Declare your variables</span></span>

<span data-ttu-id="5a6b3-206">對於此練習，我們一開始先宣告我們的變數。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-206">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="5a6b3-207">設定用於生產環境時，請以您自己是確定 tooreplace hello 值。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-207">Be sure tooreplace hello values with your own when configuring for production.</span></span>

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

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="5a6b3-208">2.連接 tooyour 訂用帳戶，並建立新的資源群組</span><span class="sxs-lookup"><span data-stu-id="5a6b3-208">2. Connect tooyour subscription and create a new resource group</span></span>

<span data-ttu-id="5a6b3-209">請確定切換 tooPowerShell 模式 toouse hello 資源管理員 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-209">Make sure you switch tooPowerShell mode toouse hello Resource Manager cmdlets.</span></span> <span data-ttu-id="5a6b3-210">如需詳細資訊，請參閱 [搭配使用 Windows PowerShell 與 Resource Manager](../powershell-azure-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-210">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="5a6b3-211">開啟 PowerShell 主控台並連接 tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-211">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="5a6b3-212">使用下列範例 toohelp 您連接的 hello:</span><span class="sxs-lookup"><span data-stu-id="5a6b3-212">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="5a6b3-213">3.建立 hello 虛擬網路、 VPN 閘道與區域網路閘道</span><span class="sxs-lookup"><span data-stu-id="5a6b3-213">3. Create hello virtual network, VPN gateway, and local network gateway</span></span>

<span data-ttu-id="5a6b3-214">hello 下列範例會建立 hello 虛擬網路，TestVNet1，三個的子網路與 hello VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-214">hello following sample creates hello virtual network, TestVNet1, with three subnets, and hello VPN gateway.</span></span> <span data-ttu-id="5a6b3-215">替代值時，務必一律將您的閘道子網路特定命名為 GatewaySubnet。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-215">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="5a6b3-216">如果您將其命名為其他名稱，閘道建立會失敗。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-216">If you name it something else, your gateway creation fails.</span></span>

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

### <span data-ttu-id="5a6b3-217"><a name="s2sconnection"></a>步驟 2 - 使用 IPsec/IKE 原則建立 S2S VPN 連線</span><span class="sxs-lookup"><span data-stu-id="5a6b3-217"><a name="s2sconnection"></a>Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="5a6b3-218">1.建立 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="5a6b3-218">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="5a6b3-219">下列範例指令碼的 hello 建立 IPsec/IKE 原則以 hello 下列演算法和參數：</span><span class="sxs-lookup"><span data-stu-id="5a6b3-219">hello following sample script creates an IPsec/IKE policy with hello following algorithms and parameters:</span></span>

* <span data-ttu-id="5a6b3-220">IKEv2：AES256、SHA384、DHGroup24</span><span class="sxs-lookup"><span data-stu-id="5a6b3-220">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="5a6b3-221">IPsec：AES256、SHA256、PFS24、SA 存留期 7200 秒和 2048KB</span><span class="sxs-lookup"><span data-stu-id="5a6b3-221">IPsec: AES256, SHA256, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

<span data-ttu-id="5a6b3-222">如果您使用 GCMAES ipsec 時，您必須使用 hello 相同 GCMAES 演算法和金鑰長度 IPsec 加密和完整性，例如：</span><span class="sxs-lookup"><span data-stu-id="5a6b3-222">If you use GCMAES for IPsec, you must use hello same GCMAES algorithm and key length for both IPsec encryption and integrity, for example:</span></span>

* <span data-ttu-id="5a6b3-223">IKEv2：AES256、SHA384、DHGroup24</span><span class="sxs-lookup"><span data-stu-id="5a6b3-223">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="5a6b3-224">IPsec：**GCMAES256、GCMAES256**、PFS24、SA 存留期 7200 秒和 2048KB</span><span class="sxs-lookup"><span data-stu-id="5a6b3-224">IPsec: **GCMAES256, GCMAES256**, PFS24, SA Lifetime 7200 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption GCMAES256 -IpsecIntegrity GCMAES256 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-hello-ipsecike-policy"></a><span data-ttu-id="5a6b3-225">2.建立 hello S2S VPN 連線以 hello IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="5a6b3-225">2. Create hello S2S VPN connection with hello IPsec/IKE policy</span></span>

<span data-ttu-id="5a6b3-226">建立 S2S VPN 連線並套用 hello 稍早建立的 IPsec/IKE 原則。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-226">Create an S2S VPN connection and apply hello IPsec/IKE policy created earlier.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="5a6b3-227">您可以選擇性地加入 「-UsePolicyBasedTrafficSelectors $True"toohello 連線 cmdlet tooenable Azure VPN 閘道 tooconnect toopolicy 型 VPN 裝置上建立內部部署，如上面所述。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-227">You can optionally add "-UsePolicyBasedTrafficSelectors $True" toohello create connection cmdlet tooenable Azure VPN gateway tooconnect toopolicy-based VPN devices on premises, as described above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a6b3-228">之後 IPsec/IKE 原則指定的連接上，將只會傳送或接受 hello 與指定的密碼編譯演算法和金鑰長度，在該特定的連接上的 IPsec/IKE 建議 hello Azure VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-228">Once an IPsec/IKE policy is specified on a connection, hello Azure VPN gateway will only send or accept hello IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="5a6b3-229">請確定在內部部署 VPN 裝置 hello 連接使用，或接受 hello 確切原則的組合，否則將不建立 hello S2S VPN 通道。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-229">Make sure your on-premises VPN device for hello connection uses or accepts hello exact policy combination, otherwise hello S2S VPN tunnel will not establish.</span></span>


## <span data-ttu-id="5a6b3-230"><a name ="vnet2vnet"></a>第 4 部分 - 使用 IPsec/IKE 原則建立新的 VNet 對 VNet 連線</span><span class="sxs-lookup"><span data-stu-id="5a6b3-230"><a name ="vnet2vnet"></a>Part 4 - Create a new VNet-to-VNet connection with IPsec/IKE policy</span></span>

<span data-ttu-id="5a6b3-231">建立 VNet 對 VNet 連線的 IPsec/IKE 原則的 hello 步驟是類似 toothat S2S VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-231">hello steps of creating a VNet-to-VNet connection with an IPsec/IKE policy are similar toothat of a S2S VPN connection.</span></span> <span data-ttu-id="5a6b3-232">hello 下列範例指令碼建立 hello 連線 hello 圖表所示：</span><span class="sxs-lookup"><span data-stu-id="5a6b3-232">hello following sample scripts create hello connection as shown in hello diagram:</span></span>

![v2v-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/v2vpolicy.png)

<span data-ttu-id="5a6b3-234">如需建立 VNet 對 VNet 連線的詳細步驟，請參閱[建立 VNet 對 VNet 連線](vpn-gateway-vnet-vnet-rm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-234">See [Create a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) for more detailed steps for creating a VNet-to-VNet connection.</span></span> <span data-ttu-id="5a6b3-235">您必須先完成[3 篇](#crossprem)toocreate 並設定 TestVNet1 hello VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-235">You must complete [Part 3](#crossprem) toocreate and configure TestVNet1 and hello VPN Gateway.</span></span>

### <span data-ttu-id="5a6b3-236"><a name="createvnet2"></a>步驟 1-建立 hello 第二個虛擬網路和 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="5a6b3-236"><a name="createvnet2"></a>Step 1 - Create hello second virtual network and VPN gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="5a6b3-237">1.宣告變數</span><span class="sxs-lookup"><span data-stu-id="5a6b3-237">1. Declare your variables</span></span>

<span data-ttu-id="5a6b3-238">為確定 tooreplace 以 hello 的 hello 值的 toouse 您的組態。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-238">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

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

#### <a name="2-create-hello-second-virtual-network-and-vpn-gateway-in-hello-new-resource-group"></a><span data-ttu-id="5a6b3-239">2.在 hello 新資源群組中建立 hello 第二個虛擬網路和 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="5a6b3-239">2. Create hello second virtual network and VPN gateway in hello new resource group</span></span>

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

### <a name="step-2---create-a-vnet-tovnet-connection-with-hello-ipsecike-policy"></a><span data-ttu-id="5a6b3-240">步驟 2-建立 VNet toVNet 連接以 hello IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="5a6b3-240">Step 2 - Create a VNet-toVNet connection with hello IPsec/IKE policy</span></span>

<span data-ttu-id="5a6b3-241">類似 toohello S2S VPN 連線，建立一個 IPsec/IKE 原則，然後套用 toopolicy toohello 新的連接。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-241">Similar toohello S2S VPN connection, create an IPsec/IKE policy then apply toopolicy toohello new connection.</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="5a6b3-242">1.建立 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="5a6b3-242">1. Create an IPsec/IKE policy</span></span>

<span data-ttu-id="5a6b3-243">下列範例指令碼的 hello 建立不同的 IPsec/IKE 原則以 hello 下列演算法和參數：</span><span class="sxs-lookup"><span data-stu-id="5a6b3-243">hello following sample script creates a different IPsec/IKE policy with hello following algorithms and parameters:</span></span>
* <span data-ttu-id="5a6b3-244">IKEv2：AES128、SHA1、DHGroup14</span><span class="sxs-lookup"><span data-stu-id="5a6b3-244">IKEv2: AES128, SHA1, DHGroup14</span></span>
* <span data-ttu-id="5a6b3-245">IPsec：GCMAES128、GCMAES128、PFS14、SA 存留期 7200 秒和 4096KB</span><span class="sxs-lookup"><span data-stu-id="5a6b3-245">IPsec: GCMAES128, GCMAES128, PFS14, SA Lifetime 7200 seconds & 4096KB</span></span>

```powershell
$ipsecpolicy2 = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup PFS14 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 4096
```

#### <a name="2-create-vnet-to-vnet-connections-with-hello-ipsecike-policy"></a><span data-ttu-id="5a6b3-246">2.建立 VNet 對 VNet 連線以 hello IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="5a6b3-246">2. Create VNet-to-VNet connections with hello IPsec/IKE policy</span></span>

<span data-ttu-id="5a6b3-247">建立 VNet 對 VNet 連線並套用您所建立的 hello IPsec/IKE 原則。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-247">Create a VNet-to-VNet connection and apply hello IPsec/IKE policy you created.</span></span> <span data-ttu-id="5a6b3-248">在此範例中，兩個閘道位於 hello 相同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-248">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="5a6b3-249">因此它可能 toocreate 而且設定與這兩個連線 hello hello 中相同的 IPsec/IKE 原則相同的 PowerShell 工作階段。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-249">So it is possible toocreate and configure both connections with hello same IPsec/IKE policy in hello same PowerShell session.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2  -ResourceGroupName $RG2

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -IpsecPolicies $ipsecpolicy2 -SharedKey 'AzureA1b2C3'
```

> [!IMPORTANT]
> <span data-ttu-id="5a6b3-250">之後 IPsec/IKE 原則指定的連接上，將只會傳送或接受 hello 與指定的密碼編譯演算法和金鑰長度，在該特定的連接上的 IPsec/IKE 建議 hello Azure VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-250">Once an IPsec/IKE policy is specified on a connection, hello Azure VPN gateway will only send or accept hello IPsec/IKE proposal with specified cryptographic algorithms and key strengths on that particular connection.</span></span> <span data-ttu-id="5a6b3-251">請確定 hello IPsec 原則的兩個連線都 hello 相同，否則將不建立 VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-251">Make sure hello IPsec policies for both connections are hello same, otherwise the VNet-to-VNet connection will not establish.</span></span>

<span data-ttu-id="5a6b3-252">完成這些步驟之後，hello 連接在幾分鐘的時間，而且您必須遵循網路拓樸 hello 開頭中所示的 hello:</span><span class="sxs-lookup"><span data-stu-id="5a6b3-252">After completing these steps, hello connection is established in a few minutes, and you will have hello following network topology as shown in hello beginning:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-ipsecikepolicy-rm-powershell/ipsecikepolicy.png)


## <span data-ttu-id="5a6b3-254"><a name ="managepolicy"></a>第 5 部分 - 更新連線的 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="5a6b3-254"><a name ="managepolicy"></a>Part 5 - Update IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="5a6b3-255">hello 最後一節將示範如何 toomanage 現有 S2S 或 VNet 對 VNet 連線的 IPsec/IKE 原則。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-255">hello last section shows you how toomanage IPsec/IKE policy for an existing S2S or VNet-to-VNet connection.</span></span> <span data-ttu-id="5a6b3-256">hello 練習下方會引導您完成下列作業的連接上的 hello:</span><span class="sxs-lookup"><span data-stu-id="5a6b3-256">hello exercise below walks you through hello following operations on a connection:</span></span>

1. <span data-ttu-id="5a6b3-257">顯示連線的 hello IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="5a6b3-257">Show hello IPsec/IKE policy of a connection</span></span>
2. <span data-ttu-id="5a6b3-258">加入或更新 hello IPsec/IKE 原則 tooa 連線</span><span class="sxs-lookup"><span data-stu-id="5a6b3-258">Add or update hello IPsec/IKE policy tooa connection</span></span>
3. <span data-ttu-id="5a6b3-259">從連線移除 hello IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="5a6b3-259">Remove hello IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="5a6b3-260">hello 相同的步驟套用 tooboth S2S 和 VNet 對 VNet 連線。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-260">hello same steps apply tooboth S2S and VNet-to-VNet connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a6b3-261">只有 Standard 和 HighPerformance 以路由為基礎的 VPN 閘道才支援 IPsec/IKE 原則。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-261">IPsec/IKE policy is supported on *Standard* and *HighPerformance* route-based VPN gateways only.</span></span> <span data-ttu-id="5a6b3-262">它不適用於 hello 基本閘道 SKU 或 hello 以原則為基礎的 VPN 閘道。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-262">It does not work on hello Basic gateway SKU or hello policy-based VPN gateway.</span></span>

#### <a name="1-show-hello-ipsecike-policy-of-a-connection"></a><span data-ttu-id="5a6b3-263">1.顯示連線的 hello IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="5a6b3-263">1. Show hello IPsec/IKE policy of a connection</span></span>

<span data-ttu-id="5a6b3-264">hello 下列範例顯示如何 tooget hello 在連接上設定的 IPsec/IKE 原則。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-264">hello following example shows how tooget hello IPsec/IKE policy configured on a connection.</span></span> <span data-ttu-id="5a6b3-265">hello 指令碼也會繼續從上述的 hello 練習。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-265">hello scripts also continue from hello exercises above.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="5a6b3-266">如果有任何 hello 最後一個命令會列出 hello hello 連接上設定目前 IPsec/IKE 原則。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-266">hello last command lists hello current IPsec/IKE policy configured on hello connection, if there is any.</span></span> <span data-ttu-id="5a6b3-267">下列範例輸出的 hello 是 hello 連接：</span><span class="sxs-lookup"><span data-stu-id="5a6b3-267">hello following sample output is for hello connection:</span></span>

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

<span data-ttu-id="5a6b3-268">如果未設定的 IPsec/IKE 原則，hello 命令 (PS > $connection6.policy) 取得傳回空白。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-268">If there is no IPsec/IKE policy configured, hello command (PS> $connection6.policy) gets an empty return.</span></span> <span data-ttu-id="5a6b3-269">它並不表示 IPsec/IKE hello 連接上未設定，但沒有自訂 IPsec/IKE 原則。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-269">It does not mean IPsec/IKE is not configured on hello connection, but that there is no custom IPsec/IKE policy.</span></span> <span data-ttu-id="5a6b3-270">hello 實際連接會使用您在內部部署 VPN 裝置和 hello Azure VPN 閘道之間進行交涉 hello 預設原則。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-270">hello actual connection uses hello default policy negotiated between your on-premises VPN device and hello Azure VPN gateway.</span></span>

#### <a name="2-add-or-update-an-ipsecike-policy-for-a-connection"></a><span data-ttu-id="5a6b3-271">2.新增或更新連線的 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="5a6b3-271">2. Add or update an IPsec/IKE policy for a connection</span></span>

<span data-ttu-id="5a6b3-272">hello 步驟 tooadd 新原則或更新現有的連接上的原則是 hello 相同： 建立新的原則，然後套用新原則 toohello 連線 hello。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-272">hello steps tooadd a new policy or update an existing policy on a connection are hello same: create a new policy then apply hello new policy toohello connection.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$newpolicy6   = New-AzureRmIpsecPolicy -IkeEncryption AES128 -IkeIntegrity SHA1 -DhGroup DHGroup14 -IpsecEncryption GCMAES128 -IpsecIntegrity GCMAES128 -PfsGroup None -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6
```

<span data-ttu-id="5a6b3-273">tooenable"UsePolicyBasedTrafficSelectors 」 時連接 tooan 內部以原則為基礎的 VPN 裝置，新增 hello"-UsePolicyBaseTrafficSelectors"參數 toohello cmdlet，或將其設定太 $False toodisable hello 選項：</span><span class="sxs-lookup"><span data-stu-id="5a6b3-273">tooenable "UsePolicyBasedTrafficSelectors" when connecting tooan on-premises policy-based VPN device, add hello "-UsePolicyBaseTrafficSelectors" parameter toohello cmdlet, or set it too$False toodisable hello option:</span></span>

```powershell
Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -IpsecPolicies $newpolicy6 -UsePolicyBasedTrafficSelectors $True
```

<span data-ttu-id="5a6b3-274">您可以取得 hello 連線一次 toocheck 如果 hello 原則更新。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-274">You can get hello connection again toocheck if hello policy is updated.</span></span>

```powershell
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
$connection6.IpsecPolicies
```

<span data-ttu-id="5a6b3-275">您應該會看到 hello hello 最後一行中，輸出 hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="5a6b3-275">You should see hello output from hello last line, as shown in hello following example:</span></span>

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

#### <a name="3-remove-an-ipsecike-policy-from-a-connection"></a><span data-ttu-id="5a6b3-276">3.移除連線的 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="5a6b3-276">3. Remove an IPsec/IKE policy from a connection</span></span>

<span data-ttu-id="5a6b3-277">一旦您從連線移除 hello 自訂原則，hello Azure VPN 閘道會還原後 toohello [IPsec/IKE 提案徵求書的預設清單](vpn-gateway-about-vpn-devices.md)並再次重新交涉，與您的內部部署 VPN 裝置。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-277">Once you remove hello custom policy from a connection, hello Azure VPN gateway reverts back toohello [default list of IPsec/IKE proposals](vpn-gateway-about-vpn-devices.md) and renegotiates again with your on-premises VPN device.</span></span>

```powershell
$RG1           = "TestPolicyRG1"
$Connection16  = "VNet1toSite6"
$connection6   = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

$currentpolicy = $connection6.IpsecPolicies[0]
$connection6.IpsecPolicies.Remove($currentpolicy)

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6
```

<span data-ttu-id="5a6b3-278">您可以使用 hello 相同的指令碼 toocheck 如果 hello 原則已經移除了 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-278">You can use hello same script toocheck if hello policy has been removed from hello connection.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a6b3-279">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5a6b3-279">Next steps</span></span>

<span data-ttu-id="5a6b3-280">如需以原則為基礎的流量選取器的詳細資訊，請參閱[連線多個內部部署以原則為基礎的 VPN 裝置](vpn-gateway-connect-multiple-policybased-rm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-280">See [Connect multiple on-premises policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) for more details regarding policy-based traffic selectors.</span></span>

<span data-ttu-id="5a6b3-281">一旦完成您的連線，您可以將虛擬機器 tooyour 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-281">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="5a6b3-282">請參閱 [建立網站的虛擬機器](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 以取得相關步驟。</span><span class="sxs-lookup"><span data-stu-id="5a6b3-282">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
