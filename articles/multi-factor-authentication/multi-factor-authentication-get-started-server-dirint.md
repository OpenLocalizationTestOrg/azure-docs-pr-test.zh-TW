---
title: "Azure Multi-factor Authentication 與 Active Directory 之間的 aaaDirectory 整合"
description: "這是描述 toointegrate 如何 hello Azure Multi-factor Authentication Server 與 Active Directory，因此您可以同步處理 hello 目錄的 hello Azure 多因素驗證頁面。"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: def7a534-cfb2-492a-9124-87fb1148ab1f
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/16/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: fbff518b4641010d5f7745096e0ff658864d0805
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="directory-integration-between-azure-mfa-server-and-active-directory"></a>Azure MFA Server 與 Active Directory 之間的目錄整合
使用 Active Directory 或其他 LDAP 目錄的 hello Azure MFA Server toointegrate hello 目錄整合 區段。 您可以設定屬性 toomatch hello 目錄結構描述，以及設定使用者自動同步處理。

## <a name="settings"></a>設定
根據預設，hello Azure Multi-factor Authentication (MFA) 伺服器是設定的 tooimport，或從 Active Directory 同步處理使用者。  hello 目錄整合 索引標籤可讓您 toooverride hello 預設行為和 toobind tooa 不同 LDAP 目錄、 ADAM 目錄或特定 Active Directory 網域控制站。  它也會提供用於 LDAP 驗證 tooproxy LDAP 的 hello 或 LDAP 繫結作為 RADIUS 目標，IIS 驗證] 或 [使用者入口網站的主要驗證的預先驗證。  hello 下表描述 hello 個別設定。

![設定](./media/multi-factor-authentication-get-started-server-dirint/dirint.png)

| 功能 | 說明 |
| --- | --- |
| 使用 Active Directory |選取 hello 使用 Active Directory 選項 toouse Active Directory 匯入和同步處理。  這是 hello 預設設定。 <br>注意： Active Directory 整合 toowork 正常運作，聯結 hello 電腦 tooa 網域，以網域帳戶登入。 |
| 包含受信任的網域 |請檢查**包含信任的網域**toohave hello 代理程式嘗試 tooconnect toodomains 信任 hello 目前的網域、 另一個 hello 樹系中的網域或樹系信任中相關的網域。  時未匯入或同步處理使用者從任何 hello 受信任的網域，請取消核取 [hello] 核取方塊 tooimprove 效能。  hello 預設為選取狀態。 |
| 使用特定 LDAP 組態 |選取 hello 使用 LDAP 選項 toouse hello 指定 LDAP 設定匯入和同步處理。 注意： 當選取 [使用 LDAP] 時，hello 使用者介面變更參考從 Active Directory tooLDAP。 |
| [編輯] 按鈕 |hello [編輯] 按鈕可讓 hello 目前 LDAP 組態設定 toomodified。 |
| 使用屬性範圍查詢 |指出是否應該使用屬性範圍查詢。  屬性範圍查詢允許有效率的目錄搜尋可用記錄根據另一個記錄屬性中的 hello 項目。  hello Azure Multi-factor Authentication Server 會使用屬性範圍查詢 tooefficiently 查詢 hello 使用者安全性群組的成員。   <br>注意：在某些情況下，雖然支援屬性範圍查詢，但卻不應該使用。  比方說，當安全性群組包含來自多個網域的成員時，Active Directory 的屬性範圍查詢可能會有問題。 在此情況下，請取消選取 [hello] 核取方塊。 |

hello 下表描述 hello LDAP 組態設定。

| 功能 | 說明 |
| --- | --- |
| 伺服器 |輸入 hello 主機名稱或執行 hello LDAP 目錄的 hello 伺服器的 IP 位址。  也可以指定備份伺服器 (以分號隔開)。 <br>注意：當 [繫結類型] 是 [SSL] 時，需要完整主機名稱。 |
| 基準 DN |輸入 hello 從中啟動所有目錄查詢 hello 基準目錄物件的辨別的名稱。  例如，dc=abc,dc=com。 |
| 繫結類型 - 查詢 |繫結 toosearch hello LDAP 目錄時，請選取使用 hello 適當繫結類型。  這用於匯入、同步處理和使用者名稱解析。 <br><br>  匿名 - 執行匿名繫結。  不會使用繫結 DN 和繫結密碼。  這只適用於 hello LDAP 目錄允許匿名繫結，而且權限允許 hello 查詢 hello 適當記錄和屬性。  <br><br> 簡單-繫結 DN 和繫結密碼會傳遞做為純文字 toobind toohello LDAP 目錄。  這是基於測試目的，可以達到 hello 伺服器的 tooverify 和該 hello 繫結帳戶具有 hello 適當的存取權。 Hello 適當的憑證安裝完成後，請改為使用 SSL。  <br><br> SSL 的繫結 DN 和繫結密碼會加密使用 SSL toobind toohello LDAP 目錄。  安裝的憑證在本機的 hello LDAP 目錄信任。  <br><br> Windows-繫結使用者名稱和繫結密碼是使用的 toosecurely 連接 tooan Active Directory 網域控制站或 ADAM 目錄。  如果繫結使用者名稱保留空白，hello 登入的使用者帳戶是使用的 toobind。 |
| 繫結類型 - 驗證 |執行 LDAP 繫結驗證時，請選取使用 hello 適當繫結類型。  請參閱底下的繫結類型-查詢 hello 繫結類型描述。  比方說，這允許匿名繫結 toobe SSL 繫結使用的 toosecure LDAP 繫結驗證時，用來進行查詢。 |
| 繫結 DN 或繫結使用者名稱 |繫結 toohello LDAP 目錄時，請輸入 hello 辨別的名稱 hello 使用者記錄 hello 帳戶 toouse。<br><br>僅在繫結類型為簡單或 SSL 時，會使用 hello 繫結辨別的名稱。  <br><br>繫結類型為 Windows，繫結 toohello LDAP 目錄時，請輸入 hello Windows 帳戶 toouse hello 使用者名稱。  如果保留空白，hello 登入之使用者的帳戶是使用的 toobind。 |
| 繫結密碼 |輸入 hello 繫結密碼 hello 繫結 DN 或使用者正在使用的 toobind toohello LDAP 目錄的名稱。  hello Multi-factor Auth Server AdSync Service 的 tooconfigure hello 密碼啟用同步處理，並確定 hello 服務正在執行 hello 本機電腦上。  hello 密碼被儲存 hello 帳戶 hello Multi-factor Auth Server AdSync 服務正在執行做為在 hello Windows 預存使用者名稱和密碼。  hello 密碼也會儲存在 hello 帳戶 hello Multi-factor Auth Server 使用者介面正在執行做為，並在 hello 帳戶 hello Multi-factor Auth Server 服務正在執行做為下。  <br><br>Hello 密碼僅儲存在 hello 本機伺服器的 Windows 預存使用者名稱和密碼，因為重複此步驟需要存取 toohello 密碼每個 Multi-factor Auth Server 上。 |
| 查詢大小限制 |指定 hello hello 的目錄搜尋將傳回的使用者數目上限的大小限制。  此限制應符合 hello hello LDAP 目錄上的組態。  針對不支援分頁的大型搜尋，匯入和同步處理會嘗試分批 tooretrieve 使用者。  如果這裡大於 hello LDAP 目錄上設定的 hello 限制時，指定 hello 大小限制，可能會遺漏某些使用者。 |
| 測試按鈕 |按一下**測試**tootest 繫結 toohello LDAP 伺服器。  <br><br>您不需要 tooselect hello**使用 LDAP**選項 tootest 繫結。 這可讓您使用 hello LDAP 設定之前，測試 hello 繫結 toobe。 |

## <a name="filters"></a>篩選器
篩選可讓您 tooset 準則 tooqualify 記錄時執行目錄搜尋。  您可以透過設定 hello 篩選器來設定領域 hello 物件想 toosynchronize。  

![篩選器](./media/multi-factor-authentication-get-started-server-dirint/dirint2.png)

Azure Multi-factor Authentication 有下列三個篩選選項的 hello:

* **容器篩選器**-指定使用 tooqualify 容器記錄 hello 篩選條件時執行目錄搜尋。  對於 Active Directory 和 ADAM，通常會使用 (|(objectClass=organizationalUnit)(objectClass=container))。  對於其他 LDAP 目錄，使用容器物件，視 hello 目錄結構描述的每一種類型的篩選準則。  <br>注意：如果空白，預設會使用 ((objectClass=organizationalUnit)(objectClass=container))。
* **安全性群組篩選器**-指定使用 tooqualify 安全性群組記錄 hello 篩選條件時執行目錄搜尋。  對於 Active Directory 和 ADAM，通常會使用 (&(objectCategory=group)(groupType:1.2.840.113556.1.4.804:=-2147483648))。  對於其他 LDAP 目錄，使用每一種安全性群組物件，視 hello 目錄結構描述篩選準則。  <br>注意：如果空白，預設會使用 (&(objectCategory=group)(groupType:1.2.840.113556.1.4.804:=-2147483648))。
* **使用者篩選器**-指定使用 tooqualify 使用者資料錄 hello 篩選條件時執行目錄搜尋。  對於 Active Directory 和 ADAM，通常會使用 (&(objectClass=user)(objectCategory=person))。  對於其他 LDAP 目錄，使用 (objectClass = inetOrgPerson) 或其他類似，視 hello 目錄結構描述。 <br>注意：如果空白，預設會使用 (&(objectCategory=person)(objectClass=user))。

## <a name="attributes"></a>屬性
您可以視需要自訂特定目錄的屬性。  這可讓您 tooadd 自訂屬性，以及微調 hello 同步 tooonly hello 屬性所需。 每個屬性欄位的 hello 值 hello 目錄結構描述中定義，請使用 hello attricute hello 名稱。 hello 下表提供每一項功能的其他資訊。

屬性可以手動輸入，而且不需要的 toomatch hello 屬性清單中的屬性。

![屬性](./media/multi-factor-authentication-get-started-server-dirint/dirint3.png)

| 功能 | 說明 |
| --- | --- |
| 唯一識別碼 |輸入做為容器、 安全性群組和使用者資料錄的 hello 唯一識別項的 hello 屬性 hello 屬性名稱。  在 Active Directory 中，這通常是 objectGUID。 其他 LDAP 實作可能使用 entryUUID 或類似的項目。  hello 預設值為 objectGUID。 |
| 唯一識別碼類型 |選取 hello hello 唯一識別碼屬性類型。  在 Active Directory 中，hello objectGUID 屬性為 GUID 類型。 其他 LDAP 實作可能使用 ASCII 位元組陣列或字串類型。  hello 預設值為 GUID。 <br><br>此類型正確後同步處理項目正由其唯一識別碼的重要 tooset 它。 hello 唯一識別碼類型是使用的 toodirectly 尋找 hello 物件 hello 目錄中。  Hello 目錄實際上會 hello 值儲存為 ASCII 字元的位元組陣列時，設定此類型 tooString 防止無法正常的同步處理。 |
| 辨別名稱 |輸入 hello hello 屬性包含 hello 每一筆記錄的辨別的名稱屬性名稱。  在 Active Directory 中，這通常是 distinguishedName。 其他 LDAP 實作可能使用 entryDN 或類似的項目。  hello 預設值是 distinguishedName。 <br><br>如果只包含 hello 辨別的名稱屬性不存在，會使用 hello adspath 屬性。  hello"LDAP: / /\<伺服器\>/"hello 路徑的一部分會自動除去，只保留 hello 辨別的名稱的 hello 物件。 |
| 容器名稱 |輸入包含容器記錄中的 hello 名稱 hello 屬性 hello 屬性名稱。  匯入從 Active Directory 時，將會顯示 hello 容器階層中的 hello 這個屬性的值或新增同步處理項目。  hello 預設為名稱。 <br><br>如果不同的容器使用不同的屬性做為名稱，請使用分號分隔 tooseparate 多個容器名稱屬性。  容器物件上找到的 hello 第一個容器名稱屬性是使用的 toodisplay 其名稱。 |
| 安全性群組名稱 |輸入包含安全性群組記錄中的 hello 名稱 hello 屬性 hello 屬性名稱。  hello 這個屬性的值會顯示 hello [安全性群組] 清單中，當從 Active Directory 匯入或新增同步處理項目。  hello 預設為名稱。 |
| 使用者名稱 |輸入包含使用者記錄中的 hello 使用者名稱的 hello 屬性 hello 屬性名稱。  此屬性 hello 值是用來做為 hello Multi-factor Auth Server 使用者名稱。  第二個屬性可指定為備份 toohello 第一次。  若 hello 第一個屬性未包含 hello 使用者的值，只會用於 hello 第二個屬性。  hello 預設值為 userPrincipalName 和 sAMAccountName。 |
| 名字 |輸入包含使用者記錄中的 hello 名字的 hello 屬性 hello 屬性名稱。  hello 預設值是 givenName。 |
| 姓氏 |輸入包含使用者記錄中的 hello 姓氏的 hello 屬性 hello 屬性名稱。  hello 預設值是 sn。 |
| 電子郵件地址 |輸入包含使用者記錄中的 hello 電子郵件地址的 hello 屬性 hello 屬性名稱。  電子郵件地址是使用的 toosend 歡迎和更新電子郵件 toohello 使用者。  hello 預設值是 mail。 |
| 使用者群組 |輸入包含使用者記錄中的 hello 使用者群組的 hello 屬性 hello 屬性名稱。  使用者群組可以是使用的 toofilter 使用者在 hello 代理程式和 hello Multi-factor Auth Server 管理入口網站中的報表。 |
| 說明 |輸入包含使用者記錄中的 hello 描述 hello 屬性 hello 屬性名稱。  描述只用於搜尋。  hello 預設值是 description。 |
| 通話語言 |輸入包含 hello 簡短名稱 hello 語言 toouse hello 使用者電話語音的 hello 屬性 hello 屬性名稱。 |
| 簡訊語言 |輸入包含 hello 簡短名稱之 hello 語言 toouse hello 使用者 SMS 簡訊 hello 屬性 hello 屬性名稱。 |
| 行動應用程式語言 |輸入包含 hello 簡短名稱之 hello 語言 toouse 電話 hello 使用者應用程式簡訊的 hello 屬性 hello 屬性名稱。 |
| OATH 權杖語言 |輸入包含 hello 簡短名稱之 hello 語言 toouse hello 使用者的 OATH 權杖文字訊息的 hello 屬性 hello 屬性名稱。 |
| 商務電話 |輸入包含使用者記錄中的 hello 公司電話號碼的 hello 屬性 hello 屬性名稱。  hello 預設值是 telephoneNumber。 |
| 住家電話 |輸入包含使用者記錄中的 hello 住家電話號碼的 hello 屬性 hello 屬性名稱。  hello 預設值是 homePhone。 |
| 呼叫器 |輸入包含使用者記錄中的 hello 呼叫器號碼的 hello 屬性 hello 屬性名稱。  hello 預設值是 pager。 |
| 行動電話 |輸入包含使用者記錄中的 hello 行動電話號碼的 hello 屬性 hello 屬性名稱。  hello 預設值是 mobile。 |
| 傳真 |輸入包含使用者記錄中的 hello 傳真號碼的 hello 屬性 hello 屬性名稱。  hello 預設值是 facsimileTelephoneNumber。 |
| IP 電話 |輸入包含使用者記錄中的 hello IP 電話號碼的 hello 屬性 hello 屬性名稱。  hello 預設值是 ipPhone。 |
| 自訂 |輸入包含使用者記錄中的自訂的電話號碼的 hello 屬性 hello 屬性名稱。  hello 預設值為空白。 |
| 分機 |輸入包含 hello 電話分機號碼使用者記錄中的 hello 屬性 hello 屬性名稱。  hello hello 延伸模組欄位值作為 hello 延伸 toohello 只用於主要電話號碼。  hello 預設值為空白。 <br><br>如果未指定 hello 延伸模組屬性，延伸可以是 hello 電話屬性的一部分。 在此情況下，在 'x' hello 擴充功能之前，讓它取得正確剖析。  例如，555-123-4567 x890 會導致 555-123-4567 與 hello 電話號碼而 890 則為 hello 延伸模組。 |
| [還原預設值] 按鈕 |按一下**還原成預設值**tooreturn 所有屬性都回 tootheir 預設值。  hello 預設值應該與 hello 一般 Active Directory 或 ADAM 結構描述正確運作。 |

按一下 [tooedit 屬性**編輯**hello 屬性] 索引標籤上。這會開啟視窗，您可以在其中編輯 hello 屬性。 選取 hello **...**下一步 tooany 屬性 tooopen 視窗，您可以在其中選擇哪些屬性 toodisplay。

![編輯屬性](./media/multi-factor-authentication-get-started-server-dirint/dirint4.png)

## <a name="synchronization"></a>同步處理
同步處理可讓 hello Azure MFA 的使用者資料庫與 Active Directory 或其他輕量型目錄存取通訊協定 (LDAP) 目錄中的 hello 使用者同步處理。 hello 程序是類似 tooimporting 使用者手動從 Active Directory，但定期輪詢 Active Directory 使用者和安全性群組變更 tooprocess。  它也可停用或移除已從容器、安全性群組或 Active Directory 中移除的使用者。

hello Multi-factor Auth ADSync 服務是一種 Windows 服務，會定期輪詢 Active Directory 的 hello。  這不是 toobe 與 Azure AD 同步或 Azure AD Connect 混淆。  hello Multi-factor Auth ADSync，雖然根據類似的程式碼基底，是特定 toohello Azure Multi-factor Authentication Server。  它會安裝在已停止 」 狀態，並 hello 設定時，Multi-factor Auth Server 服務啟動 toorun。  如果您有多伺服器 Multi-factor Auth Server 設定，hello Multi-factor Auth ADSync 只能在單一伺服器上執行。

hello Multi-factor Auth ADSync 服務會使用 hello Microsoft tooefficiently 輪詢變更提供的 DirSync LDAP 伺服器擴充功能。  此 DirSync 控制呼叫端必須具備 hello > 的 < 目錄取得變更向右鍵和 DS 複寫 Get-變更擴充的控制存取權限。  根據預設，這些權限會指派 toohello 網域控制站上的 Administrator 和 LocalSystem 帳戶。  hello Multi-factor Auth AdSync 服務預設以 localsystem 身分為設定的 toorun。  因此，它會是網域控制站上的最簡單 toorun hello 服務。  如果您設定 hello 服務 tooalways 執行完整同步處理，它可以執行身分帳戶與權限較低。  這樣比較沒有效率，但需要的帳戶權限較少。

如果 hello LDAP 目錄支援，而且會設定為目錄同步，然後輪詢使用者和安全性群組變更將會運作 hello 相同，但 Active Directory。  如果 hello LDAP 目錄不支援 hello DirSync 控制，在每個週期執行完整同步處理。

![同步處理](./media/multi-factor-authentication-get-started-server-dirint/dirint5.png)

hello 下表包含每個 hello 同步處理 索引標籤上設定的其他資訊。

| 功能 | 說明 |
| --- | --- |
| 啟用與 Active Directory 同步處理 |有選取時，hello Multi-factor Auth Server 服務會定期輪詢 Active Directory 的變更。 <br><br>請注意： 必須加入至少一個同步處理項目，並立即同步處理之前必須先執行 hello Multi-factor Auth Server 服務會開始處理變更。 |
| 同步處理頻率 |指定 hello 時間間隔 hello Multi-factor Auth Server 服務在輪詢與處理變更之間等候。 <br><br> 注意： 指定的 hello 間隔是 hello hello 開頭的每個循環之間的時間。  如果 hello 時間處理變更超過 hello 間隔，hello 服務將立即再次輪詢。 |
| 移除已不在 Active Directory 中的使用者 |Hello Multi-factor Auth Server 服務有選取時，將會處理 Active Directory 刪除使用者標記，並移除 hello 與相關的 Multi-factor Auth Server 使用者。 |
| 永遠執行完整同步處理 |有選取時，hello Multi-factor Auth Server 服務將一律執行完整同步處理。  未選取時，hello Multi-factor Auth Server 服務將會執行增量同步處理只會查詢已變更的使用者。  hello 預設為未選取狀態。 <br><br>未選取時，Azure MFA Server 會在 hello 目錄支援 hello DirSync 控制且 hello 帳戶繫結 toohello 目錄具有權限 tooperform DirSync 增量查詢時，僅執行增量同步處理。  如果 hello 帳戶沒有適當權限 hello 或 hello 同步處理中包含多個網域，Azure MFA Server 會執行完整同步處理。 |
| 超過 X 個使用者將停用或移除時，需要系統管理員核准 |同步處理項目可以設定的 toodisable 或移除使用者不再是 hello 項目的容器或安全性群組群組的成員。  做為保護措施，為系統管理員核准時可能會需要使用者 toodisable 或移除的 hello 數目超過臨界值。  核取時，超過指定的臨界值就需要核准。  hello 預設值為 5，hello 範圍是 1 too999。 <br><br> 核准時會先傳送電子郵件通知 tooadministrators。 hello 電子郵件通知會說明如何檢閱及核准 hello 停用和移除使用者。  啟動 hello Multi-factor Auth Server 使用者介面時，它會提示您進行核准。 |

hello**立即同步處理**按鈕可讓您 toorun hello 同步處理完整的同步處理指定的項目。  每當加入、修改、移除或重新排列同步處理項目時，就需要完整同步處理。  它也是所需的 hello Multi-factor Auth AdSync 服務可運作，因為它會設定 hello 起點從中 hello 服務輪詢增量變更。  如果已變更 toosynchronization 項目，但尚未執行完整同步處理，則會提示的 tooSynchronize 現在。

hello**移除**按鈕可讓 hello 管理員 toodelete hello Multi-factor Auth Server 同步處理項目清單中的一個或多個同步處理項目。

> [!WARNING]
> 一旦移除同步處理項目記錄就無法復原。 如果，則需要 tooadd hello 同步處理項目記錄一次不小心刪除。

hello 同步處理項目或同步處理項目已從 Multi-factor Auth Server。  hello Multi-factor Auth Server 服務將不會再處理 hello 同步處理項目。

hello 移 和 下移 按鈕可讓 hello 管理員 toochange hello hello 同步處理項目順序。  hello 順序很重要，因為 hello 同一使用者可能是一個以上的同步處理項目 （例如容器和安全性群組） 的成員。  hello 設定同步處理期間套用的 toohello 使用者將來自 hello 第一個同步處理項目 hello 清單 toowhich hello 使用者有關聯。  因此，應該依優先順序放置 hello 同步處理項目。

> [!TIP]
> 移除同步處理項目之後應該執行完整同步處理。  排序同步處理項目之後應該執行完整同步處理。  按一下**立即同步處理**tooperform 完整同步處理。

## <a name="multi-factor-auth-servers"></a>Multi-Factor Auth Server
其他的 Multi-factor Auth Server 可能設定 tooserve 做為備份 RADIUS proxy、 LDAP proxy 或是用於 IIS 驗證。 所有的 hello 代理程式之間共用 hello 同步處理設定。 不過，只有其中一個這些代理程式可能有 hello Multi-factor Auth Server 服務執行。 此索引標籤可讓您 tooselect hello 應該啟用同步處理的 Multi-factor Auth Server。

![Multi-Factor-Auth Server](./media/multi-factor-authentication-get-started-server-dirint/dirint6.png)
