---
title: "aaaCall REST 端點，其中包含 HTTP + Swagger Azure 邏輯應用程式連接器 |Microsoft 文件"
description: "從邏輯應用程式透過 Swagger hello HTTP + Swagger 連接器連接 tooREST 端點"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
tags: connectors
ms.assetid: eccfd87c-c5fe-4cf7-b564-9752775fd667
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan; LADocs
ms.openlocfilehash: baaa57689ff41fcd052f9d86086e36619ddec46e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-http--swagger-action"></a>開始使用 hello HTTP + Swagger 動作

您可以建立第一級連接器 tooany REST 端點，透過[Swagger 文件](https://swagger.io)當邏輯應用程式工作流程中使用 hello HTTP + Swagger 動作。 您也可以擴充邏輯應用程式 toocall 第一級的邏輯應用程式的設計工具經驗的任何 REST 端點。

如何 toocreate 邏輯應用程式使用連接器，請參閱的 toolearn[建立新的邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。

## <a name="use-http--swagger-as-a-trigger-or-an-action"></a>使用 HTTP + Swagger 做為觸發程序或動作

hello HTTP + Swagger 觸發程序和動作的工作會將相同 hello 與 hello [HTTP 動作](connectors-native-http.md)但提供較佳的體驗，在邏輯應用程式的設計工具中，藉由公開 hello API 結構和輸出 hello [Swagger 中繼資料](https://swagger.io). 您也可以使用 hello HTTP + Swagger 連接器的觸發程序。 如果您想 tooimplement 輪詢觸發程序，請依照下列所述的 hello 輪詢模式[邏輯應用程式從其他應用程式開發介面、 服務和系統建立自訂的應用程式開發介面 toocall](../logic-apps/logic-apps-create-api-app.md#polling-triggers)。

深入了解 [邏輯應用程式觸發程序和動作](connectors-overview.md)。

以下是如何 toouse hello HTTP + Swagger 範例操作，因為邏輯應用程式中的工作流程中的動作。

1. 選取 hello**新步驟** 按鈕。
2. 選取 [新增動作] 。
3. 在 hello 動作搜尋方塊中，輸入**swagger** toolist hello HTTP + Swagger 動作。
   
    ![選取 HTTP + Swagger 動作](./media/connectors-native-http-swagger/using-action-1.png)
4. 輸入 hello Swagger 文件的 URL:
   
   * toowork 從 hello 邏輯應用程式的設計工具，hello URL 必須是 HTTPS 端點，並啟用 CORS。
   * 如果 hello Swagger 文件不符合此需求，您可以使用[Azure 儲存體與啟用 CORS](#hosting-swagger-from-storage) toostore hello 文件。
5. 按一下**下一步**tooread 和轉譯來自 hello Swagger 文件。
6. 新增任何所需的 hello HTTP 呼叫的參數。
   
    ![完成 HTTP 動作](./media/connectors-native-http-swagger/using-action-2.png)
7. toosave 及發行應用程式邏輯，請按一下**儲存**設計工具工具列上。

### <a name="host-swagger-from-azure-storage"></a>從 Azure 儲存體託管 Swagger
您可能想 tooreference Swagger 文件所未裝載，或不符合 hello hello 設計工具的安全性和跨原始需求。 tooresolve 這個問題，您可以在 Azure 儲存體中儲存 hello Swagger 文件，並啟用 CORS tooreference hello 文件。  

以下是 hello 步驟 toocreate、 設定和 Swagger 文件儲存在 Azure 儲存體：

1. [使用 Azure Blob 儲存體建立 Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md) tooperform 這步驟，設定權限太**公用存取**。

2. 啟用 CORS hello blob 上。 

   tooautomatically 設定此設定，您可以使用[這個 PowerShell 指令碼](https://github.com/logicappsio/EnableCORSAzureBlob/blob/master/EnableCORSAzureBlob.ps1)。

3. Hello Swagger 檔案 toohello blob 上傳。 

   您可以執行此步驟中，從 hello [Azure 入口網站](https://portal.azure.com)或從這類工具[Azure 儲存體總管](http://storageexplorer.com/)。

4. 參考 Azure Blob 儲存體中的 HTTPS 連結 toohello 文件。 

   hello 連結會使用此格式：

   `https://*storageAccountName*.blob.core.windows.net/*container*/*filename*`

## <a name="technical-details"></a>技術詳細資訊
以下是 hello 詳細資料 hello 觸發程序和動作這個 HTTP + Swagger 連接器支援。

## <a name="http--swagger-triggers"></a>HTTP + Swagger 觸發程序
觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中所定義的事件。 [深入了解觸發程序。](connectors-overview.md) hello HTTP + Swagger 連接器有一個觸發程序。

| 觸發程序 | 說明 |
| --- | --- |
| HTTP + Swagger |進行 HTTP 呼叫，並傳回 hello 回應內容 |

## <a name="http--swagger-actions"></a>HTTP + Swagger 動作
動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。 [深入了解動作。](connectors-overview.md) hello HTTP + Swagger 連接器有一個可能的動作。

| 動作 | 說明 |
| --- | --- |
| HTTP + Swagger |進行 HTTP 呼叫，並傳回 hello 回應內容 |

### <a name="action-details"></a>動作詳細資料
hello HTTP + Swagger 連接器隨附一個可能的動作。 以下是每個 hello 動作、 必要和選擇性的輸入的欄位以及 hello 對應及其使用狀況與相關聯的輸出詳細資料的相關資訊。

#### <a name="http--swagger"></a>HTTP + Swagger
在 Swagger 中繼資料的協助下提出 HTTP 輸出要求。
星號 (*) 表示必要的欄位。

| 顯示名稱 | 屬性名稱 | 說明 |
| --- | --- | --- |
| 方法 * |method |HTTP 指令動詞 toouse。 |
| URI* |uri |Hello HTTP 要求的 URI。 |
| headers |headers |HTTP 標頭 tooinclude JSON 物件。 |
| 內文 |body |hello HTTP 要求主體。 |
| 驗證 |驗證 |要求的驗證 toouse。 如需詳細資訊，請參閱 hello [HTTP 連接器](connectors-native-http.md#authentication)。 |

**輸出詳細資料**

HTTP 回應

| 屬性名稱 | 資料類型 | 說明 |
| --- | --- | --- |
| headers |物件 |回應標頭 |
| 內文 |物件 |回應物件 |
| Status Code |整數 |HTTP 狀態碼 |

### <a name="http-responses"></a>HTTP 回應
呼叫 toovarious 動作時，您可能會收到特定的回應。 下表概述對應的回應及說明。

| 名稱 | 說明 |
| --- | --- |
| 200 |OK |
| 202 |已接受 |
| 400 |不正確的要求 |
| 401 |未經授權 |
| 403 |禁止 |
| 404 |找不到 |
| 500 |內部伺服器錯誤。 發生未知錯誤。 |

- - -
## <a name="next-steps"></a>後續步驟

* [建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)
* [尋找其他連接器](apis-list.md)