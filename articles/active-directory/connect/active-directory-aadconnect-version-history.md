---
title: "Azure AD Connect︰版本發行歷程記錄 | Microsoft Docs"
description: "本文章列出 Azure AD Connect 和 Azure AD Sync 的所有版本"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: ef2797d7-d440-4a9a-a648-db32ad137494
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: b55e0f2d426e34ceef9869d5a6d1b0956d8bd076
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-version-release-history"></a>Azure AD Connect︰版本發行歷程記錄
hello Azure Active Directory (Azure AD) 小組定期更新與新特色與功能的 Azure AD Connect。 並非所有更新版本所適用的 tooall 對象。

本文是您追蹤的 hello 版本已發行的設計的 toohelp 和 toounderstand 是否需要 tooupdate toohello 最新版本或不。

下列為相關主題的清單︰


主題 |  詳細資料
--------- | --------- |
從 Azure AD Connect 的步驟 tooupgrade | 不同的方法太[從先前版本 toohello 最新升級](active-directory-aadconnect-upgrade-previous-version.md)Azure AD Connect 的版本。
所需的權限 | 如需所需權限 tooapply 更新，請參閱[帳戶與權限](./active-directory-aadconnect-accounts-permissions.md#upgrade)。
下載| [下載 Azure AD Connect](http://go.microsoft.com/fwlink/?LinkId=615771)。

## <a name="115610"></a>1.1.561.0
狀態：2017 年 7 月 23 日

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>已修正的問題

* 已修正的問題造成 hello 現成的同步處理規則 「 出 tooAD 位使用者的 ImmutableId"toobe 移除：

  * Azure AD Connect 升級資料庫時，就會發生 hello 問題或當 hello 工作選項*更新同步處理設定*在 hello Azure AD Connect 精靈是使用的 tooupdate Azure AD Connect 同步處理設定。
  
  * 此同步處理規則是適用於 toocustomers 人員已啟用 hello [Msds-primary-computer-ConsistencyGuid 做為來源錨點功能](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor)。 此功能已在版本 1.1.524.0 和之後版本中引入。 當移除 hello 同步處理規則時，Azure AD Connect 不再可以填入內部部署 AD ms-DS-ConsistencyGuid 屬性以 hello ObjectGuid 屬性的值。 它無法防止將新的使用者佈建至 Azure AD。
  
  * hello 修正可確保在升級期間，或組態變更期間，將不會移除該 hello 同步處理規則，只要 hello 功能已啟用。 對於現有客戶已受到此問題，hello 修正也可確保該 hello 同步處理規則加入之後 toothis 版本的 Azure AD Connect 升級。

* 修正的問題，導致 toohave 優先順序值，這個值小於 100 的現成的同步處理規則：

  * 通常會將優先順序值 0-99 保留給自訂同步處理規則。 在升級期間，hello 現成的同步處理規則的優先順序值會是更新的 tooaccommodate 同步處理規則變更。 Toothis 問題，因為現成的同步處理規則可能會指派優先順序小於 100 的值。
  
  * hello 修正可防止 hello 問題在升級期間發生。 不過，它不會還原 hello 優先順序值的現有客戶所 hello 問題已受到影響。 Hello 未來 toohelp 與 hello 還原中，將會提供個別修正程式。

* 已修正的問題，其中 hello[網域和 OU 篩選螢幕](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering)在 hello Azure AD Connect 精靈顯示*同步處理所有的網域和 Ou*選項做為選取狀態，即使已啟用組織單位型篩選。

*   已修正的問題，造成的 hello[設定目錄分割螢幕](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering)中同步處理服務管理員 tooreturn 錯誤如果 hello hello*重新整理*按鈕。 hello 錯誤訊息是*「 重新整理網域時發生錯誤： 無法 toocast 物件的型別 'System.Collections.ArrayList' tootype 'Microsoft.DirectoryServices.MetadirectoryServices.UI.PropertySheetBase.MaPropertyPages.PartitionObject。 」* hello 就會發生錯誤時已經加入新的 AD 網域 tooan 現有的 AD 樹系，而且想 tooupdate Azure AD Connect 使用 hello 重新整理 按鈕。

#### <a name="new-features-and-improvements"></a>新功能和改進

* [自動升級功能](active-directory-aadconnect-feature-automatic-upgrade.md)已展開的 toosupport 客戶以 hello 的設定：
  * 您已啟用 hello 裝置回寫功能。
  * 您已啟用 hello 群組回寫功能。
  * hello 安裝不是 Express 設定或 DirSync 升級。
  * 您 hello metaverse 中有 100,000 個以上的物件。
  * 您要連接 toomore 比一個樹系。 快速安裝只連接 tooone 樹系。
  * hello AD 連接器帳戶已 hello 預設 MSOL_ 帳戶不再。
  * hello 伺服器是設定 toobe 預備模式。
  * 您已啟用 hello 使用者回寫功能。
  
  >[!NOTE]
  >hello 範圍擴充的 hello 自動升級功能會影響使用 Azure AD Connect 組建 1.1.105.0 和之後的客戶。 如果您不想自動進行升級您 Azure AD Connect 伺服器 toobe，您必須在您 Azure AD Connect 的伺服器上執行下列 cmdlet: `Set-ADSyncAutoUpgrade -AutoUpgradeState disabled`。 如需有關啟用/停用自動升級的詳細資訊，請參閱 tooarticle [Azure AD Connect： 自動升級](active-directory-aadconnect-feature-automatic-upgrade.md)。

## <a name="115580"></a>1.1.558.0
狀態：將不會發行。 這個組建中的變更隨附於版本 1.1.561.0 中。

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>已修正的問題

* 已修正的問題造成 hello 現成的同步處理規則 「 出 tooAD-使用者的 ImmutableId"toobe 中移除時就會更新組織單位型篩選設定。 此同步處理規則是為了 hello [Msds-primary-computer-ConsistencyGuid 做為來源錨點功能](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor)。

* 已修正的問題，其中 hello[網域和 OU 篩選螢幕](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering)在 hello Azure AD Connect 精靈顯示*同步處理所有的網域和 Ou*選項做為選取狀態，即使已啟用組織單位型篩選。

*   已修正的問題，造成的 hello[設定目錄分割螢幕](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering)中同步處理服務管理員 tooreturn 錯誤如果 hello hello*重新整理*按鈕。 hello 錯誤訊息是*「 重新整理網域時發生錯誤： 無法 toocast 物件的型別 'System.Collections.ArrayList' tootype 'Microsoft.DirectoryServices.MetadirectoryServices.UI.PropertySheetBase.MaPropertyPages.PartitionObject。 」* hello 就會發生錯誤時已經加入新的 AD 網域 tooan 現有的 AD 樹系，而且想 tooupdate Azure AD Connect 使用 hello 重新整理 按鈕。

#### <a name="new-features-and-improvements"></a>新功能和改進

* [自動升級功能](active-directory-aadconnect-feature-automatic-upgrade.md)已展開的 toosupport 客戶以 hello 的設定：
  * 您已啟用 hello 裝置回寫功能。
  * 您已啟用 hello 群組回寫功能。
  * hello 安裝不是 Express 設定或 DirSync 升級。
  * 您 hello metaverse 中有 100,000 個以上的物件。
  * 您要連接 toomore 比一個樹系。 快速安裝只連接 tooone 樹系。
  * hello AD 連接器帳戶已 hello 預設 MSOL_ 帳戶不再。
  * hello 伺服器是設定 toobe 預備模式。
  * 您已啟用 hello 使用者回寫功能。
  
  >[!NOTE]
  >hello 範圍擴充的 hello 自動升級功能會影響使用 Azure AD Connect 組建 1.1.105.0 和之後的客戶。 如果您不想自動進行升級您 Azure AD Connect 伺服器 toobe，您必須在您 Azure AD Connect 的伺服器上執行下列 cmdlet: `Set-ADSyncAutoUpgrade -AutoUpgradeState disabled`。 如需有關啟用/停用自動升級的詳細資訊，請參閱 tooarticle [Azure AD Connect： 自動升級](active-directory-aadconnect-feature-automatic-upgrade.md)。

## <a name="115570"></a>1.1.557.0
狀態：2017 年 7 月

>[!NOTE]
>這個組建不是使用 toocustomers 透過 hello Azure AD 連接自動升級功能。

### <a name="azure-ad-connect"></a>Azure AD Connect

#### <a name="fixed-issue"></a>已修正的問題
* 修正的問題造成 hello hello 現有服務連接點物件 toobe 變更，即使它仍然是有效的網域上設定的已驗證的網域的 hello 初始化 Initialize-adsyncdomainjoinedcomputersync cmdlet。 Azure AD 租用戶具有多個已驗證的網域可以用來設定 hello 服務連接點時，就會發生這個問題。

#### <a name="new-features-and-improvements"></a>新功能和改進
* 密碼回寫現在適用於透過 Microsoft Azure Government 雲端和 Microsoft Cloud Germany 進行預覽。 如需 Azure AD Connect hello 不同服務執行個體支援的詳細資訊，請參閱 tooarticle [Azure AD Connect： 特殊考量的執行個體](active-directory-aadconnect-instances.md)。

* hello 初始化 Initialize-adsyncdomainjoinedcomputersync cmdlet 現在有新的選擇性參數，名為 AzureADDomain。 這個參數可讓您指定的已驗證網域 toobe 可用來設定 hello 服務連接點。

### <a name="pass-through-authentication"></a>傳遞驗證

#### <a name="new-features-and-improvements"></a>新功能和改進
* hello 代理程式已變更傳遞驗證所需的 hello 名稱*Microsoft Azure AD 應用程式 Proxy 連接器*太*Microsoft Azure AD Connect 驗證代理程式*。

* 啟用傳遞驗證預設不再啟用密碼雜湊同步處理。


## <a name="115530"></a>1.1.553.0
狀態：2017 年 6 月

> [!IMPORTANT]
> 這個組建引進了結構描述和同步處理規則變更。 升級之後，Azure AD Connect 同步處理服務將會觸發完整匯入和完整同步處理步驟。 以下將詳述 hello 變更的詳細資料。 tootemporarily 延遲完整匯入和完整同步處理步驟，在升級之後，請參閱 tooarticle [toodefer 完整升級後的同步處理的方式](active-directory-aadconnect-upgrade-previous-version.md#how-to-defer-full-synchronization-after-upgrade)。
>
>

### <a name="azure-ad-connect-sync"></a>Azure AD Connect 同步處理

#### <a name="known-issue"></a>已知問題
* 有個問題會影響搭配 Azure AD Connect 同步處理使用 [OU 型篩選](active-directory-aadconnectsync-configure-filtering.md#organizational-unitbased-filtering)的客戶。當您瀏覽 toohello[網域和 OU 篩選頁面](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering)hello Azure AD Connect 精靈，在預期 hello 下列行為：
  * 如果已啟用組織單位型篩選，hello**同步處理選取的網域和 Ou**選取選項。
  * 否則，hello**同步處理所有的網域和 Ou**選取選項。

hello，就會發生的問題為該 hello**同步處理所有的網域和 Ou 選項**執行 hello 精靈時，一律會選取。  即使先前已設定 OU 型篩選，還是會發生此問題。 之前儲存任何 AAD Connect 組態變更，請先確定 hello**同步處理選取的網域和 Ou 選項**並確認已重新啟用所有需要 toosynchronize 的 Ou。 否則，將會停用 OU 型篩選。

#### <a name="fixed-issues"></a>已修正的問題

* 已修正的問題，可讓 Azure AD 管理員 tooreset hello 密碼的內部部署密碼回寫 AD 權限使用者帳戶。 Azure AD Connect 授 hello 重設密碼權限與 hello 特殊權限的帳戶時，就會發生 hello 問題。 hello 問題將在這個版本的 Azure AD Connect 不允許任意內部部署的 hello 密碼的 Azure AD 管理員 tooreset AD 特殊權限使用者帳戶 hello 管理員除非 hello 該帳戶擁有者。 如需詳細資訊，請參閱太[安全性摘要報告 4033453](https://technet.microsoft.com/library/security/4033453)。

* 已修正的問題相關 toohello [Msds-primary-computer-ConsistencyGuid 做為來源錨點](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor)功能在 Azure AD Connect 不回寫 tooon 是內部 AD Msds-primary-computer ConsistencyGuid 屬性。 hello 問題會發生多個內部部署 AD 樹系新增 tooAzure AD Connect 和 hello*跨多個目錄選項的使用者身分識別存在於*已選取。 使用這類組態時，hello 結果的同步處理規則不會填入 hello Metaverse 中的 hello sourceAnchorBinary 屬性。 hello sourceAnchorBinary 屬性做為 Msds-primary-computer ConsistencyGuid 屬性 hello 來源屬性。 如此一來，回寫 toohello ms DSConsistencyGuid 屬性不會發生。 toofix hello 問題，下列的同步處理規則已更新的 tooensure 的 hello sourceAnchorBinary hello 永遠會填入 Metaverse 中的屬性：
  * In from AD - InetOrgPerson AccountEnabled.xml
  * In from AD - InetOrgPerson Common.xml
  * In from AD - User AccountEnabled.xml
  * In from AD - User Common.xml
  * In from AD - User Join SOAInAAD.xml

* 先前，甚至如果 hello [Msds-primary-computer-ConsistencyGuid 做為來源錨點](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor)功能未啟用，hello"Out tooAD – 使用者的 ImmutableId"同步處理規則仍然會加入 tooAzure AD Connect。 hello 生效是良性的且不會造成 Msds-primary-computer ConsistencyGuid 屬性 toooccur 的回寫。 tooavoid 混淆的可能性，已加入邏輯 hello 功能啟用時，只會加入 hello 的同步處理規則的 tooensure。

* 修正造成密碼雜湊同步處理 toofail 與錯誤事件 611 的問題。 從內部部署 AD 中移除一或多個網域控制站之後，即會發生此問題。 在每個密碼同步處理循環的 hello 結尾，hello 發出的同步處理 cookie 由內部部署 AD 包含 hello 移除網域控制站的 USN （更新序列號碼） 值是 0 的引動過程識別碼。 hello 密碼同步處理管理員無法 toopersist 同步處理 cookie 包含 USN 值為 0，而且與錯誤事件 611 會失敗。 Hello 下次同步處理循環，hello 密碼同步處理管理員重複使用 hello 最後一個保存的同步處理 cookie 不包含 USN 值為 0。 這會導致 hello 相同的密碼變更 toobe 重新同步處理。 透過此修正，hello 密碼同步處理管理員會正確保存 hello 同步處理 cookie。

* 先前，即使自動升級已停用使用 hello 組 ADSyncAutoUpgrade cmdlet，hello 自動升級程序會繼續升級 toocheck 定期而且依賴 hello 下載 installer toohonor 停用。 透過此修正，hello 自動升級程序不會再檢查升級定期。 本版的 Azure AD Connect 升級安裝程式一次執行時，會自動套用 hello 修正程式。

#### <a name="new-features-and-improvements"></a>新功能和改進

* 先前，hello [Msds-primary-computer-ConsistencyGuid 做為來源錨點](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-design-concepts#using-msds-consistencyguid-as-sourceanchor)功能已僅適用於使用 toonew 部署。 現在，它是使用 tooexisting 部署。 具體而言：
  * tooaccess hello 功能、 啟動 hello Azure AD Connect 精靈並選擇 hello*更新來源錨點*選項。
  * 這個選項會使用 objectGuid 做 sourceAnchor 屬性可見 tooexisting 部署。
  * 在設定 hello 選項時，hello 精靈會驗證您在內部部署 Active Directory 中的 hello Msds-primary-computer ConsistencyGuid 屬性 hello 狀態。 Hello 屬性未設定任何 hello 目錄中的使用者物件上，如果 hello 精靈會使用 hello Msds-primary-computer ConsistencyGuid 作為 hello sourceAnchor 屬性。 如果在 hello 目錄中的一個或多個使用者物件上設定 hello 屬性，hello 精靈結束時 hello 屬性正由其他應用程式，並不適合做為 sourceAnchor 屬性，而且不允許 hello 來源錨點變更 tooproceed。 如果您確定該 hello 屬性不會使用現有的應用程式，您需要 toocontact 支援 toosuppress 如何 hello 錯誤的詳細資訊。

* 特定太**userCertificate**憑證值所需的裝置物件 （Azure AD Connect 現在） 上的屬性會尋找[連接已加入網域裝置 tooAzure for Windows 10 體驗 AD](https://docs.microsoft.com/azure/active-directory/active-directory-azureadjoin-devices-group-policy)也已經篩選掉 hello tooAzure AD 同步處理之前的其餘部分。 tooenable 這種行為，hello 鶈蜪同步規則 「 出 tooAAD-裝置加入 SOAInAD 已更新。

* Azure AD Connect 現在支援回寫的 Exchange Online **cloudPublicDelegates**屬性 tooon 內部部署 AD **publicDelegates**屬性。 這可讓其中的 Exchange Online 信箱可以授與 SendOnBehalfTo 與內部部署 Exchange 信箱的權限 toousers hello 案例。 toosupport 這項功能、 新的現成的同步處理規則 「 出 tooAD – 使用者 Exchange 混合式 PublicDelegates 回寫 」 已新增。 此同步處理規則只會加入 tooAzure AD 連接啟用 Exchange 混合功能時。

*   Azure AD Connect 現可支援同步處理 hello **altRecipient**從 Azure AD 的屬性。 這項變更，下列現成的同步處理規則已被的 toosupport 更新 tooinclude hello 所需屬性流程：
  * In from AD – User Exchange
  * Out tooAAD – 使用者 ExchangeOnline
  
* hello **cloudSOAExchMailbox** hello Metaverse 中的屬性會指出指定的使用者是否有 Exchange Online 信箱，或沒有。 其定義已更新的 tooinclude 其他 Exchange Online RecipientDisplayTypes 為這類的設備與會議室信箱。 tooenable 從更新這項變更，hello cloudSOAExchMailbox 屬性底下的現成的同步處理規則 「 在從 AAD – 使用者 Exchange 混合 」，找到的 hello 定義：

```
CBool(IIF(IsNullOrEmpty([cloudMSExchRecipientDisplayType]),NULL,BitAnd([cloudMSExchRecipientDisplayType],&amp;HFF) = 0))
```

...toohello 下列：

```
CBool(
  IIF(IsPresent([cloudMSExchRecipientDisplayType]),(
    IIF([cloudMSExchRecipientDisplayType]=0,True,(
      IIF([cloudMSExchRecipientDisplayType]=2,True,(
        IIF([cloudMSExchRecipientDisplayType]=7,True,(
          IIF([cloudMSExchRecipientDisplayType]=8,True,(
            IIF([cloudMSExchRecipientDisplayType]=10,True,(
              IIF([cloudMSExchRecipientDisplayType]=16,True,(
                IIF([cloudMSExchRecipientDisplayType]=17,True,(
                  IIF([cloudMSExchRecipientDisplayType]=18,True,(
                    IIF([cloudMSExchRecipientDisplayType]=1073741824,True,(
                       IF([cloudMSExchRecipientDisplayType]=1073741840,True,False)))))))))))))))))))),False))

```

* 加入的 hello 下列設定建立同步處理規則運算式 toohandle 憑證值 hello userCertificate 屬性中的 X509Certificate2 相容函式：

    ||||
    | --- | --- | --- |
    |CertSubject|CertIssuer|CertKeyAlgorithm|
    |CertSubjectNameDN|CertIssuerOid|CertNameInfo|
    |CertSubjectNameOid|CertIssuerDN|IsCert|
    |CertFriendlyName|CertThumbprint|CertExtensionOids|
    |CertFormat|CertNotAfter|CertPublicKeyOid|
    |CertSerialNumber|CertNotBefore|CertPublicKeyParametersOid|
    |CertVersion|CertSignatureAlgorithmOid|選取|
    |CertKeyAlgorithmParams|CertHashString|Where|
    |||With|

* 下列結構描述變更已經導入了的 tooallow 客戶 toocreate 自訂同步處理規則 tooflow sAMAccountName、 domainNetBios，以及 domainFQDN 群組物件的辨別名稱不正確的使用者物件：

  * TooMV 結構描述已加入下列屬性：
    * 群組：AccountName
    * 群組：domainNetBios
    * 群組：domainFQDN
    * 人員：distinguishedName

  * TooAzure AD 連接器結構描述已加入下列屬性：
    * 群組：OnPremisesSamAccountName
    * 群組：NetBiosName
    * 群組：DnsDomainName
    * 使用者：OnPremisesDistinguishedName

* hello Initialize-adsyncdomainjoinedcomputersync cmdlet 指令碼現在具有名為 AzureEnvironment 新的選擇性參數。 使用對應的 Azure Active Directory 租用戶裝載在哪些地區 hello 的 toospecify hello 參數。 有效值包含：
  * AzureCloud (預設值)
  * AzureChinaCloud
  * AzureGermanyCloud
  * USGovernment
 
* 更新同步處理規則編輯器 toouse 聯結 （而不是佈建） hello 的連結類型的預設值同步處理規則建立期間。

### <a name="ad-fs-management"></a>AD FS 管理

#### <a name="issues-fixed"></a>已修正的問題

* 下列 Url 會針對驗證中斷的 Azure AD tooimprove 提供恢復功能所導入新的 WS-同盟端點而且加入的 tooon 內部部署 AD FS 信賴憑證者合作對象信任設定：
  * https://ests.login.microsoftonline.com/login.srf
  * https://stamp2.login.microsoftonline.com/login.srf
  * https://ccs.login.microsoftonline.com/login.srf
  * https://ccs-sdf.login.microsoftonline.com/login.srf
  
* 修正造成 IssuerID AD FS toogenerate 不正確的宣告值的問題。 如果有多個已驗證的網域中 hello Azure AD 租用戶和 hello userPrincipalName 屬性會用 toogenerate hello 網域尾碼 hello 的 IssuerID 宣告，至少是發生 hello 問題 3 層級深層 (比方說， johndoe@us.contoso.com)。 hello 問題的解決方式更新 hello regex hello 宣告規則所使用。

#### <a name="new-features-and-improvements"></a>新功能和改進
* 先前，Azure AD Connect 所提供的 hello ADFS 憑證管理功能僅能與管理透過 Azure AD Connect 的 ADFS 伺服器陣列。 現在，您可以使用 hello 功能與未受管理使用 Azure AD Connect 的 ADFS 伺服器陣列。

## <a name="115240"></a>1.1.524.0
發行日期：2017 年 5 月

> [!IMPORTANT]
> 這個組建引進了結構描述和同步處理規則變更。 升級之後，Azure AD Connect 同步處理服務將會觸發完整匯入和完整同步處理步驟。 以下將詳述 hello 變更的詳細資料。
>
>

**已修正的問題：**

Azure AD Connect 同步處理

* 修正造成 hello Azure AD Connect 的伺服器的自動升級 toooccur，即使客戶已停用使用 hello 組 ADSyncAutoUpgrade cmdlet hello 功能的問題。 透過此修正，hello hello 伺服器上自動升級程序仍然會檢查升級定期，但是 hello 下載的安裝程式會接受 hello 自動升級組態。
* 在 DirSync 就地升級時，Azure AD Connect 會建立與 Azure AD 同步處理 hello Azure AD 連接器所用的 Azure AD 服務帳戶 toobe。 建立 hello 帳戶之後，使用 hello 帳戶的 Azure AD 驗證 Azure AD Connect。 某些情況下，驗證失敗時由於暫時性問題，這又會發生錯誤導致 DirSync 就地升級 toofail *」 設定 AAD 同步處理工作執行時發生錯誤： AADSTS50034: toosign 入此應用程式，hello 帳戶您必須新增 toohello xxx.onmicrosoft.com 目錄。"* tooimprove hello 恢復功能的 DirSync 升級，Azure AD Connect 立即重試 hello 驗證步驟。
* 與組建 443 導致 DirSync 就地升級 toosucceed 發生問題，但不是會建立所需的目錄同步作業的執行設定檔。 修復邏輯已包含在 Azure AD Connect 的此組建中。 當客戶升級 toothis 組建時，Azure AD Connect 會偵測遺漏執行設定檔，並建立它們。
* 已修正的問題與事件識別碼 6900 和錯誤會導致密碼同步處理程序 toofail toostart *"hello 已加入相同的索引鍵的項目 」*。 如果您更新 OU 篩選組態 tooinclude AD 設定磁碟分割，就會發生這個問題。 toofix 立即處理此問題，密碼同步化會同步處理 AD 網域分割區的密碼變更。 系統會略過非網域分割，例如組態分割。
* 快速安裝在 Azure AD Connect 會建立內部部署 AD DS 帳戶 toobe 供 hello AD 連接器 toocommunicate 與內部部署 AD。 先前，hello 帳戶會建立在 hello 使用者帳戶控制屬性上設定的 hello PASSWD_NOTREQD 旗標並 hello 帳戶設定的隨機密碼。 現在，Azure AD Connect 明確移除 hello PASSWD_NOTREQD 旗標之後 hello 帳戶設定 hello 密碼。
* 已修正的問題，錯誤會導致 DirSync 升級 toofail *「 死結發生 sql server 中的嘗試 tooacquire 應用程式鎖定 」*在 hello 中找到 hello mailNickname 屬性在內部部署 AD 結構描述，但不是已繫結的 toohello AD 使用者物件類別。
* 固定系統管理員正在更新 Azure AD Connect 同步處理設定，使用 Azure AD Connect 精靈時，會停用，導致裝置回寫功能 tooautomatically 的問題。 這被因為 hello 精靈執行先決條件檢查的 hello 現有裝置回寫設定在內部部署 AD 和 hello 檢查失敗。 如果先前已啟用裝置回寫，hello 修正程式是 tooskip hello 核取。
* tooconfigure OU 篩選，您可以使用 hello Azure AD Connect 精靈或 hello 同步處理服務管理員。 先前，如果您使用 hello Azure AD Connect 精靈 tooconfigure OU 篩選，建立新的 Ou 之後會包含為目錄同步作業。 如果您不想包含新的 Ou toobe，您必須設定 OU 篩選使用 hello 同步處理服務管理員。 現在，您可以達到 hello 使用 Azure AD Connect 精靈的行為相同。
* 修正的問題，導致 Azure AD Connect toobe hello hello 下 hello dbo 結構描述，而不安裝系統管理員，結構描述下建立所需的預存程序。
* 修正造成 hello TrackingId 屬性傳回的 Azure AD toobe 省略 hello AAD 連接伺服器事件記錄檔中的問題。 如果 Azure AD Connect 從 Azure AD 接收重新導向訊息以及 Azure AD Connect 無法 tooconnect toohello 端點提供，就會發生 hello 問題。 hello TrackingId 供支援工程師 toocorrelate 與服務端記錄檔中，在疑難排解期間。
* 當 Azure AD Connect 收到 LargeObject 錯誤從 Azure AD 時，Azure AD Connect 會產生具有 EventID 6941 和訊息的事件*「 hello 佈建的物件是太大。修剪 hello 的屬性值，這個物件上的數字。"* 在 hello 相同時，Azure AD Connect 也會產生誤導 EventID 6900 和訊息事件*"Microsoft.Online.Coexistence.ProvisionRetryException： 無法以 hello Windows toocommunicate Azure Active Directory 服務。 」* toominimize 混淆的可能性，Azure AD Connect 不會再產生時收到錯誤 LargeObject hello 第二個事件。
* 修正 Generic LDAP 連接器 tooupdate hello 組態時，會導致 hello 同步處理服務管理員 toobecome 沒有回應的問題。

**新功能/改進︰**

Azure AD Connect 同步處理
* 同步處理規則變更 – hello 下列實作變更的同步處理規則：
  * 更新的預設同步處理規則集 toonot 匯出屬性**userCertificate**和**userSMIMECertificate** hello 屬性有超過 15 的值。
  * AD 屬性**employeeID**和**msExchBypassModerationLink**現在會包含在 hello 預設同步處理規則集。
  * 已經從預設同步處理規則集中移除 AD 屬性 **photo**。
  * 加入**preferredDataLocation** toohello Metaverse 結構描述和 AAD 連接器結構描述。 客戶希望的 tooupdate 任一 Azure AD 中的屬性可以實作自訂同步處理規則 toodo 因此。 toofind hello 屬性，深入了解，請參閱 tooarticle 區段[Azure AD Connect 同步： 如何變更 toohello toomake 預設組態-啟用同步處理的 PreferredDataLocation](active-directory-aadconnectsync-change-the-configuration.md#enable-synchronization-of-preferreddatalocation)。
  * 加入**userType** toohello Metaverse 結構描述和 AAD 連接器結構描述。 客戶希望的 tooupdate 任一 Azure AD 中的屬性可以實作自訂同步處理規則 toodo 因此。

* Azure AD Connect 現在會自動啟用 hello 使用 ConsistencyGuid 屬性為 hello 來源錨點屬性在內部部署 AD 物件。 此外，Azure AD Connect 會填入 hello ConsistencyGuid 屬性 hello objectGuid 屬性的值，如果是空白。 這項功能是只適用 toonew 部署。 toofind 深入了解這項功能，請參閱 tooarticle 區段[Azure AD Connect： 設計概念-使用做為 sourceAnchor Msds-primary-computer ConsistencyGuid](active-directory-aadconnect-design-concepts.md#using-msds-consistencyguid-as-sourceanchor)。
* 新的疑難排解的 cmdlet 已叫用 ADSyncDiagnostics 加入的 toohelp 診斷密碼雜湊同步處理相關的問題。 如需使用 hello 指令程式的資訊，請參閱 tooarticle[與 Azure AD Connect 同步處理的密碼同步化疑難排解](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-troubleshoot-password-synchronization)。
* Azure AD Connect 現在支援同步處理擁有郵件功能的公用資料夾物件從內部部署 AD tooAzure AD。 您可以啟用 hello 功能使用 Azure AD Connect 精靈在選擇性功能 下。 toofind 深入了解這項功能，請參閱 tooarticle [Office 365 目錄基礎邊緣封鎖支援在內部部署郵件擁有公用資料夾](https://blogs.technet.microsoft.com/exchange/2017/05/19/office-365-directory-based-edge-blocking-support-for-on-premises-mail-enabled-public-folders)。
* Azure AD Connect 需要從內部部署 AD DS 帳戶 toosynchronize AD。 以前，如果您已安裝 Azure AD Connect 使用 hello 快速模式，您可以提供 hello 企業系統管理員帳戶認證以及 Azure AD Connect 會建立 hello AD DS 所需的帳戶。 不過，在自訂安裝與加入樹系 tooan 現有部署，您是需要的 tooprovide hello AD DS 帳戶改為。 現在，您也可以 hello 選項 tooprovide hello 企業系統管理員帳戶的認證在自訂安裝，並讓建立 hello AD DS 帳戶所需的 Azure AD Connect。
* Azure AD Connect 現在支援 SQL AOA。 您必須在安裝 Azure AD Connect 之前啟用 SQL AOA。 在安裝期間，Azure AD Connect 會偵測是否提供 hello SQL 執行個體已啟用 SQL AOA 與否。 如果已啟用 SQL AOA，Azure AD Connect 進一步找出 SQL AOA 是否設定的 toouse 同步或非同步複寫。 當設定 hello 可用性群組接聽程式，建議您設定 hello RegisterAllProvidersIP 屬性 too0。 這是因為 Azure AD Connect 目前使用 SQL Native Client tooconnect tooSQL 和 SQL Native Client 不支援使用 MultiSubNetFailover 屬性 hello。
* 如果您使用 LocalDB hello 資料庫做為您 Azure AD Connect 的伺服器，且已達到其 10 GB 大小限制，hello 同步處理服務不會再啟動。 先前，您需要 tooperform ShrinkDatabase 作業在 hello LocalDB tooreclaim DB 空間不足，無法 hello 同步處理服務 toostart。 之後它，您可以使用 hello 同步處理服務管理員 toodelete 執行歷程記錄 tooreclaim 多個資料庫空間。 現在，您可以使用開始 ADSyncPurgeRunHistory cmdlet toopurge 從 LocalDB tooreclaim DB 空間執行歷程記錄資料。 此外，這個 cmdlet 支援離線模式 (藉由指定 hello-offline 參數) 時，使用 hello 同步處理服務，它可以未執行。 注意： hello 離線模式可以只用 hello 同步處理服務未執行，而且使用 hello 資料庫為 LocalDB。
* tooreduce hello 儲存空間所需的數量，Azure AD Connect 現在同步錯誤詳細資料會先壓縮儲存在 LocalDB/SQL 資料庫。 從較舊版本的 Azure AD Connect toothis 版本升級時，Azure AD Connect 執行一次性的壓縮現有的同步處理錯誤詳細資料。
* 先前，在更新之後 OU 篩選組態，您必須手動執行完整匯入 tooensure 現有物件是正確包含/排除目錄同步作業。 現在，Azure AD Connect 都會自動觸發完整匯入期間 hello 下一個同步處理循環。 此外，完整匯入是只能受 hello 更新套用的 toohello AD 連接器。 注意： 這項改進是適用 tooOU 篩選使用 hello Azure AD Connect 精靈 」 所做的更新。 不適用 tooOU 篩選使用 hello 同步處理服務管理員所做的更新。
* 先前，以群組為基礎的篩選僅支援使用者、群組和連絡人物件。 現在，以群組為基礎的篩選也支援電腦物件。
* 先前，您可以刪除連接器空間資料，而不需停用 Azure AD Connect 同步排程器。 現在，hello 同步處理服務管理員區塊 hello 刪除連接器空間資料如果它偵測到該 hello 排程器已啟用。 此外，警告會傳回有關可能資料遺失的 tooinform 客戶 hello 連接器空間資料會被刪除。
* 先前，您必須停用 Azure AD Connect 精靈 toorun PowerShell 的轉譯正確。 此問題已部份解決。 如果您使用 Azure AD Connect 精靈 toomanage 同步作業組態，您可以啟用 PowerShell 文字記錄。 如果您使用 Azure AD Connect 精靈 toomanage ADFS 設定，您必須停用 PowerShell 文字記錄。



## <a name="114860"></a>1.1.486.0
發行日期︰2017 年 4 月

**已修正的問題：**
* 已修正 hello 問題，Azure AD Connect 會成功安裝當地語系化版本的 Windows Server 上。

## <a name="114840"></a>1.1.484.0
發行日期︰2017 年 4 月

**已知問題︰**

* 如果下列條件的 hello 條件都成立，不會成功安裝此版本的 Azure AD Connect:
   1. 您執行 DirSync 就地升級或全新的 Azure AD Connect 安裝。
   2. 您使用其中 hello hello 伺服器上的內建系統管理員群組的名稱不是 「 系統管理員 」 的 Windows Server 的當地語系化的版本。
   3. 您正在使用 hello 預設 SQL Server 2012 Express LocalDB 與 Azure AD Connect，而不是提供完整的 SQL 一起安裝。

**已修正的問題：**

Azure AD Connect 同步處理
* 已修正下列問題其中 hello 同步處理排程器會略過 hello 整個同步處理步驟如果該同步處理步驟的執行設定檔遺漏一個或多個連接器。 例如，您手動新增連接器，而不需要建立執行設定檔，其差異匯入使用 hello 同步處理服務管理員。 此修正可確保該 hello 同步處理排程器會繼續 toorun 差異匯入的其他連接器。
* 已修正下列問題其中 hello 同步處理服務會立即停止處理執行設定檔時遇到問題的其中一個 hello 執行步驟。 此修正可確保該 hello 同步處理服務會略過執行步驟並繼續 tooprocess hello rest。 例如，您有一個「差異匯入」執行設定檔，用於具有多個執行步驟 (每個內部部署 AD 網域各有一個執行步驟) 的 AD 連接器。 hello 同步處理服務會執行差異匯入 hello 其他的 AD 網域即使其中一個網路連線問題。
* 修正造成 hello Azure AD Connector 更新 toobe 略過自動升級期間的問題。
* 已修正的問題該原因 Azure AD Connect tooincorrectly 判斷 hello 伺服器是否為網域控制站在安裝期間，這會開啟導致 DirSync 升級 toofail。
* 固定，導致就地升級 toonot 任何建立的目錄同步的問題執行 hello Azure AD 連接器的設定檔。
* 已修正下列問題其中 hello Synchronization Service Manager 使用者介面變得沒有回應時，嘗試 tooconfigure 泛型 LDAP 連接器。

AD FS 管理
* 修正的問題如果 hello AD FS 主要節點已移動的 tooanother 伺服器 hello Azure AD Connect 精靈會失敗。

傳統型 SSO
* 修正 hello Azure AD Connect 精靈 中的問題，其中 hello 登入畫面不會讓您啟用桌面 SSO 功能，如果您選擇的密碼同步處理為全新安裝期間您登入的選項。

**新功能/改進︰**

Azure AD Connect 同步處理
* Azure AD 連接 Sync 現在支援 hello 使用虛擬服務帳戶、 受管理的服務帳戶和群組受管理的服務帳戶做為其服務帳戶。 這適用於 Azure AD connect 只 toonew 安裝。 安裝 Azure AD Connect 時：
    * 根據預設，Azure AD Connect 精靈會建立一個「虛擬服務帳戶」，並使用它作為其服務帳戶。
    * 如果您要安裝在網域控制站上，Azure AD Connect 會回復 tooprevious 行為，它會建立網域使用者帳戶和使用做為其服務帳戶。
    * 您可以藉由提供 hello 下列其中一種覆寫 hello 預設行為：
      * 群組受管理服務帳戶
      * 受管理的服務帳戶
      * 網域使用者帳戶
      * 本機使用者帳戶
* 先前，如果您升級 tooa 新組建的 Azure AD Connect 包含更新的連接器或 Azure AD Connect 同步處理規則變更將會觸發完整同步處理循環。 現在，Azure AD Connect 會選擇性地僅針對具有更新的連接器觸發「完整匯入」步驟，以及僅針對具有同步處理規則變更的連接器觸發「完整同步處理」步驟。
* 先前，hello 匯出刪除閾值僅適用於 tooexports 透過 hello 同步處理排程器會觸發。 現在，hello 功能會延伸 tooinclude 匯出 hello 客戶使用 hello 同步處理服務管理員手動觸發。
* 在您的 Azure AD 租用戶上，有一個指出是否已為租用戶啟用「密碼同步處理」功能的服務組態。 先前，很容易 hello 服務組態 toobe 您已經有作用中和臨時伺服器時不正確地設定 Azure AD Connect。 現在，Azure AD Connect 會嘗試利用使用中一致的 tookeep hello 服務組態僅限 Azure AD Connect 的伺服器。
* 如果內部部署 AD 未啟用「AD 資源回收筒」，Azure AD Connect 精靈現在會偵測到並傳回警告。
* 先前，匯出 tooAzure AD 逾時並失敗如果 hello 結合 hello 批次中的 hello 物件的大小超過某個臨界值。 現在，hello 同步處理服務將重新嘗試 tooresend hello 物件個別較小的批次中，如果遇到 hello 問題時。
* 已從 Windows [開始] 功能表移除 hello 同步處理服務金鑰管理的應用程式。 管理加密金鑰將會繼續支援透過命令列介面使用 miiskmu.exe toobe。 管理加密金鑰的相關資訊，請參閱 tooarticle [Abandoning hello Azure AD 連接同步處理加密金鑰](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnectsync-change-serviceacct-pass#abandoning-the-azure-ad-connect-sync-encryption-key)。
* 過去，如果您變更 hello Azure AD Connect 同步處理服務帳戶密碼，hello 同步處理服務之前將無法可以開始正確您已在放棄 hello 加密金鑰並重新初始化 hello Azure AD Connect 同步處理服務帳戶密碼。 現在，已不再需要這麼做。

傳統型 SSO

* Azure AD Connect 精靈不再需要時設定的傳遞驗證和桌面 SSO 開啟 hello 網路上的連接埠 9090 toobe。 只需要開啟連接埠 443。 

## <a name="114430"></a>1.1.443.0
發行日期︰2017 年 3 月

**已修正的問題：**

Azure AD Connect 同步處理
* 修正的問題，這會導致 Azure AD Connect 精靈 toofail 如果 hello 顯示 hello Azure AD Connector 名稱不包含 hello 初始 onmicrosoft.com 網域指派 toohello Azure AD 租用戶。
* 修正導致 Azure AD Connect 精靈 toofail hello hello 同步處理服務帳戶密碼包含特殊字元，例如所有格符號、 冒號和空間時進行連線 tooSQL 資料庫時的問題。
* 修正的問題，這會導致 hello 錯誤 「 hello dimage 沒有錨點不同於 hello 映像 」 toooccur，Azure AD Connect 中的伺服器上執行的模式，之後您已暫時排除在內部 AD 從同步處理物件，並重新加入正在同步處理。
* 修正的問題，這會導致 hello 錯誤 「 hello 物件的 DN 不虛設項目 」 toooccur，Azure AD Connect 中的伺服器上執行的模式，之後您已暫時排除在內部 AD 從同步處理物件，並再一次包含用於同步處理。

AD FS 管理
* 修正的問題，其中 Azure AD Connect 精靈不會更新 AD FS 組態和設定 hello 右 hello 設定替代的登入識別碼後，信賴憑證者信任宣告。
* Azure AD Connect 精靈所在 toocorrectly 無法處理 AD FS 伺服器使用 userPrincipalName 格式而不 sAMAccountName 格式設定其服務帳戶的情況下修正的問題。

傳遞驗證
* 修正的問題，這會導致 Azure AD Connect 精靈 toofail，如果已選取 傳遞透過驗證，但其連接子登錄失敗。
* 修正的問題，這會導致 Azure AD Connect 精靈 toobypass 驗證會檢查啟用桌面 SSO 功能時所選取的登入方法。

密碼重設
* 已修正的問題而導致 hello Azure AAD Connect 伺服器 toonot 嘗試 toore-如果 hello 連接已清除的防火牆或 proxy 的連線。

**新功能/改進︰**

Azure AD Connect 同步處理
* Get-ADSyncScheduler Cmdlet 現在會傳回一個名為 SyncCycleInProgress 的新布林值屬性。 如果 hello 傳回值為 true，則表示已排定的同步處理循環正在進行中。
* 已從 %localappdata%\AADConnect too%programdata%\AADConnect tooimprove 協助工具 toohello 記錄檔移目的地資料夾來儲存 Azure AD Connect 的安裝與安裝程式記錄檔。

AD FS 管理
* 新增對更新「AD FS 伺服器陣列 SSL 憑證」的支援。
* 新增對管理 AD FS 2016 的支援。
* 您現在可以在安裝 AD FS 時指定現有的 gMSA (群組受管理服務帳戶)。
* 您現在可以設定 sha-256 做為 Azure AD 信賴憑證者信任的 hello 簽章雜湊演算法。

密碼重設
* 導入了改良 tooallow hello 產品 toofunction 在環境中更嚴格的防火牆規則。
* 可靠性 tooAzure Service Bus 改善的連線。

## <a name="113800"></a>1.1.380.0
發行日期︰2016 年 12 月

**修正的問題︰**

* 這個組建中遺失固定的 hello 問題 hello issuerid Active Directory Federation services (AD FS) 宣告規則的位置。

>[!NOTE]
>這個組建不是使用 toocustomers 透過 hello Azure AD 連接自動升級功能。

## <a name="113710"></a>1.1.371.0
發行日期︰2016 年 12 月

**已知問題︰**

* 遺漏這個組建中的 AD FS 的 hello issuerid 宣告規則。 如果您正在同盟與 Azure Active Directory (Azure AD) 的多個網域需要 hello issuerid 宣告規則。 如果您在內部使用 Azure AD Connect toomanage 升級 toothis 組建的 AD FS 部署 AD FS 設定中移除 hello 現有 issuerid 宣告規則。 您可以解決 hello 問題 hello 安裝/升級之後加入 hello issuerid 宣告規則。 詳細資料，需將加入 hello issuerid 宣告規則，請參閱 toothis 發行項上[多重網域支援與 Azure AD 聯盟](active-directory-aadconnect-multiple-domains.md)。

**修正的問題︰**

* 如果尚未開啟連接埠 9090 hello 輸出連線，hello Azure AD Connect 的安裝或升級會失敗。

>[!NOTE]
>這個組建不是使用 toocustomers 透過 hello Azure AD 連接自動升級功能。

## <a name="113700"></a>1.1.370.0
發行日期︰2016 年 12 月

**已知問題︰**

* 遺漏這個組建中的 AD FS 的 hello issuerid 宣告規則。 如果您正在同盟與 Azure AD 的多個網域需要 hello issuerid 宣告規則。 如果您在內部使用 Azure AD Connect toomanage 升級 toothis 組建的 AD FS 部署 AD FS 設定中移除 hello 現有 issuerid 宣告規則。 您可以安裝/升級之後加入 hello issuerid 宣告規則，以解決 hello 問題。 詳細資料，需將加入 issuerid 宣告規則，請參閱 toothis 發行項上[多重網域支援與 Azure AD 聯盟](active-directory-aadconnect-multiple-domains.md)。
* 必須開啟傳出 toocomplete 安裝連接埠 9090。

**新功能︰**

* 傳遞驗證 (預覽)。

>[!NOTE]
>這個組建不是使用 toocustomers 透過 hello Azure AD 連接自動升級功能。

## <a name="113430"></a>1.1.343.0
發行日期：2016 年 11 月

**已知問題︰**

* 遺漏這個組建中的 AD FS 的 hello issuerid 宣告規則。 如果您正在同盟與 Azure AD 的多個網域需要 hello issuerid 宣告規則。 如果您在內部使用 Azure AD Connect toomanage 升級 toothis 組建的 AD FS 部署 AD FS 設定中移除 hello 現有 issuerid 宣告規則。 您可以安裝/升級之後加入 hello issuerid 宣告規則，以解決 hello 問題。 詳細資料，需將加入 issuerid 宣告規則，請參閱 toothis 發行項上[多重網域支援與 Azure AD 聯盟](active-directory-aadconnect-multiple-domains.md)。

**已修正的問題：**

* 有時候，安裝 Azure AD Connect 會失敗，因為它是無法 toocreate 本機服務帳戶的密碼符合 hello 層級的 hello 組織的密碼原則所指定的複雜性。
* 已修正下列問題其中聯結規則就不會重新評估 hello 連接器空間中的物件，同時變成超出範圍時的其中一個聯結規則，並成為範圍內的另一個。 如果有兩個或多個聯結規則的聯結條件互斥，也可能發生此問題。
* 已修正以下問題：相較於包含聯結規則的輸入同步處理規則，如果未包含聯結規則的輸入同步處理規則 (來自 Azure AD) 具有較低的優先順序值，則不會處理未包含聯結規則的輸入同步處理規則。

**改進：**

* 新增了在 Windows Server 2016 標準版或更新版本上安裝 Azure AD Connect 的支援。
* 已新增的支援使用與 hello 遠端資料庫的 SQL Server 2016 的 Azure AD Connect。

## <a name="112810"></a>1.1.281.0
發行日期：2016 年 8 月

**已修正的問題：**

* 變更 toosync 間隔不會直到 hello 之後下一個同步處理週期完成。
* Azure AD Connect 精靈不接受使用者名稱以底線 (\_) 開頭的 Azure AD 帳戶。
* 如果 hello 帳戶密碼包含太多的特殊字元，azure AD Connect 精靈就會失敗 tooauthenticate hello Azure AD 帳戶。 錯誤訊息 「 無法 toovalidate 認證。 已發生未預期的錯誤。 」錯誤訊息。
* 解除安裝開發用伺服器停用 Azure AD 租用戶中的密碼同步處理，則會導致密碼同步處理 toofail 有作用中的伺服器。
* 在罕見的情況下的密碼同步處理失敗，儲存在 hello 使用者沒有密碼雜湊時。
* 當 Azure AD Connect 伺服器啟用預備模式時，不會暫時停用密碼回寫。
* Azure AD Connect 精靈不會顯示 hello 實際的密碼同步處理 」 和 「 密碼回寫設定，當伺服器處於預備模式。 這些一律會顯示為停用。
* 組態變更 toopassword 同步處理 」 和 「 密碼回寫不會保存由 Azure AD Connect 精靈伺服器處於預備模式時。

**改進：**

* 它是否能 toosuccessfully 開始新的同步處理週期或不更新 hello 開始 ADSyncSyncCycle cmdlet tooindicate。
* 加入的 hello 停止 ADSyncSyncCycle cmdlet tooterminate 同步處理週期和作業，也就是目前正在進行中。
* 更新的 hello 停止 ADSyncScheduler cmdlet tooterminate 同步處理週期和作業，也就是目前正在進行中。
* 設定時[目錄延伸模組](active-directory-aadconnectsync-feature-directory-extensions.md)在 Azure AD Connect 精靈中，類型 「 Teletex 字串"hello Azure AD 屬性可以現在都已選取。

## <a name="111890"></a>1.1.189.0
發行日期：2016 年 6 月

**已修正的問題和改進︰**

* Azure AD Connect 現在可以安裝於符合 FIPS 規範的伺服器上。
  * 針對密碼同步處理，請參閱[密碼同步處理和 FIPS](active-directory-aadconnectsync-implement-password-synchronization.md#password-synchronization-and-fips)。
* NetBIOS 名稱與解決的 toohello FQDN hello Active Directory 連接器中無法修正的問題。

## <a name="111800"></a>1.1.180.0
發行日期：2016 年 5 月

**新功能︰**

* 如果您未先驗證網域就執行 Azure AD Connect，系統將會發出警告並協助您驗證網域。
* 已新增對 [Microsoft Cloud Germany](active-directory-aadconnect-instances.md#microsoft-cloud-germany)的支援。
* 新增支援的最新 hello [Microsoft Azure 政府雲端](active-directory-aadconnect-instances.md#microsoft-azure-government-cloud)URL 的新需求的基礎結構。

**已修正的問題和改進︰**

* 加入篩選 toohello 同步處理規則編輯器 toomake 它輕鬆 toofind 同步處理規則。
* 提升刪除連接器空間時的效能。
* 當相同的物件已刪除和加入的 hello hello 執行 （呼叫 delete/加入） 相同，請修正的問題。
* 已停用的同步處理規則不會在升級或目錄結構描述重新整理時，再重新啟用包含的物件和屬性。

## <a name="111300"></a>1.1.130.0
發行日期︰2016 年 4 月

**新功能︰**

* 加入支援多重值屬性太[目錄延伸模組](active-directory-aadconnectsync-feature-directory-extensions.md)。
* 新增多個組態的變化以支援[自動升級](active-directory-aadconnect-feature-automatic-upgrade.md)toobe 視為符合升級資格。
* 已新增一些適用於 [自訂排程器](active-directory-aadconnectsync-feature-scheduler.md#custom-scheduler)的 Cmdlet。

## <a name="111190"></a>1.1.119.0
發行日期︰2016 年 3 月

**已修正的問題：**

* 請確定 Windows Server 2008 (發行前 R2) 上無法使用快速安裝，因為此作業系統不支援密碼同步處理。
* 使用自訂篩選器設定從 DirSync 升級並未如預期般運作。
* 升級 tooa 較新版本時，都沒有變更 toohello 組態，不應該排程完整匯入/同步處理。

## <a name="111100"></a>1.1.110.0
發行日期︰2016 年 2 月

**已修正的問題：**

* 從舊版升級無法運作如果 hello 安裝不在 hello 預設 C:\Program Files 資料夾中。
* 如果您安裝並清除**啟動 hello 同步處理程序**結尾 hello hello 安裝精靈，執行 hello 安裝精靈的第二次將不會啟用 hello 排程器。
* hello 排程器不會如預期般運作，hello us-en 日期/時間格式未使用的伺服器上。 它也會封鎖`Get-ADSyncScheduler`tooreturn 正確時間。
* 如果為 hello 登入選項和升級，您可以安裝與 AD FS 的 Azure AD Connect 先前的版本，您無法再次執行 hello 安裝精靈。

## <a name="111050"></a>1.1.105.0
發行日期︰2016 年 2 月

**新功能︰**

* [Automatic upgrade](active-directory-aadconnect-feature-automatic-upgrade.md) 功能。
* 使用 Azure Multi-factor Authentication Server 和 Privileged Identity Management hello 安裝精靈中的 hello 全域管理員的支援。
  * 您需要 tooallow proxy tooalso 允許流量 toohttps://secure.aadcdn.microsoftonline-p.com，如果您使用多重要素驗證。
  * 您需要多因素驗證 tooproperly 工作 tooadd https://secure.aadcdn.microsoftonline-p.com tooyour 信任的網站清單。
* 允許在初始安裝後變更 hello 使用者的登入方法。
* 允許[網域和 OU 篩選](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering)hello 安裝精靈 中。 這也會讓連接 tooforests 並非所有的定義域才可使用的位置。
* [排程器](active-directory-aadconnectsync-feature-scheduler.md)toohello 同步處理引擎內建。

**從 preview tooGA 升級的功能：**

* [裝置回寫](active-directory-aadconnect-feature-device-writeback.md)。
* [目錄擴充](active-directory-aadconnectsync-feature-directory-extensions.md)。

**新的預覽功能：**

* hello 新預設同步處理週期間隔為 30 分鐘。 用於所有的舊版 toobe 三小時一次。 新增支援 toochange hello[排程器](active-directory-aadconnectsync-feature-scheduler.md)行為。

**已修正的問題：**

* hello，請確認 DNS 網域頁面一律未辨識 hello 網域。
* 設定 ADFS 時，出現網域系統管理員認證提示。
* hello 內部 AD 帳戶將無法辨識的 hello 安裝精靈，如果位於不同的樹狀目錄 DNS 比 hello 根網域的網域。

## <a name="1091310"></a>1.0.9131.0
發行日期︰2015 年 12 月

**已修正的問題：**

* 您變更 Active Directory Domain Services (AD DS) 中的密碼時，密碼同步處理可能會無法作用，但是在您設定密碼時將可作用。
* 當您的 proxy 伺服器，驗證 tooAzure AD 可能無法在安裝期間，或升級取消 hello 組態 頁面上。
* 若您並非 SQL Server 系統管理員 (SA)，從有完整 SQL Server 執行個體的舊版 Azure AD Connect 更新將會失敗。
* 從先前的版本與遠端的 SQL Server 的 Azure AD Connect 的更新會顯示 hello"無法 tooaccess hello ADSync SQL 資料庫 」 錯誤。

## <a name="1091250"></a>1.0.9125.0
發行日期：2015 年 11 月

**新功能︰**

* 可以重新設定 AD FS tooAzure AD 信任。
* 可以重新整理 hello Active Directory 架構，並重新產生同步處理規則。
* 可以停用同步處理規則。
* 可以在同步處理規則中定義 "AuthoritativeNull" 做為新的常值。

**新的預覽功能：**

* [適用於同步的 Azure AD Connect Health](../connect-health/active-directory-aadconnect-health-sync.md)。
* 支援 [Azure AD 網域服務](../active-directory-passwords-update-your-own-password.md) 密碼同步處理。

**新的支援案例：**

* 支援多個內部部署的 Exchange 組織。 如需詳細資訊，請參閱[內含多個 Active Directory 樹系的混合式部署](https://technet.microsoft.com/library/jj873754.aspx)。

**已修正的問題：**

* 密碼同步處理問題：
  * 從範圍外 tooin 範圍移動的物件不會同步處理其密碼。 這包含 OU 及屬性篩選。
  * 選取新的 OU tooinclude 同步，不需要完整密碼同步。
  * 啟用已停用的使用者時就不會同步 hello 密碼。
  * 是無限的 hello 密碼重試佇列並 hello 的 5000 物件 toobe 淘汰先前的限制已經移除。
* 您不能 tooconnect tooActive 目錄與 Windows Server 2016 的樹系功能層級。
* 您不能 toochange hello 用於群組篩選 hello 初始安裝後的群組。
* 不再進行密碼變更已啟用密碼回寫的每個使用者 hello Azure AD Connect 的伺服器上建立新的使用者設定檔。
* 您不能 toouse 長整數值的同步處理規則的範圍。
* 如果無法連線到網域控制站，hello 「 裝置回寫 」 的核取方塊保持已停用。

## <a name="1086670"></a>1.0.8667.0
發行日期：2015 年 8 月

**新功能︰**

* 安裝精靈現在是 Azure AD Connect hello 當地語系化 tooall Windows Server 語言。
* 新增在使用 Azure AD 密碼管理時的帳戶解除鎖定支援。

**已修正的問題：**

* 如果另一位使用者會繼續安裝，而不是第一次啟動 hello 安裝的 hello 人員，azure AD Connect 的安裝精靈會當機。
* 如果先前的解除安裝 Azure AD connect 完全失敗 toouninstall Azure AD Connect 同步處理，則不可能 tooreinstall。
* 無法安裝使用快速安裝，如果 hello 使用者不在 hello hello 樹系根網域，或在非英文版的 Active Directory 已使用的 Azure AD Connect。
* 如果無法解析 hello hello Active Directory 使用者帳戶的 FQDN，會顯示可能造成誤導的錯誤訊息 「 無法 toocommit hello 結構描述 」。
* Hello Active Directory 連接器上使用的 hello 帳戶已變更 hello 精靈以外，如果 hello 精靈會在後續的執行失敗。
* Azure AD Connect，有時會失敗 tooinstall 網域控制站上。
* 如果已加入擴充屬性，則無法啟用和停用「預備模式」。
* 在某些組態中的密碼回寫是因 hello Active Directory 連接器上的密碼錯誤而失敗。
* 如果辨別名稱 (DN) 用於屬性篩選，則無法升級 DirSync。
* 使用密碼重設時，CPU 使用率過高。

**已移除的預覽功能：**

* hello 預覽功能[使用者回寫](active-directory-aadconnect-feature-preview.md#user-writeback)已暫時移除根據從預覽客戶的意見反應。 它就會加入稍後我們已解決 hello 提供意見反應之後。

## <a name="1086410"></a>1.0.8641.0
發行日期：2015 年 6 月

**Azure AD Connect 的最初發行版本。**

已變更的名稱，從 Azure AD Sync tooAzure AD Connect。

**新功能︰**

* [快速設定](active-directory-aadconnect-get-started-express.md)安裝
* 可以[設定 AD FS](active-directory-aadconnect-get-started-custom.md#configuring-federation-with-ad-fs)
* 可以[從 DirSync 升級](active-directory-aadconnect-dirsync-upgrade-get-started.md)
* [防止意外刪除](active-directory-aadconnectsync-feature-prevent-accidental-deletes.md)
* 引入 [預備模式](active-directory-aadconnectsync-operations.md#staging-mode)

**新的預覽功能：**

* [使用者回寫](active-directory-aadconnect-feature-preview.md#user-writeback)
* [群組回寫](active-directory-aadconnect-feature-preview.md#group-writeback)
* [裝置回寫](active-directory-aadconnect-feature-device-writeback.md)
* [目錄擴充](active-directory-aadconnect-feature-preview.md)

## <a name="104940501"></a>1.0.494.0501
發行日期：2015 年 5 月

**新需求︰**

* Azure AD Sync，現在需要 hello.NET Framework 4.5.1 版 toobe 安裝。

**已修正的問題：**

* Azure AD 密碼回寫出現 Azure 服務匯流排連線錯誤。

## <a name="104910413"></a>1.0.491.0413
發行日期︰2015 年 4 月

**已修正的問題和改進︰**

* hello Active Directory 連接器不會處理刪除正確如果 hello 資源回收筒已啟用且 hello 樹系中有多個網域。
* hello Azure Active Directory 連接器匯入作業的 hello 效能已獲得改善。
* 當群組已經超過 hello 成員資格限制 （根據預設，hello 限制設定 too50，000 物件），Azure Active Directory 中的 hello 群組已刪除。 使用新行為 hello，hello 群組不會刪除，會擲回錯誤，且不會匯出新的成員資格變更。
* 如果以 hello 已經是相同 DN 的分段的刪除顯示 hello 連接器空間中，無法佈建一個新的物件。
* 某些物件被標示為差異同步處理期間的同步處理中，即使不沒有在 hello 物件上執行的任何變更。
* 強制執行密碼同步處理時，也會移除 hello 慣用的 DC 清單。
* CSExportAnalyzer 有一些物件狀態的問題。

**新功能︰**

* 聯結現在可以連線太"ANY"hello MV 中的物件類型。

## <a name="104850222"></a>1.0.485.0222
發行日期︰2015 年 2 月

**改進：**

* 改進匯入效能。

**已修正的問題：**

* 密碼同步接受屬性篩選所用的 hello cloudFiltered 屬性。 經過篩選的物件不再於密碼同步處理的範圍中。
* 在 hello 拓撲其中有許多網域控制站的罕見情況下，密碼同步無法運作。
* 「 已停止的伺服器 」 時裝置管理之後從 hello Azure AD 連接器匯入已啟用 Azure AD/Intune。
* 從相同樹系中的多個網域加入外部安全性主體 (FSP) 會造成模稜兩可的加入錯誤。

## <a name="104751202"></a>1.0.475.1202
發行日期︰2014 年 12 月

**新功能︰**

* 現在支援透過以屬性為基礎的篩選進行密碼同步處理。 如需詳細資訊，請參閱[透過篩選進行密碼同步處理](active-directory-aadconnectsync-configure-filtering.md)。
* hello Msds-externaldirectoryobjectid 屬性寫回 tooActive 目錄。 這項功能會新增適用於 Office 365 應用程式的支援。 它會使用 OAuth2 tooaccess 線上和內部部署混合式 Exchange 部署的信箱。

**已修正的升級問題︰**

* Hello 伺服器上使用較新版的 hello 登入小幫手。
* 自訂安裝路徑是使用的 tooinstall Azure AD Sync。
* 無效的自訂加入條件區塊 hello 升級。

**其他修正︰**

* 固定的 hello Office Pro plus 的範本。
* 已修正以破折號開頭的使用者名稱所造成的安裝問題。
* 第二次執行 hello 安裝精靈時，請修正遺失 hello sourceAnchor 設定。
* 已修正密碼同步處理的 ETW 追蹤。

## <a name="104701023"></a>1.0.470.1023
發行日期︰2014 年 10 月

**新功能︰**

* 從多個密碼同步處理內部部署 Active Directory tooAzure AD。
* 當地語系化的安裝 UI tooall Windows Server 語言。

**從 AADSync 1.0 GA 升級**

如果您已經安裝 Azure AD Sync，還有一個額外的步驟，您有 tootake，以防您變更了任何 hello 現成的同步處理規則。 您已升級 toohello 1.0.470.1023 版後，會重複 hello 同步處理規則已修改。 針對每個修改過的同步處理規則，hello 遵循：

1.  找出您已經修改，並記下的 hello 變更 hello 同步處理規則。
* 刪除 hello 同步處理規則。
* 找出 hello 新同步處理規則所建立的 Azure AD Sync，然後重新套用 hello 變更。

**Hello Active Directory 帳戶的權限**

hello Active Directory 帳戶必須從 Active Directory 授與其他權限 toobe 無法 tooread hello 密碼雜湊。 hello 權限 toogrant 名為"複寫目錄變更 」 和 「 複寫目錄變更所有。 」 這兩個權限是必要的 toobe 無法 tooread hello 密碼雜湊。

## <a name="104190911"></a>1.0.419.0911
發行日期︰2014 年 9 月

**Azure AD Sync 的最初發行版本。**

## <a name="next-steps"></a>後續步驟
深入了解 [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)。
