---
title: "在 Azure 中建立 SharePoint 伺服器陣列 | Microsoft Docs"
description: "使用 Azure 入口網站 Marketplace 在 Azure 中快速建立新的 SharePoint 2013 或 SharePoint 2016 陣列。"
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 89b124da-019d-4179-86dd-ad418d05a4f2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 00648ee35962b22fb7eeceaa6d9df7305c801abf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-sharepoint-server-farms-using-the-azure-portal-marketplace"></a><span data-ttu-id="5ca76-103">使用 Azure 入口網站 Marketplace 建立 SharePoint 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="5ca76-103">Create SharePoint server farms using the Azure portal marketplace</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a><span data-ttu-id="5ca76-104">SharePoint 2013 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="5ca76-104">SharePoint 2013 farms</span></span>
<span data-ttu-id="5ca76-105">透過 Microsoft Azure 入口網站的 Marketplace，您可以快速建立預先設定的 SharePoint Server 2013 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="5ca76-105">With the Microsoft Azure portal marketplace, you can quickly create pre-configured SharePoint Server 2013 farms.</span></span> <span data-ttu-id="5ca76-106">當您在開發/測試環境中需要基本或高可用性 SharePoint 伺服器陣列時，或是您要評估將 SharePoint Server 2013 做為組織的共同作業方案時，這將可為您省下許多時間。</span><span class="sxs-lookup"><span data-stu-id="5ca76-106">This can save you a lot of time when you need a basic or high-availability SharePoint farm for a dev/test environment or if you are evaluating SharePoint Server 2013 as a collaboration solution for your organization.</span></span>

> [!NOTE]
> <span data-ttu-id="5ca76-107">Azure 入口網站的 Azure Marketplace 中的 **SharePoint 伺服器陣列** 項目已移除。</span><span class="sxs-lookup"><span data-stu-id="5ca76-107">The **SharePoint Server Farm** item in the Azure Marketplace of the Azure portal has been removed.</span></span> <span data-ttu-id="5ca76-108">已由「SharePoint 2013 非 HA 伺服器陣列」和「SharePoint 2013 HA 伺服器陣列」項目將其取代。</span><span class="sxs-lookup"><span data-stu-id="5ca76-108">It has been replaced with the **SharePoint 2013 non-HA Farm** and **SharePoint 2013 HA Farm** items.</span></span>
>
>

<span data-ttu-id="5ca76-109">基本的 SharePoint 伺服器陣列由這個組態中的三部虛擬機器所組成。</span><span class="sxs-lookup"><span data-stu-id="5ca76-109">The basic SharePoint farm consists of three virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

<span data-ttu-id="5ca76-111">此伺服器陣列組態可用於 SharePoint 應用程式開發的簡化設定，或用於您第一次的 SharePoint 2013 評估。</span><span class="sxs-lookup"><span data-stu-id="5ca76-111">You can use this farm configuration for a simplified setup for SharePoint app development or your first-time evaluation of SharePoint 2013.</span></span>

<span data-ttu-id="5ca76-112">若要建立基本 (三部伺服器) 的 SharePoint 伺服器陣列：</span><span class="sxs-lookup"><span data-stu-id="5ca76-112">To create the basic (three-server) SharePoint farm:</span></span>

1. <span data-ttu-id="5ca76-113">按一下 [ [這裡](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/)]。</span><span class="sxs-lookup"><span data-stu-id="5ca76-113">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span></span>
2. <span data-ttu-id="5ca76-114">按一下 [ **部署**]。</span><span class="sxs-lookup"><span data-stu-id="5ca76-114">Click **Deploy**.</span></span>
3. <span data-ttu-id="5ca76-115">在 [SharePoint 2013 非 HA 伺服器陣列] 窗格中，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="5ca76-115">On the **SharePoint 2013 non-HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="5ca76-116">在 [建立 SharePoint 2013 非 HA 伺服器陣列] 窗格中，指定步驟的相關設定，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="5ca76-116">Specify settings on the steps of the **Create SharePoint 2013 non-HA Farm** pane, and then click **Create**.</span></span>

<span data-ttu-id="5ca76-117">高可用性 SharePoint 伺服器陣列由下列組態中的九個虛擬機器組成。</span><span class="sxs-lookup"><span data-stu-id="5ca76-117">The high-availability SharePoint farm consists of nine virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

<span data-ttu-id="5ca76-119">此伺服器陣列組態可用來測試較高的用戶端負載、外部 SharePoint 網站的高可用性，以及 SharePoint 伺服器陣列的 SQL Server AlwaysOn 可用性群組。</span><span class="sxs-lookup"><span data-stu-id="5ca76-119">You can use this farm configuration to test higher client loads, high availability of the external SharePoint site, and SQL Server AlwaysOn Availability Groups for a SharePoint farm.</span></span> <span data-ttu-id="5ca76-120">此組態也可用於高可用性環境中的 SharePoint 應用程式開發。</span><span class="sxs-lookup"><span data-stu-id="5ca76-120">You can also use this configuration for SharePoint app development in a high-availability environment.</span></span>

<span data-ttu-id="5ca76-121">若要建立高可用性 (九部伺服器) 的 SharePoint 伺服器陣列：</span><span class="sxs-lookup"><span data-stu-id="5ca76-121">To create the high-availability (nine-server) SharePoint farm:</span></span>

1. <span data-ttu-id="5ca76-122">按一下 [ [這裡](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/)]。</span><span class="sxs-lookup"><span data-stu-id="5ca76-122">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span></span>
2. <span data-ttu-id="5ca76-123">按一下 [ **部署**]。</span><span class="sxs-lookup"><span data-stu-id="5ca76-123">Click **Deploy**.</span></span>
3. <span data-ttu-id="5ca76-124">在 [SharePoint 2013 HA 伺服器陣列] 窗格中，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="5ca76-124">On the **SharePoint 2013 HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="5ca76-125">在 [建立 SharePoint 2013 HA 伺服器陣列] 窗格的七個步驟中指定設定，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="5ca76-125">Specify settings on the seven steps of the **Create SharePoint 2013 HA Farm** pane, and then click **Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="5ca76-126">您無法使用「Azure 免費試用版」來建立「SharePoint 2013 非 HA 伺服器陣列」或「SharePoint 2013 HA 伺服器陣列」。</span><span class="sxs-lookup"><span data-stu-id="5ca76-126">You cannot create the **SharePoint 2013 non-HA Farm** or **SharePoint 2013 HA Farm** with an Azure Free Trial.</span></span>
>
>

<span data-ttu-id="5ca76-127">Azure 入口網站會在具有網際網路對向網站空間的純雲端虛擬網路中，同時建立這兩種伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="5ca76-127">The Azure portal creates both of these farms in a cloud-only virtual network with an Internet-facing web presence.</span></span> <span data-ttu-id="5ca76-128">沒有任何站對站 VPN 或 ExpressRoute 連線會連回您的組織網路。</span><span class="sxs-lookup"><span data-stu-id="5ca76-128">There is no site-to-site VPN or ExpressRoute connection back to your organization network.</span></span>

> [!NOTE]
> <span data-ttu-id="5ca76-129">當您使用 Azure 入口網站建立基本或高可用性 SharePoint 陣列時，您不能指定現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="5ca76-129">When you create the basic or high-availability SharePoint farms using the Azure portal, you cannot specify an existing resource group.</span></span> <span data-ttu-id="5ca76-130">若要解決這項限制，請使用 Azure PowerShell 建立這些陣列。</span><span class="sxs-lookup"><span data-stu-id="5ca76-130">To work around this limitation, create these farms with Azure PowerShell.</span></span> <span data-ttu-id="5ca76-131">如需詳細資訊，請參閱[使用 Azure PowerShell 建立 SharePoint 2013 開發/測試陣列](https://technet.microsoft.com/library/mt743093.aspx#powershell)。</span><span class="sxs-lookup"><span data-stu-id="5ca76-131">For more information, see [Create SharePoint 2013 dev/test farms with Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span></span>
>
>

## <a name="sharepoint-2016-farms"></a><span data-ttu-id="5ca76-132">SharePoint 2016 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="5ca76-132">SharePoint 2016 farms</span></span>
<span data-ttu-id="5ca76-133">如需如何建置下列單一伺服器 SharePoint Server 2016 陣列的相關指示，請參閱 [這個主題](https://technet.microsoft.com/library/mt723354.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="5ca76-133">See [this article](https://technet.microsoft.com/library/mt723354.aspx) for the instructions to build the following single-server SharePoint Server 2016 farm.</span></span>

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-the-sharepoint-farms"></a><span data-ttu-id="5ca76-135">管理 SharePoint 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="5ca76-135">Managing the SharePoint farms</span></span>
<span data-ttu-id="5ca76-136">您可以透過遠端桌面連接管理這些伺服器陣列的伺服器。</span><span class="sxs-lookup"><span data-stu-id="5ca76-136">You can administer the servers of these farms through Remote Desktop connections.</span></span> <span data-ttu-id="5ca76-137">如需詳細資訊，請參閱 [登入虛擬機器](quick-create-portal.md#connect-to-virtual-machine)。</span><span class="sxs-lookup"><span data-stu-id="5ca76-137">For more information, see [Log on to the virtual machine](quick-create-portal.md#connect-to-virtual-machine).</span></span>

<span data-ttu-id="5ca76-138">在「管理中心 SharePoint」網站中，您可以設定「我的網站」、SharePoint 應用程式和其他功能。</span><span class="sxs-lookup"><span data-stu-id="5ca76-138">From the Central Administration SharePoint site, you can configure My sites, SharePoint applications, and other functionality.</span></span> <span data-ttu-id="5ca76-139">如需詳細資訊，請參閱 [設定 SharePoint](http://technet.microsoft.com/library/ee836142.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5ca76-139">For more information, see [Configure SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ca76-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5ca76-140">Next steps</span></span>
* <span data-ttu-id="5ca76-141">探索 Azure 基礎結構服務中的其他 [SharePoint 組態](https://technet.microsoft.com/library/dn635309.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="5ca76-141">Discover additional [SharePoint configurations](https://technet.microsoft.com/library/dn635309.aspx) in Azure infrastructure services.</span></span>
