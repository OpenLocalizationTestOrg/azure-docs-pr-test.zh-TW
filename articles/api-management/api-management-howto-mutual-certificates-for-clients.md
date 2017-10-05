---
title: "使用 API 管理中的用戶端憑證驗證保護 API - Azure API 管理 | Microsoft Docs"
description: "了解如何使用用戶端憑證來保護對 API 的存取"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/01/2017
ms.author: apimpm
ms.openlocfilehash: d3d51d0575a6d2dacced931601d48eb1e51a4051
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-secure-apis-using-client-certificate-authentication-in-api-management"></a><span data-ttu-id="48547-103">如何使用 API 管理中的用戶端憑證驗證保護 API</span><span class="sxs-lookup"><span data-stu-id="48547-103">How to secure APIs using client certificate authentication in API Management</span></span>

<span data-ttu-id="48547-104">API 管理提供以用戶端憑證保護對 API 之存取 (例如，用戶端對 API 管理) 的功能。</span><span class="sxs-lookup"><span data-stu-id="48547-104">API Management provides the capability to secure access to APIs (i.e., client to API Management) using client certificates.</span></span> <span data-ttu-id="48547-105">目前，您可以檢查用戶端憑證的指紋是否符合想要的值。</span><span class="sxs-lookup"><span data-stu-id="48547-105">Currently, you can check the thumbprint of a client certificate against a desired value.</span></span> <span data-ttu-id="48547-106">您也可以檢查指紋是否符合已上傳到 API 管理的現有憑證。</span><span class="sxs-lookup"><span data-stu-id="48547-106">You can also check the thumbprint against existing certificates uploaded to API Management.</span></span>  

<span data-ttu-id="48547-107">如需有關如何使用用戶端憑證保護對 API 後端服務之存取 (例如，API 管理到後端) 的資訊，請參閱[如何使用用戶端憑證驗證來保護後端服務](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span><span class="sxs-lookup"><span data-stu-id="48547-107">For information about securing access to the back-end service of an API using client certificates (i.e., API Management to back-end), see [How to secure back-end services using client certificate authentication](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)</span></span>

## <a name="checking-the-expiration-date"></a><span data-ttu-id="48547-108">檢查到期日</span><span class="sxs-lookup"><span data-stu-id="48547-108">Checking the expiration date</span></span>

<span data-ttu-id="48547-109">您可以設定下面的原則來檢查憑證是否已到期：</span><span class="sxs-lookup"><span data-stu-id="48547-109">Below policies can be configured to check if the certificate is expired:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-the-issuer-and-subject"></a><span data-ttu-id="48547-110">檢查簽發者和主旨</span><span class="sxs-lookup"><span data-stu-id="48547-110">Checking the issuer and subject</span></span>

<span data-ttu-id="48547-111">您可以設定下面的原則來檢查用戶端憑證的簽發者和主旨：</span><span class="sxs-lookup"><span data-stu-id="48547-111">Below policies can be configured to check the issuer and subject of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-the-thumbprint"></a><span data-ttu-id="48547-112">檢查指紋</span><span class="sxs-lookup"><span data-stu-id="48547-112">Checking the thumbprint</span></span>

<span data-ttu-id="48547-113">您可以設定下面的原則來檢查用戶端憑證的指紋：</span><span class="sxs-lookup"><span data-stu-id="48547-113">Below policies can be configured to check the thumbprint of a client certificate:</span></span>

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-to-api-management"></a><span data-ttu-id="48547-114">檢查指紋是否符合已上傳到 API 管理的憑證</span><span class="sxs-lookup"><span data-stu-id="48547-114">Checking a thumbprint against certificates uploaded to API Management</span></span>

<span data-ttu-id="48547-115">下列範例說明如何檢查用戶端憑證的指紋是否符合已上傳到 API 管理的憑證：</span><span class="sxs-lookup"><span data-stu-id="48547-115">The following example shows how to check the thumbprint of a client certificate against certificates uploaded to API Management:</span></span> 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a><span data-ttu-id="48547-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="48547-116">Next step</span></span>

*  [<span data-ttu-id="48547-117">如何使用用戶端憑證驗證來保護後端服務</span><span class="sxs-lookup"><span data-stu-id="48547-117">How to secure back-end services using client certificate authentication</span></span>](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [<span data-ttu-id="48547-118">如何上傳憑證</span><span class="sxs-lookup"><span data-stu-id="48547-118">How to upload certificates</span></span>](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

