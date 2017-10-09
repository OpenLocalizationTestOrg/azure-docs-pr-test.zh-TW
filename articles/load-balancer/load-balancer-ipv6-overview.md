---
title: "Azure 負載平衡器的 IPv6 的 aaaOverview |Microsoft 文件"
description: "了解 Azure Load Balancer 和負載平衡 VM 的 IPv6 支援。"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
keywords: "ipv6, azure load balancer, 雙重堆疊, 公用 ip, 原生 ipv6, 行動, iot"
ms.assetid: 6a1d583f-a305-40fd-a94b-fa42e1943bbb
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/14/2016
ms.author: kumud
ms.openlocfilehash: 5b203f77d86cc1ad455f4ebb297097aef46b658d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-ipv6-for-azure-load-balancer"></a><span data-ttu-id="b3117-104">Azure Load Balancer 的 IPv6 概觀</span><span class="sxs-lookup"><span data-stu-id="b3117-104">Overview of IPv6 for Azure Load Balancer</span></span>

<span data-ttu-id="b3117-105">網際網路面向的負載平衡器可以部署 IPv6 位址。</span><span class="sxs-lookup"><span data-stu-id="b3117-105">Internet-facing load balancers can be deployed with an IPv6 address.</span></span> <span data-ttu-id="b3117-106">此外 tooIPv4 連線，這可讓 hello 下列功能：</span><span class="sxs-lookup"><span data-stu-id="b3117-106">In addition tooIPv4 connectivity, this enables hello following capabilities:</span></span>

* <span data-ttu-id="b3117-107">原生端對端 IPv6 連線能力之間公用網際網路用戶端和 Azure 虛擬機器 (Vm) 透過 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="b3117-107">Native end-to-end IPv6 connectivity between public Internet clients and Azure Virtual Machines (VMs) through hello load balancer.</span></span>
* <span data-ttu-id="b3117-108">原生端對端 IPv6 輸出連線能力 - 在 VM 和公用網際網路上已啟用 IPv6 的用戶端之間。</span><span class="sxs-lookup"><span data-stu-id="b3117-108">Native end-to-end IPv6 outbound connectivity between VMs and public Internet IPv6-enabled clients.</span></span>

<span data-ttu-id="b3117-109">下列圖片的 hello 說明 hello IPv6 功能的 Azure 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="b3117-109">hello following picture illustrates hello IPv6 functionality for Azure Load Balancer.</span></span>

![配置有 IPv6 的 Azure Load Balancer](./media/load-balancer-ipv6-overview/load-balancer-ipv6.png)

<span data-ttu-id="b3117-111">一旦部署之後，IPv4 或 IPv6 啟用網際網路的用戶端可以與 hello 公用 IPv4 或 IPv6 位址 （或主機名稱） 的 hello Azure 網際網路對向負載平衡器進行通訊。</span><span class="sxs-lookup"><span data-stu-id="b3117-111">Once deployed, an IPv4 or IPv6-enabled Internet client can communicate with hello public IPv4 or IPv6 addresses (or hostnames) of hello Azure Internet-facing Load Balancer.</span></span> <span data-ttu-id="b3117-112">hello 負載平衡器路由 hello IPv6 封包 toohello 私人 IPv6 位址的 hello Vm 使用網路位址轉譯 (NAT)。</span><span class="sxs-lookup"><span data-stu-id="b3117-112">hello load balancer routes hello IPv6 packets toohello private IPv6 addresses of hello VMs using network address translation (NAT).</span></span> <span data-ttu-id="b3117-113">hello IPv6 網際網路用戶端無法直接與 hello hello Vm 的 IPv6 位址通訊。</span><span class="sxs-lookup"><span data-stu-id="b3117-113">hello IPv6 Internet client cannot communicate directly with hello IPv6 address of hello VMs.</span></span>

## <a name="features"></a><span data-ttu-id="b3117-114">特性</span><span class="sxs-lookup"><span data-stu-id="b3117-114">Features</span></span>

<span data-ttu-id="b3117-115">透過 Azure Resource Manager部署的原生 IPv6 支援提供︰</span><span class="sxs-lookup"><span data-stu-id="b3117-115">Native IPv6 support for VMs deployed via Azure Resource Manager provides:</span></span>

1. <span data-ttu-id="b3117-116">負載平衡 IPv6 hello 網際網路上的用戶端的 IPv6 服務</span><span class="sxs-lookup"><span data-stu-id="b3117-116">Load-balanced IPv6 services for IPv6 clients on hello Internet</span></span>
2. <span data-ttu-id="b3117-117">在 VM上提供原生 IPv6 和 IPv4 端點 (「雙重堆疊」)</span><span class="sxs-lookup"><span data-stu-id="b3117-117">Native IPv6 and IPv4 endpoints on VMs ("dual stacked")</span></span>
3. <span data-ttu-id="b3117-118">由輸入和輸出起始的原生 IPv6 連線</span><span class="sxs-lookup"><span data-stu-id="b3117-118">Inbound and outbound-initiated native IPv6 connections</span></span>
4. <span data-ttu-id="b3117-119">支援的通訊協定 - 如 TCP、UDP、HTTP(S) - 提供完整的服務架構</span><span class="sxs-lookup"><span data-stu-id="b3117-119">Supported protocols such as TCP, UDP, and HTTP(S) enable a full range of service architectures</span></span>

## <a name="benefits"></a><span data-ttu-id="b3117-120">優點</span><span class="sxs-lookup"><span data-stu-id="b3117-120">Benefits</span></span>

<span data-ttu-id="b3117-121">這項功能可讓 hello 下列主要優點：</span><span class="sxs-lookup"><span data-stu-id="b3117-121">This functionality enables hello following key benefits:</span></span>

* <span data-ttu-id="b3117-122">符合政府法規要求新的應用程式可存取的僅限 tooIPv6 用戶端</span><span class="sxs-lookup"><span data-stu-id="b3117-122">Meet government regulations requiring that new applications be accessible tooIPv6-only clients</span></span>
* <span data-ttu-id="b3117-123">啟用行動裝置版和網際網路的項目 (IOT) 開發人員 toouse 雙重堆疊 (IPv4 + IPv6) 的 Azure 虛擬機器 tooaddress hello 持續成長的行動裝置版和 IOT 市場</span><span class="sxs-lookup"><span data-stu-id="b3117-123">Enable mobile and Internet of things (IOT) developers toouse dual-stacked (IPv4+IPv6) Azure Virtual Machines tooaddress hello growing mobile & IOT markets</span></span>

## <a name="details-and-limitations"></a><span data-ttu-id="b3117-124">詳細資料和限制</span><span class="sxs-lookup"><span data-stu-id="b3117-124">Details and limitations</span></span>

<span data-ttu-id="b3117-125">詳細資料</span><span class="sxs-lookup"><span data-stu-id="b3117-125">Details</span></span>

* <span data-ttu-id="b3117-126">hello Azure DNS 服務包含 IPV4 和 IPv6 AAAA 名稱記錄，然後會回應 hello 負載平衡器的兩筆記錄。</span><span class="sxs-lookup"><span data-stu-id="b3117-126">hello Azure DNS service contains both IPv4 A and IPv6 AAAA name records and responds with both records for hello load balancer.</span></span> <span data-ttu-id="b3117-127">hello 用戶端選擇使用哪一個位址 （IPv4 或 IPv6） toocommunicate。</span><span class="sxs-lookup"><span data-stu-id="b3117-127">hello client chooses which address (IPv4 or IPv6) toocommunicate with.</span></span>
* <span data-ttu-id="b3117-128">當 VM 啟動連線 tooa 公用 IPv6 網際網路連線裝置時，hello VM 來源 IPv6 位址會是網路位址轉譯 (NAT) toohello 公用 IPv6 位址的 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="b3117-128">When a VM initiates a connection tooa public Internet IPv6-connected device, hello VM's source IPv6 address is network address translated (NAT) toohello public IPv6 address of hello load balancer.</span></span>
* <span data-ttu-id="b3117-129">執行 hello Linux 作業系統的 Vm 必須已設定的 tooreceive 透過 DHCP IPv6 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b3117-129">VMs running hello Linux operating system must be configured tooreceive an IPv6 IP address via DHCP.</span></span> <span data-ttu-id="b3117-130">許多 hello Azure 組件庫已在 hello Linux 映像設定 toosupport IPv6 而不需修改。</span><span class="sxs-lookup"><span data-stu-id="b3117-130">Many of hello Linux images in hello Azure Gallery are already configured toosupport IPv6 without modification.</span></span> <span data-ttu-id="b3117-131">如需詳細資訊，請參閱 [設定 Linux VM 的 DHCPv6](load-balancer-ipv6-for-linux.md)</span><span class="sxs-lookup"><span data-stu-id="b3117-131">For more information, see [Configuring DHCPv6 for Linux VMs](load-balancer-ipv6-for-linux.md)</span></span>
* <span data-ttu-id="b3117-132">如果您選擇的 toouse 健全狀況探查您的負載平衡器，以建立 IPv4 探查，並使用與 hello IPv4 和 IPv6 端點。</span><span class="sxs-lookup"><span data-stu-id="b3117-132">If you choose toouse a health probe with your load balancer, create an IPv4 probe and use it with both hello IPv4 and IPv6 endpoints.</span></span> <span data-ttu-id="b3117-133">如果您的 VM 上的 hello 服務關閉時，會取用 hello IPv4 和 IPv6 端點退出循環。</span><span class="sxs-lookup"><span data-stu-id="b3117-133">If hello service on your VM goes down, both hello IPv4 and IPv6 endpoints are taken out of rotation.</span></span>

<span data-ttu-id="b3117-134">限制</span><span class="sxs-lookup"><span data-stu-id="b3117-134">Limitations</span></span>

* <span data-ttu-id="b3117-135">您無法在 hello Azure 入口網站中新增 IPv6 負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="b3117-135">You cannot add IPv6 load balancing rules in hello Azure portal.</span></span> <span data-ttu-id="b3117-136">hello 規則只能建立透過 hello 範本，CLI、 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="b3117-136">hello rules can only be created through hello template, CLI, PowerShell.</span></span>
* <span data-ttu-id="b3117-137">您不可以升級現有的 Vm toouse IPv6 位址。</span><span class="sxs-lookup"><span data-stu-id="b3117-137">You may not upgrade existing VMs toouse IPv6 addresses.</span></span> <span data-ttu-id="b3117-138">您必須部署新的 VM。</span><span class="sxs-lookup"><span data-stu-id="b3117-138">You must deploy new VMs.</span></span>
* <span data-ttu-id="b3117-139">單一的 IPv6 位址可以指派每個 VM 中的 tooa 單一網路介面。</span><span class="sxs-lookup"><span data-stu-id="b3117-139">A single IPv6 address can be assigned tooa single network interface in each VM.</span></span>
* <span data-ttu-id="b3117-140">hello 公用 IPv6 位址不能指派 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="b3117-140">hello public IPv6 addresses cannot be assigned tooa VM.</span></span> <span data-ttu-id="b3117-141">它們只可以指派 tooa 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="b3117-141">They can only be assigned tooa load balancer.</span></span>
* <span data-ttu-id="b3117-142">您無法設定 hello 反向 DNS 對應，為公用的 IPv6 位址。</span><span class="sxs-lookup"><span data-stu-id="b3117-142">You cannot configure hello reverse DNS lookup for your public IPv6 addresses.</span></span>
* <span data-ttu-id="b3117-143">hello Vm 與 hello IPv6 位址不能是 Azure 雲端服務的成員。</span><span class="sxs-lookup"><span data-stu-id="b3117-143">hello VMs with hello IPv6 addresses cannot be members of an Azure Cloud Service.</span></span> <span data-ttu-id="b3117-144">它們可以連接的 tooan Azure 虛擬網路 (VNet) 和移轉的 IPv4 位址與對方進行通訊。</span><span class="sxs-lookup"><span data-stu-id="b3117-144">They can be connected tooan Azure Virtual Network (VNet) and communicate with each other over their IPv4 addresses.</span></span>
* <span data-ttu-id="b3117-145">私人 IPv6 位址可部署到資源群組中的個別 VM，但無法透過擴充集部署到資源群組。</span><span class="sxs-lookup"><span data-stu-id="b3117-145">Private IPv6 addresses can be deployed on individual VMs in a resource group but cannot be deployed into a resource group via Scale Sets.</span></span>
* <span data-ttu-id="b3117-146">Azure Vm 無法透過 IPv6 tooother Vm、 其他 Azure 服務或在內部部署裝置連線。</span><span class="sxs-lookup"><span data-stu-id="b3117-146">Azure VMs cannot connect over IPv6 tooother VMs, other Azure services, or on-premises devices.</span></span> <span data-ttu-id="b3117-147">它們只能透過 IPv6 通訊與 hello Azure 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="b3117-147">They can only communicate with hello Azure load balancer over IPv6.</span></span> <span data-ttu-id="b3117-148">不過，它們可以使用 IPv4 與這些其他資源通訊。</span><span class="sxs-lookup"><span data-stu-id="b3117-148">However, they can communicate with these other resources using IPv4.</span></span>
* <span data-ttu-id="b3117-149">雙重堆疊 (IPv4 + IPv6) 部署支援 IPv4 的網路安全性群組 (NSG) 保護。</span><span class="sxs-lookup"><span data-stu-id="b3117-149">Network Security Group (NSG) protection for IPv4 is supported in dual-stack (IPv4+IPv6) deployments.</span></span> <span data-ttu-id="b3117-150">Nsg 不會套用 toohello IPv6 端點。</span><span class="sxs-lookup"><span data-stu-id="b3117-150">NSGs do not apply toohello IPv6 endpoints.</span></span>
* <span data-ttu-id="b3117-151">上的 VM 不是的 hello hello IPv6 端點直接公開 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="b3117-151">hello IPv6 endpoint on hello VM is not exposed directly toohello internet.</span></span> <span data-ttu-id="b3117-152">而是擺在負載平衡器後。</span><span class="sxs-lookup"><span data-stu-id="b3117-152">It is behind a load balancer.</span></span> <span data-ttu-id="b3117-153">只有 hello 負載平衡器規則中指定的 hello 連接埠都可存取透過 IPv6。</span><span class="sxs-lookup"><span data-stu-id="b3117-153">Only hello ports specified in hello load balancer rules are accessible over IPv6.</span></span>
* <span data-ttu-id="b3117-154">IPv6 是變更 hello IdleTimeout 參數**目前不支援**。</span><span class="sxs-lookup"><span data-stu-id="b3117-154">Changing hello IdleTimeout parameter for IPv6 is **currently not supported**.</span></span> <span data-ttu-id="b3117-155">hello 預設值為四分鐘。</span><span class="sxs-lookup"><span data-stu-id="b3117-155">hello default is four minutes.</span></span>
* <span data-ttu-id="b3117-156">IPv6 是變更 hello loadDistributionMethod 參數**目前不支援**。</span><span class="sxs-lookup"><span data-stu-id="b3117-156">Changing hello loadDistributionMethod parameter for IPv6 is **currently not supported**.</span></span>
* <span data-ttu-id="b3117-157">**目前不支援**保留的 IPv6 IP (其中 IPAllocationMethod = 靜態)。</span><span class="sxs-lookup"><span data-stu-id="b3117-157">Reserved IPv6 IPs (where IPAllocationMethod = static) are **currently not supported**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3117-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b3117-158">Next steps</span></span>

<span data-ttu-id="b3117-159">深入了解如何 toodeploy 負載平衡器使用 IPv6。</span><span class="sxs-lookup"><span data-stu-id="b3117-159">Learn how toodeploy a load balancer with IPv6.</span></span>

* [<span data-ttu-id="b3117-160">依區域的 IPv6 可用性</span><span class="sxs-lookup"><span data-stu-id="b3117-160">Availability of IPv6 by region</span></span>](https://go.microsoft.com/fwlink/?linkid=828357)
* [<span data-ttu-id="b3117-161">使用範本部署配置有 IPv6 的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="b3117-161">Deploy a load balancer with IPv6 using a template</span></span>](load-balancer-ipv6-internet-template.md)
* [<span data-ttu-id="b3117-162">使用 Azure PowerShell 部署配置有 IPv6 的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="b3117-162">Deploy a load balancer with IPv6 using Azure PowerShell</span></span>](load-balancer-ipv6-internet-ps.md)
* [<span data-ttu-id="b3117-163">使用 Azure CLI 部署配置有 IPv6 的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="b3117-163">Deploy a load balancer with IPv6 using Azure CLI</span></span>](load-balancer-ipv6-internet-cli.md)
