---
title: "在 Azure Stack 中監視健康情況和警示 | Microsoft Docs"
description: "了解如何在 Azure Stack 中監視健康情況和警示。"
services: azure-stack
documentationcenter: 
author: chasat-MS
manager: dsavage
editor: 
ms.assetid: 69901c7b-4673-4bd8-acf2-8c6bdd9d1546
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: chasat
ms.openlocfilehash: 93835eabcf9622735aada0f5dfa46028553c25bd
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="monitor-health-and-alerts-in-azure-stack"></a><span data-ttu-id="b0c2d-103">在 Azure Stack 中監視健康情況和警示</span><span class="sxs-lookup"><span data-stu-id="b0c2d-103">Monitor health and alerts in Azure Stack</span></span>

<span data-ttu-id="b0c2d-104">Azure Stack 包含可監視基礎結構的功能，可讓雲端操作員檢視 Azure Stack 區域的健康情況和警示。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-104">Azure Stack includes infrastructure monitoring capabilities that enable a cloud operator to view health and alerts for an Azure Stack region.</span></span>

<span data-ttu-id="b0c2d-105">Azure Stack 具有一組可用於 [區域管理] 磚的區域管理功能。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-105">Azure Stack has a set of region management capabilities available in the **Region management** tile.</span></span> <span data-ttu-id="b0c2d-106">此磚依預設會釘選在預設提供者訂用帳戶的系統管理員入口網站上，可列出 Azure Stack 的所有已部署區域。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-106">This tile, pinned by default in the administrator portal for the Default Provider Subscription, lists all the deployed regions of Azure Stack.</span></span> <span data-ttu-id="b0c2d-107">它也會顯示每個區域的作用中重要和警告警示計數。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-107">It also shows the count of active critical and warning alerts for each region.</span></span> <span data-ttu-id="b0c2d-108">此磚是您進入 Azure Stack 健康情況和警示功能的進入點。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-108">This tile is your entry point into the health and alert functionality of Azure Stack.</span></span>

 ![區域管理磚](media/azure-stack-monitor-health/image1.png)

 ## <a name="understand-health-in-azure-stack"></a><span data-ttu-id="b0c2d-110">了解 Azure Stack 中的健康情況</span><span class="sxs-lookup"><span data-stu-id="b0c2d-110">Understand health in Azure Stack</span></span>

 <span data-ttu-id="b0c2d-111">在 Azure Stack 中健康情況和警示是由健康情況資源提供者來管理。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-111">Health and alerts are managed in Azure Stack by the Health resource provider.</span></span> <span data-ttu-id="b0c2d-112">在 Azure Stack 部署和設定期間，Azure Stack 基礎結構元件會向健康情況資源提供者註冊。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-112">Azure Stack infrastructure components register with the Health resource provider during Azure Stack deployment and configuration.</span></span> <span data-ttu-id="b0c2d-113">這項註冊讓每個元件的健康情況和警示得以顯示。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-113">This registration enables the display of health and alerts for each component.</span></span> <span data-ttu-id="b0c2d-114">在 Azure Stack 中健康情況是個簡單的概念。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-114">Health in Azure Stack is a simple concept.</span></span> <span data-ttu-id="b0c2d-115">如果元件的已註冊執行個體有警示存在，該元件的健康情況狀態會反映出最差的作用中警示嚴重性：警告或重要。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-115">If alerts for a registered instance of a component exist, the health state of that component reflects the worst active alert severity; warning, or critical.</span></span>
 
 ## <a name="view-and-manage-component-health-state"></a><span data-ttu-id="b0c2d-116">檢視和管理元件健康情況狀態</span><span class="sxs-lookup"><span data-stu-id="b0c2d-116">View and manage component health state</span></span>
 
 <span data-ttu-id="b0c2d-117">您可在 Azure Stack 系統管理員入口網站上檢視元件的健康情況狀態，也可以透過 REST API 和 PowerShell 來檢視。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-117">You can view the health state of components in both the Azure Stack administrator portal and through Rest API and PowerShell.</span></span>
 
<span data-ttu-id="b0c2d-118">若要在入口網站中檢視健康情況狀態，請在 [區域管理] 磚中按一下您想要檢視的區域。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-118">To view the health state in the portal, click the region that you want to view in the **Region management** tile.</span></span> <span data-ttu-id="b0c2d-119">您可以檢視基礎結構角色和資源提供者的健康情況狀態。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-119">You can view the health state of infrastructure roles and of resource providers.</span></span> <span data-ttu-id="b0c2d-120">請注意，在此版本中，「計算」資源提供者不會報告健康情況狀態。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-120">Note that in this release, the Compute resource provider does not report health state.</span></span>

![基礎結構角色的清單](media/azure-stack-monitor-health/image2.png)

<span data-ttu-id="b0c2d-122">您可以按一下資源提供者或基礎結構角色，以檢視更詳細的資訊。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-122">You can click a resource provider or infrastructure role to view more detailed information.</span></span>

> [!WARNING]
><span data-ttu-id="b0c2d-123">如果您按一下基礎結構角色，然後按一下角色執行個體，在 [角色執行個體] 刀鋒視窗中會有選項可 [啟動]、[重新啟動] 或 [關機]。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-123">If you click an infrastructure role, and then click the role instance, there are options in the **Role instance** blade to Start, Restart, or Shutdown.</span></span> <span data-ttu-id="b0c2d-124">**請勿**在 Azure Stack 開發套件環境中使用這些選項。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-124">Do **not** use these options in an Azure Stack Development Kit environment.</span></span> <span data-ttu-id="b0c2d-125">這些選項僅專為每個基礎結構角色具有多個角色執行個體的多節點環境而設計。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-125">These options are designed only for a multi-node environment, where there is more than one role instance per infrastructure role.</span></span> <span data-ttu-id="b0c2d-126">重新啟動開發套件中的角色執行個體 (特別是 AzS-Xrp01) 會導致系統不穩定。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-126">Restarting a role instance (especially AzS-Xrp01) in the development kit causes system instability.</span></span> <span data-ttu-id="b0c2d-127">如需疑難排解協助，請將您的問題張貼到 [Azure Stack 論壇](https://aka.ms/azurestackforum)。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-127">For troubleshooting assistance, please post your issue to the [Azure Stack forum](https://aka.ms/azurestackforum).</span></span>
>
 
## <a name="view-alerts"></a><span data-ttu-id="b0c2d-128">檢視警示</span><span class="sxs-lookup"><span data-stu-id="b0c2d-128">View alerts</span></span>

<span data-ttu-id="b0c2d-129">可直接從 [區域管理] 刀鋒視窗檢視每個 Azure Stack 區域的作用中警示清單。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-129">The list of active alerts for each Azure Stack region is available directly from the **Region management** blade.</span></span> <span data-ttu-id="b0c2d-130">預設設定下的第一個磚是 [警示] 磚，其中會顯示該區域的重要和警告警示摘要。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-130">The first tile in the default configuration is the **Alerts** tile, which displays a summary of the critical and warning alerts for the region.</span></span> <span data-ttu-id="b0c2d-131">就像這個刀鋒視窗中的其他磚一樣，您可以將 [警示] 磚釘選到儀表板上以便快速存取。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-131">You can pin the Alerts tile, like any other tile on this blade, to the dashboard for quick access.</span></span>   

![會顯示警告的 [警示] 磚](media/azure-stack-monitor-health/image3.png)

<span data-ttu-id="b0c2d-133">您可選取 [警示] 磚的上半部，瀏覽至區域的所有作用中警示清單。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-133">By selecting the top portion of the **Alerts** tile, you navigate to the list of all active alerts for the region.</span></span> <span data-ttu-id="b0c2d-134">如果您選取磚內的 [重要] 或 [警告] 明細項目，就會瀏覽至警示的篩選清單 (重要或警告)。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-134">If you select either the **Critical** or **Warning** line item within the tile, you navigate to a filtered list of alerts (Critical or Warning).</span></span> 

![篩選的警告警示](media/azure-stack-monitor-health/image4.png)
  
<span data-ttu-id="b0c2d-136">[警示] 刀鋒視窗支援依狀態 (作用中或已關閉) 和嚴重性 (重要或警告) 進行篩選。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-136">The **Alerts** blade supports the ability to filter both on status (Active or Closed) and severity (Critical or Warning).</span></span> <span data-ttu-id="b0c2d-137">預設檢視會顯示所有作用中警示。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-137">The default view displays all Active alerts.</span></span> <span data-ttu-id="b0c2d-138">所有已關閉的警示會在七天後從系統中移除。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-138">All closed alerts are removed from the system after seven days.</span></span>

![依重要或警告狀態進行篩選的篩選器](media/azure-stack-monitor-health/image5.png)

<span data-ttu-id="b0c2d-140">[警示] 刀鋒視窗也會公開 [檢視 API] 動作，可顯示用來產生清單檢視的 REST API。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-140">The Alerts blade also exposes the **View API** action, which displays the Rest API that was used to generate the list view.</span></span> <span data-ttu-id="b0c2d-141">這個動作可讓您快速熟悉 REST API 語法，可用以查詢警示。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-141">This action provides a quick way to become familiar with the Rest API syntax that you can use to query alerts.</span></span> <span data-ttu-id="b0c2d-142">您可用自動化方式使用此 API，或與您現有的資料中心監視、報告及票證解決方案整合。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-142">You can use this API in automation or for integration with your existing datacenter monitoring, reporting, and ticketing solutions.</span></span> 

![會顯示 REST API 的 [檢視 API] 選項](media/azure-stack-monitor-health/image6.png)

<span data-ttu-id="b0c2d-144">您可以從 [警示] 刀鋒視窗中，選取警示以瀏覽至 [警示詳細資料] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-144">From the Alerts blade, you can select an alert to navigate to the **Alert details** blade.</span></span> <span data-ttu-id="b0c2d-145">此刀鋒視窗會顯示與警示相關聯的所有欄位，並可快速瀏覽至受影響的元件和警示的來源。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-145">This blade displays all fields that are associated with the alert, and enables quick navigation to the affected component and source of the alert.</span></span> <span data-ttu-id="b0c2d-146">例如，如果其中一個基礎結構角色執行個體離線或無法存取，就會發生以下警示。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-146">For example, the following alert occurs if one of the infrastructure role instances goes offline or is not accessible.</span></span>  

![[警示詳細資料] 刀鋒視窗](media/azure-stack-monitor-health/image7.png)

<span data-ttu-id="b0c2d-148">基礎結構角色執行個體回到線上之後，會自動關閉此警示。</span><span class="sxs-lookup"><span data-stu-id="b0c2d-148">After the infrastructure role instance is back online, this alert automatically closes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b0c2d-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b0c2d-149">Next steps</span></span>

[<span data-ttu-id="b0c2d-150">在 Azure Stack 中管理更新</span><span class="sxs-lookup"><span data-stu-id="b0c2d-150">Manage updates in Azure Stack</span></span>](azure-stack-updates.md)

[<span data-ttu-id="b0c2d-151">Azure Stack 中的區域管理</span><span class="sxs-lookup"><span data-stu-id="b0c2d-151">Region management in Azure Stack</span></span>](azure-stack-region-management.md)
