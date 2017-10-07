---
title: "Azure AD Connect：了解宣告式佈建 | Microsoft Docs"
description: "說明 hello 宣告式佈建組態模型在 Azure AD Connect。"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: cfbb870d-be7d-47b3-ba01-9e78121f0067
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: f11e078f0aafacf94d69f0726ae41629a8470336
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-understanding-declarative-provisioning"></a>Azure AD Connect 同步處理：了解宣告式佈建
本主題說明在 Azure AD Connect 的 hello 組態模型。 hello 模型稱為宣告式佈建，並可讓您 toomake 就能輕鬆變更的設定。 本主題中所述的許多項目都是進階的，而且在大部分客戶案例中並非必要。

## <a name="overview"></a>概觀
宣告式佈建，是處理來自已連接的來源目錄的物件，並決定如何從來源 tooa 目標轉換 hello 物件和屬性。 同步管線中處理物件和 hello 管線輸入和輸出規則是 hello 相同。 輸入的規則是從連接器空間 toohello metaverse，輸出規則為 hello metaverse tooa 連接器空間。

![同步處理管線](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/sync1.png)  

hello 管線有數個不同的模組。 每個模組負責物件同步處理中的一個概念。

![同步處理管線](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/pipeline.png)  

* 來源，hello 來源物件
* [範圍](#scope)：尋找所有適用的同步處理規則
* [聯結](#join)：判斷連接器空間和 Metaverse 之間的關聯性
* [轉換](#transform)：計算屬性應如何轉換和流動
* [優先順序](#precedence)：解決衝突的屬性貢獻
* Hello 目標物件的目標，

## <a name="scope"></a>Scope
hello 範圍模組所評估的物件，並判斷 hello 規則範圍中，而且應該包含在 hello 處理。 Hello hello 物件上的屬性值，根據不同的同步處理規則會評估的 toobe 範圍中。 例如，沒有 Exchange 信箱的已停用使用者會有不同於具有信箱的已啟用使用者的規則。  
![Scope](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/scope1.png)  

hello 範圍定義為群組和子句。 hello 子句是位於群組內部。 邏輯 AND 使用於群組中的所有子句之間。 例如，(department =IT AND country = Denmark)。 邏輯 OR 使用於群組之間。

![Scope](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/scope2.png)  
在此圖中的 hello 範圍應該會讀取成 (部門 = IT 和國家/地區 = 丹麥) 或者 (國家/地區 = 瑞典)。 如果是群組 1 」 或 「 群組 2，評估的 tootrue hello 規則位於範圍內。

hello 範圍模組支援下列作業的 hello。

| 作業 | 說明 |
| --- | --- |
| EQUAL、NOTEQUAL |如果值為 hello 屬性中的相等 toohello 值會評估字串比較。 若為多重值屬性，請參閱 ISIN 和 ISNOTIN。 |
| LESSTHAN、LESSTHAN_OR_EQUAL |如果值是評估結果的字串比較符號的 hello hello 屬性中的值。 |
| CONTAINS、NOTCONTAINS |如果值可以某個位置中找到值 hello 屬性中會評估字串比較。 |
| STARTSWITH、NOTSTARTSWITH |如果值是以 hello 開頭 hello hello 屬性中的值會評估字串比較。 |
| ENDSWITH、NOTENDSWITH |評估如果值為 hello 最後 hello 屬性中的 hello 值的字串比較。 |
| GREATERTHAN、GREATERTHAN_OR_EQUAL |評估值是否大於 hello 屬性中的 hello 值的字串比較。 |
| ISNULL、ISNOTNULL |評估 hello 屬性不存在，如果從 hello 物件。 如果 hello 屬性不存在，因此 null hello 規則位於範圍內。 |
| ISIN、ISNOTIN |評估 hello 值是否存在於 hello 定義屬性。 這項作業是等號和不等於的 hello 多重值的變數。 hello 屬性應該 toobe 多重值屬性，且如果在任何 hello 屬性值中找不到 hello 值，然後 hello 規則範圍中。 |
| ISBITSET、ISNOTBITSET |評估是否已設定特定的位元。 例如，可以使用的 tooevaluate userAccountControl toosee hello 位元如果使用者已啟用或停用。 |
| ISMEMBEROF、ISNOTMEMBEROF |hello 值應該包含 DN tooa 群組 hello 連接器空間中。 如果 hello 物件所指定的 hello 群組的成員，hello 規則就會位於範圍內。 |

## <a name="join"></a>Join
hello 同步管線中的 hello 聯結模組負責尋找 hello 目標中的 hello hello 來源中的 hello 物件與物件之間的關聯性。 在 輸入規則，此關聯性會尋找 hello metaverse 中的關聯性 tooan 物件連接器空間中的物件。  
![聯結 cs 與 mv](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join1.png)  
hello 目標 toosee 如果中已經有物件 hello metaverse，由另一個連接器，它應該與相關聯。 例如，帳戶資源中從 hello 帳戶樹系的樹系 hello 使用者應該聯結 hello hello 資源樹系的使用者。

大部分的輸入的規則 toojoin 連接器空間物件一起 toohello 會使用聯結相同的 metaverse 物件。

hello 聯結會定義為一或多個群組。 在群組中，您有一些子句。 邏輯 AND 使用於群組中的所有子句之間。 邏輯 OR 使用於群組之間。 hello 群組會從最上層 toobottom 順序處理。 一個群組具有 hello 目標中找到一個相符的物件，會不評估其他任何聯結規則。 如果零個或多個在找到物件，處理會繼續 toohello 下的一個規則群組。 基於這個理由，hello 規則應建立 hello 大部份的 explicit 順序中第一個和更模糊 hello 結尾。  
![聯結定義](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join2.png)  
在此圖中的 hello 聯結會從最上層 toobottom 處理。 第一個 hello 同步管線會查看是否有相符項目上 employeeID。 否則，如果 hello 帳戶名稱可以使用的 toojoin hello 物件在一起，會看見 hello 第二個規則。 如果不是相符項目可能是，hello 第三個和最後一個規則是更模糊比對使用 hello 使用者名稱。

如果已評估所有聯結規則，而且不是正好一個符合項目，hello**連結類型**上 hello**描述**網頁使用。 如果此選項設定得**佈建**，則會建立 hello 目標中的新物件。  
![佈建或聯結](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/join3.png)  

一個物件應該只有一個同步處理規則具有在範圍中的聯結規則。 如果有多個同步處理規則定義了聯結，則會發生錯誤。 優先順序不使用的 tooresolve 聯結衝突。 物件必須有 「 聯結規則以 hello 屬性 tooflow 範圍中相同的輸入/輸出方向。 如果您需要 tooflow 屬性輸入和輸出 toohello 相同的物件，您必須有一個傳入與聯結的輸出同步處理規則。

嘗試 tooprovision 物件 tooa 目標連接器空間時，輸出聯結有特殊的行為。 使用的 toofirst 再試一次反向聯結 hello DN 屬性。 如果與 hello 目標連接器空間中已經有物件 hello 相同 DN，物件會聯結的 hello。

一旦新的同步處理規則進入範圍時，才會評估 hello 聯結模組。 物件已加入時，無法退出即使不再滿足 hello 聯結準則。 如果您想 toodisjoin 物件時，聯結 hello 物件的 hello 同步處理規則必須超出範圍。

### <a name="metaverse-delete"></a>Metaverse 刪除
Metaverse 物件維持只要有一個同步處理規則範圍中具有**連結類型**設定得**佈建**或**StickyJoin**。 連接器不允許新 tooprovision 時使用 StickyJoin 物件 toohello metaverse，但它已加入時，它必須先刪除 hello 來源中刪除 hello metaverse 物件。

刪除 Metaverse 物件後，所有與標示要 [佈建]  的輸出同步處理規則相關聯的物件都會標示要刪除。

## <a name="transformations"></a>轉換
hello 轉換是使用的 toodefine hello 來源 toohello 目標屬性的流程為何。 hello 流程可以有 hello 下列其中一種**流程類型**: Direct、 常數或運算式。 直接流程，讓屬性值依現狀流動，而不進行其他轉換。 常值集 hello 指定的值。 運算式使用 hello 宣告式佈建運算式語言 tooexpress 應如何 hello 轉換。 hello 詳細資料，可以找到 hello 運算式語言，在 hello[了解宣告式佈建運算式語言](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)主題。

![佈建或聯結](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/transformations1.png)  

hello**套用一次**核取方塊會定義該 hello hello 物件一開始建立時，應該只設定屬性。 比方說，這項設定可以使用的 tooset 新增的使用者物件的初始密碼。

### <a name="merging-attribute-values"></a>合併屬性值
Hello 屬性流程中設定 toodetermine 若就應該合併多重值的屬性，從數個不同的連接器。 hello 預設值是**更新**，表示具有最高優先順序的 hello 的同步處理規則應該獲勝。

![合併類型](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/mergetype.png)  

另外還有 **Merge** 和 **MergeCaseInsensitive**。 這些選項可讓您從不同來源 toomerge 值。 例如，它可以是使用的 toomerge hello 成員或 proxyAddresses 屬性從數個不同的樹系。 當您使用此選項時，所有同步處理規則範圍中的物件必須使用 hello 相同合併類型。 您不能定義從一個連接器 **Update** 和從另一個連接器 **Merge**。 如果您嘗試，您會收到錯誤。

hello 差異**合併**和**MergeCaseInsensitive**是如何 tooprocess 重複的屬性值。 hello 同步處理引擎可確保重複的值未插入 hello 目標屬性。 與**MergeCaseInsensitive**，以防不會出現 toobe 的重複值的差異。 例如，您應該不會看到兩者"SMTP:bob@contoso.com"和"smtp:bob@contoso.com"hello 目標屬性中。 **合併**只會查看在 hello 實際值和多個值只是有不同的案例可能會出現。

hello 選項**取代**hello 與相同**更新**，但不是會使用它。

### <a name="control-hello-attribute-flow-process"></a>控制 hello 屬性流程程序
多個輸入同步處理規則時設定的 toocontribute toohello 相同的 metaverse 屬性優先順序是使用的 toodetermine hello 成功者。 hello 同步處理規則，具有最高優先順序 （最小數值） 」 即將 toocontribute hello 值。 hello 相同的輸出規則的情況。 具有最高優先順序的 hello 同步處理規則獲勝] 和 [投稿 hello 值 toohello 連接的目錄。

在某些情況下，而不是提供值，hello 同步處理規則應該判斷其他規則的行為方式。 在此情況下會使用一些特殊的常值。

輸入同步處理規則，hello 常值**NULL**可以是使用的 tooindicate hello 流程有任何值 toocontribute。 具有較低優先順序的其他規則可以貢獻一個值。 如果沒有規則提供任何值，則會移除 hello metaverse 屬性。 輸出規則，如果**NULL**是 hello 最終值處理所有的同步處理規則之後, 則 hello 連接的目錄中已移除 hello 值。

常值的 hello **AuthoritativeNull**太類似**NULL**但沒有較低的優先順序規則可以提供值的 hello 差異。

屬性流程也可以使用 **IgnoreThisFlow**。 它是類似 tooNULL hello 意義上，表示沒有任何 toocontribute。 hello 差異在於它不會在 hello 目標中移除已存在的值。 像 hello 屬性流程從未發生時。

下列是一個範例：

在*出 tooAD 位使用者的 Exchange 混合式*可以找到下列流程 hello:  
`IIF([cloudSOAExchMailbox] = True,[cloudMSExchSafeSendersHash],IgnoreThisFlow)`  
這個運算式應該讀取成： 如果 hello 使用者信箱位於 Azure AD 中，然後將從 Azure AD tooAD 的 hello 屬性。 如果不是，不會流動任何項目後 tooActive 目錄。 在此情況下，它會在 AD 中保留 hello 現有的值。

### <a name="importedvalue"></a>ImportedValue
hello 函式 ImportedValue 是所有其他函式的不同，因為 hello 屬性名稱必須括在引號，而非方括號：  
`ImportedValue("proxyAddresses")`。

通常在同步處理期間屬性會使用 hello 預期的值，即使它尚未匯出或在匯出 （「 頂端 hello 塔 」） 期間收到的錯誤。 輸入同步處理會假設尚未到達已連接目錄的屬性最後還是會到達。 在某些情況下，務必 tooonly 同步處理已確認 hello 連接的目錄 （「 全像和差異匯入塔 」） 的值。

此函式的範例，請參閱 hello-現成的同步處理規則*中 from AD – User Common from Exchange*。 在混合 Exchange Exchange online 所新增的 hello 值應該只能同步處理時它已確認已成功匯出 hello 值：  
`proxyAddresses` <- `RemoveDuplicates(Trim(ImportedValue("proxyAddresses")))`

## <a name="precedence"></a>優先順序
當數個同步處理規則再試一次 toocontribute hello 相同的屬性值 toohello 目標，hello 優先順序值是使用的 toodetermine hello 成功者。 具有最高優先順序，最低數字值的 hello 規則正在 toocontribute hello 屬性衝突。

![合併類型](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/precedence1.png)  

這種排序可更精確地使用的 toodefine 屬性流程的一小部分的物件。 例如，hello 外的-方塊-規則確認的屬性從 已啟用的帳戶 (**User AccountEnabled**) 具有來自其他帳戶的優先順序。

可以定義連接器之間的優先順序。 可讓連接器使用較佳的資料 toocontribute 值第一次。

### <a name="multiple-objects-from-hello-same-connector-space"></a>從多個物件 hello 相同連接器空間
如果您有數個物件在 hello 相同的連接器空間聯結的 toohello 相同的 metaverse 物件，必須調整優先順序。 如果數個物件在範圍中是相同的 hello 同步處理規則，則 hello 同步處理引擎不能 toodetermine 優先順序。 它是模稜兩可的來源物件應該參與 hello 值 toohello metaverse。 此組態會回報為模稜兩可，即使 hello 來源中的 hello 屬性擁有 hello 相同的值。  
![多個物件聯結 toohello 相同 mv 物件](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/multiple1.png)  

此案例中，您會需要 toochange hello 範圍 hello 同步處理規則，hello 來源物件在範圍中有不同的同步處理規則。 可讓您 toodefine 不同優先順序。  
![多個物件聯結 toohello 相同 mv 物件](./media/active-directory-aadconnectsync-understanding-declarative-provisioning/multiple2.png)  

## <a name="next-steps"></a>後續步驟
* 如需詳細資訊中的 hello 運算式語言[了解宣告式佈建運算式](active-directory-aadconnectsync-understanding-declarative-provisioning-expressions.md)。
* 請參閱如何宣告式佈建須使用-蜪鎏中[了解 hello 預設組態](active-directory-aadconnectsync-understanding-default-configuration.md)。
* 請參閱 toomake 實際變更使用中的宣告式佈建[toomake 變更 toohello 預設組態的方式](active-directory-aadconnectsync-change-the-configuration.md)。
* 繼續如何使用者及連絡人中一起運作的 tooread[了解使用者和連絡人](active-directory-aadconnectsync-understanding-users-and-contacts.md)。

**概觀主題**

* [Azure AD Connect 同步處理：了解及自訂同步處理](active-directory-aadconnectsync-whatis.md)
* [整合內部部署身分識別與 Azure Active Directory](active-directory-aadconnect.md)

**參考主題**

* [Azure AD Connect 同步處理：函式參考](active-directory-aadconnectsync-functions-reference.md)
