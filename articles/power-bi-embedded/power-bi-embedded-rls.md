---
title: "使用 Power BI Embedded aaaRow 層級安全性"
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
ms.openlocfilehash: 384f78826ecc710cf8f101b251ae68b074f3e98b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a><span data-ttu-id="005cb-103">Power BI Embedded 的資料列層級安全性</span><span class="sxs-lookup"><span data-stu-id="005cb-103">Row level security with Power BI Embedded</span></span>

<span data-ttu-id="005cb-104">資料列層級安全性 (RLS) 可以是報表或資料集，讓多個不同的使用者 toouse hello 所有文件都看到不同的資料時的相同報表中使用的 toorestrict 使用者存取 tooparticular 資料。</span><span class="sxs-lookup"><span data-stu-id="005cb-104">Row level security (RLS) can be used toorestrict user access tooparticular data within a report or dataset, allowing for multiple different users toouse hello same report while all seeing different data.</span></span> <span data-ttu-id="005cb-105">Power BI Embedded 現在支援使用 RLS 設定資料集。</span><span class="sxs-lookup"><span data-stu-id="005cb-105">Power BI Embedded now supports datasets configured with RLS.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

<span data-ttu-id="005cb-106">在順序 tootake 優點 RLS，務必了解三個主要概念;使用者、 角色和規則。</span><span class="sxs-lookup"><span data-stu-id="005cb-106">In order tootake advantage of RLS, it’s important you understand three main concepts; Users, Roles, and Rules.</span></span> <span data-ttu-id="005cb-107">讓我們仔細看看每個概念：</span><span class="sxs-lookup"><span data-stu-id="005cb-107">Let’s take a closer look at each:</span></span>

<span data-ttu-id="005cb-108">**使用者**– 這些 hello 實際使用者檢視報表。</span><span class="sxs-lookup"><span data-stu-id="005cb-108">**Users** –  These are hello actual end-users viewing reports.</span></span> <span data-ttu-id="005cb-109">Power BI Embedded，使用者所識別的應用程式權杖中的 hello username 屬性。</span><span class="sxs-lookup"><span data-stu-id="005cb-109">In Power BI Embedded, users are identified by hello username property in an App Token.</span></span>

<span data-ttu-id="005cb-110">**角色**– 使用者所屬的 tooroles。</span><span class="sxs-lookup"><span data-stu-id="005cb-110">**Roles** – Users belong tooroles.</span></span> <span data-ttu-id="005cb-111">角色是規則的容器，並可命名為類似「業務經理」或「業務代表」的項目。</span><span class="sxs-lookup"><span data-stu-id="005cb-111">A role is a container for rules and can be named something like “Sales Manager” or “Sales Rep”.</span></span> <span data-ttu-id="005cb-112">Power BI Embedded，使用者所識別的應用程式權杖中的 hello 角色屬性。</span><span class="sxs-lookup"><span data-stu-id="005cb-112">In Power BI Embedded, users are identified by hello roles property in an App Token.</span></span>

<span data-ttu-id="005cb-113">**規則**– 角色其規則，而且這些規則將套用的 toobe toohello 資料 hello 實際篩選。</span><span class="sxs-lookup"><span data-stu-id="005cb-113">**Rules** – Roles have rules, and those rules are hello actual filters that are going toobe applied toohello data.</span></span> <span data-ttu-id="005cb-114">可以像 “Country = USA” 一樣簡單，或是更動態的項目。</span><span class="sxs-lookup"><span data-stu-id="005cb-114">This could be as simple as “Country = USA” or something much more dynamic.</span></span>

### <a name="example"></a><span data-ttu-id="005cb-115">範例</span><span class="sxs-lookup"><span data-stu-id="005cb-115">Example</span></span>

<span data-ttu-id="005cb-116">這篇文章 hello 其餘部分，我們會提供撰寫 RLS，並再耗用，內嵌的應用程式中的範例。</span><span class="sxs-lookup"><span data-stu-id="005cb-116">For hello rest of this article, we’ll provide an example of authoring RLS, and then consuming that within an embedded application.</span></span> <span data-ttu-id="005cb-117">我們的範例會使用 hello[零售分析範例](http://go.microsoft.com/fwlink/?LinkID=780547)PBIX 檔案。</span><span class="sxs-lookup"><span data-stu-id="005cb-117">Our example uses hello [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX file.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

<span data-ttu-id="005cb-118">我們零售分析範例會顯示特定零售鏈結中所有的 hello 商店的銷售。</span><span class="sxs-lookup"><span data-stu-id="005cb-118">Our Retail Analysis sample shows sales for all hello stores in a particular retail chain.</span></span> <span data-ttu-id="005cb-119">沒有 RLS，不論哪個地區管理員登入並檢視 hello 報表，就會看到 hello 相同的資料。</span><span class="sxs-lookup"><span data-stu-id="005cb-119">Without RLS, no matter which district manager signs in and views hello report, they’ll see hello same data.</span></span> <span data-ttu-id="005cb-120">每個區域經理只能看到 hello 銷售 hello 存放區所管理，以及 toodo 這判定資深管理，我們可以使用 RLS。</span><span class="sxs-lookup"><span data-stu-id="005cb-120">Senior management has determined each district manager should only see hello sales for hello stores they manage, and toodo this, we can use RLS.</span></span>

<span data-ttu-id="005cb-121">RLS 是在 Power BI Desktop 中撰寫。</span><span class="sxs-lookup"><span data-stu-id="005cb-121">RLS is authored in Power BI Desktop.</span></span> <span data-ttu-id="005cb-122">Hello 資料集和報表會開啟時，我們可以切換 toodiagram 檢視 toosee hello 結構描述：</span><span class="sxs-lookup"><span data-stu-id="005cb-122">When hello dataset and report are opened, we can switch toodiagram view toosee hello schema:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

<span data-ttu-id="005cb-123">以下是幾件事 toonotice 與此結構描述：</span><span class="sxs-lookup"><span data-stu-id="005cb-123">Here are a few things toonotice with this schema:</span></span>

* <span data-ttu-id="005cb-124">所有量值，例如**Total Sales**，會儲存在 hello**銷售**事實資料表。</span><span class="sxs-lookup"><span data-stu-id="005cb-124">All measures, like **Total Sales**, are stored in hello **Sales** fact table.</span></span>
* <span data-ttu-id="005cb-125">有四個額外的相關維度資料表︰**項目**、**時間**、**商店**和**區域**。</span><span class="sxs-lookup"><span data-stu-id="005cb-125">There are four additional related dimension tables: **Item**, **Time**, **Store**, and **District**.</span></span>
* <span data-ttu-id="005cb-126">hello 關聯性線條上的 hello 箭號表示篩選條件可以從一個資料表 tooanother 流動的方式。</span><span class="sxs-lookup"><span data-stu-id="005cb-126">hello arrows on hello relationship lines indicate which way filters can flow from one table tooanother.</span></span> <span data-ttu-id="005cb-127">比方說，如果篩選置於**時間 [Date]**，hello 目前結構描述中就會只往下篩選中 hello 值**銷售**資料表。</span><span class="sxs-lookup"><span data-stu-id="005cb-127">For example, if a filter is placed on **Time[Date]**, in hello current schema it would only filter down values in hello **Sales** table.</span></span> <span data-ttu-id="005cb-128">沒有其他資料表會受到這個篩選條件，因為所有的 hello 箭號 hello 關聯性線條點 toohello 銷售資料表並不會離開。</span><span class="sxs-lookup"><span data-stu-id="005cb-128">No other tables would be affected by this filter since all of hello arrows on hello relationship lines point toohello sales table and not away.</span></span>
* <span data-ttu-id="005cb-129">hello**地區**資料表表示 hello 管理員的每個區域者：</span><span class="sxs-lookup"><span data-stu-id="005cb-129">hello **District** table indicates who hello manager is for each district:</span></span>
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

<span data-ttu-id="005cb-130">根據此結構描述，如果我們套用篩選器 toohello**區域經理**中的資料行 hello 區域資料表，和該篩選條件符合 hello 使用者檢視 hello 報表，如果該篩選條件也將篩選向下 hello**存放區**和**銷售**資料表 tooonly 顯示該特定地區的資料管理員。</span><span class="sxs-lookup"><span data-stu-id="005cb-130">Based on this schema, if we apply a filter toohello **District Manager** column in hello District table, and if that filter matches hello user viewing hello report, that filter will also filter down hello **Store** and **Sales** tables tooonly show data for that particular district manager.</span></span>

<span data-ttu-id="005cb-131">方式如下：</span><span class="sxs-lookup"><span data-stu-id="005cb-131">Here’s how:</span></span>

1. <span data-ttu-id="005cb-132">在 [hello 模型] 索引標籤上按一下**管理角色**。</span><span class="sxs-lookup"><span data-stu-id="005cb-132">On hello Modeling tab, click **Manage Roles**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. <span data-ttu-id="005cb-133">建立新的角色，稱為 [經理] 。</span><span class="sxs-lookup"><span data-stu-id="005cb-133">Create a new role called **Manager**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. <span data-ttu-id="005cb-134">在 hello**地區**資料表輸入下列 DAX 運算式的 hello: **[區域經理] = username （）**</span><span class="sxs-lookup"><span data-stu-id="005cb-134">In hello **District** table enter hello following DAX expression: **[District Manager] = USERNAME()**</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. <span data-ttu-id="005cb-135">使用 toomake 確定 hello 規則，在 hello**模型**索引標籤上，按一下 **以角色身分檢視**，然後輸入 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="005cb-135">toomake sure hello rules are working, on hello **Modeling** tab, click **View as Roles**, and then enter hello following:</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   <span data-ttu-id="005cb-136">hello 報表現在將會顯示資料如同您已登入為**Andrew Ma**。</span><span class="sxs-lookup"><span data-stu-id="005cb-136">hello reports will now show data as if you were signed in as **Andrew Ma**.</span></span>

<span data-ttu-id="005cb-137">套用 hello 篩選，在這裡，我們所做的 hello 方式關閉 hello 中的所有記錄會篩選**地區**，**存放區**，和**銷售**資料表。</span><span class="sxs-lookup"><span data-stu-id="005cb-137">Applying hello filter, hello way we did here, will filter down all records in hello **District**, **Store**, and **Sales** tables.</span></span> <span data-ttu-id="005cb-138">不過，由於 hello 篩選方向 hello 之間的關聯性上**銷售**和**時間**，**銷售**和**項目**，和**項目**和**時間**將不會向下篩選資料表。</span><span class="sxs-lookup"><span data-stu-id="005cb-138">However, because of hello filter direction on hello relationships between **Sales** and **Time**, **Sales** and **Item**, and **Item** and **Time** tables will not be filtered down.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

<span data-ttu-id="005cb-139">可能是 [確定]，這項需求，不過，如果我們不想其不具有任何銷售經理 toosee 項目，我們無法開啟雙向交叉篩選兩個方向的 hello 關聯性和流程 hello 安全性篩選。</span><span class="sxs-lookup"><span data-stu-id="005cb-139">That may be ok for this requirement, however, if we don’t want managers toosee items for which they don’t have any sales, we could turn on bidirectional cross-filtering for hello relationship and flow hello security filter in both directions.</span></span> <span data-ttu-id="005cb-140">作法是藉由編輯 hello 之間的關聯性**銷售**和**項目**，如下所示：</span><span class="sxs-lookup"><span data-stu-id="005cb-140">This can be done by editing hello relationship between **Sales** and **Item**, like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

<span data-ttu-id="005cb-141">現在，篩選可以也傳送 hello Sales 資料表 toohello 從**項目**資料表：</span><span class="sxs-lookup"><span data-stu-id="005cb-141">Now, filters can also flow from hello Sales table toohello **Item** table:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> <span data-ttu-id="005cb-142">如果您使用 DirectQuery 模式為您的資料，您將需要 tooenable 雙向交叉篩選選取這兩個選項：</span><span class="sxs-lookup"><span data-stu-id="005cb-142">If you're using DirectQuery mode for your data, you will need tooenable bidirectional-cross filtering by selecting these two options:</span></span>

1. <span data-ttu-id="005cb-143">[檔案]  ->  [選項和設定]  ->  [預覽功能]  ->  [針對 DirectQuery 啟用兩個方向的交叉篩選]。</span><span class="sxs-lookup"><span data-stu-id="005cb-143">**File** -> **Options and Settings** -> **Preview Features** -> **Enable cross filtering in both directions for DirectQuery**.</span></span>
2. <span data-ttu-id="005cb-144">[檔案]  ->  [選項和設定]  ->  [DirectQuery]  ->  [允許 DirectQuery 模式中的不受限制量值]。</span><span class="sxs-lookup"><span data-stu-id="005cb-144">**File** -> **Options and Settings** -> **DirectQuery** -> **Allow unrestricted measure in DirectQuery mode**.</span></span>

<span data-ttu-id="005cb-145">深入了解雙向交叉篩選，下載 hello toolearn[雙向交叉篩選 SQL Server Analysis Services 2016 和 Power BI Desktop 中](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx)白皮書。</span><span class="sxs-lookup"><span data-stu-id="005cb-145">toolearn more about bidirectional cross-filtering, download hello [Bidirectional cross-filtering in SQL Server Analysis Services 2016 and Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) whitepaper.</span></span>

<span data-ttu-id="005cb-146">這會結束所有的 hello 工作需要 toobe 完成在 Power BI Desktop 中，但沒有一個多份工作需要完成的 toobe toomake hello RLS 規則我們在 Power BI Embedded 定義工作。</span><span class="sxs-lookup"><span data-stu-id="005cb-146">This wraps up all hello work that needs toobe done in Power BI Desktop, but there’s one more piece of work that needs toobe done toomake hello RLS rules we defined work in Power BI Embedded.</span></span> <span data-ttu-id="005cb-147">使用者獲得驗證和授權您的應用程式和應用程式語彙基元是使用的 toogrant 該使用者存取 tooa 特定 Power BI Embedded 報表。</span><span class="sxs-lookup"><span data-stu-id="005cb-147">Users are authenticated and authorized by your application and App tokens are used toogrant that user access tooa specific Power BI Embedded report.</span></span> <span data-ttu-id="005cb-148">Power BI Embedded 對於您的使用者是誰，並沒有任何特定資訊。</span><span class="sxs-lookup"><span data-stu-id="005cb-148">Power BI Embedded doesn’t have any specific information on who your user is.</span></span> <span data-ttu-id="005cb-149">RLS toowork，您將需要 toopass 某些額外的內容做為您的應用程式的權杖的一部分：</span><span class="sxs-lookup"><span data-stu-id="005cb-149">For RLS toowork, you’ll need toopass some additional context as part of your app token:</span></span>

* <span data-ttu-id="005cb-150">**使用者名稱**（選用） – 使用 rls 這是可用的字串 toohelp 套用 RLS 規則時，請識別 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="005cb-150">**username** (optional) – Used with RLS this is a string that can be used toohelp identify hello user when applying RLS rules.</span></span> <span data-ttu-id="005cb-151">請參閱「搭配使用資料列層級安全性和 Power BI Embedded」</span><span class="sxs-lookup"><span data-stu-id="005cb-151">See Using Row Level Security with Power BI Embedded</span></span>
* <span data-ttu-id="005cb-152">**角色**– 套用資料列層級安全性規則時，包含 hello 角色 tooselect 的字串。</span><span class="sxs-lookup"><span data-stu-id="005cb-152">**roles** – A string containing hello roles tooselect when applying Row Level Security rules.</span></span> <span data-ttu-id="005cb-153">如果傳遞多個角色，應該將它們傳遞為字串陣列。</span><span class="sxs-lookup"><span data-stu-id="005cb-153">If passing more than one role, they should be passed as a string array.</span></span>

<span data-ttu-id="005cb-154">使用 hello 建立 hello 語彙基元[CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__)方法。</span><span class="sxs-lookup"><span data-stu-id="005cb-154">You create hello token by using hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) method.</span></span> <span data-ttu-id="005cb-155">如果 hello username 屬性存在，則您也必須在角色中傳遞至少一個值。</span><span class="sxs-lookup"><span data-stu-id="005cb-155">If hello username property is present, you must also pass at least one value in roles.</span></span>

<span data-ttu-id="005cb-156">例如，您可以變更 hello EmbedSample。</span><span class="sxs-lookup"><span data-stu-id="005cb-156">For example, you could change hello EmbedSample.</span></span> <span data-ttu-id="005cb-157">DashboardController 第 55 行可以從</span><span class="sxs-lookup"><span data-stu-id="005cb-157">DashboardController line 55 could be updated from</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

<span data-ttu-id="005cb-158">to</span><span class="sxs-lookup"><span data-stu-id="005cb-158">to</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

<span data-ttu-id="005cb-159">hello 完整的應用程式語彙基元看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="005cb-159">hello full app token will look something like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

<span data-ttu-id="005cb-160">現在，與所有的 hello 片段放在一起，當有人登入我們的應用程式 tooview 這份報表，他們只必須能夠 toosee hello 資料才會允許 toosee，本公司的資料列層級安全性所定義。</span><span class="sxs-lookup"><span data-stu-id="005cb-160">Now, with all hello pieces together, when someone logs into our application tooview this report, they’ll only be able toosee hello data that they are allowed toosee, as defined by our row-level security.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a><span data-ttu-id="005cb-161">另請參閱</span><span class="sxs-lookup"><span data-stu-id="005cb-161">See also</span></span>

[<span data-ttu-id="005cb-162">資料列層級安全性 (RLS) 與 Power</span><span class="sxs-lookup"><span data-stu-id="005cb-162">Row-level security (RLS) with Power</span></span>](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[<span data-ttu-id="005cb-163">在 Power BI Embedded 中驗證和授權</span><span class="sxs-lookup"><span data-stu-id="005cb-163">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="005cb-164">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="005cb-164">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
[<span data-ttu-id="005cb-165">JavaScript 內嵌範例</span><span class="sxs-lookup"><span data-stu-id="005cb-165">JavaScript Embed Sample</span></span>](https://microsoft.github.io/PowerBI-JavaScript/demo/)  
<span data-ttu-id="005cb-166">有其他疑問？</span><span class="sxs-lookup"><span data-stu-id="005cb-166">More questions?</span></span> [<span data-ttu-id="005cb-167">再試一次 hello Power BI 社群</span><span class="sxs-lookup"><span data-stu-id="005cb-167">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

