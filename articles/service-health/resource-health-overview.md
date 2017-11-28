---
title: "aaaAzure 資源健全狀況概觀 |Microsoft 文件"
description: "Azure 資源健康狀態的概觀"
services: Resource health
documentationcenter: 
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/01/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: f06153864090487829f717dc3e8972c78a4a58af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-overview"></a><span data-ttu-id="81c11-103">Azure 資源健康狀態概觀</span><span class="sxs-lookup"><span data-stu-id="81c11-103">Azure resource health overview</span></span>
 
<span data-ttu-id="81c11-104">當 Azure 問題影響到您的資源健康狀態時，協助進行診斷並取得支援。</span><span class="sxs-lookup"><span data-stu-id="81c11-104">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="81c11-105">它會通知您有關 hello 目前和過去健康情況的資源，並協助您解決問題。</span><span class="sxs-lookup"><span data-stu-id="81c11-105">It informs you about hello current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="81c11-106">資源健康狀態會在您需要解決 Azure 服務問題時提供技術支援。</span><span class="sxs-lookup"><span data-stu-id="81c11-106">Resource health provides technical support when you need help with Azure service issues.</span></span>

<span data-ttu-id="81c11-107">而[Azure 狀態](https://status.azure.com)通知服務問題會影響一組廣泛的 Azure 客戶、 資源健全狀況可提供您個人化的資源的 hello 健全狀況儀表板。</span><span class="sxs-lookup"><span data-stu-id="81c11-107">Whereas [Azure Status](https://status.azure.com) informs you about service issues that affect a broad set of Azure customers, resource health provides you with a personalized dashboard of hello health of your resources.</span></span> <span data-ttu-id="81c11-108">資源健全狀況會顯示您的資源已在 hello 中無法使用的所有 hello 時間逾期未付 tooAzure 服務問題。</span><span class="sxs-lookup"><span data-stu-id="81c11-108">Resource health shows you all hello times your resources were unavailable in hello past due tooAzure service issues.</span></span> <span data-ttu-id="81c11-109">這使得您 toounderstand 簡單如果已違反 SLA。</span><span class="sxs-lookup"><span data-stu-id="81c11-109">This makes it simple for you toounderstand if an SLA was violated.</span></span> 

## <a name="what-is-considered-a-resource-and-how-does-resource-health-decides-if-a-resource-is-healthy-or-not"></a><span data-ttu-id="81c11-110">何謂資源，以及資源健康狀態如何決定資源健康與否？</span><span class="sxs-lookup"><span data-stu-id="81c11-110">What is considered a resource and how does resource health decides if a resource is healthy or not?</span></span>
<span data-ttu-id="81c11-111">資源是 Azure 服務透過 Azure Resource Manager 所提供之資源類型的執行個體，例如︰虛擬機器、Web 應用程式或 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="81c11-111">A resource is an instance of a resource type offered by an Azure service through Azure Resource Manager, for example: a virtual machine, a web app, or a SQL database.</span></span>

<span data-ttu-id="81c11-112">資源健全狀況依賴於資源是否狀況良好，hello 不同的 Azure 服務 tooassess 所發出的訊號。</span><span class="sxs-lookup"><span data-stu-id="81c11-112">Resource health relies on signals emitted by hello different Azure services tooassess if a resource is healthy or not.</span></span> <span data-ttu-id="81c11-113">如果資源會處於狀況不良，資源健全狀況會分析 hello 問題的其他資訊 toodetermine hello 來源。</span><span class="sxs-lookup"><span data-stu-id="81c11-113">If a resource is unhealthy, resource health analyzes additional information toodetermine hello source of hello problem.</span></span> <span data-ttu-id="81c11-114">它也可以識別 Microsoft 正在 toofix hello 問題，或是您可以採取 tooaddress hello 造成 hello 問題的動作。</span><span class="sxs-lookup"><span data-stu-id="81c11-114">It also identifies actions Microsoft is taking toofix hello issue or what actions you can take tooaddress hello cause of hello problem.</span></span> 

<span data-ttu-id="81c11-115">檢閱 hello 完整資源類型和健全狀況檢查清單[Azure 資源健全狀況](resource-health-checks-resource-types.md)的健全狀況評估的方式的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="81c11-115">Review hello full list of resource types and health checks in [Azure resource health](resource-health-checks-resource-types.md) for additional details on how health is assessed.</span></span>

## <a name="health-status-provided-by-resource-health"></a><span data-ttu-id="81c11-116">資源健康狀態所提供的健全狀態</span><span class="sxs-lookup"><span data-stu-id="81c11-116">Health status provided by resource health</span></span>
<span data-ttu-id="81c11-117">資源的 hello 健全狀況是 hello 下列狀態其中之一：</span><span class="sxs-lookup"><span data-stu-id="81c11-117">hello health of a resource is one of hello following statuses:</span></span>

### <a name="available"></a><span data-ttu-id="81c11-118">可用</span><span class="sxs-lookup"><span data-stu-id="81c11-118">Available</span></span>
<span data-ttu-id="81c11-119">hello 服務偵測不到任何事件影響 hello hello 資源健全狀況。</span><span class="sxs-lookup"><span data-stu-id="81c11-119">hello service has not detected any events impacting hello health of hello resource.</span></span> <span data-ttu-id="81c11-120">萬一其中 hello 資源剛從非計劃性停機期間 hello 最後 24 小時，您會看到 hello**最近復原**通知。</span><span class="sxs-lookup"><span data-stu-id="81c11-120">In cases where hello resource has recovered from unplanned downtime during hello last 24 hours you will see hello **recently recovered** notification.</span></span>

![資源健康狀態可用的虛擬機器](./media/resource-health-overview/Available.png)

### <a name="unavailable"></a><span data-ttu-id="81c11-122">無法使用</span><span class="sxs-lookup"><span data-stu-id="81c11-122">Unavailable</span></span>
<span data-ttu-id="81c11-123">hello 服務偵測到的進行中的平台或影響 hello 健全狀況的 hello 資源的非平台事件。</span><span class="sxs-lookup"><span data-stu-id="81c11-123">hello service has detected an ongoing platform or non-platform event impacting hello health of hello resource.</span></span>

#### <a name="platform-events"></a><span data-ttu-id="81c11-124">平台事件</span><span class="sxs-lookup"><span data-stu-id="81c11-124">Platform events</span></span>
<span data-ttu-id="81c11-125">這些事件所觸發的多個元件的 hello Azure 基礎結構，而且包含排程的動作，如 預定的維護和未計劃的主機重新開機類似的非預期的事件都。</span><span class="sxs-lookup"><span data-stu-id="81c11-125">These events are triggered by multiple components of hello Azure infrastructure and include both scheduled actions like planned maintenance and unexpected incidents like an unplanned host reboot.</span></span>

<span data-ttu-id="81c11-126">資源健全狀況 hello 事件，hello 復原程序提供其他詳細資料，並讓您有 toocontact 支援即使沒有使用中的 Microsoft 支援合約。</span><span class="sxs-lookup"><span data-stu-id="81c11-126">Resource health provides additional details on hello event, hello recovery process and enables you toocontact support even if you don't have an active Microsoft support agreement.</span></span>

![資源健全狀況無法使用虛擬機器因為 tooplatform 事件](./media/resource-health-overview/Unavailable.png)

#### <a name="non-platform-events"></a><span data-ttu-id="81c11-128">非平台事件</span><span class="sxs-lookup"><span data-stu-id="81c11-128">Non-Platform events</span></span>
<span data-ttu-id="81c11-129">由使用者，例如停止虛擬機器，或是達到 hello 連線 tooa Redis 快取的數目上限，所採取的動作會觸發這些事件。</span><span class="sxs-lookup"><span data-stu-id="81c11-129">These events are triggered by actions taken by users, for example stopping a virtual machine or reaching hello maximum number of connections tooa Redis Cache.</span></span>

![資源健全狀況無法使用虛擬機器因為 toonon 平台事件](./media/resource-health-overview/Unavailable_NonPlatform.png)

### <a name="unknown"></a><span data-ttu-id="81c11-131">不明</span><span class="sxs-lookup"><span data-stu-id="81c11-131">Unknown</span></span>
<span data-ttu-id="81c11-132">此健全狀態表示資源健康狀態超過 10 分鐘未收到此資源的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="81c11-132">This health status indicates that resource health has not received information about this resource for more than 10 minutes.</span></span> <span data-ttu-id="81c11-133">雖然這個狀態不是 hello hello 資源狀態的明確指示，它會是 hello 疑難排解程序中的重要資料點：</span><span class="sxs-lookup"><span data-stu-id="81c11-133">While this status is not a definitive indication of hello state of hello resource, it is an important data point in hello troubleshooting process:</span></span>
* <span data-ttu-id="81c11-134">如果 hello 資源是否如預期的 hello 的 hello 資源將會更新狀態 tooAvailable 幾分鐘後執行。</span><span class="sxs-lookup"><span data-stu-id="81c11-134">If hello resource is running as expected hello status of hello resource will update tooAvailable after a few minutes.</span></span>
* <span data-ttu-id="81c11-135">如果您遇到的問題與 hello 資源，hello 不明健康情況狀態可能會建議 hello 資源受到 hello 平台事件。</span><span class="sxs-lookup"><span data-stu-id="81c11-135">If you are experiencing problems with hello resource, hello Unknown health status may suggest hello resource is impacted by an event in hello platform.</span></span>

![資源健康狀態未知的虛擬機器](./media/resource-health-overview/Unknown.png)

## <a name="report-an-incorrect-status"></a><span data-ttu-id="81c11-137">報告不正確的狀態</span><span class="sxs-lookup"><span data-stu-id="81c11-137">Report an incorrect status</span></span>
<span data-ttu-id="81c11-138">如果在任何時間點您認為 hello 目前的健全狀況狀態不正確，您可以讓我們知道，依序按一下**報告不正確的健全狀況狀態**。</span><span class="sxs-lookup"><span data-stu-id="81c11-138">If at any point you believe hello current health status is incorrect, you can let us know by clicking **Report incorrect health status**.</span></span> <span data-ttu-id="81c11-139">在您受到影響的 Azure 問題的情況下，我們建議您 toocontact 支援 hello 資源健全狀況刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="81c11-139">In cases where you are impacted by an Azure problem, we encourage you toocontact support from hello resource health blade.</span></span> 

![資源健康狀態報告不正確的狀態](./media/resource-health-overview/incorrect-status.png)

## <a name="historical-information"></a><span data-ttu-id="81c11-141">歷程記錄資訊</span><span class="sxs-lookup"><span data-stu-id="81c11-141">Historical Information</span></span>
<span data-ttu-id="81c11-142">您可以存取向上 too14 天的健全狀況歷程記錄資料，依序按一下**檢視記錄**hello 資源健全狀況刀鋒視窗中。</span><span class="sxs-lookup"><span data-stu-id="81c11-142">You can access up too14 days of historical health data by clicking **View History** in hello Resource health blade.</span></span> 

![資源健康狀態報表歷程記錄](./media/resource-health-overview/history-blade.png)

## <a name="getting-started"></a><span data-ttu-id="81c11-144">開始使用</span><span class="sxs-lookup"><span data-stu-id="81c11-144">Getting started</span></span>
<span data-ttu-id="81c11-145">tooopen 一個資源的資源健全狀況</span><span class="sxs-lookup"><span data-stu-id="81c11-145">tooopen Resource health for one resource</span></span>
1.  <span data-ttu-id="81c11-146">登入到 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="81c11-146">Sign in into hello Azure portal.</span></span>
2.  <span data-ttu-id="81c11-147">瀏覽 tooyour 資源。</span><span class="sxs-lookup"><span data-stu-id="81c11-147">Navigate tooyour resource.</span></span>
3.  <span data-ttu-id="81c11-148">在位於 hello 左手邊 hello 資源功能表上，按一下**資源健全狀況**。</span><span class="sxs-lookup"><span data-stu-id="81c11-148">In hello resource menu located in hello left-hand side, click **Resource health**.</span></span>

![從 [資源] 刀鋒視窗將資源健康狀態開啟](./media/resource-health-overview/from-resource-blade.png)

<span data-ttu-id="81c11-150">您也可以存取資源健全狀況，依序按一下**更多服務**，並輸入**資源健全狀況**中篩選文字方塊 tooopen hello**說明 + 支援**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="81c11-150">You can also access resource health by clicking **More services**, and typing **resource health** in filter text box tooopen hello **Help + Support** blade.</span></span> <span data-ttu-id="81c11-151">最後按一下 [**資源健康狀態**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth) 。</span><span class="sxs-lookup"><span data-stu-id="81c11-151">Finally click [**Resource health**](https://ms.portal.azure.com/#blade/Microsoft_Azure_Monitoring/AzureMonitoringBrowseBlade/resourceHealth).</span></span>

![從 [更多服務] 將資源健康狀態開啟](./media/resource-health-overview/FromOtherServices.png)

## <a name="next-steps"></a><span data-ttu-id="81c11-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="81c11-153">Next steps</span></span>

<span data-ttu-id="81c11-154">請參閱這些資源 toolearn，深入了解資源健全狀況：</span><span class="sxs-lookup"><span data-stu-id="81c11-154">Check out these resources toolearn more about resource health:</span></span>
-  [<span data-ttu-id="81c11-155">Azure 資源健康狀態中的資源類型和健康情況檢查</span><span class="sxs-lookup"><span data-stu-id="81c11-155">Resource types and health checks in Azure resource health</span></span>](resource-health-checks-resource-types.md)
-  [<span data-ttu-id="81c11-156">關於 Azure 資源健康狀態的常見問題集</span><span class="sxs-lookup"><span data-stu-id="81c11-156">Frequently asked questions about Azure resource health</span></span>](resource-health-faq.md)




