---
title: "aaaAzure Active Directory 憑證型驗證在 Android 上的 |Microsoft 文件"
description: "深入了解支援的 hello 案例與方案中的憑證為基礎的驗證設定 Android 裝置中的 hello 需求"
services: active-directory
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/28/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 148275fa3da610530c278fcd57e02e907f735d9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-android"></a><span data-ttu-id="ec277-103">Android 上的 Azure Active Directory 憑證式驗證</span><span class="sxs-lookup"><span data-stu-id="ec277-103">Azure Active Directory certificate-based authentication on Android</span></span>


<span data-ttu-id="ec277-104">憑證式驗證 (CBA) 可讓您連接至您 Exchange online 帳戶時，由 Azure Active Directory 驗證 Windows、 Android 或 iOS 裝置上的用戶端憑證的 toobe:</span><span class="sxs-lookup"><span data-stu-id="ec277-104">Certificate-based authentication (CBA) enables you toobe authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

* <span data-ttu-id="ec277-105">Office 行動應用程式，例如 Microsoft Outlook 與 Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="ec277-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   
* <span data-ttu-id="ec277-106">Exchange ActiveSync (EAS) 用戶端</span><span class="sxs-lookup"><span data-stu-id="ec277-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="ec277-107">設定此功能可減少 hello 需要 tooenter 使用者名稱和密碼組合成特定郵件和行動裝置上的 Microsoft Office 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec277-107">Configuring this feature eliminates hello need tooenter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="ec277-108">本主題提供您與 hello 需求和支援的 hello 案例 CBA 裝置上設定 iOS(Android) Office 365 企業版、 企業、 教育、 美國政府、 中國，租用戶的使用者，以及德國計劃。</span><span class="sxs-lookup"><span data-stu-id="ec277-108">This topic provides you with hello requirements and hello supported scenarios for configuring CBA on an iOS(Android) device for users of tenants in Office 365 Enterprise, Business, Education, US Government, China, and Germany plans.</span></span>



<span data-ttu-id="ec277-109">在 Office 365 US Government Defense 和 Federal 方案中，這項功能處於預覽版。</span><span class="sxs-lookup"><span data-stu-id="ec277-109">This feature is available in preview in Office 365 US Government Defense and Federal plans.</span></span>


## <a name="office-mobile-applications-support"></a><span data-ttu-id="ec277-110">Office 行動應用程式支援</span><span class="sxs-lookup"><span data-stu-id="ec277-110">Office mobile applications support</span></span>
| <span data-ttu-id="ec277-111">應用程式</span><span class="sxs-lookup"><span data-stu-id="ec277-111">Apps</span></span> | <span data-ttu-id="ec277-112">支援</span><span class="sxs-lookup"><span data-stu-id="ec277-112">Support</span></span> |
| --- | --- |
| <span data-ttu-id="ec277-113">Azure 資訊保護應用程式</span><span class="sxs-lookup"><span data-stu-id="ec277-113">Azure Information Protection app</span></span> |![勾選][1] |
| <span data-ttu-id="ec277-115">Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="ec277-115">Microsoft Teams</span></span> |![勾選][1] |
| <span data-ttu-id="ec277-117">OneNote</span><span class="sxs-lookup"><span data-stu-id="ec277-117">OneNote</span></span> |![勾選][1] |
| <span data-ttu-id="ec277-119">OneDrive</span><span class="sxs-lookup"><span data-stu-id="ec277-119">OneDrive</span></span> |![勾選][1] |
| <span data-ttu-id="ec277-121">Outlook</span><span class="sxs-lookup"><span data-stu-id="ec277-121">Outlook</span></span> |![勾選][1] |
| <span data-ttu-id="ec277-123">Power BI 行動應用程式</span><span class="sxs-lookup"><span data-stu-id="ec277-123">Power BI mobile apps</span></span> |![勾選][1] |
| <span data-ttu-id="ec277-125">商務用 Skype</span><span class="sxs-lookup"><span data-stu-id="ec277-125">Skype for Business</span></span> |![勾選][1] |
| <span data-ttu-id="ec277-127">Word / Excel / PowerPoint</span><span class="sxs-lookup"><span data-stu-id="ec277-127">Word / Excel / PowerPoint</span></span> |![勾選][1] |
| <span data-ttu-id="ec277-129">Yammer</span><span class="sxs-lookup"><span data-stu-id="ec277-129">Yammer</span></span> |![勾選][1] |


### <a name="implementation-requirements"></a><span data-ttu-id="ec277-131">實作需求</span><span class="sxs-lookup"><span data-stu-id="ec277-131">Implementation requirements</span></span>

<span data-ttu-id="ec277-132">hello 裝置 OS 版本必須是 Android 5.0 （棒棒糖符號） 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="ec277-132">hello device OS version must be Android 5.0 (Lollipop) and above.</span></span> 

<span data-ttu-id="ec277-133">必須設定同盟伺服器。</span><span class="sxs-lookup"><span data-stu-id="ec277-133">A federation server must be configured.</span></span>  

<span data-ttu-id="ec277-134">Azure Active Directory toorevoke 用戶端憑證，hello ADFS 權杖必須具有下列宣告 hello:</span><span class="sxs-lookup"><span data-stu-id="ec277-134">For Azure Active Directory toorevoke a client certificate, hello ADFS token must have hello following claims:</span></span>  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  <span data-ttu-id="ec277-135">（hello 序號 hello 用戶端憑證）</span><span class="sxs-lookup"><span data-stu-id="ec277-135">(hello serial number of hello client certificate)</span></span> 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  <span data-ttu-id="ec277-136">（hello 字串 hello hello 用戶端憑證的簽發者）</span><span class="sxs-lookup"><span data-stu-id="ec277-136">(hello string for hello issuer of hello client certificate)</span></span> 

<span data-ttu-id="ec277-137">在有提供 hello ADFS 權杖 （或任何其他的 SAML 權杖） 中，azure Active Directory 會將這些宣告 toohello 重新整理權杖。</span><span class="sxs-lookup"><span data-stu-id="ec277-137">Azure Active Directory adds these claims toohello refresh token if they are available in hello ADFS token (or any other SAML token).</span></span> <span data-ttu-id="ec277-138">當 hello 重新整理權杖需要 toobe 驗證時，這項資訊是使用的 toocheck hello 撤銷。</span><span class="sxs-lookup"><span data-stu-id="ec277-138">When hello refresh token needs toobe validated, this information is used toocheck hello revocation.</span></span> 

<span data-ttu-id="ec277-139">最佳做法，您應該更新 hello ADFS 錯誤網頁指示 tooget 使用者憑證。</span><span class="sxs-lookup"><span data-stu-id="ec277-139">As a best practice, you should update hello ADFS error pages with instructions on how tooget a user certificate.</span></span>  
<span data-ttu-id="ec277-140">如需詳細資訊，請參閱[Customizing hello AD FS sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ec277-140">For more details, see [Customizing hello AD FS Sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx).</span></span>  

<span data-ttu-id="ec277-141">有些 Office 應用程式 （啟用新式驗證） 傳送 '*提示 = 登入*' tooAzure AD 在要求中的。</span><span class="sxs-lookup"><span data-stu-id="ec277-141">Some Office apps (with modern authentication enabled) send ‘*prompt=login*’ tooAzure AD in their request.</span></span> <span data-ttu-id="ec277-142">根據預設，Azure AD 平移這個 hello 要求 tooADFS 中太 '*wauth = usernamepassworduri*' （詢問 ADFS toodo U P/auth） 和 '*wfresh = 0*' （詢問 ADFS tooignore SSO 狀態和執行全新的驗證）.</span><span class="sxs-lookup"><span data-stu-id="ec277-142">By default, Azure AD translates this in hello request tooADFS too‘*wauth=usernamepassworduri*’ (asks ADFS toodo U/P auth) and ‘*wfresh=0*’ (asks ADFS tooignore SSO state and do a fresh authentication).</span></span> <span data-ttu-id="ec277-143">如果您想 tooenable 憑證式驗證這些應用程式，您會需要 toomodify hello 預設 Azure AD 的行為。</span><span class="sxs-lookup"><span data-stu-id="ec277-143">If you want tooenable certificate-based authentication for these apps, you need toomodify hello default Azure AD behavior.</span></span> <span data-ttu-id="ec277-144">只要組 hello '*PromptLoginBehavior*' 同盟的網域設定中太 '*已停用*'。</span><span class="sxs-lookup"><span data-stu-id="ec277-144">Just set hello ‘*PromptLoginBehavior*’ in your federated domain settings too‘*Disabled*‘.</span></span> <span data-ttu-id="ec277-145">您可以使用 hello [Get-msoldomainfederationsettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet tooperform 這項工作：</span><span class="sxs-lookup"><span data-stu-id="ec277-145">You can use hello [MSOLDomainFederationSettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet tooperform this task:</span></span>

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`



## <a name="exchange-activesync-clients-support"></a><span data-ttu-id="ec277-146">Exchange ActiveSync 用戶端支援</span><span class="sxs-lookup"><span data-stu-id="ec277-146">Exchange ActiveSync clients support</span></span>
<span data-ttu-id="ec277-147">支援 Android 5.0 (Lollipop) 或更新版本上的某些 Exchange ActiveSync 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec277-147">Certain Exchange ActiveSync applications on Android 5.0 (Lollipop) or later are supported.</span></span> <span data-ttu-id="ec277-148">toodetermine 如果您的電子郵件應用程式不支援這項功能，請連絡您的應用程式開發人員。</span><span class="sxs-lookup"><span data-stu-id="ec277-148">toodetermine if your email application does support this feature, please contact your application developer.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="ec277-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ec277-149">Next steps</span></span>

<span data-ttu-id="ec277-150">如果您想 tooconfigure 憑證式驗證您的環境中，請參閱[開始在 Android 上的憑證型驗證使用](active-directory-certificate-based-authentication-get-started.md)如需相關指示。</span><span class="sxs-lookup"><span data-stu-id="ec277-150">If you want tooconfigure certificate-based authentication in your environment, see [Get started with certificate-based authentication on Android](active-directory-certificate-based-authentication-get-started.md) for instructions.</span></span>

<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-android/ic195031.png
