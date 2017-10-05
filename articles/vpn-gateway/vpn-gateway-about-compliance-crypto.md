---
title: "關於密碼編譯需求和 Azure VPN 閘道 | Microsoft Docs"
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
ms.openlocfilehash: c789e6c278fc0c58c64f5d96e57f94aee5a6cefc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a><span data-ttu-id="0cc7d-103">關於密碼編譯需求和 Azure VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="0cc7d-103">About cryptographic requirements and Azure VPN gateways</span></span>

<span data-ttu-id="0cc7d-104">此文章說明如何針對 Azure 內的跨單位 S2S VPN 通道和 VNet 對 VNet 連線，設定 Azure VPN 閘道，以滿足您的密碼編譯需求。</span><span class="sxs-lookup"><span data-stu-id="0cc7d-104">This article discusses how you can configure Azure VPN gateways to satisfy your cryptographic requirements for both cross-premises S2S VPN tunnels and VNet-to-VNet connections within Azure.</span></span> 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a><span data-ttu-id="0cc7d-105">關於 Azure VPN 閘道的 IPsec 和 IKE 原則參數</span><span class="sxs-lookup"><span data-stu-id="0cc7d-105">About IPsec and IKE policy parameters for Azure VPN gateways</span></span>
<span data-ttu-id="0cc7d-106">IPsec 和 IKE 通訊協定標準支援各種不同的密碼編譯演算法的各種組合。</span><span class="sxs-lookup"><span data-stu-id="0cc7d-106">IPsec and IKE protocol standard supports a wide range of cryptographic algorithms in various combinations.</span></span> <span data-ttu-id="0cc7d-107">如果客戶未要求特定的密碼編譯演算法和參數組合，則 Azure VPN 閘道會使用一組預設的提案。</span><span class="sxs-lookup"><span data-stu-id="0cc7d-107">If customers do not request a specific combination of cryptographic algorithms and parameters, Azure VPN gateways use a set of default proposals.</span></span> <span data-ttu-id="0cc7d-108">選擇預設原則集的用意，是要在預設設定中將與各種協力廠商 VPN 裝置的互通性最大化。</span><span class="sxs-lookup"><span data-stu-id="0cc7d-108">The default policy sets were chosen to maximize interoperability with a wide range of third-party VPN devices in default configurations.</span></span> <span data-ttu-id="0cc7d-109">如此一來，原則和提案數目就無法涵蓋所有可用的密碼編譯演算法和金鑰長度組合。</span><span class="sxs-lookup"><span data-stu-id="0cc7d-109">As a result, the policies and the number of proposals cannot cover all possible combinations of available cryptographic algorithms and key strengths.</span></span>

<span data-ttu-id="0cc7d-110">下列文件列出 Azure VPN 閘道的預設原則集：[關於 VPN 裝置和站對站 VPN 閘道連線的 IPsec/IKE 參數](vpn-gateway-about-vpn-devices.md)。</span><span class="sxs-lookup"><span data-stu-id="0cc7d-110">The default policy set for Azure VPN gateway is listed in the document: [About VPN devices and IPsec/IKE parameters for Site-to-Site VPN Gateway connections](vpn-gateway-about-vpn-devices.md).</span></span>

## <a name="cryptographic-requirements"></a><span data-ttu-id="0cc7d-111">密碼編譯需求</span><span class="sxs-lookup"><span data-stu-id="0cc7d-111">Cryptographic requirements</span></span>
<span data-ttu-id="0cc7d-112">針對需要特定密碼編譯演算法或參數的通訊 (通常是基於相容性或安全性需求的原因)，客戶現在可以自行設定 Azure VPN 閘道，以搭配使用自訂的 IPsec/IKE 原則和特定的密碼編譯演算法和金鑰長度，而不使用 Azure 的預設原則集。</span><span class="sxs-lookup"><span data-stu-id="0cc7d-112">For communications that require specific cryptographic algorithms or parameters, typically due to compliance or security requirements, customers can now configure their Azure VPN gateways to use a custom IPsec/IKE policy with specific cryptographic algorithms and key strengths, rather than the Azure default policy sets.</span></span>

<span data-ttu-id="0cc7d-113">例如，Azure VPN 閘道的 IKEv2 主要模式原則僅使用 Diffie-Hellman 群組 2 (1024 位元)，但客戶可能需要指定更強的群組以用於 IKE，例如群組 14 (2048 位元)、群組 24 (2048 位元 MODP 群組) 或 ECP (橢圓曲線群組) 256 或 384 位元 (分別為群組 19 和群組 20)。</span><span class="sxs-lookup"><span data-stu-id="0cc7d-113">For example, the IKEv2 main mode policies for Azure VPN gateways utilize only Diffie-Hellman Group 2 (1024 bits), whereas customers may need to specify stronger groups to be used in IKE, such as Group 14 (2048-bit), Group 24 (2048-bit MODP Group), or ECP (elliptic curve groups) 256 or 384 bit (Group 19 and Group 20, respectively).</span></span> <span data-ttu-id="0cc7d-114">類似的需求亦適用於 IPsec 快速模式原則。</span><span class="sxs-lookup"><span data-stu-id="0cc7d-114">Similar requirements apply to IPsec quick mode policies as well.</span></span>

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a><span data-ttu-id="0cc7d-115">自訂的 IPsec/IKE 原則與 Azure VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="0cc7d-115">Custom IPsec/IKE policy with Azure VPN gateways</span></span>
<span data-ttu-id="0cc7d-116">Azure VPN 閘道現在支援個別連線的自訂 IPsec/IKE 原則。</span><span class="sxs-lookup"><span data-stu-id="0cc7d-116">Azure VPN gateways now support per-connection, custom IPsec/IKE policy.</span></span> <span data-ttu-id="0cc7d-117">針對站對站或 VNet 對 VNet 連線，您可以針對 IPsec 和 IKE 選擇特定的密碼編譯演算法組合，搭配所需的金鑰強度，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="0cc7d-117">For a Site-to-Site or VNet-to-VNet connection, you can choose a specific combination of cryptographic algorithms for IPsec and IKE with the desired key strength, as shown in the following example:</span></span>

![ipsec-ike-policy](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

<span data-ttu-id="0cc7d-119">您可以建立 IPsec/IKE 原則，並將其套用至新連線或現有連線。</span><span class="sxs-lookup"><span data-stu-id="0cc7d-119">You can create an IPsec/IKE policy and apply to a new or existing connection.</span></span> 

### <a name="workflow"></a><span data-ttu-id="0cc7d-120">工作流程</span><span class="sxs-lookup"><span data-stu-id="0cc7d-120">Workflow</span></span>

1. <span data-ttu-id="0cc7d-121">按照其他使用說明文件所述，依據連線的拓撲來建立虛擬網路、VPN 閘道或區域網路閘道。</span><span class="sxs-lookup"><span data-stu-id="0cc7d-121">Create the virtual networks, VPN gateways, or local network gateways for your connectivity topology as described in other how-to documents</span></span>
2. <span data-ttu-id="0cc7d-122">建立 IPsec/IKE 原則</span><span class="sxs-lookup"><span data-stu-id="0cc7d-122">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="0cc7d-123">您可以在建立 S2S 或 VNet 對 VNet 連線時套用原則。</span><span class="sxs-lookup"><span data-stu-id="0cc7d-123">You can apply the policy when you create a S2S or VNet-to-VNet connection</span></span>
4. <span data-ttu-id="0cc7d-124">如果已經建立連線，您可以將原則套用至現有連線或將其更新。</span><span class="sxs-lookup"><span data-stu-id="0cc7d-124">If the connection is already created, you can apply or update the policy to an existing connection</span></span>


## <a name="ipsecike-policy-faq"></a><span data-ttu-id="0cc7d-125">IPsec/IKE 原則常見問題集</span><span class="sxs-lookup"><span data-stu-id="0cc7d-125">IPsec/IKE policy FAQ</span></span>

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a><span data-ttu-id="0cc7d-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0cc7d-126">Next steps</span></span>
<span data-ttu-id="0cc7d-127">如需為連線設定自訂 IPsec/IKE 原則的逐步指示，請參閱[設定 IPsec/IKE 原則](vpn-gateway-ipsecikepolicy-rm-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="0cc7d-127">See [Configure IPsec/IKE policy](vpn-gateway-ipsecikepolicy-rm-powershell.md) for step-by-step instructions on configuring custom IPsec/IKE policy on a connection.</span></span>

<span data-ttu-id="0cc7d-128">另請參閱[連線多個原則型 VPN 裝置](vpn-gateway-connect-multiple-policybased-rm-ps.md)，以深入了解 UsePolicyBasedTrafficSelectors 選項。</span><span class="sxs-lookup"><span data-stu-id="0cc7d-128">See also [Connect multiple policy-based VPN devices](vpn-gateway-connect-multiple-policybased-rm-ps.md) to learn more about the UsePolicyBasedTrafficSelectors option.</span></span>