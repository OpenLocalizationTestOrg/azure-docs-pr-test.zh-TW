---
title: "ExpressRoute 客戶路由器組態範例 | Microsoft Docs"
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
ms.openlocfilehash: 032e584dc5abf59e9e3e8d80673b402f1fbf721b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="router-configuration-samples-to-set-up-and-manage-routing"></a><span data-ttu-id="9a8be-103">設定和管理路由的路由器組態範例</span><span class="sxs-lookup"><span data-stu-id="9a8be-103">Router configuration samples to set up and manage routing</span></span>
<span data-ttu-id="9a8be-104">此頁面提供適用於 Cisco IOS XE 和 Juniper MX 系列路由器的介面和路由組態範例。</span><span class="sxs-lookup"><span data-stu-id="9a8be-104">This page provides interface and routing configuration samples for Cisco IOS-XE and Juniper MX series routers.</span></span> <span data-ttu-id="9a8be-105">這些範例僅可用作指引，不能依原樣使用。</span><span class="sxs-lookup"><span data-stu-id="9a8be-105">These are intended to be samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="9a8be-106">您可以和廠商合作來擬定適合您網路的組態。</span><span class="sxs-lookup"><span data-stu-id="9a8be-106">You can work with your vendor to come up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="9a8be-107">此頁面中的範例純粹只用作指引。</span><span class="sxs-lookup"><span data-stu-id="9a8be-107">Samples in this page are intended to be purely for guidance.</span></span> <span data-ttu-id="9a8be-108">您必須和廠商的業務人員 / 技術小組及您的網路團隊合作，來擬定適當的組態以符合您的需求。</span><span class="sxs-lookup"><span data-stu-id="9a8be-108">You must work with your vendor's sales / technical team and your networking team to come up with appropriate configurations to meet your needs.</span></span> <span data-ttu-id="9a8be-109">Microsoft 將不支援此頁面中所列組態的相關問題。</span><span class="sxs-lookup"><span data-stu-id="9a8be-109">Microsoft will not support issues related to configurations listed in this page.</span></span> <span data-ttu-id="9a8be-110">您必須連絡您的裝置廠商來支援問題。</span><span class="sxs-lookup"><span data-stu-id="9a8be-110">You must contact your device vendor for support issues.</span></span>
> 
> 

## <a name="mtu-and-tcp-mss-settings-on-router-interfaces"></a><span data-ttu-id="9a8be-111">路由器介面上的 MTU 和 TCP MSS 設定</span><span class="sxs-lookup"><span data-stu-id="9a8be-111">MTU and TCP MSS settings on router interfaces</span></span>
* <span data-ttu-id="9a8be-112">ExpressRoute 介面的 MTU 是 1500，這是路由器上乙太網路介面的典型預設 MTU。</span><span class="sxs-lookup"><span data-stu-id="9a8be-112">The MTU for the ExpressRoute interface is 1500, which is the typical default MTU for an Ethernet interface on a router.</span></span> <span data-ttu-id="9a8be-113">除非您的路由器預設有不同的 MTU，否則沒有必要指定路由器介面上的值。</span><span class="sxs-lookup"><span data-stu-id="9a8be-113">Unless your router has a different MTU by default, there is no need to specify a value on the router interface.</span></span>
* <span data-ttu-id="9a8be-114">不同於 Azure VPN 閘道，ExpressRoute 線路的 TCP MSS 不需要指定。</span><span class="sxs-lookup"><span data-stu-id="9a8be-114">Unlike an Azure VPN Gateway, the TCP MSS for an ExpressRoute circuit does not need to be specified.</span></span>

<span data-ttu-id="9a8be-115">下列路由器組態範例適用於所有對等互連。</span><span class="sxs-lookup"><span data-stu-id="9a8be-115">Router configuration samples below apply to all peerings.</span></span> <span data-ttu-id="9a8be-116">如需路由的詳細資訊，請檢閱 [ExpressRoute 對等互連](expressroute-circuit-peerings.md)和 [ExpressRoute 路由需求](expressroute-routing.md)。</span><span class="sxs-lookup"><span data-stu-id="9a8be-116">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute routing requirements](expressroute-routing.md) for more details on routing.</span></span>


## <a name="cisco-ios-xe-based-routers"></a><span data-ttu-id="9a8be-117">Cisco IOS-XE 架構的路由器</span><span class="sxs-lookup"><span data-stu-id="9a8be-117">Cisco IOS-XE based routers</span></span>
<span data-ttu-id="9a8be-118">本節中的範例適用於任何執行 IOS-XE 作業系統系列的路由器。</span><span class="sxs-lookup"><span data-stu-id="9a8be-118">The samples in this section apply for any router running the IOS-XE OS family.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="9a8be-119">1.設定介面和子介面</span><span class="sxs-lookup"><span data-stu-id="9a8be-119">1. Configuring interfaces and sub-interfaces</span></span>
<span data-ttu-id="9a8be-120">在您連線到 Microsoft 的每個路由器中，針對每個對等互連都需要有一個子介面。</span><span class="sxs-lookup"><span data-stu-id="9a8be-120">You will require a sub interface per peering in every router you connect to Microsoft.</span></span> <span data-ttu-id="9a8be-121">子介面可使用 VLAN ID 或一組堆疊的 VLAN ID 和 IP 位址來識別。</span><span class="sxs-lookup"><span data-stu-id="9a8be-121">A sub interface can be identified with a VLAN ID or a stacked pair of VLAN IDs and an IP address.</span></span>

<span data-ttu-id="9a8be-122">**Dot1Q 介面定義**</span><span class="sxs-lookup"><span data-stu-id="9a8be-122">**Dot1Q interface definition**</span></span>

<span data-ttu-id="9a8be-123">此範例會針對含有單一 VLAN ID 的子介面提供子介面定義。</span><span class="sxs-lookup"><span data-stu-id="9a8be-123">This sample provides the sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="9a8be-124">在每個對等互連中 VLAN ID 都是唯一的。</span><span class="sxs-lookup"><span data-stu-id="9a8be-124">The VLAN ID is unique per peering.</span></span> <span data-ttu-id="9a8be-125">IPv4 位址的最後一個八位元一定是奇數。</span><span class="sxs-lookup"><span data-stu-id="9a8be-125">The last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <VLAN_ID>
     ip address <IPv4_Address><Subnet_Mask>

<span data-ttu-id="9a8be-126">**QinQ 介面定義**</span><span class="sxs-lookup"><span data-stu-id="9a8be-126">**QinQ interface definition**</span></span>

<span data-ttu-id="9a8be-127">此範例會針對含有兩個 VLAN ID 的子介面提供子介面定義。</span><span class="sxs-lookup"><span data-stu-id="9a8be-127">This sample provides the sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="9a8be-128">外部的 VLAN ID (s-tag)，如果使用方式在所有對等互連上維持不變。</span><span class="sxs-lookup"><span data-stu-id="9a8be-128">The outer VLAN ID (s-tag), if used remains the same across all the peerings.</span></span> <span data-ttu-id="9a8be-129">在每個對等互連中內部的 VLAN ID (c-tag) 都是唯一的。</span><span class="sxs-lookup"><span data-stu-id="9a8be-129">The inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="9a8be-130">IPv4 位址的最後一個八位元一定是奇數。</span><span class="sxs-lookup"><span data-stu-id="9a8be-130">The last octet of your IPv4 address will always be an odd number.</span></span>

    interface GigabitEthernet<Interface_Number>.<Number>
     encapsulation dot1Q <s-tag> seconddot1Q <c-tag>
     ip address <IPv4_Address><Subnet_Mask>

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="9a8be-131">2.設定 eBGP 工作階段</span><span class="sxs-lookup"><span data-stu-id="9a8be-131">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="9a8be-132">您必須針對每個對等互連，設定與 Microsoft 的 BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="9a8be-132">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="9a8be-133">下列範例可讓您設定與 Microsoft 的 BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="9a8be-133">The sample below enables you to setup a BGP session with Microsoft.</span></span> <span data-ttu-id="9a8be-134">如果您針對子介面使用的 IPv4 位址是 a.b.c.d，則 BGP 芳鄰 (Microsoft) 的 IP 位址會是 a.b.c.d+1。</span><span class="sxs-lookup"><span data-stu-id="9a8be-134">If the IPv4 address you used for your sub interface was a.b.c.d, the IP address of the BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="9a8be-135">BGP 芳鄰的 IPv4 位址的最後一個八位元一定是偶數。</span><span class="sxs-lookup"><span data-stu-id="9a8be-135">The last octet of the BGP neighbor's IPv4 address will always be an even number.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
     neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="3-setting-up-prefixes-to-be-advertised-over-the-bgp-session"></a><span data-ttu-id="9a8be-136">3.將前置詞設定為要透過 BGP 工作階段進行公告</span><span class="sxs-lookup"><span data-stu-id="9a8be-136">3. Setting up prefixes to be advertised over the BGP session</span></span>
<span data-ttu-id="9a8be-137">您可以設定路由器，將選取前置詞公告給 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="9a8be-137">You can configure your router to advertise select prefixes to Microsoft.</span></span> <span data-ttu-id="9a8be-138">您可以使用下列範例來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="9a8be-138">You can do so using the sample below.</span></span>

    router bgp <Customer_ASN>
     bgp log-neighbor-changes
     neighbor <IP#2_used_by_Azure> remote-as 12076
     !        
     address-family ipv4
      network <Prefix_to_be_advertised> mask <Subnet_mask>
      neighbor <IP#2_used_by_Azure> activate
     exit-address-family
    !

### <a name="4-route-maps"></a><span data-ttu-id="9a8be-139">4.路由對應</span><span class="sxs-lookup"><span data-stu-id="9a8be-139">4. Route maps</span></span>
<span data-ttu-id="9a8be-140">您可以使用路由對應和前置詞清單，來篩選要傳播到您網路中的前置詞。</span><span class="sxs-lookup"><span data-stu-id="9a8be-140">You can use route-maps and prefix lists to filter prefixes propagated into your network.</span></span> <span data-ttu-id="9a8be-141">您可以使用下列範例來完成此工作。</span><span class="sxs-lookup"><span data-stu-id="9a8be-141">You can use the sample below to accomplish the task.</span></span> <span data-ttu-id="9a8be-142">確定您已設定適當的前置詞清單。</span><span class="sxs-lookup"><span data-stu-id="9a8be-142">Ensure that you have appropriate prefix lists setup.</span></span>

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


## <a name="juniper-mx-series-routers"></a><span data-ttu-id="9a8be-143">Juniper MX 系列路由器</span><span class="sxs-lookup"><span data-stu-id="9a8be-143">Juniper MX series routers</span></span>
<span data-ttu-id="9a8be-144">本節中的範例適用於所有的 Juniper MX 系列路由器。</span><span class="sxs-lookup"><span data-stu-id="9a8be-144">The samples in this section apply for any Juniper MX series routers.</span></span>

### <a name="1-configuring-interfaces-and-sub-interfaces"></a><span data-ttu-id="9a8be-145">1.設定介面和子介面</span><span class="sxs-lookup"><span data-stu-id="9a8be-145">1. Configuring interfaces and sub-interfaces</span></span>

<span data-ttu-id="9a8be-146">**Dot1Q 介面定義**</span><span class="sxs-lookup"><span data-stu-id="9a8be-146">**Dot1Q interface definition**</span></span>

<span data-ttu-id="9a8be-147">此範例會針對含有單一 VLAN ID 的子介面提供子介面定義。</span><span class="sxs-lookup"><span data-stu-id="9a8be-147">This sample provides the sub-interface definition for a sub-interface with a single VLAN ID.</span></span> <span data-ttu-id="9a8be-148">在每個對等互連中 VLAN ID 都是唯一的。</span><span class="sxs-lookup"><span data-stu-id="9a8be-148">The VLAN ID is unique per peering.</span></span> <span data-ttu-id="9a8be-149">IPv4 位址的最後一個八位元一定是奇數。</span><span class="sxs-lookup"><span data-stu-id="9a8be-149">The last octet of your IPv4 address will always be an odd number.</span></span>

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


<span data-ttu-id="9a8be-150">**QinQ 介面定義**</span><span class="sxs-lookup"><span data-stu-id="9a8be-150">**QinQ interface definition**</span></span>

<span data-ttu-id="9a8be-151">此範例會針對含有兩個 VLAN ID 的子介面提供子介面定義。</span><span class="sxs-lookup"><span data-stu-id="9a8be-151">This sample provides the sub-interface definition for a sub-interface with a two VLAN IDs.</span></span> <span data-ttu-id="9a8be-152">外部的 VLAN ID (s-tag)，如果使用方式在所有對等互連上維持不變。</span><span class="sxs-lookup"><span data-stu-id="9a8be-152">The outer VLAN ID (s-tag), if used remains the same across all the peerings.</span></span> <span data-ttu-id="9a8be-153">在每個對等互連中內部的 VLAN ID (c-tag) 都是唯一的。</span><span class="sxs-lookup"><span data-stu-id="9a8be-153">The inner VLAN ID (c-tag) is unique per peering.</span></span> <span data-ttu-id="9a8be-154">IPv4 位址的最後一個八位元一定是奇數。</span><span class="sxs-lookup"><span data-stu-id="9a8be-154">The last octet of your IPv4 address will always be an odd number.</span></span>

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

### <a name="2-setting-up-ebgp-sessions"></a><span data-ttu-id="9a8be-155">2.設定 eBGP 工作階段</span><span class="sxs-lookup"><span data-stu-id="9a8be-155">2. Setting up eBGP sessions</span></span>
<span data-ttu-id="9a8be-156">您必須針對每個對等互連，設定與 Microsoft 的 BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="9a8be-156">You must setup a BGP session with Microsoft for every peering.</span></span> <span data-ttu-id="9a8be-157">下列範例可讓您設定與 Microsoft 的 BGP 工作階段。</span><span class="sxs-lookup"><span data-stu-id="9a8be-157">The sample below enables you to setup a BGP session with Microsoft.</span></span> <span data-ttu-id="9a8be-158">如果您針對子介面使用的 IPv4 位址是 a.b.c.d，則 BGP 芳鄰 (Microsoft) 的 IP 位址會是 a.b.c.d+1。</span><span class="sxs-lookup"><span data-stu-id="9a8be-158">If the IPv4 address you used for your sub interface was a.b.c.d, the IP address of the BGP neighbor (Microsoft) will be a.b.c.d+1.</span></span> <span data-ttu-id="9a8be-159">BGP 芳鄰的 IPv4 位址的最後一個八位元一定是偶數。</span><span class="sxs-lookup"><span data-stu-id="9a8be-159">The last octet of the BGP neighbor's IPv4 address will always be an even number.</span></span>

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

### <a name="3-setting-up-prefixes-to-be-advertised-over-the-bgp-session"></a><span data-ttu-id="9a8be-160">3.將前置詞設定為要透過 BGP 工作階段進行公告</span><span class="sxs-lookup"><span data-stu-id="9a8be-160">3. Setting up prefixes to be advertised over the BGP session</span></span>
<span data-ttu-id="9a8be-161">您可以設定路由器，將選取前置詞公告給 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="9a8be-161">You can configure your router to advertise select prefixes to Microsoft.</span></span> <span data-ttu-id="9a8be-162">您可以使用下列範例來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="9a8be-162">You can do so using the sample below.</span></span>

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


### <a name="4-route-maps"></a><span data-ttu-id="9a8be-163">4.路由對應</span><span class="sxs-lookup"><span data-stu-id="9a8be-163">4. Route maps</span></span>
<span data-ttu-id="9a8be-164">您可以使用路由對應和前置詞清單，來篩選要傳播到您網路中的前置詞。</span><span class="sxs-lookup"><span data-stu-id="9a8be-164">You can use route-maps and prefix lists to filter prefixes propagated into your network.</span></span> <span data-ttu-id="9a8be-165">您可以使用下列範例來完成此工作。</span><span class="sxs-lookup"><span data-stu-id="9a8be-165">You can use the sample below to accomplish the task.</span></span> <span data-ttu-id="9a8be-166">確定您已設定適當的前置詞清單。</span><span class="sxs-lookup"><span data-stu-id="9a8be-166">Ensure that you have appropriate prefix lists setup.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9a8be-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9a8be-167">Next Steps</span></span>
<span data-ttu-id="9a8be-168">如需詳細資訊，請參閱〈 [ExpressRoute 常見問題集](expressroute-faqs.md) 〉。</span><span class="sxs-lookup"><span data-stu-id="9a8be-168">See the [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

