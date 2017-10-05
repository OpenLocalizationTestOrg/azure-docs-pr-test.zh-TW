---
title: "如何在 Azure 入口網站中建立服務匯流排命名空間 | Microsoft Docs"
description: "使用 Azure 入口網站建立服務匯流排命名空間。"
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
ms.openlocfilehash: c8654ed547a9001e2e968d2a45d990a73ef27d3b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-service-bus-namespace-using-the-azure-portal"></a><span data-ttu-id="5a22d-103">使用 Azure 入口網站建立服務匯流排命名空間</span><span class="sxs-lookup"><span data-stu-id="5a22d-103">Create a Service Bus namespace using the Azure portal</span></span>

<span data-ttu-id="5a22d-104">命名空間是所有傳訊元件的範圍容器。</span><span class="sxs-lookup"><span data-stu-id="5a22d-104">A namespace is a scoping container for all messaging components.</span></span> <span data-ttu-id="5a22d-105">多個佇列和主題可以位於單一命名空間，而且命名空間通常會做為應用程式容器。</span><span class="sxs-lookup"><span data-stu-id="5a22d-105">Multiple queues and topics can reside within a single namespace, and namespaces often serve as application containers.</span></span> <span data-ttu-id="5a22d-106">有 2 個不同的方式可建立服務匯流排命名空間：</span><span class="sxs-lookup"><span data-stu-id="5a22d-106">There are two different ways to create a Service Bus namespace:</span></span>

1. <span data-ttu-id="5a22d-107">Azure 入口網站 (本文)</span><span class="sxs-lookup"><span data-stu-id="5a22d-107">Azure portal (this article)</span></span>
2. <span data-ttu-id="5a22d-108">[Resource Manager 範本][create-namespace-using-arm]</span><span class="sxs-lookup"><span data-stu-id="5a22d-108">[Resource Manager templates][create-namespace-using-arm]</span></span>

## <a name="create-a-namespace-in-the-azure-portal"></a><span data-ttu-id="5a22d-109">在 Azure 入口網站中建立命名空間</span><span class="sxs-lookup"><span data-stu-id="5a22d-109">Create a namespace in the Azure portal</span></span>

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

<span data-ttu-id="5a22d-110">恭喜！</span><span class="sxs-lookup"><span data-stu-id="5a22d-110">Congratulations!</span></span> <span data-ttu-id="5a22d-111">您現已建立服務匯流排訊息命名空間。</span><span class="sxs-lookup"><span data-stu-id="5a22d-111">You have now created a Service Bus Messaging namespace.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a22d-112">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5a22d-112">Next steps</span></span>

<span data-ttu-id="5a22d-113">查看 [GitHub 範例][github-samples]，其中會示範一些更進階的 Azure 服務匯流排傳訊功能。</span><span class="sxs-lookup"><span data-stu-id="5a22d-113">Check out our [GitHub samples][github-samples], which show some of the more advanced features of Azure Service Bus Messaging.</span></span>

[create-namespace-using-arm]: service-bus-resource-manager-overview.md
[github-samples]: https://github.com/Azure/azure-service-bus/tree/master/samples
