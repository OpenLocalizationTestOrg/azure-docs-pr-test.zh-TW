---
title: "匯入 aaaRestrictions 和 Azure API 管理 API 中的已知的問題 |Microsoft 文件"
description: "已知的問題與已匯入至 Azure API 管理使用 hello 開啟應用程式開發介面、 WSDL 或 WADL 格式的限制的詳細資料。"
services: api-management
documentationcenter: 
author: mattfarm
manager: vlvinogr
editor: 
ms.assetid: 7a5a63f0-3e72-49d3-a28c-1bb23ab495e2
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: apipm
ms.openlocfilehash: 0bed5ace47de6ccbfbecba25ea6b69c5329de089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="api-import-restrictions-and-known-issues"></a>API 匯入的限制和已知問題
## <a name="about-this-list"></a>關於本清單
雖然盡量 tooensure 所匯入 Azure API 管理您的應用程式開發介面的緊密性，且沒問題的越好，我們不要偶爾會強制限制或識別會需要 toobe 可以成功匯入之前修正的問題。 本文記載這些 organised hello 匯入格式的 hello 應用程式開發介面。

## <a name="open-api"> </a>Open API/Swagger
一般情況下，如果您收到錯誤匯入文件開啟的 API，請確認您已驗證-使用 hello 設計工具中的 hello 新版 Azure 入口網站 （設計-Front End-開啟應用程式開發介面規格編輯器），或第 3 與合作對象工具例如<a href="http://www.swagger.io">Swagger 編輯器</a>。

* **主機名稱** - 我們需要主機名稱屬性。
* **基本路徑** - 我們需要基本路徑屬性。
* **配置** - 我們需要配置陣列。 

## <a name="wsdl"> </a>WSDL
WSDL 檔案使用的 toogenerate SOAP 傳遞 Api，或做為 hello SOAP-REST API 的後端。

* **WSDL:Import** - 我們目前不支援使用這個屬性的 API。 客戶應該匯入的 hello 元素合併成一份文件中。
* **具有多個部分的訊息** - 目前不支援。
* **WCF wsHttpBinding** 使用 Windows Communication Foundation 建立的 SOAP 服務應該使用 basicHttpBinding - 不支援 wsHttpBinding。
* **MTOM** - 使用 MTOM 的服務「可能」<em></em>可以運作。 目前不提供官方支援。
* **遞迴**類型定義以遞迴方式 （例如，請參閱 tooan 陣列本身） 不支援。

## <a name="wadl"> </a>WADL
目前沒有任何已知的 WADL 匯入問題。


[api-management-management-console]: ./media/api-management-howto-add-operations/api-management-management-console.png
[api-management-operations]: ./media/api-management-howto-add-operations/api-management-operations.png
[api-management-add-operation]: ./media/api-management-howto-add-operations/api-management-add-operation.png
[api-management-http-method]: ./media/api-management-howto-add-operations/api-management-http-method.png
[api-management-url-template]: ./media/api-management-howto-add-operations/api-management-url-template.png
[api-management-url-template-rewrite]: ./media/api-management-howto-add-operations/api-management-url-template-rewrite.png
[api-management-description]: ./media/api-management-howto-add-operations/api-management-description.png
[api-management-caching-tab]: ./media/api-management-howto-add-operations/api-management-caching-tab.png
[api-management-request-parameters]: ./media/api-management-howto-add-operations/api-management-request-parameters.png
[api-management-request-body]: ./media/api-management-howto-add-operations/api-management-request-body.png
[api-management-response-code]: ./media/api-management-howto-add-operations/api-management-response-code.png
[api-management-response-body-content-type]: ./media/api-management-howto-add-operations/api-management-response-body-content-type.png
[api-management-response-body]: ./media/api-management-howto-add-operations/api-management-response-body.png


[api-management-contoso-api]: ./media/api-management-howto-add-operations/api-management-contoso-api.png

[api-management-add-new-api]: ./media/api-management-howto-add-operations/api-management-add-new-api.png
[api-management-api-settings]: ./media/api-management-howto-add-operations/api-management-api-settings.png
[api-management-api-settings-credentials]: ./media/api-management-howto-add-operations/api-management-api-settings-credentials.png
[api-management-api-summary]: ./media/api-management-howto-add-operations/api-management-api-summary.png
[api-management-echo-operations]: ./media/api-management-howto-add-operations/api-management-echo-operations.png

[Add an operation]: #add-operation
[Operation caching]: #operation-caching
[Request parameters]: #request-parameters
[Request body]: #request-body
[Responses]: #responses
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocache operation results in Azure API Management]: api-management-howto-cache.md
