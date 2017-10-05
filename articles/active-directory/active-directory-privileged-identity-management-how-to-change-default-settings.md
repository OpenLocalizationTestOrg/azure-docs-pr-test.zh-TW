---
title: "如何管理角色啟用設定 | Microsoft Docs"
description: "了解如何利用 Azure AD Privileged Identity Management 擴充功能，變更特殊權限身分識別的預設設定。"
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
ms.openlocfilehash: 23605e89cd1846d2e06e48cb5d3e0191cb9e9b4a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-role-activation-settings-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="da013-103">如何管理 Azure AD Privileged Identity Management 的角色啟用設定</span><span class="sxs-lookup"><span data-stu-id="da013-103">How to manage role activation settings in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="da013-104">特殊權限角色管理員可以自訂其組織中的 Azure AD Privileged Identity Management (PIM)，包括變更啟用合格角色指派之使用者的體驗。</span><span class="sxs-lookup"><span data-stu-id="da013-104">A privileged role administrator can customize Azure AD Privileged Identity Management (PIM) in their organization, including changing the experience for a user who is activating an eligible role assignment.</span></span>

## <a name="manage-the-role-activation-settings"></a><span data-ttu-id="da013-105">管理角色啟用設定</span><span class="sxs-lookup"><span data-stu-id="da013-105">Manage the role activation settings</span></span>
1. <span data-ttu-id="da013-106">移至 [Azure 入口網站](https://portal.azure.com)，然後從儀表板中選取 [Azure AD Privileged Identity Management] 應用程式。</span><span class="sxs-lookup"><span data-stu-id="da013-106">Go to the [Azure portal](https://portal.azure.com) and select the **Azure AD Privileged Identity Management** app from the dashboard.</span></span>
2. <span data-ttu-id="da013-107">選取 [管理特殊權限角色] > [設定] > [特殊權限角色]。</span><span class="sxs-lookup"><span data-stu-id="da013-107">Select **Manage privileged roles** > **Settings** > **Privileged Roles**.</span></span>
3. <span data-ttu-id="da013-108">選擇您想要管理其設定的角色。</span><span class="sxs-lookup"><span data-stu-id="da013-108">Choose the role whose settings you want to manage.</span></span>

<span data-ttu-id="da013-109">在每個角色的設定頁面上，有一些您可以設定的設定。</span><span class="sxs-lookup"><span data-stu-id="da013-109">On the settings page for each role, there are a number of settings you can configure.</span></span> <span data-ttu-id="da013-110">這些設定只會影響身為合格系統管理員 (而不是永久系統管理員) 的使用者。</span><span class="sxs-lookup"><span data-stu-id="da013-110">These settings only affect users who are eligible admins, not permanent admins.</span></span>

<span data-ttu-id="da013-111">**啟用**︰角色在到期前維持作用中狀態的時間 (以小時為單位)。</span><span class="sxs-lookup"><span data-stu-id="da013-111">**Activations**: The time, in hours, that a role stays active before it expires.</span></span> <span data-ttu-id="da013-112">此時間可介於 1 到 72 小時。</span><span class="sxs-lookup"><span data-stu-id="da013-112">This can be between 1 and 72 hours.</span></span>

<span data-ttu-id="da013-113">**通知**︰您可以選擇是否要讓系統傳送電子郵件給系統管理員來確認他們已啟用角色。</span><span class="sxs-lookup"><span data-stu-id="da013-113">**Notifications**: You can choose whether or not the system sends emails to admins confirming that they have activated a role.</span></span> <span data-ttu-id="da013-114">這對偵測未經授權或不合法的啟用而言相當有用。</span><span class="sxs-lookup"><span data-stu-id="da013-114">This can be useful for detecting unauthorized or illegitimate activations.</span></span>

<span data-ttu-id="da013-115">**事件/要求票證**︰您可以選擇是否要要求合格系統管理員在啟用其角色時包含票證號碼。</span><span class="sxs-lookup"><span data-stu-id="da013-115">**Incident/Request Ticket**: You can choose whether or not to require eligible admins to include a ticket number when they activate their role.</span></span> <span data-ttu-id="da013-116">當您執行角色存取稽核時，這會相當有用。</span><span class="sxs-lookup"><span data-stu-id="da013-116">This can be useful when you perform role access audits.</span></span>

<span data-ttu-id="da013-117">**Multi-Factor Authentication**：您可以選擇是否要要求使用者在啟用其角色之前，先以 MFA 驗證其身分識別。</span><span class="sxs-lookup"><span data-stu-id="da013-117">**Multi-Factor Authentication**: You can choose whether or not to require users to verify their identity with MFA before they can activate their roles.</span></span> <span data-ttu-id="da013-118">他們只需在每一工作階段進行一次驗證，而不需在每次啟用角色時都進行驗證。</span><span class="sxs-lookup"><span data-stu-id="da013-118">They only have to verify this once per session, not every time they activate a role.</span></span> <span data-ttu-id="da013-119">啟用 MFA 時，需要記住兩個秘訣：</span><span class="sxs-lookup"><span data-stu-id="da013-119">There are two tips to keep in mind when you enable MFA:</span></span>

* <span data-ttu-id="da013-120">具有 Microsoft 帳戶的電子郵件地址的使用者 (通常@outlook.com，但並非一定) 無法為 Azure MFA 進行註冊。</span><span class="sxs-lookup"><span data-stu-id="da013-120">Users who have Microsoft accounts for their email addresses (typically @outlook.com, but not always) cannot register for Azure MFA.</span></span> <span data-ttu-id="da013-121">如果您想要將角色指派給使用 Microsoft 帳戶的使用者，您應該將他們設為永久系統管理員，或是停用該角色的 MFA。</span><span class="sxs-lookup"><span data-stu-id="da013-121">If you want to assign roles to users with Microsoft accounts, you should either make them permanent admins or disable MFA for that role.</span></span>
* <span data-ttu-id="da013-122">您無法將 Azure AD 和 Office365 中高特殊權限角色的 MFA 停用。</span><span class="sxs-lookup"><span data-stu-id="da013-122">You cannot disable MFA for highly privileged roles for Azure AD and Office365.</span></span> <span data-ttu-id="da013-123">這是一項安全功能，因為這些角色應該嚴密地受到保護：</span><span class="sxs-lookup"><span data-stu-id="da013-123">This is a safety feature because these roles should be carefully protected:</span></span>  
  
  * <span data-ttu-id="da013-124">應用程式管理員</span><span class="sxs-lookup"><span data-stu-id="da013-124">Application administrator</span></span>
  * <span data-ttu-id="da013-125">應用程式 Proxy 伺服器管理員</span><span class="sxs-lookup"><span data-stu-id="da013-125">Application Proxy server administrator</span></span>
  * <span data-ttu-id="da013-126">計費管理員</span><span class="sxs-lookup"><span data-stu-id="da013-126">Billing administrator</span></span>  
  * <span data-ttu-id="da013-127">規範管理員</span><span class="sxs-lookup"><span data-stu-id="da013-127">Compliance administrator</span></span>  
  * <span data-ttu-id="da013-128">CRM 服務管理員</span><span class="sxs-lookup"><span data-stu-id="da013-128">CRM service administrator</span></span>
  * <span data-ttu-id="da013-129">客戶 LockBox 存取核准者</span><span class="sxs-lookup"><span data-stu-id="da013-129">Customer LockBox access approver</span></span>
  * <span data-ttu-id="da013-130">目錄寫入器</span><span class="sxs-lookup"><span data-stu-id="da013-130">Directory writer</span></span>  
  * <span data-ttu-id="da013-131">Exchange 系統管理員</span><span class="sxs-lookup"><span data-stu-id="da013-131">Exchange administrator</span></span>  
  * <span data-ttu-id="da013-132">全域管理員</span><span class="sxs-lookup"><span data-stu-id="da013-132">Global administrator</span></span>
  * <span data-ttu-id="da013-133">Intune 服務管理員</span><span class="sxs-lookup"><span data-stu-id="da013-133">Intune service administrator</span></span>
  * <span data-ttu-id="da013-134">信箱管理員</span><span class="sxs-lookup"><span data-stu-id="da013-134">Mailbox administrator</span></span>  
  * <span data-ttu-id="da013-135">合作夥伴第 1 層支援</span><span class="sxs-lookup"><span data-stu-id="da013-135">Partner tier1 support</span></span>  
  * <span data-ttu-id="da013-136">合作夥伴第 2 層支援</span><span class="sxs-lookup"><span data-stu-id="da013-136">Partner tier2 support</span></span>  
  * <span data-ttu-id="da013-137">特殊權限角色管理員</span><span class="sxs-lookup"><span data-stu-id="da013-137">Privileged role administrator</span></span>   
  * <span data-ttu-id="da013-138">安全性系統管理員</span><span class="sxs-lookup"><span data-stu-id="da013-138">Security administrator</span></span>  
  * <span data-ttu-id="da013-139">SharePoint 管理員</span><span class="sxs-lookup"><span data-stu-id="da013-139">SharePoint administrator</span></span>  
  * <span data-ttu-id="da013-140">商務用 Skype 的管理員</span><span class="sxs-lookup"><span data-stu-id="da013-140">Skype for Business administrator</span></span>  
  * <span data-ttu-id="da013-141">使用者帳戶管理員</span><span class="sxs-lookup"><span data-stu-id="da013-141">User account administrator</span></span>  

<span data-ttu-id="da013-142">如需關於搭配 PIM 使用 MFA 的詳細資訊，請參閱 [如何要求 MFA](active-directory-privileged-identity-management-how-to-require-mfa.md)。</span><span class="sxs-lookup"><span data-stu-id="da013-142">For more information about using MFA with PIM see [How to Require MFA](active-directory-privileged-identity-management-how-to-require-mfa.md).</span></span>

<!--PLACEHOLDER: Need an explanation of what the temporary Global Administrator setting is for.-->

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="da013-143">後續步驟</span><span class="sxs-lookup"><span data-stu-id="da013-143">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

