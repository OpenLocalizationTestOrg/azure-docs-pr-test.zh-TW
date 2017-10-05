---
title: "使用 Java 將事件傳送至 Azure 事件中樞 | Microsoft Docs"
description: "開始使用 Java 傳送事件至事件中樞"
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
ms.openlocfilehash: b31771001989e20b88bc8d7bca1afceb58ec197c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="send-events-to-azure-event-hubs-using-java"></a><span data-ttu-id="ed603-103">使用 Java 將事件傳送至 Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="ed603-103">Send events to Azure Event Hubs using Java</span></span>

## <a name="introduction"></a><span data-ttu-id="ed603-104">簡介</span><span class="sxs-lookup"><span data-stu-id="ed603-104">Introduction</span></span>
<span data-ttu-id="ed603-105">事件中樞是高度可擴充的擷取系統，每秒可擷取數百萬個事件，讓應用程式能處理並分析已連線裝置與應用程式產生的大量資料。</span><span class="sxs-lookup"><span data-stu-id="ed603-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="ed603-106">資料收集到事件中樞後，您可以使用任何即時分析提供者或儲存體叢集來轉換與儲存資料。</span><span class="sxs-lookup"><span data-stu-id="ed603-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="ed603-107">如需詳細資訊，請參閱 [事件中樞概觀][Event Hubs overview]。</span><span class="sxs-lookup"><span data-stu-id="ed603-107">For more information, see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="ed603-108">本教學課程也會示範如何使用以 Java 撰寫的主控台應用程式，將事件傳送到事件中樞。</span><span class="sxs-lookup"><span data-stu-id="ed603-108">This tutorial shows how to send events to an event hub by using a console application in Java.</span></span> <span data-ttu-id="ed603-109">若要使用 Java Event Processor Host 程式庫接收事件，請參閱[此文章](event-hubs-java-get-started-receive-eph.md)，或按一下左側目錄中適當的接收語言。</span><span class="sxs-lookup"><span data-stu-id="ed603-109">To receive events using the Java Event Processor Host library, see [this article](event-hubs-java-get-started-receive-eph.md), or click the appropriate receiving language in the left-hand table of contents.</span></span>

<span data-ttu-id="ed603-110">若要完成本教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="ed603-110">In order to complete this tutorial, you will need the following:</span></span>

* <span data-ttu-id="ed603-111">Java 開發環境。</span><span class="sxs-lookup"><span data-stu-id="ed603-111">A Java development environment.</span></span> <span data-ttu-id="ed603-112">針對本教學課程，我們採用 [Eclipse](https://www.eclipse.org/)。</span><span class="sxs-lookup"><span data-stu-id="ed603-112">For this tutorial, we assume [Eclipse](https://www.eclipse.org/).</span></span>
* <span data-ttu-id="ed603-113">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="ed603-113">An active Azure account.</span></span> <br/><span data-ttu-id="ed603-114">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費帳戶。</span><span class="sxs-lookup"><span data-stu-id="ed603-114">If you don't have an account, you can create a free account in just a couple of minutes.</span></span> <span data-ttu-id="ed603-115">如需詳細資料，請參閱 <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure 免費試用</a>。</span><span class="sxs-lookup"><span data-stu-id="ed603-115">For details, see <a href="http://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fdevelop%2Fmobile%2Ftutorials%2Fget-started%2F" target="_blank">Azure Free Trial</a>.</span></span>

## <a name="send-messages-to-event-hubs"></a><span data-ttu-id="ed603-116">將訊息傳送至事件中心</span><span class="sxs-lookup"><span data-stu-id="ed603-116">Send messages to Event Hubs</span></span>
<span data-ttu-id="ed603-117">[Maven 中央儲存機制](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22)中的 Maven 專案可使用事件中樞的 Java 用戶端程式庫。</span><span class="sxs-lookup"><span data-stu-id="ed603-117">The Java client library for Event Hubs is available for use in Maven projects from the [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span> <span data-ttu-id="ed603-118">您可以在 Maven 專案檔中用下列相依性宣告來參照此程式庫：</span><span class="sxs-lookup"><span data-stu-id="ed603-118">You can reference this library using the following dependency declaration inside your Maven project file:</span></span>    

```xml
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>azure-eventhubs</artifactId>
    <version>{VERSION}</version>
</dependency>
```

<span data-ttu-id="ed603-119">對於不同類型的組建環境，您可以明確從 [Maven 中央儲存機制](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22)取得最新發佈的 JAR 檔案。</span><span class="sxs-lookup"><span data-stu-id="ed603-119">For different types of build environments, you can explicitly obtain the latest released JAR files from the [Maven Central Repository](https://search.maven.org/#search%7Cga%7C1%7Ca%3A%22azure-eventhubs%22).</span></span>  

<span data-ttu-id="ed603-120">如果是簡單事件發行者，請針對事件中樞用戶端類別匯入 *com.microsoft.azure.eventhubs* 套件，以及針對公用程式類別匯入 *com.microsoft.azure.servicebus* 套件，例如，與 Azure 服務匯流排訊息用戶端共用的常見例外狀況。</span><span class="sxs-lookup"><span data-stu-id="ed603-120">For a simple event publisher, import the *com.microsoft.azure.eventhubs* package for the Event Hubs client classes and the *com.microsoft.azure.servicebus* package for utility classes such as common exceptions that are shared with the Azure Service Bus messaging client.</span></span> 

<span data-ttu-id="ed603-121">針對下列範例，在您最喜愛的 Java 開發環境中，先為主控台/殼層應用程式建立新的 Maven 專案。</span><span class="sxs-lookup"><span data-stu-id="ed603-121">For the following sample, first create a new Maven project for a console/shell application in your favorite Java development environment.</span></span> <span data-ttu-id="ed603-122">將類別命名為 `Send`。</span><span class="sxs-lookup"><span data-stu-id="ed603-122">Name the class `Send`.</span></span>     

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

<span data-ttu-id="ed603-123">使用您建立事件中樞時所使用的值，來取代命名空間和事件中樞名稱。</span><span class="sxs-lookup"><span data-stu-id="ed603-123">Replace the namespace and event hub names with the values used when you created the event hub.</span></span>

```java
    final String namespaceName = "----ServiceBusNamespaceName-----";
    final String eventHubName = "----EventHubName-----";
    final String sasKeyName = "-----SharedAccessSignatureKeyName-----";
    final String sasKey = "---SharedAccessSignatureKey----";
    ConnectionStringBuilder connStr = new ConnectionStringBuilder(namespaceName, eventHubName, sasKeyName, sasKey);
```

<span data-ttu-id="ed603-124">接著將字串轉換為 UTF-8 位元組編碼，藉以建立單一事件。</span><span class="sxs-lookup"><span data-stu-id="ed603-124">Then, create a singular event by transforming a string into its UTF-8 byte encoding.</span></span> <span data-ttu-id="ed603-125">然後從連接字串建立新的事件中樞用戶端執行個體，並傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="ed603-125">Then, create a new Event Hubs client instance from the connection string and send the message.</span></span>   

```java 

    byte[] payloadBytes = "Test AMQP message from JMS".getBytes("UTF-8");
    EventData sendEvent = new EventData(payloadBytes);

    EventHubClient ehClient = EventHubClient.createFromConnectionStringSync(connStr.toString());
    ehClient.sendSync(sendEvent);
    }
}

``` 

## <a name="next-steps"></a><span data-ttu-id="ed603-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ed603-126">Next steps</span></span>
<span data-ttu-id="ed603-127">您可以造訪下列連結以深入了解事件中樞︰</span><span class="sxs-lookup"><span data-stu-id="ed603-127">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="ed603-128">使用 EventProcessorHost 接收事件</span><span class="sxs-lookup"><span data-stu-id="ed603-128">Receive events using the EventProcessorHost</span></span>](event-hubs-java-get-started-receive-eph.md)
* <span data-ttu-id="ed603-129">[事件中樞概觀][Event Hubs overview]</span><span class="sxs-lookup"><span data-stu-id="ed603-129">[Event Hubs overview][Event Hubs overview]</span></span>
* [<span data-ttu-id="ed603-130">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="ed603-130">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="ed603-131">事件中樞常見問題集</span><span class="sxs-lookup"><span data-stu-id="ed603-131">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md