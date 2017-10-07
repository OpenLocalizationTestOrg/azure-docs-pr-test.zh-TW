---
title: "Azure AD Connect：自訂安裝 | Microsoft Docs"
description: "本文件詳述 hello Azure AD Connect 自訂安裝選項。 使用這些指示 tooinstall 透過 Azure AD Connect 的 Active Directory。"
services: active-directory
keywords: "何謂 Azure AD Connect、安裝 Active Directory、Azure AD 的必要元件"
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 6d42fb79-d9cf-48da-8445-f482c4c536af
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: c49724fab78c5a1688662043f69506fff6f82104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="custom-installation-of-azure-ad-connect"></a>自訂 Azure AD Connect 安裝
Azure AD Connect**自訂設定**想 hello 安裝更多的選項時使用。 它用於如果您有多個樹系，或如果您想 tooconfigure 未涵蓋在 hello 快速安裝的選用功能。 它，則會使用在所有情況下 hello [**快速安裝**](active-directory-aadconnect-get-started-express.md)選項不符合您的部署或拓撲。

您開始安裝 Azure AD Connect，請確定太[下載 Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)和中的步驟完成 hello 必要條件[Azure AD Connect： 硬體和必要條件](active-directory-aadconnect-prerequisites.md)。 另外，也請確定您具有 [Azure AD Connect 帳戶與權限](active-directory-aadconnect-accounts-permissions.md)中所述的必要帳戶。

如果自訂的設定不符合您的拓撲，例如 tooupgrade DirSync，請參閱[相關文件](#related-documentation)其他案例。

## <a name="custom-settings-installation-of-azure-ad-connect"></a>Azure AD Connect 的自訂設定安裝
### <a name="express-settings"></a>快速設定
這個頁面上，按一下 **自訂**toostart 自訂的設定安裝。

### <a name="install-required-components"></a>安裝必要的元件
當您安裝 hello 同步處理服務時，您可以讓 hello 選擇性的組態區段未核取和 Azure AD Connect 設定的所有項目自動。 它會設定 SQL Server 2012 Express LocalDB 執行個體、 建立 hello 適當的群組，並指派權限。 如果您想 toochange hello 預設值，您可以使用下列資料表 toounderstand hello 選擇性組態選項所提供的 hello。

![必要的元件](./media/active-directory-aadconnect-get-started-custom/requiredcomponents.png)

| 選用組態 | 說明 |
| --- | --- |
| 使用現有的 SQL Server |可讓您 toospecify hello SQL Server 名稱和 hello 執行個體名稱。 如果您已經有您想要 toouse 資料庫伺服器，請選擇此選項。 輸入後面接逗號和通訊埠的數字中的 hello 執行個體名稱**執行個體名稱**如果您的 SQL Server 並沒有啟用瀏覽。 |
| 使用現有的服務帳戶 |預設 Azure AD Connect 的 hello 同步處理服務 toouse 使用虛擬服務帳戶。 如果您使用遠端 SQL server，或使用 proxy 需要驗證，您需要 toouse**受管理的服務帳戶**或使用 hello 網域中的服務帳戶，並了解 hello 密碼。 在這些情況下，輸入 hello 帳戶 toouse。 請確定執行 hello 安裝的 hello 使用者是 SA 在 SQL 中的，因此可以建立 hello 服務帳戶的登入。 請參閱 [Azure AD Connect 帳戶與權限](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account) |
| 指定自訂同步群組 |依預設 Azure AD Connect hello 同步處理服務安裝時建立四個 toohello 本機伺服器群組。 這些群組是： 系統管理員群組、 Operators 群組、 瀏覽群組和 hello 密碼重設的群組。 您可以在此指定自己的群組。 hello 群組必須是 hello 伺服器上的本機，而且不能位於 hello 網域。 |

### <a name="user-sign-in"></a>使用者登入
安裝所需的 hello 元件，系統會要求您 tooselect 之後，您的使用者單一登入方法。 下表中的 hello 提供 hello 可用之選項的簡短描述。 Hello 登入方法的完整描述，請參閱[使用者登入](active-directory-aadconnect-user-signin.md)。

![使用者登入](./media/active-directory-aadconnect-get-started-custom/usersignin2.png)

| 單一登入選項 | 說明 |
| --- | --- |
| 密碼同步處理 |使用者會無法 toosign tooMicrosoft 雲端服務，例如 Office 365 中使用 hello 他們在其內部部署網路中使用的相同密碼。 hello 使用者密碼會同步處理的 tooAzure AD 為密碼雜湊和 hello 雲端中進行驗證。 詳細資訊請參閱[密碼同步處理](active-directory-aadconnectsync-implement-password-synchronization.md)。 |
|傳遞驗證 (預覽)|使用者會無法 toosign tooMicrosoft 雲端服務，例如 Office 365 中使用 hello 他們在其內部部署網路中使用的相同密碼。  hello 使用者密碼在經由 toohello 在內部部署 Active Directory 控制站 toobe 驗證。
| 與 AD FS 同盟 |使用者會無法 toosign tooMicrosoft 雲端服務，例如 Office 365 中使用 hello 他們在其內部部署網路中使用的相同密碼。  hello 使用者重新導向 tootheir 內部部署 AD FS 中的執行個體 toosign 和驗證，就會發生在內部部署。 |
| 請勿設定 |不會安裝和設定任何功能。 如果您已經有第三方的同盟伺服器或另一個現有的適當方案，請選擇此選項。 |
|啟用單一登入|此選項適用於密碼同步處理和傳遞驗證，並提供單一登經驗 hello 公司網路上的桌面使用者。  如需詳細資訊，請參閱[單一登入](active-directory-aadconnect-sso.md)。 </br>附註的 AD FS 客戶此選項沒有因為 AD FS 已經提供 hello 相同層級的單一登入。</br>(如果 PTA 不在 hello 釋出相同的時間)
|登入選項|此選項適用於密碼同步處理的客戶，並提供單一登經驗 hello 公司網路上的桌面使用者。  </br>如需詳細資訊，請參閱[單一登入](active-directory-aadconnect-sso.md)。 </br>附註的 AD FS 客戶此選項沒有因為 AD FS 已經提供 hello 相同層級的單一登入。


### <a name="connect-tooazure-ad"></a>連接 tooAzure AD
Hello 連接 tooAzure AD 在畫面上，輸入全域系統管理員帳戶和密碼。 如果您選取**與 AD FS 同盟**hello 上一頁未登入用的帳戶網域中您計劃 tooenable 同盟。 建議的做法是在 hello 預設帳戶 toouse **onmicrosoft.com**隨附於 Azure AD 目錄的網域。

此帳戶是只使用的 toocreate 在 Azure AD 中的服務帳戶，而且不是 hello 精靈完成後。  
![使用者登入](./media/active-directory-aadconnect-get-started-custom/connectaad.png)

如果您的全域管理員帳戶啟用 MFA，您需要 tooprovide hello 密碼再次登入快顯視窗的 hello 和完整 hello MFA 挑戰。 hello 挑戰，可能是提供驗證碼或電話。  
![使用者登入 MFA](./media/active-directory-aadconnect-get-started-custom/connectaadmfa.png)

hello 全域管理員帳戶也可以有[Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md)啟用。

如果您收到錯誤訊息，而且有連線問題，請參閱[針對連線問題進行疑難排解](active-directory-aadconnect-troubleshoot-connectivity.md)。

## <a name="pages-under-hello-section-sync"></a>Hello 下的頁面區段的同步處理

### <a name="connect-your-directories"></a>連接您的目錄
tooconnect tooyour Active Directory 網域服務，Azure AD Connect 需要 hello 樹系名稱以及有足夠的權限的帳戶認證。

![連線目錄](./media/active-directory-aadconnect-get-started-custom/connectdir01.png)

之後輸入 hello 樹系名稱並按一下**新增目錄**，快顯對話方塊出現，並提示您以 hello 下列選項：

| 選項 | 說明 |
| --- | --- |
| 使用現有帳戶 | 如果您希望 tooprovide 現有的 AD DS 帳戶 toobe 可用於 Azure AD Connect 目錄同步處理期間連接 toohello AD 樹系，請選取此選項。 您可以輸入 NetBios 或 FQDN 格式，也就是 FABRIKAM\syncuser 或 fabrikam.com\syncuser hello 網域 」 部分。 此帳戶可以是一般使用者帳戶，因為它只需要 hello 預設讀取權限。 不過，視您的情況而定，也可能需要更多權限。 如需詳細資訊，請參閱 [Azure AD Connect 帳戶與權限](active-directory-aadconnect-accounts-permissions.md#create-the-ad-ds-account)。 |
| 建立新帳戶 | 如果您要讓 Azure AD Connect 精靈 toocreate hello AD DS 帳戶所需的 Azure AD Connect 目錄同步處理期間連接 toohello AD 樹系，請選取此選項。 選取此選項時，輸入 hello 使用者名稱和密碼的企業系統管理員帳戶。 hello 提供企業系統管理員帳戶將用於 Azure AD connect 精靈 toocreate hello 需要 AD DS 帳戶。 您可以輸入 NetBios 或 FQDN 格式，也就是 FABRIKAM\administrator 或 fabrikam.com\administrator hello 網域 」 部分。 |

![連線目錄](./media/active-directory-aadconnect-get-started-custom/connectdir02.png)


### <a name="azure-ad-sign-in-configuration"></a>Azure AD 登入組態
此頁面可讓您 tooreview hello UPN 網域已存在於內部部署 AD DS，以及哪些驗證 Azure AD 中。 此頁面也可讓您針對 hello userPrincipalName tooconfigure hello 屬性 toouse。

![未驗證的網域](./media/active-directory-aadconnect-get-started-custom/aadsigninconfig.png)  
檢閱每一個標示為**未新增**和**未驗證**的網域。 確定您所使用的網域皆已在 Azure AD 中完成驗證。 當您已確認您的網域，請按一下 hello 重新整理符號。 如需詳細資訊，請參閱[新增並驗證 hello 網域](../active-directory-add-domain.md)

**UserPrincipalName** -hello 屬性 userPrincipalName 是 hello 屬性使用者使用登入 tooAzure AD 和 Office 365 時。 hello 網域，也稱為 hello UPN 尾碼，就應該同步處理 hello 使用者之前的 Azure AD 中驗證。 Microsoft 建議 tookeep hello 預設屬性 userPrincipalName。 如果這個屬性為非路由傳送，而且無法驗證，則很可能 tooselect 另一個屬性。 例如選取電子郵件作為 hello 屬性保留 hello 登入識別碼。 使用 userPrincipalName 之外的其他屬性稱為 **替代 ID**。 hello 替代 ID 屬性值必須遵循 hello RFC822 標準。 替代 ID 可以搭配密碼同步和同盟來使用。

>[!NOTE]
> 當您啟用通過驗證，您必須擁有順序 toocontinue 透過 hello 精靈中的至少一個已驗證的網域。

> [!WARNING]
> 使用替代 ID 會與所有 Office 365 工作負載不相容。 如需詳細資訊，請參閱太[設定替代的登入識別碼](https://technet.microsoft.com/library/dn659436.aspx)。
>
>

### <a name="domain-and-ou-filtering"></a>網域和 OU 篩選
預設會同步所有網域和 OU。 如果有部分的網域或 Ou，您不想 toosynchronize tooAzure AD，您可以取消選取這些網域和 Ou。  
![DomainOU 篩選](./media/active-directory-aadconnect-get-started-custom/domainoufiltering.png)  
Hello 精靈中的這個頁面會設定網域和 OU 篩選。 如果您計劃 toomake 變更，然後查看[網域型篩選](active-directory-aadconnectsync-configure-filtering.md#domain-based-filtering)和[組織單位型篩選](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering)進行這些變更之前。 一些 Ou，是不可或缺的 hello 功能，而且不應該為未選取。

如果您使用 OU 型篩選搭配 1.1.524.0 版之前的 Azure AD Connect，預設會同步處理稍後新增的 OU。 如果您想要 hello 行為，新 Ou 應該不會同步處理，則之後，您可以設定它 hello 精靈已完成且[組織單位型篩選](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering)。 Azure AD Connect 版 1.1.524.0 或之後，您可以指出是否要讓新的 Ou toobe 或不進行同步處理。

如果您計劃 toouse[群組為基礎的篩選](#sync-filtering-based-on-groups)，然後確定 hello OU 與 hello 群組是包含與未篩選的 OU 篩選。 OU 篩選會在群組型篩選之前評估。

此外，也可以部分網域未到期 toofirewall 限制可以連線。 依預設不會選取這些網域，而且會有警告。  
![無法連線到網域](./media/active-directory-aadconnect-get-started-custom/unreachable.png)  
如果您看到這個警告，請確定這些網域會確實無法連線，而且預期會 hello 警告。

### <a name="uniquely-identifying-your-users"></a>唯一識別您的使用者

#### <a name="select-how-users-should-be-identified-in-your-on-premises-directories"></a>選取在內部部署目錄中要如何識別使用者
hello 跨樹系功能可讓您將 AD DS 樹系使用者在 Azure AD 中的呈現方式 toodefine 比對。 使用者可能會在整個樹系中只顯示一次，或是具有啟用和停用帳戶的組合。 hello 使用者也可能表示某些樹系中的連絡人。

![唯一](./media/active-directory-aadconnect-get-started-custom/unique.png)

| 設定 | 說明 |
| --- | --- |
| [使用者在所有樹系中只會顯示一次](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |在 Azure AD 中，所有使用者會都建立為個別物件。 hello 物件不在 hello metaverse 中聯結。 |
| [郵件屬性](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |如果 hello mail 屬性具有相同的值不同的樹系中的 hello，此選項會聯結使用者和連絡人。 如果已透過 GALSync 建立了您的連絡人，請使用此選項。 如果選擇此選項，則使用者的 Mail 屬性並不填入的物件不會同步處理的 tooAzure AD。 |
| [ObjectSID 與 msExchangeMasterAccountSID/ msRTCSIP-OriginatorSid](active-directory-aadconnect-topologies.md#multiple-forests-single-azure-ad-tenant) |此選項會聯結帳戶樹系中已啟用的使用者與資源樹系中已停用的使用者。 在 Exchange 中，此組態稱為連結信箱。 如果您只使用 Lync，而 Exchange 不存在於 hello 資源樹系中，也可以使用此選項。 |
| sAMAccountName 與 MailNickName |此選項會聯結屬性就是可以找到 hello 使用者預期的 hello 登入識別碼。 |
| 特定的屬性 |此選項可讓您 tooselect 您自己的屬性。 如果選擇此選項，則其 （選取） 的屬性並不填入使用者物件不會同步處理的 tooAzure AD。 **限制：**做確定 toopick 已經可以找到 hello metaverse 中的屬性。 如果您挑選自訂屬性 （不在 hello metaverse)，hello 精靈無法完成。 |

#### <a name="select-how-users-should-be-identified-with-azure-ad---source-anchor"></a>選取要如何使用 Azure AD 識別使用者 - 來源錨點
hello 屬性 sourceAnchor 為 hello 使用者物件存留期間是不可變的屬性。 它是連結 hello 在內部部署使用者與 hello 使用者在 Azure AD 中的 hello 主索引鍵。

| 設定 | 說明 |
| --- | --- |
| 可讓 Azure 能管理我的 hello 來源錨點 | 如果您要為您的 Azure AD toopick hello 屬性，請選取此選項。 如果您選取此選項時，Azure AD Connect 精靈適用於文件一節所述的 hello sourceAnchor 屬性選取邏輯[Azure AD Connect： 設計概念-使用做為 sourceAnchor Msds-primary-computer ConsistencyGuid](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor)。 hello 精靈會通知您哪一個屬性具有已挑選 hello 來源錨點屬性為自訂安裝完成之後。 |
| 特定的屬性 | 如果您想 toospecify hello sourceAnchor 屬性的現有 AD 屬性，請選取此選項。 |

因為無法變更 hello 屬性，所以您必須規劃好屬性 toouse。 objectGUID 就是不錯的選項。 這個屬性不會變更，除非樹系/網域之間移動 hello 使用者帳戶。 在多樹系環境中您在樹系之間移動帳戶的位置，另一個屬性必須使用，例如 hello employeeid 屬性。 請避免使用會在某人結婚或變更指派時改變的屬性。 因為不可以使用帶有 @-sign 的屬性，所以無法使用 email 和 userPrincipalName。 hello 屬性也是區分大小寫的樹系之間移動物件，因此請確定 toopreserve hello 大寫/小寫。 二進位屬性會以 base64 編碼，但其他屬性類型則會維持未編碼狀態。 在同盟情況以及部分 Azure AD 介面中，此屬性也稱為 immutableID。 可以找到 hello 來源錨點的詳細資訊，在 hello[設計概念](active-directory-aadconnect-design-concepts.md#sourceanchor)。

### <a name="sync-filtering-based-on-groups"></a>根據群組進行同步處理篩選
hello 篩選群組功能可讓您 toosync 物件一小部分的一項試驗。 toouse 這項功能，針對此目的，在內部部署 Active Directory 中建立群組。 然後新增使用者和群組應該同步的 tooAzure AD 做為直接成員。 您可以稍後新增及移除使用者 toothis 群組 toomaintain hello 的清單應該會出現在 Azure AD 中的物件。 您想要 toosynchronize 的所有物件必須都是 hello 群組直接成員。 使用者、群組、連絡人及電腦/裝置全都必須是直接成員。 系統不會解析巢狀群組成員資格。 當您加入群組中加入成員時，只有 hello 群組本身時，不是其成員。

![同步處理篩選](./media/active-directory-aadconnect-get-started-custom/filter2.png)

> [!WARNING]
> 這項功能是預定的 toosupport 試驗部署。 請勿將其用於成熟的生產部署。
>
>

在完全成熟的生產環境部署中，它正在 toobe 硬 toomaintain 所有物件 toosynchronize 的單一群組。 相反地，您應該使用其中一種在 hello 方法[設定篩選](active-directory-aadconnectsync-configure-filtering.md)。

### <a name="optional-features"></a>選用功能
此畫面可讓您針對特定案例的 tooselect hello 選用功能。

![選用功能](./media/active-directory-aadconnect-get-started-custom/optional.png)

> [!WARNING]
> 如果您目前有 DirSync 或 Azure AD Sync 作用中，沒有啟動任何 Azure AD Connect 中的 hello 回寫功能。
>
>

| 選用功能 | 說明 |
| --- | --- |
| Exchange 混合部署 |hello Exchange 混合部署功能，可以共存的 Exchange 信箱能夠 hello 這兩個內部部署和 Office 365 中。 Azure AD Connect 會將一組特定的[屬性](active-directory-aadconnectsync-attributes-synchronized.md#exchange-hybrid-writeback)從 Azure AD 同步處理回內部部署目錄。 |
| Exchange 郵件公用資料夾 | hello Exchange 郵件公用資料夾功能可讓您從您的內部部署 Active Directory tooAzure AD toosynchronize 郵件啟用公用資料夾物件。 |
| Azure AD 應用程式和屬性篩選 |藉由啟用 Azure AD 應用程式和屬性篩選，hello 已同步處理的屬性集的可調整。 此選項會新增兩個多個組態頁面 toohello 精靈。 如需詳細資訊，請參閱 [Azure AD 應用程式和屬性篩選](#azure-ad-app-and-attribute-filtering)。 |
| 密碼同步處理 |如果您選取做為 hello 登入解決方案的同盟，您可以啟用此選項。 密碼同步處理可做為備份選項。 如需其他資訊，請參閱[密碼同步處理](active-directory-aadconnectsync-implement-password-synchronization.md)。 </br></br>如果您選取的傳遞驗證預設 tooensure 支援舊版用戶端和做為備份的選項會啟用此選項。 如需其他資訊，請參閱[密碼同步處理](active-directory-aadconnectsync-implement-password-synchronization.md)。|
| 密碼回寫 |啟用密碼回寫，源自 Azure AD 中的密碼變更寫回 tooyour 在內部部署目錄。 如需詳細資訊，請參閱[開始使用密碼管理](../active-directory-passwords-getting-started.md)。 |
| 群組回寫 |如果您使用 hello **Office 365 群組**功能，則您可以在內部部署 Active Directory 中表示這些群組。 只有當您內部部署的 Active Directory 中已經有 Exchange 時，才能使用此選項。 如需詳細資訊，請參閱[群組回寫](active-directory-aadconnect-feature-preview.md#group-writeback)。 |
| 裝置回寫 |在 Azure AD tooyour 內部部署條件式存取案例的 Active Directory，讓您 toowriteback 裝置物件。 如需詳細資訊，請參閱[在 Azure AD Connect 中啟用裝置回寫](active-directory-aadconnect-feature-device-writeback.md)。 |
| 目錄擴充屬性同步處理 |透過啟用目錄擴充屬性同步處理，會同步處理的 tooAzure AD 屬性指定。 如需詳細資訊，請參閱[目錄擴充](active-directory-aadconnectsync-feature-directory-extensions.md)。 |

### <a name="azure-ad-app-and-attribute-filtering"></a>Azure AD 應用程式和屬性篩選
如果您想的 toolimit 哪些屬性 toosynchronize tooAzure AD，首先請選取您要使用哪些服務。 如果您在此頁面上進行設定變更，新的服務有 toobe 來重新執行 hello 安裝精靈明確選取。

![選用功能應用程式](./media/active-directory-aadconnect-get-started-custom/azureadapps2.png)

根據 hello hello 先前步驟中選取的服務，此頁面會顯示已同步處理的所有屬性。 這份清單是正在同步處理的所有物件類型的組合。 如果有某些特定的屬性，您需要 toonot 同步處理，您可以取消選取這些屬性。

![選用功能屬性](./media/active-directory-aadconnect-get-started-custom/azureadattributes2.png)

> [!WARNING]
> 移除可能影響功能的屬性。 如需最佳做法和建議，請參閱[同步處理的屬性](active-directory-aadconnectsync-attributes-synchronized.md#attributes-to-synchronize)。
>
>

### <a name="directory-extension-attribute-sync"></a>目錄擴充屬性同步處理
您可以擴充在 Azure AD 中的 hello 結構描述，以加入您的組織或 Active Directory 中的其他屬性的自訂屬性。 toouse 這項功能，選取**目錄擴充屬性同步**上 hello**選用功能**頁面。 您可以選取多個屬性 toosync 此頁面上。

![目錄擴充](./media/active-directory-aadconnect-get-started-custom/extension2.png)

如需詳細資訊，請參閱[目錄擴充](active-directory-aadconnectsync-feature-directory-extensions.md)。

### <a name="enabling-single-sign-on-sso"></a>啟用單一登入 (SSO)
使用密碼同步處理或傳遞驗證設定單一登入使用的是簡單的程序，您只需要 toocomplete 一次每個樹系正在同步處理的 tooAzure AD。 設定程序包含兩個步驟，如下所示︰

1.  在內部部署 Active Directory 中建立 hello 必要的電腦帳戶。
2.  Hello 內部網路區域 hello toosupport 單一登入的用戶端機器的設定。

#### <a name="create-hello-computer-account-in-active-directory"></a>Active Directory 中建立 hello 電腦帳戶
已加入 Azure AD Connect 中的每個樹系中，您必須 toosupply 網域系統管理員認證，以便 hello 電腦帳戶可以建立每個樹系中。 hello 認證所使用的 toocreate hello 帳戶並不儲存或用於其他任何作業。 只要加入 hello 認證上 hello**啟用單一登入**頁面 hello Azure AD Connect 精靈所示：

![啟用單一登入](./media/active-directory-aadconnect-get-started-custom/enablesso.png)

>[!NOTE]
>如果您不想 toouse 單一登入具有該樹系，您可以略過特定的樹系。

#### <a name="configure-hello-intranet-zone-for-client-machines"></a>設定用戶端電腦的 hello 近端內部網路區域
tooensure hello 用戶端登入會自動在 hello 內部網路區域您需要 tooensure 兩個 Url 是 hello 近端內部網路區域的一部分。 這可確保該加入的 hello 網域之電腦會自動傳送 Kerberos 票證 tooAzure AD 連線的 toohello 公司網路時。
在 hello 群組原則管理工具的電腦。

1.  開啟 [群組原則管理工具] hello
2.  編輯 hello 群組原則將會套用的 tooall 使用者。 例如，hello 預設網域原則。
3.  瀏覽過**使用者設定 \ 系統管理範本 \windows 元件 \internet explorer\ 網際網路控制項 Panel\Security 頁面**選取**站台指派清單 tooZone**每個 hello 影像下面。
4.  啟用 hello 原則，並輸入下列兩個項目 hello 對話方塊中的 hello。

        Value: `https://autologon.microsoftazuread-sso.com`  
        Data: 1  
        Value: `https://aadg.windows.net.nsatc.net`  
        Data: 1

5.  它看起來應該類似 toohello 下列：  
![內部網路區域](./media/active-directory-aadconnect-get-started-custom/sitezone.png)

6.  按兩次 [確定]。

## <a name="configuring-federation-with-ad-fs"></a>設定與 AD FS 同盟
只要簡單按幾下，即可使用 Azure AD Connect 設定 AD FS。 hello 組態之前，需要下列 hello。

* Hello 同盟伺服器啟用遠端管理的 Windows Server 2012 R2 伺服器
* 啟用遠端管理的 hello Web 應用程式 Proxy 伺服器的 Windows Server 2012 R2 伺服器
* 使用 SSL 憑證來進行 hello 同盟服務名稱想 toouse (例如，sts.contoso.com)

### <a name="ad-fs-configuration-pre-requisites"></a>AD FS 組態必要條件
tooconfigure AD FS 伺服器陣列使用 Azure AD Connect，請確定 hello 遠端伺服器上啟用 WinRM。 此外，瀏覽列中的 hello 連接埠需求[資料表 3-Azure AD Connect 與同盟伺服器/WAP](active-directory-aadconnect-ports.md#table-3---azure-ad-connect-and-ad-fs-federation-serverswap)。

### <a name="create-a-new-ad-fs-farm-or-use-an-existing-ad-fs-farm"></a>建立新的 AD FS 伺服器陣列或使用現有的 AD FS 伺服器陣列
您可以使用現有的 AD FS 伺服器陣列，或者您可以選擇 toocreate 新的 AD FS 伺服器陣列。 如果您選擇 toocreate 新，則需要的 tooprovide hello SSL 憑證。 如果 hello SSL 憑證受密碼保護，系統會提示您 hello 密碼。

![AD FS 伺服器陣列](./media/active-directory-aadconnect-get-started-custom/adfs1.png)

如果您選擇 toouse 現有的 AD FS 伺服器陣列時，即會進入直接 toohello 設定 hello AD FS 與 Azure AD 的螢幕之間的信任關係。

### <a name="specify-hello-ad-fs-servers"></a>指定 hello AD FS 伺服器
輸入您想 tooinstall AD FS 的 hello 伺服器。 您可以根據容量規劃需求，加入一或多部伺服器。 加入所有伺服器 tooActive 目錄，才能執行這項設定。 Microsoft 建議安裝一部專門用於測試和試驗部署的 AD FS 伺服器。 然後加入並部署多個伺服器 toomeet 初始設定之後，再次執行 Azure AD Connect 的縮放的需求。

> [!NOTE]
> 請確認您的伺服器加入的 tooan AD 網域之前進行這項設定。
>
>

![AD FS 伺服器](./media/active-directory-aadconnect-get-started-custom/adfs2.png)

### <a name="specify-hello-web-application-proxy-servers"></a>指定 hello Web 應用程式 Proxy 伺服器
輸入您要做為您的 Web 應用程式 proxy 伺服器的 hello 伺服器。 hello web application proxy 伺服器部署在周邊網路 （面對外部網路），並支援從 hello 外部網路驗證要求。 您可以根據容量規劃需求，加入一或多部伺服器。 Microsoft 建議安裝一部專門用於測試和試驗部署的 Web 應用程式 Proxy 伺服器。 然後加入並部署多個伺服器 toomeet 初始設定之後，再次執行 Azure AD Connect 的縮放的需求。 我們建議您使用與 hello 內部網路 proxy 伺服器 toosatisfy 驗證對等數字。

> [!NOTE]
> <li> 如果您使用的 hello 帳戶不在 hello AD FS 伺服器上的本機系統管理員，您會提示系統管理員認證。</li>
> <li> 請確認有 hello Azure AD Connect 的伺服器與 hello Web Application Proxy 伺服器之間的 HTTP/HTTPS 連線之前執行這個步驟。</li>
> <li> 請確認有 Web 應用程式伺服器 hello 與 hello AD FS 伺服器 tooallow 驗證要求 tooflow 透過之間的 HTTP/HTTPS 連線。</li>
>

![Web 應用程式](./media/active-directory-aadconnect-get-started-custom/adfs3.png)

您是提示的 tooenter 認證，好讓 hello web 應用程式伺服器可以建立安全連線 toohello AD FS 伺服器。 這些認證必須 toobe hello AD FS 伺服器上的本機系統管理員。

![Proxy](./media/active-directory-aadconnect-get-started-custom/adfs4.png)

### <a name="specify-hello-service-account-for-hello-ad-fs-service"></a>指定 hello hello AD FS 服務的服務帳戶
hello AD FS 服務需要網域服務帳戶 tooauthenticate 使用者和 Active Directory 中的查閱使用者資訊。 它可支援兩種類型的服務帳戶：

* **群組受管理服務帳戶** ：在 Windows Server 2012 的 Active Directory 網域服務中導入。 這種類型的帳戶提供服務，例如 AD FS 中，而不需要 tooupdate hello 帳戶密碼會定期在單一帳戶。 如果您已經有 Windows Server 2012 網域控制站在 AD FS 伺服器屬於 hello 網域，請使用此選項。
* **網域使用者帳戶**-此類型的帳戶需要您 tooprovide 密碼和定期更新 hello 密碼 hello 密碼變更或過期時。 您沒有 hello 網域中的 AD FS 伺服器隸屬於 Windows Server 2012 網域控制站時，才使用此選項。

如果您選取了 [群組受管理服務帳戶]，而這項功能從未在 Active Directory 中使用過，系統會提示您輸入企業系統管理員認證。 這些認證使用的 tooinitiate hello 金鑰存放區，然後啟用 Active Directory 中的 hello 功能。

> [!NOTE]
> Azure AD Connect 執行檢查 toodetect 如果 hello AD FS 服務已經註冊為 hello 網域中的 SPN。  AD DS 將不允許重複的 SPN toobe 註冊一次。  如果找到重複的 SPN，您將無法進一步無法 tooproceed 必須先移除 hello SPN。

![AD FS 服務帳戶](./media/active-directory-aadconnect-get-started-custom/adfs5.png)

### <a name="select-hello-azure-ad-domain-that-you-wish-toofederate"></a>選取您想 toofederate hello Azure AD 網域
此設定是 AD FS 與 Azure AD 之間使用的 toosetup hello 同盟關係。 它會設定 AD FS tooissue 安全性語彙基元 tooAzure AD，並設定從這個特定的 AD FS 執行個體的 Azure AD tootrust hello 語彙基元。 此頁面只允許您 tooconfigure hello 初始安裝在單一網域。 您可稍後再次執行 Azure AD Connect 以設定其他網域。

![Azure AD 網域](./media/active-directory-aadconnect-get-started-custom/adfs6.png)

### <a name="verify-hello-azure-ad-domain-selected-for-federation"></a>確認所選取適用於同盟的 hello Azure AD 網域
當您選取 hello 網域 toobe 同盟時，Azure AD Connect 您提供必要資訊 tooverify 未經驗證的網域。 請參閱[新增並驗證 hello 網域](../active-directory-add-domain.md)如何 toouse 這項資訊。

![Azure AD 網域](./media/active-directory-aadconnect-get-started-custom/verifyfeddomain.png)

> [!NOTE]
> AD 連線嘗試 tooverify hello 網域 hello 期間設定階段。 如果您繼續 tooconfigure 而不加入 hello 必要的 DNS 記錄，hello 精靈並不能 toocomplete hello 組態。
>
>

## <a name="configure-and-verify-pages"></a>設定並確認頁面
hello 設定進行此頁面上。

> [!NOTE]
> 在繼續安裝之前，如果已設定同盟，請確定您已設定[同盟伺服器的名稱解析](active-directory-aadconnect-prerequisites.md#name-resolution-for-federation-servers)。
>
>

![準備好 tooconfigure](./media/active-directory-aadconnect-get-started-custom/readytoconfigure2.png)

### <a name="staging-mode"></a>預備模式
很可能 toosetup 新同步處理伺服器以平行方式與預備模式。 它是只支援的 toohave 一個同步處理伺服器匯出 tooone hello 雲端目錄。 但如果您想 toomove 從另一部伺服器，例如一個執行目錄同步，然後您可以啟用預備模式中的 Azure AD Connect。 啟用時，hello 同步處理引擎匯入，而且同步處理資料，做為正常的但不會匯出任何項目 tooAzure 廣告或廣告。 hello 功能密碼同步 」 和 「 密碼回寫會在預備模式停用。

![預備模式](./media/active-directory-aadconnect-get-started-custom/stagingmode.png)

在執行模式時，它是可能 toomake 必要的變更 toohello 同步處理引擎，並檢閱 toobe 匯出相關的功能。 當 hello 組態狀況良好時，請再次執行 hello 安裝精靈，並停用預備模式。 資料現在已經匯出的 tooAzure AD 從這部伺服器。 請確定 toodisable hello 相同時間因此只有一個伺服器主動將匯出的 hello 位於其他伺服器。

如需詳細資訊，請參閱[預備模式](active-directory-aadconnectsync-operations.md#staging-mode)。

### <a name="verify-your-federation-configuration"></a>驗證同盟組態
當您按一下 hello 驗證 按鈕時，azure AD Connect 確認 hello 為您的 DNS 設定。

**內部網路連線能力檢查**

* 解決同盟 FQDN: Azure AD Connect 檢查是否可以解析 DNS tooensure 連線 hello 同盟 FQDN。 如果 Azure AD Connect 無法解析 hello FQDN，hello 驗證將會失敗。 請確認存在順序 toosuccessfully 完成 hello 驗證中的 hello 同盟服務 FQDN 的 DNS 記錄。
* DNS A 記錄：Azure AD Connect 會檢查您的同盟服務是否有 A 記錄。 在 hello 沒有 A 記錄，將會失敗 hello 驗證。 建立 A 記錄而不要 CNAME 記錄為您的同盟 FQDN 順序 toosuccessfully 中完成 hello 驗證。

**外部網路連線能力檢查**

* 解決同盟 FQDN: Azure AD Connect 檢查是否可以解析 DNS tooensure 連線 hello 同盟 FQDN。

![完成](./media/active-directory-aadconnect-get-started-custom/completed.png)

![驗證](./media/active-directory-aadconnect-get-started-custom/adfs7.png)

此外，執行下列驗證步驟的 hello:

* 驗證您可以從瀏覽器從加入網域的電腦上 hello 內部網路登入： 連接 toohttps://myapps.microsoft.com 並驗證 hello 登入與您已登入的帳戶。 hello 內建的 AD DS 系統管理員帳戶未同步處理，也不能進行驗證。
* 驗證您可以從裝置的 hello 外部網路登入。 在家用電腦或行動裝置，連線 toohttps://myapps.microsoft.com 並提供您的認證。
* 驗證豐富型用戶端登入。 連接 toohttps://testconnectivity.microsoft.com，請選擇 hello **Office 365**  索引標籤，並選擇 hello **Office 365 單一登入測試**。

## <a name="next-steps"></a>後續步驟
Hello 安裝完成後，登出並登入一次 tooWindows，才能使用同步處理服務管理員或同步處理規則編輯器。

既然您已安裝的 Azure AD Connect 可以[確認 hello 安裝並指派授權](active-directory-aadconnect-whats-next.md)。

深入了解這些功能，與 hello 安裝已啟用：[防止被意外刪除](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)和[Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md)。

深入了解這些常見的主題：[排程器和 tootrigger 的同步處理](active-directory-aadconnectsync-feature-scheduler.md)。

深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。
