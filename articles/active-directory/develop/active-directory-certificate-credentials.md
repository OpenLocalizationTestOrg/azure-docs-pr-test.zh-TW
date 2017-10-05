---
title: "Azure AD 中的憑證認證 | Microsoft Docs"
description: "本文討論如何註冊和使用憑證認證來進行應用程式驗證"
services: active-directory
documentationcenter: .net
author: navyasric
manager: mbaldwin
editor: 
ms.assetid: 88f0c64a-25f7-4974-aca2-2acadc9acbd8
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 08bb5140bb35bbd120aaa506afeab8ad247f81e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="certificate-credentials-for-application-authentication"></a><span data-ttu-id="50bb1-103">適用於應用程式驗證的憑證認證</span><span class="sxs-lookup"><span data-stu-id="50bb1-103">Certificate credentials for application authentication</span></span>

<span data-ttu-id="50bb1-104">Azure Active Directory 可讓應用程式使用自己的認證進行驗證，例如，在 OAuth 2.0 用戶端認證授與流程和代理者流程中。</span><span class="sxs-lookup"><span data-stu-id="50bb1-104">Azure Active Directory allows an application to use its own credentials for authentication, for example, in the OAuth 2.0 Client Credentials Grant flow and the On-Behalf-Of flow.</span></span>
<span data-ttu-id="50bb1-105">可用的認證形式之一，便是以應用程式擁有的憑證所簽署的 JSON Web 權杖 (JWT) 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="50bb1-105">One form of credential that can be used is a JSON Web Token(JWT) assertion signed with a certificate that the application owns.</span></span>

## <a name="format-of-the-assertion"></a><span data-ttu-id="50bb1-106">判斷提示的格式</span><span class="sxs-lookup"><span data-stu-id="50bb1-106">Format of the assertion</span></span>
<span data-ttu-id="50bb1-107">為了計算判斷提示，您可能想要使用所選語言中許多 [JSON Web 權杖](https://jwt.io/) \(英文\) 程式庫其中之一。</span><span class="sxs-lookup"><span data-stu-id="50bb1-107">To compute the assertion, you probably want to use one of the many [JSON Web Token](https://jwt.io/) libraries in the language of your choice.</span></span> <span data-ttu-id="50bb1-108">權杖所攜帶的資訊是︰</span><span class="sxs-lookup"><span data-stu-id="50bb1-108">The information carried by the token is:</span></span>

#### <a name="header"></a><span data-ttu-id="50bb1-109">頁首</span><span class="sxs-lookup"><span data-stu-id="50bb1-109">Header</span></span>

| <span data-ttu-id="50bb1-110">參數</span><span class="sxs-lookup"><span data-stu-id="50bb1-110">Parameter</span></span> |  <span data-ttu-id="50bb1-111">備註</span><span class="sxs-lookup"><span data-stu-id="50bb1-111">Remark</span></span> |
| --- | --- | --- |
| `alg` | <span data-ttu-id="50bb1-112">應該是 **RS256**</span><span class="sxs-lookup"><span data-stu-id="50bb1-112">Should be **RS256**</span></span> |
| `typ` | <span data-ttu-id="50bb1-113">應該是 **JWT**</span><span class="sxs-lookup"><span data-stu-id="50bb1-113">Should be **JWT**</span></span> |
| `x5t` | <span data-ttu-id="50bb1-114">應該是 X.509 憑證 SHA-1 憑證指紋</span><span class="sxs-lookup"><span data-stu-id="50bb1-114">Should be the X.509 Certificate SHA-1 thumbprint</span></span> |

#### <a name="claims-payload"></a><span data-ttu-id="50bb1-115">宣告 (承載)</span><span class="sxs-lookup"><span data-stu-id="50bb1-115">Claims (Payload)</span></span>

| <span data-ttu-id="50bb1-116">參數</span><span class="sxs-lookup"><span data-stu-id="50bb1-116">Parameter</span></span> |  <span data-ttu-id="50bb1-117">備註</span><span class="sxs-lookup"><span data-stu-id="50bb1-117">Remark</span></span> |
| --- | --- | --- |
| `aud` | <span data-ttu-id="50bb1-118">對象︰應該是 **https://login.microsoftonline.com/*租用戶 ID*/oauth2/權杖**</span><span class="sxs-lookup"><span data-stu-id="50bb1-118">Audience: Should be **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span></span> |
| `exp` | <span data-ttu-id="50bb1-119">到期日：權杖到期的日期。</span><span class="sxs-lookup"><span data-stu-id="50bb1-119">Expiration date: the date when the token expires.</span></span> <span data-ttu-id="50bb1-120">時間會表示為從 1970 年 1 月 1 日 (1970-01-01T0:0:0Z) UTC 到權杖有效時間到期的秒數。</span><span class="sxs-lookup"><span data-stu-id="50bb1-120">The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token validity expires.</span></span>|
| `iss` | <span data-ttu-id="50bb1-121">簽發者︰應該是 client_id (用戶端服務的應用程式識別碼)</span><span class="sxs-lookup"><span data-stu-id="50bb1-121">Issuer: should be the client_id (Application Id of the client service)</span></span> |
| `jti` | <span data-ttu-id="50bb1-122">GUID：JWT ID</span><span class="sxs-lookup"><span data-stu-id="50bb1-122">GUID: the JWT ID</span></span> |
| `nbf` | <span data-ttu-id="50bb1-123">生效時間：無法在此日期之前使用權杖。</span><span class="sxs-lookup"><span data-stu-id="50bb1-123">Not Before: the date before which the token cannot be used.</span></span> <span data-ttu-id="50bb1-124">時間會表示為從 1970 年 1 月 1 日 (1970-01-01T0:0:0Z) UTC 到權杖發出時間的秒數。</span><span class="sxs-lookup"><span data-stu-id="50bb1-124">The time is represented as the number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until the time the token was issued.</span></span> |
| `sub` | <span data-ttu-id="50bb1-125">主旨：對於 `iss`，應該是 client_id (用戶端服務的應用程式識別碼)</span><span class="sxs-lookup"><span data-stu-id="50bb1-125">Subject: As for `iss`, should be the client_id (Application Id of the client service)</span></span> |

#### <a name="signature"></a><span data-ttu-id="50bb1-126">簽章</span><span class="sxs-lookup"><span data-stu-id="50bb1-126">Signature</span></span>
<span data-ttu-id="50bb1-127">簽章是使用 [JSON Web 權杖 RFC7519 規格](https://tools.ietf.org/html/rfc7519) 中所述的憑證計算的</span><span class="sxs-lookup"><span data-stu-id="50bb1-127">The signature is computed applying the certificate as described in the [JSON Web Token RFC7519 specification](https://tools.ietf.org/html/rfc7519)</span></span>

### <a name="example-of-a-decoded-jwt-assertion"></a><span data-ttu-id="50bb1-128">已解碼的 JWT 判斷提示範例</span><span class="sxs-lookup"><span data-stu-id="50bb1-128">Example of a decoded JWT assertion</span></span>
```
{
  "alg": "RS256",
  "typ": "JWT",
  "x5t": "gx8tGysyjcRqKjFPnd7RFwvwZI0"
}
.
{
  "aud": "https: //login.microsoftonline.com/contoso.onmicrosoft.com/oauth2/token",
  "exp": 1484593341,
  "iss": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05",
  "jti": "22b3bb26-e046-42df-9c96-65dbd72c1c81",
  "nbf": 1484592741,  
  "sub": "97e0a5b7-d745-40b6-94fe-5f77d35c6e05"
}
.
"Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"

```

### <a name="example-of-an-encoded-jwt-assertion"></a><span data-ttu-id="50bb1-129">已編碼的 JWT 判斷提示範例</span><span class="sxs-lookup"><span data-stu-id="50bb1-129">Example of an encoded JWT assertion</span></span>
<span data-ttu-id="50bb1-130">下列字串是已編碼判斷提示的範例。</span><span class="sxs-lookup"><span data-stu-id="50bb1-130">The following string is an example of encoded assertion.</span></span> <span data-ttu-id="50bb1-131">如果您仔細看，會發現三個以點 (.) 分隔的區段。</span><span class="sxs-lookup"><span data-stu-id="50bb1-131">If you look carefully, you notice three sections separated by dots (.).</span></span>
<span data-ttu-id="50bb1-132">第一個區段編碼標頭，第二個區段編碼承載，而最後區段則是使用前兩個區段的內容的憑證所計算的簽章。</span><span class="sxs-lookup"><span data-stu-id="50bb1-132">The first section encodes the header, the second the payload, and the last is the signature computed with the certificates from the content of the first two sections.</span></span>
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a><span data-ttu-id="50bb1-133">使用 Azure AD 註冊您的憑證</span><span class="sxs-lookup"><span data-stu-id="50bb1-133">Register your certificate with Azure AD</span></span>
<span data-ttu-id="50bb1-134">若要在 Azure AD 中將憑證認證與用戶端應用程式相關聯，您必須編輯應用程式資訊清單。</span><span class="sxs-lookup"><span data-stu-id="50bb1-134">To associate the certificate credential with the client application in Azure AD, you need to edit the application manifest.</span></span>
<span data-ttu-id="50bb1-135">擁有憑證之後，您必須計算︰</span><span class="sxs-lookup"><span data-stu-id="50bb1-135">Having hold of a certificate, you need to compute:</span></span>
- <span data-ttu-id="50bb1-136">`$base64Thumbprint`，它是憑證雜湊的 base64 編碼</span><span class="sxs-lookup"><span data-stu-id="50bb1-136">`$base64Thumbprint`, which is the base64 encoding of the certificate Hash</span></span>
- <span data-ttu-id="50bb1-137">`$base64Value`，它是憑證未經處理資料的 base64 編碼</span><span class="sxs-lookup"><span data-stu-id="50bb1-137">`$base64Value`, which is the base64 encoding of the certificate raw data</span></span>

<span data-ttu-id="50bb1-138">您也必須提供 GUID 來識別應用程式資訊清單中的金鑰 (`$keyId`)</span><span class="sxs-lookup"><span data-stu-id="50bb1-138">you also need to provide a GUID to identify the key in the application manifest (`$keyId`)</span></span>

<span data-ttu-id="50bb1-139">在適用於用戶端應用程式的 Azure 應用程式註冊中，開啟應用程式資訊清單，然後使用下列結構描述，利用您新的憑證資訊來取代 *keyCredentials* 屬性：</span><span class="sxs-lookup"><span data-stu-id="50bb1-139">In the Azure app registration for the client application, open the application manifest, and replace the *keyCredentials* property with your new certificate information using the following schema:</span></span>
```
"keyCredentials": [
    {
        "customKeyIdentifier": "$base64Thumbprint",
        "keyId": "$keyid",
        "type": "AsymmetricX509Cert",
        "usage": "Verify",
        "value":  "$base64Value"
    }
]
```

<span data-ttu-id="50bb1-140">儲存對應用程式資訊清單所做的編輯，然後上傳至 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="50bb1-140">Save the edits to the application manifest, and upload to Azure AD.</span></span> <span data-ttu-id="50bb1-141">keyCredentials 屬性是多重值，，因此您可能上傳多個憑證以進行更豐富的金鑰管理。</span><span class="sxs-lookup"><span data-stu-id="50bb1-141">The keyCredentials property is multi-valued, so you may upload multiple certificates for richer key management.</span></span>
