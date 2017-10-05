---
title: "使用 C 將事件傳送至 Azure 事件中樞 | Microsoft Docs"
description: "使用 C 將事件傳送至 Azure 事件中樞"
services: event-hubs
documentationcenter: 
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: c
ms.devlang: csharp
ms.topic: article
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a615ee39b6c3731cc7df366e9fabeed5219a71b4
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="send-events-to-azure-event-hubs-using-c"></a><span data-ttu-id="e042b-103">使用 C 將事件傳送至 Azure 事件中樞</span><span class="sxs-lookup"><span data-stu-id="e042b-103">Send events to Azure Event Hubs using C</span></span>

## <a name="introduction"></a><span data-ttu-id="e042b-104">簡介</span><span class="sxs-lookup"><span data-stu-id="e042b-104">Introduction</span></span>
<span data-ttu-id="e042b-105">事件中樞是高度可擴充的擷取系統，每秒可擷取數百萬個事件，讓應用程式能處理並分析已連線裝置與應用程式產生的大量資料。</span><span class="sxs-lookup"><span data-stu-id="e042b-105">Event Hubs is a highly scalable ingestion system that can ingest millions of events per second, enabling an application to process and analyze the massive amounts of data produced by your connected devices and applications.</span></span> <span data-ttu-id="e042b-106">資料收集到事件中樞後，您可以使用任何即時分析提供者或儲存體叢集來轉換與儲存資料。</span><span class="sxs-lookup"><span data-stu-id="e042b-106">Once collected into an event hub, you can transform and store data using any real-time analytics provider or storage cluster.</span></span>

<span data-ttu-id="e042b-107">如需詳細資訊，請參閱 [事件中樞概觀][Event Hubs overview]。</span><span class="sxs-lookup"><span data-stu-id="e042b-107">For more information, please see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="e042b-108">在本教學課程中，您將了解如何使用以 C 撰寫的主控台應用程式將事件傳送到事件中樞。若要接收事件，請按一下左側目錄中適當的接收語言。</span><span class="sxs-lookup"><span data-stu-id="e042b-108">In this tutorial, you will learn how to send events to an event hub using a console application in C. To receive events, click the appropriate receiving language in the left-hand table of contents.</span></span>

<span data-ttu-id="e042b-109">若要完成本教學課程，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="e042b-109">To complete this tutorial, you will need the following:</span></span>

* <span data-ttu-id="e042b-110">C 開發環境。</span><span class="sxs-lookup"><span data-stu-id="e042b-110">A C development environment.</span></span> <span data-ttu-id="e042b-111">在本教學課程中，我們假設 Azure Linux VM上的 gcc 堆疊有 Ubuntu 14.04。</span><span class="sxs-lookup"><span data-stu-id="e042b-111">For this tutorial, we will assume the gcc stack on an Azure Linux VM with Ubuntu 14.04.</span></span>
* <span data-ttu-id="e042b-112">[Microsoft Visual Studio](https://www.visualstudio.com/)。</span><span class="sxs-lookup"><span data-stu-id="e042b-112">[Microsoft Visual Studio](https://www.visualstudio.com/).</span></span>
* <span data-ttu-id="e042b-113">使用中的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="e042b-113">An active Azure account.</span></span> <span data-ttu-id="e042b-114">如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e042b-114">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="e042b-115">如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="e042b-115">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="send-messages-to-event-hubs"></a><span data-ttu-id="e042b-116">將訊息傳送至事件中心</span><span class="sxs-lookup"><span data-stu-id="e042b-116">Send messages to Event Hubs</span></span>
<span data-ttu-id="e042b-117">在本節中，我們會撰寫一個 C 應用程式，以將事件傳送到事件中樞。</span><span class="sxs-lookup"><span data-stu-id="e042b-117">In this section we write a C app to send events to your event hub.</span></span> <span data-ttu-id="e042b-118">此程式碼會使用 [Apache Qpid 專案](http://qpid.apache.org/)中的 Proton AMQP 程式庫。</span><span class="sxs-lookup"><span data-stu-id="e042b-118">The code uses the Proton AMQP library from the [Apache Qpid project](http://qpid.apache.org/).</span></span> <span data-ttu-id="e042b-119">這與搭配使用 Service Bus Queues and Topics 與透過 C 的 AMQP 類似 (如 [這裡](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504)所示)。</span><span class="sxs-lookup"><span data-stu-id="e042b-119">This is analogous to using Service Bus queues and topics with AMQP from C as shown [here](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504).</span></span> <span data-ttu-id="e042b-120">如需詳細資訊，請參閱 [Qpid Proton 文件](http://qpid.apache.org/proton/index.html)。</span><span class="sxs-lookup"><span data-stu-id="e042b-120">For more information, see [Qpid Proton documentation](http://qpid.apache.org/proton/index.html).</span></span>

1. <span data-ttu-id="e042b-121">從 [Qpid AMQP Messenger 頁面](https://qpid.apache.org/proton/messenger.html)，遵循指示以安裝 Qpid Proton (視您的環境而定)。</span><span class="sxs-lookup"><span data-stu-id="e042b-121">From the [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html), follow the instructions to install Qpid Proton, depending on your environment.</span></span>
2. <span data-ttu-id="e042b-122">若要編譯 Proton 程式庫，請安裝下列封裝：</span><span class="sxs-lookup"><span data-stu-id="e042b-122">To compile the Proton library, install the following packages:</span></span>
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. <span data-ttu-id="e042b-123">下載 [Qpid Proton 程式庫](http://qpid.apache.org/proton/index.html)，並將它解壓縮，例如：</span><span class="sxs-lookup"><span data-stu-id="e042b-123">Download the [Qpid Proton library](http://qpid.apache.org/proton/index.html), and extract it, e.g.:</span></span>
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. <span data-ttu-id="e042b-124">建立組建目錄、編譯並安裝：</span><span class="sxs-lookup"><span data-stu-id="e042b-124">Create a build directory, compile and install:</span></span>
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. <span data-ttu-id="e042b-125">在工作目錄中，使用下列程式碼建立一個稱為 **sender.c** 的新檔案。</span><span class="sxs-lookup"><span data-stu-id="e042b-125">In your work directory, create a new file called **sender.c** with the following code.</span></span> <span data-ttu-id="e042b-126">請記得將值替換成您的事件中樞名稱和命名空間名稱。</span><span class="sxs-lookup"><span data-stu-id="e042b-126">Remember to substitute the value for your event hub name and namespace name.</span></span> <span data-ttu-id="e042b-127">您也必須替代先前針對 **SendRule** 建立之金鑰的 URL 編碼版本。</span><span class="sxs-lookup"><span data-stu-id="e042b-127">You must also substitute a URL-encoded version of the key for the **SendRule** created earlier.</span></span> <span data-ttu-id="e042b-128">您可以在 [這裡](http://www.w3schools.com/tags/ref_urlencode.asp)對其進行 URL 編碼。</span><span class="sxs-lookup"><span data-stu-id="e042b-128">You can URL-encode it [here](http://www.w3schools.com/tags/ref_urlencode.asp).</span></span>
   
    ```c
    #include "proton/message.h"
    #include "proton/messenger.h"
   
    #include <getopt.h>
    #include <proton/util.h>
    #include <sys/time.h>
    #include <stddef.h>
    #include <stdio.h>
    #include <string.h>
    #include <unistd.h>
    #include <stdlib.h>
   
    #define check(messenger)                                                     
      {                                                                          
        if(pn_messenger_errno(messenger))                                        
        {                                                                        
          printf("check\n");                                                     
          die(__FILE__, __LINE__, pn_error_text(pn_messenger_error(messenger))); 
        }                                                                        
      }  
   
    pn_timestamp_t time_now(void)
    {
      struct timeval now;
      if (gettimeofday(&now, NULL)) pn_fatal("gettimeofday failed\n");
      return ((pn_timestamp_t)now.tv_sec) * 1000 + (now.tv_usec / 1000);
    }  
   
    void die(const char *file, int line, const char *message)
    {
      printf("Dead\n");
      fprintf(stderr, "%s:%i: %s\n", file, line, message);
      exit(1);
    }
   
    int sendMessage(pn_messenger_t * messenger) {
        char * address = (char *) "amqps://SendRule:{Send Rule key}@{namespace name}.servicebus.windows.net/{event hub name}";
        char * msgtext = (char *) "Hello from C!";
   
        pn_message_t * message;
        pn_data_t * body;
        message = pn_message();
   
        pn_message_set_address(message, address);
        pn_message_set_content_type(message, (char*) "application/octect-stream");
        pn_message_set_inferred(message, true);
   
        body = pn_message_body(message);
        pn_data_put_binary(body, pn_bytes(strlen(msgtext), msgtext));
   
        pn_messenger_put(messenger, message);
        check(messenger);
        pn_messenger_send(messenger, 1);
        check(messenger);
   
        pn_message_free(message);
    }
   
    int main(int argc, char** argv) {
        printf("Press Ctrl-C to stop the sender process\n");
   
        pn_messenger_t *messenger = pn_messenger(NULL);
        pn_messenger_set_outgoing_window(messenger, 1);
        pn_messenger_start(messenger);
   
        while(true) {
            sendMessage(messenger);
            printf("Sent message\n");
            sleep(1);
        }
   
        // release messenger resources
        pn_messenger_stop(messenger);
        pn_messenger_free(messenger);
   
        return 0;
    }
    ```
6. <span data-ttu-id="e042b-129">編譯檔案，並假設 **gcc**：</span><span class="sxs-lookup"><span data-stu-id="e042b-129">Compile the file, assuming **gcc**:</span></span>
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > <span data-ttu-id="e042b-130">在這個程式碼中，我們使用輸出視窗 1 盡快強制輸出訊息。</span><span class="sxs-lookup"><span data-stu-id="e042b-130">In this code, we use an outgoing window of 1 to force the messages out as soon as possible.</span></span> <span data-ttu-id="e042b-131">應用程式一般應該會嘗試批次處理訊息，以增加輸送量。</span><span class="sxs-lookup"><span data-stu-id="e042b-131">In general, your application should try to batch messages to increase throughput.</span></span> <span data-ttu-id="e042b-132">如需如何在此環境和其他環境中，以及從提供繫結的平台 (目前是 Perl、PHP、Python 和 Ruby) 中使用 Qpid Proton 程式庫的相關資訊，請參閱 [Qpid AMQP Messenger 頁面](https://qpid.apache.org/proton/messenger.html)。</span><span class="sxs-lookup"><span data-stu-id="e042b-132">See the [Qpid AMQP Messenger page](https://qpid.apache.org/proton/messenger.html) for information about how to use the Qpid Proton library in this and other environments, and from platforms for which bindings are provided (currently Perl, PHP, Python, and Ruby).</span></span>


## <a name="next-steps"></a><span data-ttu-id="e042b-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e042b-133">Next steps</span></span>
<span data-ttu-id="e042b-134">您可以造訪下列連結以深入了解事件中樞︰</span><span class="sxs-lookup"><span data-stu-id="e042b-134">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="e042b-135">事件中樞概觀</span><span class="sxs-lookup"><span data-stu-id="e042b-135">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md
)
* [<span data-ttu-id="e042b-136">建立事件中樞</span><span class="sxs-lookup"><span data-stu-id="e042b-136">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="e042b-137">事件中樞常見問題集</span><span class="sxs-lookup"><span data-stu-id="e042b-137">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
