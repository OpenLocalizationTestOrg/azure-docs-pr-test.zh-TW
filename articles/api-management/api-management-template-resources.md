---
title: "aaaAzure API 管理的範本資源 |Microsoft 文件"
description: "深入了解 hello 適用於在 Azure API 管理開發人員入口網站範本中所使用的資源類型。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 51a1b4c6-a9fd-4524-9e0e-03a9800c3e94
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2221e3852986d485d13817b483e473dfe451d3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-template-resources"></a>Azure API 管理中的範本資源
Azure API 管理提供下列類型的 hello 開發人員入口網站範本中所使用的資源的 hello。  
  
-   [字串資源](#strings)  
  
-   [圖像資源](#glyphs)  
  
##  <a name="strings"></a> 字串資源  
 API 管理提供用於 hello 開發人員入口網站中的一組完整的字串資源。 這些資源已當地語系化為所有支援的 API 管理的 hello 語言。 hello 組預設的範本會使用這些資源，如頁首、 標籤與 hello 開發人員入口網站中所顯示的任何常數字串。 toouse 字串中的資源範本，提供 hello 資源字串前置詞後面接著 hello 字串名稱，如 hello 下列範例所示。  
  
```  
{% localized "Prefix|Name" %}  
  
```  
  
 hello 下列範例取自 hello 產品清單範本，並顯示**產品**hello 頁面頂端的 hello。  
  
```  
<h2>{% localized "ProductsStrings|PageTitleProducts" %}</h2>  
  
```  
  
 請參閱 toohello 遵循 hello 字串資源可供您的開發人員入口網站範本中所使用的資料表。 使用該資料表中的 hello 字串資源的 hello 前置詞 hello 資料表名稱。  
  
-   [ApisStrings](#ApisStrings)  
  
-   [ApplicationListStrings](#ApplicationListStrings)  
  
-   [AppDetailsStrings](#AppDetailsStrings)  
  
-   [AppStrings](#AppStrings)  
  
-   [CommonResources](#CommonResources)  
  
-   [CommonStrings](#CommonStrings)  
  
-   [Documentation](#Documentation)  
  
-   [ErrorPageStrings](#ErrorPageStrings)  
  
-   [IssuesStrings](#IssuesStrings)  
  
-   [NotFoundStrings](#NotFoundStrings)  
  
-   [ProductDetailsStrings](#ProductDetailsStrings)  
  
-   [ProductsStrings](#ProductsStrings)  
  
-   [ProviderInfoStrings](#ProviderInfoStrings)  
  
-   [SigninResources](#SigninResources)  
  
-   [SigninStrings](#SigninStrings)  
  
-   [SignupStrings](#SignupStrings)  
  
-   [SubscriptionListStrings](#SubscriptionListStrings)  
  
-   [SubscriptionStrings](#SubscriptionStrings)  
  
-   [UpdateProfileStrings](#UpdateProfileStrings)  
  
-   [UserProfile](#UserProfile)  
  
###  <a name="ApisStrings"></a> ApisStrings  
  
|名稱|文字|  
|----------|----------|  
|PageTitleApis|API|  
  
###  <a name="AppDetailsStrings"></a> AppDetailsStrings  
  
|名稱|文字|  
|----------|----------|  
|WebApplicationsDetailsTitle|應用程式預覽|  
|WebApplicationsRequirementsHeader|需求|  
|WebApplicationsScreenshotAlt|螢幕擷取畫面|  
|WebApplicationsScreenshotsHeader|螢幕擷取畫面|  
  
###  <a name="ApplicationListStrings"></a> ApplicationListStrings  
  
|名稱|文字|  
|----------|----------|  
|WebDevelopersAppDeleteConfirmation|確定您想 tooremove 應用程式？|  
|WebDevelopersAppNotPublished|未發佈|  
|WebDevelopersAppNotSubminted|未提交|  
|WebDevelopersAppTableCategoryHeader|類別|  
|WebDevelopersAppTableNameHeader|名稱|  
|WebDevelopersAppTableStateHeader|狀況|  
|WebDevelopersEditLink|編輯|  
|WebDevelopersRegisterAppLink|註冊應用程式|  
|WebDevelopersRemoveLink|移除|  
|WebDevelopersSubmitLink|提交|  
|WebDevelopersYourApplicationsHeader|您的應用程式|  
  
###  <a name="AppStrings"></a> AppStrings  
  
|名稱|文字|  
|----------|----------|  
|WebApplicationsHeader|應用程式|  
  
###  <a name="CommonResources"></a> CommonResources  
  
|名稱|文字|  
|----------|----------|  
|NoItemsToDisplay|找不到結果。|  
|GeneralExceptionMessage|某些項目不正確。 可能是暫時性的問題或有錯誤。 請再試一次。|  
|GeneralJsonExceptionMessage|某些項目不正確。 可能是暫時性的問題或有錯誤。 請重新載入 hello 頁面並再試一次。|  
|ConfirmationMessageUnsavedChanges|有一些變更未儲存。 確定您想 toocancel 並捨棄 hello 變更？|  
|AzureActiveDirectory|Azure Active Directory|  
|HttpLargeRequestMessage|HTTP 要求本文太大。|  
  
###  <a name="CommonStrings"></a> CommonStrings  
  
|名稱|文字|  
|----------|----------|  
|ButtonLabelCancel|取消|  
|ButtonLabelSave|儲存|  
|GeneralExceptionMessage|某些項目不正確。 可能是暫時性的問題或有錯誤。 請再試一次。|  
|NoItemsToDisplay|沒有任何項目 toodisplay。|  
|PagerButtonLabelFirst|第一頁|  
|PagerButtonLabelLast|最後一頁|  
|PagerButtonLabelNext|下一頁|  
|PagerButtonLabelPrevious|上一頁|  
|PagerLabelPageNOfM|{0} 頁/共 {1\} 頁|  
|PasswordTooShort|hello 密碼是太短|  
|EmailAsPassword|請勿使用您的電子郵件做為您的密碼|  
|PasswordSameAsUserName|密碼不可包含您的使用者名稱|  
|PasswordTwoCharacterClasses|使用不同的字元類別|  
|PasswordTooManyRepetitions|太多重複|  
|PasswordSequenceFound|您的密碼包含連續數字|  
|PagerLabelPageSize|頁面大小|  
|CurtainLabelLoading|正在載入...|  
|TablePlaceholderNothingToDisplay|針對選取的 hello 段時間和範圍沒有任何資料|  
|ButtonLabelClose|關閉|  
  
###  <a name="Documentation"></a> Documentation  
  
|名稱|文字|  
|----------|----------|  
|WebDocumentationInvalidHeaderErrorMessage|無效的標頭 '{0}'|  
|WebDocumentationInvalidRequestErrorMessage|無效的要求 URL|  
|TextboxLabelAccessToken|存取權杖 *|  
|DropdownOptionPrimaryKeyFormat|主要-{0}|  
|DropdownOptionSecondaryKeyFormat|次要-{0}|  
|WebDocumentationSubscriptionKeyText|您的訂用帳戶金鑰|  
|WebDocumentationTemplatesAddHeaders|新增必要的 HTTP 標頭|  
|WebDocumentationTemplatesBasicAuthSample|基本授權範例|  
|WebDocumentationTemplatesCurlForBasicAuth|基本授權請使用：--user {username}:{password}|  
|WebDocumentationTemplatesCurlValuesForPath|指定路徑參數的值 (顯示為 {...})、您的訂用帳戶金鑰和查詢參數的值|  
|WebDocumentationTemplatesDeveloperKey|指定您的訂用帳戶金鑰|  
|WebDocumentationTemplatesJavaApache|這個範例會使用 hello Apache HTTP 用戶端從 HTTP 元件 (http://hc.apache.org/httpcomponents-client-ga/)|  
|WebDocumentationTemplatesOptionalParams|視需要指定選用參數的值|  
|WebDocumentationTemplatesPhpPackage|這個範例會使用 hello HTTP_Request2 封裝。 (如需詳細資訊︰ http://pear.php.net/package/HTTP_Request2)|  
|WebDocumentationTemplatesPythonValuesForPath|視需要指定路徑參數的值 (顯示為 {...}) 和要求本文|  
|WebDocumentationTemplatesRequestBody|指定要求本文|  
|WebDocumentationTemplatesRequiredParams|指定 hello 下列必要的參數的值|  
|WebDocumentationTemplatesValuesForPath|指定路徑參數的值 (顯示為 {...})|  
|OAuth2AuthorizationEndpointDescription|hello 授權端點是使用的 toointeract 與 hello 資源擁有者，並取得授權授與。|  
|OAuth2AuthorizationEndpointName|授權端點|  
|OAuth2TokenEndpointDescription|會使用 hello 語彙基元端點 hello 用戶端 tooobtain 呈現其授權的存取權杖授與，或重新整理權杖。|  
|OAuth2TokenEndpointName|權杖端點|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_Description|< p\> hello 用戶端會起始 hello 流程，以控制程式 hello 資源擁有者的使用者代理程式 toohello 授權端點。  hello 用戶端包含其用戶端識別碼、 要求的範圍，區域狀態中，而重新導向 URI toowhich hello 授權伺服器會傳送 hello 使用者代理程式回一旦授與 （或拒絕存取）。     </p\> < p\> hello 授權伺服器驗證 （透過 hello 使用者代理程式） 的 hello 資源擁有者，並建立 hello 資源擁有者是否會授與或拒絕用戶端 hello 存取要求。     </p\> < p\>假設 hello 資源擁有者授與存取權，hello 授權伺服器 hello 使用者代理程式後 toohello 用戶端重新導向使用 hello 重新導向 URI 提供舊版 （hello 要求或在用戶端t 註冊）。  hello 重新導向 URI 包括授權碼和稍早 hello 用戶端所提供的任何本機狀態。     </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_ErrorDescription|< p\>若 hello 使用者拒絕的 hello 存取要求，如果 hello 要求無效，就會使用下列參數上 toohello 重新導向新增 hello 通知 hello 用戶端： </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_Name|授權要求|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_RequestDescription|< p\> hello 用戶端應用程式必須傳送嗨使用者 toohello 授權端點順序 tooinitiate hello OAuth 程序中。          Hello 授權端點，在 hello 使用者驗證，然後授與或拒絕存取 toohello 應用程式。     </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_AuthorizationRequest_ResponseDescription|< p\>假設 hello 資源擁有者授與存取權，授權伺服器 hello 使用者代理程式後 toohello 用戶端重新導向使用 hello 重新導向 URI 提供舊版 （hello 要求中或在用戶端註冊時）。  hello 重新導向 URI 包括授權碼和稍早 hello 用戶端所提供的任何本機狀態。 </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_Description|< p\> hello 用戶端要求存取權杖來自 hello 授權伺服器 ' s 語彙基元端點包括收到 hello 上一個步驟中的 hello 授權碼。  Hello 要求時，會向驗證 hello 用戶端 hello 授權伺服器。  hello 用戶端包含 hello 重新導向 URI 用 tooobtain hello 授權程式碼進行驗證。 </p\> < p\> hello 授權伺服器會 hello 用戶端驗證，驗證 hello 授權程式碼，並確保該 hello 重新導向 URI 會接收符合 hello URI 使用的 tooredirect hello 用戶端在步驟 (C)。  如果有效，hello 授權伺服器會回應回與存取權杖，並選擇性地重新整理權杖。 </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_ErrorDescription|< p\> hello 要求用戶端驗證失敗，或不正確，如果 hello 授權伺服器 （除非另有指定），而且出現 HTTP 400 （不正確的要求） 狀態碼回應，並包含下列參數與 hello 回應 hello。 </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_RequestDescription|< p\> hello 用戶端會要求 toohello 權杖端點提出傳送 hello 遵循使用 hello"應用程式/x-www-表單-urlencoded 」 格式的字元編碼方式 utf-8 hello HTTP 要求實體主體中的參數。 </p\>|  
|OAuth2Flow_AuthorizationCodeGrant_Step_TokenRequest_ResponseDescription|< p\> hello 授權伺服器發出存取權杖和選擇性的重新整理權杖，並建構加入下列參數 toohello 實體本文的 hello HTTP 回應 200 (OK) 狀態碼的 hello hello 回應。 </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_Description|< p\> hello 用戶端驗證與 hello 授權伺服器，並從 hello 權杖端點要求存取權杖。 </p\> < p\> hello 授權伺服器會 hello 用戶端驗證，如果有效，就會發出存取權杖。 </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_ErrorDescription|< p\> hello 授權伺服器 hello 要求失敗的用戶端驗證或無效 （除非另有指定），而且出現 HTTP 400 （不正確的要求） 狀態碼回應，並包含下列參數與 hello 回應 hello。 </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_RequestDescription|< p\> hello 用戶端會要求 toohello 權杖端點提出加入下列參數使用 hello"應用程式/x-www-表單-urlencoded 」 格式的字元編碼方式 utf-8 hello HTTP 要求實體主體中的 hello。 </p\>|  
|OAuth2Flow_ClientCredentialsGrant_Step_TokenRequest_ResponseDescription|< p\>如果 hello 存取權杖要求是有效且已獲授權，hello 授權伺服器發出存取權杖和選擇性的重新整理權杖，以及建構加入下列參數 toohello 實體本文的 hello HTTP hello hello 回應200 (OK) 狀態碼回應。 </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_Description|< p\> hello 用戶端會起始 hello 流程，以控制程式 hello 資源擁有者 ' s 使用者代理程式 toohello 授權端點。  hello 用戶端包含其用戶端識別碼、 要求的範圍，區域狀態中，而重新導向 URI toowhich hello 授權伺服器會傳送 hello 使用者代理程式回一旦授與 （或拒絕存取）。 </p\> < p\> hello 授權伺服器驗證 （透過 hello 使用者代理程式） 的 hello 資源擁有者，並建立 hello 資源擁有者是否會授與或拒絕 hello 用戶端 ' s 存取要求。 </p\> < p\>假設 hello 資源擁有者授與存取權，hello 授權伺服器 hello 使用者代理程式後 toohello 用戶端重新導向使用 hello 重新導向 URI 之前所提供。  hello 重新導向 URI 會納入 hello URI 片段中的 hello 存取權杖。 </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_ErrorDescription|< p\>如果 hello 資源擁有者拒絕 hello 存取要求，或如果 hello 要求因遺失或無效的重新導向 URI 以外的原因而失敗，hello 授權伺服器會通知加入下列參數 toohello fragme hello hello 用戶端nt 元件 hello 重新導向 URI 使用 hello"應用程式/x-www-表單-urlencoded 」 格式。 </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_RequestDescription|< p\> hello 用戶端應用程式必須傳送嗨使用者 toohello 授權端點順序 tooinitiate hello OAuth 程序中。      Hello 授權端點，在 hello 使用者驗證，然後授與或拒絕存取 toohello 應用程式。 </p\>|  
|OAuth2Flow_ImplicitGrant_Step_AuthorizationRequest_ResponseDescription|< p\> hello 資源擁有者授與 hello 存取要求時，如果 hello 授權伺服器發出存取權杖，並將其加入下列參數 toohello 片段元件 hello 重新導向 URI 的 hello 傳遞 toohello 用戶端使用 hello"_FITTEDpplication/x-www-表單-urlencoded 」 格式。 </p\>|  
|OAuth2Flow_ObtainAuthorization_AuthorizationCodeGrant_Description|授權碼流程最適合用於用戶端能夠維護 hello 機密性其認證 （例如，網頁伺服器應用程式實作使用 PHP、 Java、 Python、 Ruby、 ASP.NET 等。）。|  
|OAuth2Flow_ObtainAuthorization_AuthorizationCodeGrant_Name|授權碼授與|  
|OAuth2Flow_ObtainAuthorization_ClientCredentialsGrant_Description|用戶端認證流程很適合在 hello 用戶端 （您的應用程式），要求存取受其控制的 toohello 受保護資源的情況下使用。 hello 用戶端會被視為資源擁有者，因此不不需要任何使用者互動。|  
|OAuth2Flow_ObtainAuthorization_ClientCredentialsGrant_Name|用戶端認證授與|  
|OAuth2Flow_ObtainAuthorization_ImplicitGrant_Description|隱含流程最適合用於無法進行維護的認證已知 toooperate 特定重新導向 URI 的 hello 機密性的用戶端。 這些用戶端通常是在使用指令碼語言 (如 JavaScript ) 的瀏覽器中實作。|  
|OAuth2Flow_ObtainAuthorization_ImplicitGrant_Name|隱含授與|  
|OAuth2Flow_ObtainAuthorization_ResourceOwnerPasswordCredentialsGrant_Description|資源擁有者密碼認證流程很適合在 hello 資源擁有者之信任關係與 hello 用戶端 （您的應用程式），例如 hello 裝置作業系統或高特殊權限的應用程式的情況下使用。 此流程可適用於用戶端能夠取得 hello 資源擁有者的認證 （使用者名稱和密碼，通常會使用互動式的形式）。|  
|OAuth2Flow_ObtainAuthorization_ResourceOwnerPasswordCredentialsGrant_Name|資源擁有者密碼認證授與|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_Description|< p\> hello 資源擁有者 hello 用戶端提供其使用者名稱和密碼。 </p\> < p\> hello 用戶端要求存取權杖來自 hello 授權伺服器 ' s 藉由從 hello 資源擁有者收到 hello 認證的權杖端點。  Hello 要求時，會向驗證 hello 用戶端 hello 授權伺服器。 </p\> < p\> hello 授權伺服器會驗證 hello 用戶端會驗證 hello 資源擁有者的認證，和如果有效，就會發出存取權杖。 </p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_ErrorDescription|< p\> hello 授權伺服器 hello 要求失敗的用戶端驗證或無效 （除非另有指定），而且出現 HTTP 400 （不正確的要求） 狀態碼回應，並包含下列參數與 hello 回應 hello。 </p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_RequestDescription|< p\> hello 用戶端會要求 toohello 權杖端點提出加入下列參數使用 hello"應用程式/x-www-表單-urlencoded 」 格式的字元編碼方式 utf-8 hello HTTP 要求實體主體中的 hello。 </p\>|  
|OAuth2Flow_ResourceOwnerPasswordCredentialsGrant_Step_TokenRequest_ResponseDescription|< p\>如果 hello 存取權杖要求是有效且已獲授權，hello 授權伺服器發出存取權杖和選擇性的重新整理權杖，以及建構 hello 回應 hello 遵循參數 toohello 實體本文的 hello HTTP respo 加nse 200 (OK) 狀態碼。 </p\>|  
|OAuth2Step_AccessTokenRequest_Name|存取權杖要求|  
|OAuth2Step_AuthorizationRequest_Name|授權要求|  
|OAuth2AccessToken_AuthorizationCodeGrant_TokenResponse|「必要」。 hello 授權伺服器所發出的 hello 存取權杖。|  
|OAuth2AccessToken_ClientCredentialsGrant_TokenResponse|「必要」。 hello 授權伺服器所發出的 hello 存取權杖。|  
|OAuth2AccessToken_ImplicitGrant_AuthorizationResponse|「必要」。 hello 授權伺服器所發出的 hello 存取權杖。|  
|OAuth2AccessToken_ResourceOwnerPasswordCredentialsGrant_TokenResponse|「必要」。 hello 授權伺服器所發出的 hello 存取權杖。|  
|OAuth2ClientId_AuthorizationCodeGrant_AuthorizationRequest|「必要」。 用戶端識別碼。|  
|OAuth2ClientId_AuthorizationCodeGrant_TokenRequest|如果 hello 用戶端不會驗證與 hello 授權伺服器所需。|  
|OAuth2ClientId_ImplicitGrant_AuthorizationRequest|「必要」。 hello 用戶端識別碼。|  
|OAuth2Code_AuthorizationCodeGrant_AuthorizationResponse|「必要」。 hello hello 授權伺服器所產生的授權碼。|  
|OAuth2Code_AuthorizationCodeGrant_TokenRequest|「必要」。 收到 hello 授權伺服器 hello 授權碼。|  
|OAuth2ErrorDescription_AuthorizationCodeGrant_AuthorizationErrorResponse|「選用」。 人類可閱讀的 ASCII 文字，提供其他資訊。|  
|OAuth2ErrorDescription_AuthorizationCodeGrant_TokenErrorResponse|「選用」。 人類可閱讀的 ASCII 文字，提供其他資訊。|  
|OAuth2ErrorDescription_ClientCredentialsGrant_TokenErrorResponse|「選用」。 人類可閱讀的 ASCII 文字，提供其他資訊。|  
|OAuth2ErrorDescription_ImplicitGrant_AuthorizationErrorResponse|「選用」。 人類可閱讀的 ASCII 文字，提供其他資訊。|  
|OAuth2ErrorDescription_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|「選用」。 人類可閱讀的 ASCII 文字，提供其他資訊。|  
|OAuth2ErrorUri_AuthorizationCodeGrant_AuthorizationErrorResponse|「選用」。 Hello 錯誤的資訊識別人類看得懂的網頁 URI。|  
|OAuth2ErrorUri_AuthorizationCodeGrant_TokenErrorResponse|「選用」。 Hello 錯誤的資訊識別人類看得懂的網頁 URI。|  
|OAuth2ErrorUri_ClientCredentialsGrant_TokenErrorResponse|「選用」。 Hello 錯誤的資訊識別人類看得懂的網頁 URI。|  
|OAuth2ErrorUri_ImplicitGrant_AuthorizationErrorResponse|「選用」。 Hello 錯誤的資訊識別人類看得懂的網頁 URI。|  
|OAuth2ErrorUri_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|「選用」。 Hello 錯誤的資訊識別人類看得懂的網頁 URI。|  
|OAuth2Error_AuthorizationCodeGrant_AuthorizationErrorResponse|「必要」。 單一的 ASCII 錯誤程式碼，從下列 hello: invalid_request，unauthorized_client，access_denied，unsupported_response_type，invalid_scope，server_error，temporarily_unavailable。|  
|OAuth2Error_AuthorizationCodeGrant_TokenErrorResponse|「必要」。 單一的 ASCII 錯誤程式碼，從下列 hello: invalid_request，invalid_client，invalid_grant，unauthorized_client，unsupported_grant_type，invalid_scope。|  
|OAuth2Error_ClientCredentialsGrant_TokenErrorResponse|「必要」。 單一的 ASCII 錯誤程式碼，從下列 hello: invalid_request，invalid_client，invalid_grant，unauthorized_client，unsupported_grant_type，invalid_scope。|  
|OAuth2Error_ImplicitGrant_AuthorizationErrorResponse|「必要」。 單一的 ASCII 錯誤程式碼，從下列 hello: invalid_request，unauthorized_client，access_denied，unsupported_response_type，invalid_scope，server_error，temporarily_unavailable。|  
|OAuth2Error_ResourceOwnerPasswordCredentialsGrant_TokenErrorResponse|「必要」。 單一的 ASCII 錯誤程式碼，從下列 hello: invalid_request，invalid_client，invalid_grant，unauthorized_client，unsupported_grant_type，invalid_scope。|  
|OAuth2ExpiresIn_AuthorizationCodeGrant_TokenResponse|「建議使用」。 以秒為單位的 hello 存取權杖的 hello 存留期。|  
|OAuth2ExpiresIn_ClientCredentialsGrant_TokenResponse|「建議使用」。 以秒為單位的 hello 存取權杖的 hello 存留期。|  
|OAuth2ExpiresIn_ImplicitGrant_AuthorizationResponse|「建議使用」。 以秒為單位的 hello 存取權杖的 hello 存留期。|  
|OAuth2ExpiresIn_ResourceOwnerPasswordCredentialsGrant_TokenResponse|「建議使用」。 以秒為單位的 hello 存取權杖的 hello 存留期。|  
|OAuth2GrantType_AuthorizationCodeGrant_TokenRequest|「必要」。 值必須設定太"authorization_code"。|  
|OAuth2GrantType_ClientCredentialsGrant_TokenRequest|「必要」。 值必須設定太"client_credentials"。|  
|OAuth2GrantType_ResourceOwnerPasswordCredentialsGrant_TokenRequest|「必要」。 值必須設定得 「 密碼 」。|  
|OAuth2Password_ResourceOwnerPasswordCredentialsGrant_TokenRequest|「必要」。 hello 資源擁有者密碼。|  
|OAuth2RedirectUri_AuthorizationCodeGrant_AuthorizationRequest|「選用」。 hello 重新導向端點的 URI 必須是絕對 URI。|  
|OAuth2RedirectUri_AuthorizationCodeGrant_TokenRequest|當 hello"redirect_uri"參數已包含在 hello 授權要求，並且其值必須相同才需要。|  
|OAuth2RedirectUri_ImplicitGrant_AuthorizationRequest|「選用」。 hello 重新導向端點的 URI 必須是絕對 URI。|  
|OAuth2RefreshToken_AuthorizationCodeGrant_TokenResponse|「選用」。 hello 重新整理權杖，可以使用的 tooobtain 新存取權杖。|  
|OAuth2RefreshToken_ClientCredentialsGrant_TokenResponse|「選用」。 hello 重新整理權杖，可以使用的 tooobtain 新存取權杖。|  
|OAuth2RefreshToken_ResourceOwnerPasswordCredentialsGrant_TokenResponse|「選用」。 hello 重新整理權杖，可以使用的 tooobtain 新存取權杖。|  
|OAuth2ResponseType_AuthorizationCodeGrant_AuthorizationRequest|「必要」。 值必須設定太 「 程式碼 」。|  
|OAuth2ResponseType_ImplicitGrant_AuthorizationRequest|「必要」。 值必須設定為太"語彙基元 」。|  
|OAuth2Scope_AuthorizationCodeGrant_AuthorizationRequest|「選用」。 hello 的 hello 存取要求的範圍。|  
|OAuth2Scope_AuthorizationCodeGrant_TokenResponse|選擇性，如果相同 toohello hello 用戶端; 要求的範圍否則，為必要項。|  
|OAuth2Scope_ClientCredentialsGrant_TokenRequest|「選用」。 hello 的 hello 存取要求的範圍。|  
|OAuth2Scope_ClientCredentialsGrant_TokenResponse|選擇性的如果相同 hello 用戶端; 要求的 toohello 範圍否則，為必要項。|  
|OAuth2Scope_ImplicitGrant_AuthorizationRequest|「選用」。 hello 的 hello 存取要求的範圍。|  
|OAuth2Scope_ImplicitGrant_AuthorizationResponse|選擇性，如果相同 toohello hello 用戶端; 要求的範圍否則，為必要項。|  
|OAuth2Scope_ResourceOwnerPasswordCredentialsGrant_TokenRequest|「選用」。 hello 的 hello 存取要求的範圍。|  
|OAuth2Scope_ResourceOwnerPasswordCredentialsGrant_TokenResponse|選擇性的如果相同 hello 用戶端; 要求的 toohello 範圍否則，為必要項。|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationErrorResponse|需要 hello"state"參數是否存在於 hello 用戶端授權要求。  收到 hello 用戶端 hello 的確切值。|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationRequest|「建議使用」。 使用 hello 用戶端 toomaintain 狀態 hello 要求與回呼之間的不透明值。  重新導向 hello 使用者代理程式後 toohello 用戶端時，hello 授權伺服器會包含此值。  hello 參數應用於防止跨站台要求偽造。|  
|OAuth2State_AuthorizationCodeGrant_AuthorizationResponse|需要 hello"state"參數是否存在於 hello 用戶端授權要求。  收到 hello 用戶端 hello 的確切值。|  
|OAuth2State_ImplicitGrant_AuthorizationErrorResponse|需要 hello"state"參數是否存在於 hello 用戶端授權要求。  收到 hello 用戶端 hello 的確切值。|  
|OAuth2State_ImplicitGrant_AuthorizationRequest|「建議使用」。 使用 hello 用戶端 toomaintain 狀態 hello 要求與回呼之間的不透明值。  重新導向 hello 使用者代理程式後 toohello 用戶端時，hello 授權伺服器會包含此值。  hello 參數應用於防止跨站台要求偽造。|  
|OAuth2State_ImplicitGrant_AuthorizationResponse|需要 hello"state"參數是否存在於 hello 用戶端授權要求。  收到 hello 用戶端 hello 的確切值。|  
|OAuth2TokenType_AuthorizationCodeGrant_TokenResponse|「必要」。 hello hello 發出的權杖類型。|  
|OAuth2TokenType_ClientCredentialsGrant_TokenResponse|「必要」。 hello hello 發出的權杖類型。|  
|OAuth2TokenType_ImplicitGrant_AuthorizationResponse|「必要」。 hello hello 發出的權杖類型。|  
|OAuth2TokenType_ResourceOwnerPasswordCredentialsGrant_TokenResponse|「必要」。 hello hello 發出的權杖類型。|  
|OAuth2UserName_ResourceOwnerPasswordCredentialsGrant_TokenRequest|「必要」。 hello 資源擁有者使用者名稱。|  
|OAuth2UnsupportedTokenType|不支援 '{0}' 權杖類型。|  
|OAuth2InvalidState|來自授權伺服器的回應無效|  
|OAuth2GrantType_AuthorizationCode|授權碼|  
|OAuth2GrantType_Implicit|隱含|  
|OAuth2GrantType_ClientCredentials|用戶端認證|  
|OAuth2GrantType_ResourceOwnerPassword|資源擁有者的密碼|  
|WebDocumentation302Code|302 已找到|  
|WebDocumentation400Code|400 (不正確的要求)|  
|OAuth2SendingMethod_AuthHeader|驗證標頭|  
|OAuth2SendingMethod_QueryParam|查詢參數|  
|OAuth2AuthorizationServerGeneralException|透過 {0} 授權存取時發生錯誤|  
|OAuth2AuthorizationServerCommunicationException|無法建立 HTTP 連線 tooauthorization 伺服器或已意外關閉。|  
|WebDocumentationOAuth2GeneralErrorMessage|發生未預期的錯誤。|  
|AuthorizationServerCommunicationException|發生授權伺服器通訊的例外狀況。 請連絡系統管理員。|  
|TextblockSubscriptionKeyHeaderDescription|訂閱可提供存取 toothis API 金鑰。 可在您的<a href='/developer'\>設定檔</a\>中找到。|  
|TextblockOAuthHeaderDescription|自 <i\>{0}</i\> 取得的 OAuth 2.0 存取權杖。 支援的授與類型︰<i\>{1}</i\>。|  
|TextblockContentTypeHeaderDescription|媒體類型 hello 主體傳送 toohello API。|  
|ErrorMessageApiNotAccessible|在這個階段，不能存取 hello 想 toocall API。 請連絡 hello API 發行者 < a href ="/ 發出"\>這裡 </a\>。|  
|ErrorMessageApiTimedout|hello 想 toocall API 所花的時間比正常 tooget 回應回。 請連絡 hello API 發行者 < a href ="/ 發出"\>這裡 </a\>。|  
|BadRequestParameterExpected|「預期收到 '{0}' 參數」|  
|TooltipTextDoubleClickToSelectAll|按兩下 tooselect 所有。|  
|TooltipTextHideRevealSecret|顯示/隱藏|  
|ButtonLinkOpenConsole|試試看|  
|SectionHeadingRequestBody|要求本文|  
|SectionHeadingRequestParameters|要求參數|  
|SectionHeadingRequestUrl|要求 URL|  
|SectionHeadingResponse|回應|  
|SectionHeadingRequestHeaders|要求標頭|  
|FormLabelSubtextOptional|選用|  
|SectionHeadingCodeSamples|程式碼範例|  
|TextblockOpenidConnectHeaderDescription|自 <i\>{0}</i\> 取得的 OpenID 連接識別碼。 支援的授與類型︰<i\>{1}</i\>。|  
  
###  <a name="ErrorPageStrings"></a> ErrorPageStrings  
  
|名稱|文字|  
|----------|----------|  
|LinkLabelBack|上一步|  
|LinkLabelHomePage|首頁|  
|LinkLabelSendUsEmail|傳送電子郵件|  
|PageTitleError|很抱歉，發生問題的處理 hello 要求的頁面|  
|TextblockPotentialCauseIntermittentIssue|這是間歇性的資料存取問題，可能已經不存在。|  
|TextblockPotentialCauseOldLink|您按一下 hello 連結可能變舊，並不是點 toohello 更正位置不再。|  
|TextblockPotentialCauseTechnicalProblem|可能是我們這一端發生技術問題。|  
|TextblockPotentialSolutionRefresh|請嘗試重新整理 hello 頁面。|  
|TextblockPotentialSolutionStartOver|自我們的 {0} 從頭開始。|  
|TextblockPotentialSolutionTryAgain|移 {0}，然後再試一次執行的 hello 動作。|  
|TextReportProblem|{0} 描述問題出在哪裡，我們會盡快查看。|  
|TitlePotentialCause|可能的原因|  
|TitlePotentialSolution|可能是只是暫時問題，幾件事 tootry|  
  
###  <a name="IssuesStrings"></a> IssuesStrings  
  
|名稱|文字|  
|----------|----------|  
|WebIssuesIndexTitle|問題|  
|WebIssuesNoActiveSubscriptions|您沒有作用中的訂用帳戶。 您需要 toosubscribe 產品 tooreport 發生問題。|  
|WebIssuesNotSignin|您尚未登入。 請 {0} tooreport 發生問題，或是張貼註解。|  
|WebIssuesReportIssueButton|報告問題|  
|WebIssuesSignIn|登入|  
|WebIssuesStatusReportedBy|狀態︰{0} &#124；由 {1} 報告|  
  
###  <a name="NotFoundStrings"></a> NotFoundStrings  
  
|名稱|文字|  
|----------|----------|  
|LinkLabelHomePage|首頁|  
|LinkLabelSendUsEmail|傳送電子郵件|  
|PageTitleNotFound|很抱歉，我們找不到您要尋找的 hello 頁面|  
|TextblockPotentialCauseMisspelledUrl|您可能拼錯 hello URL 如果您在輸入。|  
|TextblockPotentialCauseOldLink|您按一下 hello 連結可能變舊，並不是點 toohello 更正位置不再。|  
|TextblockPotentialSolutionRetype|請嘗試重新輸入 hello URL。|  
|TextblockPotentialSolutionStartOver|自我們的 {0} 從頭開始。|  
|TextReportProblem|{0} 描述問題出在哪裡，我們會盡快查看。|  
|TitlePotentialCause|可能的原因|  
|TitlePotentialSolution|可能的解決辦法|  
  
###  <a name="ProductDetailsStrings"></a> ProductDetailsStrings  
  
|名稱|文字|  
|----------|----------|  
|WebProductsAgreement|藉由訂閱太 {0} 產品，我同意 toohello `<a data-toggle='modal' href='#legal-terms'\>Terms of Use</a\>`。|  
|WebProductsLegalTermsLink|使用條款|  
|WebProductsSubscribeButton|訂閱|  
|WebProductsUsageLimitsHeader|使用限制|  
|WebProductsYouAreNotSubscribed|您已訂閱的 toothis 產品。|  
|WebProductsYouRequestedSubscription|您要求訂閱 toothis 產品。|  
|ErrorYouNeedtoAgreeWithLegalTerms|您可以繼續之前，您必須同意 toohello 使用條款。|  
|ButtonLabelAddSubscription|加入訂閱|  
|LinkLabelChangeSubscriptionName|變更|  
|ButtonLabelConfirm|確認|  
|TextblockMultipleSubscriptionsCount|您有 {0} 訂閱 toothis 產品：|  
|TextblockSingleSubscriptionsCount|您有 {0} 訂閱 toothis 產品：|  
|TextblockSingleApisCount|此產品有 {0} 個 API:|  
|TextblockMultipleApisCount|此產品有 {0} 個 API:|  
|TextblockHeaderSubscribe|訂閱 tooproduct|  
|TextblockSubscriptionDescription|已建立新的訂用帳戶如下:|  
|TextblockSubscriptionLimitReached|已達到訂用帳戶限制。|  
  
###  <a name="ProductsStrings"></a> ProductsStrings  
  
|名稱|文字|  
|----------|----------|  
|PageTitleProducts|產品|  
  
###  <a name="ProviderInfoStrings"></a> ProviderInfoStrings  
  
|名稱|文字|  
|----------|----------|  
|TextboxExternalIdentitiesDisabled|登入已停用 hello 系統管理員在 hello 的時刻。|  
|TextboxExternalIdentitiesSigninInvitation|或者，以此登入|  
|TextboxExternalIdentitiesSigninInvitationPrimary|以此登入:|  
  
###  <a name="SigninResources"></a> SigninResources  
  
|名稱|文字|  
|----------|----------|  
|PrincipalNotFound|找不到主體或簽章無效|  
|ErrorSsoAuthenticationFailed|SSO 驗證失敗|  
|ErrorSsoAuthenticationFailedDetailed|提供的權杖無效或無法驗證簽章。|  
|ErrorSsoTokenInvalid|SSO 權杖無效|  
|ValidationErrorSpecificEmailAlreadyExists|電子郵件 ' {0} ' 已註冊|  
|ValidationErrorSpecificEmailInvalid|電子郵件 '{0}' 無效|  
|ValidationErrorPasswordInvalid|密碼無效。 請更正 hello 錯誤，然後再試一次。|  
|PropertyTooShort|{0} 太短|  
|WebAuthenticationAddresserEmailInvalidErrorMessage|電子郵件地址無效。|  
|ValidationMessageNewPasswordConfirmationRequired|確認新密碼|  
|ValidationErrorPasswordConfirmationRequired|確認密碼為空白|  
|WebAuthenticationEmailChangeNotice|變更確認電子郵件正在傳送 hello 太 {0}。 請依照 tooconfirm 其內的指示進行新的電子郵件地址。 如果 hello 電子郵件未到達 tooyour 收件匣中 hello 接下來的幾分鐘內，請檢查垃圾郵件資料夾。|  
|WebAuthenticationEmailChangeNoticeHeader|已成功處理您的電子郵件變更要求|  
|WebAuthenticationEmailChangeNoticeTitle|已要求電子郵件變更|  
|WebAuthenticationEmailHasBeenRevertedNotice|您的電子郵件已經存在。 已還原要求|  
|ValidationErrorEmailAlreadyExists|電子郵件已經存在|  
|ValidationErrorEmailInvalid|電子郵件地址無效|  
|TextboxLabelEmail|電子郵件|  
|ValidationErrorEmailRequired|電子郵件為必填欄位。|  
|WebAuthenticationErrorNoticeHeader|錯誤|  
|WebAuthenticationFieldLengthErrorMessage|{0} 的長度上限是 {1}|  
|TextboxLabelEmailFirstName|名字|  
|ValidationErrorFirstNameRequired|名字為必填欄位。|  
|ValidationErrorFirstNameInvalid|名字無效|  
|NoticeInvalidInvitationToken|請注意，確認連結只在 48 小時內有效。 如果您仍在此時間範圍內時，請確定您的連結正確。 如果您的連結已過期，請重複嘗試 tooconfirm hello 動作。|  
|NoticeHeaderInvalidInvitationToken|無效的邀請權杖|  
|NoticeTitleInvalidInvitationToken|確認錯誤|  
|WebAuthenticationLastNameInvalidErrorMessage|姓氏無效|  
|TextboxLabelEmailLastName|姓氏|  
|ValidationErrorLastNameRequired|姓氏為必填欄位。|  
|WebAuthenticationLinkExpiredNotice|確認連結傳送 tooyou 已過期。 `<a href={0}?token={1}>Resend confirmation email.</a\>`|  
|NoticePasswordResetLinkInvalidOrExpired|您的密碼重設連結無效或已過期。|  
|WebAuthenticationLinkExpiredNoticeTitle|已傳送連結|  
|WebAuthenticationNewPasswordLabel|新密碼|  
|ValidationMessageNewPasswordRequired|新密碼為必填欄位。|  
|TextboxLabelNotificationsSenderEmail|通知的寄件者電子郵件|  
|TextboxLabelOrganizationName|組織名稱|  
|WebAuthenticationOrganizationRequiredErrorMessage|組織名稱為空白|  
|WebAuthenticationPasswordChangedNotice|已成功更新您的密碼|  
|WebAuthenticationPasswordChangedNoticeTitle|已更新密碼|  
|WebAuthenticationPasswordCompareErrorMessage|密碼不符|  
|WebAuthenticationPasswordConfirmLabel|確認密碼|  
|ValidationErrorPasswordInvalidDetailed|密碼太弱。|  
|WebAuthenticationPasswordLabel|密碼|  
|ValidationErrorPasswordRequired|密碼為必填欄位。|  
|WebAuthenticationPasswordResetSendNotice|變更密碼確認電子郵件正在傳送 hello 太 {0}。 請依照您的密碼變更程序內 hello 電子郵件 toocontinue hello 指示。|  
|WebAuthenticationPasswordResetSendNoticeHeader|已成功處理您的密碼重設要求|  
|WebAuthenticationPasswordResetSendNoticeTitle|已要求密碼重設|  
|WebAuthenticationRequestNotFoundNotice|找不到要求|  
|WebAuthenticationSenderEmailRequiredErrorMessage|通知的寄件者電子郵件為空白|  
|WebAuthenticationSigninPasswordLabel|請輸入密碼以確認 hello 變更|  
|WebAuthenticationSignupConfirmNotice|註冊確認電子郵件是途中太 {0}。 < b /\>內 hello 請遵循指示的電子郵件 tooactivate 您的帳戶。 < b /\>如果 hello 電子郵件未到達收件匣內 hello 中下一個幾分鐘的時間，請檢查您的垃圾郵件資料夾。|  
|WebAuthenticationSignupConfirmNoticeHeader|已成功建立您的帳戶|  
|WebAuthenticationSignupConfirmNoticeRepeatHeader|已再次傳送註冊確認電子郵件|  
|WebAuthenticationSignupConfirmNoticeTitle|已建立帳戶|  
|WebAuthenticationTokenRequiredErrorMessage|權杖為空白|  
|WebAuthenticationUserAlreadyRegisteredNotice|似乎 hello 系統中已經登錄具有這封電子郵件的使用者。 如果您忘記密碼，請再試一次 toorestore 它，或連絡支援小組。|  
|WebAuthenticationUserAlreadyRegisteredNoticeHeader|使用者已經註冊|  
|WebAuthenticationUserAlreadyRegisteredNoticeTitle|已經註冊|  
|ButtonLabelChangePassword|變更密碼|  
|ButtonLabelChangeAccountInfo|變更帳戶資訊|  
|ButtonLabelCloseAccount|關閉帳戶|  
|WebAuthenticationInvalidCaptchaErrorMessage|輸入文字不符合 hello 圖片上的文字。 請再試一次。|  
|ValidationErrorCredentialsInvalid|電子郵件或密碼無效。 請更正 hello 錯誤，然後再試一次。|  
|WebAuthenticationRequestIsNotValid|要求無效|  
|WebAuthenticationUserIsNotConfirm|請嘗試在 toosign 之前，確認您的註冊。|  
|WebAuthenticationInvalidEmailFormated|電子郵件無效: {0}|  
|WebAuthenticationUserNotFound|找不到使用者|  
|WebAuthenticationTenantNotRegistered|您的帳戶屬於 tooa Azure Active Directory 租用戶未獲得授權的 tooaccess 此入口網站。|  
|WebAuthenticationAuthenticationFailed|驗證失敗。|  
|WebAuthenticationGooglePlusNotEnabled|驗證失敗。 如果您已授權 hello 應用程式，請連絡 [hello admin toomake 確定已正確設定 Google 驗證。|  
|ValidationErrorAllowedTenantIsRequired|允許的租用戶為必填欄位|  
|ValidationErrorTenantIsNotValid|hello Azure Active Directory 租用戶 '{0}' 不是有效的。|  
|WebAuthenticationActiveDirectoryTitle|Azure Active Directory|  
|WebAuthenticationLoginUsingYourProvider|使用您的 {0} 帳戶登入|  
|WebAuthenticationUserLimitNotice|此服務已達到 hello 允許使用者的數目上限。 請`<a href="mailto:{0}"\>contact hello administrator</a\>`tooupgrade 服務再重新啟用的使用者註冊。|  
|WebAuthenticationUserLimitNoticeHeader|已停用使用者註冊|  
|WebAuthenticationUserLimitNoticeTitle|已停用使用者註冊|  
|WebAuthenticationUserRegistrationDisabledNotice|Hello 管理員已經停用註冊的使用者。 請使用外部識別提供者登入。|  
|WebAuthenticationUserRegistrationDisabledNoticeHeader|已停用使用者註冊|  
|WebAuthenticationUserRegistrationDisabledNoticeTitle|已停用使用者註冊|  
|WebAuthenticationSignupPendingConfirmationNotice|我們可以完成您的帳戶建立 hello 我們需要先 tooverify 電子郵件地址。 我們先前曾傳送一封電子郵件太 {0}。 請依照內部 hello 電子郵件 tooactivate hello 指示您的帳戶。 如果下一個幾分鐘的時間時，不 hello 內送達 hello 電子郵件，請檢查垃圾郵件資料夾。|  
|WebAuthenticationSignupPendingConfirmationAccountFoundNotice|我們 hello 電子郵件地址 {0} 中發現未確認的帳戶。 toocomplete hello 建立您的帳戶 tooverify 我們需要您的電子郵件地址。 我們先前曾傳送一封電子郵件太 {0}。 請依照內部 hello 電子郵件 tooactivate hello 指示您的帳戶。 如果下一個幾分鐘的時間時，不 hello 內送達 hello 電子郵件，請檢查垃圾郵件資料夾|  
|WebAuthenticationSignupConfirmationAlmostDone|快要完成了|  
|WebAuthenticationSignupConfirmationEmailSent|我們先前曾傳送一封電子郵件太 {0}。 請依照內部 hello 電子郵件 tooactivate hello 指示您的帳戶。 如果下一個幾分鐘的時間時，不 hello 內送達 hello 電子郵件，請檢查垃圾郵件資料夾。|  
|WebAuthenticationEmailSentNotificationMessage|電子郵件傳送成功太 {0}|  
|WebAuthenticationNoAadTenantConfigured|Hello 服務設定沒有 Azure Active Directory 租用戶。|  
|CheckboxLabelUserRegistrationTermsConsentRequired|我同意 toohello `<a data-toggle="modal" href="#" data-target="#terms"\>Terms of Use</a\>`。|  
|TextblockUserRegistrationTermsProvided|請檢閱 `<a data-toggle="modal" href="#" data-target="#terms"\>Terms of Use.</a\>`|  
|DialogHeadingTermsOfUse|使用條款|  
|ValidationMessageConsentNotAccepted|您可以繼續之前，您必須同意 toohello 使用條款。|  
  
###  <a name="SigninStrings"></a> SigninStrings  
  
|名稱|文字|  
|----------|----------|  
|WebAuthenticationForgotPassword|忘記密碼了嗎?|  
|WebAuthenticationIfAdministrator|如果您是系統管理員，您必須登入 `<a href="{0}"\>here</a\>`。|  
|WebAuthenticationNotAMember|還不是會員嗎? `<a href="/signup"\>Sign up now</a\>`|  
|WebAuthenticationRemember|在這台電腦上記住我|  
|WebAuthenticationSigininWithPassword|以您的使用者名稱和密碼登入|  
|WebAuthenticationSigninTitle|登入|  
|WebAuthenticationSignUpNow|立即註冊|  
  
###  <a name="SignupStrings"></a> SignupStrings  
  
|名稱|文字|  
|----------|----------|  
|PageTitleSignup|註冊|  
|WebAuthenticationAlreadyAMember|已經是會員嗎?|  
|WebAuthenticationCreateNewAccount|建立新的 API 管理帳戶|  
|WebAuthenticationSigninNow|立即登入|  
|ButtonLabelSignup|註冊|  
  
###  <a name="SubscriptionListStrings"></a> SubscriptionListStrings  
  
|名稱|文字|  
|----------|----------|  
|SubscriptionCancelConfirmation|確定您想 toocancel 此訂用帳戶？|  
|SubscriptionRenewConfirmation|確定您想 toorenew 此訂用帳戶？|  
|WebDevelopersManageSubscriptions|管理訂用帳戶|  
|WebDevelopersPrimaryKey|主索引鍵|  
|WebDevelopersRegenerateLink|重新產生|  
|WebDevelopersSecondaryKey|次要索引鍵|  
|ButtonLabelShowKey|顯示|  
|ButtonLabelRenewSubscription|續訂|  
|WebDevelopersSubscriptionReqested|已於 {0} 要求|  
|WebDevelopersSubscriptionRequestedState|已要求|  
|WebDevelopersSubscriptionTableNameHeader|名稱|  
|WebDevelopersSubscriptionTableStateHeader|狀態|  
|WebDevelopersUsageStatisticsLink|分析報告|  
|WebDevelopersYourSubscriptions|您的訂用帳戶|  
|SubscriptionPropertyLabelRequestedDate|已於此日期要求|  
|SubscriptionPropertyLabelStartedDate|已於此日期開始|  
|PageTitleRenameSubscription|重新命名訂用帳戶|  
|SubscriptionPropertyLabelName|訂用帳戶名稱|  
  
###  <a name="SubscriptionStrings"></a> SubscriptionStrings  
  
|名稱|文字|  
|----------|----------|  
|SectionHeadingCloseAccount|尋找 tooclose 您的帳戶嗎？|  
|PageTitleDeveloperProfile|設定檔|  
|ButtonLabelHideKey|隱藏|  
|ButtonLabelRegenerateKey|重新產生|  
|InformationMessageKeyWasRegenerated|確定您想 tooregenerate 這個機碼？|  
|ButtonLabelShowKey|顯示|  
  
###  <a name="UpdateProfileStrings"></a> UpdateProfileStrings  
  
|名稱|文字|  
|----------|----------|  
|ButtonLabelUpdateProfile|更新設定檔|  
|PageTitleUpdateProfile|變更帳戶資訊|  
  
###  <a name="UserProfile"></a> UserProfile  
  
|名稱|文字|  
|----------|----------|  
|ButtonLabelChangeAccountInfo|變更帳戶資訊|  
|ButtonLabelChangePassword|變更密碼|  
|ButtonLabelCloseAccount|關閉帳戶|  
|TextboxLabelEmail|電子郵件|  
|TextboxLabelEmailFirstName|名字|  
|TextboxLabelEmailLastName|姓氏|  
|TextboxLabelNotificationsSenderEmail|通知的寄件者電子郵件|  
|TextboxLabelOrganizationName|組織名稱|  
|SubscriptionStateActive|作用中|  
|SubscriptionStateCancelled|已取消|  
|SubscriptionStateExpired|已過期|  
|SubscriptionStateRejected|已拒絕|  
|SubscriptionStateRequested|已要求|  
|SubscriptionStateSuspended|暫止|  
|DefaultSubscriptionNameTemplate|{0}  (預設值)|  
|SubscriptionNameTemplate|開發人員存取 #{0}|  
|TextboxLabelSubscriptionName|訂用帳戶名稱|  
|ValidationMessageSubscriptionNameRequired|訂用帳戶名稱不可為空白。|  
|ApiManagementUserLimitReached|此服務已達到 hello 允許使用者的數目上限。 請升級 tooa 更高的定價層。|  
  
##  <a name="glyphs"></a> 圖像資源  
 API 管理開發人員入口網站範本可以使用從 hello 圖像[啟動程序從 Glyphicons](http://getbootstrap.com/components/#glyphicons)。 這組圖像 （glyph） 包含超過 250 圖像 （glyph） 字型格式從 hello [Glyphicon](http://glyphicons.com/) Halflings 設定。 toouse 圖像，以從這個設定，請使用下列語法的 hello。  
  
```html  
<span class="glyphicon glyphicon-user">  
```  
  
 Hello 圖像 （glyph） 的完整清單，請參閱[啟動程序從 Glyphicons](http://getbootstrap.com/components/#glyphicons)。

## <a name="next-steps"></a>後續步驟
如需有關使用範本的詳細資訊，請參閱[toocustomize hello API 管理開發人員入口網站使用範本的方式](api-management-developer-portal-templates.md)。
