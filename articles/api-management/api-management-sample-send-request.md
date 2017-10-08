---
title: "aaaUsing API 管理服務 toogenerate HTTP 要求"
description: "了解 API 管理 toocall 外部服務從您的 API 中的 toouse 要求和回應原則"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 4539c0fa-21ef-4b1c-a1d4-d89a38c242fa
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 8002ee453057513340328d99f298703c3b3a9531
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-external-services-from-hello-azure-api-management-service"></a><span data-ttu-id="798f3-103">使用來自 hello Azure API 管理服務的外部服務</span><span class="sxs-lookup"><span data-stu-id="798f3-103">Using external services from hello Azure API Management service</span></span>
<span data-ttu-id="798f3-104">hello 原則可在 Azure API 管理服務可以執行各種不同的有用的工作只根據 hello 連入要求、 hello 外寄回應和基本設定資訊。</span><span class="sxs-lookup"><span data-stu-id="798f3-104">hello policies available in Azure API Management service can do a wide range of useful work based purely on hello incoming request, hello outgoing response and basic configuration information.</span></span> <span data-ttu-id="798f3-105">不過，所能 toointeract 與外部服務從 API 管理原則會開啟更多的機會。</span><span class="sxs-lookup"><span data-stu-id="798f3-105">However, being able toointeract with external services from API Management policies opens up many more opportunities.</span></span>

<span data-ttu-id="798f3-106">我們先前看過我們可以互動 hello[來記錄、 監視和分析 Azure 事件中心服務](api-management-log-to-eventhub-sample.md)。</span><span class="sxs-lookup"><span data-stu-id="798f3-106">We have previously seen how we can interact with hello [Azure Event Hub service for logging, monitoring and analytics](api-management-log-to-eventhub-sample.md).</span></span> <span data-ttu-id="798f3-107">本文章中我們將示範原則，可讓您使用任何外部 HTTP toointeract 基礎服務。</span><span class="sxs-lookup"><span data-stu-id="798f3-107">In this article we will demonstrate policies that allow you toointeract with any external HTTP based service.</span></span> <span data-ttu-id="798f3-108">這些原則可以使用，用於觸發遠端事件或擷取將會使用的 toomanipulate hello 原始要求和回應以某種方式的資訊。</span><span class="sxs-lookup"><span data-stu-id="798f3-108">These policies can be used for triggering remote events or for retrieving information that will be used toomanipulate hello original request and response in some way.</span></span>

## <a name="send-one-way-request"></a><span data-ttu-id="798f3-109">傳送單向要求</span><span class="sxs-lookup"><span data-stu-id="798f3-109">Send-One-Way-Request</span></span>
<span data-ttu-id="798f3-110">可能是由於 hello 最簡單的外部互動不 hello 和不理樣式可讓通知種類重要事件之外部服務 toobe 的要求。</span><span class="sxs-lookup"><span data-stu-id="798f3-110">Possibly hello simplest external interaction is hello fire-and-forget style of request that allows an external service toobe notified of some kind of important event.</span></span> <span data-ttu-id="798f3-111">我們可以使用 hello 控制流程原則`choose`toodetect 滿足任何一種狀況，我們有興趣，所以，如果 hello 條件為止，我們可以讓外部 HTTP 要求使用 hello[傳送一個方式-要求](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest)原則。</span><span class="sxs-lookup"><span data-stu-id="798f3-111">We can use hello control flow policy `choose` toodetect any kind of condition that we are interested in and then, if hello condition is satisfied, we can make an external HTTP request using hello [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) policy.</span></span> <span data-ttu-id="798f3-112">這可能是要求 tooa 傳訊系統，例如 Hipchat Slack 或如 SendGrid 或 MailChimp，郵件應用程式開發介面或類似的重大支援事件 PagerDuty。</span><span class="sxs-lookup"><span data-stu-id="798f3-112">This could be a request tooa messaging system like Hipchat or Slack, or a mail API like SendGrid or MailChimp, or for critical support incidents something like PagerDuty.</span></span> <span data-ttu-id="798f3-113">所有的這些傳訊系統都具有簡單的 HTTP API，可讓我們輕鬆叫用。</span><span class="sxs-lookup"><span data-stu-id="798f3-113">All of these messaging systems have simple HTTP APIs that we can easily invoke.</span></span>

### <a name="alerting-with-slack"></a><span data-ttu-id="798f3-114">使用 Slack 提供警示</span><span class="sxs-lookup"><span data-stu-id="798f3-114">Alerting with Slack</span></span>
<span data-ttu-id="798f3-115">hello 下列範例會示範如何 toosend 訊息 tooa 延聊天室 hello HTTP 回應狀態碼是否大於或等於 too500。</span><span class="sxs-lookup"><span data-stu-id="798f3-115">hello following example demonstrates how toosend a message tooa Slack chat room if hello HTTP response status code is greater than or equal too500.</span></span> <span data-ttu-id="798f3-116">500 範圍錯誤指出 hello API 的用戶端的問題與我們的後端應用程式開發介面不能自行解決。</span><span class="sxs-lookup"><span data-stu-id="798f3-116">A 500 range error indicates a problem with our backend API that hello client of our API cannot resolve themselves.</span></span> <span data-ttu-id="798f3-117">通常我們需要進行某種形式的介入。</span><span class="sxs-lookup"><span data-stu-id="798f3-117">It usually requires some kind of intervention on our part.</span></span>  

```xml
<choose>
    <when condition="@(context.Response.StatusCode >= 500)">
      <send-one-way-request mode="new">
        <set-url>https://hooks.slack.com/services/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</set-url>
        <set-method>POST</set-method>
        <set-body>@{
                return new JObject(
                        new JProperty("username","APIM Alert"),
                        new JProperty("icon_emoji", ":ghost:"),
                        new JProperty("text", String.Format("{0} {1}\nHost: {2}\n{3} {4}\n User: {5}",
                                                context.Request.Method,
                                                context.Request.Url.Path + context.Request.Url.QueryString,
                                                context.Request.Url.Host,
                                                context.Response.StatusCode,
                                                context.Response.StatusReason,
                                                context.User.Email
                                                ))
                        ).ToString();
            }</set-body>
      </send-one-way-request>
    </when>
</choose>
```

<span data-ttu-id="798f3-118">Slack 有傳入的 web 攔截 hello 概念。</span><span class="sxs-lookup"><span data-stu-id="798f3-118">Slack has hello notion of inbound web hooks.</span></span> <span data-ttu-id="798f3-119">設定時傳入的 web 攔截，Slack 會產生特殊的 URL，這可讓您 toodo 簡單的 POST 要求和 toopass 訊息成 hello Slack 頻道。</span><span class="sxs-lookup"><span data-stu-id="798f3-119">When configuring an inbound web hook, Slack generates a special URL which allows you toodo a simple POST request and toopass a message into hello Slack channel.</span></span> <span data-ttu-id="798f3-120">hello 我們建立的 JSON 主體根據 Slack 所定義的格式。</span><span class="sxs-lookup"><span data-stu-id="798f3-120">hello JSON body that we create is based on a format defined by Slack.</span></span>

![Slack 的 Web 攔截](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a><span data-ttu-id="798f3-122">「射後不理」 夠好嗎？</span><span class="sxs-lookup"><span data-stu-id="798f3-122">Is fire and forget good enough?</span></span>
<span data-ttu-id="798f3-123">使用要求的射後不理樣式有一些特定的權衡取捨。</span><span class="sxs-lookup"><span data-stu-id="798f3-123">There are certain tradeoffs when using a fire-and-forget style of request.</span></span> <span data-ttu-id="798f3-124">如果基於某些原因，hello 要求失敗，就不會報告 hello 失敗。</span><span class="sxs-lookup"><span data-stu-id="798f3-124">If for some reason, hello request fails, then hello failure will not be reported.</span></span> <span data-ttu-id="798f3-125">在此特定情況下，不保證 hello 複雜度次要失敗報告系統並等待 hello 回應 hello 額外的效能成本。</span><span class="sxs-lookup"><span data-stu-id="798f3-125">In this particular situation, hello complexity of having a secondary failure reporting system and hello additional performance cost of waiting for hello response is not warranted.</span></span> <span data-ttu-id="798f3-126">案例中很重要的 toocheck hello 回應，然後 hello[傳送要求](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest)原則是更好的選項。</span><span class="sxs-lookup"><span data-stu-id="798f3-126">For scenarios where it is essential toocheck hello response, then hello [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy is a better option.</span></span>

## <a name="send-request"></a><span data-ttu-id="798f3-127">send-request</span><span class="sxs-lookup"><span data-stu-id="798f3-127">Send-Request</span></span>
<span data-ttu-id="798f3-128">hello`send-request`使用外部服務 tooperform 複雜處理函式和傳回資料 toohello API 管理服務，可用於進一步處理原則的原則啟用。</span><span class="sxs-lookup"><span data-stu-id="798f3-128">hello `send-request` policy enables using an external service tooperform complex processing functions and return data toohello API management service that can be used for further policy processing.</span></span>

### <a name="authorizing-reference-tokens"></a><span data-ttu-id="798f3-129">授權參考權杖</span><span class="sxs-lookup"><span data-stu-id="798f3-129">Authorizing reference tokens</span></span>
<span data-ttu-id="798f3-130">API 管理的主要功能是保護後端資源。</span><span class="sxs-lookup"><span data-stu-id="798f3-130">A major function of API Management is protecting backend resources.</span></span> <span data-ttu-id="798f3-131">如果您的 API 所使用的 hello 授權伺服器建立[JWT 權杖](http://jwt.io/)OAuth2 流程的一部分做為[Azure Active Directory](../active-directory/active-directory-aadconnect.md)存在，則您可以使用 hello`validate-jwt`原則 tooverify hello 有效性hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="798f3-131">If hello authorization server used by your API creates [JWT tokens](http://jwt.io/) as part of its OAuth2 flow, as [Azure Active Directory](../active-directory/active-directory-aadconnect.md) does, then you can use hello `validate-jwt` policy tooverify hello validity of hello token.</span></span> <span data-ttu-id="798f3-132">不過，某些授權伺服器建立所謂的[參考語彙基元](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/)，而不進行呼叫後 toohello 授權伺服器無法驗證。</span><span class="sxs-lookup"><span data-stu-id="798f3-132">However, some authorization servers create what are called [reference tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) that cannot be verified without making a call back toohello authorization server.</span></span>

### <a name="standardized-introspection"></a><span data-ttu-id="798f3-133">將自我檢查標準化</span><span class="sxs-lookup"><span data-stu-id="798f3-133">Standardized introspection</span></span>
<span data-ttu-id="798f3-134">在過去的 hello 已經過驗證與授權伺服器參考語彙基元的任何標準化的方式。</span><span class="sxs-lookup"><span data-stu-id="798f3-134">In hello past there has been no standardized way of verifying a reference token with an authorization server.</span></span> <span data-ttu-id="798f3-135">不過最近提議的標準[RFC 7662](https://tools.ietf.org/html/rfc7662) hello 定義資源伺服器可以如何確認語彙基元的 hello 有效性的 IETF 根據已發行。</span><span class="sxs-lookup"><span data-stu-id="798f3-135">However a recently proposed standard [RFC 7662](https://tools.ietf.org/html/rfc7662) was published by hello IETF that defines how a resource server can verify hello validity of a token.</span></span>

### <a name="extracting-hello-token"></a><span data-ttu-id="798f3-136">解壓縮 hello 語彙基元</span><span class="sxs-lookup"><span data-stu-id="798f3-136">Extracting hello token</span></span>
<span data-ttu-id="798f3-137">hello 第一個步驟是從 hello 授權標頭的 tooextract hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="798f3-137">hello first step is tooextract hello token from hello Authorization header.</span></span> <span data-ttu-id="798f3-138">hello 標頭值的格式應與 hello`Bearer`授權配置、 一個空格，然後 hello 授權權杖做為每個[RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1)。</span><span class="sxs-lookup"><span data-stu-id="798f3-138">hello header value should be formatted with hello `Bearer` authorization scheme, a single space and then hello authorization token as per [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span></span> <span data-ttu-id="798f3-139">不幸的是一些情況下則 hello 授權配置。</span><span class="sxs-lookup"><span data-stu-id="798f3-139">Unfortunately there are cases where hello authorization scheme is omitted.</span></span> <span data-ttu-id="798f3-140">這個 tooaccount 剖析時，我們會分割上一個空格，再選取 hello hello 傳回字串陣列中的最後一個字串 hello 標頭值。</span><span class="sxs-lookup"><span data-stu-id="798f3-140">tooaccount for this when parsing, we split hello header value on a space and select hello last string from hello returned array of strings.</span></span> <span data-ttu-id="798f3-141">這樣可為格式錯誤的授權標頭提供因應措施。</span><span class="sxs-lookup"><span data-stu-id="798f3-141">This provides a workaround for badly formatted authorization headers.</span></span>

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-hello-validation-request"></a><span data-ttu-id="798f3-142">發出 hello 驗證要求</span><span class="sxs-lookup"><span data-stu-id="798f3-142">Making hello validation request</span></span>
<span data-ttu-id="798f3-143">一旦 hello 授權權杖，我們可以讓 hello 要求 toovalidate hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="798f3-143">Once we have hello authorization token, we can make hello request toovalidate hello token.</span></span> <span data-ttu-id="798f3-144">RFC 7662 呼叫此處理序自我並要求您`POST`HTML 表單 toohello 自我資源。</span><span class="sxs-lookup"><span data-stu-id="798f3-144">RFC 7662 calls this process introspection and requires that you `POST` a HTML form toohello introspection resource.</span></span> <span data-ttu-id="798f3-145">hello HTML 表單至少必須包含與 hello 索引鍵的索引鍵/值組`token`。</span><span class="sxs-lookup"><span data-stu-id="798f3-145">hello HTML form must at least contain a key/value pair with hello key `token`.</span></span> <span data-ttu-id="798f3-146">此要求 toohello 授權伺服器也必須是惡意用戶端無法移 trawling 有效權杖的已驗證的 tooensure。</span><span class="sxs-lookup"><span data-stu-id="798f3-146">This request toohello authorization server must also be authenticated tooensure that malicious clients cannot go trawling for valid tokens.</span></span>

```xml
<send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">
  <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>
  <set-method>POST</set-method>
  <set-header name="Authorization" exists-action="override">
    <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>
  </set-header>
  <set-header name="Content-Type" exists-action="override">
    <value>application/x-www-form-urlencoded</value>
  </set-header>
  <set-body>@($"token={(string)context.Variables["token"]}")</set-body>
</send-request>
```

### <a name="checking-hello-response"></a><span data-ttu-id="798f3-147">檢查 hello 回應</span><span class="sxs-lookup"><span data-stu-id="798f3-147">Checking hello response</span></span>
<span data-ttu-id="798f3-148">hello`response-variable-name`屬性是使用的 toogive 存取 hello 傳回的回應。</span><span class="sxs-lookup"><span data-stu-id="798f3-148">hello `response-variable-name` attribute is used toogive access hello returned response.</span></span> <span data-ttu-id="798f3-149">hello 這個屬性中所定義名稱可用來做為索引鍵 hello`context.Variables`字典 tooaccess hello`IResponse`物件。</span><span class="sxs-lookup"><span data-stu-id="798f3-149">hello name defined in this property can be used as a key into hello `context.Variables` dictionary tooaccess hello `IResponse` object.</span></span>

<span data-ttu-id="798f3-150">從 hello 回應物件中，我們可以擷取 hello 主體和 RFC 7622 告訴我們 hello 回應必須是 JSON 物件，並必須包含至少一個屬性稱為`active`也就是布林值。</span><span class="sxs-lookup"><span data-stu-id="798f3-150">From hello response object we can retrieve hello body and RFC 7622 tells us that hello response must be a JSON object and must contain at least a property called `active` that is a boolean value.</span></span> <span data-ttu-id="798f3-151">當`active`hello 語彙基元會被視為有效則為 true。</span><span class="sxs-lookup"><span data-stu-id="798f3-151">When `active` is true then hello token is considered valid.</span></span>

### <a name="reporting-failure"></a><span data-ttu-id="798f3-152">報告失敗</span><span class="sxs-lookup"><span data-stu-id="798f3-152">Reporting failure</span></span>
<span data-ttu-id="798f3-153">我們使用`<choose>`原則 toodetect 如果 hello 語彙基元無效，而且如果是，會傳回 401 回應。</span><span class="sxs-lookup"><span data-stu-id="798f3-153">We use a `<choose>` policy toodetect if hello token is invalid and if so, return a 401 response.</span></span>

```xml
<choose>
  <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">
    <return-response response-variable-name="existing response variable">
      <set-status code="401" reason="Unauthorized" />
      <set-header name="WWW-Authenticate" exists-action="override">
        <value>Bearer error="invalid_token"</value>
      </set-header>
    </return-response>
  </when>
</choose>
```

<span data-ttu-id="798f3-154">根據[RFC 6750](https://tools.ietf.org/html/rfc6750#section-3)用來描述如何`bearer`應該使用語彙基元，我們也會傳回`WWW-Authenticate`hello 401 回應標頭。</span><span class="sxs-lookup"><span data-stu-id="798f3-154">As per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) which describes how `bearer` tokens should be used, we also return a `WWW-Authenticate` header with hello 401 response.</span></span> <span data-ttu-id="798f3-155">hello WWW 驗證是預定的 tooinstruct 方式上的用戶端 tooconstruct 適當授權的要求。</span><span class="sxs-lookup"><span data-stu-id="798f3-155">hello WWW-Authenticate is intended tooinstruct a client on how tooconstruct a properly authorized request.</span></span> <span data-ttu-id="798f3-156">Toohello 各種不同的方法可能與 hello OAuth2 架構，因為很難 toocommunicate 所有 hello 必要的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="798f3-156">Due toohello wide variety of approaches possible with hello OAuth2 framework, it is difficult toocommunicate all hello needed information.</span></span> <span data-ttu-id="798f3-157">幸運的是有工作進行 toohelp [tooproperly 如何授權要求 tooa 資源伺服器的用戶端探索](http://tools.ietf.org/html/draft-jones-oauth-discovery-00)。</span><span class="sxs-lookup"><span data-stu-id="798f3-157">Fortunately there are efforts underway toohelp [clients discover how tooproperly authorize requests tooa resource server](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span></span>

### <a name="final-solution"></a><span data-ttu-id="798f3-158">最終解決方案</span><span class="sxs-lookup"><span data-stu-id="798f3-158">Final solution</span></span>
<span data-ttu-id="798f3-159">我們將 hello 的所有項目放在一起，得到下列原則 hello:</span><span class="sxs-lookup"><span data-stu-id="798f3-159">Putting all hello pieces together, we get hello following policy:</span></span>

```xml
<inbound>
  <!-- Extract Token from Authorization header parameter -->
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />

  <!-- Send request tooToken Server toovalidate token (see RFC 7662) -->
  <send-request mode="new" response-variable-name="tokenstate" timeout="20" ignore-error="true">
    <set-url>https://microsoft-apiappec990ad4c76641c6aea22f566efc5a4e.azurewebsites.net/introspection</set-url>
    <set-method>POST</set-method>
    <set-header name="Authorization" exists-action="override">
      <value>basic dXNlcm5hbWU6cGFzc3dvcmQ=</value>
    </set-header>
    <set-header name="Content-Type" exists-action="override">
      <value>application/x-www-form-urlencoded</value>
    </set-header>
    <set-body>@($"token={(string)context.Variables["token"]}")</set-body>
  </send-request>

  <choose>
          <!-- Check active property in response -->
          <when condition="@((bool)((IResponse)context.Variables["tokenstate"]).Body.As<JObject>()["active"] == false)">
              <!-- Return 401 Unauthorized with http-problem payload -->
              <return-response response-variable-name="existing response variable">
                  <set-status code="401" reason="Unauthorized" />
                  <set-header name="WWW-Authenticate" exists-action="override">
                      <value>Bearer error="invalid_token"</value>
                  </set-header>
              </return-response>
          </when>
      </choose>
  <base />
</inbound>
```

<span data-ttu-id="798f3-160">這是其中一個方式的許多範例 hello`send-request`原則可以是使用的 toointegrate 有用外部的服務要求和回應流經 hello API 管理服務的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="798f3-160">This is only one of many examples of how hello `send-request` policy can be used toointegrate useful external services into hello process of requests and responses flowing through hello API Management service.</span></span>

## <a name="response-composition"></a><span data-ttu-id="798f3-161">回應組合</span><span class="sxs-lookup"><span data-stu-id="798f3-161">Response Composition</span></span>
<span data-ttu-id="798f3-162">hello`send-request`原則可用來增強主要要求 tooa 後端系統，我們了解在 hello 前一個範例中，或做為 hello 後端呼叫的完整取代。</span><span class="sxs-lookup"><span data-stu-id="798f3-162">hello `send-request` policy can be used for enhancing a primary request tooa backend system, as we saw in hello previous example, or it can be used as a complete replace for of hello backend call.</span></span> <span data-ttu-id="798f3-163">使用這項技術，我們可以輕鬆地建立複合資源，這些資源彙總自多個不同的系統。</span><span class="sxs-lookup"><span data-stu-id="798f3-163">Using this technique we can easily create composite resources that are aggregated from multiple different systems.</span></span>

### <a name="building-a-dashboard"></a><span data-ttu-id="798f3-164">建置儀表板</span><span class="sxs-lookup"><span data-stu-id="798f3-164">Building a dashboard</span></span>
<span data-ttu-id="798f3-165">有時候您會想 toobe 無法 tooexpose 資訊存在於多個後端系統，例如 toodrive 儀表板。</span><span class="sxs-lookup"><span data-stu-id="798f3-165">Sometimes you want toobe able tooexpose information that exists in multiple backend systems, for example, toodrive a dashboard.</span></span> <span data-ttu-id="798f3-166">hello Kpi 是從所有不同的後端，但您偏好 tooprovide 直接存取 toothem 而應該不錯如果 hello 的所有資訊無法都擷取單一要求中。</span><span class="sxs-lookup"><span data-stu-id="798f3-166">hello KPIs come from all different back-ends, but you would prefer not tooprovide direct access toothem and it would be nice if all hello information could be retrieved in a single request.</span></span> <span data-ttu-id="798f3-167">Hello 後端資訊的某些部分可能需要一些切割和細分有點免於第一次 ！</span><span class="sxs-lookup"><span data-stu-id="798f3-167">Perhaps some of hello backend information needs some slicing and dicing and a little sanitizing first!</span></span> <span data-ttu-id="798f3-168">要能 toocache 複合資源，會是很有用的 tooreduce hello 後端載入您知道使用者可以防止攻擊中順序 toosee hello F5 鍵，如果可能會變更其 underperforming 度量習慣。</span><span class="sxs-lookup"><span data-stu-id="798f3-168">Being able toocache that composite resource would be a useful tooreduce hello backend load as you know users have a habit of hammering hello F5 key in order toosee if their underperforming metrics might change.</span></span>    

### <a name="faking-hello-resource"></a><span data-ttu-id="798f3-169">假裝 hello 資源</span><span class="sxs-lookup"><span data-stu-id="798f3-169">Faking hello resource</span></span>
<span data-ttu-id="798f3-170">hello 第一個步驟 toobuilding 我們的儀表板資源是 tooconfigure hello API 管理發行者入口網站中的新作業。</span><span class="sxs-lookup"><span data-stu-id="798f3-170">hello first step toobuilding our dashboard resource is tooconfigure a new operation in hello API Management publisher portal.</span></span> <span data-ttu-id="798f3-171">這將會是預留位置用作業 tooconfigure 我們組合原則 toobuild 我們動態的資源。</span><span class="sxs-lookup"><span data-stu-id="798f3-171">This will be a placeholder operation used tooconfigure our composition policy toobuild our dynamic resource.</span></span>

![儀表板作業](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-hello-requests"></a><span data-ttu-id="798f3-173">提出 hello 要求</span><span class="sxs-lookup"><span data-stu-id="798f3-173">Making hello requests</span></span>
<span data-ttu-id="798f3-174">一次 hello`dashboard`已建立作業我們可以設定原則特別針對該作業。</span><span class="sxs-lookup"><span data-stu-id="798f3-174">Once hello `dashboard` operation has been created we can configure a policy specifically for that operation.</span></span> 

![儀表板作業](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

<span data-ttu-id="798f3-176">hello 第一個步驟是 tooextract hello 傳入的要求，從任何查詢參數，讓我們可以將它們轉送 tooour 後端。</span><span class="sxs-lookup"><span data-stu-id="798f3-176">hello first step  is tooextract any query parameters from hello incoming request, so that we can forward them tooour backend.</span></span> <span data-ttu-id="798f3-177">在此範例中，我們的儀表板會根據一段時間來顯示資訊，因此具有 `fromDate` 和 `toDate` 參數。</span><span class="sxs-lookup"><span data-stu-id="798f3-177">In this example our dashboard is showing information based on a period of time an therefore has a `fromDate` and `toDate` parameter.</span></span> <span data-ttu-id="798f3-178">我們可以使用 hello `set-variable` hello 要求 URL 的原則 tooextract hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="798f3-178">We can use hello `set-variable` policy tooextract hello information from hello request URL.</span></span>

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

<span data-ttu-id="798f3-179">一旦我們有這項資訊我們可以讓要求 tooall hello 後端系統。</span><span class="sxs-lookup"><span data-stu-id="798f3-179">Once we have this information we can make requests tooall hello backend systems.</span></span> <span data-ttu-id="798f3-180">每個要求建構新的 URL 與 hello 參數資訊並呼叫其個別的伺服器，並將 hello 回應儲存在內容變數。</span><span class="sxs-lookup"><span data-stu-id="798f3-180">Each request constructs a new URL with hello parameter information and calls its respective server and stores hello response in a context variable.</span></span>

```xml
<send-request mode="new" response-variable-name="revenuedata" timeout="20" ignore-error="true">
  <set-url>@($"https://accounting.acme.com/salesdata?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="materialdata" timeout="20" ignore-error="true">
  <set-url>@($"https://inventory.acme.com/materiallevels?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="throughputdata" timeout="20" ignore-error="true">
<set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>

<send-request mode="new" response-variable-name="accidentdata" timeout="20" ignore-error="true">
<set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="798f3-181">這些要求將會依序執行，但這並不理想。</span><span class="sxs-lookup"><span data-stu-id="798f3-181">These requests will execute in sequence, which is not ideal.</span></span> <span data-ttu-id="798f3-182">近期版本中我們將會導入新原則呼叫`wait`可讓所有這些要求 tooexecute，以平行方式。</span><span class="sxs-lookup"><span data-stu-id="798f3-182">In an upcoming release we will be introducing a new policy called `wait` that will enable all of these requests tooexecute in parallel.</span></span>

### <a name="responding"></a><span data-ttu-id="798f3-183">回應</span><span class="sxs-lookup"><span data-stu-id="798f3-183">Responding</span></span>
<span data-ttu-id="798f3-184">我們可以使用 hello tooconstruct hello 複合回應[傳回回應](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse)原則。</span><span class="sxs-lookup"><span data-stu-id="798f3-184">tooconstruct hello composite response we can use hello [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policy.</span></span> <span data-ttu-id="798f3-185">hello`set-body`元素可使用運算式 tooconstruct 新`JObject`與所有 hello 元件表示內嵌為屬性。</span><span class="sxs-lookup"><span data-stu-id="798f3-185">hello `set-body` element can use an expression tooconstruct a new `JObject` with all hello component representations embedded as properties.</span></span>

```xml
<return-response response-variable-name="existing response variable">
  <set-status code="200" reason="OK" />
  <set-header name="Content-Type" exists-action="override">
    <value>application/json</value>
  </set-header>
  <set-body>
    @(new JObject(new JProperty("revenuedata",((IResponse)context.Variables["revenuedata"]).Body.As<JObject>()),
                  new JProperty("materialdata",((IResponse)context.Variables["materialdata"]).Body.As<JObject>()),
                  new JProperty("throughputdata",((IResponse)context.Variables["throughputdata"]).Body.As<JObject>()),
                  new JProperty("accidentdata",((IResponse)context.Variables["accidentdata"]).Body.As<JObject>())
                  ).ToString())
  </set-body>
</return-response>
```

<span data-ttu-id="798f3-186">hello 原則如下所示：</span><span class="sxs-lookup"><span data-stu-id="798f3-186">hello complete policy looks as follows:</span></span>

```xml
<policies>
    <inbound>

  <set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
  <set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">

    <send-request mode="new" response-variable-name="revenuedata" timeout="20" ignore-error="true">
      <set-url>@($"https://accounting.acme.com/salesdata?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="materialdata" timeout="20" ignore-error="true">
      <set-url>@($"https://inventory.acme.com/materiallevels?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="throughputdata" timeout="20" ignore-error="true">
    <set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <send-request mode="new" response-variable-name="accidentdata" timeout="20" ignore-error="true">
    <set-url>@($"https://production.acme.com/throughput?from={(string)context.Variables["fromDate"]}&to={(string)context.Variables["fromDate"]}")"</set-url>
      <set-method>GET</set-method>
    </send-request>

    <return-response response-variable-name="existing response variable">
      <set-status code="200" reason="OK" />
      <set-header name="Content-Type" exists-action="override">
        <value>application/json</value>
      </set-header>
      <set-body>
        @(new JObject(new JProperty("revenuedata",((IResponse)context.Variables["revenuedata"]).Body.As<JObject>()),
                      new JProperty("materialdata",((IResponse)context.Variables["materialdata"]).Body.As<JObject>()),
                      new JProperty("throughputdata",((IResponse)context.Variables["throughputdata"]).Body.As<JObject>()),
                      new JProperty("accidentdata",((IResponse)context.Variables["accidentdata"]).Body.As<JObject>())
                      ).ToString())
      </set-body>
    </return-response>
    </inbound>
    <backend>
        <base />
    </backend>
    <outbound>
        <base />
    </outbound>
</policies>
```

<span data-ttu-id="798f3-187">我們可以設定 hello 預留位置作業 hello 組態中 hello 儀表板資源 toobe 快取的至少一小時因為我們了解 hello 性質 hello 資料表示，即使它是一小時過期，仍然會充分有效toohello tooconvey 寶貴資訊的使用者。</span><span class="sxs-lookup"><span data-stu-id="798f3-187">In hello configuration of hello placeholder operation we can configure hello dashboard resource toobe cached for at least an hour because we understand hello nature of hello data means that even if it is an hour out of date, it will still be sufficiently effective tooconvey valuable information toohello users.</span></span>

## <a name="summary"></a><span data-ttu-id="798f3-188">摘要</span><span class="sxs-lookup"><span data-stu-id="798f3-188">Summary</span></span>
<span data-ttu-id="798f3-189">Azure API 管理服務提供的彈性化原則，可以選擇性地套用 tooHTTP 流量，並可讓後端服務的構成要素。</span><span class="sxs-lookup"><span data-stu-id="798f3-189">Azure API Management service provides flexible policies that can be selectively applied tooHTTP traffic and enables composition of backend services.</span></span> <span data-ttu-id="798f3-190">當您想 tooenhance API 閘道與警示函式、 驗證、 驗證功能，或建立新的複合資源，根據多個後端服務，hello`send-request`和相關的原則開啟明亮的。</span><span class="sxs-lookup"><span data-stu-id="798f3-190">Whether you want tooenhance your API gateway with alerting functions, verification, validation capabilities or create new composite resources based on multiple backend services, hello `send-request` and related policies open a world of possibilities.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="798f3-191">觀看這些原則的影片概觀</span><span class="sxs-lookup"><span data-stu-id="798f3-191">Watch a video overview of these policies</span></span>
<span data-ttu-id="798f3-192">如需有關 hello[傳送一個方式-要求](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest)，[傳送要求](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest)，和[傳回回應](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse)原則涵蓋在本文中，請密切注意 hello 下列視訊。</span><span class="sxs-lookup"><span data-stu-id="798f3-192">For more information on hello [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), and [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policies covered in this article, please watch hello following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

