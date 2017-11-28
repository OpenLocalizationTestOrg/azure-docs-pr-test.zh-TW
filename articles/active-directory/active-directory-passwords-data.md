---
title: "Azure AD SSPR 資料需求 | Microsoft Docs"
description: "資料需求的 Azure AD 自助式密碼重設以及 toosatisfy 它們"
services: active-directory
keywords: 
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
ms.openlocfilehash: b68a1d7914dcd0bb4509d0e94914dc4309f4463a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a><span data-ttu-id="ba97e-103">部署密碼重設而不需要使用者註冊</span><span class="sxs-lookup"><span data-stu-id="ba97e-103">Deploy password reset without requiring end-user registration</span></span>

<span data-ttu-id="ba97e-104">部署自助密碼重設 (SSPR) 需要驗證資料 toobe 存在。</span><span class="sxs-lookup"><span data-stu-id="ba97e-104">Deploying Self-Service Password Reset (SSPR) requires authentication data toobe present.</span></span> <span data-ttu-id="ba97e-105">某些組織有使用者輸入他們的驗證資料本身，但許多組織都希望 toosynchronize 與 Active Directory 中的現有資料。</span><span class="sxs-lookup"><span data-stu-id="ba97e-105">Some organizations have their users enter their authentication data themselves, but many organizations prefer toosynchronize with existing data in Active Directory.</span></span> <span data-ttu-id="ba97e-106">如果您已正確地格式化資料在內部部署目錄中，並設定[使用快速設定的 Azure AD Connect](./connect/active-directory-aadconnect-get-started-express.md)，資料由可用 tooAzure AD 和 SSPR 與不需要使用者互動。</span><span class="sxs-lookup"><span data-stu-id="ba97e-106">If you have properly formatted data in your on-premises directory, and configure [Azure AD Connect using express settings](./connect/active-directory-aadconnect-get-started-express.md), that data is made available tooAzure AD and SSPR with no user interaction required.</span></span>

<span data-ttu-id="ba97e-107">任何電話號碼必須是在 hello 格式 + CountryCode PhoneNumber 範例: + 1 4255551234 toowork 正確。</span><span class="sxs-lookup"><span data-stu-id="ba97e-107">Any phone numbers must be in hello format +CountryCode PhoneNumber Example: +1 4255551234 toowork properly.</span></span>

> [!NOTE]
> <span data-ttu-id="ba97e-108">密碼重設不支援電話分機。</span><span class="sxs-lookup"><span data-stu-id="ba97e-108">Password reset does not support phone extensions.</span></span> <span data-ttu-id="ba97e-109">即使在 hello + 1 4255551234 X 12345 格式 hello 呼叫開始之前，會移除延伸模組。</span><span class="sxs-lookup"><span data-stu-id="ba97e-109">Even in hello +1 4255551234X12345 format, extensions are removed before hello call is placed.</span></span>

## <a name="fields-populated"></a><span data-ttu-id="ba97e-110">填入的欄位</span><span class="sxs-lookup"><span data-stu-id="ba97e-110">Fields populated</span></span>

<span data-ttu-id="ba97e-111">如果您使用下列 Azure AD Connect hello 中的 hello 預設設定建立對應。</span><span class="sxs-lookup"><span data-stu-id="ba97e-111">If you use hello default settings in Azure AD Connect hello following mappings are made.</span></span>

| <span data-ttu-id="ba97e-112">內部部署 AD</span><span class="sxs-lookup"><span data-stu-id="ba97e-112">On-premises AD</span></span> | <span data-ttu-id="ba97e-113">Azure AD</span><span class="sxs-lookup"><span data-stu-id="ba97e-113">Azure AD</span></span> | <span data-ttu-id="ba97e-114">Azure AD 驗證的連絡資訊</span><span class="sxs-lookup"><span data-stu-id="ba97e-114">Azure AD Authentication contact info</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ba97e-115">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="ba97e-115">telephoneNumber</span></span> | <span data-ttu-id="ba97e-116">辦公室電話</span><span class="sxs-lookup"><span data-stu-id="ba97e-116">Office phone</span></span> | <span data-ttu-id="ba97e-117">備用手機</span><span class="sxs-lookup"><span data-stu-id="ba97e-117">Alternate phone</span></span> |
| <span data-ttu-id="ba97e-118">mobile</span><span class="sxs-lookup"><span data-stu-id="ba97e-118">mobile</span></span> | <span data-ttu-id="ba97e-119">行動電話</span><span class="sxs-lookup"><span data-stu-id="ba97e-119">Mobile phone</span></span> | <span data-ttu-id="ba97e-120">電話</span><span class="sxs-lookup"><span data-stu-id="ba97e-120">Phone</span></span> |


## <a name="security-questions-and-answers"></a><span data-ttu-id="ba97e-121">安全性問題和答案</span><span class="sxs-lookup"><span data-stu-id="ba97e-121">Security questions and answers</span></span>

<span data-ttu-id="ba97e-122">安全性問題和答案會安全地儲存在 Azure AD 租用戶和是透過 hello 只存取 toousers [SSPR 註冊入口網站](https://aka.ms/ssprsetup)。</span><span class="sxs-lookup"><span data-stu-id="ba97e-122">Security questions and answers are stored securely in your Azure AD tenant and are only accessible toousers via hello [SSPR registration portal](https://aka.ms/ssprsetup).</span></span> <span data-ttu-id="ba97e-123">系統管理員無法看到或修改其他使用者的問題和答案 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="ba97e-123">Administrators can't see or modify hello contents of another users questions and answers.</span></span>

### <a name="what-happens-when-a-user-registers"></a><span data-ttu-id="ba97e-124">使用者註冊時的情況</span><span class="sxs-lookup"><span data-stu-id="ba97e-124">What happens when a user registers</span></span>

<span data-ttu-id="ba97e-125">當使用者註冊時，hello 註冊] 頁面上設定下列欄位的 hello:</span><span class="sxs-lookup"><span data-stu-id="ba97e-125">When a user registers, hello registration page sets hello following fields:</span></span>

* <span data-ttu-id="ba97e-126">驗證電話</span><span class="sxs-lookup"><span data-stu-id="ba97e-126">Authentication Phone</span></span>
* <span data-ttu-id="ba97e-127">驗證電子郵件</span><span class="sxs-lookup"><span data-stu-id="ba97e-127">Authentication Email</span></span>
* <span data-ttu-id="ba97e-128">安全性問題和答案</span><span class="sxs-lookup"><span data-stu-id="ba97e-128">Security Questions and Answers</span></span>

<span data-ttu-id="ba97e-129">如果您提供的值**行動電話**或**備用電子郵件**，使用者可以立即使用這些值 tooreset 他們的密碼，即使它們尚未註冊 hello 服務。</span><span class="sxs-lookup"><span data-stu-id="ba97e-129">If you have provided a value for **Mobile Phone** or **Alternate Email**, users can immediately use those values tooreset their passwords, even if they haven't registered for hello service.</span></span> <span data-ttu-id="ba97e-130">此外，使用者 hello 註冊第一次，請參閱這些值，而且如果他們想加以修改。</span><span class="sxs-lookup"><span data-stu-id="ba97e-130">In addition, users see those values when registering for hello first time, and modify them if they wish.</span></span> <span data-ttu-id="ba97e-131">成功註冊之後，這些值將會保存在 hello**驗證電話**和**驗證電子郵件**分別欄位。</span><span class="sxs-lookup"><span data-stu-id="ba97e-131">After they successfully register, these values will be persisted in hello **Authentication Phone** and **Authentication Email** fields, respectively.</span></span>

## <a name="set-and-read-authentication-data-using-powershell"></a><span data-ttu-id="ba97e-132">使用 PowerShell 設定和讀取驗證資料</span><span class="sxs-lookup"><span data-stu-id="ba97e-132">Set and read authentication data using PowerShell</span></span>

<span data-ttu-id="ba97e-133">可以使用 PowerShell 來設定下列欄位的 hello</span><span class="sxs-lookup"><span data-stu-id="ba97e-133">hello following fields can be set using PowerShell</span></span>

* <span data-ttu-id="ba97e-134">替代電子郵件</span><span class="sxs-lookup"><span data-stu-id="ba97e-134">Alternate Email</span></span>
* <span data-ttu-id="ba97e-135">行動電話</span><span class="sxs-lookup"><span data-stu-id="ba97e-135">Mobile Phone</span></span>
* <span data-ttu-id="ba97e-136">辦公室電話 - 只有在未與內部部署目錄同步處理時才能設定</span><span class="sxs-lookup"><span data-stu-id="ba97e-136">Office Phone - Can only be set if not synchronizing with an on-premises directory</span></span>

### <a name="using-powershell-v1"></a><span data-ttu-id="ba97e-137">使用 PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="ba97e-137">Using PowerShell V1</span></span>

<span data-ttu-id="ba97e-138">tooget 開始，您需要太[下載並安裝 hello Azure AD PowerShell 模組](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule)。</span><span class="sxs-lookup"><span data-stu-id="ba97e-138">tooget started, you need too[download and install hello Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span></span> <span data-ttu-id="ba97e-139">一旦您已經安裝，您可以依照每個欄位，請遵循 tooconfigure 的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="ba97e-139">Once you have it installed, you can follow hello steps that follow tooconfigure each field.</span></span>

#### <a name="set-authentication-data-with-powershell-v1"></a><span data-ttu-id="ba97e-140">使用 PowerShell V1 設定驗證資料</span><span class="sxs-lookup"><span data-stu-id="ba97e-140">Set Authentication Data with PowerShell V1</span></span>

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a><span data-ttu-id="ba97e-141">使用 PowerShellPowerShell V1 讀取驗證資料</span><span class="sxs-lookup"><span data-stu-id="ba97e-141">Read Authentication Data with PowerShellPowerShell V1</span></span>

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-hello-commands-that-follow"></a><span data-ttu-id="ba97e-142">驗證電話驗證電子郵件可以只讀取和使用 Powershell V1 使用 hello 命令後面</span><span class="sxs-lookup"><span data-stu-id="ba97e-142">Authentication Phone and Authentication Email can only be read using Powershell V1 using hello commands that follow</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a><span data-ttu-id="ba97e-143">使用 PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="ba97e-143">Using PowerShell V2</span></span>

<span data-ttu-id="ba97e-144">tooget 開始，您需要太[下載並安裝 Azure AD V2 hello PowerShell 模組](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md)。</span><span class="sxs-lookup"><span data-stu-id="ba97e-144">tooget started, you need too[download and install hello Azure AD V2 PowerShell module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span></span> <span data-ttu-id="ba97e-145">一旦您已經安裝，您可以依照每個欄位，請遵循 tooconfigure 的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="ba97e-145">Once you have it installed, you can follow hello steps that follow tooconfigure each field.</span></span>

<span data-ttu-id="ba97e-146">快速從最新版本的 PowerShell 支援 Find-module、 install-module tooinstall 執行這些命令 （hello 第一行只檢查 toosee 如果安裝的話）：</span><span class="sxs-lookup"><span data-stu-id="ba97e-146">tooinstall quickly from recent versions of PowerShell that support Install-Module, run these commands (hello first line simply checks toosee if it's installed already):</span></span>

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a><span data-ttu-id="ba97e-147">使用 PowerShell V2 設定驗證資料</span><span class="sxs-lookup"><span data-stu-id="ba97e-147">Set Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a><span data-ttu-id="ba97e-148">使用 PowerShell V2 讀取驗證資料</span><span class="sxs-lookup"><span data-stu-id="ba97e-148">Read Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a><span data-ttu-id="ba97e-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ba97e-149">Next steps</span></span>

<span data-ttu-id="ba97e-150">hello 下列連結提供有關密碼重設使用 Azure AD 的其他資訊</span><span class="sxs-lookup"><span data-stu-id="ba97e-150">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="ba97e-151">[**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理</span><span class="sxs-lookup"><span data-stu-id="ba97e-151">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="ba97e-152">[**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權</span><span class="sxs-lookup"><span data-stu-id="ba97e-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="ba97e-153">[**首度發行**](active-directory-passwords-best-practices.md) -計劃和部署 SSPR tooyour 使用者 hello 指引，請參閱</span><span class="sxs-lookup"><span data-stu-id="ba97e-153">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="ba97e-154">[**自訂**](active-directory-passwords-customize.md) -自訂的 hello SSPR 體驗您的公司 hello 外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="ba97e-154">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="ba97e-155">[**原則**](active-directory-passwords-policy.md) - 了解並設定 Azure AD 密碼原則</span><span class="sxs-lookup"><span data-stu-id="ba97e-155">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="ba97e-156">[**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能</span><span class="sxs-lookup"><span data-stu-id="ba97e-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="ba97e-157">[**技術的深入探討**](active-directory-passwords-how-it-works.md) -hello 帘 toounderstand 後方移它的運作方式</span><span class="sxs-lookup"><span data-stu-id="ba97e-157">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="ba97e-158">[**常見問題集**](active-directory-passwords-faq.md) - 如何？</span><span class="sxs-lookup"><span data-stu-id="ba97e-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="ba97e-159">原因為何？</span><span class="sxs-lookup"><span data-stu-id="ba97e-159">Why?</span></span> <span data-ttu-id="ba97e-160">何事？</span><span class="sxs-lookup"><span data-stu-id="ba97e-160">What?</span></span> <span data-ttu-id="ba97e-161">何地？</span><span class="sxs-lookup"><span data-stu-id="ba97e-161">Where?</span></span> <span data-ttu-id="ba97e-162">何人？</span><span class="sxs-lookup"><span data-stu-id="ba97e-162">Who?</span></span> <span data-ttu-id="ba97e-163">何時？</span><span class="sxs-lookup"><span data-stu-id="ba97e-163">When?</span></span> <span data-ttu-id="ba97e-164">-回答您總是想 tooask tooquestions</span><span class="sxs-lookup"><span data-stu-id="ba97e-164">- Answers tooquestions you always wanted tooask</span></span>
* <span data-ttu-id="ba97e-165">[**疑難排解**](active-directory-passwords-troubleshoot.md) -了解如何 tooresolve 常見問題，我們會看到與 SSPR</span><span class="sxs-lookup"><span data-stu-id="ba97e-165">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>
