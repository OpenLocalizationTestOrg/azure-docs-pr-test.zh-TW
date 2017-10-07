---
title: "aaaHow tooactivate 或停用角色 |Microsoft 文件"
description: "了解如何 tooactivate 角色的特殊權限身分識別與 hello Azure Privileged Identity Management 的應用程式。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 1ce9e2e7-452b-4f66-9588-0d9cd2539e45
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/14/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 8c68ad69e4b006263bbb8a1cfc7ed3dba974e1db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooactivate-or-deactivate-roles-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="61525-103">如何 tooactivate 或停用 Azure AD Privileged Identity Management 中的角色</span><span class="sxs-lookup"><span data-stu-id="61525-103">How tooactivate or deactivate roles in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="61525-104">Azure Active Directory (AD) 的權限身分管理可簡化企業如何管理 Azure AD 中的特殊權限的存取 tooresources 和 Office 365 或 Microsoft Intune 等其他 Microsoft online services。</span><span class="sxs-lookup"><span data-stu-id="61525-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access tooresources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="61525-105">如果您已經進行了適合管理的角色，這表示當您需要特殊權限的 tooperform 動作時，您可以啟用該角色。</span><span class="sxs-lookup"><span data-stu-id="61525-105">If you have been made eligible for an administrative role, that means you can activate that role when you need tooperform privileged actions.</span></span> <span data-ttu-id="61525-106">例如，如果您偶爾會管理 Office 365 功能，則貴組織的特殊權限角色管理員可能不會讓您成為永久全域管理員，因為該角色也會影響其他服務。</span><span class="sxs-lookup"><span data-stu-id="61525-106">For example, if you occasionally manage Office 365 features, your organization's privileged role administrators may not make you a permanent Global Administrator, since that role impacts other services, too.</span></span> <span data-ttu-id="61525-107">他們反而會讓您符合 Azure AD 角色 (例如「Exchange Online 管理員」) 的資格。</span><span class="sxs-lookup"><span data-stu-id="61525-107">Instead, they make you eligible for Azure AD roles such as Exchange Online Administrator.</span></span> <span data-ttu-id="61525-108">您可以 tooactivate 該角色而且時，要求您需要其權限，然後您就有預定的時間期間的系統管理控制權。</span><span class="sxs-lookup"><span data-stu-id="61525-108">You can request tooactivate that role when you need its privileges, and then you'll have admin control for a predetermined time period.</span></span>

<span data-ttu-id="61525-109">本文適用於需要 tooactivate 系統管理員在 Azure AD Privileged Identity Management (PIM) 中的角色。</span><span class="sxs-lookup"><span data-stu-id="61525-109">This article is for admins who need tooactivate their role in Azure AD Privileged Identity Management (PIM).</span></span> <span data-ttu-id="61525-110">它會引導您透過 hello 步驟 tooactivate 角色當您需要 hello 權限，而且當您完成時，停用 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="61525-110">It walks you through hello steps tooactivate a role when you need hello permissions, and deactivate hello role when you're done.</span></span> <span data-ttu-id="61525-111">此外，特殊權限的角色系統管理員可以要求核准 tooactivate （預覽） 的角色。</span><span class="sxs-lookup"><span data-stu-id="61525-111">In addition, privileged role administrators can require approval tooactivate a role (Preview).</span></span> <span data-ttu-id="61525-112">在這裡深入了解 [PIM 核准工作流程](./privileged-identity-management/azure-ad-pim-approval-workflow.md)。</span><span class="sxs-lookup"><span data-stu-id="61525-112">Learn more about [PIM Approval Workflows](./privileged-identity-management/azure-ad-pim-approval-workflow.md) here.</span></span>

## <a name="add-hello-privileged-identity-management-application"></a><span data-ttu-id="61525-113">新增 hello Privileged Identity Management 的應用程式</span><span class="sxs-lookup"><span data-stu-id="61525-113">Add hello Privileged Identity Management application</span></span>
<span data-ttu-id="61525-114">Hello Azure AD Privileged Identity Management 的應用程式用於 hello [Azure 入口網站](https://portal.azure.com/)toorequest 啟用角色，即使您將 toooperate 中另一個入口網站或 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="61525-114">Use hello Azure AD Privileged Identity Management application in hello [Azure portal](https://portal.azure.com/) toorequest a role activation, even if you're going toooperate in another portal or PowerShell.</span></span> <span data-ttu-id="61525-115">如果您的 Azure 入口網站上沒有 hello Azure AD Privileged Identity Management 的應用程式，請遵循啟動這些步驟 tooget。</span><span class="sxs-lookup"><span data-stu-id="61525-115">If you don't have hello Azure AD Privileged Identity Management application on your Azure portal, follow these steps tooget started.</span></span>

1. <span data-ttu-id="61525-116">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="61525-116">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="61525-117">選取您在 hello 右上角的 hello Azure 入口網站，與您將您的選取 hello 目錄中的使用者名稱進行操作。</span><span class="sxs-lookup"><span data-stu-id="61525-117">Select your username in hello upper right-hand corner of hello Azure portal, and select hello directory where you will you be operating.</span></span>
3. <span data-ttu-id="61525-118">選取**更多服務**並用的 hello 篩選文字方塊中 toosearch **Azure AD Privileged Identity Management**。</span><span class="sxs-lookup"><span data-stu-id="61525-118">Select **More services** and use hello Filter textbox toosearch for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="61525-119">請檢查**Pin toodashboard** ，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="61525-119">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="61525-120">hello Privileged Identity Management 的應用程式會開啟。</span><span class="sxs-lookup"><span data-stu-id="61525-120">hello Privileged Identity Management application opens.</span></span>

## <a name="activate-a-role"></a><span data-ttu-id="61525-121">啟用角色</span><span class="sxs-lookup"><span data-stu-id="61525-121">Activate a role</span></span>
<span data-ttu-id="61525-122">當您需要 tootake 角色上的時，您可以藉由選取 hello 要求啟用**我角色**hello Azure AD Privileged Identity Management 的應用程式中的導覽選項的左瀏覽資料行。</span><span class="sxs-lookup"><span data-stu-id="61525-122">When you need tootake on a role, you can request activation by selecting hello **My Roles** navigation option in hello Azure AD Privileged Identity Management application's left navigation column.</span></span>

1. <span data-ttu-id="61525-123">登入 toohello [Azure 入口網站](https://portal.azure.com/)和選取 hello Azure AD Privileged Identity Management 磚。</span><span class="sxs-lookup"><span data-stu-id="61525-123">Sign in toohello [Azure portal](https://portal.azure.com/) and select hello Azure AD Privileged Identity Management tile.</span></span>
2. <span data-ttu-id="61525-124">選取 [我的角色]。</span><span class="sxs-lookup"><span data-stu-id="61525-124">Select **My Roles**.</span></span> <span data-ttu-id="61525-125">指派的合格角色的清單會出現在 hello hello 頁面頂端的 hello 分組。</span><span class="sxs-lookup"><span data-stu-id="61525-125">A list of your assigned eligible roles appear in hello grouping at hello top of hello page.</span></span>
3. <span data-ttu-id="61525-126">選取角色 tooactivate。</span><span class="sxs-lookup"><span data-stu-id="61525-126">Select a role tooactivate.</span></span>
4. <span data-ttu-id="61525-127">選取 [ **啟用**]。</span><span class="sxs-lookup"><span data-stu-id="61525-127">Select **Activate**.</span></span> <span data-ttu-id="61525-128">hello**要求角色啟用**刀鋒視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="61525-128">hello **Request role activation** blade appears.</span></span>
5. <span data-ttu-id="61525-129">某些角色需要多重要素驗證 (MFA)，才能啟動 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="61525-129">Some roles require Multi-Factor Authentication (MFA) before you can activate hello role.</span></span> <span data-ttu-id="61525-130">您只需要 tooauthenticate 一次每個工作階段。</span><span class="sxs-lookup"><span data-stu-id="61525-130">You only have tooauthenticate once per session.</span></span>
   
    ![在啟用角色之前先以 MFA 驗證 - 螢幕擷取畫面][2]
6. <span data-ttu-id="61525-132">Hello 文字欄位中輸入 hello hello 啟用要求的原因。</span><span class="sxs-lookup"><span data-stu-id="61525-132">Enter hello reason for hello activation request in hello text field.</span></span>  <span data-ttu-id="61525-133">某些角色需要 toosupply 疑難票證號碼。</span><span class="sxs-lookup"><span data-stu-id="61525-133">Some roles require you toosupply a trouble ticket number.</span></span>
7. <span data-ttu-id="61525-134">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="61525-134">Select **OK**.</span></span>  <span data-ttu-id="61525-135">如果 hello 角色不需要核准，它現在已啟用，而且 hello 角色出現在 hello （正下方 hello 符合資格的角色指派清單） 的使用中角色清單。</span><span class="sxs-lookup"><span data-stu-id="61525-135">If hello role does not require approval, it is now activated, and hello role appears in hello list of active roles (directly below hello list of eligible role assignments).</span></span> <span data-ttu-id="61525-136">如果 hello[角色需要核准](./privileged-identity-management/azure-ad-pim-approval-workflow.md)tooactivate，快顯通知會短暫出現 hello 右上角的瀏覽器 hello 要求正在等待核准的通知。</span><span class="sxs-lookup"><span data-stu-id="61525-136">If hello [role requires approval](./privileged-identity-management/azure-ad-pim-approval-workflow.md) tooactivate, a toast notification will briefly appear in hello upper right-hand corner of your browser informing you hello request is pending approval.</span></span>

    ![要求擱置通知 - 螢幕擷取畫面][3]

## <a name="deactivate-a-role"></a><span data-ttu-id="61525-138">停用角色</span><span class="sxs-lookup"><span data-stu-id="61525-138">Deactivate a role</span></span>
<span data-ttu-id="61525-139">角色一經啟用，就會在達到時間限制 (合格的持續時間) 時自動停用。</span><span class="sxs-lookup"><span data-stu-id="61525-139">Once a role has been activated, it automatically deactivates when its time limit (eligible duration) is reached.</span></span>

<span data-ttu-id="61525-140">如果您提早完成管理工作，您也可以停用手動中 hello Azure AD Privileged Identity Management 的應用程式的角色。</span><span class="sxs-lookup"><span data-stu-id="61525-140">If you complete your admin tasks early, you can also deactivate a role manually in hello Azure AD Privileged Identity Management application.</span></span>  <span data-ttu-id="61525-141">選取**我角色**，選擇您完成時的 hello 角色使用從 hello**作用中的角色指派**群組，然後選取**停用**。</span><span class="sxs-lookup"><span data-stu-id="61525-141">Select **My Roles**, choose hello role you're done using from hello **Active role assignments** grouping, and select **Deactivate**.</span></span>  

## <a name="cancel-a-pending-request"></a><span data-ttu-id="61525-142">取消擱置要求</span><span class="sxs-lookup"><span data-stu-id="61525-142">Cancel a pending request</span></span>
<span data-ttu-id="61525-143">不需要啟用需要核准之角色的 hello 事件中，您可以隨時取消暫止要求。</span><span class="sxs-lookup"><span data-stu-id="61525-143">In hello event you do not require activation of a role that requires approval, you may cancel a pending request at any time.</span></span> <span data-ttu-id="61525-144">只需選取 hello**我角色**hello Azure AD Privileged Identity Management 的應用程式中的導覽選項的左瀏覽資料行。</span><span class="sxs-lookup"><span data-stu-id="61525-144">Simply select hello **My Roles** navigation option in hello Azure AD Privileged Identity Management application's left navigation column.</span></span>

1. <span data-ttu-id="61525-145">登入 toohello [Azure 入口網站](https://portal.azure.com/)和選取 hello Azure AD Privileged Identity Management 磚。</span><span class="sxs-lookup"><span data-stu-id="61525-145">Sign in toohello [Azure portal](https://portal.azure.com/) and select hello Azure AD Privileged Identity Management tile.</span></span>
2. <span data-ttu-id="61525-146">選取 [我的角色]。</span><span class="sxs-lookup"><span data-stu-id="61525-146">Select **My Roles**.</span></span> <span data-ttu-id="61525-147">指派的合格角色的清單會出現在 hello hello 頁面頂端的 hello 分組。</span><span class="sxs-lookup"><span data-stu-id="61525-147">A list of your assigned eligible roles appear in hello grouping at hello top of hello page.</span></span>
3. <span data-ttu-id="61525-148">選取角色。</span><span class="sxs-lookup"><span data-stu-id="61525-148">Select a role.</span></span>
4. <span data-ttu-id="61525-149">選取 hello**啟用正在等待核准**橫幅 hello 角色啟用詳細資料 刀鋒視窗上。</span><span class="sxs-lookup"><span data-stu-id="61525-149">Select hello **Activation is pending approval** banner on hello role activation details blade.</span></span>
5. <span data-ttu-id="61525-150">選取**取消**頂端的 hello hello**等待核准**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="61525-150">Select **Cancel** at hello top of hello **Pending approval** blade.</span></span>

   ![取消擱置要求螢幕擷取畫面][4]

## <a name="next-steps"></a><span data-ttu-id="61525-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="61525-152">Next steps</span></span>
<span data-ttu-id="61525-153">如果您想要了解更多關於 Azure AD Privileged Identity Management，hello 下列連結有更多的資訊。</span><span class="sxs-lookup"><span data-stu-id="61525-153">If you're interested in learning more about Azure AD Privileged Identity Management, hello following links have more information.</span></span>

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_activation_MFA.png
[3]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Toast2.png
[4]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Banner_Cancel.png
