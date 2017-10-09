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
# <a name="about-cryptographic-requirements-and-azure-vpn-gateways"></a>關於密碼編譯需求和 Azure VPN 閘道

本文將討論如何設定 Azure VPN 閘道 toosatisfy 跨內部部署 S2S VPN 通道，在 Azure 中的 VNet 對 VNet 連線的密碼編譯需求。 

## <a name="about-ipsec-and-ike-policy-parameters-for-azure-vpn-gateways"></a>關於 Azure VPN 閘道的 IPsec 和 IKE 原則參數
IPsec 和 IKE 通訊協定標準支援各種不同的密碼編譯演算法的各種組合。 如果客戶未要求特定的密碼編譯演算法和參數組合，則 Azure VPN 閘道會使用一組預設的提案。 hello 預設原則設定的預設組態中選擇 toomaximize 與各種不同的協力廠商 VPN 裝置的互通性。 如此一來，hello 原則和提案徵求書的 hello 數目無法涵蓋所有可能組合，可以使用的密碼編譯演算法和金鑰長度。

hello Azure VPN 閘道列示 hello 文件中設定的預設原則：[關於 VPN 裝置與站對站 VPN 閘道連線的 IPsec/IKE 參數](vpn-gateway-about-vpn-devices.md)。

## <a name="cryptographic-requirements"></a>密碼編譯需求
需要特定密碼編譯演算法或參數的通訊，通常 toocompliance 或安全性需求，因為客戶現在可以設定他們的 Azure VPN 閘道 toouse 自訂 IPsec/IKE 原則與特定密碼編譯演算法和金鑰長度，而非 hello Azure 的預設原則集。

而客戶則可能需要 toospecify 用於 IKE，例如群組 14 （2048年位元）、 群組 24 （2048年位元 MODP 群組） 或 （橢圓 ECP 更強群組 toobe hello IKEv2 主要模式原則的 Azure VPN 閘道，例如利用只 Diffie-hellman 群組 2 （1024 位元）曲線群組） 256 個 384 位元 （群組 19 和群組 20 分別）。 類似的需求都適用於 tooIPsec 快速模式原則。

## <a name="custom-ipsecike-policy-with-azure-vpn-gateways"></a>自訂的 IPsec/IKE 原則與 Azure VPN 閘道
Azure VPN 閘道現在支援個別連線的自訂 IPsec/IKE 原則。 站對站或 VNet 對 VNet 連線，您可以選擇的密碼編譯演算法的特定組合讓您 IPsec 和 IKE 與 hello 需要索引鍵強度，hello 下列範例所示：

![ipsec-ike-policy](./media/vpn-gateway-about-compliance-crypto/ipsecikepolicy.png)

您可以建立的 IPsec/IKE 原則，並套用 tooa 新的或現有的連接。 

### <a name="workflow"></a>工作流程

1. 建立 hello 虛擬網路、 VPN 閘道或區域網路閘道連線拓撲的其他方式 toodocuments 中所述
2. 建立 IPsec/IKE 原則
3. 當您建立 S2S 或 VNet 對 VNet 連線時，您可以套用 hello 原則
4. 如果已經建立 hello 連線，您可以套用或更新 hello 原則 tooan 現有連線


## <a name="ipsecike-policy-faq"></a>IPsec/IKE 原則常見問題集

[!INCLUDE [vpn-gateway-ipsecikepolicy-faq-include](../../includes/vpn-gateway-ipsecikepolicy-faq-include.md)]


## <a name="next-steps"></a>後續步驟
如需為連線設定自訂 IPsec/IKE 原則的逐步指示，請參閱[設定 IPsec/IKE 原則](vpn-gateway-ipsecikepolicy-rm-powershell.md)。

另請參閱[連接多個以原則為基礎的 VPN 裝置](vpn-gateway-connect-multiple-policybased-rm-ps.md)toolearn 更多關於 hello UsePolicyBasedTrafficSelectors 選項。
