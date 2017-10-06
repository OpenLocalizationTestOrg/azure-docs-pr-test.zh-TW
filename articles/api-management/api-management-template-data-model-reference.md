---
title: "aaaAzure API 管理的範本資料模型的參考 |Microsoft 文件"
description: "深入了解 hello 實體和類型表示法 hello 在 Azure API 管理開發人員入口網站範本在 hello 資料模型中使用的一般項目。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: b0ad7e15-9519-4517-bb73-32e593ed6380
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 7d049d8ecc9e597cf48ce0c820c172798bcf86de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-template-data-model-reference"></a>Azure API 管理範本資料模型參考
本主題描述 hello 實體和類型表示法 hello 在 Azure API 管理開發人員入口網站範本在 hello 資料模型中使用的一般項目。  
  
 如需有關使用範本的詳細資訊，請參閱[toocustomize hello API 管理開發人員入口網站使用範本的方式](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)。  
  
-   [API](#API)  
-   [API 摘要](#APISummary)  
-   [應用程式](#Application)  
-   [附件](#Attachment)  
-   [程式碼範例](#Sample)  
-   [Comment](#Comment)  
-   [篩選](#Filtering)  
-   [標頭](#Header)  
-   [HTTP 要求](#HTTPRequest)  
-   [HTTP 回應](#HTTPResponse)  
-   [問題](#Issue)  
-   [作業](#Operation)  
-   [作業功能表](#Menu)  
-   [作業功能表項目](#MenuItem)  
-   [分頁](#Paging)  
-   [參數](#Parameter)  
-   [產品](#Product)  
-   [提供者](#Provider)  
-   [表示法](#Representation)  
-   [訂用帳戶](#Subscription)  
-   [訂用帳戶摘要](#SubscriptionSummary)  
-   [使用者帳戶資訊](#UserAccountInfo)  
-   [使用者登入](#UseSignIn)  
-   [使用者註冊](#UserSignUp)  
  
##  <a name="API"></a>API  
 hello`API`實體具有下列屬性的 hello。  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|id|字串|資源識別碼。 可唯一識別 hello hello 目前 API 管理服務執行個體內的 API。 hello 值為 hello 格式的有效相對 URL`apis/{id}`其中`{id}`是 API 識別碼。 這個屬性是唯讀的。|  
|名稱|字串|Hello 應用程式開發介面的名稱。 不能空白。 長度上限是 100 個字元。|  
|說明|字串|Hello 應用程式開發介面的描述。 不能空白。 可包含 HTML 格式標籤。 長度上限是 1000 個字元。|  
|serviceUrl|字串|實作此 API 的 hello 後端服務的絕對 URL。|  
|路徑|字串|用來唯一識別此 API 及其所有資源路徑 hello API 管理服務執行個體內的相對 URL。 它會附加 toohello API 端點基礎 URL 指定 hello 服務執行個體建立 tooform 期間的公用 URL 此 api。|  
|protocols|數字陣列|描述哪些通訊協定 hello 上可以叫用此應用程式開發介面中的作業。 允許的值為 `1 - http` 和 `2 - https`或兩者兼具。|  
|authenticationSettings|[授權伺服器驗證設定](https://docs.microsoft.com/rest/api/apimanagement/apimanagementrest/azure-api-management-rest-api-contract-reference#AuthenticationSettings)|此 API 中所包含之驗證設定的集合。|  
|subscriptionKeyParameterNames|物件|選擇性屬性，可以使用的 toospecify 自訂查詢和/或標頭包含 hello 訂用帳戶金鑰的參數名稱。 當這個屬性存在時，它必須包含至少其中一個 hello 兩個下列屬性。<br /><br /> `{   "subscriptionKeyParameterNames":   {     "query": “customQueryParameterName",     "header": “customHeaderParameterName"   } }`|  
  
##  <a name="APISummary"></a>API 摘要  
 hello`API summary`實體具有下列屬性的 hello。  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|id|字串|資源識別碼。 可唯一識別 hello hello 目前 API 管理服務執行個體內的 API。 hello 值為 hello 格式的有效相對 URL`apis/{id}`其中`{id}`是 API 識別碼。 這個屬性是唯讀的。|  
|名稱|字串|Hello 應用程式開發介面的名稱。 不能空白。 長度上限是 100 個字元。|  
|說明|字串|Hello 應用程式開發介面的描述。 不能空白。 可包含 HTML 格式標籤。 長度上限是 1000 個字元。|  
  
##  <a name="Application"></a>應用程式  
 hello`application`實體具有下列屬性的 hello。  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|識別碼|字串|hello hello 應用程式的唯一識別項。|  
|Title|字串|hello hello 應用程式標題。|  
|說明|字串|hello hello 應用程式描述。|  
|Url|URI|hello hello 應用程式的 URI。|  
|版本|字串|Hello 應用程式的版本資訊。|  
|需求|字串|Hello 應用程式需求的描述。|  
|State|number|hello hello 應用程式的目前狀態。<br /><br /> - 0 - 已註冊<br /><br /> - 1 - 已提交<br /><br /> - 2 - 已發佈<br /><br /> - 3 - 已拒絕<br /><br /> - 4 - 已解除發佈|  
|RegistrationDate|DateTime|已註冊 hello 日期和時間 hello 應用程式。|  
|CategoryId|number|hello 類別的 hello 應用程式 （財務、 娛樂等等。）|  
|DeveloperId|字串|hello hello 開發人員提交 hello 應用程式的唯一識別項。|  
|附件|[附件](#Attachment)實體的集合。|Hello 應用程式，例如螢幕擷取畫面或圖示的任何附件。|  
|圖示|[附件](#Attachment)|hello 圖示 hello hello 應用程式。|  
  
##  <a name="Attachment"></a>附件  
 hello`attachment`實體具有下列屬性的 hello。  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|UniqueId|字串|hello hello 附件的唯一識別碼。|  
|Url|字串|hello hello 資源 URL。|  
|類型|字串|hello 類型的附件。|  
|ContentType|字串|hello hello 附件的媒體類型。|  
  
##  <a name="Sample"></a>程式碼範例  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|title|字串|hello hello 作業名稱。|  
|snippet|字串|此屬性已被取代而不應該使用。|  
|brush|字串|程式碼語法著色範本 toobe 顯示 hello 程式碼範例時使用。 允許的值為 `plain`、`php``java`、`xml``objc`、`python`、`ruby` 和 `csharp`。|  
|template|字串|此程式碼範例範本 hello 名稱。|  
|body|字串|Hello 程式碼範例的一部分 hello 程式碼片段的預留位置。|  
|method|字串|hello hello 作業的 HTTP 方法。|  
|scheme|字串|hello 通訊協定 toouse hello 作業要求。|  
|路徑|字串|hello 作業 hello 路徑。|  
|query|字串|具有已定義參數的查詢字串範例。|  
|主機|字串|hello hello API 管理服務閘道 hello 應用程式開發介面，其中包含這項作業的 URL。|  
|headers|[標頭](#Header)實體的集合。|此作業的標頭。|  
|參數|[參數](#Parameter)實體的集合。|針對這項作業所定義的參數。|  
  
##  <a name="Comment"></a>註解  
 hello`API`實體具有下列屬性的 hello。  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|識別碼|number|hello 識別碼 hello 註解。|  
|CommentText|字串|hello 主體 hello 註解。 可包含 HTML。|  
|DeveloperCompany|字串|hello hello 開發人員的公司名稱。|  
|PostedOn|DateTime|已張貼 hello 日期和時間 hello 的註解。|  
  
##  <a name="Issue"></a>問題  
 hello`issue`實體具有下列屬性的 hello。  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|識別碼|字串|hello hello 問題的唯一識別碼。|  
|ApiID|字串|回報這個問題發生的 hello API hello 識別碼。|  
|Title|字串|Hello 問題的標題。|  
|說明|字串|Hello 問題的描述。|  
|SubscriptionDeveloperName|字串|報告的 hello 問題的 hello 開發人員的名字。|  
|IssueState|字串|hello 問題 hello 目前狀態。 可能的值為已提議、已開啟、已關閉。|  
|ReportedOn|DateTime|hello 日期和時間 hello 問題報告。|  
|註解|[註解](#Comment)實體的集合。|此問題的註解。|  
|附件|[附件](api-management-template-data-model-reference.md#Attachment)實體的集合。|任何附件 toohello 發生問題。|  
|服務|[API](#API) 實體的集合。|hello Api 訂閱 tooby hello 使用者歸檔 hello 問題。|  
  
##  <a name="Filtering"></a>篩選  
 hello`filtering`實體具有下列屬性的 hello。  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|模式|字串|hello 目前的搜尋詞彙;或`null`如果沒有搜尋字詞。|  
|Placeholder|字串|hello 文字 toodisplay hello [搜尋] 方塊中的，指定沒有搜尋字詞時。|  
  
##  <a name="Header"></a>標頭  
 本章節描述 hello`parameter`表示法。  
  
|屬性|說明|類型|  
|--------------|-----------------|----------|  
|名稱|字串|參數名稱。|  
|說明|字串|參數描述。|  
|value|字串|標頭值。|  
|typeName|字串|標頭值的資料類型。|  
|options|字串|選項。|  
|必要|布林值|是否需要 hello 標頭。|  
|readOnly|布林值|Hello 標頭是否為唯讀。|  
  
##  <a name="HTTPRequest"></a>HTTP 要求  
 本章節描述 hello`request`表示法。  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|說明|字串|作業要求描述。|  
|標頭|[標頭](#Header)實體的陣列。|要求標頭。|  
|參數|[參數](#Parameter)的陣列|作業要求參數的集合。|  
|representations|[表示法](#Representation)的陣列|作業要求表示法的集合。|  
  
##  <a name="HTTPResponse"></a>HTTP 回應  
 本章節描述 hello`response`表示法。  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|StatusCode|正整數|作業回應狀態碼。|  
|說明|字串|作業回應描述。|  
|representations|[表示法](#Representation)的陣列|作業回應表示法的集合。|  
  
##  <a name="Operation"></a>作業  
 hello`operation`實體具有下列屬性的 hello。  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|id|字串|資源識別碼。 可唯一識別 hello hello 目前 API 管理服務執行個體內的作業。 hello 值為 hello 格式的有效相對 URL`apis/{aid}/operations/{id}`其中`{aid}`是 API 識別碼和`{id}`是操作識別碼。 這個屬性是唯讀的。|  
|名稱|字串|Hello 作業的名稱。 不能空白。 長度上限是 100 個字元。|  
|說明|字串|Hello 作業的描述。 不能空白。 可包含 HTML 格式標籤。 長度上限是 1000 個字元。|  
|scheme|字串|描述哪些通訊協定 hello 上可以叫用此應用程式開發介面中的作業。 允許的值為 `http`、`https` 或 `http` 和 `https` 兼具。|  
|uriTemplate|字串|用來識別這項作業的 hello 目標資源的相對 URL 範本。 可包含參數。 範例： `customers/{cid}/orders/{oid}/?date={date}`|  
|主機|字串|裝載 hello API hello API 管理閘道 URL。|  
|httpMethod|字串|作業 HTTP 方法。|  
|要求|[HTTP 要求](#HTTPRequest)|包含要求詳細資料的實體。|  
|responses|[HTTP 回應](#HTTPResponse)的陣列|作業 [HTTP 回應](#HTTPResponse)實體的陣列。|  
  
##  <a name="Menu"></a>作業功能表  
 hello`operation menu`實體具有下列屬性的 hello。  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|ApiId|字串|hello 識別碼 hello 目前的 API。|  
|CurrentOperationId|字串|hello hello 目前的作業識別碼。|  
|動作|字串|hello 功能表類型。|  
|MenuItems|[作業功能表項目](#MenuItem)實體的集合。|hello hello 目前的 API 作業。|  
  
##  <a name="MenuItem"></a>作業功能表項目  
 hello`operation menu item`實體具有下列屬性的 hello。  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|識別碼|字串|hello hello 作業識別碼。|  
|Title|字串|hello hello 作業描述。|  
|HttpMethod|字串|hello hello 作業的 Http 方法。|  
  
##  <a name="Paging"></a>分頁  
 hello`paging`實體具有下列屬性的 hello。  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|Page|number|hello 目前頁碼。|  
|PageSize|number|在單一頁面上顯示 hello 的最大結果 toobe。|  
|TotalItemCount|number|hello 顯示的項目數目。|  
|ShowAll|布林值|是否所有 toosho 都結果在單一頁面上。|  
|PageCount|number|hello 結果的頁面數目。|  
  
##  <a name="Parameter"></a>參數  
 本章節描述 hello`parameter`表示法。  
  
|屬性|說明|類型|  
|--------------|-----------------|----------|  
|名稱|字串|參數名稱。|  
|說明|字串|參數描述。|  
|value|字串|參數值。|  
|options|字串陣列|針對查詢參數值所定義的值。|  
|必要|布林值|指定參數是否為必要。|  
|kind|number|此參數為路徑參數 (1) 還是查詢字串參數 (2)。|  
|typeName|字串|參數類型。|  
  
##  <a name="Product"></a>產品  
 hello`product`實體具有下列屬性的 hello。  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|識別碼|字串|資源識別碼。 可唯一識別 hello hello 目前 API 管理服務執行個體內的產品。 hello 值為 hello 格式的有效相對 URL`products/{pid}`其中`{pid}`是產品識別碼。 這個屬性是唯讀的。|  
|課程名稱|字串|Hello 產品名稱。 不能空白。 長度上限是 100 個字元。|  
|說明|字串|Hello 產品的描述。 不能空白。 可包含 HTML 格式標籤。 長度上限是 1000 個字元。|  
|詞彙|字串|產品使用規定。 嘗試 toosubscribe toohello 產品的開發人員會提供，而且需要 tooaccept 這些授權條款，才能完成 hello 訂閱程序。|  
|ProductState|number|指定是否 hello 產品發佈與否。 Hello 開發人員入口網站上的開發人員可探索的已發行的產品。 未發佈的產品是可見的唯一 tooadministrators。<br /><br /> hello 產品狀態的允許值為：<br /><br /> - `0 - Not Published`<br /><br /> - `1 - Published`<br /><br /> - `2 - Deleted`|  
|AllowMultipleSubscriptions|布林值|指定使用者是否可以有多個訂用帳戶 toothis 產品 hello 在相同的時間。|  
|MultipleSubscriptionsCount|number|hello hello 目前使用者所訂用帳戶 toothis 產品數目。|  
  
##  <a name="Provider"></a>提供者  
 hello`provider`實體具有下列屬性的 hello。  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|屬性|字串字典|此驗證提供者的屬性。|  
|AuthenticationType|字串|hello 提供者類型。 (Azure Active Directory、Facebook 登入、Google 帳戶、Microsoft 帳戶、Twitter)。|  
|Caption|字串|Hello 提供者的顯示名稱。|  
  
##  <a name="Representation"></a>表示法  
 本區段描述 `representation`。  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|contentType|字串|指定此表示法的已註冊或自訂內容類型，例如 `application/xml`。|  
|sample|字串|Hello 表示法範例。|  
  
##  <a name="Subscription"></a>訂用帳戶  
 hello`subscription`實體具有下列屬性的 hello。  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|識別碼|字串|資源識別碼。 可唯一識別目前 API 管理服務執行個體 hello hello 訂用帳戶。 hello 值為 hello 格式的有效相對 URL`subscriptions/{sid}`其中`{sid}`是訂用帳戶識別碼。 這個屬性是唯讀的。|  
|ProductId|字串|hello 產品資源識別碼 hello 訂閱產品。 hello 值為 hello 格式的有效相對 URL`products/{pid}`其中`{pid}`是產品識別碼。|  
|ProductTitle|字串|Hello 產品名稱。 不能空白。 長度上限是 100 個字元。|  
|ProductDescription|字串|Hello 產品的描述。 不能空白。 可包含 HTML 格式標籤。 長度上限是 1000 個字元。|  
|ProductDetailsUrl|字串|相對的 URL toohello 產品詳細資料。|  
|state|字串|hello hello 訂用帳戶狀態。 可能的狀態為：<br /><br /> - `0 - suspended`– hello 訂用帳戶遭到封鎖，且 hello 訂閱者無法呼叫 hello 產品的任何應用程式開發介面。<br /><br /> - `1 - active`– hello 訂閱在作用中。<br /><br /> - `2 - expired`– hello 訂用帳戶已達到其到期日並且已停用。<br /><br /> - `3 - submitted`– hello 訂用帳戶要求 hello 開發人員已發出但尚未核准或拒絕。<br /><br /> - `4 - rejected`– 系統管理員已拒絕 hello 訂用帳戶要求。<br /><br /> - `5 - cancelled`– hello 開發人員或管理員已取消 hello 訂用帳戶。|  
|DisplayName|字串|Hello 訂用帳戶的顯示名稱。|  
|CreatedDate|dateTime|建立 hello 日期 hello 訂用帳戶，採用 ISO 8601 格式： `2014-06-24T16:25:00Z`。|  
|CanBeCancelled|布林值|Hello 目前使用者是否可以取消 hello 訂用帳戶。|  
|IsAwaitingApproval|布林值|是否 hello 訂用帳戶正在等待核准。|  
|StartDate|dateTime|hello 的開始日期 hello 訂用帳戶，採用 ISO 8601 格式： `2014-06-24T16:25:00Z`。|  
|ExpirationDate|dateTime|hello hello 訂用帳戶，採用 ISO 8601 格式的到期日： `2014-06-24T16:25:00Z`。|  
|NotificationDate|dateTime|hello 通知日期 hello 訂用帳戶，採用 ISO 8601 格式： `2014-06-24T16:25:00Z`。|  
|primaryKey|字串|hello 主要訂閱金鑰。 長度上限是 256 個字元。|  
|secondaryKey|字串|hello 次要訂閱金鑰。 長度上限是 256 個字元。|  
|CanBeRenewed|布林值|Hello 目前使用者是否可以更新 hello 訂用帳戶。|  
|HasExpired|布林值|是否 hello 訂閱已過期。|  
|IsRejected|布林值|是否 hello 訂用帳戶要求遭到拒絕。|  
|CancelUrl|字串|hello 相對 Url toocancel hello 訂用帳戶。|  
|RenewUrl|字串|hello 相對 Url toorenew hello 訂用帳戶。|  
  
##  <a name="SubscriptionSummary"></a>訂用帳戶摘要  
 hello`subscription summary`實體具有下列屬性的 hello。  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|識別碼|字串|資源識別碼。 可唯一識別目前 API 管理服務執行個體 hello hello 訂用帳戶。 hello 值為 hello 格式的有效相對 URL`subscriptions/{sid}`其中`{sid}`是訂用帳戶識別碼。 這個屬性是唯讀的。|  
|DisplayName|字串|hello 顯示 hello 訂用帳戶名稱|  
  
##  <a name="UserAccountInfo"></a>使用者帳戶資訊  
 hello`user account info`實體具有下列屬性的 hello。  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|名字|字串|名字。 不能空白。 長度上限是 100 個字元。|  
|姓氏|字串|姓氏。 不能空白。 長度上限是 100 個字元。|  
|電子郵件|字串|電子郵件地址。 不得為空白，而且必須是唯一 hello 服務執行個體內。 長度上限是 254 個字元。|  
|密碼|字串|使用者帳戶密碼。|  
|NameIdentifier|字串|帳戶識別碼 hello 相同 hello 使用者電子郵件。|  
|ProviderName|字串|驗證提供者名稱。|  
|IsBasicAccount|布林值|如果此帳戶已註冊使用電子郵件和密碼;，則為 true。如果使用提供者註冊 hello 帳戶，false。|  
  
##  <a name="UseSignIn"></a>使用者登入  
 hello`user sign in`實體具有下列屬性的 hello。  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|電子郵件|字串|電子郵件地址。 不得為空白，而且必須是唯一 hello 服務執行個體內。 長度上限是 254 個字元。|  
|密碼|字串|使用者帳戶密碼。|  
|ReturnUrl|字串|hello hello 使用者所按的登入位置的 hello 網頁 URL。|  
|RememberMe|布林值|是否 toosave hello 目前使用者的資訊。|  
|RegistrationEnabled|布林值|是否啟用註冊。|  
|DelegationEnabled|布林值|是否啟用委派的登入。|  
|DelegationUrl|字串|hello 委派的登入 url，如果已啟用。|  
|SsoSignUpUrl|字串|hello 單一登入 URL hello 使用者，如果有的話。|  
|AuxServiceUrl|字串|如果 hello 目前使用者是系統管理員，這是 hello Azure 傳統入口網站中的連結 toohello 服務執行個體。|  
|提供者|[提供者](#Provider)實體的集合|hello 這位使用者的驗證提供者。|  
|UserRegistrationTerms|字串|使用者必須同意 toobefore 簽章的條款。|  
|UserRegistrationTermsEnabled|布林值|是否啟用條款。|  
  
##  <a name="UserSignUp"></a>使用者註冊  
 hello`user sign up`實體具有下列屬性的 hello。  
  
|屬性|類型|說明|  
|--------------|----------|-----------------|  
|PasswordConfirm|布林值|使用 hello 值[註冊](api-management-page-controls.md#sign-up)註冊控制項。|  
|密碼|字串|使用者帳戶密碼。|  
|PasswordVerdictLevel|number|使用 hello 值[註冊](api-management-page-controls.md#sign-up)註冊控制項。|  
|UserRegistrationTerms|字串|使用者必須同意 toobefore 簽章的條款。|  
|UserRegistrationTermsOptions|number|使用 hello 值[註冊](api-management-page-controls.md#sign-up)註冊控制項。|  
|ConsentAccepted|布林值|使用 hello 值[註冊](api-management-page-controls.md#sign-up)註冊控制項。|  
|電子郵件|字串|電子郵件地址。 不得為空白，而且必須是唯一 hello 服務執行個體內。 長度上限是 254 個字元。|  
|名字|字串|名字。 不能空白。 長度上限是 100 個字元。|  
|姓氏|字串|姓氏。 不能空白。 長度上限是 100 個字元。|  
|UserData|字串|使用 hello 值[註冊](api-management-page-controls.md#sign-up)控制項。|  
|NameIdentifier|字串|使用 hello 值[註冊](api-management-page-controls.md#sign-up)註冊控制項。|  
|ProviderName|字串|驗證提供者名稱。|

## <a name="next-steps"></a>後續步驟
如需有關使用範本的詳細資訊，請參閱[toocustomize hello API 管理開發人員入口網站使用範本的方式](api-management-developer-portal-templates.md)。
