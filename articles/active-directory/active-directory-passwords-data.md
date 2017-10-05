---
title: "Azure AD SSPR 資料需求 | Microsoft Docs"
description: "Azure AD 自助式密碼重設的資料需求和如何滿足這些需求"
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
ms.openlocfilehash: 2d1afd2d1265b371e0d311ed70fffbc55874b0a7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-password-reset-without-requiring-end-user-registration"></a><span data-ttu-id="c58ce-103">部署密碼重設而不需要使用者註冊</span><span class="sxs-lookup"><span data-stu-id="c58ce-103">Deploy password reset without requiring end-user registration</span></span>

<span data-ttu-id="c58ce-104">需要有驗證資料才能部署自助式密碼重設 (SSPR)。</span><span class="sxs-lookup"><span data-stu-id="c58ce-104">Deploying Self-Service Password Reset (SSPR) requires authentication data to be present.</span></span> <span data-ttu-id="c58ce-105">某些組織會要求使用者自行輸入其驗證資料，但許多組織會選擇與 Active Directory 中現有的資料同步處理。</span><span class="sxs-lookup"><span data-stu-id="c58ce-105">Some organizations have their users enter their authentication data themselves, but many organizations prefer to synchronize with existing data in Active Directory.</span></span> <span data-ttu-id="c58ce-106">如果您已正確格式化內部部署目錄中的資料，並[使用快速設定完成 Azure AD Connect 設定](./connect/active-directory-aadconnect-get-started-express.md)，則 Azure AD 和 SSPR 可取用該資料，而不需要使用者互動。</span><span class="sxs-lookup"><span data-stu-id="c58ce-106">If you have properly formatted data in your on-premises directory, and configure [Azure AD Connect using express settings](./connect/active-directory-aadconnect-get-started-express.md), that data is made available to Azure AD and SSPR with no user interaction required.</span></span>

<span data-ttu-id="c58ce-107">任何電話號碼必須是這種格式才有效：+國碼 電話號碼。範例：+1 4255551234。</span><span class="sxs-lookup"><span data-stu-id="c58ce-107">Any phone numbers must be in the format +CountryCode PhoneNumber Example: +1 4255551234 to work properly.</span></span>

> [!NOTE]
> <span data-ttu-id="c58ce-108">密碼重設不支援電話分機。</span><span class="sxs-lookup"><span data-stu-id="c58ce-108">Password reset does not support phone extensions.</span></span> <span data-ttu-id="c58ce-109">即使是 +1 4255551234X12345 格式，撥號之前都會移除分機號碼。</span><span class="sxs-lookup"><span data-stu-id="c58ce-109">Even in the +1 4255551234X12345 format, extensions are removed before the call is placed.</span></span>

## <a name="fields-populated"></a><span data-ttu-id="c58ce-110">填入的欄位</span><span class="sxs-lookup"><span data-stu-id="c58ce-110">Fields populated</span></span>

<span data-ttu-id="c58ce-111">如果您使用 Azure AD Connect 的預設設定，則會建立下列對應。</span><span class="sxs-lookup"><span data-stu-id="c58ce-111">If you use the default settings in Azure AD Connect the following mappings are made.</span></span>

| <span data-ttu-id="c58ce-112">內部部署 AD</span><span class="sxs-lookup"><span data-stu-id="c58ce-112">On-premises AD</span></span> | <span data-ttu-id="c58ce-113">Azure AD</span><span class="sxs-lookup"><span data-stu-id="c58ce-113">Azure AD</span></span> | <span data-ttu-id="c58ce-114">Azure AD 驗證的連絡資訊</span><span class="sxs-lookup"><span data-stu-id="c58ce-114">Azure AD Authentication contact info</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c58ce-115">telephoneNumber</span><span class="sxs-lookup"><span data-stu-id="c58ce-115">telephoneNumber</span></span> | <span data-ttu-id="c58ce-116">辦公室電話</span><span class="sxs-lookup"><span data-stu-id="c58ce-116">Office phone</span></span> | <span data-ttu-id="c58ce-117">備用手機</span><span class="sxs-lookup"><span data-stu-id="c58ce-117">Alternate phone</span></span> |
| <span data-ttu-id="c58ce-118">mobile</span><span class="sxs-lookup"><span data-stu-id="c58ce-118">mobile</span></span> | <span data-ttu-id="c58ce-119">行動電話</span><span class="sxs-lookup"><span data-stu-id="c58ce-119">Mobile phone</span></span> | <span data-ttu-id="c58ce-120">電話</span><span class="sxs-lookup"><span data-stu-id="c58ce-120">Phone</span></span> |


## <a name="security-questions-and-answers"></a><span data-ttu-id="c58ce-121">安全性問題和答案</span><span class="sxs-lookup"><span data-stu-id="c58ce-121">Security questions and answers</span></span>

<span data-ttu-id="c58ce-122">安全性問題和答案會安全地儲存在 Azure AD 租用戶中，使用者只能透過 [SSPR 註冊入口網站](https://aka.ms/ssprsetup)存取。</span><span class="sxs-lookup"><span data-stu-id="c58ce-122">Security questions and answers are stored securely in your Azure AD tenant and are only accessible to users via the [SSPR registration portal](https://aka.ms/ssprsetup).</span></span> <span data-ttu-id="c58ce-123">系統管理員無法看到或修改其他使用者的問題和答案內容。</span><span class="sxs-lookup"><span data-stu-id="c58ce-123">Administrators can't see or modify the contents of another users questions and answers.</span></span>

### <a name="what-happens-when-a-user-registers"></a><span data-ttu-id="c58ce-124">使用者註冊時的情況</span><span class="sxs-lookup"><span data-stu-id="c58ce-124">What happens when a user registers</span></span>

<span data-ttu-id="c58ce-125">當使用者註冊時，註冊頁面會設定下列欄位：</span><span class="sxs-lookup"><span data-stu-id="c58ce-125">When a user registers, the registration page sets the following fields:</span></span>

* <span data-ttu-id="c58ce-126">驗證電話</span><span class="sxs-lookup"><span data-stu-id="c58ce-126">Authentication Phone</span></span>
* <span data-ttu-id="c58ce-127">驗證電子郵件</span><span class="sxs-lookup"><span data-stu-id="c58ce-127">Authentication Email</span></span>
* <span data-ttu-id="c58ce-128">安全性問題和答案</span><span class="sxs-lookup"><span data-stu-id="c58ce-128">Security Questions and Answers</span></span>

<span data-ttu-id="c58ce-129">如果您已提供 [行動電話] 或 [備用電子郵件] 的值，使用者即使尚未註冊此服務，也可以立即使用這些值來重設其密碼。</span><span class="sxs-lookup"><span data-stu-id="c58ce-129">If you have provided a value for **Mobile Phone** or **Alternate Email**, users can immediately use those values to reset their passwords, even if they haven't registered for the service.</span></span> <span data-ttu-id="c58ce-130">此外，使用者會在第一次註冊時看到這些值，並可隨意加以修改。</span><span class="sxs-lookup"><span data-stu-id="c58ce-130">In addition, users see those values when registering for the first time, and modify them if they wish.</span></span> <span data-ttu-id="c58ce-131">成功註冊之後，這些值就會分別保存在 [驗證電話] 和 [驗證電子郵件] 欄位中。</span><span class="sxs-lookup"><span data-stu-id="c58ce-131">After they successfully register, these values will be persisted in the **Authentication Phone** and **Authentication Email** fields, respectively.</span></span>

## <a name="set-and-read-authentication-data-using-powershell"></a><span data-ttu-id="c58ce-132">使用 PowerShell 設定和讀取驗證資料</span><span class="sxs-lookup"><span data-stu-id="c58ce-132">Set and read authentication data using PowerShell</span></span>

<span data-ttu-id="c58ce-133">您可以使用 PowerShell 設定下列欄位</span><span class="sxs-lookup"><span data-stu-id="c58ce-133">The following fields can be set using PowerShell</span></span>

* <span data-ttu-id="c58ce-134">替代電子郵件</span><span class="sxs-lookup"><span data-stu-id="c58ce-134">Alternate Email</span></span>
* <span data-ttu-id="c58ce-135">行動電話</span><span class="sxs-lookup"><span data-stu-id="c58ce-135">Mobile Phone</span></span>
* <span data-ttu-id="c58ce-136">辦公室電話 - 只有在未與內部部署目錄同步處理時才能設定</span><span class="sxs-lookup"><span data-stu-id="c58ce-136">Office Phone - Can only be set if not synchronizing with an on-premises directory</span></span>

### <a name="using-powershell-v1"></a><span data-ttu-id="c58ce-137">使用 PowerShell V1</span><span class="sxs-lookup"><span data-stu-id="c58ce-137">Using PowerShell V1</span></span>

<span data-ttu-id="c58ce-138">首先，您必須[下載並安裝 Azure AD PowerShell 模組](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule)。</span><span class="sxs-lookup"><span data-stu-id="c58ce-138">To get started, you need to [download and install the Azure AD PowerShell module](https://msdn.microsoft.com/library/azure/jj151815.aspx#bkmk_installmodule).</span></span> <span data-ttu-id="c58ce-139">安裝之後，即可依照下列步驟設定每一個欄位。</span><span class="sxs-lookup"><span data-stu-id="c58ce-139">Once you have it installed, you can follow the steps that follow to configure each field.</span></span>

#### <a name="set-authentication-data-with-powershell-v1"></a><span data-ttu-id="c58ce-140">使用 PowerShell V1 設定驗證資料</span><span class="sxs-lookup"><span data-stu-id="c58ce-140">Set Authentication Data with PowerShell V1</span></span>

```
Connect-MsolService

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com")
Set-MsolUser -UserPrincipalName user@domain.com -MobilePhone "+1 1234567890"
Set-MsolUser -UserPrincipalName user@domain.com -PhoneNumber "+1 1234567890"

Set-MsolUser -UserPrincipalName user@domain.com -AlternateEmailAddresses @("email@domain.com") -MobilePhone "+1 1234567890" -PhoneNumber "+1 1234567890"
```

#### <a name="read-authentication-data-with-powershellpowershell-v1"></a><span data-ttu-id="c58ce-141">使用 PowerShellPowerShell V1 讀取驗證資料</span><span class="sxs-lookup"><span data-stu-id="c58ce-141">Read Authentication Data with PowerShellPowerShell V1</span></span>

```
Connect-MsolService

Get-MsolUser -UserPrincipalName user@domain.com | select AlternateEmailAddresses
Get-MsolUser -UserPrincipalName user@domain.com | select MobilePhone
Get-MsolUser -UserPrincipalName user@domain.com | select PhoneNumber

Get-MsolUser | select DisplayName,UserPrincipalName,AlternateEmailAddresses,MobilePhone,PhoneNumber | Format-Table
```

#### <a name="authentication-phone-and-authentication-email-can-only-be-read-using-powershell-v1-using-the-commands-that-follow"></a><span data-ttu-id="c58ce-142">必須在 Powershell V1 中使用下列命令，才能讀取 [驗證電話] 和 [驗證電子郵件]</span><span class="sxs-lookup"><span data-stu-id="c58ce-142">Authentication Phone and Authentication Email can only be read using Powershell V1 using the commands that follow</span></span>

```
Connect-MsolService
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select PhoneNumber
Get-MsolUser -UserPrincipalName user@domain.com | select -Expand StrongAuthenticationUserDetails | select Email
```

### <a name="using-powershell-v2"></a><span data-ttu-id="c58ce-143">使用 PowerShell V2</span><span class="sxs-lookup"><span data-stu-id="c58ce-143">Using PowerShell V2</span></span>

<span data-ttu-id="c58ce-144">首先，您必須[下載並安裝 Azure AD V2 PowerShell 模組](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md)。</span><span class="sxs-lookup"><span data-stu-id="c58ce-144">To get started, you need to [download and install the Azure AD V2 PowerShell module](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure%20AD%20Cmdlets/AzureAD/index.md).</span></span> <span data-ttu-id="c58ce-145">安裝之後，即可依照下列步驟設定每一個欄位。</span><span class="sxs-lookup"><span data-stu-id="c58ce-145">Once you have it installed, you can follow the steps that follow to configure each field.</span></span>

<span data-ttu-id="c58ce-146">若要從支援 Install-Module 的最新 PowerShell 版本快速安裝，請執行下列命令 (第一行只是檢查是否已安裝)︰</span><span class="sxs-lookup"><span data-stu-id="c58ce-146">To install quickly from recent versions of PowerShell that support Install-Module, run these commands (the first line simply checks to see if it's installed already):</span></span>

```
Get-Module AzureADPreview
Install-Module AzureADPreview
Connect-AzureAD
```

#### <a name="set-authentication-data-with-powershell-v2"></a><span data-ttu-id="c58ce-147">使用 PowerShell V2 設定驗證資料</span><span class="sxs-lookup"><span data-stu-id="c58ce-147">Set Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("email@domain.com")
Set-AzureADUser -ObjectId user@domain.com -Mobile "+1 2345678901"
Set-AzureADUser -ObjectId user@domain.com -TelephoneNumber "+1 1234567890"

Set-AzureADUser -ObjectId user@domain.com -OtherMails @("emails@domain.com") -Mobile "+1 1234567890" -TelephoneNumber "+1 1234567890"
```

### <a name="read-authentication-data-with-powershell-v2"></a><span data-ttu-id="c58ce-148">使用 PowerShell V2 讀取驗證資料</span><span class="sxs-lookup"><span data-stu-id="c58ce-148">Read Authentication Data with PowerShell V2</span></span>

```
Connect-AzureAD

Get-AzureADUser -ObjectID user@domain.com | select otherMails
Get-AzureADUser -ObjectID user@domain.com | select Mobile
Get-AzureADUser -ObjectID user@domain.com | select TelephoneNumber

Get-AzureADUser | select DisplayName,UserPrincipalName,otherMails,Mobile,TelephoneNumber | Format-Table
```

## <a name="next-steps"></a><span data-ttu-id="c58ce-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c58ce-149">Next steps</span></span>

<span data-ttu-id="c58ce-150">下列連結提供有關使用 Azure AD 重設密碼的其他資訊</span><span class="sxs-lookup"><span data-stu-id="c58ce-150">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="c58ce-151">[**快速入門**](active-directory-passwords-getting-started.md) - 開始執行 Azure AD 自助式密碼管理</span><span class="sxs-lookup"><span data-stu-id="c58ce-151">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="c58ce-152">[**授權**](active-directory-passwords-licensing.md) - 設定 Azure AD 授權</span><span class="sxs-lookup"><span data-stu-id="c58ce-152">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="c58ce-153">[**推出**](active-directory-passwords-best-practices.md) - 使用此處提供的指引來規劃 SSPR 並部署給使用者</span><span class="sxs-lookup"><span data-stu-id="c58ce-153">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="c58ce-154">[**自訂**](active-directory-passwords-customize.md) - 為您的公司自訂 SSPR 體驗的外觀及操作方式。</span><span class="sxs-lookup"><span data-stu-id="c58ce-154">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="c58ce-155">[**原則**](active-directory-passwords-policy.md) - 了解並設定 Azure AD 密碼原則</span><span class="sxs-lookup"><span data-stu-id="c58ce-155">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="c58ce-156">[**報告**](active-directory-passwords-reporting.md) - 探索您的使用者是否、何時、何地存取 SSPR 功能</span><span class="sxs-lookup"><span data-stu-id="c58ce-156">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="c58ce-157">[**技術性深入探討**](active-directory-passwords-how-it-works.md) - 深入探索以了解其運作方式</span><span class="sxs-lookup"><span data-stu-id="c58ce-157">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="c58ce-158">[**常見問題集**](active-directory-passwords-faq.md) - 如何？</span><span class="sxs-lookup"><span data-stu-id="c58ce-158">[**Frequently Asked Questions**](active-directory-passwords-faq.md) - How?</span></span> <span data-ttu-id="c58ce-159">原因為何？</span><span class="sxs-lookup"><span data-stu-id="c58ce-159">Why?</span></span> <span data-ttu-id="c58ce-160">何事？</span><span class="sxs-lookup"><span data-stu-id="c58ce-160">What?</span></span> <span data-ttu-id="c58ce-161">何地？</span><span class="sxs-lookup"><span data-stu-id="c58ce-161">Where?</span></span> <span data-ttu-id="c58ce-162">何人？</span><span class="sxs-lookup"><span data-stu-id="c58ce-162">Who?</span></span> <span data-ttu-id="c58ce-163">何時？</span><span class="sxs-lookup"><span data-stu-id="c58ce-163">When?</span></span> <span data-ttu-id="c58ce-164">- -您一直想要詢問之問題的答案</span><span class="sxs-lookup"><span data-stu-id="c58ce-164">- Answers to questions you always wanted to ask</span></span>
* <span data-ttu-id="c58ce-165">[**疑難排解**](active-directory-passwords-troubleshoot.md) - 了解如何解決我們看到的 SSPR 常見問題</span><span class="sxs-lookup"><span data-stu-id="c58ce-165">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>
