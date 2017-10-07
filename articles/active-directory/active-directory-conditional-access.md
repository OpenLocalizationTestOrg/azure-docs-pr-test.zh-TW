---
title: "aaaConditional hello Azure 傳統入口網站中的存取權 |Microsoft 文件"
description: "使用條件式存取控制 hello Azure 傳統入口網站 toocheck 中針對特定條件的存取 tooapplications 驗證時。"
services: active-directory
keywords: "條件式存取 tooapps，Azure AD 中，使用條件式存取保護存取 toocompany 資源，條件式存取原則"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: da3f0a44-1399-4e0b-aefb-03a826ae4ead
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/07/2017
ms.author: markvi
ms.reviewer: calebb
ms.custom: oldportal
ms.openlocfilehash: 049bd3f6ec9e35479319ee7608b007b9a1e16647
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="conditional-access-in-hello-azure-classic-portal"></a>在 hello Azure 傳統入口網站中的條件式存取

本主題是關於在 hello Azure 傳統入口網站中的條件式存取。 Hello 最近 hello Azure Active Directory 中的條件式存取相關的資訊，請參閱[Azure Active Directory 中的條件式存取](active-directory-conditional-access-azure-portal.md)。


條件式存取的 Azure Active Directory (Azure AD) 中的 hello 控制功能提供簡單的方式 toohelp hello 雲端和內部部署保護的資源。 條件式存取原則，例如多重要素驗證可以協助防範 hello 風險遭竊和 phished 認證。 其他條件式存取原則可協助保護貴組織的資料安全。 例如，此外 toorequiring 認證，您可能有原則只有像 Microsoft Intune 可以存取您組織的敏感服務在行動裝置管理系統中註冊裝置。

## <a name="prerequisites"></a>必要條件
Azure AD 條件式存取是 [Azure Active Directory Premium](http://www.microsoft.com/identity) 的一項功能。 每個存取已套用條件式存取原則之應用程式的使用者，都必須有 Azure AD Premium 授權。 您可以在[未經授權的使用者報告](https://aka.ms/utc5ix)中深入了解授權需求。

## <a name="how-is-conditional-access-control-enforced"></a>如何強制執行條件式存取控制？
條件式存取控制，Azure AD 會檢查 hello 特定條件的使用者 tooaccess 設定的應用程式。 符合存取需求後，hello 使用者會驗證，且可以存取 hello 應用程式。  

![條件式存取概觀](./media/active-directory-conditional-access/conditionalaccess-overview.png)

## <a name="conditions"></a>條件
以下是您可以納入條件式存取原則的條件︰

* **群組成員資格**。 根據在群組中的成員資格，控制使用者的存取權。
* **位置**。 使用 hello 位置 hello 使用者 tootrigger 多因素驗證，並在使用者不是受信任的網路上時使用區塊控制項。
* **裝置平台**。 Hello 裝置平台，例如 iOS、 Android、 Windows Mobile 或 Windows，做為套用原則的條件。
* **啟用裝置**。 在裝置原則評估期間會驗證裝置狀態 (啟用或停用)。 如果您停用遺失或遭竊的裝置 hello 目錄中，它可以不再符合原則需求。
* **登入和使用者風險**。 您可以將使用 [Azure AD Identity Protection](active-directory-identityprotection.md) 使用於條件式存取風險原則。 條件式存取風險原則有助於根據風險事件和異常登入活動，為您的組織提供進階保護。

## <a name="controls"></a>控制
這些是您可以使用 tooenforce 條件式存取原則的控制項：

* **Multi-Factor Authentication**。 您可以透過 Multi-Factor Authentication 來要求增強式驗證。 您可以使用多重要素驗證搭配 Azure Multi-Factor Authentication，或使用結合 Active Directory Federation Services (AD FS) 的內部部署多重要素驗證提供者。 使用多因素驗證，可協助防止未經授權的使用者，可能會獲得了存取 toohello 認證是有效的使用者所存取資源。
* **封鎖**。 您可以套用條件，例如使用者位置 tooblock 使用者存取。 例如，當使用者未在受信任網路時，您可以封鎖其存取。
* **相容的裝置**。 您可以在 hello 裝置層級設定條件式存取原則。 您可以設定一個原則：只有已加入網域的電腦或已在行動裝置管理應用程式中註冊的行動裝置可以存取您組織的資源。 比方說，您可以使用 Intune toocheck 裝置相容性，並再回報 tooAzure 強制 AD hello 使用者嘗試 tooaccess 應用程式時。 如需如何 toouse Intune tooprotect 應用程式和資料，請參閱詳細指引[使用 Microsoft Intune 保護應用程式和資料](https://docs.microsoft.com/intune/deploy-use/protect-apps-and-data-with-microsoft-intune)。 您也可以使用 Intune tooenforce 資料保護遺失或遭竊的裝置。 如需詳細資訊，請參閱 [使用 Microsoft Intune 搭配完整或選擇性抹除協助保護您的資料](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune)。

## <a name="applications"></a>應用程式
您可以強制執行條件式存取原則 hello 應用程式層級。 Hello 雲端或內部部署中設定應用程式和服務的存取層級。 hello 原則會套用直接 toohello 網站或服務。 hello 原則會強制存取 toohello 瀏覽器，然後 tooapplications 存取 hello 服務。

## <a name="device-based-conditional-access"></a>裝置型條件式存取
您可以限制存取 tooapplications 從裝置會向 Azure AD，以及符合特定條件。 裝置型條件式存取保護組織的資源的使用者嘗試從 tooaccess hello 資源：

* 不明或未受管理的裝置。
* 設定您的組織不符合 hello 安全性原則的裝置。

您可以根據下列需求設定原則︰

* **已加入網域的裝置**。 設定原則 toorestrict 存取 toodevices 聯結的 tooan 在內部部署 Active Directory 網域，而且，也會向 Azure AD 註冊。 此原則適用於 tooWindows 桌上型電腦、 膝上型電腦和企業平板電腦。
  如需有關如何 tooset 設定自動註冊的已加入網域的裝置與 Azure AD，請參閱[設定自動註冊的 Windows 網域的裝置與 Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)。
* **相容的裝置**。 設定原則 toorestrict 存取 toodevices 標示**相容**hello 管理系統目錄中。 此原則可確保只有符合安全性原則 (例如在裝置上強制執行檔案加密) 的裝置會獲允許存取。 您可以使用從下列裝置 hello 這個原則 toorestrict 存取：
  
  * **已加入網域的 Windows 裝置**。 管理由 System Center Configuration Manager （在 hello 最新分支） 部署在混合式組態。
  * **Windows 10 行動裝置版的工作或個人裝置**。 由 Intune 或由支援的協力廠商行動裝置管理系統所管理。
  * **iOS 和 Android 裝置**。 由 Intune 管理。

存取受裝置為基礎的應用程式的使用者，憑證授權原則必須從符合此原則需求的裝置存取 hello 應用程式。 如果在不符合原則需求的裝置上嘗試存取，則會遭到拒絕。

如需有關如何查看 tooconfigure 以裝置為基礎，在 Azure AD 中的憑證授權原則資訊[設定 Azure Active Directory 連線應用程式的裝置型條件式存取原則](active-directory-conditional-access-policy-connected-applications.md)。

## <a name="resources"></a>資源
請參閱下列資源類別目錄與文件 toolearn 更多關於設定條件式存取貴組織的 hello。

### <a name="multi-factor-authentication-and-location-policies"></a>Multi-Factor Authentication 和位置原則
* [開始使用條件式存取 tooAzure AD 連線基礎的應用程式群組、 位置及多因素驗證原則](active-directory-conditional-access-azuread-connected-apps.md)
* [支援的應用程式和瀏覽器](active-directory-conditional-access-supported-apps.md)

### <a name="device-based-conditional-access"></a>裝置型條件式存取
* [設定存取裝置型條件式存取原則控制 tooAzure 已連線到 Active Directory 的應用程式](active-directory-conditional-access-policy-connected-applications.md)
* [設定讓已加入網域的 Windows 裝置自動向 Azure Active Directory 註冊](active-directory-conditional-access-automatic-device-registration-setup.md)
* [針對 Azure Active Directory 存取問題進行疑難排解](active-directory-conditional-access-device-remediation.md)
* [使用 Microsoft Intune 協助保護遺失或遭竊裝置上的資料](https://docs.microsoft.com/intune/deploy-use/use-remote-wipe-to-help-protect-data-using-microsoft-intune)

### <a name="protect-resources-based-on-sign-in-risk"></a>根據登入風險保護資源
* [Azure AD Identity Protection](active-directory-identityprotection.md)

### <a name="next-steps"></a>後續步驟
* [條件式存取常見問題集](active-directory-conditional-faqs.md)
* [技術參考](active-directory-conditional-access-technical-reference.md)

