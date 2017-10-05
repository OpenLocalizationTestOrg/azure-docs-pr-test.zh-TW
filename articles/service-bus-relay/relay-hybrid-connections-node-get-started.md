---
title: "在 Node 中開始使用 Azure 轉送混合式連接 | Microsoft Docs"
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
ms.openlocfilehash: c3bfc45969f250059988129f532edd12dfe3dcfe
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="d40e6-103">開始使用轉送混合式連線</span><span class="sxs-lookup"><span data-stu-id="d40e6-103">Get started with Relay Hybrid Connections</span></span>

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="d40e6-104">本教學課程提供 [Azure 轉送混合式連線](relay-what-is-it.md#hybrid-connections)的指示，並示範如何使用 Node.js 來建立用戶端應用程式，以將訊息傳送至對應的接聽端應用程式。</span><span class="sxs-lookup"><span data-stu-id="d40e6-104">This tutorial provides an introduction to [Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how to use Node.js to create a client application that sends messages to a corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="d40e6-105">將會完成的工作</span><span class="sxs-lookup"><span data-stu-id="d40e6-105">What will be accomplished</span></span>

<span data-ttu-id="d40e6-106">因為混合式連線同時需要用戶端和伺服器元件，所以我們將在本教學課程中建立兩個主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d40e6-106">Because Hybrid Connections requires both a client and a server component, we will create two console applications in this tutorial.</span></span> <span data-ttu-id="d40e6-107">步驟如下：</span><span class="sxs-lookup"><span data-stu-id="d40e6-107">Here are the steps:</span></span>

1. <span data-ttu-id="d40e6-108">使用 Azure 入口網站建立轉送命名空間。</span><span class="sxs-lookup"><span data-stu-id="d40e6-108">Create a Relay namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="d40e6-109">使用 Azure 入口網站建立混合式連線。</span><span class="sxs-lookup"><span data-stu-id="d40e6-109">Create a hybrid connection, using the Azure portal.</span></span>
3. <span data-ttu-id="d40e6-110">撰寫伺服器主控台應用程式來接收訊息。</span><span class="sxs-lookup"><span data-stu-id="d40e6-110">Write a server console application to receive messages.</span></span>
4. <span data-ttu-id="d40e6-111">撰寫用戶端主控台應用程式來傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="d40e6-111">Write a client console application to send messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d40e6-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="d40e6-112">Prerequisites</span></span>

1. <span data-ttu-id="d40e6-113">[Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="d40e6-113">[Node.js](https://nodejs.org/en/).</span></span>
2. <span data-ttu-id="d40e6-114">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d40e6-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="d40e6-115">1.使用 Azure 入口網站建立命名空間</span><span class="sxs-lookup"><span data-stu-id="d40e6-115">1. Create a namespace using the Azure portal</span></span>

<span data-ttu-id="d40e6-116">如果您已經建立轉送命名空間，請跳至[使用 Azure 入口網站建立混合式連線](#2-create-a-hybrid-connection-using-the-azure-portal)一節。</span><span class="sxs-lookup"><span data-stu-id="d40e6-116">If you already have a Relay namespace created, jump to the [Create a hybrid connection using the Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-the-azure-portal"></a><span data-ttu-id="d40e6-117">2.使用 Azure 入口網站建立混合式連線</span><span class="sxs-lookup"><span data-stu-id="d40e6-117">2. Create a hybrid connection using the Azure portal</span></span>

<span data-ttu-id="d40e6-118">如果您已經建立混合式連線，請跳至[建立伺服器應用程式](#3-create-a-server-application-listener)一節。</span><span class="sxs-lookup"><span data-stu-id="d40e6-118">If you already have a hybrid connection created, jump to the [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="d40e6-119">3.建立伺服器應用程式 (接聽程式)</span><span class="sxs-lookup"><span data-stu-id="d40e6-119">3. Create a server application (listener)</span></span>

<span data-ttu-id="d40e6-120">為了接聽並接收來自轉送的訊息，我們會撰寫 Node.js 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d40e6-120">To listen and receive messages from the Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="d40e6-121">4.建立用戶端應用程式 (傳送者)</span><span class="sxs-lookup"><span data-stu-id="d40e6-121">4. Create a client application (sender)</span></span>

<span data-ttu-id="d40e6-122">為了傳送訊息到轉送，我們會撰寫 Node.js 主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="d40e6-122">To send messages to the Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-the-applications"></a><span data-ttu-id="d40e6-123">5.執行應用程式</span><span class="sxs-lookup"><span data-stu-id="d40e6-123">5. Run the applications</span></span>

1. <span data-ttu-id="d40e6-124">執行伺服器應用程式：從 Node.js 命令提示字元中，鍵入 `node listener.js`。</span><span class="sxs-lookup"><span data-stu-id="d40e6-124">Run the server application: from a Node.js command prompt type `node listener.js`.</span></span>
2. <span data-ttu-id="d40e6-125">執行用戶端應用程式：從 Node.js 命令提示字元中，鍵入 `node sender.js`，然後輸入一些文字。</span><span class="sxs-lookup"><span data-stu-id="d40e6-125">Run the client application: from a Node.js command prompt type `node sender.js`, and enter some text.</span></span>
3. <span data-ttu-id="d40e6-126">確定伺服器應用程式主控台有將用戶端應用程式中所輸入的文字輸出。</span><span class="sxs-lookup"><span data-stu-id="d40e6-126">Ensure that the server application console outputs the text that was entered in the client application.</span></span>

![執行應用程式](./media/relay-hybrid-connections-node-get-started/running-applications.png)

<span data-ttu-id="d40e6-128">恭喜您，您已經使用 Node.js 建立端對端混合式連線應用程式！</span><span class="sxs-lookup"><span data-stu-id="d40e6-128">Congratulations, you have created an end-to-end Hybrid Connections application using Node.js!</span></span>

## <a name="next-steps"></a><span data-ttu-id="d40e6-129">後續步驟：</span><span class="sxs-lookup"><span data-stu-id="d40e6-129">Next steps:</span></span>

* [<span data-ttu-id="d40e6-130">轉送常見問題集</span><span class="sxs-lookup"><span data-stu-id="d40e6-130">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="d40e6-131">建立命名空間</span><span class="sxs-lookup"><span data-stu-id="d40e6-131">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="d40e6-132">開始使用 .NET</span><span class="sxs-lookup"><span data-stu-id="d40e6-132">Get started with .NET</span></span>](relay-hybrid-connections-dotnet-get-started.md)
* [<span data-ttu-id="d40e6-133">開始使用 Node</span><span class="sxs-lookup"><span data-stu-id="d40e6-133">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

