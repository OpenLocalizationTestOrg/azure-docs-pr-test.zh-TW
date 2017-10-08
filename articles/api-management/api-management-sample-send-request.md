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
# <a name="using-external-services-from-hello-azure-api-management-service"></a>使用來自 hello Azure API 管理服務的外部服務
hello 原則可在 Azure API 管理服務可以執行各種不同的有用的工作只根據 hello 連入要求、 hello 外寄回應和基本設定資訊。 不過，所能 toointeract 與外部服務從 API 管理原則會開啟更多的機會。

我們先前看過我們可以互動 hello[來記錄、 監視和分析 Azure 事件中心服務](api-management-log-to-eventhub-sample.md)。 本文章中我們將示範原則，可讓您使用任何外部 HTTP toointeract 基礎服務。 這些原則可以使用，用於觸發遠端事件或擷取將會使用的 toomanipulate hello 原始要求和回應以某種方式的資訊。

## <a name="send-one-way-request"></a>傳送單向要求
可能是由於 hello 最簡單的外部互動不 hello 和不理樣式可讓通知種類重要事件之外部服務 toobe 的要求。 我們可以使用 hello 控制流程原則`choose`toodetect 滿足任何一種狀況，我們有興趣，所以，如果 hello 條件為止，我們可以讓外部 HTTP 要求使用 hello[傳送一個方式-要求](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest)原則。 這可能是要求 tooa 傳訊系統，例如 Hipchat Slack 或如 SendGrid 或 MailChimp，郵件應用程式開發介面或類似的重大支援事件 PagerDuty。 所有的這些傳訊系統都具有簡單的 HTTP API，可讓我們輕鬆叫用。

### <a name="alerting-with-slack"></a>使用 Slack 提供警示
hello 下列範例會示範如何 toosend 訊息 tooa 延聊天室 hello HTTP 回應狀態碼是否大於或等於 too500。 500 範圍錯誤指出 hello API 的用戶端的問題與我們的後端應用程式開發介面不能自行解決。 通常我們需要進行某種形式的介入。  

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

Slack 有傳入的 web 攔截 hello 概念。 設定時傳入的 web 攔截，Slack 會產生特殊的 URL，這可讓您 toodo 簡單的 POST 要求和 toopass 訊息成 hello Slack 頻道。 hello 我們建立的 JSON 主體根據 Slack 所定義的格式。

![Slack 的 Web 攔截](./media/api-management-sample-send-request/api-management-slack-webhook.png)

### <a name="is-fire-and-forget-good-enough"></a>「射後不理」 夠好嗎？
使用要求的射後不理樣式有一些特定的權衡取捨。 如果基於某些原因，hello 要求失敗，就不會報告 hello 失敗。 在此特定情況下，不保證 hello 複雜度次要失敗報告系統並等待 hello 回應 hello 額外的效能成本。 案例中很重要的 toocheck hello 回應，然後 hello[傳送要求](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest)原則是更好的選項。

## <a name="send-request"></a>send-request
hello`send-request`使用外部服務 tooperform 複雜處理函式和傳回資料 toohello API 管理服務，可用於進一步處理原則的原則啟用。

### <a name="authorizing-reference-tokens"></a>授權參考權杖
API 管理的主要功能是保護後端資源。 如果您的 API 所使用的 hello 授權伺服器建立[JWT 權杖](http://jwt.io/)OAuth2 流程的一部分做為[Azure Active Directory](../active-directory/active-directory-aadconnect.md)存在，則您可以使用 hello`validate-jwt`原則 tooverify hello 有效性hello 語彙基元。 不過，某些授權伺服器建立所謂的[參考語彙基元](http://leastprivilege.com/2015/11/25/reference-tokens-and-introspection/)，而不進行呼叫後 toohello 授權伺服器無法驗證。

### <a name="standardized-introspection"></a>將自我檢查標準化
在過去的 hello 已經過驗證與授權伺服器參考語彙基元的任何標準化的方式。 不過最近提議的標準[RFC 7662](https://tools.ietf.org/html/rfc7662) hello 定義資源伺服器可以如何確認語彙基元的 hello 有效性的 IETF 根據已發行。

### <a name="extracting-hello-token"></a>解壓縮 hello 語彙基元
hello 第一個步驟是從 hello 授權標頭的 tooextract hello 語彙基元。 hello 標頭值的格式應與 hello`Bearer`授權配置、 一個空格，然後 hello 授權權杖做為每個[RFC 6750](http://tools.ietf.org/html/rfc6750#section-2.1)。 不幸的是一些情況下則 hello 授權配置。 這個 tooaccount 剖析時，我們會分割上一個空格，再選取 hello hello 傳回字串陣列中的最後一個字串 hello 標頭值。 這樣可為格式錯誤的授權標頭提供因應措施。

```xml
<set-variable name="token" value="@(context.Request.Headers.GetValueOrDefault("Authorization","scheme param").Split(' ').Last())" />
```

### <a name="making-hello-validation-request"></a>發出 hello 驗證要求
一旦 hello 授權權杖，我們可以讓 hello 要求 toovalidate hello 語彙基元。 RFC 7662 呼叫此處理序自我並要求您`POST`HTML 表單 toohello 自我資源。 hello HTML 表單至少必須包含與 hello 索引鍵的索引鍵/值組`token`。 此要求 toohello 授權伺服器也必須是惡意用戶端無法移 trawling 有效權杖的已驗證的 tooensure。

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

### <a name="checking-hello-response"></a>檢查 hello 回應
hello`response-variable-name`屬性是使用的 toogive 存取 hello 傳回的回應。 hello 這個屬性中所定義名稱可用來做為索引鍵 hello`context.Variables`字典 tooaccess hello`IResponse`物件。

從 hello 回應物件中，我們可以擷取 hello 主體和 RFC 7622 告訴我們 hello 回應必須是 JSON 物件，並必須包含至少一個屬性稱為`active`也就是布林值。 當`active`hello 語彙基元會被視為有效則為 true。

### <a name="reporting-failure"></a>報告失敗
我們使用`<choose>`原則 toodetect 如果 hello 語彙基元無效，而且如果是，會傳回 401 回應。

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

根據[RFC 6750](https://tools.ietf.org/html/rfc6750#section-3)用來描述如何`bearer`應該使用語彙基元，我們也會傳回`WWW-Authenticate`hello 401 回應標頭。 hello WWW 驗證是預定的 tooinstruct 方式上的用戶端 tooconstruct 適當授權的要求。 Toohello 各種不同的方法可能與 hello OAuth2 架構，因為很難 toocommunicate 所有 hello 必要的相關資訊。 幸運的是有工作進行 toohelp [tooproperly 如何授權要求 tooa 資源伺服器的用戶端探索](http://tools.ietf.org/html/draft-jones-oauth-discovery-00)。

### <a name="final-solution"></a>最終解決方案
我們將 hello 的所有項目放在一起，得到下列原則 hello:

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

這是其中一個方式的許多範例 hello`send-request`原則可以是使用的 toointegrate 有用外部的服務要求和回應流經 hello API 管理服務的 hello 程序。

## <a name="response-composition"></a>回應組合
hello`send-request`原則可用來增強主要要求 tooa 後端系統，我們了解在 hello 前一個範例中，或做為 hello 後端呼叫的完整取代。 使用這項技術，我們可以輕鬆地建立複合資源，這些資源彙總自多個不同的系統。

### <a name="building-a-dashboard"></a>建置儀表板
有時候您會想 toobe 無法 tooexpose 資訊存在於多個後端系統，例如 toodrive 儀表板。 hello Kpi 是從所有不同的後端，但您偏好 tooprovide 直接存取 toothem 而應該不錯如果 hello 的所有資訊無法都擷取單一要求中。 Hello 後端資訊的某些部分可能需要一些切割和細分有點免於第一次 ！ 要能 toocache 複合資源，會是很有用的 tooreduce hello 後端載入您知道使用者可以防止攻擊中順序 toosee hello F5 鍵，如果可能會變更其 underperforming 度量習慣。    

### <a name="faking-hello-resource"></a>假裝 hello 資源
hello 第一個步驟 toobuilding 我們的儀表板資源是 tooconfigure hello API 管理發行者入口網站中的新作業。 這將會是預留位置用作業 tooconfigure 我們組合原則 toobuild 我們動態的資源。

![儀表板作業](./media/api-management-sample-send-request/api-management-dashboard-operation.png)

### <a name="making-hello-requests"></a>提出 hello 要求
一次 hello`dashboard`已建立作業我們可以設定原則特別針對該作業。 

![儀表板作業](./media/api-management-sample-send-request/api-management-dashboard-policy.png)

hello 第一個步驟是 tooextract hello 傳入的要求，從任何查詢參數，讓我們可以將它們轉送 tooour 後端。 在此範例中，我們的儀表板會根據一段時間來顯示資訊，因此具有 `fromDate` 和 `toDate` 參數。 我們可以使用 hello `set-variable` hello 要求 URL 的原則 tooextract hello 資訊。

```xml
<set-variable name="fromDate" value="@(context.Request.Url.Query["fromDate"].Last())">
<set-variable name="toDate" value="@(context.Request.Url.Query["toDate"].Last())">
```

一旦我們有這項資訊我們可以讓要求 tooall hello 後端系統。 每個要求建構新的 URL 與 hello 參數資訊並呼叫其個別的伺服器，並將 hello 回應儲存在內容變數。

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

這些要求將會依序執行，但這並不理想。 近期版本中我們將會導入新原則呼叫`wait`可讓所有這些要求 tooexecute，以平行方式。

### <a name="responding"></a>回應
我們可以使用 hello tooconstruct hello 複合回應[傳回回應](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse)原則。 hello`set-body`元素可使用運算式 tooconstruct 新`JObject`與所有 hello 元件表示內嵌為屬性。

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

hello 原則如下所示：

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

我們可以設定 hello 預留位置作業 hello 組態中 hello 儀表板資源 toobe 快取的至少一小時因為我們了解 hello 性質 hello 資料表示，即使它是一小時過期，仍然會充分有效toohello tooconvey 寶貴資訊的使用者。

## <a name="summary"></a>摘要
Azure API 管理服務提供的彈性化原則，可以選擇性地套用 tooHTTP 流量，並可讓後端服務的構成要素。 當您想 tooenhance API 閘道與警示函式、 驗證、 驗證功能，或建立新的複合資源，根據多個後端服務，hello`send-request`和相關的原則開啟明亮的。

## <a name="watch-a-video-overview-of-these-policies"></a>觀看這些原則的影片概觀
如需有關 hello[傳送一個方式-要求](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendOneWayRequest)，[傳送要求](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest)，和[傳回回應](https://msdn.microsoft.com/library/azure/dn894085.aspx#ReturnResponse)原則涵蓋在本文中，請密切注意 hello 下列視訊。

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Send-Request-and-Return-Response-Policies/player]
> 
> 

