---
title: "aaaHow toouse 自助式應用程式存取 |Microsoft 文件"
description: "啟用自助服務應用程式存取 tooallow 使用者 toofind 自己的應用程式"
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
ms.openlocfilehash: 03a44c20d544a6232fa802bcffaf70e5030ad3ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-self-service-application-access"></a><span data-ttu-id="08753-103">Toouse 自助應用程式的存取方式</span><span class="sxs-lookup"><span data-stu-id="08753-103">How toouse self-service application access</span></span>

<span data-ttu-id="08753-104">您的使用者可以自行探索從他們的存取面板應用程式之前，您需要 tooenable**自助式應用程式存取**tooany 應用程式，您會希望 tooallow 使用者 tooself-探索及要求的存取權。</span><span class="sxs-lookup"><span data-stu-id="08753-104">Before your users can self-discover applications from their access panel, you need tooenable **Self-service application access** tooany applications that you wish tooallow users tooself-discover and request access to.</span></span>

<span data-ttu-id="08753-105">這項功能是為您的絕佳方式，toosave 時間和金錢為 IT 群組，並強烈建議您與 Azure Active Directory 的現代應用程式部署的一部分。</span><span class="sxs-lookup"><span data-stu-id="08753-105">This feature is a great way for you toosave time and money as an IT group, and is highly recommended as part of a modern applications deployment with Azure Active Directory.</span></span>

<span data-ttu-id="08753-106">您可以使用這項功能︰</span><span class="sxs-lookup"><span data-stu-id="08753-106">Using this feature, you can:</span></span>

-   <span data-ttu-id="08753-107">讓使用者自行找出應用程式從 hello[應用程式存取面板](https://myapps.microsoft.com/)沒有終究 hello IT 群組。</span><span class="sxs-lookup"><span data-stu-id="08753-107">Let users self-discover applications from hello [Application Access Panel](https://myapps.microsoft.com/) without bothering hello IT group.</span></span>

-   <span data-ttu-id="08753-108">讓您可以查看誰具有要求存取、 移除存取權，並管理 hello 角色指派 toothem 加入這些使用者 tooa 預先設定的群組。</span><span class="sxs-lookup"><span data-stu-id="08753-108">Add those users tooa pre-configured group so you can see who has requested access, remove access, and manage hello roles assigned toothem.</span></span>

-   <span data-ttu-id="08753-109">選擇性地允許公司核准者 tooapprove 應用程式存取要求 hello 的 IT 團隊不一定如此。</span><span class="sxs-lookup"><span data-stu-id="08753-109">Optionally allow a business approver tooapprove application access requests so hello IT group doesn’t have to.</span></span>

-   <span data-ttu-id="08753-110">選擇性地設定 too10 個人可能核准存取 toothis 應用程式。</span><span class="sxs-lookup"><span data-stu-id="08753-110">Optionally configure up too10 individuals who may approve access toothis application.</span></span>

-   <span data-ttu-id="08753-111">您可以選擇允許公司核准者 tooset hello 密碼的使用者可以使用 toosign toohello 應用程式中，直接從 hello 公司核准者[應用程式存取面板](https://myapps.microsoft.com/)。</span><span class="sxs-lookup"><span data-stu-id="08753-111">Optionally allow a business approver tooset hello passwords those users can use toosign in toohello application, right from hello business approver’s [Application Access Panel](https://myapps.microsoft.com/).</span></span>

-   <span data-ttu-id="08753-112">選擇性地自動直接指派自助服務指派的使用者 tooan 應用程式角色。</span><span class="sxs-lookup"><span data-stu-id="08753-112">Optionally automatically assign self-service assigned users tooan application role directly.</span></span>

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a><span data-ttu-id="08753-113">啟用自助服務應用程式存取 tooallow 使用者 toofind 自己的應用程式</span><span class="sxs-lookup"><span data-stu-id="08753-113">Enable self-service application access tooallow users toofind their own applications</span></span>

<span data-ttu-id="08753-114">自助應用程式的存取是很好的方法 tooallow 使用者 tooself-探索應用程式，請選擇性地允許 hello 商務群組 tooapprove 存取 toothose 應用程式。</span><span class="sxs-lookup"><span data-stu-id="08753-114">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="08753-115">您可以允許 hello 商務群組 toomanage hello 認證指派 toothose 使用者從他們的存取面板的密碼單一登入應用程式權限。</span><span class="sxs-lookup"><span data-stu-id="08753-115">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="08753-116">tooenable 自助應用程式存取 tooan 應用程式，下列的後續 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="08753-116">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="08753-117">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="08753-117">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="08753-118">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="08753-118">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="08753-119">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="08753-119">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="08753-120">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="08753-120">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="08753-121">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="08753-121">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="08753-122">如果看不到您想要顯示於此處的 hello 應用程式，請使用 hello**篩選**控制項上方的 hello hello**所有應用程式清單**組 hello 和**顯示**太選項**所有應用程式。**</span><span class="sxs-lookup"><span data-stu-id="08753-122">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="08753-123">選取您想要 tooenable 自助存取 toofrom hello 清單 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="08753-123">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="08753-124">一旦 hello 應用程式載入時，按一下 **自助**從 hello 應用程式的左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="08753-124">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="08753-125">tooenable 自助式應用程式存取此應用程式中，開啟 hello**允許使用者應用程式的存取 toothis toorequest？**太切換**[是]。**</span><span class="sxs-lookup"><span data-stu-id="08753-125">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="08753-126">Tooselect hello 群組 toowhich 要求使用者應加入 toothis 應用程式的存取，接下來，按一下 hello 選取器下一個 toohello 標籤**toowhich 群組應該指派給新增的使用者？**並選取一個群組。</span><span class="sxs-lookup"><span data-stu-id="08753-126">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="08753-127">**選擇性：**如果您想 toorequire 商務核准允許使用者存取之前，設定 hello**之前授與存取 toothis 應用程式需要核准？**太切換**是**。</span><span class="sxs-lookup"><span data-stu-id="08753-127">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="08753-128">**選用： 為應用程式上，使用密碼單一登**如果您想 tooallow toothis 應用程式的核准的使用者傳送這些商務核准者 toospecify hello 密碼時，設定 hello**允許核准者 tooset此應用程式的使用者的密碼嗎？**太切換**是**。</span><span class="sxs-lookup"><span data-stu-id="08753-128">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="08753-129">**選擇性：** toospecify hello 公司核准者允許 tooapprove 存取 toothis 應用程式中，按一下 hello 選取器下一個 toohello 標籤**誰 tooapprove 存取 toothis 應用程式？** tooselect 向上too10 個別商務核准者。</span><span class="sxs-lookup"><span data-stu-id="08753-129">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

   * <span data-ttu-id="08753-130">不支援群組。</span><span class="sxs-lookup"><span data-stu-id="08753-130">Groups are not supported.</span></span>

13. <span data-ttu-id="08753-131">**選擇性：** **的應用程式的公開角色**，如果您想 tooa tooassign 自助核准的使用者的角色，按一下 下一步 toohello 的 hello 選取器**toowhich 角色應該指派給使用者在此應用程式嗎？** tooselect hello 角色 toowhich 應該指派這些使用者。</span><span class="sxs-lookup"><span data-stu-id="08753-131">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="08753-132">按一下 hello**儲存**在 hello 刀鋒視窗 toofinish hello 最上方的按鈕。</span><span class="sxs-lookup"><span data-stu-id="08753-132">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="08753-133">一旦您完成自助應用程式組態設定，使用者可以瀏覽 tootheir[應用程式存取面板](https://myapps.microsoft.com/)按一下 hello **+ 加**按鈕 toofind hello 應用程式 toowhich 已啟用自助存取。</span><span class="sxs-lookup"><span data-stu-id="08753-133">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="08753-134">商務核准者在其[應用程式存取面板](https://myapps.microsoft.com/)中也會看到通知。</span><span class="sxs-lookup"><span data-stu-id="08753-134">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="08753-135">您可以啟用在使用者要求存取 tooan 應用程式需要核准時，通知他們的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="08753-135">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="08753-136">這些核准支援單一核准工作流程，這表示如果您指定多個核准者，任何單一核准者可能會核准存取 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="08753-136">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access toohello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08753-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="08753-137">Next steps</span></span>
[<span data-ttu-id="08753-138">設定 Azure Active Directory 進行自助服務群組管理</span><span class="sxs-lookup"><span data-stu-id="08753-138">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
