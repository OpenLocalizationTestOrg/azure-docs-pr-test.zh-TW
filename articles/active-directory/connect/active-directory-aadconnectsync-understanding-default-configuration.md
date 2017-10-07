---
title: "Azure AD Connect 同步： 了解 hello 預設組態 |Microsoft 文件"
description: "本文章說明 Azure AD Connect 同步處理中的 hello 預設組態。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: ed876f22-6892-4b9d-acbe-6a2d112f1cd1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 1cf95759af913cad8a1393839d3a836434e7c9bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-hello-default-configuration"></a>Azure AD Connect 同步： 了解 hello 預設組態
本文說明 hello 鶈蜪設定規則。 並說明 hello 規則，以及這些規則影響 hello 組態的方式。 它也會引導您透過 Azure AD Connect 同步處理的 hello 預設組態。hello 目標是 hello 讀取器瞭解運作 hello 組態模型中，名為宣告式佈建在真實世界範例。 本文假設您已安裝並設定 Azure AD Connect 同步處理使用 hello 安裝精靈。

toounderstand hello 模型的詳細資料 hello 組態，讀取[了解宣告式佈建](active-directory-aadconnectsync-understanding-declarative-provisioning.md)。

## <a name="out-of-box-rules-from-on-premises-tooazure-ad"></a>從內部部署 tooAzure AD 鶈蜪規則
hello 下列運算式可以找到 hello 鶈蜪組態中。

### <a name="user-out-of-box-rules"></a>使用者現成可用的規則
這些規則也適用於 toohello iNetOrgPerson 物件類型。

使用者物件必須滿足下列 toobe 同步處理的 hello:

* 必須具有 sourceAnchor。
* 之後 hello 物件已在 Azure AD 中建立，則無法變更 sourceAnchor。 如果 hello 值已變更的內部部署，hello 物件就會停止同步處理直到 hello sourceAnchor 變更後 tooits 先前的值。
* 必須有 hello accountEnabled (userAccountControl) 屬性擴展。 在內部部署 Active Directory 中，一律會存在並填入此屬性。

下列使用者物件的 hello 是**不**tooAzure AD 同步處理：

* `IsPresent([isCriticalSystemObject])`。 確定在 Active Directory 中，許多的鶈蜪物件，例如 hello 內建的 administrator 帳戶，不會同步處理。
* `IsPresent([sAMAccountName]) = False`。 請確定沒有 sAMAccountName 屬性的使用者物件不會同步處理。 這種情況實際上只會發生在從 NT4 升級的網域中。
* `Left([sAMAccountName], 4) = "AAD_"`，`Left([sAMAccountName], 5) = "MSOL_"`。 不要同步處理 hello Azure AD Connect 同步處理和與其舊版所使用的服務帳戶。
* 請勿同步處理不會在 Exchange Online 中運作的 Exchange 帳戶。
  * `[sAMAccountName] = "SUPPORT_388945a0"`
  * `Left([mailNickname], 14) = "SystemMailbox{"`
  * `(Left([mailNickname], 4) = "CAS_" && (InStr([mailNickname], "}") > 0))`
  * `(Left([sAMAccountName], 4) = "CAS_" && (InStr([sAMAccountName], "}")> 0))`
* 請勿同步處理不會在 Exchange Online 中運作的物件。
  `CBool(IIF(IsPresent([msExchRecipientTypeDetails]),BitAnd([msExchRecipientTypeDetails],&H21C07000) > 0,NULL))`  
  此位元遮罩 (& H21C07000) 會篩選出 hello 下列物件：
  * 擁有郵件功能的公用資料夾
  * 系統服務員信箱
  * 信箱資料庫信箱 (系統信箱)
  * 萬用安全性群組 (不會對使用者套用，但因舊版因素而存在)
  * 非萬用群組 (不會對使用者套用，但因舊版因素而存在)
  * 信箱計劃
  * 探索信箱
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`。 請不要同步處理任何複寫犧牲者物件。

適用於下列屬性的規則 hello:

* `sourceAnchor <- IIF([msExchRecipientTypeDetails]=2,NULL,..)`。 hello sourceAnchor 屬性不被由連結信箱。 它會假設，如果發現連結的信箱，稍後加入 hello 實際的帳戶。
* Exchange 相關的屬性只有當同步處理 hello 屬性**mailNickName**的值。
* 多個樹系時，屬性會耗用 hello 順序中：
  1. Toosign 中相關的屬性 （如範例 userPrincipalName) 會造成從 hello 樹系中使用已啟用的帳戶。
  2. 可以在 Exchange GAL （全域通訊清單） 中找到的屬性被由 hello 與 Exchange 信箱的樹系。
  3. 如果找不到信箱，則這些屬性可來自於任何樹系。
  4. Exchange 相關的屬性 （技術屬性未顯示在 hello GAL） 從 hello 樹系提供其中`mailNickname ISNOTNULL`。
  5. 如果有多個樹系，就可以滿足這些規則，其中一個規則，然後 hello hello 連接器 （樹系） 的建立順序 （日期/時間） 是使用的 toodetermine 哪個樹系佔 hello 屬性。

### <a name="contact-out-of-box-rules"></a>連絡人現成可用的規則
連絡人物件必須滿足下列 toobe 同步處理的 hello:

* hello 連絡人必須是擁有郵件功能。 已驗證以 hello 下列規則：
  * `IsPresent([proxyAddresses]) = True)`。 必須先填入 hello proxyAddresses 屬性。
  * 主要電子郵件地址可以找到 hello proxyAddresses 屬性或 hello mail 屬性中。 hello 與否 @ 是使用的 tooverify hello 內容是電子郵件地址。 這兩個規則的其中一個必須評估的 tooTrue。
    * `(Contains([proxyAddresses], "SMTP:") > 0) && (InStr(Item([proxyAddresses], Contains([proxyAddresses], "SMTP:")), "@") > 0))`。 是否有與項目"SMTP:"，而且如果沒有，可以 @ 是 hello 字串中找到？
    * `(IsPresent([mail]) = True && (InStr([mail], "@") > 0)`。 Hello mail 屬性填入，而且如果是，可以是 @ 是 hello 字串中找到？

hello 下列連絡人物件是**不**tooAzure AD 同步處理：

* `IsPresent([isCriticalSystemObject])`。 請確定沒有標記為重要的連絡人物件進行同步處理。 不應該是任何使用預設組態的項目。
* `((InStr([displayName], "(MSOL)") > 0) && (CBool([msExchHideFromAddressLists])))`。
* `(Left([mailNickname], 4) = "CAS_" && (InStr([mailNickname], "}") > 0))`。 這些物件無法在 Exchange Online 中運作。
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`。 請不要同步處理任何複寫犧牲者物件。

### <a name="group-out-of-box-rules"></a>群組現成可用的規則
群組物件必須滿足下列 toobe 同步處理的 hello:

* 擁有的成員必須少於 50,000 個。 這個計數會 hello hello 內部群組的成員數目。
  * 如果同步處理開始 hello 第一次之前，它具有多個成員，則 hello 群組不會同步。
  * 如果成員的 hello 數目成長從最初建立時，然後到達 50,000 的成員，它會停止同步處理，直到 hello 成員資格計數低於 50000 一次時。
  * 注意： Azure AD 也強制 hello 50,000 的成員資格計數。 您不能 toosynchronize 群組與多個成員，即使您修改或移除此規則。
* 如果 hello 群組**發佈群組**，則也必須是擁有郵件功能。 請參閱 [連絡人現成可用的規則](#contact-out-of-box-rules) ，以了解強制執行此規則的情形。

下列群組物件的 hello 是**不**tooAzure AD 同步處理：

* `IsPresent([isCriticalSystemObject])`。 確定在 Active Directory 中，許多的鶈蜪物件，例如 hello 內建的 administrators 群組，不會同步處理。
* `[sAMAccountName] = "MSOL_AD_Sync_RichCoexistence"`。 DirSync 所使用的舊版群組。
* `BitAnd([msExchRecipientTypeDetails],&amp;H40000000)`。 角色群組。
* `CBool(InStr(DNComponent(CRef([dn]),1),"\\0ACNF:")>0)`。 請不要同步處理任何複寫犧牲者物件。

### <a name="foreignsecurityprincipal-out-of-box-rules"></a>ForeignSecurityPrincipal 現成可用的規則
Fsp 聯結太 「 任何 」 (\*) hello metaverse 中的物件。 實際上，此聯結只會針對使用者和安全性群組執行。 此組態可確保跨樹系成員資格會進行解析，並正確地顯示在 Azure AD 中。

### <a name="computer-out-of-box-rules"></a>電腦現成可用的規則
電腦物件必須滿足下列 toobe 同步處理的 hello:

* `userCertificate ISNOTNULL`。 只有 Windows 10 電腦會填入此屬性。 所有具有此屬性值的電腦物件都會進行同步處理。

## <a name="understanding-hello-out-of-box-rules-scenario"></a>了解 hello 鶈蜪規則案例
在此範例中，我們會使用具有一個帳戶樹系 (A)、一個資源樹系 (R) 和一個 Azure AD 目錄的部署。

![含案例說明的圖片](./media/active-directory-aadconnectsync-understanding-default-configuration/scenario.png)

此設定會假設沒有 hello 帳戶樹系中已啟用的帳戶，而且具有連結信箱的 hello 資源樹系中停用的帳戶。

我們的目標與 hello 預設組態是：

* 屬性相關 toosign 中從 hello 樹系與 hello 啟用帳戶同步。
* 可以在 hello GAL （全域通訊清單） 中找到的屬性會從 hello 與 hello 信箱的樹系同步處理。 如果找不到信箱，則會使用任何其他樹系。
* 如果找到連結的信箱，hello 連結已啟用的帳戶必須找到的 hello 物件匯出 toobe tooAzure AD。

### <a name="synchronization-rule-editor"></a>同步處理規則編輯器
hello 組態即可檢視及變更與 hello 工具同步處理規則編輯器 」 (SRE)，可以找到捷徑 tooit hello [開始] 功能表中。

![同步處理規則編輯器圖示](./media/active-directory-aadconnectsync-understanding-default-configuration/sre.png)

hello SRE 是一個資源套件工具並安裝 Azure AD Connect 同步處理。toobe 無法 toostart，您必須是 hello ADSyncAdmins 群組的成員。 在它啟動時，您會看到如下的畫面：

![同步處理規則 (輸入)](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulesinbound.png)

在此窗格中，您會看到所有為您的組態建立的同步處理規則。 Hello 資料表中的每一行都是一個同步處理規則。 toohello 留在 規則類型，會列出兩種不同類型的 hello： 輸入及輸出。 輸入和輸出來自 hello 的 hello metaverse 的檢視。 您是主要進入 toofocus hello 上的輸入本概觀中的規則。 hello 的同步處理規則的實際清單取決在 AD 中的 hello 偵測到結構描述。 在上述的 hello 圖片，hello 帳戶樹系 (fabrikamonline.com) 沒有任何服務，例如 Exchange 和 Lync，以及任何同步處理規則已建立這些服務。 不過，在 hello 資源樹系 (res.fabrikamonline.com) 您找到的同步處理規則針對這些服務。 hello 規則 hello 內容是偵測到的 hello 版本而有所不同。 比方說，在 Exchange 2013 的部署中，屬性流程比在 Exchange 2010/2007 中設定的多。

### <a name="synchronization-rule"></a>同步處理規則
同步處理規則是一個組態物件，當滿足條件時會有一組屬性進行流動。 它也是連接器空間中的之物件的相關的 tooan hello metaverse，稱為物件的方式使用的 toodescribe**聯結**或**符合**。 hello 同步化規則具有優先順序值，指出其與其他 tooeach 的關聯。 較小的數值與同步處理規則的優先順序，並在屬性流程發生衝突時，較高的優先順序 wins hello 衝突解決。

例如，查看同步處理規則 hello**中 from AD – User AccountEnabled**。 標示 hello SRE 中的這一行，並選取**編輯**。

由於這項規則的預設規則，當您開啟 hello 規則時收到警告。 您不應做任何[變更 tooout 之 規則](active-directory-aadconnectsync-best-practices-changing-default-configuration.md)，所以系統會詢問您要的情況為何。 在此情況下，您只想 tooview hello 規則。 請選取 [否] 。

![同步處理規則警告](./media/active-directory-aadconnectsync-understanding-default-configuration/warningeditrule.png)

同步處理規則具有四個組態區段：說明、範圍篩選器、聯結規則及轉換。

#### <a name="description"></a>說明
hello 第一個區段提供基本的資訊，例如名稱和描述。

![同步處理規則編輯器中的說明索引標籤 ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncruledescription.png)

您也可以找到連接的系統此規則相關的物件類型中 hello 連線的系統中套用，以及 hello metaverse 物件類型的相關資訊。 hello metaverse 物件類型時，一定會人不論 hello 來源物件類型是使用者、 iNetOrgPerson 或 contact。 它會建立為泛型類型，應該永遠不會變更 hello metaverse 物件類型。 可以設定 hello 連結類型，tooJoin、 StickyJoin 或 Provision。 這個設定可以與 hello 聯結規則 區段一起運作，並涵蓋的更新版本。

您也可以看到此同步處理規則用於密碼同步。如果使用者在此同步處理規則的範圍內，hello 密碼會同步處理，從內部部署 toocloud （假設您已啟用 hello 密碼同步功能）。

#### <a name="scoping-filter"></a>範圍篩選器
hello 篩選範圍 區段時，使用的 tooconfigure 應套用同步處理規則。 因為您正在查看的同步處理規則 hello hello 名稱表示只應套用於啟用的使用者，設定 hello 領域因此 hello AD 屬性**userAccountControl**必須不具有 hello 設定位元 2。 當 hello 同步處理引擎會在 AD 中尋找使用者時，它會套用此同步處理規則時**userAccountControl**設定 toohello 十進位值 512 （已啟用的一般使用者）。 它不會套用 hello 規則 hello 使用者有時**userAccountControl**設定 too514 （已停用的一般使用者）。

![同步處理規則編輯器中的範圍索引標籤 ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulescopingfilter.png)

hello 範圍篩選器包含群組，但可以巢狀的子句。 同步處理規則 tooapply 必須滿足群組內的所有子句。 定義了多個群組，然後至少一個群組必須滿足 hello 規則 tooapply。 也就是說，系統會在群組間評估邏輯 OR ，而在單一群組中評估邏輯 AND。 這項設定的範例，請參閱 hello 輸出同步處理規則**出 tooAAD – Group Join**。 同步處理篩選器有數個群組，例如，一個適用於安全性群組 (`securityEnabled EQUAL True`) 的群組，和一個適用於通訊群組 (`securityEnabled EQUAL False`) 的群組。

![同步處理規則編輯器中的範圍索引標籤 ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulescopingfilterout.png)

此規則會使用的 toodefine 群組應該佈建的 tooAzure AD。 通訊群組必須是擁有郵件功能 toobe 與 Azure AD 同步處理，但對於安全性群組而言電子郵件不需要。

#### <a name="join-rules"></a>聯結規則
hello 第三個區段都是使用的 tooconfigure hello 連接器空間中的物件與 tooobjects hello metaverse 中的關聯。 hello 您稍早查看的規則沒有任何組態，聯結規則，而是會在進行 toolook**中 from AD – User Join**。

![同步處理規則編輯器中的聯結規則索引標籤 ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulejoinrules.png)

hello 聯結規則 hello 內容取決於 hello 相符 hello 安裝精靈中選取的選項。 以輸入的規則評估 hello 開頭 hello 來源連接器空間中的物件，而且 hello 聯結規則中的每個群組會依序評估。 如果來源物件是一個評估的 toomatch 物件在 hello 使用其中一種 hello 聯結規則的 metaverse，hello 物件會加入。 如果已評估所有規則，而且沒有相符項目，則會使用 hello 連結類型在 hello [描述] 頁面。 如果此組態設定得**佈建**，然後 hello 目標，hello metaverse 中建立新的物件。 新的物件 toohello metaverse 太也稱為 tooprovision**專案**物件 toohello metaverse。

hello 聯結規則只評估一次。 當連接器空間物件和 metaverse 物件聯結在一起時，它們會保留聯結 hello hello 同步處理規則範圍是仍然滿足為。

評估同步處理規則時，只有一個具有已定義聯結規則的同步處理規則必須在範圍內。 如果發現多個具有聯結規則的同步處理規則用於單一物件，就會擲回錯誤。 基於這個理由，hello 最佳作法是的 toohave 只能有一個具有聯結的同步處理規則定義多個同步處理規則的物件範圍時。 在 hello 鶈蜪組態中的 Azure AD Connect 同步處理，這些規則可以找到藉由查看 hello 名稱，並且尋找與 hello word**聯結**hello hello 名稱結尾處。 另一個同步處理規則 hello 物件聯結在一起，或佈建 hello 目標中的新物件時，同步處理規則沒有定義任何聯結規則適用於 hello 屬性流程。

如果您查看 hello 圖片上方時，您可以看到該 hello 規則正嘗試 toojoin **objectSID**與**msExchMasterAccountSid** (Exchange) 和**msRTCSIP OriginatorSid** (Lync)，這是我們預期的帳戶-資源樹系拓撲中。 Hello 尋找所有樹系上的相同規則。 hello 假設是每個樹系，可能是 「 帳戶 」 或 「 資源樹系。 如果您有駐留在單一樹系，且沒有 toobe 加入帳戶，也可以運作這項設定。

#### <a name="transformations"></a>轉換
hello 轉換區段定義當聯結 hello 物件且滿足 hello 範圍篩選時，套用 toohello 目標物件的所有屬性流程。 返回 toohello**中 from AD – User AccountEnabled**同步處理規則，尋找下列轉換 hello:

![同步處理規則編輯器中的轉換索引標籤 ](./media/active-directory-aadconnectsync-understanding-default-configuration/syncruletransformations.png)

tooput 在內容中，在帳戶資源樹系部署中，此組態是預期的 toofind hello 帳戶樹系中已啟用的帳戶和停用的帳戶在 hello 資源樹系 Exchange 和 Lync 設定。 hello 您正在查看的同步處理規則包含所需的登入的 hello 屬性，這些屬性應該從 hello 樹系沒有已啟用的帳戶。 這些屬性流程會全部放在一個同步處理規則中。

轉換可具有不同類型：Constant、Direct 和 Expression。

* Constant 流程會一律流送硬式編碼值。 在上述的 hello 情況下，它一律會將 hello 值**True**中名為 hello metaverse 屬性**accountEnabled**。
* 「 直接 」 流程一律傳送 hello hello 做為來源 toohello 目標屬性中的 hello 屬性值為是。
* hello 第三個流程類型是運算式，它可讓您更進階的組態。

hello 運算式語言是 VBA (Visual Basic 應用程式)，因此人員體驗的 Microsoft Office 或 VBScript 會辨識 hello 格式。 屬性會包在方括號之中，例如 [attributeName]。 屬性名稱和函式名稱會區分大小寫，但 hello 同步處理規則編輯器會評估 hello 運算式，並提供警告如果 hello 運算式無效。 所有運算式將會以具有巢狀函式的單一行表示。 tooshow hello 電源的 hello 設定語言，以下是 pwdLastSet，但插入額外的註解的 hello 流程：

```
// If-then-else
IIF(
// (hello evaluation for IIF) Is hello attribute pwdLastSet present in AD?
IsPresent([pwdLastSet]),
// (hello True part of IIF) If it is, then from right tooleft, convert hello AD time format tooa .Net datetime, change it toohello time format used by Azure AD, and finally convert it tooa string.
CStr(FormatDateTime(DateFromNum([pwdLastSet]),"yyyyMMddHHmmss.0Z")),
// (hello False part of IIF) Nothing toocontribute
NULL
)
```

請參閱[了解宣告式佈建運算式](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)如需有關屬性流程中的 hello 運算式語言。

### <a name="precedence"></a>優先順序
您現在已看一些個別的同步處理規則，但 hello 規則會在 hello 組態中一起運作。 在某些情況下，屬性值由多個同步處理規則 toohello 相同的目標屬性。 在此情況下，屬性優先順序是使用的 toodetermine wins 用屬性。 例如，查看 hello 屬性 sourceAnchor。 這個屬性是無法在 tooAzure AD toosign 重要屬性 toobe。 您可以在兩個不同的同步處理規則中看到此屬性的屬性流程：**In from AD – User AccountEnabled** 和 **In from AD – User Common**。 由於 tooSynchronization 規則優先順序，hello sourceAnchor 屬性被由 hello 樹系中使用已啟用的帳戶第一次當有數個物件聯結的 toohello metaverse 物件。 如果已啟用的帳戶，則 hello 同步處理引擎會使用 hello 所有同步處理規則**中 from AD – User Common**。 此組態可確保即使是已停用的帳戶，仍有 sourceAnchor。

![同步處理規則 (輸入)](./media/active-directory-aadconnectsync-understanding-default-configuration/syncrulesinbound.png)

同步處理規則的 hello 優先順序是由 hello 安裝精靈設定群組中。 在群組中的所有規則都有 hello 名稱相同，但它們所連接的連接的 toodifferent 目錄。 hello 安裝精靈會讓 hello 規則**中 from AD – User Join**最高優先順序，且它會逐一查看所有連接的 AD 目錄。 接著會繼續與 hello 下一步 群組中預先定義的順序的規則。 群組內，hello 規則會加入 hello 順序 hello hello 精靈中所加入的連接器。 如果透過 hello 精靈加入另一個連接器，hello 同步處理規則已重新排列和每個群組中最後插入 hello 新連接器的規則。

### <a name="putting-it-all-together"></a>總整理
我們現在充分瞭解同步處理規則 toobe 無法 toounderstand hello 組態以 hello 的運作方式不同的同步處理規則。 如果您查詢的使用者和 hello 屬性會造成 toohello metaverse，hello 規則會套用順序的 hello:

| 名稱 | 註解 |
|:--- |:--- |
| In from AD - User Join |聯結連接器空間物件與 Metaverse 的規則。 |
| In from AD – UserAccount Enabled |登入 tooAzure AD 和 Office 365 所需的屬性。 我們想要從啟用的 hello 帳戶的這些屬性。 |
| In from AD – User Common from Exchange |Hello 全域通訊清單中找到的屬性。 我們假設 hello 資料品質最佳 hello 我們已在此找到 hello 使用者信箱的樹系中。 |
| In from AD – User Common |Hello 全域通訊清單中找到的屬性。 如果找不到信箱，任何聯結的物件都可以構成 hello 屬性值。 |
| In from AD – User Exchange |只有在偵測到 Exchange 後才存在。 它會流送所有基礎結構 Exchange 屬性。 |
| In from AD – User Lync |只有在偵測到 Lync 後才存在。 它會流送所有基礎結構 Lync 屬性。 |

## <a name="next-steps"></a>後續步驟
* 深入了解 hello 組態模型[了解宣告式佈建](active-directory-aadconnectsync-understanding-declarative-provisioning.md)。
* 如需詳細資訊中的 hello 運算式語言[了解宣告式佈建運算式](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)。
* 繼續閱讀 hello 鶈蜪組態中的運作方式[了解使用者和連絡人](active-directory-aadconnectsync-understanding-users-and-contacts.md)
* 請參閱 toomake 實際變更使用中的宣告式佈建[toomake 變更 toohello 預設組態的方式](active-directory-aadconnectsync-change-the-configuration.md)。

**概觀主題**

* [Azure AD Connect 同步處理：了解及自訂同步處理](active-directory-aadconnectsync-whatis.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)

