---
title: "使用自助式應用程式存取 aaaProblem |Microsoft 文件"
description: "疑難排解問題相關的 tooself 服務應用程式存取"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.reviewer: japere
ms.openlocfilehash: 2487be1df191a4e7fd0bcc0ebbe4ea62fae0fd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="problem-using-self-service-application-access"></a><span data-ttu-id="87e49-103">使用自助應用程式存取時遇到問題</span><span class="sxs-lookup"><span data-stu-id="87e49-103">Problem using self-service application access</span></span>

<span data-ttu-id="87e49-104">自助應用程式的存取是很好的方法 tooallow 使用者 tooself-探索應用程式，請選擇性地允許 hello 商務群組 tooapprove 存取 toothose 應用程式。</span><span class="sxs-lookup"><span data-stu-id="87e49-104">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="87e49-105">您可以允許 hello 商務群組 toomanage hello 認證指派 toothose 使用者從他們的存取面板的密碼單一登入應用程式權限。</span><span class="sxs-lookup"><span data-stu-id="87e49-105">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="87e49-106">您的使用者可以自行探索從他們的存取面板應用程式之前，您需要 tooenable**自助式應用程式存取**tooany 應用程式，您會希望 tooallow 使用者 tooself-探索及要求的存取權。</span><span class="sxs-lookup"><span data-stu-id="87e49-106">Before your users can self-discover applications from their access panel, you need tooenable **Self-service application access** tooany applications that you wish tooallow users tooself-discover and request access to.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="87e49-107">一般會先發出 toocheck</span><span class="sxs-lookup"><span data-stu-id="87e49-107">General issues toocheck first</span></span>

-   <span data-ttu-id="87e49-108">請確定已正確設定自助應用程式存取。</span><span class="sxs-lookup"><span data-stu-id="87e49-108">Make sure self-service application access is configured correctly.</span></span> <span data-ttu-id="87e49-109">請參閱 「 如何 tooconfigure 自助應用程式存取 」。</span><span class="sxs-lookup"><span data-stu-id="87e49-109">See “How tooconfigure self-service application access”.</span></span>

-   <span data-ttu-id="87e49-110">請確定 hello 使用者或群組已啟用 toorequest 自助式應用程式存取。</span><span class="sxs-lookup"><span data-stu-id="87e49-110">Make sure hello user or group has been enabled toorequest self-service application access.</span></span>

-   <span data-ttu-id="87e49-111">請確定 hello 使用者造訪 hello 自助應用程式存取正確的位置。</span><span class="sxs-lookup"><span data-stu-id="87e49-111">Make sure hello user is visiting hello correct place for self-service application access.</span></span> <span data-ttu-id="87e49-112">使用者可瀏覽 tootheir[應用程式存取面板](https://myapps.microsoft.com/)按一下 hello **+ 加**按鈕 toofind hello 應用程式 toowhich 您已啟用自助存取。</span><span class="sxs-lookup"><span data-stu-id="87e49-112">users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled self-service access.</span></span>

-   <span data-ttu-id="87e49-113">如果最近已設定自助應用程式的存取，toosign 入和登出再試一次到 hello 使用者的存取面板後幾分鐘的時間 toosee 如果 hello 自助存取變更已出現。</span><span class="sxs-lookup"><span data-stu-id="87e49-113">If self-service application access was just recently configured, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello self-service access changes have appeared.</span></span>

## <a name="how-tooconfigure-self-service-application-access"></a><span data-ttu-id="87e49-114">Tooconfigure 自助應用程式的存取方式</span><span class="sxs-lookup"><span data-stu-id="87e49-114">How tooconfigure self-service application access</span></span>

<span data-ttu-id="87e49-115">tooenable 自助應用程式存取 tooan 應用程式，下列的後續 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="87e49-115">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="87e49-116">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="87e49-116">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="87e49-117">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="87e49-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="87e49-118">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="87e49-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="87e49-119">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="87e49-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="87e49-120">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="87e49-120">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="87e49-121">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="87e49-121">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="87e49-122">選取您想要 tooenable 自助存取 toofrom hello 清單 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="87e49-122">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="87e49-123">一旦 hello 應用程式載入時，按一下 **自助**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="87e49-123">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="87e49-124">tooenable 自助式應用程式存取此應用程式中，開啟 hello**允許使用者應用程式的存取 toothis toorequest？**太切換**[是]。**</span><span class="sxs-lookup"><span data-stu-id="87e49-124">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="87e49-125">Tooselect hello 群組 toowhich 要求使用者應加入 toothis 應用程式的存取，接下來，按一下 hello 選取器下一個 toohello 標籤**toowhich 群組應該指派給新增的使用者？**並選取一個群組。</span><span class="sxs-lookup"><span data-stu-id="87e49-125">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="87e49-126">**選擇性：**如果您想 toorequire 商務核准允許使用者存取之前，設定 hello**之前授與存取 toothis 應用程式需要核准？**太切換**是**。</span><span class="sxs-lookup"><span data-stu-id="87e49-126">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="87e49-127">**選用： 為應用程式上，使用密碼單一登**如果您想 tooallow toothis 應用程式的核准的使用者傳送這些商務核准者 toospecify hello 密碼時，設定 hello**允許核准者 tooset此應用程式的使用者的密碼嗎？**太切換**是**。</span><span class="sxs-lookup"><span data-stu-id="87e49-127">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="87e49-128">**選擇性：** toospecify hello 公司核准者允許 tooapprove 存取 toothis 應用程式中，按一下 hello 選取器下一個 toohello 標籤**誰 tooapprove 存取 toothis 應用程式？** tooselect 向上too10 個別商務核准者。</span><span class="sxs-lookup"><span data-stu-id="87e49-128">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

 >[!NOTE]
 > <span data-ttu-id="87e49-129">不支援群組。</span><span class="sxs-lookup"><span data-stu-id="87e49-129">Groups are not supported.</span></span>
 >
 >

13. <span data-ttu-id="87e49-130">**選擇性：** **的應用程式的公開角色**，如果您想 tooa tooassign 自助核准的使用者的角色，按一下 下一步 toohello 的 hello 選取器**toowhich 角色應該指派給使用者在此應用程式嗎？** tooselect hello 角色 toowhich 應該指派這些使用者。</span><span class="sxs-lookup"><span data-stu-id="87e49-130">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="87e49-131">按一下 hello**儲存**在 hello 刀鋒視窗 toofinish hello 最上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="87e49-131">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="87e49-132">一旦您完成自助應用程式組態設定，使用者可以瀏覽 tootheir[應用程式存取面板](https://myapps.microsoft.com/)按一下 hello **+ 加**按鈕 toofind hello 應用程式 toowhich 已啟用自助存取。</span><span class="sxs-lookup"><span data-stu-id="87e49-132">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="87e49-133">商務核准者在其[應用程式存取面板](https://myapps.microsoft.com/)中也會看到通知。</span><span class="sxs-lookup"><span data-stu-id="87e49-133">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="87e49-134">您可以啟用在使用者要求存取 tooan 應用程式需要核准時，通知他們的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="87e49-134">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="87e49-135">這些核准支援單一核准工作流程，這表示如果您指定多個核准者，任何單一核准者可能會核准存取 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="87e49-135">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access toohello application.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="87e49-136">如果這些疑難排解步驟無法解決 hello 問題</span><span class="sxs-lookup"><span data-stu-id="87e49-136">If these troubleshooting steps do not resolve hello issue</span></span> 

<span data-ttu-id="87e49-137">開啟支援票證以 hello 如果有的話，下列資訊：</span><span class="sxs-lookup"><span data-stu-id="87e49-137">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="87e49-138">相互關聯錯誤 ID</span><span class="sxs-lookup"><span data-stu-id="87e49-138">Correlation error ID</span></span>

-   <span data-ttu-id="87e49-139">UPN (使用者電子郵件地址)</span><span class="sxs-lookup"><span data-stu-id="87e49-139">UPN (user email address)</span></span>

-   <span data-ttu-id="87e49-140">TenantID</span><span class="sxs-lookup"><span data-stu-id="87e49-140">TenantID</span></span>

-   <span data-ttu-id="87e49-141">瀏覽器類型</span><span class="sxs-lookup"><span data-stu-id="87e49-141">Browser type</span></span>

-   <span data-ttu-id="87e49-142">錯誤發生期間的時區和時間/時間範圍</span><span class="sxs-lookup"><span data-stu-id="87e49-142">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="87e49-143">Fiddler 追蹤</span><span class="sxs-lookup"><span data-stu-id="87e49-143">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="87e49-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="87e49-144">Next steps</span></span>
[<span data-ttu-id="87e49-145">設定 Azure Active Directory 進行自助服務群組管理</span><span class="sxs-lookup"><span data-stu-id="87e49-145">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
