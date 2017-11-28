---
title: "aaaMonitor 健全狀況和 Azure 堆疊中的警示 |Microsoft 文件"
description: "深入了解如何 toomonitor 健全狀況和 Azure 堆疊中的警示。"
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
ms.openlocfilehash: 11e287c497e154b767c775fe4afcc78ec9e72fb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-health-and-alerts-in-azure-stack"></a><span data-ttu-id="9d31b-103">在 Azure Stack 中監視健康情況和警示</span><span class="sxs-lookup"><span data-stu-id="9d31b-103">Monitor health and alerts in Azure Stack</span></span>

<span data-ttu-id="9d31b-104">Azure 堆疊包含基礎結構監視功能，可讓雲端操作員 tooview 健全狀況和堆疊 Azure 區域的警示。</span><span class="sxs-lookup"><span data-stu-id="9d31b-104">Azure Stack includes infrastructure monitoring capabilities that enable a cloud operator tooview health and alerts for an Azure Stack region.</span></span>

<span data-ttu-id="9d31b-105">Azure 堆疊都有可用的 hello 的區域管理功能的一組**區域管理**磚。</span><span class="sxs-lookup"><span data-stu-id="9d31b-105">Azure Stack has a set of region management capabilities available in hello **Region management** tile.</span></span> <span data-ttu-id="9d31b-106">這個 hello hello 預設提供者訂用帳戶的系統管理員入口網站中的預設釘選的磚會列出 Azure 堆疊的所有部署的 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="9d31b-106">This tile, pinned by default in hello administrator portal for hello Default Provider Subscription, lists all hello deployed regions of Azure Stack.</span></span> <span data-ttu-id="9d31b-107">它也會顯示 hello 計數的每個區域的作用中的重大和警告警示。</span><span class="sxs-lookup"><span data-stu-id="9d31b-107">It also shows hello count of active critical and warning alerts for each region.</span></span> <span data-ttu-id="9d31b-108">此磚會進入 hello 健全狀況和 Azure 堆疊的警示功能。</span><span class="sxs-lookup"><span data-stu-id="9d31b-108">This tile is your entry point into hello health and alert functionality of Azure Stack.</span></span>

 ![hello 區域管理圖格](media/azure-stack-monitor-health/image1.png)

 ## <a name="understand-health-in-azure-stack"></a><span data-ttu-id="9d31b-110">了解 Azure Stack 中的健康情況</span><span class="sxs-lookup"><span data-stu-id="9d31b-110">Understand health in Azure Stack</span></span>

 <span data-ttu-id="9d31b-111">健全狀況和警示是由 hello 健全狀況資源提供者管理 Azure 堆疊中。</span><span class="sxs-lookup"><span data-stu-id="9d31b-111">Health and alerts are managed in Azure Stack by hello Health resource provider.</span></span> <span data-ttu-id="9d31b-112">Azure 堆疊部署和設定期間，與 hello 健全狀況資源提供者註冊 azure 的堆疊基礎結構元件。</span><span class="sxs-lookup"><span data-stu-id="9d31b-112">Azure Stack infrastructure components register with hello Health resource provider during Azure Stack deployment and configuration.</span></span> <span data-ttu-id="9d31b-113">這個登錄可讓 hello 顯示健全狀況和每個元件的警示。</span><span class="sxs-lookup"><span data-stu-id="9d31b-113">This registration enables hello display of health and alerts for each component.</span></span> <span data-ttu-id="9d31b-114">在 Azure Stack 中健康情況是個簡單的概念。</span><span class="sxs-lookup"><span data-stu-id="9d31b-114">Health in Azure Stack is a simple concept.</span></span> <span data-ttu-id="9d31b-115">如果已註冊的元件存在，執行個體警示 hello 該元件的健全狀況狀態會反映出 hello 最差作用中警示嚴重性;警告或重大。</span><span class="sxs-lookup"><span data-stu-id="9d31b-115">If alerts for a registered instance of a component exist, hello health state of that component reflects hello worst active alert severity; warning, or critical.</span></span>
 
 ## <a name="view-and-manage-component-health-state"></a><span data-ttu-id="9d31b-116">檢視和管理元件健康情況狀態</span><span class="sxs-lookup"><span data-stu-id="9d31b-116">View and manage component health state</span></span>
 
 <span data-ttu-id="9d31b-117">在這兩個 hello Azure 堆疊管理員入口網站，並透過 Rest API 和 PowerShell，您可以檢視 hello 元件健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="9d31b-117">You can view hello health state of components in both hello Azure Stack administrator portal and through Rest API and PowerShell.</span></span>
 
<span data-ttu-id="9d31b-118">tooview hello 健全狀況狀態在 hello 入口網站中，按一下您想在 hello tooview hello 區域**區域管理**磚。</span><span class="sxs-lookup"><span data-stu-id="9d31b-118">tooview hello health state in hello portal, click hello region that you want tooview in hello **Region management** tile.</span></span> <span data-ttu-id="9d31b-119">您可以檢視基礎結構角色和資源提供者的 hello 健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="9d31b-119">You can view hello health state of infrastructure roles and of resource providers.</span></span> <span data-ttu-id="9d31b-120">請注意，在此版本中，hello 計算資源提供者不會報告健全狀況狀態。</span><span class="sxs-lookup"><span data-stu-id="9d31b-120">Note that in this release, hello Compute resource provider does not report health state.</span></span>

![基礎結構角色的清單](media/azure-stack-monitor-health/image2.png)

<span data-ttu-id="9d31b-122">您可以按一下 tooview 資源提供者或基礎結構角色的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="9d31b-122">You can click a resource provider or infrastructure role tooview more detailed information.</span></span>

> [!WARNING]
><span data-ttu-id="9d31b-123">如果您按一下 [基礎結構角色]，然後按一下hello 角色執行個體時，有在 hello 選項**角色執行個體**刀鋒視窗 tooStart、 重新啟動或關閉。</span><span class="sxs-lookup"><span data-stu-id="9d31b-123">If you click an infrastructure role, and then click hello role instance, there are options in hello **Role instance** blade tooStart, Restart, or Shutdown.</span></span> <span data-ttu-id="9d31b-124">**請勿**在 Azure Stack 開發套件環境中使用這些選項。</span><span class="sxs-lookup"><span data-stu-id="9d31b-124">Do **not** use these options in an Azure Stack Development Kit environment.</span></span> <span data-ttu-id="9d31b-125">這些選項僅專為每個基礎結構角色具有多個角色執行個體的多節點環境而設計。</span><span class="sxs-lookup"><span data-stu-id="9d31b-125">These options are designed only for a multi-node environment, where there is more than one role instance per infrastructure role.</span></span> <span data-ttu-id="9d31b-126">Hello 開發套件中重新啟動角色執行個體 (特別是 Xrp01 AzS) 會導致系統不穩定。</span><span class="sxs-lookup"><span data-stu-id="9d31b-126">Restarting a role instance (especially AzS-Xrp01) in hello development kit causes system instability.</span></span> <span data-ttu-id="9d31b-127">如需疑難排解的協助，請張貼問題 toohello [Azure 堆疊論壇](https://aka.ms/azurestackforum)。</span><span class="sxs-lookup"><span data-stu-id="9d31b-127">For troubleshooting assistance, please post your issue toohello [Azure Stack forum](https://aka.ms/azurestackforum).</span></span>
>
 
## <a name="view-alerts"></a><span data-ttu-id="9d31b-128">檢視警示</span><span class="sxs-lookup"><span data-stu-id="9d31b-128">View alerts</span></span>

<span data-ttu-id="9d31b-129">針對每個 Azure 堆疊區域的作用中警示的 hello 清單是可以直接從 hello**區域管理**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9d31b-129">hello list of active alerts for each Azure Stack region is available directly from hello **Region management** blade.</span></span> <span data-ttu-id="9d31b-130">hello hello 預設組態中的第一個磚為 hello**警示**磚，其中顯示 hello 重大和警告警示 hello 區域的摘要。</span><span class="sxs-lookup"><span data-stu-id="9d31b-130">hello first tile in hello default configuration is hello **Alerts** tile, which displays a summary of hello critical and warning alerts for hello region.</span></span> <span data-ttu-id="9d31b-131">您可以釘選 hello 警示圖格，此刀鋒視窗中，讓您快速存取 toohello 儀表板上的任何其他磚。</span><span class="sxs-lookup"><span data-stu-id="9d31b-131">You can pin hello Alerts tile, like any other tile on this blade, toohello dashboard for quick access.</span></span>   

![會顯示警告的 [警示] 磚](media/azure-stack-monitor-health/image3.png)

<span data-ttu-id="9d31b-133">選取頂部 hello hello**警示**磚，您瀏覽 toohello hello 區域的所有作用中警示清單。</span><span class="sxs-lookup"><span data-stu-id="9d31b-133">By selecting hello top portion of hello **Alerts** tile, you navigate toohello list of all active alerts for hello region.</span></span> <span data-ttu-id="9d31b-134">如果您選取其中一個 hello**重大**或**警告**hello 磚中的明細項目，您瀏覽 tooa 篩選警示 （重大或警告） 的清單。</span><span class="sxs-lookup"><span data-stu-id="9d31b-134">If you select either hello **Critical** or **Warning** line item within hello tile, you navigate tooa filtered list of alerts (Critical or Warning).</span></span> 

![篩選的警告警示](media/azure-stack-monitor-health/image4.png)
  
<span data-ttu-id="9d31b-136">hello**警示**刀鋒視窗支援 hello 能力 toofilter （作用中或已關閉） 的狀態和嚴重性 （重大或警告）。</span><span class="sxs-lookup"><span data-stu-id="9d31b-136">hello **Alerts** blade supports hello ability toofilter both on status (Active or Closed) and severity (Critical or Warning).</span></span> <span data-ttu-id="9d31b-137">hello 預設檢視會顯示所有作用中警示。</span><span class="sxs-lookup"><span data-stu-id="9d31b-137">hello default view displays all Active alerts.</span></span> <span data-ttu-id="9d31b-138">所有已關閉的警示會在 7 天後從 hello 系統移除。</span><span class="sxs-lookup"><span data-stu-id="9d31b-138">All closed alerts are removed from hello system after seven days.</span></span>

![篩選窗格 toofilter 重大或警告狀態](media/azure-stack-monitor-health/image5.png)

<span data-ttu-id="9d31b-140">hello 警示刀鋒伺服器也會公開 hello**檢視 API**哪些顯示 hello Rest API 所使用的 toogenerate hello 清單檢視的動作。</span><span class="sxs-lookup"><span data-stu-id="9d31b-140">hello Alerts blade also exposes hello **View API** action, which displays hello Rest API that was used toogenerate hello list view.</span></span> <span data-ttu-id="9d31b-141">這個動作可提供快速 toobecome 熟悉 hello Rest API 語法，您可以使用 tooquery 警示。</span><span class="sxs-lookup"><span data-stu-id="9d31b-141">This action provides a quick way toobecome familiar with hello Rest API syntax that you can use tooquery alerts.</span></span> <span data-ttu-id="9d31b-142">您可用自動化方式使用此 API，或與您現有的資料中心監視、報告及票證解決方案整合。</span><span class="sxs-lookup"><span data-stu-id="9d31b-142">You can use this API in automation or for integration with your existing datacenter monitoring, reporting, and ticketing solutions.</span></span> 

![hello 顯示 hello Rest API 的 API 檢視選項](media/azure-stack-monitor-health/image6.png)

<span data-ttu-id="9d31b-144">您可以從 hello 警示刀鋒視窗中，選取警示 toonavigate toohello**警示詳細資料**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="9d31b-144">From hello Alerts blade, you can select an alert toonavigate toohello **Alert details** blade.</span></span> <span data-ttu-id="9d31b-145">此刀鋒視窗會顯示 hello 警示相關聯的所有欄位，並可讓快速瀏覽 toohello 受影響的元件和 hello 警示的來源。</span><span class="sxs-lookup"><span data-stu-id="9d31b-145">This blade displays all fields that are associated with hello alert, and enables quick navigation toohello affected component and source of hello alert.</span></span> <span data-ttu-id="9d31b-146">例如，hello 下列警示就會發生如果其中一個 hello 基礎結構角色執行個體離線或無法存取。</span><span class="sxs-lookup"><span data-stu-id="9d31b-146">For example, hello following alert occurs if one of hello infrastructure role instances goes offline or is not accessible.</span></span>  

![hello 警示詳細資料 刀鋒視窗](media/azure-stack-monitor-health/image7.png)

<span data-ttu-id="9d31b-148">Hello 基礎結構角色執行個體回到線上之後，會自動關閉此警示。</span><span class="sxs-lookup"><span data-stu-id="9d31b-148">After hello infrastructure role instance is back online, this alert automatically closes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d31b-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9d31b-149">Next steps</span></span>

[<span data-ttu-id="9d31b-150">在 Azure Stack 中管理更新</span><span class="sxs-lookup"><span data-stu-id="9d31b-150">Manage updates in Azure Stack</span></span>](azure-stack-updates.md)

[<span data-ttu-id="9d31b-151">Azure Stack 中的區域管理</span><span class="sxs-lookup"><span data-stu-id="9d31b-151">Region management in Azure Stack</span></span>](azure-stack-region-management.md)
