---
title: "aaaLearn toouse hello SFTP 連接器邏輯應用程式中的方式 |Microsoft 文件"
description: "使用 Azure App Service 建立邏輯應用程式。 連接 tooSFTP API toosend 及接收檔案。 您可以執行各種作業，例如建立、更新、取得或刪除檔案。"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/20/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3f50570191c9b9339fe6584b9056b2549512b789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sftp-connector"></a>開始使用 hello SFTP 連接器
使用 hello SFTP 連接器 tooaccess SFTP 帳戶 toosend 及接收檔案。 您可以執行各種作業，例如建立、更新、取得或刪除檔案。  

toouse[任何連接器](apis-list.md)，您必須先 toocreate 邏輯應用程式。 您可以從[立即建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)來開始。

## <a name="connect-toosftp"></a>連接 tooSFTP
邏輯應用程式可以存取任何服務之前，您首先需要 toocreate*連接*toohello 服務。 [連線](connectors-overview.md)可讓邏輯應用程式與另一個服務連線。  

### <a name="create-a-connection-toosftp"></a>建立連接 tooSFTP
> [!INCLUDE [Steps toocreate a connection tooSFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a>使用 SFTP 觸發程序
觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中定義的事件。 [深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。  

在此範例中，hello **SFTP-時加入或修改檔案**觸發程序時，才能使用的 tooinitiate 邏輯應用程式工作流程檔案，加入或修改 SFTP 伺服器上。 您也可以加入條件會檢查 hello hello 新增或修改檔案內容，而且如果其內容會指出它應該擷取使用 hello 內容之前，可以讓決策 tooextract hello 檔案。 最後，新增動作 tooextract hello 檔案的內容，並置於 hello SFTP 伺服器上的資料夾中的 hello 擷取內容。 

在企業範例中，您可以使用此觸發程序 toomonitor SFTP 資料夾代表客戶訂單的新檔案。  您無法再使用 SFTP 連接器動作，例如**取得檔案內容**，進一步處理 」 和 「 訂單 」 資料庫中的儲存體的 hello 順序 tooget hello 內容。

> [!INCLUDE [Steps toocreate an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a>新增條件
> [!INCLUDE [Steps tooadd a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a>使用 SFTP 動作
動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。 [深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。  

> [!INCLUDE [Steps toocreate an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a>連接器特定的詳細資料

檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/sftpconnector/)。

## <a name="more-connectors"></a>其他連接器
返回 toohello [Api 清單](apis-list.md)。
