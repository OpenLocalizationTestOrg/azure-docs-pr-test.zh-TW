---
title: "Azure AD Privileged Identity Management aaaConfigure |Microsoft 文件"
description: "主題，說明 Azure AD Privileged Identity Management 為何及如何 toouse PIM tooimprove 您雲端的安全性。"
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
ms.openlocfilehash: dbe49fe4a0f6e5b46ed5a17fc7e8dcdacafe3846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-ad-privileged-identity-management"></a><span data-ttu-id="54ade-103">什麼是 Azure AD Privileged Identity Management？</span><span class="sxs-lookup"><span data-stu-id="54ade-103">What is Azure AD Privileged Identity Management?</span></span>
<span data-ttu-id="54ade-104">您可以利用 Azure Active Directory (AD) Privileged Identity Management 來管理、控制和監視組織內的存取行為。</span><span class="sxs-lookup"><span data-stu-id="54ade-104">With Azure Active Directory (AD) Privileged Identity Management, you can manage, control, and monitor access within your organization.</span></span> <span data-ttu-id="54ade-105">這包括存取 tooresources 在 Azure AD 和 Office 365 或 Microsoft Intune 等其他 Microsoft online services。</span><span class="sxs-lookup"><span data-stu-id="54ade-105">This includes access tooresources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

> [!NOTE]
> <span data-ttu-id="54ade-106">Privileged 的 Identity Management 授權您的系統管理員與 Azure Active Directory Premium P2 hello 版時可用的 tooyour 整個組織。</span><span class="sxs-lookup"><span data-stu-id="54ade-106">Privileged Identity Management is available tooyour entire organization when you license your Administrators with hello Premium P2 edition of Azure Active Directory.</span></span> <span data-ttu-id="54ade-107">如需詳細資訊，請參閱 [Azure Active Directory 版本](active-directory-editions.md)。</span><span class="sxs-lookup"><span data-stu-id="54ade-107">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

<span data-ttu-id="54ade-108">組織想 toominimize hello 許多人都擁有存取 toosecure 資訊或資源，因為，可以減少惡意使用者取得存取 hello 機會。</span><span class="sxs-lookup"><span data-stu-id="54ade-108">Organizations want toominimize hello number of people who have access toosecure information or resources, because that reduces hello chance of a malicious user getting that access.</span></span> <span data-ttu-id="54ade-109">不過，使用者仍然需要 toocarry Azure、 Office 365 或 SaaS 應用程式中的特殊權限作業。</span><span class="sxs-lookup"><span data-stu-id="54ade-109">However, users still need toocarry out privileged operations in Azure, Office 365, or SaaS apps.</span></span> <span data-ttu-id="54ade-110">組織可以在 Azure AD 中授與使用者特殊權限，而不需監視這些使用者使用其系統管理權限來執行什麼作業。</span><span class="sxs-lookup"><span data-stu-id="54ade-110">Organizations give users privileged access in Azure AD without monitoring what those users are doing with their admin privileges.</span></span> <span data-ttu-id="54ade-111">Azure AD Privileged Identity Management 可協助 tooresolve 這項風險。</span><span class="sxs-lookup"><span data-stu-id="54ade-111">Azure AD Privileged Identity Management helps tooresolve this risk.</span></span>  

<span data-ttu-id="54ade-112">Azure AD Privileged Identity Management 可協助您：</span><span class="sxs-lookup"><span data-stu-id="54ade-112">Azure AD Privileged Identity Management helps you:</span></span>  

* <span data-ttu-id="54ade-113">查看哪些使用者是 Azure AD 管理員</span><span class="sxs-lookup"><span data-stu-id="54ade-113">See which users are Azure AD administrators</span></span>
* <span data-ttu-id="54ade-114">視需要啟用，"just-in-time"系統管理存取權 tooMicrosoft 線上服務，如 Office 365 和 Intune</span><span class="sxs-lookup"><span data-stu-id="54ade-114">Enable on-demand, "just in time" administrative access tooMicrosoft Online Services like Office 365 and Intune</span></span>
* <span data-ttu-id="54ade-115">取得有關系統管理員存取記錄與系統管理員指派變更的報告</span><span class="sxs-lookup"><span data-stu-id="54ade-115">Get reports about administrator access history and changes in administrator assignments</span></span>
* <span data-ttu-id="54ade-116">取得警示存取 tooa 特殊權限角色</span><span class="sxs-lookup"><span data-stu-id="54ade-116">Get alerts about access tooa privileged role</span></span>
* <span data-ttu-id="54ade-117">需要核准 tooactivate （預覽）</span><span class="sxs-lookup"><span data-stu-id="54ade-117">Require approval tooactivate (Preview)</span></span>

<span data-ttu-id="54ade-118">Azure AD Privileged Identity Management 可以管理 hello 內建的 Azure AD 組織角色，包括 （但不是限於）：</span><span class="sxs-lookup"><span data-stu-id="54ade-118">Azure AD Privileged Identity Management can manage hello built-in Azure AD organizational roles, including (but not limited to):</span></span>  

* <span data-ttu-id="54ade-119">全域管理員</span><span class="sxs-lookup"><span data-stu-id="54ade-119">Global Administrator</span></span>
* <span data-ttu-id="54ade-120">計費管理員</span><span class="sxs-lookup"><span data-stu-id="54ade-120">Billing Administrator</span></span>
* <span data-ttu-id="54ade-121">服務管理員</span><span class="sxs-lookup"><span data-stu-id="54ade-121">Service Administrator</span></span>  
* <span data-ttu-id="54ade-122">使用者管理員</span><span class="sxs-lookup"><span data-stu-id="54ade-122">User Administrator</span></span>
* <span data-ttu-id="54ade-123">密碼管理員</span><span class="sxs-lookup"><span data-stu-id="54ade-123">Password Administrator</span></span>

## <a name="just-in-time-administrator-access"></a><span data-ttu-id="54ade-124">即時管理員存取權</span><span class="sxs-lookup"><span data-stu-id="54ade-124">Just in time administrator access</span></span>
<span data-ttu-id="54ade-125">在過去，您可能會指派使用者 tooan 系統管理員角色，透過 hello Azure 傳統入口網站或 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="54ade-125">Historically, you could assign a user tooan admin role through hello Azure classic portal or Windows PowerShell.</span></span> <span data-ttu-id="54ade-126">如此一來，該使用者即成為**永久系統管理員**，一律在 hello 指派角色在作用中。</span><span class="sxs-lookup"><span data-stu-id="54ade-126">As a result, that user becomes a **permanent admin**, always active in hello assigned role.</span></span> <span data-ttu-id="54ade-127">Azure AD Privileged Identity Management 引進 hello 概念**合格的系統管理員**。合格系統管理員應該是指偶爾需要特殊存取權限而非每一天都需要此權限的使用者。</span><span class="sxs-lookup"><span data-stu-id="54ade-127">Azure AD Privileged Identity Management introduces hello concept of an **eligible admin**. Eligible admins should be users that need privileged access now and then, but not every day.</span></span> <span data-ttu-id="54ade-128">hello 角色未作用中，直到 hello 使用者需要存取時，，然後完成啟動程序，並成為使用中的系統管理員預先決定的一段時間。</span><span class="sxs-lookup"><span data-stu-id="54ade-128">hello role is inactive until hello user needs access, then they complete an activation process and become an active admin for a predetermined amount of time.</span></span>

## <a name="enable-privileged-identity-management-for-your-directory"></a><span data-ttu-id="54ade-129">啟用目錄的 Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="54ade-129">Enable Privileged Identity Management for your directory</span></span>
<span data-ttu-id="54ade-130">您可以開始使用 Azure AD Privileged Identity Management 中 hello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="54ade-130">You can start using Azure AD Privileged Identity Management in hello [Azure portal](https://portal.azure.com/).</span></span>

> [!NOTE]
> <span data-ttu-id="54ade-131">您必須是全域管理員的組織帳戶 (例如， @yourdomain.com)，不是 Microsoft 帳戶 (例如， @outlook.com)，tooenable 目錄的 Azure AD Privileged Identity Management。</span><span class="sxs-lookup"><span data-stu-id="54ade-131">You must be a global administrator with an organizational account (for example, @yourdomain.com), not a Microsoft account (for example, @outlook.com), tooenable Azure AD Privileged Identity Management for a directory.</span></span>

1. <span data-ttu-id="54ade-132">登入 toohello [Azure 入口網站](https://portal.azure.com/)您目錄的全域管理員身分。</span><span class="sxs-lookup"><span data-stu-id="54ade-132">Sign in toohello [Azure portal](https://portal.azure.com/) as a global administrator of your directory.</span></span>
2. <span data-ttu-id="54ade-133">如果您的組織具有多個目錄，選取您的使用者名稱 hello 右上角的 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="54ade-133">If your organization has more than one directory, select your username in hello upper right-hand corner of hello Azure portal.</span></span> <span data-ttu-id="54ade-134">選取您將在其中使用 Azure AD Privileged Identity Management hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="54ade-134">Select hello directory where you will use Azure AD Privileged Identity Management.</span></span>
3. <span data-ttu-id="54ade-135">選取**更多服務**並用的 hello 篩選文字方塊中 toosearch **Azure AD Privileged Identity Management**。</span><span class="sxs-lookup"><span data-stu-id="54ade-135">Select **More services** and use hello Filter textbox toosearch for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="54ade-136">請檢查**Pin toodashboard** ，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="54ade-136">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="54ade-137">hello Privileged Identity Management 的應用程式會開啟。</span><span class="sxs-lookup"><span data-stu-id="54ade-137">hello Privileged Identity Management application opens.</span></span>

<span data-ttu-id="54ade-138">如果您正在 hello 第一個人 toouse Azure AD Privileged Identity Management 目錄中，然後 hello[安全性精靈](active-directory-privileged-identity-management-security-wizard.md)會引導您完成 hello 初始設定經驗。</span><span class="sxs-lookup"><span data-stu-id="54ade-138">If you're hello first person toouse Azure AD Privileged Identity Management in your directory, then hello [security wizard](active-directory-privileged-identity-management-security-wizard.md) walks you through hello initial assignment experience.</span></span> <span data-ttu-id="54ade-139">之後，您會自動變成 hello 先**安全性系統管理員**和**特殊權限的角色管理員**的 hello 目錄。</span><span class="sxs-lookup"><span data-stu-id="54ade-139">After that you automatically become hello first **Security administrator** and **Privileged role administrator** of hello directory.</span></span>

<span data-ttu-id="54ade-140">只有特殊權限角色管理員可以管理其他系統管理員的存取權。</span><span class="sxs-lookup"><span data-stu-id="54ade-140">Only a privileged role administrator can manage access for other administrators.</span></span> <span data-ttu-id="54ade-141">您可以[PIM 中授與其他使用者 hello 能力 toomanage](active-directory-privileged-identity-management-how-to-give-access-to-pim.md)。</span><span class="sxs-lookup"><span data-stu-id="54ade-141">You can [give other users hello ability toomanage in PIM](active-directory-privileged-identity-management-how-to-give-access-to-pim.md).</span></span>

## <a name="privileged-identity-management-admin-dashboard"></a><span data-ttu-id="54ade-142">Privileged Identity Management 管理員儀表板</span><span class="sxs-lookup"><span data-stu-id="54ade-142">Privileged Identity Management admin dashboard</span></span>
<span data-ttu-id="54ade-143">Azure AD Privileged Identity Manager 有一個管理員儀表板可提供重要資訊，例如：</span><span class="sxs-lookup"><span data-stu-id="54ade-143">Azure AD Privileged Identity Manager provides an admin dashboard that gives you important information such as:</span></span>

* <span data-ttu-id="54ade-144">指出機會 tooimprove 安全性警示</span><span class="sxs-lookup"><span data-stu-id="54ade-144">Alerts that point out opportunities tooimprove security</span></span>
* <span data-ttu-id="54ade-145">hello tooeach 特殊權限的角色所指派的使用者的數目</span><span class="sxs-lookup"><span data-stu-id="54ade-145">hello number of users who are assigned tooeach privileged role</span></span>  
* <span data-ttu-id="54ade-146">hello 數字的合格和永久系統管理員</span><span class="sxs-lookup"><span data-stu-id="54ade-146">hello number of eligible and permanent admins</span></span>
* <span data-ttu-id="54ade-147">您的目錄中特殊權限角色啟用的圖表</span><span class="sxs-lookup"><span data-stu-id="54ade-147">A graph of privileged role activations in your directory</span></span>

![PIM 儀表板 - 螢幕擷取畫面][2]

## <a name="privileged-role-management"></a><span data-ttu-id="54ade-149">特殊權限角色管理</span><span class="sxs-lookup"><span data-stu-id="54ade-149">Privileged role management</span></span>
<span data-ttu-id="54ade-150">使用 Azure AD Privileged Identity Management，您可以透過加入或移除永久或符合資格的系統管理員 tooeach 角色管理 hello 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="54ade-150">With Azure AD Privileged Identity Management, you can manage hello administrators by adding or removing permanent or eligible administrators tooeach role.</span></span>

![PIM 新增/移除系統管理員 - 螢幕擷取畫面][3]

## <a name="configure-hello-role-activation-settings"></a><span data-ttu-id="54ade-152">設定 hello 角色啟動設定</span><span class="sxs-lookup"><span data-stu-id="54ade-152">Configure hello role activation settings</span></span>
<span data-ttu-id="54ade-153">使用 hello[角色設定](active-directory-privileged-identity-management-how-to-change-default-settings.md)您可以設定 hello 符合資格的角色啟動屬性，包括：</span><span class="sxs-lookup"><span data-stu-id="54ade-153">Using hello [role settings](active-directory-privileged-identity-management-how-to-change-default-settings.md) you can configure hello eligible role activation properties including:</span></span>

* <span data-ttu-id="54ade-154">hello 的 hello 角色啟動期間的持續時間</span><span class="sxs-lookup"><span data-stu-id="54ade-154">hello duration of hello role activation period</span></span>
* <span data-ttu-id="54ade-155">hello 角色啟用通知</span><span class="sxs-lookup"><span data-stu-id="54ade-155">hello role activation notification</span></span>
* <span data-ttu-id="54ade-156">hello 角色啟動程序期間需要 tooprovide hello 資訊的使用者</span><span class="sxs-lookup"><span data-stu-id="54ade-156">hello information a user needs tooprovide during hello role activation process</span></span>
* <span data-ttu-id="54ade-157">服務票證或事件數目</span><span class="sxs-lookup"><span data-stu-id="54ade-157">Service ticket or incident number</span></span>
* [<span data-ttu-id="54ade-158">核准工作流程需求 - 預覽</span><span class="sxs-lookup"><span data-stu-id="54ade-158">Approval workflow requirements - Preview</span></span>](./privileged-identity-management/azure-ad-pim-approval-workflow.md)

![PIM 設定 - 系統管理員啟動 - 螢幕擷取畫面][4]

<span data-ttu-id="54ade-160">請注意，在 hello 映像，hello 的按鈕**Multi-factor Authentication**會停用。</span><span class="sxs-lookup"><span data-stu-id="54ade-160">Note that in hello image, hello buttons for **Multi-Factor Authentication** are disabled.</span></span> <span data-ttu-id="54ade-161">針對某些高特殊權限的角色，我們會要求使用 MFA 來增強防護。</span><span class="sxs-lookup"><span data-stu-id="54ade-161">For certain, highly privileged roles, we require MFA for heightened protection.</span></span>

## <a name="role-activation"></a><span data-ttu-id="54ade-162">角色啟用</span><span class="sxs-lookup"><span data-stu-id="54ade-162">Role activation</span></span>
<span data-ttu-id="54ade-163">太[啟用角色](active-directory-privileged-identity-management-how-to-activate-role.md)，合格的系統管理員要求時間繫結至的 「 啟用 」 hello 角色。</span><span class="sxs-lookup"><span data-stu-id="54ade-163">too[activate a role](active-directory-privileged-identity-management-how-to-activate-role.md), an eligible admin requests a time-bound "activation" for hello role.</span></span> <span data-ttu-id="54ade-164">可以使用 hello 要求 hello 啟用**啟用 我的角色**Azure AD Privileged Identity Management 中的選項。</span><span class="sxs-lookup"><span data-stu-id="54ade-164">hello activation can be requested using hello **Activate my role** option in Azure AD Privileged Identity Management.</span></span>

<span data-ttu-id="54ade-165">系統管理員，並想要 tooactivate 角色都需要 tooinitialize hello Azure 入口網站中的 Azure AD Privileged Identity Management。</span><span class="sxs-lookup"><span data-stu-id="54ade-165">An admin who wants tooactivate a role needs tooinitialize Azure AD Privileged Identity Management in hello Azure portal.</span></span>

<span data-ttu-id="54ade-166">角色啟用是可自訂的。</span><span class="sxs-lookup"><span data-stu-id="54ade-166">Role activation is customizable.</span></span> <span data-ttu-id="54ade-167">在 hello PIM 設定中，您可以判斷 hello 啟用和哪些資訊 hello 系統管理員必須 tooprovide tooactivate hello 角色 hello 長度。</span><span class="sxs-lookup"><span data-stu-id="54ade-167">In hello PIM settings, you can determine hello length of hello activation and what information hello admin needs tooprovide tooactivate hello role.</span></span>

![PIM 系統管理員要求角色啟用 - 螢幕擷取畫面][5]

## <a name="review-role-activity"></a><span data-ttu-id="54ade-169">檢閱角色活動</span><span class="sxs-lookup"><span data-stu-id="54ade-169">Review role activity</span></span>
<span data-ttu-id="54ade-170">有兩種方式 tootrack 如何使用您的員工和系統管理員特殊權限的角色。</span><span class="sxs-lookup"><span data-stu-id="54ade-170">There are two ways tootrack how your employees and admins are using privileged roles.</span></span> <span data-ttu-id="54ade-171">hello 第一個選項使用[目錄角色稽核歷程](active-directory-privileged-identity-management-how-to-use-audit-log.md)。</span><span class="sxs-lookup"><span data-stu-id="54ade-171">hello first option is using [Directory Roles audit history](active-directory-privileged-identity-management-how-to-use-audit-log.md).</span></span> <span data-ttu-id="54ade-172">hello 稽核歷程記錄中的特殊權限的角色指派及角色啟動歷程記錄的追蹤變更。</span><span class="sxs-lookup"><span data-stu-id="54ade-172">hello audit history logs track changes in privileged role assignments and role activation history.</span></span>

![PIM 啟動歷程記錄 - 螢幕擷取畫面][6]

<span data-ttu-id="54ade-174">hello 第二個選項是一般向上 tooset[存取檢閱](active-directory-privileged-identity-management-how-to-start-security-review.md)。</span><span class="sxs-lookup"><span data-stu-id="54ade-174">hello second option is tooset up regular [access reviews](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="54ade-175">這些存取檢視可以執行，而指派給檢閱者 （例如小組管理員） 或 hello 員工可以檢閱其本身。</span><span class="sxs-lookup"><span data-stu-id="54ade-175">These access reviews can be performed by and assigned reviewer (like a team manager) or hello employees can review themselves.</span></span> <span data-ttu-id="54ade-176">這是 hello 最佳方式 toomonitor 人員仍需要存取，以及人員不會再。</span><span class="sxs-lookup"><span data-stu-id="54ade-176">This is hello best way toomonitor who still requires access, and who no longer does.</span></span>

## <a name="azure-ad-pim-at-subscription-expiration"></a><span data-ttu-id="54ade-177">訂用帳戶過期時的 Azure AD PIM</span><span class="sxs-lookup"><span data-stu-id="54ade-177">Azure AD PIM at subscription expiration</span></span>
<span data-ttu-id="54ade-178">檢查租用戶 toopreview Azure AD PIM 先前 tooreaching 一般可用性 Azure AD PIM 處於預覽，且沒有任何授權。</span><span class="sxs-lookup"><span data-stu-id="54ade-178">Prior tooreaching general availability Azure AD PIM was in preview and there were no license checks for a tenant toopreview Azure AD PIM.</span></span>  <span data-ttu-id="54ade-179">現在，Azure AD PIM 已達到公開上市，試用或付費的授權，必須指派 toohello hello 租用戶 toocontinue 使用 PIM 系統管理員。</span><span class="sxs-lookup"><span data-stu-id="54ade-179">Now that Azure AD PIM has reached general availability, trial or paid licenses must be assigned toohello administrators of hello tenant toocontinue using PIM.</span></span>  <span data-ttu-id="54ade-180">如果您的組織不會購買 Azure AD Premium P2，或您的試用版到期，大部分的所有 hello Azure AD PIM 功能將不再提供您的租用戶。</span><span class="sxs-lookup"><span data-stu-id="54ade-180">If your organization does not purchase Azure AD Premium P2 or your trial expires, mostly all of hello Azure AD PIM features will no longer be available in your tenant.</span></span>  <span data-ttu-id="54ade-181">閱讀更多在 hello [Azure AD PIM 訂用帳戶需求](./privileged-identity-management/subscription-requirements.md)</span><span class="sxs-lookup"><span data-stu-id="54ade-181">You can read more in hello [Azure AD PIM subscription requirements](./privileged-identity-management/subscription-requirements.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="54ade-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="54ade-182">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
[2]: ./media/active-directory-privileged-identity-management-configure/PIM_Admin_Overview.png
[3]: ./media/active-directory-privileged-identity-management-configure/PIM_AddRemove.png
[4]: ./media/active-directory-privileged-identity-management-configure/PIM_Settings_w_Approval_Disabled.png
[5]: ./media/active-directory-privileged-identity-management-configure/PIM_RequestActivation.png
[6]: ./media/active-directory-privileged-identity-management-configure/PIM_ActivationHistory.png
