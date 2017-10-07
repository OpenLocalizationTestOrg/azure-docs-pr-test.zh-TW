---
title: "Azure 邏輯應用程式中的 aaaSMTP 連接器 |Microsoft 文件"
description: "使用 Azure App Service 建立邏輯應用程式。 連接 tooSMTP toosend 電子郵件。"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d4141c08-88d7-4e59-a757-c06d0dc74300
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/15/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 36bb836851014d24f2e069fda8376ad7a08c943b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-smtp-connector"></a>開始使用 hello SMTP 連接器
連接 tooSMTP toosend 電子郵件。

toouse[任何連接器](apis-list.md)，您必須先 toocreate 邏輯應用程式。 您可以從[立即建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)來開始。

## <a name="connect-toosmtp"></a>連接 tooSMTP
邏輯應用程式可以存取任何服務之前，您首先需要 toocreate*連接*toohello 服務。 [連線](connectors-overview.md)可讓邏輯應用程式與另一個服務連線。 例如，tooconnect tooSMTP，您必須先 SMTP*連接*。 toocreate 連線，請輸入您平常用 tooaccess hello 服務連接到 hello 認證。 因此，在 hello SMTP 範例中，輸入 hello 認證 tooyour 連線名稱、 SMTP 伺服器位址，以及使用者登入資訊 toocreate hello 連接 tooSMTP。  

### <a name="create-a-connection-toosmtp"></a>建立連接 tooSMTP
> [!INCLUDE [Steps toocreate a connection tooSMTP](../../includes/connectors-create-api-smtp.md)]
> 
> 

## <a name="use-an-smtp-trigger"></a>使用 SMTP 觸發程序
觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中定義的事件。 [深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。

在此範例中，因為 SMTP 沒有觸發程序，我們將使用 hello **Salesforce-建立物件時**觸發程序。 當 Salesforce 中有新的物件建立時，觸發程序就會啟動。 範例中，我們會設定它使得每次在 Salesforce 中建立新的前置*傳送電子郵件*透過 hello SMTP 連接器，以建立 hello 新潛在客戶通知所發生的動作。

1. 輸入*salesforce* hello hello 邏輯應用程式的設計工具上的搜尋方塊中然後選取 hello **Salesforce-建立物件時**觸發程序。  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-1.png)  
2. hello**當建立物件**顯示控制項。
   ![](../../includes/media/connectors-create-api-salesforce/trigger-2.png)  
3. 選取 hello**物件型別**然後選取*導致*hello 清單中的物件。 在此步驟中，您會指出您要建立一個觸發程序，此觸發程序將在每次 Salesforce 中有建立新潛在客戶的情況時，通知您的邏輯應用程式。  
   ![](../../includes/media/connectors-create-api-salesforce/trigger3.png)  
4. 已建立 hello 觸發程序。  
   ![](../../includes/media/connectors-create-api-salesforce/trigger-4.png)  

## <a name="use-an-smtp-action"></a>使用 SMTP 動作
動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。 [深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。

既然 hello 已加入觸發程序，請遵循在 Salesforce 中建立新的負責人時，會發生這些步驟 tooadd SMTP 動作。

1. 選取**+ 新增步驟**tooadd hello 動作您想要 tootake，建立新的負責人時。  
   ![](../../includes/media/connectors-create-api-salesforce/trigger4.png)  
2. 選取 [新增動作] 。 此隨即開啟 hello 搜尋方塊中，您可以搜尋的任何動作您希望 tootake。  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-2.png)  
3. 輸入*smtp*動作相關 tooSMTP 的 toosearch。  
4. 選取**SMTP-傳送電子郵件**為 hello 動作 tootake hello 新前置建立時。 hello 動作控制區塊會開啟。 您將 tooestablish smtp 連接 hello 設計工具在區塊中有如果您有之前未曾這麼做。  
   ![](../../includes/media/connectors-create-api-smtp/smtp-2.png)    
5. 輸入您想要的電子郵件中的資訊 hello **SMTP-傳送電子郵件**區塊。  
   ![](../../includes/media/connectors-create-api-smtp/using-smtp-action-4.PNG)  
6. 儲存您的工作順序 tooactivate 在您的工作流程。  

## <a name="connector-specific-details"></a>連接器特定的詳細資料

檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/smtpconnector/)。

## <a name="more-connectors"></a>其他連接器
返回 toohello [Api 清單](apis-list.md)。
