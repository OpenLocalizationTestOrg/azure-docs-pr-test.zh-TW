---
title: "原則︰Azure AD SSPR | Microsoft Docs"
description: "Azure AD 自助式密碼重設原則選項"
services: active-directory
keywords: "Active directory 密碼管理, 密碼管理, Azure AD 自助式密碼重設"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: af7cb13794bf3a9fee91d355f788aa5c2246e57c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="password-policies-and-restrictions-in-azure-active-directory"></a><span data-ttu-id="d72d2-104">密碼原則和 Azure Active Directory 中的限制</span><span class="sxs-lookup"><span data-stu-id="d72d2-104">Password policies and restrictions in Azure Active Directory</span></span>

<span data-ttu-id="d72d2-105">本文說明 hello 密碼原則和儲存在 Azure AD 租用戶的使用者帳戶相關聯的複雜性需求。</span><span class="sxs-lookup"><span data-stu-id="d72d2-105">This article describes hello password policies and complexity requirements associated with user accounts stored in your Azure AD tenant.</span></span>

## <a name="administrator-password-policy-differences"></a><span data-ttu-id="d72d2-106">系統管理員密碼原則差異</span><span class="sxs-lookup"><span data-stu-id="d72d2-106">Administrator password policy differences</span></span>

<span data-ttu-id="d72d2-107">Microsoft 會對任何系統管理員角色 (全域管理員、技術支援系統管理員、密碼管理員等) 強制執行強式預設「雙閘道」密碼重設原則</span><span class="sxs-lookup"><span data-stu-id="d72d2-107">Microsoft enforces a strong default **two gate** password reset policy for any Azure administrator role (Example: Global Administrator, Helpdesk Administrator, Password Administrator, etc.)</span></span>

<span data-ttu-id="d72d2-108">這會停用系統管理員使用安全性問題，並強制執行 hello 下列。</span><span class="sxs-lookup"><span data-stu-id="d72d2-108">This disables administrators from using security questions and enforces hello following.</span></span>

<span data-ttu-id="d72d2-109">兩個控制原則，需要這兩項驗證資料 (電子郵件地址**和**電話號碼)，適用於下列情況下的 hello</span><span class="sxs-lookup"><span data-stu-id="d72d2-109">Two gate policy, requiring two pieces of authentication data (email address **and** phone number), applies in hello following circumstances</span></span>

* <span data-ttu-id="d72d2-110">所有的 Azure 系統管理員角色</span><span class="sxs-lookup"><span data-stu-id="d72d2-110">All Azure administrator roles</span></span>
  * <span data-ttu-id="d72d2-111">服務台系統管理員</span><span class="sxs-lookup"><span data-stu-id="d72d2-111">Helpdesk Administrator</span></span>
  * <span data-ttu-id="d72d2-112">服務支援管理員</span><span class="sxs-lookup"><span data-stu-id="d72d2-112">Service Support Administrator</span></span>
  * <span data-ttu-id="d72d2-113">計費管理員</span><span class="sxs-lookup"><span data-stu-id="d72d2-113">Billing Administrator</span></span>
  * <span data-ttu-id="d72d2-114">合作夥伴第 1 層支援</span><span class="sxs-lookup"><span data-stu-id="d72d2-114">Partner Tier1 Support</span></span>
  * <span data-ttu-id="d72d2-115">合作夥伴第 2 層支援</span><span class="sxs-lookup"><span data-stu-id="d72d2-115">Partner Tier2 Support</span></span>
  * <span data-ttu-id="d72d2-116">Exchange 服務管理員</span><span class="sxs-lookup"><span data-stu-id="d72d2-116">Exchange Service Administrator</span></span>
  * <span data-ttu-id="d72d2-117">Lync 服務管理員</span><span class="sxs-lookup"><span data-stu-id="d72d2-117">Lync Service Administrator</span></span>
  * <span data-ttu-id="d72d2-118">使用者帳戶管理員</span><span class="sxs-lookup"><span data-stu-id="d72d2-118">User Account Administrator</span></span>
  * <span data-ttu-id="d72d2-119">目錄撰寫者</span><span class="sxs-lookup"><span data-stu-id="d72d2-119">Directory Writers</span></span>
  * <span data-ttu-id="d72d2-120">全域管理員/公司系統管理員</span><span class="sxs-lookup"><span data-stu-id="d72d2-120">Global Administrator/Company Administrator</span></span>
  * <span data-ttu-id="d72d2-121">SharePoint 服務管理員</span><span class="sxs-lookup"><span data-stu-id="d72d2-121">SharePoint Service Administrator</span></span>
  * <span data-ttu-id="d72d2-122">規範管理員</span><span class="sxs-lookup"><span data-stu-id="d72d2-122">Compliance Administrator</span></span>
  * <span data-ttu-id="d72d2-123">應用程式系統管理員</span><span class="sxs-lookup"><span data-stu-id="d72d2-123">Application Administrator</span></span>
  * <span data-ttu-id="d72d2-124">安全性系統管理員</span><span class="sxs-lookup"><span data-stu-id="d72d2-124">Security Administrator</span></span>
  * <span data-ttu-id="d72d2-125">特殊權限角色管理員</span><span class="sxs-lookup"><span data-stu-id="d72d2-125">Privileged Role Administrator</span></span>
  * <span data-ttu-id="d72d2-126">Intune 服務管理員</span><span class="sxs-lookup"><span data-stu-id="d72d2-126">Intune Service Administrator</span></span>
  * <span data-ttu-id="d72d2-127">應用程式 Proxy 服務管理員</span><span class="sxs-lookup"><span data-stu-id="d72d2-127">Application Proxy Service Administrator</span></span>
  * <span data-ttu-id="d72d2-128">CRM 服務管理員</span><span class="sxs-lookup"><span data-stu-id="d72d2-128">CRM Service Administrator</span></span>
  * <span data-ttu-id="d72d2-129">Power BI 服務管理員</span><span class="sxs-lookup"><span data-stu-id="d72d2-129">Power BI Service Administrator</span></span>
  
* <span data-ttu-id="d72d2-130">試用已經過 30 天**或**</span><span class="sxs-lookup"><span data-stu-id="d72d2-130">30 days have elapsed in a trial **OR**</span></span>
* <span data-ttu-id="d72d2-131">虛名網域存在於 (contoso.com) **或**</span><span class="sxs-lookup"><span data-stu-id="d72d2-131">Vanity domain is present (contoso.com) **OR**</span></span>
* <span data-ttu-id="d72d2-132">Azure AD Connect 正在同步處理內部部署目錄中的身分識別</span><span class="sxs-lookup"><span data-stu-id="d72d2-132">Azure AD Connect is synchronizing identities from your on-premises directory</span></span>

### <a name="exceptions"></a><span data-ttu-id="d72d2-133">例外狀況</span><span class="sxs-lookup"><span data-stu-id="d72d2-133">Exceptions</span></span>
<span data-ttu-id="d72d2-134">單一閘道原則，需要一段驗證資料 (電子郵件地址**或**電話號碼)，適用於下列情況下的 hello</span><span class="sxs-lookup"><span data-stu-id="d72d2-134">One gate policy, requiring one piece of authentication data (email address **or** phone number), applies in hello following circumstances</span></span>

* <span data-ttu-id="d72d2-135">試用的前 30 天**或**</span><span class="sxs-lookup"><span data-stu-id="d72d2-135">First 30 days of a trial **OR**</span></span>
* <span data-ttu-id="d72d2-136">虛名網域不存在 (*.onmicrosoft.com) **且** Azure AD Connect 並未同步處理身分識別</span><span class="sxs-lookup"><span data-stu-id="d72d2-136">Vanity domain is not present (*.onmicrosoft.com) **AND** Azure AD Connect is not synchronizing identities</span></span>


## <a name="userprincipalname-policies-that-apply-tooall-user-accounts"></a><span data-ttu-id="d72d2-137">適用於 tooall 使用者帳戶的 UserPrincipalName 原則</span><span class="sxs-lookup"><span data-stu-id="d72d2-137">UserPrincipalName policies that apply tooall user accounts</span></span>

<span data-ttu-id="d72d2-138">需要 toosign tooAzure AD 中的每個使用者帳戶必須具有與帳戶相關聯的唯一使用者主要名稱 (UPN) 屬性值。</span><span class="sxs-lookup"><span data-stu-id="d72d2-138">Every user account that needs toosign in tooAzure AD must have a unique user principal name (UPN) attribute value associated with their account.</span></span> <span data-ttu-id="d72d2-139">hello 表概述 hello 原則適用於 tooboth 內部部署 Active Directory 使用者帳戶同步處理 toohello 雲端和 toocloud 僅限使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="d72d2-139">hello table below outlines hello polices that apply tooboth on-premises Active Directory user accounts synchronized toohello cloud and toocloud-only user accounts.</span></span>

| <span data-ttu-id="d72d2-140">屬性</span><span class="sxs-lookup"><span data-stu-id="d72d2-140">Property</span></span> | <span data-ttu-id="d72d2-141">UserPrincipalName 需求</span><span class="sxs-lookup"><span data-stu-id="d72d2-141">UserPrincipalName requirements</span></span> |
| --- | --- |
| <span data-ttu-id="d72d2-142">允許的字元</span><span class="sxs-lookup"><span data-stu-id="d72d2-142">Characters allowed</span></span> |<ul> <li><span data-ttu-id="d72d2-143">A – Z</span><span class="sxs-lookup"><span data-stu-id="d72d2-143">A – Z</span></span></li> <li><span data-ttu-id="d72d2-144">a - z</span><span class="sxs-lookup"><span data-stu-id="d72d2-144">a - z</span></span></li><li><span data-ttu-id="d72d2-145">0 – 9</span><span class="sxs-lookup"><span data-stu-id="d72d2-145">0 – 9</span></span></li> <li> <span data-ttu-id="d72d2-146">。</span><span class="sxs-lookup"><span data-stu-id="d72d2-146">.</span></span><span data-ttu-id="d72d2-147"> - \_ !</span><span class="sxs-lookup"><span data-stu-id="d72d2-147"> - \_ !</span></span> <span data-ttu-id="d72d2-148">\# ^ \~</span><span class="sxs-lookup"><span data-stu-id="d72d2-148">\# ^ \~</span></span></li></ul> |
| <span data-ttu-id="d72d2-149">不允許的字元</span><span class="sxs-lookup"><span data-stu-id="d72d2-149">Characters not allowed</span></span> |<ul> <li><span data-ttu-id="d72d2-150">任何 ' @' 不區隔 hello hello 網域的使用者名稱的字元。</span><span class="sxs-lookup"><span data-stu-id="d72d2-150">Any '@' character that is not separating hello user name from hello domain.</span></span></li> <li><span data-ttu-id="d72d2-151">不能包含句號字元 '。 '正前面的 hello' @' 符號</span><span class="sxs-lookup"><span data-stu-id="d72d2-151">Cannot contain a period character '.' immediately preceding hello '@' symbol</span></span></li></ul> |
| <span data-ttu-id="d72d2-152">長度限制</span><span class="sxs-lookup"><span data-stu-id="d72d2-152">Length constraints</span></span> |<ul> <li><span data-ttu-id="d72d2-153">總長度不得超過 113 個字元</span><span class="sxs-lookup"><span data-stu-id="d72d2-153">Total length must not exceed 113 characters</span></span></li><li><span data-ttu-id="d72d2-154">hello 前的 64 個字元 ' @' 符號</span><span class="sxs-lookup"><span data-stu-id="d72d2-154">64 characters before hello ‘@’ symbol</span></span></li><li><span data-ttu-id="d72d2-155">在 hello 後的 48 個字元 ' @' 符號</span><span class="sxs-lookup"><span data-stu-id="d72d2-155">48 characters after hello ‘@’ symbol</span></span></li></ul> |

## <a name="password-policies-that-apply-only-toocloud-user-accounts"></a><span data-ttu-id="d72d2-156">適用於 toocloud 使用者帳戶的密碼原則</span><span class="sxs-lookup"><span data-stu-id="d72d2-156">Password policies that apply only toocloud user accounts</span></span>

<span data-ttu-id="d72d2-157">hello 下表描述可為套用的 toouser 帳戶所建立及管理 Azure AD 中的 hello 密碼原則設定。</span><span class="sxs-lookup"><span data-stu-id="d72d2-157">hello following table describes hello available password policy settings that can be applied toouser accounts that are created and managed in Azure AD.</span></span>

| <span data-ttu-id="d72d2-158">屬性</span><span class="sxs-lookup"><span data-stu-id="d72d2-158">Property</span></span> | <span data-ttu-id="d72d2-159">需求</span><span class="sxs-lookup"><span data-stu-id="d72d2-159">Requirements</span></span> |
| --- | --- |
| <span data-ttu-id="d72d2-160">允許的字元</span><span class="sxs-lookup"><span data-stu-id="d72d2-160">Characters allowed</span></span> |<ul><li><span data-ttu-id="d72d2-161">A – Z</span><span class="sxs-lookup"><span data-stu-id="d72d2-161">A – Z</span></span></li><li><span data-ttu-id="d72d2-162">a - z</span><span class="sxs-lookup"><span data-stu-id="d72d2-162">a - z</span></span></li><li><span data-ttu-id="d72d2-163">0 – 9</span><span class="sxs-lookup"><span data-stu-id="d72d2-163">0 – 9</span></span></li> <li><span data-ttu-id="d72d2-164">@ # $ % ^ & * - _ !</span><span class="sxs-lookup"><span data-stu-id="d72d2-164">@ # $ % ^ & * - _ !</span></span> <span data-ttu-id="d72d2-165">+ = [ ] { } &#124; \ : ‘ , .</span><span class="sxs-lookup"><span data-stu-id="d72d2-165">+ = [ ] { } &#124; \ : ‘ , .</span></span> <span data-ttu-id="d72d2-166">?</span><span class="sxs-lookup"><span data-stu-id="d72d2-166">?</span></span> <span data-ttu-id="d72d2-167">/ \` ~ “ ( ) ;</span><span class="sxs-lookup"><span data-stu-id="d72d2-167">/ \` ~ “ ( ) ;</span></span></li></ul> |
| <span data-ttu-id="d72d2-168">不允許的字元</span><span class="sxs-lookup"><span data-stu-id="d72d2-168">Characters not allowed</span></span> |<ul><li><span data-ttu-id="d72d2-169">Unicode 字元</span><span class="sxs-lookup"><span data-stu-id="d72d2-169">Unicode characters</span></span></li><li><span data-ttu-id="d72d2-170">空格</span><span class="sxs-lookup"><span data-stu-id="d72d2-170">Spaces</span></span></li><li> <span data-ttu-id="d72d2-171">**強式密碼只**： 不能包含點字元 '。 '正前面的 hello' @' 符號</span><span class="sxs-lookup"><span data-stu-id="d72d2-171">**Strong passwords only**: Cannot contain a dot character '.' immediately preceding hello '@' symbol</span></span></li></ul> |
| <span data-ttu-id="d72d2-172">密碼限制</span><span class="sxs-lookup"><span data-stu-id="d72d2-172">Password restrictions</span></span> |<ul><li><span data-ttu-id="d72d2-173">最少 8 個字元，最多 16 個字元</span><span class="sxs-lookup"><span data-stu-id="d72d2-173">8 characters minimum and 16 characters maximum</span></span></li><li><span data-ttu-id="d72d2-174">**強式密碼只**： 需要 3，4 hello 以下的：</span><span class="sxs-lookup"><span data-stu-id="d72d2-174">**Strong passwords only**: Requires 3 out of 4 of hello following:</span></span><ul><li><span data-ttu-id="d72d2-175">小寫字元</span><span class="sxs-lookup"><span data-stu-id="d72d2-175">Lowercase characters</span></span></li><li><span data-ttu-id="d72d2-176">大寫字元</span><span class="sxs-lookup"><span data-stu-id="d72d2-176">Uppercase characters</span></span></li><li><span data-ttu-id="d72d2-177">數字 (0-9)</span><span class="sxs-lookup"><span data-stu-id="d72d2-177">Numbers (0-9)</span></span></li><li><span data-ttu-id="d72d2-178">符號 (請參閱上面的密碼限制)</span><span class="sxs-lookup"><span data-stu-id="d72d2-178">Symbols (see password restrictions above)</span></span></li></ul></li></ul> |
| <span data-ttu-id="d72d2-179">密碼到期時間</span><span class="sxs-lookup"><span data-stu-id="d72d2-179">Password expiry duration</span></span> |<ul><li><span data-ttu-id="d72d2-180">預設值：**90** 天</span><span class="sxs-lookup"><span data-stu-id="d72d2-180">Default value: **90** days</span></span> </li><li><span data-ttu-id="d72d2-181">值為可使用 hello Set-msolpasswordpolicy cmdlet 從 hello Azure Active Directory 的 Windows PowerShell 模組設定。</span><span class="sxs-lookup"><span data-stu-id="d72d2-181">Value is configurable using hello Set-MsolPasswordPolicy cmdlet from hello Azure Active Directory Module for Windows PowerShell.</span></span></li></ul> |
| <span data-ttu-id="d72d2-182">密碼到期通知</span><span class="sxs-lookup"><span data-stu-id="d72d2-182">Password expiry notification</span></span> |<ul><li><span data-ttu-id="d72d2-183">預設值：**14** 天 (密碼到期之前)</span><span class="sxs-lookup"><span data-stu-id="d72d2-183">Default value: **14** days (before password expires)</span></span></li><li><span data-ttu-id="d72d2-184">值為可使用 hello Set-msolpasswordpolicy cmdlet 設定。</span><span class="sxs-lookup"><span data-stu-id="d72d2-184">Value is configurable using hello Set-MsolPasswordPolicy cmdlet.</span></span></li></ul> |
| <span data-ttu-id="d72d2-185">密碼到期</span><span class="sxs-lookup"><span data-stu-id="d72d2-185">Password Expiry</span></span> |<ul><li><span data-ttu-id="d72d2-186">預設值︰**false** 天 (表示已啟用密碼到期)</span><span class="sxs-lookup"><span data-stu-id="d72d2-186">Default value: **false** days (indicates that password expiry is enabled)</span></span> </li><li><span data-ttu-id="d72d2-187">值可以設定為使用 hello Set-msoluser 指令程式的個別使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="d72d2-187">Value can be configured for individual user accounts using hello Set-MsolUser cmdlet.</span></span> </li></ul> |
| <span data-ttu-id="d72d2-188">密碼**變更**歷程記錄</span><span class="sxs-lookup"><span data-stu-id="d72d2-188">Password **change** history</span></span> |<span data-ttu-id="d72d2-189">**變更**密碼時，**無法**再次使用上次的密碼。</span><span class="sxs-lookup"><span data-stu-id="d72d2-189">Last password **cannot** be used again when **changing** a password.</span></span> |
| <span data-ttu-id="d72d2-190">密碼**重設**歷程記錄</span><span class="sxs-lookup"><span data-stu-id="d72d2-190">Password **reset** history</span></span> | <span data-ttu-id="d72d2-191">**重設**遺忘的密碼時，**可以**再次使用上次的密碼。</span><span class="sxs-lookup"><span data-stu-id="d72d2-191">Last password **may** be used again when **resetting** a forgotten password.</span></span> |
| <span data-ttu-id="d72d2-192">帳戶鎖定</span><span class="sxs-lookup"><span data-stu-id="d72d2-192">Account Lockout</span></span> |<span data-ttu-id="d72d2-193">10 失敗登入嘗試之後 （錯誤密碼），請花一分鐘鎖定 hello 使用者。</span><span class="sxs-lookup"><span data-stu-id="d72d2-193">After 10 unsuccessful sign-in attempts (wrong password), hello user will be locked out for one minute.</span></span> <span data-ttu-id="d72d2-194">不正確的登入嘗試鎖定 hello 使用者增加持續時間。</span><span class="sxs-lookup"><span data-stu-id="d72d2-194">Further incorrect sign-in attempts lock out hello user for increasing durations.</span></span> |

## <a name="set-password-expiration-policies-in-azure-active-directory"></a><span data-ttu-id="d72d2-195">在 Azure Active Directory 中設定密碼到期原則</span><span class="sxs-lookup"><span data-stu-id="d72d2-195">Set password expiration policies in Azure Active Directory</span></span>

<span data-ttu-id="d72d2-196">Microsoft 雲端服務的全域系統管理員可以使用使用者密碼不 tooexpire hello Microsoft Azure Active Directory 的 Windows PowerShell 模組 tooset。</span><span class="sxs-lookup"><span data-stu-id="d72d2-196">A global administrator for a Microsoft cloud service can use hello Microsoft Azure Active Directory Module for Windows PowerShell tooset up user passwords not tooexpire.</span></span> <span data-ttu-id="d72d2-197">您也可以使用 Windows PowerShell cmdlet tooremove hello 永不過期的設定或 toosee 不 tooexpire 設定哪些使用者密碼。</span><span class="sxs-lookup"><span data-stu-id="d72d2-197">You can also use Windows PowerShell cmdlets tooremove hello never-expires configuration, or toosee which user passwords are set up not tooexpire.</span></span> <span data-ttu-id="d72d2-198">本指南適用於 tooother 提供者，例如 Microsoft Intune 和 Office 365 也依賴 Microsoft Azure Active Directory 身分識別和目錄服務。</span><span class="sxs-lookup"><span data-stu-id="d72d2-198">This guidance applies tooother providers such as Microsoft Intune and Office 365, which also rely on Microsoft Azure Active Directory for identity and directory services.</span></span>

> [!NOTE]
> <span data-ttu-id="d72d2-199">只有密碼 toonot 可以設定未透過目錄同步作業同步處理的使用者帳戶到期。</span><span class="sxs-lookup"><span data-stu-id="d72d2-199">Only passwords for user accounts that are not synchronized through directory synchronization can be configured toonot expire.</span></span> <span data-ttu-id="d72d2-200">如需有關目錄同步作業，請參閱 [Connect AD 與 Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)。</span><span class="sxs-lookup"><span data-stu-id="d72d2-200">For more information about directory synchronization see[Connect AD with Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).</span></span>
>
>

## <a name="set-or-check-password-policies-using-powershell"></a><span data-ttu-id="d72d2-201">使用 PowerShell 設定或檢查密碼原則</span><span class="sxs-lookup"><span data-stu-id="d72d2-201">Set or check password policies using PowerShell</span></span>

<span data-ttu-id="d72d2-202">tooget 開始，您需要太[下載並安裝 hello Azure AD PowerShell 模組](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0)。</span><span class="sxs-lookup"><span data-stu-id="d72d2-202">tooget started, you need too[download and install hello Azure AD PowerShell module](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0).</span></span> <span data-ttu-id="d72d2-203">一旦您已經安裝，您可以依照下列 tooconfigure hello 步驟是每個欄位。</span><span class="sxs-lookup"><span data-stu-id="d72d2-203">Once you have it installed, you can follow hello steps below tooconfigure each field.</span></span>

### <a name="how-toocheck-expiration-policy-for-a-password"></a><span data-ttu-id="d72d2-204">如何 toocheck 密碼到期原則</span><span class="sxs-lookup"><span data-stu-id="d72d2-204">How toocheck expiration policy for a password</span></span>
1. <span data-ttu-id="d72d2-205">連接 tooWindows PowerShell 中使用您的公司系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="d72d2-205">Connect tooWindows PowerShell using your company administrator credentials.</span></span>
2. <span data-ttu-id="d72d2-206">執行下列其中一個 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="d72d2-206">Execute one of hello following commands:</span></span>

   * <span data-ttu-id="d72d2-207">toosee 單一使用者的密碼是否設定 toonever 過期，請執行下列指令程式使用 hello 使用者主體名稱 (UPN) 的 hello (例如， aprilr@contoso.onmicrosoft.com) 或 hello 使用者識別碼的 hello 使用者想要 toocheck:`Get-MSOLUser -UserPrincipalName <user ID> | Select PasswordNeverExpires`</span><span class="sxs-lookup"><span data-stu-id="d72d2-207">toosee whether a single user’s password is set toonever expire, run hello following cmdlet by using hello user principal name (UPN) (for example, aprilr@contoso.onmicrosoft.com) or hello user ID of hello user you want toocheck: `Get-MSOLUser -UserPrincipalName <user ID> | Select PasswordNeverExpires`</span></span>
   * <span data-ttu-id="d72d2-208">toosee hello 所有使用者的 [密碼永久有效] 設定，請執行下列 cmdlet 的 hello:`Get-MSOLUser | Select UserPrincipalName, PasswordNeverExpires`</span><span class="sxs-lookup"><span data-stu-id="d72d2-208">toosee hello "Password never expires" setting for all users, run hello following cmdlet: `Get-MSOLUser | Select UserPrincipalName, PasswordNeverExpires`</span></span>

### <a name="set-a-password-tooexpire"></a><span data-ttu-id="d72d2-209">設定密碼 tooexpire</span><span class="sxs-lookup"><span data-stu-id="d72d2-209">Set a password tooexpire</span></span>

1. <span data-ttu-id="d72d2-210">連接 tooWindows PowerShell 中使用您的公司系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="d72d2-210">Connect tooWindows PowerShell using your company administrator credentials.</span></span>
2. <span data-ttu-id="d72d2-211">執行下列其中一個 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="d72d2-211">Execute one of hello following commands:</span></span>

   * <span data-ttu-id="d72d2-212">某位使用者的 tooset hello 密碼，以便讓 hello 密碼已過期，執行下列指令程式使用 hello 使用者主體名稱 (UPN) 的 hello 或 hello hello 使用者的使用者識別碼：`Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $false`</span><span class="sxs-lookup"><span data-stu-id="d72d2-212">tooset hello password of one user so that hello password expires, run hello following cmdlet by using hello user principal name (UPN) or hello user ID of hello user: `Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $false`</span></span>
   * <span data-ttu-id="d72d2-213">hello 組織中所有使用者的 tooset hello 密碼，讓它們過期時，使用下列 cmdlet 的 hello:`Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $false`</span><span class="sxs-lookup"><span data-stu-id="d72d2-213">tooset hello passwords of all users in hello organization so that they expire, use hello following cmdlet: `Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $false`</span></span>

### <a name="set-a-password-toonever-expire"></a><span data-ttu-id="d72d2-214">將密碼 toonever 過期</span><span class="sxs-lookup"><span data-stu-id="d72d2-214">Set a password toonever expire</span></span>

1. <span data-ttu-id="d72d2-215">連接 tooWindows PowerShell 中使用您的公司系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="d72d2-215">Connect tooWindows PowerShell using your company administrator credentials.</span></span>
2. <span data-ttu-id="d72d2-216">執行下列其中一個 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="d72d2-216">Execute one of hello following commands:</span></span>

   * <span data-ttu-id="d72d2-217">一位使用者 toonever tooset hello 密碼過期，執行下列指令程式使用 hello 使用者主體名稱 (UPN) 的 hello 或 hello hello 使用者的使用者識別碼：`Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $true`</span><span class="sxs-lookup"><span data-stu-id="d72d2-217">tooset hello password of one user toonever expire, run hello following cmdlet by using hello user principal name (UPN) or hello user ID of hello user: `Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $true`</span></span>
   * <span data-ttu-id="d72d2-218">所有 hello 中的使用者組織 toonever tooset hello 密碼過期，請執行下列 cmdlet 的 hello:`Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $true`</span><span class="sxs-lookup"><span data-stu-id="d72d2-218">tooset hello passwords of all hello users in an organization toonever expire, run hello following cmdlet: `Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $true`</span></span>

## <a name="next-steps"></a><span data-ttu-id="d72d2-219">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d72d2-219">Next steps</span></span>

<span data-ttu-id="d72d2-220">hello 下列連結提供有關密碼重設使用 Azure AD 的其他資訊</span><span class="sxs-lookup"><span data-stu-id="d72d2-220">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="d72d2-221">[**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理</span><span class="sxs-lookup"><span data-stu-id="d72d2-221">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="d72d2-222">[**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權</span><span class="sxs-lookup"><span data-stu-id="d72d2-222">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="d72d2-223">[**資料**](active-directory-passwords-data.md) -了解所需的 hello 資料及如何使用密碼管理</span><span class="sxs-lookup"><span data-stu-id="d72d2-223">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="d72d2-224">[**首度發行**](active-directory-passwords-best-practices.md) -計劃和部署 SSPR tooyour 使用者 hello 指引，請參閱</span><span class="sxs-lookup"><span data-stu-id="d72d2-224">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="d72d2-225">[**自訂**](active-directory-passwords-customize.md) -自訂的 hello SSPR 體驗您的公司 hello 外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="d72d2-225">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="d72d2-226">[**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能</span><span class="sxs-lookup"><span data-stu-id="d72d2-226">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="d72d2-227">[**技術的深入探討**](active-directory-passwords-how-it-works.md) -hello 帘 toounderstand 後方移它的運作方式</span><span class="sxs-lookup"><span data-stu-id="d72d2-227">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="d72d2-228">[**常見問題集**](active-directory-passwords-faq.md) - 如何？</span><span class="sxs-lookup"><span data-stu-id="d72d2-228">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="d72d2-229">原因為何？</span><span class="sxs-lookup"><span data-stu-id="d72d2-229">Why?</span></span> <span data-ttu-id="d72d2-230">何事？</span><span class="sxs-lookup"><span data-stu-id="d72d2-230">What?</span></span> <span data-ttu-id="d72d2-231">何地？</span><span class="sxs-lookup"><span data-stu-id="d72d2-231">Where?</span></span> <span data-ttu-id="d72d2-232">何人？</span><span class="sxs-lookup"><span data-stu-id="d72d2-232">Who?</span></span> <span data-ttu-id="d72d2-233">何時？</span><span class="sxs-lookup"><span data-stu-id="d72d2-233">When?</span></span> <span data-ttu-id="d72d2-234">-回答您總是想 tooask tooquestions</span><span class="sxs-lookup"><span data-stu-id="d72d2-234">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="d72d2-235">[**疑難排解**](active-directory-passwords-troubleshoot.md) -了解如何 tooresolve 常見問題，我們會看到與 SSPR</span><span class="sxs-lookup"><span data-stu-id="d72d2-235">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>
