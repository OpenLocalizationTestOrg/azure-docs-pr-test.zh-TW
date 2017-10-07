---
title: "aaaAzure Active Directory 裝置註冊概觀 |Microsoft 文件"
description: "Azure Active Directory 裝置註冊是裝置型條件式存取案例的 hello 基礎。 註冊裝置時，Azure Active Directory 裝置註冊會佈建 hello 裝置時，才能使用的 tooauthenticate hello 裝置 hello 使用者登入身分識別。"
services: active-directory
keywords: "裝置註冊, 啟用裝置註冊, 裝置註冊和 MDM"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 1e92c1a2-01b8-4225-950b-373cd601b035
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: b9846e34fe873d271ebe71cbf8e70c6b4768885b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a>開始使用 Azure Active Directory 裝置註冊
Azure Active Directory 裝置註冊是裝置型條件式存取案例的 hello 基礎。 裝置註冊時，Azure Active Directory 裝置註冊提供 hello 裝置時，才能使用的 tooauthenticate hello 裝置 hello 使用者登入身分識別。 hello 驗證裝置 hello 裝置 hello 屬性接著可以使用的 tooenforce hello 雲端和內部部署中裝載的應用程式的條件式存取原則。

與 Microsoft Intune 等行動裝置 management(MDM) 解決方案結合時，Azure Active Directory 中的 hello 裝置屬性會更新 hello 裝置有關的其他資訊。 這可讓您 toocreate 條件式存取規則，以強制從裝置 toomeet 存取您的安全性與相容性的標準。 如需如何在 Microsoft Intune 中註冊裝置的詳細資訊，請參閱 [在 Intune 中註冊要管理的裝置](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)。

## <a name="scenarios-enabled-by-azure-active-directory-device-registration"></a>Azure Active Directory 裝置註冊所啟用的案例
Azure Active Directory 裝置註冊可支援 iOS、Android 和 Windows 裝置。 利用 Azure AD 裝置註冊的 hello 個別案例可能更特定的需求和支援的平台。 這些案例如下所示︰

* **條件式存取 tooapplications 會裝載於內部**： 您可以使用已註冊的裝置存取原則的應用程式設定 toouse AD FS 與 Windows Server 2012 R2。 如需有關設定內部部署之條件式存取的詳細資訊，請參閱[使用 Azure Active Directory 裝置註冊設定內部部署條件式存取](active-directory-device-registration-on-premises-setup.md)。
* **Office 365 應用程式使用 Microsoft Intune 的條件式存取**: IT 系統管理員可以佈建條件式存取裝置原則 toosecure 公司資源，而 hello 在相同時間允許相容裝置上的資訊工作者tooaccess hello 服務。 如需詳細資訊，請參閱 [Office 365 服務的條件式存取裝置原則](active-directory-conditional-access-device-policies.md)。

## <a name="setting-up-azure-active-directory-device-registration"></a>設定 Azure Active Directory 裝置註冊
您需要 tooenable Azure AD 裝置註冊 hello Azure 入口網站中的，讓行動裝置來探索 hello 服務尋找已知的 DNS 記錄。 您必須設定公司 DNS，讓 Windows 10、 Windows 8.1、 Windows 7、 Android 和 iOS 裝置可以探索並使用 hello 服務。
您可以檢視及啟用/停用已註冊的裝置使用 Azure Active Directory 中的 hello 管理員入口網站。

> [!NOTE]
> 如需如何設定自動裝置註冊 tooset 看到，最新的指示[toosetup 自動註冊的 Windows 網域如何聯結裝置與 Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)。
> 
> 

### <a name="enable-azure-active-directory-device-registration-service"></a>啟用 Azure Active Directory 裝置註冊服務
1. Toohello Microsoft Azure 入口網站管理員身分登入。
2. 在 hello 左窗格中，選取  **Active Directory**。
3. 在 hello**目錄**索引標籤上，選取您的目錄。
4. 選取 hello**設定** 索引標籤。
5. 捲動 toohello 區段呼叫**裝置**。
6. 針對 [使用者可以使用「加入工作場所」裝置] 選取 [全部]。
7. 選取 hello 最大數目的裝置，您想 tooauthorize 每位使用者。

> [!NOTE]
> Microsoft Intune 註冊或 Office 365 的行動裝置管理需要加入工作場所。 如果您已設定任一這些服務，選取所有與 hello NONE 按鈕已停用。
> 
> 

根據預設，不會對 hello 服務啟用雙因素驗證。 不過，建議在註冊裝置時使用雙因素驗證。

* 此服務要求雙因素驗證，您必須在 Azure Active Directory 中設定雙因素驗證提供者和設定您的使用者帳戶的多重要素驗證，請參閱[新增多因素驗證 tooAzure Active Directory](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)
* 如果您搭配使用 AD FS 與 Windows Server 2012 R2，則必須在 AD FS 中設定雙因素驗證模組，請參閱 [搭配使用 Multi-Factor Authentication 與 Active Directory Federation Services](../multi-factor-authentication/multi-factor-authentication-get-started-server.md)。

## <a name="configure-azure-active-directory-device-registration-discovery"></a>設定 Azure Active Directory 裝置註冊探索
Windows 7 和 Windows 8.1 裝置會結合 hello 使用者帳戶名稱與已知的裝置註冊的伺服器名稱以探索 hello 裝置註冊服務。

您必須建立 DNS CNAME 記錄指向與您的 Azure Active Directory 裝置註冊服務相關聯的 toohello A 記錄。 hello CNAME 記錄必須使用 hello 已知的首碼 enterpriseregistration 後面接著 hello hello 您組織的使用者帳戶所使用的 UPN 尾碼。 如果您的組織使用多個 UPN 尾碼，則必須在 DNS 中建立多個 CNAME 記錄。

例如，如果您在組織中名為使用兩個 UPN 尾碼@contoso.com和@region.contoso.com，您將建立下列 DNS 記錄的 hello。

| 項目 | 類型 | 位址 |
| --- | --- | --- |
| enterpriseregistration.contoso.com |CNAME |enterpriseregistration.windows.net |
| enterpriseregistration.region.contoso.com |CNAME |enterpriseregistration.windows.net |

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a>在 Azure Active Directory 中檢視和管理裝置物件
1. 從 hello Azure 系統管理員入口網站，您可以檢視、 封鎖和解除封鎖裝置。 已封鎖的裝置將不再有存取 tooapplications 設定的 tooallow 只有已註冊的裝置。
2. 系統管理員身分登入 toohello Microsoft Azure 入口網站。
3. 在 hello 左窗格中，選取  **Active Directory**。
4. 選取您的目錄。
5. 選取 hello**使用者** 索引標籤。然後選取使用者 tooview 他們的裝置
6. 選取 hello**裝置** 索引標籤。
7. 選取**登錄裝置**hello 從下拉功能表。
8. 您可以在此檢視，封鎖或解除封鎖 hello 使用者已註冊的裝置。

## <a name="additional-topics"></a>其他主題
您可以向 Azure AD 裝置註冊註冊 Windows 7 和 Windows 8.1 加入網域的裝置。 hello 下列主題提供在 Windows 7 和 Windows 8.1 裝置上的 hello 必要條件與 hello 步驟需要的 tooconfigure 裝置註冊的詳細資訊。

* [自動向 Azure Active Directory 註冊加入網域的 Windows 裝置](active-directory-conditional-access-automatic-device-registration.md)
* [自動向 Azure Active Directory 註冊加入網域的 Windows 10 裝置](active-directory-azureadjoin-devices-group-policy.md)

