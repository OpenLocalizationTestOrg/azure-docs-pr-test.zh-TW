---
title: "aaaAzure 資源健全狀況常見問題集 |Microsoft 文件"
description: "Azure 資源健康狀態的概觀"
services: Resource health
documentationcenter: dev-center-name
author: BernardoAMunoz
manager: 
editor: 
ms.assetid: 85cc88a4-80fd-4b9b-a30a-34ff3782855f
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/05/2017
ms.author: BernardoAMunoz
ms.openlocfilehash: fe29b2df1f9fee4b77d0100c7d872df837dc4b4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-health-faq"></a><span data-ttu-id="2a2bd-103">Azure 資源健康狀態常見問題集</span><span class="sxs-lookup"><span data-stu-id="2a2bd-103">Azure Resource Health FAQ</span></span>
<span data-ttu-id="2a2bd-104">了解 hello 解答了 toocommon 有關 Azure 資源健全狀況。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-104">Learn hello answers toocommon questions about Azure Resource Health.</span></span>

## <a name="what-is-azure-resource-health"></a><span data-ttu-id="2a2bd-105">何謂 Azure 資源健康狀態？</span><span class="sxs-lookup"><span data-stu-id="2a2bd-105">What is Azure Resource Health?</span></span>
<span data-ttu-id="2a2bd-106">當 Azure 問題影響到您的資源健康狀態時，協助進行診斷並取得支援。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-106">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="2a2bd-107">它會通知您有關 hello 目前和過去健康情況的資源，並協助您解決問題。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-107">It informs you about hello current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="2a2bd-108">資源健康狀態會在您需要解決 Azure 服務問題時提供技術支援。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-108">Resource health provides technical support when you need help with Azure service issues.</span></span>  

## <a name="what-is-hello-resource-health-intended-for"></a><span data-ttu-id="2a2bd-109">什麼是資源健全狀況適用於 hello？</span><span class="sxs-lookup"><span data-stu-id="2a2bd-109">What is hello Resource Health intended for?</span></span>
<span data-ttu-id="2a2bd-110">一旦偵測到的問題與資源，資源健全狀況可協助您診斷 hello 根本原因。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-110">Once an issue with a resource has been detected, Resource Health can help you diagnose hello root cause.</span></span> <span data-ttu-id="2a2bd-111">它提供說明 toomitigate hello 問題和技術支援人員時需要更多說明 Azure 服務的問題。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-111">It provides help toomitigate hello issue and technical support when you need more help with Azure service issues.</span></span>

## <a name="what-health-checks-are-performed-by-resource-health"></a><span data-ttu-id="2a2bd-112">資源健康狀態會執行哪些健康狀態檢查？</span><span class="sxs-lookup"><span data-stu-id="2a2bd-112">What health checks are performed by Resource Health?</span></span>
<span data-ttu-id="2a2bd-113">資源健全狀況執行各種檢查，根據 hello[資源類型](resource-health-checks-resource-types.md)。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-113">Resource health performs various checks based on hello [resource type](resource-health-checks-resource-types.md).</span></span> <span data-ttu-id="2a2bd-114">這些檢查包括設計的 tooimplement 三種問題：</span><span class="sxs-lookup"><span data-stu-id="2a2bd-114">These checks are designed tooimplement three types of issues:</span></span> 
- <span data-ttu-id="2a2bd-115">未規劃的事件，例如未預期的主機重新開機</span><span class="sxs-lookup"><span data-stu-id="2a2bd-115">Unplanned events, for example an unexpected host reboot</span></span>
- <span data-ttu-id="2a2bd-116">規劃的事件，例如排程的主機作業系統更新</span><span class="sxs-lookup"><span data-stu-id="2a2bd-116">Planned events, like scheduled host OS updates</span></span>
- <span data-ttu-id="2a2bd-117">使用者動作觸發的事件，例如使用者重新啟動虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2a2bd-117">Events triggered by user actions, for example a user rebooting a virtual machine</span></span>

## <a name="what-does-each-of-hello-health-status-mean"></a><span data-ttu-id="2a2bd-118">每個 hello 健全狀況狀態是什麼意思？</span><span class="sxs-lookup"><span data-stu-id="2a2bd-118">What does each of hello health status mean?</span></span>
<span data-ttu-id="2a2bd-119">有三個不同的健全狀態︰</span><span class="sxs-lookup"><span data-stu-id="2a2bd-119">There are three different health statuses:</span></span>
- <span data-ttu-id="2a2bd-120">可用： 沒有任何已知的問題中 hello 可能正影響此資源的 Azure 平台</span><span class="sxs-lookup"><span data-stu-id="2a2bd-120">Available: There aren't any known problems in hello Azure platform that could be impacting this resource</span></span>
- <span data-ttu-id="2a2bd-121">無法使用： 資源健全狀況偵測到會影響 hello 資源的問題</span><span class="sxs-lookup"><span data-stu-id="2a2bd-121">Unavailable: Resource health has detected issues that are impacting hello resource</span></span>
- <span data-ttu-id="2a2bd-122">未知： 資源健康情況無法判斷資源的 hello 健全狀況因為它已經停止接收其相關資訊。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-122">Unknown: Resource health can not determine hello health of a resource because it has stopped receiving information about it.</span></span> 

## <a name="what-does-hello-unknown-status-mean-is-something-wrong-with-my-resource"></a><span data-ttu-id="2a2bd-123">功能沒有 hello 未知的狀態標準嗎？</span><span class="sxs-lookup"><span data-stu-id="2a2bd-123">What does hello unknown status mean?</span></span> <span data-ttu-id="2a2bd-124">我的資源有什麼問題嗎？</span><span class="sxs-lookup"><span data-stu-id="2a2bd-124">Is something wrong with my resource?</span></span>
<span data-ttu-id="2a2bd-125">hello 健全狀況狀態會設定 toounknown，當資源健全狀況會停止接收特定資源的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-125">hello health status is set toounknown when Resource Health stops receiving information about a specific resource.</span></span> <span data-ttu-id="2a2bd-126">雖然這個狀態不是最終指示 hello 狀態 hello 資源，請在您遇到的問題，可能表示發生 Azure 的問題。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-126">While this status is not a definitive indication of hello state of hello resource, in cases where you are experiencing problems, it may indicate there is an Azure problem.</span></span>

## <a name="how-can-i-get-help-for-a-resource-that-is-unavailable"></a><span data-ttu-id="2a2bd-127">如何取得無法使用的資源說明？</span><span class="sxs-lookup"><span data-stu-id="2a2bd-127">How can I get help for a resource that is unavailable?</span></span>
<span data-ttu-id="2a2bd-128">您可以提交支援要求的 hello 資源健全狀況 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-128">You can submit a support request from hello Resource Health blade.</span></span> <span data-ttu-id="2a2bd-129">Hello 資源無法使用時不需要支援合約與 Microsoft tooopen 要求因為平台事件。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-129">You do not need a support agreement with Microsoft tooopen a request when hello resource is unavailable because platform events.</span></span>

## <a name="does-resource-health-differentiate-between-unavailability-cased-by-platform-problems-versus-something-i-did"></a><span data-ttu-id="2a2bd-130">資源健康狀態是否會區分依平台問題歸類為無法使用的案例與我所做的事情？</span><span class="sxs-lookup"><span data-stu-id="2a2bd-130">Does Resource Health differentiate between unavailability cased by platform problems versus something I did?</span></span>
<span data-ttu-id="2a2bd-131">[是]，資源無法使用時，資源健全狀況會識別其中一個類別中的 hello 根本原因：</span><span class="sxs-lookup"><span data-stu-id="2a2bd-131">Yes, when a resource is unavailable, Resource Health identifies hello root cause within one of these categories:</span></span> 
-   <span data-ttu-id="2a2bd-132">使用者啟動的動作</span><span class="sxs-lookup"><span data-stu-id="2a2bd-132">User initiated action</span></span>
-   <span data-ttu-id="2a2bd-133">規劃的事件</span><span class="sxs-lookup"><span data-stu-id="2a2bd-133">Planned event</span></span> 
-   <span data-ttu-id="2a2bd-134">未規劃的事件</span><span class="sxs-lookup"><span data-stu-id="2a2bd-134">Unplanned event</span></span>

<span data-ttu-id="2a2bd-135">在 hello 入口網站會顯示使用者起始動作使用藍色的通知圖示，而使用紅色警告圖示顯示計劃與非計劃的事件。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-135">In hello portal, user initiated actions are shown using a blue notification icon, while planned and unplanned events are shown using a red warning icon.</span></span> <span data-ttu-id="2a2bd-136">提供詳細資訊在 hello[資源健全狀況概觀](Resource-health-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-136">More details are provided in hello [Resource Health overview](Resource-health-overview.md).</span></span>  

## <a name="can-i-integrate-resource-health-with-my-monitoring-tools"></a><span data-ttu-id="2a2bd-137">可以將資源健康狀態與我的監視工具進行整合嗎？</span><span class="sxs-lookup"><span data-stu-id="2a2bd-137">Can I integrate Resource Health with my monitoring tools?</span></span>
<span data-ttu-id="2a2bd-138">資源健全狀況是您診斷及降低 Azure 服務的問題會影響您的資源服務，其設計的 toohelp。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-138">Resource health is a service designed toohelp you diagnose and mitigate Azure service issues that impact your resources.</span></span> <span data-ttu-id="2a2bd-139">雖然您可以使用 hello 資源健全狀況 API tooprogrammatically 取得 hello 健全狀況狀態，我們建議使用度量 toomonitor 您的資源。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-139">While you can use hello Resource Health API tooprogrammatically obtain hello health status, we recommend you use metrics toomonitor your resources.</span></span> <span data-ttu-id="2a2bd-140">一旦偵測到問題時，資源健全狀況可協助您判斷 hello 根本原因，並引導您完成動作 tooaddress 它們。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-140">Once an issue is detected, Resource Health helps you determine hello root cause and guides you through actions tooaddress them.</span></span> <span data-ttu-id="2a2bd-141">請瀏覽[Azure 監視器](https://docs.microsoft.com/azure/monitoring-and-diagnostics/)toolearn 深入了解如何使用度量 toocheck 您的資源。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-141">Visit [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) toolearn more about how you can use metrics toocheck your resources.</span></span>

## <a name="where-do-i-find-resource-health"></a><span data-ttu-id="2a2bd-142">哪裡可以找到資源健康狀態？</span><span class="sxs-lookup"><span data-stu-id="2a2bd-142">Where do I find Resource Health?</span></span>
<span data-ttu-id="2a2bd-143">在您登入 toohello Azure 入口網站之後，有多個方式可以存取資源健全狀況：</span><span class="sxs-lookup"><span data-stu-id="2a2bd-143">After you log in toohello Azure portal, there are multiple ways you can access Resource Health:</span></span>
- <span data-ttu-id="2a2bd-144">瀏覽 tooyour 資源。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-144">Navigate tooyour resource.</span></span> <span data-ttu-id="2a2bd-145">在 hello 左側導覽中，選取 **資源健全狀況**</span><span class="sxs-lookup"><span data-stu-id="2a2bd-145">In hello left-hand navigation, select **Resource health**</span></span>
- <span data-ttu-id="2a2bd-146">移 toohello Azure 監視器刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-146">Go toohello Azure Monitor blade.</span></span>  <span data-ttu-id="2a2bd-147">在 hello 左側導覽中，選取 **資源健全狀況**。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-147">In hello left-hand navigation, select **Resource health**.</span></span>
- <span data-ttu-id="2a2bd-148">開啟 hello**說明 + 支援**刀鋒視窗中選取 hello 問號 hello 右上角的 hello 入口網站，然後選取 **說明 + 支援**。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-148">Open hello **Help + Support** blade by selecting hello question mark in hello upper right corner of hello portal and then selecting **Help + Support**.</span></span> <span data-ttu-id="2a2bd-149">一旦 hello 刀鋒視窗中開啟時，請選取**資源健全狀況**</span><span class="sxs-lookup"><span data-stu-id="2a2bd-149">Once hello blade opens, select **Resource health**</span></span>

<span data-ttu-id="2a2bd-150">您也可以使用 hello 資源健全狀況 API tooobtain hello 健全狀況的資訊資源。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-150">You can also use hello Resource Health API tooobtain information about hello health of your resources.</span></span>

## <a name="is-resource-health-available-for-all-resource-types"></a><span data-ttu-id="2a2bd-151">資源健康狀態是否適用於所有的資源類型？</span><span class="sxs-lookup"><span data-stu-id="2a2bd-151">Is Resource Health available for all resource types?</span></span>
<span data-ttu-id="2a2bd-152">hello 健全狀況檢查和支援透過資源健全狀況的資源類型的清單可以找到[這裡](resource-health-checks-resource-types.md)。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-152">hello list of health checks and resource types supported through Resource Health can be found [here](resource-health-checks-resource-types.md).</span></span>

## <a name="what-should-i-do-if-my-resource-is-showing-available-but-i-believe-it-is-not"></a><span data-ttu-id="2a2bd-153">如果我的資源顯示無法使用，但我認為它可以使用，該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="2a2bd-153">What should I do if my resource is showing available but I believe it is not?”</span></span>
<span data-ttu-id="2a2bd-154">檢查資源的 hello 健全狀況下 hello 健全狀況狀態，, 您可以按一下 **報告不正確的健全狀況狀態**。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-154">When checking hello health of a resource, right under hello health status you can click **Report incorrect health status**.</span></span> <span data-ttu-id="2a2bd-155">之前送出 hello 報表，您可以先 hello 選項提供您為何認為 hello 目前的健全狀況狀態不正確的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-155">Before submitting hello report, you have hello option of providing additional details on why you believe hello current health status is incorrect.</span></span>

## <a name="is-resource-health-available-for-all-azure-regions"></a><span data-ttu-id="2a2bd-156">資源健康狀態是否適用於所有的 Azure 區域？</span><span class="sxs-lookup"><span data-stu-id="2a2bd-156">Is Resource Health available for all Azure regions?</span></span> 
<span data-ttu-id="2a2bd-157">資源健全狀況有跨所有 Azure geos，除了下列區域的 hello:</span><span class="sxs-lookup"><span data-stu-id="2a2bd-157">Resource health is available in across all Azure geos except hello following regions:</span></span>
- <span data-ttu-id="2a2bd-158">美國政府維吉尼亞州</span><span class="sxs-lookup"><span data-stu-id="2a2bd-158">US Gov Virginia</span></span>
- <span data-ttu-id="2a2bd-159">美國政府愛荷華州</span><span class="sxs-lookup"><span data-stu-id="2a2bd-159">US Gov Iowa</span></span>
- <span data-ttu-id="2a2bd-160">美國 DoD 東部</span><span class="sxs-lookup"><span data-stu-id="2a2bd-160">US DoD East</span></span>
- <span data-ttu-id="2a2bd-161">美國國防部中央</span><span class="sxs-lookup"><span data-stu-id="2a2bd-161">US DoD Central</span></span>
- <span data-ttu-id="2a2bd-162">德國中部</span><span class="sxs-lookup"><span data-stu-id="2a2bd-162">Germany Central</span></span>
- <span data-ttu-id="2a2bd-163">德國東北部</span><span class="sxs-lookup"><span data-stu-id="2a2bd-163">Germany Northeast</span></span>
- <span data-ttu-id="2a2bd-164">中國東部</span><span class="sxs-lookup"><span data-stu-id="2a2bd-164">China East</span></span>
- <span data-ttu-id="2a2bd-165">中國北部</span><span class="sxs-lookup"><span data-stu-id="2a2bd-165">China North</span></span>

## <a name="how-is-resource-health-different-from-hello-service-health-dashboard-or-hello-azure-portal-service-notifications"></a><span data-ttu-id="2a2bd-166">如何為資源健全狀況不同 hello 服務健全狀況儀表板或 hello Azure 入口網站服務通知？</span><span class="sxs-lookup"><span data-stu-id="2a2bd-166">How is Resource Health different from hello Service Health Dashboard or hello Azure portal service notifications?</span></span>
<span data-ttu-id="2a2bd-167">所提供的 hello Azure 服務健全狀況儀表板更特定的資源健全狀況所提供的 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-167">hello information provided by Resource Health is more specific than what is provided by hello Azure Service Health Dashboard.</span></span>

<span data-ttu-id="2a2bd-168">而[Azure 狀態](https://status.azure.com)和 hello 入口網站服務通知可通知您有關服務的問題會影響一組廣泛的客戶 （例如 Azure 地區）、 資源健全狀況公開才相關的更多細微性事件toohello 特定資源。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-168">Whereas [Azure Status](https://status.azure.com) and hello portal service notifications inform you about service issues that affect a broad set of customers (for example an Azure region), Resource Health exposes more granular events that are relevant only toohello specific resource.</span></span> <span data-ttu-id="2a2bd-169">例如，如果主機意外重新啟動，資源健康狀態只會警示虛擬機器在該主機上執行的客戶。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-169">For example, if a host unexpectedly reboots, Resource Health alerts only those customers whose virtual machines were running on that host.</span></span>

<span data-ttu-id="2a2bd-170">它是重要的 toonotice 該 tooprovide 完成事件影響您的資源，資源健全狀況也在服務通知發行事件介面的可見性，而且 hello 服務健全狀況儀表板。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-170">It is important toonotice that tooprovide you complete visibility of events impacting your resources, Resource Health also surfaces events published in Service notifications and hello Service Health Dashboard.</span></span>

## <a name="do-i-need-tooactivate-resource-health-for-each-resource"></a><span data-ttu-id="2a2bd-171">需要針對每個資源 tooactivate 資源健康情況嗎？</span><span class="sxs-lookup"><span data-stu-id="2a2bd-171">Do I need tooactivate Resource Health for each resource?</span></span>
<span data-ttu-id="2a2bd-172">否，健康情況資訊適用於可透過資源健康狀態提供的所有資源類型。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-172">No, health information is available for all resource types available through Resource Health.</span></span> 

## <a name="do-we-need-tooenable-resource-health-for-my-organization"></a><span data-ttu-id="2a2bd-173">我們讓我的組織需要 tooenable 資源健全狀況？</span><span class="sxs-lookup"><span data-stu-id="2a2bd-173">Do we need tooenable Resource Health for my organization?</span></span>
<span data-ttu-id="2a2bd-174">否。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-174">No.</span></span>  <span data-ttu-id="2a2bd-175">Hello 不需要進行任何設定的 Azure 入口網站內存取 azure 資源健全狀況。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-175">Azure Resource Health is accessible within hello Azure portal without any setup requirements.</span></span>

## <a name="is-resource-health-available-free-of-charge"></a><span data-ttu-id="2a2bd-176">是否可免費使用資源健康狀態？</span><span class="sxs-lookup"><span data-stu-id="2a2bd-176">Is Resource Health available free of charge?</span></span>
<span data-ttu-id="2a2bd-177">是。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-177">Yes.</span></span>  <span data-ttu-id="2a2bd-178">Azure 資源健康狀態是免費的。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-178">Azure Resource Health is free of charge.</span></span>

## <a name="what-are-hello-recommendations-that-resource-health-provides"></a><span data-ttu-id="2a2bd-179">提供資源健全狀況的 hello 建議有哪些？</span><span class="sxs-lookup"><span data-stu-id="2a2bd-179">What are hello recommendations that Resource Health provides?</span></span>
<span data-ttu-id="2a2bd-180">根據 hello 健全狀況狀態，資源健全狀況為您提供您所花費的疑難排解建議 hello 目標是減少 hello 時間。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-180">Based on hello health status, Resource Health provides you with recommendations with hello goal of reducing hello time you spent troubleshooting.</span></span> <span data-ttu-id="2a2bd-181">如需可用的資源，hello 建議焦點放在 toosolve hello 最常見的問題客戶遇到的方式。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-181">For available resources, hello recommendations focus on how toosolve hello most common problems customers encounter.</span></span> <span data-ttu-id="2a2bd-182">如果無法使用，因為在 hello 資源 tooan Azure 未規劃的事件，hello 焦點會在您的協助期間和之後 hello 復原程序。</span><span class="sxs-lookup"><span data-stu-id="2a2bd-182">If hello resource is unavailable due tooan Azure unplanned event, hello focus will be on assisting you during and after hello recovery process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="2a2bd-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2a2bd-183">Next steps</span></span>

<span data-ttu-id="2a2bd-184">深入了解資源健康狀態：</span><span class="sxs-lookup"><span data-stu-id="2a2bd-184">Learn more about Resource Health:</span></span>
-  [<span data-ttu-id="2a2bd-185">Azure 資源健康狀態概觀</span><span class="sxs-lookup"><span data-stu-id="2a2bd-185">Azure Resource Health overview</span></span>](Resource-health-overview.md)
-  [<span data-ttu-id="2a2bd-186">可透過 Azure 資源健康狀態使用的資源類型和健康檢查</span><span class="sxs-lookup"><span data-stu-id="2a2bd-186">Resource types and health checks available through Azure Resource Health</span></span>](resource-health-checks-resource-types.md)
