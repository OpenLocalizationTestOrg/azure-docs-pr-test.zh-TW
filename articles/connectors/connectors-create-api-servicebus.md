---
title: "在您的 logic apps aaaLearn toouse hello Azure 服務匯流排連接器 |Microsoft 文件"
description: "使用 Azure App Service 建立邏輯應用程式。 連接 tooAzure Service Bus toosend 和接收訊息。 您可以執行動作，例如傳送 tooqueue、 傳送 tootopic、 接收來自佇列，及接收來自訂用帳戶。"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d6d14f5f-2126-4e33-808e-41de08e6721f
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/02/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c815ac167c3106ade470ce139d119085558a9497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-service-bus-connector"></a>開始使用 hello Azure 服務匯流排連接器
連接 tooAzure Service Bus toosend 和接收訊息。 您可以執行動作，例如傳送 tooqueue、 傳送 tootopic、 接收來自佇列，及接收來自訂用帳戶。

toouse[任何連接器](apis-list.md)，您必須先 toocreate 邏輯應用程式。 您可以從[立即建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)來開始。

## <a name="connect-tooservice-bus"></a>連接 tooService 匯流排
邏輯應用程式可以存取任何服務之前，您必須先 toocreate 連接 toohello 服務。 [連線](connectors-overview.md)可讓邏輯應用程式與另一個服務連線。  

> [!INCLUDE [Steps toocreate a connection tooAzure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a>使用服務匯流排觸發程序
觸發程序是可以使用的 toostart hello 工作流程邏輯應用程式中定義的事件。 [深入了解觸發程序](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。  

> [!INCLUDE [Steps toocreate a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a>使用服務匯流排動作
動作是由定義在邏輯應用程式中的 hello 工作流程執行的作業。 [深入了解動作](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts)。

[!INCLUDE [Steps toocreate a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a>連接器特定的詳細資料

檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/servicebus/)。 

## <a name="next-steps"></a>後續步驟
[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。

