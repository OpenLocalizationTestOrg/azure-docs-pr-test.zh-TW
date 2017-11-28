---
title: "aaaCreate 自訂角色型存取控制角色並指派 toointernal 和在 Azure 中的外部使用者 |Microsoft 文件"
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
ms.openlocfilehash: 26793a66d6ca2f771338eed87d10ce2b3b431841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="intro-on-role-based-access-control"></a><span data-ttu-id="d5b7e-103">角色型存取控制簡介</span><span class="sxs-lookup"><span data-stu-id="d5b7e-103">Intro on role-based access control</span></span>

<span data-ttu-id="d5b7e-104">以角色為基礎的存取控制是 Azure 入口網站只功能允許 hello 訂用帳戶的擁有者 tooassign 細微角色 tooother 使用者可以在其環境中管理特定資源。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-104">Role-based access control is an Azure portal only feature allowing hello owners of a subscription tooassign granular roles tooother users who can manage specific resource scopes in their environment.</span></span>

<span data-ttu-id="d5b7e-105">RBAC 可讓大型組織及 Smb 的較佳的安全性管理的外部共同作業者、 廠商或 freelancers 需要存取您的環境，但不是一定 toohello 整個基礎結構或任何 toospecific 資源計費相關的範圍。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-105">RBAC allows better security management for large organizations and for SMBs working with external collaborators, vendors or freelancers which need access toospecific resources in your environment but not necessarily toohello entire infrastructure or any billing-related scopes.</span></span> <span data-ttu-id="d5b7e-106">RBAC 允許 hello 彈性擁有一個 hello 系統管理員帳戶 （服務在訂用帳戶層級的系統管理員角色） 所管理的 Azure 訂閱並擁有多個受邀使用者 toowork 下的 hello 相同訂用帳戶但不含任何系統管理它的權限。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-106">RBAC allows hello flexibility of owning one Azure subscription managed by hello administrator account (service administrator role at a subscription level) and have multiple users invited toowork under hello same subscription but without any administrative rights for it.</span></span> <span data-ttu-id="d5b7e-107">從管理和計費的觀點而言，hello RBAC 功能證明 toobe 在各種情況中使用 Azure 的階段和管理有效選項。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-107">From a management and billing perspective, hello RBAC feature proves toobe a time and management efficient option for using Azure in various scenarios.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5b7e-108">必要條件</span><span class="sxs-lookup"><span data-stu-id="d5b7e-108">Prerequisites</span></span>
<span data-ttu-id="d5b7e-109">使用 RBAC hello Azure 環境中需要：</span><span class="sxs-lookup"><span data-stu-id="d5b7e-109">Using RBAC in hello Azure environment requires:</span></span>

* <span data-ttu-id="d5b7e-110">具有獨立的 Azure 訂用帳戶指派 toohello 使用者作為擁有者 （訂用帳戶的角色）</span><span class="sxs-lookup"><span data-stu-id="d5b7e-110">Having a standalone Azure subscription assigned toohello user as owner (subscription role)</span></span>
* <span data-ttu-id="d5b7e-111">擁有 hello 的 hello Azure 訂用帳戶的擁有者角色</span><span class="sxs-lookup"><span data-stu-id="d5b7e-111">Have hello Owner role of hello Azure subscription</span></span>
* <span data-ttu-id="d5b7e-112">具有存取 toohello [Azure 入口網站](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="d5b7e-112">Have access toohello [Azure portal](https://portal.azure.com)</span></span>
* <span data-ttu-id="d5b7e-113">請確定下列資源提供者的 toohave hello 註冊 hello 使用者訂用帳戶： **apiversion**。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-113">Make sure toohave hello following Resource Providers registered for hello user subscription: **Microsoft.Authorization**.</span></span> <span data-ttu-id="d5b7e-114">如需有關如何 tooregister hello 資源提供者的詳細資訊，請參閱[資源管理員提供者、 區域、 應用程式開發介面版本和結構描述](/azure-resource-manager/resource-manager-supported-services.md)。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-114">For more information on how tooregister hello resource providers, see [Resource Manager providers, regions, API versions and schemas](/azure-resource-manager/resource-manager-supported-services.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d5b7e-115">Office 365 訂閱或 Azure Active Directory 的授權 (例如： 存取 tooAzure Active Directory) hello O365 入口網站不品質使用 RBAC 佈建。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-115">Office 365 subscriptions or Azure Active Directory licenses (for example: Access tooAzure Active Directory) provisioned from hello O365 portal don't quality for using RBAC.</span></span>

## <a name="how-can-rbac-be-used"></a><span data-ttu-id="d5b7e-116">如何使用 RBAC</span><span class="sxs-lookup"><span data-stu-id="d5b7e-116">How can RBAC be used</span></span>
<span data-ttu-id="d5b7e-117">RBAC 在 Azure 中可套用於三個不同範圍。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-117">RBAC can be applied at three different scopes in Azure.</span></span> <span data-ttu-id="d5b7e-118">從 hello 最高範圍 toohello 最低的其中一個，這些屬性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d5b7e-118">From hello highest scope toohello lowest one, they are as follows:</span></span>

* <span data-ttu-id="d5b7e-119">訂用帳戶 (最高)</span><span class="sxs-lookup"><span data-stu-id="d5b7e-119">Subscription (highest)</span></span>
* <span data-ttu-id="d5b7e-120">資源群組</span><span class="sxs-lookup"><span data-stu-id="d5b7e-120">Resource group</span></span>
* <span data-ttu-id="d5b7e-121">資源範圍 （hello 最低存取層級提供目標的權限 tooan 個別 Azure 資源的範圍）</span><span class="sxs-lookup"><span data-stu-id="d5b7e-121">Resource scope (hello lowest access level offering targeted permissions tooan individual Azure resource scope)</span></span>

## <a name="assign-rbac-roles-at-hello-subscription-scope"></a><span data-ttu-id="d5b7e-122">將在 hello 訂用帳戶範圍 RBAC 角色指派</span><span class="sxs-lookup"><span data-stu-id="d5b7e-122">Assign RBAC roles at hello subscription scope</span></span>
<span data-ttu-id="d5b7e-123">使用 RBAC 時，有兩個常見的範例 (但是不限於)︰</span><span class="sxs-lookup"><span data-stu-id="d5b7e-123">There are two common examples when RBAC is used (but not limited to):</span></span>

* <span data-ttu-id="d5b7e-124">讓外部使用者從 hello 組織 （非 hello 系統管理使用者的 Azure Active Directory 租用戶的一部分），受邀 toomanage 特定資源或 hello 整個訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="d5b7e-124">Having external users from hello organizations (not part of hello admin user's Azure Active Directory tenant) invited toomanage certain resources or hello whole subscription</span></span>
* <span data-ttu-id="d5b7e-125">Hello 組織 （它們是 hello 使用者的 Azure Active Directory 租用戶的一部分），但屬於不同的小組或需要細微的存取權限的群組內部使用者使用任一 toohello 整個訂用帳戶或 toocertain 資源群組或資源的範圍限制在 hello環境</span><span class="sxs-lookup"><span data-stu-id="d5b7e-125">Working with users inside hello organization (they are part of hello user's Azure Active Directory tenant) but part of different teams or groups which need granular access either toohello whole subscription or toocertain resource groups or resource scopes in hello environment</span></span>

## <a name="grant-access-at-a-subscription-level-for-a-user-outside-of-azure-active-directory"></a><span data-ttu-id="d5b7e-126">為 Azure Active Directory 外部的使用者授與訂用帳戶等級的存取權</span><span class="sxs-lookup"><span data-stu-id="d5b7e-126">Grant access at a subscription level for a user outside of Azure Active Directory</span></span>
<span data-ttu-id="d5b7e-127">RBAC 角色可授與只由**擁有者**hello 訂用帳戶的因此 hello 系統管理使用者必須使用登已預先指派此角色，或建立 hello Azure 訂用帳戶的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-127">RBAC roles can be granted only by **Owners** of hello subscription therefore hello admin user must be logged with a username which has this role pre-assigned or has created hello Azure subscription.</span></span>

<span data-ttu-id="d5b7e-128">從 hello Azure 入口網站之後您, 登入為系統管理員，選取 「 訂閱 」 並選擇 hello 所需的其中一個。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-128">From hello Azure portal, after you sign-in as admin, select “Subscriptions” and chose hello desired one.</span></span>
<span data-ttu-id="d5b7e-129">![在 Azure 入口網站中的訂用帳戶] 刀鋒視窗](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png)根據預設，如果 hello [系統管理使用者已購買 hello Azure 訂用帳戶，hello 使用者會顯示為**帳戶管理員**，這個正在 hello 訂用帳戶角色。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-129">![subscription blade in Azure portal](./media/role-based-access-control-create-custom-roles-for-internal-external-users/0.png) By default, if hello admin user has purchased hello Azure subscription, hello user will show up as **Account Admin**, this being hello subscription role.</span></span> <span data-ttu-id="d5b7e-130">如需有關 hello Azure 訂用帳戶的角色的詳細資訊，請參閱[hello 訂用帳戶或服務管理的新增或變更 Azure 系統管理員角色](/billing/billing-add-change-azure-subscription-administrator.md)。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-130">For more details on hello Azure subscription roles, see [Add or change Azure administrator roles that manage hello subscription or services](/billing/billing-add-change-azure-subscription-administrator.md).</span></span>

<span data-ttu-id="d5b7e-131">在此範例中，hello 使用者 」alflanigan@outlook.com」 為 hello**擁有者**hello 「 免費試用版 」 的訂用帳戶中 hello AAD 租用戶 「 預設的 Azure 租用戶 」。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-131">In this example, hello user "alflanigan@outlook.com" is hello **Owner** of hello "Free Trial" subscription in hello AAD tenant "Default tenant Azure".</span></span> <span data-ttu-id="d5b7e-132">因為此使用者是 hello Azure 訂用帳戶以 hello hello 建立者的初始 Outlook 」 的 Microsoft 帳戶 (Microsoft 帳戶 = Outlook，Live 等) hello 預設加入此租用戶中的所有其他使用者的網域名稱將會**"@alflaniganuoutlook.onmicrosoft.com"**.</span><span class="sxs-lookup"><span data-stu-id="d5b7e-132">Since this user is hello creator of hello Azure subscription with hello initial Microsoft Account “Outlook” (Microsoft Account = Outlook, Live etc.) hello default domain name for all other users added in this tenant will be **"@alflaniganuoutlook.onmicrosoft.com"**.</span></span> <span data-ttu-id="d5b7e-133">根據設計，hello 語法 hello 新網域的構成方式放在一起 hello 使用者名稱和網域名稱建立 hello 租用戶和新增 hello 延伸模組的 hello 使用者**"。 onmicrosoft.com"**。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-133">By design, hello syntax of hello new domain is formed by putting together hello username and domain name of hello user who created hello tenant and adding hello extension **".onmicrosoft.com"**.</span></span>
<span data-ttu-id="d5b7e-134">此外，使用者可以登入與 hello 租用戶中的自訂網域名稱新增並驗證 hello 新租用戶後。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-134">Furthermore, users can sign-in with a custom domain name in hello tenant after adding and verifying it for hello new tenant.</span></span> <span data-ttu-id="d5b7e-135">如需有關如何 tooverify 自訂網域名稱中的 Azure Active Directory 租用戶，請參閱[新增自訂網域名稱 tooyour 目錄](/active-directory/active-directory-add-domain)。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-135">For more details on how tooverify a custom domain name in an Azure Active Directory tenant, see [Add a custom domain name tooyour directory](/active-directory/active-directory-add-domain).</span></span>

<span data-ttu-id="d5b7e-136">在此範例中，hello"預設租用戶 Azure"目錄包含只有具備 hello 網域名稱的使用者 」@alflanigan.onmicrosoft.com"。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-136">In this example, hello "Default tenant Azure" directory contains only users with hello domain name "@alflanigan.onmicrosoft.com".</span></span>

<span data-ttu-id="d5b7e-137">Hello 系統管理使用者必須按一下 選取 hello 訂用帳戶之後,**存取控制 (IAM)**然後**加入新的角色**。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-137">After selecting hello subscription, hello admin user must click **Access Control (IAM)** and then **Add a new role**.</span></span>





![Azure 入口網站中的存取控制 IAM 功能](./media/role-based-access-control-create-custom-roles-for-internal-external-users/1.png)





![在 Azure 入口網站的存取控制 IAM 功能中新增使用者](./media/role-based-access-control-create-custom-roles-for-internal-external-users/2.png)

<span data-ttu-id="d5b7e-140">hello 下一個步驟是 tooselect hello 角色 toobe 指派和 hello hello RBAC 角色會指派給使用者。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-140">hello next step is tooselect hello role toobe assigned and hello user whom hello RBAC role will be assigned to.</span></span> <span data-ttu-id="d5b7e-141">在 hello**角色**下拉式功能表 hello 系統管理使用者會看到只有 hello 內建 RBAC 角色在 Azure 中可用的。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-141">In hello **Role** dropdown menu hello admin user sees only hello built-in RBAC roles which are available in Azure.</span></span> <span data-ttu-id="d5b7e-142">如需每個角色及其可指派範圍的詳細說明，請參閱 [Azure 角色型存取控制的內建角色](/active-directory/role-based-access-built-in-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-142">For more detailed explanations of each role and their assignable scopes, see [Built-in roles for Azure Role-Based Access Control](/active-directory/role-based-access-built-in-roles.md).</span></span>

<span data-ttu-id="d5b7e-143">hello 系統管理使用者就必須 hello 外部使用者 tooadd hello 電子郵件地址。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-143">hello admin user then needs tooadd hello email address of hello external user.</span></span> <span data-ttu-id="d5b7e-144">hello 預期行為是讓 hello 外部使用者 toonot 都會顯示在現有的租用戶的 hello。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-144">hello expected behavior is for hello external user toonot show up in hello existing tenant.</span></span> <span data-ttu-id="d5b7e-145">已邀請 hello 外部使用者之後，他會顯示在**訂用帳戶 > 存取控制 (IAM)**與 hello 目前所有的使用者目前指派的 RBAC 角色在 hello 訂用帳戶範圍。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-145">After hello external user has been invited, he will be visible under **Subscriptions > Access Control (IAM)** with all hello current users which are currently assigned an RBAC role at hello Subscription scope.</span></span>





![新增權限 toonew RBAC 角色](./media/role-based-access-control-create-custom-roles-for-internal-external-users/3.png)





![訂用帳戶等級的 RBAC 角色清單](./media/role-based-access-control-create-custom-roles-for-internal-external-users/4.png)

<span data-ttu-id="d5b7e-148">hello 使用者 」chessercarlton@gmail.com」 已受邀的 toobe**擁有者**hello 「 免費試用版 」 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-148">hello user "chessercarlton@gmail.com" has been invited toobe an **Owner** for hello “Free Trial” subscription.</span></span> <span data-ttu-id="d5b7e-149">在傳送嗨邀請之後, hello 外部使用者會收到電子郵件確認以啟用連結。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-149">After sending hello invitation, hello external user will receive an email confirmation with an activation link.</span></span>
<span data-ttu-id="d5b7e-150">![RBAC 角色的電子郵件邀請](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span><span class="sxs-lookup"><span data-stu-id="d5b7e-150">![email invitation for RBAC role](./media/role-based-access-control-create-custom-roles-for-internal-external-users/5.png)</span></span>

<span data-ttu-id="d5b7e-151">由於外部 toohello 組織，hello 新使用者並沒有任何現有的屬性 hello"預設租用戶 Azure 」 的目錄中。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-151">Being external toohello organization, hello new user does not have any existing attributes in hello "Default tenant Azure" directory.</span></span> <span data-ttu-id="d5b7e-152">它們將在建立之後 hello 外部使用者已授與同意 toobe 記錄與他已被指派至角色 hello 訂用帳戶相關聯的 hello 目錄中。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-152">They will be created after hello external user has given consent toobe recorded in hello directory which is associated with hello subscription which he has been assigned a role to.</span></span>





![RBAC 角色的電子郵件邀請訊息](./media/role-based-access-control-create-custom-roles-for-internal-external-users/6.png)

<span data-ttu-id="d5b7e-154">顯示 hello 中當做外部使用者從現在起的 Azure Active Directory 租用戶的 hello 外部使用者，這可以在 hello Azure 入口網站和 hello 傳統入口網站中檢視。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-154">hello external user shows in hello Azure Active Directory tenant from now on as external user and this can be viewed both in hello Azure portal and in hello classic portal.</span></span>





![使用者刀鋒視窗 Azure Active Directory Azure 入口網站](./media/role-based-access-control-create-custom-roles-for-internal-external-users/7.png)





![使用者刀鋒視窗 Azure Active Directory Azure 傳統入口網站](./media/role-based-access-control-create-custom-roles-for-internal-external-users/8.png)

<span data-ttu-id="d5b7e-157">在 hello**使用者**可以辨識這兩個入口網站的 hello 外部使用者的檢視：</span><span class="sxs-lookup"><span data-stu-id="d5b7e-157">In hello **Users** view in both portals hello external users can be recognized by:</span></span>

* <span data-ttu-id="d5b7e-158">hello Azure 入口網站中的 hello 不同的圖示類型</span><span class="sxs-lookup"><span data-stu-id="d5b7e-158">hello different icon type in hello Azure portal</span></span>
* <span data-ttu-id="d5b7e-159">hello 不同來源 hello 傳統入口網站中的點</span><span class="sxs-lookup"><span data-stu-id="d5b7e-159">hello different sourcing point in hello classic portal</span></span>

<span data-ttu-id="d5b7e-160">不過，授與**擁有者**或**參與者**存取 tooan 外部使用者在 hello**訂用帳戶**範圍，不允許 hello 存取 toohello 系統管理使用者的目錄除非 hello**全域管理員**允許它。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-160">However, granting **Owner** or **Contributor** access tooan external user at hello **Subscription** scope, does not allow hello access toohello admin user's directory, unless hello **Global Admin** allows it.</span></span> <span data-ttu-id="d5b7e-161">Hello 使用者內容，在 hello**使用者類型**具有兩個一般參數，**成員**和**客體**可以識別。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-161">In hello user proprieties,  hello **User Type** which has two common parameters, **Member** and **Guest** can be identified.</span></span> <span data-ttu-id="d5b7e-162">成員是來賓時從外部來源的受邀使用者 toohello 目錄 hello 目錄中註冊的使用者。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-162">A member is a user which is registered in hello directory while a guest is a user invited toohello directory from an external source.</span></span> <span data-ttu-id="d5b7e-163">如需詳細資訊，請參閱 [Azure Active Directory 系統管理員如何新增 B2B 共同作業使用者](/active-directory/active-directory-b2b-admin-add-users)。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-163">For more information, see [How do Azure Active Directory admins add B2B collaboration users](/active-directory/active-directory-b2b-admin-add-users).</span></span>

> [!NOTE]
> <span data-ttu-id="d5b7e-164">請確定輸入 hello 入口網站中的 hello 認證之後, hello 外部使用者選取 hello toosign 入正確的目錄。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-164">Make sure that after entering hello credentials in hello portal, hello external user selects hello correct directory toosign-in to.</span></span> <span data-ttu-id="d5b7e-165">hello 相同的使用者可以有存取 toomultiple 目錄和可以選取其中任一種按一下 hello 右上角中 hello Azure 入口網站中的 hello 使用者名稱，然後選擇 hello 適當目錄 hello 下拉式清單中。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-165">hello same user can have access toomultiple directories and can select either one of  them by clicking hello username in hello top right-hand side in hello Azure portal and then choose hello appropriate directory from hello dropdown list.</span></span>

<span data-ttu-id="d5b7e-166">同時會 hello 目錄中的客體，hello 外部使用者可以管理 hello Azure 的訂用帳戶的所有資源，但無法存取 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-166">While being a guest in hello directory, hello external user can manage all resources for hello Azure subscription, but can't access hello directory.</span></span>





![存取限制的 tooazure active directory 的 Azure 入口網站](./media/role-based-access-control-create-custom-roles-for-internal-external-users/9.png)

<span data-ttu-id="d5b7e-168">Azure Active Directory 和 Azure 訂用帳戶沒有父子式關聯性，如同其他 Azure 資源 (例如︰虛擬機器、虛擬網路、Web Apps、儲存體等) 與 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-168">Azure Active Directory and an Azure subscription don't have a child-parent relation like other Azure resources (for example: virtual machines, virtual networks, web apps, storage etc.) have with an Azure subscription.</span></span> <span data-ttu-id="d5b7e-169">所有 hello 後者是建立、 管理和 Azure 訂用帳戶時使用的 toomanage hello 存取 tooan Azure 目錄，在 Azure 訂用帳戶計費。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-169">All hello latter is created, managed and billed under an Azure subscription while an Azure subscription is used toomanage hello access tooan Azure directory.</span></span> <span data-ttu-id="d5b7e-170">如需詳細資訊，請參閱[如何為 Azure 訂用帳戶已相關的 tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory)。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-170">For more details, see [How an Azure subscription is related tooAzure AD](/active-directory/active-directory-how-subscriptions-associated-directory).</span></span>

<span data-ttu-id="d5b7e-171">從所有的 hello 內建 RBAC 角色，**擁有者**和**參與者**tooall hello 環境、 差異為，參與者無法建立 hello 及 delete 中新的資源提供完整的管理存取RBAC 角色。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-171">From all hello built-in RBAC roles, **Owner** and **Contributor** offer full management access tooall resources in hello environment, hello difference being that a Contributor can't create and delete new RBAC roles.</span></span> <span data-ttu-id="d5b7e-172">hello 其他內建角色，例如**虛擬機器參與者**提供完整的管理存取僅由 hello 名稱，不論 hello toohello 資源**資源群組**正在建立到。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-172">hello other built-in roles like **Virtual Machine Contributor** offer full management access only toohello resources indicated by hello name, regardless of hello **Resource Group** they are being created into.</span></span>

<span data-ttu-id="d5b7e-173">指派 hello 內建 RBAC 的角色**虛擬機器參與者**在訂用帳戶層級中，表示該 hello 指派的使用者 hello 角色：</span><span class="sxs-lookup"><span data-stu-id="d5b7e-173">Assigning hello built-in RBAC role of **Virtual Machine Contributor** at a subscription level, means that hello user assigned hello role:</span></span>

* <span data-ttu-id="d5b7e-174">可以檢視所有虛擬機器不論其部署日期和 hello 資源群組的一部分</span><span class="sxs-lookup"><span data-stu-id="d5b7e-174">Can view all virtual machines regardless their deployment date and hello resource groups they are part of</span></span>
* <span data-ttu-id="d5b7e-175">Hello 訂用帳戶中有完整的管理存取 toohello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d5b7e-175">Has full management access toohello virtual machines in hello subscription</span></span>
* <span data-ttu-id="d5b7e-176">無法檢視 hello 訂用帳戶中的任何其他資源類型</span><span class="sxs-lookup"><span data-stu-id="d5b7e-176">Can't view any other resource types in hello subscription</span></span>
* <span data-ttu-id="d5b7e-177">無法從計費觀點來操作任何變更</span><span class="sxs-lookup"><span data-stu-id="d5b7e-177">Can't operate any changes from a billing perspective</span></span>

> [!NOTE]
> <span data-ttu-id="d5b7e-178">RBAC 正在 Azure 入口網站的唯一功能，它不會授與存取 toohello 傳統入口網站。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-178">RBAC being an Azure portal only feature, it doesn't grant access toohello classic portal.</span></span>

## <a name="assign-a-built-in-rbac-role-tooan-external-user"></a><span data-ttu-id="d5b7e-179">指派給內建 RBAC 角色 tooan 外部使用者</span><span class="sxs-lookup"><span data-stu-id="d5b7e-179">Assign a built-in RBAC role tooan external user</span></span>
<span data-ttu-id="d5b7e-180">在這項測試不同的狀況，如 hello 外部使用者 」alflanigan@gmail.com"會成為**虛擬機器參與者**。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-180">For a different scenario in this test, hello external user "alflanigan@gmail.com" is added as a **Virtual Machine Contributor**.</span></span>




![虛擬機器參與者內建角色](./media/role-based-access-control-create-custom-roles-for-internal-external-users/11.png)

<span data-ttu-id="d5b7e-182">hello 正常的行為，這個外部的使用者與此內建的角色是 toosee，以及管理只有虛擬機器和其相鄰資源管理員唯一所需資源部署時。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-182">hello normal behavior for this external user with this built-in role is toosee and manage only virtual machines and their adjacent Resource Manager only resources necessary while deploying.</span></span> <span data-ttu-id="d5b7e-183">根據設計，這些限制的角色提供存取 hello Azure 入口網站中建立的唯一 tootheir 對應資源，無論某些仍然可以部署以及 hello 傳統的入口網站中 (例如： 虛擬機器)。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-183">By design, these limited roles offer access only tootheir correspondent resources created in hello Azure portal, regardless some can still be deployed in hello classic portal as well (for example: virtual machines).</span></span>





![Azure 入口網站中的虛擬機器參與者角色概觀](./media/role-based-access-control-create-custom-roles-for-internal-external-users/12.png)

## <a name="grant-access-at-a-subscription-level-for-a-user-in-hello-same-directory"></a><span data-ttu-id="d5b7e-185">授與存取訂用帳戶層級中 hello 使用者相同的目錄</span><span class="sxs-lookup"><span data-stu-id="d5b7e-185">Grant access at a subscription level for a user in hello same directory</span></span>
<span data-ttu-id="d5b7e-186">hello 程序並不相同 tooadding 外部使用者，同時從 hello 系統管理員觀點來看，授與 hello RBAC 角色，以及被授與存取 toohello 角色 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-186">hello process flow is identical tooadding an external user, both from hello admin perspective granting hello RBAC role as well as hello user being granted access toohello role.</span></span> <span data-ttu-id="d5b7e-187">此處 hello 差異是因為 hello 訂用帳戶內的所有 hello 資源範圍後，都即可使用 hello 儀表板中登入，該 hello 受邀使用者不會收到任何電子郵件邀請。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-187">hello difference here is that hello invited user will not receive any email invitations as all hello resource scopes within hello subscription will be available in hello dashboard after signing in.</span></span>

## <a name="assign-rbac-roles-at-hello-resource-group-scope"></a><span data-ttu-id="d5b7e-188">將在 hello 資源群組範圍的 RBAC 角色指派</span><span class="sxs-lookup"><span data-stu-id="d5b7e-188">Assign RBAC roles at hello resource group scope</span></span>
<span data-ttu-id="d5b7e-189">指派在 RBAC 角色**資源群組**範圍已指派 hello 角色在 hello 訂用帳戶層級，這兩種類型的使用者-外部或內部的相同程序 (hello 屬於相同的目錄)。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-189">Assigning an RBAC role at a **Resource Group** scope has an identical process for assigning hello role at hello subscription level, for both types of users - either external or internal (part of hello same directory).</span></span> <span data-ttu-id="d5b7e-190">hello hello RBAC 角色所指派的使用者僅在其環境中的 toosee hello 資源群組已指派給這些存取從 hello**資源群組**hello Azure 入口網站中的圖示。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-190">hello users which are assigned hello RBAC role is toosee in their environment only hello resource group they have been assigned access from hello **Resource Groups** icon in hello Azure portal.</span></span>

## <a name="assign-rbac-roles-at-hello-resource-scope"></a><span data-ttu-id="d5b7e-191">將在 hello 資源範圍 RBAC 角色指派</span><span class="sxs-lookup"><span data-stu-id="d5b7e-191">Assign RBAC roles at hello resource scope</span></span>
<span data-ttu-id="d5b7e-192">指定於 Azure 中的資源範圍 RBAC 角色指派 hello 角色在 hello 訂用帳戶層級或 hello 資源群組層級的相同程序，下列 hello 相同這兩種案例的工作流程。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-192">Assigning an RBAC role at a resource scope in Azure has an identical process for assigning hello role at hello subscription level or at hello resource group level, following hello same workflow for both scenarios.</span></span> <span data-ttu-id="d5b7e-193">同樣地，hello hello RBAC 角色所指派之使用者可以看到只有 hello，它們有已指派給項目存取，可能是在 hello**所有資源** 索引標籤或直接在儀表板中。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-193">Again, hello users which are assigned hello RBAC role can see only hello items that they have been assigned access to, either in hello **All Resources** tab or directly in their dashboard.</span></span>

<span data-ttu-id="d5b7e-194">RBAC 同時在資源群組範圍或資源範圍的一個重要環節是 hello 使用者 toomake 確定 toosign 單元 toohello 正確目錄。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-194">An important aspect for RBAC both at resource group scope or resource scope is for hello users toomake sure toosign-in toohello correct directory.</span></span>





![Azure 入口網站中的目錄登入](./media/role-based-access-control-create-custom-roles-for-internal-external-users/13.png)

## <a name="assign-rbac-roles-for-an-azure-active-directory-group"></a><span data-ttu-id="d5b7e-196">為 Azure Active Directory 群組指派 RBAC 角色</span><span class="sxs-lookup"><span data-stu-id="d5b7e-196">Assign RBAC roles for an Azure Active Directory group</span></span>
<span data-ttu-id="d5b7e-197">所有在 hello 三個不同的範圍中的管理、 部署和管理各種資源與指派的使用者沒有 hello Azure 優惠 hello 權限使用 RBAC 的 hello 案例需要的管理個人的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-197">All hello scenarios using RBAC at hello three different scopes in Azure offer hello privilege of managing, deploying and administering various resources as an assigned user without hello need of managing a personal subscription.</span></span> <span data-ttu-id="d5b7e-198">不論 hello RBAC 角色指派給訂用帳戶、 資源群組或資源範圍，所有的 hello 資源上的其他使用者所建立的 hello 分派計費 hello 一個 Azure 訂用帳戶 hello 使用者有權存取的位置。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-198">Regardless hello RBAC role is assigned for a subscription, resource group or resource scope, all hello resources created further on by hello assigned users are billed under hello one Azure subscription where hello users have access to.</span></span> <span data-ttu-id="d5b7e-199">如此一來，hello 擁有計費的整個 Azure 訂用帳戶的系統管理員權限的使用者具有完整 hello 耗用量，不論概觀 hello 資源管理者。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-199">This way, hello users who have billing administrator permissions for that entire Azure subscription has a complete overview on hello consumption, regardless who is managing hello resources.</span></span>

<span data-ttu-id="d5b7e-200">對於較大的組織而言，您可以套用 RBAC 角色在 hello 考慮 hello 觀點來看該 hello 系統管理使用者的 Azure Active Directory 群組相同的方式想 toogrant hello 細微的存取權的小組或整個部門，不會個別針對每個使用者，因此考慮為極階段和管理有效選項。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-200">For larger organizations, RBAC roles can be applied in hello same way for Azure Active Directory groups considering hello perspective that hello admin user wants toogrant hello granular access for teams or entire departments, not individually for each user, thus considering it as an extremely time and management efficient option.</span></span> <span data-ttu-id="d5b7e-201">tooillustrate 此範例中，hello**參與者**角色已加入 tooone 的 hello 群組中的 hello hello 訂用帳戶層級的租用戶。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-201">tooillustrate this example, hello **Contributor** role has been added tooone of hello groups in hello tenant at hello subscription level.</span></span>





![新增 AAD 群組的 RBAC 角色](./media/role-based-access-control-create-custom-roles-for-internal-external-users/14.png)

<span data-ttu-id="d5b7e-203">這些群組都是安全性群組，只在 Azure Active Directory 內進行佈建和管理。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-203">These groups are security groups which are provisioned and managed only within Azure Active Directory.</span></span>

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-powershell"></a><span data-ttu-id="d5b7e-204">建立自訂的 RBAC 角色 tooopen 支援要求使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5b7e-204">Create a custom RBAC role tooopen support requests using PowerShell</span></span>
<span data-ttu-id="d5b7e-205">hello 內建 RBAC 角色在 Azure 中可確保特定根據 hello hello 環境中的可用資源的權限層級。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-205">hello built-in RBAC roles which are available in Azure ensure certain permission levels based on hello available resources in hello environment.</span></span> <span data-ttu-id="d5b7e-206">不過，如果這些角色都不符合 hello 系統管理使用者的需求，是藉由建立自訂的 RBAC 角色更多的 hello 選項 toolimit 存取。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-206">However, if none of these roles suit hello admin user's needs, there is hello option toolimit access even more by creating custom RBAC roles.</span></span>

<span data-ttu-id="d5b7e-207">建立自訂的 RBAC 角色需要 tootake 一個內建角色並加以編輯，然後再將其匯回 hello 環境中。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-207">Creating custom RBAC roles requires tootake one built-in role, edit it and then import it back in hello environment.</span></span> <span data-ttu-id="d5b7e-208">使用 PowerShell 或 CLI 為管理 hello 下載和上傳的 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-208">hello download and upload of hello role are managed using either PowerShell or CLI.</span></span>

<span data-ttu-id="d5b7e-209">重要 toounderstand hello 必要條件建立自訂安全性角色可授與 hello 訂用帳戶層級更細微的存取並開啟支援要求的 hello 受邀使用者 hello 彈性也可讓它。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-209">It is important toounderstand hello prerequisites of creating a custom role which can grant granular access at hello subscription level and also allow hello invited user hello flexibility of opening support requests.</span></span>

<span data-ttu-id="d5b7e-210">此範例中的 hello 內建角色**讀取器**可讓使用者存取 tooview 所有 hello 資源範圍但不是 tooedit 它們，或建立新的已自訂開啟支援要求的 tooallow hello 使用者 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-210">For this example hello built-in role **Reader** which allows users access tooview all hello resource scopes but not tooedit them or create new ones has been customized tooallow hello user hello option of opening support requests.</span></span>

<span data-ttu-id="d5b7e-211">hello 匯出 hello 的第一個動作**讀取器**角色需求 toobe 在 PowerShell 中完成系統管理員身分執行提高權限。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-211">hello first action of exporting hello **Reader** role needs toobe completed in PowerShell ran with elevated permissions as administrator.</span></span>

```
Login-AzureRMAccount

Get-AzureRMRoleDefinition -Name "Reader"

Get-AzureRMRoleDefinition -Name "Reader" | ConvertTo-Json | Out-File C:\rbacrole2.json

```





![讀取器 RBAC 角色的 PowerShell 螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/15.png)

<span data-ttu-id="d5b7e-213">然後，您需要 hello 角色 tooextract hello JSON 的範本。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-213">Then you need tooextract hello JSON template of hello role.</span></span>





![自訂讀取器 RBAC 角色的 JSON 範本](./media/role-based-access-control-create-custom-roles-for-internal-external-users/16.png)

<span data-ttu-id="d5b7e-215">典型的 RBAC 角色是由三個主要區段所組成︰**Actions**、**NotActions** 和 **AssignableScopes**。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-215">A typical RBAC role is composed out of three main sections, **Actions**, **NotActions** and **AssignableScopes**.</span></span>

<span data-ttu-id="d5b7e-216">在 hello**動作**區段會列出所有 hello 此角色允許的操作。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-216">In hello **Action** section are listed all hello permitted operations for this role.</span></span> <span data-ttu-id="d5b7e-217">從資源提供者指派給每個動作的重要 toounderstand 它。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-217">It's important toounderstand that each action is assigned from a resource provider.</span></span> <span data-ttu-id="d5b7e-218">在此情況下，用於建立支援票證 hello **Microsoft.Support**必須列出資源提供者。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-218">In this case, for creating support tickets hello **Microsoft.Support** resource provider must be listed.</span></span>

<span data-ttu-id="d5b7e-219">toobe 無法 toosee 所有 hello 可用和已註冊您的訂用帳戶中的資源提供者，您可以使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-219">toobe able toosee all hello resource providers available and registered in your subscription, you can use PowerShell.</span></span>
```
Get-AzureRMResourceProvider

```
<span data-ttu-id="d5b7e-220">此外，您可以檢查 hello 所有 hello 使用 PowerShell cmdlet toomanage hello 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-220">Additionally, you can check for hello all hello available PowerShell cmdlets toomanage hello resource providers.</span></span>
    <span data-ttu-id="d5b7e-221">![資源提供者管理的 PowerShell 螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span><span class="sxs-lookup"><span data-stu-id="d5b7e-221">![PowerShell screenshot for resource provider management](./media/role-based-access-control-create-custom-roles-for-internal-external-users/17.png)</span></span>

<span data-ttu-id="d5b7e-222">所有 hello 特定 RBAC 角色，資源提供者會 hello 區段底下所列的動作 toorestrict **NotActions**。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-222">toorestrict all hello actions for a particular RBAC role, resource providers are listed under hello section **NotActions**.</span></span>
<span data-ttu-id="d5b7e-223">最後，是強制性該 hello RBAC 角色包含 hello 明確訂用帳戶 Id 使用的位置。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-223">Last, it's mandatory that hello RBAC role contains hello explicit subscription IDs where it is used.</span></span> <span data-ttu-id="d5b7e-224">hello 訂用帳戶 Id 列在 hello **AssignableScopes**，否則您不能 tooimport hello 角色在您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-224">hello subscription IDs are listed under hello **AssignableScopes**, otherwise you will not be allowed tooimport hello role in your subscription.</span></span>

<span data-ttu-id="d5b7e-225">之後建立和自訂 hello RBAC 角色時，它需要 toobe 匯入後的 hello 環境。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-225">After creating and customizing hello RBAC role, it needs toobe imported back hello environment.</span></span>

```
New-AzureRMRoleDefinition -InputFile "C:\rbacrole2.json"

```

<span data-ttu-id="d5b7e-226">在此範例中，hello 自訂此 RBAC 角色名稱會是 「 讀取器支援票證的存取層級 」 hello 訂用帳戶以及 tooopen 支援要求中的所有項目允許 hello 使用者 tooview。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-226">In this example, hello custom name for this RBAC role is "Reader support tickets access level" allowing hello user tooview everything in hello subscription and also tooopen support requests.</span></span>

> [!NOTE]
> <span data-ttu-id="d5b7e-227">hello 只有兩個內建 RBAC 角色允許的開啟支援要求的 hello 動作是**擁有者**和**參與者**。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-227">hello only two built-in RBAC roles allowing hello action of opening of support requests are **Owner** and **Contributor**.</span></span> <span data-ttu-id="d5b7e-228">對於使用者 toobe tooopen 無法支援要求，他必須為指派 RBAC 角色只在 hello 訂用帳戶範圍，因為根據 Azure 訂用帳戶建立支援的所有要求。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-228">For a user toobe able tooopen support requests, he must be assigned an RBAC role only at hello subscription scope, because all support requests are created based on an Azure subscription.</span></span>

<span data-ttu-id="d5b7e-229">這個新的自訂角色指派給 hello tooan 使用者相同的目錄。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-229">This new custom role has been assigned tooan user from hello same directory.</span></span>





![匯入 hello Azure 入口網站中的自訂 RBAC 角色的螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/18.png)





![螢幕擷取畫面的指派中 hello 自訂匯入的 RBAC 角色 toouser 相同的目錄](./media/role-based-access-control-create-custom-roles-for-internal-external-users/19.png)





![自訂匯入的 RBAC 角色之權限的螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/20.png)

<span data-ttu-id="d5b7e-233">hello 範例已進一步詳細的 tooemphasize hello 限制這個自訂的 RBAC 角色，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d5b7e-233">hello example has been further detailed tooemphasize hello limits of this custom RBAC role as follows:</span></span>
* <span data-ttu-id="d5b7e-234">可以建立新的支援要求</span><span class="sxs-lookup"><span data-stu-id="d5b7e-234">Can create new support requests</span></span>
* <span data-ttu-id="d5b7e-235">無法建立新的資源範圍 (例如︰虛擬機器)</span><span class="sxs-lookup"><span data-stu-id="d5b7e-235">Can't create new resource scopes (for example: virtual machine)</span></span>
* <span data-ttu-id="d5b7e-236">無法建立新的資源群組</span><span class="sxs-lookup"><span data-stu-id="d5b7e-236">Can't create new resource groups</span></span>





![建立支援要求之自訂 RBAC 角色的螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/21.png)





![螢幕擷取畫面的自訂 RBAC 角色無法 toocreate Vm](./media/role-based-access-control-create-custom-roles-for-internal-external-users/22.png)





![螢幕擷取畫面的自訂 RBAC 角色無法 toocreate 新 RGs](./media/role-based-access-control-create-custom-roles-for-internal-external-users/23.png)

## <a name="create-a-custom-rbac-role-tooopen-support-requests-using-azure-cli"></a><span data-ttu-id="d5b7e-240">建立自訂的 RBAC 角色 tooopen 支援使用 Azure CLI 要求</span><span class="sxs-lookup"><span data-stu-id="d5b7e-240">Create a custom RBAC role tooopen support requests using Azure CLI</span></span>
<span data-ttu-id="d5b7e-241">執行在 Mac 上，而不需要存取 tooPowerShell，Azure CLI 是 hello 方式 toogo。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-241">Running on a Mac and without having access tooPowerShell, Azure CLI is hello way toogo.</span></span>

<span data-ttu-id="d5b7e-242">hello 步驟 toocreate 自訂安全性角色都是相同的與 hello 唯一例外狀況，使用 CLI hello 角色無法在下載 JSON 範本，但它可以在檢視 hello CLI hello。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-242">hello steps toocreate a custom role are hello same, with hello sole exception that using CLI hello role can't be downloaded in a JSON template, but it can be viewed in hello CLI.</span></span>

<span data-ttu-id="d5b7e-243">此範例中，我已選擇 hello 的內建角色**備份讀取器**。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-243">For this example I have chosen hello built-in role of **Backup Reader**.</span></span>

```

azure role show "backup reader" --json

```





![備份讀取器角色顯示的 CLI 螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/24.png)

<span data-ttu-id="d5b7e-245">編輯 Visual Studio 中的 hello 角色 JSON 範本中複製 hello 內容之後，hello **Microsoft.Support**資源提供者已新增在 hello**動作**區段，讓這位使用者可以開啟但仍繼續 toobe hello 備份保存庫的讀取器的支援要求。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-245">Editing hello role in Visual Studio after copying hello proprieties in a JSON template, hello **Microsoft.Support** resource provider has been added in hello **Actions** sections so that this user can open support requests while continuing toobe a reader for hello backup vaults.</span></span> <span data-ttu-id="d5b7e-246">一次是必要 tooadd hello 訂用帳戶 ID，此角色將會使用 hello **AssignableScopes** > 一節。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-246">Again it is necessary tooadd hello subscription ID where this role will be used in hello **AssignableScopes** section.</span></span>

```

azure role create --inputfile <path>

```





![匯入自訂 RBAC 角色的 CLI 螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/25.png)

<span data-ttu-id="d5b7e-248">hello 新角色現已推出 hello Azure 入口網站和 hello assignation 程序是 hello 相同如 hello 先前範例所示。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-248">hello new role is now available in hello Azure portal and hello assignation process is hello same as in hello previous examples.</span></span>





![使用 CLI 1.0 所建立之自訂 RBAC 角色的 Azure 入口網站螢幕擷取畫面](./media/role-based-access-control-create-custom-roles-for-internal-external-users/26.png)

<span data-ttu-id="d5b7e-250">最新組建 2017，hello Azure 雲端殼層 hello 為上市。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-250">As of hello latest Build 2017, hello Azure Cloud Shell is generally available.</span></span> <span data-ttu-id="d5b7e-251">Azure 雲端殼層是補數 tooIDE 和 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-251">Azure Cloud Shell is a complement tooIDE and hello Azure Portal.</span></span> <span data-ttu-id="d5b7e-252">您可以利用此服務，取得經過驗證且裝載於 Azure 內以瀏覽器為基礎的殼層，您可以使用它而不使用安裝在您電腦上的 CLI。</span><span class="sxs-lookup"><span data-stu-id="d5b7e-252">With this service, you get a browser-based shell that is authenticated and hosted within Azure and you can use it instead of CLI installed on your machine.</span></span>





![Azure Cloud Shell](./media/role-based-access-control-create-custom-roles-for-internal-external-users/27.png)
