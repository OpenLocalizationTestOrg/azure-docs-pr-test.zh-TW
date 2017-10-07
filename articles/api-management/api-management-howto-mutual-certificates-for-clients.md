---
title: "aaaSecure 應用程式開發介面使用 API 管理的 Azure API 管理中的用戶端憑證驗證 |Microsoft 文件"
description: "了解如何 toosecure 存取 tooAPIs 使用用戶端憑證"
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
ms.openlocfilehash: 6ff78bda3d429829da79d0dc4d652f19669cc919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toosecure-apis-using-client-certificate-authentication-in-api-management"></a>如何 toosecure 應用程式開發介面使用用戶端憑證驗證在 API 管理

API 管理提供 hello 功能 toosecure 存取 tooAPIs (亦即，用戶端 tooAPI 管理) 使用用戶端憑證。 目前，您可以檢查 hello 的用戶端憑證指紋針對想要的值。 您也可以檢查 hello 指紋針對現有的憑證上傳 tooAPI 管理。  

如需保護存取 toohello 後端服務使用用戶端憑證 （亦即，API 管理 tooback 端） API 的資訊，請參閱[toosecure 後端服務使用用戶端憑證驗證的方式](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)

## <a name="checking-hello-expiration-date"></a>檢查 hello 到期日

下列原則可以設定的 toocheck 如果 hello 憑證已過期：

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.NotAfter < DateTime.Now)" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-issuer-and-subject"></a>檢查 hello 簽發者和主旨

下列原則可以設定的 toocheck hello 簽發者和用戶端憑證的主體：

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Issuer != "trusted-issuer" || context.Request.Certificate.SubjectName != "expected-subject-name")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-hello-thumbprint"></a>檢查 hello 指紋

下列原則可以設定的 toocheck hello 用戶端憑證指紋：

```
<choose>
    <when condition="@(context.Request.Certificate == null || context.Request.Certificate.Thumbprint != "desired-thumbprint")" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>
```

## <a name="checking-a-thumbprint-against-certificates-uploaded-tooapi-management"></a>檢查針對憑證的指紋上, 傳 tooAPI 管理

hello 下列範例顯示如何 toocheck hello 指紋的憑證對用戶端憑證上傳 tooAPI 管理： 

```
<choose>
    <when condition="@(context.Request.Certificate == null || !context.Deployment.Certificates.Any(c => c.Value.Thumbprint == context.Request.Certificate.Thumbprint))" >
        <return-response>
            <set-status code="403" reason="Invalid client certificate" />
        </return-response>
    </when>
</choose>

```

## <a name="next-step"></a>後續步驟

*  [如何 toosecure 後端服務使用用戶端憑證驗證](https://docs.microsoft.com/en-us/azure/api-management/api-management-howto-mutual-certificates)
*  [如何 tooupload 憑證](https://docs.microsoft.com/azure/api-management/api-management-howto-mutual-certificates#a-namestep1-aupload-a-client-certificate)

