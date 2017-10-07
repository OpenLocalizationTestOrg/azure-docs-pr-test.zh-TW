---
title: "Azure AD Connect：使用者登入 | Microsoft Docs"
description: "適用於自訂設定的 Azure AD Connect 使用者登入。"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: 547b118e-7282-4c7f-be87-c035561001df
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 7848b419f3855b25cfa074a46779d258bd534bae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-user-sign-in-options"></a>Azure AD Connect 使用者登入選項
Azure Active Directory (Azure AD) 連線可讓您的使用者 toosign tooboth 雲端中，使用內部部署資源 hello 相同密碼。 本文將告訴您選擇要用於登入 tooAzure AD toouse hello 身分識別的每個身分識別模型 toohelp 重要的概念。

如果您已經熟悉 hello Azure AD 身分識別模型，而且想 toolearn 深入了解特定的方法，請參閱 hello 適當的連結：

* 使用[單一登入 (SSO)](active-directory-aadconnect-sso.md) 進行[密碼同步作業](#password-synchronization)
* [傳遞驗證](active-directory-aadconnect-pass-through-authentication.md)
* [同盟 SSO (搭配 Active Directory Federation Services (AD FS))](#federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2)

## <a name="choosing-hello-user-sign-in-method-for-your-organization"></a>選擇 hello 使用者登入方法，為您的組織
對於只想 tooenable 使用者登入 tooOffice 365、 SaaS 應用程式，以及其他 Azure AD 為基礎的資源的大多數組織而言，我們建議 hello 預設密碼同步處理選項。 某些組織中，不過，有特別的理由，它們不能 toouse 此選項。 它們可以選擇同盟登入選項 (例如 AD FS) 或傳遞驗證。 您可以使用下列資料表 toohelp hello 右選擇 hello。

需要時| PS 搭配 SSO| PA 搭配 SSO| AD FS |
 --- | --- | --- | --- |
自動同步的新使用者、 連絡人及群組帳戶，在內部部署 Active Directory toohello 雲端中。|x|x|x|
設定適用於 Office 365 混合式案例的租用戶。|x|x|x|
使用內部部署密碼，即可啟用我在使用者 toosign 和存取雲端服務。|x|x|x|
使用公司認證來實作單一登入。|x|x|x|
確保不會將密碼儲存在 hello 雲端中。||x*|x|
啟用內部部署多重要素驗證解決方案。|||x|

*透過輕量連接器。

>[!NOTE]
> 傳遞驗證目前對於豐富型用戶端有一些限制。 如需詳細資訊，請參閱[傳遞驗證](active-directory-aadconnect-pass-through-authentication.md)。

### <a name="password-synchronization"></a>密碼同步處理
搭配密碼同步處理，從內部部署 Active Directory tooAzure AD 同步的使用者密碼雜湊。 立即使用，讓您的使用者可以隨時 hello 相同 hello 新密碼時密碼已變更或重設內部部署，會同步處理的 tooAzure AD 雲端資源，以及在內部部署資源的密碼。 hello 密碼永遠不會傳送 tooAzure AD 或儲存在 Azure AD 中以純文字。 您可以使用密碼回寫 tooenable 自助式密碼重設 Azure AD 中搭配密碼同步處理。

此外，您可以啟用[SSO](active-directory-aadconnect-sso.md) hello 公司網路上的已加入網域的機器上的使用者。 使用單一登入、 啟用的使用者只需要 tooenter 這些使用者安全地存取雲端資源的使用者名稱 toohelp。

![密碼同步處理](./media/active-directory-aadconnect-user-signin/passwordhash.png)

如需詳細資訊，請參閱 hello[密碼同步化](active-directory-aadconnectsync-implement-password-synchronization.md)發行項。

### <a name="pass-through-authentication"></a>傳遞驗證
使用傳遞驗證，hello 使用者的密碼會針對 hello 在內部部署 Active Directory 控制站進行驗證。 hello 密碼不需要以任何形式的 Azure AD 中 toobe。 這可讓內部部署原則，例如登入時數限制，toobe 驗證 toocloud 服務期間進行評估。

傳遞驗證 hello 在內部部署環境中的 Windows Server 2012 R2 已加入網域的電腦上使用簡單的代理程式。 此代理程式會接聽密碼驗證要求。 它並不需要任何輸入連接埠 toobe 開啟 toohello 網際網路。

此外，您也可以啟用單一登入 hello 公司網路上的已加入網域的機器上的使用者。 使用單一登入、 啟用的使用者只需要 tooenter 這些使用者安全地存取雲端資源的使用者名稱 toohelp。
![傳遞驗證](./media/active-directory-aadconnect-user-signin/pta.png)

如需詳細資訊，請參閱：
- [傳遞驗證](active-directory-aadconnect-pass-through-authentication.md)
- [單一登入](active-directory-aadconnect-sso.md)

### <a name="federation-that-uses-a-new-or-existing-farm-with-ad-fs-in-windows-server-2012-r2"></a>使用新的或現有伺服器陣列搭配 Windows Server 2012 R2 中的 AD FS 建立的同盟
使用同盟登入，您的使用者可以登入 tooAzure AD 服務與內部部署密碼。 當他們在 hello 公司網路時，即使沒有 tooenter 他們的密碼。 藉由使用 AD FS 中的 hello 同盟選項，您可以部署新的或現有的伺服陣列，與 Windows Server 2012 R2 中 AD FS。 如果您選擇 toospecify 現有的伺服器陣列時，Azure AD Connect 會設定 hello 伺服器陣列和 Azure AD 之間的信任，讓您的使用者可以登入。

<center>![與 Windows Server 2012 R2 中的 AD FS 搭配的同盟](./media/active-directory-aadconnect-user-signin/federatedsignin.png)</center>

#### <a name="deploy-federation-with-ad-fs-in-windows-server-2012-r2"></a>部署與 Windows Server 2012 R2 中 AD FS 搭配的同盟

如果要部署新的伺服器陣列，您需要：

* Hello 同盟伺服器的 Windows Server 2012 R2 伺服器。
* Windows Server 2012 R2 伺服器 hello Web 應用程式 Proxy。
* 一個 .pfx 檔案，內含一個 SSL 憑證，用於預期使用的同盟服務名稱。 例如：fs.contoso.com。

如果要部署新的伺服器陣列或使用現有的伺服器陣列，您需要：

* 同盟伺服器上的本機系統管理員認證。
* 本機系統管理員認證 （未加入網域） 的任何工作群組伺服器上您想 toodeploy hello Web 應用程式 Proxy 角色上。
* 您執行 hello 精靈 toobe 無法 tooconnect tooany 上您想 tooinstall AD FS 或 Web Application Proxy 上，使用 Windows 遠端管理其他機器 hello 機器。

如需詳細資訊，請參閱[設定與 AD FS 搭配的 SSO](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs)。

#### <a name="sign-in-by-using-an-earlier-version-of-ad-fs-or-a-third-party-solution"></a>使用舊版 AD FS 或協力廠商解決方案進行登入
如果您已經使用舊版 （例如 AD FS 2.0) 的 AD FS 或協力廠商同盟提供者設定雲端登入，您可以選擇 tooskip 使用者登入設定，透過 Azure AD Connect。 這可讓您 tooget hello 最新同步處理和其他功能的 Azure AD Connect 同時登入使用現有的方案。

如需詳細資訊，請參閱 hello [Azure AD 協力廠商同盟相容性清單](active-directory-aadconnect-federation-compatibility.md)。


## <a name="user-sign-in-and-user-principal-name"></a>使用者登入和使用者主體名稱
### <a name="understanding-user-principal-name"></a>了解使用者主體名稱
在 Active Directory 中，hello 預設使用者主要名稱 (UPN) 尾碼是 hello hello 使用者帳戶建立所在的 hello 網域 DNS 名稱。 在大部分情況下，這是 hello 註冊為 hello 網際網路上的 hello 企業網域的網域名稱。 不過，您可以使用「Active Directory 網域及信任」來新增其他 UPN 尾碼。

hello hello 使用者的 UPN hello 格式username@domain。 例如，名為"contoso.com"的 Active Directory 網域，名為 John 的使用者可能 hello UPN"john@contoso.com"。 hello hello 使用者的 UPN，根據 RFC 822。 雖然 hello UPN 和電子郵件共用 hello 相同的格式，使用者的 UPN hello hello 值可能會或可能相同 hello hello 的 hello 使用者的電子郵件地址。

### <a name="user-principal-name-in-azure-ad"></a>Azure AD 中的使用者主體名稱
hello Azure AD Connect 精靈會使用 hello userPrincipalName 屬性，或可讓您指定 hello 做為從內部 hello 使用者主體名稱在 Azure AD 中的屬性 （在自訂安裝） toobe。 這是用於簽署 tooAzure AD 中的 hello 值。 如果 hello hello userPrincipalName 屬性值未對應 tooa 驗證網域在 Azure AD 中，則 Azure AD 會將它取代預設值。 onmicrosoft.com 值。

Azure Active Directory 中的每個目錄會隨附內建的網域名稱，與 hello 格式 contoso.onmicrosoft.com，可讓您開始使用 Azure 或其他 Microsoft 服務。 您可以改善，及使用自訂網域，以簡化 hello 登入體驗。 如需自訂網域名稱在 Azure AD 中的資訊和如何 tooverify 網域，請參閱[加入您的自訂網域名稱 tooAzure Active Directory](../add-custom-domain.md#add-your-custom-domain)。

## <a name="azure-ad-sign-in-configuration"></a>Azure AD 登入組態
### <a name="azure-ad-sign-in-configuration-with-azure-ad-connect"></a>使用 Azure AD Connect 設定 Azure AD 登入組態
hello Azure AD 登入體驗取決於 Azure AD 可比對的使用者正在同步處理的 tooone hello hello Azure AD 目錄中經過驗證的自訂網域的 hello 使用者主要名稱尾碼。 Azure AD Connect 會時提供說明您設定 Azure AD 登入設定，使 hello 中的使用者登入經驗 hello 雲端類似 toohello 在內部部署經驗。

Azure AD Connect 清單 hello hello 網域和嘗試 toomatch 所定義的 UPN 尾碼他們在 Azure AD 中的自訂網域。 然後，協助您與 hello 需要 toobe 採取的適當動作。
hello Azure AD 登入頁面會列出針對在內部部署 Active Directory 所定義的 hello UPN 尾碼，並顯示 hello 相對應針對每個尾碼的狀態。 hello status 值可以是 hello 下列其中一種：

| State | 說明 | 需要採取的動作 |
|:--- |:--- |:--- |
| Verified |Azure AD Connect 在 Azure AD 中找到一個已驗證的相符網域。 此網域的所有使用者均可使用其內部部署認證來進行登入。 |不需要採取任何動作。 |
| 未驗證 |Azure AD Connect 在 Azure AD 中找到對應的自訂網域，但該網域未經驗證。 hello UPN 尾碼的 hello 這個網域的使用者將會變更 toohello 預設值。 如果不驗證 hello 網域同步處理後的 onmicrosoft.com 尾碼。 | [在 Azure AD 中驗證 hello 的自訂網域。](../add-custom-domain.md#verify-the-domain-name-with-azure-ad) |
| 未新增 |Azure AD Connect 找不到自訂網域逐步 toohello UPN 尾碼。 hello UPN 尾碼的 hello 這個網域的使用者將會變更 toohello 預設值。 如果 hello 網域未新增並驗證在 Azure 中的 onmicrosoft.com 尾碼。 | [新增並驗證自訂網域對應 toohello UPN 尾碼。](../add-custom-domain.md) |

hello Azure AD 登入頁面會列出 hello UPN 尾碼，針對在內部部署 Active Directory 進行定義，而 hello hello 目前驗證狀態的 Azure AD 中的對應自訂網域。 您現在可以在自訂安裝中，選取在 hello hello 使用者主體名稱的 hello 屬性**Azure AD 登入**頁面。

![Azure AD 登入頁面](./media/active-directory-aadconnect-user-signin/custom_azure_sign_in.png)

您可以按一下 hello 重新整理按鈕 toore 提取 hello 的最新狀態從 Azure AD 的 hello 自訂網域。

### <a name="selecting-hello-attribute-for-hello-user-principal-name-in-azure-ad"></a>選取 Azure AD 中的 hello hello 使用者主體名稱屬性
hello 屬性 userPrincipalName 是使用者使用登入時 tooAzure AD 和 Office 365 中的 hello 屬性。 您應該確認 hello 使用者已同步處理之前的 Azure AD 中所使用的 hello 網域 （也稱為 UPN 尾碼）。

我們強烈建議您保留 hello 預設屬性 userPrincipalName。 如果這個屬性是 nonroutable 且無法驗證，則可能 tooselect 做 hello 屬性所在的另一個屬性 （例如電子郵件） hello 登入識別碼。 這稱為 hello 替代識別碼。 hello 替代 ID 屬性值必須遵循標準 RFC 822 hello。 使用密碼 SSO 和同盟 SSO hello 登入解決方案，您可以使用替代的識別碼。

> [!NOTE]
> 使用替代識別碼並無法與所有的 Office 365 工作負載相容。 如需詳細資訊，請參閱[設定替代登入識別碼](https://technet.microsoft.com/library/dn659436.aspx)。
>
>

#### <a name="different-custom-domain-states-and-their-effect-on-hello-azure-sign-in-experience"></a>不同的自訂網域的狀態和它們對 hello Azure 登入經驗的影響
它是非常重要的 toounderstand hello 關聯性，Azure AD 目錄中的 hello 自訂網域狀態之間，hello 的 UPN 尾碼定義內部。 當您使用 Azure AD Connect 設定同步處理，讓我們由 hello 不同可能 Azure 登入體驗。

下列資訊的 hello，假設我們所關心的 hello UPN 尾碼 contoso.com，可做為 hello 在內部部署目錄中的 UPN-的組件，例如user@contoso.com。

###### <a name="express-settingspassword-synchronization"></a>快速設定/密碼同步處理
| State | 對使用者的 Azure 登入體驗的影響 |
|:---:|:--- |
| 未新增 |在此情況下，針對 contoso.com 沒有自訂網域已新增 hello Azure AD 目錄中。 使用者有 UPN 內部 hello 尾碼@contoso.com將不會無法 toouse tooAzure 在其內部部署 UPN toosign。 它們改為將有 toouse 有 Azure AD 所提供 toothem 加 hello 尾碼 hello 預設 Azure AD 目錄的新 UPN。 例如，如果您要同步處理使用者 toohello Azure AD 目錄 azurecontoso.onmicrosoft.com，然後 hello 內部使用者user@contoso.com會獲得的 UPN user@azurecontoso.onmicrosoft.com。 |
| 未驗證 |在此情況下，我們有 hello Azure AD 目錄中加入自訂網域 contoso.com。 不過，此網域尚未經過驗證。 如果您繼續進行同步的使用者不需驗證 hello 網域，然後 hello 使用者經由 Azure AD 會指派新的 UPN，hello 」 不會加入 「 案例中一樣。 |
| Verified |在此情況下，我們有自訂網域 contoso.com 已新增並驗證 hello Azure AD 中的 UPN 尾碼。 使用者將能夠 toouse 在內部部署使用者主體名稱，例如user@contoso.com，tooAzure 它們正在同步處理之後在 toosign tooAzure AD。 |

###### <a name="ad-fs-federation"></a>AD FS 同盟
您無法建立同盟 hello 預設值。 在 Azure AD 中的 onmicrosoft.com 網域或在 Azure AD 中未經驗證的自訂網域。 當您執行 hello Azure AD Connect 精靈 中，如果您選取未經驗證的網域 toocreate 同盟，則 Azure AD Connect 提示您以必要的 hello 記錄 toobe 建立 hello 網域裝載 DNS 的位置。 如需詳細資訊，請參閱[選取同盟驗證 hello Azure AD 網域](active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation)。

如果您選取 hello 使用者登入選項**與 AD FS 同盟**，則您必須將自訂網域 toocontinue 在 Azure AD 中建立同盟。 如我們討論中，這表示我們應該有 hello Azure AD 目錄中加入自訂網域 contoso.com。

| State | 影響 hello Azure 登入的使用者經驗 |
|:---:|:--- |
| 未新增 |在此情況下，Azure AD Connect 找不到相符的自訂網域 hello Azure AD 目錄中的 hello UPN 尾碼 contoso.com。 如果您需要在使用者 toosign 藉由在 AD FS 使用其內部部署 UPN，需要 tooadd 自訂網域 contoso.com (像是user@contoso.com)。 |
| 未驗證 |在此案例中，Azure AD Connect 會提示您適當的詳細資料，指導您如何在稍後的階段中驗證網域。 |
| Verified |在此情況下，您可以繼續使用 hello 組態，而不進行任何進一步的動作。 |

## <a name="changing-hello-user-sign-in-method"></a>變更使用者的 hello 登入方法
您可以使用 hello 工作中使用的 Azure AD Connect hello 初始設定後的 Azure AD Connect 與 hello 精靈，從同盟、 密碼同步處理或傳遞驗證變更 hello 使用者登入方法。 同樣地，執行 hello Azure AD Connect 精靈，您會看到一份您可以執行的工作。 選取**使用者登入時變更**hello 清單中的工作。

![變更使用者登入](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

Hello 下一個頁面，詢問 tooprovide hello 認證的 Azure AD。

![連接 tooAzure AD](./media/active-directory-aadconnect-user-signin/changeusersignin2.png)

在 hello**使用者登入**頁面上，選取所需的 hello 使用者登入。

![連接 tooAzure AD](./media/active-directory-aadconnect-user-signin/changeusersignin2a.png)

> [!NOTE]
> 如果您只對暫存交換器 toopassword 同步處理，然後選取 hello**不會轉換使用者帳戶**核取方塊。 未核取 hello 選項會轉換每個使用者 toofederated，而它可能需要數小時。
>
>

## <a name="next-steps"></a>後續步驟
- 深入了解[將內部部署身分識別與 Azure Active Directory 整合](active-directory-aadconnect.md)。
- 深入了解 [Azure AD Connect 設計概念](active-directory-aadconnect-design-concepts.md)。
