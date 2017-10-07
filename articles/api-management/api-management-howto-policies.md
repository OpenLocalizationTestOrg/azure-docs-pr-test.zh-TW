---
title: "在 Azure API 管理 aaaPolicies |Microsoft 文件"
description: "了解如何編輯 toocreate，，和在 API 管理中設定原則。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 537e5caf-708b-430e-a83f-72b70af28aa9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 9ab0f884a655004cb10c05085034df1795f512e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="policies-in-azure-api-management"></a>Azure API 管理中的原則
在 Azure API 管理中，原則就是 hello 的允許 hello 發行者透過組態 API toochange hello 行為的 hello 系統的強大功能。 原則是循序 hello 要求上執行的陳述式的集合或應用程式開發介面的回應。 受歡迎的陳述式包含從 XML tooJSON 格式轉換，並呼叫速率限制為開發人員的來電 toorestrict hello 數量。 更多原則是可用的 hello 方塊。

請參閱 hello[原則參考][ Policy Reference]原則陳述式和其設定的完整清單。

Hello API 取用者之間受管理的 hello API 位於 hello 閘道內會套用原則。 hello 閘道接收的所有要求和通常不變，與轉送 toohello 基礎應用程式開發介面。 但是原則可以套用變更 tooboth hello 輸入的要求和傳出的回應。

除非另外指定 hello 原則，可以使用原則運算式做為屬性值或任何 hello API 管理原則中的文字值。 某些原則，例如 hello[控制流程][ Control flow]和[設定變數][ Set variable]原則為基礎的原則運算式。 如需詳細資訊，請參閱[進階原則][Advanced policies]和[原則運算式][Policy expressions]。

## <a name="scopes"></a>如何 tooconfigure 原則
全域或 hello 範圍可以設定原則[產品][Product]， [API] [ API]或[作業][Operation]. tooconfigure 原則中，瀏覽 toohello hello 發行者入口網站中的原則編輯器。

![Policies menu][policies-menu]

hello 原則編輯器 」 包含三個主要區段： hello 原則範圍 （頂端），hello 原則定義 （左） 編輯原則而 hello 陳述式清單 （右）：

![Policies editor][policies-editor]

設定的原則，您必須先選取應該套用原則的 hello 在 hello 範圍 toobegin。 在 hello 螢幕擷取畫面下方 hello**入門**選取產品時。 注意該 hello 正方形符號 下一步 toohello 原則名稱表示已經在此層級套用原則。

![Scope][policies-scope]

已套用原則，因為 hello 組態所示 hello 定義檢視中。

![設定][policies-configure]

hello 原則會顯示唯讀狀態一開始。 在訂單 tooedit hello 定義按一下 hello**設定原則**動作。

![Edit][policies-edit]

hello 原則定義是簡單的 XML 文件描述輸入和輸出的陳述式的序列。 hello XML 可以直接在 hello 定義 視窗中編輯。 陳述式的清單是提供權限 toohello 和陳述式適用的 toohello 目前範圍都已啟用，並反白顯示。hello 所示**限制呼叫率**hello 上方螢幕擷取畫面中的陳述式。

按一下 已啟用的陳述式會將 hello hello hello 定義檢視中的 hello 游標位置上適當的 XML。 

> [!NOTE]
> 如果您想 tooadd hello 原則未啟用，請確定您是在該原則的 hello 正確範圍。 每個原則陳述式都是針對在特定範圍和原則區段中使用所設計。 tooreview hello 原則區段和領域的原則，請檢查 hello**使用量**區段，該原則在 hello[原則參考][Policy Reference]。
> 
> 

原則陳述式的完整清單以及其設定位於 hello[原則參考][Policy Reference]。

比方說，tooadd 新的陳述式 toorestrict 連入要求 toospecified IP 位址時，將 hello hello 內容之內 hello 游標`inbound`XML 項目，然後按一下 hello**限制呼叫端 Ip**陳述式。

![Restriction policies][policies-restrict]

這樣會加入 XML 程式碼片段 toohello `inbound` tooconfigure hello 陳述式的方式提供指引的項目。

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

toolimit 傳入要求，並接受只有來自 IP 位址的 1.2.3.4 修改 hello XML，如下所示：

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![儲存][policies-save]

完成後設定 hello 陳述式中的 hello 原則，請按一下**儲存**與 hello 變更將傳播的 toohello API 管理閘道器立即。

## <a name="sections"> </a>了解原則組態
原則是針對要求和回應而依序執行的一連串陳述式。 hello 組態會分成適當`inbound`， `backend`， `outbound`，和`on-error`區段 hello 下列組態所示。

```xml
<policies>
  <inbound>
    <!-- statements toobe applied toohello request go here -->
  </inbound>
  <backend>
    <!-- statements toobe applied before hello request is forwarded too
         hello backend service go here -->
  </backend>
  <outbound>
    <!-- statements toobe applied toohello response go here -->
  </outbound>
  <on-error>
    <!-- statements toobe applied if there is an error condition go here -->
  </on-error>
</policies> 
```

如果 hello 處理要求期間發生錯誤時，任何剩餘步驟 hello `inbound`， `backend`，或`outbound`會略過區段，並執行跳 toohello 陳述式中 hello `on-error` > 一節。 將原則陳述式放在 hello `on-error` > 一節，您可以使用 hello 檢閱 hello 錯誤`context.LastError`屬性，檢查及自訂 hello 錯誤回應使用 hello`set-body`原則，並設定發生錯誤時，會發生什麼事。 有內建的步驟和 hello 原則陳述式處理期間可能發生之錯誤的錯誤碼。 如需詳細資訊，請參閱 [API 管理原則中的錯誤處理方式](https://msdn.microsoft.com/library/azure/mt629506.aspx)。

因為原則可以指定在不同的層級 （全域、 產品、 api 和操作） hello 組態的方式為您提供 toospecify hello 順序方面 toohello 父原則執行所在 hello 原則定義的陳述式。 

原則範圍的評估順序的 hello。

1. 全域範圍
2. 產品範圍
3. API 範圍
4. 作業範圍

hello 評估陳述式中的，根據 hello toohello 放置`base`項目，如果有的話。 全域原則有沒有父原則並使用 hello`<base>`中它的項目沒有任何作用。

比方說，如果在 hello 全域層級和應用程式開發介面所設定的原則的原則，然後使用該特定 API 時這兩項原則會套用。 API 管理可讓您透過 hello 基底項目組合的原則陳述式的具決定性排序。 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

在 hello 範例原則定義上述 hello`cross-domain`陳述式會執行任何更高的原則可開啟，後面跟著 hello 之前`find-and-replace`原則。 

按一下 [toosee hello 原則編輯器] 中的 hello 目前範圍中的 hello 原則**重新計算選取範圍的有效原則**。

## <a name="next-steps"></a>後續步驟
請查看有關原則運算式的下列影片。

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Policy Reference]: api-management-policy-reference.md
[Product]: api-management-howto-add-products.md
[API]: api-management-howto-add-products.md#add-apis 
[Operation]: api-management-howto-add-operations.md

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx

[policies-menu]: ./media/api-management-howto-policies/api-management-policies-menu.png
[policies-editor]: ./media/api-management-howto-policies/api-management-policies-editor.png
[policies-scope]: ./media/api-management-howto-policies/api-management-policies-scope.png
[policies-configure]: ./media/api-management-howto-policies/api-management-policies-configure.png
[policies-edit]: ./media/api-management-howto-policies/api-management-policies-edit.png
[policies-restrict]: ./media/api-management-howto-policies/api-management-policies-restrict.png
[policies-save]: ./media/api-management-howto-policies/api-management-policies-save.png
