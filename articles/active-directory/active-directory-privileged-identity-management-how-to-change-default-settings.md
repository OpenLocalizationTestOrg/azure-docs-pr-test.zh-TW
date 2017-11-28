---
title: "aaaHow toomanage 角色啟用設定 |Microsoft 文件"
description: "了解如何 toochange hello 以 hello Azure Active Directory Privileged Identity Management 延伸模組的預設設定為特殊權限的身分識別。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: f6cbcb6a-8a89-4077-afd8-06c94a64f4aa
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 453bb6f8f8e0fd2598cb073ef86c1dd55458dc72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-role-activation-settings-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="89634-103">如何在 Azure AD Privileged Identity Management toomanage 角色啟用設定</span><span class="sxs-lookup"><span data-stu-id="89634-103">How toomanage role activation settings in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="89634-104">特殊權限的角色系統管理員可以自訂 Azure AD Privileged Identity Management (PIM) 在其組織中，其中包括變更 hello 啟用中的合格的角色指派的使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="89634-104">A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing hello experience for a user who is activating an eligible role assignment.</span></span>

## <a name="manage-hello-role-activation-settings"></a><span data-ttu-id="89634-105">管理 hello 角色啟用設定</span><span class="sxs-lookup"><span data-stu-id="89634-105">Manage hello role activation settings</span></span>
1. <span data-ttu-id="89634-106">移 toohello [Azure 入口網站](https://portal.azure.com)和選取 hello **Azure AD Privileged Identity Management** hello 儀表板中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="89634-106">Go toohello [Azure portal](https://portal.azure.com) and select hello **Azure AD Privileged Identity Management** app from hello dashboard.</span></span>
2. <span data-ttu-id="89634-107">選取 [管理特殊權限角色] > [設定] > [特殊權限角色]。</span><span class="sxs-lookup"><span data-stu-id="89634-107">Select **Manage privileged roles** > **Settings** > **Privileged Roles**.</span></span>
3. <span data-ttu-id="89634-108">選擇 hello 角色其設定您想要 toomanage。</span><span class="sxs-lookup"><span data-stu-id="89634-108">Choose hello role whose settings you want toomanage.</span></span>

<span data-ttu-id="89634-109">在 hello [設定] 頁面上，針對每個角色，有一些您可以設定的設定。</span><span class="sxs-lookup"><span data-stu-id="89634-109">On hello settings page for each role, there are a number of settings you can configure.</span></span> <span data-ttu-id="89634-110">這些設定只會影響身為合格系統管理員 (而不是永久系統管理員) 的使用者。</span><span class="sxs-lookup"><span data-stu-id="89634-110">These settings only affect users who are eligible admins, not permanent admins.</span></span>

<span data-ttu-id="89634-111">**啟用**: hello 的時間，以小時為單位的角色在過期前維持作用中。</span><span class="sxs-lookup"><span data-stu-id="89634-111">**Activations**: hello time, in hours, that a role stays active before it expires.</span></span> <span data-ttu-id="89634-112">此時間可介於 1 到 72 小時。</span><span class="sxs-lookup"><span data-stu-id="89634-112">This can be between 1 and 72 hours.</span></span>

<span data-ttu-id="89634-113">**通知**： 您可以選擇是否 hello 系統會傳送電子郵件 tooadmins 確認他們已啟用的角色。</span><span class="sxs-lookup"><span data-stu-id="89634-113">**Notifications**: You can choose whether or not hello system sends emails tooadmins confirming that they have activated a role.</span></span> <span data-ttu-id="89634-114">這對偵測未經授權或不合法的啟用而言相當有用。</span><span class="sxs-lookup"><span data-stu-id="89634-114">This can be useful for detecting unauthorized or illegitimate activations.</span></span>

<span data-ttu-id="89634-115">**事件/要求票證**： 您可以選擇啟用其角色時，不論是否編號 toorequire 合格 admins tooinclude 票證。</span><span class="sxs-lookup"><span data-stu-id="89634-115">**Incident/Request Ticket**: You can choose whether or not toorequire eligible admins tooinclude a ticket number when they activate their role.</span></span> <span data-ttu-id="89634-116">當您執行角色存取稽核時，這會相當有用。</span><span class="sxs-lookup"><span data-stu-id="89634-116">This can be useful when you perform role access audits.</span></span>

<span data-ttu-id="89634-117">**Multi-factor Authentication**： 您可以選擇是否 toorequire 使用者 tooverify mfa，才能啟用其角色其身分識別。</span><span class="sxs-lookup"><span data-stu-id="89634-117">**Multi-Factor Authentication**: You can choose whether or not toorequire users tooverify their identity with MFA before they can activate their roles.</span></span> <span data-ttu-id="89634-118">它們只能有 tooverify 每個工作階段，每次在啟用角色不一次。</span><span class="sxs-lookup"><span data-stu-id="89634-118">They only have tooverify this once per session, not every time they activate a role.</span></span> <span data-ttu-id="89634-119">當您啟用 MFA 記住有兩個秘訣 tookeep:</span><span class="sxs-lookup"><span data-stu-id="89634-119">There are two tips tookeep in mind when you enable MFA:</span></span>

* <span data-ttu-id="89634-120">具有 Microsoft 帳戶的電子郵件地址的使用者 (通常@outlook.com，但並非一定) 無法為 Azure MFA 進行註冊。</span><span class="sxs-lookup"><span data-stu-id="89634-120">Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA.</span></span> <span data-ttu-id="89634-121">如果您想 tooassign 角色 toousers 與 Microsoft 帳戶，您應該讓它們永久的系統管理員或停用 MFA，該角色。</span><span class="sxs-lookup"><span data-stu-id="89634-121">If you want tooassign roles toousers with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.</span></span>
* <span data-ttu-id="89634-122">您無法將 Azure AD 和 Office365 中高特殊權限角色的 MFA 停用。</span><span class="sxs-lookup"><span data-stu-id="89634-122">You cannot disable MFA for highly privileged roles for Azure AD and Office365.</span></span> <span data-ttu-id="89634-123">這是一項安全功能，因為這些角色應該嚴密地受到保護：</span><span class="sxs-lookup"><span data-stu-id="89634-123">This is a safety feature because these roles should be carefully protected:</span></span>  
  
  * <span data-ttu-id="89634-124">應用程式管理員</span><span class="sxs-lookup"><span data-stu-id="89634-124">Application administrator</span></span>
  * <span data-ttu-id="89634-125">應用程式 Proxy 伺服器管理員</span><span class="sxs-lookup"><span data-stu-id="89634-125">Application Proxy server administrator</span></span>
  * <span data-ttu-id="89634-126">計費管理員</span><span class="sxs-lookup"><span data-stu-id="89634-126">Billing administrator</span></span>  
  * <span data-ttu-id="89634-127">規範管理員</span><span class="sxs-lookup"><span data-stu-id="89634-127">Compliance administrator</span></span>  
  * <span data-ttu-id="89634-128">CRM 服務管理員</span><span class="sxs-lookup"><span data-stu-id="89634-128">CRM service administrator</span></span>
  * <span data-ttu-id="89634-129">客戶 LockBox 存取核准者</span><span class="sxs-lookup"><span data-stu-id="89634-129">Customer LockBox access approver</span></span>
  * <span data-ttu-id="89634-130">目錄寫入器</span><span class="sxs-lookup"><span data-stu-id="89634-130">Directory writer</span></span>  
  * <span data-ttu-id="89634-131">Exchange 系統管理員</span><span class="sxs-lookup"><span data-stu-id="89634-131">Exchange administrator</span></span>  
  * <span data-ttu-id="89634-132">全域管理員</span><span class="sxs-lookup"><span data-stu-id="89634-132">Global administrator</span></span>
  * <span data-ttu-id="89634-133">Intune 服務管理員</span><span class="sxs-lookup"><span data-stu-id="89634-133">Intune service administrator</span></span>
  * <span data-ttu-id="89634-134">信箱管理員</span><span class="sxs-lookup"><span data-stu-id="89634-134">Mailbox administrator</span></span>  
  * <span data-ttu-id="89634-135">合作夥伴第 1 層支援</span><span class="sxs-lookup"><span data-stu-id="89634-135">Partner tier1 support</span></span>  
  * <span data-ttu-id="89634-136">合作夥伴第 2 層支援</span><span class="sxs-lookup"><span data-stu-id="89634-136">Partner tier2 support</span></span>  
  * <span data-ttu-id="89634-137">特殊權限角色管理員</span><span class="sxs-lookup"><span data-stu-id="89634-137">Privileged role administrator</span></span>   
  * <span data-ttu-id="89634-138">安全性系統管理員</span><span class="sxs-lookup"><span data-stu-id="89634-138">Security administrator</span></span>  
  * <span data-ttu-id="89634-139">SharePoint 管理員</span><span class="sxs-lookup"><span data-stu-id="89634-139">SharePoint administrator</span></span>  
  * <span data-ttu-id="89634-140">商務用 Skype 的管理員</span><span class="sxs-lookup"><span data-stu-id="89634-140">Skype for Business administrator</span></span>  
  * <span data-ttu-id="89634-141">使用者帳戶管理員</span><span class="sxs-lookup"><span data-stu-id="89634-141">User account administrator</span></span>  

<span data-ttu-id="89634-142">如需使用 MFA PIM 的詳細資訊，請參閱[如何 tooRequire MFA](active-directory-privileged-identity-management-how-to-require-mfa.md)。</span><span class="sxs-lookup"><span data-stu-id="89634-142">For more information about using MFA with PIM see [How tooRequire MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span></span>

<!--PLACEHOLDER: Need an explanation of what hello temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="89634-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="89634-143">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

