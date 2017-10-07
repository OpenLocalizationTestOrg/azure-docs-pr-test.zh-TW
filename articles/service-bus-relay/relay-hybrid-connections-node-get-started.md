---
title: "aaaGet 開始使用 節點中的 Azure 轉送混合式連線 |Microsoft 文件"
description: "為 Azure 轉送混合式連線撰寫 Node.js 主控台應用程式。"
services: service-bus-relay
documentationcenter: node
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e44e4867-3cf3-46be-8f8a-7671e2013bc4
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: node
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 235548399570074f7fd160fec28de8d3633625c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a>開始使用轉送混合式連線

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

本教學課程中介紹過[Azure 轉送混合式連線](relay-what-is-it.md#hybrid-connections)，並示範如何 toouse Node.js toocreate 傳送用戶端應用程式訊息 tooa 對應接聽程式的應用程式。 

## <a name="what-will-be-accomplished"></a>將會完成的工作

因為混合式連線同時需要用戶端和伺服器元件，所以我們將在本教學課程中建立兩個主控台應用程式。 Hello 步驟如下：

1. 建立轉送的命名空間，使用 hello Azure 入口網站。
2. 建立使用 hello Azure 入口網站的混合式連接。
3. 主控台應用程式 tooreceive 訊息寫入伺服器。
4. 撰寫用戶端主控台應用程式 toosend 訊息。

## <a name="prerequisites"></a>必要條件

1. [Node.js](https://nodejs.org/en/).
2. Azure 訂用帳戶。

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1.建立命名空間使用 hello Azure 入口網站

如果您已經建立的轉送命名空間，跳 toohello[建立使用 hello Azure 入口網站的混合式連接](#2-create-a-hybrid-connection-using-the-azure-portal)> 一節。

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a>2.建立使用 hello Azure 入口網站的混合式連接

如果您已經建立的混合式連線，跳 toohello[建立伺服器應用程式](#3-create-a-server-application-listener)> 一節。

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3.建立伺服器應用程式 (接聽程式)

toolisten 及接收來自 hello 轉送訊息，我們會撰寫 Node.js 主控台應用程式。

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4.建立用戶端應用程式 (傳送者)

toosend 訊息 toohello 轉送，我們會撰寫 Node.js 主控台應用程式。

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-hello-applications"></a>5.執行 hello 應用程式

1. 執行 hello 伺服器應用程式： 從 Node.js 命令提示字元中輸入`node listener.js`。
2. 執行 hello 用戶端應用程式： 從 Node.js 命令提示字元中輸入`node sender.js`，並輸入一些文字。
3. 請確定 hello 伺服器應用程式主控台輸出的 hello 文字輸入 hello 用戶端應用程式中。

![執行應用程式](./media/relay-hybrid-connections-node-get-started/running-applications.png)

恭喜您，您已經使用 Node.js 建立端對端混合式連線應用程式！

## <a name="next-steps"></a>後續步驟：

* [轉送常見問題集](relay-faq.md)
* [建立命名空間](relay-create-namespace-portal.md)
* [開始使用 .NET](relay-hybrid-connections-dotnet-get-started.md)
* [開始使用 Node](relay-hybrid-connections-node-get-started.md)

