---
title: "hello 存取面板上出現 aaaHow 應用程式 |Microsoft 文件"
description: "應用程式會出現在 hello 存取面板進行疑難排解"
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
ms.openlocfilehash: 14ee732c4ed5260cba878e949cf9d90877aee67e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-applications-appear-on-hello-access-panel"></a><span data-ttu-id="e9392-103">應用程式如何 hello 存取面板上顯示</span><span class="sxs-lookup"><span data-stu-id="e9392-103">How applications appear on hello access panel</span></span>

<span data-ttu-id="e9392-104">hello 存取面板是網頁型的入口網站，可讓使用者使用工作或學校帳戶，Azure Active Directory (Azure AD) tooview 並啟動雲端架構應用程式中的 hello Azure AD 系統管理員已授與它們存取權。</span><span class="sxs-lookup"><span data-stu-id="e9392-104">hello Access Panel is a web-based portal which enables a user with a work or school account in Azure Active Directory (Azure AD) tooview and start cloud-based applications that hello Azure AD administrator has granted them access to.</span></span> <span data-ttu-id="e9392-105">這些應用程式會代表 hello Azure AD 入口網站中的 hello 使用者設定。</span><span class="sxs-lookup"><span data-stu-id="e9392-105">These applications are configured on behalf of hello user in hello Azure AD portal.</span></span> <span data-ttu-id="e9392-106">hello 系統管理員可以佈建 hello 應用程式 toohello 使用者直接或 tooa 群組的使用者是導致 hello hello 使用者的存取面板上顯示的應用程式的一部分。</span><span class="sxs-lookup"><span data-stu-id="e9392-106">hello admin can provision hello application toohello user directly or tooa group a user is part of resulting in hello application appearing on hello user’s Access Panel.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="e9392-107">一般會先發出 toocheck</span><span class="sxs-lookup"><span data-stu-id="e9392-107">General issues toocheck first</span></span>

-   <span data-ttu-id="e9392-108">如果應用程式就已從使用者或群組 hello 使用者的成員，toosign 入和登出再試一次到 hello 使用者的存取面板後幾分鐘的時間 toosee 如果 hello 應用程式中移除。</span><span class="sxs-lookup"><span data-stu-id="e9392-108">If an application was just removed from a user or group hello user is a member of, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello application is removed.</span></span>

-   <span data-ttu-id="e9392-109">授權就已從使用者或群組 hello 使用者隸屬這可能需要很長的時間，取決於 hello 大小和複雜度所做的變更 toobe hello 群組。</span><span class="sxs-lookup"><span data-stu-id="e9392-109">If a license was just removed from a user or group hello user is a member of this may take a long time, depending on hello size and complexity of hello group for changes toobe made.</span></span> <span data-ttu-id="e9392-110">允許額外的時間才能登入存取面板 hello。</span><span class="sxs-lookup"><span data-stu-id="e9392-110">Allow for extra time before signing into hello Access Panel.</span></span>

## <a name="problems-related-tooassigning-applications-toousers"></a><span data-ttu-id="e9392-111">問題相關的 tooassigning 應用程式 toousers</span><span class="sxs-lookup"><span data-stu-id="e9392-111">Problems related tooassigning applications toousers</span></span>

<span data-ttu-id="e9392-112">使用者會看見應用程式存取面板上因為其已被先前指派 tooit。</span><span class="sxs-lookup"><span data-stu-id="e9392-112">A user may be seeing an application on their Access Panel because they had been previously assigned tooit.</span></span> <span data-ttu-id="e9392-113">以下是一些方式 toocheck:</span><span class="sxs-lookup"><span data-stu-id="e9392-113">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="e9392-114">檢查 toohello 應用程式時，是否要指派使用者</span><span class="sxs-lookup"><span data-stu-id="e9392-114">Check if a user is assigned toohello application</span></span>](#check-if-a-user-is-assigned-to-the-application)

-   [<span data-ttu-id="e9392-115">檢查是否授權使用者相關 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e9392-115">Check if a user is under a license related toohello application</span></span>](#check-if-a-user-is-under-a-license-related-to-the-application)


### <a name="check-if-a-user-is-assigned-toohello-application"></a><span data-ttu-id="e9392-116">檢查 toohello 應用程式時，是否要指派使用者</span><span class="sxs-lookup"><span data-stu-id="e9392-116">Check if a user is assigned toohello application</span></span>

<span data-ttu-id="e9392-117">toocheck 如果使用者被指派 toohello 應用程式，請遵循 hello 執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="e9392-117">toocheck if a user is assigned toohello application, follow hello steps below:</span></span>

1.  <span data-ttu-id="e9392-118">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="e9392-118">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="e9392-119">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="e9392-119">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e9392-120">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="e9392-120">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e9392-121">按一下**企業應用程式**從 hello Azure Active Directory 左導覽功能表。</span><span class="sxs-lookup"><span data-stu-id="e9392-121">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="e9392-122">按一下**所有應用程式**tooview 所有應用程式的清單。</span><span class="sxs-lookup"><span data-stu-id="e9392-122">click **All Applications** tooview a list of all your applications.</span></span>

6.  <span data-ttu-id="e9392-123">**搜尋**hello hello 有問題的應用程式名稱。</span><span class="sxs-lookup"><span data-stu-id="e9392-123">**Search** for hello name of hello application in question.</span></span>

7.  <span data-ttu-id="e9392-124">按一下 [使用者和群組]。</span><span class="sxs-lookup"><span data-stu-id="e9392-124">click **Users and groups**.</span></span>

8.  <span data-ttu-id="e9392-125">如果您的使用者被指派 toohello 應用程式，請檢查 toosee。</span><span class="sxs-lookup"><span data-stu-id="e9392-125">Check toosee if your user is assigned toohello application.</span></span>

  * <span data-ttu-id="e9392-126">如果您想從 hello 應用程式、 tooremove hello 使用者**按一下 hello 列**hello 使用者，然後選取**刪除**。</span><span class="sxs-lookup"><span data-stu-id="e9392-126">If you want tooremove hello user from hello application, **click hello row** of hello user and select **delete**.</span></span>

### <a name="check-if-a-user-is-under-a-license-related-toohello-application"></a><span data-ttu-id="e9392-127">檢查是否授權使用者相關 toohello 應用程式</span><span class="sxs-lookup"><span data-stu-id="e9392-127">Check if a user is under a license related toohello application</span></span>

<span data-ttu-id="e9392-128">toocheck 使用者的指派授權，後續 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="e9392-128">toocheck a user’s assigned licenses, follow hello steps below:</span></span>

1.  <span data-ttu-id="e9392-129">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="e9392-129">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="e9392-130">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="e9392-130">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e9392-131">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="e9392-131">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e9392-132">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="e9392-132">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="e9392-133">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="e9392-133">click **All users**.</span></span>

6.  <span data-ttu-id="e9392-134">**搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="e9392-134">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="e9392-135">按一下**授權**toosee 授權 hello 使用者目前已指派。</span><span class="sxs-lookup"><span data-stu-id="e9392-135">click **Licenses** toosee which licenses hello user currently has assigned.</span></span>

   * <span data-ttu-id="e9392-136">如果這啟用第一個合作對象 Office 應用程式 tooappear tooan Office 授權指派給 hello 使用者 hello 使用者的存取面板。</span><span class="sxs-lookup"><span data-stu-id="e9392-136">If hello user is assigned tooan Office license this enable First Party Office applications tooappear on hello user’s Access Panel.</span></span>

## <a name="problems-related-tooassigning-applications-toogroups"></a><span data-ttu-id="e9392-137">問題相關的 tooassigning 應用程式 toogroups</span><span class="sxs-lookup"><span data-stu-id="e9392-137">Problems related tooassigning applications toogroups</span></span>

<span data-ttu-id="e9392-138">使用者會看見應用程式存取面板上因為它們已被指派 hello 應用程式群組的一部分。</span><span class="sxs-lookup"><span data-stu-id="e9392-138">A user may be seeing an application on their Access Panel because they are part of a group that has been assigned hello application.</span></span> <span data-ttu-id="e9392-139">以下是一些方式 toocheck:</span><span class="sxs-lookup"><span data-stu-id="e9392-139">Below are some ways toocheck:</span></span>

-   [<span data-ttu-id="e9392-140">檢查使用者的群組成員資格</span><span class="sxs-lookup"><span data-stu-id="e9392-140">Check a user’s group memberships</span></span>](#check-a-users-group-memberships)

-   [<span data-ttu-id="e9392-141">檢查使用者是否 tooa 授權指派給群組的成員</span><span class="sxs-lookup"><span data-stu-id="e9392-141">Check if a user is a member of a group assigned tooa license</span></span>](#check-if-a-user-is-a-member-of-a-group-assigned-to-a-license)

### <a name="check-a-users-group-memberships"></a><span data-ttu-id="e9392-142">檢查使用者的群組成員資格</span><span class="sxs-lookup"><span data-stu-id="e9392-142">Check a user’s group memberships</span></span>

<span data-ttu-id="e9392-143">toocheck 群組的成員資格，後續 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="e9392-143">toocheck a group’s membership, follow hello steps below:</span></span>

1.  <span data-ttu-id="e9392-144">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="e9392-144">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="e9392-145">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="e9392-145">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e9392-146">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="e9392-146">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e9392-147">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="e9392-147">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="e9392-148">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="e9392-148">click **All users**.</span></span>

6.  <span data-ttu-id="e9392-149">**搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="e9392-149">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="e9392-150">按一下 [群組]。</span><span class="sxs-lookup"><span data-stu-id="e9392-150">click **Groups.**</span></span>

8.  <span data-ttu-id="e9392-151">如果您的使用者屬於群組的核取 toosee 指派 toohello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e9392-151">Check toosee if your user is part of a Group assigned toohello application.</span></span>

   * <span data-ttu-id="e9392-152">如果您想從 hello 群組 tooremove hello 使用者**按一下 hello 列**hello 群組和選取的刪除。</span><span class="sxs-lookup"><span data-stu-id="e9392-152">If you want tooremove hello user from hello group, **click hello row** of hello group and select delete.</span></span>

### <a name="check-if-a-user-is-a-member-of-a-group-assigned-tooa-license"></a><span data-ttu-id="e9392-153">檢查使用者是否 tooa 授權指派給群組的成員</span><span class="sxs-lookup"><span data-stu-id="e9392-153">Check if a user is a member of a group assigned tooa license</span></span>

1.  <span data-ttu-id="e9392-154">開啟 hello [ **Azure 入口網站**](https://portal.azure.com/)身分登入和**全域管理員。**</span><span class="sxs-lookup"><span data-stu-id="e9392-154">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="e9392-155">開啟 hello **Azure Active Directory 延伸模組**按一下**更多服務**在 hello hello 主要左導覽功能表底部。</span><span class="sxs-lookup"><span data-stu-id="e9392-155">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="e9392-156">在中輸入**「 Azure Active Directory**"hello 篩選搜尋方塊和選取 hello **Azure Active Directory**項目。</span><span class="sxs-lookup"><span data-stu-id="e9392-156">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="e9392-157">按一下**使用者和群組**hello 瀏覽功能表中。</span><span class="sxs-lookup"><span data-stu-id="e9392-157">click **Users and groups** in hello navigation menu.</span></span>

5.  <span data-ttu-id="e9392-158">按一下 [所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="e9392-158">click **All users**.</span></span>

6.  <span data-ttu-id="e9392-159">**搜尋**hello 您感興趣的使用者和**按一下 hello 列**tooselect。</span><span class="sxs-lookup"><span data-stu-id="e9392-159">**Search** for hello user you are interested in and **click hello row** tooselect.</span></span>

7.  <span data-ttu-id="e9392-160">按一下 [群組]。</span><span class="sxs-lookup"><span data-stu-id="e9392-160">click **Groups.**</span></span>

8.  <span data-ttu-id="e9392-161">按一下 特定群組的 hello 資料列。</span><span class="sxs-lookup"><span data-stu-id="e9392-161">click hello row of a specific group.</span></span>

9.  <span data-ttu-id="e9392-162">按一下**授權**toosee 授權 hello 群組已指派 tooit。</span><span class="sxs-lookup"><span data-stu-id="e9392-162">click **Licenses** toosee which licenses hello group has assigned tooit.</span></span>

  * <span data-ttu-id="e9392-163">如果這可能會讓特定的第一個合作對象 Office 應用程式 tooappear tooan Office 授權指派給 hello 群組 hello 使用者的存取面板。</span><span class="sxs-lookup"><span data-stu-id="e9392-163">If hello group is assigned tooan Office license this may enable certain First Party Office applications tooappear on hello user’s Access Panel.</span></span>


## <a name="if-these-troubleshooting-steps-do-not-hello-resolve-hello-issue"></a><span data-ttu-id="e9392-164">如果不執行 hello 這些疑難排解步驟解決 hello 問題</span><span class="sxs-lookup"><span data-stu-id="e9392-164">If these troubleshooting steps do not hello resolve hello issue</span></span>

<span data-ttu-id="e9392-165">開啟支援票證以 hello 如果有的話，下列資訊：</span><span class="sxs-lookup"><span data-stu-id="e9392-165">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="e9392-166">相互關聯錯誤 ID</span><span class="sxs-lookup"><span data-stu-id="e9392-166">Correlation error ID</span></span>

-   <span data-ttu-id="e9392-167">UPN (使用者電子郵件地址)</span><span class="sxs-lookup"><span data-stu-id="e9392-167">UPN (user email address)</span></span>

-   <span data-ttu-id="e9392-168">租用戶識別碼</span><span class="sxs-lookup"><span data-stu-id="e9392-168">Tenant ID</span></span>

-   <span data-ttu-id="e9392-169">瀏覽器類型</span><span class="sxs-lookup"><span data-stu-id="e9392-169">Browser type</span></span>

-   <span data-ttu-id="e9392-170">錯誤發生期間的時區和時間/時間範圍</span><span class="sxs-lookup"><span data-stu-id="e9392-170">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="e9392-171">Fiddler 追蹤</span><span class="sxs-lookup"><span data-stu-id="e9392-171">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9392-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e9392-172">Next steps</span></span>
[<span data-ttu-id="e9392-173">使用 Azure Active Directory 管理應用程式</span><span class="sxs-lookup"><span data-stu-id="e9392-173">Managing Applications with Azure Active Directory</span></span>](active-directory-enable-sso-scenario.md)
