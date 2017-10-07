---
title: "aaaLotus Domino 連接器 |Microsoft 文件"
description: "本文說明如何 tooconfigure Microsoft Lotus Domino 連接器。"
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: e07fd469-d862-470f-a3c6-3ed2a8d745bf
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: affef1fec91eb39f7e91ec274fdd1b3a9c4a32fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="lotus-domino-connector-technical-reference"></a>Lotus Domino 連接器技術參考
本文說明 hello Lotus Domino 連接器。 hello 文章適用 toohello 下列產品：

* Microsoft Identity Manager 2016 (MIM2016)
* Forefront Identity Manager 2010 R2 (FIM2010R2)
  * 必須使用 Hotfix 4.1.3671.0 或更新版本 [KB3092178](https://support.microsoft.com/kb/3092178)。

MIM2016 和 FIM2010R2，hello 連接器可做為從 hello 下載[Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=717495)。

## <a name="overview-of-hello-lotus-domino-connector"></a>Hello Lotus Domino 連接器的概觀
hello Lotus Domino 連接器可讓您與 IBM 的 Lotus domino 的連接器伺服器 toointegrate hello 同步處理服務。

從高階觀點來看，hello hello 連接器目前版本支援下列功能的 hello:

| 功能 | 支援 |
| --- | --- |
| 連接的資料來源 |伺服器： <li>Lotus Domino 8.5.x</li><li>Lotus Domino 9.x</li>用戶端：<li>Lotus Domino 8.5.x</li><li>Lotus Notes 9.x</li> |
| 案例 |<li>物件生命週期管理</li><li>群組管理</li><li>密碼管理</li> |
| 作業 |<li>完整和差異匯入</li><li>匯出</li><li>設定和變更 HTTP 密碼</li> |
| 結構描述 |<li>人員 (漫遊使用者、連絡人 (沒有憑證的人員))</li><li>群組</li><li>資源 (資源、空間、線上會議)</li><li>郵寄資料庫</li><li>支援的物件之屬性的動態探索</li> |

hello Lotus Domino 連接器會使用 Lotus Domino 伺服器 hello Lotus Notes 用戶端 toocommunicate。 由於此相依性，必須安裝支援的 Lotus Notes 用戶端 hello 同步處理伺服器上。 hello hello 用戶端和伺服器之間通訊 hello 是透過 hello Lotus 備忘稿.NET Interop (Interop.domino.dll) 介面實作。 這個介面協助 hello hello Microsoft.NET 平台和 Lotus Notes 用戶端之間的通訊，並支援存取 tooLotus Domino 文件和檢視。 差異匯入，所以也可以使用該 hello c + + 原生介面 （取決於選取的 hello 差異匯入方法）。

### <a name="prerequisites"></a>必要條件
使用 hello 連接器之前，請確定您擁有 hello 遵循 hello 同步處理伺服器上的必要條件：

* Microsoft .NET 4.5.2 Framework 或更新版本
* hello Lotus Notes 用戶端必須安裝在您的同步處理伺服器
* hello Lotus Domino 連接器需要 hello 預設 Lotus Domino LDAP 結構描述資料庫 (schema.nsf) toobe hello Domino 目錄伺服器上。 如果不存在，您可以執行或重新啟動 hello LDAP 服務 hello Domino 伺服器上的安裝它。

### <a name="connected-data-source-permissions"></a>連接的資料來源權限
tooperform 任何 hello Lotus Domino 連接器中支援的工作，您必須是下列群組的成員：

* 完整存取權系統管理員
* 系統管理員
* 資料庫系統管理員

hello 下表列出每個作業所需的 hello 權限：

| 作業 | 存取權限 |
| --- | --- |
| Import |<li>讀取公用文件</li><li> 完整存取系統管理員 （當您完整存取系統管理員群組的成員，您會自動擁有 hello 有效存取權 tooin ACL）。</li> |
| 匯出和設定密碼 |有效的存取權： <li>建立文件</li><li>刪除文件</li><li>讀取公用文件</li><li>編寫公用文件</li><li>複寫或複製文件</li>若為匯出作業，您還需要下列角色的 hello: <li>CreateResource</li><li>GroupCreator</li><li>GroupModifier</li><li>UserCreator</li><li>UserModifier</li> |

### <a name="direct-operations-and-adminp"></a>直接作業和 AdminP
作業會直接移 toohello Domino 目錄，或透過 hello AdminP 處理。 hello 下列表格列出所有支援的物件、 作業和 hello 如果適用的話，關聯的實作方法：

**主要通訊錄**

| Object | 建立 | 更新 | 刪除 |
| --- | --- | --- | --- |
| Person |AdminP |直接 |AdminP |
| 群組 |AdminP |直接 |AdminP |
| MailInDB |直接 |直接 |直接 |
| 資源 |AdminP |直接 |AdminP |

**次要通訊錄**

| Object | 建立 | 更新 | 刪除 |
| --- | --- | --- | --- |
| Person |N/A |直接 |直接 |
| 群組 |直接 |直接 |直接 |
| MailInDB |直接 |直接 |直接 |
| 資源 |N/A |N/A |N/A |

建立資源時會建立 Notes 文件。 同樣地，刪除資源時，會刪除 hello 資訊文件。

### <a name="ports-and-protocols"></a>連接埠和通訊協定
IBM Lotus Notes 用戶端和 Domino 伺服器使用 Notes Remote Procedure Call (NRPC) 進行通訊，其中 NRPC 應使用 TCP/IP。 hello 預設連接埠號碼是 1352，但可以由 hello Domino 管理員變更。

### <a name="not-supported"></a>不支援
hello hello Lotus Domino 連接器目前版本不支援下列作業的 hello:

* 在伺服器之間移動信箱。

## <a name="create-a-new-connector"></a>建立新的連接器
### <a name="client-software-installation-and-configuration"></a>用戶端軟體安裝和設定
Hello 伺服器上必須安裝 lotus Notes**之前**hello 安裝連接器。

當您安裝時，請務必執行 **單一使用者安裝**。 hello 預設**多使用者安裝**無法運作。  
![Notes1](./media/active-directory-aadconnectsync-connector-domino/notes1.png)

在 hello 功能頁面上，僅安裝必要的 hello Lotus Notes 功能和**用戶端的單一登入**。 Toohello Domino 伺服器上的 hello 連接器 toobe 無法 toolog 需要單一登入。  
![Notes2](./media/active-directory-aadconnectsync-connector-domino/notes2.png)

**注意：** hello 連接器的服務帳戶做為開始 Lotus Notes 一旦與使用者位於 hello hello 與相同的伺服器帳戶。 也請確定 tooclose hello Lotus Notes 用戶端 hello 伺服器上。 它會執行相同的時間 hello 連接器會 tooconnect toohello Domino 伺服器嘗試在 hello。

### <a name="create-connector"></a>建立連接器
tooCreate Lotus Domino 連接器，請在**同步處理服務**選取**管理代理程式**和**建立**。 選取 hello **Lotus domino 的連接器 (Microsoft)**連接器。  
![CreateConnector](./media/active-directory-aadconnectsync-connector-domino/createconnector.png)

如果您的同步處理服務版本會提供 hello 能力 tooconfigure**架構**，請確定 hello 連接器設定 tooits 預設值 toorun**程序**。

### <a name="connectivity"></a>連線能力
在 hello 連線能力 頁面上，您必須指定 hello Lotus domino 的連接器的伺服器名稱，然後輸入 hello 登入認證。  
![連線能力](./media/active-directory-aadconnectsync-connector-domino/connectivity.png)

hello Domino 伺服器屬性 hello 伺服器名稱支援兩種格式：

* ServerName
* ServerName/DirectoryName

hello **ServerName/DirectoryName**格式是 hello 慣用的格式，此屬性，因為 hello 連接器連絡人 hello Domino 伺服器時，它會提供更快的回應。

hello 提供使用者識別碼的檔案會儲存在 hello 的 hello 同步處理服務的組態資料庫。

針對 **差異匯入** ，您可以使用的選項如下：

* **無**。 hello 連接器不會進行任何差異匯入。
* **新增/更新**。 hello 連接器沒有差異匯入新增和更新作業。 至於刪除作業，則需要執行 **完整匯入** 作業。 這項作業使用 hello.Net interop。
* **新增/更新/刪除**。 hello 連接器沒有差異匯入新增、 更新和刪除作業。 這項作業使用原生 c + + 介面 hello。

在**結構描述選項**您擁有 hello 下列選項：

* **預設結構描述**。 hello 連接器會偵測到從 hello Domino 伺服器 hello 結構描述。 此選取項目是 hello 預設選項。
* **DSML 結構描述**。 只有使用 hello Domino 伺服器不會公開 hello 結構描述。 然後您可以使用 hello 結構描述，以建立 DSML 檔案而改為匯入。 如需 DSML 的詳細資訊，請參閱 [OASIS](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=dsml)。

當您按一下 下一步時，就會驗證 hello 使用者識別碼和密碼設定參數。

### <a name="global-parameters"></a>全域參數
在 hello 全域參數頁面上，您可以設定 hello 時區與 hello 匯入及匯出作業的選項。  
![全域參數](./media/active-directory-aadconnectsync-connector-domino/globalparameters.png)

hello **Domino 伺服器時區**參數會定義 Domino 伺服器 hello 位置。

此組態選項是必要的 toosupport**差異匯入**作業 hello 同步處理服務因為它可判斷之間 hello 最後兩個匯入的變更。

>[!Note]
開始在 hello 2017 年 3 月更新 hello 全域參數畫面 hello 使用者刪除期間包括 hello 選項 toodelete hello 使用者的郵件資料庫。

![刪除使用者的信箱](./media/active-directory-aadconnectsync-connector-domino/AdminP.png)

#### <a name="import-settings-method"></a>匯入設定、方法
hello**執行完整匯入的**具有下列選項：

* 搜尋
* 檢視 (建議選項)

**搜尋**是使用索引 Domino，但它是一般 hello 索引不會即時更新，並傳回 hello 伺服器 hello 資料永遠不正確。 對於具有許多變更的系統，此選項通常不會運作得很好，並且會在某些情況下造成誤刪。 不過，**搜尋**的速度比**檢視**快。

**檢視**hello 建議選項因為它提供資料 hello 正確狀態。 其速度比 [搜尋] 略慢。

#### <a name="creation-of-virtual-contact-objects"></a>建立虛擬連絡人物件
hello**啟用建立\_連絡人物件**具有下列選項：

* None
* 非參考值
* 參考和非參考值

在 Domino，參考屬性可以包含許多不同的格式 tooreference 其他物件。 toobe 無法 toorepresent 不同的變化，hello 連接器實作\_連絡人物件，也稱為**虛擬連絡人**(VC)。 這些物件會建立這樣他們才能加入 tooexisting MV 物件或投影成新的物件。 如此一來，即可保留屬性參考。

啟用此設定，而且如果 hello 內容的參考屬性不是以 DN 格式，\_建立連絡人物件。 例如，群組的成員屬性可以包含 SMTP 位址。 它也可能 toohave 簡短名稱，而且其他屬性存在於參考屬性。 針對此案例，請選取 [非參考值] 。 此設定是 hello Domino 實作最常見的設定。

Lotus domino 的連接器設定的 toohave 個別通訊錄時有不同的辨別名稱代表 hello 相同的物件，其可能 tooalso 建立\_連絡通訊錄中找到的所有參考值的物件。 針對此案例中，選取 hello**參考和非參考值**選項。

如果您將多個值在 hello 屬性**FullName**在 Domino，然後您也想 tooenable hello 建立虛擬連絡人以便能夠解析的參考。 例如，在合併或分離之後，這個屬性就可以具有多個值。 選取 hello 核取方塊**啟用...**FullName 能夠具有多個值 核取方塊。

加入在 hello 正確屬性後，hello\_連絡人物件會聯結的 toohello MV 物件。

這些物件具有 VC =\_連絡人新增 tootheir DN。

#### <a name="import-settings-conflict-object"></a>匯入設定、衝突物件
**排除衝突物件**

在大型 Domino 實作中，很可能在多個物件具有 hello 相同 DN tooreplication 問題原因。 在這些情況下，hello 連接器會看到兩個具有不同 UniversalIDs 但相同 DN 的物件。 這項衝突會導致在 hello 連接器空間中建立的暫時性物件。 hello 連接器可以忽略 hello 物件中已選取 Domino 為複寫犧牲者。 hello 建議的 tookeep 選取此核取方塊。

#### <a name="export-settings"></a>匯出設定
如果 hello 選項**使用 AdminP 更新參考**是未選取，則參考的屬性，例如成員、 匯出為直接呼叫，而且不會使用 hello AdminP 程序。 只有當 AdminP 尚未設定的 toomaintain 參考完整性時，才能使用此選項。

#### <a name="routing-information"></a>路由資訊
在 Domino，它可能會參考屬性具有內嵌為後置詞 toohello DN 的路由資訊。 例如，群組中的 hello member 屬性可能包含**CN =example/organization@ABC**。 hello 尾碼@ABChello 路由資訊。 hello 路由資訊是由 Domino toosend 電子郵件 toohello 正確 Domino 系統，這可能是另一個組織中的系統。 在 hello 路由資訊欄位中，您可以指定範圍中的 hello 連接器的 hello 組織內使用 hello 路由後置字元。 如果其中一個值的參考屬性中找到做為尾碼，hello 路由資訊會移除從 hello 參考。 如果 hello 路由的後置字元的參考值不能指定，這些值相符的 tooone\_建立連絡人物件。 這些\_建立連絡人物件，用**RO = @<RoutingSuffix>** 插入 hello DN。 這些\_連絡人物件 hello 下列屬性也會加入 tooallow 聯結 tooa 實際物件，視： \_routingName， \_contactName， \_displayName，和 UniversalID。

#### <a name="additional-address-books"></a>其他通訊錄
如果您不需要**協助**安裝，這樣會提供次要通訊錄 hello 名稱，則您可以手動輸入這些通訊錄。

#### <a name="multivalued-transformation"></a>多重值的轉換
Lotus Domino 中有許多屬性具有多重值。 hello 對應的 metaverse 屬性都是通常單一值。 藉由設定 hello 匯入和 hello 匯出作業選項，您可以啟用 hello 連接器 toohelp 與 hello 需要轉譯的 hello 受影響的屬性。

**匯出**  
hello 匯出作業選項支援兩種模式：

* 附加項目
* 取代項目

**取代的項目**– 當您選取此選項時，一律 hello 連接器移除 hello 目前屬性的值 hello Domino 中並取代 hello 提供值。 hello 提供值可以是，單一值或多重值。

範例： person 物件的 hello 助理屬性都具有下列值的 hello:

* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf

如果名為的新小幫手**David Alexander**是指派 toothis person 物件，則 hello 結果會是：

* CN=David Alexander/OU=Contoso/O=Americas,NAB=names.nsf

**將項目**– 當您選取此選項，hello 連接器會保留 hello Domino 和插入新的值，在 hello hello 資料清單最上方的 hello 屬性上的現有值。

範例： person 物件的 hello 助理屬性都具有下列值的 hello:

* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf

如果名為的新小幫手**David Alexander**是指派 toothis person 物件，則 hello 結果會是：

* CN=David Alexander/OU=Contoso/O=Americas,NAB=names.nsf
* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf

**匯入**  
hello 匯入作業選項支援兩種模式：

* 預設值
* 多重值的 tooSingle 值

**預設**– 當您選取 hello 預設選項，所有屬性都會匯入的 hello 的所有值。

**多重值的 tooSingle 值**– 當您選取此選項時，多重值的屬性會轉換成單一值的屬性。 如果多個值存在，則會使用在 hello （此值通常也是 hello 最新版） 的最上層的 hello 值。

範例： person 物件的 hello 助理屬性都具有下列值的 hello:

* CN=David Alexander/OU=Contoso/O=Americas,NAB=names.nsf
* CN=Greg Winston/OU=Contoso/O=Americas,NAB=names.nsf
* CN=John Smith/OU=Contoso/O=Americas,NAB=names.nsf

hello 最新的更新 toothis 屬性是**David Alexander**。 Hello 匯入作業的選項設定 tooMultivalued tooSingle 值，因為連接器只會匯入**David Alexander** hello 連接器空間。

toohello 群組成員屬性和 toohello 人員 fullname 屬性無法套用到單一值屬性的 hello 邏輯 tooconvert 多重值的屬性。

它也可能 tooconfigure 匯入和匯出的每個屬性，多重值屬性的轉換規則做為例外狀況 toohello 全域規則。 tooconfigure 選取此選項，輸入 [objecttype]。[attributename] 在 hello**匯入排除屬性清單**和**匯出排除屬性清單**文字方塊。 比方說，如果您輸入 Person.Assistant 而且 hello 全域旗標設定 tooimport 所有值，只有 hello 第一個值都會用於 hello assistant 匯入。

#### <a name="certifiers"></a>認證者
Hello 連接器會列出所有的公司/組織單元。 toobe 無法 tooexport 人員物件 toohello 主要通訊錄，發證者及其密碼是必要的。

如果所有 certifiers hello 相同的密碼，hello**密碼所有 Certifers**可用。 您可以輸入以下 hello 密碼，並且只能指定 hello 發證者檔案。

如果您只匯入，然後您沒有 toospecify 任何 certifiers。

### <a name="configure-provisioning-hierarchy"></a>設定佈建階層
當您設定 hello Lotus Domino 連接器時，請略過此對話方塊頁面。 hello Lotus Domino 連接器不支援佈建階層。  
![佈建階層](./media/active-directory-aadconnectsync-connector-domino/provisioninghierarchy.png)

### <a name="configure-partitions-and-hierarchies"></a>設定資料分割和階層
當您設定分割和階層時，您必須選取呼叫 NAB=names.nsf hello 主要地址通訊錄。 此外 toohello 主要位址活頁簿，您可以選取次要通訊錄如果有的話。  
![分割數](./media/active-directory-aadconnectsync-connector-domino/partitions.png)

### <a name="select-attributes"></a>選取屬性
在設定屬性時，必須選取前置詞為 **\_MMS\_** 的所有屬性。 新物件 tooLotus Domino 佈建時，都需要這些屬性

![屬性](./media/active-directory-aadconnectsync-connector-domino/attributes.png)

## <a name="object-lifecycle-management"></a>物件生命週期管理
本節中的 hello Domino 不同物件的概觀。

### <a name="person-objects"></a>Person 物件
hello person 物件代表組織和組織單位中的使用者。 此外 toohello 預設屬性，hello Domino 系統管理員可以新增自訂屬性 tooa Person 物件。 Person 物件至少必須包含所有必要屬性。 如需必要屬性的完整清單，請參閱 [Lotus Notes 屬性](#lotus-notes-properties)。 必須符合 tooregister person 物件，hello 下列必要條件：

* hello 通訊錄 (names.nsf) 必須已定義，且應 hello 主要通訊錄。
* 您必須在 hello O/OU 發證者識別碼和 hello 密碼 tooregister 特定使用者 hello 組織 / 組織單位。
* 您必須為 person 物件定義一組特定的 Lotus Notes 屬性。 這些屬性可用來佈建 hello person 物件。 如需詳細資訊，請參閱 < 呼叫 hello 區段[Lotus 備忘稿屬性](#lotus-notes-properties)本文件後面。
* hello 初始 HTTP 密碼的使用者。 將屬性和設定佈建期間
* hello person 物件必須是 hello 的下列三個支援的類型的其中一個：
  1. 具有郵件檔案和使用者識別碼檔案的一般使用者
  2. 漫遊使用者 (包含所有漫遊資料庫檔案的一般使用者)
  3. 連絡人 (沒有識別碼檔案的使用者)

（除了連絡人） 以外的人員可以進一步分組到美國的使用者和國際使用者所定義的 hello hello 值\_MMS\_IDRegType 屬性。 這些人使用 hello Notes 用戶端 tooaccess Lotus domino 的連接器的伺服器，則有備忘稿識別碼和人員文件。 如果這些人使用 Notes 郵件，他們也會有郵件檔案。 hello 使用者必須是已註冊的 toobecome 作用中。 如需詳細資訊，請參閱：

* [設定 Notes 使用者](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_SETTING_UP_NOTES_USERS.html)
* [使用者註冊](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_REGISTERING_USERS.html)
* [管理使用者](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_MANAGING_USERS_5151.html)
* [重新命名使用者](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_RENAMING_A_USER_AUTOMATICALLY.html)

所有這些作業會執行 Lotus domino 的連接器，而且接著匯入至 hello 同步處理服務。

### <a name="resources-and-rooms"></a>資源和會議室
資源是 Lotus Domino 中的另一種資料庫。 資源可以是備有各種設備的會議室，例如投影機。 有資源 Lotus Domino 連接器支援 hello 資源類型屬性所定義的子類型：

| 資源類型 | 資源類型屬性 |
| --- | --- |
| 會議室 |1 |
| 資源 (其他) |2 |
| 線上會議 |3 |

如 hello 資源物件型別 toowork hello 需要滿足下列條件：

* 資源保留資料庫應該存在於連接 hello Domino 伺服器
* 已為 hello 資源定義 hello 站台

hello 資源保留項目資料庫包含三種類型的文件：

* 網站設定檔
* 資源
* 保留

如需設定的資源保留資料庫的詳細資訊，請參閱[設定 hello 資源保留項目資料庫](https://www-01.ibm.com/support/knowledgecenter/SSKTMJ_8.0.1/com.ibm.help.domino.admin.doc/DOC/H_SETTING_UP_THE_RESOURCE_RESERVATIONS_DATABASE.html)。

**建立、更新和刪除資源**  
hello Create、 Update 和 Delete 作業會執行由 hello 資源保留資料庫中的 hello Lotus Domino 連接器。 資源會建立為 Names.nsf （也就是 hello 主要通訊錄） 中的文件。 如需編輯和刪除資源的詳細資訊，請參閱 [編輯和刪除資源文件](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_EDITING_AND_DELETING_RESOURCE_DOCUMENTS.html)。

**資源的匯入和匯出作業**  
hello 資源可以匯入的 tooand 匯出從 hello 同步處理服務就像任何其他類型的物件。 選取 hello 物件類型為資源在設定期間。 為了成功執行匯出作業，您應該具有資源類型、會議資料庫和網站名稱的詳細資料。

### <a name="mail-in-databases"></a>郵寄資料庫
Mail 中資料庫是設計的 tooreceive 郵件的資料庫。 此資料庫是未與任何特定 Lotus Domino 使用者帳戶相關聯 (也就是沒有自己的識別碼檔案和密碼) 的 Lotus Domino 信箱。 郵寄資料庫具有相關聯的唯一 UserID (「簡短名稱」)，並有自己的電子郵件地址。

如果需要可讓不同使用者共用的個別信箱，且此信箱擁有自己的電子郵件地址 (例如：group@contoso.com，則會建立郵寄資料庫。 hello 存取 toothis 信箱控制是透過其存取控制清單 (ACL)，其中包含的 hello Notes 使用者允許 tooopen hello 信箱 hello 名稱。

所需的 hello 屬性清單，請參閱稱為 hello 區段[強制屬性](#mandatory-attributes)本文稍後。

當資料庫是設計的 tooreceive 郵件時，郵件中的資料庫文件會建立在 Lotus domino 的連接器。 這份文件必須存在於每個伺服器會儲存一份 hello 資料庫的 Domino 目錄。 如需建立郵寄資料庫文件的詳細說明，請參閱 [建立郵寄資料庫文件](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_A_MAILIN_DATABASE_DOCUMENT_FOR_A_NEW_DATABASE_OVERVIEW.html)。

重新建立郵件中的資料庫，hello 資料庫應該已存在 （應該都由 Lotus Admin） 在 hello Domino 伺服器。

### <a name="group-management"></a>群組管理
您可以從下列資源的 hello 取得 hello Lotus domino 的連接器群組管理的詳細的概觀：

* [使用群組](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_USING_GROUPS_OVER.html)
* [建立群組](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_AND_MODIFYING_GROUPS_STEPS_MIDTOPIC_55038956829238418.html)
* [建立和修改群組](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_CREATING_AND_MODIFYING_GROUPS_STEPS.html)
* [管理群組](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_MANAGING_GROUPS_1804.html)
* [重新命名群組](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_RENAMING_A_GROUP_STEPS.html)

### <a name="password-management"></a>密碼管理
已註冊的 Lotus Domino 使用者有兩種類型的密碼：

1. 使用者密碼 (儲存在 User.id 檔案)
2. 網際網路/HTTP 密碼

hello Lotus Domino 連接器僅支援作業使用 HTTP 的密碼。

tooperform 密碼管理，您應該啟用 hello 管理代理程式的設計工具中的 hello 連接器的密碼管理。 tooenable 密碼管理，選取**啟用密碼管理**上 hello**設定延伸模組**對話方塊頁面。  
![](./media/active-directory-aadconnectsync-connector-domino/configureextensions.png)

hello Lotus Domino 連接器支援下列網際網路密碼的作業：

* 設定密碼： 設定密碼設定 Domino 中的 hello 使用者新的 HTTP/網際網路密碼。 根據預設 hello 帳戶也是解除鎖定。 hello 解除鎖定旗標的 hello 同步處理引擎 hello WMI 介面上公開。
* 變更密碼： 這個案例中，使用者可能會想 toochange hello 密碼，或提示的 toochange 密碼之後指定的時間。 此作業 tootake 位置，同時 （hello 舊和新密碼的 hello） 都是必要項。 一旦變更，會更新 Lotus Domino hello 新密碼。

如需詳細資訊，請參閱：

* [使用 hello 網際網路鎖定功能](http://www.ibm.com/developerworks/lotus/library/domino8-lockout/)
* [管理網際網路密碼](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=/com.ibm.help.domino.admin85.doc/H_NOTES_AND_INTERNET_PASSWORD_SYNCHRONIZATION_7570_OVER.html)

## <a name="reference-information"></a>參考資訊
此區段會列出屬性描述等 hello Lotus Domino 連接器屬性需求。

### <a name="lotus-notes-properties"></a>Lotus Notes 屬性
當您佈建連絡人物件 tooyour Lotus Domino 目錄時，您的物件必須具有特定值填入的一組特定的屬性。 只有建立作業才需要這些值。

hello 下表列出這些屬性並提供它們的描述。

| 屬性 | 說明 |
| --- | --- |
| \_MMS_AltFullName |hello 替代的完整名稱的使用者。 |
| \_MMS_AltFullNameLanguage |hello 語言 toobe 用來指定 hello 替代使用者完整名稱。 |
| \_MMS_CertDaysToExpire |hello 數天內從 hello 之前 hello 憑證目前的日期到期。 如果未指定，hello 預設日期是兩年 hello 從目前的日期。 |
| \_MMS_Certifier |包含 hello 發證者 hello 組織階層名稱的屬性。 例如：OU=OrganizationUnit,O=Org,C=Country。 |
| \_MMS_IDPath |Hello 屬性是空的如果沒有使用者識別檔案在本機上建立 hello 同步伺服器。 如果 hello 屬性包含檔案名稱，使用者識別碼檔案會建立 hello madata 資料夾中。 hello 屬性也可以包含完整路徑。 |
| \_MMS_IDRegType |人員可以分類為連絡人、美國使用者和國際使用者。 hello 下表列出 hello 可能的值： <li>0 - 連絡人</li><li>1 - 美國使用者</li><li>2 - 國際使用者</li> |
| \_MMS_IDStoreType |適用於美國和國際使用者的必要屬性。 hello 屬性包含整數值，指定是否在 hello 備忘稿通訊錄或 hello 人的郵件檔案附件形式儲存 hello 的使用者身分識別。 如果 hello 使用者識別碼的檔案是 hello 通訊錄中的附加檔案，它可以選擇性地建立以檔案\_MMS_IDPath。 <li>空白 - 將識別碼檔案儲存在識別碼保存庫中，沒有識別碼檔案 (用於「連絡人」)。</li><li> 1-hello 備忘稿通訊錄中的附件。 hello \_MMS_Password 屬性必須設定的使用者識別檔案附件</li><li>2 - 人員的郵件檔案中的市集識別碼。 hello \_MMS_UseAdminP 必須設定 toofalse toolet hello 郵件 hello 人員註冊期間建立的檔案。 hello \_MMS_Password 屬性必須設定的使用者識別的檔案。</li> |
| \_MMS_MailQuotaSizeLimit |hello mb 所允許的 hello 電子郵件檔案的資料庫數目。 |
| \_MMS_MailQuotaWarningThreshold |hello hello 電子郵件檔案的資料庫會產生警告之前所允許的 mb 數。 |
| \_MMS_MailTemplateName |是使用的 toocreate hello 使用者的電子郵件檔案 hello 電子郵件範本檔案。 如果有指定 template，hello 郵件檔會建立使用 hello 指定的範本。 如果未不指定任何範本，則 hello 預設範本檔案會是使用的 toocreate hello 檔案。 |
| \_MMS_OU |選擇性屬性，是在 hello 發證者 hello OU 名稱。 連絡人的這個屬性應該是空的。 |
| \_MMS_Password |使用者的必要屬性。 hello 屬性包含 hello hello 物件的 hello 識別檔案的密碼。 |
| \_MMS_UseAdminP |屬性應設定 tootrue，如果 hello 郵件檔應該要建立 hello AdminP hello Domino 伺服器 （非同步 toohello 匯出程序） 上的處理程序。 如果屬性設定 toofalse，hello mail 會建立檔案以 hello Domino 使用者 （同步 hello 匯出程序中）。 |

具有相關聯的識別檔案的使用者，hello \_MMS_Password 屬性必須包含的值。 對於透過 hello Lotus Notes 用戶端的電子郵件存取，hello mail 伺服器和使用者 MailFile 屬性必須包含的值。

網頁瀏覽器，透過電子郵件的 tooaccess hello 下列屬性必須包含的值：

* MailFile-包含 hello 路徑儲存 hello 郵件檔案 hello Lotus domino 的連接器的伺服器上的必要屬性。
* Mail 伺服器的必要屬性，其中包含 hello hello Lotus domino 的連接器的伺服器名稱。 當您建立 hello Domino 伺服器 hello Lotus 郵件檔案時，這個值會是 hello 名稱 toouse。
* HTTPPassword-選用的屬性，其中包含 hello 物件 hello Web 存取密碼。

tooaccess hello Domino 伺服器不具備郵件功能，hello HTTPPassword 屬性必須包含的值。 hello MailFile 屬性和 hello mail 伺服器屬性可以是空的。

與\_MMS_ IDStoreType = 2 (郵件檔案中儲存區 id，) hello NotesRegistrationclass MailSystem 屬性會設定 tooREG_MAILSYSTEM_INOTES (3)。

### <a name="mandatory-attributes"></a>必要屬性
hello Lotus Domino 連接器主要是支援這些類型的物件 （文件類型）：

* 群組
* 郵寄資料庫
* Person
* 連絡人 (沒有認證者的人員)
* 資源

此區段會列出每個支援的物件 tooexport tooa Domino 伺服器強制的 hello 屬性。

| 物件類型 | 必要屬性 |
| --- | --- |
| 群組 |<li>ListName</li> |
| 郵寄資料庫 |<li>FullName</li><li>MailFile</li><li>MailServer</li><li>MailDomain</li> |
| Person |<li>姓氏</li><li>MailFile</li><li>ShortName</li><li>\_MMS_Password</li><li>\_MMS_IDStoreType</li><li>\_MMS_Certifier</li><li>\_MMS_IDRegType</li><li>\_MMS_UseAdminP</li> |
| 連絡人 (沒有認證者的人員) |<li>\_MMS_IDRegType</li> |
| 資源 |<li>FullName</li><li>ResourceType</li><li>ConfDB</li><li>ResourceCapacity</li><li>網站</li><li>displayName</li><li>MailFile</li><li>MailServer</li><li>MailDomain</li> |

## <a name="common-issues-and-questions"></a>常見問題
### <a name="schema-detection-does-not-work"></a>結構描述偵測沒有作用
toobe 無法 toodetect hello 結構描述，則需要該 hello schema.nsf 檔案存在於 hello Domino 伺服器上。 只有 LDAP hello 伺服器上已安裝，才會出現這個檔案。 如果偵測不到 hello 結構描述，hello 下列驗證：

* hello 檔案 schema.nsf 都出現在 hello hello Domino 伺服器根資料夾
* hello 使用者有權限 toosee hello schema.nsf 檔案。
* 強制 hello LDAP 伺服器的重新啟動。 開啟**Lotus Domino 主控台**並用**告訴 LDAP ReloadSchema**命令 tooreload hello 結構描述。

### <a name="not-all-secondary-address-books-are-visible"></a>無法看見所有次要通訊錄
hello Domino 連接器依賴 hello 功能**協助**toobe 無法 toofind hello 次要通訊錄。 如果遺漏了 hello 次要通訊錄，請確認如果[協助](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_DIRECTORY_ASSISTANCE.html)已啟用並設定 hello Domino 伺服器上。

### <a name="custom-attributes-in-domino"></a>Domino 中的自訂屬性
有幾種方式 Domino tooextend hello 結構描述中，依 hello 連接器做為您可以使用的自訂屬性會出現。

**方法 1：延伸 Lotus Domino 結構描述**

1. 建立一份 Domino 目錄範本 {PUBNAMES。NTF} 依照[步驟](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_CREATING_A_COPY_OF_THE_DEFAULT_PUBIC_ADDRESS_BOOK_TEMPLATE.html)（您不應該自訂 hello 預設 IBM Lotus Domino 目錄範本）：
2. 開啟 hello 複製的 Domino 目錄範本 {CONTOSO。NTF} 範本 Domino 設計工具中所建立，並遵循下列步驟：
   * 按一下 [共用元素]，然後展開子表單
   * 按兩下 ${ObjectName} InheritableSchema 子表單 (其中 {ObjectName} 是 hello hello 預設結構化物件類別名稱，例如： 人)。
   * 要插入結構描述 {MyPersonAtrribute} tooadd 的 hello 屬性和對應的 toothat 屬性名稱。 建立所選取的 hello 欄位**建立**功能表，然後選取**欄位**從功能表。
   * 在 hello 加入欄位中，請選取其類型、 樣式、 大小、 字型和欄位屬性 視窗上的其他相關的參數來設定其屬性。
   * 保留預設值相同 hello 名稱給該屬性的 hello 屬性 (例如，如果屬性名稱 MyPersonAttribute，保留以 hello hello 預設值相同的名稱)。
   * 儲存更新的值 hello ${ObjectName} InheritableSchema 子表單。
3. 取代 hello Domino 目錄範本 {PUBNAMES。NTF} hello 新自訂範本 {CONTOSO。NTF} 依照[步驟](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_RULES_FOR_CUSTOMIZING_THE_PUBLIC_ADDRESS_BOOK.html)。
4. 關閉 Domino 系統管理員，並開啟 Domino 主控台 toorestart hello LDAP 服務和 tooReload hello LDAP 結構描述：
   * 在 Domino 主控台中，插入下的 hello 命令**Domino 命令**文字歸檔 toorestart hello LDAP 服務-[重新啟動工作 LDAP](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_STARTING_AND_STOPPING_THE_LDAP_SERVER_OVER.html)。
   * tooreload LDAP 結構描述使用告訴 LDAP 命令-告訴 LDAP ReloadSchema
5. 開啟 Domino 系統管理員並選取使用者和群組] 索引標籤 toosee 加入屬性會反映在 [新增人員 domino。
6. 從 [檔案]  索引標籤開啟 Schema.nsf，並查看新增的屬性是否已反映到 dominoPerson LDAP 物件類別。

**方法 2： 建立 Domaindns 具有自訂屬性，並將與 hello 物件類別關聯**

1. 建立一份 Domino 目錄範本 {PUBNAMES。NTF} 依照[步驟](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_CREATING_A_COPY_OF_THE_DEFAULT_PUBIC_ADDRESS_BOOK_TEMPLATE.html)（永遠不會自訂 hello 預設 IBM Lotus Domino 目錄範本）：
2. 開啟 hello 複製的 Domino 目錄範本 {CONTOSO。NTF}，Domino 設計工具中所建立的範本。
3. Hello 左窗格中，選取 共用程式碼，然後子表單。
4. 按一下 [新增子表單]
5. 下列 hello 新的子表單的 toospecify hello 屬性 hello:
   * Hello 新的子表單開啟時，選擇 設計-子表單屬性
   * 下一步 toohello Name 屬性，輸入，例如 TestSubform-hello 輔助物件類別的名稱。
   * 保留"Include 中插入子表單...對話方塊"選取 hello Options 屬性
   * 取消選取 hello Options 屬性 」 呈現通過便箋中的 HTML。 」
   * 保持 hello 其他屬性 hello 相同，並關閉 hello 子內容。
   * 儲存並關閉 hello 新的子表單。
6. 請勿 hello 下列 tooadd 欄位 toodefine hello 輔助物件類別：
   * 開啟您所建立的 hello 子表單。
   * 選擇 [建立] > [欄位]。
   * 下一步 tooName hello 欄位 對話方塊中，基本概念 hello 索引標籤上的指定任何名稱，例如: {MyPersonTestAttribute}。
   * 在 hello 加入欄位中，選取其類型、 樣式、 大小、 字型和相關的屬性設定其屬性。
   * 保留預設值相同 hello 名稱給該屬性的 hello 屬性 (例如，如果屬性名稱 MyPersonTestAttribute，保留以 hello hello 預設值相同的名稱)。
   * 儲存 hello 子表單和更新值，並執行下列 hello:
     * Hello 左窗格中，選取 共用程式碼，然後子表單
     * 選取 hello 新的子表單，然後選擇設計的設計內容。
     * 按一下 hello hello 左邊，從第三個索引標籤，然後選取**傳播的設計變更這項限制**。
7. 開啟 ${ObjectName} ExtensibleSchema 子表單 （其中 {ObjectName} 是 hello hello 預設結構化物件，例如 – Person 類別名稱）。
8. 插入資源並選取 hello （您所建立，例如 – TestSubform） 子表單並儲存 hello ${ObjectName} ExtensibleSchema 子表單。
9. 取代 hello Domino 目錄範本 {PUBNAMES。NTF} hello 新自訂範本 {CONTOSO。NTF} 依照[步驟](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_ABOUT_RULES_FOR_CUSTOMIZING_THE_PUBLIC_ADDRESS_BOOK.html)。
10. 關閉 Domino 系統管理員，並開啟 Domino 主控台 toorestart hello LDAP 服務和 tooReload hello LDAP 結構描述：
    * 在 Domino 主控台中，插入下的 hello 命令**Domino 命令**文字歸檔 toorestart hello LDAP 服務-[重新啟動工作 LDAP](http://publib.boulder.ibm.com/infocenter/domhelp/v8r0/index.jsp?topic=%2Fcom.ibm.help.domino.admin85.doc%2FH_STARTING_AND_STOPPING_THE_LDAP_SERVER_OVER.html)。
    * tooreload LDAP 結構描述使用告訴 LDAP 命令**告訴 LDAP ReloadSchema**。
11. 開啟 Domino 系統管理員並選取使用者和群組] 索引標籤 toosee 加入屬性會反映在 [新增人員 domino （在其他索引標籤上）。
12. 從 [檔案]  索引標籤開啟 Schema.nsf，並查看新增的屬性是否已在 [TestSubform LDAP 輔助] 物件類別下反映。

**方法 3： 加入 hello 自訂屬性 toohello ExtensibleObject 類別**

1. 開啟 {Schema.nsf} 檔案放在 hello 根目錄
2. 從下 hello 左側功能表中選取 LDAP 物件類別**所有結構描述文件**按一下**加入的物件類別**按鈕：
3. 提供 LDAP 名稱 （其中 zzz 是 hello hello 預設結構化物件類別名稱，例如人員） {zzzExtensibleSchema} hello 形式。 例如，tooextend hello 結構描述 Person 物件類別，提供 LDAP 名稱 {PersonExtensibleSchema}。
4. 提供要 tooextend hello 結構描述的上層物件類別名稱。 例如，tooextend hello 結構描述 Person 物件類別，提供上層物件類別名稱 {dominoPerson}:
5. 請提供有效的 OID 對應 toohello 物件的類別。
6. 選取下為必要或選用的屬性類型的欄位，根據 hello 需求的延伸/自訂屬性：
7. 加入必要屬性 toohello ExtensibleObjectClass 之後，請按一下**儲存並關閉**。
8. 系統會為各自的預設物件類別建立具有延伸屬性的 ExtensibleObjectClass。

## <a name="troubleshooting"></a>疑難排解
* 如需如何 tooenable 記錄 tootroubleshoot hello 連接器資訊，請參閱 hello[如何 tooEnable ETW 追蹤連接器](http://go.microsoft.com/fwlink/?LinkId=335731)。
