---
title: "aaaAzure API 管理頁面控制項 |Microsoft 文件"
description: "深入了解適用於在 Azure API 管理開發人員入口網站範本中所使用的 hello 頁面控制項。"
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 03e0ac8d-64ff-4e9a-b029-d7be14fb31e3
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 1a16a6fce197c0a2e14807ac21e81a9a73b515b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-page-controls"></a>Azure API 管理的頁面控制項
Azure API 管理提供 hello hello 開發人員入口網站範本中所使用的控制項。  
  
 toouse 控制項，將它放在預期的 hello 位置 hello 開發人員入口網站範本中。 某些控制項，例如 hello[應用程式動作](#app-actions)控制項，具有參數，hello 下列範例所示。  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
 hello hello 參數值傳入 hello 範本的 hello 資料模型的一部分。 在大部分情況下，您可以只要貼在 hello 範例的每個控制項為它提供 toowork 正確。 如需有關 hello 參數值的詳細資訊，您可以看到每個範本可能可使用之控制項的 hello 資料模型區段。  
  
 如需有關使用範本的詳細資訊，請參閱[toocustomize hello API 管理開發人員入口網站使用範本的方式](https://azure.microsoft.com/documentation/articles/api-management-developer-portal-templates/)。  
  
## <a name="developer-portal-template-page-controls"></a>開發人員入口網站範本頁面控制項  
  
-   [app-actions](#app-actions)  
  
-   [basic-signin](#basic-signin)  
  
-   [paging-control](#paging-control)  
  
-   [提供者](#providers)  
  
-   [search-control](#search-control)  
  
-   [sign-up](#sign-up)  
  
-   [subscribe-button](#subscribe-button)  
  
-   [subscription-cancel](#subscription-cancel)  
  
##  <a name="app-actions"></a>app-actions  
 hello`app-actions`控制項可提供使用者介面與 hello 開發人員入口網站中的 hello 使用者設定檔頁面上的應用程式互動。  
  
 ![app&#45;actions 控制項](./media/api-management-page-controls/APIM-app-actions-control.png "APIM app-actions 控制項")  
  
### <a name="usage"></a>使用量  
  
```xml  
<app-actions params="{ appId: '{{app.id}}' }"></app-actions>  
```  
  
### <a name="parameters"></a>參數  
  
|參數|說明|  
|---------------|-----------------|  
|appId|hello hello 應用程式識別碼。|  
  
### <a name="developer-portal-templates"></a>開發人員入口網站範本  
 hello `app-actions` hello 遵循開發人員入口網站的範本可用來控制。  
  
-   [應用程式](api-management-user-profile-templates.md#Applications)  
  
##  <a name="basic-signin"></a>basic-signin  
 hello`basic-signin`控制項提供的控制項，如收集的使用者登入資訊在 hello 登入 hello 開發人員入口網站中的頁面。  
  
 ![basic&#45;signin 控制項](./media/api-management-page-controls/APIM-basic-signin-control.png "APIM basic-signin 控制項")  
  
### <a name="usage"></a>使用量  
  
```xml  
<basic-SignIn></basic-SignIn>  
```  
  
### <a name="parameters"></a>參數  
 無。  
  
### <a name="developer-portal-templates"></a>開發人員入口網站範本  
 hello `basic-signin` hello 遵循開發人員入口網站的範本可用來控制。  
  
-   [登入](api-management-page-templates.md#SignIn)  
  
##  <a name="paging-control"></a>paging-control  
 hello`paging-control`提供開發人員入口網站頁面顯示項目清單的分頁功能。  
  
 ![分頁控制項](./media/api-management-page-controls/APIM-paging-control.png "APIM 分頁控制項")  
  
### <a name="usage"></a>使用量  
  
```xml  
<paging-control></paging-control>  
```  
  
### <a name="parameters"></a>參數  
 無。  
  
### <a name="developer-portal-templates"></a>開發人員入口網站範本  
 hello `paging-control` hello 遵循開發人員入口網站的範本可用來控制。  
  
-   [API 清單](api-management-api-templates.md#APIList)  
  
-   [問題清單](api-management-issue-templates.md#IssueList)  
  
-   [產品清單](api-management-product-templates.md#ProductList)  
  
##  <a name="providers"></a>providers  
 hello`providers`控制項提供的驗證提供者在 hello 登入 hello 開發人員入口網站中的頁面中選取的控制項。  
  
 ![提供者控制項](./media/api-management-page-controls/APIM-providers-control.png "APIM 提供者控制項")  
  
### <a name="usage"></a>使用量  
  
```xml  
<providers></providers>  
```  
  
### <a name="parameters"></a>參數  
 無。  
  
### <a name="developer-portal-templates"></a>開發人員入口網站範本  
 hello `providers` hello 遵循開發人員入口網站的範本可用來控制。  
  
-   [登入](api-management-page-templates.md#SignIn)  
  
##  <a name="search-control"></a>search-control  
 hello`search-control`提供開發人員入口網站頁面顯示項目清單的搜尋功能。  
  
 ![搜尋控制項](./media/api-management-page-controls/APIM-search-control.png "APIM 搜尋控制項")  
  
### <a name="usage"></a>使用量  
  
```xml  
<search-control></search-control>  
```  
  
### <a name="parameters"></a>參數  
 無。  
  
### <a name="developer-portal-templates"></a>開發人員入口網站範本  
 hello `search-control` hello 遵循開發人員入口網站的範本可用來控制。  
  
-   [API 清單](api-management-api-templates.md#APIList)  
  
-   [產品清單](api-management-product-templates.md#ProductList)  
  
##  <a name="sign-up"></a>sign-up  
 hello`sign-up`控制項提供控制項，以收集 hello 註冊 頁面中 hello 開發人員入口網站中的使用者設定檔資訊。  
  
 ![註冊控制項](./media/api-management-page-controls/APIM-sign-up-control.png "APIM 註冊控制項")  
  
### <a name="usage"></a>使用量  
  
```xml  
<sign-up></sign-up>  
```  
  
### <a name="parameters"></a>參數  
 無。  
  
### <a name="developer-portal-templates"></a>開發人員入口網站範本  
 hello `sign-up` hello 遵循開發人員入口網站的範本可用來控制。  
  
-   [註冊](api-management-page-templates.md#SignUp)  
  
##  <a name="subscribe-button"></a>subscribe-button  
 hello`subscribe-button`訂閱使用者 tooa 產品提供的控制項。  
  
 ![subscribe&#45;button 控制項](./media/api-management-page-controls/APIM-subscribe-button-control.png "APIM subscribe-button 控制項")  
  
### <a name="usage"></a>使用量  
  
```xml  
<subscribe-button></subscribe-button>  
```  
  
### <a name="parameters"></a>參數  
 無。  
  
### <a name="developer-portal-templates"></a>開發人員入口網站範本  
 hello `subscribe-button` hello 遵循開發人員入口網站的範本可用來控制。  
  
-   [產品](api-management-product-templates.md#Product)  
  
##  <a name="subscription-cancel"></a>subscription-cancel  
 hello`subscription-cancel`控制項取消訂閱 tooa 產品 hello 開發人員入口網站中的 hello 使用者設定檔頁面中提供的控制項。  
  
 ![subscription&#45;cancel 控制項](./media/api-management-page-controls/APIM-subscription-cancel-control.png "APIM subscription-cancel 控制項")  
  
### <a name="usage"></a>使用量  
  
```xml  
<subscription-cancel params="{ subscriptionId: '{{subscription.id}}', cancelUrl: '{{subscription.cancelUrl}}' }">  
</subscription-cancel>  
  
```  
  
### <a name="parameters"></a>參數  
  
|參數|說明|  
|---------------|-----------------|  
|subscriptionId|hello 訂用帳戶 toocancel hello 識別碼。|  
|cancelUrl|hello 訂用帳戶取消 URL。|  
  
### <a name="developer-portal-templates"></a>開發人員入口網站範本  
 hello `subscription-cancel` hello 遵循開發人員入口網站的範本可用來控制。  
  
-   [產品](api-management-product-templates.md#Product)

## <a name="next-steps"></a>後續步驟
如需有關使用範本的詳細資訊，請參閱[toocustomize hello API 管理開發人員入口網站使用範本的方式](api-management-developer-portal-templates.md)。
