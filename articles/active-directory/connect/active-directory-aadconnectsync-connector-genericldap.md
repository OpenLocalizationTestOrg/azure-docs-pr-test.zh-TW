---
title: "一般 LDAP 連接器 | Microsoft Docs"
description: "本文說明如何設定 Microsoft 的一般 LDAP 連接器。"
services: active-directory
documentationcenter: 
author: billmath
manager: mtillman
editor: 
ms.assetid: 984beeb0-4d91-4908-ad81-c19797c4891b
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 6e2b7d23162673f0c66b1fd6c654336da42b8f6e
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/18/2018
---
# <a name="generic-ldap-connector-technical-reference"></a>一般 LDAP 連接器技術參考
本文說明一般 LDAP 連接器。 本文適用於下列產品：

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * 必須使用 Hotfix 4.1.3671.0 或更新版本 [KB3092178](https://support.microsoft.com/kb/3092178)。

對於 MIM2016 和 FIM2010R2，可以從 [Microsoft 下載中心](http://go.microsoft.com/fwlink/?LinkId=717495)下載此連接器。

提到 IETF RFC 時，本文件會使用 (RFC [RFC 編號]/[RFC 文件中的區段]) 格式，例如：(RFC 4512/4.3)。
您可以在 http://tools.ietf.org/html/rfc4500 找到詳細資訊 (您需要以正確的 RFC 編號取代 4500)。

## <a name="overview-of-the-generic-ldap-connector"></a>一般 LDAP 連接器概觀
一般 LDAP 連接器可讓您整合同步處理服務與 LDAP v3 伺服器。

IETF RFC 中未指定某些作業和結構描述項目，例如需要執行差異匯入的項目。 對於這些作業，只支援明確指定的 LDAP 目錄。

目前的連接器版本大致支援下列功能：

| 功能 | 支援 |
| --- | --- |
| 連接的資料來源 |此連接器支援所有 LDAP v3 伺服器 (RFC 4510 相容)。 此連接器已進行下列各項的測試： <li>Microsoft Active Directory Lightweight Directory Services (AD LDS)</li><li>Microsoft Active Directory Global Catalog (AD GC)</li><li>389 Directory Server</li><li>Apache Directory Server</li><li>IBM Tivoli DS</li><li>Isode Directory</li><li>NetIQ eDirectory</li><li>Novell eDirectory</li><li>Open DJ</li><li>Open DS</li><li>Open LDAP (openldap.org)</li><li>Oracle (之前為 Sun) Directory Server Enterprise Edition</li><li>RadiantOne Virtual Directory Server (VDS)</li><li>Sun One Directory Server</li>**不支援值得注意的目錄：** <li>Active Directory Domain Services (AD DS) [改為使用內建的 Active Directory 連接器]</li><li>Oracle Internet Directory (OID)</li> |
| 案例 |<li>物件生命週期管理</li><li>群組管理</li><li>密碼管理</li> |
| 作業 |所有 LDAP 目錄都支援下列作業： <li>完整匯入</li><li>匯出</li>僅在特定目錄上支援下列作業：<li>差異匯入</li><li>設定密碼、變更密碼</li> |
| 結構描述 |<li>從 LDAP 結構描述 (RFC3673 和 RFC4512/4.2) 中偵測到結構描述</li><li>支援結構化類別、aux 類別和 extensibleObject 物件類別 (RFC4512/4.3)</li> |

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

### <a name="prerequisites"></a>先決條件
在您使用連接器之前，請確定同步處理伺服器上有下列項目：

* Microsoft .NET 4.5.2 Framework 或更新版本

### <a name="detecting-the-ldap-server"></a>偵測 LDAP 伺服器
連接器會依賴各種技巧來偵測和識別 LDAP 伺服器。 連接器會使用根 DSE、廠商名稱/版本，而且檢查結構描述，以找出已知存在某些 LDAP 伺服器中的唯一物件和屬性。 如果找到此資料，則會用來預先填入連接器的設定選項。

### <a name="connected-data-source-permissions"></a>連接的資料來源權限
若要在連接的目錄中的物件上執行匯入及匯出作業，連接器帳戶必須具有足夠的權限。 連接器需要寫入權限才能匯出，需要讀取權限才能匯入。 權限設定是在目標目錄本身的管理經驗內執行。

### <a name="ports-and-protocols"></a>連接埠和通訊協定
連接器會使用組態中指定的連接埠號碼，依預設 LDAP 使用 389 及 LDAPS 使用 636 。

對於 LDAPS，您必須使用 SSL 3.0 或 TLS。 不支援 SSL 2.0，而且無法啟用。

### <a name="required-controls-and-features"></a>必要的控制項和功能
LDAP 伺服器必須提供下列 LDAP 控制項/功能，連接器才能正常運作：  
`1.3.6.1.4.1.4203.1.5.3` True/False 篩選器

True/False 篩選器通常因為由 LDAP 目錄所支援而不回報，而且可能會出現在 [找不到強制功能] 之下的 [全域頁面] 上。 它用於在 LDAP 查詢中建立 **OR** 篩選器，例如，當匯入多個物件類型時。 如果您可以匯入一種以上的物件類型，則 LDAP 伺服器會支援此功能。

如果您使用的目錄中有唯一識別碼是錨點，則也必須提供下列項目 (如需詳細資訊，請參閱[設定錨點](#configure-anchors)一節)：  
`1.3.6.1.4.1.4203.1.5.1` 所有操作屬性

如果目錄中的物件數目超過在一次呼叫目錄時可容納的數目，則建議使用分頁。 您需使用下列其中一個選項，分頁才能運作：

**選項 1：**  
`1.2.840.113556.1.4.319` pagedResultsControl

**選項 2：**  
`2.16.840.1.113730.3.4.9` VLVControl  
`1.2.840.113556.1.4.473` SortControl

如果連接器組態中已啟用這兩個選項，則會使用 pagedResultsControl。

`1.2.840.113556.1.4.417` ShowDeletedControl

只有在 ShowDeletedControl 搭配 USNChanged 差異匯入方法使用時，才能夠查看已刪除的物件。

連接器會嘗試偵測選項是否出現在伺服器上。 如果偵測不到選項，則連接器屬性的 [全域] 頁面上會出現警告。 並非所有 LDAP 伺服器都會顯示其支援的所有控制項/功能，即使出現此警告，連接器也可能正常運作。

### <a name="delta-import"></a>差異匯入
只有在偵測到支援目錄時，才可使用差異匯入。 目前使用下列方法：

* LDAP Accesslog。 請參閱 [http://www.openldap.org/doc/admin24/overlays.html#Access Logging](http://www.openldap.org/doc/admin24/overlays.html#Access Logging)
* LDAP Changelog。 請參閱 [http://tools.ietf.org/html/draft-good-ldap-changelog-04](http://tools.ietf.org/html/draft-good-ldap-changelog-04)
* TimeStamp。 對於 Novell/NetIQ eDirectory，連接器會使用最後的日期/時間來取得已建立和更新的物件。 Novell/NetIQ eDirectory 不提供對等方法來擷取已刪除的物件。 如果 LDAP 伺服器上沒有其他作用中的差異匯入方法，也可以使用此選項。 此選項無法匯入已刪除的物件。
* USNChanged。 請參閱： [https://msdn.microsoft.com/library/ms677627.aspx](https://msdn.microsoft.com/library/ms677627.aspx)

### <a name="not-supported"></a>不支援
不支援下列 LDAP 功能：

* 伺服器之間的 LDAP 轉介 (RFC 4511/4.1.10)

## <a name="create-a-new-connector"></a>建立新的連接器
若要建立一般 LDAP 連接器，請在 [同步處理服務] 中選取 [管理代理程式] 和 [建立]。 選取 [一般 LDAP (Microsoft)] 連接器。

![CreateConnector](./media/active-directory-aadconnectsync-connector-genericldap/createconnector.png)

### <a name="connectivity"></a>連線能力
在 [連線能力] 頁面上，您必須指定 [主機]、[連接埠] 和 [繫結] 資訊。 視選取的 [繫結] 而定，下列各區段中可能會提供其他資訊。

![連線能力](./media/active-directory-aadconnectsync-connector-genericldap/connectivity.png)

* [連線逾時] 設定僅適用於偵測結構描述時的第一次伺服器連線。
* 如果 [繫結] 為 [匿名]，則不會使用使用者名稱 / 密碼或憑證。
* 對於其他繫結，請在使用者名稱 / 密碼中輸入資訊或選取憑證。
* 如果您使用 Kerberos 進行驗證，也要提供使用者的 [領域/網域]。

[屬性別名]  文字方塊使用於以 RFC4522 語法在結構描述中定義的屬性。 在結構描述偵測期間無法偵測這些屬性，而連接器需要協助才能識別這些屬性。 例如，必須在 [屬性別名] 方塊中輸入下列項目，才能正確地將 userCertificate 屬性識別為二進位屬性：

`userCertificate;binary`

以下是此組態的顯示範例：

![連線能力](./media/active-directory-aadconnectsync-connector-genericldap/connectivityattributes.png)

選取 [在結構描述中包含操作屬性]  核取方塊，也會包含伺服器所建立的屬性。 其中包含物件的建立時間和上次更新時間等屬性。

若已使用可延伸物件 (RFC4512/4.3)，則選取 [在結構描述中包含可延伸屬性]  ，而且啟用此選項可讓每個屬性使用於所有物件上。 選取此選項會讓結構描述變得非常大，所以除非連接的目錄使用這項功能，否則建議不要選取這個選項。

### <a name="global-parameters"></a>全域參數
在 [全域參數] 頁面上，您可以設定差異變更記錄檔的 DN 和其他 LDAP 功能。 此頁面會預先填入以 LDAP 伺服器所提供的資訊。

![連線能力](./media/active-directory-aadconnectsync-connector-genericldap/globalparameters.png)

最上方區段顯示伺服器本身所提供的資訊，例如伺服器名稱。 連接器也會確認強制控制項是否位於根 DSE 中。 如果未列出這些控制項，則會顯示一則警告。 某些 LDAP 目錄不會列出根 DSE 中的所有功能，而即使出現警告，連接器也可能正常運作。

[支援的控制項]  核取方塊可控制特定作業的行為：

* 選取樹狀目錄刪除後，會透過一個 LDAP 呼叫來刪除階層。 若未選取樹狀目錄刪除，則連接器會視需要進行遞迴刪除。
* 選取分頁結果後，連接器會以執行步驟上指定的大小進行分頁匯入。
* VLVControl 和 SortControl 是 pagedResultsControl 的替代項目，可從 LDAP 目錄讀取資料。
* 如果三個選項 (pagedResultsControl、VLVControl 和 SortControl) 均未選取，則連接器會在一項作業中匯入所有物件，而如果是大型目錄，則有可能失敗。
* 只有在差異匯入方法是 USNChanged 時，才會使用 ShowDeletedControl。

變更記錄檔 DN 是差異變更記錄檔所使用的命名內容，例如 **cn=discovery**。 必須指定此值，才能夠進行差異匯入。

以下是預設變更記錄檔 DN 清單：

| 目錄 | 差異變更記錄檔 |
| --- | --- |
| Microsoft AD LDS 和 AD GC |自動偵測。 USNChanged。 |
| Apache Directory Server |無法使用。 |
| Directory 389 |變更記錄檔。 要使用的預設值： **cn=changelog** |
| IBM Tivoli DS |變更記錄檔。 要使用的預設值： **cn=changelog** |
| Isode Directory |變更記錄檔。 要使用的預設值： **cn=changelog** |
| Novell/NetIQ eDirectory |無法使用。 TimeStamp。 連接器會使用上次更新日期/時間來取得已新增和更新的記錄。 |
| Open DJ/DS |變更記錄檔。  要使用的預設值： **cn=changelog** |
| Open LDAP |存取記錄檔。 要使用的預設值： **cn=accesslog** |
| Oracle DSEE |變更記錄檔。 要使用的預設值： **cn=changelog** |
| RadiantOne VDS |虛擬目錄。 取決於 VDS 連接的目錄。 |
| Sun One Directory Server |變更記錄檔。 要使用的預設值： **cn=changelog** |

密碼屬性是連接器在密碼變更和密碼設定作業中應用來設定密碼的屬性名稱。
此值預設為 **userPassword** ，但特定 LDAP 系統可以視需要進行變更。

在其他資料分割清單中，可以新增其他未自動偵測到的命名空間。 比方說，如果有幾部應同時全部匯入的伺服器組成一個邏輯叢集，則可使用此設定。 就如同 Active Directory 可以在一個樹系中有多個網域，而所有網域都共用一個結構描述，在此方塊中輸入其他命名空間就可以模擬此狀況。 每個命名空間都可以從不同的伺服器匯入，並可在 [設定資料分割和階層] 頁面上進一步設定。 使用 Ctrl+Enter 來換行。

### <a name="configure-provisioning-hierarchy"></a>設定佈建階層
此頁面用於將 DN 元件 (例如 OU) 對應至應該佈建的物件類型 (例如 organizationalUnit)。

![佈建階層](./media/active-directory-aadconnectsync-connector-genericldap/provisioninghierarchy.png)

藉由設定佈建階層，您可以設定連接器在必要時自動建立結構。 例如，如果有命名空間 dc=contoso,dc=com 並已佈建一個新物件 (cn=Joe、ou=Seattle、c=US、dc=contoso、dc=com)，則連接器可以建立國家類型為美國而 organizationalUnit 為西雅圖的物件 (如果目錄中尚未出現這些項目)。

### <a name="configure-partitions-and-hierarchies"></a>設定資料分割和階層
在資料分割和階層頁面上，選取具有您打算匯入和匯出之物件的所有命名空間。

![分割數](./media/active-directory-aadconnectsync-connector-genericldap/partitions.png)

對於每個命名空間，也可以設定連線能力設定，以覆寫 [連線能力] 畫面上指定的值。 如果這些值保留為其預設的空白值，則會使用 [連線能力] 畫面中的資訊。

此外，也可以選取連接器應匯入及匯出的容器和 OU。

在執行搜尋時，這會對資料分割中的所有容器執行。 在有大量容器的情況下，這種行為會導致效能降低。

>[!NOTE]
從 2017 年 3 月的一般 LDAP 連接器更新開始，您已可將搜尋範圍限制在所選容器內。 藉由選取下圖所示的 [僅在所選容器中搜尋] 核取方塊，就能執行此操作。

![僅搜尋所選容器](./media/active-directory-aadconnectsync-connector-genericldap/partitions-only-selected-containers.png)

### <a name="configure-anchors"></a>設定錨點
此頁面一定有預先設定的值，而且無法變更。 如果已識別出伺服器廠商，則錨點可能會填入不可變的屬性，例如物件的 GUID。 如果尚未偵測到或已知沒有不可變的屬性，則連接器會使用 dn (辨別名稱) 做為錨點。

![錨點](./media/active-directory-aadconnectsync-connector-genericldap/anchors.png)


以下是 LDAP 伺服器清單和所使用的錨點：

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
本節提供此連接器特用層面的資訊，或因為其他原因而需得知的重要資訊。

### <a name="delta-import"></a>差異匯入
Open LDAP 中的差異浮水印是 UTC 日期/時間。 基於這個理由，FIM 同步處理服務與 Open LDAP 之間的時鐘必須同步。 如果沒有同步，則可能會省略差異變更記錄檔中的某些項目。

對於 Novell eDirectory，差異匯入不會偵測任何物件刪除。 基於這個理由，必須定期執行完整匯入才可找到所有刪除的物件。

對於差異變更記錄檔以日期 / 時間為基礎的目錄，強烈建議定期執行完整匯入。 此程序可讓同步處理引擎找出 LDAP 伺服器與連接器空間中目前內容之間的差異。

## <a name="troubleshooting"></a>疑難排解
* 如需如何啟用記錄來疑難排解連接器的資訊，請參閱 [如何啟用連接器的 ETW 追蹤](http://go.microsoft.com/fwlink/?LinkId=335731)。
