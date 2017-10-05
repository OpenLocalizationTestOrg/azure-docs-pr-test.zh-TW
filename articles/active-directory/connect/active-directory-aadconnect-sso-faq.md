---
title: "Azure AD Connect：無縫單一登入 - 常見問題集 | Microsoft Docs"
description: "Azure Active Directory 無縫單一登入常見問題集的答案。"
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
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: 518b2719f24be96dffba3458f6c15e65f16b7e0d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-frequently-asked-questions"></a><span data-ttu-id="2b2aa-104">Azure Active Directory 無縫單一登入：常見問題集</span><span class="sxs-lookup"><span data-stu-id="2b2aa-104">Azure Active Directory Seamless Single Sign-On: Frequently asked questions</span></span>

<span data-ttu-id="2b2aa-105">本文將會解決 Azure Active Directory 無縫單一登入 (無縫 SSO) 的常見問題。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-105">In this article, we address frequently asked questions about Azure Active Directory Seamless Single Sign-On (Seamless SSO).</span></span> <span data-ttu-id="2b2aa-106">請隨時回來查看新內容。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-106">Keep checking back for new content.</span></span>

>[!IMPORTANT]
><span data-ttu-id="2b2aa-107">無縫 SSO 功能目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-107">The Seamless SSO feature is currently in preview.</span></span>

## <a name="what-sign-in-methods-do-seamless-sso-work-with"></a><span data-ttu-id="2b2aa-108">無縫 SSO 與哪些登入方法搭配運作？</span><span class="sxs-lookup"><span data-stu-id="2b2aa-108">What sign-in methods do Seamless SSO work with?</span></span>

<span data-ttu-id="2b2aa-109">無縫 SSO 可以與[密碼雜湊同步處理](active-directory-aadconnectsync-implement-password-synchronization.md)或[傳遞驗證](active-directory-aadconnect-pass-through-authentication.md)登入方法合併使用。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-109">Seamless SSO can be combined with either the [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) or [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) sign-in methods.</span></span> <span data-ttu-id="2b2aa-110">然而，此功能無法搭配 Active Directory Federation Services (ADFS) 使用。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-110">However this feature cannot be used with Active Directory Federation Services (ADFS).</span></span>

## <a name="is-seamless-sso-a-free-feature"></a><span data-ttu-id="2b2aa-111">無縫 SSO 是免費功能嗎？</span><span class="sxs-lookup"><span data-stu-id="2b2aa-111">Is Seamless SSO a free feature?</span></span>

<span data-ttu-id="2b2aa-112">無縫 SSO 是免費功能，您不需要任何付費的 Azure AD 版本即可使用。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-112">Seamless SSO is a free feature and you don't need any paid editions of Azure AD to use it.</span></span> <span data-ttu-id="2b2aa-113">功能正式運作時，它仍然免費。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-113">It remains free when the feature reaches general availability.</span></span>

## <a name="what-applications-take-advantage-of-domainhint-or-loginhint-parameter-capability-of-seamless-sso"></a><span data-ttu-id="2b2aa-114">哪些應用程式利用無縫 SSO 的 `domain_hint` 或 `login_hint` 參數功能？</span><span class="sxs-lookup"><span data-stu-id="2b2aa-114">What applications take advantage of `domain_hint` or `login_hint` parameter capability of Seamless SSO?</span></span>

<span data-ttu-id="2b2aa-115">我們正在編譯可傳送這些參數以及未傳送這些參數的應用程式清單。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-115">We are in the process of compiling the list of applications that send these parameters and the ones that don't.</span></span> <span data-ttu-id="2b2aa-116">如果您有感興趣的應用程式，請在 comments 區段中讓我們知道。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-116">If you have applications that are interested in, let us know in the comments section.</span></span>

## <a name="does-seamless-sso-support-alternate-id-as-the-username-instead-of-userprincipalname"></a><span data-ttu-id="2b2aa-117">無縫 SSO 支援 `Alternate ID` 作為使用者名稱，而不是 `userPrincipalName`？</span><span class="sxs-lookup"><span data-stu-id="2b2aa-117">Does Seamless SSO support `Alternate ID` as the username, instead of `userPrincipalName`?</span></span>

<span data-ttu-id="2b2aa-118">是。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-118">Yes.</span></span> <span data-ttu-id="2b2aa-119">如[這裡](active-directory-aadconnect-get-started-custom.md)所述設定於 Azure AD Connect 時，無縫 SSO 支援 `Alternate ID` 作為使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-119">Seamless SSO supports `Alternate ID` as the username when configured in Azure AD Connect as shown [here](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="2b2aa-120">並非所有 Office 365 應用程式都支援 `Alternate ID`。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-120">Not all Office 365 applications support `Alternate ID`.</span></span> <span data-ttu-id="2b2aa-121">請參閱支援陳述式的特定應用程式文件。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-121">Refer to the specific application's documentation for the support statement.</span></span>

## <a name="i-want-to-register-non-windows-10-devices-with-azure-ad-without-using-ad-fs-can-i-use-seamless-sso-instead"></a><span data-ttu-id="2b2aa-122">我想要使用 Azure AD 註冊非 Windows 10 裝置，而不需要使用 AD FS。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-122">I want to register non-Windows 10 devices with Azure AD, without using AD FS.</span></span> <span data-ttu-id="2b2aa-123">我可以改為使用無縫 SSO 嗎？</span><span class="sxs-lookup"><span data-stu-id="2b2aa-123">Can I use Seamless SSO instead?</span></span>

<span data-ttu-id="2b2aa-124">是，此案例需要 2.1 版或更新版本的[加入工作場所用戶端](https://www.microsoft.com/download/details.aspx?id=53554)。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-124">Yes, this scenario needs version 2.1 or later of the [workplace-join client](https://www.microsoft.com/download/details.aspx?id=53554).</span></span>

## <a name="how-can-i-roll-over-the-kerberos-decryption-key-of-the-azureadssoacct-computer-account"></a><span data-ttu-id="2b2aa-125">如何才能變換 `AZUREADSSOACCT` 電腦帳戶的 Kerberos 解密金鑰？</span><span class="sxs-lookup"><span data-stu-id="2b2aa-125">How can I roll over the Kerberos decryption key of the `AZUREADSSOACCT` computer account?</span></span>

<span data-ttu-id="2b2aa-126">請務必經常變換在內部部署 AD 樹系中建立之 `AZUREADSSOACCT` 電腦帳戶 (這表示 Azure AD) 的 Kerberos 解密金鑰。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-126">It is important to frequently roll over the Kerberos decryption key of the `AZUREADSSOACCT` computer account (which represents Azure AD) created in your on-premises AD forest.</span></span>

>[!IMPORTANT]
><span data-ttu-id="2b2aa-127">強烈建議您至少每隔 30 天變換一次 Kerberos 解密金鑰。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-127">We highly recommend that you roll over the Kerberos decryption key at least every 30 days.</span></span>

<span data-ttu-id="2b2aa-128">請在執行 Azure AD Connect 的內部部署伺服器上依照下列步驟操作：</span><span class="sxs-lookup"><span data-stu-id="2b2aa-128">Follow these steps on the on-premises server where you are running Azure AD Connect:</span></span>

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a><span data-ttu-id="2b2aa-129">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="2b2aa-129">Step 1.</span></span> <span data-ttu-id="2b2aa-130">取得已啟用無縫 SSO 的 AD 樹系清單</span><span class="sxs-lookup"><span data-stu-id="2b2aa-130">Get list of AD forests where Seamless SSO has been enabled</span></span>

1. <span data-ttu-id="2b2aa-131">首先，下載並安裝 [Microsoft Online Services 登入小幫手](http://go.microsoft.com/fwlink/?LinkID=286152)。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-131">First, download, and install the [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span>
2. <span data-ttu-id="2b2aa-132">接著下載並安裝 [適用於 Windows PowerShell 的 64 位元 Azure Active Directory 模組](http://go.microsoft.com/fwlink/p/?linkid=236297)。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-132">Then download and install the [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>
3. <span data-ttu-id="2b2aa-133">瀏覽到 `%programfiles%\Microsoft Azure Active Directory Connect` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-133">Navigate to the `%programfiles%\Microsoft Azure Active Directory Connect` folder.</span></span>
4. <span data-ttu-id="2b2aa-134">使用此命令匯入順暢 SSO PowerShell 模組：`Import-Module .\AzureADSSO.psd1`。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-134">Import the Seamless SSO PowerShell module using this command: `Import-Module .\AzureADSSO.psd1`.</span></span>
5. <span data-ttu-id="2b2aa-135">以系統管理員身分執行 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-135">Run PowerShell as an Administrator.</span></span> <span data-ttu-id="2b2aa-136">在 PowerShell 中，呼叫 `New-AzureADSSOAuthenticationContext`。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-136">In PowerShell, call `New-AzureADSSOAuthenticationContext`.</span></span> <span data-ttu-id="2b2aa-137">此命令應提供一個快顯視窗，以便輸入租用戶的全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-137">This command should give you a popup to enter your tenant's Global Administrator credentials.</span></span>
6. <span data-ttu-id="2b2aa-138">呼叫 `Get-AzureADSSOStatus`。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-138">Call `Get-AzureADSSOStatus`.</span></span> <span data-ttu-id="2b2aa-139">此命令會提供已啟用這項功能的 AD 樹系清單 (查看 [網域] 清單)。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-139">This command provides you the list of AD forests (look at the "Domains" list) on which this feature has been enabled.</span></span>

### <a name="step-2-update-the-kerberos-decryption-key-on-each-ad-forest-that-it-was-set-it-up-on"></a><span data-ttu-id="2b2aa-140">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="2b2aa-140">Step 2.</span></span> <span data-ttu-id="2b2aa-141">在已設定 Kerberos 解密金鑰的每個 AD 樹系上更新該金鑰</span><span class="sxs-lookup"><span data-stu-id="2b2aa-141">Update the Kerberos decryption key on each AD forest that it was set it up on</span></span>

1. <span data-ttu-id="2b2aa-142">呼叫 `$creds = Get-Credential`。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-142">Call `$creds = Get-Credential`.</span></span> <span data-ttu-id="2b2aa-143">出現提示時，輸入預定 Azure AD 樹系的網域系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-143">When prompted, enter the Domain Administrator credentials for the intended AD forest.</span></span>
2. <span data-ttu-id="2b2aa-144">呼叫 `Update-AzureADSSOForest -OnPremCredentials $creds`。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-144">Call `Update-AzureADSSOForest -OnPremCredentials $creds`.</span></span> <span data-ttu-id="2b2aa-145">此命令會更新此特定 AD 樹系中 `AZUREADSSOACCT` 電腦帳戶的 Kerberos 解密金鑰，並且在 Azure AD 中更新它。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-145">This command updates the Kerberos decryption key for the `AZUREADSSOACCT` computer account in this specific AD forest and updates it in Azure AD.</span></span>
3. <span data-ttu-id="2b2aa-146">針對您已設定此功能的每個 AD 樹系，重複上述步驟。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-146">Repeat the preceding steps for each AD forest that you’ve set up the feature on.</span></span>

>[!IMPORTANT]
><span data-ttu-id="2b2aa-147">確定您「並未」執行 `Update-AzureADSSOForest` 命令一次以上。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-147">Ensure that you _don't_ run the `Update-AzureADSSOForest` command more than once.</span></span> <span data-ttu-id="2b2aa-148">否則，此功能會停止運作，直到使用者的 Kerberos 票證過期並由您的內部部署 Active Directory 重新發出為止。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-148">Otherwise, the feature stops working until the time your users' Kerberos tickets expire and are reissued by your on-premises Active Directory.</span></span>

## <a name="how-can-i-disable-seamless-sso"></a><span data-ttu-id="2b2aa-149">如何停用無縫 SSO？</span><span class="sxs-lookup"><span data-stu-id="2b2aa-149">How can I disable Seamless SSO?</span></span>

<span data-ttu-id="2b2aa-150">您可以使用 Azure AD Connect 停用無縫 SSO。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-150">Seamless SSO can be disabled using Azure AD Connect.</span></span>

<span data-ttu-id="2b2aa-151">執行 Azure AD Connect，選擇 [變更使用者登入頁面]，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-151">Run Azure AD Connect, choose "Change user sign-in page" and click "Next".</span></span> <span data-ttu-id="2b2aa-152">然後取消選取 [啟用單一登入] 選項。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-152">Then uncheck the "Enable single sign on" option.</span></span> <span data-ttu-id="2b2aa-153">繼續執行精靈。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-153">Continue through the wizard.</span></span> <span data-ttu-id="2b2aa-154">完成精靈之後，無縫 SSO 就會在您的租用戶上停用。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-154">After completion of the wizard, Seamless SSO is disabled on your tenant.</span></span>

<span data-ttu-id="2b2aa-155">但是，您會在畫面上看到一個包含以下內容的訊息：</span><span class="sxs-lookup"><span data-stu-id="2b2aa-155">However, you see a message on screen that reads as follows:</span></span>

<span data-ttu-id="2b2aa-156">「單一登入現已停用，但還要執行其他手動步驟才可完成清理。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-156">"Single sign-on is now disabled, but there are additional manual steps to perform in order to complete clean-up.</span></span> <span data-ttu-id="2b2aa-157">深入了解」</span><span class="sxs-lookup"><span data-stu-id="2b2aa-157">Learn more"</span></span>

<span data-ttu-id="2b2aa-158">若要完成此程序，請在執行 Azure AD Connect 的內部部署伺服器上依照下列手動步驟操作：</span><span class="sxs-lookup"><span data-stu-id="2b2aa-158">To complete the process, follow these manual steps on the on-premises server where you are running Azure AD Connect:</span></span>

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a><span data-ttu-id="2b2aa-159">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="2b2aa-159">Step 1.</span></span> <span data-ttu-id="2b2aa-160">取得已啟用無縫 SSO 的 AD 樹系清單</span><span class="sxs-lookup"><span data-stu-id="2b2aa-160">Get list of AD forests where Seamless SSO has been enabled</span></span>

1. <span data-ttu-id="2b2aa-161">首先，下載並安裝 [Microsoft Online Services 登入小幫手](http://go.microsoft.com/fwlink/?LinkID=286152)。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-161">First, download, and install the [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span>
2. <span data-ttu-id="2b2aa-162">接著下載並安裝 [適用於 Windows PowerShell 的 64 位元 Azure Active Directory 模組](http://go.microsoft.com/fwlink/p/?linkid=236297)。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-162">Then download and install the [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>
3. <span data-ttu-id="2b2aa-163">瀏覽到 `%programfiles%\Microsoft Azure Active Directory Connect` 資料夾。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-163">Navigate to the `%programfiles%\Microsoft Azure Active Directory Connect` folder.</span></span>
4. <span data-ttu-id="2b2aa-164">使用此命令匯入順暢 SSO PowerShell 模組：`Import-Module .\AzureADSSO.psd1`。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-164">Import the Seamless SSO PowerShell module using this command: `Import-Module .\AzureADSSO.psd1`.</span></span>
5. <span data-ttu-id="2b2aa-165">以系統管理員身分執行 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-165">Run PowerShell as an Administrator.</span></span> <span data-ttu-id="2b2aa-166">在 PowerShell 中，呼叫 `New-AzureADSSOAuthenticationContext`。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-166">In PowerShell, call `New-AzureADSSOAuthenticationContext`.</span></span> <span data-ttu-id="2b2aa-167">此命令應提供一個快顯視窗，以便輸入租用戶的全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-167">This command should give you a popup to enter your tenant's Global Administrator credentials.</span></span>
6. <span data-ttu-id="2b2aa-168">呼叫 `Get-AzureADSSOStatus`。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-168">Call `Get-AzureADSSOStatus`.</span></span> <span data-ttu-id="2b2aa-169">此命令會提供已啟用這項功能的 AD 樹系清單 (查看 [網域] 清單)。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-169">This command provides you the list of AD forests (look at the "Domains" list) on which this feature has been enabled.</span></span>

### <a name="step-2-manually-delete-the-azureadssoacct-computer-account-from-each-ad-forest-that-you-see-listed"></a><span data-ttu-id="2b2aa-170">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="2b2aa-170">Step 2.</span></span> <span data-ttu-id="2b2aa-171">從您看到的每個列出 AD 樹系，手動刪除 `AZUREADSSOACCT` 電腦帳戶。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-171">Manually delete the `AZUREADSSOACCT` computer account from each AD forest that you see listed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2b2aa-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2b2aa-172">Next steps</span></span>

- <span data-ttu-id="2b2aa-173">[**快速入門**](active-directory-aadconnect-sso-quick-start.md) - 開始使用 Azure AD 無縫 SSO。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-173">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="2b2aa-174">[**技術性深入探討**](active-directory-aadconnect-sso-how-it-works.md) - 了解這項功能的運作方式。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-174">[**Technical Deep Dive**](active-directory-aadconnect-sso-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="2b2aa-175">[**疑難排解**](active-directory-aadconnect-troubleshoot-sso.md) - 了解如何解決此功能的常見問題。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-175">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how to resolve common issues with the feature.</span></span>
- <span data-ttu-id="2b2aa-176">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。</span><span class="sxs-lookup"><span data-stu-id="2b2aa-176">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
