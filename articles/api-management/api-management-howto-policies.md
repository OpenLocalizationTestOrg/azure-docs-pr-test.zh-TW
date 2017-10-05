---
title: "Azure API 管理中的原則 | Microsoft Docs"
description: "了解如何在 API 管理中建立、編輯和設定原則。"
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
ms.openlocfilehash: 7c1f235343074ec11c635097f2b094a10f3fe781
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="policies-in-azure-api-management"></a><span data-ttu-id="8da8f-103">Azure API 管理中的原則</span><span class="sxs-lookup"><span data-stu-id="8da8f-103">Policies in Azure API Management</span></span>
<span data-ttu-id="8da8f-104">在 Azure API 管理中，原則是系統的一項強大功能，可讓發行者透過組態來變更 API 的行為。</span><span class="sxs-lookup"><span data-stu-id="8da8f-104">In Azure API Management, policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="8da8f-105">原則是「陳述式」的集合，會在 API 的要求或回應上循序執行。</span><span class="sxs-lookup"><span data-stu-id="8da8f-105">Policies are a collection of Statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="8da8f-106">常見的「陳述式」包括從 XML 至 JSON 的格式轉換，以及利用呼叫速率限制來限制開發人員傳入的呼叫數量。</span><span class="sxs-lookup"><span data-stu-id="8da8f-106">Popular Statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer.</span></span> <span data-ttu-id="8da8f-107">還有許多現成的原則可用。</span><span class="sxs-lookup"><span data-stu-id="8da8f-107">Many more policies are available out of the box.</span></span>

<span data-ttu-id="8da8f-108">如需原則陳述式及其設定的完整清單，請參閱 [原則參考文件][Policy Reference]。</span><span class="sxs-lookup"><span data-stu-id="8da8f-108">See the [Policy Reference][Policy Reference] for a full list of policy statements and their settings.</span></span>

<span data-ttu-id="8da8f-109">原則是在位於 API 取用者與受管理 API 之間的閘道內套用。</span><span class="sxs-lookup"><span data-stu-id="8da8f-109">Policies are applied inside the gateway which sits between the API consumer and the managed API.</span></span> <span data-ttu-id="8da8f-110">閘道會接收所有要求，然後通常原封不動地轉送至基礎 API。</span><span class="sxs-lookup"><span data-stu-id="8da8f-110">The gateway receives all requests and usually forwards them unaltered to the underlying API.</span></span> <span data-ttu-id="8da8f-111">不過，原則可以套用至輸入要求和輸出要求。</span><span class="sxs-lookup"><span data-stu-id="8da8f-111">However a policy can apply changes to both the inbound request and outbound response.</span></span>

<span data-ttu-id="8da8f-112">如果原則不另行指定，則可以在任何 API 管理原則中，使用原則運算式做為屬性值或文字值。</span><span class="sxs-lookup"><span data-stu-id="8da8f-112">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="8da8f-113">某些原則是以原則運算式為基礎，例如[控制流程][Control flow]和[設定變數][Set variable]原則。</span><span class="sxs-lookup"><span data-stu-id="8da8f-113">Some policies such as the [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="8da8f-114">如需詳細資訊，請參閱[進階原則][Advanced policies]和[原則運算式][Policy expressions]。</span><span class="sxs-lookup"><span data-stu-id="8da8f-114">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions].</span></span>

## <span data-ttu-id="8da8f-115"><a name="scopes"> </a>如何設定原則</span><span class="sxs-lookup"><span data-stu-id="8da8f-115"><a name="scopes"> </a>How to configure policies</span></span>
<span data-ttu-id="8da8f-116">原則可以整體設定，或在[產品][Product]、[API][API] 或[作業][Operation]的範圍上設定。</span><span class="sxs-lookup"><span data-stu-id="8da8f-116">Policies can be configured globally or at the scope of a [Product][Product], [API][API] or [Operation][Operation].</span></span> <span data-ttu-id="8da8f-117">若要設定原則，請瀏覽至發佈者入口網站的原則編輯器。</span><span class="sxs-lookup"><span data-stu-id="8da8f-117">To configure a policy, navigate to the Policies editor in the publisher portal.</span></span>

![Policies menu][policies-menu]

<span data-ttu-id="8da8f-119">原則編輯器包含三個主要區段：原則範圍 (上)、編輯原則的原則定義 (左) 和陳述式清單 (右)：</span><span class="sxs-lookup"><span data-stu-id="8da8f-119">The policies editor consists of three main sections: the policy scope (top), the policy definition where policies are edited (left) and the statements list (right):</span></span>

![Policies editor][policies-editor]

<span data-ttu-id="8da8f-121">若要開始設定原則，您必須先選取要套用原則的範圍。</span><span class="sxs-lookup"><span data-stu-id="8da8f-121">To begin configuring a policy you must first select the scope at which the policy should apply.</span></span> <span data-ttu-id="8da8f-122">在以下的螢幕擷取畫面中，已選取 **簡易版** 產品。</span><span class="sxs-lookup"><span data-stu-id="8da8f-122">In the screenshot below the **Starter** product is selected.</span></span> <span data-ttu-id="8da8f-123">請注意，原則名稱旁邊的正方形符號表示此層級上已套用原則。</span><span class="sxs-lookup"><span data-stu-id="8da8f-123">Note that the square symbol next to the policy name indicates that a policy is already applied at this level.</span></span>

![Scope][policies-scope]

<span data-ttu-id="8da8f-125">因為已套用原則，定義檢視中會顯示組態。</span><span class="sxs-lookup"><span data-stu-id="8da8f-125">Since a policy has already been applied, the configuration is shown in the definition view.</span></span>

![設定][policies-configure]

<span data-ttu-id="8da8f-127">原則最初會以唯讀顯示。</span><span class="sxs-lookup"><span data-stu-id="8da8f-127">The policy is displayed read-only at first.</span></span> <span data-ttu-id="8da8f-128">為了編輯定義，請按一下 [設定原則]  動作。</span><span class="sxs-lookup"><span data-stu-id="8da8f-128">In order to edit the definition click the **Configure Policy** action.</span></span>

![Edit][policies-edit]

<span data-ttu-id="8da8f-130">原則定義是一份簡單的 XML 文件，描述一連串輸入和輸出陳述式。</span><span class="sxs-lookup"><span data-stu-id="8da8f-130">The policy definition is a simple XML document that describes a sequence of inbound and outbound statements.</span></span> <span data-ttu-id="8da8f-131">可直接在定義視窗中編輯 XML。</span><span class="sxs-lookup"><span data-stu-id="8da8f-131">The XML can be edited directly in the definition window.</span></span> <span data-ttu-id="8da8f-132">右邊提供陳述式的清單，而且會啟用並醒目提示適用於目前範圍的陳述式，如以上螢幕擷取畫面中的 **Limit Call Rate** 陳述式所示。</span><span class="sxs-lookup"><span data-stu-id="8da8f-132">A list of statements is provided to the right and statements applicable to the current scope are enabled and highlighted; as demonstrated by the **Limit Call Rate** statement in the screenshot above.</span></span>

<span data-ttu-id="8da8f-133">按一下已啟用的陳述式會在定義檢視中的游標位置上加入適當的 XML。</span><span class="sxs-lookup"><span data-stu-id="8da8f-133">Clicking an enabled statement will add the appropriate XML at the location of the cursor in the definition view.</span></span> 

> [!NOTE]
> <span data-ttu-id="8da8f-134">如果未啟用您想要新增的原則，請確定您是在該原則的正確範圍內。</span><span class="sxs-lookup"><span data-stu-id="8da8f-134">If the policy that you want to add is not enabled, ensure that you are in the correct scope for that policy.</span></span> <span data-ttu-id="8da8f-135">每個原則陳述式都是針對在特定範圍和原則區段中使用所設計。</span><span class="sxs-lookup"><span data-stu-id="8da8f-135">Each policy statement is designed for use in certain scopes and policy sections.</span></span> <span data-ttu-id="8da8f-136">若要檢閱原則的原則區段和範圍，請檢查[原則參考][Policy Reference]中該原則的**使用方式**一節。</span><span class="sxs-lookup"><span data-stu-id="8da8f-136">To review the policy sections and scopes for a policy, check the **Usage** section for that policy in the [Policy Reference][Policy Reference].</span></span>
> 
> 

<span data-ttu-id="8da8f-137">[原則參考文件][Policy Reference]中提供原則陳述式及其設定的完整清單。</span><span class="sxs-lookup"><span data-stu-id="8da8f-137">A full list of policy statements and their settings are available in the [Policy Reference][Policy Reference].</span></span>

<span data-ttu-id="8da8f-138">例如，若要加入新的陳述式以限制接收指定 IP 位址的傳入要求，請將游標移至 `inbound` XML 元素的內容當中，然後按一下 **Restrict caller IPs** 陳述式。</span><span class="sxs-lookup"><span data-stu-id="8da8f-138">For example, to add a new statement to restrict incoming requests to specified IP addresses, place the cursor just inside the content of the `inbound` XML element and click the **Restrict caller IPs** statement.</span></span>

![Restriction policies][policies-restrict]

<span data-ttu-id="8da8f-140">這會將 XML 程式碼片段新增至提供設定陳述式之指引的 `inbound` 元素。</span><span class="sxs-lookup"><span data-stu-id="8da8f-140">This will add an XML snippet to the `inbound` element that provides guidance on how to configure the statement.</span></span>

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

<span data-ttu-id="8da8f-141">若要限制輸入要求，只接受來自 IP 位址 1.2.3.4 的要求，請如下修改 XML：</span><span class="sxs-lookup"><span data-stu-id="8da8f-141">To limit inbound requests and accept only those from an IP address of 1.2.3.4 modify the XML as follows:</span></span>

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![儲存][policies-save]

<span data-ttu-id="8da8f-143">設定完原則陳述式後，按一下 [ **儲存** ]，所作的變更便會立即傳播至 API 管理閘道器。</span><span class="sxs-lookup"><span data-stu-id="8da8f-143">When complete configuring the statements for the policy, click **Save** and the changes will be propagated to the API Management gateway immediately.</span></span>

## <span data-ttu-id="8da8f-144"><a name="sections"> </a>了解原則組態</span><span class="sxs-lookup"><span data-stu-id="8da8f-144"><a name="sections"> </a>Understanding policy configuration</span></span>
<span data-ttu-id="8da8f-145">原則是針對要求和回應而依序執行的一連串陳述式。</span><span class="sxs-lookup"><span data-stu-id="8da8f-145">A policy is a series of statements that execute in order for a request and a response.</span></span> <span data-ttu-id="8da8f-146">系統會將組態適當地劃分為 `inbound`、`backend`、`outbound` 和 `on-error` 區段，如下列組態所示。</span><span class="sxs-lookup"><span data-stu-id="8da8f-146">The configuration is divided appropriately into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in the following configuration.</span></span>

```xml
<policies>
  <inbound>
    <!-- statements to be applied to the request go here -->
  </inbound>
  <backend>
    <!-- statements to be applied before the request is forwarded to 
         the backend service go here -->
  </backend>
  <outbound>
    <!-- statements to be applied to the response go here -->
  </outbound>
  <on-error>
    <!-- statements to be applied if there is an error condition go here -->
  </on-error>
</policies> 
```

<span data-ttu-id="8da8f-147">若在處理要求期間發生錯誤，便會略過 `inbound`、`backend` 或 `outbound` 區段中的所有剩餘步驟，且執行程序會跳至 `on-error` 區段中的陳述式。</span><span class="sxs-lookup"><span data-stu-id="8da8f-147">If there is an error during the processing of a request, any remaining steps in the `inbound`, `backend`, or `outbound` sections are skipped and execution jumps to the statements in the `on-error` section.</span></span> <span data-ttu-id="8da8f-148">將原則陳述式置於 `on-error` 區段中，您即可使用 `context.LastError` 屬性檢閱錯誤、使用 `set-body` 原則檢查和自訂錯誤回應，以及設定錯誤發生時採取的動作。</span><span class="sxs-lookup"><span data-stu-id="8da8f-148">By placing policy statements in the `on-error` section you can review the error by using the `context.LastError` property, inspect and customize the error response using the `set-body` policy, and configure what happens if an error occurs.</span></span> <span data-ttu-id="8da8f-149">會出現內建步驟的錯誤碼和處理原則陳述式期間可能會發生之錯誤的錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="8da8f-149">There are error codes for built-in steps and for errors that may occur during the processing of policy statements.</span></span> <span data-ttu-id="8da8f-150">如需詳細資訊，請參閱 [API 管理原則中的錯誤處理方式](https://msdn.microsoft.com/library/azure/mt629506.aspx)。</span><span class="sxs-lookup"><span data-stu-id="8da8f-150">For more information, see [Error handling in API Management policies](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span></span>

<span data-ttu-id="8da8f-151">由於可在不同層級指定原則可於 (全域、產品、API 和作業)，因此組態可讓您針對父原則，指定原則定義的陳述式執行順序。</span><span class="sxs-lookup"><span data-stu-id="8da8f-151">Since policies can be specified at different levels (global, product, api and operation) the configuration provides a way for you to specify the order in which the policy definition's statements execute with respect to the parent policy.</span></span> 

<span data-ttu-id="8da8f-152">系統會以下列順序評估原則範圍。</span><span class="sxs-lookup"><span data-stu-id="8da8f-152">Policy scopes are evaluated in the following order.</span></span>

1. <span data-ttu-id="8da8f-153">全域範圍</span><span class="sxs-lookup"><span data-stu-id="8da8f-153">Global scope</span></span>
2. <span data-ttu-id="8da8f-154">產品範圍</span><span class="sxs-lookup"><span data-stu-id="8da8f-154">Product scope</span></span>
3. <span data-ttu-id="8da8f-155">API 範圍</span><span class="sxs-lookup"><span data-stu-id="8da8f-155">API scope</span></span>
4. <span data-ttu-id="8da8f-156">作業範圍</span><span class="sxs-lookup"><span data-stu-id="8da8f-156">Operation scope</span></span>

<span data-ttu-id="8da8f-157">系統會根據 `base` 元素的位置 (若有的話)，評估其中的陳述式。</span><span class="sxs-lookup"><span data-stu-id="8da8f-157">The statements within them are evaluated according to the placement of the `base` element, if it is present.</span></span> <span data-ttu-id="8da8f-158">全域原則沒有父系原則，在全域原則中使用 `<base>` 元素沒有任何作用。</span><span class="sxs-lookup"><span data-stu-id="8da8f-158">Global policy has no parent policy and using the `<base>` element in it has no effect.</span></span>

<span data-ttu-id="8da8f-159">例如，若您在全域層級中有一個原則，還有一個為 API 設定的原則，則每次使用該特定 API 時，皆會套用這兩個原則。</span><span class="sxs-lookup"><span data-stu-id="8da8f-159">For example, if you have a policy at the global level and a policy configured for an API, then whenever that particular API is used both policies will be applied.</span></span> <span data-ttu-id="8da8f-160">API 管理可透過 base 元素來指定組合式原則陳述式的固定順序。</span><span class="sxs-lookup"><span data-stu-id="8da8f-160">API Management allows for deterministic ordering of combined policy statements via the base element.</span></span> 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

<span data-ttu-id="8da8f-161">在上述的原則定義範例中，`cross-domain` 陳述式會在任何更高層級的原則執行之前執行，而這些原則後面又接著 `find-and-replace` 原則。</span><span class="sxs-lookup"><span data-stu-id="8da8f-161">In the example policy definition above, the `cross-domain` statement would execute before any higher policies which would in turn, be followed by the `find-and-replace` policy.</span></span> 

<span data-ttu-id="8da8f-162">若要在原則編輯器中查看位於目前範圍的原則，請按一下 [ **重新計算所選取範圍的有效原則**]。</span><span class="sxs-lookup"><span data-stu-id="8da8f-162">To see the policies in the current scope in the policy editor, click **Recalculate effective policy for selected scope**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8da8f-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8da8f-163">Next steps</span></span>
<span data-ttu-id="8da8f-164">請查看有關原則運算式的下列影片。</span><span class="sxs-lookup"><span data-stu-id="8da8f-164">Check out following video on policy expressions.</span></span>

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
