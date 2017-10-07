---
title: "aaaAzure API 管理跨網域原則 |Microsoft 文件"
description: "深入了解 hello 跨網域原則可在 Azure API 管理中使用。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7689d277-8abe-472a-a78c-e6d4bd43455d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: dd5ebfd65b92ebd0c1f589a2bac669a3928d40b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-cross-domain-policies"></a>API 管理跨網域原則
本主題提供下列 API 管理原則的 hello 的參考。 如需有關新增和設定原則的資訊，請參閱 [API 管理中的原則](http://go.microsoft.com/fwlink/?LinkID=398186)。  
  
##  <a name="CrossDomainPolicies"></a>跨網域原則  
  
-   [允許跨網域呼叫](api-management-cross-domain-policies.md#AllowCrossDomainCalls)-從 Adobe Flash 和 Microsoft Silverlight 的瀏覽器型用戶端，讓 hello API 存取。  
  
-   [CORS](api-management-cross-domain-policies.md#CORS) -將跨原始資源共用 (CORS) 支援 tooan 作業或 API tooallow 跨網域呼叫從瀏覽器型用戶端。  
  
-   [JSONP](api-management-cross-domain-policies.md#JSONP) -將 JSON padding (JSONP) 支援 tooan 作業，或從 JavaScript 瀏覽器為基礎的用戶端的應用程式開發介面 tooallow 跨網域呼叫。  
  
##  <a name="AllowCrossDomainCalls"></a>允許跨網域呼叫  
 使用 hello`cross-domain`原則 toomake hello 從 Adobe Flash 和 Microsoft Silverlight 的瀏覽器型用戶端可存取的 API。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in hello Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a>範例  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|cross-domain|根元素。 子元素必須符合 toohello [Adobe 跨網域原則檔案規格](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html)。|是|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入  
  
-   **原則範圍︰**全域  
  
##  <a name="CORS"></a>CORS  
 hello`cors`原則新增跨原始資源共用 (CORS) 支援 tooan 作業或 API tooallow 跨網域呼叫從瀏覽器型用戶端。  
  
 CORS 允許瀏覽器和伺服器 toointeract，並判斷 tooallow 特定的跨原始要求 （亦即 XMLHttpRequests 呼叫從網頁 tooother 網域上的 JavaScript 進行）。 這比只允許相同原始來源的要求更有彈性，也比允許所有跨原始來源的要求更安全。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<cors allow-credentials="false|true">  
    <allowed-origins>  
        <origin>origin uri</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="number of seconds">  
        <method>http verb</method>  
    </allowed-methods>  
    <allowed-headers>  
        <header>header name</header>  
    </allowed-headers>  
    <expose-headers>  
        <header>header name</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="example"></a>範例  
 此範例示範如何 toosupport 事前要求，例如含有自訂標頭或 GET 和 POST 以外的方法。 toosupport 自訂標頭和其他 HTTP 動詞命令，使用 hello`allowed-methods`和`allowed-headers`區段 hello 下列範例所示。  
  
```xml  
<cors allow-credentials="true">  
    <allowed-origins>  
        <!-- Localhost useful for development -->  
        <origin>http://localhost:8080/</origin>  
        <origin>http://example.com/</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="300">  
        <method>GET</method>  
        <method>POST</method>  
        <method>PATCH</method>  
        <method>DELETE</method>  
    </allowed-methods>  
    <allowed-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
        <header>x-zumo-version</header>  
        <header>x-zumo-auth</header>  
        <header>content-type</header>  
        <header>accept</header>  
    </allowed-headers>  
    <expose-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="elements"></a>元素  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|cors|根元素。|是|N/A|  
|allowed-origins|包含`origin`描述 hello 允許出處跨網域要求的項目。 `allowed-origins`可以包含單一`origin`項目，指定`*`tooallow 任何來源，或者一個或多個`origin`包含 URI 的項目。|是|N/A|  
|來源|hello 值可以是`*`tooallow 所有來源或指定單一來源的 URI。 hello URI 必須包含配置、 主機和連接埠。|是|如果 URI 中省略 hello 連接埠，則連接埠 80 用於 HTTP 和 HTTPS 使用連接埠 443。|  
|allowed-methods|如果允許 GET 或 POST 以外的方法，則需要此元素。 包含`method`指定 hello 支援 HTTP 指令動詞的項目。|否|如果這個區段不存在，則會支援 GET 和 POST。|  
|method|指定 HTTP 動詞命令。|至少一個`method`項目是必要的如果 hello`allowed-methods`區段已存在。|N/A|  
|allowed-headers|這個項目包含`header`元素，指定可以在 hello 要求中包含的 hello 標頭的名稱。|否|N/A|  
|expose-headers|這個項目包含`header`元素，指定可供存取 hello 用戶端 hello 標頭的名稱。|否|N/A|  
|頁首|指定標頭名稱。|至少一個`header`項目所需要的是`allowed-headers`或`expose-headers`如果 hello 區段存在。|N/A|  
  
### <a name="attributes"></a>屬性  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|allow-credentials|hello `Access-Control-Allow-Credentials` hello 預檢回應的標頭會設定 toohello 值，這個屬性，並影響中跨網域要求的用戶端 hello 能力 toosubmit 認證。|否|false|  
|preflight-result-max-age|hello `Access-Control-Max-Age` hello 預檢回應的標頭會設定 toohello 值，這個屬性，並會影響 hello 使用者代理程式的能力 toocache 事前回應。|否|0|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入  
  
-   **原則範圍︰**API、作業  
  
##  <a name="JSONP"></a>JSONP  
 hello`jsonp`原則新增 JSON 搭配填補 (JSONP) 支援 tooan 操作或從 JavaScript 瀏覽器為基礎的用戶端應用程式開發介面 tooallow 跨網域呼叫。 JSONP 是 JavaScript 程式 toorequest 資料位於不同的網域中，從伺服器中使用的方法。 JSONP 不強制執行大部分的網頁瀏覽器位置存取 tooweb 網頁必須在 hello hello 限制相同的網域。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a>範例  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 如果您呼叫 hello 方法沒有 hello 回呼參數？ cb = XXX，則會傳回單純 JSON （無函數呼叫包裝函式）。  
  
 如果您將加入 hello 回呼參數`?cb=XXX`則會傳回 JSONP 結果，包裝 hello 原始 JSON 結果周圍像 hello 回呼函式`XYZ('<json result goes here>');`  
  
### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|jsonp|根元素。|是|  
  
### <a name="attributes"></a>屬性  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|callback-parameter-name|hello 跨網域 JavaScript 函式呼叫前面加上 hello hello 函式所在位置的完整的網域名稱。|是|N/A|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸出  
  
-   **原則範圍︰**全域、產品、API、作業  
  
## <a name="next-steps"></a>後續步驟
如需有關使用原則的詳細資訊，請參閱 [API 管理中的原則](api-management-howto-policies.md)。  