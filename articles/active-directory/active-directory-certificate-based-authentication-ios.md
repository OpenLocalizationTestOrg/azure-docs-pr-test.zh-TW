---
title: "iOS 上的 Azure Active Directory 憑證式驗證 | Microsoft Docs"
description: "了解在有 iOS 裝置的解決方案中，設定憑證式驗證的支援案例和需求"
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: 26a6fc54-0153-44fb-b970-9b432c99e9f9
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: c781f3f054fad5c5092fed5058c932fd4e97cf35
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a><span data-ttu-id="2f3fc-103">iOS 上的 Azure Active Directory 憑證式驗證</span><span class="sxs-lookup"><span data-stu-id="2f3fc-103">Azure Active Directory certificate-based authentication on iOS</span></span>

<span data-ttu-id="2f3fc-104">在將您的 Exchange Online 帳戶連線到下列各項時，憑證式驗證 (CBA) 可讓您由 Azure Active Directory 透過用戶端憑證在 Windows、Android 或 iOS 裝置上驗證您的身分︰</span><span class="sxs-lookup"><span data-stu-id="2f3fc-104">Certificate-based authentication (CBA) enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="2f3fc-105">Office 行動應用程式，例如 Microsoft Outlook 與 Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="2f3fc-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="2f3fc-106">Exchange ActiveSync (EAS) 用戶端</span><span class="sxs-lookup"><span data-stu-id="2f3fc-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="2f3fc-107">設定這項功能之後，就不需要在行動裝置上的特定郵件和 Microsoft Office 應用程式中，輸入使用者名稱和密碼的組合。</span><span class="sxs-lookup"><span data-stu-id="2f3fc-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="2f3fc-108">本主題針對 Office 365 企業版、商務版、教育版、美國政府機關、中國和德國方案的租用戶使用者，提供在 iOS (Android) 裝置上設定 CBA 的需求和支援案例。</span><span class="sxs-lookup"><span data-stu-id="2f3fc-108">This topic provides you with the requirements and the supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>

<span data-ttu-id="2f3fc-109">在 Office 365 US Government Defense 和 Federal 方案中，這項功能處於預覽版。</span><span class="sxs-lookup"><span data-stu-id="2f3fc-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>




## <a name="office-mobile-applications-support"></a><span data-ttu-id="2f3fc-110">Office 行動應用程式支援</span><span class="sxs-lookup"><span data-stu-id="2f3fc-110">Office mobile applications support</span></span>

| <span data-ttu-id="2f3fc-111">應用程式</span><span class="sxs-lookup"><span data-stu-id="2f3fc-111">Apps</span></span> | <span data-ttu-id="2f3fc-112">支援</span><span class="sxs-lookup"><span data-stu-id="2f3fc-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="2f3fc-113">Azure 資訊保護應用程式</span><span class="sxs-lookup"><span data-stu-id="2f3fc-113">Azure Information Protection app</span></span> |![勾選][1] |
| <span data-ttu-id="2f3fc-115">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="2f3fc-115">Microsoft Teams</span></span> |![勾選][1] |
| <span data-ttu-id="2f3fc-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="2f3fc-117">OneNote</span></span> |![勾選][1] |
| <span data-ttu-id="2f3fc-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="2f3fc-119">OneDrive</span></span> |![勾選][1] |
| <span data-ttu-id="2f3fc-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="2f3fc-121">Outlook</span></span> |![勾選][1] |
| <span data-ttu-id="2f3fc-123">Power BI 行動應用程式</span><span class="sxs-lookup"><span data-stu-id="2f3fc-123">Power BI mobile apps</span></span> |![勾選][1] |
| <span data-ttu-id="2f3fc-125">商務用 Skype</span><span class="sxs-lookup"><span data-stu-id="2f3fc-125">Skype for Business</span></span> |![勾選][1] |
| <span data-ttu-id="2f3fc-127">Word / Excel / PowerPoint</span><span class="sxs-lookup"><span data-stu-id="2f3fc-127">Word / Excel / PowerPoint</span></span> |![勾選][1] |
| <span data-ttu-id="2f3fc-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="2f3fc-129">Yammer</span></span> |![勾選][1] |


## <a name="requirements"></a><span data-ttu-id="2f3fc-131">需求</span><span class="sxs-lookup"><span data-stu-id="2f3fc-131">Requirements</span></span> 

<span data-ttu-id="2f3fc-132">裝置作業系統版本必須是 iOS 9 和更新版本</span><span class="sxs-lookup"><span data-stu-id="2f3fc-132">The device OS version must be iOS 9 and above</span></span> 

<span data-ttu-id="2f3fc-133">必須設定同盟伺服器。</span><span class="sxs-lookup"><span data-stu-id="2f3fc-133">A federation server must be configured.</span></span>  

<span data-ttu-id="2f3fc-134">iOS 上的 Office 應用程式都需要 Microsoft Authenticator。</span><span class="sxs-lookup"><span data-stu-id="2f3fc-134">Microsoft Authenticator is required for Office applications on iOS.</span></span>  

<span data-ttu-id="2f3fc-135">ADFS 權杖必須要有下列宣告，Azure Active Directory 才能撤銷用戶端憑證︰</span><span class="sxs-lookup"><span data-stu-id="2f3fc-135">For Azure Active Directory to revoke a client certificate, the ADFS token must have the following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="2f3fc-136">(用戶端憑證序號)</span><span class="sxs-lookup"><span data-stu-id="2f3fc-136">(The serial number of the client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="2f3fc-137">(用戶端憑證簽發者字串)</span><span class="sxs-lookup"><span data-stu-id="2f3fc-137">(The string for the issuer of the client certificate)</span></span> 

<span data-ttu-id="2f3fc-138">如果 ADFS 權杖 (或任何其他 SAML 權杖) 中有上述宣告，Azure Active Directory 就會將這些宣告新增至重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="2f3fc-138">Azure Active Directory adds these claims to the refresh token if they are available in the ADFS token (or any other SAML token).</span></span> <span data-ttu-id="2f3fc-139">當需要驗證重新整理權杖時，這項資訊會用於檢查撤銷。</span><span class="sxs-lookup"><span data-stu-id="2f3fc-139">When the refresh token needs to be validated, this information is used to check the revocation.</span></span> 

<span data-ttu-id="2f3fc-140">最佳做法是應該以下列各項來更新 ADFS 錯誤頁面︰</span><span class="sxs-lookup"><span data-stu-id="2f3fc-140">As a best practice, you should update the ADFS error pages with the following:</span></span>

* <span data-ttu-id="2f3fc-141">在 iOS 上安裝 Microsoft Authenticator 的需求</span><span class="sxs-lookup"><span data-stu-id="2f3fc-141">The requirement for installing the Microsoft Authenticator on iOS</span></span>
* <span data-ttu-id="2f3fc-142">如何取得使用者憑證的指示。</span><span class="sxs-lookup"><span data-stu-id="2f3fc-142">Instructions on how to get a user certificate.</span></span> 

<span data-ttu-id="2f3fc-143">如需詳細資訊，請參閱 [自訂 AD FS 登入頁面](https://technet.microsoft.com/library/dn280950.aspx)。</span><span class="sxs-lookup"><span data-stu-id="2f3fc-143">For more details, see [Customizing the AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>

<span data-ttu-id="2f3fc-144">某些 Office 應用程式 (已啟用新式驗證) 會在其要求中將 ‘*prompt=login*’ 傳送至 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="2f3fc-144">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ to Azure AD in their request.</span></span> <span data-ttu-id="2f3fc-145">根據預設，Azure AD 會將給 ADFS 的要求中的這項轉譯成 ‘*wauth=usernamepassworduri*’ (請求 ADFS 進行 U/P 驗證) 和 ‘*wfresh=0*’ (請求 ADFS 忽略 SSO 狀態並進行全新驗證)。</span><span class="sxs-lookup"><span data-stu-id="2f3fc-145">By default, Azure AD translates this in the request to ADFS to ‘*wauth=usernamepassworduri*’ (asks ADFS to do U/P auth) and ‘*wfresh=0*’ (asks ADFS to ignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="2f3fc-146">如果您想要啟用這些應用程式的憑證型驗證，您必須修改預設的 Azure AD 行為。</span><span class="sxs-lookup"><span data-stu-id="2f3fc-146">If you want to enable certificate-based authentication for these apps, you need to modify the default Azure AD behavior.</span></span> <span data-ttu-id="2f3fc-147">只要將您的同盟網域設定中的 'PromptLoginBehavior' 設定為 ‘Disabled‘。</span><span class="sxs-lookup"><span data-stu-id="2f3fc-147">Just set the ‘*PromptLoginBehavior*’ in your federated domain settings to ‘*Disabled*‘.</span></span> <span data-ttu-id="2f3fc-148">您可以使用 [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) Cmdlet 來執行這項工作︰</span><span class="sxs-lookup"><span data-stu-id="2f3fc-148">You can use the [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet to perform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`
  

## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="2f3fc-149">Exchange ActiveSync 用戶端支援</span><span class="sxs-lookup"><span data-stu-id="2f3fc-149">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="2f3fc-150">iOS 9 或更新版本支援原生 iOS 郵件用戶端。</span><span class="sxs-lookup"><span data-stu-id="2f3fc-150">On iOS 9 or later, the native iOS mail client is supported.</span></span> <span data-ttu-id="2f3fc-151">針對其他所有 Exchange ActiveSync 應用程式，若要判斷這項功能是否受支援，請連絡您的應用程式開發人員。</span><span class="sxs-lookup"><span data-stu-id="2f3fc-151">For all other Exchange ActiveSync applications, to determine if this feature is supported, contact your application developer.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="2f3fc-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2f3fc-152">Next steps</span></span>

<span data-ttu-id="2f3fc-153">如果您想要在環境中設定憑證式驗證，相關指示請參閱[在 Android 上開始使用憑證式驗證](active-directory-certificate-based-authentication-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="2f3fc-153">If you want to configure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>


<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-ios/ic195031.png
