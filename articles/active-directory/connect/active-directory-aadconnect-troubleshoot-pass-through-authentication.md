---
title: "Azure AD Connect：針對傳遞驗證進行疑難排解 | Microsoft Docs"
description: "本文會說明如何針對 Azure Active Directory (Azure AD) 傳遞驗證進行疑難排解。"
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
ms.openlocfilehash: 72bd39bcf720cf5704274fcdfa0f2b8fc44a77bc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-azure-active-directory-pass-through-authentication"></a><span data-ttu-id="56a76-104">針對 Azure Active Directory 傳遞驗證進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="56a76-104">Troubleshoot Azure Active Directory Pass-through Authentication</span></span>

<span data-ttu-id="56a76-105">這篇文章可協助您尋找有關 Azure AD 傳遞驗證常見問題的疑難排解資訊。</span><span class="sxs-lookup"><span data-stu-id="56a76-105">This article helps you find troubleshooting information about common issues regarding Azure AD Pass-through Authentication.</span></span>

>[!IMPORTANT]
><span data-ttu-id="56a76-106">如果傳遞驗證發生使用者登入的問題，請不要在沒有可切換的僅限雲端全域管理員帳戶的情況下，停用此功能或解除安裝傳遞驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="56a76-106">If you are facing user sign-in issues with Pass-through Authentication, don't disable the feature or uninstall Pass-through Authentication Agents without having a cloud-only Global Administrator account to fall back on.</span></span> <span data-ttu-id="56a76-107">了解如何[新增僅限雲端管理員帳戶 (英文)](../active-directory-users-create-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="56a76-107">Learn about [adding a cloud-only Global Administrator account](../active-directory-users-create-azure-portal.md).</span></span> <span data-ttu-id="56a76-108">這是確保您不會被租用戶封鎖的關鍵步驟。</span><span class="sxs-lookup"><span data-stu-id="56a76-108">Doing this step is critical and ensures that you don't get locked out of your tenant.</span></span>

## <a name="general-issues"></a><span data-ttu-id="56a76-109">一般問題</span><span class="sxs-lookup"><span data-stu-id="56a76-109">General issues</span></span>

### <a name="check-status-of-the-feature-and-authentication-agents"></a><span data-ttu-id="56a76-110">檢查此功能和驗證代理程式的狀態</span><span class="sxs-lookup"><span data-stu-id="56a76-110">Check status of the feature and Authentication Agents</span></span>

<span data-ttu-id="56a76-111">確定您租用戶上的傳遞驗證功能仍為 [已啟用]，而驗證代理程式的狀態會顯示 [作用中]，而不是 [非作用中]。</span><span class="sxs-lookup"><span data-stu-id="56a76-111">Ensure that the Pass-through Authentication feature is still **Enabled** on your tenant and the status of Authentication Agents shows **Active**, and not **Inactive**.</span></span> <span data-ttu-id="56a76-112">您可以前往 [Azure Active Directory 管理中心](https://aad.portal.azure.com/)上的 [Azure AD Connect] 刀鋒視窗來檢查狀態。</span><span class="sxs-lookup"><span data-stu-id="56a76-112">You can check status by going to the **Azure AD Connect** blade on the [Azure Active Directory admin center](https://aad.portal.azure.com/).</span></span>

![Azure Active Directory 管理中心 - Azure AD Connect 刀鋒視窗](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Azure Active Directory 管理中心 - 傳遞驗證刀鋒視窗](./media/active-directory-aadconnect-pass-through-authentication/pta11.png)

### <a name="user-facing-sign-in-error-messages"></a><span data-ttu-id="56a76-115">使用者看到的登入錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="56a76-115">User-facing sign-in error messages</span></span>

<span data-ttu-id="56a76-116">如果使用者無法登入使用傳遞驗證，他們可能會在 Azure AD 登入畫面中看到下列其中之一的使用者錯誤：</span><span class="sxs-lookup"><span data-stu-id="56a76-116">If the user is unable to sign into using Pass-through Authentication, they may see one of the following user-facing errors on the Azure AD sign-in screen:</span></span> 

|<span data-ttu-id="56a76-117">錯誤</span><span class="sxs-lookup"><span data-stu-id="56a76-117">Error</span></span>|<span data-ttu-id="56a76-118">說明</span><span class="sxs-lookup"><span data-stu-id="56a76-118">Description</span></span>|<span data-ttu-id="56a76-119">解決方案</span><span class="sxs-lookup"><span data-stu-id="56a76-119">Resolution</span></span>
| --- | --- | ---
|<span data-ttu-id="56a76-120">AADSTS80001</span><span class="sxs-lookup"><span data-stu-id="56a76-120">AADSTS80001</span></span>|<span data-ttu-id="56a76-121">無法連線至 Active Directory</span><span class="sxs-lookup"><span data-stu-id="56a76-121">Unable to connect to Active Directory</span></span>|<span data-ttu-id="56a76-122">確定代理程式伺服器和必須驗證其密碼的使用者都是相同 AD 樹系的成員，而且都能連線到 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="56a76-122">Ensure that agent servers are members of the same AD forest as the users whose passwords need to be validated and they are able to connect to Active Directory.</span></span>  
|<span data-ttu-id="56a76-123">AADSTS8002</span><span class="sxs-lookup"><span data-stu-id="56a76-123">AADSTS8002</span></span>|<span data-ttu-id="56a76-124">連線至 Active Directory 時發生逾時</span><span class="sxs-lookup"><span data-stu-id="56a76-124">A timeout occurred connecting to Active Directory</span></span>|<span data-ttu-id="56a76-125">請檢查以確定 Active Directory 可用，並且會回應來自代理程式的要求。</span><span class="sxs-lookup"><span data-stu-id="56a76-125">Check to ensure that Active Directory is available and is responding to requests from the agents.</span></span>
|<span data-ttu-id="56a76-126">AADSTS80004</span><span class="sxs-lookup"><span data-stu-id="56a76-126">AADSTS80004</span></span>|<span data-ttu-id="56a76-127">傳遞給代理程式的使用者名稱無效</span><span class="sxs-lookup"><span data-stu-id="56a76-127">The username passed to the agent was not valid</span></span>|<span data-ttu-id="56a76-128">請確定使用者嘗試用來登入的使用者名稱正確無誤。</span><span class="sxs-lookup"><span data-stu-id="56a76-128">Ensure the user is attempting to sign in with the right username.</span></span>
|<span data-ttu-id="56a76-129">AADSTS80005</span><span class="sxs-lookup"><span data-stu-id="56a76-129">AADSTS80005</span></span>|<span data-ttu-id="56a76-130">驗證發生無法預期的 WebException</span><span class="sxs-lookup"><span data-stu-id="56a76-130">Validation encountered unpredictable WebException</span></span>|<span data-ttu-id="56a76-131">暫時性錯誤。</span><span class="sxs-lookup"><span data-stu-id="56a76-131">A transient error.</span></span> <span data-ttu-id="56a76-132">重試要求。</span><span class="sxs-lookup"><span data-stu-id="56a76-132">Retry the request.</span></span> <span data-ttu-id="56a76-133">如果持續發生失敗，請連絡 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="56a76-133">If it continues to fail, contact Microsoft support.</span></span>
|<span data-ttu-id="56a76-134">AADSTS80007</span><span class="sxs-lookup"><span data-stu-id="56a76-134">AADSTS80007</span></span>|<span data-ttu-id="56a76-135">和 Active Directory 通訊時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="56a76-135">An error occurred communicating with Active Directory</span></span>|<span data-ttu-id="56a76-136">請檢查代理程式記錄檔以了解詳細資訊，並確認 Active Directory 如預期般運作。</span><span class="sxs-lookup"><span data-stu-id="56a76-136">Check the agent logs for more information and verify that Active Directory is operating as expected.</span></span>

### <a name="sign-in-failure-reasons-on-the-azure-active-directory-admin-center"></a><span data-ttu-id="56a76-137">Azure Active Directory 管理中心上的登入失敗原因</span><span class="sxs-lookup"><span data-stu-id="56a76-137">Sign-in failure reasons on the Azure Active Directory admin center</span></span>

<span data-ttu-id="56a76-138">藉由查看 [Azure Active Directory 管理中心](https://aad.portal.azure.com/)上的[登入活動報表](../active-directory-reporting-activity-sign-ins.md)，開始針對使用者登入問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="56a76-138">Start troubleshooting user sign-in issues by looking at the [sign-in activity report](../active-directory-reporting-activity-sign-ins.md) on the [Azure Active Directory admin center](https://aad.portal.azure.com/).</span></span>

![Azure Active Directory 管理中心 - 登入報告](./media/active-directory-aadconnect-pass-through-authentication/pta4.png)

<span data-ttu-id="56a76-140">巡覽至位在 [Azure Active Directory 管理中心](https://aad.portal.azure.com/)的 **Azure Active Directory** -> [登入]，按一下特定使用者的登入活動。</span><span class="sxs-lookup"><span data-stu-id="56a76-140">Navigate to **Azure Active Directory** -> **Sign-ins** on the [Azure Active Directory admin center](https://aad.portal.azure.com/) and click a specific user's sign-in activity.</span></span> <span data-ttu-id="56a76-141">尋找 [登入錯誤碼] 欄位。</span><span class="sxs-lookup"><span data-stu-id="56a76-141">Look for the **SIGN-IN ERROR CODE** field.</span></span> <span data-ttu-id="56a76-142">使用下表，將該欄位的值對應至失敗的原因和解決方式：</span><span class="sxs-lookup"><span data-stu-id="56a76-142">Map the value of that field to a failure reason and resolution using the following table:</span></span>

|<span data-ttu-id="56a76-143">登入錯誤碼</span><span class="sxs-lookup"><span data-stu-id="56a76-143">Sign-in error code</span></span>|<span data-ttu-id="56a76-144">登入失敗原因</span><span class="sxs-lookup"><span data-stu-id="56a76-144">Sign-in failure reason</span></span>|<span data-ttu-id="56a76-145">解決方案</span><span class="sxs-lookup"><span data-stu-id="56a76-145">Resolution</span></span>
| --- | --- | ---
| <span data-ttu-id="56a76-146">50144</span><span class="sxs-lookup"><span data-stu-id="56a76-146">50144</span></span> | <span data-ttu-id="56a76-147">使用者的 Active Directory 密碼已到期。</span><span class="sxs-lookup"><span data-stu-id="56a76-147">User's Active Directory password has expired.</span></span> | <span data-ttu-id="56a76-148">在您的內部部署 Active Directory 中重設使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="56a76-148">Reset the user's password in your on-premises Active Directory.</span></span>
| <span data-ttu-id="56a76-149">80001</span><span class="sxs-lookup"><span data-stu-id="56a76-149">80001</span></span> | <span data-ttu-id="56a76-150">沒有可用的驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="56a76-150">No Authentication Agent available.</span></span> | <span data-ttu-id="56a76-151">安裝並註冊驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="56a76-151">Install and register an Authentication Agent.</span></span>
| <span data-ttu-id="56a76-152">80002</span><span class="sxs-lookup"><span data-stu-id="56a76-152">80002</span></span> | <span data-ttu-id="56a76-153">驗證代理程式的密碼驗證要求已逾時。</span><span class="sxs-lookup"><span data-stu-id="56a76-153">Authentication Agent's password validation request timed out.</span></span> | <span data-ttu-id="56a76-154">檢查是否可以從驗證代理程式連線到您的 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="56a76-154">Check if your Active Directory is reachable from the Authentication Agent.</span></span>
| <span data-ttu-id="56a76-155">80003</span><span class="sxs-lookup"><span data-stu-id="56a76-155">80003</span></span> | <span data-ttu-id="56a76-156">驗證代理程式收到無效的回應。</span><span class="sxs-lookup"><span data-stu-id="56a76-156">Invalid response received by Authentication Agent.</span></span> | <span data-ttu-id="56a76-157">如果有多位使用者發生一樣的問題，請檢查您的 Active Directory 設定。</span><span class="sxs-lookup"><span data-stu-id="56a76-157">If the problem is consistently reproducible across multiple users, check your Active Directory configuration.</span></span>
| <span data-ttu-id="56a76-158">80004</span><span class="sxs-lookup"><span data-stu-id="56a76-158">80004</span></span> | <span data-ttu-id="56a76-159">登入要求中使用的使用者主體名稱 (UPN) 不正確。</span><span class="sxs-lookup"><span data-stu-id="56a76-159">Incorrect User Principal Name (UPN) used in sign-in request.</span></span> | <span data-ttu-id="56a76-160">要求使用者以正確的使用者名稱登入。</span><span class="sxs-lookup"><span data-stu-id="56a76-160">Ask the user to sign in with the correct username.</span></span>
| <span data-ttu-id="56a76-161">80005</span><span class="sxs-lookup"><span data-stu-id="56a76-161">80005</span></span> | <span data-ttu-id="56a76-162">驗證代理程式：發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="56a76-162">Authentication Agent: Error occurred.</span></span> | <span data-ttu-id="56a76-163">暫時性錯誤。</span><span class="sxs-lookup"><span data-stu-id="56a76-163">Transient error.</span></span> <span data-ttu-id="56a76-164">請稍後再試。</span><span class="sxs-lookup"><span data-stu-id="56a76-164">Try again later.</span></span>
| <span data-ttu-id="56a76-165">80007</span><span class="sxs-lookup"><span data-stu-id="56a76-165">80007</span></span> | <span data-ttu-id="56a76-166">驗證代理程式無法連線至 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="56a76-166">Authentication Agent unable to connect to Active Directory.</span></span> | <span data-ttu-id="56a76-167">檢查是否可以從驗證代理程式連線到您的 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="56a76-167">Check if your Active Directory is reachable from the Authentication Agent.</span></span>
| <span data-ttu-id="56a76-168">80010</span><span class="sxs-lookup"><span data-stu-id="56a76-168">80010</span></span> | <span data-ttu-id="56a76-169">驗證代理程式無法連線將密碼解密。</span><span class="sxs-lookup"><span data-stu-id="56a76-169">Authentication Agent unable to decrypt password.</span></span> | <span data-ttu-id="56a76-170">如果問題一再出現，請安裝並註冊新的驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="56a76-170">If the problem is consistently reproducible, install and register a new Authentication Agent.</span></span> <span data-ttu-id="56a76-171">然後解除安裝目前的代理程式。</span><span class="sxs-lookup"><span data-stu-id="56a76-171">And uninstall the current one.</span></span> 
| <span data-ttu-id="56a76-172">80011</span><span class="sxs-lookup"><span data-stu-id="56a76-172">80011</span></span> | <span data-ttu-id="56a76-173">驗證代理程式無法擷取解密金鑰。</span><span class="sxs-lookup"><span data-stu-id="56a76-173">Authentication Agent unable to retrieve decryption key.</span></span> | <span data-ttu-id="56a76-174">如果問題一再出現，請安裝並註冊新的驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="56a76-174">If the problem is consistently reproducible, install and register a new Authentication Agent.</span></span> <span data-ttu-id="56a76-175">然後解除安裝目前的代理程式。</span><span class="sxs-lookup"><span data-stu-id="56a76-175">And uninstall the current one.</span></span>

## <a name="authentication-agent-installation-issues"></a><span data-ttu-id="56a76-176">驗證代理程式安裝問題</span><span class="sxs-lookup"><span data-stu-id="56a76-176">Authentication Agent installation issues</span></span>

### <a name="an-unexpected-error-occurred"></a><span data-ttu-id="56a76-177">發生意外的錯誤</span><span class="sxs-lookup"><span data-stu-id="56a76-177">An unexpected error occurred</span></span>

<span data-ttu-id="56a76-178">從伺服器[收集代理程式記錄](#collecting-pass-through-authentication-agent-logs)，並連絡 Microsoft 支援服務解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="56a76-178">[Collect agent logs](#collecting-pass-through-authentication-agent-logs) from the server and contact Microsoft Support with your issue.</span></span>

## <a name="authentication-agent-registration-issues"></a><span data-ttu-id="56a76-179">驗證代理程式註冊問題</span><span class="sxs-lookup"><span data-stu-id="56a76-179">Authentication Agent registration issues</span></span>

### <a name="registration-of-the-authentication-agent-failed-due-to-blocked-ports"></a><span data-ttu-id="56a76-180">由於連接埠遭到封鎖，所以驗證代理程式註冊失敗。</span><span class="sxs-lookup"><span data-stu-id="56a76-180">Registration of the Authentication Agent failed due to blocked ports</span></span>

<span data-ttu-id="56a76-181">確認已安裝驗證代理程式的伺服器，能與我們列在[這裡](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites)的服務 URL 和連接埠通訊。</span><span class="sxs-lookup"><span data-stu-id="56a76-181">Ensure that the server on which the Authentication Agent has been installed can communicate with our service URLs and ports listed [here](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).</span></span>

### <a name="registration-of-the-authentication-agent-failed-due-to-token-or-account-authorization-errors"></a><span data-ttu-id="56a76-182">因為權杖或帳戶授權錯誤，所以驗證代理程式註冊失敗。</span><span class="sxs-lookup"><span data-stu-id="56a76-182">Registration of the Authentication Agent failed due to token or account authorization errors</span></span>

<span data-ttu-id="56a76-183">請確定您在所有 Azure AD Connect 或獨立驗證代理程式安裝和註冊作業中，使用僅限雲端的全域管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="56a76-183">Ensure that you use a cloud-only Global Administrator account for all Azure AD Connect or standalone Authentication Agent installation and registration operations.</span></span> <span data-ttu-id="56a76-184">啟用 MFA 的全域管理員帳戶有一個已知的問題，請暫時關閉 MFA (只是為了完成作業) 作為因應措施。</span><span class="sxs-lookup"><span data-stu-id="56a76-184">There is a known issue with MFA-enabled Global Administrator accounts; turn off MFA temporarily (only to complete the operations) as a workaround.</span></span>

### <a name="an-unexpected-error-occurred"></a><span data-ttu-id="56a76-185">發生意外的錯誤</span><span class="sxs-lookup"><span data-stu-id="56a76-185">An unexpected error occurred</span></span>

<span data-ttu-id="56a76-186">從伺服器[收集代理程式記錄](#collecting-pass-through-authentication-agent-logs)，並連絡 Microsoft 支援服務解決您的問題。</span><span class="sxs-lookup"><span data-stu-id="56a76-186">[Collect agent logs](#collecting-pass-through-authentication-agent-logs) from the server and contact Microsoft Support with your issue.</span></span>

## <a name="authentication-agent-uninstallation-issues"></a><span data-ttu-id="56a76-187">驗證代理程式解除安裝問題</span><span class="sxs-lookup"><span data-stu-id="56a76-187">Authentication Agent uninstallation issues</span></span>

### <a name="warning-message-when-uninstalling-azure-ad-connect"></a><span data-ttu-id="56a76-188">解除安裝 Azure AD Connect 時出現的警告訊息</span><span class="sxs-lookup"><span data-stu-id="56a76-188">Warning message when uninstalling Azure AD Connect</span></span>

<span data-ttu-id="56a76-189">如果您已在租用戶上啟用傳遞驗證，但您嘗試解除安裝 Azure AD Connect，它會顯示下列警告訊息：「除非您在其他伺服器上有安裝其他傳遞驗證代理程式，否則使用者將無法登入 Azure AD。」</span><span class="sxs-lookup"><span data-stu-id="56a76-189">If you have Pass-through Authentication enabled on your tenant and you try to uninstall Azure AD Connect, it shows you the following warning message: "Users will not be able to sign-in to Azure AD unless you have other Pass-through Authentication agents installed on other servers."</span></span>

<span data-ttu-id="56a76-190">在您解除安裝 Azure AD Connect 之前，請確認您的設定為[高可用性](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability)，以避免中斷使用者登入。</span><span class="sxs-lookup"><span data-stu-id="56a76-190">Ensure that your setup is [high available](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) before you uninstall Azure AD Connect to avoid breaking user sign-in.</span></span>

## <a name="issues-with-enabling-the-feature"></a><span data-ttu-id="56a76-191">啟用此功能的問題</span><span class="sxs-lookup"><span data-stu-id="56a76-191">Issues with enabling the feature</span></span>

### <a name="enabling-the-feature-failed-because-there-were-no-authentication-agents-available"></a><span data-ttu-id="56a76-192">因為沒有任何可用的驗證代理程式，所以啟用此功能失敗。</span><span class="sxs-lookup"><span data-stu-id="56a76-192">Enabling the feature failed because there were no Authentication Agents available</span></span>

<span data-ttu-id="56a76-193">您至少必須有一個使用中的驗證代理程式，才能在租用戶上啟用傳遞驗證。</span><span class="sxs-lookup"><span data-stu-id="56a76-193">You need to have at least one active Authentication Agent to enable Pass-through Authentication on your tenant.</span></span> <span data-ttu-id="56a76-194">您可以安裝 Azure AD Connect 或獨立的驗證代理程式，來安裝驗證代理程式。</span><span class="sxs-lookup"><span data-stu-id="56a76-194">You can install an Authentication Agent by either installing Azure AD Connect or a standalone Authentication Agent.</span></span>

### <a name="enabling-the-feature-failed-due-to-blocked-ports"></a><span data-ttu-id="56a76-195">因為連接埠遭到封鎖，所以啟用功能失敗。</span><span class="sxs-lookup"><span data-stu-id="56a76-195">Enabling the feature failed due to blocked ports</span></span>

<span data-ttu-id="56a76-196">確認已安裝 Azure AD Connect 的伺服器能與我們的服務 URL 和連接埠通訊，如[這裡](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites)所列。</span><span class="sxs-lookup"><span data-stu-id="56a76-196">Ensure that the server on which Azure AD Connect is installed can communicate with our service URLs and ports listed [here](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).</span></span>

### <a name="enabling-the-feature-failed-due-to-token-or-account-authorization-errors"></a><span data-ttu-id="56a76-197">因為權杖或帳戶授權錯誤，所以啟用功能失敗。</span><span class="sxs-lookup"><span data-stu-id="56a76-197">Enabling the feature failed due to token or account authorization errors</span></span>

<span data-ttu-id="56a76-198">請確定您使用僅限雲端的全域管理員帳戶來啟用此功能。</span><span class="sxs-lookup"><span data-stu-id="56a76-198">Ensure that you use a cloud-only Global Administrator account when enabling the feature.</span></span> <span data-ttu-id="56a76-199">啟用 Multi-Factor Authentication (MFA) 的全域管理員帳戶有一個已知的問題，請暫時關閉 MFA (只是為了完成作業) 作為因應措施。</span><span class="sxs-lookup"><span data-stu-id="56a76-199">There is a known issue with multi-factor authentication (MFA)-enabled Global Administrator accounts; turn off MFA temporarily (only to complete the operation) as a workaround.</span></span>

## <a name="exchange-activesync-configuration-issues"></a><span data-ttu-id="56a76-200">Exchange ActiveSync 設定問題</span><span class="sxs-lookup"><span data-stu-id="56a76-200">Exchange ActiveSync configuration issues</span></span>

<span data-ttu-id="56a76-201">這些是在設定傳遞驗證設定的 Exchange ActiveSync 支援時常見的問題。</span><span class="sxs-lookup"><span data-stu-id="56a76-201">These are the common issues when you configure Exchange ActiveSync support for Pass-through Authentication.</span></span>

### <a name="exchange-powershell-issue"></a><span data-ttu-id="56a76-202">Exchange PowerShell 問題</span><span class="sxs-lookup"><span data-stu-id="56a76-202">Exchange PowerShell issue</span></span>

<span data-ttu-id="56a76-203">如果您看到 「**參數找不到符合的參數名稱 'PerTenantSwitchToESTSEnabled'\.**"</span><span class="sxs-lookup"><span data-stu-id="56a76-203">If you see the "**A parameter cannot be found that matches parameter name 'PerTenantSwitchToESTSEnabled'\.**"</span></span> <span data-ttu-id="56a76-204">當您執行的錯誤`Set-OrganizationConfig`Exchange PowerShell 命令，請連絡 Microsoft 支援。</span><span class="sxs-lookup"><span data-stu-id="56a76-204">error when you run the `Set-OrganizationConfig` Exchange PowerShell command, contact Microsoft Support.</span></span>

### <a name="exchange-activesync-not-working"></a><span data-ttu-id="56a76-205">Exchange ActiveSync 未運作</span><span class="sxs-lookup"><span data-stu-id="56a76-205">Exchange ActiveSync not working</span></span>

<span data-ttu-id="56a76-206">此設定需要一些時間才會生效，所需時間取決於您的環境。</span><span class="sxs-lookup"><span data-stu-id="56a76-206">The configuration takes some time to take effect - the time period depends on your environment.</span></span> <span data-ttu-id="56a76-207">如果此狀況持續很長的時間，請連絡 Microsoft 支援服務。</span><span class="sxs-lookup"><span data-stu-id="56a76-207">If the situation persists for a long time, contact Microsoft Support.</span></span>

## <a name="collecting-pass-through-authentication-agent-logs"></a><span data-ttu-id="56a76-208">收集傳遞驗證代理程式記錄</span><span class="sxs-lookup"><span data-stu-id="56a76-208">Collecting Pass-through Authentication Agent logs</span></span>

<span data-ttu-id="56a76-209">根據發生的問題類型，您需要在不同的位置尋找傳遞驗證代理程式記錄。</span><span class="sxs-lookup"><span data-stu-id="56a76-209">Depending on the type of issue you may have, you need to look in different places for Pass-through Authentication Agent logs.</span></span>

### <a name="authentication-agent-event-logs"></a><span data-ttu-id="56a76-210">驗證代理程式事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="56a76-210">Authentication Agent event logs</span></span>

<span data-ttu-id="56a76-211">如需與驗證代理程式相關的錯誤，請開啟伺服器上的事件檢視器應用程式，並於 **Application and Service Logs\Microsoft\AzureAdConnect\AuthenticationAgent\Admin** 下查看。</span><span class="sxs-lookup"><span data-stu-id="56a76-211">For errors related to the Authentication Agent, open up the Event Viewer application on the server and check under **Application and Service Logs\Microsoft\AzureAdConnect\AuthenticationAgent\Admin**.</span></span>

<span data-ttu-id="56a76-212">如需詳細分析，請啟用「工作階段」記錄。</span><span class="sxs-lookup"><span data-stu-id="56a76-212">For detailed analytics, enable the "Session" log.</span></span> <span data-ttu-id="56a76-213">不要使用正常作業期間啟用的記錄檔執行驗證代理程式，此記錄檔只適用於進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="56a76-213">Don't run the Authentication Agent with this log enabled during normal operations; use only for troubleshooting.</span></span> <span data-ttu-id="56a76-214">只有再次停用此記錄檔之後，才能看見記錄檔的內容。</span><span class="sxs-lookup"><span data-stu-id="56a76-214">The log contents are only visible after the log is disabled again.</span></span>

### <a name="detailed-trace-logs"></a><span data-ttu-id="56a76-215">詳細的追蹤記錄檔</span><span class="sxs-lookup"><span data-stu-id="56a76-215">Detailed trace logs</span></span>

<span data-ttu-id="56a76-216">若要針對使用者登入失敗進行疑難排解，請查看追蹤記錄，其位於 **%programdata%\Microsoft\Azure AD Connect Authentication Agent\Trace\\**。</span><span class="sxs-lookup"><span data-stu-id="56a76-216">To troubleshoot user sign-in failures, look for trace logs at **%programdata%\Microsoft\Azure AD Connect Authentication Agent\Trace\\**.</span></span> <span data-ttu-id="56a76-217">這些記錄包含使用傳遞驗證功能的特定使用者為什麼會登入失敗的原因。</span><span class="sxs-lookup"><span data-stu-id="56a76-217">These logs include reasons why a specific user sign-in failed using the Pass-through Authentication feature.</span></span> <span data-ttu-id="56a76-218">這些錯誤也對應到先前[資料表](#sign-in-failure-reasons-on-the-Azure-portal)中所示的登入失敗原因。</span><span class="sxs-lookup"><span data-stu-id="56a76-218">These errors are also mapped to the sign-in failure reasons shown in the preceding [table](#sign-in-failure-reasons-on-the-Azure-portal).</span></span> <span data-ttu-id="56a76-219">以下是記錄項目範例：</span><span class="sxs-lookup"><span data-stu-id="56a76-219">Following is an example log entry:</span></span>

```
    AzureADConnectAuthenticationAgentService.exe Error: 0 : Passthrough Authentication request failed. RequestId: 'df63f4a4-68b9-44ae-8d81-6ad2d844d84e'. Reason: '1328'.
        ThreadId=5
        DateTime=xxxx-xx-xxTxx:xx:xx.xxxxxxZ
```

<span data-ttu-id="56a76-220">您可以開啟命令提示字元並執行下列命令 (注意：請以您在記錄中看到的實際錯誤編號取代 '1328')，以取得錯誤 (前例中為 '1328') 的描述性詳細資料：</span><span class="sxs-lookup"><span data-stu-id="56a76-220">You can get descriptive details of the error ('1328' in the preceding example) by opening up the command prompt and running the following command (Note: Replace '1328' with the actual error number that you see in your logs):</span></span>

`Net helpmsg 1328`

![傳遞驗證](./media/active-directory-aadconnect-pass-through-authentication/pta3.png)

### <a name="domain-controller-logs"></a><span data-ttu-id="56a76-222">網域控制站記錄檔</span><span class="sxs-lookup"><span data-stu-id="56a76-222">Domain Controller logs</span></span>

<span data-ttu-id="56a76-223">如果已經啟用稽核記錄，您可以在網域控制站的安全性記錄檔中找到其他資訊。</span><span class="sxs-lookup"><span data-stu-id="56a76-223">If audit logging is enabled, additional information can be found in the security logs of your Domain Controllers.</span></span> <span data-ttu-id="56a76-224">查詢傳遞驗證代理程式所傳送之登入要求的簡單方式如下︰</span><span class="sxs-lookup"><span data-stu-id="56a76-224">A simple way to query sign-in requests sent by Pass-through Authentication Agents is as follows:</span></span>

```
    <QueryList>
    <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ProcessName'] and (Data='C:\Program Files\Microsoft Azure AD Connect Authentication Agent\AzureADConnectAuthenticationAgentService.exe')]]</Select>
    </Query>
    </QueryList>
```

### <a name="performance-monitor-counters"></a><span data-ttu-id="56a76-225">效能監視器計數器</span><span class="sxs-lookup"><span data-stu-id="56a76-225">Performance Monitor counters</span></span>

<span data-ttu-id="56a76-226">另一種監視驗證代理程式的方法就是，追蹤每個有安裝驗證代理程式之伺服器上的特定效能監視計數器。</span><span class="sxs-lookup"><span data-stu-id="56a76-226">Another way to monitor Authentication Agents is to track specific Performance Monitor counters on each server where the Authentication Agent is installed.</span></span> <span data-ttu-id="56a76-227">使用下列全域計數器 (**# PTA authentications**、**#PTA failed authentications** 及 **#PTA successful authentications**) 和錯誤計數器 (**# PTA authentication errors**)：</span><span class="sxs-lookup"><span data-stu-id="56a76-227">Use the following Global counters (**# PTA authentications**, **#PTA failed authentications** and **#PTA successful authentications**) and Error counters (**# PTA authentication errors**):</span></span>

![傳遞驗證效能監視器計數器](./media/active-directory-aadconnect-pass-through-authentication/pta12.png)

>[!IMPORTANT]
><span data-ttu-id="56a76-229">傳遞驗證使用多個驗證代理程式，且_不_進行負載平衡，而提供了高可用性。</span><span class="sxs-lookup"><span data-stu-id="56a76-229">Pass-through Authentication provides high availability using multiple Authentication Agents, and _not_ load balancing.</span></span> <span data-ttu-id="56a76-230">視您的設定而定，_並非_所有的驗證代理程式都會收到數目大約_相同_的要求。</span><span class="sxs-lookup"><span data-stu-id="56a76-230">Depending on your configuration, _not_ all your Authentication Agents receive roughly _equal_ number of requests.</span></span> <span data-ttu-id="56a76-231">特定的驗證代理程式可能完全不會收到流量。</span><span class="sxs-lookup"><span data-stu-id="56a76-231">It is possible that a specific Authentication Agent receives no traffic at all.</span></span>
