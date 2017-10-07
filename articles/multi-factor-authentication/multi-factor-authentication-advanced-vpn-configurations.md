---
title: "使用 Azure MFA 和協力廠商 Vpn aaaAdvanced 案例"
description: "Azure MFA toointegrate Cisco、 Citrix，與 Juniper 的逐步設定指南。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 1f94a214-d6f6-48a8-8a12-006b5896ae45
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/13/2017
ms.author: kgremban
ms.openlocfilehash: e23960ca4977cc01271f99fa2bec70449e9acfff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-scenarios-with-azure-multi-factor-authentication-and-third-party-vpn-solutions"></a>使用 Azure Multi-Factor Authentication 與協力廠商 VPN 解決方案的進階案例
可以使用 azure Multi-factor Authentication tooseamlessly 連線使用不同的協力廠商 VPN 解決方案。 本文著重在 Cisco® ASA VPN 應用裝置、 Citrix NetScaler SSL VPN 應用裝置及 hello Juniper 網路安全存取/Pulse Secure 連線安全 SSL VPN 應用裝置。 我們建立了組態指南 tooaddress 這些三種常見應用裝置，但 Multi-factor Authentication Server 可以與使用 RADIUS、 LDAP、 IIS 或宣告式驗證 tooAD FS 的大部分系統整合。 您可以在 [MFA Server 組態](multi-factor-authentication-get-started-server.md#next-steps)中找到更多詳細資料。

## <a name="cisco-asa-vpn-appliance-and-azure-multi-factor-authentication"></a>Cisco ASA VPN 應用裝置和 Azure Multi-Factor Authentication
Azure Multi-factor Authentication 會與您 Cisco® ASA VPN 應用裝置 tooprovide 額外的安全性 Cisco AnyConnect® VPN 登入和存取入口網站整合。  這可以使用任一 hello LDAP 或 RADIUS 通訊協定。  選取其中一個 hello 遵循 toodownload hello 詳細的逐步設定指南。

| 組態指南 | 說明 |
| --- | --- |
| [Cisco ASA with Anyconnect VPN 與 Azure MFA Configuration for LDAP](http://download.microsoft.com/download/A/2/0/A201567C-C3DE-4227-AF89-4567A470899E/Cisco_ASA_Azure_MFA_LDAP.docx) | 使用 LDAP 整合 Cisco ASA VPN 應用裝置與 Azure MFA |
| [Cisco ASA with Anyconnect VPN 與 Azure MFA Configuration for RADIUS](http://download.microsoft.com/download/4/5/7/4579C1CF-35B0-4FBE-8A1A-B49CB2CC0382/Cisco_ASA_Azure_MFA_RADIUS.docx) | 使用 RADIUS 整合 Cisco ASA VPN 應用裝置與 Azure MFA |

## <a name="citrix-netscaler-ssl-vpn-and-azure-multi-factor-authentication"></a>Citrix NetScaler SSL VPN 與 Azure Multi-Factor Authentication
Azure Multi-factor Authentication 會與您 Citrix NetScaler SSL VPN 應用裝置 tooprovide 額外的安全性 Citrix NetScaler SSL VPN 登入和存取入口網站整合。  這可以使用任一 hello LDAP 或 RADIUS 通訊協定。  選取其中一個 hello 遵循 toodownload hello 詳細的逐步設定指南。

| 組態指南 | 說明 |
| --- | --- |
| [Citrix NetScaler SSL VPN 與 Azure MFA Configuration for LDAP](http://download.microsoft.com/download/2/4/E/24E1E722-72DF-471F-A88A-D1338DB1AF83/Citrix_NS_Azure_MFA_LDAP.docx) | 使用 LDAP 整合 Citrix NetScaler SSL VPN 與 Azure MFA |
| [Citrix NetScaler SSL VPN 與 Azure MFA Configuration for RADIUS](http://download.microsoft.com/download/1/A/4/1A482764-4A63-45C2-A5EC-2B673ACCDD12/Citrix_NS_Azure_MFA_RADIUS.docx) | 使用 RADIUS 整合 Citrix NetScaler SSL VPN 應用裝置與 Azure MFA |

## <a name="juniperpulse-secure-ssl-vpn-appliance-and-azure-multi-factor-authentication"></a>Juniper/Pulse Secure SSL VPN 應用裝置和 Azure Multi-Factor Authentication
Azure Multi-factor Authentication 會與您 Juniper/Pulse 安全的 SSL VPN 應用裝置 tooprovide 額外的安全性 Juniper/Pulse 安全的 SSL VPN 登入和存取入口網站整合。  這可以使用任一 hello LDAP 或 RADIUS 通訊協定。  選取其中一個 hello 遵循 toodownload hello 詳細的逐步設定指南。

| 組態指南 | 說明 |
| --- | --- |
| [Juniper/Pulse Secure SSL VPN 與 Azure MFA Configuration for LDAP](http://download.microsoft.com/download/6/5/8/6587B418-75B1-4FCB-84D4-984BC479309E/JuniperPulse_Azure_MFA_LDAP.docx) | 使用 LDAP 整合 Juniper/Pulse Secure SSL VPN 與 Azure MFA |
| [Juniper/Pulse Secure SSL VPN 與 Azure MFA Configuration for RADIUS](http://download.microsoft.com/download/7/9/A/79AB3DAD-4799-4379-B1DA-B95ABDF231DC/JuniperPulse_Azure_MFA_RADIUS.docx) | 使用 RADIUS 整合 Juniper/Pulse Secure SSL VPN 應用裝置與 Azure MFA |

## <a name="next-steps"></a>後續步驟

- [針對 Azure Multi-factor Authentication 加強現有的驗證基礎結構以 hello NPS 擴充功能](multi-factor-authentication-nps-extension.md)

- [設定 Azure Multi-Factor Authentication 設定](multi-factor-authentication-whats-next.md)