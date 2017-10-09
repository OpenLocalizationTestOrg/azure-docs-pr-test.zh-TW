---
title: "aaaAbout 密碼編譯需求與 Azure VPN 閘道 |Microsoft 文件"
description: "本文說明密碼編譯需求與 Azure VPN 閘道。"
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
ms.date: 05/22/2017
ms.author: yushwang
ms.openlocfilehash: af5f14d66beeea5316218f9788c4ad7876826162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a><span data-ttu-id="5a0bd-103">關於密碼編譯需求和 Azure VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="5a0bd-103">About cryptographic requirements and Azure VPN gateways</span></span>

<span data-ttu-id="5a0bd-104">本文將討論如何設定 Azure VPN 閘道 toosatisfy 跨內部部署 S2S VPN 通道，在 Azure 中的 VNet 對 VNet 連線的密碼編譯需求。</span><span class="sxs-lookup"><span data-stu-id="5a0bd-104">This article discusses how you can configure Azure VPN gateways toosatisfy your cryptographic requirements for both cross-premises S2S VPN tunnels and VNet-to-VNet connections within Azure.</span></span> 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a><span data-ttu-id="5a0bd-105">關於 Azure VPN 閘道的 IPsec 和 IKE 原則參數</span><span class="sxs-lookup"><span data-stu-id="5a0bd-105">About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="5a0bd-106">IPsec 和 IKE 通訊協定標準支援各種不同的密碼編譯演算法的各種組合。</span><span class="sxs-lookup"><span data-stu-id="5a0bd-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="5a0bd-107">如果客戶未要求特定的密碼編譯演算法和參數組合，則 Azure VPN 閘道會使用一組預設的提案。</span><span class="sxs-lookup"><span data-stu-id="5a0bd-107">If customers do not request a specific combination of cryptographic algorithms and parameters, Azure VPN gateways use a set of default proposals.</span></span> <span data-ttu-id="5a0bd-108">hello 預設原則設定的預設組態中選擇 toomaximize 與各種不同的協力廠商 VPN 裝置的互通性。</span><span class="sxs-lookup"><span data-stu-id="5a0bd-108">hello default policy sets were chosen toomaximize interoperability with a wide range of third-party VPN devices in default configurations.</span></span> <span data-ttu-id="5a0bd-109">如此一來，hello 原則和提案徵求書的 hello 數目無法涵蓋所有可能組合，可以使用的密碼編譯演算法和金鑰長度。</span><span class="sxs-lookup"><span data-stu-id="5a0bd-109">As a result, hello policies and hello number of proposals cannot cover all possible combinations of available cryptographic algorithms and key strengths.</span></span>

<span data-ttu-id="5a0bd-110">hello Azure VPN 閘道列示 hello 文件中設定的預設原則：[關於 VPN 裝置與站對站 VPN 閘道連線的 IPsec/IKE 參數](vpn-gateway-about-vpn-devices.md)。</span><span class="sxs-lookup"><span data-stu-id="5a0bd-110">hello default policy set for Azure VPN gateway is listed in hello document: [About VPN devices and IPsec/IKE parameters for Site-to-Site VPN Gateway connections](vpn-gateway-about-vpn-devices.md).</span></span>

## <a name="cryptographic-requirements"></a><span data-ttu-id="5a0bd-111">密碼編譯需求</span><span class="sxs-lookup"><span data-stu-id="5a0bd-111">Cryptographic requirements</span></span>
<span data-ttu-id="5a0bd-112">需要特定密碼編譯演算法或參數的通訊，通常 toocompliance 或安全性需求，因為客戶現在可以設定他們的 Azure VPN 閘道 toouse 自訂 IPsec/IKE 原則與特定密碼編譯演算法和金鑰長度，而非 hello Azure 的預設原則集。</span><span class="sxs-lookup"><span data-stu-id="5a0bd-112">For communications that require specific cryptographic algorithms or parameters, typically due toocompliance or security requirements, customers can now configure their Azure VPN gateways toouse a custom IPsec/IKE policy with specific cryptographic algorithms and key strengths, rather than hello Azure default policy sets.</span></span>

<span data-ttu-id="5a0bd-113">而客戶則可能需要 toospecify 用於 IKE，例如群組 14 （2048年位元）、 群組 24 （2048年位元 MODP 群組） 或 （橢圓 ECP 更強群組 toobe hello IKEv2 主要模式原則的 Azure VPN 閘道，例如利用只 Diffie-hellman 群組 2 （1024 位元）曲線群組） 256 個 384 位元 （群組 19 和群組 20 分別）。</span><span class="sxs-lookup"><span data-stu-id="5a0bd-113">For example, hello IKEv2 main mode policies for Azure VPN gateways utilize only Diffie-Hellman Group 2 (1024 bits), whereas customers may need toospecify stronger groups toobe used in IKE, such as Group 14 (2048-bit), Group 24 (2048-bit MODP Group), or ECP (elliptic curve groups) 256 or 384 bit (Group 19 and Group 20, respectively).</span></span> <span data-ttu-id="5a0bd-114">類似的需求都適用於 tooIPsec 快速模式原則。</span><span class="sxs-lookup"><span data-stu-id="5a0bd-114">Similar requirements apply tooIPsec quick mode policies as well.</span></span>

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a><span data-ttu-id="5a0bd-115">自訂的 IPsec/IKE 原則與 Azure VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="5a0bd-115">Custom IPsec/IKE policy with Azure VPN gateways</span></span>
<span data-ttu-id="5a0bd-116">Azure VPN 閘道現在支援個別連線的自訂 IPsec/IKE 原則。</span><span class="sxs-lookup"><span data-stu-id="5a0bd-116">Azure VPN gateways now support per-connection, custom IPsec/IKE policy.</span></span> <span data-ttu-id="5a0bd-117">站對站或 VNet 對 VNet 連線，您可以選擇的密碼編譯演算法的特定組合讓您 IPsec 和 IKE 與 hello 需要索引鍵強度，hello 下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="5a0bd-117">For a Site-to-Site or VNet-to-VNet connection, you can choose a specific combination of cryptographic algorithms for IPsec and IKE with hello desired key strength, as shown in hello following example:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

<span data-ttu-id="5a0bd-119">您可以建立的 IPsec/IKE 原則，並套用 tooa 新的或現有的連接。</span><span class="sxs-lookup"><span data-stu-id="5a0bd-119">You can create an IPsec/IKE policy and apply tooa new or existing connection.</span></span> 

### <a name="workflow"></a><span data-ttu-id="5a0bd-120">工作流程</span><span class="sxs-lookup"><span data-stu-id="5a0bd-120">Workflow</span></span>

1. <span data-ttu-id="5a0bd-121">建立 hello 虛擬網路、 VPN 閘道或區域網路閘道連線拓撲的其他方式 toodocuments 中所述</span><span class="sxs-lookup"><span data-stu-id="5a0bd-121">Create hello virtual networks, VPN gateways, or local network gateways for your connectivity topology as described in other how-toodocuments</span></span>
2. <span data-ttu-id="5a0bd-122">建立 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="5a0bd-122">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="5a0bd-123">當您建立 S2S 或 VNet 對 VNet 連線時，您可以套用 hello 原則</span><span class="sxs-lookup"><span data-stu-id="5a0bd-123">You can apply hello policy when you create a S2S or VNet-to-VNet connection</span></span>
4. <span data-ttu-id="5a0bd-124">如果已經建立 hello 連線，您可以套用或更新 hello 原則 tooan 現有連線</span><span class="sxs-lookup"><span data-stu-id="5a0bd-124">If hello connection is already created, you can apply or update hello policy tooan existing connection</span></span>


## <a name="ipsecike-policy-faq"></a><span data-ttu-id="5a0bd-125">IPsec/IKE 原則常見問題集</span><span class="sxs-lookup"><span data-stu-id="5a0bd-125">IPsec/IKE policy FAQ</span></span>

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a><span data-ttu-id="5a0bd-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5a0bd-126">Next steps</span></span>
<span data-ttu-id="5a0bd-127">如需為連線設定自訂 IPsec/IKE 原則的逐步指示，請參閱[設定 IPsec/IKE 原則](vpn-gateway-ipsecikepolicy-rm-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="5a0bd-127">See [Configure IPsec/IKE policy](vpn-gateway-ipsecikepolicy-rm-powershell.md) for step-by-step instructions on configuring custom IPsec/IKE policy on a connection.</span></span>

<span data-ttu-id="5a0bd-128">另請參閱[連接多個以原則為基礎的 VPN 裝置](vpn-gateway-connect-multiple-policybased-rm-ps.md)toolearn 更多關於 hello UsePolicyBasedTrafficSelectors 選項。</span><span class="sxs-lookup"><span data-stu-id="5a0bd-128">See also [Connect multiple policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) toolearn more about hello UsePolicyBasedTrafficSelectors option.</span></span>
