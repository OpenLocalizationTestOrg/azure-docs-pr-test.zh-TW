---
title: "從 VNET 連接到 Azure Data Lake Store | Microsoft Docs"
description: "從 Azure VNET 連接到 Azure Data Lake Store"
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 683fcfdc-cf93-46c3-b2d2-5cb79f5e9ea5
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ff7d28d7b53e872b804788647b1e672fafcf6995
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="access-azure-data-lake-store-from-vms-within-an-azure-vnet"></a><span data-ttu-id="62212-103">從 Azure VNET 內的 VM 存取 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="62212-103">Access Azure Data Lake Store from VMs within an Azure VNET</span></span>
<span data-ttu-id="62212-104">Azure Data Lake Store 使用公用網際網路 IP 位址執行的 PaaS 服務。</span><span class="sxs-lookup"><span data-stu-id="62212-104">Azure Data Lake Store is a PaaS service that runs on public Internet IP addresses.</span></span> <span data-ttu-id="62212-105">可以連線到公用網際網路的任何伺服器，通常也可以連接到 Azure Data Lake Store 端點。</span><span class="sxs-lookup"><span data-stu-id="62212-105">Any server that can connect to the public Internet can typically connect to Azure Data Lake Store endpoints as well.</span></span> <span data-ttu-id="62212-106">根據預設，Azure VNET 中所有的 VM 可以存取網際網路，並因此可以存取 Azure Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="62212-106">By default, all VMs that are in Azure VNETs can access the Internet and hence can access Azure Data Lake Store.</span></span> <span data-ttu-id="62212-107">不過，也可以將 VNET 中的 VM 設定為無法存取網際網路。</span><span class="sxs-lookup"><span data-stu-id="62212-107">However, it is possible to configure VMs in a VNET to not have access to the Internet.</span></span> <span data-ttu-id="62212-108">對於這類 VM，也會限制對 Azure Data Lake Store 的存取。</span><span class="sxs-lookup"><span data-stu-id="62212-108">For such VMs, access to Azure Data Lake Store is restricted as well.</span></span> <span data-ttu-id="62212-109">封鎖 Azure VNET 中 VM 的公用網際網路存取，可以使用下列方法的任一個來完成。</span><span class="sxs-lookup"><span data-stu-id="62212-109">Blocking public Internet access for VMs in Azure VNETs can be done using any of the following approach.</span></span>

* <span data-ttu-id="62212-110">藉由設定網路安全性群組 (NSG)</span><span class="sxs-lookup"><span data-stu-id="62212-110">By configuring Network Security Groups (NSG)</span></span>
* <span data-ttu-id="62212-111">藉由設定使用者定義路由 (UDR)</span><span class="sxs-lookup"><span data-stu-id="62212-111">By configuring User Defined Routes (UDR)</span></span>
* <span data-ttu-id="62212-112">在使用可封鎖網際網路存取的 ExpressRoute 時，透過 BGP (產業標準動態路由通訊協定) 交換路由</span><span class="sxs-lookup"><span data-stu-id="62212-112">By exchanging routes via BGP (industry standard dynamic routing protocol) when ExpressRoute is used that block access to the Internet</span></span>

<span data-ttu-id="62212-113">在本文中，您將學習如何從已使用上述三種方法之一被限制存取資源的 Azure VM 啟用對 Azure Data Lake Store 的存取。</span><span class="sxs-lookup"><span data-stu-id="62212-113">In this article, you will learn how to enable access to the Azure Data Lake Store from Azure VMs which have been restricted to access resources using one of the three methods listed above.</span></span>

## <a name="enabling-connectivity-to-azure-data-lake-store-from-vms-with-restricted-connectivity"></a><span data-ttu-id="62212-114">從具有受限制連線的 VM 啟用對 Azure Data Lake Store 的連線</span><span class="sxs-lookup"><span data-stu-id="62212-114">Enabling connectivity to Azure Data Lake Store from VMs with restricted connectivity</span></span>
<span data-ttu-id="62212-115">若要從這類 VM 存取 Azure Data Lake Store ，您必須對其設定，以存取 Azure Data Lake Store 帳戶可供使用的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="62212-115">To access Azure Data Lake Store from such VMs, you must configure them to access the IP address where the Azure Data Lake Store account is available.</span></span> <span data-ttu-id="62212-116">您可以透過解析您的帳戶 (`<account>.azuredatalakestore.net`) 的 DNS 名稱來識別 Data Lake Store 帳戶的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="62212-116">You can identify the IP addresses for your Data Lake Store accounts by resolving the DNS names of your accounts (`<account>.azuredatalakestore.net`).</span></span> <span data-ttu-id="62212-117">對此您可以使用 **nslookup** 之類的工具。</span><span class="sxs-lookup"><span data-stu-id="62212-117">For this you can use tools such as **nslookup**.</span></span> <span data-ttu-id="62212-118">在您的電腦上開啟命令提示字元，並執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="62212-118">Open a command prompt on your computer and run the following command.</span></span>

    nslookup mydatastore.azuredatalakestore.net

<span data-ttu-id="62212-119">輸出結果類似下面。</span><span class="sxs-lookup"><span data-stu-id="62212-119">The output resembles the following.</span></span> <span data-ttu-id="62212-120">**Address** 屬性的值是與您的 Data Lake Store 帳戶相關聯的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="62212-120">The value against **Address** property is the IP address associated with your Data Lake Store account.</span></span>

    Non-authoritative answer:
    Name:    1434ceb1-3a4b-4bc0-9c69-a0823fd69bba-mydatastore.projectcabostore.net
    Address:  104.44.88.112
    Aliases:  mydatastore.azuredatalakestore.net


### <a name="enabling-connectivity-from-vms-restricted-by-using-nsg"></a><span data-ttu-id="62212-121">使用 NSG 從受限制的 VM 啟用連線</span><span class="sxs-lookup"><span data-stu-id="62212-121">Enabling connectivity from VMs restricted by using NSG</span></span>
<span data-ttu-id="62212-122">使用 NSG 規則來封鎖對網際網路的存取時，您可以建立允許存取 Data Lake Store IP 位址的另一個 NSG。</span><span class="sxs-lookup"><span data-stu-id="62212-122">When a NSG rule is used to block access to the Internet, then you can create another NSG that allows access to the Data Lake Store IP Address.</span></span> <span data-ttu-id="62212-123">NSG 規則的詳細資訊位於[什麼是網路安全性群組？](../virtual-network/virtual-networks-nsg.md)。</span><span class="sxs-lookup"><span data-stu-id="62212-123">More information on NSG rules is available at [What is a Network Security Group?](../virtual-network/virtual-networks-nsg.md).</span></span> <span data-ttu-id="62212-124">如需如何建立 NSG 的指示，請參閱[如何使用 Azure 入口網站管理 NSG](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="62212-124">For instructions on how to create NSGs see [How to manage NSGs using the Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>

### <a name="enabling-connectivity-from-vms-restricted-by-using-udr-or-expressroute"></a><span data-ttu-id="62212-125">使用 UDR 或 ExpressRoute 從受限制的 VM 啟用連線</span><span class="sxs-lookup"><span data-stu-id="62212-125">Enabling connectivity from VMs restricted by using UDR or ExpressRoute</span></span>
<span data-ttu-id="62212-126">路由時會使用 UDR 或 BGP 交換路由來封鎖對網際網路的存取，必須設定特殊的路由，才能使這類子網路中的 VM 可以存取 Data Lake Store 端點。</span><span class="sxs-lookup"><span data-stu-id="62212-126">When routes, either UDRs or BGP-exchanged routes, are used to block access to the Internet, a special route needs to be configured so that VMs in such subnets can access Data Lake Store endpoints.</span></span> <span data-ttu-id="62212-127">如需詳細資訊，請參閱[什麼是使用者定義路由？](../virtual-network/virtual-networks-udr-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="62212-127">For more information, see [What are User Defined Routes?](../virtual-network/virtual-networks-udr-overview.md).</span></span> <span data-ttu-id="62212-128">如需建立 UDR 的指示，請參閱[在 Resource Manager 中建立 UDR](../virtual-network/virtual-network-create-udr-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="62212-128">For instructions on creating UDRs, see [Create UDRs in Resource Manager](../virtual-network/virtual-network-create-udr-arm-ps.md).</span></span>

### <a name="enabling-connectivity-from-vms-restricted-by-using-expressroute"></a><span data-ttu-id="62212-129">使用 ExpressRoute 從受限制的 VM 啟用連線</span><span class="sxs-lookup"><span data-stu-id="62212-129">Enabling connectivity from VMs restricted by using ExpressRoute</span></span>
<span data-ttu-id="62212-130">設定 ExpressRoute 電路時，內部部署伺服器可以透過公用對等互連來存取 Data Lake Store。</span><span class="sxs-lookup"><span data-stu-id="62212-130">When an ExpressRoute circuit is configured, the on-premises servers can access Data Lake Store through public peering.</span></span> <span data-ttu-id="62212-131">如需針對公用互連設定 ExpressRoute 的詳細資訊，請參閱 [ExpressRoute 常見問題集](../expressroute/expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="62212-131">More details on configuring ExpressRoute for public peering is available at [ExpressRoute FAQs](../expressroute/expressroute-faqs.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="62212-132">另請參閱</span><span class="sxs-lookup"><span data-stu-id="62212-132">See also</span></span>
* [<span data-ttu-id="62212-133">Azure 資料湖儲存區概觀</span><span class="sxs-lookup"><span data-stu-id="62212-133">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
* [<span data-ttu-id="62212-134">保護儲存在 Azure Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="62212-134">Securing data stored in Azure Data Lake Store</span></span>](data-lake-store-security-overview.md)

