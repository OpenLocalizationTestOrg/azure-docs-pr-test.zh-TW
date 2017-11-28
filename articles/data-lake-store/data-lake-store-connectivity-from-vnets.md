---
title: "aaaConnect tooAzure 資料湖存放區從 Vnet |Microsoft 文件"
description: "從 Azure Vnet 連接 tooAzure 資料湖存放區"
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
ms.openlocfilehash: c695dcf49fe4e1a87a90729cf085a938f3b51fe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="access-azure-data-lake-store-from-vms-within-an-azure-vnet"></a><span data-ttu-id="0866e-103">從 Azure VNET 內的 VM 存取 Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0866e-103">Access Azure Data Lake Store from VMs within an Azure VNET</span></span>
<span data-ttu-id="0866e-104">Azure Data Lake Store 使用公用網際網路 IP 位址執行的 PaaS 服務。</span><span class="sxs-lookup"><span data-stu-id="0866e-104">Azure Data Lake Store is a PaaS service that runs on public Internet IP addresses.</span></span> <span data-ttu-id="0866e-105">通常可以連接 toohello 公用網際網路可以任何伺服器連接 tooAzure Data Lake Store 端點。</span><span class="sxs-lookup"><span data-stu-id="0866e-105">Any server that can connect toohello public Internet can typically connect tooAzure Data Lake Store endpoints as well.</span></span> <span data-ttu-id="0866e-106">根據預設，Azure Vnet 中的所有 Vm 可以存取 hello 網際網路，並且因此可存取 Azure 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="0866e-106">By default, all VMs that are in Azure VNETs can access hello Internet and hence can access Azure Data Lake Store.</span></span> <span data-ttu-id="0866e-107">不過，很可能 tooconfigure Vm 在 VNET toonot 有存取 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="0866e-107">However, it is possible tooconfigure VMs in a VNET toonot have access toohello Internet.</span></span> <span data-ttu-id="0866e-108">對於這類的 Vm，存取 tooAzure 資料湖存放區也會是受限制。</span><span class="sxs-lookup"><span data-stu-id="0866e-108">For such VMs, access tooAzure Data Lake Store is restricted as well.</span></span> <span data-ttu-id="0866e-109">封鎖公用網際網路存取 Azure Vnet 中的 Vm，才可以使用任何 hello 遵循方法。</span><span class="sxs-lookup"><span data-stu-id="0866e-109">Blocking public Internet access for VMs in Azure VNETs can be done using any of hello following approach.</span></span>

* <span data-ttu-id="0866e-110">藉由設定網路安全性群組 (NSG)</span><span class="sxs-lookup"><span data-stu-id="0866e-110">By configuring Network Security Groups (NSG)</span></span>
* <span data-ttu-id="0866e-111">藉由設定使用者定義路由 (UDR)</span><span class="sxs-lookup"><span data-stu-id="0866e-111">By configuring User Defined Routes (UDR)</span></span>
* <span data-ttu-id="0866e-112">藉由交換路由 BGP （業界標準動態路由通訊協定） 透過 ExpressRoute 使用該區塊時存取 toohello 網際網路</span><span class="sxs-lookup"><span data-stu-id="0866e-112">By exchanging routes via BGP (industry standard dynamic routing protocol) when ExpressRoute is used that block access toohello Internet</span></span>

<span data-ttu-id="0866e-113">在本文中，您將學習 tooenable 如何從 Azure Vm 已經限制的 tooaccess 上面所列的其中一種 hello 三種方法使用的資源存取 toohello Azure 資料湖存放區。</span><span class="sxs-lookup"><span data-stu-id="0866e-113">In this article, you will learn how tooenable access toohello Azure Data Lake Store from Azure VMs which have been restricted tooaccess resources using one of hello three methods listed above.</span></span>

## <a name="enabling-connectivity-tooazure-data-lake-store-from-vms-with-restricted-connectivity"></a><span data-ttu-id="0866e-114">使用受限制的連線啟用連線 tooAzure Vm 所傳來的資料湖存放區</span><span class="sxs-lookup"><span data-stu-id="0866e-114">Enabling connectivity tooAzure Data Lake Store from VMs with restricted connectivity</span></span>
<span data-ttu-id="0866e-115">tooaccess Azure 資料湖存放區從這類 Vm，您必須設定這些 tooaccess hello Azure Data Lake Store 帳戶所在的 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0866e-115">tooaccess Azure Data Lake Store from such VMs, you must configure them tooaccess hello IP address where hello Azure Data Lake Store account is available.</span></span> <span data-ttu-id="0866e-116">您也可以解決您的帳戶 hello DNS 名稱的 Data Lake Store 帳戶識別 hello IP 位址 (`<account>.azuredatalakestore.net`)。</span><span class="sxs-lookup"><span data-stu-id="0866e-116">You can identify hello IP addresses for your Data Lake Store accounts by resolving hello DNS names of your accounts (`<account>.azuredatalakestore.net`).</span></span> <span data-ttu-id="0866e-117">對此您可以使用 **nslookup** 之類的工具。</span><span class="sxs-lookup"><span data-stu-id="0866e-117">For this you can use tools such as **nslookup**.</span></span> <span data-ttu-id="0866e-118">開啟您的電腦上的命令提示字元並執行下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="0866e-118">Open a command prompt on your computer and run hello following command.</span></span>

    nslookup mydatastore.azuredatalakestore.net

<span data-ttu-id="0866e-119">hello 輸出看起來像下列 hello。</span><span class="sxs-lookup"><span data-stu-id="0866e-119">hello output resembles hello following.</span></span> <span data-ttu-id="0866e-120">hello 根據值**位址**屬性是 hello Data Lake Store 帳戶相關聯的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0866e-120">hello value against **Address** property is hello IP address associated with your Data Lake Store account.</span></span>

    Non-authoritative answer:
    Name:    1434ceb1-3a4b-4bc0-9c69-a0823fd69bba-mydatastore.projectcabostore.net
    Address:  104.44.88.112
    Aliases:  mydatastore.azuredatalakestore.net


### <a name="enabling-connectivity-from-vms-restricted-by-using-nsg"></a><span data-ttu-id="0866e-121">使用 NSG 從受限制的 VM 啟用連線</span><span class="sxs-lookup"><span data-stu-id="0866e-121">Enabling connectivity from VMs restricted by using NSG</span></span>
<span data-ttu-id="0866e-122">當 NSG 規則為內部使用 tooblock 會存取 toohello 網際網路，那麼您可以建立另一個 NSG 可存取 toohello 資料湖存放區的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0866e-122">When a NSG rule is used tooblock access toohello Internet, then you can create another NSG that allows access toohello Data Lake Store IP Address.</span></span> <span data-ttu-id="0866e-123">NSG 規則的詳細資訊位於[什麼是網路安全性群組？](../virtual-network/virtual-networks-nsg.md)。</span><span class="sxs-lookup"><span data-stu-id="0866e-123">More information on NSG rules is available at [What is a Network Security Group?](../virtual-network/virtual-networks-nsg.md).</span></span> <span data-ttu-id="0866e-124">如需有關如何查看 toocreate Nsg 指示[toomanage Nsg 使用 hello Azure 入口網站的方式](../virtual-network/virtual-networks-create-nsg-arm-pportal.md)。</span><span class="sxs-lookup"><span data-stu-id="0866e-124">For instructions on how toocreate NSGs see [How toomanage NSGs using hello Azure portal](../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>

### <a name="enabling-connectivity-from-vms-restricted-by-using-udr-or-expressroute"></a><span data-ttu-id="0866e-125">使用 UDR 或 ExpressRoute 從受限制的 VM 啟用連線</span><span class="sxs-lookup"><span data-stu-id="0866e-125">Enabling connectivity from VMs restricted by using UDR or ExpressRoute</span></span>
<span data-ttu-id="0866e-126">使用的 tooblock 存取 toohello 網際網路 UDRs 或 BGP 交換路由的路由時，特殊的路由必須 toobe 設定，讓這類的子網路中的 Vm 可以存取資料湖存放區的端點。</span><span class="sxs-lookup"><span data-stu-id="0866e-126">When routes, either UDRs or BGP-exchanged routes, are used tooblock access toohello Internet, a special route needs toobe configured so that VMs in such subnets can access Data Lake Store endpoints.</span></span> <span data-ttu-id="0866e-127">如需詳細資訊，請參閱[什麼是使用者定義路由？](../virtual-network/virtual-networks-udr-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0866e-127">For more information, see [What are User Defined Routes?](../virtual-network/virtual-networks-udr-overview.md).</span></span> <span data-ttu-id="0866e-128">如需建立 UDR 的指示，請參閱[在 Resource Manager 中建立 UDR](../virtual-network/virtual-network-create-udr-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="0866e-128">For instructions on creating UDRs, see [Create UDRs in Resource Manager](../virtual-network/virtual-network-create-udr-arm-ps.md).</span></span>

### <a name="enabling-connectivity-from-vms-restricted-by-using-expressroute"></a><span data-ttu-id="0866e-129">使用 ExpressRoute 從受限制的 VM 啟用連線</span><span class="sxs-lookup"><span data-stu-id="0866e-129">Enabling connectivity from VMs restricted by using ExpressRoute</span></span>
<span data-ttu-id="0866e-130">當設定 ExpressRoute 電路時，hello 在內部部署伺服器可以存取資料湖存放區透過公用互連。</span><span class="sxs-lookup"><span data-stu-id="0866e-130">When an ExpressRoute circuit is configured, hello on-premises servers can access Data Lake Store through public peering.</span></span> <span data-ttu-id="0866e-131">如需針對公用互連設定 ExpressRoute 的詳細資訊，請參閱 [ExpressRoute 常見問題集](../expressroute/expressroute-faqs.md)。</span><span class="sxs-lookup"><span data-stu-id="0866e-131">More details on configuring ExpressRoute for public peering is available at [ExpressRoute FAQs](../expressroute/expressroute-faqs.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="0866e-132">另請參閱</span><span class="sxs-lookup"><span data-stu-id="0866e-132">See also</span></span>
* [<span data-ttu-id="0866e-133">Azure 資料湖儲存區概觀</span><span class="sxs-lookup"><span data-stu-id="0866e-133">Overview of Azure Data Lake Store</span></span>](data-lake-store-overview.md)
* [<span data-ttu-id="0866e-134">保護儲存在 Azure Data Lake Store 中的資料</span><span class="sxs-lookup"><span data-stu-id="0866e-134">Securing data stored in Azure Data Lake Store</span></span>](data-lake-store-security-overview.md)

