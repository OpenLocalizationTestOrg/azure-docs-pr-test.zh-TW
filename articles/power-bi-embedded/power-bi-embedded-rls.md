---
title: "資料列層級安全性與 Power BI Embedded"
description: "資料列層級安全性與 Power BI Embedded 的詳細資料"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 7936ade5-2c75-435b-8314-ea7ca815867a
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 1cde5b9ee4c716af07d427d4d0eb3f0775d456ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a><span data-ttu-id="b2fb5-103">Power BI Embedded 的資料列層級安全性</span><span class="sxs-lookup"><span data-stu-id="b2fb5-103">Row level security with Power BI Embedded</span></span>

<span data-ttu-id="b2fb5-104">資料列層級安全性 (RLS) 可以用來限制使用者對於報告或資料集內特定資料的存取，讓多個不同使用者在查看不同資料的同時，能夠使用相同的報告。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-104">Row level security (RLS) can be used to restrict user access to particular data within a report or dataset, allowing for multiple different users to use the same report while all seeing different data.</span></span> <span data-ttu-id="b2fb5-105">Power BI Embedded 現在支援使用 RLS 設定資料集。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-105">Power BI Embedded now supports datasets configured with RLS.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

<span data-ttu-id="b2fb5-106">為了利用 RLS，了解三個主要概念很重要：使用者、角色和規則。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-106">In order to take advantage of RLS, it’s important you understand three main concepts; Users, Roles, and Rules.</span></span> <span data-ttu-id="b2fb5-107">讓我們仔細看看每個概念：</span><span class="sxs-lookup"><span data-stu-id="b2fb5-107">Let’s take a closer look at each:</span></span>

<span data-ttu-id="b2fb5-108">**使用者** – 這是檢視報告的實際使用者。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-108">**Users** –  These are the actual end-users viewing reports.</span></span> <span data-ttu-id="b2fb5-109">在 Power BI Embedded 中，使用者是依應用程式權杖中的使用者名稱屬性來識別。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-109">In Power BI Embedded, users are identified by the username property in an App Token.</span></span>

<span data-ttu-id="b2fb5-110">**角色** – 使用者所屬角色。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-110">**Roles** – Users belong to roles.</span></span> <span data-ttu-id="b2fb5-111">角色是規則的容器，並可命名為類似「業務經理」或「業務代表」的項目。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-111">A role is a container for rules and can be named something like “Sales Manager” or “Sales Rep”.</span></span> <span data-ttu-id="b2fb5-112">在 Power BI Embedded 中，使用者是依應用程式權杖中的角色屬性來識別。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-112">In Power BI Embedded, users are identified by the roles property in an App Token.</span></span>

<span data-ttu-id="b2fb5-113">**規則** – 角色有規則，這些規則是要套用至資料的實際篩選器。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-113">**Rules** – Roles have rules, and those rules are the actual filters that are going to be applied to the data.</span></span> <span data-ttu-id="b2fb5-114">可以像 “Country = USA” 一樣簡單，或是更動態的項目。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-114">This could be as simple as “Country = USA” or something much more dynamic.</span></span>

### <a name="example"></a><span data-ttu-id="b2fb5-115">範例</span><span class="sxs-lookup"><span data-stu-id="b2fb5-115">Example</span></span>

<span data-ttu-id="b2fb5-116">對於這篇文章的其餘部分，我們將提供撰寫 RLS，然後在內嵌應用程式中使用的範例。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-116">For the rest of this article, we’ll provide an example of authoring RLS, and then consuming that within an embedded application.</span></span> <span data-ttu-id="b2fb5-117">我們的範例會使用 [零售分析範例](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX 檔案。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-117">Our example uses the [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX file.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

<span data-ttu-id="b2fb5-118">我們的零售分析範例會顯示特定零售鏈中所有商店的銷售額。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-118">Our Retail Analysis sample shows sales for all the stores in a particular retail chain.</span></span> <span data-ttu-id="b2fb5-119">沒有 RLS，不論哪一個區域的經理登入及檢視報告，都會看到相同的資料。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-119">Without RLS, no matter which district manager signs in and views the report, they’ll see the same data.</span></span> <span data-ttu-id="b2fb5-120">資深管理階層決定每個區域經理只能看到他們所管理的商店的銷售額，為了達成這個目的，我們可以使用 RLS。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-120">Senior management has determined each district manager should only see the sales for the stores they manage, and to do this, we can use RLS.</span></span>

<span data-ttu-id="b2fb5-121">RLS 是在 Power BI Desktop 中撰寫。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-121">RLS is authored in Power BI Desktop.</span></span> <span data-ttu-id="b2fb5-122">當開啟資料集和報告時，我們可以切換至圖表檢視來查看結構描述︰</span><span class="sxs-lookup"><span data-stu-id="b2fb5-122">When the dataset and report are opened, we can switch to diagram view to see the schema:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

<span data-ttu-id="b2fb5-123">以下是一些對於此結構描述要注意的事項：</span><span class="sxs-lookup"><span data-stu-id="b2fb5-123">Here are a few things to notice with this schema:</span></span>

* <span data-ttu-id="b2fb5-124">所有量值，例如**總銷售額**，是儲存在**銷售**事實資料表。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-124">All measures, like **Total Sales**, are stored in the **Sales** fact table.</span></span>
* <span data-ttu-id="b2fb5-125">有四個額外的相關維度資料表︰**項目**、**時間**、**商店**和**區域**。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-125">There are four additional related dimension tables: **Item**, **Time**, **Store**, and **District**.</span></span>
* <span data-ttu-id="b2fb5-126">關聯線的箭號表示篩選條件可以從一個資料表流向另一個資料表的方向。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-126">The arrows on the relationship lines indicate which way filters can flow from one table to another.</span></span> <span data-ttu-id="b2fb5-127">例如，如果篩選條件置於目前結構描述中的**時間[日期]**，它只會往下篩選**銷售**資料表中的值。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-127">For example, if a filter is placed on **Time[Date]**, in the current schema it would only filter down values in the **Sales** table.</span></span> <span data-ttu-id="b2fb5-128">其他資料表都不會受到此篩選條件的影響，因為關聯線的所有箭號都指向銷售資料表，不會指向其他方向。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-128">No other tables would be affected by this filter since all of the arrows on the relationship lines point to the sales table and not away.</span></span>
* <span data-ttu-id="b2fb5-129">**區域** 資料表表示誰是每個區域的經理︰</span><span class="sxs-lookup"><span data-stu-id="b2fb5-129">The **District** table indicates who the manager is for each district:</span></span>
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

<span data-ttu-id="b2fb5-130">根據此結構描述，如果我們將篩選條件套用至區域資料表中的 [區域經理] 資料行，且如果該篩選條件符合檢視報告的使用者，則該篩選條件也會往下篩選**商店**和**銷售**資料表，只顯示該特定區域經理的資料。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-130">Based on this schema, if we apply a filter to the **District Manager** column in the District table, and if that filter matches the user viewing the report, that filter will also filter down the **Store** and **Sales** tables to only show data for that particular district manager.</span></span>

<span data-ttu-id="b2fb5-131">方式如下：</span><span class="sxs-lookup"><span data-stu-id="b2fb5-131">Here’s how:</span></span>

1. <span data-ttu-id="b2fb5-132">在 [模型] 索引標籤中，按一下 [管理角色] 。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-132">On the Modeling tab, click **Manage Roles**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. <span data-ttu-id="b2fb5-133">建立新的角色，稱為 [經理] 。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-133">Create a new role called **Manager**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. <span data-ttu-id="b2fb5-134">在 [區域] 資料表中輸入下列 DAX 運算式︰**[District Manager] = USERNAME()**</span><span class="sxs-lookup"><span data-stu-id="b2fb5-134">In the **District** table enter the following DAX expression: **[District Manager] = USERNAME()**</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. <span data-ttu-id="b2fb5-135">若要確保規則都能運作，在 [模型] 索引標籤上，按一下 [以角色身分檢視]，然後輸入下列項目︰</span><span class="sxs-lookup"><span data-stu-id="b2fb5-135">To make sure the rules are working, on the **Modeling** tab, click **View as Roles**, and then enter the following:</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   <span data-ttu-id="b2fb5-136">報告隨即會顯示資料，如同您已登入為 **Andrew Ma**。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-136">The reports will now show data as if you were signed in as **Andrew Ma**.</span></span>

<span data-ttu-id="b2fb5-137">像我們在這裡所做的一樣套用篩選條件，將會往下篩選**區域**、**商店**和**銷售**資料表中的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-137">Applying the filter, the way we did here, will filter down all records in the **District**, **Store**, and **Sales** tables.</span></span> <span data-ttu-id="b2fb5-138">不過，由於**銷售**和**時間**之間的關聯的篩選方向，**銷售**和**項目**與**項目**和**時間**資料表將不會向下篩選。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-138">However, because of the filter direction on the relationships between **Sales** and **Time**, **Sales** and **Item**, and **Item** and **Time** tables will not be filtered down.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

<span data-ttu-id="b2fb5-139">對於此需求可能沒問題，但是，如果我們不想要讓經理查看他們沒有任何銷售的項目，我們可以針對關聯性開啟雙向交叉篩選，讓安全性篩選條件同時流向兩個方向。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-139">That may be ok for this requirement, however, if we don’t want managers to see items for which they don’t have any sales, we could turn on bidirectional cross-filtering for the relationship and flow the security filter in both directions.</span></span> <span data-ttu-id="b2fb5-140">這可以藉由編輯**銷售**和**項目**之間的關聯性來完成，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b2fb5-140">This can be done by editing the relationship between **Sales** and **Item**, like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

<span data-ttu-id="b2fb5-141">現在，篩選條件可以從銷售資料表流向 **項目** 資料表：</span><span class="sxs-lookup"><span data-stu-id="b2fb5-141">Now, filters can also flow from the Sales table to the **Item** table:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> <span data-ttu-id="b2fb5-142">如果您針對資料使用 DirectQuery 模式，您必須啟用雙向交叉篩選，方法是選取這兩個選項︰</span><span class="sxs-lookup"><span data-stu-id="b2fb5-142">If you're using DirectQuery mode for your data, you will need to enable bidirectional-cross filtering by selecting these two options:</span></span>

1. <span data-ttu-id="b2fb5-143">[檔案]  ->  [選項和設定]  ->  [預覽功能]  ->  [針對 DirectQuery 啟用兩個方向的交叉篩選]。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-143">**File** -> **Options and Settings** -> **Preview Features** -> **Enable cross filtering in both directions for DirectQuery**.</span></span>
2. <span data-ttu-id="b2fb5-144">[檔案]  ->  [選項和設定]  ->  [DirectQuery]  ->  [允許 DirectQuery 模式中的不受限制量值]。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-144">**File** -> **Options and Settings** -> **DirectQuery** -> **Allow unrestricted measure in DirectQuery mode**.</span></span>

<span data-ttu-id="b2fb5-145">若要深入了解雙向交叉篩選，下載 [SQL Server Analysis Services 2016 和 Power BI Desktop 中的雙向交叉篩選] [(](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx)) 白皮書。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-145">To learn more about bidirectional cross-filtering, download the [Bidirectional cross-filtering in SQL Server Analysis Services 2016 and Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) whitepaper.</span></span>

<span data-ttu-id="b2fb5-146">這會包裝 Power BI Desktop 中需要完成的所有工作，但還有一件工作需要完成，讓我們定義的 RLS 規則在 Power BI Embedded 中運作。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-146">This wraps up all the work that needs to be done in Power BI Desktop, but there’s one more piece of work that needs to be done to make the RLS rules we defined work in Power BI Embedded.</span></span> <span data-ttu-id="b2fb5-147">使用者是由您的應用程式和應用程式權杖驗證和授權，應用程式和應用程式權杖是用來授與使用者對於特定 Power BI Embedded 報告的存取權。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-147">Users are authenticated and authorized by your application and App tokens are used to grant that user access to a specific Power BI Embedded report.</span></span> <span data-ttu-id="b2fb5-148">Power BI Embedded 對於您的使用者是誰，並沒有任何特定資訊。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-148">Power BI Embedded doesn’t have any specific information on who your user is.</span></span> <span data-ttu-id="b2fb5-149">如果要讓 RLS 運作，您需要將一些額外的內容傳遞做為您的應用程式權杖的一部分︰</span><span class="sxs-lookup"><span data-stu-id="b2fb5-149">For RLS to work, you’ll need to pass some additional context as part of your app token:</span></span>

* <span data-ttu-id="b2fb5-150">**username** (選擇性) – 與 RLS 搭配使用，這是字串，可以在套用 RLS 規則時用來協助識別使用者。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-150">**username** (optional) – Used with RLS this is a string that can be used to help identify the user when applying RLS rules.</span></span> <span data-ttu-id="b2fb5-151">請參閱「搭配使用資料列層級安全性和 Power BI Embedded」</span><span class="sxs-lookup"><span data-stu-id="b2fb5-151">See Using Row Level Security with Power BI Embedded</span></span>
* <span data-ttu-id="b2fb5-152">**角色** – 字串，包含套用資料列層級安全性規則時要選取的角色。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-152">**roles** – A string containing the roles to select when applying Row Level Security rules.</span></span> <span data-ttu-id="b2fb5-153">如果傳遞多個角色，應該將它們傳遞為字串陣列。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-153">If passing more than one role, they should be passed as a string array.</span></span>

<span data-ttu-id="b2fb5-154">您可以使用 [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) 方法來建立權杖。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-154">You create the token by using the [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) method.</span></span> <span data-ttu-id="b2fb5-155">如果 username 屬性存在，則您也必須在角色中傳遞至少一個值。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-155">If the username property is present, you must also pass at least one value in roles.</span></span>

<span data-ttu-id="b2fb5-156">例如，您可以變更 EmbedSample。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-156">For example, you could change the EmbedSample.</span></span> <span data-ttu-id="b2fb5-157">DashboardController 第 55 行可以從</span><span class="sxs-lookup"><span data-stu-id="b2fb5-157">DashboardController line 55 could be updated from</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

<span data-ttu-id="b2fb5-158">更新成</span><span class="sxs-lookup"><span data-stu-id="b2fb5-158">to</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

<span data-ttu-id="b2fb5-159">完整的應用程式權杖看起來如下：</span><span class="sxs-lookup"><span data-stu-id="b2fb5-159">The full app token will look something like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

<span data-ttu-id="b2fb5-160">現在，所有項目都聚合在一起，當有人登入我們的應用程式以檢視此報告，他們將只能夠看到他們獲得允許可以看到的資料，如同我們的資料列層級安全性所定義。</span><span class="sxs-lookup"><span data-stu-id="b2fb5-160">Now, with all the pieces together, when someone logs into our application to view this report, they’ll only be able to see the data that they are allowed to see, as defined by our row-level security.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a><span data-ttu-id="b2fb5-161">另請參閱</span><span class="sxs-lookup"><span data-stu-id="b2fb5-161">See also</span></span>

[<span data-ttu-id="b2fb5-162">資料列層級安全性 (RLS) 與 Power</span><span class="sxs-lookup"><span data-stu-id="b2fb5-162">Row-level security (RLS) with Power</span></span>](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[<span data-ttu-id="b2fb5-163">在 Power BI Embedded 中驗證和授權</span><span class="sxs-lookup"><span data-stu-id="b2fb5-163">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="b2fb5-164">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="b2fb5-164">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="b2fb5-165">JavaScript 內嵌範例</span><span class="sxs-lookup"><span data-stu-id="b2fb5-165">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="b2fb5-166">有其他疑問？</span><span class="sxs-lookup"><span data-stu-id="b2fb5-166">More questions?</span></span> [<span data-ttu-id="b2fb5-167">試用 Power BI 社群</span><span class="sxs-lookup"><span data-stu-id="b2fb5-167">Try the Power BI Community</span></span>](http://community.powerbi.com/)

