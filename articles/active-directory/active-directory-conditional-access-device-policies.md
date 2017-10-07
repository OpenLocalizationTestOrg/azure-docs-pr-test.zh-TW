---
title: "Office 365 服務的 aaaAzure Active Directory 條件式存取裝置原則 |Microsoft 文件"
description: "深入了解如何 tooprovision 條件式存取裝置原則 toohelp 使公司資源更安全，同時維持使用者相容性及存取 tooservices。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8664c0bb-bba1-4012-b321-e9c8363080a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 38229a8d9766efbf0e6b17875b3018011c6b4ea3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="active-directory-conditional-access-device-policies-for-office-365-services"></a>適用於 Office 365 服務的 Active Directory 條件式存取裝置原則

條件式存取需要多個片段 toowork。 其中包含經過多重要素驗證的使用者、已驗證的裝置及符合規範的裝置等因素。 在本文中，我們主要著重在您的組織可以使用 toohelp 控制存取 tooOffice 365 服務的裝置型條件。 

公司使用者想要在公司或學校從其個人裝置的 Exchange 和 SharePoint Online 等 tooaccess Office 365 服務。 您想 hello 存取 toobe 安全。 您可以佈建條件式存取裝置原則 toohelp 讓公司資源更安全，同時授與存取 tooservices 都使用相容的裝置的使用者。 您可以設定條件式存取原則 tooOffice 365 hello Microsoft Intune 條件式存取入口網站中。

Azure Active Directory (Azure AD) 會強制執行條件式存取原則 toohelp 安全存取 tooOffice 365 服務。 您可以建立條件式存取原則，以封鎖使用不符合規範之裝置的使用者存取 Office 365 服務。 hello 使用者在授與存取 toohello 服務之前，必須符合 toohello 公司的裝置原則。 或者，您可以建立原則，要求使用者 tooenroll 其裝置 toogain 存取 tooan Office 365 服務。 原則可以套用的 tooall 在組織中的使用者，或僅限 tooa 幾個目標群組。 您可以加入多個目標群組 tooa 原則一段時間。

強制執行裝置原則的先決條件是，使用者必須使用 hello Azure AD 裝置註冊服務註冊其裝置。 您可以選擇 tooturn multi-factor authentication 以 hello Azure AD 裝置註冊服務註冊的裝置上。 建議 hello Azure Active Directory 裝置註冊服務的多重要素驗證。 多因素驗證開啟時，使用者註冊其裝置以 hello Azure AD 裝置註冊服務會經過第二個雙因素驗證。

## <a name="how-does-a-conditional-access-policy-work"></a>條件式存取原則如何運作？

當使用者從支援的裝置平台，要求存取 tooan Office 365 服務時，Azure AD 會驗證 hello 使用者和裝置 hello。 Azure AD 授與存取 toohello 服務才 hello 使用者符合 toohello hello 服務設定的原則。 未註冊的裝置上的使用者可以指示如何 tooenroll 並變成相容 tooaccess 公司 Office 365 服務。 IOS 和 Android 裝置上的使用者都需要的 tooenroll 他們的裝置使用 hello Intune 公司入口網站應用程式。 當使用者註冊裝置時，hello 裝置已向 Azure AD 並註冊裝置管理與相容性。 Office 365 服務的行動裝置管理，您必須使用 Microsoft Intune 使用 hello Azure AD 裝置註冊服務。 會強制執行裝置原則時，需要使用者 tooaccess Office 365 服務的裝置註冊。

當使用者成功註冊裝置、 hello 裝置就會變成受信任。 Azure AD 可讓已驗證的 hello 使用者單一登入存取 toocompany 應用程式。 Azure AD 會強制執行條件式存取原則 toogrant 存取 tooa 服務不僅 hello 初次 hello 使用者要求存取權，而且每個階段 hello 使用者更新要求，以進行存取。 hello 拒絕使用者存取 tooservices 時登入認證已變更、 hello 裝置遺失或遭竊，或在要求更新的 hello 時間不符合 hello hello 原則條件。

## <a name="deployment-considerations"></a>部署考量

您必須使用 hello Azure AD 裝置註冊服務 tooregister 裝置。

在內部部署使用者即將 toobe 通過驗證，Active Directory Federation Services (AD FS) （1.0 版和更新版本） 是必要。 工作地點的多因素驗證失敗時 hello 身分識別提供者不支援多重要素驗證。 例如，您無法搭配 AD FS 2.0 使用多重要素驗證。 請確定該 hello 內部部署 AD FS 搭配多因素驗證，且有效的多因素驗證方法已準備就緒之前您開啟 hello Azure AD 裝置註冊服務的多重要素驗證。 例如，Windows Server 2012 R2 上的 AD FS 具有多重要素驗證功能。 您也必須設定其他有效的驗證 （多重要素驗證） 方法 hello AD FS 伺服器上開啟 hello Azure AD 裝置註冊服務的多重要素驗證。 如需 AD FS 中支援的多重要素驗證方法詳細資訊，請參閱[設定 AD FS 的其他驗證方法](/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs)。

## <a name="next-steps"></a>後續步驟

*   如有解答 toocommon 問題，請參閱[Azure Active Directory 條件式存取常見問題集](active-directory-conditional-faqs.md)。
