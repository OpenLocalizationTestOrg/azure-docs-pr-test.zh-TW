---
title: "在 Azure Active Directory aaaIntroduction toodevice 管理 |Microsoft 文件"
description: "瞭解裝置的管理可以協助您 tooget 控制 hello 裝置存取您的環境中的資源。"
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
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: e2fc0a3e8d00dc69cf01db9074e34427e396cfcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodevice-management-in-azure-active-directory"></a>Azure Active Directory 中的簡介 toodevice 管理

在行動裝置-首先，雲端優先世界中，Azure Active Directory (Azure AD) 可讓單一登入 toodevices、 應用程式和服務從任何地方。 Hello 激增裝置-包括攜帶您自己的裝置 (BYOD)，與 IT 專業人員正面臨著逼近對方的兩個目標：

- 無論在何處，每當加持 hello 使用者 toobe 生產力
- 在任何階段保護 hello 公司資產

透過裝置，您的使用者能夠存取 tooyour 公司資產。 tooprotect 公司資產，身為 IT 管理員，您會想 toohave 控制這些裝置。 這可讓您 toomake 確定您的使用者會從符合您的安全性與相容性的標準的裝置存取您的資源。 

裝置管理也是 hello 基礎[裝置型條件式存取](active-directory-conditional-access-policy-connected-applications.md)。 使用裝置型條件式存取，您可以確保的存取您的環境中 tooresources 只適用於受信任的裝置。   

本主題說明 Azure Active Directory 中的裝置管理運作方式。

## <a name="getting-devices-under-hello-control-of-azure-ad"></a>取得 Azure AD 的 hello 控制下的裝置

tooget hello 控制項下的 Azure AD 的裝置，您有兩個選項：

- 註冊 
- 加入

**註冊**裝置 tooAzure AD 可讓您 toomanage 裝置的身分識別。 裝置註冊時，Azure AD 裝置註冊提供 hello 裝置是使用的 tooauthenticate hello 裝置時使用者 」 登入時 AD tooAzure 的身分。 您可以使用 hello 識別 tooenable 或停用裝置。

與 Microsoft Intune 等行動裝置 management(MDM) 解決方案結合時，在 Azure AD 中的 hello 裝置屬性會更新 hello 裝置有關的其他資訊。 這可讓您 toocreate 條件式存取規則，以強制從裝置 toomeet 存取您的安全性與相容性的標準。 如需如何在 Microsoft Intune 中註冊裝置的詳細資訊，請參閱＜在 Intune 中註冊要管理的裝置＞。

**聯結**裝置是副檔名 tooregistering 裝置。 這表示，它可讓您獲得所有 hello 優勢註冊裝置，以及在加法 toothis，它也會變更裝置的 hello 本機狀態。 變更 hello 本機狀態可讓您使用組織的工作或學校帳戶，而不個人帳戶的使用者 toosign 中 tooa 裝置。

## <a name="azure-ad-registered-devices"></a>Azure AD 註冊裝置   

hello 的目標 Azure AD 註冊的裝置是您的支援 hello tooprovide**攜帶您自己的裝置 (BYOD)**案例。 在此案例中，使用者可以使用個人裝置存取貴組織的 Azure Active Directory 受控資源。  

![Azure AD 註冊裝置](./media/device-management-introduction/03.png)

hello 存取根據已輸入 hello 裝置的工作或學校帳戶。  
例如，Windows 10 可讓使用者 tooadd 工作或學校帳戶 tooa 個人電腦、 平板電腦或電話。  
當將使用者新增工作或學校帳戶，hello 裝置是向 Azure AD 註冊，並選擇性地註冊您的組織已設定的 hello 行動裝置管理 (MDM) 系統中。 貴組織的使用者可以將工作或學校帳戶 tooa 個人裝置方便：

- 當存取 hello 第一次的工作應用程式
- 手動透過 hello**設定**功能表中的 Windows 10 的 hello 大小寫 

您可以為 Windows 10、iOS、Android 和 macOS 設定 Azure AD 註冊裝置。

## <a name="azure-ad-joined-devices"></a>Azure AD 加入裝置

加入 Azure AD 裝置 hello 目標是 toosimplify:

- Windows 部署工作用的裝置 
- 存取 tooorganizational 應用程式和任何 Windows 裝置的資源

![Azure AD 註冊裝置](./media/device-management-introduction/02.png)


這些目標被透過提供自助服務體驗中的使用者，讓 Azure AD 的 hello 控制下工作所擁有的裝置。  
**Azure AD Join** 適用於雲端優先/僅限雲端的組織。 這些通常是不具內部部署 Windows Server Active Directory 基礎結構的中小型企業。 

實作已加入 Azure AD 裝置可以提供下列優點 hello:

- **單一登入 (SSO)** tooyour Azure 管理 SaaS 應用程式和服務。 存取工作資源時，您的使用者看不到額外的驗證提示。 hello SSO 功能是，即使當它們不是可用的連接的 toohello 網域網路。

- 在跨加入裝置之間進行使用者設定的**企業符合規範漫遊**。 使用者不需要 tooconnect Microsoft 帳戶 (例如 Hotmail) toosee 設定跨裝置。

- **商務用市集存取 tooWindows**使用 AD 帳戶。 您的使用者可以選擇從清查 hello 組織預先選取的應用程式。

- **用 Windows Hello**安全且方便存取 toowork 資源的支援。

- **存取的限制**tooapps 從符合相容性原則的裝置。

雖然 Azure AD Join 主要適用於沒有內部部署 Windows Server Active Directory 基礎結構的組織，您當然也可以在下列情況下使用之：

- 例如，如果您需要 tooget 行動裝置如平板電腦和手機控制下的，您無法使用在內部部署網域聯結。

- 您的使用者主要需要 tooaccess Office 365 或其他與 Azure AD 整合的 SaaS 應用程式。

- 您想 toomanage 一群使用者，而不是在 Active Directory 中的 Azure AD 中。 這可以套用，比方說，tooseasonal 工作者、 約聘員工或學生。

- 您想在具有有限的內部部署基礎結構的遠端分公司 tooprovide 聯結功能 tooworkers。

您可以設定適用於 Windows 10 裝置的 Azure AD 已加入裝置。


## <a name="hybrid-azure-ad-joined-devices"></a>混合式 Azure AD 已加入裝置

超過十年以上，許多組織已使用 hello 網域聯結 tootheir 在內部部署 Active Directory tooenable:

- IT 部門 toomanage 工作所擁有的裝置從中央位置。

- Tootheir 裝置向其 Active Directory 中的使用者 toosign 工作或學校帳戶。 

通常，組織在內部部署磁碟使用量依賴影像方法 tooprovision 裝置，並經常使用**System Center Configuration Manager (SCCM)**或**群組原則 (GP)** toomanage它們。

如果您的環境具有內部部署 AD 使用量，並也獲益 hello Azure Active Directory 所提供的功能，您可以實作混合式已加入 Azure AD 裝置。 這些是兩者的裝置，聯結的 tooyour 內部部署 Active Directory 與 Azure Active Directory。

![Azure AD 註冊裝置](./media/device-management-introduction/01.png)


您應該使用 Azure AD 混合式加入裝置，如果：

- 您有使用 NTLM 的 Win32 應用程式部署的 toothese 裝置 / Kerberos。

- 您需要 GP 或使用 SCCM / DCM toomanage 裝置。

- 您想 toocontinue toouse 影像解決方案 tooconfigure 裝置的員工。

您可以針對 Windows 10 及舊版裝置 (例如 Windows 8 和 Windows 7) 設定混合式 Azure AD 已加入裝置。

## <a name="summary"></a>摘要

使用 Azure AD 中的裝置管理，您可以： 

- 簡化 Azure AD 的 hello 控制權攜帶裝置 hello 程的序

- 為使用者提供輕鬆 toouse 存取 tooyour 組織的雲端資源

根據經驗法則，您應該使用：

- 適用於個人裝置的 Azure AD 註冊裝置

- Azure AD 已加入裝置的裝置加入 tooan 在內部部署 AD 

- Azure AD 混合式已加入裝置的裝置加入 tooan 在內部部署 AD     




## <a name="next-steps"></a>後續步驟

- 如何在 toomanage 裝置 hello Azure 入口網站，請參閱概觀 tooget[管理使用 hello Azure 入口網站的裝置](device-management-azure-portal.md)

- toolearn 進一步了解裝置型條件式存取，請參閱[設定 Azure Active Directory 裝置型條件式存取原則](active-directory-conditional-access-policy-connected-applications.md)。

- toosetup 混合加入 Azure AD 裝置，請參閱[tooconfigure 混合 Azure Active Directory 如何聯結裝置](device-management-hybrid-azuread-joined-devices-setup.md)。


