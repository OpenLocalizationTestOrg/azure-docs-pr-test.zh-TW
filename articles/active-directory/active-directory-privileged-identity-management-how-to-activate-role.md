---
title: "如何啟用或停用角色 | Microsoft Docs"
description: "了解如何利用 Azure Privileged Identity Management 應用程式，啟用特殊權限身分識別的角色。"
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
ms.openlocfilehash: a143fd78eae52fda0cbadb7e74fd8209f24629a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-activate-or-deactivate-roles-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="22cce-103">Azure AD Privileged Identity Management：如何啟用或停用角色</span><span class="sxs-lookup"><span data-stu-id="22cce-103">How to activate or deactivate roles in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="22cce-104">Azure Active Directory (AD) Privileged Identity Management 簡化了企業管理以特殊權限身分存取 Azure AD 中的資源和其他 Microsoft 線上服務 (如 Office 365 或 Microsoft Intune) 的方式。</span><span class="sxs-lookup"><span data-stu-id="22cce-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="22cce-105">如果您已被設為符合系統管理角色資格，即表示您可以在需要執行特殊權限動作時，啟用該角色。</span><span class="sxs-lookup"><span data-stu-id="22cce-105">If you have been made eligible for an administrative role, that means you can activate that role when you need to perform privileged actions.</span></span> <span data-ttu-id="22cce-106">例如，如果您偶爾會管理 Office 365 功能，則貴組織的特殊權限角色管理員可能不會讓您成為永久全域管理員，因為該角色也會影響其他服務。</span><span class="sxs-lookup"><span data-stu-id="22cce-106">For example, if you occasionally manage Office 365 features, your organization's privileged role administrators may not make you a permanent Global Administrator, since that role impacts other services, too.</span></span> <span data-ttu-id="22cce-107">他們反而會讓您符合 Azure AD 角色 (例如「Exchange Online 管理員」) 的資格。</span><span class="sxs-lookup"><span data-stu-id="22cce-107">Instead, they make you eligible for Azure AD roles such as Exchange Online Administrator.</span></span> <span data-ttu-id="22cce-108">您可以在需要權限時，要求停用該角色，然後您將會在預定的時段內擁有系統管理控制權。</span><span class="sxs-lookup"><span data-stu-id="22cce-108">You can request to activate that role when you need its privileges, and then you'll have admin control for a predetermined time period.</span></span>

<span data-ttu-id="22cce-109">本文適用對象是必須在 Azure AD Privileged Identity Management (PIM) 中啟用其角色的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="22cce-109">This article is for admins who need to activate their role in Azure AD Privileged Identity Management (PIM).</span></span> <span data-ttu-id="22cce-110">它會逐步引導您在需要權限時啟用角色，並在完成時停用角色。</span><span class="sxs-lookup"><span data-stu-id="22cce-110">It walks you through the steps to activate a role when you need the permissions, and deactivate the role when you're done.</span></span> <span data-ttu-id="22cce-111">此外，特殊權限角色系統管理員可以要求核准以啟用角色 (預覽)。</span><span class="sxs-lookup"><span data-stu-id="22cce-111">In addition, privileged role administrators can require approval to activate a role (Preview).</span></span> <span data-ttu-id="22cce-112">在這裡深入了解 [PIM 核准工作流程](./privileged-identity-management/azure-ad-pim-approval-workflow.md)。</span><span class="sxs-lookup"><span data-stu-id="22cce-112">Learn more about [PIM Approval Workflows](./privileged-identity-management/azure-ad-pim-approval-workflow.md) here.</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="22cce-113">加入 Privileged Identity Management 應用程式</span><span class="sxs-lookup"><span data-stu-id="22cce-113">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="22cce-114">請在 [Azure 入口網站](https://portal.azure.com/) 中使用 Azure AD Privileged Identity Management 應用程式來要求角色啟用，即使您是要在另一個入口網站中或透過 PowerShell 來操作，也是如此。</span><span class="sxs-lookup"><span data-stu-id="22cce-114">Use the Azure AD Privileged Identity Management application in the [Azure portal](https://portal.azure.com/) to request a role activation, even if you're going to operate in another portal or PowerShell.</span></span> <span data-ttu-id="22cce-115">如果您在 Azure 入口網站沒有 Azure AD Privileged Identity Management 應用程式，請遵循下列步驟操作。</span><span class="sxs-lookup"><span data-stu-id="22cce-115">If you don't have the Azure AD Privileged Identity Management application on your Azure portal, follow these steps to get started.</span></span>

1. <span data-ttu-id="22cce-116">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="22cce-116">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="22cce-117">選取 Azure 入口網站右上角的使用者名稱，然後選取您要操作的目錄。</span><span class="sxs-lookup"><span data-stu-id="22cce-117">Select your username in the upper right-hand corner of the Azure portal, and select the directory where you will you be operating.</span></span>
3. <span data-ttu-id="22cce-118">選取 [更多服務] 並使用 [篩選器] 文字方塊來搜尋 [Azure AD Privileged Identity Management]。</span><span class="sxs-lookup"><span data-stu-id="22cce-118">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="22cce-119">選取 [釘選到儀表板]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="22cce-119">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="22cce-120">Privileged Identity Management 應用程式隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="22cce-120">The Privileged Identity Management application opens.</span></span>

## <a name="activate-a-role"></a><span data-ttu-id="22cce-121">啟用角色</span><span class="sxs-lookup"><span data-stu-id="22cce-121">Activate a role</span></span>
<span data-ttu-id="22cce-122">當您需要擔任某個角色時，您可以選取 Azure AD Privileged Identity Management 應用程式左側瀏覽資料行中的 [我的角色] 瀏覽選項來要求啟用。</span><span class="sxs-lookup"><span data-stu-id="22cce-122">When you need to take on a role, you can request activation by selecting the **My Roles** navigation option in the Azure AD Privileged Identity Management application's left navigation column.</span></span>

1. <span data-ttu-id="22cce-123">登入 [Azure 入口網站](https://portal.azure.com/) ，選取 [Azure AD Privileged Identity Management] 圖格。</span><span class="sxs-lookup"><span data-stu-id="22cce-123">Sign in to the [Azure portal](https://portal.azure.com/) and select the Azure AD Privileged Identity Management tile.</span></span>
2. <span data-ttu-id="22cce-124">選取 [我的角色]。</span><span class="sxs-lookup"><span data-stu-id="22cce-124">Select **My Roles**.</span></span> <span data-ttu-id="22cce-125">指派的合格角色清單會出現在分頁頂端的群組。</span><span class="sxs-lookup"><span data-stu-id="22cce-125">A list of your assigned eligible roles appear in the grouping at the top of the page.</span></span>
3. <span data-ttu-id="22cce-126">選取要啟用的角色。</span><span class="sxs-lookup"><span data-stu-id="22cce-126">Select a role to activate.</span></span>
4. <span data-ttu-id="22cce-127">選取 [ **啟用**]。</span><span class="sxs-lookup"><span data-stu-id="22cce-127">Select **Activate**.</span></span> <span data-ttu-id="22cce-128">[要求啟用角色]  刀鋒視窗隨即出現。</span><span class="sxs-lookup"><span data-stu-id="22cce-128">The **Request role activation** blade appears.</span></span>
5. <span data-ttu-id="22cce-129">有些角色會要求必須先執行 Multi-Factor Authentication (MFA) 才能啟用。</span><span class="sxs-lookup"><span data-stu-id="22cce-129">Some roles require Multi-Factor Authentication (MFA) before you can activate the role.</span></span> <span data-ttu-id="22cce-130">您只需在每個工作階段驗證一次。</span><span class="sxs-lookup"><span data-stu-id="22cce-130">You only have to authenticate once per session.</span></span>
   
    ![在啟用角色之前先以 MFA 驗證 - 螢幕擷取畫面][2]
6. <span data-ttu-id="22cce-132">在啟用要求的文字欄位中輸入啟用原因。</span><span class="sxs-lookup"><span data-stu-id="22cce-132">Enter the reason for the activation request in the text field.</span></span>  <span data-ttu-id="22cce-133">有些角色會要求您提供問題票證號碼。</span><span class="sxs-lookup"><span data-stu-id="22cce-133">Some roles require you to supply a trouble ticket number.</span></span>
7. <span data-ttu-id="22cce-134">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="22cce-134">Select **OK**.</span></span>  <span data-ttu-id="22cce-135">如果角色不需要核准，它現在就會啟用，角色會出現在使用中角色的清單中 (符合角色指派資格清單正下方)。</span><span class="sxs-lookup"><span data-stu-id="22cce-135">If the role does not require approval, it is now activated, and the role appears in the list of active roles (directly below the list of eligible role assignments).</span></span> <span data-ttu-id="22cce-136">如果[角色需要核准](./privileged-identity-management/azure-ad-pim-approval-workflow.md)才能啟用，快顯通知會短暫出現在瀏覽器右上角，通知您要求正在等待核准。</span><span class="sxs-lookup"><span data-stu-id="22cce-136">If the [role requires approval](./privileged-identity-management/azure-ad-pim-approval-workflow.md) to activate, a toast notification will briefly appear in the upper right-hand corner of your browser informing you the request is pending approval.</span></span>

    ![要求擱置通知 - 螢幕擷取畫面][3]

## <a name="deactivate-a-role"></a><span data-ttu-id="22cce-138">停用角色</span><span class="sxs-lookup"><span data-stu-id="22cce-138">Deactivate a role</span></span>
<span data-ttu-id="22cce-139">角色一經啟用，就會在達到時間限制 (合格的持續時間) 時自動停用。</span><span class="sxs-lookup"><span data-stu-id="22cce-139">Once a role has been activated, it automatically deactivates when its time limit (eligible duration) is reached.</span></span>

<span data-ttu-id="22cce-140">如果您提早完成管理員工作，也可以在 Azure AD Privileged Identity Management 應用程式中手動停用角色。</span><span class="sxs-lookup"><span data-stu-id="22cce-140">If you complete your admin tasks early, you can also deactivate a role manually in the Azure AD Privileged Identity Management application.</span></span>  <span data-ttu-id="22cce-141">選取 [我的角色]，從 [使用中角色指派] 群組中選擇完成使用的角色，然後選取 [停用]。</span><span class="sxs-lookup"><span data-stu-id="22cce-141">Select **My Roles**, choose the role you're done using from the **Active role assignments** grouping, and select **Deactivate**.</span></span>  

## <a name="cancel-a-pending-request"></a><span data-ttu-id="22cce-142">取消擱置要求</span><span class="sxs-lookup"><span data-stu-id="22cce-142">Cancel a pending request</span></span>
<span data-ttu-id="22cce-143">萬一您不需要啟用需要核准的角色，您可以隨時取消擱置要求。</span><span class="sxs-lookup"><span data-stu-id="22cce-143">In the event you do not require activation of a role that requires approval, you may cancel a pending request at any time.</span></span> <span data-ttu-id="22cce-144">只要選取 Azure AD Privileged Identity Management 應用程式左側瀏覽資料行中的 [我的角色] 瀏覽選項即可。</span><span class="sxs-lookup"><span data-stu-id="22cce-144">Simply select the **My Roles** navigation option in the Azure AD Privileged Identity Management application's left navigation column.</span></span>

1. <span data-ttu-id="22cce-145">登入 [Azure 入口網站](https://portal.azure.com/) ，選取 [Azure AD Privileged Identity Management] 圖格。</span><span class="sxs-lookup"><span data-stu-id="22cce-145">Sign in to the [Azure portal](https://portal.azure.com/) and select the Azure AD Privileged Identity Management tile.</span></span>
2. <span data-ttu-id="22cce-146">選取 [我的角色]。</span><span class="sxs-lookup"><span data-stu-id="22cce-146">Select **My Roles**.</span></span> <span data-ttu-id="22cce-147">指派的合格角色清單會出現在分頁頂端的群組。</span><span class="sxs-lookup"><span data-stu-id="22cce-147">A list of your assigned eligible roles appear in the grouping at the top of the page.</span></span>
3. <span data-ttu-id="22cce-148">選取角色。</span><span class="sxs-lookup"><span data-stu-id="22cce-148">Select a role.</span></span>
4. <span data-ttu-id="22cce-149">選取角色啟用詳細資料刀鋒視窗上的 [啟用正在等待核准] 橫幅。</span><span class="sxs-lookup"><span data-stu-id="22cce-149">Select the **Activation is pending approval** banner on the role activation details blade.</span></span>
5. <span data-ttu-id="22cce-150">選取 [等待核准] 刀鋒視窗頂端的 [取消]。</span><span class="sxs-lookup"><span data-stu-id="22cce-150">Select **Cancel** at the top of the **Pending approval** blade.</span></span>

   ![取消擱置要求螢幕擷取畫面][4]

## <a name="next-steps"></a><span data-ttu-id="22cce-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="22cce-152">Next steps</span></span>
<span data-ttu-id="22cce-153">如果您有興趣進一步了解 Azure AD Privileged Identity Management，下列連結會提供詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="22cce-153">If you're interested in learning more about Azure AD Privileged Identity Management, the following links have more information.</span></span>

[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_activation_MFA.png
[3]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Toast2.png
[4]: ./media/active-directory-privileged-identity-management-how-to-activate-role/PIM_Request_Pending_Banner_Cancel.png
