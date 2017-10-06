---
title: "aaaLearn toouse hello 邏輯應用程式中的 FTP 連接器的方式 |Microsoft 文件"
description: "使用 Azure App Service 建立邏輯應用程式。 連接 tooFTP 伺服器 toomanage 您的檔案。 您可以執行各種動作，例如上傳、更新、取得及刪除 FTP 伺服器中的檔案。"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
tags: connectors
ms.assetid: d83c55fe-eb59-4b7b-a5ec-afac5c772616
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/22/2016
ms.author: mandia; ladocs
ms.openlocfilehash: a7020df2005ebb34fc569627ae0516b8528cc7a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-ftp-connector"></a>開始使用 hello FTP 連接器
使用 hello FTP 連接器 toomonitor、 管理以及建立 FTP 伺服器上的檔案。 

toouse[任何連接器](apis-list.md)，您必須先 toocreate 邏輯應用程式。 您可以從[立即建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)來開始。

## <a name="connect-tooftp"></a>連接 tooFTP
邏輯應用程式可以存取任何服務之前，您首先需要 toocreate*連接*toohello 服務。 [連線](connectors-overview.md)可讓邏輯應用程式與另一個服務連線。  

### <a name="create-a-connection-tooftp"></a>建立連接 tooFTP
> [!INCLUDE [Steps toocreate a connection tooFTP](../../includes/connectors-create-api-ftp.md)]
> 
> 

## <a name="use-a-ftp-trigger"></a>使用 FTP 觸發程序
觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中定義的事件。 [深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。  

> [!IMPORTANT]
> hello FTP 連接器，必須從 hello 網際網路存取的 FTP 伺服器是設定 toooperate 被動模式。 此外，hello FTP 連接器是**隱含 FTPS (FTP over SSL) 與不相容**。 hello FTP 連接器僅支援明確 FTPS (FTP over SSL)。  
> 
> 

在此範例中，我將示範如何 toouse hello **FTP-時加入或修改檔案**觸發 tooinitiate 邏輯應用程式工作流程時，新增或修改 FTP 伺服器上的檔案。 在企業範例中，您可以使用此觸發程序 toomonitor FTP 資料夾，表示客戶訂單的新檔案。  您無法再使用 FTP 連接器動作例如**取得檔案內容**tooget hello 內容的進一步處理和儲存體 orders 資料庫中的 hello 順序。

1. 輸入*ftp* hello hello 邏輯應用程式的設計工具上的搜尋方塊中然後選取 hello **FTP-時加入或修改檔案**觸發程序   
   ![FTP 觸發程序影像 1](./media/connectors-create-api-ftp/ftp-trigger-1.png)  
   hello**時加入或修改檔案**控制開啟  
   ![FTP 觸發程序影像 2](./media/connectors-create-api-ftp/ftp-trigger-2.png)  
2. 選取 hello **...**位於 hello 控制項 hello 右邊。 這會開啟 hello 資料夾選擇器控制項  
   ![FTP 觸發程序影像 3](./media/connectors-create-api-ftp/ftp-trigger-3.png)  
3. 選取 hello  **>**  （向右箭號），並瀏覽 toofind hello 資料夾 toomonitor 需新增或修改檔案。 選取 hello 資料夾，並注意 hello 資料夾現在會顯示在 hello**資料夾**控制項。  
   ![FTP 觸發程序影像 4](./media/connectors-create-api-ftp/ftp-trigger-4.png)   

此時，應用程式邏輯已使用的觸發程序會在開始執行的 hello 其他觸發程序和 hello 工作流程中的動作檔案修改或建立 hello 特定 FTP 資料夾中。 

> [!NOTE]
> 功能的邏輯應用程式 toobe，它必須包含至少一個觸發程序與一個動作。 請遵循下一個區段 tooadd hello 動作中的 hello 步驟。  
> 
> 

## <a name="use-a-ftp-action"></a>使用 FTP 動作
動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。 [深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。  

既然您已加入觸發程序，請遵循這些步驟 tooadd 會收到 hello hello 觸發程序所找到的 hello 新增或修改檔案內容的動作。    

1. 選取**+ 新增步驟**tooadd hello hello 動作 tooget hello hello 上檔案的內容 hello FTP 伺服器  
2. 選取 hello**將動作加入**連結。  
   ![FTP 動作影像 1](./media/connectors-create-api-ftp/ftp-action-1.png)  
3. 輸入*FTP* toosearch 所有動作相關 tooFTP。
4. 選取**FTP-取得檔案內容**為 hello 動作 tootake hello FTP 資料夾中發現新的或修改檔案時。      
   ![FTP 動作影像 2](./media/connectors-create-api-ftp/ftp-action-2.png)  
   hello**取得檔案內容**控制隨即開啟。 **請注意**： 您將會提示的 tooauthorize 您邏輯應用程式 tooaccess FTP 伺服器帳戶如果您有之前未曾這麼做。  
   ![FTP 動作影像 3](./media/connectors-create-api-ftp/ftp-action-3.png)   
5. 選取 hello**檔案**控制項 (hello 空白字元位於下方**檔案***)。 在這裡，您可以使用任何 hello 的各種屬性從 hello FTP 伺服器上找到的 hello 新增或修改檔案。  
6. 選取 hello**檔案內容**選項。  
   ![FTP 動作影像 4](./media/connectors-create-api-ftp/ftp-action-4.png)   
7. 更新 hello 控制項時，表示該 hello **FTP-取得檔案內容**動作會收到 hello*檔案內容*hello hello FTP 伺服器上新增或修改檔案。      
   ![FTP 動作影像 5](./media/connectors-create-api-ftp/ftp-action-5.png)     
8. 儲存您的工作，然後將檔案 toohello FTP 資料夾 tootest 加入您的工作流程。    

此時，已經過 hello 邏輯應用程式與觸發程序 toomonitor 資料夾上設定 FTP 伺服器，並起始 hello 工作流程時它發現新的檔案或 hello FTP 伺服器上的已修改的檔案。 

hello 邏輯應用程式也已設定與動作 tooget hello 的 hello 新增或修改檔案內容。

您現在可以加入另一個動作，例如 hello [SQL Server-插入資料列](connectors-create-api-sqlazure.md)hello 到 SQL 資料庫資料表的新增或修改檔案動作 tooinsert hello 內容。  

## <a name="connector-specific-details"></a>連接器特定的詳細資料

檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/ftpconnector/)。 

## <a name="next-steps"></a>後續步驟
[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)

