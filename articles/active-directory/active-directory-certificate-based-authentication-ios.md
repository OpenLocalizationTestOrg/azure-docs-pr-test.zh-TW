---
title: "aaaAzure Active Directory 憑證型驗證在 iOS 上的 |Microsoft 文件"
description: "深入了解支援的 hello 案例與方案中設定憑證型驗證，使用 iOS 裝置 hello 需求"
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
ms.openlocfilehash: 4486ff5239c2897b3bc187053f31d74807430301
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-certificate-based-authentication-on-ios"></a>iOS 上的 Azure Active Directory 憑證式驗證

憑證式驗證 (CBA) 可讓您連接至您 Exchange online 帳戶時，由 Azure Active Directory 驗證 Windows、 Android 或 iOS 裝置上的用戶端憑證的 toobe: 

* Office 行動應用程式，例如 Microsoft Outlook 與 Microsoft Word   
* Exchange ActiveSync (EAS) 用戶端 

設定此功能可減少 hello 需要 tooenter 使用者名稱和密碼組合成特定郵件和行動裝置上的 Microsoft Office 應用程式。 

本主題提供您與 hello 需求和支援的 hello 案例 CBA 裝置上設定 iOS(Android) Office 365 企業版、 企業、 教育、 美國政府、 中國，租用戶的使用者，以及德國計劃。

在 Office 365 US Government Defense 和 Federal 方案中，這項功能處於預覽版。




## <a name="office-mobile-applications-support"></a>Office 行動應用程式支援

| 應用程式 | 支援 |
| --- | --- |
| Azure 資訊保護應用程式 |![勾選][1] |
| Microsoft Teams |![勾選][1] |
| OneNote |![勾選][1] |
| OneDrive |![勾選][1] |
| Outlook |![勾選][1] |
| Power BI 行動應用程式 |![勾選][1] |
| 商務用 Skype |![勾選][1] |
| Word / Excel / PowerPoint |![勾選][1] |
| Yammer |![勾選][1] |


## <a name="requirements"></a>需求 

hello 裝置 OS 版本必須是 iOS 9 及更新版本 

必須設定同盟伺服器。  

iOS 上的 Office 應用程式都需要 Microsoft Authenticator。  

Azure Active Directory toorevoke 用戶端憑證，hello ADFS 權杖必須具有下列宣告 hello:  

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/<serialnumber>`  
  （hello 序號 hello 用戶端憑證） 
* `http://schemas.microsoft.com/2012/12/certificatecontext/field/<issuer>`  
  （hello 字串 hello hello 用戶端憑證的簽發者） 

在有提供 hello ADFS 權杖 （或任何其他的 SAML 權杖） 中，azure Active Directory 會將這些宣告 toohello 重新整理權杖。 當 hello 重新整理權杖需要 toobe 驗證時，這項資訊是使用的 toocheck hello 撤銷。 

最佳做法，您應該更新 hello ADFS 錯誤網頁 hello 下列：

* 在 iOS 上安裝 Microsoft Authenticator hello hello 需求
* 指示如何 tooget 使用者憑證。 

如需詳細資訊，請參閱[Customizing hello AD FS sign-in Pages](https://technet.microsoft.com/library/dn280950.aspx)。

有些 Office 應用程式 （啟用新式驗證） 傳送 '*提示 = [登入*' tooAzure AD 在要求中的。 根據預設，Azure AD 平移這個 hello 要求 tooADFS 中太 '*wauth = usernamepassworduri*' （詢問 ADFS toodo U P/auth） 和 '*wfresh = 0*' （詢問 ADFS tooignore SSO 狀態和執行全新的驗證）. 如果您想 tooenable 憑證式驗證這些應用程式，您會需要 toomodify hello 預設 Azure AD 的行為。 只要組 hello '*PromptLoginBehavior*' 同盟的網域設定中太 '*已停用*'。 您可以使用 hello [Get-msoldomainfederationsettings](/powershell/module/msonline/set-msoldomainfederationsettings?view=azureadps-1.0) cmdlet tooperform 這項工作：

`Set-MSOLDomainFederationSettings -domainname <domain> -PromptLoginBehavior Disabled`
  

## <a name="exchange-activesync-clients-support"></a>Exchange ActiveSync 用戶端支援
在 iOS 9 或更新版本、 支援 hello 原生 iOS 郵件用戶端。 所有其他的 Exchange ActiveSync 應用程式，toodetermine 支援此功能，請連絡您的應用程式開發人員。  


## <a name="next-steps"></a>後續步驟

如果您想 tooconfigure 憑證式驗證您的環境中，請參閱[開始在 Android 上的憑證型驗證使用](active-directory-certificate-based-authentication-get-started.md)如需相關指示。


<!--Image references-->
[1]: ./media/active-directory-certificate-based-authentication-ios/ic195031.png
