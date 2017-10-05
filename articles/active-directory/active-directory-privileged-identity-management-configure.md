---
title: "設定 Azure AD Privileged Identity Management | Microsoft Docs"
description: "本主題說明何謂 Azure AD Privileged Identity Management，以及如何使用 PIM 改善雲端安全性。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: c548ed2e-06e3-4eaf-a63d-0f02ee72da25
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: billmath
ms.custom: pim ; H1Hack27Feb2017
ms.openlocfilehash: eb7059368cb80be7dd625f9dc6ad2aab1bad709a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-ad-privileged-identity-management"></a><span data-ttu-id="42bc8-103">什麼是 Azure AD Privileged Identity Management？</span><span class="sxs-lookup"><span data-stu-id="42bc8-103">What is Azure AD Privileged Identity Management?</span></span>
<span data-ttu-id="42bc8-104">您可以利用 Azure Active Directory (AD) Privileged Identity Management 來管理、控制和監視組織內的存取行為。</span><span class="sxs-lookup"><span data-stu-id="42bc8-104">With Azure Active Directory (AD) Privileged Identity Management, you can manage, control, and monitor access within your organization.</span></span> <span data-ttu-id="42bc8-105">這包括存取 Azure AD 中的資源和其他 Microsoft 線上服務，例如 Office 365 或 Microsoft Intune。</span><span class="sxs-lookup"><span data-stu-id="42bc8-105">This includes access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

> [!NOTE]
> <span data-ttu-id="42bc8-106">當您將 Azure Active Directory 的 Premium P2 版本授權給系統管理員時，Privileged Identity Management 可供您的整個組織使用。</span><span class="sxs-lookup"><span data-stu-id="42bc8-106">Privileged Identity Management is available to your entire organization when you license your Administrators with the Premium P2 edition of Azure Active Directory.</span></span> <span data-ttu-id="42bc8-107">如需詳細資訊，請參閱 [Azure Active Directory 版本](active-directory-editions.md)。</span><span class="sxs-lookup"><span data-stu-id="42bc8-107">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

<span data-ttu-id="42bc8-108">組織想要將能夠存取安全資訊或資源的人數降到最低，因為這樣可以降低惡意使用者取得該存取權的機率。</span><span class="sxs-lookup"><span data-stu-id="42bc8-108">Organizations want to minimize the number of people who have access to secure information or resources, because that reduces the chance of a malicious user getting that access.</span></span> <span data-ttu-id="42bc8-109">不過，使用者仍然需要在 Azure、Office 365 或 SaaS 應用程式中執行特殊權限作業。</span><span class="sxs-lookup"><span data-stu-id="42bc8-109">However, users still need to carry out privileged operations in Azure, Office 365, or SaaS apps.</span></span> <span data-ttu-id="42bc8-110">組織可以在 Azure AD 中授與使用者特殊權限，而不需監視這些使用者使用其系統管理權限來執行什麼作業。</span><span class="sxs-lookup"><span data-stu-id="42bc8-110">Organizations give users privileged access in Azure AD without monitoring what those users are doing with their admin privileges.</span></span> <span data-ttu-id="42bc8-111">Azure AD 特殊權限身分識別管理有助於解決此風險。</span><span class="sxs-lookup"><span data-stu-id="42bc8-111">Azure AD Privileged Identity Management helps to resolve this risk.</span></span>  

<span data-ttu-id="42bc8-112">Azure AD Privileged Identity Management 可協助您：</span><span class="sxs-lookup"><span data-stu-id="42bc8-112">Azure AD Privileged Identity Management helps you:</span></span>  

* <span data-ttu-id="42bc8-113">查看哪些使用者是 Azure AD 管理員</span><span class="sxs-lookup"><span data-stu-id="42bc8-113">See which users are Azure AD administrators</span></span>
* <span data-ttu-id="42bc8-114">視需要啟用 Office 365 和 Intune 等 Microsoft Online Services 的 "just-in-time" 系統管理存取權限</span><span class="sxs-lookup"><span data-stu-id="42bc8-114">Enable on-demand, "just in time" administrative access to Microsoft Online Services like Office 365 and Intune</span></span>
* <span data-ttu-id="42bc8-115">取得有關系統管理員存取記錄與系統管理員指派變更的報告</span><span class="sxs-lookup"><span data-stu-id="42bc8-115">Get reports about administrator access history and changes in administrator assignments</span></span>
* <span data-ttu-id="42bc8-116">取得有關特殊權限角色存取的警示</span><span class="sxs-lookup"><span data-stu-id="42bc8-116">Get alerts about access to a privileged role</span></span>
* <span data-ttu-id="42bc8-117">需要核准才能啟動 (預覽)</span><span class="sxs-lookup"><span data-stu-id="42bc8-117">Require approval to activate (Preview)</span></span>

<span data-ttu-id="42bc8-118">Azure AD Privileged Identity Management 可以管理內建的 Azure AD 組織角色，包括 (但不限於)：</span><span class="sxs-lookup"><span data-stu-id="42bc8-118">Azure AD Privileged Identity Management can manage the built-in Azure AD organizational roles, including (but not limited to):</span></span>  

* <span data-ttu-id="42bc8-119">全域管理員</span><span class="sxs-lookup"><span data-stu-id="42bc8-119">Global Administrator</span></span>
* <span data-ttu-id="42bc8-120">計費管理員</span><span class="sxs-lookup"><span data-stu-id="42bc8-120">Billing Administrator</span></span>
* <span data-ttu-id="42bc8-121">服務管理員</span><span class="sxs-lookup"><span data-stu-id="42bc8-121">Service Administrator</span></span>  
* <span data-ttu-id="42bc8-122">使用者管理員</span><span class="sxs-lookup"><span data-stu-id="42bc8-122">User Administrator</span></span>
* <span data-ttu-id="42bc8-123">密碼管理員</span><span class="sxs-lookup"><span data-stu-id="42bc8-123">Password Administrator</span></span>

## <a name="just-in-time-administrator-access"></a><span data-ttu-id="42bc8-124">即時管理員存取權</span><span class="sxs-lookup"><span data-stu-id="42bc8-124">Just in time administrator access</span></span>
<span data-ttu-id="42bc8-125">在過去，您可以透過 Azure 傳統入口網站或 Windows PowerShell 將使用者指派給管理員角色。</span><span class="sxs-lookup"><span data-stu-id="42bc8-125">Historically, you could assign a user to an admin role through the Azure classic portal or Windows PowerShell.</span></span> <span data-ttu-id="42bc8-126">因此，該使用者會成為 **永久管理員**，其獲得指派的角色永遠處於作用狀態。</span><span class="sxs-lookup"><span data-stu-id="42bc8-126">As a result, that user becomes a **permanent admin**, always active in the assigned role.</span></span> <span data-ttu-id="42bc8-127">Azure AD Privileged Identity Management 導入了「合格系統管理員」 的概念。</span><span class="sxs-lookup"><span data-stu-id="42bc8-127">Azure AD Privileged Identity Management introduces the concept of an **eligible admin**.</span></span> <span data-ttu-id="42bc8-128">合格系統管理員應該是指偶爾需要特殊存取權限而非每一天都需要此權限的使用者。</span><span class="sxs-lookup"><span data-stu-id="42bc8-128">Eligible admins should be users that need privileged access now and then, but not every day.</span></span> <span data-ttu-id="42bc8-129">在使用者需要存取權之前，角色會處於非作用中狀態，然後使用者須完成啟用程序，才能在一段預定的時間內成為作用中的系統管理員。</span><span class="sxs-lookup"><span data-stu-id="42bc8-129">The role is inactive until the user needs access, then they complete an activation process and become an active admin for a predetermined amount of time.</span></span>

## <a name="enable-privileged-identity-management-for-your-directory"></a><span data-ttu-id="42bc8-130">啟用目錄的 Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="42bc8-130">Enable Privileged Identity Management for your directory</span></span>
<span data-ttu-id="42bc8-131">您可以在 [Azure 入口網站](https://portal.azure.com/)中開始使用 Azure AD Privileged Identity Management。</span><span class="sxs-lookup"><span data-stu-id="42bc8-131">You can start using Azure AD Privileged Identity Management in the [Azure portal](https://portal.azure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="42bc8-132">您必須是具有組織帳戶 (例如 @yourdomain.com) 而非 Microsoft 帳戶 (例如 @outlook.com) 的全域管理員，才能啟用目錄的 Azure AD Privileged Identity Management。</span><span class="sxs-lookup"><span data-stu-id="42bc8-132">You must be a global administrator with an organizational account (for example, @yourdomain.com), not a Microsoft account (for example, @outlook.com), to enable Azure AD Privileged Identity Management for a directory.</span></span>

1. <span data-ttu-id="42bc8-133">以目錄的全域系統管理員身分登入 [Azure 入口網站](https://portal.azure.com/) 。</span><span class="sxs-lookup"><span data-stu-id="42bc8-133">Sign in to the [Azure portal](https://portal.azure.com/) as a global administrator of your directory.</span></span>
2. <span data-ttu-id="42bc8-134">如果貴組織有多個目錄，請選取 Azure 入口網站右上角的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="42bc8-134">If your organization has more than one directory, select your username in the upper right-hand corner of the Azure portal.</span></span> <span data-ttu-id="42bc8-135">選取您將在其中使用 Azure AD Privileged Identity Management 的目錄。</span><span class="sxs-lookup"><span data-stu-id="42bc8-135">Select the directory where you will use Azure AD Privileged Identity Management.</span></span>
3. <span data-ttu-id="42bc8-136">選取 [更多服務] 並使用 [篩選器] 文字方塊來搜尋 [Azure AD Privileged Identity Management]。</span><span class="sxs-lookup"><span data-stu-id="42bc8-136">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="42bc8-137">選取 [釘選到儀表板]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="42bc8-137">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="42bc8-138">Privileged Identity Management 應用程式隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="42bc8-138">The Privileged Identity Management application opens.</span></span>

<span data-ttu-id="42bc8-139">如果您是在目錄中使用 Azure AD Privileged Identity Management 的第一個人，則 [安全性精靈](active-directory-privileged-identity-management-security-wizard.md) 會引導您完成初始指派體驗。</span><span class="sxs-lookup"><span data-stu-id="42bc8-139">If you're the first person to use Azure AD Privileged Identity Management in your directory, then the [security wizard](active-directory-privileged-identity-management-security-wizard.md) walks you through the initial assignment experience.</span></span> <span data-ttu-id="42bc8-140">之後，您就會自動成為目錄的第一個「安全性系統管理員」和「特殊權限角色管理員」。</span><span class="sxs-lookup"><span data-stu-id="42bc8-140">After that you automatically become the first **Security administrator** and **Privileged role administrator** of the directory.</span></span>

<span data-ttu-id="42bc8-141">只有特殊權限角色管理員可以管理其他系統管理員的存取權。</span><span class="sxs-lookup"><span data-stu-id="42bc8-141">Only a privileged role administrator can manage access for other administrators.</span></span> <span data-ttu-id="42bc8-142">您可以 [在 PIM 中為其他使用者提供管理能力](active-directory-privileged-identity-management-how-to-give-access-to-pim.md)。</span><span class="sxs-lookup"><span data-stu-id="42bc8-142">You can [give other users the ability to manage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="privileged-identity-management-admin-dashboard"></a><span data-ttu-id="42bc8-143">Privileged Identity Management 管理員儀表板</span><span class="sxs-lookup"><span data-stu-id="42bc8-143">Privileged Identity Management admin dashboard</span></span>
<span data-ttu-id="42bc8-144">Azure AD Privileged Identity Manager 有一個管理員儀表板可提供重要資訊，例如：</span><span class="sxs-lookup"><span data-stu-id="42bc8-144">Azure AD Privileged Identity Manager provides an admin dashboard that gives you important information such as:</span></span>

* <span data-ttu-id="42bc8-145">指出有提升安全性機會的警示</span><span class="sxs-lookup"><span data-stu-id="42bc8-145">Alerts that point out opportunities to improve security</span></span>
* <span data-ttu-id="42bc8-146">指派給每個特殊權限角色的使用者數目</span><span class="sxs-lookup"><span data-stu-id="42bc8-146">The number of users who are assigned to each privileged role</span></span>  
* <span data-ttu-id="42bc8-147">合格和永久系統管理員的數目</span><span class="sxs-lookup"><span data-stu-id="42bc8-147">The number of eligible and permanent admins</span></span>
* <span data-ttu-id="42bc8-148">您的目錄中特殊權限角色啟用的圖表</span><span class="sxs-lookup"><span data-stu-id="42bc8-148">A graph of privileged role activations in your directory</span></span>

![PIM 儀表板 - 螢幕擷取畫面][2]

## <a name="privileged-role-management"></a><span data-ttu-id="42bc8-150">特殊權限角色管理</span><span class="sxs-lookup"><span data-stu-id="42bc8-150">Privileged role management</span></span>
<span data-ttu-id="42bc8-151">使用 Azure AD Privileged Identity Management，您便可透過新增或移除每個角色的永久或合格系統管理員來管理這些管理員。</span><span class="sxs-lookup"><span data-stu-id="42bc8-151">With Azure AD Privileged Identity Management, you can manage the administrators by adding or removing permanent or eligible administrators to each role.</span></span>

![PIM 新增/移除系統管理員 - 螢幕擷取畫面][3]

## <a name="configure-the-role-activation-settings"></a><span data-ttu-id="42bc8-153">設定角色啟用設定</span><span class="sxs-lookup"><span data-stu-id="42bc8-153">Configure the role activation settings</span></span>
<span data-ttu-id="42bc8-154">您可以使用 [角色設定](active-directory-privileged-identity-management-how-to-change-default-settings.md) 來設定合格角色啟用屬性，包括：</span><span class="sxs-lookup"><span data-stu-id="42bc8-154">Using the [role settings](active-directory-privileged-identity-management-how-to-change-default-settings.md) you can configure the eligible role activation properties including:</span></span>

* <span data-ttu-id="42bc8-155">角色啟用期間的持續時間</span><span class="sxs-lookup"><span data-stu-id="42bc8-155">The duration of the role activation period</span></span>
* <span data-ttu-id="42bc8-156">角色啟用通知</span><span class="sxs-lookup"><span data-stu-id="42bc8-156">The role activation notification</span></span>
* <span data-ttu-id="42bc8-157">使用者在角色啟用程序期間所需提供的資訊</span><span class="sxs-lookup"><span data-stu-id="42bc8-157">The information a user needs to provide during the role activation process</span></span>
* <span data-ttu-id="42bc8-158">服務票證或事件數目</span><span class="sxs-lookup"><span data-stu-id="42bc8-158">Service ticket or incident number</span></span>
* [<span data-ttu-id="42bc8-159">核准工作流程需求 - 預覽</span><span class="sxs-lookup"><span data-stu-id="42bc8-159">Approval workflow requirements - Preview</span></span>](./privileged-identity-management/azure-ad-pim-approval-workflow.md)

![PIM 設定 - 系統管理員啟動 - 螢幕擷取畫面][4]

<span data-ttu-id="42bc8-161">請注意，此影像中已停用 [Multi-Factor Authentication]  的按鈕。</span><span class="sxs-lookup"><span data-stu-id="42bc8-161">Note that in the image, the buttons for **Multi-Factor Authentication** are disabled.</span></span> <span data-ttu-id="42bc8-162">針對某些高特殊權限的角色，我們會要求使用 MFA 來增強防護。</span><span class="sxs-lookup"><span data-stu-id="42bc8-162">For certain, highly privileged roles, we require MFA for heightened protection.</span></span>

## <a name="role-activation"></a><span data-ttu-id="42bc8-163">角色啟用</span><span class="sxs-lookup"><span data-stu-id="42bc8-163">Role activation</span></span>
<span data-ttu-id="42bc8-164">為了 [啟用角色](active-directory-privileged-identity-management-how-to-activate-role.md)，合格系統管理員會為角色要求一個有時效性的「啟用」。</span><span class="sxs-lookup"><span data-stu-id="42bc8-164">To [activate a role](active-directory-privileged-identity-management-how-to-activate-role.md), an eligible admin requests a time-bound "activation" for the role.</span></span> <span data-ttu-id="42bc8-165">使用 Azure AD 特殊權限身分識別管理中的 [ **啟用我的角色** ] 選項，即可要求啟用。</span><span class="sxs-lookup"><span data-stu-id="42bc8-165">The activation can be requested using the **Activate my role** option in Azure AD Privileged Identity Management.</span></span>

<span data-ttu-id="42bc8-166">想要啟用角色的管理員必須在 Azure 入口網站中初始化 Azure AD Privileged Identity Management。</span><span class="sxs-lookup"><span data-stu-id="42bc8-166">An admin who wants to activate a role needs to initialize Azure AD Privileged Identity Management in the Azure portal.</span></span>

<span data-ttu-id="42bc8-167">角色啟用是可自訂的。</span><span class="sxs-lookup"><span data-stu-id="42bc8-167">Role activation is customizable.</span></span> <span data-ttu-id="42bc8-168">在 [PIM] 設定中，您可以決定啟用的長度，以及管理員必須提供才能啟用角色的資訊。</span><span class="sxs-lookup"><span data-stu-id="42bc8-168">In the PIM settings, you can determine the length of the activation and what information the admin needs to provide to activate the role.</span></span>

![PIM 系統管理員要求角色啟用 - 螢幕擷取畫面][5]

## <a name="review-role-activity"></a><span data-ttu-id="42bc8-170">檢閱角色活動</span><span class="sxs-lookup"><span data-stu-id="42bc8-170">Review role activity</span></span>
<span data-ttu-id="42bc8-171">有兩種方式可以追蹤您的員工和系統管理員使用特殊權限角色的情況。</span><span class="sxs-lookup"><span data-stu-id="42bc8-171">There are two ways to track how your employees and admins are using privileged roles.</span></span> <span data-ttu-id="42bc8-172">第一個選項是使用[目錄角色稽核歷程](active-directory-privileged-identity-management-how-to-use-audit-log.md)。</span><span class="sxs-lookup"><span data-stu-id="42bc8-172">The first option is using [Directory Roles audit history](active-directory-privileged-identity-management-how-to-use-audit-log.md).</span></span> <span data-ttu-id="42bc8-173">稽核歷程記錄會追蹤特殊權限角色的指派和角色啟用歷程中的變更。</span><span class="sxs-lookup"><span data-stu-id="42bc8-173">The audit history logs track changes in privileged role assignments and role activation history.</span></span>

![PIM 啟動歷程記錄 - 螢幕擷取畫面][6]

<span data-ttu-id="42bc8-175">第二個選項是設定標準 [存取檢閱](active-directory-privileged-identity-management-how-to-start-security-review.md)。</span><span class="sxs-lookup"><span data-stu-id="42bc8-175">The second option is to set up regular [access reviews](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="42bc8-176">這些存取檢閱可以由指派的檢閱者 (例如團隊經理) 來執行或者員工可以檢閱自己。</span><span class="sxs-lookup"><span data-stu-id="42bc8-176">These access reviews can be performed by and assigned reviewer (like a team manager) or the employees can review themselves.</span></span> <span data-ttu-id="42bc8-177">如此來監視誰仍需要或不再需要存取是最佳的方式。</span><span class="sxs-lookup"><span data-stu-id="42bc8-177">This is the best way to monitor who still requires access, and who no longer does.</span></span>

## <a name="azure-ad-pim-at-subscription-expiration"></a><span data-ttu-id="42bc8-178">訂用帳戶過期時的 Azure AD PIM</span><span class="sxs-lookup"><span data-stu-id="42bc8-178">Azure AD PIM at subscription expiration</span></span>
<span data-ttu-id="42bc8-179">在公開上市之前，Azure AD PIM 處於預覽狀態，而且沒有租用戶的授權檢查可預覽 Azure AD PIM。</span><span class="sxs-lookup"><span data-stu-id="42bc8-179">Prior to reaching general availability Azure AD PIM was in preview and there were no license checks for a tenant to preview Azure AD PIM.</span></span>  <span data-ttu-id="42bc8-180">現在，Azure AD PIM 已公開上市，試用或付費授權必須指派給租用戶的系統管理員，才能繼續使用 PIM。</span><span class="sxs-lookup"><span data-stu-id="42bc8-180">Now that Azure AD PIM has reached general availability, trial or paid licenses must be assigned to the administrators of the tenant to continue using PIM.</span></span>  <span data-ttu-id="42bc8-181">如果您的組織並未購買 Azure AD Premium P2 或您的試用過期，您的租用戶就無法再使用幾乎所有 Azure AD PIM 功能。</span><span class="sxs-lookup"><span data-stu-id="42bc8-181">If your organization does not purchase Azure AD Premium P2 or your trial expires, mostly all of the Azure AD PIM features will no longer be available in your tenant.</span></span>  <span data-ttu-id="42bc8-182">您可以深入了解 [Azure AD PIM 訂用帳戶需求](./privileged-identity-management/subscription-requirements.md)</span><span class="sxs-lookup"><span data-stu-id="42bc8-182">You can read more in the [Azure AD PIM subscription requirements](./privileged-identity-management/subscription-requirements.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="42bc8-183">後續步驟</span><span class="sxs-lookup"><span data-stu-id="42bc8-183">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-configure/PIM_Admin_Overview.png
[3]: ./media/active-directory-privileged-identity-management-configure/PIM_AddRemove.png
[4]: ./media/active-directory-privileged-identity-management-configure/PIM_Settings_w_Approval_Disabled.png
[5]: ./media/active-directory-privileged-identity-management-configure/PIM_RequestActivation.png
[6]: ./media/active-directory-privileged-identity-management-configure/PIM_ActivationHistory.png
