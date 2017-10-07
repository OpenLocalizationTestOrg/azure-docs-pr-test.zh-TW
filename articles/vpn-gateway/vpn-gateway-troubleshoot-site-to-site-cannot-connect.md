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
# <a name="troubleshooting-an-azure-site-to-site-vpn-connection-cannot-connect-and-stops-working"></a>疑難排解：Azure 站對站 VPN 連線無法連線並停止運作

您設定站對站 VPN 連接內部部署網路與 Azure 虛擬網路之間之後，hello VPN 連線突然停止運作，而且無法重新連接。 本文章提供疑難排解步驟 toohelp 解決這個問題。 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a>疑難排解步驟

tooresolve hello 問題，請先嘗試過[重設 hello Azure VPN 閘道](vpn-gateway-resetgw-classic.md)並重設 hello 在內部部署 VPN 裝置 hello 通道。 如果 hello 問題持續發生，請遵循這些步驟 tooidentify hello 問題的原因 hello。

### <a name="prerequisite-step"></a>必要步驟

請檢查 hello hello Azure VPN 閘道類型。

1. 移 toohello [Azure 入口網站](https://portal.azure.com)。

2. 檢查 hello**概觀**hello hello 類型資訊的 VPN 閘道的頁面。
    
    ![Hello 閘道的概觀](media\vpn-gateway-troubleshoot-site-to-site-cannot-connect\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a>步驟 1. 檢查是否已驗證 hello 在內部部署 VPN 裝置

1. 檢查您是否使用[經過驗證的 VPN 裝置和作業系統版本](vpn-gateway-about-vpn-devices.md#devicetable)。 如果 hello 裝置不是已驗證的 VPN 裝置，您可能必須 toocontact hello 裝置製造商 toosee，如有相容性問題。

2. 請確定已正確設定該 hello VPN 裝置。 如需詳細資訊，請參閱[編輯裝置組態範例](/vpn-gateway-about-vpn-devices.md#editing)。

### <a name="step-2-verify-hello-shared-key"></a>步驟 2. 確認 hello 共用的金鑰

比較 hello 在內部部署 VPN 裝置 toohello Azure 虛擬網路 VPN toomake 確定 hello 索引鍵相符的 hello 共用的金鑰。 

tooview hello 共用的金鑰 hello Azure VPN 連線，使用其中一種 hello 下列方法：

**Azure 入口網站**

1. 移 toohello VPN 閘道站對站連線，您所建立。

2. 在 hello**設定**區段中，按一下**共用金鑰**。
    
    ![共用金鑰](media/vpn-gateway-troubleshoot-site-to-site-cannot-connect/sharedkey.png)

**Azure PowerShell**

Hello Azure Resource Manager 部署模型：

    Get-AzureRmVirtualNetworkGatewayConnectionSharedKey -Name <Connection name> -ResourceGroupName <Resource group name>

Hello 傳統部署模型：

    Get-AzureVNetGatewayKey -VNetName -LocalNetworkSiteName

### <a name="step-3-verify-hello-vpn-peer-ips"></a>步驟 3. 確認 hello VPN 對等 Ip

-   hello IP 定義在 hello**本機網路閘道**在 Azure 中的物件應該符合 hello 在內部部署裝置的 IP。
-   hello Azure 閘道 IP 定義 hello 上所設定內部部署裝置應符合 hello Azure 閘道 IP。

### <a name="step-4-check-udr-and-nsgs-on-hello-gateway-subnet"></a>步驟 4. 檢查 UDR 和 Nsg hello 閘道子網路

檢查和移除 hello 閘道子網路上的使用者定義路由 (UDR) 或網路安全性群組 (Nsg)，然後測試 hello 結果。 如果 hello 問題已經解決，驗證 hello UDR 或 NSG 套用的設定。

### <a name="step-5-check-hello-on-premises-vpn-device-external-interface-address"></a>步驟 5。 核取 hello 內部部署 VPN 裝置的外部介面位址

- 如果 hello hello VPN 裝置的網際網路對向的 IP 位址包含在 hello**區域網路**定義在 Azure 中，您可能會遇到偶發的連線中斷。
- hello 裝置的外部介面必須直接在 hello 網際網路上。 應該沒有網路位址轉譯 」 或 「 hello 網際網路與 hello 裝置之間的防火牆。
- tooconfigure 防火牆群集 toohave 虛擬 IP，您必須中斷 hello 叢集，並公開 （expose） hello VPN 應用裝置直接 tooa 公用介面該 hello 閘道可與互動。

### <a name="step-6-verify-that-hello-subnets-match-exactly-azure-policy-based-gateways"></a>步驟 6. 確認 hello 子網路完全相符 （Azure 以原則為基礎的閘道）

-   確認 hello Azure 虛擬網路與內部定義 hello Azure 虛擬網路之間的完全符合 hello 子網路。
-   請確認 hello 子網路相符完全之間 hello**本機網路閘道**和內部部署的 hello 與內部網路定義。

### <a name="step-7-verify-hello-azure-gateway-health-probe"></a>步驟 7. 確認 hello Azure 閘道健全狀況探查

1. 移 toohello[健全狀況探查](https://&lt;YourVirtualNetworkGatewayIP&gt;:8081/healthprobe)。

2. 按一下瀏覽 hello 憑證警告。
3. 如果您收到的回應，hello VPN 閘道會被視為狀況良好。 如果您沒有收到回應，hello 閘道可能不是狀況良好或 NSG hello 閘道子網路上的造成 hello 問題。 下列文字的 hello 是範例回應：

    &lt;?xml version="1.0"?> <string xmlns="http://schemas.microsoft.com/2003/10/Serialization/">主要執行個體: GatewayTenantWorker_IN_1 GatewayTenantVersion: 14.7.24.6</string&gt;

### <a name="step-8-check-whether-hello-on-premises-vpn-device-has-hello-perfect-forward-secrecy-feature-enabled"></a>步驟 8。 檢查是否 hello 內部部署 VPN 裝置已啟用的 hello 完整轉寄密碼功能

hello 完整轉寄密碼功能可能會造成中斷連線問題。 Hello VPN 裝置已啟用完整轉寄密碼，如果停用 hello 功能。 然後更新 hello VPN 閘道 IPsec 原則。

## <a name="next-steps"></a>後續步驟

-   [設定站對站連線 tooa 虛擬網路](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
-   [設定站對站 VPN 連線的 IPsec/IKE 原則](vpn-gateway-ipsecikepolicy-rm-powershell.md)
