---
title: "在 Azure AD 中的 aaaCertificate 認證 |Microsoft 文件"
description: "本文將討論 hello 註冊和使用憑證認證進行應用程式驗證"
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
ms.openlocfilehash: 3508803112ac06268d553db86ab74812aa53e455
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="certificate-credentials-for-application-authentication"></a><span data-ttu-id="fcca1-103">適用於應用程式驗證的憑證認證</span><span class="sxs-lookup"><span data-stu-id="fcca1-103">Certificate credentials for application authentication</span></span>

<span data-ttu-id="fcca1-104">Azure Active Directory 可讓應用程式 toouse 它自己的認證進行驗證，例如 hello OAuth 2.0 用戶端認證授與流程和 hello 代表的資料流程中。</span><span class="sxs-lookup"><span data-stu-id="fcca1-104">Azure Active Directory allows an application toouse its own credentials for authentication, for example, in hello OAuth 2.0 Client Credentials Grant flow and hello On-Behalf-Of flow.</span></span>
<span data-ttu-id="fcca1-105">一種可用形式是認證的 hello 應用程式擁有的憑證簽署的 JSON Web token （jwt） 判斷提示。</span><span class="sxs-lookup"><span data-stu-id="fcca1-105">One form of credential that can be used is a JSON Web Token(JWT) assertion signed with a certificate that hello application owns.</span></span>

## <a name="format-of-hello-assertion"></a><span data-ttu-id="fcca1-106">Hello 判斷提示的格式</span><span class="sxs-lookup"><span data-stu-id="fcca1-106">Format of hello assertion</span></span>
<span data-ttu-id="fcca1-107">toocompute hello 的判斷提示，您可能想 toouse hello 其中許多[JSON Web 權杖](https://jwt.io/)hello 您所選擇的語言中的程式庫。</span><span class="sxs-lookup"><span data-stu-id="fcca1-107">toocompute hello assertion, you probably want toouse one of hello many [JSON Web Token](https://jwt.io/) libraries in hello language of your choice.</span></span> <span data-ttu-id="fcca1-108">hello hello 語彙基元所執行的資訊為：</span><span class="sxs-lookup"><span data-stu-id="fcca1-108">hello information carried by hello token is:</span></span>

#### <a name="header"></a><span data-ttu-id="fcca1-109">標頭</span><span class="sxs-lookup"><span data-stu-id="fcca1-109">Header</span></span>

| <span data-ttu-id="fcca1-110">參數</span><span class="sxs-lookup"><span data-stu-id="fcca1-110">Parameter</span></span> |  <span data-ttu-id="fcca1-111">備註</span><span class="sxs-lookup"><span data-stu-id="fcca1-111">Remark</span></span> |
| --- | --- | --- |
| `alg` | <span data-ttu-id="fcca1-112">應該是 **RS256**</span><span class="sxs-lookup"><span data-stu-id="fcca1-112">Should be **RS256**</span></span> |
| `typ` | <span data-ttu-id="fcca1-113">應該是 **JWT**</span><span class="sxs-lookup"><span data-stu-id="fcca1-113">Should be **JWT**</span></span> |
| `x5t` | <span data-ttu-id="fcca1-114">應該是 hello X.509 憑證 sha-1 指模</span><span class="sxs-lookup"><span data-stu-id="fcca1-114">Should be hello X.509 Certificate SHA-1 thumbprint</span></span> |

#### <a name="claims-payload"></a><span data-ttu-id="fcca1-115">宣告 (承載)</span><span class="sxs-lookup"><span data-stu-id="fcca1-115">Claims (Payload)</span></span>

| <span data-ttu-id="fcca1-116">參數</span><span class="sxs-lookup"><span data-stu-id="fcca1-116">Parameter</span></span> |  <span data-ttu-id="fcca1-117">備註</span><span class="sxs-lookup"><span data-stu-id="fcca1-117">Remark</span></span> |
| --- | --- | --- |
| `aud` | <span data-ttu-id="fcca1-118">對象︰應該是 **https://login.microsoftonline.com/*租用戶 ID*/oauth2/權杖**</span><span class="sxs-lookup"><span data-stu-id="fcca1-118">Audience: Should be **https://login.microsoftonline.com/*tenant_Id*/oauth2/token**</span></span> |
| `exp` | <span data-ttu-id="fcca1-119">到期日： hello hello 權杖過期時的日期。</span><span class="sxs-lookup"><span data-stu-id="fcca1-119">Expiration date: hello date when hello token expires.</span></span> <span data-ttu-id="fcca1-120">hello 次會表示秒數 hello 從 1970 年 1 月 1 日 (1970年-01-01T0:0:0Z) UTC 直到 hello hello 權杖有效時間過期為止。</span><span class="sxs-lookup"><span data-stu-id="fcca1-120">hello time is represented as hello number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until hello time hello token validity expires.</span></span>|
| `iss` | <span data-ttu-id="fcca1-121">發行者： 應該是 hello client_id （hello client 服務的應用程式識別碼）</span><span class="sxs-lookup"><span data-stu-id="fcca1-121">Issuer: should be hello client_id (Application Id of hello client service)</span></span> |
| `jti` | <span data-ttu-id="fcca1-122">GUID: hello JWT 識別碼</span><span class="sxs-lookup"><span data-stu-id="fcca1-122">GUID: hello JWT ID</span></span> |
| `nbf` | <span data-ttu-id="fcca1-123">不能早： hello 日期之前的 hello 權杖不可用。</span><span class="sxs-lookup"><span data-stu-id="fcca1-123">Not Before: hello date before which hello token cannot be used.</span></span> <span data-ttu-id="fcca1-124">hello 次會表示秒數 hello 從 1970 年 1 月 1 日 (1970年-01-01T0:0:0Z) UTC 直到 hello 時間 hello 權杖的發出。</span><span class="sxs-lookup"><span data-stu-id="fcca1-124">hello time is represented as hello number of seconds from January 1, 1970 (1970-01-01T0:0:0Z) UTC until hello time hello token was issued.</span></span> |
| `sub` | <span data-ttu-id="fcca1-125">主旨： 做為`iss`，應該是 hello client_id （hello client 服務的應用程式識別碼）</span><span class="sxs-lookup"><span data-stu-id="fcca1-125">Subject: As for `iss`, should be hello client_id (Application Id of hello client service)</span></span> |

#### <a name="signature"></a><span data-ttu-id="fcca1-126">簽章</span><span class="sxs-lookup"><span data-stu-id="fcca1-126">Signature</span></span>
<span data-ttu-id="fcca1-127">hello 簽章計算 hello 中所述套用 hello 憑證[JSON Web 語彙基元 RFC7519 規格](https://tools.ietf.org/html/rfc7519)</span><span class="sxs-lookup"><span data-stu-id="fcca1-127">hello signature is computed applying hello certificate as described in hello [JSON Web Token RFC7519 specification](https://tools.ietf.org/html/rfc7519)</span></span>

### <a name="example-of-a-decoded-jwt-assertion"></a><span data-ttu-id="fcca1-128">已解碼的 JWT 判斷提示範例</span><span class="sxs-lookup"><span data-stu-id="fcca1-128">Example of a decoded JWT assertion</span></span>
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

### <a name="example-of-an-encoded-jwt-assertion"></a><span data-ttu-id="fcca1-129">已編碼的 JWT 判斷提示範例</span><span class="sxs-lookup"><span data-stu-id="fcca1-129">Example of an encoded JWT assertion</span></span>
<span data-ttu-id="fcca1-130">下列字串 hello 是編碼的判斷提示的範例。</span><span class="sxs-lookup"><span data-stu-id="fcca1-130">hello following string is an example of encoded assertion.</span></span> <span data-ttu-id="fcca1-131">如果您仔細看，會發現三個以點 (.) 分隔的區段。</span><span class="sxs-lookup"><span data-stu-id="fcca1-131">If you look carefully, you notice three sections separated by dots (.).</span></span>
<span data-ttu-id="fcca1-132">hello 第一個區段編碼 hello 標頭，第二個 hello 內容 hello，且 hello 上次 hello hello 憑證 hello 的 hello 前兩個區段的內容中計算所得的簽章。</span><span class="sxs-lookup"><span data-stu-id="fcca1-132">hello first section encodes hello header, hello second hello payload, and hello last is hello signature computed with hello certificates from hello content of hello first two sections.</span></span>
```
"eyJhbGciOiJSUzI1NiIsIng1dCI6Imd4OHRHeXN5amNScUtqRlBuZDdSRnd2d1pJMCJ9.eyJhdWQiOiJodHRwczpcL1wvbG9naW4ubWljcm9zb2Z0b25saW5lLmNvbVwvam1wcmlldXJob3RtYWlsLm9ubWljcm9zb2Z0LmNvbVwvb2F1dGgyXC90b2tlbiIsImV4cCI6MTQ4NDU5MzM0MSwiaXNzIjoiOTdlMGE1YjctZDc0NS00MGI2LTk0ZmUtNWY3N2QzNWM2ZTA1IiwianRpIjoiMjJiM2JiMjYtZTA0Ni00MmRmLTljOTYtNjVkYmQ3MmMxYzgxIiwibmJmIjoxNDg0NTkyNzQxLCJzdWIiOiI5N2UwYTViNy1kNzQ1LTQwYjYtOTRmZS01Zjc3ZDM1YzZlMDUifQ.
Gh95kHCOEGq5E_ArMBbDXhwKR577scxYaoJ1P{a lot of characters here}KKJDEg"
```

### <a name="register-your-certificate-with-azure-ad"></a><span data-ttu-id="fcca1-133">使用 Azure AD 註冊您的憑證</span><span class="sxs-lookup"><span data-stu-id="fcca1-133">Register your certificate with Azure AD</span></span>
<span data-ttu-id="fcca1-134">tooassociate hello 與 Azure AD 中的 hello 用戶端應用程式的憑證認證，您需要 tooedit hello 應用程式資訊清單。</span><span class="sxs-lookup"><span data-stu-id="fcca1-134">tooassociate hello certificate credential with hello client application in Azure AD, you need tooedit hello application manifest.</span></span>
<span data-ttu-id="fcca1-135">您需要保存的憑證，需要 toocompute:</span><span class="sxs-lookup"><span data-stu-id="fcca1-135">Having hold of a certificate, you need toocompute:</span></span>
- <span data-ttu-id="fcca1-136">`$base64Thumbprint`其中是 hello base64 編碼的 hello 憑證雜湊</span><span class="sxs-lookup"><span data-stu-id="fcca1-136">`$base64Thumbprint`, which is hello base64 encoding of hello certificate Hash</span></span>
- <span data-ttu-id="fcca1-137">`$base64Value`其中是 hello base64 編碼的 hello 憑證未經處理資料</span><span class="sxs-lookup"><span data-stu-id="fcca1-137">`$base64Value`, which is hello base64 encoding of hello certificate raw data</span></span>

<span data-ttu-id="fcca1-138">您也需要 tooprovide hello 應用程式資訊清單中的 GUID tooidentify hello 索引鍵 (`$keyId`)</span><span class="sxs-lookup"><span data-stu-id="fcca1-138">you also need tooprovide a GUID tooidentify hello key in hello application manifest (`$keyId`)</span></span>

<span data-ttu-id="fcca1-139">在 hello hello 用戶端應用程式的 Azure 應用程式註冊，開啟 hello 應用程式資訊清單，並取代 hello *keyCredentials*您新的憑證資訊，請使用下列結構描述的 hello 屬性：</span><span class="sxs-lookup"><span data-stu-id="fcca1-139">In hello Azure app registration for hello client application, open hello application manifest, and replace hello *keyCredentials* property with your new certificate information using hello following schema:</span></span>
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

<span data-ttu-id="fcca1-140">儲存 hello 編輯 toohello 應用程式資訊清單，並上傳 tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="fcca1-140">Save hello edits toohello application manifest, and upload tooAzure AD.</span></span> <span data-ttu-id="fcca1-141">hello keyCredentials 屬性是多重值，，因此您可以上傳更豐富的金鑰管理的多個憑證。</span><span class="sxs-lookup"><span data-stu-id="fcca1-141">hello keyCredentials property is multi-valued, so you may upload multiple certificates for richer key management.</span></span>
