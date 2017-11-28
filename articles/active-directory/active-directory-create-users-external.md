---
title: "從其他目錄或 Azure Active Directory 中的夥伴公司 aaaAdd 使用者 |Microsoft 文件"
description: "說明如何 tooadd 使用者或變更在 Azure Active Directory，包括外部和來賓使用者的使用者資訊。"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 564a04ec-53c1-470b-9ab9-f3db57da0a89
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/25/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 92099e5792365c307b0f3d4f2dff5dd8424aeab4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-users-from-other-directories-or-partner-companies-in-azure-active-directory"></a><span data-ttu-id="c8309-103">新增來自 Azure Active Directory 中其他目錄或合作夥伴公司的使用者</span><span class="sxs-lookup"><span data-stu-id="c8309-103">Add users from other directories or partner companies in Azure Active Directory</span></span>

<span data-ttu-id="c8309-104">這篇文章說明如何從 Azure Active Directory 中的其他目錄 tooadd 使用者或從夥伴公司中新增使用者。</span><span class="sxs-lookup"><span data-stu-id="c8309-104">This article explains how tooadd users from other directories in Azure Active Directory or add users from partner companies.</span></span> <span data-ttu-id="c8309-105">如需在組織中，加入新使用者以及加入具有 Microsoft 帳戶的使用者資訊，請參閱[加入新使用者 tooAzure Active Directory](active-directory-create-users.md)。</span><span class="sxs-lookup"><span data-stu-id="c8309-105">For information about adding new users in your organization, and adding users who have Microsoft accounts, see [Add new users tooAzure Active Directory](active-directory-create-users.md).</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c8309-106">Microsoft 建議您管理 Azure AD 使用 hello [Azure AD 系統管理中心](https://aad.portal.azure.com)hello 在 Azure 入口網站，而不是使用 hello 這個文件中參考的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="c8309-106">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="c8309-107">如何置 tooadd B2B 共同作業 guest 使用者，在 hello Azure AD 系統管理員中的，請參閱[什麼是 Azure AD B2B 共同作業？](active-directory-b2b-what-is-azure-ad-b2b.md)</span><span class="sxs-lookup"><span data-stu-id="c8309-107">For how tooadd B2B collaboration guest users in hello Azure AD admin center, see [What is Azure AD B2B collaboration?](active-directory-b2b-what-is-azure-ad-b2b.md)</span></span>

<span data-ttu-id="c8309-108">新增的使用者時，不需要系統管理員權限，根據預設，但您可以在任何時間指派角色 toothem。</span><span class="sxs-lookup"><span data-stu-id="c8309-108">Added users don't have administrator permissions by default, but you can assign roles toothem at any time.</span></span>

## <a name="add-a-user"></a><span data-ttu-id="c8309-109">新增使用者</span><span class="sxs-lookup"><span data-stu-id="c8309-109">Add a user</span></span>
1. <span data-ttu-id="c8309-110">登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)hello 目錄的全域管理員的帳戶。</span><span class="sxs-lookup"><span data-stu-id="c8309-110">Sign in toohello [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="c8309-111">選取 [Active Directory] ，然後開啟您的目錄。</span><span class="sxs-lookup"><span data-stu-id="c8309-111">Select **Active Directory**, and then open your directory.</span></span>
3. <span data-ttu-id="c8309-112">選取 hello**使用者**索引標籤，然後 hello 命令列中，選取**新增使用者**。</span><span class="sxs-lookup"><span data-stu-id="c8309-112">Select hello **Users** tab, and then, in hello command bar, select **Add User**.</span></span>
4. <span data-ttu-id="c8309-113">在 hello**告訴我們這位使用者**頁面的 **使用者類型**，選取：</span><span class="sxs-lookup"><span data-stu-id="c8309-113">On hello **Tell us about this user** page, under **Type of user**, select either:</span></span>

   * <span data-ttu-id="c8309-114">**另一個 Azure AD 目錄中的使用者**– 將其他 Azure AD 目錄的使用者帳戶 tooyour 目錄做為來源。</span><span class="sxs-lookup"><span data-stu-id="c8309-114">**User in another Azure AD directory** – adds a user account tooyour directory that's sourced from another Azure AD directory.</span></span> <span data-ttu-id="c8309-115">只有在您也是另一個目錄的成員時，才能選取該目錄中的使用者。</span><span class="sxs-lookup"><span data-stu-id="c8309-115">You can select a user in another directory only if you're also a member of that directory.</span></span>
   * <span data-ttu-id="c8309-116">**合作夥伴公司中的使用者**-tooinvite 並授權協力廠商公司使用者 tooyour 目錄 (請參閱[Azure Active Directory B2B 共同作業](active-directory-b2b-what-is-azure-ad-b2b.md))。</span><span class="sxs-lookup"><span data-stu-id="c8309-116">**Users in partner companies** - tooinvite and authorize partner company users tooyour directory (See [Azure Active Directory B2B collaboration](active-directory-b2b-what-is-azure-ad-b2b.md)).</span></span> <span data-ttu-id="c8309-117">您必須太[上傳 CSV 檔案指定電子郵件地址](active-directory-b2b-references-csv-file-format.md)。</span><span class="sxs-lookup"><span data-stu-id="c8309-117">You'll need too[upload a CSV file specifying email addresses](active-directory-b2b-references-csv-file-format.md).</span></span>
5. <span data-ttu-id="c8309-118">在 hello 使用者**設定檔**頁面上，提供第一個和最後一個名稱、 使用者易記的名稱，以及使用者角色的 hello**角色**清單。</span><span class="sxs-lookup"><span data-stu-id="c8309-118">On hello user **Profile** page, provide a first and last name, a user-friendly name, and a user role from hello **Roles** list.</span></span> <span data-ttu-id="c8309-119">如需有關使用者和系統管理員角色的詳細資訊，請參閱 [在 Azure AD 中指派系統管理員角色](active-directory-assign-admin-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="c8309-119">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span> <span data-ttu-id="c8309-120">指定是否太**啟用 Multi-factor Authentication** hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="c8309-120">Specify whether too**Enable Multi-Factor Authentication** for hello user.</span></span>
6. <span data-ttu-id="c8309-121">在 hello**取得暫時密碼**頁面上，選取**建立**。</span><span class="sxs-lookup"><span data-stu-id="c8309-121">On hello **Get temporary password** page, select **Create**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c8309-122">如果您的組織使用多個網域，您應該了解 hello 新增使用者帳戶時，下列問題：</span><span class="sxs-lookup"><span data-stu-id="c8309-122">If your organization uses more than one domain, you should know about hello following issues when you add a user account:</span></span>
>
> * <span data-ttu-id="c8309-123">tooadd 使用者帳戶與 hello 相同的使用者主體名稱 (UPN) 跨網域，**第一個**，例如新增geoffgrisso@contoso.onmicrosoft.com，**後面** geoffgrisso@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="c8309-123">tooadd user accounts with hello same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.</span></span>
> * <span data-ttu-id="c8309-124">請「勿」先新增 geoffgrisso@contoso.com，再新增 geoffgrisso@contoso.onmicrosoft.com。</span><span class="sxs-lookup"><span data-stu-id="c8309-124">**Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com.</span></span>
>

<span data-ttu-id="c8309-125">如果您變更與您在內部部署 Active Directory 服務同步處理身分識別使用者的資訊，您無法變更 hello hello Azure 傳統入口網站中的使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="c8309-125">If you change information for a user whose identity is synchronized with your on-premises Active Directory service, you can't change hello user information in hello Azure classic portal.</span></span> <span data-ttu-id="c8309-126">toochange hello 使用者資訊，請使用您在內部部署 Active Directory 管理工具。</span><span class="sxs-lookup"><span data-stu-id="c8309-126">toochange hello user information, use your on-premises Active Directory management tools.</span></span>

## <a name="add-external-users"></a><span data-ttu-id="c8309-127">新增外部使用者</span><span class="sxs-lookup"><span data-stu-id="c8309-127">Add external users</span></span>
<span data-ttu-id="c8309-128">您也可以新增使用者從您所隸屬的另一個 Azure AD 目錄 toowhich 或合作夥伴公司所上傳 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="c8309-128">You can also add users from another Azure AD directory toowhich you belong, or from partner companies by uploading a CSV file.</span></span> <span data-ttu-id="c8309-129">tooadd 外部使用者，如**使用者類型**，指定**另一個 Microsoft Azure AD 目錄中的使用者**或**夥伴公司中的使用者**。</span><span class="sxs-lookup"><span data-stu-id="c8309-129">tooadd an external user, for **Type of User**, specify **User in another Microsoft Azure AD directory** or **Users in partner companies**.</span></span>

<span data-ttu-id="c8309-130">這兩種類型的使用者是源自另一個目錄，並且新增為 [外部使用者] 。</span><span class="sxs-lookup"><span data-stu-id="c8309-130">Users of either type are sourced from another directory and are added as **external users**.</span></span> <span data-ttu-id="c8309-131">外部使用者可以共同作業與其他使用者在目錄中沒有任何需求 tooadd 新帳戶和認證。</span><span class="sxs-lookup"><span data-stu-id="c8309-131">External users can collaborate with other users in a directory without any requirement tooadd new accounts and credentials.</span></span> <span data-ttu-id="c8309-132">當它們登入，而該驗證也適用於已加入的任何其他目錄 toowhich 外部使用者向其主目錄中。</span><span class="sxs-lookup"><span data-stu-id="c8309-132">External users authenticate with their home directory when they sign in, and that authentication works for any other directories toowhich they have been added.</span></span>

## <a name="external-user-management-and-limitations"></a><span data-ttu-id="c8309-133">外部使用者管理和限制</span><span class="sxs-lookup"><span data-stu-id="c8309-133">External user management and limitations</span></span>
<span data-ttu-id="c8309-134">當您從另一個目錄 tooyour 目錄新增使用者時，該使用者是您目錄中的外部使用者。</span><span class="sxs-lookup"><span data-stu-id="c8309-134">When you add a user from another directory tooyour directory, that user is an external user in your directory.</span></span> <span data-ttu-id="c8309-135">hello 顯示名稱和使用者名稱已從其主目錄複製，並使用您的目錄中的 hello 外部使用者。</span><span class="sxs-lookup"><span data-stu-id="c8309-135">hello display name and user name are copied from their home directory and used for hello external user in your directory.</span></span> <span data-ttu-id="c8309-136">從那時起，hello 外部使用者帳戶的內容是完全獨立的。</span><span class="sxs-lookup"><span data-stu-id="c8309-136">From then on, properties of hello external user account are entirely independent.</span></span> <span data-ttu-id="c8309-137">如果屬性的變更 toohello 使用者主目錄中，這些變更未傳播 toohello 外部使用者帳戶，在您的目錄。</span><span class="sxs-lookup"><span data-stu-id="c8309-137">If property changes are made toohello user in their home directory, those changes aren't propagated toohello external user account in your directory.</span></span>

<span data-ttu-id="c8309-138">hello hello 兩個帳戶之間的唯一連結就是針對其主目錄或其 Microsoft 帳戶，一律會驗證該 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="c8309-138">hello only linkage between hello two accounts is that hello user always authenticates against their home directory or with their Microsoft account.</span></span> <span data-ttu-id="c8309-139">這就是為什麼您沒有看見選項 tooreset hello 密碼或啟用多因素驗證，這樣外部使用者。</span><span class="sxs-lookup"><span data-stu-id="c8309-139">That's why you don't see an option tooreset hello password or enable multi-factor authentication for an external user.</span></span> <span data-ttu-id="c8309-140">目前，hello hello 主目錄或 Microsoft 帳戶的驗證原則是只有一個 hello 使用者登入時會評估 hello。</span><span class="sxs-lookup"><span data-stu-id="c8309-140">Currently, hello authentication policy of hello home directory or Microsoft account is hello only one that's evaluated when hello user signs in.</span></span>

> [!NOTE]
> <span data-ttu-id="c8309-141">您仍可停用 hello hello 目錄，它會封鎖存取 tooyour 目錄中的外部使用者。</span><span class="sxs-lookup"><span data-stu-id="c8309-141">You can still disable hello external user in hello directory, which blocks access tooyour directory.</span></span>
>
>

<span data-ttu-id="c8309-142">如果使用者被刪除其主目錄中，或使用者取消其 Microsoft 帳戶，hello 外部使用者仍會存在目錄中。</span><span class="sxs-lookup"><span data-stu-id="c8309-142">If a user is deleted in their home directory or they cancel their Microsoft account, hello external user still exists in your directory.</span></span> <span data-ttu-id="c8309-143">不過，您的目錄中的 hello 使用者無法存取資源，因為它們無法使用的主目錄或 Microsoft 帳戶驗證。</span><span class="sxs-lookup"><span data-stu-id="c8309-143">However, hello user in your directory can't access resources because they can't authenticate with a home directory or Microsoft account.</span></span>

### <a name="services-that-currently-support-access-by-azure-ad-external-users"></a><span data-ttu-id="c8309-144">目前支援讓 Azure AD 外部使用者存取的服務</span><span class="sxs-lookup"><span data-stu-id="c8309-144">Services that currently support access by Azure AD external users</span></span>
* <span data-ttu-id="c8309-145">**Azure 傳統入口網站**： 可讓外部使用者管理員的多個目錄 toomanage 每個這些目錄。</span><span class="sxs-lookup"><span data-stu-id="c8309-145">**Azure classic portal**: allows an external user who's an administrator of multiple directories toomanage each of those directories.</span></span>
* <span data-ttu-id="c8309-146">**SharePoint Online**： 如果已啟用外部共用，讓外部使用者 tooaccess SharePoint Online 授權資源。</span><span class="sxs-lookup"><span data-stu-id="c8309-146">**SharePoint Online**: if external sharing is enabled, allows an external user tooaccess SharePoint Online authorized resources.</span></span>
* <span data-ttu-id="c8309-147">**Dynamics CRM**： 如果 hello 使用者已透過 PowerShell 授權，可讓外部使用者 tooaccess 授權 Dynamics CRM 中的資源。</span><span class="sxs-lookup"><span data-stu-id="c8309-147">**Dynamics CRM**: if hello user is licensed via PowerShell, allows an external user tooaccess authorized resources in Dynamics CRM.</span></span>
* <span data-ttu-id="c8309-148">**Dynamics AX**： 如果 hello 使用者已透過 PowerShell 授權，可讓外部使用者 tooaccess 授權 Dynamics AX 中的資源。</span><span class="sxs-lookup"><span data-stu-id="c8309-148">**Dynamics AX**: if hello user is licensed via PowerShell, allows an external user tooaccess authorized resources in Dynamics AX.</span></span> <span data-ttu-id="c8309-149">hello 限制[Azure AD 的外部使用者](#known-limitations-of-azure-ad-external-users)tooexternal 使用者 Dynamics AX 中的也會套用。</span><span class="sxs-lookup"><span data-stu-id="c8309-149">hello limitations for [Azure AD external users](#known-limitations-of-azure-ad-external-users) apply tooexternal users in Dynamics AX as well.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8309-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c8309-150">Next steps</span></span>
* [<span data-ttu-id="c8309-151">加入新使用者 tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c8309-151">Add new users tooAzure Active Directory</span></span>](active-directory-create-users.md)
* [<span data-ttu-id="c8309-152">管理 Azure AD</span><span class="sxs-lookup"><span data-stu-id="c8309-152">Administering Azure AD</span></span>](active-directory-administer.md)
* [<span data-ttu-id="c8309-153">在 Azure AD 中管理密碼</span><span class="sxs-lookup"><span data-stu-id="c8309-153">Manage passwords in Azure AD</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="c8309-154">在 Azure AD 中管理群組</span><span class="sxs-lookup"><span data-stu-id="c8309-154">Manage groups in Azure AD</span></span>](active-directory-manage-groups.md)
