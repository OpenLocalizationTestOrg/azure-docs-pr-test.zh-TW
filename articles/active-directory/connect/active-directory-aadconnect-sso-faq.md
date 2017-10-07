---
title: "Azure AD Connect：無縫單一登入 - 常見問題集 | Microsoft Docs"
description: "關於 Azure Active Directory 無縫式單一登入的常見問題的解答 toofrequently。"
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
ms.openlocfilehash: e91e7950670633c08c180ece873f7451fa19eef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-frequently-asked-questions"></a><span data-ttu-id="66baf-104">Azure Active Directory 無縫單一登入：常見問題集</span><span class="sxs-lookup"><span data-stu-id="66baf-104">Azure Active Directory Seamless Single Sign-On: Frequently asked questions</span></span>

<span data-ttu-id="66baf-105">本文將會解決 Azure Active Directory 無縫單一登入 (無縫 SSO) 的常見問題。</span><span class="sxs-lookup"><span data-stu-id="66baf-105">In this article, we address frequently asked questions about Azure Active Directory Seamless Single Sign-On (Seamless SSO).</span></span> <span data-ttu-id="66baf-106">請隨時回來查看新內容。</span><span class="sxs-lookup"><span data-stu-id="66baf-106">Keep checking back for new content.</span></span>

>[!IMPORTANT]
><span data-ttu-id="66baf-107">hello 無縫式 SSO 的功能目前為預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="66baf-107">hello Seamless SSO feature is currently in preview.</span></span>

## <a name="what-sign-in-methods-do-seamless-sso-work-with"></a><span data-ttu-id="66baf-108">無縫 SSO 與哪些登入方法搭配運作？</span><span class="sxs-lookup"><span data-stu-id="66baf-108">What sign-in methods do Seamless SSO work with?</span></span>

<span data-ttu-id="66baf-109">無縫式 SSO 可以結合其中一個 hello[密碼雜湊同步處理](active-directory-aadconnectsync-implement-password-synchronization.md)或[傳遞驗證](active-directory-aadconnect-pass-through-authentication.md)登入方法。</span><span class="sxs-lookup"><span data-stu-id="66baf-109">Seamless SSO can be combined with either hello [Password Hash Synchronization](active-directory-aadconnectsync-implement-password-synchronization.md) or [Pass-through Authentication](active-directory-aadconnect-pass-through-authentication.md) sign-in methods.</span></span> <span data-ttu-id="66baf-110">然而，此功能無法搭配 Active Directory Federation Services (ADFS) 使用。</span><span class="sxs-lookup"><span data-stu-id="66baf-110">However this feature cannot be used with Active Directory Federation Services (ADFS).</span></span>

## <a name="is-seamless-sso-a-free-feature"></a><span data-ttu-id="66baf-111">無縫 SSO 是免費功能嗎？</span><span class="sxs-lookup"><span data-stu-id="66baf-111">Is Seamless SSO a free feature?</span></span>

<span data-ttu-id="66baf-112">無縫式 SSO 是可用的功能，您不需要任何付費的版本的 Azure AD toouse 它。</span><span class="sxs-lookup"><span data-stu-id="66baf-112">Seamless SSO is a free feature and you don't need any paid editions of Azure AD toouse it.</span></span> <span data-ttu-id="66baf-113">Hello 功能正式運作時，則仍會保持可用。</span><span class="sxs-lookup"><span data-stu-id="66baf-113">It remains free when hello feature reaches general availability.</span></span>

## <a name="what-applications-take-advantage-of-domainhint-or-loginhint-parameter-capability-of-seamless-sso"></a><span data-ttu-id="66baf-114">哪些應用程式利用無縫 SSO 的 `domain_hint` 或 `login_hint` 參數功能？</span><span class="sxs-lookup"><span data-stu-id="66baf-114">What applications take advantage of `domain_hint` or `login_hint` parameter capability of Seamless SSO?</span></span>

<span data-ttu-id="66baf-115">我們很 hello 處理序編譯的應用程式傳送這些參數與 hello 的不 hello 清單中。</span><span class="sxs-lookup"><span data-stu-id="66baf-115">We are in hello process of compiling hello list of applications that send these parameters and hello ones that don't.</span></span> <span data-ttu-id="66baf-116">如果您有興趣的應用程式，讓我們知道 hello 註解區段中。</span><span class="sxs-lookup"><span data-stu-id="66baf-116">If you have applications that are interested in, let us know in hello comments section.</span></span>

## <a name="does-seamless-sso-support-alternate-id-as-hello-username-instead-of-userprincipalname"></a><span data-ttu-id="66baf-117">並無縫式 SSO 支援`Alternate ID`hello 使用者名稱，而不是因為`userPrincipalName`嗎？</span><span class="sxs-lookup"><span data-stu-id="66baf-117">Does Seamless SSO support `Alternate ID` as hello username, instead of `userPrincipalName`?</span></span>

<span data-ttu-id="66baf-118">是。</span><span class="sxs-lookup"><span data-stu-id="66baf-118">Yes.</span></span> <span data-ttu-id="66baf-119">無縫式 SSO 支援`Alternate ID`hello 使用者名稱所示，在 Azure AD Connect 中設定時為[這裡](active-directory-aadconnect-get-started-custom.md)。</span><span class="sxs-lookup"><span data-stu-id="66baf-119">Seamless SSO supports `Alternate ID` as hello username when configured in Azure AD Connect as shown [here](active-directory-aadconnect-get-started-custom.md).</span></span> <span data-ttu-id="66baf-120">並非所有 Office 365 應用程式都支援 `Alternate ID`。</span><span class="sxs-lookup"><span data-stu-id="66baf-120">Not all Office 365 applications support `Alternate ID`.</span></span> <span data-ttu-id="66baf-121">Hello 支援陳述式，請參閱 toohello 特定應用程式的文件。</span><span class="sxs-lookup"><span data-stu-id="66baf-121">Refer toohello specific application's documentation for hello support statement.</span></span>

## <a name="i-want-tooregister-non-windows-10-devices-with-azure-ad-without-using-ad-fs-can-i-use-seamless-sso-instead"></a><span data-ttu-id="66baf-122">我想 tooregister 非 Windows 10 裝置與 Azure AD，而不需要使用 AD FS。</span><span class="sxs-lookup"><span data-stu-id="66baf-122">I want tooregister non-Windows 10 devices with Azure AD, without using AD FS.</span></span> <span data-ttu-id="66baf-123">我可以改為使用無縫 SSO 嗎？</span><span class="sxs-lookup"><span data-stu-id="66baf-123">Can I use Seamless SSO instead?</span></span>

<span data-ttu-id="66baf-124">是，這種情況下需要版本 2.1 或更新版本的 hello[工作地方聯結用戶端](https://www.microsoft.com/download/details.aspx?id=53554)。</span><span class="sxs-lookup"><span data-stu-id="66baf-124">Yes, this scenario needs version 2.1 or later of hello [workplace-join client](https://www.microsoft.com/download/details.aspx?id=53554).</span></span>

## <a name="how-can-i-roll-over-hello-kerberos-decryption-key-of-hello-azureadssoacct-computer-account"></a><span data-ttu-id="66baf-125">如何可以我變換 hello Kerberos 解密金鑰的 hello`AZUREADSSOACCT`電腦帳戶？</span><span class="sxs-lookup"><span data-stu-id="66baf-125">How can I roll over hello Kerberos decryption key of hello `AZUREADSSOACCT` computer account?</span></span>

<span data-ttu-id="66baf-126">請務必 toofrequently 變換 hello Kerberos 解密金鑰的 hello`AZUREADSSOACCT`電腦帳戶 （這表示 Azure AD） 建立在您內部部署 AD 樹系。</span><span class="sxs-lookup"><span data-stu-id="66baf-126">It is important toofrequently roll over hello Kerberos decryption key of hello `AZUREADSSOACCT` computer account (which represents Azure AD) created in your on-premises AD forest.</span></span>

>[!IMPORTANT]
><span data-ttu-id="66baf-127">我們強烈建議您，您會彙總 hello Kerberos 解密金鑰至少每隔 30 天。</span><span class="sxs-lookup"><span data-stu-id="66baf-127">We highly recommend that you roll over hello Kerberos decryption key at least every 30 days.</span></span>

<span data-ttu-id="66baf-128">執行 Azure AD Connect 的情況下遵循 hello 在內部部署伺服器上的下列步驟：</span><span class="sxs-lookup"><span data-stu-id="66baf-128">Follow these steps on hello on-premises server where you are running Azure AD Connect:</span></span>

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a><span data-ttu-id="66baf-129">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="66baf-129">Step 1.</span></span> <span data-ttu-id="66baf-130">取得已啟用無縫 SSO 的 AD 樹系清單</span><span class="sxs-lookup"><span data-stu-id="66baf-130">Get list of AD forests where Seamless SSO has been enabled</span></span>

1. <span data-ttu-id="66baf-131">首先，下載並安裝 hello [Microsoft Online Services 登入小幫手](http://go.microsoft.com/fwlink/?LinkID=286152)。</span><span class="sxs-lookup"><span data-stu-id="66baf-131">First, download, and install hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span>
2. <span data-ttu-id="66baf-132">請下載並安裝 hello [64 位元 Windows PowerShell 的 Azure Active Directory 模組](http://go.microsoft.com/fwlink/p/?linkid=236297)。</span><span class="sxs-lookup"><span data-stu-id="66baf-132">Then download and install hello [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>
3. <span data-ttu-id="66baf-133">瀏覽 toohello`%programfiles%\Microsoft Azure Active Directory Connect`資料夾。</span><span class="sxs-lookup"><span data-stu-id="66baf-133">Navigate toohello `%programfiles%\Microsoft Azure Active Directory Connect` folder.</span></span>
4. <span data-ttu-id="66baf-134">使用這個命令匯入 hello 無縫式 SSO 的 PowerShell 模組： `Import-Module .\AzureADSSO.psd1`。</span><span class="sxs-lookup"><span data-stu-id="66baf-134">Import hello Seamless SSO PowerShell module using this command: `Import-Module .\AzureADSSO.psd1`.</span></span>
5. <span data-ttu-id="66baf-135">以系統管理員身分執行 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="66baf-135">Run PowerShell as an Administrator.</span></span> <span data-ttu-id="66baf-136">在 PowerShell 中，呼叫 `New-AzureADSSOAuthenticationContext`。</span><span class="sxs-lookup"><span data-stu-id="66baf-136">In PowerShell, call `New-AzureADSSOAuthenticationContext`.</span></span> <span data-ttu-id="66baf-137">此命令應該提供快顯 tooenter 租用戶的全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="66baf-137">This command should give you a popup tooenter your tenant's Global Administrator credentials.</span></span>
6. <span data-ttu-id="66baf-138">呼叫 `Get-AzureADSSOStatus`。</span><span class="sxs-lookup"><span data-stu-id="66baf-138">Call `Get-AzureADSSOStatus`.</span></span> <span data-ttu-id="66baf-139">這個命令會提供您在已啟用這項功能的 hello AD 樹系 （查看 hello 「 網域 」 清單） 的清單。</span><span class="sxs-lookup"><span data-stu-id="66baf-139">This command provides you hello list of AD forests (look at hello "Domains" list) on which this feature has been enabled.</span></span>

### <a name="step-2-update-hello-kerberos-decryption-key-on-each-ad-forest-that-it-was-set-it-up-on"></a><span data-ttu-id="66baf-140">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="66baf-140">Step 2.</span></span> <span data-ttu-id="66baf-141">更新上設定它在每個 AD 樹系的 hello Kerberos 解密金鑰</span><span class="sxs-lookup"><span data-stu-id="66baf-141">Update hello Kerberos decryption key on each AD forest that it was set it up on</span></span>

1. <span data-ttu-id="66baf-142">呼叫 `$creds = Get-Credential`。</span><span class="sxs-lookup"><span data-stu-id="66baf-142">Call `$creds = Get-Credential`.</span></span> <span data-ttu-id="66baf-143">出現提示時，輸入 hello 適合 AD 樹系 hello 網域系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="66baf-143">When prompted, enter hello Domain Administrator credentials for hello intended AD forest.</span></span>
2. <span data-ttu-id="66baf-144">呼叫 `Update-AzureADSSOForest -OnPremCredentials $creds`。</span><span class="sxs-lookup"><span data-stu-id="66baf-144">Call `Update-AzureADSSOForest -OnPremCredentials $creds`.</span></span> <span data-ttu-id="66baf-145">此命令更新 hello hello Kerberos 的解密金鑰`AZUREADSSOACCT`這個特定的 AD 樹系中的電腦帳戶在 Azure AD 中更新它。</span><span class="sxs-lookup"><span data-stu-id="66baf-145">This command updates hello Kerberos decryption key for hello `AZUREADSSOACCT` computer account in this specific AD forest and updates it in Azure AD.</span></span>
3. <span data-ttu-id="66baf-146">重複上述步驟設定好 hello 功能每個 AD 樹系的 hello。</span><span class="sxs-lookup"><span data-stu-id="66baf-146">Repeat hello preceding steps for each AD forest that you’ve set up hello feature on.</span></span>

>[!IMPORTANT]
><span data-ttu-id="66baf-147">請確定您_不_執行 hello`Update-AzureADSSOForest`命令一次以上。</span><span class="sxs-lookup"><span data-stu-id="66baf-147">Ensure that you _don't_ run hello `Update-AzureADSSOForest` command more than once.</span></span> <span data-ttu-id="66baf-148">否則，hello 功能會停止運作，直到 hello 時間過期，而且會重新發出您在內部部署 Active directory 使用者的 Kerberos 票證。</span><span class="sxs-lookup"><span data-stu-id="66baf-148">Otherwise, hello feature stops working until hello time your users' Kerberos tickets expire and are reissued by your on-premises Active Directory.</span></span>

## <a name="how-can-i-disable-seamless-sso"></a><span data-ttu-id="66baf-149">如何停用無縫 SSO？</span><span class="sxs-lookup"><span data-stu-id="66baf-149">How can I disable Seamless SSO?</span></span>

<span data-ttu-id="66baf-150">您可以使用 Azure AD Connect 停用無縫 SSO。</span><span class="sxs-lookup"><span data-stu-id="66baf-150">Seamless SSO can be disabled using Azure AD Connect.</span></span>

<span data-ttu-id="66baf-151">執行 Azure AD Connect，選擇 [變更使用者登入頁面]，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="66baf-151">Run Azure AD Connect, choose "Change user sign-in page" and click "Next".</span></span> <span data-ttu-id="66baf-152">然後取消核取 hello 」 啟用單一登入 」 選項。</span><span class="sxs-lookup"><span data-stu-id="66baf-152">Then uncheck hello "Enable single sign on" option.</span></span> <span data-ttu-id="66baf-153">繼續完成 hello 精靈。</span><span class="sxs-lookup"><span data-stu-id="66baf-153">Continue through hello wizard.</span></span> <span data-ttu-id="66baf-154">完成之後 hello 精靈，無縫式 SSO 會停用您的租用戶。</span><span class="sxs-lookup"><span data-stu-id="66baf-154">After completion of hello wizard, Seamless SSO is disabled on your tenant.</span></span>

<span data-ttu-id="66baf-155">但是，您會在畫面上看到一個包含以下內容的訊息：</span><span class="sxs-lookup"><span data-stu-id="66baf-155">However, you see a message on screen that reads as follows:</span></span>

<span data-ttu-id="66baf-156">「 單一登入現已停用，但有額外的手動步驟 tooperform 順序 toocomplete 清除中。</span><span class="sxs-lookup"><span data-stu-id="66baf-156">"Single sign-on is now disabled, but there are additional manual steps tooperform in order toocomplete clean-up.</span></span> <span data-ttu-id="66baf-157">深入了解」</span><span class="sxs-lookup"><span data-stu-id="66baf-157">Learn more"</span></span>

<span data-ttu-id="66baf-158">toocomplete hello 程序，請執行下列手動步驟 hello 在內部部署伺服器上的執行 Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="66baf-158">toocomplete hello process, follow these manual steps on hello on-premises server where you are running Azure AD Connect:</span></span>

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a><span data-ttu-id="66baf-159">步驟 1.</span><span class="sxs-lookup"><span data-stu-id="66baf-159">Step 1.</span></span> <span data-ttu-id="66baf-160">取得已啟用無縫 SSO 的 AD 樹系清單</span><span class="sxs-lookup"><span data-stu-id="66baf-160">Get list of AD forests where Seamless SSO has been enabled</span></span>

1. <span data-ttu-id="66baf-161">首先，下載並安裝 hello [Microsoft Online Services 登入小幫手](http://go.microsoft.com/fwlink/?LinkID=286152)。</span><span class="sxs-lookup"><span data-stu-id="66baf-161">First, download, and install hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span>
2. <span data-ttu-id="66baf-162">請下載並安裝 hello [64 位元 Windows PowerShell 的 Azure Active Directory 模組](http://go.microsoft.com/fwlink/p/?linkid=236297)。</span><span class="sxs-lookup"><span data-stu-id="66baf-162">Then download and install hello [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>
3. <span data-ttu-id="66baf-163">瀏覽 toohello`%programfiles%\Microsoft Azure Active Directory Connect`資料夾。</span><span class="sxs-lookup"><span data-stu-id="66baf-163">Navigate toohello `%programfiles%\Microsoft Azure Active Directory Connect` folder.</span></span>
4. <span data-ttu-id="66baf-164">使用這個命令匯入 hello 無縫式 SSO 的 PowerShell 模組： `Import-Module .\AzureADSSO.psd1`。</span><span class="sxs-lookup"><span data-stu-id="66baf-164">Import hello Seamless SSO PowerShell module using this command: `Import-Module .\AzureADSSO.psd1`.</span></span>
5. <span data-ttu-id="66baf-165">以系統管理員身分執行 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="66baf-165">Run PowerShell as an Administrator.</span></span> <span data-ttu-id="66baf-166">在 PowerShell 中，呼叫 `New-AzureADSSOAuthenticationContext`。</span><span class="sxs-lookup"><span data-stu-id="66baf-166">In PowerShell, call `New-AzureADSSOAuthenticationContext`.</span></span> <span data-ttu-id="66baf-167">此命令應該提供快顯 tooenter 租用戶的全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="66baf-167">This command should give you a popup tooenter your tenant's Global Administrator credentials.</span></span>
6. <span data-ttu-id="66baf-168">呼叫 `Get-AzureADSSOStatus`。</span><span class="sxs-lookup"><span data-stu-id="66baf-168">Call `Get-AzureADSSOStatus`.</span></span> <span data-ttu-id="66baf-169">這個命令會提供您在已啟用這項功能的 hello AD 樹系 （查看 hello 「 網域 」 清單） 的清單。</span><span class="sxs-lookup"><span data-stu-id="66baf-169">This command provides you hello list of AD forests (look at hello "Domains" list) on which this feature has been enabled.</span></span>

### <a name="step-2-manually-delete-hello-azureadssoacct-computer-account-from-each-ad-forest-that-you-see-listed"></a><span data-ttu-id="66baf-170">步驟 2.</span><span class="sxs-lookup"><span data-stu-id="66baf-170">Step 2.</span></span> <span data-ttu-id="66baf-171">手動刪除 hello`AZUREADSSOACCT`從您看到列出每個 AD 樹系的電腦帳戶。</span><span class="sxs-lookup"><span data-stu-id="66baf-171">Manually delete hello `AZUREADSSOACCT` computer account from each AD forest that you see listed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66baf-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="66baf-172">Next steps</span></span>

- <span data-ttu-id="66baf-173">[**快速入門**](active-directory-aadconnect-sso-quick-start.md) - 開始使用 Azure AD 無縫 SSO。</span><span class="sxs-lookup"><span data-stu-id="66baf-173">[**Quick Start**](active-directory-aadconnect-sso-quick-start.md) - Get up and running Azure AD Seamless SSO.</span></span>
- <span data-ttu-id="66baf-174">[**技術性深入探討**](active-directory-aadconnect-sso-how-it-works.md) - 了解這項功能的運作方式。</span><span class="sxs-lookup"><span data-stu-id="66baf-174">[**Technical Deep Dive**](active-directory-aadconnect-sso-how-it-works.md) - Understand how this feature works.</span></span>
- <span data-ttu-id="66baf-175">[**疑難排解**](active-directory-aadconnect-troubleshoot-sso.md) -了解如何 tooresolve 常見問題與 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="66baf-175">[**Troubleshoot**](active-directory-aadconnect-troubleshoot-sso.md) - Learn how tooresolve common issues with hello feature.</span></span>
- <span data-ttu-id="66baf-176">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - 用於提出新的功能要求。</span><span class="sxs-lookup"><span data-stu-id="66baf-176">[**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect) - For filing new feature requests.</span></span>
