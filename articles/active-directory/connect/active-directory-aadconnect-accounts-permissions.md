---
title: "Azure AD Connect：帳戶與權限 | Microsoft 文件"
description: "本主題描述 hello 帳戶使用並建立與所需的權限。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.reviewer: cychua
ms.assetid: b93e595b-354a-479d-85ec-a95553dd9cc2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: billmath
ms.openlocfilehash: 70a7013e0353d74714ec8a3ff54b3e811789a0b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-accounts-and-permissions"></a>Azure AD Connect：帳戶與權限
hello Azure AD Connect 的安裝精靈提供兩個不同的路徑：

* 快速設定，在 hello 精靈需要更多權限。  這是讓它可以輕鬆地設定您的組態而不需要您 toocreate 使用者或設定權限。
* 在自訂設定 hello 精靈提供您更多的選擇及選項。 不過，有某些情況下，您需要 tooensure 您擁有 hello 正確權限自己。

## <a name="related-documentation"></a>相關文件
如果您沒有讀取 hello 文件上[整合內部部署身分識別與 Azure Active Directory](../active-directory-aadconnect.md)，hello 下表提供連結 toorelated 主題。

|主題 |連結|  
| --- | --- |
|下載 Azure AD Connect | [下載 Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)|
|使用快速設定進行安裝 | [快速安裝 Azure AD Connect](./active-directory-aadconnect-get-started-express.md)|
|使用自訂設定進行安裝 | [自訂 Azure AD Connect 安裝](./active-directory-aadconnect-get-started-custom.md)|
|從 DirSync 升級 | [從 Azure AD 同步作業工具 (DirSync) 升級](./active-directory-aadconnect-dirsync-upgrade-get-started.md)|
|安裝後 | [確認 hello 安裝並指派授權](active-directory-aadconnect-whats-next.md)|

## <a name="express-settings-installation"></a>快速設定安裝
在 Express 設定 hello 安裝精靈會要求 AD DS Enterprise Admin 認證。  以便設定您的內部部署 Active Directory，使其具備必要的 Azure AD Connect 權限。 如果您從 DirSync 升級，hello AD DS Enterprise Admins 認證是使用的 tooreset hello DirSync 所使用的 hello 帳戶密碼。 您也需要 Azure AD 全域管理員認證。

| 精靈頁面 | 收集的認證 | 所需的權限 | 用於 |
| --- | --- | --- | --- |
| N/A |使用者執行 hello 安裝精靈 |Hello 本機伺服器的系統管理員 |<li>建立 hello 本機帳戶做為 hello[同步處理引擎服務帳戶](#azure-ad-connect-sync-service-account)。 |
| 連接 tooAzure AD |Azure AD 目錄認證 |Azure AD 中的全域管理員角色 |<li>正在啟用 hello Azure AD 目錄中的同步處理。</li>  <li>建立 hello [Azure AD 帳戶](#azure-ad-service-account)正進行同步處理作業在 Azure AD 中。</li> |
| 連接 tooAD DS |內部部署 Active Directory 認證 |在 Active Directory 中的 hello Enterprise Admins (EA) 群組的成員 |<li>建立[帳戶](#active-directory-account)Active Directory 和授與權限 tooit 中。 建立帳戶這是使用的 tooread 和寫入目錄資訊同步處理期間。</li> |

### <a name="enterprise-admin-credentials"></a>企業管理員認證
這些認證僅用於 hello 安裝期間，且未用 hello 當安裝完成之後。 hello 企業系統管理員，hello 網域系統管理員應該要確定可以在所有網域中設定 Active Directory 中的 hello 權限。

### <a name="global-admin-credentials"></a>全域管理員認證
這些認證僅用於 hello 安裝期間，且未用 hello 當安裝完成之後。 它是使用的 toocreate hello [Azure AD 帳戶](#azure-ad-service-account)用於同步處理變更 tooAzure AD。 hello 帳戶也會啟用為功能同步處理 Azure AD 中。

### <a name="permissions-for-hello-created-ad-ds-account-for-express-settings"></a>Hello 的權限建立快速設定的 AD DS 帳戶
hello[帳戶](#active-directory-account)建立用於讀取和寫入 tooAD DS 有下列權限時快速設定所建立的 hello:

| 權限 | 用於 |
| --- | --- |
| <li>複寫目錄變更</li><li>複寫目錄變更 (全部) |密碼同步處理 |
| 讀取/寫入所有屬性 (使用者) |匯入和 Exchange 混合 |
| 讀取/寫入所有屬性 (iNetOrgPerson) |匯入和 Exchange 混合 |
| 讀取/寫入所有屬性 (群組) |匯入和 Exchange 混合 |
| 讀取/寫入所有屬性 (連絡人) |匯入和 Exchange 混合 |
| 重設密碼 |啟用密碼回寫的準備工作 |

## <a name="custom-settings-installation"></a>自訂設定安裝
Azure AD Connect 1.1.524.0 版和更新版本已 hello 選項 toolet hello Azure AD Connect 精靈建立 hello 使用帳戶 tooconnect tooActive 目錄。  舊版需要 hello 安裝之前建立的 hello 帳戶。 hello 權限，您必須授與此帳戶可以位於[建立 hello AD DS 帳戶](#create-the-ad-ds-account)。 

| 精靈頁面 | 收集的認證 | 所需的權限 | 用於 |
| --- | --- | --- | --- |
| N/A |使用者執行 hello 安裝精靈 |<li>Hello 本機伺服器的系統管理員</li><li>如果使用完整的 SQL Server，hello 使用者必須是系統管理員 (SA) 中 SQL</li> |根據預設，會建立 hello 本機帳戶做為 hello[同步處理引擎服務帳戶](#azure-ad-connect-sync-service-account)。 hello 管理員未指定特定的帳戶時，才會建立 hello 帳戶。 |
| 安裝同步處理服務，服務帳戶選項 |AD 或本機使用者帳戶認證 |使用者的權限授與 hello 安裝精靈 |如果 hello 系統管理員指定的帳戶，此帳戶用於 hello 服務帳戶為 hello 同步服務。 |
| 連接 tooAzure AD |Azure AD 目錄認證 |Azure AD 中的全域管理員角色 |<li>正在啟用 hello Azure AD 目錄中的同步處理。</li>  <li>建立 hello [Azure AD 帳戶](#azure-ad-service-account)正進行同步處理作業在 Azure AD 中。</li> |
| 連接您的目錄 |每個樹系的連線的 tooAzure AD 內部部署 Active Directory 認證 |hello 權限而定，哪些功能啟用，並位於[建立 hello AD DS 帳戶](#create-the-ad-ds-account) |此帳戶是使用 tooread 和寫入目錄資訊同步處理期間。 |
| AD FS 伺服器 |每個伺服器 hello 清單中，hello 精靈會收集認證執行 hello 精靈 hello 使用者 hello 登入認證不足 tooconnect 時 |網域系統管理員 |安裝與 hello AD FS 伺服器角色的設定。 |
| Web 應用程式 Proxy 伺服器 |每個伺服器 hello 清單中，hello 精靈會收集認證執行 hello 精靈 hello 使用者 hello 登入認證不足 tooconnect 時 |Hello 目標電腦上的本機系統管理員 |安裝和設定 WAP 伺服器角色。 |
| Proxy 信任憑證 |同盟服務的信任憑證 （hello 認證 hello proxy 用於 tooenroll hello FS 從信任的憑證 |Hello AD FS 伺服器的本機系統管理員的網域帳戶 |FS-WAP 信任憑證的首次註冊。 |
| AD FS 服務帳戶頁面，「使用網域使用者帳戶選項」 |AD 使用者帳戶認證 |網域使用者 |hello AD 使用者帳戶所提供的認證當做 hello hello AD FS 服務登入帳戶使用。 |

### <a name="create-hello-ad-ds-account"></a>建立 hello AD DS 帳戶
hello hello 指定的帳戶**連接您的目錄**必須存在於 Active Directory 先前 tooinstallation 頁面。  它也必須擁有所需的 hello 授與的權限。 hello 安裝精靈不會確認同步處理期間才找 hello 權限以及任何問題。

您需要哪些權限取決於 hello 選用功能啟用。 如果您有多個網域，則必須授與 hello 權限 hello 樹系中的所有定義域。 如果您未啟用其中任何功能，hello 預設**網域使用者**具有足夠權限。

| 功能 | 權限 |
| --- | --- |
| msDS-ConsistencyGuid 功能 |Toohello Msds-primary-computer ConsistencyGuid 屬性中記載的寫入權限[設計概念-使用做為 sourceAnchor Msds-primary-computer ConsistencyGuid](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor)。 | 
| 密碼同步處理 |<li>複寫目錄變更</li>  <li>複寫目錄變更 (全部) |
| Exchange 混合式部署 |寫入權限 toohello 屬性記錄於[Exchange 混合式回寫](active-directory-aadconnectsync-attributes-synchronized.md#exchange-hybrid-writeback)使用者、 群組和連絡人。 |
| Exchange 郵件公用資料夾 |讀取權限 toohello 屬性記錄於[Exchange 郵件公用資料夾](active-directory-aadconnectsync-attributes-synchronized.md#exchange-mail-public-folder)公用資料夾。 | 
| 密碼回寫 |寫入權限 toohello 屬性記錄於[開始使用密碼管理](../active-directory-passwords-writeback.md)的使用者。 |
| 裝置回寫 |[裝置回寫](active-directory-aadconnect-feature-device-writeback.md)中所述的使用 PowerShell 指令碼授與權限。 |
| 群組回寫 |讀取、建立、更新和刪除已同步處理之 **Office 365 群組**的群組物件。  如需詳細資訊，請參閱[群組回寫](active-directory-aadconnect-feature-preview.md#group-writeback)。|

## <a name="upgrade"></a>升級
當您從一個版本的 Azure AD Connect tooa 新版本升級時，您需要下列權限的 hello:

| 主體 | 所需的權限 | 用於 |
| --- | --- | --- |
| 使用者執行 hello 安裝精靈 |Hello 本機伺服器的系統管理員 |更新二進位檔案。 |
| 使用者執行 hello 安裝精靈 |ADSyncAdmins 的成員 |變更 tooSync 規則和其他設定。 |
| 使用者執行 hello 安裝精靈 |如果您使用完整的 SQL server: DBO （或類似） 的 hello 同步作業引擎資料庫 |變更資料庫層級，例如更新含有新資料行的資料表。 |

## <a name="more-about-hello-created-accounts"></a>深入了解 hello 建立帳戶
### <a name="active-directory-account"></a>Active Directory 帳戶
如果您使用快速設定，則會在 Active Directory 中建立用於同步處理的帳戶。 建立 hello 帳戶位於 hello 使用者容器中的 hello 樹系根網域，而且有其名稱前面加上**MSOL_**。 hello 帳戶會建立長時間的複雜密碼不會過期。 如果在網域中有密碼原則，請確定允許這個帳戶使用長密碼和複雜密碼。

![AD 帳戶](./media/active-directory-aadconnect-accounts-permissions/adsyncserviceaccount.png)

如果您使用自訂設定，您必須負責 hello 安裝之前先建立 hello 帳戶。

### <a name="azure-ad-connect-sync-service-account"></a>Azure AD Connect 同步處理服務帳戶
hello 同步處理服務可以在不同的帳戶下執行。 它可以在**虛擬服務帳戶** (VSA)、**群組受管理服務帳戶** (gMSA/sMSA) 或一般使用者帳戶下執行。 支援的 hello 選項以 hello 2017 年 4 月發行的連接時變更執行全新安裝。 如果您從舊版的 Azure AD Connect 升級，將無法使用這些額外選項。

| 帳戶類型 | 安裝選項 | 說明 |
| --- | --- | --- |
| [虛擬服務帳戶](#virtual-service-account) | 快速和自訂，2017 年 4 月和更新版本 | 這是所有的快速安裝，除了網域控制站上安裝所使用的 hello 選項。 自訂，它是 hello 預設選項，除非使用了另一個選項。 |
| [群組受管理服務帳戶](#group-managed-service-account) | 自訂，2017 年 4 月和更新版本 | 如果您使用遠端 SQL server，則我們建議 toouse 群組受管理的服務帳戶。 |
| [使用者帳戶](#user-account) | 快速和自訂，2017 年 4 月和更新版本 | 只有在 Windows Server 2008 和網域控制站上安裝時，才會在安裝期間建立前面加上 AAD_ 的使用者帳戶。 |
| [使用者帳戶](#user-account) | 快速和自訂，2017 年 3 月和更早版本 | 在安裝期間，系統會建立本機帳戶，並於帳戶前面加上 AAD_。 而在使用自訂安裝時，您則可以指定另一個帳戶。 |

如果連接使用來自 2017 年 3 月或更早版本，則您應該密碼重設 hello hello 服務帳戶因為 Windows 終結 hello 加密金鑰基於安全性考量。 您無法變更 hello 帳戶 tooany 其他帳戶，但不重新安裝 Azure AD Connect。 如果您從 tooa 組建 2017 年 4 月或更新版本中，然後是支援的 toochange hello hello 服務帳戶的密碼但無法變更使用 hello 帳戶。

> [!Important]
> 您只能在第一次安裝上設定 hello 服務帳戶。 它不是 hello 安裝完成之後，支援 toochange hello 服務帳戶。

這是資料表 hello 預設的建議，並將支援的選項，如 hello 同步服務帳戶。

圖例：

- **粗體**表示 hello 預設選項，在大部分情況下 hello 建議的選項。
- *斜體*指出 hello 建議選項時，就會 hello 預設選項。
- 2008 - 安裝在 Windows Server 2008 時的預設選項
- 非粗體 - 支援選項
- Hello 伺服器上的本機帳戶-本機使用者帳戶
- 網域帳戶 - 網域使用者帳戶
- sMSA - [獨立受管理服務帳戶](https://technet.microsoft.com/library/dd548356.aspx)
- gMSA - [群組受管理服務帳戶](https://technet.microsoft.com/library/hh831782.aspx)

| | LocalDB</br>Express | LocalDB/LocalSQL</br>自訂 | 遠端 SQL</br>自訂 |
| --- | --- | --- | --- |
| **獨立/工作群組電腦** | 不支援 | **VSA**</br>本機帳戶 (2008)</br>本機帳戶 |  不支援 |
| **已加入網域的電腦** | **VSA**</br>本機帳戶 (2008) | **VSA**</br>本機帳戶 (2008)</br>本機帳戶</br>網域帳戶</br>sMSA、gMSA | **gMSA**</br>網域帳戶 |
| **網域控制站** | **網域帳戶** | *gMSA*</br>**網域帳戶**</br>sMSA| *gMSA*</br>**網域帳戶**|

#### <a name="virtual-service-account"></a>虛擬服務帳戶
虛擬服務帳戶是特殊的帳戶類型，這種帳戶沒有密碼，並且是由 Windows 進行管理。

![VSA](./media/active-directory-aadconnect-accounts-permissions/aadsyncvsa.png)

hello VSA 是預定的 toobe 其中 hello 同步處理引擎和 SQL 位於 hello 搭配案例使用相同的伺服器。 如果您使用遠端 SQL，則我們建議 toouse[群組受管理的服務帳戶](#managed-service-account)改為。

這項功能需要 Windows Server 2008 R2 或更新版本。 如果您在 Windows Server 2008 上安裝 Azure AD Connect，則會回復到 hello 安裝 toousing[使用者帳戶](#user-account)改為。

#### <a name="group-managed-service-account"></a>群組受管理服務帳戶
如果您使用遠端 SQL server，則我們建議 toousing**群組受管理的服務帳戶**。 如需有關如何 tooprepare 您的 Active Directory 群組受管理的服務帳戶，請參閱[群組受管理服務帳戶概觀](https://technet.microsoft.com/library/hh831782.aspx)。

選取此選項，在 hello toouse[安裝必要的元件](active-directory-aadconnect-get-started-custom.md#install-required-components)頁面上，選取**使用現有的服務帳戶**，然後選取**受管理的服務帳戶**。  
![VSA](./media/active-directory-aadconnect-accounts-permissions/serviceaccount.png)  
它也是支援的 toouse[獨立受管理的服務帳戶](https://technet.microsoft.com/library/dd548356.aspx)。 不過，僅可使用 hello 本機電腦上，而且沒有任何好處 toouse 它們透過 hello 預設虛擬服務帳戶。

這項功能需要 Windows Server 2012 或更新版本。 如果您需要 toouse 較舊的作業系統，並使用遠端 SQL，則您必須使用[使用者帳戶](#user-account)。

#### <a name="user-account"></a>使用者帳戶
（除非您自訂的設定中指定 hello 帳戶 toouse） hello 安裝精靈會建立本機服務帳戶。 hello 帳戶做為前置詞**AAD_** ，用於為 hello 實際的同步處理服務 toorun。 如果您在網域控制站上安裝 Azure AD Connect，hello 帳戶會建立 hello 網域中。 hello **AAD_**服務帳戶必須位於 hello 網域中，如果：
   - 您使用執行 SQL Server 的遠端伺服器
   - 您使用需要驗證的 Proxy

![同步服務帳戶](./media/active-directory-aadconnect-accounts-permissions/syncserviceaccount.png)

hello 帳戶會建立長時間的複雜密碼不會過期。

此帳戶是安全的方式使用的 toostore hello 密碼 hello 其他帳戶。 這些帳戶密碼會儲存在 hello 資料庫中加密。 hello hello 加密金鑰的私用金鑰受到與 hello 密碼編譯服務的秘密金鑰加密使用 Windows 資料保護 API (DPAPI)。

如果您使用 SQL Server 完整版，hello 服務帳戶是 hello hello 同步處理引擎的 hello 建立資料庫的 DBO。 hello 服務將無法如預期般與任何其他權限。 也會建立 SQL 登入。

hello 帳戶也具備權限 toofiles、 登錄機碼和其他物件相關的 toohello 同步處理引擎。

### <a name="azure-ad-service-account"></a>Azure AD 服務帳戶
在 Azure AD 的帳戶會建立 hello 同步處理服務的使用。 此帳戶可以由其顯示名稱來識別。

![AD 帳戶](./media/active-directory-aadconnect-accounts-permissions/aadsyncserviceaccount.png)

hello hello 伺服器 hello 帳戶的名稱會在識別 hello hello 使用者名稱的第二個部分。 Hello 圖片中的 hello 伺服器名稱會是 FABRIKAMCON。 如果您有預備伺服器，則每個伺服器會有自己的帳戶。

建立 hello 服務帳戶不會過期的長時間的複雜密碼。 它會授與特殊角色**目錄同步處理帳戶**具有僅限 tooperform 目錄同步處理工作。 這個特殊的內建角色無法授與外部 hello Azure AD Connect 精靈。 hello Azure 入口網站會顯示 hello 角色與此帳戶**使用者**。

Azure AD 中有 20 個同步服務帳戶的限制。 現有 Azure AD 服務帳戶在 Azure AD 中，執行下列 Azure AD PowerShell cmdlet 的 hello tooget hello 清單：`Get-AzureADDirectoryRole | where {$_.DisplayName -eq "Directory Synchronization Accounts"} | Get-AzureADDirectoryRoleMember`

tooremove 未使用 Azure AD 服務帳戶，執行下列 Azure AD PowerShell cmdlet 的 hello:`Remove-AzureADUser -ObjectId <ObjectId-of-the-account-you-wish-to-remove>`

## <a name="next-steps"></a>後續步驟
深入了解 [整合內部部署身分識別與 Azure Active Directory](../active-directory-aadconnect.md)。
