---
title: "Azure 與 Linux VM 網路概觀 |Microsoft Docs"
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
ms.openlocfilehash: 1ff4a0482d6dc6ec0eceaa89ca4b87ba1e2f89a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-and-linux-vm-network-overview"></a><span data-ttu-id="b0b17-103">Azure 與 Linux VM 網路概觀</span><span class="sxs-lookup"><span data-stu-id="b0b17-103">Azure and Linux VM Network Overview</span></span>
## <a name="virtual-networks"></a><span data-ttu-id="b0b17-104">虛擬網路</span><span class="sxs-lookup"><span data-stu-id="b0b17-104">Virtual Networks</span></span>
<span data-ttu-id="b0b17-105">Azure 虛擬網路 (VNet) 是您的網路在雲端中的身分。</span><span class="sxs-lookup"><span data-stu-id="b0b17-105">An Azure virtual network (VNet) is a representation of your own network in the cloud.</span></span> <span data-ttu-id="b0b17-106">它是專屬於您訂用帳戶的 Azure 雲端邏輯隔離。</span><span class="sxs-lookup"><span data-stu-id="b0b17-106">It is a logical isolation of the Azure cloud dedicated to your subscription.</span></span> <span data-ttu-id="b0b17-107">您可以完全控制此網路內的 IP 位址區塊、DNS 設定、安全性原則和路由表。</span><span class="sxs-lookup"><span data-stu-id="b0b17-107">You can fully control the IP address blocks, DNS settings, security policies, and route tables within this network.</span></span> <span data-ttu-id="b0b17-108">您也可以進一步將 VNet 分成子網路，並啟動 Azure IaaS 虛擬機器 (VM) 和/或雲端服務 (PaaS 角色執行個體)。</span><span class="sxs-lookup"><span data-stu-id="b0b17-108">You can also further segment your VNet into subnets and launch Azure IaaS virtual machines (VMs) and/or Cloud services (PaaS role instances).</span></span> <span data-ttu-id="b0b17-109">另外，您也可以使用 Azure 中提供的其中一個連線選項將虛擬網路連線到內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="b0b17-109">Additionally, you can connect the virtual network to your on-premises network using one of the connectivity options available in Azure.</span></span> <span data-ttu-id="b0b17-110">基本上，您可以將您的網路延伸至 Azure，透過 Azure 提供的企業級好處完整控制 IP 位址區塊。</span><span class="sxs-lookup"><span data-stu-id="b0b17-110">In essence, you can expand your network to Azure, with complete control on IP address blocks with the benefit of enterprise scale Azure provides.</span></span>

* [<span data-ttu-id="b0b17-111">虛擬網路概觀</span><span class="sxs-lookup"><span data-stu-id="b0b17-111">Virtual Network Overview</span></span>](../../virtual-network/virtual-networks-overview.md)

<span data-ttu-id="b0b17-112">若要使用 Azure CLI 建立 VNet，請前往這裡並遵循逐步解說。</span><span class="sxs-lookup"><span data-stu-id="b0b17-112">To create a VNet by using the Azure CLI, go here to follow the walk through.</span></span>

* [<span data-ttu-id="b0b17-113">如何透過 Azure CLI 建立 VNet</span><span class="sxs-lookup"><span data-stu-id="b0b17-113">How to create a VNet using the Azure CLI</span></span>](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

## <a name="network-security-groups"></a><span data-ttu-id="b0b17-114">網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="b0b17-114">Network Security Groups</span></span>
<span data-ttu-id="b0b17-115">網路安全性群組 (NSG) 包含存取控制清單 (ACL) 規則的清單，可允許或拒絕虛擬網路中 VM 執行個體的網路流量。</span><span class="sxs-lookup"><span data-stu-id="b0b17-115">Network security group (NSG) contains a list of Access Control List (ACL) rules that allow or deny network traffic to your VM instances in a Virtual Network.</span></span> <span data-ttu-id="b0b17-116">NSG 可與子網路或該子網路內的個別 VM 執行個體相關聯。</span><span class="sxs-lookup"><span data-stu-id="b0b17-116">NSGs can be associated with either subnets or individual VM instances within that subnet.</span></span> <span data-ttu-id="b0b17-117">當 NSG 與子網路相關聯時，ACL 規則便會套用至該子網路中的所有 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="b0b17-117">When a NSG is associated with a subnet, the ACL rules apply to all the VM instances in that subnet.</span></span> <span data-ttu-id="b0b17-118">此外，將 NSG 直接關聯至該 VM 即可進一步限制個別 VM 的流量。</span><span class="sxs-lookup"><span data-stu-id="b0b17-118">In addition, traffic to an individual VM can be restricted further by associating a NSG directly to that VM.</span></span>

* [<span data-ttu-id="b0b17-119">什麼是網路安全性群組 (NSG)？</span><span class="sxs-lookup"><span data-stu-id="b0b17-119">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="b0b17-120">如何在 Azure CLI 中建立 NSG</span><span class="sxs-lookup"><span data-stu-id="b0b17-120">How to create NSGs in the Azure CLI</span></span>](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

## <a name="user-defined-routes"></a><span data-ttu-id="b0b17-121">使用者定義的路由</span><span class="sxs-lookup"><span data-stu-id="b0b17-121">User Defined Routes</span></span>
<span data-ttu-id="b0b17-122">當您在 Azure 中將虛擬機器 (VM) 新增到虛擬網路 (VNet) 時，您會發現 VM 能自動透過網路彼此通訊。</span><span class="sxs-lookup"><span data-stu-id="b0b17-122">When you add virtual machines (VMs) to a virtual network (VNet) in Azure, you will notice that the VMs are able to communicate with each other over the network, automatically.</span></span> <span data-ttu-id="b0b17-123">您不需要指定閘道，即使 VM 位於不同子網路。</span><span class="sxs-lookup"><span data-stu-id="b0b17-123">You do not need to specify a gateway, even though the VMs are in different subnets.</span></span> <span data-ttu-id="b0b17-124">VM 到公開網際網路的通訊同樣適用，甚至當存在 Azure 到您的資料中心的混合連線時，也適用於您的內部網路。</span><span class="sxs-lookup"><span data-stu-id="b0b17-124">The same is true for communication from the VMs to the public Internet, and even to your on-premises network when a hybrid connection from Azure to your own datacenter is present.</span></span>

* [<span data-ttu-id="b0b17-125">什麼是使用者定義路由和 IP 轉送？</span><span class="sxs-lookup"><span data-stu-id="b0b17-125">What are User Defined Routes and IP Forwarding?</span></span>](../../virtual-network/virtual-networks-udr-overview.md)
* [<span data-ttu-id="b0b17-126">在 Azure CLI 建立 UDR</span><span class="sxs-lookup"><span data-stu-id="b0b17-126">Create a UDR in the Azure CLI</span></span>](../../virtual-network/virtual-network-create-udr-arm-cli.md)

## <a name="associating-a-fqdn-to-your-linux-vm"></a><span data-ttu-id="b0b17-127">將 FQDN 與您的 Linux VM 產生關聯</span><span class="sxs-lookup"><span data-stu-id="b0b17-127">Associating a FQDN to your Linux VM</span></span>
<span data-ttu-id="b0b17-128">在 Azure 入口網站中使用 Resource Manager 部署模型來建立虛擬機器 (VM) 時，會自動建立虛擬機器的公用 IP 資源。</span><span class="sxs-lookup"><span data-stu-id="b0b17-128">When you create a virtual machine (VM) in the Azure portal using the Resource Manager deployment model, a public IP resource for the virtual machine is automatically created.</span></span> <span data-ttu-id="b0b17-129">您可以使用此 IP 位址從遠端存取 VM。</span><span class="sxs-lookup"><span data-stu-id="b0b17-129">You use this IP address to remotely access the VM.</span></span> <span data-ttu-id="b0b17-130">雖然入口網站預設不會建立完整網域名稱，或稱為 FQDN，但是您可以在 VM 建立之後新增一個。</span><span class="sxs-lookup"><span data-stu-id="b0b17-130">Although the portal does not create a fully qualified domain name, or FQDN, by default, you can add one once the VM is created.</span></span>

* [<span data-ttu-id="b0b17-131">在 Azure 入口網站中建立完整格式的網域名稱</span><span class="sxs-lookup"><span data-stu-id="b0b17-131">Create a Fully Qualified Domain Name in the Azure portal</span></span>](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="network-interfaces"></a><span data-ttu-id="b0b17-132">網路介面</span><span class="sxs-lookup"><span data-stu-id="b0b17-132">Network interfaces</span></span>
<span data-ttu-id="b0b17-133">網路介面 (NIC) 是虛擬機器 (VM) 與基礎軟體網路之間互相連線的橋樑。</span><span class="sxs-lookup"><span data-stu-id="b0b17-133">A network interface (NIC) is the interconnection between a Virtual Machine (VM) and the underlying software network.</span></span> <span data-ttu-id="b0b17-134">本文說明什麼是網路介面，以及在 Azure Resource Manager 部署模型中如何加以使用。</span><span class="sxs-lookup"><span data-stu-id="b0b17-134">This article explains what a network interface is and how it's used in the Azure Resource Manager deployment model.</span></span>

* [<span data-ttu-id="b0b17-135">虛擬網路介面</span><span class="sxs-lookup"><span data-stu-id="b0b17-135">Virtual Network Interfaces</span></span>](../../virtual-network/virtual-network-network-interface.md)

## <a name="virtual-nics-and-dns-labeling"></a><span data-ttu-id="b0b17-136">虛擬 NIC 和 DNS 標籤</span><span class="sxs-lookup"><span data-stu-id="b0b17-136">Virtual NICs and DNS labeling</span></span>
<span data-ttu-id="b0b17-137">如果您有需要持續運作的伺服器，但是該伺服器被視為 cattle 並且頻繁地拆除和部署，您會想要在您的 NIC 上使用 DNS 標籤以在 VNET 上保持名稱。</span><span class="sxs-lookup"><span data-stu-id="b0b17-137">If you have a server that you need to be persistent, but that server is treated as cattle and is torn down and deployed frequently, you will want to use DNS labeling on your NIC to persist the name on the VNET.</span></span>  <span data-ttu-id="b0b17-138">您將使用下列逐步解說，設定持續具名的 NIC 與靜態 IP。</span><span class="sxs-lookup"><span data-stu-id="b0b17-138">With the following walk-through you will setup a persistently named NIC with a static IP.</span></span>

* [<span data-ttu-id="b0b17-139">使用 Azure CLI 建立完整的 Linux 環境</span><span class="sxs-lookup"><span data-stu-id="b0b17-139">Create a complete Linux environment by using the Azure CLI</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="virtual-network-gateways"></a><span data-ttu-id="b0b17-140">虛擬網路閘道</span><span class="sxs-lookup"><span data-stu-id="b0b17-140">Virtual Network Gateways</span></span>
<span data-ttu-id="b0b17-141">虛擬網路閘道用來傳送 Azure 虛擬網路和內部部署位置之間，以及 Azure 內的虛擬網路 (VNet 對 VNet) 之間的網路流量。</span><span class="sxs-lookup"><span data-stu-id="b0b17-141">A virtual network gateway is used to send network traffic between Azure virtual networks and on-premises locations and also between virtual networks within Azure (VNet-to-VNet).</span></span> <span data-ttu-id="b0b17-142">當您設定 VPN 閘道時，您必須建立及設定虛擬網路閘道和虛擬網路閘道連線。</span><span class="sxs-lookup"><span data-stu-id="b0b17-142">When you configure a VPN gateway, you must create and configure a virtual network gateway and a virtual network gateway connection.</span></span>

* [<span data-ttu-id="b0b17-143">關於 VPN 閘道</span><span class="sxs-lookup"><span data-stu-id="b0b17-143">About VPN Gateway</span></span>](../../vpn-gateway/vpn-gateway-about-vpngateways.md)

## <a name="internal-load-balancing"></a><span data-ttu-id="b0b17-144">內部負載平衡</span><span class="sxs-lookup"><span data-stu-id="b0b17-144">Internal Load Balancing</span></span>
<span data-ttu-id="b0b17-145">Azure 負載平衡器是第 4 層 (TCP、UDP) 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="b0b17-145">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer.</span></span> <span data-ttu-id="b0b17-146">此負載平衡器可藉由在負載平衡器集合中，將連入流量分散於雲端服務或虛擬機器中狀況良好的服務執行個體之間，來提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="b0b17-146">The load balancer provides high availability by distributing incoming traffic among healthy service instances in cloud services or virtual machines in a load balancer set.</span></span> <span data-ttu-id="b0b17-147">Azure Load Balancer 也會在多個連接埠、多個 IP 位址或兩者上顯示這些服務。</span><span class="sxs-lookup"><span data-stu-id="b0b17-147">Azure Load Balancer can also present those services on multiple ports, multiple IP addresses, or both.</span></span>

* [<span data-ttu-id="b0b17-148">使用 Azure CLI 建立內部負載平衡器</span><span class="sxs-lookup"><span data-stu-id="b0b17-148">Creating an internal load balancer using the Azure CLI</span></span>](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)

