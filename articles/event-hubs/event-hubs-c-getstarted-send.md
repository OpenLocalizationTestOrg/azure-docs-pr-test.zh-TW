---
title: "aaaSend 事件 tooAzure 事件中心使用 C |Microsoft 文件"
description: "傳送事件使用 C tooAzure 事件中心"
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
ms.openlocfilehash: bb53300c070debb4a3658a38df9d3966f08e81ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooazure-event-hubs-using-c"></a>傳送事件使用 C tooAzure 事件中心

## <a name="introduction"></a>簡介
事件中心是可高度擴充擷取系統可以內嵌包含數百萬個事件每秒，讓應用程式 tooprocess 及分析 hello 連接的裝置和應用程式所產生的資料量很大。 資料收集到事件中樞後，您可以使用任何即時分析提供者或儲存體叢集來轉換與儲存資料。

如需詳細資訊，請參閱 hello [事件中心概觀] [事件中心概觀]。

在此教學課程中，您將學習如何 toosend 事件 tooan 事件中心 C.tooreceive 事件中使用主控台應用程式按一下 hello 適當接收的語言 hello 左側資料表的內容中。

toocomplete 本教學課程中，您必須遵循的 hello:

* C 開發環境。 本教學課程，我們將假設使用 Ubuntu 14.04 Azure Linux VM 上的 hello gcc 堆疊。
* [Microsoft Visual Studio](https://www.visualstudio.com/)。
* 使用中的 Azure 帳戶。 如果您沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。

## <a name="send-messages-tooevent-hubs"></a>將訊息傳送 tooEvent 集線器
本節中，我們會撰寫 C 應用程式 toosend 事件 tooyour 事件中樞。 hello 程式碼會使用從 hello hello Proton AMQP 程式庫[Apache Qpid 專案](http://qpid.apache.org/)。 這很類似 toousing Service Bus 佇列和主題，但從 C AMQP 如下所示[這裡](https://code.msdn.microsoft.com/Using-Apache-Qpid-Proton-C-afd76504)。 如需詳細資訊，請參閱 [Qpid Proton 文件](http://qpid.apache.org/proton/index.html)。

1. 從 hello [Qpid AMQP Messenger 頁面](https://qpid.apache.org/proton/messenger.html)，遵循 hello 指示 tooinstall Qpid Proton，根據您的環境。
2. toocompile hello Proton 程式庫，請安裝下列封裝的 hello:
   
    ```shell
    sudo apt-get install build-essential cmake uuid-dev openssl libssl-dev
    ```
3. 下載 hello [Qpid Proton 程式庫](http://qpid.apache.org/proton/index.html)，並將它解壓縮，例如：
   
    ```shell
    wget http://archive.apache.org/dist/qpid/proton/0.7/qpid-proton-0.7.tar.gz
    tar xvfz qpid-proton-0.7.tar.gz
    ```
4. 建立組建目錄、編譯並安裝：
   
    ```shell
    cd qpid-proton-0.7
    mkdir build
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=/usr ..
    sudo make install
    ```
5. 在工作目錄中，建立新的檔案，稱為**sender.c**以下列程式碼的 hello。 請記住您的事件中樞的名稱和命名空間名稱的 toosubstitute hello 值。 您也必須替代 URL 編碼版本 hello 的 hello 金鑰**SendRule**稍早建立。 您可以在 [這裡](http://www.w3schools.com/tags/ref_urlencode.asp)對其進行 URL 編碼。
   
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
        printf("Press Ctrl-C toostop hello sender process\n");
   
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
6. 編譯 hello 檔案假設**gcc**:
   
    ```
    gcc sender.c -o sender -lqpid-proton
    ```

    > [!NOTE]
    > 在此程式碼中，我們使用外寄出 1 個 tooforce hello 訊息的視窗執行下列儘速。 一般情況下，您的應用程式應該嘗試 toobatch 訊息 tooincrease 輸送量。 請參閱 hello [Qpid AMQP Messenger 頁面](https://qpid.apache.org/proton/messenger.html)如需如何 toouse hello Qpid Proton 程式庫在此範例與其他環境，以及從繫結所提供的平台 （目前 Perl、 PHP、 Python 和 Ruby）。


## <a name="next-steps"></a>後續步驟
您可以進一步了解事件中心瀏覽下列連結查看 hello:

* [事件中樞概觀](event-hubs-what-is-event-hubs.md
)
* [建立事件中樞](event-hubs-create.md)
* [事件中樞常見問題集](event-hubs-faq.md)

<!-- Images. -->
[21]: ./media/event-hubs-c-ephcs-getstarted/run-csharp-ephcs1.png
[24]: ./media/event-hubs-c-ephcs-getstarted/receive-eph-c.png
