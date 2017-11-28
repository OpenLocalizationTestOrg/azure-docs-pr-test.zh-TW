---
title: "Estimate Azure RemoteApp network bandwidth usage (評估 Azure RemoteApp 網路頻寬使用量) | Microsoft Docs"
description: "深入了解 Azure RemoteApp 集合和應用程式的網路頻寬需求。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 3127f4c7-f532-46c3-ba9b-649f647abec1
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 16b4ba974742d004ea02e3f83e522b9c43f2ef40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="estimate-azure-remoteapp-network-bandwidth-usage"></a><span data-ttu-id="ed6a3-103">Estimate Azure RemoteApp network bandwidth usage (評估 Azure RemoteApp 網路頻寬使用量)</span><span class="sxs-lookup"><span data-stu-id="ed6a3-103">Estimate Azure RemoteApp network bandwidth usage</span></span>
> [!IMPORTANT]
> <span data-ttu-id="ed6a3-104">Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。</span><span class="sxs-lookup"><span data-stu-id="ed6a3-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="ed6a3-105">如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。</span><span class="sxs-lookup"><span data-stu-id="ed6a3-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="ed6a3-106">Azure RemoteApp 使用遠端桌面通訊協定 (RDP)，在 Azure 雲端中執行的應用程式與您的使用者之間進行通訊。</span><span class="sxs-lookup"><span data-stu-id="ed6a3-106">Azure RemoteApp uses the Remote Desktop Protocol (RDP) to communicate between applications running in the Azure cloud and your users.</span></span> <span data-ttu-id="ed6a3-107">本文提供一些基本指導方針，可用來評估該網路使用量，也可能評估每位 Azure RemoteApp 使用者的網路頻寬使用量。</span><span class="sxs-lookup"><span data-stu-id="ed6a3-107">This article provides some basic guidelines you can use to estimate that network usage and potentially evaluate network bandwidth usage per Azure RemoteApp user.</span></span>

<span data-ttu-id="ed6a3-108">估計每位使用者的頻寬使用量十分複雜，而且需要在多工作業案例中同時執行多個應用程式，而在此案例中，根據網路頻寬需求，應用程式可能會影響彼此的效能。</span><span class="sxs-lookup"><span data-stu-id="ed6a3-108">Estimating bandwidth usage per user is very complex and requires running multiple applications simultaneously in multitasking scenarios where applications might impact each other's performance based on their demand for network bandwidth.</span></span> <span data-ttu-id="ed6a3-109">遠端桌面用戶端類型 (例如 Mac 用戶端與 HTML5 用戶端) 甚至可能會導致不同的頻寬結果。</span><span class="sxs-lookup"><span data-stu-id="ed6a3-109">Even the type of Remote Desktop client (such as Mac client versus HTML5 client) can lead to different bandwidth results.</span></span> <span data-ttu-id="ed6a3-110">為了協助您解決這些難題，我們將使用案例分成數個複寫真實案例的常用類別。</span><span class="sxs-lookup"><span data-stu-id="ed6a3-110">To help you work through these complications, we'll break the usage scenarios into several of the common categories to replicate real-world scenarios.</span></span> <span data-ttu-id="ed6a3-111">(當然，在真實案例中，混合使用各種類別，而且會依使用者而不同)。</span><span class="sxs-lookup"><span data-stu-id="ed6a3-111">(Where the real-world scenario is, of course, a mix of categories and differs by user.)</span></span>

<span data-ttu-id="ed6a3-112">在繼續之前，請注意，我們假設 RDP 透過低於 120 毫秒的延遲和高於 5 MB 的頻寬，提供網路上的大多數使用案例擁有極佳體驗；這是根據 RDP 使用可用網路頻寬和預估應用程式頻寬需求來進行動態調整的能力。</span><span class="sxs-lookup"><span data-stu-id="ed6a3-112">Before we go further - note that we assume RDP provides a good to excellent experience for most usage scenarios on networks with latency below 120 ms and bandwidth over 5 MBs - this is based on RDP's ability to dynamically adjust by using the available network bandwidth and the estimated application bandwidth needs.</span></span> <span data-ttu-id="ed6a3-113">本文並不僅止於這些「大部分使用案例」，在其中，案例會開始回溯，而使用者體驗會開始下降。</span><span class="sxs-lookup"><span data-stu-id="ed6a3-113">This article goes beyond those "most usage scenarios" to look at the edge, where scenarios begin to unwind and user experience begins to degrade.</span></span>

<span data-ttu-id="ed6a3-114">現在，請參閱下列文章來取得詳細資料 (包括要考量的因素、基準建議，以及未包含在我們的估計值中的項目)。</span><span class="sxs-lookup"><span data-stu-id="ed6a3-114">Now check out the following articles for the details, including factors to consider, baseline recommendations, and what we did not include in our estimates.</span></span>

* [<span data-ttu-id="ed6a3-115">How do network bandwidth and quality of experience work together? (如何兼顧網路頻寬和體驗品質？)</span><span class="sxs-lookup"><span data-stu-id="ed6a3-115">How do network bandwidth and quality of experience work together?</span></span>](remoteapp-bandwidthexperience.md)
* [<span data-ttu-id="ed6a3-116">Testing your network bandwidth usage with some common scenarios (利用一些常見案例測試您的網路頻寬使用量)</span><span class="sxs-lookup"><span data-stu-id="ed6a3-116">Testing your network bandwidth usage with some common scenarios</span></span>](remoteapp-bandwidthtests.md)
* [<span data-ttu-id="ed6a3-117">Quick guidelines if you don't have the time or ability to test (沒有時間或測試能力時的快速指導方針)</span><span class="sxs-lookup"><span data-stu-id="ed6a3-117">Quick guidelines if you don't have the time or ability to test</span></span>](remoteapp-bandwidthguidelines.md)

## <a name="what-are-we-not-including"></a><span data-ttu-id="ed6a3-118">未包含的內容</span><span class="sxs-lookup"><span data-stu-id="ed6a3-118">What are we not including?</span></span>
<span data-ttu-id="ed6a3-119">當您檢閱建議的測試和我們的整體 (和公認的一般) 建議時，請注意有數個我們未考慮到的因素。</span><span class="sxs-lookup"><span data-stu-id="ed6a3-119">When you review the proposed tests and our overall (and admittedly generic) recommendations, be aware that there are several factors that we did not consider.</span></span> <span data-ttu-id="ed6a3-120">例如，上傳與下載頻寬的不對稱本質所提供的使用者體驗難題。</span><span class="sxs-lookup"><span data-stu-id="ed6a3-120">For example, the user experience complications provided by the asymmetric nature of upload vs. download bandwidth.</span></span> <span data-ttu-id="ed6a3-121">大部分 Wi-Fi 網路的不對稱本質會額外影響效能和使用者體驗觀感。</span><span class="sxs-lookup"><span data-stu-id="ed6a3-121">The asymmetric nature of most Wi-Fi networks will additionally impact the performance and the user experience perception.</span></span> <span data-ttu-id="ed6a3-122">在互動式案例中，下游流量的優先順序低於上游，而這可能會增加遺失視訊或音訊框架數目，因此影響使用者對串流體驗的觀感。</span><span class="sxs-lookup"><span data-stu-id="ed6a3-122">For interactive scenarios the downstream traffic may be prioritized lower than the upstream, which may increase the number of lost video or audio frames and therefore impact the user perception of the streaming experience.</span></span> <span data-ttu-id="ed6a3-123">您可以進行您自己的實驗，了解什麼最適合您的特定使用案例和網路。</span><span class="sxs-lookup"><span data-stu-id="ed6a3-123">You can run your own experiments to see what is good for your specific use case and network.</span></span>

<span data-ttu-id="ed6a3-124">雖然我們討論裝置重新導向，但是我們未考慮已連接裝置 (例如儲存體、印表機、掃描器、網路攝影機和其他 USB 裝置) 所造成之網路流量的頻寬影響。</span><span class="sxs-lookup"><span data-stu-id="ed6a3-124">Although we discuss device redirection, we did not take into consideration the bandwidth impact of the network traffic caused by attached devices, like storage, printers, scanners, web cameras, and other USB devices.</span></span> <span data-ttu-id="ed6a3-125">這些裝置通常會暫時導致頻寬需求變高，並在工作完成時回復正常。</span><span class="sxs-lookup"><span data-stu-id="ed6a3-125">The effect of those devices usually spikes the bandwidth needs temporarily and goes away when the task is complete.</span></span> <span data-ttu-id="ed6a3-126">但是，如果經常這樣做，則頻寬需求可能會相當可觀。</span><span class="sxs-lookup"><span data-stu-id="ed6a3-126">But if done frequently, that bandwidth demand could be quite noticeable.</span></span>

<span data-ttu-id="ed6a3-127">我們也不會討論一位使用者對相同網路內的其他使用者的影響。</span><span class="sxs-lookup"><span data-stu-id="ed6a3-127">We also do not discuss how one user can impact other users within the same network.</span></span> <span data-ttu-id="ed6a3-128">例如，在 100 MB/s 網路上使用 4K 視訊的一位使用者可能會大幅地影響該相同網路內嘗試執行相同工作的其他使用者。</span><span class="sxs-lookup"><span data-stu-id="ed6a3-128">For example, one user consuming 4K video on a 100 MB/s network might significantly impact other users on that same network trying to do the same task.</span></span> <span data-ttu-id="ed6a3-129">不幸的是，越來越難判斷並行使用的影響，以提供有關系統整體效能的通用或全方位建議。</span><span class="sxs-lookup"><span data-stu-id="ed6a3-129">Unfortunately it gets progressively harder to determine the impact of concurrent usage to give a common or all-encompassing recommendation about how the system performs at aggregate.</span></span> <span data-ttu-id="ed6a3-130">我們只能說基礎通訊協定技術會善用可用的網路頻寬，但有其限制。</span><span class="sxs-lookup"><span data-stu-id="ed6a3-130">All we can say is that the underlying protocol technology will make the best use of the available network bandwidth, but it does have its limitations.</span></span>

