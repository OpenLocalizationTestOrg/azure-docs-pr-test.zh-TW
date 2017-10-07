---
title: "aaaCustom 快取在 Azure API 管理"
description: "了解 toocache 在 Azure API 管理中的索引鍵的項目"
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 772bc8dd-5cda-41c4-95bf-b9f6f052bc85
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 681380743c8c96af5d0a8e25948a8c0663e9fd35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="custom-caching-in-azure-api-management"></a>在 Azure API 管理中自訂快取
Azure API 管理服務已內建支援[快取 HTTP 回應](api-management-howto-cache.md)hello 索引鍵使用 hello 資源 URL。 hello 金鑰就可以修改的要求標頭使用 hello`vary-by`屬性。 這適用於快取整個 HTTP 回應 （也稱為表示法），但有時候很有用的 toojust 快取的表示法的部分。 新的 hello[快取查閱值](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey)和[快取存放區值](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey)原則提供 hello 能力 toostore 並擷取任意內部原則定義的資料。 這項功能也會將先前導入的值 toohello[傳送要求](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest)原則因為您現在可以快取從外部服務的回應。

## <a name="architecture"></a>架構
API 管理服務會使用共用每個租用戶資料快取，以便為您 toomultiple 單位向上延展您仍可以存取 toohello 相同快取資料。 不過，使用多區域部署時有個 hello 區域內的獨立快取。 到期 toothis，務必 toonot hello 快取視為資料存放區，其所在的部分資訊片段 hello 唯一來源。 如果您未，並稍後決定 tootake 優點 hello 多區域部署時，客戶與旅行的使用者可能會遺失存取 toothat 快取資料。

## <a name="fragment-caching"></a>片段快取
有某些情況下，其中傳回的回應包含某些部分是高度耗費資源的 toodetermine，還會在合理的時間的保留全新的資料。 以航空公司建立的服務為例，服務提供航班訂位、航班狀態等相關資訊。如果 hello 使用者所屬的 hello airlines 點程式，他們也會擁有與 tootheir 目前狀態和累積的里程數資訊。 此使用者相關的資訊可能會儲存在不同的系統，但它可能會希望 tooinclude 它在回應中傳回有關航班狀態和保留項目。 這可以用稱為｢片段快取｣的程序做到。 hello 主要的表示法可從傳回使用某種類型的語彙基元 tooindicate 其中 hello 與使用者相關的資訊插入 toobe hello 原始伺服器。 

請考慮下列 JSON 回應從後端應用程式開發介面的 hello。

```json
{
  "airline" : "Air Canada",
  "flightno" : "871",
  "status" : "ontime",
  "gate" : "B40",
  "terminal" : "2A",
  "userprofile" : "$userprofile$"
}  
```

在 `/userprofile/{userid}` 的次要資源看起來像，

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

在訂單 toodetermine hello 適當的使用者資訊 tooinclude，我們需要 tooidentify hello 終端使用者是。 這個機制取決於實作。 例如，我使用 hello`Subject`宣告的`JWT`語彙基元。 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

我們會將這個 `enduserid` 值儲存在內容變數中供稍後使用。 如果已擷取 hello 使用者資訊並儲存在 hello 快取中前一個要求，就 toodetermine hello 下一個步驟。 為此，我們使用 hello`cache-lookup-value`原則。

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

如果對應 toohello 索引鍵值，則否 hello 快取中沒有任何項目`userprofile`內容變數將會建立。 我們會檢查使用 hello hello 查閱 hello 成功`choose`控制流程原則。

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If hello userprofile context variable doesn’t exist, make an HTTP request tooretrieve it.  -->
    </when>
</choose>
```

如果 hello`userprofile`內容變數不存在，則我們會持續 toohave toomake HTTP 要求 tooretrieve 它。

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points toohello profile for hello current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

我們使用 hello `enduserid` tooconstruct hello URL toohello 使用者設定檔資源。 一旦 hello 回應，我們可以拉出 hello 回應 hello 本文文字，並將它儲存回內容變數。

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

tooavoid 我們需要 toomake 此 HTTP 要求，hello 相同的使用者發出另一個要求時，我們可以儲存 hello 使用者設定檔在 hello 快取中。

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

我們使用 hello 完全相同索引鍵我們原本嘗試 tooretrieve hello 快取中儲存 hello 值使用。 hello，我們選擇 toostore hello 值的持續時間應根據頻率 hello 資訊變更以及如何容錯被使用者 tooout 的日期資訊。 

重要 toorealize，從 hello 快取擷取仍然是跨處理序、 網路要求，並可能還是可以加入數十毫秒 toohello 要求。 決定 hello 使用者設定檔資訊花的時間大幅多於，到期 tooneeding toodo 資料庫查詢或從多個後端的彙總資訊時，就會開始 hello 優點。

hello hello 程序中的最後一個步驟是 tooupdate hello 傳回我們的使用者設定檔資訊的回應。

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

選取了 tooinclude hello 引號當成 hello token 的一部分，以便 hello 回應 hello 取代不會發生，即使是仍然有效的 JSON。 這是主要 toomake 偵錯更容易。

一旦您將一起結合所有這些步驟，hello 最終結果會是看起來像 hello 下列其中一個原則。

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in hello cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in hello cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request tooget user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points toohello profile for hello current end-user -->
                    <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),(string)context.Variables["enduserid"]).AbsoluteUri)</set-url>
                    <set-method>GET</set-method>
                </send-request>

                <!-- Store response body in context variable -->
                <set-variable
                  name="userprofile"
                  value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />

                <!-- Store result in cache -->
                <cache-store-value
                  key="@("userprofile-" + context.Variables["enduserid"])"
                  value="@((string)context.Variables["userprofile"])"
                  duration="100000" />
            </when>
        </choose>
        <base />
    </inbound>
    <outbound>
        <!-- Update response body with user profile-->
        <find-and-replace
              from='"$userprofile$"'
              to="@((string)context.Variables["userprofile"])" />
        <base />
    </outbound>
</policies>
```

此快取的方法主要使用在網站中，HTML 組成 hello 伺服器端上，讓它可以轉譯成單一頁面。 不過，它也可以用於應用程式開發介面，用戶端無法執行動作用戶端端 HTTP 快取，或最好不 tooput hello 用戶端上的該項責任。

此同類的片段快取也可以透過使用 Redis 快取伺服器 hello 後端 web 伺服器上，不過，使用 hello API 管理服務 tooperform 這項工作時，快取的 hello 片段來自不同的後端比 hello主要的回應。

## <a name="transparent-versioning"></a>透明的版本設定
一般作法是讓多個不同的實作版本支援在任何時候 API toobe。 這可能是 toosupport 不同環境，例如開發、 測試、 生產等，或者可能是 toosupport API 取用者 toomigrate toonewer 版本 hello API toogive 時間的較舊的版本。 

此改為需要從用戶端開發人員 toochange hello Url 的其中一個方法 toohandling`/v1/customers`太`/v2/customers`也無需 toostore hello 取用者的設定檔資料中的 hello API 版本他們目前想 toouse 呼叫適當的 hello後端 URL。 在訂單 toodetermine hello 正確的後端 URL toocall 特定用戶端，就需要 tooquery 某些組態資料。 藉由快取此設定資料，我們可以最小化 hello 執行這項執行此查詢的效能帶來負面影響。

hello 第一個步驟是 toodetermine hello 識別項使用 tooconfigure hello 所需的版本。 在此範例中，選取了 tooassociate hello 版本 toohello 產品訂用帳戶金鑰。 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

我們接著執行快取查閱 toosee，如果我們已經有擷取 hello 所需的用戶端版本。

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

然後我們會檢查 toosee 如果我們找不到它在 hello 快取中。

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

如果沒有，就去擷取它。

```xml
<send-request
    mode="new"
    response-variable-name="clientconfiguresponse"
    timeout="10"
    ignore-error="true">
            <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
            <set-method>GET</set-method>
</send-request>
```

擷取 hello 回應 hello 回應本文文字。

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

請將它儲存回在 hello 快取供未來使用。

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

與最後更新 hello 後端 URL tooselect hello 版本 hello hello 用戶端所需的服務。

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

hello 完全原則如下所示。

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in hello cache, make a request for it and store it -->
    <choose>
        <when condition="@(!context.Variables.ContainsKey("clientversion"))">
            <send-request mode="new" response-variable-name="clientconfiguresponse" timeout="10" ignore-error="true">
                <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
                <set-method>GET</set-method>
            </send-request>
            <!-- Store response body in context variable -->
            <set-variable name="clientversion" value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
            <!-- Store result in cache -->
            <cache-store-value key="@("clientversion-" + context.Variables["clientid"])" value="@((string)context.Variables["clientversion"])" duration="100000" />
        </when>
    </choose>
    <set-backend-service base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
</inbound>
```

啟用後端版本由用戶端不需要 tooupdate 和重新部署用戶端存取 API 取用者 tootransparently 控制是一種精緻的解決方案，解決許多應用程式開發介面版本設定問題。

## <a name="tenant-isolation"></a>租用戶隔離
在大型、多租用戶的部署中，有些公司會在後端硬體的不同部署上建立不同的租用戶群組。 這會將 hello hello 後端上的硬體問題所影響的客戶數目降到最低。 它也可讓新的軟體版本 toobe 階段中推出。 在理想情況下這個後端架構應該是透明的 tooAPI 取用者。 這可以來達成類似的方式 tootransparent 版本控制中因為它根據 hello 操作 hello 後端 URL 使用每個應用程式開發介面的索引鍵的設定狀態的相同技巧。  

而不是傳回 hello API 的每個訂用帳戶金鑰的慣用的版本，您將會傳回有關租用戶指派 toohello 硬體群組識別項。 該識別碼可以是使用的 tooconstruct hello 適當的後端 URL。

## <a name="summary"></a>摘要
hello 自由 toouse hello Azure API 管理快取來儲存任何種類的資料可讓您能夠有效率地存取 tooconfiguration 資料可能會影響 hello 方式處理傳入的要求。 它也可以使用的 toostore 資料片段可以擴大從後端 API 傳回的回應。

## <a name="next-steps"></a>後續步驟
請提供您的意見 hello Disqus 執行緒中取得此主題是否有目前可能會有這些原則已啟用，或如果沒有案例希望 tooachieve，但不要覺得其他案例。

