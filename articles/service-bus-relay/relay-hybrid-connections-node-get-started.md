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
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="ad5e9-103">開始使用轉送混合式連線</span><span class="sxs-lookup"><span data-stu-id="ad5e9-103">Get started with Relay Hybrid Connections</span></span>

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="ad5e9-104">本教學課程中介紹過[Azure 轉送混合式連線](relay-what-is-it.md#hybrid-connections)，並示範如何 toouse Node.js toocreate 傳送用戶端應用程式訊息 tooa 對應接聽程式的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ad5e9-104">This tutorial provides an introduction too[Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how toouse Node.js toocreate a client application that sends messages tooa corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="ad5e9-105">將會完成的工作</span><span class="sxs-lookup"><span data-stu-id="ad5e9-105">What will be accomplished</span></span>

<span data-ttu-id="ad5e9-106">因為混合式連線同時需要用戶端和伺服器元件，所以我們將在本教學課程中建立兩個主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ad5e9-106">Because Hybrid Connections requires both a client and a server component, we will create two console applications in this tutorial.</span></span> <span data-ttu-id="ad5e9-107">Hello 步驟如下：</span><span class="sxs-lookup"><span data-stu-id="ad5e9-107">Here are hello steps:</span></span>

1. <span data-ttu-id="ad5e9-108">建立轉送的命名空間，使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="ad5e9-108">Create a Relay namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="ad5e9-109">建立使用 hello Azure 入口網站的混合式連接。</span><span class="sxs-lookup"><span data-stu-id="ad5e9-109">Create a hybrid connection, using hello Azure portal.</span></span>
3. <span data-ttu-id="ad5e9-110">主控台應用程式 tooreceive 訊息寫入伺服器。</span><span class="sxs-lookup"><span data-stu-id="ad5e9-110">Write a server console application tooreceive messages.</span></span>
4. <span data-ttu-id="ad5e9-111">撰寫用戶端主控台應用程式 toosend 訊息。</span><span class="sxs-lookup"><span data-stu-id="ad5e9-111">Write a client console application toosend messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad5e9-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="ad5e9-112">Prerequisites</span></span>

1. <span data-ttu-id="ad5e9-113">[Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="ad5e9-113">[Node.js](https://nodejs.org/en/).</span></span>
2. <span data-ttu-id="ad5e9-114">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ad5e9-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="ad5e9-115">1.建立命名空間使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ad5e9-115">1. Create a namespace using hello Azure portal</span></span>

<span data-ttu-id="ad5e9-116">如果您已經建立的轉送命名空間，跳 toohello[建立使用 hello Azure 入口網站的混合式連接](#2-create-a-hybrid-connection-using-the-azure-portal)> 一節。</span><span class="sxs-lookup"><span data-stu-id="ad5e9-116">If you already have a Relay namespace created, jump toohello [Create a hybrid connection using hello Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a><span data-ttu-id="ad5e9-117">2.建立使用 hello Azure 入口網站的混合式連接</span><span class="sxs-lookup"><span data-stu-id="ad5e9-117">2. Create a hybrid connection using hello Azure portal</span></span>

<span data-ttu-id="ad5e9-118">如果您已經建立的混合式連線，跳 toohello[建立伺服器應用程式](#3-create-a-server-application-listener)> 一節。</span><span class="sxs-lookup"><span data-stu-id="ad5e9-118">If you already have a hybrid connection created, jump toohello [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="ad5e9-119">3.建立伺服器應用程式 (接聽程式)</span><span class="sxs-lookup"><span data-stu-id="ad5e9-119">3. Create a server application (listener)</span></span>

<span data-ttu-id="ad5e9-120">toolisten 及接收來自 hello 轉送訊息，我們會撰寫 Node.js 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ad5e9-120">toolisten and receive messages from hello Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="ad5e9-121">4.建立用戶端應用程式 (傳送者)</span><span class="sxs-lookup"><span data-stu-id="ad5e9-121">4. Create a client application (sender)</span></span>

<span data-ttu-id="ad5e9-122">toosend 訊息 toohello 轉送，我們會撰寫 Node.js 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="ad5e9-122">toosend messages toohello Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-hello-applications"></a><span data-ttu-id="ad5e9-123">5.執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="ad5e9-123">5. Run hello applications</span></span>

1. <span data-ttu-id="ad5e9-124">執行 hello 伺服器應用程式： 從 Node.js 命令提示字元中輸入`node listener.js`。</span><span class="sxs-lookup"><span data-stu-id="ad5e9-124">Run hello server application: from a Node.js command prompt type `node listener.js`.</span></span>
2. <span data-ttu-id="ad5e9-125">執行 hello 用戶端應用程式： 從 Node.js 命令提示字元中輸入`node sender.js`，並輸入一些文字。</span><span class="sxs-lookup"><span data-stu-id="ad5e9-125">Run hello client application: from a Node.js command prompt type `node sender.js`, and enter some text.</span></span>
3. <span data-ttu-id="ad5e9-126">請確定 hello 伺服器應用程式主控台輸出的 hello 文字輸入 hello 用戶端應用程式中。</span><span class="sxs-lookup"><span data-stu-id="ad5e9-126">Ensure that hello server application console outputs hello text that was entered in hello client application.</span></span>

![執行應用程式](./media/relay-hybrid-connections-node-get-started/running-applications.png)

<span data-ttu-id="ad5e9-128">恭喜您，您已經使用 Node.js 建立端對端混合式連線應用程式！</span><span class="sxs-lookup"><span data-stu-id="ad5e9-128">Congratulations, you have created an end-to-end Hybrid Connections application using Node.js!</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad5e9-129">後續步驟：</span><span class="sxs-lookup"><span data-stu-id="ad5e9-129">Next steps:</span></span>

* [<span data-ttu-id="ad5e9-130">轉送常見問題集</span><span class="sxs-lookup"><span data-stu-id="ad5e9-130">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="ad5e9-131">建立命名空間</span><span class="sxs-lookup"><span data-stu-id="ad5e9-131">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="ad5e9-132">開始使用 .NET</span><span class="sxs-lookup"><span data-stu-id="ad5e9-132">Get started with .NET</span></span>](relay-hybrid-connections-dotnet-get-started.md)
* [<span data-ttu-id="ad5e9-133">開始使用 Node</span><span class="sxs-lookup"><span data-stu-id="ad5e9-133">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

