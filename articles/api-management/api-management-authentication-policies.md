---
title: "aaaAzure API 管理驗證原則 |Microsoft 文件"
description: "深入了解 hello 可在 Azure API 管理中使用的驗證原則。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 061702a7-3a78-472b-a54a-f3b1e332490d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: ce93cced66cb67520e97c7c15f3685bffb08e1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-authentication-policies"></a>API 管理驗證原則
本主題提供下列 API 管理原則的 hello 的參考。 如需有關新增和設定原則的資訊，請參閱 [API 管理中的原則](http://go.microsoft.com/fwlink/?LinkID=398186)。  
  
##  <a name="AuthenticationPolicies"></a> 驗證原則  
  
-   [使用基本驗證進行驗證](api-management-authentication-policies.md#Basic) - 使用基本驗證來驗證後端服務。  
  
-   [使用用戶端憑證進行驗證](api-management-authentication-policies.md#ClientCertificate) - 使用用戶端憑證來驗證後端服務。  
  
##  <a name="Basic"></a> 使用基本驗證進行驗證  
 使用 hello`authentication-basic`原則 tooauthenticate 使用基本驗證的後端服務。 此原則實際上是設定 hello HTTP 授權標頭 toohello 值 hello 原則中提供對應 toohello 認證。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a>範例  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|authentication-basic|根元素。|是|  
  
### <a name="attributes"></a>屬性  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|username|指定 hello 的 hello 基本認證的使用者名稱。|是|N/A|  
|password|指定 hello 的 hello 基本認證的密碼。|是|N/A|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入  
  
-   **原則範圍︰**API  
  
##  <a name="ClientCertificate"></a> 使用用戶端憑證進行驗證  
 使用 hello`authentication-certificate`原則 tooauthenticate 與後端服務使用用戶端憑證。 hello 憑證必須 toobe[安裝到 API 管理](http://go.microsoft.com/fwlink/?LinkID=511599)第一次，並由其指紋識別。  
  
### <a name="policy-statement"></a>原則陳述式  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a>範例  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a>元素  
  
|名稱|說明|必要|  
|----------|-----------------|--------------|  
|authentication-certificate|根元素。|是|  
  
### <a name="attributes"></a>屬性  
  
|名稱|說明|必要|預設值|  
|----------|-----------------|--------------|-------------|  
|thumbprint|hello hello 用戶端憑證指紋。|是|N/A|  
  
### <a name="usage"></a>使用量  
 此原則可用於下列原則 hello[區段](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections)和[範圍](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes)。  
  
-   **原則區段︰**輸入  
  
-   **原則範圍︰**API  
  

## <a name="next-steps"></a>後續步驟
如需有關使用原則的詳細資訊，請參閱 [API 管理中的原則](api-management-howto-policies.md)。  