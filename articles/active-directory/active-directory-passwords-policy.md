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
ms.openlocfilehash: 4b35c5d126375735f070a7fe2331896c524b5a61
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="password-policies-and-restrictions-in-azure-active-directory"></a><span data-ttu-id="c33ed-104">密碼原則和 Azure Active Directory 中的限制</span><span class="sxs-lookup"><span data-stu-id="c33ed-104">Password policies and restrictions in Azure Active Directory</span></span>

<span data-ttu-id="c33ed-105">本文說明與儲存在 Azure AD 租用戶中的使用者帳戶相關聯的密碼原則和複雜性需求。</span><span class="sxs-lookup"><span data-stu-id="c33ed-105">This article describes the password policies and complexity requirements associated with user accounts stored in your Azure AD tenant.</span></span>

## <a name="administrator-password-policy-differences"></a><span data-ttu-id="c33ed-106">系統管理員密碼原則差異</span><span class="sxs-lookup"><span data-stu-id="c33ed-106">Administrator password policy differences</span></span>

<span data-ttu-id="c33ed-107">Microsoft 會對任何系統管理員角色 (全域管理員、技術支援系統管理員、密碼管理員等) 強制執行強式預設「雙閘道」密碼重設原則</span><span class="sxs-lookup"><span data-stu-id="c33ed-107">Microsoft enforces a strong default **two gate** password reset policy for any Azure administrator role (Example: Global Administrator, Helpdesk Administrator, Password Administrator, etc.)</span></span>

<span data-ttu-id="c33ed-108">這會讓系統管理員無法使用安全性問題，並強制執行下列各項。</span><span class="sxs-lookup"><span data-stu-id="c33ed-108">This disables administrators from using security questions and enforces the following.</span></span>

<span data-ttu-id="c33ed-109">在下列狀況下適用需要兩種驗證資料 (電子郵件地址「和」電話號碼) 的雙關卡原則</span><span class="sxs-lookup"><span data-stu-id="c33ed-109">Two gate policy, requiring two pieces of authentication data (email address **and** phone number), applies in the following circumstances</span></span>

* <span data-ttu-id="c33ed-110">所有的 Azure 系統管理員角色</span><span class="sxs-lookup"><span data-stu-id="c33ed-110">All Azure administrator roles</span></span>
  * <span data-ttu-id="c33ed-111">服務台系統管理員</span><span class="sxs-lookup"><span data-stu-id="c33ed-111">Helpdesk Administrator</span></span>
  * <span data-ttu-id="c33ed-112">服務支援管理員</span><span class="sxs-lookup"><span data-stu-id="c33ed-112">Service Support Administrator</span></span>
  * <span data-ttu-id="c33ed-113">計費管理員</span><span class="sxs-lookup"><span data-stu-id="c33ed-113">Billing Administrator</span></span>
  * <span data-ttu-id="c33ed-114">合作夥伴第 1 層支援</span><span class="sxs-lookup"><span data-stu-id="c33ed-114">Partner Tier1 Support</span></span>
  * <span data-ttu-id="c33ed-115">合作夥伴第 2 層支援</span><span class="sxs-lookup"><span data-stu-id="c33ed-115">Partner Tier2 Support</span></span>
  * <span data-ttu-id="c33ed-116">Exchange 服務管理員</span><span class="sxs-lookup"><span data-stu-id="c33ed-116">Exchange Service Administrator</span></span>
  * <span data-ttu-id="c33ed-117">Lync 服務管理員</span><span class="sxs-lookup"><span data-stu-id="c33ed-117">Lync Service Administrator</span></span>
  * <span data-ttu-id="c33ed-118">使用者帳戶管理員</span><span class="sxs-lookup"><span data-stu-id="c33ed-118">User Account Administrator</span></span>
  * <span data-ttu-id="c33ed-119">目錄撰寫者</span><span class="sxs-lookup"><span data-stu-id="c33ed-119">Directory Writers</span></span>
  * <span data-ttu-id="c33ed-120">全域管理員/公司系統管理員</span><span class="sxs-lookup"><span data-stu-id="c33ed-120">Global Administrator/Company Administrator</span></span>
  * <span data-ttu-id="c33ed-121">SharePoint 服務管理員</span><span class="sxs-lookup"><span data-stu-id="c33ed-121">SharePoint Service Administrator</span></span>
  * <span data-ttu-id="c33ed-122">規範管理員</span><span class="sxs-lookup"><span data-stu-id="c33ed-122">Compliance Administrator</span></span>
  * <span data-ttu-id="c33ed-123">應用程式系統管理員</span><span class="sxs-lookup"><span data-stu-id="c33ed-123">Application Administrator</span></span>
  * <span data-ttu-id="c33ed-124">安全性系統管理員</span><span class="sxs-lookup"><span data-stu-id="c33ed-124">Security Administrator</span></span>
  * <span data-ttu-id="c33ed-125">特殊權限角色管理員</span><span class="sxs-lookup"><span data-stu-id="c33ed-125">Privileged Role Administrator</span></span>
  * <span data-ttu-id="c33ed-126">Intune 服務管理員</span><span class="sxs-lookup"><span data-stu-id="c33ed-126">Intune Service Administrator</span></span>
  * <span data-ttu-id="c33ed-127">應用程式 Proxy 服務管理員</span><span class="sxs-lookup"><span data-stu-id="c33ed-127">Application Proxy Service Administrator</span></span>
  * <span data-ttu-id="c33ed-128">CRM 服務管理員</span><span class="sxs-lookup"><span data-stu-id="c33ed-128">CRM Service Administrator</span></span>
  * <span data-ttu-id="c33ed-129">Power BI 服務管理員</span><span class="sxs-lookup"><span data-stu-id="c33ed-129">Power BI Service Administrator</span></span>
  
* <span data-ttu-id="c33ed-130">試用已經過 30 天**或**</span><span class="sxs-lookup"><span data-stu-id="c33ed-130">30 days have elapsed in a trial **OR**</span></span>
* <span data-ttu-id="c33ed-131">虛名網域存在於 (contoso.com) **或**</span><span class="sxs-lookup"><span data-stu-id="c33ed-131">Vanity domain is present (contoso.com) **OR**</span></span>
* <span data-ttu-id="c33ed-132">Azure AD Connect 正在同步處理內部部署目錄中的身分識別</span><span class="sxs-lookup"><span data-stu-id="c33ed-132">Azure AD Connect is synchronizing identities from your on-premises directory</span></span>

### <a name="exceptions"></a><span data-ttu-id="c33ed-133">例外狀況</span><span class="sxs-lookup"><span data-stu-id="c33ed-133">Exceptions</span></span>
<span data-ttu-id="c33ed-134">在下列狀況下適用需要一種驗證資料 (電子郵件地址「或」電話號碼) 的單關卡原則</span><span class="sxs-lookup"><span data-stu-id="c33ed-134">One gate policy, requiring one piece of authentication data (email address **or** phone number), applies in the following circumstances</span></span>

* <span data-ttu-id="c33ed-135">試用的前 30 天**或**</span><span class="sxs-lookup"><span data-stu-id="c33ed-135">First 30 days of a trial **OR**</span></span>
* <span data-ttu-id="c33ed-136">虛名網域不存在 (*.onmicrosoft.com) **且** Azure AD Connect 並未同步處理身分識別</span><span class="sxs-lookup"><span data-stu-id="c33ed-136">Vanity domain is not present (*.onmicrosoft.com) **AND** Azure AD Connect is not synchronizing identities</span></span>


## <a name="userprincipalname-policies-that-apply-to-all-user-accounts"></a><span data-ttu-id="c33ed-137">適用於所有使用者帳戶的 UserPrincipalName 原則</span><span class="sxs-lookup"><span data-stu-id="c33ed-137">UserPrincipalName policies that apply to all user accounts</span></span>

<span data-ttu-id="c33ed-138">每個需要登入 Azure AD 的使用者帳戶都必須具有與其帳戶相關聯的唯一使用者主體名稱 (UPN) 屬性值。</span><span class="sxs-lookup"><span data-stu-id="c33ed-138">Every user account that needs to sign in to Azure AD must have a unique user principal name (UPN) attribute value associated with their account.</span></span> <span data-ttu-id="c33ed-139">下表概述的原則適用於已同步至雲端的內部部署 Active Directory 使用者帳戶和僅限雲端的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="c33ed-139">The table below outlines the polices that apply to both on-premises Active Directory user accounts synchronized to the cloud and to cloud-only user accounts.</span></span>

| <span data-ttu-id="c33ed-140">屬性</span><span class="sxs-lookup"><span data-stu-id="c33ed-140">Property</span></span> | <span data-ttu-id="c33ed-141">UserPrincipalName 需求</span><span class="sxs-lookup"><span data-stu-id="c33ed-141">UserPrincipalName requirements</span></span> |
| --- | --- |
| <span data-ttu-id="c33ed-142">允許的字元</span><span class="sxs-lookup"><span data-stu-id="c33ed-142">Characters allowed</span></span> |<ul> <li><span data-ttu-id="c33ed-143">A – Z</span><span class="sxs-lookup"><span data-stu-id="c33ed-143">A – Z</span></span></li> <li><span data-ttu-id="c33ed-144">a - z</span><span class="sxs-lookup"><span data-stu-id="c33ed-144">a - z</span></span></li><li><span data-ttu-id="c33ed-145">0 – 9</span><span class="sxs-lookup"><span data-stu-id="c33ed-145">0 – 9</span></span></li> <li> <span data-ttu-id="c33ed-146">。</span><span class="sxs-lookup"><span data-stu-id="c33ed-146">.</span></span><span data-ttu-id="c33ed-147"> - \_ !</span><span class="sxs-lookup"><span data-stu-id="c33ed-147"> - \_ !</span></span> <span data-ttu-id="c33ed-148">\# ^ \~</span><span class="sxs-lookup"><span data-stu-id="c33ed-148">\# ^ \~</span></span></li></ul> |
| <span data-ttu-id="c33ed-149">不允許的字元</span><span class="sxs-lookup"><span data-stu-id="c33ed-149">Characters not allowed</span></span> |<ul> <li><span data-ttu-id="c33ed-150">任何不是用來分隔使用者名稱和網域的 '@' 字元。</span><span class="sxs-lookup"><span data-stu-id="c33ed-150">Any '@' character that is not separating the user name from the domain.</span></span></li> <li><span data-ttu-id="c33ed-151">'@' 符號前面不可直接包含句點字元 '.'</span><span class="sxs-lookup"><span data-stu-id="c33ed-151">Cannot contain a period character '.' immediately preceding the '@' symbol</span></span></li></ul> |
| <span data-ttu-id="c33ed-152">長度限制</span><span class="sxs-lookup"><span data-stu-id="c33ed-152">Length constraints</span></span> |<ul> <li><span data-ttu-id="c33ed-153">總長度不得超過 113 個字元</span><span class="sxs-lookup"><span data-stu-id="c33ed-153">Total length must not exceed 113 characters</span></span></li><li><span data-ttu-id="c33ed-154">'@' 符號前為 64 個字元</span><span class="sxs-lookup"><span data-stu-id="c33ed-154">64 characters before the ‘@’ symbol</span></span></li><li><span data-ttu-id="c33ed-155">'@' 符號後為 48 個字元</span><span class="sxs-lookup"><span data-stu-id="c33ed-155">48 characters after the ‘@’ symbol</span></span></li></ul> |

## <a name="password-policies-that-apply-only-to-cloud-user-accounts"></a><span data-ttu-id="c33ed-156">僅適用於雲端使用者帳戶的密碼原則</span><span class="sxs-lookup"><span data-stu-id="c33ed-156">Password policies that apply only to cloud user accounts</span></span>

<span data-ttu-id="c33ed-157">下表描述可套用至在 Azure AD 中建立及管理的使用者帳戶的可用密碼原則設定。</span><span class="sxs-lookup"><span data-stu-id="c33ed-157">The following table describes the available password policy settings that can be applied to user accounts that are created and managed in Azure AD.</span></span>

| <span data-ttu-id="c33ed-158">屬性</span><span class="sxs-lookup"><span data-stu-id="c33ed-158">Property</span></span> | <span data-ttu-id="c33ed-159">需求</span><span class="sxs-lookup"><span data-stu-id="c33ed-159">Requirements</span></span> |
| --- | --- |
| <span data-ttu-id="c33ed-160">允許的字元</span><span class="sxs-lookup"><span data-stu-id="c33ed-160">Characters allowed</span></span> |<ul><li><span data-ttu-id="c33ed-161">A – Z</span><span class="sxs-lookup"><span data-stu-id="c33ed-161">A – Z</span></span></li><li><span data-ttu-id="c33ed-162">a - z</span><span class="sxs-lookup"><span data-stu-id="c33ed-162">a - z</span></span></li><li><span data-ttu-id="c33ed-163">0 – 9</span><span class="sxs-lookup"><span data-stu-id="c33ed-163">0 – 9</span></span></li> <li><span data-ttu-id="c33ed-164">@ # $ % ^ & * - _ !</span><span class="sxs-lookup"><span data-stu-id="c33ed-164">@ # $ % ^ & * - _ !</span></span> <span data-ttu-id="c33ed-165">+ = [ ] { } &#124; \ : ‘ , .</span><span class="sxs-lookup"><span data-stu-id="c33ed-165">+ = [ ] { } &#124; \ : ‘ , .</span></span> <span data-ttu-id="c33ed-166">?</span><span class="sxs-lookup"><span data-stu-id="c33ed-166">?</span></span> <span data-ttu-id="c33ed-167">/ \` ~ “ ( ) ;</span><span class="sxs-lookup"><span data-stu-id="c33ed-167">/ \` ~ “ ( ) ;</span></span></li></ul> |
| <span data-ttu-id="c33ed-168">不允許的字元</span><span class="sxs-lookup"><span data-stu-id="c33ed-168">Characters not allowed</span></span> |<ul><li><span data-ttu-id="c33ed-169">Unicode 字元</span><span class="sxs-lookup"><span data-stu-id="c33ed-169">Unicode characters</span></span></li><li><span data-ttu-id="c33ed-170">空格</span><span class="sxs-lookup"><span data-stu-id="c33ed-170">Spaces</span></span></li><li> <span data-ttu-id="c33ed-171">**僅限使用強式密碼**：'@' 符號前面不能直接包含點字元 '.'</span><span class="sxs-lookup"><span data-stu-id="c33ed-171">**Strong passwords only**: Cannot contain a dot character '.' immediately preceding the '@' symbol</span></span></li></ul> |
| <span data-ttu-id="c33ed-172">密碼限制</span><span class="sxs-lookup"><span data-stu-id="c33ed-172">Password restrictions</span></span> |<ul><li><span data-ttu-id="c33ed-173">最少 8 個字元，最多 16 個字元</span><span class="sxs-lookup"><span data-stu-id="c33ed-173">8 characters minimum and 16 characters maximum</span></span></li><li><span data-ttu-id="c33ed-174">**僅限使用增強式密碼**︰需要下列 4 種字元中的 3 種︰</span><span class="sxs-lookup"><span data-stu-id="c33ed-174">**Strong passwords only**: Requires 3 out of 4 of the following:</span></span><ul><li><span data-ttu-id="c33ed-175">小寫字元</span><span class="sxs-lookup"><span data-stu-id="c33ed-175">Lowercase characters</span></span></li><li><span data-ttu-id="c33ed-176">大寫字元</span><span class="sxs-lookup"><span data-stu-id="c33ed-176">Uppercase characters</span></span></li><li><span data-ttu-id="c33ed-177">數字 (0-9)</span><span class="sxs-lookup"><span data-stu-id="c33ed-177">Numbers (0-9)</span></span></li><li><span data-ttu-id="c33ed-178">符號 (請參閱上面的密碼限制)</span><span class="sxs-lookup"><span data-stu-id="c33ed-178">Symbols (see password restrictions above)</span></span></li></ul></li></ul> |
| <span data-ttu-id="c33ed-179">密碼到期時間</span><span class="sxs-lookup"><span data-stu-id="c33ed-179">Password expiry duration</span></span> |<ul><li><span data-ttu-id="c33ed-180">預設值：**90** 天</span><span class="sxs-lookup"><span data-stu-id="c33ed-180">Default value: **90** days</span></span> </li><li><span data-ttu-id="c33ed-181">值可透過適用於 Windows PowerShell 的 Azure Active Directory 模組使用 Set-MsolPasswordPolicy Cmdlet 設定。</span><span class="sxs-lookup"><span data-stu-id="c33ed-181">Value is configurable using the Set-MsolPasswordPolicy cmdlet from the Azure Active Directory Module for Windows PowerShell.</span></span></li></ul> |
| <span data-ttu-id="c33ed-182">密碼到期通知</span><span class="sxs-lookup"><span data-stu-id="c33ed-182">Password expiry notification</span></span> |<ul><li><span data-ttu-id="c33ed-183">預設值：**14** 天 (密碼到期之前)</span><span class="sxs-lookup"><span data-stu-id="c33ed-183">Default value: **14** days (before password expires)</span></span></li><li><span data-ttu-id="c33ed-184">您可使用 Set-MsolPasswordPolicy Cmdlet 設定此值。</span><span class="sxs-lookup"><span data-stu-id="c33ed-184">Value is configurable using the Set-MsolPasswordPolicy cmdlet.</span></span></li></ul> |
| <span data-ttu-id="c33ed-185">密碼到期</span><span class="sxs-lookup"><span data-stu-id="c33ed-185">Password Expiry</span></span> |<ul><li><span data-ttu-id="c33ed-186">預設值︰**false** 天 (表示已啟用密碼到期)</span><span class="sxs-lookup"><span data-stu-id="c33ed-186">Default value: **false** days (indicates that password expiry is enabled)</span></span> </li><li><span data-ttu-id="c33ed-187">可以針對個別使用者帳戶使用 Set-msoluser Cmdlet 設定值。</span><span class="sxs-lookup"><span data-stu-id="c33ed-187">Value can be configured for individual user accounts using the Set-MsolUser cmdlet.</span></span> </li></ul> |
| <span data-ttu-id="c33ed-188">密碼**變更**歷程記錄</span><span class="sxs-lookup"><span data-stu-id="c33ed-188">Password **change** history</span></span> |<span data-ttu-id="c33ed-189">**變更**密碼時，**無法**再次使用上次的密碼。</span><span class="sxs-lookup"><span data-stu-id="c33ed-189">Last password **cannot** be used again when **changing** a password.</span></span> |
| <span data-ttu-id="c33ed-190">密碼**重設**歷程記錄</span><span class="sxs-lookup"><span data-stu-id="c33ed-190">Password **reset** history</span></span> | <span data-ttu-id="c33ed-191">**重設**遺忘的密碼時，**可以**再次使用上次的密碼。</span><span class="sxs-lookup"><span data-stu-id="c33ed-191">Last password **may** be used again when **resetting** a forgotten password.</span></span> |
| <span data-ttu-id="c33ed-192">帳戶鎖定</span><span class="sxs-lookup"><span data-stu-id="c33ed-192">Account Lockout</span></span> |<span data-ttu-id="c33ed-193">10 次嘗試登入失敗 (錯誤密碼) 之後，使用者會被封鎖一分鐘。</span><span class="sxs-lookup"><span data-stu-id="c33ed-193">After 10 unsuccessful sign-in attempts (wrong password), the user will be locked out for one minute.</span></span> <span data-ttu-id="c33ed-194">後續嘗試登入的錯誤會增加使用者被封鎖的時間。</span><span class="sxs-lookup"><span data-stu-id="c33ed-194">Further incorrect sign-in attempts lock out the user for increasing durations.</span></span> |

## <a name="set-password-expiration-policies-in-azure-active-directory"></a><span data-ttu-id="c33ed-195">在 Azure Active Directory 中設定密碼到期原則</span><span class="sxs-lookup"><span data-stu-id="c33ed-195">Set password expiration policies in Azure Active Directory</span></span>

<span data-ttu-id="c33ed-196">Microsoft 雲端服務的全域管理員可以使用「適用於 Windows PowerShell 的 Microsoft Azure Active Directory 模組」，將使用者密碼設為不會到期。</span><span class="sxs-lookup"><span data-stu-id="c33ed-196">A global administrator for a Microsoft cloud service can use the Microsoft Azure Active Directory Module for Windows PowerShell to set up user passwords not to expire.</span></span> <span data-ttu-id="c33ed-197">您亦可使用 Windows PowerShell Cmdlet 移除永不到期組態，或是查看哪些使用者密碼設為不會到期。</span><span class="sxs-lookup"><span data-stu-id="c33ed-197">You can also use Windows PowerShell cmdlets to remove the never-expires configuration, or to see which user passwords are set up not to expire.</span></span> <span data-ttu-id="c33ed-198">本指引適用於其他提供者 (例如 Microsoft Intune 和 Office 365)，他們也仰賴 Microsoft Azure Active Directory 提供身分識別和目錄服務。</span><span class="sxs-lookup"><span data-stu-id="c33ed-198">This guidance applies to other providers such as Microsoft Intune and Office 365, which also rely on Microsoft Azure Active Directory for identity and directory services.</span></span>

> [!NOTE]
> <span data-ttu-id="c33ed-199">您僅可將未透過目錄同步作業執行同步處理的使用者帳戶密碼，設定為不會到期。</span><span class="sxs-lookup"><span data-stu-id="c33ed-199">Only passwords for user accounts that are not synchronized through directory synchronization can be configured to not expire.</span></span> <span data-ttu-id="c33ed-200">如需有關目錄同步作業，請參閱 [Connect AD 與 Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)。</span><span class="sxs-lookup"><span data-stu-id="c33ed-200">For more information about directory synchronization see[Connect AD with Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect).</span></span>
>
>

## <a name="set-or-check-password-policies-using-powershell"></a><span data-ttu-id="c33ed-201">使用 PowerShell 設定或檢查密碼原則</span><span class="sxs-lookup"><span data-stu-id="c33ed-201">Set or check password policies using PowerShell</span></span>

<span data-ttu-id="c33ed-202">首先，您必須[下載並安裝 Azure AD PowerShell 模組](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0)。</span><span class="sxs-lookup"><span data-stu-id="c33ed-202">To get started, you need to [download and install the Azure AD PowerShell module](https://docs.microsoft.com/powershell/module/Azuread/?view=azureadps-2.0).</span></span> <span data-ttu-id="c33ed-203">一旦安裝好，即可依照下列步驟設定每一個欄位。</span><span class="sxs-lookup"><span data-stu-id="c33ed-203">Once you have it installed, you can follow the steps below to configure each field.</span></span>

### <a name="how-to-check-expiration-policy-for-a-password"></a><span data-ttu-id="c33ed-204">如何檢查密碼到期原則</span><span class="sxs-lookup"><span data-stu-id="c33ed-204">How to check expiration policy for a password</span></span>
1. <span data-ttu-id="c33ed-205">使用您公司的管理員認證連線至 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="c33ed-205">Connect to Windows PowerShell using your company administrator credentials.</span></span>
2. <span data-ttu-id="c33ed-206">執行下列其中一個命令：</span><span class="sxs-lookup"><span data-stu-id="c33ed-206">Execute one of the following commands:</span></span>

   * <span data-ttu-id="c33ed-207">若要查看單一使用者的密碼是否設為永久有效，請透過使用者主體名稱 (UPN) (例如 aprilr@contoso.onmicrosoft.com)，或是您想要檢查之使用者的使用者識別碼，來執行下列 Cmdlet：`Get-MSOLUser -UserPrincipalName <user ID> | Select PasswordNeverExpires`</span><span class="sxs-lookup"><span data-stu-id="c33ed-207">To see whether a single user’s password is set to never expire, run the following cmdlet by using the user principal name (UPN) (for example, aprilr@contoso.onmicrosoft.com) or the user ID of the user you want to check: `Get-MSOLUser -UserPrincipalName <user ID> | Select PasswordNeverExpires`</span></span>
   * <span data-ttu-id="c33ed-208">若要查看所有使用者的「密碼永久有效」設定，請執行下列 Cmdlet：`Get-MSOLUser | Select UserPrincipalName, PasswordNeverExpires`</span><span class="sxs-lookup"><span data-stu-id="c33ed-208">To see the "Password never expires" setting for all users, run the following cmdlet: `Get-MSOLUser | Select UserPrincipalName, PasswordNeverExpires`</span></span>

### <a name="set-a-password-to-expire"></a><span data-ttu-id="c33ed-209">設定密碼到期</span><span class="sxs-lookup"><span data-stu-id="c33ed-209">Set a password to expire</span></span>

1. <span data-ttu-id="c33ed-210">使用您公司的管理員認證連線至 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="c33ed-210">Connect to Windows PowerShell using your company administrator credentials.</span></span>
2. <span data-ttu-id="c33ed-211">執行下列其中一個命令：</span><span class="sxs-lookup"><span data-stu-id="c33ed-211">Execute one of the following commands:</span></span>

   * <span data-ttu-id="c33ed-212">若要將某位使用者的密碼設為會到期，請透過使用使用者主體名稱 (UPN) 或使用者的使用者識別碼，執行下列 Cmdlet：`Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $false`</span><span class="sxs-lookup"><span data-stu-id="c33ed-212">To set the password of one user so that the password expires, run the following cmdlet by using the user principal name (UPN) or the user ID of the user: `Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $false`</span></span>
   * <span data-ttu-id="c33ed-213">若要將組織中所有使用者的密碼設為會到期，請使用下列 Cmdlet：`Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $false`</span><span class="sxs-lookup"><span data-stu-id="c33ed-213">To set the passwords of all users in the organization so that they expire, use the following cmdlet: `Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $false`</span></span>

### <a name="set-a-password-to-never-expire"></a><span data-ttu-id="c33ed-214">設定密碼為永久有效</span><span class="sxs-lookup"><span data-stu-id="c33ed-214">Set a password to never expire</span></span>

1. <span data-ttu-id="c33ed-215">使用您公司的管理員認證連線至 Windows PowerShell。</span><span class="sxs-lookup"><span data-stu-id="c33ed-215">Connect to Windows PowerShell using your company administrator credentials.</span></span>
2. <span data-ttu-id="c33ed-216">執行下列其中一個命令：</span><span class="sxs-lookup"><span data-stu-id="c33ed-216">Execute one of the following commands:</span></span>

   * <span data-ttu-id="c33ed-217">若要將某位使用者的密碼設為永久有效，請透過使用使用者主體名稱 (UPN) 或使用者的使用者識別碼，來執行下列 Cmdlet： `Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $true`</span><span class="sxs-lookup"><span data-stu-id="c33ed-217">To set the password of one user to never expire, run the following cmdlet by using the user principal name (UPN) or the user ID of the user: `Set-MsolUser -UserPrincipalName <user ID> -PasswordNeverExpires $true`</span></span>
   * <span data-ttu-id="c33ed-218">若要將組織中所有使用者的密碼設為永久有效，請執行下列 Cmdlet： `Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $true`</span><span class="sxs-lookup"><span data-stu-id="c33ed-218">To set the passwords of all the users in an organization to never expire, run the following cmdlet: `Get-MSOLUser | Set-MsolUser -PasswordNeverExpires $true`</span></span>

## <a name="next-steps"></a><span data-ttu-id="c33ed-219">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c33ed-219">Next steps</span></span>

<span data-ttu-id="c33ed-220">下列連結提供有關使用 Azure AD 重設密碼的其他資訊</span><span class="sxs-lookup"><span data-stu-id="c33ed-220">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="c33ed-221">[**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理</span><span class="sxs-lookup"><span data-stu-id="c33ed-221">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="c33ed-222">[**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權</span><span class="sxs-lookup"><span data-stu-id="c33ed-222">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="c33ed-223">[**資料**](active-directory-passwords-data.md) -了解所需的資料以及如何將它使用於密碼管理</span><span class="sxs-lookup"><span data-stu-id="c33ed-223">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="c33ed-224">[**推出**](active-directory-passwords-best-practices.md) - 使用此處提供的指引來規劃 SSPR 並將它部署至使用者</span><span class="sxs-lookup"><span data-stu-id="c33ed-224">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="c33ed-225">[**自訂**](active-directory-passwords-customize.md) - 為您的公司自訂 SSPR 體驗的外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="c33ed-225">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="c33ed-226">[**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能</span><span class="sxs-lookup"><span data-stu-id="c33ed-226">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="c33ed-227">[**技術性深入探討**](active-directory-passwords-how-it-works.md) - 深入探索以了解其運作方式</span><span class="sxs-lookup"><span data-stu-id="c33ed-227">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="c33ed-228">[**常見問題集**](active-directory-passwords-faq.md) - 如何？</span><span class="sxs-lookup"><span data-stu-id="c33ed-228">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="c33ed-229">原因為何？</span><span class="sxs-lookup"><span data-stu-id="c33ed-229">Why?</span></span> <span data-ttu-id="c33ed-230">何事？</span><span class="sxs-lookup"><span data-stu-id="c33ed-230">What?</span></span> <span data-ttu-id="c33ed-231">何地？</span><span class="sxs-lookup"><span data-stu-id="c33ed-231">Where?</span></span> <span data-ttu-id="c33ed-232">何人？</span><span class="sxs-lookup"><span data-stu-id="c33ed-232">Who?</span></span> <span data-ttu-id="c33ed-233">何時？</span><span class="sxs-lookup"><span data-stu-id="c33ed-233">When?</span></span> <span data-ttu-id="c33ed-234">- -您一直想要詢問之問題的答案</span><span class="sxs-lookup"><span data-stu-id="c33ed-234">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="c33ed-235">[**疑難排解**](active-directory-passwords-troubleshoot.md) - 了解如何解決我們看到的 SSPR 常見問題</span><span class="sxs-lookup"><span data-stu-id="c33ed-235">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>
