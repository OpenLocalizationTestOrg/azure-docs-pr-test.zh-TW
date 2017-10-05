---
title: "將使用者新增至 Azure Active Directory | Microsoft Docs"
description: "說明如何在 Azure Active Directory 中新增新的使用者或變更使用者資訊。"
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
ms.openlocfilehash: ff4b742e772a6062885313e9bb49e55907fe125a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="add-new-users-or-users-with-microsoft-accounts-to-azure-active-directory"></a><span data-ttu-id="de17e-103">在 Azure Active Directory 新增新的使用者或具有 Microsoft 帳戶的使用者</span><span class="sxs-lookup"><span data-stu-id="de17e-103">Add new users or users with Microsoft accounts to Azure Active Directory</span></span>
<span data-ttu-id="de17e-104">請新增使用者來填入您的目錄。</span><span class="sxs-lookup"><span data-stu-id="de17e-104">Add users to populate your directory.</span></span> <span data-ttu-id="de17e-105">本文說明如何在組織中新增新的使用者，以及如何新增具有 Microsoft 帳戶的使用者。</span><span class="sxs-lookup"><span data-stu-id="de17e-105">This article explains how to add new users in your organization, and how to add users who have Microsoft accounts.</span></span> <span data-ttu-id="de17e-106">如需新增來自 Azure Active Directory 中其他目錄之使用者或是來自合作夥伴公司之使用者的詳細資訊，請參閱 [新增來自 Azure Active Directory 中其他目錄或合作夥伴公司的使用者](active-directory-create-users-external.md)。</span><span class="sxs-lookup"><span data-stu-id="de17e-106">For more information about adding users from other directories in Azure Active Directory or adding users from partner companies, see [Add users from other directories or partner companies in Azure Active Directory](active-directory-create-users-external.md).</span></span> <span data-ttu-id="de17e-107">新增的使用者預設不會有系統管理員權限，但是您可以隨時指派角色給他們。</span><span class="sxs-lookup"><span data-stu-id="de17e-107">Added users don't have administrator permissions by default, but you can assign roles to them at any time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="de17e-108">Microsoft 建議您使用 Azure 入口網站中的 [Azure AD 系統管理中心](https://aad.portal.azure.com)來管理 Azure AD，而不要使用本文所提及的 Azure 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="de17e-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="de17e-109">關於如何在 Azure AD 系統管理中心新增使用者，請參閱[將新的使用者新增至 Azure Active Directory](active-directory-users-create-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="de17e-109">For how to add a user in the Azure AD admin center, see [Add new users to Azure Active Directory](active-directory-users-create-azure-portal.md).</span></span>

## <a name="add-a-user"></a><span data-ttu-id="de17e-110">新增使用者</span><span class="sxs-lookup"><span data-stu-id="de17e-110">Add a user</span></span>
1. <span data-ttu-id="de17e-111">使用屬於目錄全域管理員的帳戶登入 [Azure 傳統入口網站](https://manage.windowsazure.com) 。</span><span class="sxs-lookup"><span data-stu-id="de17e-111">Sign in to the [Azure classic portal](https://manage.windowsazure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="de17e-112">選取 [Active Directory] ，然後選取貴組織目錄的名稱。</span><span class="sxs-lookup"><span data-stu-id="de17e-112">Select **Active Directory**, and then select the name of your organization directory.</span></span>
3. <span data-ttu-id="de17e-113">選取 [使用者] 索引標籤，然後在命令列中選取 [新增使用者]。</span><span class="sxs-lookup"><span data-stu-id="de17e-113">Select the **Users** tab, and then, in the command bar, select **Add User**.</span></span>
4. <span data-ttu-id="de17e-114">在 [告訴我們這位使用者] 頁面上，於 [使用者類型] 底下選取下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="de17e-114">On the **Tell us about this user** page, under **Type of user**, select either:</span></span>

   * <span data-ttu-id="de17e-115">**您組織中的新使用者** – 在您的目錄中新增使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="de17e-115">**New user in your organization** – adds a new user account in your directory.</span></span>
   * <span data-ttu-id="de17e-116">**現有 Microsoft 帳戶的使用者** – 將現有的 Microsoft 取用者帳戶加入至您的目錄 (例如，Outlook 帳戶)。</span><span class="sxs-lookup"><span data-stu-id="de17e-116">**User with an existing Microsoft account** – adds an existing Microsoft consumer account to your directory (for example, an Outlook account)</span></span>
5. <span data-ttu-id="de17e-117">根據 [使用者類型] 輸入使用者名稱 (適用於新使用者) 或電子郵件地址 (適用於具有 Microsoft 帳戶的使用者)。</span><span class="sxs-lookup"><span data-stu-id="de17e-117">Depending on **Type of user**, enter a user name (for new user) or an email address (for a user with a Microsoft account).</span></span>
6. <span data-ttu-id="de17e-118">在 [使用者設定檔] 頁面上，提供姓氏和名字、使用者易記名稱，並從 [角色] 清單中選擇使用者角色。</span><span class="sxs-lookup"><span data-stu-id="de17e-118">On the user **Profile** page, provide a first and last name, a user-friendly name, and a user role from the **Roles** list.</span></span> <span data-ttu-id="de17e-119">如需有關使用者和系統管理員角色的詳細資訊，請參閱 [在 Azure AD 中指派系統管理員角色](active-directory-assign-admin-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="de17e-119">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span> <span data-ttu-id="de17e-120">指定是否為使用者**啟用 Multi-Factor Authentication**。</span><span class="sxs-lookup"><span data-stu-id="de17e-120">Specify whether to **Enable Multi-Factor Authentication** for the user.</span></span>
7. <span data-ttu-id="de17e-121">在 [取得暫時密碼] 頁面上，選取 [建立]。</span><span class="sxs-lookup"><span data-stu-id="de17e-121">On the **Get temporary password** page, select **Create**.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="de17e-122">如果您的組織使用多個網域，當您新增使用者帳戶時，請注意下列問題：</span><span class="sxs-lookup"><span data-stu-id="de17e-122">If your organization uses more than one domain, you should know about the following issues when you add a user account:</span></span>
>
> * <span data-ttu-id="de17e-123">若要跨網域新增具有相同使用者主體名稱 (UPN) 的使用者帳戶，請**先**新增 geoffgrisso@contoso.onmicrosoft.com，**再**新增 geoffgrisso@contoso.com。</span><span class="sxs-lookup"><span data-stu-id="de17e-123">TO add user accounts with the same user principal name (UPN) across domains, **first** add, for example, geoffgrisso@contoso.onmicrosoft.com, **followed by** geoffgrisso@contoso.com.</span></span>
> * <span data-ttu-id="de17e-124">請「勿」先新增 geoffgrisso@contoso.com，再新增 geoffgrisso@contoso.onmicrosoft.com。</span><span class="sxs-lookup"><span data-stu-id="de17e-124">**Don't** add geoffgrisso@contoso.com before you add geoffgrisso@contoso.onmicrosoft.com.</span></span> <span data-ttu-id="de17e-125">此順序很重要，事後想要復原會很麻煩。</span><span class="sxs-lookup"><span data-stu-id="de17e-125">This order is important, and can be cumbersome to undo.</span></span>
>
>

## <a name="change-user-information"></a><span data-ttu-id="de17e-126">變更使用者資訊</span><span class="sxs-lookup"><span data-stu-id="de17e-126">Change user information</span></span>
<span data-ttu-id="de17e-127">您可以變更任何使用者屬性，但物件識別碼除外。</span><span class="sxs-lookup"><span data-stu-id="de17e-127">You can change any user attribute except for the object ID.</span></span>

1. <span data-ttu-id="de17e-128">開啟您的目錄。</span><span class="sxs-lookup"><span data-stu-id="de17e-128">Open your directory.</span></span>
2. <span data-ttu-id="de17e-129">選取 [使用者]  索引標籤，然後選取想要變更之使用者的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="de17e-129">Select the **Users** tab, and then select the display name of the user you want to change.</span></span>
3. <span data-ttu-id="de17e-130">完成您的變更，然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="de17e-130">Complete your changes, and then click **Save**.</span></span>

<span data-ttu-id="de17e-131">如果您嘗試變更的使用者已經與內部部署 Active Directory 服務同步處理，您將無法使用此程序來變更使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="de17e-131">If the user that you're changing is synchronized with your on-premises Active Directory service, you can't change the user information using this procedure.</span></span> <span data-ttu-id="de17e-132">若要變更此使用者，請使用您的內部部署 Active Directory 管理工具。</span><span class="sxs-lookup"><span data-stu-id="de17e-132">To change the user, use your on-premises Active Directory management tools.</span></span>

## <a name="guest-user-management-and-limitations"></a><span data-ttu-id="de17e-133">來賓使用者管理和限制</span><span class="sxs-lookup"><span data-stu-id="de17e-133">Guest user management and limitations</span></span>
<span data-ttu-id="de17e-134">來賓帳戶是來自其他目錄的使用者，其已受邀至您的目錄以存取 SharePoint 文件、應用程式或其他 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="de17e-134">Guest accounts are users from other directories who were invited to your directory to access SharePoint documents, applications, or other Azure resources.</span></span> <span data-ttu-id="de17e-135">您的目錄中的來賓帳戶會將其基礎 UserType 屬性設為 [來賓]。</span><span class="sxs-lookup"><span data-stu-id="de17e-135">A guest account in your directory has its underlying UserType attribute set to "Guest."</span></span> <span data-ttu-id="de17e-136">一般使用者 (具體而言是指您目錄的成員) 的 UserType 屬性則為 [成員]。</span><span class="sxs-lookup"><span data-stu-id="de17e-136">Regular users (specifically, members of your directory) have the UserType attribute "Member."</span></span>

<span data-ttu-id="de17e-137">來賓在目錄中有一組受限的權限。</span><span class="sxs-lookup"><span data-stu-id="de17e-137">Guests have a limited set of rights in the directory.</span></span> <span data-ttu-id="de17e-138">這些權限會禁止來賓探索目錄中其他使用者的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="de17e-138">These rights limit the ability for Guests to discover information about other users in the directory.</span></span> <span data-ttu-id="de17e-139">不過，來賓使用者仍可與其使用之資源相關聯的使用者和群組互動。</span><span class="sxs-lookup"><span data-stu-id="de17e-139">However, guest users can still interact with the users and groups associated with the resources they're working on.</span></span> <span data-ttu-id="de17e-140">來賓使用者可以：</span><span class="sxs-lookup"><span data-stu-id="de17e-140">Guest users can:</span></span>

* <span data-ttu-id="de17e-141">查看與他們被指派到的 Azure 訂用帳戶相關聯的使用者和群組</span><span class="sxs-lookup"><span data-stu-id="de17e-141">See other users and groups associated with an Azure subscription to which they're assigned</span></span>
* <span data-ttu-id="de17e-142">查看其所屬之群組的成員</span><span class="sxs-lookup"><span data-stu-id="de17e-142">See the members of groups to which they belong</span></span>
* <span data-ttu-id="de17e-143">如果他們已經知道使用者的完整電子郵件地址，則可以查閱目錄中的其他使用者</span><span class="sxs-lookup"><span data-stu-id="de17e-143">Look up other users in the directory, if they know the full email address of the user</span></span>
* <span data-ttu-id="de17e-144">僅能查看他們查閱的使用者的有限屬性集 - 僅限於顯示名稱、電子郵件地址、使用者主體名稱 (UPN) 和相片縮圖</span><span class="sxs-lookup"><span data-stu-id="de17e-144">See only a limited set of attributes of the users they look up--limited to display name, email address, user principal name (UPN), and thumbnail photo</span></span>
* <span data-ttu-id="de17e-145">取得目錄中已驗證的網域清單</span><span class="sxs-lookup"><span data-stu-id="de17e-145">Get a list of verified domains in the directory</span></span>
* <span data-ttu-id="de17e-146">同意應用程式，授與它們與在您的目錄中相同的成員存取權</span><span class="sxs-lookup"><span data-stu-id="de17e-146">Consent to applications, granting them the same access that Members have in your directory</span></span>

## <a name="set-guest-user-access-policies"></a><span data-ttu-id="de17e-147">設定來賓使用者存取原則</span><span class="sxs-lookup"><span data-stu-id="de17e-147">Set guest user access policies</span></span>
<span data-ttu-id="de17e-148">目錄內的 [設定]  索引標籤內含可控制來賓使用者存取權限的選項。</span><span class="sxs-lookup"><span data-stu-id="de17e-148">The **Configure** tab of a directory includes options to control access for guest users.</span></span> <span data-ttu-id="de17e-149">這些選項只可以由目錄全域管理員在 Azure 傳統入口網站中進行變更。</span><span class="sxs-lookup"><span data-stu-id="de17e-149">These options can be changed only in Azure classic portal by a directory global administrator.</span></span> <span data-ttu-id="de17e-150">目前沒有透過 PowerShell 或 API 的方法。</span><span class="sxs-lookup"><span data-stu-id="de17e-150">Currently, there's no PowerShell or API method.</span></span>

<span data-ttu-id="de17e-151">若要在 Azure 傳統入口網站中開啟 [設定] 索引標籤，請選取 [Active Directory]，然後選取目錄的名稱。</span><span class="sxs-lookup"><span data-stu-id="de17e-151">To open the **Configure** tab in the Azure classic portal, select **Active Directory**, and then select the name of the directory.</span></span>

![在 Azure Active Directory 中設定索引標籤][1]

<span data-ttu-id="de17e-153">接著您可以編輯選項來控制來賓使用者的存取權限。</span><span class="sxs-lookup"><span data-stu-id="de17e-153">Then you can edit the options to control access for guest users.</span></span>

![來賓使用者的存取控制選項][2]

## <a name="whats-next"></a><span data-ttu-id="de17e-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="de17e-155">What's next</span></span>
* [<span data-ttu-id="de17e-156">新增來自 Azure Active Directory 中其他目錄或合作夥伴公司的使用者</span><span class="sxs-lookup"><span data-stu-id="de17e-156">Add users from other directories or partner companies in Azure Active Directory</span></span>](active-directory-create-users-external.md)
* [<span data-ttu-id="de17e-157">管理 Azure AD</span><span class="sxs-lookup"><span data-stu-id="de17e-157">Administering Azure AD</span></span>](active-directory-administer.md)
* [<span data-ttu-id="de17e-158">在 Azure AD 中管理密碼</span><span class="sxs-lookup"><span data-stu-id="de17e-158">Manage passwords in Azure AD</span></span>](active-directory-manage-passwords.md)
* [<span data-ttu-id="de17e-159">在 Azure AD 中管理群組</span><span class="sxs-lookup"><span data-stu-id="de17e-159">Manage groups in Azure AD</span></span>](active-directory-manage-groups.md)

<!--Image references-->
[1]: ./media/active-directory-create-users/RBACDirConfigTab.png
[2]: ./media/active-directory-create-users/RBACGuestAccessControls.png
