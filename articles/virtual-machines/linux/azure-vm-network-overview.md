---
title: "aaaAzure 和 Linux VM 網路概觀 |Microsoft 文件"
description: "Azure 與 Linux VM 網路概觀。"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: b5420e35-0463-4456-9803-6142db150f2e
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: c3de2dc583c62160e10c0e97e96fef49b9eaffbf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux-vm-network-overview"></a><span data-ttu-id="7b85c-103">Azure 與 Linux VM 網路概觀</span><span class="sxs-lookup"><span data-stu-id="7b85c-103">Azure and Linux VM Network Overview</span></span>
## <a name="virtual-networks"></a><span data-ttu-id="7b85c-104">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="7b85c-104">Virtual Networks</span></span>
<span data-ttu-id="7b85c-105">Azure 虛擬網路 (VNet) 是網路的您自己 hello 雲端中的表示法。</span><span class="sxs-lookup"><span data-stu-id="7b85c-105">An Azure virtual network (VNet) is a representation of your own network in hello cloud.</span></span> <span data-ttu-id="7b85c-106">它是 hello 的隔離的邏輯專用的 Azure 雲端 tooyour 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b85c-106">It is a logical isolation of hello Azure cloud dedicated tooyour subscription.</span></span> <span data-ttu-id="7b85c-107">您也可以完全控制 hello IP 位址區塊、 DNS 設定、 安全性原則，以及此網路內的路由表。</span><span class="sxs-lookup"><span data-stu-id="7b85c-107">You can fully control hello IP address blocks, DNS settings, security policies, and route tables within this network.</span></span> <span data-ttu-id="7b85c-108">您也可以進一步將 VNet 分成子網路，並啟動 Azure IaaS 虛擬機器 (VM) 和/或雲端服務 (PaaS 角色執行個體)。</span><span class="sxs-lookup"><span data-stu-id="7b85c-108">You can also further segment your VNet into subnets and launch Azure IaaS virtual machines (VMs) and/or Cloud services (PaaS role instances).</span></span> <span data-ttu-id="7b85c-109">此外，您可以使用其中一種可在 Azure 中的 hello 連線選項的 hello 虛擬網路 tooyour 在內部部署網路連線。</span><span class="sxs-lookup"><span data-stu-id="7b85c-109">Additionally, you can connect hello virtual network tooyour on-premises network using one of hello connectivity options available in Azure.</span></span> <span data-ttu-id="7b85c-110">基本上，您可以展開您的網路 tooAzure，並且可以完全控制在使用 Azure 提供的企業規模的 hello 優點的 IP 位址區塊。</span><span class="sxs-lookup"><span data-stu-id="7b85c-110">In essence, you can expand your network tooAzure, with complete control on IP address blocks with hello benefit of enterprise scale Azure provides.</span></span>

* [<span data-ttu-id="7b85c-111">虛擬網路概觀</span><span class="sxs-lookup"><span data-stu-id="7b85c-111">Virtual Network Overview</span></span>](../../virtual-network/virtual-networks-overview.md)

<span data-ttu-id="7b85c-112">toocreate 使用 VNet hello Azure CLI，移這裡 toofollow hello 逐步解說。</span><span class="sxs-lookup"><span data-stu-id="7b85c-112">toocreate a VNet by using hello Azure CLI, go here toofollow hello walk through.</span></span>

* [<span data-ttu-id="7b85c-113">如何使用 VNet toocreate hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7b85c-113">How toocreate a VNet using hello Azure CLI</span></span>](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

## <a name="network-security-groups"></a><span data-ttu-id="7b85c-114">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="7b85c-114">Network Security Groups</span></span>
<span data-ttu-id="7b85c-115">網路安全性群組 (NSG) 包含存取控制清單 (ACL) 規則，允許或拒絕網路流量 tooyour 虛擬網路中的 VM 執行個體的清單。</span><span class="sxs-lookup"><span data-stu-id="7b85c-115">Network security group (NSG) contains a list of Access Control List (ACL) rules that allow or deny network traffic tooyour VM instances in a Virtual Network.</span></span> <span data-ttu-id="7b85c-116">NSG 可與子網路或該子網路內的個別 VM 執行個體相關聯。</span><span class="sxs-lookup"><span data-stu-id="7b85c-116">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="7b85c-117">將 nsg 關聯與子網路產生關聯時，hello ACL 規則適用於 tooall hello VM 執行個體中子網路。</span><span class="sxs-lookup"><span data-stu-id="7b85c-117">When a NSG is associated with a subnet, hello ACL rules apply tooall hello VM instances in that subnet.</span></span> <span data-ttu-id="7b85c-118">此外，流量 tooan 個別 VM 可能會限制其他關聯 NSG 直接 toothat VM。</span><span class="sxs-lookup"><span data-stu-id="7b85c-118">In addition, traffic tooan individual VM can be restricted further by associating a NSG directly toothat VM.</span></span>

* [<span data-ttu-id="7b85c-119">什麼是網路安全性群組 (NSG)？</span><span class="sxs-lookup"><span data-stu-id="7b85c-119">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="7b85c-120">如何在 toocreate Nsg hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7b85c-120">How toocreate NSGs in hello Azure CLI</span></span>](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

## <a name="user-defined-routes"></a><span data-ttu-id="7b85c-121">使用者定義的路由</span><span class="sxs-lookup"><span data-stu-id="7b85c-121">User Defined Routes</span></span>
<span data-ttu-id="7b85c-122">當您在 Azure 中新增虛擬機器 (Vm) tooa 虛擬網路 (VNet) 時，您會發現 hello Vm 會自動無法 toocommunicate 彼此 hello 網路上。</span><span class="sxs-lookup"><span data-stu-id="7b85c-122">When you add virtual machines (VMs) tooa virtual network (VNet) in Azure, you will notice that hello VMs are able toocommunicate with each other over hello network, automatically.</span></span> <span data-ttu-id="7b85c-123">您不需要 toospecify 閘道，即使 hello Vm 位於不同的子網路。</span><span class="sxs-lookup"><span data-stu-id="7b85c-123">You do not need toospecify a gateway, even though hello VMs are in different subnets.</span></span> <span data-ttu-id="7b85c-124">hello 也適用於來自 hello Vm toohello 通訊公用網際網路，以及混合式連線從 Azure tooyour 擁有資料中心已存在時，甚至 tooyour 與內部網路。</span><span class="sxs-lookup"><span data-stu-id="7b85c-124">hello same is true for communication from hello VMs toohello public Internet, and even tooyour on-premises network when a hybrid connection from Azure tooyour own datacenter is present.</span></span>

* [<span data-ttu-id="7b85c-125">什麼是使用者定義路由和 IP 轉送？</span><span class="sxs-lookup"><span data-stu-id="7b85c-125">What are User Defined Routes and IP Forwarding?</span></span>](../../virtual-network/virtual-networks-udr-overview.md)
* [<span data-ttu-id="7b85c-126">在 hello Azure CLI 中建立 UDR</span><span class="sxs-lookup"><span data-stu-id="7b85c-126">Create a UDR in hello Azure CLI</span></span>](../../virtual-network/virtual-network-create-udr-arm-cli.md)

## <a name="associating-a-fqdn-tooyour-linux-vm"></a><span data-ttu-id="7b85c-127">FQDN tooyour Linux VM 建立關聯</span><span class="sxs-lookup"><span data-stu-id="7b85c-127">Associating a FQDN tooyour Linux VM</span></span>
<span data-ttu-id="7b85c-128">Hello Azure 入口網站中建立虛擬機器 (VM) 時使用 hello Resource Manager 部署模型，公用 IP 資源 hello 虛擬機器會自動建立。</span><span class="sxs-lookup"><span data-stu-id="7b85c-128">When you create a virtual machine (VM) in hello Azure portal using hello Resource Manager deployment model, a public IP resource for hello virtual machine is automatically created.</span></span> <span data-ttu-id="7b85c-129">您使用此 IP 位址 tooremotely 存取 hello VM。</span><span class="sxs-lookup"><span data-stu-id="7b85c-129">You use this IP address tooremotely access hello VM.</span></span> <span data-ttu-id="7b85c-130">雖然 hello 入口網站不會建立一個完整的網域名稱或 FQDN，根據預設，您可以加入一個，一旦建立 hello VM。</span><span class="sxs-lookup"><span data-stu-id="7b85c-130">Although hello portal does not create a fully qualified domain name, or FQDN, by default, you can add one once hello VM is created.</span></span>

* [<span data-ttu-id="7b85c-131">在 hello Azure 入口網站中建立完整網域名稱</span><span class="sxs-lookup"><span data-stu-id="7b85c-131">Create a Fully Qualified Domain Name in hello Azure portal</span></span>](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="network-interfaces"></a><span data-ttu-id="7b85c-132">網路介面</span><span class="sxs-lookup"><span data-stu-id="7b85c-132">Network interfaces</span></span>
<span data-ttu-id="7b85c-133">網路介面 (NIC) 是虛擬機器 (VM) 與 hello 基礎軟體網路之間的 hello 互相連線。</span><span class="sxs-lookup"><span data-stu-id="7b85c-133">A network interface (NIC) is hello interconnection between a Virtual Machine (VM) and hello underlying software network.</span></span> <span data-ttu-id="7b85c-134">本文說明的網路介面，且它 hello Azure Resource Manager 部署模型中的使用方式。</span><span class="sxs-lookup"><span data-stu-id="7b85c-134">This article explains what a network interface is and how it's used in hello Azure Resource Manager deployment model.</span></span>

* [<span data-ttu-id="7b85c-135">虛擬網路介面</span><span class="sxs-lookup"><span data-stu-id="7b85c-135">Virtual Network Interfaces</span></span>](../../virtual-network/virtual-network-network-interface.md)

## <a name="virtual-nics-and-dns-labeling"></a><span data-ttu-id="7b85c-136">虛擬 NIC 和 DNS 標籤</span><span class="sxs-lookup"><span data-stu-id="7b85c-136">Virtual NICs and DNS labeling</span></span>
<span data-ttu-id="7b85c-137">如果您的伺服器，您需要 toobe 持續性，但該伺服器會被視為牛與終止並經常部署，您會想 toouse 標記 hello VNET 您 NIC 的 toopersist hello 名稱上的 DNS。</span><span class="sxs-lookup"><span data-stu-id="7b85c-137">If you have a server that you need toobe persistent, but that server is treated as cattle and is torn down and deployed frequently, you will want toouse DNS labeling on your NIC toopersist hello name on hello VNET.</span></span>  <span data-ttu-id="7b85c-138">以 hello 遵循逐步解說中，您將設定持續具名的 NIC 與靜態 ip 位址。</span><span class="sxs-lookup"><span data-stu-id="7b85c-138">With hello following walk-through you will setup a persistently named NIC with a static IP.</span></span>

* [<span data-ttu-id="7b85c-139">使用 Azure CLI hello 建立完整的 Linux 環境</span><span class="sxs-lookup"><span data-stu-id="7b85c-139">Create a complete Linux environment by using hello Azure CLI</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="virtual-network-gateways"></a><span data-ttu-id="7b85c-140">虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="7b85c-140">Virtual Network Gateways</span></span>
<span data-ttu-id="7b85c-141">使用虛擬網路閘道 toosend 網路流量的 Azure 虛擬網路與內部部署位置之間和 Azure (VNet 對 VNet) 內的虛擬網路之間。</span><span class="sxs-lookup"><span data-stu-id="7b85c-141">A virtual network gateway is used toosend network traffic between Azure virtual networks and on-premises locations and also between virtual networks within Azure (VNet-to-VNet).</span></span> <span data-ttu-id="7b85c-142">當您設定 VPN 閘道時，您必須建立及設定虛擬網路閘道和虛擬網路閘道連線。</span><span class="sxs-lookup"><span data-stu-id="7b85c-142">When you configure a VPN gateway, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

* [<span data-ttu-id="7b85c-143">關於 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="7b85c-143">About VPN Gateway</span></span>](../../vpn-gateway/vpn-gateway-about-vpngateways.md)

## <a name="internal-load-balancing"></a><span data-ttu-id="7b85c-144">內部負載平衡</span><span class="sxs-lookup"><span data-stu-id="7b85c-144">Internal Load Balancing</span></span>
<span data-ttu-id="7b85c-145">Azure 負載平衡器是第 4 層 (TCP、UDP) 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="7b85c-145">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="7b85c-146">hello 負載平衡器連入流量的各項雲端服務中的狀況良好的服務執行個體或虛擬機器中負載平衡器集可提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="7b85c-146">hello load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="7b85c-147">Azure Load Balancer 也會在多個連接埠、多個 IP 位址或兩者上顯示這些服務。</span><span class="sxs-lookup"><span data-stu-id="7b85c-147">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

* [<span data-ttu-id="7b85c-148">建立使用 Azure CLI hello 內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="7b85c-148">Creating an internal load balancer using hello Azure CLI</span></span>](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)

