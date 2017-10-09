---
title: "aaaGet 開始使用.net 的 Azure 轉送混合式連線 |Microsoft 文件"
description: "為 Azure 轉送混合式連線撰寫 C# 主控台應用程式。"
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d1386900-b942-4abf-acfc-38d2ef826253
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 1e4af28e7cd4393c8ca965a149a0b83ebcc44f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a>開始使用轉送混合式連線
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

本教學課程中介紹過[Azure 轉送混合式連線](relay-what-is-it.md#hybrid-connections)，並示範如何 toouse.NET toocreate 傳送用戶端應用程式訊息 tooa 對應接聽程式的應用程式。 

## <a name="what-will-be-accomplished"></a>將會完成的工作
混合式連線需要用戶端和伺服器元件，因為 hello 教學課程會建立兩個主控台應用程式。 Hello 步驟如下：

1. 建立轉送的命名空間，使用 hello Azure 入口網站。
2. 該命名空間，使用 hello Azure 入口網站中建立混合式連接。
3. 寫入伺服器 （接聽程式） 主控台應用程式 tooreceive 訊息。
4. 撰寫用戶端 （傳送者） 主控台應用程式 toosend 訊息。

## <a name="prerequisites"></a>必要條件

toocomplete 本教學課程中，您將需要下列必要條件 hello:

1. [Visual Studio 2015 或更新版本](http://www.visualstudio.com)。 在此教學課程中的 hello 範例會使用 Visual Studio 2017。
2. Azure 訂用帳戶。

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1.建立命名空間使用 hello Azure 入口網站
如果您已經建立轉送命名空間，跳 toohello[建立使用 hello Azure 入口網站的混合式連接](#2-create-a-hybrid-connection-using-the-azure-portal)> 一節。

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a>2.建立使用 hello Azure 入口網站的混合式連接
如果您已經建立混合式連接，跳 toohello[建立伺服器應用程式](#3-create-a-server-application-listener)> 一節。

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3.建立伺服器應用程式 (接聽程式)
toolisten 和接收訊息從 hello 轉送，我們會撰寫 C# 主控台應用程式使用 Visual Studio。

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4.建立用戶端應用程式 (傳送者)
toosend 訊息 toohello 轉送，我們會撰寫 C# 主控台應用程式使用 Visual Studio。

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-hello-applications"></a>5.執行 hello 應用程式
1. 執行 hello 伺服器應用程式。
2. 執行 hello 用戶端應用程式並輸入一些文字。
3. 請確定 hello 伺服器應用程式主控台輸出的 hello 文字輸入 hello 用戶端應用程式中。

![執行應用程式](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

恭喜您，您已建立端對端混合式連線應用程式。

## <a name="next-steps"></a>後續步驟：
* [轉送常見問題集](relay-faq.md)
* [建立命名空間](relay-create-namespace-portal.md)
* [開始使用 Node](relay-hybrid-connections-node-get-started.md)

