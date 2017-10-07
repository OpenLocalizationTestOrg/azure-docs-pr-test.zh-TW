---
title: "aaaHow toocreate hello Azure 入口網站中的服務匯流排命名空間 |Microsoft 文件"
description: "建立服務匯流排命名空間使用 hello Azure 入口網站。"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fbb10e62-b133-4851-9d27-40bd844db3ba
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: d8907e7e4a804056f6d66d5a177d9ace967ed2ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-hello-azure-portal"></a><span data-ttu-id="e91fe-103">建立服務匯流排命名空間使用 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="e91fe-103">Create a Service Bus namespace using hello Azure portal</span></span>

<span data-ttu-id="e91fe-104">命名空間是所有傳訊元件的範圍容器。</span><span class="sxs-lookup"><span data-stu-id="e91fe-104">A namespace is a scoping container for all messaging components.</span></span> <span data-ttu-id="e91fe-105">多個佇列和主題可以位於單一命名空間，而且命名空間通常會做為應用程式容器。</span><span class="sxs-lookup"><span data-stu-id="e91fe-105">Multiple queues and topics can reside within a single namespace, and namespaces often serve as application containers.</span></span> <span data-ttu-id="e91fe-106">有兩個不同的方式 toocreate 服務匯流排命名空間：</span><span class="sxs-lookup"><span data-stu-id="e91fe-106">There are two different ways toocreate a Service Bus namespace:</span></span>

1. <span data-ttu-id="e91fe-107">Azure 入口網站 (本文)</span><span class="sxs-lookup"><span data-stu-id="e91fe-107">Azure portal (this article)</span></span>
2. <span data-ttu-id="e91fe-108">[Resource Manager 範本][create-namespace-using-arm]</span><span class="sxs-lookup"><span data-stu-id="e91fe-108">[Resource Manager templates][create-namespace-using-arm]</span></span>

## <a name="create-a-namespace-in-hello-azure-portal"></a><span data-ttu-id="e91fe-109">在 hello Azure 入口網站中建立命名空間</span><span class="sxs-lookup"><span data-stu-id="e91fe-109">Create a namespace in hello Azure portal</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

<span data-ttu-id="e91fe-110">恭喜！</span><span class="sxs-lookup"><span data-stu-id="e91fe-110">Congratulations!</span></span> <span data-ttu-id="e91fe-111">您現已建立服務匯流排訊息命名空間。</span><span class="sxs-lookup"><span data-stu-id="e91fe-111">You have now created a Service Bus Messaging namespace.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e91fe-112">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e91fe-112">Next steps</span></span>

<span data-ttu-id="e91fe-113">請查看我們[GitHub 範例][github-samples]，示範一些更進階功能的 Azure Service Bus 訊息 hello。</span><span class="sxs-lookup"><span data-stu-id="e91fe-113">Check out our [GitHub samples][github-samples], which show some of hello more advanced features of Azure Service Bus Messaging.</span></span>

[create-namespace-using-arm]: service-bus-resource-manager-overview.md
[github-samples]: https://github.com/Azure/azure-service-bus/tree/master/samples
