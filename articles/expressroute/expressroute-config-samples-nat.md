---
title: "aaaExpressRoute 客戶路由器組態範例 |Microsoft 文件"
description: "此頁面提供適用於 Cisco 和 Juniper 路由器的路由器組態範例。"
documentationcenter: na
services: expressroute
author: cherylmc
manager: carmonm
editor: 
ms.assetid: d6ea716f-d5ee-4a61-92b0-640d6e7d6974
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: b5faca0666bda6173e54abb0b6560d5f8bf8bfc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="router-configuration-samples-tooset-up-and-manage-nat"></a><span data-ttu-id="d3cdf-103">路由器組態範例 tooset 註冊和管理 NAT</span><span class="sxs-lookup"><span data-stu-id="d3cdf-103">Router configuration samples tooset up and manage NAT</span></span>
<span data-ttu-id="d3cdf-104">此頁面提供適用於 Cisco ASA 和 Juniper SRX 系列路由器的 NAT 組態範例。</span><span class="sxs-lookup"><span data-stu-id="d3cdf-104">This page provides NAT configuration samples for Cisco ASA and Juniper SRX series routers.</span></span> <span data-ttu-id="d3cdf-105">這些是預定的 toobe 適用於只指引的範例，而且必須不直接使用。</span><span class="sxs-lookup"><span data-stu-id="d3cdf-105">These are intended toobe samples for guidance only and must not be used as is.</span></span> <span data-ttu-id="d3cdf-106">您可以使用廠商 toocome 適當設定為您的網路。</span><span class="sxs-lookup"><span data-stu-id="d3cdf-106">You can work with your vendor toocome up with appropriate configurations for your network.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d3cdf-107">在這個頁面中的範例是預定的 toobe 只提供指引。</span><span class="sxs-lookup"><span data-stu-id="d3cdf-107">Samples in this page are intended toobe purely for guidance.</span></span> <span data-ttu-id="d3cdf-108">您必須使用供應商的銷售 / 技術團隊和您網路小組 toocome 設定適當的組態 toomeet 與您的需求。</span><span class="sxs-lookup"><span data-stu-id="d3cdf-108">You must work with your vendor's sales / technical team and your networking team toocome up with appropriate configurations toomeet your needs.</span></span> <span data-ttu-id="d3cdf-109">Microsoft 將不支援問題相關 tooconfigurations 列在這個頁面。</span><span class="sxs-lookup"><span data-stu-id="d3cdf-109">Microsoft will not support issues related tooconfigurations listed in this page.</span></span> <span data-ttu-id="d3cdf-110">您必須連絡您的裝置廠商來支援問題。</span><span class="sxs-lookup"><span data-stu-id="d3cdf-110">You must contact your device vendor for support issues.</span></span>
> 
> 

* <span data-ttu-id="d3cdf-111">下面的路由器組態範例套用 tooAzure 公用及 Microsoft 對等互連。</span><span class="sxs-lookup"><span data-stu-id="d3cdf-111">Router configuration samples below apply tooAzure Public and Microsoft peerings.</span></span> <span data-ttu-id="d3cdf-112">您必須設定 Azure 私人對等互連的 NAT。</span><span class="sxs-lookup"><span data-stu-id="d3cdf-112">You must not configure NAT for Azure private peering.</span></span> <span data-ttu-id="d3cdf-113">如需詳細資訊，請檢閱 [ExpressRoute 對等互連](expressroute-circuit-peerings.md)和 [ExpressRoute NAT 需求](expressroute-nat.md)。</span><span class="sxs-lookup"><span data-stu-id="d3cdf-113">Review [ExpressRoute peerings](expressroute-circuit-peerings.md) and [ExpressRoute NAT requirements](expressroute-nat.md) for more details.</span></span>

* <span data-ttu-id="d3cdf-114">您必須使用 NAT IP 集區的個別連線 toohello 網際網路和 ExpressRoute。</span><span class="sxs-lookup"><span data-stu-id="d3cdf-114">You MUST use separate NAT IP pools for connectivity toohello internet and ExpressRoute.</span></span> <span data-ttu-id="d3cdf-115">使用相同的 NAT IP 集區之間的 hello hello 網際網路和 ExpressRoute 會導致非對稱的路由和連線中斷。</span><span class="sxs-lookup"><span data-stu-id="d3cdf-115">Using hello same NAT IP pool across hello internet and ExpressRoute will result in asymmetric routing and loss of connectivity.</span></span>


## <a name="cisco-asa-firewalls"></a><span data-ttu-id="d3cdf-116">Cisco ASA 防火牆</span><span class="sxs-lookup"><span data-stu-id="d3cdf-116">Cisco ASA firewalls</span></span>
### <a name="pat-configuration-for-traffic-from-customer-network-toomicrosoft"></a><span data-ttu-id="d3cdf-117">從客戶網路 tooMicrosoft 流量 PAT 組態</span><span class="sxs-lookup"><span data-stu-id="d3cdf-117">PAT configuration for traffic from customer network tooMicrosoft</span></span>
    object network MSFT-PAT
      range <SNAT-START-IP> <SNAT-END-IP>


    object-group network MSFT-Range
      network-object <IP> <Subnet_Mask>

    object-group network on-prem-range-1
      network-object <IP> <Subnet-Mask>

    object-group network on-prem-range-2
      network-object <IP> <Subnet-Mask>

    object-group network on-prem
      network-object object on-prem-range-1
      network-object object on-prem-range-2

    nat (outside,inside) source dynamic on-prem pat-pool MSFT-PAT destination static MSFT-Range MSFT-Range

### <a name="pat-configuration-for-traffic-from-microsoft-toocustomer-network"></a><span data-ttu-id="d3cdf-118">從 Microsoft toocustomer 網路流量的 PAT 組態</span><span class="sxs-lookup"><span data-stu-id="d3cdf-118">PAT configuration for traffic from Microsoft toocustomer network</span></span>

<span data-ttu-id="d3cdf-119">**介面和方向：**</span><span class="sxs-lookup"><span data-stu-id="d3cdf-119">**Interfaces and Direction:**</span></span>

    Source Interface (where hello traffic enters hello ASA): inside
    Destination Interface (where hello traffic exits hello ASA): outside

<span data-ttu-id="d3cdf-120">**組態：**</span><span class="sxs-lookup"><span data-stu-id="d3cdf-120">**Configuration:**</span></span>

<span data-ttu-id="d3cdf-121">NAT 集區：</span><span class="sxs-lookup"><span data-stu-id="d3cdf-121">NAT Pool:</span></span>

    object network outbound-PAT
        host <NAT-IP>

<span data-ttu-id="d3cdf-122">目標伺服器：</span><span class="sxs-lookup"><span data-stu-id="d3cdf-122">Target Server:</span></span>

    object network Customer-Network
        network-object <IP> <Subnet-Mask>

<span data-ttu-id="d3cdf-123">客戶 IP 位址的物件群組</span><span class="sxs-lookup"><span data-stu-id="d3cdf-123">Object Group for Customer IP Addresses</span></span>

    object-group network MSFT-Network-1
        network-object <MSFT-IP> <Subnet-Mask>

    object-group network MSFT-PAT-Networks
        network-object object MSFT-Network-1

<span data-ttu-id="d3cdf-124">NAT 命令：</span><span class="sxs-lookup"><span data-stu-id="d3cdf-124">NAT Commands:</span></span>

    nat (inside,outside) source dynamic MSFT-PAT-Networks pat-pool outbound-PAT destination static Customer-Network Customer-Network


## <a name="juniper-srx-series-routers"></a><span data-ttu-id="d3cdf-125">Juniper SRX 系列路由器</span><span class="sxs-lookup"><span data-stu-id="d3cdf-125">Juniper SRX series routers</span></span>
### <a name="1-create-redundant-ethernet-interfaces-for-hello-cluster"></a><span data-ttu-id="d3cdf-126">1.建立重複的乙太網路介面的 hello 叢集</span><span class="sxs-lookup"><span data-stu-id="d3cdf-126">1. Create redundant Ethernet interfaces for hello cluster</span></span>
    interfaces {
        reth0 {
            description "tooInternal Network";
            vlan-tagging;
            redundant-ether-options {
                redundancy-group 1;
            }
            unit 100 {
                vlan-id 100;
                family inet {
                    address <IP-Address/Subnet-mask>;
                }
            }
        }
        reth1 {
            description "tooMicrosoft via Edge Router";
            vlan-tagging;
            redundant-ether-options {
                redundancy-group 2;
            }
            unit 100 {
                description "tooMicrosoft via Edge Router";
                vlan-id 100;
                family inet {
                    address <IP-Address/Subnet-mask>;
                }
            }
        }
    }


### <a name="2-create-two-security-zones"></a><span data-ttu-id="d3cdf-127">2.建立兩個安全性區域</span><span class="sxs-lookup"><span data-stu-id="d3cdf-127">2. Create two security zones</span></span>
* <span data-ttu-id="d3cdf-128">內部網路的信任區域和外部網路面向邊緣路由器的未受信任區域</span><span class="sxs-lookup"><span data-stu-id="d3cdf-128">Trust Zone for internal network and Untrust Zone for external network facing Edge Routers</span></span>
* <span data-ttu-id="d3cdf-129">指派適當的介面 toohello 區域</span><span class="sxs-lookup"><span data-stu-id="d3cdf-129">Assign appropriate interfaces toohello zones</span></span>
* <span data-ttu-id="d3cdf-130">允許在 hello 介面上的服務</span><span class="sxs-lookup"><span data-stu-id="d3cdf-130">Allow services on hello interfaces</span></span>

    <span data-ttu-id="d3cdf-131">security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }</span><span class="sxs-lookup"><span data-stu-id="d3cdf-131">security {       zones {           security-zone Trust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth0.100;               }           }           security-zone Untrust {               host-inbound-traffic {                   system-services {                       ping;                   }                   protocols {                       bgp;                   }               }               interfaces {                   reth1.100;               }           }       }   }</span></span>


### <a name="3-create-security-policies-between-zones"></a><span data-ttu-id="d3cdf-132">3.建立區域之間的安全性原則</span><span class="sxs-lookup"><span data-stu-id="d3cdf-132">3. Create security policies between zones</span></span>
    security {
        policies {
            from-zone Trust to-zone Untrust {
                policy allow-any {
                    match {
                        source-address any;
                        destination-address any;
                        application any;
                    }
                    then {
                        permit;
                    }
                }
            }
            from-zone Untrust to-zone Trust {
                policy allow-any {
                    match {
                        source-address any;
                        destination-address any;
                        application any;
                    }
                    then {
                        permit;
                    }
                }
            }
        }
    }


### <a name="4-configure-nat-policies"></a><span data-ttu-id="d3cdf-133">4.設定 NAT 原則</span><span class="sxs-lookup"><span data-stu-id="d3cdf-133">4. Configure NAT policies</span></span>
* <span data-ttu-id="d3cdf-134">建立兩個 NAT 集區。</span><span class="sxs-lookup"><span data-stu-id="d3cdf-134">Create two NAT pools.</span></span> <span data-ttu-id="d3cdf-135">其中一個會使用的 tooNAT 流量輸出 tooMicrosoft 和其他 Microsoft toohello 客戶。</span><span class="sxs-lookup"><span data-stu-id="d3cdf-135">One will be used tooNAT traffic outbound tooMicrosoft and other from Microsoft toohello customer.</span></span>
* <span data-ttu-id="d3cdf-136">TooNAT hello 個別流量建立規則</span><span class="sxs-lookup"><span data-stu-id="d3cdf-136">Create rules tooNAT hello respective traffic</span></span>
  
       security {
           nat {
               source {
                   pool SNAT-To-ExpressRoute {
                       routing-instance {
                           External-ExpressRoute;
                       }
                       address {
                           <NAT-IP-address/Subnet-mask>;
                       }
                   }
                   pool SNAT-From-ExpressRoute {
                       routing-instance {
                           Internal;
                       }
                       address {
                           <NAT-IP-address/Subnet-mask>;
                       }
                   }
                   rule-set Outbound_NAT {
                       from routing-instance Internal;
                       toorouting-instance External-ExpressRoute;
                       rule SNAT-Out {
                           match {
                               source-address 0.0.0.0/0;
                           }
                           then {
                               source-nat {
                                   pool {
                                       SNAT-To-ExpressRoute;
                                   }
                               }
                           }
                       }
                   }
                   rule-set Inbound-NAT {
                       from routing-instance External-ExpressRoute;
                       toorouting-instance Internal;
                       rule SNAT-In {
                           match {
                               source-address 0.0.0.0/0;
                           }
                           then {
                               source-nat {
                                   pool {
                                       SNAT-From-ExpressRoute;
                                   }
                               }
                           }
                       }
                   }
               }
           }
       }

### <a name="5-configure-bgp-tooadvertise-selective-prefixes-in-each-direction"></a><span data-ttu-id="d3cdf-137">5.在每個方向中設定 BGP tooadvertise 選擇性前置詞</span><span class="sxs-lookup"><span data-stu-id="d3cdf-137">5. Configure BGP tooadvertise selective prefixes in each direction</span></span>
<span data-ttu-id="d3cdf-138">參考在 toosamples[路由組態範例](expressroute-config-samples-routing.md)頁面。</span><span class="sxs-lookup"><span data-stu-id="d3cdf-138">Refer toosamples in [Routing configuration samples ](expressroute-config-samples-routing.md) page.</span></span>

### <a name="6-create-policies"></a><span data-ttu-id="d3cdf-139">6.建立原則</span><span class="sxs-lookup"><span data-stu-id="d3cdf-139">6. Create policies</span></span>
    routing-options {
                  autonomous-system <Customer-ASN>;
    }
    policy-options {
        prefix-list Microsoft-Prefixes {
            <IP-Address/Subnet-Mask;
            <IP-Address/Subnet-Mask;
        }
        prefix-list private-ranges {
            10.0.0.0/8;
            172.16.0.0/12;
            192.168.0.0/16;
            100.64.0.0/10;
        }
        policy-statement Advertise-NAT-Pools {
            from {
                protocol static;
                route-filter <NAT-Pool-Address/Subnet-mask> prefix-length-range /32-/32;
            }
            then accept;
        }
        policy-statement Accept-from-Microsoft {
            term 1 {
                from {
                    instance External-ExpressRoute;
                    prefix-list-filter Microsoft-Prefixes orlonger;
                }
                then accept;
            }
            term deny {
                then reject;
            }
        }
        policy-statement Accept-from-Internal {
            term no-private {
                from {
                    instance Internal;
                    prefix-list-filter private-ranges orlonger;
                }
                then reject;
            }
            term bgp {
                from {
                    instance Internal;
                    protocol bgp;
                }
                then accept;
            }
            term deny {
                then reject;
            }
        }
    }
    routing-instances {
        Internal {
            instance-type virtual-router;
            interface reth0.100;
            routing-options {
                static {
                    route <NAT-Pool-IP-Address/Subnet-mask> discard;
                }
                instance-import Accept-from-Microsoft;
            }
            protocols {
                bgp {
                    group customer {
                        export <Advertise-NAT-Pools>;
                        peer-as <Customer-ASN-1>;
                        neighbor <BGP-Neighbor-IP-Address>;
                    }
                }
            }
        }
        External-ExpressRoute {
            instance-type virtual-router;
            interface reth1.100;
            routing-options {
                static {
                    route <NAT-Pool-IP-Address/Subnet-mask> discard;
                }
                instance-import Accept-from-Internal;
            }
            protocols {
                bgp {
                    group edge-router {
                        export <Advertise-NAT-Pools>;
                        peer-as <Customer-Public-ASN>;
                        neighbor <BGP-Neighbor-IP-Address>;
                    }
                }
            }
        }
    }

## <a name="next-steps"></a><span data-ttu-id="d3cdf-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d3cdf-140">Next steps</span></span>
<span data-ttu-id="d3cdf-141">請參閱 hello [ExpressRoute 常見問題集](expressroute-faqs.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="d3cdf-141">See hello [ExpressRoute FAQ](expressroute-faqs.md) for more details.</span></span>

