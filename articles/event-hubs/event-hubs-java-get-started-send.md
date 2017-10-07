---
title: "aaaSend 事件 tooAzure 事件中心使用 Java |Microsoft 文件"
description: "開始傳送 tooEvent 集線器使用 Java"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: core
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: ec537b8849a0cb49855e76c0c0ef4093108fe83c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-java"></a>使用 Java tooAzure 事件中心傳送事件

## <a name="introduction"></a>簡介
事件中心是可高度擴充擷取系統可以內嵌包含數百萬個事件每秒，讓應用程式 tooprocess 及分析 hello 連接的裝置和應用程式所產生的資料量很大。 資料收集到事件中樞後，您可以使用任何即時分析提供者或儲存體叢集來轉換與儲存資料。

如需詳細資訊，請參閱 hello[事件中心概觀][Event Hubs overview]。

本教學課程示範如何使用主控台應用程式在 Java 中的 toosend 事件 tooan 事件中心。 tooreceive 事件使用 hello Java 事件處理器主機程式庫，請參閱[本文](event-hubs-java-get-started-receive-eph.md)，或按一下 hello 適當接收的語言 hello 左側資料表的內容中。

在順序 toocomplete 本教學課程中，您必須遵循的 hello:

* Java 開發環境。 針對本教學課程，我們採用 [Eclipse](https://www.eclipse.org/)。
* 使用中的 Azure 帳戶。 <br/>如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費帳戶。 如需詳細資料，請參閱 <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure 免費試用</a>。

## <a name="send-messages-tooevent-hubs"></a>將訊息傳送 tooEvent 集線器
hello 事件中心的 Java 用戶端程式庫是可用於從 hello Maven 專案[Maven 中央儲存機制](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22)。 您可以參考使用 hello Maven 專案檔內的相依性宣告之後此文件庫：    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

對於不同類型的建置環境，您可以明確地取得最新發行的 hello JAR 檔案從 hello [Maven 中央儲存機制](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22)。  

簡單事件發行者，匯入 hello *com.microsoft.azure.eventhubs* hello 事件中心的用戶端類別和 hello 套件*com.microsoft.azure.servicebus*封裝的公用程式類別，例如常見的例外狀況為共用的 hello Azure 服務匯流排訊息用戶端。 

Hello 遵循範例，先在您最愛的 Java 開發環境中建立新 Maven 專案主控台/shell 應用程式。 Hello 類別命名`Send`。     

```java
import java.io.IOException;
import java.nio.charset.*;
import java.util.*;
import java.util.concurrent.ExecutionException;

import com.microsoft.azure.eventhubs.*;
import com.microsoft.azure.servicebus.*;

public class Send
{
    public static void main(String[] args) 
            throws ServiceBusException, ExecutionException, InterruptedException, IOException
    {
```

當您建立 hello 事件中樞時，使用的 hello 值取代 hello 的命名空間和事件中樞的名稱。

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

接著將字串轉換為 UTF-8 位元組編碼，藉以建立單一事件。 然後，從 hello 連接字串建立新的事件中心用戶端執行個體，並傳送 hello 訊息。   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a>後續步驟
您可以進一步了解事件中心瀏覽下列連結查看 hello:

* [接收使用 hello EventProcessorHost 事件](event-hubs-java-get-started-receive-eph.md)
* [事件中樞概觀][Event Hubs overview]
* [建立事件中樞](event-hubs-create.md)
* [事件中樞常見問題集](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md