---
title: "aaaPen 測試 |Microsoft 文件"
description: "hello 文件提供 hello 滲透測試 (pentest) 處理程序的概觀，以及如何執行 pentest 針對您在 Azure 基礎結構中執行的應用程式。"
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ms.assetid: 695d918c-a9ac-4eba-8692-af4526734ccc
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: yurid
ms.openlocfilehash: 202c239f46d8693ab7aa85e237235372e743e108
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="pen-testing"></a><span data-ttu-id="4023f-103">滲透測試</span><span class="sxs-lookup"><span data-stu-id="4023f-103">Pen Testing</span></span>
<span data-ttu-id="4023f-104">Hello 優點的應用程式測試和部署使用 Microsoft Azure 的其中一個是，您不需要 tooput 一起在內部部署基礎結構 toodevelop、 測試及部署您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4023f-104">One of hello great things about using Microsoft Azure for application testing and deployment is that you don’t need tooput together an on-premises infrastructure toodevelop, test and deploy your applications.</span></span> <span data-ttu-id="4023f-105">所有的 hello 基礎結構是由 hello Microsoft Azure 平台服務的處理。</span><span class="sxs-lookup"><span data-stu-id="4023f-105">All hello infrastructure is taken care of by hello Microsoft Azure platform services.</span></span> <span data-ttu-id="4023f-106">您不需要 tooworry 有關 requisitioning、 取得和"軌道和堆疊 」 在內部部署硬體。</span><span class="sxs-lookup"><span data-stu-id="4023f-106">You don’t have tooworry about requisitioning, acquiring, and “racking and stacking” your own on-premises hardware.</span></span>

<span data-ttu-id="4023f-107">這是很棒 –，但您仍須確定您執行一般的安全性 toomake 審慎。</span><span class="sxs-lookup"><span data-stu-id="4023f-107">This is great – but you still need toomake sure you perform your normal security due diligence.</span></span> <span data-ttu-id="4023f-108">其中一個，您需要的 hello 事情 toodo 是滲透測試 hello 應用程式在 Azure 中部署。</span><span class="sxs-lookup"><span data-stu-id="4023f-108">One of hello things you need toodo is penetration test hello applications you deploy in Azure.</span></span>

<span data-ttu-id="4023f-109">您可能已經知道 Microsoft 會執行 [我們的 Azure 環境的滲透測試](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e)。</span><span class="sxs-lookup"><span data-stu-id="4023f-109">You might already know that Microsoft performs [penetration testing of our Azure environment](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e).</span></span> <span data-ttu-id="4023f-110">這有助於改善我們的平台，並在改善安全性控制、推出新的安全性控制及改善我們的安全性程序方面引導我們的行動。</span><span class="sxs-lookup"><span data-stu-id="4023f-110">This helps us improve our platform and guides our actions in terms of improving security controls, introducing new security controls, and improving our security processes.</span></span>

<span data-ttu-id="4023f-111">我們不畫筆測試您的應用程式，但我們並了解，您會想要而且需要 tooperform 畫筆測試自己的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4023f-111">We don’t pen test your application for you, but we do understand that you will want and need tooperform pen testing on your own applications.</span></span> <span data-ttu-id="4023f-112">這是好的結果，，因為當您加強 hello 應用程式的安全性，協助讓 hello 整個 Azure 生態系統的更安全。</span><span class="sxs-lookup"><span data-stu-id="4023f-112">That’s a good thing, because when you enhance hello security of your applications, you help make hello entire Azure ecosystem more secure.</span></span>

<span data-ttu-id="4023f-113">當您畫筆測試您的應用程式時，看起來可能會攻擊 toous。</span><span class="sxs-lookup"><span data-stu-id="4023f-113">When you pen test your applications, it might look like an attack toous.</span></span> <span data-ttu-id="4023f-114">我們會 [持續監視](http://blogs.msdn.com/b/azuresecurity/archive/2015/07/05/best-practices-to-protect-your-azure-deployment-against-cloud-drive-by-attacks.aspx) 攻擊模式，並且在需要時會起始事件回應程序。</span><span class="sxs-lookup"><span data-stu-id="4023f-114">We [continuously monitor](http://blogs.msdn.com/b/azuresecurity/archive/2015/07/05/best-practices-to-protect-your-azure-deployment-against-cloud-drive-by-attacks.aspx) for attack patterns and will initiate an incident response process if we need to.</span></span> <span data-ttu-id="4023f-115">它無法協助您，這樣不會有幫助我們我們觸發事件的回應到期 tooyour 自己到期勤加注意畫筆測試。</span><span class="sxs-lookup"><span data-stu-id="4023f-115">It doesn’t help you and it doesn’t help us if we trigger an incident response due tooyour own due diligence pen testing.</span></span>

<span data-ttu-id="4023f-116">哪些 toodo？</span><span class="sxs-lookup"><span data-stu-id="4023f-116">What toodo?</span></span>

<span data-ttu-id="4023f-117">當您準備好 toopen 測試 Azure 託管應用程式，您可以選擇太[讓我們知道](https://portal.msrc.microsoft.com/en-us/engage/pentest)。</span><span class="sxs-lookup"><span data-stu-id="4023f-117">When you’re ready toopen test your Azure-hosted applications, you have an option too[let us know](https://portal.msrc.microsoft.com/en-us/engage/pentest).</span></span> <span data-ttu-id="4023f-118">我們知道您要執行特定測試的 toobe，我們將不會不小心關閉，您 （例如封鎖您要從測試的 hello IP 位址），只要您的測試符合 toohello Azure 畫筆測試的條款和條件中所述[Microsoft 雲端整合滲透測試往來的規則](https://technet.microsoft.com/en-us/mt784683)。</span><span class="sxs-lookup"><span data-stu-id="4023f-118">Once we know that you’re going toobe performing specific tests, we won’t inadvertently shut you down (such as blocking hello IP address that you’re testing from), as long as your tests conform toohello Azure pen testing terms and conditions described in [Microsoft Cloud Unified Penetration Testing Rules of Engagement](https://technet.microsoft.com/en-us/mt784683).</span></span>
<span data-ttu-id="4023f-119">您可以執行的標準測試包括：</span><span class="sxs-lookup"><span data-stu-id="4023f-119">Standard tests you can perform include:</span></span>

* <span data-ttu-id="4023f-120">測試您的端點 toouncover hello[開啟 Web 應用程式安全性專案 (OWASP) 的前 10 個弱點](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)</span><span class="sxs-lookup"><span data-stu-id="4023f-120">Tests on your endpoints toouncover hello [Open Web Application Security Project (OWASP) top 10 vulnerabilities](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)</span></span>
* <span data-ttu-id="4023f-121">[模糊測試](https://blogs.microsoft.com/cybertrust/2007/09/20/fuzz-testing-at-microsoft-and-the-triage-process/) </span><span class="sxs-lookup"><span data-stu-id="4023f-121">[Fuzz testing](https://blogs.microsoft.com/cybertrust/2007/09/20/fuzz-testing-at-microsoft-and-the-triage-process/) of your endpoints</span></span>
* <span data-ttu-id="4023f-122">[連接埠掃描](https://en.wikipedia.org/wiki/Port_scanner) </span><span class="sxs-lookup"><span data-stu-id="4023f-122">[Port scanning](https://en.wikipedia.org/wiki/Port_scanner) of your endpoints</span></span>

<span data-ttu-id="4023f-123">您不能執行的一種測試是任何種類的 [拒絕服務 (DoS)](https://en.wikipedia.org/wiki/Denial-of-service_attack) 攻擊。</span><span class="sxs-lookup"><span data-stu-id="4023f-123">One type of test that you can’t perform is any kind of [Denial of Service (DoS)](https://en.wikipedia.org/wiki/Denial-of-service_attack) attack.</span></span> <span data-ttu-id="4023f-124">這包括起始 DoS 攻擊本身，或是執行可能會決定、示範或模擬任何類型的 DoS 攻擊的相關測試。</span><span class="sxs-lookup"><span data-stu-id="4023f-124">This includes initiating a DoS attack itself, or performing related tests that might determine, demonstrate or simulate any type of DoS attack.</span></span>

<span data-ttu-id="4023f-125">正在準備 tooget 入門畫筆測試 Microsoft Azure 中裝載之應用程式嗎？</span><span class="sxs-lookup"><span data-stu-id="4023f-125">Are you ready tooget started with pen testing your applications hosted in Microsoft Azure?</span></span> <span data-ttu-id="4023f-126">如果是，則透過 toohello 前端上[滲透測試概觀](https://technet.microsoft.com/library/mt784683.aspx)頁面 （和按一下 hello 建立在 hello hello 頁面底部的 [測試要求] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="4023f-126">If so, then head on over toohello [Penetration Test Overview](https://technet.microsoft.com/library/mt784683.aspx) page (and click hello Create a Testing Request button at hello bottom of hello page.</span></span> <span data-ttu-id="4023f-127">您也可以找到測試條款及條件與有用的連結上如何報告安全性缺陷相關的 tooAzure 或任何其他 Microsoft 服務的 hello 畫筆上的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="4023f-127">You’ll also find more information on hello pen testing terms and conditions and helpful links on how you can report security flaws related tooAzure or any other Microsoft service.</span></span>
