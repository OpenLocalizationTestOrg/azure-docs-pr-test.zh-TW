---
title: "aaaHow tooconfigure 自動註冊的 Windows 網域的裝置與 Azure Active Directory |Microsoft 文件"
description: "設定您已加入網域的 Windows 裝置 tooregister 自動且無訊息地與 Azure Active Directory。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 1d736eba734418231f12e23a8fc1a93405f129c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a>開始使用 Azure Active Directory 裝置註冊

Azure Active Directory 裝置註冊是裝置型條件式存取案例的 hello 基礎。 裝置註冊時，Azure Active Directory 裝置註冊提供 hello 裝置時，才能使用的 tooauthenticate hello 裝置 hello 使用者登入身分識別。 hello 驗證裝置 hello 裝置 hello 屬性接著可以使用的 tooenforce hello 雲端和內部部署中裝載的應用程式的條件式存取原則。

與 Microsoft Intune 等行動裝置 management(MDM) 解決方案結合時，Azure Active Directory 中的 hello 裝置屬性會更新 hello 裝置有關的其他資訊。 這可讓您 toocreate 條件式存取規則，以強制從裝置 toomeet 存取您的安全性與相容性的標準。 如需如何在 Microsoft Intune 中註冊裝置的詳細資訊，請參閱＜在 Intune 中註冊要管理的裝置＞。
由 Azure Active Directory 裝置註冊 Azure Active Directory 裝置註冊啟用的案例包括對 iOS、Android 與 Windows 裝置的支援。 利用 Azure AD 裝置註冊的 hello 個別案例可能更特定的需求和支援的平台。 

這些案例如下所示︰

- **Office 365 應用程式使用 Microsoft Intune 的條件式存取：** IT 系統管理員可以佈建條件式存取裝置原則 toosecure 公司資源，而 hello 在相同時間允許相容裝置上的資訊工作者tooaccess hello 服務。 如需詳細資訊，請參閱 Office 365 服務的條件式存取裝置原則。

- **條件式存取 tooapplications 屬於裝載在內部部署：**的應用程式設定 toouse AD FS 與 Windows Server 2012 R2，您可以存取原則搭配使用已註冊的裝置。 如需有關設定內部部署之條件式存取的詳細資訊，請參閱[使用 Azure Active Directory 裝置註冊設定內部部署條件式存取](active-directory-device-registration-on-premises-setup.md)。

## <a name="setting-up-azure-active-directory-device-registration"></a>設定 Azure Active Directory 裝置註冊

toosetup 裝置註冊，您有多個選項：

- 裝置可以註冊時聯結的 tooAzure AD 網域。 如需本主題的詳細資訊，您可以進一步了解 Azure AD Join 和 hello 設定所需的使用者 toojoin Azure AD 網域。

- 當使用者新增工作或學校帳戶 tooWindows，個人裝置或行動裝置連線需要登錄 tooa 工作資源時，就可以註冊裝置。 tooensure，您必須啟用 Azure AD 裝置註冊 hello Azure 入口網站中的。 

- 裝置可以針對已加入網域的傳統電腦使用自動裝置註冊。 tooensure，繼續進行 自動註冊裝置之前，必須第一個安裝 Azure AD Connect。

最新說明，請參閱[如何 tooconfigure 自動註冊的 Windows 網域的裝置與 Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)。  
您也可以檢閱和啟用或停用已註冊的裝置使用 Azure Active Directory 中的 hello 管理員入口網站。

## <a name="enable-hello-azure-active-directory-device-registration-service"></a>啟用 hello Azure Active Directory 裝置註冊服務

**tooenable hello Azure Active Directory 裝置註冊服務：**

1.  Toohello Microsoft Azure 入口網站管理員身分登入。

2.  在 hello 左窗格中，選取  **Active Directory**。

3.  Hello 目錄索引標籤上，選取您的目錄。

4.  按一下 [設定] 。

5.  捲動太**裝置**。

6.  針對 [使用者可以向 Azure AD 註冊其裝置] 選取 [全部]。

7.  選取 hello 最大數目的裝置，您想 tooauthorize 每位使用者。

使用 Microsoft Intune 或行動裝置管理 Office 365 的 hello 註冊需要裝置註冊。 如果您已設定任一服務，則會選取 [全部] 並停用 [無]。 請確定它們已正確設定，且有 hello 適當授權。

根據預設，不會對 hello 服務啟用雙因素驗證。 不過，建議在註冊裝置時使用雙因素驗證。

- 此服務要求雙因素驗證，您必須在 Azure Active Directory 中設定雙因素驗證提供者和設定您的使用者帳戶的多重要素驗證，請參閱新增多因素驗證tooAzure Active Directory

- 如果您搭配使用 AD FS 與 Windows Server 2012 R2，則必須在 AD FS 中設定雙因素驗證模組，請參閱＜搭配使用 Multi-Factor Authentication 與 Active Directory 同盟服務＞。

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a>在 Azure Active Directory 中檢視和管理裝置物件

從 hello Azure 系統管理員入口網站，您可以檢視、 封鎖和解除封鎖裝置。 已封鎖的裝置將不再有存取 tooapplications 設定的 tooallow 只有已註冊的裝置。

**tooview 和管理 Azure Active Directory 中的裝置物件：**
 
1.  Toohello Microsoft Azure 入口網站管理員身分登入。

2.  在 hello 左窗格中，選取  **Active Directory**。

3.  選取您的目錄。

4.  選取 [使用者]。 

5.  按一下您想要的 toosee hello 裝置 hello 使用者。

6.  選取 [裝置]。

7.  選取 [註冊的裝置]。

現在，您可以檢閱、 封鎖或解除封鎖 hello 使用者已註冊的裝置。
會在內部部署網域和自動註冊的 Windows 10 裝置不會出現在 hello 使用者 索引標籤下。請使用 hello Get MsolDevice PowerShell 命令 toofind 所有企業裝置。 


## <a name="next-steps"></a>後續步驟

toosetup 自動裝置註冊，請參閱[如何 tooconfigure 自動註冊的 Windows 網域的裝置與 Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)。


