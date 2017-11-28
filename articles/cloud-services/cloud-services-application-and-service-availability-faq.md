---
title: "aaaApplication 和服務可用性問題的 Microsoft Azure 雲端服務的常見問題集 |Microsoft 文件"
description: "本文列出 hello 常見問題集有關應用程式和服務可用性的 Microsoft Azure 雲端服務。"
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
ms.openlocfilehash: cd0d9ba0beb1dc72d4761f8b89c2ecadb51c7e48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-availability-issues-for-azure-cloud-services-frequently-asked-questions-faqs"></a><span data-ttu-id="273c1-103">Azure 雲端服務之應用程式和服務可用性問題：常見問題集 (FAQ)</span><span class="sxs-lookup"><span data-stu-id="273c1-103">Application and service availability issues for Azure Cloud Services: Frequently asked questions (FAQs)</span></span>

<span data-ttu-id="273c1-104">本文包含 [Microsoft Azure 雲端服務](https://azure.microsoft.com/services/cloud-services)之應用程式和服務可用性問題的相關常見問題集。</span><span class="sxs-lookup"><span data-stu-id="273c1-104">This article includes frequently asked questions about application and service availability issues for [Microsoft Azure Cloud Services](https://azure.microsoft.com/services/cloud-services).</span></span> <span data-ttu-id="273c1-105">此外，您也可以參考 hello[雲端服務 VM 大小頁面](cloud-services-sizes-specs.md)大小資訊。</span><span class="sxs-lookup"><span data-stu-id="273c1-105">You can also consult hello [Cloud Services VM Size page](cloud-services-sizes-specs.md) for size information.</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-role-got-recycled-was-there-any-update-rolled-out-for-my-cloud-service"></a><span data-ttu-id="273c1-106">我的角色被回收了。</span><span class="sxs-lookup"><span data-stu-id="273c1-106">My role got recycled.</span></span> <span data-ttu-id="273c1-107">我的雲端服務是否推出任何更新？</span><span class="sxs-lookup"><span data-stu-id="273c1-107">Was there any update rolled out for my cloud service?</span></span>
<span data-ttu-id="273c1-108">Microsoft 大約一個月會發行一次適用於 Windows Azure PaaS VM 的新客體 OS 版本。</span><span class="sxs-lookup"><span data-stu-id="273c1-108">Roughly once a month, Microsoft releases a new Guest OS version for Windows Azure PaaS VMs.</span></span><span data-ttu-id="273c1-109"> 客體 OS 是 hello 管線中的只能有一個這類更新。</span><span class="sxs-lookup"><span data-stu-id="273c1-109"> The Guest OS is only one such update in hello pipeline.</span></span> <span data-ttu-id="273c1-110">發行可能會受到許多其他因素所影響。</span><span class="sxs-lookup"><span data-stu-id="273c1-110">A release can be affected by many other factors.</span></span> <span data-ttu-id="273c1-111">此外，Azure 是在成千上萬個電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="273c1-111">In addition, Azure runs on hundreds of thousands of machines.</span></span> <span data-ttu-id="273c1-112">因此，它是不可能 toopredict hello 確切日期和時間時將重新啟動您的角色。</span><span class="sxs-lookup"><span data-stu-id="273c1-112">Therefore, it's impossible toopredict hello exact date and time when your roles will reboot.</span></span> <span data-ttu-id="273c1-113">我們更新客體 OS 更新 RSS 摘要的 hello 與 hello 最新的資訊，我們有，但您應該考慮，報告時間 toobe 近似的值。</span><span class="sxs-lookup"><span data-stu-id="273c1-113">We update hello Guest OS Update RSS Feed with hello latest information that we have, but you should consider that reported time toobe an approximate value.</span></span> <span data-ttu-id="273c1-114">我們了解這是對於客戶而言有問題，並使用計劃 toolimit 或精確時間重新開機。</span><span class="sxs-lookup"><span data-stu-id="273c1-114">We are aware that this is problematic for customers and are working on a plan toolimit or precisely time reboots.</span></span>

<span data-ttu-id="273c1-115">如需最新客體 OS 更新的完整詳細資訊，請參閱 [Azure 客體 OS 版本與 SDK 相容性矩陣](cloud-services-guestos-update-matrix.md)。</span><span class="sxs-lookup"><span data-stu-id="273c1-115">For complete details about recent Guest OS updates, see [Azure Guest OS releases and SDK compatibility matrix](cloud-services-guestos-update-matrix.md).</span></span>

<span data-ttu-id="273c1-116">很有幫助的來賓和主機作業系統更新的重新啟動和指標 tootechnical 詳細資料的詳細資訊，請參閱 hello MSDN 部落格文章[角色執行個體因而重新啟動 tooOS 升級](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)。</span><span class="sxs-lookup"><span data-stu-id="273c1-116">For helpful information on restarts and pointers tootechnical details of Guest and Host OS updates, see hello MSDN blog post [Role Instance Restarts Due tooOS Upgrades](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx).</span></span>

## <a name="why-does-hello-first-request-toomy-cloud-service-after-hello-service-has-been-idle-for-some-time-take-longer-than-usual"></a><span data-ttu-id="273c1-117">為什麼沒有 hello 第一個要求 toomy 雲端服務之後，hello 服務閒置段時間比平常長？</span><span class="sxs-lookup"><span data-stu-id="273c1-117">Why does hello first request toomy cloud service after hello service has been idle for some time take longer than usual?</span></span>
<span data-ttu-id="273c1-118">Hello 網頁伺服器收到 hello 第一個要求時，它會先重新編譯 hello 程式碼，然後再處理 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="273c1-118">When hello Web Server receives hello first request, it first recompiles hello code and then processes hello request.</span></span> <span data-ttu-id="273c1-119">原因是其他人 hello 第一個要求所花費的時間比 hello。</span><span class="sxs-lookup"><span data-stu-id="273c1-119">That's why hello first request takes longer than hello others.</span></span> <span data-ttu-id="273c1-120">根據預設，hello 應用程式集區取得關閉在使用者閒置的情況下。</span><span class="sxs-lookup"><span data-stu-id="273c1-120">By default, hello app pool gets shut down in cases of user inactivity.</span></span> <span data-ttu-id="273c1-121">hello 應用程式集區將也會進行回收預設每隔 1,740 分鐘 （29 小時）。</span><span class="sxs-lookup"><span data-stu-id="273c1-121">hello app pool will also recycle by default every 1,740 minutes (29 hours).</span></span>

<span data-ttu-id="273c1-122">網際網路資訊服務 (IIS) 應用程式集區可以定期回收的 tooavoid 可能會導致 tooapplication 當機、 無回應或記憶體流失的不穩定狀態。</span><span class="sxs-lookup"><span data-stu-id="273c1-122">Internet Information Services (IIS) application pools can be periodically recycled tooavoid unstable states that can lead tooapplication crashes, hangs, or memory leaks.</span></span>

<span data-ttu-id="273c1-123">下列文件的 hello 將協助您了解並減輕這個問題：</span><span class="sxs-lookup"><span data-stu-id="273c1-123">hello following documents will help you understand and mitigate this issue:</span></span>
* [<span data-ttu-id="273c1-124">修正 IIS 的緩慢初始載入</span><span class="sxs-lookup"><span data-stu-id="273c1-124">Fixing slow initial load for IIS</span></span>](http://stackoverflow.com/questions/13386471/fixing-slow-initial-load-for-iis)
* [<span data-ttu-id="273c1-125">應用程式集區回收非常緩慢之後 IIS 7.5 Web 應用程式的第一個要求</span><span class="sxs-lookup"><span data-stu-id="273c1-125">IIS 7.5 web application first request after app-pool recycle very slow</span></span>](http://stackoverflow.com/questions/13917205/iis-7-5-web-application-first-request-after-app-pool-recycle-very-slow)

<span data-ttu-id="273c1-126">如果您想 toochange hello IIS 的預設行為，您需要 toouse 啟動工作，因為如果您手動套用變更 toohello Web 角色執行個體，最後會 hello 變更遺失。</span><span class="sxs-lookup"><span data-stu-id="273c1-126">If you want toochange hello default behavior of IIS, you will need toouse startup tasks, because if you manually apply changes toohello Web Role instances, hello changes will eventually be lost.</span></span>

<span data-ttu-id="273c1-127">如需詳細資訊，請參閱[tooconfigure] 和 [執行啟動工作的雲端服務的方式](cloud-services-startup-tasks.md)。</span><span class="sxs-lookup"><span data-stu-id="273c1-127">For more information, see [How tooconfigure and run startup tasks for a cloud service](cloud-services-startup-tasks.md).</span></span>
