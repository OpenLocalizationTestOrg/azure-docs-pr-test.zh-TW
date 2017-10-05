---
title: "何謂 Microsoft Power BI Embedded？"
description: "Power BI Embedded 可讓您將 Power BI 報告整合到 Web 或行動應用程式中，您就不需要建置自訂解決方案。"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 03649b72-b7d7-40ca-b077-12356d72d4f3
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/20/2017
ms.author: asaxton
ms.openlocfilehash: 0b5f7a2c3fd16ac32b0bc382616ca6600d378bb8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-microsoft-power-bi-embedded"></a><span data-ttu-id="23d4e-103">何謂 Microsoft Power BI Embedded？</span><span class="sxs-lookup"><span data-stu-id="23d4e-103">What is Microsoft Power BI Embedded?</span></span>
<span data-ttu-id="23d4e-104">運用 **Power BI Embedded**，您可以將 Power BI 報告整合至您的 Web 應用程式或行動應用程式。</span><span class="sxs-lookup"><span data-stu-id="23d4e-104">With **Power BI Embedded**, you can integrate Power BI reports right into your web or mobile applications.</span></span>

![](media/powerbi-embedded-whats-is/what-is.png)

<span data-ttu-id="23d4e-105">Power BI Embedded 是一個 **Azure 服務** ，可讓 ISV 和應用程式開發人員在其應用程式中呈現 Power BI 資料體驗。</span><span class="sxs-lookup"><span data-stu-id="23d4e-105">Power BI Embedded is an **Azure service** that enables ISVs and app developers to surface Power BI data experiences within their applications.</span></span> <span data-ttu-id="23d4e-106">身為開發人員，您已建置應用程式，這些應用程式有它們自己的使用者和個別的功能集。</span><span class="sxs-lookup"><span data-stu-id="23d4e-106">As a developer, you've built applications, and those applications have their own users and distinct set of features.</span></span> <span data-ttu-id="23d4e-107">這些應用程式也可能已經內建一些資料元素，例如現在可以由 Microsoft Power BI Embedded 提供的圖表和報表。</span><span class="sxs-lookup"><span data-stu-id="23d4e-107">Those apps may also happen to have some built-in data elements like charts and reports that can now be powered by Microsoft Power BI Embedded.</span></span> <span data-ttu-id="23d4e-108">您不需要 Power BI 帳戶就可以使用您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="23d4e-108">You don’t need a Power BI account to use your app.</span></span> <span data-ttu-id="23d4e-109">您可以像以前一樣繼續登入您的應用程式，以及在不需要任何額外授權的情況下，檢視 Power BI 記錄體驗並與它們互動。</span><span class="sxs-lookup"><span data-stu-id="23d4e-109">You can continue to sign in to your application just like before, and view and interact with the Power BI reporting experience without requiring any additional licensing.</span></span>

## <a name="licensing-for-microsoft-power-bi-embedded"></a><span data-ttu-id="23d4e-110">Microsoft Power BI Embedded 授權</span><span class="sxs-lookup"><span data-stu-id="23d4e-110">Licensing for Microsoft Power BI Embedded</span></span>
<span data-ttu-id="23d4e-111">在 **Microsoft Power BI Embedded** 使用模型中，Power BI 的授權並不是使用者的責任。</span><span class="sxs-lookup"><span data-stu-id="23d4e-111">In the **Microsoft Power BI Embedded** usage model, licensing for Power BI is not the responsibility of the end-user.</span></span>  <span data-ttu-id="23d4e-112">而是由使用視覺效果之應用程式的開發人員購買**工作階段**，並向擁有那些資源的訂用帳戶收費。</span><span class="sxs-lookup"><span data-stu-id="23d4e-112">Instead, **sessions** are purchased by the developer of the app that is consuming the visuals, and are charged to the subscription that owns those resources.</span></span> <span data-ttu-id="23d4e-113">在[價格](https://azure.microsoft.com/en-us/pricing/details/power-bi-embedded/)頁面上可以找到其他資訊。</span><span class="sxs-lookup"><span data-stu-id="23d4e-113">Additional information can be found on the [pricing page](https://azure.microsoft.com/en-us/pricing/details/power-bi-embedded/).</span></span>

## <a name="microsoft-power-bi-embedded-conceptual-model"></a><span data-ttu-id="23d4e-114">Microsoft Power BI Embedded 概念模型</span><span class="sxs-lookup"><span data-stu-id="23d4e-114">Microsoft Power BI Embedded conceptual model</span></span>

![](media/powerbi-embedded-whats-is/model.png)

<span data-ttu-id="23d4e-115">就像 Azure 中的任何其他服務一樣，Power BI Embedded 的資源也是透過 [Azure Resource Manager API](https://msdn.microsoft.com/library/mt712306.aspx) 佈建。</span><span class="sxs-lookup"><span data-stu-id="23d4e-115">Like any other service in Azure, resources for Power BI Embedded are provisioned through the [Azure Resource Manager APIs](https://msdn.microsoft.com/library/mt712306.aspx).</span></span> <span data-ttu-id="23d4e-116">在此情況下，您佈建的資源是 **Power BI 工作區集合**。</span><span class="sxs-lookup"><span data-stu-id="23d4e-116">In this case, the resource that you provision is a **Power BI Workspace Collection**.</span></span>

## <a name="workspace-collection"></a><span data-ttu-id="23d4e-117">工作區集合</span><span class="sxs-lookup"><span data-stu-id="23d4e-117">Workspace collection</span></span>
<span data-ttu-id="23d4e-118">**工作區集合**是包含 0 個或更多**工作區**之資源的最上層 Azure 容器。</span><span class="sxs-lookup"><span data-stu-id="23d4e-118">A **Workspace Collection** is the top-level Azure container for resources that contains 0 or more **Workspaces**.</span></span>  <span data-ttu-id="23d4e-119">**工作區****集合**擁有所有標準 Azure 屬性，以及下列項目：</span><span class="sxs-lookup"><span data-stu-id="23d4e-119">A **Workspace** **Collection** has all of the standard Azure properties, as well as the following:</span></span>

* <span data-ttu-id="23d4e-120">**存取金鑰** – 安全呼叫 Power BI API 時使用的金鑰 (會在稍後的小節中說明)。</span><span class="sxs-lookup"><span data-stu-id="23d4e-120">**Access Keys** – Keys used when securely calling the Power BI APIs (described in a later section).</span></span>
* <span data-ttu-id="23d4e-121">**使用者** – 具有管理權現，可透過 Azure 入口網站或 Azure Resource Manager API 管理 Power BI 工作區集合的 Azure Active Directory (AAD) 使用者。</span><span class="sxs-lookup"><span data-stu-id="23d4e-121">**Users** – Azure Active Directory (AAD) users that have administrator rights to manage the Power BI Workspace Collection through the Azure portal or Azure Resource Manager API.</span></span>
* <span data-ttu-id="23d4e-122">**區域** – 佈建**工作區集合**時，您可以選取要佈建的區域。</span><span class="sxs-lookup"><span data-stu-id="23d4e-122">**Region** – As part of provisioning a **Workspace Collection**, you can select a region to be provisioned in.</span></span> <span data-ttu-id="23d4e-123">如需詳細資訊，請參閱 [Azure 地區](https://azure.microsoft.com/regions/)。</span><span class="sxs-lookup"><span data-stu-id="23d4e-123">For more information, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span>

## <a name="workspace"></a><span data-ttu-id="23d4e-124">工作區</span><span class="sxs-lookup"><span data-stu-id="23d4e-124">Workspace</span></span>
<span data-ttu-id="23d4e-125">**工作區**是 Power BI 內容的容器，可包括資料集和報告。</span><span class="sxs-lookup"><span data-stu-id="23d4e-125">A **Workspace** is a container of Power BI content, which can include datasets and reports.</span></span> <span data-ttu-id="23d4e-126">**工作區** 在第一次建立時是空白的。</span><span class="sxs-lookup"><span data-stu-id="23d4e-126">A **Workspace** is empty when first created.</span></span> <span data-ttu-id="23d4e-127">您將會使用 Power BI Desktop 編寫內容，且您會使用 [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx) 將 PBIX 自動部署至您的工作區中。</span><span class="sxs-lookup"><span data-stu-id="23d4e-127">You’ll author content using Power BI Desktop and you'll programmatically deploy the PBIX into your workspace using the [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx).</span></span> <span data-ttu-id="23d4e-128">您也可以透過程式設計方式建立資料集，然後在應用程式內建立報告，而不是使用 Power BI Desktop 來建立。</span><span class="sxs-lookup"><span data-stu-id="23d4e-128">You can also programmatically create your dataset and then create reports within your application instead of using Power BI Desktop.</span></span>

## <a name="using-workspace-collections-and-workspaces"></a><span data-ttu-id="23d4e-129">使用工作區集合和工作區</span><span class="sxs-lookup"><span data-stu-id="23d4e-129">Using workspace collections and workspaces</span></span>
<span data-ttu-id="23d4e-130">**工作區集合**與**工作區**是內容的容器，您可以針對您正在建立之應用程式的設計，採用任何最佳方式來使用及組織內容。</span><span class="sxs-lookup"><span data-stu-id="23d4e-130">**Workspace Collections** and **Workspaces** are containers of content that are used and organized in whichever way best fits the design of the application you are building.</span></span> <span data-ttu-id="23d4e-131">將會有許多不同的方式可供您管理它們內部的內容。</span><span class="sxs-lookup"><span data-stu-id="23d4e-131">There will be many different ways that you could arrange the content within them.</span></span> <span data-ttu-id="23d4e-132">您可以選擇將所有內容放在某一個工作區內，然後之後再使用應用程式權杖進一步在您的客戶之間細分內容。</span><span class="sxs-lookup"><span data-stu-id="23d4e-132">You may choose to put all content within one workspace and then later use app tokens to further subdivide the content amongst your customers.</span></span> <span data-ttu-id="23d4e-133">您也可以選擇將所有客戶放在個別工作區中，這樣一來他們之間就會有一些區隔。</span><span class="sxs-lookup"><span data-stu-id="23d4e-133">You may also choose to put all of your customers in separate workspaces so that there is some separation between them.</span></span> <span data-ttu-id="23d4e-134">或者，您可選擇依據地區 (而非依據客戶) 來組織使用者。</span><span class="sxs-lookup"><span data-stu-id="23d4e-134">Or, you may choose to organize users by region rather than by customer.</span></span> <span data-ttu-id="23d4e-135">這個彈性設計可讓您選擇最佳的內容組織方式。</span><span class="sxs-lookup"><span data-stu-id="23d4e-135">This flexible design allows you to choose the best way to organize content.</span></span>

## <a name="cached-datasets"></a><span data-ttu-id="23d4e-136">快取的資料集</span><span class="sxs-lookup"><span data-stu-id="23d4e-136">Cached datasets</span></span>
<span data-ttu-id="23d4e-137">您可以使用快取的資料集。</span><span class="sxs-lookup"><span data-stu-id="23d4e-137">Cached datasets can be used.</span></span>  <span data-ttu-id="23d4e-138">但是，在資料已載入 **Microsoft Power BI Embedded** 之後，您無法重新整理快取的資料。</span><span class="sxs-lookup"><span data-stu-id="23d4e-138">However, you cannot refresh cached data once it has been loaded into **Microsoft Power BI Embedded**.</span></span> <span data-ttu-id="23d4e-139">快取的資料集表示您已將資料匯入 Power BI Desktop，而不是使用 DirectQuery。</span><span class="sxs-lookup"><span data-stu-id="23d4e-139">A cached dataset means you have imported the data into Power BI Desktop instead of using DirectQuery.</span></span>

## <a name="authentication-and-authorization-with-app-tokens"></a><span data-ttu-id="23d4e-140">應用程式權杖中的驗證與授權</span><span class="sxs-lookup"><span data-stu-id="23d4e-140">Authentication and authorization with app tokens</span></span>
<span data-ttu-id="23d4e-141">**Microsoft Power BI Embedded** 會延遲到您的應用程式執行所有必要的使用者驗證和授權。</span><span class="sxs-lookup"><span data-stu-id="23d4e-141">**Microsoft Power BI Embedded** defers to your application to perform all the necessary user authentication and authorization.</span></span> <span data-ttu-id="23d4e-142">並沒有明確要求您的使用者必須是 Azure Active Directory (Azure AD) 的客戶。</span><span class="sxs-lookup"><span data-stu-id="23d4e-142">There is no explicit requirement that your end users be customers of Azure Active Directory (Azure AD).</span></span>  <span data-ttu-id="23d4e-143">您的應用程式會透過使用「應用程式驗證權杖」(應用程式權杖)，將轉譯 Power BI 報表的授權出示給 **Microsoft Power BI Embedded**。</span><span class="sxs-lookup"><span data-stu-id="23d4e-143">Instead, your application expresses to **Microsoft Power BI Embedded** authorization to render a Power BI report by using **Application Authentication Tokens (App Tokens)**.</span></span>  <span data-ttu-id="23d4e-144">這些 **應用程式權杖** 會在您的應用程式想要轉譯報表時視需要建立。</span><span class="sxs-lookup"><span data-stu-id="23d4e-144">These **App Tokens** are created as needed when your app wants to render a report.</span></span>

![](media/powerbi-embedded-whats-is/app-tokens.png)

<span data-ttu-id="23d4e-145">應用程式驗證權杖 (應用程式權杖) 是用來針對 **Microsoft Power BI Embedded** 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="23d4e-145">**Application Authentication Tokens (App Tokens)** are used to authenticate against **Microsoft Power BI Embedded**.</span></span>  <span data-ttu-id="23d4e-146">應用程式權杖 有三種類型：</span><span class="sxs-lookup"><span data-stu-id="23d4e-146">There are three types of **App Tokens**:</span></span>

1. <span data-ttu-id="23d4e-147">佈建權杖 - 將新的「工作區」佈建到「工作區集合」時使用</span><span class="sxs-lookup"><span data-stu-id="23d4e-147">Provisioning Tokens - Used when provisioning a new **Workspace** into a **Workspace Collection**</span></span>
2. <span data-ttu-id="23d4e-148">開發權杖 - 在直接呼叫 **Power BI REST API**</span><span class="sxs-lookup"><span data-stu-id="23d4e-148">Development Tokens - Used when making calls directly to the **Power BI REST APIs**</span></span>
3. <span data-ttu-id="23d4e-149">內嵌權杖 - 在進行呼叫以在內嵌的 iframe 中轉譯報表時使用</span><span class="sxs-lookup"><span data-stu-id="23d4e-149">Embedding Tokens - Used when making calls to render a report in the embedded iframe</span></span>

<span data-ttu-id="23d4e-150">這些權杖會在您和 **Microsoft Power BI Embedded**互動時的各種不同階段使用。</span><span class="sxs-lookup"><span data-stu-id="23d4e-150">These tokens are used for the various phases of your interactions with **Microsoft Power BI Embedded**.</span></span>  <span data-ttu-id="23d4e-151">設計權杖的目的是為了讓您從您的應用程式委派權限給 Power BI。</span><span class="sxs-lookup"><span data-stu-id="23d4e-151">The tokens are designed so that you can delegate permissions from your app to Power BI.</span></span> <span data-ttu-id="23d4e-152">如需詳細資訊，請參閱 [應用程式權杖流程](power-bi-embedded-app-token-flow.md)。</span><span class="sxs-lookup"><span data-stu-id="23d4e-152">For more information, see [App Token Flow](power-bi-embedded-app-token-flow.md).</span></span>

## <a name="create-or-edit-reports-within-your-application"></a><span data-ttu-id="23d4e-153">在應用程式內建立或編輯報告</span><span class="sxs-lookup"><span data-stu-id="23d4e-153">Create or edit reports within your application</span></span>

<span data-ttu-id="23d4e-154">您現在可以直接在應用程式中編輯現有報告或建立新報告，而不必使用 Power BI Desktop。</span><span class="sxs-lookup"><span data-stu-id="23d4e-154">You can now edit exist reports or create new reports directly in your application without having to use Power BI Desktop.</span></span> <span data-ttu-id="23d4e-155">這需要工作區內已存在資料集。</span><span class="sxs-lookup"><span data-stu-id="23d4e-155">This requires that a dataset exist within your workspace.</span></span>

## <a name="see-also"></a><span data-ttu-id="23d4e-156">另請參閱</span><span class="sxs-lookup"><span data-stu-id="23d4e-156">See also</span></span>

[<span data-ttu-id="23d4e-157">Microsoft Power BI Embedded 常見案例</span><span class="sxs-lookup"><span data-stu-id="23d4e-157">Common Microsoft Power BI Embedded scenarios</span></span>](power-bi-embedded-scenarios.md)  
[<span data-ttu-id="23d4e-158">開始使用 Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="23d4e-158">Get started with Microsoft Power BI Embedded</span></span>](power-bi-embedded-get-started.md)  
[<span data-ttu-id="23d4e-159">開始使用範例</span><span class="sxs-lookup"><span data-stu-id="23d4e-159">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="23d4e-160">內嵌報告</span><span class="sxs-lookup"><span data-stu-id="23d4e-160">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
[<span data-ttu-id="23d4e-161">在 Power BI Embedded 中驗證和授權</span><span class="sxs-lookup"><span data-stu-id="23d4e-161">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="23d4e-162">JavaScript 內嵌範例</span><span class="sxs-lookup"><span data-stu-id="23d4e-162">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
[<span data-ttu-id="23d4e-163">PowerBI-CSharp Git 存放庫</span><span class="sxs-lookup"><span data-stu-id="23d4e-163">PowerBI-CSharp Git Repo</span></span>](https://github.com/Microsoft/PowerBI-CSharp)  
[<span data-ttu-id="23d4e-164">PowerBI-Node Git存放庫</span><span class="sxs-lookup"><span data-stu-id="23d4e-164">PowerBI-Node Git Repo</span></span>](https://github.com/Microsoft/PowerBI-Node)  
<span data-ttu-id="23d4e-165">有其他疑問？</span><span class="sxs-lookup"><span data-stu-id="23d4e-165">More questions?</span></span> [<span data-ttu-id="23d4e-166">試用 Power BI 社群</span><span class="sxs-lookup"><span data-stu-id="23d4e-166">Try the Power BI Community</span></span>](http://community.powerbi.com/)
