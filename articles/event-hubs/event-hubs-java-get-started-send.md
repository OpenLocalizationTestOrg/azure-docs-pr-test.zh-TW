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
# <a name="send-events-tooazure-event-hubs-using-java"></a><span data-ttu-id="633e4-103">使用 Java tooAzure 事件中心傳送事件</span><span class="sxs-lookup"><span data-stu-id="633e4-103">Send events tooAzure Event Hubs using Java</span></span>

## <a name="introduction"></a><span data-ttu-id="633e4-104">簡介</span><span class="sxs-lookup"><span data-stu-id="633e4-104">Introduction</span></span>
<span data-ttu-id="633e4-105">事件中心是可高度擴充擷取系統可以內嵌包含數百萬個事件每秒，讓應用程式 tooprocess 及分析 hello 連接的裝置和應用程式所產生的資料量很大。</span><span class="sxs-lookup"><span data-stu-id="633e4-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application tooprocess and analyze hello massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="633e4-106">資料收集到事件中樞後，您可以使用任何即時分析提供者或儲存體叢集來轉換與儲存資料。</span><span class="sxs-lookup"><span data-stu-id="633e4-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="633e4-107">如需詳細資訊，請參閱 hello[事件中心概觀][Event Hubs overview]。</span><span class="sxs-lookup"><span data-stu-id="633e4-107">For more information, see hello [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="633e4-108">本教學課程示範如何使用主控台應用程式在 Java 中的 toosend 事件 tooan 事件中心。</span><span class="sxs-lookup"><span data-stu-id="633e4-108">This tutorial shows how toosend events tooan event hub by using a console application in Java.</span></span> <span data-ttu-id="633e4-109">tooreceive 事件使用 hello Java 事件處理器主機程式庫，請參閱[本文](event-hubs-java-get-started-receive-eph.md)，或按一下 hello 適當接收的語言 hello 左側資料表的內容中。</span><span class="sxs-lookup"><span data-stu-id="633e4-109">tooreceive events using hello Java Event Processor Host library, see [this article](event-hubs-java-get-started-receive-eph.md), or click hello appropriate receiving language in hello left-hand table of contents.</span></span>

<span data-ttu-id="633e4-110">在順序 toocomplete 本教學課程中，您必須遵循的 hello:</span><span class="sxs-lookup"><span data-stu-id="633e4-110">In order toocomplete this tutorial, you will need hello following:</span></span>

* <span data-ttu-id="633e4-111">Java 開發環境。</span><span class="sxs-lookup"><span data-stu-id="633e4-111">A Java development environment.</span></span> <span data-ttu-id="633e4-112">針對本教學課程，我們採用 [Eclipse](https://www.eclipse.org/)。</span><span class="sxs-lookup"><span data-stu-id="633e4-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="633e4-113">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="633e4-113">An active Azure account.</span></span> <br/><span data-ttu-id="633e4-114">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費帳戶。</span><span class="sxs-lookup"><span data-stu-id="633e4-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="633e4-115">如需詳細資料，請參閱 <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure 免費試用</a>。</span><span class="sxs-lookup"><span data-stu-id="633e4-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="send-messages-tooevent-hubs"></a><span data-ttu-id="633e4-116">將訊息傳送 tooEvent 集線器</span><span class="sxs-lookup"><span data-stu-id="633e4-116">Send messages tooEvent Hubs</span></span>
<span data-ttu-id="633e4-117">hello 事件中心的 Java 用戶端程式庫是可用於從 hello Maven 專案[Maven 中央儲存機制](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22)。</span><span class="sxs-lookup"><span data-stu-id="633e4-117">hello Java client library for Event Hubs is available for use in Maven projects from hello [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span> <span data-ttu-id="633e4-118">您可以參考使用 hello Maven 專案檔內的相依性宣告之後此文件庫：</span><span class="sxs-lookup"><span data-stu-id="633e4-118">You can reference this library using hello following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

<span data-ttu-id="633e4-119">對於不同類型的建置環境，您可以明確地取得最新發行的 hello JAR 檔案從 hello [Maven 中央儲存機制](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22)。</span><span class="sxs-lookup"><span data-stu-id="633e4-119">For different types of build environments, you can explicitly obtain hello latest released JAR files from hello [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span>  

<span data-ttu-id="633e4-120">簡單事件發行者，匯入 hello *com.microsoft.azure.eventhubs* hello 事件中心的用戶端類別和 hello 套件*com.microsoft.azure.servicebus*封裝的公用程式類別，例如常見的例外狀況為共用的 hello Azure 服務匯流排訊息用戶端。</span><span class="sxs-lookup"><span data-stu-id="633e4-120">For a simple event publisher, import hello *com.microsoft.azure.eventhubs* package for hello Event Hubs client classes and hello *com.microsoft.azure.servicebus* package for utility classes such as common exceptions that are shared with hello Azure Service Bus messaging client.</span></span> 

<span data-ttu-id="633e4-121">Hello 遵循範例，先在您最愛的 Java 開發環境中建立新 Maven 專案主控台/shell 應用程式。</span><span class="sxs-lookup"><span data-stu-id="633e4-121">For hello following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="633e4-122">Hello 類別命名`Send`。</span><span class="sxs-lookup"><span data-stu-id="633e4-122">Name hello class `Send`.</span></span>     

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

<span data-ttu-id="633e4-123">當您建立 hello 事件中樞時，使用的 hello 值取代 hello 的命名空間和事件中樞的名稱。</span><span class="sxs-lookup"><span data-stu-id="633e4-123">Replace hello namespace and event hub names with hello values used when you created hello event hub.</span></span>

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

<span data-ttu-id="633e4-124">接著將字串轉換為 UTF-8 位元組編碼，藉以建立單一事件。</span><span class="sxs-lookup"><span data-stu-id="633e4-124">Then, create a singular event by transforming a string into its UTF-8 byte encoding.</span></span> <span data-ttu-id="633e4-125">然後，從 hello 連接字串建立新的事件中心用戶端執行個體，並傳送 hello 訊息。</span><span class="sxs-lookup"><span data-stu-id="633e4-125">Then, create a new Event Hubs client instance from hello connection string and send hello message.</span></span>   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a><span data-ttu-id="633e4-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="633e4-126">Next steps</span></span>
<span data-ttu-id="633e4-127">您可以進一步了解事件中心瀏覽下列連結查看 hello:</span><span class="sxs-lookup"><span data-stu-id="633e4-127">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="633e4-128">接收使用 hello EventProcessorHost 事件</span><span class="sxs-lookup"><span data-stu-id="633e4-128">Receive events using hello EventProcessorHost</span></span>](event-hubs-java-get-started-receive-eph.md)
* <span data-ttu-id="633e4-129">[事件中樞概觀][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="633e4-129">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="633e4-130">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="633e4-130">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="633e4-131">事件中樞常見問題集</span><span class="sxs-lookup"><span data-stu-id="633e4-131">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md