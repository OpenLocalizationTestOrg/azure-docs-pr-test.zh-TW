---
title: "在 Azure API 管理原則中的 aaaHow toouse 屬性"
description: "深入了解如何在 Azure API 管理原則中的 toouse 屬性。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 6f39b00f-cf6e-4cef-9bf2-1f89202c0bc0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 1ff096deeb97543b48dcf1f40be9dbfcbcd09542
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-properties-in-azure-api-management-policies"></a>如何在 Azure API 管理原則中的 toouse 屬性
API 管理原則是 hello 的透過組態 API toochange hello 行為允許 hello publisher 的 hello 系統的強大功能。 原則是循序 hello 要求上執行的陳述式的集合或應用程式開發介面的回應。 原則陳述可以使用引述的文字、值、原則運算式及屬性來建構。 

每個 API 管理服務執行個體有一個屬性集合的全域 toohello 服務執行個體索引鍵/值組。 這些屬性可以跨所有應用程式開發介面設定和原則是使用的 toomanage 常數字串值。 每個屬性具有下列屬性的 hello。

| 屬性 | 類型 | 說明 |
| --- | --- | --- |
| Name |字串 |hello hello 屬性名稱。 只能包含字母、數字、句點、破折號和底線字元。 |
| 值 |字串 |hello hello 屬性值。 不能是空白或只由空白字元組成。 |
| Secret |布林值 |決定是否 hello 值是密碼，以及應該加密。 |
| 標記 |字串陣列 |選擇性標記，提供可使用的 toofilter hello 屬性清單時。 |

屬性在 hello hello 發行者入口網站中設定**屬性** 索引標籤。在下列範例的 hello，會設定三個屬性。

![屬性][api-management-properties]

屬性值可以包含常值字串及 [原則運算式](https://msdn.microsoft.com/library/azure/dn910913.aspx)。 hello 下表顯示 hello 先前的三個範例屬性和其屬性。 hello 值`ExpressionProperty`是可傳回字串，包含的原則運算式 hello 目前日期和時間。 hello 屬性`ContosoHeaderValue`標示為機密，因此不會顯示其值。

| 名稱 | 值 | Secret | 標記 |
| --- | --- | --- | --- |
| ContosoHeader |TrackingId |False |Contoso |
| ContosoHeaderValue |•••••••••••••••••••••• |True |Contoso |
| ExpressionProperty |@(DateTime.Now.ToString()) |False | |

## <a name="toouse-a-property"></a>toouse 屬性
toouse 原則中的屬性，對雙括號內的位置 hello 屬性名稱類似`{{ContosoHeader}}`hello 下列範例所示。

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

在此範例中，`ContosoHeader`做為標頭中的 hello 名稱`set-header`原則，和`ContosoHeaderValue`做為該標頭中的 hello 值。 此原則會評估要求或回應 toohello API 管理閘道器，`{{ContosoHeader}}`和`{{ContosoHeaderValue}}`其各自的屬性值取代。

屬性可用來當做完整的屬性或項目值 hello 先前範例中所示，但它們也可以插入或結合常值文字運算式的一部分，hello 下列範例所示：`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`

屬性也可以包含原則運算式。 在下列範例的 hello，hello`ExpressionProperty`用。

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

當評估此原則時，`{{ExpressionProperty}}` 會替代為其值 `@(DateTime.Now.ToString())`。 由於 hello 值為原則運算式，評估 hello 運算式，以及 hello 原則會繼續執行。

您可以在 hello 開發人員入口網站中測試時藉由呼叫包含屬性的原則在範圍內的運算。 在下列範例的 hello，此作業稱為 hello 兩個先前的範例與`set-header`原則與屬性。 請注意 hello 回應包含兩個屬性搭配使用原則設定的自訂標頭。

![開發人員入口網站][api-management-send-results]

如果您看一下 hello [API 偵測器追蹤](api-management-howto-api-inspector.md)呼叫包含 hello 兩個先前範例原則使用的屬性，請參閱 hello 兩`set-header`hello 插入以及 hello 原則運算式的屬性值與原則評估 hello 屬性包含 hello 原則運算式。

![API 檢查器追蹤][api-management-api-inspector-trace]

請注意，雖然屬性值可以包含原則運算式，但屬性值不能包含其他屬性。 如果文字包含的屬性參考用於屬性值，例如`Property value text {{MyProperty}}`，屬性參考不會被取代，而且會納入為 hello 屬性值的一部分。

## <a name="toocreate-a-property"></a>toocreate 屬性
toocreate 屬性中，按一下**將屬性加入**上 hello**屬性** 索引標籤。

![新增屬性][api-management-properties-add-property-menu]

[名稱] 和 [值] 都是必要值。 如果這個屬性值是密碼，請檢查 hello**這是密碼**核取方塊。 輸入一或多個選用標記 toohelp 與組織您的內容，然後按一下 **儲存**。

![新增屬性][api-management-properties-add-property]

儲存新的屬性時，hello**搜尋屬性**文字方塊中會填入 hello hello 新屬性名稱，並顯示 hello 新屬性。 所有屬性，都清除 toodisplay hello**搜尋屬性**文字方塊中，然後按 enter。

![屬性][api-management-properties-property-saved]

如需建立屬性，使用 hello REST API 的資訊，請參閱[建立屬性，使用 REST API hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put)。

## <a name="tooedit-a-property"></a>tooedit 屬性
tooedit 屬性中，按一下**編輯**hello 屬性 tooedit 旁邊。

![編輯屬性][api-management-properties-edit]

進行想要的變更，然後按一下 [儲存] 。 如果您變更 hello 屬性名稱，參考該屬性的任何原則將會自動更新的 toouse hello 新名稱。

![編輯屬性][api-management-properties-edit-property]

如需編輯該屬性使用 hello REST API 的資訊，請參閱[編輯該屬性使用 REST API hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch)。

## <a name="toodelete-a-property"></a>toodelete 屬性
toodelete 屬性中，按一下**刪除**hello 屬性 toodelete 旁邊。

![刪除屬性][api-management-properties-delete]

按一下**是，將它刪除**tooconfirm。

![Confirm delete][api-management-delete-confirm]

> [!IMPORTANT]
> Hello 屬性的任何原則所參考時，如果您將無法 toosuccessfully 從使用它的所有原則移除 hello 屬性之前將它刪除。
> 
> 

如需刪除該屬性使用 hello REST API 的資訊，請參閱[刪除該屬性使用 REST API hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete)。

## <a name="toosearch-and-filter-properties"></a>toosearch 和篩選屬性
hello**屬性** 索引標籤包含搜尋和篩選功能 toohelp 管理您的屬性。 toofilter hello 屬性清單，以屬性名稱輸入搜尋詞彙在 hello**搜尋屬性**文字方塊。 所有屬性，都清除 toodisplay hello**搜尋屬性**文字方塊中，然後按 enter。

![搜尋][api-management-properties-search]

toofilter hello 屬性清單的標記值，將一個或多個標記輸入 hello**依標記篩選**文字方塊。 所有屬性，都清除 toodisplay hello**依標記篩選**文字方塊中，然後按 enter。

![Filter][api-management-properties-filter]

## <a name="next-steps"></a>後續步驟
* 深入了解原則的使用方式
  * [API 管理中的原則](api-management-howto-policies.md)
  * [原則參考文件](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [原則運算式](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a>觀看影片概觀
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Use-Properties-in-Policies/player]
> 
> 

[api-management-properties]: ./media/api-management-howto-properties/api-management-properties.png
[api-management-properties-add-property]: ./media/api-management-howto-properties/api-management-properties-add-property.png
[api-management-properties-edit-property]: ./media/api-management-howto-properties/api-management-properties-edit-property.png
[api-management-properties-add-property-menu]: ./media/api-management-howto-properties/api-management-properties-add-property-menu.png
[api-management-properties-property-saved]: ./media/api-management-howto-properties/api-management-properties-property-saved.png
[api-management-properties-delete]: ./media/api-management-howto-properties/api-management-properties-delete.png
[api-management-properties-edit]: ./media/api-management-howto-properties/api-management-properties-edit.png
[api-management-delete-confirm]: ./media/api-management-howto-properties/api-management-delete-confirm.png
[api-management-properties-search]: ./media/api-management-howto-properties/api-management-properties-search.png
[api-management-send-results]: ./media/api-management-howto-properties/api-management-send-results.png
[api-management-properties-filter]: ./media/api-management-howto-properties/api-management-properties-filter.png
[api-management-api-inspector-trace]: ./media/api-management-howto-properties/api-management-api-inspector-trace.png

