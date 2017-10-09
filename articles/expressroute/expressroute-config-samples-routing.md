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
# <a name="router-configuration-samples-tooset-up-and-manage-routing"></a><span data-ttu-id="db547-103">路由器組態範例 tooset 註冊和管理路由</span><span class="sxs-lookup"><span data-stu-id="db547-103">Router configuration samples tooset up and manage routing</span></span>
<span data-ttu-id="db547-104">此頁面提供適用於 Cisco IOS XE 和 Juniper MX 系列路由器的介面和路由組態範例。</span><span class="sxs-lookup"><span data-stu-id="db547-104">This page provides interface and routing configuration samples for Cisco IOS-XE and Juniper MX series routers.</span></span> <span data-ttu-id="db547-105">這些是預定的 toobe 適用於只指引的範例，而且必須不直接使用。</span><span class="sxs-lookup"><span data-stu-id="db547-105">These are intended toobe samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="db547-106">您可以使用廠商 toocome 適當設定為您的網路。</span><span class="sxs-lookup"><span data-stu-id="db547-106">You can work with your vendor toocome up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="db547-107">在這個頁面中的範例是預定的 toobe 只提供指引。</span><span class="sxs-lookup"><span data-stu-id="db547-107">Samples in this page are intended toobe purely for guidance.</span></span> <span data-ttu-id="db547-108">您必須使用供應商的銷售 / 技術團隊和您網路小組 toocome 設定適當的組態 toomeet 與您的需求。</span><span class="sxs-lookup"><span data-stu-id="db547-108">You must work with your vendor's sales / technical team and your networking team toocome up with appropriate configurations toomeet your needs.</span></span> <span data-ttu-id="db547-109">Microsoft 將不支援問題相關 tooconfigurations 列在這個頁面。</span><span class="sxs-lookup"><span data-stu-id="db547-109">Microsoft will not support issues related tooconfigurations listed in this page.</span></span> <span data-ttu-id="db547-110">您必須連絡您的裝置廠商來支援問題。</span><span class="sxs-lookup"><span data-stu-id="db547-110">You must contact your device vendor for support issues.</span></span>
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a><span data-ttu-id="db547-111">路由器介面上的 MTU 和 TCP MSS 設定</span><span class="sxs-lookup"><span data-stu-id="db547-111">MTU and TCP MSS settings on router interfaces</span></span>
* <span data-ttu-id="db547-112">hello ExpressRoute 介面的 MTU hello 是 1500，hello 一般預設 MTU 的路由器上的乙太網路介面。</span><span class="sxs-lookup"><span data-stu-id="db547-112">hello MTU for hello ExpressRoute interface is 1500, which is hello typical default MTU for an Ethernet interface on a router.</span></span> <span data-ttu-id="db547-113">除非您的路由器預設具有不同的 MTU，沒有任何需要 toospecify 值 hello 路由器介面。</span><span class="sxs-lookup"><span data-stu-id="db547-113">Unless your router has a different MTU by default, there is no need toospecify a value on hello router interface.</span></span>
* <span data-ttu-id="db547-114">不同於 Azure VPN 閘道 hello TCP MSS ExpressRoute 循環不需要指定 toobe。</span><span class="sxs-lookup"><span data-stu-id="db547-114">Unlike an Azure VPN Gateway, hello TCP MSS for an ExpressRoute circuit does not need toobe specified.</span></span>

<span data-ttu-id="db547-115">下面的路由器組態範例套用 tooall 對等互連。</span><span class="sxs-lookup"><span data-stu-id="db547-115">Router configuration samples below apply tooall peerings.</span></span> <span data-ttu-id="db547-116">如需路由的詳細資訊，請檢閱 [ExpressRoute 對等互連](expressroute-circuit-peerings.md)和 [ExpressRoute 路由需求](expressroute-routing.md)。</span><span class="sxs-lookup"><span data-stu-id="db547-116">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute routing requirements](expressroute-routing.md) for more details on routing.</span></span>


## <a name="cisco-ios-xe-based-routers"></a><span data-ttu-id="db547-117">Cisco IOS-XE 架構的路由器</span><span class="sxs-lookup"><span data-stu-id="db547-117">Cisco IOS-XE based routers</span></span>
<span data-ttu-id="db547-118">本節中的 hello 範例適用於任何執行 hello IOS XE 作業系統系列的路由器。</span><span class="sxs-lookup"><span data-stu-id="db547-118">hello samples in this section apply for any router running hello IOS-XE OS family.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="db547-119">1.設定介面和子介面</span><span class="sxs-lookup"><span data-stu-id="db547-119">1. Configuring interfaces and sub-interfaces</span></span>
<span data-ttu-id="db547-120">您會需要每個互連中每個路由器的子介面連線 tooMicrosoft。</span><span class="sxs-lookup"><span data-stu-id="db547-120">You will require a sub interface per peering in every router you connect tooMicrosoft.</span></span> <span data-ttu-id="db547-121">子介面可使用 VLAN ID 或一組堆疊的 VLAN ID 和 IP 位址來識別。</span><span class="sxs-lookup"><span data-stu-id="db547-121">A sub interface can be identified with a VLAN ID or a stacked pair of VLAN IDs and an IP address.</span></span>

<span data-ttu-id="db547-122">**Dot1Q 介面定義**</span><span class="sxs-lookup"><span data-stu-id="db547-122">**Dot1Q interface definition**</span></span>

<span data-ttu-id="db547-123">此範例提供 hello 子介面定義的子介面具有單一 VLAN id。</span><span class="sxs-lookup"><span data-stu-id="db547-123">This sample provides hello sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="db547-124">hello VLAN 識別碼是唯一的每個對等互連。</span><span class="sxs-lookup"><span data-stu-id="db547-124">hello VLAN ID is unique per peering.</span></span> <span data-ttu-id="db547-125">hello 的 IPv4 位址的最後一個八位元一律為奇數。</span><span class="sxs-lookup"><span data-stu-id="db547-125">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

<span data-ttu-id="db547-126">**QinQ 介面定義**</span><span class="sxs-lookup"><span data-stu-id="db547-126">**QinQ interface definition**</span></span>

<span data-ttu-id="db547-127">這個範例提供 hello 子介面定義具有兩個 VLAN 識別碼的子介面。</span><span class="sxs-lookup"><span data-stu-id="db547-127">This sample provides hello sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="db547-128">外部的 VLAN ID （s-已標記），如果使用維持的 hello hello 相同跨所有 hello 對等互連。</span><span class="sxs-lookup"><span data-stu-id="db547-128">hello outer VLAN ID (s-tag), if used remains hello same across all hello peerings.</span></span> <span data-ttu-id="db547-129">hello 內部 VLAN ID （c-已標記） 是每個對等互連唯一的。</span><span class="sxs-lookup"><span data-stu-id="db547-129">hello inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="db547-130">hello 的 IPv4 位址的最後一個八位元一律為奇數。</span><span class="sxs-lookup"><span data-stu-id="db547-130">hello last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="db547-131">2.設定 eBGP 工作階段</span><span class="sxs-lookup"><span data-stu-id="db547-131">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="db547-132">您必須針對每個對等互連，設定與 Microsoft 的 BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="db547-132">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="db547-133">以下 hello 範例可讓您與 Microsoft 的 BGP 工作階段的 toosetup。</span><span class="sxs-lookup"><span data-stu-id="db547-133">hello sample below enables you toosetup a BGP session with Microsoft.</span></span> <span data-ttu-id="db547-134">如果您用於子介面的 IPv4 位址 hello a.b.c.d，hello hello (Microsoft) 的 BGP 芳鄰 IP 位址會 a.b.c.d+1。</span><span class="sxs-lookup"><span data-stu-id="db547-134">If hello IPv4 address you used for your sub interface was a.b.c.d, hello IP address of hello BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="db547-135">hello hello BGP 芳鄰的 IPv4 位址的最後一個八位元一定是偶數。</span><span class="sxs-lookup"><span data-stu-id="db547-135">hello last octet of hello BGP neighbor's IPv4 address will always be an even number.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a><span data-ttu-id="db547-136">3.設定前置詞 toobe hello BGP 工作階段期間所公告</span><span class="sxs-lookup"><span data-stu-id="db547-136">3. Setting up prefixes toobe advertised over hello BGP session</span></span>
<span data-ttu-id="db547-137">您可以設定您的路由器 tooadvertise 選取的前置詞 tooMicrosoft。</span><span class="sxs-lookup"><span data-stu-id="db547-137">You can configure your router tooadvertise select prefixes tooMicrosoft.</span></span> <span data-ttu-id="db547-138">您可以執行使用 hello 以下的範例。</span><span class="sxs-lookup"><span data-stu-id="db547-138">You can do so using hello sample below.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a><span data-ttu-id="db547-139">4.路由對應</span><span class="sxs-lookup"><span data-stu-id="db547-139">4. Route maps</span></span>
<span data-ttu-id="db547-140">您可以使用路由對應和前置詞清單到您的網路傳播 toofilter 前置詞。</span><span class="sxs-lookup"><span data-stu-id="db547-140">You can use route-maps and prefix lists toofilter prefixes propagated into your network.</span></span> <span data-ttu-id="db547-141">您可以使用以下 tooaccomplish hello 工作 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="db547-141">You can use hello sample below tooaccomplish hello task.</span></span> <span data-ttu-id="db547-142">確定您已設定適當的前置詞清單。</span><span class="sxs-lookup"><span data-stu-id="db547-142">Ensure that you have appropriate prefix lists setup.</span></span>

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


## <a name="juniper-mx-series-routers"></a><span data-ttu-id="db547-143">Juniper MX 系列路由器</span><span class="sxs-lookup"><span data-stu-id="db547-143">Juniper MX series routers</span></span>
<span data-ttu-id="db547-144">本節中的 hello 範例適用於 Juniper MX 數列的任何路由器。</span><span class="sxs-lookup"><span data-stu-id="db547-144">hello samples in this section apply for any Juniper MX series routers.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="db547-145">1.設定介面和子介面</span><span class="sxs-lookup"><span data-stu-id="db547-145">1. Configuring interfaces and sub-interfaces</span></span>

<span data-ttu-id="db547-146">**Dot1Q 介面定義**</span><span class="sxs-lookup"><span data-stu-id="db547-146">**Dot1Q interface definition**</span></span>

<span data-ttu-id="db547-147">此範例提供 hello 子介面定義的子介面具有單一 VLAN id。</span><span class="sxs-lookup"><span data-stu-id="db547-147">This sample provides hello sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="db547-148">hello VLAN 識別碼是唯一的每個對等互連。</span><span class="sxs-lookup"><span data-stu-id="db547-148">hello VLAN ID is unique per peering.</span></span> <span data-ttu-id="db547-149">hello 的 IPv4 位址的最後一個八位元一律為奇數。</span><span class="sxs-lookup"><span data-stu-id="db547-149">hello last octet of your IPv4 address will always be an odd number.</span></span>

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


<span data-ttu-id="db547-150">**QinQ 介面定義**</span><span class="sxs-lookup"><span data-stu-id="db547-150">**QinQ interface definition**</span></span>

<span data-ttu-id="db547-151">這個範例提供 hello 子介面定義具有兩個 VLAN 識別碼的子介面。</span><span class="sxs-lookup"><span data-stu-id="db547-151">This sample provides hello sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="db547-152">外部的 VLAN ID （s-已標記），如果使用維持的 hello hello 相同跨所有 hello 對等互連。</span><span class="sxs-lookup"><span data-stu-id="db547-152">hello outer VLAN ID (s-tag), if used remains hello same across all hello peerings.</span></span> <span data-ttu-id="db547-153">hello 內部 VLAN ID （c-已標記） 是每個對等互連唯一的。</span><span class="sxs-lookup"><span data-stu-id="db547-153">hello inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="db547-154">hello 的 IPv4 位址的最後一個八位元一律為奇數。</span><span class="sxs-lookup"><span data-stu-id="db547-154">hello last octet of your IPv4 address will always be an odd number.</span></span>

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

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="db547-155">2.設定 eBGP 工作階段</span><span class="sxs-lookup"><span data-stu-id="db547-155">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="db547-156">您必須針對每個對等互連，設定與 Microsoft 的 BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="db547-156">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="db547-157">以下 hello 範例可讓您與 Microsoft 的 BGP 工作階段的 toosetup。</span><span class="sxs-lookup"><span data-stu-id="db547-157">hello sample below enables you toosetup a BGP session with Microsoft.</span></span> <span data-ttu-id="db547-158">如果您用於子介面的 IPv4 位址 hello a.b.c.d，hello hello (Microsoft) 的 BGP 芳鄰 IP 位址會 a.b.c.d+1。</span><span class="sxs-lookup"><span data-stu-id="db547-158">If hello IPv4 address you used for your sub interface was a.b.c.d, hello IP address of hello BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="db547-159">hello hello BGP 芳鄰的 IPv4 位址的最後一個八位元一定是偶數。</span><span class="sxs-lookup"><span data-stu-id="db547-159">hello last octet of hello BGP neighbor's IPv4 address will always be an even number.</span></span>

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

### <a name="3-setting-up-prefixes-toobe-advertised-over-hello-bgp-session"></a><span data-ttu-id="db547-160">3.設定前置詞 toobe hello BGP 工作階段期間所公告</span><span class="sxs-lookup"><span data-stu-id="db547-160">3. Setting up prefixes toobe advertised over hello BGP session</span></span>
<span data-ttu-id="db547-161">您可以設定您的路由器 tooadvertise 選取的前置詞 tooMicrosoft。</span><span class="sxs-lookup"><span data-stu-id="db547-161">You can configure your router tooadvertise select prefixes tooMicrosoft.</span></span> <span data-ttu-id="db547-162">您可以執行使用 hello 以下的範例。</span><span class="sxs-lookup"><span data-stu-id="db547-162">You can do so using hello sample below.</span></span>

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


### <a name="4-route-maps"></a><span data-ttu-id="db547-163">4.路由對應</span><span class="sxs-lookup"><span data-stu-id="db547-163">4. Route maps</span></span>
<span data-ttu-id="db547-164">您可以使用路由對應和前置詞清單到您的網路傳播 toofilter 前置詞。</span><span class="sxs-lookup"><span data-stu-id="db547-164">You can use route-maps and prefix lists toofilter prefixes propagated into your network.</span></span> <span data-ttu-id="db547-165">您可以使用以下 tooaccomplish hello 工作 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="db547-165">You can use hello sample below tooaccomplish hello task.</span></span> <span data-ttu-id="db547-166">確定您已設定適當的前置詞清單。</span><span class="sxs-lookup"><span data-stu-id="db547-166">Ensure that you have appropriate prefix lists setup.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="db547-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="db547-167">Next Steps</span></span>
<span data-ttu-id="db547-168">請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="db547-168">See hello [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

