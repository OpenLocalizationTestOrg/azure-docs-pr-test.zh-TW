---
title: "aaaAzure AD 服務 tooService Auth 使用 OAuth2.0 |Microsoft 文件"
description: "本文說明如何 toouse HTTP 訊息 tooimplement 服務使用 hello OAuth2.0 用戶端認證授與流程 tooservice 驗證。"
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: a7f939d9-532d-4b6d-b6d3-95520207965d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: f4bfd4ea8a7de1929c7dcf7ad65a156edff74f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# 使用用戶端認證 （共用的密碼或憑證） 的服務 tooservice 呼叫
hello OAuth 2.0 用戶端認證授與流程可允許 web 服務 (*機密用戶端*) toouse 它自己的認證，而不是模擬使用者，tooauthenticate 時呼叫另一個 web 服務。 在此案例中，通常的 hello 用戶端是中間層 web 服務、 精靈服務或網站。 更高等級的保證，Azure AD 也可讓 hello 呼叫服務 toouse （而不是共用的密碼） 做為認證的憑證。

## 用戶端認證授與流程圖
hello 下列圖表說明如何 hello 用戶端認證授與流程在 Azure Active Directory (Azure AD) 中的運作方式。

![OAuth2.0 用戶端認證授與流程](media/active-directory-protocols-oauth-service-to-service/active-directory-protocols-oauth-client-credentials-grant-flow.jpg)

1. hello 用戶端應用程式會驗證 toohello Azure AD 權杖發行端點，並要求存取權杖。
2. hello Azure AD 權杖發行端點問題 hello 存取權杖。
3. 受保護資源的使用的 tooauthenticate toohello hello 存取權杖。
4. Toohello web 應用程式時，會傳回從 hello 保護資源的資料。

## 在 Azure AD 中註冊 hello 服務
註冊呼叫服務的 hello 和接收服務在 Azure Active Directory (Azure AD) 中的 hello。 如需詳細指示，請參閱[整合應用程式與 Azure Active Directory](active-directory-integrating-applications.md)。

## 要求存取權杖
toorequest 存取權杖，使用 HTTP POST toohello 租用戶特定 Azure AD 端點。

```
https://login.microsoftonline.com/<tenant id>/oauth2/token
```

## 服務對服務存取權杖要求
有兩種情況下，根據 hello 用戶端應用程式是否選擇 toobe 受到共用的密碼或憑證。

### 第一種情況︰使用共用密碼的存取權杖要求
當使用共用的密碼時，服務對服務存取權杖要求包含下列參數的 hello:

| 參數 |  | 說明 |
| --- | --- | --- |
| grant_type |必要 |指定要求的 hello 授與類型。 Hello 值必須是在用戶端認證授與流程中， **client_credentials**。 |
| client_id |必要 |指定呼叫 web 服務的 hello hello Azure AD 用戶端識別碼。 在 hello 中呼叫應用程式的用戶端識別碼，toofind hello [Azure 入口網站](https://portal.azure.com)，按一下**Active Directory**，切換目錄，按一下 hello 應用程式。 hello client_id 為 hello*應用程式識別碼* |
| client_secret |必要 |輸入為呼叫 web 服務或協助程式應用程式在 Azure AD 中的 hello 註冊金鑰。 toocreate hello Azure 入口網站中的索引鍵，按一下**Active Directory**，切換目錄中，按一下 hello 應用程式，按一下**設定**，按一下 **金鑰**，並加入的機碼。|
| resource |必要 |輸入 hello hello 接收 web 服務應用程式識別碼 URI。 toofind hello 應用程式識別碼 URI，在 hello Azure 入口網站中的按一下**Active Directory**，切換目錄、 按一下 hello 服務應用程式，然後按一下**設定**和**屬性** |

#### 範例
hello 下列 HTTP POST 要求 hello https://service.contoso.com/ web 服務的存取權杖。 hello`client_id`識別 hello 要求 hello 存取權杖的 web 服務。

```
POST /contoso.com/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&client_id=625bc9f6-3bf6-4b6d-94ba-e97cf07a22de&client_secret=qkDwDJlDfig2IpeuUZYKH1Wb8q1V0ju6sILxQQqhJ+s=&resource=https%3A%2F%2Fservice.contoso.com%2F
```

### 第二種情況︰使用憑證的存取權杖要求
使用憑證服務對服務存取權杖要求包含下列參數的 hello:

| 參數 |  | 說明 |
| --- | --- | --- |
| grant_type |必要 |指定 hello 要求的回應類型。 Hello 值必須是在用戶端認證授與流程中， **client_credentials**。 |
| client_id |必要 |指定呼叫 web 服務的 hello hello Azure AD 用戶端識別碼。 在 hello 中呼叫應用程式的用戶端識別碼，toofind hello [Azure 入口網站](https://portal.azure.com)，按一下**Active Directory**，切換目錄，按一下 hello 應用程式。 hello client_id 為 hello*應用程式識別碼* |
| client_assertion_type |必要 |hello 值必須是`urn:ietf:params:oauth:client-assertion-type:jwt-bearer` |
| client_assertion |必要 | 判斷提示 （JSON Web 權杖），您需要 toocreate hello 以簽署憑證，您會註冊為您的應用程式的認證。 閱讀有關[憑證認證](active-directory-certificate-credentials.md)toolearn 如何 tooregister hello 判斷提示您憑證和 hello 的格式。|
| resource | 必要 |輸入 hello hello 接收 web 服務應用程式識別碼 URI。 toofind hello 應用程式識別碼 URI，在 hello Azure 入口網站中的按一下**Active Directory**、 按一下 hello 目錄、 按一下 hello 應用程式，然後按一下**設定**。 |

請注意，hello 參數幾乎 hello 與 hello 大小寫的 hello 要求相同的共用密碼之處在於會以兩個參數取代 hello client_secret 參數： client_assertion_type 和 client_assertion。

#### 範例
hello 下列 HTTP POST 要求的憑證 hello https://service.contoso.com/ web 服務的存取權杖。 hello`client_id`識別 hello 要求 hello 存取權杖的 web 服務。

```
POST /<tenant_id>/oauth2/token HTTP/1.1
Host: login.microsoftonline.com
Content-Type: application/x-www-form-urlencoded

resource=https%3A%2F%contoso.onmicrosoft.com%2Ffc7664b4-cdd6-43e1-9365-c2e1c4e1b3bf&client_id=97e0a5b7-d745-40b6-94fe-5f77d35c6e05&client_assertion_type=urn%3Aietf%3Aparams%3Aoauth%3Aclient-assertion-type%3Ajwt-bearer&client_assertion=eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJ{a lot of characters here}M8U3bSUKKJDEg&grant_type=client_credentials
```

### 服務對服務存取權杖回應

成功回應包含 JSON OAuth 2.0 回應以 hello 下列參數：

| 參數 | 說明 |
| --- | --- |
| access_token |hello 要求的存取權杖。 hello 呼叫 web 服務可以使用這個語彙基元 tooauthenticate toohello，接收 web 服務。 |
| token_type |表示 hello 語彙基元型別值。 hello Azure AD 支援的類型**承載**。 如需承載權杖的詳細資訊，請參閱 hello [OAuth 2.0 授權架構： 承載權杖用法 (RFC 6750)](http://www.rfc-editor.org/rfc/rfc6750.txt)。 |
| expires_in |多久 hello 存取權杖是有效 （以秒為單位）。 |
| expires_on |hello hello 存取權杖到期的時間。 hello 日期以 hello 的秒數表示從 1970年-01-01T0:0:0Z UTC 直到 hello 到期時間。 這個值是使用的 toodetermine hello 存留期，快取權杖。 |
| not_before |hello 時間從哪些 hello 存取權杖就會變成可用。 hello 日期以 hello 的秒數表示從 1970年-01-01T0:0:0Z UTC 直到 hello 權杖的有效時間。|
| resource |hello hello 接收 web 服務應用程式識別碼 URI。 |

#### 回應範例
hello 下列範例顯示成功回應 tooa 要求存取權杖 tooa web 服務。

```
{
"access_token":"eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJodHRwczovL3NlcnZpY2UuY29udG9zby5jb20vIiwiaXNzIjoiaHR0cHM6Ly9zdHMud2luZG93cy5uZXQvN2ZlODE0NDctZGE1Ny00Mzg1LWJlY2ItNmRlNTdmMjE0NzdlLyIsImlhdCI6MTM4ODQ0ODI2NywibmJmIjoxMzg4NDQ4MjY3LCJleHAiOjEzODg0NTIxNjcsInZlciI6IjEuMCIsInRpZCI6IjdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZSIsIm9pZCI6ImE5OTE5MTYyLTkyMTctNDlkYS1hZTIyLWYxMTM3YzI1Y2RlYSIsInN1YiI6ImE5OTE5MTYyLTkyMTctNDlkYS1hZTIyLWYxMTM3YzI1Y2RlYSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzdmZTgxNDQ3LWRhNTctNDM4NS1iZWNiLTZkZTU3ZjIxNDc3ZS8iLCJhcHBpZCI6ImQxN2QxNWJjLWM1NzYtNDFlNS05MjdmLWRiNWYzMGRkNThmMSIsImFwcGlkYWNyIjoiMSJ9.aqtfJ7G37CpKV901Vm9sGiQhde0WMg6luYJR4wuNR2ffaQsVPPpKirM5rbc6o5CmW1OtmaAIdwDcL6i9ZT9ooIIicSRrjCYMYWHX08ip-tj-uWUihGztI02xKdWiycItpWiHxapQm0a8Ti1CWRjJghORC1B1-fah_yWx6Cjuf4QE8xJcu-ZHX0pVZNPX22PHYV5Km-vPTq2HtIqdboKyZy3Y4y3geOrRIFElZYoqjqSv5q9Jgtj5ERsNQIjefpyxW3EwPtFqMcDm4ebiAEpoEWRN4QYOMxnC9OUBeG9oLA0lTfmhgHLAtvJogJcYFzwngTsVo6HznsvPWy7UP3MINA",
"token_type":"Bearer",
"expires_in":"3599",
"expires_on":"1388452167",
"resource":"https://service.contoso.com/"
}
```

## 另請參閱
* [Azure AD 中的 OAuth 2.0](active-directory-protocols-oauth-code.md)
* [在 C# 中使用共用密碼 hello 服務 tooservice 呼叫的範例](https://github.com/Azure-Samples/active-directory-dotnet-daemon)和[在 C# 中使用憑證的 hello 服務 tooservice 呼叫的範例](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential)
