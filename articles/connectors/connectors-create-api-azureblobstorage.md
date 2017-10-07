---
title: "aaaAdd hello Azure blob 儲存體邏輯應用程式中的連接器 |Microsoft 文件"
description: "開始使用和設定邏輯應用程式中的 hello Azure blob 儲存體連接器"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5dc3f75-6bea-420b-b250-183668d2848d
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/02/2017
ms.author: mandia; ladocs
ms.openlocfilehash: add61287ef1b2228ef9d3f54ce082807bad6858b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-blob-storage-connector-in-a-logic-app"></a>在邏輯應用程式中使用 hello Azure blob 儲存體連接器
使用 hello Azure Blob 儲存體連接器 tooupload，更新、 取得，並刪除 blob 儲存體帳戶，全部都在邏輯應用程式中。  

您可以利用 Azure Blob 儲存體來：

* 上傳新專案或取得最近更新的檔案以建置工作流程。
* 使用動作 tooget 檔案中繼資料，請刪除檔案、 複製檔案等等。 例如，當 Azure 網站中的工具更新時 (觸發程序)，便更新 Blob 儲存體中的檔案 (動作)。 

本主題說明如何 toouse hello blob 儲存體邏輯應用程式中的連接器。

toolearn 進一步了解邏輯應用程式，請參閱[為何的 logic apps](../logic-apps/logic-apps-what-are-logic-apps.md)和[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。

toolearn 進一步了解邏輯應用程式，請參閱[為何的 logic apps](../logic-apps/logic-apps-what-are-logic-apps.md)和[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。

## <a name="connect-tooazure-blob-storage"></a>連接 tooAzure blob 儲存體
邏輯應用程式可以存取任何服務之前，您先建立*連接*toohello 服務。 連線可讓邏輯應用程式與另一個服務連線。 例如，tooconnect tooa 儲存體帳戶，您先建立 blob 儲存體*連接*。 toocreate 連接，輸入您平常用 tooaccess hello 服務，您所連接的 hello 認證。 Azure 儲存體，因此輸入 hello 認證 tooyour 儲存體帳戶 toocreate hello 連接。 

#### <a name="create-hello-connection"></a>建立 hello 連線
> [!INCLUDE [Create a connection tooAzure blob storage](../../includes/connectors-create-api-azureblobstorage.md)]

## <a name="use-a-trigger"></a>使用觸發程序
此連接器並沒有任何觸發程序。 使用其他觸發程序 toostart hello 邏輯應用程式，例如循環觸發程序、 HTTP Webhook 觸發程序、 觸發程序適用於其他連接器，等等。 [建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md) 可提供範例。

## <a name="use-an-action"></a>使用動作
動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。

1. 選取加號 hello。 您會看到幾個選擇：**將動作加入**，**加入條件**，或其中一個 hello**詳細**選項。
   
    ![](./media/connectors-create-api-azureblobstorage/add-action.png)
2. 選擇 [新增動作] 。
3. 在 [hello] 文字方塊中，輸入"blob"tooget 所有 hello 可用動作的清單。
   
    ![](./media/connectors-create-api-azureblobstorage/actions.png) 
4. 在我們的範例中，選擇 [AzureBlob - 使用路徑取得檔案中繼資料]。 如果連接已存在，然後選取 hello **...**按鈕 tooselect 檔案 （顯示選擇器）。
   
    ![](./media/connectors-create-api-azureblobstorage/sample-file.png)
   
    如果系統提示您輸入 hello 連接資訊，然後輸入 hello 詳細資料 toocreate hello 連接。 [建立 hello 連接](connectors-create-api-azureblobstorage.md#create-the-connection)本主題說明這些屬性。 
   
   > [!NOTE]
   > 在此範例中，我們可以得到 hello 中繼資料的檔案。 toosee hello 中繼資料，並將另一個動作，建立新的檔案，使用另一個連接器。 例如，加入建立 hello 中繼資料為基礎的新 「 測試 」 檔案的 OneDrive 動作。 


5. **儲存**您的變更 （hello 工具列的左上的角）。 邏輯應用程式將會儲存，而且可能會自動啟用。

> [!TIP]
> [儲存體總管](http://storageexplorer.com/)是很棒的工具太管理多個儲存體帳戶。

## <a name="connector-specific-details"></a>連接器特定的詳細資料

檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/azureblobconnector/)。 

## <a name="next-steps"></a>後續步驟
[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。 瀏覽 hello 在邏輯應用程式中其他可用的連接器我們[Api 清單](apis-list.md)。

