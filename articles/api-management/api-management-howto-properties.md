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
# <a name="how-toouse-properties-in-azure-api-management-policies"></a><span data-ttu-id="b8166-103">如何在 Azure API 管理原則中的 toouse 屬性</span><span class="sxs-lookup"><span data-stu-id="b8166-103">How toouse properties in Azure API Management policies</span></span>
<span data-ttu-id="b8166-104">API 管理原則是 hello 的透過組態 API toochange hello 行為允許 hello publisher 的 hello 系統的強大功能。</span><span class="sxs-lookup"><span data-stu-id="b8166-104">API Management policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="b8166-105">原則是循序 hello 要求上執行的陳述式的集合或應用程式開發介面的回應。</span><span class="sxs-lookup"><span data-stu-id="b8166-105">Policies are a collection of statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="b8166-106">原則陳述可以使用引述的文字、值、原則運算式及屬性來建構。</span><span class="sxs-lookup"><span data-stu-id="b8166-106">Policy statements can be constructed using literal text values, policy expressions, and properties.</span></span> 

<span data-ttu-id="b8166-107">每個 API 管理服務執行個體有一個屬性集合的全域 toohello 服務執行個體索引鍵/值組。</span><span class="sxs-lookup"><span data-stu-id="b8166-107">Each API Management service instance has a properties collection of key/value pairs that are global toohello service instance.</span></span> <span data-ttu-id="b8166-108">這些屬性可以跨所有應用程式開發介面設定和原則是使用的 toomanage 常數字串值。</span><span class="sxs-lookup"><span data-stu-id="b8166-108">These properties can be used toomanage constant string values across all API configuration and policies.</span></span> <span data-ttu-id="b8166-109">每個屬性具有下列屬性的 hello。</span><span class="sxs-lookup"><span data-stu-id="b8166-109">Each property has hello following attributes.</span></span>

| <span data-ttu-id="b8166-110">屬性</span><span class="sxs-lookup"><span data-stu-id="b8166-110">Attribute</span></span> | <span data-ttu-id="b8166-111">類型</span><span class="sxs-lookup"><span data-stu-id="b8166-111">Type</span></span> | <span data-ttu-id="b8166-112">說明</span><span class="sxs-lookup"><span data-stu-id="b8166-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b8166-113">Name</span><span class="sxs-lookup"><span data-stu-id="b8166-113">Name</span></span> |<span data-ttu-id="b8166-114">字串</span><span class="sxs-lookup"><span data-stu-id="b8166-114">string</span></span> |<span data-ttu-id="b8166-115">hello hello 屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="b8166-115">hello name of hello property.</span></span> <span data-ttu-id="b8166-116">只能包含字母、數字、句點、破折號和底線字元。</span><span class="sxs-lookup"><span data-stu-id="b8166-116">It may contain only letters, digits, period, dash, and underscore characters.</span></span> |
| <span data-ttu-id="b8166-117">值</span><span class="sxs-lookup"><span data-stu-id="b8166-117">Value</span></span> |<span data-ttu-id="b8166-118">字串</span><span class="sxs-lookup"><span data-stu-id="b8166-118">string</span></span> |<span data-ttu-id="b8166-119">hello hello 屬性值。</span><span class="sxs-lookup"><span data-stu-id="b8166-119">hello value of hello property.</span></span> <span data-ttu-id="b8166-120">不能是空白或只由空白字元組成。</span><span class="sxs-lookup"><span data-stu-id="b8166-120">It may not be empty or consist only of whitespace.</span></span> |
| <span data-ttu-id="b8166-121">Secret</span><span class="sxs-lookup"><span data-stu-id="b8166-121">Secret</span></span> |<span data-ttu-id="b8166-122">布林值</span><span class="sxs-lookup"><span data-stu-id="b8166-122">boolean</span></span> |<span data-ttu-id="b8166-123">決定是否 hello 值是密碼，以及應該加密。</span><span class="sxs-lookup"><span data-stu-id="b8166-123">Determines whether hello value is a secret and should be encrypted or not.</span></span> |
| <span data-ttu-id="b8166-124">標記</span><span class="sxs-lookup"><span data-stu-id="b8166-124">Tags</span></span> |<span data-ttu-id="b8166-125">字串陣列</span><span class="sxs-lookup"><span data-stu-id="b8166-125">array of string</span></span> |<span data-ttu-id="b8166-126">選擇性標記，提供可使用的 toofilter hello 屬性清單時。</span><span class="sxs-lookup"><span data-stu-id="b8166-126">Optional tags that when provided can be used toofilter hello property list.</span></span> |

<span data-ttu-id="b8166-127">屬性在 hello hello 發行者入口網站中設定**屬性** 索引標籤。在下列範例的 hello，會設定三個屬性。</span><span class="sxs-lookup"><span data-stu-id="b8166-127">Properties are configured in hello publisher portal on hello **Properties** tab. In hello following example, three properties are configured.</span></span>

![屬性][api-management-properties]

<span data-ttu-id="b8166-129">屬性值可以包含常值字串及 [原則運算式](https://msdn.microsoft.com/library/azure/dn910913.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b8166-129">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span></span> <span data-ttu-id="b8166-130">hello 下表顯示 hello 先前的三個範例屬性和其屬性。</span><span class="sxs-lookup"><span data-stu-id="b8166-130">hello following table shows hello previous three sample properties and their attributes.</span></span> <span data-ttu-id="b8166-131">hello 值`ExpressionProperty`是可傳回字串，包含的原則運算式 hello 目前日期和時間。</span><span class="sxs-lookup"><span data-stu-id="b8166-131">hello value of `ExpressionProperty` is a policy expression that returns a string containing hello current date and time.</span></span> <span data-ttu-id="b8166-132">hello 屬性`ContosoHeaderValue`標示為機密，因此不會顯示其值。</span><span class="sxs-lookup"><span data-stu-id="b8166-132">hello property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span></span>

| <span data-ttu-id="b8166-133">名稱</span><span class="sxs-lookup"><span data-stu-id="b8166-133">Name</span></span> | <span data-ttu-id="b8166-134">值</span><span class="sxs-lookup"><span data-stu-id="b8166-134">Value</span></span> | <span data-ttu-id="b8166-135">Secret</span><span class="sxs-lookup"><span data-stu-id="b8166-135">Secret</span></span> | <span data-ttu-id="b8166-136">標記</span><span class="sxs-lookup"><span data-stu-id="b8166-136">Tags</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b8166-137">ContosoHeader</span><span class="sxs-lookup"><span data-stu-id="b8166-137">ContosoHeader</span></span> |<span data-ttu-id="b8166-138">TrackingId</span><span class="sxs-lookup"><span data-stu-id="b8166-138">TrackingId</span></span> |<span data-ttu-id="b8166-139">False</span><span class="sxs-lookup"><span data-stu-id="b8166-139">False</span></span> |<span data-ttu-id="b8166-140">Contoso</span><span class="sxs-lookup"><span data-stu-id="b8166-140">Contoso</span></span> |
| <span data-ttu-id="b8166-141">ContosoHeaderValue</span><span class="sxs-lookup"><span data-stu-id="b8166-141">ContosoHeaderValue</span></span> |<span data-ttu-id="b8166-142">••••••••••••••••••••••</span><span class="sxs-lookup"><span data-stu-id="b8166-142">••••••••••••••••••••••</span></span> |<span data-ttu-id="b8166-143">True</span><span class="sxs-lookup"><span data-stu-id="b8166-143">True</span></span> |<span data-ttu-id="b8166-144">Contoso</span><span class="sxs-lookup"><span data-stu-id="b8166-144">Contoso</span></span> |
| <span data-ttu-id="b8166-145">ExpressionProperty</span><span class="sxs-lookup"><span data-stu-id="b8166-145">ExpressionProperty</span></span> |<span data-ttu-id="b8166-146">@(DateTime.Now.ToString())</span><span class="sxs-lookup"><span data-stu-id="b8166-146">@(DateTime.Now.ToString())</span></span> |<span data-ttu-id="b8166-147">False</span><span class="sxs-lookup"><span data-stu-id="b8166-147">False</span></span> | |

## <a name="toouse-a-property"></a><span data-ttu-id="b8166-148">toouse 屬性</span><span class="sxs-lookup"><span data-stu-id="b8166-148">toouse a property</span></span>
<span data-ttu-id="b8166-149">toouse 原則中的屬性，對雙括號內的位置 hello 屬性名稱類似`{{ContosoHeader}}`hello 下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="b8166-149">toouse a property in a policy, place hello property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in hello following example.</span></span>

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

<span data-ttu-id="b8166-150">在此範例中，`ContosoHeader`做為標頭中的 hello 名稱`set-header`原則，和`ContosoHeaderValue`做為該標頭中的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="b8166-150">In this example, `ContosoHeader` is used as hello name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as hello value of that header.</span></span> <span data-ttu-id="b8166-151">此原則會評估要求或回應 toohello API 管理閘道器，`{{ContosoHeader}}`和`{{ContosoHeaderValue}}`其各自的屬性值取代。</span><span class="sxs-lookup"><span data-stu-id="b8166-151">When this policy is evaluated during a request or response toohello API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span></span>

<span data-ttu-id="b8166-152">屬性可用來當做完整的屬性或項目值 hello 先前範例中所示，但它們也可以插入或結合常值文字運算式的一部分，hello 下列範例所示：`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span><span class="sxs-lookup"><span data-stu-id="b8166-152">Properties can be used as complete attribute or element values as shown in hello previous example, but they can also be inserted into or combined with part of a literal text expression as shown in hello following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span></span>

<span data-ttu-id="b8166-153">屬性也可以包含原則運算式。</span><span class="sxs-lookup"><span data-stu-id="b8166-153">Properties can also contain policy expressions.</span></span> <span data-ttu-id="b8166-154">在下列範例的 hello，hello`ExpressionProperty`用。</span><span class="sxs-lookup"><span data-stu-id="b8166-154">In hello following example, hello `ExpressionProperty` is used.</span></span>

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

<span data-ttu-id="b8166-155">當評估此原則時，`{{ExpressionProperty}}` 會替代為其值 `@(DateTime.Now.ToString())`。</span><span class="sxs-lookup"><span data-stu-id="b8166-155">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span></span> <span data-ttu-id="b8166-156">由於 hello 值為原則運算式，評估 hello 運算式，以及 hello 原則會繼續執行。</span><span class="sxs-lookup"><span data-stu-id="b8166-156">Since hello value is a policy expression, hello expression is evaluated and hello policy proceeds with its execution.</span></span>

<span data-ttu-id="b8166-157">您可以在 hello 開發人員入口網站中測試時藉由呼叫包含屬性的原則在範圍內的運算。</span><span class="sxs-lookup"><span data-stu-id="b8166-157">You can test this out in hello developer portal by calling an operation that has a policy with properties in scope.</span></span> <span data-ttu-id="b8166-158">在下列範例的 hello，此作業稱為 hello 兩個先前的範例與`set-header`原則與屬性。</span><span class="sxs-lookup"><span data-stu-id="b8166-158">In hello following example, an operation is called with hello two previous example `set-header` policies with properties.</span></span> <span data-ttu-id="b8166-159">請注意 hello 回應包含兩個屬性搭配使用原則設定的自訂標頭。</span><span class="sxs-lookup"><span data-stu-id="b8166-159">Note that hello response contains two custom headers that were configured using policies with properties.</span></span>

![開發人員入口網站][api-management-send-results]

<span data-ttu-id="b8166-161">如果您看一下 hello [API 偵測器追蹤](api-management-howto-api-inspector.md)呼叫包含 hello 兩個先前範例原則使用的屬性，請參閱 hello 兩`set-header`hello 插入以及 hello 原則運算式的屬性值與原則評估 hello 屬性包含 hello 原則運算式。</span><span class="sxs-lookup"><span data-stu-id="b8166-161">If you look at hello [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes hello two previous sample policies with properties, you can see hello two `set-header` policies with hello property values inserted as well as hello policy expression evaluation for hello property that contained hello policy expression.</span></span>

![API 檢查器追蹤][api-management-api-inspector-trace]

<span data-ttu-id="b8166-163">請注意，雖然屬性值可以包含原則運算式，但屬性值不能包含其他屬性。</span><span class="sxs-lookup"><span data-stu-id="b8166-163">Note that while property values can contain policy expressions, property values can't contain other properties.</span></span> <span data-ttu-id="b8166-164">如果文字包含的屬性參考用於屬性值，例如`Property value text {{MyProperty}}`，屬性參考不會被取代，而且會納入為 hello 屬性值的一部分。</span><span class="sxs-lookup"><span data-stu-id="b8166-164">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of hello property value.</span></span>

## <a name="toocreate-a-property"></a><span data-ttu-id="b8166-165">toocreate 屬性</span><span class="sxs-lookup"><span data-stu-id="b8166-165">toocreate a property</span></span>
<span data-ttu-id="b8166-166">toocreate 屬性中，按一下**將屬性加入**上 hello**屬性** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="b8166-166">toocreate a property, click **Add property** on hello **Properties** tab.</span></span>

![新增屬性][api-management-properties-add-property-menu]

<span data-ttu-id="b8166-168">[名稱] 和 [值] 都是必要值。</span><span class="sxs-lookup"><span data-stu-id="b8166-168">**Name** and **Value** are required values.</span></span> <span data-ttu-id="b8166-169">如果這個屬性值是密碼，請檢查 hello**這是密碼**核取方塊。</span><span class="sxs-lookup"><span data-stu-id="b8166-169">If this property value is a secret, check hello **This is a secret** checkbox.</span></span> <span data-ttu-id="b8166-170">輸入一或多個選用標記 toohelp 與組織您的內容，然後按一下 **儲存**。</span><span class="sxs-lookup"><span data-stu-id="b8166-170">Enter one or more optional tags toohelp with organizing your properties, and click **Save**.</span></span>

![新增屬性][api-management-properties-add-property]

<span data-ttu-id="b8166-172">儲存新的屬性時，hello**搜尋屬性**文字方塊中會填入 hello hello 新屬性名稱，並顯示 hello 新屬性。</span><span class="sxs-lookup"><span data-stu-id="b8166-172">When a new property is saved, hello **Search property** textbox is populated with hello name of hello new property and hello new property is displayed.</span></span> <span data-ttu-id="b8166-173">所有屬性，都清除 toodisplay hello**搜尋屬性**文字方塊中，然後按 enter。</span><span class="sxs-lookup"><span data-stu-id="b8166-173">toodisplay all properties, clear hello **Search property** textbox and press enter.</span></span>

![屬性][api-management-properties-property-saved]

<span data-ttu-id="b8166-175">如需建立屬性，使用 hello REST API 的資訊，請參閱[建立屬性，使用 REST API hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put)。</span><span class="sxs-lookup"><span data-stu-id="b8166-175">For information on creating a property using hello REST API, see [Create a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span></span>

## <a name="tooedit-a-property"></a><span data-ttu-id="b8166-176">tooedit 屬性</span><span class="sxs-lookup"><span data-stu-id="b8166-176">tooedit a property</span></span>
<span data-ttu-id="b8166-177">tooedit 屬性中，按一下**編輯**hello 屬性 tooedit 旁邊。</span><span class="sxs-lookup"><span data-stu-id="b8166-177">tooedit a property, click **Edit** beside hello property tooedit.</span></span>

![編輯屬性][api-management-properties-edit]

<span data-ttu-id="b8166-179">進行想要的變更，然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="b8166-179">Make any desired changes, and click **Save**.</span></span> <span data-ttu-id="b8166-180">如果您變更 hello 屬性名稱，參考該屬性的任何原則將會自動更新的 toouse hello 新名稱。</span><span class="sxs-lookup"><span data-stu-id="b8166-180">If you change hello property name, any policies that reference that property are automatically updated toouse hello new name.</span></span>

![編輯屬性][api-management-properties-edit-property]

<span data-ttu-id="b8166-182">如需編輯該屬性使用 hello REST API 的資訊，請參閱[編輯該屬性使用 REST API hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch)。</span><span class="sxs-lookup"><span data-stu-id="b8166-182">For information on editing a property using hello REST API, see [Edit a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span></span>

## <a name="toodelete-a-property"></a><span data-ttu-id="b8166-183">toodelete 屬性</span><span class="sxs-lookup"><span data-stu-id="b8166-183">toodelete a property</span></span>
<span data-ttu-id="b8166-184">toodelete 屬性中，按一下**刪除**hello 屬性 toodelete 旁邊。</span><span class="sxs-lookup"><span data-stu-id="b8166-184">toodelete a property, click **Delete** beside hello property toodelete.</span></span>

![刪除屬性][api-management-properties-delete]

<span data-ttu-id="b8166-186">按一下**是，將它刪除**tooconfirm。</span><span class="sxs-lookup"><span data-stu-id="b8166-186">Click **Yes, delete it** tooconfirm.</span></span>

![Confirm delete][api-management-delete-confirm]

> [!IMPORTANT]
> <span data-ttu-id="b8166-188">Hello 屬性的任何原則所參考時，如果您將無法 toosuccessfully 從使用它的所有原則移除 hello 屬性之前將它刪除。</span><span class="sxs-lookup"><span data-stu-id="b8166-188">If hello property is referenced by any policies, you will be unable toosuccessfully delete it until you remove hello property from all policies that use it.</span></span>
> 
> 

<span data-ttu-id="b8166-189">如需刪除該屬性使用 hello REST API 的資訊，請參閱[刪除該屬性使用 REST API hello](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete)。</span><span class="sxs-lookup"><span data-stu-id="b8166-189">For information on deleting a property using hello REST API, see [Delete a property using hello REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span></span>

## <a name="toosearch-and-filter-properties"></a><span data-ttu-id="b8166-190">toosearch 和篩選屬性</span><span class="sxs-lookup"><span data-stu-id="b8166-190">toosearch and filter properties</span></span>
<span data-ttu-id="b8166-191">hello**屬性** 索引標籤包含搜尋和篩選功能 toohelp 管理您的屬性。</span><span class="sxs-lookup"><span data-stu-id="b8166-191">hello **Properties** tab includes searching and filtering capabilities toohelp you manage your properties.</span></span> <span data-ttu-id="b8166-192">toofilter hello 屬性清單，以屬性名稱輸入搜尋詞彙在 hello**搜尋屬性**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="b8166-192">toofilter hello property list by property name, enter a search term in hello **Search property** textbox.</span></span> <span data-ttu-id="b8166-193">所有屬性，都清除 toodisplay hello**搜尋屬性**文字方塊中，然後按 enter。</span><span class="sxs-lookup"><span data-stu-id="b8166-193">toodisplay all properties, clear hello **Search property** textbox and press enter.</span></span>

![搜尋][api-management-properties-search]

<span data-ttu-id="b8166-195">toofilter hello 屬性清單的標記值，將一個或多個標記輸入 hello**依標記篩選**文字方塊。</span><span class="sxs-lookup"><span data-stu-id="b8166-195">toofilter hello property list by tag values, enter one or more tags into hello **Filter by tags** textbox.</span></span> <span data-ttu-id="b8166-196">所有屬性，都清除 toodisplay hello**依標記篩選**文字方塊中，然後按 enter。</span><span class="sxs-lookup"><span data-stu-id="b8166-196">toodisplay all properties, clear hello **Filter by tags** textbox and press enter.</span></span>

![Filter][api-management-properties-filter]

## <a name="next-steps"></a><span data-ttu-id="b8166-198">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b8166-198">Next steps</span></span>
* <span data-ttu-id="b8166-199">深入了解原則的使用方式</span><span class="sxs-lookup"><span data-stu-id="b8166-199">Learn more about working with policies</span></span>
  * [<span data-ttu-id="b8166-200">API 管理中的原則</span><span class="sxs-lookup"><span data-stu-id="b8166-200">Policies in API Management</span></span>](api-management-howto-policies.md)
  * [<span data-ttu-id="b8166-201">原則參考文件</span><span class="sxs-lookup"><span data-stu-id="b8166-201">Policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [<span data-ttu-id="b8166-202">原則運算式</span><span class="sxs-lookup"><span data-stu-id="b8166-202">Policy expressions</span></span>](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="b8166-203">觀看影片概觀</span><span class="sxs-lookup"><span data-stu-id="b8166-203">Watch a video overview</span></span>
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

