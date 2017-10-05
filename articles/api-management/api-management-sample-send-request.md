---
title: "使用 API 管理服務產生 HTTP 要求"
description: "了解如何使用 API 管理中的要求和回應原則，從您的 API 呼叫外部服務"
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
ms.openlocfilehash: e778943715d6ca5256ad612d82bdc1f82197df0d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="using-external-services-from-the-azure-api-management-service"></a><span data-ttu-id="bb015-103">使用來自 Azure API 管理服務的外部服務</span><span class="sxs-lookup"><span data-stu-id="bb015-103">Using external services from the Azure API Management service</span></span>
<span data-ttu-id="bb015-104">Azure API 管理服務中可用的原則可純粹根據連入要求、傳出回應及基本組態資訊來進行各式各樣的有用工作。</span><span class="sxs-lookup"><span data-stu-id="bb015-104">The policies available in Azure API Management service can do a wide range of useful work based purely on the incoming request, the outgoing response and basic configuration information.</span></span> <span data-ttu-id="bb015-105">不過，能夠與來自 API 管理原則的外部服務進行互動，可開啟更多的機會。</span><span class="sxs-lookup"><span data-stu-id="bb015-105">However, being able to interact with external services from API Management policies opens up many more opportunities.</span></span>

<span data-ttu-id="bb015-106">我們先前曾討論過如何與 [適用於記錄、監視及分析的 Azure 事件中樞服務](api-management-log-to-eventhub-sample.md)互動的方式。</span><span class="sxs-lookup"><span data-stu-id="bb015-106">We have previously seen how we can interact with the [Azure Event Hub service for logging, monitoring and analytics](api-management-log-to-eventhub-sample.md).</span></span> <span data-ttu-id="bb015-107">在本文中，我們將示範可讓您與任何以 HTTP 為基礎之外部服務進行互動的原則。</span><span class="sxs-lookup"><span data-stu-id="bb015-107">In this article we will demonstrate policies that allow you to interact with any external HTTP based service.</span></span> <span data-ttu-id="bb015-108">這些原則可用來觸發遠端事件，或用來擷取將以某種方式用於操作原始要求和回應的資訊。</span><span class="sxs-lookup"><span data-stu-id="bb015-108">These policies can be used for triggering remote events or for retrieving information that will be used to manipulate the original request and response in some way.</span></span>

## <a name="send-one-way-request"></a><span data-ttu-id="bb015-109">傳送單向要求</span><span class="sxs-lookup"><span data-stu-id="bb015-109">Send-One-Way-Request</span></span>
<span data-ttu-id="bb015-110">或許對要求來說，最簡單的外部互動是射後不理的樣式，讓外部服務能夠獲得某些種類之重要事件的通知。</span><span class="sxs-lookup"><span data-stu-id="bb015-110">Possibly the simplest external interaction is the fire-and-forget style of request that allows an external service to be notified of some kind of important event.</span></span> <span data-ttu-id="bb015-111">我們可以使用控制流程原則 `choose` 來偵測任何一種我們感興趣的狀況，接著，如果條件成立，我們就可以使用 [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) 原則提出外部的 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="bb015-111">We can use the control flow policy `choose` to detect any kind of condition that we are interested in and then, if the condition is satisfied, we can make an external HTTP request using the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest) policy.</span></span> <span data-ttu-id="bb015-112">這可能是對傳訊系統 (例如 Hipchat 或 Slack) 的要求，也可能是對郵件 API (例如 SendGrid 或 MailChimp) 的要求，或者是針對某些像是 PagerDuty 的重大支援事件的要求。</span><span class="sxs-lookup"><span data-stu-id="bb015-112">This could be a request to a messaging system like Hipchat or Slack, or a mail API like SendGrid or MailChimp, or for critical support incidents something like PagerDuty.</span></span> <span data-ttu-id="bb015-113">所有的這些傳訊系統都具有簡單的 HTTP API，可讓我們輕鬆叫用。</span><span class="sxs-lookup"><span data-stu-id="bb015-113">All of these messaging systems have simple HTTP APIs that we can easily invoke.</span></span>

### <a name="alerting-with-slack"></a><span data-ttu-id="bb015-114">使用 Slack 提供警示</span><span class="sxs-lookup"><span data-stu-id="bb015-114">Alerting with Slack</span></span>
<span data-ttu-id="bb015-115">下列範例示範如果 HTTP 回應狀態碼大於或等於 500，如何將訊息傳送至 Slack 聊天室。</span><span class="sxs-lookup"><span data-stu-id="bb015-115">The following example demonstrates how to send a message to a Slack chat room if the HTTP response status code is greater than or equal to 500.</span></span> <span data-ttu-id="bb015-116">500 範圍錯誤表示我們的後端 API發生問題，而我們 API 的用戶端無法解決這類問題。</span><span class="sxs-lookup"><span data-stu-id="bb015-116">A 500 range error indicates a problem with our backend API that the client of our API cannot resolve themselves.</span></span> <span data-ttu-id="bb015-117">通常我們需要進行某種形式的介入。</span><span class="sxs-lookup"><span data-stu-id="bb015-117">It usually requires some kind of intervention on our part.</span></span>  

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

<span data-ttu-id="bb015-118">Slack 具有傳入 Web 攔截的概念。</span><span class="sxs-lookup"><span data-stu-id="bb015-118">Slack has the notion of inbound web hooks.</span></span> <span data-ttu-id="bb015-119">在設定傳入的 Web 攔截時，Slack 會產生特殊的 URL，讓您能夠執行簡單的 POST 要求，並將訊息傳遞至 Slack 通道。</span><span class="sxs-lookup"><span data-stu-id="bb015-119">When configuring an inbound web hook, Slack generates a special URL which allows you to do a simple POST request and to pass a message into the Slack channel.</span></span> <span data-ttu-id="bb015-120">我們建立的 JSON 主體是以 Slack 所定義的格式為根據。</span><span class="sxs-lookup"><span data-stu-id="bb015-120">The JSON body that we create is based on a format defined by Slack.</span></span>

![Slack 的 Web 攔截](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a><span data-ttu-id="bb015-122">「射後不理」 夠好嗎？</span><span class="sxs-lookup"><span data-stu-id="bb015-122">Is fire and forget good enough?</span></span>
<span data-ttu-id="bb015-123">使用要求的射後不理樣式有一些特定的權衡取捨。</span><span class="sxs-lookup"><span data-stu-id="bb015-123">There are certain tradeoffs when using a fire-and-forget style of request.</span></span> <span data-ttu-id="bb015-124">如果基於某些原因而導致要求失敗，則不會報告失敗。</span><span class="sxs-lookup"><span data-stu-id="bb015-124">If for some reason, the request fails, then the failure will not be reported.</span></span> <span data-ttu-id="bb015-125">在此特殊情況下，無法保證具有次要失敗報告系統的複雜度，以及等待回應所需的其他效能成本。</span><span class="sxs-lookup"><span data-stu-id="bb015-125">In this particular situation, the complexity of having a secondary failure reporting system and the additional performance cost of waiting for the response is not warranted.</span></span> <span data-ttu-id="bb015-126">如果檢查回應很重要，則 [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) 原則是較好的選項。</span><span class="sxs-lookup"><span data-stu-id="bb015-126">For scenarios where it is essential to check the response, then the [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy is a better option.</span></span>

## <a name="send-request"></a><span data-ttu-id="bb015-127">send-request</span><span class="sxs-lookup"><span data-stu-id="bb015-127">Send-Request</span></span>
<span data-ttu-id="bb015-128">`send-request` 原則能夠使用外部服務來執行複雜的處理函式，並將資料傳回 API 管理服務，此服務可用來進一步處理原則。</span><span class="sxs-lookup"><span data-stu-id="bb015-128">The `send-request` policy enables using an external service to perform complex processing functions and return data to the API management service that can be used for further policy processing.</span></span>

### <a name="authorizing-reference-tokens"></a><span data-ttu-id="bb015-129">授權參考權杖</span><span class="sxs-lookup"><span data-stu-id="bb015-129">Authorizing reference tokens</span></span>
<span data-ttu-id="bb015-130">API 管理的主要功能是保護後端資源。</span><span class="sxs-lookup"><span data-stu-id="bb015-130">A major function of API Management is protecting backend resources.</span></span> <span data-ttu-id="bb015-131">如果您的 API 所使用的授權伺服器會建立 [JWT 權杖](http://jwt.io/) 做為其 OAuth2 流程的一部分，當 [Azure Active Directory](../active-directory/active-directory-aadconnect.md) 這樣做時，則您可以使用 `validate-jwt` 原則來驗證權杖的有效性。</span><span class="sxs-lookup"><span data-stu-id="bb015-131">If the authorization server used by your API creates [JWT tokens](http://jwt.io/) as part of its OAuth2 flow, as [Azure Active Directory](../active-directory/active-directory-aadconnect.md) does, then you can use the `validate-jwt` policy to verify the validity of the token.</span></span> <span data-ttu-id="bb015-132">不過，某些授權伺服器會建立所謂的 [參考權杖](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) ，其無法在不對授權伺服器進行回呼的情況下進行驗證。</span><span class="sxs-lookup"><span data-stu-id="bb015-132">However, some authorization servers create what are called [reference tokens](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/) that cannot be verified without making a call back to the authorization server.</span></span>

### <a name="standardized-introspection"></a><span data-ttu-id="bb015-133">將自我檢查標準化</span><span class="sxs-lookup"><span data-stu-id="bb015-133">Standardized introspection</span></span>
<span data-ttu-id="bb015-134">過去一直沒有標準化的方式可使用授權伺服器來驗證參考權杖。</span><span class="sxs-lookup"><span data-stu-id="bb015-134">In the past there has been no standardized way of verifying a reference token with an authorization server.</span></span> <span data-ttu-id="bb015-135">不過，IETF 最近發佈的提議標準 [RFC 7662](https://tools.ietf.org/html/rfc7662) 定義了資源伺服器如何驗證權杖的有效性。</span><span class="sxs-lookup"><span data-stu-id="bb015-135">However a recently proposed standard [RFC 7662](https://tools.ietf.org/html/rfc7662) was published by the IETF that defines how a resource server can verify the validity of a token.</span></span>

### <a name="extracting-the-token"></a><span data-ttu-id="bb015-136">擷取權杖</span><span class="sxs-lookup"><span data-stu-id="bb015-136">Extracting the token</span></span>
<span data-ttu-id="bb015-137">第一個步驟是從授權標頭擷取權杖。</span><span class="sxs-lookup"><span data-stu-id="bb015-137">The first step is to extract the token from the Authorization header.</span></span> <span data-ttu-id="bb015-138">標頭值應該使用 `Bearer` 授權配置、單一空格和授權權杖，按照每個 [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1)進行格式化。</span><span class="sxs-lookup"><span data-stu-id="bb015-138">The header value should be formatted with the `Bearer` authorization scheme, a single space and then the authorization token as per [RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1).</span></span> <span data-ttu-id="bb015-139">不過，有一些情況需要省略授權配置。</span><span class="sxs-lookup"><span data-stu-id="bb015-139">Unfortunately there are cases where the authorization scheme is omitted.</span></span> <span data-ttu-id="bb015-140">為了在剖析時說明這一點，我們會使用空格來分割標頭值，並從字串的傳回陣列中選取最後一個字串。</span><span class="sxs-lookup"><span data-stu-id="bb015-140">To account for this when parsing, we split the header value on a space and select the last string from the returned array of strings.</span></span> <span data-ttu-id="bb015-141">這樣可為格式錯誤的授權標頭提供因應措施。</span><span class="sxs-lookup"><span data-stu-id="bb015-141">This provides a workaround for badly formatted authorization headers.</span></span>

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-the-validation-request"></a><span data-ttu-id="bb015-142">提出驗證要求</span><span class="sxs-lookup"><span data-stu-id="bb015-142">Making the validation request</span></span>
<span data-ttu-id="bb015-143">一旦擁有授權權杖之後，就可以提出要求來驗證權杖。</span><span class="sxs-lookup"><span data-stu-id="bb015-143">Once we have the authorization token, we can make the request to validate the token.</span></span> <span data-ttu-id="bb015-144">RFC 7662 會呼叫此程序進行自我檢查，並要求您將 HTML 表單 `POST` 到自我檢查資源。</span><span class="sxs-lookup"><span data-stu-id="bb015-144">RFC 7662 calls this process introspection and requires that you `POST` a HTML form to the introspection resource.</span></span> <span data-ttu-id="bb015-145">HTML 表單至少必須包含具有索引鍵 `token`的索引鍵/值組。</span><span class="sxs-lookup"><span data-stu-id="bb015-145">The HTML form must at least contain a key/value pair with the key `token`.</span></span> <span data-ttu-id="bb015-146">這項對授權伺服器的要求也必須經過驗證，以確保惡意用戶端無法撈取有效的權杖。</span><span class="sxs-lookup"><span data-stu-id="bb015-146">This request to the authorization server must also be authenticated to ensure that malicious clients cannot go trawling for valid tokens.</span></span>

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

### <a name="checking-the-response"></a><span data-ttu-id="bb015-147">檢查回應</span><span class="sxs-lookup"><span data-stu-id="bb015-147">Checking the response</span></span>
<span data-ttu-id="bb015-148">`response-variable-name` 屬性可用來提供所傳回回應的存取權。</span><span class="sxs-lookup"><span data-stu-id="bb015-148">The `response-variable-name` attribute is used to give access the returned response.</span></span> <span data-ttu-id="bb015-149">這個屬性中定義的名稱可以用來做為 `context.Variables` 字典的索引鍵來存取 `IResponse` 物件。</span><span class="sxs-lookup"><span data-stu-id="bb015-149">The name defined in this property can be used as a key into the `context.Variables` dictionary to access the `IResponse` object.</span></span>

<span data-ttu-id="bb015-150">從回應物件中，我們可以擷取主體，而 RFC 7622 告訴我們，回應必須是 JSON 物件，而且必須包含至少一個稱為 `active` 的屬性 (此為布林值)。</span><span class="sxs-lookup"><span data-stu-id="bb015-150">From the response object we can retrieve the body and RFC 7622 tells us that the response must be a JSON object and must contain at least a property called `active` that is a boolean value.</span></span> <span data-ttu-id="bb015-151">當 `active` 為 true，則權杖會被視為有效。</span><span class="sxs-lookup"><span data-stu-id="bb015-151">When `active` is true then the token is considered valid.</span></span>

### <a name="reporting-failure"></a><span data-ttu-id="bb015-152">報告失敗</span><span class="sxs-lookup"><span data-stu-id="bb015-152">Reporting failure</span></span>
<span data-ttu-id="bb015-153">我們使用 `<choose>` 原則來偵測權杖是否無效，如果無效，則會傳回 401 回應。</span><span class="sxs-lookup"><span data-stu-id="bb015-153">We use a `<choose>` policy to detect if the token is invalid and if so, return a 401 response.</span></span>

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

<span data-ttu-id="bb015-154">根據每個說明應如何使用 `bearer` 權杖的 [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3)，我們也會傳回 `WWW-Authenticate` 標頭以及 401 回應。</span><span class="sxs-lookup"><span data-stu-id="bb015-154">As per [RFC 6750](https://tools.ietf.org/html/rfc6750#section-3) which describes how `bearer` tokens should be used, we also return a `WWW-Authenticate` header with the 401 response.</span></span> <span data-ttu-id="bb015-155">WWW 驗證的目的是指示用戶端如何建構適當授權的要求。</span><span class="sxs-lookup"><span data-stu-id="bb015-155">The WWW-Authenticate is intended to instruct a client on how to construct a properly authorized request.</span></span> <span data-ttu-id="bb015-156">由於有各式各樣可能具備 OAuth2 架構的處理方法，因此很難傳達所有必要的資訊。</span><span class="sxs-lookup"><span data-stu-id="bb015-156">Due to the wide variety of approaches possible with the OAuth2 framework, it is difficult to communicate all the needed information.</span></span> <span data-ttu-id="bb015-157">幸好我們仍持續努力來協助 [用戶端探索如何適當地將要求授權給資源伺服器](http://tools.ietf.org/html/draft-jones-oauth-discovery-00)。</span><span class="sxs-lookup"><span data-stu-id="bb015-157">Fortunately there are efforts underway to help [clients discover how to properly authorize requests to a resource server](http://tools.ietf.org/html/draft-jones-oauth-discovery-00).</span></span>

### <a name="final-solution"></a><span data-ttu-id="bb015-158">最終解決方案</span><span class="sxs-lookup"><span data-stu-id="bb015-158">Final solution</span></span>
<span data-ttu-id="bb015-159">將所有項目放在一起，就能得到下列原則：</span><span class="sxs-lookup"><span data-stu-id="bb015-159">Putting all the pieces together, we get the following policy:</span></span>

```xml
<inbound>
  <!-- Extract Token from Authorization header parameter -->
  <set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />

  <!-- Send request to Token Server to validate token (see RFC 7662) -->
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

<span data-ttu-id="bb015-160">這是眾多範例中唯一一個說明如何使用 `send-request` 原則來將有用的外部服務整合至要求和回應的程序，此程序的流程會通過 API 管理服務。</span><span class="sxs-lookup"><span data-stu-id="bb015-160">This is only one of many examples of how the `send-request` policy can be used to integrate useful external services into the process of requests and responses flowing through the API Management service.</span></span>

## <a name="response-composition"></a><span data-ttu-id="bb015-161">回應組合</span><span class="sxs-lookup"><span data-stu-id="bb015-161">Response Composition</span></span>
<span data-ttu-id="bb015-162">`send-request` 原則可用來增強對後端系統的主要要求 (如同我們在上述範例中所見)，或者它可用來完全取代後端呼叫。</span><span class="sxs-lookup"><span data-stu-id="bb015-162">The `send-request` policy can be used for enhancing a primary request to a backend system, as we saw in the previous example, or it can be used as a complete replace for of the backend call.</span></span> <span data-ttu-id="bb015-163">使用這項技術，我們可以輕鬆地建立複合資源，這些資源彙總自多個不同的系統。</span><span class="sxs-lookup"><span data-stu-id="bb015-163">Using this technique we can easily create composite resources that are aggregated from multiple different systems.</span></span>

### <a name="building-a-dashboard"></a><span data-ttu-id="bb015-164">建置儀表板</span><span class="sxs-lookup"><span data-stu-id="bb015-164">Building a dashboard</span></span>
<span data-ttu-id="bb015-165">有時您想要能夠公開存在於多個後端系統中的資訊，例如，驅動儀表板。</span><span class="sxs-lookup"><span data-stu-id="bb015-165">Sometimes you want to be able to expose information that exists in multiple backend systems, for example, to drive a dashboard.</span></span> <span data-ttu-id="bb015-166">KPI 來自所有不同的後端，但是您習慣不提供它們的直接存取權，而且如果所有資訊都是擷取自單一要求，這就非常有用。</span><span class="sxs-lookup"><span data-stu-id="bb015-166">The KPIs come from all different back-ends, but you would prefer not to provide direct access to them and it would be nice if all the information could be retrieved in a single request.</span></span> <span data-ttu-id="bb015-167">或許有一些後端資訊需要進行某些切割與細分，需要先稍微處理一下！</span><span class="sxs-lookup"><span data-stu-id="bb015-167">Perhaps some of the backend information needs some slicing and dicing and a little sanitizing first!</span></span> <span data-ttu-id="bb015-168">當您知道使用者習慣按 F5 鍵來查看其效能不佳的指標是否可能變更時，若要降低後端負載，能夠快取該複合資源就非常實用。</span><span class="sxs-lookup"><span data-stu-id="bb015-168">Being able to cache that composite resource would be a useful to reduce the backend load as you know users have a habit of hammering the F5 key in order to see if their underperforming metrics might change.</span></span>    

### <a name="faking-the-resource"></a><span data-ttu-id="bb015-169">假造資源</span><span class="sxs-lookup"><span data-stu-id="bb015-169">Faking the resource</span></span>
<span data-ttu-id="bb015-170">建置儀表板資源的第一個步驟是在 API 管理發行者入口網站中設定新的作業。</span><span class="sxs-lookup"><span data-stu-id="bb015-170">The first step to building our dashboard resource is to configure a new operation in the API Management publisher portal.</span></span> <span data-ttu-id="bb015-171">這是用來設定我們的撰寫原則以建置動態資源的預留位置作業。</span><span class="sxs-lookup"><span data-stu-id="bb015-171">This will be a placeholder operation used to configure our composition policy to build our dynamic resource.</span></span>

![儀表板作業](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-the-requests"></a><span data-ttu-id="bb015-173">提出要求</span><span class="sxs-lookup"><span data-stu-id="bb015-173">Making the requests</span></span>
<span data-ttu-id="bb015-174">一旦建立 `dashboard` 作業之後，我們就能特別針對該作業來設定原則。</span><span class="sxs-lookup"><span data-stu-id="bb015-174">Once the `dashboard` operation has been created we can configure a policy specifically for that operation.</span></span> 

![儀表板作業](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

<span data-ttu-id="bb015-176">第一個步驟是擷取來自傳入要求的任何查詢參數，讓我們可以將其轉送到後端。</span><span class="sxs-lookup"><span data-stu-id="bb015-176">The first step  is to extract any query parameters from the incoming request, so that we can forward them to our backend.</span></span> <span data-ttu-id="bb015-177">在此範例中，我們的儀表板會根據一段時間來顯示資訊，因此具有 `fromDate` 和 `toDate` 參數。</span><span class="sxs-lookup"><span data-stu-id="bb015-177">In this example our dashboard is showing information based on a period of time an therefore has a `fromDate` and `toDate` parameter.</span></span> <span data-ttu-id="bb015-178">我們可以使用 `set-variable` 原則來擷取要求 URL 中的資訊。</span><span class="sxs-lookup"><span data-stu-id="bb015-178">We can use the `set-variable` policy to extract the information from the request URL.</span></span>

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

<span data-ttu-id="bb015-179">一旦擁有這項資訊之後，就可以對所有後端系統提出要求。</span><span class="sxs-lookup"><span data-stu-id="bb015-179">Once we have this information we can make requests to all the backend systems.</span></span> <span data-ttu-id="bb015-180">每個要求都會使用參數資訊來建構新的 URL，並呼叫各自的伺服器，將回應儲存於內容變數中。</span><span class="sxs-lookup"><span data-stu-id="bb015-180">Each request constructs a new URL with the parameter information and calls its respective server and stores the response in a context variable.</span></span>

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

<span data-ttu-id="bb015-181">這些要求將會依序執行，但這並不理想。</span><span class="sxs-lookup"><span data-stu-id="bb015-181">These requests will execute in sequence, which is not ideal.</span></span> <span data-ttu-id="bb015-182">在即將推出的版本中，我們將導入稱為 `wait` 的新原則，讓所有的這些要求都能以平行方式執行。</span><span class="sxs-lookup"><span data-stu-id="bb015-182">In an upcoming release we will be introducing a new policy called `wait` that will enable all of these requests to execute in parallel.</span></span>

### <a name="responding"></a><span data-ttu-id="bb015-183">回應</span><span class="sxs-lookup"><span data-stu-id="bb015-183">Responding</span></span>
<span data-ttu-id="bb015-184">若要建構複合回應，我們可以使用 [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) 原則。</span><span class="sxs-lookup"><span data-stu-id="bb015-184">To construct the composite response we can use the [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policy.</span></span> <span data-ttu-id="bb015-185">`set-body` 元素可以使用運算式，來建構新的 `JObject` 以及內嵌為屬性的所有元件表示法。</span><span class="sxs-lookup"><span data-stu-id="bb015-185">The `set-body` element can use an expression to construct a new `JObject` with all the component representations embedded as properties.</span></span>

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

<span data-ttu-id="bb015-186">完整的原則看起來如下：</span><span class="sxs-lookup"><span data-stu-id="bb015-186">The complete policy looks as follows:</span></span>

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

<span data-ttu-id="bb015-187">在預留位置作業的組態中，我們可以將儀表板資源設定為至少快取一個小時，因為我們了解資料的本質意味著即使它在一個小時之後就會過期，仍然可以充分有效傳達重要資訊給使用者。</span><span class="sxs-lookup"><span data-stu-id="bb015-187">In the configuration of the placeholder operation we can configure the dashboard resource to be cached for at least an hour because we understand the nature of the data means that even if it is an hour out of date, it will still be sufficiently effective to convey valuable information to the users.</span></span>

## <a name="summary"></a><span data-ttu-id="bb015-188">Summary</span><span class="sxs-lookup"><span data-stu-id="bb015-188">Summary</span></span>
<span data-ttu-id="bb015-189">Azure API 管理服務提供彈性的原則，可以選擇性地套用到 HTTP 流量，並且能夠組合後端服務。</span><span class="sxs-lookup"><span data-stu-id="bb015-189">Azure API Management service provides flexible policies that can be selectively applied to HTTP traffic and enables composition of backend services.</span></span> <span data-ttu-id="bb015-190">不論您是否想要使用警示功能、確認、驗證功能或根據多個後端服務建立新的複合資源來增強您的 API 閘道器， `send-request` 及相關原則都會開啟各種可能性。</span><span class="sxs-lookup"><span data-stu-id="bb015-190">Whether you want to enhance your API gateway with alerting functions, verification, validation capabilities or create new composite resources based on multiple backend services, the `send-request` and related policies open a world of possibilities.</span></span>

## <a name="watch-a-video-overview-of-these-policies"></a><span data-ttu-id="bb015-191">觀看這些原則的影片概觀</span><span class="sxs-lookup"><span data-stu-id="bb015-191">Watch a video overview of these policies</span></span>
<span data-ttu-id="bb015-192">如需本文所介紹之 [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest)、[send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) 和 [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) 原則的詳細資訊，請觀看以下影片。</span><span class="sxs-lookup"><span data-stu-id="bb015-192">For more information on the [send-one-way-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest), [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest), and [return-response](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse) policies covered in this article, please watch the following video.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

