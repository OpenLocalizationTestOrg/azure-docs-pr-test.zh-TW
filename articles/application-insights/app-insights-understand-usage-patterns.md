---
title: "aaaAzure 應用程式 Insights 漏斗圖"
description: "了解如何使用漏斗圖 toodiscover 客戶如何與您的應用程式互動。"
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
ms.openlocfilehash: 3a90cfd11cb193e303136504df44008ffd04a290
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="discover-how-customers-are-using-your-application-with-hello-application-insights-funnels"></a><span data-ttu-id="ccd17-103">探索客戶如何使用您的應用程式以 hello 應用程式 Insights 漏斗圖</span><span class="sxs-lookup"><span data-stu-id="ccd17-103">Discover how customers are using your application with hello Application Insights Funnels</span></span>

<span data-ttu-id="ccd17-104">Hello 責 tooyour 商務是了解客戶經驗。</span><span class="sxs-lookup"><span data-stu-id="ccd17-104">Understanding customer experience is of hello utmost importance tooyour business.</span></span> <span data-ttu-id="ccd17-105">如果您的應用程式牽涉到多個階段，您需要 tooknow 如果大多數客戶所進行 hello 整個程序，或如果它們結束 hello 處理程序，在某個時間點。</span><span class="sxs-lookup"><span data-stu-id="ccd17-105">If your application involves multiple stages, you will need tooknow if most customers are progressing through hello entire process, or if they are ending hello process at some point.</span></span> <span data-ttu-id="ccd17-106">hello 依序經歷一系列的 web 應用程式中的步驟就是所謂 「 漏斗圖 」。</span><span class="sxs-lookup"><span data-stu-id="ccd17-106">hello progression through a series of steps in a web application is known as a "funnel".</span></span> <span data-ttu-id="ccd17-107">您可以使用 hello 應用程式 Insights 漏斗圖 toogain 深入了解您的使用者和監視逐步轉換比率。</span><span class="sxs-lookup"><span data-stu-id="ccd17-107">You can use hello Application Insights Funnels toogain insights into your users and monitor step-by-step conversion rates.</span></span> 

## <a name="get-started-with-hello-funnels-blade"></a><span data-ttu-id="ccd17-108">Hello 漏斗圖刀鋒視窗快速入門</span><span class="sxs-lookup"><span data-stu-id="ccd17-108">Get started with hello Funnels blade</span></span>
<span data-ttu-id="ccd17-109">hello 最簡單方式 toolearn 有關漏斗圖是 toowalk，雖然範例。</span><span class="sxs-lookup"><span data-stu-id="ccd17-109">hello easiest way toolearn about Funnels is toowalk though an example.</span></span> <span data-ttu-id="ccd17-110">hello 圖示範 hello 步驟的擁有者的電子商務的企業需要的 toolearn 他們的客戶與 web 應用程式之間的互動方式。</span><span class="sxs-lookup"><span data-stu-id="ccd17-110">hello following illustrations demonstrate hello steps owners of an e-commerce business would take toolearn how their customers interact with their web application.</span></span>  

### <a name="create-your-funnel"></a><span data-ttu-id="ccd17-111">建立您的漏斗圖</span><span class="sxs-lookup"><span data-stu-id="ccd17-111">Create your funnel</span></span>
<span data-ttu-id="ccd17-112">建立您的漏斗圖之前，您需要 toodecide 想 tooanswer hello 問題。</span><span class="sxs-lookup"><span data-stu-id="ccd17-112">Before you create your funnel, you need toodecide on hello question you want tooanswer.</span></span> <span data-ttu-id="ccd17-113">例如，您可能會希望 tooknow 公告上檢視您的首頁上按一下多少客戶。</span><span class="sxs-lookup"><span data-stu-id="ccd17-113">For example, you might want tooknow how many customers viewing your home page click on an advertisement.</span></span> <span data-ttu-id="ccd17-114">在此範例中，hello hello Fabrikam Fiber 公司擁有者想 tooknow hello 百分比進行加入 hello 上個月期間購物車的項目 tootheir 之後購買的客戶。</span><span class="sxs-lookup"><span data-stu-id="ccd17-114">In this example, hello owners of hello Fabrikam Fiber company want tooknow hello percentage of customers who make a purchase after adding items tootheir shopping cart during hello last month.</span></span>

<span data-ttu-id="ccd17-115">以下是他們採取 toocreate 他們漏斗圖的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="ccd17-115">Here are hello steps they take toocreate their funnel.</span></span>

1. <span data-ttu-id="ccd17-116">按一下 hello hello 漏斗圖刀鋒視窗上的新增 按鈕。</span><span class="sxs-lookup"><span data-stu-id="ccd17-116">Click hello New button on hello Funnels blade.</span></span>
1. <span data-ttu-id="ccd17-117">選取 「 上個月"hello 時間範圍從 hello**時間範圍**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="ccd17-117">Select hello time range of "Last month" from hello **Time Range** drop-down.</span></span> 
1. <span data-ttu-id="ccd17-118">選取 hello**產品頁面**事件從 hello**步驟 1**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="ccd17-118">Select hello **Product page** event from hello **Step 1** drop-down list.</span></span> 
1. <span data-ttu-id="ccd17-119">選取 hello**新增 tooshopping 車**事件從 hello**步驟 2**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="ccd17-119">Select hello **Add tooshopping cart** event from hello **Step 2** drop-down list.</span></span>
1. <span data-ttu-id="ccd17-120">選取 hello**按一下購買**事件從 hello**步驟 3**下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="ccd17-120">Select hello **Click purchase** event from hello **Step 3** drop-down list.</span></span>
1. <span data-ttu-id="ccd17-121">新增名稱 toohello 漏斗圖，然後按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="ccd17-121">Add a name toohello funnel and click **Save**.</span></span>

<span data-ttu-id="ccd17-122">hello 如下圖所示範 hello 資料 hello 漏斗圖刀鋒視窗會產生。</span><span class="sxs-lookup"><span data-stu-id="ccd17-122">hello following illustration demonstrates hello data hello Funnels blade generates.</span></span> <span data-ttu-id="ccd17-123">從這裡 hello Fabrikam 擁有者可以看到在 hello 過去一週，22.7%的客戶加入項目 tootheir 購物車已完成的 hello 購買。</span><span class="sxs-lookup"><span data-stu-id="ccd17-123">From here hello Fabrikam owners can see that during hello last week, 22.7% of their customers who added an item tootheir shopping cart completed hello purchase.</span></span> <span data-ttu-id="ccd17-124">它們也可以查看之前造訪 hello 產品網頁和 20%的客戶完成採購後已登出 1%的 hello 客戶按下公告。</span><span class="sxs-lookup"><span data-stu-id="ccd17-124">They can also see that 1% of hello customers clicked an advertisement before visiting hello product page, and 20% of their customers signed out after completing their purchase.</span></span>


![含有資料的 [漏斗圖] 刀鋒視窗](./media/app-insights-understand-usage-patterns/funnel1.png)

## <a name="next-steps"></a><span data-ttu-id="ccd17-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ccd17-126">Next steps</span></span>
- <span data-ttu-id="ccd17-127">深入了解[使用方式分析](app-insights-usage-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="ccd17-127">Learn more about [usage analysis](app-insights-usage-overview.md).</span></span> 
