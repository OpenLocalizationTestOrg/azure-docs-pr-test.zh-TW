---
title: "Azure 資源健康狀態概觀 | Microsoft Docs"
description: "Azure 資源健康狀態的概觀"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: resource-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 06/01/2016
ms.author: BernardoAMunoz
ms.openlocfilehash: d54979995ca97a70ba92c64915b919da09f548ec
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-resource-health-overview"></a><span data-ttu-id="d39cf-103">Azure 資源健康狀態概觀</span><span class="sxs-lookup"><span data-stu-id="d39cf-103">Azure resource health overview</span></span>
 
<span data-ttu-id="d39cf-104">當 Azure 問題影響到您的資源健康狀態時，協助進行診斷並取得支援。</span><span class="sxs-lookup"><span data-stu-id="d39cf-104">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="d39cf-105">它會通知您資源的目前及過去的健康狀態，並協助您解決問題。</span><span class="sxs-lookup"><span data-stu-id="d39cf-105">It informs you about the current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="d39cf-106">資源健康狀態會在您需要解決 Azure 服務問題時提供技術支援。</span><span class="sxs-lookup"><span data-stu-id="d39cf-106">Resource health provides technical support when you need help with Azure service issues.</span></span>

<span data-ttu-id="d39cf-107">[Azure 狀態](https://status.azure.com)會通知您影響大規模客戶的服務問題，而資源健康狀態會提供資源健康情況的個人化儀表板。</span><span class="sxs-lookup"><span data-stu-id="d39cf-107">Whereas [Azure Status](https://status.azure.com) informs you about service issues that affect a broad set of Azure customers, resource health provides you with a personalized dashboard of the health of your resources.</span></span> <span data-ttu-id="d39cf-108">資源健康狀態會顯示您的資源過去因 Azure 服務問題而無法使用的所有時間。</span><span class="sxs-lookup"><span data-stu-id="d39cf-108">Resource health shows you all the times your resources were unavailable in the past due to Azure service issues.</span></span> <span data-ttu-id="d39cf-109">這可讓您更輕鬆了解是否違反 SLA。</span><span class="sxs-lookup"><span data-stu-id="d39cf-109">This makes it simple for you to understand if an SLA was violated.</span></span> 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a><span data-ttu-id="d39cf-110">何謂資源，以及資源健康狀態如何決定資源健康與否？</span><span class="sxs-lookup"><span data-stu-id="d39cf-110">What is considered a resource and how does resource health decides if a resource is healthy or not?</span></span>
<span data-ttu-id="d39cf-111">資源是 Azure 服務透過 Azure Resource Manager 所提供之資源類型的執行個體，例如︰虛擬機器、Web 應用程式或 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="d39cf-111">A resource is an instance of a resource type offered by an Azure service through Azure Resource Manager, for example: a virtual machine, a web app, or a SQL database.</span></span>

<span data-ttu-id="d39cf-112">資源健康狀態依賴不同的 Azure 服務所發出的訊號，來評估資源健康與否。</span><span class="sxs-lookup"><span data-stu-id="d39cf-112">Resource health relies on signals emitted by the different Azure services to assess if a resource is healthy or not.</span></span> <span data-ttu-id="d39cf-113">如果資源健康情況不良，資源健康狀態會分析其他資訊，來判斷問題的來源。</span><span class="sxs-lookup"><span data-stu-id="d39cf-113">If a resource is unhealthy, resource health analyzes additional information to determine the source of the problem.</span></span> <span data-ttu-id="d39cf-114">它也會識別 Microsoft 為修正這個問題所採取的動作，或您可以採取哪些動作來解決問題的原因。</span><span class="sxs-lookup"><span data-stu-id="d39cf-114">It also identifies actions Microsoft is taking to fix the issue or what actions you can take to address the cause of the problem.</span></span> 

<span data-ttu-id="d39cf-115">檢閱 [Azure 資源健康狀態](resource-health-checks-resource-types.md)中的資源類型及健康情況檢查完整清單，以了解健康情況評估方式的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d39cf-115">Review the full list of resource types and health checks in [Azure resource health](resource-health-checks-resource-types.md) for additional details on how health is assessed.</span></span>

## <a name="health-status-provided-by-resource-health"></a><span data-ttu-id="d39cf-116">資源健康狀態所提供的健全狀態</span><span class="sxs-lookup"><span data-stu-id="d39cf-116">Health status provided by resource health</span></span>
<span data-ttu-id="d39cf-117">資源的健康情況為下列其中一個狀態︰</span><span class="sxs-lookup"><span data-stu-id="d39cf-117">The health of a resource is one of the following statuses:</span></span>

### <a name="available"></a><span data-ttu-id="d39cf-118">可用</span><span class="sxs-lookup"><span data-stu-id="d39cf-118">Available</span></span>
<span data-ttu-id="d39cf-119">服務偵測不到影響資源健康情況的任何事件。</span><span class="sxs-lookup"><span data-stu-id="d39cf-119">The service has not detected any events impacting the health of the resource.</span></span> <span data-ttu-id="d39cf-120">如果資源在過去 24 小時內從未規劃的停機時間復原，您會看到**最近復原**通知。</span><span class="sxs-lookup"><span data-stu-id="d39cf-120">In cases where the resource has recovered from unplanned downtime during the last 24 hours you will see the **recently recovered** notification.</span></span>

![資源健康狀態可用的虛擬機器](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a><span data-ttu-id="d39cf-122">無法使用</span><span class="sxs-lookup"><span data-stu-id="d39cf-122">Unavailable</span></span>
<span data-ttu-id="d39cf-123">服務偵測到的進行中平台或非平台事件會影響資源的健康情況。</span><span class="sxs-lookup"><span data-stu-id="d39cf-123">The service has detected an ongoing platform or non-platform event impacting the health of the resource.</span></span>

#### <a name="platform-events"></a><span data-ttu-id="d39cf-124">平台事件</span><span class="sxs-lookup"><span data-stu-id="d39cf-124">Platform events</span></span>
<span data-ttu-id="d39cf-125">這些事件會由 Azure 基礎結構的多個元件觸發，並包含排程的動作 (例如規劃的維護) 和非預期的事件 (例如未規劃的主機重新開機)。</span><span class="sxs-lookup"><span data-stu-id="d39cf-125">These events are triggered by multiple components of the Azure infrastructure and include both scheduled actions like planned maintenance and unexpected incidents like an unplanned host reboot.</span></span>

<span data-ttu-id="d39cf-126">資源健康狀態會提供關於事件、復原程序的其他詳細資料，並讓您即使在沒有有效的 Microsoft 支援合約時，也能連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="d39cf-126">Resource health provides additional details on the event, the recovery process and enables you to contact support even if you don't have an active Microsoft support agreement.</span></span>

![由於平台事件而資源健康狀態無法使用的虛擬機器](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a><span data-ttu-id="d39cf-128">非平台事件</span><span class="sxs-lookup"><span data-stu-id="d39cf-128">Non-Platform events</span></span>
<span data-ttu-id="d39cf-129">這些事件會由使用者所採取的動作觸發，例如停止虛擬機器或觸達 Redis 快取的連線數目上限。</span><span class="sxs-lookup"><span data-stu-id="d39cf-129">These events are triggered by actions taken by users, for example stopping a virtual machine or reaching the maximum number of connections to a Redis Cache.</span></span>

![由於非平台事件而資源健康狀態無法使用的虛擬機器](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a><span data-ttu-id="d39cf-131">不明</span><span class="sxs-lookup"><span data-stu-id="d39cf-131">Unknown</span></span>
<span data-ttu-id="d39cf-132">此健全狀態表示資源健康狀態超過 10 分鐘未收到此資源的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d39cf-132">This health status indicates that resource health has not received information about this resource for more than 10 minutes.</span></span> <span data-ttu-id="d39cf-133">雖然此狀態並非資源狀態的明確指示，卻是疑難排解程序中的重要資料點︰</span><span class="sxs-lookup"><span data-stu-id="d39cf-133">While this status is not a definitive indication of the state of the resource, it is an important data point in the troubleshooting process:</span></span>
* <span data-ttu-id="d39cf-134">如果資源如預期般執行，幾分鐘後資源的狀態會更新為「可用」。</span><span class="sxs-lookup"><span data-stu-id="d39cf-134">If the resource is running as expected the status of the resource will update to Available after a few minutes.</span></span>
* <span data-ttu-id="d39cf-135">如果您遇到資源的問題，不明的健全狀態可能會建議資源是受到平台的事件影響。</span><span class="sxs-lookup"><span data-stu-id="d39cf-135">If you are experiencing problems with the resource, the Unknown health status may suggest the resource is impacted by an event in the platform.</span></span>

![資源健康狀態未知的虛擬機器](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a><span data-ttu-id="d39cf-137">報告不正確的狀態</span><span class="sxs-lookup"><span data-stu-id="d39cf-137">Report an incorrect status</span></span>
<span data-ttu-id="d39cf-138">如果您在任何時間點認為目前的健全狀態不正確，您可以按一下 [報告不正確的健全狀態] 來告知我們。</span><span class="sxs-lookup"><span data-stu-id="d39cf-138">If at any point you believe the current health status is incorrect, you can let us know by clicking **Report incorrect health status**.</span></span> <span data-ttu-id="d39cf-139">在您受到 Azure 問題影響的情況下，建議您從 [資源健康狀態] 刀鋒視窗連絡支援人員。</span><span class="sxs-lookup"><span data-stu-id="d39cf-139">In cases where you are impacted by an Azure problem, we encourage you to contact support from the resource health blade.</span></span> 

![資源健康狀態報告不正確的狀態](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a><span data-ttu-id="d39cf-141">歷程記錄資訊</span><span class="sxs-lookup"><span data-stu-id="d39cf-141">Historical Information</span></span>
<span data-ttu-id="d39cf-142">您可以按一下 [資源健康狀態] 刀鋒視窗中的 [檢視歷程記錄]，來存取多達 14 天的歷程記錄健康情況資料。</span><span class="sxs-lookup"><span data-stu-id="d39cf-142">You can access up to 14 days of historical health data by clicking **View History** in the Resource health blade.</span></span> 

![資源健康狀態報表歷程記錄](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a><span data-ttu-id="d39cf-144">開始使用</span><span class="sxs-lookup"><span data-stu-id="d39cf-144">Getting started</span></span>
<span data-ttu-id="d39cf-145">若要將一個資源的資源健康狀態開啟</span><span class="sxs-lookup"><span data-stu-id="d39cf-145">To open Resource health for one resource</span></span>
1.  <span data-ttu-id="d39cf-146">登入 Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="d39cf-146">Sign in into the Azure portal.</span></span>
2.  <span data-ttu-id="d39cf-147">瀏覽至您的資源。</span><span class="sxs-lookup"><span data-stu-id="d39cf-147">Navigate to your resource.</span></span>
3.  <span data-ttu-id="d39cf-148">在位於左側的 [資源] 功能表，按一下 [資源健康狀態]。</span><span class="sxs-lookup"><span data-stu-id="d39cf-148">In the resource menu located in the left-hand side, click **Resource health**.</span></span>

![從 [資源] 刀鋒視窗將資源健康狀態開啟](./media/resource-health-overview/from-resource-blade.png)

<span data-ttu-id="d39cf-150">您也可以存取資源健康狀態，方法為按一下 [更多服務]，然後在 [篩選] 文字方塊中輸入**資源健康狀態**，將 [說明 + 支援] 刀鋒視窗開啟。</span><span class="sxs-lookup"><span data-stu-id="d39cf-150">You can also access resource health by clicking **More services**, and typing **resource health** in filter text box to open the **Help + Support** blade.</span></span> <span data-ttu-id="d39cf-151">最後按一下 [**資源健康狀態**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth) 。</span><span class="sxs-lookup"><span data-stu-id="d39cf-151">Finally click [**Resource health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span></span>

![從 [更多服務] 將資源健康狀態開啟](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a><span data-ttu-id="d39cf-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d39cf-153">Next steps</span></span>

<span data-ttu-id="d39cf-154">若要深入了解資源健康狀態，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="d39cf-154">Check out these resources to learn more about resource health:</span></span>
-  [<span data-ttu-id="d39cf-155">Azure 資源健康狀態中的資源類型和健康情況檢查</span><span class="sxs-lookup"><span data-stu-id="d39cf-155">Resource types and health checks in Azure resource health</span></span>](resource-health-checks-resource-types.md)
-  [<span data-ttu-id="d39cf-156">關於 Azure 資源健康狀態的常見問題集</span><span class="sxs-lookup"><span data-stu-id="d39cf-156">Frequently asked questions about Azure resource health</span></span>](resource-health-faq.md)




