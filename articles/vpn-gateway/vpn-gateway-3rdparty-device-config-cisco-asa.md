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
# <a name="sample-configuration-cisco-asa-device-ikev2no-bgp"></a>範例組態：Cisco ASA 裝置 (IKEv2/無 BGP)
本文章提供範例設定適用於 Cisco ASA 裝置連接 tooAzure VPN 閘道。

## <a name="device-at-a-glance"></a>裝置速覽

|                        |                                   |
| ---                    | ---                               |
| 裝置廠商          | Cisco                             |
| 裝置型號           | ASA (Adaptive Security Appliance) |
| 目標版本         | 8.4+                              |
| 測試的型號           | ASA 5505                          |
| 測試的版本         | 9.2                               |
| IKE 版本            | **IKEv2**                         |
| BGP                    | **否**                            |
| Azure VPN 閘道類型 | **路由式** VPN 閘道       |
|                        |                                   |

> [!NOTE]
> 1. 下列的 hello 組態連接 Cisco ASA 裝置 tooan Azure**路由式**"UserPolicyBasedTrafficSelectors 」 選項時，使用自訂 IPsec/IKE 原則，如下所示的 VPN 閘道[本文](vpn-gateway-connect-multiple-policybased-rm-ps.md).
> 2. 它需要 ASA 裝置 toouse **IKEv2**使用存取清單為基礎的組態，不以 VTI 為基礎。
> 3. 請洽詢您 tooensure hello 原則在內部部署 VPN 裝置支援的 VPN 裝置廠商規格。

## <a name="vpn-device-requirements"></a>VPN 裝置需求
Azure VPN 閘道使用標準 IPsec/IKE 通訊協定套件 tooestablish S2S VPN 通道。 請參閱太[關於 VPN 裝置](vpn-gateway-about-vpn-devices.md)hello 詳細的 IPsec/IKE 通訊協定參數和 Azure VPN 閘道的預設密碼編譯演算法。 中所述，您可以選擇指定的密碼編譯演算法和金鑰長度為特定連線的 hello 確切組合[有關密碼編譯需求](vpn-gateway-about-compliance-crypto.md)。 如果您選取特定密碼編譯演算法和金鑰長度的組合，請確定您使用您的 VPN 裝置 hello 對應規格。

## <a name="single-vpn-tunnel"></a>單一 VPN 通道
此拓撲是由 Azure VPN 閘道與您內部部署 VPN 裝置之間的單一 S2S VPN 通道所組成。 您可以選擇性地跨 hello VPN 通道設定 BGP。

![單一通道](./media/vpn-gateway-3rdparty-device-config-cisco-asa/singletunnel.png)

請參閱太[單一通道設定](vpn-gateway-3rdparty-device-config-overview.md#singletunnel)如詳細，逐步解說 toobuild hello Azure 組態。

### <a name="network-and-vpn-gateway-information"></a>網路和 VPN 閘道資訊
本節列出此範例的 hello hello 參數。

| **參數**                | **值**                    |
| ---                          | ---                          |
| VNet 位址首碼        | 10.11.0.0/16<br>10.12.0.0/16 |
| Azure VPN 閘道 IP         | Azure_Gateway_Public_IP      |
| 內部部署位址首碼 | 10.51.0.0/16<br>10.52.0.0/16 |
| 內部部署 VPN 裝置 IP    | OnPrem_Device_Public_IP     |
| *VNet BGP ASN                | 65010                        |
| *Azure BGP 對等 IP           | 10.12.255.30                 |
| *內部部署 BGP ASN         | 65050                        |
| *內部部署 BGP 對等 IP     | 10.52.255.254                |
|                              |                              |

* (*) 僅適用於 BGP 的選擇性參數。

### <a name="ipsecike-policy--parameters"></a>IPsec/IKE 原則與參數

hello 下表列出 hello IPsec/IKE 演算法和 hello 範例中使用的參數。 請參閱您 VPN 裝置規格 toomake 確定您的 VPN 裝置型號和軔體版本支援以上所列的所有演算法。

| **IPsec/IKEv2**  | **值**                            |
| ---              | ---                                  |
| IKEv2 加密 | AES256                               |
| IKEv2 完整性  | SHA384                               |
| DH 群組         | DHGroup24                            |
| IPsec 加密 | AES256                               |
| IPsec 完整性  | SHA1                                 |
| PFS 群組        | PFS24                                |
| QM SA 存留期   | 7200 秒                         |
| 流量選取器 | UsePolicyBasedTrafficSelectors $True |
| 預先共用金鑰   | PreSharedKey                         |
|                  |                                      |

- (*) 在某些裝置上，如果使用 GCM AES 作為 IPsec 加密演算法，IPsec 完整性就必須為 "null"。

### <a name="device-notes"></a>裝置注意事項

>[!NOTE]
>
> 1. IKEv2 支援需要 ASA 8.4 版及更新版本。
> 2. 較高的 DH 和 PFS 群組支援 (除了群組 5) 需要 ASA 版本 9.x。
> 3. 在較新的 ASA 硬體上，支援透過 AES-GCM 進行的 IPsec 加密及具備 SHA-256、SHA-384、SHA-512 的 IPsec 完整性需要 ASA 版本 9.x；**不**支援 ASA 5505、5510、5520、5540、5550、5580 （請查看 hello 廠商規格 tooconfirm。）
>


### <a name="sample-device-configurations"></a>範例裝置組態
下列 hello 指令碼提供設定 hello 拓撲為基礎的範例與上面所列的參數。 hello S2S VPN 通道設定包含下列組件的 hello:

1. 介面與路由
2. 存取清單存取清單
3. IKE 原則和參數 (第 1 階段或主要模式)
4. IPsec 原則和參數 (第 2 階段或快速模式)
5. 其他參數 (TCP MSS 固定等)

>[!IMPORTANT] 
>請確定您完成下面所列的 hello 其他設定，而且 hello 預留位置取代為 hello 實際值：
> 
> - 適用於內部和外部介面的介面組態
> - 適用於您內部/私用和外部/公用網路的路由
> - 確定所有名稱和原則的數字都是唯一 hello 裝置上
> - 請確定您的裝置上支援 hello 密碼編譯演算法
> - 取代下列預留位置 hello 實際值的 hello
>   - 外部介面名稱："outside"
>   - Azure_Gateway_Public_IP
>   - OnPrem_Device_Public_IP
>   - IKE Pre_Shared_Key
>   - VNet 與區域網路閘道名稱 (VNetName、LNGName)
>   - VNet 和內部部署網路位址首碼
>   - 適當的網路遮罩

#### <a name="sample-configuration"></a>範例組態

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

## <a name="simple-debugging-commands"></a>簡單偵錯命令

以下是一些可基於偵錯用途使用的 ASA 命令：

1. 顯示 hello IPsec 和 IKE SA
    - "show crypto ipsec sa"
    - "show crypto ikev2 sa"
2. 輸入的偵錯模式-這可以取得非常累贅 hello 主控台上
    - "debug crypto ikev2 platform <level>"
    - "debug crypto ikev2 protocol <level>"
3. 列出目前的組態
    - 「 顯示執行 」-顯示 hello hello 裝置; 上目前的組態您可以使用 hello 各種子命令 toolist 的特定部分 hello 組態。 例如，"show run crypto"、"show run access-list"、"show run tunnel-group" 等。


## <a name="next-steps"></a>後續步驟
請參閱[跨單位和 VNet 對 VNet 連線設定主動-主動 VPN 閘道](vpn-gateway-activeactive-rm-powershell.md)步驟 tooconfigure 主動-主動跨單位和 VNet 對 VNet 連線。

