---
title: "Azure AD Connect：針對傳遞驗證進行疑難排解 | Microsoft Docs"
description: "本文說明如何 tootroubleshoot Azure Active Directory (Azure AD) 的傳遞驗證。"
services: active-directory
keywords: "針對 Azure AD Connect 傳遞驗證進行疑難排解, 安裝 Active Directory, Azure AD, SSO, 單一登入的必要元件"
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 87130952f660762f91b0a34b05287603b565639f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-active-directory-pass-through-authentication"></a><span data-ttu-id="1403f-104">針對 Azure Active Directory 傳遞驗證進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="1403f-104">Troubleshoot Azure Active Directory Pass-through Authentication</span></span>

<span data-ttu-id="1403f-105">這篇文章可協助您尋找有關 Azure AD 傳遞驗證常見問題的疑難排解資訊。</span><span class="sxs-lookup"><span data-stu-id="1403f-105">This article helps you find troubleshooting information about common issues regarding Azure AD Pass-through Authentication.</span></span>

>[!IMPORTANT]
><span data-ttu-id="1403f-106">如果您所面對的使用者登入使用傳遞驗證問題，不會停用 hello 功能，或解除安裝傳遞驗證代理程式，而不需僅限雲端的全域管理員帳戶 toofall 回到上。</span><span class="sxs-lookup"><span data-stu-id="1403f-106">If you are facing user sign-in issues with Pass-through Authentication, don't disable hello feature or uninstall Pass-through Authentication Agents without having a cloud-only Global Administrator account toofall back on.</span></span> <span data-ttu-id="1403f-107">了解如何[新增僅限雲端管理員帳戶 (英文)](../active-directory-users-create-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="1403f-107">Learn about [adding a cloud-only Global Administrator account](../active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="1403f-108">這是確保您不會被租用戶封鎖的關鍵步驟。</span><span class="sxs-lookup"><span data-stu-id="1403f-108">Doing this step is critical and ensures that you don't get locked out of your tenant.</span></span>

## <a name="general-issues"></a><span data-ttu-id="1403f-109">一般問題</span><span class="sxs-lookup"><span data-stu-id="1403f-109">General issues</span></span>

### <a name="check-status-of-hello-feature-and-authentication-agents"></a><span data-ttu-id="1403f-110">檢查 hello 功能與驗證代理程式狀態</span><span class="sxs-lookup"><span data-stu-id="1403f-110">Check status of hello feature and Authentication Agents</span></span>

<span data-ttu-id="1403f-111">確定該 hello 傳遞驗證功能仍然**啟用**驗證代理程式的租用戶和 hello 狀態顯示**Active**，而非**非作用中**。</span><span class="sxs-lookup"><span data-stu-id="1403f-111">Ensure that hello Pass-through Authentication feature is still **Enabled** on your tenant and hello status of Authentication Agents shows **Active**, and not **Inactive**.</span></span> <span data-ttu-id="1403f-112">您可以查看狀態移 toohello **Azure AD Connect**刀鋒視窗上 hello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="1403f-112">You can check status by going toohello **Azure AD Connect** blade on hello [Azure Active Directory admin center](https://aad.portal.azure.com/).</span></span>

![Azure Active Directory 管理中心 - Azure AD Connect 刀鋒視窗](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Azure Active Directory 管理中心 - 傳遞驗證刀鋒視窗](./media/active-directory-aadconnect-pass-through-authentication/pta11.png)

### <a name="user-facing-sign-in-error-messages"></a><span data-ttu-id="1403f-115">使用者看到的登入錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="1403f-115">User-facing sign-in error messages</span></span>

<span data-ttu-id="1403f-116">如果無法使用傳遞驗證 toosign hello 使用者，他們可能會看到 hello 下列使用者面向錯誤 hello Azure AD 登入畫面上的其中一個：</span><span class="sxs-lookup"><span data-stu-id="1403f-116">If hello user is unable toosign into using Pass-through Authentication, they may see one of hello following user-facing errors on hello Azure AD sign-in screen:</span></span> 

|<span data-ttu-id="1403f-117">錯誤</span><span class="sxs-lookup"><span data-stu-id="1403f-117">Error</span></span>|<span data-ttu-id="1403f-118">說明</span><span class="sxs-lookup"><span data-stu-id="1403f-118">Description</span></span>|<span data-ttu-id="1403f-119">解決方案</span><span class="sxs-lookup"><span data-stu-id="1403f-119">Resolution</span></span>
| --- | --- | ---
|<span data-ttu-id="1403f-120">AADSTS80001</span><span class="sxs-lookup"><span data-stu-id="1403f-120">AADSTS80001</span></span>|<span data-ttu-id="1403f-121">無法 tooconnect tooActive 目錄</span><span class="sxs-lookup"><span data-stu-id="1403f-121">Unable tooconnect tooActive Directory</span></span>|<span data-ttu-id="1403f-122">請確認代理程式伺服器 hello 相同 AD 樹系的成員以其密碼需要驗證的 toobe hello 使用者都能 tooconnect tooActive 目錄。</span><span class="sxs-lookup"><span data-stu-id="1403f-122">Ensure that agent servers are members of hello same AD forest as hello users whose passwords need toobe validated and they are able tooconnect tooActive Directory.</span></span>  
|<span data-ttu-id="1403f-123">AADSTS8002</span><span class="sxs-lookup"><span data-stu-id="1403f-123">AADSTS8002</span></span>|<span data-ttu-id="1403f-124">發生連接 tooActive 目錄逾時。</span><span class="sxs-lookup"><span data-stu-id="1403f-124">A timeout occurred connecting tooActive Directory</span></span>|<span data-ttu-id="1403f-125">請檢查 Active Directory 可用，而且從 hello 代理程式回應 toorequests tooensure。</span><span class="sxs-lookup"><span data-stu-id="1403f-125">Check tooensure that Active Directory is available and is responding toorequests from hello agents.</span></span>
|<span data-ttu-id="1403f-126">AADSTS80004</span><span class="sxs-lookup"><span data-stu-id="1403f-126">AADSTS80004</span></span>|<span data-ttu-id="1403f-127">hello 傳遞 toohello 代理程式的使用者名稱無效。</span><span class="sxs-lookup"><span data-stu-id="1403f-127">hello username passed toohello agent was not valid</span></span>|<span data-ttu-id="1403f-128">請確定 hello 使用者嘗試 toosign 入 hello 正確的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="1403f-128">Ensure hello user is attempting toosign in with hello right username.</span></span>
|<span data-ttu-id="1403f-129">AADSTS80005</span><span class="sxs-lookup"><span data-stu-id="1403f-129">AADSTS80005</span></span>|<span data-ttu-id="1403f-130">驗證發生無法預期的 WebException</span><span class="sxs-lookup"><span data-stu-id="1403f-130">Validation encountered unpredictable WebException</span></span>|<span data-ttu-id="1403f-131">暫時性錯誤。</span><span class="sxs-lookup"><span data-stu-id="1403f-131">A transient error.</span></span> <span data-ttu-id="1403f-132">重試 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="1403f-132">Retry hello request.</span></span> <span data-ttu-id="1403f-133">如果持續 toofail，請連絡 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="1403f-133">If it continues toofail, contact Microsoft support.</span></span>
|<span data-ttu-id="1403f-134">AADSTS80007</span><span class="sxs-lookup"><span data-stu-id="1403f-134">AADSTS80007</span></span>|<span data-ttu-id="1403f-135">和 Active Directory 通訊時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="1403f-135">An error occurred communicating with Active Directory</span></span>|<span data-ttu-id="1403f-136">請檢查 hello 代理程式記錄檔，如需詳細資訊，並確認 Active Directory 皆如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="1403f-136">Check hello agent logs for more information and verify that Active Directory is operating as expected.</span></span>

### <a name="sign-in-failure-reasons-on-hello-azure-active-directory-admin-center"></a><span data-ttu-id="1403f-137">登入失敗的原因，在 hello Azure Active Directory 系統管理中心</span><span class="sxs-lookup"><span data-stu-id="1403f-137">Sign-in failure reasons on hello Azure Active Directory admin center</span></span>

<span data-ttu-id="1403f-138">啟動使用者登入問題疑難排解藉由查看 hello[登入活動報表](../active-directory-reporting-activity-sign-ins.md)上 hello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="1403f-138">Start troubleshooting user sign-in issues by looking at hello [sign-in activity report](../active-directory-reporting-activity-sign-ins.md) on hello [Azure Active Directory admin center](https://aad.portal.azure.com/).</span></span>

![Azure Active Directory 管理中心 - 登入報告](./media/active-directory-aadconnect-pass-through-authentication/pta4.png)

<span data-ttu-id="1403f-140">瀏覽過**Azure Active Directory** -> **登入**上 hello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com/)，按一下 特定使用者的登入活動。</span><span class="sxs-lookup"><span data-stu-id="1403f-140">Navigate too**Azure Active Directory** -> **Sign-ins** on hello [Azure Active Directory admin center](https://aad.portal.azure.com/) and click a specific user's sign-in activity.</span></span> <span data-ttu-id="1403f-141">尋找 hello**登入錯誤碼**欄位。</span><span class="sxs-lookup"><span data-stu-id="1403f-141">Look for hello **SIGN-IN ERROR CODE** field.</span></span> <span data-ttu-id="1403f-142">對應欄位 tooa 失敗的原因和解決使用下表中的 hello 的 hello 的值：</span><span class="sxs-lookup"><span data-stu-id="1403f-142">Map hello value of that field tooa failure reason and resolution using hello following table:</span></span>

|<span data-ttu-id="1403f-143">登入錯誤碼</span><span class="sxs-lookup"><span data-stu-id="1403f-143">Sign-in error code</span></span>|<span data-ttu-id="1403f-144">登入失敗原因</span><span class="sxs-lookup"><span data-stu-id="1403f-144">Sign-in failure reason</span></span>|<span data-ttu-id="1403f-145">解決方案</span><span class="sxs-lookup"><span data-stu-id="1403f-145">Resolution</span></span>
| --- | --- | ---
| <span data-ttu-id="1403f-146">50144</span><span class="sxs-lookup"><span data-stu-id="1403f-146">50144</span></span> | <span data-ttu-id="1403f-147">使用者的 Active Directory 密碼已到期。</span><span class="sxs-lookup"><span data-stu-id="1403f-147">User's Active Directory password has expired.</span></span> | <span data-ttu-id="1403f-148">重設您的內部部署 Active Directory 中的 hello 使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="1403f-148">Reset hello user's password in your on-premises Active Directory.</span></span>
| <span data-ttu-id="1403f-149">80001</span><span class="sxs-lookup"><span data-stu-id="1403f-149">80001</span></span> | <span data-ttu-id="1403f-150">沒有可用的驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="1403f-150">No Authentication Agent available.</span></span> | <span data-ttu-id="1403f-151">安裝並註冊驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="1403f-151">Install and register an Authentication Agent.</span></span>
| <span data-ttu-id="1403f-152">80002</span><span class="sxs-lookup"><span data-stu-id="1403f-152">80002</span></span> | <span data-ttu-id="1403f-153">驗證代理程式的密碼驗證要求已逾時。</span><span class="sxs-lookup"><span data-stu-id="1403f-153">Authentication Agent's password validation request timed out.</span></span> | <span data-ttu-id="1403f-154">檢查是否可以從 hello 驗證代理程式連線到您的 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="1403f-154">Check if your Active Directory is reachable from hello Authentication Agent.</span></span>
| <span data-ttu-id="1403f-155">80003</span><span class="sxs-lookup"><span data-stu-id="1403f-155">80003</span></span> | <span data-ttu-id="1403f-156">驗證代理程式收到無效的回應。</span><span class="sxs-lookup"><span data-stu-id="1403f-156">Invalid response received by Authentication Agent.</span></span> | <span data-ttu-id="1403f-157">如果 hello 問題一致地重現跨多個使用者，請檢查您的 Active Directory 設定。</span><span class="sxs-lookup"><span data-stu-id="1403f-157">If hello problem is consistently reproducible across multiple users, check your Active Directory configuration.</span></span>
| <span data-ttu-id="1403f-158">80004</span><span class="sxs-lookup"><span data-stu-id="1403f-158">80004</span></span> | <span data-ttu-id="1403f-159">登入要求中使用的使用者主體名稱 (UPN) 不正確。</span><span class="sxs-lookup"><span data-stu-id="1403f-159">Incorrect User Principal Name (UPN) used in sign-in request.</span></span> | <span data-ttu-id="1403f-160">要求 hello 使用者 toosign 入 hello 正確的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="1403f-160">Ask hello user toosign in with hello correct username.</span></span>
| <span data-ttu-id="1403f-161">80005</span><span class="sxs-lookup"><span data-stu-id="1403f-161">80005</span></span> | <span data-ttu-id="1403f-162">驗證代理程式：發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="1403f-162">Authentication Agent: Error occurred.</span></span> | <span data-ttu-id="1403f-163">暫時性錯誤。</span><span class="sxs-lookup"><span data-stu-id="1403f-163">Transient error.</span></span> <span data-ttu-id="1403f-164">請稍後再試。</span><span class="sxs-lookup"><span data-stu-id="1403f-164">Try again later.</span></span>
| <span data-ttu-id="1403f-165">80007</span><span class="sxs-lookup"><span data-stu-id="1403f-165">80007</span></span> | <span data-ttu-id="1403f-166">驗證代理程式無法 tooconnect tooActive 目錄。</span><span class="sxs-lookup"><span data-stu-id="1403f-166">Authentication Agent unable tooconnect tooActive Directory.</span></span> | <span data-ttu-id="1403f-167">檢查是否可以從 hello 驗證代理程式連線到您的 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="1403f-167">Check if your Active Directory is reachable from hello Authentication Agent.</span></span>
| <span data-ttu-id="1403f-168">80010</span><span class="sxs-lookup"><span data-stu-id="1403f-168">80010</span></span> | <span data-ttu-id="1403f-169">驗證代理程式無法 toodecrypt 密碼。</span><span class="sxs-lookup"><span data-stu-id="1403f-169">Authentication Agent unable toodecrypt password.</span></span> | <span data-ttu-id="1403f-170">如果 hello 問題是一致地重現問題，請安裝並註冊新的驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="1403f-170">If hello problem is consistently reproducible, install and register a new Authentication Agent.</span></span> <span data-ttu-id="1403f-171">然後解除安裝目前的 hello。</span><span class="sxs-lookup"><span data-stu-id="1403f-171">And uninstall hello current one.</span></span> 
| <span data-ttu-id="1403f-172">80011</span><span class="sxs-lookup"><span data-stu-id="1403f-172">80011</span></span> | <span data-ttu-id="1403f-173">驗證代理程式無法 tooretrieve 解密金鑰。</span><span class="sxs-lookup"><span data-stu-id="1403f-173">Authentication Agent unable tooretrieve decryption key.</span></span> | <span data-ttu-id="1403f-174">如果 hello 問題是一致地重現問題，請安裝並註冊新的驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="1403f-174">If hello problem is consistently reproducible, install and register a new Authentication Agent.</span></span> <span data-ttu-id="1403f-175">然後解除安裝目前的 hello。</span><span class="sxs-lookup"><span data-stu-id="1403f-175">And uninstall hello current one.</span></span>

## <a name="authentication-agent-installation-issues"></a><span data-ttu-id="1403f-176">驗證代理程式安裝問題</span><span class="sxs-lookup"><span data-stu-id="1403f-176">Authentication Agent installation issues</span></span>

### <a name="an-unexpected-error-occurred"></a><span data-ttu-id="1403f-177">發生意外的錯誤</span><span class="sxs-lookup"><span data-stu-id="1403f-177">An unexpected error occurred</span></span>

<span data-ttu-id="1403f-178">[收集代理程式記錄檔](#collecting-pass-through-authentication-agent-logs)從 hello 伺服器以及與您的問題，請連絡 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="1403f-178">[Collect agent logs](#collecting-pass-through-authentication-agent-logs) from hello server and contact Microsoft Support with your issue.</span></span>

## <a name="authentication-agent-registration-issues"></a><span data-ttu-id="1403f-179">驗證代理程式註冊問題</span><span class="sxs-lookup"><span data-stu-id="1403f-179">Authentication Agent registration issues</span></span>

### <a name="registration-of-hello-authentication-agent-failed-due-tooblocked-ports"></a><span data-ttu-id="1403f-180">Hello 驗證代理程式註冊失敗，因為 tooblocked 連接埠</span><span class="sxs-lookup"><span data-stu-id="1403f-180">Registration of hello Authentication Agent failed due tooblocked ports</span></span>

<span data-ttu-id="1403f-181">請驗證代理程式已安裝哪些 hello 該 hello 伺服器可與我們的服務 Url 和連接埠的列通訊[這裡](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="1403f-181">Ensure that hello server on which hello Authentication Agent has been installed can communicate with our service URLs and ports listed [here](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).</span></span>

### <a name="registration-of-hello-authentication-agent-failed-due-tootoken-or-account-authorization-errors"></a><span data-ttu-id="1403f-182">Hello 驗證代理程式註冊失敗，因為 tootoken 或帳戶授權錯誤</span><span class="sxs-lookup"><span data-stu-id="1403f-182">Registration of hello Authentication Agent failed due tootoken or account authorization errors</span></span>

<span data-ttu-id="1403f-183">請確定您在所有 Azure AD Connect 或獨立驗證代理程式安裝和註冊作業中，使用僅限雲端的全域管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="1403f-183">Ensure that you use a cloud-only Global Administrator account for all Azure AD Connect or standalone Authentication Agent installation and registration operations.</span></span> <span data-ttu-id="1403f-184">沒有啟用 MFA 的全域管理員帳戶; 的已知的問題因應措施關閉暫時 MFA （只有 toocomplete hello 作業）。</span><span class="sxs-lookup"><span data-stu-id="1403f-184">There is a known issue with MFA-enabled Global Administrator accounts; turn off MFA temporarily (only toocomplete hello operations) as a workaround.</span></span>

### <a name="an-unexpected-error-occurred"></a><span data-ttu-id="1403f-185">發生意外的錯誤</span><span class="sxs-lookup"><span data-stu-id="1403f-185">An unexpected error occurred</span></span>

<span data-ttu-id="1403f-186">[收集代理程式記錄檔](#collecting-pass-through-authentication-agent-logs)從 hello 伺服器以及與您的問題，請連絡 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="1403f-186">[Collect agent logs](#collecting-pass-through-authentication-agent-logs) from hello server and contact Microsoft Support with your issue.</span></span>

## <a name="authentication-agent-uninstallation-issues"></a><span data-ttu-id="1403f-187">驗證代理程式解除安裝問題</span><span class="sxs-lookup"><span data-stu-id="1403f-187">Authentication Agent uninstallation issues</span></span>

### <a name="warning-message-when-uninstalling-azure-ad-connect"></a><span data-ttu-id="1403f-188">解除安裝 Azure AD Connect 時出現的警告訊息</span><span class="sxs-lookup"><span data-stu-id="1403f-188">Warning message when uninstalling Azure AD Connect</span></span>

<span data-ttu-id="1403f-189">如果您有在租用戶啟用傳遞驗證，而且您嘗試 toouninstall Azure AD Connect，它就會顯示您 hello 下列警告訊息: 「 使用者並不會無法 toosign 中 tooAzure AD 除非有其他的傳遞驗證代理程式其他伺服器上安裝。 」</span><span class="sxs-lookup"><span data-stu-id="1403f-189">If you have Pass-through Authentication enabled on your tenant and you try toouninstall Azure AD Connect, it shows you hello following warning message: "Users will not be able toosign-in tooAzure AD unless you have other Pass-through Authentication agents installed on other servers."</span></span>

<span data-ttu-id="1403f-190">請確定您的設定不[高可用](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability)才能解除安裝 Azure AD Connect tooavoid 中斷使用者登入。</span><span class="sxs-lookup"><span data-stu-id="1403f-190">Ensure that your setup is [high available](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) before you uninstall Azure AD Connect tooavoid breaking user sign-in.</span></span>

## <a name="issues-with-enabling-hello-feature"></a><span data-ttu-id="1403f-191">啟用 「 hello 」 功能的問題</span><span class="sxs-lookup"><span data-stu-id="1403f-191">Issues with enabling hello feature</span></span>

### <a name="enabling-hello-feature-failed-because-there-were-no-authentication-agents-available"></a><span data-ttu-id="1403f-192">啟用 「 hello 」 功能失敗，因為沒有任何驗證代理程式</span><span class="sxs-lookup"><span data-stu-id="1403f-192">Enabling hello feature failed because there were no Authentication Agents available</span></span>

<span data-ttu-id="1403f-193">您需要 toohave 至少一個作用中驗證代理程式 」 tooenable 傳遞驗證您的租用戶上。</span><span class="sxs-lookup"><span data-stu-id="1403f-193">You need toohave at least one active Authentication Agent tooenable Pass-through Authentication on your tenant.</span></span> <span data-ttu-id="1403f-194">您可以安裝 Azure AD Connect 或獨立的驗證代理程式，來安裝驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="1403f-194">You can install an Authentication Agent by either installing Azure AD Connect or a standalone Authentication Agent.</span></span>

### <a name="enabling-hello-feature-failed-due-tooblocked-ports"></a><span data-ttu-id="1403f-195">啟用 「 hello 」 功能失敗，因為 tooblocked 連接埠</span><span class="sxs-lookup"><span data-stu-id="1403f-195">Enabling hello feature failed due tooblocked ports</span></span>

<span data-ttu-id="1403f-196">確認已安裝的 Azure AD Connect 該 hello 伺服器能與我們的服務 Url 和連接埠的列通訊[這裡](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="1403f-196">Ensure that hello server on which Azure AD Connect is installed can communicate with our service URLs and ports listed [here](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).</span></span>

### <a name="enabling-hello-feature-failed-due-tootoken-or-account-authorization-errors"></a><span data-ttu-id="1403f-197">啟用 「 hello 」 功能失敗，因為 tootoken 或帳戶授權錯誤</span><span class="sxs-lookup"><span data-stu-id="1403f-197">Enabling hello feature failed due tootoken or account authorization errors</span></span>

<span data-ttu-id="1403f-198">請啟用 「 hello 」 功能時，使用僅限雲端的全域管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="1403f-198">Ensure that you use a cloud-only Global Administrator account when enabling hello feature.</span></span> <span data-ttu-id="1403f-199">使用 multi-factor authentication (MFA) 的已知問題-啟用全域系統管理員帳戶。因應措施關閉暫時 MFA （只有 toocomplete hello 作業）。</span><span class="sxs-lookup"><span data-stu-id="1403f-199">There is a known issue with multi-factor authentication (MFA)-enabled Global Administrator accounts; turn off MFA temporarily (only toocomplete hello operation) as a workaround.</span></span>

## <a name="exchange-activesync-configuration-issues"></a><span data-ttu-id="1403f-200">Exchange ActiveSync 設定問題</span><span class="sxs-lookup"><span data-stu-id="1403f-200">Exchange ActiveSync configuration issues</span></span>

<span data-ttu-id="1403f-201">當您設定 Exchange ActiveSync 支援通過驗證時，這些是 hello 常見的問題。</span><span class="sxs-lookup"><span data-stu-id="1403f-201">These are hello common issues when you configure Exchange ActiveSync support for Pass-through Authentication.</span></span>

### <a name="exchange-powershell-issue"></a><span data-ttu-id="1403f-202">Exchange PowerShell 問題</span><span class="sxs-lookup"><span data-stu-id="1403f-202">Exchange PowerShell issue</span></span>

<span data-ttu-id="1403f-203">如果您看到 hello"**參數找不到符合的參數名稱 'PerTenantSwitchToESTSEnabled'\.**"</span><span class="sxs-lookup"><span data-stu-id="1403f-203">If you see hello "**A parameter cannot be found that matches parameter name 'PerTenantSwitchToESTSEnabled'\.**"</span></span> <span data-ttu-id="1403f-204">當您執行 hello 錯誤`Set-OrganizationConfig`Exchange PowerShell 命令，請連絡 Microsoft 支援。</span><span class="sxs-lookup"><span data-stu-id="1403f-204">error when you run hello `Set-OrganizationConfig` Exchange PowerShell command, contact Microsoft Support.</span></span>

### <a name="exchange-activesync-not-working"></a><span data-ttu-id="1403f-205">Exchange ActiveSync 未運作</span><span class="sxs-lookup"><span data-stu-id="1403f-205">Exchange ActiveSync not working</span></span>

<span data-ttu-id="1403f-206">hello 設定生效，某些時間 tootake-hello 取決於您環境的時間週期。</span><span class="sxs-lookup"><span data-stu-id="1403f-206">hello configuration takes some time tootake effect - hello time period depends on your environment.</span></span> <span data-ttu-id="1403f-207">如果 hello 情況持續發生一段時間，請連絡 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="1403f-207">If hello situation persists for a long time, contact Microsoft Support.</span></span>

## <a name="collecting-pass-through-authentication-agent-logs"></a><span data-ttu-id="1403f-208">收集傳遞驗證代理程式記錄</span><span class="sxs-lookup"><span data-stu-id="1403f-208">Collecting Pass-through Authentication Agent logs</span></span>

<span data-ttu-id="1403f-209">根據 hello 類型您可能有的問題，您會需要在不同的地方 toolook 傳遞驗證代理程式記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1403f-209">Depending on hello type of issue you may have, you need toolook in different places for Pass-through Authentication Agent logs.</span></span>

### <a name="authentication-agent-event-logs"></a><span data-ttu-id="1403f-210">驗證代理程式事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="1403f-210">Authentication Agent event logs</span></span>

<span data-ttu-id="1403f-211">是否有錯誤相關 toohello 驗證代理程式，開啟 hello hello 伺服器上事件檢視器應用程式，並檢查下**應用程式和服務 Logs\Microsoft\AzureAdConnect\AuthenticationAgent\Admin**。</span><span class="sxs-lookup"><span data-stu-id="1403f-211">For errors related toohello Authentication Agent, open up hello Event Viewer application on hello server and check under **Application and Service Logs\Microsoft\AzureAdConnect\AuthenticationAgent\Admin**.</span></span>

<span data-ttu-id="1403f-212">進行詳細分析，啟用 hello 「 工作階段 」 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1403f-212">For detailed analytics, enable hello "Session" log.</span></span> <span data-ttu-id="1403f-213">不正常的作業; 期間啟用此記錄檔以執行 hello 驗證代理程式使用此選項只有在進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="1403f-213">Don't run hello Authentication Agent with this log enabled during normal operations; use only for troubleshooting.</span></span> <span data-ttu-id="1403f-214">已再次停用 hello 記錄之後，才會顯示 hello 記錄內容。</span><span class="sxs-lookup"><span data-stu-id="1403f-214">hello log contents are only visible after hello log is disabled again.</span></span>

### <a name="detailed-trace-logs"></a><span data-ttu-id="1403f-215">詳細的追蹤記錄檔</span><span class="sxs-lookup"><span data-stu-id="1403f-215">Detailed trace logs</span></span>

<span data-ttu-id="1403f-216">追蹤記錄檔，尋找 tootroubleshoot 使用者登入失敗， **%programdata%\Microsoft\Azure AD 連線驗證 Agent\Trace\\**。</span><span class="sxs-lookup"><span data-stu-id="1403f-216">tootroubleshoot user sign-in failures, look for trace logs at **%programdata%\Microsoft\Azure AD Connect Authentication Agent\Trace\\**.</span></span> <span data-ttu-id="1403f-217">這些記錄檔包含在特定使用者登入失敗的原因使用 hello 傳遞驗證功能的原因。</span><span class="sxs-lookup"><span data-stu-id="1403f-217">These logs include reasons why a specific user sign-in failed using hello Pass-through Authentication feature.</span></span> <span data-ttu-id="1403f-218">這些錯誤也會顯示 hello 上述對應的 toohello 登入失敗原因[資料表](#sign-in-failure-reasons-on-the-Azure-portal)。</span><span class="sxs-lookup"><span data-stu-id="1403f-218">These errors are also mapped toohello sign-in failure reasons shown in hello preceding [table](#sign-in-failure-reasons-on-the-Azure-portal).</span></span> <span data-ttu-id="1403f-219">以下是記錄項目範例：</span><span class="sxs-lookup"><span data-stu-id="1403f-219">Following is an example log entry:</span></span>

```
    AzureADConnectAuthenticationAgentService.exe Error: 0 : Passthrough Authentication request failed. RequestId: 'df63f4a4-68b9-44ae-8d81-6ad2d844d84e'. Reason: '1328'.
        ThreadId=5
        DateTime=xxxx-xx-xxTxx:xx:xx.xxxxxxZ
```

<span data-ttu-id="1403f-220">您可以藉由開啟 hello 命令提示字元並執行下列命令的 hello 取得 hello 錯誤 (hello 前面範例中為 ' 1328') 的敘述性的詳細資料 (附註: '1328' 取代為您在記錄中看到的 hello 實際的錯誤號碼):</span><span class="sxs-lookup"><span data-stu-id="1403f-220">You can get descriptive details of hello error ('1328' in hello preceding example) by opening up hello command prompt and running hello following command (Note: Replace '1328' with hello actual error number that you see in your logs):</span></span>

`Net helpmsg 1328`

![傳遞驗證](./media/active-directory-aadconnect-pass-through-authentication/pta3.png)

### <a name="domain-controller-logs"></a><span data-ttu-id="1403f-222">網域控制站記錄</span><span class="sxs-lookup"><span data-stu-id="1403f-222">Domain Controller logs</span></span>

<span data-ttu-id="1403f-223">如果已啟用稽核記錄，其他資訊可以找到網域控制站的 hello 安全性記錄檔中。</span><span class="sxs-lookup"><span data-stu-id="1403f-223">If audit logging is enabled, additional information can be found in hello security logs of your Domain Controllers.</span></span> <span data-ttu-id="1403f-224">簡單的方式 tooquery 登入傳送的要求傳遞驗證代理程式如下所示：</span><span class="sxs-lookup"><span data-stu-id="1403f-224">A simple way tooquery sign-in requests sent by Pass-through Authentication Agents is as follows:</span></span>

```
    <QueryList>
    <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ProcessName'] and (Data='C:\Program Files\Microsoft Azure AD Connect Authentication Agent\AzureADConnectAuthenticationAgentService.exe')]]</Select>
    </Query>
    </QueryList>
```

### <a name="performance-monitor-counters"></a><span data-ttu-id="1403f-225">效能監視器計數器</span><span class="sxs-lookup"><span data-stu-id="1403f-225">Performance Monitor counters</span></span>

<span data-ttu-id="1403f-226">另一個方式 toomonitor 驗證代理程式是 tootrack 特定的效能監視器計數器 hello 驗證代理程式安裝所在的每個伺服器上。</span><span class="sxs-lookup"><span data-stu-id="1403f-226">Another way toomonitor Authentication Agents is tootrack specific Performance Monitor counters on each server where hello Authentication Agent is installed.</span></span> <span data-ttu-id="1403f-227">下列全域計數器使用 hello (**# PTA 驗證**， **#PTA 失敗驗證**和**#PTA 成功驗證**) 和錯誤計數器 (**# PTA 驗證錯誤**):</span><span class="sxs-lookup"><span data-stu-id="1403f-227">Use hello following Global counters (**# PTA authentications**, **#PTA failed authentications** and **#PTA successful authentications**) and Error counters (**# PTA authentication errors**):</span></span>

![傳遞驗證效能監視器計數器](./media/active-directory-aadconnect-pass-through-authentication/pta12.png)

>[!IMPORTANT]
><span data-ttu-id="1403f-229">傳遞驗證使用多個驗證代理程式，且_不_進行負載平衡，而提供了高可用性。</span><span class="sxs-lookup"><span data-stu-id="1403f-229">Pass-through Authentication provides high availability using multiple Authentication Agents, and _not_ load balancing.</span></span> <span data-ttu-id="1403f-230">視您的設定而定，_並非_所有的驗證代理程式都會收到數目大約_相同_的要求。</span><span class="sxs-lookup"><span data-stu-id="1403f-230">Depending on your configuration, _not_ all your Authentication Agents receive roughly _equal_ number of requests.</span></span> <span data-ttu-id="1403f-231">特定的驗證代理程式可能完全不會收到流量。</span><span class="sxs-lookup"><span data-stu-id="1403f-231">It is possible that a specific Authentication Agent receives no traffic at all.</span></span>
