---
title: "使用 Azure Active Directory 連接 Active Directory。 | Microsoft Docs"
description: "Azure AD Connect 會整合您的內部部署目錄與 Azure Active Directory。 這可讓您與 Azure AD 整合 Office 365、 Azure 和 SaaS 應用程式的通用識別身分的 tooprovide。"
keywords: "簡介 tooAzure AD Connect，Azure AD Connect 的概觀，什麼是 Azure AD Connect，安裝 active directory"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 59bd209e-30d7-4a89-ae7a-e415969825ea
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: e49f2af4b67e9ed3ad093888541da7c82af0e052
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-on-premises-directories-with-azure-active-directory"></a>整合您的內部部署目錄與 Azure Active Directory
Azure AD Connect 會整合您的內部部署目錄與 Azure Active Directory。 這可讓您 tooprovide 通用識別身分為您的 Office 365、 Azure 和 SaaS 應用程式的使用者與 Azure AD 整合。 本主題將引導您完成 hello 規劃、 部署和作業步驟。 它是連結 toohello 主題相關的 toothis 區域的集合。

> [!IMPORTANT]
> [Azure AD Connect 是 hello 最佳方式 tooconnect 在內部部署目錄與 Azure AD 和 Office 365。這是很好的時間 tooupgrade tooAzure AD Connect，從 Windows Azure Active Directory 同步作業 (DirSync) 或 Azure AD Sync 因為這些工具現在已被取代，並會到達結束在 2017 年 4 月 13，支援。](active-directory-aadconnect-dirsync-deprecated.md)
> 
> 

![何謂 Azure AD Connect](media/active-directory-aadconnect/arch.png)

## <a name="why-use-azure-ad-connect"></a>使用 Azure AD Connect 的理由
將內部部署目錄與 Azure AD 整合可提供通用身分識別供存取雲端和內部部署資源，進而讓您的使用者更具生產力。 使用者和組織可以利用下列 hello:

* 使用者可以使用單一識別 tooaccess 在內部部署應用程式和雲端服務，例如 Office 365。
* 單一工具 tooprovide 同步作業和登入的方便部署經驗。
* 為您的案例提供 hello 最新功能。 Azure AD Connect 會取代舊版的身分識別整合工具，如 DirSync 和 Azure AD Sync。如需詳細資訊，請參閱 [混合式身分識別目錄整合工具比較](../active-directory-hybrid-identity-design-considerations-tools-comparison.md)。

### <a name="how-azure-ad-connect-works"></a>Azure AD Connect 運作方式
Azure Active Directory Connect 三個主要元件組成： hello 同步處理服務、 hello 選擇性 Active Directory Federation Services 元件和 hello 監視的元件，名為[Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md).

<center>![Azure AD Connect 堆疊](./media/active-directory-aadconnect-how-it-works/AADConnectStack2.png)
</center>

* 同步處理 - 此元件負責建立使用者、群組和其他物件。 它也會負責確保您在內部部署使用者和群組的識別資訊會比對 hello 雲端。
* AD FS 的同盟是 Azure AD Connect 的選擇性部分而且可以使用的 tooconfigure 混合式環境中使用內部部署 AD FS 基礎結構。 這可供組織 tooaddress 複雜的部署，例如網域加入 SSO，強制執行 AD 登入的原則和智慧卡或第 3 個合作對象 MFA。
* 健全狀況監視-Azure AD Connect Health 可以提供強大的監視，並提供中央位置，在 Azure 入口網站 tooview hello 此活動。 如需詳細資訊，請參閱 [Azure Active Directory Connect Health](../connect-health/active-directory-aadconnect-health.md)。

## <a name="install-azure-ad-connect"></a>安裝 Azure AD Connect。
您可以在找到 Azure AD Connect 的 hello 下載[Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=615771)。

| 方案 | 案例 |
| --- | --- |
| 開始之前 - [硬體和必要條件](active-directory-aadconnect-prerequisites.md) |<li>步驟 toocomplete 之前啟動 tooinstall Azure AD Connect。</li> |
| [快速設定](active-directory-aadconnect-get-started-express.md) |<li>如果您有單一樹系 AD 然後這 hello 建議 toouse 選項。</li> <li>使用者登入 hello 相同密碼使用密碼同步處理。</li> |
| [自訂設定](active-directory-aadconnect-get-started-custom.md) |<li>有多個樹系時使用。 支援許多內部部署[拓撲](active-directory-aadconnect-topologies.md)。</li> <li>自訂您登入的選項，例如同盟的 ADFS 或使用第三方身分識別提供者。</li> <li>自訂同步處理功能，例如篩選和回寫。</li> |
| [從 DirSync 升級](active-directory-aadconnect-dirsync-upgrade-get-started.md) |<li>在您有已在執行中的現有 DirSync 伺服器時使用。</li> |
| [從 Azure AD Sync 或 Azure AD Connect 升級](active-directory-aadconnect-upgrade-previous-version.md) |<li>視您的偏好而定會有數種不同的方法。</li> |

[在安裝後](active-directory-aadconnect-whats-next.md)您應該確認它已如預期般運作，並將 toohello 使用者指派授權。

### <a name="next-steps-tooinstall-azure-ad-connect"></a>後續步驟 tooInstall Azure AD Connect
|主題 |連結|  
| --- | --- |
|下載 Azure AD Connect | [下載 Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)|
|使用快速設定進行安裝 | [快速安裝 Azure AD Connect](./active-directory-aadconnect-get-started-express.md)|
|使用自訂設定進行安裝 | [自訂 Azure AD Connect 安裝](./active-directory-aadconnect-get-started-custom.md)|
|從 DirSync 升級 | [從 Azure AD 同步作業工具 (DirSync) 升級](./active-directory-aadconnect-dirsync-upgrade-get-started.md)|
|安裝後 | [確認 hello 安裝並指派授權](active-directory-aadconnect-whats-next.md)|

### <a name="learn-more-about-install-azure-ad-connect"></a>深入了解安裝 Azure AD Connect
您也需要如 tooprepare[操作](active-directory-aadconnectsync-operations.md)考量。 您可能會想 toohave 待命伺服器，讓您輕鬆地可切換如果沒有[災害](active-directory-aadconnectsync-operations.md#disaster-recovery)。 如果您計劃 toomake 頻繁的組態變更，您應該規劃[預備模式](active-directory-aadconnectsync-operations.md#staging-mode)伺服器。

|主題 |連結|  
| --- | --- |
|支援的拓撲 | [Azure AD Connect 的拓撲](active-directory-aadconnect-topologies.md)|
|設計概念 | [Azure AD Connect 的設計概念](active-directory-aadconnect-design-concepts.md)|
|用於安裝的帳戶 | [進一步了解 Azure AD Connect 認證和權限](./active-directory-aadconnect-accounts-permissions.md)|
|作業規劃 | [Azure AD Connect 同步處理：作業工作和考量](active-directory-aadconnectsync-operations.md)|
|使用者登入選項 | [Azure AD Connect 使用者登入選項](active-directory-aadconnect-user-signin.md)|

## <a name="configure-sync-features"></a>設定同步處理功能
Azure AD Connect 隨附數個您可以選擇性地開啟或預設為啟用的功能。 在特定案例與拓撲中，有些功能有時可能需要進行其他設定。

[篩選](active-directory-aadconnectsync-configure-filtering.md)您想的 toolimit 哪些物件同步處理 tooAzure AD 時使用。 預設會同步處理所有使用者、連絡人、群組和 Windows 10 電腦。 您可以變更 hello 篩選根據網域、 Ou 或屬性。

[密碼同步化](active-directory-aadconnectsync-implement-password-synchronization.md)同步處理 Active Directory tooAzure AD 中的 hello 密碼雜湊。 hello 使用者可以使用相同的密碼在內部部署，但僅限於 hello 雲端中管理它在一個位置的 hello。 因為它會使用您在內部部署 Active Directory 做為 hello 授權單位，您也可以使用您自己的密碼原則。

[密碼回寫](../active-directory-passwords-getting-started.md)會允許使用者 toochange 和重設其密碼 hello 定域機組中的並套用您在內部部署密碼原則。

[裝置回寫](active-directory-aadconnect-feature-device-writeback.md)可讓 Azure AD toobe tooon 內部部署 Active Directory 以便用於條件式存取寫入中註冊的裝置。

hello[防止被意外刪除](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)功能預設為開啟，並避免 hello 大量刪除作業的雲端目錄相同的時間。 根據預設，它每回允許 500 次刪除。 您可以根據您組織的大小來變更此設定。

[自動升級](active-directory-aadconnect-feature-automatic-upgrade.md)快速設定安裝的預設會啟用，並確保您的 Azure AD Connect 一律由 toodate hello 最新版本。

### <a name="next-steps-tooconfigure-sync-features"></a>下一個步驟 tooconfigure 同步處理功能
|主題 |連結|  
| --- | --- |
|設定篩選 | [Azure AD Connect 同步處理：設定篩選](active-directory-aadconnectsync-configure-filtering.md)|
|密碼同步處理 | [Azure AD Connect 同步處理：實作密碼同步處理](active-directory-aadconnectsync-implement-password-synchronization.md)|
|密碼回寫 | [開始使用密碼管理](../active-directory-passwords-getting-started.md)|
|裝置回寫 | [在 Azure AD Connect 中啟用裝置回寫](active-directory-aadconnect-feature-device-writeback.md)|
|防止意外刪除 | [Azure AD Connect 同步處理：防止意外刪除](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)|
|自動升級 | [Azure AD Connect：自動升級](active-directory-aadconnect-feature-automatic-upgrade.md)|

## <a name="customize-azure-ad-connect-sync"></a>自訂 Azure AD Connect 同步處理
Azure AD Connect 同步隨附預定的 toowork 大部分的客戶和拓撲之組態的預設組態。 但是一定有 hello 預設組態無法運作，以及必須調整的情況。 它是支援的 toomake 隨著記載這個區段與連結的主題。

如果您沒有使用過的同步處理拓撲想 toostart toounderstand hello 基本概念和 hello hello 中所述的詞彙之前[技術概念](active-directory-aadconnectsync-technical-concepts.md)。 Azure AD Connect 是 MIIS2003、 ILM2007，和 FIM2010 hello 演進。 即使有些東西相同，但改變的卻更多。

hello[預設組態](active-directory-aadconnectsync-understanding-default-configuration.md)假設 hello 組態中可能有多個樹系。 在那些拓撲中，使用者物件可能會表示為另一個樹系中的連絡人。 hello 使用者也可能會有另一個資源樹系連結的信箱。 hello 設定行為的 hello 預設述[使用者及連絡人](active-directory-aadconnectsync-understanding-users-and-contacts.md)。

同步的 hello 組態模型稱為[宣告式佈建](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)。 hello 進階的屬性流程使用[函式](active-directory-aadconnectsync-functions-reference.md)tooexpress 屬性轉換。 您可以看到，並檢查 hello 整個組態使用的工具隨附於 Azure AD Connect。 如果您需要 toomake 組態變更，請確定您遵循 hello[最佳做法](active-directory-aadconnectsync-best-practices-changing-default-configuration.md)因此很容易 tooadopt 新版本。

### <a name="next-steps-toocustomize-azure-ad-connect-sync"></a>後續步驟 toocustomize Azure AD Connect 同步
|主題 |連結|  
| --- | --- |
|所有 Azure AD Connect 同步處理文章 | [Azure AD Connect 同步處理](active-directory-aadconnectsync-whatis.md)|
|技術概念 | [Azure AD Connect 同步處理：技術概念](active-directory-aadconnectsync-technical-concepts.md)|
|了解 hello 預設組態 | [Azure AD Connect 同步： 了解 hello 預設組態](active-directory-aadconnectsync-understanding-default-configuration.md)|
|了解使用者和連絡人 | [Azure AD Connect 同步處理：了解使用者和連絡人](active-directory-aadconnectsync-understanding-users-and-contacts.md)|
|宣告式佈建 | [Azure AD Connect 同步處理：了解宣告式佈建運算式](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)|
|變更 hello 預設組態 | [變更 hello 預設組態的最佳作法](active-directory-aadconnectsync-best-practices-changing-default-configuration.md)|

## <a name="configure-federation-features"></a>設定同盟功能
ADFS 可以設定的 toosupport[多個網域](active-directory-aadconnect-multiple-domains.md)。 例如，您可能會有多個最上層網域，您需要為同盟的 toouse。

如果您的 ADFS 伺服器已從 Azure AD 設定的 tooautomatically 更新憑證，或如果您使用非 ADFS 方案，然後系統會通知您當您有太[更新憑證](active-directory-aadconnect-o365-certs.md)。

### <a name="next-steps-tooconfigure-federation-features"></a>下一個步驟 tooconfigure 同盟功能
|主題 |連結|  
| --- | --- |
|AD FS 的所有發行項 | [Azure AD Connect 和同盟](active-directory-aadconnectfed-whatis.md)|
|設定 ADFS 與子網域 | [與 Azure AD 同盟的多網域支援](active-directory-aadconnect-multiple-domains.md)|
|管理 AD FS 伺服器陣列 | [使用 Azure AD Connect 管理和自訂 AD FS](active-directory-aadconnect-federation-management.md)|
|手動更新同盟憑證 | [續約 Office 365 和 Azure AD 的同盟憑證](active-directory-aadconnect-o365-certs.md)|

## <a name="more-information-and-references"></a>詳細資訊和參考
|主題 |連結|  
| --- | --- |
|版本歷程記錄 | [版本歷程記錄](active-directory-aadconnect-version-history.md)|
|比較 DirSync、Azure ADSync 和 Azure AD Connect | [目錄整合工具比較](../active-directory-hybrid-identity-design-considerations-tools-comparison.md)|
|Azure AD 的非 ADFS 相容性清單 | [Azure AD 同盟相容性清單](active-directory-aadconnect-federation-compatibility.md)|
|設定 SAML 2.0 Idp|[使用 SAML 2.0 識別提供者 (IdP) 來進行單一登入](active-directory-aadconnect-federation-saml-idp.md)|
|同步處理的屬性 | [同步處理的屬性](active-directory-aadconnectsync-attributes-synchronized.md)|
|使用 Azure AD Connect Health 進行監控 | [Azure AD Connect Health](../connect-health/active-directory-aadconnect-health.md)|
|常見問題集 | [Azure AD Connect 常見問題集](active-directory-aadconnect-faq.md)|

**其他資源**

Ignite 2015 簡報擴充您的內部部署目錄 toohello 雲端。

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3862/player]
> 
> 

