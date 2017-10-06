---
title: "aaaUnderstand Azure 身分識別 |Microsoft 文件"
description: "取得 Microsoft Azure 身分識別解決方案條款、 概念和您 toomake hello 最佳身分識別控管決定為您的組織的建議的基本知識。"
keywords: 
author: jeffgilb
manager: femila
ms.reviewer: jsnow
ms.author: jeffgilb
ms.date: 7/17/2017
ms.topic: article
ms.prod: 
ms.service: azure
ms.technology: 
ms.assetid: 
ms.custom: it-pro
ms.openlocfilehash: 4d9c90bd7a6bcc9637be3107998f9da5bd4cbdae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-identity-solutions"></a>了解 Azure 身分識別解決方案
Microsoft Azure Active Directory (Azure AD) 是一個身分識別和存取管理的雲端解決方案，可提供目錄服務、身分識別治理及應用程式存取管理。 Azure AD 快速[啟用單一登入 (SSO)](https://docs.microsoft.com/azure/active-directory/active-directory-enterprise-apps-manage-sso) too1，000 的預先整合商業和自訂應用程式 hello [Azure AD 應用程式庫](https://azure.microsoft.com/marketplace/active-directory/all/)。 您可能已經使用這其中有許多應用程式，例如 Office 365、Salesforce.com、Box、ServiceNow 及 Workday。

單一 Azure AD 目錄會在建立時自動與 Azure 訂用帳戶產生關聯。 為 Azure 中的 hello 身分識別服務，然後 Azure AD 會提供所有身分識別管理和存取控制功能的雲端式資源。 這些資源包括使用者、 應用程式及群組的個別租用戶 （組織） 中 hello 下列圖表所示：

![Azure Active Directory](./media/understand-azure-identity-solutions/azure-ad.png)

Microsoft Azure 提供數種方式 tooleverage 識別為服務 (IDaaS) 與不同層級的複雜性 toomeet 個別組織的需求。 hello 本文其餘部分，可協助您了解基本 Azure 身分識別的詞彙和概念，以及您 toomake hello 最好的選擇從 hello 可用之選項的建議。

## <a name="terms-tooknow"></a>條款 tooknow

您可以為您的組織決定 Azure 身分識別解決方案之前，您會需要 hello 條款論及 Azure 識別服務時常用的基本知識。

|詞彙 tooknow| 說明|
|-----|-----|
|Azure 訂閱 |訂閱是使用 Azure 雲端服務的 toopay，通常連結的 tooa 信用卡。 您可以有數個訂閱，但可能很難 tooshare 訂用帳戶之間的資源。|
|Azure 租用戶 | Azure AD 租用戶是代表單一組織。 它是組織在註冊 Microsoft 雲端服務訂用帳戶 (例如 Azure、Intune 或 Office 365) 時，自動建立的專屬且受信任 Azure AD 執行個體。 租用戶可以獲得存取 tooservices 在任一個專用的環境 （單一租用戶），或在與其他組織 （多租用戶） 共用的環境。|
|Azure AD 目錄 | 每個 Azure 租用戶都有專用的受信任的 Azure AD 目錄，包含 hello 租用戶的使用者、 群組和應用程式。 它是租用戶資源的使用的 tooperform 身分識別和存取管理功能。 因為唯一 Azure AD 目錄會自動佈建的 toorepresent 貴組織註冊 Microsoft 雲端服務，例如 Azure、 Microsoft Intune 或 Office 365 時，您會有時看到 hello 詞彙*租用戶*，*Azure AD*，和*Azure AD 目錄*交替使用。 |
|自訂網域 | 當您第一次註冊 Microsoft 雲端服務訂用帳戶時，您的租用戶 (組織) 會使用 .onmicrosoft.com 網域名稱。 不過，大部分組織擁有一或多個網域名稱是使用的 toodo 商務和使用者使用 tooaccess 公司資源。 您可以新增您的自訂網域名稱 tooAzure AD，以便 hello 網域名稱是熟悉 tooyour 使用者，例如 *alice@contoso.com* 而不是 *alice@contoso.onmicrosoft.com* 。 |
|Azure AD 帳戶 | 這些身分識別是使用 Azure AD 或其他 Microsoft 雲端服務 (例如 Office 365) 所建立的。 在 Azure AD 中儲存和存取 tooany hello 組織的雲端服務訂閱。 |
|Azure 訂用帳戶管理員| hello 帳戶系統管理員是 hello 人員註冊或購買 hello Azure 訂用帳戶。 他們可以使用 hello[帳戶中心](https://account.windowsazure.com/Home/Index)tooperform 各項管理工作，例如建立訂用帳戶、 取消訂用帳戶、 變更 hello 計費訂用帳戶，或變更 hello 服務系統管理員。 |
|Azure AD 全域系統管理員 | Azure AD 全域系統管理員具有完整存取 tooall Azure AD 系統管理功能。 hello 註冊人員的 Microsoft 雲端服務訂用帳戶會自動根據預設，會成為全域管理員。 您可以有一個以上的全域管理員，但只有全域管理員才能指派任一[hello 其他系統管理員角色](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal)toousers。 |
|Microsoft 帳戶 | （您建立的個人使用） 的 Microsoft 帳戶提供存取 tooconsumer 導向的 Microsoft 產品與雲端服務，例如 Outlook (Hotmail)、 OneDrive、 Xbox LIVE 或 Office 365。 這些身分識別建立和儲存在 hello Microsoft 所執行的 Microsoft 消費者識別帳戶系統中。|
|工作或學校帳戶 | （用於商務/學術作業管理員發出） 的工作或學校帳戶提供 tooenterprise 商業層級 Microsoft 雲端服務中的，例如 Azure、 Intune 或 Office 365 的存取。|


## <a name="concepts-toounderstand"></a>概念 toounderstand

您現在知道 hello 基本 Azure 身分識別的詞彙，您應該深入了解這些 Azure 身分識別的概念可協助您做出明智的 Azure 身分識別的服務決定。

|概念 toounderstand |說明|
|-----|-----|
|[Azure 訂用帳戶如何與 Azure Active Directory 產生關聯](https://docs.microsoft.com/azure/active-directory/active-directory-how-subscriptions-associated-directory) |每個 Azure 訂用帳戶具有信任關係之 azure AD 目錄 tooauthenticate 使用者、 服務和裝置。 *多個訂閱可以信任 hello 相同的 Azure AD 目錄中，但訂用帳戶只會信任單一 Azure AD 目錄*。 此信任關係是不同的訂用帳戶已與其他 Azure 資源 （網站、 資料庫等等），後者比較像是訂閱的子資源的 hello 關係。 如果訂閱已過期，則 Azure AD hello 訂用帳戶相關聯的存取 tooresources 也會停止。 不過，hello Azure AD 目錄會保留在 Azure 中，以便您可以將其他訂用帳戶與該目錄產生關聯，並繼續 toomanage 租用戶資源。|
|[Azure AD 授權的運作方式](https://docs.microsoft.com/azure/active-directory/active-directory-licensing-get-started-azure-portal) | 當您購買或啟用 Enterprise Mobility Suite、 Azure AD Premium 或 Azure AD Basic，您的目錄會更新與 hello 訂用帳戶，包括其有效期間內，而且預付授權。 一旦 hello 訂用帳戶正在使用時，就可以由 Azure AD 全域系統管理員管理和使用授權的使用者 hello 服務。 您的訂用帳戶資訊，包括 hello 分派或可用授權數目 hello hello 從 Azure 入口網站位於**Azure Active Directory** > **授權**刀鋒視窗。 這也是 hello 最佳地方 toomanage 授權指派。|
|[Hello Azure 入口網站中的 角色型存取控制](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is)|Azure 角色型存取控制 (RBAC) 可協助提供 Azure 資源的更細緻存取權管理。 太多的權限可以公開 （expose） 和帳戶 tooattackers。 權限太少則會讓員工無法有效率地完成工作。 使用 RBAC，您可以提供給員工 hello 確切所需權限套用 tooall 資源群組的三個基本角色為基礎： 擁有者、 參與者、 讀取器。 您也可以建立 too2，000 您自己的總[RBAC 的自訂角色](https://docs.microsoft.com/azure/active-directory/role-based-access-control-custom-roles)toomeet 您特定需求。 |
|[混合式身分識別](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)|您可以使用 [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)，將內部部署 Windows Server Active Directory (AD DS) 與 Azure AD 整合，來達成混合式身分識別。 這可讓您 tooprovide 通用識別身分的使用者的 Office 365、 Azure 和內部部署應用程式或 SaaS 應用程式與 Azure AD 整合。 使用混合式身分識別，您有效地擴充您內部部署環境 toohello 雲端身分識別和存取。|

### <a name="hello-difference-between-windows-server-ad-ds-and-azure-ad"></a>Windows Server AD DS 與 Azure AD 之間的 hello 差異
Azure Active Directory (Azure AD) 和內部部署 Active Directory (Active Directory Domain Services 或 AD DS) 是儲存目錄資料及管理使用者與資源間通訊的系統，包括使用者登入程序、驗證和目錄搜尋。

如果您已經熟悉內部部署 Windows Server Active Directory 網域服務 (AD DS)，第一次引進 Windows 2000 Server，則您應該了解 hello 的身分識別服務的基本概念。 不過，它也是 Azure AD 不是只在 hello 雲端中的網域控制站的重要 toounderstand。 則為，需要考慮 toofully 運用雲端式功能的全新的方式與現今的威脅保護您的組織的 Azure 服務 (IDaaS) 形式提供身分識別的全新的方式。 

AD DS 是 Windows Server 上的伺服器角色，這表示它可以部署在實體或虛擬機器上。 它具有以 X.500 為基礎的階層式結構。 它會將 DNS 用於尋找物件 (可與使用 LDAP 互動)，而且主要使用 Kerberos 進行驗證。 Active Directory 可讓組織單位 (Ou) 和群組原則物件 (Gpo) 此外 toojoining 機器 toohello 網域及信任被建立網域之間。

多年來，IT 都是使用 AD DS 來保護其安全性周邊，但現代化、無周邊的企業基於為員工、客戶及合作夥伴提供識別身分需求的支援，而需要新的控制項平面。 Azure AD 就是這個身分識別控制平面。 安全性動作已超越 hello Azure AD 其中保護公司資源和存取透過一個通用識別身分提供給使用者的公司防火牆 toohello 雲端 (內部或 hello 雲端)。 這可讓您的使用者 hello 彈性 toosecurely 存取 hello 應用程式所需 tooget 從幾乎任何裝置完成其工作。 無縫式的風險型資料保護控制項，由機器學習功能和深入了解報告，也會提供資料的安全，IT 需求 tookeep 公司。

Azure AD 是多客戶公用目錄服務，這表示您可以在 Azure AD 中針對雲端伺服器和應用程式 (例如 Office 365) 建立租用戶。 使用者和群組會建立於單層式結構中 (不含 OU 或 GPO)。 驗證會透過通訊協定 (如 SAML、WS-同盟和 OAuth) 執行。 可能 tooquery Azure AD 中，但不使用 LDAP 中，您必須使用 REST API 呼叫 AD Graph API。 這些全都透過 HTTP 和 HTTPS 進行。

### <a name="extend-office-365-management-and-security-capabilities"></a>擴充 Office 365 管理與安全性功能
已經在使用 Office 365 了嗎？ 您可以加速您數位的轉換，藉由擴充內建 Office 365 的功能與 Azure AD toosecure 所有的資源，您的整個工作力啟用安全的產能。 當您使用 Azure AD 時，此外 tooOffice 365 功能，您可以保護使用一個啟用單一登入的所有應用程式的身分識別整個應用程式概況。 您不只能以裝置狀態，還能以使用者、位置、應用程式和風險作為基礎，來擴充條件式存取功能。 您在需要時，Multi-Factor Authentication (MFA) 功能提供更多的保護。 您將取得使用者權限的其他監督權，並提供隨選、及時的管理存取。 您的使用者會更具生產力，並建立較少的服務台票證，謝謝 toohello 自助功能 Azure AD 會提供類似重設忘記的密碼，應用程式存取要求，以及建立及管理群組。

> [!TIP]
> 想深入了解 Azure AD 身分識別管理使用 Office 365 toolearn 嗎？ [取得 hello 電子書](https://info.microsoft.com/Extend-Office-365-security-with-EMS.html)。

## <a name="microsoft-azure-identity-solutions"></a>Microsoft Azure 身分識別解決方案

Microsoft Azure 提供數種方式 toomanage 使用者的身分識別是否進行維護完全在內部，僅在 hello 雲端，或甚至地方之間。 這些選項包括︰Azure 中的自己動手做 (DIY) AD DS、Azure Active Directory (Azure AD)、混合式身分識別和 Azure AD Domain Services。

### <a name="do-it-yourself-diy-ad-ds"></a>自己動手做 (DIY) AD DS
對於需要小耗用量 hello 雲端中的公司**自助式 (DIY) AD DS**在 Azure 中可用。 此選項所支援的許多 Windows Server AD DS 案例，非常適合在 Azure 上部署作為虛擬機器 (VM)。 例如，您可以建立 Azure VM 與遠方的資料中心，在連接的 toohello 遠端網路中執行網域控制站。 從該處，hello VM 會無法 toosupport 遠端使用者的驗證要求，改善驗證效能。 此選項也是由裝載少量的網域控制站和單一虛擬網路在 Azure 上的適合用來做為以成本相對低替代 toootherwise 高成本的災害復原站台。 最後，您可能需要 toodeploy Azure 中，例如 SharePoint，需要 Windows Server AD DS，但是並沒有相依性 hello 與內部網路上的應用程式，或 hello 公司 Windows Server Active Directory。 在此情況下，您可以部署在 Azure toomeet hello SharePoint 伺服器陣列的需求上隔離的樹系。 它也有支援 toodeploy 網路應用程式需要連接 toohello 與內部網路和 hello 內部部署 Active Directory。

### <a name="azure-active-directory-azure-ad"></a>Azure Active Directory (Azure AD)
**Azure AD 獨立**是一個完整的雲端式身分識別與存取管理即服務 (IDaaS) 解決方案。 Azure AD 提供一組強固的功能 toomanage 使用者和群組。 它可協助保護存取 tooon 內部部署和雲端應用程式，包括 Microsoft web 服務，例如 Office 365 和許多非 Microsoft 軟體即服務 (SaaS) 應用程式。 Azure AD 共有三種版本：免費版、基本版及進階版。 Azure AD 提升組織效能，並擴充安全性超出 hello 周邊防火牆 tooa 新控制項的平面受到 Azure 機器學習和其他進階的安全性功能。

### <a name="hybrid-identity"></a>混合式身分識別
而不是在內部部署或雲端身分識別解決方案之間的選擇，許多轉寄思考 Cio 和企業開始預計公司的長期方向，擴充其內部目錄 toohello 雲端通過**混合式身分識別**解決方案。 混合式身分識別，您取得遍佈全球的身分識別，而且提供安全且更有生產力存取 toohello 應用程式使用者的存取管理解決方案需要 toodo 他們的工作。

> [!TIP]
> 深入了解 toolearn 方式 Cio 有進行 Azure Active Directory 管理中心他們的 IT 策略的一部分下載 hello [CIO 的指南 tooAzure Active Directory](https://aka.ms/AzureADCIOGuide)。

### <a name="azure-ad-domain-services"></a>Azure AD 網域服務
**Azure AD 網域服務**提供雲端式選項 toouse AD DS 輕量型的 Azure VM 組態控制與方式 toomeet 網路應用程式開發和測試內部部署身分識別需求。 Azure AD 網域服務並未包含廣泛 toolift 然後平移您內部部署 AD DS 基礎結構 tooAzure Vm 受 Azure AD 網域服務。 相反地，hello 受管理的網域中的 Azure Vm 應使用的 toosupport hello 開發、 測試以及在內部部署應用程式需要 AD DS 驗證方法 toohello 雲端的移動。

## <a name="common-scenarios-and-recommendations"></a>常見案例和建議

以下是一些常見的身分識別和存取案例的建議，因為 toowhich Azure 身分識別選項可能會針對每個最適合。

|身分識別案例| 建議|
|-----|-----|
|我的組織已進行大量投資在內部部署 Windows Server Active Directory，但是我們希望 tooextend 識別 toohello 雲端。| 最常使用的 hello Azure 身分識別解決方案是[混合式身分識別](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview)。 如果您所做過投資在內部部署 AD DS，您可以輕鬆地擴充識別 toohello 雲端中使用 Azure AD Connect。|
|我企業出生 hello 雲端中，我們沒有投資在內部部署身分識別解決方案。| [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis)是 hello 最好的選擇，適用於僅限雲端的企業，且沒有執行任何內部部署投資。|
|我需要輕量型 Azure VM 組態和控制 toomeet 在內部部署身分識別需求的應用程式開發和測試。|[Azure AD 網域服務](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-overview)是不錯的選擇，如果您需要針對輕量型的 Azure VM 組態控制 toouse AD DS 或需要 toodevelop 或移轉舊版、 目錄感知的內部部署應用程式 toohello 雲端。|  
|我需要 toosupport 少量的虛擬機器，在 Azure 中，但我的公司仍大量投資在內部部署 Active Directory (AD DS) 中。|使用[DIY AD DS](https://msdn.microsoft.com/library/azure/jj156090.aspx) toouse 時您需要 toosupport 少量的虛擬機器，且有大型 AD DS 投資在內部部署的 Azure Vm。 |

## <a name="where-can-i-learn-more"></a>哪裡可以深入了解？
我們有大量的絕佳的資源線上 toohelp 您深入了解 Azure AD。 以下是一份絕佳文件 tooget 啟動：

* [使用 Azure AD Connect 啟用目錄的混合式管理](active-directory-aadconnect.md)
* [為連線過的項目提供額外的安全性](../multi-factor-authentication/multi-factor-authentication.md)
* [自動化使用者佈建和取消佈建 tooSaaS 與 Azure Active Directory 的應用程式](active-directory-saas-app-provisioning.md)
* [開始使用 Azure AD 報告](active-directory-reporting-getting-started.md)
* [從任何地方管理您的密碼](active-directory-passwords.md)
* [什麼是搭配 Azure Active Directory 的應用程式存取和單一登入？](active-directory-appssoaccess-whatis.md)
* [自動化使用者佈建和取消佈建 tooSaaS 與 Azure Active Directory 的應用程式](active-directory-saas-app-provisioning.md)
* [如何 tooprovide 安全的遠端存取 tooon 內部部署應用程式](active-directory-application-proxy-get-started.md)
* [使用 Azure Active Directory 群組來管理存取 tooresources](active-directory-manage-groups.md)
* [什麼是 Microsoft Azure Active Directory 授權？](active-directory-licensing-what-is.md)
* [如何探索組織內使用未經批准的雲端應用程式](active-directory-cloudappdiscovery-whatis.md)

## <a name="next-steps"></a>後續步驟

既然您了解 Azure 身分識別的概念和 hello 選項可用 tooyou，您可以使用下列資源 tooget 啟動實作 hello 選項您選擇的 hello:

[深入了解 Azure 混合式身分識別解決方案](https://docs.microsoft.com/azure/active-directory/choose-hybrid-identity-solution)

[深入了解 Azure 概念證明環境中的其他資訊](https://aka.ms/aad-poc)

[在生產環境中部署 Azure AD](https://aka.ms/aad-onboard)
