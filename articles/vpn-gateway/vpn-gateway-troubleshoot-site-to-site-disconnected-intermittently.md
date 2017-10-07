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
# <a name="troubleshooting-azure-site-to-site-vpn-disconnects-intermittently"></a>疑難排解：Azure 站對站 VPN 間歇性中斷

您可能會遇到新的或現有的 Microsoft Azure 點對站 VPN 連線可能會不穩定或中斷定期的 hello 問題。 本文章提供疑難排解步驟 toohelp 您識別及解決 hello hello 問題原因。 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-steps"></a>疑難排解步驟

### <a name="prerequisite-step"></a>必要步驟

Azure 虛擬網路閘道的核取 hello 類型：

1. 跳過[Azure 入口網站](https://portal.azure.com)。
2. 檢查 hello**概觀**hello hello 型別資訊的虛擬網路閘道的頁面。
    
    ![hello 閘道的 hello 概觀](media\vpn-gateway-troubleshoot-site-to-site-disconnected-intermittently\gatewayoverview.png)

### <a name="step-1-check-whether-hello-on-premises-vpn-device-is-validated"></a>步驟 1 檢查是否 hello 內部部署 VPN 裝置會進行驗證

1. 檢查您是否使用[經過驗證的 VPN 裝置和作業系統版本](vpn-gateway-about-vpn-devices.md#devicetable)。 如果 hello VPN 裝置未經過驗證，您可能需要 toocontact hello 裝置製造商 toosee，如果有任何相容性問題。
2. 請確定已正確設定該 hello VPN 裝置。 如需詳細資訊，請參閱[編輯裝置組態範例](vpn-gateway-about-vpn-devices.md#editing)。

### <a name="step-2-check-hello-security-association-settingsfor-policy-based-azure-virtual-network-gateways"></a>步驟 2 檢查 hello （適用於以原則為基礎的 Azure 虛擬網路閘道） 的安全性關聯設定

1. 請確定該 hello 虛擬網路，子網路和範圍中 hello**區域網路閘道**Microsoft Azure 中的定義會與 hello hello 在內部部署 VPN 裝置上的設定相同。
2. 請確認該 hello 安全性關聯的設定相符。

### <a name="step-3-check-for-user-defined-routes-or-network-security-groups-on-gateway-subnet"></a>步驟 3：檢查閘道子網路上使用者定義的路由或網路安全性群組

Hello 閘道子網路的使用者定義路由可能會限制一些流量，並允許其他流量。 這使得出現 hello VPN 連線的一些流量不可靠且適用於其他人。 

### <a name="step-4-check-hello-one-vpn-tunnel-per-subnet-pair-setting-for-policy-based-virtual-network-gateways"></a>步驟 4 核取 hello"一個 VPN 通道每組子網路 」 設定 （適用於以原則為基礎的虛擬網路閘道）

請確定該 hello 內部部署 VPN 裝置設定 toohave**一個每組子網路的 VPN 通道**以原則為基礎的虛擬網路閘道。

### <a name="step-5-check-for-security-association-limitation-for-policy-based-virtual-network-gateways"></a>步驟 5：檢查安全性關聯限制 (適用於原則式虛擬網路閘道)

hello 以原則為基礎的虛擬網路閘道的上限為 200 的子網路的安全性關聯組。 如果 Azure 虛擬網路子網路的 hello 數目乘以時間 hello 的本機子網路的數字會大於 200，您會看到偶爾中斷連線的子網路。

### <a name="step-6-check-on-premises-vpn-device-external-interface-address"></a>步驟 6：檢查內部部署 VPN 裝置外部介面位址

- 如果 hello 網際網路對向 hello VPN 裝置 IP 位址會包含在 hello**區域網路閘道**定義在 Azure 中，您可能會遇到偶發的連線中斷。
- hello 裝置的外部介面必須直接在 hello 網際網路上。 應該沒有網路位址轉譯 (NAT) 或網際網路 hello 與 hello 裝置之間的防火牆。
-  如果您設定防火牆叢集 toohave 虛擬 IP，您必須中斷 hello 叢集，而且可與互動 tooa hello 閘道的公用介面直接公開 hello VPN 應用裝置。

### <a name="step-7-check-whether-hello-on-premises-vpn-device-has-perfect-forward-secrecy-enabled"></a>步驟 7 的核取是否 hello 內部部署 VPN 裝置有完整轉寄密碼啟用

hello**完整轉寄密碼**功能造成 hello 中斷連線的問題。 如果 hello VPN 裝置有**完整轉寄密碼**啟用、 停用 hello 功能。 然後[更新 hello 虛擬網路閘道 IPsec 原則](vpn-gateway-ipsecikepolicy-rm-powershell.md#managepolicy)。

## <a name="next-steps"></a>後續步驟

- [設定站對站連線 tooa 虛擬網路](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
- [設定站對站 VPN 連線的 IPsec/IKE 原則](vpn-gateway-ipsecikepolicy-rm-powershell.md)

