---
title: "Microsoft Azure 雲端服務之應用程式和服務可用性問題的常見問題集 | Microsoft Docs"
description: "本文列出 Microsoft Azure 雲端服務之應用程式和服務可用性的相關常見問題集。"
services: cloud-services
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 84985660-2cfd-483a-8378-50eef6a0151d
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: a893a6d009dd018ad440964419e0a5a1963084b4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="application-and-service-availability-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a><span data-ttu-id="77ab5-103">Azure 雲端服務之應用程式和服務可用性問題：常見問題集 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="77ab5-103">Application and service availability issues for Azure Cloud Services: Frequently asked questions (FAQs)</span></span>

<span data-ttu-id="77ab5-104">本文包含 [Microsoft Azure 雲端服務](https://azure.microsoft.com/services/cloud-services)之應用程式和服務可用性問題的相關常見問題集。</span><span class="sxs-lookup"><span data-stu-id="77ab5-104">This article includes frequently asked questions about application and service availability issues for [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services).</span></span> <span data-ttu-id="77ab5-105">您也可以參閱 [雲端服務 VM 大小頁面](cloud-services-sizes-specs.md) 以取得大小資訊。</span><span class="sxs-lookup"><span data-stu-id="77ab5-105">You can also consult the [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-role-got-recycled-was-there-any-update-rolled-out-for-my-cloud-service"></a><span data-ttu-id="77ab5-106">我的角色被回收了。</span><span class="sxs-lookup"><span data-stu-id="77ab5-106">My role got recycled.</span></span> <span data-ttu-id="77ab5-107">我的雲端服務是否推出任何更新？</span><span class="sxs-lookup"><span data-stu-id="77ab5-107">Was there any update rolled out for my cloud service?</span></span>
<span data-ttu-id="77ab5-108">Microsoft 大約一個月會發行一次適用於 Windows Azure PaaS VM 的新客體 OS 版本。</span><span class="sxs-lookup"><span data-stu-id="77ab5-108">Roughly once a month, Microsoft releases a new Guest OS version for Windows Azure PaaS VMs.</span></span><span data-ttu-id="77ab5-109"> 客體作業系統只是這過程中的一項更新。</span><span class="sxs-lookup"><span data-stu-id="77ab5-109"> The Guest OS is only one such update in the pipeline.</span></span> <span data-ttu-id="77ab5-110">發行可能會受到許多其他因素所影響。</span><span class="sxs-lookup"><span data-stu-id="77ab5-110">A release can be affected by many other factors.</span></span> <span data-ttu-id="77ab5-111">此外，Azure 是在成千上萬個電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="77ab5-111">In addition, Azure runs on hundreds of thousands of machines.</span></span> <span data-ttu-id="77ab5-112">因此，不可能預測您的角色重新啟動的確切日期和時間。</span><span class="sxs-lookup"><span data-stu-id="77ab5-112">Therefore, it's impossible to predict the exact date and time when your roles will reboot.</span></span> <span data-ttu-id="77ab5-113">我們會在客體 OS 更新 RSS 摘要中隨時提供最新資訊，但您應將該報告的時間視為大約的值。</span><span class="sxs-lookup"><span data-stu-id="77ab5-113">We update the Guest OS Update RSS Feed with the latest information that we have, but you should consider that reported time to be an approximate value.</span></span> <span data-ttu-id="77ab5-114">我們知道這對客戶造成困擾，所以正計劃對重新啟動設限或精確訂定時間。</span><span class="sxs-lookup"><span data-stu-id="77ab5-114">We are aware that this is problematic for customers and are working on a plan to limit or precisely time reboots.</span></span>

<span data-ttu-id="77ab5-115">如需最新客體 OS 更新的完整詳細資訊，請參閱 [Azure 客體 OS 版本與 SDK 相容性矩陣](cloud-services-guestos-update-matrix.md)。</span><span class="sxs-lookup"><span data-stu-id="77ab5-115">For complete details about recent Guest OS updates, see [Azure Guest OS releases and SDK compatibility matrix](cloud-services-guestos-update-matrix.md).</span></span>

<span data-ttu-id="77ab5-116">如需有關重新啟動的實用資訊，以及客體和主機 OS 更新的技術細節線索，請參閱[角色執行個體因 OS 升級而重新啟動 (英文)](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx) 的 MSDN 部落格文章。</span><span class="sxs-lookup"><span data-stu-id="77ab5-116">For helpful information on restarts and pointers to technical details of Guest and Host OS updates, see the MSDN blog post [Role Instance Restarts Due to OS Upgrades](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx).</span></span>

## <a name="why-does-the-first-request-to-my-cloud-service-after-the-service-has-been-idle-for-some-time-take-longer-than-usual"></a><span data-ttu-id="77ab5-117">為什麼在服務已閒置一段時間後，對我雲端服務的第一個要求所花費時間比平常更久？</span><span class="sxs-lookup"><span data-stu-id="77ab5-117">Why does the first request to my cloud service after the service has been idle for some time take longer than usual?</span></span>
<span data-ttu-id="77ab5-118">當網頁伺服器收到第一個要求時，會先重新編譯程式碼，然後再處理要求。</span><span class="sxs-lookup"><span data-stu-id="77ab5-118">When the Web Server receives the first request, it first recompiles the code and then processes the request.</span></span> <span data-ttu-id="77ab5-119">這就是第一個要求比其他要求更費時的原因。</span><span class="sxs-lookup"><span data-stu-id="77ab5-119">That's why the first request takes longer than the others.</span></span> <span data-ttu-id="77ab5-120">依預設，應用程式集區在使用者閒置的情況下會加以關閉。</span><span class="sxs-lookup"><span data-stu-id="77ab5-120">By default, the app pool gets shut down in cases of user inactivity.</span></span> <span data-ttu-id="77ab5-121">應用程式集區也會進行回收，預設為每隔 1,740 分鐘 (29 小時)。</span><span class="sxs-lookup"><span data-stu-id="77ab5-121">The app pool will also recycle by default every 1,740 minutes (29 hours).</span></span>

<span data-ttu-id="77ab5-122">可以定期將 Internet Information Services (IIS) 應用程式集區進行回收，以避免不穩定的狀態，可能會導致應用程式當機、停止回應，或記憶體流失等問題。</span><span class="sxs-lookup"><span data-stu-id="77ab5-122">Internet Information Services (IIS) application pools can be periodically recycled to avoid unstable states that can lead to application crashes, hangs, or memory leaks.</span></span>

<span data-ttu-id="77ab5-123">下列文件將協助您了解並減輕這個問題：</span><span class="sxs-lookup"><span data-stu-id="77ab5-123">The following documents will help you understand and mitigate this issue:</span></span>
* [<span data-ttu-id="77ab5-124">修正 IIS 的緩慢初始載入</span><span class="sxs-lookup"><span data-stu-id="77ab5-124">Fixing slow initial load for IIS</span></span>](http://stackoverflow.com/questions/13386471/fixing-slow-initial-load-for-iis)
* [<span data-ttu-id="77ab5-125">應用程式集區回收非常緩慢之後 IIS 7.5 Web 應用程式的第一個要求</span><span class="sxs-lookup"><span data-stu-id="77ab5-125">IIS 7.5 web application first request after app-pool recycle very slow</span></span>](http://stackoverflow.com/questions/13917205/iis-7-5-web-application-first-request-after-app-pool-recycle-very-slow)

<span data-ttu-id="77ab5-126">如果您想要變更 IIS 的預設行為，將需要使用啟動工作，因為如果您以手動方式將變更套用至 Web 角色執行個體，所做的變更最終將會遺失。</span><span class="sxs-lookup"><span data-stu-id="77ab5-126">If you want to change the default behavior of IIS, you will need to use startup tasks, because if you manually apply changes to the Web Role instances, the changes will eventually be lost.</span></span>

<span data-ttu-id="77ab5-127">如需詳細資訊，請參閱[如何設定和執行雲端服務的啟動工作](cloud-services-startup-tasks.md)。</span><span class="sxs-lookup"><span data-stu-id="77ab5-127">For more information, see [How to configure and run startup tasks for a cloud service](cloud-services-startup-tasks.md).</span></span>
