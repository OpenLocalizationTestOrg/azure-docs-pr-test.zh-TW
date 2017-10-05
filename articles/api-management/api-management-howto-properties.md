---
title: "如何在 Azure API 管理原則中使用屬性"
description: "了解如何在 Azure API 管理原則中使用屬性。"
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
ms.openlocfilehash: 3b0fe2a300038e13cc488bdb4f50f8be270ea8f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-properties-in-azure-api-management-policies"></a><span data-ttu-id="54082-103">如何在 Azure API 管理原則中使用屬性</span><span class="sxs-lookup"><span data-stu-id="54082-103">How to use properties in Azure API Management policies</span></span>
<span data-ttu-id="54082-104">API 管理原則是系統的強大功能，可讓發行者透過設定來變更 API 的行為。</span><span class="sxs-lookup"><span data-stu-id="54082-104">API Management policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="54082-105">原則是陳述式的集合，會因 API 的要求或回應循序執行。</span><span class="sxs-lookup"><span data-stu-id="54082-105">Policies are a collection of statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="54082-106">原則陳述可以使用引述的文字、值、原則運算式及屬性來建構。</span><span class="sxs-lookup"><span data-stu-id="54082-106">Policy statements can be constructed using literal text values, policy expressions, and properties.</span></span> 

<span data-ttu-id="54082-107">每個 API 管理服務執行個體都有服務執行個體全域適用的之鍵/值組的屬性集合。</span><span class="sxs-lookup"><span data-stu-id="54082-107">Each API Management service instance has a properties collection of key/value pairs that are global to the service instance.</span></span> <span data-ttu-id="54082-108">這個屬性可用來管理所有 API 組態及原則的常數字串值。</span><span class="sxs-lookup"><span data-stu-id="54082-108">These properties can be used to manage constant string values across all API configuration and policies.</span></span> <span data-ttu-id="54082-109">每個屬性都有下列屬性。</span><span class="sxs-lookup"><span data-stu-id="54082-109">Each property has the following attributes.</span></span>

| <span data-ttu-id="54082-110">屬性</span><span class="sxs-lookup"><span data-stu-id="54082-110">Attribute</span></span> | <span data-ttu-id="54082-111">類型</span><span class="sxs-lookup"><span data-stu-id="54082-111">Type</span></span> | <span data-ttu-id="54082-112">說明</span><span class="sxs-lookup"><span data-stu-id="54082-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="54082-113">Name</span><span class="sxs-lookup"><span data-stu-id="54082-113">Name</span></span> |<span data-ttu-id="54082-114">string</span><span class="sxs-lookup"><span data-stu-id="54082-114">string</span></span> |<span data-ttu-id="54082-115">屬性的名稱。</span><span class="sxs-lookup"><span data-stu-id="54082-115">The name of the property.</span></span> <span data-ttu-id="54082-116">只能包含字母、數字、句點、破折號和底線字元。</span><span class="sxs-lookup"><span data-stu-id="54082-116">It may contain only letters, digits, period, dash, and underscore characters.</span></span> |
| <span data-ttu-id="54082-117">值</span><span class="sxs-lookup"><span data-stu-id="54082-117">Value</span></span> |<span data-ttu-id="54082-118">string</span><span class="sxs-lookup"><span data-stu-id="54082-118">string</span></span> |<span data-ttu-id="54082-119">屬性的值。</span><span class="sxs-lookup"><span data-stu-id="54082-119">The value of the property.</span></span> <span data-ttu-id="54082-120">不能是空白或只由空白字元組成。</span><span class="sxs-lookup"><span data-stu-id="54082-120">It may not be empty or consist only of whitespace.</span></span> |
| <span data-ttu-id="54082-121">Secret</span><span class="sxs-lookup"><span data-stu-id="54082-121">Secret</span></span> |<span data-ttu-id="54082-122">布林值</span><span class="sxs-lookup"><span data-stu-id="54082-122">boolean</span></span> |<span data-ttu-id="54082-123">決定該值是否為密碼且是否應該加密。</span><span class="sxs-lookup"><span data-stu-id="54082-123">Determines whether the value is a secret and should be encrypted or not.</span></span> |
| <span data-ttu-id="54082-124">標記</span><span class="sxs-lookup"><span data-stu-id="54082-124">Tags</span></span> |<span data-ttu-id="54082-125">字串陣列</span><span class="sxs-lookup"><span data-stu-id="54082-125">array of string</span></span> |<span data-ttu-id="54082-126">若有提供選用的標記，則可用來篩選屬性清單。</span><span class="sxs-lookup"><span data-stu-id="54082-126">Optional tags that when provided can be used to filter the property list.</span></span> |

<span data-ttu-id="54082-127">屬性是在發行者入口網站上的 [屬性]  索引標籤中設定。</span><span class="sxs-lookup"><span data-stu-id="54082-127">Properties are configured in the publisher portal on the **Properties** tab.</span></span> <span data-ttu-id="54082-128">在以下範例中，設定了三個屬性。</span><span class="sxs-lookup"><span data-stu-id="54082-128">In the following example, three properties are configured.</span></span>

![屬性][api-management-properties]

<span data-ttu-id="54082-130">屬性值可以包含常值字串及 [原則運算式](https://msdn.microsoft.com/library/azure/dn910913.aspx)。</span><span class="sxs-lookup"><span data-stu-id="54082-130">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span></span> <span data-ttu-id="54082-131">下表顯示之前的三個範例屬性和其屬性。</span><span class="sxs-lookup"><span data-stu-id="54082-131">The following table shows the previous three sample properties and their attributes.</span></span> <span data-ttu-id="54082-132">`ExpressionProperty` 的值是會傳回包含目前日期與時間之字串的運算式。</span><span class="sxs-lookup"><span data-stu-id="54082-132">The value of `ExpressionProperty` is a policy expression that returns a string containing the current date and time.</span></span> <span data-ttu-id="54082-133">`ContosoHeaderValue` 屬性已標記為密碼，所以未顯示其值。</span><span class="sxs-lookup"><span data-stu-id="54082-133">The property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span></span>

| <span data-ttu-id="54082-134">Name</span><span class="sxs-lookup"><span data-stu-id="54082-134">Name</span></span> | <span data-ttu-id="54082-135">值</span><span class="sxs-lookup"><span data-stu-id="54082-135">Value</span></span> | <span data-ttu-id="54082-136">Secret</span><span class="sxs-lookup"><span data-stu-id="54082-136">Secret</span></span> | <span data-ttu-id="54082-137">標記</span><span class="sxs-lookup"><span data-stu-id="54082-137">Tags</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="54082-138">ContosoHeader</span><span class="sxs-lookup"><span data-stu-id="54082-138">ContosoHeader</span></span> |<span data-ttu-id="54082-139">TrackingId</span><span class="sxs-lookup"><span data-stu-id="54082-139">TrackingId</span></span> |<span data-ttu-id="54082-140">False</span><span class="sxs-lookup"><span data-stu-id="54082-140">False</span></span> |<span data-ttu-id="54082-141">Contoso</span><span class="sxs-lookup"><span data-stu-id="54082-141">Contoso</span></span> |
| <span data-ttu-id="54082-142">ContosoHeaderValue</span><span class="sxs-lookup"><span data-stu-id="54082-142">ContosoHeaderValue</span></span> |<span data-ttu-id="54082-143">••••••••••••••••••••••</span><span class="sxs-lookup"><span data-stu-id="54082-143">••••••••••••••••••••••</span></span> |<span data-ttu-id="54082-144">True</span><span class="sxs-lookup"><span data-stu-id="54082-144">True</span></span> |<span data-ttu-id="54082-145">Contoso</span><span class="sxs-lookup"><span data-stu-id="54082-145">Contoso</span></span> |
| <span data-ttu-id="54082-146">ExpressionProperty</span><span class="sxs-lookup"><span data-stu-id="54082-146">ExpressionProperty</span></span> |<span data-ttu-id="54082-147">@(DateTime.Now.ToString())</span><span class="sxs-lookup"><span data-stu-id="54082-147">@(DateTime.Now.ToString())</span></span> |<span data-ttu-id="54082-148">False</span><span class="sxs-lookup"><span data-stu-id="54082-148">False</span></span> | |

## <a name="to-use-a-property"></a><span data-ttu-id="54082-149">使用屬性</span><span class="sxs-lookup"><span data-stu-id="54082-149">To use a property</span></span>
<span data-ttu-id="54082-150">若要在原則中使用屬性，請將屬性名稱放在雙大括號 (如 `{{ContosoHeader}}`) 內，如以下範例所示。</span><span class="sxs-lookup"><span data-stu-id="54082-150">To use a property in a policy, place the property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in the following example.</span></span>

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

<span data-ttu-id="54082-151">在此範例中，`ContosoHeader` 是做為 `set-header` 原則中標頭的名稱，且 `ContosoHeaderValue` 是用來做為該標頭的值。</span><span class="sxs-lookup"><span data-stu-id="54082-151">In this example, `ContosoHeader` is used as the name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as the value of that header.</span></span> <span data-ttu-id="54082-152">當此原則在對 API 管理閘道提出要求或回應管理閘道期間被評估時，`{{ContosoHeader}}` 和 `{{ContosoHeaderValue}}` 會被其各自的屬性值取代。</span><span class="sxs-lookup"><span data-stu-id="54082-152">When this policy is evaluated during a request or response to the API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span></span>

<span data-ttu-id="54082-153">如前一個範例所示，屬性可以做為完整的屬性或元素值使用，但它們也可以插入部分的常值文字運算式或與之結合，如以下範例所示： `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span><span class="sxs-lookup"><span data-stu-id="54082-153">Properties can be used as complete attribute or element values as shown in the previous example, but they can also be inserted into or combined with part of a literal text expression as shown in the following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span></span>

<span data-ttu-id="54082-154">屬性也可以包含原則運算式。</span><span class="sxs-lookup"><span data-stu-id="54082-154">Properties can also contain policy expressions.</span></span> <span data-ttu-id="54082-155">以下範例使用 `ExpressionProperty`。</span><span class="sxs-lookup"><span data-stu-id="54082-155">In the following example, the `ExpressionProperty` is used.</span></span>

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

<span data-ttu-id="54082-156">當評估此原則時，`{{ExpressionProperty}}` 會替代為其值 `@(DateTime.Now.ToString())`。</span><span class="sxs-lookup"><span data-stu-id="54082-156">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span></span> <span data-ttu-id="54082-157">因為該值是原則運算式，所以會評估運算式，且原則會繼續執行。</span><span class="sxs-lookup"><span data-stu-id="54082-157">Since the value is a policy expression, the expression is evaluated and the policy proceeds with its execution.</span></span>

<span data-ttu-id="54082-158">您可以在開發人員入口網站測試此項目，方法是呼叫在範圍內有包含屬性支援則的作業。</span><span class="sxs-lookup"><span data-stu-id="54082-158">You can test this out in the developer portal by calling an operation that has a policy with properties in scope.</span></span> <span data-ttu-id="54082-159">在下列範例中，已使用前兩個含屬性的範例 `set-header` 原則呼叫作業。</span><span class="sxs-lookup"><span data-stu-id="54082-159">In the following example, an operation is called with the two previous example `set-header` policies with properties.</span></span> <span data-ttu-id="54082-160">請注意，該回應中包含兩個已使用含屬性原則所設定的自訂標頭。</span><span class="sxs-lookup"><span data-stu-id="54082-160">Note that the response contains two custom headers that were configured using policies with properties.</span></span>

![開發人員入口網站][api-management-send-results]

<span data-ttu-id="54082-162">如果您查看包含之前兩個含屬性之範例原則的呼叫的 [API 檢查器追蹤](api-management-howto-api-inspector.md)，會看到兩個已插入屬性值的 `set-header` 原則，以及含原則運算式之屬性的原則運算式評估。</span><span class="sxs-lookup"><span data-stu-id="54082-162">If you look at the [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes the two previous sample policies with properties, you can see the two `set-header` policies with the property values inserted as well as the policy expression evaluation for the property that contained the policy expression.</span></span>

![API 檢查器追蹤][api-management-api-inspector-trace]

<span data-ttu-id="54082-164">請注意，雖然屬性值可以包含原則運算式，但屬性值不能包含其他屬性。</span><span class="sxs-lookup"><span data-stu-id="54082-164">Note that while property values can contain policy expressions, property values can't contain other properties.</span></span> <span data-ttu-id="54082-165">如果文字包含做為屬性值的屬性參照 (例如 `Property value text {{MyProperty}}`)，該屬性參照不會被取代，且將會包含做為屬性值的一部分。</span><span class="sxs-lookup"><span data-stu-id="54082-165">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of the property value.</span></span>

## <a name="to-create-a-property"></a><span data-ttu-id="54082-166">建立屬性</span><span class="sxs-lookup"><span data-stu-id="54082-166">To create a property</span></span>
<span data-ttu-id="54082-167">若要建立屬性，請按一下 [屬性] 索引標籤上的 [新增屬性]。</span><span class="sxs-lookup"><span data-stu-id="54082-167">To create a property, click **Add property** on the **Properties** tab.</span></span>

![新增屬性][api-management-properties-add-property-menu]

<span data-ttu-id="54082-169">[名稱] 和 [值] 都是必要值。</span><span class="sxs-lookup"><span data-stu-id="54082-169">**Name** and **Value** are required values.</span></span> <span data-ttu-id="54082-170">如果此屬性值是密碼，請選取 [這是密碼]  核取方塊。</span><span class="sxs-lookup"><span data-stu-id="54082-170">If this property value is a secret, check the **This is a secret** checkbox.</span></span> <span data-ttu-id="54082-171">輸入一或多個選擇性標籤來協助組織您的屬性，然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="54082-171">Enter one or more optional tags to help with organizing your properties, and click **Save**.</span></span>

![新增屬性][api-management-properties-add-property]

<span data-ttu-id="54082-173">儲存新屬性之後，[搜尋屬性]  文字方塊會填入新屬性的名稱並且顯示新屬性。</span><span class="sxs-lookup"><span data-stu-id="54082-173">When a new property is saved, the **Search property** textbox is populated with the name of the new property and the new property is displayed.</span></span> <span data-ttu-id="54082-174">若要顯示所有屬性，請清除 [搜尋屬性]  文字方塊並按 Enter。</span><span class="sxs-lookup"><span data-stu-id="54082-174">To display all properties, clear the **Search property** textbox and press enter.</span></span>

![屬性][api-management-properties-property-saved]

<span data-ttu-id="54082-176">如需使用 REST API 建立屬性的詳細資訊，請參閱 [使用 REST API 建立屬性](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put)。</span><span class="sxs-lookup"><span data-stu-id="54082-176">For information on creating a property using the REST API, see [Create a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span></span>

## <a name="to-edit-a-property"></a><span data-ttu-id="54082-177">編輯屬性</span><span class="sxs-lookup"><span data-stu-id="54082-177">To edit a property</span></span>
<span data-ttu-id="54082-178">若要編輯屬性，請按一下屬性旁邊的 [編輯]  來編輯。</span><span class="sxs-lookup"><span data-stu-id="54082-178">To edit a property, click **Edit** beside the property to edit.</span></span>

![編輯屬性][api-management-properties-edit]

<span data-ttu-id="54082-180">進行想要的變更，然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="54082-180">Make any desired changes, and click **Save**.</span></span> <span data-ttu-id="54082-181">如果您變更屬性名稱，任何參照該屬性的原則會自動更新以使用新的名稱。</span><span class="sxs-lookup"><span data-stu-id="54082-181">If you change the property name, any policies that reference that property are automatically updated to use the new name.</span></span>

![編輯屬性][api-management-properties-edit-property]

<span data-ttu-id="54082-183">如需使用 REST API 編輯屬性的詳細資訊，請參閱 [使用 REST API 編輯屬性](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch)。</span><span class="sxs-lookup"><span data-stu-id="54082-183">For information on editing a property using the REST API, see [Edit a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span></span>

## <a name="to-delete-a-property"></a><span data-ttu-id="54082-184">刪除屬性</span><span class="sxs-lookup"><span data-stu-id="54082-184">To delete a property</span></span>
<span data-ttu-id="54082-185">若要刪除屬性，請按一下屬性旁邊的 [刪除]  來刪除。</span><span class="sxs-lookup"><span data-stu-id="54082-185">To delete a property, click **Delete** beside the property to delete.</span></span>

![刪除屬性][api-management-properties-delete]

<span data-ttu-id="54082-187">按一下 [Yes, delete it]  加以確認。</span><span class="sxs-lookup"><span data-stu-id="54082-187">Click **Yes, delete it** to confirm.</span></span>

![Confirm delete][api-management-delete-confirm]

> [!IMPORTANT]
> <span data-ttu-id="54082-189">如有任何原則參照該屬性，則您必須將該屬性從所有使用它的原則中移除，才能成功刪除該屬性。</span><span class="sxs-lookup"><span data-stu-id="54082-189">If the property is referenced by any policies, you will be unable to successfully delete it until you remove the property from all policies that use it.</span></span>
> 
> 

<span data-ttu-id="54082-190">如需使用 REST API 刪除屬性的詳細資訊，請參閱 [使用 REST API 刪除屬性](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete)。</span><span class="sxs-lookup"><span data-stu-id="54082-190">For information on deleting a property using the REST API, see [Delete a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span></span>

## <a name="to-search-and-filter-properties"></a><span data-ttu-id="54082-191">搜尋與篩選屬性</span><span class="sxs-lookup"><span data-stu-id="54082-191">To search and filter properties</span></span>
<span data-ttu-id="54082-192">[屬性]  索引標籤包括可協助您管理屬性的搜尋與篩選功能。</span><span class="sxs-lookup"><span data-stu-id="54082-192">The **Properties** tab includes searching and filtering capabilities to help you manage your properties.</span></span> <span data-ttu-id="54082-193">若要按照屬性名稱篩選屬性清單，請在 [搜尋屬性]  文字方塊中輸入搜尋字詞。</span><span class="sxs-lookup"><span data-stu-id="54082-193">To filter the property list by property name, enter a search term in the **Search property** textbox.</span></span> <span data-ttu-id="54082-194">若要顯示所有屬性，請清除 [搜尋屬性]  文字方塊並按 Enter。</span><span class="sxs-lookup"><span data-stu-id="54082-194">To display all properties, clear the **Search property** textbox and press enter.</span></span>

![搜尋][api-management-properties-search]

<span data-ttu-id="54082-196">若要按照標籤值篩選屬性清單，請在 [依標籤篩選]  文字方塊中輸入一或多個標籤。</span><span class="sxs-lookup"><span data-stu-id="54082-196">To filter the property list by tag values, enter one or more tags into the **Filter by tags** textbox.</span></span> <span data-ttu-id="54082-197">若要顯示所有屬性，請清除 [依標籤篩選]  文字方塊並按 Enter。</span><span class="sxs-lookup"><span data-stu-id="54082-197">To display all properties, clear the **Filter by tags** textbox and press enter.</span></span>

![篩選器][api-management-properties-filter]

## <a name="next-steps"></a><span data-ttu-id="54082-199">後續步驟</span><span class="sxs-lookup"><span data-stu-id="54082-199">Next steps</span></span>
* <span data-ttu-id="54082-200">深入了解原則的使用方式</span><span class="sxs-lookup"><span data-stu-id="54082-200">Learn more about working with policies</span></span>
  * [<span data-ttu-id="54082-201">API 管理中的原則</span><span class="sxs-lookup"><span data-stu-id="54082-201">Policies in API Management</span></span>](api-management-howto-policies.md)
  * [<span data-ttu-id="54082-202">原則參考文件</span><span class="sxs-lookup"><span data-stu-id="54082-202">Policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [<span data-ttu-id="54082-203">原則運算式</span><span class="sxs-lookup"><span data-stu-id="54082-203">Policy expressions</span></span>](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="54082-204">觀看影片概觀</span><span class="sxs-lookup"><span data-stu-id="54082-204">Watch a video overview</span></span>
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

