---
title: "建立自訂的角色型存取控制角色，並指派給 Azure 中的內部和外部使用者 | Microsoft Docs"
description: "將針對內部和外部使用者使用 PowerShell 和 CLI 所建立的自訂 RBAC 角色進行指派"
services: active-directory
documentationcenter: 
author: andreicradu
manager: catadinu
editor: kgremban
ms.assetid: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/10/2017
ms.author: a-crradu
ms.openlocfilehash: d687f94bebfd0b6c1ec0690da798be5409640954
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
## <a name="intro-on-role-based-access-control"></a><span data-ttu-id="38c7e-103">角色型存取控制簡介</span><span class="sxs-lookup"><span data-stu-id="38c7e-103">Intro on role-based access control</span></span>

<span data-ttu-id="38c7e-104">角色型存取控制是僅限 Azure 入口網站使用的功能，可讓訂用帳戶擁有者將細微角色指派給其他能夠管理其環境中特定資源範圍的使用者。</span><span class="sxs-lookup"><span data-stu-id="38c7e-104">Role-based access control is an Azure portal only feature allowing the owners of a subscription to assign granular roles to other users who can manage specific resource scopes in their environment.</span></span>

<span data-ttu-id="38c7e-105">RBAC 可提供更好的安全性管理，對象包括大型組織，以及與需要存取您環境中的特定資源，但不一定需要存取整個基礎結構或任何計費相關範圍的外部共同作業者、廠商或自由工作者共同合作的 SMB。</span><span class="sxs-lookup"><span data-stu-id="38c7e-105">RBAC allows better security management for large organizations and for SMBs working with external collaborators, vendors or freelancers which need access to specific resources in your environment but not necessarily to the entire infrastructure or any billing-related scopes.</span></span> <span data-ttu-id="38c7e-106">RBAC 能提供彈性，可擁有一個系統管理員帳戶 (訂用帳戶等級中的服務系統管理員角色) 所管理的 Azure 訂用帳戶，並邀請多個使用者在相同的訂用帳戶下運作，而無需任何系統管理權限。</span><span class="sxs-lookup"><span data-stu-id="38c7e-106">RBAC allows the flexibility of owning one Azure subscription managed by the administrator account (service administrator role at a subscription level) and have multiple users invited to work under the same subscription but without any administrative rights for it.</span></span> <span data-ttu-id="38c7e-107">從管理和計費的觀點而言，RBAC 功能證實是各種情況中使用 Azure 的有效時間和管理選項。</span><span class="sxs-lookup"><span data-stu-id="38c7e-107">From a management and billing perspective, the RBAC feature proves to be a time and management efficient option for using Azure in various scenarios.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38c7e-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="38c7e-108">Prerequisites</span></span>
<span data-ttu-id="38c7e-109">在 Azure 環境中使用 RBAC 需要︰</span><span class="sxs-lookup"><span data-stu-id="38c7e-109">Using RBAC in the Azure environment requires:</span></span>

* <span data-ttu-id="38c7e-110">將獨立的 Azure 訂用帳戶指派至使用者作為擁有者 (訂用帳戶角色)</span><span class="sxs-lookup"><span data-stu-id="38c7e-110">Having a standalone Azure subscription assigned to the user as owner (subscription role)</span></span>
* <span data-ttu-id="38c7e-111">具有 Azure 訂用帳戶的擁有者角色</span><span class="sxs-lookup"><span data-stu-id="38c7e-111">Have the Owner role of the Azure subscription</span></span>
* <span data-ttu-id="38c7e-112">具有 [Azure 入口網站](https://portal.azure.com)的存取權</span><span class="sxs-lookup"><span data-stu-id="38c7e-112">Have access to the [Azure portal](https://portal.azure.com)</span></span>
* <span data-ttu-id="38c7e-113">請確定使用者訂用帳戶已登錄下列資源提供者︰**Microsoft.Authorization**。</span><span class="sxs-lookup"><span data-stu-id="38c7e-113">Make sure to have the following Resource Providers registered for the user subscription: **Microsoft.Authorization**.</span></span> <span data-ttu-id="38c7e-114">如需有關如何登錄資源提供者的詳細資訊，請參閱 [Resource Manager 提供者、區域、API 版本及結構描述](/azure-resource-manager/resource-manager-supported-services.md)。</span><span class="sxs-lookup"><span data-stu-id="38c7e-114">For more information on how to register the resource providers, see [Resource Manager providers, regions, API versions and schemas](/azure-resource-manager/resource-manager-supported-services.md).</span></span>

> [!NOTE]
> <span data-ttu-id="38c7e-115">從 O365 入口網站佈建的 Office 365 訂用帳戶或 Azure Active Directory 授權 (例如︰存取 Azure Active Directory) 沒有資格使用 RBAC。</span><span class="sxs-lookup"><span data-stu-id="38c7e-115">Office 365 subscriptions or Azure Active Directory licenses (for example: Access to Azure Active Directory) provisioned from the O365 portal don't quality for using RBAC.</span></span>

## <a name="how-can-rbac-be-used"></a><span data-ttu-id="38c7e-116">如何使用 RBAC</span><span class="sxs-lookup"><span data-stu-id="38c7e-116">How can RBAC be used</span></span>
<span data-ttu-id="38c7e-117">RBAC 在 Azure 中可套用於三個不同範圍。</span><span class="sxs-lookup"><span data-stu-id="38c7e-117">RBAC can be applied at three different scopes in Azure.</span></span> <span data-ttu-id="38c7e-118">從最低到最高的範圍，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="38c7e-118">From the highest scope to the lowest one, they are as follows:</span></span>

* <span data-ttu-id="38c7e-119">訂用帳戶 (最高)</span><span class="sxs-lookup"><span data-stu-id="38c7e-119">Subscription (highest)</span></span>
* <span data-ttu-id="38c7e-120">資源群組</span><span class="sxs-lookup"><span data-stu-id="38c7e-120">Resource group</span></span>
* <span data-ttu-id="38c7e-121">資源範圍 (向個別 Azure 資源範圍提供目標權限的最低存取等級)</span><span class="sxs-lookup"><span data-stu-id="38c7e-121">Resource scope (the lowest access level offering targeted permissions to an individual Azure resource scope)</span></span>

## <a name="assign-rbac-roles-at-the-subscription-scope"></a><span data-ttu-id="38c7e-122">指派訂用帳戶範圍內的 RBAC 角色</span><span class="sxs-lookup"><span data-stu-id="38c7e-122">Assign RBAC roles at the subscription scope</span></span>
<span data-ttu-id="38c7e-123">使用 RBAC 時，有兩個常見的範例 (但是不限於)︰</span><span class="sxs-lookup"><span data-stu-id="38c7e-123">There are two common examples when RBAC is used (but not limited to):</span></span>

* <span data-ttu-id="38c7e-124">邀請來自組織 (並非管理使用者 Azure Active Directory 租用戶的一部分) 外部的使用者來管理特定的資源或是整個訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="38c7e-124">Having external users from the organizations (not part of the admin user's Azure Active Directory tenant) invited to manage certain resources or the whole subscription</span></span>
* <span data-ttu-id="38c7e-125">適用於組織內部 (它們屬於使用者 Azure Active Directory 租用戶的一部分) 的使用者，但屬於不同小組或群組的使用者除外，它們需要細微存取整個訂用帳戶，或特定資源群組或環境中之資源範圍</span><span class="sxs-lookup"><span data-stu-id="38c7e-125">Working with users inside the organization (they are part of the user's Azure Active Directory tenant) but part of different teams or groups which need granular access either to the whole subscription or to certain resource groups or resource scopes in the environment</span></span>

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a><span data-ttu-id="38c7e-126">為 Azure Active Directory 外部的使用者授與訂用帳戶等級的存取權</span><span class="sxs-lookup"><span data-stu-id="38c7e-126">Grant access at a subscription level for a user outside of Azure Active Directory</span></span>
<span data-ttu-id="38c7e-127">只有訂用帳戶的**擁有者**可授與 RBAC 角色，因此必須使用此角色已預先指派或已建立 Azure 訂用帳戶的使用者名稱來記錄管理使用者。</span><span class="sxs-lookup"><span data-stu-id="38c7e-127">RBAC roles can be granted only by **Owners** of the subscription therefore the admin user must be logged with a username which has this role pre-assigned or has created the Azure subscription.</span></span>

<span data-ttu-id="38c7e-128">從 Azure 入口網站中，在您以管理員身分登入之後，請選取「訂用帳戶」，並選擇所需的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="38c7e-128">From the Azure portal, after you sign-in as admin, select “Subscriptions” and chose the desired one.</span></span>
<span data-ttu-id="38c7e-129">![Azure 入口網站中的訂用帳戶刀鋒視窗](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) 根據預設，如果管理使用者已購買 Azure 訂用帳戶，使用者就會顯示為**帳戶管理員**，這是訂用帳戶角色。</span><span class="sxs-lookup"><span data-stu-id="38c7e-129">![subscription blade in Azure portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) By default, if the admin user has purchased the Azure subscription, the user will show up as **Account Admin**, this being the subscription role.</span></span> <span data-ttu-id="38c7e-130">如需 Azure 訂用帳戶角色的詳細資訊，請參閱[新增或變更管理訂用帳戶或服務的 Azure 系統管理員角色](/billing/billing-add-change-azure-subscription-administrator.md)。</span><span class="sxs-lookup"><span data-stu-id="38c7e-130">For more details on the Azure subscription roles, see [Add or change Azure administrator roles that manage the subscription or services](/billing/billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="38c7e-131">在此範例中，使用者 "alflanigan@outlook.com" 是「預設租用戶 Azure」AAD 租用戶中的「免費試用版」訂用帳戶之**擁有者**。</span><span class="sxs-lookup"><span data-stu-id="38c7e-131">In this example, the user "alflanigan@outlook.com" is the **Owner** of the "Free Trial" subscription in the AAD tenant "Default tenant Azure".</span></span> <span data-ttu-id="38c7e-132">這個使用者是利用初始 Microsoft 帳戶 “Outlook” (Microsoft Account = Outlook, Live etc.) 的 Azure 訂用帳戶建立者，因此這個租用戶中新增之所有其他使用者的預設網域名稱為 **"@alflaniganuoutlook.onmicrosoft.com"**。</span><span class="sxs-lookup"><span data-stu-id="38c7e-132">Since this user is the creator of the Azure subscription with the initial Microsoft Account “Outlook” (Microsoft Account = Outlook, Live etc.) the default domain name for all other users added in this tenant will be **"@alflaniganuoutlook.onmicrosoft.com"**.</span></span> <span data-ttu-id="38c7e-133">根據設計，新網域的語法構成方式是，將建立租用戶的使用者之使用者名稱和網域名稱加以組合，並新增 **".onmicrosoft.com"** 延伸。</span><span class="sxs-lookup"><span data-stu-id="38c7e-133">By design, the syntax of the new domain is formed by putting together the username and domain name of the user who created the tenant and adding the extension **".onmicrosoft.com"**.</span></span>
<span data-ttu-id="38c7e-134">此外，使用者在新增及驗證新租用戶的自訂網域名稱之後，可以使用租用戶中的自訂網域名稱進行登入。</span><span class="sxs-lookup"><span data-stu-id="38c7e-134">Furthermore, users can sign-in with a custom domain name in the tenant after adding and verifying it for the new tenant.</span></span> <span data-ttu-id="38c7e-135">如需如何驗證 Azure Active Directory 租用戶中自訂網域名稱的詳細資訊，請參閱[將自訂網域名稱新增至您的目錄](/active-directory/active-directory-add-domain)。</span><span class="sxs-lookup"><span data-stu-id="38c7e-135">For more details on how to verify a custom domain name in an Azure Active Directory tenant, see [Add a custom domain name to your directory](/active-directory/active-directory-add-domain).</span></span>

<span data-ttu-id="38c7e-136">在此範例中，「預設租用戶 Azure」目錄僅包含具有 "@alflanigan.onmicrosoft.com" 網域名稱的使用者。</span><span class="sxs-lookup"><span data-stu-id="38c7e-136">In this example, the "Default tenant Azure" directory contains only users with the domain name "@alflanigan.onmicrosoft.com".</span></span>

<span data-ttu-id="38c7e-137">選取訂用帳戶之後，管理使用者必須依序按一下 [存取控制 (IAM)] 以及 [新增角色]。</span><span class="sxs-lookup"><span data-stu-id="38c7e-137">After selecting the subscription, the admin user must click **Access Control (IAM)** and then **Add a new role**.</span></span>





![Azure 入口網站中的存取控制 IAM 功能](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![在 Azure 入口網站的存取控制 IAM 功能中新增使用者](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

<span data-ttu-id="38c7e-140">下一個步驟是選取要指派的角色，以及要指派 RBAC 角色的使用者。</span><span class="sxs-lookup"><span data-stu-id="38c7e-140">The next step is to select the role to be assigned and the user whom the RBAC role will be assigned to.</span></span> <span data-ttu-id="38c7e-141">在 [角色] 下拉式功能表中，管理使用者只會看到 Azure 中提供的內建 RBAC 角色。</span><span class="sxs-lookup"><span data-stu-id="38c7e-141">In the **Role** dropdown menu the admin user sees only the built-in RBAC roles which are available in Azure.</span></span> <span data-ttu-id="38c7e-142">如需每個角色及其可指派範圍的詳細說明，請參閱 [Azure 角色型存取控制的內建角色](/active-directory/role-based-access-built-in-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="38c7e-142">For more detailed explanations of each role and their assignable scopes, see [Built-in roles for Azure Role-Based Access Control](/active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="38c7e-143">然後，管理使用者必須新增外部使用者的電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="38c7e-143">The admin user then needs to add the email address of the external user.</span></span> <span data-ttu-id="38c7e-144">預期的行為是要使外部使用者不顯示在現有的租用戶中。</span><span class="sxs-lookup"><span data-stu-id="38c7e-144">The expected behavior is for the external user to not show up in the existing tenant.</span></span> <span data-ttu-id="38c7e-145">外部使用者受邀請之後，他會與目前已指派訂用帳戶範圍內之 RBAC 角色的所有目前使用者一起顯示在 [訂用帳戶] > [存取控制 (IAM)] 下。</span><span class="sxs-lookup"><span data-stu-id="38c7e-145">After the external user has been invited, he will be visible under **Subscriptions > Access Control (IAM)** with all the current users which are currently assigned an RBAC role at the Subscription scope.</span></span>





![將權限新增至新的 RBAC 角色](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![訂用帳戶等級的 RBAC 角色清單](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

<span data-ttu-id="38c7e-148">已邀請使用者 "chessercarlton@gmail.com" 成為「免費試用」訂用帳戶的**擁有者**。</span><span class="sxs-lookup"><span data-stu-id="38c7e-148">The user "chessercarlton@gmail.com" has been invited to be an **Owner** for the “Free Trial” subscription.</span></span> <span data-ttu-id="38c7e-149">傳送邀請之後，外部使用者會收到包含啟用連結的電子郵件確認。</span><span class="sxs-lookup"><span data-stu-id="38c7e-149">After sending the invitation, the external user will receive an email confirmation with an activation link.</span></span>
<span data-ttu-id="38c7e-150">![RBAC 角色的電子郵件邀請](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span><span class="sxs-lookup"><span data-stu-id="38c7e-150">![email invitation for RBAC role](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span></span>

<span data-ttu-id="38c7e-151">在組織外部的新使用者，沒有任何「預設租用戶 Azure」目錄中的現有屬性。</span><span class="sxs-lookup"><span data-stu-id="38c7e-151">Being external to the organization, the new user does not have any existing attributes in the "Default tenant Azure" directory.</span></span> <span data-ttu-id="38c7e-152">外部使用者取得同意在與訂用帳戶 (已受指派角色) 相關聯的目錄中加以記錄之後，便會建立它們。</span><span class="sxs-lookup"><span data-stu-id="38c7e-152">They will be created after the external user has given consent to be recorded in the directory which is associated with the subscription which he has been assigned a role to.</span></span>





![RBAC 角色的電子郵件邀請訊息](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

<span data-ttu-id="38c7e-154">從現在起，外部使用者在 Azure Active Directory 租用戶中會顯示為外部使用者，在 Azure 入口網站和傳統入口網站中都可加以檢視。</span><span class="sxs-lookup"><span data-stu-id="38c7e-154">The external user shows in the Azure Active Directory tenant from now on as external user and this can be viewed both in the Azure portal and in the classic portal.</span></span>





![使用者刀鋒視窗 Azure Active Directory Azure 入口網站](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![使用者刀鋒視窗 Azure Active Directory Azure 傳統入口網站](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

<span data-ttu-id="38c7e-157">在這兩個入口網站的**使用者**檢視中，外部使用者的辨識方式為︰</span><span class="sxs-lookup"><span data-stu-id="38c7e-157">In the **Users** view in both portals the external users can be recognized by:</span></span>

* <span data-ttu-id="38c7e-158">Azure 入口網站中不同的圖示類型</span><span class="sxs-lookup"><span data-stu-id="38c7e-158">The different icon type in the Azure portal</span></span>
* <span data-ttu-id="38c7e-159">傳統入口網站中不同的來源點</span><span class="sxs-lookup"><span data-stu-id="38c7e-159">The different sourcing point in the classic portal</span></span>

<span data-ttu-id="38c7e-160">不過，除非**全域管理員**加以允許，否則將**擁有者**或**參與者**存取權授與給**訂用帳戶**範圍內的外部使用者，並不允許存取管理使用者的目錄。</span><span class="sxs-lookup"><span data-stu-id="38c7e-160">However, granting **Owner** or **Contributor** access to an external user at the **Subscription** scope, does not allow the access to the admin user's directory, unless the **Global Admin** allows it.</span></span> <span data-ttu-id="38c7e-161">在使用者內容中，可以識別具有 **Member** 和 **Guest** 這兩個常見的參數的**使用者類型**。</span><span class="sxs-lookup"><span data-stu-id="38c7e-161">In the user proprieties,  the **User Type** which has two common parameters, **Member** and **Guest** can be identified.</span></span> <span data-ttu-id="38c7e-162">當來賓為外部來源受邀至目錄的使用者時，在目錄中登錄的使用者就是成員。</span><span class="sxs-lookup"><span data-stu-id="38c7e-162">A member is a user which is registered in the directory while a guest is a user invited to the directory from an external source.</span></span> <span data-ttu-id="38c7e-163">如需詳細資訊，請參閱 [Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者](/active-directory/active-directory-b2b-admin-add-users)。</span><span class="sxs-lookup"><span data-stu-id="38c7e-163">For more information, see [How do Azure Active Directory admins add B2B collaboration users](/active-directory/active-directory-b2b-admin-add-users).</span></span>

> [!NOTE]
> <span data-ttu-id="38c7e-164">在入口網站中輸入認證後，請確定外部使用者選取正確的目錄進行登入。</span><span class="sxs-lookup"><span data-stu-id="38c7e-164">Make sure that after entering the credentials in the portal, the external user selects the correct directory to sign-in to.</span></span> <span data-ttu-id="38c7e-165">相同使用者可以存取多個目錄，並且可以選擇其中一個目錄，方法是按一下 Azure 入口網站右上角的使用者名稱，然後從下拉式清單中選取適當的目錄。</span><span class="sxs-lookup"><span data-stu-id="38c7e-165">The same user can have access to multiple directories and can select either one of  them by clicking the username in the top right-hand side in the Azure portal and then choose the appropriate directory from the dropdown list.</span></span>

<span data-ttu-id="38c7e-166">在目錄中使用來賓身分時，外部使用者可以管理 Azure 訂用帳戶的所有資源，但無法存取目錄。</span><span class="sxs-lookup"><span data-stu-id="38c7e-166">While being a guest in the directory, the external user can manage all resources for the Azure subscription, but can't access the directory.</span></span>





![存取限於 Azure Active Directory Azure 入口網站](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

<span data-ttu-id="38c7e-168">Azure Active Directory 和 Azure 訂用帳戶沒有父子式關聯性，如同其他 Azure 資源 (例如︰虛擬機器、虛擬網路、Web Apps、儲存體等) 與 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="38c7e-168">Azure Active Directory and an Azure subscription don't have a child-parent relation like other Azure resources (for example: virtual machines, virtual networks, web apps, storage etc.) have with an Azure subscription.</span></span> <span data-ttu-id="38c7e-169">將 Azure 訂用帳戶用來管理 Azure 目錄的存取權時，所有後者會建立在 Azure 訂用帳戶下，並加以管理和計費。</span><span class="sxs-lookup"><span data-stu-id="38c7e-169">All the latter is created, managed and billed under an Azure subscription while an Azure subscription is used to manage the access to an Azure directory.</span></span> <span data-ttu-id="38c7e-170">如需詳細資訊，請參閱 [Azure 訂用帳戶與 Azure AD 有何相關](/active-directory/active-directory-how-subscriptions-associated-directory)。</span><span class="sxs-lookup"><span data-stu-id="38c7e-170">For more details, see [How an Azure subscription is related to Azure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span></span>

<span data-ttu-id="38c7e-171">所有內建 RBAC 角色的**擁有者**和**參與者**會提供對環境中所有資源的完整管理存取權，差異在於參與者無法建立新的 RBAC 角色並加以刪除。</span><span class="sxs-lookup"><span data-stu-id="38c7e-171">From all the built-in RBAC roles, **Owner** and **Contributor** offer full management access to all resources in the environment, the difference being that a Contributor can't create and delete new RBAC roles.</span></span> <span data-ttu-id="38c7e-172">其他內建角色 (例如**虛擬機器參與者**) 僅對該名稱所表示的資源提供完整管理存取權，不論它們要建立在哪一個**資源群組**。</span><span class="sxs-lookup"><span data-stu-id="38c7e-172">The other built-in roles like **Virtual Machine Contributor** offer full management access only to the resources indicated by the name, regardless of the **Resource Group** they are being created into.</span></span>

<span data-ttu-id="38c7e-173">在訂用帳戶等級指派**虛擬機器參與者**的內建 RBAC 角色，表示使用者指派角色︰</span><span class="sxs-lookup"><span data-stu-id="38c7e-173">Assigning the built-in RBAC role of **Virtual Machine Contributor** at a subscription level, means that the user assigned the role:</span></span>

* <span data-ttu-id="38c7e-174">可以檢視所有虛擬機器，不論其部署日期和所屬的資源群組</span><span class="sxs-lookup"><span data-stu-id="38c7e-174">Can view all virtual machines regardless their deployment date and the resource groups they are part of</span></span>
* <span data-ttu-id="38c7e-175">具有訂用帳戶中虛擬機器的完整管理存取權</span><span class="sxs-lookup"><span data-stu-id="38c7e-175">Has full management access to the virtual machines in the subscription</span></span>
* <span data-ttu-id="38c7e-176">無法檢視訂用帳戶中任何其他資源類型</span><span class="sxs-lookup"><span data-stu-id="38c7e-176">Can't view any other resource types in the subscription</span></span>
* <span data-ttu-id="38c7e-177">無法從計費觀點來操作任何變更</span><span class="sxs-lookup"><span data-stu-id="38c7e-177">Can't operate any changes from a billing perspective</span></span>

> [!NOTE]
> <span data-ttu-id="38c7e-178">RBAC 是僅限 Azure 入口網站使用的功能，它不會授與傳統入口網站的存取權。</span><span class="sxs-lookup"><span data-stu-id="38c7e-178">RBAC being an Azure portal only feature, it doesn't grant access to the classic portal.</span></span>

## <a name="assign-a-built-in-rbac-role-to-an-external-user"></a><span data-ttu-id="38c7e-179">將內建的 RBAC 角色指派給外部使用者</span><span class="sxs-lookup"><span data-stu-id="38c7e-179">Assign a built-in RBAC role to an external user</span></span>
<span data-ttu-id="38c7e-180">這項測試的不同案例中，會將外部使用者 "alflanigan@gmail.com" 新增為**虛擬機器參與者**。</span><span class="sxs-lookup"><span data-stu-id="38c7e-180">For a different scenario in this test, the external user "alflanigan@gmail.com" is added as a **Virtual Machine Contributor**.</span></span>




![虛擬機器參與者內建角色](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

<span data-ttu-id="38c7e-182">這個具有此內建角色之外部使用者的正常行為，就是僅查看和管理虛擬機器，以及其相鄰 Resource Manager 僅在部署時所需的資源。</span><span class="sxs-lookup"><span data-stu-id="38c7e-182">The normal behavior for this external user with this built-in role is to see and manage only virtual machines and their adjacent Resource Manager only resources necessary while deploying.</span></span> <span data-ttu-id="38c7e-183">根據設計，這些限制的角色只會向他們在 Azure 入口網站中建立的對應資源提供存取權，不論部分角色仍可部署在傳統入口網站中 (例如︰虛擬機器)。</span><span class="sxs-lookup"><span data-stu-id="38c7e-183">By design, these limited roles offer access only to their correspondent resources created in the Azure portal, regardless some can still be deployed in the classic portal as well (for example: virtual machines).</span></span>





![Azure 入口網站中的虛擬機器參與者角色概觀](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-the-same-directory"></a><span data-ttu-id="38c7e-185">為相同目錄中的使用者授與訂用帳戶等級的存取權</span><span class="sxs-lookup"><span data-stu-id="38c7e-185">Grant access at a subscription level for a user in the same directory</span></span>
<span data-ttu-id="38c7e-186">程序流程與新增外部使用者的相同，從授與 RBAC 角色的系統管理員觀點以及取得角色存取權的使用者皆然。</span><span class="sxs-lookup"><span data-stu-id="38c7e-186">The process flow is identical to adding an external user, both from the admin perspective granting the RBAC role as well as the user being granted access to the role.</span></span> <span data-ttu-id="38c7e-187">此處的差異在於，受邀的使用者無法接收任何電子郵件邀請，因為訂用帳戶內的所有資源範圍在登入之後都會在儀表板中提供使用。</span><span class="sxs-lookup"><span data-stu-id="38c7e-187">The difference here is that the invited user will not receive any email invitations as all the resource scopes within the subscription will be available in the dashboard after signing in.</span></span>

## <a name="assign-rbac-roles-at-the-resource-group-scope"></a><span data-ttu-id="38c7e-188">指派資源群組範圍內的 RBAC 角色</span><span class="sxs-lookup"><span data-stu-id="38c7e-188">Assign RBAC roles at the resource group scope</span></span>
<span data-ttu-id="38c7e-189">對於兩種類型的使用者 - 外部或內部 (相同目錄的一部分)，指派**資源群組**範圍內的 RBAC 角色與指派訂用帳戶等級的角色程序相同。</span><span class="sxs-lookup"><span data-stu-id="38c7e-189">Assigning an RBAC role at a **Resource Group** scope has an identical process for assigning the role at the subscription level, for both types of users - either external or internal (part of the same directory).</span></span> <span data-ttu-id="38c7e-190">獲指派 RBAC 角色的使用者只會在其環境中看到已從 Azure 入口網站中的**資源群組**圖示指派存取權的資源群組。</span><span class="sxs-lookup"><span data-stu-id="38c7e-190">The users which are assigned the RBAC role is to see in their environment only the resource group they have been assigned access from the **Resource Groups** icon in the Azure portal.</span></span>

## <a name="assign-rbac-roles-at-the-resource-scope"></a><span data-ttu-id="38c7e-191">指派資源範圍內的 RBAC 角色</span><span class="sxs-lookup"><span data-stu-id="38c7e-191">Assign RBAC roles at the resource scope</span></span>
<span data-ttu-id="38c7e-192">在 Azure 中指派資源範圍內的角色與指派訂用帳戶等級或資源群組等級的角色程序相同，這兩個案例皆遵循相同的工作流程。</span><span class="sxs-lookup"><span data-stu-id="38c7e-192">Assigning an RBAC role at a resource scope in Azure has an identical process for assigning the role at the subscription level or at the resource group level, following the same workflow for both scenarios.</span></span> <span data-ttu-id="38c7e-193">同樣地，獲指派 RBAC 角色的使用者只能在 [所有資源] 索引標籤或直接在儀表板中，看到他們已獲指派可存取的項目。</span><span class="sxs-lookup"><span data-stu-id="38c7e-193">Again, the users which are assigned the RBAC role can see only the items that they have been assigned access to, either in the **All Resources** tab or directly in their dashboard.</span></span>

<span data-ttu-id="38c7e-194">在資源群組範圍或資源範圍內之 RBAC 的一個重點是，讓使用者確定登入正確的目錄。</span><span class="sxs-lookup"><span data-stu-id="38c7e-194">An important aspect for RBAC both at resource group scope or resource scope is for the users to make sure to sign-in to the correct directory.</span></span>





![Azure 入口網站中的目錄登入](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a><span data-ttu-id="38c7e-196">為 Azure Active Directory 群組指派 RBAC 角色</span><span class="sxs-lookup"><span data-stu-id="38c7e-196">Assign RBAC roles for an Azure Active Directory group</span></span>
<span data-ttu-id="38c7e-197">在 Azure 中三個不同的範圍使用 RBAC 的所有案例，都提供以指派的使用者身分管理、部署和系統管理各種資源，而不需要管理個人訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="38c7e-197">All the scenarios using RBAC at the three different scopes in Azure offer the privilege of managing, deploying and administering various resources as an assigned user without the need of managing a personal subscription.</span></span> <span data-ttu-id="38c7e-198">無論 RBAC 角色是指派給訂用帳戶、資源群組還是資源範圍，所有已指派的使用者所進一步建立的資源，都會以使用者擁有存取權的其中一個 Azure 訂用帳戶加以計費。</span><span class="sxs-lookup"><span data-stu-id="38c7e-198">Regardless the RBAC role is assigned for a subscription, resource group or resource scope, all the resources created further on by the assigned users are billed under the one Azure subscription where the users have access to.</span></span> <span data-ttu-id="38c7e-199">如此一來，擁有整個 Azure 訂用帳戶計費系統管理員權限的使用者，可以完整概觀耗用量，不論資源管理者是誰。</span><span class="sxs-lookup"><span data-stu-id="38c7e-199">This way, the users who have billing administrator permissions for that entire Azure subscription has a complete overview on the consumption, regardless who is managing the resources.</span></span>

<span data-ttu-id="38c7e-200">對於較大型組織，考慮到管理使用者想要將細微存取授與小組或整個部門的方面，而非個別授與每位使用者，可透過相同的方式來套用 Azure Active Directory 群組的 RBAC 角色，因此考慮將它作為非常有效率的時間和管理選項。</span><span class="sxs-lookup"><span data-stu-id="38c7e-200">For larger organizations, RBAC roles can be applied in the same way for Azure Active Directory groups considering the perspective that the admin user wants to grant the granular access for teams or entire departments, not individually for each user, thus considering it as an extremely time and management efficient option.</span></span> <span data-ttu-id="38c7e-201">為了說明此範例中，**參與者**角色已新增至訂用帳戶等級之租用戶的其中一個群組。</span><span class="sxs-lookup"><span data-stu-id="38c7e-201">To illustrate this example, the **Contributor** role has been added to one of the groups in the tenant at the subscription level.</span></span>





![新增 AAD 群組的 RBAC 角色](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

<span data-ttu-id="38c7e-203">這些群組都是安全性群組，只在 Azure Active Directory 內進行佈建和管理。</span><span class="sxs-lookup"><span data-stu-id="38c7e-203">These groups are security groups which are provisioned and managed only within Azure Active Directory.</span></span>

## <a name="create-a-custom-rbac-role-to-open-support-requests-using-powershell"></a><span data-ttu-id="38c7e-204">建立自訂的 RBAC 角色，才能使用 PowerShell 開啟支援要求</span><span class="sxs-lookup"><span data-stu-id="38c7e-204">Create a custom RBAC role to open support requests using PowerShell</span></span>
<span data-ttu-id="38c7e-205">Azure 中提供的內建 RBAC 角色會以環境中可用的資源作為基礎來確保特定權限等級。</span><span class="sxs-lookup"><span data-stu-id="38c7e-205">The built-in RBAC roles which are available in Azure ensure certain permission levels based on the available resources in the environment.</span></span> <span data-ttu-id="38c7e-206">不過，如果這些角色都不符合管理使用者的需求，可透過建立自訂的 RBAC 角色，選擇限制更多存取權。</span><span class="sxs-lookup"><span data-stu-id="38c7e-206">However, if none of these roles suit the admin user's needs, there is the option to limit access even more by creating custom RBAC roles.</span></span>

<span data-ttu-id="38c7e-207">建立自訂的 RBAC 角色需要採用一個內建角色、加以編輯，然後將它匯入回環境中。</span><span class="sxs-lookup"><span data-stu-id="38c7e-207">Creating custom RBAC roles requires to take one built-in role, edit it and then import it back in the environment.</span></span> <span data-ttu-id="38c7e-208">會使用 PowerShell 或 CLI 來管理角色的上傳與下載。</span><span class="sxs-lookup"><span data-stu-id="38c7e-208">The download and upload of the role are managed using either PowerShell or CLI.</span></span>

<span data-ttu-id="38c7e-209">請務必了解建立自訂角色的必要條件，其可授與訂用帳戶等級的細微存取權，並且提供受邀使用者開啟支援要求的彈性。</span><span class="sxs-lookup"><span data-stu-id="38c7e-209">It is important to understand the prerequisites of creating a custom role which can grant granular access at the subscription level and also allow the invited user the flexibility of opening support requests.</span></span>

<span data-ttu-id="38c7e-210">此範例中，讓使用者可存取並檢視所有資源範圍，但不能加以編輯或新建的內建角色**讀取器**已進行自訂，可供使用者選擇開啟支援要求。</span><span class="sxs-lookup"><span data-stu-id="38c7e-210">For this example the built-in role **Reader** which allows users access to view all the resource scopes but not to edit them or create new ones has been customized to allow the user the option of opening support requests.</span></span>

<span data-ttu-id="38c7e-211">將**讀取器**角色匯出的第一個動作，必須在以系統管理員身分透過提高權限執行的 PowerShell 中完成。</span><span class="sxs-lookup"><span data-stu-id="38c7e-211">The first action of exporting the **Reader** role needs to be completed in PowerShell ran with elevated permissions as administrator.</span></span>

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![讀取器 RBAC 角色的 PowerShell 螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

<span data-ttu-id="38c7e-213">然後，您必須擷取角色的 JSON 範本。</span><span class="sxs-lookup"><span data-stu-id="38c7e-213">Then you need to extract the JSON template of the role.</span></span>





![自訂讀取器 RBAC 角色的 JSON 範本](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

<span data-ttu-id="38c7e-215">典型的 RBAC 角色是由三個主要區段所組成︰**Actions**、**NotActions** 和 **AssignableScopes**。</span><span class="sxs-lookup"><span data-stu-id="38c7e-215">A typical RBAC role is composed out of three main sections, **Actions**, **NotActions** and **AssignableScopes**.</span></span>

<span data-ttu-id="38c7e-216">在**動作**區段中，會列出此角色所有允許的作業。</span><span class="sxs-lookup"><span data-stu-id="38c7e-216">In the **Action** section are listed all the permitted operations for this role.</span></span> <span data-ttu-id="38c7e-217">請務必了解，每個動作都會從資源提供者加以指派。</span><span class="sxs-lookup"><span data-stu-id="38c7e-217">It's important to understand that each action is assigned from a resource provider.</span></span> <span data-ttu-id="38c7e-218">在此情況下，必須列出 **Microsoft.Support** 資源提供者才能建立支援票證。</span><span class="sxs-lookup"><span data-stu-id="38c7e-218">In this case, for creating support tickets the **Microsoft.Support** resource provider must be listed.</span></span>

<span data-ttu-id="38c7e-219">若要查看所有可用且已在您訂用帳戶中登錄的資源提供者，您可以使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="38c7e-219">To be able to see all the resource providers available and registered in your subscription, you can use PowerShell.</span></span>
```
Get-AzureRMResourceProvider

```
<span data-ttu-id="38c7e-220">此外，您可以檢查所有可用的 PowerShell Cmdlet 來管理資源提供者。</span><span class="sxs-lookup"><span data-stu-id="38c7e-220">Additionally, you can check for the all the available PowerShell cmdlets to manage the resource providers.</span></span>
    <span data-ttu-id="38c7e-221">![資源提供者管理的 PowerShell 螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span><span class="sxs-lookup"><span data-stu-id="38c7e-221">![PowerShell screenshot for resource provider management](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span></span>

<span data-ttu-id="38c7e-222">為限制特定 RBAC 角色的所有動作，會在 **NotActions** 一節中列出資源提供者。</span><span class="sxs-lookup"><span data-stu-id="38c7e-222">To restrict all the actions for a particular RBAC role, resource providers are listed under the section **NotActions**.</span></span>
<span data-ttu-id="38c7e-223">最後，在使用 RBAC 角色的位置必須包含明確的訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="38c7e-223">Last, it's mandatory that the RBAC role contains the explicit subscription IDs where it is used.</span></span> <span data-ttu-id="38c7e-224">訂用帳戶識別碼會列在 **AssignableScopes** 下，否則不允許您將角色匯入您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="38c7e-224">The subscription IDs are listed under the **AssignableScopes**, otherwise you will not be allowed to import the role in your subscription.</span></span>

<span data-ttu-id="38c7e-225">建立並自訂 RBAC 角色之後，必須將它匯入回環境。</span><span class="sxs-lookup"><span data-stu-id="38c7e-225">After creating and customizing the RBAC role, it needs to be imported back the environment.</span></span>

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

<span data-ttu-id="38c7e-226">在此範例中，此 RBAC 角色的自訂名稱為「讀取器支援票證存取等級」，讓使用者可檢視訂用帳戶中的所有項目，並且開啟支援要求。</span><span class="sxs-lookup"><span data-stu-id="38c7e-226">In this example, the custom name for this RBAC role is "Reader support tickets access level" allowing the user to view everything in the subscription and also to open support requests.</span></span>

> [!NOTE]
> <span data-ttu-id="38c7e-227">允許開啟支援要求的兩個內建 RBAC 角色動作是**擁有者**和**參與者**。</span><span class="sxs-lookup"><span data-stu-id="38c7e-227">The only two built-in RBAC roles allowing the action of opening of support requests are **Owner** and **Contributor**.</span></span> <span data-ttu-id="38c7e-228">使用者若要開啟支援要求，必須僅獲指派訂用帳戶範圍內的 RBAC 角色，因為所有支援要求都會以 Azure 訂用帳戶作為基礎加以建立。</span><span class="sxs-lookup"><span data-stu-id="38c7e-228">For a user to be able to open support requests, he must be assigned an RBAC role only at the subscription scope, because all support requests are created based on an Azure subscription.</span></span>

<span data-ttu-id="38c7e-229">已從相同的目錄將這個新的自訂角色指派給使用者。</span><span class="sxs-lookup"><span data-stu-id="38c7e-229">This new custom role has been assigned to an user from the same directory.</span></span>





![匯入 Azure 入口網站之自訂 RBAC 角色的螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![將自訂匯入的 RBAC 角色指派給相同目錄中之使用者的螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![自訂匯入的 RBAC 角色之權限的螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

<span data-ttu-id="38c7e-233">此範例已進一步詳細說明，強調此自訂 RBAC 角色的限制，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="38c7e-233">The example has been further detailed to emphasize the limits of this custom RBAC role as follows:</span></span>
* <span data-ttu-id="38c7e-234">可以建立新的支援要求</span><span class="sxs-lookup"><span data-stu-id="38c7e-234">Can create new support requests</span></span>
* <span data-ttu-id="38c7e-235">無法建立新的資源範圍 (例如︰虛擬機器)</span><span class="sxs-lookup"><span data-stu-id="38c7e-235">Can't create new resource scopes (for example: virtual machine)</span></span>
* <span data-ttu-id="38c7e-236">無法建立新的資源群組</span><span class="sxs-lookup"><span data-stu-id="38c7e-236">Can't create new resource groups</span></span>





![建立支援要求之自訂 RBAC 角色的螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![無法建立 VM 之自訂 RBAC 角色的螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![無法建立新 RG 之自訂 RBAC 角色的螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-to-open-support-requests-using-azure-cli"></a><span data-ttu-id="38c7e-240">建立自訂的 RBAC 角色，才能使用 Azure CLI 開啟支援要求</span><span class="sxs-lookup"><span data-stu-id="38c7e-240">Create a custom RBAC role to open support requests using Azure CLI</span></span>
<span data-ttu-id="38c7e-241">在 Mac 上執行而不需要存取 PowerShell，Azure CLI 就是最好的選擇。</span><span class="sxs-lookup"><span data-stu-id="38c7e-241">Running on a Mac and without having access to PowerShell, Azure CLI is the way to go.</span></span>

<span data-ttu-id="38c7e-242">建立自訂角色的步驟都相同，唯一的例外狀況是，使用 CLI，就無法在 JSON 範本中下載角色，但可以在 CLI 中加以檢視。</span><span class="sxs-lookup"><span data-stu-id="38c7e-242">The steps to create a custom role are the same, with the sole exception that using CLI the role can't be downloaded in a JSON template, but it can be viewed in the CLI.</span></span>

<span data-ttu-id="38c7e-243">此範例中，我選擇的內建角色是**備份讀取器**。</span><span class="sxs-lookup"><span data-stu-id="38c7e-243">For this example I have chosen the built-in role of **Backup Reader**.</span></span>

```

azure role show "backup reader" --json

```





![備份讀取器角色顯示的 CLI 螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

<span data-ttu-id="38c7e-245">在 JSON 範本中複製內容後編輯 Visual Studio 中的角色，已在**動作**區段中新增 **Microsoft.Support** 資源提供者，讓這個使用者可以開啟支援要求，同時可繼續當作備份保存庫的讀取器。</span><span class="sxs-lookup"><span data-stu-id="38c7e-245">Editing the role in Visual Studio after copying the proprieties in a JSON template, the **Microsoft.Support** resource provider has been added in the **Actions** sections so that this user can open support requests while continuing to be a reader for the backup vaults.</span></span> <span data-ttu-id="38c7e-246">同樣地，在 **AssignableScopes** 區段中要使用此角色的位置必須新增訂用帳戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="38c7e-246">Again it is necessary to add the subscription ID where this role will be used in the **AssignableScopes** section.</span></span>

```

azure role create --inputfile <path>

```





![匯入自訂 RBAC 角色的 CLI 螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

<span data-ttu-id="38c7e-248">現在可於 Azure 入口網站中使用新角色，指派程序與先前範例中的相同。</span><span class="sxs-lookup"><span data-stu-id="38c7e-248">The new role is now available in the Azure portal and the assignation process is the same as in the previous examples.</span></span>





![使用 CLI 1.0 所建立之自訂 RBAC 角色的 Azure 入口網站螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

<span data-ttu-id="38c7e-250">從最新的組建 2017 起，Azure Cloud Shell 已正式推出。</span><span class="sxs-lookup"><span data-stu-id="38c7e-250">As of the latest Build 2017, the Azure Cloud Shell is generally available.</span></span> <span data-ttu-id="38c7e-251">Azure Cloud Shell 是 IDE 和 Azure 入口網站的補充。</span><span class="sxs-lookup"><span data-stu-id="38c7e-251">Azure Cloud Shell is a complement to IDE and the Azure Portal.</span></span> <span data-ttu-id="38c7e-252">您可以利用此服務，取得經過驗證且裝載於 Azure 內以瀏覽器為基礎的殼層，您可以使用它而不使用安裝在您電腦上的 CLI。</span><span class="sxs-lookup"><span data-stu-id="38c7e-252">With this service, you get a browser-based shell that is authenticated and hosted within Azure and you can use it instead of CLI installed on your machine.</span></span>





![Azure Cloud Shell](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
