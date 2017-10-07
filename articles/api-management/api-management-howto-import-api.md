---
title: "Azure API 管理的應用程式開發介面 aaaImport |Microsoft 文件"
description: "深入了解如何 tooimport API 和 Azure API 管理其作業。"
services: api-management
documentationcenter: 
author: steved0x
manager: erikre
editor: 
ms.assetid: 40398b0a-ac2c-43f0-89e1-07e4abbf502f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 20fbbb53243aecc24d72833ec0904ae8fab97863
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooimport-hello-definition-of-an-api-with-operations-in-azure-api-management"></a>如何 tooimport hello Azure API 管理中的作業的應用程式開發介面的定義
在 API 管理中，可以建立新的 Api，並手動新增的 hello 作業或 hello API 可以匯入以及 hello 作業在一個步驟中。

應用程式開發介面和其作業可以使用匯入下列格式的 hello。

* WADL
* Swagger

本指南示範如何在一個步驟中建立新的 API 並匯入其操作。 如需手動建立應用程式開發介面，並將作業加入資訊，請參閱[如何 toocreate Api] [ How toocreate APIs]和[如何 tooadd 作業 tooan API] [ How tooadd operations tooan API].

## <a name="import-api"> </a>匯入 API
建立並設定在 hello 發行者入口網站應用程式開發介面。 tooaccess hello 發行者入口網站中，按一下**發行者入口網站**API 管理服務的 hello Azure 入口網站中。 如果您尚未建立 API 管理服務執行個體，請參閱[建立 API 管理服務執行個體][ Create an API Management service instance]在 hello[開始使用 Azure API 管理][Get started with Azure API Management]教學課程。

![發行者入口網站][api-management-management-console]

按一下**Api**從 hello **API 管理**hello 左、，然後按一下功能表**匯入 API**。

![Import API][api-management-import-apis]

hello**匯入 API**視窗有對應 toohello 三種方式 tooprovide hello API 規格的三個索引標籤。

* **從剪貼簿**可讓您在 hello 指定的文字方塊的 toopaste hello API 規格。
* **從檔案**可讓您包含 hello API 規格的 toobrowse tooand 選取 hello 檔案。
* **從 URL** toosupply hello URL toohello 規格 hello API 可讓您。

![Import API format][api-management-import-api-clipboard]

提供 hello API 規格之後, 使用 hello 圓鈕 hello 右 tooindicate hello 規格格式。 支援下列格式的 hello。

* WADL
* Swagger

接下來，輸入 [Web API URL 尾碼] 。 這是您的 API 管理服務的附加的 toohello 基底 URL。 hello 基底 URL 是很常見的 API 管理服務的每個執行個體上裝載的所有 Api。 API 管理它們的後置字元來區分應用程式開發介面，因此 hello 後置字元必須是唯一的特定 API 管理服務執行個體中的每一種 API。

輸入所有的值，當按一下**儲存**toocreate hello API 和 hello 相關聯的作業。 

> [!NOTE]
> 如需以 Swagger 格式匯入基本計算機 API 的教學課程，請參閱 [在 Azure API 管理中管理您的第一個 API](api-management-get-started.md)。
> 
> 

## <a name="export-api"> </a> 匯出 API
加法 tooimporting 中新的 Api，您可以從 hello 發行者入口網站匯出您的應用程式開發介面的 hello 定義。 toodo，請按一下**匯出應用程式開發介面**從 hello**摘要 索引標籤**的您**API**。

![Export API][api-management-export-api]

您可以使用 WADL 或 Swagger 來匯出 API。 選取 hello 所要的格式，請按一下**儲存**，並選擇哪些 toosave hello 檔案中的 hello 位置。

![Export API format][api-management-export-api-format]

## <a name="next-steps"> </a>後續步驟
一旦建立應用程式開發介面，並匯入的 hello 作業，您可以檢閱並設定任何其他設定，hello API tooa 產品，加上發佈，讓開發人員使用。 如需詳細資訊，請參閱下列指南中的 hello。

* [如何設定 tooconfigure 應用程式開發介面][How tooconfigure API settings]
* [如何 toocreate 及發佈產品][How toocreate and publish a product]

[api-management-management-console]: ./media/api-management-howto-import-api/api-management-management-console.png
[api-management-import-apis]: ./media/api-management-howto-import-api/api-management-api-import-apis.png
[api-management-import-api-clipboard]: ./media/api-management-howto-import-api/api-management-import-api-wizard.png
[api-management-export-api]: ./media/api-management-howto-import-api/api-management-export-api.png
[api-management-export-api-format]: ./media/api-management-howto-import-api/api-management-export-api-format.png

[Import an API]: #import-api
[Export an API]: #export-api
[Configure API settings]: #configure-api-settings
[Next steps]: #next-steps

[Get started with Azure API Management]: api-management-get-started.md
[Create an API Management service instance]: api-management-get-started.md#create-service-instance

[How tooadd operations tooan API]: api-management-howto-add-operations.md
[How toocreate and publish a product]: api-management-howto-add-products.md
[How toocreate APIs]: api-management-howto-create-apis.md
[How tooconfigure API settings]: api-management-howto-create-apis.md#configure-api-settings
