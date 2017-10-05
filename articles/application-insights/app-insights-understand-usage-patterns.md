---
title: "Azure Application Insights 漏斗圖"
description: "了解如何使用漏斗圖來探索客戶與您的應用程式互動的方式。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: cfreeman
ms.openlocfilehash: 85f47daaaff8967eb83c330bab839023f128b486
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="discover-how-customers-are-using-your-application-with-the-application-insights-funnels"></a><span data-ttu-id="6c421-103">使用 Application Insights 漏斗圖來探索客戶如何使用您的應用程式</span><span class="sxs-lookup"><span data-stu-id="6c421-103">Discover how customers are using your application with the Application Insights Funnels</span></span>

<span data-ttu-id="6c421-104">了解客戶體驗對於您的企業非常重要。</span><span class="sxs-lookup"><span data-stu-id="6c421-104">Understanding customer experience is of the utmost importance to your business.</span></span> <span data-ttu-id="6c421-105">如果您的應用程式牽涉到多個階段，您必須了解大部分客戶是否進行了整個流程，或是在某個時間點結束流程。</span><span class="sxs-lookup"><span data-stu-id="6c421-105">If your application involves multiple stages, you will need to know if most customers are progressing through the entire process, or if they are ending the process at some point.</span></span> <span data-ttu-id="6c421-106">在 Web 應用程式中通過一系列步驟的過程便稱為「漏斗圖」。</span><span class="sxs-lookup"><span data-stu-id="6c421-106">The progression through a series of steps in a web application is known as a "funnel".</span></span> <span data-ttu-id="6c421-107">您可以使用 Application Insights 漏斗圖來深入了解使用者，並監視各步驟的轉換率。</span><span class="sxs-lookup"><span data-stu-id="6c421-107">You can use the Application Insights Funnels to gain insights into your users and monitor step-by-step conversion rates.</span></span> 

## <a name="get-started-with-the-funnels-blade"></a><span data-ttu-id="6c421-108">開始使用 [漏斗圖] 刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="6c421-108">Get started with the Funnels blade</span></span>
<span data-ttu-id="6c421-109">了解漏斗圖最簡單的方法是透過範例逐步執行。</span><span class="sxs-lookup"><span data-stu-id="6c421-109">The easiest way to learn about Funnels is to walk though an example.</span></span> <span data-ttu-id="6c421-110">下圖示範電子商務企業的擁有者會採取的步驟，以了解其客戶如何與 Web 應用程式互動。</span><span class="sxs-lookup"><span data-stu-id="6c421-110">The following illustrations demonstrate the steps owners of an e-commerce business would take to learn how their customers interact with their web application.</span></span>  

### <a name="create-your-funnel"></a><span data-ttu-id="6c421-111">建立您的漏斗圖</span><span class="sxs-lookup"><span data-stu-id="6c421-111">Create your funnel</span></span>
<span data-ttu-id="6c421-112">建立您的漏斗圖之前，您需要決定要獲得回答的問題。</span><span class="sxs-lookup"><span data-stu-id="6c421-112">Before you create your funnel, you need to decide on the question you want to answer.</span></span> <span data-ttu-id="6c421-113">例如，您可能想知道有多少檢視首頁的客戶在廣告上按一下。</span><span class="sxs-lookup"><span data-stu-id="6c421-113">For example, you might want to know how many customers viewing your home page click on an advertisement.</span></span> <span data-ttu-id="6c421-114">在此範例中，Fabrikam Fiber 公司的擁有者想知道上個月中，客戶將項目加入購物車後進行購買的百分比為何。</span><span class="sxs-lookup"><span data-stu-id="6c421-114">In this example, the owners of the Fabrikam Fiber company want to know the percentage of customers who make a purchase after adding items to their shopping cart during the last month.</span></span>

<span data-ttu-id="6c421-115">以下是他們用來建立漏斗圖所採取的步驟。</span><span class="sxs-lookup"><span data-stu-id="6c421-115">Here are the steps they take to create their funnel.</span></span>

1. <span data-ttu-id="6c421-116">按一下 [漏斗圖] 刀鋒視窗上的 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="6c421-116">Click the New button on the Funnels blade.</span></span>
1. <span data-ttu-id="6c421-117">在 [時間範圍] 下拉式清單中，選取 [上個月] 作為時間範圍。</span><span class="sxs-lookup"><span data-stu-id="6c421-117">Select the time range of "Last month" from the **Time Range** drop-down.</span></span> 
1. <span data-ttu-id="6c421-118">從 [步驟 1] 下拉式清單選取 [產品頁面] 活動。</span><span class="sxs-lookup"><span data-stu-id="6c421-118">Select the **Product page** event from the **Step 1** drop-down list.</span></span> 
1. <span data-ttu-id="6c421-119">從 [步驟 2] 下拉式清單選取 [加入至購物車] 活動。</span><span class="sxs-lookup"><span data-stu-id="6c421-119">Select the **Add to shopping cart** event from the **Step 2** drop-down list.</span></span>
1. <span data-ttu-id="6c421-120">從 [步驟 3] 下拉式清單選取 [按一下購買] 活動。</span><span class="sxs-lookup"><span data-stu-id="6c421-120">Select the **Click purchase** event from the **Step 3** drop-down list.</span></span>
1. <span data-ttu-id="6c421-121">新增漏斗圖的名稱，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="6c421-121">Add a name to the funnel and click **Save**.</span></span>

<span data-ttu-id="6c421-122">下圖示範 [漏斗圖] 刀鋒視窗產生的資料。</span><span class="sxs-lookup"><span data-stu-id="6c421-122">The following illustration demonstrates the data the Funnels blade generates.</span></span> <span data-ttu-id="6c421-123">在這裡，Fabrikam 的擁有者可看到上星期中，將項目加入購物車的客戶有 22.7% 完成了購買。</span><span class="sxs-lookup"><span data-stu-id="6c421-123">From here the Fabrikam owners can see that during the last week, 22.7% of their customers who added an item to their shopping cart completed the purchase.</span></span> <span data-ttu-id="6c421-124">他們也會看到有 1% 的客戶在瀏覽產品頁面之前按了一下廣告，而 20% 的客戶在完成購買之後就登出。</span><span class="sxs-lookup"><span data-stu-id="6c421-124">They can also see that 1% of the customers clicked an advertisement before visiting the product page, and 20% of their customers signed out after completing their purchase.</span></span>


![含有資料的 [漏斗圖] 刀鋒視窗](./media/app-insights-understand-usage-patterns/funnel1.png)

## <a name="next-steps"></a><span data-ttu-id="6c421-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6c421-126">Next steps</span></span>
- <span data-ttu-id="6c421-127">深入了解[使用方式分析](app-insights-usage-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6c421-127">Learn more about [usage analysis](app-insights-usage-overview.md).</span></span> 
