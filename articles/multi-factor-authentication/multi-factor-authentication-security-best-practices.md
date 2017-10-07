---
title: "為 MFA aaaSecurity 最佳作法 |Microsoft 文件"
description: "本文件提供搭配 Azure 帳戶使用 Azure MFA 的最佳做法"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3be7d968-96bb-4320-8701-869fd04a2595
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 7f18c2592764878b842d81783b321a05f29ee3d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-best-practices-for-using-azure-multi-factor-authentication-with-azure-ad-accounts"></a>搭配 Azure AD 帳戶使用 Azure Multi-Factor Authentication 的安全性最佳做法

雙步驟驗證是慣用的 hello 選擇大部分的組織希望 tooenhance 其驗證程序。 Azure Multi-Factor Authentication (MFA) 協助公司符合其安全性和合規性需求，同時為使用者提供簡單的登入體驗。 本文涵蓋了規劃 hello 採用的 Azure MFA 時，您應該考慮的一些秘訣。

## <a name="deploy-azure-mfa-in-hello-cloud"></a>部署 hello 雲端中的 Azure MFA

有兩種方式 tooenable Azure MFA 給所有使用者。

* 為每個使用者購買授權 (Azure MFA、Azure AD Premium 或 Enterprise Mobility + Security)
* 建立 Multi-Factor Auth Provider，並依每個使用者或每次驗證付費

### <a name="licenses"></a>授權
![EMS](./media/multi-factor-authentication-security-best-practices/ems.png)

如果您有 Azure AD Premium 或 Enterprise Mobility + Security 授權，則您已經有 Azure MFA。 您的組織不需要任何額外 tooextend hello 雙步驟驗證功能 tooall 使用者。 您只需要 tooassign 授權 tooa 使用者，然後您可以開啟 MFA。

設定多因素驗證，請考慮下列秘訣 hello:

* 不要建立依每次驗證的 Multi-Factor Auth Provider。 如果這麼做，您可能因為已有授權的使用者提出驗證要求而需要付費。
* 如果您沒有足夠的授權給所有使用者，您可以建立您組織的每位使用者的 Multi-factor Auth 提供者 toocover hello rest。 
* 唯有當您將內部部署 Active Directory 環境與 Azure AD 目錄同步處理時，才需要 Azure AD Connect。 如果您使用不與內部部署 Active Directory 執行個體同步處理的 Azure AD 目錄，就不需要 Azure AD Connect。

### <a name="multi-factor-auth-provider"></a>Multi-Factor Auth Provider
![Multi-Factor Auth Provider](./media/multi-factor-authentication-security-best-practices/authprovider.png)

如果沒有包含 Azure MFA 的授權，您可以建立 MFA 驗證提供者。 

在建立 hello Auth 提供者時，您需要 tooselect 目錄，並考慮下列詳細資料的 hello:

* 您不需要 Azure AD 目錄 toocreate Multi-factor Auth 提供者，但取得更多的功能，其中包含一個。 Azure AD 目錄中與 hello Auth 提供者時，會啟用下列功能的 hello:  
  * 將雙步驟驗證 tooall 擴充您的使用者  
  * 會提供其他功能，例如 hello 管理入口網站、 自訂問候及報告讓全域管理員。
* 如果您將內部部署 Active Directory 環境與 Azure AD 目錄同步處理，則需要 DirSync 或 AAD Sync。如果您使用不與內部部署 Active Directory 執行個體同步處理的 Azure AD 目錄，就不需要 DirSync 或 AAD Sync。
* 選擇最適合您企業的 hello 取用模型。 一旦您選取 hello 使用量模型，您無法變更它。 hello 的兩個模型如下：
  * 每次驗證︰向您收取每次驗證的費用。 如果您想要所有存取特定應用程式的人員都使用雙步驟驗證，請使用這個模型。
  * 每個啟用的使用者︰會針對啟用 Azure MFA 的每個使用者向您數費。 如果您有某些使用者具有 Azure AD Premium 或 Enterprise Mobility Suite 授權，有些則沒有，請使用此模型。

### <a name="supportability"></a>支援能力
由於大部分使用者都是習慣的 toousing 只有密碼 tooauthenticate，務必貴公司帶來感知 tooall 使用者關於此程序。 此認知可以減少使用者連絡服務台，用於一些小問題相關 tooMFA hello 可能性。 不過，有一些案例是需要暫時停用 MFA。 下列指導方針 toounderstand 如何使用 hello toohandle 這些案例：

* 訓練您其中 hello 使用者無法登入，因為 hello 行動裝置應用程式或電話未收到通知或電話的技術支援人員 toohandle 案例。 技術支援人員可以[啟用一次性略過](multi-factor-authentication-whats-next.md#one-time-bypass)tooallow 使用者 tooauthenticate 「 略過 「 雙步驟驗證一次。 hello 略過是暫時性的指定的秒數後過期。
* 請考慮 hello[信任的 Ip 功能](multi-factor-authentication-whats-next.md#trusted-ips)中做為方法 toominimize 雙步驟驗證的 Azure MFA。 利用此功能的受管理或同盟租用戶系統管理員可以略過從 hello 公司近端內部網路登入的使用者的雙步驟驗證。 hello 功能可供 Azure AD Premium、 Enterprise Mobility Suite 或 Azure Multi-factor Authentication 授權的 Azure AD 租用戶。

## <a name="best-practices-for-an-on-premises-deployment"></a>內部部署的最佳作法
如果您的公司決定 tooleverage 它自己的基礎結構 tooenable MFA，您需要的 toodeploy Azure Multi-factor Authentication Server 的內部。 hello 下列圖表顯示 hello MFA 伺服器元件：

![MFA Server 預設元件︰主控台、同步處理引擎、管理入口網站、雲端服務](./media/multi-factor-authentication-security-best-practices/server.png) \*依預設未安裝\**已安裝，但依預設未啟用

Azure Multi-Factor Authentication Server 可以使用同盟來保護雲端資源和內部部署資源的安全。 您必須擁有 AD FS 並讓它與您的 Azure AD 租用戶同盟。
設定 Multi-factor Authentication Server，請考慮下列詳細資料的 hello:

* 如果您的安全使用 Active Directory Federation Services (AD FS)，就會進行 hello 第一個驗證步驟的 Azure AD 資源之內部使用 AD FS。 hello 第二個步驟是內部執行區分 hello 宣告。
* 您不需要 tooinstall hello Azure Multi-factor Authentication Server 在 AD FS 同盟伺服器。 不過，必須執行 AD FS 的 Windows Server 2012 R2 上安裝 hello Multi-factor Authentication Adapter for AD FS。 您可以 hello 上安裝不同的電腦，只要是支援的版本，並在 AD FS 同盟伺服器上個別安裝 hello AD FS 配接器。 
* hello Multi-factor Authentication AD FS 配接器安裝精靈會建立呼叫您的 Active Directory 中 PhoneFactor Admins 安全性群組，然後新增 AD FS 服務帳戶 toothis 群組。 請確認 hello PhoneFactor Admins 群組在您的網域控制站上建立，且該 hello AD FS 服務帳戶是這個群組的成員。 如有必要，請手動在網域控制站上新增 hello AD FS 服務帳戶 toohello PhoneFactor Admins 群組。

### <a name="user-portal"></a>使用者入口網站
hello 使用者入口網站可讓自助功能，並提供一組完整的使用者管理功能。 它在 Internet Information Server (IIS) 網站中執行。 此元件使用下列指導方針 tooconfigure hello:

* 使用 IIS 6 或更新版本
* 安裝和註冊 ASP.NET v2.0.507207
* 請確定此伺服器可以部署在周邊網路中

### <a name="app-passwords"></a>應用程式密碼
如果貴組織已針對 SSO 與 Azure AD 同盟，而且您正在使用 Azure MFA toobe，然後應注意下列詳細資料的 hello:

* hello 應用程式密碼由 Azure AD 驗證，因此會略過同盟。 唯有在設定應用程式密碼時才會使用同盟。
* 適用於同盟 (SSO) 使用者，密碼會儲存在 hello 組織識別碼。如果 hello 使用者離開公司 hello，這些資訊必須使用 DirSync tooflow tooorganizational id。 帳戶停用/刪除可能佔用 toothree 小時 toosync，因而延遲在 Azure AD 中保持在停用/刪除的應用程式密碼。
* 應用程式密碼不會遵守內部部署用戶端存取控制設定。
* 應用程式密碼不適用內部部署驗證記錄/稽核功能。
* 某些進階架構設計在使用雙步驟驗證時，可能需要搭配使用組織使用者名稱和密碼及應用程式密碼，需視驗證的位置而定。 對於根據內部部署基礎結構進行驗證的用戶端，您可以使用組織使用者名稱和密碼。 對 Azure AD 進行驗證的用戶端，您會使用 hello 應用程式密碼。
* 根據預設，使用者無法建立應用程式密碼。 如果您需要 tooallow 使用者 toocreate 應用程式密碼，請選取 hello**到非瀏覽器應用程式允許使用者 toocreate 應用程式密碼 toosign**選項。

## <a name="additional-considerations"></a>其他考量
針對部署在內部部署的每個元件，請使用此清單以了解其他考量和最佳做法：

- 搭配 [Active Directory Federation Service](multi-factor-authentication-get-started-adfs.md) 來設定 Multi-Factor Authentication。
- 安裝和設定 hello 與 Azure MFA Server [RADIUS 驗證](multi-factor-authentication-get-started-server-radius.md)。
- 安裝和設定 hello 與 Azure MFA Server [IIS 驗證](multi-factor-authentication-get-started-server-iis.md)。
- 安裝和設定 hello 與 Azure MFA Server [Windows 驗證](multi-factor-authentication-get-started-server-windows.md)。
- 安裝和設定 hello 與 Azure MFA Server [LDAP 驗證](multi-factor-authentication-get-started-server-ldap.md)。
- 安裝和設定 hello 與 Azure MFA Server[遠端桌面閘道和使用 RADIUS 的 Azure Multi-factor Authentication Server](multi-factor-authentication-get-started-server-rdg.md)。
- 安裝和設定 hello Azure MFA Server 之間的同步處理和[Windows Server Active Directory](multi-factor-authentication-get-started-server-dirint.md)。
- [部署 Azure Multi-factor Authentication 伺服器行動應用程式 Web 服務的 hello](multi-factor-authentication-get-started-server-webservice.md)。
- [採用 Azure Multi-Factor Authentication 的進階 VPN 設定](multi-factor-authentication-advanced-vpn-configurations.md)，適用於使用 LDAP 或 RADIUS 的 Cisco ASA、Citrix Netscaler 和 Juniper/Pulse 安全 VPN 應用裝置。

## <a name="next-steps"></a>後續步驟
雖然這篇文章強調 Azure MFA 的一些最佳做法，還有其他資源您也可以在規劃 MFA 部署時使用。 下列的 hello 清單具有某些索引鍵的文件可協助您在此程序：

* [Azure Multi-Factor Authentication 中的報告](multi-factor-authentication-manage-reports.md)
* [hello 雙步驟驗證的註冊體驗](multi-factor-authentication-end-user-first-time.md)
* [Azure Multi-Factor Authentication 常見問題集](multi-factor-authentication-faq.md)

