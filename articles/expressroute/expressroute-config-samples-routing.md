---
title: "aaaExpressRoute 客戶路由器組態範例 |Microsoft 文件"
description: "此頁面提供適用於 Cisco 和 Juniper 路由器的路由器組態範例。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: 564826bc-017a-4683-a385-37c9fa814948
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: 5c91f24e6082e01c3e8df91b4fcfda46a6c29fa8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="router-configuration-samples-tooset-up-and-manage-routing"></a>路由器組態範例 tooset 註冊和管理路由
此頁面提供適用於 Cisco IOS XE 和 Juniper MX 系列路由器的介面和路由組態範例。 這些是預定的 toobe 適用於只指引的範例，而且必須不直接使用。 您可以使用廠商 toocome 適當設定為您的網路。 

> [!IMPORTANT]
> 在這個頁面中的範例是預定的 toobe 只提供指引。 您必須使用供應商的銷售 / 技術團隊和您網路小組 toocome 設定適當的組態 toomeet 與您的需求。 Microsoft 將不支援問題相關 tooconfigurations 列在這個頁面。 您必須連絡您的裝置廠商來支援問題。
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a>路由器介面上的 MTU 和 TCP MSS 設定
* hello ExpressRoute 介面的 MTU hello 是 1500，hello 一般預設 MTU 的路由器上的乙太網路介面。 除非您的路由器預設具有不同的 MTU，沒有任何需要 toospecify 值 hello 路由器介面。
* 不同於 Azure VPN 閘道 hello TCP MSS ExpressRoute 循環不需要指定 toobe。

下面的路由器組態範例套用 tooall 對等互連。 如需路由的詳細資訊，請檢閱 [ExpressRoute 對等互連](expressroute-circuit-peerings.md)和 [ExpressRoute 路由需求](expressroute-routing.md)。


## <a name="cisco-ios-xe-based-routers"></a>Cisco IOS-XE 架構的路由器
本節中的 hello 範例適用於任何執行 hello IOS XE 作業系統系列的路由器。

### <a name="1-configuring-interfaces-and-sub-interfaces"></a>1.設定介面和子介面
您會需要每個互連中每個路由器的子介面連線 tooMicrosoft。 子介面可使用 VLAN ID 或一組堆疊的 VLAN ID 和 IP 位址來識別。

**Dot1Q 介面定義**

此範例提供 hello 子介面定義的子介面具有單一 VLAN id。 hello VLAN 識別碼是唯一的每個對等互連。 hello 的 IPv4 位址的最後一個八位元一律為奇數。

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

**QinQ 介面定義**

這個範例提供 hello 子介面定義具有兩個 VLAN 識別碼的子介面。 外部的 VLAN ID （s-已標記），如果使用維持的 hello hello 相同跨所有 hello 對等互連。 hello 內部 VLAN ID （c-已標記） 是每個對等互連唯一的。 hello 的 IPv4 位址的最後一個八位元一律為奇數。

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a>2.設定 eBGP 工作階段
您必須針對每個對等互連，設定與 Microsoft 的 BGP 工作階段。 以下 hello 範例可讓您與 Microsoft 的 BGP 工作階段的 toosetup。 如果您用於子介面的 IPv4 位址 hello a.b.c.d，hello hello (Microsoft) 的 BGP 芳鄰 IP 位址會 a.b.c.d+1。 hello hello BGP 芳鄰的 IPv4 位址的最後一個八位元一定是偶數。

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a>3.設定前置詞 toobe hello BGP 工作階段期間所公告
您可以設定您的路由器 tooadvertise 選取的前置詞 tooMicrosoft。 您可以執行使用 hello 以下的範例。

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a>4.路由對應
您可以使用路由對應和前置詞清單到您的網路傳播 toofilter 前置詞。 您可以使用以下 tooaccomplish hello 工作 hello 範例。 確定您已設定適當的前置詞清單。

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
      neighbor <IP#2_used_by_Azure> route-map <MS_Prefixes_Inbound> in
     exit-address-family
    !
    route-map <MS_Prefixes_Inbound> permit 10
     match ip address prefix-list <MS_Prefixes>
    !


## <a name="juniper-mx-series-routers"></a>Juniper MX 系列路由器
本節中的 hello 範例適用於 Juniper MX 數列的任何路由器。

### <a name="1-configuring-interfaces-and-sub-interfaces"></a>1.設定介面和子介面

**Dot1Q 介面定義**

此範例提供 hello 子介面定義的子介面具有單一 VLAN id。 hello VLAN 識別碼是唯一的每個對等互連。 hello 的 IPv4 位址的最後一個八位元一律為奇數。

    interfaces {
        vlan-tagging;
        <Interface_Number> {
            unit <Number> {
                vlan-id <VLAN_ID>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }
            }
        }
    }


**QinQ 介面定義**

這個範例提供 hello 子介面定義具有兩個 VLAN 識別碼的子介面。 外部的 VLAN ID （s-已標記），如果使用維持的 hello hello 相同跨所有 hello 對等互連。 hello 內部 VLAN ID （c-已標記） 是每個對等互連唯一的。 hello 的 IPv4 位址的最後一個八位元一律為奇數。

    interfaces {
        <Interface_Number> {
            flexible-vlan-tagging;
            unit <Number> {
                vlan-tags outer <S-tag> inner <C-tag>;
                family inet {
                    address <IPv4_Address/Subnet_Mask>;
                }                           
            }                               
        }                                   
    }                           

### <a name="2-setting-up-ebgp-sessions"></a>2.設定 eBGP 工作階段
您必須針對每個對等互連，設定與 Microsoft 的 BGP 工作階段。 以下 hello 範例可讓您與 Microsoft 的 BGP 工作階段的 toosetup。 如果您用於子介面的 IPv4 位址 hello a.b.c.d，hello hello (Microsoft) 的 BGP 芳鄰 IP 位址會 a.b.c.d+1。 hello hello BGP 芳鄰的 IPv4 位址的最後一個八位元一定是偶數。

    routing-options {
        autonomous-system <Customer_ASN>;
    }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a>3.設定前置詞 toobe hello BGP 工作階段期間所公告
您可以設定您的路由器 tooadvertise 選取的前置詞 tooMicrosoft。 您可以執行使用 hello 以下的範例。

    policy-options {
        policy-statement <Policy_Name> {
            term 1 {
                from protocol OSPF;
        route-filter <Prefix_to_be_advertised/Subnet_Mask> exact;
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }


### <a name="4-route-maps"></a>4.路由對應
您可以使用路由對應和前置詞清單到您的網路傳播 toofilter 前置詞。 您可以使用以下 tooaccomplish hello 工作 hello 範例。 確定您已設定適當的前置詞清單。

    policy-options {
        prefix-list MS_Prefixes {
            <IP_Prefix_1/Subnet_Mask>;
            <IP_Prefix_2/Subnet_Mask>;
        }
        policy-statement <MS_Prefixes_Inbound> {
            term 1 {
                from {
        prefix-list MS_Prefixes;
                }
                then {
                    accept;
                }
            }
        }
    }
    protocols {
        bgp { 
            group <Group_Name> { 
                export <Policy_Name>
                import <MS_Prefixes_Inbound>
                peer-as 12076;              
                neighbor <IP#2_used_by_Azure>;
            }                               
        }                                   
    }

## <a name="next-steps"></a>後續步驟
請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)如需詳細資訊。

