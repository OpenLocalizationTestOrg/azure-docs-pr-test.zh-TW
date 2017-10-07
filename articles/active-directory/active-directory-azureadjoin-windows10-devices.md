---
title: "在您的工作場所 aaaUsing Windows 10 裝置 |Microsoft 文件"
description: "提供功能的快照集的使用者和 IT 消費化、 對比 hello 不同的方式可以佈建裝置，並與 Windows 10 企業中使用。"
services: active-directory
documentationcenter: 
author: femila
manager: swadhwa
editor: 
tags: azure-classic-portal
ms.assetid: 94ccc8fd-b17b-4fda-8d56-9d87aa37a9f9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 8767e1649ced8737d20875f425c24198dcaa7f6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-windows-10-devices-in-your-workplace"></a>在您的工作場所中使用 Windows 10 裝置
適用於︰Windows 10 電腦

Windows 10 提供三個模型的組織，使用者 tooaccess 工作資源啟用安全且方便的方式。

* **Azure Active Directory Join** (Azure AD Join)，針對工作者存取資源，例如主要 hello 雲端中的 Office 365。 Azure AD Join 是 Windows 10 中新增的自助式工作佈建體驗。
* **加入網域**，適用於已投資於內部部署應用程式和資源的組織。 網域加入提供較佳的體驗，在連接時，Windows 10 tooAzure AD。
* **新的簡化 BYOD 體驗**，針對想 tooadd 工作的使用者帳戶或學校 tooWindows，輕鬆地存取個人的裝置上的資源。

hello 下表列出適用於使用者和 IT 系統管理員，對照 hello 不同的方式可以佈建裝置，並使用與 Windows 10 企業功能的快照集：

|  | 加入網域 | Azure AD Join | 個人裝置 |
| --- | --- | --- | --- |
| 使用公司帳戶或學校帳戶登入 Windows 裝置。 |是 |是 |否 |
| 使用者單一登入 (SSO) tooOffice 365 與 Azure AD 應用程式。 SSO 是讓 hello 能力 toosign 中只有一次 tooaccess 組織資源。 |是 |是 |是 |
| 使用者的 SSO tooKerberos/NTLM 應用程式。 |是 |限制 |是，透過 VPN |
| 透過 Microsoft Passport 和 Windows Hello 讓公司帳戶或學校帳戶進行增強式驗證與便利的登入。 |是 |是 |是 |
| 存取 tooenterprise Windows 市集使用公司或學校帳戶 （而不是 Microsoft 帳戶）。 |是 |是 |是 |
| 使用公司帳戶或學校帳戶進行符合企業標準的跨裝置使用者設定漫遊。 |是 |是 |是 |
| hello 能力 toorestrict 存取 tooorganizational 應用程式 toodevices 與組織的裝置原則相容。 |是 |是 |是 |
| 使用者可進行裝置的自助式佈建以「隨處工作」。 |否 |是 |是 |
| 能力 toomanage 裝置。 |是，透過 GP/SCCM |是 |是 |

## <a name="use-work-owned-devices-with-azure-ad-join-and-domain-join-in-windows-10"></a>在 Windows 10 中搭配 Azure AD Join 和加入網域使用工作用的裝置
Windows 10 提供兩個工作所擁有的裝置 tooaccess 工作資源的方式：

* Azure AD Join
* 加入網域
  
  兩者都是有效的選項，視組織的需要和需求而定。 在某些情況下，組織可能會受益於同時使用這兩種方法進行部署。

## <a name="when-toouse-azure-active-directory-join"></a>當 toouse Azure Active Directory Join
Azure AD Join 是 Windows 10 中新的自助式工作佈建體驗。  目標是存取工作資源，例如主要 hello 雲端中的 Office 365 的工作者。 它是輕量方式 tooconfigure 電腦、 平板電腦和手機 hello 企業版。 在 Windows 平台之間使用一致的控制功能，透過行動裝置管理來管理裝置。

**您可以基於下列任何原因使用「加入 Azure AD」**：

* 您想 tooenable hello 自助服務佈建裝置的 hello 工作者。
* 您為使用者提供工作用的行動裝置，例如平板電腦和手機。
* 在您要 toomanage 一組使用者的 Azure AD 而不是在 Active Directory 中，例如季節性的背景工作、 約聘員工或學生。
* 您想在具有有限的內部部署基礎結構的遠端分公司 tooprovide 聯結功能 tooworkers。
* 您沒有內部部署 Active Directory。

某些組織會使用 Azure AD Join 做 hello 主要方式 toodeploy 工作所擁有的裝置，特別是大部分或所有其資源 toohello 雲端將移轉。 與 Active Directory 和 Azure AD 混合式組織也可以選擇 toodeploy 其中一種方法或另一個根據 hello 使用者或部門。

比方說，學區和大學會在 Active Directory 中管理職員，在 Azure AD 中管理學生。 在 Azure AD 中有些公司可能會想 toomanage 遠端辦公室或銷售部門。 Azure AD Join 和加入網域方法都可在混合式組織中使用。 加入 azure AD 可以是很好的補數 toodomain 聯結部署工作環境中的裝置。

**如果透過 hello 雲端 hello 最平常存取 tooenterprise 資源時，您的組織可能享受額外的好處**:

* 可以免除對內部部署身分識別基礎結構的倚賴。
* 可以啟用自助式設定擺脫映像處理解決方案，而簡化您的裝置部署模型。
* 您可以使用行動裝置管理 toomanage 所有裝置，各種不同平台。

如需有關 Azure AD Join 的詳細資訊，請參閱[擴充雲端功能 tooWindows 10 裝置透過 Azure Active Directory Join](active-directory-azureadjoin-overview.md)。

## <a name="when-toouse-domain-join-or-keep-using-it"></a>當 toouse 網域加入 （或繼續使用它）
Hello 過去 15 年，許多組織使用的是網域聯結 tooconnect 工作的裝置。 它可讓使用者 toosign tootheir 裝置向其 Active Directory 中的工作或學校帳戶。 也可讓 IT toocentrally 加入網域，並完全管理這些裝置。 組織通常依賴影像方法 tooprovision 裝置，而且通常可以使用 System Center Configuration Manager (SCCM) 或群組原則 (GP) toomanage 它們。

**基於下列任何理由，您的企業應該使用 (或繼續使用) 加入網域**：

* 您必須使用 NTLM/Kerberos 的 Win32 應用程式部署的 toothese 裝置。
* 您需要 GP 或 SCCM/DCM toomanage 裝置。
* 您想 toocontinue toouse 影像解決方案 tooconfigure 裝置的員工。

**在 Windows 10 中的網域加入也可讓您 hello 下列優勢在於，當連線 tooAzure AD**:

* 透過 Microsoft Passport 和 Windows Hello 進行公司帳戶或學校帳戶的增強式驗證與便利的登入。
* 存取 toohello 企業 Windows 市集裝置，使用工作或學校帳戶 （不需要 Microsoft 帳戶）。
* 使用公司帳戶或學校帳戶進行符合企業標準的跨裝置使用者設定漫遊 (不需要 Microsoft 帳戶)。
* hello 能力 toorestrict 存取 tooorganizational 應用程式 toodevices 與組織的裝置原則相容。

如需有關 Azure AD Join 的詳細資訊，請參閱[擴充雲端功能 tooWindows 10 裝置透過 Azure Active Directory Join](active-directory-azureadjoin-overview.md)。

## <a name="enable-joining-of-personally-owned-devices-for-work-or-school"></a>讓個人擁有的裝置在工作或學校中加入
toosupport BYOD hello 企業，Windows 10 中的提供 hello 使用者 hello 能力 tooadd 工作或學校帳戶 tootheir 電腦、 平板電腦或電話。 Hello 之後使用者新增工作或學校帳戶，hello 裝置是向 Azure AD 註冊並選擇性地在 hello 組織已設定的 hello 行動裝置管理系統中註冊。 '已註冊' vs hello 目錄會顯示這些裝置。Azure AD Join。 IT 管理員可根據這項資訊套用不同的原則，在必要時在個人擁有的裝置上提供比工作用裝置更少的操作。

使用者可以將工作或學校帳戶 tootheir 個人裝置非常方便。 他們可以執行這項操作時存取工作的應用程式的 hello 第一次，或他們可以執行手動透過 hello 設定功能表。 此帳戶會提供 SSO tooorganizational 資源。

如需有關 Azure AD Join 的詳細資訊，請參閱[連接已加入網域裝置 tooAzure AD 以進行 Windows 10 體驗](active-directory-azureadjoin-devices-group-policy.md)。

## <a name="enable-domain-join-or-azure-ad-join"></a>啟用加入網域或 Azure AD Join
稍早所述的所有方法 （加入網域、 加入 Azure AD，並新增公司或學校帳戶） 中 hello Windows 10 使用者體驗有進入點。 不過，所有必須 hello 基礎結構中的 IT 系統管理員 tooenable hello 功能才能運作 hello 體驗。

## <a name="requirements-for-deploying-azure-ad-join"></a>Azure AD Join 的部署需求
任何一組使用者的 Azure AD Join toodeploy 您需要遵循的 hello:

* Azure AD 訂用帳戶。
* Azure AD Premium 訂用帳戶，例如行動裝置管理自動註冊 (如果您需要更多的功能)。
* 行動裝置管理-例如 Microsoft Intune 訂閱、 Office 365 的行動裝置管理或任何 hello 協力廠商行動裝置管理廠商與 Azure AD 整合。 (請參閱 hello[常見問題集 > 一節](#frequently-asked-questions)本文，如需詳細資訊的 hello 結尾附近)。

如果您的設備為混合式，我們強烈建議您部署 Azure AD Connect tooextend hello 在內部部署目錄 tooAzure AD。

## <a name="requirements-for-using-domain-join-with-azure-ad"></a>使用加入網域與 Azure AD 的需求
加入網域會繼續 toowork，因為它一律具有。 不過，tooget hello Azure AD 的優點您需要遵循的 hello:

* Azure AD 訂用帳戶。
* 若要部署的 Azure AD Connect tooextend hello 在內部部署目錄 tooAzure AD。
* 允許已加入網域裝置 toohave 條件式存取 tooAzure AD 原則。
* 允許存取太 「 加入網域的 「 裝置，如果您想 toobe toorestrict 無法存取某些裝置的原則。
* System Center Configuration Manager Technical Preview，tooenable 規則需要相容的裝置 1509年版。 （請參閱 hello TechNet 文件和部落格文章）。

如需在 Windows 10 中加入網域的詳細資訊，請參閱[連接已加入網域裝置 tooAzure AD 以進行 Windows 10 體驗](active-directory-azureadjoin-devices-group-policy.md)

## <a name="requirements-for-using-byod-and-add-a-work-or-school-account"></a>使用 BYOD 和「新增公司帳戶或學校帳戶」的需求
tooenable 「 攜帶您自己的裝置 」 (BYOD) 工作或學校帳戶，您需要下列 hello:

* Azure AD 訂用帳戶。
* Azure AD Premium 訂用帳戶，例如行動裝置管理自動註冊 (如果您需要更多的功能)。

## <a name="requirements-for-using-microsoft-passport"></a>使用 Microsoft Passport 的需求
tooenable Microsoft Passport，您需要下列 hello:

* 公開金鑰基礎結構 (PKI)，以支援使用 Microsoft Passport 的憑證型驗證。
* Intune 訂用帳戶，以支援將 Microsoft Passport 用於 Azure AD Join 和公司帳戶或學校帳戶的憑證型驗證。
* System Center Configuration Manager Technical Preview 1509 版 （請參閱 hello TechNet 文件和部落格文章） 使用 Microsoft Passport 的網域加入的憑證基礎的驗證支援。
* 啟用 Microsoft Passport hello 組織中部署的原則。

做為替代 toousing PKI，您可以藉由 hello 下列啟用金鑰為基礎的 Microsoft Passport:

* 部署 Windows Server 2016 "Production Preview 1" DC (在網域或樹系功能層級上不需要；以數個 DC 為每個 Active Directory 網站提供備援功能即已足夠)。
* 設定原則 tooenable Microsoft Passport hello 組織中。

如需 Windows 10 中 Microsoft Passport 和 Windows Hello 的詳細資訊，請參閱 <link-to-MS-Passport-and-Windows-Hello-document>。

## <a name="frequently-asked-questions"></a>常見問題集
### <a name="which-partner-mobile-device-management-products-integrate-with-azure-ad"></a>哪些協力廠商行動裝置管理產品與 Azure AD 整合？
hello 下列廠商產品與整合 Azure AD 整合的註冊和 Windows 10 中的條件式存取：

* AirWatch by VMware
* Citrix Xenmobile
* Lightspeed Mobile Manager
* SOTI 內部部署行動裝置管理
* MobileIron

### <a name="what-about-workplace-join-in-windows-10"></a>Windows 10 中的「加入工作場所」有何功能？
Windows 8.1 tooenable BYOD 中使用工作地方聯結。 在 Windows 10 中，必須透過本文稍早所述的「新增公司帳戶或學校帳戶」來啟用 BYOD。 不與 Azure AD 整合其行動裝置管理的組織，使用者可以手動透過管理註冊裝置 hello**設定** > **帳戶** > **工作存取**。

### <a name="can-users-connect-their-microsoft-account-tootheir-domain-account-in-windows-10"></a>使用者可以連線其 Microsoft 帳戶 tootheir 網域帳戶在 Windows 10 嗎？
在 Windows 10 中不行。 在 Windows 8.1 中已加入網域裝置的使用者可以 「 連接 」 其 Microsoft 帳戶 （例如 Hotmail、 Live、 Outlook、 Xbox、 等等） tootheir 網域帳戶 tooenable 如 SSO tooLive 服務、 使用 Windows 市集 hello 和漫遊的特定體驗在裝置上的使用者設定。 在 Windows 10 中已淘汰 hello 「 連接 」 功能的 Microsoft 帳戶。 hello 使用者可以新增一或多個 Microsoft 帳戶做為其他帳戶 tooenable SSO tooconsumer 服務，例如 hello Windows 市集。 這作業可在 [設定]  >  [帳戶]  >  [您的帳戶] 中完成。

升級，並從 Windows 8.1 網域的裝置並誰有其 Microsoft 帳戶連接的使用者，會自動擁有其已連線的 Microsoft 帳戶加入 toohello 他們使用的其他帳戶清單。

## <a name="additional-information"></a>其他資訊
* [Hello 企業版的 Windows 10： 工作的方式 toouse 裝置](active-directory-azureadjoin-windows10-devices-overview.md)
* [擴充功能 tooWindows 10 裝置透過 Azure Active Directory 加入雲端](active-directory-azureadjoin-user-upgrade.md)
* [了解適用於 Azure AD Join 的使用案例](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [連接已加入網域裝置 tooAzure AD 進行 Windows 10 體驗](active-directory-azureadjoin-devices-group-policy.md)
* [設定 Azure AD Join](active-directory-azureadjoin-setup.md)

