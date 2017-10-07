---
title: "aaaGeneric LDAP 連接器 |Microsoft 文件"
description: "本文說明如何 tooconfigure Microsoft 泛型 LDAP 連接器。"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 984beeb0-4d91-4908-ad81-c19797c4891b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 25031b4da196bd073902b04b0705762bfa0118b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="generic-ldap-connector-technical-reference"></a>一般 LDAP 連接器技術參考
本文說明 hello 泛型 LDAP 連接器。 hello 文章適用 toohello 下列產品：

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * 必須使用 Hotfix 4.1.3671.0 或更新版本 [KB3092178](https://support.microsoft.com/kb/3092178)。

MIM2016 和 FIM2010R2，hello 連接器可做為從 hello 下載[Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495)。

這份文件參考時 tooIETF Rfc，使用 hello 格式 (RFC [RFC number] / [一節中 RFC 文件])，例如 (RFC 4512/4.3)。
您可以在 http://tools.ietf.org/html/rfc4500 （您將需要與 hello 正確 RFC number tooreplace 4500） 中找到詳細資訊。

## <a name="overview-of-hello-generic-ldap-connector"></a>Hello 泛型 LDAP 連接器的概觀
hello 泛型 LDAP 連接器可讓您 toointegrate hello 同步處理服務與 LDAP v3 伺服器。

特定作業和結構描述項目，例如那些需要 tooperform 差異匯入，未指定在 hello IETF Rfc 中。 對於這些作業，只支援明確指定的 LDAP 目錄。

從高階觀點來看，hello hello 連接器目前版本支援下列功能的 hello:

| 功能 | 支援 |
| --- | --- |
| 連接的資料來源 |hello 連接器僅支援所有的 LDAP v3 伺服器 (符合 RFC 4510)。 經過 hello 下列測試： <li>Microsoft Active Directory Lightweight Directory Services (AD LDS)</li><li>Microsoft Active Directory Global Catalog (AD GC)</li><li>389 Directory Server</li><li>Apache Directory Server</li><li>IBM Tivoli DS</li><li>Isode Directory</li><li>NetIQ eDirectory</li><li>Novell eDirectory</li><li>Open DJ</li><li>Open DS</li><li>Open LDAP (openldap.org)</li><li>Oracle (之前為 Sun) Directory Server Enterprise Edition</li><li>RadiantOne Virtual Directory Server (VDS)</li><li>Sun One Directory Server</li>**不支援值得注意的目錄：** <li>Microsoft Active Directory 網域服務 (AD DS) [使用 hello 內建的 Active Directory 連接器改用]</li><li>Oracle Internet Directory (OID)</li> |
| 案例 |<li>物件生命週期管理</li><li>群組管理</li><li>密碼管理</li> |
| 作業 |所有的 LDAP 目錄上支援下列作業的 hello: <li>完整匯入</li><li>匯出</li>在指定的目錄上才支援 hello 下列作業：<li>差異匯入</li><li>設定密碼、變更密碼</li> |
| 結構描述 |<li>Hello LDAP 結構描述 （RFC3673 和 RFC4512/4.2） 中偵測到結構描述</li><li>支援結構化類別、aux 類別和 extensibleObject 物件類別 (RFC4512/4.3)</li> |

### <a name="delta-import-and-password-management-support"></a>差異匯入和密碼管理支援
支援差異匯入和密碼管理的目錄：

* Microsoft Active Directory Lightweight Directory Services (AD LDS)
  * 支援所有作業進行差異匯入
  * 支援設定密碼
* Microsoft Active Directory Global Catalog (AD GC)
  * 支援所有作業進行差異匯入
  * 支援設定密碼
* 389 Directory Server
  * 支援所有作業進行差異匯入
  * 支援設定密碼和變更密碼
* Apache Directory Server
  * 不支援差異匯入，因為此目錄沒有持續性的變更記錄檔
  * 支援設定密碼
* IBM Tivoli DS
  * 支援所有作業進行差異匯入
  * 支援設定密碼和變更密碼
* Isode Directory
  * 支援所有作業進行差異匯入
  * 支援設定密碼和變更密碼
* Novell eDirectory 和 NetIQ eDirectory
  * 支援 [新增]、[更新] 和 [重新命名] 作業進行差異匯入
  * 不支援 [刪除] 作業進行差異匯入
  * 支援設定密碼和變更密碼
* Open DJ
  * 支援所有作業進行差異匯入
  * 支援設定密碼和變更密碼
* Open DS
  * 支援所有作業進行差異匯入
  * 支援設定密碼和變更密碼
* Open LDAP (openldap.org)
  * 支援所有作業進行差異匯入
  * 支援設定密碼
  * 不支援變更密碼
* Oracle (之前為 Sun) Directory Server Enterprise Edition
  * 支援所有作業進行差異匯入
  * 支援設定密碼和變更密碼
* RadiantOne Virtual Directory Server (VDS)
  * 必須使用 7.1.1 版或更高版本
  * 支援所有作業進行差異匯入
  * 支援設定密碼和變更密碼
* Sun One Directory Server
  * 支援所有作業進行差異匯入
  * 支援設定密碼和變更密碼

### <a name="prerequisites"></a>必要條件
使用 hello 連接器之前，請確定您擁有 hello 同步處理伺服器 hello 下列項目：

* Microsoft .NET 4.5.2 Framework 或更新版本

### <a name="detecting-hello-ldap-server"></a>偵測 hello LDAP 伺服器
hello 連接器依賴各種技術 toodetect，並找出 hello LDAP 伺服器。 hello 連接器使用 hello 根目錄 DSE，廠商名稱/版本，而且它會檢驗 hello 架構 toofind 唯一物件和已知 tooexist 中特定的 LDAP 伺服器的屬性。 這項資料，如果找到，是使用的 toopre-填入 hello 連接器中的 hello 組態選項。

### <a name="connected-data-source-permissions"></a>連接的資料來源權限
tooperform 匯入和匯出 hello 連接的目錄中的 hello 物件上的作業，hello 連接器的帳戶必須擁有足夠的權限。 hello 連接器需要寫入權限 toobe 無法 tooexport 和讀取權限 toobe 無法 tooimport。 Hello 管理經驗的 hello 目標目錄本身內執行權限組態。

### <a name="ports-and-protocols"></a>連接埠和通訊協定
hello 連接器使用 hello hello 組態，其預設值是 389 LDAP 和 636 LDAPS 如中所指定的連接埠號碼。

對於 LDAPS，您必須使用 SSL 3.0 或 TLS。 不支援 SSL 2.0，而且無法啟用。

### <a name="required-controls-and-features"></a>必要的控制項和功能
hello 下列 LDAP 控制項/功能上必須要有 hello 連接器 toowork 的 hello LDAP 伺服器正確：  
`1.3.6.1.4.1.4203.1.5.3` True/False 篩選器

hello True/False 篩選不常報告為 LDAP 目錄支援和可能會出現在 hello**全域頁面**下**強制功能找不到**。 它是使用的 toocreate**或**中 LDAP 查詢篩選條件，例如，當匯入多個物件類型。 如果您可以匯入一種以上的物件類型，則 LDAP 伺服器會支援此功能。

如果您使用的唯一識別碼的所在目錄 hello 錨點 hello 下列也必須提供使用 (如需詳細資訊，請參閱 hello[設定錨點](#configure-anchors)> 一節):  
`1.3.6.1.4.1.4203.1.5.1` 所有操作屬性

如果 hello 目錄有比在一個呼叫 toohello 目錄中容納更多的物件，然後建議 toouse 分頁。 分頁 toowork，您需要一個 hello 下列選項：

**選項 1：**  
`1.2.840.113556.1.4.319` pagedResultsControl

**選項 2：**  
`2.16.840.1.113730.3.4.9` VLVControl  
`1.2.840.113556.1.4.473` SortControl

如果 hello 連接器組態中，會啟用這兩個選項，則會使用 pagedResultsControl。

`1.2.840.113556.1.4.417` ShowDeletedControl

ShowDeletedControl 只能搭配 hello USNChanged 差異匯入方法 toobe 無法 toosee 刪除物件。

hello 連接器會嘗試 toodetect hello 存在 hello 伺服器選項。 如果無法偵測 hello 選項，警告的 hello 全域頁面並 hello 連接器內容中。 並非所有的 LDAP 伺服器存在所有控制項/功能支援，而且即使這個警告已存在，hello 連接器可能都運作而不發生問題。

### <a name="delta-import"></a>差異匯入
只有在偵測到支援目錄時，才可使用差異匯入。 目前用於 hello 下列方法：

* LDAP Accesslog。 請參閱 [http://www.openldap.org/doc/admin24/overlays.html#Access Logging](http://www.openldap.org/doc/admin24/overlays.html#Access Logging)
* LDAP Changelog。 請參閱 [http://tools.ietf.org/html/draft-good-ldap-changelog-04](http://tools.ietf.org/html/draft-good-ldap-changelog-04)
* TimeStamp。 Novell/NetIQ eDirectory 的 hello 連接器會使用最後一個日期/時間 tooget 會建立及更新的物件。 Novell/NetIQ eDirectory 不提供對等項目表示 tooretrieve 刪除物件。 如果沒有其他差異匯入方法為作用中的 hello LDAP 伺服器上，可以也使用此選項。 這個選項不能 tooimport 刪除物件。
* USNChanged。 請參閱： [https://msdn.microsoft.com/library/ms677627.aspx](https://msdn.microsoft.com/library/ms677627.aspx)

### <a name="not-supported"></a>不支援
不支援下列 LDAP 功能的 hello:

* 伺服器之間的 LDAP 轉介 (RFC 4511/4.1.10)

## <a name="create-a-new-connector"></a>建立新的連接器
tooCreate Generic LDAP 連接器，請在**同步處理服務**選取**管理代理程式**和**建立**。 選取 hello **Generic LDAP (Microsoft)**連接器。

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericldap/createconnector.png)

### <a name="connectivity"></a>連線能力
在 hello 連線能力 頁面上，您必須指定 hello 主機、 連接埠和繫結資訊。 視繫結已選取，其他則可能會提供 hello 下列各節中的資訊。

![連線能力](./media/active-directory-aadconnectsync-connector-genericldap/connectivity.png)

* hello 連接逾時設定只用於第一個連接 toohello 伺服器 hello 時偵測 hello 結構描述。
* 如果 [繫結] 為 [匿名]，則不會使用使用者名稱 / 密碼或憑證。
* 對於其他繫結，請在使用者名稱 / 密碼中輸入資訊或選取憑證。
* 如果您使用 Kerberos tooauthenticate，也提供 hello hello 使用者領域/網域。

hello**屬性別名**文字方塊用於 hello RFC4522 語法的結構描述中定義的屬性。 這些屬性無法偵測到結構描述偵測期間和 hello 連接器需要協助 tooidentify 那些屬性。 比方說 hello hello 屬性別名方塊 toocorrectly 必須輸入下列識別 hello userCertificate 屬性做為二進位屬性：

`userCertificate;binary`

hello 的範例如下的這項設定可能的模樣：

![連線能力](./media/active-directory-aadconnectsync-connector-genericldap/connectivityattributes.png)

選取 hello**包含結構描述中的操作屬性**核取方塊 tooalso 包含 hello 伺服器所建立的屬性。 這些包括 hello 物件時所建立和上次更新時間 」 等屬性。

選取**包括可延伸的屬性結構描述中**如果可延伸的物件 (RFC4512/4.3) 用和啟用此選項可讓所有的物件上使用每個屬性 toobe。 選取此選項會 hello 結構描述非常大以便讓這個功能 hello 建議除非使用 hello 連接的目錄是 tookeep hello 選項未選取。

### <a name="global-parameters"></a>全域參數
在 hello 全域參數頁面上，您可以設定 hello DN toohello 差異變更記錄檔和其他 LDAP 功能。 hello 頁面都會預先填入的 hello hello LDAP 伺服器所提供的資訊。

![連線能力](./media/active-directory-aadconnectsync-connector-genericldap/globalparameters.png)

hello 頂部區段會顯示 hello 伺服器本身，例如 hello 伺服器 hello 名稱所提供的資訊。 hello 連接器也會確認 hello 強制控制項有 hello 根目錄 DSE 中。 如果未列出這些控制項，則會顯示一則警告。 某些 LDAP 目錄不會列出 hello 根目錄 DSE 中的所有功能，就有可能 hello 連接器運作，而不發生問題，即使有警告是。

hello**支援控制項**核取方塊來控制特定作業的 hello 行為：

* 選取樹狀目錄刪除後，會透過一個 LDAP 呼叫來刪除階層。 與樹狀目錄中刪除未選取，hello 連接器視執行遞迴刪除。
* 選取分頁的結果，與 hello 連接器用途 hello 大小上執行的 hello 步驟指定分頁匯入。
* hello VLVControl 和 SortControl 是替代 toohello pagedResultsControl tooread 資料從 hello LDAP 目錄。
* 如果未選取所有三個選項 (pagedResultsControl，VLVControl 和 SortControl) 然後 hello 連接器匯入所有物件在一個作業中，如果是大型的目錄可能會失敗。
* ShowDeletedControl 只用 USNChanged hello 差異匯入方法時。

hello 變更記錄 DN 是 hello 例如 hello 差異變更記錄檔所使用的命名內容**cn = 變更記錄**。 此值必須是指定 toobe 無法 toodo 差異匯入。

hello 以下是一份變更記錄檔預設 DNs:

| 目錄 | 差異變更記錄檔 |
| --- | --- |
| Microsoft AD LDS 和 AD GC |自動偵測。 USNChanged。 |
| Apache Directory Server |無法使用。 |
| Directory 389 |變更記錄檔。 預設值 toouse: **cn = 變更記錄** |
| IBM Tivoli DS |變更記錄檔。 預設值 toouse: **cn = 變更記錄** |
| Isode Directory |變更記錄檔。 預設值 toouse: **cn = 變更記錄** |
| Novell/NetIQ eDirectory |無法使用。 TimeStamp。 hello 連接器會使用上次更新的日期/時間 tooget 加入，並更新記錄。 |
| Open DJ/DS |變更記錄檔。  預設值 toouse: **cn = 變更記錄** |
| Open LDAP |存取記錄檔。 預設值 toouse: **cn = accesslog** |
| Oracle DSEE |變更記錄檔。 預設值 toouse: **cn = 變更記錄** |
| RadiantOne VDS |虛擬目錄。 Hello 連接目錄 tooVDS 而定。 |
| Sun One Directory Server |變更記錄檔。 預設值 toouse: **cn = 變更記錄** |

hello 密碼屬性是 hello hello 屬性 hello 連接器名稱應該使用 tooset hello 密碼變更密碼和密碼設定作業中。
此值預設會設定太**userPassword**但需要特定的 LDAP 系統時，可以變更。

Hello 額外的磁碟分割在清單中，就不會自動偵測到可能 tooadd 其他命名空間。 例如，使用此設定數部伺服器組成邏輯叢集中，應該匯入所有在 hello 若相同的時間。 就像 Active Directory 可以在樹系中有多個網域，但所有定義域都共用一個結構描述，可以在此方塊中輸入 hello 其他命名空間在模擬相同的 hello。 每個命名空間可以從不同的伺服器匯入，且進一步 hello 設定分割和階層 頁面上的設定。 使用 Ctrl + Enter tooget 新行。

### <a name="configure-provisioning-hierarchy"></a>設定佈建階層
此頁面是使用的 toomap hello DN 元件，例如 OU toohello 物件型別應該佈建，例如 organizationalUnit。

![佈建階層](./media/active-directory-aadconnectsync-connector-genericldap/provisioninghierarchy.png)

藉由設定佈建階層，您可以設定 hello 連接器 tooautomatically 建立時所需的結構。 比方說，如果沒有命名空間 dc = contoso，dc = com 和新的物件 cn = Joe，ou = 西雅圖，c = US，dc = contoso，dc = com 已佈建，然後 hello 連接器可以建立的型別國家/地區為美國和 organizationalUnit Seattle 的物件，如果這些不是已hello 目錄中。

### <a name="configure-partitions-and-hierarchies"></a>設定資料分割和階層
在 hello 資料分割和階層] 頁面上，選取 [所有命名空間與物件規劃 tooimport 和匯出。

![分割數](./media/active-directory-aadconnectsync-connector-genericldap/partitions.png)

對於每個命名空間，所以也可能 tooconfigure 連線設定，就會覆寫 hello hello 連線能力畫面上指定的值。 如果這些值保留 tootheir 預設空白值，則會使用從 hello 連線能力畫面 hello 資訊。

它也是可能 tooselect 連接器的容器和 Ou hello 應該從匯入和匯出至。

執行搜尋時是 hello 資料分割中的所有容器。 萬一這個行為在有大量的容器會導致 tooperformance 降低。

>[!NOTE]
從開始 hello 2017 年 3 月更新 toohello Generic LDAP 連接器搜尋可限制範圍 tooonly hello 選取容器中。 Hello 圖所示選取 '只能在所選容器中搜尋' hello 核取方塊可以完成此動作。

![僅搜尋所選容器](./media/active-directory-aadconnectsync-connector-genericldap/partitions-only-selected-containers.png)

### <a name="configure-anchors"></a>設定錨點
此頁面一定有預先設定的值，而且無法變更。 如果已經識別 hello 伺服器廠商，hello 錨點可能會填入且不可變的屬性，如範例 hello GUID 物件。 如果它偵測不到或已知 toonot 不可變的屬性，則 hello 連接器 hello 錨點使用 dn （辨別名稱）。

![錨點](./media/active-directory-aadconnectsync-connector-genericldap/anchors.png)


hello 以下是 LDAP 伺服器和 hello 錨點所使用的清單：

| 目錄 | 錨點屬性 |
| --- | --- |
| Microsoft AD LDS 和 AD GC |objectGUID |
| 389 Directory Server |dn |
| Apache Directory |dn |
| IBM Tivoli DS |dn |
| Isode Directory |dn |
| Novell/NetIQ eDirectory |GUID |
| Open DJ/DS |dn |
| Open LDAP |dn |
| Oracle ODSEE |dn |
| RadiantOne VDS |dn |
| Sun One Directory Server |dn |

## <a name="other-notes"></a>其他注意事項
本章節提供特定 toothis 連接器或因為其他原因而重要 tooknow 方面的資訊。

### <a name="delta-import"></a>差異匯入
在 LDAP 中開啟的 hello 差異浮水印是 UTC 日期/時間。 基於這個理由，FIM 同步處理服務與 hello Open LDAP 之間 hello 時鐘必須同步處理。 如果沒有，則可能會省略 hello 差異變更記錄檔中的某些項目。

Novell eDirectory hello 差異匯入沒有偵測的任何物件刪除。 基於這個理由，則需要 toorun 完整定期匯入 toofind 刪除所有物件。

如目錄與差異變更日期/時間為基礎的記錄檔，強烈建議 toorun 完整匯入在定期的時間。 這個程序允許 hello 同步處理引擎 toofind 和還是之間 hello LDAP 伺服器目前是 hello 連接器空間中。

## <a name="troubleshooting"></a>疑難排解
* 如需如何 tooenable 記錄 tootroubleshoot hello 連接器資訊，請參閱 hello[如何 tooEnable ETW 追蹤連接器](http://go.microsoft.com/fwlink/?LinkId=335731)。
