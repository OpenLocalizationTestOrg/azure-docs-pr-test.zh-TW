---
title: "Azure Stack 中的區域管理 | Microsoft Docs"
description: "Azure Stack 中的區域管理概觀。"
services: azure-stack
documentationcenter: 
author: efemmano
manager: dsavage
editor: 
ms.assetid: e94775d5-d473-4c03-9f4e-ae2eada67c6c
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: efemmano
ms.openlocfilehash: 15a3bc9dce3cc76f98816ba5c88066fdc23cdbe1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="region-management-in-azure-stack"></a><span data-ttu-id="bb3d3-103">Azure Stack 中的區域管理</span><span class="sxs-lookup"><span data-stu-id="bb3d3-103">Region management in Azure Stack</span></span>
<span data-ttu-id="bb3d3-104">Azure Stack 具有區域概念，也就是由邏輯實體組成硬體資源以形成 Azure Stack 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-104">Azure Stack has the concept of regions, which are logical entities comprised of the hardware resources that make up the Azure Stack infrastructure.</span></span> <span data-ttu-id="bb3d3-105">在區域管理內，您可以找到成功操作 Azure Stack 基礎結構生命週期所需的所有資源。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-105">Inside Region management, you can find all resources that are required to successfully operate the Azure Stack infrastructure lifecycle.</span></span>

<span data-ttu-id="bb3d3-106">Azure Stack 開發套件屬於單一節點部署，且等於一個區域。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-106">The Azure Stack Development Kit is a single-node deployment, and equals one region.</span></span> <span data-ttu-id="bb3d3-107">如果您在不同硬體上設定 Azure Stack 開發套件的另一個執行個體，則此執行個體屬於不同的區域。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-107">If you set up another instance of the Azure Stack Development Kit on separate hardware, this instance is a different region.</span></span>

## <a name="information-available-through-the-region-management-tile"></a><span data-ttu-id="bb3d3-108">您可以透過 [區域管理] 磚取得資訊</span><span class="sxs-lookup"><span data-stu-id="bb3d3-108">Information available through the Region Management tile</span></span>
<span data-ttu-id="bb3d3-109">Azure Stack 具有一組可用於 [區域管理] 磚的區域管理功能。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-109">Azure Stack has a set of region management capabilities available in the **Region management** tile.</span></span> <span data-ttu-id="bb3d3-110">雲端系統管理員可以在系統管理員入口網站中的預設儀表板上存取此磚。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-110">This tile is available to a cloud administrator on the default dashboard in the administrator portal.</span></span> <span data-ttu-id="bb3d3-111">您可以透過此磚來監視和更新特定區域的 Azure Stack 區域及其元件。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-111">Through this tile, you can monitor and update your Azure Stack region and its components, which are region-specific.</span></span>

 ![區域管理磚](media/azure-stack-manage-region/image1.png)

 <span data-ttu-id="bb3d3-113">如果您按一下 [區域管理] 磚中的區域，則可以存取下列資訊：</span><span class="sxs-lookup"><span data-stu-id="bb3d3-113">If you click a region in the Region management tile, you can access the following information:</span></span>

  ![[區域管理] 刀鋒視窗上的窗格說明](media/azure-stack-manage-region/image2.png)

1. <span data-ttu-id="bb3d3-115">[資源功能表]。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-115">**The resource menu**.</span></span> <span data-ttu-id="bb3d3-116">您可以在這裡存取特定的基礎結構管理領域，以及檢視和管理租用戶資源，例如儲存體帳戶和虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-116">Here, you can access specific infrastructure management areas, and view and manage tenant resources such as storage accounts and virtual networks.</span></span>

2. <span data-ttu-id="bb3d3-117">**警示**。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-117">**Alerts**.</span></span> <span data-ttu-id="bb3d3-118">此磚會列出全系統警示，並提供每個警示的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-118">This tile lists system-wide alerts and provides details on each of those alerts.</span></span>

3. <span data-ttu-id="bb3d3-119">**更新**。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-119">**Updates**.</span></span> <span data-ttu-id="bb3d3-120">在此磚中，您可以檢視 Azure Stack 基礎結構的目前版本。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-120">In this tile, you can view the current version of your Azure Stack infrastructure.</span></span>

4. <span data-ttu-id="bb3d3-121">**資源提供者**。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-121">**Resource providers**.</span></span> <span data-ttu-id="bb3d3-122">資源提供者是可讓您管理執行 Azure Stack 時所需元件所提供之租用戶功能的位置。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-122">Resource providers is the place to manage the tenant functionality offered by the components required to run Azure Stack.</span></span> <span data-ttu-id="bb3d3-123">每個資源提供者皆隨附系統管理體驗。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-123">Each resource provider comes with an administrative experience.</span></span> <span data-ttu-id="bb3d3-124">這項體驗可能包含特定提供者的警示、度量以及其他資源提供者專屬的管理功能。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-124">This experience can include alerts for the specific provider, metrics, and other management capabilities specific to the resource provider.</span></span>
 
5. <span data-ttu-id="bb3d3-125">**基礎結構角色**。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-125">**Infrastructure roles**.</span></span> <span data-ttu-id="bb3d3-126">基礎結構角色是執行 Azure Stack 時所需的元件。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-126">Infrastructure roles are the components necessary to run Azure Stack.</span></span> <span data-ttu-id="bb3d3-127">僅報告警示的基礎結構角色會列出。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-127">Only the infrastructure roles that report alerts are listed.</span></span> <span data-ttu-id="bb3d3-128">您可以按一下角色來檢視與特定角色相關聯的警示，以及此角色執行所在的角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-128">By clicking a role, you can view the alerts associated with the specific role and the role instances where this role is running.</span></span> <span data-ttu-id="bb3d3-129">儘管包含啟動、重新啟動，或關閉基礎結構角色執行個體的功能，請**勿**在開發套件環境中執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-129">Although there is the capability to start, restart, or shut down an infrastructure role instance, do **not** do this in a development kit environment.</span></span> <span data-ttu-id="bb3d3-130">這些選項僅專為每個基礎結構角色具有多個角色執行個體的多節點環境而設計。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-130">These options are designed only for a multi-node environment, where there is more than one role instance per infrastructure role.</span></span> <span data-ttu-id="bb3d3-131">重新啟動開發套件中的角色執行個體 (特別是 AzS-Xrp01) 會導致系統不穩定。</span><span class="sxs-lookup"><span data-stu-id="bb3d3-131">Restarting a role instance (especially AzS-Xrp01) in the development kit causes system instability.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb3d3-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bb3d3-132">Next steps</span></span>
[<span data-ttu-id="bb3d3-133">在 Azure Stack 中監視健康情況和警示</span><span class="sxs-lookup"><span data-stu-id="bb3d3-133">Monitor health and alerts in Azure Stack</span></span>](azure-stack-monitor-health.md)

[<span data-ttu-id="bb3d3-134">在 Azure Stack 中管理更新</span><span class="sxs-lookup"><span data-stu-id="bb3d3-134">Manage updates in Azure Stack</span></span>](azure-stack-updates.md)






