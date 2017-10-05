---
title: "Azure 資源健康狀態常見問題集 | Microsoft Docs"
description: "Azure 資源健康狀態的概觀"
services: Resource health
documentationcenter: dev-center-name
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
ms.openlocfilehash: 41522a85cac05304b3ae60c45b48920eefbe8f5c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-resource-health-faq"></a><span data-ttu-id="526df-103">Azure 資源健康狀態常見問題集</span><span class="sxs-lookup"><span data-stu-id="526df-103">Azure Resource health FAQ</span></span>
<span data-ttu-id="526df-104">了解 Azure 資源健康狀態相關常見問題的答案。</span><span class="sxs-lookup"><span data-stu-id="526df-104">Learn the answers to common questions about Azure resource health.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="526df-105">常見問題集</span><span class="sxs-lookup"><span data-stu-id="526df-105">Frequently asked questions</span></span>
* [<span data-ttu-id="526df-106">何謂 Azure 資源健康狀態？</span><span class="sxs-lookup"><span data-stu-id="526df-106">What is Azure resource health?</span></span>](#what-is-azure-resource-health)
* [<span data-ttu-id="526df-107">資源健康狀態的目的為何？</span><span class="sxs-lookup"><span data-stu-id="526df-107">What is the resource health intended for?</span></span>](#what-is-the-resource-health-intended-for)
* [<span data-ttu-id="526df-108">資源健康狀態會執行哪些健全狀況檢查？</span><span class="sxs-lookup"><span data-stu-id="526df-108">What health checks are performed by resource health?</span></span>](#what-health-checks-are-performed-by-resource-health)
* [<span data-ttu-id="526df-109">每個健康情況所代表的意義為何？</span><span class="sxs-lookup"><span data-stu-id="526df-109">What does each of the health status mean?</span></span>](#what-does-each-of-the-health-status-mean)
* [<span data-ttu-id="526df-110">不明狀態的意義為何？我的資源有什麼問題嗎？</span><span class="sxs-lookup"><span data-stu-id="526df-110">What does the unknown status mean? Is something wrong with my resource?</span></span>](#what-does-the-unknown-status-mean-is-something-wrong-with-my-resource)
* [<span data-ttu-id="526df-111">如何取得無法使用的資源說明？</span><span class="sxs-lookup"><span data-stu-id="526df-111">How can I get help for a resource that is unavailable?</span></span>](#how-can-i-get-help-for-a-resource-that-is-unavailable)
* [<span data-ttu-id="526df-112">資源健康狀態是否會區分依平台問題歸類為無法使用的案例與我所做的事情？</span><span class="sxs-lookup"><span data-stu-id="526df-112">Does resource health differentiate between unavailability cased by platform problems versus something I did?</span></span>](#does-resource-health-differentiate-between-unavailability-cased-by-platform-problems-versus-something-i-did)
* [<span data-ttu-id="526df-113">可以將資源健康狀態與我的監視工具進行整合嗎？</span><span class="sxs-lookup"><span data-stu-id="526df-113">Can I integrate resource health with my monitoring tools?</span></span>](#can-i-integrate-resource-health-with-my-monitoring-tools)
* [<span data-ttu-id="526df-114">哪裡可以找到資源健康狀態？</span><span class="sxs-lookup"><span data-stu-id="526df-114">Where do I find resource health?</span></span>](#where-do-i-find-resource-health)
* [<span data-ttu-id="526df-115">資源健康狀態是否適用於所有的資源類型？</span><span class="sxs-lookup"><span data-stu-id="526df-115">Is resource health available for all resource types?</span></span>](#is-resource-health-available-for-all-resource-types)
* [<span data-ttu-id="526df-116">如果我的資源顯示無法使用，但我認為它可以使用，該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="526df-116">What should I do if my resource is showing available but I believe it is not?</span></span>](#what-should-i-do-if-my-resource-is-showing-available-but-i-believe-it-is-not)
* [<span data-ttu-id="526df-117">資源健康狀態是否適用於所有的 Azure 區域？</span><span class="sxs-lookup"><span data-stu-id="526df-117">Is resource health available for all Azure regions?</span></span>](#is-resource-health-available-for-all-azure-regions)
* [<span data-ttu-id="526df-118">資源健康狀態與服務健康情況儀表板或 Azure 入口網站服務通知有何不同？</span><span class="sxs-lookup"><span data-stu-id="526df-118">How is resource health different from the Service Health Dashboard or the Azure portal service notifications?</span></span>](#how-is-resource-health-different-from-the-service-health-dashboard-or-the-azure-portal-service-notifications)
* [<span data-ttu-id="526df-119">是否需要啟用每個資源的資源健康狀態？</span><span class="sxs-lookup"><span data-stu-id="526df-119">Do I need to activate resource health for each resource?</span></span>](#do-i-need-to-activate-resource-health-for-each-resource)
* [<span data-ttu-id="526df-120">我們是否需要為我的組織啟用資源健康狀態？</span><span class="sxs-lookup"><span data-stu-id="526df-120">Do we need to enable resource health for my organization?</span></span>](#do-we-need-to-enable-resource-health-for-my-organization)
* [<span data-ttu-id="526df-121">是否可免費使用資源健康狀態？</span><span class="sxs-lookup"><span data-stu-id="526df-121">Is resource health available free of charge?</span></span>](#is-resource-health-available-free-of-charge)
* [<span data-ttu-id="526df-122">資源健康狀態所提供的建議有哪些？</span><span class="sxs-lookup"><span data-stu-id="526df-122">What are the recommendations that resource health provides?</span></span>](#what-are-the-recommendations-that-resource-health-provides)


## <a name="what-is-azure-resource-health"></a><span data-ttu-id="526df-123">何謂 Azure 資源健康狀態？</span><span class="sxs-lookup"><span data-stu-id="526df-123">What is Azure resource health?</span></span>
<span data-ttu-id="526df-124">當 Azure 問題影響到您的資源健康狀態時，協助進行診斷並取得支援。</span><span class="sxs-lookup"><span data-stu-id="526df-124">Resource health helps you diagnose and get support when an Azure issue impacts your resources.</span></span> <span data-ttu-id="526df-125">它會通知您資源的目前及過去的健康狀態，並協助您解決問題。</span><span class="sxs-lookup"><span data-stu-id="526df-125">It informs you about the current and past health of your resources and helps you mitigate issues.</span></span> <span data-ttu-id="526df-126">資源健康狀態會在您需要解決 Azure 服務問題時提供技術支援。</span><span class="sxs-lookup"><span data-stu-id="526df-126">Resource health provides technical support when you need help with Azure service issues.</span></span>  

## <a name="what-is-the-resource-health-intended-for"></a><span data-ttu-id="526df-127">資源健康狀態的目的為何？</span><span class="sxs-lookup"><span data-stu-id="526df-127">What is the resource health intended for?</span></span>
<span data-ttu-id="526df-128">一旦偵測到發生問題的資源後，資源健康狀態便可協助您診斷根本原因。</span><span class="sxs-lookup"><span data-stu-id="526df-128">Once an issue with a resource has been detected, resource health can help you diagnose the root cause.</span></span> <span data-ttu-id="526df-129">它會協助減輕問題，並在您需要 Azure 服務問題的詳細說明時提供技術支援。</span><span class="sxs-lookup"><span data-stu-id="526df-129">It provides help to mitigate the issue and technical support when you need more help with Azure service issues.</span></span>

## <a name="what-health-checks-are-performed-by-resource-health"></a><span data-ttu-id="526df-130">資源健康狀態會執行哪些健康情況檢查？</span><span class="sxs-lookup"><span data-stu-id="526df-130">What health checks are performed by resource health?</span></span>
<span data-ttu-id="526df-131">資源健康狀態會根據[資源類型](resource-health-checks-resource-types.md)執行各種檢查。</span><span class="sxs-lookup"><span data-stu-id="526df-131">Resource health performs various checks based on the [resource type](resource-health-checks-resource-types.md).</span></span> <span data-ttu-id="526df-132">這些檢查旨在實作三種類型的問題︰</span><span class="sxs-lookup"><span data-stu-id="526df-132">These checks are designed to implement three types of issues:</span></span> 
1. <span data-ttu-id="526df-133">未規劃的事件，例如未預期的主機重新開機</span><span class="sxs-lookup"><span data-stu-id="526df-133">Unplanned events, for example an unexpected host reboot</span></span>
2. <span data-ttu-id="526df-134">規劃的事件，例如排程的主機作業系統更新</span><span class="sxs-lookup"><span data-stu-id="526df-134">Planned events, like scheduled host OS updates</span></span>
3. <span data-ttu-id="526df-135">使用者動作觸發的事件，例如使用者重新啟動虛擬機器</span><span class="sxs-lookup"><span data-stu-id="526df-135">Events triggered by user actions, for example a user rebooting a virtual machine</span></span>

## <a name="what-does-each-of-the-health-status-mean"></a><span data-ttu-id="526df-136">每個健全狀態所代表的意義為何？</span><span class="sxs-lookup"><span data-stu-id="526df-136">What does each of the health status mean?</span></span>
<span data-ttu-id="526df-137">有三個不同的健全狀態︰</span><span class="sxs-lookup"><span data-stu-id="526df-137">There are three different health statuses:</span></span>
1. <span data-ttu-id="526df-138">可用︰Azure 平台沒有任何可能會影響此資源的已知問題</span><span class="sxs-lookup"><span data-stu-id="526df-138">Available: There aren't any known problems in the Azure platform that could be impacting this resource</span></span>
2. <span data-ttu-id="526df-139">無法使用︰資源健康狀態偵測到會影響資源的問題</span><span class="sxs-lookup"><span data-stu-id="526df-139">Unavailable: Resource health has detected issues that are impacting the resource</span></span>
3. <span data-ttu-id="526df-140">未知︰資源健康狀態無法判斷資源的健康情況，因為它已停止接收相關的資訊。</span><span class="sxs-lookup"><span data-stu-id="526df-140">Unknown: Resource health can not determine the health of a resource because it has stopped receiving information about it.</span></span> 

## <a name="what-does-the-unknown-status-mean-is-something-wrong-with-my-resource"></a><span data-ttu-id="526df-141">不明狀態的意義為何？</span><span class="sxs-lookup"><span data-stu-id="526df-141">What does the unknown status mean?</span></span> <span data-ttu-id="526df-142">我的資源有什麼問題嗎？</span><span class="sxs-lookup"><span data-stu-id="526df-142">Is something wrong with my resource?</span></span>
<span data-ttu-id="526df-143">當資源健康狀態停止接收特定資源的相關資訊時，健全狀態會設定為未知。</span><span class="sxs-lookup"><span data-stu-id="526df-143">The health status is set to unknown when resource health stops receiving information about a specific resource.</span></span> <span data-ttu-id="526df-144">儘管此狀態不是資源狀態的明確指示，如果您遇到問題，則可能表示 Azure 發生問題。</span><span class="sxs-lookup"><span data-stu-id="526df-144">While this status is not a definitive indication of the state of the resource, in cases where you are experiencing problems, it may indicate there is an Azure problem.</span></span>

## <a name="how-can-i-get-help-for-a-resource-that-is-unavailable"></a><span data-ttu-id="526df-145">如何取得無法使用的資源說明？</span><span class="sxs-lookup"><span data-stu-id="526df-145">How can I get help for a resource that is unavailable?</span></span>
<span data-ttu-id="526df-146">您可以從 [資源健康狀態] 刀鋒視窗提交支援要求。</span><span class="sxs-lookup"><span data-stu-id="526df-146">You can submit a support request from the resource health blade.</span></span> <span data-ttu-id="526df-147">當資源因為平台事件而無法使用時，您無需 Microsoft 的支援合約即可將要求開啟。</span><span class="sxs-lookup"><span data-stu-id="526df-147">You do not need a support agreement with Microsoft to open a request when the resource is unavailable because platform events.</span></span>

## <a name="does-resource-health-differentiate-between-unavailability-cased-by-platform-problems-versus-something-i-did"></a><span data-ttu-id="526df-148">資源健康狀態是否會區分依平台問題歸類為無法使用的案例與我所做的事情？</span><span class="sxs-lookup"><span data-stu-id="526df-148">Does resource health differentiate between unavailability cased by platform problems versus something I did?</span></span>
<span data-ttu-id="526df-149">是，當資源無法使用時，資源健康狀態會識別下列其中一種類別內的根本原因︰</span><span class="sxs-lookup"><span data-stu-id="526df-149">Yes, when a resource is unavailable, resource health identifies the root cause within one of these categories:</span></span> 
1.  <span data-ttu-id="526df-150">使用者啟動的動作</span><span class="sxs-lookup"><span data-stu-id="526df-150">User initiated action</span></span>
2.  <span data-ttu-id="526df-151">規劃的事件</span><span class="sxs-lookup"><span data-stu-id="526df-151">Planned event</span></span> 
3.  <span data-ttu-id="526df-152">未規劃的事件</span><span class="sxs-lookup"><span data-stu-id="526df-152">Unplanned event</span></span>

<span data-ttu-id="526df-153">在入口網站中，會使用藍色通知圖示來顯示使用者啟動的動作，而規劃與未規劃的事件則會使用紅色警告圖示來顯示。</span><span class="sxs-lookup"><span data-stu-id="526df-153">In the portal, user initiated actions are shown using a blue notification icon, while planned and unplanned events are shown using a red warning icon.</span></span> <span data-ttu-id="526df-154">[資源健康狀態概觀](Resource-health-overview.md)中會提供更多詳細資料。</span><span class="sxs-lookup"><span data-stu-id="526df-154">More details are provided in the [resource health overview](Resource-health-overview.md).</span></span>  

## <a name="can-i-integrate-resource-health-with-my-monitoring-tools"></a><span data-ttu-id="526df-155">可以將資源健康狀態與我的監視工具進行整合嗎？</span><span class="sxs-lookup"><span data-stu-id="526df-155">Can I integrate resource health with my monitoring tools?</span></span>
<span data-ttu-id="526df-156">資源健康狀態是專為協助您診斷和解決會影響您資源的 Azure 服務問題所設計的服務。</span><span class="sxs-lookup"><span data-stu-id="526df-156">Resource health is a service designed to help you diagnose and mitigate Azure service issues that impact your resources.</span></span> <span data-ttu-id="526df-157">雖然您可以使用資源健康狀態 API 以程式設計方式取得健全狀態，我們建議您使用計量來監視您的資源。</span><span class="sxs-lookup"><span data-stu-id="526df-157">While you can use the resource health API to programmatically obtain the health status, we recommend you use metrics to monitor your resources.</span></span> <span data-ttu-id="526df-158">一旦偵測到問題後，資源健康狀態可協助您判斷根本原因，並引導您完成動作來解決這些問題。</span><span class="sxs-lookup"><span data-stu-id="526df-158">Once an issue is detected, resource health helps you determine the root cause and guides you through actions to address them.</span></span> <span data-ttu-id="526df-159">若要深入了解如何使用計量來檢查您的資源，請瀏覽 [Azure 監視器](https://docs.microsoft.com/azure/monitoring-and-diagnostics/)。</span><span class="sxs-lookup"><span data-stu-id="526df-159">Visit [Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/) to learn more about how you can use metrics to check your resources.</span></span>

## <a name="where-do-i-find-resource-health"></a><span data-ttu-id="526df-160">哪裡可以找到資源健康狀態？</span><span class="sxs-lookup"><span data-stu-id="526df-160">Where do I find resource health?</span></span>
<span data-ttu-id="526df-161">登入 Azure 入口網站之後，您可以使用多種方式來存取資源健康狀態︰</span><span class="sxs-lookup"><span data-stu-id="526df-161">After you log in to the Azure portal, there are multiple ways you can access resource health:</span></span>
1. <span data-ttu-id="526df-162">瀏覽至您的資源。</span><span class="sxs-lookup"><span data-stu-id="526df-162">Navigate to your resource.</span></span> <span data-ttu-id="526df-163">在左側導覽中，按一下 [資源健康狀態]。</span><span class="sxs-lookup"><span data-stu-id="526df-163">In the left-hand navigation, click **Resource health**.</span></span>
2. <span data-ttu-id="526df-164">移至 [Azure 監視器] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="526df-164">Go to the Azure Monitor blade.</span></span>  <span data-ttu-id="526df-165">在左側導覽中，按一下 [資源健康狀態]。</span><span class="sxs-lookup"><span data-stu-id="526df-165">In the left-hand navigation, click **Resource health**.</span></span>
3. <span data-ttu-id="526df-166">按一下入口網站右上角的問號，然後選取 [說明 + 支援]，即可將 [說明 + 支援] 刀鋒視窗開啟。</span><span class="sxs-lookup"><span data-stu-id="526df-166">Open the **Help + Support** blade by clicking the question mark in the upper right corner of the portal and then selecting **Help + Support**.</span></span> <span data-ttu-id="526df-167">將刀鋒視窗開啟後，按一下 [資源健康狀態]</span><span class="sxs-lookup"><span data-stu-id="526df-167">Once the blade opens, click **Resource health**</span></span>

<span data-ttu-id="526df-168">您也可以使用資源健康狀態 API 取得資源的健康情況相關資訊。</span><span class="sxs-lookup"><span data-stu-id="526df-168">You can also use the resource health API to obtain information about the health of your resources.</span></span>

## <a name="is-resource-health-available-for-all-resource-types"></a><span data-ttu-id="526df-169">資源健康狀態是否適用於所有的資源類型？</span><span class="sxs-lookup"><span data-stu-id="526df-169">Is resource health available for all resource types?</span></span>
<span data-ttu-id="526df-170">您可以在[這裡](resource-health-checks-resource-types.md)找到透過資源健康狀態支援的健康情況檢查和資源類型清單</span><span class="sxs-lookup"><span data-stu-id="526df-170">The list of health checks and resource types supported through resource health can be found [here](resource-health-checks-resource-types.md)</span></span>

## <a name="what-should-i-do-if-my-resource-is-showing-available-but-i-believe-it-is-not"></a><span data-ttu-id="526df-171">如果我的資源顯示無法使用，但我認為它可以使用，該怎麼辦？</span><span class="sxs-lookup"><span data-stu-id="526df-171">What should I do if my resource is showing available but I believe it is not?”</span></span>
<span data-ttu-id="526df-172">檢查資源的健康情況時，您可以在健全狀態下面按一下 [報告不正確的健全狀態]。</span><span class="sxs-lookup"><span data-stu-id="526df-172">When checking the health of a resource, right under the health status you can click **Report incorrect health status**.</span></span> <span data-ttu-id="526df-173">提交報表之前，您可以選擇提供為何您認為目前健全狀態不正確的其他相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="526df-173">Before submitting the report, you have the option of providing additional details on why you believe the current health status is incorrect.</span></span>

## <a name="is-resource-health-available-for-all-azure-regions"></a><span data-ttu-id="526df-174">資源健康狀態是否適用於所有的 Azure 區域？</span><span class="sxs-lookup"><span data-stu-id="526df-174">Is resource health available for all Azure regions?</span></span> 
<span data-ttu-id="526df-175">資源健康狀態可在所有 Azure 地區使用，除了下列區域︰</span><span class="sxs-lookup"><span data-stu-id="526df-175">Resource health is available in across all Azure geos except the following regions:</span></span>
* <span data-ttu-id="526df-176">美國政府維吉尼亞州</span><span class="sxs-lookup"><span data-stu-id="526df-176">US Gov Virginia</span></span>
* <span data-ttu-id="526df-177">美國政府愛荷華州</span><span class="sxs-lookup"><span data-stu-id="526df-177">US Gov Iowa</span></span>
* <span data-ttu-id="526df-178">美國 DoD 東部</span><span class="sxs-lookup"><span data-stu-id="526df-178">US DoD East</span></span>
* <span data-ttu-id="526df-179">美國國防部中央</span><span class="sxs-lookup"><span data-stu-id="526df-179">US DoD Central</span></span>
* <span data-ttu-id="526df-180">德國中部</span><span class="sxs-lookup"><span data-stu-id="526df-180">Germany Central</span></span>
* <span data-ttu-id="526df-181">德國東北部</span><span class="sxs-lookup"><span data-stu-id="526df-181">Germany Northeast</span></span>
* <span data-ttu-id="526df-182">中國東部</span><span class="sxs-lookup"><span data-stu-id="526df-182">China East</span></span>
* <span data-ttu-id="526df-183">中國北部</span><span class="sxs-lookup"><span data-stu-id="526df-183">China North</span></span>

## <a name="how-is-resource-health-different-from-the-service-health-dashboard-or-the-azure-portal-service-notifications"></a><span data-ttu-id="526df-184">資源健康狀態與服務健康狀態儀表板或 Azure 入口網站服務通知有何不同？</span><span class="sxs-lookup"><span data-stu-id="526df-184">How is resource health different from the Service Health Dashboard or the Azure portal service notifications?</span></span>
<span data-ttu-id="526df-185">資源健康狀態可提供比 Azure 服務健康情況儀表板更明確的資訊。</span><span class="sxs-lookup"><span data-stu-id="526df-185">The information provided by resource health is more specific than what is provided by the Azure Service Health Dashboard.</span></span>

<span data-ttu-id="526df-186">[Azure 狀態](https://status.azure.com)和入口網站服務通知會通知您影響大規模客戶 (例如 Azure 區域) 的服務問題，而資源健康狀態會公開更多僅與特定資源相關的細微事件。</span><span class="sxs-lookup"><span data-stu-id="526df-186">Whereas [Azure Status](https://status.azure.com) and the portal service notifications inform you about service issues that affect a broad set of customers (for example an Azure region), resource health exposes more granular events that are relevant only to the specific resource.</span></span> <span data-ttu-id="526df-187">例如，如果主機意外重新啟動，資源健康狀態只會警示虛擬機器在該主機上執行的客戶。</span><span class="sxs-lookup"><span data-stu-id="526df-187">For example, if a host unexpectedly reboots, resource health alerts only those customers whose virtual machines were running on that host.</span></span>

<span data-ttu-id="526df-188">請務必注意，為了讓您可完整看到影響您資源的事件，資源健康狀態也會呈現諸如服務通知和服務健康情況儀表板中發佈的事件。</span><span class="sxs-lookup"><span data-stu-id="526df-188">It is important to notice that to provide you complete visibility of events impacting your resources, resource health also surfaces events published in Service notifications and the Service Health Dashboard.</span></span>

## <a name="do-i-need-to-activate-resource-health-for-each-resource"></a><span data-ttu-id="526df-189">是否需要啟用每個資源的資源健康狀態？</span><span class="sxs-lookup"><span data-stu-id="526df-189">Do I need to activate resource health for each resource?</span></span>
<span data-ttu-id="526df-190">否，健康情況資訊適用於可透過資源健康狀態提供的所有資源類型。</span><span class="sxs-lookup"><span data-stu-id="526df-190">No, health information is available for all resource types available through resource health.</span></span> 

## <a name="do-we-need-to-enable-resource-health-for-my-organization"></a><span data-ttu-id="526df-191">我們是否需要為我的組織啟用資源健康狀態？</span><span class="sxs-lookup"><span data-stu-id="526df-191">Do we need to enable resource health for my organization?</span></span>
<span data-ttu-id="526df-192">不用。</span><span class="sxs-lookup"><span data-stu-id="526df-192">No.</span></span>  <span data-ttu-id="526df-193">不需要進行任何安裝程式即可在 Azure 入口網站內存取 Azure 資源健康狀態。</span><span class="sxs-lookup"><span data-stu-id="526df-193">Azure resource health is accessible within the Azure portal without any setup requirements.</span></span>

## <a name="is-resource-health-available-free-of-charge"></a><span data-ttu-id="526df-194">是否可免費使用資源健康狀態？</span><span class="sxs-lookup"><span data-stu-id="526df-194">Is resource health available free of charge?</span></span>
<span data-ttu-id="526df-195">是。</span><span class="sxs-lookup"><span data-stu-id="526df-195">Yes.</span></span>  <span data-ttu-id="526df-196">Azure 資源健康狀態是免費的。</span><span class="sxs-lookup"><span data-stu-id="526df-196">Azure resource health is free of charge.</span></span>

## <a name="what-are-the-recommendations-that-resource-health-provides"></a><span data-ttu-id="526df-197">資源健康狀態所提供的建議有哪些？</span><span class="sxs-lookup"><span data-stu-id="526df-197">What are the recommendations that resource health provides?</span></span>
<span data-ttu-id="526df-198">根據健全狀態，資源健康狀態會為您提供建議，旨在讓您減少疑難排解所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="526df-198">Based on the health status, resource health provides you with recommendations with the goal of reducing the time you spent troubleshooting.</span></span> <span data-ttu-id="526df-199">針對可用的資源，建議著重於如何解決客戶會發生的最常見問題。</span><span class="sxs-lookup"><span data-stu-id="526df-199">For available resources, the recommendations focus on how to solve the most common problems customers encounter.</span></span> <span data-ttu-id="526df-200">如果資源是因為 Azure 未規劃事件而無法使用，則會著重於在復原程序期間以及之後協助您。</span><span class="sxs-lookup"><span data-stu-id="526df-200">If the resource is unavailable due to an Azure unplanned event, the focus will be on assisting you during and after the recovery process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="526df-201">後續步驟</span><span class="sxs-lookup"><span data-stu-id="526df-201">Next steps</span></span>

<span data-ttu-id="526df-202">若要深入了解資源健康狀態，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="526df-202">Check out these resources to learn more about resource health:</span></span>
-  [<span data-ttu-id="526df-203">Azure 資源健康狀態概觀</span><span class="sxs-lookup"><span data-stu-id="526df-203">Azure resource health overview</span></span>](Resource-health-overview.md)
-  [<span data-ttu-id="526df-204">可透過 Azure 資源健康狀態使用的資源類型和健康檢查</span><span class="sxs-lookup"><span data-stu-id="526df-204">Resource types and health checks available through Azure resource health</span></span>](resource-health-checks-resource-types.md)
