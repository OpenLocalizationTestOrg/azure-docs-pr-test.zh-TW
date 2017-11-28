---
title: "新使用者 tooAzure aaaAdd Active Directory |Microsoft 文件"
description: "說明如何 tooadd 新使用者或變更 Azure Active Directory 中的使用者資訊。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: e3673727-6bec-4fdc-87a4-d65b213c4c3c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 72f67ad41022fd19fd94c8e1301943b0db1e57bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-tooazure-active-directory"></a><span data-ttu-id="2b79b-103">新增使用者或與 Microsoft 帳戶 tooAzure Active Directory 使用者</span><span class="sxs-lookup"><span data-stu-id="2b79b-103">Add new users or users with Microsoft accounts tooAzure Active Directory</span></span>
<span data-ttu-id="2b79b-104">新增使用者 toopopulate 您的目錄。</span><span class="sxs-lookup"><span data-stu-id="2b79b-104">Add users toopopulate your directory.</span></span> <span data-ttu-id="2b79b-105">這篇文章說明如何 tooadd 新使用者在您的組織，以及如何 tooadd 使用者具有 Microsoft 帳戶。</span><span class="sxs-lookup"><span data-stu-id="2b79b-105">This article explains how tooadd new users in your organization, and how tooadd users who have Microsoft accounts.</span></span> <span data-ttu-id="2b79b-106">如需新增來自 Azure Active Directory 中其他目錄之使用者或是來自合作夥伴公司之使用者的詳細資訊，請參閱 [新增來自 Azure Active Directory 中其他目錄或合作夥伴公司的使用者](active-directory-create-users-external.md)。</span><span class="sxs-lookup"><span data-stu-id="2b79b-106">For more information about adding users from other directories in Azure Active Directory or adding users from partner companies, see [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md).</span></span> <span data-ttu-id="2b79b-107">新增的使用者時，不需要系統管理員權限，根據預設，但您可以在任何時間指派角色 toothem。</span><span class="sxs-lookup"><span data-stu-id="2b79b-107">Added users don't have administrator permissions by default, but you can assign roles toothem at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b79b-108">Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="2b79b-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="2b79b-109">針對如何 tooadd hello Azure AD 系統管理中心中的使用者看到[加入新使用者 tooAzure Active Directory](active-directory-users-create-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="2b79b-109">For how tooadd a user in hello Azure AD admin center, see [Add new users tooAzure Active Directory](active-directory-users-create-azure-portal.md).</span></span>

## <a name="add-a-user"></a><span data-ttu-id="2b79b-110">新增使用者</span><span class="sxs-lookup"><span data-stu-id="2b79b-110">Add a user</span></span>
1. <span data-ttu-id="2b79b-111">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)hello 目錄的全域管理員的帳戶。</span><span class="sxs-lookup"><span data-stu-id="2b79b-111">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="2b79b-112">選取**Active Directory**，然後選取您的組織目錄中的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="2b79b-112">Select **Active Directory**, and then select hello name of your organization directory.</span></span>
3. <span data-ttu-id="2b79b-113">選取 hello**使用者**索引標籤，然後 hello 命令列中，選取**新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="2b79b-113">Select hello **Users** tab, and then, in hello command bar, select **Add User**.</span></span>
4. <span data-ttu-id="2b79b-114">在 hello**告訴我們這位使用者**頁面的 **使用者類型**，選取：</span><span class="sxs-lookup"><span data-stu-id="2b79b-114">On hello **Tell us about this user** page, under **Type of user**, select either:</span></span>

   * <span data-ttu-id="2b79b-115">**您組織中的新使用者** – 在您的目錄中新增使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="2b79b-115">**New user in your organization** – adds a new user account in your directory.</span></span>
   * <span data-ttu-id="2b79b-116">**使用現有的 Microsoft 帳戶使用者**– 新增的現有 Microsoft 消費者帳戶 tooyour 目錄 （例如 Outlook 帳戶）</span><span class="sxs-lookup"><span data-stu-id="2b79b-116">**User with an existing Microsoft account** – adds an existing Microsoft consumer account tooyour directory (for example, an Outlook account)</span></span>
5. <span data-ttu-id="2b79b-117">根據 [使用者類型] 輸入使用者名稱 (適用於新使用者) 或電子郵件地址 (適用於具有 Microsoft 帳戶的使用者)。</span><span class="sxs-lookup"><span data-stu-id="2b79b-117">Depending on **Type of user**, enter a user name (for new user) or an email address (for a user with a Microsoft account).</span></span>
6. <span data-ttu-id="2b79b-118">在 hello 使用者**設定檔**頁面上，提供第一個和最後一個名稱、 使用者易記的名稱，以及使用者角色的 hello**角色**清單。</span><span class="sxs-lookup"><span data-stu-id="2b79b-118">On hello user **Profile** page, provide a first and last name, a user-friendly name, and a user role from hello **Roles** list.</span></span> <span data-ttu-id="2b79b-119">如需有關使用者和系統管理員角色的詳細資訊，請參閱 [在 Azure AD 中指派系統管理員角色](active-directory-assign-admin-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="2b79b-119">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span> <span data-ttu-id="2b79b-120">指定是否太**啟用 Multi-factor Authentication** hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="2b79b-120">Specify whether too**Enable Multi-Factor Authentication** for hello user.</span></span>
7. <span data-ttu-id="2b79b-121">在 hello**取得暫時密碼**頁面上，選取**建立**。</span><span class="sxs-lookup"><span data-stu-id="2b79b-121">On hello **Get temporary password** page, select **Create**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2b79b-122">如果您的組織使用多個網域，您應該了解 hello 新增使用者帳戶時，下列問題：</span><span class="sxs-lookup"><span data-stu-id="2b79b-122">If your organization uses more than one domain, you should know about hello following issues when you add a user account:</span></span>
>
> * <span data-ttu-id="2b79b-123">tooadd 使用者帳戶與 hello 相同的使用者主體名稱 (UPN) 跨網域，**第一個**，例如新增geoffgrisso@contoso.onmicrosoft.com，**後面** geoffgrisso@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="2b79b-123">tooadd user accounts with hello same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.</span></span>
> * <span data-ttu-id="2b79b-124">請「勿」先新增 geoffgrisso@contoso.com，再新增 geoffgrisso@contoso.onmicrosoft.com。這個順序很重要，而且可以麻煩 tooundo。</span><span class="sxs-lookup"><span data-stu-id="2b79b-124">**Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com. This order is important, and can be cumbersome tooundo.</span></span>
>
>

## <a name="change-user-information"></a><span data-ttu-id="2b79b-125">變更使用者資訊</span><span class="sxs-lookup"><span data-stu-id="2b79b-125">Change user information</span></span>
<span data-ttu-id="2b79b-126">您可以變更任何使用者屬性除了 hello 物件識別碼。</span><span class="sxs-lookup"><span data-stu-id="2b79b-126">You can change any user attribute except for hello object ID.</span></span>

1. <span data-ttu-id="2b79b-127">開啟您的目錄。</span><span class="sxs-lookup"><span data-stu-id="2b79b-127">Open your directory.</span></span>
2. <span data-ttu-id="2b79b-128">選取 hello**使用者**索引標籤，然後再選取 hello 顯示名稱 hello 想 toochange 使用者。</span><span class="sxs-lookup"><span data-stu-id="2b79b-128">Select hello **Users** tab, and then select hello display name of hello user you want toochange.</span></span>
3. <span data-ttu-id="2b79b-129">完成您的變更，然後按一下儲存 。</span><span class="sxs-lookup"><span data-stu-id="2b79b-129">Complete your changes, and then click **Save**.</span></span>

<span data-ttu-id="2b79b-130">如果您要變更的 hello 使用者會與您的內部部署 Active Directory 服務同步處理，您無法變更使用此程序的 hello 使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="2b79b-130">If hello user that you're changing is synchronized with your on-premises Active Directory service, you can't change hello user information using this procedure.</span></span> <span data-ttu-id="2b79b-131">toochange hello 使用者，使用您在內部部署 Active Directory 管理工具。</span><span class="sxs-lookup"><span data-stu-id="2b79b-131">toochange hello user, use your on-premises Active Directory management tools.</span></span>

## <a name="guest-user-management-and-limitations"></a><span data-ttu-id="2b79b-132">來賓使用者管理和限制</span><span class="sxs-lookup"><span data-stu-id="2b79b-132">Guest user management and limitations</span></span>
<span data-ttu-id="2b79b-133">Guest 帳戶是從已受邀的 tooyour 目錄 tooaccess SharePoint 文件、 應用程式或其他 Azure 資源的其他目錄的使用者。</span><span class="sxs-lookup"><span data-stu-id="2b79b-133">Guest accounts are users from other directories who were invited tooyour directory tooaccess SharePoint documents, applications, or other Azure resources.</span></span> <span data-ttu-id="2b79b-134">來賓帳戶在您的目錄中具有其基礎的 UserType 屬性設定太"Guest。"</span><span class="sxs-lookup"><span data-stu-id="2b79b-134">A guest account in your directory has its underlying UserType attribute set too"Guest."</span></span> <span data-ttu-id="2b79b-135">一般使用者 （具體而言，您的目錄成員） 具有 hello UserType 屬性 「 成員 」。</span><span class="sxs-lookup"><span data-stu-id="2b79b-135">Regular users (specifically, members of your directory) have hello UserType attribute "Member."</span></span>

<span data-ttu-id="2b79b-136">來賓 hello 目錄中有一組有限的權限。</span><span class="sxs-lookup"><span data-stu-id="2b79b-136">Guests have a limited set of rights in hello directory.</span></span> <span data-ttu-id="2b79b-137">這些權限限制 hello 有關客體 toodiscover hello 目錄中的其他使用者的能力。</span><span class="sxs-lookup"><span data-stu-id="2b79b-137">These rights limit hello ability for Guests toodiscover information about other users in hello directory.</span></span> <span data-ttu-id="2b79b-138">不過，來賓使用者仍然可以互動 hello 使用者與群組正努力 hello 資源相關聯。</span><span class="sxs-lookup"><span data-stu-id="2b79b-138">However, guest users can still interact with hello users and groups associated with hello resources they're working on.</span></span> <span data-ttu-id="2b79b-139">來賓使用者可以：</span><span class="sxs-lookup"><span data-stu-id="2b79b-139">Guest users can:</span></span>

* <span data-ttu-id="2b79b-140">其他使用者和群組指派給這些是 Azure 訂用帳戶 toowhich 相關聯，請參閱</span><span class="sxs-lookup"><span data-stu-id="2b79b-140">See other users and groups associated with an Azure subscription toowhich they're assigned</span></span>
* <span data-ttu-id="2b79b-141">請參閱其所屬的群組 toowhich hello 成員</span><span class="sxs-lookup"><span data-stu-id="2b79b-141">See hello members of groups toowhich they belong</span></span>
* <span data-ttu-id="2b79b-142">查閱 hello 目錄中的其他使用者知道 hello 使用者 hello 完整電子郵件地址</span><span class="sxs-lookup"><span data-stu-id="2b79b-142">Look up other users in hello directory, if they know hello full email address of hello user</span></span>
* <span data-ttu-id="2b79b-143">請參閱僅提供有限的查閱-有限的 toodisplay 名稱、 電子郵件地址、 使用者主要名稱 (UPN) 和縮圖相片的 hello 使用者屬性</span><span class="sxs-lookup"><span data-stu-id="2b79b-143">See only a limited set of attributes of hello users they look up--limited toodisplay name, email address, user principal name (UPN), and thumbnail photo</span></span>
* <span data-ttu-id="2b79b-144">取得一份 hello 目錄中的已驗證網域</span><span class="sxs-lookup"><span data-stu-id="2b79b-144">Get a list of verified domains in hello directory</span></span>
* <span data-ttu-id="2b79b-145">同意 tooapplications，授與他們 hello 相同目錄中有成員的存取權</span><span class="sxs-lookup"><span data-stu-id="2b79b-145">Consent tooapplications, granting them hello same access that Members have in your directory</span></span>

## <a name="set-guest-user-access-policies"></a><span data-ttu-id="2b79b-146">設定來賓使用者存取原則</span><span class="sxs-lookup"><span data-stu-id="2b79b-146">Set guest user access policies</span></span>
<span data-ttu-id="2b79b-147">hello**設定**目錄的索引標籤包含 guest 使用者的選項 toocontrol 存取。</span><span class="sxs-lookup"><span data-stu-id="2b79b-147">hello **Configure** tab of a directory includes options toocontrol access for guest users.</span></span> <span data-ttu-id="2b79b-148">這些選項只可以由目錄全域管理員在 Azure 傳統入口網站中進行變更。</span><span class="sxs-lookup"><span data-stu-id="2b79b-148">These options can be changed only in Azure classic portal by a directory global administrator.</span></span> <span data-ttu-id="2b79b-149">目前沒有透過 PowerShell 或 API 的方法。</span><span class="sxs-lookup"><span data-stu-id="2b79b-149">Currently, there's no PowerShell or API method.</span></span>

<span data-ttu-id="2b79b-150">tooopen hello**設定**] 索引標籤中 hello Azure 傳統入口網站中，選取**Active Directory**，然後選取 [hello hello 目錄名稱。</span><span class="sxs-lookup"><span data-stu-id="2b79b-150">tooopen hello **Configure** tab in hello Azure classic portal, select **Active Directory**, and then select hello name of hello directory.</span></span>

![在 Azure Active Directory 中設定索引標籤][1]

<span data-ttu-id="2b79b-152">然後您可以編輯 guest 使用者的 hello 選項 toocontrol 存取。</span><span class="sxs-lookup"><span data-stu-id="2b79b-152">Then you can edit hello options toocontrol access for guest users.</span></span>

![來賓使用者的存取控制選項][2]

## <a name="whats-next"></a><span data-ttu-id="2b79b-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2b79b-154">What's next</span></span>
* [<span data-ttu-id="2b79b-155">新增來自 Azure Active Directory 中其他目錄或合作夥伴公司的使用者</span><span class="sxs-lookup"><span data-stu-id="2b79b-155">Add users from other directories or partner companies in Azure Active Directory</span></span>](active-directory-create-users-external.md)
* [<span data-ttu-id="2b79b-156">管理 Azure AD</span><span class="sxs-lookup"><span data-stu-id="2b79b-156">Administering Azure AD</span></span>](active-directory-administer.md)
* [<span data-ttu-id="2b79b-157">在 Azure AD 中管理密碼</span><span class="sxs-lookup"><span data-stu-id="2b79b-157">Manage passwords in Azure AD</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="2b79b-158">在 Azure AD 中管理群組</span><span class="sxs-lookup"><span data-stu-id="2b79b-158">Manage groups in Azure AD</span></span>](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
