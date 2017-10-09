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
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="b521e-103">開始使用轉送混合式連線</span><span class="sxs-lookup"><span data-stu-id="b521e-103">Get started with Relay Hybrid Connections</span></span>
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="b521e-104">本教學課程中介紹過[Azure 轉送混合式連線](relay-what-is-it.md#hybrid-connections)，並示範如何 toouse.NET toocreate 傳送用戶端應用程式訊息 tooa 對應接聽程式的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b521e-104">This tutorial provides an introduction too[Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how toouse .NET toocreate a client application that sends messages tooa corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="b521e-105">將會完成的工作</span><span class="sxs-lookup"><span data-stu-id="b521e-105">What will be accomplished</span></span>
<span data-ttu-id="b521e-106">混合式連線需要用戶端和伺服器元件，因為 hello 教學課程會建立兩個主控台應用程式。</span><span class="sxs-lookup"><span data-stu-id="b521e-106">Because Hybrid Connections requires both a client and a server component, hello tutorial creates two console applications.</span></span> <span data-ttu-id="b521e-107">Hello 步驟如下：</span><span class="sxs-lookup"><span data-stu-id="b521e-107">Here are hello steps:</span></span>

1. <span data-ttu-id="b521e-108">建立轉送的命名空間，使用 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b521e-108">Create a Relay namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="b521e-109">該命名空間，使用 hello Azure 入口網站中建立混合式連接。</span><span class="sxs-lookup"><span data-stu-id="b521e-109">Create a hybrid connection in that namespace, using hello Azure portal.</span></span>
3. <span data-ttu-id="b521e-110">寫入伺服器 （接聽程式） 主控台應用程式 tooreceive 訊息。</span><span class="sxs-lookup"><span data-stu-id="b521e-110">Write a server (listener) console application tooreceive messages.</span></span>
4. <span data-ttu-id="b521e-111">撰寫用戶端 （傳送者） 主控台應用程式 toosend 訊息。</span><span class="sxs-lookup"><span data-stu-id="b521e-111">Write a client (sender) console application toosend messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b521e-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="b521e-112">Prerequisites</span></span>

<span data-ttu-id="b521e-113">toocomplete 本教學課程中，您將需要下列必要條件 hello:</span><span class="sxs-lookup"><span data-stu-id="b521e-113">toocomplete this tutorial, you'll need hello following prerequisites:</span></span>

1. <span data-ttu-id="b521e-114">[Visual Studio 2015 或更新版本](http://www.visualstudio.com)。</span><span class="sxs-lookup"><span data-stu-id="b521e-114">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="b521e-115">在此教學課程中的 hello 範例會使用 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="b521e-115">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="b521e-116">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b521e-116">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="b521e-117">1.建立命名空間使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="b521e-117">1. Create a namespace using hello Azure portal</span></span>
<span data-ttu-id="b521e-118">如果您已經建立轉送命名空間，跳 toohello[建立使用 hello Azure 入口網站的混合式連接](#2-create-a-hybrid-connection-using-the-azure-portal)> 一節。</span><span class="sxs-lookup"><span data-stu-id="b521e-118">If you have already created a Relay namespace, jump toohello [Create a hybrid connection using hello Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a><span data-ttu-id="b521e-119">2.建立使用 hello Azure 入口網站的混合式連接</span><span class="sxs-lookup"><span data-stu-id="b521e-119">2. Create a hybrid connection using hello Azure portal</span></span>
<span data-ttu-id="b521e-120">如果您已經建立混合式連接，跳 toohello[建立伺服器應用程式](#3-create-a-server-application-listener)> 一節。</span><span class="sxs-lookup"><span data-stu-id="b521e-120">If you have already created a hybrid connection, jump toohello [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="b521e-121">3.建立伺服器應用程式 (接聽程式)</span><span class="sxs-lookup"><span data-stu-id="b521e-121">3. Create a server application (listener)</span></span>
<span data-ttu-id="b521e-122">toolisten 和接收訊息從 hello 轉送，我們會撰寫 C# 主控台應用程式使用 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="b521e-122">toolisten and receive messages from hello Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="b521e-123">4.建立用戶端應用程式 (傳送者)</span><span class="sxs-lookup"><span data-stu-id="b521e-123">4. Create a client application (sender)</span></span>
<span data-ttu-id="b521e-124">toosend 訊息 toohello 轉送，我們會撰寫 C# 主控台應用程式使用 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="b521e-124">toosend messages toohello Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-hello-applications"></a><span data-ttu-id="b521e-125">5.執行 hello 應用程式</span><span class="sxs-lookup"><span data-stu-id="b521e-125">5. Run hello applications</span></span>
1. <span data-ttu-id="b521e-126">執行 hello 伺服器應用程式。</span><span class="sxs-lookup"><span data-stu-id="b521e-126">Run hello server application.</span></span>
2. <span data-ttu-id="b521e-127">執行 hello 用戶端應用程式並輸入一些文字。</span><span class="sxs-lookup"><span data-stu-id="b521e-127">Run hello client application and enter some text.</span></span>
3. <span data-ttu-id="b521e-128">請確定 hello 伺服器應用程式主控台輸出的 hello 文字輸入 hello 用戶端應用程式中。</span><span class="sxs-lookup"><span data-stu-id="b521e-128">Ensure that hello server application console outputs hello text that was entered in hello client application.</span></span>

![執行應用程式](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

<span data-ttu-id="b521e-130">恭喜您，您已建立端對端混合式連線應用程式。</span><span class="sxs-lookup"><span data-stu-id="b521e-130">Congratulations, you have created an end-to-end Hybrid Connections application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b521e-131">後續步驟：</span><span class="sxs-lookup"><span data-stu-id="b521e-131">Next steps:</span></span>
* [<span data-ttu-id="b521e-132">轉送常見問題集</span><span class="sxs-lookup"><span data-stu-id="b521e-132">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="b521e-133">建立命名空間</span><span class="sxs-lookup"><span data-stu-id="b521e-133">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="b521e-134">開始使用 Node</span><span class="sxs-lookup"><span data-stu-id="b521e-134">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

