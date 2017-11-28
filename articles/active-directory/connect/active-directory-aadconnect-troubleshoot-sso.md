---
title: "Azure AD Connect：針對無縫單一登入進行疑難排解 | Microsoft Docs"
description: "本主題描述如何 tootroubleshoot Azure Active Directory 無接縫單一登入 (Azure AD 無縫式 SSO)。"
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
ms.openlocfilehash: f1c1c11522f22d5bc742c126fff483c5b06e1f06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-active-directory-seamless-single-sign-on"></a><span data-ttu-id="63bd6-104">針對 Azure Active Directory 無縫單一登入進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="63bd6-104">Troubleshoot Azure Active Directory Seamless Single Sign-On</span></span>

<span data-ttu-id="63bd6-105">這篇文章可協助您尋找有關 Azure AD 無縫單一登入常見問題的疑難排解資訊。</span><span class="sxs-lookup"><span data-stu-id="63bd6-105">This article helps you find troubleshooting information about common issues regarding Azure AD Seamless Single Sign-On.</span></span>

## <a name="known-issues"></a><span data-ttu-id="63bd6-106">已知問題</span><span class="sxs-lookup"><span data-stu-id="63bd6-106">Known issues</span></span>

- <span data-ttu-id="63bd6-107">如果您正在同步處理 30 個或更多的 AD 樹系，您無法使用 Azure AD Connect 啟用無縫 SSO。</span><span class="sxs-lookup"><span data-stu-id="63bd6-107">If you are synchronizing 30 or more AD forests, you can't enable Seamless SSO using Azure AD Connect.</span></span> <span data-ttu-id="63bd6-108">因應措施，您可以[手動啟用](#manual-reset-of-azure-ad-seamless-sso)hello 在租用戶的功能。</span><span class="sxs-lookup"><span data-stu-id="63bd6-108">As a workaround, you can [manually enable](#manual-reset-of-azure-ad-seamless-sso) hello feature on your tenant.</span></span>
- <span data-ttu-id="63bd6-109">加入 Azure AD 服務 Url （https://autologon.microsoftazuread-sso.com、 https://aadg.windows.net.nsatc.net） toohello 「 信任的網站 」 區域而不是 hello 「 近端內部網路 」 區域**封鎖使用者登入**。</span><span class="sxs-lookup"><span data-stu-id="63bd6-109">Adding Azure AD service URLs (https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net) toohello "Trusted sites" zone instead of hello "Local intranet" zone **blocks users from signing in**.</span></span>
- <span data-ttu-id="63bd6-110">無縫 SSO 無法在 Firefox 和 Edge 的私人瀏覽模式中運作。</span><span class="sxs-lookup"><span data-stu-id="63bd6-110">Seamless SSO doesn't work in private browsing mode on Firefox and Edge.</span></span> <span data-ttu-id="63bd6-111">此外當「增強保護」模式開啟時，Internet Explorer 也是如此。</span><span class="sxs-lookup"><span data-stu-id="63bd6-111">And also on Internet Explorer when Enhanced Protection mode is turned on.</span></span>

>[!IMPORTANT]
><span data-ttu-id="63bd6-112">我們最近回復的邊緣 tooinvestigate 支援客戶回報的問題。</span><span class="sxs-lookup"><span data-stu-id="63bd6-112">We recently rolled back support for Edge tooinvestigate customer-reported issues.</span></span>

## <a name="check-status-of-hello-feature"></a><span data-ttu-id="63bd6-113">Hello 功能的核取狀態</span><span class="sxs-lookup"><span data-stu-id="63bd6-113">Check status of hello feature</span></span>

<span data-ttu-id="63bd6-114">請確定該 hello 無縫式 SSO 的功能仍然是**啟用**在租用戶。</span><span class="sxs-lookup"><span data-stu-id="63bd6-114">Ensure that hello Seamless SSO feature is still **Enabled** on your tenant.</span></span> <span data-ttu-id="63bd6-115">您可以查看狀態移 toohello **Azure AD Connect**刀鋒視窗上 hello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="63bd6-115">You can check status by going toohello **Azure AD Connect** blade on hello [Azure Active Directory admin center](https://aad.portal.azure.com/).</span></span>

![Azure Active Directory 管理中心 - Azure AD Connect 刀鋒視窗](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="sign-in-failure-reasons-on-hello-azure-active-directory-admin-center"></a><span data-ttu-id="63bd6-117">登入失敗的原因，在 hello Azure Active Directory 系統管理中心</span><span class="sxs-lookup"><span data-stu-id="63bd6-117">Sign-in failure reasons on hello Azure Active Directory admin center</span></span>

<span data-ttu-id="63bd6-118">使用者登入的問題疑難排解無縫式 SSO 的好地方 toostart 是在 hello toolook[登入活動報表](../active-directory-reporting-activity-sign-ins.md)上 hello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="63bd6-118">A good place toostart troubleshooting user sign-in issues with Seamless SSO is toolook at hello [sign-in activity report](../active-directory-reporting-activity-sign-ins.md) on hello [Azure Active Directory admin center](https://aad.portal.azure.com/).</span></span>

![Azure Active Directory 管理中心 - 登入報告](./media/active-directory-aadconnect-sso/sso9.png)

<span data-ttu-id="63bd6-120">瀏覽過**Azure Active Directory** -> **登入**上 hello [Azure Active Directory 系統管理中心](https://aad.portal.azure.com/)，按一下 特定使用者的登入活動。</span><span class="sxs-lookup"><span data-stu-id="63bd6-120">Navigate too**Azure Active Directory** -> **Sign-ins** on hello [Azure Active Directory admin center](https://aad.portal.azure.com/) and click a specific user's sign-in activity.</span></span> <span data-ttu-id="63bd6-121">尋找 hello**登入錯誤碼**欄位。</span><span class="sxs-lookup"><span data-stu-id="63bd6-121">Look for hello **SIGN-IN ERROR CODE** field.</span></span> <span data-ttu-id="63bd6-122">對應欄位 tooa 失敗的原因和解決使用下表中的 hello 的 hello 的值：</span><span class="sxs-lookup"><span data-stu-id="63bd6-122">Map hello value of that field tooa failure reason and resolution using hello following table:</span></span>

|<span data-ttu-id="63bd6-123">登入錯誤碼</span><span class="sxs-lookup"><span data-stu-id="63bd6-123">Sign-in error code</span></span>|<span data-ttu-id="63bd6-124">登入失敗原因</span><span class="sxs-lookup"><span data-stu-id="63bd6-124">Sign-in failure reason</span></span>|<span data-ttu-id="63bd6-125">解決方案</span><span class="sxs-lookup"><span data-stu-id="63bd6-125">Resolution</span></span>
| --- | --- | ---
| <span data-ttu-id="63bd6-126">81001</span><span class="sxs-lookup"><span data-stu-id="63bd6-126">81001</span></span> | <span data-ttu-id="63bd6-127">使用者的 Kerberos 票證太大。</span><span class="sxs-lookup"><span data-stu-id="63bd6-127">User's Kerberos ticket is too large.</span></span> | <span data-ttu-id="63bd6-128">降低使用者的群組成員資格，並再試一次。</span><span class="sxs-lookup"><span data-stu-id="63bd6-128">Reduce user's group memberships and try again.</span></span>
| <span data-ttu-id="63bd6-129">81002</span><span class="sxs-lookup"><span data-stu-id="63bd6-129">81002</span></span> | <span data-ttu-id="63bd6-130">無法 toovalidate 使用者的 Kerberos 票證。</span><span class="sxs-lookup"><span data-stu-id="63bd6-130">Unable toovalidate user's Kerberos ticket.</span></span> | <span data-ttu-id="63bd6-131">請參閱[針對檢查清單進行疑難排解](#troubleshooting-checklist)。</span><span class="sxs-lookup"><span data-stu-id="63bd6-131">See [troubleshooting checklist](#troubleshooting-checklist).</span></span>
| <span data-ttu-id="63bd6-132">81003</span><span class="sxs-lookup"><span data-stu-id="63bd6-132">81003</span></span> | <span data-ttu-id="63bd6-133">無法 toovalidate 使用者的 Kerberos 票證。</span><span class="sxs-lookup"><span data-stu-id="63bd6-133">Unable toovalidate user's Kerberos ticket.</span></span> | <span data-ttu-id="63bd6-134">請參閱[針對檢查清單進行疑難排解](#troubleshooting-checklist)。</span><span class="sxs-lookup"><span data-stu-id="63bd6-134">See [troubleshooting checklist](#troubleshooting-checklist).</span></span>
| <span data-ttu-id="63bd6-135">81004</span><span class="sxs-lookup"><span data-stu-id="63bd6-135">81004</span></span> | <span data-ttu-id="63bd6-136">Kerberos 驗證嘗試失敗。</span><span class="sxs-lookup"><span data-stu-id="63bd6-136">Kerberos authentication attempt failed.</span></span> | <span data-ttu-id="63bd6-137">請參閱[針對檢查清單進行疑難排解](#troubleshooting-checklist)。</span><span class="sxs-lookup"><span data-stu-id="63bd6-137">See [troubleshooting checklist](#troubleshooting-checklist).</span></span>
| <span data-ttu-id="63bd6-138">81008</span><span class="sxs-lookup"><span data-stu-id="63bd6-138">81008</span></span> | <span data-ttu-id="63bd6-139">無法 toovalidate 使用者的 Kerberos 票證。</span><span class="sxs-lookup"><span data-stu-id="63bd6-139">Unable toovalidate user's Kerberos ticket.</span></span> | <span data-ttu-id="63bd6-140">請參閱[針對檢查清單進行疑難排解](#troubleshooting-checklist)。</span><span class="sxs-lookup"><span data-stu-id="63bd6-140">See [troubleshooting checklist](#troubleshooting-checklist).</span></span>
| <span data-ttu-id="63bd6-141">81009</span><span class="sxs-lookup"><span data-stu-id="63bd6-141">81009</span></span> | <span data-ttu-id="63bd6-142">「 無法 toovalidate 使用者的 Kerberos 票證。</span><span class="sxs-lookup"><span data-stu-id="63bd6-142">"Unable toovalidate user's Kerberos ticket.</span></span> | <span data-ttu-id="63bd6-143">請參閱[針對檢查清單進行疑難排解](#troubleshooting-checklist)。</span><span class="sxs-lookup"><span data-stu-id="63bd6-143">See [troubleshooting checklist](#troubleshooting-checklist).</span></span>
| <span data-ttu-id="63bd6-144">81010</span><span class="sxs-lookup"><span data-stu-id="63bd6-144">81010</span></span> | <span data-ttu-id="63bd6-145">無縫式 SSO 失敗，因為 hello 使用者的 Kerberos 票證已過期或無效。</span><span class="sxs-lookup"><span data-stu-id="63bd6-145">Seamless SSO failed because hello user's Kerberos ticket has expired or is invalid.</span></span> | <span data-ttu-id="63bd6-146">使用者必須從加入網域的裝置，您公司網路內部的 toosign 中。</span><span class="sxs-lookup"><span data-stu-id="63bd6-146">User needs toosign in from a domain-joined device inside your corporate network.</span></span>
| <span data-ttu-id="63bd6-147">81011</span><span class="sxs-lookup"><span data-stu-id="63bd6-147">81011</span></span> | <span data-ttu-id="63bd6-148">無法 toofind hello 使用者的 Kerberos 票證中的資訊為基礎的使用者物件。</span><span class="sxs-lookup"><span data-stu-id="63bd6-148">Unable toofind user object based on information in hello user's Kerberos ticket.</span></span> | <span data-ttu-id="63bd6-149">使用 Azure AD 到 Azure AD Connect toosynchronize 使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="63bd6-149">Use Azure AD Connect toosynchronize user information into Azure AD.</span></span>
| <span data-ttu-id="63bd6-150">81012</span><span class="sxs-lookup"><span data-stu-id="63bd6-150">81012</span></span> | <span data-ttu-id="63bd6-151">嘗試 toosign tooAzure AD 中的 hello 使用者所登入 hello 裝置 hello 使用者不同。</span><span class="sxs-lookup"><span data-stu-id="63bd6-151">hello user trying toosign in tooAzure AD is different from hello user signed into hello device.</span></span> | <span data-ttu-id="63bd6-152">從不同的裝置登入。</span><span class="sxs-lookup"><span data-stu-id="63bd6-152">Sign in from a different device.</span></span>
| <span data-ttu-id="63bd6-153">81013</span><span class="sxs-lookup"><span data-stu-id="63bd6-153">81013</span></span> | <span data-ttu-id="63bd6-154">無法 toofind hello 使用者的 Kerberos 票證中的資訊為基礎的使用者物件。</span><span class="sxs-lookup"><span data-stu-id="63bd6-154">Unable toofind user object based on information in hello user's Kerberos ticket.</span></span> |<span data-ttu-id="63bd6-155">使用 Azure AD 到 Azure AD Connect toosynchronize 使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="63bd6-155">Use Azure AD Connect toosynchronize user information into Azure AD.</span></span> 

## <a name="troubleshooting-checklist"></a><span data-ttu-id="63bd6-156">疑難排解檢查清單</span><span class="sxs-lookup"><span data-stu-id="63bd6-156">Troubleshooting checklist</span></span>

<span data-ttu-id="63bd6-157">使用下列檢查清單 tootroubleshoot 無縫式 SSO 所發出的 hello:</span><span class="sxs-lookup"><span data-stu-id="63bd6-157">Use hello following checklist tootroubleshoot Seamless SSO issues:</span></span>

- <span data-ttu-id="63bd6-158">請檢查是否已在 Azure AD Connect 啟用 hello 無縫式 SSO 功能。</span><span class="sxs-lookup"><span data-stu-id="63bd6-158">Check if hello Seamless SSO feature is enabled in Azure AD Connect.</span></span> <span data-ttu-id="63bd6-159">如果您無法啟用 hello 功能 （例如，由於 tooa 封鎖連接埠），請確定您有所有的 hello[先決條件](active-directory-aadconnect-sso-quick-start.md#step-1-check-prerequisites)備妥。</span><span class="sxs-lookup"><span data-stu-id="63bd6-159">If you can't enable hello feature (for example, due tooa blocked port), ensure that you have all hello [pre-requisites](active-directory-aadconnect-sso-quick-start.md#step-1-check-prerequisites) in place.</span></span>
- <span data-ttu-id="63bd6-160">請檢查這兩個 Azure AD Url （https://autologon.microsoftazuread-sso.com 和 https://aadg.windows.net.nsatc.net） 是否是 hello 使用者的內部網路區域設定的一部分。</span><span class="sxs-lookup"><span data-stu-id="63bd6-160">Check if both these Azure AD URLs (https://autologon.microsoftazuread-sso.com and https://aadg.windows.net.nsatc.net) are part of hello user's Intranet zone settings.</span></span>
- <span data-ttu-id="63bd6-161">確認 hello 公司的裝置已加入的 toohello AD 網域。</span><span class="sxs-lookup"><span data-stu-id="63bd6-161">Ensure hello corporate device is joined toohello AD domain.</span></span>
- <span data-ttu-id="63bd6-162">請確定 hello 使用者登入 toohello 裝置使用的 AD 網域帳戶。</span><span class="sxs-lookup"><span data-stu-id="63bd6-162">Ensure hello user is logged on toohello device using an AD domain account.</span></span>
- <span data-ttu-id="63bd6-163">請確認 hello 使用者帳戶來自已無縫式 SSO 的 AD 樹系設定。</span><span class="sxs-lookup"><span data-stu-id="63bd6-163">Ensure that hello user's account is from an AD forest where Seamless SSO has been set up.</span></span>
- <span data-ttu-id="63bd6-164">確認 hello 裝置 hello 公司網路上連線。</span><span class="sxs-lookup"><span data-stu-id="63bd6-164">Ensure hello device is connected on hello corporate network.</span></span>
- <span data-ttu-id="63bd6-165">請確認 hello 裝置時間的 hello Active Directory 的和 hello 網域控制站的時間同步相差五分鐘內。</span><span class="sxs-lookup"><span data-stu-id="63bd6-165">Ensure that hello device's time is synchronized with hello Active Directory's and hello Domain Controllers' time and is within five minutes of each other.</span></span>
- <span data-ttu-id="63bd6-166">列出現有的 Kerberos 票證 hello 裝置上使用 hello **klist**命令從命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="63bd6-166">List existing Kerberos tickets on hello device using hello **klist** command from a command prompt.</span></span> <span data-ttu-id="63bd6-167">檢查是否 hello 發出票證`AZUREADSSOACCT`電腦帳戶會出現。</span><span class="sxs-lookup"><span data-stu-id="63bd6-167">Check if tickets issued for hello `AZUREADSSOACCT` computer account are present.</span></span> <span data-ttu-id="63bd6-168">使用者的 Kerberos 票證有效期通常為 12 個小時。</span><span class="sxs-lookup"><span data-stu-id="63bd6-168">Users' Kerberos tickets are typically valid for 12 hours.</span></span> <span data-ttu-id="63bd6-169">您的 Active Directory 可能有不同的設定。</span><span class="sxs-lookup"><span data-stu-id="63bd6-169">You may have  different settings in your Active Directory.</span></span>
- <span data-ttu-id="63bd6-170">清除現有的 Kerberos 票證 hello 透過從裝置 hello **klist 清除**命令，並再試一次。</span><span class="sxs-lookup"><span data-stu-id="63bd6-170">Purge existing Kerberos tickets from hello device using hello **klist purge** command, and try again.</span></span>
- <span data-ttu-id="63bd6-171">toodetermine 是否有 JavaScript 相關問題，檢閱 hello hello 瀏覽器 （在 [開發人員工具）] 下的主控台記錄檔。</span><span class="sxs-lookup"><span data-stu-id="63bd6-171">toodetermine if there are JavaScript-related issues, review hello console logs of hello browser (under "Developer Tools").</span></span>
- <span data-ttu-id="63bd6-172">檢閱 hello[網域控制站記錄](#domain-controller-logs)以及。</span><span class="sxs-lookup"><span data-stu-id="63bd6-172">Review hello [Domain Controller logs](#domain-controller-logs) as well.</span></span>

### <a name="domain-controller-logs"></a><span data-ttu-id="63bd6-173">網域控制站記錄</span><span class="sxs-lookup"><span data-stu-id="63bd6-173">Domain Controller logs</span></span>

<span data-ttu-id="63bd6-174">如果成功稽核已啟用您的網域控制站上，然後每次使用者登入時使用無縫式 SSO 的安全性項目會記錄在 hello 事件記錄檔。</span><span class="sxs-lookup"><span data-stu-id="63bd6-174">If success auditing is enabled on your Domain Controller, then every time a user signs in using Seamless SSO a security entry is recorded in hello Event log.</span></span> <span data-ttu-id="63bd6-175">您可以找到使用下列查詢的 hello 這些安全性事件 (請查看事件**4769** hello 電腦帳戶相關聯**AzureADSSOAcc$**):</span><span class="sxs-lookup"><span data-stu-id="63bd6-175">You can find these security events using hello following query (look for event **4769** associated with hello computer account **AzureADSSOAcc$**):</span></span>

```
    <QueryList>
      <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ServiceName'] and (Data='AZUREADSSOACC$')]]</Select>
      </Query>
    </QueryList>
```

## <a name="manual-reset-of-hello-feature"></a><span data-ttu-id="63bd6-176">手動重設的 hello 功能</span><span class="sxs-lookup"><span data-stu-id="63bd6-176">Manual reset of hello feature</span></span>

<span data-ttu-id="63bd6-177">如果疑難排解沒有幫助，可以在租用戶的手動重設 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="63bd6-177">If troubleshooting didn't help, you can manually reset hello feature on your tenant.</span></span> <span data-ttu-id="63bd6-178">執行 Azure AD Connect 的情況下遵循 hello 在內部部署伺服器上的下列步驟：</span><span class="sxs-lookup"><span data-stu-id="63bd6-178">Follow these steps on hello on-premises server where you are running Azure AD Connect:</span></span>

### <a name="step-1-import-hello-seamless-sso-powershell-module"></a><span data-ttu-id="63bd6-179">步驟 1： 匯入 hello 無縫式 SSO 的 PowerShell 模組</span><span class="sxs-lookup"><span data-stu-id="63bd6-179">Step 1: Import hello Seamless SSO PowerShell module</span></span>

1. <span data-ttu-id="63bd6-180">首先，下載並安裝 hello [Microsoft Online Services 登入小幫手](http://go.microsoft.com/fwlink/?LinkID=286152)。</span><span class="sxs-lookup"><span data-stu-id="63bd6-180">First, download, and install hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span>
2. <span data-ttu-id="63bd6-181">請下載並安裝 hello [64 位元 Windows PowerShell 的 Azure Active Directory 模組](http://go.microsoft.com/fwlink/p/?linkid=236297)。</span><span class="sxs-lookup"><span data-stu-id="63bd6-181">Then download and install hello [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>
3. <span data-ttu-id="63bd6-182">瀏覽 toohello`%programfiles%\Microsoft Azure Active Directory Connect`資料夾。</span><span class="sxs-lookup"><span data-stu-id="63bd6-182">Navigate toohello `%programfiles%\Microsoft Azure Active Directory Connect` folder.</span></span>
4. <span data-ttu-id="63bd6-183">使用這個命令匯入 hello 無縫式 SSO 的 PowerShell 模組： `Import-Module .\AzureADSSO.psd1`。</span><span class="sxs-lookup"><span data-stu-id="63bd6-183">Import hello Seamless SSO PowerShell module using this command: `Import-Module .\AzureADSSO.psd1`.</span></span>

### <a name="step-2-get-hello-list-of-ad-forests-on-which-seamless-sso-has-been-enabled"></a><span data-ttu-id="63bd6-184">步驟 2： 取得 AD 樹系啟用無縫式 SSO 的 hello 清單</span><span class="sxs-lookup"><span data-stu-id="63bd6-184">Step 2: Get hello list of AD forests on which Seamless SSO has been enabled</span></span>

1. <span data-ttu-id="63bd6-185">以系統管理員身分執行 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="63bd6-185">Run PowerShell as Administrator.</span></span> <span data-ttu-id="63bd6-186">在 PowerShell 中，呼叫 `New-AzureADSSOAuthenticationContext`。</span><span class="sxs-lookup"><span data-stu-id="63bd6-186">In PowerShell, call `New-AzureADSSOAuthenticationContext`.</span></span> <span data-ttu-id="63bd6-187">出現提示時，輸入您租用戶的全域管理員認證。</span><span class="sxs-lookup"><span data-stu-id="63bd6-187">When prompted, enter your tenant's Global Administrator credentials.</span></span>
2. <span data-ttu-id="63bd6-188">呼叫 `Get-AzureADSSOStatus`。</span><span class="sxs-lookup"><span data-stu-id="63bd6-188">Call `Get-AzureADSSOStatus`.</span></span> <span data-ttu-id="63bd6-189">這個命令會提供您在已啟用這項功能的 hello AD 樹系 （查看 hello 「 網域 」 清單） 的清單。</span><span class="sxs-lookup"><span data-stu-id="63bd6-189">This command provides you hello list of AD forests (look at hello "Domains" list) on which this feature has been enabled.</span></span>

### <a name="step-3-disable-seamless-sso-for-each-ad-forest-that-it-was-set-it-up-on"></a><span data-ttu-id="63bd6-190">步驟3：針對已設定無縫 SSO 的每個 AD 樹系停用該功能</span><span class="sxs-lookup"><span data-stu-id="63bd6-190">Step 3: Disable Seamless SSO for each AD forest that it was set it up on</span></span>

1. <span data-ttu-id="63bd6-191">呼叫 `$creds = Get-Credential`。</span><span class="sxs-lookup"><span data-stu-id="63bd6-191">Call `$creds = Get-Credential`.</span></span> <span data-ttu-id="63bd6-192">出現提示時，輸入 hello 適合 AD 樹系 hello 網域系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="63bd6-192">When prompted, enter hello Domain Administrator credentials for hello intended AD forest.</span></span>
2. <span data-ttu-id="63bd6-193">呼叫 `Disable-AzureADSSOForest -OnPremCredentials $creds`。</span><span class="sxs-lookup"><span data-stu-id="63bd6-193">Call `Disable-AzureADSSOForest -OnPremCredentials $creds`.</span></span> <span data-ttu-id="63bd6-194">此命令會移除 hello `AZUREADSSOACCT` hello 電腦帳戶在內部部署網域控制站為此特定的 AD 樹系。</span><span class="sxs-lookup"><span data-stu-id="63bd6-194">This command removes hello `AZUREADSSOACCT` computer account from hello on-premises Domain Controller for this specific AD forest.</span></span>
3. <span data-ttu-id="63bd6-195">重複上述步驟設定好 hello 功能每個 AD 樹系的 hello。</span><span class="sxs-lookup"><span data-stu-id="63bd6-195">Repeat hello preceding steps for each AD forest that you’ve set up hello feature on.</span></span>

### <a name="step-4-enable-seamless-sso-for-each-ad-forest"></a><span data-ttu-id="63bd6-196">步驟 4：為每個 AD 樹系啟用無縫 SSO</span><span class="sxs-lookup"><span data-stu-id="63bd6-196">Step 4: Enable Seamless SSO for each AD forest</span></span>

1. <span data-ttu-id="63bd6-197">呼叫 `Enable-AzureADSSOForest`。</span><span class="sxs-lookup"><span data-stu-id="63bd6-197">Call `Enable-AzureADSSOForest`.</span></span> <span data-ttu-id="63bd6-198">出現提示時，輸入 hello 適合 AD 樹系 hello 網域系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="63bd6-198">When prompted, enter hello Domain Administrator credentials for hello intended AD forest.</span></span>
2. <span data-ttu-id="63bd6-199">重複上述步驟，每個 AD 樹系上您想要向上 hello 功能 tooset hello。</span><span class="sxs-lookup"><span data-stu-id="63bd6-199">Repeat hello preceding steps for each AD forest that you want tooset up hello feature on.</span></span>

### <a name="step-5-enable-hello-feature-on-your-tenant"></a><span data-ttu-id="63bd6-200">步驟 5。</span><span class="sxs-lookup"><span data-stu-id="63bd6-200">Step 5.</span></span> <span data-ttu-id="63bd6-201">啟用在租用戶的 hello 功能</span><span class="sxs-lookup"><span data-stu-id="63bd6-201">Enable hello feature on your tenant</span></span>

<span data-ttu-id="63bd6-202">呼叫`Enable-AzureADSSO` 並輸入"true"，在 hello`Enable: `提示 tooturn 租用戶中的 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="63bd6-202">Call `Enable-AzureADSSO` and type in "true" at hello `Enable: ` prompt tooturn on hello feature in your tenant.</span></span>
