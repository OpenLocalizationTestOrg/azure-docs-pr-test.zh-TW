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
# <a name="policies-in-azure-api-management"></a><span data-ttu-id="57df3-103">Azure API 管理中的原則</span><span class="sxs-lookup"><span data-stu-id="57df3-103">Policies in Azure API Management</span></span>
<span data-ttu-id="57df3-104">在 Azure API 管理中，原則就是 hello 的允許 hello 發行者透過組態 API toochange hello 行為的 hello 系統的強大功能。</span><span class="sxs-lookup"><span data-stu-id="57df3-104">In Azure API Management, policies are a powerful capability of hello system that allow hello publisher toochange hello behavior of hello API through configuration.</span></span> <span data-ttu-id="57df3-105">原則是循序 hello 要求上執行的陳述式的集合或應用程式開發介面的回應。</span><span class="sxs-lookup"><span data-stu-id="57df3-105">Policies are a collection of Statements that are executed sequentially on hello request or response of an API.</span></span> <span data-ttu-id="57df3-106">受歡迎的陳述式包含從 XML tooJSON 格式轉換，並呼叫速率限制為開發人員的來電 toorestrict hello 數量。</span><span class="sxs-lookup"><span data-stu-id="57df3-106">Popular Statements include format conversion from XML tooJSON and call rate limiting toorestrict hello amount of incoming calls from a developer.</span></span> <span data-ttu-id="57df3-107">更多原則是可用的 hello 方塊。</span><span class="sxs-lookup"><span data-stu-id="57df3-107">Many more policies are available out of hello box.</span></span>

<span data-ttu-id="57df3-108">請參閱 hello[原則參考][ Policy Reference]原則陳述式和其設定的完整清單。</span><span class="sxs-lookup"><span data-stu-id="57df3-108">See hello [Policy Reference][Policy Reference] for a full list of policy statements and their settings.</span></span>

<span data-ttu-id="57df3-109">Hello API 取用者之間受管理的 hello API 位於 hello 閘道內會套用原則。</span><span class="sxs-lookup"><span data-stu-id="57df3-109">Policies are applied inside hello gateway which sits between hello API consumer and hello managed API.</span></span> <span data-ttu-id="57df3-110">hello 閘道接收的所有要求和通常不變，與轉送 toohello 基礎應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="57df3-110">hello gateway receives all requests and usually forwards them unaltered toohello underlying API.</span></span> <span data-ttu-id="57df3-111">但是原則可以套用變更 tooboth hello 輸入的要求和傳出的回應。</span><span class="sxs-lookup"><span data-stu-id="57df3-111">However a policy can apply changes tooboth hello inbound request and outbound response.</span></span>

<span data-ttu-id="57df3-112">除非另外指定 hello 原則，可以使用原則運算式做為屬性值或任何 hello API 管理原則中的文字值。</span><span class="sxs-lookup"><span data-stu-id="57df3-112">Policy expressions can be used as attribute values or text values in any of hello API Management policies, unless hello policy specifies otherwise.</span></span> <span data-ttu-id="57df3-113">某些原則，例如 hello[控制流程][ Control flow]和[設定變數][ Set variable]原則為基礎的原則運算式。</span><span class="sxs-lookup"><span data-stu-id="57df3-113">Some policies such as hello [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="57df3-114">如需詳細資訊，請參閱[進階原則][Advanced policies]和[原則運算式][Policy expressions]。</span><span class="sxs-lookup"><span data-stu-id="57df3-114">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions].</span></span>

## <span data-ttu-id="57df3-115"><a name="scopes"></a>如何 tooconfigure 原則</span><span class="sxs-lookup"><span data-stu-id="57df3-115"><a name="scopes"> </a>How tooconfigure policies</span></span>
<span data-ttu-id="57df3-116">全域或 hello 範圍可以設定原則[產品][Product]， [API] [ API]或[作業][Operation].</span><span class="sxs-lookup"><span data-stu-id="57df3-116">Policies can be configured globally or at hello scope of a [Product][Product], [API][API] or [Operation][Operation].</span></span> <span data-ttu-id="57df3-117">tooconfigure 原則中，瀏覽 toohello hello 發行者入口網站中的原則編輯器。</span><span class="sxs-lookup"><span data-stu-id="57df3-117">tooconfigure a policy, navigate toohello Policies editor in hello publisher portal.</span></span>

![Policies menu][policies-menu]

<span data-ttu-id="57df3-119">hello 原則編輯器 」 包含三個主要區段： hello 原則範圍 （頂端），hello 原則定義 （左） 編輯原則而 hello 陳述式清單 （右）：</span><span class="sxs-lookup"><span data-stu-id="57df3-119">hello policies editor consists of three main sections: hello policy scope (top), hello policy definition where policies are edited (left) and hello statements list (right):</span></span>

![Policies editor][policies-editor]

<span data-ttu-id="57df3-121">設定的原則，您必須先選取應該套用原則的 hello 在 hello 範圍 toobegin。</span><span class="sxs-lookup"><span data-stu-id="57df3-121">toobegin configuring a policy you must first select hello scope at which hello policy should apply.</span></span> <span data-ttu-id="57df3-122">在 hello 螢幕擷取畫面下方 hello**入門**選取產品時。</span><span class="sxs-lookup"><span data-stu-id="57df3-122">In hello screenshot below hello **Starter** product is selected.</span></span> <span data-ttu-id="57df3-123">注意該 hello 正方形符號 下一步 toohello 原則名稱表示已經在此層級套用原則。</span><span class="sxs-lookup"><span data-stu-id="57df3-123">Note that hello square symbol next toohello policy name indicates that a policy is already applied at this level.</span></span>

![Scope][policies-scope]

<span data-ttu-id="57df3-125">已套用原則，因為 hello 組態所示 hello 定義檢視中。</span><span class="sxs-lookup"><span data-stu-id="57df3-125">Since a policy has already been applied, hello configuration is shown in hello definition view.</span></span>

![設定][policies-configure]

<span data-ttu-id="57df3-127">hello 原則會顯示唯讀狀態一開始。</span><span class="sxs-lookup"><span data-stu-id="57df3-127">hello policy is displayed read-only at first.</span></span> <span data-ttu-id="57df3-128">在訂單 tooedit hello 定義按一下 hello**設定原則**動作。</span><span class="sxs-lookup"><span data-stu-id="57df3-128">In order tooedit hello definition click hello **Configure Policy** action.</span></span>

![Edit][policies-edit]

<span data-ttu-id="57df3-130">hello 原則定義是簡單的 XML 文件描述輸入和輸出的陳述式的序列。</span><span class="sxs-lookup"><span data-stu-id="57df3-130">hello policy definition is a simple XML document that describes a sequence of inbound and outbound statements.</span></span> <span data-ttu-id="57df3-131">hello XML 可以直接在 hello 定義 視窗中編輯。</span><span class="sxs-lookup"><span data-stu-id="57df3-131">hello XML can be edited directly in hello definition window.</span></span> <span data-ttu-id="57df3-132">陳述式的清單是提供權限 toohello 和陳述式適用的 toohello 目前範圍都已啟用，並反白顯示。hello 所示**限制呼叫率**hello 上方螢幕擷取畫面中的陳述式。</span><span class="sxs-lookup"><span data-stu-id="57df3-132">A list of statements is provided toohello right and statements applicable toohello current scope are enabled and highlighted; as demonstrated by hello **Limit Call Rate** statement in hello screenshot above.</span></span>

<span data-ttu-id="57df3-133">按一下 已啟用的陳述式會將 hello hello hello 定義檢視中的 hello 游標位置上適當的 XML。</span><span class="sxs-lookup"><span data-stu-id="57df3-133">Clicking an enabled statement will add hello appropriate XML at hello location of hello cursor in hello definition view.</span></span> 

> [!NOTE]
> <span data-ttu-id="57df3-134">如果您想 tooadd hello 原則未啟用，請確定您是在該原則的 hello 正確範圍。</span><span class="sxs-lookup"><span data-stu-id="57df3-134">If hello policy that you want tooadd is not enabled, ensure that you are in hello correct scope for that policy.</span></span> <span data-ttu-id="57df3-135">每個原則陳述式都是針對在特定範圍和原則區段中使用所設計。</span><span class="sxs-lookup"><span data-stu-id="57df3-135">Each policy statement is designed for use in certain scopes and policy sections.</span></span> <span data-ttu-id="57df3-136">tooreview hello 原則區段和領域的原則，請檢查 hello**使用量**區段，該原則在 hello[原則參考][Policy Reference]。</span><span class="sxs-lookup"><span data-stu-id="57df3-136">tooreview hello policy sections and scopes for a policy, check hello **Usage** section for that policy in hello [Policy Reference][Policy Reference].</span></span>
> 
> 

<span data-ttu-id="57df3-137">原則陳述式的完整清單以及其設定位於 hello[原則參考][Policy Reference]。</span><span class="sxs-lookup"><span data-stu-id="57df3-137">A full list of policy statements and their settings are available in hello [Policy Reference][Policy Reference].</span></span>

<span data-ttu-id="57df3-138">比方說，tooadd 新的陳述式 toorestrict 連入要求 toospecified IP 位址時，將 hello hello 內容之內 hello 游標`inbound`XML 項目，然後按一下 hello**限制呼叫端 Ip**陳述式。</span><span class="sxs-lookup"><span data-stu-id="57df3-138">For example, tooadd a new statement toorestrict incoming requests toospecified IP addresses, place hello cursor just inside hello content of hello `inbound` XML element and click hello **Restrict caller IPs** statement.</span></span>

![Restriction policies][policies-restrict]

<span data-ttu-id="57df3-140">這樣會加入 XML 程式碼片段 toohello `inbound` tooconfigure hello 陳述式的方式提供指引的項目。</span><span class="sxs-lookup"><span data-stu-id="57df3-140">This will add an XML snippet toohello `inbound` element that provides guidance on how tooconfigure hello statement.</span></span>

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

<span data-ttu-id="57df3-141">toolimit 傳入要求，並接受只有來自 IP 位址的 1.2.3.4 修改 hello XML，如下所示：</span><span class="sxs-lookup"><span data-stu-id="57df3-141">toolimit inbound requests and accept only those from an IP address of 1.2.3.4 modify hello XML as follows:</span></span>

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![儲存][policies-save]

<span data-ttu-id="57df3-143">完成後設定 hello 陳述式中的 hello 原則，請按一下**儲存**與 hello 變更將傳播的 toohello API 管理閘道器立即。</span><span class="sxs-lookup"><span data-stu-id="57df3-143">When complete configuring hello statements for hello policy, click **Save** and hello changes will be propagated toohello API Management gateway immediately.</span></span>

## <span data-ttu-id="57df3-144"><a name="sections"> </a>了解原則組態</span><span class="sxs-lookup"><span data-stu-id="57df3-144"><a name="sections"> </a>Understanding policy configuration</span></span>
<span data-ttu-id="57df3-145">原則是針對要求和回應而依序執行的一連串陳述式。</span><span class="sxs-lookup"><span data-stu-id="57df3-145">A policy is a series of statements that execute in order for a request and a response.</span></span> <span data-ttu-id="57df3-146">hello 組態會分成適當`inbound`， `backend`， `outbound`，和`on-error`區段 hello 下列組態所示。</span><span class="sxs-lookup"><span data-stu-id="57df3-146">hello configuration is divided appropriately into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in hello following configuration.</span></span>

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

<span data-ttu-id="57df3-147">如果 hello 處理要求期間發生錯誤時，任何剩餘步驟 hello `inbound`， `backend`，或`outbound`會略過區段，並執行跳 toohello 陳述式中 hello `on-error` > 一節。</span><span class="sxs-lookup"><span data-stu-id="57df3-147">If there is an error during hello processing of a request, any remaining steps in hello `inbound`, `backend`, or `outbound` sections are skipped and execution jumps toohello statements in hello `on-error` section.</span></span> <span data-ttu-id="57df3-148">將原則陳述式放在 hello `on-error` > 一節，您可以使用 hello 檢閱 hello 錯誤`context.LastError`屬性，檢查及自訂 hello 錯誤回應使用 hello`set-body`原則，並設定發生錯誤時，會發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="57df3-148">By placing policy statements in hello `on-error` section you can review hello error by using hello `context.LastError` property, inspect and customize hello error response using hello `set-body` policy, and configure what happens if an error occurs.</span></span> <span data-ttu-id="57df3-149">有內建的步驟和 hello 原則陳述式處理期間可能發生之錯誤的錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="57df3-149">There are error codes for built-in steps and for errors that may occur during hello processing of policy statements.</span></span> <span data-ttu-id="57df3-150">如需詳細資訊，請參閱 [API 管理原則中的錯誤處理方式](https://msdn.microsoft.com/library/azure/mt629506.aspx)。</span><span class="sxs-lookup"><span data-stu-id="57df3-150">For more information, see [Error handling in API Management policies](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span></span>

<span data-ttu-id="57df3-151">因為原則可以指定在不同的層級 （全域、 產品、 api 和操作） hello 組態的方式為您提供 toospecify hello 順序方面 toohello 父原則執行所在 hello 原則定義的陳述式。</span><span class="sxs-lookup"><span data-stu-id="57df3-151">Since policies can be specified at different levels (global, product, api and operation) hello configuration provides a way for you toospecify hello order in which hello policy definition's statements execute with respect toohello parent policy.</span></span> 

<span data-ttu-id="57df3-152">原則範圍的評估順序的 hello。</span><span class="sxs-lookup"><span data-stu-id="57df3-152">Policy scopes are evaluated in hello following order.</span></span>

1. <span data-ttu-id="57df3-153">全域範圍</span><span class="sxs-lookup"><span data-stu-id="57df3-153">Global scope</span></span>
2. <span data-ttu-id="57df3-154">產品範圍</span><span class="sxs-lookup"><span data-stu-id="57df3-154">Product scope</span></span>
3. <span data-ttu-id="57df3-155">API 範圍</span><span class="sxs-lookup"><span data-stu-id="57df3-155">API scope</span></span>
4. <span data-ttu-id="57df3-156">作業範圍</span><span class="sxs-lookup"><span data-stu-id="57df3-156">Operation scope</span></span>

<span data-ttu-id="57df3-157">hello 評估陳述式中的，根據 hello toohello 放置`base`項目，如果有的話。</span><span class="sxs-lookup"><span data-stu-id="57df3-157">hello statements within them are evaluated according toohello placement of hello `base` element, if it is present.</span></span> <span data-ttu-id="57df3-158">全域原則有沒有父原則並使用 hello`<base>`中它的項目沒有任何作用。</span><span class="sxs-lookup"><span data-stu-id="57df3-158">Global policy has no parent policy and using hello `<base>` element in it has no effect.</span></span>

<span data-ttu-id="57df3-159">比方說，如果在 hello 全域層級和應用程式開發介面所設定的原則的原則，然後使用該特定 API 時這兩項原則會套用。</span><span class="sxs-lookup"><span data-stu-id="57df3-159">For example, if you have a policy at hello global level and a policy configured for an API, then whenever that particular API is used both policies will be applied.</span></span> <span data-ttu-id="57df3-160">API 管理可讓您透過 hello 基底項目組合的原則陳述式的具決定性排序。</span><span class="sxs-lookup"><span data-stu-id="57df3-160">API Management allows for deterministic ordering of combined policy statements via hello base element.</span></span> 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

<span data-ttu-id="57df3-161">在 hello 範例原則定義上述 hello`cross-domain`陳述式會執行任何更高的原則可開啟，後面跟著 hello 之前`find-and-replace`原則。</span><span class="sxs-lookup"><span data-stu-id="57df3-161">In hello example policy definition above, hello `cross-domain` statement would execute before any higher policies which would in turn, be followed by hello `find-and-replace` policy.</span></span> 

<span data-ttu-id="57df3-162">按一下 [toosee hello 原則編輯器] 中的 hello 目前範圍中的 hello 原則**重新計算選取範圍的有效原則**。</span><span class="sxs-lookup"><span data-stu-id="57df3-162">toosee hello policies in hello current scope in hello policy editor, click **Recalculate effective policy for selected scope**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="57df3-163">後續步驟</span><span class="sxs-lookup"><span data-stu-id="57df3-163">Next steps</span></span>
<span data-ttu-id="57df3-164">請查看有關原則運算式的下列影片。</span><span class="sxs-lookup"><span data-stu-id="57df3-164">Check out following video on policy expressions.</span></span>

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
