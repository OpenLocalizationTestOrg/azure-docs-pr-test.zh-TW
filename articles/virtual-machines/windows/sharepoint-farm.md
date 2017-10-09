---
title: "在 Azure 中的 aaaCreate SharePoint 伺服器陣列 |Microsoft 文件"
description: "快速建立新的 SharePoint 2013 或 SharePoint 2016 伺服器陣列在 Azure 中使用 hello Azure marketplace 入口網站所提供。"
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
ms.openlocfilehash: d71c7177d9b99cf377bab767342508007285b452
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-sharepoint-server-farms-using-hello-azure-portal-marketplace"></a><span data-ttu-id="f6ed4-103">建立使用 hello Azure marketplace 入口網站所提供的 SharePoint 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="f6ed4-103">Create SharePoint server farms using hello Azure portal marketplace</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="sharepoint-2013-farms"></a><span data-ttu-id="f6ed4-104">SharePoint 2013 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="f6ed4-104">SharePoint 2013 farms</span></span>
<span data-ttu-id="f6ed4-105">您可以使用 Microsoft Azure 入口網站 marketplace hello，快速建立預先設定的 SharePoint Server 2013 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-105">With hello Microsoft Azure portal marketplace, you can quickly create pre-configured SharePoint Server 2013 farms.</span></span> <span data-ttu-id="f6ed4-106">當您在開發/測試環境中需要基本或高可用性 SharePoint 伺服器陣列時，或是您要評估將 SharePoint Server 2013 做為組織的共同作業方案時，這將可為您省下許多時間。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-106">This can save you a lot of time when you need a basic or high-availability SharePoint farm for a dev/test environment or if you are evaluating SharePoint Server 2013 as a collaboration solution for your organization.</span></span>

> [!NOTE]
> <span data-ttu-id="f6ed4-107">hello **SharePoint 伺服器陣列**hello Azure Marketplace 中的 hello Azure 入口網站的項目已經移除。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-107">hello **SharePoint Server Farm** item in hello Azure Marketplace of hello Azure portal has been removed.</span></span> <span data-ttu-id="f6ed4-108">它已被取代 hello **SharePoint 2013 非高可用性伺服器陣列**和**SharePoint 2013 的高可用性伺服器陣列**項目。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-108">It has been replaced with hello **SharePoint 2013 non-HA Farm** and **SharePoint 2013 HA Farm** items.</span></span>
>
>

<span data-ttu-id="f6ed4-109">hello 基本的 SharePoint 伺服器陣列包含在此組態中的三部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-109">hello basic SharePoint farm consists of three virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/Non-HAFarm.png)

<span data-ttu-id="f6ed4-111">此伺服器陣列組態可用於 SharePoint 應用程式開發的簡化設定，或用於您第一次的 SharePoint 2013 評估。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-111">You can use this farm configuration for a simplified setup for SharePoint app development or your first-time evaluation of SharePoint 2013.</span></span>

<span data-ttu-id="f6ed4-112">toocreate hello 基本 （三部伺服器） SharePoint 伺服陣列：</span><span class="sxs-lookup"><span data-stu-id="f6ed4-112">toocreate hello basic (three-server) SharePoint farm:</span></span>

1. <span data-ttu-id="f6ed4-113">按一下 [ [這裡](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/)]。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-113">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-nonha/).</span></span>
2. <span data-ttu-id="f6ed4-114">按一下 [ **部署**]。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-114">Click **Deploy**.</span></span>
3. <span data-ttu-id="f6ed4-115">在 hello **SharePoint 2013 非高可用性伺服器陣列** 窗格中，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-115">On hello **SharePoint 2013 non-HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="f6ed4-116">指定設定的 hello hello 步驟**建立 SharePoint 2013 非高可用性伺服器陣列** 窗格中，然後再按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-116">Specify settings on hello steps of hello **Create SharePoint 2013 non-HA Farm** pane, and then click **Create**.</span></span>

<span data-ttu-id="f6ed4-117">hello 高可用性 SharePoint 伺服器陣列包含在此組態的九個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-117">hello high-availability SharePoint farm consists of nine virtual machines in this configuration.</span></span>

![sharepointfarm](./media/sharepoint-farm/HAFarm.png)

<span data-ttu-id="f6ed4-119">您可以使用此伺服器陣列組態 tootest 更高版本用戶端負載、 hello 外部 SharePoint 網站的高可用性和 SQL Server AlwaysOn 可用性群組的 SharePoint 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-119">You can use this farm configuration tootest higher client loads, high availability of hello external SharePoint site, and SQL Server AlwaysOn Availability Groups for a SharePoint farm.</span></span> <span data-ttu-id="f6ed4-120">此組態也可用於高可用性環境中的 SharePoint 應用程式開發。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-120">You can also use this configuration for SharePoint app development in a high-availability environment.</span></span>

<span data-ttu-id="f6ed4-121">toocreate hello 高可用性 （九伺服器） SharePoint 伺服陣列：</span><span class="sxs-lookup"><span data-stu-id="f6ed4-121">toocreate hello high-availability (nine-server) SharePoint farm:</span></span>

1. <span data-ttu-id="f6ed4-122">按一下 [ [這裡](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/)]。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-122">Click [here](https://azure.microsoft.com/marketplace/partners/sharepoint2013/sharepoint2013farmsharepoint2013-ha/).</span></span>
2. <span data-ttu-id="f6ed4-123">按一下 [ **部署**]。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-123">Click **Deploy**.</span></span>
3. <span data-ttu-id="f6ed4-124">在 hello **SharePoint 2013 的高可用性伺服器陣列** 窗格中，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-124">On hello **SharePoint 2013 HA Farm** pane, click **Create**.</span></span>
4. <span data-ttu-id="f6ed4-125">在 [hello hello 七個步驟中指定設定**建立 SharePoint 2013 HA 陣列**] 窗格中，然後再按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-125">Specify settings on hello seven steps of hello **Create SharePoint 2013 HA Farm** pane, and then click **Create**.</span></span>

> [!NOTE]
> <span data-ttu-id="f6ed4-126">您無法建立 hello **SharePoint 2013 非高可用性伺服器陣列**或**SharePoint 2013 的高可用性伺服器陣列**Azure 免費試用版。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-126">You cannot create hello **SharePoint 2013 non-HA Farm** or **SharePoint 2013 HA Farm** with an Azure Free Trial.</span></span>
>
>

<span data-ttu-id="f6ed4-127">hello Azure 入口網站會建立這兩個這些伺服器陣列中純雲端虛擬網路與網際網路對向網頁存在。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-127">hello Azure portal creates both of these farms in a cloud-only virtual network with an Internet-facing web presence.</span></span> <span data-ttu-id="f6ed4-128">沒有站對站 VPN 或 ExpressRoute 連線後 tooyour 組織網路。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-128">There is no site-to-site VPN or ExpressRoute connection back tooyour organization network.</span></span>

> [!NOTE]
> <span data-ttu-id="f6ed4-129">當您建立 hello 基本或高可用性 SharePoint 伺服器陣列使用 hello Azure 入口網站，您不能指定現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-129">When you create hello basic or high-availability SharePoint farms using hello Azure portal, you cannot specify an existing resource group.</span></span> <span data-ttu-id="f6ed4-130">toowork 這項限制，使用 Azure PowerShell 建立這些陣列。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-130">toowork around this limitation, create these farms with Azure PowerShell.</span></span> <span data-ttu-id="f6ed4-131">如需詳細資訊，請參閱[使用 Azure PowerShell 建立 SharePoint 2013 開發/測試陣列](https://technet.microsoft.com/library/mt743093.aspx#powershell)。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-131">For more information, see [Create SharePoint 2013 dev/test farms with Azure PowerShell](https://technet.microsoft.com/library/mt743093.aspx#powershell).</span></span>
>
>

## <a name="sharepoint-2016-farms"></a><span data-ttu-id="f6ed4-132">SharePoint 2016 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="f6ed4-132">SharePoint 2016 farms</span></span>
<span data-ttu-id="f6ed4-133">請參閱[本文](https://technet.microsoft.com/library/mt723354.aspx)hello 指示 toobuild hello 遵循單一伺服器 SharePoint Server 2016 伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-133">See [this article](https://technet.microsoft.com/library/mt723354.aspx) for hello instructions toobuild hello following single-server SharePoint Server 2016 farm.</span></span>

![sharepointfarm](./media/sharepoint-farm/SP2016Farm.png)

## <a name="managing-hello-sharepoint-farms"></a><span data-ttu-id="f6ed4-135">管理 hello SharePoint 伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="f6ed4-135">Managing hello SharePoint farms</span></span>
<span data-ttu-id="f6ed4-136">您可以管理這些伺服器陣列，透過遠端桌面連線的 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-136">You can administer hello servers of these farms through Remote Desktop connections.</span></span> <span data-ttu-id="f6ed4-137">如需詳細資訊，請參閱[登入 toohello 虛擬機器](quick-create-portal.md#connect-to-virtual-machine)。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-137">For more information, see [Log on toohello virtual machine](quick-create-portal.md#connect-to-virtual-machine).</span></span>

<span data-ttu-id="f6ed4-138">從 hello 中央系統管理 SharePoint 網站上，您可以設定我的網站、 SharePoint 應用程式及其他功能。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-138">From hello Central Administration SharePoint site, you can configure My sites, SharePoint applications, and other functionality.</span></span> <span data-ttu-id="f6ed4-139">如需詳細資訊，請參閱 [設定 SharePoint](http://technet.microsoft.com/library/ee836142.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-139">For more information, see [Configure SharePoint](http://technet.microsoft.com/library/ee836142.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6ed4-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f6ed4-140">Next steps</span></span>
* <span data-ttu-id="f6ed4-141">探索 Azure 基礎結構服務中的其他 [SharePoint 組態](https://technet.microsoft.com/library/dn635309.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="f6ed4-141">Discover additional [SharePoint configurations](https://technet.microsoft.com/library/dn635309.aspx) in Azure infrastructure services.</span></span>
