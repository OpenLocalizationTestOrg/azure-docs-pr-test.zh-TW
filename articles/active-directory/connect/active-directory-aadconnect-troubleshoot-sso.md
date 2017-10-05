---
title: "Azure AD Connect：針對無縫單一登入進行疑難排解 | Microsoft Docs"
description: "本主題說明如何針對 Azure Active Directory 無縫單一登入 (Azure AD 無縫 SSO) 進行疑難排解。"
services: active-directory
keywords: "何謂 Azure AD Connect、安裝 Active Directory、Azure AD、SSO、單一登入的必要元件"
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
ms.openlocfilehash: bc4ff9125553c8918df3a1f84041560a5b7d4cd8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-azure-active-directory-seamless-single-sign-on"></a><span data-ttu-id="3499a-104">針對 Azure Active Directory 無縫單一登入進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="3499a-104">Troubleshoot Azure Active Directory Seamless Single Sign-On</span></span>

<span data-ttu-id="3499a-105">這篇文章可協助您尋找有關 Azure AD 無縫單一登入常見問題的疑難排解資訊。</span><span class="sxs-lookup"><span data-stu-id="3499a-105">This article helps you find troubleshooting information about common issues regarding Azure AD Seamless Single Sign-On.</span></span>

## <a name="known-issues"></a><span data-ttu-id="3499a-106">已知問題</span><span class="sxs-lookup"><span data-stu-id="3499a-106">Known issues</span></span>

- <span data-ttu-id="3499a-107">如果您正在同步處理 30 個或更多的 AD 樹系，您無法使用 Azure AD Connect 啟用無縫 SSO。</span><span class="sxs-lookup"><span data-stu-id="3499a-107">If you are synchronizing 30 or more AD forests, you can't enable Seamless SSO using Azure AD Connect.</span></span> <span data-ttu-id="3499a-108">您可以在租用戶上[手動啟用](#manual-reset-of-azure-ad-seamless-sso)此功能，以解決這個問題。</span><span class="sxs-lookup"><span data-stu-id="3499a-108">As a workaround, you can [manually enable](#manual-reset-of-azure-ad-seamless-sso) the feature on your tenant.</span></span>
- <span data-ttu-id="3499a-109">將 Azure AD 服務 URL (https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net) 新增至「信任的網站」區域而非「近端內部網路」區域，**以阻止使用者登入**。</span><span class="sxs-lookup"><span data-stu-id="3499a-109">Adding Azure AD service URLs (https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net) to the "Trusted sites" zone instead of the "Local intranet" zone **blocks users from signing in**.</span></span>
- <span data-ttu-id="3499a-110">無縫 SSO 無法在 Firefox 和 Edge 的私人瀏覽模式中運作。</span><span class="sxs-lookup"><span data-stu-id="3499a-110">Seamless SSO doesn't work in private browsing mode on Firefox and Edge.</span></span> <span data-ttu-id="3499a-111">此外當「增強保護」模式開啟時，Internet Explorer 也是如此。</span><span class="sxs-lookup"><span data-stu-id="3499a-111">And also on Internet Explorer when Enhanced Protection mode is turned on.</span></span>

>[!IMPORTANT]
><span data-ttu-id="3499a-112">我們最近已復原對 Edge 的支援，以調查客戶回報的問題。</span><span class="sxs-lookup"><span data-stu-id="3499a-112">We recently rolled back support for Edge to investigate customer-reported issues.</span></span>

## <a name="check-status-of-the-feature"></a><span data-ttu-id="3499a-113">檢查功能的狀態</span><span class="sxs-lookup"><span data-stu-id="3499a-113">Check status of the feature</span></span>

<span data-ttu-id="3499a-114">確認您租用戶端的無縫 SSO 功能仍為 [已啟用]。</span><span class="sxs-lookup"><span data-stu-id="3499a-114">Ensure that the Seamless SSO feature is still **Enabled** on your tenant.</span></span> <span data-ttu-id="3499a-115">您可以前往 [Azure Active Directory 管理中心](https://aad.portal.azure.com/)上的 [Azure AD Connect] 刀鋒視窗來檢查狀態。</span><span class="sxs-lookup"><span data-stu-id="3499a-115">You can check status by going to the **Azure AD Connect** blade on the [Azure Active Directory admin center](https://aad.portal.azure.com/).</span></span>

![Azure Active Directory 管理中心 - Azure AD Connect 刀鋒視窗](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="sign-in-failure-reasons-on-the-azure-active-directory-admin-center"></a><span data-ttu-id="3499a-117">Azure Active Directory 管理中心上的登入失敗原因</span><span class="sxs-lookup"><span data-stu-id="3499a-117">Sign-in failure reasons on the Azure Active Directory admin center</span></span>

<span data-ttu-id="3499a-118">[Azure Active Directory 管理中心](https://aad.portal.azure.com/)的[登入活動報表](../active-directory-reporting-activity-sign-ins.md)，是開始針對無縫 SSO 使用者登入問題進行疑難排解的好地方。</span><span class="sxs-lookup"><span data-stu-id="3499a-118">A good place to start troubleshooting user sign-in issues with Seamless SSO is to look at the [sign-in activity report](../active-directory-reporting-activity-sign-ins.md) on the [Azure Active Directory admin center](https://aad.portal.azure.com/).</span></span>

![Azure Active Directory 管理中心 - 登入報告](./media/active-directory-aadconnect-sso/sso9.png)

<span data-ttu-id="3499a-120">巡覽至位在 [Azure Active Directory 管理中心](https://aad.portal.azure.com/)的 **Azure Active Directory** -> [登入]，按一下特定使用者的登入活動。</span><span class="sxs-lookup"><span data-stu-id="3499a-120">Navigate to **Azure Active Directory** -> **Sign-ins** on the [Azure Active Directory admin center](https://aad.portal.azure.com/) and click a specific user's sign-in activity.</span></span> <span data-ttu-id="3499a-121">尋找 [登入錯誤碼] 欄位。</span><span class="sxs-lookup"><span data-stu-id="3499a-121">Look for the **SIGN-IN ERROR CODE** field.</span></span> <span data-ttu-id="3499a-122">使用下表，將該欄位的值對應至失敗的原因和解決方式：</span><span class="sxs-lookup"><span data-stu-id="3499a-122">Map the value of that field to a failure reason and resolution using the following table:</span></span>

|<span data-ttu-id="3499a-123">登入錯誤碼</span><span class="sxs-lookup"><span data-stu-id="3499a-123">Sign-in error code</span></span>|<span data-ttu-id="3499a-124">登入失敗原因</span><span class="sxs-lookup"><span data-stu-id="3499a-124">Sign-in failure reason</span></span>|<span data-ttu-id="3499a-125">解決方案</span><span class="sxs-lookup"><span data-stu-id="3499a-125">Resolution</span></span>
| --- | --- | ---
| <span data-ttu-id="3499a-126">81001</span><span class="sxs-lookup"><span data-stu-id="3499a-126">81001</span></span> | <span data-ttu-id="3499a-127">使用者的 Kerberos 票證太大。</span><span class="sxs-lookup"><span data-stu-id="3499a-127">User's Kerberos ticket is too large.</span></span> | <span data-ttu-id="3499a-128">降低使用者的群組成員資格，並再試一次。</span><span class="sxs-lookup"><span data-stu-id="3499a-128">Reduce user's group memberships and try again.</span></span>
| <span data-ttu-id="3499a-129">81002</span><span class="sxs-lookup"><span data-stu-id="3499a-129">81002</span></span> | <span data-ttu-id="3499a-130">無法驗證使用者的 Kerberos 票證。</span><span class="sxs-lookup"><span data-stu-id="3499a-130">Unable to validate user's Kerberos ticket.</span></span> | <span data-ttu-id="3499a-131">請參閱[針對檢查清單進行疑難排解](#troubleshooting-checklist)。</span><span class="sxs-lookup"><span data-stu-id="3499a-131">See [troubleshooting checklist](#troubleshooting-checklist).</span></span>
| <span data-ttu-id="3499a-132">81003</span><span class="sxs-lookup"><span data-stu-id="3499a-132">81003</span></span> | <span data-ttu-id="3499a-133">無法驗證使用者的 Kerberos 票證。</span><span class="sxs-lookup"><span data-stu-id="3499a-133">Unable to validate user's Kerberos ticket.</span></span> | <span data-ttu-id="3499a-134">請參閱[針對檢查清單進行疑難排解](#troubleshooting-checklist)。</span><span class="sxs-lookup"><span data-stu-id="3499a-134">See [troubleshooting checklist](#troubleshooting-checklist).</span></span>
| <span data-ttu-id="3499a-135">81004</span><span class="sxs-lookup"><span data-stu-id="3499a-135">81004</span></span> | <span data-ttu-id="3499a-136">Kerberos 驗證嘗試失敗。</span><span class="sxs-lookup"><span data-stu-id="3499a-136">Kerberos authentication attempt failed.</span></span> | <span data-ttu-id="3499a-137">請參閱[針對檢查清單進行疑難排解](#troubleshooting-checklist)。</span><span class="sxs-lookup"><span data-stu-id="3499a-137">See [troubleshooting checklist](#troubleshooting-checklist).</span></span>
| <span data-ttu-id="3499a-138">81008</span><span class="sxs-lookup"><span data-stu-id="3499a-138">81008</span></span> | <span data-ttu-id="3499a-139">無法驗證使用者的 Kerberos 票證。</span><span class="sxs-lookup"><span data-stu-id="3499a-139">Unable to validate user's Kerberos ticket.</span></span> | <span data-ttu-id="3499a-140">請參閱[針對檢查清單進行疑難排解](#troubleshooting-checklist)。</span><span class="sxs-lookup"><span data-stu-id="3499a-140">See [troubleshooting checklist](#troubleshooting-checklist).</span></span>
| <span data-ttu-id="3499a-141">81009</span><span class="sxs-lookup"><span data-stu-id="3499a-141">81009</span></span> | <span data-ttu-id="3499a-142">「無法驗證使用者的 Kerberos 票證。</span><span class="sxs-lookup"><span data-stu-id="3499a-142">"Unable to validate user's Kerberos ticket.</span></span> | <span data-ttu-id="3499a-143">請參閱[針對檢查清單進行疑難排解](#troubleshooting-checklist)。</span><span class="sxs-lookup"><span data-stu-id="3499a-143">See [troubleshooting checklist](#troubleshooting-checklist).</span></span>
| <span data-ttu-id="3499a-144">81010</span><span class="sxs-lookup"><span data-stu-id="3499a-144">81010</span></span> | <span data-ttu-id="3499a-145">無縫式 SSO 失敗，因為使用者的 Kerberos 票證已過期或無效。</span><span class="sxs-lookup"><span data-stu-id="3499a-145">Seamless SSO failed because the user's Kerberos ticket has expired or is invalid.</span></span> | <span data-ttu-id="3499a-146">使用者需要從您公司網路內部已加入網域的裝置登入。</span><span class="sxs-lookup"><span data-stu-id="3499a-146">User needs to sign in from a domain-joined device inside your corporate network.</span></span>
| <span data-ttu-id="3499a-147">81011</span><span class="sxs-lookup"><span data-stu-id="3499a-147">81011</span></span> | <span data-ttu-id="3499a-148">找不到以使用者的 Kerberos 票證中資訊為基礎的使用者物件。</span><span class="sxs-lookup"><span data-stu-id="3499a-148">Unable to find user object based on information in the user's Kerberos ticket.</span></span> | <span data-ttu-id="3499a-149">使用 Azure AD Connect 同步處理使用者資訊至 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="3499a-149">Use Azure AD Connect to synchronize user information into Azure AD.</span></span>
| <span data-ttu-id="3499a-150">81012</span><span class="sxs-lookup"><span data-stu-id="3499a-150">81012</span></span> | <span data-ttu-id="3499a-151">嘗試登入 Azure AD 的使用者與登入裝置的使用者不同。</span><span class="sxs-lookup"><span data-stu-id="3499a-151">The user trying to sign in to Azure AD is different from the user signed into the device.</span></span> | <span data-ttu-id="3499a-152">從不同的裝置登入。</span><span class="sxs-lookup"><span data-stu-id="3499a-152">Sign in from a different device.</span></span>
| <span data-ttu-id="3499a-153">81013</span><span class="sxs-lookup"><span data-stu-id="3499a-153">81013</span></span> | <span data-ttu-id="3499a-154">找不到以使用者的 Kerberos 票證中資訊為基礎的使用者物件。</span><span class="sxs-lookup"><span data-stu-id="3499a-154">Unable to find user object based on information in the user's Kerberos ticket.</span></span> |<span data-ttu-id="3499a-155">使用 Azure AD Connect 同步處理使用者資訊至 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="3499a-155">Use Azure AD Connect to synchronize user information into Azure AD.</span></span> 

## <a name="troubleshooting-checklist"></a><span data-ttu-id="3499a-156">疑難排解檢查清單</span><span class="sxs-lookup"><span data-stu-id="3499a-156">Troubleshooting checklist</span></span>

<span data-ttu-id="3499a-157">使用下列檢查清單來針對無縫 SSO 問題進行疑難排解︰</span><span class="sxs-lookup"><span data-stu-id="3499a-157">Use the following checklist to troubleshoot Seamless SSO issues:</span></span>

- <span data-ttu-id="3499a-158">在 Azure AD Connect 上檢查是否已啟用無縫 SSO 功能。</span><span class="sxs-lookup"><span data-stu-id="3499a-158">Check if the Seamless SSO feature is enabled in Azure AD Connect.</span></span> <span data-ttu-id="3499a-159">如果您無法啟用此功能 (例如，因為連接埠已封鎖)，請確定您已完成所有[必要條件](active-directory-aadconnect-sso-quick-start.md#step-1-check-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="3499a-159">If you can't enable the feature (for example, due to a blocked port), ensure that you have all the [pre-requisites](active-directory-aadconnect-sso-quick-start.md#step-1-check-prerequisites) in place.</span></span>
- <span data-ttu-id="3499a-160">請檢查這兩個 Azure AD URL (https://autologon.microsoftazuread-sso.com 和 https://aadg.windows.net.nsatc.net) 都屬於使用者的內部網路區域設定。</span><span class="sxs-lookup"><span data-stu-id="3499a-160">Check if both these Azure AD URLs (https://autologon.microsoftazuread-sso.com and https://aadg.windows.net.nsatc.net) are part of the user's Intranet zone settings.</span></span>
- <span data-ttu-id="3499a-161">確定公司裝置已加入 AD 網域。</span><span class="sxs-lookup"><span data-stu-id="3499a-161">Ensure the corporate device is joined to the AD domain.</span></span>
- <span data-ttu-id="3499a-162">確定使用者是使用 AD 網域帳戶登入裝置。</span><span class="sxs-lookup"><span data-stu-id="3499a-162">Ensure the user is logged on to the device using an AD domain account.</span></span>
- <span data-ttu-id="3499a-163">確定使用者帳戶是來自已設定無縫 SSO 的 AD 樹系。</span><span class="sxs-lookup"><span data-stu-id="3499a-163">Ensure that the user's account is from an AD forest where Seamless SSO has been set up.</span></span>
- <span data-ttu-id="3499a-164">確定裝置已連線到公司網路。</span><span class="sxs-lookup"><span data-stu-id="3499a-164">Ensure the device is connected on the corporate network.</span></span>
- <span data-ttu-id="3499a-165">確定裝置的時間已經與 Active Directory 和網域控制站的時間同步，且彼此的時間差不到五分鐘。</span><span class="sxs-lookup"><span data-stu-id="3499a-165">Ensure that the device's time is synchronized with the Active Directory's and the Domain Controllers' time and is within five minutes of each other.</span></span>
- <span data-ttu-id="3499a-166">從命令提示字元使用 **klist** 命令，列出裝置上現有的 Kerberos 票證。</span><span class="sxs-lookup"><span data-stu-id="3499a-166">List existing Kerberos tickets on the device using the **klist** command from a command prompt.</span></span> <span data-ttu-id="3499a-167">檢查是否有核發給 `AZUREADSSOACCT` 電腦帳戶的票證。</span><span class="sxs-lookup"><span data-stu-id="3499a-167">Check if tickets issued for the `AZUREADSSOACCT` computer account are present.</span></span> <span data-ttu-id="3499a-168">使用者的 Kerberos 票證有效期通常為 12 個小時。</span><span class="sxs-lookup"><span data-stu-id="3499a-168">Users' Kerberos tickets are typically valid for 12 hours.</span></span> <span data-ttu-id="3499a-169">您的 Active Directory 可能有不同的設定。</span><span class="sxs-lookup"><span data-stu-id="3499a-169">You may have  different settings in your Active Directory.</span></span>
- <span data-ttu-id="3499a-170">使用 **klist purge** 命令從裝置中清除現有的 Kerberos 票證，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="3499a-170">Purge existing Kerberos tickets from the device using the **klist purge** command, and try again.</span></span>
- <span data-ttu-id="3499a-171">若要判斷是否有 JavaScript 相關問題，請檢閱瀏覽器的主控台記錄 (在 [開發人員工具] 底下)。</span><span class="sxs-lookup"><span data-stu-id="3499a-171">To determine if there are JavaScript-related issues, review the console logs of the browser (under "Developer Tools").</span></span>
- <span data-ttu-id="3499a-172">同時檢閱[網域控制站記錄](#domain-controller-logs)。</span><span class="sxs-lookup"><span data-stu-id="3499a-172">Review the [Domain Controller logs](#domain-controller-logs) as well.</span></span>

### <a name="domain-controller-logs"></a><span data-ttu-id="3499a-173">網域控制站記錄</span><span class="sxs-lookup"><span data-stu-id="3499a-173">Domain Controller logs</span></span>

<span data-ttu-id="3499a-174">如果網域控制站已啟用成功稽核，則每次使用者使用無縫 SSO 登入時，系統都會在事件記錄中記錄一個安全性項目。</span><span class="sxs-lookup"><span data-stu-id="3499a-174">If success auditing is enabled on your Domain Controller, then every time a user signs in using Seamless SSO a security entry is recorded in the Event log.</span></span> <span data-ttu-id="3499a-175">您可以使用下列查詢找到這些安全性事件 (尋找與電腦帳戶 **AzureADSSOAcc$** 建立關聯的事件 **4769**)：</span><span class="sxs-lookup"><span data-stu-id="3499a-175">You can find these security events using the following query (look for event **4769** associated with the computer account **AzureADSSOAcc$**):</span></span>

```
    <QueryList>
      <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ServiceName'] and (Data='AZUREADSSOACC$')]]</Select>
      </Query>
    </QueryList>
```

## <a name="manual-reset-of-the-feature"></a><span data-ttu-id="3499a-176">手動重設該功能</span><span class="sxs-lookup"><span data-stu-id="3499a-176">Manual reset of the feature</span></span>

<span data-ttu-id="3499a-177">如果疑難排解無法解決問題，您可以在租用戶上手動重設此功能。</span><span class="sxs-lookup"><span data-stu-id="3499a-177">If troubleshooting didn't help, you can manually reset the feature on your tenant.</span></span> <span data-ttu-id="3499a-178">請在執行 Azure AD Connect 的內部部署伺服器上依照下列步驟操作：</span><span class="sxs-lookup"><span data-stu-id="3499a-178">Follow these steps on the on-premises server where you are running Azure AD Connect:</span></span>

### <a name="step-1-import-the-seamless-sso-powershell-module"></a><span data-ttu-id="3499a-179">步驟 1：匯入無縫 SSO PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="3499a-179">Step 1: Import the Seamless SSO PowerShell module</span></span>

1. <span data-ttu-id="3499a-180">首先，下載並安裝 [Microsoft Online Services 登入小幫手](http://go.microsoft.com/fwlink/?LinkID=286152)。</span><span class="sxs-lookup"><span data-stu-id="3499a-180">First, download, and install the [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span>
2. <span data-ttu-id="3499a-181">接著下載並安裝 [適用於 Windows PowerShell 的 64 位元 Azure Active Directory 模組](http://go.microsoft.com/fwlink/p/?linkid=236297)。</span><span class="sxs-lookup"><span data-stu-id="3499a-181">Then download and install the [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>
3. <span data-ttu-id="3499a-182">瀏覽到 `%programfiles%\Microsoft Azure Active Directory Connect` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="3499a-182">Navigate to the `%programfiles%\Microsoft Azure Active Directory Connect` folder.</span></span>
4. <span data-ttu-id="3499a-183">使用此命令匯入順暢 SSO PowerShell 模組：`Import-Module .\AzureADSSO.psd1`。</span><span class="sxs-lookup"><span data-stu-id="3499a-183">Import the Seamless SSO PowerShell module using this command: `Import-Module .\AzureADSSO.psd1`.</span></span>

### <a name="step-2-get-the-list-of-ad-forests-on-which-seamless-sso-has-been-enabled"></a><span data-ttu-id="3499a-184">步驟 2：取得已啟用無縫 SSO 的 AD 樹系清單</span><span class="sxs-lookup"><span data-stu-id="3499a-184">Step 2: Get the list of AD forests on which Seamless SSO has been enabled</span></span>

1. <span data-ttu-id="3499a-185">以系統管理員身分執行 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="3499a-185">Run PowerShell as Administrator.</span></span> <span data-ttu-id="3499a-186">在 PowerShell 中，呼叫 `New-AzureADSSOAuthenticationContext`。</span><span class="sxs-lookup"><span data-stu-id="3499a-186">In PowerShell, call `New-AzureADSSOAuthenticationContext`.</span></span> <span data-ttu-id="3499a-187">出現提示時，輸入您租用戶的全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="3499a-187">When prompted, enter your tenant's Global Administrator credentials.</span></span>
2. <span data-ttu-id="3499a-188">呼叫 `Get-AzureADSSOStatus`。</span><span class="sxs-lookup"><span data-stu-id="3499a-188">Call `Get-AzureADSSOStatus`.</span></span> <span data-ttu-id="3499a-189">此命令會提供已啟用這項功能的 AD 樹系清單 (查看 [網域] 清單)。</span><span class="sxs-lookup"><span data-stu-id="3499a-189">This command provides you the list of AD forests (look at the "Domains" list) on which this feature has been enabled.</span></span>

### <a name="step-3-disable-seamless-sso-for-each-ad-forest-that-it-was-set-it-up-on"></a><span data-ttu-id="3499a-190">步驟3：針對已設定無縫 SSO 的每個 AD 樹系停用該功能</span><span class="sxs-lookup"><span data-stu-id="3499a-190">Step 3: Disable Seamless SSO for each AD forest that it was set it up on</span></span>

1. <span data-ttu-id="3499a-191">呼叫 `$creds = Get-Credential`。</span><span class="sxs-lookup"><span data-stu-id="3499a-191">Call `$creds = Get-Credential`.</span></span> <span data-ttu-id="3499a-192">出現提示時，輸入預定 Azure AD 樹系的網域系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="3499a-192">When prompted, enter the Domain Administrator credentials for the intended AD forest.</span></span>
2. <span data-ttu-id="3499a-193">呼叫 `Disable-AzureADSSOForest -OnPremCredentials $creds`。</span><span class="sxs-lookup"><span data-stu-id="3499a-193">Call `Disable-AzureADSSOForest -OnPremCredentials $creds`.</span></span> <span data-ttu-id="3499a-194">此命令會從此特定 AD 樹系的內部部署網域控制站中移除 `AZUREADSSOACCT` 電腦帳戶。</span><span class="sxs-lookup"><span data-stu-id="3499a-194">This command removes the `AZUREADSSOACCT` computer account from the on-premises Domain Controller for this specific AD forest.</span></span>
3. <span data-ttu-id="3499a-195">針對您已設定此功能的每個 AD 樹系，重複上述步驟。</span><span class="sxs-lookup"><span data-stu-id="3499a-195">Repeat the preceding steps for each AD forest that you’ve set up the feature on.</span></span>

### <a name="step-4-enable-seamless-sso-for-each-ad-forest"></a><span data-ttu-id="3499a-196">步驟 4：為每個 AD 樹系啟用無縫 SSO</span><span class="sxs-lookup"><span data-stu-id="3499a-196">Step 4: Enable Seamless SSO for each AD forest</span></span>

1. <span data-ttu-id="3499a-197">呼叫 `Enable-AzureADSSOForest`。</span><span class="sxs-lookup"><span data-stu-id="3499a-197">Call `Enable-AzureADSSOForest`.</span></span> <span data-ttu-id="3499a-198">出現提示時，輸入預定 Azure AD 樹系的網域系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="3499a-198">When prompted, enter the Domain Administrator credentials for the intended AD forest.</span></span>
2. <span data-ttu-id="3499a-199">針對您想要設定此功能的每個 AD 樹系，重複上述步驟。</span><span class="sxs-lookup"><span data-stu-id="3499a-199">Repeat the preceding steps for each AD forest that you want to set up the feature on.</span></span>

### <a name="step-5-enable-the-feature-on-your-tenant"></a><span data-ttu-id="3499a-200">步驟 5。</span><span class="sxs-lookup"><span data-stu-id="3499a-200">Step 5.</span></span> <span data-ttu-id="3499a-201">啟用租用戶上的功能</span><span class="sxs-lookup"><span data-stu-id="3499a-201">Enable the feature on your tenant</span></span>

<span data-ttu-id="3499a-202">呼叫 `Enable-AzureADSSO` 並且在 `Enable: ` 提示字元鍵入 "true"，以在租用戶中開啟該功能。</span><span class="sxs-lookup"><span data-stu-id="3499a-202">Call `Enable-AzureADSSO` and type in "true" at the `Enable: ` prompt to turn on the feature in your tenant.</span></span>
