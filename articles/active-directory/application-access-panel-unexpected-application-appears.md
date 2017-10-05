---
title: "應用程式如何出現在存取面板上 | Microsoft Docs"
description: "針對應用程式為什麼出現在存取面板上進行疑難排解"
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
ms.reviewr: japere
ms.openlocfilehash: f8ccf2cf66b49940bc7f2b9f4764020efc04838e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-applications-appear-on-the-access-panel"></a><span data-ttu-id="316a4-103">應用程式如何出現在存取面板上</span><span class="sxs-lookup"><span data-stu-id="316a4-103">How applications appear on the access panel</span></span>

<span data-ttu-id="316a4-104">存取面板是網頁型入口網站，可讓在 Azure Active Directory (Azure AD) 中具有公司或學校帳戶的使用者，檢視和啟動 Azure AD 系統管理員已授權他們存取的雲端式應用程式。</span><span class="sxs-lookup"><span data-stu-id="316a4-104">The Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) to view and start cloud-based applications that the Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="316a4-105">在 Azure AD 入口網站中可代表使用者設定這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="316a4-105">These applications are configured on behalf of the user in the Azure AD portal.</span></span> <span data-ttu-id="316a4-106">系統管理員可以直接將應用程式佈建給使用者，或使用者所屬的群組，而讓應用程式出現在使用者的存取面板上。</span><span class="sxs-lookup"><span data-stu-id="316a4-106">The admin can provision the application to the user directly or to a group a user is part of resulting in the application appearing on the user’s Access Panel.</span></span>

## <a name="general-issues-to-check-first"></a><span data-ttu-id="316a4-107">首先檢查的一般問題</span><span class="sxs-lookup"><span data-stu-id="316a4-107">General issues to check first</span></span>

-   <span data-ttu-id="316a4-108">如果才剛從使用者或使用者所屬的群組移除應用程式，請在幾分鐘之後嘗試登入並再次登出使用者的存取面板，查明是否已移除該應用程式。</span><span class="sxs-lookup"><span data-stu-id="316a4-108">If an application was just removed from a user or group the user is a member of, try to sign in and out again into the user’s Access Panel after a few minutes to see if the application is removed.</span></span>

-   <span data-ttu-id="316a4-109">如果才剛從使用者或使用者所屬群組移除授權，則根據群組的大小和複雜度而定，可能要經過一段很長的時間，變更才會生效。</span><span class="sxs-lookup"><span data-stu-id="316a4-109">If a license was just removed from a user or group the user is a member of this may take a long time, depending on the size and complexity of the group for changes to be made.</span></span> <span data-ttu-id="316a4-110">登入存取面板之前，請多等一些時間。</span><span class="sxs-lookup"><span data-stu-id="316a4-110">Allow for extra time before signing into the Access Panel.</span></span>

## <a name="problems-related-to-assigning-applications-to-users"></a><span data-ttu-id="316a4-111">將應用程式指派給使用者的相關問題</span><span class="sxs-lookup"><span data-stu-id="316a4-111">Problems related to assigning applications to users</span></span>

<span data-ttu-id="316a4-112">使用者可能因為先前已指派至應用程式，而在存取面板上看見該應用程式。</span><span class="sxs-lookup"><span data-stu-id="316a4-112">A user may be seeing an application on their Access Panel because they had been previously assigned to it.</span></span> <span data-ttu-id="316a4-113">以下是一些檢查方法︰</span><span class="sxs-lookup"><span data-stu-id="316a4-113">Below are some ways to check:</span></span>

-   [<span data-ttu-id="316a4-114">檢查使用者是否已指派至應用程式</span><span class="sxs-lookup"><span data-stu-id="316a4-114">Check if a user is assigned to the application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="316a4-115">檢查使用者是否獲得應用程式相關的授權</span><span class="sxs-lookup"><span data-stu-id="316a4-115">Check if a user is under a license related to the application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-to-the-application"></a><span data-ttu-id="316a4-116">檢查使用者是否已指派至應用程式</span><span class="sxs-lookup"><span data-stu-id="316a4-116">Check if a user is assigned to the application</span></span>

<span data-ttu-id="316a4-117">若要檢查是否已將使用者指派給應用程式，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="316a4-117">To check if a user is assigned to the application, follow the steps below:</span></span>

1.  <span data-ttu-id="316a4-118">開啟 [**Azure 入口網站**](https://portal.azure.com/)，然後以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="316a4-118">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="316a4-119">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="316a4-119">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="316a4-120">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="316a4-120">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="316a4-121">從 Azure Active Directory 左邊瀏覽功能表，按一下 [企業應用程式]。</span><span class="sxs-lookup"><span data-stu-id="316a4-121">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="316a4-122">按一下 [所有應用程式]，以檢視所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="316a4-122">click **All Applications** to view a list of all your applications.</span></span>

6.  <span data-ttu-id="316a4-123">**搜尋**相關應用程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="316a4-123">**Search** for the name of the application in question.</span></span>

7.  <span data-ttu-id="316a4-124">按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="316a4-124">click **Users and groups**.</span></span>

8.  <span data-ttu-id="316a4-125">檢查使用者是否已指派至應用程式。</span><span class="sxs-lookup"><span data-stu-id="316a4-125">Check to see if your user is assigned to the application.</span></span>

  * <span data-ttu-id="316a4-126">如果您想要從應用程式移除使用者，請**按一下使用者的資料列**，然後選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="316a4-126">If you want to remove the user from the application, **click the row** of the user and select **delete**.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-to-the-application"></a><span data-ttu-id="316a4-127">檢查使用者是否獲得應用程式相關的授權</span><span class="sxs-lookup"><span data-stu-id="316a4-127">Check if a user is under a license related to the application</span></span>

<span data-ttu-id="316a4-128">若要檢查指派給使用者的授權，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="316a4-128">To check a user’s assigned licenses, follow the steps below:</span></span>

1.  <span data-ttu-id="316a4-129">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="316a4-129">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="316a4-130">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="316a4-130">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="316a4-131">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="316a4-131">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="316a4-132">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="316a4-132">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="316a4-133">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="316a4-133">click **All users**.</span></span>

6.  <span data-ttu-id="316a4-134">**搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。</span><span class="sxs-lookup"><span data-stu-id="316a4-134">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="316a4-135">按一下 [授權]，以查看目前已指派給使用者的授權。</span><span class="sxs-lookup"><span data-stu-id="316a4-135">click **Licenses** to see which licenses the user currently has assigned.</span></span>

   * <span data-ttu-id="316a4-136">如果使用者已指派至 Office 授權，這會讓第一方 Office 應用程式出現在使用者的存取面板上。</span><span class="sxs-lookup"><span data-stu-id="316a4-136">If the user is assigned to an Office license this enable First Party Office applications to appear on the user’s Access Panel.</span></span>

## <a name="problems-related-to-assigning-applications-to-groups"></a><span data-ttu-id="316a4-137">指派應用程式給群組的相關問題</span><span class="sxs-lookup"><span data-stu-id="316a4-137">Problems related to assigning applications to groups</span></span>

<span data-ttu-id="316a4-138">使用者可能因為屬於已被指派應用程式的群組，所以能在存取面板上看見該應用程式。</span><span class="sxs-lookup"><span data-stu-id="316a4-138">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned the application.</span></span> <span data-ttu-id="316a4-139">以下是一些檢查方法：</span><span class="sxs-lookup"><span data-stu-id="316a4-139">Below are some ways to check:</span></span>

-   [<span data-ttu-id="316a4-140">檢查使用者的群組成員資格</span><span class="sxs-lookup"><span data-stu-id="316a4-140">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="316a4-141">檢查使用者是否屬於指派至授權的群組</span><span class="sxs-lookup"><span data-stu-id="316a4-141">Check if a user is a member of a group assigned to a license</span></span>](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="316a4-142">檢查使用者的群組成員資格</span><span class="sxs-lookup"><span data-stu-id="316a4-142">Check a user’s group memberships</span></span>

<span data-ttu-id="316a4-143">若要檢查群組的成員資格，請依照下列步驟執行：</span><span class="sxs-lookup"><span data-stu-id="316a4-143">To check a group’s membership, follow the steps below:</span></span>

1.  <span data-ttu-id="316a4-144">開啟 [**Azure 入口網站**](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="316a4-144">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="316a4-145">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="316a4-145">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="316a4-146">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="316a4-146">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="316a4-147">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="316a4-147">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="316a4-148">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="316a4-148">click **All users**.</span></span>

6.  <span data-ttu-id="316a4-149">**搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。</span><span class="sxs-lookup"><span data-stu-id="316a4-149">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="316a4-150">按一下 [群組]。</span><span class="sxs-lookup"><span data-stu-id="316a4-150">click **Groups.**</span></span>

8.  <span data-ttu-id="316a4-151">檢查使用者是否屬於已指派至應用程式的群組。</span><span class="sxs-lookup"><span data-stu-id="316a4-151">Check to see if your user is part of a Group assigned to the application.</span></span>

   * <span data-ttu-id="316a4-152">如果您想要從群組移除使用者，請**按一下群組的資料列**，然後選取 [刪除]。</span><span class="sxs-lookup"><span data-stu-id="316a4-152">If you want to remove the user from the group, **click the row** of the group and select delete.</span></span>

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-to-a-license"></a><span data-ttu-id="316a4-153">檢查使用者是否屬於指派至授權的群組</span><span class="sxs-lookup"><span data-stu-id="316a4-153">Check if a user is a member of a group assigned to a license</span></span>

1.  <span data-ttu-id="316a4-154">開啟 [Azure 入口網站](https://portal.azure.com/)，以**全域管理員**身分登入。</span><span class="sxs-lookup"><span data-stu-id="316a4-154">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="316a4-155">按一下左邊主瀏覽功能表底部的 [更多服務]，以開啟 [Azure Active Directory 延伸模組]。</span><span class="sxs-lookup"><span data-stu-id="316a4-155">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="316a4-156">在篩選搜尋方塊中輸入 **“Azure Active Directory**”，然後選取 [Azure Active Directory] 項目。</span><span class="sxs-lookup"><span data-stu-id="316a4-156">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="316a4-157">按一下瀏覽功能表中的 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="316a4-157">click **Users and groups** in the navigation menu.</span></span>

5.  <span data-ttu-id="316a4-158">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="316a4-158">click **All users**.</span></span>

6.  <span data-ttu-id="316a4-159">**搜尋**您感興趣的使用者，**按一下資料列**選取該使用者。</span><span class="sxs-lookup"><span data-stu-id="316a4-159">**Search** for the user you are interested in and **click the row** to select.</span></span>

7.  <span data-ttu-id="316a4-160">按一下 [群組]。</span><span class="sxs-lookup"><span data-stu-id="316a4-160">click **Groups.**</span></span>

8.  <span data-ttu-id="316a4-161">按一下特定群組的資料列。</span><span class="sxs-lookup"><span data-stu-id="316a4-161">click the row of a specific group.</span></span>

9.  <span data-ttu-id="316a4-162">按一下 [授權]，以查看已指派給群組的授權。</span><span class="sxs-lookup"><span data-stu-id="316a4-162">click **Licenses** to see which licenses the group has assigned to it.</span></span>

  * <span data-ttu-id="316a4-163">如果群組已指派至 Office 授權，這可能會讓某些第一方 Office 應用程式出現在使用者的存取面板上。</span><span class="sxs-lookup"><span data-stu-id="316a4-163">If the group is assigned to an Office license this may enable certain First Party Office applications to appear on the user’s Access Panel.</span></span>


## <a name="if-these-troubleshooting-steps-do-not-the-resolve-the-issue"></a><span data-ttu-id="316a4-164">如果這些疑難排解步驟無法解決問題</span><span class="sxs-lookup"><span data-stu-id="316a4-164">If these troubleshooting steps do not the resolve the issue</span></span>

<span data-ttu-id="316a4-165">使用下列資訊 (若有的話) 開啟支援票證︰</span><span class="sxs-lookup"><span data-stu-id="316a4-165">open a support ticket with the following information if available:</span></span>

-   <span data-ttu-id="316a4-166">相互關聯錯誤 ID</span><span class="sxs-lookup"><span data-stu-id="316a4-166">Correlation error ID</span></span>

-   <span data-ttu-id="316a4-167">UPN (使用者電子郵件地址)</span><span class="sxs-lookup"><span data-stu-id="316a4-167">UPN (user email address)</span></span>

-   <span data-ttu-id="316a4-168">租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="316a4-168">Tenant ID</span></span>

-   <span data-ttu-id="316a4-169">瀏覽器類型</span><span class="sxs-lookup"><span data-stu-id="316a4-169">Browser type</span></span>

-   <span data-ttu-id="316a4-170">錯誤發生期間的時區和時間/時間範圍</span><span class="sxs-lookup"><span data-stu-id="316a4-170">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="316a4-171">Fiddler 追蹤</span><span class="sxs-lookup"><span data-stu-id="316a4-171">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="316a4-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="316a4-172">Next steps</span></span>
[<span data-ttu-id="316a4-173">使用 Azure Active Directory 管理應用程式</span><span class="sxs-lookup"><span data-stu-id="316a4-173">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
